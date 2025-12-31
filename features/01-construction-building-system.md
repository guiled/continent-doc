---
layout: default
title: Construction & Building System
parent: Features
nav_order: 1
---

# Construction & Building System

## Overview

The Construction & Building System allows players to construct, maintain, and manage buildings on the game map. Buildings serve various purposes including production, defense, storage, and special functions. The system includes building construction, upgrades, maintenance, state management, and terrain modification capabilities.

## Feature List

1. [Building Construction](#building-construction)
2. [Building Upgrades](#building-upgrades)
3. [Construction Progress](#construction-progress)
4. [Construction Requirements](#construction-requirements)
5. [Building Placement](#building-placement)
6. [Building Sprites](#building-sprites)
7. [Building Repairs](#building-repairs)
8. [Building State](#building-state)
9. [Building Collapse](#building-collapse)
10. [Automatic Maintenance](#automatic-maintenance)
11. [Targeted Repairs](#targeted-repairs)
12. [Repair Costs](#repair-costs)
13. [Terrain Paving](#terrain-paving)
14. [Terrain Damage](#terrain-damage)
15. [Terrain Transformation](#terrain-transformation)
16. [Terrain Requirements](#terrain-requirements)
17. [Naval Construction](#naval-construction)

---

## Building Construction

### Functional Description

Players can construct various types of buildings including castles, farms, mines, forges, and other structures. Each building type serves specific functions in the game economy and military systems.

### Business Rules

- Buildings are constructed over time through construction tasks
- Construction requires workers (peons), tools, and materials
- Each building type has specific resource requirements
- Buildings occupy specific map coordinates with defined footprints
- Construction progress is tracked as a percentage (0-100%)
- Construction can be paused or cancelled
- Multiple buildings can be constructed simultaneously

### Player Interactions

- Players initiate construction by selecting a building type and location
- Players assign workers to construction tasks
- Players must provide required materials and tools
- Players can view construction progress
- Players can cancel ongoing construction

### System Requirements

- System must track construction tasks with progress indicators
- System must validate building placement (terrain compatibility, space availability)
- System must manage resource consumption during construction
- System must support building footprint calculations (multiple map tiles)
- System must handle concurrent construction tasks per player
- System must validate resource availability before construction starts

### Dependencies

- **Production System**: Requires tools and materials from production
- **Map System**: Requires map coordinate system and terrain validation
- **Population System**: Requires peons (workers) to be available
- **Inventory System**: Requires resource storage and management

### Data Model Requirements

- Building type definitions (name, requirements, footprint, function)
- Construction task tracking (progress, assigned workers, required resources)
- Building instances (type, position, state, owner)
- Resource consumption records
- Building footprint data (occupied map tiles)

---

## Building Upgrades

### Functional Description

Existing buildings can be upgraded to higher levels, improving their capabilities, capacity, or efficiency.

### Business Rules

- Upgrades follow the same construction process as new buildings
- Upgraded buildings retain their position and ownership
- Upgrade requirements may differ from initial construction
- Upgrades may change building appearance or capabilities
- Some buildings may have maximum upgrade levels

### Player Interactions

- Players select existing buildings to upgrade
- Players provide upgrade resources
- Players assign workers to upgrade tasks

### System Requirements

- System must track building levels
- System must validate upgrade eligibility
- System must handle upgrade-specific requirements
- System must update building capabilities after upgrade completion

### Dependencies

- **Building Construction**: Uses same construction mechanics
- **Building State**: Upgrades may affect building state

### Data Model Requirements

- Building level/upgrade tracking
- Upgrade requirement definitions per building type and level

---

## Construction Progress

### Functional Description

Construction tasks progress over time based on worker assignment, resource availability, and other factors. Progress is tracked as a percentage toward completion.

### Business Rules

- Progress advances each game turn based on:
  - Number of assigned workers
  - Availability of required tools
  - Building type and size
  - Morale and other bonuses
- Progress is cumulative (0% to 100%)
- Construction completes when progress reaches 100%
- Progress can be affected by resource shortages
- Minimum progress per turn is guaranteed if resources are available

### Player Interactions

- Players view construction progress in task lists
- Players receive notifications when construction completes
- Players can adjust worker assignments to affect progress speed

### System Requirements

- System must calculate progress increment per turn
- System must track progress percentage accurately
- System must handle progress calculation with variable factors
- System must trigger completion events at 100% progress

### Dependencies

- **Population System**: Worker availability affects progress
- **Resource System**: Tool availability affects progress
- **Morale System**: Village morale may affect construction speed

### Data Model Requirements

- Progress percentage storage (0-100)
- Progress calculation history
- Turn-based progress tracking

---

## Construction Requirements

### Functional Description

Each building type requires specific resources, tools, and workers to construct. Requirements vary by building type and may include materials, tools, and minimum worker counts.

### Business Rules

- Each building type defines:
  - Required materials (wood, stone, metal, etc.)
  - Required tools (quantity per turn)
  - Minimum and maximum workers
  - Total work cost (construction time)
- Resources must be available before construction starts
- Resources are consumed during construction
- Insufficient resources pause construction
- Some buildings may require specific terrain types

### Player Interactions

- Players see requirement lists when selecting buildings
- Players must gather required resources before starting
- Players receive warnings for insufficient resources
- Players can check resource availability before construction

### System Requirements

- System must validate resource availability
- System must track resource consumption during construction
- System must handle resource shortages gracefully
- System must support requirement definitions per building type

### Dependencies

- **Production System**: Provides required materials
- **Inventory System**: Manages resource storage
- **Resource Types**: Defines available resource types

### Data Model Requirements

- Building requirement definitions (materials, tools, workers)
- Resource requirement tracking per construction task
- Resource consumption logs

---

## Building Placement

### Functional Description

Buildings are placed on specific map coordinates with defined footprints. Placement must respect terrain constraints, spacing rules, and ownership boundaries.

### Business Rules

- Buildings occupy multiple map tiles (footprint)
- Placement must be on valid terrain for building type
- Buildings cannot overlap with existing structures
- Placement must respect minimum spacing rules
- Buildings must be within player's territory or controlled area
- Some buildings may have adjacency requirements
- Placement validation occurs before construction starts

### Player Interactions

- Players select map location for new buildings
- Players see building footprint preview
- Players receive feedback on placement validity
- Players can adjust placement before confirming

### System Requirements

- System must calculate building footprints
- System must validate terrain compatibility
- System must check for overlapping structures
- System must enforce spacing rules
- System must support hexagonal map coordinate system
- System must handle multi-tile building footprints

### Dependencies

- **Map System**: Requires map coordinate system and terrain data
- **Territory System**: Requires territory ownership validation
- **Building System**: Requires existing building data for overlap checks

### Data Model Requirements

- Building footprint definitions (tile patterns)
- Terrain compatibility rules per building type
- Placement validation rules
- Building position and footprint storage

---

## Building Sprites

### Functional Description

Buildings have visual representations (sprites) on the map that indicate their type, state, and ownership. Sprites provide visual feedback for building management.

### Business Rules

- Each building type has associated sprite(s)
- Sprites may vary by building level or state
- Sprites are placed on map obstacle layer
- Sprites update when buildings change state
- Sprites are removed when buildings are destroyed

### Player Interactions

- Players see building sprites on the map
- Players can identify building types visually
- Players can see building state through visual indicators

### System Requirements

- System must associate sprites with building types
- System must render sprites on map layer
- System must update sprites when buildings change
- System must support sprite variations (level, state)

### Dependencies

- **Map System**: Requires map rendering system
- **Building System**: Requires building type and state data

### Data Model Requirements

- Sprite definitions per building type
- Sprite-to-building associations
- Sprite rendering data

---

## Building Repairs

### Functional Description

Buildings can be repaired when damaged. Repairs restore building state and prevent collapse. Players can initiate targeted repairs or rely on automatic maintenance.

### Business Rules

- Repairs consume resources (tools, wood, stone)
- Repairs require workers
- Repairs restore building state toward maximum
- Repairs can be targeted (specific building) or automatic (all buildings)
- Repair progress is tracked similar to construction
- Repairs are more efficient than construction (faster progress)

### Player Interactions

- Players initiate repairs on damaged buildings
- Players assign workers to repair tasks
- Players provide repair resources
- Players can prioritize which buildings to repair

### System Requirements

- System must track building damage/state
- System must support repair task creation
- System must calculate repair resource requirements
- System must handle repair progress similar to construction

### Dependencies

- **Building State**: Requires state tracking system
- **Resource System**: Requires repair materials
- **Construction System**: Uses similar task mechanics

### Data Model Requirements

- Repair task tracking
- Repair resource requirements
- Building state before/after repair

---

## Building State

### Functional Description

Buildings have a state/condition value that represents their structural integrity. State degrades over time and affects building functionality.

### Business Rules

- Building state ranges from 0% to 100%
- State degrades naturally over time (wear and tear)
- Degradation rate varies by building type
- Enclosure buildings (walls) degrade differently than regular buildings
- State affects building efficiency and functionality
- State below certain thresholds may cause penalties
- State can be restored through repairs

### Player Interactions

- Players view building state in building information
- Players receive warnings for low state buildings
- Players can prioritize repairs based on state

### System Requirements

- System must track state percentage for each building
- System must calculate degradation per turn
- System must apply different degradation formulas per building type
- System must enforce state bounds (0-100%)
- System must trigger events at state thresholds

### Dependencies

- **Building System**: Core building data
- **Event System**: State threshold events

### Data Model Requirements

- Building state storage (percentage)
- Degradation formula definitions
- State history tracking

---

## Building Collapse

### Functional Description

Buildings can collapse if not maintained, causing population loss, reputation penalties, and building destruction.

### Business Rules

- Buildings collapse when state reaches 0% or below
- Collapse causes population deaths (peons in building area)
- Collapse reduces village reputation
- Collapse reduces village morale
- Collapse removes building from map
- Collapse generates event messages
- Number of deaths depends on building size/area
- Reputation and morale penalties scale with deaths

### Player Interactions

- Players receive collapse event notifications
- Players see population and reputation impacts
- Players can prevent collapses through maintenance

### System Requirements

- System must detect state reaching collapse threshold
- System must calculate collapse consequences
- System must remove collapsed buildings
- System must update population, reputation, and morale
- System must generate collapse event messages

### Dependencies

- **Building State**: Requires state tracking
- **Population System**: Affects population counts
- **Reputation System**: Affects village reputation
- **Morale System**: Affects village morale
- **Event System**: Generates collapse events

### Data Model Requirements

- Collapse detection logic
- Collapse consequence calculations
- Building removal procedures

---

## Automatic Maintenance

### Functional Description

A general maintenance system automatically maintains all buildings, preventing excessive degradation and collapse.

### Business Rules

- Automatic maintenance applies to all buildings each turn
- Maintenance slows degradation but doesn't prevent it entirely
- Maintenance may consume resources (tools)
- Maintenance effectiveness may vary
- Players can disable automatic maintenance (if implemented)
- Maintenance is less effective than targeted repairs

### Player Interactions

- Players benefit from automatic maintenance passively
- Players may need to supplement with targeted repairs

### System Requirements

- System must apply maintenance to all buildings
- System must calculate maintenance effects
- System must handle resource consumption for maintenance

### Dependencies

- **Building State**: Maintains building state
- **Resource System**: May consume maintenance resources

### Data Model Requirements

- Maintenance application logic
- Maintenance resource consumption tracking

---

## Targeted Repairs

### Functional Description

Players can initiate specific repair tasks for individual buildings, providing more effective restoration than automatic maintenance.

### Business Rules

- Targeted repairs are more effective than automatic maintenance
- Repairs require explicit player action
- Repairs consume resources (tools, wood, stone)
- Repairs require worker assignment
- Repairs progress similar to construction tasks
- Players can prioritize which buildings to repair

### Player Interactions

- Players select specific buildings to repair
- Players assign workers to repair tasks
- Players provide repair resources
- Players track repair progress

### System Requirements

- System must support repair task creation per building
- System must track repair progress
- System must handle repair resource consumption
- System must apply repair effects to building state

### Dependencies

- **Building State**: Restores building state
- **Construction System**: Uses similar task mechanics
- **Resource System**: Consumes repair materials

### Data Model Requirements

- Repair task definitions
- Repair progress tracking
- Repair resource requirements

---

## Repair Costs

### Functional Description

Repairs consume specific resources including tools, wood, and stone. Costs vary based on building type, size, and damage level.

### Business Rules

- Repairs consume tools (required for work)
- Repairs consume wood (construction material)
- Repairs consume stone (construction material)
- Resource consumption scales with repair scope
- Insufficient resources prevent or pause repairs
- Resource costs are calculated per repair task

### Player Interactions

- Players see repair cost estimates
- Players must provide required resources
- Players receive warnings for insufficient resources

### System Requirements

- System must calculate repair resource requirements
- System must validate resource availability
- System must consume resources during repairs
- System must handle resource shortages

### Dependencies

- **Resource System**: Provides repair materials
- **Inventory System**: Manages resource storage

### Data Model Requirements

- Repair cost formulas
- Resource consumption tracking

---

## Terrain Paving

### Functional Description

Players can convert terrain to paved surfaces, improving movement and potentially enabling certain constructions.

### Business Rules

- Paving converts terrain types to paved surfaces
- Paving requires tools and workers
- Paving affects map terrain layer
- Paved terrain may enable certain building types
- Paving may improve movement speed
- Paving is a terrain modification action

### Player Interactions

- Players select terrain areas to pave
- Players assign workers to paving tasks
- Players provide required tools
- Players see terrain changes on map

### System Requirements

- System must support terrain type conversion
- System must update map terrain layer
- System must validate paving requirements
- System must handle paving task progress

### Dependencies

- **Map System**: Requires terrain layer modification
- **Terrain Modification**: Uses terrain modification mechanics

### Data Model Requirements

- Terrain modification task tracking
- Terrain type conversion rules

---

## Terrain Damage

### Functional Description

Players can modify terrain by damaging it, such as filling swamps or water holes to create usable land.

### Business Rules

- Terrain damage converts problematic terrain (swamps, water holes) to usable land
- Damage requires tools and workers
- Damage is a terrain modification action
- Damage affects map terrain layer
- Some terrain types may be more difficult to modify

### Player Interactions

- Players select terrain to damage/modify
- Players assign workers to modification tasks
- Players provide required tools

### System Requirements

- System must support terrain type modification
- System must update map terrain layer
- System must validate modification requirements

### Dependencies

- **Map System**: Requires terrain layer modification
- **Terrain Modification**: Uses terrain modification mechanics

### Data Model Requirements

- Terrain modification task tracking
- Terrain modification rules

---

## Terrain Transformation

### Functional Description

Players can transform terrain types, converting marshes to land, water holes to land, or other terrain conversions.

### Business Rules

- Terrain transformation changes terrain types permanently
- Transformation requires tools and workers
- Transformation affects map terrain layer (layer 1)
- Different transformations have different requirements
- Transformation may enable new construction possibilities
- Transformation is irreversible (or requires reverse transformation)

### Player Interactions

- Players select terrain to transform
- Players choose transformation type
- Players assign workers to transformation tasks
- Players provide required tools

### System Requirements

- System must support terrain type transformations
- System must update map terrain layer
- System must validate transformation requirements
- System must handle transformation task progress

### Dependencies

- **Map System**: Requires terrain layer modification
- **Terrain Modification**: Uses terrain modification mechanics

### Data Model Requirements

- Terrain transformation definitions
- Transformation task tracking
- Terrain type conversion rules

---

## Terrain Requirements

### Functional Description

Terrain modifications require specific resources (tools) and workers to complete. Requirements vary by modification type.

### Business Rules

- Terrain modifications require tools
- Terrain modifications require workers (peons)
- Requirements vary by modification type
- Resources are consumed during modification
- Insufficient resources prevent or pause modifications

### Player Interactions

- Players see modification requirements
- Players must provide required resources
- Players assign workers to modification tasks

### System Requirements

- System must validate modification requirements
- System must track resource consumption
- System must handle resource shortages

### Dependencies

- **Resource System**: Provides required tools
- **Population System**: Provides workers

### Data Model Requirements

- Terrain modification requirement definitions
- Resource consumption tracking

---

## Naval Construction

### Functional Description

Players can construct naval vessels (boats) for maritime operations. Naval construction follows similar mechanics to building construction but results in mobile units.

### Business Rules

- Boat construction requires specific resources
- Boats are constructed at construction sites
- Completed boats are automatically placed on water tiles
- Boat construction sites are visually represented on map
- Boats become military units after construction
- Boat construction may require specific buildings (docks, shipyards)

### Player Interactions

- Players initiate boat construction
- Players provide construction resources
- Players assign workers to boat construction
- Players see construction progress
- Players receive completed boats on water tiles

### System Requirements

- System must support boat construction tasks
- System must find valid water tile placement
- System must create naval units from completed boats
- System must handle boat construction site visualization

### Dependencies

- **Construction System**: Uses construction mechanics
- **Military System**: Creates naval units
- **Map System**: Requires water tile detection

### Data Model Requirements

- Boat construction task definitions
- Naval unit creation from boats
- Water tile placement logic

---

## Feature Interactions

### Internal Interactions

- **Construction Progress** affects **Building Construction** completion
- **Building State** affects **Building Collapse** risk
- **Building Repairs** restore **Building State**
- **Construction Requirements** must be met for **Building Construction**
- **Building Placement** validates before **Building Construction** starts

### External System Interactions

- **Production System**: Provides construction materials and tools
- **Map System**: Provides terrain data and coordinate system
- **Population System**: Provides workers (peons) for construction
- **Inventory System**: Manages resource storage and consumption
- **Military System**: Naval construction creates military units
- **Event System**: Building collapse generates events
- **Reputation System**: Building collapse affects reputation
- **Morale System**: Building collapse affects morale

---

## Technical Considerations

### Performance Requirements

- System must efficiently handle multiple concurrent construction tasks
- Building state degradation calculations must be performant for all buildings
- Map validation must be fast for real-time placement feedback
- Sprite rendering must support many buildings simultaneously

### Scalability Requirements

- System must support hundreds of buildings per player
- System must handle thousands of buildings across all players
- Construction task processing must scale with player count
- Building state updates must be efficient at scale

### Data Persistence

- Building data must persist across game sessions
- Construction progress must be saved each turn
- Building state must be tracked over time
- Construction history may be needed for analytics

### Real-time Requirements

- Building placement validation should be immediate
- Construction progress updates occur per turn (not real-time)
- Building state degradation occurs per turn

### Validation Requirements

- All construction actions must validate requirements before execution
- Building placement must validate terrain and spacing
- Resource availability must be checked before consumption
- State changes must respect bounds and rules

