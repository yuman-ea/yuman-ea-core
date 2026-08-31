# Journey analysis rules

This reference constrains **how stage scores become a status, and what the map may conclude about systems**. Background, loaded on demand.

## Status rules

Applied in this order. The first that matches wins.

| # | Status | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | The stage could not be described, or three or more criteria are unscoreable |
| 2 | `non_conforming` | The stage breaches `accessibility_standard` or `data_residency` |
| 3 | `blind_spot` | `visibility_to_organization` ≤ 2 — nothing the customer does here leaves a record |
| 4 | `no_recovery` | `recovery_capability` ≤ 2 — a customer who hits a problem here has no route to resolution |
| 5 | `moment_of_truth` | `moment_criticality` ≥ 4 **and** any other criterion ≤ 2 |
| 6 | `high_effort` | `customer_effort` is the worst score |
| 7 | `fragmented` | `system_coherence` is the worst score |
| 8 | `smooth` | Everything else |

Two orderings are deliberate and worth defending.

**`non_conforming` outranks everything except unscoreable.** A stage that fails an accessibility standard is not a poor experience to be weighed against others; it is a stage some customers cannot complete at all, and averaging it into an effort score conceals that.

**`blind_spot` outranks the pain statuses.** A stage the organization cannot see cannot be managed, will not appear on an improvement list, and is not improving. Its invisibility is the more actionable finding than whatever score was estimated for it — and that score is an estimate, because there is no data.

## Effort predicts defection better than satisfaction

`customer_effort` carries the heaviest weight because of what it predicts. Customers tolerate a great deal — delay, imperfection, a mistake honestly handled — and leave over having to ask twice, explain again, or work out for themselves what should have been obvious.

Score it on what the customer has to *do*, not on how they feel about it:

- What they must supply, and whether they have supplied it before.
- What they must chase, and how they know to.
- What they must work out for themselves.
- How many times they must change channel.

The last one is disproportionately expensive and disproportionately invisible, because each channel's own metrics look fine.

## Visibility is a property of the organization

`visibility_to_organization` is unusual among criteria in this project: it scores the organization, not the thing being examined.

It earns its 0.20 weight because it is causal. A stage that produces no record has no metric, so it appears in no report, so it is on nobody's improvement list, so it does not improve — regardless of how bad it is. Every other criterion describes a problem; this one describes why the problem persists.

It is also the criterion that a digital-only map cannot score at all, which is why `channel_coverage` moves it.

## Systems: findings, not dispositions

A system named against a pain point is a **finding**. It is not a recommendation to replace, consolidate, or invest in it.

The reasoning is the same seam that runs through the whole framework. A disposition rests on run cost, contract position, dependency load, technical fitness, and what else in the estate would be affected — none of which this method sees. A journey map that concludes "replace the portal" has made a portfolio decision on customer-experience evidence alone, and it will be wrong roughly as often as it is right.

What the map may say: which stages hurt, what they cost the customer, which systems are involved, and that the disposition question is open. That is a strong input to `application-rationalization`, and a weak substitute for it.

## Pain lives at transitions

Record pain between stages at the **transition**, not inside either stage.

Re-entering information already given, being handed from one channel to another, losing a place in a queue, discovering that the answer differs depending on where you asked — none of these belong to a stage. Recorded inside one, they are assigned to a team that cannot resolve them alone, and both teams either side are correct that the problem is not theirs.

## Moments of truth: a few, not many

The instinct after mapping is to improve everything. Resist it, because improvement capacity is finite and journeys are not uniform: a small number of stages carry most of the outcome.

Identify them from what the customer says decides the relationship, not from where the scores are worst. A stage can be genuinely poor and irrelevant — the customer passes through it, notices nothing, and forms no view. Effort spent there buys nothing.

Where a small weight change reorders the moments of truth, report a candidate set rather than a ranking. The evidence is not separating them, and presenting a false order invites the organization to fix the second one first.

## What the map may not conclude

**That a pain point is worth fixing.** This method says what it costs the customer. What it costs to fix, and whether that pays, is `business-case`.

**That the journey is representative.** Where segments were not separated, the map describes an average customer who may not exist.

**That the pain list is complete.** Where pain was inferred internally, it is an inventory of what the organization already knew, reorganised into stages. That is genuinely useful and it is not the same as knowing what customers experience.
