---
title: "Workshop"
date: 2026-07-09
weight: 5
chapter: false
pre: "<b>5. </b>"
---

**FlashLearn** is an intelligent English learning web application that enables users to create, organize, and review vocabulary using a **Flashcard** system powered by the **Spaced Repetition** learning technique.

In this workshop, you will deploy the **FlashLearn** application built with **ASP.NET Core 8.0** to **Amazon Web Services (AWS)** using a production-style three-tier architecture. Upon completion, the application will authenticate users with **Amazon Cognito**, run on **Amazon EC2**, store application data in **Amazon RDS for PostgreSQL**, and manage uploaded images in **Amazon S3**.

---

## Architecture Overview

```text
                [User]
                   │
                HTTPS
                   │
                   ▼
          [Amazon Cognito]
 Authentication & Authorization
                   │
                   ▼
     [Amazon EC2 - ASP.NET Core 8.0]
   Application Server (Public Subnet)
            │                   │
            ▼                   ▼
[Amazon RDS for PostgreSQL]   [Amazon S3]
      (Private Subnet)      (Image Storage)
```

The deployed architecture provides the following capabilities:

- Authenticate and authorize users with Amazon Cognito.
- Host the ASP.NET Core 8.0 application on Amazon EC2.
- Store application data in Amazon RDS for PostgreSQL.
- Store uploaded Flashcard images in Amazon S3.
- Improve security by separating application and database resources using Public and Private Subnets.

---

## AWS Services Used

| AWS Service | Purpose |
|------------|---------|
| **Amazon VPC** | Create an isolated virtual network with Public and Private Subnets. |
| **Amazon EC2** | Host and run the ASP.NET Core 8.0 web application. |
| **Amazon RDS for PostgreSQL** | Provide a managed PostgreSQL database service. |
| **Amazon S3** | Store Flashcard images uploaded by users. |
| **Amazon Cognito** | Handle user authentication and issue JWT access tokens. |

---

## Learning Objectives

By completing this workshop, you will be able to:

- Design and configure a Virtual Private Cloud (VPC).
- Deploy an ASP.NET Core 8.0 application on Amazon EC2.
- Connect the application to Amazon RDS for PostgreSQL.
- Store and retrieve files using Amazon S3.
- Implement user authentication with Amazon Cognito.
- Deploy a secure and scalable ASP.NET Core application on AWS following AWS best practices.

---

## Workshop Content

{{% children showhidden="false" /%}}
