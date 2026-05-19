# Exercise 04 - Model data

## What this exercise is testing

This exercise tests whether you can design a data model that supports both operational processes and reporting, while separating what belongs in Dataverse from what should remain in external systems.

## How to analyze it

Break the requirements into entities, relationships, lifecycle events, and data storage decisions.

### Likely core tables

- Visitor
- Visit
- Guest or Visit Guest
- Reservation
- Waiver Acceptance
- Tracking Device Assignment
- Sales Lead or Opportunity link
- Location Tracking Snapshot or Tracking Session reference

Use standard tables where they fit. Contact can often represent visitors if that aligns with future engagement and identity needs.

## Recommended data-model direction

### Visitor and visit structure

- Use Contact for the person when reuse across multiple visits matters.
- Use a custom Visit table for each reservation or attendance occurrence.
- Use a related Guest table or guest-child visit records if guests must be named and checked individually.

### Sales linkage

- If the visitor was invited by sales staff, relate the visit to Lead, Opportunity, or Account depending on where the sales process is governed.
- If the visitor is recreational only, allow the visit without a sales-process relationship.

### Photos

Store photos outside the row when possible and keep Dataverse as the metadata system.

Recommended approach:

- Store the image in Dataverse image or file capability if the volume is manageable and direct app display is needed.
- If scale or retention is a concern, store in SharePoint or Azure Blob and save the reference plus metadata in Dataverse.

### Waiver acceptance and signature

Create a Waiver Acceptance table linked to Visit and Visitor with:

- accepted date/time
- waiver version
- signature or signed-document reference
- capture method
- audit fields

This must be stored per visit because the requirement says each visit requires acceptance.

### Tracking data

Do not push high-volume location telemetry directly into core operational tables unless you have a strong reason. A better pattern is:

- Dataverse stores device assignment, session metadata, and the latest summarized or relevant view.
- The tracking cloud or a supporting data store retains detailed telemetry.
- Sales users access tracking details through embedded experiences, virtual tables, custom pages, or a custom connector depending on latency and UX needs.

## How to accommodate reporting needs

Marketing wants visit analytics and close rates after visits. Design for reporting early.

Recommended approach:

- Ensure Visit has timestamps, visitor type, invitation source, and related sales identifiers.
- Use Power BI over Dataverse and the sales data model.
- Create measures for visits by day, month, quarter, and downstream conversion rate.

## Use of Common Data Model

Yes, use standard tables where possible:

- Contact for person
- Lead or Opportunity for sales relationship
- User for employees

Use custom tables where the business concept is domain-specific, such as Visit, Waiver Acceptance, and Device Assignment.

## Risks and tradeoffs

- Putting all telemetry in Dataverse may become expensive and noisy.
- Storing signatures as simple text without versioning may fail legal review.
- Modeling guests only as free text reduces traceability and safety compliance.

## A strong solution-architect response

"I would separate person identity, visit events, compliance records, and telemetry concerns. Contact can represent recurring visitors, while Visit handles each reservation and arrival. Waiver acceptance should be a per-visit record with signature evidence and versioning. Tracking data should be summarized into Dataverse and exposed to sales through a connector or embedded experience rather than storing raw telemetry indiscriminately. I would design the schema so reporting can correlate visits to later sales outcomes."