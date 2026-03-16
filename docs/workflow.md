# Workflow Explanation

This document explains each step (node) of the AI support triage workflow.

## 1. Webhook Trigger

The workflow begins with a webhook endpoint: `POST http://localhost:5678/webhook-test/support-intake`

This endpoint receives support requests as JSON payloads.

Example request format:
```json
{ 
    "id": "123", 
    "source": "email", 
    "message": "Our dashboard stopped loading for all users." 
}
```
Incoming payloads are passed to the next stage for processing.


## 2. Request Body Extraction

The webhook request contains metadata along with the request body. A normalization step extracts only the body content to ensure a consistent
input format for the AI agents.


## 3. AI Classification Agent

The first AI agent classifies the request using an LLM accessed through **OpenRouter**.

Generated fields:
- category
- priority
- confidence_score

Supported categories:
- Bug Report
- Feature Request
- Billing Issue
- Technical Question
- Incident/Outage


## 4. Classification Parsing

AI responses are parsed into structured JSON. This removes markdown formatting sometimes returned by LLMs and validates the JSON structure.


## 5. AI Enrichment Agent

The enrichment agent extracts additional structured information from the message.

Generated fields:
- core_issue
- identifiers
- urgency_signal


## 6. Routing Logic

The routing engine determines which internal team should receive the request based on the classification result and escalation conditions.


## 7. AI Summary Agent

A final AI agent generates a concise summary to help internal teams quickly understand the request context.


## 8. Escalation Check

Requests that meet escalation criteria are routed to an escalation webhook.
Used **Webhoo.site** to generate a webhook that listens to upcoming escalated requests.

All other requests are stored in the processed requests log.


## 9. Storing Processed Requests

Processed requests are stored in Google Sheets providing a persistent audit trail.
All the JSON response fields are automatically mapped to the Google Sheets file.
