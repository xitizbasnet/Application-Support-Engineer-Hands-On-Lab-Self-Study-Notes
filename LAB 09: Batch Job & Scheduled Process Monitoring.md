# LAB 09: Batch Job & Scheduled Process Monitoring

> **Objective**
> BFSI applications rely heavily on scheduled batch processes for critical business operations such as EMI generation, payment posting, loan status synchronization, and regulatory reporting.
>
> Missed or failed batch jobs can create cascading business issues across multiple systems and customer-facing processes.

---

# 📖 Scenario

The Operations team reports:

> **"EMI statements were not sent to customers today."**

Your task is to investigate the batch job failure, identify the cause, recover the process, and ensure successful completion.

---

# 🛠️ Step-by-Step Tasks

| Step     | Task                                | Details                                                                                                                                                                                 |
| -------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **9.1**  | **Check Job Scheduler Dashboard**   | Open the batch scheduler dashboard:<br><br>- Control-M<br>- Autosys<br>- Quartz<br><br>Filter jobs by today's date and identify jobs with status:<br><br>- **FAILED**<br>- **ABENDED**  |
| **9.2**  | **Identify the Failed Job**         | Failed Job Details:<br><br>**Job Name:** `EMI_STATEMENT_GEN`<br>**Status:** FAILED<br>**Start Time:** 02:00 AM<br>**End Time:** 02:07 AM<br>**Exit Code:** 9                            |
| **9.3**  | **Review Job Execution Log**        | Review the batch execution log:<br><br>`bash tail -500 /var/log/batch/emi_statement_gen_20250115.log \| grep -i 'ERROR\|FAIL\|EXIT' `                                                   |
| **9.4**  | **Check Job Dependencies**          | Verify that all upstream jobs completed successfully:<br><br>Example:<br><br>`LOAN_STATUS_SYNC` must complete before `EMI_STATEMENT_GEN` starts.                                        |
| **9.5**  | **Identify Failure Cause**          | Common batch failure causes include:<br><br>- Data issue (NULL value in mandatory field)<br>- Database timeout<br>- Disk full<br>- Dependency job failure<br>- Application/system error |
| **9.6**  | **Validate Data Fix (If Required)** | If the failure is caused by incorrect data:<br><br>- Coordinate with DBA team to correct data.<br>- Validate the fix using `SELECT` queries before restarting the job.                  |
| **9.7**  | **Re-run the Failed Job**           | Review the job restart procedure in the runbook.<br><br>Restart from the failure point instead of the beginning if restart functionality is supported.                                  |
| **9.8**  | **Validate Job Completion**         | After restart, verify:<br><br>- Job Status = **COMPLETED**<br>- EMI statements generated successfully<br>- Customer emails sent<br>- Database records updated correctly                 |
| **9.9**  | **Notify Business Team**            | Inform Operations:<br><br>`EMI statements re-processed at HH:MM. Customers will receive statements within the expected timeframe.`                                                      |
| **9.10** | **Document & Raise Problem Record** | If the issue is recurring:<br><br>- Create a Problem ticket.<br>- Tag recurring batch failures.<br>- Track permanent corrective actions.                                                |

---

# 📊 Critical Batch Jobs in BFSI Loan Processing

| Job Name               | Schedule           | Purpose                                | Impact if Failed                             |
| ---------------------- | ------------------ | -------------------------------------- | -------------------------------------------- |
| **LOAN_STATUS_SYNC**   | Every 2 hours      | Synchronize loan status across modules | Users may see stale or incorrect loan status |
| **EMI_GENERATION**     | 1st of month 01:00 | Generate EMI due records               | EMI deductions may not occur for the month   |
| **PAYMENT_POSTING**    | Daily 06:00        | Post collected payments to ledger      | Payments may appear unpaid in the system     |
| **NOTIFICATION_JOB**   | Daily 08:00        | Send EMI reminders to customers        | Customers do not receive due date reminders  |
| **REPORT_GEN_EOD**     | Daily 23:30        | Generate MIS and regulatory reports    | Compliance reports may be missing            |
| **NPA_CLASSIFICATION** | Daily 00:00        | Mark overdue loans as NPA              | NPA accounts may not be identified correctly |

---

# 💡 Best Practice Tips

> **Follow these batch monitoring practices to prevent operational failures and reduce business impact.**

| #     | Best Practice                                                                                                                                                  |
| ----- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | 🌅 Check **all batch jobs** at the start of every morning shift. Missed overnight failures are a common source of high-priority incidents.                     |
| **2** | 🔗 Always verify batch job dependency chains. A failed upstream job can silently prevent downstream jobs from executing.                                       |
| **3** | ⚠️ Never restart a batch job without validating the data state first. Restarting with incorrect data can create duplicate records or inconsistent results.     |
| **4** | 📅 Maintain a batch job calendar, especially for month-end and year-end processing. Business-critical jobs require additional monitoring during these periods. |
| **5** | 🔍 For partial failures, always verify **how many records were processed**. Partial success can sometimes be more dangerous than a complete failure.           |

---

# 📌 Summary

During this lab, you learned how to:

* Monitor scheduled batch processes.
* Identify failed and abended jobs.
* Analyze batch execution logs.
* Validate job dependencies.
* Identify common batch failure causes.
* Perform controlled job recovery.
* Validate successful batch completion.
* Communicate recovery status to business teams.
* Create problem records for recurring failures.

> **Outcome:** Effective batch monitoring ensures reliable business operations, prevents data inconsistencies, and reduces customer impact caused by failed scheduled processes.
