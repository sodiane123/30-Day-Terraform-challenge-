# Day 13: Secure secrete management using AWS sECRETE MANAGER

## Participant Details

- **Name:Sodiane123
- **Task Completed:Learned how to manage sensitive data securely within Terraform
- **Date and Time:10/18/24 

## Terraform Code 
```hcl
resource "aws_secretsmanager_secret" "example" {
  name        = "my-secret"
  description = "This secret contains sensitive information"
}

resource "aws_secretsmanager_secret_version" "example_version" {
  secret_id     = aws_secretsmanager_secret.example.id
  secret_string = jsonencode({
    username = "admin"
    password = "SuperSecretPassword"
  })
}

To ensure sensitive data is masked or encrypted in your Terraform state file, you can use Terraform’s sensitive attribute:

hcl

output "secret_value" {
  value     = data.aws_secretsmanager_secret_version.example_version.secret_string
  sensitive = true
}

If you are using remote state (e.g., AWS S3 for state storage), ensure that the state file is encrypted:

hcl

terraform {
  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "state/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    kms_key_id     = "alias/my-kms-key"
    dynamodb_table = "terraform-lock"
  }
}



```
## Architecture 

[Name](link to image in S3 bucket)
