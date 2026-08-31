# Process modelling rules

This reference constrains **what gets modelled, at what depth, and how the as-is is established**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## Model the process as run

The documented procedure and the observed process differ in almost every process older than a couple of years. The model is of the **observed** one; the document is a separate input, compared against it.

This is the rule most often broken, and it is broken with good intentions. A modeller shown a workaround naturally records the correct step instead — the document says so, the workaround looks like an error, and correcting it makes a tidier model. It also erases the single most valuable finding available and produces a model of a process nobody runs.

The right question at every divergence is not "which is correct?" but **"why does the workaround exist?"** Almost always the documented route failed in some specific way, and that failure is the actual defect.

## Depth follows purpose

| Purpose | Model to |
|---|---|
| Automation | Every decision rule explicit, every input and output typed, every exception path present |
| Control assurance | Every control, what it prevents, and the evidence it produces |
| Handover or training | The judgement calls and the exceptions — the parts an experienced person knows and a document does not say |
| Redesign | Enough to see where effort and delay sit, and what the constraints are |

Modelling for all four at once produces something too dense for any of them. It is also the commonest way a process model becomes an artifact nobody maintains, and **a coarse model that stays true is worth more than a detailed one that goes stale.**

Stop when the reader can act. Further decomposition is not more rigour.

## Lanes are roles

Never individuals. A model naming people is obsolete at the next departure, unusable for capacity work, and awkward to circulate.

Where a step's lane is contested — two roles each believe the other does it, or both do it inconsistently — record the contest rather than assigning it. That is where the process stalls under pressure, and it is invisible once a lane has been picked.

## Exceptions are part of the process

The standard path is the part everyone already understands. It is not where the effort is, and it is not where the risk is.

Exception paths routinely carry a third of the volume. Where they are excluded, say which ones and what share they carry, so a reader can judge what the model does not cover. Where volumes are unknown, say the share is unknown — implying exceptions are marginal is worse than saying nothing, because it is the assumption an automation business case will silently inherit.

A useful prompt for finding them: *what happened the last five times this did not go as planned?* People recall specific incidents far more reliably than they describe general variation.

## Decision points need three things

At every gateway: **the criteria**, **who has authority**, and **what they may not decide alone.**

The third is the one that gets missed and the one that matters. A decision that can be made by a role up to a threshold and needs escalation above it looks like a single decision in most models, and behaves like two.

Mark inferred rules. An inferred rule and a stated one are indistinguishable in a model and behave completely differently in an implementation — this is the specific mechanism by which automation projects reproduce the usual case correctly and get every escalation wrong.

## On notation

The model is BPMN-shaped: pools and lanes, tasks, gateways, events, sequence flow. It is expressed as a table because a table renders in every host, and the table carries everything needed to draw the diagram where a host can draw one.

BPMN is cited as a notation. The specification is not reproduced, and no part of this method requires a reader to know it — the `step_type` values are ordinary words for ordinary things, and a model that needs a notation guide to read has failed the business-language rule this project applies to every deliverable.

Where a diagram is rendered, it is a view of the table, not a second source. Two representations that can drift is one representation too many.

## A to-be needs an as-is

Where both exist they share step IDs, so the model can be diffed and every change reads as a change.

`to_be_only` is legitimate and sometimes the only option — a process that does not exist yet has no as-is. It carries a limitation that must be stated: without the current process written down, nobody can assess the risk of the change or tell whether the design solves the actual problem, because the actual problem was never recorded.

The failure mode to watch for is a to-be presented as an as-is. It happens when the modeller works from the documented procedure in an organization that does not follow it — the result describes a process that exists only on paper, and it will be signed off by people who have never performed it.
