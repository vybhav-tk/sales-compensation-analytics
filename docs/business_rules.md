# Business Rules

This document defines the fictional sales-compensation rules used in the **Sales Compensation & Incentive Analytics** portfolio project.

> All rules in this repository are fictional and were created solely for the portfolio simulation. They do not represent the compensation plan, quota methodology, payroll process, or internal practices of Staples Canada or any other employer.

---

## Company Scenario

The model represents a fictional Canadian B2B organization called **Northstar Workplace Solutions Canada**.

The simulated quota-carrying sales organization contains:

- 48 sales representatives
- 8 sales managers
- 4 regions
- Account Executive I, Account Executive II, and Senior Account Executive roles
- $60M annual Finance sales plan
- $63M approved gross quota book
- 105% gross quota coverage

---

# 1. Compensation Period

Compensation is calculated on a **calendar-month basis**.

- monthly quota attainment resets each month
- core commission is calculated monthly
- there is no annual commission true-up in scope
- the modeled payout process operates one month in arrears
- Q3 SPIFF awards are validated after quarter end

---

# 2. Quota Rules

Annual nominal quota is allocated to months using seasonality.

| Month | Annual Allocation |
|---|---:|
| January | 7% |
| February | 7% |
| March | 8% |
| April | 8% |
| May | 8% |
| June | 9% |
| July | 7% |
| August | 7% |
| September | 10% |
| October | 10% |
| November | 9% |
| December | 10% |

The percentages total 100%.

## Effective Monthly Quota

The performance denominator is:

**Effective Monthly Quota = Nominal Monthly Quota × Active-Day Factor × Ramp Factor**

where:

**Nominal Monthly Quota = Annual Nominal Quota × Monthly Seasonality**

---

# 3. New-Hire Ramp and Proration

New hires use the following ramp schedule:

| Employment Stage | Ramp Factor |
|---|---:|
| Hire month | 50% |
| Second month | 75% |
| Third month onward | 100% |

The hire month is also prorated based on active employment days.

Termination months are prorated based on active days.

---

# 4. Eligible Credited Sales

The project defines eligible credited sales as:

> Net invoiced sales assigned to an eligible sales representative during the compensation period for commissionable products or services, after approved exclusions, cancellations, returns, and duplicate corrections.

## Eligible Categories

- Office Products
- Technology Hardware
- Furniture
- Technology Services

## Excluded Items

- sales tax
- shipping / delivery
- gift cards
- internal transfers
- cancelled transactions
- duplicate transactions pending resolution
- invalid employee transactions
- transactions outside the applicable compensation period

---

# 5. Returns and Cancellations

## Cancellation Before Invoice

The transaction is not eligible for compensation.

## Return After Invoice

The return is processed as **negative credited sales in the month in which the return is processed**.

The original compensation period is not reopened in this simplified model.

If a return or adjustment would create negative total variable compensation, the result is placed on **HOLD for manual review** rather than automatically producing negative payroll.

---

# 6. Core Commission Plan

The plan uses **marginal commission tiers**.

| Attainment Band | Rate | Component |
|---|---:|---|
| 0%–80% | 1.0% | Base Commission |
| 80%–100% | 2.0% | Base Commission |
| 100%–110% | 3.5% | Accelerator |
| >110% | 5.0% | Accelerator |

Only the sales dollars within each tier receive that tier's rate.

The plan is **not retroactive**.

---

# 7. Commission Example

For a rep with:

- quota = $100,000
- eligible sales = $120,000
- attainment = 120%

the payout is:

- $80,000 × 1.0% = $800
- $20,000 × 2.0% = $400
- $10,000 × 3.5% = $350
- $10,000 × 5.0% = $500

Total commission:

**$2,050**

The 5% rate is not applied to all $120,000.

---

# 8. Accelerator Rules

The 3.5% and 5.0% rates are the accelerator tiers.

The model distinguishes:

## Accelerator-Band Commission

The total commission earned on sales above 100% of quota.

## Incremental Accelerator Premium

The additional compensation expense compared with continuing the normal 2% marginal rate above quota.

This distinction is used for Finance forecasting and plan-effectiveness analysis.

---

# 9. Commission Cap

The modeled commission plan is **uncapped**.

There is no hard maximum payout.

However:

> Attainment above 175% automatically triggers a review.

This is a validation control, not a payout cap.

---

# 10. Q3 Technology Services SPIFF

The temporary SPIFF runs from:

**July 1 through September 30**

Technology Services sales also remain eligible for core commission.

The additional incentive is intentional.

## Target

**TSVC Target = 12% × Effective Q3 Sales Quota**

## Award Tiers

| TSVC Target Attainment | Award |
|---|---:|
| <80% | $0 |
| 80%–99.99% | $250 |
| 100%–119.99% | $600 |
| 120%+ | $1,000 |

Only the highest achieved tier is paid.

Awards are not cumulative.

---

# 11. Employee Eligibility

A rep must have:

- an eligible sales role
- an active compensation-plan assignment
- valid effective dates
- a valid quota
- active employment for at least part of the compensation period
- transactions occurring within the employee's valid employment period

Sales managers are excluded from the rep-level commission plan.

---

# 12. Missing Quota

A missing, invalid, overlapping, zero, or otherwise unusable quota results in:

**HOLD — Quota**

The model does not assume a quota value.

Without a valid denominator:

- quota attainment is not finalized
- core commission is not finalized
- the affected amount is not payroll-ready

---

# 13. Missing Compensation Plan

If there is no valid compensation-plan assignment for an employee-month:

**HOLD — Missing Plan**

The model does not automatically assign a default plan.

---

# 14. Transaction Controls

Examples of modeled controls include:

| Condition | Treatment |
|---|---|
| Duplicate Transaction ID | HOLD |
| Invalid Employee ID | HOLD |
| Transaction after termination | HOLD |
| Unknown Product Category | HOLD |
| Negative revenue coded as Sale | Review |
| Outside modeled compensation period | Review |
| Valid cancelled transaction | Excluded |
| Valid noncommissionable category | Excluded |
| Valid return | Eligible negative credit |

Unresolved HOLD or Review transactions contribute **$0** to eligible credited sales until resolved.

---

# 15. High-Attainment Review

Attainment greater than 175% is flagged as:

**Review — High Attainment**

The calculated commission is preserved as a working result.

The review does not automatically:

- cap the payout
- reduce the payout
- delete the payout

It prevents approval until the result has been validated.

---

# 16. Adjustments

Corrections are not made by overwriting historical compensation.

Adjustments are recorded separately with fields such as:

- Adjustment ID
- Employee ID
- original earning period
- processing period
- reason
- amount
- approval status
- approver
- approval date
- notes

This preserves an audit trail.

---

# 17. Approval Lifecycle

The modeled process is:

**Calculated → Exception / Hold → Reviewed → Approved → Sent to Payroll**

Approval is treated as a human governance decision.

A formula can determine whether an amount is eligible for approval, but it does not authorize payment by itself.

---

# 18. Payroll Reconciliation

The core reconciliation relationship is:

**Working Compensation = Approved Compensation + Held / Review Compensation**

A reconciliation difference other than zero indicates a control failure that must be investigated.

---

# 19. Currency and Rounding

Currency:

**CAD**

Revenue remains at full precision.

Payout components should be rounded to the nearest cent after component calculation.

---

# 20. Scope Exclusions

The current project does not fully model:

- split credit
- multi-currency compensation
- draws
- annual true-ups
- complex clawbacks
- payroll tax
- multi-measure incentive plans
- complex territory changes
- contribution margin
- quota difficulty / territory potential
- manager compensation plans
