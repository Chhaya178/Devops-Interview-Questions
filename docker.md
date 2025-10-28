1. Volumes vs Bind Mounts

“Volumes are managed by Docker and stored in Docker’s path — best for production.
Bind mounts map a host path into the container — used for local development when we want real-time file sync.”

2. What are Cgroups and dangling objects?

“Cgroups (control groups) are a Linux kernel feature that Docker uses to limit CPU, memory, and I/O for containers.
Dangling objects are unused images, containers, or volumes that take up space — for example, untagged images left after rebuilds.”

3. Techniques to cache Docker layers in pipelines

“I keep frequently changing steps like COPY . and RUN npm install at the bottom of the Dockerfile, and static steps like dependency installation on top.
Also, I use build cache options like --cache-from in CI pipelines to reuse previously built layers.”

4. How to delete all Docker resources in one command

“You can use:

''' docker system prune -a --volumes '''


That removes all stopped containers, unused networks, dangling images, and volumes.”
