# Fintech Platform Operations Runbook
### Focus: Mission-Critical Application Support & Azure Infrastructure

This repository serves as a comprehensive technical framework for managing and troubleshooting a high-availability Fintech platform. It is designed to ensure data integrity, maintain 99.9%+ uptime, and provide structured incident response for complex lending systems.

## 🛠 Tech Stack Focus
* **Cloud:** Microsoft Azure (App Services, SQL Database, Service Bus)
* **DevOps:** Azure DevOps (Pipelines/Boards), Octopus Deploy
* **Monitoring:** Application Insights, KQL, Log Analytics
* **Automation:** PowerShell, Azure CLI, Bicep

## 📖 Runbook Index

To ensure rapid response during incidents, this runbook is organized by operational category:

### 📂 [01. Incident Response](./01-incident-response/)
* **[Platform Incident Triage](./01-incident-response/platform-incident-triage.md):** The "First 10 Minutes" framework for scope and impact assessment.

### 📂 [02. Technical Troubleshooting](./02-technical-troubleshooting/)
* **[SQL & Data Integrity](./02-technical-troubleshooting/sql-troubleshooting-data-integrity.md):** Safe investigation patterns and performance tuning for the data layer.
* **[App Service Log Analysis](./02-technical-troubleshooting/app-service-log-analysis.md):** KQL queries for Application Insights and identifying performance anti-patterns.
* **[Service Bus Management](./02-technical-troubleshooting/service-bus-queue-management.md):** Monitoring message health and handling dead-letter queues.
* **[External API Integration](./02-technical-troubleshooting/external-api-integration-troubleshooting.md):** Troubleshooting 3rd-party dependencies and credit bureau connectivity.

### 📂 [03. Platform Maintenance](./03-platform-maintenance/)
* **[Identity & Access (IAM)](./03-platform-maintenance/identity-access-management.md):** RBAC, Key Vault management, and secure secret rotation.
* **[Scheduled Tasks & Maintenance](./03-platform-maintenance/maintenance-scheduled-tasks.md):** Managing background WebJobs and database maintenance windows.
* **[Automation & PowerShell](./03-platform-maintenance/automation-powershell-utilities.md):** Self-healing scripts and Azure DevOps/Octopus Deploy integration.

### 📂 [04. Communication & Processes](./04-communication-and-processes/)
* **[Incident Communication Templates](./04-communication-and-processes/incident-communication-templates.md):** Professional templates for dealership and stakeholder updates.

---
*Developed for Application Support & Product Operations Excellence.*