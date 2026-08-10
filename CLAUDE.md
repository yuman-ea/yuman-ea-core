# CLAUDE.md — standing constraints for Yuman EA

Read this before changing anything in this repository. It is not a summary of the docs; it is the set of rules that keep contributions — human and agent — consistent. When this file and a generated suggestion disagree, this file wins.

Full reasoning, including options that were considered and rejected, is in `docs/adr/0000-initial-architecture.md`. That file is a frozen decision record — **never edit it.** If a decision changes, add a new ADR.

---

## What this is

An open framework of AI agents and skills for Enterprise Architecture, covering business architecture, technology architecture, and portfolio management. Skills encode repeatable EA methods — build-vs-buy, application rationalization, cloud disposition — as declarative contracts that produce defined artifacts.

## Mission — codify enterprise architecture

**EA's methods live in consultants' heads, proprietary platforms, and expensive training. This project writes them down** — as open, executable skills that state their criteria, their weightings, the data a decision actually requires, and the artifact it should produce. Any organization can run them, inspect them, argue with them, and override them for its own context. Success is a real decision improved: an architect who can walk into a steering committee with analysis that holds up.

**Built for every organization. Designed against the hardest case.** A method that produces defensible analysis from incomplete data also works when the data is complete; the reverse is not true. So when a design choice is genuinely arguable, resolve it in favor of the architect with no platform, no budget, and partial data. That is a design tiebreaker, not a market boundary — large enterprises are first-class users, and the overlay mechanism exists for them.

Three rules follow, and they are not negotiable:

1. **Degrade honestly, never demand.** The defining constraint on this user is *missing data*, not missing software. A skill that requires a complete application inventory before it produces anything is useless to the person we built this for. Declare `on_missing` behavior for every optional input, state the assumption made, and lower the confidence rating accordingly. Prefer low-`data_intensity` skills in early phases.
2. **Output must be defensible by a non-specialist.** The user takes the artifact to a CFO or a steering committee. Deliverables explain their reasoning in business language, not framework vocabulary. Nobody should need to have read TOGAF to defend the result.
3. **Always show the work.** The assumptions register, confidence rating, and sensitivity analysis in `verify` are not quality garnish — they are the product. A consultancy's actual deliverable is a defensible argument, and that is what we are replacing.

Corollary for prioritization: **success is a real decision improved, not a star count.** The people this serves are largely not on GitHub. Judge the project by practitioners who return to it, not by repository metrics.

---

## Prime directives

1. **Skills are data, not code.** A skill is markdown plus YAML. If a skill needs a Python file to be useful, redesign it. This is the single biggest lever on contributor volume — protect it.
2. **Agents are few and stable; skills are many and contributed.** If a routine contribution requires touching an agent, the design is wrong.
3. **Never commit real enterprise data.** Schemas and synthetic fixtures only. No real application inventories, vendor names tied to costs, or customer identifiers — ever, in any form, including examples and test data.
4. **No vendor names inside skills.** A skill that says "query ServiceNow" is useless at the next company. Go through the tool interface in `tools/`.
5. **Every weight, threshold, and criterion is declared and addressable** in `skill.yaml` — never buried in prose. Organizations override them via overlays; buried values can't be overridden.
6. **Conform to the Agent Skills standard.** `skills/<domain>/<slug>/SKILL.md` must be directly loadable by any standard-compliant tool with no build step. Do not invent a competing format.
7. **No telemetry.** Anything phoning home from a tool that reads application portfolios and costs fails enterprise security review. This is a permanent non-goal.

---

## Naming — enforce exactly

| Thing | Convention | Example |
|---|---|---|
| Directories | kebab-case, plural for collections | `skills/`, `agents/`, `connectors/` |
| Skill ID | `yea.<domain>.<slug>` | `yea.technology.build-vs-buy` |
| Agent ID | `<domain>-ea`; the router is `orchestrator` | `technology-ea` |
| Subagent ID | `<verb>-<noun>` | `app-profiler`, `cost-modeler` |
| Third-party / org skill | `x.<org>.<domain>.<slug>` | `x.acme.technology.mainframe-exit` |
| YAML keys | snake_case | `default_weights`, `on_missing` |
| Enum values | lowercase snake_case | `strategic_3_5y` |
| Artifact filenames | `<skill-slug>--<artifact>.<ext>` | `build-vs-buy--scorecard.xlsx` |
| Branches | `skill/<domain>-<slug>`, `spec/<topic>` | `skill/technology-build-vs-buy` |

**UPPERCASE filename = written for a human. lowercase = read by a machine.** `SKILL.md` + `skill.yaml`, `AGENT.md` + `agent.yaml`.

### Naming a skill

Name the **decision or deliverable**, not the process. Noun phrases, never gerunds.

- Good: `build-vs-buy`, `application-rationalization`, `cloud-disposition`, `capability-model`
- Bad: `evaluating-sourcing-options`, `app-rat`, `rationalizer`, `cloud-migration-helper`

**Banned suffixes:** `-helper`, `-manager`, `-handler`, `-service`, `-util`. **Banned:** version numbers in names (that's what semver is for), invented abbreviations, aliases of any kind.

**Allowed acronyms — this list only:** `ea`, `adr`, `tco`, `nfr`, `api`, `slo`, `bia`. Everything else is spelled out.

**One canonical name per concept.** A friendlier label goes in a `display_name` field — never a second directory, ID, or alias.

---

## Closed enums — do not extend without an ADR

**`domain`:** `business` · `technology` · `portfolio` · `risk` · `assurance` · `cross`

**`category`:** `discover` · `assess` · `aggregate` · `prioritize` · `simplify` · `design` · `govern` · `align`

**`maturity`:** `draft` · `usable` · `proven` · `certified`

These are closed deliberately. An open category list becomes forty categories within a year and stops being a navigation aid. Adding a value requires an ADR.

---

## The seven-phase skill contract

Every skill implements all seven, in this order, using these exact key names in `skill.yaml`:

| Key | Purpose |
|---|---|
| `frame` | Restate the user's goal as a precise EA decision statement |
| `ask` | Only questions that change the answer. **Maximum five.** Each declares `why` |
| `gather` | Required vs. optional inputs, source, and explicit `on_missing` behavior |
| `bound` | Constraints referenced **by policy ID**, never inline text |
| `analyze` | Method, criteria, weights, reasoning steps |
| `deliver` | Named artifacts with defined schemas |
| `verify` | Assumptions register, confidence rating, sensitivity analysis |

**`ask` is structured data, not prose.** It must render as a chat interview, a web form, or a batch payload without modification.

**`verify` is not optional.** Confidence ratings and assumption registers separate a credible EA tool from a plausible-sounding one. CI rejects skills that don't emit them.

**Write skills that constrain, not skills that explain.** The model already knows what TOGAF is; a skill that teaches the framework adds nothing and decays as models improve. Encode decision rubrics, data contracts, artifact schemas, and run-to-run consistency. That's the durable part.

---

## Skill or subagent?

| Skill | Subagent |
|---|---|
| A method, framework, or procedure | Needs its own context window |
| Produces a named deliverable | Fans out N-ways in parallel |
| Same steps, different inputs | Long, noisy tool work |
| "How we do X" | "Someone who goes and gets X" |
| *build-vs-buy* | *`app-profiler` — reads 400 CMDB records, returns 400 profiles* |

Build-vs-buy, application-rationalization, and cloud-disposition are **skills**. A skill may fan out subagents for labor; the method stays in the skill.

---

## Where things go

```
spec/          schemas + lifecycle.md + standard-mapping.md   ← the contract
agents/        orchestrator + <domain>-ea                     ← judgment
subagents/     L2 workers                                      ← labor
skills/        <domain>/<slug>/                                ← method (the contribution surface)
tools/         tool interface contracts, no vendor code
connectors/    vendor adapters behind those interfaces
templates/     shared artifact templates
context/       schemas + synthetic fixtures ONLY
overlays/      example org customization
docs/adr/      frozen decision records
```

`GLOSSARY.md` is the normative vocabulary. `CONTRIBUTING.md` is the contributor on-ramp.

---

## The orchestrator does five things

Classify intent · decompose · assemble context · arbitrate conflicts between domain agents · synthesize.

**It does not run methods itself, and it does not invent data.** Orchestrator bloat — the router quietly starting to answer instead of routing — is the most common failure in multi-agent systems. There is an eval for exactly this: given a build-vs-buy question, does it invoke the skill or answer from its own head?

---

## Scope guard — we are in phase 1

**Phase 1 ships:** `spec/`, the four root docs, `orchestrator` + `technology-ea`, **one** complete skill (`build-vs-buy`), the `northwind-corp` synthetic fixture, and ADR-0000.

**Phase 1 does not ship:** additional skills, `business-ea`, `portfolio-ea`, the CLI, connectors beyond CSV, or the artifact renderer. Do not add these because they seem obviously needed — each is justified only by evidence phase 1 hasn't produced yet.

**The gate to phase 2** is a demand signal, not completion: ten practising EAs run build-vs-buy on a real decision, and at least two return unprompted. If that doesn't happen, fix the skill or change the target user. Breadth cannot rescue a method nobody wanted.

If asked to scaffold "the whole framework," build phase 1 and say why the rest is deferred.

---

## Anti-patterns — reject these in review

1. **Orchestrator bloat** — the router answering instead of routing.
2. **Skills requiring code** — shrinks the contributor pool tenfold.
3. **Method without data** — a build-vs-buy with no cost baseline is a well-formatted opinion. Hence mandatory `on_missing` and confidence ratings.
4. **Vendor names in skills** — unusable at the next company.
5. **Alias creep** — two names for one concept.
6. **Agent proliferation** — every new domain looks like it needs an agent. Most need a skill. New agents require an ADR, precisely to create that friction.
7. **Editing an ADR** — supersede it with a new one instead.

---

## Open decisions

- **License.** Repo currently ships MIT. Apache-2.0 was recommended for its explicit patent grant, which matters to the enterprise legal reviews this project's users will face. Relicensing needs every contributor's agreement, so the cost rises with each merged PR. Unresolved — see ADR-0000 §16.4.
