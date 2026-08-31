# Concern and viewpoint rules

This reference constrains **what qualifies as a concern, how it maps to a view, and how scores become a status**. Background, loaded on demand.

## A concern is a question

The test: **could a deliverable answer this, and would the stakeholder recognise the answer?**

| Concern | Topic |
|---|---|
| Will this pass the March inspection? | Compliance |
| Can my team still close the period in three days? | Finance operations |
| What happens to driver shift patterns? | People impact |
| Which of my systems stop working on day one? | Integration |

A topic tells you what someone cares about. A question tells you what to produce, what it must contain, and how you will know it worked. Everything downstream of this method depends on having the second.

**Do not convert a topic into a question on the stakeholder's behalf.** The conversion is a guess, and it will be wrong in a specific direction: toward whatever the architect already intended to produce. "Security" becomes "does the design meet the security baseline", when what they meant was "am I going to be personally accountable if this is breached". The first has a view; the second needs a conversation.

Record it as a topic, mark it, and go and ask.

## Stated, prior, or inferred

Three sources, and they are not interchangeable:

| Source | Weight |
|---|---|
| `stated_by_stakeholder` | Evidence |
| `from_prior_engagement` | Probably still true; check if the decision matters |
| `inferred_by_architect` | A prediction, not evidence |

An inferred concern is often a good prediction — experienced architects are usually right about what a Finance Director will want to know. It is still the architect's concern with someone else's name on it, and the deliverables built to answer inferred concerns are reliably the ones nobody reads.

The sensitivity analysis removes all of them and reports what is left. It is the cheapest way to find out which planned deliverables have no stakeholder behind them, and it costs nothing to run before they are produced.

## One view rarely answers three concerns

Views get claimed to answer several concerns. In practice a view answers one concern well, and the others get a paragraph nobody finds.

The sensitivity test — assume each deliverable answers only its primary concern — exists to make that visible. Where it turns four concerns into one addressed and three unaddressed, the coverage claim was optimistic and the gap will surface at sign-off.

The practical rule: a view should have one named primary concern and one named stakeholder who has to be satisfied by it. Additional coverage is a bonus, not a plan.

## A view in the wrong language has not answered anything

`view_must_contain` is stated **in the stakeholder's terms**, not the architect's.

A finance stakeholder's concern about period close is not answered by a component diagram, however completely the diagram contains the information. A regulator's concern is not answered by an architecture pattern, however conformant. The content may be right and the answer still unreceived.

This is also where the project's business-language rule gets its sharpest test: the map explicitly records who has to be able to read each view.

## Status rules

Applied in this order. The first that matches wins.

| # | Status | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | Neither the concern nor the stakeholder's position could be established |
| 2 | `blocker_unengaged` | The stakeholder has blocking power and no stated concern |
| 3 | `restricted_view` | The view answering it cannot lawfully be shown to the stakeholder who holds it |
| 4 | `vague_concern` | What was supplied is a topic, not a question |
| 5 | `conflicting` | Satisfying it makes another stakeholder's concern impossible |
| 6 | `inferred_only` | No stakeholder has stated it |
| 7 | `unaddressed` | A real, stated concern with no deliverable behind it |
| 8 | `addressed` | Everything else |

`blocker_unengaged` sits second deliberately. Everything below it presumes the concern is known; that status says the most consequential concern on the map may not be recorded at all.

`restricted_view` is third because it looks like coverage. A view exists, it answers the question, and the person who needs it cannot see it — which is functionally identical to no view at all and reads as complete on any coverage count.

## Conflicts are decisions

Two stakeholders wanting incompatible things is not an analysis problem. It is a decision, and it belongs to a named person.

Three things must never happen to a conflict:

- **Resolved quietly inside a deliverable.** The decision gets made by the architect, invisibly, and the losing stakeholder finds out at sign-off.
- **Averaged.** A design satisfying half of each concern usually satisfies neither, and nobody chose it.
- **Deferred without a name.** "To be resolved" with no owner means it will be resolved by whoever is most senior in the room on the day.

Record who decides. Where a conflict is likely to be settled by seniority rather than argument — which is common and not illegitimate — saying so in advance lets the likely loser be consulted rather than informed, which is frequently the difference between an accepted decision and a reopened one.

## Concerns determine deliverables

Where the deliverable set is open, the concerns decide it. That is the only order that produces views anyone reads.

Where the set is already committed — which is the more common case, since deliverable lists tend to be written into statements of work before anyone has asked a stakeholder anything — this method's job changes. It finds the concerns nothing will answer, and reports them as a declared gap.

**Do not stretch a committed view to cover an uncovered concern.** The view then answers neither question well, and the gap disappears from the record without being closed.
