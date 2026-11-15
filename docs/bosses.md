# Math Ninja notes: Bosses, game over, victory moves, races

Part of the code notes; `CLAUDE.md` has the index. Search `index.html` for the names in backticks (line numbers drift).

## Bosses

`buildArena`, `BOSS_SPR`, `BOSS_SPECS`, `bossAttack`, `updateArena`, `spawnOrbs`, `runOutro`. **Entrance** (owner approved, Nov 11 2026; replaced the boss card): `startBossIn` (from `startStage`) → `G.bossIn`, `bossInTick` (in `update`, nothing else moves), `bossInPlace` per `BOSS_ENTRY` (drop with a THUD: golem/bot/yeti; rise: octo; leap: shogun; smoke: kage), `drawBossIn` (from `drawHUD`, which skips its banner meanwhile): letterbox, name slam + gong at `BOSS_SLAM`, taunt, FIGHT! + "Dodge! Then grab the right answer." at `BOSS_FIGHT`; Kai in guard (`kaiPose`); jump / a tap skips

## Victory moves (owner approved, Nov 11 2026)

`startVictory` from `updateWin` (level: after the scroll is caught, winT 40; boss: winT 30) → `G.victory`, `victoryTick`, `victoryPose` (`VIC_SEGS`, strike at `VIC_STRIKE` with burst + move name): a random learned dojo move (not Bow) or Hana's high kick, else `VICTORY_JUMP` (fist in the air); the diver just says Hooray. Kai walks home after `VIC_LEN`

## Game over / boss miss

**Team run** (owner, Nov 15 2026: "if they die they start at the last gate instead of leaving the game ... for team play only"): one button, Keep going ▶ → `continueLevel` (full hearts at `G.checkpoint`, gates and team kept; no Restart / Levels on the card). Solo unchanged: `gameOver` (K and 1st grade, by `curPlayer().grade`, get `continueLevel`: full hearts at `G.checkpoint`, level kept, "Restart level" as the other button; others and bosses restart), `startDodge(miss)` (half dodge, attack waits 40 frames). The score stays on the HUD (`dreamy-hamilton` hid it; not ported)

## Boss shuriken (all bosses)

The answer shuriken keep their numbers (owner asked; kept: answers live in the world). `hitOrb`: the right one becomes a shot with `catch: true` that flies to Kai's hand first, then Kai throws it (`updateShotsAndProjectiles`)

## Hand held out (last boss answer)

`hitOrb` / `openBossPad` `onRight`: when `L.boss.hp <= 1` no shuriken, `offerHand()` (`ar.wait` 9999, `G.hand`); `updateHand` (called before `updatePlayer`) walks Kai to the boss with `HAND_POSE` (from `kaiPose`), a heart for golem/bot/yeti, then a gentle boss-down (`b.gentle`: gold sparkles, small shake); HUD reads "Take my hand?"; Kage's outro starts at "Never."

## Races

`startRace(travel)`, `travelRace`, `judgeGate`, `updateRace`, `TRACKS`, `RIVALS`, `RIDES`. All answers right always wins, also in Easy (`boost` is not scaled by `slow`; accel/decay are)
