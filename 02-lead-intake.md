# Lead Intake and Scoring Agent

**Status:** working demo, tested on invented sample leads. No client data, no client results yet.

## The problem
Inbound leads arrive as messy web-form text. Someone has to read each one, check that the contact details are usable, guess how serious the buyer is, and write a first reply. Hot leads wait behind tire-kickers, and incomplete forms get lost.

## What the agent does
1. Checks each lead for name, email, and message, and validates the email format. Incomplete leads are held for follow-up.
2. Scores each lead on four signals:
   - a dollar budget mentioned in the message (largest amount wins);
   - a request for automation, AI, or integration work;
   - urgent timing (with "nothing urgent" correctly ignored);
   - a business email domain rather than a free mail provider.
3. Tiers each lead hot, warm, or cold, and lists the reasons.
4. Writes a CRM-ready CSV with a follow-up draft per lead. It never sends.

## Sample result
Five invented leads produced:
- 2 hot (a dental office with a $3,000 budget and an urgent start; a logistics firm at $8,000 ASAP).
- 1 warm (a $800 invoice-automation request).
- 1 cold (a general chatbot question marked not urgent).
- 1 held (invalid email, no usable contact).

A false positive was found during testing ("nothing urgent" was scored as urgent) and fixed.

## What it does not do
- It uses keyword rules, not a language model. A budget written as words ("three grand") is missed.
- It does not check whether the company exists or verify the budget.
- It does not send emails or write to a CRM.

## Build it for a client
1. Pull 100 to 300 real past leads, with the outcome of each (replied, booked, closed).
2. Check the hot tier against outcomes and adjust the weights.
3. Connect the form or inbox, and push the CSV or CRM rows as a draft queue.
4. Measure: time to first reply for hot leads, and the share of hot leads that book a call.

## Code
`demo-agents/lead_intake/intake.py`, with `sample_leads.json` and `sample_out.csv`.
