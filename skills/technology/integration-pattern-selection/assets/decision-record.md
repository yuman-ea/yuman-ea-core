# {NNNN} — {Source} to {target}: {pattern}

- **Status:** {Proposed | Accepted | Superseded by {NNNN}}
- **Date:** {YYYY-MM-DD}
- **Deciders:** {names or roles}
- **Confidence at time of decision:** {low | medium | high}
- **Method:** yea.technology.integration-pattern-selection {version}

## Status

{Proposed | Accepted | Superseded by ADR-NNNN}

## Context

{What the integration is for, and the characteristics that drove the choice — timing,
volume, payload, delivery guarantee, replay, and whether it crosses an organizational
boundary. Enough that a reader in two years can tell whether their situation is the same.}

{State which figures were measured and which were estimated. The volume assumption is the
one most likely to have changed by the time anyone reads this.}

## Decision

{One sentence, active voice: "Order submissions will be published to the broker and
consumed asynchronously by order capture."}

{What is in scope of this decision, and what was deliberately left open — normally the
interface contract and the implementing product.}

## Consequences

**What this commits us to:** {infrastructure, support arrangements, and the skills to run it.}

**What the receiver must handle:** {idempotency, out-of-order arrival, backlog — whatever
the pattern does not guarantee.}

**What this closes off:** {options that become expensive after this is in production,
particularly adding consumers or changing the payload shape.}

## Failure path

{What happens when the receiver is unavailable, when a message is rejected, and when the
backlog grows faster than it drains. Where the data waits, for how long, and who is alerted.}

{This section is here rather than only in the recommendation because it is what an incident
review will look for, and the recommendation is not where anyone looks first.}

## What would make us revisit this

{Observable events, not sentiments:}

- {"If peak volume passes {N} per hour."}
- {"If a second consumer is proposed."}
- {"If the maximum payload exceeds {size}."}
- {"If the broker's support position changes."}

## Assumptions this rests on

| # | Assumption | Still valid? |
|---|---|---|
| A1 | {…} | {to be reviewed at {date}} |
