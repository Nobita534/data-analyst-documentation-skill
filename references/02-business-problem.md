# Business Problem Specification

## 1. Purpose

This document identifies and structures the business problems that justify analytical work.

The primary purpose is to translate the Business Context into clearly defined **analytical problems** that can later be decomposed into:

`Business Problem -> Decision -> Analysis Objective -> Business Question`

The document may also identify supporting problems related to:

* data availability;
* data integration;
* Data Warehouse readiness;
* ETL/ELT processes;
* data consistency;
* reporting data architecture;

but only when these problems are explicitly supported by the user's request, supplied context, or available source evidence.

Data platform problems must remain secondary to the analytical objective of this skill.

This document must not:

* answer the Business Questions;
* calculate metrics;
* perform EDA;
* determine root causes from data;
* produce findings;
* prescribe final business solutions;
* design a complete Data Warehouse;
* design detailed ETL/ELT pipelines.

---

# 2. Required Input

The primary input is:

`01-business-context.md`

The Business Context should provide enough information to understand:

* business/domain environment;
* relevant business processes;
* stakeholders;
* key business entities;
* available data;
* current business and data context;
* known limitations;
* source/evidence status.

Additional information from the user's prompt may also be used.

Examples:

* a specific analytical concern;
* a suspected business issue;
* a reporting limitation;
* a Data Warehouse requirement;
* ETL/ELT concerns;
* fragmented data sources;
* data refresh issues.

When user-provided information conflicts with the Business Context, surface the conflict instead of silently resolving it.

---

# 3. Problem Discovery Principles

## 3.1 Start From Context, Not From Available Columns

Do not create Business Problems merely because certain fields exist in the dataset.

Incorrect reasoning:

`Dataset has customer_id -> create a customer segmentation problem`

Correct reasoning:

`Business Context identifies customer-value decisions -> customer data can support investigation -> formulate an analytical problem`

Available data constrains what can be analyzed.

It does not independently determine what the business problem is.

---

## 3.2 Analytical Problems Are Primary

Prioritize problems involving uncertainty that can reasonably be reduced through data analysis.

Typical analytical problem categories include:

* unclear performance drivers;
* declining or changing business performance;
* customer behavior uncertainty;
* customer retention or repeat-purchase uncertainty;
* profitability uncertainty;
* product performance differences;
* geographic performance differences;
* seller/vendor performance;
* operational or fulfillment performance;
* conversion behavior;
* customer experience;
* risk concentration;
* resource prioritization.

Do not automatically create one problem for every available business entity.

---

## 3.3 Distinguish Context From Problem

A business condition is not automatically a Business Problem.

Example:

Context:

> The company operates an e-commerce marketplace with customers, sellers, products, orders, and delivery operations.

This is not a Business Problem.

A Business Problem requires an unresolved business concern such as:

> Management lacks sufficient evidence to determine which customer, product, or geographic factors are driving differences in commercial performance.

---

## 3.4 Distinguish Problem From Root Cause

Do not claim the cause of a problem before analysis has been performed.

Incorrect:

> Low retention is caused by delivery delays.

Better:

> Repeat-purchase behavior is limited or uncertain, while the potential relationship between fulfillment experience and subsequent purchasing has not yet been established.

The cause belongs to a hypothesis or future analysis.

---

# 4. Problem Sources

A Business Problem may originate from one of three evidence situations.

## 4.1 Explicit Problem

Use when the user, stakeholder, or authoritative source explicitly states the problem.

Example:

> The business suspects that bike profitability is declining while return rates are increasing.

Preserve the original concern while separating verified facts from stakeholder claims.

Evidence status:

`User-provided` or `Source-provided`

---

## 4.2 Context-Derived Analytical Problem

Use when no explicit problem exists but the Business Context reveals a legitimate analytical uncertainty.

The problem may be constructed from:

`Business Context + Business Process + Available Data + Decision Need`

The resulting problem must:

* be plausible within the documented context;
* be supportable by available or reasonably required data;
* not claim nonexistent internal business facts;
* be explicitly identified as a constructed analytical problem.

Evidence status:

`Context-derived`

---

## 4.3 Supporting Data Problem

Use only when the user's prompt or Business Context explicitly raises a problem involving data infrastructure or analytical data availability.

Examples:

* multiple operational sources are not integrated;
* reporting depends on manual data consolidation;
* no analytical warehouse currently exists;
* ETL/ELT processes are inconsistent;
* reporting tables have incompatible grains;
* historical data is difficult to query;
* transformations are duplicated across reports.

These problems should be documented only at the level required to explain their impact on analytical work.

Do not turn this document into a Data Engineering design specification.

---

# 5. Core Analytical Problem Definition

For each Business Problem, define the following.

## 5.1 Problem ID

Use:

`PROB-01`, `PROB-02`, ...

Identifiers must remain stable across downstream documents.

---

## 5.2 Problem Statement

Use a neutral structure:

`Observed or claimed condition + unresolved analytical uncertainty + business consequence`

Example structure:

> The business observes or suspects [condition], but lacks sufficient evidence to determine [analytical uncertainty], limiting its ability to [business decision or action].

Avoid causal language unless causality has already been established.

---

## 5.3 Problem Type

Classify the problem where useful.

Recommended analytical categories:

* Performance Monitoring.
* Comparative Analysis.
* Diagnostic Analysis.
* Segmentation.
* Customer Behavior.
* Profitability.
* Operational Performance.
* Product Performance.
* Geographic Performance.
* Risk / Prioritization.
* Data Availability / Analytical Readiness.

Use the category to describe the nature of the problem, not to predetermine the analytical technique.

---

## 5.4 Evidence Status

Classify the problem as:

* `Confirmed`
* `Source-provided`
* `User-provided`
* `Context-derived`
* `Hypothesis`
* `Unknown`

Do not mark a constructed problem as confirmed.

---

# 6. Current Condition & Analytical Uncertainty

For each problem, distinguish:

### Current / Claimed Condition

What is currently known, observed, or claimed?

### Analytical Uncertainty

What does the business still not know?

The analytical uncertainty is the core reason analysis is required.

Example:

**Current condition**

> Revenue has increased during the available historical period.

**Analytical uncertainty**

> It is unclear whether growth is broadly distributed or concentrated in specific customer, product, seller, or geographic segments.

Do not fabricate performance values.

---

# 7. Business Impact

Explain why the unresolved problem matters.

Possible categories include:

* Revenue.
* Profitability.
* Customer retention.
* Customer experience.
* Operational efficiency.
* Resource allocation.
* Commercial prioritization.
* Reporting reliability.
* Decision speed.

Only include impact that is supported by the context.

If financial magnitude is unknown, do not estimate it.

Use:

`Impact magnitude: TBD`

instead of inventing a value.

---

# 8. Decision Context

Every priority Business Problem should identify the decision that future analysis is intended to support.

Assign:

`DEC-01`, `DEC-02`, ...

For each decision define:

* **Decision ID**
* **Related Problem ID**
* **Decision Owner**
* **Decision to Support**
* **Decision Timing**
* **Potential Decision Options**
* **Evidence Status**

If owner or deadline is unknown, use `TBD`.

## Decision Rule

Do not write the expected analytical conclusion as the decision.

Incorrect:

> Stop selling Category X.

Correct:

> Determine whether Category X requires pricing, product, operational, or portfolio intervention.

The analysis should inform the choice rather than assume it.

---

# 9. Analysis Objectives

Assign:

`OBJ-01`, `OBJ-02`, ...

Each Analysis Objective must trace to a Business Problem and business decision.

For each objective define:

| Objective ID | Related Problem | Related Decision | Analysis Objective | Priority |
| ------------ | --------------- | ---------------- | ------------------ | -------- |

Objectives should describe what the analysis needs to establish.

Preferred verbs:

* quantify;
* compare;
* identify;
* evaluate;
* segment;
* assess;
* determine;
* validate.

Avoid vague objectives such as:

* understand the data;
* generate insights;
* analyze business performance;
* explore trends.

Example:

> Quantify differences in repeat-purchase behavior across customer segments and geographic areas.

---

# 10. Supporting Data & Platform Problems

This section is optional.

Include it only when:

1. the user explicitly mentions a Data Warehouse, ETL, ELT, data pipeline, or analytical architecture; or
2. the Business Context contains clear evidence that data availability or integration materially limits the analysis.

Possible supporting categories include:

* Data Warehouse availability.
* Source-system fragmentation.
* ETL/ELT reliability.
* Transformation consistency.
* Historical data availability.
* Data freshness.
* Analytical-model readiness.
* Reporting-layer consistency.

For each supporting problem define:

| Supporting Problem ID | Category | Description | Analytical Impact | Evidence Status |
| --------------------- | -------- | ----------- | ----------------- | --------------- |

Use identifiers:

`DP-01`, `DP-02`, ...

where `DP` means **Data Problem**.

---

## 10.1 Depth Boundary

Describe data-platform problems only at a high level.

Allowed:

> Customer, order, and payment data currently originate from separate sources, creating additional integration requirements before cross-domain analysis can be performed.

Allowed:

> A centralized analytical warehouse is required by the project scope to provide reusable historical datasets for reporting and analysis.

Do not specify here:

* detailed medallion architecture;
* dimension/fact table design;
* orchestration activities;
* incremental-load algorithms;
* SCD implementation;
* partition strategy;
* detailed pipeline dependencies;
* cloud infrastructure configuration.

Those belong to Data Engineering or Analytics Engineering design documentation.

---

## 10.2 Analytical Relevance Rule

Every supporting data problem must explain:

> How does this problem affect the ability to answer analytical questions reliably or efficiently?

If no meaningful analytical impact exists, omit the issue from this document.

---

# 11. Problem Prioritization

Prioritize analytical problems using:

* `P0 — Critical`
* `P1 — Important`
* `P2 — Supporting`

Priority should reflect:

* relevance to the business decision;
* expected business impact;
* analytical importance;
* feasibility with available data.

Do not assign P0 merely because a problem sounds important.

Where prioritization evidence is insufficient, use:

`Priority: TBD`

---

# 12. Scope & Boundaries

Define the analytical scope derived from each problem.

Document:

### In Scope

Business areas, populations, processes, periods, or analytical concerns that belong to the problem.

### Out of Scope

Related concerns intentionally excluded.

### Boundary Rules

Do not expand scope simply because additional data exists.

Do not introduce unrelated analytical domains merely to make the project appear more comprehensive.

---

# 13. Assumptions & Constraints

Document assumptions required to frame the problem.

For each assumption include:

| Assumption | Why Required | Validation Needed |
| ---------- | ------------ | ----------------- |

Typical constraints may include:

* limited historical period;
* missing business targets;
* unavailable cost data;
* incomplete customer identifiers;
* lack of external market data;
* unavailable operational fields;
* constructed rather than official business context.

Do not use assumptions to hide unsupported facts.

---

# 14. Required Output Structure

# Business Problems

## 1. Problem Portfolio Overview

| Problem ID | Business Problem | Problem Type | Evidence Status | Priority |
| ---------- | ---------------- | ------------ | --------------- | -------- |

---

## 2. Detailed Business Problems

### PROB-XX — [Problem Name]

#### 2.1 Problem Statement

[Neutral description of the unresolved analytical problem.]

#### 2.2 Current / Claimed Condition

[What is known, observed, or claimed.]

#### 2.3 Analytical Uncertainty

[What the business does not yet know.]

#### 2.4 Business Impact

[Why resolving the uncertainty matters.]

#### 2.5 Evidence Status

[Confirmed / Source-provided / User-provided / Context-derived / Hypothesis / Unknown]

---

## 3. Decision Context

| Decision ID | Related Problem | Decision Owner | Decision to Support | Timing | Evidence Status |
| ----------- | --------------- | -------------- | ------------------- | ------ | --------------- |

---

## 4. Analysis Objectives

| Objective ID | Related Problem | Related Decision | Analysis Objective | Priority |
| ------------ | --------------- | ---------------- | ------------------ | -------- |

---

## 5. Supporting Data & Platform Problems

Include this section only when relevant.

| Data Problem ID | Category | Description | Analytical Impact | Evidence Status |
| --------------- | -------- | ----------- | ----------------- | --------------- |

If no Data Warehouse, ETL/ELT, integration, or data-platform concern exists, state:

`No material supporting data-platform problem identified from the supplied context.`

---

## 6. Scope & Boundaries

### In Scope

[...]

### Out of Scope

[...]

---

## 7. Assumptions & Constraints

| Item | Type | Description | Validation Needed |
| ---- | ---- | ----------- | ----------------- |

---

## 8. Traceability Summary

| Problem | Decision | Analysis Objective |
| ------- | -------- | ------------------ |
| PROB-XX | DEC-XX   | OBJ-XX             |

This traceability becomes the input for:

`03-business-question.md`
