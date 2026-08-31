# Value stream rules

This reference constrains **what qualifies as a value stream and where its boundaries go**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## The three-part test

A value stream has a **trigger**, a **recipient**, and **value the recipient can recognise**. All three, or it is not one.

The test that catches most miscategorised streams: *if this completed perfectly and stopped where the map stops, would anyone outside the team be better off?* If the honest answer is "the next department would have what it needs", it is a process. Map it with [`business-process-model`](../business-process-model/SKILL.md) instead.

This distinction matters more than it sounds. A process map optimises how work is done. A value stream map asks whether the work should be done at all, and it can only ask that because it knows who the value is for.

## Stages are named for value, not for departments

| Good | Poor |
|---|---|
| Credit assessed | Finance review |
| Order confirmed to customer | Sales admin step 3 |
| Goods available to pick | Warehouse processing |

Naming a stage after the department that performs it embeds the current arrangement in the map, and every conclusion afterward is constrained by it. It also makes the stage impossible to score for value contribution, because "Finance review" describes who acts rather than what changes.

## Boundaries: the two failures

**Starting too late.** The overwhelmingly common one. The map begins where work arrives in the department that commissioned it, which excludes everything the requester did to get it there — filling in a form, chasing an approval, finding out what was needed, waiting for someone to respond. That excluded region routinely contains most of the elapsed time and nearly all of the frustration.

Ask directly: *what had already happened before the first stage on this map?*

**Ending too early.** The map ends when the organization considers the work done rather than when the recipient has value. An order is "complete" at dispatch; the customer has value on delivery, and everything between the two is invisible to a map that stops at the warehouse door.

Both failures share a cause. The boundaries get drawn where the commissioning function's authority ends, which is exactly where the interesting problems begin.

## Value-adding, necessary, and waste

Three categories, and the middle one is where the argument usually is:

- **Value-adding** — the recipient would recognise it as something they want, and would notice its absence.
- **Necessary but non-value-adding** — regulatory checks, controls, audit evidence. The recipient does not want it and the organization cannot lawfully or safely skip it.
- **Waste** — neither. Handoffs that exist because of how the organization is arranged, re-keying between systems, checks on checks, approvals nobody reads.

Be rigorous about the second category and generous with nothing. "Necessary" is where every stage retreats to when challenged, and the useful follow-up is always: *necessary because of what, specifically?* A named regulation or a stated control objective qualifies. "We have always done it" does not, and neither does "Finance requires it" without a person who will say so.

## One stream, one recipient

A stream serving two recipients is two streams sharing stages. Map them separately.

This looks like duplication and is not: the same stage frequently adds value for one recipient and none for the other, and a single map forces one answer where two are true. The commonest instance is a stream serving both a customer and a regulator, where the evidence-producing stages are pure overhead to one and the entire point to the other.

## Variation is the subject, not a complication

The instinct is to map the standard path and note the exceptions separately. Resist it where the exceptions carry material volume.

A stream where 80% of items take three days and 20% take five weeks has a mean of about fourteen days, which describes no item that has ever passed through it. The exceptions are not noise around the standard path; in elapsed-time terms they frequently *are* the stream.

Where exceptions are excluded for a good reason, say which ones and what share of volume they carry, so the reader can judge what the map is not covering.

## On mapping notation

This method produces tables, not diagrams, deliberately.

Value stream notations exist and several are useful. None of them are required to reason about flow, all of them add a rendering dependency, and a table survives every host — which is the floor this project builds to. Where a host can render a diagram, the stage table has everything needed to draw one.

Published value stream and lean practice is cited by name where it is drawn on. It is not reproduced.
