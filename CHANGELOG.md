# Changelog

## v2.1.1 — Endgame Hall Dungeon Fix, Multiplayer Hardening & Granular Auto-Yield

Pure-performance update closing a major Endgame Hall dungeon-loading gap, hardening multiplayer Hall runs across listen servers and split-world groups, and making Hall Auto-Yield granular—with zero gameplay changes and zero new config toggles.

- **Fixed Vanilla Sky-Interior Dungeons Loading Beneath Halls:** Swamp Sunken Crypts, Burial Chambers, Troll Caves, Frost Caves, and Infested Mines float high in the sky alongside Endgame Halls, which previously slipped past the surface-height check. Endgame Hall protection now defers any off-altitude dungeon while you are inside a Hall and resumes it smoothly when you leave.
- **Multiplayer Host & Wide-Party Hardening:** Fixed an edge case where a host inside an Endgame Hall could defer unexplored overworld locations for teammates exploring elsewhere on the map, and hardened Hall detection so protection stays engaged when groups spread across large Hall Maps or run lower simulation distances.
- **Granular Hall Auto-Yield & ValheimAVX Compatibility:** Split Endgame Hall protection into independent dungeon, spawn, and biome guards under the existing Hall guard toggle—so an overlap with creature or spawn-control mods only yields surface spawn suppression while keeping dungeon deferral and the Hall biome guard active. Also lifted the blanket ValheimAVX skip on Path of Valheiman-specific Hall guards so Auto-Yield handles only real overlaps.
- **Multiplayer Tip:** When running an Endgame Hall together in co-op, all players entering the Hall should have this mod installed so no unmodded teammate who owns a nearby zone triggers surface creature spawns beneath the Hall.


---


## v2.1.0 — Valheim `1.0.31` Support, Automatic Mod-Overlap Safety & Hall/Inventory Smoothness

Pure-performance release bringing automatic feature-level mod-overlap protection, a clear Main Menu status line, a universal Endgame Hall biome guard, and smoother first-time Equipment & Gem UI opening—with zero gameplay changes and zero runtime overhead during play.


### Automatic Mod-Overlap Safety & Clear Main Menu Status

- **Automatic Mod-Overlap Safety (`Auto-Yield on Mod Overlap`):** Enabled by default in **01. General** right beside **Allow Untested Versions**. Runs a single lightweight check once on the Main Menu after all mods finish loading (zero overhead during gameplay). If another installed mod behaviorally overlaps with a specific boost, only that overlapping feature steps aside cleanly while everything else keeps running—pausing the entire mod only if a core lifecycle system conflicts.
- **Clear Main Menu Status Line:** Prints one status line near the bottom of the BepInEx console (mirrored once to `BepInEx/LogOutput.log`) on Main Menu load so you can confirm at a glance that everything is active—or see exactly which feature stepped aside and why.


### Universal Endgame Hall Biome Guard

- **Eliminated Overworld Biome Noise Inside Halls:** Stops Valheim from running once-per-second surface biome checks while you are inside elevated Endgame Halls—eliminating repeated biome warning log spam, false overworld biome banners (such as "Ocean"), background music flickering, and unnecessary surface biome pre-warming across all biome boundaries. Resumes normal overworld biome detection immediately upon leaving the Hall.


### Smoother First-Time Inventory & Equipment Opening

- **Faster First Inventory Open:** Moves Path of Valheiman's Equipment and Gem UI code warmup onto the background Main Menu startup thread and gently pre-warms static slot icons and gem graphics one step per quiet frame after spawn—automatically standing down whenever an external equipment UI mod is hosting equipment slots.


---


## v2.0.0 — Valheim `1.0.30` & Path of Valheiman `6.0.16`

Large pure-performance update bringing smoother exploration, faster Passive Tree & Jewel browsing, steadier Monoliths and Endgame Halls, and full Valheim `1.0.30` / Path of Valheiman `6.0.16` support—with zero changes to gameplay, balance, or loot.

### Built for Valheim `1.0.30` & Upgraded Diagnostics

- **Valheim `1.0.30` & Path of Valheiman `6.0.16` Ready:** Verified across live game and mod updates, aligned cleanly with `1.0.30`'s background memory cleanup, and skips unnecessary Deep North snow checks in other biomes.
- **Vanilla Stability Cleanups:** Silences universal Deep North missing-texture log spam with no visual change and hardens Plains shield-effect cleanup.
- **Upgraded Opt-In Diagnostics:** Expanded Valheim `1.0.30` release-build stutter logging with clearer frame breakdowns and exit summaries—Off by default with zero overhead.

### Smoother Passive Tree & Jewel UI

- **Fluid Tree & Jewel Browsing:** Separates animated overlays and Jewel layers from the main tree so hovering, zooming, and socketing Jewels no longer redraw the entire tree.
- **Faster Repeat Opens:** Significantly reduces idle open-tree hitches, speeds up repeat opens, and prevents mid-session menu cleanup pauses—with zero cost while closed.

### Smoother Monoliths & Sieges (All Biomes)

- **Lighter Activation & Early Waves:** Prepares Monolith dome visuals and your current biome's runic guardians gradually during calm moments before combat starts.
- **Smoother Arena Clearing & Idols:** Spreads Monolith arena obstacle clearing across frames and batches idol placement updates cleanly with identical physics and layout.
- **Siege-Time World Protection:** Holds distant off-screen dungeon loads and far-away unexplored zones until your active Monolith siege finishes, while keeping your immediate area and multiplayer teammates' areas loading normally.

### Smoother Endgame Halls

- **Distant-Room Visual Culling**
  - *Problem:* In large multi-room Halls, the game keeps drawing distant rooms far down the dungeon even when they are completely blocked by stone walls. As you push deeper into a run, rendering dozens of unseen rooms at once can cause heavy, sustained framerate drops during big fights.
  - *Solution:* Temporarily hides visuals on far-away rooms (well beyond your current room and connecting corridors, so nothing pops in) and restores them smoothly as you approach. All room layouts, collisions, enemies, and loot stay completely untouched while delivering noticeably steadier framerates across long runs.
- **Stopped Wasted Overworld Activity Beneath Halls**
  - *Problem:* Endgame Halls float high in the sky, yet Valheim's surface spawner and world loader only check your horizontal map position—not your height. While you fight inside a Hall, the game keeps spawning overworld creatures, loading surface dungeons, and building terrain far below you in areas you cannot even reach.
  - *Solution:* Pauses surface creature spawns, surface dungeon reloads, and overworld churn directly beneath sky-high Halls while you are inside—staying multiplayer-safe so teammates on the surface continue playing with normal spawns and world loading.
- **Cleaner Hall Launches, Saves & Gate Audio**
  - *Problem:* Launching a Hall map right after packing it can trigger overlapping world saves that stall entry, mid-fight progress saves can hitch intense rooms, and inactive Hall gates repeatedly log harmless audio warnings in the background.
  - *Solution:* Waits for any active pack save to finish before starting the launch save, holds non-critical progress saves until combat rooms settle (always saving immediately on death, logout, or exit), and silences disabled Hall gate audio spam.

### Exploration Pacing

- **Steadier World Exploration:** Spaces out heavy unexplored dungeon, village, and fortress loading while keeping the ground around you responsive.
- **Smoother Background Dungeons:** Loads distant dungeon rooms gradually across frames, adding brief breathing room after large Deep North halls to reduce back-to-back hitches while still finishing immediately when you approach.
- **Zone-Border Stability:** Keeps nearby loaded crypts, caves, and fortresses steady when fighting across zone borders instead of repeatedly unloading and reloading them.

### Universal Combat Pre-Warming (Load-Time Friendly)

- **Automatic Gear & Summon Support:** Automatically discovers Path of Valheiman's live weapons, summoning staves, essences, bombs, and unique gear—warming equipped items and hotbar gear quietly with no hardcoded lists.
- **Built to Protect Load Times:** Breaks preparation into small calm-frame steps scoped only to your active gear and current biome to affect load times as little as possible in exchange for smoother gameplay.

### ValheimAVX Status Notice

- **Temporarily Stepping Away from ValheimAVX Co-op Features: Active ValheimAVX cooperation toggles are temporarily paused in v2.0.0 (the config category remains visible, with a status note).**

---

## v1.0.0

- Initial standalone public release for Valheim `1.0.21` and Path of Valheiman `6.0.10 – 6.0.15`.
- Added background main-menu code warmup and quiet-frame pre-warming for equipped gear, current-biome enemies, loot drops, lighting, weather shifts, altars, and short sound effects.
- Added build-aware combat skipping for unused skills and weapons, multi-shot stat reuse, and a cosmetic-only overlapping hit-effect limiter.
- Added faster Passive & Craft Tree toggling, minimap spike protection, out-of-combat save pacing, timer spreading, and solo network stand-down.
- Added FPS-adaptive world object loading, solo alternating load/cleanup frames, smart water/shoreline refresh, optional ValheimAVX cooperation toggles (Off by default), and opt-in stutter loggers.
