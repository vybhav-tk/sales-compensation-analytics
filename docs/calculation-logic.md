# Compensation Calculation Logic

## Objective

Convert eligible performance into an incentive payout through transparent, auditable intermediate calculations.

## Calculation Sequence

1. Confirm the participant is eligible for the period.
2. Determine eligible performance for the applicable measure.
3. Retrieve the correct quota or target.
4. Calculate attainment.
5. Apply the compensation-plan threshold or tier.
6. Determine the applicable payout rate or target-incentive factor.
7. Calculate preliminary incentive earnings.
8. Apply accelerators, caps, guarantees, or permitted adjustments where relevant.
9. Calculate final payout.
10. Retain the fields used to derive the result.

## Core Metric

**Attainment = Eligible Performance / Target**

Attainment and payout are intentionally treated as different concepts. Two participants with similar sales can have different attainment if their targets differ, and similar attainment can produce different payouts when plan rules or weights differ.

## Audit Fields

A calculation-level output should retain, at minimum, participant, period, measure, eligible performance, target, attainment, threshold/tier, applied rate, preliminary payout, adjustments, cap impact, final payout, and exception status.

## Portfolio Note

The compensation parameters used in this project are synthetic and were created for demonstration. They do not represent an official employer compensation plan.
