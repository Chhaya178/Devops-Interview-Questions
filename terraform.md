###How do you securely store the state file?

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

### How do you use Terraform in your environment?

I use Terraform for provisioning and managing infrastructure as code.
For example, I’ve created reusable Terraform modules for AWS services like VPC, EC2, EKS, and RDS.
I maintain separate workspaces for dev, staging, and prod environments and store state files remotely in an S3 bucket with DynamoDB table for state locking.
This allows version control, consistency, and easy rollback of infrastructure changes.

### How will you utilize Terraform modules and version upgrade in your environment?

I structure Terraform code using modules for reusability — for example, one module for networking, one for compute, one for IAM.
Each module is version-controlled in Git. When upgrading Terraform or a provider version, I test it first in a dev workspace using terraform init -upgrade, then apply changes in staging before promoting to production.
This ensures backward compatibility and reduces production risk.

### What security, autoscaling, and scalability approaches are you using in your environment?

For security, I implement IAM roles with least privilege, use encrypted S3 buckets and EBS volumes, enable security groups and NACLs, and enforce SSL/TLS for data in transit.
For autoscaling, I configure AWS Auto Scaling Groups for EC2 and Horizontal Pod Autoscaler (HPA) in Kubernetes based on CPU/memory utilization.
For scalability, I use load balancers (ALB/NLB) with multi-AZ deployment and Infrastructure-as-Code (Terraform) to replicate infrastructure easily across regions.

### Can you give some instances of using Ansible?

I use Ansible mainly for configuration management and post-provisioning automation.
Examples:

Installing Docker and Kubernetes components on EC2 instances

Setting up Prometheus and Grafana monitoring agents

Automating package updates and security patches
I use Ansible playbooks integrated with Jenkins pipelines to achieve consistent configurations.

### What are you doing for monitoring your resources?

I use a combination of Prometheus + Grafana for metrics, ELK/EFK stack for logs, and CloudWatch for AWS services.
Alerts are configured via Alertmanager (email/Slack).
I also use tools like Loki for lightweight log aggregation and Node Exporter for system-level metrics.
This setup helps in proactive monitoring and quick troubleshooting.

### Suppose you want to host one application job on any cloud. How will you approach it?

First, I’ll identify the application requirements — language, dependencies, storage, scalability, and networking.
Then I’ll choose an appropriate service (like EC2, ECS, or EKS).
I’ll write Terraform scripts to provision infrastructure, set up CI/CD using Jenkins/GitHub Actions, containerize the app with Docker, deploy it to Kubernetes, and expose it via ALB or Ingress.
I’ll also integrate monitoring and logging from day one.

### What will be your approach for creating a security group for the instance?

I’ll define security groups using Terraform — specifying ingress and egress rules based on the principle of least privilege.
For example, allowing port 22 from specific IPs for SSH and port 80/443 for web traffic.
I’ll use variables for flexibility and tag resources for easier management.
Everything is version-controlled in Git to ensure auditable security changes.
