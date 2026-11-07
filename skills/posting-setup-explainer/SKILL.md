---
name: posting-setup-explainer
description: Explains, step by step, which ledger accounts a Dynamics 365 Finance or Supply Chain Management (F&O) document or journal posts to, and which setup decides it (posting profiles, inventory posting, item groups, ledger posting groups for tax, fixed asset posting profiles, financial dimension defaults). Use when a key user or functional consultant asks "which account does this post to?", "why did this hit account X?", "where does the revenue or COGS account come from?" or wants to check the posting setup before go-live.
license: MIT
metadata:
  status: "draft: Nurlin to review"
  checked-against: "not yet checked against a live F&O version"
  author: "Nurlin Aberra"
  version: "0.1.0"
---

# Posting setup explainer

> **Draft: Nurlin to review.** This skill has not yet been checked against a live
> F&O environment. Menu paths can differ between versions.

You explain how F&O decides which ledger accounts (and financial dimensions) a
document or journal posts to. The user either wants to predict the accounts
before posting, or to understand why a posted voucher used the accounts it did.

## When to use this skill

- "Which account does this item post to when we invoice it?"
- "Why did this vendor invoice go to account 600100 instead of 600200?"
- "Where does F&O get the COGS / revenue / accrual account from?"
- "We're adding a new item group / vendor group. What posting setup do we need?"
- Reviewing posting setup before go-live or before opening a new legal entity.

If the user has an actual error message, use the posting-error-explainer
skill instead, if it's installed.

## Ask these first

Ask only for what is missing.

1. **Legal entity.** Posting setup is per legal entity.
2. **The document or journal:** sales order invoice, free text invoice, purchase
   order invoice, vendor invoice journal, general journal, inventory journal,
   production order, fixed asset transaction, payment.
3. **What's on the line:** a stocked item, a non-stock item, a procurement
   category, a main account, a charge.
4. **The parties:** customer or vendor, and their group.
5. **Which amount** they care about: balance (customer or vendor), revenue,
   cost of goods sold, inventory, accrual, tax, discount, charges.
6. **F&O version**, if they know it.
7. For a posted document: the **voucher number**, so they can open the voucher
   and compare.

## How to work through it

1. **List the posting types the document creates.** A sales invoice for a
   stocked item, for example, creates customer balance, revenue, inventory issue,
   cost of goods sold and sales tax. `references/posting-map.md` has the
   common documents.
2. **For each posting type, name the setup that holds the account.** For
   example: customer posting profile for the balance, inventory posting for
   revenue and cost, ledger posting group for tax.
3. **Walk the lookup order.** F&O uses the most specific row it can find.
   - Posting profiles (customer, vendor): the profile on the document, or the
     default from the module parameters. Inside the profile, a row for this
     customer or vendor (Table) beats their group (Group), which beats All.
   - Inventory posting: a row for this item (Table) beats its item group
     (Group), which beats All. Within that, the customer or vendor follows the
     same Table / Group / All order.
     <!-- REVIEW: confirm the full precedence order (item relation first, then account relation). -->
4. **Check for overrides:** a posting profile chosen on the order header, a
   fixed offset account on the journal name, a main account with a fixed
   dimension value.
5. **Explain the financial dimensions**, if asked: they come from defaults on
   the customer, vendor, item, order and line, merged by F&O, and then checked
   against the account structure.
6. **Tell them how to see it in F&O**: open the voucher for a posted document,
   or the accounting distributions and subledger journal entries for a vendor
   invoice or free text invoice before posting.
7. **Give them a test.** For a setup change, post one document in a sandbox and
   check the voucher.

## How to answer

1. A short **table of posting types**, with the setup page and the row that
   applies to their case, and the account if they gave you enough to know it.
2. **The lookup order** in one or two sentences, using their item group,
   vendor or customer names.
3. **How to check it** in F&O (voucher, or distributions before posting).
4. Any **risks**: for example, changing inventory posting affects every future
   transaction for that item group, not just the one that went wrong.

## When to hand over to a person

- The user asks which account is **right** for a business case. That's a
  chart-of-accounts decision for the accountant or finance lead.
- Posted vouchers are wrong and need **correcting** or reversing.
- **Standard cost, production or project accounting** questions beyond the
  basics, and the user needs a firm answer for month-end.
- **Country-specific** postings (localizations, tax reporting).
- Customizations change the posting logic.

## Ground rules

- Never say a posting setup change is safe in production without a sandbox test.
- Remind the user that changes to posting setup affect only **future**
  transactions. Posted vouchers stay as they are.
- Don't invent account numbers. Use placeholders unless the user gave them.
- Write in your own words. Link to Microsoft Learn rather than quoting it.

## Further reading (Microsoft Learn)

- [Posting profiles overview](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/pstg-prfles-ovrvw)
- [Recommended practices for posting profiles](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/recommended-practices-pstg-prfles)
- [Inventory posting profiles](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/inventory-posting-profiles)
- [Sales order posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/sales-order-posting)
- [Purchase order posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/purchase-order-posting)
- [Accounts for automatic transactions](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/accounts-for-auto-transactions)
- [Financial dimensions and posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/default-dimensions)
- [Accounting distributions and subledger journal entries for vendor invoices](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-payable/accounting-distributions-subledger-journal-entries-vendor-invoices)

The common documents and their posting types: `references/posting-map.md`.
