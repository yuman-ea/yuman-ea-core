# Status, numbering, and superseding

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when a decision changes one already recorded, or when setting up a decision log for the first time.

## The one rule

**Never edit an accepted decision record.** Mark it superseded, write a new one, and link them both ways.

This is not tidiness. A decision log's entire value is that it preserves *why* — including reasoning that later turned out to be wrong. Editing a record to match what you now believe destroys the only evidence of how the organization got here, and the reliable consequence is that somebody reopens the settled argument from scratch, makes the original mistake again, and has no way of knowing they are repeating it.

The same rule governs this repository's own ADRs, for the same reason.

**Fixing a typo is fine. Changing the reasoning is not.** If you find yourself explaining why an edit is really a clarification, it is not.

## Status values

| Status | Means |
|---|---|
| **Proposed** | Written, not yet agreed. Cite it as a proposal, never as settled |
| **Accepted** | Agreed and in force |
| **Superseded by {NNNN}** | No longer in force. Left otherwise untouched |

Three is enough. Projects that add `deprecated`, `on hold`, `partially accepted`, and `under review` end up with a log nobody can read, and the ambiguity always lands on the reader least equipped to resolve it.

**A record with no status is unusable** — a reader cannot tell whether it describes a decision or a discussion.

## Numbering

Sequential, zero-padded, never reused: `0001`, `0002`, `0003`. Assign at merge, not at drafting, so two people writing on the same day do not collide.

**Do not number by topic or date.** Topic prefixes go stale the moment the taxonomy changes, and dates make the number carry information that the date field already carries. A plain sequence is the only scheme that never needs rethinking.

**A superseded record keeps its number forever.** The gap in the sequence is the point.

## Superseding well

When a new decision replaces an old one:

1. **The new record links back:** `Supersedes: 0007 — Order state held in the capture system.`
2. **The old record gets one line changed** — its status — and nothing else.
3. **The new record says what changed and why now.** Not just the new decision, but what made the old reasoning stop holding. That sentence is the most valuable thing in the record, because the same change may invalidate other decisions nobody has revisited.

The third step is the one that gets skipped. "We now do X" tells a reader what; "the volume assumption behind 0007 was wrong by an order of magnitude" tells them where else to look.

## Partial supersession

Sometimes a new decision changes half of an old one. Two honest options, and the choice matters less than making it explicitly:

- **Supersede fully and restate the surviving half** in the new record. Cleaner to read, and the surviving reasoning is repeated rather than pointed at.
- **Record it as a narrower new decision** and leave the old one accepted, with a `Conflicts with` link on both. Truthful, but a reader now has to reconcile two live records.

Prefer the first where the surviving half is short. Never leave a partial supersession undeclared — an accepted record that is half-wrong is more dangerous than one that is entirely wrong, because the wrong half still reads as authoritative.

## Where the records live

In the organization's own repository, next to what they govern — not in `yuman-ea-core`, and not in a wiki that drifts.

Markdown, one file per decision, in a directory of their own. That is why `decision_record` prefers markdown output while every other artifact in this framework prefers a richer format: a decision record's natural home is version control, where it is diffable, reviewable, and dated by the history rather than by a field somebody forgot to update.

## Revisit triggers, and actually revisiting

Every record names an observable event that should reopen it: a volume threshold, a support date, a contract expiry, a review cycle. **A trigger phrased as "if circumstances change" is not a trigger** — nobody will ever notice it firing.

The triggers only work if someone reads them. A standing review — quarterly is common — that does nothing but scan open triggers costs half an hour and is the difference between a decision log and an archive.
