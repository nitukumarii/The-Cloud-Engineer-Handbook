1. How did you coordinate with developers and testers before and after a deployment?
Who gave the deployment go-ahead?
The deployment go-ahead was typically provided by the release manager or the designated product owner after the successful completion of automated tests, UAT sign-off, and the final review.
What was your communication channel—Jira, Slack, emails?
We primarily used Slack for real-time communication, Jira for tracking tasks and issues, and email for formal notifications about deployments, post-deployment reports, and status updates.
Did you follow a formal UAT sign-off?
Yes, we followed a formal UAT (User Acceptance Testing) sign-off process. Once all test cases were successfully completed and signed off by the QA and product teams, we proceeded with the deployment to production.
2. Did you follow a change management or CAB process before production deployments?
What documentation was required?
Yes, we followed the Change Advisory Board (CAB) process, which required detailed change requests, deployment plans, rollback strategies, and risk assessments. We also documented potential impacts and validation steps for each deployment.
Did you create or just update change tickets?
I was responsible for creating and updating change tickets, ensuring all relevant details (deployment schedule, steps, resources) were accurately captured and shared with the team.
3. What was your role in post-deployment validation?
Did you monitor logs? Check dashboards?
After deployment, my role was to monitor logs for any unusual behavior and check dashboards to track application performance, errors, and resource utilization.
Did you work with QA for sanity testing?
Yes, I collaborated closely with the QA team to conduct sanity testing post-deployment to ensure that the system was functioning as expected in production.
4. How did your team manage deployment timelines—daily, weekly, or release window-based?
Did you follow sprint release cycles?
We followed weekly release windows based on sprint cycles. At the end of each sprint, we had scheduled deployment windows for production releases.
What happened if a deployment failed outside of hours?
If a deployment failed outside of regular hours, we had a on-call support system in place to resolve critical issues. In non-critical cases, we would revert changes and investigate the failure during the next working window.
5. Were you involved in sprint planning or retrospectives? If yes, how?
Did you raise DevOps-related tasks in planning?
Yes, during sprint planning, I raised tasks related to CI/CD improvements, automation of manual deployment steps, and performance monitoring improvements.
How did you suggest improvements in retrospectives?
In retrospectives, I suggested improvements related to build pipeline efficiency, deployment automation, and better coordination with QA teams to streamline testing cycles.
6. How did you ensure that deployment or performance tasks didn’t become bottlenecks in the delivery cycle?
Did you track or monitor CI/CD metrics (like build duration, failure rate)?
Yes, I closely tracked CI/CD metrics, such as build duration, failure rates, and deployment time. This helped identify areas that were slowing down the process.
Did you proactively automate or parallelize steps?
Absolutely. I proactively automated manual tasks such as deployments and performance tests and parallelized steps where possible to speed up the process.
7. What documentation were you responsible for?
Did you maintain runbooks, onboarding docs, CI/CD flowcharts, or troubleshooting guides?
I was responsible for maintaining runbooks, CI/CD flowcharts, and troubleshooting guides for deployments, performance validation, and incident response.
8. How did you handle last-minute or ad-hoc deployment requests?
Were there policies for emergency releases?
Yes, there were predefined policies for emergency releases. We followed strict protocols and communication channels for emergency patches or hotfixes.
Did you create hotfix branches or short-cycle builds?
Yes, if a critical issue was identified, I would create hotfix branches and use short-cycle builds to quickly deploy fixes to production without waiting for the next regular release cycle.
9. How did you handle coordination across time zones if the team or client was global?
Did you hand off work or have staggered deployment windows?
Yes, when coordinating with global teams, we established staggered deployment windows to accommodate different time zones. I often had to hand off tasks and ensure that teams in other regions were fully prepared to handle post-deployment activities.
10. What was your escalation process when something went wrong in production?
Who was the first point of contact?
The first point of contact for any production issues was typically the on-call engineer or the lead engineer responsible for the deployment. If the issue was more complex, I would escalate it to the production support team.
Did you lead RCA calls or create incident reports?
Yes, I often led Root Cause Analysis (RCA) calls and created incident reports to identify the cause of failures and document the steps taken to resolve them.
11. Were you responsible for release notes?
How did you gather changelog inputs from developers?
Yes, I was responsible for release notes. I gathered changelog inputs from developers by reviewing commit messages, Jira tickets, and talking to them directly for any last-minute changes.
What format did you use to make it easy for business teams to understand?
I used a clear and concise format, typically bullet points, which highlighted new features, bug fixes, and critical changes in a way that business teams could easily digest.
12. What tools or methods did you use for tracking deployment readiness?
Jira, Confluence, Excel tracker?
We used Jira for tracking deployment readiness, Confluence for knowledge sharing, and an Excel tracker to track specific deployment tasks and timelines.
Did you use checklists before pushing to prod?
Yes, we followed a checklist to ensure all tasks were completed before pushing to production, including pre-deployment testing, code review sign-offs, and UAT completion.
13. How did you contribute to knowledge sharing within the team?
Did you run internal training or walkthroughs?
Yes, I ran regular internal training sessions and walkthroughs on CI/CD best practices and troubleshooting deployment issues.
Did you help onboard new team members?
Yes, I helped onboard new team members by providing them with documentation, conducting hands-on sessions, and guiding them through the CI/CD pipeline and deployment processes.
14. What did your daily stand-up update usually sound like?
Did you highlight blockers?
Yes, I highlighted any blockers such as issues in the build pipeline, deployment failures, or resources needed for performance testing.
How did you communicate delays or progress?
I provided clear updates on progress, such as deployments successfully completed or ongoing issues, and communicated delays if something was holding up the deployment.
15. What steps did you follow during a feature freeze or code freeze before a release?
How did you enforce it?


The PwC financial application was designed to support portfolio management for institutional investors, enabling real-time tracking of fund performance, asset allocation, and risk management. It facilitated client financial reporting, including customized investment reports, performance analytics, and tax-related documents. Additionally, it handled compliance validation by ensuring transactions adhered to financial regulations and internal policies. The application also incorporated automated report generation to streamline auditing processes and financial forecasting.

The backend was primarily built using Java with Spring Boot, leveraging microservices architecture to ensure scalability and maintainability. For the frontend, the application utilized Angular to provide a dynamic and responsive user interface. Additionally, the application integrated with Python-based data enrichment services for advanced analytics and processing of financial data, such as real-time market data feeds and historical performance analysis.
I helped enforce feature freezes by ensuring no code changes were made to the release branch, except for critical bug fixes. We also communicated this freeze across teams to ensure everyone was aligned.
What was your role during that buffer window?
During the buffer window, my role was to ensure all the necessary pre-production checks were completed and that no urgent deployments or changes would affect the release cycle.
