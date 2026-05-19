# Exercise 03 - Review workbook

## What this exercise is testing

This exercise tests whether you can review another architect's work with discipline. The point is not to prove the other team wrong. The point is to determine whether their design is coherent, complete, and defensible against the stated requirements.

## How to analyze it

Review the workbook in three passes.

### 1. Coverage pass

Check whether every requirement is represented somewhere in the architecture, app list, or fit-gap matrix.

### 2. Decision-quality pass

Review whether the chosen products and app types are appropriate. Look for mismatches such as using a canvas app where Customer Service or Field Service already provides stronger capabilities.

### 3. Delivery-risk pass

Identify ambiguity, missing assumptions, hidden custom effort, licensing impact, and operational risk.

## What to review in the architecture diagram

- Does it show all major channels, systems, and users?
- Does it distinguish operational apps, self-service, automation, and integration?
- Does it reflect core data entities and external dependencies?
- Does it make field service, reporting, and customer-facing experiences visible?

## What to review in the app-selection tab

- Are first-party Dynamics 365 apps used where they are a natural fit?
- Have they introduced unnecessary custom apps?
- Have they justified portal, chatbot, or mobile choices?
- Have they acknowledged licensing and governance implications?

## What to review in the fit-gap tab

For each requirement ask:

- Is the category correct: out-of-the-box, configure, extend, integrate, or third-party?
- Is the effort estimate believable?
- Does the implementation detail mention the real controlling component?
- Are risks and assumptions surfaced?

## How to provide good feedback

Constructive feedback should have this form:

1. Observation: what you saw.
2. Impact: why it matters.
3. Recommendation: how to improve it.

Example:

"Requirement 5 is marked as a simple flow, but the nightly manufacturer feed looks like a higher-volume integration. That matters because restartability, deduplication, and monitoring may be weak in a basic flow design. I would recommend describing an ingestion pattern with staging, idempotency, and replay."

## What strong feedback usually covers

- missed requirements
- app-type mismatches
- over-customization
- underestimated integration complexity
- weak security or ALM thinking
- unclear ownership of assumptions

## Poorly written requirement example

If asked to identify one, choose a requirement that lacks measurable acceptance criteria. Requirement 17 is a strong candidate because "acceptable response time" is vague. A solution architect should ask for a target such as page-load thresholds, regional expectations, and which user journeys matter.

## A strong solution-architect response

"I would review the workbook for requirement coverage, decision quality, and delivery risk. My feedback would focus on whether the architecture clearly maps each requirement to the right product and whether the fit-gap analysis is realistic. I would keep feedback constructive by explaining the design impact and offering a better option, especially where integration, SLA management, field service, or portal security appear under-specified."