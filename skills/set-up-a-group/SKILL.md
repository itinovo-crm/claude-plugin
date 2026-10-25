---
name: set-up-a-group
description: Set up a group trip in itinovo from what the organiser sends — a participant list (a spreadsheet, a CSV, a pasted list) with classes, teams or service levels, and for meetings and events the programme of sessions — as a group lead with its sub-groups, travellers and sessions. Use when the user shares a group's participant list or an event's programme to load.
---

# Setting up a group

## Steps

1. **Find the group's lead** with `search`. If there is none, ask the user, then find or create the
   organiser with `search` and `save_client` (a school or a company: `clientType: company`,
   `companyName`), and create the lead with `create_lead`: `clientId`, `groupName`, `groupType`,
   `expectedPax` (10 or more), destination and dates.
2. **Make sure it has a quote** (`get_lead`, `include: ["details"]`): travellers belong to a quote. If it
   has none, `create_quote` (`leadId`, `from: empty`, the dates) or the `quote-from-request` skill.
3. **Read the list** and keep, for each participant, first name, last name, date of birth (YYYY-MM-DD) and
   email, and the sub-group the file gives (class, team, role, service level). Write names with capitals
   as names are written. Say which rows have no last name or appear twice.
4. **Create the sub-groups** the list has with `save_group` (`what: sub_group`, `leadId`, `name`, and
   `serviceLevel` when the file says standard, premium or VIP). Keep the id each call returns.
5. **Load the travellers** with `save_travellers` (`quoteId`, `travelers`, each with its `subGroupId`),
   at most 50 per call. First read who is already there (`get_quote`, `include: ["travellers"]`) and leave
   them out: same name and date of birth is the same person.
6. **For a meeting, incentive, conference or other event**, add the programme with
   `edit_quote_settings` (`action: add_sessions`, `quoteId`, `sessions`: name, type, date, start and end
   time, venue, room, capacity, setup, `allGroup: true` or the `subGroupIds` taking part,
   `visibleToClient`). Then read the programme's checks with `get_quote` (`include: ["editing"]`) — a
   room too small, a session before the group lands, a session with no cost — tell the user each one with
   its fix, and apply a fix (`action: update_session`) only when the user asks.
7. **Report**: travellers loaded per sub-group, rows left out and why, sessions added, checks still open.

## Rules

- Load only names, dates of birth and emails. Identity documents and health details (allergies, diets,
  medical needs) stay out: the participants give them in the app, through their own forms.
- Ask before creating a lead or a client.
- Group prices, free places and rooming are set in the app or on the user's explicit request.
