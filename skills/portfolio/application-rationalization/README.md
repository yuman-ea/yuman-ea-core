# Application Rationalization skill

**ID:** `yea.portfolio.application-rationalization`  
**Domain:** Portfolio Management  
**Maturity:** `draft`

## Purpose

Assess an application portfolio and recommend one primary disposition per application: `invest`, `maintain`, `modernize`, `consolidate`, `retire`, or `needs_validation`.

## Inputs

Minimum: portfolio scope plus an application list containing stable ID, name, and business purpose. Optional business, technical, risk, cost, dependency, overlap, contract, and owner evidence improves confidence.

Use [`assets/application-rationalization-inputs.csv`](./assets/application-rationalization-inputs.csv) for offline preparation.

## Outputs

- application scorecard;
- steering-committee decision memo;
- rationalization roadmap;
- dated decision record;
- assumptions register, confidence rating, sensitivity analysis, data-quality note, and dissent note.

## Example invocation

> Rationalize these 35 applications. I need to identify retirement and consolidation candidates for the next 18 months, but do not recommend anything that could disrupt customer operations without calling out the dependency risk.

## Repository note

This is a **skill**, not a new L1 agent. The repository's standing architecture explicitly classifies application rationalization as a portfolio skill. `owner_agent: portfolio-ea` is the canonical ownership target; the portfolio agent is currently gated/deferred and requires its own ADR before it is added.
