
### Identify blocking processes in SQL

"If I suspect a database issue, I first confirm the application impact through monitoring and logs. Then I check for long-running or blocking queries using the 
database's monitoring views or commands—for example, SHOW PROCESSLIST in MySQL or pg_stat_activity in PostgreSQL. If I identify a blocking session, I
coordinate with the DBA team to investigate or terminate it if required. After that, I verify that application transactions are processing normally."
