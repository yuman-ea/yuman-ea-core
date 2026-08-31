# Case strength rules

This reference constrains **how the criteria produce a status**, and why the status is about the argument rather than about the return. Background, loaded on demand.

## The score assesses the case, not the return

This is the unusual move in this method and it is deliberate.

A case can carry a large net present value and be worthless, because one unevidenced assumption produces all of it. A case can carry a modest return and be entirely reliable. Scoring the return would rank those the wrong way round, and the organization would fund the first.

So the six criteria score **how much weight the argument will bear**. The return is reported separately, and a reader is expected to consider both.

## Status rules

Applied in this order. The first that matches wins.

| # | Status | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | Costs or benefits could not be established at all |
| 2 | `not_yet_a_case` | Benefit evidence ≤ 2, or no benefit has a named owner |
| 3 | `depends_on_one_assumption` | Removing or varying a single input within its plausible range flips the conclusion |
| 4 | `marginal` | The net present value falls inside the range produced by the sensitivity analysis |
| 5 | `fundable_with_conditions` | Sound, with specific named things to fix — usually ownership or a missing baseline |
| 6 | `fundable` | Evidenced, owned, whole-life, and robust across the sensitivity range |

Two orderings are worth defending.

**`not_yet_a_case` outranks everything below it**, including a large return. A case whose benefits are asserted and unowned is not a weak case; it is a proposal that has not yet been turned into a case, and the honest response is to say what would make it one rather than to grade it.

**`depends_on_one_assumption` outranks `marginal`.** A case resting on one input can have a very large headline number, which is exactly what makes it dangerous — the size of the return is doing the persuading and the fragility is invisible.

## `marginal` is a real and useful answer

Where the net present value is smaller than the range its own sensitivity produces, the honest statement is that this analysis cannot separate the investment from doing nothing.

That is not a failure of the analysis. It is a finding, and it usually means the decision should be made on grounds the model does not contain — strategic fit, risk appetite, capability building — which is a legitimate basis and a much better conversation than a false precision about a number.

The failure mode to avoid is reporting a positive net present value of 40,000 on a 2 million investment as though it were a result.

## One assumption carrying the result

Test it directly: for each major input, move it across its plausible range and see whether the recommendation changes.

Where one does it alone, that assumption **is** the case. Say so in the summary, name it, and state what would have to be true. The argument in the room should then be about that assumption, conducted by whoever knows most about it — which is rarely the person who built the model.

This is one of the highest-value outputs available in the method, and it takes minutes.

## Benefit ownership is the strongest predictor

Stronger than the size of the return, the quality of the cost estimate, or the rigour of the model.

The mechanism is simple. A benefit with no owner has no measure. A benefit with no measure is never checked. A benefit never checked cannot fail — so it survives every review, gets counted in the total, and does not arrive. Nobody is dishonest at any point in that sequence.

Three things make a benefit owned:

1. **A named person**, not a function or a committee.
2. **A measure**, with what it reads today. Without the baseline, a delivered benefit and an undelivered one are indistinguishable in eighteen months.
3. **A date** when it starts and a date when it reaches full run rate.

`committed_in_writing` versus `verbally_agreed` matters more than it looks. The written commitment survives the owner's next reorganization; the verbal one does not survive their next set of objectives.

## Benefits requiring an untaken decision

The specific failure mode of released-effort benefits.

The effort is genuinely released. The case was right. And then nobody decides to redeploy the capacity, reduce the headcount, or stop backfilling — because that decision belongs to someone who was not in the room when the case was approved and has no reason to make it.

Record these separately, with the decision named and its owner named. A benefit requiring a decision nobody has agreed to take is not yet a benefit, and the case is stronger for saying so than for including it and being wrong.

## What the case may not do

**Decide.** This method makes an argument. Whether to fund it belongs to someone accountable for the money, and a case that reads as a decision has taken that from them.

**Rank.** A strong case for one investment says nothing about whether it is the best use of the budget. That is a portfolio comparison, and it needs cases for the alternatives.

**Choose the option.** Build-vs-buy and product selection run first. A case built for an option that was never compared is a case for a decision already made.

**Substitute for measurement afterwards.** The realisation plan's check date is what makes the *next* case in this organization better than this one. Without it, an organization has no basis for knowing how optimistic its cases usually are — which is why `comparable_outcomes` carries an assumption when it is absent.
