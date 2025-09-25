## Kubernetes & Terraform

### What is StatefulSet?

- What: StatefulSet is a Kubernetes workload used for stateful applications where each pod needs a unique identity.

- Why: It maintains stable pod names, persistent storage, and ordered deployments.

- Where/How: I use it for databases like MySQL or MongoDB where data and pod identity must persist even after restarts.

### Where do you store the statefile?

- What: Terraform keeps infrastructure information in a state file.

- Why: It tracks real resources to know what’s already deployed.

- Where/How: By default, it’s stored locally, but in production, I use S3 with DynamoDB for locking and versioning so the team can collaborate securely.

### What is a null resource in Terraform?

- What: A null resource is a resource that doesn’t create infrastructure.

- Why: It lets me run scripts or commands after deployment.

- Where/How: I usually use it with local-exec or remote-exec provisioners when I need to run a shell script post-deployment.

### How can you secure the Terraform state file?

- What: Securing the state file is important because it may have secrets like DB passwords.

- Why: If exposed, it can cause security risks.

- Where/How: I use a remote backend like S3 with KMS encryption, enable versioning, IAM roles for access, and Vault for secrets management.

### What are Terraform workspaces?

- What: Workspaces are like different environments using the same Terraform code.

- Why: It avoids maintaining separate code for dev, staging, and prod.

- Where/How: I create them with terraform workspace new dev and switch using workspace select prod.

### Explain the Terraform module and its purpose.

- What: A module is a reusable set of Terraform configurations.

- Why: It reduces code duplication and maintains standardization.

- Where/How: I create modules for VPCs or EC2 instances and call them in main.tf across multiple environments.

## DevOps

### What is DevOps? How is it different from traditional IT practices?

- What: DevOps combines development and operations for faster, automated, and reliable delivery.

- Why: It removes silos and reduces release cycles.

- Where/How: In traditional IT, deployments were manual and slow. With DevOps, I use CI/CD pipelines, automation, and tools like Jenkins, Docker, and Kubernetes.

### Benefits of implementing DevOps

- What: It brings speed, automation, and collaboration to software delivery.

- Why: Businesses want faster releases with fewer errors.

- Where/How: Using CI/CD, containers, infrastructure-as-code, and monitoring tools for continuous feedback.

### Explain the DevOps lifecycle.

- What: It’s the process from planning to monitoring software.

- Why: To ensure faster delivery with continuous feedback.

- Where/How: The stages are Plan → Code → Build → Test → Release → Deploy → Operate → Monitor → Feedback using tools like Jira, Git, Jenkins, Kubernetes, and Prometheus.

### Explain the CI/CD pipeline and its benefits.

- What: CI/CD pipeline automates code build, testing, and deployment.

- Why: It speeds up delivery, reduces errors, and ensures consistency.

- Where/How: I use Jenkins or GitLab CI with automated testing and deployment to Kubernetes.

### Difference between Terraform, Ansible, and CloudFormation

- What: Terraform is for infra provisioning, Ansible is for configuration management, and CloudFormation is AWS-specific provisioning.

- Why: Each has a different purpose—Terraform and CloudFormation are declarative; Ansible is procedural.

- Where/How: I use Terraform for multi-cloud infra, Ansible for app config, and CloudFormation when it's AWS-only.

### Explain blue-green deployment strategy

- What: It’s a deployment method using two environments—Blue is live, Green is new.

- Why: Ensures zero downtime and easy rollback.

- Where/How: I test the new version on Green, then switch traffic to it using load balancers.

## Jenkins

### What are parameterized jobs in Jenkins?

- What: These jobs accept inputs like branch name or environment before running.

- Why: Makes pipelines reusable and flexible.

- Where/How: I enable "This project is parameterized" in Jenkins and pass parameters in the pipeline script.

### What are the different plugins you have used?

- What: Plugins extend Jenkins’ features.

- Why: To integrate SCM, code quality, containers, and notifications.

- Where/How: I use Git, Pipeline, Docker, SonarQube, Slack, and Credentials Binding plugins frequently.

### What is the default root directory of Jenkins?

- What: The directory where Jenkins stores job configs, plugins, and builds.

- Why: It’s important for backup and migration.

- Where/How: On Linux, it’s /var/lib/jenkins, and on Windows, it’s C:\Program Files (x86)\Jenkins.

### Types of jobs in Jenkins

- What: Jenkins offers different job types.

- Why: To support everything from simple builds to multi-branch pipelines.

- Where/How: I use Freestyle, Pipeline, Multibranch Pipeline, and Multiconfiguration jobs based on project needs.

### How do you ensure the security of your CI/CD pipeline?

- What: Security ensures safe code, secrets, and deployments.

- Why: To prevent data leaks and unauthorized access.

- Where/How: I use RBAC, encrypt credentials, enable HTTPS, integrate code scans like SonarQube, and secure Docker images with signed artifacts.
