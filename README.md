===
                           SCIPATH WAYFARER 🌍
       A PROCEDURAL POST-APOCALYPTIC RPG WITH A LIVING CIVILIZATION
===

Created by Matthew Taraschke
Version 1.0 · 2026


PLAY NOW
===

https://behelit2.github.io/Scipath-Wayfarer/


THE SHORT VERSION
===

Scipath Wayfarer is an open-world, systems-driven RPG set 350 years after a
nuclear catastrophe shattered civilization.

It combines:

  • A vast, continuously generated wilderness.
  • A ten-region campaign against ten mechanically distinct bosses.
  • Turn-based encounters with visible enemy intentions.
  • Villages with supplies, materials, security, prosperity, and memory.
  • Reconstruction routes, equipment-supported patrols, and protected roads.
  • Confederations, trade agreements, commercial cargo, and emergency relief.
  • Thirty authored old-world discoveries placed differently in every world.
  • Persistent radio towers with selectable broadcasts and regional influence.
  • Multi-stage airship construction and a permanent fleet of movable vessels.
  • A world that continues developing after the main campaign is complete.

Every road, settlement, crisis, patrol, broadcast, discovery, trade route, and
airship belongs to the same persistent seeded world.

The in-game Instruction Manual covers controls and detailed playing guidance.
This README presents the game, its engine, its simulated systems, their
interactions, and the complete procedural content catalog.


CONTENTS
===

  01. The Game
  02. The Engine in Plain English
  03. Everything the World Simulates
  04. Emergent Possibilities
  05. Complete Procedural Generation Atlas
  06. Persistence and Portable Saves
  07. Running and Hosting
  08. Audio Assets
  09. Credits


===
01. THE GAME
===

Scipath Wayfarer is a retro-styled post-apocalyptic RPG, exploration adventure,
settlement simulation, and reconstruction sandbox contained inside a browser
game.

The old world is gone. Its roads, laboratories, shelters, communications
systems, military facilities, power stations, and machines remain scattered
across an immense wilderness. Humanity survives in small feudal settlements
while ten regional rulers preserve the final command of the civilization that
destroyed itself.

The result is a world built from two equally important layers:

THE ADVENTURE
-------------------------------------------------------------------------------

  • Explore an enormous seeded world.
  • Cross Greenlands, Forests, Wastes, Frozen Reaches, Coasts, and Seas.
  • Encounter biome-specific creatures and regional mini bosses.
  • Confront ten regional bosses with ten distinct combat patterns.
  • Recover equipment, provisions, and old-world salvage.
  • Discover thirty unique historical locations.
  • Trace the final testimony of the old civilization.
  • Build and operate a persistent fleet of airships.

THE LIVING WORLD
-------------------------------------------------------------------------------

  • Discover villages with persistent names and residents.
  • Watch settlement conditions rise, fall, strain, and recover.
  • Liberate regions and remove continuing hostile pressure.
  • Connect villages with reconstruction routes.
  • Donate equipment to create wider patrol corridors.
  • Form confederations from connected independent settlements.
  • Establish foreign trade agreements without erasing political borders.
  • Carry commercial exports between confederations.
  • Answer emergency requests created by real settlement crises.
  • Activate radio towers that affect sound, security, and coordination.
  • Read journals and dialogue that remember what has changed.

THE CONTINUING WORLD
-------------------------------------------------------------------------------

Defeating all ten bosses completes the central campaign while preserving the
entire generated world.

Exploration, settlement development, reconstruction, trade, relief, radio
operation, discovery hunting, and airship construction continue as one
persistent civilization-building simulation.


===
02. THE ENGINE IN PLAIN ENGLISH
===

Scipath Wayfarer uses a purpose-built engine written in vanilla JavaScript.
The world, interface, combat, simulation, rendering, journals, save system, and
game logic live inside one self-contained HTML entry point. Audio files sit
beside it.

There is no framework, server-side game process, database, installer, or build
pipeline. The browser runs the complete game.


HOW THE WORLD EXISTS
-------------------------------------------------------------------------------

The world seed acts like the world's DNA.

  • The seed and a coordinate determine the terrain at that coordinate.
  • The same seed and coordinate always rebuild the same base tile.
  • The engine generates nearby tiles when they are needed.
  • It does not need to store an enormous finished map.
  • The save records everything meaningful that happens on top of that map.

In compact form:

  WORLD SEED + COORDINATES
       │
       ├── Terrain
       ├── Biome
       ├── Region
       ├── Villages
       ├── Ruins
       ├── Radio towers
       ├── Boss lairs
       └── Discovery sites

  GENERATED WORLD + SAVED HISTORY
       │
       ├── Named settlements
       ├── Explored ruins
       ├── Revealed discoveries
       ├── Defeated bosses
       ├── Active broadcasts
       ├── Reconstruction links
       ├── Patrols
       ├── Confederations
       ├── Trade agreements
       ├── Settlement conditions
       ├── Crises and deliveries
       ├── Airships
       └── Remembered conversations


THE ENGINE'S MAJOR SYSTEMS
-------------------------------------------------------------------------------

  • WORLD FORGE
    Terrain noise, coastlines, climates, biomes, regions, landmarks, lairs,
    discoveries, and starting positions.

  • CONTENT FORGE
    Village identities, residents, professions, shops, enemies, equipment,
    salvage, exports, missions, and assembly targets.

  • HERO STATE
    Position, refuge, health, level, experience, gold, provisions, inventory,
    equipment, temporary wards, and current travel mode.

  • COMBAT
    Damage, armor, penetration, critical hits, evasion, retaliation, wards,
    weakening, multi-strike attacks, regeneration, life stealing, rewards,
    retreat, victory, and defeat.

  • SETTLEMENT SIMULATION
    Production, consumption, adaptation, incidents, good seasons, shipments,
    shortages, prosperity, crises, relief, and recovery.

  • RECONSTRUCTION
    Village links, route costs, donated supplies, patrol equipment, corridor
    geometry, encounter protection, and shipment quality.

  • POLITICS
    Connected settlement groups, confederation formation, membership,
    founding cities, exports, and foreign agreements.

  • LOGISTICS
    Commercial cargo, emergency relief, mission rewards, mission history, and
    destination compasses.

  • AIRSHIPS
    Component selection, outward and return journeys, assembly progress,
    persistent vessel identities, flight, landing, and fleet positions.

  • WORLD MEMORY
    Boss reports, testimony, discoveries, village notes, dialogue memory,
    Network Overview, and Network Chronicle.

  • PRESENTATION
    Canvas-rendered terrain and landmarks, responsive interface panels,
    programmatic icons, combat telegraphs, journals, and the illustrated
    in-game Instruction Manual.

  • AUDIO
    Combat effects, sequential impacts, sea music, radio broadcasts, and one
    continuous engine loop for airship flight.

  • PERSISTENCE
    Browser saves, validation, migration, automatic saving, and portable JSON
    import and export.


FOUR KINDS OF RANDOMNESS
-------------------------------------------------------------------------------

Scipath Wayfarer separates randomness so the world can be permanent without
becoming predictable.

  1. COORDINATE-HASHED GENERATION

     • Terrain
     • Landmark rolls
     • Shop availability
     • Resident knowledge
     • Radio and export identity properties
     • Stable coordinate-based details

  2. SEEDED LOCAL GENERATORS

     • Village names and residents
     • Boss lair placement
     • Discovery placement
     • Ruin salvage
     • Airship component assignments

  3. LIVE ADVENTURE RANDOMNESS

     • Encounter checks
     • Creature selection
     • Enemy archetypes
     • Mini-boss selection
     • Combat variance
     • Critical hits
     • Evasion
     • Retreat
     • Conversation selection
     • Commercial destinations

  4. DETERMINISTIC SIMULATION RANDOMNESS

     • Settlement incidents
     • Good seasons
     • Shipment outcomes
     • Pressure selection
     • Incident severity

Simulation events are tied to the world seed, settlement cycle, and event
identity. A saved world therefore preserves its own history instead of
rerolling completed developments.


RENDERING AND INTERFACE
-------------------------------------------------------------------------------

  • Canvas 2D draws the world map.
  • Terrain colors and landmark art are generated programmatically.
  • HTML and CSS provide the HUD, dialogs, journals, shops, and village tabs.
  • requestAnimationFrame coordinates smooth map rendering.
  • Dirty flags redraw only when the visible state changes.
  • A bounded tile cache keeps nearby world generation fast.
  • Six tile sizes support compact and enlarged map views.
  • World modes prevent movement while an interaction is active.
  • Transactions confirm their requirements before changing persistent state.
  • Responsive layouts support desktop and touch-oriented screens.


===
03. EVERYTHING THE WORLD SIMULATES
===

THE WAYFARER
-------------------------------------------------------------------------------

  • Current coordinates
  • Registered refuge coordinates
  • Icon color
  • Current and maximum health
  • Base attack and defense
  • Equipped attack and defense
  • Level
  • Experience
  • Next-level requirement
  • Gold
  • Provisions
  • Inventory
  • Equipped weapon
  • Equipped armor
  • Temporary ward charges
  • Foot, boat, or airship travel
  • Airship provision phase
  • Victories
  • Traveled tiles
  • Campaign completion


THE WORLD
-------------------------------------------------------------------------------

  • Six terrain types
  • Twenty color variations per terrain type
  • Radial regional difficulty
  • Coastlines and islands
  • Villages
  • Ruins
  • Radio towers
  • Ten boss lairs
  • Thirty discovery sites
  • Grounded airships
  • Active compass targets
  • Revealed and unrevealed landmarks
  • Explored and unexplored locations


TRAVEL AND LOGISTICS
-------------------------------------------------------------------------------

  • Foot movement
  • Boat rental
  • Sea provision consumption
  • Airship provision consumption
  • Travel speed by transport
  • Encounter eligibility by transport
  • Provision exhaustion
  • Health loss after provision exhaustion
  • Landing terrain
  • Landing obstructions
  • Persistent grounded vessel positions
  • Settlement time advanced by every traveled tile


COMBAT
-------------------------------------------------------------------------------

  • Hero attack
  • Hero defense
  • Weapon critical chance
  • Weapon armor penetration
  • Armor evasion
  • Armor retaliation
  • Enemy armor
  • Direct-damage items
  • Armor reduction
  • Temporary wards
  • Delayed weakening
  • Multi-strike attacks
  • Enemy regeneration
  • Enemy life stealing
  • Turn-indexed attack patterns
  • Health-threshold transformations
  • Retreat probability
  • Experience rewards
  • Gold rewards
  • Level advancement
  • Regional victory rewards
  • Difficulty-specific healing and penalties


SETTLEMENTS
-------------------------------------------------------------------------------

Every discovered village receives four persistent conditions:

  • Supplies
  • Materials
  • Security
  • Prosperity

Those conditions respond to:

  • Biome
  • Shops
  • Everyday consumption
  • Regional danger
  • Regional liberation
  • Radio coverage
  • Local adaptation
  • Resource abundance
  • Material conversion
  • Incidents
  • Good seasons
  • Informal exchange
  • Reconstruction routes
  • Patrol quality
  • Confederation membership
  • Trade agreements
  • Commercial deliveries
  • Emergency relief
  • Crisis recovery


RECONSTRUCTION
-------------------------------------------------------------------------------

  • Pending relay journeys
  • Link endpoints
  • Distance-based construction costs
  • Gold donations
  • Provision donations
  • Consumable donations
  • Free endpoint inns
  • Formal exchange routes
  • Weapon donations
  • Armor donations
  • Patrol strength
  • Patrol radius
  • Land-corridor geometry
  • Encounter reduction
  • Shipment capacity
  • Shipment reliability


POLITICS AND TRADE
-------------------------------------------------------------------------------

  • Independent settlements
  • Connected settlement components
  • Confederation formation
  • Confederation membership
  • Founding villages
  • Founding resource cities
  • Generated political names
  • Biome-based exports
  • Foreign trade agreements
  • Passive commercial prosperity
  • Commercial delivery offers
  • Emergency relief offers
  • Sealed cargo
  • Destination selection
  • Distance-and-region rewards
  • Completed, cancelled, and failed mission history


WORLD MEMORY
-------------------------------------------------------------------------------

  • Persistent village names
  • Resident identities
  • Boss reports
  • Boss coordinates
  • Boss compass selection
  • Final testimony
  • Discovered historical accounts
  • Radio settings
  • Settlement condition trends
  • Significant shipment records
  • Crisis history
  • Relief history
  • Reconstruction history
  • Confederation membership
  • Trade relationships
  • Airship assembly progress
  • Recent dialogue lines
  • Recent dialogue topics
  • Structural changes noticed by residents


===
04. EMERGENT POSSIBILITIES
===

Scipath Wayfarer's greatest strength is not any individual mechanic. It is the
way every mechanic can change several others.

These are system chains, not scripted scenes.


REGIONAL LIBERATION
-------------------------------------------------------------------------------

  BOSS DEFEATED
       → Regional encounters are halved
       → Known settlements gain Security and Prosperity
       → Continuing boss pressure ends
       → Reconstruction Boards unlock
       → Formal routes become possible
       → Confederations can emerge
       → Trade and foreign relief can follow


EQUIPMENT AS PERSONAL OR CIVIC POWER
-------------------------------------------------------------------------------

  WEAPON + ARMOR
       → Equip them for personal combat

  OR

  WEAPON + ARMOR
       → Donate them to a route patrol
       → Patrol radius is calculated from their combined strength
       → More land receives encounter protection
       → Shipments gain capacity and reliability
       → Settlements recover more effectively


A REGIONAL ECONOMY
-------------------------------------------------------------------------------

  COAST OR GREENLANDS
       → Stronger Supplies production

  FOREST, WASTES, OR FROZEN REACH
       → Stronger Materials production

  RECONSTRUCTION ROUTE
       → Surplus can move toward shortage
       → Successful aid can raise Prosperity
       → Better conditions change future production
       → A receiver can later become a donor


RADIO AS INFRASTRUCTURE
-------------------------------------------------------------------------------

  ACTIVE TOWER
       → Creates a geographic broadcast
       → Supports Security growth in covered settlements
       → Improves shipments involving covered endpoints
       → Becomes a possible Navigation Coil source
       → Connects sound, economics, logistics, and construction


COMPOUND ROAD SAFETY
-------------------------------------------------------------------------------

  DEFEATED REGIONAL BOSS
       → Encounter chance × 0.5

  GUARDED PATROL CORRIDOR
       → Encounter chance × 0.5

  BOTH TOGETHER
       → Encounter chance × 0.25


CRISIS, DIPLOMACY, AND RELIEF
-------------------------------------------------------------------------------

  CONDITION REMAINS DIRE
       → Settlement crisis opens
       → Internal network aid may resolve it

  OR

  FOREIGN TRADE AGREEMENT
       → Eligible partner posts emergency relief
       → Source settlement contributes real reserves
       → Wayfarer carries sealed cargo
       → Destination receives a major recovery boost
       → Chronicle records the complete event


POLITICAL GROWTH WITHOUT POLITICAL ERASURE
-------------------------------------------------------------------------------

  THREE CONNECTED INDEPENDENT VILLAGES
       → Confederation forms
       → Founders, name, resource city, and export are generated
       → Internal formal routes gain capacity

  CONFEDERATION + FOREIGN CONFEDERATION
       → Agreement creates commerce and relief opportunities
       → Both governments retain separate identities


TRAVEL AS WORLD TIME
-------------------------------------------------------------------------------

  EVERY 24 TRAVELED TILES
       → One settlement cycle advances
       → Villages produce and consume
       → Incidents and good seasons resolve
       → Shipments move or are lost
       → Crises open or recover
       → Trade relationships provide prosperity

An airship crosses tiles at twice the ordinary movement rate, linking personal
mobility to the real-time pace of the wider simulation.


AIRSHIP CONSTRUCTION AS A WORLD-SPANNING JOURNEY
-------------------------------------------------------------------------------

  DISCOVERY SITE
       → Lift Envelope Material

  DEFEATED BOSS LAIR
       → Stabilizer Gyroscope

  RADIO TOWER
       → Navigation Coil

  THREE OUTWARD-AND-RETURN JOURNEYS
       → Persistent completed vessel
       → New long-distance travel possibilities
       → A growing geographic fleet


A WORLD THAT RECOGNIZES ITS OWN HISTORY
-------------------------------------------------------------------------------

  NEW LINK
  NEW PATROL
  WIDER PATROL
  REGIONAL VICTORY
  CONFEDERATION MEMBERSHIP
  TRADE AGREEMENT
  SETTLEMENT CRISIS
  RECENT SHIPMENT
       → Village Notes change
       → Network Chronicle changes
       → Resident dialogue changes
       → The world acknowledges what happened


===
05. COMPLETE PROCEDURAL GENERATION ATLAS
===

NOTATION
-------------------------------------------------------------------------------

  ×          Cartesian combination
  {A, B}     One selection from the listed set
  [A..B]     Inclusive integer range
  P(N, K)    Ordered selection of K unique entries from N entries

Finite source catalogs are printed in full below. Continuing or numerical
spaces are represented by their exact range and combination rule.


5.1 WORLD GENERATION
===

WORLD SEED
-------------------------------------------------------------------------------

  • One unsigned 32-bit seed
  • Range: 0 through 4,294,967,295


TERRAIN NOISE FIELDS
-------------------------------------------------------------------------------

  Continental elevation
    • Coordinate scale: 0.0048
    • Octaves: 5
    • Offset: none

  Coastal detail
    • Coordinate scale: 0.018
    • Octaves: 4
    • Offset: x + 4300, y - 2700

  Island detail
    • Coordinate scale: 0.038
    • Octaves: 3
    • Offset: x - 8100, y + 6100

  Moisture
    • Coordinate scale: 0.009
    • Octaves: 4
    • Offset: x + 12000, y - 9000

  Local climate
    • Coordinate scale: 0.0035
    • Octaves: 3
    • Offset: x - 3500, y + 7300

Each octave doubles frequency and halves amplitude.

  Raw elevation
    = 0.74 × continental
    + 0.20 × coastal detail
    + 0.06 × island detail

  Final elevation
    = 0.5 + (raw elevation - 0.5) × 1.55


COMPLETE BIOME CLASSIFICATION
-------------------------------------------------------------------------------

  1. Sea
     • Elevation below 0.495
     • Base RGB: 22, 70, 145

  2. Coast
     • Elevation from 0.495 to below 0.515
     • Base RGB: 211, 191, 121

  3. Frozen Reach
     • Remaining land with elevation at least 0.69
       OR
     • Remaining land with elevation at least 0.635 and climate below 0.47
     • Base RGB: 232, 238, 240

  4. Wastes
     • Remaining land with moisture below 0.425
     • Base RGB: 207, 171, 70

  5. Forest
     • Remaining land with moisture above 0.565
     • Base RGB: 25, 85, 31

  6. Greenlands
     • All remaining land
     • Base RGB: 49, 132, 51


TERRAIN COLOR VARIATION
-------------------------------------------------------------------------------

  • Shared RGB offset: every integer from -10 through +9
  • Variants per biome: 20
  • Biomes: 6
  • Underlying terrain-color combinations: 120


REGIONAL BANDS
-------------------------------------------------------------------------------

  Region = min(10, floor(distance from origin / 220) + 1)

  • Region 1  : distance below 220
  • Region 2  : 220 to below 440
  • Region 3  : 440 to below 660
  • Region 4  : 660 to below 880
  • Region 5  : 880 to below 1100
  • Region 6  : 1100 to below 1320
  • Region 7  : 1320 to below 1540
  • Region 8  : 1540 to below 1760
  • Region 9  : 1760 to below 1980
  • Region 10 : 1980 and beyond

The coordinate world continues outward while regional strength remains capped
at ten.


BASE LANDMARK ROLL
-------------------------------------------------------------------------------

One coordinate hash creates mutually exclusive base landmarks on non-water
tiles.

  • Village
    Hash interval: [0.000000, 0.000300)
    Chance: 0.0300%

  • Ruins
    Hash interval: [0.000300, 0.000498)
    Chance: 0.0198%

  • Radio tower
    Hash interval: [0.000498, 0.000597)
    Chance: 0.0099%

  • Ordinary terrain
    Remaining interval
    Chance: 99.9403%


BASE TILE GRAMMAR
-------------------------------------------------------------------------------

  Sea
    × Ordinary terrain

  OR

  {Coast, Greenlands, Forest, Wastes, Frozen Reach}
    ×
  {Ordinary terrain, Village, Ruins, Radio tower}

  • Land categories: 5 × 4 = 20
  • Sea categories: 1
  • Base categorical tile classes: 21


OVERLAY PRIORITY
-------------------------------------------------------------------------------

  1. Boss lair
  2. Village
  3. Ruins
  4. Radio tower
  5. Discovery
  6. Ordinary terrain

A boss-lair candidate excludes water and villages. It can therefore supersede
an underlying ruin or radio roll. Discovery placement excludes all other
landmarks and discoveries. Grounded airships occupy clear landing tiles.


BOSS-LAIR PLACEMENT
-------------------------------------------------------------------------------

  • One lair per region
  • Ten lairs per world
  • Region 1 radius: 70 through 212
  • Regions 2–10 inner radius:
      (region - 1) × 220 + 8
  • Regions 2–10 outer radius:
      region × 220 - 8
  • Area-weighted seeded selection
  • Non-water, village-free candidates
  • Up to 20,000 seeded candidates
  • Coastal footing supplied when the final seeded position requires it
  • Boss identity fixed by region
  • Lair coordinate and local biome generated from the seed


DISCOVERY PLACEMENT
-------------------------------------------------------------------------------

  • Thirty discoveries
  • Three assigned to every regional band
  • Independent seeded stream
  • Minimum separation: 24 tiles
  • Excludes villages, ruins, radio towers, boss lairs, and other discoveries
  • First 160 candidates favor each discovery's preferred biome
  • Broader eligible land follows the preference pass
  • Coastal footing supports the final seeded location when required


STARTING POSITION
-------------------------------------------------------------------------------

Primary starting set:

  • Radius: up to 175 tiles from the origin
  • Eligible biomes:
      Greenlands
      Forest
      Coast
  • Excludes:
      Villages
      Ruins
      Radio towers
      Boss lairs
      Discoveries

Expanded seeded selection supplies any additional clear non-water start.


5.2 VILLAGE IDENTITIES
===

VILLAGE NAME GRAMMAR
-------------------------------------------------------------------------------

  Prefix + space + Suffix

  • Prefixes: 36
  • Suffixes: 36
  • Complete name combinations: 36 × 36 = 1,296


ALL PREFIXES
-------------------------------------------------------------------------------

  New, Fort, Saint, Old, East, West
  High, Stone, Iron, Green, Ash, Last
  North, South, Red, White, Black, Grey
  Silver, Copper, Oak, Pine, Willow, Cedar
  Birch, Moss, Thorn, Frost, Ember, Dawn
  Dusk, Sun, Moon, Wolf, Raven, Still


ALL SUFFIXES
-------------------------------------------------------------------------------

  Haven, Crossing, Watch, Ford, Rest, Vale
  Gate, Shelter, Market, Reach, Hold, Harbor
  Bridge, Keep, Hollow, Field, Hill, Ridge
  Brook, Creek, Spring, Falls, Bend, Grove
  Wood, Meadow, Heath, Marsh, Shore, Cove
  Point, Bluff, Pass, Landing, Refuge, Outpost


VILLAGE SERVICE ROLLS
-------------------------------------------------------------------------------

The inn is universal. Each shop category receives its own 70% availability
check.

All eight possible service sets:

  1. Inn
  2. Inn + Weapon Shop
  3. Inn + Armor Shop
  4. Inn + Item Shop
  5. Inn + Weapon Shop + Armor Shop
  6. Inn + Weapon Shop + Item Shop
  7. Inn + Armor Shop + Item Shop
  8. Inn + Weapon Shop + Armor Shop + Item Shop

Exact set probabilities:

  • Inn only: 2.7%
  • Each exact one-shop combination: 6.3%
  • Each exact two-shop combination: 14.7%
  • All three shops: 34.3%


RESIDENT COUNT
-------------------------------------------------------------------------------

  • One resident
  • Two residents
  • Three residents


ALL 96 RESIDENT NAMES
-------------------------------------------------------------------------------

  Ada, Alden, Bram, Cora, Dain, Elia
  Fenn, Greta, Hale, Iris, Jora, Kellan
  Lina, Marek, Nora, Orin, Pella, Quinn
  Rhea, Silas, Tamsin, Ulric, Vera, Wren

  Aeron, Anwen, Arlen, Bastian, Bryn, Calder
  Cassia, Cedric, Daria, Delia, Edric, Eira
  Elric, Ember, Enid, Esme, Evren, Faris
  Fiora, Galen, Gareth, Gilda, Hadrian, Hazel

  Idris, Isolde, Jasper, Kael, Keira, Leif
  Lenora, Lucan, Lyra, Maela, Mira, Niall
  Odette, Oren, Petra, Ronan, Rowan, Sable
  Selene, Soren, Talia, Tarin, Thane, Tobin

  Torin, Valen, Veda, Willa, Yara, Yorin
  Zara, Zev, Alma, Brina, Corvin, Dorian
  Elowen, Freya, Hector, Iona, Liora, Maris
  Nessa, Oskar, Perrin, Roslyn, Sera, Varek


ALL 11 PROFESSIONS
-------------------------------------------------------------------------------

  • Farmer       → Supplies
  • Hunter       → Security
  • Guard        → Security
  • Scholar      → Prosperity
  • Scavenger    → Materials
  • Healer       → Supplies
  • Trader       → Prosperity
  • Cartographer → Security
  • Mechanist    → Materials
  • Fisher       → Supplies
  • Storykeeper  → Lowest local pressure


ALL FOUR GREETING PERSONALITIES
-------------------------------------------------------------------------------

  • Practical
  • Warm
  • Wary
  • Reflective


RESIDENT COMPOSITION
-------------------------------------------------------------------------------

Each resident combines:

  • One of 96 names
  • One of 11 professions
  • One of 4 greeting personalities
  • Boss knowledge: Yes or No

Resident names are unique inside a village. Professions may repeat.

Per-resident non-name combinations:

  11 professions × 4 personalities × 2 knowledge states = 88

Ordered resident-roster combinations:

  • One resident:
      P(96, 1) × 88
      = 8,448

  • Two residents:
      P(96, 2) × 88²
      = 70,625,280

  • Three residents:
      P(96, 3) × 88³
      = 584,212,316,160

  • Complete ordered resident-roster catalog:
      584,282,949,888 combinations


CORE VILLAGE PROFILE GRAMMAR
-------------------------------------------------------------------------------

  1,296 names
    × 8 service sets
    × 5 land biomes
    × 10 regions
    × 584,282,949,888 resident rosters

  = 302,892,281,221,939,200 raw categorical village profiles

Initial pressure jitter adds:

  11 Supplies offsets
    × 11 Materials offsets
    × 11 Security offsets
    × 11 Prosperity offsets

  = 14,641 initial jitter combinations

Complete raw village profile space before ongoing simulation:

  302,892,281,221,939,200 × 14,641

  = 4,434,645,889,370,411,827,200 combinations


5.3 CONTEXTUAL DIALOGUE
===

ACTIVE AUTHORED RESIDENT CATALOG
-------------------------------------------------------------------------------

  • Four personality greeting pools:
      12 lines

  • Eleven profession pools:
      33 lines

  • Five biome-lore pools:
      25 lines

  • General advice pool:
      17 lines

  • Twenty-six situational pools:
      78 lines

  • Active resident catalog:
      165 authored selectable lines

  • Arrival report pools:
      30 additional lines

Dynamic settlement sentences are assembled from live pressure, trend, event,
profession, and crisis values.


ALL 26 SITUATIONAL TOPICS
-------------------------------------------------------------------------------

  01. Boss directions
  02. Boss unknown
  03. Regional peace
  04. Campaign peace
  05. Isolated settlement
  06. Basic links
  07. Mixed guarded and unguarded links
  08. All direct links guarded
  09. Widened patrol
  10. Wider connected network
  11. Pending relay start
  12. Pending relay arrival
  13. Pending duplicate link
  14. Nearby patrol
  15. Wounded Wayfarer
  16. New link remembered
  17. New guard remembered
  18. Wider patrol remembered
  19. Regional victory remembered
  20. Campaign victory remembered
  21. Network growth remembered
  22. Independent politics
  23. Confederation membership
  24. Confederation membership change
  25. Trade partners
  26. New foreign trade


ALL REMEMBERED STRUCTURAL NOTICE TYPES
-------------------------------------------------------------------------------

  • New link
  • New guard
  • Wider patrol
  • Regional victory
  • Campaign victory
  • Network growth
  • Confederation joined
  • Trade opened


NETWORK MILESTONES RECOGNIZED BY DIALOGUE
-------------------------------------------------------------------------------

  • 3 connected villages
  • 5 connected villages
  • 10 connected villages
  • 20 connected villages
  • 50 connected villages
  • 100 connected villages


DIALOGUE COMPOSITION GRAMMAR
-------------------------------------------------------------------------------

  Optional personality greeting
    +
  {Profession, Biome, Advice, Situation, Simulation} topic line
    +
  Live substitutions

Live substitutions include:

  • Hero name
  • Village name
  • Neighboring village name
  • Boss name
  • Boss identity
  • Region
  • Coordinates
  • Distance
  • Direction
  • Direct-link count
  • Guarded-link count
  • Unguarded-link count
  • Connected-network size
  • Indirect settlement name
  • Patrol radius
  • Pending relay origin
  • Inn price
  • Gold
  • Provisions
  • Boat fee
  • Provision-exhaustion damage
  • Confederation name
  • Confederation membership count
  • Resource city
  • Export
  • Foreign partners
  • Settlement pressure
  • Condition band
  • Rising, falling, or steady trend
  • Active crisis
  • Latest significant event

Recent lines and recent topic families are remembered, allowing residents to
rotate through relevant conversation instead of behaving like static signs.


5.4 ORDINARY CREATURES
===

GREENLANDS
-------------------------------------------------------------------------------

  Mutant Hare
  Razor Boar
  Feral Hound
  Road Bandit
  Ash Stag
  Scavenger
  Horned Slime
  Ruined Knight
  Boneback Bison
  Wandering Marauder
  Thorn Lizard
  War Hound


FOREST
-------------------------------------------------------------------------------

  Glowcap Crawler
  Forest Bat
  Goblin Forager
  Spore Wolf
  Barkhide Ent
  Web Stalker
  Moss Ogre
  Root Wraith
  Toxic Dryad
  Canopy Hunter
  Ancient Treant
  Night Howler


WASTES
-------------------------------------------------------------------------------

  Glass Scarab
  Sand Imp
  Cactus Beast
  Dust Raider
  Irradiated Mummy
  Sand Golem
  Dune Stalker
  Ash Djinn
  Burrowing Wyrm
  Sun Vulture
  Tomb Guardian
  Waste Reaver


FROZEN REACH
-------------------------------------------------------------------------------

  Frost Hare
  Ice Wolf
  Pale Imp
  Snow Troll
  Ice Golem
  Frost Giant
  Blizzard Spirit
  White Wyrm
  Ruins Yeti
  Cold Wraith
  Shard Bear
  Aurora Hunter


COAST
-------------------------------------------------------------------------------

  Iron Crab
  Razor Gull
  Coast Bandit
  Shell Beast
  Tide Spirit
  Sea Raider
  Salt Slime
  Wave Elemental
  Marsh Serpent
  Drowned Sailor
  Reef Stalker
  Storm Gull


ALL ENEMY ARCHETYPES
-------------------------------------------------------------------------------

  Aggressive
    • HP multiplier: 0.85
    • Attack multiplier: 1.18
    • Defense multiplier: 0.85

  Stalwart
    • HP multiplier: 1.25
    • Attack multiplier: 0.90
    • Defense multiplier: 1.08

  Armored
    • HP multiplier: 0.95
    • Attack multiplier: 0.95
    • Defense multiplier: 1.25

  Balanced
    • HP multiplier: 1.00
    • Attack multiplier: 1.00
    • Defense multiplier: 1.00


ORDINARY CREATURE COMBINATION SPACE
-------------------------------------------------------------------------------

  5 biomes
    × 12 biome-specific names
    × 4 archetypes
    × 10 regions

  = 2,400 categorical ordinary creatures per difficulty

Across all three difficulties:

  2,400 × 3 = 7,200 categorical ordinary creature configurations

Numerical variance, combat history, current health, armor state, weakening,
wards, and turn state expand each configuration further.


5.5 MINI BOSSES
===

MINI-BOSS SELECTION
-------------------------------------------------------------------------------

  • Chance within an eligible random encounter: 10%
  • HP multiplier: 2.00
  • Attack multiplier: 1.15
  • Defense multiplier: 1.15
  • Gold multiplier: 1.80
  • XP multiplier: 1.80


ALL RANKS
-------------------------------------------------------------------------------

  • Regions 1–3  : Alpha
  • Regions 4–6  : Elite
  • Regions 7–10 : Dread


ALL BIOME-AND-TIER PATTERNS
-------------------------------------------------------------------------------

  GREENLANDS
    • Alpha : Stampeding Blow  → Cleave
    • Elite : Pack Dominance   → Rally
    • Dread : Blood Frenzy     → Meltdown

  FOREST
    • Alpha : Fungal Renewal       → Regrowth
    • Elite : Parasitic Roots      → Siphon
    • Dread : Blinding Sporeburst  → Whiteout

  WASTES
    • Alpha : Glasshide Shell  → Plating
    • Elite : Shatterfang      → Piercing
    • Dread : Solar Overload   → Reactor

  FROZEN REACH
    • Alpha : Icebound Armor     → Plating
    • Elite : Killing Blizzard   → Whiteout
    • Dread : Aurora Discharge   → Reactor

  COAST
    • Alpha : Crashing Tide       → Cleave
    • Elite : Reefbreaker         → Piercing
    • Dread : Twin Tidal Strike   → Broadside


MINI-BOSS NAME GRAMMAR
-------------------------------------------------------------------------------

  Base Creature Name + " - " + {Alpha, Elite, Dread}


MINI-BOSS COMBINATION SPACE
-------------------------------------------------------------------------------

  5 biomes
    × 12 biome-specific names
    × 4 archetypes
    × 10 regions

  = 2,400 categorical mini bosses per difficulty

Across all three difficulties:

  2,400 × 3 = 7,200 categorical mini-boss configurations


TOTAL PROCEDURAL CREATURE CATALOG
-------------------------------------------------------------------------------

  7,200 ordinary configurations
    +
  7,200 mini-boss configurations

  = 14,400 difficulty-specific categorical creature configurations

This total precedes numerical variance and live combat state.


5.6 REGIONAL BOSSES
===

  01. THE CARRION BARON
      Identity : Warlord of the inner roads
      Mechanic : Heavy Cleave
      Testimony: The Promise

  02. MOTHER GLOWCAP
      Identity : Queen of the mutating spores
      Mechanic : Spore Regrowth
      Testimony: The Custodians

  03. THE RUSTED COLOSSUS
      Identity : Guardian of a fallen reactor
      Mechanic : Fortress Plating
      Testimony: The Hidden Design

  04. KING GLASSCLAW
      Identity : Terror of the shattered wastes
      Mechanic : Piercing Claw
      Testimony: The Sleeping Arsenal

  05. THE HOLLOW GENERAL
      Identity : Commander of a dead army
      Mechanic : Rally
      Testimony: The False Warning

  06. VEYRA OF THE BLACK ROOT
      Identity : Corruptor of ancient forests
      Mechanic : Root Siphon
      Testimony: The Broken Seal

  07. THE COBALT BEHEMOTH
      Identity : A beast changed by blue fire
      Mechanic : Reactor Cycle
      Testimony: The Blue Fire

  08. ADMIRAL DREADTIDE
      Identity : Master of the poisoned coast
      Mechanic : Broadside
      Testimony: The Forsaken Fleet

  09. THE AURORA DEVOURER
      Identity : Hunter beneath the polar lights
      Mechanic : Whiteout
      Testimony: The Command Eternal

  10. EMPEROR FALLOUT
      Identity : Last tyrant of the old world's ruins
      Mechanic : Meltdown
      Testimony: The Last King


ALL TEN COMBAT MECHANICS
-------------------------------------------------------------------------------

  CLEAVE
    • Every third response uses 160% attack.

  REGROWTH
    • Every third response restores up to 10% maximum HP afterward.
    • Healing occurs when both combatants remain alive.

  PLATING
    • Odd-numbered responses gain:
      max(2, round(original defense × 0.5)) defense.

  PIERCING
    • Every third response ignores 50% of hero defense.

  RALLY
    • Attack bonus:
      min(6, response number - 1).

  SIPHON
    • Every third response heals up to half the HP actually removed.

  REACTOR
    • Every fourth response uses double attack.
    • The response immediately before it uses half attack.

  BROADSIDE
    • Every third response creates two strikes.
    • Each strike uses 65% attack.

  WHITEOUT
    • Every third response uses 125% attack.
    • Evasion is bypassed.
    • Wards remain effective.

  MELTDOWN
    • At half health or below, attack rises by 35%.
    • The increase activates immediately when the threshold is crossed.


MULTI-STRIKE RESOLUTION
-------------------------------------------------------------------------------

Each strike separately resolves:

  • Ward
  • Evasion, where eligible
  • Delayed weakening
  • Defense
  • Health removal
  • Retaliation
  • Life stealing


5.7 ENEMY NUMERICAL GENERATION
===

Let:

  L       = regional level
  v       = shared stat variance
  AHP     = archetype HP multiplier
  AATK    = archetype attack multiplier
  ADEF    = archetype defense multiplier
  MHP     = ordinary or mini-boss HP multiplier
  MATK    = ordinary or mini-boss attack multiplier
  MDEF    = ordinary or mini-boss defense multiplier
  MREWARD = ordinary or mini-boss reward multiplier


ORDINARY AND MINI-BOSS VARIANCE
-------------------------------------------------------------------------------

  v ∈ [0.90, 1.10)


ORDINARY AND MINI-BOSS FORMULAS
-------------------------------------------------------------------------------

  HP
    = max(1, round((12 + 6L) × AHP × v × MHP))

  Attack
    = max(1, round(difficulty attack × AATK × v × MATK))

  Defense
    = max(0, round((1 + 0.85L) × ADEF × v × MDEF))

  Gold
    = max(1, round(difficulty gold × v × MREWARD))

  XP
    = max(1, round((8 + 4.2L) × v × MREWARD))


ORDINARY MULTIPLIERS
-------------------------------------------------------------------------------

  MHP     = 1.00
  MATK    = 1.00
  MDEF    = 1.00
  MREWARD = 1.00


MINI-BOSS MULTIPLIERS
-------------------------------------------------------------------------------

  MHP     = 2.00
  MATK    = 1.15
  MDEF    = 1.15
  MREWARD = 1.80


REGIONAL-BOSS VARIANCE
-------------------------------------------------------------------------------

  v ∈ [0.95, 1.05)


REGIONAL-BOSS FORMULAS
-------------------------------------------------------------------------------

  HP
    = round((42 + 30L) × v)

  Attack
    = round(difficulty boss attack × v)

  Defense
    = round((2 + 1.15L) × v)

  Gold
    = round(difficulty boss gold)

  XP
    = 42 + 17L

  Emperor Fallout:
    Generated HP × 2


5.8 DIFFICULTY AND HERO PROGRESSION
===

                              WANDERER      ADVENTURER      WAYFARER
                              Easy          Normal          Hard
-------------------------------------------------------------------------------
Starting HP                   36            33              30
Starting gold                 12            9               6
First XP requirement          140           152             160
HP gained per level           6             5               4
Defense interval              2             2.5             3
Max HP per boss               4             3               2
Boss-victory healing          100%          70%             40%
Equipment resale              35%           27.5%           20%
Consumable resale             35%           22.5%           10%
Defeat gold rate              12%           18.5%           25%
Effective minimum loss        0             2               3


ALL HEROES BEGIN WITH
-------------------------------------------------------------------------------

  • Base Attack: 6
  • Base Defense: 2
  • Provisions: 200
  • Level: 1


LEVEL ADVANCEMENT
-------------------------------------------------------------------------------

  • Base Attack: +1 per level
  • Maximum HP: difficulty-specific increase
  • Health: fully restored
  • Defense: increased when the difficulty interval is crossed

For hero level H above 1:

  Next XP requirement = 4 × (35 + 18H)


DIFFICULTY-SPECIFIC ENEMY FORMULAS
-------------------------------------------------------------------------------

  EASY — WANDERER
    • Ordinary attack: 4 + 2.2L
    • Ordinary gold: 5 + 3.5L
    • Boss attack: 8 + 2.8L
    • Boss gold: 42 + 24L
    • Item-price base: 8 + 4L

  NORMAL — ADVENTURER
    • Ordinary attack: 4.5 + 2.475L
    • Ordinary gold: 3.75 + 2.6L
    • Boss attack: 9 + 3.1L
    • Boss gold: 31 + 18.5L
    • Item-price base: 10 + 5L

  HARD — WAYFARER
    • Ordinary attack: 5 + 2.75L
    • Ordinary gold: 2.5 + 1.7L
    • Boss attack: 10 + 3.4L
    • Boss gold: 20 + 13L
    • Item-price base: 12 + 6L


RETREAT PROBABILITY
-------------------------------------------------------------------------------

For ordinary creatures and mini bosses:

  min(0.78, 0.48 + 0.04 × max(0, hero level - enemy level))


DEFEAT GOLD LOSS
-------------------------------------------------------------------------------

  min(
    available gold,
    max(effective minimum loss, floor(gold × difficulty rate))
  )


5.9 WEAPONS
===

Every generated weapon family has Marks 1 through 10.

Let L be the regional mark.

WAYFARER SWORD MK L
-------------------------------------------------------------------------------

  • Attack: 3 + 2L
  • Critical chance: 6%
  • Armor penetration: 0%
  • Price: 18 + 24L


SALVAGED WAR AXE MK L
-------------------------------------------------------------------------------

  • Attack: 5 + 2L
  • Critical chance: 3%
  • Armor penetration: 0%
  • Price: 26 + 29L


REACTOR SPEAR MK L
-------------------------------------------------------------------------------

  • Attack: 2 + 2L
  • Critical chance: 8%
  • Armor penetration: 28%
  • Price: 30 + 31L


GLASSEDGE BLADE MK L
-------------------------------------------------------------------------------

  • Attack: 3 + 2L
  • Critical chance: 18%
  • Armor penetration: 8%
  • Price: 38 + 35L


WEAPON CATALOG SIZE
-------------------------------------------------------------------------------

  4 families × 10 marks = 40 generated weapon templates

Critical damage:

  round(calculated attack damage × 1.75)


5.10 ARMOR
===

Every generated armor family has Marks 1 through 10.

ROADWARDEN LEATHER MK L
-------------------------------------------------------------------------------

  • Defense: 2 + floor(1.4L)
  • Evasion: 8%
  • Retaliation: none
  • Price: 18 + 23L


SCRAP-MAIL COAT MK L
-------------------------------------------------------------------------------

  • Defense: 3 + floor(1.6L)
  • Evasion: 3%
  • Retaliation: none
  • Price: 25 + 28L


BUNKER PLATE MK L
-------------------------------------------------------------------------------

  • Defense: 5 + floor(1.7L)
  • Evasion: 0%
  • Retaliation: none
  • Price: 34 + 33L


REACTIVE CARAPACE MK L
-------------------------------------------------------------------------------

  • Defense: 3 + floor(1.5L)
  • Evasion: 2%
  • Retaliation: 1 + floor(L / 2)
  • Price: 42 + 37L


ARMOR CATALOG SIZE
-------------------------------------------------------------------------------

  4 families × 10 marks = 40 generated armor templates


5.11 CONSUMABLES AND PROVISIONS
===

Let B be the difficulty-specific item-price base for regional level L.

TRAVEL PROVISIONS — 200 UNITS
-------------------------------------------------------------------------------

  • Effect: +200 provisions
  • Price: B


HEALING DRAUGHT +L
-------------------------------------------------------------------------------

  • Effect: Heal 16 + 6L
  • Price: B


RECONSTRUCTION TONIC +L
-------------------------------------------------------------------------------

  • Effect: Heal 28 + 8L
  • Price: B + 9


SPARK BOMB +L
-------------------------------------------------------------------------------

  • Effect: Direct damage 14 + 7L
  • Price: B + 7


ARMOR-MELT FLASK +L
-------------------------------------------------------------------------------

  • Direct damage: 8 + 5L
  • Defense reduction:
      round(original enemy defense × 0.35)
  • Minimum requested reduction: 1
  • Price: B + 11


AEGIS WARD +L
-------------------------------------------------------------------------------

  • Effect: Block one enemy strike
  • Price: B + 12


STATIC SMOKE +L
-------------------------------------------------------------------------------

  • Effect:
      Reduce the next connecting enemy strike by 45%
  • Warded and evaded strikes preserve the weakening
  • Price: B + 10


GUARDIAN SERUM +L
-------------------------------------------------------------------------------

  • Healing: 18 + 5L
  • Ward charges: +1
  • Price: B + 20


REGIONAL STOCK SIZE
-------------------------------------------------------------------------------

Per region:

  • 4 weapons
  • 4 armors
  • 7 consumables
  • 1 provision entry
  • 16 stock entries

Across ten regions:

  • 40 weapons
  • 40 armors
  • 70 consumables
  • 10 provision entries
  • 160 regional stock templates


FIXED STARTER ITEMS
-------------------------------------------------------------------------------

  Traveler's Draught
    • Heal: 22
    • Stored price: 0

  Salvaged Knife
    • Attack: +3
    • Critical chance: 8%
    • Armor penetration: 0%
    • Stored price: 5


5.12 RUINS AND SALVAGE
===

RUIN IDENTITY BY BIOME
-------------------------------------------------------------------------------

  • Greenlands   → Old roadside settlement
  • Forest       → Collapsed research station
  • Wastes       → Roofless supply depot
  • Frozen Reach → Frozen mountain outpost
  • Coast        → Ruined coastal warehouse


RUIN STATE
-------------------------------------------------------------------------------

  • Unsearched
  • Explored


SALVAGE BRANCHES
-------------------------------------------------------------------------------

  • Quiet ruin with no recoverable cache: 34%
  • One regional stock selection: 66%


SUCCESSFUL STOCK SELECTION
-------------------------------------------------------------------------------

Uniform selection from:

  • 4 regional weapons
  • 4 regional armors
  • 7 regional consumables
  • 1 provisions entry

If provisions are selected:

  • Quantity: every integer from 100 through 200
  • Possible quantities: 101


DISTINCT SUCCESSFUL RESULT PAYLOADS PER REGION AND DIFFICULTY
-------------------------------------------------------------------------------

  4 weapons
    + 4 armors
    + 7 consumables
    + 101 provision quantities

  = 116 successful salvage results

Including the quiet-ruin branch:

  116 + 1 = 117 result classes per region and difficulty

Across ten regions and three difficulties:

  117 × 10 × 3 = 3,510 contextual ruin outcome classes


5.13 DISCOVERY CATALOG
===

Each discovery has:

  • One fixed authored identity
  • One fixed historical account
  • One programmatic icon
  • One color palette
  • One seeded coordinate
  • Unknown or known state
  • Independent airship-component assignment state


REGION 1
-------------------------------------------------------------------------------

  • Crashed Orbital Relay
    Preferred: Greenlands, Wastes

  • Buried Bunker Entrance
    Preferred: Wastes, Greenlands

  • Abandoned Research Station
    Preferred: Forest, Greenlands


REGION 2
-------------------------------------------------------------------------------

  • Mass Grave from the Collapse
    Preferred: Greenlands, Forest

  • Ruined Hydroelectric Facility
    Preferred: Coast, Greenlands

  • Functioning Greenhouse
    Preferred: Greenlands, Forest


REGION 3
-------------------------------------------------------------------------------

  • Pre-War Memorial
    Preferred: Greenlands, Coast

  • Sealed Command Center
    Preferred: Wastes, Greenlands

  • Derelict Air Traffic Control Tower
    Preferred: Greenlands, Wastes


REGION 4
-------------------------------------------------------------------------------

  • Partially Flooded Nuclear Shelter
    Preferred: Coast, Forest

  • Automated Weather Monitoring Station
    Preferred: Frozen Reach, Greenlands

  • Fallen Space Elevator Anchor Site
    Preferred: Wastes, Coast


REGION 5
-------------------------------------------------------------------------------

  • Underground Data Archive
    Preferred: Forest, Frozen Reach

  • Collapsed Transit Tunnel
    Preferred: Greenlands, Wastes

  • Deserted Children's School
    Preferred: Greenlands, Forest


REGION 6
-------------------------------------------------------------------------------

  • Long-Abandoned Hospital Ward
    Preferred: Greenlands, Frozen Reach

  • Quarantined Biohazard Laboratory
    Preferred: Forest, Wastes

  • Forgotten Military Checkpoint
    Preferred: Wastes, Greenlands


REGION 7
-------------------------------------------------------------------------------

  • Frozen Evacuation Convoy
    Preferred: Frozen Reach

  • Silent Underground Metro Platform
    Preferred: Greenlands, Wastes

  • Solar Farm Still Tracking the Sun
    Preferred: Wastes, Greenlands


REGION 8
-------------------------------------------------------------------------------

  • Ancient Robotics Manufacturing Plant
    Preferred: Wastes, Greenlands

  • Derelict Deep-Sea Communications Station
    Preferred: Coast

  • Abandoned Agricultural Seed Vault
    Preferred: Frozen Reach, Forest


REGION 9
-------------------------------------------------------------------------------

  • Municipal Water Purification Complex
    Preferred: Coast, Greenlands

  • Emergency Broadcast Station No. 17
    Preferred: Greenlands, Wastes

  • Underground Geothermal Power Facility
    Preferred: Wastes, Frozen Reach


REGION 10
-------------------------------------------------------------------------------

  • Hall of the Last Parliament
    Preferred: Greenlands, Wastes

  • Autonomous Drone Maintenance Hangar
    Preferred: Wastes, Greenlands

  • Cryogenic Preservation Vault
    Preferred: Frozen Reach


DISCOVERY COMBINATIONS
-------------------------------------------------------------------------------

Per site:

  {Unknown, Known}
    ×
  {Not assigned to assembly, Assigned as Lift Envelope source}

Global reveal-state combinations:

  2³⁰ = 1,073,741,824 possible discovery reveal sets


5.14 RADIO TOWERS
===

Each tower has three independent persistent properties:

  • Transmitter:
      Off
      On

  • Song:
      Song 1
      Song 2
      Song 3

  • Navigation component:
      Unharvested
      Harvested


RADIO CONFIGURATION SPACE
-------------------------------------------------------------------------------

  2 transmitter states
    × 3 songs
    × 2 component states

  = 12 persistent configurations per tower


RADIO SONG FILES
-------------------------------------------------------------------------------

  • Song 1 → Signal.mp3
  • Song 2 → Signal2.mp3
  • Song 3 → Signal3.mp3


BROADCAST SELECTION
-------------------------------------------------------------------------------

  • Broadcast radius: 75 straight-line tiles
  • Nearest active tower wins
  • Equal distance: coordinate-key order
  • Same-song tower transitions continue without restarting the song
  • Broadcast contexts:
      Foot travel
      Airship travel
      Villages
      Ruins
      Discoveries
      Radio interactions
      Battle
  • Boat travel uses the sea soundtrack


SIMULATION EFFECTS
-------------------------------------------------------------------------------

A radio-covered settlement can receive:

  • +1 Security on even-numbered settlement cycles
  • Shipment-reliability bonus for exchanges involving a covered endpoint


5.15 SETTLEMENT GENERATION AND SIMULATION
===

SIMULATION CLOCK
-------------------------------------------------------------------------------

  • One settlement cycle per 24 traveled tiles
  • Foot, boat, and airship tiles all advance the same world clock


PRESSURE VALUES
-------------------------------------------------------------------------------

  • Supplies: 0 through 100
  • Materials: 0 through 100
  • Security: 0 through 100
  • Prosperity: 0 through 100

Numerical pressure snapshots per village:

  101⁴ = 104,060,401


CONDITION BANDS
-------------------------------------------------------------------------------

  70–100
    • Supplies: Abundant
    • Materials: Abundant
    • Security: Secure
    • Prosperity: Thriving

  40–69
    • Stable

  20–39
    • Strained

  0–19
    • Dire


TREND STATES
-------------------------------------------------------------------------------

  • Rising
  • Falling
  • Steady

Band-and-trend combinations across four pressures:

  4⁴ bands × 3⁴ trends = 20,736 combinations


INITIAL PRESSURE GRAMMAR
-------------------------------------------------------------------------------

For each pressure:

  52
    + seeded integer from -5 through +5
    + twice the biome production delta
    + shop modifiers
    + active-boss modifiers

Final initial value:

  clamp to 32 through 72


INITIAL SHOP MODIFIERS
-------------------------------------------------------------------------------

  Item Shop
    • Supplies: +4
    • Prosperity: +2

  Weapon Shop
    • Materials: +2
    • Security: +4
    • Prosperity: +2

  Armor Shop
    • Materials: +2
    • Security: +4
    • Prosperity: +2


INITIAL ACTIVE-BOSS MODIFIERS
-------------------------------------------------------------------------------

  • Security:
      -(3 + floor(region / 4))

  • Prosperity:
      -2


BIOME PRODUCTION PER CYCLE
-------------------------------------------------------------------------------

                    Supplies   Materials   Security   Prosperity
  Greenlands          +2           0          0           +1
  Forest              +1          +2         -1            0
  Wastes              -1          +2          0           +1
  Frozen Reach        -1          +2         +1            0
  Coast               +2           0         -1           +2


RECURRING LOCAL INFLUENCES
-------------------------------------------------------------------------------

  Every village
    • Supplies: -1

  Item Shop
    • Supplies: +1
    • Prosperity: +1

  Weapon Shop
    • Materials: -1
    • Security: +1
    • Prosperity: +1

  Armor Shop
    • Materials: -1
    • Security: +1
    • Prosperity: +1

  Active regional boss
    • Security:
        -(1 + floor((region - 1) / 5))
    • Prosperity:
        -1 when current Security is below 50

  Liberated region
    • Security:
        +1 while below 62

  Active radio coverage
    • Security:
        +1 on even cycles while below 65

  Local adaptation
    • Any pressure below 45:
        +1

  Abundance relaxation
    • Any pressure above 78:
        -1


POST-PRODUCTION CONVERSIONS
-------------------------------------------------------------------------------

  • Materials above 55
    + Security below 36
    → Materials -1
    → Security +1

  • Supplies above 55
    + Security above 55
    → Prosperity +1

  • Supplies below 25
    OR Security below 25
    → Prosperity -1


INCIDENTS
-------------------------------------------------------------------------------

Incident chance per cycle:

  0.055
    + 0.0025 × region
    + 0.045 when the regional boss is active

Incident outcome:

  • One of four pressures
  • Loss from 5 through 9

Complete incident payloads:

  4 pressures × 5 loss amounts = 20


GOOD SEASONS
-------------------------------------------------------------------------------

When no incident occurs:

  • Separate chance: 4%
  • One of four pressures
  • Gain: +4

Complete good-season payloads:

  4 pressures × 1 gain amount = 4


PER-CYCLE EVENT CLASSES
-------------------------------------------------------------------------------

  • Ordinary production cycle
  • 20 incident payloads
  • 4 good-season payloads

  = 25 local event classes before route exchange


5.16 SETTLEMENT EXCHANGE
===

ROUTE TYPES
-------------------------------------------------------------------------------

  INFORMAL CONTACT
    • Capacity: 1 per pressure
    • Base reliability: 0.58
    • Transfers:
        Supplies
        Materials

  BASIC RECONSTRUCTION LINK
    • Capacity: 3 per pressure
    • Base reliability: 0.76
    • Transfers:
        Supplies
        Materials
        Security

  GUARDED LINK — RADIUS 1
    • Capacity: 6 per pressure
    • Base reliability: 0.925

  GUARDED LINK — RADIUS 2
    • Capacity: 7 per pressure
    • Base reliability: 0.950

  GUARDED LINK — RADIUS 3
    • Capacity: 8 per pressure
    • Base reliability: 0.975


CONFEDERATION ROUTE BONUS
-------------------------------------------------------------------------------

Formal endpoints in the same confederation:

  • Capacity: +1


INFORMAL CONTACT SELECTION
-------------------------------------------------------------------------------

  • Same region
  • Nearest eligible known settlement
  • Maximum distance: 275 tiles
  • Duplicate pairs consolidated
  • Independent from reconstruction
  • No free-inn or political effect


TRANSFER REQUIREMENTS
-------------------------------------------------------------------------------

  • Projected donor value: at least 65
  • Projected receiver value: at most 35

  Available
    = max(0, donor value - 65 - reserved donations)

  Needed
    = max(0, 40 - receiver value)

  Shipment amount
    = floor(min(route capacity, available, needed))


RELIABILITY ADJUSTMENTS
-------------------------------------------------------------------------------

  Base route reliability

    + (average endpoint Security - 50) / 250

    - 0.08 when either endpoint's regional boss is active

    + 0.04 when either endpoint has active radio coverage

Final reliability:

  clamp to 0.32 through 0.98


SHIPMENT OUTCOMES
-------------------------------------------------------------------------------

  SUCCESS
    • Donor loses shipment amount
    • Receiver gains shipment amount
    • Shipment of at least 2 adds +1 receiver Prosperity

  LOSS
    • Donor loses shipment amount
    • Donor Prosperity: -1


5.17 CRISES AND RECOVERY
===

CRISIS OPENING RULE
-------------------------------------------------------------------------------

  • A pressure remains below 20
  • Duration: two consecutive settlement cycles


SEVERITY
-------------------------------------------------------------------------------

  • Value 15–19 → Severity 1
  • Value 10–14 → Severity 2
  • Value 0–9   → Severity 3


CRISIS TYPES
-------------------------------------------------------------------------------

  • Supply Crisis
  • Materials Crisis
  • Security Crisis
  • Prosperity Crisis


CRISIS COMBINATION SPACE
-------------------------------------------------------------------------------

  4 pressure types × 3 severities = 12 crisis classes


CRISIS LIFECYCLE
-------------------------------------------------------------------------------

  Open
    → Aid En Route
    → Resolved

  OR

  Open
    → Network Recovery
    → Resolved


RECOVERY THRESHOLD
-------------------------------------------------------------------------------

  • Matching pressure reaches 40


5.18 RECONSTRUCTION
===

BASIC LINK GRAMMAR
-------------------------------------------------------------------------------

  Known liberated village A
    × Different known liberated village B
    × One owned consumable donation
    × Gold cost
    × Provision cost


COST FORMULAS
-------------------------------------------------------------------------------

Let d be endpoint distance.

  Gold
    = 20
    + 4 × max(endpoint regions)
    + ceil(d / 10)

  Provisions
    = 8 + ceil(d / 8)


BASIC LINK EFFECTS
-------------------------------------------------------------------------------

  • Both endpoint inns become free
  • Formal resource route is created
  • Link becomes a reconstruction-graph edge
  • Link can contribute to confederation formation
  • Link can receive patrol equipment


PATROL GRAMMAR
-------------------------------------------------------------------------------

  One donated weapon
    × One donated armor
    × Combined Attack and Defense


PATROL RADIUS
-------------------------------------------------------------------------------

  1 + min(2, floor((weapon attack + armor defense) / 14))


PATROL STRENGTH BANDS
-------------------------------------------------------------------------------

  Combined strength below 14
    → Radius 1

  Combined strength 14–27
    → Radius 2

  Combined strength 28 or more
    → Radius 3


ROUTE STATE
-------------------------------------------------------------------------------

  • Basic
  • Guarded, radius 1
  • Guarded, radius 2
  • Guarded, radius 3


PATROL EFFECTS
-------------------------------------------------------------------------------

  • Geometric distance from land tile to route segment
  • Wider protected land corridor
  • Encounter chance × 0.5 within covered land
  • Increased shipment capacity
  • Increased shipment reliability


5.19 CONFEDERATIONS
===

FORMATION RULES
-------------------------------------------------------------------------------

  • Three or more connected independent villages:
      New confederation

  • One or two connected independent villages adjoining exactly one
    established confederation:
      Join that confederation

  • Independent component adjoining multiple established confederations:
      Retains independent status unless it forms its own qualifying group

  • Two established confederations connected together:
      Remain separate governments


CONFEDERATION IDENTITY
-------------------------------------------------------------------------------

Each confederation stores:

  • Stable ID
  • Member set
  • Three founding villages
  • Generated name
  • Founding resource city
  • Distinctive export
  • Formation step
  • Foreign agreements


NAME GRAMMAR
-------------------------------------------------------------------------------

  First word of Founder 1
    + First word of Founder 2
    + First word of Founder 3

Collision sequence:

  BaseName
  BaseName-2
  BaseName-3
  BaseName-4
  ...


RESOURCE CITY
-------------------------------------------------------------------------------

  • One of the three founders
  • Selected by coordinate hash


ALL EXPORT SPECIALTIES
-------------------------------------------------------------------------------

  GREENLANDS
    • Sungrain
    • Meadow flax
    • Orchard honey
    • Roadwarden wool

  FOREST
    • Amber resin
    • Ironwood sap
    • Medicinal moss
    • Cedar oil

  WASTES
    • Vitrified silica
    • Sun-cured dates
    • Copper salts
    • Glassfiber

  FROZEN REACH
    • Blue frostglass
    • Cold-preserved cultures
    • Glacier minerals
    • Winterroot extract

  COAST
    • Brine pearls
    • Sea-salt crystals
    • Kelp fiber
    • Shell-lime


EXPORT GRAMMAR
-------------------------------------------------------------------------------

  Full Resource-City Name + Biome Specialty

Biome-specialty combinations:

  5 biomes × 4 specialties = 20


5.20 COMMERCIAL TRADE
===

TRADE AGREEMENT GRAMMAR
-------------------------------------------------------------------------------

  Confederation A
    × Different Confederation B
    × Established agreement

A reconstruction link between the governments is not required.


PASSIVE COMMERCIAL EFFECT
-------------------------------------------------------------------------------

Every other settlement cycle, each agreement supplies:

  • +1 Prosperity to Confederation A's resource city
  • +1 Prosperity to Confederation B's resource city

An eligible member serves as the destination when a designated resource city
is outside the active known-settlement set.


COMMERCIAL MISSION GRAMMAR
-------------------------------------------------------------------------------

  Origin village in Confederation A
    × Agreement with Confederation B
    × Eligible member destination in Confederation B
    × Confederation A export
    × Region-and-distance reward
    × Mission lifecycle


COMMERCIAL REWARD
-------------------------------------------------------------------------------

  35
    + 5 × max(origin region, destination region)
    + ceil(distance / 6)


COMMERCIAL DELIVERY EFFECT
-------------------------------------------------------------------------------

  • Gold reward
  • Origin Prosperity: +2
  • Destination Prosperity: +2
  • Chronicle event
  • Mission-history entry


5.21 EMERGENCY RELIEF
===

SUPPLIES
-------------------------------------------------------------------------------

  • Cargo: Emergency provisions and medicine
  • Source contribution: 12 Supplies
  • Destination relief: +30 Supplies
  • Reward bonus: +24 gold


MATERIALS
-------------------------------------------------------------------------------

  • Cargo: Emergency tools and repair stock
  • Source contribution: 11 Materials
  • Destination relief: +28 Materials
  • Reward bonus: +26 gold


SECURITY
-------------------------------------------------------------------------------

  • Cargo: Emergency patrol stores and defensive equipment
  • Source contribution: 10 Security
  • Destination relief: +27 Security
  • Reward bonus: +30 gold


PROSPERITY
-------------------------------------------------------------------------------

  • Cargo: Emergency market goods and reconstruction credit
  • Source contribution: 11 Prosperity
  • Destination relief: +28 Prosperity
  • Reward bonus: +28 gold


EMERGENCY ELIGIBILITY
-------------------------------------------------------------------------------

  • Open crisis
  • Distressed village belongs to a confederation
  • Source village belongs to a different confederation
  • Confederations have an agreement
  • Source pressure is at least 55
  • No other active delivery
  • Request cooldown complete


EMERGENCY MISSION GRAMMAR
-------------------------------------------------------------------------------

  Eligible source village
    × Foreign agreement
    × Open crisis destination
    × {Supplies, Materials, Security, Prosperity}
    × Severity {1, 2, 3}
    × Pressure-specific cargo
    × Pressure-specific source contribution
    × Pressure-specific destination relief
    × Reward


EMERGENCY REWARD
-------------------------------------------------------------------------------

  Commercial reward
    + Pressure reward bonus
    + 8 × crisis severity


SUCCESSFUL RELIEF EFFECT
-------------------------------------------------------------------------------

  • Matching pressure receives the relief amount
  • Destination Prosperity: +4
  • Matching crisis resolves when still active
  • Gold reward
  • Chronicle event
  • Mission-history entry


MISSION LIFECYCLES
-------------------------------------------------------------------------------

  Active → Completed
  Active → Cancelled
  Active → Failed

Commercial and emergency cargo share one focused active-delivery slot.


5.22 AIRSHIP ASSEMBLY
===

WORKSHOP LOCATIONS
-------------------------------------------------------------------------------

  • Villages in Regions 6 through 10
  • Independent from ordinary Reconstruction Board availability


ASSEMBLY ORIGIN GRAMMAR
-------------------------------------------------------------------------------

  Any eligible Region 6–10 village
    × One active assembly
    × Seeded assembly serial


THREE ORDERED COMPONENTS
-------------------------------------------------------------------------------

  1. Lift Envelope Material
     Source: one of 30 discovery sites

  2. Stabilizer Gyroscope
     Source: one eligible defeated regional boss lair

  3. Navigation Coil
     Source: nearest eligible unharvested radio tower


FULL ASSEMBLY LIFECYCLE
-------------------------------------------------------------------------------

  Discovery outbound
    → Lift material carried
    → Lift material returned

  Defeated-lair outbound
    → Stabilizer carried
    → Stabilizer returned

  Radio outbound
    → Navigation coil carried
    → Navigation coil returned

  Ready
    → Completed vessel


TARGET ROTATION
-------------------------------------------------------------------------------

  • Discovery target rotates away from the previous assignment when possible
  • Defeated-lair target rotates away from the previous assignment when possible
  • Repeat completed builds use a different defeated lair when alternatives exist
  • Radio target uses nearest eligible unharvested tower
  • All three sources are selected when assembly begins


RADIO SEARCH
-------------------------------------------------------------------------------

  • Expanding coordinate rings
  • Search radius: up to 1,024 tiles
  • Harvest state persists independently from transmitter state


COMPLETED-VESSEL PLACEMENT
-------------------------------------------------------------------------------

Eligible terrain:

  • Greenlands
  • Coast
  • Wastes

Required state:

  • No village
  • No ruins
  • No radio tower
  • No boss lair
  • No discovery
  • No other grounded airship

Placement:

  • Nearest eligible tile
  • Expanding rings up to 512 tiles


AIRSHIP IDENTITY
-------------------------------------------------------------------------------

Every completed vessel stores:

  • Persistent vessel ID
  • Current x-coordinate
  • Current y-coordinate
  • Grounded or occupied state


5.23 TRAVEL STATES
===

ON FOOT
-------------------------------------------------------------------------------

  • Movement interval: 105 ms
  • Provision use: none
  • Ordinary land encounters: eligible


BOAT
-------------------------------------------------------------------------------

  • Movement interval: 105 ms
  • Entry fee: 10 gold
  • Provision use: 1 per water tile
  • Encounters: none


AIRSHIP
-------------------------------------------------------------------------------

  • Movement interval: 52.5 ms
  • Provision use: 1 per 2 air tiles
  • Encounters: none
  • Terrain traversal: unrestricted
  • Ground interactions during flight: bypassed


PROVISION EXHAUSTION
-------------------------------------------------------------------------------

Further sea or air movement removes:

  max(1, ceil(maximum HP × 0.05))


DEFEAT RECOVERY
-------------------------------------------------------------------------------

  • Return to registered refuge
  • Health restored to maximum
  • Difficulty-scaled gold loss
  • Levels retained
  • Experience retained
  • Equipment retained
  • Discoveries retained
  • Boss victories retained
  • Reconstruction retained
  • Confederations retained
  • Trade agreements retained
  • Settlement history retained
  • Grounded airships retained
  • Pending relay journey ends
  • Active delivery enters failed history
  • Unfinished assembly resets
  • Occupied airship is removed after airborne defeat


5.24 ENCOUNTER PROBABILITY
===

BASE LAND ENCOUNTER CHANCE
-------------------------------------------------------------------------------

  0.04 + 0.003 × regional level


BY REGION
-------------------------------------------------------------------------------

  • Region 1  : 4.3%
  • Region 2  : 4.6%
  • Region 3  : 4.9%
  • Region 4  : 5.2%
  • Region 5  : 5.5%
  • Region 6  : 5.8%
  • Region 7  : 6.1%
  • Region 8  : 6.4%
  • Region 9  : 6.7%
  • Region 10 : 7.0%


MODIFIERS
-------------------------------------------------------------------------------

  • Defeated regional boss:
      × 0.5

  • Guarded land corridor:
      × 0.5

  • Both:
      × 0.25


5.25 NETWORK CHRONICLE EVENT CATALOG
===

All thirteen event types:

  01. condition-strained
  02. condition-recovered
  03. crisis-opened
  04. crisis-resolved
  05. shipment-lost
  06. shipment-arrived
  07. relief-requested
  08. relief-dispatched
  09. relief-arrived
  10. relief-failed
  11. settlement-thriving
  12. regional-recovery
  13. commercial-delivery


EVENT GRAMMAR
-------------------------------------------------------------------------------

  Event type
    × Involved known villages
    × Relevant pressure
    × Amount or condition value
    × Route type
    × Crisis or regional identity
    × Simulation cycle
    × Severity


5.26 COMPLETE OBJECT-STATE INDEX
===

BASE TERRAIN
-------------------------------------------------------------------------------

  • Sea
  • Coast
  • Greenlands
  • Forest
  • Wastes
  • Frozen Reach

Each combines with:

  • Twenty tonal offsets
  • Regional level 1–10
  • Permitted base landmark
  • Permitted world overlay


VILLAGE
-------------------------------------------------------------------------------

  • Unrecorded
  • Recorded with persistent name

  ×

  • Independent
  • Confederation member

  ×

  • Eight service sets
  • One to three residents
  • Four 0–100 pressures
  • Four condition bands per pressure
  • Three trends per pressure
  • Crisis states
  • Dialogue-memory states


RUINS
-------------------------------------------------------------------------------

  • Unsearched
  • Explored

  ×

  • Quiet result
  • Weapon salvage
  • Armor salvage
  • Consumable salvage
  • Provision salvage


DISCOVERY
-------------------------------------------------------------------------------

  • Unknown
  • Known

  ×

  • Not an active assembly target
  • Active Lift Envelope target
  • Previously used component source


REGIONAL BOSS
-------------------------------------------------------------------------------

  • Living
  • Defeated

  ×

  • Unreported
  • Reported

  ×

  • Compass off
  • Selected as cyan compass target

  ×

  • Testimony unheard
  • Testimony recorded


CAMPAIGN BOSS SETS
-------------------------------------------------------------------------------

Ten bosses may be defeated in any regional order.

  2¹⁰ = 1,024 possible living/defeated boss sets


RADIO TOWER
-------------------------------------------------------------------------------

  • Off or On
  • Song 1, 2, or 3
  • Navigation component unharvested or harvested

  = 12 configurations per tower


RECONSTRUCTION LINK
-------------------------------------------------------------------------------

  • Basic
  • Guarded radius 1
  • Guarded radius 2
  • Guarded radius 3


RELAY JOURNEY
-------------------------------------------------------------------------------

  • None
  • Pending from one village
  • Completing at a different eligible village
  • Arriving at an already linked village


SETTLEMENT PRESSURE
-------------------------------------------------------------------------------

  • 0–100 value
  • Abundant, Stable, Strained, or Dire
  • Rising, Falling, or Steady


CRISIS
-------------------------------------------------------------------------------

  • Open
  • Aid En Route
  • Resolved

  ×

  • Supplies
  • Materials
  • Security
  • Prosperity

  ×

  • Severity 1
  • Severity 2
  • Severity 3


TRADE MISSION
-------------------------------------------------------------------------------

  • None
  • Active commercial
  • Active emergency relief
  • Completed commercial
  • Completed relief
  • Cancelled commercial
  • Cancelled relief
  • Failed commercial
  • Failed relief


ASSEMBLY OBJECTIVE
-------------------------------------------------------------------------------

  • Pending
  • Carried
  • Returned


ASSEMBLY LEG
-------------------------------------------------------------------------------

  • Outbound
  • Returning
  • Ready


AIRSHIP
-------------------------------------------------------------------------------

  • Grounded at persistent coordinates
  • Occupied in flight


TRAVEL
-------------------------------------------------------------------------------

  • Foot
  • Boat
  • Airship


PROVISIONS
-------------------------------------------------------------------------------

  • Available
  • Exhausted
  • Airship phase 0
  • Airship phase 1


ENCOUNTER
-------------------------------------------------------------------------------

  • Ordinary creature
  • Mini boss
  • Regional boss


ENEMY RESPONSE
-------------------------------------------------------------------------------

  • Standard
  • Cleave
  • Regrowth
  • Plating
  • Piercing
  • Rally
  • Siphon
  • Reactor
  • Broadside
  • Whiteout
  • Meltdown


INCOMING STRIKE
-------------------------------------------------------------------------------

  • Warded
  • Evaded
  • Connecting and weakened
  • Connecting at ordinary strength
  • Connecting with armor piercing
  • Connecting with evasion bypass
  • One strike in a multi-strike response


HERO STRIKE
-------------------------------------------------------------------------------

  • Ordinary
  • Critical
  • No penetration
  • Partial penetration
  • Direct item damage
  • Armor-reducing item damage


BATTLE OUTCOME
-------------------------------------------------------------------------------

  • Victory
  • Successful retreat
  • Failed retreat followed by enemy response
  • Defeat


CAMPAIGN
-------------------------------------------------------------------------------

  • Regional campaign in progress
  • All ten bosses defeated
  • Continuing world development


5.27 COMPASS COMBINATIONS
===

COMPASS COLORS
-------------------------------------------------------------------------------

  • Cyan  → Selected known living boss
  • Red   → Active commercial or emergency delivery
  • Green → Active airship component destination or return village


ALL VISIBILITY COMBINATIONS
-------------------------------------------------------------------------------

  1. No compass
  2. Cyan
  3. Red
  4. Green
  5. Cyan + Red
  6. Cyan + Green
  7. Red + Green
  8. Cyan + Red + Green

Each color occupies its own radial lane around the Wayfarer.


===
06. PERSISTENCE AND PORTABLE SAVES
===

Scipath Wayfarer stores its living world in browser localStorage using save
format version 9.

The saved world includes:

  • World seed
  • Difficulty
  • Character identity and icon color
  • Position and refuge
  • Health, level, XP, gold, and provisions
  • Inventory and equipment
  • Village discoveries and persistent names
  • Explored ruins
  • Revealed discoveries
  • Boss reports, compass state, victories, and testimony
  • Radio transmitter and song settings
  • Reconstruction links
  • Donated patrol equipment
  • Confederations
  • Membership
  • Resource cities
  • Exports
  • Trade agreements
  • Active and historical missions
  • Settlement pressures and trends
  • Simulation cycles
  • Crises
  • Network Chronicle events
  • Airship assembly progress
  • Harvested component sources
  • Airship identities and positions
  • Dialogue memory
  • Campaign completion

Loading performs:

  • Schema normalization
  • Reference validation
  • Geography validation
  • Derived-cache reconstruction
  • Political-state validation
  • Mission validation
  • Airship validation
  • Save migration

Recognized browser save versions:

  • Version 4
  • Version 5
  • Version 6
  • Version 7
  • Version 8
  • Version 9


PORTABLE JSON EXPORT
-------------------------------------------------------------------------------

Exports identify themselves with:

  format:
    scipath-wayfarer-save

  exportVersion:
    1

  game:
    Scipath Wayfarer

  saveVersion:
    9


SAVE BEHAVIOR
-------------------------------------------------------------------------------

  • Automatic saving after significant world changes
  • Immediate on-screen saving
  • Portable JSON export
  • Portable JSON import
  • Browser-to-browser transfer
  • Device-to-device transfer
  • Deterministic regeneration of the base world
  • Persistent preservation of everything that changed it


===
07. RUNNING AND HOSTING
===

Scipath Wayfarer is a static client-side web project.

No installation, compilation, package manager, application server, or database
is required.


LOCAL PREVIEW
-------------------------------------------------------------------------------

From the published game directory:

  python -m http.server 8000

Then open:

  http://localhost:8000/


GITHUB PAGES
-------------------------------------------------------------------------------

Publish the directory containing:

  • The HTML entry point
  • All adjacent audio assets

World generation, combat, rendering, settlement simulation, reconstruction,
politics, trade, airships, dialogue, and persistence all run in the browser.


===
08. AUDIO ASSETS
===

  hit.wav
    Combat impact

  die.wav
    Defeat

  item.wav
    Item and component feedback

  discover.wav
    Discovery feedback

  levelup.wav
    Level advancement and completed construction

  airship.wav
    Sequentially repeating airship engine

  Sea_Travel.mp3
    Sea-travel music

  Signal.mp3
    Radio Song 1

  Signal2.mp3
    Radio Song 2

  Signal3.mp3
    Radio Song 3


AUDIO ENGINE FEATURES
-------------------------------------------------------------------------------

  • Sequential combat impacts
  • Dedicated discovery and advancement effects
  • Continuous sea music
  • One persistent airship engine loop
  • Geographic radio-source selection
  • Same-song transmitter continuity
  • Visibility-aware ambient playback
  • Trusted-input audio initialization
  • Native HTML audio path
  • Dedicated iOS and iPadOS Web Audio path
  • Decoded effect buffers
  • Sequential hit scheduling
  • Browser-safe playback recovery


===
09. CREDITS
===

Scipath Wayfarer was created by Matthew Taraschke.

Developed over the course of a year from an experimental project into a
full-scale browser RPG, it combines procedural world generation, authored
post-apocalyptic history, tactical combat, persistent exploration, economic
simulation, reconstruction, politics, logistics, responsive dialogue, and
open-ended civilization building.

It is an exceptional amount of game contained inside an extraordinarily clean
static-web foundation: one seeded world, one persistent history, and a network
of systems designed to change one another.

The old world left commands behind.

The new world is built through connections.
