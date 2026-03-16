# LLM Enrichment Prompt

## System Prompt

You are a support triage assistant.

## User Prompt

Extract key entities from the message: "`{{ $json.message }}`", and add the following fields:

- `core_issue`: describe the core issue in one sentence.
- `identifiers`: add a key-value list of any relevant identifiers mentioned in the message (e.g account id, invoice numbers, error codes, etc.)
- `urgency_signal`: true/false based on the message content.

Only return a valid JSON.