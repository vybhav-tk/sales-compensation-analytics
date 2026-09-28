# Power BI Reporting Layer

This folder contains the Power BI reporting design and semantic-model assets for the **Sales Compensation & Incentive Analytics** portfolio project.

## Current Files

### `sales_compensation_powerbi_data_model.xlsx`

A Power BI-ready data package containing:

#### Dimensions

- Dim Employee
- Dim Date
- Dim Product Category
- Dim Scenario

#### Fact Tables

- Fact Sales Credit
- Fact Monthly Performance
- Fact SPIFF
- Fact Exceptions
- Fact Payroll
- Fact Forecast Monthly

The workbook also includes:

- model relationship documentation
- DAX measure catalogue
- report-page blueprint
- Power BI build steps
- model parameters

## Recommended Power BI Model

The reporting layer uses a **star schema**.

Dimensions should filter facts in a single direction.

Avoid direct fact-to-fact relationships.

The primary shared dimensions are:

- Employee
- Date
- Product Category
- Forecast Scenario

## Recommended Report Pages

### Page 1 — Executive Overview

Designed to answer:

> What happened, what should we pay, and can management trust the result?

Suggested visuals:

- Eligible Credited Sales
- Effective Quota
- Weighted Quota Attainment
- Working Core Commission
- Approved Compensation
- Effective Quota Coverage
- Open Exceptions
- monthly sales vs quota
- attainment distribution
- working vs approved compensation

---

### Page 2 — Performance & Compensation

Designed to answer:

> How is performance translating into compensation?

Suggested visuals:

- quota attainment vs commission scatterplot
- employee-period performance matrix
- base vs accelerator commission
- attainment-band distribution
- employee drillthrough

---

### Page 3 — Controls & Payroll

Designed to answer:

> Can the compensation result safely proceed to payroll?

Suggested visuals:

- Critical Exceptions
- Review Exceptions
- Blocked / Pending Compensation
- Approval Rate
- exceptions by type
- payroll reconciliation
- exception register

---

### Page 4 — Finance & Incentives

Designed to answer:

> What are the financial implications of quota coverage and incentive design?

Suggested visuals:

- quota coverage by region
- 90% / 100% / 110% / 120% forecast scenarios
- forecast commission expense
- accelerator premium
- SPIFF cost and target attainment
- compensation-to-sales rate

## Important Modeling Note

The Payroll fact can be analyzed using two different dates:

- **Scheduled Payout Date**
- **Earning Period Start**

The recommended model uses Scheduled Payout Date as the active relationship to the Date dimension.

Earning Period Start can be configured as an inactive relationship and activated in specific measures using `USERELATIONSHIP()` when earning-period analysis is required.

## DAX Principles

The measure catalogue includes calculations for:

- eligible credited sales
- effective quota
- weighted attainment
- base commission
- accelerator commission
- working compensation
- approved compensation
- blocked compensation
- approval rate
- quota coverage
- forecast commission
- accelerator premium
- SPIFF economics

A key rule is that weighted attainment should not infer a denominator for employee-months with invalid or missing quota.

## Dashboard Screenshots

Final exported screenshots should be stored in:

`powerbi/screenshots/`

Recommended filenames:

- `executive_overview.png`
- `performance_compensation.png`
- `controls_payroll.png`
- `finance_incentives.png`

These images can then be embedded in the repository's root README.

## PBIX File

When the native Power BI report is built, add:

`powerbi/sales_compensation_dashboard.pbix`

## Synthetic Data Disclaimer

The Power BI model uses synthetic portfolio data and fictional compensation rules.

It is designed to demonstrate semantic modeling, DAX thinking, compensation analytics, and management reporting rather than reproduce any employer's internal reporting environment.
