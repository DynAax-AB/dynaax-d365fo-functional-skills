# Parameters reference

> **Draft: Nurlin to review.** Field labels follow the English UI of current
> versions. Tabs move between versions. Every row marked `REVIEW` (in the
> source) needs checking before publishing.

This is not a full list. It covers fields key users ask about often, and the
traps around them.

---

## General ledger

Page: General ledger > Ledger setup > General ledger parameters

| Field | What it controls | Watch out for |
|---|---|---|
| Check for voucher used | What happens when a voucher number has already been used: reject, warn or accept. | Accepting duplicates makes audit harder. Most companies reject or warn. <!-- REVIEW: confirm option names --> |
| Allow multiple transactions within one voucher | Whether one voucher may hold several customer or vendor transactions. | Microsoft discourages it, and some features need it off. Read the One voucher page first. |
| Number sequences tab | Sequences for journal batches, vouchers and other GL references. | A missing sequence here stops journals being created. |

Page: General ledger > Ledger setup > Ledger

| Field | What it controls | Watch out for |
|---|---|---|
| Accounting currency, reporting currency | The currencies the ledger keeps balances in. | Changing them once transactions exist is a project, not a setting. Hand over. |
| Exchange rate type | Which set of exchange rates the ledger uses. | Rates must exist for that type, or postings in foreign currency fail. |
| Balancing financial dimension | A dimension whose values must each balance on every voucher. | Turning it on affects every journal. Test intercompany and allocation journals. |
| Accounts for currency revaluation | Realized and unrealized gain and loss accounts. | Missing accounts make revaluation and settlement fail. |

Page: General ledger > Ledger setup > Batch transfer rules

| Field | What it controls | Watch out for |
|---|---|---|
| Transfer mode per document type | Whether subledger postings go to the general ledger at once, in the background, or in a scheduled batch. | With batch modes, users see a posted invoice before it reaches the ledger. Explain this before month-end. |

Page: General ledger > Calendars > Ledger calendars

| Field | What it controls | Watch out for |
|---|---|---|
| Period status | Open, On hold or Permanently closed. | Permanently closed can't be reopened. |
| Module access | Which modules can post in the period. | Lets finance close AP or inventory before GL. Users see "period not open" errors. |

Page: General ledger > Chart of accounts > Accounts > Main accounts

| Field | What it controls | Watch out for |
|---|---|---|
| Do not allow manual entry | Blocks the account in journals; only automatic postings can use it. | Good for control accounts (AP, AR, inventory). Users will see errors if they try. |
| Suspended, Active from / to | Stops new postings to the account. | Posting setup that still points to the account will fail. |
| Fixed value on a financial dimension | Forces one dimension value on every posting to this account. | Overrides defaults silently; users can be surprised. |

## Journal names

Page: General ledger > Journal setup > Journal names

| Field | What it controls | Watch out for |
|---|---|---|
| New voucher | One voucher per balanced set of lines ("in connection with balance"), one voucher for the whole journal, or manual. | "One voucher number only" makes all lines one entry; it must balance as a whole. |
| Approval workflow | Whether journals of this name must be approved before posting. | Needs a working GL journal workflow. |
| Fixed offset account | Forces the offset account. | Users can't change the offset on the line. |
| Amounts include sales tax | Whether amounts on lines are entered gross. | Wrong setting doubles or misses tax. |
| Private for user group | Only one user group sees these journals. | Others can't find or post them. |
| Posting restrictions | Limits who can post journals of this name. | Users get "not allowed to post" errors. <!-- REVIEW: confirm button location --> |

## Accounts payable

Page: Accounts payable > Setup > Accounts payable parameters

| Field | What it controls | Watch out for |
|---|---|---|
| Ledger and sales tax tab > Posting profile | The default vendor posting profile. | Changing it affects new documents only. |
| Invoice tab > Check the invoice number used | Accept or reject a vendor invoice number already used (optionally per fiscal year). | Accepting duplicates risks paying twice. <!-- REVIEW: confirm tab and option names --> |
| Invoice validation tab > Enable invoice matching validation, line matching policy | Whether F&O compares invoices with orders and receipts (two-way or three-way). | Three-way needs product receipts posted before invoicing. |
| Invoice validation tab > Post invoice with discrepancies | Allow with warning, or require approval of discrepancies. | Require approval blocks posting until someone approves. |
| Settlement tab > Automatic settlement | Settle payments against open invoices automatically. | Can settle against the wrong invoice if payments aren't marked. |

## Accounts receivable

Page: Accounts receivable > Setup > Accounts receivable parameters

| Field | What it controls | Watch out for |
|---|---|---|
| Ledger and sales tax tab > Posting profile | The default customer posting profile. | New documents only. |
| Settlement tab > Automatic settlement | Settle payments against open invoices automatically. | Same as AP. |
| Credit limit settings | When F&O checks the credit limit (balance only, or including open orders and packing slips). | Newer credit management features add their own rules and holds. <!-- REVIEW: confirm where these live when credit management is on --> |
| Post packing slip in ledger | Whether packing slips create ledger postings (accruals). | Needs inventory posting accounts for packing slip types. <!-- REVIEW: confirm which page holds this field in current versions --> |

## Procurement and sourcing

Page: Procurement and sourcing > Setup > Procurement and sourcing parameters

| Field | What it controls | Watch out for |
|---|---|---|
| Activate change management | Purchase orders need approval again after they change. | Needs a purchase order workflow. Switching it on affects open orders. |
| Post product receipt in ledger | Whether product receipts create accrual postings. | Needs accounts for Product receipt and Purchase expenditure un-invoiced. <!-- REVIEW: confirm which page holds this field in current versions --> |

## Inventory: item model groups

Page: Inventory management > Setup > Inventory > Item model groups

| Field | What it controls | Watch out for |
|---|---|---|
| Inventory model | FIFO, LIFO, weighted average, standard cost, moving average and others. | Changing it for items with transactions needs a costing plan. Hand over. |
| Stocked product | Whether F&O keeps on-hand for the item. | Non-stocked items don't post to inventory accounts. |
| Post physical inventory | Whether receipts and issues post to the ledger before invoicing. | Needs the physical posting accounts. |
| Post financial inventory | Whether invoices post inventory value. | Normally on for stocked items. |
| Physical negative inventory, Financial negative inventory | Whether on-hand can go below zero. | Allowing it hides process problems and affects costing. |

## Number sequences

Page: Organization administration > Number sequences > Number sequences

| Field | What it controls | Watch out for |
|---|---|---|
| Continuous | No gaps allowed in the numbers. | Slower, and failed postings can leave numbers in the status list. Use only where law or audit needs it. |
| Manual | Users type the number. | Risk of duplicates. |
| Smallest, Largest, Next | The range and next number. | When Next reaches Largest, the sequence is exhausted. |
| Scope (Shared, Legal entity and so on) | Whether one sequence serves all legal entities or one. | Changing scope on a sequence in use is risky. |

---

Learn:
[One voucher](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/one-voucher),
[Subledger transfer to the General ledger](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/subledger-transfer),
[Fiscal calendars, fiscal years, and periods](https://learn.microsoft.com/en-us/dynamics365/finance/budgeting/fiscal-calendars-fiscal-years-periods),
[Main account types](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/main-account-types),
[Three-way matching policies](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-payable/three-way-matching-policies),
[Credit management setup](https://learn.microsoft.com/en-us/dynamics365/finance/accounts-receivable/cm-credit-mgmt-setup),
[Number sequences overview](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/number-sequence-overview),
[Inventory close](https://learn.microsoft.com/en-us/dynamics365/supply-chain/cost-management/inventory-close).
