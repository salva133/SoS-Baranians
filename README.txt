================================================================================
BARANIANS
Race mod for Songs of Syx 0.71.x
================================================================================

A near-immortal species from a dead star, almost indistinguishable from man.
Peerless at research, administration, statecraft and open battle, and born
nobles. The price is the future: they bear roughly one child in four centuries
and will not migrate to a city that merely calls for workers. Your Baranians
will always be a handful. Everyone else does the digging.


--------------------------------------------------------------------------------
INSTALL
--------------------------------------------------------------------------------

This folder belongs in:
  C:\Users\Asus\AppData\Roaming\songsofsyx\mods\Baranians

Enable it in the game launcher under MODS, then start a new world. The race
appears in the species picker.

While testing, switch on DEVELOPER and DEBUG in the launcher. Data errors in
Songs of Syx are otherwise silent or only land in the error log at
  ...\Steam\steamapps\common\Songs of Syx\errorLogs


--------------------------------------------------------------------------------
FILES
--------------------------------------------------------------------------------

  _Info.txt                                        launcher metadata
  README.txt                                       this file
  Baranian_SheetGuide.png                          visual map of the sprite sheet

  V71\assets\init\race\BARANIAN.txt                stats, boosts, population, traits
  V71\assets\init\race\sprite\BARANIAN.txt         appearance definition
  V71\assets\text\race\BARANIAN.txt                name, description, pros/cons
  V71\assets\text\race\bio\specific\Baranian.txt   citizen biography lines

  V71\assets\sprite\race\Baranian.png              body sheet          448 x 546
  V71\assets\sprite\race\infant\Baranian.png       infant sheet        352 x  22
  V71\assets\sprite\icon\24\race\Baranian.png      small icon           72 x  36
  V71\assets\sprite\icon\32\race\Baranian.png      large icon           88 x  44

The four PNGs are byte-identical copies of the vanilla human art, renamed and
already wired up. Repaint them in place; no file name or path needs to change.
They are Songs of Syx assets, so do not redistribute the mod with them untouched.

The version folder is V71 because the game is 0.71.x and the major version is
what counts. When the game moves to 0.72, copy V71 to V72 and check the files
against the new data.zip. The game picks the highest V-folder that is not above
the running major version, so a stale V71 will keep being used and may silently
misbehave.


--------------------------------------------------------------------------------
EFFECTIVE VALUES
--------------------------------------------------------------------------------

Base values are the game's defaults from game/boosting/BOOSTABLES.java.
"Effective" is what a Baranian actually ends up with.

LIFE AND BODY
  Lifespan            base 100 years, x4.0    -> 400 max, ~349 on average
  Health              base 1.0, x4.0
  Stamina             base 1.0, x2.5
  Speed               base 4.5, x1.25
  Acceleration        base 3.0, x1.25
  Mass                base 80,  x1.15
  Soiling             base 0.125, x0.25       -> stay clean far longer
  Heat/cold resist    base 0.5, +0.5 each     -> immune to climate
  Reproduction speed  base 0.1, x0.060        -> see REPRODUCTION below

BATTLE
  Offence skill       base 1, x4.0
  Defence skill       base 1, x4.0
  Block               base 1, x3.0
  Dexterity           base 5, x2.5
  Charge              base 1, x2.5
  Morale              base 4, x4.0
  Bow                 base 0.1 per weapon, x3.0
  Formation skill     base 0, +3.0
  Blunt/slash/pierce  base 40 each, +80 attack and +80 defence

BEHAVIOUR
  Lawfulness          base 1.0, x2.0          -> barely any crime
  Sanity              base 1.0, x4.0          -> effectively never break
  Loyalty             base 0,   +0.25
  Submission          base 0,   x0.4          -> poor slaves

CIVIC  (these are settlement-wide, see POPULATION WEIGHTING below)
  Immigration         base 4.5, x0.02
  Knowledge           base 0,   +150          research output
  Admin               base 0,   +50
  Innovation          base 0,   +1.0
  Diplomacy           base 0,   +1.0
  Trust               base 0,   +0.5
  Government          base 5,   x2.0
  Law                 base 0.10, x2.0
  Maintenance         base 1.0, x0.5          -> buildings decay slower
  Accidents           base 1.0, x0.25
  Nobles max          base 0,   +8
  Noble promotions    base 0,   +10

NOBLE PERSONALITY  (drives your king and appointed nobles)
  Competence          base 1.0, +1.0
  Honour              base 1.0, +0.5
  Tolerance           base 1.0, +0.5
  Pride               base 1.0, +0.5
  Mercy               base 1.0, +0.25
  Aggression          base 1.0, +0.25

NEEDS  (lower is better here, these are consumption rates)
  Hunger              x0.5
  Thirst              x0.5
  Constipation        x0.5
  Doctor              x0.25
  Grooming            x0.75

ROOMS
  every room          x3.0     the broad dial, covers modded rooms too
  University          x4.0
  School              x4.0
  Library             x4.0
  Laboratory          x4.0
  Admin               x4.0
  Builder             x4.0
  Hauler              x3.5
  Transport           x3.5
  Stockpile           x3.5
  all six mines       x3.5     clay, coal, gem, ore, sithilon, stone
  Barracks            x3.5
  Archery             x3.5
  Artillery           x3.5

  Note that ROOM* also covers the ROOM_CONSUMPTION_* boostables, which are
  a DIVISOR on input use (IndustryUtil.calcConsumptionRate). Output and
  consumption rate rise together, so the net effect is roughly three times
  the output for the same inputs rather than three times the raw throughput.

WORLD MAP
  nothing, deliberately. See SCOPE below.

TRAIT block  (personality traits rolled per individual, 0..1 occurrence)
  COMPETENT 1.0   TOLERANT 0.85   HONEST 0.7   WARRIOR 0.7   PROUD 0.6
  MERCIFUL 0.35   CUNNING 0.1     CONSERVATIVE 0.1   MODEST 0.1
  CRUEL 0.05      LAZY 0.0        WARRIOR_NOT 0.0

  COMPETENT at 1.0 means every single Baranian carries the trait, which adds a
  further +0.5 to NOBLE_COMPETENCE and +0.1 to PHYSICS_SPEED on top of the
  race boost. LAZY and WARRIOR_NOT at 0.0 means they can never roll the two
  traits that would cancel it.

STATS_ON_SPAWN
  EDUCATION_EDUCATION 1.0   -> Baranians arrive fully educated, no school time


--------------------------------------------------------------------------------
HOW THE ENGINE ACTUALLY BEHAVES
--------------------------------------------------------------------------------

None of this is documented anywhere. It was read out of the game's own source
in info\SongsOfSyx-sources.jar. Getting it wrong produces boosts that silently
do nothing, which is worse than a crash.

1. WILDCARD KEYS DO NOT STACK, AND CAN BE SILENTLY DISCARDED

   A boost key ending in * expands to every boostable whose key starts with the
   prefix. In BoostSpecs.PromiseList a key that matches MORE THAN ONE boostable
   is flagged "weak". The rule in add():

     - a weak entry is DROPPED if any entry for that boostable already exists
     - a strong entry (exactly one match) REPLACES whatever is there

   They never multiply. This is the single biggest trap in race modding.

   Concretely, this does not do what it looks like:

       ROOM*>MUL: 1.5,
       ROOM_MINE*>MUL: 0.75,

   ROOM* is weak and covers all 112 room boostables first. ROOM_MINE* is also
   weak, because it matches six mines, so it hits an existing entry and returns
   without doing anything. The mines end up at 1.5, a bonus, and the 0.75 is
   thrown away with no warning.

   That is why every override in BARANIAN.txt is written out as an exact key.
   ROOM_UNIVERSITY* would happen to work today because there is exactly one
   university room, but it would break the moment the game adds a second.

   Vanilla relies on the same rule: DONDORIAN.txt has ROOM_WORKSHOP*>MUL 1.20
   and ROOM_WORKSHOP_SMITHY>MUL 1.25, and smithies end up at 1.25, not 1.5.

2. HOW MULTIPLE BOOSTS ON ONE VALUE COMBINE

   From BUtil.value: all ADD boosters are summed, all MUL boosters are
   multiplied, and the result is (base + positive adds) * muls + negative adds.
   Only relevant once several different sources touch the same boostable, for
   example a race boost plus a player level plus a trait.

3. SCOPE: WHO ACTUALLY RECEIVES A RACE BOOST

   RaceBoosts.BV builds one BValue per boosted stat, and which overload the
   engine calls decides who benefits:

     vGet(Induvidual)   that creature's race            per creature
     vGet(Div)          that division's race            per army unit
     vGet(HCLASS_RACE)  your settlement, weighted       your city only
     vGet(Region)       that world region, weighted     anyone who owns it
     vGet(FactionNPC)   the faction's capitol region    NPC factions
     vGet(Player)       returns the neutral value       nothing

   The consequence is that WORLD_* boostables are region scoped. They are
   attached with BoostableCat.ALL().WORLD and evaluated per region through
   vGet(Region), which averages over the races living in that region. Your
   own settlement never reads them - the city runs on ROOM_* instead. So a
   WORLD_BUILDING_MINE boost does nothing for your city, a little for world
   regions you own, and exactly the same little for every NPC faction whose
   provinces happen to hold Baranians.

   That is why this mod sets no WORLD_* boosts at all. Adding them would
   hand the enemy the same bonus for almost no gain to you, since Baranians
   are capped at 3 percent of any region by POPULATION MAX.

   PHYSICS_* and BATTLE_* are unavoidably universal: they resolve per
   creature, so a Baranian in an NPC army is just as strong as one in yours.
   A race mod cannot scope those to the player without scripting.

4. SETTLEMENT-WIDE BOOSTS ARE WEIGHTED BY POPULATION SHARE

   Anything queried at the settlement level rather than per individual is
   averaged over your population, weighted by headcount (RaceBoosts.BV.vGet,
   the popTime.race == null branch). A city that is 10 percent Baranian gets
   10 percent of the listed value.

   This bites hardest on the noble boosts, because the consumer casts to int:

       ranksAllocated() < (int) MAX_RANKS.get(HCLASS_RACE.clP())

   At a 5 percent Baranian share, +8 nobles becomes 0.4, which truncates to 0.
   The flagship perk is invisible until roughly 13 percent of your citizens are
   Baranian. Rarity and the noble bonus pull against each other by design; if
   you want the nobles to show up in a small elite, raise the ADD values.

5. IMMIGRATION IS THROTTLED PER RACE, NOT CITY-WIDE

   Immigration.java line 272 queries the boost with clP(race, CITIZEN), so
   CIVIC_IMMIGRATION>MUL 0.02 only throttles Baranians. Humans and everyone
   else still arrive normally. The intended pattern works: a tiny immortal
   elite, with other species doing the labour.

   One leak: a few lines earlier, if a world camp of that race is available,
   the code returns the camp replenish rate and skips the boost entirely. A
   Baranian settlement on the world map next door defeats the throttle.

6. THE TRAIT BLOCK IS CALLED "TRAIT", NOT "TRAITS"

   TRAITS.serRaceData reads a block named TRAIT (the map key is the singular).
   Every vanilla race file carries a TRAITS block full of FIGHTER, GLUTTON and
   SPRINTER, and none of it is read by anything. Valid trait keys are the file
   names in assets\init\race\trait\.

7. DEAD KEYS IN THE VANILLA FILES

   TECH is not read anywhere in the source. PORTRAIT_FILE in the sprite
   definition is not read either; portraits are assembled from the shared
   face part sheets via the FACE block. ADULT_AT_DAY in PROPERTIES is likewise
   ignored; adulthood is BABY_DAYS + CHILD_DAYS.

8. VALUE RANGES ARE CLAMPED SILENTLY

   POPULATION MAX is clamped 0..1, GROWTH 0.0001..1, CLIMATE entries 0..1,
   TERRAIN 0..100, TRAIT occurrence 0..1, structure and road preferences 0..1,
   WORK preferences -10000..10000. Boost values are not clamped.

   Terrain and climate entries you leave out default to 0, not to 1.


--------------------------------------------------------------------------------
REPRODUCTION
--------------------------------------------------------------------------------

A game year is 16 days (4 seasons at DAYS_PER_SEASON 4).

  Baby days             24
  Child days           200      -> adult at day 224, about 14 years
  Fertile from         day 336  = ceil(1.5 * adult day), about year 21
  Fertile until        year 210 = (lifespan - from) * 0.5 + from
  Lifespan             400 years maximum

Death is not uniform. StatsPopulation.death() draws a value skewed towards the
top of the range and returns 0.45 + 0.55 * it, so a Baranian dies somewhere
between 180 and 400 years, averaging about 349.

Reproduction is checked four times a year per fertile individual, each with a
chance of REPRODUCTION_SPEED / 4. Both genders can become a parent.

Simulating the game's own formulas over 600 years with 400 individuals:

      MUL      per century     doubling time
    0.040          -11 %       dies out
    0.047            0 %       replacement level
    0.050           +4 %       ~1700 years
    0.055          +11 %        ~660 years
    0.060          +19 %        ~395 years     <-- current setting
    0.080          +47 %        ~180 years

At 0.060 a Baranian bears about 1.1 children in a full life. Twenty starting
Baranians become roughly 40 after 300 game years.

DO NOT shrink the fertile window with PHYSICS_REPRODUCTION_AGE to suppress
births. It works, but it leaves only a few percent of the race fertile at any
moment, and a small colony then swings wildly. Measured with the window cut to
19 years: a colony of four died out in 39 percent of runs, against 9 percent
with the normal window at the same effective growth rate. Change the rate, not
the window.


--------------------------------------------------------------------------------
SPRITE SHEET
--------------------------------------------------------------------------------

Baranian.png must stay exactly 448 x 546.

  left  224 px   the picture (diffuse)
  right 224 px   normal map for lighting. Leave as is, or fill flat with
                 #8080FF. Same pixel position, shifted 224 to the right.

Inside the left half:

  x   0 - 65    body      2 columns x 18 rows of 24x24, origin (6,6), pitch 30
  x  66 - 223   lying     4 columns x  3 rows of 32x32, origin (72,6), pitch 38
                          (y 0-119 only)
  x  66 - 223   addons    8 slots, first at y 194, pitch 44
                          per slot: 2x 24x24 at x 72 and 102
                                    2x 32x32 at x 138 and 176

The 18 body rows, top to bottom (names from HSpriteConst.java):

   0  FEET_NONE (leave empty)      9  TORSO_RIGHT3
   1  FEET_RIGHT                  10  TORSO_LEFT
   2  FEET_RIGHT2                 11  TORSO_LEFT2
   3  FEET_LEFT                   12  TORSO_LEFT3
   4  FEET_LEFT2                  13  TORSO_CARRY
   5  TUNIC                       14  TORSO_OUT
   6  TORSO_STILL                 15  TORSO_OUT2
   7  TORSO_RIGHT                 16  HEAD
   8  TORSO_RIGHT2                17  SHADOW

The two tiles in a row are the two animation frames.

Addon slots: 0 armour, 2 noble cloak, 3 hair, 4 hair behind the head, rest free.

Lying block groups, left to right then top to bottom:
  PANTS, TORSO, ARMS, HEAD, SHADOW, unused

WHAT THE ART MUST LOOK LIKE

Top-down view. The figure is tiny, about 13 x 11 px, centred in its 24x24 tile.

Draw one facing only. The game rotates every row into all four directions
(paste(3, true) in RaceSheet).

Paint in greyscale. Skin, clothes, armour and hair are tinted at runtime from
the COLORS block in the sprite definition. Coloured pixels cannot be tinted
cleanly afterwards.

Separation of skin, legs and clothing happens through the rows, not through
colour markers: FEET rows are tinted with COLOR_LEG, TORSO and HEAD with
COLOR_SKIN, TUNIC with COLOR_CLOTHES.

Unused pixels must be alpha 0. Not black, not blue.

The green and blue lines in the margins are only a drawing grid. The game never
reads them, so they can stay or go.

The two icons are different: front-facing portraits, one 24x24 tile at (6,6)
resp. one 32x32 tile at (6,6), again with the normal map in the right half.
Icon sheets must satisfy (width/2 - 6) % (tile + 6) == 0 in both axes.

SHARED, NOT PER RACE

These stay vanilla and need no copies:
  sprite\race\face\*.png        portrait parts (skull, nose, eyes, hair, ...)
  sprite\race\skelleton\        skeleton
  sprite\race\sleep\            blanket
  sprite\race\extra\            tools, water, trolley
  sprite\race\face\addon\       crown, helmet, raider gear

To give the Baranians their own portrait parts, add a new file next to the
vanilla ones, e.g. sprite\race\face\SkullBaranian.png (416 wide, height a
multiple of 60, 4 frames per row, cell 40x48 at x 6+52*col, y 6+60*row) and
reference it in the FACE block as  SkullBaranian: 0.

The world map look (WORLD block: TOWN, VILLAGE, OVERLAY, WALL, TERRAIN) still
points at the vanilla human tiles and can stay that way.


--------------------------------------------------------------------------------
TUNING DIALS
--------------------------------------------------------------------------------

Rarity            POPULATION MAX 0.03 caps their share of any world region.
                  POPULATION GROWTH 0.0005 is the world-map growth rate, and
                  0.0001 is the engine minimum. CIVIC_IMMIGRATION>MUL 0.02
                  throttles arrivals into your own city.

Reproduction      PHYSICS_REPRODUCTION_SPEED>MUL, see the table above.
                  Leave PHYSICS_REPRODUCTION_AGE alone.

Lifespan          PHYSICS_DEATH_AGE>MUL, base is 100 years.
                  Long lives also mean long childhoods are cheap: BABY_DAYS
                  and CHILD_DAYS in PROPERTIES set the 224-day growing-up time.

Noble slots       CIVIC_NOBLES_MAX>ADD and CIVIC_NOBLES_RANKS_MAX>ADD.
                  Weighted by population share and then truncated to int, so
                  raise these hard if you want the effect at low headcount.
                  For reference, vanilla player level titles grant +5 nobles
                  and up to +20 promotions.

Noble quality     NOBLE_COMPETENCE>ADD plus the TRAIT block.

Power level       ROOM*>MUL 3.0 is the broad "good at everything" dial.
                  CIVIC_KNOWLEDGE>ADD 150 is the research dial; vanilla player
                  levels sit between 35 and 200, so this is roughly one extra
                  title's worth of research at full Baranian population.


--------------------------------------------------------------------------------
KNOWN INCONSISTENCIES
--------------------------------------------------------------------------------

The race is not balanced against the vanilla species and is not meant to be.
It was built to the brief "absolutely overpowered, but almost never reproduces
and almost never migrates".


--------------------------------------------------------------------------------
CHANGELOG
--------------------------------------------------------------------------------

1.0   Initial build. Race, texts, biography lines, sprite wiring.

1.1   Reproduction reworked. PHYSICS_REPRODUCTION_AGE>MUL 0.1 removed; it cut
      the fertile window to 19 years of a 400-year life, which both read
      absurdly and made the population collapse. PHYSICS_REPRODUCTION_SPEED>MUL
      raised from 0.02 (far below replacement, guaranteed extinction) to 0.060.
      Description and CONS text corrected to match.

      ROOM_MINE* and ROOM_REFINER* replaced with exact per-room keys. As
      wildcards they were weak and silently discarded, leaving mines and
      refiners at the ROOM* bonus of 1.5 while the pros/cons text claimed they
      were a weakness. Mines now 0.6, refiners 0.75. The five intellectual
      rooms were rewritten as exact keys too, for the same failure mode.

      Sprite art split out into own files (copies of the human art) so the
      Baranians can be repainted without touching the human race.

1.2   Production, construction and combat raised to match the brief.

      Mines went from a 0.6 penalty to a 3.5 bonus, and the matching WORK
      preferences flipped from negative to positive so Baranians are no
      longer unhappy doing the job they are now good at. Refiners and
      workshops likewise.

      ROOM*>MUL raised from 1.5 to 3.0, so every room including those added
      by other mods is covered. Builder, hauler, transport, stockpile,
      barracks, archery and artillery called out explicitly above that.

      Battle skills raised from x3.0 to x4.0, morale to x4.0, block to x3.0,
      bow to x3.0, formation to +3.0, every damage type from +60 to +80, and
      health from x3.0 to x4.0.

      PROS/CONS and the description corrected: the mining weakness is gone,
      and CHALLENGE dropped from Hard to Easy, which is now honest.

1.3   All WORLD_* boosts removed. They are evaluated per world region, not
      per settlement, so they did nothing for your own city while handing
      every NPC faction with Baranians in its provinces the identical bonus.
      The advantage now lives entirely inside your own walls.
