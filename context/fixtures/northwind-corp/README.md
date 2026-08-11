# Northwind Corp — synthetic reference enterprise

> ## Every figure in this directory is invented.
>
> Northwind Corp does not exist. The applications, costs, contracts, suppliers, and
> policies here were written to exercise the skills in this repository. **Nothing in
> this directory came from a real organization, and nothing real may ever be added to
> it** — no application inventories, no supplier names tied to costs, no customer
> identifiers, in any file, including examples (lifecycle.md R15).
>
> Suppliers are named `Vendor Alpha`, `Vendor Bravo`, and so on, precisely so that no
> reader can mistake one for a real product.

This is the canonical enterprise every eval runs against. One shared fixture does more
for onboarding than any volume of documentation: a contributor writing their second
skill already knows this estate, and two skills scored against the same twenty
applications can be compared.

---

## The company

Northwind Corp is a specialty food and beverage distributor.

| | |
|---|---|
| Revenue | USD 740m |
| Employees | ~1,800 |
| Sites | Head office, 4 regional distribution centres, 1 cold-storage facility |
| Customers | ~4,200 trade accounts — restaurants, independent grocers, regional chains |
| Products | ~11,000 SKUs, roughly a third temperature-controlled |
| IT team | 28.7 FTE across run and change |
| Application run cost | USD 10.0m in FY2026 |
| Fiscal year | Starts 1 April |

**Why this shape.** It is deliberately the organization ADR-0001 describes as the primary
user: large enough to have real architecture decisions, too small to have an EA platform.
There is no CMDB. The inventory below is a spreadsheet somebody maintains, and several
columns in it are estimates. That is the normal case, not the degraded one.

**What Northwind competes on.** Perishable logistics and trade pricing. Its route
planning, cold chain handling, and customer-specific pricing are where margin is won or
lost. Everything else — payroll, accounting, collaboration, service desk — it does the
same way as everybody else. This split is what makes it a useful fixture for
`build-vs-buy`: the correct answer genuinely differs by capability.

**The state of the estate.** Two decades of accumulation. A core order capture system
built in-house in 2009 that everything integrates with, a customer master from 2007 that
nobody wants to touch, a customer portal from 2014 that is failing, and a set of modern
cloud services bought in the last five years that work well. Technical fitness across the
estate averages just under 3 out of 5.

---

## Files

| File | What it holds | Rows |
|---|---|---|
| [`organization.yaml`](./organization.yaml) | Profile facts skills read: currency, fiscal year, discount rate, loaded cost per engineer | — |
| [`capabilities.csv`](./capabilities.csv) | Two-level business capability model with strategic importance | 30 |
| [`applications.csv`](./applications.csv) | The application inventory | 20 |
| [`application-costs.csv`](./application-costs.csv) | FY2026 run cost, broken into licence, hosting, support, and internal labour | 20 |
| [`vendors.csv`](./vendors.csv) | Suppliers, contract values, and expiry dates | 12 |
| [`integrations.csv`](./integrations.csv) | Point-to-point and brokered interfaces between applications | 26 |
| [`policies.csv`](./policies.csv) | Northwind's stated architecture policies, by ID | 8 |

CSV throughout, because CSV is what the target user can actually produce. There is no
connector, no database, and no loader — a skill reads these files or is handed the
relevant rows by its owning agent.

### How the numbers reconcile

- `application-costs.csv` totals **USD 9,995,500** for FY2026.
- `internal_labour_cost_usd` = `internal_ftes` × **USD 155,000**, the loaded engineer cost
  in `organization.yaml`. The two columns are consistent by construction, so a skill that
  derives one from the other gets the same answer as one that reads it directly.
- `total_cost_usd` is the sum of the four cost columns on each row.

### Deliberate gaps

The fixture has holes, on purpose. A skill that only works against complete data is not
the skill this project is trying to produce.

- **No historical cost.** One fiscal year only. Anything wanting a trend has to say it is
  assuming one.
- **No user counts for three applications** (`nw-005`, `nw-013`, `nw-015`). Blank, not zero.
- **`policies.csv` has no `budget_ceiling` entry.** A skill declaring that policy must
  take its `on_policy_absent` path rather than assuming there is no ceiling.
- **Two applications have no named business owner** (`nw-015`, `nw-019`) — both of them
  critical, which is the usual pattern rather than the unusual one.
- **No build-cost history.** Northwind has never costed a build properly, which is
  exactly the situation `cost-model-notes.md` addresses.

---

## Using it

Skills reference this fixture from their evals by path:

```yaml
fixture: context/fixtures/northwind-corp
```

The three `build-vs-buy` eval cases in
[`skills/technology/build-vs-buy/evals/`](../../../skills/technology/build-vs-buy/evals/)
run against it, and each names the rows it uses.

**Adding to the fixture:** extend it rather than reshaping it. Evals across skills depend
on these IDs and figures, so changing `nw-002`'s cost breaks somebody else's expected
result. New columns are cheap; changed values are not.
