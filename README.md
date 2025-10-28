### Public vs Private subnets

“Public subnets have internet access through an Internet Gateway — typically for web servers.
Private subnets don’t have direct internet access; they route outbound traffic through a NAT Gateway — typically for databases or internal services.”

### What is CloudFront and Elastic IP?

“CloudFront is AWS’s CDN that caches content globally for faster delivery and DDoS protection.
Elastic IP is a static public IP that stays attached even if you stop or restart an instance — useful for stable DNS mapping.”

### VPC Peering vs Direct Connect

“VPC Peering connects two VPCs over AWS’s internal network — low cost but not transitive.
Direct Connect provides a dedicated private link between on-prem and AWS — used for high bandwidth and low latency applications.”

### Explain Route53 routing policies

“Route53 supports multiple routing policies like:

Simple Routing (one endpoint),

Weighted Routing (traffic split),

Latency-based Routing,

Failover Routing,

Geolocation Routing for regional control.”

### How to monitor CPU, memory, and disk of 50+ EC2 instances with CloudWatch?

“For CPU, default CloudWatch metrics are enough.
For memory and disk, I install CloudWatch Agent to collect custom metrics.
Then I create dashboards and set up alarms for thresholds across multiple instances using metric filters or EC2 Auto Scaling groups.”

### Workaround if private key is lost and SSM is disabled

“If both SSH key and SSM are unavailable, I can:

Detach the root volume, attach it to another instance, and modify authorized_keys to insert a new key.
Then reattach it to the original instance.
This way I regain SSH access safely.”
