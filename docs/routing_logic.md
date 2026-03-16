# Routing Logic

Routing decisions are based on classification results from the AI agent.

## Category Routing

| Category | Destination |
| ---------| ------------|
| Feature Request | Product |
| Billing Issue | Billing |
| Technical Question | IT/Security |
| Incident/Outage | Engineering |
| Bug Report | Engineering |

## Escalation Rules

Requests are escalated when any of the following occurs:

1. **Low Confidence Classification:** The AI agent's confidence in the classifcation he made.<br>
`confidence_score < 0.70`

2. **Critical Keywords:** The support message contains one or more of the following terms:
    - outage
    - down for all users
    - billing error > $500

3. **Escalation Destination:** Escalated requests are sent to an external webhook endpoint for manual review.

4. **Escalation Metadata:** The workflow records:
    - `escalation_flag`
    - `escalation_reason`

   This provides transparency for operational teams reviewing escalated cases.
