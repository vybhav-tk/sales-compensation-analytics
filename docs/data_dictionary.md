# Data Dictionary

This document describes the main logical tables used in the Sales Compensation & Incentive Analytics portfolio project.

A central design principle is **grain discipline**:

> Every table should have a clear definition of what one row represents.

---

# Master and Organization Tables

## Employee_Master

**Grain:** one row per employee.

Purpose:

Stores the core employee identity and employment attributes used throughout the compensation model.

Typical fields:

- Employee_ID
- Employee_Name
- Role
- Hire_Date
- Termination_Date
- Employment_Status

Primary key:

**Employee_ID**

---

## Organization_Assignment

**Grain:** one employee × effective organization-assignment period.

Purpose:

Tracks manager and region assignments over time.

Typical fields:

- Employee_ID
- Manager_ID
- Region_ID
- Effective_Start_Date
- Effective_End_Date

This table supports mid-year manager or region changes without overwriting historical hierarchy.

---

## Region

**Grain:** one row per region.

Typical fields:

- Region_ID
- Region_Name

Modeled regions:

- Ontario
- Quebec
- West
- Atlantic

---

# Planning and Rule Tables

## Company_Financial_Plan

**Grain:** one row per fiscal year.

Purpose:

Stores the Finance sales-plan target used for quota-coverage analysis.

Typical fields:

- Fiscal_Year
- Sales_Plan
- Target_Quota_Coverage
- Approved_Gross_Quota

---

## Annual_Quota_Assignment

**Grain:** one employee × fiscal year.

Purpose:

Stores the approved annual nominal quota before monthly allocation and lifecycle adjustments.

Typical fields:

- Employee_ID
- Fiscal_Year
- Annual_Nominal_Quota
- Effective_Start_Date
- Effective_End_Date

---

## Quota_Seasonality

**Grain:** one row per month.

Purpose:

Allocates annual quota into monthly nominal quota.

Typical fields:

- Month_Number
- Month_Name
- Annual_Allocation_Pct

---

## Compensation_Period

**Grain:** one row per compensation month.

Typical fields:

- Period_ID
- Period_Start_Date
- Period_End_Date
- Data_Cutoff_Date
- Payment_Date

---

## Compensation_Plan

**Grain:** one row per compensation-plan version.

Purpose:

Defines the applicable plan version and effective dates.

Typical fields:

- Plan_ID
- Plan_Name
- Effective_Start_Date
- Effective_End_Date

---

## Compensation_Tier

**Grain:** one compensation plan × tier.

Purpose:

Stores marginal commission thresholds and rates.

Typical fields:

- Plan_ID
- Tier_Number
- Attainment_From
- Attainment_To
- Commission_Rate
- Component_Type

---

## Employee_Plan_Assignment

**Grain:** one employee × plan-assignment period.

Purpose:

Determines which compensation plan is valid for an employee at a point in time.

Typical fields:

- Employee_ID
- Plan_ID
- Effective_Start_Date
- Effective_End_Date

---

## Product_Category

**Grain:** one row per product category.

Purpose:

Defines whether a product category is commissionable.

Typical fields:

- Product_Category_ID
- Product_Category_Name
- Commissionable_Flag

Example categories:

- OFFICE
- TECH
- FURN
- TSVC
- SHIP
- TAX

---

# SPIFF and Contest Tables

## SPIFF_Definition

**Grain:** one row per SPIFF program.

Typical fields:

- SPIFF_ID
- SPIFF_Name
- Start_Date
- End_Date
- Target_Method
- Target_Percentage

---

## SPIFF_Tier

**Grain:** one SPIFF × award tier.

Typical fields:

- SPIFF_ID
- Tier
- Attainment_From
- Attainment_To
- Award_Amount

---

## SPIFF_Employee_Eligibility

**Grain:** one employee × SPIFF.

Purpose:

Determines which employees are eligible to participate.

Typical fields:

- SPIFF_ID
- Employee_ID
- Eligible_Flag

---

## Contest_Definition

**Grain:** one row per sales contest.

Purpose:

Stores contest dates, eligibility conditions, ranking criteria, and award structure.

---

# Transaction Tables

## Sales_Transaction

**Grain:** one raw sales transaction event.

Purpose:

Preserves exactly what the source system reported.

Typical fields:

- Transaction_ID
- Employee_ID
- Transaction_Date
- Product_Category_ID
- Raw_Revenue
- Transaction_Type
- Transaction_Status
- Original_Transaction_ID

Important principle:

**Suspicious source transactions are preserved rather than silently deleted or overwritten.**

---

## Sales_Credit_Detail

**Grain:** one transaction evaluated for compensation.

Purpose:

Records how Sales Compensation treated each source transaction.

Typical fields:

- Transaction_ID
- Employee_ID
- Period_ID
- Raw_Revenue
- Credit_Status
- Reason_Code
- Eligible_Credited_Amount

Possible Credit_Status values:

- Eligible
- Excluded
- Review
- HOLD

This table provides the bridge between source-system revenue and compensationable revenue.

---

# Performance and Compensation Tables

## Monthly_Performance

**Grain:** one employee × compensation month.

Purpose:

Combines effective quota and credited sales to calculate monthly attainment.

Typical fields:

- Employee_ID
- Period_ID
- Effective_Monthly_Quota
- Raw_Revenue
- Eligible_Credited_Sales
- Excluded_Revenue
- Review_Rows
- HOLD_Rows
- Quota_Attainment
- Performance_Band
- Quota_Control_Status
- Sales_Credit_Control_Status
- Processing_Status

Key calculation:

**Quota_Attainment = Eligible_Credited_Sales ÷ Effective_Monthly_Quota**

---

## Commission_Tier_Detail

**Grain:** one employee × month × commission tier.

Purpose:

Explains exactly how marginal commission is calculated.

Typical fields:

- Employee_ID
- Period_ID
- Tier_Number
- Attainment_From
- Attainment_To
- Commission_Rate
- Tier_Floor_Dollars
- Tier_Ceiling_Dollars
- Sales_In_Tier
- Commission_Amount

This table is essential for payout traceability.

---

## Incentive_Award

**Grain:** one employee × incentive award.

Purpose:

Stores SPIFF or contest awards separately from regular commission.

Typical fields:

- Employee_ID
- Incentive_ID
- Incentive_Type
- Earning_Period
- Award_Tier
- Award_Amount
- Calculation_Status

---

## Compensation_Adjustment

**Grain:** one adjustment record.

Purpose:

Stores later-cycle corrections without overwriting original compensation.

Typical fields:

- Adjustment_ID
- Employee_ID
- Original_Earning_Period
- Processing_Period
- Reason_Code
- Adjustment_Amount
- Approval_Status
- Approved_By
- Approval_Date
- Notes

---

# Control Tables

## Compensation_Exception

**Grain:** one detected exception.

Purpose:

Creates an auditable case register for issues that require investigation.

Typical fields:

- Exception_ID
- Employee_ID
- Period_ID
- Exception_Type
- Related_Transaction_ID
- Severity
- Blocking_Flag
- Related_Sales_Amount
- Working_Comp_Amount
- Exception_Status
- Resolution_Action
- Description

---

## Compensation_Payout

**Grain:** one employee × payout period.

Purpose:

Combines approved compensation components into the final payout result.

Typical components include:

- regular commission
- SPIFF
- contest award
- approved adjustment

Important distinction:

**Calculated compensation and approved compensation are not the same thing.**

---

# Power BI Reporting Tables

The reporting layer simplifies the operational model into a star schema.

## Dim_Employee

**Grain:** one employee.

Used for:

- employee slicers
- role
- region
- annual quota attributes

---

## Dim_Date

**Grain:** one calendar date.

Used for:

- transaction date
- compensation month
- SPIFF period
- payroll date
- forecast month

---

## Dim_Product_Category

**Grain:** one product category.

Used for product/category sales-credit analysis.

---

## Dim_Scenario

**Grain:** one forecast scenario.

Values:

- Downside — 90%
- Plan — 100%
- Upside — 110%
- High Upside — 120%

---

## Fact_Sales_Credit

**Grain:** one transaction.

Used for:

- raw revenue
- eligible credited sales
- exclusions
- product analysis
- transaction controls

---

## Fact_Monthly_Performance

**Grain:** one employee × month.

Used for:

- effective quota
- quota attainment
- performance bands
- base commission
- accelerator commission
- working core commission

---

## Fact_SPIFF

**Grain:** one employee × SPIFF period.

Used for:

- target
- target attainment
- award tier
- SPIFF cost

---

## Fact_Exceptions

**Grain:** one exception.

Used for:

- exception counts
- severity
- blocked dollars
- operational investigation

---

## Fact_Payroll

**Grain:** one compensation component.

Used for:

- working amount
- approval status
- approved amount
- payroll eligibility

---

## Fact_Forecast_Monthly

**Grain:** one scenario × month.

Used for:

- forecast sales
- forecast commission
- accelerator premium
- scenario compensation rate
