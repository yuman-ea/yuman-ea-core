---
name: capability-gap-assessment
description: >
  Assesses where capability maturity stands against what the strategy actually requires, and
  turns the difference into a backlog of things that have to change. Derives each target from
  a stated strategic requirement rather than defaulting to the top of the scale, records the
  assessor and the evidence behind every rating, and expresses a gap as the process, people,
  information, and governance changes that close it rather than as the distance between two
  numbers. Produces the maturity assessment, the gap backlog, and the reasoning behind both.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.capability-gap-assessment
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: assess
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Capability Gap Assessment

The bridge from a strategy to a list of things that have to change.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The target is the whole argument

> **A target of "level 5 everywhere" is not a target. It is the absence of one** — and it is the most expensive assumption available in this method, because it generates real, fundable work on capabilities nobody competes on.

Every target is derived from a **stated strategic requirement**, and the artifact records which one. A target with nothing behind it is an aspiration, and it will be defended in a steering committee as though it were a need.

This is why `over_targeted` is a status, and why the rationale carries a section nobody asks for: **where the target is higher than the strategy needs.** It is the counterpart to the gap list and usually releases more money.

## A maturity score is an opinion until you say whose

Every rating carries **the assessor** and **the evidence**. Both columns, always.

Self-assessment inflates in a known direction, and the direction is useful:

> Capability owners rate **process and governance generously** — they inhabit those, and they know the intent behind them. They rate **technology harshly** — they experience it. The bias is not dishonesty and it is not random, which is what makes it correctable.

The method states the bias rather than silently adjusting the numbers, and the sensitivity analysis quantifies it.

## A gap is what has to change, not a distance

"2 → 4" cannot be estimated, argued with, or assigned to anyone.

Every gap is expressed across five columns — **process, people, information, technology, governance** — because that is what makes it a backlog item rather than a score. Most gaps that look like technology gaps are not.

## Status comes from the pattern

| Status | Meaning |
|---|---|
| `close_now` | Strategy depends on it, and someone could start |
| `close_next` | Real and important, not yet ready or not yet affordable |
| `accept_gap` | A decision, recorded with **who accepted it** |
| `over_targeted` | The target exceeds what the strategy needs |
| `not_closable_in_horizon` | Takes longer to build than the strategy has — a constraint **on the strategy** |
| `blocked_by_another_gap` | Something else has to close first |
| `insufficient_evidence` | Could not be assessed |

Rules are in [`references/gap-and-target-rules.md`](./references/gap-and-target-rules.md).

**`accept_gap` has to be explicit.** A gap that is silently absent from the backlog is indistinguishable from one that was overlooked — and in two years nobody will be able to tell which it was.

## When not to use this

| The question | Use |
|---|---|
| What does the organization do, as capabilities? | [`business-capability-map`](../business-capability-map/SKILL.md) — this consumes it |
| How should we be arranged to run them? | [`operating-model-design`](../operating-model-design/SKILL.md) |
| In what order, against our capacity? | [`roadmap-sequencing`](../../portfolio/roadmap-sequencing/SKILL.md) |
| Build or buy what closes the gap? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) |
| Does closing it pay for itself? | [`business-case`](../business-case/SKILL.md) |

---

## Run it in this order

### 1. Frame

This method **assesses** a capability model. It does not build one — if there is no model, run [`business-capability-map`](../business-capability-map/SKILL.md) first rather than inventing capabilities to rate.

### 2. Ask

Five questions. `target_source` is the one the whole assessment rests on, and `assessment_basis` caps its confidence.

### 3. Gather

Three required: the **capability model**, the **strategic requirements** (specific enough that a level can be *derived*, not asserted), and the **current maturity evidence**.

Two optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `target_maturity_definitions` | Without targets there is no gap, only a rating |
| `capability_owners` | A gap with no owner is a wish — and unowned capabilities have the largest gaps, because nobody has been accountable |

### 4. Bound

`budget_ceiling` is a hard constraint. Northwind publishes none, so `proceed_and_note` records the absence — the backlog is then unconstrained, which is stated rather than implied.

### 5. Analyze

Derive targets from requirements, **challenge every target at the top of the scale**, rate against behavioural anchors with the assessor named, then express each gap as a change across five dimensions.

Test each against the horizon: **a capability that takes longer to build than the strategy has is a constraint on the strategy**, and saying so early is worth more than a backlog item nobody can deliver in time.

### 6. Deliver

| Artifact | File |
|---|---|
| Maturity assessment | `capability-gap-assessment--maturity-assessment.md` \| `.csv` \| `.xlsx` |
| Gap backlog | `capability-gap-assessment--gap-backlog.md` \| `.csv` \| `.xlsx` |
| Assessment rationale | `capability-gap-assessment--assessment-rationale.md` \| `.docx` |

### 7. Verify

**Confidence** is `low` where targets came from aspiration or are undefined — however carefully the current state was rated. Rating the present precisely against an invented future is precision in the wrong place.

**Sensitivity** includes the cheapest useful test in the method:

> **Lower every target by one level.** How many gaps disappear, and how much effort is released. Targets are set high by default and defended as requirements; this finds the ones that are real.

---

## Standing rules

**Rank by strategic dependency, not by gap size.** A large gap on a capability nothing depends on is not a priority, and ranking by size is exactly how commodity capabilities get expensive.

**The scale travels with the assessment.** Ratings on an unstated scale are not comparable across capabilities or across time, which makes the next assessment worthless as a comparison.

**Name the unowned gaps.** They are disproportionately the largest ones, and they will still be on the list at the next assessment unless an owner is assigned now.

**An accepted gap is a decision with a name on it.**

**Enabling gaps first.** Capability rarely builds in isolation; a gap that blocks three others returns its investment through all of them.
