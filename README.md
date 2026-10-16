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

- Five skills (Markdown instructions) in `skills/`.
- `.mcp.json`, which points Claude to the itinovo connector at `https://api-crm.itinovo.com/mcp`. All
  data goes only between Claude and that server, under your itinovo sign-in.
- No scripts, hooks, commands or binaries.

## Links

- Guide: https://crm.itinovo.com/en-GB/features/claude/guide
- Privacy: https://crm.itinovo.com/en-GB/privacy
- Support: support@itinovo.com · Security: security@itinovo.com

Claude is a trademark of Anthropic, PBC. itinovo is not affiliated with Anthropic.
