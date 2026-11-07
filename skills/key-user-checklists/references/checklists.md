# Checklists

> **Draft: Nurlin to review.** Menu paths follow current versions. Remove steps
> for modules the company doesn't use. "(shared)" means the setup is shared
> across legal entities: check it exists before creating it again.

---

## A. New legal entity, ready for intercompany

1. **Create the legal entity**: Organization administration > Organizations >
   Legal entities. Done when name, address, country and registration numbers
   are filled in.
2. **Ledger**: General ledger > Ledger setup > Ledger. Chart of accounts
   (shared), account structures, fiscal calendar, accounting and reporting
   currency, exchange rate type. Done when all fields are set.
3. **Ledger calendar**: General ledger > Calendars > Ledger calendars. Open the
   periods the company will post in.
4. **Financial dimensions** (shared): check legal entity overrides for values
   this company must not use.
5. **Number sequences**: Organization administration > Number sequences >
   Number sequences > Generate, for the new legal entity. Done when every
   module's parameters page shows a sequence on its Number sequences tab.
6. **Module parameters**: General ledger, Accounts payable, Accounts receivable,
   Cash and bank management, and Inventory, Procurement and Sales if used.
7. **Posting setup**: customer and vendor posting profiles, inventory posting,
   accounts for automatic transactions, ledger posting groups for tax.
8. **Tax**: sales tax authorities, settlement periods, tax codes, sales tax
   groups and item sales tax groups.
9. **Groups and terms**: customer groups, vendor groups, terms of payment,
   methods of payment.
10. **Intercompany accounting**: General ledger > Posting setup > Intercompany
    accounting, due-to and due-from accounts for each pair of legal entities.
11. **Intercompany trade**: in each company, a customer that represents the
    other company and a vendor that represents it, linked as an intercompany
    trading relation. Check the intercompany parameters.
12. **Test**: in a sandbox, post one intercompany journal and one intercompany
    sales order to invoice, in both directions. Check both vouchers.

Tip: setup can be copied from an existing legal entity with the
"Copy into legal entity" option in the Data management workspace.
<!-- REVIEW: confirm the name and location of "Copy into legal entity". -->

Learn: [Create legal entities](https://learn.microsoft.com/en-us/dynamics365/fin-ops-core/fin-ops/organization-administration/tasks/create-legal-entity),
[Intercompany accounting setup](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/intercompany-accounting-setup),
[Set up vendors, customers, and items for intercompany trade](https://learn.microsoft.com/en-us/dynamics365/supply-chain/sales-marketing/intercompany-set-up-vendors-customers-items),
[Intercompany parameters](https://learn.microsoft.com/en-us/dynamics365/supply-chain/sales-marketing/intercompany-parameters).

---

## B. Month-end close (finance)

1. **Agree the cut-off** date and time with AP, AR, inventory and payroll.
2. **Post or clear open journals**: check General journals and invoice journals
   for unposted lines.
3. **Vendor invoices**: post the ones that belong to this month; review the
   pending vendor invoices list.
4. **Accruals**: product receipts not yet invoiced, and any manual accruals.
5. **Customer invoices**: all sales invoices and free text invoices for the month.
6. **Bank**: reconcile each bank account.
7. **Fixed assets**: run depreciation and post the proposal.
8. **Foreign currency revaluation**: for AP, AR and General ledger, if the
   company uses foreign currencies.
9. **Inventory**: run recalculation or inventory close as agreed with the cost
   accountant.
10. **Subledger transfer**: make sure scheduled transfers to the ledger have run.
11. **Sales tax**: settle and post sales tax for the period, if it's a tax period.
12. **Close the period** for each module: General ledger > Calendars > Ledger
    calendars, set module access or put the period on hold.
13. **Reports**: trial balance and financial reports. Investigate differences.

Tip: the Financial period close workspace can hold this checklist as tasks with
owners and due dates.

Learn: [Financial period close workspace](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/financial-period-close-workspace),
[Close the general ledger at period end](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/close-general-ledger-at-period-end),
[Foreign currency revaluation for General ledger](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/foreign-currency-revaluation-general-ledger),
[Accruals overview](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/accruals-overview).

---

## C. Opening a new fiscal year

1. **Fiscal calendar**: General ledger > Calendars > Fiscal calendars, create the
   new year with its periods.
2. **Ledger calendar**: open the first periods of the new year for the modules
   that need them.
3. **Sales tax settlement periods**: add period intervals for the new year.
4. **Number sequences**: check sequences that restart each year, and any "reject
   duplicate within fiscal year" settings.
5. **Budgets**: load the new year's budget if budget control is on.
6. **Year-end close template**: General ledger > Period close > Year-end close
   template setup. Opening and closing transaction settings, retained earnings
   account.
7. **Run year-end close** when the old year is final (it can be rerun).
8. **Test**: post one journal dated in the new year in a sandbox, or in
   production once the periods are open.

<!-- REVIEW: confirm the path for year-end close template setup. -->

Learn: [Fiscal calendars, fiscal years, and periods](https://learn.microsoft.com/en-us/dynamics365/finance/budgeting/fiscal-calendars-fiscal-years-periods),
[Year-end close](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/year-end-close),
[Set up sales tax settlement periods](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/tasks/set-up-sales-tax-settlement-periods).

---

## D. New vendor

1. **Vendor group** exists and has a posting profile row.
2. **Create the vendor**: Accounts payable > Vendors > All vendors. Name, address,
   group, currency.
3. **Payment**: terms of payment, method of payment, bank account (with the
   company's bank account approval process, if any).
4. **Tax**: sales tax group, tax registration number.
5. **Default financial dimensions**, if the company uses them on vendors.
6. **Hold status**: not on hold, or on hold until approved, as the company's
   process requires.
7. **Test**: one vendor invoice in a sandbox, and check the voucher.

---

## E. New customer

1. **Customer group** exists and has a posting profile row.
2. **Create the customer**: Accounts receivable > Customers > All customers.
   Name, address, group, currency.
3. **Credit**: credit limit and, if credit management is on, the credit group
   and risk settings.
4. **Payment**: terms of payment, method of payment.
5. **Tax**: sales tax group, tax registration number.
6. **Default financial dimensions**, if used.
7. **Test**: one free text invoice or sales order invoice in a sandbox.

---

## F. New stocked product

1. **Product** (shared): Product information management > Products > Products.
   Product type Item, product subtype, dimension groups.
2. **Release it** to the legal entity.
3. **Released product**: item model group, item group, storage and tracking
   dimension groups, units, item sales tax groups, default order settings.
4. **Posting**: check the item group has inventory posting accounts (see the
   posting setup explainer).
5. **Cost**: a cost price, or an activated standard cost if the item model group
   uses standard cost.
6. **Test**: receive and sell one unit in a sandbox, and check both vouchers.

---

## G. Before changing a setup or parameter in production

1. **Write down** the current value, the new value and the reason.
2. **Agree** with the process owner (finance lead, supply chain lead).
3. **Test in a sandbox** with real scenarios: new documents, open documents,
   reversals.
4. **Check Feature management** for related features.
5. **Plan the change**: a quiet time, who changes it, how to undo it.
6. **Tell the users** what will change for them.
7. **After the change**, check the first real documents.
