# Project Phases

This document explains the project sequentially: **what was done, why it was done, how it was approached, and what the phase produced**.

## Phase 1 — Business Understanding

### What was done

Defined the purpose of sales compensation analytics, the stakeholder groups, the difference between performance and payout, and the business questions the analysis must answer.

### Why

It is possible to build a technically correct model that does not reflect the actual compensation process. Establishing the business problem first prevents the project from becoming a formula-only exercise.

### How

The project identified typical stakeholder needs across Sales Leadership, Finance, Payroll, HR, Sales Operations, and Compensation. It also separated three concepts:

- performance;
- attainment against target;
- payout under the incentive plan.

### Outcome

A clear problem statement, project objective, business-risk framework, and set of management questions.

---

## Phase 2 — Compensation Plan and Data Architecture

### What was done

Translated the conceptual compensation process into structured datasets, fields, keys, and relationships.

### Why

Compensation calculations depend on joining the right performance to the right participant, target, period, and plan rule. Ambiguous grain or keys can silently produce incorrect results.

### How

Defined logical datasets for participant master data, performance, quotas, plan parameters, eligibility, calculated payout, and exceptions. For each dataset, the row-level grain and join keys were considered explicitly.

### Outcome

A logical data model that supports traceable and reproducible calculations.

---

## Phase 3 — Data Preparation and Validation

### What was done

Designed validation steps before compensation calculations were applied.

### Why

Compensation logic cannot correct missing targets, duplicated sales, invalid participant mappings, or out-of-period transactions. Data-quality issues need to be surfaced before payout calculation.

### How

Created validation concepts for:

- missing keys;
- duplicate records;
- unmatched participants;
- missing quotas;
- invalid plan assignments;
- eligibility problems;
- unusual negative or zero values;
- period mismatches;
- source-total reconciliation.

### Outcome

A clean analytical population plus an exception population requiring review.

---

## Phase 4 — Attainment and Incentive Calculation

### What was done

Structured the sequence that converts eligible performance into compensation payout.

### Why

The payout must be explainable at the participant-period level. Separating the calculation into intermediate steps makes it possible to audit and troubleshoot.

### How

The calculation framework follows a sequence such as:

1. determine eligible performance;
2. retrieve the assigned target;
3. calculate attainment;
4. apply threshold / tier rules;
5. determine the applicable rate or target incentive factor;
6. calculate preliminary payout;
7. apply accelerators, caps, or other plan provisions where applicable;
8. calculate final payout;
9. retain calculation-driver fields for auditability.

### Outcome

A reproducible payout-calculation framework rather than a black-box result.

---

## Phase 5 — Reconciliation and Quality Assurance

### What was done

Designed controls to verify that the payout output is complete and reasonable.

### Why

A correct formula can still produce an incorrect compensation file if the population is incomplete, source totals are wrong, or records are duplicated. QA is a separate analytical responsibility.

### How

The project uses a combination of:

- population reconciliation;
- source-total tie-outs;
- target completeness checks;
- duplicate detection;
- payout reasonableness tests;
- extreme-value review;
- zero-payout review;
- manual participant spot checks;
- exception counts by category.

### Outcome

A controlled compensation output that can be defended before downstream use.

---

## Phase 6 — Performance and Payout Analysis

### What was done

Analyzed the validated payout data to understand how performance and compensation outcomes are distributed.

### Why

The role of a Sales Compensation Analyst extends beyond calculation administration. Management needs to know whether the observed payouts and attainment patterns make sense operationally and financially.

### How

The analysis considers:

- target attainment distribution;
- percentage of participants below / at / above target;
- payout distribution;
- top and bottom performers;
- concentration of compensation cost;
- payout relative to performance;
- unusual or high-leverage records;
- team / territory / organizational comparisons where data supports them.

### Outcome

Management-ready insight into both sales performance and incentive cost.

---

## Phase 7 — Scenario and Sensitivity Analysis

### What was done

Built a framework for testing changes in compensation assumptions.

### Why

Compensation plans influence behavior and cost. Management may need to understand the financial effect of changing rates, thresholds, targets, caps, or performance assumptions before making decisions.

### How

The base case is compared against alternative scenarios while changing one or more controlled assumptions. Results are evaluated using metrics such as total payout, average payout, attainment distribution, number of participants affected, and payout concentration.

### Outcome

A structured what-if capability that supports evidence-based compensation discussions.

---

## Phase 8 — Management Reporting and Recommendations

### What was done

Converted the technical work into a business narrative suitable for management and interviews.

### Why

A compensation analyst must be able to explain not only **what** the numbers are, but **why** they occurred, whether they are reliable, and what action should follow.

### How

The reporting structure emphasizes:

1. business context;
2. methodology;
3. controls;
4. key findings;
5. exceptions / risks;
6. scenarios;
7. recommendations;
8. limitations and next steps.

### Outcome

An end-to-end portfolio story demonstrating analytical, compensation, and stakeholder-communication capability.

---

## Phase 9 — Power BI Dashboard — Pending

### What will be done

Build an interactive Power BI layer on top of the validated analytical output.

### Why

Power BI will provide an easier way for stakeholders to monitor attainment, payout, cost, outliers, and exceptions without reviewing calculation-level worksheets or query outputs.

### Planned approach

The model should prioritize a clean star schema, explicit measures, drill-through capability, and visible QA indicators.

### Planned outcome

A dashboard with executive KPIs, attainment and payout distributions, participant/team detail, exception monitoring, and scenario comparison.
