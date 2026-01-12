# Azure Service Bus & Message Queue Management

This document outlines the procedures for monitoring and troubleshooting asynchronous message processing. In a Fintech environment, queues ensure that spikes in loan applications or payment processing do not overwhelm backend services.

## 1. Monitoring Queue Health
The primary indicator of a bottleneck is the **Message Count**.
* **Active Messages:** High numbers indicate the backend "worker" service is too slow or down.
* **Dead-Letter Messages:** These are messages that failed to process after multiple attempts (Max Delivery Count exceeded). These require manual investigation.

## 2. Troubleshooting "Dead-Letter" Queues (DLQ)
When a message moves to the DLQ, it usually indicates a data or logic error.
1. **Peek Messages:** Use Service Bus Explorer to "Peek" at the message body without removing it.
2. **Check Dead-Letter Reason:** Look at the `DeadLetterReason` property (e.g., `HeaderSizeExceeded` or `TTLExpiredException`).
3. **Check Dependencies:** Often, messages dead-letter because the SQL Database was too busy to accept the "Write" request.

## 3. Handling the "Thundering Herd" (Traffic Spikes)
To prevent a sudden rush of users from crashing the system:
* **Throttling:** Implement rate-limiting at the API layer so the queue doesn't grow faster than it can be cleared.
* **Competing Consumers:** Scale out the "Worker" services (add more instances) to pull messages off the queue faster during peak hours.

## 4. KQL for Queue Monitoring
To see the trend of dead-lettered messages over the last 4 hours:
AzureMetrics | where ResourceProvider == "MICROSOFT.SERVICEBUS" | where MetricName == "DeadletteredMessages" | summarize max(Maximum) by bin(TimeGenerated, 15m), Resource | render timechart

## 5. Emergency Recovery Actions
* **Re-submit Messages:** After fixing the root cause (e.g., a SQL timeout), re-submit dead-lettered messages back to the Active queue for processing.
* **Purge Queue:** Only used in development/testing or if the queue is filled with corrupted, non-essential messages. Never purge a production "Loan Application" queue.