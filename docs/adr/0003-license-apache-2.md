# ADR-0003 — Apache-2.0, decided

- **Status:** Accepted
- **Date:** 2026-08-13
- **Deciders:** @vishaljavalkar-ai, @rajesh-malviya
- **Supersedes:** ADR-0000 §16.4 (open question), ADR-0000 §12 (licence bullet, which recommended but did not decide)
- **Superseded by:** none

> Decision record. Do not edit — supersede with a new ADR if this changes.

---

## Context

ADR-0000 §12 recommended Apache-2.0. ADR-0000 §16.4 then recorded that the repository had nonetheless shipped MIT, left the question open, and attached a deadline of a particular shape:

> *"Relicensing requires agreement from every contributor, so the cost of this decision rises with every merged PR. **Decide it while the contributor count is small.**"*

That is the whole reason this is being decided now rather than later. At the time of this record the repository has **20 commits and two human copyright holders**, no external pull requests, and no merge commits. The consent conversation is two people. After the first outside contribution it is two people plus everyone who has arrived since, indefinitely — and the project has just started actively inviting that traffic.

Nothing about the arguments changed. Only the cost of acting on them did, and it is about to go up.

## Decision

**The repository is licensed under the Apache License, Version 2.0.**

`LICENSE` carries the verbatim Apache-2.0 text. `NOTICE` carries the copyright line, the relicensing record, and the standing statement that all data in the repository is synthetic.

Copyright is attributed to **The Yuman EA Authors** rather than to an enumerated list. The list would need editing on every contribution, which is friction landing on exactly the people the project cannot afford to add friction to. Authorship of record is the git history.

### Why Apache-2.0 for this project specifically

**The patent grant is the reason, and it is not abstract here.** Apache-2.0 §3 grants patent rights explicitly; MIT is silent. The users this project targets are enterprise architects whose organizations run legal review before adopting anything, and that review is where a silent patent position becomes a blocking question. Many corporate open-source policies list Apache-2.0 as pre-approved and treat anything else as an exception request. For a project whose distribution model has no procurement step at all, being a licence that clears review unassisted is worth more than it would be to most projects.

**§5 removes the need for a CLA.** Contributions are automatically under the licence unless the contributor states otherwise. ADR-0000 §12 already rejected a CLA on contributor-cost grounds — *"a CLA will lose you contributors who'd need legal review"* — and Apache-2.0 gives the clarity a CLA was wanted for without the paperwork. DCO sign-off remains the recommendation for provenance; it is a per-commit line, not a legal process.

**The explicit terms suit a framework meant to be extended.** Overlays, private `x.<org>.*` skills, and third-party redistribution are all first-class in this design. Apache-2.0's attribution and modification-notice requirements state what an organization must do when it takes this in-house, rather than leaving them to infer it.

The cost is real but small: `NOTICE` conventions, §4 attribution obligations on redistribution, and a longer file than MIT's eleven lines.

### Consent

Consent from every copyright holder of record is tracked in issue **#TBD — replace before merging.** Both holders are maintainers; the git history at the time of this record shows 20 commits, two human authors, and no external pull requests.

The relicensing is **not retroactive**: releases already published under MIT remain available under MIT, and nothing here withdraws a grant already made.

Strictly, unanimous consent was not legally required — MIT permits sublicensing, so MIT-licensed contributions may be redistributed under Apache-2.0 with the original notice retained. It was obtained anyway, deliberately. **The audience for this repository is enterprise legal review**, and a reviewer who finds an ambiguous relicensing history rejects the project rather than investigating it. A clean consent record is worth considerably more here than the legal minimum.

### Scope

Applies to everything in `yuman-ea-core`: skills, agents, spec, schemas, docs, and synthetic fixtures.

It does **not** apply to third-party or organization skills in the `x.<org>.*` namespace. Those carry their own `license` field in `skill.yaml` and always did — the per-skill licence field, added for unrelated reasons, turns out to have been the right call.

## Consequences

**Enabling:**

- The single most common blocking question in an enterprise legal review is answered before it is asked.
- No CLA is needed, and none will be introduced.
- Organizations taking this in-house have written terms for doing so.

**Constraining:**

- `NOTICE` must be maintained and shipped with redistributions.
- Contributors adding third-party material must check licence compatibility. Apache-2.0 is one-way compatible with GPL-3.0 and not with GPL-2.0; this matters if a skill ever references bundled material rather than citing it. ADR-0000 §12's rule already covers the common case: **cite frameworks, never reproduce proprietary content.**
- The licence file is 11KB rather than 1KB. Cosmetic.

## Rejected alternatives

**Stay on MIT.** Rejected. Familiar and short, but silent on patents in front of the precise audience that asks about patents. Deferring again would only raise the price of the same decision.

**Dual-license: Apache-2.0 for code, CC-BY-4.0 for documentation.** Rejected. Defensible in principle — this repository is mostly prose — but the boundary is genuinely unclear here. A skill is markdown and YAML that behaves like code, and asking a contributor which licence their `SKILL.md` falls under is a question with no good answer. One licence for everything.

**Wait for an adopter to ask.** Rejected. It inverts the causation: the adopter who would have asked is the one who quietly does not adopt, and never files the issue that would have told us.

## How this is measured

By its absence. If licensing never comes up again in an adoption conversation, this worked.
