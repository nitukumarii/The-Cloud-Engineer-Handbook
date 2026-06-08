Scope: External access via node IP
Port range: 30000–32767
Use case: Simple way to expose an app outside the cluster
How it works: Opens a specific port on every node → forwards traffic to Pods

👉 Access using:
http://<NodeIP>:<NodePort>
