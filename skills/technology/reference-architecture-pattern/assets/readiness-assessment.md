# {Candidate pattern} — readiness assessment

**Date:** {YYYY-MM-DD} · **Origin:** {existing implementations \| external practice \| recurring problem}
**Intended authority:** {guidance \| default expectation \| mandated} · **Scope:** {…}
**Confidence:** {low | medium | high} — {the rule that produced it}

## Outcome

| | |
|---|---|
| **Status** | **{mandated \| recommended \| proposed \| not_yet_a_pattern}** |
| **Implementations counted** | {n} — {named} |
| **Weighted score** | {0.00} |
| **Blocked by constraint** | {policy_id, or "none"} |

{Where the status was capped by a hard constraint or by the confidence rule, say so here
in a sentence. A status that was blocked reads identically to one that was judged, unless
the document says otherwise.}

### If the status is `not_yet_a_pattern`

{Say what it actually is — a solution design, or a single decision — and name the skill
that owns it. Then say precisely what would make it a pattern: usually "a second
independent implementation, built by a different team against a different starting point."}

**No pattern definition is produced at this status.**

## Implementations counted

| System | Team | Built | What was genuinely different about it |
|---|---|---|---|
| {…} | {…} | {…} | {…} |

*Two systems that differ only in name are **one** implementation. So are two built by the
same team in the same quarter from the same starting point — they share the assumptions
that have not been tested yet. The last column is where that judgement is shown.*

## Scores

| Criterion | Score | Weight | Weighted | Evidence | Assumption | Score confidence |
|---|---|---|---|---|---|---|
| evidence_base | {1-5} | 0.25 | {0.00} | {evidence_id: the specific fact} | {A1, or blank} | {low \| medium \| high} |
| problem_recurrence | | 0.20 | | | | |
| constraint_clarity | | 0.15 | | | | |
| scope_boundedness | | 0.15 | | | | |
| adoption_cost | | 0.10 | | | | |
| estate_fit | | 0.10 | | | | |
| maintainability | | 0.05 | | | | |

**Evidence** names the input the score rests on and the fact taken from it — not a
restatement of the criterion.

## Weights used

| Criterion | Default | Used | Changed by |
|---|---|---|---|
| evidence_base | 0.25 | {0.00} | {overlay \| renormalization \| unchanged} |
| problem_recurrence | 0.20 | | |
| constraint_clarity | 0.15 | | |
| scope_boundedness | 0.15 | | |
| adoption_cost | 0.10 | | |
| estate_fit | 0.10 | | |
| maintainability | 0.05 | | |

*Must sum to 1.00.*

## Conformance criteria review

| # | Proposed criterion | Checkable? | If not, the rewrite |
|---|---|---|---|
| C1 | {…} | {yes \| no} | {the specific, observable version} |

*Any criterion marked not checkable blocks `mandated` and caps confidence at `low`. This
table is where "loosely coupled" gets turned into something a reviewer can actually
verify, or dropped.*

## Assumptions this assessment depends on

| # | Assumption | Source | Affects | Confidence penalty |
|---|---|---|---|---|
| A1 | {…} | {on_missing path taken} | {criteria affected} | {low \| medium \| high} |

## What would change the status

| Varied | How | Result |
|---|---|---|
| Implementations | Remove the most-cited one | {does it still generalize, or was it always one system's design} |
| Adoption effort | Double it | {does the pattern still earn its place} |
| Scope | Apply one scope wider | {where it breaks first, and whether the anti-scope already says so} |
| Evidence weight | ±0.10 | {would a more or less demanding organization reach the same status} |

*The first row is the most revealing test in the method. Run it even when the answer looks
obvious.*
