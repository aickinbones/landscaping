# Unreal: Create the plant Structure and import `plants.json`

How to create the `S_PlantRow` Structure asset in the Unreal editor, then import `data/plants.json` as a Data Table.

## Create the Structure
1. Open the **Content Browser** and click the **Content** folder. Make a subfolder first if you like, such as `Content/Data`, by right-clicking and choosing **New Folder**.
2. Right-click an empty area, then **Blueprints**, then **Structure**.
3. Name it `S_PlantRow` and press Enter.
4. Double-click it to open the Structure editor.

## Add the members
1. Click **New Variable** (top left). Rename the new variable in the Details panel, and set its **type** with the dropdown next to it.
2. Repeat for each member below.

| Type | Member names |
|---|---|
| **String** | `CommonName`, `MaoriName`, `BotanicalName`, `Form`, `GrowthRate`, `Sun`, `Moisture`, `FrostTolerance`, `WindTolerance`, `SaltTolerance`, `Notes`, `Source`, `DataQuality` |
| **Boolean** | `Evergreen` |
| **Float** (shown as "Float (double-precision)" in UE5) | `MatureHeightM`, `MatureSpreadM`, `Height0M`, `Spread0M`, `Height5yM`, `Spread5yM`, `Height20yM`, `Spread20yM` |

3. Click **Save** (top left), then close the editor.

## Things to watch
- **Do not add a `Name` member.** Unreal uses the JSON `Name` key as the Data Table row name automatically, and a duplicate member would cause an error.
- **Spelling and capitalisation must match** the JSON keys exactly (for example `Height5yM`, not `Height5YM`). Mismatches import as empty or default values.
- The choice fields (`Form`, `Sun` and so on) are **Strings** for now. You can switch to Enums later once the rest works.

## Import the JSON
1. Drag `data/plants.json` from File Explorer into the Content Browser.
2. In the import dialog, set **Data Table Row Type** to `S_PlantRow` and click **Apply**.
3. Double-click the new Data Table asset to check that all 10 species appear with values filled in.

If any column shows blank or zero, it usually means a member name doesn't match the JSON.

## Re-importing after edits
Edit `data/plants.json`, then right-click the Data Table asset in Unreal and choose **Reimport**.

See `data/README.md` for the field definitions and `data/plants.schema.json` for the allowed values.
