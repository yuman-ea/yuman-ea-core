# Renewal calendar — {organization}

**Reviewed:** {YYYY-MM-DD} · **Horizon:** {12 | 24 | 36} months · **Objective:** {…}
**Posture:** {…} · **Change capacity:** {…} · **Confidence:** {low | medium | high} — {reason}

> **Sorted by notice date, not expiry.** The notice date is expiry minus the notice period,
> and it is when the decision window closes. A contract expiring in nine months with a
> twelve-month notice period was decided three months ago, by nobody.

## Windows already closed

| Contract | Supplier | Expiry | Notice period | Notice date | What this means now |
|---|---|---|---|---|---|
| {…} | {…} | {…} | {…} | {passed} | {the term the organization is now committed to, and when the next window opens} |

*State "None — every window in scope is still open" explicitly if that is true. It is the
best sentence in this document when it is honest.*

## Calendar

| Notice date | Contract | Supplier | Covers | Annual value | Expiry | Window | Position | True-up exposure | Confidence |
|---|---|---|---|---|---|---|---|---|---|
| {YYYY-MM-DD} | {…} | {…} | {…} | {…} | {…} | {open \| closing \| closed \| unknown} | {renegotiate \| renew_as_is \| consolidate \| re_compete \| exit \| needs_evidence} | {range, metric named, or unknown} | {…} |

**Window** is `closing` when the notice date falls inside the time a supplier change would
realistically take — not when it is soon. A three-month notice on a system needing nine
months to replace is closing today.

**True-up exposure** is never a bare number. "Entitlement gap of roughly 300-350 named
users; priced at list this is {range}, at contract rate {range}" is usable. "£200k" is not.

## Positions eliminated by constraint

| Contract | Position removed | Policy | What it says |
|---|---|---|---|
| {…} | re_compete | approved_vendors | {…} |

*Removing `re_compete` removes leverage. Where a constraint has done that, the leverage
score reflects it and the brief says so.*

## Spend across the horizon

| Year | Committed | At assumed uplift | At uncapped uplift |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

*Where uplift terms were not confirmed, plan against the range. State the currency.*

## Assumptions this calendar depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {contracts affected} | {low \| medium \| high} |

## What would change it

| Varied | How | Result |
|---|---|---|
| Consumption | +20% on recorded | {which contracts cross into material exposure} |
| Notice period | Twice the assumed length | {which windows close, which positions become unavailable} |
| Uplift | Capped versus uncapped | {spread in committed spend across the horizon} |
| Leverage weight | ±0.10 | {whether positions hold for a more or less mobile organization} |
