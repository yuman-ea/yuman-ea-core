# Appraisal rules

This reference constrains **how the numbers are built**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## Doing nothing is an option and it has a cost

Every case compares at least two futures. The failure is comparing one future against zero.

What the do-nothing baseline contains depends on what is being decided:

| Decision | Doing nothing means |
|---|---|
| New investment | Current costs continue, and any trend in them continues |
| Continue or stop | The current spend continues, and so does the current outcome |
| **Renewal** | Something may stop working — support ends, a contract lapses, a licence expires |

The renewal row is the one that changes cases most. When the alternative to renewing is that a critical system becomes unsupported, the case is not a return on investment at all — it is the cost of continuity against the cost of an alternative, and framing it as a return produces a weak-looking case for something the organization has no choice about.

Doing-nothing costs also **rise**. Maintenance on an ageing system, growing manual effort, increasing failure rates. A flat baseline understates the case by the amount of the trend.

## Whole-life cost

Four components, and the third is the one omitted:

1. **Build or purchase** — the number everyone has.
2. **Transition and change** — migration, training, parallel running, temporary capacity, and the disruption while it happens.
3. **Run cost, every year** — licence, hosting, support, and the people who operate it.
4. **Exit** — where a term is fixed and something must be replaced at the end of it.

Over a five-year appraisal, run cost frequently exceeds build cost. A case that stops at go-live has omitted its largest number, and it does so consistently in one direction.

**Parallel running deserves its own line.** It is rarely optional, almost never as short as planned, and it is the transition cost most often left out entirely.

## Four kinds of benefit, and only one reduces spending

| Type | Reduces a budget? | The test |
|---|---|---|
| Cashable saving | **Yes** | Name the budget line that falls, and by how much |
| Released effort | No | Nobody's budget changes; capacity is returned |
| Revenue | No — increases income | Is it new, or protected? Both are legitimate and they are different claims |
| Risk avoidance | No | Probability multiplied by impact. Both halves belong in the source |

**Never total them.** The single most damaging convention in business case writing is the summary line that adds released effort to cashable saving and calls the result a benefit. Two years later the budget has not fallen, and a case that delivered everything it promised is remembered as one that failed.

For released effort, the honest formulation is: *this returns roughly n days a year to team X; whether that becomes a saving depends on a decision nobody has taken.* That sentence is both more accurate and more useful than a currency figure, because it names the decision.

**Risk avoidance stated as a single number has concealed a judgement.** A 20% chance of a 5 million loss is not "1 million of benefit" in any sense a finance function will accept — it is a 20% chance of a 5 million loss, and the case should say so and let the reader apply their own appetite.

## Discounting

State the rate. Where no organizational rate exists, present undiscounted figures and label them.

Undiscounted comparison is not neutral: it favours options whose costs fall late and whose benefits fall early, which describes most investment cases as their authors write them. Saying "undiscounted" is what stops that bias being invisible.

Where the conclusion changes across a ±2 point range on the rate, the case depends on the cost of capital rather than on the merits of the investment. That is worth stating explicitly, because it is a different argument and it belongs to the finance function rather than to the architect.

## Payback, net present value, and internal rate of return

Three measures, and they answer different questions:

- **Payback** — how long before the money is back. Crude, ignores everything after the payback point, and is the number executives actually use.
- **Net present value** — the whole-period value in today's money. The most complete, and the most sensitive to inputs nobody can check.
- **Internal rate of return** — only meaningful where the cash flow has one sign change. Where costs and benefits alternate, it can produce several answers or none, and reporting one anyway is worse than saying it does not apply.

Report payback alongside net present value always. A twenty-year payback with a positive net present value is arithmetically sound and will not be funded, and knowing that early is more useful than being right.

## Appraisal period

The period decides the answer more than almost any other choice.

A short period penalises anything with a long build and rewards short-lived fixes. A long one flatters investments whose benefits are furthest out and least certain — and the further out a benefit is, the less anyone can defend it.

Two guards: use the organization's standard period where one exists, and where the case only works at ten years, say that plainly. An investment whose case requires the tenth year is an investment whose case requires a forecast nobody would defend on its own.

## The break-even is the deliverable

"The net present value is 1.4 million" invites an argument about a number nobody can check.

"The case holds unless the benefit is more than 40% below estimate" invites a judgement about a claim someone can. It is also robust to the criticism every case receives — that the numbers are optimistic — because it has already answered it.

Give at least three break-evens: on cost, on benefit, and on timing.
