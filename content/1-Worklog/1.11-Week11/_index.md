---
title: "Week 11 Worklog"
date: 2026-06-29
weight: 11
chapter: false
pre: "  1.11.  "
---

### Week 11 Objectives:

This week, the system begins touching real data: the security member's OAuth flow is complete, and the backend member's Worker starts reading Gmail and calling OpenAI. My role shifts from "framework builder" to "first user" — running server-side end-to-end testing using command-line tools, and precisely in this role, I am the first to encounter the team's biggest incident of the week. In parallel, I write the most technically dense documentation chapter: Gmail OAuth integration.

* Test the server-side end-to-end OAuth flow: retrieve Cognito token via CLI, call the init endpoint, complete consent, verify data in DynamoDB.
* Test the complete pipeline with real emails: call `/check-gmail`, monitor SQS/Worker, verify the summarized results.
* Detect and coordinate the tracing of the Worker's `403 Forbidden` incident — reporting exact symptoms for the security member to handle.
* Monitor error queues: track the Dead-Letter Queue and CloudWatch alarms throughout the testing process.
* Write the entire "Gmail OAuth Integration" documentation chapter (parent section + child sections) based on the security member's incident notes.

---

### Tasks to be implemented this week:

| Day | Task Category | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Prepare server-side testing tools on Windows: get ID Token via `aws cognito-idp initiate-auth`, call API using `curl.exe` (do not use PowerShell's `curl` alias as it is `Invoke-WebRequest` with completely different syntax). <br> - Handle PowerShell swallowing quotes in inline JSON: switch to writing JSON to a file with `-Encoding ascii` and point to `file://`. | 29/06/2026 | 29/06/2026 | [https://docs.aws.amazon.com/cli/](https://docs.aws.amazon.com/cli/) |
| Tuesday | - Test OAuth flow: call `/auth/gmail/init` to receive the consent URL, complete consent on the browser with an account in Test users, confirm the callback page reports success. <br>- Verify the record in the `inboxiq-gmail-connections` table: must have accessToken, refreshToken, gmailAddress, expiresAt. | 30/06/2026 | 30/06/2026 | Internal team |
| Wednesday | - Test the complete pipeline: call `/check-gmail`, receive `202 Accepted` with jobId. But after waiting, the `inboxiq-email-summaries` table is empty — no results. <br> - Systematically gather symptoms: Lambda metric reports `Errors = 0` but SQS's `Messages Deleted` is 0, messages are retried every 5 minutes perfectly matching the visibility timeout cycle. Provide a full report to the backend and security members. | 01/07/2026 | 01/07/2026 | Internal team |
| Thursday | - Support tracing: provide the DynamoDB record for the security member to cross-reference — the `scope` field missing `gmail.readonly` in the record I extracted was the conclusive clue (granular permissions). <br> - Encountered a secondary error when extracting data: AWS CLI on Windows cannot print Vietnamese characters (`charmap codec error`) even with `chcp 65001` — switched to viewing via the DynamoDB Console. | 02/07/2026 | 02/07/2026 | Internal team |
| Friday | - Retest after the security member's fix (re-consent to acquire sufficient scopes): the pipeline runs completely, real emails are summarized with the correct summary/category/priority/action structure along with TTL. <br> - Monitor DLQ during testing: error messages from the 403 batch were pushed to the Dead-Letter Queue exactly as designed (after 3 retries), the `inboxiq-dlq-messages` alarm switched to "In alarm" — confirming the alert mechanism works. Purge DLQ after the incident is resolved. | 03/07/2026 | 03/07/2026 | [https://docs.aws.amazon.com/sqs/](https://docs.aws.amazon.com/sqs/) |
| Saturday | - Write the "Gmail OAuth Integration" documentation chapter: parent section (why a separate section is needed, flow diagram, the key point of init having auth / callback lacking auth) and a child section on Lambda + Layer (from the security member's notes). | 04/07/2026 | 04/07/2026 | Internal team |
| Sunday | - Write the "End-to-end testing and troubleshooting" child section: the entire CLI testing process, the granular permissions incident, and a summary table of other errors encountered during the week. <br> - Check Billing + OpenAI dashboard: AWS cost remains 0, OpenAI cost is negligible. Write the weekly report. | 05/07/2026 | 05/07/2026 | InboxIQ project internal |

---

### Achieved Results for Week 11:

#### 1. The "first user" role — and the value of accurate symptom reporting

The `403 Forbidden` incident of the week was the biggest lesson on the testing role. I was not the one who found the root cause (that is the security member's expertise), but the one who **detected** and — more importantly — **reported symptoms accurately enough for others to trace**: not just saying "there are no results," but pointing out the crucial triad of facts: Lambda `Errors = 0` (Worker did not crash — it caught the error internally), `Messages Deleted = 0` (messages were not completely processed), and a 5-minute retry cycle matching the visibility timeout (SQS is redelivering). The exact DynamoDB record I extracted — with the `scope` field missing `gmail.readonly` — became the conclusive clue.

Career lesson: a good bug report is half the solution. "The system is not running" is a complaint; "The Worker doesn't crash but messages aren't deleted from the queue, and here is the actual data" is an input for diagnosis.

#### 2. The testing toolkit on Windows — traps not found in any documentation

Testing APIs on PowerShell taught me the three most time-consuming environmental traps: `curl` on PowerShell is an alias for `Invoke-WebRequest` (completely different syntax, must explicitly type `curl.exe`); inline JSON parameters swallow quotes (solution: write to a file with `-Encoding ascii` and point to `file://`); and the Windows version of the AWS CLI cannot print Vietnamese (`charmap codec error`) regardless of `chcp 65001` — data with diacritics must be viewed via the DynamoDB Console. All three were recorded in an "environmental notes" section in the documentation so successors won't waste time like I did.

#### 3. Confirming the fault tolerance mechanism works as designed — via a real incident

The 403 incident inadvertently became a practical combat test for the entire fault tolerance mechanism built by the backend member: error messages were retried exactly 3 times then moved to the Dead-Letter Queue instead of being stuck forever in the main queue, and the `inboxiq-dlq-messages` alarm switched to "In alarm" status right on time — meaning if this were a production environment, the operations team would have been alerted. There are few ways to confirm a fault-tolerant design more convincingly than a real incident playing out exactly according to the anticipated scenario. After the incident was resolved, I purged the DLQ and noted tracking the alarm as it returned to the OK state.

#### 4. The OAuth documentation chapter — written while the event is still fresh

The "Gmail OAuth Integration" chapter was completed in the very week the incident occurred, with a troubleshooting section detailed down to every metric — something impossible to achieve if written from memory a month later. The "record in the week" convention established last week proved effective right on time: the raw notes from the security member (cause, solution) plus my testing data (symptoms, metrics, records) were combined into a complete documentation section capturing both perspectives.

---

### Week 11 Results Evaluation:

* The complete pipeline with real emails was successfully tested after the incident — including verification of the correct data structure and TTL mechanism.
* Played the role of detecting and providing crucial data points for the team's biggest incident of the week.
* The fault tolerance mechanism (DLQ, alarms) was confirmed to work exactly as designed through a real incident.
* The Gmail OAuth documentation chapter was completed with high-quality troubleshooting content thanks to being written while the event was still fresh.

---

### Difficulties Encountered:

* Three Windows/PowerShell environmental traps (curl alias, JSON escaping, charmap codec) consumed significant time before real testing could begin.
* Role boundaries during the 403 incident were initially unclear: I detected it but lacked the OAuth expertise to trace it, having to learn how to effectively "hand over symptoms" instead of trying to fix it myself or just giving a generic report.
* Writing technical documentation from someone else's raw notes requires multiple rounds of questioning to avoid misinterpreting the technical nature.

---

### Solutions and Best Practices Derived:

* Standardize a "bug report template" for testing: symptoms, relevant metrics, extracted data, reproduction steps — to be applied to all future incidents.
* Record all environmental traps in a shared "operational notes" section, separated from the main technical content.
* When writing documentation based on others' notes, send the draft to that exact person for review before finalizing — the one who fixed the bug is the only one who can confirm if the technical explanation is right or wrong.

---

### Directions for Next Week:

* Conduct end-to-end testing on real devices with the whole team when the Flutter app is integrated into the system — expected to be the week with the most integration incidents.
* Write the Flutter documentation chapter and the resource cleanup chapter.
* Compile project-wide cost data and a service lookup table for the final report.