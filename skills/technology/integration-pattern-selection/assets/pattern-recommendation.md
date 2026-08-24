# {Source system} to {target system} — integration pattern

**Purpose:** {the business event or need this serves}
**Date:** {YYYY-MM-DD} · **Author:** {name}
**Confidence:** {low | medium | high} — {the rule that produced it}

## The integration

| | |
|---|---|
| **Sends** | {system} |
| **Receives** | {system} |
| **Carries** | {what data, whole record or changes only} |
| **Volume** | {rate} — **peak {rate}** |
| **Payload** | typical {size}, maximum {size} |
| **Caller** | {waits \| continues \| nothing is waiting} |
| **Latency requirement** | {number and percentile, or "not quantified — see finding below"} |
| **Delivery guarantee needed** | {best effort \| no loss \| no loss, no duplicates} |
| **Ordering** | {required within {grouping} \| not required} |
| **Consumers** | {one \| several known \| unknown and growing} |
| **Replay** | {never \| occasionally \| routinely} |
| **Crosses to another organization** | {no \| one partner \| many partners} |
| **Data classification** | {…} |

*Where "real time" could not be quantified, say so here rather than substituting a number.
It is a finding, and it is cheaper to surface now than in testing.*

## Recommended pattern

**{pattern}**

{One paragraph a delivery team can act on: what gets built, roughly, and what the shape is.}

{Where the recommendation is a deliberate combination — brokered events with a file-based
backfill, for example — say so explicitly and state that it is a combination rather than
an unresolved choice between two patterns.}

{Where the top two are inside the indifference band, say that instead: which two, why they
cannot be separated on this evidence, and the one measurement that would separate them.}

## Why

{The two or three characteristics that actually decided it, as reasons rather than scores.
"The warehouse system cannot be relied on to be up during the overnight window, and the
order must not be lost, so the sender must be able to hand over and walk away" — not
"coupling_and_resilience scored 4".}

{The full arithmetic is in the pattern comparison for anyone who wants it.}

## Patterns eliminated, and by what

| Pattern | Eliminated by | Why |
|---|---|---|
| {pattern} | {the timing answer \| policy_id} | {…} |

*Include the patterns removed by the response-timing answer before scoring, not only those
removed by policy. State "None" explicitly if nothing was eliminated. Options that quietly
disappear read as an analysis that was steered toward its conclusion.*

## What happens when it fails

**Mandatory section.**

| Failure | What the sender does | Where the data waits | For how long | Who finds out |
|---|---|---|---|---|
| Receiver unavailable | {…} | {…} | {…} | {…} |
| Message rejected as invalid | {…} | {…} | {…} | {…} |
| Backlog building faster than it drains | {…} | {…} | {…} | {…} |

{An integration design that documents only the happy path has documented the path that
never causes an incident.}

## Delivery guarantees this provides

| | The pattern provides | The receiver must handle |
|---|---|---|
| Loss | {…} | {…} |
| Duplication | {…} | {at-least-once delivery means the receiver must be idempotent} |
| Ordering | {…} | {…} |
| Replay | {…} | {…} |

*No pattern gives you everything. Naming what the receiver must handle itself is cheaper
here than in an incident review.*

## What it costs to build and run

{Build effort, the infrastructure it needs, and — separately — what it costs to operate
and who operates it. Where the pattern needs capability the organization does not have
today, say what would have to be built and by whom.}

## What we assumed

| # | Assumption | Why we had to assume it | What it affects |
|---|---|---|---|
| A1 | {…} | {the input that was not available} | {…} |

## How confident this is

**{low | medium | high}** — {the rule that produced this rating}.

{What would raise it, specifically. "A measured peak-hour message count would move this to
high" is useful; "more data" is not.}

## What would change this answer

- "At {N}× the stated peak, {the part that gives way} becomes the constraint and the pattern would change to {…}."
- "Adding a second consumer costs {…} under this pattern. If that is expected within a year, {alternative} is the better choice now."
- "If the maximum payload is {N}× larger than stated, the design shifts to passing a reference rather than the data."
- "If the latency requirement is actually {stricter figure}, {…}."

## Deliberately not decided here

{The interface contract, field names, schemas, error codes. Which product implements the
pattern. The architecture of either system. Whether the two systems should be integrated at
all.}
