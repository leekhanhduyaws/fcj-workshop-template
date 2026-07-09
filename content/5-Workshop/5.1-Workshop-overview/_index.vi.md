---
title: "Giới thiệu"
date: 2026-07-09
weight: 1
chapter: false
pre: "<b>5.1. </b>"
---

## FlashLearn là gì?

**FlashLearn** là ứng dụng web học tiếng Anh được phát triển bằng **ASP.NET Core 8.0**, giúp người dùng học từ vựng thông qua hệ thống **Flashcard** kết hợp thuật toán **Spaced Repetition**.

Ứng dụng cung cấp các tính năng:

- **Tạo và quản lý Flashcard Decks**
- **Ôn tập theo thuật toán Spaced Repetition**
- **Đính kèm hình ảnh cho Flashcard**
- **Battle Mode thời gian thực bằng SignalR**
- **Theo dõi Streak và tiến độ học tập**

Phiên bản hiện tại sử dụng **SQLite** trong môi trường phát triển. Trong workshop này, bạn sẽ triển khai toàn bộ hệ thống lên **Amazon Web Services (AWS)** và chuyển cơ sở dữ liệu sang **Amazon RDS for PostgreSQL**.

---

## Kiến trúc hệ thống

Ứng dụng được triển khai theo mô hình **Three-Tier Architecture** trong một **Amazon Virtual Private Cloud (Amazon VPC)** với Public Subnet và Private Subnet được tách biệt nhằm tăng cường bảo mật.

![Kiến trúc FlashLearn AWS](/images/5-Workshop/5.1-Workshop-overview/aws_whiteboard.png)

### Các thành phần chính

| Layer | Thành phần | Dịch vụ AWS |
|-------|------------|-------------|
| **Presentation** | Web UI, SignalR | Amazon EC2 (Public Subnet) |
| **Authentication** | User Authentication | Amazon Cognito |
| **Business Logic** | ASP.NET Core Controllers | Amazon EC2 (Public Subnet) |
| **Database** | User & Flashcard Data | Amazon RDS for PostgreSQL (Private Subnet) |
| **Storage** | Flashcard Images | Amazon S3 |

---

### Luồng hoạt động

```text
User
 │
 ├──► Amazon Cognito
 │      └── Authenticate user and issue JWT Token
 │
 ├──► Amazon EC2 (ASP.NET Core 8.0)
 │      │
 │      ├──► Amazon RDS for PostgreSQL
 │      │        Read/Write application data
 │      │
 │      └──► Amazon S3
 │               Upload/Download Flashcard images
 │
 └──► SignalR Hub
         Real-time Battle Mode
```

---

## Mục tiêu workshop

Sau khi hoàn thành workshop, bạn sẽ có thể:

- Thiết lập Amazon VPC với Public và Private Subnets.
- Triển khai ứng dụng ASP.NET Core 8.0 lên Amazon EC2.
- Di chuyển dữ liệu từ SQLite sang Amazon RDS for PostgreSQL.
- Lưu trữ hình ảnh bằng Amazon S3.
- Tích hợp xác thực người dùng với Amazon Cognito.
- Dọn dẹp tài nguyên AWS để tránh phát sinh chi phí không cần thiết.

---

## Thời gian thực hiện

| Bước | Nội dung | Thời gian |
|------|----------|-----------|
| **5.2** | Chuẩn bị môi trường | ~30 phút |
| **5.3** | Thiết lập Amazon VPC | ~20 phút |
| **5.4** | Triển khai Amazon RDS | ~25 phút |
| **5.5** | Triển khai Amazon EC2 & ASP.NET Core | ~45 phút |
| **5.6** | Cấu hình Amazon S3 | ~20 phút |
| **5.7** | Tích hợp Amazon Cognito | ~30 phút |
| **5.8** | Dọn dẹp tài nguyên | ~15 phút |
| **Tổng** | | **~3 giờ** |

---

## Chi phí ước tính

> **AWS Free Tier** cho phép hầu hết người dùng mới thực hiện workshop mà không phát sinh chi phí. Nếu tài khoản của bạn đã hết Free Tier, chi phí ước tính như sau:

| Dịch vụ | Cấu hình | Chi phí/tháng |
|---------|----------|---------------|
| Amazon EC2 (t3.micro) | 1 On-Demand Instance | ~$8.47 |
| Amazon RDS (db.t3.micro) | PostgreSQL, Single-AZ | ~$15.33 |
| Amazon S3 | 5 GB Standard Storage | ~$0.12 |
| Amazon Cognito | < 50,000 Monthly Active Users | $0.00 |
| **Tổng** | | **~$24/tháng** |

> **Lưu ý:** Sau khi hoàn thành workshop, hãy thực hiện **Bước 5.8 – Dọn dẹp tài nguyên** để xóa các tài nguyên AWS đã tạo và tránh phát sinh chi phí ngoài ý muốn.
