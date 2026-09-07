# Metric Dictionary Specification

## 1. Purpose

This document defines and standardizes the metrics required by the Analytical Requirements in `04-analytical-requirement.md`.

The Metric Dictionary ensures that each metric has:

* one clear business meaning;
* one consistent calculation logic;
* one defined analytical population;
* one defined grain;
* one defined time interpretation;
* explicit filtering and edge-case rules.

The document provides the bridge between:

`Analytical Requirement -> Metric -> Data Requirement`

This document must not:

* calculate actual metric values;
* provide analytical findings;
* perform EDA;
* create dashboard visuals;
* define complete SQL pipelines;
* design Data Warehouse architecture;
* define ETL/ELT implementation.

---

# 2. Required Input

The primary input is:

`04-analytical-requirement.md`

Use primarily:

* `AR ID`;
* `Related BQ`;
* `Required Metrics`;
* `Unit of Analysis`;
* `Eligible Population`;
* `Analysis Period`;
* `Baseline / Comparator`;
* `Dimensions`;
* `Filters & Exclusions`;
* `Analytical Approach`.

Where necessary, trace back to:

* `03-business-question.md`;
* `02-business-problem.md`.

Do not create metrics that do not support a documented Analytical Requirement unless they are explicitly classified as a supporting or guardrail metric.

---

# 3. Metric Identification

Assign stable identifiers:

`MET-01`, `MET-02`, ...

Each metric must have one canonical definition.

Do not create duplicate metrics with different names when they represent the same business concept.

Example:

Avoid:

* `Revenue`
* `Total Revenue`
* `Sales Revenue`

as three separate metrics unless their business definitions materially differ.

---

# 4. Metric Classification

Each metric should be classified using two separate dimensions.

## 4.1 Metric Role

Use one of:

* **Core KPI**
* **Supporting Metric**
* **Guardrail Metric**
* **Diagnostic Metric**

### Core KPI

Directly measures the primary business outcome.

### Supporting Metric

Provides additional context for a Core KPI.

### Guardrail Metric

Helps ensure improvement in one area does not create unacceptable deterioration elsewhere.

### Diagnostic Metric

Helps investigate possible drivers or components of a Core KPI.

---

## 4.2 Metric Domain

Examples:

* Revenue.
* Profitability.
* Customer.
* Product.
* Operations.
* Fulfillment.
* Retention.
* Conversion.
* Seller / Vendor.
* Risk.

Use only domains relevant to the project.

---

# 5. Metric Type

Do not assume every metric is a ratio.

Classify each metric as one of:

* Count.
* Distinct Count.
* Sum.
* Ratio.
* Rate.
* Average.
* Median.
* Percentile.
* Index.
* Snapshot.
* Derived Metric.

The formula must match the metric type.

Examples:

### Sum

`Revenue = SUM(Eligible Revenue Amount)`

### Average

`Average Order Value = Eligible Revenue / Eligible Orders`

### Rate

`Return Rate = Returned Eligible Units / Eligible Units`

### Count

`Total Orders = COUNT(DISTINCT Eligible Order ID)`

Do not force numerator/denominator logic onto metrics where it does not apply.

---

# 6. Business Definition

Every metric must have a plain-language business definition.

The definition should answer:

> What real business concept does this metric represent?

Example:

Weak:

> Return Rate is the rate of returns.

Better:

> Return Rate represents the proportion of eligible sold units that were subsequently returned under the defined return rules.

Do not include implementation-specific SQL syntax in the business definition.

---

# 7. Mathematical Definition

Define the metric mathematically.

Where applicable, specify:

* numerator;
* denominator;
* aggregation function;
* distinct-count behavior;
* weighting;
* derived components.

Examples:

### Ratio / Rate

`Metric = Numerator / Denominator`

### Average

`Metric = Total Eligible Value / Eligible Entity Count`

### Sum

`Metric = SUM(Eligible Value)`

### Distinct Count

`Metric = COUNT(DISTINCT Eligible Entity ID)`

Do not append `× 100` by default to ratio/rate metrics.

---

# 8. Percentage Convention

Unless the user or target BI system explicitly requires another representation:

* store ratios/rates internally on a `0–1` scale;
* use percentage formatting only for display.

Example:

`0.2537`

represents:

`25.37%`

Do not calculate:

`0.2537 × 100 = 25.37`

and then also apply `%` formatting.

This prevents double scaling.

---

# 9. Eligible Population

Define the population used by the metric.

Examples:

* delivered orders;
* customers with at least one completed purchase;
* active sellers;
* valid order items;
* eligible customer cohorts.

Population rules must align with the related Analytical Requirement.

Do not silently change the population between different reports.

---

# 10. Inclusion & Exclusion Rules

## 10.1 Inclusion Rules

Define conditions required for records to participate.

Example:

`order_status = 'delivered'`

---

## 10.2 Exclusion Rules

Examples:

* test records;
* cancelled orders;
* invalid transactions;
* duplicate business keys;
* records outside the analysis window.

Do not invent exclusions not supported by business rules or analytical requirements.

If exclusion logic is unknown:

`TBD`

---

# 11. Grain Definition

For each metric, distinguish:

## 11.1 Source Grain

What does one row in the source represent?

Example:

`1 row per order item`

---

## 11.2 Unit of Analysis

What business entity is being measured?

Example:

`Order`

---

## 11.3 Reporting Grain

At what level will the metric commonly be aggregated?

Example:

`Month × Product Category`

Do not assume these three grains are identical.

This distinction is required when incorrect aggregation could cause double counting.

---

# 12. Time Semantics

For time-dependent metrics, define:

* relevant event date;
* reporting date;
* analysis window;
* cohort date where applicable;
* late-arriving or post-period events where relevant.

Examples:

Revenue may use:

`order_purchase_date`

Returns may use either:

* original sale period; or
* return event period.

The selected rule must be explicit.

If the correct business rule is unknown:

`TBD`

Do not silently choose a time field.

---

# 13. Null & Edge-Case Handling

Define behavior explicitly.

Possible cases:

* null numerator;
* null denominator;
* denominator = 0;
* missing entity key;
* duplicate transaction;
* negative amount;
* refunded order;
* partially returned order.

Do not write ambiguous rules such as:

`Return 0 or NULL`

Select one rule.

### Default Ratio Rule

When the eligible denominator is zero and the metric is mathematically undefined:

`Return NULL / BLANK`

unless business semantics explicitly require another treatment.

`0%`

must not be used when no eligible population exists, because it implies an observed zero rate.

---

# 14. Supported Dimensions

List dimensions on which the metric may validly be analyzed.

Examples:

* Time.
* Geography.
* Customer Segment.
* Product Category.
* Seller.
* Channel.

Only include dimensions that:

1. are required by downstream Analytical Requirements; and
2. can reasonably be supported by the available or required data.

Do not use the Metric Dictionary as a catalog of every possible dataset column.

---

# 15. Metric Dependencies

Derived metrics should identify required component metrics.

Example:

`MET-03 Gross Margin %`

depends on:

* `MET-01 Revenue`
* `MET-02 Gross Profit`

Represent:

`MET-03 <- MET-01, MET-02`

Avoid duplicating component logic independently across multiple metrics.

---

# 16. Implementation Reference

Implementation logic is optional.

Include SQL or DAX only when:

* the user explicitly requests it; or
* the available schema is sufficiently defined to avoid invented fields.

Implementation examples must remain secondary to the semantic metric definition.

If implementation cannot be safely defined:

`Implementation Reference: TBD`

### SQL Dialect

When SQL is provided, identify:

* PostgreSQL;
* SQL Server;
* BigQuery;
* Snowflake;
* other specified dialect.

Do not present pseudo-SQL as production-ready SQL without labeling it.

---

# 17. Metric Feasibility

Classify each metric as:

* **Ready**
* **Partially Defined**
* **Blocked**
* **TBD**

### Ready

Business logic and required data are sufficiently defined.

### Partially Defined

Metric concept is valid, but one or more rules remain unresolved.

### Blocked

Required business rule or required data is unavailable.

### TBD

Definition is not yet sufficiently developed.

Do not classify a metric as Ready solely because its name is known.

---

# 18. Required Metric Master Table

The final document must include:

| Metric ID | Metric Name | Business Definition | Metric Role | Metric Type | Related AR | Status |
| --------- | ----------- | ------------------- | ----------- | ----------- | ---------- | ------ |

## Required Columns

At minimum:

* `Metric ID`
* `Metric Name`
* `Business Definition`
* `Metric Type`
* `Related AR`
* `Status`

`Metric Role` is recommended.

---

# 19. Detailed Metric Specification

Use the following structure for each metric.

## MET-XX — [Metric Name]

### Related Analytical Requirement

`AR-XX`

### Business Definition

[...]

### Metric Role

`Core KPI / Supporting / Guardrail / Diagnostic`

### Metric Domain

[...]

### Metric Type

[...]

### Mathematical Definition

[...]

### Numerator

[Required only when applicable.]

### Denominator

[Required only when applicable.]

### Eligible Population

[...]

### Inclusion Rules

* [...]

### Exclusion Rules

* [...]

### Source Grain

[...]

### Unit of Analysis

[...]

### Reporting Grain

[...]

### Time Semantics

* Event Date:
* Reporting Date:
* Analysis Window:
* Late-arriving Treatment:

### Null & Edge-Case Handling

* [...]

### Supported Dimensions

* [...]

### Metric Dependencies

[Optional]

### Display Unit

Examples:

* Currency.
* Percentage.
* Count.
* Days.
* Score.

### Display Format

Examples:

* `0.00%`
* `#,##0`
* `#,##0.00`
* Currency format.

### Implementation Reference

[Optional / TBD]

### Metric Status

`Ready / Partially Defined / Blocked / TBD`

### Assumptions & Limitations

* [...]

---

# 20. Traceability Summary

Maintain:

`BQ -> AR -> MET`

Provide:

| Business Question | Analytical Requirement | Metric |
| ----------------- | ---------------------- | ------ |

Metrics may be reused across multiple Analytical Requirements.

Do not duplicate a metric merely because multiple ARs use it.

This document becomes an input for:

`06-data-requirements-quality.md`

---

# 21. Practice / Review Rules

When the user submits their own Metric Dictionary for review:

1. Identify the metrics actually defined by the user.
2. Match their meaning against the semantic requirements in this reference.
3. Do not mark a metric incorrect merely because optional headings are absent.
4. Validate whether each metric supports the related Analytical Requirement.
5. Check mathematical consistency before formatting.
6. Specifically verify:

   * metric type;
   * population;
   * numerator/denominator where applicable;
   * grain;
   * percentage convention;
   * null handling;
   * time semantics.
7. Separate feedback into:

   * Correct.
   * Needs revision.
   * Missing required logic.
   * Optional enhancement.
8. Do not rewrite the user's metric definitions unless explicitly requested.

---

# 22. Definition of Done

Before returning the document, verify:

* [ ] Every primary metric supports at least one Analytical Requirement.
* [ ] Duplicate semantic metrics have been consolidated.
* [ ] Metric type matches its mathematical definition.
* [ ] Sum/count metrics are not incorrectly forced into ratio formulas.
* [ ] Ratio/rate percentage representation is consistent.
* [ ] Eligible population is explicit where material.
* [ ] Inclusion and exclusion rules are unambiguous.
* [ ] Source Grain, Unit of Analysis, and Reporting Grain are not silently conflated.
* [ ] Time semantics are explicit for time-dependent metrics.
* [ ] Zero-denominator behavior is unambiguous.
* [ ] Unsupported business rules or fields have not been invented.
* [ ] Supported dimensions are analytically relevant.
* [ ] Metric dependencies are documented where required.
* [ ] Metric feasibility/status reflects actual definition readiness.
* [ ] Metric IDs remain stable for downstream traceability.
