---
title: "Week 12 Worklog"
date: 2026-07-06
weight: 12
chapter: false
pre: "  1.12.  "
---

### Week 12 Objectives:

In the final week of the project, while the system entered its final integration phase and other members focused their energy on debugging, I concentrated my efforts on packaging: transforming three weeks of team effort into a comprehensive Hugo report that allows any external reader to fully understand our journey. My three major tasks included: writing the complete Flutter chapter (closely following the live, hot integration incidents occurring throughout the week), writing the resource cleanup chapter, and synthesizing the "intellectual backbone" of the report — the service lookup table accompanied by actual cost figures.

* Participate in end-to-end integration testing sessions in a logging role: capturing original evidence for each incident (logs, Console screenshots) to serve the documentation.
* Write the entire Flutter chapter: the parent section and all child sections (setup, OAuth deep linking, WebSocket testing & troubleshooting).
* Write the bilingual resource cleanup chapter: a step-by-step guide distinguishing between in-stack and out-of-stack resources.
* Review all utilized services to establish a lookup table (service – role – reason for choice – risks) — verifying the actual status of each resource instead of relying on outdated documentation.
* Finalize project-wide cost metrics from the Billing Dashboard and OpenAI usage.

---

### Tasks to be implemented this week:

| Day | Task Category | Start Date | End Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Attend the first integration testing session in a logging role: capturing screenshots of the "WebSocket not ready" symptom and Forbidden logs — serving as original evidence for the subsequent troubleshooting section. | 06/07/2026 | 06/07/2026 | Internal team |
| Tuesday | - Follow the backend member's tracing process, capturing evidence at each milestone: the "Log group does not exist" alert, and the Deployment history showing only the old version. <br> - Document raw incident notes using the 4-part framework within the same day. | 07/07/2026 | 07/07/2026 | Internal team |
| Wednesday | - Write the parent section of the Flutter chapter: flow diagram from button click to results, the key point of "push via WebSocket instead of REST polling", and the cost paid in terms of complexity. <br> - Write the environment setup and app architecture child section based on the Flutter member's notes. | 08/07/2026 | 08/07/2026 | Internal team |
| Thursday | - Record the 410 Gone incident: capturing Worker logs (GoneException, httpStatusCode 410) and the backend member's three-source timestamp cross-reference table — material for the most valuable troubleshooting section in the chapter. <br> - Write the client-side OAuth deep linking child section (the Chrome blocking redirect incident from the perspectives of both Flutter and security members). | 09/07/2026 | 09/07/2026 | Internal team |
| Friday | - System runs fully end-to-end — receive the complete flow image set from the Flutter member and embed them into the documentation. <br> - Write the "End-to-end testing and WebSocket troubleshooting" child section: 4 major incidents following the symptom → cause → solution → lesson framework. | 10/07/2026 | 10/07/2026 | Internal team |
| Saturday | - Write the bilingual Vietnamese/English "Resource Cleanup" chapter: `sam delete` for the main stack, separate deletion for Cognito/Secrets (both OpenAI and Google secrets), S3 artifact bucket, and leftover CloudWatch Logs — accompanied by placeholder image locations for "before deletion". <br> - Clearly state the context: resources will remain intact until the grading period concludes, this chapter serves as a post-grading execution guide. | 11/07/2026 | 11/07/2026 | [https://docs.aws.amazon.com/serverless-application-model/](https://docs.aws.amazon.com/serverless-application-model/) |
| Sunday | - Review the entire system to compile the service lookup table: opening each resource directly on the Console to verify its true state — discovering that the `inboxiq-processing-jobs` table was recently declared in the template but has no data-writing code yet. <br> - Finalize cost metrics: AWS remains within Free Tier, OpenAI cost is negligible. Write the final weekly report and cross-review the entire report. | 12/07/2026 | 12/07/2026 | InboxIQ project internal |

---

### Achieved Results for Week 12:

#### 1. The role of "historian" during debug week — original evidence is worth more than recollection

The team's most intense debugging week turned out to be the most harvest-rich week for the documentation area. By being present at the testing sessions in a logging capacity, I captured original evidence at the exact moments they occurred: the red "Log group does not exist" alert (proof that the request never touched Lambda), the Deployment history before and after the fix, and the complete GoneException log with status code 410. These screenshots cannot be recreated after an incident is resolved — if you want them, you must capture them live. As a result, the troubleshooting section of the Flutter chapter possesses the reliability of an on-scene report rather than a retold story.

#### 2. The Flutter chapter — turning two debugging stories into two universal lessons

Rewriting two major incidents (unpublished route, dead connectionId) from the logs of two team members taught me a core skill of a technical writer: separating the **universal lesson** from the **specific details**. "The whoami route returning Forbidden" is a project-specific detail; "CloudFormation successfully creating a route does not equate to the route being published to a stage" is a lesson every API Gateway user needs. Each troubleshooting entry concludes with a lesson written at a universal layer — that is the part grading panels and future readers can truly take away.

#### 3. The cleanup chapter — seemingly simple, yet requiring many editorial decisions

The "Resource Cleanup" chapter raised a series of non-obvious editorial questions: what tense should be used when resources cannot be deleted yet (the system must stay alive until grading ends)? The solution: write it as a step-by-step guide with "state before deletion" illustration placeholders, clearly noting the timeline context. What should be listed? It had to cover resources **outside** the SAM stack (manually created Cognito, both OpenAI and Google secrets, the S3 artifact bucket automatically generated by SAM CLI) — things that `sam delete` won't touch and that do not appear on the architecture diagram, yet silently persist in the account. The English version was translated in parallel as soon as the Vietnamese version was finalized, preventing content divergence between the two languages.

#### 4. The service lookup table — and the principle of "verifying directly on the Console"

The final and most rigorous task: auditing every service in the architecture, opening them directly on the Console to verify their true state instead of trusting the documentation from previous weeks. This principle immediately yielded results: I discovered that the `inboxiq-processing-jobs` table only existed in the SAM template, **with no lines of code actually writing data into it** — presenting it in the report as an active feature would have resulted in a heavy penalty during deep-dive Q&A. The actual status of each resource (in use / newly declared / backup) was transparently documented.

Cost metrics were finalized: all AWS services remained within the Free Tier throughout the three weeks of development; OpenAI costs (GPT-4o-mini) were negligible compared to the credit limit — accompanied by notes on "hidden costs" we proactively bypassed from day one (caching secrets to reduce Secrets Manager calls, capping at 10 emails/pull to block OpenAI cost spikes).

---

### Week 12 Results Evaluation:

* Complete Hugo report package: architecture chapter, OAuth, Flutter (with troubleshooting at an "on-scene report" level), bilingual cleanup, and costs.
* Service lookup table with statuses verified directly on the Console — including the honest discovery of the unused table.
* All incident evidence systematically preserved, ready for the report defense.
* Three-week cost figures finalized with a clear conclusion: within Free Tier + negligible OpenAI costs.

---

### Difficulties Encountered:

* Writing documentation while incidents are actively unfolding means the content changes continuously — some sections had to be rewritten twice because the team's initial diagnosis turned out not to be the root cause.
* Balancing technical granular detail (sufficient for reproduction) and report length (so that graders can actually read through) is an editorial problem with no absolute answer.
* Honestly reporting incomplete items (unused table, secrets needing rotation, maintenance backlogs) required total team alignment — fortunately, a culture of transparency had been agreed upon from the start.

---

### Solutions and Best Practices Derived:

* For troubleshooting documentation, capture evidence at the exact moment of the incident — there is no second chance after the bug is fixed.
* Conclude each incident entry with a lesson written at a universal layer, separated from project details — that is the enduring value of documentation.
* Before finalizing the report, verify the true status of every resource directly on the Console; do not trust any notes older than one week.
* Reporting limitations honestly (along with remediation plans) is more convincing than a "perfect" report — and much safer when facing deep-dive questioning.

---

### Directions Post-Project:

* Finish taking the remaining illustration screenshots for the cleanup chapter (Console pages "before deletion") and support the team in executing the actual cleanup after the grading period.
* Update the report one final time with Billing screenshots close to the submission date so that cost figures reflect the full project lifecycle.
* Synthesize the collection of "universal lessons" from the troubleshooting entries into a dedicated standalone page — our team's intellectual legacy for future cohorts.