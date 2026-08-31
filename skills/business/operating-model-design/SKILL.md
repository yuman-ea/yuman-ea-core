---
name: operating-model-design
description: >
  Designs how an organization is arranged to deliver what it has committed to — across work,
  organization, locations, information, suppliers, and the management system that governs
  them. Starts from the value proposition rather than the current structure, requires every
  design choice to name what it makes harder, and treats the transition as part of the design
  rather than as an implementation detail. Produces the operating model canvas, a design
  decision register, a transition view, and the reasoning behind all three.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.operating-model-design
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: design
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Operating Model Design

How the organization is arranged to deliver what it has promised — across all six dimensions, not just the org chart.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The org chart is the last thing you design

> Reorganizations start with boxes and lines, redraw them, and stop. That is why so many of them change reporting relationships and no outcomes.

The design starts from the **value proposition** — what the organization has committed to deliver, to whom — and works through the work, the locations, the information, the suppliers, and the management system before it arranges anybody.

A design that starts from the current structure has already decided the answer.

## Six dimensions, all of them answered

| Dimension | The question |
|---|---|
| **Work** | What actually gets done, at what volume and standard |
| **Organization** | Which roles are accountable for it |
| **Locations** | Where it happens, and what is genuinely location-bound |
| **Information** | What has to be known, by whom, when |
| **Suppliers** | What others do for us, and how tightly we are coupled to them |
| **Management system** | What is measured, who decides, what escalates |

A design that answers organization and technology and skips the rest is a reorganization with a diagram.

**The management system is the one that decides whether it works.** It is the most-skipped dimension and the most determinative, because it is what people actually respond to. A perfect structure with the wrong measures produces the behaviour the measures reward.

This dimensional frame follows the published Operating Model Canvas work (Campbell and others) and the POLISM shorthand, cited rather than reproduced.

## Every choice names what it makes harder

Mandatory column in the decision register. **An arrangement that optimises for something de-optimises for something else** — centralising gains consistency and loses local responsiveness, federating does the reverse — and a choice with no stated trade-off has not been made, only asserted.

It is also the column that makes the design survivable. When the de-optimised thing goes wrong in eighteen months, the register shows it was a known cost rather than an oversight.

## Transition is part of the design

A target with no viable path is a picture, and it is the most common output of operating model work.

The transition view carries two columns that do the real work:

- **`must_keep_running`** — what cannot stop while this change happens. This is what turns a plausible transition into an implausible one.
- **`if_it_stalls_here`** — the state the organization is left in. **Transitions stall.** An option that is unworkable halfway is a worse choice than a weaker end state that is not, and that trade-off is invisible in an end-state comparison.

## When not to use this

| The question | Use |
|---|---|
| What does the organization do, as capabilities? | [`business-capability-map`](../business-capability-map/SKILL.md) — this consumes it |
| Where are we against the maturity we need? | [`capability-gap-assessment`](../capability-gap-assessment/SKILL.md) |
| How does work flow end to end today? | [`value-stream-map`](../value-stream-map/SKILL.md) |
| What has to work on day one after an acquisition? | [`acquisition-integration-blueprint`](../acquisition-integration-blueprint/SKILL.md) |
| In what order, against our capacity? | [`roadmap-sequencing`](../../portfolio/roadmap-sequencing/SKILL.md) |
| Does the reorganization pay for itself? | [`business-case`](../business-case/SKILL.md) |

---

## Run it in this order

### 1. Frame

State the value proposition and what is held constant around the scope. The design is measured against the proposition and **nothing else**.

### 2. Ask

Five questions. Two of them exist to surface things that are usually decided in advance and defended afterwards as conclusions:

- **`centralisation_preference`** — the axis nearly every operating model argument actually runs on. Asking separates a preference the design must accommodate from a question the design should answer.
- **`people_constraint`** — most of this work happens under an unstated headcount assumption. Leaving it unstated distorts every other choice and makes the design impossible to argue with.

### 3. Gather

Three required: the **value proposition**, the **capability model**, and the **design scope**.

Three optional inputs carry a **high** penalty, and they are the three that decide whether the design is grounded:

| Input | Why |
|---|---|
| `current_operating_arrangement` | Without it there is no transition, only a target |
| `decision_rights_map` | The management system cannot be designed against an unknown one |
| `performance_measures` | What is measured today explains the behaviour the design has to change |

### 4. Bound

`segregation_of_duties` and `data_residency` are hard constraints. An option breaching either is **eliminated, not scored down**, with the policy ID.

### 5. Analyze

Value proposition → work → the other five dimensions → **organization last**. Check every capability has a home and an owner; where one is split across units, name who owns the outcome.

### 6. Deliver

| Artifact | File |
|---|---|
| Operating model canvas | `operating-model-design--operating-model-canvas.md` \| `.docx` \| `.pptx` |
| Design decision register | `operating-model-design--design-decision-register.md` \| `.csv` \| `.xlsx` |
| Transition view | `operating-model-design--transition-view.md` \| `.csv` \| `.xlsx` |
| Model rationale | `operating-model-design--model-rationale.md` \| `.docx` |

### 7. Verify

**Confidence** is `low` where the management system dimension could not be evidenced — however complete the rest.

`dissent_note` is emitted. Operating model design generates real disagreement between people who will have to live with the result, and averaging it away removes the information the decision needed.

**Sensitivity** includes the test the design will be challenged on anyway:

> **Design the opposite of the stated centralisation preference and score it.** Where the preference and the winning option coincide, this is the only available evidence that the design was derived rather than assumed.

---

## Standing rules

**Roles, never individuals.** Designing around the people currently available produces a model that works once and is obsolete at the first departure.

**Name what each choice makes harder.** Mandatory, every time.

**A split capability needs an outcome owner.** Splits are where capabilities quietly stop being anybody's job.

**Name the capabilities the model needs and the organization does not have.** A model resting on them is a capability programme with an organization chart attached.

**Prefer the reversible option when scores are close.** Operating models are wrong more often than they are catastrophic, and the cost of being wrong is dominated by how hard it is to change again.
