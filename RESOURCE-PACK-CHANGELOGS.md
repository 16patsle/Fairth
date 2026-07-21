# Resource Pack Changelog Notes (1.20.5 → 26.2)

Resource-pack-relevant changes per version, condensed from the official minecraft.net changelogs. Each entry notes the impact on this pack. Covers everything since format 22 (1.20.3/4), the pack's previous target.

## 1.20.5 / 1.20.6 (formats 23 → 32)

- **`gui/options_background.png` and `gui/light_dirt_background.png` removed**, replaced by `gui/menu_background.png`, `gui/menu_list_background.png`, `gui/inworld_menu_*` and header/footer separator textures.
- Map decoration icons split from `map_icons.png` into individual files under `textures/map/decorations/` (Mojang slicer tool available).
- TTF font provider defaults reworked; font variant filters added (`uniform`, `jp`).
- Wolf variant, armadillo, wolf armor, vault/trial textures added; various shader renames.
- *Pack impact: `options_background.png` is dead (listed in remaining work).*

## 1.21 / 1.21.1 (formats 33 → 34)

- New music disc assets; a few sound events renamed (ominous trial spawner); minor shader removals (`position_color_tex`, `glint_direct`, `armor_glint`).
- *Pack impact: none.*

## 1.21.2 / 1.21.3 (formats 35 → 42)

- **Equipment/armor textures moved and renamed** into `textures/entity/equipment/` subfolders (`<material>_layer_1` → `humanoid/<material>`, etc.); equipment model definitions introduced (`models/equipment/`).
- **Bundle sprites reworked:** `container/bundle/background`, `slot`, and `blocked_slot` sprites removed; new slot_background/progress-bar sprites. Bundle item got 16 colored variants.
- **Torch and Redstone-Torch-containing block models/UV updated**; Dragon Egg model/UV updated; Arrow/Bee Stinger texture maps updated.
- `light_emission` field added to block model elements (emissive layers); `broken` override property for all items.
- Tooltip background/frame and slot-highlight sprites became customizable; `stretch_inner` option for nine-slice sprites.
- Post-processing effect definitions moved (`shaders/post` → `post_effect/`) and heavily reformatted; core shader configs consolidated.
- **Deprecated translation strings are now removed/renamed automatically at startup** — packs using them must re-add manually (list in `assets/minecraft/lang/deprecated.json` in the game JAR).
- *Pack impact: confirms `textures/gui/container/bundle.png` is dead. The pack's custom torch models replace the updated vanilla ones — should be visually verified. Lang override should be checked against `deprecated.json`.*

## 1.21.4 (formats 43 → 46)

- **New data-driven item model format:** item info lives in `assets/<ns>/items/<item>.json`; the `overrides` section (including `custom_model_data` predicates) was removed from models. Tint sources, condition/select/range_dispatch model types, special model types introduced.
- **Empty slot sprites moved:** `textures/item/empty_armor_slot_<piece>.png` and `empty_slot_<tool>` → `textures/gui/sprites/container/slot/<piece>.png`. Loom, brewing stand, and horse slot sprites split from their container backgrounds.
- Block entities (banners, heads, beds, chests, conduits, decorated pots, shulker boxes, signs) now also render a normal block model on top.
- `models/equipment/` moved up to `equipment/`; Unifont 16.0.01.
- *Pack impact: the CMD override migration and the empty-armor-slot sprite moves — both now applied to the pack.*

## 1.21.5 (formats 47 → 55)

- `textures/misc/enchanted_glint_entity.png` renamed to `enchanted_glint_armor.png`.
- **New colormap `textures/colormap/dry_foliage.png`** for dry-foliage tinting.
- Per-mob spawn egg sprites replace the tinted generic pair; pig/cow/chicken temperature variants added and base textures renamed (`pig` → `temperate_pig`, etc.); sheep wool undercoat split out.
- Saddle textures moved/split into `entity/equipment/<mob>_saddle/saddle.png`.
- Item models can dispatch on component contents (`minecraft:component` select/condition properties).
- Shader program JSON definitions removed (GLSL still overridable); post-effect uniform format reworked.
- *Pack impact: pack overrides `colormap/grass.png` and `foliage.png` — a matching `dry_foliage.png` should be considered for visual consistency.*

## 1.21.6 (formats 56 → 63)

- Mob effect atlas removed — `textures/mob_effect/` sprites are now part of the GUI atlas.
- Panorama textures must all be equal size and square; `blur` texture parameter in `.png.mcmeta` now consistently respected.
- Block model element rotation freed from 22.5° steps (any angle −45…45).
- Waypoint styles (locator bar) added; several sound files moved from `entity/` to `mob/` folders.
- Core shader uniforms became uniform blocks; fog split into environmental and render-distance uniforms; Unifont 16.0.03.
- *Pack impact: none.*

## 1.21.7 / 1.21.8 (format 64)

- Format bump only; no resource-pack section in the changelog.
- *Pack impact: none.*

## 1.21.9 / 1.21.10 (formats 64.0 → 69.0)

- Pack formats adopted major.minor versioning; `min_format`/`max_format` fields introduced in `pack.mcmeta`.
- **`gui/container/villager.png`: result slot moved up by one pixel.**
- `chain` block/item sprites renamed to `iron_chain`; copper golem, shelf, copper-family sprites added; `environment/end_flash.png` added; new `on_shelf` display transform.
- OpenGL 3.3 required — all shaders bumped from version 150 to 330; full-screen passes reworked.
- *Pack impact: the pack ships `gui/container/villager2.png` — the changelog references `villager.png`, so the filename and slot position need verification/updating.*

## 1.21.11 (formats 70.0 → 75.0)

- **Items atlas split from the blocks atlas** (no mipmaps); all textures in an item model must come from one atlas, block models only from the blocks atlas.
- **New `.png.mcmeta` texture fields:** `mipmap_strategy` (`auto`/`mean`/`cutout`/`strict_cutout`/`dark_cutout`) and `alpha_cutoff_bias` — most cutout blocks became mipmapped.
- New celestials atlas: `environment/sun.png` and `moon_phases.png` moved/split into `textures/environment/celestial/` sprites.
- Glass, glass panes, and redstone dust now support translucent textures; still water/lava texture names hardcoded.
- Block models: rotation around multiple axes (x/y/z fields); blockstates: z rotation added.
- Sprite animations moved to GPU; leather horse armor split into base + overlay; Unifont 17.0.01.
- *Pack impact: the atlas split is why the pack now ships `atlases/items.json`. The pack's cutout textures (leaves, grass, wheat) may want explicit `mipmap_strategy` tuning — the repo previously carried a mipmapping fix.*

## 26.1 (formats 75.0 → 84.0)

- **Entity textures mass-renamed and reorganized:** variant prefixes became suffixes (`cold_cow.png` → `cow_cold.png`, same pattern for cat, chicken, pig, panda, llama, fox, frog, copper golem, projectiles), and loose files moved into per-entity subfolders (`entity/bat.png` → `entity/bat/bat.png`, `entity/banner_base.png` → `entity/banner/banner_base.png`, etc.).
- **Baby mobs got dedicated models and textures** for nearly all species, plus baby-sized armor textures (`entity/equipment/humanoid_baby/`) and new baby sound events.
- **Block model render passes are now auto-detected per sprite** (solid / cutout / translucent based on pixel content), with an optional `force_translucent` flag; non-string entries in a model's `textures` map are now rejected.
- **Item models:** all item model types gained a `transformation` field; special model types reworked (bed `part`, banner/sign `attachment`, chest `chest_type`; new `bell`, `book`, `end_cube` types).
- **Core shaders consolidated** (entity/item split, lightmap rework), with an explicit dev note that overriding core shaders is unsupported.
- `demo_background.png` removed; tripwire texture now alpha cutout.
- *Pack impact: none — `entity/shulker/*` and `entity/banner/creeper.png` keep their paths.*

## 26.2 (formats 84.0 → 88.0)

- **Beds, signs, and hanging signs now use regular block models** instead of built-in entity models. The special model types (`minecraft:bed`, `minecraft:standing_sign`, `minecraft:hanging_sign`) and the `minecraft:beds`/`minecraft:signs` atlases were removed; textures moved to per-block files under `textures/block/` (e.g. `<color>_bed_head_*.png`, `<wood_type>_sign.png`). Mojang provides an automated slicer tool for converting existing bed/sign textures.
- `block/quartz_pillar.png` and `block/purpur_pillar.png` renamed with an `_side` suffix.
- Text rendering core shaders consolidated into `core/text` and `core/text_background` (variants via shader defines).
- New content textures: sulfur cave blocks, sulfur cube entity, geyser/noxious gas particles, friends-list and pause-menu GUI sprites, per-wood-type sign edit screen backgrounds (`gui/sign/<wood_type>.png`).
- *Pack impact: none of the renamed/removed files are present. Any future bed, sign, or mob-variant retextures must follow the new layouts.*
