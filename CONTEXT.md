# Domain language

One name per concept. Use these terms in code, UI copy, emails and issues.

## Refunds

| Term                   | Meaning                                                                                                                                                                                                                          |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Refund**             | Money given back to a learner for a course purchase.                                                                                                                                                                             |
| **Refund request**     | What the learner submits from the course page, with a reason. A person reviews every refund request — nothing is refunded automatically. Stored in the `refunds` table.                                                          |
| **Refund status**      | `Refund requested`, `Refund approved` or `Refund declined` — the `RefundStatus` enum, shown to learners with these exact words.                                                                                                  |
| **Refund policy**      | The 14-day refund policy.                                                                                                                                                                                                        |
| **Refund eligibility** | Whether a purchase can get a refund request. All must hold: within 14 calendar days of purchase; under 2 hours watched; under 50% of lessons completed; not a claimed team seat; no refund request already open on the purchase. |
| **Refund amount**      | What the learner actually paid for that purchase (`purchases.amountPaid`).                                                                                                                                                       |

### Avoid

| Word                  | Why                                                                                                                      |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------ |
| Cancel / Cancellation | Suggests ending a subscription, and something instant. Cadence sells one-off purchases and refunds are reviewed by hand. |
| Reversal              | A payments operation, not something a learner asks for.                                                                  |
| Chargeback            | A dispute the cardholder files with their bank — the opposite of a refund we grant. Never use it for a refund.           |
| Pending               | Use the refund status: "Refund requested".                                                                               |

### Known inconsistencies

The code does not match the definitions above yet (tracked in #1):

- Refund eligibility is checked twice — `getRefundEligibility` in `app/routes/courses.$slug.tsx` and the action in `app/routes/courses.$slug.refund.ts` — and the action skips the 50% completion rule.
- The refund amount shown in the form and email is the course's current list price unless the purchase had a PPP discount, instead of `purchases.amountPaid`.
