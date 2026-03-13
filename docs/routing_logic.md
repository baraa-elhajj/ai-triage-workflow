# Routing Logic

## Purpose

The routing component determines which internal team should receive an inbound customer request after the AI classification and enrichment steps. The goal is to ensure that each request is directed to the team best equipped to resolve the issue while minimizing manual triage.

The routing decision is based primarily on the **classification category**, with additional safeguards for **low-confidence predictions** and **high-risk messages**.

---

# Destination Queues

The workflow routes requests to the following internal queues:

| Queue            | Responsibility                                            |
| ---------------- | --------------------------------------------------------- |
| Engineering      | Product bugs, outages, and system failures                |
| Product          | Feature requests and product improvements                 |
| Billing          | Payment issues, invoices, and contract disputes           |
| IT / Security    | Authentication, integrations, and configuration questions |
| Escalation Queue | Low-confidence or high-risk cases requiring human review  |

---

# Category → Queue Mapping

The primary routing rule maps the LLM classification category to the responsible team.

| Classification Category | Destination Queue |
| ----------------------- | ----------------- |
| Bug Report              | Engineering       |
| Feature Request         | Product           |
| Billing Issue           | Billing           |
| Technical Question      | IT / Security     |
| Incident / Outage       | Engineering       |

This mapping reflects common SaaS operational ownership where engineering teams handle bugs and outages, product teams handle roadmap requests, and billing teams manage financial disputes.

---

# Priority Influence

Priority does not change the destination queue but signals urgency for the receiving team.

| Priority | Interpretation                |
| -------- | ----------------------------- |
| High     | Immediate attention required  |
| Medium   | Standard operational priority |
| Low      | Non-urgent request            |

For example, a **high-priority bug report** is still routed to Engineering but should be addressed sooner.

---

# Fallback Routing (Low Confidence)

If the LLM classification confidence score is **below 0.70**, the message is considered uncertain.

In these cases the workflow routes the request to the **Escalation Queue** for human review instead of automatically assigning it to a team.

This prevents misclassification from sending requests to the wrong department.

---

# Escalation Overrides

Certain message patterns trigger escalation regardless of the confidence score:

* messages containing keywords such as **"outage"** or **"down for all users"**
* billing discrepancies greater than **$500**
* ambiguous messages that reference multiple issue types

These requests are routed to the **Escalation Queue**, where a human operator can review and manually assign them.

---

# Final Routing Process

The routing workflow follows this decision order:

1. Receive classification results from the AI model
2. Check for escalation conditions
3. If escalation triggered → route to Escalation Queue
4. Otherwise check classification confidence
5. If confidence < 0.70 → route to Escalation Queue
6. Otherwise apply the Category → Queue mapping
7. Deliver structured record to the destination queue
