# Business Analysis Reference

Use this reference to turn a narrow request into an accountable business decision.

## 1. Decision frame

Write these fields before evaluating solutions:

| Field | Required content |
| --- | --- |
| Surface request | What the user literally asked for |
| Real decision | The decision that changes the business outcome |
| Desired outcome | Observable end state |
| Scope | Systems, actors, markets, and time horizon |
| Assumptions | Only consequential assumptions |
| Invariants | Conditions that must never be violated |
| Owner decisions | Confirmed product choices and acceptable tradeoffs |
| Authorized change | Exact behavior and files permitted to change |
| Preserve | Behavior that must remain unchanged |

An invariant should be testable. Prefer “a refundable amount remains recoverable until the refund window closes” over “refunds should be safe.”

## 2. System reconstruction

Create a lifecycle table when three or more states are involved:

| State | Entry trigger | Owner/controller | Money or data state | Allowed transition | Timeout/automatic action | Failure responsibility |
| --- | --- | --- | --- | --- | --- | --- |

Inspect these evidence surfaces where available:

- business requirements and merchant/customer promises;
- current source code, database schema, jobs, callbacks, and authorization checks;
- production configuration and logs;
- external platform products, rules, notices, and qualification requirements;
- contracts, operational playbooks, reserves, guarantees, and manual recovery paths.

Do not infer the business lifecycle from one API definition.

Before declaring a missing workflow, search customer routes, merchant/admin routes, workers, callbacks, schedulers, UI actions, API contracts, and tests. A customer action may intentionally create a request that a merchant action later approves; the lack of automatic worker submission is not itself a broken loop.

## 3. Finding classification

Use exactly one primary label for each finding:

| Label | Evidence threshold |
| --- | --- |
| `verified defect` | Violates an explicit requirement, invariant, test, or intended end-to-end flow |
| `verified external requirement` | Current authoritative source imposes the behavior |
| `risk` | Credible failure exposure, but no authorized product decision yet |
| `product choice` | Multiple valid behaviors; owner intent decides |
| `optional improvement` | Improves usability or operations without fixing a violation |
| `unresolved` | Available evidence cannot distinguish the above |

Do not assign P0/P1 severity to `risk`, `product choice`, `optional improvement`, or `unresolved`. Cite the violated requirement beside every severity claim.

Perform a negative-evidence check: “Did I prove the flow is absent, or did I only fail to find it in the first file?”

A business-critical defect may exist between components even when each component works as documented. Compare the customer promise with the longest control window. If the promise remains active after the platform control expires and no independent recovery source covers the gap, test that mismatch against the stated invariant and launch criteria. Do not wait for one API or test to fail before recognizing it.

## 4. Evidence ledger

For each material claim record:

| Claim | Status | Primary source | Date/version | Applicability | Consequence if wrong |
| --- | --- | --- | --- | --- | --- |

Use these statuses: `verified`, `inferred`, `unresolved`, `contradicted`.

Research adjacent solution families. A search for one interface often misses a different operating model that owns the real capability. Verify qualifications before treating an option as available.

## 5. Option matrix

Evaluate complete options rather than isolated features:

| Option | Invariants passed | Access/qualification | Lifecycle coverage | Worst-case loss | Operational burden | Decision |
| --- | --- | --- | --- | --- | --- | --- |

Reject an option on the first critical invariant it fails. Do not compensate for a hard failure by averaging unrelated benefits.

## 6. Adversarial validation

At minimum, test:

- a counterparty rapidly scales volume before detection;
- funds or data are moved at the earliest permitted time;
- the counterparty becomes insolvent or stops cooperating;
- a refund, reversal, or dispute arrives at the latest permitted time;
- callbacks are duplicated, reordered, delayed, or permanently missing;
- a partial operation succeeds and the retry runs against stale state;
- external rules or permissions differ from the assumed account model;
- manual operations are unavailable during peak load.

State the maximum credible exposure and who bears it. If that cannot be determined, the design is incomplete.

## 7. Change authorization

Before implementation, write:

```text
Current behavior:
Desired behavior:
Explicit requirement or owner decision:
Authorized scope:
Must preserve:
Approval/financial/customer-rights change: yes/no
```

When a user says “only fix X,” discard unrelated implementation ideas. Mention another issue only if the requested patch would make it unsafe or impossible to preserve.

## 8. Decision language

Use decisive labels:

- `feasible`: every critical invariant and access constraint passes;
- `feasible with required controls`: passes only after named controls are implemented;
- `mitigation only`: reduces likelihood or impact but does not guarantee the outcome;
- `not feasible under the current constraints`: at least one hard invariant or access gate fails.

Never turn “unknown” into “yes.” When a missing fact blocks safe approval, give the safest default decision and name the exact fact that would change it.
