---
title: "Migrate & Seed Data"
date: "2026-07-09"
weight: 2
chapter: false
pre: "<b>5.4.2. </b>"
---

Sau khi Amazon RDS đã sẵn sàng, bước tiếp theo là cấu hình ứng dụng để sử dụng PostgreSQL thay cho SQLite, sau đó chạy Entity Framework Core Migrations để tạo schema và nạp dữ liệu mẫu.

---

# 1. Cập nhật Connection String

Mở file **appsettings.json** của dự án FlashLearn và cập nhật chuỗi kết nối:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=flashlearn-db.xxxx.ap-southeast-1.rds.amazonaws.com;Port=5432;Database=flashlearn;Username=flashlearn_admin;Password=<YOUR_PASSWORD>"
  }
}
```

> **Lưu ý:** Thay `flashlearn-db.xxxx.ap-southeast-1.rds.amazonaws.com` bằng **RDS Endpoint** đã lưu ở bước **5.4.1** và nhập đúng mật khẩu của bạn.

---

# 2. Cài đặt PostgreSQL Provider

Đảm bảo project đã cài đặt package **Npgsql.EntityFrameworkCore.PostgreSQL**:

```bash
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

Sau đó cập nhật file **Program.cs** để sử dụng PostgreSQL thay cho SQLite:

```csharp
// SQLite
// builder.Services.AddDbContext<ApplicationDbContext>(options =>
//     options.UseSqlite(connectionString));

// PostgreSQL
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseNpgsql(
        builder.Configuration.GetConnectionString("DefaultConnection")));
```

---

# 3. Tạo Migration (nếu cần)

Nếu project chưa có Migration dành cho PostgreSQL, tạo mới bằng lệnh:

```bash
dotnet ef migrations add InitialPostgreSQL
```

---

# 4. Chạy Migration lên Amazon RDS

Do Amazon RDS nằm trong **Private Subnet**, bạn cần SSH vào EC2 trước khi thực hiện migration.

### Bước 1: SSH vào EC2

```bash
ssh -i flashlearn-key.pem ubuntu@<EC2-Public-IP>
```

### Bước 2: Clone project và chạy Migration

```bash
# Clone source code
git clone <repo-url>
cd WebHocTiengAnhFlashLearn

# Cài đặt .NET SDK
sudo snap install dotnet-sdk --classic --channel=8.0

# Thiết lập Connection String
export ConnectionStrings__DefaultConnection="Host=<RDS-Endpoint>;Port=5432;Database=flashlearn;Username=flashlearn_admin;Password=<YOUR_PASSWORD>"

# Chạy Migration
dotnet ef database update
```

### Bước 3: Kiểm tra kết quả

Kết nối tới PostgreSQL:

```bash
psql -h <RDS-Endpoint> -U flashlearn_admin -d flashlearn
```

Liệt kê các bảng đã được tạo:

```sql
\dt
```

Kết quả mong đợi:

```text
 Schema |      Name       | Type  |      Owner
--------+-----------------+-------+-----------------
 public | AspNetRoles     | table | flashlearn_admin
 public | AspNetUsers     | table | flashlearn_admin
 public | Cards           | table | flashlearn_admin
 public | Decks           | table | flashlearn_admin
 public | UserProgress    | table | flashlearn_admin
```

---

# 5. Seed dữ liệu mẫu (Tùy chọn)

Nếu ứng dụng hỗ trợ Database Initializer, chạy:

```bash
dotnet run --seed
```

Hoặc chèn dữ liệu trực tiếp bằng PostgreSQL:

```sql
INSERT INTO "Decks"
("Id", "Name", "Description", "CreatedAt", "UserId")
VALUES
(gen_random_uuid(), '500 từ vựng tiếng Anh cơ bản',
 'Từ vựng cơ bản A1', NOW(), NULL),

(gen_random_uuid(), '100 động từ bất quy tắc',
 'Danh sách động từ bất quy tắc thông dụng', NOW(), NULL);
```

---

# Kết quả

Sau khi hoàn thành bước này, bạn đã:

- Cập nhật ứng dụng để sử dụng Amazon RDS PostgreSQL.
- Tạo schema cơ sở dữ liệu bằng Entity Framework Core Migrations.
- Xác nhận các bảng đã được tạo thành công trên Amazon RDS.
- Seed dữ liệu mẫu vào cơ sở dữ liệu (nếu có).
