---
name: Search and book a hotel with the Despegar B2B API
description: Search hotel availability, prebook a rate, resolve payment options, and confirm a hotel booking against the Despegar B2B API.
api: https://api.despegar.com/v3
docs: https://api-docs.despegar.com/docs/hotels
method: generated
operations:
  - searchAvailability
  - getHotelAvailability
  - createPrebook
  - getPaymentOptions
  - createBooking
  - getReservation
---

# Search and book a hotel (Despegar B2B)

Use the partner **API key** in the request header (test key against
`https://apis-uat.despegar.com/v3`, production key against
`https://api.despegar.com/v3`). Keys are environment-specific.

## Steps

1. **Search availability** — `searchAvailability`: search hotels for a
   destination and stay dates to get a list of available properties/rates.
2. **Get live detail** — `getHotelAvailability`: fetch live availability for the
   chosen hotel to confirm the rate is still bookable.
3. **Prebook** — `createPrebook`: lock the selected rate. The response returns a
   `prebook_id` and an `extended_info` block (exchange/cancellation policies,
   important data, hints) — surface mandatory hints to the traveler.
4. **Payment options** — `getPaymentOptions`: retrieve accepted payment methods
   for the `prebook_id`.
5. **Book** — `createBooking`: confirm the booking using the `prebook_id` and the
   selected payment option.
6. **Confirm** — `getReservation`: read back the reservation to confirm status.

## Rules

- Carry the `prebook_id` forward from step 3 into steps 4-6; do not re-search.
- Honor and display exchange/cancellation policies from `extended_info` before
  booking.
- No idempotency-key contract is documented — do not blindly retry
  `createBooking`; on an ambiguous failure, reconcile with `getReservation`
  before retrying.
