# spec/lifecycle.md — the seven-phase skill contract

**Status:** normative. This document and the JSON schemas beside it are the contract. Where this file and a schema disagree, the schema wins for anything a schema can express; this file is authoritative for the rules a schema cannot express.

Reasoning behind these decisions is frozen in [ADR-0000](../docs/adr/0000-initial-architecture.md) §6 and [ADR-0001](../docs/adr/0001-invocation-and-distribution.md). Do not edit those. Do edit this file when a rule changes.

---

## Why the contract exists

Fifty skills written by fifty people is a directory, not a product. The seven phases are what turn independent contributions into something an architect can trust the same way twice — and what lets an organization override a weight without reading the prose.

One sentence governs the whole thing: **a skill declares what it needs, what it does when it doesn't get it, and how confident that leaves it.** Everything below is that sentence made checkable.

---

## The seven phases

Implemented in this order, under these exact key names in `skill.yaml`. All seven are mandatory. None may be empty.

### 1 `frame` — restate the question

Capture the goal in the user's words and restate it as a precise EA decision statement, **before** any analysis. The restatement is shown to the user so a wrong question can be corrected while it is still cheap.

`restatement_template` interpolates `{placeholders}` that resolve from `ask` and `gather` IDs. `out_of_scope` states what this skill deliberately does not decide — the first defence against a skill quietly growing into a neighbouring one.

### 2 `ask` — only what changes the answer

**Maximum five questions.** The schema enforces the ceiling; review enforces the intent. Each question declares `why` — the sentence explaining what moves in the result depending on the answer. If that sentence cannot be written, the question is curiosity, not method, and belongs in `gather` as an optional input or nowhere.

`ask` is **structured data, never prose**. The same block must render as a chat interview, a web form, or a batch payload with no modification. That is what "framework-agnostic" actually means in practice.

Every required question declares `default_if_skipped`. The primary user is an architect answering on a Thursday afternoon with partial knowledge; a skill that deadlocks on an unanswered question is a skill they abandon.

`affects` lists the criterion IDs an answer moves. It is optional in the schema and expected in review: it is how "only questions that change the answer" stops being an assertion.

### 3 `gather` — inputs, and honest behaviour when they are absent

Two lists, both required, either may be empty.

`required` inputs are those without which the skill genuinely cannot run. Keep the list short. **Every entry is a reason the target user gives up** — the architect with no CMDB, no budget, and partial data.

`optional` inputs each declare:

| Key | Purpose |
|---|---|
| `on_missing` | One of the closed behaviours below |
| `assumption_template` | The sentence written into the assumptions register when the estimating path is taken |
| `confidence_penalty` | How far the overall rating drops — `none` \| `low` \| `medium` \| `high` |

**`on_missing` closed enum:**

| Value | Meaning |
|---|---|
| `ask_user` | Ask once, in line, with a cheap way to say "don't know" |
| `estimate_with_assumption` | Derive a figure and state the derivation |
| `use_proxy_metric` | Substitute a named stand-in (declare `proxy`) |
| `use_default_value` | Apply a declared default (declare `default_value`) |
| `omit_criterion_and_reweight` | Drop the affected criterion and renormalize, reporting both |
| `halt_with_explanation` | Stop and say what is needed and why |

Data is **never silently imputed.** A number that appears in an artifact without a stated source or a stated assumption is the defect this contract exists to prevent.

### 4 `bound` — constraints by ID

`policies` lists **policy IDs only**. A core skill declares which constraints it consults; the overlay says what they mean. Inline constraint text is rejected — an organization cannot override a sentence buried in prose, and a skill that hard-codes "prefer SaaS" is useless at the next company.

The primary user has no overlay. `on_policy_absent` therefore defaults to `proceed_and_note`: run, and record in the assumptions register which constraints were unstated.

`hard_constraints` eliminate options outright rather than adjusting scores. **Elimination is always reported.** An option that vanished without explanation reads as a rigged analysis, and in a steering committee it will be treated as one.

### 5 `analyze` — the method, fully declared

Criteria, weights, scoring scale, ordered steps, tie-breakers. Every one of them addressable by an overlay, none of them buried in prose.

- **Weights sum to 1.0** (R7).
- **Every criterion declares `evidence`** — the `ask` and `gather` IDs that produce its score. A criterion with no evidence path is an opinion with a weight attached (R18).
- **`scoring_scale.anchors` say what each point means in business language.** Anchors are the difference between a score that reproduces run to run and one that doesn't.
- **`tie_breakers` and `indifference_band` are how a close call gets reported as a close call.** Announcing a winner separated by 0.03 is a failure mode, not a result.

Write skills that **constrain, not skills that explain.** The model already knows what TOGAF is. Encode the rubric, the data contract, the artifact schema, and the consistency rules — that is the part that does not decay as models improve.

### 6 `deliver` — named artifacts with defined schemas

Each artifact declares `formats`, and **`md` must be among them** (R11). Hosts differ in whether they can write `.docx` and `.xlsx`; markdown is the floor that makes the deliverable real everywhere (ADR-0001 §4).

`content_schema` is the "defined schema" the phase requires: `columns` for a table, `sections` for a document. It is what lets CI check that a run produced the artifact rather than something artifact-shaped.

At least one artifact is `always: true`. A run must not be able to end with nothing in the user's hands.

**Artifact filenames are derived, never declared:**

```
<skill-slug>--<artifact-id with _ replaced by ->.<ext>
```

`yea.technology.build-vs-buy` + artifact `option_scorecard` + `xlsx` → `build-vs-buy--option-scorecard.xlsx`.

Deliverables explain their reasoning **in business language**. The user takes this to a CFO. Nobody should need to have read a framework to defend the result.

### 7 `verify` — the part that is actually the product

Three emissions are mandatory and CI rejects their absence:

- **`assumptions_register`** — every assumption made, its source, and what it affects.
- **`confidence_rating`** — `low` \| `medium` \| `high`, **derived** from `confidence_rules` against the evidence actually available, not asserted.
- **`sensitivity_analysis`** — what was varied, by how much, and **which conclusions flip**. "The recommendation holds unless the internal cost estimate is more than 30% low" is the sentence that survives a finance review.

A consultancy's real deliverable is a defensible argument. This phase is where that argument is made, which is why it is not optional and not a formatting concern.

---

## Validation rules

CI enforces these. Severity `error` blocks merge; `warn` is raised on the pull request for a human to judge. Numbers are stable — they are cited from the schemas and from `CONTRIBUTING.md`.

| # | Rule | Severity |
|---|---|---|
| R1 | `id`, `slug`, `domain`, and the directory path `skills/<domain>/<slug>/` all agree | error |
| R2 | Name is a noun phrase for the decision or deliverable. Banned suffixes and version numbers are rejected by the schema; gerunds, invented abbreviations, and acronyms outside the allowed list are flagged here | warn |
| R3 | `SKILL.md` frontmatter agrees with `skill.yaml` on name, description, and licence — see [standard-mapping.md](./standard-mapping.md) | error |
| R4 | `ask` has at most five items, each with a `why`; every required item has `default_if_skipped` | error |
| R5 | Every `gather.optional` input declares `on_missing` and `confidence_penalty` | error |
| R6 | `halt_with_explanation` does not appear on an optional input — if absence stops the skill, the input is required | error |
| R7 | `analyze.criteria` weights sum to 1.0 ± 0.001 | error |
| R8 | A partial weight override in an overlay renormalizes the remaining criteria proportionally, and the artifact's method note records that it happened | error |
| R9 | No vendor or product name appears anywhere under `skills/`, `agents/`, `subagents/`, or `spec/`. Overlays and `connectors/` are exempt — that is where product names belong | error |
| R10 | `bound.policies` contains policy IDs only, no inline constraint text | error |
| R11 | Every artifact includes `md` in `formats`, and at least one artifact is `always: true` | error |
| R12 | At least three eval cases in `./evals/`, each with expected outcome, expected confidence, and the assumptions it should surface | error |
| R13 | `verify.emits` contains `assumptions_register`, `confidence_rating`, and `sensitivity_analysis` | error |
| R14 | A skill declaring `data_intensity` above `low` states in `SKILL.md` why it cannot degrade honestly to manual input | error |
| R15 | No real enterprise data. Application inventories, vendor names tied to costs, and customer identifiers are rejected in any file, including examples and test fixtures | error |
| R16 | The orchestrator's eval suite includes the routing case: given a build-vs-buy question, does it invoke the skill or answer from its own head? | error |
| R17 | No two agents' `owns_questions` overlap; every `refuses.route_to` names an agent that exists in this release | error |
| R18 | Every `criterion.evidence` ID resolves to an `ask` ID or a `gather` input ID | error |
| R19 | Every ID in `ask.affects` resolves to a criterion ID | error |
| R20 | A skill directory contains no executable code. Markdown, YAML, JSON, and CSV only | error |
| R21 | A skill removed from a release was `deprecated: true` with a `superseded_by` pointer for at least two prior releases | error |
| R22 | Promotion past `draft` requires `hosts_verified` to name at least two standard-compliant hosts, one of which is the reference host | error |
| R23 | Every skill declares at least four `triggers.phrases` in practitioner language. Weak triggers make a skill invisible and fail review on that basis alone | error |

R9 and R15 are the two that create legal and trust problems simultaneously if they leak. They run on every file in every pull request, not just changed skills.

---

## Skill directory layout

```
skills/<domain>/<slug>/
├── SKILL.md        # the method, prose, for humans and for the host tool
├── skill.yaml      # the contract, structured, for machines
├── assets/         # templates shipped with the skill, incl. markdown artifact forms
├── references/     # background loaded on demand, never upfront
└── evals/          # golden cases, minimum three
```

`SKILL.md` at this path is directly loadable by any Agent Skills standard host with **no build step**. A skill that only works after a transform is a design failure — see [standard-mapping.md](./standard-mapping.md).

Uppercase filename = written for a human. Lowercase = read by a machine.

---

## Maturity

Maturity is how a maintainer says yes without endorsing. It is a badge in the skill index, not a quality gate on merging.

| Level | What it means | To reach it |
|---|---|---|
| `draft` | Schema-valid and honest about its gaps | Passes all `error` rules; three evals; one domain maintainer review |
| `usable` | Produces a defensible artifact on the reference fixture | Evals pass on `northwind-corp`; artifacts reviewed by a practitioner |
| `proven` | Has improved a real decision | Used on a real decision by someone outside the maintainer group, who reports back; verified on a second host (R22) |
| `certified` | Method reviewed by domain practitioners as sound, not merely functional | Two practitioner reviews plus a maintainer sign-off, recorded in the pull request |

Merging a rough contribution at `draft` is preferable to rejecting it or rewriting it yourself. The binding constraint on this project is contributor supply.

---

## Versioning

| Concern | Rule |
|---|---|
| `spec_version` | On every skill, agent, and overlay. Breaking spec changes require an RFC and a major bump |
| Skill version | Semver per skill. **Weight or criteria change → minor. Changed artifact `content_schema` → major.** Wording and reference changes → patch |
| Agent version | Semver. Changing `owns_questions` or `refuses` is minor; changing `layer` or `non_goals` requires an ADR |
| Overlay compatibility | An overlay pins `extends: yuman-ea-core@<major>.<minor>.x`. A major core bump requires the overlay to be revalidated |
| Deprecation | `deprecated: true` plus `superseded_by`, for a minimum of two releases before removal (R21) |
| Release | The repository releases as a set. Distribution is a versioned archive on GitHub Releases (ADR-0001 §3) |

---

## What this spec does not cover yet

Stated so nobody builds them speculatively:

- **`artifact.schema.json`** — artifact structure currently lives inside `deliver.artifacts[].content_schema`. It is promoted to its own schema when a second skill needs to share an artifact definition, and not before.
- **`registry.json`** — the generated skill index. One skill does not need an index.
- **RFC process** (`spec/rfcs/`) — added when the first spec change is proposed by someone outside the maintainer group.

Each is justified by evidence phase 1 has not yet produced.
