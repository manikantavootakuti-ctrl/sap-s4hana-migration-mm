# 03 - CVI and business partner

If there's one thing to start early on a brownfield project, it's this. The conversion won't run until every vendor (and customer) has a business partner. On a system with years of data, cleaning it up takes months, not weeks.

## What CVI does

Customer-Vendor Integration links the BP to the classic vendor/customer tables. After it's active, you maintain everything in BP and CVI keeps LFA1/LFB1/LFM1 in sync.

## Steps (rough order)

1. **Pre-checks** - run the CVI pre-check report (PRECHECK_UPGRADATION_REPORT) in ECC. It shows missing config and data problems.
2. **Data cleansing** - this is the long part:
   - vendors with missing / invalid postal codes, tax numbers, bank data
   - duplicates (same supplier created 3 times)
   - old vendors nobody uses - archive or flag them, don't convert junk
   - vendors that are also customers - decide if they share one BP
3. **Config**
   - BP roles (FLVN00, FLVN01)
   - BP groupings and number ranges
   - mapping: vendor account group <-> BP grouping
   - number assignment - usually same number for BP and vendor, makes life much easier
   - field mapping for things like industry, titles, etc.
4. **Synchronization** - MDS_LOAD_COCKPIT to create BPs from the existing vendors in bulk
5. **Errors** - MDS_PPO2 (post processing office) shows what failed. Fix, re-run, repeat.
6. **Activate BP-first** - from now on new suppliers are created via BP, even in ECC

## Things that bite

- number ranges that overlap between BP and vendor
- mandatory fields in BP that were optional in the vendor master
- contact persons - they become BPs too
- interfaces that create vendors (from an MDM tool or a portal) - they have to switch to BP
- someone still creating vendors in XK01 halfway through - lock it down once BP-first is on

## Greenfield

No CVI conversion needed - you load suppliers straight into the new system with the "Supplier" migration object. But the cleansing work is the same, so don't skip it.
