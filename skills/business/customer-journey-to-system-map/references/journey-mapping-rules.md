# Journey mapping rules

This reference constrains **whose journey it is, where its boundaries go, and what counts as a stage**. Background, loaded on demand — the method in [`SKILL.md`](../SKILL.md) is complete without it.

## Name stages for intent

Every stage answers: *what is the customer trying to do here?*

| The customer's stage | The organization's name | Why the difference matters |
|---|---|---|
| Finding out whether it will arrive in time | Order status enquiry handling | The organization's name assumes an enquiry. The customer's assumes anxiety, and the fix might be a notification rather than a better enquiry process |
| Working out who to ask | Contact routing | The customer's version has no system in it at all |
| Proving we already sent that | Documentation resubmission | The organization's name treats a failure as a normal step |

The pattern in the third row is worth watching for. When a stage's organizational name normalises a failure — resubmission, re-verification, chaser call — the customer's name for the same moment usually contains the word "again", and that word is the finding.

## Stages with no channel are stages

Waiting. Chasing. Asking a colleague. Working out what to do next. Deciding whether it is worth the effort.

These carry a large share of total journey effort, produce no system record, appear in no analytics, and are therefore absent from every journey map assembled from touchpoint data. They also tend to score worst, which means a map that omits them is not merely incomplete — it systematically excludes the worst part of the experience.

Find them by asking about the gaps: *between this step and the next, what is the customer doing?* The answer "nothing, they wait" is a stage, and the follow-up — *do they know how long for?* — is usually where the pain is.

## Boundaries: start before the organization does

The commonest failure is to start the map where the organization's process starts: at order receipt, at application submission, at the first support ticket.

Everything before that point belongs to the customer and is where they formed their impression — working out whether the organization offers what they need, finding the right form, deciding which channel to use, gathering what they were told to bring. That region routinely contains the highest-effort stages in the journey and never appears in a system.

End late, too. The organization considers the journey complete when its process closes; the customer's journey ends when they have what they needed and know they have it.

## One segment at a time

A large account with a named representative and a small account using self-service are having two different experiences of the same organization. Averaged, both disappear.

Where several segments are mapped, map them separately and compare. Where only one map is possible, name the segment it describes rather than presenting it as the customer journey — and say what the other segments are likely experiencing instead.

## Failure paths are part of the journey

Abandonment, complaint, escalation, and exit are journeys in their own right.

They are systematically absent from maps drawn by the people who designed the intended journey, for an understandable reason: those people know how it is supposed to work, and the failure paths are precisely the parts nobody designed. They are also the paths that decide revenue.

The most useful question here is rarely asked: *what does a customer do when they give up?* The answers — phones a representative directly, asks another supplier, does nothing and the order never arrives — are stages, and each has a system story behind it.

## Pain evidence and its direction of error

Internally inferred pain is not randomly wrong. It is wrong in one direction:

- The organization knows about the problems customers **complained about**.
- It is blind to the problems customers **worked around silently**, which are more numerous.
- It is completely blind to the problems customers **left over**, which are the expensive ones.

So a map built on internal opinion is a reasonable inventory of known issues and a poor guide to what is actually costing the relationship. That is why `pain_evidence` caps the confidence of the entire run rather than only the pain register, and why the sensitivity analysis explicitly asks what changes if the silent problems are the worst ones.

## On journey mapping practice

Published customer experience and service design practice is cited by name where drawn on. It is not reproduced.

Two conventions from that practice are deliberately not adopted here. **Emotion curves** are omitted because they require research this method's primary user usually does not have, and an invented emotion curve is confident fiction of exactly the kind this project exists to prevent. **Persona narratives** are omitted for the same reason — where segment definitions exist they are used, and where they do not, the map says it describes an average customer who may not exist.
