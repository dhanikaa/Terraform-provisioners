# Terraform and Flask App on AWS

This project demonstrates how to use **Terraform** to provision an **AWS infrastructure** and deploy a **Flask web application**. The Flask app is deployed on an **EC2 instance** within a VPC, with a public subnet and a security group configured for HTTP and SSH access.

## Architecture Overview

- **AWS Infrastructure:**
  - **VPC** with CIDR block `10.0.0.0/16`
  - **Subnet** in `us-east-1a` with CIDR block `10.0.0.0/24`
  - **Internet Gateway** for internet connectivity
  - **Security Group** to allow HTTP (port 80) and SSH (port 22) access
  - **EC2 Instance** running a Flask app

- **Flask Application:**
  - The Flask application is a simple "Hello, Terraform!" web service running on port 80.

## Pre-requisites

Before you begin, ensure that you have the following installed on your local machine:

- [Terraform](https://www.terraform.io/downloads)
- [AWS CLI](https://aws.amazon.com/cli/)
- [Python](https://www.python.org/downloads/)
- [SSH Key Pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) for secure SSH access to the EC2 instance

Make sure to generate an SSH key pair and place the public key in the correct location on your system:

```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa
```

## Getting Started

Follow these steps to deploy the Flask app on AWS using Terraform:

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd <your-repository-folder>
```

### 2. Initialize Terraform

Run the following command to initialize the Terraform configuration and download the necessary provider plugins.

```bash
terraform init
```

### 3. Apply the Terraform Configuration

Run the following command to create the AWS resources specified in the `main.tf` file:

```bash
terraform apply
```

This command will prompt you to confirm the action. Type `yes` to proceed.

### 4. SSH into the EC2 Instance

Once the `terraform apply` process is complete, note the public IP address of the EC2 instance that was created. You can find this in the Terraform output or the AWS EC2 Dashboard.

SSH into the EC2 instance using the private key you generated earlier:

```bash
ssh -i ~/.ssh/id_rsa ubuntu@<ec2-public-ip>
```

### 5. Access the Flask Application

After SSHing into the EC2 instance, the Flask application will be running on port 80. Open your web browser and navigate to the public IP address of the instance:

```
http://<ec2-public-ip>
```

You should see the message:

```
Hello, Terraform!
```

## Files

- `app.py`: The Flask application that returns a simple message “Hello, Terraform!”
- `main.tf`: Terraform configuration file that defines the AWS resources (VPC, subnet, security group, EC2 instance).
- `terraform.tfvars`: Optionally, you can use this file to define your variable values, such as the CIDR block for your VPC.

## Resources Created

- **VPC** with CIDR block `10.0.0.0/16`
- **Subnet** in availability zone `us-east-1a`
- **Internet Gateway** to enable public internet access
- **Security Group** allowing HTTP and SSH traffic
- **EC2 Instance** running the Flask application on Ubuntu

## Clean Up

To remove all the resources created by Terraform, run the following command:

```bash
terraform destroy
```

This will prompt you to confirm the deletion of all resources. Type `yes` to proceed.

## Troubleshooting

- If the Flask app is not accessible, check the Security Group settings to ensure that port 80 is open for inbound traffic.
- If the EC2 instance is not starting, check the instance logs in the AWS EC2 console for more details.