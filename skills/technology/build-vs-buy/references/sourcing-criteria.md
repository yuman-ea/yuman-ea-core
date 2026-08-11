# Scoring the seven criteria

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file** — reach for it when a score is genuinely contested, when a reviewer asks why an option scored what it did, or when two options are inside the indifference band and the tie has to be defended.

Weights are not discussed here. They live in [`skill.yaml`](../skill.yaml) and are changed through an overlay.

## The one rule that makes scorecards readable

**Scores express favourability, not magnitude.** Every criterion is `higher_is_better`. A cheap option scores 5 on five-year cost; a supplier with a thin balance sheet scores 2 on supplier risk. The cost itself belongs in the memo's cost table, not in a score column.

Mixing the two conventions — high score means "more cost" on one row and "less cost" on another — is the most common way a scorecard becomes unreadable, and it usually survives until someone recomputes it in a spreadsheet in front of the steering committee.

---

## strategic_differentiation

*Is owning this outright how the organization competes?*

The question is not "is this important". Payroll is important and differentiates nobody. The test is whether a customer, a regulator, or a margin would notice if this were done differently from everyone else.

| Score | For a build option | For a buy option |
|---|---|---|
| 5 | The capability is how the organization wins, and control of it is the point | The capability is pure commodity and every serious supplier does it the same way |
| 3 | Competitive parity — the organization needs to be as good as peers, not better | Same, from the other direction |
| 1 | Building a commodity, and the effort is a distraction from what does differentiate | Buying the thing the organization is supposed to be distinctive at |

**The trap.** Almost every business sponsor believes their capability is differentiating. Test the claim: *what would a customer notice if we did this the same way as everyone else?* If the answer is "nothing", it is parity at best.

**The split.** Differentiation is rarely uniform across a capability. Order capture is usually commodity; the pricing or routing logic on top of it may not be. Where the answer differs across the parts, say so and evaluate a split option — build the differentiating slice, buy the rest. It is frequently the correct answer and it is invisible to a two-column comparison.

---

## tco_5y

*Five years, all in, including the parts that do not appear on an invoice.*

See [`cost-model-notes.md`](./cost-model-notes.md) for how to build the comparison from partial data. For scoring:

| Score | Meaning |
|---|---|
| 5 | Clearly the cheapest over five years, and the conclusion holds at the top of its estimate range |
| 4 | Cheaper, but the margin is inside the estimate uncertainty |
| 3 | Comparable to the alternatives once internal effort is counted |
| 2 | More expensive, for reasons the organization would have to justify |
| 1 | Materially more expensive with no compensating advantage |

**The trap.** Build options look cheaper than they are, because the largest cost — engineers, over five years, running it — is a headcount the organization already has and therefore feels free. It is not free; it is capacity that cannot be spent on something else. Count it, and say in the memo whether it is counted, because that single line is the most common reason two people reading the same analysis disagree about the answer.

**Estimated cost never scores 5.** A 5 asserts that the conclusion survives the estimate range. If the range has not been tested, the score is a 4 at most and the reason belongs in the evidence column.

---

## time_to_value

*When the business is actually using it — not when the project is declared finished.*

Measure to first genuine business use, not to go-live. A phased delivery that puts something useful in front of users in month four beats a complete delivery in month fourteen on this criterion, even if the fourteen-month result is better.

| Score | Meaning |
|---|---|
| 5 | Weeks, or a phased path with real value inside a quarter |
| 3 | Comparable to the alternatives, or a delay the business has already absorbed |
| 1 | So slow the business need will have changed before it lands |

**The trap.** Buy options are quoted as installation timelines and delivered as integration and data-migration timelines. Score against what the organization will experience, and if the quoted timeline excludes integration, record that as an assumption rather than a score.

---

## integration_complexity

*How much work to make this exchange data with what already runs, and how brittle it leaves the estate.*

Count the integration points, but weight them by tightness. Three read-only extracts are not three synchronous transactional interfaces.

| Score | Meaning |
|---|---|
| 5 | Few points, standard interfaces, no change to anything upstream |
| 3 | Several points, mostly conventional, one that will need care |
| 1 | Tightly coupled into systems that are themselves fragile or at end of life |

**The trap.** Integration cost is where a build option quietly wins and a buy option quietly loses, because a bought product has its own model of the world and something has to reconcile it with the organization's. Where an existing system is already the integration bottleneck, that is a fact about the estate, not about the option — note it once and do not penalize every option for it.

---

## vendor_risk

*Exposure to a supplier's viability, roadmap, pricing power, and security posture, weighted by how much of the capability sits with them.*

Applies to partner options as strongly as to buy options, and is not zero for build — an internally built system with one person who understands it carries a concentration risk of its own.

| Score | Meaning |
|---|---|
| 5 | Little dependency, or the dependency is on something genuinely substitutable |
| 3 | Normal commercial dependency with a workable contract position |
| 1 | Critical process inside a supplier the organization could not replace inside a year |

Score against what is knowable: how substitutable the supplier is, whether data can be extracted in a usable form, whether pricing power sits with the supplier at renewal, and whether the data classification raises the stakes. **Do not score a supplier's financial health from impressions.** If it has not been checked, it is an assumption.

---

## talent_availability

*Can the organization staff this for five years — not deliver it once?*

The honest answer to `talent_reality` usually decides this criterion on its own.

| Score | Meaning |
|---|---|
| 5 | People are in place, not fully committed elsewhere, and the skills are not scarce locally |
| 3 | Recruitment is needed and is plausible on the timeline |
| 1 | The organization would be pretending, or would depend on one individual |

**The trap.** Build options are staffed by the team that is currently finishing something else. Ask what that team is committed to for the next two quarters before scoring above a 3. Bus-factor-of-one is a 1 regardless of how good the individual is.

---

## exit_cost

*What it costs to reverse this in three years.*

Carries the smallest default weight and decides more ties than any other criterion, which is why the first tie-breaker is exactly this.

| Score | Meaning |
|---|---|
| 5 | Could move within a year without major disruption; data is extractable in a usable form |
| 3 | Painful and expensive, but survivable |
| 1 | The data model or the process would hold the organization there regardless of the commercial position |

**The trap.** Exit cost is rarely the licence. It is the data, the process the organization reshaped around the product, and the integrations built on top. Ask *what would we have to rebuild*, not *what would we have to cancel*.

---

## Scoring hygiene

**One evidence citation per score.** The evidence ID and the fact taken from it. "Scored 2 because `talent_reality` is `could_hire` and the must-have list runs to eleven items" can be argued with. "Scored 2" cannot.

**Score the option honestly, not toward the answer.** The characteristic failure is scoring the last two criteria to make the total match a conclusion already reached. The sensitivity analysis exists partly to catch this: a recommendation that only survives at exactly the scores given is a recommendation that was written first.

**Where evidence is absent, the assumption is recorded before the score, not after.** An assumption written afterwards is a justification.
