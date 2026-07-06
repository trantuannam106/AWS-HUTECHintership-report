---
title: "Week 4 Worklog"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

- Learn the overview of Amazon RDS and its role in Cloud database systems.
- Understand RDS features such as managed service, automated backup, scaling, Multi-AZ, and Read Replicas.
- Practice creating VPCs, Subnets, and Security Groups for EC2 and RDS.
- Create a DB Subnet Group to prepare the database deployment environment.
- Launch an EC2 Instance as an application server to connect to RDS.
- Create an RDS Database Instance and verify the Endpoint, Port, and Username.
- Deploy the AWS FCJ Management application connected to the RDS database.
- Practice database backup, snapshot, and restore.
- Clean up resources after completing the lab to avoid unnecessary charges.

---

### Tasks Planned for This Week:

| Day | Tasks | Start Date | Completion Date | Reference |
| --- | --- | --- | --- | --- |
| Monday | - Read the Introduction to Amazon RDS <br> - Understand what RDS is, OLTP, DB Instance, and Endpoint <br> - Learn about supported database engines such as MySQL, PostgreSQL, MariaDB, SQL Server, Oracle, and Aurora | 11/05/2026 | 11/05/2026 | https://000005.awsstudygroup.com/ |
| Tuesday | - Module 2.1: Create a VPC <br> - Create VPC, Public Subnet, and Private Subnet <br> - Configure multiple Availability Zones to prepare for RDS | 12/05/2026 | 12/05/2026 | https://000005.awsstudygroup.com/ |
| Wednesday | - Module 2.2: Create EC2 Security Group <br> - Module 2.3: Create RDS Security Group <br> - Open necessary ports for EC2 and restrict RDS to only accept connections from the EC2 Security Group | 13/05/2026 | 13/05/2026 | https://000005.awsstudygroup.com/ |
| Thursday | - Module 2.4: Create DB Subnet Group <br> - Module 3: Create EC2 Instance <br> - Launch Amazon Linux EC2, assign Key Pair, and connect via SSH using MobaXterm | 14/05/2026 | 14/05/2026 | https://000005.awsstudygroup.com/ |
| Friday | - Module 4: Create RDS Database Instance <br> - Create database instance, configure engine, username, password, VPC, and Security Group <br> - Check the Available status, Endpoint, and Port of the RDS | 15/05/2026 | 15/05/2026 | https://000005.awsstudygroup.com/ |
| Saturday | - Module 5: Application Deployment <br> - Clone AWS FCJ Management source code <br> - Install Node.js, npm packages, and MySQL client <br> - Create database, user table, and run the application on port 5000 | 16/05/2026 | 16/05/2026 | https://000005.awsstudygroup.com/ |
| Sunday | - Module 6: Backup and Restore <br> - Verify RDS backup, snapshot, and restore <br> - Module 7: Clean up resources <br> - Delete EC2, RDS, Snapshot, Subnet Group, Security Group, and VPC to avoid generating charges | 17/05/2026 | 17/05/2026 | https://000005.awsstudygroup.com/ |

---

### Week 4 Achievements:

#### Knowledge Gained

**What is Amazon RDS?**

- Understood that Amazon RDS is a managed relational database service provided by AWS.
- RDS allows users to set up, operate, and scale a database without managing the underlying physical server or virtual machine.
- RDS is ideal for transactional processing systems (OLTP) such as user management, orders, billing, or structured data.
- RDS supports multiple database engines including Amazon Aurora, MySQL, MariaDB, Oracle, SQL Server, and PostgreSQL.

**Managed Service in RDS**

- Understood that as a managed service, RDS eliminates the need for users to manage the operating system underlying the DB Instance.
- AWS handles administrative tasks like backups, patching, software updates, scaling, Multi-AZ deployments, and failover.
- Users can focus more on database design, connection security, and application operation.

**VPC, Subnet, and DB Subnet Group**

- Understood that a VPC is a virtual private network used to isolate AWS resources.
- Learned how to create a VPC with public and private subnets.
- Public subnets are suitable for EC2 instances requiring internet access.
- Private subnets are ideal for RDS to restrict direct access from the internet.
- Learned that a DB Subnet Group is a collection of subnets designated for RDS.
- A DB Subnet Group should include subnets in at least two Availability Zones to support high availability.

**Security Groups for EC2 and RDS**

- Understood that Security Groups act as instance-level firewalls for EC2 and RDS.
- EC2 Security Group needs inbound rules for:
  - SSH: `22`
  - HTTP: `80`
  - HTTPS: `443`
  - Application port: `5000`
- RDS Security Group needs to open the database port, e.g., `3306` for MySQL/Aurora.
- Configured RDS to only allow inbound traffic from the EC2 Security Group rather than opening public access.

**EC2 Instance as an Application Server**

- Learned how to launch an Amazon Linux EC2 Instance.
- Selected the Amazon Linux 2023 AMI.
- Chose an appropriate Instance Type like `t2.micro` or `t3.micro`.
- Assigned a Key Pair to SSH into the server.
- Connected to the EC2 instance using MobaXterm via Public IP or Public DNS.

**RDS Database Instance**

- Learned how to create an RDS Database Instance using the Standard create method.
- Configured the engine, version, template, master username, password, VPC, and Security Group.
- Monitored the RDS status transition from `Creating` to `Available`.
- Retrieved the Endpoint, Port, and Username to connect the application or EC2 instance to the database.

**Deploying Application Connected to RDS**

- Cloned the source code from GitHub to the EC2 instance.
- Installed Node.js, npm, and required packages like Express, dotenv, and MySQL.
- Created a `.env` file to store database connection details including Endpoint, Database Name, Username, and Password.
- Created the `first_cloud_users` database, `user` table, and inserted sample data.
- Ran the application using `npm start` and accessed it via port `5000`.

**Backup and Restore in RDS**

- Understood that RDS supports automated backups and manual snapshots.
- Checked backups in the Maintenance & backups tab.
- Created a manual snapshot and restored it into a new DB Instance.
- Understood that a restored database will have a new Endpoint, requiring the application's connection string to be updated if switching to the new database.

**Resource Cleanup**

- Deleted the RDS Database Instance, DB Snapshot, and DB Subnet Group.
- Terminated the EC2 Instance after completing the lab.
- Deleted the Security Group, NAT Gateway, Elastic IP, and VPC if no longer needed.
- Understood the importance of checking the Billing Dashboard or Cost Explorer post-cleanup to prevent unexpected charges.

---

#### Hands-on Practice

**Module 1 — Introduction**

- Read the overview of Amazon RDS.
- Learned that RDS is a managed relational database service.
- Differentiated RDS from self-managed databases on EC2.
- Explored concepts:
  - DB Instance
  - Endpoint
  - Database Engine
  - Maintenance Window
  - Backup
  - Snapshot
  - Multi-AZ
  - Read Replica
- 📸 _Evidence: Introduction page of the Amazon RDS workshop._

**Module 2.1 — Create a VPC**

- Created a VPC for the RDS deployment environment.
- Configured the IPv4 CIDR block.
- Created a public subnet for the EC2 instance.
- Created a private subnet for the RDS instance.
- Selected at least two Availability Zones for high availability.
- Verified auto-assign public IPv4 settings for the appropriate subnet.
- 📸 _Evidence: VPC successfully created._
- 📸 _Evidence: Public and private subnets._

**Module 2.2 — Create EC2 Security Group**

- Created a Security Group for the EC2 Instance.
- Configured inbound rules:
  - SSH port `22`
  - HTTP port `80`
  - HTTPS port `443`
  - Custom TCP port `5000`
- Restricted SSH access to personal IP to enhance security.
- Noted the Security Group ID for use when creating EC2 and configuring RDS.
- 📸 _Evidence: EC2 Security Group created._
- 📸 _Evidence: Inbound rules of the EC2 Security Group._

**Module 2.3 — Create RDS Security Group**

- Created a dedicated Security Group for RDS.
- Configured inbound rule for MySQL/Aurora on port `3306`.
- Selected the EC2 Security Group as the source instead of opening to public internet.
- Verified that the RDS Security Group is located in the correct VPC.
- 📸 _Evidence: RDS Security Group created._
- 📸 _Evidence: Rule allowing EC2 connection to RDS._

**Module 2.4 — Create DB Subnet Group**

- Accessed the Amazon RDS Console.
- Created a DB Subnet Group.
- Selected the previously created VPC.
- Selected subnets across at least two Availability Zones.
- Prioritized private subnets for the database.
- Verified the DB Subnet Group after successful creation.
- 📸 _Evidence: DB Subnet Group created._
- 📸 _Evidence: Subnets added to the DB Subnet Group._

**Module 3 — Create EC2 Instance**

- Launched an Amazon Linux EC2 Instance.
- Selected the Amazon Linux 2023 AMI.
- Chose an Instance Type suitable for the lab.
- Assigned a Key Pair for SSH login.
- Attached the previously created EC2 Security Group.
- Launched the instance and waited for the `running` status.
- Connected to the EC2 instance using MobaXterm.
- Verified the terminal prompt after successful SSH login.
- 📸 _Evidence: EC2 Instance in running status._
- 📸 _Evidence: Successful SSH connection to EC2._

**Module 4 — Create RDS Database Instance**

- Accessed the Amazon RDS Console.
- Clicked Create database.
- Selected Standard create.
- Chose the database engine specified in the workshop.
- Configured the DB Instance identifier.
- Set up the master username and master password.
- Selected the VPC, DB Subnet Group, and RDS Security Group.
- Created the database instance.
- Waited for the RDS status to transition to `Available`.
- Retrieved the Endpoint, Port, and Username.
- 📸 _Evidence: RDS Database Instance being created._
- 📸 _Evidence: RDS in Available status._
- 📸 _Evidence: Endpoint and Port details of the RDS._

**Module 5 — Application Deployment**

- SSH'd into the EC2 Instance.
- Installed Git on Amazon Linux.
- Cloned the AWS FCJ Management repository.
- Installed Node.js and npm.
- Installed required dependencies for the application.
- Installed the MySQL client to connect to RDS.
- Created a `.env` file containing:
  - `DB_HOST`
  - `DB_NAME`
  - `DB_USER`
  - `DB_PASS`
- Connected to the RDS using the Endpoint.
- Created the `first_cloud_users` database.
- Created the `user` table.
- Inserted sample data into the table.
- Started the application using the command:

```bash
npm start