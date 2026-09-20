# Splunk Production Support — Interview Notes

## 1. What is Splunk?

Splunk is a platform used for collecting, indexing, searching, monitoring, and analyzing machine-generated data such as application logs, system logs, events, and other operational data.

In production support, Splunk can be used to:

* Search application logs
* Investigate production incidents
* Identify when an issue started
* Search for errors and exceptions
* Correlate events using timestamps and transaction/request IDs
* Identify affected hosts or services
* Analyze recurring errors
* Monitor application behavior
* Create dashboards, reports, and alerts

### Production usage example

During a production incident, I have primarily used Splunk to trace application logs and events, correlate them based on timestamps and transaction or request identifiers, identify when the issue started and which services were affected, and then use Dynatrace and other monitoring data to narrow down the root cause.

---

# 2. Splunk Search

### What is a Splunk Search?

A Splunk search is a query that we enter in the Splunk search bar to retrieve specific events or log data.

We can filter the results using:

* Index
* Keywords
* Fields
* Host
* Source
* Sourcetype
* Timestamp
* Conditions

### Example

```spl
index=production "ERROR"
```

This searches for events containing `ERROR` in the `production` index.

Another example:

```spl
index=production host="server01" "ERROR"
```

This searches for ERROR events from a specific host.

---

# 3. Splunk Dashboard

### What is a Splunk Dashboard?

A Splunk dashboard is a visual representation of data collected in Splunk.

It can contain:

* Charts
* Tables
* Graphs
* Metrics
* Event panels
* Search results

Dashboards can be used to monitor:

* Application health
* Error trends
* Traffic
* Events
* Performance
* Availability
* Operational metrics

### Interview Answer

> A Splunk dashboard is a visual representation of data collected in Splunk. It can contain panels, charts, tables, and graphs that help us monitor application health, errors, events, and trends. In production, we can use dashboards to quickly identify abnormalities and investigate incidents.

---

# 4. Splunk Alert

### What is a Splunk Alert?

A Splunk alert is a notification that is triggered when a predefined search condition is met.

For example:

If the number of ERROR events crosses a defined threshold, Splunk can trigger an alert and notify the support team.

### Example scenario

```text
More than 100 errors within 5 minutes
            ↓
      Splunk Search
            ↓
    Threshold reached
            ↓
        Alert
            ↓
   Support team notified
```

### Interview Answer

> A Splunk alert is triggered when a predefined search condition or threshold is met. For example, if the number of application errors crosses a certain threshold within a defined period, an alert can be generated and the support team can be notified.

---

# 5. Splunk Report

### What is a Splunk Report?

A Splunk report is a saved search that can be run on demand or on a schedule.

It can be used for:

* Daily operational reporting
* Error summaries
* Incident analysis
* Trend analysis
* Management reporting

The results can be viewed in Splunk and, depending on the configuration, exported into formats such as CSV.

### Interview Answer

> A Splunk report is a saved search that can be executed on demand or on a scheduled basis. It provides specific information from Splunk and the results can be viewed or exported, for example as CSV, for further analysis or reporting.

---

# 6. What is a Splunk Index?

### Definition

A Splunk index is a repository where Splunk stores and organizes indexed data.

Data can be routed into different indexes based on factors such as:

* Application
* Environment
* Data type
* Business function
* Operational requirements

Specifying the index in a search helps narrow down the data that Splunk needs to search.

### Example

```spl
index=production
```

This searches data stored in the `production` index.

### Important

An index is **not simply a tag**.

If an organization has an index called `production`, then `production` is the name of that index.

### Interview Answer

> A Splunk index is a repository where Splunk stores and organizes indexed data. Different types of application or operational data can be routed into different indexes. When searching, specifying the index helps narrow down the data that Splunk needs to search.

---

# 7. Source vs Sourcetype vs Host

These three terms are frequently asked in Splunk interviews.

## Host

Identifies the machine or system from which the data originated.

### Example

```text
host = server01
```

Think:

> **Which machine?**

---

## Source

Identifies where the data came from, such as a particular log file, directory, or input.

### Example

```text
source = /var/log/application.log
```

Think:

> **Where did the data come from?**

---

## Sourcetype

Identifies the format or type of data being indexed.

It helps Splunk categorize and process the incoming data appropriately.

### Example

```text
sourcetype = application_log
```

Think:

> **What type of data is it?**

---

## Easy way to remember

```text
Host       → Which machine?
Source     → Where did the data come from?
Sourcetype → What type of data is it?
```

### Interview Answer

> Host identifies the machine from which the data originated. Source identifies where the data came from, such as a log file or input. Sourcetype identifies the type or format of the data and helps Splunk categorize and process it.

---

# 8. How do you search logs for a particular application?

First identify the appropriate:

* Index
* Application
* Host
* Source
* Sourcetype
* Time range

Then add application-specific keywords or fields.

### Example

```spl
index=production application="ngft"
```

You can add additional conditions depending on the issue.

For example:

```spl
index=production application="ngft" "ERROR"
```

### Interview Answer

> I would first identify the appropriate index and then filter the search using application-specific fields, keywords, source, host, or sourcetype. I would also select the relevant time range. If required, I can use the pipe operator to further filter or analyze the results.

---

# 9. How do you search logs within a particular time range?

Splunk provides a time picker where we can select a predefined or custom time range.

During production troubleshooting, the time range should be based on the incident timeline.

### Approach

```text
Incident reported
       ↓
Identify approximate timestamp
       ↓
Select time range around the incident
       ↓
Search logs/events
       ↓
Expand time range if required
       ↓
Identify when the issue actually started
```

### Interview Answer

> I select the appropriate time range based on the incident timeline. I normally start around the time the issue was reported and expand the window if required. I correlate timestamps of errors, alerts, deployments, and other events to determine when the issue actually started.

---

# 10. How do you search for ERROR, WARN, or Exception messages?

### ERROR

```spl
index=production "ERROR"
```

### WARN

```spl
index=production "WARN"
```

### Exception

```spl
index=production "Exception"
```

### Multiple keywords

```spl
index=production ("ERROR" OR "WARN" OR "Exception")
```

### Interview Answer

> I would specify the relevant index and search for keywords such as ERROR, WARN, Exception, or a specific error message. I would also set the appropriate time range and, if required, filter the results by host, source, application, or other fields.

---

# 11. How do you filter logs based on multiple conditions?

We can use:

* Fields
* Boolean operators
* Keywords
* Pipe operator

### Example

```spl
index=production host="server01" "ERROR"
```

### Using OR

```spl
index=production ("ERROR" OR "Exception") host="server01"
```

### Using pipe

```spl
index=production "ERROR"
| search host="server01"
```

### Interview Answer

> I can filter logs using multiple conditions such as index, host, source, application, keywords, and timestamps. I can use Boolean operators such as AND and OR, and the pipe operator to pass search results to another command for additional filtering or analysis.

---

# 12. What is the Pipe `|` in Splunk?

The pipe operator passes the output of one search command to another command.

### Example

```spl
index=production "ERROR"
| stats count by host
```

The first part searches for ERROR events.

The `stats` command then analyzes those results and gives the error count by host.

### Easy explanation

```text
Search data
    ↓
Filter/transform data
    ↓
Analyze results
```

---

# 13. How do you extract useful fields from unstructured logs?

If the information is not already available as a field, Splunk provides commands such as `rex` to extract values from raw log messages.

### Example log

```text
transaction_id=TX12345 status=FAILED
```

### Extract transaction ID

```spl
index=production
| rex "transaction_id=(?<transaction_id>\S+)"
```

This creates a field called:

```text
transaction_id
```

which contains:

```text
TX12345
```

### Interview Answer

> If the required information is not already available as a field, I can extract it from unstructured logs using Splunk commands such as `rex`. For example, I can extract a transaction ID, error code, or another value from the raw log message and then use that field for further filtering or analysis.

---

# 14. Important Splunk Commands

For production-support interviews, understand the purpose of these commands:

| Command     | Purpose                                  |
| ----------- | ---------------------------------------- |
| `search`    | Filter search results                    |
| `stats`     | Calculate statistics                     |
| `timechart` | Analyze values over time                 |
| `table`     | Display selected fields                  |
| `fields`    | Include/exclude fields                   |
| `sort`      | Sort results                             |
| `dedup`     | Remove duplicate results                 |
| `rex`       | Extract fields using regular expressions |
| `eval`      | Create or calculate fields               |
| `where`     | Filter based on expressions              |
| `top`       | Find most common values                  |
| `rare`      | Find least common values                 |

---

# 15. Useful Production Search Examples

## Search errors

```spl
index=production "ERROR"
```

## Search errors on a specific host

```spl
index=production host="server01" "ERROR"
```

## Count errors by host

```spl
index=production "ERROR"
| stats count by host
```

## Error trend over time

```spl
index=production "ERROR"
| timechart count
```

## Search application errors

```spl
index=production application="ngft" "ERROR"
```

## Search for multiple error types

```spl
index=production ("ERROR" OR "Exception" OR "failed")
```

## Find top error messages

```spl
index=production "ERROR"
| top limit=10 error_message
```

---

# 16. How would you investigate a production incident using Splunk?

This is one of the most important questions.

### Approach

```text
Incident reported
       ↓
Understand business/technical impact
       ↓
Identify affected application/service
       ↓
Identify approximate incident timestamp
       ↓
Select appropriate Splunk index
       ↓
Search application logs
       ↓
Search ERROR / Exception / timeout messages
       ↓
Use transaction/request ID if available
       ↓
Check surrounding events
       ↓
Identify affected host/service
       ↓
Correlate with deployment/change timeline
       ↓
Use Dynatrace/other monitoring data
       ↓
Identify probable root cause
       ↓
Mitigate / restore service
       ↓
RCA / Problem Management if required
```

### Interview Answer

> During a production incident, I first understand the impact and identify the affected application or service. I then determine the approximate time when the issue started and search the relevant Splunk index within that time range. I look for errors, exceptions, timeouts, and other abnormal events and use transaction or request IDs where available to trace the issue. I correlate the logs with deployment, infrastructure, and monitoring information and use Dynatrace where required to narrow down the root cause and support service restoration.

---

# 17. How do you investigate HTTP 500 errors?

### Approach

1. Identify affected application/service.
2. Identify when 500 errors started.
3. Search Splunk for HTTP 500.
4. Search for related exceptions.
5. Check transaction/request ID.
6. Check affected host.
7. Look at surrounding logs.
8. Check whether a deployment/change occurred.
9. Use Dynatrace to investigate service/dependency behavior.
10. Determine mitigation or rollback if required.

### Example

```spl
index=production "500"
```

More specifically, depending on the log structure:

```spl
index=production status=500
```

---

# 18. How do you investigate application latency?

Use both Splunk and Dynatrace.

### Dynatrace

Check:

* Response time
* Failure rate
* Throughput
* Affected service
* Dependencies
* Distributed traces/PurePaths
* Database calls
* External APIs

### Splunk

Check:

* Application logs
* Timeout messages
* Exceptions
* Request/transaction IDs
* Deployment timestamps
* Infrastructure/application events

### Interview Answer

> I would first confirm when the latency started and whether it affects all requests or a specific endpoint. In Dynatrace, I would check response time, failure rate, throughput, service dependencies, and traces to identify where the latency is being introduced. In Splunk, I would correlate the same time period with application logs and look for timeouts, exceptions, or other errors.

---

# 19. How do you investigate intermittent failures?

Intermittent issues require correlation rather than looking at a single error.

### Approach

```text
Identify affected transactions
        ↓
Find timestamps
        ↓
Search transaction/request IDs
        ↓
Compare successful vs failed requests
        ↓
Check affected hosts
        ↓
Check application/dependency behavior
        ↓
Check deployment/change timeline
        ↓
Look for patterns
```

Useful questions:

* Does it happen on one host or multiple hosts?
* Is it one endpoint?
* Is it a specific transaction type?
* Does it happen during a specific time?
* Is one downstream dependency involved?
* Did a deployment happen before the issue?

---

# 20. How do you investigate a failed transaction?

For a production file-transfer/application transaction:

### Step 1 — Identify transaction

```text
Transaction ID
```

### Step 2 — Search Splunk

```spl
index=production "TX12345"
```

### Step 3 — Check surrounding logs

Look for:

* Started
* Processing
* Completed
* Failed
* Timeout
* Exception
* Connection failure

### Step 4 — Correlate with Dynatrace

Check:

* Service
* Response time
* Failure rate
* Dependencies
* Trace/PurePath
* Database/API calls

### Step 5 — Determine impact

Check whether:

* One transaction is affected
* Multiple transactions are affected
* One partner is affected
* One application is affected
* Multiple services are affected

---

# 21. Splunk + Dynatrace Together

This is particularly important for production-support/SRE interviews.

## Scenario: Application latency increased

### Dynatrace

```text
Confirm latency increase
        ↓
Identify affected service
        ↓
Check response time
        ↓
Check failure rate
        ↓
Check throughput
        ↓
Check dependencies
        ↓
Inspect traces/PurePaths
```

### Splunk

```text
Search same time period
        ↓
Search application logs
        ↓
Search ERROR/Exception/timeout
        ↓
Search transaction/request ID
        ↓
Check affected hosts
        ↓
Correlate with deployment/change
```

---

# 22. Splunk vs Dynatrace

| Splunk                           | Dynatrace                                   |
| -------------------------------- | ------------------------------------------- |
| Strong log analysis              | Strong APM/observability                    |
| Search application logs          | Application/service monitoring              |
| Search events                    | Distributed tracing                         |
| Investigate errors/exceptions    | Analyze response time                       |
| Search transaction IDs           | Follow transactions across services         |
| Log correlation                  | Dependency analysis                         |
| Dashboards/reports/alerts        | Service/application dashboards              |
| Useful for detailed log evidence | Useful for application performance analysis |

### Important

They can complement each other.

A production investigation may look like:

```text
Alert
  ↓
Dynatrace identifies affected service
  ↓
Check response time / failure rate
  ↓
Open trace/PurePath
  ↓
Identify suspicious component
  ↓
Splunk search using timestamp + transaction ID
  ↓
Find exact application error
  ↓
Correlate with deployment/change
  ↓
Mitigate and restore service
```

---

# 23. Most Important Splunk Interview Questions

Prepare these first:

1. What is Splunk?
2. How have you used Splunk in production?
3. What is a Splunk index?
4. What are source, sourcetype, and host?
5. What is a Splunk search?
6. What is a dashboard?
7. What is an alert?
8. What is a report?
9. How do you search application logs?
10. How do you search within a specific time range?
11. How do you search ERROR and Exception messages?
12. How do you filter using multiple conditions?
13. What is the pipe operator?
14. What is `stats`?
15. What is `timechart`?
16. What is `rex`?
17. How do you extract fields from logs?
18. How do you investigate HTTP 500 errors?
19. How do you investigate application latency?
20. How do you investigate intermittent failures?
21. How do you investigate a failed transaction?
22. How do you correlate logs with a transaction ID?
23. How do you identify when an issue started?
24. How do you identify affected services?
25. How do you determine whether an issue was caused by a deployment?
26. What do you do if Splunk has no logs for the affected transaction?
27. How do you use Splunk and Dynatrace together?
28. Tell me about a production incident you investigated using Splunk.

---

# 24. Best Production-Support Answer Pattern

For scenario questions, use this structure:

```text
1. Confirm the issue
2. Understand impact
3. Identify affected service/application
4. Establish timeline
5. Search logs
6. Correlate transaction/request IDs
7. Check errors/exceptions
8. Check dependencies
9. Check recent changes/deployments
10. Use Dynatrace/other monitoring data
11. Mitigate and restore service
12. Perform RCA if required
```

### Example interview answer

> If an application starts failing in production, I would first confirm the impact and identify the affected service. I would establish when the issue started and search the relevant Splunk index around that timeframe. I would look for errors, exceptions, timeouts, and transaction or request IDs and correlate the events across the affected hosts. I would then use Dynatrace to check application performance, dependencies, and traces. I would also check for recent deployments or changes. Based on the findings, I would work with the relevant team on mitigation or rollback, restore the service, and then support RCA and preventive actions if required.

---

# 25. Quick Memory Sheet

```text
INDEX
→ Where Splunk stores/organizes indexed data

HOST
→ Which machine generated the data?

SOURCE
→ Where did the data come from?

SOURCETYPE
→ What type/format of data is it?

SEARCH
→ Query to retrieve/filter events

DASHBOARD
→ Visual representation of data

ALERT
→ Notification triggered by a search condition

REPORT
→ Saved/scheduled search for reporting

PIPE |
→ Pass output to another command

STATS
→ Calculate statistics

TIMECHART
→ Analyze data over time

REX
→ Extract fields from raw text

TRANSACTION ID
→ Trace a specific transaction through logs

TIMESTAMP
→ Establish when an event/issue occurred
```

# 26. Key Point for Senior Production Interviews

Don't focus only on remembering SPL syntax.

The interviewer is usually trying to understand whether you can **troubleshoot a production issue systematically**.

The important chain is:

```text
ALERT
  ↓
IMPACT
  ↓
TIMELINE
  ↓
AFFECTED SERVICE
  ↓
SPLUNK LOGS
  ↓
ERROR / EXCEPTION
  ↓
TRANSACTION / REQUEST ID
  ↓
DYNATRACE TRACE
  ↓
DEPENDENCY
  ↓
RECENT CHANGE
  ↓
MITIGATION
  ↓
SERVICE RESTORATION
  ↓
RCA / PROBLEM MANAGEMENT
```

This demonstrates **production troubleshooting and SRE thinking**, rather than simply knowing how to search Splunk.
