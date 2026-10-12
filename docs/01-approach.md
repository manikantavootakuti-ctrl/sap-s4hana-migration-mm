# 01 - Picking an approach

Three ways to get there. The decision is usually made above the MM team, but it changes MM's work a lot, so it's worth knowing the trade-offs.

## Greenfield (new implementation)

New S/4 system, processes redesigned, only master data and open items are migrated.

For MM that means:
- you build config again from scratch (or from SAP Best Practices)
- data migration is the main job - products, suppliers, info records, open POs, stock
- no history in the new system. Old POs and material docs stay in ECC (or an archive)
- good chance to get rid of years of custom stuff

## Brownfield (system conversion)

The existing ECC system is converted with SUM. Config, data and history come along.

For MM:
- CVI must be finished before the conversion - see [03](03-cvi-business-partner.md)
- simplification items need fixing beforehand (MRP areas, material ledger etc.)
- custom code needs to be adapted (MSEG, KONV...)
- less redesign, faster, but you also bring the old mess with you

## Selective data transition

Somewhere in between - e.g. new config but selected history moved over, or company codes moved in waves. Usually done with specialist tools / partners.

## Questions that usually decide it

- how much custom code is there, and is it still needed?
- are the current processes good, or does the business want to change them?
- how important is history in the system (audits, warranty, returns)?
- one go-live or waves by country / company code?
- timeline and budget (brownfield is normally quicker)

I keep a list of questions for the first workshops in [templates/readiness-questions.md](../templates/readiness-questions.md).
