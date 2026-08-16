---
name: architecture-decision-record
description: >
  Decides between two or more technology options and records why — the context that forced
  the decision, the alternatives considered, the reasoning, the consequences accepted, and
  what would make the organization revisit it. Scores the options against declared criteria
  and rates its own confidence lower when only two options existed, or when the reasoning
  rests on judgement rather than evidence. Works from manual input; no tooling required.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.technology.architecture-decision-record
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: technology
  yuman_ea_category: assess
  yuman_ea_owner_agent: technology-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Architecture Decision Record

Decides between technology options and records why — so that in two years someone can read the record, disagree with it, and know exactly what they are disagreeing with.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

**This is the general method.** Where a specialised skill owns the decision, use that one instead:

| The question is | Use |
|---|---|
| Build, buy, or partner? | [`build-vs-buy`](../build-vs-buy/SKILL.md) — it emits its own decision record |
| What should the whole solution look like? | [`high-level-architecture`](../high-level-architecture/SKILL.md) — it emits its own decision log |
| Everything else — a pattern, a format, a boundary, a deviation from standard | **This skill** |

## Three options is the working practice. Two is acceptable. One is not a decision.

This is the rule the skill exists to hold you to, and it is enforced through the confidence rating rather than by refusing to run:

| Options assessed | What happens |
|---|---|
| **Three or more**, genuinely different | Can reach `high` confidence |
| **Two** | Capped at `medium`, **and the record must state why a third was not available** |
| **One** | Not a decision. See below |

Two options that differ only in a component name are **one** option, and scoring them is theatre.

**When only one option exists, do not manufacture alternatives.** Say plainly that this is a *rationale record* rather than a decision, record why the others were not viable, and rate the run `low`. A retrofitted straw man — two obviously bad alternatives written after the fact to make a settled choice look considered — is the most common defect in a written decision record, and every experienced reviewer recognises it on sight. It damages the credibility of the decision it was meant to protect.

**Deferring is an option.** Where the urgency answer allows it, keeping the choice open is a legitimate architectural act and belongs in the option list. Recording that you *could* have waited and chose not to is more useful than pretending the decision was forced.

---

## Run it in this order

### 1. Frame

Restate the decision and confirm the **subject is narrow enough** that a future reader can tell whether their decision is the same question or a different one:

> Decide between **{options_considered}** for **{decision_subject}**, at **{decision_scope}** scope, given that the choice is **{decision_reversibility}**, and record the reasoning.

A record titled "Data architecture" will be cited for twenty unrelated things. One titled "Where order state is held between capture and fulfilment" will be cited for the decision it actually made.

### 2. Ask

Five questions, in `skill.yaml`. The two doing most of the work:

- **Reversibility** sets how much rigour the decision deserves. Applying irreversible-decision rigour to a two-way door wastes effort; applying two-way-door rigour to a one-way door accepts real risk.
- **Existing precedent** is usually why an ADR is being written at all. A deviation from standard needs a stated argument, not a silent departure.

### 3. Gather

Three required inputs — **subject**, **options**, **context** — all held by whoever is making the decision.

Six optional inputs declare what happens when absent. The one that matters:

> **`evidence_available` carries a `high` confidence penalty.** It asks what was actually tried — a spike, a benchmark, direct prior experience. When nothing was, the record says so, and the sensitivity analysis re-runs the comparison with every judgement-based score marked down a point. This is the cheapest weakness in any ADR to fix: one afternoon's spike usually moves the rating.

### 4. Bound

Apply policies as an overlay supplies them; with no overlay, proceed and record which were unstated. **Apply hard constraints before scoring** and record every eliminated option with the policy ID that removed it. An option that vanishes without explanation reads as a rigged record.

### 5. Analyze

Seven criteria, scored 1-5, weights in `skill.yaml`. Scores express **favourability** — higher is always better, so a cheap-to-run option scores 5 on run burden.

Every score cites the evidence ID it rests on, and is marked `measured` or `judged`. **That column is what separates a decision record from a well-argued opinion**, and it is the first thing a reviewer should look at.

Two rules that decide whether this produces a record or a justification:

> **Fit to the estate that exists beats fit to the estate you would prefer.** If an option only works once something else is fixed, that is a dependency to state, not an assumption to bury.

> **Score the options honestly, not toward the answer.** The characteristic failure is scoring the last two criteria to make the total match a conclusion already reached. The sensitivity analysis exists partly to catch this.

Inside the indifference band (0.3), report the options as too close to separate and apply the tie-breakers in order. **A recorded tie is more useful than an invented winner.**

Background on generating genuinely different options is in [`references/finding-real-options.md`](./references/finding-real-options.md); status, numbering, and supersession are in [`references/status-and-supersession.md`](./references/status-and-supersession.md). Neither is needed to run the method.

### 6. Deliver

| Artifact | File |
|---|---|
| Decision record | `architecture-decision-record--decision-record.md` \| `.docx` |
| Option comparison | `architecture-decision-record--option-comparison.md` \| `.csv` \| `.xlsx` |

Markdown first, always — an ADR's natural home is a repository, and markdown is what belongs there.

**Never edit an earlier record.** If this decision changes a previous one, mark the previous one superseded and link both ways. The reasoning trail is what stops a settled argument being reopened from scratch in month eight, and editing it away destroys the only thing a decision log is for.

**Write a revisit trigger that names an observable event.** "If circumstances change" is not a trigger. "If peak intake passes 5,000 messages an hour" is.

### 7. Verify

**Assumptions register** — numbered, with source and effect.

**Confidence rating** — derived from `verify.confidence_rules`. Two options caps you at `medium` however clean the reasoning; nothing measured caps you lower still.

**Sensitivity** — four targets, of which one is specific to this method and unusually revealing:

> **Remove the recommended option entirely. What happens?** If the runner-up is nearly as good, the decision matters less than the meeting suggested, and the record should say so. If the runner-up is far worse, this choice is load-bearing and deserves the scrutiny.

---

## Standing rules

**No vendor or product names.** Describe options by what they do — a message broker, a managed relational store, an event log. A record naming products is unusable at the next organization and pre-empts a selection decision that has not been taken.

**Write for someone who was not there.** Not for the people in the room, who already agree.

**Record what you are giving up.** The consequences section is half about what the decision closes off, and that half is what a future reader will care about most.
