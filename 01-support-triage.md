# Support Ticket Triage Agent

**Status:** working demo, tested on invented sample tickets. No client data, no client results yet.

## The problem
Support queues mix routine questions with urgent ones: duplicate charges, login outages, possible account takeovers, and threats of legal action or chargebacks. Routine tickets wait while urgent ones get the same first-come treatment.

## What the agent does
1. Reads each ticket (subject and body).
2. Assigns one category: billing, outage, security, bug, how-to, or general.
3. Sets priority (high, medium, low) from category and urgency wording.
4. Flags tickets for a human when they mention legal action, a breach, unauthorized access, or a chargeback.
5. Drafts a reply for a person to approve. It never sends anything.

## Sample result
Eight invented tickets produced:
- 2 escalations: an unauthorized-login report, and a customer threatening a lawyer and a chargeback.
- 3 high priority, 2 medium, 3 low.

## What it does not do
- It uses keyword rules, not a language model. Unusual wording can be missed or misfiled.
- It does not read attachments or check order history.
- It does not send replies or change ticket status.

## Build it for a client
1. Export 200 to 500 real tickets, anonymized, from their helpdesk.
2. Tune the category rules on that set and record the miss rate.
3. Connect it to their helpdesk as a draft-only step, with a human approving each reply.
4. Measure: time to first response for high-priority tickets, and misfiled rate.

## Code
`demo-agents/support_triage/triage.py`, with `sample_tickets.json` and `sample_report.json`.
