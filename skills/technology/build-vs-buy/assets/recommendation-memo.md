# {Capability} — build, buy, or partner

**To:** {audience}
**From:** {author}
**Date:** {date}
**Confidence:** {low | medium | high}

> **Writing rule for this document.** The reader is a CFO or a steering committee
> member who was not part of the analysis and has not read an architecture framework.
> No criterion IDs, no method vocabulary, no acronyms beyond the ones the business
> already uses. If a sentence needs a glossary, rewrite the sentence.

## The decision

{One paragraph. What is being decided, for which capability, over what horizon, and what
it is being optimized for. This is the framed decision statement in plain prose.}

{What this decision does **not** cover — one line, so nobody leaves the room believing
more was settled than was.}

## Recommendation

{One option — or an explicit statement that two options are too close to separate on the
evidence available, and what would separate them.}

{If recommending, one sentence on what happens next and who owns it.}

## Why

{The two or three things that actually decided it. Not a tour of all seven criteria — a
reader who wants the full arithmetic has the scorecard.}

{Where a criterion was decisive, say what the evidence was, not just the score:
"Buying wins on time to value because the team that would build it is committed to the
warehouse programme until Q3" — not "buy scored 4 on time to value".}

## What it costs

| Option | Year 1 | Five-year total | Basis |
|---|---|---|---|
| {option} | {figure or range} | {figure or range} | {supplied by finance \| estimated — see assumption A#} |

{Estimated figures are shown as ranges. A single number implies a precision the evidence
does not support, and it is the number that gets quoted back in six months.}

{State the currency. State whether internal effort is included — it usually is not, and
that is the most common reason a build looks cheaper than it is.}

## Options considered

| Option | What it means in practice |
|---|---|
| {option} | {one line a non-specialist can picture} |

{Where a split option was considered — build the part that differentiates, buy the rest —
say so here even if it was not recommended. Its absence is the most common gap in a
build-versus-buy paper.}

## Options eliminated, and by what

{Every option removed by a constraint before scoring, with the constraint that removed it,
stated as the organization states it.}

{If nothing was eliminated, say "No option was eliminated by policy." Do not omit the
section — a missing section reads as an omitted option.}

## What we assumed

| # | Assumption | Why we had to assume it | What it affects |
|---|---|---|---|
| A1 | {sentence} | {the data that was not available} | {which part of the recommendation moves if this is wrong} |

{This section is not an apology. It is the part that makes the recommendation checkable,
and the reason a reader can trust the parts that are not assumed.}

## How confident this is

**{low | medium | high}** — {the rule that produced this rating, in plain words}.

{What would raise it. Be specific: "Supplier pricing from two suppliers would move this
to medium" is useful; "more data would improve confidence" is not.}

## What would change this answer

{Plain sentences with thresholds, one per sensitivity target:}

- "The recommendation holds unless the internal build estimate is more than {N}% low. Past that, {option A} and {option B} are indistinguishable."
- "An organization that weights differentiation more heavily than we have would reach {the same | a different} conclusion."

## Next steps

1. {Action, owner, date.}

## The case against

{Include where a reasonable architect could have reached the other conclusion. Stating
the strongest version of the opposing argument is what makes the recommendation credible;
its absence is what makes a paper look like advocacy.}
