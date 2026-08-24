# Sequencing rules

This reference constrains **how priority order becomes a wave assignment**. The weighted score is a claim on an early wave; it is not the placement.

Background, loaded on demand. The method in [`SKILL.md`](../SKILL.md) is complete without this file.

## Order of application

Placement is constrained before it is optimized. Apply in this order, because each step narrows what the next may choose from:

1. **Hard constraints** — change freezes and budget ceilings remove wave slots outright.
2. **Fixed dates** — a contract expiry or regulatory deadline sets the *latest* wave an initiative may occupy. An input, never something the sequence may move.
3. **Dependencies** — an initiative cannot precede what it depends on, and a soft dependency sets an overlap rather than an ordering.
4. **Capacity** — after in-flight commitments are subtracted and slack is reserved.
5. **Priority score** — chooses among whatever remains feasible.

Running these in the wrong order produces the characteristic bad roadmap: a sequence optimized for value, then adjusted for reality, in which every adjustment looks like a compromise rather than a constraint — and is argued about as if it were one.

## Placement reasons

Every initiative records why it landed where it did:

| Reason | Meaning |
|---|---|
| `priority_order` | It scored its way there and nothing constrained it |
| `dependency_constrained` | It could not be earlier; something it needs is not ready |
| `fixed_date_constrained` | A date that will not move pulled it earlier |
| `capacity_constrained` | It scored for an earlier wave and there was no room |
| `freeze_constrained` | A change freeze removed the wave it would have taken |
| `does_not_fit` | No wave within the horizon can accommodate it |
| `beyond_horizon` | Feasible, but later than the plan extends |

**A plan where every reason is `priority_order` has no constraints in it**, which in a real organization means the constraints were not looked for.

## Never compress to fit

The single rule that decides whether the plan is worth anything.

When an initiative does not fit, the available moves are: **reduce its scope, add capacity, or move a date.** All three are organizational decisions. What the method may not do is assume any of them silently — a smaller effort figure, a faster dependency resolution, a wave that quietly absorbs 110% of capacity.

A plan that fits because the arithmetic was adjusted fails in wave two, and it fails having spent the credibility that would have made the hard conversation possible in wave one. **The infeasible plan, reported as infeasible with the three options named, is the more useful document.**

## Enablers are placed first

An initiative two or more others depend on is an enabler. Enablers are placed before what they unblock, and the placement is checked explicitly: **an enabler in a later wave than something it unblocks means the plan does not work.**

This needs a rule rather than falling out of the dependency graph, because of funding. Enablers have no business case of their own — the benefit accrues to the initiatives they unblock — so they arrive unsponsored, undersized, and easy to cut. The graph places them correctly and the organization removes them anyway, unless they are named as enablers in front of whoever is doing the cutting.

## Waves are not evenly sized

A common instinct is to balance waves so each carries similar effort. Resist it.

Wave one is usually smaller, because it is where the organization is least certain and where the plan learns. Later waves absorb more once dependencies have resolved and sizing has improved. **A perfectly balanced plan is usually a plan that was fitted to the waves rather than derived from the work.**

## When the horizon is the constraint

Where an initiative is feasible but falls outside the planning window, record it as `beyond_horizon` rather than dropping it.

The distinction matters because **the horizon is arbitrary and the consequence is not.** A twelve-month horizon turns "wave five" into "never" without anyone deciding to cancel anything. Naming what fell outside is how that decision gets made deliberately, and it is frequently the argument that extends the horizon.
