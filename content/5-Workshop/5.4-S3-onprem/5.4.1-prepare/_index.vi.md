---
title: "Tạo RDS PostgreSQL"
date: "2026-07-09"
weight: 1
chapter: false
pre: "<b>5.4.1. </b>"
---

Trong bước này, bạn sẽ tạo **Amazon RDS for PostgreSQL** để lưu trữ dữ liệu cho ứng dụng FlashLearn. Trước tiên cần tạo **DB Subnet Group**, sau đó khởi tạo **RDS Instance** và lưu lại thông tin kết nối.

---

# 1. Tạo DB Subnet Group

DB Subnet Group giúp xác định các **Private Subnet** mà Amazon RDS sẽ sử dụng.

1. Truy cập **Amazon RDS Console** → **Subnet groups** → **Create DB subnet group**

2. Cấu hình:

| Trường | Giá trị |
|--------|----------|
| Name | `flashlearn-db-subnet-group` |
| Description | Subnet group for FlashLearn RDS |
| VPC | `flashlearn-vpc` |

3. Trong phần **Add subnets**, thêm cả hai Private Subnet:

- **ap-southeast-1a** → `flashlearn-private-subnet-1 (10.0.2.0/24)`
- **ap-southeast-1b** → `flashlearn-private-subnet-2 (10.0.3.0/24)`

4. Nhấn **Create**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.4/5.4.1/5.4.1.1.png" width="900">
</p>

---

# 2. Tạo Amazon RDS PostgreSQL

1. Chọn **Databases** → **Create database**

2. Trong phần **Engine options**:

- Engine type: **PostgreSQL**
- Engine version: **PostgreSQL 16.x**

3. Trong **Templates**, chọn:

- **Free tier** (nếu tài khoản còn Free Tier)
- Hoặc **Dev/Test**

4. Thiết lập thông tin cơ sở dữ liệu:

| Trường | Giá trị |
|--------|----------|
| DB instance identifier | `flashlearn-db` |
| Master username | `flashlearn_admin` |
| Master password | Đặt mật khẩu mạnh |
| Confirm password | Nhập lại mật khẩu |

5. Cấu hình Instance:

| Trường | Giá trị |
|--------|----------|
| DB instance class | `db.t3.micro` |
| Storage type | `gp2` |
| Allocated storage | `20 GB` |
| Storage autoscaling | Tắt |

6. Cấu hình kết nối:

| Trường | Giá trị |
|--------|----------|
| VPC | `flashlearn-vpc` |
| DB subnet group | `flashlearn-db-subnet-group` |
| Public access | **No** |
| VPC security group | `flashlearn-rds-sg` |
| Availability Zone | `ap-southeast-1a` |

> **Lưu ý:** Bắt buộc chọn **Public access = No** để cơ sở dữ liệu không thể truy cập trực tiếp từ Internet.

7. Cấu hình bổ sung:

| Trường | Giá trị |
|--------|----------|
| Initial database name | `flashlearn` |
| Backup retention period | `7 days` |
| Encryption | Enable |

8. Nhấn **Create database** và chờ khoảng **5–10 phút** để RDS được khởi tạo.

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.4/5.4.1/5.4.1.2.png" width="900">
</p>

---

# 3. Lưu lại thông tin kết nối

Sau khi trạng thái của RDS chuyển sang **Available**, lưu lại Endpoint để sử dụng trong các bước triển khai ứng dụng.

1. Chọn database **flashlearn-db**
2. Mở tab **Connectivity & security**
3. Sao chép các thông tin sau:

- Endpoint
- Port: `5432`
- Master username

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.4/5.4.1/5.4.1.3.png" width="900">
</p>

---

# Kết quả

Sau khi hoàn thành bước này, bạn đã có:

- DB Subnet Group được tạo trên hai Private Subnet.
- Amazon RDS PostgreSQL ở trạng thái **Available**.
- Amazon RDS chỉ cho phép kết nối từ EC2 thông qua Security Group.
- Đã lưu lại thông tin kết nối gồm **Endpoint**, **Username** và **Password** để sử dụng ở các bước tiếp theo.
