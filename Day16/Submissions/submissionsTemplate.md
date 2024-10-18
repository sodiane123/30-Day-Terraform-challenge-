# Day 16:Building Production-Grade Infrastructure
Modular code is essential for production infrastructure. Each module should be small, composable, and reusable. Here's how you can refactor a typical infrastructure project:

    Create Modules Directory: Structure your project by creating a modules/ directory. Each module (e.g., VPC, EC2, S3) should have its own subdirectory with its own configuration files.

## Participant Details

- **Name:Sodiane123
- **Task Completed:Building Production-Grade Infrastructure
- **Date and Time:10/18/24

## Terraform Code 
```hcl
# modules/vpc/main.tf
resource "aws_vpc" "my_vpc" {
  cidr_block = var.cidr_block
}

output "vpc_id" {
  value = aws_vpc.my_vpc.id
}

# modules/vpc/variables.tf
variable "cidr_block" {
  description = "The CIDR block for the VPC"
  type        = string
}
Invoke Modules in Root Configuration:

In your root module (e.g., main.tf), invoke the VPC module:

hcl

    module "vpc" {
      source     = "./modules/vpc"
      cidr_block = "10.0.0.0/16"
    }

Implement Version Control for Modules:

Production-grade Terraform requires version control for your modules. You can either use versioning for internal modules via a Git repository or reference publicly available modules with versions.

For example, using a public AWS VPC module with versioning:

hcl

module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "2.78.0"
  cidr    = "10.0.0.0/16"
}



```
## Architecture 

[Name](link to image in S3 bucket)
