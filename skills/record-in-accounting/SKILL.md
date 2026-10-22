---
name: record-in-accounting
description: Enter itinovo's invoices, credit notes, supplier invoices, payments and refunds of a period into the agency's accounting software (Xero, QuickBooks Online, Zoho Books…) through that software's own connector. Use when the user asks to record, post, sync or send the month's (or quarter's) invoices and payments to their accounting software or accountant.
---

# Recording a period in the accounting software

itinovo keeps the books booking by booking; the accounting software stays the agency's statutory
ledger. You carry the documents from one to the other: you never decide how they are taxed.

## Steps

1. **Ask what is needed**: which accounting software (its connector must be connected in Claude) and
   which period. Default: the last full month.
2. **Read the period** with `get_money` (view `accounting`, `dateFrom`, `dateTo`). It says how many
   documents and payments there are in all: read every page.
3. **Read what the accounting software already has** for the period, and leave out every document
   whose number is already there (the itinovo number is the reference): nothing is entered twice.
4. **Ask once for the mapping**, and never guess it: the sales account, the accounts for supplier
   costs, and the tax code for each VAT treatment the period has — margin scheme (TOMS in the UK: no
   VAT on the invoice), margin scheme zero-rated (travel outside the UK, or outside the EU), standard by
   rate, outside the scope. These are the accountant's choices: if the user does not know them, stop
   and suggest asking the accountant.
5. **Show the table** of what you will enter — number, date, party, total, currency, account, tax code —
   and the payments to match, then wait for the user's yes.
6. **Enter it** with the accounting software's connector:
   - client invoices and credit notes as sales invoices and credit notes, the credit note linked to the
     invoice it corrects (`correctedInvoice`);
   - supplier invoices as bills, in their own currency;
   - payments and refunds against their document, with date, method and reference. A deposit
     collected on a payment request (no invoice yet) goes in as a prepayment or deposit received, as
     the accountant prefers.
7. **Report** what was entered, what was left out because it was already there, and anything that
   failed, with the reason.

## Rules

- A margin-scheme document carries no VAT: the VAT is inside the margin and worked out for the period.
  For the margin VAT give the accountant the figures of `get_money` view `margin`: never post a VAT
  amount of your own.
- Keep the legal wording (`marginSchemeNotice`) on the sales invoice when the software has a field for it.
- Never reconcile the bank, file a VAT return or close a period: the accounting software and the
  accountant do that.
- Never change anything in itinovo from here: invoices, payments and refunds are recorded in the app.
