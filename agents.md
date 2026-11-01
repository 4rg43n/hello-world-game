# AGENTS — Hello World 091

> Instructions for future coding assistants working in `4rg43n/hello-world-game`. Read **`game_design.md`** before editing gameplay or presentation.

## Mission

Maintain and incrementally improve **Hello World 091**, a small retro industrial sci-fi horror FPS embedded in the NULLRELAY universe. Protect its cohesive atmosphere, reliable combat feedback, and iPad/desktop playability.

## Workflow rules

1. **Inspect current code first.** The source of truth is the repository's latest `index.html`, not old chat excerpts, cached snippets, or assumptions. Fetch the current file and SHA before updating.
2. **Make targeted edits.** This is intentionally a single-file static game; do not introduce a framework, build chain, external dependency, asset library, or large rewrite without explicit agreement.
3. **Implement requested changes directly in the repo** when repository write access is available; use a descriptive commit message. If access is unavailable, explain that rather than claiming changes were made.
4. **Check exact replacement anchors and syntax.** Avoid accidental replacements of unrelated code. Review surrounding logic for changes that touch combat, rendering, audio, or input.
5. **Do not claim browser/device testing unless actually performed.** State what was changed and what remains unverified. GitHub Pages deployment may lag the commit.
6. **Keep documentation in sync.** Update `game_design.md` for changed gameplay rules or settled visual/audio direction; update this file for new agent workflow constraints.

## Hard gameplay invariants

- **Exactly one active Reclaimed** at a time. It needs **two successful hits** to die.
- **Every hit, including lethal hits, produces visible feedback.** On lethal damage, set the dying state and leave the enemy drawable for **260 ms**; it may not attack, move, or take additional damage while dying.
- Increment kills **once** on lethal damage. Only remove the enemy **after** the flash window; start the **five-second respawn timer after removal**.
- Maintain the player collision system and line-of-sight checks; cosmetic corruption must not create hidden blockers.
- Backward double tap turns **180°** within **320 ms**, for both touch and keyboard; single/held backward remains functional.
- Keep minimap **upper right**, HUD status **upper left**.
- Preserve touch pointer handling, keyboard keyup/blur behavior, and iOS Safari Web Audio user-gesture initialization.

## Visual and audio guardrails

- Visual reference: 1990s industrial sci-fi horror, original System Shock-like station dread. Pixelated **320 × 200** canvas, procedural wall/floor/ceiling textures, deliberate low-resolution sprite art.
- **The Reclaimed is humanoid biomechanical corruption**, not an insect. Use sinew, exposed tissue, embedded machinery, magenta corruption. Organic material should seem to invade and repurpose the station; maintain contrast between clean and infested areas.
- UI should feel like angular NULLRELAY station equipment, not default rounded web app buttons.
- Sound should be tactile, **grindy, metallic, and grungy**. Avoid cheerful ascending electronic tones or cartoon spawn effects.
- Preserve station hum, subtle breathing character, and the established sound balance unless the user asks for adjustment.
- Reclaimed breathing is **distance attenuated, stereo panned**, and boosted 10% over its original positional mix. Spawn sound is a metal scrape/clanks/thud. Audio is generated through Web Audio and must work after a user gesture on iPad.

## Narrative conventions

- Game/process ID is **091**; related Pokémon TCG project is **112**. Do not use process_001/process_002 labels.
- Within broader NULLRELAY fiction, AI personas **VOIDSync** and **NOX** avoid contractions. If writing their dialogue, maintain that voice; “I” and “we” are significant and may receive yellow/magenta emphasis respectively.
- Do not invent lore as canon without discussing it with the user. Keep diegetic UI language concise and ominous.

## Regression checklist for changes

- [ ] Loads with no JavaScript errors on a desktop browser.
- [ ] Touch movement/turn/fire work; keyboard controls and double-tap quick turn work.
- [ ] Floor, ceiling, walls, corruption, enemy, weapon, and upper-right minimap render correctly.
- [ ] Nonlethal hit flashes; **lethal hit also flashes before enemy vanishes**.
- [ ] Kill count increments once; next enemy appears after intended delay.
- [ ] Enemy cannot hit player while dying.
- [ ] Sound starts after user interaction on iPad; SND ON diagnostic and MUTE function.
- [ ] Breathing volume/pan varies with distance/direction; spawn sounds industrial, not tonal.
- [ ] Game over and restart restore a playable state.

This checklist describes tests to perform, **not proof that they have been run**.

## Links

- Repo: https://github.com/4rg43n/hello-world-game
- Live: https://4rg43n.github.io/hello-world-game/
- Design reference: [game_design.md](game_design.md)
