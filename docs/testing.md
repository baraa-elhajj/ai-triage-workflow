# Testing the Workflow

## Starting the Workflow

1. Install and start n8n locally:
    ```bash
    npm install n8n
    npx n8n
    ```

2. Activate the workflow to enable the webhook endpoint.

## Sending Test Requests

Requests can be sent using Postman or CURL.

Webhook endpoint: 
```POST http://localhost:5678/webhook-test/support-intake```

Check this [postman collection](../testing/ArcVault_Triage_Workflow.postman_collection.json) with several support request samples that can be imported and tested easily.

## Observing Results

Depending on the routing decision:

- Normal requests → stored in Google Sheets
- Escalated requests → forwarded to webhook.site endpoint.
