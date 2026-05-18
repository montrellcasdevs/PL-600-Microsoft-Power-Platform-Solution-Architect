# PL-600 Requirements to Backlog Matrix

Source requirements: [Instructions/Exercises/Exercise02[PL-600]_Conceptualize_Design.md](Exercise02%5BPL-600%5D_Conceptualize_Design.md)

| Req ID | Requirement summary | Component(s) | Priority | Estimate | Test focus |
|---|---|---|---|---|---|
| 1 | Route help requests by service level + incident type | Customer Service queues, unified routing, assignment rules | High | M | Correct route for each scenario |
| 2 | Staff can see list of open requests and pick qualified work | Model-driven views, queue filtering, skill tags | High | S | Only qualified requests shown |
| 3 | Customer can open request from web interactive chat | Power Pages + Copilot Studio + Dataverse case create | High | M | Bot creates case with transcript |
| 4 | Staff can search knowledge base and send articles | Knowledge articles, relevance search, email template | High | S | Article send in 2 clicks |
| 5 | Process nightly manufacturer feed for customer/bed config | Dataflow/ETL flow, staging table, upsert logic | High | L | Feed imports without duplicates |
| 6 | Staff can schedule onsite technician | Field Service work order + booking | High | M | Booking generated from case |
| 7 | Staff can see proactive maintenance candidates | Predictive/wear rules + list view + outreach flow | Medium | M | Candidate list reflects thresholds |
| 8 | Field tech sees next visit, details, directions | Field Service mobile, map integration | High | M | Tech receives next assignment data |
| 9 | Staff can sell support agreement | Sales process, quote/order, agreement table | High | M | Agreement created and linked |
| 10 | Customer receives close email + feedback request | Resolution-triggered cloud flow + survey link | High | S | Email sent on close status |
| 11 | Manager sees requests outside SLA | SLA KPI + escalation dashboard | High | S | SLA breaches visible real-time |
| 12 | Customer sees request status on website | Power Pages authenticated status page | High | M | Correct owner-only visibility |
| 13 | Manager receives upset customer comms copy | Sentiment/keyword routing flow + manager notify | Medium | M | Escalation fired on threshold |
| 14 | Staff sees remaining SLA time | SLA timer control/PCF and KPI fields | High | S | Timer accuracy vs KPI timestamps |
| 15 | Track opened date, days open, resolved | Dataverse columns + calculated fields + BI | High | S | Aging and closure metrics correct |
| 16 | Used-bed ownership/support transfer | Ownership transfer process + validation flow | Medium | M | Transfer updates rights correctly |
| 17 | Acceptable response time globally | Performance design, async patterns, indexing | High | M | Page load targets met in regions |
| 18 | Executive real-time support metrics | Power BI near real-time dashboard | High | M | Executive KPI dashboard updated |

## Suggested delivery order
1. Req 1,2,4,10,11,14,15 (core service operations)
2. Req 3,12,13 (customer experience)
3. Req 5,6,8,9,16 (integration + field/sales complexity)
4. Req 7,17,18 (optimization + executive analytics)

## Definition of Done (per requirement)
- User story accepted by business owner
- Security validated (least privilege)
- Automated flow monitored with failure alerts
- Regression test updated
- Included in managed solution release notes
