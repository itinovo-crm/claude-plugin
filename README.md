# itinovo CRM for Claude

Skills that teach Claude how a travel agency, tour operator or DMC works in **itinovo**, the CRM for
travel businesses across Europe — bookings, day-by-day quotes, clients and travellers, suppliers and
their rates, confirmations and tasks. The plugin uses the **itinovo CRM connector**
(`https://api-crm.itinovo.com/mcp`), the same one listed in Claude's connectors directory.

## What it adds

| Skill | What Claude does |
|---|---|
| `quote-from-request` | Turns a client's email or message into a booking with a draft quote, priced from the agency's own suppliers, and shows it as a card |
| `load-supplier-price-list` | Loads a supplier's price list or contract (PDF, spreadsheet) as the supplier with its rates by season, room and board |
| `import-clients` | Imports a client list from a spreadsheet or another CRM, cleaning it and updating those already there |
| `review-the-week` | Shows the coming departures with what each still misses, the day's tasks, and proposes the next steps |
| `revise-a-sent-quote` | Prepares a new version of a quote after the client's change request, leaving the sent one untouched |
| `record-in-accounting` | Enters a period's invoices, credit notes, supplier invoices, payments and refunds into the agency's accounting software (Xero, QuickBooks Online, Zoho Books…), without doubles and only after the user's yes |
| `log-client-emails` | Records in a booking's Communications the emails exchanged with its client in Outlook or Gmail (found with the mailbox's own connector), only those the user chooses, with a short summary; nothing is sent |
| `follow-up-open-quotes` | Finds the quotes still waiting for the client's answer and proposes the next step for each: a follow-up task with a short draft message, a new version, or the lead marked lost with its reason, each after the user's yes |
| `confirm-with-suppliers` | Asks suppliers for the confirmations still missing (only after the user's yes) and records what a supplier confirmed — code, price, option, cancellation terms, payment dates — from the email or voucher the user shares |
| `offer-to-template` | Turns an offer the agency sold before, or a programme of a tour operator it works with, into a reusable template with the agency's own suppliers |
| `set-up-a-group` | Sets up a group from the organiser's participant list: the group lead, its sub-groups and travellers, and for events the programme of sessions with its checks |
| `review-the-numbers` | Reviews a month's, quarter's or year's figures against the period before, with what clients still owe and what is due to suppliers (administrators) |
| `prepare-travel-documents` | Checks the coming departures and generates their roadbook, vouchers, contract and group documents in itinovo, without sending anything |

## Requirements

- An itinovo account (30-day free trial or paid plan) with Claude enabled for the agency by its owner or
  an administrator in **Settings → Integrations → Claude**, and **Continue with Claude** pressed by each
  member.
- On the first use Claude asks you to sign in with your itinovo account (OAuth). Claude then acts with
  your role and permissions in itinovo.

## What it never does

Claude does not send quotes, documents or messages to clients, take or request payments, issue
invoices or change the agency's settings: those stay in the itinovo app. Identity documents and health
details never leave itinovo. Every action is recorded in the agency's AI Log.

## What the plugin contains, runs and sends

- Thirteen skills (Markdown instructions) in `skills/`.
- `.mcp.json`, which points Claude to the itinovo connector at `https://api-crm.itinovo.com/mcp`. All
  data goes only between Claude and that server, under your itinovo sign-in. `record-in-accounting`
  also writes to your accounting software, and `log-client-emails` reads your mailbox, each through that
  software's own connector, which you connect in Claude yourself: the plugin does not include them.
- No scripts, hooks, commands or binaries.

## Links

- Guide: https://crm.itinovo.com/en-GB/features/claude/guide
- Privacy: https://crm.itinovo.com/en-GB/privacy
- Support: support@itinovo.com · Security: security@itinovo.com

Claude is a trademark of Anthropic, PBC. itinovo is not affiliated with Anthropic.
