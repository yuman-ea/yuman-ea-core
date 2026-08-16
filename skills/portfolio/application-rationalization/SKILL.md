---
name: application-rationalization
description: >
  Determines a defensible disposition for applications in a portfolio — invest,
  maintain, modernize, consolidate, retire, or validate further — using declared
  business, technical, risk, cost, overlap, and change-feasibility criteria. It
  works from manual input or CSV, degrades honestly when evidence is incomplete,
  and produces a scorecard, executive decision memo, roadmap, and decision record
  with assumptions, confidence, and sensitivity analysis.
license: MIT
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.portfolio.application-rationalization
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: portfolio
  yuman_ea_category: simplify
  yuman_ea_owner_agent: portfolio-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---
# Application Rationalization

Decides what to do with applications in a portfolio and produces an argument a steering committee can inspect: **invest, maintain, modernize, consolidate, retire, or validate further**.

The machine-readable method is in [`skill.yaml`](./skill.yaml). That file is authoritative for criteria, weights, missing-data behaviour, artifact schemas, confidence rules, and sensitivity targets. Do not tune the method mid-run because a score feels wrong; use an overlay.

**This skill is deliberately usable with incomplete portfolio data.** A spreadsheet with application name and business purpose is enough to begin screening. Missing evidence lowers confidence and can convert an irreversible recommendation into `needs_validation`; it does not get silently guessed.

## When not to use this

- **The question is build versus buy for a new capability.** Use `yea.technology.build-vs-buy`.
- **The replacement has already been chosen and you need its architecture.** Use `yea.technology.high-level-architecture`.
- **The question is only where to host one application.** That is a technology disposition question, not portfolio rationalization.
- **The question is which investment gets funded first.** Rationalization produces application dispositions; portfolio investment prioritization is a different method.

Say which question it is and stop. A rationalization scorecard used to answer a sourcing or funding question is a polished answer to the wrong decision.

---
## Run it in this order

### 1. Frame

Restate the decision before scoring anything:

> Determine the recommended disposition for applications in **{portfolio_scope}** over a **{decision_horizon}** horizon, optimizing for **{primary_objective}** while protecting business continuity and mandatory obligations.

State the out-of-scope items from `frame.out_of_scope`. In particular, a screening exercise does **not** approve a retirement.

### 2. Ask

Ask only the four questions declared in `skill.yaml`. Do not add a fifth because it would be interesting. The questions set the decision horizon, the dominant outcome, the organization's change appetite, and whether this is candidate screening or decision-ready analysis.

If the user already answered one, confirm it in one line rather than asking again. If an answer is skipped, apply `default_if_skipped` and record it in the assumptions register.

### 3. Gather

Two inputs are required: the **portfolio scope** and an **application inventory** with a stable ID, name, and business purpose. Everything else is optional and has an explicit missing-data behaviour.

A one-file CSV is provided at [`assets/application-rationalization-inputs.csv`](./assets/application-rationalization-inputs.csv). Blank cells are expected. A blank means **unknown**, never zero, safe, cheap, unused, or unimportant.

The highest-value evidence is usually:

1. accountable business-owner view of criticality and replacement coverage;
2. technical lifecycle/supportability and material incidents;
3. dependencies that would block change;
4. validated functional overlap;
5. current security/compliance obligations;
6. comparable run-cost data.

Do not spend the first hour hunting perfect cost data if the business owner cannot yet say what the application does. Work with the evidence that changes the decision first.

### 4. Bound

Apply overlay policies before scoring. Core declares policy IDs but does not decide what they mean at an organization.

A hard constraint can block a disposition without changing the application's scores. That distinction matters. A low-value application may still be **not retireable now** because of retention, continuity, residency, or contract commitments. Report that as a blocked action, not as a mysteriously higher score.

If no overlay is present, proceed and say which constraints were unstated.

### 5. Analyze

Score each criterion on the common 1–5 favourability scale in `skill.yaml`, citing the evidence used. Higher is always better on every criterion.

The seven criteria are:

- business value;
- technical fitness;
- risk posture;
- strategic fit;
- cost efficiency;
- portfolio uniqueness;
- change feasibility.

The weighted score is a **comparison aid, not the disposition**. Rationalization is driven by the pattern across those criteria.

Use [`references/disposition-rules.md`](./references/disposition-rules.md) for the decision rules. The important safety rules are:

- high value + healthy technology usually means **invest**;
- high value + unhealthy technology or risk means **modernize**;
- adequate value + adequate fitness and no decisive change signal means **maintain**;
- confirmed functional duplication with a stronger target may mean **consolidate**;
- low value may mean **retire**, but only after dependencies, obligations, and accountable-owner confirmation are checked;
- insufficient evidence for an irreversible action means **needs_validation**, not a confident guess.

`needs_validation` is not a failure state. It is the correct answer when the analysis knows what it does not know.

#### Never auto-retire from a score

A low score is not permission to decommission. Retirement requires all of the following to be evidenced or explicitly validated:

- the business need is gone or covered elsewhere;
- no hard policy blocks retirement;
- no material dependency still requires the application;
- the accountable owner confirms the disposition, when the run is `decision_ready`.

Without those checks, output `needs_validation` with `retire_candidate` as the proposed action.

#### Never auto-consolidate from semantic similarity

The overlap proxy may identify candidates from similar business-purpose text. It is only a hypothesis generator. Consolidation requires validated overlap and a named target that covers the need at equal or better business coverage and equal or better technical/risk fitness.

### 6. Deliver

Four artifacts are always produced, and all have markdown fallbacks:

| Artifact | File | Purpose |
|---|---|---|
| Application rationalization scorecard | `application-rationalization--application-scorecard.md` / `.csv` / `.xlsx` | Inspectable application-by-application evidence and arithmetic |
| Portfolio decision memo | `application-rationalization--decision-memo.md` / `.docx` | Steering-committee argument in business language |
| Rationalization roadmap | `application-rationalization--rationalization-roadmap.md` / `.csv` / `.xlsx` | Validation and execution sequencing |
| Decision record | `application-rationalization--decision-record.md` / `.csv` | Dated audit trail and review dates |

Produce markdown first. Rich files are an upgrade, not a dependency.

Write the decision memo for people who were not in the analysis. Do not lead with framework vocabulary. Lead with what can change, what value or risk it addresses, what evidence supports it, and what still needs confirmation.

### 7. Verify

Verification is part of the product, not a footnote.

**Assumptions register** — every missing-data path, proxy, default, and policy gap appears here with the part of the decision it affects.

**Confidence rating** — derived from the rules in `skill.yaml`. Never promote a result because the narrative sounds persuasive.

**Sensitivity analysis** — vary business value, technical fitness, cost, uniqueness, and change feasibility exactly as declared. Report which dispositions or roadmap waves change.

**Data-quality note** — state how much of the portfolio had current owner, technical, dependency, overlap, risk, and cost evidence. A portfolio-wide percentage is more useful than a vague sentence saying "data quality was mixed."

**Dissent note** — where a business owner, technical owner, or policy source disagrees with the calculated disposition, preserve the disagreement rather than averaging it away. The steering committee needs to see the conflict.

---
## Standing rules

- No vendor names in the method. User-supplied application names are data and may appear in outputs.
- Never treat a blank as zero, no risk, no dependency, or no usage.
- Never claim cost savings when comparable cost evidence was omitted.
- Never turn a semantic-overlap hypothesis into a consolidation decision without validation.
- Never issue an execution-ready retire or consolidate decision without the evidence posture required by the run.
- Every disposition travels with its evidence, assumptions, confidence, and next validating action.
