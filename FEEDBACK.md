# Client review: Larkspur disruption-care agent

**To:** larkspur-exercise  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-19 05:58

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. agent.py line 1 starts with a U+FEFF byte, and your diff adds it; the static scan says the file does not parse.**

The diff changes the first line of agent.py from the docstring opener to the same line prefixed with a byte order mark. The scan reports "invalid non-printable character U+FEFF", finds no functions, no while loop and zero tool schemas. Python can strip a BOM when it reads a file from disk, so run.py may behave differently from the scan, but this review cannot see a run that proves either way.

Run python3 run.py K7PQ2M --trace and paste the first 20 lines of output, so it is clear whether agent.py loads.

**2. PITCH.md claims 21,536 input tokens per resolved contact, 107,680 over 5 ticket types, and no run or bench output is in the repository.**

There is no readout-trace.json, and the Number line is a single run per ticket type ("1 run each"). 107,680 divided by 5 is 21,536, so it is an average over all five tickets, and nothing says how many of the five resolved. Your eval cases name PNRs K7PQ2M, R8KD3F, F7GK2D, M3XR8T and E2SX5G, but nothing ties the five token totals to those tickets.

Run python3 run.py --all --trace and paste the totals footer.

**3. PITCH.md reports 5 eval cases with 4 passing, but evals/cases.json has 3 hard gates and PITCH.md says tone-0101 fails.**

If tone-0101 is the one failure it is a hard gate, so the release is blocked at 80%, which your own Still broken line says. Four of the five cases have author "<your name>" or are placeholders in the same file: grnd-0101, irrv-0101 and ref-0101 still carry "<your name>" as author, so only tushar's two cases are attributed. Those three are the shipped examples, so the 4 of 5 is mostly the workshop's cases, not yours.

Run python3 eval_harness.py and paste the per-case lines and the pass-rate footer.

**4. TONE_ADDENDUM in agent.py is 0 characters, and tone-0101 expects escalate_to_human on abuse plus a legal threat.**

The only text steering tone is SYSTEM_PROMPT from support, and your diff does not touch it. A bigger model gets the same empty addendum and the same tool list, so it would face the same instruction gap on R8KD3F. PITCH.md names this as Next, which means the fix is a prompt edit you have not made yet, and that prompt edit is what Priya's question has to be weighed against.

Run python3 bench.py --label before --stage 1 --runs 3 and paste the tone-0101 pass count across the 3 runs.

**5. Your seats_left and departures_in_window executors read flights.csv through load_flights() with no test, and PITCH.md reports no trace in which either was.**

Both functions are in LOCAL_TOOLS and both descriptions are long, with example phrases such as 'is there room on that flight for the three of us?'. None of the 5 eval cases asks a seat-count or departure-window question, so the tool-selection claim in those descriptions has nothing measuring it. Each added schema also rides on every turn through tool_list(), which is an input-token cost counted in your 21,536 whether or not the tool is used.

Run python3 run.py --tool-tax and paste the per-tool token cost for seats_left and departures_in_window.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (338 lines)`
- `PITCH.md`
- `TEAM.md`
- `evals/cases.json`
- given files that differ from the shipped pack: `verify.py`, `eval_harness.py`, `bench.py`, `readout.py`, `setup.py`, `pod_sync.py`, `run.py`, `review.py`, `support/__init__.py`, `support/client.py`, `support/data.py`, `support/models.py`, `support/tools.py`, `support/trace.py`, `support/offline.py`, `support/mock_backend.py`, `support/mcp_client.py`, `support/mcp_server.py`, `support/mcp_selftest.py`, `support/access.py`, `support/keyscan.py`, `support/review.py`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
