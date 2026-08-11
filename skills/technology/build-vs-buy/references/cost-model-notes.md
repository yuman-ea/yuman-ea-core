# Building a five-year cost comparison from partial data

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when cost is the contested criterion, which it usually is.

The premise: the architect this method is built for does not have a cost model. They have a rough idea of the team, possibly one supplier quote, and no idea what the current arrangement costs because it has never been broken out. **That situation produces a defensible answer.** What it does not produce is a precise one, and the difference has to be visible in the artifact.

---

## What goes in the comparison

The same lines for every option, so the totals are comparable. A line the organization cannot estimate is recorded as unknown — never as zero.

| Line | Build | Buy | Partner |
|---|---|---|---|
| Software licence or subscription | — | Yes | Usually bundled in the fee |
| Implementation and configuration | Part of build | Yes | Yes |
| Data migration | Yes | Yes | Yes |
| Integration work | Yes | Yes | Yes |
| Internal engineering to deliver | Yes | Smaller, not zero | Smaller, not zero |
| **Internal engineering to run, per year** | Yes | Yes | Reduced |
| Infrastructure and hosting | Yes | Depends on model | Usually included |
| Support and maintenance | Internal | Contracted | Contracted |
| Training and change | Yes | Yes | Yes |
| Contract or vendor management | — | Yes | Yes, more |
| Exit or extraction, at end of term | Lower | Yes | Yes |

**Zero is a claim.** "Buy has no internal engineering cost" is almost never true — somebody configures it, integrates it, supports the users, and manages the supplier. A zero that has not been checked is an assumption and belongs in the register.

---

## The three lines that decide most comparisons

**Internal engineering to run, over five years.** The single largest and most frequently omitted line in a build option. Four engineers at a fully loaded cost, for five years, is usually larger than any licence under discussion. Omitting it does not make a build cheaper; it makes the analysis wrong in a way that will be found.

**Integration.** Under-estimated for buy options roughly as often as run cost is omitted for build options, and for the same reason: it is work the option's price does not mention.

**The current run cost.** Not a cost of any option, but the baseline that tells the reader whether any of this is worth doing. If the organization cannot separate it out, say so — *"the current arrangement's cost could not be isolated from the platform it runs on"* is a legitimate and informative statement.

---

## Estimating a build cost with no cost model

Where `internal_build_cost` is absent, the declared behaviour is `estimate_with_assumption` with a **high** confidence penalty. The estimate is a range, and the method for producing it is stated in the memo.

A defensible approach, in the absence of anything better:

1. **Size from the must-have requirements.** Count them. Sort into straightforward, moderate, and genuinely hard. The count is already gathered, so this needs no new input.
2. **Convert to a team over a duration**, not to a number of hours. Business readers understand "four engineers for nine months"; hour totals invite arguments about rates that go nowhere.
3. **Apply a fully loaded cost per engineer per year** — salary plus employment costs plus overhead. Where the organization has no figure, use a stated public range for the market and label it as such.
4. **Add the run cost from year two**, typically a fraction of the build team, sustained. This is the line that gets forgotten.
5. **Widen the range honestly.** Build estimates produced without a cost model are conventionally optimistic. A range of roughly −20% to +60% around the point estimate is more honest than a symmetric band, and saying why is more honest still.

Then write the assumption:

> "A1. Internal build cost was not available. It has been estimated at four engineers for nine months plus one engineer sustained thereafter, giving a five-year range of {low}–{high}. Build estimates made this way are typically optimistic, so the range is asymmetric. This is the largest single uncertainty in the analysis; the recommendation changes if the true figure is above {threshold}."

**That last clause is the point of the whole exercise.** An estimate with a stated threshold is usable. An estimate without one is a number waiting to be quoted back.

---

## Supplier pricing with no quote

Declared behaviour is `estimate_with_assumption`, high penalty. Two rules:

**List price is not the negotiated price.** Published pricing for this category typically overstates what an organization of this size actually pays. Say which one the figure is.

**Price the shape, not the product.** Per-user-per-month against a user count the organization can state, or a band for the category. Naming a product in the analysis makes it unusable at the next organization and violates the standing rule in `SKILL.md`.

Where pricing is genuinely unavailable for the buy option but available for build, **say that the comparison is asymmetric.** An estimated figure against a known one, presented as if both were equal, is the most misleading thing a scorecard can do.

---

## Present costs as ranges, and state the currency

A single number implies a precision the evidence does not support, and it is the number that gets quoted back six months later with the range stripped off.

| Option | Year 1 | Five-year total | Basis |
|---|---|---|---|
| Build in house | 0.9–1.4m | 3.2–4.8m | Estimated — assumption A1 |
| Commercial platform | 0.6–0.8m | 2.4–3.1m | List price band — assumption A2 |
| Managed service | 0.5m | 2.6m | Supplier quote, dated |

State the currency, and state whether internal effort is included. That one line resolves most of the disagreements two readers will have about the same table.

---

## Discounting

If the organization's overlay supplies a `discount_rate`, discount the five-year totals and say that you have. If it does not, **do not invent one** — present undiscounted totals and note it.

An undiscounted comparison mildly favours options with costs late in the term. That is worth a sentence in the assumptions register and is not worth inventing a rate to avoid.

---

## When cost cannot be estimated at all

It happens: no build estimate, no supplier pricing, no baseline.

Do not drop the criterion silently. Options in order of preference:

1. **Ask.** `internal_build_cost` and `vendor_pricing` are the two inputs worth one direct question each, because they carry the highest confidence penalty in the skill.
2. **Estimate with an explicit range and a threshold**, as above.
3. **Omit and renormalize** — only if there is genuinely nothing. Then say so on the scorecard, show the renormalized weights, and rate the run `low` confidence. A build-versus-buy with no cost dimension at all is a well-formatted opinion, and the artifact must say so rather than let the reader assume otherwise.
