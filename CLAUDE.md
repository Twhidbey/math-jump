# Math Ninja: notes for Claude

A kids' math platformer. **Everything is in `index.html`** (~13,600 lines, about 1 MB: HTML, CSS and one big JS IIFE). No build step, no dependencies. `README.md` describes the game for people; this file is the short index of the code notes (the detail per area is in `docs/`, see Where things are). **Keep this file short** (owner, Nov 15 2026: it is loaded in every chat): new detail goes in the matching `docs/` file, only rules and one-line pointers go here.

## Working with the owner

- **Repo: `Twhidbey/math-jump`, branch `main`.** This repo IS the live game: GitHub Pages serves `index.html` at https://twhidbey.github.io/math-jump/, so pushing `main` publishes it (Pages takes 1–2 min; the Actions tab shows a green ✓; a phone may cache up to 10 min, so tell the owner to bump `?v=N` on the link). Commit and push after every change, then tell the owner it's live. The notes live here too and the repo is public: keep personal details about the family out of them. (Until Nov 2026 the game and notes lived in `math-jump/` of `banhamt/quickpoll_private`; that repo is no longer used for Math Ninja.) **Start a new chat by reading `HANDOFF.md`** (what was built most recently, open questions, ideas).
- **Build stamp:** the home screen shows `Updated <date time> PT · <what changed>` (search `class="build"`). Update it on every change so the owner can see the new file loaded. `checkUpdate` (end of the script) fetches the page with `no-store` on load and when the app comes back (home screen only), compares the stamp, and reloads once with `?v=<time>` if it differs (`sessionStorage` `mn-update` stops loops). So the iPad home-screen icon updates itself: **the stamp must change on every release** or the check can't see it. **Also after every level** (owner, Nov 11 2026): `finishLevel` calls `checkUpdate(true)` (fetches only bytes 0–65535 with a `Range` header via `fetchStamp`, full page as fallback; **keep the build stamp near the top of the file**), which sets `updateReady`; the next `startStage(i)` / `toMenu()` calls `updateBeforeLeaving` → reload with `sessionStorage` `mn-resume` = i, and startup goes straight into that level.
- Players: young kids, kindergarten to about 3rd grade math. Mostly played and tested on an iPhone.
- Owner prefers: **ask before coding** (propose a short plan or options with a recommendation, then build when they say go), short kid-friendly text, pixel art over emoji, subtle Christian themes (grace, a hero who gives himself for those who don't deserve it, welcome home).
- Owner cares about: cohesion (each world should feel like one place), things making sense conceptually, keeping Kai moving, every right answer visibly doing something. **Keep visuals plain**: reuse the world's own tiles and styles ("normal squares that fit into each level, nothing fancy") rather than new decorative art.

## Where things are

The detail lives in `docs/`, one file per area. **Open the file for the area you are about to change** (and update it afterwards); don't load them all. Search `index.html` for the names in backticks (line numbers drift).

| Notes file | What it covers | Names to start from |
|---|---|---|
| `docs/story.md` | Story text and pages (`STORY.md` is the source: keep in sync), animated story pictures, Read to me, the scroll row | `STORY`, `ENDING`, `SCENES`, `runScenes`, `readAloud`, `storyBook` |
| `docs/levels.md` | The 7 worlds and 28 stages, `slotOf` indexing, the level builder, twists, flavours, backgrounds, ? boxes, physics, draw order, HUD text, home screen | `WORLDS`, `STAGES`, `slotOf`, `buildLevel`, `TWISTS`, `FLAVORS`, `updatePlayer`, `render`, `buildMenu` |
| `docs/sea.md` | The Coral Sea (swimming, depth gates, clams, deep sea, octopus boss, current tunnel, sea twists) and fractions | `seaBuild`, `swimY`, `seaDoors`, `drawSeaDark`, `isFrac` |
| `docs/math.md` | Skills, grade tracks, Easier math, test-out, fact tracking / Fact Book / Daily Dojo, kindergarten help, Never get hurt, Sensei's tricks and Work it out | `SKILLS`, `GRADE_TRACKS`, `planStage`, `noteFact`, `makeEasier`, `trickInfo`, `kidPic` |
| `docs/crossings.md` | Gates, the hungry animal and math ? boxes, stepping stones, pattern walls, swings, bridges, ski lift | `gateNear`, `resolveAnswer`, `miniTarget`, `stepsPick`, `wallPuzzle`, `swingTick`, `liftChunk` |
| `docs/dojo.md` | Training rooms: the drill, moves, poses, entrances, leaving early | `MOVES`, `buildVault`, `trainAnswer`, `posedFigure`, `ENTRANCES` |
| `docs/bosses.md` | Bosses and their entrances, the held-out hand, game over, victory moves, races | `buildArena`, `BOSS_SPECS`, `offerHand`, `gameOver`, `startVictory`, `startRace` |
| `docs/friends.md` | The six lost friends, rescue scenes, guards, treasures, friend powers | `FRIENDS`, `addFriend`, `startRescue`, `GUARD_STYLE`, `hasFriend` |
| `docs/badges-gear.md` | Badges, the Gear Pack and gear powers, the shop, pixel icons, saves, music | `BADGES`, `GEAR`, `gearPowTick`, `SHOP`, `PIX`, `loadProg`, `SONGS` |
| `docs/team.md` | Team play on two devices (Firebase rooms): team boss, team run, shared level, gates together, Shadow Twins and showdown, helping each other, staying in sync | `TEAM_DB`, `tmSync`, `tmRunTick`, `LAYOUT`, `tmGateTick`, `tmTwinTick`, `tmShowdownTick`, `tmFriendSync` |

`docs/HISTORY.md` holds the older "what was built" notes that used to be in `HANDOFF.md`.

Tile letters: `X` pattern-wall block, `Z` pattern-wall choice block, `#` ground, `B` brick, `?` box, `U` used box, `S` stair, `O` world pillar, `G` gate, `A` answer block, `N` bridge stone, `b` plank, `R` room answer, `J` spring bamboo, `C/c` conveyor, `I` ice, `L` ladder (not solid). Each level has one flaming golden gem (`gold: true` coin) from `goldSpots`. Constants: `T = 36` px tiles, `GR = 13` ground row, `VW` 960 (540 on upright phones), `VH = 540`. 60 fps fixed step.

**Load-order gotcha:** `buildLevel` runs during startup (menu backdrop), so anything it uses must be defined above it or be a hoisted `function` (a `const` defined later throws "Cannot access before initialization" and the whole game fails to load). `ANIMALS`, `stepX`, `STONE_TOPS`, `FLAVORS` sit just above `buildLevel` for this reason. Helpers called while building must use the level being built (pass `L` in, as `stepsSet(st, L)`), not the global `L`.

## Testing (keep it cheap)

1. Syntax: `node -e "const s=require('fs').readFileSync('index.html','utf8');new Function(s.match(/<script>([\s\S]*)<\/script>/)[1]);console.log('ok')"` (this does NOT catch load-order errors; step 2 does).
2. Browser: Playwright + Chromium are preinstalled (`require('playwright')`). To reach internals, copy `index.html` to a scratch file and insert before the final `requestAnimationFrame(frame);\n})();` a hook like
   `window.__t = { get L(){return L}, get G(){return G}, get P(){return P}, get mode(){return mode}, get prog(){return prog}, keys, startStage, begin, tapAnswer, answerTarget, openGate, bump };`
   Then `startStage(i); begin();` and move `P.x/P.y` to the spot under test (e.g. `L.squads[0].foods[0].x`, `L.steps[0].c0`). Answer with `const m = answerTarget(); tapAnswer(m.vals.indexOf(m.q.ans))`. Set `localStorage` `mathninja-v2` to `{"seenIntro":true,"layout":7,"allOpen":true}` to skip the story. If `window.__t` is undefined, the game crashed on load: print `pageerror`s.
3. Only take screenshots for visual changes (a grid of small shots per world works well); check page errors (`page.on('pageerror')`) every time.

## Design decisions so far (don't undo without asking)

- **Goal: drill math, keep Kai moving.** About 16–21 problems per level. **Gates take ONE answer** (owner: 2–3 answer gates felt like "you think it'll open, then it doesn't"). Density comes from math on the run: one hungry animal per level (owner: only one; no stomping), math ? boxes, stepping stones or bridges (alternating levels; no bridges for K), training rooms, lost friends. Long plain runs after big moments are wanted. Number labels: dark text on white with a coloured border (white text on colour was hard to read). Every right answer should visibly do something right away.
- **Math should be the move, not tricky platforming** (stepping stones are crossed by answering). Things must make sense conceptually: a number-line zipline was tried and removed (spacing wasn't a real number line; dropping to build a bridge was arbitrary).
- **Answering:** answer blocks stay in the world (owner likes them). Phones: colour-matched buttons in an arc by the right thumb. Computers: no buttons; bonk, or press , . / (1–5 also work). **Bonks are forgiving** (owner: kids were missing hits): any part of Kai's head counts on answer blocks and pattern-wall choice blocks (no "middle under the block" rule), and in `moveY` a head that passes within 6 px of the side of an `A`/`Z` block counts too. Every new math thing also answers with buttons / keys via `miniTarget`.
- **No +1 / ×1 / n÷n outside the K skills** (add5, add10, make10, sub10 keep them). Also applies to tens facts, room puzzles, number machine and bridge stones.
- **Cohesion:** each world shares one background; per-level differences are small touches. Full per-level scenes were tried and rejected as "too much". Nothing hangs from the sky (lanterns hang on ropes between roofs, banners hang from a wall). Background lavafalls were rejected; the moon is only on Moon Tower; lanterns only on Lantern Roofs.
- **Training rooms replaced the secret puzzle rooms** (owner chose: replace, optional door, one Sensei throughout, learned moves as a gate flourish only). Moves go easy → hard: Bow, Straight Punch, Front Kick, Rising Block, Knife-Hand Chop / Side Kick, Spinning Back Fist, Roundhouse / Double Punch, Jump Front Kick, Sweep / Flying Side Kick, Spinning Hook Kick, 360 Jump Kick / The Master's Move ("The strongest move is to protect others").
- **Kind to kids:** falls into stepping-stone pits and the first fall at each bridge never cost a heart; animals never hurt Kai; messages stay up long enough to read.
- **Golden gems:** one flaming golden gem per level, a little tricky (climb + full jump), not hidden.
- Owner tried and rejected: answer bar only (no blocks), "blocks only, no buttons", stomping number critters, the zipline, full per-level background scenes, the busiest extras (bamboo in front of Kai, mirror beams, lightning, giant robot, wall of screens, ice-cave openings), oval stepping stones and the bounce cloud in pits.

- **Learning rules (from a math-education review, see `MATH_GOALS.md`):** a miss always shows the right answer (`Oops! 7 × 8 = 56`, gates and bosses; animals, boxes and stones already did). "Fast" comes from `fastFrames(skill, q, walk)`: 3 s for × ÷ (6 s walking/bonking), 5 s otherwise (10 s), also used by the Daily Dojo. Auto mode moves on when `skillProgress(k).ready` (90% learned AND half gold), not just `done`; the end-of-level card says "Come back tomorrow!" in between.

## Open requests / ideas

- **Pattern walls: built, waiting for owner/kids feedback.** Owner chose: touch the wall, "find all" primes, older kid only. Offered next: Square Towers (1, 4, 9, ?), Triangle Stairs (1, 3, 6, 10, ?), and a K Number Pyramid.

- **Math-learning ideas** (not chosen yet) are in `MATH_GOALS.md`.

- **Training rooms: built, waiting for owner/kids feedback.** Possible next: moves usable in boss fights, a Moves page with pictures, bigger Sensei sprite.
- **Lost friends: built, waiting for owner/kids feedback.** Owner chose: human-like kids (no dragon), freed with the kid's own tricky facts (option A), powers stay for good, friends go home to the dojo.
- **Approved, not built yet:** the pet asks a quick question while Kai runs (answer with buttons/keys for a pet trick + gems).
- Ideas offered, not chosen yet: cannon barrels (hop in the barrel with the answer to launch), target practice (hit all the 4s-table numbers), gem thief chase, gem grids (arrays: "how many?"), rescue friends trapped in bubbles (fits "welcome home"), fork in the path (right answer = shortcut), number gem trails during kite flight, locked treasure chest. Parked earlier: time medals, speed meter, ghost race, settings per kid.
- Not yet tested on a real phone: the answer-button arc and sizes, long-press paste for save codes, the iPhone sound fix (if still silent: ask which phone/browser).
