# sap-s4hana-migration-mm

My working notes for the MM side of an ECC to S/4HANA move. The bigger picture (basis, SUM, sizing) is covered well elsewhere, so this sticks to what an MM consultant actually has to do: business partner conversion, simplification items, data migration, cutover and testing.

There's also a `templates` folder with sample load files and checklists I use as a starting point. All data in there is made up.

## Why bother now

ECC 6.0 mainstream maintenance ends end of 2027. Extended maintenance runs to 2030, but it costs extra. So most ECC customers are somewhere in their S/4 journey right now, and the MM workstream is usually one of the busiest ones.

## Contents

- [01 - Picking an approach](docs/01-approach.md) - greenfield, brownfield, selective
- [02 - Simplification items for MM](docs/02-simplification-items.md)
- [03 - CVI / business partner](docs/03-cvi-business-partner.md) - the thing that blocks a conversion if you leave it too late
- [04 - Data migration](docs/04-data-migration.md) - migration cockpit, objects, load sequence
- [05 - Cutover](docs/05-cutover.md) - what MM has to do on the weekend
- [06 - Testing](docs/06-testing.md) - test scenarios for P2P and inventory
- [07 - Custom code, output and Fiori](docs/07-custom-code-output-fiori.md)

Templates:

- [cutover-checklist.csv](templates/cutover-checklist.csv)
- [readiness-questions.md](templates/readiness-questions.md) - questions I ask in the first workshops
- sample load files: [products](templates/sample-products.csv), [suppliers](templates/sample-suppliers.csv), [info records](templates/sample-info-records.csv), [open POs](templates/sample-open-pos.csv), [stock](templates/sample-stock.csv)

The sample files are simplified. The real Migration Cockpit templates have many more fields and change between releases, so always download the template from your own system.

Related: my [P2P notes repo](https://github.com/manikantavootakuti-ctrl/sap-mm-procure-to-pay) for the process side.

*SAP, S/4HANA and Fiori are trademarks of SAP SE. Personal notes, not affiliated with SAP.*
