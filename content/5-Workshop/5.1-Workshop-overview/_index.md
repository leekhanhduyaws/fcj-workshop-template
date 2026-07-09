---
title: "Introduction"
date: 2026-07-09
weight: 1
chapter: false
pre: "<b>5.1. </b>"
---

## What is FlashLearn?

**FlashLearn** is an intelligent English learning web application built with **ASP.NET Core 8.0**. It enables users to:

- Create **flashcard decks** with English–Vietnamese vocabulary
- Practice vocabulary using the **Spaced Repetition** learning method
- Attach **images** to each flashcard
- Compete with other users in **real-time vocabulary battles** powered by SignalR
- Track learning progress and maintain a daily learning **streak**

The application currently uses **SQLite** in the local development environment. In this workshop, you will migrate the entire application to **AWS Cloud** and replace SQLite with a fully managed **Amazon RDS for PostgreSQL** database.

---

## System Architecture

The application follows a **3-Tier Architecture** deployed inside a **Virtual Private Cloud (VPC)** with properly separated public and private subnets.

![FlashLearn AWS Architecture](/images/5-Workshop/architecture-overview.png)

### Architecture Components

| Layer | Component | AWS Service |
| ------ | --------- | ----------- |
| **Presentation** | Web UI, SignalR | Amazon EC2 (Public Subnet) |
| **Authentication** | User Sign Up / Sign In | Amazon Cognito |
| **Business Logic** | ASP.NET Core Controllers | Amazon EC2 (Public Subnet) |
| **Database** | User and Flashcard Data | Amazon RDS for PostgreSQL (Private Subnet) |
| **Storage** | Flashcard Images | Amazon S3 |

### Application Workflow

```text
User
  │
  ├─► [1] Amazon Cognito
  │         │
  │         └─ Authenticate user and return a JWT token
  │
  ├─► [2] Amazon EC2 (ASP.NET Core 8.0)
  │         │
  │         ├─► Amazon RDS for PostgreSQL
  │         │      Read and write application data
  │         │
  │         └─► Amazon S3
  │                Upload and download flashcard images
  │
  └─► [3] SignalR Hub
            Real-time multiplayer vocabulary battles
```

---

## Workshop Objectives

After completing this workshop, you will be able to:

- Configure a secure **Amazon VPC** with public and private subnets
- Deploy an **ASP.NET Core 8.0** application on Amazon EC2
- Migrate the database from **SQLite** to **Amazon RDS for PostgreSQL**
- Store user-uploaded media in **Amazon S3**
- Implement user authentication using **Amazon Cognito**
- Clean up AWS resources to prevent unnecessary charges

---

## Estimated Duration

| Step | Task | Estimated Time |
| ---- | ---- | -------------- |
| 5.2 | Environment Setup | ~30 minutes |
| 5.3 | Configure Amazon VPC | ~20 minutes |
| 5.4 | Deploy Amazon RDS | ~25 minutes |
| 5.5 | Deploy EC2 and Application | ~45 minutes |
| 5.6 | Configure Amazon S3 | ~20 minutes |
| 5.7 | Integrate Amazon Cognito | ~30 minutes |
| 5.8 | Resource Cleanup | ~15 minutes |
| **Total** | | **~3 hours** |

---

## Estimated Cost

> **AWS Free Tier** includes many of the services used in this workshop for new AWS accounts during the first 12 months. If your account is no longer eligible for the Free Tier, the estimated monthly cost is:

| AWS Service | Configuration | Estimated Monthly Cost |
| ------------ | ------------- | ---------------------- |
| Amazon EC2 | t3.micro (1 On-Demand instance) | ~$8.47 |
| Amazon RDS | db.t3.micro PostgreSQL (Single-AZ) | ~$15.33 |
| Amazon S3 | 5 GB Standard Storage | ~$0.12 |
| Amazon Cognito | Fewer than 50,000 Monthly Active Users | $0.00 |
| **Total** | | **~$24/month** |

> **Important:** Complete **Step 5.8 – Resource Cleanup** immediately after finishing the workshop to avoid unexpected AWS charges.
