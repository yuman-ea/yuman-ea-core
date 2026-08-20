# Conformance criteria, variation, and keeping a pattern alive

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when writing conformance criteria, or when a pattern has been published and needs to survive contact with delivery.

## Why conformance criteria decide whether a pattern is real

A pattern's authority is exactly as strong as a reviewer's ability to tell whether a solution follows it. That is the whole mechanism. Without it, "conforms to the pattern" means "the architect who wrote the pattern likes this design," which is not governance — it is a bottleneck with a document attached.

**The test:** could someone who did not write the pattern, reading only the criterion and the solution, reach the same verdict as you? If not, it is not a criterion.

## Turning wishes into criteria

| Wish | Criterion |
|---|---|
| "Services should be loosely coupled" | "No component reads another component's data store directly. Every cross-component read goes through a published interface." |
| "It should be resilient" | "The consumer continues to serve requests when the producer is unavailable, using last-known data, and surfaces staleness after 24 hours." |
| "Use the standard integration approach" | "New interfaces are registered with the broker. Point-to-point interfaces require a recorded deviation." |
| "It should be secure" | "Every interface authenticates. Authorization decisions are logged with an exportable audit trail retained for the period the policy requires." |
| "It should be observable" | "Each component emits request rate, error rate, and latency, and a failed message is retrievable by correlation ID." |

The pattern in the right-hand column: **an observable thing, and a threshold or a boundary.** Anything else is a preference.

Aim for **five to nine criteria.** Fewer, and the pattern is not really constraining. More, and reviewers stop checking them, which is worse than having none because it produces the appearance of governance.

## What a criterion should never do

**Name a product.** Products change on procurement cycles; a criterion naming one expires with the contract and cannot be adopted by anyone else.

**Encode a preference as a rule.** "Written in the same language as the reference implementation" is usually taste. If it genuinely matters, say why in terms of the force it resolves — supportability, skills, operational tooling — and then the criterion writes itself differently.

**Restate the shape.** "Follows the structure in the diagram" is not checkable. Say which property of the structure matters.

## Variation

The `variability_tolerance` answer decides what the pattern may claim.

**`strict_conformance`** — every criterion must be met. Appropriate where the whole benefit comes from uniformity — a shared operational model, a compliance position, one on-call team supporting many systems. Rare, and honest patterns are rare in claiming it.

**`conform_or_explain`** — the working default. Teams may vary where they must, and record why in a decision record. **This only works if somebody reads those records.** A conform-or-explain pattern nobody audits has become guidance without anyone noticing, and the catalogue is now telling a lie about its own authority.

The records are also the most valuable input the pattern owner has. Three teams deviating from the same criterion for the same reason is not three deviations — it is a defect in the pattern, and the right response is to revise it rather than to keep granting exceptions.

**`adapt_freely`** — take the ideas, shape them locally. Legitimate and often correct for patterns whose value is conceptual. **Say so plainly and do not publish conformance criteria**, because criteria you will not enforce train people to ignore the ones you would.

## Waivers, where the pattern is mandated

A waiver process needs four things, and most have two:

1. **Who grants it** — a named role, not a committee that meets monthly, or teams will build first and ask later.
2. **What evidence is required** — normally: which criteria cannot be met, why, what is done instead, and what risk that carries.
3. **How long it lasts.** A permanent waiver is an admission the pattern is wrong. Time-box it and revisit.
4. **Where it is recorded**, so the next reviewer of the pattern can see the accumulated exceptions.

If the fourth is missing, the pattern will be defended long after the evidence stopped supporting it, because nobody can see the pile of waivers.

## Keeping it alive

**An owner and a review date, or the pattern rots.** Not into being wrong — into being *quietly* wrong, still cited, still shaping designs, while the estate it described has moved on. That failure is slow and hard to spot, and the cost lands on whoever trusted it.

At each review, three questions:

- **Is the operating envelope still true?** Volumes grow; a pattern sized for one scale silently becomes a liability at another.
- **What did the deviations say?** Repeated deviation against the same criterion means revise, not enforce.
- **Is it still cheaper to follow than to ignore?** When the adoption cost rises — through platform change, or the pattern accreting requirements — teams route around it, and a routed-around pattern damages every other pattern in the catalogue.

**Withdrawing a pattern is a legitimate act and should be easy.** Mark it superseded or withdrawn, say what replaced it or why nothing did, and leave the record intact. Never edit a published pattern into a different one — the systems built against the original version still exist, and their teams need to be able to find what they were told.
