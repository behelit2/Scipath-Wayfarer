SCIPATH WAYFARER

A procedural, post-apocalyptic RPG with a living settlement network

Created by Matthew Taraschke
2026 | Version 0.99 Beta

PLAY NOW!

---
https://behelit2.github.io/Scipath-Wayfarer/
---

INTRODUCTION

Scipath Wayfarer began as an experiment by Matthew Taraschke. Over the course of a year, it grew into a full browser-based adventure combining a continuously generated world, tactical encounters, old-world discoveries, and an interconnected simulation of civilization rebuilding itself.

Its central idea is simple: an adventure becomes more interesting when its systems can change one another. Defeating a regional ruler changes wilderness danger and settlement conditions. Equipment can strengthen the hero or support a wider patrol. Radio coverage improves coordination. Connected villages exchange resources, form confederations, and create opportunities for trade and emergency relief.

This document covers the game’s design, engine, simulation, and complete procedural content structure. Controls, practical instructions, and detailed playing guidance are available in the in-game Instruction Manual.


CONTENTS

The Game
The Browser Engine
What the Game Simulates
Emergent Gameplay
Complete Procedural Generation Reference
Persistence and Save Architecture
Running and Hosting
Credits


THE GAME

Scipath Wayfarer is a retro-styled, open-world role-playing game set 350 years after a catastrophic nuclear event. Humanity survives in scattered feudal settlements, surrounded by abandoned infrastructure, mutated wildlife, and the enduring machinery of the old civilization.

The main campaign centers on ten regional bosses. Around that campaign is an open-ended world of exploration and recovery.

Procedural geography: Seas, coasts, greenlands, forests, wastes, and frozen highlands.

Encounter-driven combat: Biome-specific creatures, four enemy archetypes, and regional mini-boss patterns.

Tactical boss encounters: Ten distinct mechanics with visible response telegraphs.

Regional equipment: Weapons, armor, consumables, and salvage scaled to local danger.

Authored discoveries: Thirty distinctive locations whose placement changes with the world seed.

Persistent landmarks: Searched ruins, discovered sites, reported lairs, and configured radio transmitters.

Settlement simulation: Supplies, materials, security, prosperity, production, exchange, hardship, and recovery.

Reconstruction networks: Connections, equipment-supported patrols, and geometric protection corridors.

Political development: Independent villages become confederations while retaining their local identities.

Commercial and emergency logistics: Deliveries connect separate political groups.

Airship construction and travel: Multi-stage component journeys and a persistent fleet of individually positioned vessels.

Contextual dialogue: Residents respond to their professions, local conditions, network changes, and remembered conversations.

The campaign and reconstruction simulation complement each other. Each liberated region can begin rebuilding immediately, while the completed campaign opens a continuing world of exploration, development, and cooperation.


THE BROWSER ENGINE

Scipath Wayfarer uses a purpose-built engine written in vanilla JavaScript. Its interface, styling, rendering, simulation, and game logic are contained in a single HTML entry point. Audio assets are served alongside that file.


Architecture

The engine is organized into logical subsystems within a strict-mode JavaScript closure.

World generation: Coordinate hashing, layered noise, biome classification, landmark placement, and regional boundaries.

Content generation: Village identities, NPCs, enemy selection, regional stock, salvage, and mission targets.

Player state: Position, refuge, health, experience, currency, provisions, inventory, and equipment.

Combat: Turn responses, damage, critical hits, defense, evasion, wards, weakening, retaliation, and rewards.

World simulation: Settlement production, resource pressures, exchanges, incidents, crises, and recovery.

Reconstruction: Village connections, donations, patrol equipment, and corridor geometry.

Politics: Connected-component analysis, confederation identity, membership, and agreements.

Missions: Commercial cargo, emergency relief, assembly objectives, completion, and history.

Presentation: Canvas map, HUD, dialogs, shops, village tabs, journals, and Network Chronicle.

Audio: Effects, sequential impacts, sea music, radio selection, and airship engines.

Persistence: Browser saves, validation, migration, and portable JSON import and export.

A central state object stores persistent world progress. Temporary runtime objects manage the current encounter, open interface, active input, and rendering state.


Deterministic Geography and Independent Random Domains

The engine combines three complementary forms of randomness.

Coordinate-hashed generation:
Terrain, landmark rolls, shop availability, and several identity properties are derived from the world seed, coordinates, and dedicated salts.

Seeded local generators:
Mulberry32 streams generate repeatable village content, ruin salvage, boss lairs, discovery placement, and assembly selections.

Runtime random choices:
Encounters, creature selection, archetypes, combat variance, critical hits, evasion, retreat results, conversation selection, and commercial destinations use runtime randomness.

Settlement incidents and shipment outcomes have their own deterministic domain, keyed by the world seed, simulation tick, and event identity.

This separation gives the world a stable geographic identity while allowing encounters and conversations to remain lively.


World Data and Persistent Overlays

The base map is generated on demand rather than stored as a complete grid. Persistent records are layered over that geography:

Village discoveries and recorded names.
Explored ruins.
Known discoveries.
Boss reports, compass targets, defeats, and testimony.
Active transmitters and song selections.
Reconstruction links and patrols.
Confederations and trade agreements.
Settlement conditions, crises, and significant events.
Missions and mission history.
Airship construction and vessel positions.
Dialogue memory.

A tile can therefore be regenerated from its coordinates while retaining everything meaningful that has happened there.


Rendering and Interface

The map is drawn with Canvas 2D. Terrain colors, buildings, ruins, towers, fortresses, discoveries, boats, airships, and compass arrows are constructed programmatically.

The responsive HTML and CSS interface provides:

A compact status display.
Inventory and equipment management.
Combat panels and telegraphs.
Village Town, Rebuild, and Trade tabs.
Boss, discovery, and mission journals.
Network overview and settlement Chronicle.
A classic console-booklet-inspired instruction manual.

Rendering uses requestAnimationFrame, dirty flags, and a bounded tile cache of approximately 24,000 entries. Canvas dimensions are fitted to whole tiles, with six selectable tile sizes.

Input and transactions are coordinated through world modes and blocking overlays. Movement is suspended during interactions, and actions validate their required state before changing resources or progress.


Audio Architecture

Audio reinforces both immediate actions and geographic context.

Combat impacts are queued sequentially.
Item use, discovery, defeat, and level advancement have dedicated effects.
Sea travel uses a looping music track.
Airship flight uses one sequentially repeating engine loop.
Active radio towers provide a geographically selected broadcast.

The engine uses native HTML audio and an iOS/iPadOS Web Audio path for decoded effects and the airship loop. Trusted input gestures initialize audio, while radio and airship playback respond to visibility and travel state.


WHAT THE GAME SIMULATES

Hero Development and Combat

The hero has persistent health, maximum health, attack, defense, level, experience, gold, provisions, inventory, equipment, and refuge coordinates.

Combat combines:

Equipment attack and defense.
Critical-hit chance and critical damage.
Weapon armor penetration.
Armor evasion.
Reactive armor retaliation.
Direct-damage consumables.
Enemy armor reduction.
Temporary wards.
Weakening applied to the next enemy strike that actually connects.
Multi-strike responses.
Enemy regeneration and life stealing.
Turn-based attack cycles.
Health-threshold transformations.
Retreat probabilities.
Experience, currency, and regional victory rewards.

Bosses and mini-bosses expose their next response before the hero acts. Their intent is calculated from the response number and, where relevant, current health.

Equipment is also part of the reconstruction economy. A weapon or armor can be retained for personal combat or permanently contributed to a patrol.


Travel and Provisions

Travel has three states.

On foot:
Movement interval: 105 ms.
Provision consumption: None.
Encounters: Eligible ordinary land tiles can generate encounters.

Boat:
Movement interval: 105 ms.
Provision consumption: One per water tile.
Encounters: None.

Airship:
Movement interval: 52.5 ms.
Provision consumption: One per two air tiles.
Encounters: None.

Boat entry costs 10 gold. Airship provision accounting preserves a two-step phase, so consumption remains consistent across travel.

After provisions are exhausted, each additional sea or air tile removes this much health:

max(1, ceil(maximum HP × 0.05))

Airship flight crosses terrain and landmarks without activating ground interactions. Landing is a spatial placement operation restricted to clear grass, beach, or desert tiles.

Defeat returns the hero to the registered refuge with full health and a difficulty-dependent gold penalty. Long-term character, exploration, and reconstruction progress remain part of the world.

Active field projects have their own failure outcomes. An occupied airborne vessel is removed if the hero is defeated in flight.


Regional Liberation and Wilderness Danger

Ordinary land encounter probability is:

0.04 + 0.003 × regional level

Two protections can modify that probability:

Defeated regional boss: Multiply by 0.5.
Guarded land corridor: Multiply by 0.5.

Together, they reduce the local encounter probability to one quarter of its original value.

Regional liberation also affects settlements. Each already-known village in the liberated region immediately gains:

Security: +8.
Prosperity: +5.

The active-boss production pressure is removed from subsequent settlement cycles, and regional reconstruction becomes available.


Living Settlement Conditions

Every discovered village participates in a step-driven simulation with four integer conditions, each ranging from 0 to 100.

Supplies: Food, medicine, everyday necessities, and communal provisions.
Materials: Wood, metal, tools, salvage, and repair stock.
Security: Defenses, route safety, and resistance to hostile pressure.
Prosperity: Economic health, confidence, and productive success.

The world advances one settlement cycle for every 24 traveled tiles, across all travel modes.


Condition Bands

70–100:
General condition: Abundant.
Security wording: Secure.
Prosperity wording: Thriving.

40–69:
General condition, Security, and Prosperity wording: Stable.

20–39:
General condition, Security, and Prosperity wording: Strained.

0–19:
General condition, Security, and Prosperity wording: Dire.

Reports also compare current values with the previous snapshot to describe each condition as rising, falling, or steady.


Initial Settlement Values

Each condition begins at:

52 + seeded integer from -5 through +5

Initialization then applies:

Twice the village biome’s recurring delta.
Item Shop: Supplies +4; Prosperity +2.
Weapon Shop: Materials +2; Security +4; Prosperity +2.
Armor Shop: Materials +2; Security +4; Prosperity +2.

If the regional boss is active:

Security: -[3 + floor(region / 4)].
Prosperity: -2.

The resulting initial values are clamped to 32–72.


Biome Production Profile

These changes apply every simulation cycle and also contribute to initialization.

Greenlands:
Supplies +2; Materials 0; Security 0; Prosperity +1.

Forest:
Supplies +1; Materials +2; Security -1; Prosperity 0.

Wastes:
Supplies -1; Materials +2; Security 0; Prosperity +1.

Frozen Reach:
Supplies -1; Materials +2; Security +1; Prosperity 0.

Coast:
Supplies +2; Materials 0; Security -1; Prosperity +2.


Recurring Local Influences

The simulation layers the following influences onto biome production.

Every village consumes one Supplies point per cycle.

Item Shop:
Supplies +1; Prosperity +1.

Weapon Shop:
Materials -1; Security +1; Prosperity +1.

Armor Shop:
Materials -1; Security +1; Prosperity +1.

An active boss reduces Security by:

1 + floor((region - 1) / 5)

An active-boss village with Security below 50 also loses one Prosperity point.

A liberated village with Security below 62 gains one Security point.

Radio-covered villages with Security below 65 gain one Security point on even-numbered cycles.

A condition below 45 receives a one-point local adaptation benefit.

A condition above 78 relaxes by one point.

After production and exchange:

Materials above 55 can contribute one point toward Security when Security is below 36.

Supplies and Security both above 55 contribute one Prosperity point.

Supplies below 25 or Security below 25 apply one point of Prosperity pressure.

These interacting rules give each village a distinctive economic character.


Incidents and Good Seasons

A settlement’s incident probability per cycle is:

0.055 + 0.0025 × region + active-boss modifier

The active-boss modifier is 0.045.

An incident selects one of the four conditions and removes 5–9 points. When no incident occurs, a separate 4% good-season check can add four points to a selected condition.

The selections and outcomes are deterministic for the current simulation tick.


Settlement Exchange

The simulation builds an exchange graph from formal reconstruction links and limited informal regional contacts.

Informal route:
Capacity per condition: 1.
Base reliability: 0.58.

Basic reconstruction link:
Capacity per condition: 3.
Base reliability: 0.76.

Guarded link, radius 1:
Capacity per condition: 6.
Base reliability: 0.925.

Guarded link, radius 2:
Capacity per condition: 7.
Base reliability: 0.95.

Guarded link, radius 3:
Capacity per condition: 8.
Base reliability: 0.975.

A formal route whose endpoints belong to the same confederation receives one additional capacity point.

Informal contacts select eligible nearby villages in the same region, within 275 tiles, with duplicate pairs consolidated. Informal exchanges carry Supplies and Materials. Formal routes can also carry Security support.


Transfer Rules

An exchange requires:

A projected donor value of at least 65.
A projected receiver value of at most 35.

The shipment amount is calculated as follows:

available = max(0, donor projected value - 65 - reserved donations)
needed = max(0, 40 - receiver projected value)
amount = floor(min(route capacity, available, needed))

Reliability is adjusted as follows:

base reliability
+ (average endpoint Security - 50) / 250
- 0.08 if either endpoint’s regional boss is active
+ 0.04 if either endpoint has active radio coverage

Final reliability is clamped to 0.32–0.98.

Dispatched resources leave the donor. A successful shipment adds them to the receiver. A shipment of at least two points also adds one Prosperity point there.

A lost shipment applies one point of Prosperity pressure to the donor.

Because shipments change settlement conditions, they also change future production, donor eligibility, recovery, and crisis behavior.


Crises and Recovery

A condition remaining below 20 for two consecutive cycles can open a crisis.

Value when opened:
15–19: Severity 1.
10–14: Severity 2.
0–9: Severity 3.

A crisis has three lifecycle states:

Open -> Aid En Route -> Resolved

Ordinary network recovery resolves a crisis when its affected condition reaches 40. Emergency delivery can close its associated relief request and provide a substantial condition boost.

Residents and services remain part of the settlement throughout its recovery cycle. Hardship creates new relationships and opportunities rather than erasing the village’s identity.


Reconstruction and Patrol Geometry

A basic reconstruction connection records two different liberated villages, a donated consumable, and its patrol state.

For endpoint distance d:

Gold = 20 + 4 × max(endpoint regions) + ceil(d / 10)
Provisions = 8 + ceil(d / 8)

A completed link:

Makes both endpoint inns free.
Creates a stronger resource exchange route.
Becomes an edge in the reconstruction graph.
Can influence confederation formation.

A patrol consumes one weapon and one armor. Its radius is:

1 + min(2, floor((weapon attack + armor defense) / 14))

Combined donated attack and defense:
Below 14: Patrol radius 1.
14–27: Patrol radius 2.
28 or more: Patrol radius 3.

Patrol coverage is calculated using the distance from a land tile to the connection’s line segment. Wider patrols protect more surrounding ground and increase shipment capacity and base reliability.


Confederations and Political Identity

The engine analyzes connected components of independent villages.

A component of three or more independent settlements establishes a confederation.

A component of one or two independent settlements adjoining exactly one existing confederation can join it.

Established confederations retain separate identities when connected to one another.

An independent component bordering multiple established confederations retains its own political status unless it forms its own qualifying group.

Each confederation stores:

A stable ID.
Members.
Three founding villages.
A generated name.
A founding resource city.
A distinctive export.
Formation progress.
Trade agreements.

Confederation cooperation improves capacity over existing internal reconstruction links.


Commercial Trade and Emergency Relief

Trade agreements connect distinct confederations. Their commercial relationships operate independently of whether a reconstruction link exists between them.

Every other simulation cycle, each agreement adds one Prosperity point to each partner’s designated resource city, or an eligible member fallback.

Commercial deliveries:

Carry the source confederation’s distinctive export.
Select an eligible destination village in the partner confederation.
Keep sealed cargo separate from personal inventory.
Award gold on arrival.
Add two Prosperity points to both origin and destination.

Commercial reward:

35 + 5 × max(origin region, destination region) + ceil(distance / 6)

Emergency relief connects that political structure to actual settlement conditions.

Supplies crisis:
Cargo: Emergency provisions and medicine.
Source contribution: 12 Supplies.
Destination relief: +30 Supplies.
Reward bonus: +24.

Materials crisis:
Cargo: Emergency tools and repair stock.
Source contribution: 11 Materials.
Destination relief: +28 Materials.
Reward bonus: +26.

Security crisis:
Cargo: Emergency patrol stores and defensive equipment.
Source contribution: 10 Security.
Destination relief: +27 Security.
Reward bonus: +30.

Prosperity crisis:
Cargo: Emergency market goods and reconstruction credit.
Source contribution: 11 Prosperity.
Destination relief: +28 Prosperity.
Reward bonus: +28.

An eligible source village has at least 55 points in the requested condition and belongs to a distinct confederation with an agreement with the distressed village’s confederation.

Emergency reward:

commercial reward + crisis reward bonus + 8 × severity

Successful relief also adds four Prosperity points at the destination.

Commercial and emergency deliveries share one active mission slot. Both have completed, cancelled, and failed history states.

Failed emergency cargo remains a spent source contribution. An unresolved request can become available again after a two-cycle delay.

An accepted relief delivery remains valid if the ordinary network resolves the crisis during transit. The delivery still rewards the traveler and reinforces the settlement’s recovery.


Airship Construction and Fleet Persistence

Airship workshops appear in villages in Regions 6–10, independently of that village’s ordinary Reconstruction Board.

Each assembly creates three ordered objectives:

Lift Envelope Material from a discovery site.
Stabilizer Gyroscope from a defeated regional boss lair.
Navigation Coil from an eligible radio tower.

Every component has its own outward and return journey. All three sources are selected when construction begins, while the active objective controls the green compass.

Assembly lifecycle:

Discovery outbound
-> Discovery component carried
-> Discovery component returned
-> Defeated-lair outbound
-> Stabilizer carried
-> Stabilizer returned
-> Radio outbound
-> Navigation coil carried
-> Navigation coil returned
-> Ready
-> Completed vessel

Discovery and lair targets use seeded selection based on the assembly serial and rotate away from the previous assignment when alternatives exist.

Completed repeat builds use a different defeated lair. Radio components are recovered from unharvested eligible towers, using nearest-distance selection.

Completed vessels are placed on the nearest eligible clear grass, beach, or desert tile. Each airship receives its own persistent ID and position.

Grounded vessels remain in the world, allowing construction and travel to create a lasting geographic fleet.


Memory, Reports, and Journals

World changes are reflected through several complementary records.

Boss Log: Regional reports, compass state, defeats, and final testimony.

Discovery Log: Revealed sites and their authored accounts.

Trade Missions: Accepted deliveries and their outcomes.

Network Overview: Connections, patrols, confederations, and agreements.

Network Chronicle: Major condition changes, shipments, crises, relief, and recovery.

Village Notes: Local condition trends and recent developments.

Resident dialogue: Profession-specific observations and remembered structural changes.

Dialogue memory tracks recent lines, topic families, and pending notices. Residents can recognize liberation, new links, newly guarded routes, wider patrols, political membership, trade agreements, and network growth.


EMERGENT GAMEPLAY

The game’s strongest possibilities arise from combinations rather than isolated features.


Complementary Village Economies

A coastal or greenland village can develop a Supplies surplus while a forest, waste, or frozen settlement produces Materials.

Connections let these strengths answer different needs. Successful exchange can improve Prosperity, strengthen recovery, and change which village becomes the next useful donor.


Liberation Changes More Than Combat

Defeating a boss simultaneously reduces encounter danger, improves known regional settlements, removes ongoing hostile pressure, improves shipment conditions, and enables rebuilding.

A region’s liberation can therefore begin a chain of recovery extending through several connected villages.


Equipment Becomes a Strategic Resource

A powerful weapon and armor can support the hero directly, or their combined statistics can establish a wider patrol.

That patrol affects geographic coverage, encounter frequency, shipment capacity, and delivery reliability.

Personal advancement and collective reconstruction are linked by the same equipment catalog.


Radio Can Influence a Recovery Chain

A transmitter adds coordination benefits to nearby known settlements and improves exchanges involving covered endpoints.

A modest reliability increase can determine whether aid reaches a village before its condition becomes a crisis, or whether an existing crisis resolves during a relief journey.

The same tower also creates a recognizable soundscape and can become an airship component destination.


Political Borders Produce Meaningful Logistics

Connections can create confederations without collapsing every settlement into one government. Agreements between separate groups create commercial destinations and foreign relief relationships.

A crisis is therefore shaped not only by resource levels, but also by membership, existing agreements, source reserves, and the traveler’s route.


Travel Changes the Simulation’s Pace

Every traveled tile advances the same world clock. Airships cover tiles twice as quickly while using provisions more efficiently, so long-distance movement also accelerates settlement cycles in real time.

Transport choice connects personal logistics to the pace of production, exchange, and recovery.


Construction Journeys Intersect Other Goals

An assembly can direct the hero to an unknown discovery, a previously defeated fortress, and a radio tower.

Those destinations belong to the same persistent world as trade routes, patrol corridors, villages, and active broadcasts.

One journey can contribute to several systems at once.


The World Acknowledges Its Own History

A resident’s next conversation can reflect a new patrol, a local shortage, a recent shipment, or a confederation formed since the previous visit.

The journals and dialogue translate numerical changes into a world that remembers the traveler’s work.


COMPLETE PROCEDURAL GENERATION REFERENCE

The following catalogs define the game’s complete procedural choice sets and composition rules.

Combinations are expressed as catalogs, Cartesian products, numerical ranges, and eligibility constraints. This specifies generated objects precisely, including coordinate-dependent and continuing state combinations, while keeping the reference organized by system.


1. WORLD GENERATION

Noise Fields

Terrain uses smoothly interpolated coordinate-hashed value noise, combined through fractal Brownian motion.

Each additional octave doubles frequency and halves amplitude.

Continental elevation:
Coordinate scale: 0.0048.
Octaves: 5.
Coordinate offset: None.

Coastal detail:
Coordinate scale: 0.018.
Octaves: 4.
Coordinate offset: x + 4300, y - 2700.

Island detail:
Coordinate scale: 0.038.
Octaves: 3.
Coordinate offset: x - 8100, y + 6100.

Moisture:
Coordinate scale: 0.009.
Octaves: 4.
Coordinate offset: x + 12000, y - 9000.

Local climate:
Coordinate scale: 0.0035.
Octaves: 3.
Coordinate offset: x - 3500, y + 7300.

Elevation:

raw elevation = 0.74 × continental + 0.20 × coastal detail + 0.06 × island detail

elevation = 0.5 + (raw elevation - 0.5) × 1.55


Complete Biome Classification

Classification is evaluated in this order.

Sea:
Rule: Elevation below 0.495.
Base RGB: (22, 70, 145).

Coast:
Rule: Elevation from 0.495 to below 0.515.
Base RGB: (211, 191, 121).

Frozen Reach:
Rule: Remaining land with elevation at least 0.69, or elevation at least 0.635 and local climate below 0.47.
Base RGB: (232, 238, 240).

Wastes:
Rule: Remaining land with moisture below 0.425.
Base RGB: (207, 171, 70).

Forest:
Rule: Remaining land with moisture above 0.565.
Base RGB: (25, 85, 31).

Greenlands:
Rule: Remaining land.
Base RGB: (49, 132, 51).

Ordinary terrain color receives one shared RGB offset selected from the integers -10 through +9. This defines twenty tonal variations for each biome.


Regional Bands

region = min(10, floor(distance from world origin / 220) + 1)

Region 1: Distance below 220.
Region 2: Distance from 220 to below 440.
Region 3: Distance from 440 to below 660.
Region 4: Distance from 660 to below 880.
Region 5: Distance from 880 to below 1100.
Region 6: Distance from 1100 to below 1320.
Region 7: Distance from 1320 to below 1540.
Region 8: Distance from 1540 to below 1760.
Region 9: Distance from 1760 to below 1980.
Region 10: Distance of 1980 and beyond.

The coordinate world continues outward while regional difficulty remains capped at ten.


Base Landmark Combinations

One coordinate hash determines mutually exclusive base landmarks on non-water tiles.

Village:
Hash interval: [0, 0.000300).
Chance per eligible non-water tile: 0.0300%.

Ruins:
Hash interval: [0.000300, 0.000498).
Chance per eligible non-water tile: 0.0198%.

Radio tower:
Hash interval: [0.000498, 0.000597).
Chance per eligible non-water tile: 0.0099%.

Ordinary terrain:
Hash interval: Remaining interval.
Chance per eligible non-water tile: 99.9403%.

The base categorical tile grammar is:

Sea × Ordinary Terrain

or

{Coast, Greenlands, Forest, Wastes, Frozen Reach}
× {Ordinary Terrain, Village, Ruins, Radio Tower}

Boss lairs and discovery sites are independent seeded overlays.

Rendering and ground interaction use this priority order:

Boss Lair -> Village -> Ruins -> Radio Tower -> Discovery -> Ordinary Terrain

A special site placed over water can provide coastal footing.


Boss-Lair Placement

Each region receives one seeded lair.

Region 1 search radius: 70–212 tiles.

For Regions 2–10:

inner radius = (region - 1) × 220 + 8
outer radius = region × 220 - 8

Candidate selection is area-weighted within its annulus.

The search prioritizes non-water, village-free locations. Up to 20,000 candidates are examined before the fallback placement rule.

Boss identity and mechanic are fixed by regional level. The lair’s coordinates and biome come from generation.


Starting Location

The starting position uses a separate seeded stream.

The primary search samples clear Greenlands, Forest, or Coast within 175 tiles of the origin, excluding landmarks and discoveries.

An alternate clear-land search provides the additional non-water starting possibilities.


2. VILLAGE NAMES

A generated village name is:

Prefix + " " + Suffix

There are 36 prefixes × 36 suffixes = 1,296 name combinations.

Prefixes:

New, Fort, Saint, Old, East, West,
High, Stone, Iron, Green, Ash, Last,
North, South, Red, White, Black, Grey,
Silver, Copper, Oak, Pine, Willow, Cedar,
Birch, Moss, Thorn, Frost, Ember, Dawn,
Dusk, Sun, Moon, Wolf, Raven, Still

Suffixes:

Haven, Crossing, Watch, Ford, Rest, Vale,
Gate, Shelter, Market, Reach, Hold, Harbor,
Bridge, Keep, Hollow, Field, Hill, Ridge,
Brook, Creek, Spring, Falls, Bend, Grove,
Wood, Meadow, Heath, Marsh, Shore, Cove,
Point, Bluff, Pass, Landing, Refuge, Outpost

Recorded village names persist after discovery.


3. VILLAGE SERVICES AND RESIDENT COMPOSITION

Each shop category uses its own 70% availability check.

All eight service combinations are possible:

Inn only.
Inn and Weapon Shop.
Inn and Armor Shop.
Inn and Item Shop.
Inn, Weapon Shop, and Armor Shop.
Inn, Weapon Shop, and Item Shop.
Inn, Armor Shop, and Item Shop.
Inn, Weapon Shop, Armor Shop, and Item Shop.

Each village has one, two, or three residents. Resident names are unique within that village; professions can repeat.

A resident combines:

One of 96 names
× One of 11 professions
× One of 4 greeting personalities
× Boss knowledge: Yes or No

Boss knowledge has a 50% coordinate-hashed chance for each resident slot.


Complete Resident Name Catalog

Ada, Alden, Bram, Cora, Dain, Elia,
Fenn, Greta, Hale, Iris, Jora, Kellan,
Lina, Marek, Nora, Orin, Pella, Quinn,
Rhea, Silas, Tamsin, Ulric, Vera, Wren,

Aeron, Anwen, Arlen, Bastian, Bryn, Calder,
Cassia, Cedric, Daria, Delia, Edric, Eira,
Elric, Ember, Enid, Esme, Evren, Faris,
Fiora, Galen, Gareth, Gilda, Hadrian, Hazel,

Idris, Isolde, Jasper, Kael, Keira, Leif,
Lenora, Lucan, Lyra, Maela, Mira, Niall,
Odette, Oren, Petra, Ronan, Rowan, Sable,
Selene, Soren, Talia, Tarin, Thane, Tobin,

Torin, Valen, Veda, Willa, Yara, Yorin,
Zara, Zev, Alma, Brina, Corvin, Dorian,
Elowen, Freya, Hector, Iona, Liora, Maris,
Nessa, Oskar, Perrin, Roslyn, Sera, Varek


Professions and Condition Interests

Farmer: Supplies.
Hunter: Security.
Guard: Security.
Scholar: Prosperity.
Scavenger: Materials.
Healer: Supplies.
Trader: Prosperity.
Cartographer: Security.
Mechanist: Materials.
Fisher: Supplies.
Storykeeper: The village’s lowest condition.

Greeting personalities:

Practical.
Warm.
Wary.
Reflective.


4. CONTEXTUAL DIALOGUE COMBINATIONS

Resident speech combines authored wording with live world context.

The resident catalog contains:

Four greeting personalities: 12 entries.
Eleven profession pools: 33 entries.
Five biome pools: 25 entries.
General conversation pool: 17 entries.
Twenty-six situational topic pools: 78 entries.

Total resident catalog entries: 165.


Complete Selectable Topic Set

Role: Profession-specific observations.

Biome: Local environmental lore.

Advice: General world and system observations.

Simulation: Local hardship, crisis, trends, or recorded events.

Boss directions: Living regional boss and knowledgeable resident.

Boss unknown: Living regional boss without reliable resident directions.

Regional peace: Defeated local boss.

Campaign peace: All ten bosses defeated.

Isolated: Liberated village with no reconstruction links.

Linked basic: Direct links exist, all unguarded.

Guarded mixed: Both guarded and unguarded direct links.

Guarded all: Every direct link guarded.

Widened: A direct patrol has radius two or three.

Network: Indirectly connected settlements exist.

Pending start: Relay journey originated here.

Pending arrival: A relay can be completed here.

Pending duplicate: The pending origin is already linked here.

Nearby patrol: Patrol coverage passes nearby without this village being an endpoint.

Wounded: Hero health below 40%.

New link: A newly observed basic connection.

New guard: A newly observed guarded connection.

Wider patrol: A remembered patrol increased in radius.

Regional victory: Local boss defeated since an earlier conversation.

Campaign victory: Campaign completed since an earlier conversation.

Network growth: Connected component crossed a remembered milestone.

Independent politics: Village remains independent.

Confederation member: Village belongs to a confederation.

Confederation joined: Membership changed since an earlier conversation.

Trade partners: Confederation has foreign partners.

Trade opened: Partner count increased since an earlier conversation.

The twenty-six situational pools each contain three authored alternatives.

Topic selection is weighted by context. A first reliable boss report and remembered structural notices receive priority.

The two most recent topic families are avoided where alternatives exist, and recently discussed families receive a reduced weight.

Remembered network milestones:

3, 5, 10, 20, 50, and 100 connected villages.


Dialogue Template Values

Hero and village identity.
Boss name, trait, region, coordinates, distance, and direction.
Neighbor and indirect settlement names.
Direct, guarded, unguarded, and connected-network counts.
Patrol radius.
Pending relay origin.
Inn price, gold, provisions, boat fee, and starvation damage.
Confederation name, membership count, resource city, export, and partners.

Dynamic simulation sentences combine:

Condition
× Condition band
× {Rising, Falling, Steady}
× Profession interest
× Crisis or latest-event context

Arrival reports combine first-visit or return wording with regional status, reconstruction status, political membership, workshop availability, local trends, and relevant delivery or assembly messages.

Dialogue memory retains up to 384 records, with twenty recent line identifiers, five recent topic families, and eight pending notices per record.


5. ORDINARY CREATURE CATALOG

Every ordinary encounter selects a name from its biome, an archetype, regional level, and combat variance.

Greenlands:

Mutant Hare, Razor Boar, Feral Hound, Road Bandit,
Ash Stag, Scavenger, Horned Slime, Ruined Knight,
Boneback Bison, Wandering Marauder, Thorn Lizard, War Hound

Forest:

Glowcap Crawler, Forest Bat, Goblin Forager, Spore Wolf,
Barkhide Ent, Web Stalker, Moss Ogre, Root Wraith,
Toxic Dryad, Canopy Hunter, Ancient Treant, Night Howler

Wastes:

Glass Scarab, Sand Imp, Cactus Beast, Dust Raider,
Irradiated Mummy, Sand Golem, Dune Stalker, Ash Djinn,
Burrowing Wyrm, Sun Vulture, Tomb Guardian, Waste Reaver

Frozen Reach:

Frost Hare, Ice Wolf, Pale Imp, Snow Troll,
Ice Golem, Frost Giant, Blizzard Spirit, White Wyrm,
Ruins Yeti, Cold Wraith, Shard Bear, Aurora Hunter

Coast:

Iron Crab, Razor Gull, Coast Bandit, Shell Beast,
Tide Spirit, Sea Raider, Salt Slime, Wave Elemental,
Marsh Serpent, Drowned Sailor, Reef Stalker, Storm Gull


Archetypes

Aggressive:
HP multiplier: 0.85.
Attack multiplier: 1.18.
Defense multiplier: 0.85.

Stalwart:
HP multiplier: 1.25.
Attack multiplier: 0.90.
Defense multiplier: 1.08.

Armored:
HP multiplier: 0.95.
Attack multiplier: 0.95.
Defense multiplier: 1.25.

Balanced:
HP multiplier: 1.00.
Attack multiplier: 1.00.
Defense multiplier: 1.00.

The ordinary categorical combination space is:

5 biomes
× 12 biome-specific names
× 4 archetypes
× 10 regions
= 2,400 combinations per difficulty

Across three difficulties, this gives 7,200 ordinary creature configurations before numerical variance.


6. MINI-BOSS COMBINATIONS

An eligible random encounter has a 10% mini-boss selection chance.

Mini-bosses use the same name and archetype catalogs, with these multipliers:

HP: ×2.
Attack: ×1.15.
Defense: ×1.15.
Gold and XP: ×1.8.

Rank and mechanic are determined by biome and regional tier.

Regions 1–3: Alpha.
Regions 4–6: Elite.
Regions 7–10: Dread.

Greenlands:
Alpha: Stampeding Blow — Cleave.
Elite: Pack Dominance — Rally.
Dread: Blood Frenzy — Meltdown.

Forest:
Alpha: Fungal Renewal — Regrowth.
Elite: Parasitic Roots — Siphon.
Dread: Blinding Sporeburst — Whiteout.

Wastes:
Alpha: Glasshide Shell — Plating.
Elite: Shatterfang — Piercing.
Dread: Solar Overload — Reactor.

Frozen Reach:
Alpha: Icebound Armor — Plating.
Elite: Killing Blizzard — Whiteout.
Dread: Aurora Discharge — Reactor.

Coast:
Alpha: Crashing Tide — Cleave.
Elite: Reefbreaker — Piercing.
Dread: Twin Tidal Strike — Broadside.

Generated names take these forms:

Base Creature Name - Alpha
Base Creature Name - Elite
Base Creature Name - Dread

Mini-bosses provide another 2,400 categorical combinations per difficulty, or 7,200 across all difficulties.

Together, ordinary creatures and mini-bosses define 14,400 difficulty-specific categorical configurations, with rank and pattern constrained by their regional tier.


7. REGIONAL BOSSES AND SHARED MECHANICS

Region 1: The Carrion Baron
Identity: Warlord of the inner roads.
Mechanic: Heavy Cleave.
Testimony chapter: The Promise.

Region 2: Mother Glowcap
Identity: Queen of the mutating spores.
Mechanic: Spore Regrowth.
Testimony chapter: The Custodians.

Region 3: The Rusted Colossus
Identity: Guardian of a fallen reactor.
Mechanic: Fortress Plating.
Testimony chapter: The Hidden Design.

Region 4: King Glassclaw
Identity: Terror of the shattered wastes.
Mechanic: Piercing Claw.
Testimony chapter: The Sleeping Arsenal.

Region 5: The Hollow General
Identity: Commander of a dead army.
Mechanic: Rally.
Testimony chapter: The False Warning.

Region 6: Veyra of the Black Root
Identity: Corruptor of ancient forests.
Mechanic: Root Siphon.
Testimony chapter: The Broken Seal.

Region 7: The Cobalt Behemoth
Identity: A beast changed by blue fire.
Mechanic: Reactor Cycle.
Testimony chapter: The Blue Fire.

Region 8: Admiral Dreadtide
Identity: Master of the poisoned coast.
Mechanic: Broadside.
Testimony chapter: The Forsaken Fleet.

Region 9: The Aurora Devourer
Identity: Hunter beneath the polar lights.
Mechanic: Whiteout.
Testimony chapter: The Command Eternal.

Region 10: Emperor Fallout
Identity: Last tyrant of the old world’s ruins.
Mechanic: Meltdown.
Testimony chapter: The Last King.


Shared Mechanic Definitions

The ten mechanic definitions are shared by regional bosses and the corresponding mini-boss patterns.

Cleave:
Every third response has 60% more attack.

Regrowth:
Every third response restores up to 10% maximum HP afterward, if both combatants remain alive.

Plating:
Odd-numbered responses add max(2, round(original defense × 0.5)) defense.

Piercing:
Every third response ignores 50% of hero defense.

Rally:
Attack bonus is min(6, response number - 1).

Siphon:
Every third response heals up to half the HP actually removed.

Reactor:
Every fourth response doubles attack. The preceding response uses half attack.

Broadside:
Every third response makes two strikes at 65% attack each.

Whiteout:
Every third response has 25% more attack and bypasses evasion.

Meltdown:
At half health or below, attack increases by 35%, including immediately after the hero crosses that threshold.

Wards can block individual strikes, including Whiteout. A two-strike response resolves defense, wards, evasion, weakening, and retaliation separately for each strike.


8. ENEMY NUMERICAL GENERATION

In the formulas below:

L is regional level.
v is shared stat variance.
Archetype multipliers come from the archetype catalog.
mHP, mATK, mDEF, and mReward are ordinary or mini-boss multipliers.


Ordinary Creatures and Mini-Bosses

v is in the interval [0.90, 1.10).

HP = max(1, round((12 + 6L) × archetype HP × v × mHP))

Attack = max(1, round(difficulty normal attack × archetype attack × v × mATK))

Defense = max(0, round((1 + 0.85L) × archetype defense × v × mDEF))

Gold = max(1, round(difficulty normal gold × v × mReward))

XP = max(1, round((8 + 4.2L) × v × mReward))

Ordinary multipliers are all 1.

Mini-boss multipliers:
mHP = 2.
mATK = 1.15.
mDEF = 1.15.
mReward = 1.8.


Regional Bosses

v is in the interval [0.95, 1.05).

HP = round((42 + 30L) × v)
Attack = round(difficulty boss attack × v)
Defense = round((2 + 1.15L) × v)
Gold = round(difficulty boss gold)
XP = 42 + 17L

Emperor Fallout doubles the generated boss HP.


9. DIFFICULTY AND PROGRESSION PARAMETERS

Easy — Wanderer

Starting HP: 36.
Starting gold: 12.
First level XP requirement: 140.
HP gained per level: 6.
Defense growth interval: 2.
Maximum HP gained per regional boss: 4.
Boss victory healing: Full restoration.
Equipment resale rate: 35%.
Consumable resale rate: 35%.
Defeat gold rate: 12%.
Minimum defeat loss: 0.

Regional formulas:
Ordinary enemy attack = 4 + 2.2L.
Ordinary enemy gold = 5 + 3.5L.
Boss attack = 8 + 2.8L.
Boss gold = 42 + 24L.
Item price base = 8 + 4L.


Normal — Adventurer

Starting HP: 33.
Starting gold: 9.
First level XP requirement: 152.
HP gained per level: 5.
Defense growth interval: 2.5.
Maximum HP gained per regional boss: 3.
Boss victory healing: 70% maximum HP.
Equipment resale rate: 27.5%.
Consumable resale rate: 22.5%.
Defeat gold rate: 18.5%.
Minimum defeat loss: 2.

Regional formulas:
Ordinary enemy attack = 4.5 + 2.475L.
Ordinary enemy gold = 3.75 + 2.6L.
Boss attack = 9 + 3.1L.
Boss gold = 31 + 18.5L.
Item price base = 10 + 5L.


Hard — Wayfarer

Starting HP: 30.
Starting gold: 6.
First level XP requirement: 160.
HP gained per level: 4.
Defense growth interval: 3.
Maximum HP gained per regional boss: 2.
Boss victory healing: 40% maximum HP.
Equipment resale rate: 20%.
Consumable resale rate: 10%.
Defeat gold rate: 25%.
Minimum defeat loss: 3.

Regional formulas:
Ordinary enemy attack = 5 + 2.75L.
Ordinary enemy gold = 2.5 + 1.7L.
Boss attack = 10 + 3.4L.
Boss gold = 20 + 13L.
Item price base = 12 + 6L.


Starting Character and Progression

All new heroes begin with:

Base Attack: 6.
Base Defense: 2.
Provisions: 200.
Level: 1.

Each level adds one Base Attack point and the difficulty’s HP gain, then fully restores health.

For hero level H > 1, the next XP requirement is:

4 × (35 + 18H)

Defense increases whenever:

floor(H / defense interval) > floor((H - 1) / defense interval)

Retreat probability for ordinary creatures and mini-bosses is:

min(0.78, 0.48 + 0.04 × max(0, hero level - enemy level))

Defeat loss is the smaller of available gold and:

max(minimum loss, floor(gold × defeat rate))


10. WEAPONS

All four generated weapon families have regional marks 1–10. L is the regional mark.

Wayfarer Sword Mk L:
Attack: 3 + 2L.
Critical chance: 6%.
Armor penetration: 0%.
Price: 18 + 24L.

Salvaged War Axe Mk L:
Attack: 5 + 2L.
Critical chance: 3%.
Armor penetration: 0%.
Price: 26 + 29L.

Reactor Spear Mk L:
Attack: 2 + 2L.
Critical chance: 8%.
Armor penetration: 28%.
Price: 30 + 31L.

Glassedge Blade Mk L:
Attack: 3 + 2L.
Critical chance: 18%.
Armor penetration: 8%.
Price: 38 + 35L.

This produces 40 regional weapon templates.

Critical hits multiply the calculated attack damage by 1.75, then round.


11. ARMOR

All four armor families have regional marks 1–10. L is the regional mark.

Roadwarden Leather Mk L:
Defense: 2 + floor(1.4L).
Evasion: 8%.
Retaliation: None.
Price: 18 + 23L.

Scrap-Mail Coat Mk L:
Defense: 3 + floor(1.6L).
Evasion: 3%.
Retaliation: None.
Price: 25 + 28L.

Bunker Plate Mk L:
Defense: 5 + floor(1.7L).
Evasion: 0%.
Retaliation: None.
Price: 34 + 33L.

Reactive Carapace Mk L:
Defense: 3 + floor(1.5L).
Evasion: 2%.
Retaliation: 1 + floor(L / 2).
Price: 42 + 37L.

This produces 40 regional armor templates.


12. CONSUMABLES AND PROVISIONS

Let B be the difficulty-specific item price base for regional level L.

Travel Provisions — 200 units:
Effect: Adds 200 provisions directly.
Price: B.
Use context: Purchase.

Healing Draught +L:
Effect: Heal 16 + 6L.
Price: B.
Use context: World or battle.

Reconstruction Tonic +L:
Effect: Heal 28 + 8L.
Price: B + 9.
Use context: World or battle.

Spark Bomb +L:
Effect: Direct damage 14 + 7L.
Price: B + 7.
Use context: Battle.

Armor-Melt Flask +L:
Effect: Direct damage 8 + 5L; reduce enemy defense by 35% of original defense, rounded, with a minimum requested reduction of one.
Price: B + 11.
Use context: Battle.

Aegis Ward +L:
Effect: Block one enemy strike.
Price: B + 12.
Use context: Battle.

Static Smoke +L:
Effect: Reduce the next connecting enemy strike’s attack by 45%.
Price: B + 10.
Use context: Battle.

Guardian Serum +L:
Effect: Heal 18 + 5L; add one ward.
Price: B + 20.
Use context: Battle.

Each region supplies four weapons, four armors, and eight item entries: 160 level-indexed stock entries across ten regions.

Two additional starter templates are fixed.

Traveler’s Draught:
Heal 22.
Stored price: 0.

Salvaged Knife:
Attack: +3.
Critical chance: 8%.
Armor penetration: 0%.
Stored price: 5.

Provision purchases and provision salvage update the travel counter directly. Other items become individually identified inventory objects.

Resale uses the appropriate difficulty rate, rounded down, with a minimum value of one gold.


13. RUIN COMBINATIONS AND SALVAGE

Ruins combine:

Land biome
× Regional level
× {Unsearched, Explored}
× Seeded one-time salvage result

Biome descriptions:

Greenlands: Old roadside settlement.
Forest: Collapsed research station.
Wastes: Roofless supply depot.
Frozen Reach: Frozen mountain outpost.
Coast: Ruined coastal warehouse.

Salvage has two initial branches:

34%: Empty salvage result.
66%: Select uniformly from the sixteen regional stock entries.

The successful branch includes:

Four weapon templates.
Four armor templates.
Seven consumable templates.
One provision template.

The provision template expands to every integer amount from 100 through 200, inclusive: 101 possible provision quantities.

At a given region and difficulty, successful ruin content is therefore described by:

4 weapons
+ 4 armors
+ 7 consumables
+ 101 provision quantities

Exploration state persists, making salvage a permanent part of the world’s history.


14. DISCOVERY CATALOG

The catalog assigns three discoveries to each regional band.

Placement uses an independent seed stream, excludes other landmarks and discoveries, and keeps sites at least 24 tiles apart.

For the first 160 placement attempts, each site favors its listed biomes. The broader placement rules then accept other eligible land, with coastal footing available through the fallback rule.

Each discovery has its own authored account, color palette, and programmatically drawn icon.


Region 1

Crashed Orbital Relay
ID: orbital-relay.
Preferred biomes: Greenlands, Wastes.

Buried Bunker Entrance
ID: bunker-entrance.
Preferred biomes: Wastes, Greenlands.

Abandoned Research Station
ID: research-station.
Preferred biomes: Forest, Greenlands.


Region 2

Mass Grave from the Collapse
ID: collapse-grave.
Preferred biomes: Greenlands, Forest.

Ruined Hydroelectric Facility
ID: hydroelectric-facility.
Preferred biomes: Coast, Greenlands.

Functioning Greenhouse
ID: functioning-greenhouse.
Preferred biomes: Greenlands, Forest.


Region 3

Pre-War Memorial
ID: prewar-memorial.
Preferred biomes: Greenlands, Coast.

Sealed Command Center
ID: sealed-command-center.
Preferred biomes: Wastes, Greenlands.

Derelict Air Traffic Control Tower
ID: air-traffic-tower.
Preferred biomes: Greenlands, Wastes.


Region 4

Partially Flooded Nuclear Shelter
ID: flooded-nuclear-shelter.
Preferred biomes: Coast, Forest.

Automated Weather Monitoring Station
ID: weather-station.
Preferred biomes: Frozen Reach, Greenlands.

Fallen Space Elevator Anchor Site
ID: space-elevator-anchor.
Preferred biomes: Wastes, Coast.


Region 5

Underground Data Archive
ID: underground-data-archive.
Preferred biomes: Forest, Frozen Reach.

Collapsed Transit Tunnel
ID: collapsed-transit-tunnel.
Preferred biomes: Greenlands, Wastes.

Deserted Children’s School
ID: childrens-school.
Preferred biomes: Greenlands, Forest.


Region 6

Long-Abandoned Hospital Ward
ID: hospital-ward.
Preferred biomes: Greenlands, Frozen Reach.

Quarantined Biohazard Laboratory
ID: biohazard-laboratory.
Preferred biomes: Forest, Wastes.

Forgotten Military Checkpoint
ID: military-checkpoint.
Preferred biomes: Wastes, Greenlands.


Region 7

Frozen Evacuation Convoy
ID: frozen-evacuation-convoy.
Preferred biome: Frozen Reach.

Silent Underground Metro Platform
ID: silent-metro-platform.
Preferred biomes: Greenlands, Wastes.

Solar Farm Still Tracking the Sun
ID: tracking-solar-farm.
Preferred biomes: Wastes, Greenlands.


Region 8

Ancient Robotics Manufacturing Plant
ID: robotics-manufacturing-plant.
Preferred biomes: Wastes, Greenlands.

Derelict Deep-Sea Communications Station
ID: deepsea-communications.
Preferred biome: Coast.

Abandoned Agricultural Seed Vault
ID: agricultural-seed-vault.
Preferred biomes: Frozen Reach, Forest.


Region 9

Municipal Water Purification Complex
ID: water-purification-complex.
Preferred biomes: Coast, Greenlands.

Emergency Broadcast Station No. 17
ID: broadcast-station-17.
Preferred biomes: Greenlands, Wastes.

Underground Geothermal Power Facility
ID: geothermal-power-facility.
Preferred biomes: Wastes, Frozen Reach.


Region 10

Hall of the Last Parliament
ID: last-parliament.
Preferred biomes: Greenlands, Wastes.

Autonomous Drone Maintenance Hangar
ID: drone-maintenance-hangar.
Preferred biomes: Wastes, Greenlands.

Cryogenic Preservation Vault
ID: cryogenic-vault.
Preferred biome: Frozen Reach.


Discovery State

Unknown Site -> Known named discovery

A discovery can also be the active lift-material source for an assembly mission. That mission assignment and the site’s discovery state are independent until entry.


15. RADIO TOWER COMBINATIONS

Each tower has three independent persistent properties:

Transmitter: Off or On.
Song: 1, 2, or 3.
Navigation component: Unharvested or Harvested.

This defines twelve configuration combinations per tower.

Song 1: Signal.mp3.
Song 2: Signal2.mp3.
Song 3: Signal3.mp3.

Broadcast range is 75 straight-line tiles.

When active ranges overlap, the nearest tower selects the broadcast. Equal distances use coordinate-key ordering. The same song can continue while moving between transmitters.

Broadcasts accompany land travel, flight, village interactions, and battle. Boat travel selects the sea-travel soundtrack instead.


16. CONFEDERATION NAMES AND EXPORTS

A confederation’s base name concatenates the first word of its three founding village names. Founders are selected from the coordinate-sorted member list.

Name collisions receive numbered suffixes:

BaseName
BaseName-2
BaseName-3
And so on.

A coordinate-hashed selection chooses one founding village as the resource city. Another coordinate hash selects one of four specialties for that city’s biome.

The export name combines:

Full resource-city name + specialty

Matching export names can be distinguished with resource-city coordinates.


Complete Export Specialty Catalog

Greenlands:
Sungrain; meadow flax; orchard honey; roadwarden wool.

Forest:
Amber resin; ironwood sap; medicinal moss; cedar oil.

Wastes:
Vitrified silica; sun-cured dates; copper salts; glassfiber.

Frozen Reach:
Blue frostglass; cold-preserved cultures; glacier minerals; winterroot extract.

Coast:
Brine pearls; sea-salt crystals; kelp fiber; shell-lime.

The political identity grammar is:

Founding village trio
× Generated confederation name
× One founding resource city
× One eligible biome specialty
× Member set
× Trade-partner set


17. RECONSTRUCTION AND MISSION COMBINATION RULES

Reconstruction Links

Two distinct known liberated villages
× One owned consumable donation
× {Basic, Patrol Radius 1, Patrol Radius 2, Patrol Radius 3}

Guarded states additionally record one donated weapon and one donated armor. Their statistics determine the eligible radius.


Commercial Missions

Origin village in Confederation A
× Existing agreement with Confederation B
× Eligible member destination in Confederation B
× Confederation A’s export
× Distance-and-region reward
× Mission lifecycle


Emergency Missions

Eligible source village in Confederation A
× Existing agreement with Confederation B
× Open crisis in a member of Confederation B
× {Supplies, Materials, Security, Prosperity}
× Severity {1, 2, 3}
× Condition-specific cargo, contribution, and relief
× Distance-and-region reward
× Mission lifecycle

Mission lifecycle:

Active -> Completed
Active -> Cancelled
Active -> Failed

Emergency offers are ordered by descending severity, then ascending distance. They are presented before ordinary commercial offers.


Airship Assemblies

Origin village in Region 6–10
× One of 30 discovery sites
× One eligible defeated regional lair
× Nearest eligible unharvested radio tower
× Ordered component-and-return lifecycle

Target-selection constraints include prior assignments, completed builds, defeated-boss eligibility, and harvested tower records.

Radio target search examines expanding coordinate rings up to 1,024 tiles.

Completed-vessel placement examines eligible landing positions in expanding rings up to 512 tiles.


18. COMPLETE SETTLEMENT EVENT CATALOG

The Network Chronicle records thirteen event types.

condition-strained:
A stable condition crosses into the strained band.

condition-recovered:
A condition returns to stability without an active crisis requiring separate resolution.

crisis-opened:
A condition remains dire for the qualifying streak.

crisis-resolved:
Network recovery or emergency relief closes a crisis.

shipment-lost:
A significant or crisis-sensitive shipment fails.

shipment-arrived:
Aid reaches a settlement with an active matching crisis.

relief-requested:
An eligible foreign relief request is first announced.

relief-dispatched:
Emergency cargo is accepted and source reserves are contributed.

relief-arrived:
Emergency cargo reaches its destination.

relief-failed:
Emergency cargo is lost through cancellation or defeat.

settlement-thriving:
Prosperity crosses into the abundant band.

regional-recovery:
A boss defeat improves known regional settlements.

commercial-delivery:
Completed trade improves origin and destination Prosperity.

Events combine:

Event type
× Involved known villages
× Relevant condition
× Amount or condition value
× Route type
× Crisis or regional identity
× Simulation tick
× Severity

Major condition and shipment notices use a three-cycle settlement event cooldown.

The Chronicle retains the latest 180 significant events, with a 24-record resolved-crisis history and protection for crisis records referenced by an active relief mission.


19. PERSISTENT OBJECT AND SITUATION STATES

Base terrain:
Six biomes, with permitted landmark and tonal combinations.

Village discovery:
Unrecorded, or recorded with a persistent name.

Village politics:
Independent or confederation member.

Village condition:
Four conditions ranging from 0 to 100, each with four condition bands and three trend descriptions.

Ruins:
Unsearched or explored.

Discovery:
Unknown or known.

Regional boss:
Living or defeated.

Boss intelligence:
Unreported or reported.

Boss compass:
Off, or one known living boss selected.

Boss testimony:
Recorded on defeat, with heard or recovered provenance.

Radio:
Off/on × three songs × component harvest state.

Reconstruction connection:
Basic, or guarded at radius one, two, or three.

Relay journey:
None, or one pending origin.

Crisis:
Open, aid en route, or resolved.

Trade mission:
None, or one active commercial/relief mission; completed, cancelled, and failed history.

Assembly objective:
Pending, carried, or returned.

Assembly leg:
Outbound, returning, or ready.

Airship:
Grounded at its own coordinates, or occupied in flight.

Travel:
Foot, boat, or airship.

Provision state:
Available or exhausted. Flight additionally retains its two-step consumption phase.

Encounter:
Ordinary creature, mini-boss, or regional boss.

Enemy response:
Standard, or one of the ten mechanic-driven intents.

Incoming strike:
Warded, evaded where eligible, weakened connecting strike, or ordinary connecting strike.

Hero strike:
Ordinary or critical, with equipped penetration.

Battle outcome:
Victory, eligible successful retreat, or defeat.

Campaign:
Continuing regional campaign, or completed campaign with ongoing world development.


Compass Systems

The three compass systems can coexist.

Cyan: Selected known living boss.
Red: Active commercial or emergency delivery.
Green: Active assembly destination or return village.

They use separate radial drawing lanes around the hero. Each expresses direct geometric direction, making concurrent world objectives visually distinct.


PERSISTENCE AND SAVE ARCHITECTURE

Scipath Wayfarer stores progress in browser localStorage using the current version 9 save format.

The saved world includes:

World seed and difficulty.
Character identity, position, refuge, statistics, inventory, and equipment.
Exploration and landmark records.
Defeated bosses, reports, compass selection, and testimony.
Radio transmitter settings.
Reconstruction connections and donated patrol equipment.
Confederations, membership, exports, and agreements.
Active and historical trade missions.
Settlement conditions, previous values, ticks, crises, and events.
Assembly objectives, harvested component sources, and airship positions.
Dialogue memory.

Loading normalizes data, validates references against regenerated geography, and reconstructs the world’s derived caches.

The persistence layer recognizes save versions 4–9, with versioned optional schemas for settlement simulation, airships, and dialogue memory.

Simulation counters and event history preserve completed world developments across sessions.

Portable exports use a JSON wrapper with these identifying fields:

format: scipath-wayfarer-save
exportVersion: 1
game: Scipath Wayfarer
saveVersion: 9

Automatic saves accompany significant progress changes. The interface also provides explicit saving and portable import/export.


RUNNING AND HOSTING

The game is a client-side static web project, making it well suited to GitHub Pages and other static hosting services.

Serve the HTML entry point and its audio assets from the same published directory.


Audio Asset Filenames

hit.wav: Combat impact.
die.wav: Defeat.
item.wav: Item and component feedback.
discover.wav: Discovery feedback.
levelup.wav: Advancement and completed construction.
airship.wav: Repeating flight engine.
Sea_Travel.mp3: Sea-travel music.
Signal.mp3: Radio Song 1.
Signal2.mp3: Radio Song 2.
Signal3.mp3: Radio Song 3.


Local Static Preview

Run this command from the project directory:

python -m http.server 8000

Open the served game entry point through:

http://localhost:8000/


GitHub Pages

Publish the directory containing the HTML entry point and the adjacent audio assets.

World generation, simulation, rendering, and progress management run in the browser.


CREDITS

Scipath Wayfarer was created by Matthew Taraschke.
