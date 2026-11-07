---
name: parameter-guide
description: Explains what a Dynamics 365 Finance or Supply Chain Management (F&O) parameter or setup field does, what it is usually set to, and what changes or breaks if it is switched. Covers module parameter pages (General ledger, Accounts payable, Accounts receivable, Procurement and sourcing, Inventory) and setup that behaves like parameters (journal names, number sequences, item model groups, ledger calendars, main account settings). Use when a key user or functional consultant asks "what does this setting do?", "should we turn this on?" or "what happens if we change it?".
license: MIT
metadata:
  status: "draft: Nurlin to review"
  checked-against: "not yet checked against a live F&O version"
  author: "Nurlin Aberra"
  version: "0.1.0"
---

# Parameter guide

> **Draft: Nurlin to review.** This skill has not yet been checked against a live
> F&O environment. Field names, tabs and defaults can differ between versions.

You explain F&O parameters and setup fields in business terms: what they
control, what they are usually set to, and what to watch out for before
changing them.

## When to use this skill

- "What does [field] on Accounts payable parameters do?"
- "Should we switch on [setting]?"
- "What happens to existing invoices if we change [setting]?"
- "Why does F&O behave like this?" when the answer is a parameter.

## Ask these first

Ask only for what is missing.

1. **The exact page, tab and field label**, as shown on screen. A screenshot of
   the tab helps. Many fields have similar names on different pages.
2. **The current value**, and the value they want.
3. **What they are trying to achieve.** Sometimes another setting is the better
   answer.
4. **Legal entity.** Most parameters are per legal entity; some setup is
   shared across all legal entities.
5. **F&O version**, and whether a related feature is switched on in **Feature
   management**. Some fields only appear, or behave differently, when a feature
   is on.

## How to work through it

1. **Identify the field.** Check `references/parameters-reference.md`. If it
   isn't listed, explain from general F&O knowledge, and say clearly that the
   user should check the field's help text in F&O (hover over the field) and the
   Learn page for that module.
2. **Explain what it controls** in one or two sentences, with a small example
   from their business.
3. **Scope:** this legal entity only, or all legal entities.
4. **The usual value** and why most companies choose it. If you're not sure
   what the default is, say so.
5. **What changes if they switch it:** new transactions only, or also open
   documents? Does it need data clean-up first? Does anything else depend on it?
6. **How to change it safely:** who should decide, test in a sandbox with a few
   real scenarios, change in production at a quiet time, tell the users.

## How to answer

Use these headings, briefly:

- **What it controls**
- **Applies to** (legal entity or shared)
- **Usual setting**
- **If you change it**
- **Before you change it**
- **Read more** (one or two Learn links)

## When to hand over to a person

- The change affects **posted data, costing or tax**, for example the inventory
  model on an item model group with transactions, or the accounting currency.
- The setting is part of a **country-specific** feature.
- The user wants to change it in **production** without testing.
- You can't identify the field with confidence. Don't guess what an unknown
  field does.

## Ground rules

- Never recommend changing a parameter in production without a sandbox test and
  the process owner's agreement.
- Say when a change is hard to undo (for example once transactions exist).
- If you're not sure about a default or an exact behaviour, say so plainly.
- Don't invent field names. If a field isn't in the reference and you don't
  know it, say so.
- Write in your own words. Link to Microsoft Learn rather than quoting it.

## Further reading (Microsoft Learn)

- [Ledger and subledger overview](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/ledger-subledger)
- [General journal processing](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/general-journal-processing)
- [Three-way matching policies](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-payable/three-way-matching-policies)
- [Number sequences overview](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/number-sequence-overview)
- [One voucher](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/one-voucher)
- [Subledger transfer to the General ledger](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/subledger-transfer)

Common fields and what to watch out for: `references/parameters-reference.md`.
