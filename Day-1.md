# Day 1 - Create Key Pair Using Terraform

## ✅ Task Goal

  Create an AWS key pair using Terraform

  Key name: datacenter-kp

  Type: RSA

  Private key saved at: /home/bob/datacenter-kp.pem

  Terraform directory: /home/bob/terraform

  File: main.tf only

##  Step 1: Open terminal

In VS Code → Right-click Explorer → Open in Integrated Terminal
```bash
cd /home/bob/terraform
```
##  **Step 2**: Create main.tf
```bash
vi main.tf
```

**Paste this exact content:**
```bash
provider "aws" {
  region = "us-east-1"
}

resource "tls_private_key" "datacenter" {
  algorithm = "RSA"
  rsa_bits  = 2048
}

resource "aws_key_pair" "datacenter_kp" {
  key_name   = "datacenter-kp"
  public_key = tls_private_key.datacenter.public_key_openssh
}

resource "local_file" "private_key" {
  content         = tls_private_key.datacenter.private_key_pem
  filename        = "/home/bob/datacenter-kp.pem"
  file_permission = "0400"
}
```
## Save and exit (:wq).

##  Step 3: Initialize Terraform
```bash
terraform init
```
##  Step 4: Apply configuration
```bash
terraform apply -auto-approve
```
##  Step 5: Verify
```bash
ls -l /home/bob/datacenter-kp.pem
```
## File should exist with read-only permissions.

If the file exists, you are 100% done ✔️

Good job 👍
You can now move to the next task.

## ✅ Task Completed

✔ Key pair created

✔ RSA type used

✔ Private key saved correctly

✔ Only main.tf used

## Screenshots

<img width="1050" height="915" alt="Screenshot 2025-12-14 194211" src="https://github.com/user-attachments/assets/daee86f0-e74e-4171-b689-cc031694c50d" />

<img width="1033" height="979" alt="Screenshot 2025-12-14 194220" src="https://github.com/user-attachments/assets/e2fc199c-eb31-46af-870f-644b5ca8120d" />

<img width="1700" height="900" alt="Screenshot 2025-12-14 194147" src="https://github.com/user-attachments/assets/55d28585-2cc3-47b7-8bff-9aeb1768252f" />

<img width="1006" height="914" alt="Screenshot 2025-12-14 194123" src="https://github.com/user-attachments/assets/79ca9330-d376-4a02-b4ad-7fb26a535382" />

