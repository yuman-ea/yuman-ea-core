# ADR-0000 — Initial architecture for Yuman EA

- **Status:** Accepted
- **Date:** 2026-08-10
- **Deciders:** @vishaljavalkar-ai, @rajesh-malviya
- **Supersedes:** none
- **Superseded by:** none

> **This is a decision record, not living documentation.** It captures what was decided at the founding of the project and why, including the options that were rejected. **Do not edit it.** If a decision here changes, write a new ADR that marks the relevant section superseded. The living, enforceable versions of these rules belong in `GLOSSARY.md`, `CONTRIBUTING.md`, `spec/`, and `CLAUDE.md` — see §15.

---

**An open-source framework of AI agents and skills for Enterprise Architecture.**
Version 0.3 · 2026-08-10

> **Naming policy.** "Yuman EA" is the project name and the only coined word in the system. Everything a contributor types — directories, IDs, YAML keys, enums — is plain English. Whatever the name means to you belongs in `README.md`, in one paragraph, and nowhere else. No invented vocabulary in code, paths, or schemas.

---

## 1. Design principles

Six decisions that everything else follows from. Put these at the top of `CONTRIBUTING.md`.

1. **Agents are few and stable. Skills are many and contributed.** The contribution surface is skills. If a common contribution requires touching an agent, the design is wrong.
2. **Skills are data, not code.** A skill is a markdown method plus a YAML contract. No programming language required to contribute one. This is the single biggest lever on contributor volume.
3. **Target the Agent Skills open standard; do not build runtime adapters.** `SKILL.md` in the standard layout is read by roughly 40 tools as of mid-2026 — Claude Code, Codex, Copilot, Cursor, Gemini CLI, Goose, Kiro. Conforming to the standard buys portability that hand-written LangGraph and CrewAI adapters would only approximate, at a fraction of the maintenance. *(Amended from v0.2, which specified a generated `runtimes/` layer. See §16.)*
4. **Every skill declares its inputs, its constraints, and what it does when data is missing.** An EA recommendation built on absent data is a well-formatted opinion. The framework must be honest about when it is guessing.
5. **Extend without forking.** Enterprises will need their own weights, policies, connectors, and skills. If the only way to get them is a fork, you lose every serious adopter. Overlays are a day-one requirement, not a later feature.
6. **No real enterprise data in the repo. Ever.** Schemas and synthetic fixtures only.

---

## 2. Naming conventions

Normative. Enforce with a linter in CI, not with review comments.

### 2.1 Identifiers

| Thing | Convention | Example |
|---|---|---|
| Repository | kebab-case | `yuman-ea-core` (org: `yuman-ea`; overlays live in separate repos) |
| Directories | kebab-case, plural for collections | `skills/`, `agents/`, `connectors/` |
| Skill ID | `yea.<domain>.<slug>` | `yea.technology.build-vs-buy` |
| Agent ID | `<domain>-ea`, orchestrator is `orchestrator` | `technology-ea`, `orchestrator` |
| Subagent ID | `<verb>-<noun>`, hyphenated | `app-profiler`, `cost-modeler` |
| Third-party / org skill | `x.<org>.<domain>.<slug>` | `x.acme.technology.mainframe-exit` |
| YAML keys | snake_case | `default_weights`, `on_missing` |
| Enum values | lowercase snake_case | `strategic_3_5y`, `estimate_with_assumption` |
| Artifact filenames | `<skill-slug>--<artifact>.<ext>` | `build-vs-buy--scorecard.xlsx` |
| Branches | `skill/<domain>-<slug>`, `spec/<topic>` | `skill/technology-build-vs-buy` |
| npm/PyPI packages | `@yuman-ea/<thing>` / `yuman_ea_<thing>` | `@yuman-ea/cli` |

The `x.` namespace matters more than it looks. It lets a vendor or an enterprise publish skills that can never collide with core IDs, which is what makes a third-party ecosystem possible at all.

### 2.2 File naming

Uppercase filename = written for a human. Lowercase = read by a machine.

```
skills/technology/build-vs-buy/
├── SKILL.md        # the method, prose, for humans
├── skill.yaml      # the contract, structured, for machines
├── assets/         # templates shipped with the skill
├── references/     # background loaded on demand, not upfront
└── evals/          # golden test cases
```

Same pattern for agents: `AGENT.md` + `agent.yaml`.

### 2.3 How to name a skill

**Name the decision or the deliverable, not the process.** Noun phrases, not gerunds.

| Good | Bad | Why |
|---|---|---|
| `build-vs-buy` | `evaluating-sourcing-options` | Names the decision an EA is asked to make |
| `application-rationalization` | `app-rat`, `rationalizer` | No invented abbreviations, no agent-nouns |
| `cloud-disposition` | `cloud-migration-helper` | "Helper", "manager", "handler", "service" are banned suffixes |
| `capability-model` | `business-capability-modeling-v2` | No version numbers in names; that's what semver is for |

Allowed acronyms — only these, only because every practicing EA already uses them: `ea`, `adr`, `tco`, `nfr`, `api`, `slo`, `bia`. Anything else is spelled out.

### 2.4 The two-name rule

Every concept has exactly one canonical name. If you want a friendlier label for docs or UI, put it in a `display_name` field — never a second directory, ID, or alias. Aliases are how vocabularies fragment.

---

## 3. Architecture

```
   L0  Orchestration      ┌──────────────────────────┐
                          │       orchestrator        │
                          └────────────┬─────────────┘
                                       │  routes on intent
        ┌──────────────┬───────────────┼───────────────┬───────────────┐
        ▼              ▼               ▼               ▼               ▼
   L1  Domain     business-ea    technology-ea    portfolio-ea      risk-ea
        agents                                                     (phase 4)

        │              │               │               │
        ▼              ▼               ▼               ▼
   L2  Workers    subagents — only where fan-out or context isolation is needed
                  app-profiler · comparable-finder · cost-modeler ·
                  dependency-tracer · evidence-collector · artifact-renderer

        │
        ▼
   L3  Skills     ~40-60 methods. One skill = one repeatable EA decision or deliverable.

   ── platform ──────────────────────────────────────────────────────────────────
   tools/  ·  connectors/  ·  context/  ·  templates/  ·  policies/  ·  evals/
```

Read the layers as **responsibility, not call depth**. L0 and L1 hold judgment — *which question is this, who owns it, are the answers coherent*. L3 holds method — *how a build-vs-buy is actually run*. L2 exists only for parallelism and context hygiene.

### L0 — orchestrator

Five responsibilities, and explicitly nothing else:

1. **Classify intent** — which EA question is this really?
2. **Decompose** — split compound requests into domain-owned parts.
3. **Assemble context** — pull the right slice of enterprise context and hand it down.
4. **Arbitrate** — when business-ea says "this capability is strategic" and portfolio-ea says "this app is unfunded," surface the conflict; never average it away.
5. **Synthesize** — one coherent answer, one artifact set, one traceable rationale.

Non-goals, stated in its own prompt: it does not run methods itself, and it does not invent data. **Orchestrator bloat is the most common failure mode in multi-agent systems** — the router quietly starts answering. Put an eval on exactly this: *given a build-vs-buy question, did it invoke the skill or answer from its own head?*

### L1 — domain agents

| Agent | Owns questions like | Signature skills |
|---|---|---|
| `business-ea` | "What capability does this serve?" "Where is the value-stream gap?" | capability-model, value-stream-map, operating-model-design, strategy-traceability, benefits-case |
| `technology-ea` | "Build or buy?" "Which pattern?" "Is this our standard?" | build-vs-buy, cloud-disposition, reference-pattern-selection, integration-strategy, technology-lifecycle, technical-debt-quantification, vendor-evaluation |
| `portfolio-ea` | "What do we fund?" "What's the sequence?" "What does it cost to run?" | application-rationalization, investment-prioritization, roadmap-sequencing, tco-model, obsolescence-heatmap, portfolio-merge |
| `risk-ea` *(phase 4)* | "What breaks us?" "Where's the concentration risk?" | threat-model-review, resilience-assessment, compliance-conformance, concentration-risk |
| `assurance-ea` *(phase 5)* | "Is our EA data trustworthy?" | repository-data-quality, model-conformance, ea-kpi-report |

Ship the first three. An empty agent is worse than a missing one.

---

## 4. Agent or skill? The decision rule

This is the question every contributor will get wrong first. Put the table in `CONTRIBUTING.md`.

| Make it a **skill** when… | Make it a **subagent** when… |
|---|---|
| It's a method, framework, or procedure | It needs its own context window |
| It produces a named deliverable | It fans out N-ways in parallel |
| Same steps every time, different inputs | It does long, noisy tool work you don't want in the parent's context |
| A human EA would call it "how we do X" | A human EA would call it "someone who goes and gets X" |
| *Build-vs-buy evaluation* | *`app-profiler` — reads 400 CMDB records, returns 400 normalized profiles* |

Applied to the obvious candidates: **build-vs-buy, application-rationalization, and cloud-disposition are all skills.** Application rationalization is one skill (the method, the rubric, the artifact) that *may* fan out an `app-profiler` subagent per application. The method is a skill; the labor is a subagent.

This matters commercially, not just aesthetically: **a skill is a pull request a stranger can write.** A subagent is an architectural change requiring a maintainer conversation. Push the contribution surface to L3 and the project scales.

---

## 5. Taxonomy

Two orthogonal axes. Domain determines ownership and directory; category determines routing and browsing.

**Domain** (owns it): `business` · `technology` · `portfolio` · `risk` · `assurance` · `cross`

**Category** (what kind of work it is) — a closed enum of eight:

| Category | What it does | Examples |
|---|---|---|
| `discover` | Find and normalize what exists | cmdb-harvest, vendor-scan, landscape-discovery |
| `assess` | Deep-dive a single thing | application-assessment, nfr-analysis, adr-authoring |
| `aggregate` | Roll up to an enterprise view | portfolio-rollup, capability-heatmap |
| `prioritize` | Score, weight, rank | investment-prioritization, technical-debt-quantification |
| `simplify` | Reduce and remove | application-rationalization, decommission-plan, standards-pruning |
| `design` | Produce a target state | target-architecture, roadmap-sequencing, scenario-model |
| `govern` | Enforce standards and policy | arb-review-pack, waiver-assessment, conformance-check |
| `align` | Move people and narrative | stakeholder-map, business-case-narrative, change-impact |

Closed enum, deliberately. An open category list becomes 40 categories within a year and stops being a navigation aid.

---

## 6. The skill contract — seven phases

Every skill implements the same seven phases in the same order. This single constraint is what turns 50 independent contributions into a coherent product.

| # | Phase | What it does |
|---|---|---|
| 1 | **Frame** | Capture the goal in the user's words; restate it as a precise EA decision statement |
| 2 | **Ask** | Only the questions that change the answer. Maximum five. Each declares *why it matters* |
| 3 | **Gather** | Required vs. optional inputs, source system, and explicit behavior when data is missing |
| 4 | **Bound** | Constraints: policy, budget, regulatory, standards, organizational red lines |
| 5 | **Analyze** | The actual method — framework, rubric, criteria, weights, reasoning steps |
| 6 | **Deliver** | Named artifacts with defined schemas |
| 7 | **Verify** | Assumptions register, confidence rating, sensitivity — what would change the answer |

**Phase 2 is declared as data, not prose.** This is what makes "framework-agnostic" real: the same block renders as a chat interview, a web form, or a batch API payload.

```yaml
ask:
  - id: decision_horizon
    question: "Is this a decision for the next 12 months or a 3-5 year commitment?"
    why: "Shifts weighting between TCO and strategic fit."
    type: choice
    options: [tactical_12m, strategic_3_5y]
    required: true
    default_if_skipped: strategic_3_5y
  - id: differentiation
    question: "Does this capability differentiate you competitively, or is it table stakes?"
    why: "Differentiating capabilities bias toward build; commodity biases toward buy."
    type: choice
    options: [differentiating, competitive_parity, commodity]
    required: true
```

**Phase 7 is not optional.** Confidence ratings and assumption registers are the difference between a credible EA tool and a plausible-sounding one. Make CI reject a skill that doesn't emit them.

---

## 7. Repository layout

```
yuman-ea-core/
├── README.md                    # what it is, in functional language, in the first line
├── CONTRIBUTING.md              # the primary on-ramp
├── GOVERNANCE.md
├── GLOSSARY.md                  # normative vocabulary
├── ROADMAP.md
│
├── spec/                        # the contract — source of truth
│   ├── skill.schema.json
│   ├── agent.schema.json
│   ├── artifact.schema.json
│   ├── overlay.schema.json
│   ├── lifecycle.md             # the seven phases, normative
│   └── standard-mapping.md      # how Yuman fields map to the Agent Skills standard
│
├── agents/
│   ├── orchestrator/            # AGENT.md + agent.yaml
│   ├── business-ea/
│   ├── technology-ea/
│   └── portfolio-ea/
│
├── skills/
│   ├── business/
│   ├── technology/
│   │   ├── build-vs-buy/
│   │   ├── cloud-disposition/
│   │   └── vendor-evaluation/
│   ├── portfolio/
│   └── cross/
│
├── subagents/                   # L2 workers
├── tools/                       # tool interface contracts, no vendor code
├── connectors/                  # servicenow · leanix · ardoq · csv · excel
├── templates/                   # shared artifact templates (adr, arb-pack, roadmap)
├── context/                     # SCHEMAS + synthetic fixtures only — never real data
│   ├── schema/
│   └── fixtures/northwind-corp/ # the canonical reference enterprise
│
├── overlays/                    # example org customization, see §8
├── cli/                         # scaffolding + validation + build
├── examples/
└── registry.json                # generated index the orchestrator reads
```

Two things worth defending in review:

- **`context/` never holds real enterprise data.** State it loudly in `CONTRIBUTING.md` on day one. The first time someone commits a real application inventory with vendor names and costs, the project has a legal problem and a trust problem simultaneously.
- **Skills are laid out to the Agent Skills standard.** `skills/<domain>/<slug>/SKILL.md` is directly loadable by any standard-compliant tool with no build step. `skill.yaml` carries the Yuman-specific contract alongside it. A skill that only works after a transform is a design failure.

---

## 8. Extension without forking — the adoption lever

The single most important thing for scale adoption, and the thing most OSS agent frameworks get wrong. An enterprise adopting this will immediately want to: change scoring weights, add its own policies, point at its own CMDB, and add three proprietary skills. If the answer is "fork it," they fork it, drift, and never contribute back.

**The overlay model.** A company keeps a small private repo that layers over the public one. Nothing in core is edited.

```yaml
# acme-ea-overlay/overlay.yaml
extends: yuman-ea-core@0.4.x

profile:
  organization: "Acme Corp"
  currency: USD
  fiscal_year_start: "04-01"

skill_overrides:
  yea.technology.build-vs-buy:
    weights:
      strategic_differentiation: 0.35   # Acme weights differentiation higher
      tco_5y: 0.15
    additional_criteria:
      - id: regulatory_data_residency
        weight: 0.10

policies:                                # feed every skill's Bound phase
  - id: cloud_first
    statement: "Prefer SaaS unless data residency or latency prohibits."
  - id: approved_vendors
    source: ./data/approved-vendor-list.csv

connectors:
  cmdb: servicenow
  ea_repository: leanix

skills:
  - x.acme.technology.mainframe-exit    # private skills, namespaced, never collide
```

Design consequences this forces on core, all of which are good hygiene anyway:

- Every weight, threshold, and criterion in a skill must be **declared and addressable**, never buried in prose.
- Skills reference policies **by ID**, not by inline text.
- Connectors are **swappable behind a tool interface**; a skill never names a vendor system.

---

## 9. Schemas

### `skill.yaml`

```yaml
spec_version: "1.0"
id: yea.technology.build-vs-buy
name: Build vs Buy Evaluation
version: 0.3.0                    # semver, per skill
domain: technology
category: design
owner_agent: technology-ea
maturity: proven                  # draft | usable | proven | certified
license: Apache-2.0

triggers:
  phrases: ["build or buy", "make vs buy", "should we build", "cots vs custom"]
  decision_types: [sourcing]

frame:
  restatement_template: >
    Determine whether to build, buy, or partner for {capability},
    optimizing for {primary_driver} over a {decision_horizon} horizon.

ask: [ ... ]                      # see §6

gather:
  required:
    - id: capability
      description: The business capability in scope
      source: context.capability_model
    - id: candidate_solutions
      source: [user, connector.vendor_catalog]
  optional:
    - id: internal_cost_baseline
      source: connector.finance
      on_missing: estimate_with_assumption

bound:
  policies: [cloud_first, approved_vendors, budget_ceiling]

analyze:
  method: weighted_multi_criteria
  criteria:
    - {id: strategic_differentiation, weight: 0.25}
    - {id: tco_5y,                    weight: 0.20}
    - {id: time_to_value,             weight: 0.15}
    - {id: integration_complexity,    weight: 0.15}
    - {id: vendor_risk,               weight: 0.10}
    - {id: talent_availability,       weight: 0.10}
    - {id: exit_cost,                 weight: 0.05}
  weights_overridable: true
  references: [./references/sourcing-criteria.md]

deliver:
  artifacts:
    - {id: recommendation_memo, format: docx, template: templates/decision-memo}
    - {id: option_scorecard,    format: xlsx, template: templates/scorecard}
    - {id: decision_record,     format: md,   template: templates/adr, always: true}

verify:
  emits: [assumptions_register, confidence_rating, sensitivity_analysis]
  evals: ./evals/
```

### `agent.yaml`

```yaml
spec_version: "1.0"
id: technology-ea
name: Technology EA
role: Technology and solution architecture decisions
owns_questions:
  - "Build, buy, or partner?"
  - "Which reference pattern applies?"
  - "Does this conform to our technology standards?"
refuses:
  - question: "Investment funding decisions"
    route_to: portfolio-ea
  - question: "Business capability definition"
    route_to: business-ea
skills: [yea.technology.*]
subagents: [app-profiler, comparable-finder]
escalates_to: orchestrator
```

`refuses` is doing real work. In multi-agent EA systems the failure mode is never "no agent answered" — it's "three agents answered differently." Make boundaries declarative and machine-checkable, and have CI flag overlapping `owns_questions` across agents.

---

## 10. Worked example — `yea.portfolio.application-rationalization`

**Frame.** User: *"We have too many apps in HR, help us clean up."*
Restated: *"Determine a tolerate / invest / migrate / eliminate disposition for each application supporting the HR capability domain, with a sequenced 24-month execution plan."*

**Ask** (5 max): scope boundary (capability vs. org unit vs. cost center) · primary driver (cost / risk / agility / post-merger) · disposition horizon · non-negotiables (systems that cannot be touched) · available data quality tier.

**Gather.** Required: application inventory, capability mapping, annual cost, business criticality, technical fitness. Optional: user counts, incident volume, contract end dates. Missing data drops to a documented proxy and flags reduced confidence — **never silently imputed.**

**Bound.** Regulatory retention obligations, in-flight programs, works-council constraints, contractual lock-in.

**Analyze.** Business value × technical fitness placement → functional-redundancy clustering → cost-of-change vs. benefit → sequence by dependency and contract expiry.

**Deliver.** `application-rationalization--scorecard.xlsx` (per-app scores and disposition) · `application-rationalization--roadmap.pptx` (waves) · `application-rationalization--savings-model.xlsx` (run-rate reduction with confidence bands) · `application-rationalization--adr.md`.

**Verify.** Assumptions register; per-application confidence driven by data completeness; sensitivity — *which dispositions flip if cost data is ±20% wrong*; three golden eval cases with expected dispositions.

Execution notes: fans out `app-profiler` once per application, calls `artifact-renderer` for outputs, and never touches a connector directly — always through the tool interface.

---

## 11. Versioning, distribution, compatibility

| Concern | Approach |
|---|---|
| **Spec version** | `spec_version` on every artifact. Breaking spec changes require an RFC and a major bump |
| **Skill version** | Semver per skill. Weight or criteria changes = minor; changed output schema = major |
| **Release** | The repo releases as a set; `registry.json` pins skill versions per release |
| **Distribution** | `yea install` pulls a release or a subset. Skill *packs* (e.g. `pack:cloud-migration`) bundle related skills |
| **Standard conformance** | Every skill validates against the Agent Skills standard *and* `spec/skill.schema.json`. CI checks both. Portability is inherited from the standard, not built |
| **Deprecation** | Minimum two releases with a `deprecated: true` flag and a `superseded_by` pointer before removal |

---

## 12. Contribution and governance

**Tiered review** — the thing that prevents maintainer burnout:

| Change type | Reviewer | Bar |
|---|---|---|
| New skill, `draft` maturity | One domain maintainer | Schema-valid, 3 evals, no real data |
| Promote skill to `proven` | Domain maintainer + one practitioner review | Evals pass, used on a real decision, artifacts reviewed |
| New agent or subagent | Two core maintainers | RFC |
| Spec change | RFC + core maintainer consensus | Migration path documented |

**Maturity levels are how you say yes without endorsing.** `draft` · `usable` · `proven` · `certified`, shown as a badge in the skill index. You can merge a rough contribution at `draft` rather than rejecting it or rewriting it yourself — the single most useful mechanic for keeping first-time contributors.

**Structural choices:**

- **CODEOWNERS per domain directory.** Domain maintainers own `skills/technology/`, etc. Recruit them from practicing EAs, not developers.
- **DCO, not a CLA.** A sign-off line is a low enough bar that individual EAs will clear it; a CLA will lose you contributors who'd need legal review.
- **Apache-2.0.** The explicit patent grant matters for enterprise adoption in a way MIT doesn't.
- **Framework IP.** TOGAF, BIZBOK, and various analyst frameworks have licensing considerations. **Reference and cite; never reproduce proprietary content into the repo.** Say this in `CONTRIBUTING.md` before it becomes an issue, and prefer neutral formulations of common methods.
- **RFC process** in `spec/rfcs/`, for spec and agent changes only. Skills never need an RFC — that's the point.
- **No telemetry.** For an EA tool touching application portfolios and costs, any phone-home kills enterprise adoption. Make it a stated non-goal.

**Contributor on-ramp — in priority order:**

1. `yea new skill --domain technology --category design` scaffolding a compliant skeleton. Worth more to adoption than five more skills.
2. **One canonical synthetic enterprise** (`context/fixtures/northwind-corp/`) — 120 applications, capability model, costs, contracts. Every eval runs against it. This single asset does more for onboarding than any volume of documentation.
3. A 15-minute quickstart that ends with a real generated artifact.
4. `good-first-skill` labeled issues, each naming the method and the expected deliverable.
5. Schema validation + eval runs in CI, so review is about EA judgment rather than formatting.

**Discoverability.** Nobody searching for "enterprise architecture AI agents" searches for a project name they've never heard. The README's first line, the repo description, and the GitHub topics must be relentlessly functional: *enterprise-architecture, ai-agents, togaf, application-portfolio-management, architecture-governance*. The name and the positioning go in paragraph two.

One check worth doing before you commit to it: "Yuman" is also the name of an Indigenous language family and people of Arizona, California, and Baja California, and Yuma is a US city. That's not a blocker — it's a coined product name in an unrelated field — but it does mean unqualified searches for "yuman" won't surface you. Always publish as **"Yuman EA"**, never "Yuman" alone.

---

## 13. Build order

| Phase | Scope | Done when |
|---|---|---|
| **0 — Spec** | GLOSSARY, lifecycle, schemas, CONTRIBUTING, CLI scaffold | An outsider writes a valid skill without asking you a question |
| **1 — Vertical slice** | orchestrator + technology-ea + **one** skill (build-vs-buy) + CSV connector, packaged to the Agent Skills standard | **Ten practising EAs run it on a real decision and at least two return to it unprompted.** See §17 |
| **2 — Breadth** | business-ea + portfolio-ea, 3-4 skills each, artifact-renderer, generated registry | Orchestrator routes a compound question across two domains and synthesizes one answer |
| **3 — Community** | Eval harness in CI, overlay mechanism, good-first-skill issues, ~15 skills | First merged PR from someone you don't know |
| **4 — Ecosystem** | risk-ea, ServiceNow/LeanIX connectors, published skill packs | A team you have never met runs it on their own portfolio |

Resist starting at phase 2. Three half-built domain agents demo worse than one that genuinely works.

---

## 14. Anti-patterns to name explicitly in CONTRIBUTING

1. **Orchestrator bloat** — the router starts answering instead of routing. Guard with an eval.
2. **Skills that require code** — the moment a skill needs a Python file to be useful, your contributor pool shrinks by 10x. Push logic into declared criteria and weights.
3. **Method without data** — a build-vs-buy with no cost baseline. Mitigated by `on_missing` behavior and mandatory confidence ratings.
4. **Vendor names inside skills** — a skill that says "query ServiceNow" is unusable at the next company. Always go through the tool interface.
5. **Alias creep** — two names for one concept. See the two-name rule (§2.4).
6. **Agent proliferation** — every new domain looks like it needs an agent. Most need a skill. Adding an agent requires an RFC precisely to create that friction.

---

## 15. Where this document lives

Yes — it belongs in the repository. But **do not commit it as one file called `DESIGN.md`.** A monolithic design doc is the most reliably rotten artifact in any open-source repo: within three months it disagrees with the code, and contributors can't tell which one is authoritative.

Split it by *how each part ages*:

| Part of this doc | Goes to | Why |
|---|---|---|
| §2 Naming conventions | `GLOSSARY.md` + a CI linter | Normative. Must be enforceable, not aspirational |
| §4 Agent-vs-skill rule, §12 contribution model, §14 anti-patterns | `CONTRIBUTING.md` | Where a contributor actually looks |
| §6 Seven phases, §9 schemas, §11 versioning | `spec/lifecycle.md`, `spec/*.schema.json` | Machine-checkable; the schema *is* the spec |
| §3 Architecture, §5 taxonomy, §8 overlays | `docs/architecture.md` | Living overview, updated with the code |
| §1 Principles, §13 build order | `README.md` + `ROADMAP.md` | The pitch and the plan |
| **The reasoning** — *why* skills over subagents, *why* a closed category enum, *why* overlays | `docs/adr/0001-*.md` … | Frozen, dated, never edited |

The distinction that matters: **normative documents get updated; decision records get superseded.** An ADR says "on 2026-08-10 we decided X, because Y, having rejected Z." You never edit it — if you change your mind, you write ADR-0009 marking 0001 superseded. That preserves the reasoning trail, which is what stops a new contributor in month eight from reopening a settled argument.

Practical suggestion: commit this file **as-is** at `docs/adr/0000-initial-architecture.md`, dated and marked *accepted*, then distribute the living parts to the destinations above. The blueprint becomes the historical record of the founding decisions; the enforceable parts become CI.

One more: keep `docs/` in the same repo, not a separate docs site, until you have real adoption. Split repos are where documentation goes to die.

---

## 16. Amendments to v0.2, and the options rejected

Recorded here because the reasoning is the part that's expensive to reconstruct.

### 16.1 Rejected: a generated `runtimes/` adapter layer

v0.2 specified generating Claude Code, LangGraph, and CrewAI adapters from the spec. **Rejected.** Agent Skills became an open standard in December 2025; by mid-2026 roughly 40 products read the same `SKILL.md` from the same directory layout. Conforming to the standard delivers the portability the adapter layer was invented to provide, without the maintenance surface. MCP covers the complementary question — MCP is *what the agent can reach*, Skills are *how the agent should work*. Yuman EA sits in the second layer and connects to the first.

Consequence: `spec/conformance.md` becomes `spec/standard-mapping.md` — documenting how Yuman's `skill.yaml` relates to the standard's frontmatter, rather than defining a compliance regime of our own. **Do not invent a competing format.**

### 16.2 Rejected: mythological vocabulary in code

An earlier draft named agents and lifecycle phases after figures and concepts from the Ramayana. **Rejected** on contributor-cost grounds: it required learning roughly 25 terms before filing a first pull request, in a project whose binding constraint is contributor supply. The name "Yuman EA" is retained; nothing else carries story. See the naming policy at the top.

### 16.3 Rejected: building breadth before demand evidence

v0.2's build order implied moving from phase 1 to phase 2 on completion. **Amended:** phase 2 is gated on a demand signal, not on phase 1 being finished. See §17.

### 16.4 Open question: license

The repository currently ships MIT. Apache-2.0 was recommended for its explicit patent grant, which matters to enterprise legal review — the exact audience this project targets. Relicensing requires agreement from every contributor, so the cost of this decision rises with every merged PR. **Decide it while the contributor count is small.** Not decided as of this ADR.

---

## 17. Scope discipline — what phase 1 is allowed to contain

The failure mode for a project like this is not building the wrong thing. It is building *all* of it before finding out whether anyone wants any of it.

**Phase 1 ships exactly this:**

- `spec/` — skill, agent, and overlay schemas; `lifecycle.md`; `standard-mapping.md`
- `GLOSSARY.md`, `CONTRIBUTING.md`, `CLAUDE.md`, rewritten `README.md`
- `agents/orchestrator/` and `agents/technology-ea/`
- `skills/technology/build-vs-buy/` — complete: `SKILL.md`, `skill.yaml`, assets, references, three evals
- `context/fixtures/northwind-corp/` — synthetic reference enterprise, ~20 applications
- `docs/adr/0000-initial-architecture.md` — this file

**Phase 1 explicitly does not contain:** additional skills, business-ea, portfolio-ea, the CLI, connectors beyond CSV, or the artifact renderer. Each is justified only by evidence phase 1 hasn't produced yet.

**The gate to phase 2** is not "phase 1 is complete." It is: *ten practising enterprise architects run the build-vs-buy skill on a real decision, and at least two return to it unprompted.* If that doesn't happen, the correct response is to fix the skill or change the target user — not to add more skills. Breadth cannot rescue a method nobody wanted.

**The target user is worth stating plainly**, because it shapes every subsequent decision: EA teams with **no** EA tool. The teams running on Excel, Visio, and PowerPoint, whom no vendor is courting, and who face the same decisions as teams with a six-figure platform. Teams that already own SAP LeanIX or Ardoq get their copilot bundled with their data; competing there is a losing position. Teams with no tool have no incumbent at all.

---

---

*`GLOSSARY.md` is the normative vocabulary. This document is the reasoning behind it.*
