# ADR-0001 — Invocation and distribution, individual architect first

- **Status:** Accepted
- **Date:** 2026-08-10
- **Deciders:** @vishaljavalkar-ai, @rajesh-malviya
- **Supersedes:** none
- **Superseded by:** none

> Decision record. Do not edit — supersede with a new ADR if this changes.

---

## Context

ADR-0000 defines what a skill is and how it is structured. It does not say how anyone reaches one. Without that decision, the exemplar skill will be built around unstated assumptions about its runtime, and those assumptions are expensive to unwind later.

The mission commits us to the architect who has no EA platform, no framework training, and no consulting budget. That person is not a developer. Any distribution path requiring a terminal, a package manager, or a build step excludes them — which would make the mission decorative.

Three adopter tiers exist, and they differ only in where data comes from, not in what the skills are:

| Tier | Data source | Setup cost |
|---|---|---|
| **Individual architect** | Manual entry, CSV, the architect's own knowledge | Minutes |
| **EA team** | Shared overlay repo with team weights, policies, CSV exports | An afternoon |
| **Enterprise** | Tools backed by MCP servers over ServiceNow, LeanIX, Ardoq | Integration work |

**The individual tier is the primary target for phase 1.** The other two are supported by the same skills without modification, and are not optimized for until the phase-2 gate is met.

---

## Decision

### 1. Invocation is through Agent Skills standard host tools

Skills are invoked inside a tool the architect already has — Claude Desktop, Claude Code, Copilot, Cursor, Gemini CLI, or any of the other standard-compliant hosts. **Yuman EA ships no runtime, no server, no account, and no application of its own.**

This follows directly from ADR-0000 §16.1. The consequence worth stating explicitly: the architect's cost of entry is zero beyond a subscription they already have. There is nothing to procure, pilot, or get approved.

### 2. Two invocation modes, both required

**Direct** — the skill is named: *"Run build-vs-buy for our customer portal."* Predictable and repeatable. This is how someone uses it the fifth time.

**Conversational** — no skill is named: *"We're trying to decide whether to build or buy a customer portal."* The orchestrator classifies intent, routes to the owning domain agent, which invokes the skill. This is what makes the framework feel like an advisor rather than a command line.

The `triggers` block in `skill.yaml` exists to serve the conversational mode. **A skill with weak or missing triggers is effectively invisible**, and should fail review on that basis alone. Conversational invocation drives adoption; direct invocation makes results trustworthy. Both are required.

### 3. Distribution is a versioned archive attached to GitHub Releases

Every release publishes `yuman-ea-skills-<version>.zip`, containing the skills in the standard layout, unzipped by the architect into their host tool's skills folder. `docs/install.md` documents the folder location for each supported host and is updated at release time.

Where a host offers a plugin or marketplace mechanism, we publish there as well — lower friction still, at the cost of being host-specific. That is additive, never the only path.

**`git clone` remains available and is not the documented route for this tier.** It is how contributors work, not how practitioners install.

### 4. Markdown is the guaranteed artifact floor

Hosts differ in whether they can write `.docx` and `.xlsx` files. A skill must therefore always be able to produce its deliverables as markdown, and produce richer formats only where the host supports file generation.

This is a hard requirement on the `deliver` phase: **every artifact declares a markdown fallback.** A skill whose output is unusable without Office file generation is not usable by the tier we are building for.

### 5. Phase-1 skills require no connectors

At the individual tier there is no CMDB and no EA repository. Phase-1 skills must be fully usable with manual input and CSV alone. This is the practical enforcement of `data_intensity: low` and of the `on_missing` requirement — both stop being paperwork and become the thing that makes the product work at all.

### 6. Evals run against at least two hosts

Riding an open standard means behavior varies across implementations. A skill validated only in one tool will be mediocre elsewhere and we will not know. Claude Code is the reference host; at least one other standard-compliant host is checked before a skill is promoted beyond `draft`.

---

## Consequences

**Enabling:**

- Zero procurement, zero infrastructure, zero cost of entry for the primary user.
- No servers to run means no operational burden and no security review surface — consistent with the no-telemetry directive in ADR-0000.
- The same skills serve all three tiers; enterprise adoption is a connector swap behind the tool interface, not a different product.

**Constraining:**

- CI must build and attach the release archive. That is new work in phase 1.
- Every artifact needs a markdown form, which limits how much the framework can lean on spreadsheet-native output for scoring models.
- Cross-host eval doubles validation effort per skill.
- We inherit whatever the standard does and does not support. We do not extend it privately.

**Deferred:** a CLI installer, a hosted web form over the `ask` block, and any programmatic or batch invocation path. Each is justified only by evidence phase 1 has not yet produced.

---

## Rejected alternatives

**`git clone` as the documented install path.** Rejected. Requires git and a terminal. Excludes the primary user, and doing this would make the mission statement decorative.

**A Yuman EA web application.** Rejected. Introduces hosting, accounts, data custody, and a security review — precisely the procurement burden the mission exists to avoid. It would also put enterprise portfolio data on our infrastructure, which we will not do.

**Shipping only to one host's plugin marketplace.** Rejected as the sole channel. Convenient, but it converts an open framework into a single vendor's ecosystem and forfeits the portability that motivated ADR-0000 §16.1.

**Copy-paste of skill text into a chat window.** Rejected as the primary path. Zero install, but nothing persists, versions drift immediately, and there is no route to overlays or evals. Acceptable as a demo, not as distribution.

**A CLI installer in phase 1.** Deferred rather than rejected. It solves a real friction problem, but it is developer tooling and the phase-1 user is not a developer. Revisit if install friction is what the demand test actually surfaces.

---

## Open questions

- Which second host is the conformance reference? Decide before the first skill is promoted past `draft`.
- Does the release archive contain all skills, or per-domain packs? Trivial while there is one skill; decide before there are ten.
- Is `docs/install.md` maintained by hand or generated? Hand-maintained until it is wrong twice.

---

## How this is measured

The phase-2 gate in ADR-0000 §17 is unchanged, but this ADR makes it concrete: **ten practising architects install from a release archive, run build-vs-buy on a real decision, and at least two return unprompted.** If install friction is what stops them, that is a finding about this ADR, and it supersedes accordingly.
