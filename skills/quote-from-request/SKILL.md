---
name: quote-from-request
description: Turn a client's travel request (an email, a message, notes from a call) into a booking with a draft quote in itinovo, priced from the agency's own suppliers. Use when the user pastes or describes a request and wants a quote prepared.
---

# From a client's request to a draft quote

The agency works in itinovo: a **lead** (in Italian «pratica») holds the client's request, and its
**quote** holds the trip day by day, with services priced as the quote editor prices them.

## Steps

1. **Read the request** and list what it gives: client, dates (or month and length), number and ages of
   travellers, places, budget, wishes. Ask the user only for what blocks the quote (usually dates and
   number of travellers); everything else can be refined later.
2. **Find the client** with `search` (name, email). If found, use its ID; if not, `prepare_quote`
   creates it.
3. **Find the services among the agency's suppliers** before inventing any: `show_hotels` for hotels in
   a place (with dates, board and room), `list_suppliers` with `what: services` for transfers,
   excursions and the rest. Prefer what the agency already sells; say when a place has no supplier.
4. **Prepare the trip** with `prepare_quote` in one call: client, lead details, and the days, each with
   its place, a short text and its services (type, name, supplier, figures). The tool creates the lead
   and the draft quote, priced as the editor does.
5. **Show it** with `show_quote`, so the user sees the card and can open the itinerary full screen.
6. **Tell the user what is missing**: services without a supplier, prices to confirm, choices to make.

## Rules

- Never invent a price, a date or a supplier: leave out what the request and the agency's data do not say.
- Write the day texts in the client's language, in your own words.
- Nothing is sent to the client from Claude: the user reviews and sends the quote from the itinovo app.
