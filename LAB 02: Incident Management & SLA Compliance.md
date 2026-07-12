# LAB 02: Incident Management & SLA Compliance

> **Module:** LAB 02


> **Level:** Beginner to Intermediate


> **Estimated Duration:** 45–60 Minutes

---

# Overview

Incident Management is the core responsibility of an **Application Support Engineer**. This lab walks through the complete incident lifecycle—from detection to closure—while ensuring compliance with defined **Service Level Agreements (SLAs)**.

Understanding how to manage incidents efficiently helps minimize business impact, maintain system availability, and ensure timely communication with stakeholders.

---

# Learning Objectives

After completing this lab, you will be able to:

* Detect and acknowledge production incidents within SLA.
* Classify incidents using the Priority Matrix.
* Create and manage incident tickets using an ITSM tool.
* Communicate effectively with stakeholders.
* Perform initial production investigations.
* Escalate incidents according to the escalation matrix.
* Validate fixes before closing incidents.
* Conduct post-incident reviews and Root Cause Analysis (RCA).

---

# Scenario

A critical production issue has been reported:

> **Scenario:** Loan disbursement is failing for all customers. The Operations team reports **zero disbursements** in the last **30 minutes**.

Your objective is to manage the incident from detection through resolution while meeting all SLA requirements.

---

# Step-by-Step Tasks

## Step 2.1 – Detect & Acknowledge

**🎯 Objective**

Identify the production alert and acknowledge it within the required SLA response window.

### Actions

* Detect the alert from the monitoring dashboard.
* Acknowledge the incident within the SLA window.
* Record the exact time of detection.

> ⚠️ **Important**
>
> The SLA response timer begins as soon as the incident is detected.

---

## Step 2.2 – Classify Priority

**🎯 Objective**

Determine the appropriate incident priority using the organization's Priority Matrix.

### Evaluation

* **Impact:** High (All users affected)
* **Urgency:** High (Financial impact)

### Result

```text
Impact (High) × Urgency (High)
                │
                ▼
           Priority = P1
```

> 📌 **Note**
>
> Always evaluate **business impact** before assigning the final priority.

---

## Step 2.3 – Create Incident Ticket

**🎯 Objective**

Create an incident in the ITSM platform.

### Ticket Details

| Field      | Value                                |
| ---------- | ------------------------------------ |
| Title      | **Disbursement Failure - All Users** |
| Priority   | **P1**                               |
| Category   | Application                          |
| Assignment | Appropriate Support Team             |

> 📝 **Best Practice**
>
> Use clear, concise titles that immediately communicate the production issue.

---

## Step 2.4 – Notify Stakeholders

**🎯 Objective**

Send an initial incident communication to affected stakeholders.

### Initial Communication

> "We are aware of disbursement failures since **HH:MM**. Investigation is currently underway."

> 📢 **Communication Guideline**
>
> Initial communication should be sent immediately after ticket creation.

---

## Step 2.5 – Investigate Root Cause

**🎯 Objective**

Perform the initial technical investigation.

### Investigation Checklist

* Review application logs for API errors.
* Verify database connectivity and connection timeouts.
* Check infrastructure health:

  * CPU utilization
  * Memory utilization
* Verify recent deployments or configuration changes.

> 🔍 **Investigation Tip**
>
> Start with the most recent changes before investigating historical issues.

---

## Step 2.6 – Escalate if Needed

**🎯 Objective**

Follow the defined escalation process when the incident cannot be resolved within SLA targets.

### Escalation Rules

* If unresolved after **15 minutes**, escalate to **L2 Support**.
* If L2 cannot resolve within **30 minutes**, escalate to the **Development Team**.

```text
L1 Support
     │
15 Minutes
     ▼
L2 Support
     │
30 Minutes
     ▼
Development Team
```

> 🚨 **Critical**
>
> Escalate early rather than risking an SLA breach.

---

## Step 2.7 – Apply Fix & Validate

**🎯 Objective**

Collaborate with technical teams to restore service.

### Activities

* Work with the Development Team and/or DBA.
* Apply the approved fix.
* Validate the solution by:

  * Performing an end-to-end loan disbursement test.
  * Confirming that transactions are processing successfully.

> ✅ **Validation**
>
> Never close an incident without verifying successful business transactions.

---

## Step 2.8 – Close Incident Ticket

**🎯 Objective**

Complete all required documentation before resolving the incident.

### Update the Ticket

Include the following:

* Root Cause
* Fix Applied
* Validation Steps
* Time to Resolve
* Final Status = **Resolved**

> 📄 **Documentation**
>
> Ensure all incident actions and timestamps are accurately recorded.

---

## Step 2.9 – Post-Incident Review

**🎯 Objective**

Conduct a formal Root Cause Analysis (RCA) review.

### Schedule

* Conduct the RCA meeting within **24 hours**.

### Document the Following

* Incident Timeline
* Root Cause Analysis (RCA)
* Business Impact
* Permanent Fix
* Preventive Actions

> 📌 **Note**
>
> The objective of the RCA is continuous improvement—not assigning blame.

---

# SLA Priority Matrix

| Priority          | Impact              | Urgency       | Response Time  | Resolution Time    | Escalation                                |
| ----------------- | ------------------- | ------------- | -------------- | ------------------ | ----------------------------------------- |
| **P1 – Critical** | All Users           | Business Halt | **15 Minutes** | **2 Hours**        | L1 → L2 → Development (within 30 minutes) |
| **P2 – High**     | Department / Module | High          | **30 Minutes** | **4 Hours**        | L1 → L2 (within 1 hour)                   |
| **P3 – Medium**   | Few Users           | Medium        | **2 Hours**    | **8 Hours**        | L1 → L2 (within 4 hours)                  |
| **P4 – Low**      | One User            | Low           | **4 Hours**    | **1 Business Day** | Managed by L1                             |

> 📊 **Reference**
>
> Use this matrix consistently to ensure correct prioritization and SLA compliance.

---

# ✅ Best Practice Tips

| #     | Best Practice                                                                                                                  |
| ----- | ------------------------------------------------------------------------------------------------------------------------------ |
| **1** | Never skip the **Acknowledge** step. Unacknowledged incidents breach SLA even if work has already started.                     |
| **2** | Send stakeholder updates every **15–30 minutes** during a **P1** incident, even if there is no new resolution.                 |
| **3** | Classify incidents based on **business impact first**, followed by urgency. Avoid unnecessarily escalating P3 incidents to P1. |
| **4** | Document every investigation step with accurate timestamps. These records are essential for the RCA report.                    |
| **5** | Use a dedicated **War Room / Bridge Call** for P1 incidents. Avoid managing critical incidents solely through email or chat.   |

---

# Summary

In this lab, you learned how to:

* Detect and acknowledge production incidents.
* Classify incidents using the SLA Priority Matrix.
* Create and manage incident tickets.
* Communicate with stakeholders during outages.
* Perform technical investigations.
* Escalate incidents according to defined procedures.
* Validate production fixes.
* Close incidents with complete documentation.
* Conduct post-incident reviews and Root Cause Analysis (RCA).

---
