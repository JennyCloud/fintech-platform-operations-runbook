# SQL Troubleshooting & Data Integrity Guide

In a Fintech environment, the database is the "Source of Truth." Troubleshooting must be performed with a "Read-Only" mindset to prevent accidental data corruption or locking.

## 1. Investigation Protocol (The Safe Approach)
* **Always use `WITH (NOLOCK)`:** Prevent blocking active transactions during investigations.
* **Verify before Modify:** Never run a `DELETE` or `UPDATE` without first running a `SELECT` to confirm the exact rows affected.
* **Transactions:** Wrap any data correction in a transaction (`BEGIN TRAN` ... `ROLLBACK`) until the results are verified.

## 2. Common Scenarios & Query Patterns

### A. Finding a "Missing" Record
Used when a user reports a record was submitted but isn't visible in the UI.

-- Search by unique identifier with no-lock
SELECT * FROM Applications WITH (NOLOCK)
WHERE ApplicationID = 'APP-12345' 
OR (CustomerName LIKE '%Smith%' AND CreatedDate > '2026-01-10');

### B. Checking for Database "Blocking"
Used when the application is slow or timing out.

-- Identify which session is blocking others
SELECT 
    blocking_session_id AS BlockingSessionID,
    session_id AS VictimSessionID,
    wait_type, 
    wait_time,
    last_wait_type
FROM sys.dm_exec_requests
WHERE blocking_session_id <> 0;

### C. Verifying "Ghost" Data (Audit Trail)
Used to see if a record was changed or deleted by a process.

-- Check Audit table for recent changes to a specific record
SELECT * FROM AuditLogs WITH (NOLOCK)
WHERE TableName = 'Applications' 
AND RecordID = 'APP-12345'
ORDER BY ChangeDate DESC;

## 3. Performance Metrics (Azure SQL)
DTU/CPU Utilization: If > 80%, investigate long-running queries or missing indexes.
Connection Pooling: Check if the application is failing to close connections, leading to "Pool Exhaustion."