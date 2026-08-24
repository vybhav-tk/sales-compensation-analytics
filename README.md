# Sales Compensation & Incentive Analytics

A portfolio project demonstrating how a Sales Compensation Analyst can translate a compensation plan into an auditable analytical workflow: from business rules and source data through attainment, incentive calculations, reconciliation, exception analysis, scenario testing, and management reporting.

> **Synthetic-data / portfolio disclaimer**  
> This project is an independent analytical case study built with **synthetic data created for portfolio and learning purposes**. It is not an official compensation plan, payroll process, quota methodology, or reporting solution of any organization. The participant records, performance results, targets, compensation rates, thresholds, tiers, and payout outcomes are simulated and do not represent real employees or official company compensation rules.

## Executive Summary

Sales compensation sits at the intersection of sales performance, finance, payroll, HR, and operations. The core challenge is not simply calculating a commission. The analyst must make sure that incentive payments are **accurate, explainable, reproducible, and aligned with the intent of the compensation plan**.

This project builds an end-to-end sales compensation analytics workflow that answers four fundamental questions:

1. **What performance did each participant achieve?**
2. **How should the compensation plan translate that performance into incentive earnings?**
3. **Can the payout be validated and explained before payment?**
4. **What can management learn from the resulting performance and payout patterns?**

The project uses Excel, SQL, structured QA controls, scenario analysis, and management-oriented reporting. A Power BI dashboard is the remaining visualization layer and will be added later.

## Business Problem

A sales organization may have hundreds or thousands of transactions, multiple performance measures, individual targets, eligibility rules, tiers, accelerators, caps, and exception conditions. Raw sales results alone do not determine what an employee should be paid.

A Sales Compensation Analyst therefore needs a controlled process that can:

- connect sales results to the correct participant and performance period;
- apply the correct quota or target;
- calculate attainment consistently;
- translate attainment into incentive earnings using the compensation-plan rules;
- detect missing, duplicated, inconsistent, or unusual records;
- reconcile calculated earnings before payroll or finance consumption;
- explain payout differences to stakeholders;
- quantify the financial effect of alternative plan assumptions;
- provide management with clear performance and cost insights.

Without these controls, organizations face risks such as overpayment, underpayment, employee disputes, poor plan credibility, budgeting surprises, and weak auditability.

## Solution

The project addresses the problem through a controlled analytical pipeline:

**Source data → validation → plan-rule mapping → target attainment → payout calculation → QA/reconciliation → exception analysis → scenario analysis → management reporting → Power BI**

The solution is designed around three principles:

- **Accuracy:** calculations should match the documented plan rules.
- **Auditability:** every payout should be traceable back to source data, target, rule, and calculation.
- **Decision usefulness:** outputs should help management understand both sales performance and compensation cost.

## Project Phases

| Phase | Focus | Why it matters | Main outcome |
|---|---|---|---|
| 1 | Business understanding | Prevents technically correct analysis from solving the wrong problem | Defined stakeholders, business questions, risks, and success criteria |
| 2 | Compensation-plan and data architecture | Converts plan language into measurable fields and rules | Defined inputs, relationships, data grain, measures, and rule dependencies |
| 3 | Data preparation and validation | Bad source data creates bad payouts | Clean analytical dataset with validation controls and exception flags |
| 4 | Attainment and incentive logic | Performance must be converted consistently into earnings | Reproducible target, attainment, tier, accelerator, and payout calculations |
| 5 | Reconciliation and QA | Compensation requires payroll-grade control | Validation checks, payout tie-outs, reasonableness tests, and exception review |
| 6 | Performance and payout analysis | Payouts should be explainable, not just calculated | Distribution, variance, productivity, and cost insights |
| 7 | Scenario and sensitivity analysis | Management needs to understand plan-cost and behavior tradeoffs | What-if analysis of targets, thresholds, rates, caps, and performance changes |
| 8 | Management reporting and recommendations | Analysis must support action | Executive summary, findings, risks, recommendations, and interview-ready narrative |
| 9 | Power BI dashboard | Interactive visualization improves ongoing monitoring | **Pending** — dashboard model, visuals, and screenshots will be added later |

Detailed documentation is available in [`docs/project-phases.md`](docs/project-phases.md).

## Analytical Workflow

### 1. Establish the business and plan context

The first step is to identify who uses the output and what decisions depend on it. Typical stakeholders include Sales Leadership, Finance, Payroll, HR, Compensation, and Sales Operations.

The analytical process distinguishes between three different concepts:

- **Performance:** what the participant sold or achieved.
- **Attainment:** performance relative to the assigned target.
- **Payout:** the incentive amount produced by the compensation formula.

Keeping these concepts separate is essential because a participant can have strong raw sales but low attainment if the quota is higher, or strong attainment but a different payout because of plan weighting, thresholds, tiers, accelerators, caps, or eligibility rules.

### 2. Build the analytical data model

The project treats compensation analysis as a small relational model rather than a single flat calculation sheet. Typical logical datasets include:

- participant / employee master;
- performance or transaction data;
- quota / target data;
- compensation-plan parameters;
- eligibility or assignment data;
- calculated payout output;
- exception / validation output.

The most important design decision is **grain**. Each dataset must have a clearly defined row-level meaning, such as one row per participant per month, one row per transaction, or one row per plan measure per participant-period.

See [`docs/data-model.md`](docs/data-model.md) and [`docs/calculation-logic.md`](docs/calculation-logic.md).

### 3. Prepare and validate data

Before calculating compensation, the project checks for conditions such as:

- missing participant IDs;
- missing targets;
- duplicate transactions or participant-period rows;
- invalid or inconsistent dates;
- non-eligible participants;
- unmatched plan assignments;
- negative or unusual values;
- inconsistent source totals;
- records outside the compensation period.

The goal is to isolate data-quality problems before they become payout problems.

### 4. Calculate attainment and incentive earnings

The core analytical flow is:

**Eligible performance ÷ target = attainment → plan tier / rate → calculated incentive payout**

Depending on plan design, the model can also support:

- multiple weighted measures;
- minimum thresholds;
- target payouts;
- tiered commission rates;
- accelerators above target;
- decelerators below target;
- caps or maximum payouts;
- guarantees or draws;
- period-level adjustments;
- exception overrides with documented reasons.

The calculations are intentionally separated into intermediate steps so that the final payout can be audited.

### 5. Reconcile and quality-check the output

A compensation calculation is not considered complete when the formula returns a number. The output must be validated.

The QA process includes:

- source-to-model total reconciliation;
- participant count reconciliation;
- target and plan assignment completeness;
- duplicate and missing-key checks;
- reasonableness testing for extreme payouts;
- payout distribution review;
- zero-payout and maximum-payout review;
- manual spot checks;
- comparison of independently calculated control totals where possible.

See [`docs/qa-and-controls.md`](docs/qa-and-controls.md).

### 6. Analyze performance and compensation outcomes

Once payouts are validated, the output becomes a management dataset. The analysis can answer questions such as:

- What percentage of participants achieved target?
- How is attainment distributed across the population?
- Which participants or teams are materially above or below plan?
- What is the relationship between performance and payout?
- Where are compensation costs concentrated?
- Are there unusual payout-to-sales relationships?
- Which records require operational investigation?

This turns the project from a calculation exercise into a compensation analytics solution.

### 7. Perform scenario analysis

Scenario analysis evaluates how compensation cost or participant outcomes may change if assumptions change. Examples include:

- increasing or decreasing targets;
- moving an accelerator threshold;
- changing a commission rate;
- applying a payout cap;
- changing the mix of weighted measures;
- simulating stronger or weaker sales performance.

The objective is not to recommend arbitrary plan changes. It is to show management the measurable tradeoff between **motivation, attainability, differentiation, and compensation cost**.

### 8. Communicate the result

The final output is designed to support both technical and business audiences. The project therefore documents:

- the business problem;
- the compensation logic;
- the data model;
- the calculation sequence;
- the QA framework;
- analytical findings;
- scenario results;
- limitations and assumptions;
- recommendations and next steps.

An interview-oriented explanation is included in [`docs/interview-walkthrough.md`](docs/interview-walkthrough.md).

## Synthetic Dataset

All project data is synthetic. The dataset was designed to resemble the types of inputs a Sales Compensation Analyst may work with—participant attributes, sales/performance, quotas, plan parameters, eligibility, calculated payout, and QA exceptions—without using real employee, payroll, or confidential company information.

The final source files will be stored in [`data/`](data/) so that the Excel, SQL, and Power BI workflow can be reproduced from the same public portfolio dataset.

## Tools and Skills Demonstrated

- **Excel:** structured calculations, lookups, reconciliation, exception flags, scenario analysis, summary reporting
- **SQL:** joins, aggregations, validation queries, participant-period calculations, exception detection
- **Power BI:** data model and dashboard visualization — **pending**
- **Data modeling:** fact/dimension thinking, grain definition, key relationships
- **Sales compensation:** quota attainment, incentive calculation, tiers, accelerators, caps, eligibility, payout validation
- **Analytics:** variance analysis, distribution analysis, exception analysis, sensitivity testing
- **Business communication:** management summaries, audit explanations, recommendations, stakeholder-oriented storytelling

## Power BI — Pending

The Power BI layer will be added after the calculation and QA workflow is finalized. Planned dashboard sections include:

- Executive Overview
- Attainment Distribution
- Payout Distribution
- Participant / Team Performance
- Compensation Cost Analysis
- Exceptions and QA
- Scenario Comparison

### Dashboard Image Placeholder — Executive Overview

> **Power BI screenshot will be added here.**

<!-- When ready, replace the placeholder above with:
![Power BI Executive Overview](assets/power-bi/executive-overview.png)
-->

### Dashboard Image Placeholder — Attainment & Payout Analysis

> **Power BI screenshot will be added here.**

<!-- When ready, replace the placeholder above with:
![Power BI Attainment and Payout Analysis](assets/power-bi/attainment-payout.png)
-->

### Dashboard Image Placeholder — QA / Exceptions

> **Power BI screenshot will be added here.**

<!-- When ready, replace the placeholder above with:
![Power BI QA and Exceptions](assets/power-bi/qa-exceptions.png)
-->

See [`powerbi/README.md`](powerbi/README.md) for the planned dashboard structure.

## Repository Structure

```text
sales-compensation-analysis/
│
├── README.md
├── PROJECT_STATUS.md
├── .gitignore
│
├── docs/
│   ├── business-problem.md
│   ├── project-phases.md
│   ├── data-model.md
│   ├── calculation-framework.md
│   ├── qa-and-controls.md
│   ├── scenario-analysis.md
│   └── interview-walkthrough.md
│
├── data/
│   └── README.md
│
├── excel/
│   └── README.md
│
├── sql/
│   ├── README.md
│   └── example-analysis-queries.sql
│
├── powerbi/
│   └── README.md
│
└── assets/
    └── power-bi/
        └── .gitkeep
```

## What the Project Demonstrates

The most important capability demonstrated by this project is the ability to move beyond dashboarding and treat compensation as a controlled business process.

The project shows how an analyst can:

1. interpret a business rule;
2. translate it into structured data and calculation logic;
3. validate the result independently;
4. identify exceptions before downstream use;
5. explain why a participant received a particular result;
6. assess the cost and behavioral implications of plan assumptions;
7. communicate the output to management.

That combination of analytical rigor, business understanding, and stakeholder communication is central to Sales Compensation Analytics.

## Current Status

The core project documentation and analytical workflow are complete. The Power BI visualization layer is still in progress.

See [`PROJECT_STATUS.md`](PROJECT_STATUS.md) for the implementation checklist.
