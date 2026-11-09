# Plant data

- `plants.json`: the plant library (one object per species).
- `plants.schema.json`: JSON Schema describing every field and its allowed values.

## Status
All 10 starter species are marked `"DataQuality": "draft"`. Sizes, growth rates and tolerances were entered from general knowledge and have **not** been checked against NZ Flora (Manaaki Whenua) or the NZ Plant Conservation Network. Check each one, fill in `Source`, and then set it to `"verified"`. Sizes are typical figures for a home garden and vary with site and cultivar.

## Design notes
- **Flat, PascalCase fields with a unique `Name` key.** Unreal's Data Table import expects an array of objects with a `Name` row key, and fields that match the struct's member names. This avoids nesting.
- **Growth stages are explicit** (`Height0M`, `Height5yM`, `Height20yM`, and the matching spreads). The growth slider interpolates between them. `Mature*` is the long-term ceiling and the size used for the footprint circle.
- **Units** are metres everywhere (the `M` suffix). Unreal's native unit is centimetres, so multiply by 100 when applying sizes to actors.
- **Enums** keep filtering simple (`Sun`, `Moisture`, `FrostTolerance`, `WindTolerance`, `SaltTolerance`, `Form`). The allowed values are in the schema.

## Importing into Unreal
1. In Unreal, create a **Structure** asset (for example `S_PlantRow`) with members matching the field names and types in the schema. Use Enums (or strings for a first pass) for the choice fields.
2. Drag `plants.json` into the Content Browser. Choose **DataTable** and pick `S_PlantRow` as the row type.
3. To update, edit the JSON and use **Reimport** on the Data Table.

The struct must be created first. Unreal won't generate it from the JSON.

## Adding a species
Copy an existing entry, give it a unique lowercase `Name`, and fill in every required field. You can check the file against the schema in an editor with JSON Schema support (such as VS Code, via `"$schema"` mapping) or any online validator.
