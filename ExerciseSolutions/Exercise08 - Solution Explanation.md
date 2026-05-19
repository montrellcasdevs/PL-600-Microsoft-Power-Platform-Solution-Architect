# Exercise 08 - Security model

## What this exercise is testing

This exercise tests whether you can design security as a combination of identity, environment governance, app access, Dataverse privileges, team-based visibility, and external-user controls.

## How to analyze it

Split the problem into five layers:

1. Environment and connector governance
2. App access
3. Dataverse roles and business units
4. Record-sharing model
5. External portal access

## 1. Calm the IT security concerns

The requirement about rogue connectors is mainly a governance problem.

Recommended response:

- Define DLP policies separating business connectors from blocked or non-business connectors.
- Restrict who can create flows in the relevant environments.
- Use managed environments and admin monitoring where available.
- Separate dev and production usage appropriately.

This shows the security team that the risk is being controlled at the platform level, not just by user training.

## 2. Ensure only managers approve discounts

Use multiple controls, not one.

- Security roles: only managers can update approval fields.
- Form logic or command visibility: sales staff cannot self-approve.
- Power Automate approval or business logic: ensure approver is a manager and not the requesting seller.
- Audit: track approver, timestamp, and previous values.

## 3. Control access to apps

- Sales Central model-driven app: share with sales staff and managers only.
- Reception canvas app: share only with reception users.
- Power Pages portal: expose only the required external functionality.

App access is necessary but not sufficient. Dataverse security must also prevent unauthorized data access.

## 4. Accommodate per-app licensing for reception staff

Reception staff should only be granted access to the specific app and required underlying tables. Keep their scope minimal so licensing and data exposure stay aligned.

## 5. Recommended Dataverse roles

- Sales Representative
- Sales Manager
- Reception Staff
- System Administrator or Support Admin
- Portal User web role mapping for external users

You may also need app-specific or process-specific roles if approval and administration duties are separated.

## 6. Business-unit design

A reasonable starting point based on the organization is:

- Root organization
- Sales
- Sales - Small Deals
- Sales - Large Deals
- Wholesale
- Marketing
- Operations
- Manufacturing
- Showroom
- Shipping
- Customer Service

Do not overcomplicate the hierarchy, but use it to reflect visibility boundaries that actually matter.

## 7. Portal users seeing only their own records

Use Power Pages table permissions tied to the authenticated contact. The guiding principle is contact-scoped access so a portal user can only see their own visit requests and related records.

## 8. Small deals versus large deals visibility

This is the key record-access design problem.

Recommended approach:

- Small deals: use owner teams or business-unit visibility so the group can work from the same pool.
- Large deals: default to user-owned records for privacy and competitive behavior.
- Very large deal teams: grant access through access teams or team ownership when collaboration is needed.

## A strong solution-architect response

"I would address security at both platform and data level. DLP policies and environment governance control rogue connectors. App sharing controls entry points, while Dataverse roles, business units, owner teams, and access teams control data visibility. Reception users would have tightly scoped per-app access with no sales-data privileges. Discount approval would be enforced through role design plus business logic and audit. Portal users would be restricted with contact-based table permissions so they can only see their own records."