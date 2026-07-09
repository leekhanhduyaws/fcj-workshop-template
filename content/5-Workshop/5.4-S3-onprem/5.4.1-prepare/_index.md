---
title: "Create Amazon RDS PostgreSQL"
date: "2026-07-09"
weight: 1
chapter: false
pre: "<b>5.4.1. </b>"
---

In this section, you will create an **Amazon RDS for PostgreSQL** instance to store data for the FlashLearn application. First, you will create a **DB Subnet Group**, then provision the **RDS instance**, and finally save the database connection details for later use.

---

# 1. Create a DB Subnet Group

A **DB Subnet Group** specifies which **Private Subnets** Amazon RDS can use when deploying the database instance.

1. Open the **Amazon RDS Console** → **Subnet groups** → **Create DB subnet group**

2. Configure the following settings:

| Field | Value |
|--------|-------|
| Name | `flashlearn-db-subnet-group` |
| Description | Subnet group for FlashLearn RDS |
| VPC | `flashlearn-vpc` |

3. Under **Add subnets**, add both Private Subnets:

- **ap-southeast-1a** → `flashlearn-private-subnet-1 (10.0.2.0/24)`
- **ap-southeast-1b** → `flashlearn-private-subnet-2 (10.0.3.0/24)`

4. Click **Create**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.4-S3-onprem/5.4.1/1.png" width="900">
</p>

---

# 2. Create an Amazon RDS PostgreSQL Instance

1. Navigate to **Databases** → **Create database**.

2. Under **Engine options**:

- Engine type: **PostgreSQL**
- Engine version: **PostgreSQL 16.x**

3. Under **Templates**, select:

- **Free tier** (if your AWS account is still eligible)
- Or **Dev/Test**

4. Configure the database settings:

| Field | Value |
|--------|-------|
| DB instance identifier | `flashlearn-db` |
| Master username | `flashlearn_admin` |
| Master password | Create a strong password |
| Confirm password | Re-enter the password |

5. Configure the instance:

| Field | Value |
|--------|-------|
| DB instance class | `db.t3.micro` |
| Storage type | `gp2` |
| Allocated storage | `20 GB` |
| Storage autoscaling | Disabled |

6. Configure connectivity:

| Field | Value |
|--------|-------|
| VPC | `flashlearn-vpc` |
| DB subnet group | `flashlearn-db-subnet-group` |
| Public access | **No** |
| VPC security group | `flashlearn-rds-sg` |
| Availability Zone | `ap-southeast-1a` |

> **Note:** Set **Public access = No** to ensure the database cannot be accessed directly from the Internet.

7. Configure additional settings:

| Field | Value |
|--------|-------|
| Initial database name | `flashlearn` |
| Backup retention period | `7 days` |
| Encryption | Enabled |

8. Click **Create database** and wait approximately **5–10 minutes** for the RDS instance to become available.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.4-S3-onprem/5.4.1/2.png" width="900">
</p>

---

# 3. Save the Connection Information

Once the RDS instance status changes to **Available**, save the connection details for use in the upcoming deployment steps.

1. Select the **flashlearn-db** database.
2. Open the **Connectivity & security** tab.
3. Copy the following information:

- Endpoint
- Port: `5432`
- Master username

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.4-S3-onprem/5.4.1/3.png" width="900">
</p>

---

# Result

After completing this section, you will have:

- A **DB Subnet Group** spanning both Private Subnets.
- An **Amazon RDS PostgreSQL** instance in the **Available** state.
- An RDS instance that accepts connections only from the EC2 instance through its Security Group.
- The required connection details (**Endpoint**, **Username**, and **Password**) for use in the next deployment steps.
