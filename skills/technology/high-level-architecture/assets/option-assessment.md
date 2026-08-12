# High level architecture — option assessment

**Solution:** {solution_intent}
**Scope:** {single application | multi-system solution | capability domain}
**Dominant quality attribute:** {…} · **Estate position:** {…} · **Delivery and run model:** {…}
**Date:** {YYYY-MM-DD} · **Confidence:** {low | medium | high} — {reason}

> Scores are **favourability on a 1-5 scale**, not magnitude. An option that is cheap to
> run scores high on ongoing cost; an option that carries heavy integration effort scores
> low on fit with what already exists.

## Summary

| Option | Weighted score | Verdict |
|---|---|---|
| {opt-1} | {0.00} | {recommended \| viable \| eliminated} |

**Gap between the top two:** {0.00} — indifference band is 0.30.
{State explicitly whether the gap is inside or outside the band. Inside it, no single
option is recommended and the tie-breakers below apply.}

## Options eliminated before scoring

| Option | Eliminated by | What the constraint says |
|---|---|---|
| {opt-n} | {policy_id} | {…} |

*State "None" explicitly if no option was eliminated. Silent elimination is not permitted.*

## Scores

| Option | Criterion | Score | Weight | Weighted | Evidence | Assumption | Score confidence |
|---|---|---|---|---|---|---|---|
| {opt-1} | requirements_fit | {1-5} | 0.20 | {0.00} | {evidence_id: the specific fact} | {A1, or blank} | {low \| medium \| high} |
| {opt-1} | nonfunctional_fit | | 0.20 | | | | |
| {opt-1} | estate_coherence | | 0.15 | | | | |
| {opt-1} | delivery_feasibility | | 0.15 | | | | |
| {opt-1} | operability | | 0.10 | | | | |
| {opt-1} | security_and_data_protection | | 0.10 | | | | |
| {opt-1} | change_tolerance | | 0.05 | | | | |
| {opt-1} | cost_and_run_burden | | 0.05 | | | | |

**Evidence** names the input the score rests on and the fact taken from it, not a
restatement of the criterion. **Assumption** is blank where the score rests on data the
user supplied.

**Scores resting on a derived non-functional target carry `score_confidence: low`**,
whatever the score itself is. That column is how a reviewer tells a measured judgement
from a proposed one.

## Weights used

| Criterion | Default | Used | Changed by |
|---|---|---|---|
| requirements_fit | 0.20 | {0.00} | {overlay \| renormalization \| unchanged} |
| nonfunctional_fit | 0.20 | | |
| estate_coherence | 0.15 | | |
| delivery_feasibility | 0.15 | | |
| operability | 0.10 | | |
| security_and_data_protection | 0.10 | | |
| change_tolerance | 0.05 | | |
| cost_and_run_burden | 0.05 | | |

*Must sum to 1.00. Where a criterion was dropped for lack of evidence, say so and show the
renormalized weights.*

## Assumptions this assessment depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {criteria affected} | {low \| medium \| high} |

## What would change the ranking

| Varied | By | Result |
|---|---|---|
| Availability target | one step stricter / looser | {which option changes, and at what point} |
| Peak volume | ×3 and ×10 | {…} |
| Quality-attribute weight | ±0.10 | {…} |
| Delivery feasibility weight | ±0.10 | {…} |

## Tie-breakers

*Include only when the top two are inside the band. Apply in order and show which resolved it.*

1. Fits the estate that exists over the estate you would prefer.
2. The organization can operate it the day the delivery team leaves.
3. Fewer moving parts, where the quality attributes are met either way.
4. Still tied — report the tie and name the one piece of evidence that would break it.
