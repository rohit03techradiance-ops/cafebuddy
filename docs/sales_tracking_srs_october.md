# Sales Tracking and Analysis Software SRS (October Dataset, INR Context)

## 1) Software Requirements Specification (SRS) Outline

### 1.1 Functional Requirements

#### FR-01: Data Ingestion and Validation
- The system shall import Excel workbooks (`.xlsx`, `.xls`) containing October sales and inventory usage data.
- The system shall support multi-sheet mapping (e.g., Sales, Inventory Usage, Product Master, Outlet Master).
- The system shall auto-detect column headers and allow manual remapping when headers differ.
- The system shall validate required fields:
  - Date, Invoice/Transaction ID, Product, Quantity Sold, Unit Selling Price, Net Sales Amount (if available).
  - Inventory Consumed/Used, Unit Cost, Stock Movement Date.
- The system shall flag missing, duplicated, malformed, or out-of-range records before analysis.
- The system shall persist import logs and validation summaries.

#### FR-02: INR-Centric Data Standardization
- The system shall standardize all monetary values to Indian Rupees (INR).
- The system shall render currency using Indian number grouping and symbols (e.g., `₹1,23,456.78`).
- The system shall support configurable rounding rules (paise precision at 2 decimals, optional whole-rupee display).
- The system shall permit GST-inclusive and GST-exclusive value handling where fields exist.

#### FR-03: Core Sales Metrics Computation
- The system shall compute total sales revenue for October in INR.
- The system shall compute gross sales, discounts, returns, net sales, and average order value (AOV).
- The system shall compute total quantity sold and unique invoices/orders.
- The system shall compute day-wise, week-wise, and month-to-date trend lines.
- The system shall compute category-wise and product-wise revenue contribution.

#### FR-04: Cost, Usage, and Profitability Analytics
- The system shall compute cost of goods sold (COGS) from inventory usage and/or unit costs.
- The system shall compute gross profit and gross margin (%) overall and by product/category.
- The system shall compute inventory usage efficiency:
  - Consumption-to-sales ratio.
  - High-consumption low-revenue items.
  - Potential wastage indicators based on configurable thresholds.
- The system shall identify negative-margin products and exceptions.

#### FR-05: Operational Dashboards
- The system shall provide an executive dashboard on load with KPI cards and key charts.
- The system shall provide drill-down views by:
  - Date range (within October and comparable periods if present).
  - Product, category, outlet/store, and sales channel.
- The system shall support filters for weekdays/weekends, festive periods, and peak hours (if timestamp exists).
- The system shall allow sorting/ranking (Top N/Bottom N products, categories, outlets).

#### FR-06: Exception Detection and Alerts
- The system shall surface anomalies immediately after data load:
  - Sudden day-over-day sales drops/spikes.
  - Sharp inventory consumption variance.
  - Stockouts/near-stockouts where opening/closing stock fields exist.
- The system shall provide rule-based alerts and severity tagging (high/medium/low).

#### FR-07: Reporting and Export
- The system shall generate owner-ready reports in PDF and Excel.
- The system shall allow scheduled and on-demand report generation.
- The system shall export filtered views and chart-ready datasets.
- The system shall include one-click “October Business Summary (INR)” report.

#### FR-08: Data Governance and Auditability
- The system shall maintain lineage from raw row to computed KPI.
- The system shall provide an audit trail for manual corrections and mapping overrides.
- The system shall support versioned data imports for repeatable analysis.

### 1.2 Non-Functional Requirements

#### NFR-01: Performance
- Initial workbook load and KPI rendering shall complete within 5 seconds for up to 100,000 rows.
- Dashboard filter interactions shall respond within 1 second for common queries.
- Export generation shall complete within 10 seconds for standard report bundles.

#### NFR-02: Accuracy and Reliability
- Monetary calculations shall maintain deterministic precision suitable for INR accounting.
- Re-running the same dataset and filter conditions shall produce identical KPI outputs.
- Validation coverage shall detect schema and value errors with clear diagnostics.

#### NFR-03: Usability (Owner-First Design)
- The first screen shall present a concise “Owner Snapshot” with key October answers in under one minute.
- All monetary visualizations shall default to INR and Indian digit grouping.
- The UI shall avoid jargon and use business labels (Revenue, Profit, Wastage, Fast Movers).
- Critical metrics shall include definitions/tooltips.

#### NFR-04: Security and Access Control
- Role-based access control shall restrict who can upload, edit mappings, and publish reports.
- Data at rest and in transit shall be encrypted.
- The system shall log user actions affecting data interpretation.

#### NFR-05: Maintainability and Extensibility
- Metric logic shall be configurable (e.g., margin formula variants, GST treatment).
- Data connectors shall be modular for future POS/ERP integration.
- The system shall support monthly roll-forward beyond October without redesign.

#### NFR-06: Availability and Backup
- Monthly data and reports shall be backed up automatically.
- Recovery point and recovery time objectives shall be documented and testable.

#### NFR-07: Compliance and Localization
- Date formats shall support Indian conventions (`DD-MM-YYYY`).
- Currency, tax and reporting views shall support Indian business practices.
- The software shall support English labels with option to localize later.

---

## 2) Mandatory Owner Questions (Must Be Answered Immediately on Data Load)

### A. Revenue and Sales Health
1. What is the **total net sales revenue in INR** for October?
2. What are the **gross sales, discounts, returns, and net sales** values in INR?
3. What is the **average order value (AOV)** in INR?
4. Which **3 days had the highest sales** and which 3 had the lowest?
5. What is the **day-wise sales trend** across October (with weekday/weekend split)?

### B. Product and Category Performance
6. Which **product categories contributed the highest revenue** in INR?
7. Which **top 10 products** generated the most sales revenue?
8. Which products have **high sales volume but low revenue per unit**?
9. Which products/categories are **underperforming** versus the month average?

### C. Profitability and Cost Control
10. What is the **total COGS** and **gross profit** in INR for October?
11. What is the **overall gross margin (%)** for the month?
12. Which products/categories have the **highest and lowest profit margins**?
13. Are there any **negative-margin products**? What is the impact in INR?

### D. Inventory Usage and Wastage Signals
14. What is the **total inventory consumed** and its cost in INR?
15. Which items show **high inventory consumption with low sales contribution**?
16. Where is the **largest usage-to-sales mismatch** (possible wastage/leakage)?
17. Which SKUs are potential **stockout risks** based on sales velocity and usage?

### E. Exceptions, Risks, and Actions
18. Were there any **abnormal sales drops/spikes** during October? On which dates?
19. Which categories/products require **immediate corrective action** (price, procurement, promotion)?
20. What are the **top 5 owner actions** recommended from this month’s data?

### F. One-Screen Executive Snapshot
21. What are the **single-page KPI answers** for: Revenue, Profit, Margin, Top Category, Top Product, Highest Wastage Risk, and Worst Margin Product?
22. If the owner asks “**How did we perform this October in INR, and what should we fix first?**”, what is the instant evidence-backed summary?
