# Position rules

This reference constrains **how the score pattern becomes a position**. The weighted score is a comparison aid; it is not the position.

Background, loaded on demand. The method in [`SKILL.md`](../SKILL.md) is complete without this file.

## Timing gates everything

Before any position is assigned, the window is established. Positions that need time are unavailable without it.

| Window | Positions available |
|---|---|
| `open` | All |
| `closing` | `renegotiate`, `renew_as_is`, `needs_evidence`. **Not** `re_compete` — going to market takes longer than the window allows |
| `closed_auto_renewed` | `renew_as_is` only, plus a note on when the next window opens |
| `unknown` | Treat as `closing` until the notice date is confirmed |

**A position the organization cannot act on in the time remaining is not a position.** Recommending re-competition with four months left on a nine-month replacement is a plan to miss the deadline and renew from the weakest possible footing.

---

## The positions

### Renegotiate

Stay with the supplier, improve the terms. The default where leverage is real and the relationship is worth keeping.

Requires **leverage scoring 3 or better**, which in turn requires alternatives, capacity, and time. Where leverage is 2 or below, `renegotiate` is still available but the brief must say the organization is asking rather than negotiating — those are different conversations and the supplier knows which one is happening.

### Renew as is

Accept the terms. Legitimate and frequently correct: where the contract is small, the terms are fair, leverage is thin, or the effort is better spent on the three contracts behind it.

Say why. "Renew as is" with no reasoning reads as an oversight, and next cycle nobody knows whether it was considered.

### Consolidate

Fold this contract into another, or bring several together at a common date.

Requires overlap that is real rather than apparent, a target contract that covers the need, and `supplier_consolidation_preference` that is not `more_narrower`. Note the trade honestly: **consolidation buys discount and costs leverage.** One large relationship is harder to leave than three small ones, and the discount is usually visible while the lost optionality is not.

Aligning renewal dates is often worth more than the discount, because it creates one window with real scale instead of four windows with none.

### Re-compete

Go to market. Available only where the window is `open`, alternatives exist, and change capacity is at least `one_switch`.

**This hands off.** Re-competition is a sourcing exercise — route it to `build-vs-buy` for the make-or-buy question if that is still open, and to `vendor-product-selection` to run the evaluation. This skill's job ends at establishing that going to market is viable and worth the effort.

### Exit

**Never derived from a commercial score.** Available only where the application disposition already says retire or replace — an `application-rationalization` decision, taken elsewhere, on business and technical grounds.

Where the commercials point at leaving and no disposition exists, the position is `needs_evidence` and the named question is *"do we still need this capability?"* Deciding to switch a system off because its contract is expensive is how an organization discovers what depended on it.

Where a disposition does exist, this skill's contribution is **timing**: exit at the notice date that costs least, with the dependency list attached.

### Needs evidence

The correct answer when the timing is known but the position is not determinable — entitlement unknown, terms unread, or the disposition question unanswered.

Name four things: the missing evidence, who holds it, the single next step, and **the date it must be answered by, measured against the notice date rather than against convenience.** Evidence that arrives after the window closes is history.

---

## Close calls

**Prefer the position that keeps the decision open.** A one-year extension preserving the option beats a three-year commitment at a marginally better rate, wherever the estate around the contract is changing — and in most organizations it is.

**Prefer acting on the nearest notice date.** Time is the only lever that expires without anyone doing anything.

**Where exposure and price point different ways and the objective is balanced, reduce exposure.** A price rise arrives with a renewal notice and a conversation. A true-up arrives with an audit letter and a number.
