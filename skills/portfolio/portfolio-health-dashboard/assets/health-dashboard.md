# Portfolio health — {scope}, {period}

**As at:** {YYYY-MM-DD} · **Status source:** {self reported | programme office | measured}
**Tolerances:** {from overlay policy portfolio_tolerances | declared defaults}
**Intervention capacity this period:** {…} · **Confidence:** {low | medium | high} — {reason}

> **Overall is the worst dimension, not an average.** An initiative with a red risk and four
> greens is red. **`not_yet_measurable` is not green** — it is a distinct state and renders
> distinctly. **`unknown` is not green** either.

## Summary

| Status | Count | Of which escalated |
|---|---|---|
| Red | {n} | {n} |
| Amber | {n} | {n} |
| Green | {n} | — |
| Unknown | {n} | {n} |

{Where the distribution is implausible — everything green in a portfolio under strain, or
everything red — say so. A dashboard that always returns the same colour has stopped
measuring anything.}

## Dashboard

| Initiative | Phase | Overall | Cost | Schedule | Risk | Benefit | Dependency | Reported | Movement | Periods in state | Escalated | Confidence |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| {…} | {…} | {red} | {…} | {…} | {…} | {not_yet_measurable} | {…} | {green} | {deteriorated} | {3} | {yes} | {…} |

**Reported** is what the initiative said. The columns to its left are what the tolerances
derived. **The gap between them is the most useful thing on this page** — more useful than
either column alone.

## Ratings and the bands that produced them

| Initiative | Dimension | Rating | Band applied | Evidence | Assumption |
|---|---|---|---|---|---|
| {…} | cost | red | {"forecast at completion 22% over budget, against a 15% red threshold"} | {evidence_id: the fact} | {A1, or blank} |

*A rating without the band behind it cannot be argued with, which means it cannot be
trusted either.*

## Where reported and derived disagree

| Initiative | Reported | Derived | Why |
|---|---|---|---|
| {…} | green | amber | {the band that was crossed, and by how much} |

*State "None — reported and derived agree throughout" explicitly if that is true. It is a
meaningful finding when the status source is self-reported, and worth saying out loud.*

## Optimism correction

{Where `status_source` is self_reported, state that the declared correction was applied,
which initiatives it moved, and by how much. A correction applied silently is
indistinguishable from a rating that was simply wrong.}

## Assumptions this dashboard depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {initiatives or dimensions affected} | {low \| medium \| high} |

## What would change it

| Varied | How | Result |
|---|---|---|
| Self-reported ratings | One band more pessimistic | {which initiatives change status} |
| Forecast at completion | +15% | {which breach the cost tolerance} |
| Benefit measurement | None before close | {how much of the justification would be undemonstrated} |
| Prior period | Removed | {what can still be said without trend or persistence} |
