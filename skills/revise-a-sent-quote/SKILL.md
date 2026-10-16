---
name: revise-a-sent-quote
description: Prepare a new version of a quote the client already has in itinovo after a change request (other dates, another hotel, a different price), keeping what was sent untouched. Use when the user says the client asked for changes to a quote.
---

# Revising a quote after a change request

## What can change, and where

In itinovo a quote **sent to the client** keeps its money and contract as sent. Its texts can still be
edited, but **costs, prices and services change in a new version**, which the user then sends.

## Steps

1. **Find the quote** with `search` or `list_quotes`, and read it with `get_quote` (`include:
   ["summary", "messages"]`) to see the client's change request.
2. **Create the new version** with `create_quote` (`from: new_version`, `quoteId`).
3. **Read it for editing** with `get_quote` (`include: ["editing"]`): it gives the IDs of days and services.
4. **Apply the changes** with `edit_quote_items` (services, costs, markups, days) and
   `edit_quote_texts` (texts the client reads); look for another hotel with `show_hotels`.
5. **Mark the request handled** with `edit_quote_settings` (`action: change_request_handled`) and a note.
6. **Show the result** with `show_quote` and tell the user what changed in price and margin.

## Rules

- Never change the version the client already has: always work on the new draft.
- The user sends the new version from the itinovo app.
