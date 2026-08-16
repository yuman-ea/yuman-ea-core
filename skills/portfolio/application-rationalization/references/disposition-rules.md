# Disposition rules

This reference constrains **how the score pattern becomes a disposition**. The weighted score is not itself the answer.

## Invest

Use when business value and strategic fit are favourable, technical fitness and risk posture are favourable, and there is no validated overlap indicating that another application should become the strategic target.

The action must say what to invest in: capacity, feature enablement, resilience, data quality, user experience, or another evidenced outcome. "Keep" is not an investment thesis.

## Maintain

Use when the application is fit enough for the decision horizon, business value is real but not demanding further investment, and no strong retire, consolidate, or modernize signal is present.

Maintain is deliberate. Name the review trigger: contract event, support deadline, material cost change, capability consolidation, or strategic change.

## Modernize

Use when business value is favourable but technical fitness or risk posture is unfavourable. State the evidenced problem: lifecycle, maintainability, resilience, performance, security, compliance, or operational burden.

Modernize describes the portfolio decision, not the technical solution. Do not smuggle rehost/replatform/refactor choices into this skill.

## Consolidate

Use only when all are true:

1. portfolio uniqueness is unfavourable because functional overlap is validated;
2. a named target application covers the same business need;
3. the target has equal or better business coverage;
4. the target has equal or better technical and risk fitness;
5. dependencies and contractual constraints do not block the move;
6. accountable owner evidence meets the run's evidence posture.

If overlap came only from semantic similarity, output `needs_validation` and `consolidate_candidate`.

## Retire

Use only when all are true:

1. business value is unfavourable or the need is confirmed as no longer required;
2. no hard policy blocks retirement;
3. no material dependency still requires the application;
4. replacement coverage is confirmed where the need continues;
5. accountable owner evidence meets the run's evidence posture.

If any of 2–5 is unknown, output `needs_validation` and `retire_candidate` rather than `retire`.

## Needs validation

Use when the likely direction is visible but evidence is insufficient for a defensible irreversible decision, or when a hard conflict exists between owner evidence and the scorecard.

Always name:

- the proposed action;
- the missing or conflicting evidence;
- the single next validation step most likely to resolve it;
- the consequence of making the wrong decision.

## Close calls

Where multiple dispositions are genuinely plausible, prefer the more reversible action and let the sensitivity analysis show what would change the answer. False certainty is worse than an explicit validation step.
