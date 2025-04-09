![Alt text](/EKS-rentzone-project.png)

# Kubernetes-Based Dynamic Application on AWS with EKS

This project demonstrates the deployment of a dynamic application using Kubernetes on AWS EKS. The infrastructure was built from scratch using VPC networking components, Amazon RDS, Amazon ECR, IAM, EC2 instances, and other AWS services for a secure and scalable deployment.

## 🚀 Overview

The application architecture includes:
- A custom Virtual Private Cloud (VPC)
- Subnetting across multiple availability zones
- Private and public networking configurations
- Amazon EKS for container orchestration
- Amazon RDS for relational data
- Amazon ECR for container image storage
- Secrets Manager for secure configuration management
- Route 53 and Network Load Balancer for DNS and traffic routing

---

## 🏗️ Infrastructure Setup

### 1. VPC Configuration
- Created a custom VPC with DNS Hostnames enabled.
- Set up an Internet Gateway and attached it to the VPC.

### 2. Subnetting
- Created **6 subnets**:
  - **2 Public Subnets** (with auto-assign public IP enabled)
  - **4 Private Subnets** (split across two Availability Zones)

### 3. Routing
- Created a Route Table for public subnets and associated them.
- Created a NAT Gateway in a public subnet.
- Created two Route Tables for private subnets (one per AZ) and associated 2 private subnets in each AZ accordingly.

### 4. Security & Access
- Created appropriate **Security Groups** for EC2, RDS, EKS, and Load Balancers.
- Set up an **EC2 Instance Connect Endpoint** for secure access to instances in private subnets.

---

## 💾 Data Layer

### 5. RDS Setup
- Created an **Amazon RDS** instance in private subnets for persistent data storage.

### 6. Data Migration
- Created an **Amazon S3** bucket and uploaded the SQL migration script.
- Created an **IAM Role** with S3 read permissions.
- Launched a **bastion EC2 instance** in a private subnet to run the migration script into the RDS instance.

---

## 🐳 Application & Containerization

### 7. Docker & GitHub
- Created a `Dockerfile` for the application.
- Created a **GitHub repository** to store the source code and a GitHub Docker repository for CI/CD testing.
- Cloned the repo locally for image building and testing.

### 8. Amazon ECR
- Created an **Amazon ECR** repository.
- Pushed the built Docker image to the ECR repository.

---

## 🔐 Secrets & Configurations

### 9. AWS Secrets Manager
- Stored application secrets in **Secrets Manager**.
- Created an **IAM policy and role** with access permissions to retrieve secrets securely in the app.

---

## ☸️ Kubernetes on AWS

### 10. EKS Cluster Setup
- Created an **EKS Cluster** using the previously created VPC and subnets.
- Created **Worker Nodes** and connected them to the cluster.

### 11. Load Balancing & DNS
- Set up a **Network Load Balancer** for handling incoming traffic to the EKS service.
- Created a **Route 53 Record Set** for DNS resolution to the NLB.

---

## ✅ Final Result

The dynamic application is now:
- Running on a secure and scalable Kubernetes cluster
- Backed by a managed relational database (RDS)
- Leveraging ECR, S3, and Secrets Manager for secure and efficient CI/CD
- Exposed via Route 53 DNS using a Network Load Balancer

---

## 📁 Repository Structure

```bash
├── Dockerfile
├── k8s-manifests/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── ingress.yaml
├── sql-scripts/
│   └── init-db.sql
├── scripts/
│   └── migrate-data.sh
└── README.md

