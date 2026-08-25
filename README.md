# Baranians

**A race mod for Songs of Syx 0.71.x**

A near-immortal species from a dead star, almost indistinguishable from man.
Peerless at research, administration, statecraft and open battle, and born nobles.
The price is the future: they bear roughly one child in four centuries and will not
migrate to a city that merely calls for workers. Your Baranians will always be a
handful. Everyone else does the digging.

---

## Install

Put this folder in:

```
C:\Users\<you>\AppData\Roaming\songsofsyx\mods\Baranians
```

Enable it in the game launcher under **MODS**, then start a new world. The race
appears in the species picker.

> **A savegame is bound to the mod set that created it.** Adding or removing any
> race mod invalidates existing saves — the per-race arrays in the save are written
> raw, without a length prefix, so a changed race count desynchronises the stream.
> The symptom is `OutOfMemoryError: Requested array size exceeds VM limit` while
> loading. Start a new world, or disable this mod to load an older save.

While testing, switch on **DEVELOPER** and **DEBUG** in the launcher. Data errors in
Songs of Syx are otherwise silent, or only land in the error log at
`...\Steam\steamapps\common\Songs of Syx\errorLogs` and
`...\AppData\Roaming\songsofsyx\logs`.

---

## Files

| Path | Purpose |
| --- | --- |
| `_Info.txt` | launcher metadata |
| `README.md` | this file |
| `Baranian_SheetGuide.png` | visual map of the sprite sheet |
| `V71\assets\init\race\BARANIAN.txt` | stats, boosts, population, traits |
| `V71\assets\init\race\sprite\BARANIAN.txt` | appearance definition |
| `V71\assets\text\race\BARANIAN.txt` | name, description, pros/cons |
| `V71\assets\text\race\bio\specific\Baranian.txt` | citizen biography lines |
| `V71\assets\text\misc\Quotes.txt` | loading screen quotes |
| `V71\assets\text\names\nameset\BaranianFirst.txt` | male and child first names, 367 |
| `V71\assets\text\names\nameset\BaranianFemaleFirst.txt` | female first names, 159 |
| `V71\assets\text\names\nameset\BaranianLast.txt` | surnames, 454 |
| `V71\assets\text\names\nameset\BaranianLastNoble.txt` | noble surnames, 133 |

| Sprite | Size |
| --- | --- |
| `V71\assets\sprite\race\Baranian.png` | 448 × 546 |
| `V71\assets\sprite\race\infant\Baranian.png` | 352 × 22 |
| `V71\assets\sprite\icon\24\race\Baranian.png` | 72 × 36 |
| `V71\assets\sprite\icon\32\race\Baranian.png` | 88 × 44 |

The four PNGs are byte-identical copies of the vanilla human art, renamed and
already wired up. Repaint them in place; no file name or path needs to change.
**They are Songs of Syx assets, so do not redistribute the mod with them untouched.**

The version folder is `V71` because the game is 0.71.x and the major version is what
counts. When the game moves to 0.72, copy `V71` to `V72` and check the files against
the new `data.zip`. The game picks the highest `V`-folder that is not above the
running major version, so a stale `V71` keeps being used and may silently misbehave.

---

## Effective values

Base values are the game's defaults from `game/boosting/BOOSTABLES.java`.
"Effective" is what a Baranian actually ends up with.

### Life and body

| Stat | Base | Boost | Effect |
| --- | --- | --- | --- |
| Lifespan | 100 years | ×4.0 | 400 max, ~349 average |
| Health | 1.0 | ×4.0 | |
| Stamina | 1.0 | ×2.5 | |
| Speed | 4.5 | ×1.25 | |
| Acceleration | 3.0 | ×1.25 | |
| Mass | 80 | ×1.15 | |
| Soiling | 0.125 | ×0.25 | stay clean far longer |
| Heat / cold resist | 0.5 each | +0.5 each | effectively immune to climate |
| Reproduction speed | 0.1 | ×0.060 | see [Reproduction](#reproduction) |

### Battle

| Stat | Base | Boost |
| --- | --- | --- |
| Offence skill | 1 | ×4.0 |
| Defence skill | 1 | ×4.0 |
| Block | 1 | ×3.0 |
| Dexterity | 5 | ×2.5 |
| Charge | 1 | ×2.5 |
| Morale | 4 | ×4.0 |
| Bow | 0.1 per weapon | ×3.0 |
| Formation skill | 0 | +3.0 |
| Blunt / slash / pierce | 40 each | +80 attack, +80 defence |

### Behaviour

| Stat | Base | Boost | Effect |
| --- | --- | --- | --- |
| Lawfulness | 1.0 | ×2.0 | barely any crime |
| Sanity | 1.0 | ×4.0 | effectively never break |
| Loyalty | 0 | +0.25 | |
| Submission | 0 | ×0.4 | poor slaves |

### Civic

Settlement-wide, so weighted by population share — see
[Settlement-wide boosts](#4-settlement-wide-boosts-are-weighted-by-population-share).

| Stat | Base | Boost | Effect |
| --- | --- | --- | --- |
| Immigration | 4.5 | ×0.02 | |
| Knowledge | 0 | +150 | research output |
| Admin | 0 | +50 | |
| Innovation | 0 | +1.0 | |
| Diplomacy | 0 | +1.0 | |
| Trust | 0 | +0.5 | |
| Government | 5 | ×2.0 | |
| Law | 0.10 | ×2.0 | |
| Maintenance | 1.0 | ×0.5 | buildings decay slower |
| Accidents | 1.0 | ×0.25 | |
| Nobles max | 0 | +8 | |
| Noble promotions | 0 | +10 | |

### Noble personality

Drives your king and your appointed nobles.

| Stat | Base | Boost |
| --- | --- | --- |
| Competence | 1.0 | +1.0 |
| Honour | 1.0 | +0.5 |
| Tolerance | 1.0 | +0.5 |
| Pride | 1.0 | +0.5 |
| Mercy | 1.0 | +0.25 |
| Aggression | 1.0 | +0.25 |

### Needs

These are consumption rates, so lower is better.

| Rate | Boost |
| --- | --- |
| Hunger | ×0.5 |
| Thirst | ×0.5 |
| Constipation | ×0.5 |
| Doctor | ×0.25 |
| Grooming | ×0.75 |

### Rooms

| Room | Boost |
| --- | --- |
| every room (`ROOM*`) | ×3.0 — the broad dial, covers modded rooms too |
| University, School, Library, Laboratory, Admin | ×4.0 |
| Stockpile | ×3.5 |
| all six mines (clay, coal, gem, ore, sithilon, stone) | ×3.5 |
| Barracks, Archery, Artillery | ×3.5 |

Construction speed cannot be boosted from a race file. The builder, hauler and
transport rooms register **no** boostable at all — `ROOM_BUILDER`, `ROOM_HAULER`
and `ROOM_TRANSPORT` do not exist, and neither does any `CONSTRUCTION_*` key. Only
`PHYSICS_SPEED` helps indirectly, by moving the builders around faster.

`ROOM*` also covers the `ROOM_CONSUMPTION_*` boostables, which are a **divisor** on
input use (`IndustryUtil.calcConsumptionRate`). Output and consumption rate rise
together, so the net effect is roughly three times the output for the same inputs,
rather than three times the raw throughput.

### World map

Nothing, deliberately. See [Scope](#3-scope-who-actually-receives-a-race-boost).

### TRAIT block

Personality traits rolled per individual, occurrence 0..1.

```
COMPETENT 1.0   TOLERANT 0.85   HONEST 0.7   WARRIOR 0.7   PROUD 0.6
MERCIFUL 0.35   CUNNING 0.1     CONSERVATIVE 0.1   MODEST 0.1
CRUEL 0.05      LAZY 0.0        WARRIOR_NOT 0.0
```

`COMPETENT` at 1.0 means every single Baranian carries the trait, which adds a
further +0.5 to `NOBLE_COMPETENCE` and +0.1 to `PHYSICS_SPEED` on top of the race
boost. `LAZY` and `WARRIOR_NOT` at 0.0 means they can never roll the two traits that
would cancel it.

### STATS_ON_SPAWN

`EDUCATION_EDUCATION: 1.0` — Baranians arrive fully educated, no school time.

---

## How the engine actually behaves

None of this is documented anywhere. It was read out of the game's own source in
`info\SongsOfSyx-sources.jar`. Getting it wrong produces boosts that silently do
nothing, which is worse than a crash.

### 1. Wildcard keys do not stack, and can be silently discarded

A boost key ending in `*` expands to every boostable whose key starts with the
prefix. In `BoostSpecs.PromiseList` a key that matches **more than one** boostable is
flagged *weak*. The rule in `add()`:

- a **weak** entry is **dropped** if any entry for that boostable already exists
- a **strong** entry (exactly one match) **replaces** whatever is there

They never multiply. This is the single biggest trap in race modding.

Concretely, this does not do what it looks like:

```
ROOM*>MUL: 1.5,
ROOM_MINE*>MUL: 0.75,
```

`ROOM*` is weak and covers all 112 room boostables first. `ROOM_MINE*` is also weak,
because it matches six mines, so it hits an existing entry and returns without doing
anything. The mines end up at 1.5, a bonus, and the 0.75 is thrown away with no
warning.

That is why every override in `BARANIAN.txt` is written out as an exact key.
`ROOM_UNIVERSITY*` would happen to work today because there is exactly one university
room, but it would break the moment the game adds a second.

Vanilla relies on the same rule: `DONDORIAN.txt` has `ROOM_WORKSHOP*>MUL 1.20` and
`ROOM_WORKSHOP_SMITHY>MUL 1.25`, and smithies end up at 1.25, not 1.5.

### 2. How multiple boosts on one value combine

From `BUtil.value`: all `ADD` boosters are summed, all `MUL` boosters are multiplied,
and the result is `(base + positive adds) * muls + negative adds`. Only relevant once
several different sources touch the same boostable — a race boost plus a player level
plus a trait, for instance.

### 3. Scope: who actually receives a race boost

`RaceBoosts.BV` builds one `BValue` per boosted stat, and which overload the engine
calls decides who benefits:

| Overload | Resolves to | Who benefits |
| --- | --- | --- |
| `vGet(Induvidual)` | that creature's race | every creature, everywhere |
| `vGet(Div)` | that division's race | every army unit |
| `vGet(HCLASS_RACE)` | your settlement, weighted | your city only |
| `vGet(Region)` | that world region, weighted | whoever owns it |
| `vGet(FactionNPC)` | the faction's capitol region | NPC factions |
| `vGet(Player)` | the neutral value | nobody |

The consequence is that `WORLD_*` boostables are region scoped. They are attached
with `BoostableCat.ALL().WORLD` and evaluated per region through `vGet(Region)`,
which averages over the races living in that region. Your own settlement never reads
them — the city runs on `ROOM_*` instead. So a `WORLD_BUILDING_MINE` boost does
nothing for your city, a little for world regions you own, and exactly the same
little for every NPC faction whose provinces happen to hold Baranians.

That is why this mod sets **no** `WORLD_*` boosts at all. Adding them would hand the
enemy the same bonus for almost no gain to you, since Baranians are capped at 3
percent of any region by `POPULATION MAX`.

`PHYSICS_*` and `BATTLE_*` are unavoidably universal: they resolve per creature, so a
Baranian in an NPC army is just as strong as one in yours. A race mod cannot scope
those to the player without scripting.

### 4. Settlement-wide boosts are weighted by population share

Anything queried at the settlement level rather than per individual is averaged over
your population, weighted by headcount (`RaceBoosts.BV.vGet`, the
`popTime.race == null` branch). A city that is 10 percent Baranian gets 10 percent of
the listed value.

This bites hardest on the noble boosts, because the consumer casts to `int`:

```java
ranksAllocated() < (int) MAX_RANKS.get(HCLASS_RACE.clP())
```

At a 5 percent Baranian share, +8 nobles becomes 0.4, which truncates to 0. The
flagship perk is invisible until roughly 13 percent of your citizens are Baranian.
Rarity and the noble bonus pull against each other by design; if you want the nobles
to show up in a small elite, raise the `ADD` values.

### 5. Immigration is throttled per race, not city-wide

`Immigration.java` line 272 queries the boost with `clP(race, CITIZEN)`, so
`CIVIC_IMMIGRATION>MUL 0.02` only throttles Baranians. Humans and everyone else still
arrive normally. The intended pattern works: a tiny immortal elite, with other
species doing the labour.

One leak: a few lines earlier, if a world camp of that race is available, the code
returns the camp replenish rate and skips the boost entirely. A Baranian settlement
on the world map next door defeats the throttle.

### 6. The trait block is called `TRAIT`, not `TRAITS`

`TRAITS.serRaceData` reads a block named `TRAIT` — the map key is the singular. Every
vanilla race file carries a `TRAITS` block full of `FIGHTER`, `GLUTTON` and
`SPRINTER`, and none of it is read by anything. Valid trait keys are the file names
in `assets\init\race\trait\`.

### 7. Dead keys in the vanilla files

`TECH` is not read anywhere in the source. `PORTRAIT_FILE` in the sprite definition is
not read either; portraits are assembled from the shared face part sheets via the
`FACE` block. `ADULT_AT_DAY` in `PROPERTIES` is likewise ignored — adulthood is
`BABY_DAYS + CHILD_DAYS`.

### 8. Not every room has a boostable

Do not assume that a room file in `assets\init\room\` implies a boostable named
`ROOM_<key>`. Only rooms whose blueprint extends `RoomBlueprintIns` register one.
`_STOCKPILE` gives `ROOM_STOCKPILE`, but `_BUILDER`, `_HAULER` and `_TRANSPORT` give
nothing. Leading underscores are also stripped inconsistently: vanilla `_CANNIBAL`
ends up as `ROOM__CANNIBAL`, with two underscores.

The authoritative list is printed by the game itself. Enable DEVELOPER and DEBUG,
reference one deliberately bogus key, and `BOOSTING.available()` dumps every valid
boostable as `KEY  - Name` lines into
`AppData\Roaming\songsofsyx\logs\UnhandledDump.txt`. On this install that is 537
entries, 116 of them `ROOM_*` — and that list already includes the boostables added
by your other mods, which no amount of reading the vanilla files will tell you.

### 9. Value ranges are clamped silently

`POPULATION MAX` is clamped 0..1, `GROWTH` 0.0001..1, `CLIMATE` entries 0..1,
`TERRAIN` 0..100, `TRAIT` occurrence 0..1, structure and road preferences 0..1, `WORK`
preferences −10000..10000. Boost values are not clamped.

Terrain and climate entries you leave out default to **0**, not to 1.

---

## Reproduction

A game year is 16 days (4 seasons at `DAYS_PER_SEASON 4`).

| | |
| --- | --- |
| Baby days | 24 |
| Child days | 200 → adult at day 224, about 14 years |
| Fertile from | day 336 = `ceil(1.5 * adult day)`, about year 21 |
| Fertile until | year 210 = `(lifespan - from) * 0.5 + from` |
| Lifespan | 400 years maximum |

Death is not uniform. `StatsPopulation.death()` draws a value skewed towards the top
of the range and returns `0.45 + 0.55 * it`, so a Baranian dies somewhere between 180
and 400 years, averaging about 349.

Reproduction is checked four times a year per fertile individual, each with a chance
of `REPRODUCTION_SPEED / 4`. Both genders can become a parent.

Simulating the game's own formulas over 600 years with 400 individuals:

| `REPRODUCTION_SPEED>MUL` | Per century | Doubling time |
| --- | --- | --- |
| 0.040 | −11 % | dies out |
| 0.047 | 0 % | replacement level |
| 0.050 | +4 % | ~1700 years |
| 0.055 | +11 % | ~660 years |
| **0.060** | **+19 %** | **~395 years — current setting** |
| 0.080 | +47 % | ~180 years |

At 0.060 a Baranian bears about 1.1 children in a full life. Twenty starting
Baranians become roughly 40 after 300 game years.

> **Do not** shrink the fertile window with `PHYSICS_REPRODUCTION_AGE` to suppress
> births. It works, but it leaves only a few percent of the race fertile at any
> moment, and a small colony then swings wildly. Measured with the window cut to 19
> years: a colony of four died out in 39 percent of runs, against 9 percent with the
> normal window at the same effective growth rate. Change the rate, not the window.

---

## Sprite sheet

See `Baranian_SheetGuide.png` for the same information as a picture.

`Baranian.png` must stay exactly **448 × 546**.

| Half | Contents |
| --- | --- |
| left 224 px | the picture (diffuse) |
| right 224 px | normal map for lighting — leave as is, or fill flat with `#8080FF`. Same pixel position, shifted 224 to the right. |

Inside the left half:

| Region | Layout |
| --- | --- |
| x 0–65 | body: 2 columns × 18 rows of 24×24, origin (6,6), pitch 30 |
| x 66–223, y 0–119 | lying: 4 columns × 3 rows of 32×32, origin (72,6), pitch 38 |
| x 66–223, from y 194 | addons: 8 slots, pitch 44 — per slot 2× 24×24 at x 72 and 102, plus 2× 32×32 at x 138 and 176 |

The 18 body rows, top to bottom (names from `HSpriteConst.java`):

| # | Row | # | Row |
| --- | --- | --- | --- |
| 0 | `FEET_NONE` (leave empty) | 9 | `TORSO_RIGHT3` |
| 1 | `FEET_RIGHT` | 10 | `TORSO_LEFT` |
| 2 | `FEET_RIGHT2` | 11 | `TORSO_LEFT2` |
| 3 | `FEET_LEFT` | 12 | `TORSO_LEFT3` |
| 4 | `FEET_LEFT2` | 13 | `TORSO_CARRY` |
| 5 | `TUNIC` | 14 | `TORSO_OUT` |
| 6 | `TORSO_STILL` | 15 | `TORSO_OUT2` |
| 7 | `TORSO_RIGHT` | 16 | `HEAD` |
| 8 | `TORSO_RIGHT2` | 17 | `SHADOW` |

The two tiles in a row are the two animation frames.

Addon slots: 0 armour, 2 noble cloak, 3 hair, 4 hair behind the head, rest free.

Lying block groups, left to right then top to bottom: `PANTS`, `TORSO`, `ARMS`,
`HEAD`, `SHADOW`, unused.

### What the art must look like

**Top-down view.** The figure is tiny, about 13 × 11 px, centred in its 24×24 tile.

**Draw one facing only.** The game rotates every row into all four directions
(`paste(3, true)` in `RaceSheet`).

**Paint in greyscale.** Skin, clothes, armour and hair are tinted at runtime from the
`COLORS` block in the sprite definition. Coloured pixels cannot be tinted cleanly
afterwards.

Separation of skin, legs and clothing happens through the rows, not through colour
markers: `FEET` rows are tinted with `COLOR_LEG`, `TORSO` and `HEAD` with
`COLOR_SKIN`, `TUNIC` with `COLOR_CLOTHES`.

**Unused pixels must be alpha 0.** Not black, not blue.

The green and blue lines in the margins are only a drawing grid. The game never reads
them, so they can stay or go.

The two icons are different: front-facing portraits, one 24×24 tile at (6,6) and one
32×32 tile at (6,6), again with the normal map in the right half. Icon sheets must
satisfy `(width/2 - 6) % (tile + 6) == 0` in both axes.

### Shared, not per race

These stay vanilla and need no copies:

| Folder | Contents |
| --- | --- |
| `sprite\race\face\*.png` | portrait parts (skull, nose, eyes, hair, …) |
| `sprite\race\skelleton\` | skeleton |
| `sprite\race\sleep\` | blanket |
| `sprite\race\extra\` | tools, water, trolley |
| `sprite\race\face\addon\` | crown, helmet, raider gear |

To give the Baranians their own portrait parts, add a new file next to the vanilla
ones — e.g. `sprite\race\face\SkullBaranian.png`, 416 wide, height a multiple of 60,
4 frames per row, cell 40×48 at `x = 6 + 52*col`, `y = 6 + 60*row` — and reference it
in the `FACE` block as `SkullBaranian: 0`.

The world map look (`WORLD` block: `TOWN`, `VILLAGE`, `OVERLAY`, `WALL`, `TERRAIN`)
still points at the vanilla human tiles and can stay that way.

---

## Loading screen quotes

The loading screen picks a random entry from `assets\text\misc\Quotes.txt`, read in
`RLoadPrinter` as key `QUOTES`. Each entry is one string holding both the quote and
its attribution, separated by `:::`:

```
""Kingdoms are a weather to us.":::-The Ashen Order",
```

The outer quotes delimit the string. The inner pair is displayed, so the text shows
up in quotation marks the way vanilla does it. The part after `:::` is rendered
underneath as the author.

### Appending instead of replacing

A mod file with the same path replaces the vanilla file wholesale, which would wipe
all 34 vanilla quotes. To append, the file needs **both** flags at the top:

```
_JSON_ADD: true,
_ARRAY_ADD: true,
```

`_ARRAY_ADD` alone does nothing. In `JsonValueJson.overwrite` the recursion into an
existing key only happens when `jsonAdd` is set — otherwise the key is replaced with
`putReplace` and the array-level `arrayAdd` flag is never reached. Verified: vanilla
34 + this mod's 8 = 42 entries.

### Traps

| Written as | Result |
| --- | --- |
| `""text":::-Author"` | correct |
| `""text"::-Author"` | also works, `::` is the fallback separator |
| `""text"` — no separator | **quote and author both render empty.** A blank loading screen, logged only as `unable to parse` |
| `""text":::"` — nothing after | author renders as a stray `:` |
| `""text":::-"` | author renders as a lone dash, harmless |

So every entry must carry a separator with something after it. There is no error, no
crash, and nothing in the launcher — a forgotten `:::` simply produces an empty
screen. Avoid `:::` inside the quote text itself for the same reason.

### Quotation marks and apostrophes inside the text

`JsonValue.findValue` is called with `"` as both the opening and the closing
character, so its nesting counter decrements and increments on the very same
character and never leaves zero. The whole rule reduces to one line:

> The string ends at the first `"` that is **immediately** followed by a comma.

Everything else is ordinary text. In particular:

| Inside the quote | Result |
| --- | --- |
| `'` apostrophes, any number | fine, the parser does not look at them |
| a nested `"..."` pair | fine, as long as its closing `"` is not directly before a comma |
| `..."yes", he said` | **hard parse error**, `The entry is not a string`. This is a thrown `Errors.DataError`, not a warning — it takes the game down |
| `..."yes" , he said` | fine. The check is `charAt(i+1) == ','` exactly, so one space defuses it |
| `..."sticks".` | fine, and this is how vanilla does it |

Vanilla contains exactly this case and solves it by putting the sentence period
after the inner closing quote:

```
""The preacher was chained ... to which he replied "I bear no ill will towards
these fools, nor do I towards stones or sticks".":::-Chronicles of the Third Age 49:87",
```

Note the `sticks".` — period after the quote, never `sticks",`.

Single colons are harmless, which is why `49:87` in that attribution works.

### Characters that render

`assets\init\config\Charset.txt` defines the font's glyph set. The default western
charset covers ASCII plus the full Latin-1 range, so German umlauts and `ß` display
correctly. It does **not** contain typographic punctuation: the curly quotes `“ ” ‘ ’`
and the en and em dash `– —` are all missing. Draft the text in a plain editor, or
a word processor's autocorrect will silently replace your straight `'` with a
character the font cannot draw.

`**` at the start of a line comments it out, inside the array as well. The skeleton
uses that for the empty slots, so unfilled ones cannot reach the screen.

### Not usable for tips

`assets\text\misc\Advice.txt` looks similar but is not extensible: `EventAdvisor`
hardcodes the four keys `WORKFORCE`, `SICKNESS`, `CRIME` and `LOYALTY` in Java. A mod
can reword those, not add new ones. `assets\init\event\HINT.txt` is a full event
with trigger conditions and choices, not a one-liner.

---

## Names

Until 1.6 the Baranians had no name set of their own. Their sprite file was a copy of
the human one and pointed at the shared `Std*` lists, so a Baranian was named exactly
like a human and any name mod installed alongside silently renamed them too.

They now carry four dedicated lists under `V71\assets\text\names\nameset`. Each one
begins with the complete human list as it stands on this installation, in the original
order, and appends the Baranian names after it. Nothing that could appear before can
stop appearing, so an existing save keeps every name it already handed out.

| List | Human base | Baranian additions | Total |
| --- | --- | --- | --- |
| `BaranianFirst` | 269 | 98 | 367 |
| `BaranianFemaleFirst` | 79 | 80 | 159 |
| `BaranianLast` | 372 | 82 | 454 |
| `BaranianLastNoble` | 96 | 37 | 133 |

The human base is taken from the *active* lists, that is vanilla plus Argo's Names
Expanded, workshop 3748583275, which replaces the four `Std*` files outright rather
than merging into them. If that mod is uninstalled the Baranian lists are unaffected,
they are self-contained.

The additions draw on three registers, kept deliberately mixed so a Baranian settlement
does not read as a single monoculture:

- Arkonide and Perry Rhodan material for the long-lived star-people register:
  Atlan, Gonozal, Orbanaschol, Fartuloon, Crest, Thora, Farnathia.
- The star's own names across traditions: *al-dabaran* the Follower, Latin
  *Palilicium*, Sanskrit *Rohini*, the Hyades, *Alnath* and *Elnath* on the
  neighbouring horn of Taurus. Hence Dabaran, Palilion, Rohinar, Hyador, Elnath.
- The mod's own lore, rendered as English compound surnames the way vanilla does it:
  Ashenveil, Starless, Deadstar, Longwatch, Undiminished, Coldfire, Exilebourne,
  Vaultkeeper, Silentcolumn.

Noble surnames follow the vanilla shapes, either `of <place>` or a `-stein` / `-berg`
compound, so Baranian nobles sit alongside human ones without looking pasted in:
of the Ashen Order, of Palilicium, of the Hyades, Aldebstein, Baranberg, Hyadstein.

Four references in `V71\assets\init\race\sprite\BARANIAN.txt` point at the lists:
`NAMESET_FILE_NOBLE` at the top, and `NAMESET_FILE_FIRST` / `NAMESET_FILE_SURNAME`
in each of the CHILD, male and female blocks. To go back to human names, set those
seven lines to `StdLastNoble`, `StdFirst`, `StdFemaleFirst` and `StdLast` again.

The engine cap is `StatsAppearance.NAME_MAX`, 4095 entries per list, so there is
room for roughly ten times the current count.

---

## Tuning dials

**Rarity** — `POPULATION MAX` 0.03 caps their share of any world region.
`POPULATION GROWTH` 0.0005 is the world-map growth rate, and 0.0001 is the engine
minimum. `CIVIC_IMMIGRATION>MUL` 0.02 throttles arrivals into your own city.

**Reproduction** — `PHYSICS_REPRODUCTION_SPEED>MUL`, see the table above. Leave
`PHYSICS_REPRODUCTION_AGE` alone.

**Lifespan** — `PHYSICS_DEATH_AGE>MUL`, base is 100 years. Long lives also make long
childhoods cheap: `BABY_DAYS` and `CHILD_DAYS` in `PROPERTIES` set the 224-day
growing-up time.

**Noble slots** — `CIVIC_NOBLES_MAX>ADD` and `CIVIC_NOBLES_RANKS_MAX>ADD`. Weighted
by population share and then truncated to `int`, so raise these hard if you want the
effect at low headcount. For reference, vanilla player level titles grant +5 nobles
and up to +20 promotions.

**Noble quality** — `NOBLE_COMPETENCE>ADD` plus the `TRAIT` block.

**Power level** — `ROOM*>MUL` 3.0 is the broad "good at everything" dial.
`CIVIC_KNOWLEDGE>ADD` 150 is the research dial; vanilla player levels sit between 35
and 200, so this is roughly one extra title's worth of research at full Baranian
population.

---

## Known inconsistencies

The race is not balanced against the vanilla species and is not meant to be. It was
built to the brief *"absolutely overpowered, but almost never reproduces and almost
never migrates"*.

---

## Changelog

### 1.0

Initial build. Race, texts, biography lines, sprite wiring.

### 1.1

Reproduction reworked. `PHYSICS_REPRODUCTION_AGE>MUL 0.1` removed; it cut the fertile
window to 19 years of a 400-year life, which both read absurdly and made the
population collapse. `PHYSICS_REPRODUCTION_SPEED>MUL` raised from 0.02 (far below
replacement, guaranteed extinction) to 0.060. Description and CONS text corrected to
match.

`ROOM_MINE*` and `ROOM_REFINER*` replaced with exact per-room keys. As wildcards they
were weak and silently discarded, leaving mines and refiners at the `ROOM*` bonus of
1.5 while the pros/cons text claimed they were a weakness. Mines set to 0.6, refiners
to 0.75. The five intellectual rooms were rewritten as exact keys too, for the same
failure mode.

Sprite art split out into own files (copies of the human art) so the Baranians can be
repainted without touching the human race.

### 1.2

Production, construction and combat raised to match the brief.

Mines went from a 0.6 penalty to a 3.5 bonus, and the matching `WORK` preferences
flipped from negative to positive so Baranians are no longer unhappy doing the job
they are now good at. Refiners and workshops likewise.

`ROOM*>MUL` raised from 1.5 to 3.0, so every room including those added by other mods
is covered. Builder, hauler, transport, stockpile, barracks, archery and artillery
called out explicitly above that.

Battle skills raised from ×3.0 to ×4.0, morale to ×4.0, block to ×3.0, bow to ×3.0,
formation to +3.0, every damage type from +60 to +80, and health from ×3.0 to ×4.0.

PROS/CONS and the description corrected: the mining weakness is gone, and `CHALLENGE`
dropped from Hard to Easy, which is now honest.

### 1.3

All `WORLD_*` boosts removed. They are evaluated per world region, not per
settlement, so they did nothing for your own city while handing every NPC faction
with Baranians in its provinces the identical bonus. The advantage now lives entirely
inside your own walls.

### 1.5

Loading screen quotes added, `assets\text\misc\Quotes.txt`, with eight filled
entries and eight commented-out slots. Uses `_JSON_ADD` plus `_ARRAY_ADD` so the
vanilla quotes survive.

### 1.4

`ROOM_BUILDER`, `ROOM_HAULER` and `ROOM_TRANSPORT` removed. They are not boostables,
so the game logged `no BOOSTABLE named` for each and the values did nothing. Those
three rooms carry no work-rate boost in the engine. `ROOM_STOCKPILE` is real and
stays. Every key is now checked against `BOOSTING.available()` from the game's own
log rather than against the vanilla room file names, which over-generate.

### 1.6

Own name set. Four lists under `V71\assets\text\names\nameset`, each carrying the
full human list first and Baranian names after it, and the seven `NAMESET_FILE_*`
references in the sprite file repointed at them. See **Names** above.

`Secondexile` and `of the Second Exile` were removed again in favour of the plain
`Exilebourne` and `Farexile`, to match the `Of the Exile` attribution in
`Quotes.txt`. The ordinal survives only as an army name in
`V71\assets\text\race\BARANIAN.txt`.

### 1.7

`PREFERRED > OTHER_RACES` raised from a blanket `*: 0.8` to 1.0, with every vanilla
race also listed explicitly. Baranians no longer take the discrimination penalty from
living in a city whose population is mostly other races, which in practice means a
city staffed by foreign slaves. The wildcard stays for modded races.

Explicit entries matter here. A wildcard is a weak match and loses to any strong entry
another race declares through its own `OTHER_RACES_REVERSE`, the way ARGONOSH does.
The forward pass runs after the reverse pass in `RacePreferrence.init()`, so a strong
entry in our own file wins outright.

`OTHER_RACES_REVERSE` is deliberately left at 0.9. That is what everyone else thinks
of the Baranians, and there is no reason a stranger should warm to them.

### 1.8

`STATS > POPULATION_SLAVES_OTHER` added. The stat is the share of the total population
held as slaves, defined in `StatsPopulation.java` line 195. Left uninverted it reads as
a virtue, so a Baranian's standing rises with the size of the slave force.

```
POPULATION_SLAVES_OTHER: {
	CITIZEN: 2.0,
	NOBLE: 2.0,
	SLAVE: 0,
	MULTIPLIER: 2,
	PRIO: 5,
},
```

`MULTIPLIER: 2` means the value saturates at a city that is half slaves rather than
demanding a city that is nothing but slaves. Weight 2.0 places it above every other
standing entry the race carries. Argonosh is the vanilla comparison at `CITIZEN: 1.5`
with no multiplier; Cretonians and Dondorians set the same stat `INVERTED`, which is
why they resent a city full of slaves.

`SLAVE: 0` keeps Baranian slaves out of it. A Baranian in chains has no opinion worth
modelling on the subject.

Emigration is unrelated to being outnumbered. `EventCitizen.getAmount()` reads only
`STANDINGS.CITIZEN().loyalty`, so anything that lifts standing lifts loyalty and
suppresses emigration. Both this entry and the 1.7 tolerance change work through that
one channel.

### 1.9

`STATS > POPULATION_SLAVES_SELF` added as the counterpart to 1.8. The stat is defined
in `StatsPopulation.java` line 183 as own-race slaves divided by own-race citizens plus
one, so it measures how much of the race is in chains rather than how large the city is.

```
POPULATION_SLAVES_SELF: {
	INVERTED: true,
	CITIZEN: 6,
	NOBLE: 6,
	SLAVE: 0,
	MULTIPLIER: 4,
	PRIO: 5,
},
```

`INVERTED` turns the value into a grievance. Weight 6 matches the harshest vanilla
setting, used by Argonosh and Cantor, and outweighs the approval of foreign slaves
three to one. `MULTIPLIER: 4` saturates at a quarter, so with a Baranian population
this small a single one of them in chains is already a full outrage.

The pair reads as one rule: slaves are correct, and Baranians are not slaves.
