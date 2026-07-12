# SWE-Skills-Bench evaluation

Evaluation date: 2026-07-12  
Dataset: `GeniusHTX/SWE-Skills-Bench` at commit `95b3ce519fcb58d0b19e90a5b6e5165211dc6dd1`  
Agent/model: Codex CLI 0.144.1 with GPT-5.5  
Conditions: no Skill, original Skill, revised Skill  
Budget: 1,800 seconds per trajectory

The task, repository commit, and official verifier were held constant within every comparison. Only Skill injection changed.

## Reproducible cells

| Official task | No Skill | Original | Revised | Result |
| --- | ---: | ---: | ---: | --- |
| `tdd-workflow/batch1` | 3/14 | 3/14 | 3/14 | zero lift |
| `xlsx/batch1` | 4/11 | 4/11 | 4/11 | zero lift |
| `risk-metrics-calculation/batch1` | 7/10 | 7/10 | 7/10 | zero lift |

All three conditions failed the task-level 100% acceptance threshold in every cell. Both task-resolution lift and aggregate subtest lift were therefore zero.

## Cost

Across the three reproducible cells:

| Condition | Tokens | Relative to no Skill |
| --- | ---: | ---: |
| No Skill | 254,960 | — |
| Original Skill | 303,035 | +18.9% |
| Revised Skill | 290,158 | +13.8% |

The revised Skill was cheaper than the original but did not improve correctness. This is negative evidence against forcing a business-decision Skill onto unrelated, fully specified coding tasks.

## Excluded cell and infrastructure findings

`turborepo/batch1` was excluded from Skill Lift. The official verifier searches recursively for the first `turbo.json`; on the pinned repository it selects the pre-existing root JSON5 file instead of the required `examples/cache-demo/turbo.json`, then parses it as strict JSON. Every condition is consequently fixed at 5/10. The revised Skill did finish within budget and its target project passed the configured build, while the other conditions timed out, but the broken verifier prevents an official success claim.

The published Python image also lacked `jdcal` and used Python 3.12 with an old openpyxl commit that imports removed `collections` aliases. A common evaluation image restored the declared dependency and compatibility behavior for all conditions; no task or verifier was modified. This reproduced the paper's 36.4% XLSX baseline.

## Limits

- One trial per cell is insufficient for a confidence interval.
- The benchmark measures software implementation, not business responsibility.
- The Skill was deliberately forced onto tasks outside its intended routing boundary.
- Extension batches could not run after the Codex workspace exhausted its credits; failed model startups were not scored.

Conclusion: this evaluation does not show that the revised Skill improves generic coding. It does show that irrelevant Skill injection consumes context and that benchmark infrastructure must be audited before scores are trusted.
