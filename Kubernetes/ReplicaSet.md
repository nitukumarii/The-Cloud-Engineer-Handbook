# ❓ Kubernetes Interview Question: ReplicaSet & Pod Scheduling

## Question
If a pod fails on a node (for example, Node1), will the ReplicaSet create the new pod on the same node or a different node?

## Answer
ReplicaSet does not decide on which node the pod will run. Its responsibility is only to ensure that the desired number of pod replicas are always running. When a pod fails, the ReplicaSet creates a new pod to maintain the desired state. The actual decision of where the new pod will run is handled by the Kubernetes scheduler. The scheduler evaluates factors such as node availability, resource capacity (CPU and memory), node health, taints and tolerations, and any scheduling constraints like node selectors or affinity rules. Based on these conditions, the new pod may be scheduled on the same node if it is healthy and has sufficient resources, or on a different node if the original node is unavailable, under resource pressure, or restricted by scheduling rules. This clearly separates responsibilities where ReplicaSet handles reconciliation and the scheduler handles placement decisions.
