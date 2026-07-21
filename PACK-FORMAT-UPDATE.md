# Resource Pack Format Update: 22 → 88

Updated the pack from format 22 (Minecraft 1.20.3/4) to format 88 (Java Edition 26.2), targeting formats 75–88 (1.21.11 → 26.2). Work lives on the `update-26.2` branch. Per-version changelog research: [RESOURCE-PACK-CHANGELOGS.md](RESOURCE-PACK-CHANGELOGS.md). Task tracking: [UPGRADE-PLAN.md](UPGRADE-PLAN.md). Testing: [TEST-PLAN.md](TEST-PLAN.md).

## Changes applied

- **`pack.mcmeta`** — new `min_format`/`max_format` fields (75/88); `supported_formats` dropped (rejected by the game for packs ≥65); `pack_format` kept for a clean incompatible marker on old clients.
- **`blockstates/grass.json` → `short_grass.json`** — 1.20.3 rename; the custom grass models had been silently broken ever since.
- **Custom-model-data items** — old model `overrides` (dead since 1.21.4) migrated to `assets/minecraft/items/` definitions using `range_dispatch`; same CMD thresholds, old integer values auto-migrate.
- **Atlas registration** — `textures/custom/` added to the items atlas (`atlases/items.json`); required since 1.19.3, items atlas split in 1.21.11.
- **Empty armor slot sprites** moved to `textures/gui/sprites/container/slot/` per 1.21.4 (incl. shield, verified in-game).
- **`lang/en_us.json` rebuilt** — was a full ~1.16 vanilla copy (4,812 keys, 193 dead, thousands of stale strings); now only the ~90 genuine customizations (Arcaena branding, `§f` white GUI titles incl. all 16 current creative tabs, `⑤⑥⑦` logo glyphs, banner pattern names + the new `.new` title key). Original file remains in `master` history.
- **`arcaena` lang file** — fixed 13 JSON syntax errors that made the game skip the whole file.
- **GUI sheets sliced into sprites** (dead since 1.20.2) via Mojang slicer + manual corrections against the 26.2 jar; creative tabs re-sliced at the correct 28px stride; `villager2.png` renamed to `villager.png`; 7 dead sheets deleted.
- **Redundancy audit vs vanilla 26.2 + Faithful 32x (all 358 textures)** — stats icon sprites and colormaps removed (pixel-exact vanilla copies); everything else confirmed custom (incl. the high-res `accented.png` font carrying the logo glyphs — do not remove). Three paintings have odd off-by-one sizes (63×63 etc.) but render fine; an edge-padding attempt was visible in-game and reverted.
- **`menu.shareToLan` override removed** — in-game testing confirmed the game's deprecated-key strip discards it on all supported versions, so the "arcaena.com" LAN-button branding no longer works via lang. If that branding matters, it needs a different mechanism (project-leader call).

- **Menu backgrounds recreated** — the four post-1.20.5 tiles generated from the pack's `options_background.png` with the old engine's darkening baked in; menus keep the classic pack look instead of vanilla's translucent black.
- **Villager trading GUI** — renamed to the current filename, trade sprites split, and the 1.21.9 one-pixel result-slot shift applied; verified in-game.

## Remaining

- Decision: menus — keep the recreated classic dirt-style background, or revert to vanilla's modern translucent style (delete the four new tiles).
- Decision: delete or recreate dead files (`container/bundle.png`, `particle/particles.png`, `particle/footprint.png`).
- `mipmap_strategy` tuning for cutout textures; pad `arcaena:block/framed_glass_pane_top` (4×32 drops the whole blocks atlas to mip 2).
- Decision: OptiFine CTM folders — port to Continuity (reads OptiFine format in place), keep, or drop.
- Art polish: bottom selected creative tabs could account for the inventory's rounded corners.
- Merge `update-26.2` to master.
