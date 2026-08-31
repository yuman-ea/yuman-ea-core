# ADR-0005 — Ship the business-ea agent

- **Status:** Accepted
- **Date:** 2026-08-28
- **Deciders:** @vishaljavalkar-ai, @rajesh-malviya
- **Supersedes:** ADR-0000 §17 (business-ea deferral), ADR-0002 §4 (in part — business-ea only)
- **Superseded by:** none

> Decision record. Do not edit — supersede with a new ADR if this changes.

---

## Context

ADR-0004 shipped `portfolio-ea` and was explicit that it set no precedent: *"a skill does not entitle its domain to an agent."* It shipped because a merged skill was unreachable without one — evidence, not intuition.

`business-ea` has no such argument available, because it has no merged skills. So this record has to make a different one, and it should be judged on whether that argument holds rather than on symmetry with ADR-0004.

Three facts frame it.

**1. Both shipped agents already refuse business questions into a void.** `technology-ea` and `portfolio-ea` each carry a `refuses` entry routing *"What business capability is this, and what value stream does it serve?"* to `business-ea` with `available: false`, and the orchestrator carries the same. Three of three shipped agents declare the same gap. That is not a coincidence of drafting: capability and value-stream questions are the ones the other two domains keep bouncing, because their own methods take a capability model as an **input**.

**2. The input nothing produces.** `application-rationalization` reads `context.capability_model` to find duplication. `roadmap-sequencing` reads `capability_targets` and says plainly that without them the plan *"optimizes for delivery convenience, which produces a defensible order that builds nothing in particular."* `build-vs-buy` asks whether a capability is differentiating before it will recommend building. Every one of those degrades on an asset **no skill in this repository produces**. The fixture ships a capability model because the skills need one; nothing in the framework can construct one for an organization that lacks it.

**3. Nine skills arrive at once, not one.** This is the material difference from ADR-0004 and the reason the ADR-0002 bar is doing real work here. Nine skills covering capability modelling, value streams, operating model, maturity gaps, process modelling, stakeholder concerns, business cases, journey-to-system mapping, and acquisition integration is a domain's worth of method, contributed together. Assigning them to `technology-ea` or `portfolio-ea` would put capability definition inside an agent whose own contract refuses it.

## Decision

**Ship `business-ea` as an L1 domain agent**, and merge the nine skills into `skills/business/` at `maturity: draft`.

It owns business architecture questions — what the organization does, how value reaches the customer, how the organization is arranged to deliver it, where capability falls short of what strategy requires, and whether an investment stands up as a case — and answers them by invoking the declared method, never by improvising one.

Skills are claimed by glob (`yea.business.*`), the same arrangement the other two L1 agents use, so future business skills never require editing the agent.

### The seams it must hold

Three agents is where a multi-agent system starts answering one question three ways. R17 checks `owns_questions` for overlap; these are the seams that check cannot see.

| The question | Owner | Why |
|---|---|---|
| What capability is this, and how mature is it? | `business-ea` | The definition, not the systems under it |
| Which applications support that capability, and which do we retire? | `portfolio-ea` | Disposition is portfolio's, always |
| Should we build or buy the capability? | `technology-ea` | Sourcing is technology's, always |
| Does this investment stand up as a case? | `business-ea` | The argument for one investment |
| Which investment do we fund first? | `portfolio-ea` | Comparison across the portfolio |
| In an acquisition, what must work on day one? | `business-ea` | Capability and continuity |
| In an acquisition, which of the two order systems survives? | `portfolio-ea` | An application disposition wearing a merger hat |

Stated as a rule: **`business-ea` reasons about capability and value; `portfolio-ea` reasons about disposition and sequence; `technology-ea` reasons about fitness and sourcing.**

The last two rows are the seam most likely to fail, because an acquisition genuinely spans them. `acquisition-integration-blueprint` therefore decides consolidation at the **capability** level and routes every application-level disposition to `application-rationalization` and every sequencing question to `roadmap-sequencing`, by ID, in its `not_this_skill` block.

### What is still gated

`risk-ea` and `assurance-ea` remain unshipped and remain behind an ADR each. Neither has a skill, and ADR-0000 §3 remains blunt: **an empty agent is worse than a missing one.**

## Consequences

**Enabling:**

- The capability model becomes something the framework can **produce** rather than only consume. Three existing skills stop degrading on an asset nothing supplied.
- The `available: false` entries in three agents' `refuses` blocks become live routes. A declared gap closes rather than being restated.
- The orchestrator gains a third destination, which is where its `classify_intent` responsibility starts being genuinely tested. Two destinations can be separated by vocabulary; three cannot.

**Constraining:**

- **R17 overlap checking now runs across three agents**, and the business/portfolio seam is narrower than the technology/portfolio one. "Which capability should we invest in" and "which investment do we fund first" are one careless rephrasing apart.
- The orchestrator's routing eval needs a business case, and — more importantly — a case that is *deliberately* ambiguous between business and portfolio, so that escalation rather than a coin-flip is what gets evaluated.
- Nine skills at `draft` in one domain moves the project's ratio sharply toward the failure ADR-0002 named: *"Thirty draft and none promoted is a directory, not a product."* This ADR accepts that risk and states the countermeasure below.

**Accepted risk — and it is the real one:** nine skills merged together have had nine times less scrutiny per skill than one merged alone. The mitigation is that every quality rule still binds individually — seven phases, R7 weights, three evals each, all three `verify` emissions, `on_missing` on every optional input — and that none may self-declare above `draft`. If the business domain accumulates `draft` skills without a single promotion while other domains promote, that is the signal this decision was volume rather than value.

## Rejected alternatives

**Defer the agent and merge the skills unowned.** Rejected on ADR-0004's own reasoning: an unreachable skill is worse than an absent one, and this would create nine of them at once.

**Merge one skill now, the agent later, the rest after.** Rejected, though it is the most conservative option and was genuinely arguable. The nine are interdependent as a set — `capability-gap-assessment` consumes the capability model, `operating-model-design` consumes both the model and the value streams, `acquisition-integration-blueprint` consumes nearly all of them. Merging one produces a skill whose most important input still has no producer, which is the exact condition this ADR exists to end.

**Name the agent `business-architect`.** Rejected. The naming table in `CLAUDE.md` fixes L1 agents at `<domain>-ea` and `agent.schema.json` enforces it as a pattern; `display_name: Business architecture` carries the friendlier label. Alias creep is anti-pattern 5, and an agent ID is the worst place to start one because every `refuses.route_to` already in the repository names `business-ea`.

**Give the business skills to `technology-ea`.** Rejected for the same reason ADR-0004 rejected giving it the portfolio skills, and more sharply: `technology-ea`'s own `refuses` block explicitly routes capability definition away. An agent that refuses a question in its contract and answers it in practice is worse than one that does neither.

## How this is measured

Whether the orchestrator routes cleanly between three domains, and whether a capability model produced by `business-capability-map` is actually consumed by `application-rationalization` and `roadmap-sequencing` on the same fixture without manual reshaping. If the two models do not fit together, the domain seam is wrong regardless of how the routing behaves.

The promotion test is unchanged and applies per skill: a real decision, reported by someone outside the maintainer group.
