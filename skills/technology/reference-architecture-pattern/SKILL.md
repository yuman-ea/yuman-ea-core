---
name: reference-architecture-pattern
description: >
  Decides whether a proposed reference pattern is actually a pattern, and publishes it if it
  is. Scores the candidate against declared criteria — how many real implementations it
  generalizes from, whether it constrains anything, whether its limits are stated, and what
  it costs to adopt — then sets a status of mandated, recommended, proposed, or not yet a
  pattern. Produces the pattern definition, the readiness assessment behind it, and a
  decision record. Works from manual input; no modelling tool required.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.technology.reference-architecture-pattern
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: technology
  yuman_ea_category: design
  yuman_ea_owner_agent: technology-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Reference Architecture Pattern

Authors a reusable pattern the organization will apply to many future solutions — **and refuses to author one when the evidence does not support it.**

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The question this actually answers

Not *"is this a good design?"* — it may well be. The question is **"does this deserve to be reused, and may it be published?"**

Those are different, and conflating them is how pattern catalogues fill with documents nobody applies. An architect asking for a pattern usually wants one. **This skill must be willing to answer: you have an implementation, not a pattern.**

## When not to use this

| The question | Use |
|---|---|
| What should the architecture of *this* solution be? | [`high-level-architecture`](../high-level-architecture/SKILL.md) |
| Why did we choose *this* option, once? | [`architecture-decision-record`](../architecture-decision-record/SKILL.md) |
| Build, buy, or partner? | [`build-vs-buy`](../build-vs-buy/SKILL.md) |
| Which applications do we keep or retire? | [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) |

A pattern **pre-makes a class of decisions** ahead of time; an ADR records one, after. If you are deciding rather than generalizing, you are in the wrong skill.

---

## One implementation is not a pattern

The rule the whole method turns on:

| Implementations it generalizes from | What it is |
|---|---|
| **Three or more** | Can be `mandated` |
| **Two** | Can be `recommended` — you have generalized something |
| **One** | An implementation. Publish it as a worked example, not a pattern |
| **None** | A proposal. It may be a good one, and it is still not a pattern |

Two systems that differ only in name are **one** implementation. So are two built by the same team in the same quarter from the same starting point — they share the assumptions that have not been tested yet.

**External practice is evidence, not proof.** Something well established elsewhere may be entirely right for you and still fail here for reasons nobody outside your estate could know. It can reach `proposed` on reputation. It reaches `recommended` when you have run it.

---

## Run it in this order

### 1. Frame

Restate what is being assessed, and check the problem statement is a **problem** — not a solution and not a technology:

> Determine whether **{problem_statement}** is served by a reusable pattern, assess **{candidate_shape}** against the evidence in **{known_implementations}**, and set a publication status for use at **{scope_breadth}** scope.

A pattern named after a technology is a preference with a diagram attached. If the problem statement cannot be written without naming the solution, that is the finding.

### 2. Ask

Five questions, in `skill.yaml`. The two that carry most weight:

- **`pattern_origin`** — whether the evidence is yours or someone else's.
- **`intended_authority`** — anything teams are *held to* needs testable conformance criteria. Guidance can be loose; a mandate cannot.

### 3. Gather

Three required inputs: the **problem**, the **candidate shape**, and the **known implementations**.

> **"None" is a valid answer to `known_implementations`, and it is not a gap to fill.** It changes the outcome. Record it and continue — do not go looking for systems that sort of resemble the pattern in order to reach a count.

`nonfunctional_position` carries a **high** confidence penalty when absent. A pattern with no stated operating envelope gets applied where it does not fit, and the team that finds out is the one whose system fell over.

### 4. Bound

Apply hard constraints before scoring. **A pattern that cannot satisfy the security baseline or data residency cannot be `mandated` regardless of its score** — record it as *blocked*, with the policy ID, never as a quietly lower status. A reader who sees `recommended` and does not know it was capped will assume it was judged rather than blocked.

### 5. Analyze

Seven criteria, 1-5 favourability, higher always better. **The weighted score is a comparison aid — it is not the status.** The score pattern produces the status, via [`references/pattern-readiness.md`](./references/pattern-readiness.md).

| Status | Meaning |
|---|---|
| `mandated` | Solutions in scope must use it; deviation needs a waiver |
| `recommended` | The default; deviation needs a recorded reason |
| `proposed` | The shape is sound, the evidence is thin. Published as a candidate, naming what would promote it |
| `not_yet_a_pattern` | It is a design or a decision. Say which, name the skill that owns it, and stop |

**When the status is `not_yet_a_pattern`, do not write a pattern definition.** Producing a polished pattern document for something that is one system's design is worse than producing nothing, because it will be cited.

Four rules that decide whether this produces a pattern or a diagram:

> **It must say what NOT to do.** A pattern that forbids nothing constrains nothing.

> **The anti-scope is mandatory.** Where does this not apply, and what should a team do instead there? Patterns are discredited by misapplication far more often than by being wrong.

> **Conformance must be checkable by someone who did not write it.** "Services should be loosely coupled" cannot govern anything. If a criterion cannot be checked, rewrite it or drop it.

> **Name the decisions it pre-makes.** That list *is* the value proposition — it should read as the decision records nobody has to write again.

### 6. Deliver

| Artifact | File |
|---|---|
| Pattern definition | `reference-architecture-pattern--pattern-definition.md` \| `.docx` |
| Readiness assessment | `reference-architecture-pattern--readiness-assessment.md` \| `.csv` \| `.xlsx` |
| Decision record | `reference-architecture-pattern--decision-record.md` |

Markdown preferred throughout — a pattern's natural home is the organization's own repository or wiki, next to what it governs, where it is diffable and dated by history rather than by a field somebody forgot to update.

**Every pattern carries an owner and a review date.** An unowned pattern rots into something people cite that no longer reflects how anything is built, and nobody notices until it is quoted in a review.

### 7. Verify

**Confidence** is derived, and it is unforgiving here for a reason: a pattern document is very easy to write well and very hard to earn. Fewer than two implementations, or a derived operating envelope, or an uncheckable conformance criterion, means `low` — however good the document looks.

**Sensitivity** includes the test specific to this method:

> **Remove the most-cited implementation. Does the pattern still generalize?** If it collapses, it was always one system's design with the others cited for support. This is the single most revealing check in the skill.

---

## Standing rules

**No vendor or product names in the pattern.** Describe parts by what they do — a message broker, a managed relational store, an identity provider. A pattern naming products expires with the procurement cycle and cannot be adopted by anyone else.

**Record how it has gone wrong.** A pattern with no failure modes listed has not been used enough to publish.

**Prefer the lower status when it is close.** Publishing as `recommended` something that should have been `proposed` costs more than the reverse, because teams build on it before it has earned that.
