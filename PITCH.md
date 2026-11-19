# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A Larkspur disruption-care agent on the Claude Messages API with nine local tools plus next_available_day and fare_rules served over MCP, with seats_left and departures_in_window added locally.
Does: Looks up a booking, reads flight status and policy, then offers rebooking options and holds a seat, leaving the final confirm-click to the customer.
Number: 21,536 input tokens per resolved contact (107,680 across 5 ticket types, 1 run each).
Safety check: 5 eval cases, 4 pass (80%); the agent refuses to confirm a rebooking on a chat message and does not accept a flight number that does not exist.
Next: Author a TONE_ADDENDUM so abusive or legal-threat messages escalate to a human.
Still broken: nothing watches tone, so tone-0101 (abuse plus a legal threat) calls issue_voucher and never escalates, which blocks the release.
Lever: intelligence

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
