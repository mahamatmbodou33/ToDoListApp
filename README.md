### 🧰 AWS To-Do List Application — Two-Tier Architecture Deployment
📘 Overview

This project demonstrates how to deploy a To-Do List web application using a two-tier architecture on AWS. The setup is designed for scalability, security, and cost-efficiency, using EC2 for the application layer and Amazon RDS for the database layer, with an Application Load Balancer (ALB) distributing traffic between instances.

## 🏗️ Architecture Summary
- Application Layer: Two EC2 instances host the Node.js application to ensure high availability.
- Database Layer: Amazon RDS (MySQL) stores and manages data securely.
- Load Balancing: An ALB distributes incoming requests evenly across both EC2 instances.
- Security & Networking: Security Groups and VPC configurations protect communication between components.

## 🖼️ Architecture Diagram

<img width="648" height="481" alt="Screenshot 2025-10-15 121323" src="https://github.com/user-attachments/assets/8975435b-b411-4b18-a316-b9ff0c089293" />

## ☁️ AWS Services Used
Service	Description	Category:
- Amazon EC2	hosts the Node.js app on two instances for redundancy.	Compute
- Amazon RDS (MySQL)	Manages relational database for app data.	Database
- Application Load Balancer (ALB)	balances traffic between EC2 instances.	Networking
- Amazon VPC	provides an isolated network environment with public/private subnets.	Networking
- Security Groups	Control inbound/outbound traffic.	Security
- 
## ⚙️ Project Setup
# 1️⃣ Prerequisites
- AWS Account
- Basic knowledge of EC2, RDS, and VPC
- MySQL Workbench or any SQL client
- Git installed locally
# 2️⃣ Clone the Repository
- git clone https://github.com/techwithlucy/zero-to-cloud.git
- cd projects/intermediate/project5
# 3️⃣ Setup VPC and Networking
- Create VPC (10.0.0.0/16)
- Create 2 public subnets for EC2 and 2 private subnets for RDS
- Create an Internet Gateway and attach it to the VPC
- Configure Route Tables for proper communication
- Create Security Groups for Web and Database layers
# 4️⃣ Database Layer — RDS Setup
- Launch an RDS MySQL instance in a private subnet.
- Use a Bastion Host (EC2 in public subnet) to access RDS securely.
- Create your application database and tables:
- CREATE DATABASE TodoAppDB;
- USE TodoAppDB;
- CREATE TABLE Tasks (
  id INT AUTO_INCREMENT PRIMARY KEY,
  task_name VARCHAR(255) NOT NULL,
  task_description TEXT,
  due_date DATE NULL,
  completed BOOLEAN DEFAULT FALSE
);
# 5️⃣ Application Layer — EC2 Setup
- Launch two EC2 instances in public subnets.
- Connect via SSH and install dependencies:
- sudo yum update -y
- sudo yum install -y nodejs git nginx
- Clone the app repo and create an environment file:

DB_HOST="<your-rds-endpoint>"
DB_USER="<your-db-username>"
DB_PASSWORD="<your-db-password>"
DB_NAME="TodoAppDB"
PORT="3306"
API_BASE_URL="http://<your-alb-dns-name>"
- Install dependencies and configure Nginx as a reverse proxy.
- Start the application and verify it works via EC2 Public IP.
# 6️⃣ Configure Application Load Balancer (ALB)
- Create an ALB and target group for EC2 instances.
- Assign the proper security group and VPC subnets.
- Register both EC2 instances as targets.
-Access app through ALB DNS name:
http://<ALB-DNS-Name>
# 🔒 Security Highlights
- Used private subnets for RDS to prevent public access.
- Implemented Security Groups for controlled traffic flow.

## 🚀 Outcome
<img width="917" height="853" alt="Screenshot 2025-10-15 001835" src="https://github.com/user-attachments/assets/0d379bb8-6868-4f64-a641-9ff6dfb914d9" />

A fully functional and secure To-Do List web app hosted on AWS infrastructure with automated load balancing and a managed database backend.
