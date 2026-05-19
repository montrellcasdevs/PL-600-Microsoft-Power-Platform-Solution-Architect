# Exercise 11 - PVA architecture

## What this exercise is testing

This exercise tests whether you can recognize when a chatbot is the right tool, when search or knowledge capabilities are more important, and how bot, portal, and live-agent capabilities should work together.

## Scenario 1 - Product and pricing

### Analysis

The requirements focus on helping internal sales users find product combinations and pricing rules that vary by country. This is knowledge discovery and guided assistance, not necessarily a standalone chat problem.

### Recommended solution direction

- Use Copilot or chatbot capabilities only if conversational guidance adds value.
- Back the experience with a structured knowledge source for products, compatible combinations, and country-specific pricing rules.
- Integrate with the sales experience so users do not have to leave their workflow.

### Architect point of view

If the information is complex and rule-driven, the primary challenge is governing the knowledge source. The bot is only the access layer.

## Scenario 2 - Customer service

### Analysis

This is a stronger chatbot scenario because the requirements explicitly include self-service, search, FAQ handling, and handoff to a human agent.

### Recommended solution direction

- Use Power Pages or the existing web experience as the customer front door.
- Use Copilot Studio for bot-driven conversations.
- Integrate with Dynamics 365 Customer Service so the bot can retrieve ticket status and latest actions.
- Integrate SharePoint knowledge content for search and answer generation where appropriate.
- Enable escalation to a live agent with transcript handoff.

### What the bot should handle

- request status questions
- common troubleshooting
- article discovery
- basic intake before human transfer

### What should not be bot-only

- complex or emotionally sensitive cases
- cases that require secure verification beyond the configured journey
- high-risk support decisions

## Strong architect answer

"For product and pricing, I would not start by assuming the chatbot is the whole answer. I would first establish a trustworthy knowledge source for product combinations and country-specific pricing rules, then decide whether conversational access improves usability for sales users. For customer service, Copilot Studio is a strong fit when combined with Dynamics 365 Customer Service, Power Pages, and SharePoint knowledge. The design should allow customers to search, get bot help, retrieve ticket status and latest actions, and escalate to a human agent with the conversation context preserved."