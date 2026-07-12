# LAB 04: Log Analysis & Troubleshooting

> **Objective**
> Log analysis is the primary investigative skill of an Application Support Engineer. This lab teaches you how to read, filter, and interpret application logs to diagnose production issues.

---

# 📖 Scenario

Users report that **loan applications are stuck in the *Processing* status**.

Your task is to investigate the issue and determine the root cause by analyzing application, database, and batch logs.

---

# 🛠️ Step-by-Step Tasks

| Step     | Task                             | Details / Command                                                                                                                                                                                        |
| -------- | -------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **4.1**  | **Identify Log Location**        | Locate the required log files:<br><br>**Application Logs**<br>`/var/log/loanapp/application.log`<br><br>**Error Logs**<br>`/var/log/loanapp/error.log`<br><br>**Batch Logs**<br>`/var/log/batch/`        |
| **4.2**  | **Filter by Error Level**        | Search for application errors using the following command:<br><br>`bash grep -i 'ERROR\|EXCEPTION\|FATAL\|WARN' /var/log/loanapp/application.log \| tail -200 `                                          |
| **4.3**  | **Search by Time Window**        | Filter logs for a specific incident time:<br><br>`bash grep '2025-01-15 14:' /var/log/loanapp/application.log \| grep -i error `                                                                         |
| **4.4**  | **Find Specific Loan ID**        | Search logs for a particular loan request:<br><br>`bash grep 'LOAN_ID:LN20250115001' /var/log/loanapp/application.log \| tail -50 `                                                                      |
| **4.5**  | **Identify Exception Type**      | Look for common exceptions, including:<br>- `NullPointerException`<br>- Database Connection Timeout<br>- API Timeout<br>- HTTP 500 Errors<br>- `OutOfMemoryError`                                        |
| **4.6**  | **Check Stack Trace**            | Review the complete stack trace following the exception. Capture the following details before forwarding to the Development team:<br>- Class Name<br>- Method Name<br>- Line Number                      |
| **4.7**  | **Correlate with Database Logs** | Review the database slow query log:<br><br>`text /var/log/mysql/slow-query.log `<br><br>Identify queries taking more than **3 seconds** during the incident window.                                      |
| **4.8**  | **Use ELK / Kibana**             | Execute the following Kibana query:<br><br>`text level:ERROR AND service:loan-origination AND @timestamp:[now-1h TO now] `                                                                               |
| **4.9**  | **Identify Error Patterns**      | Count recurring errors using:<br><br>`bash grep -c 'Connection refused' error.log `<br><br>A high occurrence count typically indicates a systemic issue.                                                 |
| **4.10** | **Document Findings**            | Copy relevant log entries into the incident ticket. Include your technical interpretation and tag the appropriate support teams (Development or DBA) if application code or database fixes are required. |

---

# 🔍 Common Log Patterns & Meanings

The following log patterns are frequently encountered in production environments.

---

## 🌐 API Timeout

**Sample Log**

```text
ERROR 2025-01-15 14:32:11 [LoanService]
API call to /disburse timed out after 30000ms
```

**Meaning**

The downstream API did not respond within the configured timeout period.

💡 **Recommended Action**

* Verify downstream bank API availability.
* Check network connectivity.
* Review API response latency.

---

## 🗄️ Database Connection Failure

**Sample Log**

```text
ERROR 2025-01-15 14:32:15 [DBPool]
Cannot get connection, pool exhausted (max: 50, active: 50)
```

**Meaning**

The database connection pool has reached its maximum capacity.

⚠️ **Recommended Action**

* Alert the DBA team.
* Investigate long-running database queries.
* Check for connection leaks.

---

## 🔄 Workflow Stuck

**Sample Log**

```text
WARN 2025-01-15 14:31:00 [WorkflowEngine]
Loan LN001 stuck in PENDING_APPROVAL for >60 min
```

**Meaning**

The workflow engine has not progressed the loan application.

💡 **Recommended Action**

* Verify the approval queue.
* Confirm reviewer availability.
* Review workflow configuration.

---

## 💥 Out of Memory (OOM) Error

**Sample Log**

```text
FATAL 2025-01-15 14:30:55 [JVM]
java.lang.OutOfMemoryError: Java heap space
```

**Meaning**

The JVM has exhausted the allocated Java heap memory.

🚨 **Recommended Action**

* Restart the application server.
* Notify the Infrastructure team.
* Evaluate increasing the JVM heap size.

---

## 📦 Batch Job Failure

**Sample Log**

```text
ERROR 2025-01-15 02:00:15 [BatchRunner]
Job EMI_GENERATION failed:
DataIntegrityViolationException
```

**Meaning**

The scheduled EMI generation batch job failed due to a data integrity issue.

💡 **Recommended Action**

* Verify EMI table data.
* Notify the DBA team.
* Correct the data and rerun the batch job.

---

# 💡 Best Practice Tips

> **Follow these recommendations to improve investigation speed and accuracy during production incidents.**

| #     | Best Practice                                                                                                                                                                                                                                                         |
| ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | ✅ Always narrow your log search using a specific **time window** first. Searching entire log files during an incident significantly increases investigation time.                                                                                                     |
| **2** | 🛠️ Learn the five essential `grep` options:<br><br>- `-i` → Case-insensitive search<br>- `-c` → Count matching lines<br>- `-A 10` → Display 10 lines after the match<br>- `-B 5` → Display 5 lines before the match<br>- `-E` → Extended regular expressions (Regex) |
| **3** | 🔒 Never modify production log files. Maintain **read-only access**. Log tampering is a compliance violation in BFSI environments.                                                                                                                                    |
| **4** | 🔍 Correlate application logs, database logs, and server logs together. Single-source log analysis often misses the complete root cause.                                                                                                                              |
| **5** | 📋 Save relevant log snippets to the incident ticket immediately. Production logs rotate, and valuable evidence may be lost over time.                                                                                                                                |
| **6** | 📚 Learn how to interpret Java and Python stack traces. In most cases, the actual root cause appears on the **first line immediately following** `Caused by:`.                                                                                                        |

---

# 📌 Summary

During this lab, you learned how to:

* Locate production application logs.
* Filter logs by severity, timestamp, and transaction identifier.
* Identify common exception types.
* Analyze Java stack traces.
* Correlate application logs with database logs.
* Use Kibana to investigate production incidents.
* Detect recurring error patterns.
* Document technical findings in incident tickets.
* Apply production log analysis best practices.

> **Outcome:** Effective log analysis enables faster root cause identification, reduces Mean Time to Resolution (MTTR), and improves production support efficiency.
