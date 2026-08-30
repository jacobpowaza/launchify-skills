# Payments and Business Logic

**Category ID:** `payments`

---

## Scope

Inspect all payment processing, billing, subscription, pricing, and business logic for abuse vectors and security controls.

---

## Checks

### Price and Payment Manipulation
- Price manipulation
- Coupon abuse
- Refund abuse
- Subscription bypass
- Trial abuse
- Currency manipulation
- Currency and rounding bugs
- Negative quantity or amount abuse
- Integer overflow
- Decimal precision errors
- Currency conversion errors

### Webhook Security
- Payment webhook validation issues
- Unsigned webhooks
- Webhook replay
- Missing webhook signature verification
- Missing webhook timestamp validation
- Missing webhook idempotency

### Transaction Integrity
- Duplicate transaction handling failures
- Duplicate processing
- Race conditions
- Time-of-check/time-of-use bugs
- Concurrent redemption abuse
- Failed payment state confusion
- Partial payment handling failures
- Chargeback handling failures

### Business Logic
- Business logic abuse
- Workflow bypasses
- Client-controlled entitlement state
- Frontend-only payment checks
- Client-controlled prices, product identifiers, discounts, subscription status
- Missing server-side payment verification
- Missing payment event ordering
- Missing refund authorization
- Refund to unauthorized destination
- Trial reset abuse
- Coupon stacking abuse
- Account sharing abuse
- Entitlement caching errors

### Audit and Monitoring
- Missing payment audit logs
- Missing payment reconciliation
- Missing financial alerts
- Missing manual review for high-risk actions

---

## Methodology

1. Trace the complete payment flow from frontend to backend to payment provider
2. Verify prices, products, and discounts are determined server-side
3. Test for price manipulation through client-side modifications
4. Test webhook signature verification and replay protection
5. Test for duplicate transaction handling
6. Test for race conditions in payment processing
7. Verify subscription and entitlement enforcement is server-side
8. Test trial and coupon abuse vectors
9. Verify refund authorization and audit logging
10. Check for financial reconciliation and alerting

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Client-controlled price in payment flow | CRITICAL |
| Unsigned payment webhooks | CRITICAL |
| Missing webhook replay protection | HIGH |
| Subscription bypass through client manipulation | HIGH |
| Race condition allowing duplicate redemption | HIGH |
| Missing payment audit logs | MEDIUM |

---

## Evidence Requirements

- Payment provider and integration type
- Specific payment flow or endpoint affected
- Whether server-side validation is enforced
- Whether webhooks are properly validated
- Financial impact of the finding
