---
title: "Thiết lập mạng riêng ảo (VPC)"
date: "2026-07-09"
weight: 3
chapter: false
pre: "<b>5.3. </b>"
---

**Amazon Virtual Private Cloud (Amazon VPC)** cho phép bạn tạo một mạng riêng ảo trên AWS, giúp triển khai các tài nguyên trong một môi trường được cô lập và bảo mật.

## Kiến trúc mạng

Trong workshop này, bạn sẽ xây dựng kiến trúc mạng như sau:

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

## Tại sao cần tách Public Subnet và Private Subnet?

| Tiêu chí | Public Subnet | Private Subnet |
| -------- | ------------- | -------------- |
| **Kết nối Internet** | Có | Không |
| **Tài nguyên triển khai** | EC2 (Web Server) | Amazon RDS (Database) |
| **Mức độ bảo mật** | Trung bình | Cao |

> **Best Practice:** Không nên cho phép cơ sở dữ liệu truy cập trực tiếp từ Internet. Đặt Amazon RDS trong **Private Subnet** giúp cô lập hoàn toàn cơ sở dữ liệu, chỉ các EC2 instance trong VPC mới có thể kết nối đến.

## Nội dung thực hiện

{{% children showhidden="false" /%}}
