# 04 - Data migration (greenfield / selective)

For a greenfield you load data into the new system. The standard tool is the SAP S/4HANA Migration Cockpit - in current releases it's the Fiori app *Migrate Your Data* (the old LTMC transaction is gone).

Two ways to feed it:
- **staging tables** - you fill database tables (or upload files into them), cockpit loads from there
- **direct transfer** - cockpit reads straight from the ECC system

File upload via XML templates was the old way and still shows up in some releases.

## MM objects I usually need

| object | notes |
|---|---|
| Product | material master - basic, plant, storage location, valuation, purchasing views |
| Supplier | BP with supplier roles, company code and purch. org data |
| Purchasing info record | with conditions |
| Source list | |
| Purchase contract | only valid ones |
| Scheduling agreement | only open ones |
| Purchase order (only open PO) | open quantity only, not history |
| Material inventory balance | stock per plant / sloc / batch, with value |
| Batch | if batch managed |

## Load sequence

Dependencies decide the order:

1. Org structure and config are in place (not a migration object - it's transported)
2. Supplier
3. Product
4. Batches (if needed)
5. Purchasing info records, source lists
6. Contracts / scheduling agreements
7. Open POs
8. Stock balances - last, close to go-live, after the stock count / freeze

## Open POs - decide the rules early

- partially delivered PO -> migrate only the open quantity
- PO with GR but no invoice -> usually close in ECC and handle the invoice there, or migrate with a special rule. Agree this with FI, it affects GR/IR.
- old POs that will never be delivered -> close them in ECC, don't migrate

## Stock

- stock count / freeze before the load
- value: usually take the ECC value so the balance sheet matches
- the offsetting entry goes to a migration clearing account, FI reconciles it

## Data cleansing

Most of the effort. What I check before every load:
- duplicates (materials and suppliers)
- missing mandatory fields for the target (e.g. valuation class, purchasing group)
- units of measure and conversions
- obsolete materials - flagged for deletion in ECC? then don't migrate
- mapping tables for anything that changes (plants, material groups, purchasing groups...)

## Reconciliation

Every load gets a check: record counts and key values, source vs target. For stock, quantity and value per plant / sloc must match. For open POs, count and open value per supplier.

Sample load files are in [templates](../templates/). They're simplified - get the real template from your system.
