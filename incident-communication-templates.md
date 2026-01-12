# Incident Communication Templates

Standardized templates for communicating technical issues to non-technical stakeholders (Dealers, Underwriters, and Partners).

## 1. External Dependency Outage (e.g., Credit Bureau Down)
**Scenario:** A 3rd party service is failing, causing app timeouts.
* **The Message:** "We have identified a connection delay with one of our external data partners. This is preventing some applications from processing immediately. Our team is monitoring the partner's status, and we recommend retrying in 15-30 minutes."

## 2. System Slowness (Database Contention)
**Scenario:** The SQL database is slow, making the UI lag.
* **The Message:** "We are currently experiencing high traffic volumes on the platform, which may result in slower-than-usual response times. We are working to optimize performance and expect normal speeds to return shortly. No data has been lost."

## 3. Deployment Window Notification
**Scenario:** A scheduled update via Octopus Deploy.
* **The Message:** "The platform will undergo scheduled maintenance on [Date] at [Time] to introduce new features and performance enhancements. The system will be unavailable for approximately [X] minutes. Thank you for your cooperation."

## 4. Communication Principles
* **Be Proactive:** It is better to tell the user there is a problem before they call us.
* **Be Clear:** Avoid technical jargon (e.g., use "Connection issue" instead of "TCP Handshake Failure").
* **Provide a 'Next Step':** Always tell the user what they should do (Wait, Refresh, or Contact Support again).