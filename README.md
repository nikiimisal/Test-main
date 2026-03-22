# 🚀 Project 3: Data Ingestion from S3 to RDS with Glue Fallback

## 📌 Objective

Develop a Dockerized Python application that automates the process of:

- Reading data from an Amazon S3 bucket  
- Pushing it to an RDS (MySQL-compatible) database  
- Automatically falling back to AWS Glue if the RDS database is unavailable or the push operation fails  

This project helps integrate multiple AWS services (S3, RDS, Glue), work with data pipelines, and use Docker for packaging and deployment.

---

## 🏗️ Architecture

```
Normal Flow:
S3 → Python → RDS ✅

Failure Flow:
S3 → Python → ❌ RDS → ✅ Glue
```

👉 This is a real-world fault-tolerant pipeline 🔥

---

## 📁 Step 1: Prepare Project Files

Create a folder and inside it create:

```
project-folder/
│── data.csv    # Sample dataset
│── app.py      # Python script (S3 → RDS → Glue fallback)
│── Dockerfile
│── requirements.txt
│── .env
```

You can:
- Create files directly in terminal  
- OR clone a repo and edit  
- OR create locally and upload to EC2  

>I have created this files in directly in terminal

---

## 🔐 Step 2: IAM User (Permission System)

Go to → ***AWS** → **IAM** → **Users** → **Create User**

Configuration Fill:
- Name: `project-user`
- Enable: ✅ Programmatic access  

Attach Permissions:
- `AmazonS3FullAccess`  
- `AmazonRDSFullAccess`  
- `AWSGlueConsoleFullAccess`

Go to Security Credentials → Access Keys → Create  

Save:

```
AWS_ACCESS_KEY_ID=XXXX
AWS_SECRET_ACCESS_KEY=XXXX
```

👉 These will be used inside Docker

---

## ☁️ Step 3: Set up Amazon S3

1. Open AWS Console → S3  
2. Create bucket (e.g., `my-data-bucket-277`)  
3. Upload `data.csv`  
4. Note the bucket name and object key (`data.csv`) for environment variables.
  
---

## 🗄️ Step 4: Set up Amazon RDS (MySQL)

Go to AWS Console → RDS → Create database

Select:
- Engine: MySQL  
- Version: 8.0  
- Free tier  

Configure:
- DB Identifier: `my-rds`  
- Database Name: `mydb`  
- Username: `admin`  
- Password: `password123`  
- Public access: Enabled  

Note the endpoint:
```
my-rds.xxxxx.region.rds.amazonaws.com
```

---

## 🧾 Step 4a: Create Table in RDS

```SQL
CREATE DATABASE mydb;

USE mydb;

CREATE TABLE mytable (
id INT PRIMARY KEY,
name VARCHAR(100),
age INT,
city VARCHAR(100)
);
```
>For this, we’ll need to launch a server instance — we can do that later.

---

## 🧠 Step 5: Set up AWS Glue (Fallback)

Go to AWS Glue → Data Catalog

- Create database: `fallback_db`  
- Do NOT create tables manually  

👉 Python script will create tables automatically if RDS fails.

---

## 💻 Step 6: Launch EC2 Instance

Go to EC2 → Launch Instance

- Amazon Linux 2 / 2023  
- Instance type: `t2.micro `

Enable:
- SSH (port 22)  

Download `.pem` key

Connect:
```Bash
ssh -i "your-key.pem" ec2-user@your-ec2-ip
```

---

## 🐳 Step 7: Install Docker

```Bash
sudo yum update -y
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user
```

Reconnect SSH so the user is added to the Docker group.

---

## 🏗️ Step 8: Build Docker Image

```Bash
docker build -t s3-rds-glue-app .
```
This creates a Docker image with your Python script and dependencies.

---

## ▶️ Step 9: Run Docker Container

```Bash
docker run --env-file .env s3-rds-glue-app
```

---

## ⚙️ Expected Behavior

- Reads CSV from S3  
- Uploads to RDS  

### If RDS works:
- Data inserted successfully  

### If RDS fails:
- Error occurs  
- Glue fallback triggered  
- Table created in Glue  

---

## 🔍 Step 10: Verification

### Check RDS:

```Bash
SELECT * FROM mytable;
```

### Check Glue:

- Go to Glue → Tables → `my_glue_table`  
- Columns match CSV  

### Optional (Athena):

```SQL
SELECT * FROM my_glue_table;
```

---

## 📜 Step 11: Docker Logs

```Bash
docker ps                      # find running container
docker logs <container_id>
```
Logs will show:

- RDS success OR
- Glue fallback triggered

---

## 🧪 Step 12: Test Glue Fallback (Optional)

Edit `.env`:

```
RDS_PASS=wrongpassword
```

Run again:

```Bash
docker run --env-file .env s3-rds-glue-app
```

Output:

```
📤 Uploading data to RDS...
❌ RDS upload failed
⚠️ Falling back to Glue...
✅ Glue table created successfully
```
Verify Glue table:

Go to Glue → Tables → my_glue_table

Columns reflect CSV headers: id, name, age, city

✅ This step confirms the fallback mechanism works.
---

## 🧹 Step 13: Cleanup

```
docker stop <container_id>
```

---




# 📄 Summary Report: Data Ingestion Pipeline (S3 → RDS → Glue Fallback)

## 1. Python script and Dockerfile stored in a GitHub repository

[click here](https://github.com/nikiimisal/Internship__Project__3__-Raw-material)

## 2. Working Docker image and container logs showing: 

o Successful push to RDS or fallback to Glue 

## 3. Screenshot of: 
o Records inserted into RDS or 
o Table created in AWS Glue Catalog 

## 4. 🔄 Data Flow

This project implements a fault-tolerant data ingestion pipeline where data is read from Amazon S3 and inserted into an RDS MySQL database. If the RDS operation fails, the system automatically switches to AWS Glue as a fallback mechanism.

### ✅ Normal Flow:
S3 → Python Application → RDS MySQL

- The Python script reads a CSV file from an S3 bucket
- Data is parsed using pandas
- Data is inserted into RDS using SQLAlchemy and PyMySQL

### ❌ Failure Flow:
S3 → Python Application → RDS (Failure) → AWS Glue

- If RDS connection fails (wrong credentials / DB down / network issue)
- Exception is handled in Python
- AWS Glue is triggered using boto3
- A table is created in Glue Data Catalog with the same schema

👉 This ensures **no data loss and continuous processing**

---

## 5. ☁️ AWS Services Used

### Amazon S3
- Stores raw CSV data
- Acts as the source of the pipeline

### Amazon RDS (MySQL)
- Primary database for structured data storage
- Receives data from the Python application

### AWS Glue
- Used as a fallback mechanism
- Creates tables in Data Catalog when RDS fails

### IAM (Identity and Access Management)
- Manages permissions and access
- Provides secure access keys for programmatic usage

### Amazon EC2
- Hosts the Docker container
- Runs the Python application in a cloud environment

---

## 6. 🐳 Docker Setup

Docker is used to package the application and ensure consistency across environments.

### Key Components:
- Base Image: Python 3.9
- Dependencies installed:
  - boto3
  - pandas
  - sqlalchemy
  - pymysql

### Working:
- Application code is copied into the container
- The container runs the Python script automatically on startup

### Environment Variables:
- Managed using `.env` file
- Includes:
  - AWS credentials
  - S3 bucket details
  - RDS connection configuration

### Commands Used:
```
docker build -t s3-rds-glue-app .
docker run --env-file .env s3-rds-glue-app
```
👉 Docker ensures portability and avoids dependency issues

---

## 7. ⚠️ Challenges Faced & Solutions

### 1. RDS Connection Failure
- Issue: Incorrect password / DB not reachable
- Solution: Implemented try-except block and fallback to AWS Glue

### 2. Dependency Management Issues
- Issue: Python libraries mismatch across environments
- Solution: Used Docker and requirements.txt for consistent setup

### 3. AWS Permission Errors
- Issue: Access denied while accessing S3 or Glue
- Solution: Configured IAM user with required permissions (S3, RDS, Glue)

### 4. Testing Fallback Mechanism
- Issue: Difficult to simulate failure
- Solution: Intentionally changed RDS password in `.env` file to trigger fallback

---

## ✅ Conclusion

This project demonstrates a real-world, fault-tolerant data ingestion pipeline using AWS services and Docker.  
It ensures that data is reliably processed even in failure scenarios by automatically switching to AWS Glue.

---
---
