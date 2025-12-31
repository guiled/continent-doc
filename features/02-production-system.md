# Production System

## Overview

The Production System enables players to produce various resources through worker assignment, building utilization, and production tasks. The system includes multiple production types, worker management, capacity limits, bonuses, seasonal effects, and visual representation of workers on the map.

## Feature List

1. [Multiple Production Types](#multiple-production-types)
2. [Production Buildings](#production-buildings)
3. [Worker Assignment](#worker-assignment)
4. [Production Capacity](#production-capacity)
5. [Production Bonuses](#production-bonuses)
6. [Production Efficiency](#production-efficiency)
7. [Farming](#farming)
8. [Mining](#mining)
9. [Logging](#logging)
10. [Hunting](#hunting)
11. [Fishing](#fishing)
12. [Livestock](#livestock)
13. [Crafting](#crafting)
14. [Gathering](#gathering)
15. [Material Consumption](#material-consumption)
16. [Tool Consumption](#tool-consumption)
17. [Seasonal Effects](#seasonal-effects)
18. [Reproduction Rates](#reproduction-rates)
19. [Capacity Limits](#capacity-limits)
20. [Spring Bonus](#spring-bonus)
21. [Random Factors](#random-factors)
22. [Worker Placement on Map](#worker-placement-on-map)
23. [Forestry Workers](#forestry-workers)
24. [Fishermen](#fishermen)
25. [Farmers](#farmers)
26. [Miners](#miners)
27. [Blacksmiths](#blacksmiths)
28. [Deep Sea Fishing](#deep-sea-fishing)
29. [Slaughtering](#slaughtering)
30. [Tree Planting](#tree-planting)

---

## Multiple Production Types

### Functional Description

The system supports production of various resource types including food, wood, stone, metal, tools, and other commodities. Each production type has specific requirements, mechanics, and outputs.

### Business Rules

- Each production type produces specific resource(s)
- Production occurs over time through production tasks
- Production output is calculated per turn
- Different production types have different mechanics
- Production can be continuous or one-time tasks
- Multiple production types can run simultaneously

### Player Interactions

- Players select production types to initiate
- Players assign workers to production tasks
- Players receive produced resources in inventory
- Players can view production progress and output

### System Requirements

- System must support multiple production type definitions
- System must calculate production output per type
- System must handle concurrent production tasks
- System must track production history

### Dependencies

- **Inventory System**: Stores produced resources
- **Building System**: Requires production buildings
- **Population System**: Requires workers

### Data Model Requirements

- Production type definitions
- Production task tracking
- Resource output tracking

---

## Production Buildings

### Functional Description

Production requires specific buildings (farms, mines, forges, etc.) to be present. Each production type is associated with required building types.

### Business Rules

- Each production type requires specific building types
- Production capacity depends on number of available buildings
- Buildings must be functional (not collapsed) to support production
- Multiple buildings of same type increase production capacity
- Building destruction reduces or eliminates production capacity
- Production tasks automatically adjust when buildings are lost

### Player Interactions

- Players must construct required buildings before production
- Players see building requirements when selecting production
- Players receive notifications when buildings are lost
- Players can prioritize building construction for production

### System Requirements

- System must validate building availability for production
- System must calculate capacity based on building count
- System must handle building loss during production
- System must adjust production when buildings change

### Dependencies

- **Construction System**: Provides production buildings
- **Building System**: Tracks building state and availability

### Data Model Requirements

- Building-to-production type associations
- Building requirement definitions
- Building availability tracking

---

## Worker Assignment

### Functional Description

Players assign workers (peons) to production tasks. The number of workers affects production output and efficiency.

### Business Rules

- Workers are assigned per production task
- Minimum workers required per task
- Maximum workers limited by building capacity
- Workers are consumed/occupied during production
- Workers cannot be assigned to multiple tasks simultaneously
- Worker assignment affects production output linearly (more workers = more output)

### Player Interactions

- Players assign workers when creating production tasks
- Players can adjust worker assignments
- Players see worker requirements and limits
- Players receive warnings for insufficient workers

### System Requirements

- System must track worker assignments per task
- System must validate worker availability
- System must enforce worker limits
- System must calculate production based on worker count

### Dependencies

- **Population System**: Provides available workers
- **Building System**: Determines worker capacity limits

### Data Model Requirements

- Worker assignment tracking
- Worker availability calculation
- Production task-worker associations

---

## Production Capacity

### Functional Description

Maximum workers per production is limited by the number of available production buildings. Capacity determines how many workers can be assigned to a production task.

### Business Rules

- Capacity = (Number of buildings) × (Workers per building)
- Capacity is calculated dynamically based on available buildings
- Capacity can decrease if buildings are destroyed
- Production tasks automatically adjust when capacity decreases
- Different production types may have different capacity formulas

### Player Interactions

- Players see capacity limits when assigning workers
- Players receive notifications when capacity changes
- Players can plan building construction to increase capacity

### System Requirements

- System must calculate capacity per production type
- System must enforce capacity limits
- System must handle capacity changes dynamically
- System must adjust existing tasks when capacity changes

### Dependencies

- **Building System**: Provides building count
- **Production Buildings**: Defines capacity per building

### Data Model Requirements

- Capacity calculation formulas
- Building count tracking
- Capacity limit enforcement

---

## Production Bonuses

### Functional Description

Production output is modified by various bonuses including research (sciences), regional modifiers, and morale. Bonuses can increase or decrease production efficiency.

### Business Rules

- Bonuses are multiplicative factors applied to base production
- Research bonuses come from completed sciences
- Regional modifiers may affect certain production types
- Morale affects production (higher morale = better production)
- Bonuses stack multiplicatively
- Different production types may have different bonus sources

### Player Interactions

- Players benefit from bonuses automatically
- Players can invest in research to improve bonuses
- Players can improve morale to boost production

### System Requirements

- System must calculate bonus values from multiple sources
- System must apply bonuses to production calculations
- System must support different bonus types per production
- System must handle bonus changes dynamically

### Dependencies

- **Research System**: Provides science bonuses
- **Morale System**: Provides morale bonuses
- **Regional System**: Provides regional modifiers

### Data Model Requirements

- Bonus calculation formulas
- Bonus source tracking
- Production bonus application logic

---

## Production Efficiency

### Functional Description

Production efficiency is affected by morale, tool availability, and various bonuses. Efficiency determines the actual output compared to theoretical maximum.

### Business Rules

- Efficiency = Base Production × Morale Factor × Tool Factor × Bonuses
- Morale affects production: (1 + morale/200) multiplier
- Tool availability affects production (insufficient tools reduce output)
- Bonuses from research and other sources multiply efficiency
- Efficiency can vary between 0% and well over 100% (with bonuses)
- Efficiency is calculated per turn

### Player Interactions

- Players see efficiency factors affecting production
- Players can improve efficiency through morale and research
- Players must maintain tool supply for optimal efficiency

### System Requirements

- System must calculate efficiency factors
- System must apply efficiency to production output
- System must handle efficiency changes dynamically

### Dependencies

- **Morale System**: Provides morale factor
- **Resource System**: Provides tool availability
- **Production Bonuses**: Provides bonus factors

### Data Model Requirements

- Efficiency calculation formulas
- Efficiency factor tracking

---

## Farming

### Functional Description

Farming produces food through crop cultivation. Farmers work in fields and production may vary seasonally.

### Business Rules

- Farming requires farm buildings
- Farmers are visually represented on map near farms
- Production may be affected by seasons
- Farming produces food resources
- Multiple farms increase farming capacity

### Player Interactions

- Players create farming production tasks
- Players assign workers to farms
- Players see farmers working in fields on map

### System Requirements

- System must support farming production type
- System must place farmer sprites on map
- System must handle seasonal variations

### Dependencies

- **Production System**: Core production mechanics
- **Seasonal System**: Provides seasonal effects
- **Map System**: Places worker sprites

### Data Model Requirements

- Farming production definitions
- Farmer sprite placement

---

## Mining

### Functional Description

Mining extracts stone and metal from mines. Miners work at mine sites with visual effects (smoke).

### Business Rules

- Mining requires mine buildings
- Mining produces stone or metal resources
- Miners are visually represented at mines
- Mining may have visual effects (smoke)
- Different mines produce different resources

### Player Interactions

- Players create mining production tasks
- Players assign workers to mines
- Players see miners and smoke effects on map

### System Requirements

- System must support mining production type
- System must place miner sprites on map
- System must support visual effects

### Dependencies

- **Production System**: Core production mechanics
- **Map System**: Places worker sprites and effects

### Data Model Requirements

- Mining production definitions
- Miner sprite and effect placement

---

## Logging

### Functional Description

Logging produces wood through forest management. Loggers work in forest areas.

### Business Rules

- Logging requires appropriate buildings or forest access
- Logging produces wood resources
- Loggers are visually represented in forest areas
- Logging may affect forest density over time

### Player Interactions

- Players create logging production tasks
- Players assign workers to logging
- Players see loggers working in forests

### System Requirements

- System must support logging production type
- System must place logger sprites on map
- System must handle forest management

### Dependencies

- **Production System**: Core production mechanics
- **Map System**: Places worker sprites
- **Forest System**: Manages forest resources

### Data Model Requirements

- Logging production definitions
- Logger sprite placement

---

## Hunting

### Functional Description

Hunting produces food through wildlife hunting. Hunters work in wilderness areas.

### Business Rules

- Hunting produces food resources
- Hunting may not require specific buildings
- Hunting efficiency may vary by area
- Hunting may affect wildlife populations

### Player Interactions

- Players create hunting production tasks
- Players assign workers to hunting
- Players receive food from hunting

### System Requirements

- System must support hunting production type
- System must calculate hunting output

### Dependencies

- **Production System**: Core production mechanics

### Data Model Requirements

- Hunting production definitions

---

## Fishing

### Functional Description

Fishing produces food through aquatic resource harvesting. Fishermen work at docks or water bodies.

### Business Rules

- Fishing requires docks or water access
- Fishing produces food resources
- Fishing is affected by seasons (better in some seasons)
- Fishermen are visually represented at docks
- Fishing may be more productive in certain seasons

### Player Interactions

- Players create fishing production tasks
- Players assign workers to fishing
- Players see fishermen at docks on map

### System Requirements

- System must support fishing production type
- System must place fisherman sprites on map
- System must handle seasonal effects

### Dependencies

- **Production System**: Core production mechanics
- **Seasonal System**: Provides seasonal effects
- **Map System**: Places worker sprites

### Data Model Requirements

- Fishing production definitions
- Fisherman sprite placement
- Seasonal modifier definitions

---

## Livestock

### Functional Description

Livestock production involves animal breeding (cattle, horses, pigeons). Animals reproduce based on existing herd size.

### Business Rules

- Livestock production depends on existing animal population
- Reproduction rate is limited by herd size
- Production is capped at percentage of existing herd (e.g., 20% max)
- Reproduction includes random factors
- Spring season may increase reproduction
- Animals require appropriate buildings (stables, enclosures)

### Player Interactions

- Players create livestock production tasks
- Players assign workers to animal care
- Players receive new animals from breeding

### System Requirements

- System must track animal populations
- System must calculate reproduction rates
- System must apply capacity limits
- System must handle seasonal bonuses

### Dependencies

- **Production System**: Core production mechanics
- **Seasonal System**: Provides spring bonus
- **Inventory System**: Tracks animal resources

### Data Model Requirements

- Livestock production definitions
- Animal population tracking
- Reproduction rate formulas

---

## Crafting

### Functional Description

Crafting produces tools and weapons through skilled labor. Blacksmiths work at forges.

### Business Rules

- Crafting requires forge buildings
- Crafting produces tools or weapons
- Crafting may consume raw materials (metal)
- Blacksmiths are visually represented at forges
- Crafting requires specific skills or buildings

### Player Interactions

- Players create crafting production tasks
- Players assign workers to forges
- Players provide raw materials for crafting
- Players see blacksmiths working at forges

### System Requirements

- System must support crafting production type
- System must handle material consumption
- System must place blacksmith sprites on map

### Dependencies

- **Production System**: Core production mechanics
- **Material Consumption**: Consumes raw materials
- **Map System**: Places worker sprites

### Data Model Requirements

- Crafting production definitions
- Material requirement definitions
- Blacksmith sprite placement

---

## Gathering

### Functional Description

Gathering produces food through collection of natural resources. Gatherers work in various terrain types.

### Business Rules

- Gathering produces food resources
- Gathering is affected by seasons (winter reduces gathering)
- Gathering may not require specific buildings
- Gatherers are visually represented on map

### Player Interactions

- Players create gathering production tasks
- Players assign workers to gathering
- Players see gatherers on map

### System Requirements

- System must support gathering production type
- System must handle seasonal effects
- System must place gatherer sprites on map

### Dependencies

- **Production System**: Core production mechanics
- **Seasonal System**: Provides seasonal effects
- **Map System**: Places worker sprites

### Data Model Requirements

- Gathering production definitions
- Seasonal modifier definitions

---

## Material Consumption

### Functional Description

Some production types consume raw materials to produce finished goods. Materials are taken from inventory during production.

### Business Rules

- Certain productions require input materials
- Materials are consumed during production
- Material consumption rate may vary
- Insufficient materials may reduce or stop production
- Material requirements are defined per production type

### Player Interactions

- Players must provide required materials
- Players see material requirements when creating tasks
- Players receive warnings for insufficient materials

### System Requirements

- System must track material requirements per production
- System must consume materials during production
- System must validate material availability
- System must handle material shortages

### Dependencies

- **Inventory System**: Provides material storage
- **Resource System**: Defines material types

### Data Model Requirements

- Material requirement definitions
- Material consumption tracking

---

## Tool Consumption

### Functional Description

Production tasks consume tools during operation. Tool availability affects production efficiency.

### Business Rules

- Tools are consumed during production
- Tool consumption rate depends on worker count
- Insufficient tools reduce production output
- Tool consumption is calculated per turn
- Different production types may have different tool consumption rates

### Player Interactions

- Players must maintain tool supply
- Players see tool consumption rates
- Players receive warnings for tool shortages

### System Requirements

- System must calculate tool consumption
- System must consume tools during production
- System must handle tool shortages
- System must reduce production when tools are insufficient

### Dependencies

- **Inventory System**: Provides tool storage
- **Resource System**: Defines tools

### Data Model Requirements

- Tool consumption formulas
- Tool consumption tracking

---

## Seasonal Effects

### Functional Description

Production output is affected by seasons. Winter typically reduces certain production types, while spring may boost others.

### Business Rules

- Seasons affect production output
- Winter reduces most production types
- Spring may increase animal reproduction
- Seasonal effects are applied as multipliers
- Different production types have different seasonal sensitivities

### Player Interactions

- Players see seasonal effects on production
- Players can plan production around seasons
- Players receive notifications about seasonal changes

### System Requirements

- System must track current season
- System must apply seasonal modifiers to production
- System must handle season transitions

### Dependencies

- **Event System**: Provides seasonal events
- **Seasonal System**: Tracks current season

### Data Model Requirements

- Seasonal modifier definitions per production type
- Season tracking

---

## Reproduction Rates

### Functional Description

Animal production (livestock) is based on existing herd size. Reproduction rates determine how many new animals are produced.

### Business Rules

- Reproduction rate depends on existing animal population
- Maximum reproduction is limited (e.g., 20% of herd)
- Reproduction includes random variation
- Reproduction rate formula: 0.5 × min(1, herd_size / reproduction_threshold)
- Production is capped at herd_size / 5

### Player Interactions

- Players see reproduction rates
- Players can increase herd size to improve production
- Players receive animals based on reproduction

### System Requirements

- System must calculate reproduction rates
- System must apply reproduction limits
- System must handle random variation

### Dependencies

- **Livestock**: Animal production mechanics
- **Inventory System**: Tracks animal populations

### Data Model Requirements

- Reproduction rate formulas
- Animal population tracking

---

## Capacity Limits

### Functional Description

Production is limited by building capacity. Stables and enclosures have maximum animal capacity that limits livestock production.

### Business Rules

- Buildings have maximum capacity for animals
- Production cannot exceed building capacity
- Capacity is calculated based on building count
- Different building types have different capacities

### Player Interactions

- Players see capacity limits
- Players can construct more buildings to increase capacity

### System Requirements

- System must track building capacity
- System must enforce capacity limits
- System must calculate total capacity

### Dependencies

- **Building System**: Provides building capacity data

### Data Model Requirements

- Building capacity definitions
- Capacity limit enforcement

---

## Spring Bonus

### Functional Description

Animal reproduction receives a bonus during spring season, increasing production rates.

### Business Rules

- Spring season increases animal reproduction
- Bonus is applied to reproduction calculations
- Bonus may vary by animal type

### Player Interactions

- Players benefit from spring bonus automatically
- Players can plan breeding around spring

### System Requirements

- System must detect spring season
- System must apply spring bonus to reproduction

### Dependencies

- **Seasonal System**: Provides season information
- **Reproduction Rates**: Applies bonus to reproduction

### Data Model Requirements

- Spring bonus definitions

---

## Random Factors

### Functional Description

Production includes random variation to add unpredictability. Random factors affect final output.

### Business Rules

- Production output includes random variation
- Random factor: 0.75 × base + (0.35 × random × base)
- Random variation adds 0-35% additional output
- Different production types may have different random ranges

### Player Interactions

- Players see variable production output
- Players cannot predict exact output

### System Requirements

- System must apply random factors to production
- System must use appropriate random number generation

### Dependencies

- **Production System**: Applies to production calculations

### Data Model Requirements

- Random factor formulas

---

## Worker Placement on Map

### Functional Description

Workers are visually represented on the map through sprites. Different worker types have different visual representations.

### Business Rules

- Workers appear as sprites on map obstacle layer
- Sprites are placed near production buildings
- Sprites update when workers are assigned/removed
- Different production types have different worker sprites

### Player Interactions

- Players see workers on map
- Players can identify production activity visually

### System Requirements

- System must place worker sprites on map
- System must update sprites when assignments change
- System must support different sprite types

### Dependencies

- **Map System**: Provides sprite placement
- **Production System**: Provides worker assignment data

### Data Model Requirements

- Worker sprite definitions
- Sprite placement logic

---

## Forestry Workers

### Functional Description

Foresters plant trees as part of forest management. They work to maintain and expand forests.

### Business Rules

- Foresters plant trees on map
- Tree planting is part of forest management
- Foresters are visually represented on map
- Tree planting may be automatic or task-based

### Player Interactions

- Players see foresters planting trees
- Players benefit from forest regeneration

### System Requirements

- System must support tree planting
- System must place forester sprites on map

### Dependencies

- **Map System**: Places trees and sprites
- **Forest System**: Manages forest resources

### Data Model Requirements

- Forester sprite definitions
- Tree planting logic

---

## Fishermen

### Functional Description

Fishermen work at docks to produce food. They are visually represented at water-adjacent locations.

### Business Rules

- Fishermen appear at docks or water bodies
- Fishermen produce food through fishing
- Fishermen sprites are placed on map

### Player Interactions

- Players see fishermen at docks
- Players can identify fishing activity

### System Requirements

- System must place fisherman sprites at docks
- System must support dock locations

### Dependencies

- **Map System**: Places sprites
- **Fishing**: Fishing production mechanics

### Data Model Requirements

- Fisherman sprite definitions
- Dock location tracking

---

## Farmers

### Functional Description

Farmers work in fields to produce food. They are visually represented near farm buildings.

### Business Rules

- Farmers appear in fields near farms
- Farmers produce food through farming
- Farmer sprites are placed on map

### Player Interactions

- Players see farmers working in fields
- Players can identify farming activity

### System Requirements

- System must place farmer sprites in fields
- System must support field locations

### Dependencies

- **Map System**: Places sprites
- **Farming**: Farming production mechanics

### Data Model Requirements

- Farmer sprite definitions
- Field location tracking

---

## Miners

### Functional Description

Miners work at mines to extract stone and metal. They may have visual effects like smoke.

### Business Rules

- Miners appear at mine locations
- Miners produce stone or metal
- Miners may have visual effects (smoke)
- Miner sprites are placed on map

### Player Interactions

- Players see miners at mines
- Players see smoke effects from mining
- Players can identify mining activity

### System Requirements

- System must place miner sprites at mines
- System must support visual effects

### Dependencies

- **Map System**: Places sprites and effects
- **Mining**: Mining production mechanics

### Data Model Requirements

- Miner sprite definitions
- Visual effect definitions

---

## Blacksmiths

### Functional Description

Blacksmiths work at forges to craft tools and weapons. They are visually represented at forge buildings.

### Business Rules

- Blacksmiths appear at forges
- Blacksmiths produce tools or weapons
- Blacksmith sprites are placed on map

### Player Interactions

- Players see blacksmiths at forges
- Players can identify crafting activity

### System Requirements

- System must place blacksmith sprites at forges
- System must support forge locations

### Dependencies

- **Map System**: Places sprites
- **Crafting**: Crafting production mechanics

### Data Model Requirements

- Blacksmith sprite definitions
- Forge location tracking

---

## Deep Sea Fishing

### Functional Description

Extended fishing campaigns using naval vessels. Produces larger quantities of food through maritime operations.

### Business Rules

- Deep sea fishing requires naval vessels
- Fishing campaigns last multiple turns
- Production results vary based on conditions
- Naval vessels must be available and operational

### Player Interactions

- Players initiate deep sea fishing campaigns
- Players assign naval vessels to fishing
- Players receive fishing results after campaigns

### System Requirements

- System must support naval fishing campaigns
- System must track campaign progress
- System must calculate fishing results

### Dependencies

- **Naval System**: Provides naval vessels
- **Fishing**: Fishing production mechanics

### Data Model Requirements

- Deep sea fishing campaign definitions
- Campaign progress tracking

---

## Slaughtering

### Functional Description

Automatic weekly slaughtering of animals converts livestock to food. Provides regular food production from animal herds.

### Business Rules

- Slaughtering occurs automatically on schedule (weekly)
- Slaughtering converts animals to food
- Slaughtering rate may be configurable
- Slaughtering may be affected by winter (interrupted)

### Player Interactions

- Players receive food from automatic slaughtering
- Players may configure slaughtering rates

### System Requirements

- System must schedule automatic slaughtering
- System must convert animals to food
- System must handle seasonal interruptions

### Dependencies

- **Livestock**: Animal resources
- **Inventory System**: Converts animals to food

### Data Model Requirements

- Slaughtering schedule definitions
- Slaughtering rate formulas

---

## Tree Planting

### Functional Description

Forest management includes tree planting to maintain and expand forests. Foresters plant trees as part of their work.

### Business Rules

- Trees are planted by foresters
- Tree planting maintains forest resources
- Tree planting may be automatic or task-based
- Tree planting affects map obstacle layer

### Player Interactions

- Players see trees being planted
- Players benefit from forest regeneration

### System Requirements

- System must support tree planting
- System must update map with new trees
- System must manage forest resources

### Dependencies

- **Map System**: Places trees on map
- **Forest System**: Manages forest resources

### Data Model Requirements

- Tree planting logic
- Forest resource tracking

---

## Feature Interactions

### Internal Interactions

- **Worker Assignment** affects **Production Capacity** limits
- **Production Bonuses** modify **Production Efficiency**
- **Tool Consumption** affects **Production Efficiency**
- **Seasonal Effects** modify all production types
- **Material Consumption** is required for some **Crafting** productions

### External System Interactions

- **Construction System**: Provides production buildings
- **Population System**: Provides workers (peons)
- **Inventory System**: Stores produced resources and consumes materials
- **Research System**: Provides production bonuses
- **Morale System**: Affects production efficiency
- **Event System**: Provides seasonal events
- **Map System**: Places worker sprites and visual effects
- **Naval System**: Provides vessels for deep sea fishing

---

## Technical Considerations

### Performance Requirements

- System must efficiently process many production tasks per turn
- Production calculations must be performant for all players
- Worker sprite placement must be efficient
- Capacity calculations must be fast

### Scalability Requirements

- System must support hundreds of production tasks per player
- System must handle thousands of tasks across all players
- Production processing must scale with player count
- Worker sprite management must be efficient at scale

### Data Persistence

- Production task data must persist across game sessions
- Production progress must be saved each turn
- Production history may be needed for analytics

### Real-time Requirements

- Production output is calculated per turn (not real-time)
- Worker assignment changes take effect next turn
- Production bonuses update when research completes

### Validation Requirements

- All production actions must validate requirements before execution
- Worker assignments must respect capacity limits
- Resource availability must be checked before consumption
- Building availability must be validated for production

