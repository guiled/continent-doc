# Features Extracted from Continent Project

This document lists all features identified in the Continent codebase that are being refactored into the Renaissance project.

## Table of Contents
1. [Construction & Building System](#construction--building-system)
2. [Production System](#production-system)
3. [Military System](#military-system)
4. [Diplomacy System](#diplomacy-system)
5. [Guild System](#guild-system)
6. [Exploration System](#exploration-system)
7. [Research System](#research-system)
8. [Feudalism & Vassalage](#feudalism--vassalage)
9. [Events & Random Events](#events--random-events)
10. [Map & Territory Management](#map--territory-management)
11. [Trade & Economy](#trade--economy)
12. [Naval System](#naval-system)
13. [Heroes System](#heroes-system)
14. [Swag System](#swag-system)
15. [Pacts & Treaties](#pacts--treaties)
16. [Infrastructure & Utilities](#infrastructure--utilities)

---

## Construction & Building System

### Building Construction
- **Building Construction**: Players can construct various buildings (castles, farms, mines, forges, etc.)
  - `Continent/Construction.bas` - `processBuildTask()` function
  - `Continent/cntSRV.frm` - Main server loop calling construction tasks

- **Building Upgrades**: Buildings can be upgraded to higher levels
  - `Continent/Construction.bas` - Building upgrade logic in `processBuildTask()`

- **Construction Progress**: Buildings are constructed over time with progress tracking
  - `Continent/Construction.bas` - `processBuildTask()` tracks `avancement` vs `cout_total`
  - `Continent/outils.bas` - `avancetask()` function updates progress

- **Construction Requirements**: Buildings require tools, materials, and workers (peons)
  - `Continent/Construction.bas` - Tool consumption calculation in `processBuildTask()`
  - `Continent/Construction.bas` - Material requirements from `TYPE_TACHES` table

- **Building Placement**: Buildings are placed on specific map coordinates with footprint management
  - `Continent/Construction.bas` - Building placement logic
  - `Continent/carte.bas` - `getCases()` function calculates building footprint

- **Building Sprites**: Visual representation of buildings on the map with different sprites per building type
  - `Continent/carte.bas` - `updateMap()` function places sprites on map layer 2

### Building Maintenance
- **Building Repairs**: Buildings can be repaired when damaged
  - `Continent/Construction.bas` - `processRepareTask()` function
  - `Continent/cntSRV.frm` - Server loop processes repair tasks

- **Building State**: Buildings have a state/condition that degrades over time
  - `Continent/CONSTRUCTIONS` table - `etat` field tracks building condition
  - `Continent/Construction.bas` - State management in repair functions

- **Building Collapse**: Buildings can collapse if not maintained (state < 5%)
  - `Continent/evenements.bas` - Building collapse events
  - `Continent/cntSRV.frm` - Collapse detection and handling

- **Automatic Maintenance**: General building maintenance task for all buildings
  - `Continent/Construction.bas` - `processRepareTask()` handles general maintenance
  - `Continent/cntSRV.frm` - Maintenance task scheduling

- **Targeted Repairs**: Specific building repair tasks
  - `Continent/Construction.bas` - `processRepareTask()` handles specific repairs

- **Repair Costs**: Repairs consume tools, wood, and stone
  - `Continent/Construction.bas` - `processRepareTask()` consumes resources

### Terrain Modification
- **Terrain Paving**: Convert terrain to paved surfaces
  - `Continent/Construction.bas` - Terrain modification tasks
  - `Continent/carte.bas` - `updateMap()` updates terrain layer

- **Terrain Damage**: Damage terrain (fill swamps, water holes)
  - `Continent/Construction.bas` - Terrain modification actions
  - `Continent/carte.bas` - Map layer updates

- **Terrain Transformation**: Transform terrain types (marsh to land, water holes to land)
  - `Continent/Construction.bas` - Terrain transformation logic
  - `Continent/carte.bas` - `updateMap()` modifies terrain layer (layer 1)

- **Terrain Requirements**: Terrain modifications require tools and workers
  - `Continent/Construction.bas` - Resource consumption for terrain tasks

### Naval Construction
- **Boat Building**: Construction of naval vessels
  - `Continent/Construction.bas` - `processBuildBoatTask()` function
  - `Continent/cntSRV.frm` - Server processes boat construction tasks

- **Boat Repair**: Repair damaged naval vessels
  - `Continent/Construction.bas` - `processRepareBoatTask()` function

- **Boat Placement**: Automatic placement of completed boats on water tiles
  - `Continent/Construction.bas` - `processBuildBoatTask()` finds water tiles and places boats
  - `Continent/militaire.bas` - `createBateau()` function creates naval units

- **Boat Construction Sites**: Visual representation of boats under construction on map
  - `Continent/Construction.bas` - Sprite 254 used for construction sites
  - `Continent/carte.bas` - `updateMap()` places construction sprites

---

## Production System

### Resource Production
- **Multiple Production Types**: Production of various resources (food, wood, stone, metal, etc.)
  - `Continent/production.bas` - `processProdTask()` function handles all production types
  - `Continent/cntSRV.frm` - Server loop processes production tasks

- **Production Buildings**: Production requires specific buildings (farms, mines, forges, etc.)
  - `Continent/production.bas` - `getMaxPeonsForProd()` checks building requirements
  - `Continent/production.bas` - Building validation in `processProdTask()`

- **Worker Assignment**: Assign workers (peons) to production tasks
  - `Continent/production.bas` - `processProdTask()` uses `nb_peons` parameter
  - `Continent/ACTIONS` table - Stores peon assignments per production

- **Production Capacity**: Maximum workers per production based on building count
  - `Continent/production.bas` - `getMaxPeonsForProd()` calculates capacity

- **Production Bonuses**: Bonuses from sciences, regional modifiers, morale
  - `Continent/production.bas` - `getBonusProdMR()` calculates production bonuses
  - `Continent/server_tools.bas` - `getBonus()` function retrieves science bonuses

- **Production Efficiency**: Production affected by morale, tools availability, and bonuses
  - `Continent/production.bas` - `processProdTask()` includes morale and tool calculations

### Specific Productions
- **Farming**: Crop production with seasonal variations
  - `Continent/production.bas` - `placeFermiers()` places farmers on map
  - `Continent/production.bas` - Seasonal effects in production calculations

- **Mining**: Stone and metal extraction
  - `Continent/production.bas` - Mining production logic
  - `Continent/production.bas` - `placeMiners()` places miners with smoke effects

- **Logging**: Wood production with forest management
  - `Continent/production.bas` - `processAbattageTask()` handles logging
  - `Continent/production.bas` - `placeBucherons()` places loggers on map

- **Hunting**: Food production from hunting
  - `Continent/production.bas` - Hunting production type

- **Fishing**: Food production from fishing (affected by season)
  - `Continent/production.bas` - `placePecheurs()` places fishermen at docks
  - `Continent/production.bas` - Seasonal fishing calculations

- **Livestock**: Animal breeding (cattle, horses, pigeons)
  - `Continent/production.bas` - `processAbattageTask()` handles animal slaughtering
  - `Continent/production.bas` - Animal reproduction logic

- **Crafting**: Tool and weapon production
  - `Continent/production.bas` - Crafting production types
  - `Continent/production.bas` - `placeForgerons()` places blacksmiths

- **Gathering**: Food gathering (seasonal, affected by winter)
  - `Continent/production.bas` - `placeCueilleurs()` places gatherers
  - `Continent/production.bas` - Winter effects on gathering

### Production Mechanics
- **Material Consumption**: Some productions consume raw materials
  - `Continent/production.bas` - `processProdTask()` consumes materials from inventory

- **Tool Consumption**: Productions consume tools
  - `Continent/production.bas` - `processProdTask()` calculates and consumes tools

- **Seasonal Effects**: Production affected by seasons (winter reduces some productions)
  - `Continent/production.bas` - Seasonal modifiers in production calculations
  - `Continent/evenements.bas` - Winter event affects production

- **Reproduction Rates**: Animal production based on existing herd size
  - `Continent/production.bas` - Animal reproduction calculations

- **Capacity Limits**: Production limited by building capacity (stables, enclosures)
  - `Continent/production.bas` - `getMaxPeonsForProd()` enforces capacity limits

- **Spring Bonus**: Increased animal reproduction in spring
  - `Continent/production.bas` - Seasonal bonuses for animal production

- **Random Factors**: Production includes random variation
  - `Continent/production.bas` - Random factors in production calculations

### Production Visualization
- **Worker Placement on Map**: Visual representation of workers on map (loggers, miners, farmers, etc.)
  - `Continent/production.bas` - `placeBucherons()`, `placeCarriers()`, `placeFermiers()`, etc.
  - `Continent/carte.bas` - `updateMap()` places worker sprites on map layer 2

- **Forestry Workers**: Foresters planting trees
  - `Continent/production.bas` - `placeForestiers()` places foresters
  - `Continent/carte.bas` - Tree planting in map normalization

- **Fishermen**: Fishermen at docks
  - `Continent/production.bas` - `placePecheurs()` places fishermen

- **Farmers**: Farmers in fields
  - `Continent/production.bas` - `placeFermiers()` places farmers

- **Miners**: Miners at mines with smoke effects
  - `Continent/production.bas` - `placeMiners()` places miners with visual effects

- **Blacksmiths**: Blacksmiths at forges
  - `Continent/production.bas` - `placeForgerons()` places blacksmiths

### Special Productions
- **Deep Sea Fishing**: Extended fishing campaigns with naval vessels
  - `Continent/Productions.bas` - `PROD_ResultatPechehauturiere()` function
  - `Continent/militaire.bas` - Naval fishing campaigns in `processArmeeTask()`

- **Slaughtering**: Automatic weekly slaughtering of animals
  - `Continent/production.bas` - `processAbattageTask()` handles weekly slaughtering

- **Tree Planting**: Forest management and tree planting
  - `Continent/carte.bas` - `normaliseCarte()` includes tree planting logic

---

## Military System

### Army Management
- **Army Formation**: Train and form military units
  - `Continent/militaire.bas` - `processArmeeTask()` handles unit training
  - `Continent/militaire.bas` - `createTroupe()` function creates new units
  - `Continent/cntSRV.frm` - Server processes army formation tasks

- **Unit Composition**: Units composed of different troop types
  - `Continent/ARMEES` table - `composition` field stores unit composition
  - `Continent/militaire.bas` - Composition parsing and management

- **Unit Experience**: Units gain experience from combat and actions
  - `Continent/ARMEES` table - `experience` field tracks unit experience
  - `Continent/militaire.bas` - Experience gain in combat and travel

- **Unit Movement**: Units can move across the map
  - `Continent/militaire.bas` - `processArmeeTask()` handles "voyage" action
  - `Continent/carte.bas` - Map position updates for moving units

- **Unit Speed**: Movement speed based on composition and bonuses
  - `Continent/militaire.bas` - `getTroupeSpeed()` calculates movement speed
  - `Continent/server_tools.bas` - `getBonus()` provides navigation bonuses

- **Unit Power**: Combat power calculation based on composition and experience
  - `Continent/militaire.bas` - `getTroupeForceNoSiege()` calculates combat power
  - `Continent/militaire.bas` - Experience affects power in `doBattle()`

- **Unit Sprites**: Visual representation of units on map
  - `Continent/militaire.bas` - `getTroupeSprite()` generates unit sprites
  - `Continent/militaire.bas` - `generateTroupePic()` creates unit images
  - `Continent/carte.bas` - `updateMap()` places unit sprites on map

### Military Actions
- **Combat**: Battle resolution between units
  - `Continent/militaire.bas` - `resolveBattle()` resolves skirmishes
  - `Continent/militaire.bas` - `doBattle()` handles instant combat
  - `Continent/cntSRV.frm` - Battle resolution in server loop

- **Siege**: Siege of fortified positions
  - `Continent/militaire.bas` - `processArmeeTask()` handles "siege" action
  - `Continent/militaire.bas` - Siege resolution logic

- **Assault**: Assault on citadels
  - `Continent/militaire.bas` - `processArmeeTask()` handles "assaut" action
  - `Continent/militaire.bas` - Citadel assault resolution

- **Raid**: Raid operations
  - `Continent/militaire.bas` - Raid actions in `processArmeeTask()`

- **Garrison**: Units can garrison in villages
  - `Continent/militaire.bas` - Garrison logic in `processArmeeTask()`
  - `Continent/ARMEES` table - `action` field tracks garrison status

- **Protection**: Units can protect allied villages
  - `Continent/militaire.bas` - Protection actions in `processArmeeTask()`

- **Escort**: Units can escort convoys
  - `Continent/militaire.bas` - Escort actions in `processArmeeTask()`

### Naval Military
- **Naval Units**: Naval vessels as military units
  - `Continent/militaire.bas` - `createBateau()` creates naval units
  - `Continent/militaire.bas` - `isBoat()` checks if unit is naval
  - `Continent/ARMEES` table - Naval units stored with composition > 3999 and < 5999

- **Naval Combat**: Naval battle system
  - `Continent/militaire.bas` - Naval combat in `doBattle()` and `resolveBattle()`

- **Naval Movement**: Ship movement on water tiles
  - `Continent/militaire.bas` - `processArmeeTask()` handles naval movement
  - `Continent/militaire.bas` - Navigation actions for ships

- **Naval Repair**: Ship repair system
  - `Continent/Construction.bas` - `processRepareBoatTask()` repairs ships
  - `Continent/militaire.bas` - Ship condition tracking

- **Ship Life**: Ships have durability that degrades
  - `Continent/ARMEES` table - Ship condition/life tracking
  - `Continent/militaire.bas` - Ship degradation over time

- **Ship Sinking**: Ships can sink if not maintained
  - `Continent/evenements.bas` - Ship sinking logic
  - `Continent/militaire.bas` - Ship sinking in naval operations

### Special Military Features
- **Portal Teleportation**: Units can teleport through portals (with risk of failure)
  - `Continent/militaire.bas` - `processArmeeTask()` handles "distorsion" action
  - `Continent/militaire.bas` - Portal jump logic with success/failure rates

- **Portal Jump Requests**: Request permission for portal jumps
  - `Continent/militaire.bas` - "ASK_JUMP" action type
  - `Continent/militaire.bas` - Portal jump request handling

- **Portal Jump Authorization**: Players can authorize/refuse portal jumps
  - `Continent/militaire.bas` - Portal authorization logic
  - `Continent/militaire.bas` - Jump refusal handling

- **Distortion Travel**: Teleportation system with success/failure rates
  - `Continent/militaire.bas` - Distortion travel with random success rates
  - `Continent/militaire.bas` - Failed teleportation consequences

- **Travel**: Units travel to specific coordinates
  - `Continent/militaire.bas` - `processArmeeTask()` handles "voyage" action
  - `Continent/militaire.bas` - Travel progress and arrival logic

- **Exploration**: Units can explore special locations
  - `Continent/exploration.bas` - `processExplore()` function
  - `Continent/militaire.bas` - Calls `processExplore()` for exploration actions

### Combat System
- **Battle Resolution**: Detailed battle system
  - `Continent/militaire.bas` - `resolveBattle()` resolves skirmishes
  - `Continent/militaire.bas` - `doBattle()` handles instant combat
  - `Continent/militaire.bas` - Force calculations, casualties, experience gain

- **Defense Bonuses**: Village defense bonuses
  - `Continent/militaire.bas` - Defense bonuses in combat calculations
  - `Continent/militaire.bas` - Village fortification effects

- **Combat Results**: Victory/defeat tracking
  - `Continent/militaire.bas` - Battle outcome determination
  - `Continent/militaire.bas` - Win/loss tracking in battle results

- **Casualties**: Unit losses in combat
  - `Continent/militaire.bas` - `removeSoldatsFromTroupe()` removes casualties
  - `Continent/militaire.bas` - Casualty calculations in `doBattle()` and `resolveBattle()`

- **Battle Reports**: Detailed battle reports for players
  - `Continent/militaire.bas` - Battle result messages
  - `Continent/server_tools.bas` - `generateMessageFor()` creates battle reports

---

## Diplomacy System

### Diplomatic Relations
- **Nation Relations**: Diplomatic status between nations (War, Hostile, Neutral, Peace, Alliance)
  - `Continent/Diplo.bas` - `getDiploNation()` retrieves nation relations
  - `Continent/Diplo.bas` - `InitDiploNations()` initializes diplomatic matrix
  - `Continent/NATIONS` table - `diplomatie` field stores relation matrix

- **Player Relations**: Diplomatic relations between players/fiefs
  - `Continent/Diplo.bas` - `getDiploJoueur()` calculates player relations
  - `Continent/Diplo.bas` - `DIP_EstJoueurEnGuerre()`, `DIP_EstJoueurEnnemi()`, etc.

- **Diplomatic Status Matrix**: Matrix of relations between all nations
  - `Continent/Diplo.bas` - `arrDiploNations()` array stores relation matrix
  - `Continent/Diplo.bas` - `InitDiploNations()` builds matrix from database

- **Alliance System**: Military alliances between players
  - `Continent/Diplo.bas` - `allianceEntre()` checks for alliances
  - `Continent/Diplo.bas` - Alliances override national diplomatic status

- **Pact Effects**: Pacts affect diplomatic relations
  - `Continent/Pactes.bas` - `PAC_EstParia()`, `PAC_EstPNA()` check pact status
  - `Continent/Diplo.bas` - Pact effects in `getDiploJoueur()`

### Diplomatic Features
- **Ambassadors**: Ambassador system for diplomatic relations
  - `Continent/Diplo.bas` - `DIP_NbAmbassadeursAmis()`, `DIP_NbAmbassadeursEnnemis()`
  - `Continent/AMBASSADES` table - Stores ambassador data
  - `Continent/cntSRV.frm` - Ambassador management in server

- **Embassy Management**: Count of friendly/enemy ambassadors
  - `Continent/Diplo.bas` - Ambassador counting functions
  - `Continent/cntSRV.frm` - Embassy management interface

- **Pariah Status**: Players can be declared pariahs by nations
  - `Continent/Pactes.bas` - `PAC_EstParia()`, `PAC_setParia()`, `PAC_unsetParia()`
  - `Continent/PACTES` table - Stores pariah status (PDR)

- **Non-Aggression Pacts**: Pacts of non-aggression (PNA)
  - `Continent/Pactes.bas` - `PAC_EstPNA()`, `PAC_setPNA()`, `PAC_unsetPNA()`
  - `Continent/PACTES` table - Stores PNA pacts

- **Diplomatic Override**: Alliances override national diplomatic status
  - `Continent/Diplo.bas` - `getDiploJoueur()` checks alliances first

---

## Guild System

### Guild Types
- **Commerce Guild**: Trade and economic guild
  - `Continent/guildes.bas` - Commerce guild operations
  - `Continent/NIVEAUX_GUILDES` table - `commerce` field tracks level

- **Shadow Guild**: Secret operations guild
  - `Continent/guildes.bas` - Shadow guild (ombre) operations
  - `Continent/NIVEAUX_GUILDES` table - `ombre` field tracks level

- **Saffron Guild**: Specialized guild
  - `Continent/guildes.bas` - Saffron guild operations
  - `Continent/NIVEAUX_GUILDES` table - `saffran` field tracks level

- **Church Guild**: Religious guild
  - `Continent/guildes.bas` - Church guild (eglise) operations
  - `Continent/NIVEAUX_GUILDES` table - `eglise` field tracks level

### Guild Services
- **Banking**: Interest-bearing bank accounts
  - `Continent/guildes.bas` - `processGuildeTask()` handles banking
  - `Continent/guildes.bas` - Interest calculations with `BANQUE_TAUX_INTERET`

- **Loans**: Debt system with repayment
  - `Continent/guildes.bas` - `processGuildeTask()` handles debt repayment
  - `Continent/guildes.bas` - Loan management

- **Artifact Market**: Market for magical artifacts
  - `Continent/guildes.bas` - `updateMarcheArtefacts()` updates artifact market
  - `Continent/guildes.bas` - `getObjetValue()` calculates artifact values
  - `Continent/MARCHE_ARTEFACTS` table - Stores artifact market data

- **Auction System**: Auction system for artifacts
  - `Continent/guildes.bas` - Auction resolution logic
  - `Continent/guildes.bas` - `updateCours()` updates auction prices

- **Delivery Service**: Guild delivery of goods
  - `Continent/guildes.bas` - `processGuildeTask()` handles deliveries
  - `Continent/guildes.bas` - Delivery logistics

- **Black Market**: Black market operations
  - `Continent/guildes.bas` - Black market functionality

### Guild Features
- **Guild Reputation**: Reputation levels with different guilds
  - `Continent/NIVEAUX_GUILDES` table - Tracks reputation levels per guild
  - `Continent/guildes.bas` - Reputation management

- **Guild Levels**: Level progression in guilds
  - `Continent/NIVEAUX_GUILDES` table - Level tracking
  - `Continent/cntSRV.frm` - Level normalization in server loop

- **Lottery**: Guild-run lottery system
  - `Continent/guildes.bas` - Lottery functionality

- **Artifact Valuation**: Dynamic artifact pricing
  - `Continent/guildes.bas` - `getObjetValue()` calculates values
  - `Continent/guildes.bas` - `updateCours()` updates prices

- **Market Updates**: Regular market updates and price fluctuations
  - `Continent/guildes.bas` - `updateCours()` updates market prices
  - `Continent/cntSRV.frm` - Market updates in server loop

### Alchemy
- **Alchemical Effects**: Temporary magical effects
  - `Continent/guildes.bas` - `processAlchimieTask()` handles alchemy
  - `Continent/guildes.bas` - Alchemical effect application

- **Alchemical Cancellation**: Cancel alchemical effects
  - `Continent/guildes.bas` - `processAlchimieTask()` handles cancellation

- **Alchemical Duration**: Time-limited magical bonuses
  - `Continent/guildes.bas` - Duration tracking in alchemy tasks

---

## Exploration System

### Location Exploration
- **Location Discovery**: Discover and explore special locations
  - `Continent/exploration.bas` - `processExplore()` function handles exploration
  - `Continent/militaire.bas` - Calls `processExplore()` for exploration actions
  - `Continent/LIEUX` table - Stores location data

- **Location Content**: Locations contain treasures, monsters, events
  - `Continent/exploration.bas` - `generateContenuLieu()` generates location content
  - `Continent/exploration.bas` - Content parsing and application

- **Location Generation**: Dynamic location content generation
  - `Continent/exploration.bas` - `generateContenuLieu()` creates location content
  - `Continent/exploration.bas` - Random content generation

- **Location Visits**: Track last visit to locations
  - `Continent/LIEUX` table - `last_visit` field tracks visits
  - `Continent/exploration.bas` - Updates `last_visit` after exploration

- **Location Recharge**: Locations can recharge over time
  - `Continent/exploration.bas` - Location recharge logic
  - `Continent/LIEUX` table - Recharge tracking

### Exploration Results
- **Treasure Discovery**: Find treasures (resources, artifacts)
  - `Continent/exploration.bas` - Treasure discovery in `processExplore()`
  - `Continent/exploration.bas` - Resource and artifact rewards

- **Monster Encounters**: Encounter monsters during exploration
  - `Continent/exploration.bas` - Monster encounters trigger combat
  - `Continent/exploration.bas` - Calls `doBattle()` for monster combat

- **Artifact Discovery**: Find powerful artifacts
  - `Continent/exploration.bas` - Artifact discovery logic
  - `Continent/exploration.bas` - Artifact rewards

- **Super Treasures**: Discover unique super treasures
  - `Continent/exploration.bas` - Super treasure discovery

- **Messages**: Encoded messages in locations
  - `Continent/exploration.bas` - `encodeMessage()` encodes messages
  - `Continent/exploration.bas` - Message discovery and decoding

- **Events**: Trigger special events from exploration
  - `Continent/exploration.bas` - Event triggering from exploration
  - `Continent/exploration.bas` - Special event handling

- **Experience Gain**: Units gain experience from exploration
  - `Continent/exploration.bas` - Experience rewards from exploration

### Exploration Mechanics
- **Combat in Exploration**: Combat can occur during exploration
  - `Continent/exploration.bas` - Calls `doBattle()` for combat encounters
  - `Continent/militaire.bas` - `doBattle()` resolves exploration combat

- **Unit Loss**: Units can be lost during exploration
  - `Continent/exploration.bas` - Unit loss handling
  - `Continent/exploration.bas` - Checks if unit exists before exploration

- **Location Exit**: Units exit locations after exploration
  - `Continent/exploration.bas` - Unit exit logic
  - `Continent/exploration.bas` - Map position updates after exit

- **Exploration Priority**: Priority system for exploration results
  - `Continent/exploration.bas` - Priority handling in `processExplore()`

---

## Research System

### Science Research
- **Research Progress**: Research progresses over time
  - `Continent/recherche.bas` - `processRechercheTask()` advances research
  - `Continent/recherche.bas` - `avancement` calculation with bonuses
  - `Continent/cntSRV.frm` - Server processes research tasks

- **Research Levels**: Multiple levels of research per science
  - `Continent/BONUS` table - Stores research levels per player
  - `Continent/recherche.bas` - Level tracking and progression

- **Research Costs**: Research costs money (researcher salaries)
  - `Continent/recherche.bas` - Cost calculation in `processRechercheTask()`
  - `Continent/recherche.bas` - Financial requirements for research

- **Research Bonuses**: Bonuses affect research speed
  - `Continent/recherche.bas` - `getBonus(joueur, "SCIENCE")` provides bonuses
  - `Continent/recherche.bas` - Morale and bonus effects on research speed

- **Research Completion**: Research completion grants bonuses
  - `Continent/recherche.bas` - Completion detection and bonus application
  - `Continent/BONUS` table - Bonus storage after completion

### Research Types
- **Combat Sciences**: Military research
  - `Continent/TYPE_BONUS` table - Combat science types
  - `Continent/recherche.bas` - Combat research handling

- **Production Sciences**: Production efficiency research
  - `Continent/TYPE_BONUS` table - Production science types
  - `Continent/recherche.bas` - Production research handling

- **Navigation Sciences**: Naval and movement research
  - `Continent/TYPE_BONUS` table - Navigation science types
  - `Continent/recherche.bas` - Navigation research handling

- **Magic Sciences**: Magical research (levels 600-999)
  - `Continent/recherche.bas` - Magic research detection (levels 600-999)
  - `Continent/recherche.bas` - Special handling for magic sciences

- **Specialized Production**: Special production research
  - `Continent/TYPE_BONUS` table - Specialized production types
  - `Continent/recherche.bas` - Specialized research handling

### Research Effects
- **Automatic Updates**: Research automatically updates unit stats
  - `Continent/server_tools.bas` - `getBonus()` retrieves research bonuses
  - `Continent/militaire.bas` - Bonuses applied to unit calculations

- **Combat Power Updates**: Combat research updates unit power
  - `Continent/militaire.bas` - `getBonus(joueur, "COMBAT")` affects combat power
  - `Continent/militaire.bas` - Combat bonuses in `getTroupeForceNoSiege()`

- **Movement Updates**: Navigation research updates movement speed
  - `Continent/militaire.bas` - `getBonus(joueur, "NAVIGATION")` affects speed
  - `Continent/militaire.bas` - Navigation bonuses in `getTroupeSpeed()`

- **Reputation Gain**: Research completion increases reputation
  - `Continent/recherche.bas` - Reputation updates on completion
  - `Continent/VILLAGES` table - Reputation field updates

- **Rank Increase**: Research completion increases rank
  - `Continent/recherche.bas` - Rank updates on completion
  - `Continent/server_tools.bas` - `augmenteRang()` function

---

## Feudalism & Vassalage

### Vassal System
- **Vassalization**: Players can become vassals of other players
  - `Continent/militaire.bas` - `changeSuzerain()` function handles vassalization
  - `Continent/VILLAGES` table - `suzerain` field stores suzerain ID
  - `Continent/Fief.bas` - Fief management functions

- **Suzerain System**: Suzerain-vassal relationships
  - `Continent/militaire.bas` - `changeSuzerain()` manages relationships
  - `Continent/VILLAGES` table - Suzerain tracking
  - `Continent/feodalisme.bas` - Feudal relationship functions

- **Vassal Protection**: Suzerains must protect vassals
  - `Continent/feodalisme.bas` - `checkPresenceSuzeniale()` checks protection
  - `Continent/militaire.bas` - Protection requirements

- **Required Garrison**: Minimum military presence required for vassals
  - `Continent/feodalisme.bas` - `getSuzerainRequiredLames()` calculates required garrison
  - `Continent/feodalisme.bas` - `checkPresenceSuzeniale()` validates presence

- **Vassal Tax**: Tax system between suzerain and vassal
  - `Continent/VILLAGES` table - `taxe_suz` field stores tax rate
  - `Continent/militaire.bas` - Tax collection in `changeSuzerain()`
  - `Continent/production.bas` - Tax handling in treasury management

### Feudal Mechanics
- **Suzerain Authority**: Suzerains have authority over vassals
  - `Continent/militaire.bas` - Authority in `changeSuzerain()`
  - `Continent/feodalisme.bas` - Authority calculations

- **Vassal Loss Penalties**: Penalties for losing vassals
  - `Continent/militaire.bas` - `changeSuzerain()` applies penalties to former suzerain
  - `Continent/militaire.bas` - Reputation and rank penalties

- **Feudal Reputation**: Reputation affected by feudal management
  - `Continent/militaire.bas` - Reputation updates in `changeSuzerain()`
  - `Continent/VILLAGES` table - Reputation field

- **Vassal Independence**: Vassals can break free
  - `Continent/militaire.bas` - Vassal independence logic
  - `Continent/militaire.bas` - Breaking vassalage

- **Feudal Relations**: Diplomatic relations affect vassal requirements
  - `Continent/feodalisme.bas` - Diplomatic effects on vassalage
  - `Continent/Diplo.bas` - Relation checks

### Influence System
- **Political Influence**: Players can influence other players' populations
  - `Continent/INFLUENCES` table - Stores influence data
  - `Continent/Diplomatie.bas` - Influence management

- **Influence Resistance**: Resistance to influence
  - `Continent/Diplomatie.bas` - Resistance calculations
  - `Continent/INFLUENCES` table - Resistance tracking

- **Influence Effects**: Influence affects various game mechanics
  - `Continent/Diplomatie.bas` - Influence application
  - `Continent/evenements.bas` - Influence effects on events

- **Revolt Management**: Influence can cause or stop revolts
  - `Continent/evenements.bas` - `processRevolteTask()` handles revolts
  - `Continent/evenements.bas` - Planned revolts from influence

---

## Events & Random Events

### Random Events
- **Disease System**: Epidemic system with multiple disease types
  - `Continent/evenements.bas` - `RandomEvents()` function generates diseases
  - `Continent/evenements.bas` - `processMaladieTask()` handles disease progression
  - `Continent/ACTIONS` table - Disease actions stored with type 'MALADIE'

- **Disease Contagion**: Diseases spread through population
  - `Continent/evenements.bas` - Contagion calculations in `RandomEvents()`
  - `Continent/evenements.bas` - `MALADIE_CONTAGION_*` parameters control spread

- **Disease Treatment**: Medicine consumption for disease treatment
  - `Continent/evenements.bas` - Medicine consumption in `processMaladieTask()`
  - `Continent/INVENTAIRE` table - Medicine (denree=10) consumption

- **Disease Mortality**: Diseases can kill population
  - `Continent/evenements.bas` - Mortality calculations in `processMaladieTask()`
  - `Continent/evenements.bas` - Population reduction from diseases

- **Disease Recovery**: Natural and medical recovery from diseases
  - `Continent/evenements.bas` - Recovery calculations in `processMaladieTask()`
  - `Continent/evenements.bas` - `MALADIE_GUERISON_*` parameters control recovery

### Monster Events
- **Monster Attacks**: Random monster attacks on villages
  - `Continent/evenements.bas` - `attaqueMonstres()` function
  - `Continent/evenements.bas` - `addMonstre()` adds monsters to map
  - `Continent/cntSRV.frm` - Monster attack processing

- **Monster Raids**: Monster raids with pillaging
  - `Continent/evenements.bas` - Raid logic in `attaqueMonstres()`
  - `Continent/evenements.bas` - Pillaging effects

- **Monster Movement**: Monsters move across the map
  - `Continent/evenements.bas` - Monster movement logic
  - `Continent/carte.bas` - Monster sprite updates

- **Monster Aggressiveness**: Increased monster activity in winter
  - `Continent/evenements.bas` - Winter effects on monsters
  - `Continent/evenements.bas` - Seasonal monster behavior

- **Monster Escarmouches**: Random skirmishes with monsters
  - `Continent/evenements.bas` - `generateEscarmouches()` function
  - `Continent/militaire.bas` - Combat resolution for skirmishes

### Revolts
- **Revolt System**: Population revolts against player
  - `Continent/evenements.bas` - `processRevolteTask()` handles revolts
  - `Continent/ACTIONS` table - Revolt actions stored
  - `Continent/evenements.bas` - `generateRumeurs()` generates revolt rumors

- **Revolt Causes**: Various causes for revolts
  - `Continent/evenements.bas` - Multiple revolt triggers
  - `Continent/INFLUENCES` table - External influence causes revolts

- **Revolt Resolution**: Revolts can be resolved diplomatically or by force
  - `Continent/evenements.bas` - Resolution logic in `processRevolteTask()`
  - `Continent/evenements.bas` - Diplomatic and military resolution

- **Revolt Effects**: Revolts affect production and reputation
  - `Continent/evenements.bas` - Production reduction during revolts
  - `Continent/evenements.bas` - Reputation penalties

- **Planned Revolts**: Revolts can be planned by external influence
  - `Continent/evenements.bas` - Planned revolt logic in `processRevolteTask()`
  - `Continent/INFLUENCES` table - Influence-based revolts

### Other Events
- **Building Collapse**: Buildings collapse if not maintained
  - `Continent/evenements.bas` - Building collapse detection
  - `Continent/cntSRV.frm` - Collapse processing

- **Fires**: Forest fires that spread
  - `Continent/carte.bas` - `generateIncendies()` generates fires
  - `Continent/carte.bas` - `allumeIncendie()` starts fires
  - `Continent/carte.bas` - Fire propagation logic

- **Weather Effects**: Weather affects various game mechanics
  - `Continent/evenements.bas` - Weather event handling
  - `Continent/cntSRV.frm` - Weather effects on production, naval, etc.

- **RP Events**: Role-playing events system
  - `Continent/evenements.bas` - `createRandomRPE()` generates RP events
  - `Continent/evenements.bas` - `createPlanifiedRPE()` creates scheduled RP events
  - `Continent/RP_EVENTS` table - RP event definitions
  - `Continent/RP_PLANIF` table - Scheduled RP events

- **Scheduled Events**: Events scheduled for specific cycles/turns
  - `Continent/evenements.bas` - Event scheduling logic
  - `Continent/RP_PLANIF` table - Scheduled events
  - `Continent/RP_SCRIPT` table - Event scripts

---

## Map & Territory Management

### Map System
- **Hexagonal Map**: Hexagonal grid-based map system
  - `Continent/carte.bas` - Hexagonal coordinate calculations
  - `Continent/carte.bas` - `getCases()` handles hexagonal offsets
  - `Continent/cntSRV.frm` - `MAP_WIDTH` parameter defines map size

- **Map Layers**: Multiple map layers (terrain, objects, units)
  - `Continent/carte.bas` - `getMap()` and `updateMap()` work with layers
  - `Continent/carte.bas` - Layer 1 (terrain), Layer 2 (objects/sprites), Layer 3 (territory)
  - `Continent/map/` directory - Binary map files (layer0.map, layer1.map)

- **Map Coordinates**: X,Y coordinate system
  - `Continent/carte.bas` - Coordinate calculations
  - `Continent/carte.bas` - Position conversion: `pos = 1 + x + (y * MAP_WIDTH)`

- **Map Sprites**: Visual representation system with sprites
  - `Continent/carte.bas` - `updateMap()` places sprites on layer 2
  - `Continent/militaire.bas` - `getTroupeSprite()` generates unit sprites
  - `Continent/carte.bas` - Sprite management

- **Map Updates**: Dynamic map updates during turn resolution
  - `Continent/carte.bas` - `normaliseCarte()` updates map each turn
  - `Continent/cntSRV.frm` - Map normalization in server loop

### Map Features
- **Terrain Types**: Various terrain types (land, water, mountains, etc.)
  - `Continent/carte.bas` - Terrain type checking (layer 1)
  - `Continent/carte.bas` - Terrain validation (e.g., `getMap(1, pos) > 19` for land)

- **Obstacles**: Obstacles on map (trees, buildings, etc.)
  - `Continent/carte.bas` - Obstacle checking on layer 2
  - `Continent/carte.bas` - `getMap(2, pos)` retrieves obstacles

- **Resource Nodes**: Natural resources on map
  - `Continent/carte.bas` - Resource placement in `normaliseCarte()`
  - `Continent/MAP_SPECIAL` table - Special map features

- **Special Locations**: Special locations for exploration
  - `Continent/LIEUX` table - Special locations
  - `Continent/exploration.bas` - Location exploration

- **Treasure Spawning**: Random treasure placement
  - `Continent/carte.bas` - Treasure placement in `normaliseCarte()`
  - `Continent/carte.bas` - Random treasure generation

### Map Management
- **Map Normalization**: Map cleanup and normalization
  - `Continent/carte.bas` - `normaliseCarte()` main normalization function
  - `Continent/carte.bas` - Worker removal, tree planting, animal spawning
  - `Continent/cntSRV.frm` - Called each turn

- **Sprite Management**: Sprite placement and removal
  - `Continent/carte.bas` - `updateMap()` places/removes sprites
  - `Continent/carte.bas` - `normaliseTroupes()` manages unit sprites

- **Case Locking**: Case locking for construction sites
  - `Continent/carte.bas` - Sprite 254 and 255 used for locked cases
  - `Continent/Construction.bas` - Case locking during construction

- **Pathfinding**: Pathfinding for unit movement
  - `Continent/militaire.bas` - Pathfinding in `processArmeeTask()`
  - `Continent/militaire.bas` - Movement calculations

- **Distance Calculation**: Distance calculations between points
  - `Continent/militaire.bas` - Distance calculations: `Sqr((nx * nx) + (ny * ny))`
  - `Continent/server_tools.bas` - `getDistanceBetween()` function

### Seasonal Map Effects
- **Tree Growth**: Trees grow over time
  - `Continent/carte.bas` - Tree growth in `normaliseCarte()`
  - `Continent/carte.bas` - Tree planting and growth logic

- **Forest Regeneration**: Forest regeneration system
  - `Continent/carte.bas` - Forest regeneration in `normaliseCarte()`
  - `Continent/carte.bas` - Tree placement algorithms

- **Animal Spawning**: Wild animals spawn on map
  - `Continent/carte.bas` - Animal spawning in `normaliseCarte()`
  - `Continent/carte.bas` - `getCaseLibreSauvage()` finds spawn locations

- **Monster Spawning**: Monsters spawn on map
  - `Continent/evenements.bas` - `addMonstre()` adds monsters
  - `Continent/carte.bas` - Monster sprite placement

- **Fire Propagation**: Forest fires spread
  - `Continent/carte.bas` - `generateIncendies()` generates fires
  - `Continent/carte.bas` - `allumeIncendie()` starts fires
  - `Continent/carte.bas` - Fire spread logic

- **Weather Effects on Map**: Weather affects map elements
  - `Continent/carte.bas` - Weather effects in normalization
  - `Continent/evenements.bas` - Weather event effects

---

## Trade & Economy

### Economic System
- **Currency System**: Gold/écus currency system
  - `Continent/VILLAGES` table - `tresor` field stores gold/écus
  - `Continent/server_tools.bas` - `addEntreeTresor()` manages treasury
  - `Continent/production.bas` - `handleTresor()` manages village treasury

- **Resource Trading**: Trading of various resources
  - `Continent/Diplomatie.bas` - Trading functions
  - `Continent/INVENTAIRE` table - Resource storage
  - `Continent/server_tools.bas` - `addEntreeStocks()` manages inventory

- **Market Prices**: Dynamic market prices
  - `Continent/guildes.bas` - `updateCours()` updates market prices
  - `Continent/guildes.bas` - Price calculations

- **Price Fluctuations**: Prices change based on supply/demand
  - `Continent/guildes.bas` - Price fluctuation logic
  - `Continent/cntSRV.frm` - Market updates in server loop

- **Stock Management**: Inventory management system
  - `Continent/INVENTAIRE` table - Stores player inventories
  - `Continent/server_tools.bas` - `addEntreeStocks()` manages stocks
  - `Continent/server_tools.bas` - `getVal()` and `setVal()` for inventory

### Trade Features
- **Guild Commerce**: Trade through guilds
  - `Continent/guildes.bas` - Guild commerce operations
  - `Continent/guildes.bas` - `processGuildeTask()` handles commerce
  - `Continent/NIVEAUX_GUILDES` table - Commerce guild levels

- **Market Updates**: Regular market price updates
  - `Continent/guildes.bas` - `updateCours()` updates prices
  - `Continent/cntSRV.frm` - Regular market updates

- **Trade Routes**: Trade route system
  - `Continent/militaire.bas` - Trade route actions
  - `Continent/ARMEES` table - Trade route tracking

- **Convoys**: Trade convoy system
  - `Continent/militaire.bas` - Convoy actions in `processArmeeTask()`
  - `Continent/ARMEES` table - Convoy tracking (action like 'CONVOI-%')

- **Black Market**: Black market trading
  - `Continent/guildes.bas` - Black market operations
  - `Continent/guildes.bas` - Shadow guild black market

### Economic Mechanics
- **Interest System**: Bank interest on deposits
  - `Continent/guildes.bas` - `processGuildeTask()` calculates interest
  - `Continent/guildes.bas` - `BANQUE_TAUX_INTERET` parameter
  - `Continent/guildes.bas` - Interest payments

- **Loan System**: Loan and debt system
  - `Continent/guildes.bas` - `processGuildeTask()` handles loans
  - `Continent/guildes.bas` - Debt repayment logic

- **Tax System**: Tax collection from population
  - `Continent/production.bas` - `handleTresor()` collects taxes
  - `Continent/VILLAGES` table - `taxe` field stores tax rate
  - `Continent/server_tools.bas` - Tax calculations with `getBonus(joueur, "TAXE_ACC")`

- **Reputation Effects**: Reputation affects economic opportunities
  - `Continent/VILLAGES` table - `reputation` field
  - `Continent/guildes.bas` - Reputation affects guild services
  - `Continent/production.bas` - Reputation affects market income

---

## Naval System

### Naval Operations
- **Deep Sea Fishing**: Extended fishing campaigns
  - `Continent/Productions.bas` - `PROD_ResultatPechehauturiere()` function
  - `Continent/militaire.bas` - `processArmeeTask()` handles fishing campaigns
  - `Continent/militaire.bas` - Fishing action type 'peche-%'

- **Naval Travel**: Ship movement across water
  - `Continent/militaire.bas` - `processArmeeTask()` handles naval movement
  - `Continent/militaire.bas` - Navigation actions for ships
  - `Continent/militaire.bas` - Ship movement on water tiles

- **Naval Combat**: Naval battle system
  - `Continent/militaire.bas` - `doBattle()` and `resolveBattle()` handle naval combat
  - `Continent/militaire.bas` - Naval units in combat

- **Ship Maintenance**: Ship repair and maintenance
  - `Continent/Construction.bas` - `processRepareBoatTask()` repairs ships
  - `Continent/militaire.bas` - Ship maintenance tracking

- **Ship Durability**: Ship condition system
  - `Continent/ARMEES` table - Ship condition/life tracking
  - `Continent/militaire.bas` - Ship degradation over time
  - `Continent/evenements.bas` - Ship sinking from poor condition

### Naval Mechanics
- **Weather Effects**: Weather affects naval operations
  - `Continent/militaire.bas` - Weather effects on naval movement
  - `Continent/evenements.bas` - Weather events affect ships

- **Ship Sinking**: Ships can sink from damage or poor maintenance
  - `Continent/evenements.bas` - Ship sinking logic
  - `Continent/militaire.bas` - Ship sinking from damage
  - `Continent/evenements.bas` - Ship condition checks

- **Naval Experience**: Ships gain experience
  - `Continent/ARMEES` table - `experience` field for ships
  - `Continent/militaire.bas` - Experience gain from naval operations

- **Fishing Results**: Variable fishing results based on conditions
  - `Continent/Productions.bas` - `PROD_ResultatPechehauturiere()` calculates results
  - `Continent/militaire.bas` - Fishing result variations

- **Naval Bonuses**: Navigation bonuses affect naval operations
  - `Continent/militaire.bas` - `getBonus(joueur, "NAVIGATION")` affects naval speed
  - `Continent/militaire.bas` - `getBonus(joueur, "NAVAL_ACC")` affects construction
  - `Continent/server_tools.bas` - `getBonus()` retrieves bonuses

---

## Heroes System

### Hero Management
- **Hero Recruitment**: Recruit powerful hero units
  - `Continent/militaire.bas` - `isHeros()` checks if unit is hero (composition > 9999)
  - `Continent/militaire.bas` - Hero unit creation
  - `Continent/ARMEES` table - Heroes stored with special composition IDs

- **Hero Maintenance**: Heroes require payment (money or sacrifices)
  - `Continent/militaire.bas` - Hero maintenance logic
  - `Continent/militaire.bas` - Payment and sacrifice requirements

- **Hero Resurrection**: Heroes can be resurrected with special items
  - `Continent/militaire.bas` - Hero resurrection logic
  - `Continent/INVENTAIRE` table - Special items for resurrection

- **Hero Requirements**: Heroes require palaces
  - `Continent/CONSTRUCTIONS` table - Palace building requirements
  - `Continent/militaire.bas` - Palace validation for heroes

- **Hero Departure**: Heroes leave if not paid or if palace destroyed
  - `Continent/militaire.bas` - Hero departure logic
  - `Continent/militaire.bas` - Payment failure handling

### Hero Features
- **Hero Salaries**: Heroes require regular payment
  - `Continent/militaire.bas` - Salary payment logic
  - `Continent/VILLAGES` table - Treasury used for payments

- **Hero Sacrifices**: Some heroes require population sacrifices
  - `Continent/militaire.bas` - Sacrifice requirements
  - `Continent/VILLAGES` table - Population reduction for sacrifices

- **Hero Resurrection Cost**: Resurrection requires special items (blue stones)
  - `Continent/militaire.bas` - Resurrection item requirements
  - `Continent/INVENTAIRE` table - Special items (blue stones)

- **Hero Experience Loss**: Heroes lose experience on death
  - `Continent/militaire.bas` - Experience loss on hero death
  - `Continent/ARMEES` table - Experience tracking

- **Hero Reputation**: Hero management affects reputation
  - `Continent/militaire.bas` - Reputation effects from hero management
  - `Continent/VILLAGES` table - Reputation updates

---

## Swag System

### Swag Competition
- **Team System**: Teams compete in swag matches
  - `Continent/swag.bas` - `resolveSwagJournee()` processes swag day
  - `Continent/SWAG_TEAMS` table - Team data
  - `Continent/SWAG_MATCHS` table - Match data

- **Match Resolution**: Match results based on strategies
  - `Continent/swag.bas` - `resolveSwagMatch()` resolves matches
  - `Continent/swag.bas` - Strategy-based resolution

- **Strategy System**: Different strategies for matches
  - `Continent/swag.bas` - Strategy handling in `resolveSwagMatch()`
  - `Continent/SWAG_TEAMS` table - `strategie` field stores strategies
  - `Continent/swag.bas` - `swagGetBonusCombinaison()` calculates strategy bonuses

- **Round System**: Multiple rounds per match
  - `Continent/swag.bas` - Round system in `resolveSwagMatch()`
  - `Continent/SWAG_POULES` table - Round tracking
  - `Continent/swag.bas` - Round progression

- **Victory/Defeat**: Win/loss tracking
  - `Continent/swag.bas` - Victory/defeat determination
  - `Continent/SWAG_TEAMS` table - `victoires`, `defaites` fields
  - `Continent/swag.bas` - Win/loss updates

### Swag Features
- **Arena Requirements**: Matches require arenas
  - `Continent/CONSTRUCTIONS` table - Arena building requirements
  - `Continent/swag.bas` - Arena validation

- **Portal Requirements**: Portals needed for matches
  - `Continent/CONSTRUCTIONS` table - Portal building requirements
  - `Continent/swag.bas` - Portal validation for matches

- **Reputation Effects**: Swag results affect reputation
  - `Continent/swag.bas` - Reputation updates from swag results
  - `Continent/VILLAGES` table - Reputation field updates

- **Prize Money**: Financial rewards for victories
  - `Continent/swag.bas` - `addEntreeTresor()` awards prize money
  - `Continent/swag.bas` - Financial rewards in `resolveSwagMatch()`

- **Experience System**: Teams gain experience
  - `Continent/swag.bas` - Experience gain in `resolveSwagMatch()`
  - `Continent/SWAG_TEAMS` table - `experience` field
  - `Continent/swag.bas` - Experience calculations

---

## Pacts & Treaties

### Pact Types
- **Pariah Status (PDR)**: Outcast status with nations
  - `Continent/Pactes.bas` - `PAC_EstParia()` checks pariah status
  - `Continent/Pactes.bas` - `PAC_setParia()`, `PAC_unsetParia()` manage pariah
  - `Continent/PACTES` table - Stores pariah pacts (nature='PDR')

- **Non-Aggression Pacts (PNA)**: Non-aggression agreements
  - `Continent/Pactes.bas` - `PAC_EstPNA()` checks PNA status
  - `Continent/Pactes.bas` - `PAC_setPNA()`, `PAC_unsetPNA()` manage PNA
  - `Continent/PACTES` table - Stores PNA pacts (nature='PNG')

- **Vassal Pacts (PSV)**: Temporary vassal pacts after capture
  - `Continent/Pactes.bas` - PSV pact management
  - `Continent/PACTES` table - Stores PSV pacts
  - `Continent/militaire.bas` - PSV creation on capture

### Pact Management
- **Pact Duration**: Time-limited pacts
  - `Continent/PACTES` table - `duree` field stores duration
  - `Continent/Pactes.bas` - Duration tracking and expiration

- **Pact Modification**: Pacts modified on suzerain change
  - `Continent/Pactes.bas` - `PAC_ModifPactesSurChangeSuzerain()` function
  - `Continent/militaire.bas` - Calls pact modification in `changeSuzerain()`

- **Pact Inheritance**: Vassals inherit suzerain pacts
  - `Continent/Pactes.bas` - `PAC_ModifPactesSurChangeSuzerain()` inherits pacts
  - `Continent/Pactes.bas` - PNA and Pariah inheritance logic

- **Pact Conflicts**: Pacts can conflict with each other
  - `Continent/Pactes.bas` - Conflict detection in `PAC_setPNA()`
  - `Continent/Diplo.bas` - Pact conflict resolution in `getDiploJoueur()`

---

## Infrastructure & Utilities

### Server Infrastructure
- **Multi-Server Support**: Support for multiple server configurations
  - `Continent/servers/` directory - Server configuration files (continent-DEV.ini, continent-CONTIBOX1.ini)
  - `Continent/Parametres.bas` - Server parameter management
  - `Continent/cntSRV.frm` - Server object with `serverParams` collection

- **Configuration Files**: INI-based configuration system
  - `Continent/servers/*.ini` - INI configuration files
  - `Continent/Parametres.bas` - Configuration loading
  - `Continent/outils_serveur.bas` - `loadConfig()` function

- **Database Connection**: MySQL database connectivity
  - `Continent/mysql.bas` - MySQL connection management
  - `Continent/outils_serveur.bas` - `ServerConnect()` function
  - `Continent/AccesBDD.bas` - Database access functions
  - `Continent/cntSRV.frm` - `mySql` connection object

- **Logging System**: Comprehensive logging system
  - `Continent/server_tools.bas` - `Logit()` function for logging
  - `Continent/server_tools.bas` - `LogNoFile()` for console logging
  - `Continent/logs/` directory - Log files
  - `Continent/cntSRV.frm` - `logfile` and `logfileerr` properties

- **Error Handling**: Error handling and reporting
  - `Continent/Erreur.bas` - Error handling module
  - `Continent/cntSRV.frm` - `safemode` error handling
  - `Continent/outils.bas` - Error handling functions

### Utility Systems
- **Message System**: In-game messaging system
  - `Continent/server_tools.bas` - `generateMessageFor()` creates messages
  - `Continent/MESSAGES_INTENDANT` table - Stores messages
  - `Continent/cntSRV.frm` - Message generation

- **Gazette System**: News and announcements system
  - `Continent/server_tools.bas` - `AddEncartGazette()` adds gazette entries
  - `Continent/ENCARTS_GAZETTE` table - Gazette entries
  - `Continent/cntSRV.frm` - Gazette management

- **Shadow Log**: Secret log of player actions
  - `Continent/server_tools.bas` - `shadowLog()` function
  - `Continent/LOG_OMBRE` table - Shadow log entries
  - `Continent/militaire.bas`, `Continent/Diplomatie.bas` - Shadow log usage

- **Chronicles**: Historical record of fief events
  - `Continent/server_tools.bas` - `chroniclesLog()` function
  - `Continent/HISTOIRE` table - Chronicles storage
  - `Continent/cntSRV.frm` - Chronicle generation

- **Rank System**: Player rank and title system
  - `Continent/server_tools.bas` - `getRang()`, `getRangNiveau()`, `augmenteRang()` functions
  - `Continent/VILLAGES` table - `rang` field
  - `Continent/server_tools.bas` - Rank calculations

- **Reputation System**: Reputation tracking and effects
  - `Continent/VILLAGES` table - `reputation` field
  - `Continent/server_tools.bas` - Reputation management
  - `Continent/militaire.bas`, `Continent/production.bas` - Reputation effects

### Administrative Tools
- **Database Dumps**: Database backup and restore tools
  - `Continent/basedump.bas` - Database dump functions
  - `Continent/restore_tools.bas` - Database restore functions
  - `Continent/restore.frm` - Restore interface
  - `Continent/dumpthisbase.frm` - Dump interface

- **Server Tools**: Various server administration tools
  - `Continent/server_tools.bas` - Server utility functions
  - `Continent/cntSRV.frm` - Server administration interface
  - `Continent/outils_serveur.bas` - Server tools

- **Map Tools**: Map generation and manipulation tools
  - `Continent/carte.bas` - Map manipulation functions
  - `Continent/map/` directory - Map files
  - `Continent/cntSRV.frm` - Map generation tools

- **Image Generation**: Automatic image generation for units
  - `Continent/militaire.bas` - `generateTroupePic()` generates unit images
  - `Continent/gdi/` directory - GDI+ image processing
  - `Continent/pics/` directory - Generated images
  - `Continent/pics/gentroupespics.bat` - Batch image generation

---

## Additional Features

### Population Management
- **Peons**: Worker population
  - `Continent/VILLAGES` table - `peons` field
  - `Continent/production.bas`, `Continent/Construction.bas` - Peon usage
  - `Continent/cntSRV.frm` - Peon management

- **Bourgeois**: Middle class population
  - `Continent/VILLAGES` table - `bourgeois` field
  - `Continent/evenements.bas` - Bourgeois effects on events
  - `Continent/production.bas` - Bourgeois effects on production

- **Population Growth**: Population growth mechanics
  - `Continent/cntSRV.frm` - Population growth calculations
  - `Continent/VILLAGES` table - Population tracking

- **Population Morale**: Morale system affecting various mechanics
  - `Continent/VILLAGES` table - `moral` field
  - `Continent/production.bas` - Morale affects production
  - `Continent/Construction.bas` - Morale affects construction speed
  - `Continent/militaire.bas` - Morale affects combat power

- **Population Effects**: Population affects production, defense, etc.
  - `Continent/production.bas` - Population effects on production
  - `Continent/militaire.bas` - Population effects on defense
  - `Continent/cntSRV.frm` - Population calculations

### Weather System
- **Weather Types**: Different weather conditions
  - `Continent/evenements.bas` - Weather event types
  - `Continent/cntSRV.frm` - Weather management

- **Weather Effects**: Weather affects production, naval operations, fires
  - `Continent/evenements.bas` - Weather effects on various systems
  - `Continent/production.bas` - Weather effects on production
  - `Continent/militaire.bas` - Weather effects on naval operations

- **Seasonal Cycles**: Seasonal changes (winter, spring, etc.)
  - `Continent/evenements.bas` - Seasonal event generation
  - `Continent/cntSRV.frm` - Seasonal cycle management

- **Winter Effects**: Winter reduces certain activities
  - `Continent/evenements.bas` - Winter event effects
  - `Continent/production.bas` - Winter reduces production
  - `Continent/production.bas` - `processAbattageTask()` interrupted by winter

### Special Buildings
- **Castles**: Main player buildings
  - `Continent/CONSTRUCTIONS` table - Castle buildings
  - `Continent/Construction.bas` - Castle construction
  - `Continent/Fief.bas` - Castle management

- **Portals**: Teleportation portals
  - `Continent/CONSTRUCTIONS` table - Portal buildings
  - `Continent/militaire.bas` - Portal teleportation logic

- **Arenas**: Swag competition arenas
  - `Continent/CONSTRUCTIONS` table - Arena buildings
  - `Continent/swag.bas` - Arena requirements for swag

- **Palaces**: Required for heroes
  - `Continent/CONSTRUCTIONS` table - Palace buildings
  - `Continent/militaire.bas` - Palace requirements for heroes

- **Cathedrals**: Special religious buildings
  - `Continent/CONSTRUCTIONS` table - Cathedral buildings
  - `Continent/guildes.bas` - Cathedral effects on church guild
  - `Continent/cntSRV.frm` - Cathedral effects on guild levels

- **Halls**: Special gathering buildings
  - `Continent/CONSTRUCTIONS` table - Hall buildings
  - `Continent/guildes.bas` - Hall effects on commerce guild
  - `Continent/cntSRV.frm` - Hall effects on guild levels

### Resource Types
- **Food**: Basic food resource
  - `Continent/TYPE_DENREES` table - Food resource type
  - `Continent/INVENTAIRE` table - Food storage
  - `Continent/production.bas` - Food production

- **Wood**: Construction material
  - `Continent/TYPE_DENREES` table - Wood resource type
  - `Continent/INVENTAIRE` table - Wood storage
  - `Continent/production.bas` - Wood production (logging)

- **Stone**: Construction material
  - `Continent/TYPE_DENREES` table - Stone resource type
  - `Continent/INVENTAIRE` table - Stone storage
  - `Continent/production.bas` - Stone production (mining)

- **Metal**: Crafting material
  - `Continent/TYPE_DENREES` table - Metal resource type
  - `Continent/INVENTAIRE` table - Metal storage
  - `Continent/production.bas` - Metal production (mining)

- **Tools**: Required for most activities
  - `Continent/TYPE_DENREES` table - Tools resource type (denree=5)
  - `Continent/INVENTAIRE` table - Tools storage
  - `Continent/Construction.bas`, `Continent/production.bas` - Tool consumption

- **Medicine**: Disease treatment
  - `Continent/TYPE_DENREES` table - Medicine resource type (denree=10)
  - `Continent/INVENTAIRE` table - Medicine storage
  - `Continent/evenements.bas` - Medicine consumption for disease treatment

- **Animals**: Livestock resources
  - `Continent/TYPE_DENREES` table - Animal resource types
  - `Continent/INVENTAIRE` table - Animal storage
  - `Continent/production.bas` - Animal production and breeding

- **Special Items**: Artifacts and magical items
  - `Continent/guildes.bas` - Artifact management
  - `Continent/MARCHE_ARTEFACTS` table - Artifact market
  - `Continent/guildes.bas` - `getObjetValue()` calculates artifact values

---

## Technical Features

### Database
- **MySQL Database**: Primary database system
  - `Continent/mysql.bas` - MySQL connection management
  - `Continent/outils_serveur.bas` - `ServerConnect()` uses MySQL ODBC 5.1 Driver
  - `Continent/AccesBDD.bas` - Database access functions

- **ODBC Connection**: Database connectivity via ODBC
  - `Continent/outils_serveur.bas` - `ServerConnect()` establishes ODBC connection
  - `Continent/cntSRV.frm` - `mySql` connection object

- **SQL Execution**: Dynamic SQL query execution
  - `Continent/outils_serveur.bas` - `executeSQL()` executes queries
  - `Continent/AccesBDD.bas` - `BDD_ExecuteSQL()` function
  - `Continent/server_tools.bas` - `getVal()`, `setVal()` wrapper functions

- **Recordset Management**: ADO recordset handling
  - `Continent/AccesBDD.bas` - ADO recordset functions
  - `Continent/outils_serveur.bas` - Recordset management
  - `Continent/Fief.bas` - `LeRecordsetVillage` cached recordset

### Map Storage
- **Binary Map Files**: Map stored in binary format
  - `Continent/map/layer0.map` - Layer 0 (normalization base)
  - `Continent/map/layer1.map` - Layer 1 (terrain)
  - `Continent/carte.bas` - `Get`, `Put` statements for binary access
  - `Continent/carte.bas` - Binary file operations

- **Layer System**: Multiple map layers
  - `Continent/carte.bas` - Layer 1 (terrain), Layer 2 (objects/sprites), Layer 3 (territory)
  - `Continent/carte.bas` - `getMap()`, `updateMap()` work with layers
  - `Continent/map/` directory - Separate files per layer

- **Map Compression**: Efficient map data storage
  - `Continent/carte.bas` - Binary format for efficient storage
  - `Continent/map/` directory - Compressed map files

### Image Processing
- **GDI+ Integration**: Image manipulation using GDI+
  - `Continent/gdi/` directory - GDI+ wrapper classes
  - `Continent/gdi/GDIPlus.cls` - GDI+ main class
  - `Continent/gdi/Graphics.cls`, `Continent/gdi/Image.cls` - GDI+ classes
  - `Continent/gdi/GDIPlusWrapper.dll` - GDI+ wrapper DLL

- **Sprite Generation**: Automatic sprite generation
  - `Continent/militaire.bas` - `getTroupeSprite()` generates sprites
  - `Continent/militaire.bas` - Sprite calculation based on composition and nation

- **Unit Image Generation**: Dynamic unit image creation
  - `Continent/militaire.bas` - `generateTroupePic()` creates unit images
  - `Continent/gdi/` directory - GDI+ used for image generation
  - `Continent/pics/gentroupespics.bat` - Batch image generation script

- **FTP Support**: FTP library for file transfers
  - `Continent/ftplib/` directory - FTP client library
  - `Continent/ftplib/CFtpClient.cls` - FTP client class
  - `Continent/ftplib/CSocket.cls` - Socket support for FTP

---

## Notes

- This is a comprehensive list based on code analysis of the Continent project
- Some features may have dependencies or interactions not fully detailed here
- The Renaissance project is a refactoring, so implementation details may differ
- Some features may be simplified, enhanced, or removed in the refactoring process

