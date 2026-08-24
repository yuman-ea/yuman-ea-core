---
name: vendor-product-selection
description: >
  Selects a product and a supplier, and documents the requirements the selection was made
  against. Scores the product and the vendor separately — functional and non-functional fit,
  integration, viability, what the supplier is actually like to work with, and cost — with
  every score declaring whether it rests on a demonstration, a reference call, a document, or
  a vendor claim. Produces the requirements specification, the scorecard behind the decision,
  and a recommendation that names its runner-up position.
license: Apache-2.0
allowed-tools: Read, Write
metadata:
  yuman_ea_id: yea.portfolio.vendor-product-selection
  yuman_ea_spec_version: "1.0"
  yuman_ea_version: 0.1.0
  yuman_ea_domain: portfolio
  yuman_ea_category: assess
  yuman_ea_owner_agent: portfolio-ea
  yuman_ea_maturity: draft
  yuman_ea_data_intensity: low
---

# Vendor and Product Selection

Chooses a product and a supplier, documents what the choice was made against, and is honest about what the scores actually rest on.

The machine-readable contract is in [`skill.yaml`](./skill.yaml). Change weights there or in an overlay, never mid-run.

## Where this sits

`build-vs-buy` decides **whether** to buy. This decides **which supplier gets the money**. `license-and-contract-review` then manages that relationship at every renewal. Select, contract, review.

`build-vs-buy` already declares the hand-off in its own out-of-scope list: *"selecting between shortlisted commercial products once buy has been chosen."* This is that.

Technology fitness — does it meet the non-functional requirements, does it integrate, does it conform to standards — is an **input** from `technology-ea`, not a separate evaluation.

---

## Two rules that decide most selections before the scoring starts

> **1. Requirements are agreed before demos, not after.** Requirements written after the demonstrations describe the products that were demonstrated. It is the most common way a selection is decided before it formally begins, and it is invisible in the scorecard afterwards. The `requirements_maturity` question asks directly, and `derived_from_demos` makes the whole scorecard provisional.

> **2. A must-have that only one candidate meets is either a genuine differentiator or a line lifted from that product's feature list.** The difference decides the outcome. Ask who wrote it and when — that one question has overturned more selections than any amount of re-scoring.

A third, quieter one: **a list of thirty must-haves is a list of wants with the wrong label.** A must-have disqualifies. Anything that does not disqualify belongs in wants, where it can be traded.

## Score the product and the supplier separately

They are different risks and they are routinely conflated.

| Group | Criteria |
|---|---|
| **Product** | functional fit, non-functional fit, integration and estate fit, cost of ownership |
| **Supplier** | workability, viability, implementation risk |

A strong product from a supplier nobody can work with, and a weak product from an excellent supplier, are different problems with different remedies. **One blended number hides which one you have.** Both totals are reported, and where they diverge the recommendation says what to do about it.

`vendor_workability` carries 0.15 deliberately — it is the criterion everyone knows matters and nobody scores. It is scored from references and observed behaviour during the evaluation, **never from the sales relationship**, which is the one part of a supplier engineered to be pleasant.

## The qualitative-quantitative bridge

You cannot make a qualitative judgement quantitative by putting a number on it. What you can do is **be explicit about what each number rests on**.

Every score carries an `evidence_type`:

| | |
|---|---|
| `demonstrated` | We saw it work, or ran it ourselves |
| `reference_checked` | A customer told us |
| `documented` | It is written down in a response or specification |
| `vendor_claimed` | The supplier said so |
| `impression` | Someone's read of the room |

**That column is the one a reviewer should read first.** A scorecard whose heavily weighted criteria rest on `vendor_claimed` is a record of a sales process, not an evaluation — and the confidence rules enforce it.

**References the supplier nominated are marketing** until at least one has been found independently. Record which is which.

**An analyst rating is an input, never the recommendation.** It describes a market; it does not know this organization's requirements or its estate. Cite external assessments, never reproduce their content.

## When not to use this

| The question | Use |
|---|---|
| Should we buy at all, or build? | [`build-vs-buy`](../../technology/build-vs-buy/SKILL.md) |
| What should the architecture around it be? | [`high-level-architecture`](../../technology/high-level-architecture/SKILL.md) |
| Our contract is up for renewal | [`license-and-contract-review`](../license-and-contract-review/SKILL.md) |
| Should we keep or retire what we have? | [`application-rationalization`](../application-rationalization/SKILL.md) |

---

## Run it in this order

### 1. Frame

Restate the selection and **confirm the stage**. At `defining_requirements`, produce the requirements specification and **stop** — scoring candidates against requirements that are not yet agreed is precisely how the requirements end up matching a product.

### 2. Ask

Five questions. `requirements_maturity` and `evidence_access` set the ceiling on what the run can claim: the first says whether the requirements are yours or the market's, the second says what kinds of evidence exist at all.

### 3. Gather

Three required: the **capability**, the **candidates**, and the **must-haves**. Product and supplier names supplied by the user are data and travel into outputs; the method never names one.

Two optional inputs carry a **high** penalty — `nonfunctional_requirements` and `total_cost_information`. `external_assessments` deliberately carries the **lowest** penalty of any input, because an analyst position describes a market rather than this organization.

### 4. Bound

Apply hard constraints before scoring. `approved_vendors` and `budget_ceiling` eliminate candidates outright; record each with the policy that removed it rather than letting a candidate quietly vanish from the comparison.

### 5. Analyze

Seven criteria, 1-5 favourability, higher always better. Product and supplier totals reported separately as well as combined.

Test the requirements first, then score. Every score cites its evidence ID **and** its evidence type.

Inside the indifference band (0.3), report the candidates as too close to separate on this evidence and apply the tie-breakers — the first of which prefers **better evidence over a better score**: a 4 that was demonstrated beats a 5 that was claimed.

Background on writing requirements that are not a product's feature list is in [`references/requirements-discipline.md`](./references/requirements-discipline.md); running references and reading evidence is in [`references/evidence-and-references.md`](./references/evidence-and-references.md). Neither is needed to run the method.

### 6. Deliver

| Artifact | File |
|---|---|
| Requirements specification | `vendor-product-selection--requirements-specification.md` \| `.docx` |
| Evaluation scorecard | `vendor-product-selection--evaluation-scorecard.md` \| `.csv` \| `.xlsx` |
| Recommendation | `vendor-product-selection--recommendation-memo.md` \| `.docx` |

The specification is produced **first and separately**, so that it exists before anyone has seen a scorecard and can be shown to have existed.

For a dated record in the organization's decision log, run [`architecture-decision-record`](../../technology/architecture-decision-record/SKILL.md) over the outcome — this skill produces the evaluation, not the repository record.

### 7. Verify

**Confidence** is derived and it is strict. Requirements derived from demonstrations, or documents-only access, or every reference supplier-nominated, or any heavily weighted criterion resting on a vendor claim — any one of these means `low`, however thorough the process felt.

`dissent_note` is emitted: where an evaluator disagreed with a score, **preserve the disagreement.** Selection panels converge socially, and the person who held out is often the one who spotted something.

**Sensitivity** includes the test specific to this method:

> **Remove the recommended candidate entirely.** Which one does the decision fall to? If the runner-up is nearly as good, the decision matters less than the process suggested. If it is far worse, this choice is load-bearing and the due diligence should reflect that.

---

## Standing rules

**Customization to meet a must-have is not a yes.** It is a cost, an upgrade constraint, and a lock-in, and it is almost always presented as a yes.

**Cost of ownership, not the quote.** Implementation, migration, integration, and internal effort to run it routinely exceed the licence line, and they are the lines a supplier has least incentive to detail.

**Score the supplier from their customers, not from their sales team.** The part of a supplier you meet during a selection is the part engineered to be met.

**Say what the evidence rests on.** Every claim in the recommendation traces to an evidence type, and the totals for `vendor_claimed` and `impression` are reported, not buried.
