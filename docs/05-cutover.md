# 05 - Cutover

The MM part of the cutover plan. Exact timings depend on the project, but the order is pretty much always like this.

A full checklist with owners and timings is in [templates/cutover-checklist.csv](../templates/cutover-checklist.csv).

## Weeks before

- final cleansing round (suppliers, materials)
- close old open POs that won't be delivered
- clear GR/IR as far as possible (MR11) - fewer open items = easier reconciliation
- agree the business freeze window: when do buyers stop creating POs, when does the warehouse stop posting?
- dress rehearsal (mock cutover) - at least one, better two

## Freeze

- stop new POs / PRs
- last goods movements posted
- invoices posted or put on hold
- MM period closed (MMPV) in the old system

## Extract / reports from old system

Take these **before** anything is loaded, they're the baseline for reconciliation:
- stock per plant / sloc / batch with value (MB52 / MB5L)
- open POs (ME2N with "open" selection)
- GR/IR balance
- list of suppliers and materials in scope

## Load (greenfield) or conversion (brownfield)

Greenfield: load in the order from [04](04-data-migration.md).

Brownfield: SUM runs the conversion, MATDOC migration and ML activation happen here. MM's job is mainly the checks after.

## Validation

- stock quantity and value match per plant / sloc
- open PO count and value match
- spot checks: open a few POs, info records, BPs in the new system
- post a test GR and test invoice (and reverse them) to prove account determination works

## Go / no-go

Business signs off the reconciliation. Only then is the system opened for users.

## First days after go-live

- hypercare - be on site / reachable
- watch for: GR errors (account determination, periods), invoice blocks, output not printing, authorizations
- daily check of MATDOC / stock values and GR/IR
