---
title: "Deploy the Database (Amazon RDS)"
date: "2026-07-09"
weight: 4
chapter: false
pre: "<b>5.4. </b>"
---

**Amazon Relational Database Service (Amazon RDS)** is a fully managed relational database service that automates routine administration tasks such as backups, patching, monitoring, and high availability.

## Why migrate from SQLite to Amazon RDS?

The FlashLearn application initially uses **SQLite**, which stores data locally on the application server. While this is suitable for development, it is not recommended for production environments.

By migrating to **Amazon RDS for PostgreSQL**, the application benefits from improved scalability, reliability, and managed database operations.

| Feature | SQLite (Local) | Amazon RDS (PostgreSQL) |
|---------|----------------|--------------------------|
| **Storage** | Local database file | Managed database service |
| **Backup** | Manual | Automatic backups (7 days) |
| **Scalability** | Limited | Easy to scale vertically |
| **Availability** | Single point of failure | Multi-AZ option available |
| **Management** | Self-managed | Fully managed by AWS |

Amazon RDS also integrates seamlessly with Amazon EC2 inside the same VPC, allowing secure communication without exposing the database directly to the Internet.

## Contents

{{% children showhidden="false" /%}}
