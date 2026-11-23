# Math Ninja notes: Math: skills, grade tracks, facts, help for kids

Part of the code notes; `CLAUDE.md` has the index. Search `index.html` for the names in backticks (line numbers drift).

## Math skills, decks, Think problems

`const SKILLS`, `deck(`, `thinkMissAdd`…

## Auto path / grades

`const PATH`, `const GRADES`, `pathRound(skill, { right, wrong, fast, race })`, `genFor(skill, reviews)`. **Grade tracks** (auto + a grade set; no grade = old PATH): `GRADE_TRACKS` (per grade: kinds, each easy → hard; a kind = its first skill's `cat`), `TRACK_REQ` (divide waits for its times table, same grade only), `trackState`/`trackPlan` (spot = first skill not `ready`; next grade when all passed). **Worlds favour a kind** (`WORLD_HOME`: japan add, lava sub, robot mul, snow div, sea frac, castle think): `planStage(i, commit)` (called by `startStage` with commit, and by `confirmStage` as a preview): level 1 (`st.k === 0`) = only the home kind at its spot ± `prog.gtrack.adj` (challenge / back); levels 2–3 and boss = mix, home ≥ 40% (and 10 points over an even share), others share the rest (boss also passed kinds); home missing/locked/passed → `behind()` (furthest behind). The plan goes to `LEVEL_MIX` (a `var` above `buildLevel`, load order!) → `mixGen` (1 in 4 reviews; questions carry `trk`, `sk`; `noteFact` / `fastFrames` use `q.sk`; `noteFact` fills `G.byTrack`). `trackRound` judges each kind with ≥ 4 questions (90% right & 70% fast → adj +1; under 60% → −1; `G.tipSoon` = tip after one miss on a step-back level 1) and lists passed skills (`trackNow.passed` snapshot). Hand-picked math: `prog.pickOnce` (one level). State: `prog.gtrack` (`last`, `adj`, `seen`), `prog.trackNow`; **`prog.track` is the race track, don't reuse**. Skills screen `#trackBox` rows

## Easier math (owner, Nov 11 2026: a 1st grader got discouraged; owner isn't worried about kids skipping ahead)

Pause menu button **Easier math** and Sensei's offer (`missed`: once a level, after 4 misses when misses > half the rights, not in rooms / rescues / gear rooms: tip card "Too tricky?" with an **Easier ▶** button (`G.tip.easy`, key E)) → `makeEasier`: restarts the level one step easier on every kind in it (`prog.gtrack.down[track]`, used by `planStage` via `easierSkill(id, n)`, a ladder of each kind's skills across all grades, so it can go below the kid's grade; PATH as a fallback). Hand-picked / no grade: `prog.skill` steps back. Nothing easier: offers Easy mode. A great round on that kind (`trackRound`) takes one step back off ("Great job! Next time: …")

## Test-out (owner asked: can a check move a kid up a grade?)

`#testBtn` in the skill picker under the grade tracks (Auto on + a grade): `startTest(gi)` 20 questions (`TEST_N`) from `testSkills(gi)` (grade skills not passed) in the Daily Dojo screen (`dojo.test`, `#djTitle`), `finishTest`: 90% right + 70% fast → every skill of the grade in `prog.testedOut` (`skillProgress` treats them as ready, so `trackPlan` moves to the next grade); else a track all right and fast (3+ questions) passes alone. One try per grade per day (`prog.testDay`)

## Fact tracking, Fact Book, Daily Dojo

`noteFact(q, right, fast, skill)` (skips `op: 'room'`; `fast === null` = time unknown: no silver, not slow; right but `fast === false` twice in a row → `f.practice` (in `reviewPool` and Dojo practice picks, status unchanged, cleared by a fast right); races time it in `judgeGate` (`g.shownAt` when the gate becomes next, `RC.laneT` last steer, `RC.fastN`)). Daily Dojo: silver/gold facts are typed (`dojo.typing`, `dojoType`, keys 0–9 / Backspace / Enter, +`DOJO_TYPE_EXTRA` s), others picked; "One more round" in `finishDojo`. `skillProgress`, `renderFacts`, `startDojo`; **Fact Book summary** (owner, Nov 11 2026: easy overview first, tap to dive in): `openFacts` opens on `renderSummary` (`fbSum`): grade + working on / next, one `.fsrow` per grade track (no grade: per kind played) with a gold / silver / practice bar over all its facts and skill chips (`factSkill` → that skill's page, which has a `◀ Summary` button), "Coming later" kinds, and "Needs practice" (`weakFacts`, up to 8) with **Practice these** → `startFactPractice` (practice screen, `dojo.practice.facts`, own end card in `finishPractice`); right answers pay gems via `payGems` (fly to the counter); end-of-level summary in `finishLevel` (`G.solved/fastN/lightN`, `prog.mathBest`)

## Never get hurt (owner, Nov 7 2026: a K kid was frustrated)

Settings switch `#safeBtn`, `setSafe`, `prog.safe` (per player, applied in `applyProg`): `hurt()` just blinks Kai and hops him back a little (`P.inv` 70, `sfx.bump`), no heart; `fell()` is free too. Math unchanged

## Kindergarten in Easy mode

`kEasy()` (Easy mode and grade K or a tier-1 skill): no stepping-stone timer (`stepTimed`). **Shadow Walls sentries** (owner, Nov 14 2026: "4–5 ninja appear, even in K level"; before it was 2, none for K Easy): a guard that spots Kai makes five shadow ninjas appear in smoke puffs (3 ahead, 2 behind, all walking toward him; a blocked spot moves to the nearest open ground, so it is always five, for every player); in `kEasy` they are just slower (1 instead of 1.4)

## K picture with the question

`kidPic` (only right before the problem, owner asked: a `miniTarget`, or a gate once Kai is between `st.s − 3` and the gate; tier-1 skill, judged per question by `q.sk` in mixed levels: `picFor` ten frames in a small panel under the HUD banner, via `drawTipPic(..., big)`); not in bosses, rooms, drill or Daily Dojo, hidden while `G.tip` shows

## Math dash

every 3 in a row (`streakUp` → `startDash`): `G.dash` frames of extra speed (`vmax` 7.4) + wind trail; not in boss fights

## Answer rows and tips

`rowChoices`: the closest numbers around the answer (times rows keep table neighbours, at most one table row away); `tipFor`: "Make the next ten first" (47 + 5) and "Take away to the ten first" (43 − 6) for 2-digit ± 1-digit

## Sensei's help: tricks, "New trick!", Work it out (owner asked, Nov 7 2026)

`trickInfo(q)` → `{ id, txt }` (one place that names each trick; `tipFor` = its text), `workSteps(q)` (the trick as 1–7 small steps `{text with ?, ans}`; null for think puzzles / `op: 'room'`), `TRICK_NAME`, `TRICK_EX` + `trickExample` (a sample fact, never the coming question). **New trick:** `previewTrick` (from `update`, every 10 frames): the first time a gate (from 8 tiles out), animal or math box needs a trick the player hasn't met, the tip card shows it with the sample fact ("New trick!", 8 s); once per player (`prog.tricks`). **Work it out:** `missed(q)` counts misses per fact per day (`prog.missToday`, across levels); the 2nd miss of the same fact opens `openWork(q)`: `#work` card, game frozen (`mode = 'work'`, skipped in `frame`), 3 choices per step (`workOpts`, answer colours), wrong pick greys out, ✕ / Escape closes, keys 1–3 or , . /, last 3 done steps shown; worked facts go in `G.helped` so `noteFact` gives no silver in that level. The tip card has a **Show me ▶** button (`G.tip.show`, key H) that opens the same walkthrough (`G.tip.q`; the sample fact for New trick cards). Otherwise two misses in a row still bring the plain tip

## Word problem at the animal

`wordQ(q, animal, food)` (above `buildLevel`; `WORD_ANIMAL`, `WORD_FOOD` singular/plural) adds `q.story` for + − × ÷ facts (not missing/step/think); `drawMini` shows it in a two-line bubble only when `reader()` (grade 2–5), clamped on screen; answer, choices and fact key unchanged

## A picture after a miss (owner, Nov 23 2026)

`missed(q)` → `missPicture(q)`: `G.missPic = { pic: picFor(q), txt: qSolved(q), t: 170 }`, drawn in `drawHUD` under the banner (the picture plus its equation, no other words; it replaces the "Oops!" float for that miss). Sensei's tip card after two misses and the one-time "New trick!" cards (`previewTrick`, now a no-op) are gone; "Too tricky?" (easier math) and Work it out (the same fact missed twice in a day) stay.

## Fixes from the six-reviewer math review (Nov 23 2026)

- **Skills without a fact list could never pass** (add2d1d, add2d, sub2d1d, sub2d and the Think skills): `prog.win[id]` holds only the last 10 answers and "ready" needed 2 different days among them, but a level asks more than 10. `noteFact` now also records in `prog.winOk[id]` the days (last 3) on which the window was good (9 of 10); `skillProgressRaw` counts those days too. So: a good day, then a good day another day = ready.
- **`fastFrames`:** skills without a fact list get 12 s on touch (18 s walking/bonking) instead of 5 / 10: those questions are worked out, not recalled.
- **`choices(q, 3)`:** the right answer was the middle value 57-70% of the time (wrong ones were mostly one above and one below). Now the number of wrong choices below the answer is picked evenly (0, 1 or 2), so lowest / middle / highest come up about a third each (measured over 600 questions per skill; very small answers are still the lowest more often).
- Not done from that review (ideas): typing the answer for gold facts at gates, pictures before the question for more than K, counting / place value / time / money, multi-step problems for strong third graders, `fcmp` "=" only 9% of the time.

