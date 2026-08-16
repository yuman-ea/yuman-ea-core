# spec/standard-mapping.md — how Yuman EA relates to the Agent Skills standard

**Status:** normative.

This file documents how `skill.yaml` relates to the Agent Skills standard's `SKILL.md`. It is **not** a compliance regime of our own. ADR-0000 §16.1 rejected building runtime adapters precisely so that we would inherit portability from the standard rather than reimplement it — that decision only pays off if we resist extending the standard privately.

Three rules follow from it, and they are the whole point of this file:

1. **`skills/<domain>/<slug>/SKILL.md` is loadable by any standard-compliant host with no build step.** A skill that only works after a transform is a design failure.
2. **We do not invent a competing format.** Nothing Yuman EA needs is added to the standard's namespace; it goes in `skill.yaml` or in `metadata`.
3. **`skill.yaml` is the source of truth.** `SKILL.md` frontmatter is a hand-maintained projection of it, and CI checks the two agree (lifecycle.md R3).

---

## Why two files at all

The standard gives a host what it needs to *find and load* a skill: a name, a description, and the method in markdown. It has no opinion on scoring weights, missing-data behaviour, confidence rules, or artifact schemas — reasonably, since it is a general standard and those are enterprise-architecture concerns.

Yuman EA's contract is exactly those concerns. So:

| File | Audience | Contains |
|---|---|---|
| `SKILL.md` | Host tools, and the human reading the method | Standard frontmatter + the method in prose |
| `skill.yaml` | CI, overlays, the orchestrator | The seven-phase contract: weights, `on_missing`, policies, artifact schemas, confidence rules |

A host that knows nothing about Yuman EA reads `SKILL.md` and runs a usable skill. A host, overlay, or CI job that does know reads `skill.yaml` and gets the enforceable contract. Neither file duplicates the other's job; the overlap is three fields, listed below, and CI keeps them honest.

**Why not generate `SKILL.md` from `skill.yaml`?** Because generation implies a build step, and a build step breaks rule 1 above. The three shared fields are cheap to keep in sync by hand and cheaper still to check.

---

## Field mapping

### Standard frontmatter → Yuman EA

| `SKILL.md` frontmatter | `skill.yaml` | Rule |
|---|---|---|
| `name` | `name` | Must match exactly (R3). **Slug form** — see below |
| `description` | `description` | Must match exactly (R3). Written to carry trigger vocabulary — see below |
| `license` | `license` | Must match exactly (R3). SPDX identifier |
| `allowed-tools` | — | Declared in `SKILL.md` only; see the tools section below |
| `metadata` | mirrors identity fields | Advisory copy, see next table |
| — | `display_name` | Stays in `skill.yaml`. The standard has no home for it, and putting a human title in `name` breaks invocation |

### Why `name` is a slug and not a title

Hosts use frontmatter `name` as the skill's **invocation name**. In a plugin it becomes the last segment of the command (`/yuman-ea:build-vs-buy`); at personal and project scope it is the display label while the directory supplies the command. A value like `Build vs Buy Evaluation` therefore produces a command nobody can type.

So `name` carries the canonical slug — identical to the directory name and to the last segment of `id` — and `display_name` carries the human title used in artifact headings and skill indexes. This is not a concession to one host: it is ADR-0000 §2.4's two-name rule landing exactly where it was always pointed. One canonical name, one optional friendlier label, no third.

`display_name` is deliberately **not** mirrored into frontmatter. The standard has nowhere to put it, and a private key would be tolerated rather than supported.

### `metadata` block convention

Hosts that support a `metadata` map get the identity fields; hosts that do not, ignore it harmlessly. This is the only place Yuman-specific vocabulary touches the standard's file, and it is advisory — **`skill.yaml` remains authoritative for every one of these values.**

```yaml
---
name: Build vs Buy Evaluation
description: >
  Decides whether to build, buy, or partner for a business capability, using
  declared criteria and weights, and produces a scorecard, a recommendation
  memo, and a decision record — with assumptions, confidence, and sensitivity
  stated. Works from manual input and CSV; no portfolio tooling required.
license: Apache-2.0
metadata:
  yuman_ea_id: yea.technology.build-vs-buy
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: technology
  yuman_ea_category: design
  yuman_ea_owner_agent: technology-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---
```

Flat `yuman_ea_*` keys rather than a nested object: hosts vary in how deeply they surface `metadata`, and a flat map degrades to something readable everywhere.

### What has no home in the standard, and stays in `skill.yaml`

`triggers` · `frame` · `ask` · `gather` · `bound` · `analyze` · `deliver` · `verify` · `hosts_verified` · `deprecated` / `superseded_by`.

None of these are pushed into the standard's frontmatter, even where a host would tolerate unknown keys. Tolerated is not supported, and a private extension that half-works across forty tools is worse than a second file that works everywhere.

---

## Writing `description` — it is the trigger surface

`triggers.phrases` in `skill.yaml` is what the **orchestrator** routes on. But a host loading `SKILL.md` directly never sees `skill.yaml`, and routes on `description` alone.

So the description must do double duty: state what the skill decides, in the words a practitioner would use, and name the deliverable. Reflect the vocabulary from `triggers.phrases` into it rather than writing marketing prose.

- **Good:** "Decides whether to build, buy, or partner for a business capability… produces a scorecard, a recommendation memo, and a decision record."
- **Bad:** "A comprehensive framework-aligned approach to sourcing strategy." — Nothing a user would type appears in it.

A skill with a weak description is invisible in direct-host use for the same reason weak triggers make it invisible to the orchestrator (ADR-0001 §2), and fails review on the same basis (R23).

---

## `allowed-tools`

Declared in `SKILL.md` frontmatter where the host supports it, and kept minimal.

Phase-1 skills need to read files the architect provides and write artifacts. **They need no network access** — that follows from ADR-0001 §5 (no connectors) and from the no-telemetry directive. A phase-1 skill requesting network tools should be treated as a defect in the skill, not a requirement.

Enterprise adopters reach their CMDB or EA repository through MCP servers configured in *their host and their overlay* — never through a tool the skill demands. MCP is what the agent can reach; Skills are how it should work. Yuman EA sits in the second layer and does not reach into the first.

---

## Agents

The same two-file pattern, for the same reason: `agent.yaml` is authoritative, `AGENT.md` frontmatter is the host-facing projection, and CI checks they agree (R24).

| `AGENT.md` frontmatter | `agent.yaml` | Rule |
|---|---|---|
| `name` | `id` | Must match exactly (R24) |
| `description` | `description` | Must match exactly (R24). The delegation trigger — when to reach for this agent |
| `tools` | — | Declared in `AGENT.md` only, and currently left unset. See below |
| — | `role`, `owns_questions`, `refuses`, `skills`, `non_goals`, `layer`, `responsibilities` | No home in any host's agent format. Stays in `agent.yaml` |

**`name` must be explicit.** Both agents' files are called `AGENT.md`. A host that falls back to the filename would load one agent twice and drop the other, and it would do so silently.

**`description` is not `role`.** `role` says what the agent is responsible for and is read by people. `description` says *when to delegate to it* and is read by a router that knows nothing else about the agent. Keeping them separate is not alias creep — they answer different questions, and collapsing them makes the routing worse.

### The layer distinction does not survive the crossing

This is the part worth understanding before packaging.

Yuman EA's `orchestrator` is **L0** — the top of the stack, the thing that receives the question first. Most hosts' agent construct is a *subagent*: a delegate invoked by the main thread, running in its own context, returning a summary. Mapping the orchestrator onto that construct **inverts the architecture** — the router becomes something the router routes to.

Where a host can promote an agent to the main thread, use that instead. In Claude Code it is a `settings.json` key at the plugin root, or the `settings` field in `plugin.json`:

```json
"settings": { "agent": "orchestrator" }
```

L1 domain agents map onto the subagent construct cleanly and need no special handling.

Where a host has no main-thread mechanism, **do not ship the orchestrator as a subagent as a workaround.** Ship the domain agents and let the host's own top-level model route, which at least fails honestly. A router installed one level below where it belongs will quietly answer questions instead of routing them, which is the failure ADR-0000 §3 names as the most common in multi-agent systems.

### `tools` is deliberately unset

Neither agent restricts tools today. Skills already declare `allowed-tools`, which is the narrower and more portable control, and restricting an agent's tools risks blocking skill invocation in ways that vary by host. Tighten this once the behaviour has been verified on both conformance hosts — and record what was verified, rather than assuming it transfers.

## Extra files in the skill directory

```
skills/technology/build-vs-buy/
├── SKILL.md        ← the standard reads this
├── skill.yaml      ← the standard ignores this
├── assets/         ← referenced from SKILL.md by relative path
├── references/     ← referenced from SKILL.md by relative path
└── evals/          ← ignored by hosts; used by CI
```

Standard-compliant hosts load `SKILL.md` and ignore what they do not recognize. `assets/` and `references/` are referenced by relative path from the method prose so that progressive-disclosure hosts load them on demand rather than upfront — which is also why `references/` must never contain anything the method needs in order to run.

---

## Host variance, and the markdown floor

Riding an open standard means behaviour differs between implementations. The two differences that actually bite:

**File generation.** Some hosts can write `.docx` and `.xlsx`; some cannot. Hence the hard requirement that every artifact declare `md` among its `formats` (R11, ADR-0001 §4). Rich formats are an upgrade where available, never the only route to the deliverable.

**Progressive disclosure.** Hosts differ in when they load referenced files, and some load none. A skill must be correct if only `SKILL.md` is ever read; `references/` carries background, not method.

Evals therefore run against **at least two standard-compliant hosts** before a skill is promoted past `draft` (R22). Claude Code is the reference host. The second host is an open question in ADR-0001 and must be settled before the first promotion.

---

## Conflict resolution

| Situation | Resolution |
|---|---|
| `SKILL.md` frontmatter disagrees with `skill.yaml` | CI error (R3). `skill.yaml` is correct by definition; fix the frontmatter |
| The standard adds a field that duplicates something in `skill.yaml` | Adopt the standard's field, keep `skill.yaml` authoritative, and record the change here |
| A host requires a private key to work | It does not get one. Fix it in the host or accept the degraded behaviour and note it in `hosts_verified` |
| We want a capability the standard lacks | It goes in `skill.yaml`. We do not extend the standard's namespace |

The last row is the one that will be argued with. It was decided in ADR-0000 §16.1, and the cost of relitigating it is a maintenance surface across forty host tools.
