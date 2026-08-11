# Eval cases — build-vs-buy

Three golden cases, the minimum to merge at `draft` (lifecycle.md R12). Each declares an
expected outcome, an expected confidence rating, and the assumptions the run must surface.

| Case | What it tests |
|---|---|
| [`01-commodity-capability-no-cost-data`](./01-commodity-capability-no-cost-data.yaml) | Degrading honestly. No financial data at all — does it still produce artifacts, and is it honest about what they rest on? |
| [`02-differentiating-capability-full-data`](./02-differentiating-capability-full-data.yaml) | Following the declared weights when they disagree with the cheapest option, and earning a `high` rating |
| [`03-close-call-with-hard-constraint`](./03-close-call-with-hard-constraint.yaml) | Reporting a tie as a tie, and reporting an eliminated option rather than dropping it |

They are deliberately different in shape. A skill that scores well on all three is one
that behaves the same way whether the data is complete, absent, or ambiguous — which is
the property the seven-phase contract exists to produce.

## Case structure

`spec/` does not yet define an eval schema — one skill is not enough evidence to fix a
format. Until it does, follow this shape:

| Key | Purpose |
|---|---|
| `id` · `skill` · `fixture` | Identity, and the synthetic enterprise the case runs against |
| `description` | What failure this case exists to catch. Write this first; a case without a named failure tends not to catch one |
| `given.scenario` | The situation in the words a practitioner would use |
| `given.ask` | Answers to the five questions |
| `given.gather.provided` / `.withheld` | What the run has, and what it must degrade around. **`withheld` is the interesting half** |
| `given.policies_supplied` | Constraints, where the case tests `bound`. Omit to test the no-overlay path |
| `expect` | Outcome, confidence, what must be stated, what must be emitted |
| `must_not` | Specific wrong behaviours. Usually more diagnostic than `expect` |
| `fails_if` | The failure in one sentence, for the reviewer reading the diff |
| `tolerance` | What may legitimately vary between runs, and what may not |
| `notes` | Why this case is worth its place |

## Writing a new one

**Name the failure before the scenario.** "Checks that it works" produces a case that
passes whatever the skill does. "Checks that it does not declare a winner separated by
0.04" produces one that catches something.

**Withhold something.** A case where every input is supplied tests the arithmetic. The
`on_missing` paths are where this skill's real behaviour lives, and they are the paths a
real user takes.

**Assert on reasoning, not only on the answer.** A run that reaches the right
recommendation for the wrong reason will reach the wrong one next time the inputs shift.
`must_state` is where that is caught.

**Keep expected scores out of it.** Individual scores vary by a point between runs and
between hosts. Assert on rankings, confidence ratings, eliminations, and the sentences
that must appear. Use `tolerance` to say so explicitly.
