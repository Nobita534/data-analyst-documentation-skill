# Analytical Requirement Specification

## 1. Purpose

This reference defines how to translate approved Business Questions into implementation-oriented Analytical Requirements for Data Analysts and Analytics Engineers.

Analytical Requirements define **how the analysis should be structured** without executing the analysis.

They form the bridge:

`Business Question -> Analytical Requirement -> Metric -> Data Requirement`

Use this reference when creating, reviewing, refining, or extending Analytical Requirement documentation.

---

## 2. Scope

Analytical Requirements may define:

- Unit of analysis.
- Eligible population.
- Analysis period.
- Baseline or comparator.
- Required metrics.
- Dimensions.
- Inclusion rules.
- Exclusion rules.
- Analytical approach.
- Hypotheses and alternative explanations where relevant.
- Expected analytical output.
- Feasibility.
- Assumptions and limitations.

Analytical Requirements must not:

- Execute SQL, Python, DAX, or other analytical code.
- Calculate actual metric values.
- Perform EDA or statistical analysis.
- State findings as if analysis has been completed.
- Invent unsupported business rules, filters, thresholds, dimensions, or fields.
- Predetermine recommendations or business decisions.

---

## 3. Input Requirements

Primary upstream input:

- `03-business-question.md`

Trace back to the following when needed:

- `02-business-problem.md`
- `01-business-context.md`

Each Analytical Requirement must trace to a valid Business Question.

Before defining an Analytical Requirement, confirm that the upstream Business Question is:

- Business-oriented.
- Decision-relevant.
- Measurable.
- Within the analytical scope.

If the Business Question itself is invalid or unsupported, fix or flag the upstream issue rather than compensating for it inside the Analytical Requirement.

---

## 4. Identifier Convention

Use stable IDs:

- `AR-01`
- `AR-02`
- `AR-03`

Do not renumber existing Analytical Requirements when extending an established specification unless explicitly requested.

A single Business Question may map to one or more Analytical Requirements.

Split one Business Question into multiple Analytical Requirements only when the analytical work requires materially different analytical steps, populations, approaches, or outputs.

Do not create multiple Analytical Requirements merely to restate the same question in different wording.

---

## 5. Required Analytical Requirement Structure

Each Analytical Requirement should define the fields below where applicable.

### 5.1 Analytical Requirement ID

Stable identifier such as:

`AR-01`

---

### 5.2 Related Business Question

Reference the upstream Business Question ID.

Example:

`BQ-02`

An Analytical Requirement without a valid Business Question is an orphan requirement.

---

### 5.3 Analytical Objective

Describe what this specific analytical requirement must accomplish.

Prefer action verbs such as:

- Quantify.
- Compare.
- Identify.
- Evaluate.
- Segment.
- Assess.
- Determine.
- Validate.

Avoid vague wording such as:

- Analyze the data.
- Understand performance.
- Find insights.

The Analytical Objective should be narrower and more implementation-oriented than the upstream Business Question.

---

### 5.4 Unit of Analysis

Define the business analytical unit being evaluated.

Examples:

- Customer.
- Order.
- Product.
- Seller.
- Accident.
- Store-day.
- Product-month.

Do not automatically equate Unit of Analysis with the physical row grain of a source table.

If the unit cannot be determined safely, use `TBD`.

---

### 5.5 Eligible Population

Define the analytical universe included in the requirement.

Examples:

- Completed orders within the analysis period.
- Active customers meeting the stated eligibility rule.
- Accidents within the defined jurisdiction and time window.

Do not invent eligibility rules from schema fields alone.

If business eligibility is not defined, mark it `TBD` rather than creating an arbitrary filter.

---

### 5.6 Analysis Period

Define the period required for the analysis when time is relevant.

Examples:

- Calendar year 2025.
- Rolling 12 months ending at the reporting date.
- Order cohort from January to June 2026.

If the user or upstream documentation does not define the period, use `TBD`.

Do not infer a period merely from the minimum and maximum dates available in a dataset unless the task explicitly requests dataset-bounded analysis.

---

### 5.7 Baseline or Comparator

Required when the analytical objective implies comparison.

Examples:

- Previous period.
- Same period last year.
- Historical baseline.
- Business target.
- Another product category.
- Another customer segment.
- Control or reference group.

If comparison is necessary but the correct comparator is unknown, set:

`TBD`

Do not invent a comparator to make the requirement appear complete.

---

### 5.8 Required Metrics

List the metrics needed to answer the Analytical Requirement.

If a Metric Dictionary already exists, reference stable IDs such as:

- `MET-01`
- `MET-03`

If the Metric Dictionary has not yet been created, use provisional business metric names only.

Do not fully define metric formulas inside this document unless explicitly needed for clarification. Metric definitions belong in `05-metric-dictionary.md`.

---

### 5.9 Dimensions

Define the business dimensions needed to segment, compare, or explain the analytical result.

Examples:

- Geography.
- Product category.
- Customer segment.
- Sales channel.
- Time period.

Dimensions must be relevant to the Business Question and analytically useful.

Do not add dimensions merely because corresponding columns exist in the dataset.

---

### 5.10 Inclusion Rules

Define explicit analytical inclusion rules only when supported by business context, upstream requirements, or authoritative source material.

Examples:

- Include only delivered orders.
- Include only records within the approved analysis period.

If an inclusion rule is required but unsupported, mark it `TBD`.

---

### 5.11 Exclusion Rules

Define explicit analytical exclusions only when supported.

Examples:

- Exclude test transactions.
- Exclude records classified as invalid by an existing business rule.

Do not create exclusions based on intuition or convenience.

---

### 5.12 Analytical Approach

Define the analysis pattern required to answer the Business Question.

Possible approaches include:

- Trend analysis.
- Comparative analysis.
- Segmentation.
- Cohort analysis.
- Funnel analysis.
- RFM analysis.
- Distribution analysis.
- Ranking.
- Variance analysis.
- Correlation analysis.
- Cross-dimensional analysis.

Select the approach because it fits the analytical need, not because a method is fashionable or available.

Do not include implementation code.

---

### 5.13 Hypothesis

Optional.

Use when the analysis is intended to test a specific proposition.

Clearly label it as a hypothesis, not a fact.

Example:

`Hypothesis: lower delivery performance may be associated with lower customer review scores.`

Do not imply causality unless causal evidence or a causal analytical design is explicitly available.

---

### 5.14 Alternative Explanation

Optional but recommended when the analysis risks confirmation bias.

Document another plausible explanation that could produce the same observed pattern.

Example:

`Alternative explanation: lower review scores may be associated with product category differences rather than delivery performance.`

---

### 5.15 Expected Analytical Output

Define the structure of the expected output, not the result itself.

Examples:

- Monthly trend table by customer segment.
- Cohort retention matrix.
- Ranked product-category comparison.
- Cross-tab of risk rate by environmental condition.

Do not invent findings, values, rankings, thresholds, or conclusions.

---

### 5.16 Visualization Guidance

Optional.

Use only when a visualization type materially clarifies the expected analytical output.

Examples:

- Line chart for time trend.
- Cohort heatmap for retention.
- Scatter plot for relationship exploration.

Do not prescribe a chart when the analytical structure is better represented as a table or when visualization is not necessary.

Visualization Guidance is advisory, not a dashboard specification.

---

### 5.17 Feasibility

Classify each Analytical Requirement as one of:

- **Answerable** — required data appears available and sufficient.
- **Partially Answerable** — some components are supported but material limitations remain.
- **Blocked** — required information or data is unavailable.
- **TBD** — feasibility cannot yet be determined.

Feasibility must be evidence-based.

Do not mark a requirement Answerable solely because similarly named fields exist.

---

### 5.18 Assumptions & Limitations

Document material assumptions, unknowns, and analytical constraints.

Examples:

- Comparator remains TBD.
- Historical data is unavailable before a specific date.
- A required business classification is not present in the current schema.

Do not hide important limitations in footnotes or prose outside the formal requirement.

---

## 6. Business Question vs Analytical Requirement

Use this separation consistently.

### Business Question

Defines:

- **WHAT** the business needs answered.
- **WHY** the answer matters.

Example:

`Which customer segments show the lowest repeat-purchase behavior, and where should retention analysis be prioritized?`

### Analytical Requirement

Defines:

- **HOW** the analysis must be structured to answer that Business Question.

Example components:

- Unit of analysis: customer.
- Population: eligible customers in the approved period.
- Required metrics: repeat purchase rate, purchase frequency.
- Dimensions: customer segment, geography.
- Approach: segmentation + comparative analysis.

Do not push AR-level implementation details into the Business Question table.

---

## 7. Traceability Rules

Maintain the following chain:

`PROB -> DEC -> OBJ -> BQ -> AR -> MET -> DR`

Rules:

- Every `AR` must trace to at least one `BQ`.
- Every `MET` must support at least one `AR` unless explicitly classified as a supporting or guardrail metric.
- Every `DR` must support an `AR`, a `MET`, or a clearly stated analytical constraint.
- Do not create orphan Analytical Requirements.
- Do not create Analytical Requirements that answer a different problem from their upstream Business Question.

---

## 8. Feasibility and Missing Data Rules

When data support is incomplete:

- Do not invent fields.
- Do not invent relationships.
- Do not invent business rules.
- Do not automatically create proxy fields.

A proxy may be proposed only when its business meaning reasonably represents the missing concept.

If a valid proxy is unavailable, state:

`No valid proxy identified.`

If physical implementation details are unknown, document the conceptual analytical requirement and defer the mapping to `06-data-requirements-quality.md`.

---

## 9. Recommended Output Format

### Analytical Requirement Summary

| AR ID | Related BQ | Analytical Objective | Unit of Analysis | Required Metrics | Analytical Approach | Feasibility |
|---|---|---|---|---|---|---|
| AR-01 | BQ-01 | ... | ... | ... | ... | ... |

### Detailed Analytical Requirement

#### AR-01 — [Short Requirement Name]

- **Related Business Question:** BQ-01
- **Analytical Objective:** ...
- **Unit of Analysis:** ...
- **Eligible Population:** ...
- **Analysis Period:** ...
- **Baseline / Comparator:** ...
- **Required Metrics:** ...
- **Dimensions:** ...
- **Inclusion Rules:** ...
- **Exclusion Rules:** ...
- **Analytical Approach:** ...
- **Hypothesis:** ...
- **Alternative Explanation:** ...
- **Expected Analytical Output:** ...
- **Visualization Guidance:** ...
- **Feasibility:** ...
- **Assumptions & Limitations:** ...

Repeat for each Analytical Requirement.

---

## 10. Practice / Review Mode

When reviewing a user-created Analytical Requirement document:

1. Identify the actual Analytical Requirements even if headings differ from this template.
2. Identify the upstream Business Question for each requirement.
3. Check whether each requirement genuinely answers its Business Question.
4. Check whether Unit of Analysis and Eligible Population are conceptually correct.
5. Check whether comparison requirements have a valid baseline or `TBD`.
6. Check whether metrics and dimensions are analytically necessary rather than schema-driven additions.
7. Check whether inclusion/exclusion rules are supported.
8. Check whether the Analytical Approach fits the question.
9. Check hypotheses for confirmation bias or unsupported causality.
10. Check feasibility and limitations.
11. Classify findings as:
   - Correct
   - Needs revision
   - Missing required content
   - Optional enhancement
12. Do not rewrite the document unless explicitly requested.

---

## 11. Definition of Done

An Analytical Requirement specification is complete when:

- [ ] Every AR has a stable `AR-xx` ID.
- [ ] Every AR traces to a valid Business Question.
- [ ] Analytical Objective is specific and implementation-oriented.
- [ ] Unit of Analysis is defined or marked `TBD`.
- [ ] Eligible Population is defined or marked `TBD`.
- [ ] Analysis Period is defined when time-dependent or marked `TBD`.
- [ ] Required comparison has a baseline/comparator or `TBD`.
- [ ] Required Metrics are listed without duplicating the Metric Dictionary.
- [ ] Dimensions are analytically relevant.
- [ ] Inclusion and Exclusion Rules are supported or explicitly `TBD`.
- [ ] Analytical Approach fits the Business Question.
- [ ] Hypotheses are not presented as facts.
- [ ] Expected Analytical Output describes structure, not findings.
- [ ] Feasibility is classified where possible.
- [ ] Material assumptions and limitations are visible.
- [ ] No unsupported fields, rules, thresholds, causal claims, or results are invented.
- [ ] Traceability to downstream Metrics and Data Requirements can be maintained.
