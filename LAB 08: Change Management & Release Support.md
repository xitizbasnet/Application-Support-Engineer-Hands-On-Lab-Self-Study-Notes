# LAB 08: Change Management & Release Support

> **Objective**
> Every production change carries risk. Change management ensures that changes are **planned, tested, approved, deployed, and monitored** in a controlled manner.
>
> This lab covers the complete change lifecycle and post-release validation activities.

---

# 📖 Scenario

A **hotfix for the EMI calculation bug** is scheduled for deployment at **11 PM**.

You are the **Application Support Engineer on duty** and must support the release process, validate the deployment, and monitor production health after the change.

---

# 🛠️ Step-by-Step Tasks

| Step     | Task                                  | Details                                                                                                                                                                                                          |
| -------- | ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **8.1**  | **Review Change Request (CR)**        | Review the Change Request details:<br><br>- What is changing<br>- Why the change is required<br>- Risk level<br>- Rollback plan<br>- Testing completed<br>- Approvals received                                   |
| **8.2**  | **Attend Pre-Change CAB Meeting**     | Participate in the **Change Advisory Board (CAB)** meeting:<br><br>- Validate risk assessment.<br>- Confirm maintenance window.<br>- Approve or reject the change.                                               |
| **8.3**  | **Prepare Pre-Deployment Checklist**  | Complete pre-deployment preparation:<br><br>- Backup configuration.<br>- Record current application version.<br>- Verify rollback steps.<br>- Inform the on-call team.<br>- Confirm test environment validation. |
| **8.4**  | **Perform Pre-Deployment Baseline**   | Capture current production health metrics:<br><br>- API error rate<br>- API response time<br>- Database connection count<br>- Active users<br>- Batch job status                                                 |
| **8.5**  | **Support Deployment Team**           | Stay connected on the deployment bridge call.<br><br>- Monitor alerts in real time.<br>- Record the exact deployment start time.                                                                                 |
| **8.6**  | **Execute Smoke Testing**             | After deployment, test critical business flows:<br><br>- Loan Application Submission<br>- KYC Submission<br>- EMI View<br>- Repayment Processing<br><br>Verify that key APIs are functioning correctly.          |
| **8.7**  | **Perform Sanity Testing**            | Test additional business scenarios:<br><br>- Maximum loan amount<br>- Partial payment<br>- Document re-upload<br>- Overdue EMI scenario                                                                          |
| **8.8**  | **Post-Release Monitoring (2 Hours)** | Monitor production after deployment for:<br><br>- New error patterns<br>- Response time spikes<br>- Database errors<br>- Failed transactions<br>- Batch job failures                                             |
| **8.9**  | **Production Health Check**           | Perform a health validation **30 minutes after deployment**:<br><br>- Compare metrics against pre-deployment baseline.<br>- Confirm no service degradation.                                                      |
| **8.10** | **Close Change Record**               | Update the Change Request with:<br><br>- Actual deployment time<br>- Issues identified<br>- Smoke test results<br>- Final sign-off<br><br>Update status to **Completed**.                                        |

---

# ✅ Smoke Test Checklist — Post Deployment

| Test Case                   | Module            | Expected Result                                          | Pass/Fail |
| --------------------------- | ----------------- | -------------------------------------------------------- | --------- |
| Submit new loan application | Loan Origination  | Application ID generated and status = **SUBMITTED**      | ☐         |
| Upload KYC documents        | KYC Module        | Documents uploaded and status = **UNDER_REVIEW**         | ☐         |
| Check loan approval status  | Approval Workflow | Current workflow stage displayed correctly               | ☐         |
| View EMI schedule           | EMI Module        | All EMI records displayed with correct amounts and dates | ☐         |
| Make EMI payment            | Repayment         | Payment accepted, status = **PAID**, balance updated     | ☐         |
| Check disbursement status   | Disbursement      | Disbursement record displayed with bank reference number | ☐         |
| Generate account statement  | Reporting         | Statement downloaded successfully as PDF without errors  | ☐         |

---

# 💡 Best Practice Tips

> **Follow these release management practices to reduce deployment risk and maintain production stability.**

| #     | Best Practice                                                                                                                                       |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | 🔄 Always maintain a clear rollback plan before deployment. If smoke tests fail, rollback must be initiated within **15 minutes**.                  |
| **2** | 📊 Capture a complete pre-deployment baseline of key metrics. This provides a comparison point to identify impact or confirm no degradation.        |
| **3** | 🕙 Schedule deployments during low-traffic windows:<br><br>- Weekday late nights: **10 PM – 2 AM**<br>- Sunday mornings for BFSI systems            |
| **4** | 🚫 Never combine multiple changes in a single release window. Perform one change per deployment to simplify rollback isolation and troubleshooting. |
| **5** | 👀 Continue post-deployment monitoring for a minimum of **2 hours**. Most deployment-related issues appear within the first **60–90 minutes**.      |

---

# 📌 Summary

During this lab, you learned how to:

* Review and validate Change Requests.
* Participate in CAB approval processes.
* Prepare deployment checklists.
* Capture production baselines.
* Support deployment activities.
* Perform smoke and sanity testing.
* Monitor post-release application health.
* Validate production stability.
* Complete and close change records.

> **Outcome:** Effective change management reduces production risk, improves release reliability, and ensures controlled delivery of application enhancements and fixes.
