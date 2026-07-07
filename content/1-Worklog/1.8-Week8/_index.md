---
title: "Week 8 Worklog"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Key Objectives for Week 8:

- Explore the big picture of the AWS Identity and Access Management (IAM) service.
- Deeply understand the core role of IAM in controlling identities and allocating permissions within a cloud computing environment.
- Deploy robust account protection layers through the Multi-Factor Authentication (MFA) mechanism.
- Directly practice the identity management process: initializing IAM Users, allocating Groups, setting up Roles, and attaching Policies.
- Internalize and strictly apply the "Principle of Least Privilege" in security.
- Research an overview of the Amazon Virtual Private Cloud (Amazon VPC) network architecture.
- Dissect and analyze the network nodes that make up a complete VPC system.
- Manually build network infrastructure from scratch: configuring a VPC, partitioning Subnets, setting up Route Tables, and opening outbound internet access (Internet Gateway).
- Deploy network security checkpoints through Security Group and Network ACL firewalls.
- Consolidate the mindset of designing a secure, isolated, and optimized network infrastructure on the AWS platform.

---

### Detailed Action Plan:

| Day | Task Details | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Mon | - Read the AWS IAM lab guide <br> - Evaluate the function of IAM within the AWS ecosystem <br> - Prepare a safe account and practice environment | 06/08/2026 | 06/08/2026 | https://000009.awsstudygroup.com/ |
| Tue | - Distinguish the nature of entities: IAM User, Group, Role, and Policy <br> - Practice creating new users and assigning them to corresponding groups <br> - Grant permissions using available policies (Managed Policy) | 06/09/2026 | 06/09/2026 | https://000009.awsstudygroup.com/ |
| Wed | - Research account protection mechanisms using Multi-Factor Authentication (MFA) <br> - Activate MFA for both the Root user and IAM Users <br> - Delve into cloud security standards | 06/10/2026 | 06/10/2026 | https://000009.awsstudygroup.com/ |
| Thu | - Shift focus to virtual networking with Amazon VPC <br> - Analyze the architectural diagram and data flow within a VPC network <br> - Familiarize with foundational networking concepts | 06/11/2026 | 06/11/2026 | https://000010.awsstudygroup.com/ |
| Fri | - Initialize an independent Virtual Private Cloud <br> - Partition the network range into Public Subnets and Private Subnets <br> - Attach an Internet Gateway and route traffic via Route Tables | 06/12/2026 | 06/12/2026 | https://000010.awsstudygroup.com/ |
| Sat | - Build security barriers: Security Groups and Network ACLs <br> - Test connection flows between instances to verify configurations <br> - Fine-tune and finalize the network architecture | 06/13/2026 | 06/13/2026 | https://000010.awsstudygroup.com/ |
| Sun | - Review the entire list of deployed resources <br> - Perform environment Cleanup to avoid incurring charges <br> - Consolidate knowledge, note errors, and write the weekly report | 06/14/2026 | 06/14/2026 | https://000009.awsstudygroup.com/ <br> https://000010.awsstudygroup.com/ |

---

### Summary of Achieved Results:

#### Knowledge Base

**AWS IAM Identity Management**
- Deeply understand that IAM is the central control hub determining "who" is allowed to do "what" in an AWS account.
- Master the lifecycle of creating and managing entity groups: IAM User, Group, Role, and Policy.
- Engrave the core principle of Least Privilege to prevent data leakage risks.
- Clearly define the boundaries between AWS Managed Policies and Customer Managed Policies.
- Understand safe management methods for login credentials and Access Keys.

**AWS Account Security**
- Highly value the role of MFA as a secondary "shield" against account takeover attacks.
- Master the device synchronization process to configure MFA.
- Internalize the golden rule of security: Never use the Root account for daily tasks; instead, create and use an IAM User.

**Amazon VPC Network Architecture**
- Grasp how a VPC creates an isolated, software-defined network space in the cloud.
- Understand the principle of IP range allocation (CIDR Block) and how to subdivide them into Subnets for specific purposes.
- See the importance of the Internet Gateway in opening internet access and how Route Tables act as the "navigator" for data packets.
- Identify the core difference between a Public Subnet (with internet outbound access) and a Private Subnet (completely isolated).

**Network Infrastructure Security**
- Master the mechanism of Security Groups: acting as stateful virtual firewalls that protect at the EC2 Instance level.
- Understand the principle of Network ACLs: acting as stateless gatekeepers at the Subnet network level.
- Know how to strictly establish Inbound and Outbound data flow rules.
- Perfect the mindset for designing multi-layered secure network systems.

---

#### Visual Practical Implementation

**Module 1 — AWS IAM**
- Successfully logged into the IAM console.
- Initialized Users and placed them into corresponding Groups.
- Attached permissions via Managed Policies.
- Successfully configured IAM Roles for hypothetical services.
- Successfully activated two-factor authentication (MFA).
- Performed a test login using an IAM User to verify permission boundaries.

**Module 2 — AWS Security**
- Applied security standards according to AWS best practices.
- Disabled or deleted unnecessary Access Keys, strictly applying Least Privilege.
- Re-verified the safe configuration of the Root account.

**Module 3 — Amazon VPC**
- Successfully initialized a VPC with a custom CIDR block.
- Completely set up the structure of Public Subnets and Private Subnets.
- Initialized and attached an Internet Gateway to the VPC.
- Successfully routed traffic from the Public Subnet to the internet via Route Tables.

**Module 4 — Network Security Configuration**
- Created and attached Security Groups allowing basic communication ports (SSH/HTTP).
- Configured Network ACLs to block/allow IP ranges based on scenarios.
- Successfully performed ping tests to confirm the network flowed exactly as designed.
- Verified the effectiveness of the virtual firewalls.

**Module 5 — Resource Cleanup**
- Cross-checked the entire VPC, Subnets, IGW, and IAM Users created during the lab.
- Safely deleted and removed each component.
- Completed the cleanup process, returning the account to a clean environment.

---

### Evaluation of Week 8 Results:

- Excellently mastered the IAM tool to manage access permissions.
- Operated smoothly in creating and allocating permissions for Users, Groups, Roles, and Policies.
- Successfully activated MFA, ensuring the account is at the highest safety level.
- Manually designed, configured, and fully operated a basic Amazon VPC network system.
- Accurately allocated network components: Public/Private Subnets, Route Tables, and IGWs.
- Successfully configured a multi-tier protection network using Security Groups and Network ACLs.
- Became much more confident in planning and deploying secure infrastructure on AWS.

---

### Challenges and Obstacles Faced:

- In the early stages, it was easy to confuse the concepts between an IAM Role (used for temporary authorization/services) and an IAM User (used for people).
- Struggled to distinguish the difference between a Managed Policy (standalone policy) and an Inline Policy (embedded policy).
- The concepts of "stateful" (Security Group) and "stateless" (Network ACL) firewalls were a bit abstract and hard to grasp.
- Struggled for a while to understand how to calculate CIDR Block IP ranges and the data routing logic of Route Tables.
- Encountered Timeout errors unable to access instances due to forgetting to open Inbound ports in the Security Group or misconfiguring the Route Table.

---

### Solutions and Lessons Learned:

- Re-read use-cases in AWS documentation over and over to fully understand the core differences between a Role and a User.
- Directly practiced creating both types of Policies to clearly see the differences in flexibility and reusability.
- Proactively drew the network architecture diagram on paper or used tools (like draw.io) to clearly visualize the packet flow (from IGW -> Route Table -> NACL -> Subnet -> SG -> Instance).
- Formed a habit of carefully cross-checking every Inbound/Outbound rule when conducting network troubleshooting.
- Firmly applied the "only open truly necessary ports" mindset instead of taking the easy route of opening All Traffic (0.0.0.0/0).
