# Business Context Specification

## 1. Purpose

This document defines the business environment in which the analytical project exists.

The Business Context must help downstream analytical documentation understand:

* what business/domain the data represents;
* how the relevant business process operates;
* which stakeholders are likely involved;
* which business entities are represented by the available data;
* which current business or data-related needs make the dataset analytically relevant.

This document provides **context only**.

It must not define:

* a specific Business Problem;
* Business Questions;
* Analytical Requirements;
* Metrics;
* Data Requirements;
* conclusions or recommendations.

These belong to downstream specification documents.

---

## 2. Accepted Inputs

The skill may receive one or multiple input sources.

### 2.1 Web / Dataset Sources

Examples:

* Dataset landing page.
* Dataset documentation page.
* Company or organization website.
* Public documentation.
* Open-data portal.
* Kaggle or similar dataset page.
* Public report or article related to the dataset/domain.

Input example:

`https://example.com/dataset/...`

---

### 2.2 GitHub Repository

Examples:

* Dataset repository.
* Analytics project repository.
* Data dictionary.
* Schema documentation.
* README.
* SQL models.
* CSV files stored inside the repository.

Input example:

`https://github.com/owner/repository`

The repository must be inspected for relevant business and data context before external assumptions are introduced.

---

### 2.3 Uploaded Dataset

Supported examples include:

* CSV.
* Excel (`.xlsx`, `.xls`).
* Structured tabular datasets.

When a raw dataset is supplied, inspect available evidence such as:

* file names;
* worksheet names;
* table structure;
* column names;
* data types where available;
* entity relationships that can be safely inferred;
* metadata supplied with the file.

Do not use data values to perform actual analysis at this stage.

Dataset inspection is used only to understand the represented business domain and available entities.

---

### 2.4 Multiple Sources

When multiple inputs are available, use them together.

Recommended evidence precedence:

1. Official dataset/company documentation.
2. Dataset metadata or schema.
3. Repository documentation.
4. Authoritative external sources.
5. Reputable industry sources.
6. Constructed analytical assumptions.

Do not allow a weaker source to silently override a stronger source.

---

# 3. Context Generation Modes

The Business Context must operate in one of two modes.

---

## Mode 1 — Source-Grounded Context

Use this mode when the supplied website, dataset page, documentation, repository, or accompanying metadata already provides sufficient business context.

### Objective

Preserve and structure the existing context rather than inventing a new business scenario.

### Workflow

1. Inspect the supplied source.
2. Identify explicitly stated business/domain information.
3. Identify the organization, platform, process, or operational environment represented by the data.
4. Identify relevant stakeholders when explicitly documented.
5. Identify available business entities from documentation or schema.
6. Identify explicitly stated objectives, operational concerns, or use cases.
7. Structure this information using the output template in Section 6.
8. Mark material information with the appropriate evidence status.

### Evidence Status

Prefer:

* `Confirmed`
* `Source-provided`
* `Schema-derived`

Do not rewrite an existing business context into a substantially different scenario merely because another scenario appears more analytically interesting.

### Example

If dataset documentation explicitly states that the data belongs to an e-commerce marketplace connecting customers and sellers, preserve that context.

Do not transform it into:

> The company is currently facing severe customer-retention problems.

unless the supplied source actually states this.

---

## Mode 2 — Constructed Analytical Context

Use this mode when the supplied source provides data but does not contain enough business context for a meaningful Data Analyst project.

Examples:

* A CSV with transaction records but no business description.
* A database schema with little domain documentation.
* A GitHub repository containing raw data only.
* A dataset page describing fields but not the business use case.

### Objective

Construct a **plausible and analytically useful business context** grounded in:

1. evidence from the supplied dataset;
2. the identifiable business/domain represented by the data;
3. current external information about similar businesses, industries, or operational challenges.

The resulting context should represent a realistic scenario for modern Data Analyst work without falsely claiming that it is the actual internal context of the original organization.

### Required Workflow

#### Step 1 — Identify Dataset Domain

Determine what domain the dataset most likely represents.

Examples:

* E-commerce.
* Retail.
* Logistics.
* Transportation.
* SaaS.
* Banking.
* Marketing.
* Healthcare.
* Manufacturing.

Base this classification primarily on supplied metadata, schema, entities, and documentation.

---

#### Step 2 — Identify Available Business Entities

Identify only entities supported by the dataset.

Examples:

* Customer.
* Order.
* Product.
* Seller.
* Shipment.
* Payment.
* Campaign.
* Subscription.
* Incident.

Do not invent entities that cannot be connected to the available data.

---

#### Step 3 — Research Relevant External Context

Research authoritative or reputable sources about current challenges, operating models, or analytical needs in the identified domain.

Prefer sources such as:

* official company documentation;
* government or regulatory publications;
* established industry organizations;
* major consulting or research publications;
* reputable technology/data publications;
* authoritative domain-specific sources.

External research should answer questions such as:

* What business pressures are currently relevant to this domain?
* Which operational or customer challenges are commonly monitored?
* What decisions are increasingly data-driven?
* Which trends materially affect businesses represented by this dataset?

Do not collect trends merely because they are popular.

Only retain context that can reasonably connect to the available dataset.

---

#### Step 4 — Test Dataset–Context Compatibility

Before including an external business need, verify:

`Can the supplied dataset plausibly support analysis related to this context?`

If not, exclude it.

Example:

Dataset contains:

* orders;
* customers;
* products;
* delivery timestamps.

Reasonable context:

* customer purchasing behavior;
* product performance;
* fulfillment efficiency;
* delivery performance.

Unsupported context:

* employee productivity;
* advertising ROI;

unless employee or advertising data is also available.

---

#### Step 5 — Construct the Analytical Context

Combine:

`Dataset Evidence + Domain Context + Relevant Current Business Need`

into a coherent analytical context.

The context should explain why the available data could reasonably be analyzed by a modern Data Analyst.

---

#### Step 6 — Label Constructed Content

All material context that is not explicitly supplied by the original dataset source must be distinguishable as:

`Constructed Context`

or:

`Externally Grounded Context`

Do not represent constructed context as an official business statement from the dataset owner.

---

# 4. Context Construction Rules

## 4.1 Evidence Before Plausibility

Prefer what is known over what merely sounds realistic.

Never replace documented context with a more interesting invented scenario.

---

## 4.2 Do Not Invent Internal Company Facts

For Mode 2, never fabricate statements such as:

* revenue declined by 20%;
* churn is increasing;
* management has set a target of 15%;
* the company recently lost market share;
* the CEO requested this analysis;
* operating costs increased last quarter.

Unless supported by a source, these are not Business Context facts.

Such statements belong later as hypotheses or constructed Business Problems if explicitly requested.

---

## 4.3 Context Is Not the Business Problem

Do not turn the Business Context into a predetermined analytical problem.

Incorrect:

> The company suffers from poor customer retention and must identify why customers are leaving.

Better:

> Customer retention and repeat purchasing are important analytical concerns in e-commerce because sustainable growth depends on both customer acquisition and continued purchasing behavior.

The first claims an internal problem.

The second establishes relevant business context.

---

## 4.4 Current Business Relevance

For Mode 2, favor context relevant to current data-driven business needs.

Potential categories include:

* customer acquisition and retention;
* profitability;
* operational efficiency;
* product performance;
* fulfillment and service quality;
* geographic performance;
* inventory efficiency;
* seller/vendor performance;
* conversion;
* customer experience;
* risk monitoring.

However, include a category only when the supplied dataset can reasonably support it.

---

## 4.5 Avoid Artificial Complexity

The goal is not to invent the most sophisticated business scenario possible.

For a personal Data Analyst project, prioritize a context that is:

* realistic;
* understandable;
* supported by available data;
* rich enough to generate meaningful analytical problems;
* simple enough to explain during an interview.

---

# 5. Evidence Classification

Use the following statuses when useful.

| Evidence Status       | Meaning                                                                    |
| --------------------- | -------------------------------------------------------------------------- |
| `Confirmed`           | Explicitly supported by an authoritative supplied source                   |
| `Source-provided`     | Explicitly stated on the supplied webpage/repository/dataset documentation |
| `Schema-derived`      | Directly supported by tables, columns, entities, or metadata               |
| `Externally grounded` | Supported by external domain/business research                             |
| `Constructed context` | Synthesized for the analytical project from available evidence             |
| `Unknown`             | Cannot be established from available information                           |

Do not label constructed context as `Confirmed`.

---

# 6. Required Output Structure

# Business Context

## 1. Project Metadata

* **Project / Dataset Name:**
* **Primary Source:**
* **Source Type:** Website / Dataset Page / GitHub / CSV / Excel / Other
* **Context Mode:** Source-Grounded / Constructed Analytical Context
* **Domain:**
* **Context Status:** Draft / Validated

---

## 2. Business / Domain Overview

Describe:

* the relevant industry or domain;
* the business model or operating environment represented by the dataset;
* the role played by the major entities represented in the data.

For Mode 1, prioritize source-provided information.

For Mode 2, clearly distinguish externally grounded or constructed context.

---

## 3. Operating Context

Describe the business process represented by the available data.

Focus only on processes supported by the source.

Example for e-commerce:

`Customer -> Order -> Payment -> Fulfillment -> Delivery`

Do not invent unsupported process stages.

---

## 4. Key Stakeholders

Identify stakeholders relevant to the represented business process.

For each stakeholder, specify:

| Stakeholder | Role in Context | Evidence Status |
| ----------- | --------------- | --------------- |

Do not invent named individuals.

Generic organizational roles may be used for constructed contexts when reasonable, such as:

* Sales Manager.
* Marketing Manager.
* Operations Manager.
* Product Manager.
* Customer Experience Team.

---

## 5. Key Business Entities

Document major entities supported by the available data.

| Entity | Business Meaning | Evidence Source |
| ------ | ---------------- | --------------- |

Examples:

* Customer.
* Order.
* Product.
* Seller.
* Payment.

Only include entities supported by the supplied source/schema.

---

## 6. Current Business & Data Context

Describe the business conditions that make analysis of this dataset relevant.

### For Source-Grounded Mode

Include context explicitly stated by the supplied sources.

### For Constructed Analytical Context Mode

Include externally grounded modern business needs that:

1. are relevant to the identified domain;
2. can reasonably be analyzed using the supplied data;
3. are not presented as confirmed internal company problems.

Clearly identify these statements as externally grounded or constructed.

---

## 7. Analytical Relevance

Explain why the available data is useful for analytical decision support.

Map:

`Available Data -> Business Area -> Potential Analytical Value`

Do not define final Business Questions here.

Example:

| Available Data      | Business Area | Potential Analytical Value                   |
| ------------------- | ------------- | -------------------------------------------- |
| Orders              | Sales         | Evaluate sales patterns over time            |
| Customers           | Customer      | Understand customer composition and behavior |
| Delivery timestamps | Operations    | Evaluate fulfillment performance             |

---

## 8. Known Context Limitations

Document limitations such as:

* missing business documentation;
* incomplete dataset description;
* unknown organizational objectives;
* unclear business rules;
* constructed rather than official context;
* unavailable external evidence.

Do not resolve a limitation through unsupported assumptions.

---

## 9. Source & Evidence Summary

List the major sources used to construct the Business Context.

For each source, record:

| Source | Purpose | Evidence Type |
| ------ | ------- | ------------- |

For Mode 2, clearly distinguish:

* dataset evidence;
* external domain evidence;
* constructed analytical interpretation.
