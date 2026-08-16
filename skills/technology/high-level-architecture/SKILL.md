---
name: high-level-architecture
description: >
  Produces a high level architecture for a solution: the candidate architecture options,
  the one recommended, the views a reviewer needs, the significant decisions with their
  rationale, and the risks. Assesses options against declared quality attributes and
  states the non-functional requirements it had to assume rather than inventing them.
  Works from manual input and CSV; no modelling tool required.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.technology.high-level-architecture
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: technology
  yuman_ea_category: design
  yuman_ea_owner_agent: technology-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# High Level Architecture

Produces the architecture a solution will actually be built to, and the argument for why it is that one rather than the two others that were on the table.

The machine-readable contract — criteria, weights, missing-data behaviour, artifact sections — is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

**An architecture document is unusually good at looking finished.** Sixteen sections, four views, a decision log — it reads as authoritative whether or not anything in it was checked. That is the specific hazard of this skill, and it is why the confidence rating is derived from the evidence rather than from how complete the document looks.

## When not to use this

- **The sourcing question is still open.** Build, buy, or partner comes first — [`build-vs-buy`](../build-vs-buy/SKILL.md). Architecting before that decision produces an architecture for an option that may not be chosen.
- **A product has been selected and you need the interface specifications.** That is detailed design.
- **The question is what it costs or whether to fund it.** Different owner.

Say which it is and stop.

---

## Run it in this order

### 1. Frame

Restate the request and **get the scope boundary agreed before drawing anything**:

> Define a high level architecture for **{solution_intent}**, at **{architecture_scope}** scope, optimizing above all for **{dominant_quality_attribute}**, given that the solution **{estate_position}** and will be delivered and run under a **{delivery_and_run_model}** arrangement.

Then state what this run will not decide. **Scope disagreement is the most common reason an architecture document is sent back**, and it costs one sentence to settle here against a rewrite later.

### 2. Ask

Five questions, in `skill.yaml`. The one that carries the most weight is the dominant quality attribute — an architect who will not choose one is telling you the drivers have not been agreed, which is itself a finding worth reporting.

Apply `default_if_skipped` where the user declines, say which default you applied, and register it.

### 3. Gather

Three required inputs: **solution intent**, **must-have requirements**, **existing estate touchpoints**. All three come from the user's own knowledge.

Six optional inputs each declare what happens when absent. One of them matters more than the rest:

> **Non-functional requirements are the input most often missing and the one that most changes the architecture.** When they are absent, derive indicative targets and label them **proposals for confirmation** — not findings. Mark every decision that rests on one. Then rate the run's confidence accordingly, which for this input means `low`.

An availability target invented in passing and then designed against for six months is the most expensive mistake this skill can make.

Where the owning agent can supply an input from a context slice, use it and say which slice. A looked-up figure and a derived one must never look the same in the register.

### 4. Bound

Apply the policies in `bound.policies` as an overlay supplies them. With no overlay — the normal case — proceed and record which constraints were unstated.

**Apply hard constraints before generating options**, and record every option eliminated with the policy ID that eliminated it. `customer_master_authority`-style rules routinely kill an otherwise attractive architecture, and the reader has to see that happen rather than wonder why an obvious option is missing.

### 5. Analyze

**Two to four genuinely different options.** Two options that differ only in a component name are one option, and the assessment is theatre. If only one architecture is realistically available, say so plainly — that is a legitimate finding — and do not manufacture a straw alternative to score against it.

Score on the 1-5 favourability scale against the anchors, every score citing the evidence ID it rests on. Same scale and same convention as every other skill in this repository: **higher is always better**, so a cheap-to-run option scores 5 on run burden.

Two rules that decide whether this skill produces architecture or produces a wish:

> **Fit to the estate that exists beats fit to the estate you would prefer.** The most common failure of an architecture document is a clean target that quietly assumes somebody else fixes the thing in the middle. If the recommended option depends on a system being replaced, that is a dependency to state, not an assumption to bury.

> **An architecture the organization cannot operate is not an architecture.** Score `operability` against the team that will hold it after the delivery team has moved on.

Compare the top two against the indifference band (0.3). Inside it, report that the options are too close to separate and apply the tie-breakers in order.

Then record the **significant** decisions — the ones expensive to reverse. A decision that could be changed in a sprint does not belong in the log, and a log of forty entries is a design document, not an architecture.

Background on views is in [`references/architecture-views.md`](./references/architecture-views.md); turning vague non-functional wishes into testable targets is in [`references/quality-attribute-scenarios.md`](./references/quality-attribute-scenarios.md). **Neither is needed to run the method.**

### 6. Deliver

| Artifact | File | For |
|---|---|---|
| Architecture overview | `high-level-architecture--architecture-overview.md` \| `.docx` | The document itself |
| Option assessment | `high-level-architecture--option-assessment.md` \| `.csv` \| `.xlsx` | The arithmetic, open to inspection |
| Decision log | `high-level-architecture--decision-log.md` \| `.csv` \| `.xlsx` | The record that outlives the project |

Markdown templates are in [`assets/`](./assets/). **Produce markdown first**, then the richer format if the host can write files.

**Views go in the document as mermaid fenced blocks plus a sentence of prose each.** Mermaid renders in most hosts and reads as text everywhere else, which keeps the document usable for a user whose tool cannot draw. Every view answers a stated question — a view that answers none is decoration and should be cut.

Write for the audience in `target_audience`. A review board needs enough to approve; a delivery team needs enough to build from; a steering committee needs the first two sections and the risks.

### 7. Verify

**Assumptions register** — numbered, with source and effect. Every derived non-functional target appears here, marked as a proposal.

**Confidence rating** — derived from `verify.confidence_rules`. Derived non-functional targets or unconfirmed touchpoints mean `low`, however complete the document is.

**Sensitivity** — all four targets, in plain sentences with thresholds:

> "At three times the current peak the recommended architecture still holds. At ten times, the shared database becomes the constraint and would have to be separated first."

That sentence is worth more to the delivery team than any diagram in the document.

---

## Standing rules

**No vendor or product names.** Describe building blocks by what they do — a message broker, a managed relational store, an identity provider. A product name makes the architecture unusable at the next organization and forecloses a selection decision that has not been taken.

**Trace every must-have requirement** to the part of the architecture that delivers it. An untraced requirement is one nobody will notice is missing until testing.

**List the risks.** An architecture with no risks recorded has not been examined. Each one gets a mitigation or an explicit acceptance.

**Say what you did not decide.** The "deliberately not decided here" section is what stops a reader assuming the silence means agreement.
