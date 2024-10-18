# Day 14: Working with multiple providers
What Is a Provider? A provider in Terraform is responsible for understanding the API interactions between your infrastructure and a service, like AWS, Azure, or GCP. Each provider allows Terraform to interact with cloud platforms or other APIs

## Participant Details

- **Name:Sodiane123
- **Task Completed:Understtod how to use multiple providers in a single configuration file
- **Date and Time:10/18/24 

## Terraform Code 
```hcl
provider "aws" {
  region = "us-west-1"
}

provider "aws" {
  alias  = "us_east"
  region = "us-east-1"
}

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
    google = {
      source  = "hashicorp/google"
      version = "~> 3.0"
    }
  }
}




```
## Architecture 

[Name](link to image in S3 bucket)
