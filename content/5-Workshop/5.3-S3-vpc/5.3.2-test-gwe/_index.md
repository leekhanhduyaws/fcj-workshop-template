---
title: "Configure Internet Gateway & Route Tables"
date: "2026-07-09"
weight: 2
chapter: false
pre: "<b>5.3.2. </b>"
---

After creating the VPC and subnets, the next step is to configure the **Internet Gateway**, **Route Table**, and **Security Groups** so that your resources can communicate properly while maintaining network security.

---

# 1. Create an Internet Gateway

An **Internet Gateway (IGW)** enables resources in the **Public Subnet** to communicate with the Internet.

1. In the **VPC Console**, navigate to **Internet gateways** → **Create internet gateway**.

2. Configure the following:

| Field | Value |
|-------|--------|
| Name tag | `flashlearn-igw` |

3. Click **Create internet gateway**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.2/5.3.2.1.png" width="900">
</p>

4. After the Internet Gateway is created:

- Select **flashlearn-igw**
- Choose **Actions → Attach to VPC**
- Select **flashlearn-vpc**
- Click **Attach internet gateway**

---

# 2. Create a Route Table for the Public Subnet

A **Route Table** defines how network traffic is routed within the VPC.

1. Navigate to **Route tables** → **Create route table**.

2. Configure the following:

| Field | Value |
|-------|--------|
| Name | `flashlearn-public-rt` |
| VPC | `flashlearn-vpc` |

3. Click **Create route table**.

4. Add a route to the Internet:

- Select **flashlearn-public-rt**
- Open the **Routes** tab
- Choose **Edit routes**
- Click **Add route**

| Destination | Target |
|-------------|--------|
| `0.0.0.0/0` | `flashlearn-igw` |

5. Click **Save changes**.

6. Associate the Route Table with the Public Subnet:

- Open the **Subnet associations** tab
- Choose **Edit subnet associations**
- Select **flashlearn-public-subnet**
- Click **Save associations**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.2/5.3.2.2.png" width="900">
</p>

---

# 3. Create Security Groups

## Create a Security Group for EC2

1. Navigate to **Security Groups** → **Create security group**.

2. Configure the following:

| Field | Value |
|-------|--------|
| Security group name | `flashlearn-ec2-sg` |
| Description | Security group for FlashLearn EC2 |
| VPC | `flashlearn-vpc` |

3. Add the following inbound rules:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| HTTP | TCP | 80 | `0.0.0.0/0` |
| HTTPS | TCP | 443 | `0.0.0.0/0` |
| Custom TCP | TCP | 5000 | `0.0.0.0/0` |
| SSH | TCP | 22 | My IP |

4. Click **Create security group**.

---

## Create a Security Group for Amazon RDS

1. Click **Create security group**.

2. Configure the following:

| Field | Value |
|-------|--------|
| Security group name | `flashlearn-rds-sg` |
| Description | Security group for FlashLearn RDS |
| VPC | `flashlearn-vpc` |

3. Add the following inbound rule:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| PostgreSQL | TCP | 5432 | `flashlearn-ec2-sg` |

> **Best Practice:** Set the PostgreSQL rule source to the **EC2 Security Group** instead of an IP address. This ensures that only EC2 instances associated with that Security Group can access the database.

4. Click **Create security group**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.2/5.3.2.3.png" width="900">
</p>

---

# Result

After completing this step, you will have:

- An Internet Gateway named `flashlearn-igw` attached to the VPC.
- A Route Table named `flashlearn-public-rt` that allows the Public Subnet to access the Internet.
- A Security Group named `flashlearn-ec2-sg` that allows HTTP, HTTPS, SSH, and application traffic.
- A Security Group named `flashlearn-rds-sg` that allows only the EC2 Security Group to connect to the PostgreSQL database.
