---
name: prepare-travel-documents
description: Get the travel documents of the coming departures ready in itinovo — roadbook, vouchers, contract, and for groups the rooming list, the manifest and the delegates' agenda — after checking that each trip has what they need, without sending anything. Use when the user asks to prepare the documents for the week's departures or for one trip.
---

# Preparing the travel documents

## Steps

1. **Find the trips**: `show_departures` for the period asked (by default the next 7 days), or the trip
   the user names with `search`.
2. **Check each trip** with `get_lead` (`include: ["readiness", "documents"]`): what it still misses
   (supplier confirmations, travellers' names, payments) and which documents it already has.
3. **Show a table** — trip, departure, what is missing, documents already there — and say which documents
   would come out incomplete: a voucher without the supplier's confirmation code, a rooming list without
   rooms.
4. **Generate, after the user's yes**, with `generate_document` (`leadId`, `type`: `roadbook`,
   `voucher`, `contract`; for groups `rooming_list`, `group_manifest`, `delegate_agenda`). Vouchers are
   one per service the supplier has confirmed: `type: voucher` makes them all, `serviceId` only that one.
   Leave out the documents already there unless the user wants them made again.
5. **Report** what was generated — it is in the booking's Documents tab in itinovo — and what is still
   missing, with the next step (confirmations with the `confirm-with-suppliers` skill).

## Rules

- Nothing is sent to the client: the user sends the documents from the itinovo app.
- Never fill a gap with invented data: a missing confirmation code or room stays missing until it arrives.
