# Design decision register — {scope}

**Confidence:** {low | medium | high}

> **`Makes harder` is mandatory on every row.** A design choice with no stated trade-off has
> not been made, only asserted.

## The register

| # | Dimension | Decision | Options considered | Chosen | Because | **Makes harder** | Reversibility | Decided by |
|---|---|---|---|---|---|---|---|---|
| D1 | {work \| organization \| locations \| information \| suppliers \| management_system} | {…} | {…} | {…} | {…} | {…} | {easily reversed \| costly to reverse \| **effectively permanent**} | {…} |

## Decisions that are effectively permanent

| # | Decision | Why it cannot readily be undone | What would have to be true for it to be right |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

*Worth separating out. Operating models are wrong more often than they are catastrophic, and
the cost of being wrong is dominated by how hard it is to change again.*

## Options eliminated by a hard constraint

| # | Option | Blocked by | What it would have achieved |
|---|---|---|---|
| {…} | {policy ID only} | {segregation_of_duties \| data_residency} | {stated, so the constraint's cost is visible} |

*Eliminated, not scored down. An option that vanished without explanation reads as a rigged
analysis, and in a steering committee it will be treated as one.*

## Decisions still open

| # | Dimension | The question | Who has to decide | By when | What is blocked until then |
|---|---|---|---|---|---|
| {…} | {…} | {…} | {…} | {…} | {…} |

## Where the design followed a stated preference

| # | Decision | Stated preference | Did the analysis independently support it? |
|---|---|---|---|
| {…} | {centralised \| federated \| devolved} | {…} | {yes / **no — accommodated rather than derived**} |

*This table exists because the centralisation question is usually settled before the design
starts and defended afterwards as a conclusion. Saying which it was here is more honest than
the alternative, and it is the question the design will be challenged on.*
