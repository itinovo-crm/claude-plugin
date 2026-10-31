---
name: log-client-emails
description: Record in an itinovo booking the emails exchanged with its client in Outlook, Gmail or another mailbox, found with that mailbox's own connector, so the booking's Communications tab holds the whole history. Use when the user asks to log, file, attach or save a client's emails to a booking, or to bring the history of a client's emails into itinovo.
---

# Recording a client's emails on a booking

## Steps

1. **Find the booking** with `search` (the client's name, the destination) and read it with `get_lead`
   (`include: ["details", "communications"]`): the client's email address, and what the timeline already has.
2. **Find the emails** with the mailbox's connector (Microsoft 365, Gmail…): those to and from the client's
   address in the period asked (default: the last 7 days).
3. **Show the list** — date and time, received or sent, subject — marking those already in the booking's
   communications, and wait for the user to choose.
4. **Record each chosen email** with `log_email`: `direction` (`inbound` from the client, `outbound` to the
   client), `sentAt` with its time, `from`, `to`, `subject`, `text` and `mailbox` (Outlook, Gmail…).
   The `text` is the email's whole text, as written: the message itself, without the earlier emails it
   quotes. If the client has no booking, record it on the client with `clientId` instead of `leadId`.
5. **Report** what was recorded and what was already there.

## Rules

- Nothing is ever sent from here: `log_email` only records.
- Record only emails with the booking's client, or about the booking, and only those the user chose.
- Never copy a payment card's number into the text: write that the email has one.
- The same email (same minute, sender and subject) is never recorded twice: itinovo answers that it is already there.
