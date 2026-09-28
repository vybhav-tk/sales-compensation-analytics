# Methodology

This document explains the analytical methodology used to build the Sales Compensation & Incentive Analytics portfolio project.

The project was intentionally developed from the **business process outward**, rather than starting with Excel formulas or dashboards.

---

# 1. Define the Business Problem

The first step was to define the three core responsibilities of a compensation analytics process.

## Compensation Administration

Determine:

> How much should each salesperson be paid?

## Financial Control

Determine:

> Can the result be trusted and approved?

## Management Analytics

Determine:

> What do performance and compensation results tell management?

This framing guided every later modeling decision.

---

# 2. Define the Fictional Business Rules

Before building calculations, the project established explicit rules for:

- Finance sales plan
- quota coverage
- quota seasonality
- new-hire ramp
- termination proration
- sales eligibility
- returns
- cancellations
- commission tiers
- accelerators
- SPIFF eligibility
- SPIFF award tiers
- missing quota
- missing plan
- exception treatment
- approval workflow
- payroll reconciliation

This prevents formulas from embedding undocumented assumptions.

---

# 3. Design the Data Model

The conceptual model separates five layers.

## Layer 1 — Master and Organization

Examples:

- Employee Master
- Organization Assignment
- Region

## Layer 2 — Planning and Rules

Examples:

- Finance Plan
- Annual Quota
- Quota Seasonality
- Compensation Plan
- Commission Tiers
- SPIFF Rules

## Layer 3 — Transactions

Examples:

- Sales Transaction
- Sales Credit Detail

## Layer 4 — Calculated Compensation

Examples:

- Monthly Performance
- Commission Tier Detail
- Incentive Award
- Compensation Payout

## Layer 5 — Controls and Audit

Examples:

- Compensation Exception
- Compensation Adjustment
- approval and payroll status

The model explicitly avoids mixing table grains.

---

# 4. Generate Synthetic Source Data

A fictional dataset was created with:

- 48 quota-carrying reps
- 8 managers
- 4 regions
- annual quotas
- effective-dated organization assignments
- new hires
- terminations
- approximately 6,800 raw sales transactions
- returns
- cancellations
- noncommissionable product categories
- deliberately planted control cases

The purpose of the synthetic controls was to test whether the model could detect realistic compensation problems.

---

# 5. Build the Monthly Quota Engine

For each employee-month:

**Nominal Monthly Quota = Annual Quota × Seasonality**

Then:

**Effective Monthly Quota = Nominal Monthly Quota × Active-Day Factor × Ramp Factor**

Controls detect:

- missing quota
- invalid quota
- overlapping quota
- not-employed periods

---

# 6. Apply Sales Crediting Rules

Each transaction is classified as:

- Eligible
- Excluded
- Review
- HOLD

The project uses a control hierarchy so unresolved transactions contribute zero compensation credit until resolved.

Valid returns are allowed to create negative credited sales.

This stage converts:

**Raw Revenue → Eligible Credited Sales**

---

# 7. Calculate Monthly Performance

For each employee-month:

**Quota Attainment = Eligible Credited Sales ÷ Effective Monthly Quota**

The model then assigns a performance band.

Performance and processing status are kept separate.

A rep can have strong sales performance while the compensation record remains on HOLD because the underlying inputs are invalid.

---

# 8. Calculate Marginal Commission

Commission is calculated tier by tier.

For each tier:

**Sales in Tier = max(0, min(Eligible Sales, Tier Ceiling) − Tier Floor)**

Then:

**Commission Amount = Sales in Tier × Commission Rate**

Tier-level detail is retained so the final payout is explainable.

---

# 9. Validate Accelerator Economics

The model tests plan thresholds around:

- 80%
- 100%
- 110%

This confirms that the marginal plan creates smooth payout progression rather than retroactive payout cliffs.

The model then calculates:

## Accelerator-Band Commission

Commission earned on above-quota sales.

## Incremental Accelerator Premium

Additional expense relative to continuing the normal 2% marginal rate above quota.

---

# 10. Calculate the Q3 SPIFF

For each eligible rep:

**TSVC Target = 12% × Effective Q3 Quota**

Then:

**TSVC Attainment = Eligible Q3 TSVC Sales ÷ TSVC Target**

The employee receives the highest achieved fixed-dollar award tier.

The SPIFF remains separate from core commission.

---

# 11. Build the Compensation Control Layer

The project consolidates issues from:

- quota controls
- plan assignment
- sales crediting
- high attainment
- SPIFF validation

into a central exception register.

The control lifecycle is:

**Calculated → Exception / Hold → Reviewed → Approved → Payroll**

This stage also corrected a deliberate missing-plan case that earlier pure calculation logic would have allowed.

---

# 12. Reconcile Payroll

The model tests:

**Working Compensation = Approved Compensation + Held / Review Compensation**

Any unexplained difference is treated as a reconciliation failure.

---

# 13. Analyze Quota Coverage

Three coverage concepts are separated.

## Gross Coverage

**Gross Quota Book ÷ Finance Plan**

## Nominal In-Force Coverage

Quota that is actually effective during the year ÷ Finance Plan.

## Effective Operational Coverage

Quota after ramp and active-day proration ÷ Finance Plan.

This identifies whether the original planning buffer remains after employee lifecycle effects.

---

# 14. Forecast Commission Expense

The model uses uniform attainment scenarios:

- 90%
- 100%
- 110%
- 120%

For each scenario:

1. multiply effective quota by assumed attainment
2. allocate sales through the marginal tiers
3. calculate base commission
4. calculate accelerator commission
5. compare to a no-accelerator baseline

This demonstrates that compensation expense is nonlinear above quota.

---

# 15. Analyze Plan Effectiveness

The project evaluates descriptive plan economics using:

- attainment distribution
- commission rate by attainment band
- payout concentration
- accelerator share
- incremental accelerator premium
- SPIFF participation
- SPIFF cost ratios
- approval/control viability

The analysis deliberately distinguishes:

> **descriptive evidence**

from:

> **causal evidence**

The synthetic dataset cannot prove that incentives caused the observed sales results.

---

# 16. Build the Excel Portfolio Model

The final Excel workbook consolidates the model into a recruiter/interview-friendly structure.

The flow is:

**Dashboard → Rules → Quota Coverage → Sales Credit → Performance & Commission → SPIFF → Controls → Forecast → Effectiveness → Traceability → Business Insights**

The detailed phase workbooks remain development artifacts rather than the primary portfolio deliverable.

---

# 17. Design the Power BI Semantic Model

The reporting model uses a star-schema approach.

Dimensions:

- Employee
- Date
- Product Category
- Scenario

Facts:

- Sales Credit
- Monthly Performance
- SPIFF
- Exceptions
- Payroll
- Forecast

This allows slicers to filter facts consistently without fact-to-fact relationships.

---

# 18. Translate Analysis Into Management Insight

The final stage asks:

- what happened?
- why does it matter?
- what should management investigate?
- who should own the action?
- what limitation applies?

This converts calculation output into decision support.

---

# Validation Approach

Throughout the project, validation included:

- formula error scans
- row-count reconciliation
- revenue reconciliation
- transaction-status reconciliation
- quota rollup reconciliation
- tier-boundary tests
- payout reconciliation
- exception reconciliation
- forecast scenario comparison
- management-level reasonableness checks

---

# Analytical Principles

The project is built around several recurring principles.

## Traceability

Every payout should be reconstructable.

## Grain Discipline

Do not combine transaction-level and employee-month-level records in the same table without aggregation.

## Effective Dating

Employee, quota, hierarchy, and plan status must be evaluated for the relevant period.

## Working vs Approved

Calculated compensation is not automatically an authorized payment.

## Preserve Source History

Do not silently delete suspicious transactions or overwrite historical compensation.

## Separate Administration From Effectiveness

Two different questions must be answered:

> Did we pay correctly?

and:

> Is the incentive design producing economically sensible outcomes?

## Avoid Causal Overreach

Observed association between incentives and performance is not proof that incentives caused performance.
