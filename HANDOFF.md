# Block Blast: Handoff

A mobile-first, cartoon first-person shooter that runs in the browser. This doc is for continuing the build in Claude Code.

## Status

- Working prototype, single file: `index.html` (~75 kB, no build step). Git repo in this folder.
- **Visual overhaul done (Oct 2026):** the box arena is now an illustrated cartoon world (village, forest, field, backdrop landmarks, ambient life), with new enemy characters and a first-person toy blaster. Gameplay code is unchanged.
- Verified in a browser at 844×390 (landscape phone) and 375×812 (portrait phone): renders with no console errors, the shoot/KO/next-wave loop works. **Not yet run on a real phone.**
- This folder is the source of truth.

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
| Arena | Flat, clamped to ±38 units; 12 cover objects (same positions/radii as the old pillars) + the Wishing Star as cover |
| Score | KO count and wave number only; no persistence |

**Controls:** left thumbstick moves, drag anywhere on the right to aim, FIRE button (hold = auto-fire). Desktop: WASD to move; click to capture the mouse, move to aim, hold left-click or Space to fire, Esc to release (pointer lock, sensitivity `MSENS`).

## Art direction

**Goal:** it should feel like playing an FPS inside an animated cartoon: illustrative, warm, whimsical, slightly surreal. Not low-poly assets, not realistic. Inspired by the *feeling* of modern whimsical cartoons; no copied characters or locations.

**World ("the Wishing Star village"):** a fallen Wishing Star floats over a cracked plinth in a cobbled plaza. Paths lead north to a mushroom-and-teapot village (with a striped lighthouse), west into a strange forest (gumdrop pines, swirl lollipop trees, droopy lavender trees, a giant blossom tree on a hill), east to a windmill field with a giant fallen robot that someone now lives in (ladder, door, mailbox), and south to a meadow with an abandoned swing set. A sleepy mountain with a face watches from the south horizon. Old robot heads lie overgrown around the arena, and the poster column has "wanted" posters of the Grinnies. The story is told through objects, not text.

**Cover (gameplay positions unchanged):** giant mushroom, swirl tree (owl in the knot), mushroom cottage, camp tent + campfire, stump house, kiosk shop, fallen robot head (flower growing from its eye), teapot house, boulders, mushroom cluster, poster column, boulders with signpost.

**Characters, "Grinnies":** tangerine egg-heads on long plum legs, with striped socks, chunky shoes, noodle arms with mittens, belly patch, toothy grin and angry brows. Variety comes from hats (beanie, party cone, leaf sprout, horns), mouths and a cyclops variant, never from colour. They pop in, squash and stretch as they walk, blink, flail their arms when close, recoil when hit, and burst into stars on KO.

**Player:** blue toy star-blaster (cream body, gold rings, goo bubble), white cartoon mitten, blue sleeve. It has walk bob, look sway, recoil and a star-shaped muzzle flash.

**Visual hierarchy:** player (blue) → enemies (tangerine, ink outline, rim light) → objective (gold star, glow) → cover (soft line) → environment (muted, no line) → backdrop (pre-hazed, no fog).

**Palette** (`P` in the script, CSS vars in `:root`):
- Environment: grass `#a9cc7e`, haze `#f3d9cc`, sky `#9fd0ea`, cream `#fff1d6`, dusty pink `#eba3b4`, lavender `#b9a6dc`, teal `#72c0b6`, butter `#f3d98a`, wood `#b27e5c`, stone `#cfc3cc`.
- Accents with meaning: **tangerine `#ff7a2c` = enemies only**, **gold `#ffc53d` = objective only**, **blue `#2f9be0` = player**, coral `#f0604c` = damage/low HP, ink `#2a1830` = outlines/UI.

**Rendering techniques:**
- `MeshToonMaterial` with a 4-step *tinted* ramp: shadows are lavender, never grey.
- A shader patch (`patch()`) adds: contact shading near the ground, warm rim light, painted surface variation chosen per vertex by `aKind` (0 smooth, 1 plaster, 2 stone, 3 wood, 4 foliage), and wind sway for grass, flowers and canopies.
- Constant-width outlines (normal extrusion, `olMat`) applied selectively; see CLAUDE.md.
- Soft shapes everywhere: `rbox` (superellipsoid), `lathe`, `bend`, `lumpy`, `flatBottom`.
- A hand-painted 2048² ground map (meadow blotches, brush strokes, dirt paths) plus a hi-res plaza decal; merged blob contact shadows.

**UI rules:** thick 4–5 px ink borders, hard drop shadow (`0 5–7px 0 ink`), pill shapes, Fredoka font. The thumbstick knob is a cartoon eye on purpose. FIRE is player-blue. Overlays are see-through so the living world shows behind them; the intro slowly pans the camera.

Earlier directions (pastel low-poly, then sticker robots + 3 reference images) were superseded. The user once liked a mud/grass ground; it could return as an alternate theme.

## Code map (`index.html`)

Three `<script>` blocks that share globals, in this order:

0. Utilities: seeded `rnd`/`rr`/`pick` (the world is identical on every load) and the palette `P`
1. Renderer, main camera `C`, gun scene `GS`/`GC`, sky dome, sun, haze, lights, `rs()` (resize, gun placement, pixel ratio)
2. Materials: tinted `GRAD` ramp, `patch()`, `toon()`, outline `olMat`/`ol`, bucket materials `MAT` (t static, d double-sided, f foliage/wind, g glow, b/c backdrop/clouds)
3. Shape kit: `M()` matrix helper, `B` merge builder (vertex colours + `aKind`, per-triangle colour functions), `rbox`, `lathe`, `bend`, `lumpy`
4. Ground: `PATHS`, `pathD()`, painted ground texture, plaza decal
5. Cover builders (`mushroomHouse`, `teapotHouse`, `kiosk`, `posterColumn`, `fallenRobot`, `boulders`, `giantMushroom`, `swirlTree`, `stumpHouse`, `tent`, `campfire`), the `COVER` layout loop (`obs`, `obsM`), Wishing Star `cr`, `push()`
6. Wider world: tree types, fence + gates + hedges, north village + lighthouse, forest sectors, east field + windmill + giant robot, south meadow + mountains, merged shadows, `instGrid` grass/flowers
7. Ambient life: clouds, islands, birds, butterflies, smoke (`smokeAt` emitters), bunting, pollen, critters. Everything that moves registers in `anim[]`.
8. Player rig: `gun` → `rig` (blaster, glove, sleeve), `goo`, `fl` muzzle flash
9. Enemies: cached geometry `EG` (legs, arms, body, eye/face variants), `mkEnemy()`, `spawnWave()`, `setHp()`
10. FX pool (`fx`, `burst`, `stepFx`), `shoot()`, controls, `reset()`
11. `loop()`: gameplay block (unchanged), enemy visual layer, KO `dying` list, pollen, gun bob/sway/recoil, two-pass render, adaptive pixel ratio

Everything is still global, with no modules or state object. Splitting it up is roadmap item 2.

## Constraints and gotchas

- **three.js is r128 via cdnjs UMD.** Several APIs differ from modern three (`LuminanceFormat`, no `outputEncoding` changes, `CapsuleGeometry` unavailable). Check before upgrading; when migrating to npm `three`, expect to touch the toon gradient map, colour management and lighting intensities.
- The chat's publishing sandbox only allowed scripts from cdnjs.cloudflare.com and Google Fonts. Not a constraint for Claude Code, but it explains the single-file shape and the absence of image assets (everything is procedural).
- **Raycasting is non-recursive:** only meshes listed in `obsM` and each enemy's meshes are hit-tested. The outline children are deliberately excluded. Add new hittable parts to those arrays.
- Enemy hit flash uses `material.emissive`; keep materials per-mesh (not shared) for anything that can flash.
- Cover is one merged mesh per bucket per object; all of a cover's meshes (including posters and signs) are in `obsM`, so bullets stop on the visible shape. Foliage canopies are hittable too.
- The gun is drawn in a second pass (`GS`, after `clearDepth`), so it never clips into walls. It is not in the world scene.
- Instanced scatter must go through `instGrid` (or set `frustumCulled=false`): r128 culls `InstancedMesh` by its base geometry only.
- The browser pane / background tabs pause `requestAnimationFrame`. Measure performance with manual `R.render` calls or on a visible tab.
- Touch handling uses pointer capture per control; the look layer sits under the stick and fire button.

## Known issues / unverified

- **Never run on a real phone.** Desktop GPU renders a frame in ~1.6 ms; typical views are 85–215 draw calls and 190–370k triangles. Each enemy adds about 14 draw calls, so wave 10 (22 enemies) adds about 300. If phones struggle, the adaptive pixel ratio kicks in first; next steps would be fewer outlined enemy parts or merging legs/arms.
- **Hit-shape changes (visual, not numbers):** cover silhouettes now match the new art instead of boxes (e.g. you can shoot past a mushroom stem under its cap). The star plinth and lanterns now block shots below the floating star (they sit inside the star's existing collision circle). Enemies grow in over ~0.4 s when they spawn. KO'd enemies play a 0.22 s squash after they've already been removed from play.
- In portrait the blaster sits partly behind the FIRE button (it's scaled down for portrait, but still overlaps).
- Ground texture is 2048² over 170 units, so it's soft up close (the plaza has its own hi-res decal).
- No pause, no landscape-specific layout.
- **Sound** is pure WebAudio (section 12, object `A`): a looping 16-bar whistle + acoustic-strum song (Karplus-Strong guitar, G major, 104 bpm), footsteps per surface (grass/dirt/cobble), blaster "pew", hit/KO chimes, and a cartoon "oof" when the player is hurt (throttled to one per 0.15 s). It starts on the first tap or keypress (browser autoplay rules) and pauses when the tab is hidden. The mute button / M key choice is saved in `localStorage`. On iPhone, the hardware silent switch mutes WebAudio. Not yet heard on a real phone.
- Enemies can stack on one another and cluster; there is no separation steering.
- The start overlay is the only place the controls are explained.

## Roadmap (suggested order)

1. **Verify and fix.** Run on a phone and desktop, fix whatever breaks, and profile.
2. **Project structure.** Vite + npm `three`; split into `src/{scene,materials,enemies,player,input,ui,game}.ts`; one `GameState` object instead of globals; add lint and typecheck.
3. **Feel.** ~~Hit sparks, enemy hit-stagger, squash on death (pop into stars), better recoil~~ (done in the visual overhaul). Remaining: damage numbers, screen shake.
4. **Audio.** ~~Music, footsteps, shoot, hit, KO~~ (done). Remaining: wave-start sting, a game-over jingle.
5. **Content.** Second enemy type (fast runner), a boss every 5th wave, health pickups (gold stars), a second weapon.
6. **Meta.** Best-wave score in `localStorage`, pause menu, settings (look sensitivity, left-handed layout).
7. **Style pass.** ~~World/character/weapon art direction~~ (done). Remaining: alternate arena themes (e.g. mud/grass, dusk lighting), more Grinnie variants, a second enemy species designed in the same family.
8. **Ship.** PWA manifest and offline cache, deploy to Netlify or GitHub Pages.

## Suggested first prompts for Claude Code

1. "Read HANDOFF.md and CLAUDE.md, run `index.html` locally, and list anything broken or janky before changing code."
2. "Migrate to Vite with npm three, keep the game behaving identically, and split the file per the code map."
3. "Add hit sparks, screen shake and a star-burst on enemy KO, keeping the cartoon style."

## Definition of done for any change

- Plays correctly on a phone-sized viewport with touch controls.
- Holds roughly 60 fps on a mid-range phone.
- Matches the art direction above (selective outlines, tinted toon shading, colour = meaning, sticker UI).
