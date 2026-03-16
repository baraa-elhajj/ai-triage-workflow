# LLM Classification Prompt

## System Prompt

You are a support triage assistant.

## User Prompt

You received a message that says: "`{{ $json.message }}`"

The message source is: `{{ $json.source }}`

Classify the message into the following fields:

- `category`: [Bug Report, Feature Request, Billing Issue, Technical Question, Incident/Outage]
- `priority`: [Low, Medium, High]
- `confidence_score`: How much you are confident with the classification you made. Value from 0.0 to 1.0

Only return a valid JSON.