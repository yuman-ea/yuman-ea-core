---
name: stakeholder-and-concern-map
description: >
  Establishes who has a stake in a piece of architecture work, what question each of them
  needs answered, and which deliverable answers it. Requires a concern to be a question
  rather than a topic, distinguishes concerns stakeholders actually stated from ones the
  architect inferred on their behalf, records conflicting concerns as conflicts rather than
  resolving them silently, and surfaces the stakeholder who can stop the work and has never
  been asked. Produces the stakeholder register, the concern-to-viewpoint matrix, and the
  reasoning behind both.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.stakeholder-and-concern-map
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: align
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Stakeholder and Concern Map

Run this at kick-off. Run it at the end and it explains why the work landed badly.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## A concern is a question, not a topic

| A concern | A topic |
|---|---|
| Will this pass our regulator's inspection in March? | Compliance |
| Can my team still close the period in three days? | Finance operations |
| What happens to the drivers' shift patterns? | People impact |

**Only the left column can be answered by a deliverable.** A topic tells you what someone cares about; a question tells you what to produce. The whole method turns on that distinction, and a map full of topics looks complete while telling nobody what to build.

Where what you were given is a topic, **mark it as a topic**. Converting it into a question on the stakeholder's behalf is a guess about what they meant, and it will be wrong in the direction of what the architect already wanted to produce.

## Stated or inferred — never blurred

An inferred concern is **the architect's concern wearing somebody else's name**.

It is not useless — it is often a good prediction — but it is not evidence, and deliverables built to answer inferred concerns are the ones nobody reads. Every row records which it is, and the sensitivity analysis removes the inferred ones to show what is left.

## The blocker nobody asked

> A stakeholder with **high blocking power and no recorded concern** has either not been asked or has not engaged. Both are the same risk, and it is the single most reliable source of late failure in architecture work.

They get their own section in the rationale, and they win every tie-break — because every other concern on the list is at least known about.

Note that blocking power and interest are different things. In a board-governed or regulated process, an approver with **no interest in the content** still holds a veto, and that combination is the most dangerous cell in the matrix.

## Conflicts are recorded, not resolved

Two stakeholders wanting incompatible things is a **decision someone has to make**. Resolving it quietly inside a deliverable removes their chance to make it, and the conflict returns at sign-off with a worse temper.

Every conflict records `who_decides_the_conflict`.

## Three groups of stakeholder, and the third is always missing

| Group | Usually captured? |
|---|---|
| Those consulted | Yes |
| Those who approve | Yes |
| **Those affected with no seat** | No |

Operators, support teams, customers, suppliers. They cannot raise a concern themselves, so their objection arrives through somebody else, late and distorted.

## When not to use this

| The question | Use |
|---|---|
| How should the organization be arranged? | [`operating-model-design`](../operating-model-design/SKILL.md) |
| Record why we chose this option | [`architecture-decision-record`](../../technology/architecture-decision-record/SKILL.md) |
| What does the customer experience? | [`customer-journey-to-system-map`](../customer-journey-to-system-map/SKILL.md) |
| Which domain owns this question? | `orchestrator` |

---

## Run it in this order

### 1. Frame

A concern is only meaningful against a **specific piece of work**. "What do you care about" produces topics; "what do you need to know before you can approve this" produces concerns.

### 2. Ask

Five questions. `concern_source` caps the confidence of the whole map, and `engagement_stage` decides what the map is for — at `after_pushback` it is usually diagnosing which stakeholder was missed, and the honest answer is frequently that they were on the list and never asked.

### 3. Gather

Three required: the **engagement definition**, the **stakeholder list**, and the **stated concerns**.

Three optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `decision_and_veto_rights` | Who can stop the work is not who is interested |
| `planned_viewpoints` | Without them there is no coverage question, only a list |
| `affected_but_unrepresented` | The group that produces late objections |

### 4. Bound

`information_classification` is a hard constraint. Where a view **cannot be shown** to the stakeholder whose concern it answers, that is a gap reported with the policy ID — not an answered concern.

### 5. Analyze

Concerns as questions. Stated or inferred, always. Blockers separately from the interested. Then map each concern to the deliverable that answers it — and where the deliverable set is open, **let the concerns determine it.** That is the only order that produces views anyone reads.

### 6. Deliver

| Artifact | File |
|---|---|
| Stakeholder register | `stakeholder-and-concern-map--stakeholder-register.md` \| `.csv` \| `.xlsx` |
| Concern to viewpoint matrix | `stakeholder-and-concern-map--concern-viewpoint-matrix.md` \| `.csv` \| `.xlsx` |
| Engagement rationale | `stakeholder-and-concern-map--engagement-rationale.md` \| `.docx` |

**A blank `answered_by` is a real value.** Concerns nothing will answer are the deliverable, not an incomplete row.

### 7. Verify

**Confidence** is `low` if any stakeholder with blocking power has no recorded concern — however complete the rest of the map.

`dissent_note` is emitted: where a stakeholder disagrees with how their own concern has been recorded, that is worth more than the record.

**Sensitivity** includes the cheapest useful test:

> **Remove every inferred concern.** What is left, and which deliverables lose their justification. It finds the views nobody will read before they are produced.

---

## Standing rules

**Roles, not just names.** The register has to survive a departure.

**Never present an inferred concern as a stated one.** The map's entire value rests on that line.

**Do not judge whether a concern is reasonable.** A concern held by someone who can stop the work is material whether or not it is well founded.

**A view in language the stakeholder cannot read has not answered their concern.** State what each view must contain, in their terms.

**Concerns determine deliverables, not the reverse** — wherever the set is still open.
