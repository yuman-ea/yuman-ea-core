---
name: business-case
description: >
  Builds the funding argument for one investment — whole-life costs against benefits, with
  net present value, payback, and the assumptions the result rests on. Costs the do-nothing
  option rather than comparing against zero, separates benefits that reduce a budget from
  benefits that do not, refuses to record a benefit with no named owner and no date, and
  reports what would have to be true rather than only what the numbers currently say.
  Produces the cost and benefit model, a benefit realisation plan, and the case itself.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.business-case
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: prioritize
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Business Case

The argument for **one** investment. Not which option, not which investment first — those run before this one.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The four ways a case is wrong while its arithmetic is right

> **1. Compared against zero.** Doing nothing is never free, and for a renewal it may mean something stops working. A case with no costed baseline flatters itself by exactly the amount the baseline was worth.

> **2. Stops at go-live.** Over five years the run cost is routinely larger than the build cost. A case that ends at delivery has omitted its largest number.

> **3. Totals cashable and non-cashable benefits.** Half a person released across eight teams is eight fractions of a person and **no reduction in spend** unless somebody's headcount changes. Presenting it as a saving is the commonest way a case that delivered is remembered as a case that failed.

> **4. Benefits nobody owns.** A benefit with no owner is never measured, and a benefit never measured **cannot fail** — which is precisely why it survives scrutiny and never arrives.

## The criteria score the case, not the return

This is the unusual part of the method. The weighted score assesses **how strong the argument is**, not how large the number is.

A case can carry a large net present value and be worthless because one unevidenced assumption produces all of it. That is a status of its own:

| Status | Meaning |
|---|---|
| `fundable` | Evidenced, owned, whole-life, survives its sensitivity |
| `fundable_with_conditions` | Sound, with named things to fix first |
| `depends_on_one_assumption` | Remove one input and the conclusion flips |
| `marginal` | The return is inside the noise of its own inputs |
| `not_yet_a_case` | Benefits unevidenced or unowned |
| `insufficient_evidence` | Could not be assessed |

Rules are in [`references/case-strength-rules.md`](./references/case-strength-rules.md).

## Report the break-even, not just the estimate

> "The recommendation holds unless the benefit is more than 40% below estimate" survives a finance review.
>
> "The net present value is 1.4 million" does not — it invites an argument about a number nobody can check.

## When not to use this

| The question | Use |
|---|---|
| Build it or buy it? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) — runs **before** this |
| Which supplier, which product? | [`vendor-product-selection`](../../portfolio/vendor-product-selection/SKILL.md) |
| Which investment do we fund first? | `portfolio-ea` |
| In what order do we deliver? | [`roadmap-sequencing`](../../portfolio/roadmap-sequencing/SKILL.md) |
| Which applications do we retire to save money? | [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) |

---

## Run it in this order

### 1. Frame

State what is funded and what is **excluded**. Costs and benefits must refer to the same scope — the commonest arithmetic error in a business case is that they do not.

### 2. Ask

Five questions. `benefit_owner_commitment` is the strongest available predictor of whether benefits materialise, and it is almost never asked before money is committed.

### 3. Gather

Three required: the **investment definition**, the **cost estimate**, and the **benefit estimate**.

Three optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `do_nothing_baseline` | Without it the return is overstated by an unknown amount |
| `benefit_owners` | Unowned benefits are the ones that never arrive |
| `ongoing_run_cost` | Usually the largest number in a five-year model |

### 4. Bound

`budget_ceiling` is a hard constraint. Where the investment exceeds it, that is **reported with the policy ID** — never handled by adjusting the case to fit.

### 5. Analyze

Cost the counterfactual. Build whole-life costs. Classify every benefit and **report the classes separately**. Require an owner, a date, and a measure. Discount and state the rate.

Then find out whether **one assumption carries the result** — if it does, that assumption is the case, and the argument should be about it rather than about the net present value.

### 6. Deliver

| Artifact | File |
|---|---|
| Cost and benefit model | `business-case--cost-benefit-model.md` \| `.csv` \| `.xlsx` |
| Benefit realisation plan | `business-case--benefit-realisation-plan.md` \| `.csv` \| `.xlsx` |
| Business case | `business-case--business-case-summary.md` \| `.docx` \| `.pptx` |

**Every figure names its source.** A number with a blank source column is the defect this whole method exists to prevent — and in a board pack, a number acquires authority from the pack rather than from its derivation.

**Every benefit has a baseline value.** Without what the measure reads today, the benefit cannot be demonstrated afterwards even if it is fully delivered.

### 7. Verify

**Confidence** is `low` if benefit ownership was never discussed, or if a single assumption carries the conclusion — whatever the return.

**Sensitivity** includes the one the finance function will run anyway:

> **Count only benefits that reduce a budget.** Constructing that number first is how a case survives the meeting instead of being rebuilt in it.

---

## Standing rules

**Never total cashable and non-cashable benefits.**

**Never present released effort as a saving** unless a budget actually falls. Say which budget.

**A benefit with no owner, date, and measure is recorded as unowned** — not omitted. Omitting it hides the problem; leaving it in the total *is* the problem.

**State the discount rate, or state that figures are undiscounted.** Undiscounted comparisons favour options whose costs fall late and benefits fall early, which describes most cases as they are written.

**This method does not decide whether to fund it.** It makes the argument; someone accountable decides.
