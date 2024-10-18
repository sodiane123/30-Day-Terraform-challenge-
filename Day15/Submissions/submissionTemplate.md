# Day 15: Working with Multiple AWS Regions
To manage infrastructure across multiple AWS regions, use provider aliases in your Terraform configuration:

## Participant Details

- **Name:sodiane123
- **Task Completed:Working with Multiple AWS Regions
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
When deploying resources in multiple regions, specify the provider alias

resource "aws_instance" "west_instance" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  provider      = aws
}

resource "aws_instance" "east_instance" {
  ami           = "ami-789101"
  instance_type = "t2.micro"
  provider      = aws.us_east
}
Creating Multi-Provider Modules
variable "aws_provider" {
  description = "AWS provider"
}

variable "gcp_provider" {
  description = "GCP provider"
}

resource "aws_instance" "aws_vm" {
  ami           = "ami-123456"
  instance_type = "t2.micro"
  provider      = var.aws_provider
}

resource "google_compute_instance" "gcp_vm" {
  name         = "gcp-vm"
  machine_type = "e2-micro"
  zone         = "us-central1-a"
  provider     = var.gcp_provider
}
When calling the module, pass the provider configuration:

hcl
module "multi_provider" {
  source       = "./modules/aws_gcp"
  aws_provider = aws
  gcp_provider = google
}

Use the aws_eks_cluster resource to create a Kubernetes cluster:

hcl

resource "aws_eks_cluster" "my_cluster" {
  name     = "my-cluster"
  role_arn = aws_iam_role.eks_role.arn

  vpc_config {
    subnet_ids = aws_subnet.eks_subnet[*].id
  }
}
After setting up the EKS cluster, use the Kubernetes provider to deploy Docker containers:

hcl

provider "kubernetes" {
  host                   = aws_eks_cluster.my_cluster.endpoint
  cluster_ca_certificate = base64decode(aws_eks_cluster.my_cluster.certificate_authority[0].data)
  token                  = data.aws_eks_cluster_auth.my_cluster.token
}

resource "kubernetes_deployment" "nginx" {
  metadata {
    name = "nginx"
  }

  spec {
    replicas = 2

    template {
      metadata {
        labels = {
          app = "nginx"
        }
      }

      spec {
        container {
          image = "nginx:latest"
          name  = "nginx"
        }
      }
    }
  }
}





```
## Architecture 

[Name](link to image in S3 bucket)
