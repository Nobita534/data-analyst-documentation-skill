---
name: data-analyst-documentation-skill
description: >-
  Use this skill when the user wants to transform a business problem, stakeholder request, dataset schema, or existing analytics documentation into structured Data Analyst documentation, including business context, business problems, business questions, analytical requirements, metric definitions, data requirements, and data-quality specifications. Do not use this skill for direct data analysis, KPI calculation, SQL execution, dashboard building, backend/API specifications, or software-development requirements.
---

# Data Analyst Documentation Skill

## 1. Purpose & Scope

This skill creates structured, implementation-ready analytical documentation for Data Analysts and Analytics Engineers.

Canonical traceability:

`Business Context -> PROB -> DEC -> OBJ -> BQ -> AR -> MET -> DR`

Where:

- `PROB` — Business Problem
- `DEC` — Business Decision
- `OBJ` — Analysis Objective
- `BQ` — Business Question
- `AR` — Analytical Requirement
- `MET` — Metric
- `DR` — Data Requirement

This is a documentation and specification workflow, not a data-analysis workflow.

### In Scope

Use this skill to:

- Establish business/domain context for analytical work.
- Frame and refine Business Problems.
- Identify the business decision the analysis should support.
- Define Analysis Objectives and Business Questions.
- Define Analytical Requirements: population, period, baseline, dimensions, filters, exclusions, analytical approach, and expected output.
- Define metrics and business logic.
- Define required entities, fields, grain, relationships, time semantics, and data-quality expectations.
- Assess analytical feasibility and data readiness.
- Review, refine, extend, or practice analytical documentation.
- Maintain cross-document traceability.

### Out of Scope

Do not:

- Execute queries or analytical code.
- Calculate actual KPI values.
- Perform EDA, statistical analysis, or root-cause analysis.
- Present findings or recommendations as if analysis has already been executed.
- Build dashboards.
- Design backend APIs or BRD/FRD software requirements.
- Invent unsupported facts, fields, keys, relationships, data types, business rules, thresholds, SLA values, causal relationships, or proxies.

---

## 2. Input Handling

### Minimum Input

At least one of the following must be available:

- A business problem or stakeholder request.
- A dataset/schema/source from which an analytical context can be established.
- Existing analytical documentation to review or extend.

### Recommended Supporting Inputs

When available, use:

- Business/domain context.
- Stakeholder and decision context.
- Dataset page, schema, data dictionary, repository documentation, or uploaded structured data.
- Existing Business Questions, Analytical Requirements, metrics, or data requirements.
- Analysis period, business rules, exclusions, targets, and baselines.

### Missing Information

Classify missing information as:

- **Blocking** — proceeding would make the specification logically invalid or materially misleading.
- **Non-blocking** — proceed while explicitly marking the missing item.

For non-blocking gaps use `TBD`, `Unknown`, or `Assumption`. Ask only the minimum clarification required for blocking gaps.

---

## 3. Evidence & Assumption Policy

Keep evidence, claims, assumptions, and hypotheses distinct.

Use statuses when relevant:

| Status | Meaning |
|---|---|
| Confirmed | Explicitly validated by an authoritative source |
| User-provided | Stated by the user/stakeholder but not independently validated |
| Schema-derived | Directly supported by supplied schema/metadata |
| Source-provided | Directly stated by the supplied source |
| Context-derived | Reasonably synthesized from supported context |
| Hypothesis | Proposition for future analysis to test |
| Assumption | Temporary working condition |
| TBD | Required information not yet defined |
| Unknown | Information unavailable and unsafe to infer |

Never fabricate business performance, percentages, financial impact, fields, keys, relationships, data types, targets, thresholds, SLA values, business rules, causal claims, or proxies.

Association is not causation. Prefer wording such as `is associated with`, `coincides with`, `the stakeholder suspects`, or `hypothesis to be tested` unless causal evidence or an appropriate causal design is available.

Do not predetermine a business solution. Define the **decision to be supported**, not the action that must be taken.

---

## 4. Operating Modes

### Mode A — Scaffold

Create requested analytical documentation from a new problem, source, dataset, or schema using the workflow in Section 5.

### Mode B — Review / Refine

Review existing analytical documentation for logical inconsistencies, unsupported claims, upstream misalignment, weak questions or requirements, metric defects, data gaps, feasibility risks, and broken traceability. Preserve correct content and avoid unnecessary rewrites.

### Mode C — Extend

Add only requested scope while preserving existing IDs, naming conventions, and traceability.

### Mode D — Practice / Review

When the user submits their own document:

1. Identify the document type.
2. Identify its direct upstream artifact.
3. Detect the actual semantic content even when headings differ.
4. Compare it with the corresponding reference requirements.
5. Validate upstream alignment.
6. Identify logical, analytical, or scope issues.
7. Classify findings as `Correct`, `Needs revision`, `Missing required content`, or `Optional enhancement`.
8. Suggest optional additions only after core correctness is assessed.
9. Do not rewrite unless explicitly requested.

### Delivery Mode

- **Complete** — return the complete requested document set when practical.
- **Staged** — one document/stage at a time when requested or necessary.
- **Append** — return only added/changed content.

Do not force one-file-per-turn when the user requests a complete deliverable.

---

## 5. Execution Workflow

Follow these steps in sequence.

### Step 1 — Parse the Request

Identify the requested deliverable, business/analytical request, stakeholder, constraints, available sources/schema, existing documentation, and exact requested item counts.

If the user requests exactly `N` items, produce exactly `N`.

---

### Step 2 — Resolve Business Context

Business Context is the upstream foundation for Business Problem framing. It describes the business/domain environment; it is not itself a Business Problem, Business Question, Analytical Requirement, Metric, Data Requirement, finding, or recommendation.

First inspect the available source material and choose one context mode.

#### Mode 1 — Source-Grounded Context

Use when supplied sources provide enough business/domain context.

Possible sources include:

- Official dataset or company documentation.
- Dataset metadata or schema.
- Repository documentation.
- User-provided files or stakeholder context.
- Authoritative source material supplied in the task.

Rules:

- Preserve the source's meaning.
- Distinguish source statements from schema-derived observations.
- Do not add unsupported internal business conditions.
- Raw structured data may be inspected for file/sheet/table names, columns, types, entities, and metadata, but do not perform value-level analysis unless explicitly requested outside this skill.

#### Mode 2 — Constructed Analytical Context

Use when the available source is analytically useful but does not provide enough real business context for downstream documentation.

Construct a plausible analytical context using only:

`Dataset Evidence + Domain Context + Relevant Current Business Need`

Process:

1. Identify the domain represented by the source.
2. Identify supported business entities and processes.
3. Gather relevant external/domain context when external research is appropriate and permitted.
4. Check that the external context is compatible with the dataset scope.
5. Construct a realistic analytical context without claiming it is the actual internal context of a real company.
6. Label constructed elements clearly as `Context-derived`, `Assumption`, or equivalent.

Do not invent claims such as revenue decline, churn increase, margin compression, return-rate deterioration, operational failures, or strategic priorities unless supported by a source.

If external research is unavailable, proceed with dataset/domain evidence only and explicitly state the limitation.

Expected Business Context sections when producing a full context document:

1. Project Metadata
2. Business / Domain Overview
3. Operating Context
4. Key Stakeholders
5. Key Business Entities
6. Current Business & Data Context
7. Analytical Relevance
8. Known Context Limitations
9. Source & Evidence Summary

---

### Step 3 — Separate Facts, Claims, and Unknowns

Classify material information as Confirmed, User-provided, Schema-derived, Source-provided, Context-derived, Hypothesis, Assumption, TBD, or Unknown.

Do not silently promote claims or assumptions into facts.

---

### Step 4 — Define the Business Problem

Start from Business Context, not from dataset columns.

A Business Problem should describe an observed/claimed condition, unresolved analytical uncertainty, and relevant business consequence without asserting unsupported root cause.

Use stable IDs such as `PROB-01`.

Supporting data/platform issues may use `DP-xx` only when explicitly supported. They are secondary analytical-readiness issues, not the primary traceability chain.

---

### Step 5 — Define Decision Context

Use `DEC-xx`. Identify the decision, owner, timing, options, and required evidence when supported. If the decision need is unknown but non-blocking, use `TBD`; do not invent a decision to complete a template.

---

### Step 6 — Define Analysis Objectives

Use `OBJ-xx`. Objectives should use verbs such as quantify, compare, identify, evaluate, segment, assess, determine, or validate and must support a decision.

Avoid generic goals such as `analyze the data` or `find insights`.

---

### Step 7 — Define Business Questions

Business Questions define **WHAT** the business needs answered and **WHY** the answer matters.

Use `BQ-xx`. Each BQ should include, where applicable:

- Related Problem
- Business Question
- Purpose
- Decision Supported
- Priority

Do not place Unit of Analysis, Population, Baseline, Metrics, Dimensions, Filters, Methods, Expected Output, or physical fields in the BQ specification; these belong downstream.

---

### Step 8 — Define Analytical Requirements

Analytical Requirements define **HOW** the analysis must be structured.

Use `AR-xx`. Each AR should trace to a BQ and define where applicable:

- Analytical Objective
- Unit of Analysis
- Eligible Population
- Analysis Period
- Baseline / Comparator
- Required Metrics
- Dimensions
- Inclusion / Exclusion Rules
- Analytical Approach
- Hypothesis / Alternative Explanation
- Expected Analytical Output
- Feasibility
- Assumptions & Limitations

Do not perform the analysis itself.

---

### Step 9 — Define Metrics

Use `MET-xx`. Each metric must trace to an AR and define business meaning, role, type, mathematical logic, eligible population, grains, time semantics, null/zero-denominator behavior, dimensions, and dependencies as applicable.

A Core KPI, Supporting Metric, Guardrail Metric, or Diagnostic Metric must have an explicit analytical purpose. Supporting or guardrail metrics may support multiple ARs, but they must not be orphaned.

Do not assume all metrics are ratios. Internal ratios/rates should normally use a `0–1` representation with `%` as display formatting.

---

### Step 10 — Define Data Requirements

Use `DR-xx` and map data requirements from **Analytical Requirements and Metrics**, not directly from Business Questions or source columns.

Required downstream mapping:

`AR -> MET -> DR`

A Data Requirement must support at least one:

- `AR-xx`
- `MET-xx`
- Explicit analytical constraint that is documented in the AR or metric definition

Where applicable, define:

- Related AR ID
- Related Metric ID
- Business entity
- Conceptual data requirement
- Physical field/source only when confirmed
- Analytical role
- Source grain
- Identifier/key semantics when known
- Required relationship and cardinality when supported
- Required time field
- Availability
- Data-quality requirement
- Known limitation and analytical impact

Rules:

- Do not derive DRs merely because columns exist in the source.
- Do not map `BQ -> DR` as the primary relationship; BQ-level needs must first be translated into ARs.
- Do not invent physical fields, keys, relationships, cardinality, data types, or proxies.
- When a conceptual requirement is known but physical implementation is not, keep the conceptual requirement and set the physical field/source to `TBD`.
- If one DR supports multiple ARs or metrics, record all relevant IDs rather than duplicating the requirement without need.

---

### Step 11 — Assess Data Feasibility

Use evidence-based readiness statuses such as `Answerable / Partially Answerable / Blocked / TBD` for AR feasibility and `Ready / Partially Ready / Blocked / TBD` for downstream data readiness where appropriate.

Do not automatically create proxies. If no semantically valid proxy exists, state `No valid proxy identified.`

---

### Step 12 — Validate Traceability

Validate the complete chain:

`Business Context -> PROB -> DEC -> OBJ -> BQ -> AR -> MET -> DR`

Minimum traceability checks:

- Every Business Problem aligns with Business Context.
- Every priority BQ traces to a valid PROB and supports a DEC/OBJ.
- Every BQ that requires implementation has at least one AR, unless explicitly documented as deferred or out of scope.
- Every AR traces to at least one BQ.
- Every primary MET traces to at least one AR.
- Supporting/guardrail METs have an explicit analytical purpose and upstream linkage.
- Every DR traces to an AR, a MET, or an explicit analytical constraint documented downstream of the BQ.
- No primary DR is mapped only to a BQ while bypassing AR/MET.
- Cross-document IDs remain stable and consistent.
- No orphan PROB, DEC, OBJ, BQ, AR, MET, or DR remains in the requested scope.

A structurally complete document can still be logically incorrect if it is misaligned with its upstream artifact.

---

## 6. Reference Routing

Read only the reference files needed for the requested task.

- Business Context: `references/01-business-context.md`
- Business Problem: `references/02-business-problem.md`
- Business Question: `references/03-business-question.md`
- Analytical Requirement: `references/04-analytical-requirement.md`
- Metric Dictionary: `references/05-metric-dictionary.md`
- Data Requirements & Quality: `references/06-data-requirements-quality.md`

When creating a complete specification, follow the reference order above.

---

## 7. Output Standards

- Follow the language requested by the user.
- Use Markdown unless another format is explicitly requested.
- Use concise, implementation-oriented language while retaining enough detail for another analyst to execute the specification without guessing core business logic.
- Preserve required semantic content of the relevant reference template; exact headings need not match unless strict conformance is requested.
- Avoid vague qualifiers such as `high`, `low`, `good`, `bad`, `significant`, `fast`, or `large` unless a comparator, definition, or supported threshold exists.
- Do not invent thresholds merely to eliminate qualitative wording.
- Respect exact requested item counts.
- Keep material assumptions, limitations, and feasibility constraints visible.

### Complete Document Structure

When generating a complete standalone document, begin with an **Outline** that lists the major sections that will follow.

The Outline must reflect the actual document structure. Do not include sections that are not present in the final document.

After the Outline, provide the full specification using the mandatory semantic sections defined by the relevant reference file.

When useful for navigation, use numbered Markdown headings consistently throughout the document.

### Summary Requirement

For a complete standalone analytical document, include a concise **Summary** near the end unless:

- the reference already contains an equivalent summary/master section that adequately serves this purpose;
- the user explicitly asks for no summary; or
- the requested output is intentionally narrow, such as a single table, patch, critique, or append-only change.

The Summary should synthesize the specification itself, not introduce new findings or recommendations.

Depending on the document type, it may summarize:

- scope and analytical purpose;
- key IDs and traceability;
- major assumptions or unresolved TBD items;
- feasibility or readiness constraints;
- handoff to the next downstream document.

### Complete vs Staged vs Append Output

- **Complete:** return a self-contained document with Outline, required body sections, and Summary where applicable.
- **Staged:** return the complete requested stage/document, not fragments of individual template fields unless the user explicitly asks for them.
- **Append:** return only the changed or newly added content and clearly identify where it belongs in the existing document.

Do not duplicate the same information solely to satisfy Outline or Summary requirements.

### Markdown Quality

- Use headings, tables, bullets, and code formatting only when they improve specification readability.
- Keep tables compact and implementation-oriented.
- Do not place long explanatory prose inside table cells when a dedicated section would be clearer.
- Keep identifiers such as `PROB-01`, `BQ-01`, `AR-01`, `MET-01`, and `DR-01` visually stable and consistent.
- Do not mix multiple heading conventions within the same standalone document.

### Semantic Template Matching

Reference templates define required **semantic content**, not mandatory word-for-word headings or formatting, unless strict template conformance is explicitly requested.

When producing or reviewing documentation:

- ensure every required semantic element is present;
- allow equivalent headings when their meaning is unambiguous;
- distinguish missing required content from optional enhancement;
- prioritize logical correctness and upstream alignment over cosmetic conformity.

---

## 8. Definition of Done

Before returning final documentation verify:

### Evidence Quality

- [ ] No unsupported business facts, values, thresholds, fields, data types, relationships, rules, causal claims, or proxies were invented.
- [ ] Facts, claims, assumptions, hypotheses, and unknowns are distinguishable where material.
- [ ] Constructed Business Context is clearly labeled and not presented as actual internal company context.

### Context & Analytical Correctness

- [ ] Business Context is established using the appropriate Source-Grounded or Constructed mode.
- [ ] Business Problem follows from Business Context rather than being reverse-engineered from columns.
- [ ] Decision is defined or explicitly `TBD`.
- [ ] Objectives support the decision.
- [ ] BQs are business-oriented and decision-relevant.
- [ ] BQs contain WHAT/WHY rather than AR-level implementation detail.
- [ ] ARs define analytical structure and trace to BQs.
- [ ] Required comparisons have a comparator or `TBD`.
- [ ] Unit of Analysis, Population, analysis period, and analytical approach are explicit where material.
- [ ] Metrics trace to ARs and have mathematically coherent definitions.
- [ ] Time semantics and edge cases are explicit for time-dependent or ratio/rate metrics.

### Data Feasibility

- [ ] DRs are derived from ARs/Metrics or explicit analytical constraints, not directly from source columns.
- [ ] No primary `BQ -> DR` mapping bypasses the AR/MET layer.
- [ ] Conceptual and physical fields are not conflated.
- [ ] Source grain and analytical/reporting grain are not silently conflated.
- [ ] Keys, relationships, cardinality, and data types are evidence-based or `TBD`.
- [ ] Missing data and analytical impact are visible.
- [ ] Semantically invalid proxies are not proposed.
- [ ] Feasibility/readiness is classified where material.

### Traceability

- [ ] `Business Context -> PROB -> DEC -> OBJ -> BQ -> AR -> MET -> DR` is maintained where applicable.
- [ ] Priority BQs trace to PROB/DEC/OBJ.
- [ ] Implementable BQs trace to at least one AR unless explicitly deferred/out of scope.
- [ ] Every AR traces to a BQ.
- [ ] Primary Metrics trace to ARs.
- [ ] Supporting/guardrail Metrics have an explicit upstream purpose.
- [ ] Every DR traces to an AR, Metric, or explicit analytical constraint.
- [ ] Cross-document identifiers remain stable and consistent.
- [ ] No orphan requirements remain in the requested scope.

### Output Quality

- [ ] Requested scope and item counts are respected.
- [ ] Complete standalone documents begin with an Outline that matches the actual document structure.
- [ ] Required semantic sections are preserved even when headings differ from the reference wording.
- [ ] Complete standalone documents include a Summary when applicable and do not introduce new analytical findings in that Summary.
- [ ] Staged outputs deliver a complete requested stage rather than accidental fragments.
- [ ] Append outputs clearly identify the insertion/update location.
- [ ] Markdown heading style and identifiers remain consistent within the document.
- [ ] No unnecessary implementation details were introduced.
- [ ] Material assumptions, limitations, and unresolved `TBD` items remain visible.
- [ ] The resulting documentation is directly usable by a Data Analyst or Analytics Engineer.
