# 07 - Custom code, output and Fiori

The "technical" bits an MM consultant still gets pulled into.

## Custom code

Developers run the ATC (ABAP test cockpit) with the S/4HANA readiness checks, or the *Custom Code Migration* app. It lists every place that conflicts with simplification items. MM's job is to say which reports and enhancements are still needed - a surprising number aren't used any more.

Typical MM findings:
- SELECTs on MSEG / MKPF / aggregate stock tables (works via compat views, but check performance)
- direct writes to stock tables - must go
- SELECTs on KONV - change to PRCD_ELEMENTS
- user exits / BAdIs in MRP that MRP Live doesn't call
- 18-char material number assumptions (if extended material number is on)
- custom vendor master screens / fields - need to move to BP

Usage data from the old system (e.g. from the usage statistics) helps a lot to decide what to retire.

## Output management

Decisions to make for PO, RFQ, scheduling agreement:
- keep NAST or move to the new output management
- which forms - new Adobe forms, or redo the old Smart Forms
- channels - print, email, EDI / Ariba Network
- email: who gets it (from BP? from a partner function?)

The PO form is always on the critical path. Start early, get the business to approve the layout.

## Fiori

Not everything needs Fiori on day one, but some things only exist there (e.g. flexible workflow config, some analytics). Typical MM role setup:

- buyer - manage PRs/POs, monitor items, supplier evaluation
- warehouse - post GR, stock overview
- AP clerk - create/manage supplier invoices
- master data - products, BPs, info records

Use SAP's business role templates as the starting point and trim, rather than building catalogs from zero.

Users will still ask for ME21N and MIGO. That's fine - SAP GUI transactions can sit in the launchpad too.
