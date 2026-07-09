---
title: "Introduction"
date: 2026-07-09
weight: 1
chapter: false
pre: "<b>5.1. </b>"
---

## What is FlashLearn?

**FlashLearn** is an English vocabulary learning web application built with **ASP.NET Core 8.0**. It helps users learn and review vocabulary using **Flashcards** combined with the **Spaced Repetition** learning technique.

The application provides the following features:

- **Create and manage Flashcard Decks**
- **Review vocabulary using the Spaced Repetition algorithm**
- **Attach images to Flashcards**
- **Real-time Battle Mode powered by SignalR**
- **Track learning progress and daily streaks**

The current version uses **SQLite** as the local development database. In this workshop, you will deploy the entire application to **Amazon Web Services (AWS)** and migrate the database to **Amazon RDS for PostgreSQL**.

---

## System Architecture

The application is deployed using a **Three-Tier Architecture** within an **Amazon Virtual Private Cloud (Amazon VPC)**. Public and Private Subnets are separated to enhance security and follow AWS best practices.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.1-Workshop-overview/aws_whiteboard.png" width="700">
</p>

<p align="center">
  <em>Figure 1. FlashLearn deployment architecture on AWS.</em>
</p>

### Main Components

| Layer | Component | AWS Service |
|-------|-----------|-------------|
| **Presentation** | Web UI, SignalR | Amazon EC2 (Public Subnet) |
| **Authentication** | User Authentication | Amazon Cognito |
| **Business Logic** | ASP.NET Core Controllers | Amazon EC2 (Public Subnet) |
| **Database** | User and Flashcard Data | Amazon RDS for PostgreSQL (Private Subnet) |
| **Storage** | Flashcard Images | Amazon S3 |

---

### Application Workflow

```text
User
 │
 ├──► Amazon Cognito
 │      └── Authenticate user and issue JWT Token
 │
 ├──► Amazon EC2 (ASP.NET Core 8.0)
 │      │
 │      ├──► Amazon RDS for PostgreSQL
 │      │        Read and write application data
 │      │
 │      └──► Amazon S3
 │               Upload and download Flashcard images
 │
 └──► SignalR Hub
         Real-time Battle Mode
```

---

## Workshop Objectives

By the end of this workshop, you will be able to:

- Configure an Amazon VPC with Public and Private Subnets.
- Deploy an ASP.NET Core 8.0 application on Amazon EC2.
- Migrate data from SQLite to Amazon RDS for PostgreSQL.
- Store and manage images using Amazon S3.
- Integrate Amazon Cognito for user authentication.
- Clean up AWS resources to prevent unnecessary charges.

---

## Estimated Duration

| Step | Activity | Estimated Time |
|------|----------|----------------|
| **5.2** | Prepare the environment | ~30 minutes |
| **5.3** | Configure Amazon VPC | ~20 minutes |
| **5.4** | Deploy Amazon RDS | ~25 minutes |
| **5.5** | Deploy Amazon EC2 and ASP.NET Core application | ~45 minutes |
| **5.6** | Configure Amazon S3 | ~20 minutes |
| **5.7** | Integrate Amazon Cognito | ~30 minutes |
| **5.8** | Clean up resources | ~15 minutes |
| **Total** | | **~3 hours** |

---

## Estimated Cost

> **AWS Free Tier** allows most new AWS accounts to complete this workshop at no additional cost. If your account is no longer eligible for the Free Tier, the estimated monthly cost is as follows:

| AWS Service | Configuration | Estimated Monthly Cost |
|-------------|---------------|------------------------|
| Amazon EC2 (t3.micro) | 1 On-Demand Instance | ~$8.47 |
| Amazon RDS (db.t3.micro) | PostgreSQL, Single-AZ | ~$15.33 |
| Amazon S3 | 5 GB Standard Storage | ~$0.12 |
| Amazon Cognito | Fewer than 50,000 Monthly Active Users | $0.00 |
| **Total** | | **~$24/month** |

> **Note:** After completing the workshop, be sure to follow **Step 5.8 – Clean Up Resources** to delete all AWS resources created during the workshop and avoid unexpected charges.
