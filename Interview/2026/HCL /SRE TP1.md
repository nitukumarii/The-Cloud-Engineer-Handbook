# Production Support / SRE Interview Questions

1. Suppose you have a Kubernetes-hosted application experiencing high latency. Which Linux commands would you use to identify the root cause?

2. Suppose you have a P1 incident and your pod is getting crashed. How would you investigate this? What would be your approach?

3. Any database-related experience — SQL or RDBMS, anything?

4. If you want to identify blocking processes in SQL, which kind of query would you use?

5. Whenever you're taking any production database backup, what precautions do you need to take before that?

6. Any programming language you have — have you done any kind of automation using this scripting?

7. Can you tell me about the last application you worked on at Mastercard — the flow, upstream, downstream, that kind of thing?

8. What was your major role in that?

9. What kind of issues did you face in certificate management? Any issue you can recall?

10. For monitoring, you've worked with Splunk, Dynatrace, CloudWatch, and Grafana — is that right?

11. Can you tell me how you can reduce alert conditions? Are you aware of the concept of alert fatigue?

12. In Splunk, you have concepts like search, stats, and eval — what's the difference between those?

13. What is `eval` in Splunk?

14. How would you identify the root cause of increased API latency using a Grafana dashboard?

15. Your dashboard shows healthy infrastructure, but customers report poor application performance. How would you investigate?

16. What's the difference between Change Management and Problem Management?

17. Are you aware of CVRT (Customer Visible Revenue Threatening) incidents?

18. A payment processing application is down for premium customers, but monitoring alerts haven't triggered. How would you classify and handle this incident?

19. How will you ensure recurring incidents are permanently resolved?

20. Can you explain an Error Budget? How much error budget is acceptable in an environment?

21. Are you aware of the concept of "toil" in Site Reliability Engineering (SRE)?

22. What SRE practices help reduce MTTR (Mean Time to Recovery)?

23. To improve reliability, which operational activities can you automate?

24. You've worked with CI/CD pipelines using Jenkins. Can you describe a major issue you faced and how you recovered from it?

25. A critical downstream service undergoes changes without prior notification, causing transaction failures. How would you manage this incident?

26. A payment request is received successfully, but the response from the third-party payment gateway is delayed. Is this an upstream or downstream issue? How would you investigate?

27. Do you have an understanding of Blue-Green and Canary deployment strategies? Can you briefly explain them?

28. Which AWS services have you used for observability and monitoring?

29. Suppose you need to troubleshoot a connectivity issue between an EC2 instance and an RDS database. What steps would you follow?

30. A card transaction is approved, but the merchant did not receive the funds. How would you investigate this issue?

31. Do you have any experience working with Mainframe systems?

32. Can you describe one of your major P1 production incidents and explain how you handled it?
