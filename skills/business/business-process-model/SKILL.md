---
name: business-process-model
description: >
  Models how a process actually runs — its steps, lanes, decision points, handoffs, and
  controls — and, where asked, the shape it should take instead. Records the difference
  between the documented procedure and the observed one as a finding rather than correcting
  it silently, requires every control to name the failure it prevents, and treats exception
  paths as part of the process rather than as notes beneath it. Produces the process model,
  a control and handoff register, and the reasoning behind both.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.business-process-model
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: design
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Business Process Model

Documents how a process **actually runs**, at the level of detail its purpose requires and no further.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## Four rules that make it a model rather than a diagram

> **1. Model the process as run; record the procedure alongside it.** In any process older than a couple of years these differ, and the difference is the most useful finding available. **Do not correct the model to match the document.** The workaround is usually rational, and the reason it exists is usually the actual defect.

> **2. Every control names the failure it prevents.** A control that cannot is recorded as `ceremony` — not removed, because removal belongs to the control owner. Ceremony is expensive, slow, and defended more fiercely than anything that works.

> **3. Exceptions are part of the process.** They routinely carry a third of the volume and most of the effort. A model of the standard path documents the cases that were never the problem, and it is why automation programmes discover their real scope after the build starts.

> **4. Handoffs are where processes fail.** Model what passes, in what form, and — the column that earns its place — **what the receiver has to assume because it was not passed.**

## Status comes from the pattern

The weighted score orders steps for attention; the status says what to do:

| Status | Meaning |
|---|---|
| `control_gap` | A failure is claimed to be controlled and is not |
| `ceremony` | A control that cannot name what it prevents |
| `handoff_risk` | Context does not survive the transfer |
| `undocumented_variance` | Practice diverges from the procedure |
| `unmodelled_exception` | A path carrying volume that is not in the model |
| `unclear_decision` | Nobody could state the rule or the authority |
| `sound` | Nothing here needs a decision |
| `insufficient_evidence` | Could not be assessed |

Rules are in [`references/control-and-handoff-rules.md`](./references/control-and-handoff-rules.md).

## A to-be with no as-is cannot be risk-assessed

Where both are produced, they **share step IDs** so the model can be diffed. Every change is then visible as a change, with what it costs and what it assumes.

`to_be_only` is a legitimate answer to `model_state` and is sometimes the only one available. It carries a stated limitation: nobody can tell whether the new design solves the actual problem, because the actual problem was never written down.

## On BPMN

The model is BPMN-shaped — lanes, tasks, gateways, events — expressed as a **table**, which every host can render and which carries everything needed to draw the diagram where a host can.

That is a deliberate choice. Notation is cited, never reproduced, and a diagram that only renders in one tool is not a deliverable for an architect with no platform.

## When not to use this

| The question | Use |
|---|---|
| How does value flow end to end across the business? | [`value-stream-map`](../value-stream-map/SKILL.md) |
| What does the customer experience, on which systems? | [`customer-journey-to-system-map`](../customer-journey-to-system-map/SKILL.md) |
| How should the organization be arranged to run it? | [`operating-model-design`](../operating-model-design/SKILL.md) |
| Which system should run this process? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) |
| How should these two systems exchange the data? | [`integration-pattern-selection`](../../technology/integration-pattern-selection/SKILL.md) |

---

## Run it in this order

### 1. Frame

Trigger, outcome, boundaries. **A process with no stated trigger is a set of activities**, and it will grow to absorb whatever the modeller finds interesting.

### 2. Ask

Five questions. Two set the ceiling:

- **`evidence_source`** decides whether this can claim to be the as-is at all. `documentation_only` means the model describes the process as designed, which is a different artifact.
- **`modelling_purpose`** sets what detail is useful and what is noise. An automation model needs every decision rule explicit; a training model needs the judgement calls. Modelling for all four purposes at once produces something too dense for any of them.

### 3. Gather

Three required: the **process definition**, the **activity sequence as performers describe it**, and the **performers and systems**.

Three optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `control_inventory` | Without the failure each control prevents, control effectiveness cannot be scored at all |
| `exception_and_volume_data` | Decides whether the model covers the volume or just the happy path |
| `decision_rules` | Inferred rules capture the usual case and miss the escalations — exactly where automation diverges |

### 4. Bound

`segregation_of_duties` and `records_retention` are hard constraints. A to-be step breaking either is **eliminated, not scored down**, and the elimination is reported with the policy ID.

`control_context: regulated` changes what may be removed. A step that adds no value can still be mandatory, and a redesign dropping it creates an exposure nobody costed.

### 5. Analyze

Steps as performers describe them, lanes by accountable role, handoffs modelled explicitly, controls challenged to name their failure, exceptions modelled at the same depth as the standard path.

Then **stop at the level the purpose requires.** Detail beyond that is not more rigour — it is a model nobody will maintain, which is worse than a coarse one that stays true.

### 6. Deliver

| Artifact | File |
|---|---|
| Process model | `business-process-model--process-model.md` \| `.csv` \| `.xlsx` |
| Control and handoff register | `business-process-model--control-and-handoff-register.md` \| `.csv` \| `.xlsx` |
| Process rationale | `business-process-model--process-rationale.md` \| `.docx` |

**`differs_from_procedure` is a column, not a comment.** Divergences are countable, and their count is a measure of how much the process depends on undocumented judgement.

### 7. Verify

**Confidence** is `low` where the model came from documentation or recollection alone — however complete and tidy the result.

**Sensitivity** includes the one that most often changes a business case:

> **Exception paths carry a third of total volume.** A model built on the standard path routinely underestimates real scope by about this much.

---

## Standing rules

**Lanes are roles, never individuals.** A model naming people is obsolete at the next departure and unusable for anything else.

**A control with no named failure is ceremony — recorded, not deleted.** Removal is the control owner's decision, and some of what looks like ceremony is the only thing standing between the process and a known failure.

**A control producing no evidence cannot be assured.** Whatever it prevents.

**Mark every inferred decision rule.** An inferred rule and a stated one look identical in a model and behave completely differently in an implementation.

**Never correct the model to match the document.** That erases the finding and produces a model that describes a process nobody runs.
