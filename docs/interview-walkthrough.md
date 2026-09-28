# Interview Walkthrough

This document provides a concise way to explain the **Sales Compensation & Incentive Analytics** portfolio project in an interview.

The project uses synthetic data and fictional compensation rules.

It should be presented as a portfolio simulation demonstrating domain understanding, analytical modeling, controls, Excel, and Power BI design — not as professional sales-compensation administration experience.

---

# 60–90 Second Project Summary

> “I wanted to understand sales compensation beyond simply calculating commission percentages, so I built a portfolio simulation of the monthly compensation process.
>
> I modeled employee and quota assignments, effective quota after new-hire ramping and proration, transaction-level sales crediting, quota attainment, marginal commissions and accelerators, a Q3 Technology Services SPIFF, exception controls, payroll reconciliation, quota coverage against a Finance plan, and commission-expense forecasting.
>
> I then consolidated the process into an Excel model and designed a Power BI semantic model for executive, performance, control, and Finance reporting.
>
> The project is not professional sales-compensation administration experience, but it helped me understand how plan rules and sales results translate into auditable employee payouts and financial reporting.”

---

# What Problem Was I Solving?

The business problem was:

> **How do you convert raw sales activity into accurate, explainable, and payroll-ready incentive compensation?**

The project addresses four questions:

1. What happened?
2. What should we pay?
3. Can we trust the payment?
4. What should management do next?

---

# What Did I Build?

I built a simplified end-to-end compensation process covering:

- employee and organizational assignments
- annual and monthly quota
- new-hire ramp and active-day proration
- transaction-level sales crediting
- quota attainment
- marginal commission tiers
- accelerators
- Technology Services SPIFF
- exception management
- payout approval logic
- payroll reconciliation
- quota coverage vs Finance plan
- compensation-expense forecasting
- plan-effectiveness analysis
- Power BI reporting design

---

# How Does the Commission Plan Work?

The fictional plan uses marginal tiers:

| Attainment | Rate |
|---|---:|
| 0%–80% | 1.0% |
| 80%–100% | 2.0% |
| 100%–110% | 3.5% |
| >110% | 5.0% |

I would explain that the plan is **marginal**, meaning only the sales inside each band receive that band's rate.

For example, at 120% attainment, the 5% rate is not applied to all sales.

That prevents a retroactive payout cliff.

---

# A Strong Traceability Example

One of the best examples is Maya Chen in August.

She had:

- effective quota: $85,400
- eligible sales: $100,772
- attainment: 118%

Her commission was broken into four marginal bands.

That produced:

- base commission: $1,024.80
- accelerator commission: $640.50
- total working commission: $1,665.30

The important point is not just the amount.

The model can explain exactly **why** she received that amount.

---

# A Strong Controls Example

A different employee had a January commission that was mathematically calculated correctly.

However, the compensation-plan assignment did not begin until February.

The downstream control layer therefore placed the January result on:

**HOLD — Missing Plan**

I would use this example to explain:

> **A mathematically correct calculation can still be an administratively invalid payment.**

That is why eligibility, effective dates, exceptions, and reconciliation matter.

---

# Quota Coverage Insight

The Finance sales plan is:

**$60M**

Gross quota book:

**$63M**

Gross coverage:

**105%**

However, after effective dating, new-hire ramping, and employee lifecycle proration:

Effective quota is approximately:

**$58.4M**

Effective coverage:

**~97.3%**

This shows that the initial 5% planning buffer can disappear operationally.

The analyst's role is to surface that gap.

Sales Leadership and Finance would decide how to respond.

---

# Forecasting Insight

The plan contains accelerators, so commission expense does not increase linearly with sales.

At 110% attainment:

- sales are approximately 10% above the 100% scenario
- commission expense is approximately 29% higher

At 120% attainment:

- sales are approximately 20% higher
- commission expense is approximately 71% higher

I would explain this as:

> “Finance should forecast commission using the actual payout curve rather than multiplying sales by one historical average commission percentage.”

---

# Accelerator Insight

The project separates:

### Accelerator-Band Commission

All commission earned on sales above quota.

from:

### Incremental Accelerator Premium

The additional cost caused specifically by increasing the marginal rate above quota.

The modeled incremental premium is approximately:

**$115K**

This gives Finance a more useful measure of the cost of the accelerator design.

---

# SPIFF Insight

The Q3 Technology Services SPIFF produced:

- 46 eligible reps
- 25 award recipients
- $18,500 total SPIFF cost
- approximately $1.70M of eligible Technology Services sales
- SPIFF cost / TSVC sales of approximately 1.09%

I would be careful not to say the SPIFF caused the sales.

Instead:

> “The project shows the observed economics of the program, but stronger causal analysis would require a baseline, comparison group, or experimental design.”

---

# Controls and Payroll Insight

The model identified:

- 13 compensation exceptions
- 10 Critical
- 3 Review
- approximately $19K of working compensation blocked or under review
- zero payroll reconciliation difference

This demonstrates that compensation controls have financial consequences and are not just administrative checks.

---

# What Did Power BI Add?

The Power BI reporting design converts the calculation model into a star-schema reporting layer.

The report is designed around four pages:

1. Executive Overview
2. Performance & Compensation
3. Controls & Payroll
4. Finance & Incentives

This separates operational compensation administration from management reporting while using the same validated analytical outputs.

---

# What Is the Biggest Business Insight?

A strong answer is:

> “One of the biggest insights was that gross quota coverage and effective operational quota coverage are not the same thing. The company started with a 105% gross quota buffer, but lifecycle effects reduced effective coverage below 100%. Sales still exceeded the Finance plan because the active population overperformed. That is positive performance, but it also shows why management should not rely on rep overachievement to compensate for structural quota-capacity gaps.”

---

# What Did I Learn?

The biggest learning was that Sales Compensation is not just commission calculation.

The analyst needs to understand:

- business rules
- quota administration
- transaction eligibility
- effective dating
- calculation logic
- exception controls
- payroll reconciliation
- Finance forecasting
- incentive economics
- stakeholder communication

The calculation is only one part of the process.

---

# How Should I Position My Experience?

I would say:

> “I have not worked as a Sales Compensation Analyst professionally yet. I built this portfolio project specifically to understand the domain and connect my existing analytics skills — Excel, BI, data modeling, KPI analysis, and stakeholder communication — to the responsibilities of the role.”

Avoid saying:

- “I administered commissions for a sales team”
- “I designed compensation plans professionally”
- “I owned payroll compensation”
- “This is how Staples calculates commission”

Those statements would overstate the experience.

---

# Questions the Project Helps Me Answer

The project gives me examples to discuss if asked:

- How would you validate a commission payout?
- How would you investigate a rep dispute?
- What is quota attainment?
- What is an accelerator?
- Why are marginal tiers important?
- How do new hires affect quota?
- What is quota coverage?
- How would you forecast commission expense?
- How do you reconcile compensation before Payroll?
- How would you evaluate a SPIFF?
- How would you automate a compensation process?
- How would you communicate compensation results to Finance or Sales Leadership?

---

# Closing Interview Statement

> “The biggest thing this project taught me is that a Sales Compensation Analyst needs both analytical accuracy and operational discipline. You have to understand how a plan is supposed to work, make sure the underlying data is valid, calculate the payout transparently, reconcile it before payroll, and then be able to explain the result to both the salesperson and management.”
