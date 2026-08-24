# {Capability} — requirements specification

**Date:** {YYYY-MM-DD} · **Author:** {name} · **Stage:** {defining requirements}
**Written:** {before any product was seen | drafted first, refined during | **derived from demonstrations**}

> **Produce this before any candidate is scored, and date it.** A specification that exists
> only after the demonstrations cannot be shown to be independent of them, whatever its
> content. This document is the evidence that the requirements were the organization's.

## What this is for

{The business outcome, in one or two sentences. Not a feature list, and not a product
category.}

## Must-haves

**Each one disqualifies a candidate that cannot meet it.** If it does not disqualify, it is
a want — move it.

| # | Requirement | Why it disqualifies | Who wrote it, and when |
|---|---|---|---|
| M1 | {…} | {what breaks without it} | {name, date relative to first demonstration} |

*A list of thirty must-haves is a list of wants with the wrong label, and it produces a
selection where every candidate fails and the decision is made on something else entirely.*

**Requirements only one candidate meets:**

| # | Requirement | Only met by | Genuine differentiator, or lifted from a feature list? |
|---|---|---|---|
| M{n} | {…} | {candidate} | {the answer, with who wrote it and when} |

*State "None" explicitly if none. This table decides more selections than the scoring does.*

## Wants, and what we would trade

| # | Want | Value if present | Would we trade it, and for what |
|---|---|---|---|
| W1 | {…} | {…} | {…} |

## Non-functional requirements

| Attribute | Target | Source |
|---|---|---|
| Availability | {…} | {stated by the business \| **PROPOSED — confirm**} |
| Performance | {at our volumes, at peak} | {…} |
| Scale and growth | {…} | {…} |
| Recovery | {data loss tolerance, time to restore} | {…} |
| Retention | {how long, retrievable by whom} | {…} |
| Security | {classification, access model, audit evidence} | {…} |

**Targets marked PROPOSED were derived, not stated.** A product selected without confirmed
non-functional targets is selected on features alone, and the gap surfaces during
implementation when the choice is no longer reversible.

## What we need from the supplier

*Scored separately from the product. These are requirements, not preferences.*

| # | Requirement | Why it matters here |
|---|---|---|
| S1 | {support model and hours} | {…} |
| S2 | {escalation path and response commitments} | {…} |
| S3 | {roadmap transparency and influence} | {…} |
| S4 | {contract flexibility — term, scaling down, exit} | {…} |
| S5 | {reference customers of comparable size and sector} | {…} |

## Constraints

| Constraint | Source | Effect |
|---|---|---|
| {…} | {policy ID, regulation, contract} | {which candidates it eliminates} |

## Where these requirements came from

{Who was consulted, over what period, and — stated plainly — whether any product had been
seen at the time. This section is why the document is credible.}

## Deliberately not required

{What the organization decided it does not need, and why. Recording this prevents a supplier
introducing a requirement the organization never had, and stops the list growing during
evaluation.}
