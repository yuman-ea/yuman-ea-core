# Exposure, and which levers actually work

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when sizing a true-up or writing the levers section.

## Exposure is not price

Price arrives with a renewal notice and a conversation. **Exposure arrives without a decision being taken** — an audit letter, an indexation clause firing, a metric that was always going to be breached once headcount grew.

That difference is why exposure carries more weight than value for money in this method, and why the sensitivity analysis varies consumption before it varies anything else.

## Sizing a true-up

Three things, and the middle one is where most estimates go wrong.

**1. The metric the contract actually uses.** Not the metric the organization thinks in. Named users, concurrent users, devices, processor cores, transactions, revenue band, employee headcount — these can differ by several times over the same population. An estimate against the wrong metric is not a rough number; it is a different question answered confidently.

**2. Entitlement versus consumption, at the same date.** Entitlement is a contract fact. Consumption is a measurement, and it is routinely understated because nobody counts what nobody is billed for yet — dormant accounts still provisioned, test environments, contractors, service accounts, people who left last quarter. The gap between "who uses it" and "who is licensable" is often the whole exposure.

**3. How a shortfall prices.** At list, at contract rate, or with penalty and backdating. This changes the number more than the gap itself does, and it lives in the audit clause, which is the clause nobody has read.

Then state it as a range with all three named:

> "Entitlement 1,800 named users; approximately 2,140 provisioned, of which perhaps 1,950 are genuinely in scope once dormant accounts are removed. Gap of 150-340. At contract rate that is {range}; at list with backdating, {range}. The metric is named users, not concurrent — confirmed."

**Never a bare number.** A single figure will be quoted back, in a budget, without the caveats.

## Uplift and indexation

Read for three things: **the cap**, **what it is indexed to**, and **whether it compounds**. An uncapped uplift on a large multi-year contract can exceed the entire negotiating gain from the renewal.

Where the terms were not supplied, the method assumes uncapped, because that is the conservative reading and the assumption is stated. Budget against the range, not the point.

## Levers that work

**Term length.** The most reliable lever the organization has, and the cheapest for the supplier to give. Longer term for better rate is the standard trade — but it spends optionality, and where the estate around the contract is changing, that optionality is worth more than the discount.

**Timing.** Suppliers have quarters and years. Aligning a decision with a supplier's period end is legitimate and effective, and it costs the organization nothing but planning.

**Scope precision.** Paying for what is used rather than what was bought years ago. Often the largest single reduction available, and it requires the consumption data the method keeps asking for.

**Date alignment.** Bringing several contracts to a common renewal date creates one window with scale instead of four with none. Underused, because the benefit lands a year later than the effort.

**Reference and advocacy.** Case studies, reference calls, speaking slots. Genuinely valuable to a supplier and cheap for the organization — worth trading deliberately rather than giving away as goodwill.

**Removing a genuine irritant.** Suppliers will trade real money for a resolved dispute, a cleaned-up payment history, or a consolidated purchase order process.

## Levers that do not work

**A threat the organization cannot execute.** Suppliers track this across renewal cycles. A walk-away claimed and not acted on in one cycle costs credibility in the next two.

**Volume the organization does not have.** Committing to growth that will not happen buys a rate and produces a shortfall.

**Pressure applied after the notice date has passed.** There is no lever left; there is only a request. The brief should say so rather than dressing it up.

**Escalation as a first move.** It works once, and it converts a working relationship into a managed one.

## Where architecture actually adds value

An architect brings three things procurement usually cannot get quickly, and they are worth more than an opinion on price:

- **The dependency map.** What actually stops if this lapses, named. It sets the true cost of failure and it is nearly always broader than assumed.
- **The substitutability read.** Whether an alternative could genuinely do this, at what integration cost, on what timeline. This is what makes leverage real or exposes it as a bluff.
- **The lock-in position.** Where the data is, what format it leaves in, what was built on top. Contractual exit terms and practical exit cost are frequently unrelated.

Bring those. Leave the price to the people who do it every day.
