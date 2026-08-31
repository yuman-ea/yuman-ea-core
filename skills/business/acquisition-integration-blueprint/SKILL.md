---
name: acquisition-integration-blueprint
description: >
  Plans what must keep working the day an acquisition closes and which capabilities
  consolidate in the hundred days after it. Separates continuity from integration so day one
  carries only what genuinely breaks at close, decides consolidation at the capability level
  and routes application disposition elsewhere, treats adopting the acquirer's way as a
  decision rather than a default, and names the capability the deal was for so that
  standardisation does not remove it. Produces the day-one plan, the capability
  consolidation map, and the reasoning behind both.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.acquisition-integration-blueprint
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: design
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Acquisition Integration Blueprint

Day one is a **continuity** problem. Day one hundred is an integration problem. Confusing them is how integrations fail in their first week.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## Day one has exactly one question

> **What breaks the moment the deal closes?**

People unpaid. Customers uninvoiced. A regulatory return missed. A service commitment broken. A seller-provided service switched off.

Everything else — however sensible, however cheap, however much somebody wants it — belongs after day one. The correct answer for most capabilities on day one is **"exactly as it does today, unchanged"**, and a plan whose day-one list is short is a plan that works.

The blueprint therefore carries a section that matters as much as the day-one list: **what we are deliberately not doing on day one.** Every item there was proposed by somebody and refused for a reason, and writing the reason down is what stops it being proposed again in week three.

## Name what you bought, or standardisation will remove it

An integration programme's own logic is to standardise. That logic is usually right, and it is catastrophic when applied to the capability the deal was for.

`deal_rationale: capability_acquisition` triggers the strongest protection in the method — a `protect_do_not_touch` disposition and an explicit list. It is short, and it is the most important output here, because it protects what was bought at precisely the moment the organization is most enthusiastic about making everything consistent.

**Consolidation deferred can be revisited. A capability standardised away does not come back** — and by the time anyone notices, the people who carried it have left.

## "Adopt ours" is a decision, not a default

Where both organizations do the same thing, the question is **which way is better**, not which organization owns it.

`adopt_target` is a real disposition and it is chosen more often than acquirers expect. The acquired business is frequently smaller, more recent, and less encumbered, and its way of doing something is better often enough that assuming otherwise is expensive.

## Capability level, not application level

This method decides that a capability consolidates. It does **not** decide which named system survives — that rests on run cost, contract position, dependency load, and technical fitness, none of which this method holds.

Every consolidation row names [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) as the owner of that question. This is the seam [ADR-0005](../../../docs/adr/0005-business-ea-agent.md) exists to police, and an acquisition is where it is most likely to be crossed.

## When not to use this

| The question | Use |
|---|---|
| Which of the two order systems survives? | [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) |
| In what order, against our capacity? | [`roadmap-sequencing`](../../portfolio/roadmap-sequencing/SKILL.md) |
| How should the combined organization be arranged? | [`operating-model-design`](../operating-model-design/SKILL.md) |
| What do the two contract sets cost to merge or exit? | [`license-and-contract-review`](../../portfolio/license-and-contract-review/SKILL.md) |
| Does the acquisition pay for itself? | [`business-case`](../business-case/SKILL.md) |

---

## Run it in this order

### 1. Frame

Describe **both** organizations' capabilities in the same terms before comparing anything. A comparison across two vocabularies produces false overlaps and misses real ones — so record the translation.

### 2. Ask

Five questions. `deal_rationale` decides what must be protected; `access_to_target_information` caps the confidence of everything and decides which findings are conclusions and which are questions for day one.

### 3. Gather

Three required: the **deal definition**, the **acquirer's capability model**, and the **target capability view**.

Four optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `day_one_obligations` | The day-one list is built from it |
| `separation_service_schedule` | End dates set by someone outside the organization |
| `target_contracts` | Change-of-control terms are found late and expensively |
| `target_people_and_knowledge` | The window is weeks and it closes on its own |

### 4. Bound

`data_residency` and `security_baseline` are hard constraints. Where the acquired business cannot meet one, that is **reported with the policy ID** as a constraint on the integration — not scored as a weakness.

### 5. Analyze

Same vocabulary. Name what was bought. Build day one from the one question. Refuse everything else from it. Map separation dependencies and their dates. Then compare capabilities pairwise and score.

### 6. Deliver

| Artifact | File |
|---|---|
| Day one plan | `acquisition-integration-blueprint--day-one-plan.md` \| `.csv` \| `.xlsx` |
| Capability consolidation map | `acquisition-integration-blueprint--capability-consolidation-map.md` \| `.csv` \| `.xlsx` |
| Integration blueprint | `acquisition-integration-blueprint--integration-blueprint.md` \| `.docx` |

**`verified_or_assumed` is a column on every day-one item.** Where access was limited, most of the list is assumed — and an assumed day-one item is the one that fails on day one.

### 7. Verify

**Confidence** is `low` if the separation schedule is unknown, or contracts have not been checked for change-of-control terms — however thorough the capability work.

`dissent_note` is emitted. The acquired business's own view of what matters differs from the acquirer's, reliably and usefully.

**Sensitivity** includes the one that argues for the do-not-touch list:

> **Standardise every acquired capability onto the acquirer's way.** What is lost, named specifically. That is the default outcome of an integration programme left to run on its own logic.

---

## Standing rules

**Day one is continuity. Everything else is after it.**

**State day-one items as outcomes** — "people get paid on the 28th" — not as systems or tasks.

**Name the capability the deal was for**, in the first section, every time.

**Record the acquired business's own term for each capability.** Comparing across vocabularies is how false overlaps get created and real ones get missed.

**A transitional service end date is harder than any internal deadline.** It belongs to a party with no interest in the acquirer's readiness, and it is renegotiated from a weak position.

**Nothing here is about specific people**, roles at risk, or retention. Knowledge concentration is recorded as a risk to capture, not as a judgement about anyone.
