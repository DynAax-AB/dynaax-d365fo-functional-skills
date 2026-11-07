# Posting error patterns: detailed checks

> **Draft: Nurlin to review.** Error wording varies by version and language.
> Match on meaning. Lines marked `REVIEW` (in the source) need checking.

Each section has: what the message means, what to check (in order), the fix,
and when to hand over.

---

## 1. "Account number for transaction type ... does not exist"

**Meaning.** F&O tried to find a ledger account for one posting type and found
none. The transaction type named in the message tells you which setup is
missing.

**Check, based on the transaction type in the message:**

| Transaction type in the message | Where the account comes from |
|---|---|
| Vendor balance | Vendor posting profile: Accounts payable > Setup > Vendor posting profiles. Find the profile used on the invoice or order, then a row whose account code (Table / Group / All) covers this vendor. |
| Customer balance | Customer posting profile: Accounts receivable > Setup > Customer posting profiles. Same idea. |
| Receipt, Issue, Purchase expenditure for product, Purchase expenditure un-invoiced, Product receipt, Revenue, Consumption, Packing slip, Discount | Inventory posting: Inventory management > Setup > Posting > Posting, on the Purchase order, Sales order or Inventory tab. Check the item code (Table = this item, Group = its item group, All) and the account code (customer or vendor). The same accounts also show on the item group (Inventory management > Setup > Inventory > Item groups). |
| Purchase expenditure for expense | A purchase line with a procurement category and no item. Inventory posting > Purchase order tab, with item code Category. |
| Sales tax payable, Sales tax receivable, Use tax | The ledger posting group on the sales tax code: Tax > Setup > Sales tax > Ledger posting groups. |
| Fixed asset transaction types (acquisition, depreciation, disposal) | Fixed asset posting profile: Fixed assets > Setup > Fixed asset posting profiles, for the book and posting layer. |
| Penny difference, rounding, cash discount, exchange gain or loss | General ledger > Posting setup > Accounts for automatic transactions, and the accounts for currency revaluation on the Ledger page (General ledger > Ledger setup > Ledger). |

<!-- REVIEW: confirm the menu path for Ledger posting groups (Tax > Setup > Sales tax > Ledger posting groups) in current versions. -->

**Typical story.** A new item group, vendor group or procurement category was
created and nobody added it to the posting setup. Or a new legal entity was set
up without copying the posting setup.

**Fix.** Add the missing row with the right account, in the right legal entity.
Usually the finance lead or a consultant does this. Then post again.

**Hand over** if the user can't tell which account should be used. That's an
accounting decision.

---

## 2. Dimension or account combination not valid

**Typical wording:** a value "is not valid for" a dimension, the combination "is
not allowed" for an account structure, a dimension value "is suspended" or
"is not active for the date", or the main account "does not allow manual entry".

**Check, in order:**

1. **The account structure** for that main account: General ledger > Chart of
   accounts > Structures > Configure account structures. Does it allow this
   combination of dimension values? Is a dimension required here that's empty
   on the line?
2. **Advanced rules** that add extra required dimensions for some accounts.
3. **The dimension value itself:** General ledger > Chart of accounts >
   Dimensions > Financial dimensions > Dimension values. Is it suspended? Are
   its active from / to dates outside the posting date? Is it blocked for this
   legal entity (legal entity overrides)?
4. **The main account:** General ledger > Chart of accounts > Accounts > Main
   accounts. Is it suspended, outside its active dates, or set to not allow
   manual entry? Does it have a fixed dimension value that clashes with the
   line?
5. **Where the line's dimensions came from:** the defaults on the customer,
   vendor, item, order header or journal. A wrong default on the master record
   causes the same error on every document.

**Fix.** Correct the dimension values on the line, or fix the default on the
master record. Changing an account structure or advanced rule is a design
decision for the finance lead.

**Hand over** if the account structure itself looks wrong, or the user wants
to relax the rules.

Learn: [Dimension data validation](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/financial-dimension-data-validation),
[Configure account structures](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/configure-account-structures),
[Create and assign advanced rule structures](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/tasks/create-assign-advanced-rule-structures),
[Default financial dimensions on financial journals](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/dimensions-default-values).

---

## 3. Period not open, on hold or closed

**Check, in order:**

1. **The posting date.** A typo in the year is common.
2. **The ledger calendar:** General ledger > Calendars > Ledger calendars.
   Select the fiscal year and look at the period for that date. Status must be
   Open.
3. **Module access** for that period. A period can be open for General ledger
   but closed for Accounts payable, Inventory and so on.
4. **Whether the period exists.** If the fiscal calendar doesn't have the next
   year yet, there's no period to post into. That's common in the first days of
   a new year.

**Fix.** If the date is right, the finance lead or controller opens the period
or the module access. Don't advise reopening a closed period without the
controller's agreement.

Learn: [Fiscal calendars, fiscal years, and periods](https://learn.microsoft.com/en-us/dynamics365/finance/budgeting/fiscal-calendars-fiscal-years-periods),
[Close the general ledger at period end](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/close-general-ledger-at-period-end).

---

## 4. "The transactions on voucher ... do not balance"

**Meaning.** For at least one voucher, debits and credits don't add up to zero,
in the accounting currency, the reporting currency, or both.

**Check, in order:**

1. **Group the journal lines by voucher** and add them up. Manual journals often
   have one line too many or a wrong sign.
2. **Dates.** Lines on the same voucher with different dates can make each date
   unbalanced.
3. **Currency.** Lines in a foreign currency can balance in transaction currency
   but not in accounting or reporting currency because of rounding or
   different exchange rates. The message often says which currency is out.
4. **Legal entities.** Lines for several legal entities on one voucher need
   intercompany accounting set up (see section 13).
5. **Balancing dimension.** If the ledger uses a balancing financial dimension,
   each value of that dimension must balance too.
6. **Journal name voucher setting.** "One voucher number only" puts all lines
   on one voucher. Lines meant to be separate entries then must balance
   together.

**Fix.** Correct the lines. For rounding differences in reporting currency,
check the penny difference account in Accounts for automatic transactions.

Learn: [Journal posting failure due to imbalance](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/posting-fail-imbalance),
[How do I set up balancing financial dimensions?](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/set-up-balance-dimensions).

---

## 5. Vendor invoice: matching, price or quantity

**Check, in order:**

1. **Matching details** on the vendor invoice (Review > Matching details).
   Which line, which check (price, quantity, totals), and by how much?
2. **Policy:** Accounts payable > Setup > Accounts payable parameters >
   Invoice validation. With "Post invoice with discrepancies" set to require
   approval, an invoice outside tolerance can't post until someone approves
   the discrepancy.
3. **Quantity.** Is the invoiced quantity more than the received quantity? Post
   the product receipt first, or invoice the received quantity only.
4. **Price.** Did the purchase order price change, or is the vendor's price
   wrong? Price tolerances are set per legal entity, vendor or item.
5. **Duplicate invoice number.** Accounts payable parameters can reject an
   invoice number the vendor already used.

<!-- REVIEW: confirm "Review > Matching details" and the price tolerance menu path in current versions. -->

**Fix.** Correct the invoice, post the missing product receipt, or have the
right person approve the discrepancy. Don't change the tolerance to make one
invoice pass.

Learn: [Accounts payable invoice matching](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-payable/accounts-payable-invoice-matching),
[Three-way matching policies](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-payable/three-way-matching-policies).

---

## 6. Number sequences and duplicate vouchers

**Check, in order:**

1. **Not set up.** The module's parameters page (for example Accounts payable
   parameters) > Number sequences tab. Is a sequence code filled in for that
   reference?
2. **Exhausted.** Organization administration > Number sequences > Number
   sequences. Has the sequence reached its largest value?
3. **Continuous sequence problems.** A continuous sequence keeps a status list
   of numbers in use. Numbers left behind by failed postings can block it.
   A system administrator cleans it up.
4. **"Voucher already used."** A voucher number used before on another date.
   Check how the journal name assigns vouchers, and the duplicate-voucher
   check in General ledger parameters.

**Fix.** Normally a system administrator or consultant. Increasing the
largest value or adding a sequence is low risk; changing a sequence that's in
use needs care.

Learn: [Number sequences overview](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/number-sequence-overview).

---

## 7. Sales tax

**Check, in order:**

1. **Settlement period:** Tax > Indirect taxes > Sales tax > Sales tax
   settlement periods. Every sales tax code belongs to a settlement period, and
   that period needs a period interval covering the posting date. A new year
   often needs new intervals.
2. **Ledger posting group** on the sales tax code has all the accounts it
   needs (see section 1).
3. **Tax not calculated at all.** That's not an error message but a common
   question. The sales tax group (from customer, vendor or address) and item
   sales tax group (from item or category) must share at least one tax code.

**Hand over** questions about which tax rate or code is legally right.

Learn: [Set up sales tax settlement periods](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/tasks/set-up-sales-tax-settlement-periods),
[Set up ledger posting groups for sales tax](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/tasks/set-up-ledger-posting-groups-sales-tax),
[Tax isn't calculated or the tax amount is zero](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/sales-tax-troubleshooting-tax-not-calculated-amount-zero).

---

## 8. Holds, credit limits and approvals

1. **Vendor on hold:** the vendor record has a hold setting (for example for
   invoices, payments or all). Someone in AP sets or clears it.
2. **Customer on hold:** the customer record has an invoicing and delivery hold.
3. **Credit limit:** with credit management, a sales order can go on credit
   hold. Someone with credit rights releases it.
4. **Workflow:** a journal or vendor invoice under workflow must be submitted
   and approved before posting. Check the workflow history. If it's stuck,
   check that the workflow batch jobs are running.

Learn: [Credit holds for sales orders](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-receivable/cm-sales-order-credit-holds),
[Workflow system overview](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/overview-workflow-system).

---

## 9. Not enough inventory

1. **On-hand in the right place.** Check on-hand for the exact site, warehouse,
   location, batch and serial on the line. Stock in a different warehouse doesn't count.
2. **Reservations.** The stock may be reserved for other orders.
3. **Item model group:** Inventory management > Setup > Inventory > Item model
   groups. If physical negative inventory isn't allowed, F&O blocks issues
   beyond on-hand.
4. **Inventory close.** Posting into a period that's already been closed for
   inventory is blocked. Use a date after the last close.
   <!-- REVIEW: confirm wording and behaviour for posting before the last inventory close date. -->

**Fix.** Post the missing receipt or transfer first. Don't switch on negative
inventory to get one document through: it changes costing for every item in
that model group.

Learn: [Inventory close](https://learn.microsoft.com/en-us/dynamics365/supply-chain/cost-management/inventory-close).

---

## 10. Exchange rate missing

The ledger uses an exchange rate type (General ledger > Ledger setup > Ledger).
That type needs a rate for the currency pair on or before the posting date:
General ledger > Currencies > Currency exchange rates. Some journals or modules
use their own rate type, so check which one applies.

Learn: [Import currency exchange rates](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/import-currency-exchange-rates).

---

## 11. Budget control

Budget control can block a document when not enough budget remains for the
dimensions on the line. Check the budget check result on the document, then the
budget control configuration. Overruns are a business decision for the budget
owner.

Learn: [Budget control overview](https://learn.microsoft.com/en-us/dynamics365/finance/budgeting/budget-control-overview-configuration).

---

## 12. Not allowed to post

1. **Posting restrictions** on the journal name can limit posting to certain
   users or user groups (General ledger > Journal setup > Journal names >
   Posting restrictions).
2. **Security roles.** The user may be able to create the journal but not post
   it. The security admin checks the role.

<!-- REVIEW: confirm the button name for posting restrictions on Journal names. -->

---

## 13. Intercompany

A journal or document that hits two legal entities needs due-to and due-from
accounts for that pair: General ledger > Posting setup > Intercompany
accounting. For intercompany orders, the customer and vendor that represent
each company also need their intercompany setup.

Learn: [Intercompany accounting setup](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/intercompany-accounting-setup),
[Set up intercompany trade](https://learn.microsoft.com/en-us/dynamics365/supply-chain/sales-marketing/intercompany-trade-set-up).

---

## 14. "It posted, but it's not in the ledger"

1. **Subledger transfer.** Some documents post to a subledger first and move to
   the general ledger in a batch. Check General ledger > Ledger setup > Batch
   transfer rules for that document type.
2. **Posting in batch.** If the user posted in batch, the error went to the
   batch job log, not the screen. Check the batch job history.

Learn: [Subledger transfer to the General ledger](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/subledger-transfer).

---

## 15. Technical or unknown messages

If the message mentions class names, table names, "stack trace", unknown
fields or labels like `@XYZ123`, or anything that isn't standard F&O wording,
it is probably from a customization or an ISV add-on. Don't guess. Ask the
user to send the full message, the time it happened and the steps to repeat it
to their technical team or partner.
