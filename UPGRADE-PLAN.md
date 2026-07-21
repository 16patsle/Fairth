# Upgrade Plan: Format 22 → 88 (Working Document)

Task tracker for the `update-26.2` branch. Status: `todo` / `in progress` / `done` / `blocked` / `decision needed`. Summary of applied changes: [PACK-FORMAT-UPDATE.md](PACK-FORMAT-UPDATE.md).

| # | Task | Status |
|---|------|--------|
| 0 | Foundation (mcmeta, blockstate, item defs, atlas, slot sprites, lang, arcaena lang fix) | done |
| 1 | Slice 1.20.2-era GUI sheets into sprites | done — QA pending |
| 2 | Recreate menu background | implemented — keep/revert is a project-leader call |
| 3 | Villager trading GUI | done — verified in-game |
| 4 | Remove dead files (bundle, particles, footprint) | decision needed |
| 5 | ~~dry_foliage colormap~~ | dropped — moot after colormap removal |
| 6 | `mipmap_strategy` tuning | todo |
| 7 | OptiFine CTM → Continuity | decision needed |
| 8 | In-game verification on 26.2 | done — trading screen pending under task 3 |
| 9 | Support range | done — 75–88 |
| 10 | Merge to master | todo |

## Open task notes

**2. Menu background** — implemented: the four post-1.20.5 tiles generated from the pack's `options_background.png` with the old engine's 25%/12.5% darkening baked in, restoring the classic dirt-style menus. **Project-leader decision:** keep this classic look, or revert to vanilla's modern translucent-black-over-blur style (= delete the four tiles).

**3. Villager GUI** — done and verified in-game 2026-07-21.

**4. Dead files** — `container/bundle.png` (bundle UI sprite-based since 1.20.2), `particle/particles.png` + `footprint.png` (unused since 1.14). Delete outright, or recreate modern equivalents? Project-leader call.

**6. Mipmap tuning** — 1.21.11 made most cutout blocks mipmapped; `.png.mcmeta` now supports `mipmap_strategy` / `alpha_cutoff_bias`. Test leaves/grass/wheat at max render distance; vanilla uses `dark_cutout` for leaves. Also pad `arcaena:block/framed_glass_pane_top` (4×32) — it drags the whole blocks atlas from mip 4 to 2 (log-confirmed).

**7. OptiFine CTM** — `optifine/ctm/` (16 wool colors + arcaena framed glass) is ignored by vanilla; OptiFine is unmaintained past 1.21. Continuity reads OptiFine-format files in place, so porting may be test-only. Port / keep / drop? Project-leader call.

**8. QA** — second pass 2026-07-21 evening: stale strings fixed ✓, creative tabs good ✓ (polish note: bottom selected tabs could account for the inventory's rounded corners), sliced GUI renders pack art ✓. LAN button shows vanilla text → `menu.shareToLan` override confirmed dead (removed from lang; alternative branding is a project-leader question). Painting edge-padding was visible → reverted, originals kept. Still open: villager trading screen (task 3).

## Log

- 2026-07-21 — Research: changelogs 1.20.5→26.2 compiled from official sources (RESOURCE-PACK-CHANGELOGS.md). Foundation work committed one commit per item.
- 2026-07-21 — In-game test session: all old-pack breakages and new-pack fixes confirmed on 26.2; `slot/shield` name verified; found + fixed arcaena lang JSON errors; Faithful's own mcmeta identified as the source of unrelated log errors.
- 2026-07-21 — `supported_formats` removed after 26.2 rejected it (pack showed incompatible); range set to 75–88; blocks-atlas registration dropped (duplicate-sprite warnings).
- 2026-07-21 — GUI sheets sliced (Mojang slicer v1.1.3 + manual corrections vs the 26.2 jar); creative tabs re-sliced at the correct 28px stride after the in-game leak report.
- 2026-07-21 — Texture audit vs vanilla + Faithful: stats sprites and colormaps removed (pixel-exact vanilla copies), three paintings padded, `accented.png` confirmed custom high-res (logo glyphs `⑤⑥⑦`) and kept. Lesson: small diffs on 2× canvases can be custom detail — verify with a downscale round-trip before removing.
- 2026-07-21 — History rewritten into clean commits authored as 16patsle; `reference/` lang backups scrubbed from history; branch renamed `update-26.2` and force-pushed to the fork.
- 2026-07-21 — Second in-game pass: tabs/strings/GUI confirmed good; LAN override confirmed stripped (key removed); painting padding reverted after visible artifacts (odd sizes are harmless in practice — no atlas warnings).
