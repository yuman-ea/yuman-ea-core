# Day one rules

This reference constrains **what goes on the day-one list and what is refused from it**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## The single test

> **What breaks the moment the deal closes?**

Not what would be better. Not what is easy while everyone is paying attention. Not what somebody has wanted for two years and sees an opportunity to attach. **What breaks.**

Five things break at close, and almost nothing else does:

| Cause | Example |
|---|---|
| A seller-provided service stops | Payroll run by the seller's shared service |
| A contract terminates on change of control | A licence that does not transfer |
| A regulatory obligation transfers | A return that is now the acquirer's to file |
| A customer commitment must be honoured | A service level that does not pause for a transaction |
| Access to data or premises is lost | An account that was the seller's |

Anything not traceable to one of those is not a day-one item. The correct day-one answer for most capabilities is **"exactly as it does today, unchanged"**, and that answer should be written in the plan rather than left implicit — because a blank looks like an omission and invites somebody to fill it.

## Day-one scope creep

The commonest way an integration fails in its first week, and it arrives through entirely reasonable individual decisions.

Every added item competes for the same attention as the items that cannot fail, and day one is the moment with the least slack in the entire programme: two organizations are meeting for the first time, half the acquired staff are anxious, and the people who know how things work are answering questions instead of working.

Hence the blueprint's second list — **what we are deliberately not doing on day one** — with the proposer and the reason recorded. Without it, each refused item returns in week three, proposed by somebody who was not in the room, and has to be refused again by someone with less standing to do it.

## State items as outcomes

"People get paid on the 28th." Not "migrate payroll" and not "payroll system available".

Three reasons. An outcome can be verified by somebody who does not understand the systems. It admits solutions the acquirer has not thought of — including doing nothing. And it survives the discovery that the acquirer's assumption about how the outcome is currently achieved was wrong, which happens often.

## Verified or assumed

Every day-one item records which it is.

Before close, most integration planning is done on what the acquirer *assumes* the acquired business looks like, because that is all anyone had. That is legitimate and unavoidable. What is not legitimate is presenting the result as a plan without saying which parts rest on assumptions.

**An assumed day-one item is the one that fails on day one.** There is exactly one opportunity to convert assumptions into verified items, it is the period before close, and it closes permanently.

Where access is clean-room only, say plainly that the day-one plan is a day-one hypothesis and that its first task is verification.

## Separation dependencies are the hard deadlines

A transitional service arrangement has an end date set by the seller.

That date is harder than any internal deadline in the programme, for a reason worth stating: the seller has no interest in the acquirer's readiness, is usually keen to stop, and any extension is negotiated from a position of weakness by a party that has already paid. Internal deadlines slip by agreement; this one does not.

So the work has to finish before the service stops, not before the organization is ready — and the sensitivity analysis tests an end date three months earlier than scheduled, because that is roughly the distance between a scheduled end and an effective one when notice periods and wind-down are counted.

## Change-of-control terms

Found late, and expensively.

A supplier agreement that terminates or reprices on change of control is invisible in every capability view and appears on the day the supplier's account team notices the announcement. In an acquisition of any size there are usually several, and at least one matters.

Where contracts have not been checked, the confidence rating drops to `low` regardless of how thorough the rest of the work is. `unknown` in that column is not a gap in the analysis — it is an outage waiting for somebody else to spot it.

## What day one is not for

**Not for demonstrating progress.** The pressure to show something visible at close is real and it is the mechanism by which the day-one list grows. A day-one plan whose only content is continuity, delivered without incident, is the best possible outcome and looks like nothing happened.

**Not for standardising anything.** Even something small. Especially something small, because small standardisations are the ones nobody argues about and they establish that day one is a suitable time for standardising.

**Not for deciding which systems survive.** That decision is not urgent, is a portfolio question, and is made far better in month four with real information than in week one with none.
