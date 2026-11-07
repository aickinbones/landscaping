# NZ Landscaping App: Plan

## Recommendation
Build it as a **web app** using **TypeScript + React + Three.js (via React Three Fiber)**. It runs on Windows, Mac and tablets with no install. It's easy to share with clients, and you can wrap it later as a desktop or mobile app if needed. Three.js handles orbit, zoom and pan out of the box.

## Core features (MVP)
1. **Site setup**: draw a section boundary (or import a satellite or LINZ aerial as a ground texture), and set the scale.
2. **3D view**: orbit, zoom and pan, with a top-down and a walk-through (eye-height) mode.
3. **Plant library**: searchable NZ natives, filterable by region, sun, moisture, wind and salt tolerance, frost hardiness, mature height and spread, and growth rate.
4. **Placement**: drag plants onto the terrain, with a footprint circle showing mature spread. Add paths, lawn, garden beds and structures as simple shapes.
5. **Growth slider**: show the garden at planting, 5 years and 20 years. This is the feature that makes it more than a generic landscaping tool.
6. **Save/export**: a plant list with quantities, plus screenshots.

## Later phases
- Sun and shadow simulation by date and time of year.
- Terrain and slope from LINZ elevation data.
- Ecological-region planting suggestions, such as "plants that suit coastal Wellington".
- Companion and pest information, and a planting calendar.
- Cost estimates and nursery links.
- AR preview on a phone.

## Data sources
- **NZ Flora** (Manaaki Whenua / Landcare Research) for botanical data.
- **NZ Plant Conservation Network** for conservation status and descriptions.
- **iNaturalist NZ** for distribution and photos (check licensing).
- **LINZ Data Service** for aerial imagery and elevation (open data).
- **Māori names**: use te reo names alongside the common and botanical ones, and consider consulting a cultural advisor or using sources like the Māori Plant Use database.

## 3D plant approach
This is the biggest design decision:
- **Billboards/sprites** (flat images that face the camera): cheap, fast and good for hundreds of plants. This is my suggestion for the MVP.
- **Procedural trees/shrubs** (generated meshes, with parameters for height, spread and habit): scales well and supports the growth slider.
- **Hand-modelled assets**: the best looking, but slow to produce for hundreds of species.

A hybrid works well. Use procedural generation by plant form (tree fern, flax, rounded shrub, groundcover, canopy tree) and add custom models only for hero species like pōhutukawa, kōwhai and ponga.

## Suggested build order
1. Scaffold the project (Vite + React + R3F) and a flat ground plane with orbit controls.
2. Build the plant data schema and seed about 30 well-known species by hand.
3. Add placement and selection, with spread footprints.
4. Add the plant browser and filters.
5. Add save/load (local storage first, then a backend if needed).
6. Add the growth slider and procedural plant forms.
7. Add terrain and aerial imagery.

## Questions that would change the plan
- **Who is it for?** Home gardeners, professional designers or students. This affects how much detail and polish you need.
- **Platform**: is web OK, or do you want a native desktop app (Unity or Godot would be the alternative)?
- **Solo or team**, and what's your experience with 3D? This changes how ambitious the MVP should be.
- **Realism**: stylised and clean, or photorealistic?
- Will you need **user accounts and cloud saving**, or is local-only fine at first?
