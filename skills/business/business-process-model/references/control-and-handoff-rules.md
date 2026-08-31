# Control and handoff rules

This reference constrains **how step scores become a status, what qualifies as a control, and how handoffs are recorded**. Background, loaded on demand.

## A control names the failure it prevents

The test is one question, asked of every step believed to be a control:

> **What goes wrong if this step does not happen?**

A specific answer — "an order ships to an account over its credit limit", "a payment is released without a second approver" — qualifies. "It is part of the process", "audit asked for it", and "we have always done it" do not.

A step failing the test is recorded as `ceremony`. It is **not removed.** Removal is the control owner's decision, and this method has two reasons to be careful about it:

- Some ceremony is the residue of a real failure that happened before anyone currently involved started, and the reason has simply been forgotten. The step is doing something; nobody can say what.
- In a regulated process, a step may be mandatory whether or not it adds value. Removing it creates an exposure that nobody costed and that will not surface until an inspection.

What the method does contribute is the effort each ceremonial step consumes, so that the decision is made with a number attached.

## Three kinds of control, and evidence for all of them

| Type | Acts | Example question it answers |
|---|---|---|
| Preventive | Before the failure | Can the wrong thing happen at all? |
| Detective | After the failure | Would we know if it had? |
| Corrective | After detection | What puts it right, and how fast? |

Every one of them needs **evidence that it ran**. A control producing no evidence cannot be assured — it may well work, and nobody can demonstrate it, which in an audit is the same position as not having it.

A control that has never been tested against a real failure is an intention. Record it as such: `tested_against_real_failure: false` is not a criticism, it is the difference between a control that is known to work and one that is believed to.

## A claimed control that does not work is worse than a gap

Worth stating plainly because it inverts the intuition.

A known gap gets compensating attention — people are careful, someone checks informally, the risk is on a register. A control everyone believes in gets none of that, and it fails silently the first time it matters. This is why `control_gap` outranks almost everything else in the status rules.

## Status rules

Applied in this order. The first that matches wins.

| # | Status | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | The step could not be described from any evidence, or two or more criteria are unscoreable |
| 2 | `control_gap` | A failure is claimed to be controlled at this step and the control would not prevent it, or produces no evidence |
| 3 | `unmodelled_exception` | A path off this step carries material volume and is not in the model |
| 4 | `ceremony` | The step is believed to be a control and could not name what it prevents |
| 5 | `handoff_risk` | Handoff integrity is the worst score — information the receiver needs is not transmitted |
| 6 | `unclear_decision` | A decision step where nobody could state the criteria or the authority |
| 7 | `undocumented_variance` | The observed step differs from the documented one, with no other status applying |
| 8 | `sound` | Everything else |

`undocumented_variance` sits low deliberately. It is a finding rather than a fault, and where it coincides with a real problem one of the statuses above will have caught it. A step that diverges from the procedure and works better is still worth recording — and it is not a defect.

## Handoffs: record what does not pass

Every handoff records what is transmitted. The column that earns its place is the other one: **what the receiver has to assume because it was not transmitted.**

That is where processes fail. The sending role knows the context, judges that it is obvious, and passes the artifact without it. The receiving role fills the gap with an assumption that is right most of the time. The residual is rework, and it appears in the receiving stage's numbers rather than the sending one's.

Two practical notes:

- **Friction at a handoff is owned by nobody.** Both roles have optimised their own side and both are correct that the problem is not theirs. Recording the handoff as an entry in its own right, rather than as a property of either step, is what makes an owner assignable.
- **Manual crossings are invisible to inference.** Where system touchpoints were derived from an application inventory and interface map, only automated handoffs appear. Re-keying, spreadsheets, and email are exactly where information is lost, and they will be under-represented unless someone was asked.

## Rework points backwards

Rework appearing at a step is usually caused by the step before it. Record where it appears and where its root is, and aim the improvement at the root.

Pointing it at the step where rework is visible produces a step that becomes very good at handling bad input, which entrenches the cause and looks like progress for about two quarters.

## Segregation of duties is a hard constraint

A proposed to-be step in which one role both initiates and approves is **eliminated**, not scored down, and the elimination is reported with the policy ID.

This is the constraint most often breached by a well-intentioned redesign, because merging two steps performed by two roles is the most obvious efficiency available in any process and the reason those two roles exist is frequently not written anywhere.
