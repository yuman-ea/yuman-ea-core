# Eval cases — application-rationalization

These cases test the failures most likely to make portfolio rationalization unsafe:

| Case | Failure it catches |
|---|---|
| `01-incomplete-data-screening` | Inventing business, cost, dependency, or risk facts when the inventory is sparse |
| `02-validated-duplicate-with-modernization` | Collapsing every low score into retirement instead of distinguishing consolidate and modernize patterns |
| `03-retention-and-dependency-block-retirement` | Retiring a low-value application despite a policy or dependency blocker |
| `04-semantic-overlap-is-not-proof` | Treating AI-inferred similarity as validated duplication |

Expected outputs assert on dispositions, confidence, assumptions, and safety behaviour rather than exact numeric scores.
