# Business Question Specification

## 1. Purpose

This document converts the primary analytical Business Problems defined in `02-business-problem.md` into a focused set of Business Questions.

Business Questions define **what the business needs the analysis to answer**.

They provide the bridge between:

`Business Problem -> Business Question -> Analytical Requirement`

This document must remain business-oriented.

It must not define:

* detailed metric formulas;
* dimensions or filters;
* analytical grain;
* SQL logic;
* expected output schemas;
* data requirements;
* dashboard visualizations;
* analytical findings;
* recommendations.

Those belong to downstream documentation.

---

# 2. Required Input

The primary input is:

`02-business-problem.md`

Use primarily the following sections:

* Core Analytical Problems (`PROB-xx`);
* Decision Context (`DEC-xx`);
* Analysis Objectives (`OBJ-xx`);
* Scope & Boundaries;
* Assumptions & Constraints.

Supporting Data Problems (`DP-xx`) must **not automatically become Business Questions**.

Data Warehouse, ETL/ELT, integration, or infrastructure concerns are supporting analytical-readiness issues rather than primary Business Questions.

Example:

Incorrect:

> How should the ETL pipeline be designed?

Correct:

> Which business areas require integrated historical data to support consistent analytical reporting?

Even this type of question should only be included if it directly supports a documented analytical Business Problem.

---

# 3. Business Question Derivation Rules

## 3.1 Start From Primary Business Problems

Every Business Question must trace to at least one primary Business Problem:

`PROB-xx`

Do not generate Business Questions solely from:

* dataset columns;
* available tables;
* interesting analytical techniques;
* dashboard ideas;
* technologies used in the project.

Incorrect reasoning:

`Dataset has geography -> create a geography question`

Correct reasoning:

`PROB-01 requires identifying where performance differs -> geography may become a relevant Business Question`

---

## 3.2 Business Questions Must Reduce Decision Uncertainty

A Business Question should help reduce uncertainty around a documented business decision.

Preferred structure:

`What / Which / How much / How does ...`

Examples:

* Which customer segments generate the highest business value?
* How does repeat-purchase behavior differ across customer segments?
* Which product categories contribute most to revenue across geographic areas?
* How has fulfillment performance changed over time?

Avoid questions that do not support a decision.

Weak:

> What does the dataset show?

Weak:

> What interesting insights can be found?

Strong:

> Which customer segments should be prioritized for retention-focused analysis based on purchasing behavior and business value?

---

## 3.3 Do Not Predetermine the Answer

A Business Question must remain neutral.

Incorrect:

> Why are delivery delays causing customer churn?

This assumes causality.

Better:

> How does repeat-purchase behavior differ across customers with different delivery experiences?

Incorrect:

> Which poorly performing sellers should be removed?

This assumes removal is the correct solution.

Better:

> Which sellers show consistently weaker fulfillment performance and therefore require further evaluation?

---

## 3.4 Distinguish Business Questions From Analysis Tasks

A Business Question describes **what needs to be known**.

It should not describe the technical method.

Incorrect:

> Use RFM analysis to segment customers.

This is an Analytical Requirement.

Better:

> Which customer groups differ materially in purchasing frequency, recency, and business value?

The later `04-analytical-requirement.md` may specify RFM as the analytical approach.

---

## 3.5 Distinguish Business Questions From Metrics

Incorrect:

> What is the retention rate?

This may be too narrow to serve as a meaningful Business Question.

Better:

> How does customer retention vary across acquisition cohorts and customer segments?

`Retention Rate` may later become a Metric used to answer this question.

---

# 4. Business Question Quality Criteria

Every Business Question should satisfy the following criteria.

## 4.1 Relevant

The question must relate directly to a documented Business Problem.

---

## 4.2 Decision-Oriented

The answer should help support a business decision, prioritization, or further investigation.

---

## 4.3 Measurable

The question must be answerable using measurable analytical evidence.

Avoid vague wording such as:

* good;
* bad;
* successful;
* effective;
* strong;
* weak;

unless downstream Analytical Requirements can define the comparison or measurement.

---

## 4.4 Neutral

The question must not assume:

* a root cause;
* a relationship;
* an expected result;
* a preferred business solution.

---

## 4.5 Data-Relevant

The question should be reasonably compatible with the known or required data.

Do not reject a useful Business Question merely because one field is currently missing.

Data feasibility is evaluated more deeply in downstream files.

However, do not create questions that clearly require an entirely unrelated data domain.

---

## 4.6 Non-Duplicate

Each Business Question should represent a materially distinct analytical need.

Avoid questions such as:

* Which products generate the most revenue?
* Which products contribute the highest sales?
* Which product categories have the largest revenue?

unless they genuinely support different decisions.

Merge overlapping questions where possible.

---

# 5. Business Question Scope

Business Questions may commonly address areas such as:

* performance;
* customer behavior;
* customer segmentation;
* retention;
* product performance;
* profitability;
* geographic performance;
* seller/vendor performance;
* fulfillment;
* operational efficiency;
* conversion;
* risk or prioritization.

Do not attempt to cover every category in one project.

Select only questions that are justified by the Business Problems.

For a personal Data Analyst project, a smaller set of strong, connected Business Questions is preferable to a large collection of unrelated questions.

---

# 6. Question Count

If the user specifies an exact number of Business Questions:

`Generate exactly N Business Questions.`

Do not generate additional questions.

If the user does not specify a number, generate the smallest set necessary to cover the primary Business Problems without unnecessary overlap.

As a general guideline for a personal portfolio project:

`3-6 strong Business Questions`

is usually sufficient.

This is a guideline, not a mandatory quota.

---

# 7. Required Business Question Table

The final output must include the following table.

| BQ ID | Related Problem | Business Question | Purpose | Decision Supported | Priority |
| ----- | --------------- | ----------------- | ------- | ------------------ | -------- |

## Column Definitions

### BQ ID

Use stable identifiers:

`BQ-01`, `BQ-02`, ...

These identifiers must remain unchanged in downstream documents.

---

### Related Problem

Reference the primary Business Problem:

`PROB-xx`

A Business Question may map to more than one Business Problem only when genuinely necessary.

Prefer one primary problem where possible.

---

### Business Question

State the business-facing analytical question.

The question should be:

* concise;
* neutral;
* measurable;
* decision-relevant.

---

### Purpose

Explain **why this question needs to be answered**.

The Purpose should describe the analytical/business value of answering the question.

It should not merely rephrase the question.

Weak:

> Purpose: To understand customer segments.

Better:

> Purpose: Identify which customer groups contribute the most value and exhibit different purchasing behaviors so that downstream analysis can support customer prioritization.

---

### Decision Supported

Reference the relevant decision:

`DEC-xx`

Optionally include a short description when necessary.

This ensures that Business Questions exist to support actual business decisions rather than generic exploration.

If the decision has not yet been defined:

`TBD`

---

### Priority

Use:

* `P0 — Critical`
* `P1 — Important`
* `P2 — Supporting`

Priority should consider:

* importance of the related Business Problem;
* importance of the related business decision;
* analytical value;
* overlap with other questions.

Do not assign every Business Question as `P0`.

---

# 8. Traceability Rules

The minimum traceability chain is:

`PROB -> BQ`

The preferred chain is:

`PROB -> DEC -> OBJ -> BQ`

Before finalizing, verify:

* every BQ traces to a primary Business Problem;
* every BQ supports a decision or Analysis Objective;
* every P0 Business Problem has at least one BQ;
* no BQ exists solely because a dataset field or analytical technique is available;
* no BQ is duplicated under slightly different wording.

---

# 9. Required Output Structure

# Business Questions

## 1. Business Question Overview

Briefly state which primary Business Problems these questions are intended to address.

Do not repeat the full Business Problem specification.

---

## 2. Business Question Table

| BQ ID | Related Problem | Business Question | Purpose | Decision Supported | Priority     |
| ----- | --------------- | ----------------- | ------- | ------------------ | ------------ |
| BQ-01 | PROB-XX         | [...]             | [...]   | DEC-XX             | P0 / P1 / P2 |

---

## 3. Traceability Summary

| Business Problem | Analysis Objective | Business Questions |
| ---------------- | ------------------ | ------------------ |
| PROB-XX          | OBJ-XX             | BQ-XX, BQ-XX       |

This section provides the handoff to:

`04-analytical-requirement.md`

---

# 10. Definition of Done

Before returning the document, verify:

* [ ] Every Business Question originates from a primary analytical Business Problem.
* [ ] Supporting Data Problems were not incorrectly converted into technical Business Questions.
* [ ] Every Business Question contains a clear Purpose.
* [ ] The Purpose explains business/analytical value rather than repeating the question.
* [ ] Every question is neutral and does not assume a root cause.
* [ ] Every question avoids preselecting a business solution.
* [ ] Every question can reasonably be answered through measurable analysis.
* [ ] Questions are not generated merely from available columns or technologies.
* [ ] Duplicate or highly overlapping questions have been consolidated.
* [ ] Priority levels are not assigned arbitrarily.
* [ ] Business Question IDs remain stable for downstream traceability.
* [ ] The requested Business Question count is respected exactly.
