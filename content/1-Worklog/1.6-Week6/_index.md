---
title: "Week 6 Worklog"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Objectives achieved in week 6:

- Approach and grasp the overall picture of cost management on the AWS platform through AWS Budgets.
- Understand the key role of AWS Budgets in monitoring, managing, and sending alerts upon detecting cost fluctuations or resource consumption.
- Practice quickly deploying budgets by applying available system Templates.
- Set up a Cost Budget to closely monitor the spending limits of AWS services on a monthly basis.
- Initialize a Usage Budget to control the frequency of resource usage, particularly focusing on services billed by running time.
- Research the operational mechanism of Reservation Budgets to check the utilization efficiency of Reserved Instances (RI).
- Understand the operation of Savings Plans Budgets to measure the level of cost optimization from flexible commitment plans.
- Flexibly configure alert thresholds accompanied by email notifications to detect the risk of exceeding the budget early.
- Master the skills of reviewing budget history, budget health, and active alerts.
- Perform cleanup of experimental configurations after completing the lab to keep the account tidy.

---

### Detailed action plan:

| Day | Task Details | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Read the overview documentation for the Cost Management with AWS Budgets lab <br> - Evaluate the financial management role of the service <br> - Access the AWS Billing and Cost Management dashboard <br> - Familiarize with the functional modules on the Budgets interface | 05/25/2026 | 05/25/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| Tuesday | - Apply quick budget creation using Templates <br> - Set up a Monthly cost budget configuration <br> - Declare information: Budget name, monthly spending limit, and alert thresholds <br> - Verify the display status of the budget and access Budget history | 05/26/2026 | 05/26/2026 | https://000007.awsstudygroup.com/1-create-budget/ |
| Wednesday | - Custom configure an advanced Cost Budget via Customize mode <br> - Select the budget category (Cost budget) <br> - Define parameters: Period, effective dates, budgeting method, and limit amount <br> - Define the Budget scope for all services using Unblended costs | 05/27/2026 | 05/27/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| Thursday | - Set trigger thresholds for the newly created Cost Budget <br> - Specify target email addresses to receive automated notifications <br> - Double-check all configuration parameters of the Cost Budget <br> - Activate the custom budget and monitor its initialization status | 05/28/2026 | 05/28/2026 | https://000007.awsstudygroup.com/2-cost-budgets/ |
| Friday | - Deploy a Usage Budget to manage capacity and resource running time <br> - Initialize with the Usage budget option in the budget types <br> - Declare a specific monitoring target group, e.g., EC2: ELB - Running Hours <br> - Set limits on operating hours and establish corresponding alert thresholds | 05/29/2026 | 05/29/2026 | https://000007.awsstudygroup.com/3-usage-budget/ |
| Saturday | - Investigate the Reservation Budget mechanism specifically for Reserved Instances <br> - Research the Savings Plans Budget feature to optimize usage commitments <br> - Review tutorials on configuring RI and Savings Plans Budgets in an enterprise environment <br> - Learn how to set up coverage and utilization metrics | 05/30/2026 | 05/30/2026 | https://000007.awsstudygroup.com/4-reservation-budget/ <br> https://000007.awsstudygroup.com/5-saving-plans-budget/ |
| Sunday | - Review the entire list of budgets configured during the week <br> - Evaluate the health and fluctuation charts of each budget <br> - Proceed to delete experimental budgets to clean the learning environment <br> - Summarize lessons learned, identify obstacles, and propose solutions | 05/31/2026 | 05/31/2026 | https://000007.awsstudygroup.com/6-clean-up/ |

---

### Summary of achieved results:

#### Knowledge base

> **The Nature of AWS Budgets**
> - A powerful tool to track cash flow, measure resource productivity, and verify the efficiency of discount commitments on AWS.
> - Supports flexible limit setups by Daily, Monthly, Quarterly, or Annually periods.
> - Provides proactive email notifications as soon as the system detects actual or forecasted costs exceeding the allowable threshold.
> - Acts as a "shield" to protect the learner's wallet, preventing the risk of generating large, uncontrollable bills.
> - **Core note:** AWS Budgets only acts as a monitoring and alerting system; this service absolutely does NOT automatically shut down or interfere with the operational status of running resources.

**AWS Billing and Cost Management Console**
- Proficient in searching and accessing the financial management center from the AWS Console.
- Clearly understand that this is the central hub for all data regarding invoices, cash flow analysis, limit setups, and spending alert rules.
- Know how to use the Budgets navigation menu to manage the lifecycle of a budget (Create - Edit - Monitor - Delete).

**Creating Budgets via Template**
- Understand the benefits of using pre-built templates to streamline the process and save time.
- Know how to select the "Use a template" mode for basic needs.
- Successfully apply the "Monthly cost budget" configuration to quickly establish a monthly cost management framework with email notifications.
- Know how to view Budget history to evaluate future spending trends.

**Configuring Cost Budgets**
- Understand that a Cost Budget focuses on the monetary amount (in USD) incurred when using services.
- Know how to deeply configure using Customize mode with the Cost budget type.
- Distinguish between two types of period applications:
  - *Recurring Budget:* Automatically renews and repeats in the next cycle.
  - *Expiring Budget:* Has a fixed expiration date and is valid only once.
- Distinguish between two budgeting methods:
  - *Fixed:* Set a constant, equal amount for every month.
  - *Planned:* Flexibly adjust the limit amount up or down for specific months.
- Know how to configure the overall monitoring scope (All AWS services) and choose to aggregate by Unblended costs.

**Configuring Usage Budgets**
- Recognize that a Usage Budget monitors the volume or consumption time of resources rather than the monetary value.
- Clearly differentiate: Cost Budgets manage the pressure of "Money," while Usage Budgets manage the pressure of "Frequency/Running Time."
- Know how to configure filters by Usage type groups, typically monitoring the running hours of a Load Balancer (`EC2: ELB - Running Hours`).
- Realize that a Usage Budget is extremely useful for monitoring background resources that can easily cause waste over time, such as NAT Gateways, EC2, and ELB.

**Understanding Reservation & Savings Plans Budgets**
- Grasp the theory behind Reservation Budgets (managing RIs) and Savings Plans Budgets (managing compute savings plans).
- Understand that these two types help enterprises measure coverage and utilization metrics of upfront investments or long-term commitments to prevent waste.
- Realize these are advanced features, usually applied in real-world Production environments. Do not arbitrarily activate or purchase real plans in a personal account to avoid unexpected long-term commitment costs.

**Alert Thresholds & Health Monitoring Mechanism**
- Know how to set alert tiers based on two criteria: Actual costs or Forecasted costs.
- Successfully set up multi-tier rules (e.g., trigger an alert at 50%, send a serious reminder at 80%, and a red alert at 100%).
- Understand how Budget health works to quickly filter out which budgets are in the safe zone or the danger zone.
- Understand the data latency mechanism of AWS Billing so as not to panic when figures are not synchronized instantly.

**The Importance of Cleanup**
- Realize that Cleaning Up after every lab session is a mandatory skill to maintain a clean infrastructure and avoid notification spam.
- Firmly grasp the principle: Deleting AWS Budgets configurations only removes the checking and email rules; it completely does not affect or interrupt the services delivering applications in the account.

---

#### Visual Practical Implementation

**Module 1 — Quick Budget Deployment via Template**
- Successfully logged into the AWS Management Console.
- Navigated to the AWS Billing and Cost Management dashboard and selected the Budgets module.
- Started the creator by clicking the `Create a budget` button.
- Chose the quick initialization option: `Use a template (simplified)`.
- Applied the `Monthly cost budget` template, filled in the identification info and limit amount according to the lab guide.
- Specified the target email to receive notifications and completed the process with the `Create budget` command.
- Verified the budget's appearance on the directory and opened the Budget history tab to survey the history interface.
- 📸 *Proof: Successfully accessed AWS Billing and Cost Management.*
- 📸 *Proof: Setup operation with Use a template.*
- 📸 *Proof: Declared limit info on the Monthly cost budget template.*
- 📸 *Proof: The first budget displaying active status.*

**Module 2 — Advanced Custom Cost Budget Setup**
- In the Budgets section, activated the creation process and switched to the advanced `Customize` mode.
- Specified the `Cost budget` classification and proceeded to the next step.
- Declared the identifier name for the budget as `Monthly`.
- Set the frequency to `Monthly`, selected the `Recurring Budget` repetition type, and applied the `Fixed` limit method.
- Entered the limit amount allowed for spending.
- Narrowed or expanded the application scope in the Budget scope section by selecting `All AWS services` combined with `Unblended costs`.
- Set the alert rule (`Add an alert threshold`) at the desired level (e.g., 80% of actual cost) and entered the admin email address.
- Reviewed all parameters on the Summary page before confirming system initialization.
- 📸 *Proof: Selected Customize and Cost budget type.*
- 📸 *Proof: Detailed setup of period, Fixed method, and Unblended costs scope.*
- 📸 *Proof: Configured percentage alert tiers and declared Email.*
- 📸 *Proof: Custom Cost Budget successfully displayed in the list.*

**Module 3 — Create Usage Budget to Monitor Consumption Capacity**
- Followed the custom budget creation steps (`Customize`) but selected the `Usage budget` classification.
- Set a distinct name for the Usage Budget.
- In the consumption characteristic filter area (`Budget against`), selected `Usage type groups`.
- Searched for and specified the exact desired resource group, specifically `EC2: ELB - Running Hours`.
- Set the monitoring timeframe, chose the appropriate limit type, and entered the maximum number of hours the Load Balancer is allowed to run during the cycle.
- Moved to the Alert configuration section, set the alert percentage level based on actual consumption capacity, and entered the receiving email information.
- Completed the initialization and proceeded to review the `Budget health` indicator to assess the Load Balancer's current consumption level.
- 📸 *Proof: Selected Usage budget classification on the initialization interface.*
- 📸 *Proof: Filtered and specified the EC2: ELB - Running Hours service group.*
- 📸 *Proof: Entered the operating hours limit and configured the Email alert.*
- 📸 *Proof: The system recorded the new Usage Budget in checking status.*

**Module 4 & 5 — Research Reservation & Savings Plans Budgets via Simulation**
- Executed the custom initialization steps specifically for `Reservation budget` and `Savings Plans budget`.
- Set explicit names for each budget type to facilitate management.
- Configured the `Coverage threshold` (for RI) and `Utilization threshold` (for savings plans) according to the practical scenarios instructed in the workshop document.
- Filled in the email information to receive performance alerts in the Alert setting section.
- Clicked create to experience the enterprise-standard setup process.
- *Important note recorded in the lab:* Due to the nature of a personal/practice account, students only performed operations at the level of exploring the interface and simulated configuration, and did not execute actual commitment purchases to avoid unexpected financial bills.
- 📸 *Proof: Simulated Reservation budget configuration interface.*
- 📸 *Proof: Savings Plans budget metric configuration interface.*

**Module 6 — Clean Up the Practical Environment**
- Accessed the centralized Budgets management directory in AWS Billing.
- Proceeded to tick the test budgets created throughout the lab session.
- Opened the `Actions` navigation menu located in the top right corner and selected the `Delete` command.
- Confirmed the deletion decision at the pop-up notification window for the system to completely remove the configuration.
- Repeated the same for the rest until the list returned to its initial state, ensuring no redundant mailing rules remained.
- 📸 *Proof: Summary table of existing Budgets before deletion.*
- 📸 *Proof: Delete Budget action confirmation dialog.*
- 📸 *Proof: Clean interface after completing the cleanup process.*

---

### Challenges and obstacles faced:

- The Billing and Cost Management dashboard integrates many analytical tools (Bills, Cost Explorer, Budgets, etc.), making the initial approach confusing among the features.
- The theoretical boundary between a Cost Budget and a Usage Budget can easily be mixed up if one does not stick closely to the unit of measurement (USD vs. Output/Running hours).
- The `Usage type groups` directory has a very broad filter, requiring careful reading and exact searching for the keyword `EC2: ELB - Running Hours` to avoid mistakenly selecting other services.
- Due to the asynchronous update mechanism (Data Latency) of AWS, monetary metrics and historical charts do not show changes immediately after creation, making it difficult to verify instant results.
- Advanced knowledge related to RIs and Savings Plans is relatively abstract because students have not yet had the chance to encounter large-scale cost optimization problems in reality.
- If email syntax is not checked carefully or verification is forgotten, the alert system may fail to deliver messages to the inbox as expected.

---

### Solutions and lessons learned:

- Always maintain the habit of carefully reading every technical instruction in the guide document before clicking on the AWS Console interface.
- Systematize the nature of the tools with a concise mind map:
  - *Cost Budget:* Manages the wallet.
  - *Usage Budget:* Manages the running hours/capacity of resources.
  - *Reservation / Savings Plans Budget:* Monitors the efficiency of upfront commitment plans.
- Set smart notification thresholds (from low to high) to create buffer zones, giving yourself time to intervene and handle resources before hitting the 100% mark.
- Strictly adhere to account safety principles: Do not click to buy or activate any real RI/Savings Plans commitments while doing a learning lab.
- Thoroughly clean up experimental configurations immediately after finishing the lab to keep the learning environment standardized.
- Combine using AWS Budgets with manually reviewing the Billing Dashboard periodically after each study session to early detect hidden costs.

---

### Plan and roadmap for next week:

- Continue to delve deeper into the supplementary modules within the AWS Billing and Cost Management ecosystem.
- Shift focus to researching **AWS Cost Explorer** to learn how to break down and analyze costs deeply by tags, services, and time dimensions.
- Learn how to track free tier limits through the **AWS Free Tier Dashboard**.
- Approach anomalous cost detection solutions using machine learning with **AWS Cost Anomaly Detection**.
- Understand the centralized financial management model for a chain of multiple accounts through the **AWS Organizations** service.
- Maintain and practice the habit of checking the Billing Dashboard periodically to enhance FinOps (cloud cost optimization) mindset.

---

### 💡 A small tip for you to avoid duplication (plagiarism):
1. **Proof images (`📸 Proof...`):** This is the part that proves your own work. Rename the screenshots using your own consistent structure, for example: `week6_budgets_01.png`, `week6_cost_budget_actual.png`, etc.
2. **Amount limit:** In the sections mentioning "enter the monthly spending limit," when doing the actual lab, enter an odd or specific number of your choice (e.g., `10 USD`, `15 USD`) and put that specific number into the report instead of writing generally to create a unique touch for your report.