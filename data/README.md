# Synthetic Data

The files in this folder contain the synthetic source data used in the **Sales Compensation & Incentive Analytics** portfolio project.

> No real customer, employee, compensation-plan, quota, payroll, or employer data is included.

---

# Why Synthetic Data?

Sales compensation data is commercially sensitive.

A realistic portfolio project needs:

- employee records
- quota assignments
- transaction-level sales
- manager hierarchy
- compensation rules
- returns
- exceptions
- incentive awards

Using synthetic data allows those analytical problems to be demonstrated without exposing confidential information.

---

# Modeled Organization

The dataset represents the fictional company:

**Northstar Workplace Solutions Canada**

The quota-carrying sales organization contains:

- 48 sales representatives
- 8 managers
- 4 regions
- 3 sales roles

Modeled regions:

- Ontario
- Quebec
- West
- Atlantic

---

# Main Synthetic Data Areas

The source workbook contains data representing:

- employee master
- organization assignments
- Finance sales plan
- annual quotas
- quota seasonality
- compensation periods
- compensation plan
- commission tiers
- employee plan assignments
- product categories
- SPIFF rules
- sales transactions

---

# Transaction Dataset

The model contains approximately:

**6,839 raw transaction rows**

Transaction categories include:

- eligible sales
- returns
- cancellations
- shipping / delivery
- tax
- deliberately invalid or suspicious control cases

---

# Deliberately Planted Control Cases

The synthetic data intentionally contains compensation-control issues so the model can test exception detection.

Examples include:

- duplicate Transaction IDs
- transaction after employee termination
- invalid Employee ID
- negative revenue incorrectly classified as a Sale
- unknown product category
- transaction outside the modeled compensation period
- missing quota
- missing compensation-plan assignment
- attainment greater than 175%
- effective-dated manager change

These records are intentional test cases rather than accidental data-quality errors.

---

# Lifecycle Cases

The dataset also includes:

- new hires
- terminations
- new-hire ramping
- termination-month proration
- mid-year manager change

These cases allow the project to test effective dating and quota proration.

---

# Synthetic Performance Profiles

Sales performance was generated across several broad fictional performance profiles.

Examples include:

- Under Target
- Near Target
- Solid Performer
- High Performer
- Outlier

The synthetic profiles are generation metadata.

They are not compensation-plan inputs.

---

# Data Limitations

Because the dataset is synthetic:

- observed performance should not be interpreted as representative of a real company
- incentive relationships cannot be interpreted causally
- regional results are illustrative
- quota fairness cannot be conclusively assessed
- profitability cannot be calculated without margin data

The goal of the dataset is to support realistic modeling and analytical reasoning rather than reproduce any real employer environment.
