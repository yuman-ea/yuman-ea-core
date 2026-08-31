# Control and handoff register — {process name}

**Control regime:** {regulated | internally audited | no formal regime}
**Confidence:** {low | medium | high}

## Controls

| # | At step | Prevents | Type | Evidence it ran | Performed by | Policy | Tested against a real failure? |
|---|---|---|---|---|---|---|---|
| C1 | {…} | {the specific failure — or **none stated**} | {preventive \| detective \| corrective} | {…} | {role} | {policy ID only} | {yes / no} |

*A control producing no evidence cannot be assured, whatever it prevents. A control never
tested against a real failure is an intention — this register cannot distinguish one that
works from one that has simply never been needed.*

## Steps that could not state what they prevent

| # | Step | Believed to be a control because | Effort it consumes |
|---|---|---|---|
| {…} | {…} | {inherited, requested once, nobody remembers} | {…} |

*Recorded as `ceremony`, **not removed**. Removal is the control owner's decision, and some
of what looks like ceremony is the only thing standing between the process and a known
failure that happened before anyone here started.*

## Where a failure is claimed to be controlled and is not

| # | The failure | Believed control | Why it does not prevent it |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

*A control believed to be working is worse than a known gap, because nothing compensates
for it.*

## Handoffs

| # | From lane | To lane | What passes | In what form | **Receiver must assume** | Cost when it goes wrong |
|---|---|---|---|---|---|---|
| H1 | {…} | {…} | {…} | {system record \| form \| email \| spreadsheet \| verbal} | {what was NOT passed and has to be taken on trust} | {…} |

*The "receiver must assume" column is where processes fail. Everything in it is information
the process depends on and does not transmit.*

## Handoffs across a system boundary

| # | Between | What crosses | How | Re-keyed? |
|---|---|---|---|---|
| {…} | {system A → system B} | {…} | {interface \| export \| **manual re-entry**} | {yes / no} |

*Where system touchpoints were inferred from the inventory, only automated crossings are
visible. Steps carried by spreadsheet, email, or a shared document will be under-represented
here, and those are usually the ones where information is lost.*

## Segregation of duties

| Steps | Same role performs | Constraint | Status |
|---|---|---|---|
| {…} | {…} | {segregation_of_duties} | {satisfied \| **breached** \| not assessed} |
