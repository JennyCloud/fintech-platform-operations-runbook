# External API & Third-Party Integration Troubleshooting

Fintech platforms rely heavily on external integrations (Credit Bureaus, VIN Decoders, Address Validation). When a process fails, it is often due to an external dependency rather than internal code.

## 1. Identifying Integration Failures
Use Application Insights to determine if the failure happened "Outside" our network.
* **Dependency Failures:** Look for `ResultCode` 401 (Unauthorized), 403 (Forbidden), or 504 (Gateway Timeout) from external URLs.
* **Duration Spikes:** If an external credit check usually takes 2 seconds but is now taking 20 seconds, the platform will likely time out.

## 2. KQL: Correlating Internal Requests with External Calls
Use this query to see which external dependencies are failing:

dependencies | where timestamp > ago(1h) | where success == false | summarize count() by name, target, resultCode | order by count_ desc

## 3. Common Integration Issues
* **Expired API Keys:** Check Azure Key Vault for secret expiration dates.
* **IP Whitelisting:** If Inovatec scales its App Service, the new outbound IP address might need to be whitelisted by the partner (e.g., Equifax/TransUnion).
* **TLS Mismatch:** Ensure the external partner hasn't disabled older TLS versions (e.g., moving from 1.1 to 1.2/1.3).

## 4. Emergency Action: "Circuit Breaking"
If an external API is completely down and causing the Inovatec platform to crash:
* **Feature Flag:** If available, disable the specific feature (e.g., "Instant Credit Check") via the configuration panel to allow users to still submit applications for manual review.
* **Bypass:** Divert the traffic to a secondary provider if a failover partner is configured.