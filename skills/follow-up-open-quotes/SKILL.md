---
name: follow-up-open-quotes
description: Find the quotes in itinovo still waiting for an answer — sent and not answered, opened, with a change request, expired, or drafts left unsent — and propose the next step for each — a follow-up task with a short draft message, a new version, or the lead marked lost with its reason. Use when the user asks which quotes are waiting, whom to call back, or to tidy up the pipeline.
---

# Following up the quotes waiting for an answer

## Steps

1. **Read what is waiting**: `get_overview` (`view: follow_ups`, `scope: quotes`) gives the leads
   itinovo itself suggests following up, with how long they have been still. Then `list_quotes` with
   `status: sent`, `viewed`, `changes_requested` and `expired`, one call each, reading every page: each
   quote comes with the day it was sent and the day the client opened it.
2. **Read only what decides the next step**: `get_quote` (`include: ["messages"]`) for the client's last
   message, `get_lead` (`include: ["tasks"]`) for a follow-up already planned.
3. **Sort them**:
   - a change request → a new version, as the `revise-a-sent-quote` skill does;
   - opened, no answer → a follow-up now;
   - sent, never opened → a follow-up by phone: the email may not have reached the client;
   - expired → a follow-up with a new version, or the lead lost;
   - a draft never sent, or a trip whose dates have passed → the user finishes and sends it from the
     app, or the lead is lost;
   - a follow-up task already open → leave it, and say so.
4. **Show a short table** — client, trip, sent on, days waiting, opened or not, proposed step — and wait
   for the user to choose.
5. **Do what the user chose**:
   - a follow-up with `save_task` (`leadId`, `title`, `dueDate`, `priority`), with a short draft message
     in the client's language in `description`, for the user to send from itinovo or to say on the phone;
   - a lead lost with `set_lead_state` (`action: lost`, `leadId`, `reason`, `note`, `closeTasks: true`),
     one lead at a time, each after the user's yes. The reason is the client's: `too_expensive`,
     `dates_not_flexible`, `chose_competitor`, `changed_plans`, `no_response` (only when the client never
     answered) or `other` with a note. `action: reactivate` brings a lead back.
6. **Report** what was planned, what was marked lost and what is left to the user.

## Rules

- Never send anything to the client: the draft message is for the user, who sends it from the itinovo app.
- Never mark a lead lost without the user's yes for that lead.
- Never add a second follow-up where one is already open.
