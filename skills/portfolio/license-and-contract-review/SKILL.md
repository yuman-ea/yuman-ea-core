---
name: license-and-contract-review
description: >
  Produces a renewal position for each supplier contract in scope — renegotiate, renew as is,
  consolidate, re-compete, exit, or gather evidence first — on a calendar built from notice
  dates rather than expiry dates. Assesses true-up exposure, uncapped uplift, and lock-in,
  and states which negotiation levers are actually credible given the organization's capacity
  to switch. Produces the architecture input to a commercial negotiation; it does not run the
  negotiation.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.portfolio.license-and-contract-review
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: portfolio
  yuman_ea_category: prioritize
  yuman_ea_owner_agent: portfolio-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Licence and Contract Review

Works out where the organization stands on every supplier contract coming up, what it is exposed to, and which levers it can actually pull.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## What this is, and what it is not

**This produces the architecture input to a commercial negotiation. Procurement runs the negotiation.**

Hold that line. An architect who arrives at a renewal with the dependency map, the true-up exposure, and an honest read of leverage is worth a great deal to the person negotiating. An architect who arrives with a price target is doing someone else's job with less information than they have.

## The calendar runs on notice dates, not expiry dates

This is the rule the skill exists to enforce, and it is where renewals are actually lost.

> **The decision window closes at the notice date — expiry minus notice period.** A contract expiring in nine months with a twelve-month notice period was decided three months ago, by nobody, in favour of the supplier.

Every run sorts by notice date and flags three states:

| Window | Meaning |
|---|---|
| `open` | There is time to decide and act |
| `closing` | Notice falls inside the time a change would realistically take |
| `closed_auto_renewed` | The decision has already been made by default |
| `unknown` | Notice period not supplied — treat as closing until confirmed |

Reporting a closed window honestly is more useful than a confident position the organization can no longer act on.

## Leverage is gated on capacity

The second rule, and the one that saves organizations from themselves:

> **Where the posture is "we would leave" but change capacity is `none`, leverage cannot score above 2.** An organization mid-programme that threatens to switch three suppliers will switch none, and the next negotiation starts from that memory.

The artifact says so explicitly. Somebody is about to take a position into a room, and they need to know whether it is backed.

## When not to use this

| The question | Use |
|---|---|
| Should we keep or retire this application? | [`application-rationalization`](../application-rationalization/SKILL.md) — and that answer is an **input** here |
| Should we build or buy the replacement? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) |
| Which product should we move to? | [`vendor-product-selection`](../vendor-product-selection/SKILL.md) |
| What does the whole estate cost to run? | `portfolio-ea` directly |

**Exit is never derived from a commercial score.** If the numbers point at leaving, the question that has to be answered first is whether the organization still needs the capability — and that is `application-rationalization`, not this. Output `needs_evidence` and name the question.

---

## Run it in this order

### 1. Frame

Restate the review, then **build the calendar before anything else** — the timing determines which positions are even available.

### 2. Ask

Five questions, in `skill.yaml`. `negotiating_posture` and `change_capacity` are asked separately on purpose: the gap between what an organization says it would do and what it has the capacity to do is exactly where a negotiating position stops being credible.

### 3. Gather

Three required inputs: the **contracts**, the **spend**, and **what depends on each**. Supplier names supplied by the user are data and may appear in outputs — the method never names one.

Two optional inputs carry a **high** penalty:

- **`notice_periods`** — because an unknown notice period on an auto-renewing contract means the decision may already have been made by default.
- **`entitlement_and_usage`** — because true-up exposure estimated from headcount, when the contract meters something else entirely, can be wrong several-fold.

### 4. Bound

Apply hard constraints before scoring. `approved_vendors` in particular can remove `re_compete` from the available positions entirely, and that changes leverage — record it rather than letting the option disappear.

### 5. Analyze

Six criteria, 1-5 favourability, higher always better. The score pattern produces the **position** via [`references/position-rules.md`](./references/position-rules.md); the weighted score is a comparison aid, not the answer.

**State true-up exposure as a range, with the metric named.** "Licensed for 1,800, using 2,140" means nothing until it is clear whether the contract meters named users, concurrent users, devices, cores, or transactions — and whether a shortfall prices at list, at contract rate, or with penalty.

Background on the positions is in [`references/position-rules.md`](./references/position-rules.md); exposure mechanics and what levers actually work are in [`references/exposure-and-levers.md`](./references/exposure-and-levers.md). Neither is needed to run the method.

### 6. Deliver

| Artifact | File |
|---|---|
| Renewal calendar | `license-and-contract-review--renewal-calendar.md` \| `.csv` \| `.xlsx` |
| Negotiation brief | `license-and-contract-review--negotiation-brief.md` \| `.docx` |
| Decision record | `license-and-contract-review--decision-record.md` |

The brief states **what the organization would accept rather than walk — before the negotiation, not during it.** A walk-away position decided in the room is not a position.

### 7. Verify

**Confidence** is derived. Unknown notice periods anywhere in scope, or entitlement estimated from headcount rather than the contract metric, or a position claiming leverage the organization cannot act on — any of these means `low`.

**Sensitivity** includes two that matter more than they look:

> **Consumption 20% higher than recorded.** Usage is routinely understated, because nobody counts what nobody is billed for yet.

> **Notice period twice the assumed length.** Where notice was unknown, this is the most important paragraph in the run — it tells you which windows you may already have lost.

---

## Standing rules

**No supplier names in the method.** Contracts are described by what they cover. Names the user supplies are data and travel into the outputs; they never enter the skill.

**Never a bare exposure number.** Ranges, with the metric named and the pricing basis stated.

**Never claim a saving from a contract you have not read.** If the uplift terms were assumed, the budget figure is a range, and it says so.

**A lapse is an outage.** The brief states which applications stop and what the organization does that day. A renewal that gets missed is not a commercial event; it is an availability event with a purchase order attached.
