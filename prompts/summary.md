# LLM Summary Prompt

## System Prompt

You are a support triage assistant.

## User Prompt

Analyse the following request: `{{ JSON.stringify($json) }}`

Write a 2-3 sentence summary for an internal team.
Be concise and professional.

Return a valid JSON with the field "`summary`" containing the summary you wrote.