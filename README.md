# Project 1: Using AWS Elastic Beanstalk to Set Up RDS and Access It from an EC2 Instance

## 📌 Objective

This project demonstrates how to:
- Deploy a web application using **AWS Elastic Beanstalk**
- Provision and configure an integrated **Amazon RDS (MySQL)** database
- Access the RDS instance from a separate **EC2 instance** within the same **VPC**
- Securely store RDS credentials using **AWS Systems Manager Parameter Store**
- Perform database operations via a **Python script** from the EC2 instance

---

## 🧱 Architecture Diagram

![Architecture Diagram](./architecture.png)

> This diagram shows:
- Elastic Beanstalk environment with integrated RDS (MySQL)
- EC2 instance (manually launched)
- VPC, Subnet, and Security Group configuration to enable secure access

---

## 🚀 Technologies & Tools

- **AWS Elastic Beanstalk**
- **Amazon RDS (MySQL)**
- **Amazon EC2**
- **Amazon VPC, Subnets, Security Groups**
- **AWS Systems Manager (SSM)**
- **MySQL client / Python Connector**

---

## ⚙️ Project Setup Guide

### 1. Elastic Beanstalk Setup

- Created an **Elastic Beanstalk environment** (`InternshipProject-env`)
- Platform: Python (Preconfigured)
- During environment creation:
  - Enabled the **RDS database** option
  - Chose `MySQL` engine with version `8.0.41`
  - Set instance type as `db.t3.micro` with 5 GB storage
  - Made sure it was in the same **VPC** as the EC2

📸 ![Beanstalk RDS Config](./Screenshot\ \(94\).png)

---

### 2. RDS Database Configuration

- The RDS DB (`awseb-e-ixuepimter-stack-awsebrdsdatabase-*`) was auto-created
- Engine: MySQL Community
- Availability Zone: `us-east-1b`
- Class: `db.t3.small`
- Public access **disabled** for better security
- Security group rules allowed only:
  - Elastic Beanstalk EC2 instance
  - Manually created EC2 instance

📸 ![RDS Console](./Screenshot\ \(99\).png)

---

### 3. EC2 Instance Setup

- Launched a **separate EC2 instance**
- Installed:
  ```bash
  sudo apt update
  sudo apt install mysql-client python3-pip
  pip install mysql-connector-python
