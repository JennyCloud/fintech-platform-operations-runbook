# Platform Incident Triage & Critical Response

This document outlines the immediate steps to be taken when a high-priority (P1/P2) incident is reported. The goal is to minimize Mean Time to Recovery (MTTR) without sacrificing data integrity.

## 1. Initial Triage: Scope Assessment
Before performing any technical actions, determine the **Blast Radius**:
* **Individual:** Single user or single dealership (Check browser cache, local ISP, or specific account permissions).
* **Regional:** Multiple users in one geographic area (Check Azure Region health or local CDN endpoints).
* **Global:** System-wide failure (Check Core API, SQL Cluster, or Global Identity provider).

## 2. The "What Changed?" Check
Analyze the environment for recent modifications using the following logs:
* **Azure Activity Logs:** Filter for `Write` or `Delete` operations in the last 60 minutes.
* **Deployment Pipeline:** Check for recent code deployments or configuration changes (CI/CD).
* **DB Audit Logs:** Look for unexpected Schema changes or massive `UPDATE` queries.

## 3. Layer Isolation Checklist
Work from the "outside in" to find the bottleneck:
1. **Connectivity:** Can we ping the endpoint? Are there SSL certificate errors?
2. **Web Layer:** Check Azure App Service logs for `5xx` errors.
3. **Queue/Bus Layer:** Check for backed-up messages in Azure Service Bus (The "Thundering Herd" indicator).
4. **Data Layer:** Check SQL for blocking sessions or high CPU/DTU usage.

## 4. Emergency Action Guardrails
* **No "Blind" Restarts:** Do not restart a server without capturing a memory dump or checking logs first.
* **Log Everything:** Every command run during an incident must be documented for the Post-Mortem.
* **Stakeholder Sync:** Provide a brief status update every 15-30 minutes during a total outage.