---
name: offer-to-template
description: Turn an offer the agency sold before (a quote in Word or PDF, an old programme) or the programme of a tour operator it works with into a reusable itinovo template, day by day with its services from the agency's suppliers. Use when the user wants to bring past offers or programmes into itinovo to reuse them, for example after moving from another system.
---

# From an old offer to a template

In itinovo a **template** is a trip ready to reuse: its days with their texts and services. A new quote
starts from it with `create_quote` (`from: template`). A template is saved from a quote, so you build the
quote first on a working lead, save it, and then remove the working lead.

## Steps

1. **Read the whole source** and list: the trip's name and length, each day with its place and text, the
   services of each day (hotel with room and board, transfers, excursions, guides…), what is included and
   excluded, the prices and what they refer to (per person, per room, total).
2. **Find each service among the agency's suppliers**: `show_hotels` for hotels, `list_suppliers`
   (`what: services`, `query`: the service or its place) for the rest. For a tour operator's programme, the tour operator is the supplier.
   Say which services have no supplier: they go in without one, and the user can add it later.
3. **Tell the user what you will do** — a working lead named after the template, removed at the end — and
   wait for the yes.
4. **Build the quote** with `prepare_quote`: as client, the agency itself (`firstName: "Template"`,
   `lastName`: the template's name), no dates unless the programme has fixed ones, the days with their
   texts in your own words and their services with the figures the source gives.
5. **Show it** with `show_quote` and fix what the user asks with `edit_quote_items` and `edit_quote_texts`.
6. **Save the template** with `save_as_template`: `clientName` and `destination` as written on the
   working lead (and its `leadId`), `name`, `category` (beach, mountain, city, tour, cruise, other) and a
   short `description`.
7. **Remove the working lead and its client** with `delete` (`what: lead`, then `what: client`), after the
   user's yes: the template keeps its own copy of the days and services.
8. **Report** the template's name, its days and services, and the services left without a supplier. The
   agency finds it among its templates (`get_agency_info`, `view: templates`).

## Rules

- Never invent a price, a supplier or a service the source does not have.
- Write the day texts in your own words; names, codes and prices go in as they are.
- Load only offers and programmes the agency has the right to use: its own, or those of the tour
  operators it works with.
