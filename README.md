# Terraform AWS Assignments

This repository contains two Terraform projects completed as part of my DevOps learning.

The aim of these assignments was to practise using Infrastructure as Code to create AWS resources in a repeatable and automated way, instead of manually configuring everything through the AWS Console.

# Assignment 1 – WordPress Deployment with Terraform

## Objective

The objective of this assignment was to deploy a working WordPress website on AWS using Terraform.

The focus was on using Terraform to create the infrastructure and using EC2 user data to automatically configure the server when it launched.

## What I Built

I created an AWS EC2 instance and configured it to run WordPress.

Terraform was used to define the AWS infrastructure, including the EC2 instance and the security group. The security group allowed web traffic so that the WordPress site could be accessed from a browser.

When the EC2 instance launched, a user data script ran automatically. This script installed Apache, MariaDB, PHP, and WordPress. It also created the WordPress database and configured WordPress so the site was ready to access without manually installing the software through SSH.

## Infrastructure Process

The deployment process started by configuring the AWS provider so Terraform could interact with my AWS account in the selected region.

I then created a security group to control network access to the EC2 instance. HTTP traffic was allowed so the WordPress site could be viewed in a browser, and SSH access was included for troubleshooting if needed.

After that, I created the EC2 instance using an Ubuntu AMI and a small instance type suitable for testing. The instance used the security group created earlier.

To automate the WordPress installation, I passed a user data script into the EC2 instance. This meant the server configured itself during the first boot. The script installed the required packages, started the necessary services, created the database, downloaded WordPress, configured the WordPress settings, and placed the files in Apache’s web directory.

Finally, Terraform outputs were used to display the public IP address and the WordPress URL after deployment.

## Files Used

* `provider.tf` – configures the AWS provider and region
* `main.tf` – creates the EC2 instance and security group rules
* `variables.tf` – stores reusable values such as the AMI ID, AWS region, and instance type
* `outputs.tf` – displays the instance public IP address and WordPress URL
* `user_data.sh` – installs and configures Apache, MariaDB, PHP, and WordPress automatically
* `.gitignore` – prevents Terraform state files and local generated files from being pushed to GitHub
* `.terraform.lock.hcl` – records the provider version used by Terraform
* `screenshots/wordpress.png` – shows the working WordPress deployment

## Screenshot

The screenshot below shows the WordPress site running successfully.

![WordPress Screenshot](terraform/assignment-1-wordpress/screenshots/wordpress.png)


# Assignment 2 – EC2 Deployment with Cloud-Init

## Objective

The objective of this assignment was to deploy an EC2 instance using Terraform and configure it automatically with cloud-init.

The focus was on understanding how Terraform can pass a cloud-init YAML file into an EC2 instance through user data, allowing the server to configure itself when it starts.

## What I Built

I created an AWS EC2 instance that automatically installs and runs Apache when it launches.

Terraform was used to create the infrastructure, including the EC2 instance and security group. A cloud-init YAML file was passed into the instance using the `user_data` argument.

When the instance booted, cloud-init updated the package list, installed Apache, created a custom HTML page, and started the Apache service. This meant the server came online fully configured with no manual setup required after launch.

## Infrastructure Process

The deployment began by configuring the AWS provider and setting reusable values such as the AWS region, AMI ID, and instance type in `variables.tf`.

I then created a security group for the EC2 instance. The security group allowed HTTP traffic on port 80 so the web page could be accessed through a browser. SSH access was also included for troubleshooting.

Next, I created the EC2 instance and attached the security group to it. Instead of manually logging into the server to install software, I used Terraform’s `user_data` argument to pass in a cloud-init YAML file.

The cloud-init file handled the server configuration automatically. It installed Apache using the `packages` section, created an `index.html` file using the `write_files` section, and started Apache using the `runcmd` section.

After Terraform created the infrastructure, the public IP address and website URL were displayed using Terraform outputs. Opening the URL in a browser showed the custom Apache page created by cloud-init.

## Files Used

* `provider.tf` – configures the AWS provider and region
* `main.tf` – creates the EC2 instance, security group, security group rules, and passes cloud-init through user data
* `variables.tf` – stores reusable values such as the AWS region, AMI ID, and instance type
* `outputs.tf` – displays the instance public IP address and website URL
* `cloud-init.yaml` – installs Apache, creates the web page, and starts the Apache service automatically
* `.gitignore` – prevents Terraform state files and local generated files from being pushed to GitHub
* `screenshots/cloud-init-working.png` – shows the working Apache page created by cloud-init

## Cloud-Init Workflow

The cloud-init file was used to automate the server setup during the first boot of the EC2 instance.

It performed the following steps:

* Updated the package list
* Installed Apache
* Created a custom `index.html` file in `/var/www/html`
* Enabled and started the Apache service

Terraform passed the cloud-init file into the EC2 instance using:

```hcl
user_data = file("${path.module}/cloud-init.yaml")
```

This allowed the EC2 instance to come online fully configured without requiring any manual installation steps.

## Screenshot

The screenshot below shows the Apache web page created by cloud-init.

![Cloud-Init Screenshot](terraform/assignment-2-cloud-init-ec2/screenshots/cloud-init-working.png)

