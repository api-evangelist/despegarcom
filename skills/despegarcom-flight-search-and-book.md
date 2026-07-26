---
name: Search and book a flight with the Despegar B2B API
description: Search flight availability, prebook a fare, resolve payment options, and issue a flight booking against the Despegar B2B API.
api: https://api.despegar.com/v3
docs: https://api-docs.despegar.com/docs/flight
method: generated
operations:
  - searchFlightsAvailability
  - createPrebook
  - getPaymentOptions
  - createBooking
  - getReservation
---

# Search and book a flight (Despegar B2B)

Authenticate with the partner **API key** header, matching the environment
(`apis-uat.despegar.com/v3` for test, `api.despegar.com/v3` for production).

## Steps

1. **Search** — `searchFlightsAvailability`: search flight itineraries for the
   requested origin/destination and dates.
2. **Prebook** — `createPrebook`: lock the selected itinerary/fare. Response
   carries a `prebook_id` plus `extended_info` (exchange policies, required
   documents such as visas/vaccinations, and mandatory hints).
3. **Payment options** — `getPaymentOptions`: list accepted payment methods for
   the `prebook_id`.
4. **Book / issue** — `createBooking`: confirm and issue the ticket using the
   `prebook_id`.
5. **Confirm** — `getReservation`: read the reservation status.

## Rules

- Present required-document and exchange-policy hints from `extended_info` to the
  traveler before issuing.
- Price-variation detection (`getPriceJump` / `recoveryBooking`) may interrupt the
  flow if the fare changed between prebook and book — accept or reject the new
  value explicitly rather than silently proceeding.
- On an ambiguous `createBooking` result, reconcile with `getReservation` before
  retrying (no documented idempotency key).
