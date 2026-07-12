---
name: business-outcome-research
description: Research and decide high-impact business, product, architecture, payment, compliance, marketplace, and operational questions by reconstructing the real business and code lifecycle, defining invariants, verifying current primary sources and eligibility, stress-testing failure paths, and producing one feasible evidence-backed recommendation. Use when a technically correct local answer could still create financial loss, compliance failure, broken refunds, unsafe state transitions, or an incomplete business outcome.
---

# Business Outcome Research

Turn a surface question into a verified end-to-end business decision. Treat documentation and APIs as evidence; treat preservation of the business invariants as the acceptance test.

The business owner defines product intent and authorized scope. Do not turn risk analysis into unrequested product control.

## Route References

- Read [references/business-analysis.md](references/business-analysis.md) for every material architecture, product, or operational decision.
- Also read [references/payment-risk.md](references/payment-risk.md) whenever money, settlement, refunds, merchant onboarding, credit, reserves, guarantees, or platform payment rules are involved.

## Workflow

### 1. Frame the real decision

- State the desired business outcome in one sentence.
- Separate the user's literal question from the underlying decision.
- Derive the conditions that must remain true. Treat these business invariants as acceptance criteria.
- Do not ask routine questions. Inspect the available business context, code, configuration, and prior decisions; state consequential assumptions and proceed.

### 2. Reconstruct the existing system

- Identify actors, assets, ownership, permissions, trust boundaries, and responsibility for loss.
- Trace the relevant code and data paths instead of reasoning from documentation alone.
- Build the lifecycle: state transitions, triggers, time windows, expiry, retries, reversals, and terminal states.
- For each critical state, identify who holds the money or data, who can move it, and what recourse remains.
- Trace all branches that can complete the workflow: customer actions, merchant/admin approval, workers, callbacks, scheduled jobs, manual operations, and UI/API contracts. Absence in one branch is not proof that the lifecycle is incomplete.

### 3. Research external constraints

- Use the Exa MCP when available for external research. Use current primary sources: official product documentation, platform rules, standards, law, source code, or original research.
- Research the whole capability family, not only the feature named in the question. Look for adjacent products, operating models, exceptions, presale or delayed flows, reserve or guarantee mechanisms, and qualification paths.
- Verify existence, applicability, eligibility, limits, time windows, automatic behavior, and failure behavior separately.
- Record source dates when rules may change. Distinguish verified facts, inferences, and unresolved facts.

### 4. Test end-to-end feasibility

- Compare every platform limit with the full business liability window.
- Treat a mismatch across individually valid components as a defect when it violates an explicit business invariant. A payment API may work correctly while its control window still makes the product unsafe to launch.
- Reject a capability that exists but is unavailable to the user, does not apply to the business category, expires too early, or leaves a critical loss unassigned.
- Trace cancellation, refund, dispute, reversal, insolvency, timeout, partial failure, duplicate event, stale state, and exhausted-balance paths.
- Run an adversarial scenario in which a counterparty scales abuse quickly, withdraws value, or stops cooperating.
- Label a control that only reduces risk as a mitigation, never as a complete solution.
- Classify each finding as `verified defect`, `verified external requirement`, `risk`, `product choice`, `optional improvement`, or `unresolved`.
- Call something a defect only when it violates an explicit requirement, invariant, test, security boundary, or authoritative external rule. Do not promote a design preference into a bug or severity label.
- Do not infer a missing workflow from the first route or service. Trace approval paths, workers, callbacks, and automatic completion branches before assigning severity.

### 5. Make one decision

- Recommend one feasible end-to-end course of action and show how it satisfies every critical invariant.
- Resolve conflicts between sources and explain the decisive tradeoff.
- If the current constraints make the outcome impossible, say `not feasible under the current constraints` and identify the minimum qualification, commercial, product, or architectural change required.
- Do not manufacture certainty, recommend an unavailable product, or provide a menu of disconnected features.
- Treat confirmed owner decisions as authoritative unless they conflict with a verified external rule, security boundary, or invariant. State any conflict precisely; do not silently replace the decision.
- If the user narrows the requested change, implement only that change and preserve all other behavior. A diagnosis or risk observation is not authorization to redesign the product.
- Recommend `no change` when the existing end-to-end flow already implements the intended policy.

## Change-Authorization Gate

Before proposing or making a change, answer:

1. What is the verified current behavior across every completion branch?
2. What explicit requirement says the current behavior is wrong?
3. Is the finding a defect, or only a different product choice?
4. Who authorized changing approval rights, financial rights, customer promises, or loss ownership?
5. What exact files and behavior are in scope, and what must remain unchanged?

If questions 2 or 4 have no evidence, do not implement the policy change. Report it as a risk or optional improvement.

## Hard Decision Gates

Do not approve a solution unless all applicable gates pass:

1. **Outcome:** It achieves the business result, not merely the local technical task.
2. **Lifecycle:** It remains valid through the longest refund, delivery, redemption, dispute, and liability window.
3. **Access:** The user can actually obtain the required product, permission, and qualification.
4. **Control:** The claimed control changes the real money, data, or authorization state—not only a label or order status.
5. **Failure:** The worst credible failure has an identified owner, funding source, recovery path, and operational response.
6. **Evidence:** Current authoritative evidence supports the material claims.
7. **Verification:** Repository behavior and external rules agree, or the conflict is explicitly resolved.
8. **Authority:** The change is within the user's scope and does not silently replace an intentional approval or policy decision.

## Response Contract

Lead with the decision. Then provide, in the smallest useful format:

1. underlying business outcome;
2. critical invariants;
3. verified current-state lifecycle;
4. decisive evidence with citations;
5. rejected options and the exact failed gate;
6. finding classification and evidence that any claimed defect violates an explicit requirement;
7. adversarial failure result;
8. authorized implementation or business change;
9. behavior that must remain unchanged;
10. residual risk and verification still required.

Do not end with an open-ended question. End with the concrete decision or completed result.
