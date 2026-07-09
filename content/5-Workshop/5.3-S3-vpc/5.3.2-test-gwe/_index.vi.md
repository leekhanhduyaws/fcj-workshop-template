---
title: "Cấu hình Internet Gateway & Route Tables"
date: "2026-07-09"
weight: 2
chapter: false
pre: "<b>5.3.2. </b>"
---

Sau khi tạo VPC và các Subnet, bước tiếp theo là cấu hình **Internet Gateway**, **Route Table** và **Security Group** để các tài nguyên có thể giao tiếp đúng cách và đảm bảo an toàn.

---

# 1. Tạo Internet Gateway

Internet Gateway (IGW) cho phép các tài nguyên trong Public Subnet kết nối ra Internet.

1. Trong **VPC Console** → **Internet gateways** → **Create internet gateway**

2. Nhập thông tin:

| Trường | Giá trị |
|--------|----------|
| Name tag | `flashlearn-igw` |

3. Nhấn **Create internet gateway**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.2/5.3.2.1.png" width="900">
</p>

4. Sau khi tạo xong:

- Chọn **flashlearn-igw**
- **Actions → Attach to VPC**
- Chọn **flashlearn-vpc**
- Nhấn **Attach internet gateway**

---

# 2. Tạo Route Table cho Public Subnet

Route Table xác định đường đi của lưu lượng mạng.

1. Chọn **Route tables** → **Create route table**

2. Cấu hình:

| Trường | Giá trị |
|--------|----------|
| Name | `flashlearn-public-rt` |
| VPC | `flashlearn-vpc` |

3. Nhấn **Create route table**

4. Thêm Route ra Internet:

- Chọn **flashlearn-public-rt**
- Tab **Routes**
- **Edit routes**
- **Add route**

| Destination | Target |
|-------------|--------|
| `0.0.0.0/0` | `flashlearn-igw` |

5. Nhấn **Save changes**

6. Gán Route Table cho Public Subnet:

- Tab **Subnet associations**
- **Edit subnet associations**
- Chọn **flashlearn-public-subnet**
- **Save associations**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.2/5.3.2.2.png" width="900">
</p>

---

# 3. Tạo Security Group

## Security Group cho EC2

1. Chọn **Security Groups** → **Create security group**

2. Cấu hình:

| Trường | Giá trị |
|--------|----------|
| Security group name | `flashlearn-ec2-sg` |
| Description | Security group for FlashLearn EC2 |
| VPC | `flashlearn-vpc` |

3. Thêm các Inbound Rules:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| HTTP | TCP | 80 | 0.0.0.0/0 |
| HTTPS | TCP | 443 | 0.0.0.0/0 |
| Custom TCP | TCP | 5000 | 0.0.0.0/0 |
| SSH | TCP | 22 | My IP |

4. Nhấn **Create security group**

---

## Security Group cho Amazon RDS

1. Chọn **Create security group**

2. Cấu hình:

| Trường | Giá trị |
|--------|----------|
| Security group name | `flashlearn-rds-sg` |
| Description | Security group for FlashLearn RDS |
| VPC | `flashlearn-vpc` |

3. Thêm Inbound Rule:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| PostgreSQL | TCP | 5432 | `flashlearn-ec2-sg` |

> **Lưu ý:** Source của rule PostgreSQL nên là **Security Group của EC2**, không phải địa chỉ IP. Điều này giúp chỉ EC2 trong VPC mới có thể truy cập cơ sở dữ liệu.

4. Nhấn **Create security group**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.2/5.3.2.3.png" width="900">
</p>

---

# Kết quả

Sau bước này, bạn đã có:

- Internet Gateway `flashlearn-igw` được gắn vào VPC.
- Route Table `flashlearn-public-rt` cho phép Public Subnet truy cập Internet.
- Security Group `flashlearn-ec2-sg` cho phép HTTP, HTTPS, SSH và cổng ứng dụng.
- Security Group `flashlearn-rds-sg` chỉ cho phép EC2 truy cập PostgreSQL.
