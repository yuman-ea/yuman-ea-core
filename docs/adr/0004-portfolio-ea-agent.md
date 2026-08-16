# ADR-0004 — Ship the portfolio-ea agent

- **Status:** Accepted
- **Date:** 2026-08-16
- **Deciders:** @vishaljavalkar-ai, @rajesh-malviya
- **Supersedes:** ADR-0000 §17 (portfolio-ea deferral), ADR-0002 §4 (in part — portfolio-ea only)
- **Superseded by:** none

> Decision record. Do not edit — supersede with a new ADR if this changes.

---

## Context

ADR-0002 opened the skill contribution surface and left agents gated, on the reasoning that **agent proliferation is a worse failure than skill proliferation** — an agent that answers badly poisons the routing for everything beneath it. New agents require an ADR precisely to create that friction.

The friction worked, and this record is what it produced.

`yea.portfolio.application-rationalization` merged in PR #9: a complete skill, seven phases, four eval cases, weights summing to 1.0, all three mandatory emissions. It declares `owner_agent: portfolio-ea`.

**That agent does not exist**, and the consequences are not cosmetic:

1. **The skill is invisible to conversational invocation.** The orchestrator routes on domain agents' `owns_questions`. Nothing owns portfolio questions, so a user asking *"which applications can we retire?"* reaches nothing — the exact question the skill answers.
2. **The orchestrator actively refuses it.** Its `refuses` block routes that question to `portfolio-ea` with `available: false`. The router correctly declares a gap, and the thing that would fill the gap is already sitting in the repository.
3. **`owner_agent` points at nothing**, which no schema rule catches because the pattern is satisfied by a string.
4. **The skill's own `not_this_skill` block routes to `portfolio-ea`**, so the contributor wrote against an agent they reasonably assumed would exist.

This is the evidence ADR-0000 §17 asked for and never got under the freeze: not an intuition that a domain agent would be useful, but a working method that cannot be reached without one.

## Decision

**Ship `portfolio-ea` as an L1 domain agent.**

It owns application portfolio questions — disposition, duplication, run cost of the estate, and sequencing of portfolio change — and answers them by invoking the declared method, never by improvising one.

Skills are claimed by glob (`yea.portfolio.*`), so future portfolio skills never require editing the agent. That is the same arrangement `technology-ea` uses and the reason a routine contribution has not touched an agent file yet.

### What it owns, and what it must refuse

The boundary that matters is against `technology-ea`, because the two brush along a real seam and CI checks `owns_questions` for overlap (R17).

| The question | Owner |
|---|---|
| Is this technology at end of life? | `technology-ea` |
| Given that it is, do we retire, modernize, or tolerate this application, and when? | `portfolio-ea` |
| What should the replacement be built on? | `technology-ea` |
| Which replacement do we fund first? | `portfolio-ea` |

Stated as a rule: **`technology-ea` reasons about fitness, `portfolio-ea` reasons about disposition and sequence.** A lifecycle finding is an input to a disposition decision, not the decision itself. Both agents declare the crossing in `refuses`.

### What is still gated

`business-ea`, `risk-ea`, and `assurance-ea` remain unshipped and remain behind an ADR each. **This record is not a precedent that a skill entitles its domain to an agent** — it is a decision that *this* skill, already merged and already unreachable, does. A domain with no skills has no equivalent argument, because nothing is broken by its absence.

## Consequences

**Enabling:**

- The rationalization skill becomes reachable conversationally, which is the only invocation mode ADR-0001 says drives adoption.
- **Arbitration becomes exercisable for the first time.** ADR-0000 §3 gives the orchestrator five responsibilities, and *arbitrate* has been dead code with one domain agent. The canonical conflict — technology-ea judging a system architecturally sound while portfolio-ea judges it redundant — can now actually occur, which means the orchestrator's most important behaviour can finally be evaluated rather than asserted.
- Two domains make the seven-phase contract portable across domains in practice, not just in principle.

**Constraining:**

- R17 overlap checking now has three agents and becomes a real check rather than a formality.
- The orchestrator's routing eval needs a portfolio case. A router with two destinations can be wrong in a way a router with one cannot.
- Every future portfolio skill inherits an owner, which lowers the bar to contributing one. That is the intent, and it is also the risk.

**Accepted risk:** two domain agents is where multi-agent systems start answering the same question differently. The mitigations are declarative and already in place — `owns_questions`, `refuses`, `escalates_to`, and R17 — and they are worth nothing unless CI enforces them. If routing conflicts show up before the phase-2 demand signal does, this decision was premature.

## Rejected alternatives

**Leave the skill unowned.** Rejected. It is already merged, and an unreachable skill is worse than an absent one: it consumes review effort, appears in the index, and quietly fails the users who most needed it.

**Give portfolio skills to `technology-ea`.** Rejected, and it is the tempting one because it costs nothing today. It would mean `technology-ea` owning funding, retirement, and sequencing questions — which directly contradicts its own `refuses` block, and would make the one shipped agent the answer to everything. That *is* the agent-bloat failure, arriving through the back door rather than the front.

**Delete the skill until an agent is justified.** Rejected. It inverts the project's own contribution model, and it would tell the first outside contributor that a conforming skill can be removed for a reason they had no way to anticipate.

**Ship `business-ea` and `risk-ea` at the same time, for symmetry.** Rejected. Neither has a skill. ADR-0000 §3 is blunt about it: *an empty agent is worse than a missing one.*

## How this is measured

Whether the orchestrator routes correctly between two domains without either answering out of scope. The routing eval covers the first half; `owns_questions` overlap checking covers the second. If a user gets a different answer depending on which agent picked up the question, this ADR is the thing to revisit.
