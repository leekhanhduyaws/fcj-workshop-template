---
title: "Set Up the Development Environment"
date: "2026-07-09"
weight: 2
chapter: false
pre: "<b>5.2.2. </b>"
---

In this section, you will install the essential tools required to work with AWS and prepare your local development environment for the FlashLearn application.

## 1. Install AWS CLI

The **AWS Command Line Interface (AWS CLI)** enables you to interact with AWS services directly from the command line.

### Windows

Download the installer from the official AWS website:

```text
https://awscli.amazonaws.com/AWSCLIV2.msi
```

After the installation is complete, verify that AWS CLI has been installed successfully:

```bash
aws --version
# aws-cli/2.x.x Python/3.x.x Windows/x86_64
```

### Configure AWS CLI

Run the following command and provide the credentials for the IAM user created in **Section 5.2.1**:

```bash
aws configure
```

```text
AWS Access Key ID [None]: <IAM User Access Key>
AWS Secret Access Key [None]: <IAM User Secret Access Key>
Default region name [None]: ap-southeast-1
Default output format [None]: json
```

> 💡 To create an **Access Key**, navigate to **IAM → Users → `flashlearn-admin` → Security credentials → Create access key**.

---

## 2. Install .NET SDK 8.0

The **FlashLearn** application is built with **.NET 8.0**. Installing the .NET SDK is required to build and publish the project.

Download the .NET 8.0 SDK from:

```text
https://dotnet.microsoft.com/download/dotnet/8.0
```

Verify the installation:

```bash
dotnet --version
# 8.0.x
```

---

## 3. Install Git

**Git** is required to clone the project repository and manage source code.

Download Git from:

```text
https://git-scm.com/downloads
```

Verify the installation:

```bash
git --version
# git version 2.x.x
```

---

## 4. Install an SSH Client

An SSH client is required to establish secure connections to Amazon EC2 instances.

- **Windows 10/11** includes **OpenSSH** by default.
- To verify that SSH is available, open **PowerShell** and run:

```bash
ssh
```

---

## 5. Clone the FlashLearn Source Code

Clone the repository to your local machine:

```bash
git clone <your FlashLearn repository URL>
cd WebhocTiengAnhFlashLearn
```

Verify that the project can be built successfully:

```bash
dotnet restore
dotnet build
```

Expected output:

```text
Build succeeded.
    0 Warning(s)
    0 Error(s)
```

---

## Result

After completing this section, you will have:

- AWS CLI installed and configured with your IAM user credentials.
- .NET SDK 8.0 installed on your local machine.
- Git and an SSH client ready for use.
- The FlashLearn source code cloned locally and successfully built.
