# {NNNN} — {The decision, as a short noun phrase}

- **Status:** {Proposed | Accepted | Superseded by {NNNN}}
- **Date:** {YYYY-MM-DD}
- **Deciders:** {names or roles}
- **Scope:** {single team | single product | whole estate}
- **Reversibility:** {easily reversible | costly to reverse | effectively irreversible}
- **Confidence:** {low | medium | high} — {the rule that produced it, in plain words}

> **Write this for someone who was not in the room** and who may disagree with it. They
> should be able to tell exactly what they are disagreeing with. No product names, no
> framework vocabulary, no acronym the business does not already use.

## Context

{What forces this decision now. What is true today, what is changing, and what happens if
nothing is chosen. Enough that the decision reads as reasonable to a stranger — without
requiring them to agree with it.}

{Name the constraints that are genuinely fixed, and mark any that were assumed rather than
confirmed.}

## Decision drivers

{The two or three things this is being optimized for, in priority order. If the drivers
were not agreed before the options were compared, say so — that is a finding.}

## Options considered

| Option | What it means in practice |
|---|---|
| {opt-1} | {one line a non-specialist can picture} |
| {opt-2} | {…} |
| {opt-3} | {…} |

*Three is the working practice. **If only two are listed, state here why a third was not
available** — "no third approach exists that satisfies the retention constraint" is a
legitimate and useful sentence.*

*If deferring was available, it belongs in this table as an option.*

*If only one option existed, this is a **rationale record**, not a decision. Say so in the
status line, record why the alternatives were not viable, and do not invent alternatives
to fill the table.*

## Options eliminated by constraint

| Option | Eliminated by | What the constraint says |
|---|---|---|
| {opt-n} | {policy_id} | {the constraint as the organization states it} |

*State "No option was eliminated by constraint" explicitly if none was.*

## Decision

**{One sentence, active voice: "We will hold order state in the intake service until
fulfilment acknowledges it."}**

{What is in scope of this decision, and what was deliberately left open.}

## Why

{The two or three things that decided it, as reasons rather than scores. "The broker is
already in place and both other options would have added a second integration style to an
estate that has too many" — not "estate_fit scored 4".}

{The full arithmetic is in the option comparison for anyone who wants it.}

## Consequences

**What this commits us to:** {effort, skills, licences, operational load}

**What this closes off:** {options that become expensive or impossible after this. Be
specific — this is the section a future reader will care about most.}

**What we accept:** {the known downside. Every option had one. Recording it here is what
stops this decision being relitigated from scratch the first time it shows up.}

## Standards position

{One of:}

- **Follows** {standard or precedent}.
- **Deviates** from {standard}, because {the argument}. {What would have to be true for us to come back into line, and whether a waiver is needed.}
- **Sets a new precedent**, because nothing covered this. {Whether this should become a standard, and who would own it.}

## What we assumed

| # | Assumption | Why we had to assume it | What it affects |
|---|---|---|---|
| A1 | {…} | {the input that was not available} | {what changes if it is wrong} |

## How confident this is

**{low | medium | high}** — {the rule that produced this rating}.

{Be specific about what would raise it: "a two-day spike on option 2's throughput would
move this to high" is useful. "More information" is not.}

**If the recommended option were unavailable**, the decision falls to {option}, which is
{nearly as good / materially worse}. {If nearly as good, this decision matters less than
it appears. If materially worse, it is load-bearing and deserves the scrutiny.}

## What would make us revisit this

{Observable events, not sentiments:}

- {"If peak intake passes {N} messages an hour."}
- {"If the {supplier-agnostic capability} is retired or its support position changes."}
- {"At the next review of {standard}, currently {date}."}

## Related and superseded decisions

- **Supersedes:** {NNNN — title}. *That record is marked superseded and left otherwise unchanged.*
- **Superseded by:** {NNNN, once that happens}
- **Depends on:** {NNNN}
- **Conflicts with:** {NNNN — and what is being done about it}

> **Never edit a superseded record.** Mark it and link it. The reasoning trail is the
> entire value of a decision log, and editing it away is how a settled argument gets
> reopened from scratch two years later.
