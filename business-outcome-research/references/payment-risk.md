# Payment and Settlement Risk Reference

Read this reference for payment, marketplace, merchant, settlement, refund, reserve, guarantee, or regulated-money flows.

## Money lifecycle

Model each stage explicitly:

| Question | What to verify |
| --- | --- |
| Who paid? | Payer identity and authorization |
| Who received? | Legal and platform account owner |
| Where is the money? | Pending, frozen, available, settled, withdrawn, reserved, or returned |
| Who can move it? | Merchant, service provider, platform, payment provider, or bank |
| What releases it? | API instruction, delivery, confirmation, timeout, schedule, or manual review |
| What happens automatically? | Auto-settlement, auto-unfreeze, expiry, closure, or retry |
| How is a refund funded? | Frozen order funds, available balance, reserve, receiver clawback, or platform capital |
| What if the balance is empty? | Rejection, debt, guarantee claim, platform loss, or consumer loss |
| How long does liability last? | Refund, redemption, delivery, dispute, and statutory windows |
| Who bears a shortfall? | Contractual and operational loss owner |

## Do not conflate controls

Verify each mechanism independently:

- **Order reporting** communicates transaction or fulfillment state.
- **Presale handling** changes an allowed fulfillment promise or reporting path.
- **Delayed settlement** postpones availability under named triggers.
- **Profit sharing** allocates order proceeds and may introduce a product-specific frozen state.
- **Fund freezing** restricts movement for a defined account, amount, and period.
- **Reserve or guarantee** provides a separate loss-absorption source.
- **Refund recovery or reversal** attempts to recover money after allocation.

One mechanism does not imply another. A status such as `pending`, `unfulfilled`, `presale`, or `profit-sharing-enabled` is not proof of protected funds.

## Qualification and operating-model check

Identify the exact account model before proposing integration:

- direct merchant;
- ordinary service provider and sub-merchant;
- ecommerce or marketplace platform and second-level merchant;
- SaaS provider without control of merchant funds;
- regulated or licensed payment institution;
- another platform-specific model.

For every proposed product, verify application eligibility, required entity and industry qualifications, merchant migration constraints, supported transaction types, account ownership, and audit obligations.

## Time-axis check

Put the platform and business windows on one line:

```text
payment ─ platform control expiry ─ delivery/redemption ─ last refund/dispute date
```

If the platform control expires first, it does not satisfy the refund invariant. Treat later recovery from the merchant as credit risk, not as protected funds.

## Marketplace abuse test

Simulate this path with actual limits:

1. A merchant offers an unusually attractive price.
2. Sales volume grows faster than review or reserve adjustments.
3. Funds become available at the earliest platform-permitted time.
4. The merchant withdraws funds or becomes insolvent.
5. Refunds or disputes arrive near the end of the customer liability window.
6. Determine the exact funding source and maximum platform loss.

If no committed source covers the shortfall, the payment design is incomplete.

## WeChat-style voucher example

For a voucher valid longer than an ordinary profit-sharing freeze:

1. Verify the current ordinary service-provider freeze and automatic-release rules from official documentation.
2. Verify whether a platform/ecommerce product offers a longer control window and whether the operator qualifies for it.
3. Investigate order-management and presale functions separately; prove their applicability to the voucher transaction type and their effect on the real fund state.
4. Compare every verified window with voucher redemption and refund liability.
5. If the operator lacks the qualifying product and no independent lawful reserve or guarantee covers the gap, conclude that the native flow alone is not feasible.

Re-research all product limits and qualifications each time; do not rely on values embedded in an old answer.
