| Term         | Description                                                                                                               |
| ------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **provider** | Specifies the cloud platform or service (e.g., AWS, Azure, GCP, etc.). Needed to provision resources.                     |
| **resource** | Defines a piece of infrastructure to create (e.g., an EC2 instance, S3 bucket, etc.).                                     |
| **variable** | Input values you can parameterize for reuse or customization (e.g., `instance_type = var.type`).                          |
| **output**   | Displays values after apply, such as public IPs or IDs. Useful for chaining or debugging.                                 |
| **module**   | Reusable container of Terraform code. Helps organize and reuse infrastructure.                                            |
| **state**    | Stores the current status of your infrastructure (in `.tfstate` file). Terraform uses this to track real-world resources. |

