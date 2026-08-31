---
name: customer-journey-to-system-map
description: >
  Maps what a customer is trying to do at each stage of a journey onto the systems that
  stage actually touches, and locates the pain between them. Names stages for the customer's
  intent rather than the organization's process, scores whether the organization can even
  see what happens at each stage, and treats the stages with no system and no record as
  findings rather than gaps in the data. Produces the journey-to-system map, a pain point
  register, and the reasoning behind both.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.business.customer-journey-to-system-map
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: business
  yuman_ea_category: discover
  yuman_ea_owner_agent: business-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Customer Journey to System Map

Joins what the customer is trying to do to what the estate actually does, and finds the pain in between.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## The journey belongs to the customer

Stages are named for **what the customer is trying to do**, never for the organization's process.

| The customer's stage | The organization's name for it |
|---|---|
| Finding out whether it will arrive in time | Order status enquiry handling |
| Working out who to ask | Contact routing |
| Proving we already sent that | Documentation resubmission |

This is not presentation. A map whose stages carry the organization's names has already decided that the organization's view is the true one, and every finding after that is inside-out.

## The four things this finds

> **1. The stages with no system at all.** Waiting. Chasing. Asking a colleague what to do next. They are stages, they carry most of the effort, and they are absent from every map drawn from system data — which is why they have never been on an improvement list and will not appear on one by themselves.
>
> `visibility_to_organization` carries a full 0.20 weight for exactly this reason.

> **2. One stage, six systems.** The customer experiences a single action; behind it sit several systems that disagree. **The customer does not care about the seams, and the seams are where the pain is.**

> **3. Pain the organization has never heard about.** Internally inferred pain is wrong in a predictable direction: the organization knows about the problems it has been *told* about, and is blind to the ones customers work around silently or leave over. `pain_evidence` caps the whole run's confidence.

> **4. What happens when it goes wrong.** The least-mapped part of any journey. **Customers forgive failures and leave over how they were handled.**

## Status comes from the pattern

| Status | Meaning | What it needs |
|---|---|---|
| `high_effort` | The customer does the work | Remove steps, not add help |
| `fragmented` | The customer meets several organizations | One source of truth |
| `blind_spot` | The organization cannot see this stage | Instrumentation, or someone to ask |
| `no_recovery` | It fails and cannot be put right | A recovery path |
| `moment_of_truth` | This stage decides the relationship | Disproportionate attention |
| `non_conforming` | Breaches accessibility or residency | Reported with the policy ID |
| `smooth` | Nothing here needs a decision | — |

Rules are in [`references/journey-analysis-rules.md`](./references/journey-analysis-rules.md).

## When not to use this

| The question | Use |
|---|---|
| How does work flow end to end **inside** the business? | [`value-stream-map`](../value-stream-map/SKILL.md) |
| How does this one process run, with its controls? | [`business-process-model`](../business-process-model/SKILL.md) |
| Which of these systems do we replace? | [`application-rationalization`](../../portfolio/application-rationalization/SKILL.md) |
| What should the replacement be built on? | [`high-level-architecture`](../../technology/high-level-architecture/SKILL.md) |
| Does fixing this pay for itself? | [`business-case`](../business-case/SKILL.md) |

---

## Run it in this order

### 1. Frame

Restate the journey **from the customer's side**. A journey that starts where the organization's process starts has excluded everything the customer did to arrive — which is usually where they formed their opinion.

### 2. Ask

Five questions. Two decide whether the map finds anything:

- **`channel_coverage`** — a digital-only map finds a coherent journey and misses the stages where the customer gave up on the digital channel and phoned somebody. Those stages carry the effort, produce no system record, and are why the digital metrics look better than the relationship.
- **`include_failure_paths`** — **a journey with no failure paths is a brochure.**

### 3. Gather

Three required: the **journey definition**, the **stages in the customer's words**, and the **touchpoints**.

Two optional inputs carry a **high** penalty:

| Input | Why |
|---|---|
| `customer_research` | Without it, pain is what the organization has been told about |
| `drop_off_and_completion_data` | Where they stop is the only unarguable evidence in the run |

### 4. Bound

`accessibility_standard` and `data_residency` are hard constraints. A stage failing either is `non_conforming` **with the policy ID** — never quietly rated as merely poor.

### 5. Analyze

Name the stages for intent. **Include the stages with no channel.** Map to systems including the ones behind the screen. Score visibility explicitly. Locate pain *between* stages as well as within them.

### 6. Deliver

| Artifact | File |
|---|---|
| Journey to system map | `customer-journey-to-system-map--journey-system-map.md` \| `.csv` \| `.xlsx` |
| Pain point register | `customer-journey-to-system-map--pain-point-register.md` \| `.csv` \| `.xlsx` |
| Journey rationale | `customer-journey-to-system-map--journey-rationale.md` \| `.docx` |

**`organization_aware` is a column.** Where false, the pain has never been on anyone's list — and that fact is frequently more useful than the pain itself.

**Customer cost is stated in the customer's terms.** Time, calls, uncertainty, risk to their own operation. Not in the organization's terms, which is how a pain point becomes a cost saving and stops being about the customer.

### 7. Verify

**Confidence** is `low` if pain was inferred internally, if only digital channels were covered, or if failure paths were excluded — however complete the map looks.

**Sensitivity** includes the one that makes the method's own bias visible:

> **Remove every stage carried by phone, email, or a person.** That is the map the organization's analytics already produce. The gap between the two maps is the argument for the wider one.

---

## Standing rules

**A stage with no system is still a stage.** `channel: none` is a real value and those stages usually score worst.

**Pain at a system is a finding, not a disposition.** That a system is involved in a painful stage says nothing about whether it should be replaced — that decision rests on cost, contract, and estate evidence this method never sees.

**Attribute pain to a stage or a transition, never to a team.**

**Do not spread attention evenly.** A few moments decide the relationship; the rest the customer passes through without forming a view.

**One segment at a time where you can.** A large account with a named representative and a small account using self-service are having two different experiences, and the average describes neither.
