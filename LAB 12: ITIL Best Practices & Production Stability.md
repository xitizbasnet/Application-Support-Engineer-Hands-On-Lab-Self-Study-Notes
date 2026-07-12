# LAB 12: ITIL Best Practices & Production Stability

> **Objective**
> ITIL (Information Technology Infrastructure Library) provides the framework that structures Application Support activities and enables consistent, reliable, and measurable IT service delivery.
>
> This final lab consolidates ITIL concepts and covers comprehensive production health maintenance practices required for BFSI application support.

---

# 📘 ITIL Processes in Application Support

The following ITIL processes define key Application Support responsibilities, activities, and tools.

| ITIL Process                   | Your Role                     | Key Activity                                                                                | Tool Used                            |
| ------------------------------ | ----------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------ |
| **Incident Management**        | L1/L2 Engineer                | Detect, classify, resolve, and close incidents while maintaining SLA compliance             | ServiceNow / Jira Service Management |
| **Problem Management**         | L2 Engineer + Problem Manager | Identify recurring issues, perform Root Cause Analysis (RCA), and implement permanent fixes | ServiceNow Problems                  |
| **Change Management**          | Support Engineer + CAB        | Review, approve, validate, and support all production changes                               | ServiceNow Change Management         |
| **Service Request Management** | L1 Engineer                   | Fulfill standard requests such as reports, access requests, and data queries                | ServiceNow Service Catalog           |
| **Event Management**           | L1 Monitoring Engineer        | Monitor alerts, classify events, and proactively respond to system conditions               | Grafana / Splunk                     |
| **Knowledge Management**       | L1/L2 Engineer                | Create and update Knowledge Base articles based on incident learnings                       | Confluence / SharePoint              |
| **SLA Management**             | Team Lead + L1 Engineer       | Track SLA compliance, report breaches, and identify service trends                          | ServiceNow Reports                   |

---

# 🏥 Daily Production Stability Checklist

Use this checklist at the beginning of each shift to ensure production health and stability.

| Step     | Task                                | Details                                                                                                                                                                                                     |
| -------- | ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **12.1** | **Morning Health Check**            | Verify:<br><br>- All services are running<br>- No overnight alerts<br>- Batch jobs completed successfully<br>- No open P1/P2 incidents from the night shift                                                 |
| **12.2** | **Application Health Verification** | Test five critical business workflows:<br><br>- Loan Application<br>- KYC Submission<br>- EMI View<br>- Repayment Processing<br>- Disbursement Check<br><br>All workflows must return successful responses. |
| **12.3** | **Server Connectivity Check**       | Perform infrastructure validation:<br><br>- Ping/curl all application servers.<br>- Verify database connectivity using:<br><br>`sql SELECT 1; `<br><br>- Check load balancer health page.                   |
| **12.4** | **Database Validation**             | Verify database health:<br><br>- Active connections<br>- Long-running queries (>60 seconds)<br>- Table lock waits<br>- Replication lag (if applicable)                                                      |
| **12.5** | **Error Rate Review**               | Review Grafana metrics:<br><br>- Compare current error rate with the same time yesterday.<br>- Raise an alert if deviation exceeds **10%**.                                                                 |
| **12.6** | **Open Incident Review**            | Review all active incidents:<br><br>- Check approaching SLA breaches.<br>- Identify stuck P2 incidents requiring escalation.                                                                                |
| **12.7** | **Recurring Incident Analysis**     | Perform weekly analysis:<br><br>- Categorize incidents.<br>- Identify the top three recurring categories.<br>- Raise Problem tickets where required.                                                        |
| **12.8** | **Shift Handover**                  | Prepare a complete handover note containing:<br><br>- Open incidents<br>- Ongoing deployments<br>- Pending escalations<br>- Things to monitor<br>- Important contacts                                       |

---

# 💡 Best Practice Tips

> **Follow these ITIL-based practices to maintain production stability and improve support effectiveness.**

| #     | Best Practice                                                                                                                                              |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | 🌅 Start every shift with a **5-minute health check**. Detecting issues before users report them is a key characteristic of an effective support engineer. |
| **2** | 🎯 Own tickets end-to-end. Handing off issues without tracking them can result in SLA breaches and poor customer experience.                               |
| **3** | 🔄 Build repeatable habits instead of relying on individual heroics. Consistent processes prevent more incidents than emergency recoveries.                |
| **4** | 🤖 Automate repetitive checks. Create scripts for daily health validation so engineers can focus on complex troubleshooting activities.                    |
| **5** | 📚 Treat every incident as a learning opportunity. Review RCA documents, understand patterns, and prepare for future occurrences.                          |
| **6** | ⚙️ ITIL is a framework, not a strict rulebook. Adapt processes to your environment while ensuring that core ITIL practices are always followed.            |

---

# 📌 Production Support Maturity Checklist

| Capability                                            | Implemented |
| ----------------------------------------------------- | ----------- |
| Incident Management process established               | ☐           |
| Problem Management and RCA process followed           | ☐           |
| Change approvals completed before production releases | ☐           |
| Service Requests managed through catalog workflow     | ☐           |
| Monitoring alerts actively managed                    | ☐           |
| Knowledge Base maintained and updated                 | ☐           |
| SLA metrics tracked and reviewed                      | ☐           |
| Daily production health checks completed              | ☐           |
| Shift handovers documented                            | ☐           |
| Recurring issues converted into Problem Records       | ☐           |

---

# 📌 Summary

During this final lab, you learned how to:

* Apply ITIL processes in Application Support.
* Understand Incident, Problem, Change, Request, Event, Knowledge, and SLA Management.
* Perform daily production stability checks.
* Validate application, server, and database health.
* Review incidents and identify recurring problems.
* Perform effective shift handovers.
* Apply ITIL best practices for continuous improvement.

> **Outcome:** A strong ITIL-based support approach improves service reliability, reduces incident recurrence, increases operational efficiency, and ensures stable BFSI production environments.
