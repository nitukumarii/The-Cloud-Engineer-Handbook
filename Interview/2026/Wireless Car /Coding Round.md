# Daily KPI Pipeline and Statistical Anomaly Detection Engine

---

# Project Overview

Build a data pipeline that:

- Processes daily KPI batch logs from CSV files.
- Stores historical KPI data in PostgreSQL.
- Detects statistical anomalies using a 14-day rolling window.
- Produces a JSON report containing only newly detected anomalies.
- Supports idempotent re-runs without duplicate anomaly reporting.

---

# System Architecture

```
CSV Input
    │
    ▼
run_pipeline.sh
    │
    ▼
CSV Parser
    │
    ▼
PostgreSQL (readings)
    │
    ▼
Rolling Window Statistics
    │
    ▼
Z-Score Calculation
    │
    ▼
New Anomaly Detection
    │
    ▼
JSON Output (stdout)
```

---

# Entry Points

## Initialize Database

```bash
bash start.sh
```

Responsibilities:

- Wait for PostgreSQL availability.
- Create required tables.
- Create indexes.
- Create constraints.

---

## Execute Pipeline

```bash
bash run_pipeline.sh --input data.csv
```

Responsibilities:

- Read CSV.
- Store data.
- Detect anomalies.
- Print JSON report.

---

# PostgreSQL Configuration

| Property | Value |
|----------|-------|
| Host | db |
| Port | 5432 |
| Database | postgres |
| Username | postgres |
| Password | postgres |

Environment Variable:

```text
DATABASE_URL=postgresql://postgres:postgres@db:5432/postgres
```

---

# Input Specification

CSV Format

```csv
date,metric,region,value
2024-03-15,revenue,EU,10450.00
2024-03-15,revenue,US,88200.00
2024-03-15,signups,EU,312.00
2024-03-15,signups,US,1840.00
```

Rules

- Header always exists.
- One date per file.
- One row per `(metric, region)`.
- Values are numeric.

---

# Database Schema

## readings

| Column | Type |
|---------|------|
| date | DATE |
| metric | TEXT |
| region | TEXT |
| value | DOUBLE PRECISION |

Primary Key

```sql
(date, metric, region)
```

Equivalent SQL

```sql
CREATE TABLE readings (
    date DATE,
    metric TEXT,
    region TEXT,
    value DOUBLE PRECISION,
    PRIMARY KEY(date, metric, region)
);
```

---

# Statistical Processing

Performed independently for every:

```text
(metric, region)
```

---

# Rolling Window

Use only previous **14 calendar days**.

Current day's value is **excluded**.

Example

```
Today = 2024-03-15

Window

2024-03-01
...
2024-03-14
```

---

# Mean

Formula

```text
μ = Σx / n
```

---

# Population Standard Deviation

Formula

```text
σ = √( Σ(x−μ)² / n )
```

Population variance must divide by:

```text
n
```

NOT

```text
n-1
```

---

# Z-Score

Formula

```text
z = (value − μ) / σ
```

---

# Detection Rules

## Rule 1

History < 5 records

Result

```text
Skip anomaly detection
```

---

## Rule 2

Standard deviation

```text
σ = 0
```

Result

```text
Skip anomaly detection
```

---

## Rule 3

Flag anomaly when

```text
|z| > 2.5
```

Otherwise

```text
Normal reading
```

---

# Idempotency Rules

Pipeline must support re-execution safely.

Requirements

- Same CSV can be processed multiple times.
- No duplicate database rows.
- No duplicate anomaly reporting.
- Existing anomaly must never be emitted again.

---

# Output JSON

Exactly one JSON object must be written to:

```text
stdout
```

No debug logs.

---

# Output Schema

```json
{
  "processed_date": "YYYY-MM-DD",
  "rows_processed": 0,
  "anomalies": []
}
```

---

# Example Output

```json
{
  "processed_date": "2024-03-15",
  "rows_processed": 4,
  "anomalies": [
    {
      "metric": "revenue",
      "region": "EU",
      "date": "2024-03-15",
      "value": 10450.0,
      "zscore": -3.21
    }
  ]
}
```

---

# JSON Fields

## processed_date

- ISO date
- Format

```text
YYYY-MM-DD
```

---

## rows_processed

Total number of rows in CSV.

Example

```text
4
```

---

## anomalies

Array of newly detected anomalies only.

Each object contains

- metric
- region
- date
- value
- zscore

---

# Z-Score Formatting

Round to:

```text
2 decimal places
```

Example

```text
-3.21456

↓

-3.21
```

---

# Complete Processing Flow

```
Start Pipeline
      │
      ▼
Read CSV
      │
      ▼
Validate Input
      │
      ▼
Insert/Upsert into readings
      │
      ▼
For each (metric, region)
      │
      ▼
Fetch previous 14 days
      │
      ▼
History >= 5 ?
      │
 ┌────┴─────┐
 │          │
No         Yes
 │          │
Skip     Calculate Mean
            │
            ▼
Calculate Population Std Dev
            │
            ▼
σ == 0 ?
            │
     ┌──────┴──────┐
     │             │
    Yes           No
     │             │
   Skip      Calculate Z-score
                   │
                   ▼
             |z| > 2.5 ?
                   │
          ┌────────┴────────┐
          │                 │
         No                Yes
          │                 │
      Ignore         New anomaly?
                             │
                  ┌──────────┴─────────┐
                  │                    │
                 No                   Yes
                  │                    │
              Ignore          Save & Output
                  │
                  ▼
Generate JSON
                  │
                  ▼
Print to stdout
```
