---
title: "Week 9 Practice Report"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Key Objectives for Week 9:

- Explore the overview of the AWS Command Line Interface (AWS CLI).
- Grasp the advantages and role of the CLI in automating and managing AWS resources, replacing the traditional web interface.
- Directly install and set up the AWS CLI environment on a personal computer.
- Practice the skill of querying information and controlling the system entirely using terminal commands.
- Apply AWS CLI to interact with the Amazon S3 storage service (manage buckets, objects).
- Configure and navigate the Amazon SNS notification service via the command line.
- Access and manage identity information (IAM) through the AWS CLI.
- Understand how to fetch information and manage virtual networks (Amazon VPC) using scripts.
- Deploy, inspect, and tear down Amazon EC2 virtual servers without using a mouse.
- Execute cleanup scripts after completing the lab to protect the AWS budget.

---

### Detailed Action Plan:

| Day | Task Details | Start Date | Completion Date | Reference Materials |
| --- | --- | --- | --- | --- |
| Monday | - Research the introductory documentation on AWS CLI <br> - Analyze the API calling mechanism via the command line <br> - Prepare the personal computer and practice account | 06/15/2026 | 06/15/2026 | https://000011.awsstudygroup.com/1-introduction/ |
| Tuesday | - Download and install the AWS CLI software package <br> - Execute `aws configure` to input the Access Key and Region <br> - Authenticate the connection to the AWS account | 06/16/2026 | 06/16/2026 | https://000011.awsstudygroup.com/2-prerequiste/ <br> https://000011.awsstudygroup.com/3-installation/ |
| Wednesday | - Use query commands to inventory existing resources <br> - Familiarize with the basic grammar structure of the CLI | 06/17/2026 | 06/17/2026 | https://000011.awsstudygroup.com/4-check-resource/ |
| Thursday | - Operate Amazon S3 via the terminal <br> - Run the script to create a new Bucket <br> - Execute commands to copy, upload, and download files | 06/18/2026 | 06/18/2026 | https://000011.awsstudygroup.com/5-cli-with-s3/ |
| Friday | - Interact with Amazon SNS using CLI <br> - Create a notification Topic <br> - Subscribe an email and push a test message | 06/19/2026 | 06/19/2026 | https://000011.awsstudygroup.com/6-cli-with-sns/ |
| Saturday | - Retrieve IAM information (User, Group) via the command line <br> - Detail network infrastructure (VPC, Subnet, SG) <br> - Use the `run-instances` command to provision an EC2 server | 06/20/2026 | 06/20/2026 | https://000011.awsstudygroup.com/7-cli-with-iam/ <br> https://000011.awsstudygroup.com/8-cli-with-vpc/ <br> https://000011.awsstudygroup.com/9-create-ec2/ |
| Sunday | - Cross-check the initialized resources <br> - Run the Cleanup command for the entire practice infrastructure <br> - Write the report and summarize experiences | 06/21/2026 | 06/21/2026 | https://000011.awsstudygroup.com/11-clean-up/ |

---

### Summary of Achieved Results:

#### Knowledge Base

**The Nature of AWS CLI**
- Understand that AWS CLI is an open-source toolset acting as a wrapper to communicate directly with AWS APIs.
- Evaluate the power of CLI in helping DevOps engineers optimize time and easily automate repetitive tasks using shell scripts.
- Master the process of securely managing credentials in a local environment.

**Installation & Configuration Process**
- Proficient in setting up the CLI executable on the current operating system.
- Clearly understand the meaning of the 4 parameters when running `aws configure`: Access Key ID, Secret Access Key, Default Region, and Default Output Format (usually `json`).
- Know how to use the `aws sts get-caller-identity` command to verify the operating identity.

**Amazon S3 Management via Command Line**
- Smoothly use the `aws s3` command family for high-level management (create bucket `mb`, synchronize `sync`, copy `cp`, remove `rm`).
- Understand how to completely clean up a bucket using force parameters.

**Navigating Amazon SNS**
- Understand how to call commands to initialize a new Topic and extract the Topic ARN.
- Know how to add an Endpoint (like an Email) to a Topic and trigger a test Notification directly from the terminal.

**Identity Management (IAM)**
- Know how to use the `aws iam` command to list users, display groups, and extract Policies for security auditing purposes.

**Network Control (Amazon VPC)**
- Effectively use the `describe` command to get detailed information about VPC IDs, Subnet IDs, and Security Group IDs. This is a mandatory stepping stone for initializing EC2 via the command line.

**Deploying Virtual Servers (Amazon EC2)**
- Master the complex syntax of the `aws ec2 run-instances` command.
- Clearly understand the need to pass minimum parameters: Image ID (AMI), Instance Type, Subnet ID, and Key Pair to successfully create a server.

---

#### Visual Practical Implementation

**Module 1 — Introduction**
- Carefully studied the theoretical documentation.
- Grasped the structural logic of a standard CLI command: `aws <command> <subcommand> [options and parameters]`.

**Module 2 — Installation**
- Successfully downloaded and installed AWS CLI v2.
- Entered the Access Key information and successfully configured the default profile.
- Ran the `aws --version` command to verify a valid installation.

**Module 3 — Check Resource**
- Practiced running `describe` and `list` commands to scan running services on the account.
- Familiarized with reading the returned results in JSON format.

**Module 4 — Interacting with Amazon S3**
- Successfully created a brand new Bucket using the `aws s3 mb` command.
- Successfully pushed a test text file from the computer to the cloud and pulled it back to the local machine.
- Used the `aws s3 rb` command to delete the bucket, completing the S3 lab.

**Module 5 — Interacting with Amazon SNS**
- Successfully initialized an SNS Topic.
- Ran the subscribe command to link a personal email and confirmed the mailbox.
- Used the `publish` command to shoot a simulated alert message and received the response email.

**Module 6 — Interacting with IAM**
- Ran the `aws iam list-users` command to output the current user list.
- Successfully queried the Group and Policy information associated with the operating User.

**Module 7 — Interacting with Amazon VPC**
- Practiced the `aws ec2 describe-vpcs` and `describe-subnets` command set.
- Copied and stored the ID values of the network infrastructure into a draft file to prepare for the EC2 creation step.

**Module 8 — Create EC2**
- Successfully wrote and executed the long command chain to initialize an EC2 Instance.
- Called the Status check command to confirm the server transitioned to "running".
- Proceeded to run the `terminate-instances` command to manually shut down the server remotely.

**Module 9 — Cleanup Resources**
- Reviewed via CLI to ensure no running EC2 instances or forgotten S3 Buckets remained.
- Saved cleanup time by typing commands instead of clicking back and forth between screens on the Console.

---

### Evaluation of Week 9 Results:

- Successfully took the initial step in shifting the operational mindset from a Graphical User Interface (GUI) to a Command Line Interface (CLI).
- Installation, configuration, and authentication of the CLI environment worked perfectly.
- Flexibly utilized AWS CLI to handle basic needs with S3, SNS, IAM, VPC, and EC2.
- Clearly felt a significant improvement in operational speed once accustomed to the syntax.
- Upgraded foundational skills solidly to aim towards fully automating the DevOps process on AWS.

---

### Challenges and Obstacles Faced:

- The command syntax is quite long, especially in the EC2 module; typing just one character wrong or missing a space causes an error.
- Faced initial difficulties when having to read and parse data from the lengthy JSON blocks returned by the CLI.
- The EC2 creation operation requires high sequentiality: one must use CLI to obtain the Subnet ID, AMI ID, and Security Group ID before assembling them into an executable command.
- Sometimes encountered an `Access Denied` error because the IAM User account used to issue the Access Key lacked sufficient permissions (Policy) to execute the task.

---

### Solutions and Lessons Learned:

- Frequently attach the `--help` flag after a command to read the built-in documentation, or look up the AWS CLI Command Reference page.
- Pre-write long commands in a Note software (like Notepad, VS Code), and carefully review the ID parameters before copying and pasting them into the Terminal to run.
- Form a habit of checking the identity with the `aws sts get-caller-identity` command to ensure the correct authorized profile is being used.
- To get used to JSON, one can combine the `jq` tool or the `--query` feature of the AWS CLI to filter the output, making it neater and easier to read.
