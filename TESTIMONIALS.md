# Testimonials

Architects who have run a skill on a real decision, and what happened.

**Not a praise wall.** A report of what broke is worth more here than a report of what worked, and it is what makes a stranger trust the rest of the file.

This file also decides something: a skill cannot reach `proven` maturity without a real decision reported by someone outside the maintainer group ([spec/lifecycle.md](spec/lifecycle.md)). **Entries here are that evidence.** Without them, everything stays at `draft` — correctly.

## Where each skill stands

| Skill | Maturity | Reports |
|---|---|---|
| [build-vs-buy](skills/technology/build-vs-buy/SKILL.md) | `draft` | 0 |
| [high-level-architecture](skills/technology/high-level-architecture/SKILL.md) | `draft` | 0 |

## Before you write one

Describe the decision's **shape**, never its content. "A build-versus-buy call on a customer-facing system" is useful. The system, the option chosen, the figures, and supplier names are not.

Post anonymously if that is easier — *"an architect at a mid-size logistics company"* is a complete attribution.

## Template

```markdown
### <skill> — <what kind of decision, in five words>

- **Who:** <name and organization, or "an architect at a <sector> company">
- **Skill and version:** <e.g. build-vs-buy 0.1.0>
- **Date:** <YYYY-MM>
- **Data I actually had:** <e.g. "no cost model, one quote, no NFRs written down">
- **A real decision?** <yes / no — a dry run still counts, just say so>
- **Gone back to it since, unprompted?** <yes / no>

**What it got right:** <two or three specific sentences>

**What it got wrong:** <the important half — a criterion weighted badly, a question
that missed, an assumption it should have flagged and didn't>

**Would you use it again?** <yes / no / with changes — and which changes>
```

## Entries

<!-- Newest first. We will not write our own entries here: one invented testimonial
     makes every genuine one worthless. -->

*None yet. If you have run one of these on a real decision, yours would be the first — including, and especially, if it did not go well.*

## How to add one

Open a pull request with your filled-in template, or [an issue](../../issues) titled `Testimonial: <skill>`.
