# Plan 04: Switch to Unreal Engine 5

Replaces the engine-specific parts of plans 02 and 03 (Unity, HDRP, Unity Learn, the Unity folder layout). Everything else carries over: own property only, free tools only, local storage with backups, and the MVP feature list.

## Why this is a good fit
Photorealistic vegetation is where Unreal is strongest:
- **Nanite** renders very dense, high-polygon geometry (rocks, trunks, and in recent versions foliage) without hand-built LODs.
- **Lumen** gives realistic global lighting and soft shadows with no baking, which suits sun and shade studies in a garden.
- Built-in **Landscape** (terrain), **Foliage** tool and **PCG** (Procedural Content Generation) framework for scattering plants.
- Free for you. Unreal charges royalties only above a high revenue threshold (check Epic's current terms).

## The trade-offs
- Steeper learning curve and a heavier editor than Unity.
- Large disk usage: the engine is tens of GB, and projects get big fast.
- Longer first-time shader compiles and project loads.
- Your hardware is fine. The 5070 Ti desktop is a great fit, and the 5070 laptop should cope for testing if you keep Lumen and Nanite settings sensible.

## Scripting: use Blueprints first
Unreal offers C++ and **Blueprints** (visual node scripting).
- **Start with Blueprints.** You can build the whole MVP (placement, UI, growth slider, save/load) in Blueprints without writing C++.
- Learn C++ later only if you hit performance limits or want cleaner code. You can mix both in one project.
- Visual Studio is only needed once you start with C++.

## Free toolchain (updated)
| Need | Free tool |
|---|---|
| Engine | Unreal Engine 5 (latest stable 5.x) via the Epic Games Launcher |
| Modelling and cleanup | **Blender** |
| Free plant and rock assets | **Fab** (Epic's marketplace) free content, including Megascans. **Check the licence on each asset**, because terms vary and some are limited to Unreal |
| Textures and HDRIs | **Poly Haven** and **ambientCG** (CC0) |
| Photogrammetry | **Meshroom** or **Polycam** free tier, or **RealityScan** (Epic's free scanning tool) |
| Tree generation | Blender Sapling Tree Gen, Geometry Nodes, or Unreal's **Procedural Vegetation Editor** (check whether it is available and stable in the current engine version before relying on it) |
| Version control | Git + Git LFS |

## Revised build order

### Phase 0: Setup (1 to 2 days)
1. Install the **Epic Games Launcher** and the current stable **Unreal Engine 5**.
2. Install **Blender** and **Git LFS**.
3. Create a new project. Choose a blank or Architecture/"Games" template with **no starter content that you don't need**, Blueprint (not C++), and desktop/maximum quality.
4. Put it in this repo in a subfolder, for example `unreal/NZLandscape/`.
5. Add an Unreal `.gitignore` (excluding `Binaries/`, `Intermediate/`, `Saved/`, `DerivedDataCache/`, `.vs/`) and a `.gitattributes` for LFS covering `.uasset`, `.umap` and large textures and models.
6. Commit the empty project as a baseline.

### Phase 1: Learn the basics (1 to 3 weeks)
Free official material on **Epic Developer Community Learning** (dev.epicgames.com/community/learning):
- Unreal Engine editor basics and the level editor.
- Blueprint fundamentals.
- Landscape, Foliage and Lumen lighting intro.
- A Blender beginner tutorial (modelling basics).

### Phase 2: Vertical slice (1 to 2 weeks)
Goal: **one plant, placed by clicking, in a realistic scene.**
1. Level with sky, sun, a landscape and Lumen lighting.
2. Camera pawn with orbit, pan and zoom (and a walk mode).
3. One plant actor (free asset as a stand-in).
4. Click to place and delete, using Blueprints.

### Phase 3: MVP (several weeks)
1. Plant data table (Unreal's **Data Table** from a CSV/JSON, or a Data Asset per species).
2. 10 to 15 NZ species with models, starting with stand-ins.
3. Spread footprint circle for each plant.
4. Plant browser UI panel (UMG widgets).
5. **Growth slider**: swap or scale plant meshes per age stage (planting, 5 years, 20 years).
6. **Save/load**: use Unreal's SaveGame system, plus exporting designs to a local file, with automatic timestamped backups.
7. Screenshot export (High Resolution Screenshot) and a plant shopping list.

### Phase 4: Make it your property
1. Measure the section and build the landscape, house, fences and existing trees.
2. Set the sun's location and orientation for your real latitude and longitude, so shadows match your site through the year.
3. Design variants (Plan A, Plan B).

### Packaging
When ready, **package** the project as a standalone Windows `.exe` so it runs without opening the editor.

## Suggested folder layout
```
landscaping/
  doc/plans/              <- these plans
  unreal/NZLandscape/     <- the Unreal project
  data/
    plants.json / .csv    <- species data, imported into a Data Table
  assets-src/             <- Blender files and raw textures (LFS or kept outside the repo)
```

## Risks and mitigations
- **Learning curve**: keep the first slice tiny, and stay in Blueprints.
- **Project size and repo bloat**: LFS from day one, and never commit `Intermediate/`, `Saved/` or `DerivedDataCache/`. Consider backing up the project to an external drive in addition to Git.
- **Asset licences**: record the source and licence of every imported asset in a simple `assets-licences.md`.
- **Plant realism for NZ species**: few exact assets exist. Start with stand-ins, then replace species by species with scans or Blender models.
- **Version upgrades**: Unreal projects can be hard to move between engine versions. Pick a stable 5.x version and stay on it for the whole project.

## Next actions
1. Install Epic Games Launcher, Unreal Engine 5, Blender and Git LFS.
2. Create the Blueprint project in `unreal/NZLandscape/`.
3. Start the Epic Developer Community learning paths.
4. Once the project exists, I can help with the `.gitignore` and LFS config, the folder structure, and the plant data schema with the first species.

## Open questions (not blocking)
- Do you want a private remote for repo backups, and where?
- Do you have measurements or photos of your section yet?
- Which plants matter most for your property? That sets the first 10 to 15 species.
