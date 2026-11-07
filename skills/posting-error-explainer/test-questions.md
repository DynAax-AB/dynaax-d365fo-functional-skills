# Test questions: posting-error-explainer

> **Draft: Nurlin to review.** Use these to check the skill before publishing.
> Ask each question in a fresh chat with the skill installed. A good answer
> covers every "must cover" point and none of the "must not" points.

### Q1. Missing inventory posting

> "Posting a vendor invoice for PO 00045 in USMF. Error: Account number for
> transaction type Purchase expenditure, un-invoiced does not exist."

Must cover:
- Explains in plain words that an account is missing in the posting setup.
- Points to Inventory management > Setup > Posting > Posting, Purchase order tab.
- Says to check the item's item group (or the item itself) and the vendor
  against the Table / Group / All rows.
- Asks or checks whether the item or item group is new.
- Says who usually adds the setup, and to post again afterwards.

Must not:
- Suggest posting without the account, or editing data in the database.

### Q2. Unbalanced general journal

> "General journal won't post: The transactions on voucher GJ-001234 do not
> balance as per 31/10/2026."

Must cover:
- Debits and credits for that voucher don't add up.
- Check the lines on that voucher: amounts, signs, dates, currency.
- Mentions the journal name's voucher setting if several entries share one
  voucher.
- Mentions intercompany if lines are for more than one legal entity.

### Q3. Closed period at year start

> "Can't post anything dated 2 January 2027. It says the period isn't open."

Must cover:
- Check the date first.
- General ledger > Calendars > Ledger calendars, status of the period and
  module access.
- The new fiscal year may not exist yet in the fiscal calendar.
- Opening periods is for the controller or finance lead.

### Q4. Suspended dimension value

> "Sales invoice error: Dimension value 'CC-410' for Cost center is suspended."

Must cover:
- The cost centre value is suspended (or outside its active dates) for this
  legal entity.
- Where to check the dimension value.
- Where the value came from (customer, item or order defaults) and to fix the
  default if it will keep happening.
- Either use a valid cost centre or ask the finance lead to reactivate it.

### Q5. Unknown message (hand-over test)

> "Error when posting: Object reference not set to an instance of an object.
> ZZ_InvoiceExtension.validate()."

Must cover:
- Says this looks like a customization or add-on, not standard setup.
- Hands over to the technical team with the full message, time and steps.

Must not:
- Invent a setup fix.
