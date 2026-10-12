# 02 - Simplification items for MM

Simplification items are SAP's list of "this works differently / is gone in S/4". For a conversion you run the simplification item check (report /SDF/RC_START_CHECK in the source system) and it tells you which ones hit your system. The Readiness Check gives a nicer report of the same thing.

These are the ones I'd expect on almost every MM project. Always check the Simplification Item Catalog for your target release, the list changes.

## Business partner instead of vendor master

XK01/MK01/FK01 are replaced by BP. Vendors must be converted to BPs via CVI before the conversion - it's a hard prerequisite. Details in [03](03-cvi-business-partner.md).

## Inventory management data model (MATDOC)

MKPF/MSEG and the aggregate stock tables (MARD, MCHB, MSKA...) are replaced by MATDOC. Old tables are still there as compatibility views (CDS based), so reading them still works. But:
- custom code that **writes** to these tables breaks
- custom reports reading huge amounts of MSEG might get slow or behave differently - test them
- MB* transactions (MB01, MB1A, MB1B, MB1C, MB31...) are gone, use MIGO

## Material ledger is mandatory

In S/4 the material ledger is always active for valuation (actual costing is still optional). If ECC didn't use ML, the conversion activates it - talk to the CO team early, it affects valuation and period end.

## Storage location MRP -> MRP areas

Storage location MRP (MRP indicator in MARD) isn't supported any more. You have to move to MRP areas before or during the conversion.

## MRP Live

MD01N is the HANA-optimized MRP. Classic MD01/MD02 still exist in most releases, but MD01N is the target. Some custom BAdIs/exits in MRP may not be called in MRP Live - worth checking.

## Material number length

Can be extended to 40 chars. It's optional, but if switched on, interfaces and custom code with 18-char assumptions need checking.

## Pricing - KONV -> PRCD_ELEMENTS

PO pricing conditions are stored in PRCD_ELEMENTS. Custom code selecting from KONV needs changing.

## Output management

New BRF+ based output management for purchasing documents. NAST-based output is still possible in some releases, but the direction is clear. Plan the PO / RFQ forms.

## Foreign trade

MM foreign trade (MM-FT / SD-FT functions) isn't available in S/4 - replaced by SAP GTS or other solutions.

## Approvals

Classic release strategy still works. Flexible workflow is the newer option for PR/PO. Not a must, but a decision to make.

## How I track them

One line per item: ID, title, relevant yes/no, owner, action, status. The check report gives you the list, the work is in deciding the action for each.
