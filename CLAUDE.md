# Block Blast

Mobile-first cartoon first-person shooter in the browser (three.js). Read HANDOFF.md for status, gameplay numbers, art direction and roadmap.

## Stack

- Currently: single `index.html`, three.js r128 from cdnjs, no build.
- Planned: Vite + TypeScript + npm `three`.

## Commands

- Run now: `python3 -m http.server 8080` in this folder.
- After migration: `npm run dev`, `npm run build`, `npm run typecheck`, `npm run lint`.

## Rules

- **Mobile first.** Every feature must work with touch controls on a phone-sized screen. Keep desktop keys as a bonus.
- **Keep the art direction.** Toon shading with a stepped gradient map, ink outlines on every character and prop, sticker-style UI with thick borders and hard shadows, palette from the CSS variables. No realistic textures.
- **No image or audio asset files unless asked:** graphics are procedural, sound should be WebAudio synthesis.
- **Performance budget:** ~60 fps on a mid-range phone. Cap pixel ratio at 2, reuse geometries and materials where flashing is not needed, avoid per-frame allocations.
- **Hit detection** is non-recursive raycasting against explicit mesh lists; any new hittable part must be added to those lists, and outline meshes must not be.
- **Do not change gameplay numbers** (see HANDOFF.md) without saying so and explaining why.
- **Verify visually** (screenshot or run in a browser) before calling a visual change done; this project has not yet been seen running.

## Workflow

- Make small, reviewable changes; run the game after each.
- When migrating to modules, keep behaviour identical first, then add features in separate commits.
- Update HANDOFF.md (status, known issues, roadmap) whenever something meaningful changes.
