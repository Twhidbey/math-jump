# Math Ninja notes: the parent page

Part of the code notes; `CLAUDE.md` has the index. Search `index.html` / `parent.html` for the names in backticks.

## What it is (owner, Nov 2026)

`parent.html` is a separate page (its own link, not linked from the game): each kid's play time (today, last 7 days, playing now), a daily time limit per kid, their math level and plain suggestions. Owner chose: when time runs out the kid finishes the level they're in, then "Time's up for today!"; a 4-digit parent PIN.

## Data (the team database, `TEAM_DB`)

`families/<8-char code>`: `made` (server time), `kids/<kidId>` (the game's report), `limits/<kidId>` (`{on, mins, extra: {day, mins}}`, written by the parent page). Only numbers, the grade, the player's picture (a small PNG data URL) and plain-text facts/suggestions are sent: **never a name**. The parent names each kid on their own phone (`mathninja-parent` in localStorage: `fam`, `pin`, `names`). The PIN is only on that phone; "Forgot the PIN?" asks for the family code. The database rules allow `families/$fam` (8 letters/numbers) next to `rooms/$code` and deny everything else; the owner pasted them on Nov 20 2026 (text in `HANDOFF.md`). Any new path the game writes needs a rules change first.

## In the game

At the end of the script, above `checkUpdate`: `FAM_KEY` (`mathninja-family`, the device's family code), `famKid` (`prog.kidId`, random, per player), the 1-second timer (counts `prog.time[YYYY-MM-DD]` while the page is visible and the kid is in a level/race or touched something in the last 2 minutes; keeps 14 days), `famPush` (every 60 s, after each level, when the app goes to the background), `famPull` (the limit, every 60 s and when the app comes back), `famLeft`, `famStop` (at the top of `startStage`, `startRace`, `tmHost`, `tmJoin`), `famTimeUp` (the card: Check again / Switch player), `famMath` (grade from `trackPlan`, belt, each grade track's %, current skill, weak facts, right-but-slow facts), `famSuggest` (up to 4 sentences). "5 minutes left today!" and "Time's up! Finish this level." float over Kai. Settings > `famBtn` "Parent page" links the device (type the family code; checked against `made`); unlinking needs the code too. Nothing happens on a device that isn't linked.

## Honest limits

It only sees time inside Math Ninja (not the whole device; that's Apple Screen Time). Clearing the browser's data or using another browser gets around it. Anyone who knows a family code could read or change that family's data (no names in it).

## Stop after this level (owner, Nov 20 2026)

Parent page: a red **Stop after this level** button on each kid (and **Stop everyone after this level** at the top when there's more than one) writes `stop: <today>` into `limits/<kidId>`; **Let them play** removes it. In the game `famStopped()` makes `famLeft()` 0 for today only (it clears by itself the next day): the kid finishes the level they're in ("Last level! Finish this one."), then the card says "Time to stop! Great work today, Sam! See you next time." (Check again / Switch player). The game asks for the limit every 20 s.

## Tap for details (owner, Nov 20 2026: "summary, but I can dive in")

The game also sends `families/<code>/detail/<kidId>` after each level, when linking and at start-up (`famDetail` / `famPushDetail`, about 20 KB): each grade track's skills (passed / now / later, gold of n), every fact of them (status, right-and-fast count, wrong count, slow, days since last seen), Think skills' last 10 tries, 14 days of play time, `prog.plog` (each level played: time, name, skill, right, wrong, medal or ran out of hearts; `famLog` in `finishLevel` and `gameOver`; kept 14 days, from Nov 20 2026 on), levels won with medals and golden gems, badges, the closest badges, friends, gems, gates. The parent page shows it in `<details>` sections (`dt`): tap a kind of math (skills + a coloured fact grid; tap a fact for its numbers, `factInfo`), the week chart (14 days with the levels played), the tricky / slow chips, and Progress. Open sections survive the 20-second refresh (`openSet` in sessionStorage).

## Parent PIN on the kids' devices (owner, Nov 20 2026: switching player got around the time limit)

On a linked device, switching to another player, adding one, or opening Edit (change / delete / move) asks for the parent PIN (`famAsk`, from the Players screen in `showPlayers`). The parent page saves `sha256('mn:<code>:<pin>')` at `families/<code>/pin` (`sendPin`, once per family, again after a new PIN); the game caches it in `mathninja-family-pin` (refreshed by `famPull`). Before the parent page has sent a PIN, the family code works instead. The prompt is asked first (still inside the tap, for iPhone) and checked after. Unlinked devices are unchanged.

## Switching families (owner, Nov 20 2026, after losing a code)

Parent page: **Switch family** (bottom) opens `setup()` in switching mode: the families used on this phone before (`st.fams`, up to 8, tap to go back), another code, or a new empty family (asks first). The PIN stays the same and is sent to the new family (`sendPin`). In the game, Settings > Parent page on a linked device asks for the parent PIN or the family code (`famLink`), then offers **Link to another family** (`famLinkNew`: the same kid id moves over, its limit is cleared until the new family sets one) or **Unlink**. Lost code: the Firebase console's Data tab shows `families/<code>` (the owner can see it; the rules hide the list from everyone else).
