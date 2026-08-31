---
name: value-stream-map
description: >
  Maps how value reaches the stakeholder who triggered the work — stage by stage, with the
  value each stage adds, the capabilities it consumes, and where the flow sticks. Measures
  waiting as well as working, because elapsed time in most streams is dominated by queues
  between stages rather than effort within them, and locates friction at handoffs rather
  than inside the teams either side of them. Produces the stream map, a capability
  cross-map, a friction register, and the reasoning behind all three.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.value-stream-map
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: discover
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Value Stream Map

Shows how value actually reaches the person who triggered the work, and where it stops moving.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## What makes it a stream and not a process

Three things, and all three are required:

1. **A trigger** — something a stakeholder does that starts it.
2. **A recipient** — someone who ends up holding value.
3. **Value they can recognise** at the end.

If it ends at an internal handoff rather than at value reaching someone, it is a process. Say so and route to [`business-process-model`](../business-process-model/SKILL.md) rather than mapping it as a stream — the two look similar on a whiteboard and support completely different conclusions.

## The three things this method exists to find

> **1. The queue, not the work.** In most unmeasured streams, value-adding time is **under ten per cent** of elapsed time. Teams report their own work time accurately and have no visibility of the queue in front of them, so a map built from self-reported durations finds a stream that is entirely efficient and takes six weeks.
>
> Work time and wait time are captured **separately**, always. A single duration per stage conceals the answer.

> **2. Friction at the handoff.** Between stages, between functions, between systems. Friction belongs to nobody, which is exactly why it survives every round of local improvement — each team either side has optimised its own part and is correct that the problem is not theirs.

> **3. The stage nobody can name the value of.** It usually exists to serve an internal arrangement that no longer exists. Do not optimise it: report it as a candidate for removal, and name who would have to agree.

## Start boundary is a finding, not a setup step

Streams are routinely drawn starting at the moment work arrives in the department that commissioned the map.

That excludes everything the customer did to get it there — which is frequently where most of the elapsed time sits, and always where the complaints come from. `boundary_confidence` makes it an explicit question, and a contested boundary changes what the map is allowed to conclude.

## Status comes from the pattern

The weighted score orders stages for attention. The **status** comes from which criterion drove it, because these need different interventions:

| Status | What it means | What it needs |
|---|---|---|
| `queue_bound` | The time is in the wait, not the work | Capacity, batching, or prioritisation |
| `rework_bound` | Work arrives wrong and goes back | A fix in the stage **before** |
| `handoff_bound` | The cost is in the transfer | An owner for the seam |
| `no_stated_value` | Nobody could say what it adds | A decision to stop, not an improvement |
| `flows` | Nothing here needs a decision | — |
| `insufficient_evidence` | Could not be assessed | Say so |

Rules are in [`references/flow-analysis-rules.md`](./references/flow-analysis-rules.md).

## When not to use this

| The question | Use |
|---|---|
| What does the customer experience, and on which systems? | [`customer-journey-to-system-map`](../customer-journey-to-system-map/SKILL.md) |
| How does this one process run, with its controls? | [`business-process-model`](../business-process-model/SKILL.md) |
| What does the organization do, as capabilities? | [`business-capability-map`](../business-capability-map/SKILL.md) |
| How should we be organized to run it? | [`operating-model-design`](../operating-model-design/SKILL.md) |
| Which systems should we replace? | [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) |

---

## Run it in this order

### 1. Frame

Confirm trigger, recipient, and value. Then **test the start boundary** before anything else.

### 2. Ask

Five questions. `timing_evidence` caps the confidence of the whole run, and `path_coverage` decides whether the map finds anything: a stream where four items in five flow through in days and one takes weeks has an average nobody experiences.

### 3. Gather

Three required: the **stream definition**, the **stage sequence as it actually runs**, and the **stage evidence**.

Two optional inputs carry a **high** penalty and are the two the analysis rests on:

| Input | Why |
|---|---|
| `elapsed_and_work_time` | Work and wait, separately. The gap is the finding |
| `rework_and_exception_rates` | Rework is counted as work and is invisible in stage times |

`system_touchpoints` degrades to the inventory and interface map — which finds the automated handoffs and **misses every one carried by email, spreadsheet, or phone call**, disproportionately where the friction is. The assumption says so.

### 4. Bound

`segregation_of_duties` is a hard constraint. A stage merge that breaks it is eliminated rather than scored down, and the elimination is reported with the policy ID.

### 5. Analyze

Lay out stages **as people describe doing them**, not as the procedure says. Where the two differ, record both — the difference is a finding.

Then separate work from wait, compute the flow ratio, locate friction at the handoffs, and cross-map to capabilities in **both** directions.

### 6. Deliver

| Artifact | File |
|---|---|
| Value stream map | `value-stream-map--value-stream-map.md` \| `.csv` \| `.xlsx` |
| Capability cross-map | `value-stream-map--capability-cross-map.md` \| `.csv` \| `.xlsx` |
| Friction register | `value-stream-map--friction-register.md` \| `.csv` \| `.xlsx` |
| Stream rationale | `value-stream-map--stream-rationale.md` \| `.docx` |

**Report the flow ratio.** Value-adding time as a share of elapsed time reframes the conversation faster than any individual stage finding, and it is a single number.

**The friction register names a root stage.** The cause of rework is usually the stage *before* the one where it shows up, and pointing the improvement at the wrong stage is the most common way effort is wasted here.

### 7. Verify

**Confidence** is `low` if wait time was not separated from work time — even where the map is otherwise complete. A stream mapped without its queues has measured the wrong thing thoroughly.

**Sensitivity** includes the one that most often moves the answer:

> **Wait time doubled at every handoff.** Where timings were self-reported, the queue is the component nobody could see, and doubling it is closer to reality than the reported figure.

---

## Standing rules

**Work time and wait time are two numbers.** Never one.

**Improve the constraint or improve nothing.** Improving a stage that is not the bottleneck changes end-to-end time by exactly zero, and it is where most improvement effort goes.

**Friction is located between stages.** Recording it inside one of them assigns it to a team that cannot fix it alone.

**A stage with no stated value is reported, not optimised.** Making an unnecessary stage faster is the most expensive kind of improvement.

**The capability cross-map runs both ways.** Stages consume capabilities, and capabilities the model claims that no stage uses are a finding about the model.
