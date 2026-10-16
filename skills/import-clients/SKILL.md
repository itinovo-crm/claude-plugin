---
name: import-clients
description: Import a list of clients into itinovo from a spreadsheet, a CSV or another CRM's export, cleaning names, countries and phone numbers and updating those already there instead of doubling them. Use when the user attaches a client list and wants it in itinovo.
---

# Importing clients

## Steps

1. **Read the file** and map its columns to itinovo's client fields: first and last name (or company
   name), email, phone, city, country, date of birth, language, notes, tags, companions.
2. **Clean, never invent**: split full names, write countries as the app expects (the tool accepts
   names in six languages and turns them into ISO codes), keep phone numbers with their prefix, drop
   empty rows. Leave out identity documents and health details.
3. **Import** with `import_clients`, at most the batch size the tool allows per call. The same person is
   found by email, phone or name and updated, not created twice.
4. **Report from the result card**: created, updated, left out and why (usually a row with no name),
   and the rows not reached in time, which go in another call.

## Rules

- Marketing consents are never set from Claude: they stay as the clients gave them.
- Import only clients the agency has the right to hold.
