# Exercise 09 - Evaluate integration options

## What this exercise is testing

This exercise tests whether you can choose the right inbound or outbound integration pattern based on volume, freshness, coupling, data-retention rules, and operational support.

## How to analyze each scenario

For every integration ask:

- Is the data pushed or pulled?
- How fresh must it be?
- What is the volume?
- Is Dataverse the system of record or only a consumer?
- What happens when the external system is down?
- How will failures be detected and replayed?

## Scenario 1 - Weekly property hazard file

### Analysis

555,000 records total with about 1,000 weekly changes indicates a batch synchronization pattern. The unique key is county plus parcel ID.

### Recommended design

- Scheduled ingestion from the supplied URL.
- Land the JSON file in staging.
- Transform and upsert using county plus parcel ID as the business key.
- Store hazard indicator, hazard type, and last-reported date.
- Log import batch status and rejects.

### Why this works

This is not a real-time API scenario. Batch processing is simpler and more supportable.

## Scenario 2 - Property tax authority API

### Analysis

The data changes continuously and can only be stored locally for 24 hours. That means the app should retrieve on demand or cache very carefully. Weekend downtime must be handled gracefully.

### Recommended design

- Call the REST API on demand through a custom connector or integration layer.
- Present the data in the model-driven app without making Dataverse the long-term store.
- If short-lived caching is used, enforce the 24-hour retention rule.
- Surface unavailability and send operational alerts to the manager when transmission fails.

### Why this matters

A scheduled sync into Dataverse would violate the freshness and retention profile.

## Scenario 3 - Outbound customer data to outsourced support

### Analysis

This is an outbound event-style integration using a webhook. Reliability and alerting are the key issues.

### Recommended design

- Trigger on new and changed customer records.
- Transform to the provided JSON schema.
- Post to the webhook.
- Capture request and response details in an integration log.
- Retry transient failures.
- Notify the manager on persistent failures.

### Additional note

Use an integration queue or durable mechanism if delivery guarantees are important.

## Scenario 4 - Internal referral API

### Analysis

Only about 25 leads per week and both parties are on the same internal network. This is low volume and can support a simple API-based inbound pattern.

### Recommended design

- Expose a secured API endpoint through Power Platform or Azure API Management fronting Dataverse logic.
- Validate account existence.
- Create account if needed, then opportunity.
- Route to sales team by region.
- Create research task.
- Return a response with status and identifiers.

### Why this works

The volume is low enough for a transactional service pattern, and the sending division explicitly asked for API access.

## A strong solution-architect response

"I would choose patterns based on data shape and freshness. Weekly hazard data is a staged batch upsert. Property tax data should be retrieved on demand because retention is tightly constrained and source data changes constantly. Outbound customer synchronization to the outsourced support firm should be event-driven with retries, logging, and manager alerts. Internal referrals are best handled through a secured API that performs the account, opportunity, assignment, and task creation steps in one controlled process."