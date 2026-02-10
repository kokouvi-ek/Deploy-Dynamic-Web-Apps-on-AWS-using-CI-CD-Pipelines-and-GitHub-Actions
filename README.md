
# Deploy Dynamic Web Apps on AWS using CI/CD Pipelines and GitHub Actions

This project demonstrates how to deploy a scalable, containerized web application on AWS using **Terraform**, **GitHub Actions**, **Docker**, and a CI/CD pipeline. It automates the full deployment lifecycle, from infrastructure provisioning to container builds and database migrations.

---

##  Project Overview

This guide walks you through:
- Infrastructure provisioning with **Terraform**
- CI/CD automation using **GitHub Actions**
- Building and pushing Docker images to **Amazon ECR**
- Deploying apps on **Amazon ECS Fargate**
- Managing secrets with **AWS Secrets Manager**
- Automating database migrations using **Flyway**
- Registering domains and configuring DNS via **Route 53**

---

##  Prerequisites

- Git and GitHub account
- AWS account
- [Terraform](https://developer.hashicorp.com/terraform/downloads)
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- Visual Studio Code with Terraform extensions
- Docker installed locally
- SSH key pair

---

##  Project Setup

### 1. Authentication and Repository Configuration
- Generate SSH key pairs for secure GitHub access
- Add the **public key** to my GitHub profile
- Create a GitHub repository and clone it
- Set up a **GitHub Personal Access Token** and add it as a repository secret

### 2. Terraform and AWS Initialization
- Install the necessary Terraform extensions in VS Code
- Create an **IAM user** in AWS and generate access keys
- Create:
  - An **S3 bucket** for Terraform state
  - A **DynamoDB table** for state locking
- Add Terraform code to your repository ( I use the same terraform code I create in the project "Host-a-Dynamic-Web-App-on-AWS-with-Terraform-Docker-Amazon-ECR-and-ECS")
- Create a `terraform.tfvars` file with values
- Register a domain name in **Route 53**
- Update my Terraform backend with S3 and DynamoDB info

### 3. Secrets Management
- Create secrets in **AWS Secrets Manager** for DB credentials
- Add secrets to GitHub Repository as well

---

##  Infrastructure Deployment

### GitHub Actions Workflow
- Create a GitHub Actions workflow file (`.github/workflows/deploy.yml`)
- Define jobs for:
  - Configuring AWS credentials
  - Deploying infrastructure with Terraform
  - Creating ECR repositories

### EC2 Instance (For Self-Hosted Runner)
- Launch Amazon Linux 2 EC2 instance
- Install Docker and Git
- Create an AMI from the instance and terminate it
- Use GitHub Actions to:
  - Start the self-hosted runner
  - Stop the runner when complete

---

##  Docker and ECR Deployment

### Application Code
- Create a separate repository for my application
- Add a `Dockerfile` and any supporting code 

### GitHub Actions Jobs
- Build Docker image and push to **Amazon ECR**
- Export environment variables to an S3 bucket
- Use **Flyway** to migrate SQL data into the **RDS database**
- Restart ECS services and update ECS task definitions

---

##  Project Structure

```

.
├── terraform/                  # Infrastructure as Code
├── .github/workflows/         # GitHub Actions workflow files
├── sql/                       # SQL migration scripts
├── app/                       # Application codebase
│   └── Dockerfile             # Docker build file
└── README.md

```

---

##  Key Features

- End-to-end CI/CD with GitHub Actions
- Fully automated infrastructure with Terraform
- Secure secrets management with AWS Secrets Manager
- Immutable infrastructure practices via Docker and AMI builds
- Scalable, production-ready deployments using ECS Fargate

---


This project demonstrates the power of **Infrastructure as Code** combined with **CI/CD** and containerization. It's an ideal foundation for production-grade web applications on AWS with zero manual deployment steps.
