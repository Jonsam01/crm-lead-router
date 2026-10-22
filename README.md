# CRM Lead Router

n8n workflows that score scraped leads from a Google Sheet, push Hot leads to HubSpot, and alert on Telegram.

## Workflows
- crm-lead-router.json: live router (Google Sheets trigger, scoring Code node, HubSpot upsert, Telegram alert, dead-letter sheet)
- error-handler.json: Error Trigger workflow that sends a crash alert to Telegram
- daily-digest.json: scheduled 24-hour summary to Telegram
- backfill.json: manual workflow that processes existing leads 25 at a time

## Design
- Idempotent: a Status column (Scored, Pushed, Failed) means reruns skip finished leads
- Validation gate and email gate: no valid email means a lead can never be Hot
- HubSpot upsert on email: no duplicate contacts
- Failed pushes are logged to a Failed Leads sheet with the error text
- Scoring tiers and thresholds live in one Config node

## Setup
Import each JSON into n8n, attach your own Google Sheets, HubSpot, and Telegram credentials, and point the sheet nodes at your leads tab.
