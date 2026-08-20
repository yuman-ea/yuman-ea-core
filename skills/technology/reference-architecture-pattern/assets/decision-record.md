# {NNNN} — {Pattern name}: {status}

- **Status:** {Proposed | Accepted | Superseded by {NNNN}}
- **Date:** {YYYY-MM-DD}
- **Deciders:** {names or roles}
- **Pattern status set to:** {mandated | recommended | proposed | not_yet_a_pattern}
- **Confidence:** {low | medium | high}
- **Method:** yea.technology.reference-architecture-pattern {version}

> This records the decision **about the pattern** — whether to publish it and with what
> authority. It is not the pattern. Keep it in the organization's decision log; the pattern
> definition lives wherever patterns live.

## Status

{Proposed | Accepted | Superseded by ADR-NNNN}

## Context

{What prompted the question. Who proposed the pattern and why now — a recurring problem, a
solution somebody wants to generalize, an external practice under consideration.}

{How many implementations existed at the time of the decision, and what they were. This is
the fact a future reader will most want, because it is the one that will have changed.}

## Decision

{One sentence, active voice: "We will publish X as a recommended pattern for Y, owned by Z."}

{Or, for `not_yet_a_pattern`: "We will not publish X as a pattern. It is a solution design
for {system}, and it is recorded as a worked example instead."}

## Consequences

**What this commits us to:** {maintaining it, reviewing it on a cycle, answering questions
about it, and — at `mandated` — running a waiver process.}

**What it closes off:** {the local choices teams can no longer make, and the decisions they
no longer have to make. Both halves matter.}

**What we accept:** {the known weakness. Every pattern published early has one; recording
it here is what stops the pattern being quietly abandoned instead of revised.}

## Blocked by constraint

{Where a hard constraint capped the status below what the score supported, name the policy
ID and what it says. State "None — the status reflects the assessment" explicitly if
nothing was blocked.}

{This section exists because a capped status and a judged status look identical from
outside, and the difference matters to anyone deciding whether to argue with it.}

## What would change the status

{Observable events, not sentiments:}

- {"A second independent implementation, built by a different team." — the usual promotion trigger from `proposed`.}
- {"Conformance criteria C2 and C4 rewritten so a reviewer can check them." — the usual blocker on `mandated`.}
- {"The operating envelope confirmed rather than derived."}
- {"At the review date, {YYYY-MM-DD}."}

## Assumptions this rests on

| # | Assumption | Still valid? |
|---|---|---|
| A1 | {…} | {to be reviewed at {date}} |
