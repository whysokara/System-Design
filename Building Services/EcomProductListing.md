# 🛒 E-Commerce System Design (AWS Setup Notes)

🎯 Goal: Build a simple product listing site with ~100 products  
Frontend (for users) + Backend + Admin UI + DB + Load Balancer + Read Replica

---

## 🔧 Infra Components + AWS Services

| What?                   | AWS Service                    |
|-------------------------|--------------------------------|
| Master + Read DB        | Amazon RDS (MySQL/Postgres)    |
| Backend Server          | EC2 (or Lambda + API Gateway)  |
| Frontend UI             | S3 + CloudFront (for SPA)      |
| Admin UI                | EC2 or S3 (if static)          |
| Load Balancer           | Application Load Balancer      |
| Domain + HTTPS          | Route 53 + ACM                 |
| Networking              | Amazon VPC                     |

---

## 🧠 DB Schema – `products` table

CREATE TABLE products (
  product_id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  description TEXT,
  price DECIMAL(10,2) NOT NULL,
  image_url VARCHAR(512),
  category VARCHAR(100),
  stock_quantity INT DEFAULT 0,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

---

## 🪜 Step-by-Step AWS Flow

Step 1️⃣ – Setup RDS (DB)
- Launch Amazon RDS (MySQL/Postgres)
- Enable Multi-AZ
- Create Read Replica
- Master → for writes  
- Replica → for reads (e.g., listing products)

---

Step 2️⃣ – Backend Server

Option 1: EC2
- Launch EC2 instance
- SSH + Deploy backend
- Connect to RDS
- API:
  - GET /products → read replica
  - POST, PUT, DELETE → master DB

Option 2: Lambda + API Gateway
- Serverless backend
- Ideal for lightweight APIs

---

Step 3️⃣ – Admin UI (for Shop Owner)
- Build React/Vue admin panel
- Deploy via:
  - EC2 (server-rendered)
  - S3 + CloudFront (static)
- Protect with login page / Cognito

---

Step 4️⃣ – Frontend UI (Users)
- Build static React site
- Deploy to S3 (enable static site)
- Use CloudFront as CDN
- Connect to backend/API Gateway for data

---

Step 5️⃣ – Load Balancer
- Use Application Load Balancer (ALB)
- Target group → EC2s
- Listeners:
  - HTTP (80)
  - HTTPS (443 with ACM cert)

---

Step 6️⃣ – VPC + Security
- Use Amazon VPC
- EC2 → Public subnet
- RDS → Private subnet
- Create Security Groups:
  - EC2 → access to DB
  - Public → access to backend (via ALB)

---

Step 7️⃣ – Route 53 + Domain
- Buy or use domain
- Create DNS records:
  - shop.example.com → CloudFront
  - admin.example.com → Admin EC2/S3
  - api.example.com → ALB/API Gateway

---

## ✅ Bonus Tips

- Use CloudWatch Logs for monitoring
- Add Auto Scaling for EC2
- Use IAM roles for permission control
- Protect backend with API Gateway rate limiting or WAF

---

## 📊 Architecture Sketch (Text)

    Internet
       ↓
    Route 53
     / | \
   UI API Admin
   ↓   ↓     ↓
  S3  EC2   EC2
       ↓
  Load Balancer
       ↓
    Backend EC2
       ↓      ↓
   RDS Master  → Read Replica

---

