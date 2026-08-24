# Evidence, references, and what a score actually rests on

Background, loaded on demand. **The method in [`SKILL.md`](../SKILL.md) is complete without this file.** Reach for it when running reference calls, or when a scorecard looks more confident than the evidence behind it.

## The evidence ladder

Five types, and the gap between the top and the bottom is enormous:

| Type | What it means | What it is worth |
|---|---|---|
| `demonstrated` | We ran it ourselves, on our data, or watched it run | The most reliable thing available |
| `reference_checked` | A customer told us, unprompted by the supplier | Strong, especially on the supplier criteria |
| `documented` | Written in a formal response or specification | Real — it can be held to contractually |
| `vendor_claimed` | The supplier said so | Not evidence. It is a position |
| `impression` | Someone's read of the room | Occasionally the most accurate thing in the room, and never defensible |

**A 4 that was demonstrated beats a 5 that was claimed**, which is why it is the first tie-breaker. And why the run reports the counts per candidate rather than burying them: a scorecard whose heavily weighted criteria sit in the bottom two rows is a record of a sales process.

`impression` is included deliberately rather than being disallowed. Experienced evaluators pick up real signal from how a supplier behaves under pressure, and pretending otherwise just gets that signal recorded as `documented`. Record it honestly, weight it accordingly, and never let it carry a heavily weighted criterion on its own.

## Reference calls

The single highest-value evidence available, and the most commonly skipped because it takes time and feels awkward.

**A reference the supplier nominated is marketing.** Not worthless — a nominated reference will still tell you useful things if you ask well — but it is a customer selected because they will say good things. Treat it as such and record it as such.

**Find one yourself.** A user group, a conference contact, a peer at a comparable organization, someone on a professional network who lists the product. One independently found reference is worth several nominated ones, and its absence caps the confidence of the whole run.

**Ask about the bad day, not the product.** Nominated or not, references answer feature questions the same way the supplier would. The questions that produce signal are about what happened when things went wrong:

- What broke, and how long did it take to get someone competent on it?
- What did the implementation cost against what was quoted, and where did the difference come from?
- What did you discover after signature that you wish you had asked?
- Has the roadmap you were shown actually arrived?
- Would you buy it again? — and then wait through the pause.

**Ask for someone comparable.** A reference three times your size on a different continent tells you about a different product, because the supplier's attention scales with the account.

## Reading a supplier response

**A yes with no detail is a no in progress.** Where a response says a requirement is met with no explanation of how, the answer is usually "on the roadmap", "with customization", or "if you count this adjacent feature".

**"Configurable" and "customizable" are different words.** Configurable means someone sets it up. Customizable means someone writes something, which is a cost, an upgrade constraint, and a lock-in. Suppliers use them interchangeably; evaluations should not.

**Roadmap commitments are not commitments** unless they are in the contract with a date. A capability arriving "next release" has arrived when it has arrived.

## The sales relationship is not the working relationship

The part of a supplier an organization meets during a selection is the part engineered to be met. Attentive, responsive, senior. That team is not who answers the support ticket in month eight.

So `vendor_workability` is scored from **references and observed behaviour during the evaluation**, never from how the account team feels to deal with. Useful observations during the evaluation itself:

- Did they answer the hard question, or answer a different one?
- Did they volunteer a limitation before being asked? *(This one is worth a great deal — it is rare and it correlates with everything else.)*
- Did they meet their own deadlines during the process, when they were trying hardest?
- Did they push back on a requirement that genuinely does not suit them, or agree to everything?

A supplier who agrees to everything during a selection has either not read it or is planning to renegotiate later.

## Analyst positions and published evaluations

Useful for finding candidates. Not useful for choosing between them.

An analyst position describes a market as a whole — vendor scale, roadmap ambition, geographic coverage — against criteria that are not this organization's. It knows nothing about the estate, the volumes, the constraints, or the requirements. A product ranked highly in a market can be entirely wrong for one organization in it, and frequently is.

**Cite it as one input among several. Never reproduce its content**, which is licensed, and never let it be the recommendation. Where a selection is being justified primarily on an analyst position, that is a finding to report rather than a rationale to accept.
