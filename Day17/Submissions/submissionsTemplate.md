# Day 17:Manual Testing Activity for Terraform Configuration 
Perform Manual Tests

    Verify Resource Creation:

    After running your Terraform configuration, check whether the resources are created as expected.

        Example: If you have a module creating an AWS EC2 instance, verify in the AWS Management Console that the EC2 instance is running, the correct instance type is used, and the instance is deployed in the correct region.

        Steps:
            Run terraform apply in your terminal.
            Go to the AWS Console and check the EC2 dashboard to verify the instance.
            Confirm that the attributes (e.g., VPC, security groups, tags) match the configuration.

  

terraform apply

Check Infrastructure Behavior:

Validate the behavior of the infrastructure across different environments (development, staging, production).

    Example: In a multi-environment setup, ensure that your development environment uses smaller instance types (e.g., t2.micro) and your production environment uses larger types (e.g., t3.large).

    Steps:
        Set up different environment variables or workspaces (dev, staging, prod).
        Apply the configuration for each environment and verify the behavior.



    terraform workspace new dev
    terraform apply

Test for Regressions:

Ensure that the changes you made do not break existing infrastructure or introduce any regressions.

    Steps:
        Use terraform plan to simulate changes and ensure no unexpected modifications are introduced.
        Manually inspect the output of the plan to confirm that only intended changes are listed.

  

        terraform plan

Step 2: Cleanup After Tests

To avoid incurring costs or leaving unwanted resources, clean up the infrastructure after testing.

    Steps:
        Run terraform destroy to remove all the resources created during the manual tests.
        Verify in the cloud provider's console (e.g., AWS or GCP) that all resources have been deleted.

  

    terraform destroy

    Example Cleanup Verification:
        Ensure that EC2 instances, RDS databases, and any other resources created for testing are properly deleted.
        Check that there are no lingering S3 buckets, VPCs, or IAM roles.



## Participant Details

- **Name:sodiane123
- **Task Completed:Manual Testing Activity for Terraform Configuration
- **Date and Time:10/18/24 

## Terraform Code 
```hcl


```
## Architecture 

[Name](link to image in S3 bucket)
