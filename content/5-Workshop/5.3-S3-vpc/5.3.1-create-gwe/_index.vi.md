---
title: "Khởi tạo VPC & Subnets"
date: "2026-07-09"
weight: 1
chapter: false
pre: "<b>5.3.1. </b>"
---

Trong bước này, chúng ta sẽ tạo một VPC mới và chia mạng thành các subnet dành riêng cho từng lớp của ứng dụng.

---

# 1. Tạo VPC

1. Đăng nhập **AWS Console** → Tìm kiếm **VPC** → Chọn **VPC**

2. Chọn **Create VPC**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1-vpc-created.png" width="900">
</p>

3. Cấu hình VPC:

| Trường | Giá trị |
|--------|----------|
| **Resources to create** | VPC only |
| **Name tag** | `flashlearn-vpc` |
| **IPv4 CIDR block** | `10.0.0.0/16` |
| **IPv6 CIDR block** | No IPv6 CIDR block |
| **Tenancy** | Default |

4. Nhấn **Create VPC**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1.1.png" width="900">
</p>

---

# 2. Tạo Public Subnet

Public Subnet sẽ chứa EC2 instance chạy ứng dụng FlashLearn.

1. Trong **VPC Console** → **Subnets** → **Create subnet**

2. Cấu hình:

| Trường | Giá trị |
|--------|----------|
| **VPC ID** | Chọn `flashlearn-vpc` |
| **Subnet name** | `flashlearn-public-subnet` |
| **Availability Zone** | `ap-southeast-1a` |
| **IPv4 CIDR block** | `10.0.1.0/24` |

3. Nhấn **Create subnet**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1.2.png" width="900">
</p>

4. Sau khi tạo xong, bật **Auto-assign public IP**:

- Chọn subnet `flashlearn-public-subnet`
- Chọn **Actions** → **Edit subnet settings**
- Tích chọn **Enable auto-assign public IPv4 address**
- Nhấn **Save**

---

# 3. Tạo Private Subnets

Private Subnet sẽ chứa cơ sở dữ liệu Amazon RDS và không có kết nối Internet trực tiếp.

1. Trong **Subnets** → **Create subnet**

2. Tạo subnet thứ nhất:

| Trường | Giá trị |
|--------|----------|
| **VPC ID** | Chọn `flashlearn-vpc` |
| **Subnet name** | `flashlearn-private-subnet-1` |
| **Availability Zone** | `ap-southeast-1a` |
| **IPv4 CIDR block** | `10.0.2.0/24` |

3. Nhấn **Add new subnet** để tạo subnet thứ hai (Amazon RDS yêu cầu tối thiểu hai Availability Zones):

| Trường | Giá trị |
|--------|----------|
| **Subnet name** | `flashlearn-private-subnet-2` |
| **Availability Zone** | `ap-southeast-1b` |
| **IPv4 CIDR block** | `10.0.3.0/24` |

4. Nhấn **Create subnet**

<p align="center">
  <img src="/fcj-workshop-template/images/5-Workshop/5.3-S3-vpc/5.3.1/5.3.1.3.png" width="900">
</p>

---

## Kết quả

Sau bước này, bạn đã tạo thành công:

- VPC `flashlearn-vpc` với CIDR `10.0.0.0/16`
- Public Subnet `10.0.1.0/24` tại `ap-southeast-1a`
- Private Subnet `10.0.2.0/24` tại `ap-southeast-1a`
- Private Subnet `10.0.3.0/24` tại `ap-southeast-1b`

Các subnet này sẽ được sử dụng ở các bước tiếp theo để triển khai Internet Gateway, Route Tables, EC2 và Amazon RDS.
