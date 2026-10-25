---
name: review-the-numbers
description: Review an itinovo agency's figures for a month, a quarter or a year — sold, margin, collected, leads and conversion, destinations and operators, compared with the period before — with what clients still owe, what is due to suppliers and what is left to invoice. For the agency's administrators. Use when the user asks how the month or the quarter went, for the agency's numbers, or for a summary for the owner or the partners.
---

# Reviewing the agency's numbers

## Steps

1. **Settle the period**: the one the user asks for; by default the last full month. «This month» runs
   to today.
2. **Read the report** with `get_analytics` (`view: report`, `period`: month, quarter, year or custom
   with `from` and `to`; `anchor`: a day of a past month, quarter or year). It holds sold, margin,
   collected, conversion, destinations and operators against the period before, and as of today what
   clients owe by how late it is, what is due to suppliers and what is left to invoice.
3. **For the detail** of what is owed, `get_money` (`view: invoices`, `status: overdue`; `view:
   payment_requests`, `status: sent`, then `partially_paid`).
4. **Write the review** in a few lines:
   - what grew and what fell against the period before, with the figures;
   - where it comes from, as the data shows it: destinations, operators, conversion;
   - what is still to collect, the largest amounts first with how late they are, and what is due to
     suppliers;
   - two or three next steps: quotes to follow up (the `follow-up-open-quotes` skill), payments to chase
     and bookings to invoice from the app.
5. **On request**, a table for the partners, or the narrative summary with `get_analytics`
   (`view: executive_summary`, month, quarter or year).

## Rules

- The figures are itinovo's: never recompute margins or VAT of your own, and always say the period and
  the currency.
- Name the app's pages as the report says them, in the user's language.
- Analytics are for administrators: if itinovo refuses, say that an administrator can see them.
- Never request a payment or send a reminder from here: they leave from the itinovo app.
