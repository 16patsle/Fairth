# Test Plan: 26.2 Verification

Confirms the updated pack (`update-26.2`) works on Java Edition 26.2, against the old pack (format 22, `master`) as the broken baseline. The 2026-07-21 session confirmed all predicted breakages on the old pack and all fixes on the new one (details in UPGRADE-PLAN.md log); this document keeps the setup and the still-open checks.

## Builds

```sh
RP=~/Library/Application\ Support/minecraft/resourcepacks
git archive --format=zip -o "$RP/Fairth-new.zip" update-26.2
git archive --format=zip -o "$RP/Fairth-old.zip" master   # only needed for baseline comparisons
```

Enable above Faithful 32x. `F3+T` reloads resources after swapping.

## Remaining checks (new pack @ 26.2)

Second pass 2026-07-21 confirmed: current vanilla strings ✓, creative tabs ✓, sliced GUI shows pack art ✓, LAN button = vanilla (override stripped, key removed), painting padding reverted.

- [ ] Villager trading screen after the result-slot shift (task 3)
- [ ] Leaves at max render distance (task 6, mipmap tuning)
- [ ] Still-vanilla by design until their tasks land: menu background (2), bundle UI (4)

## Reference: custom item give commands (26.2 syntax)

```
/give @s egg[custom_model_data={floats:[101]},custom_name="Blue Dragon Egg"] 1
/give @s egg[custom_model_data={floats:[102]},custom_name="Red Dragon Egg"] 1
/give @s egg[custom_model_data={floats:[103]},custom_name="Green Dragon Egg"] 1
/give @s ender_pearl[custom_model_data={floats:[201]},custom_name="Blue Eldunarí"] 1
/give @s ender_pearl[custom_model_data={floats:[202]},custom_name="Red Eldunarí"] 1
/give @s ender_pearl[custom_model_data={floats:[203]},custom_name="Green Eldunarí"] 1
/give @s gold_nugget[custom_model_data={floats:[10001]},custom_name="Gold Coin"] 1
/give @s gold_nugget[custom_model_data={floats:[10002]},custom_name="Silver Coin"] 1
/give @s paper[custom_model_data={floats:[10003]},custom_name="Roll of Bandages"] 1
/give @s snowball[custom_model_data={floats:[10004]},custom_name="Tomato"] 1
/give @s shears[custom_model_data={floats:[10005]},custom_name="Scissors"] 1
```

(1.20.6-era syntax for baseline tests: `[custom_model_data=101,custom_name='"Blue Dragon Egg"']`.)

## Regression spot-check list

Leaves / wheat stages / lily pads / sugar cane; torches (all variants); sand, soul sand, path blocks; wool; shulker colors; creeper banner; container GUIs; fonts (accented `é ü`, SGA, `⑤⑥⑦` logo glyphs); custom items above. All passed 2026-07-21.
