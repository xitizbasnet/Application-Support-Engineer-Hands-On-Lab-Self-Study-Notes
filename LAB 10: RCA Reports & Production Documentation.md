# LAB 10: RCA Reports & Production Documentation

> **Objective**
> Professional documentation is non-negotiable in BFSI environments. Accurate and complete documentation ensures accountability, supports audits, improves incident response, and enables continuous operational improvement.
>
> This lab covers the creation of:
>
> * Root Cause Analysis (RCA) Reports
> * Daily Support Reports
> * SLA Compliance Reports
> * Incident Summaries
> * Knowledge Base Articles

---

# 📖 Scenario

You must write a complete **RCA Report** for the **P1 Loan Approval System Outage** identified in **Lab 07**.

The report must meet enterprise documentation standards and be suitable for sharing with technical teams, management, and audit stakeholders.

---

# 🛠️ Step-by-Step Tasks

| Step      | Task                             | Details                                                                                                                                                                                                                |
| --------- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **10.1**  | **Structure the RCA Report**     | Create the following sections:<br><br>- Executive Summary<br>- Incident Timeline<br>- Impact Assessment<br>- Root Cause<br>- Contributing Factors<br>- Corrective Actions                                              |
| **10.2**  | **Write Executive Summary**      | Provide a 3–4 sentence summary covering:<br><br>- What failed<br>- When it occurred<br>- Duration of impact<br>- Number of affected users<br>- Current status                                                          |
| **10.3**  | **Build Incident Timeline**      | Create a chronological timeline using:<br><br>**Time | Event | Owner | Duration**<br><br>Minimum events required:<br>- Alert Detection<br>- Acknowledgement<br>- L2 Escalation<br>- Fix Implementation<br>- Resolution |
| **10.4**  | **Calculate Business Impact**    | Document:<br><br>- Number of affected users<br>- Failed transactions<br>- Revenue impact (if measurable)<br>- SLA breach details                                                                                       |
| **10.5**  | **Document Root Cause**          | Write a clear, technical, and factual root cause statement.<br><br>Reference:<br>- Application logs<br>- Database findings<br>- Monitoring data                                                                        |
| **10.6**  | **List Corrective Actions**      | Create a corrective action table:<br><br>**Action | Owner | Target Date | Status**<br><br>Minimum required actions:<br>- Immediate<br>- Short-term<br>- Long-term                                                      |
| **10.7**  | **Write Daily Support Report**   | Include:<br><br>- Open tickets<br>- Closed tickets<br>- P1/P2 incident count<br>- SLA compliance percentage<br>- Pending escalations                                                                                   |
| **10.8**  | **Create SLA Compliance Report** | Prepare monthly SLA metrics:<br><br>- Total incidents<br>- Incidents responded within SLA<br>- Incidents resolved within SLA<br>- SLA breach count<br>- MTTR (Mean Time To Resolve)                                    |
| **10.9**  | **Update Knowledge Base**        | Create a KB article containing:<br><br>- Symptom<br>- Root cause<br>- Resolution steps<br>- Prevention steps<br><br>Apply appropriate tags for searchability.                                                          |
| **10.10** | **Archive & Distribute**         | Complete documentation distribution:<br><br>- Save in shared drive.<br>- Email to:<br>  - Support Lead<br>  - Development Manager<br>  - Operations Head<br>- Archive in ITSM tool.                                    |

---

# 📄 RCA Report Template

# ROOT CAUSE ANALYSIS REPORT

---

## Incident Details

| Field           | Details                  |
| --------------- | ------------------------ |
| **Incident ID** | INC-2025-001234          |
| **Severity**    | P1 — Critical            |
| **System**      | Loan Approval API        |
| **Reported By** | Application Support Team |
| **Report Date** | 15 January 2025          |

---

# 📝 Executive Summary

The Loan Approval API experienced a complete outage from **14:00 to 15:32 IST on 15 Jan 2025**, lasting **92 minutes**.

Approximately **2,000 customers** were unable to check or receive loan approvals.

The issue was caused by **JVM heap exhaustion triggered by a memory leak introduced in version v2.3.1**, which was deployed at **12:30 IST**.

---

# ⏱️ Incident Timeline

| Time          | Event                                                                     | Owner                        |
| ------------- | ------------------------------------------------------------------------- | ---------------------------- |
| **13:58 IST** | Grafana alert triggered: API error rate exceeded **10%**                  | Monitoring                   |
| **14:00 IST** | L1 acknowledged alert and created incident **INC-2025-001**               | L1 Support                   |
| **14:12 IST** | Root cause not identified; escalated to L2                                | L1 Support                   |
| **14:18 IST** | L2 identified OOM errors in application logs and engaged Development team | L2 Support                   |
| **14:45 IST** | Development team confirmed memory leak in version **v2.3.1**              | Development Team             |
| **15:10 IST** | Emergency rollback to version **v2.3.0** initiated                        | Development + Infrastructure |
| **15:32 IST** | Service fully restored and all APIs returned healthy status               | L2 Support                   |

---

# 🔍 Root Cause

## Technical Root Cause

A memory leak was introduced in:

```text
DocumentParserService.parseApprovalDocs()
```

method in application version:

```text
v2.3.1
```

Objects created during document parsing were not released correctly, causing continuous JVM heap growth from **12:30 IST to 14:00 IST**.

This resulted in:

* JVM heap exhaustion.
* Application server failure.
* HTTP 503 responses from the Loan Approval API.

---

# 🔧 Corrective Actions

| #     | Action                                      | Status         | Owner          | Target Date |
| ----- | ------------------------------------------- | -------------- | -------------- | ----------- |
| **1** | Emergency rollback to version v2.3.0        | ✅ DONE         | Dev + Infra    | 15 Jan      |
| **2** | Fix memory leak and complete code review    | 🔄 IN PROGRESS | Development    | 17 Jan      |
| **3** | Add JVM heap usage alert at 85%             | 📅 PLANNED     | Infrastructure | 20 Jan      |
| **4** | Add memory profiling step to CI/CD pipeline | 📅 PLANNED     | DevOps         | 31 Jan      |

---

# 💡 Best Practice Tips

> **Follow these documentation practices to create effective RCA and operational reports.**

| #     | Best Practice                                                                                                                                                                                                      |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1** | 📝 Write RCA reports for different audiences:<br><br>- Executive Summary → Managers and stakeholders<br>- Technical Details → Engineers and support teams<br><br>Maintain one document that serves both audiences. |
| **2** | 📌 Every corrective action must have a defined owner and completion date. Generic actions such as "improve monitoring" are difficult to track and rarely complete successfully.                                    |
| **3** | 📊 Use factual language in RCA documentation.<br><br>Preferred:<br>`The API returned HTTP 503 at 14:00:05.`<br><br>Avoid:<br>`The system crashed suddenly.`                                                        |
| **4** | 📚 Maintain a P1/P2 incident register. After analyzing multiple incidents, recurring patterns can reveal opportunities for systemic improvements.                                                                  |
| **5** | 🔄 Keep Knowledge Base articles updated. Outdated KB articles force engineers to repeat investigations for already-known issues.                                                                                   |

---

# 📌 Summary

During this lab, you learned how to:

* Create professional RCA reports.
* Document incident timelines.
* Measure business impact.
* Identify and document root causes.
* Define corrective actions with ownership.
* Prepare daily support reports.
* Track SLA compliance.
* Maintain knowledge base documentation.
* Archive and distribute production documentation.

> **Outcome:** High-quality production documentation improves incident transparency, accelerates troubleshooting, supports compliance requirements, and enables continuous improvement across BFSI application support operations.
