# Plan 03: Unity, Free Toolchain and First Steps

Follows on from `02-desktop-engine-and-mvp-plan.md`. This version locks in your decisions.

## Decisions locked in
| Question | Answer |
|---|---|
| Engine | **Unity (HDRP)**, no Unreal comparison needed |
| Budget | **Free tools only** |
| Hardware | Desktop RTX 5070 Ti, laptop RTX 5070 (mobile) |
| Scope | **Your own property only** |

## What these decisions change

### Own property only
This simplifies the app a lot:
- No need for a general site-drawing tool or LINZ import for arbitrary locations. You can **hand-build your one section** once.
- The best way to get an accurate site is to measure it: tape measure or phone LiDAR/photogrammetry for the boundary, house footprint, existing trees, fences and slope. A free option is to trace a LINZ aerial image once as a ground texture and reference.
- Multiple "designs" can be saved as variants of the same site (for example "Plan A" and "Plan B").
- Later, you can add real shadow and sun-path simulation for your actual latitude and orientation. This is a high-value feature for one known site.

### Free only
| Need | Free tool |
|---|---|
| Engine | Unity Personal (free under the revenue threshold) |
| Render pipeline | HDRP, included |
| Modelling and cleanup | **Blender** |
| Tree/shrub generation | Unity's built-in **Tree Editor**, Blender's built-in **Sapling Tree Gen** add-on, and Blender Geometry Nodes |
| Textures and HDRIs | **Poly Haven** and **ambientCG** (CC0, free for any use) |
| Photogrammetry | **Meshroom** (free, needs an NVIDIA GPU, which you have) or **Polycam** free tier |
| Generic foliage, grass, rocks | Unity Asset Store free section, plus Fab free content (**check licence for each pack**) |
| Version control | Git, with Git LFS for large assets |
| Plant data | NZ Flora and NZPCN (you enter the data into your own JSON file) |

Note: SpeedTree is out because of the budget. The Unity Tree Editor and Blender will do the job, with more manual effort.

**Licence check:** the terms of Megascans and other Fab content change over time and may be restricted to certain engines. Check the current licence before using any pack in Unity.

### Hardware
Both GPUs are comfortably above what HDRP needs. Notes:
- Develop on the desktop (5070 Ti). Test on the laptop to confirm it still runs smoothly.
- Hardware ray tracing and path tracing are options in HDRP for beauty screenshots, but keep them off for everyday editing.
- Expect to need an LOD (level of detail) setup for plants so that a full garden still runs at a good frame rate on the laptop.

## Plan from here

### Phase 0: Setup (about 1 to 2 days)
1. Install **Unity Hub**, then the current **Unity LTS** release (pick the latest LTS, and check that HDRP is available for it).
2. Install **Blender** and **Git + Git LFS**.
3. Create a Unity project from the **HDRP template** inside this repo (or a subfolder such as `unity/`).
4. Add a Unity `.gitignore` (excluding `Library/`, `Temp/`, `Logs/`, `obj/` and the like) and a `.gitattributes` for LFS (textures, models, audio).
5. Commit the empty project as a baseline.

### Phase 1: Learn the basics (about 1 to 2 weeks)
Work through these in order. Free official material is on Unity Learn:
- Unity Essentials pathway (editor, scenes, GameObjects, prefabs).
- Junior Programmer pathway (C# basics).
- A short HDRP lighting/volume tutorial.
- A Blender Donut-style beginner tutorial (modelling basics).

Do not skip this. You are new to 3D, and a few weeks of foundations will save a lot of confusion.

### Phase 2: Vertical slice (about 1 to 2 weeks)
Goal: **one plant, placed by clicking, in a realistic scene.**
1. HDRP scene with sky, sun and a flat terrain.
2. Camera controls: orbit, pan, zoom (and a walk mode).
3. One plant prefab (use a free tree or shrub as a stand-in).
4. Click to place, and delete.

### Phase 3: MVP (several weeks)
Follow the MVP list from plan 02:
1. Plant data file (JSON) and loader.
2. 10 to 15 NZ species with models (start with generated or stand-in assets).
3. Spread footprint circle for each plant.
4. Plant browser panel.
5. Growth slider (planting, 5 years, 20 years).
6. Save/load and automatic backups.
7. Screenshot export and a plant shopping list.

### Phase 4: Make it your property
1. Measure the section and build the terrain, house, fences and existing trees.
2. Add sun-path/shadow preview for your site's orientation.
3. Support design variants (Plan A, Plan B).

## Suggested folder layout
```
landscaping/
  doc/plans/          <- these plans
  unity/              <- the Unity project
  data/
    plants.json       <- species data
  assets-src/         <- Blender files, raw textures (LFS or kept outside the repo)
```

## Backups
- App-level: timestamped copies of each project file on every save, keeping the last N.
- Repo-level: push the repo to a private remote (GitHub or similar) with LFS. Raw assets and large files may need a separate backup (external drive or cloud folder).

## Next actions
1. Install Unity Hub, Unity LTS (with the HDRP template), Blender and Git LFS.
2. Start the Unity Essentials pathway.
3. When Phase 0 is done, I can help set up the repo structure, `.gitignore`/LFS config and the plant data schema (`data/plants.json`) with the first species filled in.

## Open questions (not blocking)
- Do you want a private remote for the repo (for backups), and where?
- Do you already have measurements or photos of your section, or will those need to be gathered?
- Which plants matter most for your property? That sets the first 10 to 15 species.
