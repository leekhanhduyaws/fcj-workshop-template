---
title: "Create VPC & Subnets"
date: "2026-07-09"
weight: 1
chapter: false
pre: "<b>5.3.1. </b>"
---

In this step, you will create a new Amazon VPC and configure separate subnets for different application tiers.

---

# 1. Create a VPC

1. Sign in to the **AWS Management Console** → Search for **VPC** → Select **VPC**.

2. Choose **Create VPC**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1-vpc-created.png" width="900">
</p>

3. Configure the VPC using the following settings:

| Field | Value |
|--------|-------|
| **Resources to create** | VPC only |
| **Name tag** | `flashlearn-vpc` |
| **IPv4 CIDR block** | `10.0.0.0/16` |
| **IPv6 CIDR block** | No IPv6 CIDR block |
| **Tenancy** | Default |

4. Choose **Create VPC**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1.1.png" width="900">
</p>

---

# 2. Create a Public Subnet

The Public Subnet will host the Amazon EC2 instance running the FlashLearn application.

1. In the **VPC Console**, select **Subnets** → **Create subnet**.

2. Configure the subnet as follows:

| Field | Value |
|--------|-------|
| **VPC ID** | Select `flashlearn-vpc` |
| **Subnet name** | `flashlearn-public-subnet` |
| **Availability Zone** | `ap-southeast-1a` |
| **IPv4 CIDR block** | `10.0.1.0/24` |

3. Choose **Create subnet**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1.2.png" width="900">
</p>

4. Enable **Auto-assign public IPv4 address** for the subnet:

- Select `flashlearn-public-subnet`.
- Choose **Actions** → **Edit subnet settings**.
- Select **Enable auto-assign public IPv4 address**.
- Choose **Save**.

---

# 3. Create Private Subnets

The Private Subnets will host the Amazon RDS database and will not have direct Internet access.

1. In **Subnets**, choose **Create subnet**.

2. Configure the first private subnet:

| Field | Value |
|--------|-------|
| **VPC ID** | Select `flashlearn-vpc` |
| **Subnet name** | `flashlearn-private-subnet-1` |
| **Availability Zone** | `ap-southeast-1a` |
| **IPv4 CIDR block** | `10.0.2.0/24` |

3. Choose **Add new subnet** to create a second private subnet. Amazon RDS requires at least two Availability Zones for a DB subnet group.

| Field | Value |
|--------|-------|
| **Subnet name** | `flashlearn-private-subnet-2` |
| **Availability Zone** | `ap-southeast-1b` |
| **IPv4 CIDR block** | `10.0.3.0/24` |

4. Choose **Create subnet**.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1.3.png" width="900">
</p>

---

## Result

After completing this section, you will have successfully created:

- A VPC named `flashlearn-vpc` with the CIDR block `10.0.0.0/16`
- A Public Subnet (`10.0.1.0/24`) in `ap-southeast-1a`
- A Private Subnet (`10.0.2.0/24`) in `ap-southeast-1a`
- A Private Subnet (`10.0.3.0/24`) in `ap-southeast-1b`

These networking resources will be used in the following sections to configure the Internet Gateway, Route Tables, Amazon EC2, and Amazon RDS.
