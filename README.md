# Desglose AI — Technical Case Study

**Desglose AI is an AI-assisted platform for public procurement planning in Chile.**

The product helps public-sector teams transform an institutional purchasing need into structured requirements — items, quantities, specifications, and supporting procurement references — while keeping a human reviewer in control of the final output.

I am the founder and sole product engineer behind Desglose AI.

> This repository documents the product and engineering decisions behind Desglose AI. Proprietary source code, private infrastructure, credentials, and internal operational configuration are intentionally excluded.

## The problem

Public procurement often begins with an informal need:

> “We need 12 notebooks for a school laboratory.”

That need still has to become a usable purchasing requirement:

- What exactly needs to be purchased?
- How many units?
- Which specifications matter?
- What level of detail is appropriate?
- What budget is realistic?
- What comparable purchases have other public institutions made?

Much of this work is manual, repetitive, and difficult to standardize.

Desglose AI is designed to reduce that friction without removing human oversight.

## What I am building

The core workflow turns an unstructured purchasing need into a reviewable procurement draft.

For example:

```text
Input

"12 notebooks for a school laboratory"
```

becomes:

```text
Structured requirement

Item: Notebook computer
Quantity: 12

Specifications:
- Processor requirements
- Memory
- Storage
- Display
- Connectivity
- Operating requirements
```

The user can then review and adjust the generated requirement before using it operationally.

## Product workflow

```text
Institutional need
        ↓
AI-assisted requirement generation
        ↓
Structured items and quantities
        ↓
Technical specifications
        ↓
Comparable public purchases
        ↓
Budget-supporting evidence
        ↓
Human review
        ↓
Exportable purchasing requirement
```

The system is designed around a simple principle:

> AI proposes structure. The user remains responsible for the purchasing decision.

## Core product capabilities

### Requirement generation

The product converts natural-language purchasing needs into structured procurement requirements.

The output can include:

- Items
- Quantities
- Technical specifications
- Relevant constraints
- Structured descriptions
- Procurement-ready organization

### Human review

Generated content is not treated as authoritative.

Users can inspect and modify the requirement before it becomes a final document.

This is important because procurement specifications can affect:

- Budget
- Supplier eligibility
- Technical compatibility
- Institutional operations
- Purchasing outcomes

AI is used to accelerate the drafting process, not replace institutional judgment.

## Comparable purchases

One of the central capabilities under development is **Compras similares**.

For each requirement, Desglose aims to surface real public purchases with comparable characteristics.

Example:

```text
Requirement

12 notebooks for a school laboratory
```

The system can use comparable procurement records to help answer questions such as:

- What have similar institutions purchased?
- When was the purchase made?
- What price was paid?
- How similar was the purchase?
- Is the proposed budget consistent with recent public procurement activity?

The goal is not to generate an arbitrary AI price.

The goal is to connect purchasing decisions with traceable public procurement evidence.

## Procurement data

The data strategy is based on Chilean public procurement records.

The current development work is focused on replacing demonstration prices with real comparable purchases drawn from a corpus of approximately **4.8 million public procurement records**.

This introduces several engineering problems beyond simple semantic search:

- Identifying genuinely comparable purchases
- Normalizing product descriptions
- Comparing quantities and units
- Handling price variation over time
- Detecting irrelevant matches
- Ranking comparable records
- Preserving the source of every reference
- Separating evidence from model-generated interpretation

## Relevance over superficial similarity

Two purchases can contain similar words without being useful comparables.

For example:

```text
"Notebook for administrative use"
```

and:

```text
"High-performance notebook for architecture laboratory"
```

may share the same general category while representing very different requirements and price ranges.

The comparable-purchase layer therefore needs to consider more than keywords.

Relevant signals may include:

- Product category
- Technical characteristics
- Quantity
- Institutional context
- Date
- Procurement description
- Price range
- Purchase purpose

A major product question is how to rank comparables so that the references are useful rather than merely textually similar.

## Evidence and traceability

A central design principle is that procurement evidence must remain inspectable.

Where the system presents information derived from public purchasing data, the user should be able to distinguish:

```text
AI-generated interpretation
```

from:

```text
Source procurement record
```

This reduces the risk of presenting generated content as factual procurement evidence.

## AI design

Desglose uses AI primarily for tasks where language interpretation is valuable:

- Understanding an institutional need
- Decomposing that need into structured items
- Proposing specifications
- Organizing procurement requirements
- Interpreting comparable records

Deterministic software and structured data should handle the parts of the workflow where correctness and traceability matter more than linguistic flexibility.

The architecture follows this boundary:

```text
Natural language
      ↓
LLM interpretation
      ↓
Structured output
      ↓
Validation
      ↓
Procurement data
      ↓
Deterministic processing
      ↓
Human review
```

## Product principles

### Human-in-the-loop

Desglose is not designed to autonomously execute procurement decisions.

The user remains responsible for reviewing:

- Specifications
- Quantities
- Comparable purchases
- Budget assumptions
- Final purchasing documents

### Structured outputs

AI-generated text becomes more useful when it is converted into structured, inspectable data rather than treated as free-form prose.

### Evidence before confidence

A fluent AI response is not evidence.

Where possible, factual claims about previous purchases and prices should be tied to actual procurement records.

### Explainable recommendations

Comparable purchases should be accompanied by enough context for the user to understand why they were selected.

### Operational usefulness

The objective is not to demonstrate AI.

The objective is to reduce the work required to move from:

```text
"We need to buy something"
```

to:

```text
"We have a structured requirement that can be reviewed and used in a procurement process."
```

## Engineering challenges

### Retrieval quality

Finding purchases that are actually comparable is harder than simple text matching.

The system must balance:

- Recall
- Precision
- Semantic similarity
- Product attributes
- Price relevance
- Temporal relevance

### Price normalization

Public procurement data can contain differences in:

- Unit price
- Total price
- Quantity
- Currency
- Bundled products
- Taxes
- Purchase date

Those differences have to be handled before prices can be meaningfully compared.

### Data quality

Historical procurement records are not guaranteed to have clean or consistent product descriptions.

The system therefore needs to tolerate:

- Missing attributes
- Inconsistent terminology
- Abbreviations
- Typographical errors
- Mixed product descriptions
- Different units of measurement

### AI hallucination risk

Procurement is a poor domain for invented evidence.

The system must prevent the LLM from manufacturing:

- Historical purchases
- Prices
- Institutions
- Procurement identifiers
- Unsupported specifications

Real procurement references must come from the data layer rather than model memory.

## Current development focus

The current priority is the **Compras similares** layer.

The main engineering objective is to move from demonstration pricing toward real procurement evidence.

The system is being evaluated around:

- Comparable-purchase relevance
- Coverage across purchasing categories
- Price-reference usefulness
- Stability of results over time
- Traceability of source records

## My role

As founder and sole product engineer, I work across:

- Product definition
- User workflows
- UX
- AI system design
- Data architecture
- Retrieval strategy
- Backend logic
- Validation
- Product experimentation
- Technical documentation
- Deployment decisions

AI coding tools are part of the engineering workflow, but architecture, product decisions, validation, and production decisions remain human-controlled.

## Current status

Desglose AI is under active development.

The core product direction and requirement-generation workflow are established.

The main technical work currently focuses on connecting the product with real public procurement evidence and improving the quality of comparable-purchase retrieval.

The product should not yet be interpreted as having validated product-market fit or as providing authoritative procurement pricing.

## Repository scope

This repository intentionally does not include:

- Proprietary production source code
- Credentials
- Private infrastructure configuration
- Internal prompts
- Non-public operational documentation
- Private datasets
- Commercial information

The repository exists to document the product architecture, engineering problems, design decisions, and technical evolution of Desglose AI.

## About

Desglose AI is an independent product developed by **HaikuFlow** in Chile.

[HaikuFlow](https://haikuflow.com) · [GitHub](https://github.com/holahaikuflow) · [LinkedIn](https://www.linkedin.com/in/victorurrutiacisterna/)
