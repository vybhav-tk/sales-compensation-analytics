# QA, Reconciliation, and Controls

## Purpose

Sales compensation outputs require stronger controls than ordinary KPI reporting because the result can affect financial payments. A formula returning a value is not sufficient evidence that the payout population is correct.

## Data-Quality Controls

- Missing participant IDs
- Duplicate source records
- Missing quotas or targets
- Missing or invalid plan assignments
- Ineligible participants included in the calculation
- Invalid or out-of-period dates
- Negative or unusual performance values
- Unmatched joins between source datasets

## Reconciliation Controls

- Source performance totals versus analytical-model totals
- Source participant counts versus calculation population
- Assigned-target completeness
- Calculated payout totals by period/team/plan
- Exception counts by category
- Manual participant-level spot checks

## Reasonableness Tests

The model also reviews zero payouts, unusually high payouts, maximum/capped payouts, extreme attainment, material adjustments, and unusual payout-to-performance relationships.

## Outcome

The goal is a calculation file that can be explained and defended: source records reconcile, rule assignments are complete, exceptions are visible, and material results have been reviewed before downstream use.
