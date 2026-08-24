# Benefit realization, and why it is always green

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when a benefit rating is contested, or when an initiative is closing and somebody asks whether it worked.

## The structural problem

Benefit realization is the dimension that gets reported green longest and checked last, and there is a mechanical reason rather than a cultural one.

Cost and schedule have **continuous evidence** — money is spent weekly, milestones arrive monthly, and a variance shows up on its own. Benefit has **no evidence at all until the thing is live**, and often for a period after that. So during delivery there is nothing to report, and "nothing to report" gets entered as green.

By the time evidence exists, the initiative has usually closed, the team has moved on, and nobody owns the question. **The dimension the investment was justified on is the only one never independently checked.**

That is what `not_yet_measurable` is for. It says "no evidence yet, and that is currently fine" without saying "good", and it converts to a finding automatically when the initiative passes its measurement point.

## Making a benefit measurable

Four parts. A benefit missing any of them cannot be rated, and should be recorded as `no_definition` rather than given a colour:

| Part | Example |
|---|---|
| **The measure** | Cost per order processed |
| **The baseline** | 4.10 today, measured over the last two quarters |
| **The target** | Below 3.20 |
| **The date** | Two quarters after go-live, allowing for stabilization |

Without the **baseline** the change cannot be demonstrated, and this is the part most often missing — because it has to be captured *before* delivery starts, when nobody is thinking about measurement yet. An initiative that reaches go-live without a baseline has usually lost the ability to prove its benefit permanently.

Without the **date**, the benefit is never late, so it is never a finding.

## The architectural commitment

The part only architecture asks about, and the reason this skill exists alongside programme reporting.

Initiatives are frequently justified on estate changes: *we will decommission three systems*, *we will retire the point-to-point interfaces*, *we will repay the debt in the order path*. Those commitments carry the business case — the savings are real money in a real budget line.

They are also **the first thing dropped when delivery gets tight**, and dropping them is nearly invisible. The new system goes live, the initiative reports success on cost and schedule, and the old system quietly stays running because something still points at it. The saving was booked; the cost is still being paid.

So the check is simple and it belongs in every period:

> **What did this initiative say it would remove, and is it gone?**

An initiative that closed with outstanding architectural commitments has not realized its benefit, whatever its final report said. Record it, quantify the ongoing cost where possible, and keep it on the note until the commitment is met or formally abandoned.

**Formal abandonment is a legitimate outcome.** Circumstances change and a decommissioning can stop making sense. What is not legitimate is the commitment quietly ceasing to be tracked, which is the normal case.

## Benefit and the run-cost line

The strongest evidence available, and it is usually already in the estate data: **an initiative that promised to remove a system's run cost can be checked against whether that run cost stopped.**

Where the application inventory carries annual run cost, an outstanding decommissioning has a number attached to it. That number is what makes the finding land with finance, and it is considerably more persuasive than an amber square.

## Attributing benefit honestly

Two cautions worth carrying into any benefit conversation:

**Several initiatives will claim the same saving.** Where two initiatives both count the same decommissioning, the portfolio has booked it twice. Check for it — it is common, it is rarely deliberate, and it is embarrassing when finance finds it first.

**Not every improvement is attributable.** Volumes change, the market moves, a different team fixed something. Where the measure moved and the attribution is genuinely uncertain, say so. A benefit claimed on a movement that would have happened anyway costs credibility on every subsequent claim, and credibility is the thing that makes the next business case land.
