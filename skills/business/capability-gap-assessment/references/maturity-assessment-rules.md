# Maturity assessment rules

This reference constrains **how a level is assigned and what makes it defensible**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## The default scale

Where no organization-defined scale exists, this five-level behavioural scale is used and is printed with the assessment. The wording is deliberately plain: a scale that needs a framework glossary cannot be applied consistently by the people who know the capability best.

| Level | What a capability at this level looks like |
|---|---|
| 1 | It happens because particular people make it happen. No defined way of working, outcomes vary with who is available |
| 2 | A way of working exists and is mostly followed. It is not written down in a form anyone else could pick up |
| 3 | Defined, documented, and followed. Someone new could be trained into it. Outcomes are consistent |
| 4 | Measured. Performance is known, deviations are visible, and the capability is managed against evidence rather than impression |
| 5 | Improved deliberately and continuously, with the improvement itself governed. Changes are made on evidence and their effect is checked |

Three properties matter more than the exact wording:

- **The levels are cumulative.** A capability cannot be at 4 without satisfying 3. Where measurement exists on top of an undefined process, the rating is 2 with a note, not 4.
- **They describe behaviour, not intent.** "There is a policy" is not level 3; "the policy is followed and someone could be trained into it" is.
- **Level 5 is rarely the right target.** It costs real money to sustain and almost nothing competes on it.

## Every rating carries an assessor and evidence

Two columns, always. A level without them is a number with no standing, and it will be quoted for years by people with no way to check it.

Evidence does not have to be quantitative. "A documented procedure exists, three people have been trained into it, and the last two hires were productive within a fortnight" is stronger evidence for level 3 than a metric would be.

## Self-assessment bias has a direction

Capability owners rate their own capability in a predictable pattern:

| Dimension | Direction | Why |
|---|---|---|
| Process | Generous | They inhabit it and know the intent behind each step, so they rate the intent rather than the practice |
| Governance | Generous | They know decisions get made well, and cannot see that the mechanism is themselves |
| People | Roughly accurate | They know who they would struggle without |
| Technology | Harsh | They experience its failures daily and are not comparing it to anything |
| Information | Harsh | They know exactly which data they do not trust |

This is not dishonesty and it is not random, which is what makes it correctable. **State the bias rather than adjusting the numbers.** Silently applying a correction produces ratings nobody can reconcile with what they said, destroys the willingness to be assessed again, and is itself an unevidenced judgement.

The sensitivity analysis quantifies the exposure by lowering self-assessed process and governance ratings by one level and reporting which gaps grow.

## Independent assessment is not automatically better

It is better calibrated across capabilities and worse informed within them. An external assessor compares consistently and misses the informal mechanisms that make a capability work.

The strongest arrangement, where available, is a self-assessment challenged by someone outside the capability — which is what `independently_assessed` should mean in practice. Where only one is available, use it and say which.

## Comparison requires the same scale

A rating is meaningless without the scale it was made against, and the two most common failures are both quiet:

- **Comparing across capabilities rated on different scales.** Happens when parts of an assessment are inherited from earlier work.
- **Comparing against a prior assessment made on a different scale.** Produces apparent movement that is entirely an artifact of the scale change, and it is usually reported as progress.

Print the scale with the assessment. Where a prior assessment used a different one, say that the comparison is not available rather than converting between them.

## Point-in-time ratings have no direction

A capability at level 2 that has been there for three years, and one that has just dropped to it, need completely different responses. A single assessment cannot distinguish them.

Where no prior assessment exists, say so and treat the absence as a limitation rather than filling it with an impression of trend. Where one does exist, movement is often the more useful number than the level.

## On published maturity frameworks

Established maturity models are cited by name where drawn on and are not reproduced. Several carry licensing terms, and a permissive repository licence does not make incompatible material safe to embed.

Two cautions when an organization uses one:

- **They are calibrated for their own domain.** A model built for software process assessment applied to a commercial capability will produce ratings that look rigorous and mean something different from what the reader assumes.
- **They come with an implied target of the top level**, which is the assumption this method exists to challenge. Take the scale; do not take the ambition.
