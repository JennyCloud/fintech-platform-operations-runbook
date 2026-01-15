# Automation & PowerShell Utilities

This document centralizes scripts used for routine maintenance, rapid diagnostics, and self-healing operations within the Fintech platform. 

> **CRITICAL:** All scripts must be heavily tested in a "Sandbox" or "UAT" environment before being executed against Production. Data integrity is the highest priority.

## 1. Automation Philosophy
* **Read-Only First:** Scripts should gather data and report status before making changes.
* **Idempotency:** Scripts should be safe to run multiple times without causing unintended side effects.
* **Logging:** All automated actions must log to a central repository (Log Analytics) for audit purposes.

## 2. Essential Diagnostic Scripts

### A. Azure App Service Health Check
Quickly check the status of all instances in a production App Service Plan.

Get-AzWebApp -ResourceGroupName "Fintech-Prod-RG" | Select-Object Name, State, DefaultHostName, AppServicePlan

### B. SQL Connection Test (Connectivity Validation)
Verify that the application layer can physically reach the SQL backend.

Test-NetConnection -ComputerName "fintech-prod-sql.database.windows.net" -Port 1433

### C. Clean Up Old Temp Files (Self-Healing)
A script to clear temporary storage when a server disk hits a specific threshold.

$threshold = 90 $disk = Get-PSDrive C | Select-Object Used, Free $percentUsed = ($disk.Used / ($disk.Used + $disk.Free)) * 100

if ($percentUsed -gt $threshold) { Write-Output "Disk usage above threshold. Initiating cleanup..." Remove-Item "C:\Temp*" -Recurse -Force }

## 3. CI/CD & Deployment Framework (Inovatec Stack)
To maintain environment consistency and minimize deployment risk, the platform utilizes:
* **Azure DevOps Pipelines:** For Continuous Integration (CI), automated testing, and security scanning of .NET code.
* **Octopus Deploy:** Used for release orchestration and environment-scoped variable management.
* **Infrastructure as Code (IaC):** Bicep or ARM templates are used to prevent "Environment Drift."

## 4. Deployment Troubleshooting (Octopus Deploy)
1. **Check the Task Log:** Look for "Variable Substitution" errors (most common).
2. **Verify Tentacle Health:** Ensure the target App Service or Server is communicating with the Octopus server.
3. **Manual Intervention:** If a release hangs, check the "Guided Failure" logs to see if a specific SQL migration script blocked the release.

## 5. Observability & Synthetic Monitoring (Future Roadmap)
To shift from reactive to proactive support, the platform strategy includes:
* **Synthetic Transactions:** Utilizing Selenium-based scripts to emulate end-to-end user journeys (Login -> Loan Submission).
* **Observability with NRQL:** Transitioning KQL query logic to New Relic (NRQL) to monitor Real-User Monitoring (RUM) and backend transaction health.
* **Proactive Alerting:** Configuring alerts based on "Synthetic Failures" to resolve issues before they impact real users.