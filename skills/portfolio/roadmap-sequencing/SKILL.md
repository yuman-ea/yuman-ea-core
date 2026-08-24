---
name: roadmap-sequencing
description: >
  Sequences capability-building initiatives into waves that respect dependencies, fixed
  external dates, and the delivery capacity the organization actually has. Surfaces enabling
  work that nothing funds, dependencies that live in the estate rather than in anyone's plan,
  and the point at which a wave exceeds capacity — reported as infeasible rather than
  smoothed. Produces a wave plan, the reasoning behind the order, and a capacity profile
  showing where it breaks.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.portfolio.roadmap-sequencing
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: portfolio
  yuman_ea_category: design
  yuman_ea_owner_agent: portfolio-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Roadmap Sequencing

Puts capability-building initiatives into waves that survive contact with the organization's actual delivery capacity.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The three things that make a roadmap fiction

> **1. Capacity applied last, if at all.** A roadmap with fourteen parallel workstreams and three teams is a wish list with dates on it. Capacity is the binding constraint on almost every plan, and it is routinely the last thing checked — after the sequence has been agreed and socialised.

> **2. Enabling work nobody funds.** The capability three initiatives depend on has no business case of its own, because its benefit accrues to those three. So it never gets a wave, and three initiatives quietly slip instead. `enabling_value` carries the highest weight in this method for exactly that reason.

> **3. Dependencies discovered rather than designed.** The ones that stop a wave are the ones nobody stated — two initiatives both needing the same system, each correct that they need it, neither knowing the other is coming.

## Score sets priority. Constraints set placement.

The weighted score is a claim on an early wave. It is **not** the wave assignment.

Waves are assigned in priority order, then dependencies, fixed dates, freezes, and capacity determine what is actually feasible. Same model as `application-rationalization`: the score is a comparison aid, the placement comes from rules.

## Hard and soft dependencies

**Teams state everything as hard.** "A must finish before B" is very often "A must be far enough along that B can start" — and the difference between those two readings is routinely several months of plan.

Every dependency is classified `hard`, `soft`, or `inferred_from_estate`, and **every reclassification from hard to soft is recorded with who confirmed it**. That table is where the plan gained its months, and it is where the plan will break if the reclassification was wrong.

## Capacity is not a single number

Three teams is not capacity for work needing a data engineer if all three are front-end teams. The `skills_profile` input exists for this, and when it is absent the run says plainly that capacity has been treated as fungible — **the most common error in capacity planning**, and one that only surfaces when the wave starts.

Two more capacity rules, both easy to skip:

- **Subtract in-flight commitments before placing anything new.** Organizations are never starting from zero.
- **Reserve the slack before the wave is declared full.** A plan allocated to 100% of capacity fails on the first slip, and every plan slips. `slack_policy` makes it an explicit choice rather than an omission nobody decided on.

## When a plan does not fit

**Report it as infeasible. Never compress an initiative to make it fit, and never assume a dependency resolves faster than stated.**

Say what would have to give — capacity, scope, or a date — and let the organization choose. A plan that fits because the arithmetic was adjusted is a plan that fails in wave two, having spent the credibility that would have made the hard conversation possible in wave one.

## When not to use this

| The question | Use |
|---|---|
| Which initiatives are in trouble right now? | [`portfolio-health-dashboard`](../portfolio-health-dashboard/SKILL.md) |
| Which applications do we keep or retire? | [`application-rationalization`](../application-rationalization/SKILL.md) — its dispositions are an input here |
| Should we build or buy this capability? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) |
| Should this be funded at all? | `portfolio-ea` directly. This sequences what has been funded |

---

## Run it in this order

### 1. Frame

Restate the sequence and **confirm the capability targets**. Without them the plan optimizes for delivery convenience, which produces a defensible order that builds nothing in particular.

### 2. Ask

Five questions. `capacity_basis` caps the confidence of everything downstream — a capacity figure from headcount is systematically optimistic, because it counts people rather than throughput.

### 3. Gather

Three required: the **initiatives**, the **capability targets**, and the **capacity**. A rough capacity figure is fine; how good it is comes from the ask.

Four optional inputs carry a **high** penalty, and they are the four that decide whether the plan is real:

| Input | Why it matters |
|---|---|
| `stated_dependencies` | The sequence is only as good as the graph |
| `in_flight_commitments` | Planning on free capacity over-commits before publication |
| `initiative_sizing` | The whole capacity comparison rests on it |
| `fixed_dates` | A date discovered after publication moves everything behind it |

`estate_dependencies` is the architecture contribution — dependencies inferred from initiatives sharing a system, which nobody declares because each is correct that they need it.

### 4. Bound

`change_freeze_periods` is a hard constraint. A distribution business that freezes changes over its peak season cannot cut over in that window, whatever the plan says.

### 5. Analyze

Build the dependency graph, classify hard versus soft, name the enablers, apply fixed dates as **constraints on placement rather than outputs of the sequence**, then score for priority and assign waves against capacity.

Background on placement rules is in [`references/sequencing-rules.md`](./references/sequencing-rules.md); capacity and dependency mechanics are in [`references/capacity-and-dependencies.md`](./references/capacity-and-dependencies.md). Neither is needed to run the method.

### 6. Deliver

| Artifact | File |
|---|---|
| Wave plan | `roadmap-sequencing--wave-plan.md` \| `.csv` \| `.xlsx` |
| Capacity profile | `roadmap-sequencing--capacity-profile.md` \| `.csv` \| `.xlsx` |
| Sequencing rationale | `roadmap-sequencing--sequencing-rationale.md` \| `.docx` |

**The capacity profile is where the plan is honest.** Demand against supply per wave per skill, with `over_capacity` reported rather than smoothed.

**No initiative is left blank in the wave column.** `does_not_fit` and `beyond_horizon` are placements too, and where a horizon turns "later" into "never", that is a decision by omission that needs to be visible.

### 7. Verify

**Confidence** is derived and strict. Unknown capacity basis, assumed dependencies, estimated sizing, missing in-flight commitments, or **any wave over capacity** — any one of these means `low`.

`dissent_note` is emitted: where a delivery lead disagrees with a placement, record it. They usually know something the graph does not.

**Sensitivity** includes two that matter more than they look:

> **Capacity 20% lower than stated.** Where the basis is headcount rather than history, this is closer to the real number than the stated one.

> **One additional dependency discovered per initiative.** Dependencies are discovered, not designed. A plan with no tolerance for discovery is a plan for the first wave only.

---

## Standing rules

**Fixed dates are inputs, not outputs.** A contract expiry sets the latest wave an initiative can occupy. The plan works around it; it does not move it.

**Name the enablers.** Every initiative two or more others depend on, called out explicitly — because it is the work with no sponsor and it is the first thing cut.

**Every placement states its reason.** `priority_order`, `dependency_constrained`, `capacity_constrained`, `fixed_date_constrained`, `freeze_constrained`. A wave assignment with no reason cannot be argued with, which means it cannot be trusted.

**Smaller first, when tied.** It returns capacity sooner and the plan learns faster.
