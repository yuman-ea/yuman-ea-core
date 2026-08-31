---
name: business-capability-map
description: >
  Builds a levelled model of what an organization does — stable capabilities rather than
  departments or systems — and heat-maps it against strategic importance, performance,
  system support, process maturity, and ownership. Refuses to decompose past the level the
  evidence supports, reports overlaps rather than resolving them silently, and rates each
  capability on its worst dimension rather than an average that hides it. Produces the
  capability model, the heat map, and the reasoning behind both.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.business-capability-map
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: discover
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Business Capability Map

Produces a model of **what the organization does** — and one that is still true after the next reorganization.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## Why this one carries more risk than it looks

A capability model is the artifact a language model can produce inline that looks completely correct. Plausible nouns, sensible levels, a tidy hierarchy — and no derivation, no coverage check, no confidence rating.

That matters more here than elsewhere because **nothing downstream ever contradicts it.** A wrong cost is caught by finance. A wrong architecture is caught when the system is built. A wrong capability model simply becomes the frame that every investment argument is conducted inside, for years.

So this method traces every capability back to evidence, and marks the ones it cannot.

## Three defects, in the order they occur

> **1. The model is the org chart with different borders.** The commonest failure by a distance. It looks finished, everyone recognises it, and it is obsolete the day the organization restructures — which is very often the event that prompted the request.
>
> The test is one question, applied to every capability: **would this still exist if we reorganized tomorrow?** "Claims Handling" survives. "Central Operations Team" does not.

> **2. Decomposed past the evidence.** Anything can be split further. Whether it *should* be depends on whether the split changes a decision. A model taken to level 3 on level 2 evidence has added precision that reads as added confidence — and `depth_required: evidence_led` exists to stop it.

> **3. Heat-mapped on a blended average.** A capability can be strategically vital, generously funded, well supported by systems, and still delivered entirely by three people who know how. Averaged, that reads "adequate". This method scores five dimensions **separately** and takes the status from the pattern.

## Score orders attention. The pattern sets the status.

Same model as `application-rationalization` and `roadmap-sequencing`: the weighted total is a comparison aid, never the rating.

| Status | The pattern behind it |
|---|---|
| `hotspot` | Matters a lot, performs badly on at least one dimension |
| `fragile` | Performs adequately, but on one person or one unsupported system |
| `overinvested` | Commodity work carrying differentiating-level cost or attention |
| `adequate` | Nothing here needs a decision |
| `strength` | Differentiating and performing. Protect it; do not optimise it |
| `insufficient_evidence` | Could not be rated, and says so |

Rules are in [`references/heat-map-rules.md`](./references/heat-map-rules.md).

**`overinvested` is the one nobody asks for.** Every organization requests the hotspots. The commodity capability quietly consuming differentiating-level money is frequently the most actionable finding in the run, and it is invisible to a map that only colours weakness.

## When not to use this

| The question | Use |
|---|---|
| How mature are we against where we need to be? | [`capability-gap-assessment`](../capability-gap-assessment/SKILL.md) — it consumes this |
| How does work actually flow end to end? | [`value-stream-map`](../value-stream-map/SKILL.md) |
| How should we be organized to deliver it? | [`operating-model-design`](../operating-model-design/SKILL.md) |
| Which applications support this, and which do we retire? | [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) |
| Should we build or buy this capability? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) |

---

## Run it in this order

### 1. Frame

State the boundary and what is deliberately outside it. **A capability model with no stated boundary grows until it describes everything and decides nothing.**

### 2. Ask

Five questions. Two of them set the ceiling on everything downstream:

- **`heat_basis`** caps confidence on the half of this artifact that drives money. An architect's read is a legitimate starting point and a poor thing to present as an assessment.
- **`structural_starting_point`** decides whether defect 1 gets corrected or inherited. Answering `org_structure` is not wrong — it is the most common honest answer — but it changes what the method has to do next.

### 3. Gather

Three required: the **business description**, the **scope boundary**, and the **activity evidence** the capabilities get traced back to.

Two optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `capability_performance_evidence` | The heat map rests on it entirely |
| `strategic_positioning` | Every rating is weighted against it, and stated position diverges from believed position more than either party expects |

`cost_by_capability` degrades to a roll-up of application run costs. That captures technology cost only — which understates people-intensive capabilities and flatters the automated ones. The assumption says so.

### 4. Bound

`capability_model_standard` and `strategic_priorities`. Most organizations have neither written down; `proceed_and_note` records the absence rather than stalling.

### 5. Analyze

Derive capabilities as **nouns**, apply the reorganization test, group into levels, run the coverage check **in both directions**, then score five dimensions separately.

Background is in [`references/capability-modelling-rules.md`](./references/capability-modelling-rules.md) and [`references/heat-map-rules.md`](./references/heat-map-rules.md). Neither is needed to run the method.

### 6. Deliver

| Artifact | File |
|---|---|
| Capability model | `business-capability-map--capability-model.md` \| `.csv` \| `.xlsx` |
| Capability heat map | `business-capability-map--capability-heat-map.md` \| `.csv` \| `.xlsx` |
| Model rationale | `business-capability-map--model-rationale.md` \| `.docx` |

**Every capability shows what it was derived from.** A capability with nothing in that column is aspiration, and is marked as such rather than left blank — blank reads as an oversight, and aspiration reads as fact.

### 7. Verify

**Confidence** is capped by `heat_basis`. Architect judgement or no basis means `low`, however complete the model looks.

**Sensitivity** includes the one that changes most conversations:

> **Move each differentiating capability to parity in turn.** Almost every organization overstates what it competes on. The capabilities that survive this test are the short list that actually matters, and it is usually much shorter than the executive team expects.

---

## Standing rules

**Capabilities are nouns.** Not verbs, not departments, not systems, not projects. "Demand Forecasting", not "Improve Forecasting", not "Planning Team", not "the forecasting platform".

**Report overlaps; do not resolve them.** Where two capabilities contest the same activity, that is usually a real organizational ambiguity. Picking a side quietly hides the finding — and the ambiguity is often the reason the work is done twice.

**Unassigned ownership is a finding, not a blank cell.** The capability nobody is accountable for is the one that never improves, whatever the other four dimensions say.

**Stop at the level where decisions are made.** Not at level 3 because level 3 is conventional.

**This model is not an operating model and does not imply a structure.** Say so in the rationale, every time. The single fastest way for this artifact to cause damage is for someone to read the level 1 list as a proposed set of departments.
