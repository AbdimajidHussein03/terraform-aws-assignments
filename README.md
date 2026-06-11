# Terraform WordPress Deployment

## Objective

This project uses Terraform to deploy a WordPress website on AWS.

The aim was to create AWS infrastructure using code instead of manually setting everything up in the AWS Console.

## What I Built

I deployed a WordPress website on an AWS EC2 instance using Terraform.

Terraform creates the infrastructure, including the EC2 instance and security group. When the EC2 instance starts, a user data script runs automatically to install and configure Apache, MariaDB, PHP, and WordPress.

## Setup Includes

- EC2 instance running WordPress
- Security group allowing HTTP access
- User data script to install WordPress dependencies
- Public URL to access the WordPress site
- Infrastructure created and managed using Terraform

## Project Structure

```text
terraform/
└── wordpress/
    ├── screenshots/
    │   └── wordpress.png
    ├── .gitignore
    ├── .terraform.lock.hcl
    ├── main.tf
    ├── outputs.tf
    ├── user_data.sh
    └── variables.tf

## Files Used

- `main.tf` – contains the AWS provider, security group rules, and EC2 instance resource
- `variables.tf` – stores reusable values such as the AWS region, AMI ID, instance type, and project name
- `outputs.tf` – outputs the public IP address and WordPress URL after deployment
- `user_data.sh` – installs and configures Apache, MariaDB, PHP, and WordPress on the EC2 instance
- `.gitignore` – prevents Terraform state files and local generated files from being pushed to GitHub
- `.terraform.lock.hcl` – records the provider version used by Terraform
- `screenshots/wordpress.png` – shows the working WordPress deployment

## Terraform Commands Used

The following Terraform commands were used during the deployment:

```bash
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply
terraform output
