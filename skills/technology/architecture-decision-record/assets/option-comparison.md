# {Decision subject} — option comparison

**Date:** {YYYY-MM-DD} · **Scope:** {…} · **Driver:** {…} · **Reversibility:** {…}
**Confidence:** {low | medium | high} — {reason}

> Scores are **favourability on a 1-5 scale**, not magnitude. An option that is cheap to
> run scores high on ongoing burden; an option needing heavy migration scores low on effort
> to adopt.

## Summary

| Option | Weighted score | Measured / judged | Verdict |
|---|---|---|---|
| {opt-1} | {0.00} | {n of 7 measured} | {chosen \| viable \| eliminated} |

**Options assessed:** {n}. {Three or more — full confidence available. Two — capped at
medium, and the reason a third was unavailable is recorded below. One — this is a
rationale record, not a decision.}

**Gap between the top two:** {0.00} — indifference band is 0.30. {Inside or outside, stated
explicitly. Inside it, no single option is chosen and the tie-breakers apply.}

## Why there was no third option

*Required whenever only two options were assessed. Delete this section if three or more were.*

{"No third approach satisfies the seven-year retention constraint." That is a legitimate
and useful sentence. "We didn't have time to think of one" is also legitimate, and more
useful still, because it tells a reader exactly how much weight to put on the result.}

## Options eliminated before scoring

| Option | Eliminated by | What the constraint says |
|---|---|---|
| {opt-n} | {policy_id} | {…} |

*State "None" explicitly if no option was eliminated.*

## Scores

| Option | Criterion | Score | Weight | Weighted | Evidence | Measured or judged | Assumption | Score confidence |
|---|---|---|---|---|---|---|---|---|
| {opt-1} | fit_to_requirement | {1-5} | 0.25 | {0.00} | {evidence_id: the specific fact} | {measured \| judged} | {A1, or blank} | {low \| medium \| high} |
| {opt-1} | estate_fit | | 0.20 | | | | | |
| {opt-1} | reversal_cost | | 0.15 | | | | | |
| {opt-1} | risk_exposure | | 0.15 | | | | | |
| {opt-1} | standards_alignment | | 0.10 | | | | | |
| {opt-1} | effort_to_adopt | | 0.10 | | | | | |
| {opt-1} | run_burden | | 0.05 | | | | | |

**Measured or judged** is the column a reviewer should read first. `measured` means
something was actually tried — a spike, a benchmark, direct prior experience with this
option in this estate. Everything else is `judged`, however well reasoned.

## Weights used

| Criterion | Default | Used | Changed by |
|---|---|---|---|
| fit_to_requirement | 0.25 | {0.00} | {overlay \| renormalization \| unchanged} |
| estate_fit | 0.20 | | |
| reversal_cost | 0.15 | | |
| risk_exposure | 0.15 | | |
| standards_alignment | 0.10 | | |
| effort_to_adopt | 0.10 | | |
| run_burden | 0.05 | | |

*Must sum to 1.00.*

## Assumptions this comparison depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {criteria affected} | {low \| medium \| high} |

## What would change the result

| Varied | How | Result |
|---|---|---|
| The recommended option | Remove it entirely | {which option it falls to, and whether the consequences change materially} |
| Judgement-based scores | Each one point worse | {does the recommendation survive without unmeasured optimism} |
| Cost of being wrong | Weight ±0.10 | {…} |
| Solving the problem | Weight ±0.10 | {…} |

## Tie-breakers

*Include only when the top two are inside the band. Apply in order and show which resolved it.*

1. Cheaper to reverse.
2. Follows the existing standard.
3. Fewer moving parts to operate.
4. Still tied — report the tie and name the one piece of evidence that would break it.
