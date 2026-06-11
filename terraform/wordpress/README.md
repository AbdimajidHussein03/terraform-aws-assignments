Deploy WordPress Using Terraform
Objective

The objective of this project was to use Terraform to deploy a WordPress website on AWS.

This project shows how Terraform can create and manage real cloud infrastructure using code instead of manually setting everything up in the AWS Console.

What I Built

I deployed a WordPress website on an AWS EC2 instance using Terraform.

Terraform was used to create the AWS infrastructure, including the EC2 instance and security group. The EC2 instance then used a user data script to automatically install and configure the software needed for WordPress.

The setup includes:

An EC2 instance to host the WordPress website
A security group to allow web access
A user data script to install Apache, MariaDB, PHP, and WordPress
A public URL to access the WordPress site in a browser
Infrastructure created and managed through Terraform
How It Works

Terraform connects to AWS using the AWS provider.

It then creates a security group that allows HTTP traffic so the WordPress website can be accessed from the internet.

Terraform also creates an EC2 instance. When the EC2 instance starts, the user data script runs automatically. This script installs the required software, downloads WordPress, creates the database, and configures WordPress.

After the deployment is complete, Terraform outputs the public IP address and website URL so the WordPress site can be opened in a browser.

Project Files
main.tf – creates the AWS resources
variables.tf – stores reusable input values
outputs.tf – shows the public IP and WordPress URL
user_data.sh – installs and configures WordPress
.gitignore – prevents Terraform-generated files from being pushed
How to Run
terraform init
terraform fmt
terraform validate
terraform plan
terraform apply

When prompted, type:

yes

After Terraform finishes, open the WordPress URL shown in the output.

Screenshots