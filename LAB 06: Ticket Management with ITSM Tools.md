# LAB 06: Ticket Management with ITSM Tools

> **Objective**
> Effective ticket management ensures that every issue is tracked, prioritized, escalated, and resolved with full accountability. This lab covers the end-to-end lifecycle of support tickets using ITSM tools such as **ServiceNow** or **Jira Service Management**.

---

# 📖 Scenario

You receive **three simultaneous support tickets**:

* 🔴 **P2** – API Failure
* 🟡 **P3** – Data Query
* 🔵 **P4** – Report Request

Your task is to prioritize, manage, escalate, and resolve these tickets according to ITSM best practices.

---

# 🛠️ Step-by-Step Tasks

| Step     | Task                           | Details                                                                                                                                                                                                             |
| -------- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **6.1**  | **Triage Incoming Tickets**    | Review all newly created tickets and prioritize them.<br><br>- **P1 / P2** → Immediate action<br>- **P3** → Queue for investigation<br>- **P4** → Schedule for completion                                           |
| **6.2**  | **Create an Incident Ticket**  | Create a new **Incident** and complete the required fields:<br><br>- Short Description<br>- Category (Application / Network / Database)<br>- Priority<br>- Affected Service                                         |
| **6.3**  | **Assign & Own the Ticket**    | Assign the incident to yourself or the appropriate support team. Update the status to **In Progress** and record work notes, for example:<br><br>`Investigating API failure on /loan-...`                           |
| **6.4**  | **Update Ticket in Real Time** | For **P1/P2 incidents**, add work notes every **15 minutes**, including:<br><br>- Timestamp<br>- Findings<br>- Actions Taken<br>- Teams or Individuals Engaged                                                      |
| **6.5**  | **Escalate Using the Ticket**  | Reassign the ticket to the appropriate **L2**, **Development**, or **DBA** team when required. Include an escalation note, for example:<br><br>`Escalating to Development – Database connection pool exhausted.`    |
| **6.6**  | **Link Related Tickets**       | Use the **Related Tickets** feature to associate duplicate incidents with the primary ticket. Mark duplicate incidents as **Duplicate of** the parent ticket.                                                       |
| **6.7**  | **Create a Service Request**   | For data queries and report requests, create a **Service Request** instead of an Incident. Assign the appropriate SLA based on **P3/P4** priority and route it to the responsible team.                             |
| **6.8**  | **Create a Problem Record**    | For recurring incidents, create a **Problem** record. Link all associated incidents and assign the problem to the **Problem Manager** for Root Cause Analysis (RCA).                                                |
| **6.9**  | **Close the Ticket Properly**  | Before closure, complete the following fields:<br><br>- Resolution Code<br>- Resolution Notes<br>- Close Code (Resolved / Workaround / Not Reproducible)<br><br>Obtain user confirmation before closing the ticket. |
| **6.10** | **Generate Ticket Report**     | At the end of the shift, export a ticket summary showing:<br><br>- Tickets Opened<br>- Tickets Closed<br>- SLA Breaches<br>- Escalated Tickets<br><br>Share the report with the team.                               |

---

# 🔄 Ticket Lifecycle Stages

| Stage         | Status      | Owner                  | Required Action                                                            |
| ------------- | ----------- | ---------------------- | -------------------------------------------------------------------------- |
| **New**       | Open        | Queue / Unassigned     | Pick up the ticket within the defined SLA response time.                   |
| **Assigned**  | In Progress | L1 Support Engineer    | Investigate the issue and continuously update work notes.                  |
| **Pending**   | On Hold     | L1 Support Engineer    | Await additional information from the user or another support team.        |
| **Escalated** | In Progress | L2 / Development / DBA | Perform advanced investigation and implement the required fix.             |
| **Resolved**  | Resolved    | L1 Support Engineer    | Verify the solution and await user confirmation.                           |
| **Closed**    | Closed      | System / Manager       | Automatically close after three days or once the user confirms resolution. |

---

# 💡 Best Practice Tips

> **Follow these ITSM best practices to improve ticket quality, SLA compliance, and customer communication.**

| #     | Best Practice                                                                                                                                  |
| ----- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | ✅ Never close a **P1** or **P2** ticket without obtaining user confirmation. Premature closure is considered an SLA compliance violation.      |
| **2** | 📝 Use **Work Notes** for internal technical updates and **Additional Comments** for customer-facing communication.                            |
| **3** | ⏱️ Never leave a ticket in the **New** state for more than **5 minutes**. Unacknowledged tickets may breach SLA response targets.              |
| **4** | 🔗 Link duplicate incidents to a parent ticket. This prevents multiple teams from investigating the same issue and improves incident tracking. |
| **5** | 📞 Record every phone conversation in the ticket work notes.<br><br>Example:<br>`Call with John at 14:30 – User confirmed issue resolved.`     |

---

# 📌 Summary

During this lab, you learned how to:

* Prioritize and triage incoming support tickets.
* Create and manage incidents.
* Assign ticket ownership.
* Record investigation progress using work notes.
* Escalate tickets to the appropriate support teams.
* Link duplicate incidents.
* Create service requests and problem records.
* Close tickets correctly with proper documentation.
* Generate end-of-shift ticket reports.

> **Outcome:** Effective ticket management ensures SLA compliance, improves communication across support teams, provides complete audit trails, and enables timely resolution of production issues.
