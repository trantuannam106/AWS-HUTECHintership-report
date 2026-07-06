---
title: "Week 5 Worklog"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

- Grasp the big picture of operating the FCJ Management application combined with the power of Auto Scaling Groups.
- Understand the automatic resource scaling mechanism (adding/removing EC2 Instances) of Amazon EC2 Auto Scaling based on actual traffic volume.
- Know how to integrate an Application Load Balancer (ALB) with an ASG to ensure high availability and excellent fault tolerance.
- Manually set up core network and server infrastructure, including: VPC, Subnets (Public/Private), Security Group firewalls, EC2 instances, and RDS databases.
- Install and run the FCJ Management app on an EC2 environment, establish a successful connection with the RDS database, and maintain the application using Node.js and PM2.
- Package the complete EC2 configuration into an AMI, then build a Launch Template as a standard blueprint to deploy new instances consistently.
- Set up a Target Group and ALB to act as a traffic coordinator, distributing user requests evenly across the EC2 instances.
- Initialize an Auto Scaling Group, define capacity limits (Desired, Min, Max Capacity), and synchronize this system with the Load Balancer.
- Directly test and compare 4 resource scaling scenarios: Manual, Scheduled, Dynamic, and Predictive Scaling.
- Monitor performance metrics through CloudWatch, analyze scaling efficiency, and systematically clean up resources to avoid unnecessary costs.

---

### Tasks Planned for This Week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------------------------------------------------- |
| Monday | - Module 01: Introduction <br> - Module 02.1: Setup Network Infrastructure <br> - **Hands-on Practice:** <br>&emsp;+ Create `AutoScaling-Lab` VPC across 3 AZs <br>&emsp;+ Allocate Public and Private Subnets <br>&emsp;+ Configure Security Groups to secure both application and database traffic | 18/05/2026   | 18/05/2026      | https://000006.awsstudygroup.com/ |
| Tuesday | - Module 02.2: Launch EC2 Instance <br> - Module 02.3: Launch a Database Instance with RDS <br> - **Hands-on Practice:** <br>&emsp;+ Launch `FCJ-Management` EC2 instance using Amazon Linux 2023 <br>&emsp;+ Group private subnets into a DB Subnet Group and launch RDS MySQL Instance <br>&emsp;+ Connect to RDS from EC2, build database structure, and insert mock data into the `user` table | 19/05/2026   | 19/05/2026      | https://000006.awsstudygroup.com/ |
| Wednesday | - Module 02.4: Setup data for Database <br> - Module 02.5: Deploy Web Server <br> - Module 02.6: Prepare metric for Predictive Scaling <br> - **Hands-on Practice:** <br>&emsp;+ Set up the environment and clone FCJ Management source code from GitHub <br>&emsp;+ Install PM2, start the app via `npm start`, and configure auto-restart on boot <br>&emsp;+ Prepare mock metric data and upload it to CloudWatch | 20/05/2026   | 20/05/2026      | https://000006.awsstudygroup.com/ |
| Thursday | - Module 03: Create Launch Template <br> - Module 04.1: Create Target Group <br> - **Hands-on Practice:** <br>&emsp;+ Create an AMI from the perfectly running EC2 instance <br>&emsp;+ Use this AMI to forge the `FCJ-Management-template` Launch Template <br>&emsp;+ Create `FCJ-Management-TG` Target Group using HTTP protocol on port `5000` | 21/05/2026   | 21/05/2026      | https://000006.awsstudygroup.com/ |
| Friday | - Module 04.2: Create Load Balancer <br> - Module 05: Test <br> - **Hands-on Practice:** <br>&emsp;+ Deploy an Internet-facing Application Load Balancer named `FCJ-Management-LB` <br>&emsp;+ Route ALB traffic directly to the Target Group <br>&emsp;+ Access the web app using ALB's DNS name and smoothly test CRUD operations | 22/05/2026   | 22/05/2026      | https://000006.awsstudygroup.com/ |
| Saturday | - Module 06: Create Auto Scaling Group <br> - Module 07.1: Test Manual Scaling Solution <br> - Module 07.2: Test Scheduled Scaling Solution <br> - **Hands-on Practice:** <br>&emsp;+ Initialize `FCJ-Management-ASG` based on the Launch Template <br>&emsp;+ Execute Manual Scaling test (manually terminating instances) <br>&emsp;+ Schedule a scaling action to anticipate rush hour traffic | 23/05/2026   | 23/05/2026      | https://000006.awsstudygroup.com/ |
| Sunday | - Module 07.3: Test Dynamic Scaling Solution <br> - Module 07.4: Read Metrics of Predictive Scaling Solution <br> - Module 08: Cleanup Resources <br> - **Hands-on Practice:** <br>&emsp;+ Write a Dynamic Scaling policy to spawn instances based on ALB Request counts <br>&emsp;+ Configure and analyze a Predictive Scaling Policy <br>&emsp;+ Thoroughly wipe out the system (ASG, ALB, TG, Template, AMI, EC2, RDS) and double-check Billing | 24/05/2026   | 24/05/2026      | https://000006.awsstudygroup.com/ |

---

### Week 5 Achievements:

#### Knowledge Gained

**Amazon EC2 Auto Scaling and ALB Concepts**
- Discovered EC2 Auto Scaling as a smart tool that automatically injects or removes EC2 servers purely based on actual traffic pressure.
- Ensures the system never runs out of resources by replacing failed instances, maintaining desired capacity, and scaling out flexibly during high traffic.
- Mastered the Layer 7 characteristics of ALB, which is highly optimized for HTTP/HTTPS traffic to receive user requests and distribute them evenly across EC2 servers.
- ALB protects the system by hiding Private IPs and preventing users from seeing or connecting directly to individual EC2 machines.

**Target Group, AMI, and Launch Template Mechanisms**
- Understood that a Target Group acts as a gathering point for destination devices, categorized by `Instances`, running the `HTTP` protocol on port `5000`, and automatically blocking traffic to failed nodes (Unhealthy).
- Concept of AMI: An exact image containing the operating system, application code, and all configurations of a server used for cloning.
- A Launch Template serves as a "technical blueprint" storing core parameters (AMI, instance type, Key Pair, network, firewall) allowing the ASG to mass-produce consistent instances.

**Amazon RDS and Layered Network Architecture**
- Applied the tiered model: completely decoupling the database from EC2 and moving it down to the private subnet zone of RDS to minimize security risks.
- Designed a network spanning at least 3 Availability Zones to maximize High Availability and eliminate single points of failure.
- Established strict Security Groups: The Web App SG opens application port (`5000`) to the public; whereas the Database SG completely blocks all traffic except for port `3306` originating explicitly from the Application SG.

**Monitoring Systems and 4 Resource Scaling Solutions**
- Recognized CloudWatch as a performance monitoring dashboard (CPU Utilization, Request Count) that displays visual metrics to support scaling decisions.
- **Manual Scaling:** Adjusting the desired capacity directly on the Console. It is easy to control but requires the administrator to be on standby, reacting slowly to sudden traffic spikes.
- **Scheduled Scaling:** Pre-programming a timetable to increase server capacity for services with predictable load cycles (rush hours, sale seasons).
- **Dynamic Scaling:** An automatic scaling scenario based on real-time load, applying a Target Tracking Policy to closely monitor the request count sent to the Target Group.
- **Predictive Scaling:** Leveraging Machine Learning algorithms to learn from historical data, proactively preparing servers one step ahead of the actual traffic storm.

---

#### Hands-on Practice

**Module 2 — Setup Network Infrastructure and Deploy Database:**
- Initialized the `AutoScaling-Lab` VPC (CIDR `10.0.0.0/16`), structuring the network with 3 public subnets and 3 private subnets spread across 3 different AZs.
- Set up the Application Security Group (`FCJ-Management-SG`) to open ports 22, 80, 443, and 5000, while configuring the Database SG to strictly accept port 3306 only from the Application SG.
- Built a DB Subnet Group as a launchpad for a Production-ready, Multi-AZ RDS MySQL Instance.
- SSH'd into the initial EC2 server, installed Git and MariaDB client, and securely connected to the RDS endpoint to initialize table structures and seed data into the `user` table.

- 📸 ![Proof Image: RDS MySQL Database System successfully created in Available status](/aws-intership-report/images/1-Worklog/1.5-Week5/rds-mysql-available.png)

**Module 3 & 4 — Web Server Operation, AMI Packaging, and Load Balancing:**
- Deployed Node.js 20 environment, cloned code from GitHub, and configured the `.env` file to connect directly with the RDS Database Endpoint.
- Installed the global PM2 manager to keep the application running in the background on port 5000, executing `pm2 startup` and `pm2 save` to ensure the app resurrects automatically upon server reboot.
- Snapshotted the EC2 state into `FCJ-Management-AMI` and built the `FCJ-Management-template` Launch Template to standardize hardware and networking.
- Configured the `FCJ-Management-TG` Target Group (Port 5000) and deployed an Internet-facing Application Load Balancer named `FCJ-Management-LB`.

- 📸 ![Proof Image: FCJ Management app interface loaded successfully with smooth CRUD operations via ALB's DNS](/aws-intership-report/images/1-Worklog/1.5-Week5/alb-dns-crud-success.png)

**Module 6 & 7 — Auto Scaling Configuration and Testing:**
- Initialized `FCJ-Management-ASG` attached to the Launch Template with capacity limits (Min: 1, Desired: 1, Max: 3) and enabled ELB Health Checks.
- Fired high-intensity load testing tools at the ALB's DNS link, executed **Manual Scaling** by dropping Desired capacity to 0 to watch the ASG automatically terminate instances.
- Scheduled a **Scheduled Action** named `Rush hour` (timezone `Asia/Ho_Chi_Minh`) to scale up servers, verifying precise execution logs in the Activity tab.
- Wrote a **Dynamic Scaling** (Target Tracking) policy based on the `ALB Request Count Per Target` at a 500-request threshold to verify autonomous scaling.
- Used AWS CLI to push mock JSON data (CPU and instance metrics) to CloudWatch, created a **Predictive Scaling Policy** using a custom metric pair, and analyzed the AI's intelligent forecast graph.

- 📸 ![Proof Image: Load and Capacity charts showcasing Predictive Scaling's ability to anticipate future load](/aws-intership-report/images/1-Worklog/1.5-Week5/asg-predictive-metrics-chart.png)

**Module 8 — System Cleanup Process:**
- Systematically dismantled resources in the correct order: Delete ASG -> Remove ALB -> Delete Target Group -> Delete Launch Template -> Deregister AMI -> Terminate initial EC2 -> Delete RDS Database and DB Subnet Group to prevent hidden charges.

---

#### Difficulties and Solutions

**Difficulties:**
- The application ran on port `5000`, but the Application Load Balancer continuously reported connection errors and failed to load the interface because this port was not opened in the Security Group.
- When configuring RDS MySQL, the system failed to connect or isolate network tiers due to mistakenly selecting public VPC subnets or a DB Subnet Group containing public subnets.
- The Auto Scaling Group flagged severe errors and refused to launch new machines because the Launch Template was linked to an AMI that was still in `Pending` status (not yet `Available`).
- High risk of incurring massive hidden billing charges from hourly-billed resources like Multi-AZ RDS and Application Load Balancer if accidentally left running after lab completion.

**Solutions:**
- Thoroughly reviewed Security Group Inbound rules, widely opened TCP port 5000 for the app, and applied strict security configurations so RDS only accepts port 3306 from the Application SG's ID.
- Systematized the data flow diagram on paper before execution, accurately grouping hidden subnets into the DB Subnet Group and burying RDS entirely within the Private Subnet range.
- Practiced patience, waiting until the AMI packaging progress bar on the EC2 Console turned completely green (`Available`) before embedding it into the Launch Template.
- Established a rigorous cloud garbage cleanup checklist from top to bottom (including hidden resources like EBS Snapshots and CloudWatch Logs) and double-checked the Billing Dashboard.

---

#### Lessons Learned

- A deep understanding of the classic 3-tier architecture (ALB coordinating - EC2 processing - RDS storing) helps the system eliminate single points of failure and achieve maximum security.
- Always trust the PM2 process manager wrapping the Node.js app combined with system configuration save commands (`pm2 startup`) as an insurance policy in case the server crashes unexpectedly.
- Realized the importance of running Dynamic Scaling in parallel with Predictive Scaling, allowing the system to react flexibly to live load while proactively stepping ahead of incoming traffic storms.
- Quality Cloud system design always requires architects to place both Cost Optimization and Security on the balance scale right from the very first blueprint drafts.