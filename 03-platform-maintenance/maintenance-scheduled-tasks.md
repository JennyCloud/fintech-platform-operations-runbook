# Maintenance & Scheduled Tasks

This document covers the management of routine background operations, automated jobs, and lifecycle maintenance (Certificates/Secrets).

## 1. Automated Batch Jobs (Azure WebJobs / Functions)
Fintech platforms often use background jobs for end-of-day reporting or bulk interest calculations.
* **Monitoring:** Check the "WebJobs" dashboard in the Azure Portal for "Failed" or "Aborted" statuses.
* **Investigation:** If a job fails, check for **SQL Timeouts**. Large batch jobs often lock tables, causing themselves (and the UI) to slow down.

## 2. Certificate & Secret Lifecycle
To prevent "401 Unauthorized" or "SSL Handshake" errors:
* **Key Vault Secrets:** Check the `Expiration Date` attribute. Secrets should be rotated every 90 days.
* **App Service Certificates:** Ensure the `.pfx` or App Service Managed Certificate is not within 30 days of expiry.
* **Octopus Deploy Variables:** When updating a secret in Key Vault, ensure the corresponding variable in Octopus Deploy is updated and the project is re-deployed to "sync" the change.

## 3. Database Maintenance Windows
* **Index Rebuilding:** Highly active tables (like `Applications`) require regular index maintenance to prevent query performance degradation.
* **Statistics Update:** Ensure SQL Statistics are updated so the Query Optimizer chooses the most efficient path.

## 4. Maintenance Check-list
- Verify backup integrity before major schema changes.
- Ensure "Maintenance Mode" page is ready if the UI needs to be taken offline.
- Check Azure Advisor for "Cost" and "Performance" recommendations monthly.