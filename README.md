# Math Ninja

A side-scrolling math platformer. Everything is in `index.html`: no build step, no dependencies, and it works offline. Open the file in a browser to play.

## Story

Kuro, Kai's big brother, took the five Math Scrolls, ran away and became the Shadow Shogun. Sensei sends Kai to bring the scrolls home, and his brother too. Kai is kind to the bosses (the Golem, Mega-Bot and the Snowman turn good; Kage runs away), and at the castle he saves Kuro from a falling beam. In the morning Kuro asks why; "Because you're my brother." Sensei runs to welcome his two sons home. Every page is 1–3 short sentences with a picture, and a 🔊 **Read to me** button reads it out loud. The full text is in `STORY.md`.

## Math skills

The math comes from the skill you pick, not from the level, so any level can be played with any skill. Tap the yellow math chip on the home screen (or "Change math" before a level) to choose.

| Kind | Skills (★ difficulty) |
|------|-----------------------|
| Add | within 5 ★, within 10 ★, make 10 (7 + ? = 10) ★, within 20 ★★, tens (30 + 40) ★★, 2-digit + 1-digit ★★★, 2-digit + 2-digit ★★★★ |
| Take away | within 10 ★, within 20 ★★, tens ★★, 2-digit − 1-digit ★★★, 2-digit − 2-digit ★★★★ |
| Times | each table ×2 to ×12 (★★ to ★★★★), 2 to 5 mix ★★★, 6 to 9 mix ★★★★, tens (3 × 40) ★★★★, all tables ★★★★★ |
| Divide | ÷2 to ÷10 (★★★ to ★★★★), all division ★★★★★ |
| 🧩 Think | missing number (8 + ? = 13) ★★, skip counting (5, 10, ?, 20) ★★, balance it (7 + 5 = ? + 8) ★★★, missing factor (? × 6 = 42) ★★★★, missing in division (? ÷ 4 = 7) ★★★★, number patterns (1, 2, 4, 8, ?) ★★★★, balance times (4 × 6 = 8 × ?) ★★★★★ |

**Auto mode (🧭, on by default)** moves the math up by itself, based on the facts the player actually knows (see Fact Book below). When 90% of a skill's facts are learned and at least half are gold (remembered fast on two different days), auto mode moves to the next skill on the path, so new math only comes once the old facts have stuck: add within 5 → add within 10 → take away → make 10 → within 20 → tens → skip counting → missing numbers → 2-digit adding and taking away → balance it → ×2, ×5, ×10, ×3, ×4 → times 2 to 5 → ÷2, ÷5, ÷10 → ×6 to ×9 → times 6 to 9 → missing factor → the other divisions → missing in division → ×11, ×12 → patterns → tens → all tables → balance times → all division. The math chip shows facts learned (like 6/10). About 1 question in 5 brings back a fact to practice or one that is due for review. Picking a skill by hand moves them to that spot on the path. The 🧭 switch at the top of the math picker turns auto off.

**With a grade set, auto mode mixes the grade's math, and each world favours one kind.** Each grade is split into a few kinds (tracks), each easy → hard; for 3rd grade: Times, Divide, Big adding, Big take-away and Think. Worlds: Japan = Add, Lava = Take away, Robot = Times, Snow = Divide, Sea = Fractions, Castle = Think. **Level 1** of a world is only that kind, at the kid's spot in it. **Levels 2 and 3 and the boss are mixed**: about 40% the world's kind (always more than any other kind; 60/40 when the grade has only two kinds), the rest shared by the other kinds being learned; the boss also brings back kinds already passed. If the grade has no such kind, or it's locked (Divide waits for its times table: "Divide opens after Times 2") or passed, level 1 takes the kind furthest behind. After each level, every kind with at least 4 questions is judged on its own: 9 in 10 right with most of them fast = that kind's next level 1 is one step harder (⭐ Challenge!); under 6 in 10 = one step easier, with Sensei's tips after one miss instead of two. A kind is passed skill by skill as above (90% learned, half gold); when every kind of the grade is passed, the next grade's kinds take over. About 1 question in 4 is a review. The level card shows the plan ("Mixed · mostly Times"), the math picker shows a row of squares per kind (gold = passed, green = learned, ring = up next). Picking a skill by hand works for one level.

Each skill deals every fact in shuffled order before repeating, so a level of "Times 7" only asks 7× facts and doesn't repeat them. Harder skills pay more: gems are multiplied by ×1 to ×3, ninja points for a stage are accuracy (1 to 3) × stars, and each skill earns its own bronze, silver or gold medal. Bridge targets follow the difficulty too (make 10, 20, 50 or 100).

## Worlds

Instead of pipes, each world has its own pillars: stone lanterns, basalt columns, steel crates, snow-capped ice blocks and castle stone.

| World | Enemies | Levels | Boss (scroll won) |
|-------|---------|--------|-------------------|
| 1 Japan Village | bandit ninjas | Cherry Path, Bamboo Grove, Koi Pond | Kage the Shadow Blade |
| 2 Lava Volcano | rock monsters, leaping lava blobs | Ash Trail, Lava Falls, Obsidian Caves | Magma Golem |
| 3 Robot Factory | robots | Gear Works, Conveyor Run, Laser Lab | Mega-Bot 3000 |
| 4 Frozen Peaks | grumpy penguins | Frosty Slopes, Icicle Caves, Blizzard Peak | The Abominable Snowman (throws snowballs, some lobbed, some rolling) |
| 5 Coral Sea (Kai swims: floats at the surface, dives under rafts; gates are reef walls with doors at different depths) | fish, jellyfish | Coral Reef, Kelp Forest, Sunken Ship | The Great Octopus (ink blobs at Kai's depth) |
| 6 Night Castle | hopping shadow ninjas | Lantern Roofs, Moon Tower, Shadow Walls | The Shadow Shogun |

**Boss fights** take turns. First you **dodge**: the boss moves and attacks (low shuriken, lasers or rolling snowballs to jump over, or rocks, snowballs and fireballs lobbed from above). Then the boss gets **dizzy**: its attacks vanish and giant shuriken with answers on them float in the air (3, or 5 for the harder bosses and in expert mode). Jump and grab the one with the right answer, and Kai throws it straight at the boss. A wrong one bursts, gives you a new question and sends you back to a shorter dodge (half as long, and the boss waits a moment before attacking). The last right answer throws no shuriken: Kai walks up and holds out his hand ("Take my hand?"), and the boss calms down. When the boss goes down, it acts out what happens next with one short speech bubble: Kage says "Never!" and fades away; the Golem cools down ("Thank you, little ninja."); Mega-Bot lets every robot rest; the Snowman melts and has a friend; and in the Shogun's castle the ceiling falls in, Kai shouts "Look out!", pushes the Shogun clear and is hit by the falling beam, leading into the ending. Then you grab the scroll to finish.

**Anti-guessing:** a wrong answer at a gate swaps in a new question, answers in a row build a streak that multiplies points, and missed facts come back later and are listed on the results card.

## Gates

One right answer opens a gate. Gates don't just lift. Each world opens them its own way: Japan's paper screens slide apart in a shower of petals; in the lava world Ash Trail's cracked stone wall crumbles, a lavafall on Lava Falls pours across the path until the right answer block flies up and plugs its spout, and Obsidian Caves' black crystal shatters; the factory's force field shorts out with a crack of lightning, ice walls are blown away by a gust of wind, and the castle's shadow wall turns into a flock of white doves.

## What makes each level different

Every level has its own twist (shown in yellow when the level starts):

| World | Level 1 | Level 2 | Level 3 |
|-------|---------|---------|---------|
| Japan | Cherry Path: grab a **koi kite** and fly (tap jump to flap) along trails of sky gems | Bamboo Grove: **springy bamboo** launches you over tall walls; pandas peek out | Koi Pond: wide ponds with **lily pads that sink** and **leaping koi** to bounce on |
| Lava | Ash Trail: **falling rocks**, with a red warning circle before each lands | Lava Falls: a **wall of lava chases** you; it waits behind each unopened gate | Obsidian Caves: **dark cave**; you only see around Kai, and crystals light up when touched |
| Robot | Gear Works: **spinning gear platforms** carry you over gaps | Conveyor Run: **conveyor belts** and **crushers** to time | Laser Lab: **lasers** blink on and off |
| Snow | Frosty Slopes: **slippery ice** ponds | Icicle Caves: **icicles** shake and drop when you run under them | Blizzard Peak: **giant snowballs** roll at you through a blizzard (jump on them for a gem) |
| Castle | Lantern Roofs: **wall jumps** up chimneys for gems, under **fireworks** | Moon Tower: **ladders** (hold jump to climb) to high ledges | Shadow Walls: **guards with flashlights**; standing still in a barrel hides you, being spotted calls more shadow ninjas |

## Math on the run

Between gates the math keeps coming, without stopping Kai:

- **A hungry animal:** once per level, an animal that fits the level (a rabbit on Cherry Path, a panda in Bamboo Grove, a penguin on Frosty Slopes, a raccoon on Shadow Walls...) waits with a problem in a thought bubble. Three pieces of its favourite food float ahead with numbers; jump into the right one (or tap its button / press its key) to feed it, and it gives gems. For players set to 2nd grade or up, the bubble tells the problem as a short story about the animal ("The panda finds 2 piles of 9 bamboo. How many?"); the banner keeps the numbers.
- **Math ? boxes:** some ? boxes say "Quick question!" and send three answer bubbles floating ahead of Kai. Grab the right one for the box's prize.
- **Pattern walls (older players):** once per level a gate is guarded by a wall of number blocks in a famous pattern. **Pascal's Triangle** (each block is the two above it added) and **Fibonacci Stairs** (each step is the two before it added) have ? holes: bonk, tap or press the right number and it flies into place. On the **Prime Wall** you touch the wall itself: find every prime (a wrong one shows why, like 9 = 3 × 3). Finish the pattern and it lights up, crumbles, and the gate opens. Kindergarten skills don't get walls.
- **Skip-count stepping stones:** one pit in every other level (bridges take the other levels; kindergarten math gets stones in every level). A sign gives the rule with an arrow ("Count up by 3s" ↑, "Count back by 2s" ↓), and each hop shows +3 or −2. Kai hops onto the first stone by himself, then each answer is the move: pick the next number and he hops onto that block. Each answer has a time limit (a bar over the blocks: 8 seconds, 12 in Easy mode, and no time limit in Easy mode for kindergarten). A wrong block crumbles, and if time runs out every block crumbles; either way he drops back to the start to try a new pattern (no heart lost). Reach the far side and a bridge appears.
- **Pictures for kindergarten math:** kindergarten questions (add within 5 or 10, make 10, take away within 10) show a ten frame under the question, so 2 + 3 is dots and not just digits.
- **Swing crossings:** once per level Kai climbs two steps to a ledge over a wide gap. A right answer swings him across to a perch in the middle, where he stops; another right answer swings him the rest of the way down. Each world swings on its own thing: ropes from a torii gate, chains under a rock arch, crane hooks in the factory, a ski lift in the snow (it stops at the middle tower until you answer) and lantern ropes on the castle roofs. A wrong answer just wobbles him, shows the right one and asks another; no timer, and a fall into the gap puts him back on the ledge with no heart lost.
- **Room to run:** after each big moment (the animal, the stones, a bridge, a pattern wall) comes a long stretch of plain running, and two of them have ledges up in the sky with gems on top to jump to.
- **Math dash:** every 3 right answers in a row gives Kai a few seconds of super speed.

Outside the kindergarten skills there are no "+1", "× 1" or "8 ÷ 8" problems.

Each level also has one extra touch that fits its name: cherry trees to shake, bamboo, frogs, ash vents that puff you up, glow mushrooms, snowmen with hats, ice crystals that play Amazing Grace, wind gusts, lanterns to stand on, owls under a huge moon, bats and torches.

## Lost friends

Five little students from Sensei's dojo got lost, one in each world. Each is hidden behind a secret way in, and a small "Help!" bubble shows when Kai is close:

| World (level) | Friend | The secret | Freeing them | Power (rest of that level) |
|---|---|---|---|---|
| Japan (Koi Pond) | **Hana** (pink kimono) | Bonk the golden key block: a trapdoor slides open; walk onto it and the screen slides down into a cave | each right answer cuts a rope on her bamboo cage | **Fan glide:** hold jump to float down slowly |
| Lava (Ash Trail) | **Tomo** (miner's helmet) | Stand on the big glowing vent: it blows Kai up out of sight to a hidden ledge | each right answer breaks a fallen rock | **Brave heart:** the first hit in each level doesn't hurt |
| Robot (Conveyor Run) | **Niko** (goggles, wrench) | Jump onto the crate with the blinking light: it drops Kai down a chute | each right answer plugs in a battery for her broken lift | **Gem magnet:** gems near Kai fly to him |
| Snow (Icicle Caves) | **Yuki** (big furry hat) | Walk into the frozen waterfall: it cracks open | each right answer rings an ice chime and melts the ice (the last plays Amazing Grace) | **Spring feet:** Kai jumps a little higher |
| Castle (Moon Tower) | **Mei** (holding her lamb) | Climb the ladder that goes past the top of the screen to the tower roof | each right answer lights a lantern and a step down from her ledge | **Ninja vanish:** tap the vanish button (V on a computer) to turn into a dotted outline for 5 seconds; nothing can hurt Kai and the guards can't see him. Refills in 15 seconds, or at once with a right answer. Works in Moon Tower and the next level, Shadow Walls |

Each rescue has a treasure to find, and every right answer uses it: Kai's **high kick** knocks Hana's stone wall apart, **Tomo's mining hammer** smashes the boulders, **Niko's laser** cuts her lift's bars, a **fire torch** melts Yuki's ice, and **flaming throwing stars** light Mei's lanterns, each hit with a flash, flying pieces and a big comic word (KICK! SMASH! ZAP! WHOOSH! SHING!). Kai keeps the treasures: they're shown next to each friend in the Badge Book. Freeing a friend takes three right answers, and the questions are the player's own **tricky facts** (ones they missed or answered slowly), so the rescue is real practice. No timer; a miss shows the right answer and brings another fact. Freed friends go home to the dojo: they stand with Sensei on the Welcome Home page and in the Badge Book (which also says where the missing ones are lost). Finding all five earns the **Every One Matters** badge.

## Extra ways to play

- **Number-stone bridges:** in every other level (not for kindergarten math), some pits are too wide to jump. Bonk the floating number stones to pick one up, carry it to the altar at the edge, and make the exact target (10, 20, 50 or 100 by world). Too much and the bridge cracks and the stones go back.
- **Secret rooms:** one secret door per level leads inside a room that matches the world (a paper-screen dojo, a lava cave, a robot control room, a castle hall). Each room has a two-step puzzle on the back wall: a **balance scale** (7 + 5 = ? + 8), a **magic square** (every line adds to the same number) or a **number machine** (find the rule: 2 → 6, 3 → 9, 5 → ?). Bonk the right answer block to solve each step. Solving it opens the treasure chest and the gems spill out; each wrong guess takes 5 gems off the chest. The puzzles follow the chosen math's difficulty.
- **Surprise boxes:** about a third of the ? boxes hold a surprise instead of a gem: a shield, a double jump, speed boots, a gem magnet, a super star (can't be hurt, knocks out enemies), a fire aura or an extra heart.
- **Streak power-ups:** every 5 answers in a row gives a double jump, a shield that blocks one hit, or a fire aura that knocks out enemies and burns away boss attacks.
- **Dojo Shop:** gems are saved between levels and races. Spend them on headbands, suits, trails and pets. To buy something you work out how many gems you'll have left.
- **Races between worlds:** after each boss you ride to the next world, on a track that matches it (Lava Run, Night City, Snowy Pass). Your place doesn't block you; the race always leads on to the new world.
- **Race (menu button):** replay any track any time, using your chosen math skill. Pick a ride (panda, horse or tiger) and a track (Cherry Valley, Lava Run or Night City). Steer into the lane whose sign has the right answer for a speed boost. A wrong lane makes your ride stumble. A fact only counts as fast (silver) if you steered into the right lane soon after its gate came up. You race three rivals, and best times are saved per topic.

## Extras

- **Music:** each world has its own chiptune theme, and it grows stronger level by level: level 1 is the theme as written, level 2 is a bit faster with soft hi-hats and a pulsing bass, level 3 is faster again with a driving beat, an octave-bouncing bass and an echo of the tune, and the boss plays the world's theme at full strength (fastest, punchier lead, pumping bass). Races and the menu have their own themes. Turn it on or off with the 🎵 button.
- **Wolf pup and other pets:** the wolf pup costs only 5 gems (it's offered after the first level). Pets cheer right answers, look worried after mistakes, say "Ouch!" when you get hit and dance at the flag.
- **Expert rows:** the five answers in a row are the closest numbers around the right one, so they can't be guessed by size.
- **Sensei's tips:** two wrong answers in a row brings Sensei with a tip and a picture for the fact you missed: ten frames for adding and taking away within 20, dot arrays for times, groups for division, number-line hops for bigger numbers and patterns, and a balance for balance problems.
- **Golden gems:** each level has one flaming golden gem high above a pillar or stairs; climb and jump for it (worth 25). The level card shows 🌟 once it's found.
- **Scroll row (home screen, under the buttons):** one slot per world. Beating a boss fills its slot with that world's scroll; tap it to read that part of the story again.
- **Badge Book:** 47 badges in three sections, each badge not yet earned showing a progress bar:
  - **Math:** a badge for each times table from 2s to 10s (every fact gold in the Fact Book), all shown together in one **Times Tables** card with a tile per table (tap a tile to see its progress and prize). Each one unlocks gear you can't buy: Petal trail (2s), Lightning headband (3s, flashes), Bubble trail (4s), Ocean suit (5s), Snowflake trail (6s), Lava suit with embers (7s), a little octopus pet (8s), Rainbow headband (9s), an owl pet (10s). All nine make you a **Times-Table Master**: the sparkling Diamond suit and a title. The prizes show from the start, faded until earned, so kids know what they're working toward. Plus Gold Medal and Brave Brain.
  - **Keep going:** one card per goal with its bronze, silver and gold medals side by side and a bar to the next one: math gates opened (50 / 250 / 1000), right answers (100 / 500 / 2000), answers in a row (10 / 25 / 50) and perfect levels (1 / 5 / 20). Bronze pays 10 gems, silver 25, and gold gives a **title** (Gate Breaker, Math Machine, Unstoppable, Perfect Ninja) that the player can pick in the Badge Book; it shows under the belt on the home screen.
  - **Adventures:** things to do, such as finishing 5 of each kind of pattern wall (Triangle Builder, Stair Climber, Prime Hunter), feeding all 15 hungry animals, 10 Lightning bonuses, winning a race on every track, all 18 golden gems (unlocks the Golden suit), Untouchable and Champion Rider.
  - New gear pops up on the next end-of-level card with a **Wear it** button.

## Mastery

- **Fact Book (📒 on the home screen):** every fact a player answers is tracked. Right on the first try and fast makes it **silver**. Fast means from memory, not counted out: 5 seconds for adding and taking away (10 when Kai has to walk or bonk on a computer), 3 seconds for times and divide (6), 8 in a boss fight. A wrong answer always shows the right one (like "Oops! 7 × 8 = 56"), and the fact comes back later in the level. Silver again on a different day makes it **gold**, which means mastered. A wrong answer turns it red (practice) until it is learned again. A fact that is right but slow twice in a row (probably counted out) quietly comes back for practice in levels and the Daily Dojo, without losing its colour, until it's fast again. Each skill has a page; the mixed times tables and all division show a times-table grid that fills in gold. Skills without a fixed list of facts (big numbers and Think problems) show the last 10 answers instead, and 9 right and fast means learned.
- **Trophies:** when every fact of a skill is gold, the player gets a 🏆 for that skill and 25 gems.
- **Daily Dojo (🔥 on the home screen):** 10 quick questions with a 10-second fuse. Facts the player already knows (silver or gold) are **typed** on a number keypad ("You know this one. Type it!"; on a computer, number keys and Enter), because pulling an answer from memory builds it better than spotting it; typing gets 1.5 seconds more to count as fast. New and practice facts show 5 answers to pick from. **One more round** at the end starts another set. It picks facts to practice first, then silver facts from an earlier day (so they can turn gold) and gold facts due for review, then new facts from the current math. The first Dojo each day grows the streak and pays 10 gems plus 2 per streak day (up to 10). The pet grows a little bigger with the streak, and 7 days in a row earns the Dedicated badge. More Dojos on the same day are extra practice.
- **Expert mode:** once 60% of a skill's facts are learned, gates show five close answers in order instead of three, and boss fights use a number keypad, so guessing stops working.

## Ninja belts

Each level and boss earns ninja points: accuracy (3 for no wrong answers, 2 for one or two, 1 for more) times the math skill's stars. Your best score on each stage counts. Points add up to belts: White, Yellow (10), Orange (25), Green (50), Blue (83), Purple (125), Red (166), Brown (216) and Black (266 of 300). The ninja wears the belt you've earned.

Wrong answers never cost a heart. Only enemies, boss attacks and falling do.

**Out of hearts:** the level starts over. Players set to kindergarten or 1st grade go on from the last gate they opened instead, with full hearts and everything they'd done kept (a **Restart level** button is there too). Boss fights always start over.

## Controls

- Move: ← → or A / D
- Jump: Space, ↑ or W (hold to jump higher)
- Pause: P or Esc
- Answer: , . / (or N M , . / when there are five), or 1–5
- Sound on/off: the 🔊 button on the home screen
- The home screen sits over Sensei's dojo on the mountain at night. A big **Play** button continues the newest level. Below it, one framed panel holds the player, the math, the belt, the Daily Dojo and six pixel buttons. The world map shows each world's real scenery in its strip; worlds you haven't reached are under drifting fog, their levels dimmed in the world's colour and their boss a dark silhouette marked ???. Each strip has a straight path of 3 levels and a boss, with Kai standing on the newest level.
- Phones and tablets get big on-screen buttons. Upright phones get a squarer view (and a narrower boss arena), with the buttons underneath.

## Settings (⚙️ on the home screen)

- **Easy mode:** no holes, fewer and slower enemies, slower and less frequent boss attacks, and 5 hearts instead of 3. For kindergarten (grade K, or kindergarten math) Easy mode also takes the timer off the stepping stones, and in Shadow Walls the guard still spots you but sends no ninjas. Phones and tablets start with it on.
- **Unlock all levels / Lock levels again:** a switch. Turning it off goes back to only the levels you've earned.
- **Story:** shows the opening story again.
- **Sound and music:** separate on/off switches.
- **Reset progress:** clears points, belts and skill medals.

## Players

Several kids can share one device. Tap the name chip at the top of the home screen (or ⚙️ → Players) to open **Who's playing?**. Add a player with a name, grade (K to 5+) and picture. The grade sets their starting math (K: add within 5, 1st: add within 10, 2nd: add within 20, 3rd: times 2, 4th: times 6, 5th+: times 6 to 9), from where auto mode carries on, turns Easy mode on for K and 1st, and marks the skills for that grade with a 🎒 tag in the math picker. They can still pick any skill. Tap ✏️ on a player to rename them, change their grade or delete them. When more than one player exists, the game asks who's playing each time it opens.

## Saved progress

Each player's progress (points, belts, gems, shop items, badges, chosen math, Easy mode, the unlock switch) is saved separately in the browser's local storage on each device. An older single-player save becomes "Player 1". Progress isn't shared between devices or browsers, and it's lost if the browser's site data is cleared or a private window is used.

## Full screen on phones

Open the link in Safari, tap Share, then **Add to Home Screen**. It opens like an app, without the browser bars. On Android, use Chrome's ⋮ menu, then **Add to Home screen**.

## Hosting on GitHub Pages

1. Put `index.html` at the top level of a **public** GitHub repository.
2. Go to **Settings → Pages**. Under "Build and deployment", pick **Deploy from a branch**, then choose `main` and `/ (root)`.
3. After a minute or two the game is live at `https://<user>.github.io/<repo>/`.

## Changing the math

Each stage in the `STAGES` array uses a question generator from `gens`, for example `gen: gens.add20`. To add a new kind of question, add a generator that returns `mk(a, '+', b, answer)`.
