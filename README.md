# TIDEBOUND — The Last Tidekeeper

**make.fun bounty:** Make the best game (`best-game-01`)
**Prize:** $1,000 split top 10 — 1st $400, 2nd $200, 3rd $120, 4–10 $40 each
**Deadline:** 01:00 Thu 19 Nov 2026 (+07)
**Entry:** `game.html` — ONE self-contained HTML file. No external resources, no network calls, no build step. Open it in a desktop browser and play offline.

## Submission (to be done by the owner — NOT done here)
- Intended repo: **github.com/quanglyv/** (owner's GitHub is `quanglyv`)
- Payout wallet for USDC: **A7Vi7oZyDdw7xaoRfckwkyfxz1NT4XStrRC5Hs4Ea2Yp** (Solana)
- Submission normally needs: public GitHub repo + screenshots + this dossier + transcript via the make.fun kit (`node cli/makefun.mjs record/submit`). No repo was created, nothing was pushed, and no wallet was connected or signed in this build — this folder is the local product only.

## Concept
You are the last Tidekeeper of a moonlit bay. Ink-creatures rise from the deep to swallow its light. You have no sword — only your **tidal pulse**, a shockwave that shoves and shatters them. Creatures drop **pearls**; collecting them builds a **combo** that multiplies your score. Survive all **5 waves** and defeat the **Tide Leviathan** to wake the dawn.

Why it is original, not a clone: it is not Snake / Tetris / Flappy / a platformer. The core loop is *positioning + timed pulse + risk/reward pearl-chasing*: pulsing clears space but has a cooldown, so every pulse is a decision — clear now, or wait and let the combo grow? Between waves you draft **one of 3 tide-gifts**, so no two runs build the same keeper.

## Controls
- **Move:** WASD or arrow keys (mouse / touch-drag also steers)
- **Tidal pulse:** Space or click
- **Pause / resume:** P or the Pause button
- **Replay:** R or the Replay button · **Start:** Enter or the Start button
- **Sound on/off:** M or the Sound button (all sound is synthesised WebAudio — no audio files)
- **Upgrade choice:** click a card, or press 1 / 2 / 3

## Rules
- **Hearts:** 5 (a hit costs 1; the boss costs 2). Touching a creature hurts you; you are briefly invulnerable after a hit.
- **Enemies:** Drifters crawl at you · Darters lunge when close · Splitters burst into 2 minis · the Tide Leviathan (wave 5, 22 HP) charges and slams.
- **Pearls:** +10 base, multiplied by your combo (up to ×8) and by Greed upgrades. Combo grows as you gather pearls and fades if you stop.
- **Waves:** 5 waves, escalating numbers and speed. Clearing a wave gives +200 and a tide-gift draft.
- **Win:** defeat the Leviathan on wave 5. **Lose:** hearts reach 0.

## Tide-gifts (drafted between waves)
Deep Pulse (+1 damage, +25% radius) · Swift Current (+25% speed, faster cooldown) · Pearl Magnet (2.2× pickup range) · Thick Shell (+1 max heart, heal 2) · Twin Tide (every pulse fires twice) · Greed of the Deep (pearls ×2, longer combo).

## Depth & polish
- 5 distinct enemy behaviours, a boss with HP bar, escalating waves, 6 upgrade paths, combo economy, invulnerability frames, screen shake, particles, floating score text, parallax stars / light rays / bubbles / animated seabed.
- Synthesised sound effects (pulse, pearl chime that rises with combo, hits, wave horn).
- Start / Pause / Replay buttons, win and lose screens with final stats, and a How-to-play screen — all in the file.

## How to test locally
```bash
# just open it — no server needed
open game.html        # or double-click it in a browser
# headless check used during development (Playwright + system Chromium):
# load file://…/game.html, assert no console errors, click Start,
# move + pulse with keyboard, force wave-clear / win / lose via window.__tide
# test hooks, and screenshot menu / gameplay / win screens.
```
Screenshots in this folder (taken in headless Chrome during testing): `screenshot-menu.png`, `screenshot-gameplay.png`, `screenshot-upgrade.png`, `screenshot-lose.png`, `screenshot-win.png`.

## Test notes
- Headless Chromium (Playwright, system Chrome) — page loads with **0 console errors**.
- Start button starts wave 1 and spawns enemies; Space/click fires a pulse (cooldown ring shown); Pause freezes the game and Resume continues; Replay restarts from wave 1 with score reset.
- Win and lose paths were exercised via the `window.__tide` test hooks (`killAll()` + wave-clear, and `setHp(1)` + a hit) — both show the correct end screen with final stats.
- Known issues: none found in testing. The game is tuned for a ~2–3 minute run. On very small screens the canvas scales down; best played on desktop Chrome (as the bounty requires).
