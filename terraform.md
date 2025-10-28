How do you securely store the state file?

“State files contain sensitive data like credentials, so I never keep them locally.
I use remote backends like AWS S3 with DynamoDB for state locking, or Terraform Cloud for managed storage.
I also enable encryption at rest and restrict access with IAM policies.”

### How do you avoid storing secrets in Terraform/Terragrunt?

“I avoid hardcoding secrets in Terraform variables. Instead, I use data sources that fetch secrets dynamically from AWS Secrets Manager or Vault.
In Terragrunt, I can use environment variables or external secret backends.
This way, secrets are never exposed in code or state files.”

### How to restrict resource deletion but allow init/plan/apply?

“Terraform has a lifecycle block where I can use prevent_destroy = true.
That stops accidental deletion of critical resources like databases or VPCs, while still allowing changes or new resource creation.”

### Difference between count and for_each?

“count is used when I want to create multiple resources based on a numeric value — like creating 3 EC2 instances.
for_each is used when I want to create resources based on a map or set — it gives more control and allows identifying specific items by key.”

### Lifecycle blocks — real-world use cases

“Common lifecycle settings include:

create_before_destroy for zero-downtime replacements,

ignore_changes to skip certain attributes managed outside Terraform,

prevent_destroy to protect critical resources,

replace_triggered_by to recreate when another resource changes”

### What happens during terraform init, plan, apply?

“terraform init sets up the backend and downloads provider plugins.
terraform plan compares the current state with configuration to show proposed changes.
terraform apply executes those changes and updates the state file.”
