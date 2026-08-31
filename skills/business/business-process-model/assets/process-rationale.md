# Process model — rationale

**Process:** {…} · **Purpose:** {automation | control assurance | handover or training | redesign}
**Confidence:** {low | medium | high}

## The process, and its boundaries

{Trigger, outcome, where it starts and stops, and what was deliberately excluded.}

## Where the procedure and the practice differ

{The most useful section in most runs. For each divergence: what the document says, what
people do, and — the part that matters — **why**.}

{The workaround is usually rational. Someone found the documented route did not work and
built a way around it, and the reason it did not work is normally the actual defect. State
the count as well as the examples: how many steps diverge is a measure of how much this
process depends on undocumented judgement, which is exactly what is lost when experienced
people leave.}

{Where no documented procedure was available, say so here rather than omitting the section —
its absence is a limitation of this run, not evidence that no gap exists.}

## What the controls actually cover

{Which failures are controlled, which are claimed to be controlled and are not, and which
controls produce no evidence that they ran.}

{Where the process is regulated, be explicit about what may not be removed regardless of
whether it adds value.}

## Steps that could not state what they prevent

{Named individually, with the effort each consumes. Recorded as ceremony, not removed —
removal is the control owner's call. Some of these are the only thing standing between the
process and a failure that happened before anyone currently involved started.}

## Where the process changes hands

{Handoffs, with what the receiver has to assume because it was not passed. Processes fail
at their seams far more often than inside their steps, and a handoff is owned by neither
role either side of it.}

## The paths off the standard route

{Exception paths, their volume share, and what they cost. Where volumes were not supplied,
say that the share is unknown rather than implying the exceptions are marginal.}

## What changes in the target design

{Only where a to-be was requested. Every change stated as a change against the as-is, with
what it assumes and what it costs. Include the changes that were considered and eliminated
by a hard constraint, with the policy ID.}

## What we assumed

| # | Assumption | Source | Affects | Penalty |
|---|---|---|---|---|
| A1 | {…} | {…} | {…} | {…} |

## How confident this is

**{low | medium | high}** — {derived from the confidence rules, naming the evidence used.}

{Where the model came from documentation or recollection alone, say plainly that it
describes the process as designed rather than as run, and that the divergence finding — the
most valuable one this method produces — is unavailable.}

## What would change this

{Sensitivity results. Include what happens if exception paths carry a third of the volume,
and what appears if every control that could not name its failure were removed.}

## What this model may and may not be used for

**May be used to:** {stated against the purpose it was built for.}

**May not be used to:**

- Size an implementation, where timings and volumes were estimated.
- Assure controls, where no audit or incident history was available — control effectiveness
  was judged from design rather than from outcome.
- Automate directly, where decision rules were inferred. **An inferred rule and a stated one
  look identical in a model and behave completely differently in an implementation.**
- Choose the system that will run the process, or design the interfaces between systems.
- Decide who should own the process. This records who does, and where that is unclear.
