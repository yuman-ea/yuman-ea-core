# Capacity profile — {scope}

**Capacity basis:** {measured from history | estimated from headcount | **unknown**}
**Slack policy:** {none | 10% | 20%+} · **Skills profiled:** {yes | **no — capacity treated as fungible**}

> **This is where the plan is honest.** `over_capacity` is reported, never smoothed. A plan
> that exceeds capacity in any wave is infeasible for that scope.

## By wave

| Wave | Skill group | Capacity available | In-flight committed | Slack reserved | Allocatable | Demand placed | Over / under | Status |
|---|---|---|---|---|---|---|---|---|
| {W1} | {all \| data \| front-end \| integration} | {…} | {…} | {…} | {…} | {…} | {+/-} | {within_capacity \| at_capacity \| **over_capacity**} |

**In-flight committed** is subtracted before anything new is placed. Organizations are never
starting from zero, and a plan built on free capacity is over-committed before it is
published.

**Slack reserved** comes off before the wave is declared full. Every plan slips.

## Where skills bind before totals do

| Wave | Total position | Binding skill | Position on that skill |
|---|---|---|---|
| {…} | {within capacity overall} | {data engineering} | {**over by {n}**} |

*Three teams is not capacity for work needing a data engineer if all three are front-end
teams. Where skills were not profiled, say so here rather than reporting a total that hides
it — the shortfall appears only when the wave starts.*

## Over-capacity waves

| Wave | Over by | Options |
|---|---|---|
| {…} | {…} | {move {initiative} to wave {n} \| reduce scope of {initiative} \| add {capacity} \| move the date} |

*State the options; do not choose between them. Capacity, scope, and date are the three
things that can give, and which one gives is an organizational decision rather than an
analytical one.*

## If capacity is 20% lower than stated

| Wave | Status at stated capacity | Status at -20% | Initiatives that move |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

*Where the capacity basis is headcount rather than delivery history, this table is closer to
the real plan than the one above it.*
