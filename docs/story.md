# Math Ninja notes: Story, story pictures, Read to me

Part of the code notes; `CLAUDE.md` has the index. Search `index.html` for the names in backticks (line numbers drift).

## Story text (opening, ending pages). **`STORY.md` is the source for all story text; keep them in sync

`const STORY`, `const ENDING`, `const MORNING`, `const HOME`, `showEnding`, `showMorning`, `showHome`, `endBody`, boss scenes in `runOutro`, win cards in `BOSS_CARD`; Settings > Read the story is `storyBook`/`storyPages`

## Story pictures (animated pixel scenes on story pages)

`SCENES` (in two parts: `const SCENES` has the opening, `Object.assign(SCENES, {...})` the rest; per page 2–3 slides of `{cap, draw(c, t, p)}`, captions a few words), `sceneHTML(name)` (canvas inside `.scenepic`, a storybook scroll frame), `runScenes` (started by `showMsg`; owner Nov 10 2026: `SLIDE_LEN` 4 s, ◀ ▶ `.scarrow` buttons, ← → keys (`sceneSt`, top of the keydown handler), swipe, tappable dots; a flip by hand sets `s.hold` so it stops moving on; slides change with a pixel dissolve on the art canvas (`DISSOLVE` order, 450 ms); `sceneLife` adds a few drifting single pixels and a light tint per page (`SCENE_MOOD`: petals, embers, sparks, snow, bubbles, twinkling stars, warm motes)). **One pixel grid:** every scene is drawn on a 192×108 art canvas and blown up by a whole number; sprites at 1 px per cell via `scSpr.kai/sensei/shogun/kuro` (never scaled, no zoom), flat colours, eyes 1×2 px on everyone, mountains/hills fill to the bottom (no floating). Kit: `dot`, `bands`, `disc`, `ring`, `mountains`, `scHills`, `pine`, `scCherry`, `scDojo`, `torii`, `birds`, `tufts`, `branch`, `petals`, `senseiFig`, `sPut`, `scroll`, `baby`. Young Kuro (`KURO_SHEET`) = the Shogun's body with a face, topknot and red headband. **Owner wants the story very simple** (Nov 2026): 1–3 short sentences per page, 2–3 slides with few-word captions, Kuro is the brother from page one, no clues or mystery

## Read to me

`readAloud(btn)` / `stopReading` (`speechSynthesis`, rate 0.9, en-US voice): `showMsg` adds a "🔊 Read to me" button to any page with a `scenebox` (the button becomes "⏹ Stop" while reading); reads the page's `<p>` text; stopped by `showMsg`, `begin` and closing the story book. **iPhone: the silent switch mutes the voice** (owner's phone was on silent; the game music plays anyway via `audioSession`), so on iOS (`isIOS`) the first tap adds a `.readtip` line "No voice? Flip the silent switch". Only cancels when something is speaking (Safari drops a speak() right after cancel())

## Scroll row (home screen)

`#scrollRow` filled in `buildMenu`: one `.scrl` per world, `pixImg('scroll')` once `prog.best[bossOf(w)]`; tap opens that boss's story page (the Shogun's opens The Castle Falls) via `storyBook`

## Kuro's journal and the world map (owner, Nov 22 2026)

Why Kuro went to each world (popularity, anger about past hurts, control, needing no one, riches, revenge, the throne) is in `JOURNAL` (`why`, `text`; above `storyPages`), the `WORLDS[].intro` lines, and one added line per boss in `runOutro` (timings pushed later). Pages: `placePage(i)` in `startStage` puts `L.page` 40 px above the gem nearest 55% of the level in each world's middle level (castle: also Shadow Walls for the last page); `pageTick` (from `shopPowTick`) picks it up into `prog.journal[j]` with `G.pageGot`; `drawPage` (after the coins); `journalHTML` on the level's end card. Home screen `.maprow`: **World map** (owner: "like a map from Lord of the Rings, with regions, pixel style": `drawWorldMap` paints a 250 × 160 parchment map (sea `mapSea`, inked coast, river, hills, each region `MAP_LAND` with a colour wash and its own `MAP_GLYPH` symbols, mist over lands not reached, two `MAP_FOG` unknown lands, compass, frame, Kuro's red dotted route, the gold road home) and `openMap` scales it 4× and adds the labels; tap a land for its line, its page and Go there) and **Kuro's journal** (`openJournal`, `SENSEI_NOTE` once the castle boss is won and the last page found). A new world needs a `JOURNAL` entry, a `MAP_AT` spot (take a fog spot) and a `MAP_LAND` entry.
