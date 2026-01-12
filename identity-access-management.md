# Identity & Access Management (IAM) and RBAC

This document outlines the security protocols for managing access to the Fintech platform, ensuring that all actions are authenticated, authorized, and audited.

## 1. The Principle of Least Privilege (PoLP)
Access should be granted only to the level required to perform a specific task.
* **Reader/Contributor:** Use for general support staff who need to view logs but not change infrastructure.
* **Custom Roles:** Prefer specific actions (e.g., `Microsoft.Web/sites/restart/Action`) over broad "Contributor" roles for support engineers.
* **PIM (Privileged Identity Management):** Use "Just-In-Time" (JIT) access for high-level admin tasks to ensure permanent global admin accounts do not exist.

## 2. Managing External Access (B2B/B2C)
For dealership users and external partners:
* **Conditional Access Policies:** Require MFA (Multi-Factor Authentication) for all logins, especially those coming from outside the corporate network.
* **Sign-in Risk:** Block or challenge logins that originate from "impossible travel" locations or known malicious IP addresses.

## 3. Auditing & Troubleshooting Access Issues
When a user or service principal cannot access a resource:

### A. Checking Effective Permissions
Use the **"Access Control (IAM) -> Check Access"** tool in the Azure Portal to determine why a user is blocked.

### B. KQL Query for Audit Logs
To find out "Who deleted/changed this resource?":
AzureActivity | where TimeGenerated > ago(7d) | where OperationNameValue contains "Delete" or OperationNameValue contains "Write" | project TimeGenerated, Caller, OperationNameValue, ResourceGroup, _ResourceId | order by TimeGenerated desc

## 4. Key Vault & Secret Management
* **Managed Identities:** Use System-Assigned Managed Identities for App Services to access SQL or Storage. This eliminates the need to store passwords in `appsettings.json`.
* **Secret Rotation:** Ensure that API keys for 3rd party services (Credit Bureaus, etc.) are stored in Key Vault and rotated every 90 days.

## 5. Security Incident Guardrails
* **Compromised Account:** Immediately revoke all active sessions for the user in Entra ID (Azure AD) and reset their password.
* **Locking Resources:** Use "ReadOnly" or "CanNotDelete" resource locks on production databases to prevent accidental deletion during high-pressure incidents.