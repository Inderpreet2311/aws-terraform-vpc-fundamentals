# AWS VPC Infrastructure with Terraform

Hands-on Terraform labs covering AWS provider setup through multi-resource networking with dependencies, variables, and data sources. Built while studying for the HashiCorp Terraform Associate certification.

## What This Project Demonstrates

- Configuring the Terraform AWS provider and managing version constraints
- Provisioning a VPC and understanding in-place updates vs. forced replacement
- Using variables, `terraform.tfvars`, and variable precedence to avoid hardcoded values
- Applying provider-level default tags for consistent resource tagging
- Managing multiple interconnected resources (subnets, route tables, route table associations, security groups) and understanding Terraform's implicit dependency resolution
- Using data sources (`aws_region`, `aws_availability_zones`, `aws_caller_identity`) to make configurations dynamic and environment-aware
- Working with Terraform outputs, including sensitive output handling
- Core Terraform CLI workflow: `fmt`, `validate`, `plan`, `apply`, `state list`, `state show`, `output`, `destroy`

## Repository Structure

```
aws-terraform-vpc-fundamentals/
├── terraform/                  # Core VPC configuration (Labs 1–4)
│   ├── main.tf                 # VPC, subnets, route table, security group
│   ├── variables.tf            # Input variable definitions
│   ├── terraform.tfvars        # Variable value overrides
│   ├── outputs.tf              # Output values (VPC ID, ARN, subnet IDs, etc.)
│   └── providers.tf            # AWS provider and version constraints
├── development/                 # Data source exploration environment (Lab 5)
│   ├── main.tf                 # VPC/subnet built using data source lookups
│   ├── variables.tf
│   ├── outputs.tf
│   └── providers.tf
└── README.md
```

## Lab Progression

| Lab | Focus | Key Concepts |
|-----|-------|---------------|
| 01 | Provider setup | `terraform init`, `fmt`, `validate`, version constraints |
| 02 | First resource | VPC creation, in-place update vs. resource replacement |
| 03 | Variables & outputs | `variable` blocks, `terraform.tfvars`, variable precedence, default tags, `output` blocks |
| 04 | Multi-resource dependencies | Subnets, route tables, route table associations, security groups, implicit dependencies |
| 05 | State & data sources | `terraform state` commands, `aws_region`/`aws_availability_zones`/`aws_caller_identity` data sources, sensitive outputs |

## Key Takeaways

**Variable precedence matters.** Command-line `-var-file` flags override `terraform.tfvars`, which overrides variable defaults. Understanding this order prevents unexpected resource replacement in real environments.

**Not everything is caught by `validate`.** Some errors — like a missing string quote in a `.tfvars` file — only surface at `plan` or `apply`. Testing the full workflow matters, not just static checks.

**Implicit dependencies keep configurations safe.** Terraform automatically sequences resource creation (VPC → subnets → route table associations) based on resource references, without needing to manually define build order.

**Data sources reduce hardcoding.** Pulling account ID, region, and availability zones dynamically makes configurations portable across accounts and regions without manual edits.

## Tools

Terraform 1.12.2 · AWS Provider (`hashicorp/aws` ~> 5.0 / ~> 6.0) · AWS CLI

## Next Steps

- Extend the VPC with NAT Gateway and internet gateway for full public/private subnet routing
- Add auto scaling group and load balancer as part of a three-tier architecture project
- Migrate local state to an S3 backend with DynamoDB state locking
- Introduce Terraform modules to make this VPC configuration reusable across environments
