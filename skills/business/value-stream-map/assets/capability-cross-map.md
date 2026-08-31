# Capability cross-map — {stream name}

**Capability source:** {existing model | **derived from stage names**}
**Confidence:** {low | medium | high}

> Where capabilities were **derived from the stage names**, this cross-map is circular — the
> stages defined the capabilities that are then mapped back to the stages — and it cannot
> find capabilities that no stage consumes. Say so rather than presenting it as a check.

## Stage to capability

| Stage | Capability | Dependency | Support | Supporting systems | If the capability were absent |
|---|---|---|---|---|---|
| {…} | {…} | {critical \| contributing \| incidental} | {adequate \| strained \| absent \| not assessed} | {…} | {…} |

## Capabilities under strain

| Capability | Stages depending on it | Where it strains | Consequence in the stream |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

*A stage failing because the capability behind it is immature cannot be fixed by changing
the stage. This table is how those two diagnoses are kept apart.*

## Capabilities the model claims that no stage uses

| Capability | In the model because | Used by any mapped stream? |
|---|---|---|
| {…} | {…} | no |

*Only meaningful where an existing capability model was supplied. This is the reverse check,
and it is a finding about the model rather than about the stream — a capability nothing
consumes is either aspiration, or evidence that the streams mapped so far are incomplete.*

## Capabilities consumed by several stages

| Capability | Stages | Why this matters |
|---|---|---|
| {…} | {…} | {a shared capability is a shared constraint: improving it moves several stages, and degrading it stops them all} |
