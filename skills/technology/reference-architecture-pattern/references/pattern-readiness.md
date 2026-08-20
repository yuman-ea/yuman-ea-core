# Pattern readiness rules

This reference constrains **how the score pattern becomes a status**. The weighted score is not itself the answer.

Background, loaded on demand. The method in [`SKILL.md`](../SKILL.md) is complete without this file; reach for it when a status is contested.

## Counting implementations

Everything starts here, because `evidence_base` carries the heaviest weight and the count is what most people get wrong.

**An implementation counts when it was built by people who could have chosen otherwise, and did not.** That is the test. Two systems that share a team, a quarter, and a starting point are one implementation with two names — they share every assumption that has not yet been challenged.

| Count | Ceiling |
|---|---|
| Three or more, genuinely independent | `mandated` available |
| Two | `recommended` available |
| One | `proposed` at best, and usually `not_yet_a_pattern` |
| None | `proposed` if the shape is sound and external practice is credible; otherwise `not_yet_a_pattern` |

**External practice is evidence, not proof.** A practice established elsewhere may be entirely right for you and still fail here for reasons nobody outside your estate could know — an integration that does not exist in the reference case, a compliance obligation, a platform you cannot leave. It can carry a pattern to `proposed` on reputation. It reaches `recommended` when you have run it.

---

## The statuses

### Mandated

Use when **all** of the following hold:

1. three or more independent implementations;
2. `constraint_clarity` is favourable — the pattern forbids specific things and every conformance criterion is checkable;
3. `scope_boundedness` is favourable — the anti-scope is written and specific;
4. no hard constraint blocks it;
5. `intended_authority` is `mandated` — a pattern is never promoted past the authority its owner asked for;
6. confidence is not `low`.

If any conformance criterion cannot be checked by a reviewer who did not write the pattern, **the mandate is not available**. An unenforceable mandate is worse than a recommendation, because it invites teams to ignore governance generally.

### Recommended

Use when the pattern is genuinely generalized — two or more implementations — the anti-scope is stated, and adoption cost is understood well enough that a team can plan against it.

Say what "recommended" obliges: deviation is allowed and must be recorded with a reason. If nobody will ever read those records, this is `guidance` wearing a stronger word.

### Proposed

Use when the shape is sound but the evidence is thin — one implementation, or none plus credible external practice.

**A proposed pattern is published, not hidden.** It is how an organization says *we think this is the direction, come and try it.* It must name:

- what would promote it, concretely — usually "a second independent implementation, built by a different team";
- who is expected to try it next;
- the date by which it is promoted, revised, or withdrawn.

Without that third item, `proposed` becomes a permanent parking space and the catalogue fills with candidates nobody ever decided about.

### Not yet a pattern

Use when it generalizes from one implementation or none, and no credible external practice supports it.

**This is not a rejection**, and the distinction matters when delivering it. The design may be excellent. It is simply not yet the kind of thing that governs other people's work.

Always name:

- what it actually is — a solution design, or a single technology decision;
- the skill that owns it: `high-level-architecture` for a solution shape, `architecture-decision-record` for a single choice;
- the one thing that would change the answer;
- where the work is recorded meanwhile, so it is not lost — usually as a worked example attached to the system that implements it.

**Produce no pattern definition at this status.** A polished pattern document for one system's design is worse than no document, because it will be cited by someone who assumes it was earned.

---

## When a constraint blocks a status

A hard constraint caps the status; it does not change the scores.

Record it as **blocked**, with the policy ID, in the assessment and the decision record. A capped status and a judged status look identical from outside, and the difference matters to anyone deciding whether to argue with it. *"Scored for `mandated`, capped at `recommended` because the pattern cannot produce an exportable audit log"* is a sentence that tells a reader exactly what to fix.

## Close calls

**Prefer the lower status.** Publishing as `recommended` something that should have been `proposed` costs more than the reverse, because teams build on it before it has earned that, and unwinding a pattern people have adopted is expensive in credibility as well as effort.

Where two statuses are genuinely plausible, publish at the lower one and name the single implementation or piece of evidence that would raise it. That sentence is more useful to the organization than the higher status would have been.

## A note on the shape of a catalogue

Ring counts are a signal. A catalogue where everything is `mandated` is not governing, it is dictating, and teams will route around it. One where everything is `proposed` has never decided anything.

If the same organization keeps producing `not_yet_a_pattern`, that is not a failure of the method — it usually means patterns are being written at the moment of first invention rather than after the second or third time the problem was solved. The fix is timing, not standards.
