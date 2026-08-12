# Turning vague non-functional wishes into targets you can design against

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when the non-functional requirements are missing, which is most of the time.

## Why this is the input that matters most

An architecture is shaped almost entirely by its quality attributes. The same functional requirements produce completely different architectures at 99.5% availability and at 99.95%, at a thousand transactions an hour and at a hundred thousand.

So the input most often absent is also the one that most changes the answer. **The failure this file exists to prevent is an availability target invented in passing, designed against for six months, and never confirmed.** By the time somebody checks, the architecture is built.

The skill's declared behaviour is `estimate_with_assumption` with a **high** confidence penalty, and a specific labelling rule: derived targets are written as **proposals for confirmation**, never as findings.

## "It needs to be fast and reliable" is not a requirement

It cannot be designed against, tested against, or argued with. A usable target has four parts:

| Part | Example |
|---|---|
| **The condition** | When a trade customer submits an order |
| **The measure** | The confirmation returns |
| **The value** | Within 2 seconds |
| **When it applies** | At the Monday morning peak, 95th percentile |

*"When a trade customer submits an order at the Monday peak, the confirmation returns within 2 seconds at the 95th percentile."* That is testable, it can be traced to a part of the architecture, and a business sponsor can tell you it is wrong.

The last part is the one that gets dropped and the one that decides the architecture. A two-second average with no peak qualifier is met by a system that is unusable every Monday.

## Deriving targets when none exist

Ask two questions, in this order. They get you further than a requirements workshop.

**"What happens to the business if this is unavailable for an hour?"** The answer is usually concrete — orders stop, drivers wait, a shift cannot be scheduled — and it converts directly into an availability class and a recovery target. "Nothing much until the next morning" is a genuine and useful answer that saves a great deal of money.

**"What is the busiest hour, and what happens in it?"** Peaks drive architecture; averages drive nothing. A distributor whose orders arrive across two hours on a Monday has a different architecture from one with the same weekly volume spread evenly.

Then anchor to what already exists. **The systems this solution replaces or sits alongside are the best available evidence**, and they are in the inventory: business criticality, user counts, and the current run cost all say something about the expectation the organization already has. Deriving from those and saying so is honest. Reaching for an industry figure is not.

### Write the assumption like this

> "A1. No non-functional requirements were supplied. Availability of 99.5% during business hours has been proposed, derived from the business criticality recorded against the systems this replaces and from the answer that an hour's outage stops order taking but is recoverable the same day. **This is a proposal for confirmation, not a finding.** Decisions D2 and D5 rest on it; if the confirmed target is 99.9% or better, both reverse."

The last clause is what makes the assumption usable. An unconfirmed target with a named consequence gets confirmed. One without gets accepted by silence.

## The attributes worth a target on almost every solution

| Attribute | The question that produces the number |
|---|---|
| **Availability** | What happens to the business during an hour of downtime? Does it differ in and out of business hours? |
| **Performance** | What must feel instant to whom, and at which peak? |
| **Capacity and growth** | Today's peak, and the multiple to design headroom for over the horizon |
| **Recovery** | How much data can the business afford to lose, and how long can it wait to be back? |
| **Retention** | How long must this be kept, and who asks for it — an auditor, a regulator, a customer? |
| **Security** | What is the worst disclosure, and what evidence would a reviewer be shown? |

Six is usually enough at high level. Producing twenty makes the document longer and the architecture no better.

## Recovery: ask for both numbers separately

How much data the business can afford to lose, and how long it can wait to be running again, are different questions with different architectural answers, and people conflate them constantly. "We can't lose anything and we need it back immediately" is a request for the most expensive architecture available, and it is almost never what the business actually needs when the cost is put next to it.

Put the cost next to it. The conversation changes.

## Testing the target against the architecture

For each attribute, the document states the **mechanism** that meets it, not the aspiration.

- Weak: "The system will be highly available."
- Usable: "Two instances behind a load balancer across availability zones; the session cache is replicated; a single instance failure is transparent to the user and a zone failure costs under a minute of reconnection."

If no mechanism can be written for an attribute, the architecture does not meet it yet, whatever the document says. That is a finding, and it belongs in the risk table rather than being smoothed over.

## Where this connects to the rest of the skill

- Derived targets go in the **assumptions register**, marked as proposals.
- Every decision resting on one is marked in the **decision log**, in its own table.
- The **sensitivity analysis** varies the availability target one step in each direction and reports which decisions change. Where the targets were derived rather than supplied, that paragraph is the most valuable one in the document.
- Confidence is `low` while any of this is true. That is not pessimism — it is the difference between a document that gets confirmed and one that gets believed.
