---
name: integration-pattern-selection
description: >
  Selects the integration pattern for a use case — synchronous or asynchronous interface,
  publish and subscribe, queue, file transfer, data streaming, or partner document exchange —
  from the timing, volume, payload, delivery guarantee, and replay characteristics of the
  integration. Scores the realistic patterns against declared criteria, eliminates the ones
  the requirements rule out, and states the failure path for the pattern it recommends.
  Works from manual input; no integration tooling required.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.technology.integration-pattern-selection
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: technology
  yuman_ea_category: design
  yuman_ea_owner_agent: technology-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Integration Pattern Selection

Chooses how two systems should exchange data, from the measurable characteristics of the exchange rather than from what the team used last time.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The option set is fixed

Unlike most skills here, the options are declared by the method, not supplied by you. That is the point — the value is forcing consideration of the patterns nobody proposed in the meeting.

| Pattern | In one line |
|---|---|
| `api_synchronous` | Caller asks and waits for the answer |
| `api_asynchronous` | Caller hands over work, result arrives later by callback or polling |
| `publish_subscribe` | Producer broadcasts; any number of consumers subscribe |
| `queue_based` | Point to point, guaranteed delivery, receiver works at its own pace |
| `file_transfer` | Batches of records exchanged on a schedule |
| `data_streaming` | Continuous ordered event log, retained and replayable |
| `partner_document_exchange` | Industry-standard document formats across an organizational boundary |
| `direct_data_access` | One system reads another's data store directly |

**`direct_data_access` is in the set on purpose.** It is what teams reach for when integration is hard, it is almost always wrong, and a comparison that never mentions it does not help the person deciding. Score it honestly and let it lose on its merits.

## When not to use this

| The question | Use |
|---|---|
| What should the whole solution look like? | [`high-level-architecture`](../high-level-architecture/SKILL.md) — this answers its "Integration approach" section |
| Should we buy an integration platform? | [`build-vs-buy`](../build-vs-buy/SKILL.md) |
| Write our standard integration approach up as a reusable pattern | [`reference-architecture-pattern`](../reference-architecture-pattern/SKILL.md) |
| Record why we chose something, generally | [`architecture-decision-record`](../architecture-decision-record/SKILL.md) |

---

## Two rules that decide most of it

> **The timing answer comes first and eliminates half the set.** If the caller cannot proceed without the result, file transfer, publish-subscribe, and data streaming are out before anything is scored. Record the eliminations — options that quietly disappear read as an analysis that was steered.

> **"Real time" must become a number.** Nobody means the same thing by it. If the latency requirement cannot be stated as a figure and a percentile, that is a finding worth reporting on its own, and the run continues on the coarse answer with reduced confidence.

## Run it in this order

### 1. Frame

Restate the integration, naming both ends:

> Select the integration pattern for **{integration_purpose}**, carrying **{payload_profile}** at **{volume_and_frequency}**, where the caller **{response_timing}** and delivery must be **{delivery_guarantee}**.

### 2. Ask

Five questions, in `skill.yaml`. Two carry most of the weight:

- **`response_timing`** eliminates half the set, as above.
- **`replay_need`** separates streaming from queueing, and is the one most often skipped. A queue that has delivered its messages has forgotten them. Discovering that after a bad deployment, when someone asks to reprocess yesterday, is expensive.

`consumer_count` is a question about eighteen months from now, not today. One consumer today with more likely later is a publish-subscribe case, not a queue case.

### 3. Gather

Three required facts: **purpose**, **volume and frequency**, **payload profile**. State the peak separately from the average — averages design nothing.

`existing_integration_estate` carries a **high** confidence penalty when absent, and it is the input that most often decides the answer in practice:

> **Choosing a pattern the organization cannot operate is the most common way an integration design fails after approval.** A streaming platform is the right answer to a great many problems and the wrong answer for a team of two who have never run one.

### 4. Bound

Apply hard constraints before scoring and record each elimination with its policy ID. `customer_master_authority`-style rules routinely remove `direct_data_access`, and a reader needs to see that happen rather than wonder where it went.

### 5. Analyze

Seven criteria, 1-5 favourability, higher always better. Every score cites the evidence ID it rests on.

Inside the indifference band (0.3), report the patterns as too close to separate and apply the tie-breakers — the first of which prefers what the organization already runs.

**A combination can be the right answer.** Brokered events with a file-based backfill for recovery is a real design, not a failure to decide. Recommend it as a deliberate combination with its own failure path.

Background on what each pattern actually costs is in [`references/pattern-characteristics.md`](./references/pattern-characteristics.md); guarantees, ordering, and failure behaviour are in [`references/failure-paths-and-guarantees.md`](./references/failure-paths-and-guarantees.md). Neither is needed to run the method.

### 6. Deliver

| Artifact | File |
|---|---|
| Pattern recommendation | `integration-pattern-selection--pattern-recommendation.md` \| `.docx` |
| Pattern comparison | `integration-pattern-selection--pattern-comparison.md` \| `.csv` \| `.xlsx` |
| Decision record | `integration-pattern-selection--decision-record.md` |

**The failure path section is mandatory and is the one that gets skipped.** What happens when the receiver is down, what the sender does, where the data waits, how long it can wait, and who finds out. An integration design that documents only the happy path has documented the path that never causes an incident.

### 7. Verify

**Confidence** is derived. No quantified latency, or no peak volume, or an external interface designed without establishing what the partner can actually support, means `low`.

**Sensitivity** includes the test that matters most here:

> **Add a second consumer that nobody planned for.** What does it cost? This is the change that most often invalidates a point-to-point choice, and it usually arrives within a year of go-live.

---

## Standing rules

**No vendor or product names.** Patterns are described by behaviour — a broker, a stream, a scheduled file exchange. Which product implements it is a separate decision this skill does not take.

**State what the receiver must handle itself.** No pattern gives you everything. At-least-once delivery means the receiver must be idempotent, and saying so here is cheaper than a duplicate-billing incident later.

**Peak, not average.** Every volume figure in the output is a peak figure or is labelled as an average.
