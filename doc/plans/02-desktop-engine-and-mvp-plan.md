# Plan 02: Desktop Engine Choice and Revised MVP

Follows on from `nz-landscaping-app-plan.md`. This version reflects your answers.

## Your decisions
| Question | Answer |
|---|---|
| Audience | Just you (home gardener and landscaper) |
| Platform | Native Windows desktop app (Unity suggested) |
| Experience | Solo, new to 3D, quick learner |
| Realism | Preferably photorealistic |
| Storage | Local only, with backups |

This replaces the web recommendation in the first plan. A native engine is the right call for photorealism.

## Engine choice

| | Unity (HDRP) | Unreal Engine 5 | Godot |
|---|---|---|---|
| Photorealism | Very good | Best in class (Nanite, Lumen, foliage tools) | Limited |
| Language | C# (gentle learning curve) | C++ or Blueprints (visual scripting) | GDScript / C# |
| Beginner friendliness | Good | Steeper, heavier editor | Easiest |
| Foliage and terrain | Good, with some setup | Excellent | Basic |
| Licence for personal use | Free tier | Free until revenue threshold | Free, open source |

**Recommendation: Unity with the High Definition Render Pipeline (HDRP).**
- C# is a much easier first language for 3D than Unreal's C++.
- HDRP gives photorealistic lighting, shadows and sky.
- Unity has a huge amount of beginner material and a good terrain and tree system.

**The alternative is Unreal Engine 5.** It is better at dense, realistic vegetation out of the box. If photorealism turns out to matter more than ease of coding, switch. Do a one-weekend test with each before committing (see Step 0).

Godot is not suited to the photorealism goal.

## The honest constraint: assets, not code
Photorealism depends mostly on **plant models**, and NZ natives are poorly covered by stock asset stores. Expect to spend as much time on assets as on code. Options:
1. **SpeedTree** (subscription) or Unity's built-in Tree Editor. You model species procedurally with real leaf textures. This is the best fit for the growth slider, because a tree can be generated at several ages.
2. **Photogrammetry**: scan real plants with a phone, using tools like RealityCapture or Polycam. Good for hero plants.
3. **Blender** for hand-modelling and cleanup. It is free and you will want it either way.
4. **Stock libraries** (Fab / Unity Asset Store / Quixel Megascans). They cover generic grass, ferns, rocks and groundcover, but few true NZ species.

**Strategy:** start with a stylised-realistic look using generic stand-ins plus a small set of real NZ species, then raise the quality species by species. Do not try to build 300 photoreal plants before the app works.

## Revised MVP
1. A realistic ground and sky with free-fly and orbit camera (zoom, pan and look).
2. **10 to 15 hero NZ species** with good models. Candidates:
   - pōhutukawa
   - kōwhai
   - ponga (silver fern)
   - harakeke (flax)
   - karamu
   - mānuka
   - rengarenga
   - toetoe
   - hebe
   - kawakawa
3. Plant data file (JSON) for each species: names (common, Māori and botanical), mature size, conditions, growth rate.
4. Place, move and delete plants, with a spread footprint circle.
5. **Growth slider** (planting, 5 years, 20 years).
6. Save and load a project to a local file.
7. Screenshot export and a plant shopping list.

Deliberately out of the MVP: terrain from LINZ, sun and shadow simulation, the full species library, and cost estimates.

## Data and storage design
- **Projects** saved as JSON files in a folder, for example `Documents/NZLandscape/projects/`.
- **Plant library** as JSON or CSV, easy to edit by hand and to extend.
- **Backups**: automatic timestamped copies on every save, keeping the last N versions. Optionally sync the folder with OneDrive or Git. This covers the "local with backups" requirement without a server.

## Build order
0. **Evaluation weekend**: install Unity Hub + Unity (HDRP template) and do the official beginner tutorials. Also open a UE5 sample project so you can compare feel. Pick one.
1. Create a Unity HDRP project and put it in this git repo (with a proper `.gitignore` for Unity and Git LFS for large assets).
2. Terrain, sky and camera controls.
3. Import or build the first 3 plants (a tree, a shrub, a flax).
4. Plant data loader (JSON) and placement tool.
5. Selection, move and delete, with a UI panel for the plant list.
6. Growth slider.
7. Save, load and backups.
8. Add species and polish the visuals.

## Risks
- **Learning curve of 3D plus a new engine**: mitigate by shipping the smallest vertical slice first (one plant placed in a scene).
- **Asset effort**: see above. Budget time for it.
- **Performance** with many realistic plants: handle with LOD (level of detail) and instancing. Unity and Unreal both support these.
- **Repo size**: Unity projects and assets are big. Use Git LFS or keep raw assets outside the repo.

## Decisions I need from you
1. Go with **Unity HDRP**, or do the weekend evaluation of Unity vs Unreal first?
2. Is there a budget for tools or assets (SpeedTree, asset packs), or free only?
3. What GPU does the computer have? HDRP needs a reasonably modern one.
4. Is the target your own property, or a design tool for different sites? That changes how much terrain import matters.
