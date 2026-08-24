# {Source} to {target} — pattern comparison

**Date:** {YYYY-MM-DD} · **Caller:** {waits | continues | scheduled} · **Consumers:** {…}
**Delivery:** {…} · **Replay:** {…} · **Confidence:** {low | medium | high} — {reason}

> Scores are **favourability on a 1-5 scale**, not magnitude. A pattern that handles the
> volume comfortably scores high on volume fit; it does not show the throughput here.

## Summary

| Pattern | Weighted score | Verdict |
|---|---|---|
| api_synchronous | {0.00} | {recommended \| viable \| eliminated} |
| api_asynchronous | {0.00} | |
| publish_subscribe | {0.00} | |
| queue_based | {0.00} | |
| file_transfer | {0.00} | |
| data_streaming | {0.00} | |
| partner_document_exchange | {0.00} | |
| direct_data_access | {0.00} | |

**Gap between the top two:** {0.00} — indifference band is 0.30. {Inside or outside, stated
explicitly. Inside it, no single pattern is recommended and the tie-breakers apply.}

## Eliminated before scoring

| Pattern | Eliminated by | What it says |
|---|---|---|
| {pattern} | response_timing = caller_waits | Cannot return a result to a waiting caller |
| {pattern} | {policy_id} | {the constraint as the organization states it} |

*State "None" explicitly if nothing was eliminated.*

## Scores

| Pattern | Criterion | Score | Weight | Weighted | Evidence | Assumption | Score confidence |
|---|---|---|---|---|---|---|---|
| {pattern} | timing_fit | {1-5} | 0.20 | {0.00} | {evidence_id: the specific fact} | {A1, or blank} | {low \| medium \| high} |
| {pattern} | delivery_semantics_fit | | 0.20 | | | | |
| {pattern} | estate_fit | | 0.15 | | | | |
| {pattern} | coupling_and_resilience | | 0.15 | | | | |
| {pattern} | volume_and_payload_fit | | 0.15 | | | | |
| {pattern} | operability | | 0.10 | | | | |
| {pattern} | change_tolerance | | 0.05 | | | | |

**Evidence** names the input the score rests on and the fact taken from it — not a
restatement of the criterion. "Scored 2 on estate fit because the register shows no
streaming interface anywhere and integration is supported by 2.1 FTE" can be argued with.
"Scored 2 on estate fit" cannot.

## Weights used

| Criterion | Default | Used | Changed by |
|---|---|---|---|
| timing_fit | 0.20 | {0.00} | {overlay \| renormalization \| unchanged} |
| delivery_semantics_fit | 0.20 | | |
| estate_fit | 0.15 | | |
| coupling_and_resilience | 0.15 | | |
| volume_and_payload_fit | 0.15 | | |
| operability | 0.10 | | |
| change_tolerance | 0.05 | | |

*Must sum to 1.00.*

## Assumptions this comparison depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {criteria affected} | {low \| medium \| high} |

## What would change the ranking

| Varied | How | Result |
|---|---|---|
| Peak volume | ×10 | {which pattern changes, and what becomes the constraint first} |
| Consumers | Add one nobody planned for | {what it costs under the recommended pattern} |
| Maximum payload | ×10 | {does it still carry, or does the design pass a reference instead} |
| Latency requirement | Halved | {does the recommendation survive a stricter figure} |

## Tie-breakers

*Include only when the top two are inside the band. Apply in order and show which resolved it.*

1. The organization already runs it.
2. Tolerates a second consumer without redesign.
3. Simpler failure path — fewer places a message can be sitting when someone asks where it is.
4. Still tied — report the tie and name the one measurement that would break it.
