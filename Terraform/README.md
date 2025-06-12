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



| File Name           | Purpose                                      | Description                                                                 | Example                                                                 |
|---------------------|----------------------------------------------|-----------------------------------------------------------------------------|-------------------------------------------------------------------------|
| `variables.tf`      | Declare input variables                      | Defines variable names, types, defaults, and descriptions                  | ```hcl<br>variable "region" {<br>  type = string<br>  default = "us-east-1"<br>}``` |
| `terraform.tfvars`  | Provide values for declared input variables  | Supplies actual values for use during `terraform plan`/`apply`             | ```hcl<br>region = "ap-south-1"<br>```                                  |

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
