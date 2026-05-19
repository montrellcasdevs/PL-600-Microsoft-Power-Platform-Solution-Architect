# Exercise 07 - Power Automate architecture

## What this exercise is testing

This exercise tests whether you can decide when Power Automate is appropriate, when it is not, and how to design flows that are reliable, scalable, and aligned with user-experience expectations.

## General decision rule

Use Power Automate for orchestration, approvals, notifications, and asynchronous integration. Be careful when the requirement needs instant in-form calculation, very high volume processing, or strong transactional behavior.

## Scenario 1 - Replacement bed authorization

### Analysis

This is a business process with human approval, external communication, and customer follow-up. That is a strong fit for Power Automate.

### Recommended design

- Trigger from case or replacement request record.
- Determine manufacturer and approval contact.
- Send approval request through the appropriate channel.
- Record approval outcome and timestamps in Dataverse.
- Notify support staff and optionally customer when approval is granted.
- Add timeout, reminder, and escalation behavior.

### Why this works

It is workflow-centric, auditable, and not latency-sensitive at sub-second level.

## Scenario 2 - Warranty allowance and prioritization

### Analysis

A plug-in may be too heavy if the logic is mainly orchestration and data updates. However, if the user must see the result immediately during save, timing matters.

### Recommended design

- If near-immediate post-create calculation is acceptable, use a real-time or low-latency automation pattern with Dataverse-triggered flow and careful performance testing.
- If the value must be shown instantly during record creation, consider calculated logic, client-side logic, or a server-side extension depending on the complexity.
- Reserve plug-ins for strict transaction requirements or logic that cannot tolerate eventual consistency.

### Architect answer

Do not accept "use a plug-in" by default. Explain that the decision depends on required immediacy, transactional consistency, and maintainability.

## Scenario 3 - Large recall file, 200,000+ beds

### Analysis

This is the clearest case where naive cloud-flow processing is risky. Volume, restartability, and deduplication are the controlling concerns.

### Recommended design

- Ingest the file into a staging location.
- Store import batch metadata and processing status.
- Process records in chunks.
- Use an idempotency key based on serial number plus recall identifier.
- Upsert or tag affected records instead of blind create.
- Log errors by batch and record.
- Allow restart from the last successful checkpoint.

### Tooling position

Power Automate can participate in orchestration, but Azure services or a more robust batch-processing approach may be better for the heavy lifting.

## Scenario 4 - Deductible shown immediately on create

### Analysis

The requirement says support staff need the value displayed as soon as they create the record. That points away from an asynchronous flow.

### Recommended design

- Prefer a formula, calculated column, business rule, client script, or plug-in depending on where the bed age data and percentage rules live.
- Use Power Automate only if the timing requirement can tolerate delay, which the scenario suggests it cannot.

## A strong solution-architect response

"I would use Power Automate for approval and communication workflows, but I would not force every scenario into a flow. Scenario 1 is a strong orchestration use case. Scenario 3 needs a restartable batch pattern with staging, chunking, and idempotency, potentially with Azure support. Scenario 4 likely needs synchronous logic because the deductible must be visible immediately. The right answer is not just whether Power Automate can do it, but whether it should own the critical part of the solution."