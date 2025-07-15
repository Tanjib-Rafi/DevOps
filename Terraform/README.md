| Term         | Description                                                                                                               |
| ------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **provider** | Specifies the cloud platform or service (e.g., AWS, Azure, GCP, etc.). Needed to provision resources.                     |
| **resource** | Defines a piece of infrastructure to create (e.g., an EC2 instance, S3 bucket, etc.).                                     |
| **variable** | Input values you can parameterize for reuse or customization (e.g., `instance_type = var.type`).                          |
| **output**   | Displays values after apply, such as public IPs or IDs. Useful for chaining or debugging.                                 |
| **module**   | Reusable container of Terraform code. Helps organize and reuse infrastructure.                                            |
| **state**    | Stores the current status of your infrastructure (in `.tfstate` file). Terraform uses this to track real-world resources. |



| Command             | Description                                                                     |
| ------------------- | ------------------------------------------------------------------------------- |
| `terraform init`    | Initializes the working directory. Downloads provider plugins. Run this first.  |
| `terraform plan`    | Shows what Terraform **will do** (add/change/destroy) before applying. Dry run. |
| `terraform apply`   | Executes the plan and actually creates/changes resources.                       |
| `terraform destroy` | Destroys all resources managed by Terraform. Use with caution!                  |



## 📁 Terraform File Reference Guide

| File Name                 | Purpose                                        | Description                                                                                 | Example                                                                                         |
|---------------------------|------------------------------------------------|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `main.tf`                 | Main configuration                             | Declares resources (e.g., AWS EC2, VPC), modules, locals, and data sources                 | ```hcl<br>resource "aws_instance" "web" {<br>  ami = var.ami_id<br>  instance_type = "t3.micro"<br>}``` |
| `variables.tf`            | Declare input variables                        | Defines variable names, types, defaults, and descriptions                                  | ```hcl<br>variable "region" {<br>  type = string<br>  default = "us-east-1"<br>}```              |
| `terraform.tfvars`        | Provide values for input variables             | Supplies actual values used in `plan`/`apply`, especially per environment                  | ```hcl<br>region = "ap-south-1"<br>instance_type = "t3.micro"<br>```                             |
| `outputs.tf`              | Export values from the config                  | Allows Terraform to display or pass important outputs like IPs, URLs, ARNs                 | ```hcl<br>output "alb_dns" {<br>  value = aws_lb.main.dns_name<br>}```                           |
| `backend.tf`              | Remote state configuration                     | Specifies S3/DynamoDB or other backend to store state safely in teams                      | ```hcl<br>terraform {<br>  backend "s3" {<br>    bucket = "my-tfstate"<br>    key = "prod.tfstate"<br>  }<br>}``` |
| `provider.tf`             | Configure provider plugins                     | Defines cloud providers (e.g., AWS, Azure, GCP) with region, profile, etc.                 | ```hcl<br>provider "aws" {<br>  region = var.region<br>}```                                     |
| `versions.tf`             | Lock required Terraform and provider versions | Ensures consistent versions across teams/CI                                                | ```hcl<br>terraform {<br>  required_version = ">= 1.4.0"<br>}```                                 |
| `terraform.lock.hcl`      | Lock provider versions                         | Auto-generated; locks exact versions of providers for reproducibility                      | ```hcl<br>provider "registry.terraform.io/hashicorp/aws" {<br>  version = "5.38.0"<br>}```       |
| `.terraform/`             | Local cache of providers/modules               | Internal directory created by `terraform init`; should be in `.gitignore`                  | *Do not edit manually*                                                                          |
| `terraform.tfstate`       | Stores real-world infrastructure state        | Contains actual resource IDs, IPs, metadata — DO NOT COMMIT                                | *Sensitive file; use remote state in prod*                                                      |
| `terraform.tfstate.backup`| Auto-created backup of last state             | Helps recover if the main state is corrupted or deleted                                    | *Used internally*                                                                               |

---

### ✅ Recommended to Commit:
- `*.tf`, `terraform.tfvars.example`, `.terraform.lock.hcl`

### 🚫 Never Commit:
- `terraform.tfstate`, `*.tfvars`, `.terraform/`

### 🔄 Relationship:
- `variables.tf` is like a form definition.
- `terraform.tfvars` is the filled-out form with values.

### 📌 Best Practice:
- Add `.tfvars` to `.gitignore` if it contains secrets or env-specific data.



## 🪣 Store Terraform State Remotely (Production Ready)

### Why?
- Prevents conflicts when multiple people run Terraform
- Enables collaboration, locking, and versioning
- Keeps state file safe

---

### 🔧 Recommended Backend

**Use Terraform Cloud** *or* **S3 + DynamoDB** (for AWS users)

---

### ✅ Example: S3 + DynamoDB Backend

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-states"
    key            = "prod/app/terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-locks"
  }
}
