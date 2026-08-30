# Payments and Business Logic

**Category ID:** `payments`

---

## Scope

Inspect all payment processing, billing, subscription, pricing, coupon management, refund workflows, and business logic for abuse vectors and security controls. Payment vulnerabilities directly cause financial loss.

---

## Checks

### Price and Payment Manipulation
- Price manipulation (client sends different price than server-side)
- Client-controlled product price in request body
- Client-controlled discount amount
- Client-controlled coupon code validation
- Client-controlled shipping cost
- Client-controlled tax amount
- Client-controlled currency
- Negative quantity abuse
- Negative price abuse
- Zero-price abuse
- Integer overflow in price calculations
- Decimal precision errors (floating point in money)
- Currency conversion errors
- Rounding errors in multi-step calculations
- Price race conditions (price changes between cart and checkout)

### Coupon and Discount Abuse
- Coupon reuse (single-use coupon used multiple times)
- Coupon stacking abuse (combining incompatible coupons)
- Coupon code brute-forcing
- Coupon generation through predictable patterns
- Coupon not invalidated after use
- Coupon validation client-side only
- Coupon abuse through concurrent requests
- Coupon abuse through account switching
- Discount abuse through referral manipulation
- Loyalty points abuse

### Subscription and Trial Abuse
- Subscription bypass (client sets subscription status)
- Trial abuse (creating multiple accounts for free trials)
- Trial reset abuse (resetting trial without legitimate flow)
- Subscription downgrade bypass
- Subscription cancellation bypass
- Entitlement caching errors (stale subscription status)
- Subscription status not validated server-side
- Account sharing abuse (multiple users on one subscription)
- Feature access bypassed through API

### Refund Abuse
- Refund abuse (requesting refunds for delivered goods/services)
- Duplicate refund requests
- Refund amount manipulation
- Refund to unauthorized destination
- Partial refund bypass
- Refund without order verification
- Refund race conditions (refund + usage simultaneously)
- Missing refund authorization

### Webhook Security
- Unsigned webhooks (no signature verification)
- Missing webhook signature verification
- Webhook replay attacks (replaying old webhook events)
- Missing webhook timestamp validation
- Missing webhook idempotency (duplicate processing)
- Webhook payload tampering
- Webhook delivered over HTTP instead of HTTPS
- Webhook endpoint not validating source IP
- Webhook retry abuse
- Missing webhook event ordering

### Transaction Integrity
- Duplicate transaction handling failures
- Duplicate processing (same payment processed twice)
- Race conditions in payment flows
- Time-of-check/time-of-use bugs
- Concurrent redemption abuse (same coupon used in parallel)
- Failed payment state confusion
- Partial payment handling failures
- Chargeback handling failures
- Payment state machine manipulation
- Missing transaction idempotency

### Business Logic
- Workflow bypasses (skipping steps in multi-step flows)
- Step skipping (completing a flow without required intermediate steps)
- State machine manipulation (forcing invalid state transitions)
- Race conditions in business flows
- Missing server-side validation (client-side only checks)
- Missing abuse prevention controls
- Missing entitlement enforcement
- Entitlement bypass through API manipulation
- Entitlement bypass through concurrent requests
- Stale entitlement cache
- Missing entitlement revocation
- Client-controlled business logic state
- Missing payment event ordering
- Missing payment reconciliation

### Audit and Monitoring
- Missing payment audit logs
- Missing payment reconciliation
- Missing financial alerts (unusual transactions, large refunds)
- Missing manual review for high-risk actions
- Missing fraud detection
- Missing anomaly detection for payment patterns
- Missing chargeback monitoring

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
11. Test for concurrent request abuse
12. Verify idempotency on payment operations
13. Check for state machine manipulation
14. Test for amount manipulation in refund requests

---

## Severity Guide

| Finding | Typical Severity |
|---|---|
| Client-controlled price in payment flow | CRITICAL |
| Unsigned payment webhooks | CRITICAL |
| Missing webhook replay protection | HIGH |
| Subscription bypass through client manipulation | HIGH |
| Race condition allowing duplicate redemption | HIGH |
| Duplicate payment processing | HIGH |
| Coupon reuse | MEDIUM |
| Missing payment audit logs | MEDIUM |
| Missing fraud detection | MEDIUM |
| Trial abuse | MEDIUM |

---

## Evidence Requirements

- Payment provider and integration type
- Specific payment flow or endpoint affected
- Whether server-side validation is enforced
- Whether webhooks are properly validated
- Financial impact of the finding
- Whether the finding allows financial loss
