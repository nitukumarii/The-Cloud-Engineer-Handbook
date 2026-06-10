🔹 What is a Namespace in Kubernetes?

A namespace in Kubernetes is a way to logically divide a cluster into multiple virtual clusters.

It helps organize resources (pods, services, deployments)
Allows multiple teams/projects to share the same cluster safely
Prevents naming conflicts (same resource name can exist in different namespaces)

👉 In short: “Namespace = a folder to organize and isolate resources inside a Kubernetes cluster.”

🔹 3 Default Namespaces Created by Kubernetes
1. default
Used when you don’t specify any namespace
All your basic workloads go here by default

👉 “General-purpose workspace”

🔹 kube-system
This namespace is for core Kubernetes components.
It contains things like:
DNS (CoreDNS)
kube-proxy
network plugins
control plane add-ons
Purpose: Keep system workloads separate from user workloads so you don’t accidentally modify or delete critical services.

👉 In short: “Internal brain of Kubernetes runs here.”

🔹 kube-public
This namespace is readable by all users (even unauthenticated).
Used for public cluster information, like:
cluster configuration data (ConfigMaps like cluster-info)
Purpose: Expose non-sensitive info to anyone who needs basic cluster access

👉 In short: “Public notice board of the cluster.”
