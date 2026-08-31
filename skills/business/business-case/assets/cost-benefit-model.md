# Cost and benefit model — {investment}

**Period:** {three | five | ten} years · **Discount rate:** {n% | **undiscounted**}
**Cost basis:** {supplier quote | delivery team estimate | analogous comparison | **unknown**}
**Confidence:** {low | medium | high} — {reason}

> **Every figure names its source.** A number with a blank source is the defect this method
> exists to prevent — in a board pack, figures acquire authority from the pack rather than
> from their derivation.

## Costs

| # | Type | Description | Y0 | Y1 | Y2 | Y3 | Y4 | Source | Basis |
|---|---|---|---|---|---|---|---|---|---|
| {…} | {build_cost \| purchase_cost \| transition_cost \| **run_cost**} | {…} | {…} | {…} | {…} | {…} | {…} | {…} | {…} |

*Run cost appears in every year of the appraisal, not only in the first. Over five years it
is routinely larger than the build cost, and a model that stops at go-live has omitted its
largest number.*

## Doing nothing

| # | Description | Y0 | Y1 | Y2 | Y3 | Y4 | Source | Rises over time? |
|---|---|---|---|---|---|---|---|---|
| {…} | {…} | {…} | {…} | {…} | {…} | {…} | {…} | {yes / no} |

*Never zero. For a renewal, doing nothing may mean something stops working — say what, and
when.*

## Benefits — cashable

| # | Description | Y0 | Y1 | Y2 | Y3 | Y4 | **Which budget falls** | Source |
|---|---|---|---|---|---|---|---|---|
| {…} | {…} | {…} | {…} | {…} | {…} | {…} | {named} | {…} |

## Benefits — released effort

| # | Description | Y0 | Y1 | Y2 | Y3 | Y4 | Budget falls? | Source |
|---|---|---|---|---|---|---|---|---|
| {…} | {…} | {…} | {…} | {…} | {…} | {…} | {**no**} | {…} |

*Reported separately and **never totalled with the cashable line**. Half a person released
across eight teams is eight fractions of a person and no reduction in spend unless somebody's
headcount changes.*

## Benefits — revenue and risk avoided

| # | Type | Description | Y1 | Y2 | Y3 | Y4 | Source | Basis |
|---|---|---|---|---|---|---|---|---|
| {…} | {revenue \| risk_avoidance} | {…} | {…} | {…} | {…} | {…} | {…} | {…} |

*Risk avoidance is a probability multiplied by an impact, and both halves belong in the
source column. A risk-avoidance benefit stated as a single figure has concealed a judgement.*

## The result

| | Value |
|---|---|
| Net present value | {…} |
| Payback period | {…} |
| Internal rate of return | {… \| **not meaningful — cash flow pattern does not support one**} |
| Net present value, **cashable benefits only** | {…} |
| Discount rate applied | {n% \| none} |

*The cashable-only line is the number the finance function will construct independently.
Constructing it first is how a case survives the meeting rather than being rebuilt in it.*

## Assumptions

| # | Assumption | Source | Lines affected | Penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {…} | {low \| medium \| high} |

## Against the constraint

| Constraint | Position |
|---|---|
| {budget_ceiling} | {within \| **exceeds — reported, not adjusted to fit**} |
