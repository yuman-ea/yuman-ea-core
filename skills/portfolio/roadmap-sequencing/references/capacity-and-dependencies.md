# Capacity, and the dependencies nobody stated

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when a capacity figure is contested, or when a plan looks achievable and everyone in the room is quiet.

## Capacity is a throughput number, not a headcount

The most common capacity figure in a roadmap is people multiplied by time, and it is wrong in the same direction every time.

Headcount counts availability. Throughput counts what actually got delivered — after the support rota, the incidents, the leavers, the onboarding, the meetings, and the thirty per cent of a delivery team's year that goes to work nobody put on a roadmap. **An organization that delivered four initiatives last year will deliver about four this year**, regardless of how the headcount arithmetic comes out.

That is why `capacity_basis` caps confidence. `measured_from_history` is worth more than a precise-looking calculation, because it has already absorbed everything the calculation forgets.

Where only headcount is available, the sensitivity analysis runs the plan at 20% lower capacity — and that version is usually closer to what happens.

## Capacity has a shape

**Three teams is not capacity for work needing a data engineer if all three are front-end teams.**

Total capacity is the number people plan with because it is the number that exists. But work needs particular skills, and a wave can sit comfortably within total capacity while being impossible on the one skill everything needs. Integration capability is the usual culprit — it is scarce, it is needed by almost everything, and it is invisible in a total.

When `skills_profile` is absent the method says plainly that capacity has been treated as fungible. That statement is doing real work: it converts a silent scheduling failure into a stated assumption someone can challenge.

## Subtract what is already running

Organizations are never starting from zero, and roadmaps are routinely drawn as though they are — because in-flight work belongs to a different governance forum, a different spreadsheet, and frequently a different director.

A wave-one plan that assumes full capacity, in an organization with three programmes already running, is over-committed on the day it is published. `in_flight_commitments` carries a high confidence penalty for that reason.

## Slack is a decision, not a leftover

A plan allocated to 100% of capacity fails on the first slip, and every plan slips.

Making slack an explicit percentage does two things: it survives the meeting where someone asks why the plan is not full, and it stops the reserve being consumed silently by the first initiative that runs over. **Ten per cent is a common floor; twenty is more honest in an organization that has not measured its throughput.**

## Hard and soft dependencies

Teams state every dependency as hard, for a reasonable reason: "we need X" is true, and adding "but we could start once X reaches its second milestone" invites being scheduled against it.

The difference between the two readings is routinely a whole wave. So the method asks for the classification explicitly and records every reclassification with the name of whoever confirmed it — because the plan's schedule was bought with those reclassifications, and if one is wrong, that is where the plan breaks.

**The question that separates them:** *what specifically do you need from X, and when does it exist?* "The customer data model" exists at design sign-off, not at go-live. "The migrated data" exists at go-live. Same dependency, two different waves.

## The dependencies nobody stated

The ones that stop a wave are rarely in anyone's plan.

Two initiatives both need the same system available. Each is correct that it needs it. Neither knows the other is coming, because they are sponsored by different directors and tracked in different forums. Nobody has stated a dependency between them because, from inside either one, there is not one.

This is the architecture contribution to sequencing, and it is why `estate_dependencies` is inferred from initiatives sharing a system rather than waiting to be declared. An inferred dependency is a **prompt to check**, not a finding — but the check is cheap and the collision is expensive.

The usual shape: a fragile shared system, several initiatives arriving at it within two quarters, and no single initiative's plan showing a problem. Look for the systems with the most initiatives pointing at them and the lowest technical fitness. That intersection is where roadmaps fail.

## Dependencies are discovered, not designed

However good the graph, more dependencies will surface during delivery than were known at planning.

That is not a failure of analysis; it is the nature of estates that grew rather than being designed. The planning response is not more analysis — it is the slack policy, and a sensitivity run that shows what one additional dependency per initiative does to the plan.

**A plan with no tolerance for discovery is a plan for the first wave only.**
