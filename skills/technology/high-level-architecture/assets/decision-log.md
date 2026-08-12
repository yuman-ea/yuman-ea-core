# {Solution name} — architecture decision log

**Architecture version:** {0.1} · **Date:** {YYYY-MM-DD} · **Recommended option:** {opt-n}

> **What belongs here.** Decisions that would be **expensive to reverse** — the shape of
> the data, where the boundary sits, the integration style, the hosting position, the
> identity model. A decision that could be changed in a sprint does not belong in this
> log, and a log of forty entries is a design document rather than an architecture.
>
> This log outlives the project. Write each entry for somebody joining in two years who
> cannot find anyone who was there.

## Decisions

### D1 — {the decision, in the active voice}

| | |
|---|---|
| **Status** | {proposed \| accepted \| superseded by D#} |
| **Options considered** | {…} |
| **Chosen** | {…} |
| **Driving criterion** | {requirements_fit \| nonfunctional_fit \| estate_coherence \| delivery_feasibility \| operability \| security_and_data_protection \| change_tolerance \| cost_and_run_burden} |
| **Forced by constraint** | {policy_id, or "not forced — chosen on the assessment"} |
| **Rests on assumption** | {A#, or blank} |

**Rationale.** {In business language. The reason, not the score. "Orders have to keep
being taken while the warehouse system is down, so the two are decoupled through the
broker" — not "estate_coherence scored 4".}

**Consequences.** {What this commits the organization to, and what it closes off. The
second half is what a future reader will care about most.}

**What would make us revisit this.** {An observable trigger, not "if circumstances
change". "If peak volume passes {N} per hour." "If the availability target is confirmed
stricter than the assumed {value}." "At contract expiry in {date}."}

---

### D2 — {…}

{Repeat the block.}

---

## Decisions resting on a proposed target

*Where non-functional targets were derived rather than supplied, list every decision that
depends on one. This table is what a review board should read first.*

| Decision | Proposed target it rests on | If the real target is stricter | If it is looser |
|---|---|---|---|
| D# | {A#: availability {value}} | {what changes} | {what becomes unnecessary} |

*State "None — all targets were supplied" explicitly where that is true. It is the
strongest sentence in the document when it is honest, and the most damaging when it
is not.*

## Decisions deliberately deferred

| Deferred decision | Why now is the wrong time | Who decides, and by when |
|---|---|---|
| {…} | {…} | {…} |

*Deferring is a legitimate architectural act. Deferring silently is not — an unrecorded
deferral reads to a delivery team as a decision that was made and not written down.*
