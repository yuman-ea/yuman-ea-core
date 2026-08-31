# Flow analysis rules

This reference constrains **how stage scores become a status, and what the timings are allowed to conclude**. Background, loaded on demand.

## Work time and wait time are two numbers

Never one. This is the single rule that decides whether the map finds anything.

Teams report their own work time accurately. They have no visibility of the queue in front of their stage, because it is not happening to them — it is happening to an item sitting in a list. So a map assembled from self-reported durations shows a stream in which every stage is efficient and the whole thing takes six weeks, and it offers nothing to act on.

Where only a single duration per stage is available, it is a **work time**, and the wait is unmeasured. Record it that way. Do not distribute the missing elapsed time across the stages to make the arithmetic close — that invents the exact quantity the analysis exists to find.

## The flow ratio

$$\text{value-adding share} = \frac{\text{value-adding work time}}{\text{total elapsed time}}$$

Report it as a single number, early.

In most streams that have never been measured this lands somewhere under ten per cent, and frequently under three. The figure is far more persuasive than any individual stage finding, because it is not arguable in the way a stage judgement is — it reframes the question from "who is slow" to "why is nothing moving", which is the correct question and a much less defensive one.

Two cautions. It is a ratio of *elapsed* time, so it says nothing about efficiency of effort — a stream can be 2% value-adding and use every person in it fully. And it degrades badly with poor timing evidence: where wait time was not measured, the ratio is unknown rather than high.

## Status rules

Applied in this order. The first that matches wins.

| # | Status | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | No timing basis, or two or more criteria unscoreable |
| 2 | `no_stated_value` | Nobody in the stream could state what value the stage adds to the recipient |
| 3 | `rework_bound` | Rework or exception rate is the worst score, and material |
| 4 | `queue_bound` | Wait time at or into this stage is the dominant share of its elapsed contribution |
| 5 | `handoff_bound` | Handoff friction is the worst score — several teams, systems, or re-keyings to enter the stage |
| 6 | `flows` | Everything else |

`no_stated_value` sits above the diagnostic statuses on purpose. A stage that should not exist does not need a queue analysis, and optimising it is the most expensive kind of improvement available.

## The constraint, and why only it matters for speed

Exactly one stage is the constraint. Improving any other changes end-to-end elapsed time by **nothing**.

This is worth stating flatly because it contradicts how improvement effort is usually allocated — spread across whichever stages have willing owners and visible problems. Those improvements are often worth making for cost, error, or morale. They will not make the stream faster, and promising that they will is how improvement programmes lose credibility.

When the constraint is relieved, it moves. Say where it moves to, because the second constraint is usually much harder than the first and knowing that in advance changes what people commit to.

**And the constraint is frequently not a stage at all.** It is often a handoff, an approval that runs weekly, or a person who is the only signatory. A map that can only nominate stages will nominate the wrong thing.

## Rework points backwards

Rework appearing at a stage is nearly always caused by the stage *before* it — work arrives incomplete, ambiguous, or wrong, and the receiving stage absorbs the correction.

So the register records both where rework **appears** and where its **root** is. Pointing an improvement at the stage where the rework is visible is the most common misdiagnosis in flow work, and it produces a stage that gets better at handling bad input, which entrenches the actual problem.

Rework is also invisible in stage timings, because from inside the stage it is simply work. A stage with 40% rework and a stage with none can report identical durations.

## Friction belongs to the handoff

Friction between two stages is recorded **between** them, not inside either.

The reason is ownership rather than tidiness. Recorded inside a stage, the friction is assigned to a team that cannot resolve it alone; both teams either side have optimised their own part, both are correct that the problem is not theirs, and it survives indefinitely. Recorded at the seam with `owned_by: nobody`, it becomes a question about ownership — which is usually the actual intervention.

## What the analysis may not conclude

**That a system should be replaced.** Friction at a system boundary is a finding. The disposition belongs to `application-rationalization`, which weighs things this method never sees.

**That a team is underperforming.** Elapsed time is a property of the stream. A stage taking three weeks is more often starved, batched, or waiting on an approval than slow.

**That the to-be is achievable.** Where a future shape is drawn, it is a shape. Sequencing it against capacity is `roadmap-sequencing`, and the difference between a to-be map and a plan is the difference between an aspiration and a commitment.
