# Fintech Platform Operations Runbook
### Focus: Mission-Critical Application Support & Proactive Product Operations

This repository serves as a comprehensive technical framework for managing and troubleshooting a high-availability, **multi-tenant SaaS** platform. It is designed to ensure data integrity, protect contractual SLAs (99.9% uptime), and shift from reactive support to **proactive observability**.

## 🛠 Tech Stack Focus
* **Cloud:** Microsoft Azure (App Services, SQL Database, Service Bus)
* **DevOps:** Azure DevOps, Octopus Deploy (Multi-tenant Release Orchestration)
* **Observability:** New Relic (NRQL), Application Insights (KQL), Log Analytics
* **Automation:** PowerShell, Azure CLI, Synthetic Monitoring Concepts (Selenium)

### 🚀 Deployment Philosophy: The "Best-of-Breed" Stack
While tools like GitHub Actions offer a unified experience, this runbook is optimized for the **Azure DevOps + Octopus Deploy** architecture:
* **Azure DevOps (The Factory):** Handles CI, automated testing, and secure artifact generation.
* **Octopus Deploy (The Logistics):** Specialized CD engine for managing environment-scoped variables and complex releases across dealership tenants.

---

## 📖 Runbook Index

### 📂 [01. Incident Response](./01-incident-response/)
* **[Platform Incident Triage](./01-incident-response/platform-incident-triage.md):** Framework for rapid impact assessment.
* **[SLA & Severity Levels](./01-incident-response/sla-and-severity-levels.md):** Defining P1-P4 priorities and managing SLIs/SLOs.

### 📂 [02. Technical Troubleshooting](./02-technical-troubleshooting/)
* **[SQL & Data Integrity](./02-technical-troubleshooting/sql-troubleshooting-data-integrity.md):** Investigation patterns for multi-tenant data isolation.
* **[App Service & Observability](./02-technical-troubleshooting/app-service-log-analysis.md):** KQL/NRQL queries for identifying performance bottlenecks.
* **[Service Bus Management](./02-technical-troubleshooting/service-bus-queue-management.md):** Monitoring asynchronous message health.
* **[External API Integration](./02-technical-troubleshooting/external-api-integration-troubleshooting.md):** Troubleshooting 3rd-party dependencies (Credit Bureaus).

### 📂 [03. Platform Maintenance](./03-platform-maintenance/)
* **[Identity & Access (IAM)](./03-platform-maintenance/identity-access-management.md):** RBAC and secure Key Vault secret rotation.
* **[Scheduled Tasks & Maintenance](./03-platform-maintenance/maintenance-scheduled-tasks.md):** Managing WebJobs and background processing.
* **[Automation & Synthetics](./03-platform-maintenance/automation-powershell-utilities.md):** Self-healing scripts and **Synthetic Monitoring** (User Emulation) strategies.

### 📂 [04. Communication & Processes](./04-communication-and-processes/)
* **[Incident Communication Templates](./04-communication-and-processes/incident-communication-templates.md):** Stakeholder and dealership communication.
* **[Root Cause Analysis (RCA)](./04-communication-and-processes/root-cause-analysis-template.md):** Post-mortem documentation using the "5-Whys."

---
*Developed for Application Support & Product Operations Excellence.*