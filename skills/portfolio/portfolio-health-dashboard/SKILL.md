---
name: portfolio-health-dashboard
description: >
  Produces a health view across change initiatives — cost, schedule, risk, and benefit
  realization rated red, amber, or green from declared tolerances rather than asserted.
  Overall status is the worst dimension and never an average; unmeasured benefits are
  reported as not yet measurable rather than green; and an initiative amber for several
  periods escalates regardless of trajectory. Ranks the exceptions against the
  organization's actual capacity to intervene.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.portfolio.portfolio-health-dashboard
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: portfolio
  yuman_ea_category: aggregate
  yuman_ea_owner_agent: portfolio-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Portfolio Health Dashboard

Rates change initiatives red, amber, or green across cost, schedule, risk, and benefit realization — **derived from declared tolerances, never asserted.**

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Tolerance bands come from the `portfolio_tolerances` policy an overlay supplies; the defaults are in [`references/rating-rules.md`](./references/rating-rules.md).

## What this is, and what it is not

**This does not replace programme or project status reporting.** A programme office reports on delivery, and does it closer to the work than an architect can.

The architecture view adds three things a delivery status report structurally cannot:

- **Whether the architectural commitment landed.** An initiative justified on decommissioning a system, which completed while that system still runs, did not realize its benefit — whatever its cost and schedule said on the day it closed.
- **Collisions between initiatives.** Two programmes each depending on the same system being available, each reporting green independently, because neither is wrong about itself.
- **Benefit that was never defined.** Which is not a rating; it is a governance finding, and it belongs at the top of the exception report.

Run this alongside programme reporting, not instead of it.

---

## Four rules that stop this becoming a colouring exercise

> **1. Overall status is the worst dimension. Never an average.** An initiative with a red risk and four greens is red. Averaging is precisely how a red risk becomes an amber overall that nobody acts on, and it is the single most common defect in portfolio reporting.

> **2. Unmeasured is not green.** Where benefits are defined but nothing has been measured, the status is `not_yet_measurable` — a distinct state with its own colour. Most initiatives report benefit green throughout delivery because nothing has been checked, and a dashboard that renders that as green is lying by omission.

> **3. No evidence means `unknown`, not green.** Absence of bad news is not good news.

> **4. Persistent amber escalates regardless of trajectory.** Amber never crosses into red, so it never triggers anything, so it persists. The `escalation_threshold` answer sets how many consecutive periods is too many, and the rule fires even when the trend is improving.

The weighted score exists only to **rank initiatives for attention**. It never sets a status.

## The watermelon problem

Green on the outside, red in the middle. It is what the `status_source` question is for.

Where status is self-reported, the method applies a declared optimism correction **and says that it did**, per initiative. The dashboard keeps `reported_status` beside the derived rating, because **the gap between those two columns is the most useful thing on the page** — more useful than either column alone.

A correction applied silently is indistinguishable from a rating that was simply wrong.

## When not to use this

| The question | Use |
|---|---|
| Which applications do we keep or retire? | [`application-rationalization`](../application-rationalization/SKILL.md) |
| When do contracts come up, and what is our position? | [`license-and-contract-review`](../license-and-contract-review/SKILL.md) |
| Which investment should we fund first? | `portfolio-ea` directly — this reports health, it does not prioritize spend |
| Should this initiative continue? | An investment decision. This informs it; it does not take it |

**Ratings describe initiatives, never people.** If a rating reads as a judgement on a delivery team, rewrite it.

---

## Run it in this order

### 1. Frame

Restate the scope and confirm which initiatives are in and which are out. **A dependency that crosses the scope boundary is invisible to the run**, and that limitation is stated rather than discovered.

### 2. Ask

Five questions, in `skill.yaml`. `status_source` and `intervention_capacity` do the most work — the first sets how far the reported ratings can be trusted, the second stops the exception report becoming a list nobody can act on.

### 3. Gather

Three required: **initiatives**, **cost position**, **schedule position**. For cost, say which of budget, spent, and forecast-at-completion are actuals and which are estimates — a forecast carried forward from last quarter is not a forecast.

Two optional inputs carry a **high** penalty, and one behaves unusually:

- **`benefit_definitions`** uses `omit_criterion_and_reweight`. If no benefits were defined, benefit realization cannot be rated, so the criterion is dropped and the weights renormalize. **The absence is itself the finding** — an initiative with no defined, measurable benefit cannot succeed or fail on its own terms — and it goes at the top of the exception report, not into a footnote.
- **`benefit_actuals`** absent means every benefit rating is `not_yet_measurable`. Never green.

`architecture_commitments` is the input that makes this an architecture view rather than a second delivery report. Without it, this dashboard tells a steering committee what its programme office already told them.

### 4. Bound

Tolerance bands come from `portfolio_tolerances`. With no overlay, the declared defaults apply and the run **says which bands were used** — a rating is meaningless without the band behind it.

### 5. Analyze

Rate each dimension **from the tolerances, not from the reported colour**. Where the derived rating differs from what was reported, show both.

Then set overall to the worst dimension, compute time-in-state from the prior period, fire the persistent-amber escalation, check architectural commitments against what actually happened, and identify collisions.

Rank the exception report **to intervention capacity**. Everything beyond it is listed as *carried*, not as actioned.

### 6. Deliver

| Artifact | File |
|---|---|
| Health dashboard | `portfolio-health-dashboard--health-dashboard.md` \| `.csv` \| `.xlsx` |
| Exception report | `portfolio-health-dashboard--exception-report.md` \| `.docx` |
| Benefit realization note | `portfolio-health-dashboard--benefit-realization-note.md` \| `.csv` |

The exception report is the half that gets read. The dashboard is the evidence behind it.

### 7. Verify

**Confidence** is derived. Self-reported status with no independent challenge, or no benefit definitions, or no prior period, means `low`.

`dissent_note` is emitted alongside the usual three: **where a delivery team disagrees with a derived rating, preserve the disagreement rather than averaging it away.** A team that says amber where the tolerances say red usually knows something the tolerances do not — and occasionally the reverse. The steering committee needs to see both.

**Sensitivity** includes the closest thing to an independent check available:

> **Treat every self-reported rating as one band optimistic.** Which initiatives change status? Where status is self-reported, this is the most important paragraph in the run.

---

## Standing rules

**Every rating cites the tolerance band that produced it.** "Red because forecast at completion is 22% over budget, against a 15% red threshold" can be argued with. "Red" cannot.

**Never render `unknown` or `not_yet_measurable` as green.** They need their own colour, and if the output format cannot support five states, say so rather than collapsing them.

**Trend beats status.** Green that was amber and green that has been green for six months are different situations, and only one of them needs looking at.

**Say what is not being acted on.** A dashboard implying fourteen simultaneous interventions is worse than one that names two and admits the other twelve are being carried.
