# LAB 07: Root Cause Analysis (RCA) & Cross-Team Coordination

> **Objective**
> Root Cause Analysis (RCA) identifies **why an incident occurred** and **how to prevent recurrence**. Effective cross-team coordination ensures faster resolution and long-term service improvement.
>
> This lab covers the complete RCA process for BFSI loan application incidents.

---

# 📖 Scenario

A **P1 incident** has occurred:

> **Loan Approval System Down for 90 Minutes**

Your task is to conduct a complete **Root Cause Analysis (RCA)** and coordinate with all required teams to identify the cause, define corrective actions, and prevent recurrence.

---

# 🛠️ Step-by-Step Tasks

| Step    | Task                              | Details                                                                                                                                                                                                                                                                                |
| ------- | --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **7.1** | **Gather Incident Timeline**      | Collect the complete incident timeline:<br><br>- Alert Time<br>- Detection Time<br>- Acknowledgement Time<br>- Escalation Time<br>- Resolution Time<br>- Business Impact                                                                                                               |
| **7.2** | **Assemble RCA Team**             | Invite required stakeholders:<br><br>- L2 Support Lead<br>- Developer<br>- DBA<br>- Infrastructure Team<br>- Network Team<br>- Business / Operations Representative                                                                                                                    |
| **7.3** | **Define Problem Statement**      | Clearly document the issue statement:<br><br>**"Loan approval API returned HTTP 503 from 14:00–15:30 IST affecting all 2,000 users."**                                                                                                                                                 |
| **7.4** | **Apply 5-Why Analysis**          | Perform structured root cause analysis:<br><br>**Why 1:** Why did the API return 503?<br>➡ Application server was down.<br><br>**Why 2:** Why was the application server down?<br>➡ JVM heap memory was exhausted.<br><br>Continue analysis until the actual root cause is identified. |
| **7.5** | **Collect Evidence**              | Gather supporting technical evidence:<br><br>- Application Logs<br>- Garbage Collection (GC) Logs<br>- Heap Dump<br>- Database Slow Query Logs<br>- Network Traffic During Incident                                                                                                    |
| **7.6** | **Identify Contributing Factors** | Document additional factors that contributed to the incident:<br><br>- No heap monitoring alert configured<br>- Recent code deployment without memory profiling<br>- Missing circuit breaker implementation                                                                            |
| **7.7** | **Cross-Team Coordination**       | Define ownership across teams:<br><br>**Development:** Fix memory leak.<br><br>**Infrastructure:** Add JVM heap monitoring alerts.<br><br>**QA:** Add memory-focused load testing.<br><br>**Release Management:** Schedule deployment activities.                                      |
| **7.8** | **Define Corrective Actions**     | Define actions based on priority:<br><br>**Immediate:** Restart application with larger heap allocation.<br><br>**Short-Term:** Deploy memory leak fix.<br><br>**Long-Term:** Implement automated heap profiling.                                                                      |
| **7.9** | **Document & Share RCA**          | Complete the RCA report and:<br><br>- Share with all stakeholders.<br>- Archive in the knowledge base.<br>- Update operational runbooks with new preventive actions.                                                                                                                   |

---

# 📋 5-Why RCA Template

## Incident Details

| Field           | Details                |
| --------------- | ---------------------- |
| **Incident**    | Loan Approval API Down |
| **Time Window** | 14:00–15:30 IST        |
| **Impact**      | 2,000 users affected   |
| **Duration**    | 90 minutes             |

---

## 🔍 5-Why Analysis

### WHY 1: Why did the API fail?

**Answer:**

➡ Application server returned:

```text
HTTP 503 - Service Unavailable
```

---

### WHY 2: Why did the application server fail?

**Answer:**

➡ JVM heap memory was exhausted.

```text
OOM: Java heap space at 14:00:05
```

---

### WHY 3: Why did heap memory get exhausted?

**Answer:**

➡ Memory leak occurred in:

```text
DocumentParserService
```

Objects were not released after document parsing operations.

---

### WHY 4: Why was the memory leak not detected earlier?

**Answer:**

➡ Recent code change:

```text
Version: v2.3.1
Deployment Time: 12:30
```

was not profiled for memory usage before deployment.

---

### WHY 5: Why was the code deployed without memory profiling?

**Answer:**

➡ There was:

* No memory profiling step in the CI/CD pipeline.
* No production heap usage alert configured.

---

# 🎯 Root Cause

> **Insufficient pre-deployment memory profiling combined with missing production JVM heap monitoring alerts.**

---

# ✅ Corrective Action

Implement the following improvements:

| Priority       | Action                                                                                         |
| -------------- | ---------------------------------------------------------------------------------------------- |
| **Immediate**  | Restart application with increased heap allocation.                                            |
| **Short-Term** | Deploy the memory leak fix.                                                                    |
| **Long-Term**  | Add heap profiling to the CI/CD pipeline and configure JVM heap alerts at **85% utilization**. |

---

# 💡 Best Practice Tips

> **Follow these RCA practices to improve reliability, accountability, and continuous improvement.**

| #     | Best Practice                                                                                                                                                                |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | ✅ Always blame the **process**, never the person. RCA focuses on systemic improvement rather than individual blame.                                                          |
| **2** | ⏱️ Complete RCA within **48 hours of P1 resolution**. Evidence quality and incident details become harder to capture as time passes.                                         |
| **3** | 📌 Assign a specific owner and deadline for every corrective action. Actions without ownership are often not completed.                                                      |
| **4** | 🔍 Categorize root causes:<br><br>- Infrastructure<br>- Code<br>- Configuration<br>- Process<br>- Human Error<br><br>Patterns across categories help identify systemic gaps. |
| **5** | 📚 Share RCA summaries (without sensitive information) across teams. Other teams can learn from incidents they did not directly experience.                                  |

---

# 📌 Summary

During this lab, you learned how to:

* Build an incident timeline.
* Assemble a cross-functional RCA team.
* Define a clear problem statement.
* Perform 5-Why analysis.
* Collect technical evidence.
* Identify contributing factors.
* Coordinate corrective actions across teams.
* Document and share RCA reports.
* Improve operational processes through preventive actions.

> **Outcome:** A structured RCA process reduces repeat incidents, improves system reliability, and enables continuous improvement across application support, development, infrastructure, and business teams.
