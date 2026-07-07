#  Interview Questions

1. How are you?
2. Is this your last interview for today?
3. How were the interviews?
4. Should I introduce myself?
5. How much experience do you have with containers, Kubernetes, Docker?
6. When you say containerization, was it again Kubernetes?
7. Which platform?
8. Which cloud platform or on-premises Kubernetes cluster?
9. What could be the possible causes of a pod continuously restarting with a "Back-off restarting failed container" error?
10. Do you have two screens in front of you or just one?
11. How will you check this error?
12. Which command will you run?
13. Can you explain the step-by-step process of pod creation?
14. How does the communication happen between different Kubernetes components during pod creation?
15. What parameters does the scheduler consider while selecting a node?
16. How does the scheduler know which node to select for a pod?
17. If the scheduler cannot place a pod because of taints and tolerations, will it result in a CrashLoopBackOff error or some other error?
18. If the image is not present in the registry, will the pod ever start?
19. If Kubelet cannot pull the image due to permission issues, will it result in a CrashLoopBackOff error?
20. If the container never starts, how will it restart?
21. Can you explain the different types of Kubernetes Services?
22. ClusterIP is used for pod-to-pod communication, right?
23. How will Nginx communicate with MySQL if both are running as multiple pods?
24. Will you use the Pod IP or the ClusterIP?
25. Why use ClusterIP instead of Pod IP?
26. What is the difference between NodePort and LoadBalancer services?
27. Why would you choose NodePort over LoadBalancer?
28. How can you check a Docker image for vulnerabilities and how would you fix them?
29. Can you tell me a few Docker image building best practices?
30. What is the difference between CMD and ENTRYPOINT?
31. How would you solve the issue where a user's shopping cart becomes empty after the container is terminated?
32. Can you explain static provisioning versus dynamic provisioning of volumes?
33. Have you heard of static and dynamic volume provisioning?
34. If you are managing multiple EKS clusters from your laptop, how does kubectl know which cluster to connect to?
35. How do you access an EKS cluster?
36. What information is stored in the kubeconfig file?
37. How can you switch from one Kubernetes cluster to another?
38. If an application behind an Ingress intermittently returns HTTP 503 errors, what could be the possible causes?
39. How would you troubleshoot intermittent HTTP 503 errors?
40. Which permissions would you check?
41. Would you check Kubernetes permissions, IAM permissions, or application permissions?
42. If a public user gets a 503 error, why would you check IAM permissions?
43. Walk me through a major problem you solved in your organization.
44. How did you become aware of the problem?
45. What information did you gather?
46. What information was missing?
47. How did you fill those gaps?
48. Did you perform a retrospective after the issue was resolved?
49. What did you learn from the incident?
50. Can you explain the architecture of that application?
51. Why was there an EC2 instance in the request path?
52. What did you see in the VPC Flow Logs that helped you identify the issue?
53. What was the error or event in the VPC Flow Logs?
54. If it was a security group issue, why was the application working intermittently instead of failing all the time?
55. Do you have any questions for me?
