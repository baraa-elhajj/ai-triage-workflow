# ArcVault AI Support Triage Workflow

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
| [architecture.md](/docs/architecture.md)   | System architecture overview |
| [workflow.md](/docs/workflow.md)       | Detailed workflow explanation|
| [routing_logic.md](/docs/routing_logic.md)  | Routing and escalation rules |
| [testing.md](/docs/testing.md)        | How to test the workflow     |
