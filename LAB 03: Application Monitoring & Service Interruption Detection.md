# LAB 03: Application Monitoring & Service Interruption Detection

> **Objective**
> Proactive monitoring allows you to detect issues before they become customer-impacting incidents. This lab covers monitoring key application health indicators across BFSI loan processing modules.

---

## 📖 Scenario

You are **on shift**. Your task is to perform active monitoring of all loan application services.

---

# 🛠️ Step-by-Step Tasks

| Step    | Task                                    | Details / Actions                                                                                                                                                                       |
| ------- | --------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **3.1** | **Open Monitoring Dashboard**           | Open **Grafana** or **Dynatrace**. Select the **Loan Application Production** dashboard. Verify that all dashboard panels are loading successfully.                                     |
| **3.2** | **Check API Health**                    | Monitor the **API error rate**. Raise an alert if the error rate exceeds **2%**. Check the following endpoints:<br>- `/loan-apply`<br>- `/kyc-verify`<br>- `/disburse`<br>- `/emi-calc` |
| **3.3** | **Monitor Transaction Throughput**      | Verify that **Transactions Per Minute (TPM)** remain within the expected range. A sudden drop may indicate a possible outage.                                                           |
| **3.4** | **Check Database Connections**          | Monitor the **database connection pool usage**. Raise an alert if usage exceeds **80%**. Verify that the average **query response time** does not exceed **3 seconds**.                 |
| **3.5** | **Verify Batch Job Status**             | Review the scheduled jobs dashboard for:<br>- EMI Generation<br>- Loan Synchronization<br>- Notification Jobs<br><br>Flag any jobs with a **FAILED** status.                            |
| **3.6** | **Monitor Server Resources**            | Monitor all application server nodes:<br>- **CPU:** Alert if > **80%**<br>- **Memory:** Alert if > **85%**<br>- **Disk:** Alert if > **90%**                                            |
| **3.7** | **Review Application Logs (Real-Time)** | Tail logs in **Kibana** or **Splunk**. Filter for the following log levels:<br>- `ERROR`<br>- `EXCEPTION`<br>- `TIMEOUT`<br>- `FAILED`<br><br>Flag any new error patterns.              |
| **3.8** | **Check Integration Endpoints**         | Verify third-party integrations:<br>- CIBIL API<br>- eNACH<br>- NSDL<br>- Bank APIs<br><br>Any timeout may indicate a potential disbursement issue.                                     |
| **3.9** | **Document Monitoring Findings**        | Record findings in the shift diary using the following status indicators:<br>- 🟢 **Green** – Normal<br>- 🟡 **Amber** – Watching<br>- 🔴 **Red** – Incident Raised                     |

---

# 📊 Key Metrics to Monitor

| Metric                 | Normal Range          | Warning Threshold    | Critical Threshold   | Required Action                 |
| ---------------------- | --------------------- | -------------------- | -------------------- | ------------------------------- |
| **API Error Rate**     | **< 0.5%**            | **0.5% – 2%**        | **> 2%**             | 🚨 Raise Incident               |
| **API Response Time**  | **< 500 ms**          | **500 ms – 2 s**     | **> 2 s**            | 🔍 Check Database & Application |
| **DB Connection Pool** | **< 60%**             | **60% – 80%**        | **> 80%**            | 📢 Alert DBA                    |
| **CPU Utilization**    | **< 60%**             | **60% – 80%**        | **> 80%**            | ⚙️ Check Running Processes      |
| **Batch Job Duration** | **Expected Duration** | **+20% of Expected** | **+50% of Expected** | 📄 Review Job Logs              |
| **Transaction Volume** | **Baseline ±10%**     | **Baseline ±20%**    | **Drop > 30%**       | 🚨 Potential Outage             |

---

# 💡 Best Practice Tips

> **Follow these best practices to improve monitoring effectiveness and reduce incident response time.**

| #     | Best Practice                                                                                                                                                                                                                                                       |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | ✅ Set up automated alerts so you are notified before users report issues. **Proactive monitoring is always better than reactive monitoring.**                                                                                                                       |
| **2** | 📈 Establish baseline traffic patterns (morning peak, lunch dip, batch processing windows) to reduce false alarms.                                                                                                                                                  |
| **3** | 🔗 Monitor integration APIs (CIBIL, eNACH, NSDL, Bank APIs) independently, as they are common external failure points beyond your control.                                                                                                                          |
| **4** | 🔍 Correlate multiple metrics together. For example:<br>**CPU Spike + Database Slowness + API Errors = Likely Database Bottleneck (not necessarily an application bug).**                                                                                           |
| **5** | ⭐ Create a **Golden Signals** dashboard to monitor the four primary service health indicators:<br>- **Latency**<br>- **Errors**<br>- **Traffic**<br>- **Saturation**<br><br>These four signals typically help identify approximately **90% of operational issues**. |

---

# 📌 Summary

During this lab, you performed proactive monitoring of production loan application services by:

* Monitoring application dashboards.
* Validating API health and response times.
* Tracking transaction throughput.
* Monitoring database health.
* Verifying scheduled batch jobs.
* Checking server resource utilization.
* Reviewing real-time application logs.
* Validating third-party integrations.
* Documenting monitoring observations and incident status.

> **Outcome:** Effective proactive monitoring enables early detection of issues, minimizes customer impact, and improves overall service availability.
