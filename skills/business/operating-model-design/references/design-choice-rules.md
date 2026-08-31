# Design choice rules

This reference constrains **how options are compared, what a choice must declare, and how the transition is treated**. Background, loaded on demand.

## Every choice names what it makes harder

Mandatory, and the single most useful discipline in this method.

An operating model optimises for something. Centralising a capability gains consistency, scale, and a clear owner, and loses local responsiveness and context. Federating gains the reverse. Neither is right; each is a purchase, and the trade-off column is the receipt.

Two things follow from writing it down:

- **A choice with no stated cost has not been made.** It has been asserted, usually because it matched a preference nobody examined.
- **When the de-optimised thing goes wrong**, and it will, the register shows it was a known cost rather than an oversight. That distinction determines whether the model gets adjusted or abandoned.

## The centralisation axis

Nearly every operating model argument runs on this axis, and it is usually settled before the design starts.

That is not illegitimate. Executives have views, and a design that ignores a firm preference is a document nothing happens to. What is illegitimate is presenting an accommodated preference as a derived conclusion — because the design will be challenged on exactly this point, and an honest answer survives the challenge while a dressed-up one does not.

Hence two mechanisms: `centralisation_preference` is asked directly, and the sensitivity analysis designs the opposite and scores it. Where the preference and the winning option coincide and the opposite scores nearly as well, say so.

The useful reframing when the argument is genuinely open: **centralise the decisions whose information is naturally central, devolve the ones whose information is only available locally.** That converts a philosophical dispute into an evidence question.

## Roles, never individuals

Design names roles. It does not name people, and it does not shape itself around who is currently available.

The reasoning is practical. A model designed around a specific individual's unusual combination of skills works precisely as long as that individual stays, and it cannot be explained to anyone afterwards. It also makes the design impossible to discuss honestly, because every structural question becomes a question about a person.

Where an individual genuinely is a constraint — a sole licence holder, a single named signatory, the only person who can operate something — that belongs in the transition view as a dependency, not in the model as a role.

## Split capabilities need an outcome owner

A capability delivered across several units is common and often correct. What is not optional is naming who owns the **outcome**.

Without that, each unit optimises its own portion, all of them succeed against their local measures, and the capability as a whole degrades with nobody accountable. It is the same failure as friction at a process handoff, one level up, and it is harder to see because every part of it is performing well.

## Comparing options

Score candidate models against each other, and respect the indifference band. Two operating models separated by 0.1 are not distinguishable by this evidence, and announcing a winner is worse than reporting the tie — because the announcement ends the conversation that should have happened.

Where options tie, the tie-breakers are ordered deliberately:

1. **Simpler management system.** Coordination overhead never appears in the business case and never goes away.
2. **Fails more gracefully halfway.** Because transitions stall.
3. **Fewer new capabilities.** A model resting on capabilities the organization lacks is a capability programme with a chart attached.
4. **Easier to reverse.** Operating models are wrong more often than they are catastrophic.

## Transition: the two columns that matter

**`must_keep_running`** — what cannot stop while a change happens. This is what separates a plausible transition from an implausible one, and it is routinely discovered after the design is signed off. In an operating business the answer is usually "everything the customer sees", which constrains the sequence far more than dependencies do.

**`if_it_stalls_here`** — the state the organization is left in. Transitions stall for reasons that have nothing to do with the design: a change of sponsor, a bad quarter, an acquisition. An end state that is better but whose halfway point is unworkable is a worse choice than a weaker end state that can be paused, and that comparison is invisible in an end-state-only evaluation.

Stages that cannot be resting points should be short and should be labelled, so nobody plans a pause inside one.

## Parallel running

The cost most consistently omitted from transition estimates, and the one that most reliably extends beyond its plan.

Running the old arrangement and the new one together means two sets of people, two sets of measures, and someone coordinating between them. It is rarely optional and almost never as short as estimated. Put it in the transition view with a cost and a named coordinator.

## What the design may not conclude

**The schedule.** A stage order is not a plan. Sequencing against capacity, dependencies, and fixed dates is `roadmap-sequencing`, and a stage list presented as a schedule will be committed to as one.

**The sourcing.** That a capability is needed says nothing about whether to build, buy, or partner for it.

**The business case.** That a model is better says nothing about whether the change pays for itself.

**Anything about specific people.** Including, and especially, where the people constraint is a headcount reduction. The design says what roles are needed; who fills them and who does not is a decision made elsewhere, by people accountable for it, under obligations this method does not model.
