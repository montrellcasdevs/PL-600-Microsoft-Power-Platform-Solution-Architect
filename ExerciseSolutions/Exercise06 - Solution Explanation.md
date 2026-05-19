# Exercise 06 - App composition and solution segmentation

## What this exercise is testing

This exercise tests whether you can move beyond an MVP and decide both application composition and ALM structure. You are being asked to think like a platform owner, not just like an app builder.

## How to analyze it

Treat the problem as two linked decisions:

1. Which user experiences are needed for the full security solution?
2. How should solution components be segmented so the system can evolve safely?

## Recommended application composition

### 1. Security operations app

Use a model-driven app for security officers and managers to manage visits, buildings, incidents, inspections, entitlements, and operational records.

Reason:

- rich relational data
- auditability
- role-based views and dashboards
- easier support for multiple processes in one secured app

### 2. Entrance tablet app

Use a canvas app for public entrance check-in and check-out because the workflow is narrow, touch-friendly, and should be optimized for speed and simplicity.

### 3. Employee self-service booking experience

Use Power Pages or an internal app depending on the audience.

Recommended direction:

- if internal employees across the business need lightweight access, Power Pages or Teams integration can work well
- if access is strictly internal and Dataverse-centric, a model-driven or canvas option may suffice

### 4. Visitor self-service experience

Use Power Pages for external visitor access to visit details, QR code retrieval, and parking registration.

### 5. Incident submission experience

Allow all employees to raise incidents through an employee-facing app or portal. This should not be forced through the security officer app.

## How to think about the swipe-card integration

The dedicated-computer constraint matters. This is an integration boundary, not just an app feature.

Recommended pattern:

- manage employee entitlements in Dataverse
- use a local integration agent, scheduled process, or on-premises data gateway pattern from the dedicated building computer
- track outbound sync status and failures centrally

## Solution segmentation recommendation

The MVP has everything in one solution. That becomes risky as scope expands.

Use segmentation. A practical design is vertical layering with some horizontal separation.

### Suggested solution set

- Core Data: tables, choices, relationships, business rules
- Security Operations App: model-driven app components
- Entry Experience: canvas app and related assets
- Portal Experience: Power Pages components
- Automation: flows, approvals, scheduled jobs
- Integration: swipe-card sync, QR generation, external connectors
- Reporting: dashboards, Power BI related artifacts if managed in solution

This lets teams deploy and version related capabilities more safely.

## Why this is better than one large solution

- clearer ownership
- less merge and deployment conflict
- better release management
- easier isolation of hotfixes

## Additional design corrections to the MVP

- The contact table may work for visitors, but confirm whether visitor records should remain distinct from broader contact management.
- Parking availability logic should be re-evaluated for concurrency and edge cases, not just morning recalculation.
- Inspection scheduling and incident management will likely need more than the current minimal automation.

## A strong solution-architect response

"I would expand the MVP into multiple user experiences: a model-driven security operations app, a tablet-oriented check-in canvas app, an employee booking experience, and a visitor self-service portal. For ALM, I would not keep everything in one solution. I would segment into core data, apps, automation, integration, and portal layers so that changes can be deployed with less coupling and clearer ownership. The swipe-card system should be treated as a constrained integration requiring a local synchronization approach and monitoring."