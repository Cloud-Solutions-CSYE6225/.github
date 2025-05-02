# Infrastructure and Web Application Overview

## Overview

This organization consists of three core repositories, each contributing to the deployment and functionality of a cloud-based web application:

### 1. TF AWS Infra
- Manages cloud infrastructure using **Terraform** for provisioning **AWS** services and resources.

### 2. WebApp
- Hosts the **Spring Boot**-based web application, designed to run on the AWS infrastructure provisioned by Terraform.

### 3. Serverless
- Implements **serverless**, event-driven components for email verification, using **AWS Lambda** functions and the **SendGrid API**.

![image](https://github.com/user-attachments/assets/2fcc2379-da57-430d-8099-c1388b80958c)

# Repositories

## 1. TF AWS Infra

The **TF AWS Infra** repository is dedicated to managing the cloud infrastructure required to run the CSYE 6225 web application. Using Infrastructure as Code (IaC) with Terraform, this repository automates the deployment of all necessary AWS resources, including:

### Key Components:
- **Network Configuration**: Creates a Virtual Private Cloud (VPC) with public and private subnets.
- **Security**: Defines security groups for both web applications and databases, ensuring controlled access to services.
- **Compute Resources**: Deploys EC2 instances with custom AMIs tailored to run the web application.
- **Database**: Sets up a MySQL database hosted on Amazon RDS with secure network configurations.
- **Load Balancing and Routing**: Configures route tables, internet gateways, and load balancers for traffic management.
- **Auto Scaling Groups**: EC2 resources are later replaced with templates used to deploy EC2 instances using ASG, where up-scaling and down-scaling depend on CPU utilization metrics.
- **CloudWatch Monitoring**: Implements CloudWatch monitoring to fetch application logs and custom metrics for API counters and timers using StatsD.
- **Storage System**:
  - AWS RDS connects to the private subnet to fetch data for the application.
  - S3 is used to store user profile pictures.

The goal of this repository is to provide a scalable and secure foundation for running cloud-based web applications, enabling automated and repeatable infrastructure deployments.

---

## 2. WebApp  
👉 [View Repository](https://github.com/Cloud-Solutions-CSYE6225/webapp)

The **WebApp** repository contains the source code for a Spring Boot web application designed to run seamlessly on the AWS infrastructure set up by TF AWS Infra.

### Key Features:
- **Stateless Web Application**: Implements REST APIs for various functionalities using Spring Boot.
- **Database Integration**: Connects to the MySQL database hosted on Amazon RDS, with dynamic configurations handled through environment variables.
- **Packer Integration**: Utilizes Packer templates to build custom Amazon Machine Images (AMIs) that include the web application and its dependencies.
- **Continuous Integration**: Implements GitHub Actions for:
  - Code testing
  - Validation
  - Packer image creation

This repository is responsible for delivering the application logic and services that interact with the cloud infrastructure set up by TF AWS Infra.

---

## 3. Serverless

The **Serverless** repository contains the source code for a Spring-based application designed to run seamlessly on the AWS Lambda set up by TF AWS Infra.

### Key Responsibilities:
- The Lambda function fetches user data passed in via SNS (created by TF AWS Infra).
- Based on that data, it sends a verification email to the user using SendGrid.
- The email contains a link that, when clicked, activates the user account.

This repository is responsible for activating user accounts and validating email IDs using cloud services provided via TF AWS Infra.

---

## Summary

By combining Infrastructure as Code with a cloud-native web application and a serverless component, this project demonstrates best practices in scalable and automated cloud deployments using GitHub Actions for CI/CD.

