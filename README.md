# 📊 Accounting & Internal Controls Automation

An automated accounting control and exception-monitoring framework built with **Excel and Power Query** using synthetic SAP-style financial data.

The project demonstrates how repetitive accounting checks can be transformed into a refreshable control workflow covering **General Ledger validation, internal controls, period-end review, and selected IFRS-oriented accounting scenarios**.

---

## 🎯 Project Objective

Accounting teams routinely perform controls such as:

- checking whether journal entries balance,
- validating GL accounts and cost centers,
- identifying duplicate postings,
- reviewing segregation of duties,
- investigating unusual transactions,
- reviewing period-end postings,
- and performing accounting-specific valuation and recognition checks.

Performing these checks manually becomes time-consuming as transaction volumes increase.

This project creates an automated workflow:

**Source Data → Power Query → Accounting Controls → Exception Reports → Control Summary → Excel Dashboard**

The objective is to identify transactions requiring review while providing a concise management-level overview of control results.

---

## 🏗️ Solution Architecture

```text
Synthetic SAP-Style Data
        │
        ▼
┌──────────────────────┐
│     Power Query      │
│  Data Transformation │
└──────────┬───────────┘
           │
           ▼
┌──────────────────────────────┐
│ Automated Accounting Controls│
│                              │
│ • Debit / Credit             │
│ • GL Accounts                │
│ • Cost Centers               │
│ • Segregation of Duties      │
│ • Duplicate Detection        │
│ • Posting Period             │
│ • High-Value Transactions    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ IFRS-Oriented Reviews        │
│                              │
│ • IAS 16 Depreciation        │
│ • IFRS 15 Revenue            │
│ • IAS 2 Inventory            │
│ • IAS 37 Provisions          │
└──────────────┬───────────────┘
               │
               ▼
       Exception Reports
               │
               ▼
      Master Control Summary
               │
               ▼
        Excel Dashboard
```

---

## 📂 Repository Structure

```text
accounting-internal-controls-automation/
│
├── data/
│   ├── transactions.csv
│   ├── gl_accounts.csv
│   └── cost_centers.csv
│
├── excel/
│   └── Accounting_Internal_Controls.xlsx
│
├── power-query/
│   └── controls/
│
├── documentation/
│   ├── control_matrix.md
│   ├── ifrs_scenarios.md
│   └── methodology.md
│
├── Screenshots/
│   └── dashboard.png
│
└── README.md
```

---

## 🔍 Automated Control Framework

| ID | Control | Purpose | Exception / Review Logic |
|---|---|---|---|
| **C01** | Debit / Credit Reconciliation | Detect unbalanced accounting documents | Total Debit ≠ Total Credit |
| **C02** | GL Account Validation | Detect postings to invalid accounts | GL account not found in Chart of Accounts |
| **C03** | Cost Center Validation | Check expense-account cost center assignment | Required cost center missing or invalid |
| **C04** | Segregation of Duties | Detect preparer/approver conflicts | Prepared By = Approved By |
| **C05** | Duplicate Detection | Identify potentially duplicated accounting documents | Matching accounting-document signature |
| **C06** | Posting Period Review | Support period-end transaction review | Transactions within selected closing period |
| **C07** | High-Value Transaction Review | Flag material transactions for additional review | Transaction amount > €20,000 |

The €20,000 threshold is an **illustrative internal-control threshold** used for this synthetic project rather than an IFRS requirement.

---

## 📘 IFRS-Oriented Accounting Scenarios

In addition to transaction-level controls, the project contains selected accounting scenarios designed to demonstrate how Power Query can support accounting review processes.

### IAS 16 — Property, Plant and Equipment

A depreciation workflow calculates depreciation expense for fixed assets and prepares information for the corresponding accounting entry.

Example year-end logic:

```text
Debit:  Depreciation Expense
Credit: Accumulated Depreciation
```

**FY 2026 calculated depreciation: €29,866.67**

---

### IFRS 15 — Revenue Recognition

The revenue-control scenario evaluates:

- recognition timing relative to the service period,
- recognized amounts,
- and GL-account validity.

The synthetic test population produced:

**3 revenue-recognition exceptions**

> This is a simplified control scenario and does not attempt to implement the complete IFRS 15 five-step revenue model.

---

### IAS 2 — Inventories

Inventory is evaluated using the **lower of cost and net realisable value (NRV)** principle.

```text
NRV =
Estimated Selling Price
− Completion Costs
− Selling Costs
```

Where NRV falls below cost, the model calculates the required inventory write-down.

**Calculated inventory write-down: €8,800.00**

---

### IAS 37 — Provisions

The provision-control scenario evaluates simplified recognition criteria including:

- present obligation,
- probability of outflow,
- ability to estimate the obligation,
- recognized amount,
- and GL-account validity.

The synthetic test population produced:

**3 provision exceptions**

> The IAS 37 implementation is intentionally simplified for control-automation demonstration purposes.

---

## 📈 Control Dashboard

The Excel dashboard consolidates the results of the automated control framework.

### Current Test Results

| KPI | Result |
|---|---:|
| Controls Performed | **9** |
| Control Exceptions | **51** |
| Controls Requiring Attention | **8** |
| High-Value Review Items | **106** |

### Exceptions by Control Area

| Area | Exceptions |
|---|---:|
| General Ledger | **18** |
| Internal Controls | **26** |
| IFRS-oriented controls | **7** |
| **Total** | **51** |

The dashboard separates **exceptions** from **review items**. For example, a transaction exceeding the €20,000 threshold is not automatically an accounting error; it is flagged for additional review.

---

## 🖼️ Dashboard Preview

Add the final dashboard screenshot to:

```text
Screenshots/dashboard.png
```

Then display it here:

![Accounting & Internal Control Dashboard](Screenshots/dashboard.png)

---

## ⚙️ Power Query Workflow

The solution uses Power Query as the transformation and control engine.

Typical processing flow:

```text
Import
   ↓
Data-Type Validation
   ↓
Master-Data Enrichment
   ↓
Accounting Control Logic
   ↓
PASS / FAIL / REVIEW Classification
   ↓
Exception Queries
   ↓
Master Control Summary
   ↓
Dashboard
```

Separate exception queries make it possible to investigate the underlying transactions rather than seeing only aggregated KPIs.

---

## 🔄 Refreshable Design

The workbook is designed so that the control workflow can be rerun when source data changes.

```text
New Source Data
      ↓
Excel → Refresh All
      ↓
Power Query Transformations
      ↓
Controls Recalculated
      ↓
Exceptions Updated
      ↓
Control Summary Updated
      ↓
Dashboard Updated
```

This separates the **control logic** from the presentation layer: Power Query performs the transformations and tests, while Excel presents the resulting KPIs and exception information.

---

## 🗃️ Data Model

The core synthetic datasets include:

### Transactions

SAP-style journal-entry data containing fields such as:

- Document ID
- Posting Date
- Company Code
- GL Account
- Cost Center
- Debit
- Credit
- Currency
- Document Type
- Prepared By
- Approved By

### Chart of Accounts

GL master data used to validate accounting postings and distinguish account categories.

### Cost Centers

Cost-center master data used to validate expense-account assignments.

Additional synthetic datasets support the fixed-asset, revenue, inventory and provision scenarios.

---

## 🛠️ Technologies Used

- **Microsoft Excel**
- **Power Query / M**
- Accounting reconciliation and exception analysis
- Data validation and transformation
- Automated control testing
- Dashboard reporting

---

## 💡 Key Skills Demonstrated

This project demonstrates practical experience with:

- General Ledger data analysis
- Debit/credit reconciliation
- Account and cost-center validation
- Internal control design
- Segregation-of-duties testing
- Duplicate transaction detection
- Period-end accounting review
- Exception-based reporting
- Power Query transformation and automation
- Excel dashboard development
- Selected IFRS-oriented accounting analyses

---

## ⚠️ Data & Accounting Disclaimer

All company names, users, transactions, balances and accounting scenarios in this repository are **synthetic and created solely for demonstration purposes**.

No confidential employer, client, SAP, or production financial data is included.

The IFRS-related components are simplified analytical/control scenarios designed to demonstrate accounting automation techniques. They should **not** be interpreted as complete implementations of IAS 2, IAS 16, IAS 37, IFRS 15, or as accounting advice.

---

## 🚀 Future Improvements

Potential extensions include:

- configurable materiality thresholds,
- automated control-owner notifications,
- historical exception trend analysis,
- Power BI reporting,
- SQL-based transaction storage,
- automated period-close control packs,
- control evidence and remediation tracking.

---

## 👤 Author

**Ayesha Ayesha**  
M.Sc. Economics — University of Bonn  
Focus: Finance, Data Analytics & Process Automation
