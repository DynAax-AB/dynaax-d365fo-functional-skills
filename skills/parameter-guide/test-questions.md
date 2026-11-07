# Test questions: parameter-guide

> **Draft: Nurlin to review.** Ask each question in a fresh chat with the skill
> installed. A good answer covers every "must cover" point.

### Q1. Duplicate vendor invoice numbers

> "What does 'Check the invoice number used' on Accounts payable parameters do?
> We want to stop paying invoices twice."

Must cover:
- Controls whether F&O accepts an invoice number the same vendor already used.
- The options (accept, reject, reject within the fiscal year).
- Applies per legal entity.
- Rejecting is the usual choice to prevent double payment.
- Test in a sandbox first.

### Q2. Negative inventory

> "Can we just switch on physical negative inventory so the warehouse stops
> getting errors?"

Must cover:
- It's on the item model group and affects every item in that group.
- It hides the real problem (receipts posted late, wrong warehouse).
- Costing effects; hand over to the cost accountant before changing.
- Suggests fixing the process first.

### Q3. Continuous number sequence

> "Our auditor wants invoice numbers without gaps. Which setting is that?"

Must cover:
- The Continuous flag on the number sequence.
- It slows posting and can leave numbers in the status list after errors.
- Use it only for the sequences that need it.
- Check country rules with the finance lead.

### Q4. Change management on purchase orders

> "What happens if we turn on change management in Procurement and sourcing
> parameters?"

Must cover:
- Changed purchase orders must go through approval again.
- Needs a purchase order approval workflow set up.
- Think about open orders and train buyers.
- Sandbox test with a few real orders.

### Q5. Unknown field (hand-over test)

> "What does the field 'XYZ auto-sync mode' on AP parameters do?"

Must cover:
- Says it doesn't recognise this as a standard field.
- Suggests checking the field help text in F&O, and asking whether it comes
  from an add-on or customization.

Must not:
- Invent a meaning for the field.
