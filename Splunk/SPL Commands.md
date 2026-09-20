# Splunk SPL Commands — Production Practice

These are some of the most useful SPL commands for **production log analysis and troubleshooting**.

---

## 1. `stats`

### Definition

`stats` is used to **calculate and summarize data**.

It can count events, calculate averages, find maximum/minimum values, and group results by fields such as `host`, `source`, or `status`.

### Example

```spl
index=production "ERROR"
| stats count by host
```

### What it does

1. Searches for `ERROR` events in the `production` index.
2. Counts the number of matching events.
3. Groups the count by `host`.

### Example Result

| host          | count |
| ------------- | ----: |
| app-server-01 |   125 |
| app-server-02 |    78 |
| app-server-03 |   210 |

### Production Use

This can help identify **which server is generating the most errors** during an incident.

For example:

> "I used `stats count by host` to identify whether the errors were concentrated on a specific server."

---

# 2. `timechart`

### Definition

`timechart` is used to **visualize how events or metrics change over time**.

It automatically groups data into time intervals such as minutes, hours, or days.

### Example

```spl
index=production "ERROR"
| timechart count
```

### What it does

It counts `ERROR` events and shows the count over time.

### Example Result

| Time  | count |
| ----- | ----: |
| 10:00 |     5 |
| 10:05 |     8 |
| 10:10 |    12 |
| 10:15 |    85 |
| 10:20 |   140 |
| 10:25 |    18 |

Splunk can display this as a **time-series chart**.

### Production Use

This is useful for identifying **when an issue started and whether error volume increased suddenly**.

For example:

> "I use `timechart` to see whether the error rate increased at a specific point in time and correlate it with a deployment or infrastructure change."

---

# 3. `table`

### Definition

`table` is used to **display only the fields you are interested in**.

It makes the search results easier to read.

### Example

```spl
index=production
| table _time host source message
```

### What it does

Instead of displaying many fields, Splunk displays only:

* `_time`
* `host`
* `source`
* `message`

### Example Result

| _time    | host  | source          | message                    |
| -------- | ----- | --------------- | -------------------------- |
| 10:15:21 | app01 | application.log | Connection timeout         |
| 10:15:25 | app01 | application.log | Database connection failed |
| 10:16:03 | app02 | application.log | Request failed             |

### Production Use

Useful when investigating an incident and you only want to see the **important fields**.

For example:

> "I use `table` to reduce the search output and focus on fields such as timestamp, host, source, and message."

---

# 4. `rex`

### Definition

`rex` is used to **extract fields from unstructured text using a regular expression**.

This is especially useful when important information exists inside a log message but is not already available as a Splunk field.

### Example

```spl
index=production
| rex "transaction_id=(?<transaction_id>\S+)"
```

### Example Log

```text
2026-09-20 10:15:21 ERROR transaction_id=TXN12345 payment failed
```

The `rex` command extracts:

```text
transaction_id = TXN12345
```

### Example Result

| transaction_id |
| -------------- |
| TXN12345       |
| TXN12346       |
| TXN12347       |

### Production Use

This is useful when troubleshooting a **specific transaction/request**.

For example:

> "If the transaction ID is embedded inside the log message, I can use `rex` to extract it and then use that field to investigate the transaction across related logs."

### Important

The syntax:

```spl
(?<transaction_id>\S+)
```

means:

* `transaction_id` → name of the new field
* `\S+` → one or more non-space characters

---

# 5. `eval`

### Definition

`eval` is used to **create or calculate fields** using expressions.

It can perform mathematical calculations, string operations, conditional logic, and other transformations.

### Example

```spl
index=production
| eval duration_seconds=duration_ms/1000
```

### Example Input

Suppose the existing field is:

```text
duration_ms = 2500
```

The command calculates:

```text
duration_seconds = 2500 / 1000
```

### Example Result

| duration_ms | duration_seconds |
| ----------: | ---------------: |
|        2500 |              2.5 |
|        5000 |                5 |
|        1250 |             1.25 |

### Production Use

Useful when log data is stored in a format that is not convenient for analysis.

For example:

> "If application response time is stored in milliseconds, I can use `eval` to convert it to seconds for easier analysis."

---

# Production Practice Patterns

## Pattern 1 — Count Errors by Host

```spl
index=production "ERROR"
| stats count by host
```

### Question this answers

> Which servers are generating the most errors?

### Example Result

```text
app-server-01    125
app-server-02     78
app-server-03    210
```

---

## Pattern 2 — See Errors Over Time

```spl
index=production "ERROR"
| timechart count
```

### Question this answers

> When did the error volume increase?

### Example

```text
10:00 → 5 errors
10:05 → 8 errors
10:10 → 12 errors
10:15 → 85 errors
10:20 → 140 errors
```

This can help correlate the spike with:

* Deployment
* Configuration change
* Infrastructure issue
* Dependency failure
* Traffic increase

---

## Pattern 3 — Display Important Fields

```spl
index=production
| table _time host source message
```

### Question this answers

> What happened, when did it happen, and which server/source generated it?

### Example Result

```text
10:15:21 | app01 | application.log | Connection timeout
10:15:25 | app01 | application.log | Database connection failed
10:16:03 | app02 | application.log | Request failed
```

---

## Pattern 4 — Extract Transaction ID

```spl
index=production
| rex "transaction_id=(?<transaction_id>\S+)"
```

### Question this answers

> Can I extract the transaction ID from the raw log message?

### Example

Input:

```text
ERROR transaction_id=TXN12345 request failed
```

Output:

```text
transaction_id = TXN12345
```

You can then use the extracted field for further investigation.

For example:

```spl
index=production
| rex "transaction_id=(?<transaction_id>\S+)"
| search transaction_id="TXN12345"
```

---

## Pattern 5 — Convert Milliseconds to Seconds

```spl
index=production
| eval duration_seconds=duration_ms/1000
```

### Question this answers

> Can I convert the response time into a more readable unit?

### Example

```text
duration_ms = 3500
```

becomes:

```text
duration_seconds = 3.5
```

---

# Quick Interview Summary

| Command     | Purpose                      | Production Use                    |
| ----------- | ---------------------------- | --------------------------------- |
| `stats`     | Aggregate/summarize data     | Count errors by host              |
| `timechart` | Analyze data over time       | Find error spikes                 |
| `table`     | Display selected fields      | Focus on important fields         |
| `rex`       | Extract fields from raw text | Extract transaction/request IDs   |
| `eval`      | Create/calculate fields      | Convert units or calculate values |

## Easy Way to Remember

```text
stats     → summarize
timechart → trend over time
table     → show selected fields
rex       → extract data
eval      → calculate/create fields
```

## Production Troubleshooting Flow

A practical incident investigation might look like:

```text
Incident/Alert
      ↓
Identify time window
      ↓
Search correct index
      ↓
Find ERROR / Exception
      ↓
Use stats to identify affected hosts
      ↓
Use timechart to identify error spike
      ↓
Use rex to extract transaction/request ID
      ↓
Use table to focus on relevant fields
      ↓
Use eval if calculations are required
      ↓
Correlate with Dynatrace / deployment / infrastructure
      ↓
Identify probable cause
      ↓
Mitigate / restore service
      ↓
RCA
```

This is the level of SPL that is useful for **production support/SRE troubleshooting** without positioning yourself as a Splunk Administrator or Splunk Platform Engineer.
