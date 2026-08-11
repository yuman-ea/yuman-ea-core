# Build vs buy — option scorecard

**Capability:** {capability}
**Decision date:** {date}
**Horizon:** {decision_horizon} · **Primary driver:** {primary_driver}
**Confidence:** {confidence_rating} — {confidence_reason}

> Scores are **favourability on a 1-5 scale**, not magnitude. A cheaper option scores
> higher on five-year cost; it does not show its cost here. Costs are in the summary
> table below.

## Summary

| Option | Type | Weighted score | Five-year cost | Verdict |
|---|---|---|---|---|
| {option_id} | {build \| buy \| partner} | {0.00} | {range or figure} | {recommended \| viable \| eliminated} |

**Gap between the top two options:** {0.00} — indifference band is 0.30.
{State explicitly whether the gap is inside or outside the band. Inside the band, no
single option is recommended; the tie-breakers below apply instead.}

## Options eliminated by constraint

| Option | Eliminated by | What the constraint says |
|---|---|---|
| {option_id} | {policy_id} | {the constraint as the organization states it} |

*State "None" explicitly if no option was eliminated. Silent elimination is not permitted.*

## Scores

| Option | Type | Criterion | Score | Weight | Weighted | Evidence | Assumption | Score confidence |
|---|---|---|---|---|---|---|---|---|
| {option_id} | {option_type} | {criterion_id} | {1-5} | {0.00} | {0.00} | {evidence_id: the specific fact} | {A1, or blank} | {low \| medium \| high} |

**Evidence** names the input the score rests on and the fact taken from it — not a
restatement of the criterion. **Assumption** is blank where the score rests on data the
user actually supplied.

## Weights used

| Criterion | Default weight | Weight used | Changed by |
|---|---|---|---|
| strategic_differentiation | 0.25 | {0.00} | {overlay \| renormalization \| unchanged} |
| tco_5y | 0.20 | {0.00} | |
| time_to_value | 0.15 | {0.00} | |
| integration_complexity | 0.15 | {0.00} | |
| vendor_risk | 0.10 | {0.00} | |
| talent_availability | 0.10 | {0.00} | |
| exit_cost | 0.05 | {0.00} | |

*Weights used must sum to 1.00. Where a criterion was dropped for lack of evidence, say
so here and show the renormalized weights — a reader comparing this to the published
defaults will otherwise assume an error.*

## Assumptions this scorecard depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {the assumption, stated as a sentence} | {on_missing path taken} | {criteria affected} | {low \| medium \| high} |

## What would change this

| Varied | By | Result |
|---|---|---|
| Internal build cost | ±30% | {does the leading option change, and at what threshold} |
| Supplier pricing | ±20% | {…} |
| Strategic differentiation weight | ±0.10 | {…} |
| Five-year cost weight | ±0.10 | {…} |

## Tie-breakers

*Include this section only when the top two are inside the indifference band. Apply in
order and show which one resolved it.*

1. Lower exit cost.
2. Earliest delivery of the must-have requirements.
3. Keep the differentiating part in-house.
4. Still tied — report the tie and name the one piece of evidence that would break it.
