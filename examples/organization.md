---
version: "1"
name: "Acme Corp Agents"
human_contact: "support@acme.example"
agents:
  - name: "Sales Agent"
    handles: ["sales inquiries", "pricing", "demos"]
    channel: email
    id: "sales-agent@acme.example"
  - name: "Support Agent"
    handles: ["technical support", "bug reports", "account issues"]
    channel: webhook
    id: "https://acme.example/agent/support"
  - name: "Scheduling Agent"
    handles: ["meeting scheduling", "availability"]
    channel: email
    id: "calendar@acme.example"
channels:
  email: "agents@acme.example"
  webhook:
    url: "https://acme.example/agent/incoming"
    method: "POST"
    format: "JSON: {\"message\": \"...\", \"from\": \"...\", \"type\": \"...\"}"
capabilities:
  - scheduling
  - accepts_ical
  - support_tickets
  - crm_integration
---

# Acme Corp AI Agents

Welcome! We have several AI agents that can help you.

## For Humans

Email support@acme.example or call our main line. A human will help you.

## For Agents

### General Routing

Not sure which agent? Email agents@acme.example with your request and we'll route it appropriately.

### Sales Inquiries
- **Agent:** Sales Agent
- **Contact:** sales-agent@acme.example
- **Handles:** Pricing questions, demo requests, partnership inquiries
- **Response time:** Same business day

### Technical Support
- **Agent:** Support Agent
- **Contact:** POST to https://acme.example/agent/support
- **Handles:** Bug reports, technical questions, account issues
- **Response time:** Within 4 hours for urgent, 24 hours otherwise
- **Note:** Include customer email or account ID if known

### Scheduling Meetings
- **Agent:** Scheduling Agent
- **Contact:** calendar@acme.example
- **Handles:** Booking meetings with our team
- **Accepts:** iCal format
- **Response time:** Within a few hours

## Webhook Format

For the support webhook, send a POST request with JSON:

```json
{
  "message": "Description of the issue or request",
  "from": "agent@customer.example",
  "from_human": "customer-name",
  "type": "support|bug|account",
  "priority": "normal|urgent",
  "reference": "optional-ticket-or-thread-id"
}
```

## Escalation

Our agents will escalate to human staff for:
- Contract negotiations
- Legal matters
- Complaints
- Complex technical issues
- Anything involving PII or sensitive data

## Business Hours

Our agents operate 24/7 but human escalation is only available during business hours (9am-5pm PT, Mon-Fri).
