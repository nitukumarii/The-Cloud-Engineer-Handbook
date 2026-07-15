# ☸️ Kubernetes Interview Questions

## Kubernetes Fundamentals

1. What experience do you have with containers, Kubernetes, and Docker?

2. When you say containerization, was it Kubernetes?

3. Which Kubernetes platform have you worked with?

4. Which cloud platform or on-premises Kubernetes cluster have you used?

5. Explain Kubernetes architecture.

6. Explain Kubernetes control plane components.

7. Explain the role of API Server, Scheduler, Controller Manager, and etcd.

8. What happens internally when a Kubernetes object is created?


---

# Kubernetes Pod Management

9. A Kubernetes pod is continuously restarting. How do you troubleshoot it?

10. What could be the possible causes of a pod continuously restarting with a "Back-off restarting failed container" error?

11. How will you check a Kubernetes pod error?

12. Which commands will you run to troubleshoot pod failures?

13. If the image is not present in the registry, will the pod ever start?

14. If Kubelet cannot pull the image due to permission issues, will it result in CrashLoopBackOff?

15. If the container never starts, how will it restart?

16. What is CrashLoopBackOff?

17. Difference between ImagePullBackOff and CrashLoopBackOff.

18. How do you troubleshoot Kubernetes pod failures?


---

# Pod Creation Workflow

19. Explain the step-by-step process of pod creation.

20. How does communication happen between Kubernetes components during pod creation?

21. How does the scheduler know which node to select for a pod?

22. What parameters does the scheduler consider while selecting a node?

23. If the scheduler cannot place a pod because of taints and tolerations, will it result in CrashLoopBackOff or another error?


---

# Kubernetes Scheduler

24. Explain Kubernetes scheduler.

25. How does Kubernetes scheduler select nodes?

26. What are node selectors?

27. What are node affinity and pod affinity?

28. What are taints and tolerations?


---

# Kubernetes Services & Networking

29. Explain different types of Kubernetes Services.

30. ClusterIP is used for pod-to-pod communication, right?

31. How will Nginx communicate with MySQL if both are running as multiple pods?

32. Will you use Pod IP or ClusterIP?

33. Why use ClusterIP instead of Pod IP?

34. Difference between NodePort and LoadBalancer services.

35. Why would you choose NodePort over LoadBalancer?

36. How does service discovery work in Kubernetes?

37. How do pods communicate with each other?


---

# Kubernetes Storage

38. Explain static provisioning versus dynamic provisioning of volumes.

39. Have you heard of static and dynamic volume provisioning?

40. What are Persistent Volumes (PV)?

41. What are Persistent Volume Claims (PVC)?

42. How does Kubernetes handle persistent storage?

43. How do you manage application data when containers restart?


---

# Kubernetes Access & Configuration

44. If you are managing multiple EKS clusters from your laptop, how does kubectl know which cluster to connect to?

45. How do you access an EKS cluster?

46. What information is stored in the kubeconfig file?

47. How can you switch from one Kubernetes cluster to another?

48. Explain kubectl context.


---

# Kubernetes Ingress

49. If an application behind an Ingress intermittently returns HTTP 503 errors, what could be the possible causes?

50. How would you troubleshoot intermittent HTTP 503 errors?

51. What components would you check when troubleshooting Ingress issues?

52. How does Kubernetes Ingress work?


---

# Kubernetes Deployment Strategies

53. How do you perform rolling updates in Kubernetes?

54. How do you rollback a Kubernetes deployment?

55. Explain Kubernetes deployment strategy.

56. Canary deployment in Kubernetes.

57. Blue-Green deployment in Kubernetes.


---

# Kubernetes Docker Integration

58. Explain a Jenkins + Docker + Kubernetes deployment workflow.

59. How does a pipeline deploy applications into EKS?

60. How do you build and deploy Docker images to Kubernetes?

61. How do you push Docker images to a container registry?

62. How do Kubernetes nodes pull container images?


---

# Kubernetes Security

63. Which permissions would you check during Kubernetes issues?

64. Would you check Kubernetes permissions, IAM permissions, or application permissions?

65. How do you secure Kubernetes clusters?

66. Explain Kubernetes RBAC.

67. How do you manage secrets in Kubernetes?

68. How do you scan Kubernetes workloads for vulnerabilities?


---

# Kubernetes EKS

69. How do you access an EKS cluster?

70. Explain EKS architecture.

71. What AWS components are involved with EKS?

72. How does EKS networking work?

73. How do pods communicate with AWS services in EKS?

74. How do you troubleshoot EKS issues?


---

# Kubernetes Troubleshooting Scenarios

75. Pod is stuck in Pending state. How do you troubleshoot?

76. Pod is in CrashLoopBackOff. How do you troubleshoot?

77. Pod is running but application is not reachable. What do you check?

78. Service is not routing traffic to pods. What do you check?

79. Kubernetes node is NotReady. How do you troubleshoot?

80. Application returns HTTP 503 from Kubernetes Ingress. How do you troubleshoot?

81. Container is consuming excessive CPU/memory. How do you investigate?

82. Deployment rollout is stuck. What steps do you follow?


---

# Kubernetes Commands

83. Which kubectl commands do you use for troubleshooting?

84. How do you check pod logs?

85. How do you describe a Kubernetes resource?

86. How do you check pod events?

87. How do you check node status?

88. How do you check resource utilization in Kubernetes?

89. How do you debug a running container?
