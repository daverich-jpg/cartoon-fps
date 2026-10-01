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
- **Keep the art direction** (see HANDOFF.md → Art direction). Illustrated cartoon world: tinted toon ramp, soft silhouettes (`rbox`, `lathe`, `lumpy`; never raw cubes), sticker-style UI with thick borders and hard shadows. No realistic textures.
- **Outlines are selective, not universal.** Ink (`INK`) on enemies, the Wishing Star and the player rig; soft `LINE` on cover objects; none on backdrop/foliage.
- **Colour carries meaning.** Tangerine = enemies only. Gold = the Wishing Star / objectives only. Blue = the player. Environment stays in the muted palette (`P` in the script, CSS vars in `:root`).
- **No image or audio asset files unless asked:** graphics are procedural, sound should be WebAudio synthesis.
- **Performance budget:** ~60 fps on a mid-range phone. Pixel ratio capped at 2 (auto-steps down under ~45 fps). Static props go through the `B` merge builder (one draw per material bucket); scatter goes through `instGrid` so it culls. Keep a view under ~250 draw calls / ~400k triangles. Avoid per-frame allocations.
- **Hit detection** is non-recursive raycasting against explicit mesh lists (`obsM`, each enemy's `meshes`); any new hittable part must be added to those lists, and outline meshes must not be. Cover is merged per object: push `group.meshes` into `obsM`. Enemy meshes need their own materials (hit flash uses `emissive`).
- **Do not change gameplay numbers** (see HANDOFF.md) without saying so and explaining why.
- **Verify visually** (screenshot or run in a browser) before calling a visual change done; this project has not yet been seen running.

## Workflow

- Make small, reviewable changes; run the game after each.
- When migrating to modules, keep behaviour identical first, then add features in separate commits.
- Update HANDOFF.md (status, known issues, roadmap) whenever something meaningful changes.
