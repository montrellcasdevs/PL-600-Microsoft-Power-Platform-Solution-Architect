# Exercise 05 - Power Apps architecture

## What this exercise is testing

This exercise tests whether you can select the right app types for different user groups and combine Power Apps, connectors, components, and automation into one coherent application architecture.

## How to analyze it

Start by separating users by work style, device context, security boundary, and business need.

### User groups

- Sales staff
- Sales managers
- Reception staff
- External visitors or customers
- Administrators and support staff

These users should not all be forced into one app.

## Recommended app architecture

### Sales staff and sales managers

Use a model-driven app, likely centered on Dynamics 365 Sales capabilities, because the process is data-rich, relational, and tied to leads, opportunities, visits, approvals, and reporting.

Why:

- better fit for structured business data
- built-in security and business process support
- easier reuse of forms, views, dashboards, and role-based access

### Reception staff

Use a canvas app for visitor check-in because it is task-based, optimized for a narrow workflow, and needs simple photo capture with minimal exposure to sales data.

### External customers requesting visits

Use Power Pages so external users can request showroom visits and manage limited self-service interactions.

## How to accommodate offline or poor connectivity

The large-deal sales staff work in unreliable connectivity conditions. You should explicitly address this.

Recommended direction:

- Prefer model-driven app offline capability if the user journey and tables are supported.
- If the experience requires more tailored offline behavior, evaluate a dedicated canvas app for a specific mobile scenario.
- Limit the offline data footprint to the minimal records needed for meetings and follow-up.

## Custom connector usage

The device-service cloud API should not drive the core sales data model directly. Use a custom connector to surface tour-tracking data in the sales experience.

Recommended pattern:

- Keep system-of-record data in Dataverse.
- Use the connector for on-demand retrieval of tracking details or summarized views.
- Cache or persist only business-relevant summaries when they need to participate in reporting or downstream automation.

## Where PCF can help

Potential component uses:

- QR or badge display component
- map or floor-journey visualization
- richer tracking timeline visualization in the sales app
- controlled discount approval UI if a tailored experience is needed

Use PCF only where standard controls are insufficient.

## What to offload to Power Automate

- reminder SMS 24 hours before visit
- notifications and approvals
- follow-up communications
- integration handoffs where response time is not immediate

Do not use flows for client-side UI behavior that users expect instantly.

## Multi-maker canvas-app strategy

If a canvas app is used, plan for maintainability:

- use solution-aware development
- split reusable UI and logic into components
- define ownership boundaries by screen or feature area
- use source control and environment-based deployment

## A strong solution-architect response

"I would use a model-driven app for sales and management, a canvas app for reception check-in, and Power Pages for external visit requests. I would support low-connectivity field selling with offline design rather than assuming always-on access. The custom connector should expose tracking data to the sales experience without turning the external telemetry API into the core system of record. Power Automate should handle reminders, approvals, and asynchronous notifications, while PCF is reserved for specialized UX elements such as tracking visualization or QR interactions."