# Data Model

## Purpose

The compensation model separates business entities and calculation inputs so each payout can be traced to its participant, performance period, target, and plan rule.

## Logical Datasets

| Dataset | Typical grain | Purpose |
|---|---|---|
| Participant master | One row per participant | Identifies the person or analytical participant and organizational attributes |
| Performance | One row per transaction or participant-period-measure | Stores eligible sales/performance results |
| Quota / target | One row per participant-period-measure | Stores the target used to calculate attainment |
| Plan parameters | One row per plan / measure / effective period / tier | Stores thresholds, rates, accelerators, caps, and related rules |
| Eligibility / assignment | One row per participant-plan-period | Determines which plan applies and whether the participant is eligible |
| Calculated payout | One row per participant-period-measure or participant-period | Stores attainment, applied rule, preliminary payout, adjustments, and final payout |
| Exceptions | One row per detected issue | Stores QA flags requiring review |

## Key Relationships

The analytical joins are designed around stable keys such as participant ID, performance period, measure, and plan assignment. The exact grain is documented before calculations are built because an incorrect one-to-many relationship can duplicate performance or payout amounts.

## Design Principles

- Keep source data separate from calculated outputs.
- Define row-level grain before joining datasets.
- Retain calculation-driver columns for auditability.
- Use effective dates where plan rules or assignments can change over time.
- Reconcile record counts and totals after major joins.
