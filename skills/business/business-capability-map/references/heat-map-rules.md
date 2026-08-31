# Heat map rules

This reference constrains **how five separate dimension scores become one status**. Background, loaded on demand.

## The weighted total is not the status

The weighted score exists to order capabilities for attention. It is a sorting aid.

Taking it as the rating produces the characteristic failure of every heat map built on an average:

> A capability scores **5** on strategic importance, **4** on system support, **4** on cost, **4** on ownership, and **1** on process maturity — it is delivered entirely by three people who happen to know how. The weighted total says *adequate*. The capability is one resignation away from stopping.

Averages hide exactly the thing a heat map exists to find. **The status comes from the pattern.**

## Status rules

Applied in this order. The first that matches wins.

| # | Status | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | Two or more dimensions could not be scored from any evidence, or the capability was not traced to activity evidence at all |
| 2 | `hotspot` | `strategic_importance` ≥ 4 **and** any of `performance_gap`, `system_support`, `process_maturity` ≤ 2 |
| 3 | `fragile` | No dimension ≤ 2, but the capability rests on a single point of failure — one person, one unsupported system, one supplier — evidenced rather than assumed |
| 4 | `overinvested` | `strategic_importance` ≤ 2 **and** cost or system support sits in the top quartile of the model |
| 5 | `strength` | `strategic_importance` ≥ 4 **and** every other dimension ≥ 4 |
| 6 | `adequate` | Everything else |

Rule 1 comes first deliberately. **An unrated capability must never fall through into `adequate`**, which is what happens when missing evidence is scored as a 3.

## Always name the driving dimension

Every status records which dimension produced it.

This is not presentation detail. A capability that is hot because nobody owns it, one that is hot because the systems fight it, and one that is hot because it has never been defined need three completely different interventions — and all three are the same colour on the map. The colour starts the conversation; the driving dimension is what makes it actionable.

## `overinvested` is the finding nobody requests

Every organization asks for the weaknesses. Almost none ask which commodity capability is quietly consuming differentiating-level money and attention.

It is worth flagging for two reasons. It is usually the most actionable finding in the run — reducing spend on something nobody competes on needs no business case, only a decision. And it is **structurally invisible** to a map that only colours weakness, because an overinvested capability is performing perfectly well. That is precisely the problem: it is performing well at something that does not matter.

Two cautions before reporting one:

- **Check the cost basis.** Where cost was rolled up from application run cost, it captures technology only. A people-intensive commodity capability will look cheap and an automated one expensive, which can invert the finding entirely.
- **Regulatory and safety capabilities are not overinvested.** They are commodity by definition — nobody competes on them — and the correct spend is whatever satisfies the obligation. Exclude them explicitly rather than letting the rule catch them, and say in the artifact that they were excluded.

## `fragile` requires evidence, not intuition

The single-point-of-failure judgement is easy to make and easy to make badly. Every capability looks fragile if you ask whether one person leaving would hurt.

Require something concrete: a named individual with no documented alternative, a system past support with no replacement path, a supplier with no second source, or a process that has failed when a specific person was absent. Without one of those, the capability is `adequate` and the concern goes in the rationale as an observation.

## What the map may not be used for

**It is not a maturity assessment.** Maturity is measured against a defined target using a defined scale, by someone accountable for the rating. This is a heat map: it says where attention is warranted, on the evidence available, at a stated confidence. Where a real maturity judgement is needed, the gap assessment is the method — and it will ask for its own evidence rather than inheriting these scores.

**It is not a budget allocation.** A hotspot is where a decision is warranted, not where money should go. Some hotspots are resolved by a decision costing nothing at all — naming an owner is the commonest.

**And a blank cell is read as "fine".** Whatever the legend says, an uncoloured capability in a room full of coloured ones is understood as unproblematic. `insufficient_evidence` must be visually distinct from `adequate`, in every rendering, or the map lies quietly about its own coverage.
