---
name: confirm-with-suppliers
description: Ask suppliers to confirm the services of sold trips in itinovo, chase the answers still missing, and record what a supplier confirmed — code, price, option, cancellation terms, payment dates — from the email, voucher or PDF the user pastes or attaches. Use when the user asks which confirmations are missing, to request or chase them, or shares a supplier's confirmation.
---

# Supplier confirmations

## Asking for them

1. **See what is missing** with `list_confirmations`: `status: pending` (still to ask) and
   `status: requested` (asked, no answer yet), for the agency or for one trip (`leadId`).
2. **Put them on their trips**: `list_leads` (`stage: confirmed`, then `travelling`) gives each trip's
   client and departure. Leave out the trips already back.
3. **Show them by trip**, nearest departure first: supplier, service, status.
4. **Ask** with `ask_suppliers` after the user's yes, saying who will get an email: `leadId` for every
   pending confirmation of a trip, `all: true` for every pending one of the agency, or `confirmationId`
   with its `leadId` for a reminder. itinovo writes with the agency's own supplier email template.

## Recording a supplier's answer

1. **Read the answer** and list what it says: the confirmation code, the confirmed price, an option and
   until when it is held, the cancellation terms (free until, penalties from which date and how much,
   non-refundable), the deposit and balance with their due dates.
2. **Find the confirmation**: the trip with `search`, then `list_confirmations` (`leadId`), matching
   supplier and service.
3. **Show what you will record**, then record it with `update_confirmation` (`action: status`, `leadId`,
   `confirmationId`, `newStatus: confirmed` — or `option_held` with `optionExpiresAt` —,
   `confirmationCode`, `confirmedPrice`, `cancellation`, `paymentSchedule` or `paymentDueDate`, `notes`).
4. **Compare the price**: when the confirmed price differs from the cost in the quote, say by how much.
   On the user's yes, `update_confirmation` (`action: apply_prices`, `leadId`, `quoteId`) makes a new
   version of the quote with the confirmed prices.

## Rules

- `ask_suppliers` writes to people outside the agency: always the user's yes first.
- Record only what the supplier wrote: never invent a code, a price or a date. Without a code, record the
  rest without `newStatus` and say that the confirmation stays open until the code arrives.
- A confirmed service cannot go back to pending: check supplier and service before confirming.
- Mark a confirmation `paid` only when the user says the supplier has been paid.
- Nothing goes to the client from here.
