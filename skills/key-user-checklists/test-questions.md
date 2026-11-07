# Test questions: key-user-checklists

> **Draft: Nurlin to review.** Ask each question in a fresh chat with the skill
> installed. A good answer covers every "must cover" point.

### Q1. New legal entity for intercompany

> "We're adding a Danish company that will buy from our UK company. What are the
> steps?"

Must cover:
- Legal entity, ledger, calendar, number sequences, parameters, posting setup,
  tax, in that rough order.
- Intercompany accounting (due to / due from) for the pair.
- Intercompany customer and vendor relation in both companies.
- Shared setup (chart of accounts, dimensions, products) is reused, not recreated.
- Country tax questions go to the tax adviser.
- A sandbox test in both directions.

### Q2. Month-end

> "Give me a month-end checklist for AP and GL only. We don't use inventory."

Must cover:
- Leaves out inventory steps and says so.
- Cut-off, open journals, vendor invoices, accruals, bank, revaluation if
  foreign currency, sales tax, closing the period by module, trial balance.
- Mentions the Financial period close workspace.

### Q3. New fiscal year

> "It's December. What do we need to set up so we can post in January?"

Must cover:
- New fiscal year in the fiscal calendar, open ledger periods.
- New sales tax settlement period intervals.
- Number sequences that reset yearly.
- Year-end close is a separate step once the old year is final.

### Q4. Production change

> "We want to switch on three-way matching next week. What should we do first?"

Must cover:
- Sandbox test with real invoices, including open ones.
- Agreement from the AP process owner.
- Product receipts must be posted before invoicing.
- Tell AP users, check the first invoices after the change.
