# Day 18: Automated Testing for Terraform Code 

## Participant Details

- **Name:sodaine123
- **Task Completed:Automated Testing for Terraform Code
- **Date and Time:10/18/24 

## Terraform Code 
```hcl
Terraform itself does not have built-in support for writing automated tests in HCL directly. However, you can integrate testing with tools like Terratest (written in Go) or use kitchen-terraform. Below is an HCL-based setup with Terraform for running automated tests via Terratest.

Terratest does the testing part, and Terraform focuses on provisioning. To facilitate testing, we configure Terraform resources and outputs that are validated using Terratest or other external tools.
Example: HCL Code for Automated Testing

In this example, we'll provision simple infrastructure (e.g., AWS EC2) and then set up outputs that will be verified via Terratest.
1. Terraform Configuration (HCL) – main.tf

hcl

# AWS Provider Configuration
provider "aws" {
  region = "us-west-2"
}

# Define a VPC
resource "aws_vpc" "example" {
  cidr_block = "10.0.0.0/16"
}

# Define an EC2 instance
resource "aws_instance" "example" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  subnet_id     = aws_vpc.example.id

  tags = {
    Name = "TerraformInstance"
  }
}

# Outputs for testing
output "instance_id" {
  value = aws_instance.example.id
}

output "public_ip" {
  value = aws_instance.example.public_ip
}

output "vpc_id" {
  value = aws_vpc.example.id
}
GitHub Actions for CI/CD

Here’s an example of how you could integrate this into a CI/CD pipeline using GitHub Actions to automatically run the Terratest code:

yaml

name: Terraform Test

on:
  push:
    branches:
      - main

jobs:
  terraform:
    name: Terraform Testing
    runs-on: ubuntu-latest

    steps:
      - name: Checkout the repository
        uses: actions/checkout@v2

      - name: Set up Go
        uses: actions/setup-go@v2
        with:
          go-version: '1.16'

      - name: Install dependencies
        run: |
          go get -v github.com/gruntwork-io/terratest/modules/terraform
          go get -v github.com/gruntwork-io/terratest/modules/aws

      - name: Run Terraform Tests
        run: go test -v ./test

```
## Architecture 

[Name](link to image in S3 bucket)
