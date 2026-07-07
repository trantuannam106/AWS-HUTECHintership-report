---
title: "Week 7 Worklog"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Key Objectives for Week 7:

- Grasp the overall picture of the Amazon CloudWatch monitoring service.
- Evaluate the importance of CloudWatch in managing and monitoring the "health" of resources and applications in the AWS environment.
- Directly interact with CloudWatch Metrics to measure and assess system performance.
- Familiarize with advanced syntaxes: Search Expressions, Math Expressions, and Dynamic Labels.
- Analyze activity logs through CloudWatch Logs and the advanced query tool, CloudWatch Logs Insights.
- Set up Metric Filters to extract data directly from log data.
- Install an automated alerting system (CloudWatch Alarms) for early detection and troubleshooting.
- Design CloudWatch Dashboards to centralize and visualize monitoring metrics.
- Perform the Cleanup process to release resources after the lab.
- Hone and upgrade cloud infrastructure operation and monitoring skills.

---

### Detailed Action Plan:

| Day | Task Details | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Research the overview document of the Amazon CloudWatch lab <br> - Analyze the role and monitoring architecture of CloudWatch <br> - Configure and prepare the AWS account environment | 06/01/2026 | 06/01/2026 | https://000008.awsstudygroup.com/1-introduction/ |
| Tuesday | - Explore the functions of CloudWatch Metrics <br> - Read and analyze existing resource metrics <br> - Practice data filtering commands with Search Expressions | 06/02/2026 | 06/02/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| Wednesday | - Apply Math Expressions to perform calculations on metrics <br> - Deploy Dynamic Labels for clearer chart displays <br> - Fine-tune visual graphs for Metrics | 06/03/2026 | 06/03/2026 | https://000008.awsstudygroup.com/3-cloud-watch-metric/ |
| Thursday | - Operate the CloudWatch Logs storage system <br> - Write log query syntaxes via Logs Insights <br> - Configure Metric Filters to count the number of errors from Logs | 06/04/2026 | 06/04/2026 | https://000008.awsstudygroup.com/4-cloud-watch-logs/ |
| Friday | - Initialize CloudWatch Alarms rule sets <br> - Integrate Amazon SNS service to receive automated notifications (via email) <br> - Simulate incidents to test the triggering capability of Alarms | 06/05/2026 | 06/05/2026 | https://000008.awsstudygroup.com/5-cloud-watch-alarm/ |
| Saturday | - Build a professional CloudWatch Dashboards interface <br> - Integrate Metrics charts and Alarms statuses into a single view <br> - Observe real-time fluctuating data flows | 06/06/2026 | 06/06/2026 | https://000008.awsstudygroup.com/6-cloud-watch-dashboard/ |
| Sunday | - Review the entire configured system <br> - Proceed to delete resources (Cleanup) to avoid cost risks <br> - Summarize experiences and complete the weekly report | 06/07/2026 | 06/07/2026 | https://000008.awsstudygroup.com/7-clean-up/ |

---

### Summary of Achieved Results:

#### Knowledge Base

**The Nature of Amazon CloudWatch**
- Define CloudWatch as a "control center" for comprehensive observation of the AWS ecosystem.
- Understand the data collection flow: from fetching metrics to storing logs.
- Deeply understand why proactive monitoring is a vital factor in ensuring application uptime.

**CloudWatch Metrics System**
- Proficient in searching and extracting performance measurement metrics.
- Know how to use the Search Expressions tool to rapidly scan large amounts of data.
- Successfully apply Math Expressions to aggregate or calculate derivative metrics.
- Understand how to apply smart labeling (Dynamic Labels) so graphs automatically update display names in a user-friendly way.

**Managing CloudWatch Logs**
- Understand the grouping mechanism and log lifecycle (Log Groups and Log Streams).
- Know how to use specific query syntaxes in Logs Insights to dig for the root cause of errors.
- Master the technique of using Metric Filters to turn inanimate text strings in logs into actionable, alarm-triggering numbers (e.g., counting the keyword "ERROR").

**CloudWatch Alarms Mechanism**
- Clearly understand the 3 states of an alarm: *OK, ALARM, INSUFFICIENT_DATA*.
- Master how to establish activation thresholds based on static data or anomalous data (Anomaly Detection).
- Grasp the process of connecting with Amazon SNS to route notifications to the operations team.

**Visualization with CloudWatch Dashboards**
- Develop a mindset on how to logically arrange Widgets on the Dashboard workspace.
- Understand that grouping Metrics and Alarms in one place saves time when diagnosing system errors.

---

#### Visual Practical Implementation

**Module 1 — Introduction**
- Successfully accessed the Amazon CloudWatch console.
- Familiarized with the navigation menu and checked the prerequisites of the lab.
- Booted up a safe resource testing environment.

**Module 2 — Deploying CloudWatch Metrics**
- Navigated to the Metrics interface of running AWS services.
- Successfully wrote and executed Search Expressions syntaxes.
- Applied mathematical functions (Math Expressions) to line charts.
- Configured and verified display name changes via Dynamic Labels.

**Module 3 — Operating CloudWatch Logs**
- Successfully initialized new Log Groups.
- Poured sample data in and proceeded to run filter commands using Logs Insights.
- Set up Metric Filters to recognize specific keywords and cross-checked the results.

**Module 4 — Configuring CloudWatch Alarms**
- Created a new alert rule based on CPU metrics or the filtered error count.
- Set up an SNS Topic and added an email subscription to receive messages.
- Triggered an event to force the metric over the threshold and confirmed the alarm email was sent to the inbox.

**Module 5 — Designing CloudWatch Dashboards**
- Created a new workspace (Dashboard).
- Added bar chart and line chart Widgets representing Metrics.
- Attached Alarm status Widgets to monitor the red/green alert conditions.

**Module 6 — Cleanup Resources**
- Accessed each module: Alarms, Dashboards, and Logs to clean up the created items.
- Ensured the environment returned to a clean state.
- Completed the review to ensure no background services were running to limit incurred bills.

---

### Challenges and Obstacles Faced:

- Felt overwhelmed in the initial stage due to not clearly distinguishing the functions between Metrics (measurement data), Logs (text journals), and Metric Filters (the bridge between the two).
- The syntax of Search Expressions and Math Expressions is quite specific and easy to write incorrectly if the documentation is not read carefully.
- The Logs Insights query language is quite similar to SQL but has many differences; it takes time to get used to functions like `stats` and `parse`.
- The process of configuring the SNS notification flow was sometimes interrupted due to forgetting to click "Confirm subscription" in the email.

---

### Solutions and Lessons Learned:

- Delve deeper into standard documentation (AWS Documentation) in parallel with reading the lab guide.
- Note down sample Query syntaxes to reuse for subsequent configurations.
- Always carefully check the inbox and spam folder to ensure the SNS endpoint is verified before proceeding to test the Alarms flow.
- Proactively search for practical videos or AWS Use-case articles to clearly understand the platform's data transformation logic.

---

### Plan and Roadmap for Next Week:

- Move on to the topic of identity management with AWS Identity and Access Management (IAM).
- Directly manipulate the IAM lifecycle including: Creating Users, attaching Groups, and allocating permission Policies.
- Delve into multi-factor authentication (MFA) to strengthen AWS account security.
- Analyze and design an optimal least privilege authorization model in a cloud environment.
- Prepare screenshot proofs and important notes in advance to attach to next week's practical report.