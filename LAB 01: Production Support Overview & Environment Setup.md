# LAB 01: Production Support Overview & Environment Setup

> **Module:** LAB 01

> **Level:** Beginner

> **Estimated Duration:** 30–45 Minutes

---

## Overview

Before handling live production incidents, an **Application Support Engineer** must understand the production landscape, available support tools, and their role within the support chain.

This lab establishes the foundational knowledge required to effectively support a production environment.

---

## Learning Objectives

After completing this lab, you will be able to:

* Understand the BFSI loan application architecture.
* Identify production support tools and required access.
* Set up monitoring dashboards and communication channels.

---

## Prerequisites

Before starting this lab, ensure that you have:

* Required production support onboarding completed.
* Access approval process initiated.
* Corporate email account configured.
* VPN access (if applicable).
* Required permissions for production support tools.

---

# Step-by-Step Tasks

## Step 1.1 – Understand System Architecture

**🎯 Objective**

Review the overall loan processing workflow to understand how customer requests move through the application.

**Application Flow**

```text
Customer Onboarding
        │
        ▼
KYC Verification
        │
        ▼
Document Upload
        │
        ▼
Loan Approval
        │
        ▼
Loan Disbursement
```

> 📌 **Note**
>
> Understanding this workflow is essential for identifying where production issues originate during incident investigation.

---

## Step 1.2 – Identify Application Modules

**🎯 Objective**

Become familiar with the major application modules involved in the loan lifecycle.

### Application Modules

* Loan Origination
* KYC Verification
* Approval Workflow
* Disbursement Engine
* EMI Calculator

> ℹ️ **Information**
>
> Each module may have separate services, logs, databases, monitoring dashboards, and support teams.

---

## Step 1.3 – Access Production Tools

**🎯 Objective**

Obtain the required access credentials for production support activities.

### Required Tools

| Tool Category   | Examples                  |
| --------------- | ------------------------- |
| ITSM Tool       | ServiceNow / Jira         |
| Monitoring Tool | Grafana / Splunk          |
| Database        | Read-only database access |

> 🔒 **Security**
>
> Production database access should always be **read-only** unless explicitly approved through the organization's change management process.

---

## Step 1.4 – Review Runbook & SLA Matrix

**🎯 Objective**

Review the team's operational runbook and understand incident response expectations.

### SLA Matrix

| Priority | Response Time  |
| -------- | -------------- |
| **P1**   | 15 minutes     |
| **P2**   | 1 hour         |
| **P3**   | 4 hours        |
| **P4**   | 1 business day |

> 📌 **Note**
>
> Familiarize yourself with the team's runbook before taking ownership of production incidents.

---

## Step 1.5 – Set Up Alerts & Notifications

**🎯 Objective**

Configure production monitoring alerts to ensure timely notification of critical events.

### Configure Alerts For

* CPU utilization > 80%
* Memory utilization > 85%
* Failed batch jobs
* API error rate > 5%

> 🚨 **Important**
>
> Ensure alerts are delivered through the approved communication channels (email, Slack, or other enterprise notification systems).

---

## Step 1.6 – Join Support Channels

**🎯 Objective**

Connect with the production support communication channels.

### Join the Following Channels

* `#prod-alerts`
* `#incident-bridge`
* `#change-management`

### Additional Task

* Subscribe to the on-call rotation.

> 💬 **Tip**
>
> Staying connected to the correct communication channels helps reduce incident response time.

---

## Step 1.7 – Verify Dashboard Access

**🎯 Objective**

Verify that monitoring dashboards are accessible and displaying production metrics.

### Validate the Following Dashboards

* API Latency Panel
* Error Rate Panel
* Database Connection Pool
* Batch Job Status

> 📊 **Verification**
>
> Confirm that each dashboard is loading successfully and displaying current production metrics.

---

## Step 1.8 – Review Escalation Matrix

**🎯 Objective**

Understand the production support escalation hierarchy.

### Escalation Path

```text
L1 Support
     │
     ▼
L2 Support
     │
     ▼
Development Lead
     │
     ▼
Solution Architect
```

### Key Contacts

* DBA Team
* Infrastructure Team
* Network Team

> ⚠️ **Important**
>
> Know who to contact for database, infrastructure, and network-related issues before handling live production incidents.

---

# ✅ Best Practice Tips

| #     | Best Practice                                                                                                                             |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | Always maintain a personal contact directory with DBA, Infrastructure, Network, and Development Leads for quick escalation.               |
| **2** | Keep **read-only** database access only. Never request DML rights on production databases.                                                |
| **3** | Maintain a **Shift Handover Checklist** that includes open incidents, pending tasks, and ongoing deployments.                             |
| **4** | Bookmark all production monitoring dashboards and keep them open on a secondary monitor during support shifts.                            |
| **5** | Read historical **P1** and **P2** RCA documents to understand recurring production failure patterns before your first live support shift. |

---

# Summary

In this lab, you learned how to:

* Understand the BFSI loan application architecture.
* Identify key production application modules.
* Obtain access to production support tools.
* Review the Runbook and SLA matrix.
* Configure monitoring alerts.
* Join production communication channels.
* Verify monitoring dashboard access.
* Understand the escalation process.
* Apply production support best practices.

---

 
