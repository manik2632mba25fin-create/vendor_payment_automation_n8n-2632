# Financial Risk Monitoring & Approval Workflow (n8n)

## Overview

This project automates the identification, review, approval, and notification of high-risk financial transactions using **n8n**, **Google Sheets**, **Gmail**, and AI-driven risk assessment rules.

The workflow monitors invoice transactions stored in Google Sheets, evaluates risk levels based on predefined business rules, sends approval notifications to the appropriate stakeholders, and updates transaction statuses automatically.

---

## Features

* Automated transaction risk assessment
* Multi-level approval workflow
* Gmail notifications for reviewers and approvers
* Google Sheets integration for transaction management
* Duplicate transaction detection
* AI-generated risk insights
* Automatic status updates after review
* Finance Manager, Finance Head, and CFO approval routing

---

## Workflow Architecture

### 1. Trigger

* Manual execution using **Execute Workflow**
* Can be converted to scheduled execution using Cron Trigger

### 2. Read Transactions

* Fetch invoice records from Google Sheets
* Read transaction details including:

  * Invoice ID
  * Vendor Name
  * Department
  * Amount
  * GST Number
  * Payment Mode
  * Duplicate Check
  * Risk Flag
  * Approval Level

### 3. Risk Evaluation

Transactions are categorized into:

| Risk Level      | Criteria                            |
| --------------- | ----------------------------------- |
| Normal          | Standard transaction                |
| Review Required | Medium-risk transaction             |
| High Risk       | Large-value transaction             |
| Fraud/Review    | Duplicate or suspicious transaction |

---

### 4. Approval Routing

#### Finance Manager Approval

Triggered for:

* Review Required transactions
* Medium-risk invoices

Email Subject:

```
Medium Risk Review – Finance Manager Verification Required
```

#### Finance Head Approval

Triggered for:

* Fraud/Review transactions
* Suspicious activities

Email Subject:

```
Fraud Review Alert – Finance Head Verification Required
```

#### CFO Approval

Triggered for:

* High-value transactions
* High-risk invoices

Email Subject:

```
Financial Risk Alert – CFO Approval Required
```

---

## Email Templates

### High Risk Alert

Includes:

* Invoice ID
* Vendor Name
* Department
* Amount
* Risk Status
* AI Insight

Example:

> AI monitoring detected a high-value transaction requiring CFO approval.

---

### Medium Risk Review

Includes:

* Invoice Information
* Department
* Amount
* Risk Status
* AI-generated recommendation

Example:

> Medium-risk transaction requires finance review.

---

## Google Sheet Structure

| Column          | Description                      |
| --------------- | -------------------------------- |
| Invoice ID      | Unique invoice number            |
| Vendor Name     | Vendor details                   |
| Amount          | Invoice amount                   |
| Due Date        | Payment due date                 |
| Department      | Business unit                    |
| GST Number      | Tax identification               |
| Payment Mode    | UPI, Bank Transfer, Cheque, etc. |
| Status          | Current workflow status          |
| Risk Flag       | Risk classification              |
| Duplicate Check | Duplicate detection result       |
| Approval Level  | Required approver                |
| Company ID      | Organization identifier          |

---

## Workflow Logic

```text
Read Google Sheet
        │
        ▼
   Evaluate Risk
        │
 ┌──────┼──────┐
 ▼      ▼      ▼
Medium High  Fraud
Risk   Risk  Review
 │      │      │
 ▼      ▼      ▼
Finance CFO Finance
Manager      Head
Approval     Review
 │      │      │
 ▼      ▼      ▼
Send Email Notifications
 │
 ▼
Update Google Sheet Status
```

---

## Status Updates

After notification:

| Risk Type    | Updated Status      |
| ------------ | ------------------- |
| Medium Risk  | Review Required     |
| High Risk    | CFO Approval        |
| Fraud Review | Finance Head Review |
| Approved     | Payment Approved    |
| Rejected     | Payment On Hold     |

---

## Technology Stack

* **n8n** – Workflow Automation
* **Google Sheets** – Transaction Database
* **Gmail** – Email Notifications
* **AI Rules Engine** – Risk Assessment Logic

---

## Business Benefits

* Reduces manual review effort
* Improves financial governance
* Detects duplicate and suspicious payments
* Accelerates approval processes
* Maintains audit-ready transaction records
* Enhances compliance and risk management

---

## Future Enhancements

* Integration with ERP systems (SAP, Oracle, NetSuite)
* Slack / Microsoft Teams notifications
* AI anomaly detection using transaction history
* Approval dashboard
* Real-time monitoring and reporting
* Automated payment release after approval

---


