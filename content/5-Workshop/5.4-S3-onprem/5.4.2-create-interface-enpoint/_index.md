---
title: "Migrate & Seed Data"
date: "2026-07-09"
weight: 2
chapter: false
pre: "<b>5.4.2. </b>"
---

After your Amazon RDS instance is ready, the next step is to configure the application to use PostgreSQL instead of SQLite. You will then run Entity Framework Core Migrations to create the database schema and optionally seed sample data.

---

# 1. Update the Connection String

Open the **appsettings.json** file in the FlashLearn project and update the connection string:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=flashlearn-db.xxxx.ap-southeast-1.rds.amazonaws.com;Port=5432;Database=flashlearn;Username=flashlearn_admin;Password=<YOUR_PASSWORD>"
  }
}
```

> **Note:** Replace `flashlearn-db.xxxx.ap-southeast-1.rds.amazonaws.com` with the **RDS Endpoint** you saved in **Step 5.4.1**, and enter your own password.

---

# 2. Install the PostgreSQL Provider

Make sure the project includes the **Npgsql.EntityFrameworkCore.PostgreSQL** package:

```bash
dotnet add package Npgsql.EntityFrameworkCore.PostgreSQL
```

Next, update **Program.cs** to use PostgreSQL instead of SQLite:

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

# 3. Create a Migration (If Needed)

If your project does not already have a migration for PostgreSQL, create one by running:

```bash
dotnet ef migrations add InitialPostgreSQL
```

---

# 4. Run the Migration on Amazon RDS

Because Amazon RDS is deployed in a **Private Subnet**, you must connect to your EC2 instance before running the migration.

### Step 1: Connect to EC2 via SSH

```bash
ssh -i flashlearn-key.pem ubuntu@<EC2-Public-IP>
```

### Step 2: Clone the Project and Run the Migration

```bash
# Clone the source code
git clone <repo-url>
cd WebHocTiengAnhFlashLearn

# Install the .NET SDK
sudo snap install dotnet-sdk --classic --channel=8.0

# Configure the connection string
export ConnectionStrings__DefaultConnection="Host=<RDS-Endpoint>;Port=5432;Database=flashlearn;Username=flashlearn_admin;Password=<YOUR_PASSWORD>"

# Run the migration
dotnet ef database update
```

### Step 3: Verify the Migration

Connect to PostgreSQL:

```bash
psql -h <RDS-Endpoint> -U flashlearn_admin -d flashlearn
```

List all tables:

```sql
\dt
```

Expected output:

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

# 5. Seed Sample Data (Optional)

If your application supports a database initializer, run:

```bash
dotnet run --seed
```

Or insert sample data directly into PostgreSQL:

```sql
INSERT INTO "Decks"
("Id", "Name", "Description", "CreatedAt", "UserId")
VALUES
(gen_random_uuid(), '500 Basic English Vocabulary',
 'Basic A1 vocabulary', NOW(), NULL),

(gen_random_uuid(), '100 Irregular Verbs',
 'A collection of common irregular verbs', NOW(), NULL);
```

---

# Result

After completing this step, you have:

- Configured the application to use Amazon RDS PostgreSQL.
- Created the database schema using Entity Framework Core Migrations.
- Verified that the required tables were successfully created in Amazon RDS.
- Seeded sample data into the database (optional).
