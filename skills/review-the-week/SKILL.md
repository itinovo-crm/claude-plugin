---
name: review-the-week
description: Review the agency's coming departures, deadlines and open tasks in itinovo, and what each sold trip still misses (supplier confirmations, vouchers, documents, payments). Use when the user asks what is coming up, who leaves soon, or what to do this week.
---

# Reviewing the week

## Steps

1. **Show the departures** with `show_departures` for the period asked (default: the next 7 days). Each
   card says what the trip still misses, as the itinovo Dashboard does.
2. **Add the day's work** with `get_overview` (`my_day`): tasks due, follow-ups, notifications.
3. **Summarise in a few lines**: what needs doing first and why (a departure in two days missing a
   confirmation comes before a task due next week).
4. **Offer the next step** for each gap, and wait for the user:
   - a supplier confirmation → `ask_suppliers` (it asks the user before sending anything);
   - a task to record → `save_task`;
   - a booking to look into → `get_lead`.

## Rules

- Never send anything to clients: documents, messages and payment requests leave from the itinovo app.
- Ask before writing to suppliers or changing a booking.
