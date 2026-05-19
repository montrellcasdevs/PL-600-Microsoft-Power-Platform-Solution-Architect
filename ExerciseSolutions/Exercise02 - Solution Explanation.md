# Exercise 02 - Design from requirements

## What this exercise is testing

This exercise tests whether you can convert raw requirements into a high-level solution architecture, choose the right first-party products, and perform a fit-gap analysis that is practical rather than theoretical.

## How to analyze it

Start by grouping the 18 requirements into capability areas instead of treating them as isolated items.

### Capability groupings

- Service intake and routing: requirements 1, 2, 11, 14, 15
- Customer self-service: requirements 3, 10, 12, 13
- Knowledge and agent productivity: requirement 4
- Data and integration: requirement 5
- Field operations: requirements 6, 8
- Proactive service: requirement 7
- Commercial motion: requirements 9, 16
- Performance and executive reporting: requirements 17, 18

This grouping helps you avoid a fragmented design.

## Recommended solution direction

### Core platform

Use Dataverse as the operational data layer because the requirements depend on shared case, customer, agreement, bed, telemetry, SLA, and activity data.

### First-party apps

- Dynamics 365 Customer Service for case management, queues, SLAs, knowledge, agent experience, and routing.
- Dynamics 365 Field Service for onsite dispatch, work orders, scheduling, and technician experience.
- Dynamics 365 Sales or a light sales capability if selling support agreements is in scope and must be governed with quotes or agreements.
- Power Pages for customer self-service status and request submission.
- Copilot Studio for chat-based intake and deflection on the website.
- Power BI for executive near real-time reporting.

### Automation and integration

- Power Automate for notifications, escalations, status updates, and orchestration.
- Dataflows, Azure integration services, or batch processing for the nightly manufacturer feed, depending on scale and reliability requirements.

## Example fit-gap position

- Requirement 1: mostly configure with Customer Service routing, queues, skills, and SLA logic.
- Requirement 3: configure plus extend with Power Pages, Copilot Studio, and Dataverse case creation.
- Requirement 5: extend or integrate because nightly telemetry and customer-bed synchronization require external ingestion logic.
- Requirement 7: extend because proactive maintenance candidates depend on wear-indicator rules and possibly custom logic.
- Requirement 18: configure plus extend with Power BI and possibly streaming or near-real-time refresh design.

## High-level architecture to describe

Your diagram should show:

1. Channels in: phone, email, chat, web, social, manufacturer feeds.
2. Dataverse and core business tables in the middle.
3. Customer Service and Field Service as operational apps.
4. Power Pages and Copilot Studio for customer interaction.
5. Power Automate and integration services for orchestration.
6. Power BI for executive analytics.

## How to answer like a solution architect

Explain why each product is selected, which requirements it covers, and where the boundaries are between out-of-the-box configuration and custom extension.

For example:

- Use Customer Service for help-request lifecycle because queueing, SLAs, and knowledge are core capabilities.
- Use Field Service for requirement 6 and 8 because work orders, resource scheduling, and mobile technician scenarios are first-party strengths.
- Do not force nightly telemetry ingestion into a simple cloud flow if scale and restartability are important.

## Key assumptions to validate

- Are support agreements already managed in a source system?
- How much of the manufacturer feed is master data versus telemetry history?
- Is real-time executive reporting truly real-time or near real-time?
- Must online status be anonymous, authenticated, or delegated?

## Common mistakes to avoid

- Choosing canvas apps for core service processes that fit better in model-driven apps.
- Treating chat as a replacement for portal and agent workflows.
- Ignoring nonfunctional requirements such as scale, licensing, governance, and supportability.
- Marking too many items as custom when first-party products already cover most of the need.

## A strong solution-architect response

"I would center the solution on Dataverse, Dynamics 365 Customer Service, Field Service, Power Pages, Copilot Studio, Power Automate, and Power BI. I would group requirements into service operations, self-service, integration, field service, commercial processes, and analytics. My fit-gap would classify routing, knowledge, queues, SLAs, and technician dispatch as primarily first-party capabilities, while manufacturer feed processing, proactive maintenance logic, ownership transfer, and real-time metrics would require extension and integration design."