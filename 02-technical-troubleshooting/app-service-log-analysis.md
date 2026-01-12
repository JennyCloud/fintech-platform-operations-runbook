# Azure App Service & Log Analysis Guide

This document covers the investigation of application-level failures, slow response times, and "5xx" server errors using Azure-native monitoring tools.

## 1. Application Insights: The "First Look"
When a failure is reported, use Application Insights to correlate the user's experience with the backend logs.
* **Failures Tab:** Look for "Top Exceptions" and "Dependency Failures" (e.g., the app cannot reach the SQL DB).
* **End-to-End Transaction Details:** Use the `Operation ID` to trace a single request through every service it touched.

## 2. KQL (Kusto Query Language)
Azure Log Analytics is the primary tool for deep-dive investigation.

### A. Find the Top 10 Most Frequent Exceptions
exceptions | where timestamp > ago(1h) | summarize count() by problemId | order by count_ desc | take 10

### B. Investigate a Specific User's Session
requests | where timestamp > ago(24h) | where client_IP == "IP_ADDRESS_HERE" | project timestamp, url, resultCode, duration | order by timestamp desc

### C. Identify Slow Dependencies (SQL or API Calls)
dependencies | where success == false or duration > 5000 | summarize count(), avg(duration) by name, target | order by avg(duration) desc

## 3. App Service Health Checks
* **Diagnose and Solve Problems:** Use this built-in Azure tool to check for "Memory Thrashing" (the memory leak pattern) or "TCP Socket Exhaustion."
* **Log Stream:** For real-time troubleshooting, use the Log Stream to see stdout and stderr logs as errors occur.

## 4. Performance "Anti-Patterns" to Watch For
* **The "Sawtooth" Pattern:** Steady memory growth followed by a crash/restart (Classic Memory Leak).
* **Dependency Timeout:** When a 3rd party API (like a credit check service) is down, causing the Inovatec app to hang.