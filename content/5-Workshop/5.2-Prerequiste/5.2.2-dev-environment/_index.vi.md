---
title: "Cài đặt môi trường phát triển"
date: "2026-07-09"
weight: 2
chapter: false
pre: "<b>5.2.2. </b>"
---

Trong bước này, bạn sẽ cài đặt các công cụ cần thiết trên máy tính để làm việc với AWS và chuẩn bị môi trường phát triển cho ứng dụng FlashLearn.

## 1. Cài đặt AWS CLI

**AWS CLI** cho phép bạn tương tác với các dịch vụ AWS thông qua dòng lệnh.

### Windows

Tải và cài đặt từ trang chính thức:

```text
https://awscli.amazonaws.com/AWSCLIV2.msi
```

Sau khi cài đặt hoàn tất, kiểm tra phiên bản:

```bash
aws --version
# aws-cli/2.x.x Python/3.x.x Windows/x86_64
```

### Cấu hình AWS CLI

Chạy lệnh sau và nhập thông tin của IAM User đã tạo ở bước **5.2.1**:

```bash
aws configure
```

```text
AWS Access Key ID [None]: <Access Key của IAM User>
AWS Secret Access Key [None]: <Secret Key của IAM User>
Default region name [None]: ap-southeast-1
Default output format [None]: json
```

> Để lấy **Access Key**: Vào **IAM → Users → `flashlearn-admin` → Security credentials → Create access key**

---

## 2. Cài đặt .NET SDK 8.0

Ứng dụng **FlashLearn** được xây dựng bằng **.NET 8.0**. Bạn cần cài đặt SDK để có thể build và publish dự án.

Tải .NET SDK 8.0 tại:

```text
https://dotnet.microsoft.com/download/dotnet/8.0
```

Kiểm tra sau khi cài đặt:

```bash
dotnet --version
# 8.0.x
```

---

## 3. Cài đặt Git

**Git** được sử dụng để clone source code và quản lý phiên bản dự án.

Tải Git tại:

```text
https://git-scm.com/downloads
```

Kiểm tra sau khi cài đặt:

```bash
git --version
# git version 2.x.x
```

---

## 4. Cài đặt SSH Client

SSH Client được sử dụng để kết nối tới EC2 instance.

- **Windows 10/11**: OpenSSH đã được tích hợp sẵn.
- Kiểm tra bằng cách mở **PowerShell** và chạy:

```bash
ssh
```

---

## 5. Clone source code FlashLearn

Clone repository về máy:

```bash
git clone <đường dẫn repo FlashLearn của bạn>
cd WebhocTiengAnhFlashLearn
```

Kiểm tra project có thể build thành công:

```bash
dotnet restore
dotnet build
```

Kết quả mong đợi:

```text
Build succeeded.
    0 Warning(s)
    0 Error(s)
```

---

## Kết quả

Sau khi hoàn thành bước này, bạn sẽ có:

- AWS CLI đã được cấu hình với IAM User.
- .NET SDK 8.0 đã được cài đặt.
- Git và SSH Client sẵn sàng sử dụng.
- Source code FlashLearn đã được clone về máy và có thể build thành công.
