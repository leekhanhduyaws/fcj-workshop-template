---
title: "Set Up Virtual Private Cloud (VPC)"
date: "2026-07-09"
weight: 3
chapter: false
pre: "<b>5.3. </b>"
---

**Amazon Virtual Private Cloud (Amazon VPC)** enables you to create an isolated virtual network within AWS, allowing you to securely deploy and manage your cloud resources.

## Network Architecture

In this workshop, you will build the following network architecture:

```text
VPC: 10.0.0.0/16 (FlashLearn VPC)
│
├── Public Subnet: 10.0.1.0/24 (ap-southeast-1a)
│   ├── Internet Gateway
│   └── EC2 (ASP.NET Core Application)
│
└── Private Subnet: 10.0.2.0/24 (ap-southeast-1a)
    └── Amazon RDS for PostgreSQL
```

## Why Separate Public and Private Subnets?

| Criteria | Public Subnet | Private Subnet |
| -------- | ------------- | -------------- |
| **Internet Access** | Yes | No |
| **Hosted Resources** | EC2 (Web Server) | Amazon RDS (Database) |
| **Security Level** | Moderate | High |

> **Best Practice:** A database should never be exposed directly to the Internet. Deploying Amazon RDS in a **Private Subnet** isolates the database from external access, ensuring that only EC2 instances within the VPC can connect to it securely.

## Workshop Tasks

{{% children showhidden="false" /%}}
