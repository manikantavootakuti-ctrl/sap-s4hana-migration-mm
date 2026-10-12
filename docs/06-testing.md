# 06 - Testing

Test cycles on a typical project: unit test (each consultant tests own config), SIT (integration, end to end across modules), UAT (business tests real scenarios), regression (after fixes / before go-live).

Below are the MM scenarios I'd always have in the test plan. Each one should run end to end, including the FI postings.

## Procure to pay

| # | scenario | check |
|---|---|---|
| P01 | PR -> PO -> GR -> invoice -> payment, stock material | stock, BSX/WRX, invoice matched, F110 pays it |
| P02 | same with price control S, PO price != standard | PRD posting |
| P03 | PO with account assignment K (cost center) | consumption posting, no stock |
| P04 | PR release strategy / flexible workflow | right approver, PO blocked until released |
| P05 | PO release | output only after release |
| P06 | PO output | form prints / emails correctly |
| P07 | GR into quality inspection | stock type QI |
| P08 | GR blocked stock 103 -> 105 | not valuated until 105 |
| P09 | return to supplier 122 | stock and value reduce |
| P10 | invoice with price variance > tolerance | blocked R, release with MRBR |
| P11 | invoice before GR | blocked or not, depending on GR-based IV |
| P12 | credit memo | posting reverses correctly |
| P13 | foreign currency PO and invoice | exchange rate differences (KDM) |
| P14 | GR/IR clearing with MR11 | balance cleared |

## Inventory

| # | scenario | check |
|---|---|---|
| I01 | transfer sloc to sloc (311) | |
| I02 | transfer plant to plant (301) / STO (351) | |
| I03 | goods issue to cost center (201) | GBB/VBR account |
| I04 | scrapping (551) | |
| I05 | physical inventory - count, difference posting | |
| I06 | stock reports MMBE / MB52 / Fiori apps | values match MATDOC |

## Special procurement

| # | scenario |
|---|---|
| S01 | subcontracting - component provision, GR of finished item |
| S02 | consignment - withdrawal and settlement |
| S03 | scheduling agreement - delivery schedule, GR |

## Migration-specific

- migrated open PO can be received and invoiced
- migrated info record price is picked up on new PO
- migrated stock can be issued, value correct
- BP created via CVI can be used on a PO, with the right payment terms and bank

## Period end

- MMPV period close / open
- GR/IR analysis
- material ledger closing (with CO)

For each test: expected result, actual result, document numbers, pass/fail, defect ID if failed. Sounds obvious but it saves a lot of discussion later.
