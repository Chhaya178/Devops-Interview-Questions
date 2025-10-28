### Pod stuck in CrashLoopBackOff — how do you debug and fix it?

“First, I’d check the pod events using kubectl describe pod <pod-name> to see if there’s any error like OOMKilled, image pull failure, or probe failure. Then I’d look at the container logs using kubectl logs <pod-name> -p to find the reason for the crash.
If the issue is configuration related, like missing env variables or wrong image tag, I fix that in the Deployment manifest and redeploy.
Sometimes it’s due to resource limits or failed init containers — I check those too.
Once the root cause is fixed, I delete the bad pod so a new healthy one can start automatically.”

### How do you perform zero-downtime deployments in Kubernetes?

“To ensure zero downtime, I use the rolling update strategy that Kubernetes provides by default.
I make sure readiness probes are configured so traffic only goes to healthy pods.
I also keep maxUnavailable as 0 and maxSurge as 1 to ensure a new pod is ready before the old one terminates.
For safer deployments, I sometimes use canary or blue-green strategies using Argo Rollouts or service mesh tools like Istio.”

### Your service is not accessible externally — how do you troubleshoot?

“I’ll start by checking the service type using kubectl get svc.
If it’s ClusterIP, it’s internal only — I’ll change it to LoadBalancer or set up an Ingress for external access.
Next, I’ll check endpoints using kubectl get endpoints <service> to confirm pods are linked to the service.
If pods aren’t showing up, there might be a label mismatch.
Then I’ll verify if network policies or firewalls are blocking traffic.
Finally, I’ll test access using curl inside the cluster or through the LoadBalancer IP.”

### How do you handle a failed rollout during a deployment?

“If a deployment fails, I’ll check its rollout status with kubectl rollout status.
If I see pods failing readiness or image pull errors, I’ll inspect the logs and events.
To restore service quickly, I’ll roll back to the last stable version using kubectl rollout undo deployment/<name>.
Then I’ll identify the root cause — maybe it was a bad image, wrong config, or probe failure.
To prevent this in future, I’d implement canary or progressive rollouts.”

### How do you optimize resource requests and limits?

“In production, I monitor actual CPU and memory usage using metrics-server or Prometheus.
Based on average and peak usage, I set requests as the average and limits as around 1.5x of that.
This helps prevent throttling or OOM errors.
I also use Vertical Pod Autoscaler for recommendations and apply ResourceQuotas or LimitRanges per namespace to avoid resource hogging.”

### How do you secure secrets in Kubernetes?

“I always store sensitive data in Kubernetes Secrets instead of config maps or env files.
Then, I enable encryption at rest on the API server.
For better security, I integrate with external secret managers like AWS Secrets Manager or HashiCorp Vault.
I also make sure access is controlled through RBAC so only the right service accounts can access those secrets.”

### A node went down suddenly — what happens to pods running on it?

“If a node fails, the control plane marks it as NotReady after a short grace period.
Then, the pods running on that node are automatically rescheduled on healthy nodes, provided they’re part of a ReplicaSet or Deployment.
However, if the pod was using local storage or not managed by a controller, it won’t be recreated automatically.”

### How do you handle database credential rotation in Kubernetes?

“Database credentials are usually stored in Secrets.
When they’re updated, I either manually update the Secret or automate it using an external secrets manager.
Then I trigger a deployment restart using kubectl rollout restart, so the pods reload the new credentials.
For production systems, I prefer using Vault or External Secrets Operator to rotate credentials automatically.”

### What’s your strategy for backup and restore in a cluster?

“I take regular etcd snapshots because they store the entire cluster state.
For workloads and persistent volumes, I use Velero to back up resources and data to cloud storage like S3.
Backups are scheduled using CronJobs, and I also perform test restores regularly to ensure data integrity.”

### How do you implement auto-scaling when traffic fluctuates heavily?

“I use Horizontal Pod Autoscaler to scale pods based on CPU, memory, or custom metrics.
For node-level scaling, I use Cluster Autoscaler so new nodes are added automatically when needed.
In some cases, I integrate Prometheus Adapter to scale on business metrics like request rate or latency.
This setup ensures the system scales up during peak traffic and scales down when it’s idle, saving costs.”
