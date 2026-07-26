---
name: Cancel a Despegar reservation (after-sales)
description: Check cancellation allowance, quote the refund, and cancel an existing Despegar reservation through the after-sales flow.
api: https://api.despegar.com/v3
docs: https://api-docs.despegar.com/docs/aftersales
method: generated
operations:
  - getReservationStatus
  - getCancelAllowance
  - createCancelQuote
  - cancelReservation
---

# Cancel a reservation (Despegar after-sales)

Authenticate with the partner **API key** header for the correct environment.

## Steps

1. **Status** — `getReservationStatus`: confirm the reservation exists and is in
   a cancellable state.
2. **Allowance** — `getCancelAllowance`: check whether cancellation is permitted
   and under what conditions.
3. **Quote** — `createCancelQuote`: get the refund/penalty breakdown for the
   cancellation before committing.
4. **Cancel** — `cancelReservation`: execute the cancellation once the quote is
   accepted.

## Rules

- Always show the `createCancelQuote` refund/penalty amounts to the customer and
  get explicit confirmation before calling `cancelReservation`.
- Refund outcomes arrive asynchronously via the Communication (webhook) events
  (`Refund Confirmation`, `Refund Information`, `Refund rejected chargeback`) —
  do not assume the refund is settled at cancel time.
