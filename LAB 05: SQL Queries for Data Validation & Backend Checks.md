# LAB 05: SQL Queries for Data Validation & Backend Checks

> **Objective**
> SQL is a critical skill for verifying loan application data, investigating mismatches, validating backend records, and performing reconciliation without touching the application layer.

---

# 📖 Scenario

A customer reports that their **EMI has been deducted**, but the **loan status still shows as *Overdue***.

Your task is to validate the backend data using SQL queries and identify any inconsistencies.

---

# 🛠️ Step-by-Step Tasks

| Step    | Task                               | Details                                                                                                                        |
| ------- | ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| **5.1** | **Verify Customer Record**         | Check whether the customer exists, verify that KYC is complete, and confirm the account status is **ACTIVE**.                  |
| **5.2** | **Check Loan Application Status**  | Verify the loan record, including status, disbursement date, loan amount, and assigned Relationship Manager (RM).              |
| **5.3** | **Verify EMI Schedule**            | Review all EMI installments, including due dates, installment amounts, payment status, and payment dates.                      |
| **5.4** | **Validate Payment Transaction**   | Search the payment transaction table for recent payments associated with the loan.                                             |
| **5.5** | **Check for Reconciliation Issue** | Compare the number of paid EMI records with successful payment transactions. Any mismatch may indicate a reconciliation issue. |
| **5.6** | **Verify Workflow Status**         | Determine whether the loan is stuck in a workflow stage due to a processing error.                                             |
| **5.7** | **Validate Document Status**       | Confirm that all required documents have been uploaded and successfully verified.                                              |
| **5.8** | **Cross-check Disbursement**       | Verify the disbursement record, including amount, beneficiary bank account, and transfer status.                               |

---

# 💻 Key SQL Queries Used in Production Support

## 5.1 Verify Customer Record

```sql
SELECT
    customer_id,
    name,
    mobile,
    email,
    kyc_status,
    account_status,
    created_date
FROM customers
WHERE customer_id = 'CUST123456';
```

> ℹ️ **Purpose**
> Confirms the customer exists, KYC is complete, and the account is active.

---

## 5.2 Check Loan Application Status

```sql
SELECT
    loan_id,
    customer_id,
    loan_amount,
    status,
    disburse_date,
    emi_start_date,
    tenure_months,
    interest_rate,
    assigned_rm
FROM loan_applications
WHERE customer_id = 'CUST123456'
ORDER BY created_date DESC;
```

> ℹ️ **Purpose**
> Validates the current loan application status and associated loan details.

---

## 5.3 Verify EMI Schedule

```sql
SELECT
    emi_no,
    due_date,
    emi_amount,
    paid_amount,
    payment_date,
    status
FROM emi_schedule
WHERE loan_id = 'LN20250115001'
ORDER BY emi_no;
```

> ℹ️ **Purpose**
> Reviews the complete EMI schedule and payment history.

---

## 5.4 Validate Payment Transaction

```sql
SELECT
    txn_id,
    loan_id,
    amount,
    payment_mode,
    payment_date,
    status,
    bank_ref_no
FROM payment_transactions
WHERE loan_id = 'LN20250115001'
  AND payment_date >= '2025-01-01'
ORDER BY payment_date DESC;
```

> ℹ️ **Purpose**
> Confirms that payment transactions were successfully recorded.

---

## 5.5 Reconciliation Check

```sql
SELECT
(
    SELECT COUNT(*)
    FROM emi_schedule
    WHERE loan_id = 'LN20250115001'
      AND status = 'PAID'
) AS emi_paid_count,

(
    SELECT COUNT(*)
    FROM payment_transactions
    WHERE loan_id = 'LN20250115001'
      AND status = 'SUCCESS'
) AS txn_count;
```

> ⚠️ **Validation Rule**
> If **EMI Paid Count** and **Successful Transaction Count** do not match, a reconciliation issue may exist.

---

## 5.6 Check Workflow Status

```sql
SELECT
    loan_id,
    current_stage,
    stage_status,
    last_updated,
    error_message
FROM workflow_tracker
WHERE loan_id = 'LN20250115001';
```

> ℹ️ **Purpose**
> Determines whether the loan application is stalled within the workflow engine.

---

## 5.7 Document Verification Status

```sql
SELECT
    doc_type,
    upload_date,
    verification_status,
    verified_by,
    rejection_reason
FROM loan_documents
WHERE loan_id = 'LN20250115001';
```

> ℹ️ **Purpose**
> Verifies that all required loan documents have been uploaded and approved.

---

## 5.8 Disbursement Record

```sql
SELECT
    disburse_id,
    loan_id,
    amount,
    beneficiary_account,
    ifsc_code,
    transfer_status,
    transfer_date,
    bank_ref_no
FROM disbursements
WHERE loan_id = 'LN20250115001';
```

> ℹ️ **Purpose**
> Validates that loan disbursement was successfully processed.

---

# 💡 Best Practice Tips

> **Follow these best practices when executing SQL queries in a production environment.**

| #     | Best Practice                                                                                                                                                                                                     |
| ----- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | 🔒 **Always use `SELECT` statements only.** Never execute `UPDATE`, `DELETE`, or `INSERT` statements in production without DBA approval and an approved change request.                                           |
| **2** | ⚠️ Always include a `WHERE` clause using specific identifiers. Running queries without filters may result in full table scans and can negatively impact production performance.                                   |
| **3** | 📌 When exploring data, use a `LIMIT` clause to prevent unnecessary database load.<br><br>Example:<br>`sql SELECT * FROM payment_transactions LIMIT 100; `                                                        |
| **4** | ⏰ Whenever possible, execute complex queries during low-traffic periods. Large joins and expensive queries can increase database load.                                                                            |
| **5** | 📚 Maintain a personal query library (Notepad, Wiki, or Knowledge Base) containing validated production SQL queries for common support scenarios.                                                                 |
| **6** | ✅ Always cross-reference related tables. If one table shows **PAID** while another shows **PENDING**, this indicates a data inconsistency and should be raised to the appropriate support team for investigation. |

---

# 📌 Summary

During this lab, you learned how to:

* Validate customer information.
* Verify loan application details.
* Review EMI schedules.
* Confirm payment transactions.
* Identify reconciliation mismatches.
* Check workflow processing status.
* Validate document verification.
* Confirm loan disbursement records.
* Apply SQL best practices for production support.

> **Outcome:** Effective SQL validation enables Application Support Engineers to quickly identify backend data inconsistencies, perform accurate production investigations, and reduce incident resolution time while maintaining production database integrity.
