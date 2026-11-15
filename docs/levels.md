# Math Ninja notes: Worlds, the level builder, drawing, home screen

Part of the code notes; `CLAUDE.md` has the index. Search `index.html` for the names in backticks (line numbers drift).

## Worlds (6: japan, lava, robot, snow, sea, castle)

`const WORLDS` (skies, colours, intro text, boss, `slot`). **The sea world was put in before the castle (Nov 2026)**, so world 4 = sea, 5 = castle. Per-level lists (`TWISTS`, `ENTRANCES`, `ANIMALS`, `MOVES`, `FLAVORS`, wall kinds, bridge parity) are indexed by `slotOf(def)` = `WORLDS[w].slot + k`: the old 15 levels keep 0–14 (castle 12–14), the sea is 15–17 (filled since Nov 14 2026: animals, entrances, moves, twists, flavours). Stages have `si` (their original number: castle 16–19, sea 20–23) used for level seeds and speed, so castle layouts didn't change. Never index a list by `w * 3 + k` or a 5-long array by world

## Stages (24 = 6 worlds × 3 levels + boss)

`const STAGES`, `PER_WORLD`, `bossOf`; level index within world is `L.def.k` (0–2, boss 3)

## Level builder

`function buildLevel`, `chunk(type)`, `twistChunk`, `bridgeChunk`, `doorChunk`, `stepsChunk`, `run()`, `sky(c)`; per gate loop: animal (only at `feedAt`, the middle gate), chunks, bridge, door, stepping stones, twist, gate station. **Bridges and stepping stones take turns** (owner): `useBridge` = level index (world × 3 + level) odd, so stones in 8 levels, bridges (1–2) in 7; **kindergarten math (`skill.tier === 1`) never gets bridges**, stones every level (they already count by 1s/2s). **Breathing room** (owner wanted a lot more plain running): `run()` = 14–18 tiles of flat ground after the animal, the stones, each bridge and a pattern wall; the first two runs get `sky(c)`: two 3-block ledges of `S` (rows GR−4 and GR−7) with gems on top, reachable with a held jump. Math per level dropped to ~15 (K) / ~16 (3rd); add a gate if the owner wants more

## Polar bear ninjas (owner, Nov 10 2026: the snow world was all penguins)

Blizzard Peak's walkers are `bear` (`walker` in `buildLevel`: snow and `def.k === 2`), size 38 × 41 in `walkerFor`, drawn 1.2× in `drawEnemy` case `'bear'` (owner: a bit bigger): creamy white with a grey-blue outline so it shows on snow, red ninja headband with flying tails. Yuki's rescue guard is still the penguin bouncer

## Per-level twists (kite, spring, koi, rocks, chase, dark, gears, conveyor, lasers, ice, icicles, avalanche, walljump, ladders, sneak)

`const TWISTS`, `TWIST_HINT`, `updateTwist`, `twistMove`, `drawTwist`

## Per-level flavour (one extra thing per level, fits its name: cherry trees to shake, bamboo, frogs + dragonflies, ash vents that puff Kai up, lava bubbles, glow mushrooms, steam pipes + cogs, crate belt, lab flasks + screens, snowmen with hats (Frosty Slopes: owner asked for far fewer, every 3rd spot, each with its own scarf colour `f.sc`; bump one and its hat pops off with a gem), ice chimes playing Amazing Grace, wind gusts, lantern platforms, owls, bats + torches)

`const FLAVORS`, `addFlavor` (own rng seed, so layouts don't change), `updateFlavor`, `drawFlavorSky/Back/Front`, `drawFlavor`, `CHIME_TUNE`; lantern platforms live in `L.plats`

## Level backgrounds

Each world shares one base background (the original look); levels add one small touch keyed on `L.def.k` inside `bgJapan/bgRobot/bgSnow/bgLava/bgCastle`: Japan cherry trees / bamboo / lake strip + torii; robot gears / low crate shelf / blue tint; snow sunny / northern lights / grey + blowing snow; lava ash clouds / glowing rock cracks / (dark cave); castle lanterns on ropes roof to roof / huge moon (only Moon Tower has a moon) / low wall with banners + torches. Bosses use the base. Castle decor: stone lanterns only on Lantern Roofs, potted pines elsewhere

## ? box surprises / power-ups

`BOX_PRIZES`, `boxPrize(c, r, asked)`, `const POWERS`, `fiery()`; end of `buildLevel` evens out ? boxes to 3–6 per level by world

## Player physics

`updatePlayer` (calls `updateTwist`, `updateFlavor`, `updateMini`, `updateSteps`; returns early while `G.cross`), `moveX`, `moveY`, `SOLID`

## Drawing

`render()` order: background → `drawFlavorSky` → decor → `drawFlavorBack` → tiles → `drawTwist` → `drawFlavor` → `drawSteps` → `drawMini` → coins, enemies, player → `drawTwistFront`, `drawFlavorFront`; darkness holes in `drawDarkness`

## Text on screen

`floatText` (life scales with text length), pet bubbles `petSay` (160 frames), `senseiTip` (owner: was too big at key moments; now a small card top-left under the hearts, `TIP_T` 6 s, `drawTip` sets `G.tip.box`; tap it (✕) to close, and `gotIt` closes it after the next right answer), HUD `drawHUD`

## Home screen / map

`buildMenu`, `worldScene`, `drawMenuBackdrop`, `#menu` HTML. Top row (owner, Nov 11 2026: less cluttered): Race, Shop, Badges, Gear, Settings; the **Fact Book** button is at the bottom of the Badge Book (`#factBtn`) and **How to play** is in Settings (`#helpBtn`)

## Carried scroll

`drawCarriedScroll` (drawn right after Kai in `render`, so the house never covers the scroll he carries home); `drawGoal` only draws it while it waits on its holder
