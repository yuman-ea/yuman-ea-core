# Rating rules

This reference constrains **how evidence becomes a rating**. It carries the default tolerance bands used when no overlay supplies `portfolio_tolerances`.

Background, loaded on demand. The method in [`SKILL.md`](../SKILL.md) is complete without this file.

## Default tolerance bands

Used only where the organization has not supplied its own. **State which set was used in every run** — a rating means nothing without the band behind it.

| Dimension | Green | Amber | Red |
|---|---|---|---|
| **Cost** | Forecast at completion within 5% of approved budget | 5-15% over | More than 15% over |
| **Schedule** | Next committed milestone forecast on or before plan | Slip up to one reporting period | Slip beyond one period, or a milestone missed and not re-forecast |
| **Risk** | No open high-severity risk, or all with mitigations in flight | Open high-severity risk with a mitigation named but not started | Open high-severity risk with no mitigation, or an issue already materialized |
| **Benefit** | Measured and tracking to the defined target | Measured and behind target | Measured and not appearing, or the initiative has passed its measurement point with nothing measured |
| **Dependency** | No shared dependency, or all confirmed with the owning initiative | Shared dependency identified but not confirmed between the initiatives | Two initiatives depending on the same thing with incompatible assumptions about it |

These are deliberately conventional. The point is not that they are the right numbers for any given organization — it is that **the numbers are written down and the same ones are applied every period.** An overlay replaces them; nothing else should.

## The states that are not colours

**`unknown`** — no evidence for this dimension. Not green. Absence of bad news is not good news, and the most dangerous initiative on any portfolio is the one nobody has heard from.

**`not_yet_measurable`** — the benefit is defined, the measurement approach exists, and the initiative has not yet reached the point where anything could be observed. Legitimate and common early in delivery. It becomes a finding the moment the initiative passes that point with nothing measured.

**`no_definition`** — no benefit was ever defined. This is not a rating at all; it is a governance finding, and it outranks every colour on the dashboard.

If the output format cannot render five states, **say so rather than collapsing them.** Collapsing `unknown` into green is how a portfolio discovers a failed initiative at closure.

## Overall status

**The worst dimension. Always.**

Not an average, not a weighted average, not "mostly green with one issue". An initiative with a red risk and four greens is red.

Averaging is the single most common defect in portfolio reporting and it is worth being explicit about why: a red risk that becomes an amber overall never triggers the escalation that a red would, so the one dimension that needed attention is precisely the one the arithmetic suppressed. The averaging is not a rounding error; it is a mechanism that reliably hides the thing you built the dashboard to find.

The weighted score exists to **rank initiatives for attention** — which of four reds to look at first. It never sets a status.

## The optimism correction

Where `status_source` is `self_reported`, apply **one band of pessimism** to cost, schedule, and risk before rating, and state per initiative that it was applied.

This is not cynicism about delivery teams. It is a structural fact: a team reporting its own status is reporting on its own work, to people who fund it, with incomplete information about how the rest of the portfolio is going. Optimism is the rational response to that position, and correcting for it openly is more respectful than discounting the ratings privately.

Where `status_source` is `programme_office_assessed`, no correction. Where it is `measured`, no correction and confidence rises.

**Never apply the correction silently.** A correction nobody can see is indistinguishable from a rating that was simply wrong, and it destroys the delivery teams' willingness to report honestly next period.

## Persistence

Time in state is computed from the prior period and escalation fires on count, not on trajectory.

An initiative amber for three periods with an improving trend is still escalated. The reasoning: amber never crosses into red, so it never triggers anything, so it persists — and "improving" reported three periods running has usually not improved. If the trajectory is genuine, the escalation costs one conversation and closes.

## Movement

Report `improved`, `unchanged`, `deteriorated`, or `no_prior_period` per initiative.

**Green that was amber and green that has been green for six periods are different situations.** Only one of them needs looking at, and a dashboard showing only current state cannot tell them apart.
