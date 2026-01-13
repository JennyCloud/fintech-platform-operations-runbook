# Root Cause Analysis (RCA) Template

This template is used to document major incidents and prevent future recurrence.

## 1. Incident Overview
* **Date/Time:** * **Duration:** * **Impact:** (e.g., 15 Dealerships unable to submit loans)

## 2. The "5-Whys" Analysis
1. **The Problem:** The application was slow.
2. **Why?** The SQL database was at 100% DTU.
3. **Why?** A new reporting query was running without an index.
4. **Why?** The query was deployed without being tested on a production-sized dataset.
5. **Root Cause:** Lack of performance testing in the CI/CD pipeline for new reporting features.

## 3. Corrective Actions (Preventative Measures)
* **Short-Term:** Killed the blocking process and added a missing index.
* **Long-Term:** Updated the Azure DevOps pipeline to include a "Query Performance" check stage.
* **Monitoring:** Added an Azure Monitor Alert for SQL DTU usage > 80%.