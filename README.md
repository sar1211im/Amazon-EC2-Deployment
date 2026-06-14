# AWS EC2 Deployment using Terraform & Docker

## 📌 Project Overview

This project demonstrates how to provision and automate AWS EC2 infrastructure using Terraform and Docker. The infrastructure is deployed on AWS Cloud using Infrastructure as Code (IaC) practices, and Docker is automatically installed using `user_data` scripts. An Nginx container is deployed on the EC2 instance for web hosting.

---

## 🚀 Technologies Used

* AWS EC2
* Terraform
* Docker
* Nginx
* Git & GitHub
* Linux

---

## 🛠️ Features

* Automated EC2 instance provisioning using Terraform
* Infrastructure as Code (IaC) implementation
* Automated Docker installation using `user_data`
* Nginx container deployment on EC2
* Version control using Git and GitHub
* Scalable and repeatable deployment workflow

---

## 📂 Project Structure

```bash
terraform-ec2-docker/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
└── README.md
```

---

## ⚙️ Prerequisites

Before starting, ensure you have:

* AWS Account
* AWS CLI configured
* Terraform installed
* Git installed
* AWS Key Pair created

---

## 🔑 Configure AWS Credentials

Run the following command:

```bash
aws configure
```

Provide:

* AWS Access Key
* AWS Secret Key
* Region
* Output format

---

## 📝 Terraform Configuration

main.tf:

provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web_server" {
  ami           = "ami-0f5ee92e2d63afc18"
  instance_type = "t2.micro"
  key_name      = "your-key-name"

  user_data = <<-EOF
              #!/bin/bash
              yum update -y
              yum install docker -y
              systemctl start docker
              docker run -d -p 80:80 nginx
              EOF

  tags = {
    Name = "Terraform-Docker-Server"
  }
}


--------

# variables.tf:

variable "aws_region" {
  description = "AWS region for deployment"
  default     = "ap-south-1"
}

variable "instance_type" {
  description = "EC2 instance type"
  default     = "t2.micro"
}

variable "ami_id" {
  description = "Amazon Linux AMI ID"
  default     = "ami-0f5ee92e2d63afc18"
}

variable "key_name" {
  description = "AWS EC2 Key Pair Name"
  default     = "your-key-name"
}



--------

terraform.tfvars:


aws_region   = "ap-south-1"
instance_type = "t2.micro"
ami_id       = "ami-0f5ee92e2d63afc18"
key_name     = "your-key-name"

---------

outputs.tf:


output "instance_public_ip" {
  description = "Public IP of EC2 Instance"
  value       = aws_instance.web_server.public_ip
}

output "instance_id" {
  description = "EC2 Instance ID"
  value       = aws_instance.web_server.id
}

output "instance_state" {
  description = "State of EC2 Instance"
  value       = aws_instance.web_server.instance_state


---------


▶️ Procedure
Step 1 — Initialize Terraform
terraform init
Purpose

Downloads required Terraform providers and initializes the project.

Step 2 — Validate Terraform Code
terraform validate
Purpose

Checks configuration syntax and validates Terraform files.

Step 3 — Preview Infrastructure
terraform plan
Purpose

Displays resources Terraform will create.

Step 4 — Deploy Infrastructure
terraform apply

Type:

yes
Purpose

Creates AWS EC2 infrastructure and installs Docker automatically.

--------

## 🌐 Access Application

After deployment, open:

```bash
http://<EC2-Public-IP>
```

You will see the Nginx welcome page.

---

## 🧹 Destroy Infrastructure

To avoid AWS charges:

```bash
terraform destroy
```

---

## 📈 Learning Outcomes

* Infrastructure as Code (IaC)
* AWS EC2 provisioning
* Docker container deployment
* Terraform automation workflow
* Cloud infrastructure management
* Basic DevOps practices

---

## 👨‍💻 Author

Sheikh Sarim

GitHub: https://github.com/sar1211im

