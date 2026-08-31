# Process model — {process name}

**Trigger:** {…} · **Outcome:** {…}
**Boundaries:** starts at {…}, ends at {…}
**State:** {as-is only | as-is and to-be | **to-be only**}
**Evidence:** {observed | walkthrough with performers | **documentation only** | **recalled**}
**Purpose:** {automation | control assurance | handover or training | redesign}
**Control regime:** {regulated | internally audited | no formal regime}
**Confidence:** {low | medium | high} — {reason}

> Modelled to the level this purpose requires and no further. Detail beyond that point is
> not more rigour; it is a model nobody will maintain.

## Lanes

| Lane | Role accountable | Steps |
|---|---|---|
| {…} | {a role, never an individual} | {…} |

*A step whose lane is contested is a finding, and it is where the process stalls under
pressure.*

## As-is — standard path

| # | Step | Type | Lane | In | Out | System | Decision rule | Status | Differs from procedure |
|---|---|---|---|---|---|---|---|---|---|
| 1 | {…} | {start_event \| task \| user_task \| service_task \| decision \| handoff \| wait \| control \| end_event} | {…} | {…} | {…} | {…} | {criteria, authority, limits — **marked where inferred**} | {…} | {yes / no} |

## As-is — exception paths

| # | Step | Branches from | Trigger for this path | Volume share | Type | Lane | Status |
|---|---|---|---|---|---|---|---|
| {…} | {…} | {step #} | {…} | {…%} | {…} | {…} | {…} |

*Modelled at the same depth as the standard path where volume is material. Exceptions in
footnotes are exceptions that get discovered during implementation.*

## Rework loops

| From | Back to | Why work returns | Frequency |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

## To-be

{Only where requested. Shares step IDs with the as-is so the model can be diffed — a to-be
that cannot be diffed against an as-is cannot be risk-assessed.}

| # | Step | Change | Type | Lane | System | What it assumes | What it costs |
|---|---|---|---|---|---|---|---|
| {…} | {…} | {unchanged \| modified \| added \| removed \| merged \| automated} | {…} | {…} | {…} | {…} | {…} |

### Eliminated by constraint

| Change considered | Blocked by | Effect |
|---|---|---|
| {…} | {segregation_of_duties \| records_retention} | {removed from the design, not scored down} |

## Where the procedure and the practice differ

| # | The procedure says | What people actually do | Why | What this suggests |
|---|---|---|---|---|
| {…} | {…} | {…} | {usually rational} | {the reason is usually the actual defect} |

*Recorded as findings. **Never corrected in the model** — that erases the finding and
produces a model of a process nobody runs.*

## Assumptions

| # | Assumption | Source | Affects | Penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {steps affected} | {low \| medium \| high} |
