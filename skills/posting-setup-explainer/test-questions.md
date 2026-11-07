# Test questions: posting-setup-explainer

> **Draft: Nurlin to review.** Ask each question in a fresh chat with the skill
> installed. A good answer covers every "must cover" point.

### Q1. Revenue account for an item

> "In USMF, which account does item 1000 post its revenue to when we invoice a
> sales order? The item is in item group 'Audio'."

Must cover:
- Revenue comes from inventory posting, Sales order tab, posting type Revenue.
- Lookup order: a row for item 1000, then item group Audio, then All, combined
  with the customer, customer group or All.
- The same accounts can be seen on the item group.
- How to check: post in a sandbox and open the voucher, or look at an existing
  invoice voucher.

### Q2. Wrong expense account on a category purchase

> "A PO line with procurement category 'Office supplies' posted to the wrong
> expense account. Where does that account come from?"

Must cover:
- Purchase expenditure for expense, inventory posting > Purchase order tab,
  item code Category.
- A row for this category may be missing, so a broader row (All) was used.
  <!-- REVIEW: confirm whether rows for a parent category apply to child categories. -->
- The account can also be overridden on the line's accounting distribution.
- Fixing the setup only affects future invoices; the posted one needs a
  correction decided by the accountant.

### Q3. New vendor group

> "We're creating a new vendor group 'IC' for intercompany vendors. What posting
> setup do we need?"

Must cover:
- A vendor posting profile row for the group (summary account), or a dedicated
  profile.
- Check inventory posting rows that use vendor group.
- Intercompany accounting (due to / due from) if these vendors are other legal
  entities.
- Test one invoice in a sandbox.

### Q4. Where do dimensions come from?

> "Why did the vendor invoice get department 200 when I didn't enter it?"

Must cover:
- Default dimensions from the vendor, the order header or the item.
- A fixed dimension on the main account would override.
- How to check the vendor's and item's default dimensions.
