# AI Support Triage Workflow

This project implements an AI-powered support request triage pipeline
using **n8n**. Incoming requests are automatically classified, enriched
with additional context, summarized, and routed to the appropriate
internal team.

The system demonstrates how **LLM-powered agents** can automate support
intake workflows while preserving auditability and escalation paths.

## Key Features

-   Webhook-based request ingestion
-   AI-powered classification of support requests
-   Context enrichment and entity extraction
-   Intelligent routing logic
-   Automatic escalation handling
-   Structured logging of processed requests
-   Integration with external systems

## Technology Stack

| Component | Technology |
| --------- | ---------- |
| Workflow Engine | n8n |
| AI Model Access | OpenRouter |
| Storage | Google Sheets |
| Escalation Webhook | Webhook.site |
| Testing | Postman |

## Documentation

Detailed documentation is available below:

| File              | Description                  |
| ----------------- | ---------------------------- |
| [Architecture](/docs/architecture.md)   | System architecture overview |
| [Workflow](/docs/workflow.md)       | Detailed workflow explanation|
| [Routing Logic](/docs/routing_logic.md)  | Routing and escalation rules |
| [Testing](/docs/testing.md)        | How to test the workflow     |


## Production Scale

To improve the following at production scale, we can:
- Introduce a message queue like AWS SQS between webhook ingestion and processing to prevent data loss, enable retries, and support DLQ for failed requests.
- Reduce LLM usage by adding rule-based pre-filters and caching for repetitive requests, and use smaller models for simple tasks like classification.
- Run independent AI steps (e.g., enrichment and summarization) in parallel and move processing to async background workers so the webhook can respond immediately.

## Feature Ideas

- Build a dashboard for reviewing escalated requests. This interface would allow support teams to inspect AI decisions, adjust routing, and provide feedback to improve the system.
- Instead of sending escalations to a webhook, we could configure the system to integrate with ticketing platforms like Jira to automatically create and assign tickets to the appropriate team.
