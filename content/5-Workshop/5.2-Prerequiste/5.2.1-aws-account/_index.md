---
title: "Create an AWS Account"
date: "2026-07-09"
weight: 1
chapter: false
pre: "<b>5.2.1. </b>"
---

To complete this workshop, you need an AWS account. If you do not already have one, follow the instructions below.

## 1. Create an AWS Account

1. Visit https://aws.amazon.com and choose **Create an AWS Account**.

2. Complete the registration form:

   - **Email address**: Enter your email address.
   - **AWS account name**: Choose an account name (for example, `flashlearn-workshop`).

3. Select the **Free Tier** plan when prompted to choose an account type.

4. Enter your payment information. AWS may temporarily charge **$1** to verify your payment method. This amount will be refunded shortly afterward.

5. Complete the phone verification process.

6. Select the **Basic Support Plan** (Free).

---

## 2. Enable Multi-Factor Authentication (MFA)

After creating your account, you should enable **Multi-Factor Authentication (MFA)** for the root user to improve account security.

1. Sign in to the **AWS Management Console**.

2. Click your account name in the upper-right corner, then select **Security credentials**.

3. Under **Multi-factor authentication (MFA)**, choose **Assign MFA device**.

4. Select **Authenticator app** and follow the on-screen instructions.

---

## 3. Create an IAM User for the Workshop

> It is not recommended to use the root account for daily tasks. Instead, create an IAM user with the appropriate permissions.

1. Search for **IAM** in the AWS Management Console, then navigate to **Users** → **Create user**.

2. Configure the new user:

   - **User name**: `flashlearn-admin`
   - Enable **Provide user access to the AWS Management Console**.
   - Select **I want to create an IAM user**.
   - Set a **Console password**.

3. Grant permissions by selecting **Attach policies directly**, then search for and choose **AdministratorAccess**.

4. Choose **Create user** and save the sign-in credentials in a secure location.

---

## 4. Configure an AWS Budget

To avoid unexpected charges, create an AWS Budget to monitor your spending.

1. Navigate to **Billing and Cost Management** → **Budgets** → **Create budget**.

2. Select **Use a template** → **Zero spend budget**.

3. Enter your email address for notifications, then choose **Create budget**.

> The **Zero spend budget** sends an email notification whenever any AWS service incurs a charge, even as little as **$0.01**, helping you detect unexpected costs as early as possible.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.2-Prerequisite/budget.png" width="700">
</p>

<p align="center">
  <em>Figure 1. Configuring an AWS Zero Spend Budget.</em>
</p>

---

## Result

After completing this section, you will have:

- An AWS account with **Multi-Factor Authentication (MFA)** enabled.
- An IAM user named `flashlearn-admin` with **AdministratorAccess** permissions.
- An AWS **Zero Spend Budget** configured to help monitor and control costs.
