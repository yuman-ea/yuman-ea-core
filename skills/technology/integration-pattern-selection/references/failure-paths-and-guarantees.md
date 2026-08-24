# Guarantees, ordering, and the failure path

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when writing the failure-path section, or when someone says the integration needs to be "reliable".

## Why this section is mandatory and still gets skipped

An integration design describes what happens when things work. Production is mostly the other case. The failure path is where the design either holds or turns into an incident, and it is skipped because at design time it feels like pessimism rather than engineering.

Four questions. If the design cannot answer all four, it is not finished:

1. **When the receiver is unavailable, what does the sender do?**
2. **Where does the data wait, and how long can it wait before something breaks?**
3. **When a message is rejected as invalid, what happens to it?**
4. **Who finds out, and how?**

The fourth is the one that decides whether a failure is a ten-minute fix or a customer complaint. "It goes to a dead letter queue" is only half an answer if nobody is watching the dead letter queue.

## "Reliable" is not a requirement

It has to become one of these, and they cost different amounts:

| What is actually meant | What it demands |
|---|---|
| We can afford to lose the occasional message | Best effort. Cheapest by a distance |
| Nothing may be lost | Durable storage before acknowledgement, and retry |
| Nothing lost, nothing processed twice | The above, plus idempotency in the receiver or deduplication in transit |
| Things must happen in the right order | Ordering guarantees, which constrain parallelism and therefore throughput |

**At-least-once is the normal default**, and it means duplicates will happen. Not might — will, on retry, on rebalance, on redelivery after a crash. The receiver must be idempotent, and that work belongs in the estimate.

**Exactly-once is usually a claim about a boundary, not about the world.** It typically holds within one system's transactional scope and stops at the edge. Where a use case truly needs it, the honest implementation is at-least-once plus deduplication on a business key, and the design should say so rather than asserting the stronger guarantee.

## Ordering

Ordering is expensive and is asked for more often than it is needed.

**Ask what breaks if two messages arrive out of order.** Frequently the answer is nothing, because the messages are independent — two different customers, two different products. Ordering usually only matters *within a grouping*: per account, per order, per item. A pattern that guarantees ordering within a partition and not globally is nearly always sufficient, and is far cheaper than global ordering.

**Global ordering means serial processing**, which caps throughput at one consumer. If the volume figures and the ordering requirement are both taken at face value, they will sometimes turn out to be mutually impossible — and finding that here beats finding it in performance testing.

## Backlogs

The failure nobody alerts on. Everything reports healthy, no errors are thrown, and the data is six hours stale.

**Alert on depth and on age, not on errors.** Age is the more useful of the two: a queue with a thousand messages is fine if it drains in a minute and an incident if the oldest is from yesterday.

State in the design **how long the data can be late before it matters**. That number is the alert threshold, and it usually differs sharply from the latency requirement — an integration that wants sub-second delivery may still be tolerable at five minutes late and business-critical at four hours.

## Poison messages

One message that cannot be processed, retried forever, blocking everything behind it.

Every asynchronous design needs a stated answer: how many retries, over what period, and then where does it go. A dead letter destination with nobody responsible for it is a queue where messages go to be forgotten, which is worse than dropping them, because the design claims they were kept.

## Replay

Two different needs, frequently conflated:

- **Recovery** — reprocess after a bug corrupted the target. Occasional, and a backup restore usually covers it.
- **Onboarding** — a new consumer needs history it was never sent. Routine in event-driven estates, and the thing only retained streams give you.

If the second is expected, that is a `data_streaming` signal and it should be established before the pattern is chosen rather than retrofitted, since bolting retention onto a queue-based design usually means rebuilding it.

## Testing the failure path

Where the organization has the discipline, the design should say how the failure path will be *tested*, not just what it is. An untested failure path is a paragraph, and the first real outage is when everyone discovers which parts of it were true.
