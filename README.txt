BARANIANS - Race mod for Songs of Syx 0.71.x

INSTALL
This folder belongs in:
  C:\Users\Asus\AppData\Roaming\songsofsyx\mods\Baranians
Enable it in the game launcher under MODS, then start a new world.
Enable DEVELOPER and DEBUG in the launcher while testing so parse errors are shown.

FILES
  _Info.txt                                        mod metadata shown in the launcher
  Baranian_SheetGuide.png                          visual map of the sprite sheet
  V71\assets\init\race\BARANIAN.txt                all stats, boosts, population, traits
  V71\assets\init\race\sprite\BARANIAN.txt         appearance definition
  V71\assets\text\race\BARANIAN.txt                name, description, pros/cons, army names
  V71\assets\text\race\bio\specific\Baranian.txt   citizen biography lines
  V71\assets\sprite\race\Baranian.png              body sheet          448 x 546
  V71\assets\sprite\race\infant\Baranian.png       infant sheet        352 x  22
  V71\assets\sprite\icon\24\race\Baranian.png      small icon           72 x  36
  V71\assets\sprite\icon\32\race\Baranian.png      large icon           88 x  44

The four PNGs are copies of the vanilla human art, already renamed and already
wired up. Repaint them in place - no file names or paths need to change.
They are Songs of Syx assets, so do not redistribute the mod with them untouched.


=== HOW THE BODY SHEET WORKS ===============================================

Baranian.png must stay exactly 448 x 546.

  left  224 px   the picture (diffuse)
  right 224 px   normal map for lighting. Leave it as is, or fill it flat
                 with #8080FF. Same pixel position, just shifted 224 to the right.

Inside the left half:

  x   0 - 65    body      2 columns x 18 rows of 24x24, origin (6,6), pitch 30
  x  66 - 223   lying     4 columns x  3 rows of 32x32, origin (72,6), pitch 38
                          (y 0-119 only)
  x  66 - 223   addons    8 slots, first at y 194, pitch 44
                          per slot: 2x 24x24 at x 72 and 102
                                    2x 32x32 at x 138 and 176

The 18 body rows, top to bottom:

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


=== WHAT THE ART MUST LOOK LIKE ============================================

Top-down view. The figure is tiny, about 13 x 11 px, centred in its 24x24 tile.

Draw one facing only. The game rotates every row into all four directions.

Paint in greyscale. Skin, clothes, armour and hair are tinted at runtime from
the COLORS block in V71\assets\init\race\sprite\BARANIAN.txt. Coloured pixels
cannot be tinted cleanly afterwards.

Separation of skin, legs and clothing happens through the rows, not through
colour markers: FEET rows are tinted with COLOR_LEG, TORSO and HEAD with
COLOR_SKIN, TUNIC with COLOR_CLOTHES.

Unused pixels must be alpha 0. Not black, not blue.

The green and blue lines in the margins are only a drawing grid. The game
never reads them, so they can stay or go.

The two icons are different: they are front-facing portraits, one 24x24 tile
at (6,6) resp. one 32x32 tile at (6,6), again with the normal map in the
right half of the file.


=== SHARED, NOT PER RACE ===================================================

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


=== TUNING =================================================================

Rarity            BARANIAN.txt -> POPULATION MAX / GROWTH, and CIVIC_IMMIGRATION>MUL
Reproduction      PHYSICS_REPRODUCTION_SPEED>MUL and PHYSICS_REPRODUCTION_AGE>MUL
Lifespan          PHYSICS_DEATH_AGE>MUL   (base is 100 years, 4.0 = 400 years)
Noble slots       CIVIC_NOBLES_MAX>ADD and CIVIC_NOBLES_RANKS_MAX>ADD
                  These are weighted by the Baranian share of your population,
                  so a city that is 10 percent Baranian gets 10 percent of the value.
Noble quality     NOBLE_COMPETENCE>ADD, plus the TRAIT block (COMPETENT at 1.0
                  gives every Baranian a further +0.5 competence)
Childhood         PROPERTIES BABY_DAYS and CHILD_DAYS (a year is 16 days)
