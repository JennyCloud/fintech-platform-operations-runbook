# SLA & Severity Level Definitions

To ensure we meet our contractual obligations to our partners, incidents are categorized by business impact.

## 1. Severity Levels (The "Priority" Matrix)

| Level | Definition | Response Goal (MTTA) | Resolution Goal (MTTR) |
| :--- | :--- | :--- | :--- |
| **P1 - Critical** | Platform-wide outage. No one can submit loans. | < 15 Mins | < 4 Hours |
| **P2 - High** | Major feature broken (e.g., Credit Bureau down). | < 1 Hour | < 8 Hours |
| **P3 - Medium** | Minor bug. Workaround exists. UI glitch. | < 4 Hours | < 3 Business Days |
| **P4 - Low** | Cosmetic issue or request for info. | < 1 Business Day | Next Release |

## 2. Defending the SLA
As Product Operations, we protect the 99.9% uptime target by:
* **Proactive Alerting:** Using Azure Monitor to catch CPU/DTU spikes *before* they cause a crash.
* **Rapid Triage:** Using the "Incident Triage Guide" to identify the blast radius immediately.
* **Automated Self-Healing:** Using PowerShell scripts to clear temp files or restart stalled services before they impact users.

## 3. SLA Exceptions
* **Scheduled Maintenance:** Updates performed via Octopus Deploy during the 2:00 AM - 4:00 AM window.
* **Force Majeure:** Major Azure Region outages (e.g., US East is down).