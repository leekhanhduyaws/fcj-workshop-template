---
title: "Triển khai Cơ sở dữ liệu (Amazon RDS)"
date: "2026-07-09"
weight: 4
chapter: false
pre: "<b>5.4. </b>"
---

**Amazon Relational Database Service (Amazon RDS)** là dịch vụ cơ sở dữ liệu quan hệ được AWS quản lý hoàn toàn, giúp tự động hóa các tác vụ như sao lưu, cập nhật bản vá, giám sát và nâng cao tính sẵn sàng của hệ thống.

## Tại sao chuyển từ SQLite sang Amazon RDS?

Trong giai đoạn phát triển, ứng dụng **FlashLearn** sử dụng **SQLite** để lưu trữ dữ liệu cục bộ. Tuy nhiên, khi triển khai trên môi trường thực tế, việc sử dụng một dịch vụ cơ sở dữ liệu chuyên biệt như **Amazon RDS for PostgreSQL** sẽ mang lại khả năng mở rộng, độ tin cậy và tính bảo mật cao hơn.

Bảng dưới đây so sánh giữa SQLite và Amazon RDS:

| Tiêu chí | SQLite (Cục bộ) | Amazon RDS (PostgreSQL) |
| -------- | ---------------- | ----------------------- |
| **Vị trí lưu trữ** | Tệp dữ liệu trên máy chủ | Dịch vụ cơ sở dữ liệu được quản lý |
| **Sao lưu** | Thực hiện thủ công | Tự động (7 ngày) |
| **Khả năng mở rộng** | Hạn chế | Dễ dàng nâng cấp tài nguyên |
| **Tính sẵn sàng** | Single Point of Failure | Hỗ trợ Multi-AZ (tùy chọn) |
| **Quản lý** | Tự quản lý | AWS quản lý hoàn toàn |

Ngoài ra, Amazon RDS được triển khai trong **Private Subnet** của VPC, giúp cơ sở dữ liệu không tiếp xúc trực tiếp với Internet. Chỉ các EC2 instance được cấp quyền thông qua **Security Group** mới có thể kết nối đến cơ sở dữ liệu, đảm bảo tính bảo mật theo khuyến nghị của AWS.

## Nội dung

{{% children showhidden="false" /%}}
