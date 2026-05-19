# Exercise 10 - First-party apps

## What this exercise is testing

This exercise tests whether you know when to solve a requirement with standard Dynamics 365 capabilities, when to configure, when to extend, and when to avoid first-party apps for a specific need.

## How to answer it

For each requirement, classify it as one of these:

- out of the box
- configure
- extend
- integrate
- not a first-party-app responsibility

Then justify the choice briefly.

## Dynamics 365 Sales

### Parent account details on contact

Usually configure. Use quick view forms or related information on the contact form.

### Preferred pricing with expiration

Configure plus extend as needed. Use price lists, agreements, validity dates, and automation to revert pricing when the agreement expires.

### Product configurator currently in WPF

This is an integration or redevelopment decision. Do not assume Dynamics 365 Sales replaces a complex configurator by itself. The architect should evaluate embedding, API-based integration, or rebuilding if justified.

### Show and hide fields on opportunity

Configure with business rules or client logic depending on complexity.

### Real-time top current events on account form

Integrate external news or events through a connector, embedded component, or custom control. This is not a core Sales feature by itself.

### Reassign over $1M opportunities to the user's team and notify

Configure or extend with Power Automate and team ownership logic. Validate ownership semantics carefully.

### Current lead stage in grid

Likely extend or configure through a surfaced column reflecting process stage. Standard grids do not always expose what users expect without extra setup.

## Dynamics 365 Customer Service

### Sell support tickets without leaving the case

Likely use embedded or related sales process capability. This may be configure plus extend depending on whether support-ticket products and commerce flow already exist.

### Offer more incidences to preferred customers when depleted

Good fit for automation and sales follow-up logic.

### Users must not access on mobile devices

This is an access-policy and device-management question, not just app configuration. Consider conditional access and app-level restrictions.

### Dispatch available qualified field resource

Use Dynamics 365 Field Service integration. This is a strong first-party scenario.

### Personal chart should be available to all agents

Recreate as a system chart or dashboard rather than relying on one user's personal artifact.

### Current case stage in grid

Same pattern as lead stage. Usually requires exposing the stage in a usable column or custom presentation.

### Show and hide sections on case form

Configure with business rules or client logic.

## Dynamics 365 Field Service

### Auto-update skills after training completion

Integrate training-system outcomes with resource skill records.

### All screens under 5.25 seconds

This is a nonfunctional requirement. It must be addressed with performance design, telemetry, optimization, and testing, not a single feature switch.

### Resources must be certified before completing tickets unsupervised

Use qualification, security, and business-rule enforcement. Possibly combine skill/certification data with booking or completion validation.

### Each work order requires a work order type

Mostly configuration.

### Dispatchers book 70 percent, technicians self-book via mobile

Use standard Field Service booking patterns where possible, with mobile enablement and guardrails.

### Avoid unnecessary technician dispatch

Use triage, remote diagnostics, knowledge, and better intake before creating or dispatching work orders.

## A strong solution-architect response

"I would classify each requirement by whether Dynamics 365 can handle it out of the box, through configuration, through extension, or only through integration. The key is not to overstate first-party coverage. Quick views, charts, business rules, Field Service scheduling, and standard process controls cover several items well. Complex configurators, external event feeds, and training-driven skill updates are integration-led problems. Performance and device restrictions are architecture and governance concerns, not simple feature toggles."