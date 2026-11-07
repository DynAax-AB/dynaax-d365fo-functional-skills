---
name: key-user-checklists
description: Produces short, ordered checklists with menu paths for common Dynamics 365 Finance or Supply Chain Management (F&O) key-user tasks, such as setting up a new legal entity (including intercompany), month-end close, opening a new fiscal year, onboarding a new vendor or customer, releasing a new stocked product, and preparing a setup change for production. Use when a key user or functional consultant asks "what are the steps to...", "what do we need to set up for...", or "what should we check before...".
license: MIT
metadata:
  status: "draft: Nurlin to review"
  checked-against: "not yet checked against a live F&O version"
  author: "Nurlin Aberra"
  version: "0.1.0"
---

# Key-user checklists

> **Draft: Nurlin to review.** This skill has not yet been checked against a live
> F&O environment. Menu paths can differ between versions.

You give key users a short checklist in the right order, with the menu path for
each step, so they can do the task or check that someone else did it.

## When to use this skill

- "Steps to set up a new legal entity for intercompany."
- "What do we need to do at month end?"
- "Checklist for opening the new fiscal year."
- "What must be set up before we can invoice a new vendor / customer / item?"
- "We want to change a parameter in production. What should we do first?"

## Ask these first

Ask only for what is missing.

1. **Legal entity or entities** involved.
2. **Modules in use** (only General ledger and AP/AR, or also inventory,
   production, projects, fixed assets).
3. **F&O version**, if they know it.
4. **Is there a template?** An existing legal entity, item or vendor to copy
   from. F&O can copy setup between legal entities.
5. **Who does what:** is the user doing the steps or checking a partner's work?

## How to work through it

1. Start from the matching checklist in `references/checklists.md`.
2. **Remove steps that don't apply** (for example inventory steps when they
   don't use inventory). Say which ones you removed.
3. **Keep the order.** Later steps depend on earlier ones (for example posting
   setup needs the chart of accounts, number sequences come before parameters).
4. For each step give: **what**, **where** (menu path), **done when** (how to
   check it), and **who** usually does it.
5. Mark steps that are **shared across legal entities** (chart of accounts,
   financial dimensions, product masters, global address book) so the user
   doesn't create duplicates.
6. End with a **test**: one real transaction end to end in a sandbox.

If no checklist matches, build one using the same format, keep it under 15
steps, and say it's built from general F&O knowledge and should be checked.

## How to answer

A numbered list. Each item: **step** — menu path — done when. Add the "who"
only when it isn't the user. Keep it short enough to print on one page. Offer
more detail for any step on request.

## When to hand over to a person

- The task involves **legal or tax registration** decisions.
- **Data migration**, opening balances or large imports.
- **Security roles** and segregation of duties.
- Anything that needs the **partner or Microsoft** (new environments, database
  copies, upgrades).

## Ground rules

- Every setup change goes to a sandbox first, then production with the owner's
  agreement.
- Don't invent menu paths. If unsure, name the page and suggest the navigation
  search.
- Keep checklists short. A 40-step list doesn't get used.
- Write in your own words. Link to Microsoft Learn rather than quoting it.

## Further reading (Microsoft Learn)

- [Create legal entities](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/tasks/create-legal-entity)
- [Set up intercompany trade](https://learn.microsoft.com/en-us/dynamics365/supply-chain/sales-marketing/intercompany-trade-set-up)
- [Intercompany accounting setup](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/intercompany-accounting-setup)
- [Financial period close workspace](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/financial-period-close-workspace)
- [Year-end close](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/year-end-close)
- [Set up number sequences using a wizard](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/tasks/set-up-number-sequences-wizard)

The checklists: `references/checklists.md`.
