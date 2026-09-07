---

name: data-analyst-documentation-skill
description: Use this skill when the user wants to transform a business problem, stakeholder request, dataset schema, or existing analytics documentation into structured Data Analyst documentation, including business context, analytical questions, analytical requirements, metric definitions, data requirements, and data-quality specifications. Do not use this skill for direct data analysis, KPI calculation, SQL execution, dashboard building, backend/API specifications, or software-development requirements.
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Data Analyst Documentation Skill

## 1. Purpose & Scope

This skill creates structured, implementation-ready analytical documentation for Data Analysts and Analytics Engineers.

Its primary responsibility is to translate an ambiguous business request into the following traceable specification chain:

`Business Problem -> Decision -> Analysis Objective -> Business Question -> Metric -> Data Requirement`

This skill is a **documentation and specification workflow**, not a data-analysis workflow.

### In Scope

Use this skill to:

* Frame and refine business problems for analytical work.
* Identify the business decision that the analysis should support.
* Define analysis objectives.
* Define measurable Business Questions.
* Specify analytical requirements, including population, baseline, dimensions, filters, exclusions, and expected outputs.
* Define metrics and their business logic.
* Define required data entities, fields, grain, relationships, time semantics, and data-quality expectations.
* Assess whether available data can support a Business Question.
* Review, refine, or extend existing Data Analyst documentation.
* Identify ambiguity, unsupported assumptions, logical flaws, data gaps, and feasibility risks.
* Maintain traceability across analytical documents.

### Out of Scope

Do not:

* Query or execute against datasets.
* Calculate actual KPI or metric values.
* Perform EDA or statistical analysis.
* Perform root-cause analysis.
* Produce analytical findings as if analysis had already been executed.
* Generate evidence-backed recommendations without analytical results.
* Build Power BI dashboards or other visualization artifacts.
* Design backend APIs.
* Write BRD/FRD for software systems.
* Create use cases, BPMN flows, or backend architecture specifications.
* Invent business facts, dataset fields, business rules, thresholds, data types, or SLA values that are not supported by provided information.

---

## 2. Input Handling

Before generating documentation, determine what information is available.

### Minimum Input

At least one of the following must be available:

* A business problem or stakeholder request.
* Existing analytical documentation that the user wants to review or extend.

### Recommended Supporting Inputs

When available, use:

* Stakeholder or business context.
* Business decision that the analysis should support.
* Dataset schema or data dictionary.
* Available tables, entities, fields, and relationships.
* Existing Business Questions.
* Existing metrics or KPIs.
* Analysis period or reporting window.
* Business rules, exclusions, targets, or comparison baselines.

### Missing Information

Classify missing information as:

* **Blocking:** Missing information would make the specification logically invalid or materially misleading.
* **Non-blocking:** Documentation can continue if the missing information is explicitly marked.

For blocking information, ask only the minimum clarification required to continue.

For non-blocking information, continue and use one of:

* `TBD`
* `Unknown`
* `Assumption`

Do not stop the workflow merely because every field is not known.

---

## 3. Evidence & Assumption Policy

Maintain a strict distinction between evidence, stakeholder claims, assumptions, and hypotheses.

Use the following statuses when relevant:

| Status             | Meaning                                                              |
| ------------------ | -------------------------------------------------------------------- |
| **Confirmed**      | Explicitly validated by an authoritative source provided in the task |
| **User-provided**  | Stated by the user or stakeholder but not independently validated    |
| **Schema-derived** | Directly supported by the supplied dataset schema                    |
| **Hypothesis**     | Proposition that the future analysis should test                     |
| **Assumption**     | Temporary working condition required to proceed                      |
| **TBD**            | Required information has not yet been defined                        |
| **Unknown**        | Information is unavailable and cannot safely be inferred             |

### Never Invent

Never fabricate or silently infer:

* Business performance values.
* Percentages or data-quality rates.
* Financial impacts.
* Dataset tables or fields.
* Primary or foreign keys.
* Relationships between entities.
* Data types not provided by the schema.
* Metric targets.
* Threshold values.
* SLA values.
* Business rules.
* Causal relationships.
* Proxy fields.

If required information is unsupported, mark it as `TBD`, `Unknown`, or `Assumption`.

### Causality

Do not convert correlation, co-movement, temporal association, or stakeholder suspicion into causality.

Prefer wording such as:

* `is associated with`
* `coincides with`
* `the stakeholder suspects`
* `hypothesis to be tested`

unless causal evidence or an appropriate causal analytical design is explicitly available.

### Solution Bias

Do not select a business solution before analytical evidence exists.

Specify:

`Decision to be supported`

rather than:

`Action that must be taken`

The analysis may evaluate decision options, but the documentation must not predetermine the conclusion.

---

## 4. Operating Modes

Select the mode based on the user's request.

### Mode A — Scaffold

Use when creating analytical documentation from a new business problem.

Create the requested documents according to the workflow defined in Section 5.

### Mode B — Review / Refine

Use when analytical documentation already exists.

Review for:

* Logical inconsistencies.
* Unsupported claims.
* Missing decision context.
* Ambiguous Business Questions.
* Missing baselines.
* Incorrect metric logic.
* Missing data requirements.
* Data-feasibility issues.
* Broken traceability.

Preserve correct existing content.

Do not rewrite sections that do not materially need correction.

### Mode C — Extend

Use when the user wants to add Business Questions, metrics, requirements, or other documentation.

When extending:

* Preserve existing identifiers.
* Preserve established naming conventions.
* Add only the requested scope.
* Maintain traceability with existing documents.

### Delivery Mode

Follow the user's requested delivery style.

Available modes:

* **Complete:** Return all requested documentation together when practical.
* **Staged:** Produce one document at a time when explicitly requested or when the full output would be impractical.
* **Append:** Return only newly added or changed content.

Do not force one-file-per-turn when the user requests a complete deliverable.

### Mode D — Practice / Review

Use when the user submits their own analytical documentation for evaluation.

The goal is to assess the user's reasoning and document quality before suggesting improvements.

Review in this order:

1. Identify the document type.
2. Identify its upstream document.
3. Detect the user's actual core content even when headings differ from the reference template.
4. Compare the core content with the semantic requirements of the corresponding reference.
5. Validate alignment with the upstream document.
6. Identify logical, analytical, or scope issues.
7. Separate findings into:
   - Correct
   - Needs revision
   - Missing required content
   - Optional enhancement
8. Suggest additional sections only after core correctness has been evaluated.
9. Do not rewrite the document unless the user explicitly requests rewriting.

---

## 5. Execution Workflow

Follow the steps below in sequence.

### Step 1 — Parse the Request

Identify:

* Business problem or analytical request.
* Stakeholder or intended decision-maker.
* Requested deliverable.
* Explicit constraints.
* Available data/schema context.
* Existing documentation.
* Requested number of items, if specified.

If the user requests exactly `N` Business Questions, metrics, or other items, produce exactly `N`.

---

### Step 2 — Separate Facts, Claims, and Unknowns

Before framing the problem, distinguish:

* Confirmed information.
* Stakeholder/user claims.
* Schema-derived facts.
* Hypotheses.
* Assumptions.
* Unknown information.
* TBD requirements.

Do not silently promote a stakeholder claim or assumption into a confirmed fact.

---

### Step 3 — Define the Business Problem

Describe:

* Observed or claimed current condition.
* Business concern.
* Known or suspected business impact.
* Relevant business scope.
* Boundaries.
* Assumptions.
* Constraints.

Do not state unsupported causal relationships.

---

### Step 4 — Define the Decision Context

Determine what business decision the analysis is intended to support.

Where information is available, identify:

* Decision ID.
* Decision owner.
* Decision to support.
* Decision deadline or relevant timing.
* Potential decision options.

Decision options must not be presented as predetermined recommendations.

If the decision is not yet known and this does not block the remaining specification, mark it `TBD`.

---

### Step 5 — Define Analysis Objectives

Each Analysis Objective must describe what the analysis needs to:

* Measure.
* Quantify.
* Compare.
* Segment.
* Diagnose.
* Validate.

Every Analysis Objective must support at least one business decision.

Avoid generic objectives such as:

* `Understand business performance`
* `Analyze the data`
* `Find useful insights`

---

### Step 6 — Define Business Questions

Each Business Question must be:

* Decision-relevant.
* Measurable.
* Analytically answerable.
* Traceable to an Analysis Objective.
* Compatible with the available or required data.

Where applicable, define:

* Business Question ID.
* Analysis Objective ID.
* Decision ID.
* Business Question.
* Analysis type.
* Unit of analysis.
* Eligible population.
* Baseline or comparator.
* Primary metrics.
* Dimensions.
* Filters.
* Exclusions.
* Analytical hypothesis.
* Alternative explanation.
* Expected analytical output.

### Comparative Questions

Questions involving terms such as:

* increase
* decrease
* higher
* lower
* better
* worse
* growth
* decline
* improvement

must specify a comparator or baseline.

Examples:

* Previous period.
* Same period last year.
* Business target.
* Historical baseline.
* Other product category.
* Control/reference group.

If the comparator is unknown, mark it `TBD`.

### Analytical Hypotheses

A hypothesis is not a fact.

When appropriate, include:

* Primary hypothesis.
* Alternative explanation.
* Condition that would contradict or weaken the primary hypothesis.

Avoid designing Business Questions solely to confirm an existing belief.

---

### Step 7 — Define Metrics

Every metric must have a stable identifier when part of a multi-document specification.

Where applicable, define:

* Metric ID.
* Metric name.
* Business definition.
* Metric role.
* Metric domain.
* Metric type.
* Mathematical logic.
* Eligible population.
* Inclusion rules.
* Exclusion rules.
* Null handling.
* Zero-denominator behavior.
* Unit of analysis.
* Source grain.
* Reporting grain.
* Time semantics.
* Supported dimensions.
* Implementation reference.

### Metric Types

Do not assume every metric follows a numerator/denominator formula.

Possible metric types include:

* Count.
* Sum.
* Ratio.
* Rate.
* Average.
* Median.
* Percentile.
* Index.
* Snapshot.
* Derived metric.

The mathematical formulation must match the metric type.

### Percentage Convention

Unless the user or target system explicitly requires another convention, represent ratio/rate values internally on a `0–1` scale.

Example:

`0.2537`

represents:

`25.37%`

Treat `%` as display formatting.

Do not combine an internal `×100` transformation with percentage formatting unless explicitly required by the target system.

### Zero Denominator

Do not write ambiguous rules such as:

`return 0 or NULL`

Define one behavior.

Unless business semantics explicitly require another treatment, an undefined ratio caused by a zero eligible denominator should be represented as `NULL` or equivalent blank semantics rather than `0%`.

---

### Step 8 — Define Data Requirements

Map analytical requirements to the data needed to implement them.

Where supported by provided information, specify:

* Data Requirement ID.
* Related Business Question ID.
* Related Metric ID.
* Entity or source table.
* Required field.
* Business meaning.
* Data type.
* Source grain.
* Primary/foreign key where known.
* Required relationships.
* Time field.
* Required data-quality rule.
* Known limitation.

Never invent fields or relationships that are absent from the supplied schema.

If a field is conceptually required but unavailable, document the requirement and mark availability accordingly.

---

### Step 9 — Assess Data Feasibility

Classify analytical feasibility as:

* **Answerable:** Required data is available and sufficient.
* **Partially Answerable:** Some parts can be answered, but limitations materially constrain the result.
* **Blocked:** Required information or data is unavailable.

For unavailable fields:

* Do not automatically create a proxy.
* A proxy may only be proposed when its business meaning reasonably represents the missing concept.
* Explicitly document the limitation introduced by the proxy.

If no valid proxy exists, state:

`No valid proxy identified.`

---

### Step 10 — Validate Traceability

Maintain the following analytical chain where applicable:

`PROB -> DEC -> OBJ -> BQ -> MET -> DR`

Interpretation:

* `PROB` — Business Problem
* `DEC` — Business Decision
* `OBJ` — Analysis Objective
* `BQ` — Business Question
* `MET` — Metric
* `DR` — Data Requirement

Validation rules:

* Every priority Business Question must support an Analysis Objective.
* Every Analysis Objective must support a business decision.
* Every primary Metric must support at least one Business Question.
* Supporting or guardrail Metrics must have an explicit purpose.
* Every Data Requirement must support a Business Question, Metric, or analytical constraint.

Avoid orphan requirements.

### Upstream Alignment Check

When reviewing or extending an existing document, validate it against its direct upstream artifact.

Examples:

- Business Problem must align with Business Context.
- Business Question must align with Business Problem, Decision, and Analysis Objective.
- Analytical Requirement must align with Business Question.
- Metric must align with Analytical Requirement.
- Data Requirement must align with Metric or Analytical Requirement.

A document may be structurally complete but still be considered logically incorrect if it does not align with its upstream artifact.

---

## 6. Reference Routing

Read only the reference files required for the requested task.

### Business Context & Problem

Use:

`references/data-analyst/01-business-context-problem.md`

For:

* Business context.
* Problem framing.
* Decision context.
* Analysis objectives.
* Scope and boundaries.
* Assumptions and constraints.

---

### Business Questions & Analytical Requirements

Use:

`references/data-analyst/02-business-question-requirement.md`

For:

* Objective-to-question mapping.
* Business Question specification.
* Analysis type.
* Unit of analysis.
* Population.
* Baseline/comparator.
* Dimensions.
* Filters and exclusions.
* Expected analytical outputs.
* Data feasibility.

---

### Metric Dictionary

Use:

`references/data-analyst/03-metric-dictionary.md`

For:

* Metric master index.
* Business definitions.
* Metric type and classification.
* Mathematical formulation.
* Population and filtering rules.
* Grain.
* Time semantics.
* Null/edge-case handling.
* Implementation reference logic.

---

### Data Requirements & Quality

Use:

`references/data-analyst/04-data-requirements-quality.md`

For:

* Required entities and fields.
* Source grain.
* Keys and relationships.
* Data availability.
* Data-quality requirements.
* Known data gaps.
* Feasibility constraints.

---

## 7. Output Standards

* Follow the language requested by the user.
* Produce Markdown documentation unless another format is explicitly requested.
* Use concise, implementation-oriented language.
* Avoid unnecessary conversational introductions inside formal documentation.
* Avoid vague terms such as `high`, `low`, `good`, `bad`, `significant`, `fast`, or `large` without a comparator, definition, or threshold.
* Do not invent thresholds merely to remove qualitative wording.
* Use `TBD` when an implementation requirement needs a threshold that has not been defined.
* Preserve mandatory core sections of the relevant reference template.

### Semantic Template Matching

Reference templates define required semantic content, not mandatory word-for-word headings or formatting, unless the user explicitly requests strict template conformance.

When reviewing user-created documentation:

- identify whether the required meaning is present even if headings differ;
- do not mark content incorrect solely because section names or order differ;
- distinguish between missing required content and missing optional template sections;
- evaluate logical alignment before formatting conformity.

* Do not remove or rename core sections unless the user explicitly requests a template redesign.
* Additional sections may be introduced only when necessary for correctness, traceability, or implementation and when the information cannot logically fit an existing section.
* Respect exact item counts requested by the user.
* Explicitly document material assumptions, limitations, and feasibility constraints.
* Do not hide important analytical limitations outside the formal specification.


---

## 8. Definition of Done

Before returning any final documentation, verify all applicable checks.

### Evidence Quality

* [ ] No unsupported business facts were invented.
* [ ] Claims and confirmed facts are distinguishable where material.
* [ ] Hypotheses are not presented as facts.
* [ ] Assumptions are explicit.
* [ ] Unknown or undefined values are marked `Unknown` or `TBD`.
* [ ] No unsupported causal relationships are stated as facts.
* [ ] No unsupported thresholds, fields, data types, percentages, or business rules were fabricated.

### Analytical Correctness

* [ ] The Business Problem is specific enough to guide analysis.
* [ ] The intended business decision is identified or explicitly marked `TBD`.
* [ ] Analysis Objectives support the business decision.
* [ ] Every Business Question is measurable and decision-relevant.
* [ ] Comparative Business Questions define a baseline/comparator or explicitly mark it `TBD`.
* [ ] Unit of analysis is defined where material.
* [ ] Eligible population is defined where material.
* [ ] Metric formulas match their metric types.
* [ ] Percentage/rate representation is mathematically consistent.
* [ ] Zero-denominator behavior is unambiguous.
* [ ] Time semantics are defined for time-dependent metrics.

### Data Feasibility

* [ ] Required entities and fields come from supplied evidence or are marked `TBD`.
* [ ] Source grain and analytical/reporting grain are not silently conflated.
* [ ] Missing data is explicitly documented.
* [ ] Semantically invalid proxy fields are not proposed.
* [ ] Feasibility is classified where data limitations materially affect a Business Question.

### Traceability

* [ ] Priority Business Questions trace to an Analysis Objective.
* [ ] Analysis Objectives trace to a business decision.
* [ ] Primary Metrics trace to Business Questions.
* [ ] Supporting Metrics have an explicit purpose.
* [ ] Data Requirements trace to Business Questions, Metrics, or analytical constraints.
* [ ] Cross-document identifiers remain consistent.

### Output Quality

* [ ] Requested item counts are respected.
* [ ] Required template sections are preserved.
* [ ] No unnecessary implementation details were introduced.
* [ ] Material assumptions and limitations remain visible.
* [ ] The resulting documentation is directly usable by a Data Analyst or Analytics Engineer.
