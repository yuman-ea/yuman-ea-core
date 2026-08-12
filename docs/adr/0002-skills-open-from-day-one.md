# ADR-0002 — Skills are open from day one

- **Status:** Accepted
- **Date:** 2026-08-12
- **Deciders:** @vishaljavalkar-ai
- **Supersedes:** ADR-0000 §17 (skill clause only), ADR-0000 §13 (phase-1→2 ordering, as it applies to skills)
- **Superseded by:** none

> Decision record. Do not edit — supersede with a new ADR if this changes.

---

## Context

ADR-0000 §17 froze phase 1 to exactly one skill, and gated everything after it on a demand signal: *ten practising architects run build-vs-buy on a real decision and at least two return unprompted.* ADR-0000 §13 put breadth in phase 2, behind that gate.

The reasoning was sound and is worth restating, because this ADR narrows it rather than dismissing it: **the failure mode for a project like this is building all of it before finding out whether anyone wants any of it.** Three half-built domain agents demo worse than one that genuinely works. That remains true.

But the freeze was applied to two things that behave differently:

**Agents** are few, stable, and expensive to get wrong. Every new one adds a routing surface, a boundary to police, and a maintainer conversation. Friction there is the point.

**Skills** are the contribution surface. ADR-0000 §12 is explicit: *"Skills never need an RFC — that's the point."* §1 makes the contributor pool the binding constraint on the whole project. A freeze on skills works directly against both, and it does so in a specific and costly way: **it turns away the contributor who arrives with a method they already use.**

That contributor is not hypothetical and not replaceable. A practising architect with a working high-level-architecture method, or a rationalization rubric they have run for years, is exactly who this project exists to collect from. Telling them to wait for a demand signal on a different skill is asking them to come back later, and they do not come back later.

There is also a measurement problem the freeze conceals. The phase-2 gate asks whether one skill earned repeat use. That answers *"is this method good?"* It does not answer *"does the seven-phase contract hold up across different kinds of EA work?"* — and the second question is the one the architecture actually rests on. A second and third skill of a genuinely different shape test the contract in a way that repeating the first one never will. The high-level-architecture skill has already exercised this: it revealed that the `analyze` block's weighted-criteria requirement fits a design-category skill only when the thing being scored is whole options rather than individual decisions. That is a finding about the spec, and no amount of build-vs-buy usage would have produced it.

---

## Decision

### 1. New skills may be contributed at any time, with no phase gate

The restriction in ADR-0000 §17 on additional skills is lifted. `skills/<domain>/<slug>/` is open. No ADR, no RFC, no demand evidence is required to add one — as ADR-0000 §12 always intended.

### 2. Everything that made a skill trustworthy still binds

Nothing in this ADR relaxes a quality rule. A contributed skill must still:

- implement all seven phases, in order, with the exact key names;
- validate against `spec/skill.schema.json` and pass every `error` rule in `spec/lifecycle.md`;
- emit `assumptions_register`, `confidence_rating`, and `sensitivity_analysis`;
- declare `on_missing` and a confidence penalty for every optional input;
- ship at least three eval cases against `northwind-corp`;
- contain no real enterprise data and no vendor names;
- carry `triggers` strong enough to be found conversationally.

**Removing the scarcity does not remove the bar.** It moves where the bar sits: from *how many skills exist* to *what each one is allowed to claim about itself.*

### 3. Maturity becomes the load-bearing control

The `draft` · `usable` · `proven` · `certified` ladder was already defined in ADR-0000 §12 and `spec/lifecycle.md`. Under the freeze it was decorative, because there was one skill. It is now the primary quality signal and must be treated as such:

- A new skill enters at **`draft`**. It may not self-declare higher.
- **`proven` still requires a real decision**, reported by someone outside the maintainer group. That criterion is unchanged and is not negotiable — it is the only rung that carries evidence of usefulness.
- Maturity is displayed wherever skills are listed. A reader must be able to tell a rough contribution from a tested one at a glance.

This is how a maintainer says yes without endorsing, which is the mechanic that keeps first-time contributors.

### 4. Agents are unchanged

New domain agents still require an ADR. `business-ea`, `portfolio-ea`, and `risk-ea` remain unshipped and remain gated. **Agent proliferation is a different and worse failure than skill proliferation**, because an agent that answers badly poisons the routing for everything beneath it.

### 5. The rest of ADR-0000 §17 stands

Still deferred, still justified only by evidence not yet produced: the CLI, connectors beyond CSV, the artifact renderer, and `registry.json`. Nothing in ADR-0001 changes.

### 6. The demand signal is retained as a measurement

*Ten practising architects run a skill on a real decision, and at least two return unprompted* remains the project's definition of success. It stops being a gate on contribution and becomes what it always should have been for skills: **the criterion for promotion to `proven`, and the measure the project judges itself by.**

---

## Consequences

**Enabling:**

- A contributor arriving with a working method can land it the week they arrive. This is the single largest effect and the reason for the change.
- The seven-phase contract gets tested across categories — `design`, `assess`, `simplify` — rather than validated once. Contract defects surface while the spec is still cheap to change.
- Depth and breadth stop being framed as opposites. They were never actually in tension for skills; they are for agents.

**Constraining:**

- **Review load rises immediately and falls on domain maintainers who do not yet exist.** CODEOWNERS per domain directory, recruited from practising architects, moves from "structural choice" to prerequisite.
- A repository of unpromoted `draft` skills is a real risk to credibility. Volume without promotion is the failure signature to watch for, and it is measurable.
- CI must run on every contributed skill, not on one. Schema validation and eval execution stop being optional infrastructure.

**Accepted risk, stated plainly:** this trades a guarantee of depth for a chance at contribution. If the repository fills with `draft` skills that nobody promotes, this ADR was wrong and should be superseded — not worked around.

---

## Rejected alternatives

**Hold the freeze until the demand test completes.** Rejected. The gate was designed to stop breadth-instead-of-depth, which is a real failure for *agents*. Applied to skills it also blocks the contributor the project depends on, and that cost is certain while the benefit is speculative.

**Cap the skill count — say, five before the gate.** Rejected as arbitrary. A cap creates a queue and a race, and it answers no question that maturity labelling does not answer better.

**Require an ADR per new skill.** Rejected. It directly contradicts ADR-0000 §12, and the friction would land on exactly the contributors the project cannot afford to lose.

**Open agents too, on the same reasoning.** Rejected. The reasoning does not transfer. Skills are additive and independently labelled; an agent changes how every question is routed. ADR-0000 §14's agent-proliferation anti-pattern stands untouched.

**Lift the restriction by editing ADR-0000 §17.** Rejected on principle, and worth recording because it was the obvious move. ADR-0000 §15 and CLAUDE.md's anti-pattern 7 both forbid it: decision records are superseded, never edited, precisely so a contributor in month eight can see that the freeze existed, why it existed, and why it was lifted. Editing it would erase the reasoning that makes this decision reviewable.

---

## Open questions

- **Who reviews at volume?** Domain maintainers recruited from practising architects, per ADR-0000 §12. Unresolved until the first non-maintainer contribution arrives.
- **Does an unpromoted pile of `draft` skills damage credibility more than an empty directory?** Genuinely unknown. Watch the promotion rate; if `draft` count grows while `proven` stays at zero, revisit this ADR rather than adding process.
- **Does the seven-phase contract hold for every category?** The `analyze` block assumes something is being scored. `discover` and `aggregate` skills may not fit. First such contribution decides whether the schema flexes or the category does.

---

## How this is measured

Not by skill count. **By promotion rate: how many skills move from `draft` to `usable` to `proven`, and how quickly.**

A repository with four `proven` skills and six `draft` ones is healthy. One with thirty `draft` skills and none promoted has produced a directory rather than a product, and this decision will have been the wrong one.
