# Value stream map — {stream name}

**Trigger:** {what starts it} · **Recipient:** {who ends up holding value}
**Value delivered:** {…}
**Boundary:** starts at {…}, ends at {…} — {agreed | **contested** | not discussed}
**Coverage:** {happy path | includes exceptions | exceptions only}
**Timing basis:** {measured from systems | observed walkthrough | **asked the teams** | **none**}
**Confidence:** {low | medium | high} — {reason}

## How much of the time is value-adding

| | Time |
|---|---|
| Total elapsed, end to end | {…} |
| Of which work time | {…} |
| Of which wait time | {…} |
| **Value-adding share** | **{…}%** |

*In most unmeasured streams this is under ten per cent. The number reframes the conversation
faster than any individual stage finding — lead with it.*

## The stages

| # | Stage | Value item | Performed by | Work | **Wait** | Rework | Systems | Capabilities | Status | Driven by |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | {…} | {what the recipient has that they did not before — or **none stated**} | {…} | {…} | {…} | {…} | {…} | {…} | {flows \| queue_bound \| rework_bound \| handoff_bound \| no_stated_value \| insufficient_evidence} | {…} |

*Work and wait are separate columns, always. A single duration per stage conceals the queue,
and the queue is usually the answer.*

## The constraint

**{Stage}** — {why it is the bottleneck, and what the end-to-end time would be without it}.

> Improving any stage other than the constraint changes end-to-end elapsed time by nothing.
> This is where improvement effort should go, and it is frequently not where it is going.

## Stages nobody could name the value of

| Stage | What it was for | Who would have to agree to stop it |
|---|---|---|
| {…} | {often an internal arrangement that no longer exists} | {…} |

*Reported, not optimised. Making an unnecessary stage faster is the most expensive kind of
improvement.*

## Where the documented process and the actual one differ

| Stage | The procedure says | What people actually do | Why |
|---|---|---|---|
| {…} | {…} | {…} | {usually a rational workaround for something upstream} |

## Eliminated by constraint

| Change considered | Blocked by | Effect |
|---|---|---|
| {e.g. merging two stages} | {segregation_of_duties} | {removed from consideration, not scored down} |

## Assumptions

| # | Assumption | Source | Affects | Penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {stages affected} | {low \| medium \| high} |
