# PL-600 Practice Solution Build Plan

## Goal
Build a complete Power Platform + Dynamics 365 solution that satisfies the workbook requirements and gives exam-quality implementation practice.

## Scope (from your exercises)
- Intake and routing of support/cancellation requests
- Agent workspace for queue handling and SLA tracking
- Customer self-service status via Power Pages + chatbot
- Offer/discount workflow with manager approval
- Notifications, escalations, and lifecycle retention cleanup
- Integration back to originating systems with reliability controls
- Security model with roles, business units, teams, and Entra groups
- ALM with managed solutions and pipeline promotion

## Reference artifacts
- Exercises: [Instructions/Exercises](Instructions/Exercises)
- Filled workbook (moved): [Project Workbook PL-600 Applied Exercise.xlsx](../Project%20Workbook%20PL-600%20Applied%20Exercise.xlsx)

## Phase 1 - Foundation (Day 1)
1. Create environments: Dev, Test/UAT, Prod.
2. Define DLP policies (block non-approved external connectors).
3. Create base solution structure:
   - `Core.Data`
   - `Core.Apps`
   - `Core.Automation`
   - `Core.Integration`
   - `Core.Reporting`
4. Create environment variables + connection references.

## Phase 2 - Dataverse model (Day 1-2)
Create/extend tables:
- Account, Contact
- Complaint/Cancel Request
- Service Agreement
- Offer
- Integration Event
- Reason, Channel, Priority, Sentiment, Resolution Type (reference)

Add:
- Required relationships and cascading rules
- Business rules for required data and status progression
- Auditing on key fields (discount, SLA dates, resolution)

## Phase 3 - Apps (Day 2-3)
1. Model-driven app: **Retention Hub**
   - Queue views, My Work, SLA indicators, timeline
2. Power Pages portal
   - Authenticated customer status page
   - New request + follow-up submission
3. Copilot Studio chatbot
   - FAQ + request status + handoff to human agent
4. Optional canvas supervisor app for real-time floor monitoring

## Phase 4 - Automation (Day 3-4)
Power Automate flows:
1. Intake routing flow (priority/SLA/team routing)
2. Reminder and overdue follow-up flow
3. Resolution notification flow (email)
4. Discount approval flow (`discount > 50%` -> manager)
5. Data retention flow (archive/delete after 28 days)
6. Escalation flow (upset sentiment/keywords -> manager copy)

## Phase 5 - Integration (Day 4)
1. Outbound resolution callback pattern:
   - Trigger on resolved request
   - Publish to queue/webhook
   - Retry with exponential backoff
   - Dead-letter + replay capability
2. Inbound request/event ingestion:
   - Idempotency key to avoid duplicates
   - Integration log table entries for observability

## Phase 6 - Security (Day 5)
Define:
- Security roles: Agent, Manager, Executive Read-Only, Integration Admin, Portal User
- Business Units: Americas, EMEA, APAC, Shared Services
- Teams: Small Deals (owner), Enterprise Pods (access), Escalation
- Entra groups for automatic role assignment

Validate:
- Reception/portal users cannot access sales-sensitive data
- Managers can view team records
- Field-level controls for discount approval and audit

## Phase 7 - Reporting (Day 5)
Power BI dashboards:
- SLA compliance
- Resolution throughput
- Success/failure retention outcomes
- Agent workload and aging buckets
- Executive real-time KPI view

## Phase 8 - ALM and release (Day 6)
1. Store unpacked solutions in source control.
2. Build validation gates:
   - Solution checker
   - Smoke tests
   - Security review
3. Promote managed solutions Dev -> Test/UAT -> Prod.
4. Define rollback package and support runbook.

## Minimum acceptance criteria
- All workbook fit-gap requirements mapped to a feature
- SLA and queue routing working end-to-end
- Portal status and bot interaction operational
- Discount approval enforced and auditable
- Integration retries + dead-letter tested
- Security access matrix signed off
- Deployment pipeline repeatable

## Study checkpoints (PL-600)
- Explain why each requirement is OOB/Configure/Custom/Other
- Justify app type choices per user group
- Defend security and DLP decisions
- Describe integration reliability patterns (retry, idempotency, DLQ)
- Explain ALM layering and environment promotion strategy

## Immediate next step
Start with a **requirements-to-backlog matrix** and map each workbook row to:
- user story
- solution component
- owner
- estimate
- test case
