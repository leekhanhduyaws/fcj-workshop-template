---
title: "Workshop"
date: 2026-07-09
weight: 5
chapter: false
pre: "<b>5. </b>"
---

**FlashLearn** là một ứng dụng web học tiếng Anh thông minh, cho phép người dùng tạo, quản lý và ôn luyện từ vựng thông qua hệ thống **Flashcard** kết hợp thuật toán **Spaced Repetition** nhằm tối ưu hiệu quả ghi nhớ.

Trong workshop này, bạn sẽ từng bước triển khai ứng dụng **FlashLearn** sử dụng **ASP.NET Core 8.0** lên **Amazon Web Services (AWS)** theo mô hình triển khai thực tế dành cho doanh nghiệp. Sau khi hoàn thành, ứng dụng sẽ hỗ trợ xác thực người dùng bằng **Amazon Cognito**, chạy trên **Amazon EC2**, lưu trữ dữ liệu trong **Amazon RDS PostgreSQL** và quản lý hình ảnh bằng **Amazon S3**.

---

## Những gì bạn sẽ xây dựng

```text
                [Người dùng]
                     │
                  HTTPS
                     │
                     ▼
             [Amazon Cognito]
          Xác thực & phân quyền
                     │
                     ▼
        [Amazon EC2 - ASP.NET Core]
      Máy chủ ứng dụng (Public Subnet)
              │                 │
              ▼                 ▼
 [Amazon RDS PostgreSQL]   [Amazon S3]
    (Private Subnet)      (Lưu trữ hình ảnh)
```

Kiến trúc trên giúp ứng dụng:

- Xác thực người dùng bằng Amazon Cognito.
- Chạy ứng dụng ASP.NET Core trên Amazon EC2.
- Lưu trữ dữ liệu PostgreSQL trong Amazon RDS.
- Lưu trữ ảnh Flashcard trên Amazon S3.
- Phân tách tài nguyên giữa Public Subnet và Private Subnet để tăng tính bảo mật.

---

## Các dịch vụ AWS sử dụng

| Dịch vụ | Mục đích |
|---------|----------|
| **Amazon VPC** | Xây dựng hạ tầng mạng riêng, phân chia Public Subnet và Private Subnet. |
| **Amazon EC2** | Triển khai và vận hành ứng dụng ASP.NET Core 8.0. |
| **Amazon RDS for PostgreSQL** | Quản lý cơ sở dữ liệu PostgreSQL trên AWS. |
| **Amazon S3** | Lưu trữ hình ảnh Flashcard do người dùng tải lên. |
| **Amazon Cognito** | Xác thực người dùng và cấp JWT Token cho ứng dụng. |

---

## Bạn sẽ học được gì

Sau khi hoàn thành workshop, bạn sẽ có thể:

- Tạo và cấu hình Amazon VPC.
- Triển khai ứng dụng ASP.NET Core lên Amazon EC2.
- Kết nối ứng dụng với Amazon RDS PostgreSQL.
- Lưu trữ và truy xuất hình ảnh bằng Amazon S3.
- Thiết lập xác thực người dùng bằng Amazon Cognito.
- Hoàn thiện quy trình triển khai một ứng dụng web trên AWS.

---

## Nội dung workshop

{{% children showhidden="false" /%}}
