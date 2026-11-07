# Posting map: common documents and where their accounts come from

> **Draft: Nurlin to review.** Posting type names follow the English UI of
> current versions. The exact debit and credit pairs depend on settings such as
> "post product receipt in ledger" and the inventory model. Check a real voucher
> in a sandbox before relying on this for a design.

Paths used below:

- **Customer posting profiles:** Accounts receivable > Setup > Customer posting profiles
- **Vendor posting profiles:** Accounts payable > Setup > Vendor posting profiles
- **Inventory posting:** Inventory management > Setup > Posting > Posting
- **Item groups:** Inventory management > Setup > Inventory > Item groups (shows the same inventory posting accounts, per item group)
- **Ledger posting groups (tax):** Tax > Setup > Sales tax > Ledger posting groups
- **Accounts for automatic transactions:** General ledger > Posting setup > Accounts for automatic transactions
- **Fixed asset posting profiles:** Fixed assets > Setup > Fixed asset posting profiles

<!-- REVIEW: confirm each path in a current version. -->

---

## Sales order invoice (stocked item)

| Amount | Posting type | Setup |
|---|---|---|
| What the customer owes | Customer balance | Customer posting profile (summary account) |
| Sales value | Revenue | Inventory posting > Sales order tab |
| Stock leaving inventory | Issue | Inventory posting > Sales order tab |
| Cost of the stock sold | Consumption (cost of goods sold) | Inventory posting > Sales order tab |
| Line or total discount | Discount | Inventory posting > Sales order tab |
| Sales tax | Sales tax payable | Ledger posting group on the tax code |
| Charges (freight, fees) | Set on the charge code | Accounts receivable > Charges setup > Charges code |
| Packing slip postings | Packing slip, packing slip offset | Inventory posting, only if the legal entity posts packing slips to the ledger |

## Free text invoice

| Amount | Posting type | Setup |
|---|---|---|
| What the customer owes | Customer balance | Customer posting profile |
| Each line | The main account on the line | Entered by the user (can default from a template) |
| Sales tax | Sales tax payable | Ledger posting group |

## Purchase order invoice (stocked item)

| Amount | Posting type | Setup |
|---|---|---|
| What we owe the vendor | Vendor balance | Vendor posting profile (summary account) |
| Stock coming in | Receipt | Inventory posting > Purchase order tab |
| Offset of the receipt | Purchase expenditure for product | Inventory posting > Purchase order tab |
| Accrual at product receipt (reversed at invoice) | Product receipt, Purchase expenditure un-invoiced | Inventory posting > Purchase order tab, only if product receipts post to the ledger |
| Sales tax | Sales tax receivable | Ledger posting group |
| Price difference (standard cost) | Standard cost variance types | Inventory posting > Standard cost variance tab |

<!-- REVIEW: confirm debit/credit pairs against Learn "Purchase order posting" and a sandbox voucher. -->

## Purchase order invoice (procurement category, no item)

| Amount | Posting type | Setup |
|---|---|---|
| What we owe the vendor | Vendor balance | Vendor posting profile |
| The expense | Purchase expenditure for expense | Inventory posting > Purchase order tab, item code = Category |
| Sales tax | Sales tax receivable | Ledger posting group |

## Vendor invoice journal and general journal

- Each line has an **account type** (Ledger, Customer, Vendor, Bank, Fixed
  asset) and an **offset account**.
- Customer and vendor lines post their balance through the **posting profile**
  on the journal line.
- The **journal name** can fix the offset account.
- Bank lines use the **main account on the bank account**.
- Fixed asset lines use the **fixed asset posting profile** for the book and
  posting layer.

## Inventory journals

| Journal | Accounts |
|---|---|
| Movement journal | The offset account on the line (it can default from the journal name) |
| Counting journal | Inventory profit or loss, Inventory posting > Inventory tab |
| Transfer journal | Normally no ledger impact unless dimensions or sites change the account |

## Fixed assets

The fixed asset posting profile gives one account per transaction type
(acquisition, depreciation, disposal and so on), per book and posting layer.

## Automatic accounts

Penny differences, rounding, cash discounts, and some system postings come from
**Accounts for automatic transactions**. Exchange gains and losses come from the
**accounts for currency revaluation** on the Ledger page, or the currency
revaluation posting profile for customers and vendors.

---

## Where the dimensions come from

1. Default dimensions on the **master record**: customer, vendor, item,
   project, employee.
2. The **document header**, which copies from the master record and can be
   changed.
3. The **line**, which copies from the header and the item, and can be changed.
4. A **fixed dimension value on the main account**, which overrides all of these.
5. The **account structure and advanced rules** then check that the combination
   is allowed.

<!-- REVIEW: confirm the merge order in current versions. -->

Learn: [Financial dimensions and posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/default-dimensions),
[Default financial dimensions on financial journals](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/dimensions-default-values),
[Accounts receivable posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/accts-recvble-posting),
[Accounts payable posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/accts-payble-posting),
[Inventory posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/inventory-posting),
[Production posting](https://learn.microsoft.com/en-us/dynamics365/finance/general-ledger/production-posting),
[Set up fixed asset posting profiles](https://learn.microsoft.com/en-us/dynamics365/finance/fixed-assets/tasks/set-up-fixed-asset-posting-profiles).
