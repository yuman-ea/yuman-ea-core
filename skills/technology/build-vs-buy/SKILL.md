---
name: build-vs-buy
description: >
  Decides whether to build, buy, or partner for a business capability. Scores the
  realistic options against declared, overridable criteria and produces a scorecard,
  a recommendation memo a non-specialist can defend, and a decision record — each
  stating its assumptions, its confidence, and what would change the answer. Works
  from manual input and CSV; no portfolio tooling required.
license: MIT
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.technology.build-vs-buy
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: technology
  yuman_ea_category: design
  yuman_ea_owner_agent: technology-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Build vs Buy Evaluation

Decides whether to **build**, **buy**, or **partner** for a business capability, and produces an argument that survives a room full of people who were not part of the analysis.

The machine-readable contract — every weight, threshold, and missing-data behaviour — is in [`skill.yaml`](./skill.yaml). Change weights there or through an overlay, never in the middle of a run.

**You can run this with nothing but the answers in the user's head.** No CMDB, no portfolio tool, no cost model. That is the design point, not a limitation: the analysis degrades to a lower confidence rating rather than refusing to start.

## When not to use this

- **A product has already been chosen and you are comparing two of them.** That is vendor evaluation, and this skill will not do it well.
- **The question is whether to fund the capability at all.** Different decision, different owner.
- **An application already exists and the question is whether to keep it.** That is rationalization, not sourcing.

Say which of these it is and stop. Stretching this method to cover them produces a confident answer to a question nobody asked.

---

## Run it in this order

### 1. Frame

Restate the request as a decision statement and **show it to the user before doing anything else**:

> Determine whether to build, buy, or partner for **{capability}**, optimizing for **{primary_driver}** over a **{decision_horizon}** horizon, evaluated across **{candidate_options}**.

Then state what this run will not decide (`frame.out_of_scope`). A wrong frame caught here costs a sentence. Caught after the scorecard, it costs the user's confidence in the whole thing.

### 2. Ask

Five questions, in `skill.yaml`. **Ask no more than these five**, and ask them in the user's language, not the framework's.

Answers that are already obvious from the conversation are not re-asked — confirm them in one line and move on. If the user declines a question, apply its `default_if_skipped`, say which default you applied, and note it in the assumptions register.

### 3. Gather

Three required inputs: the **capability**, the **candidate options**, and the **must-have requirements**. All three come from the user; none require a system.

Six optional inputs each declare what happens when they are absent. **Apply the declared behaviour and write the assumption down before any score depends on it.** The order matters — an assumption recorded after the fact is a justification, not an assumption.

Never silently impute a number. A figure in an artifact with no source and no assumption behind it is the specific defect this method exists to prevent.

Where the owning agent can supply an input from a context slice, use it and say which slice it came from. A looked-up value and a guess must never look the same in the register.

A user who prefers to prepare offline can fill in [`assets/option-inputs.csv`](./assets/option-inputs.csv) and hand it over instead. **Blank cells are expected** — the template exists so that what is unknown is stated as unknown rather than left out.

### 4. Bound

Apply the policies named in `bound.policies` **as an overlay supplies them**. Core does not know what "cloud first" means at this organization, and must not assume.

Where no overlay is present — the normal case for an individual architect — proceed and record which constraints were unstated. Ask the user directly if one plausibly eliminates an option; do not invent one.

**Apply hard constraints before scoring**, and record every eliminated option with the policy ID that eliminated it. An option that disappears without explanation reads as a rigged analysis, and in front of a steering committee it will be treated as one.

### 5. Analyze

Weighted multi-criteria across seven criteria, weights in `skill.yaml`, scored 1-5.

**Scores express favourability, never magnitude.** A cheap option scores 5 on five-year cost, not its cost in dollars. Every criterion is `higher_is_better` for this reason — mixing conventions produces a scorecard nobody can read.

Score against the anchors, not against a feeling:

| | |
|---|---|
| **5** | Best outcome realistically available on this criterion |
| **4** | Clear advantage a reviewer would recognize without explanation |
| **3** | No real advantage either way, or advantages that cancel |
| **2** | Material disadvantage the organization must accept and manage |
| **1** | Grounds on its own to reject the option |

**Every score cites the evidence ID it rests on.** "Scored 2 on time to value because `talent_reality` is `could_hire` and the must-have list contains eleven items" is a score a reviewer can argue with. "Scored 2 on time to value" is an assertion.

Follow `analyze.steps` in order. The step people skip is the seventh:

> **Compare the top two scores against the indifference band (0.3).** Inside the band, the honest output is *"these two are too close to separate on this evidence"* followed by the tie-breakers in order — not a winner.

Announcing a winner separated by 0.04 is false precision, and the first person to recompute it in a spreadsheet will notice.

Deeper guidance on scoring each criterion is in [`references/sourcing-criteria.md`](./references/sourcing-criteria.md); cost modelling from partial data is in [`references/cost-model-notes.md`](./references/cost-model-notes.md). **Neither is required to run the method** — load them when a score is genuinely contested.

### 6. Deliver

Three artifacts, all `always: true`, all available as markdown:

| Artifact | File | What it is for |
|---|---|---|
| Option scorecard | `build-vs-buy--option-scorecard.md` \| `.csv` \| `.xlsx` | The arithmetic, open to inspection |
| Recommendation memo | `build-vs-buy--recommendation-memo.md` \| `.docx` | The argument, for people who were not in the room |
| Decision record | `build-vs-buy--decision-record.md` | The dated record, for the organization's repository |

Markdown templates are in [`assets/`](./assets/). **Produce the markdown form first**, then the richer format if the host can write files. A user who ends a session with nothing they can paste into an email has received nothing.

Write the memo for a CFO. No framework vocabulary, no criterion IDs in prose, no "TOGAF" anywhere. If a sentence needs a glossary, rewrite it.

### 7. Verify

Not a summary. This is a large part of what the user is actually taking away.

**Assumptions register** — numbered, each with its source and what it affects. Every `on_missing` path taken appears here.

**Confidence rating** — *derived* from `verify.confidence_rules` against the evidence actually used. Never asserted, and never raised because the conclusion feels right. Both cost inputs estimated means `low`, however clean the scorecard looks.

**Sensitivity analysis** — run all four declared targets and report in plain sentences with thresholds:

> "The recommendation holds unless the internal build estimate is more than 35% low. At that point buying and building are indistinguishable."

That is the sentence that survives a finance review. "Sensitivity analysis was performed" is not.

---

## Standing rules

**No vendor names.** Not in the skill, not in the artifacts unless the user supplied them as candidate options. Options are described by type — a commercial platform, a managed service — so this analysis is reusable at the next organization.

**Three options minimum where honest.** Build-versus-buy is a false binary in most cases. If a managed or hosted arrangement realistically exists, evaluate it. A split option — build the differentiating part, buy the rest — is frequently the correct answer and is invisible to a two-column comparison.

**Costs are ranges when estimated.** A single number implies a precision the evidence does not support, and it is the number that gets quoted back six months later.

**Confidence travels with the recommendation.** Including when the user asks for "just the answer".
