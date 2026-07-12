# LAB 11: Data Mismatch Investigation & Resolution

> **Objective**
> Data mismatches in BFSI loan systems can create serious customer experience, financial, and compliance issues.
>
> This lab covers the systematic investigation and resolution of data discrepancies across:
>
> * Loan tables
> * Payment tables
> * EMI tables
> * Document management tables

---

# 📖 Scenario

A customer contacts support:

> **"I paid my EMI 3 days ago, but the application still shows the payment as due. My CIBIL score may be affected."**

Your task is to investigate the mismatch, identify the root cause, validate the data, and coordinate resolution.

---

# 🛠️ Step-by-Step Tasks

| Step      | Task                                    | Details                                                                                                                                                                                |
| --------- | --------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **11.1**  | **Gather Customer Details**             | Collect complete customer information:<br><br>- Customer ID<br>- Loan ID<br>- Payment Date<br>- Payment Amount<br>- Payment Mode (NEFT / UPI / eNACH)<br>- Bank Reference Number       |
| **11.2**  | **Verify Payment in Transaction Table** | Query the `payment_transactions` table.<br><br>Verify:<br>- Transaction exists<br>- Transaction status (`SUCCESS` / `FAILED` / `PENDING` / `PROCESSING`)                               |
| **11.3**  | **Check EMI Schedule Status**           | Query the `emi_schedule` table.<br><br>Confirm whether the EMI is still showing as **UNPAID** even though a payment transaction exists.                                                |
| **11.4**  | **Identify Mismatch Type**              | Determine the mismatch category:<br><br>- Payment exists but EMI status not updated<br>- Payment SUCCESS but bank reversal occurred<br>- Payment stuck in PROCESSING status            |
| **11.5**  | **Check Payment Reconciliation Job**    | Review reconciliation job execution logs.<br><br>Verify:<br>- Did `PAYMENT_POSTING` job run today?<br>- Was this specific transaction processed successfully?                          |
| **11.6**  | **Verify Bank Confirmation**            | Check bank API response logs using the bank reference number.<br><br>Confirm whether money was actually transferred successfully.                                                      |
| **11.7**  | **Check for Duplicate Transactions**    | Search for possible duplicate transactions:<br><br>Criteria:<br>- Same amount<br>- Same payment date<br>- Same loan ID<br><br>Identify double debit or duplicate processing scenarios. |
| **11.8**  | **Identify Resolution Path**            | Select appropriate resolution:<br><br>**Option A:** Trigger manual EMI update if payment is confirmed.<br><br>**Option B:** Raise issue to Development team for reconciliation fix.    |
| **11.9**  | **Coordinate with DBA**                 | DBA performs approved database updates to mark EMI as paid after all validations are completed.<br><br>⚠️ Never perform financial data updates directly.                               |
| **11.10** | **Communicate Resolution**              | Update customer ticket:<br><br>- Confirm resolution.<br>- Document investigation details.<br>- Inform customer:<br>`Advise customer to re-check CIBIL after 72 hours.`                 |

---

# 📊 Data Mismatch Types & Resolution

| Mismatch Type              | Symptom                                                       | Likely Cause                                     | Resolution                                         |
| -------------------------- | ------------------------------------------------------------- | ------------------------------------------------ | -------------------------------------------------- |
| **Payment / EMI Mismatch** | Payment shows **SUCCESS**, but EMI shows **UNPAID**           | Payment reconciliation job failed                | Re-run `PAYMENT_POSTING` job                       |
| **Status Sync Issue**      | Application shows old status after update                     | Cache not refreshed or synchronization job delay | Clear cache or wait for next synchronization cycle |
| **Document Mismatch**      | Documents uploaded but verification shows **PENDING**         | Document service delay or configuration issue    | Manually trigger document verification             |
| **Disbursement Mismatch**  | Loan shows **DISBURSED**, but customer has not received money | Bank API failure after status update             | Verify bank confirmation and raise urgent ticket   |
| **Duplicate Transaction**  | Customer charged twice for the same EMI                       | Duplicate click or network retry issue           | Confirm with bank and initiate refund process      |

---

# 💡 Best Practice Tips

> **Follow these practices when investigating BFSI financial data issues.**

| #     | Best Practice                                                                                                                                                 |
| ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | 🔒 **NEVER manually update financial data in production.** Always route database changes through DBA teams with proper approval and change management.        |
| **2** | 🏦 Always obtain bank confirmation using the bank reference number before marking a payment as successful in the system.                                      |
| **3** | 🚨 Treat EMI data mismatches as **P2 priority minimum**. BFSI data errors can directly impact customer CIBIL scores and regulatory compliance.                |
| **4** | 📸 Document every data mismatch investigation with screenshots of SQL query results. Audit teams require evidence of validation activities.                   |
| **5** | 🔍 Determine whether the mismatch affects:<br><br>- A single customer → Isolated issue<br>- Multiple customers → Possible systemic issue requiring escalation |

---

# 📌 Investigation Checklist

Use this checklist during a data mismatch investigation:

| Check                                    | Completed |
| ---------------------------------------- | --------- |
| Customer and loan details collected      | ☐         |
| Payment transaction verified             | ☐         |
| EMI schedule checked                     | ☐         |
| Mismatch type identified                 | ☐         |
| Reconciliation job validated             | ☐         |
| Bank confirmation verified               | ☐         |
| Duplicate transaction checked            | ☐         |
| DBA coordination completed (if required) | ☐         |
| Customer communication completed         | ☐         |
| Evidence attached to ticket              | ☐         |

---

# 📌 Summary

During this lab, you learned how to:

* Investigate payment and EMI mismatches.
* Validate backend transaction records.
* Analyze reconciliation failures.
* Verify bank transaction confirmations.
* Identify duplicate payments.
* Coordinate with DBA and Development teams.
* Resolve customer-impacting financial data issues.
* Maintain audit-ready investigation records.

> **Outcome:** A structured data mismatch investigation process protects customer records, prevents compliance issues, improves financial accuracy, and enables faster resolution of BFSI production incidents.
