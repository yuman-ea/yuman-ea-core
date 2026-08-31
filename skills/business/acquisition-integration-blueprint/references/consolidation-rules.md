# Consolidation rules

This reference constrains **how capability scores become a disposition, and where this method stops**. Background, loaded on demand.

## Same vocabulary before any comparison

Both organizations' capabilities are described in the same terms before anything is compared, and the acquired business's own term is recorded alongside.

Skipping this produces two errors at once. **False overlaps**: two capabilities with similar names that do different things, merged on the strength of the label. **Missed overlaps**: the same capability under two names, run twice indefinitely because nobody noticed.

The translation table is also the most useful artifact for the acquired business's own people, who will otherwise spend six months not recognising themselves in the acquirer's model.

## Disposition rules

Applied in this order. The first that matches wins.

| # | Disposition | Condition |
|---|---|---|
| 1 | `insufficient_evidence` | The capability could not be assessed on either side |
| 2 | `day_one_critical` | It breaks at close — see [`day-one-rules.md`](./day-one-rules.md) |
| 3 | `blocked_by_separation` | It cannot be consolidated until a seller service ends or a constraint clears |
| 4 | `protect_do_not_touch` | It is the capability the deal was for, and standardising it would remove what was bought |
| 5 | `adopt_target` | Both do it, and the acquired business's way is better on the evidence |
| 6 | `adopt_acquirer` | Both do it, and the acquirer's way is better on the evidence |
| 7 | `run_both_for_now` | Both do it and consolidation returns little relative to what it costs |
| 8 | `consolidate_later` | Consolidation is worth doing and not in the first hundred days |

`protect_do_not_touch` outranks both adopt rules deliberately. Once a capability is in the consolidation conversation at all, the gravity of an integration programme pulls toward standardising it, and the protection has to be applied before that conversation starts.

## "Adopt ours" is a decision

Where both organizations do the same thing, the question is *which way is better*, not *which organization owns it*.

`adopt_target` is chosen more often than acquirers expect. The acquired business is frequently smaller, more recent, less encumbered by history, and has often rebuilt something the acquirer has been extending for fifteen years. Assuming the acquirer's way wins by default is expensive in two ways: it discards a better arrangement, and it tells the acquired staff — accurately — that nothing they built is valued.

The honest formulation for each overlap is a comparison on evidence, with the acquirer's incumbency noted as what it is: an advantage in migration cost, not in quality.

## Duplication is not automatically waste

`run_both_for_now` is a legitimate disposition and it is under-used.

Consolidation costs real money and real attention, both of which are scarce in the year after an acquisition. Where two capabilities overlap and consolidation returns little — no meaningful cost saving, no consistency that anyone needs, no single view that matters — running both is cheaper than a migration nobody needed.

The test is what merging actually returns, evidenced. "We should not have two of these" is an aesthetic preference, and it has funded a great many migrations that returned nothing.

## The capability that was bought

Where `deal_rationale` is `capability_acquisition`, the protection is the method's most important output.

The mechanism of loss is not malice or carelessness. It is that an integration programme is *set up* to standardise — that is its remit, its measures, and its definition of progress — and the acquired capability is an exception to a rule the programme is being judged on applying. It gets standardised by people doing their jobs correctly.

Two consequences follow:

- **The protection must be explicit and written down.** An intention to protect it does not survive contact with a programme whose scorecard counts standardised processes.
- **Asymmetry of reversibility.** Consolidation deferred can be revisited next year. A capability standardised away does not come back — and by the time anyone notices it is gone, the people who carried it have left, which is why the tie-breaker prefers protection over consolidation.

## Knowledge concentration

Undocumented knowledge leaves faster after an acquisition than at any other time, for reasons nobody controls.

The window to capture it is measured in weeks. It closes on its own, without anyone deciding, and anything not identified during it is lost rather than found later.

Record it as a **risk to capture**: which capability, what is undocumented, how few people hold it, and by when. Never as a judgement about individuals, and never as an input to a retention decision — those belong to people accountable for them, under obligations this method does not model.

## Where this method stops

**Application disposition.** This method decides that a capability consolidates. Which named system survives rests on run cost, contract position, dependency load, technical fitness, and what else in the estate depends on it — evidence held by `application-rationalization` and not here.

This is the seam most likely to be crossed in an acquisition, because the two questions arrive together and the second sounds like a detail of the first. It is not. An acquisition is a bad reason to make an application disposition on capability evidence alone, and "we are integrating anyway" has retired a great many systems that should have survived the comparison.

**Sequence.** A priority order is not a schedule. Sequencing against capacity, dependencies, and fixed dates is `roadmap-sequencing`.

**Operating model.** Where capabilities live is in scope. How the combined organization is arranged to run them — decision rights, locations, the management system — is `operating-model-design`.

**Contracts.** That a change-of-control term exists is in scope. What the merged or exited contract position should be is `license-and-contract-review`.
