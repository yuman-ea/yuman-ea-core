# What each pattern actually costs

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when a score is contested, or when a pattern looks obviously right and you want to know what it will cost you later.

Each entry states what the pattern is good at, what it costs, and **the failure mode it is known for** — because the failure mode is usually what decides between two patterns that both look adequate on paper.

---

## api_synchronous

Caller asks, waits, gets an answer or an error.

**Good at:** immediate validation, anything where the caller must act on the result. Simple to reason about — one call, one outcome, no intermediate state to inspect.

**Costs:** the caller's availability is now bounded by the receiver's. Every synchronous hop multiplies downtime rather than adding it, and retries under load turn a slow receiver into a failing one.

**Known failure mode:** cascading timeouts. The receiver slows, callers hold connections waiting, the caller's own thread pool exhausts, and a component two hops away falls over for reasons nobody can see from its logs.

**Reach for it when** the caller genuinely cannot proceed — a credit check before accepting an order, a price before showing a total. **Not** because it is the easiest to build.

## api_asynchronous

Caller submits, receives an acknowledgement, and gets the result later by callback or polling.

**Good at:** long-running work where the caller needs a result but not immediately. Keeps the caller's availability independent while still giving it an answer.

**Costs:** two interfaces instead of one, correlation identifiers, and somewhere to hold the result until it is collected. The caller now needs state it did not need before.

**Known failure mode:** the result is produced and never collected, because the callback failed and nothing polls. Silent, and usually discovered by a customer.

## publish_subscribe

Producer broadcasts an event; any number of consumers subscribe.

**Good at:** unknown or growing consumers. New consumers attach without the producer changing or knowing.

**Costs:** the producer loses visibility of who depends on it, which makes payload changes hazardous. Requires a broker, and requires discipline about event schemas.

**Known failure mode:** a schema change breaks a consumer nobody remembered existed. The mitigation is versioning and a register of subscribers, and neither is free.

## queue_based

Point to point, guaranteed delivery, receiver works at its own pace.

**Good at:** load levelling and decoupling availability. The sender hands over and stops caring; the queue absorbs the difference between the two systems' rates.

**Costs:** a broker to run, and a backlog that needs monitoring. Delivery is normally at-least-once, so **the receiver must be idempotent** — that work is real and is routinely left out of estimates.

**Known failure mode:** silent backlog growth. Everything reports healthy, nothing errors, and the data is hours stale before anyone notices. Alert on queue depth and age, not just on errors.

## file_transfer

Batches of records exchanged on a schedule.

**Good at:** high volume, large payloads, and partners whose capability you cannot control. Cheap, universally supported, and easy to reprocess — the file is still there.

**Costs:** latency is the schedule. Partial failures are awkward: half a file processed is a state nobody designed for.

**Known failure mode:** the file that did not arrive. Nothing errors, because nothing ran. Absence detection has to be built deliberately, and usually is not.

**Underrated.** Where the timing requirement genuinely tolerates it, a scheduled file exchange is often the most operable choice in the set, and it is dismissed for looking old-fashioned rather than for failing a requirement.

## data_streaming

Continuous ordered event log, retained and replayable.

**Good at:** replay, multiple independent consumers reading at their own positions, and rebuilding state after a bug. Ordering within a partition is guaranteed.

**Costs:** the most operationally demanding pattern in the set by a wide margin. Retention, partitioning, consumer offsets, rebalancing — all of it needs people who have run it before.

**Known failure mode:** adopted for the replay story by a team who cannot operate it. It then becomes the least reliable component in the estate, and reverting is expensive because consumers have been built against it.

**Reach for it when** `replay_need` is `routinely` **and** the organization can genuinely run it. Both halves.

## partner_document_exchange

Industry-standard document formats across an organizational boundary.

**Good at:** many partners with heterogeneous capability. The standard is the point — partners already support it, and you are not asking each one to build something bespoke.

**Costs:** mapping to and from the standard, onboarding per partner, and a schedule set by convention rather than by your requirements.

**Known failure mode:** treating it as a technical integration. Most of the cost is partner onboarding, testing, and the long tail of partners who implement the standard slightly differently.

## direct_data_access

One system reads another's data store directly.

**Good at:** being quick to build. That is the entire list.

**Costs:** the two systems are now coupled at their most brittle layer. The owning system cannot change its schema, cannot be replaced, and often does not know it is being read.

**Known failure mode:** discovered during a migration, years later, when a change to a table breaks something nobody knew was connected.

**It is in the option set so it can be rejected explicitly.** Teams reach for it when integration is hard, and a comparison that never names it leaves that pressure unaddressed. Score it honestly; it usually loses on `change_tolerance` and `operability` without needing to be argued against.
