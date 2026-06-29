# Multi-Tier Bank Application on Kubernetes

A full-stack banking application deployed using modern DevOps practices. This project demonstrates how to build a Spring Boot web app, containerize it with Docker, deploy it on Kubernetes, and provision an AWS EKS environment with Terraform.

## Project Overview

This repository contains a simple multi-tier banking web application with:

- a Spring Boot backend
- a MySQL database
- Docker-based containerization
- Kubernetes manifests for deployment
- Terraform infrastructure as code for AWS EKS
- RBAC setup guidance for CI/CD automation

The goal of this project is to showcase a practical end-to-end DevOps workflow from application development to cloud deployment.

## What the Application Does

Users can:

- register an account
- log in securely
- view their dashboard
- deposit funds
- withdraw funds
- transfer money to another user
- view transaction history

The application is built with Spring Boot, Spring Security, Thymeleaf, and MySQL.

## Architecture

The project follows a multi-tier architecture:

- Frontend: Thymeleaf-based web UI
- Backend: Spring Boot application
- Database: MySQL running inside Kubernetes
- Infrastructure: AWS EKS provisioned with Terraform

High-level flow:

```text
User -> Spring Boot App -> MySQL Database
         |                 |
         |                 +--> Persistent Volume
         |
         +--> Docker Container
         |
         +--> Kubernetes Deployment / Service
```

## Tech Stack

### Application
- Java 17
- Spring Boot 3
- Spring Security
- Thymeleaf
- MySQL
- Maven

### DevOps / Cloud
- Docker
- Kubernetes
- AWS EKS
- Terraform
- RBAC / Kubernetes Service Accounts

## Repository Structure

```text
Multi-Tier-BankApp-CI-main/
├── Dockerfile
├── pom.xml
├── mvnw
├── src/
│   ├── main/java/
│   ├── main/resources/
│   └── test/java/
├── Setup-RBAC.md
└── README.md

Manifest-Code/
└── Manifest.yml

Terraform-Code/
├── main.tf
├── output.tf
├── variables.tf
```

## Prerequisites

Before running or deploying this project, make sure you have:

- Java 17+
- Maven
- Docker
- kubectl
- Terraform
- An AWS account
- Access to an EKS-compatible environment

## Run Locally

### 1. Build the application

```bash
./mvnw clean package
```

### 2. Run the Spring Boot app

```bash
./mvnw spring-boot:run
```

The application will be available at:

```text
http://localhost:8080
```

## Containerize with Docker

Build the Docker image:

```bash
docker build -t your-dockerhub-username/bankapp:latest .
```

Run it locally:

```bash
docker run -p 8080:8080 your-dockerhub-username/bankapp:latest
```

## Kubernetes Deployment

The Kubernetes manifests in the Manifest-Code directory define:

- a MySQL Secret and ConfigMap
- a StorageClass and PersistentVolumeClaim
- MySQL deployment and service
- the bank application deployment and service

Apply the manifests:

```bash
kubectl apply -f Manifest-Code/Manifest.yml
```

## Terraform for AWS EKS

The Terraform files in the Terraform-Code directory provision:

- a VPC
- public subnets
- an internet gateway
- an EKS cluster
- an EKS node group
- IAM roles and policies
- EBS CSI support

Initialize and apply:

```bash
cd Terraform-Code
terraform init
terraform plan
terraform apply
```

## RBAC and CI/CD Notes

The Setup-RBAC.md file contains Kubernetes RBAC configuration for creating a service account, role, role binding, and cluster role binding. This is especially useful when integrating Jenkins or another CI/CD tool with Kubernetes.

## DevOps Flow Demonstrated

This project highlights the following DevOps practices:

1. Version control with Git
2. Application packaging with Maven
3. Containerization with Docker
4. Orchestration with Kubernetes
5. Infrastructure provisioning with Terraform
6. Cloud deployment on AWS EKS
7. RBAC and security configuration for automation

## Blog-Worthy Story Outline

If you plan to write about this project on Hashnode, Dev.to, or Medium, this project gives you a strong narrative:

- Why I built a banking app as a DevOps project
- How I moved from a local Java application to a containerized service
- How Kubernetes helped manage the database and application together
- How Terraform made the AWS infrastructure reproducible
- What I learned about CI/CD, security, and cloud-native deployment

A good article structure could be:

1. Introduction: why this project matters
2. Architecture overview
3. Building the application
4. Dockerizing the app
5. Deploying on Kubernetes
6. Provisioning EKS with Terraform
7. Lessons learned and next steps

## Contributing

Contributions are welcome. If you improve the application, deployment manifests, or Terraform configuration, feel free to open a pull request.

## License

This project is open for learning and experimentation.
