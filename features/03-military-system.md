# Military System

## Overview

The Military System enables players to form, train, and command military units. Units can move across the map, engage in combat, conduct sieges, and perform various military operations. The system includes unit formation, composition management, experience tracking, movement mechanics, combat resolution, and special features like portal teleportation.

## Feature List

1. [Army Formation](#army-formation)
2. [Unit Composition](#unit-composition)
3. [Unit Experience](#unit-experience)
4. [Unit Movement](#unit-movement)
5. [Unit Speed](#unit-speed)
6. [Unit Power](#unit-power)
7. [Unit Sprites](#unit-sprites)
8. [Combat](#combat)
9. [Siege](#siege)
10. [Assault](#assault)
11. [Raid](#raid)
12. [Garrison](#garrison)
13. [Protection](#protection)
14. [Escort](#escort)
15. [Naval Units](#naval-units)
16. [Naval Combat](#naval-combat)
17. [Naval Movement](#naval-movement)
18. [Naval Repair](#naval-repair)
19. [Ship Life](#ship-life)
20. [Ship Sinking](#ship-sinking)
21. [Portal Teleportation](#portal-teleportation)
22. [Portal Jump Requests](#portal-jump-requests)
23. [Portal Jump Authorization](#portal-jump-authorization)
24. [Distortion Travel](#distortion-travel)
25. [Travel](#travel)
26. [Exploration](#exploration)
27. [Battle Resolution](#battle-resolution)
28. [Defense Bonuses](#defense-bonuses)
29. [Combat Results](#combat-results)
30. [Casualties](#casualties)
31. [Battle Reports](#battle-reports)

---

## Army Formation

### Functional Description

Players can train and form military units by assembling different troop types. Unit formation is a task that progresses over time.

### Business Rules

- Unit formation requires resources and time
- Formation progress is tracked similar to construction
- Units are created when formation completes
- Formation requires specific resources (varies by unit type)
- Multiple units can be formed simultaneously
- Formation can be cancelled before completion

### Player Interactions

- Players initiate unit formation
- Players select unit composition
- Players provide required resources
- Players track formation progress
- Players receive completed units

### System Requirements

- System must track formation tasks
- System must validate resource requirements
- System must create units upon completion
- System must support multiple concurrent formations

### Dependencies

- **Resource System**: Provides formation materials
- **Population System**: May require population for units

### Data Model Requirements

- Formation task definitions
- Unit creation logic
- Resource requirement tracking

---

## Unit Composition

### Functional Description

Military units are composed of different troop types (infantry, cavalry, archers, etc.). Composition affects unit capabilities, speed, and combat power.

### Business Rules

- Units contain multiple troop types
- Composition is stored as structured data
- Composition affects unit speed (slowest unit determines speed)
- Composition affects combat power
- Composition can be modified (troops added/removed)
- Different compositions have different capabilities

### Player Interactions

- Players select composition when forming units
- Players can view unit composition
- Players may modify composition (if supported)

### System Requirements

- System must store unit composition data
- System must calculate unit properties from composition
- System must support composition modifications

### Dependencies

- **Unit Power**: Composition affects power calculations
- **Unit Speed**: Composition affects speed calculations

### Data Model Requirements

- Composition data structure
- Troop type definitions
- Composition-to-properties calculations

---

## Unit Experience

### Functional Description

Units gain experience from combat and various actions. Experience improves unit effectiveness and combat power.

### Business Rules

- Experience is gained from combat participation
- Experience is gained from travel and actions
- Experience increases unit combat power
- Experience is cumulative (does not decrease)
- Different actions provide different experience amounts
- Experience affects unit capabilities

### Player Interactions

- Players see unit experience levels
- Players benefit from experienced units automatically
- Players can prioritize experienced units for important missions

### System Requirements

- System must track experience per unit
- System must calculate experience gains
- System must apply experience bonuses to unit power

### Dependencies

- **Combat System**: Provides experience from battles
- **Unit Power**: Experience affects power calculations

### Data Model Requirements

- Experience tracking per unit
- Experience gain formulas
- Experience-to-power conversion

---

## Unit Movement

### Functional Description

Units can move across the map to different coordinates. Movement consumes movement points and follows pathfinding rules.

### Business Rules

- Units have movement points per turn
- Movement consumes points based on distance and terrain
- Units move along valid paths (pathfinding)
- Movement is limited by unit speed
- Units cannot move through obstacles or enemy territory (depending on rules)
- Movement progress is tracked per turn

### Player Interactions

- Players order units to move to coordinates
- Players see movement progress
- Players can cancel or redirect movement
- Players see unit positions on map

### System Requirements

- System must calculate movement paths
- System must track movement points
- System must update unit positions
- System must handle pathfinding

### Dependencies

- **Map System**: Provides terrain and pathfinding
- **Unit Speed**: Determines movement capability

### Data Model Requirements

- Movement point tracking
- Pathfinding data
- Position updates

---

## Unit Speed

### Functional Description

Unit movement speed is determined by composition and bonuses. Speed affects how far units can move per turn.

### Business Rules

- Speed is based on slowest unit type in composition
- Speed is modified by number of units (more units = slower)
- Navigation research bonuses increase speed
- Speed formula: base_speed + bonuses - penalties
- Speed determines maximum movement per turn

### Player Interactions

- Players see unit speed values
- Players can improve speed through research
- Players can optimize composition for speed

### System Requirements

- System must calculate speed from composition
- System must apply speed bonuses
- System must use speed for movement calculations

### Dependencies

- **Unit Composition**: Determines base speed
- **Research System**: Provides speed bonuses

### Data Model Requirements

- Speed calculation formulas
- Speed bonus tracking

---

## Unit Power

### Functional Description

Combat power represents unit effectiveness in battle. Power is calculated from composition, experience, and bonuses.

### Business Rules

- Power is calculated from unit composition
- Experience increases power
- Combat research bonuses increase power
- Power determines battle outcomes
- Power formula: base_power × experience_factor × bonuses
- Different unit types have different base power

### Player Interactions

- Players see unit power values
- Players can improve power through experience and research
- Players use power to plan military operations

### System Requirements

- System must calculate power from multiple factors
- System must apply power in combat calculations
- System must update power when factors change

### Dependencies

- **Unit Composition**: Determines base power
- **Unit Experience**: Affects power
- **Research System**: Provides power bonuses

### Data Model Requirements

- Power calculation formulas
- Power factor tracking

---

## Unit Sprites

### Functional Description

Units are visually represented on the map through sprites. Sprites indicate unit type, composition, and ownership.

### Business Rules

- Each unit has associated sprite(s)
- Sprites are generated based on composition
- Sprites may vary by nation/faction
- Sprites are placed on map obstacle layer
- Sprites update when units move or change

### Player Interactions

- Players see unit sprites on map
- Players can identify unit types visually
- Players can see unit ownership through sprites

### System Requirements

- System must generate sprites from composition
- System must place sprites on map
- System must update sprites when units change

### Dependencies

- **Map System**: Provides sprite placement
- **Unit Composition**: Determines sprite appearance

### Data Model Requirements

- Sprite generation logic
- Sprite-to-composition mappings

---

## Combat

### Functional Description

Units engage in combat when they encounter enemy units. Combat resolution determines casualties, experience gain, and battle outcomes.

### Business Rules

- Combat occurs when units meet on map
- Combat can be instant (doBattle) or extended (resolveBattle for skirmishes)
- Combat power determines outcomes
- Casualties are calculated based on power differences
- Experience is gained from combat
- Winners may capture resources or territory
- Combat can result in unit destruction

### Player Interactions

- Players initiate combat by moving units to enemy positions
- Players receive battle reports
- Players see combat results and casualties

### System Requirements

- System must detect unit encounters
- System must resolve combat calculations
- System must apply casualties and experience
- System must generate battle reports

### Dependencies

- **Unit Power**: Determines combat outcomes
- **Unit Experience**: Gains experience from combat
- **Message System**: Generates battle reports

### Data Model Requirements

- Combat resolution formulas
- Casualty calculation logic
- Battle outcome tracking

---

## Siege

### Functional Description

Units can besiege fortified positions (villages, castles). Sieges are extended operations that reduce defenses over time.

### Business Rules

- Sieges require units to remain at target location
- Sieges progress over multiple turns
- Siege effectiveness depends on attacker power vs defender strength
- Defenders may surrender or be defeated
- Successful sieges may capture territory
- Sieges may be broken by relief forces

### Player Interactions

- Players initiate sieges by positioning units
- Players track siege progress
- Players receive siege updates
- Players can break sieges with relief forces

### System Requirements

- System must track siege progress
- System must calculate siege effectiveness
- System must handle siege resolution
- System must support siege breaking

### Dependencies

- **Unit Power**: Affects siege effectiveness
- **Building System**: Fortifications affect defense
- **Territory System**: Sieges may capture territory

### Data Model Requirements

- Siege progress tracking
- Siege effectiveness calculations
- Siege resolution logic

---

## Assault

### Functional Description

Units can assault citadels (fortified strongholds). Assaults are direct attacks on heavily defended positions.

### Business Rules

- Assaults target citadels specifically
- Assaults are high-risk, high-reward operations
- Assault effectiveness depends on attacker power
- Successful assaults may capture citadels
- Assaults may result in heavy casualties

### Player Interactions

- Players initiate assaults on citadels
- Players receive assault results
- Players can capture citadels through successful assaults

### System Requirements

- System must support citadel targeting
- System must resolve assault calculations
- System must handle citadel capture

### Dependencies

- **Unit Power**: Affects assault effectiveness
- **Building System**: Citadels are special buildings

### Data Model Requirements

- Assault resolution logic
- Citadel capture mechanics

---

## Raid

### Functional Description

Units can conduct raids on enemy territory. Raids are quick attacks that may capture resources or cause damage.

### Business Rules

- Raids are fast operations
- Raids may capture resources
- Raids may damage enemy infrastructure
- Raids may be intercepted by defenders
- Raids have limited duration

### Player Interactions

- Players initiate raids on enemy positions
- Players receive raid results
- Players may gain resources from successful raids

### System Requirements

- System must support raid operations
- System must calculate raid effectiveness
- System must handle resource capture

### Dependencies

- **Unit Power**: Affects raid success
- **Resource System**: Raids may capture resources

### Data Model Requirements

- Raid operation definitions
- Raid effectiveness calculations

---

## Garrison

### Functional Description

Units can garrison in villages to provide defense. Garrisons protect villages from attacks and may provide other benefits.

### Business Rules

- Units can be assigned to garrison villages
- Garrisons provide defense bonuses
- Garrisons consume resources (maintenance)
- Garrisons can be attacked by enemies
- Garrisons may be required for vassal protection

### Player Interactions

- Players assign units to garrisons
- Players see garrison status
- Players can withdraw garrisons

### System Requirements

- System must track garrison assignments
- System must calculate defense bonuses
- System must handle garrison maintenance

### Dependencies

- **Defense Bonuses**: Garrisons provide defense
- **Vassal System**: May require garrisons

### Data Model Requirements

- Garrison assignment tracking
- Defense bonus calculations

---

## Protection

### Functional Description

Units can protect allied villages. Protection provides defense and may be required by diplomatic agreements.

### Business Rules

- Units can be assigned to protect allied villages
- Protection provides defense similar to garrisons
- Protection may be required by alliances
- Protection units can engage attackers

### Player Interactions

- Players assign units to protect allies
- Players see protection status
- Players can withdraw protection

### System Requirements

- System must track protection assignments
- System must provide defense benefits
- System must handle protection in combat

### Dependencies

- **Diplomacy System**: Protection may be required by alliances
- **Defense Bonuses**: Protection provides defense

### Data Model Requirements

- Protection assignment tracking

---

## Escort

### Functional Description

Units can escort convoys (trade caravans). Escorts protect convoys from attacks during travel.

### Business Rules

- Escorts accompany convoys during movement
- Escorts protect convoys from attacks
- Escorts can engage attackers
- Escorts may be required for safe trade

### Player Interactions

- Players assign units to escort convoys
- Players see escort status
- Players can withdraw escorts

### System Requirements

- System must track escort assignments
- System must handle escort in combat
- System must protect convoys during movement

### Dependencies

- **Trade System**: Escorts protect trade convoys
- **Combat System**: Escorts engage attackers

### Data Model Requirements

- Escort assignment tracking

---

## Naval Units

### Functional Description

Naval vessels function as military units. Ships can move on water, engage in combat, and perform naval operations.

### Business Rules

- Naval units are identified by composition range (4000-5999)
- Ships can only move on water tiles
- Ships have different capabilities than land units
- Ships can engage in naval combat
- Ships require maintenance and can degrade

### Player Interactions

- Players create naval units through boat construction
- Players command ships like land units
- Players see ships on water tiles

### System Requirements

- System must identify naval units
- System must restrict movement to water
- System must support naval-specific mechanics

### Dependencies

- **Naval Construction**: Creates naval units
- **Map System**: Provides water tile detection

### Data Model Requirements

- Naval unit identification
- Water movement validation

---

## Naval Combat

### Functional Description

Naval units engage in combat on water. Naval combat follows similar mechanics to land combat but with naval-specific factors.

### Business Rules

- Naval combat occurs between ships on water
- Combat resolution similar to land combat
- Ship condition affects combat effectiveness
- Naval combat may result in ship sinking
- Experience is gained from naval combat

### Player Interactions

- Players engage in naval combat
- Players receive naval battle reports
- Players see ship condition after combat

### System Requirements

- System must support naval combat resolution
- System must handle ship condition in combat
- System must generate naval battle reports

### Dependencies

- **Combat System**: Uses combat mechanics
- **Ship Life**: Condition affects combat

### Data Model Requirements

- Naval combat resolution logic

---

## Naval Movement

### Functional Description

Ships move across water tiles. Naval movement is restricted to water and may be affected by weather.

### Business Rules

- Ships can only move on water tiles
- Naval movement speed may differ from land movement
- Weather may affect naval movement
- Ships follow pathfinding on water
- Ships cannot move on land

### Player Interactions

- Players order ships to move
- Players see ship movement on water
- Players receive weather warnings

### System Requirements

- System must validate water-only movement
- System must handle naval pathfinding
- System must apply weather effects

### Dependencies

- **Map System**: Provides water tile detection
- **Weather System**: Affects naval movement

### Data Model Requirements

- Water movement validation
- Naval pathfinding logic

---

## Naval Repair

### Functional Description

Ships can be repaired when damaged. Repairs restore ship condition and prevent sinking.

### Business Rules

- Ship repair requires resources (similar to building repair)
- Repairs restore ship condition
- Repairs can be performed at docks
- Repairs prevent ship sinking
- Repairs consume tools and materials

### Player Interactions

- Players initiate ship repairs
- Players provide repair resources
- Players see repair progress

### System Requirements

- System must support ship repair tasks
- System must consume repair resources
- System must restore ship condition

### Dependencies

- **Ship Life**: Tracks ship condition
- **Resource System**: Provides repair materials

### Data Model Requirements

- Ship repair task tracking
- Repair resource requirements

---

## Ship Life

### Functional Description

Ships have durability/condition that degrades over time. Poor condition can lead to sinking.

### Business Rules

- Ships have condition value (similar to building state)
- Condition degrades over time
- Condition degrades from combat damage
- Low condition increases sinking risk
- Condition can be restored through repairs

### Player Interactions

- Players see ship condition
- Players receive warnings for low condition
- Players can repair ships to restore condition

### System Requirements

- System must track ship condition
- System must calculate degradation
- System must trigger sinking at low condition

### Dependencies

- **Naval Repair**: Restores condition
- **Ship Sinking**: Triggered by low condition

### Data Model Requirements

- Ship condition tracking
- Degradation formulas

---

## Ship Sinking

### Functional Description

Ships can sink if not maintained or from combat damage. Sinking results in unit loss.

### Business Rules

- Ships sink when condition reaches critical level
- Sinking results in unit destruction
- Sinking may cause resource loss
- Sinking can occur from poor maintenance or combat
- Sinking generates event messages

### Player Interactions

- Players receive sinking notifications
- Players lose ships from sinking
- Players can prevent sinking through maintenance

### System Requirements

- System must detect sinking conditions
- System must destroy sinking ships
- System must generate sinking events

### Dependencies

- **Ship Life**: Condition determines sinking risk
- **Event System**: Generates sinking events

### Data Model Requirements

- Sinking detection logic
- Sinking consequence handling

---

## Portal Teleportation

### Functional Description

Units can teleport through portals to distant locations. Teleportation has risks and may fail.

### Business Rules

- Portals allow instant travel between locations
- Teleportation has success/failure rates
- Failed teleportation may have consequences (unit loss, damage)
- Portals may require authorization
- Teleportation consumes movement points or resources

### Player Interactions

- Players order units to teleport through portals
- Players see teleportation results
- Players may lose units from failed teleportation

### System Requirements

- System must support portal teleportation
- System must calculate success rates
- System must handle teleportation failures
- System must update unit positions

### Dependencies

- **Building System**: Portals are special buildings
- **Map System**: Provides portal locations

### Data Model Requirements

- Portal teleportation logic
- Success rate calculations
- Failure consequence handling

---

## Portal Jump Requests

### Functional Description

Players can request permission to use portals owned by other players. Portal owners can authorize or refuse requests.

### Business Rules

- Portal jumps require permission from portal owner
- Players send jump requests
- Portal owners receive requests
- Owners can authorize or refuse
- Refused requests prevent teleportation

### Player Interactions

- Players send portal jump requests
- Portal owners receive and respond to requests
- Players see authorization status

### System Requirements

- System must support request/response mechanism
- System must track authorization status
- System must enforce authorization requirements

### Dependencies

- **Portal Teleportation**: Requires authorization
- **Message System**: Handles requests

### Data Model Requirements

- Portal request tracking
- Authorization status management

---

## Portal Jump Authorization

### Functional Description

Portal owners can authorize or refuse portal jump requests from other players. Authorization controls portal access.

### Business Rules

- Portal owners receive jump requests
- Owners can authorize or refuse
- Authorization is required before teleportation
- Refused requests prevent teleportation
- Authorization may be automatic or manual

### Player Interactions

- Portal owners see jump requests
- Owners authorize or refuse requests
- Requesters see authorization status

### System Requirements

- System must support authorization decisions
- System must enforce authorization requirements
- System must notify both parties of decisions

### Dependencies

- **Portal Jump Requests**: Receives requests
- **Portal Teleportation**: Enforces authorization

### Data Model Requirements

- Authorization decision tracking
- Authorization enforcement logic

---

## Distortion Travel

### Functional Description

Teleportation system with variable success rates. Distortion travel allows rapid movement with risk of failure.

### Business Rules

- Distortion travel has random success rates
- Success rate may vary by factors (research, portal type)
- Failed teleportation has consequences
- Consequences may include unit loss or damage
- Distortion travel is faster than normal movement

### Player Interactions

- Players initiate distortion travel
- Players see travel results
- Players may lose units from failures

### System Requirements

- System must calculate success rates
- System must handle failures
- System must apply consequences

### Dependencies

- **Portal Teleportation**: Uses teleportation mechanics
- **Research System**: May affect success rates

### Data Model Requirements

- Success rate calculations
- Failure consequence handling

---

## Travel

### Functional Description

Units travel to specific coordinates over time. Travel is standard movement across the map.

### Business Rules

- Units move toward destination coordinates
- Travel progress is tracked per turn
- Travel consumes movement points
- Travel follows pathfinding
- Units arrive when reaching destination

### Player Interactions

- Players order units to travel to coordinates
- Players see travel progress
- Players receive arrival notifications

### System Requirements

- System must track travel destinations
- System must calculate travel progress
- System must handle arrival

### Dependencies

- **Unit Movement**: Uses movement mechanics
- **Pathfinding**: Determines travel paths

### Data Model Requirements

- Travel destination tracking
- Travel progress calculations

---

## Exploration

### Functional Description

Units can explore special locations on the map. Exploration may reveal treasures, trigger events, or encounter monsters.

### Business Rules

- Units can explore special locations
- Exploration may reveal rewards (treasures, resources)
- Exploration may trigger events
- Exploration may encounter monsters (combat)
- Exploration may provide experience
- Locations may be explored multiple times (with cooldowns)

### Player Interactions

- Players order units to explore locations
- Players receive exploration results
- Players gain rewards from exploration

### System Requirements

- System must support location exploration
- System must generate exploration results
- System must handle exploration rewards

### Dependencies

- **Exploration System**: Provides location mechanics
- **Combat System**: May trigger combat
- **Event System**: May trigger events

### Data Model Requirements

- Exploration result generation
- Location exploration tracking

---

## Battle Resolution

### Functional Description

Combat between units is resolved through battle calculations. Resolution determines casualties, experience, and outcomes.

### Business Rules

- Battle resolution calculates outcomes from unit power
- Casualties are proportional to power differences
- Experience is gained by survivors
- Winners may capture resources or territory
- Battle results are deterministic with random factors
- Extended battles (skirmishes) progress over multiple turns

### Player Interactions

- Players receive battle reports
- Players see casualties and outcomes
- Players gain experience from victories

### System Requirements

- System must resolve battle calculations
- System must apply casualties and experience
- System must generate battle reports

### Dependencies

- **Unit Power**: Determines outcomes
- **Casualties**: Calculates losses
- **Combat Results**: Tracks outcomes

### Data Model Requirements

- Battle resolution formulas
- Casualty calculation logic

---

## Defense Bonuses

### Functional Description

Villages and fortified positions provide defense bonuses in combat. Defenders receive advantages when attacked.

### Business Rules

- Villages provide defense bonuses
- Fortifications increase defense
- Garrisons provide additional defense
- Defense bonuses reduce attacker effectiveness
- Defense bonuses vary by fortification level

### Player Interactions

- Players benefit from defense bonuses automatically
- Players can improve defense through fortifications
- Players see defense values

### System Requirements

- System must calculate defense bonuses
- System must apply bonuses in combat
- System must track fortification levels

### Dependencies

- **Building System**: Fortifications provide defense
- **Garrison**: Provides defense
- **Combat System**: Applies defense bonuses

### Data Model Requirements

- Defense bonus calculations
- Fortification level tracking

---

## Combat Results

### Functional Description

Combat outcomes are tracked including victory/defeat, casualties, and consequences. Results affect unit experience and player reputation.

### Business Rules

- Combat results determine victory or defeat
- Results affect unit experience gain
- Results may affect player reputation
- Results determine resource capture
- Results may affect territory control

### Player Interactions

- Players see combat results
- Players receive battle reports
- Players gain/lose based on results

### System Requirements

- System must determine combat outcomes
- System must track results
- System must apply consequences

### Dependencies

- **Battle Resolution**: Determines outcomes
- **Unit Experience**: Gains from results
- **Reputation System**: Affected by results

### Data Model Requirements

- Combat result tracking
- Result consequence application

---

## Casualties

### Functional Description

Units suffer losses in combat. Casualties reduce unit strength and may destroy units.

### Business Rules

- Casualties are calculated from combat power differences
- Casualties reduce unit composition
- Units may be destroyed if casualties exceed strength
- Casualty calculations include random factors
- Casualties affect both attackers and defenders

### Player Interactions

- Players see casualty reports
- Players lose units from casualties
- Players can reinforce units after combat

### System Requirements

- System must calculate casualties
- System must apply losses to units
- System must handle unit destruction

### Dependencies

- **Battle Resolution**: Calculates casualties
- **Unit Composition**: Affected by casualties

### Data Model Requirements

- Casualty calculation formulas
- Unit loss application logic

---

## Battle Reports

### Functional Description

Players receive detailed reports after battles. Reports include casualties, outcomes, experience gained, and other relevant information.

### Business Rules

- Battle reports are generated after combat
- Reports include detailed information
- Reports are sent to involved players
- Reports may include map links to battle locations
- Reports are stored in message system

### Player Interactions

- Players receive battle reports
- Players can review battle history
- Players see detailed combat information

### System Requirements

- System must generate battle reports
- System must format report information
- System must deliver reports to players

### Dependencies

- **Message System**: Delivers reports
- **Battle Resolution**: Provides report data

### Data Model Requirements

- Battle report generation
- Report data formatting

---

## Feature Interactions

### Internal Interactions

- **Unit Composition** affects **Unit Speed** and **Unit Power**
- **Unit Experience** increases **Unit Power**
- **Unit Power** determines **Combat** outcomes
- **Combat** provides **Unit Experience**
- **Unit Movement** enables **Combat** encounters
- **Garrison** provides **Defense Bonuses**

### External System Interactions

- **Construction System**: Creates naval units through boat building
- **Map System**: Provides terrain and pathfinding for movement
- **Research System**: Provides speed and power bonuses
- **Building System**: Provides fortifications and portals
- **Diplomacy System**: Affects combat permissions
- **Exploration System**: Units can explore locations
- **Event System**: Generates battle and sinking events
- **Message System**: Delivers battle reports
- **Territory System**: Combat may affect territory control

---

## Technical Considerations

### Performance Requirements

- System must efficiently process many unit movements per turn
- Combat resolution must be performant for concurrent battles
- Pathfinding must be fast for real-time movement planning
- Unit sprite rendering must support many units simultaneously

### Scalability Requirements

- System must support hundreds of units per player
- System must handle thousands of units across all players
- Combat processing must scale with player count
- Movement calculations must be efficient at scale

### Data Persistence

- Unit data must persist across game sessions
- Movement progress must be saved each turn
- Combat history may be needed for analytics
- Experience gains must be saved

### Real-time Requirements

- Unit movement planning should be immediate
- Combat resolution occurs per turn (not real-time)
- Movement progress updates occur per turn

### Validation Requirements

- All military actions must validate requirements before execution
- Movement must validate pathfinding and terrain
- Combat must validate unit availability
- Formation must validate resource requirements

