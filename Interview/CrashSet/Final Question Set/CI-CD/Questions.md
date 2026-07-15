# 🚀 CI/CD Interview Questions (Non-Overlapping)

## CI/CD Fundamentals

1. What is CI/CD?

2. Explain the difference between Continuous Integration, Continuous Delivery, and Continuous Deployment.

3. What are the benefits of implementing CI/CD in an organization?

4. Explain the typical stages of a CI/CD pipeline.

5. Design an enterprise-level CI/CD pipeline.

6. What tools have you used for CI/CD?

7. Explain your experience with Jenkins/GitHub Actions.

8. What happens internally when a code change triggers a CI/CD pipeline?


---

# Jenkins

9. Explain Jenkins architecture.

10. What are Jenkins agents/slaves?

11. Controller vs Agent in Jenkins.

12. How do Jenkins agents communicate with the Jenkins controller?

13. What is a Jenkinsfile?

14. Declarative pipeline vs Scripted pipeline.

15. Explain Jenkins pipeline syntax.

16. What are Jenkins pipeline stages?

17. What are Jenkins shared libraries?

18. Why do we use Jenkins shared libraries?

19. How do you manage Jenkins plugins?

20. How do you upgrade Jenkins safely?

21. How do you secure Jenkins?

22. How do you manage Jenkins credentials?

23. How do you integrate Jenkins with Git repositories?

24. How do webhooks trigger Jenkins pipelines?

25. How do you troubleshoot Jenkins connectivity issues?


---

# GitHub Actions

26. Explain GitHub Actions architecture.

27. Workflow vs Job vs Step in GitHub Actions.

28. What is a GitHub Actions runner?

29. Self-hosted runner vs GitHub-hosted runner.

30. How do you secure GitHub Actions workflows?

31. How do you manage secrets in GitHub Actions?

32. How do you trigger GitHub Actions workflows?

33. GitHub Actions vs Jenkins.


---

# Git & Source Control Integration

34. Explain Git branching strategies used in CI/CD.

35. GitFlow vs Trunk-based development.

36. How do you handle merge conflicts in CI/CD?

37. How do you trigger builds based on branches?

38. How do you implement pull request validation?

39. How do you prevent broken code from reaching production?


---

# Build & Artifact Management

40. What happens during the build stage of a pipeline?

41. What is an artifact in CI/CD?

42. How do you manage build artifacts?

43. What artifact repositories have you used?

44. Nexus vs JFrog Artifactory.

45. How do you version application artifacts?

46. How do you promote artifacts from Dev → QA → Production?


---

# Deployment Strategies

47. Explain Rolling deployment.

48. Explain Recreate deployment.

49. Explain Immutable deployment.

50. When would you choose Blue-Green deployment?

51. When would you choose Canary deployment?

52. How do you implement deployment approvals?

53. How do you implement manual approval gates?

54. How do you implement automated quality gates?


---

# Kubernetes CI/CD Integration

55. How does CI/CD work with Kubernetes?

56. Explain a Jenkins + Docker + Kubernetes deployment workflow.

57. How does a pipeline deploy applications into EKS?

58. How do you manage Kubernetes manifests in CI/CD?

59. Helm-based deployment workflow.

60. Helm upgrade vs Kubernetes apply.

61. How do you manage Helm charts across environments?

62. How do you handle Kubernetes configuration changes through CI/CD?


---

# GitOps

63. What is GitOps?

64. GitOps vs traditional CI/CD.

65. Explain GitOps workflow.

66. Why is Git considered the source of truth in GitOps?

67. Explain Argo CD architecture.

68. How does Argo CD synchronize applications?

69. How does Argo CD detect drift?

70. Push-based vs Pull-based deployment model.

71. Argo CD vs Jenkins.


---

# Pipeline Security / DevSecOps

72. What security checks should be included in CI/CD pipelines?

73. Explain SAST, DAST, and SCA.

74. How do you integrate SonarQube into CI/CD?

75. How do you scan container images in pipelines?

76. How do you perform dependency vulnerability scanning?

77. How do you prevent secrets from being committed to Git?

78. How do you implement security gates in pipelines?


---

# CI/CD Monitoring & Optimization

79. How do you monitor CI/CD pipelines?

80. Which CI/CD metrics do you track?

81. How do you reduce pipeline execution time?

82. How do you optimize build performance?

83. How do you handle flaky tests?

84. How do you scale CI/CD pipelines for multiple teams?

85. How do you design a highly available CI/CD platform?


---

# CI/CD Troubleshooting

86. A Jenkins pipeline is stuck. How do you troubleshoot?

87. A build suddenly starts failing. What do you check?

88. Pipeline is successful but deployment is not happening. What do you investigate?

89. Build takes 2 hours suddenly. How do you troubleshoot?

90. Pipeline works in Dev but fails in Production. What would you check?

91. How do you troubleshoot dependency failures during builds?

92. How do you debug failed pipeline stages?


---

# Terraform + CI/CD

93. How do you integrate Terraform with CI/CD?

94. Explain Terraform workflow inside Jenkins.

95. How do you automate infrastructure deployment using pipelines?

96. How do you implement Terraform approval workflow?

97. How do you manage different environments using CI/CD and Terraform?


---

# Release Engineering

98. What is a release pipeline?

99. How do you manage application version releases?

100. How do you ensure deployment consistency across environments?

101. How do you implement zero-downtime deployments?

102. How do you coordinate application releases with multiple teams?
