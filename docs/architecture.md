# System Architecture

## Overview

The ArcVault AI Triage Workflow automatically processes incoming support requests and routes them to the appropriate internal team. The system combines automation with AI agents to interpret unstructured messages and produce structured operational data.


## Design Principles

The workflow convers the following principles:

1. **Event‑Driven Intake:** Requests enter the system through a webhook endpoint exposed by n8n.

2. **AI Augmentation:** LLM agents provide semantic understanding of support messages enabling: 
    - classification 
    - entity extraction 
    - contextual summaries

3. **Deterministic Routing:** Routing decisions are made using deterministic logic based on AI outputs.

4. **Observability:** Each processed request is stored with: 
    - classification results 
    - extracted entities 
    - routing decision 
    - AI summary

    This enables monitoring and auditing of AI decisions.

5. **Human‑in‑the‑Loop Escalation:** Low‑confidence or high‑impact requests are escalated for manual review.
