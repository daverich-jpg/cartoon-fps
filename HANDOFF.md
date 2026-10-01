# Block Blast: Handoff

A mobile-first, cartoon first-person shooter that runs in the browser. This doc is for continuing the build in Claude Code.

## Status

- Working prototype, single file: `index.html` (~15 kB, no build step).
- Syntax-checked, but never visually verified or playtested by the author (it was built in a chat sandbox with no browser). Treat the first task as "run it and see what's broken."
- Published as a Claude artifact during the chat; this folder is the source of truth now.

## Run it

```bash
cd block-blast
python3 -m http.server 8080   # then open http://localhost:8080 (phone: use your LAN IP)
```

Needs internet for two CDN resources: three.js r128 and the Fredoka font (see Constraints).

## Gameplay (current)

| Thing | Value |
|---|---|
| Player HP | 100; each enemy touch costs 10, once per 0.8 s per enemy |
| Fire rate | 1 shot / 0.2 s, hitscan raycast from screen centre |
| Enemy HP | 3. Head hit = 2 damage, body/limb hit = 1 |
| Waves | Wave *n* spawns 2 + 2n enemies, speed 2 + 0.25n; next wave 1.8 s after clear |
| Arena | Flat, clamped to ±38 units; 12 robot-head pillars + giant central star as cover |
| Score | KO count and wave number only; no persistence |

**Controls:** left thumbstick moves, drag anywhere on the right to aim, FIRE button (hold = auto-fire). Desktop: WASD + Space (no mouse look yet).

## Art direction

Cartoon, driven by three reference images the user supplied:

1. **Geometric gradient face** (blue/pink/mint gradient, flat bold shapes, big toothy grin) → sky gradient, UI colours, sticker look.
2. **Sketchy dome-head robot sheet** (grey box head, cream dome, yellow eyes, red torso, gold stars on dusty pink) → cover pillars, star motif, ground colour.
3. **Long-legged toothy orange creatures** → the enemies.

**Implementation:** `MeshToonMaterial` with a 3-step gradient map plus an inverted-hull outline (a back-side ink mesh scaled ~1.07 as a child of each mesh).

**Palette tokens** (CSS vars in the file): ink `#2a1830`, blue `#3aa6d0`, pink `#f0a0c0`, mint `#9fd08a`, gold `#f5b82e`, coral `#f0604c`, cream `#fff1c9`.

**UI rules:** thick 4–5 px ink borders, hard drop shadow (`0 5–7px 0 ink`), pill shapes, Fredoka font. The thumbstick knob is a cartoon eye on purpose.

A previous direction (pastel low-poly + procedural mud/grass ground) was replaced by this one. The user liked the mud/grass idea earlier; it could return as an optional arena theme.

## Code map (`index.html`)

One `<script>`, roughly in this order:

1. Renderer, scene, gradient sky, fog, lights
2. Toon helpers: `T(color)` material, `ol(mesh, k)` outline
3. Ground texture (canvas, tiled) and star geometry (`SG`)
4. Cover: robot-head pillars (`obs` collision circles, `obsM` raycast meshes) and the central star
5. `push()` circle collision for player and enemies
6. Blaster (child of camera), muzzle flash
7. `mkEnemy()`, `spawnWave()`, `shoot()`
8. Pointer controls (stick, look, fire) and keyboard
9. `reset()` and the game loop

Everything is global, with no modules or state object. Splitting this up is task #1 (see roadmap).

## Constraints and gotchas

- **three.js is r128 via cdnjs UMD.** Several APIs differ from modern three (`LuminanceFormat`, no `outputEncoding` changes, `CapsuleGeometry` unavailable). Check before upgrading; when migrating to npm `three`, expect to touch the toon gradient map, colour management and lighting intensities.
- The chat's publishing sandbox only allowed scripts from cdnjs.cloudflare.com and Google Fonts. Not a constraint for Claude Code, but it explains the single-file shape and the absence of image assets (everything is procedural).
- **Raycasting is non-recursive:** only meshes listed in `obsM` and each enemy's meshes are hit-tested. The outline children are deliberately excluded. Add new hittable parts to those arrays.
- Enemy hit flash uses `material.emissive`; keep materials per-mesh (not shared) for anything that can flash.
- Pillars' eyes/knobs are decoration: bullets pass through them and hit the box behind.
- Touch handling uses pointer capture per control; the look layer sits under the stick and fire button.

## Known issues / unverified

- Never run on a real phone: check frame rate (outlines double the mesh count; pixel ratio is capped at 2).
- Gun may clip or sit oddly at some aspect ratios.
- Thin parts (arms, legs) use a bigger outline scale; outline thickness may look uneven.
- Ground texture repeat (30×) may show visible tiling.
- No pause, no sound, no mouse look on desktop, no landscape-specific layout.
- Enemies can stack on one another and cluster; there is no separation steering.
- The start overlay is the only place the controls are explained.

## Roadmap (suggested order)

1. **Verify and fix.** Run on a phone and desktop, fix whatever breaks, and profile.
2. **Project structure.** Vite + npm `three`; split into `src/{scene,materials,enemies,player,input,ui,game}.ts`; one `GameState` object instead of globals; add lint and typecheck.
3. **Feel.** Hit sparks, damage numbers, enemy hit-stagger, screen shake, squash on death (pop into stars), better recoil.
4. **Audio.** WebAudio synth blips for shoot, hit, KO, hurt (no asset files needed).
5. **Content.** Second enemy type (fast runner), a boss every 5th wave, health pickups (gold stars), a second weapon.
6. **Meta.** Best-wave score in `localStorage`, pause menu, settings (look sensitivity, left-handed layout).
7. **Style pass.** Apply the gradient-face reference (image 1) to enemy faces and the UI, and bring back the mud/grass ground as an alternate theme.
8. **Ship.** PWA manifest and offline cache, deploy to Netlify or GitHub Pages.

## Suggested first prompts for Claude Code

1. "Read HANDOFF.md and CLAUDE.md, run `index.html` locally, and list anything broken or janky before changing code."
2. "Migrate to Vite with npm three, keep the game behaving identically, and split the file per the code map."
3. "Add hit sparks, screen shake and a star-burst on enemy KO, keeping the cartoon style."

## Definition of done for any change

- Plays correctly on a phone-sized viewport with touch controls.
- Holds roughly 60 fps on a mid-range phone.
- Matches the art direction above (ink outlines, flat toon shading, sticker UI).
