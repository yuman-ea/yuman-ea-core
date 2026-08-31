# Capability modelling rules

This reference constrains **what counts as a capability and where the model stops**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## What a capability is

A capability is **what the organization does**, expressed as a noun, independent of who does it, how it is done, and what it is done with.

That independence is the entire point. It is what makes the model survive a reorganization, a system replacement, and an outsourcing decision — and therefore what makes it worth building rather than redrawing every eighteen months.

| Is a capability | Is not |
|---|---|
| Demand Forecasting | The Planning Team *(who)* |
| Cold Chain Compliance | Temperature Monitoring Rollout *(a project)* |
| Customer Onboarding | Improve Onboarding *(a verb — an initiative)* |
| Route Planning | The routing platform *(a system)* |
| Payroll | Shared Services *(an arrangement)* |

## The reorganization test

Applied to every candidate, and mandatory where the starting point was the org structure:

> **Would this still exist if we reorganized tomorrow?**

"Claims Handling" survives any structure. "Central Operations" does not — it is an arrangement, and it will be renamed within two years, taking the model's credibility with it.

This test is the difference between a model that is still used in five years and one that is quietly abandoned after the next restructure. It is cheap to apply and almost never applied, because starting from the org chart is fast and the result looks finished.

## Where to stop

Anything can be decomposed further. The question is never "can this be split?" — it always can — but:

> **Does the split change a decision anyone is going to make?**

Stop at the level where decisions are made. For most organizations that is level 2, occasionally level 3 for the capabilities under active scrutiny. A model taken uniformly to level 3 has usually been taken there because level 3 is conventional, and the bottom level is decomposition rather than evidence.

**Uneven depth is correct.** A model that is level 3 where a decision is pending and level 2 everywhere else is a model that was built for a purpose. A uniformly deep model was built to look complete.

## Coverage runs in both directions

Two checks, and the second is the one usually skipped:

1. **Every capability traces to evidence** of something the organization actually does. A capability with no derivation is aspiration — often imported from a reference model — and is marked as such rather than left blank.
2. **Every significant activity in the evidence lands in exactly one capability.** Activity with no home is either a capability nobody wanted to name, or work that should have stopped. Both findings are useful and neither survives a one-directional check.

## Overlaps are reported, not resolved

Where two capabilities contest the same activity, record the contest.

The temptation is to resolve it — assign the activity, tidy the model, move on. Resist it, because **the overlap is usually a real organizational ambiguity** rather than a modelling error. Two functions both believe they own customer data; the model did not create that, it found it. Quietly assigning the activity to one of them hides the finding and produces a model that one of the two parties will reject on sight.

Where the ambiguity is genuinely a drafting artifact, say so and merge. The distinction is whether anyone in the organization would argue about it.

## Levels are not a hierarchy of importance

Level 1 capabilities are not more important than level 3 ones. They are broader.

This is worth stating because level 1 lists get put on slides, and a slide of eight boxes reads as "the eight things that matter". A level 3 capability can be the single largest source of cost or risk in the organization, and it is one of forty on a page nobody prints.

## On reference models

Published industry reference models are useful starting points and are cited, never reproduced. Several carry licensing terms of their own, and a permissive repository licence does not launder incompatible material into a model an organization then publishes internally.

Two practical cautions when one is used:

- **Reference models describe an industry, not this organization.** Every capability inherited from one and not traced to local activity evidence is aspiration until it is.
- **They come with a depth convention**, which is where the pressure to decompose uniformly comes from. Take the structure; do not take the depth.

## On strategic position

`differentiating` / `parity` / `commodity` is a judgement about competition, not about how much the organization spends or how much it cares.

The failure is predictable and near-universal: **organizations classify far too much as differentiating.** Everything feels important from the inside, and the classification is often made by the people who run the capability. This is why the sensitivity analysis moves each differentiating capability to parity in turn — what survives that test is the short list, and it is usually much shorter than the executive team expects.

A useful challenge for each one: *would a competitor buying the same software from the same supplier be at the same level within a year?* If yes, it is parity at best, however well it is run.
