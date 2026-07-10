---
title: "Proposal"
date: 2026-07-04
weight: 2
chapter: false
pre: "  2.  "
---
# InboxIQ

## AI-powered email triage on Serverless AWS

### 1. Project Overview

InboxIQ is a smart virtual assistant designed to solve email overload for modern users (students, office workers). The mobile application (Flutter) securely connects to Gmail via the OAuth 2.0 standard, utilizing an artificial intelligence model (GPT-4o-mini) to summarize content, categorize emails (work / personal / promo / notification), and assess the priority level of each email. The results are then pushed back to the app in real-time via WebSockets. The entire backend operates on AWS's Serverless Event-Driven architecture (Region `us-east-1`), built within the framework of the First Cloud AI Journey (FCAJ) 2026 internship program.

### 2. Objectives

* Build a complete end-to-end system: from a mobile application on real devices, through a serverless backend, to external AI/Gmail services — validated with real email data.
* Apply an asynchronous architecture (Producer/Worker via SQS) to provide immediate responses to users while heavy processing runs in the background, combined with WebSocket push instead of polling.
* Ensure multi-layer security: user authentication via Cognito (JWT), Gmail read authorization via OAuth 2.0 with minimum scopes, all credentials stored in Secrets Manager, and IAM Roles following the Least Privilege principle.
* Operate the entire project within the AWS Free Tier limits, strictly controlling AI costs using hard limits.
* Manage infrastructure entirely using Infrastructure as Code (AWS SAM) and document the complete process — including incidents and lessons learned — into a bilingual Hugo report.

### 3. Problem Statement

Modern users typically receive 50–100 emails daily, consuming significant time filtering information and making it easy to miss important emails. Existing solutions are either manual (keyword filters, manual labels) or expensive third-party AI services that pose privacy risks, as email data is centrally processed beyond the user's control.

The technical challenge consists of three main issues: (1) accessing the user's mailbox securely with explicit consent (OAuth, without storing Gmail passwords); (2) handling time-consuming AI processing (from seconds to tens of seconds) without blocking the mobile app; (3) returning results to the correct user, in the correct session, in real-time.

### 4. Solution Architecture

The system is organized into 5 separate functional layers based on the Serverless Event-Driven model:

```
LAYER 1 · USER       → Users, Mobile App (Flutter)
LAYER 2 · BACKEND    → Cognito, API Gateway (REST + WebSocket), Lambda (Producer + Worker + Authorizer)
LAYER 3 · WORKFLOW   → SQS (Main Queue + Dead-Letter Queue), EventBridge Scheduler (optional)
LAYER 4 · STORAGE    → DynamoDB (4 tables, TTL auto-cleanup), Secrets Manager
LAYER 5 · MONITORING → CloudWatch, X-Ray, IAM Role
EXTERNAL SERVICES    → Gmail API, OpenAI API (outside AWS Cloud)

```

**Main processing flow:** The user clicks "Check Gmail" on the app → REST API (JWT authentication) → Lambda Producer packages the request with the `connectionId` and pushes it to SQS, returning `202 Accepted` immediately → Lambda Worker consumes the message, retrieves the Gmail token from DynamoDB (auto-refreshing if expired), calls the Gmail API to fetch unread emails, and calls GPT-4o-mini for parallel summarization → saves the results to DynamoDB (with a 30-day TTL) → pushes the results back to the app via API Gateway WebSocket.

**AWS Services Used:**

* **Amazon Cognito:** Identity management, user authentication, and JWT issuance.
* **Amazon API Gateway:** REST endpoint for synchronous tasks; WebSocket endpoint (`$connect`, `$disconnect`, `whoami` routes) for a two-way real-time channel, authenticated by a Lambda Authorizer.
* **AWS Lambda:** Independent processing functions — Authorizer, Producer, Worker, WebSocket lifecycle functions, and OAuth flows (init/callback), sharing common logic via Lambda Layers.
* **Amazon SQS:** `inboxiq-main` queue (Partial Batch Response — only retrying failed messages) and a Dead-Letter Queue isolating failed messages after 3 retries, accompanied by CloudWatch Alarms for alerts.
* **Amazon DynamoDB:** 4 specialized tables (Gmail connections, email summaries, WebSocket sessions, processing jobs) in On-Demand mode, using TTL for data lifecycle management.
* **AWS Secrets Manager:** Securely stores the OpenAI API key and Google OAuth Client Secret, read with caching at the Lambda global scope.
* **Amazon EventBridge Scheduler** (optional): Schedules periodic email checks every 30 minutes.
* **CloudWatch & X-Ray:** End-to-end logging, metrics, alarms, and tracing.

Due to the program's account limitations regarding Amazon Bedrock access, the solution opted for the OpenAI API, designed to abstract the AI provider so it can easily be migrated to Bedrock in the future.

### 5. Timeline

The project is implemented over 3 weeks with 4 members, assigned to specialized areas (backend/architecture, Flutter, OAuth/security, documentation/testing/costing):

* **Week 1 — Foundation:** Finalize architecture and assignments; set up the storage layer (DynamoDB, SQS + DLQ) and identity layer (Cognito, IAM Roles, Secrets Manager); write Lambda Producer/Worker, integrate OpenAI; initialize the Google Cloud project and OAuth consent screen; set up the Hugo documentation repo, and establish cost monitoring discipline.
* **Week 2 — Core Integration:** Complete the Gmail OAuth flow (Lambda init/callback, Lambda Layer for token refresh); deploy API Gateway WebSocket with Authorizer and `whoami` route; integrate real Gmail into the Worker; build the Flutter client side (Cognito auth, OAuth deep links, WebSocket service); test the pipeline with real emails.
* **Week 3 — Final Integration and Polish:** End-to-end testing on real Android devices, handling integration issues; optimize the Worker (parallel processing, element-level fault tolerance); finalize the Material 3 UI; conduct a security review; compile documentation, cost metrics, and resource cleanup guides.

### 6. Budget

The infrastructure is designed using the On-Demand model to fully leverage the AWS Free Tier:

| Category | Estimated Monthly Cost | Notes |
| --- | --- | --- |
| AWS Lambda | $0.00 | Within the 1 million requests/month limit |
| Amazon SQS & API Gateway | ~$0.00 | MVP request volume is well below the Free Tier limit |
| Amazon DynamoDB | $0.00 | On-Demand mode, small data footprint |
| Secrets Manager, CloudWatch, X-Ray | ~$0.00 | Trial usage tier; secret caching reduces API calls |
| OpenAI API (GPT-4o-mini) | ~$1.00 – $2.00 | Test volume of 50–100 emails/day; capped at 10 emails/call |

Financial risk control mechanisms: AWS Budgets alerts via email at specific cost milestones; a hard limit of **$5.00/month** on the OpenAI Platform; restricting `maxResults = 10` emails per processing run to prevent sudden cost spikes when a mailbox has too many unread emails.

### 7. Risks

**Risk Matrix:**

| Risk | Impact | Probability |
| --- | --- | --- |
| Gmail OAuth token expires or lacks scopes (user doesn't grant full permissions on the consent screen) | High | Medium |
| WebSocket connection drops silently, preventing results from reaching the app | High | Medium |
| Throttling from OpenAI or Secrets Manager during bursts of calls | Medium | Low |
| AWS/OpenAI costs spiraling out of control | High | Low |
| App can only be used with accounts on the Test users list (consent screen in Testing mode) | Medium | Certain (known limitation) |

**Mitigation Strategies:**

* **Gmail Token:** Store token state in DynamoDB, check validity before each call, auto-refresh via a shared Lambda Layer; verify the actual `scope` field received in the token response instead of assuming the consent flow was fully approved.
* **WebSocket:** The client verifies the `connectionId` at the point of use (not trusting cached values) and auto-reconnects when a drop is detected; on the Worker side, wrap the push call in its own error handling so a push failure doesn't crash the entire processing batch.
* **Throttling:** Cache API keys at the Lambda global scope; process emails in parallel with element-level fault tolerance (one failed email won't crash the batch); use SQS Partial Batch Response to retry only the specific failed messages.
* **Costs:** Multiple AWS Budgets alert milestones; OpenAI hard limits; cap on the number of emails per processing run; weekly review of the Billing Dashboard.
* **Test users limitation:** Accept this as the project scope (the Google verification process for Gmail scopes exceeds the internship timeframe), document it clearly in the Limitations section of the report along with the process for adding test accounts when a demo is needed.