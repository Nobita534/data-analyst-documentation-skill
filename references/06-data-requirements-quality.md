# Data Requirements & Quality Specification

## 1. Purpose

This reference defines how to translate approved Analytical Requirements and Metrics into implementation-ready Data Requirements for Data Analysts and Analytics Engineers.

It completes the downstream analytical traceability chain:

`Analytical Requirement -> Metric -> Data Requirement`

Use this reference when creating, reviewing, refining, or extending Data Requirements and Data Quality documentation.

This document specifies **what data is required and what quality conditions must hold for the analysis to be valid**. It does not perform data profiling, cleaning, transformation, or pipeline implementation.

---

## 2. Scope

Data Requirements may define:

- Required business entities.
- Required identifiers or keys.
- Required measures.
- Required dimensions.
- Required statuses or classifications.
- Required dates and timestamps.
- Required relationships between entities.
- Required business-rule fields.
- Required derived fields at a conceptual level.
- Required data-quality conditions.
- Data availability and known gaps.
- Analytical-readiness constraints.

Data Requirements must not:

- Perform actual data profiling or calculate quality rates.
- Execute SQL, Python, DAX, dbt, or ETL logic.
- Design detailed production ETL/ELT pipelines.
- Design detailed star schemas, SCD strategies, medallion layers, orchestration, or cloud architecture unless explicitly requested in another scope.
- Invent physical field names, data types, keys, relationships, cardinalities, thresholds, SLA values, or business rules that are not supported by evidence.
- Create proxy fields merely because the required business concept is unavailable.
- Present findings or recommendations as if data analysis had already been executed.

---

## 3. Input Requirements

Primary upstream inputs:

- `04-analytical-requirement.md`
- `05-metric-dictionary.md`

Trace further upstream when necessary:

- `03-business-question.md`
- `02-business-problem.md`
- `01-business-context.md`

Every Data Requirement must support at least one of the following:

- An Analytical Requirement.
- A Metric.
- A clearly stated analytical constraint.

Do not create a Data Requirement merely because a field or table exists in the schema.

---

## 4. Identifier Convention

Use stable IDs:

- `DR-01`
- `DR-02`
- `DR-03`

Do not renumber existing Data Requirements when extending an established specification unless explicitly requested.

A single Analytical Requirement or Metric may map to multiple Data Requirements.

A single Data Requirement may support multiple Analytical Requirements or Metrics when the same data concept is genuinely shared.

---

## 5. Data Requirement Categories

Classify each Data Requirement into one or more categories when useful:

- **Entity** — business object required by the analysis.
- **Identifier / Key** — identifier needed to distinguish or relate business entities.
- **Measure** — numeric value required for a metric or analytical calculation.
- **Dimension** — descriptive attribute required for segmentation, comparison, or grouping.
- **Status / Classification** — categorical field that determines business state or eligibility.
- **Date / Timestamp** — event or reporting time required for period logic.
- **Relationship** — entity linkage required to combine relevant business concepts.
- **Business Rule Field** — field required to apply an explicit business rule.
- **Derived Field** — conceptually derived attribute required by the analysis.
- **Data Quality Requirement** — condition required for analytical correctness.

A requirement may have one primary category and additional supporting roles.

---

## 6. Required Entity Specification

For each required business entity, document where applicable:

- Entity name.
- Business meaning.
- Source or source table when known.
- Source grain.
- Identifier(s) when known.
- Related Analytical Requirement(s).
- Related Metric(s).
- Availability status.

Examples of business entities:

- Customer.
- Order.
- Product.
- Seller.
- Payment.
- Accident.
- Store.

Do not invent physical source tables when only the business entity is known.

If the entity is conceptually required but not present in the available schema, mark it as `Missing` rather than fabricating a source.

---

## 7. Required Field Specification

For each required field, define where applicable:

- Conceptual field name.
- Business meaning.
- Related entity.
- Related Analytical Requirement ID.
- Related Metric ID.
- Analytical role.
- Physical source field, if confirmed.
- Availability status.
- Data type, only if supported by the schema or authoritative metadata.
- Known limitations.

### Conceptual vs Physical Fields

Use conceptual field names when the analytical need is known but the physical implementation is not.

Example:

- Conceptual field: `Order Completion Timestamp`
- Physical field: `TBD`

Do not invent a physical column name such as `completed_at` unless it is present in the supplied schema or authoritative source.

---

## 8. Availability Status

Use one of the following statuses:

- **Available** — the required data is supported by the supplied schema or authoritative source.
- **Partially Available** — some but not all required data components are available.
- **Missing** — the required data is not present in the available source.
- **TBD** — availability cannot yet be determined.

Availability must be evidence-based.

Do not mark a requirement Available solely because a similarly named field exists.

---

## 9. Source Grain

Document source grain separately from Unit of Analysis and Reporting Grain.

Examples:

- One row per order item.
- One row per payment transaction.
- One row per customer snapshot.
- One row per accident.

If source grain is unknown, use `TBD`.

Do not infer grain from table names alone.

Do not silently treat source grain as analytical grain.

---

## 10. Identifiers and Keys

Document identifiers only when supported.

Possible roles include:

- Business identifier.
- Primary key.
- Foreign key.
- Composite key.
- Natural key.

If key semantics are not explicitly supported by the schema or documentation, do not label a field as a primary or foreign key.

Use:

`Key role: TBD`

when the identifier exists but its formal relationship semantics are not known.

---

## 11. Relationship Requirements

Document relationships required to answer the analysis.

Recommended format:

| From Entity | From Key | To Entity | To Key | Cardinality | Status |
|---|---|---|---|---|---|
| ... | ... | ... | ... | ... | ... |

Use relationship status values such as:

- **Confirmed** — explicitly documented by an authoritative source.
- **Schema-derived** — directly supported by schema metadata.
- **Assumed** — plausible but not confirmed; must be clearly labeled.
- **TBD** — relationship cannot yet be determined.

Do not invent cardinality.

If the business need requires a relationship but the join path is unknown, document the relationship requirement conceptually and mark the implementation as `TBD`.

### Join Purpose

Explain why a relationship is needed in business terms.

Example:

`Customer-to-order linkage is required to calculate customer-level repeat-purchase metrics.`

Do not write production SQL join logic unless explicitly requested.

---

## 12. Time Field Requirements

Time-dependent metrics and analyses must identify the required time concept.

Examples:

- Order creation date.
- Delivery timestamp.
- Reporting date.
- Snapshot date.
- Cohort start date.

The required time field must align with the Time Semantics defined in `05-metric-dictionary.md`.

Do not substitute one date for another merely because it is available.

Example:

`Order purchase timestamp` is not automatically equivalent to `delivery timestamp`.

If the required event date is unavailable, mark the requirement accordingly.

---

## 13. Derived Field Requirements

A derived field may be documented when the analysis requires a concept that can be obtained from supported source data.

For each derived field, define:

- Derived field name.
- Business meaning.
- Source inputs.
- Conceptual transformation.
- Related AR/MET.
- Assumptions or limitations.

Keep transformation logic conceptual unless the user explicitly requests implementation logic.

Example:

`Repeat Customer Flag = whether an eligible customer has more than one qualifying order within the defined analysis window.`

Do not write detailed SQL or DAX by default.

---

## 14. Data Quality Requirements

Data Quality Requirements should protect analytical correctness, not become a generic enterprise-governance checklist.

Use only categories relevant to the analysis.

Possible categories include:

- **Completeness** — required values are populated when analytically necessary.
- **Uniqueness** — identifiers are unique at the required grain.
- **Validity** — values conform to allowed business or schema rules.
- **Referential Integrity** — required relationships resolve correctly.
- **Consistency** — related fields or sources do not contradict each other.
- **Timeliness** — data is available within the analytical reporting need.

Each quality rule should answer:

`What must be true for this analysis or metric to remain valid?`

Do not add quality checks that have no analytical consequence.

---

## 15. Data Quality Thresholds

Do not invent numeric thresholds.

If a threshold is required but not defined, use:

`Threshold: TBD`

Examples of invalid behavior:

- `Missing rate must be below 5%` when no such standard is provided.
- `Freshness must be under 24 hours` without a business SLA.

Examples of acceptable requirements:

- `Customer identifier must be present for records included in customer-level analysis.`
- `Order identifier must be unique at the stated order grain.`
- `Threshold for acceptable missingness: TBD.`

---

## 16. Data Quality Assessment Status

When actual profiling results are available from an authoritative source, quality may be classified as:

- **Pass**
- **Warning**
- **Fail**
- **Unknown**

If no profiling has been performed, use:

`Not Assessed`

Do not infer Pass/Fail status from schema structure alone.

This reference defines quality requirements; it does not perform the profiling itself.

---

## 17. Missing Data and Analytical Impact

For each material missing data requirement, document:

- Missing concept.
- Related AR/MET.
- Analytical impact.
- Whether the analysis is still partially possible.
- Valid fallback, if one exists.
- Limitation introduced by the fallback.

Do not automatically create a proxy.

A proxy is acceptable only when its business meaning reasonably represents the missing concept.

Example of an invalid proxy:

`Cancellation timestamp` used as a proxy for `cancellation reason`.

These represent different business concepts.

If no valid proxy exists, state:

`No valid proxy identified.`

---

## 18. Analytical Feasibility

Classify downstream analytical readiness as:

- **Ready** — required data is available and quality requirements can be supported.
- **Partially Ready** — material gaps or limitations remain, but part of the analysis is feasible.
- **Blocked** — a critical data requirement is unavailable or unsupported.
- **TBD** — readiness cannot yet be determined.

Feasibility must be tied to the affected Analytical Requirement or Metric.

Do not classify the entire dataset globally when different Analytical Requirements have different readiness levels.

---

## 19. Optional Data Platform Requirements

Only include high-level data-platform requirements when the project context explicitly includes DWH, ETL, ELT, or analytical-platform readiness.

Acceptable examples:

- Historical data must be retained for the required comparison window.
- Required source entities must be integrated into an analytical layer.
- Transformation logic for a shared business definition must be consistent across reporting outputs.

Do not expand this section into detailed engineering design by default.

Avoid unsupported decisions about:

- Star schema design.
- SCD types.
- Medallion architecture.
- Cloud services.
- Orchestration tools.
- Storage engines.

Those belong to a separate Data Engineering or architecture scope.

---

## 20. Recommended Output Format

### Data Requirement Master Table

| DR ID | Related AR | Related Metric | Entity | Required Data | Role | Availability | Quality Requirement |
|---|---|---|---|---|---|---|---|
| DR-01 | AR-01 | MET-01 | ... | ... | ... | ... | ... |

For personal or portfolio projects, the following compact columns are sufficient when appropriate:

| DR ID | Related AR/MET | Entity | Required Data | Source Grain | Relationship | Availability | Quality Requirement |
|---|---|---|---|---|---|---|---|

### Detailed Data Requirement

#### DR-01 — [Short Requirement Name]

- **Related Analytical Requirement:** AR-01
- **Related Metric:** MET-01
- **Category:** ...
- **Entity:** ...
- **Required Data:** ...
- **Business Meaning:** ...
- **Analytical Role:** ...
- **Physical Source Field:** ...
- **Source Grain:** ...
- **Identifier / Key:** ...
- **Required Relationship:** ...
- **Time Field:** ...
- **Availability:** ...
- **Data Quality Requirement:** ...
- **Threshold:** ...
- **Quality Status:** ...
- **Known Limitation:** ...
- **Analytical Impact:** ...
- **Fallback / Proxy:** ...

Repeat for each Data Requirement.

---

## 21. Practice / Review Mode

When reviewing a user-created Data Requirements document:

1. Identify the actual Data Requirements even when headings differ from this template.
2. Identify the related Analytical Requirement and Metric.
3. Check whether every Data Requirement is analytically necessary.
4. Check whether conceptual and physical field names are clearly distinguished.
5. Check whether source grain is correctly understood.
6. Check keys and relationships for unsupported assumptions.
7. Check time fields against Metric time semantics.
8. Check whether derived fields are conceptually valid and supported.
9. Check whether quality rules protect analytical correctness.
10. Check whether numeric quality thresholds are supported or correctly marked `TBD`.
11. Check missing-data impact and reject invalid proxies.
12. Check analytical feasibility.
13. Classify findings as:
   - Correct
   - Needs revision
   - Missing required content
   - Optional enhancement
14. Do not rewrite the document unless explicitly requested.

---

## 22. Traceability Rules

Maintain the chain:

`PROB -> DEC -> OBJ -> BQ -> AR -> MET -> DR`

Rules:

- Every `DR` must support at least one `AR`, `MET`, or explicit analytical constraint.
- Data fields must exist because an analytical requirement needs them, not merely because they exist in the source.
- Relationship requirements must support an analytical join or metric dependency.
- Quality requirements must protect the correctness of a specific analytical requirement, metric, or data dependency.
- Missing data must be connected to its analytical impact.

Avoid orphan Data Requirements.

---

## 23. Definition of Done

A Data Requirements & Quality specification is complete when:

- [ ] Every DR has a stable `DR-xx` ID.
- [ ] Every DR traces to an Analytical Requirement, Metric, or explicit analytical constraint.
- [ ] Required entities are defined with business meaning.
- [ ] Required data is described conceptually even when physical fields are unknown.
- [ ] Physical field names are not invented.
- [ ] Source grain is documented or marked `TBD`.
- [ ] Key semantics are supported or marked `TBD`.
- [ ] Relationships and cardinalities are not invented.
- [ ] Time fields align with Metric time semantics.
- [ ] Derived fields are conceptually defined without unnecessary implementation code.
- [ ] Data Quality Requirements are tied to analytical correctness.
- [ ] Unsupported numeric thresholds are not invented.
- [ ] Quality status is `Not Assessed` when no profiling evidence exists.
- [ ] Missing data and analytical impact are visible.
- [ ] Invalid proxy fields are not proposed.
- [ ] Feasibility is classified where possible.
- [ ] Optional DWH / ETL / ELT requirements remain high-level and within scope.
- [ ] No actual profiling results, KPI values, findings, or recommendations are fabricated.
