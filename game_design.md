# HELLO WORLD 091 — Game Design

> Living design reference. Last updated 2026-10-31. Describes the implemented prototype, not an aspirational feature list.

## Identity and purpose

**Hello World 091** is a compact, browser-playable, first-person retro sci-fi horror shooter within the **NULLRELAY** fiction. Its in-world process number is **091** (not process_001). Play: https://4rg43n.github.io/hello-world-game/ .

**Mood:** original *System Shock* / 1990s industrial sci-fi horror: claustrophobic station corridors, machinery and flesh fused together, mechanical unease, deliberate pixel art. The enemy should seem produced by the station, not pasted into it. The soundscape should be industrial and threatening, never cheerful arcade “beep boop.”

## Current playable loop

- Player explores a fixed **16 × 16** corridor map in first person, with a pistol and minimap.
- **One** Reclaimed enemy is active at a time. It spawns at a valid map corner, approaches the player, and deals melee damage.
- Player shoots the enemy; it takes **two hits** to kill. The kill counter increments once.
- After a lethal hit, the enemy **remains visible for 260 ms** in a hit/death flash, cannot move/attack/be hit, then despawns. **Five seconds after despawn**, another enemy spawns. Repeat indefinitely.
- Player begins at **100 health**; Reclaimed attacks subtract **10 health**, with a **900 ms** attack interval when within range and with line of sight.
- At zero health: game over, total kills, restart.

## Movement and combat

- Keyboard: **W / ↑** forward; **S / ↓** backward; **A / D** strafe; **Q / E or ← / →** turn; **Space** fire.
- Touch: on-screen six-button movement/turn cluster and FIRE; hold controls for continuous movement/shooting.
- **Double tap backward** (touch ▼ or keyboard S/↓, within **320 ms**) to instantly turn **180°**. Normal single press still moves backward.
- Player speed ~**2.8 map units/s**; turn speed ~**2.3 rad/s**; collision checks prevent moving through walls.
- Weapon fire cooldown **300 ms**; aim based on target angular width plus unobstructed line of sight. No ammunition or reloading system at present.
- Shooting adds muzzle flash, recoil, screen shake; successful hits add magenta hit marker and Reclaimed flash. Gentle weapon bob while walking.

## The Reclaimed (asset 091-R)

A damaged station worker/security-machine hybrid: exposed flesh, metal armor/implants, corrupted magenta eye. Not an insect or generic monster. The sprite is a procedural **32 × 64** pixel image with two motion frames. Enemy movement ~**1.05 units/s**; proximity and line of sight govern melee attacks. Its death is deliberately a **state transition**, not immediate removal.

## Environment and presentation

- Rendered at **320 × 200** internal resolution and scaled pixel-sharp to the viewport.
- Software raycast walls, depth-tested enemy billboard, perspective-correct tiled floor and ceiling.
- Industrial panel textures, grates, recessed cyan ceiling lights, flickering cyan/magenta wall details.
- **Localized biomechanical infestation** on selected wall panels and nearby floor/ceiling tiles: dark sinew, tissue, embedded magenta nodes. Keep unaffected sections for contrast. Corruption changes appearance **without changing collision or map topology**.
- NULLRELAY-themed angular HUD with health, kills, enemy/signal state; **minimap in upper right** to avoid HUD text at upper left.
- Palette: dark steel blues/charcoal, cold cyan technology, magenta corruption, restrained blood-red/brown tissue. Avoid glossy generic UI.

## Audio direction and implemented sounds

All sounds are **procedural Web Audio**, no downloaded samples:
- Continuous, low industrial station hum (keep this).
- Metallic footsteps; punchy pistol, hit, kill, and player damage sounds.
- Reclaimed breathing: **soft, low bandpass-filtered grinding whoosh**, not a cartoon jump. Audible within ~**8 tiles**; volume increases nonlinearly as it approaches (current mix includes a **10% boost**), stereo pan depends on angle relative to player. Breathing becomes somewhat more frequent nearby.
- Spawn: **~1.2 s rough scraping metal**, irregular clanks, and a heavy final impact, as if crawling out of ductwork or sharp debris. No melodic or electronic spawn chirps.
- Occasional faint interference/static.
- iOS/iPad audio must be initiated/resumed from user interaction. HUD includes SND ON test tone and MUTE control. Preserve Safari compatibility.

## Technical implementation

Single-file static web app: **`index.html`** contains HTML, CSS, JavaScript, textures, sprites, renderer, logic, and audio. No framework/build process. Hosted by GitHub Pages from repository **`4rg43n/hello-world-game`**.

Important source landmarks:
- `map`, `wall`, `solid`, `infestation`, `corruptedTile`: map/collision/corruption.
- `makeTexture`, `makeInfestedTexture`, `makeSurface`, `makeOrganicSurface`: procedural textures.
- `drawSurfaces`, `rayDistance`, `render`: floor casting, wall raycasting, billboard, HUD.
- `makeGuard`, `reclaimedFrames`: Reclaimed sprite/animation.
- `initializeAudio`, `tone`, `noise`, `sound`: Web Audio.
- `spawnEnemy`, `shoot`, `update`, `reset`, `loop`: gameplay.

## Established priorities

1. **Atmosphere first:** claustrophobia, physical machinery, encroaching biological corruption.
2. **Clear feedback:** damage, hit flash, death, sound, and respawn order must remain reliable.
3. **Playability on iPad/touch and desktop:** responsive controls, readable HUD, correct Web Audio unlock.
4. **Incremental changes:** prefer small, testable improvements; avoid overbuilding a prototype.
5. **Respect approved audio mix:** the station hum and subdued breathing were tuned deliberately; do not casually replace them.

## Possible future work (not implemented)

Wall-occluded/muffled positional audio; richer death animation; bulkhead doors/sector markings; environmental storytelling; further links to NULLRELAY terminal fiction. These are ideas, **not current features or commitments**.
