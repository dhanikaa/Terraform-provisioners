# AWS EC2 Flask App Deployment with Terraform

This project demonstrates the use of Terraform to set up a basic AWS infrastructure. It provisions an EC2 instance running a Flask application, along with a VPC, subnet, internet gateway, and security group.

## Overview

This Terraform configuration performs the following steps:

1. **Provider Configuration:**
   - Configures Terraform to use AWS in the `us-east-1` region.

2. **Variable:**
   - Defines a CIDR block `10.0.0.0/16` for the VPC.

3. **AWS Key Pair:**
   - Creates an SSH key pair named `terraform-demo` using the public key from `~/.ssh/id_rsa.pub`.

4. **AWS VPC:**
   - Creates a VPC with a CIDR block of `10.0.0.0/16`.

5. **AWS Subnet:**
   - Creates a subnet within the VPC with a CIDR block of `10.0.0.0/24`, specifically in availability zone `us-east-1a`, enabling public IP assignment.

6. **AWS Internet Gateway:**
   - Attaches an internet gateway to the VPC to enable internet access for instances.

7. **AWS Route Table & Association:**
   - Sets up a route table for routing traffic to the internet through the internet gateway and associates it with the subnet.

8. **AWS Security Group:**
   - Creates a security group allowing HTTP (port 80) and SSH (port 22) traffic from anywhere, and egress traffic to anywhere.

9. **AWS EC2 Instance:**
   - Launches a `t2.micro` EC2 instance using the specified Amazon Machine Image (AMI).
   - The instance is connected to the subnet and security group and is configured for SSH access.

10. **Provisioners:**
    - Copies the `app.py` file to the instance and runs commands to:
      1. Update the package list.
      2. Install Python's pip package manager.
      3. Install Flask.
      4. Run the `app.py` Flask application in the background.

## How to Run

1. Clone the repository:
   ```bash
   git clone <repository-url>
   ```

2. Initialize Terraform:
   ```bash
   terraform init
   ```

3. Apply the Terraform configuration:
   ```bash
   terraform apply
   ```

4. Follow the prompt to confirm the infrastructure creation.

After successful deployment, the EC2 instance will be running the Flask app, and you can SSH into it using the key specified.

---

This project provides a simple template to deploy a Python Flask application on AWS using Terraform.
