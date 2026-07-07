How are you?
Is this your last interview for today?
How were the interviews?
Should I introduce myself?
How much experience do you have with containers, Kubernetes, Docker?
When you say containerization, was it again Kubernetes?
Which platform?
Which cloud platform or on-premises Kubernetes cluster?
What could be the possible causes of a pod continuously restarting with a "Back-off restarting failed container" error?
Do you have two screens in front of you or just one?
How will you check this error?
Which command will you run?
Can you explain the step-by-step process of pod creation?
How does the communication happen between different Kubernetes components during pod creation?
What parameters does the scheduler consider while selecting a node?
How does the scheduler know which node to select for a pod?
If the scheduler cannot place a pod because of taints and tolerations, will it result in a CrashLoopBackOff error or some other error?
If the image is not present in the registry, will the pod ever start?
If Kubelet cannot pull the image due to permission issues, will it result in a CrashLoopBackOff error?
If the container never starts, how will it restart?
Can you explain the different types of Kubernetes Services?
ClusterIP is used for pod-to-pod communication, right?
How will Nginx communicate with MySQL if both are running as multiple pods?
Will you use the Pod IP or the ClusterIP?
Why use ClusterIP instead of Pod IP?
What is the difference between NodePort and LoadBalancer services?
Why would you choose NodePort over LoadBalancer?
How can you check a Docker image for vulnerabilities and how would you fix them?
Can you tell me a few Docker image building best practices?
What is the difference between CMD and ENTRYPOINT?
How would you solve the issue where a user's shopping cart becomes empty after the container is terminated?
Can you explain static provisioning versus dynamic provisioning of volumes?
Have you heard of static and dynamic volume provisioning?
If you are managing multiple EKS clusters from your laptop, how does kubectl know which cluster to connect to?
How do you access an EKS cluster?
What information is stored in the kubeconfig file?
How can you switch from one Kubernetes cluster to another?
If an application behind an Ingress intermittently returns HTTP 503 errors, what could be the possible causes?
How would you troubleshoot intermittent HTTP 503 errors?
Which permissions would you check?
Would you check Kubernetes permissions, IAM permissions, or application permissions?
If a public user gets a 503 error, why would you check IAM permissions?
Walk me through a major problem you solved in your organization.
How did you become aware of the problem?
What information did you gather?
What information was missing?
How did you fill those gaps?
Did you perform a retrospective after the issue was resolved?
What did you learn from the incident?
Can you explain the architecture of that application?
Why was there an EC2 instance in the request path?
What did you see in the VPC Flow Logs that helped you identify the issue?
What was the error or event in the VPC Flow Logs?
If it was a security group issue, why was the application working intermittently instead of failing all the time?
Do you have any questions for me?
