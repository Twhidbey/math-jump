# Math Ninja notes: Worlds, the level builder, drawing, home screen

Part of the code notes; `CLAUDE.md` has the index. Search `index.html` for the names in backticks (line numbers drift).

## Worlds (7: japan, lava, robot, snow, sea, desert, castle)

`const WORLDS` (skies, colours, intro text, boss, `slot`). **The sea world was put in before the castle (Nov 2026)**, so world 4 = sea, 5 = castle. Per-level lists (`TWISTS`, `ENTRANCES`, `ANIMALS`, `MOVES`, `FLAVORS`, wall kinds, bridge parity) are indexed by `slotOf(def)` = `WORLDS[w].slot + k`: the old 15 levels keep 0–14 (castle 12–14), the sea is 15–17 (filled since Nov 14 2026: animals, entrances, moves, twists, flavours). Stages have `si` (their original number: castle 16–19, sea 20–23) used for level seeds and speed, so castle layouts didn't change. Never index a list by `w * 3 + k` or a 5-long array by world

## Red Rock Desert (world 5, added Nov 15 2026; **built as a preview, the owner checks it before it goes live**)

Owner asked for "a new world - maybe desert with utah national park kinda look to one of the levels". Key `desert`, slot 18–20, stages `si` 24–27, before the castle (castle is now world 6, stage numbers 24–27; `loadProg` layout 7 moves old saves: `best` / `golden` 20–23 → 24–27, `seenWorld[5]` → 6; `FRIENDS` Mei and the Paper Lantern moved to `w: 6`). Levels: **Arch Canyon** (stone arches), **Hoodoo Trail** (thin spires, sunset sky), **Slot Canyon** (tall striped walls, a strip of sky). One background, `bgDesert` (far mesas, banded buttes `butte`, low dunes; per level `rockArch`, `hoodoo`, the wavy slot walls); boss uses the base. Red rock look: `rockBands` / `rockBandsClip` (bands depend only on height, so tiles line up), used by pillars, gates (stacked slabs that tumble in red dust, `g.k === 'desert'`), the crumbling ledges and the scroll rock. Pit kind `canyon` (dark crack, `drawPits`). Enemies: `scorpion` ninja walkers, `snake` (rattlesnake) in Slot Canyon. Animals: roadrunner + bug, tortoise + cactus pear, coyote pup + bone. Twists: `crumble` (three `crumb` plats like steps, shake then drop after ~50 frames on them, grow back), `devil` (a dust devil wanders, lifts Kai to gems), `quicksand` (`sand` fx: `G.sandIn`, walking half speed, hop to go faster; no harm). Flavours: `arches` (run-under arch + a blue gem), `cactus` (flower pops off with a gem), `sunbeams`. Dojo: Canyon Dojo, entrances cave / crack / cave, moves Elbow Strike, Axe Kick, Tornado Kick. No home math kind (`WORLD_HOME` has no desert: level 1 takes the kind furthest behind), scroll "Scroll of Remembering". Level end: balanced rock / tall cactus (`HOLDERS`), an adobe house (`HOMES`). Music `SONGS.desert`; race track `desert` (Red Rock Road, also the ride in). Menu: `.z-desert`, pix `cactus`, `arch`. **One signature moment per level** (owner, Nov 16: wanted more variety between levels; asked for the swing on arches): Arch Canyon's swing ropes hang from two stone arches standing on the ledges (`look.rock` + `L.def.k === 0` in `drawSwings`; Hoodoo Trail's posts are thin rock spires, Slot Canyon's are plain wooden posts and a beam: owner wants hoodoos only in the hoodoo level); Hoodoo Trail's stepping stones are the **hoodoo hop** (`hop` in `drawSteps`: every stone is the cap of a banded spire, and the three choices are bands of one tall hoodoo that rises out of the canyon; the desert never gets number-stone bridges, `useBridge`). Time of day: morning with a low sun, sunset, shade, and the boss at night under stars (`W.skies[3]`, used by `buildArena`). **Slot Canyon light** (owner liked the beams, Nov 19; chose all but birds): more beams of different widths (`sunbeams`: `f.s`, every other `f.pour`) that slowly brighten and fade (`beamBr`, geometry `beamAt`), the walls glow warm around them, more dust motes, sand trickling from the rim (bright where it crosses a beam, a little pile below), a warm patch on the sand, Kai glows when he stands in one (`G.inBeam` → `G.lit`, `drawFlavorFront`), gems in a beam twinkle, and the canyon echoes (`L.echo`: `echoTone` for jumps, gems and right answers). Slot Canyon's swing is a **raft ride** down the canyon river (see `docs/crossings.md`). Lost friend **Suna** in Arch Canyon (see `docs/friends.md`). Tuning (Nov 16): quicksand is a little less slow (walking at 60%). Offered, not built: a rock that tips over into a bridge. `TEAM_V` 9 (stage numbers changed).

## Stages (28 = 7 worlds × 3 levels + boss)

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

## Ghost Kai demos (owner, Nov 23 2026: show, don't tell; later the same day: only for very special things, `DEMO_KEEP`: the number-stone bridge, wall jumps, the koi kite, hiding in barrels)

The first time a player meets a level feature, play waits while a see-through Kai does it once (`demoSpots` in `startStage`: the first twist (`L.twistAt`, set in `twistChunk`), swing, stepping stones, number-stone bridge; `demoPath` turns each one's layout into waypoints; `demoCheck` starts it 6 tiles before; `demoTick` replaces `updatePlayer` while `G.demo`; the camera follows the ghost and eases back (`G.camBack`); `drawDemo`). A tap or key skips it. Seen ones go in `prog.demos`; Settings > Show me again (`demoBtn`) clears them. No demo for rocks / chase / avalanche (they come at Kai) or the sea's twists yet. A new twist needs a `demoPath` case.

## Upright phones (review, Nov 23 2026)

`layout()`: in portrait `VW` is no longer always 540. It shrinks in whole tiles down to 432 on tall screens (`floor(540 * width / (height - 250) / T) * T`, clamped 432..540), so the picture is taller on the screen and up to 25% bigger; about 250 px stay free for the buttons. (A 390 x 780 phone gets 432; 390 x 664 gets 504; a short 375 x 553 keeps 540.) Everything already keys off `VW < 700` for "narrow". The band under the picture takes the colour of the picture's bottom-left pixel (`#wrap` background), so the ground carries on down the screen. **Never read pixels from the game's canvas in the frame loop:** the first version did (`getImageData` twice a second) and the owner reported the buttons dead on a portrait phone the same morning; reading a canvas makes iPhone Safari stop drawing it on the graphics chip, so the game crawls. Now one pixel is copied with `drawImage` to a 1 x 1 canvas of its own (`bandCv`) and read there, once per level / room / view change (`bandKey`), 40 ticks after the change. Not done: whole-pixel sprite scale (would need a 390-wide view, only 11 tiles: too little warning for small kids) and pixel-style touch buttons. The story card's buttons (`#msgBtns`) are sticky at the bottom of the card, so "Let's go!" is in view on short screens (it was below the fold on a brand-new save in landscape).

Band colour flash (owner saw it when a level first loads): `#wrap` now eases its colour (`transition: background-color .6s`), and the colour is sampled 12 ticks after a change and once more at 150 ticks (after any fade-in), instead of once at 40.

## Home screen slimmed (owner, Nov 23 2026: "a ton of buttons"; 19 controls down to 11, nothing removed)

`#menu` now: a title bar with a small cog (`#settingsBtn`, `.cogbtn`) in its corner; Play; the player chip, math chip and Daily Dojo; one row of five picture buttons (`.iconrow`, 5 columns): **Team** (the kids use it often, so it stays), Shop, Badges, Gear, **Story** (`#storyBtn`). **Race** (`#raceBtn`, used least) is a small pill (`.racechip`) beside Daily Dojo in the chip row (it was first put below the last world; the owner said it looked lost there). The seven scroll slots, World map and Kuro's journal are gone from the home screen: **Story** opens `openMap`, now titled "Story": the map, the lost friends, the scroll row (`#storyScrolls`: copies of the hidden `#scrollRow` buttons that forward the tap, so a won scroll still rereads that part of the story) and a "Kuro's journal n/8" button. `#scrollRow`, `#mapBtn`, `#journalBtn` stay in the page with class `hidden` because `buildMenu` still fills them.

Later the same day (owner: "kids never change their math level; is the belt the best use of space?"): the **math chip** (`#skillChip`) is hidden on the home screen; the skill picker is under Settings > Grown-ups > **Math level** (`#mathBtn` → `openSkills(toMenu)`), and the parent page still shows and suggests the math level. The **belt line** is gone: the belt is a small colour bar on the player's chip (`.chipbelt`, and Kai wears it), and `#rank` shows only the chosen title, hidden when there is none. Home screen: 10 controls; on a 390-wide phone the levels start 314 px down (510 this morning). A long player name is cut with "…" so Race and Daily Dojo stay on screen. **Bug fixed:** the new home Story button had been given `id="storyBtn"`, which Settings > "Read the story" already used, so that Settings button did nothing for a few hours; the home button is `#storyHomeBtn` now. Check for duplicate ids when adding a button (`grep -o 'id="[^"]*"' index.html | sort | uniq -d`).

