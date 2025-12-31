# Map & Territory Management

## Overview

The Map & Territory Management System provides the game world foundation. It includes a hexagonal grid-based map with multiple layers (terrain, obstacles, territory), coordinate systems, pathfinding, map updates, and seasonal effects. The system manages terrain types, obstacles, resource nodes, special locations, and dynamic map changes.

## Feature List

1. [Hexagonal Map](#hexagonal-map)
2. [Map Layers](#map-layers)
3. [Map Coordinates](#map-coordinates)
4. [Map Sprites](#map-sprites)
5. [Map Updates](#map-updates)
6. [Terrain Types](#terrain-types)
7. [Obstacles](#obstacles)
8. [Resource Nodes](#resource-nodes)
9. [Special Locations](#special-locations)
10. [Treasure Spawning](#treasure-spawning)
11. [Map Normalization](#map-normalization)
12. [Sprite Management](#sprite-management)
13. [Case Locking](#case-locking)
14. [Pathfinding](#pathfinding)
15. [Distance Calculation](#distance-calculation)
16. [Tree Growth](#tree-growth)
17. [Forest Regeneration](#forest-regeneration)
18. [Animal Spawning](#animal-spawning)
19. [Monster Spawning](#monster-spawning)
20. [Fire Propagation](#fire-propagation)
21. [Weather Effects on Map](#weather-effects-on-map)

---

## Hexagonal Map

### Functional Description

The game uses a hexagonal grid-based map system. Hexagonal coordinates enable efficient neighbor calculations and movement.

### Business Rules

- Map uses hexagonal grid
- Hexagonal coordinates enable 6-directional movement
- Map size is configurable (MAP_WIDTH parameter)
- Hexagonal offsets are calculated for neighbor access
- Map supports efficient spatial queries

### Player Interactions

- Players see hexagonal map
- Players move units on hexagonal grid
- Players interact with hexagonal tiles

### System Requirements

- System must support hexagonal coordinate system
- System must calculate hexagonal neighbors
- System must handle hexagonal movement
- System must support configurable map size

### Dependencies

- **Map Coordinates**: Hexagonal coordinates
- **Pathfinding**: Hexagonal pathfinding

### Data Model Requirements

- Hexagonal coordinate calculations
- Neighbor calculation logic
- Map size configuration

---

## Map Layers

### Functional Description

Map uses multiple layers for different data types. Layers include terrain, objects/sprites, and territory.

### Business Rules

- Layer 1: Terrain (ground types)
- Layer 2: Objects/sprites (buildings, units, obstacles)
- Layer 3: Territory (ownership)
- Layers are stored separately
- Layers can be queried independently

### Player Interactions

- Players see combined layer visualization
- Players interact with different layers
- Players see layer-specific information

### System Requirements

- System must support multiple layers
- System must store layers separately
- System must combine layers for display
- System must query layers efficiently

### Dependencies

- **Terrain Types**: Layer 1 data
- **Obstacles**: Layer 2 data
- **Territory System**: Layer 3 data

### Data Model Requirements

- Layer data structures
- Layer storage format
- Layer query mechanisms

---

## Map Coordinates

### Functional Description

X,Y coordinate system for map positions. Coordinates enable spatial calculations and pathfinding.

### Business Rules

- Coordinates use X,Y system
- Position conversion: pos = 1 + x + (y * MAP_WIDTH)
- Coordinates enable distance calculations
- Coordinates support pathfinding
- Coordinate system is consistent across layers

### Player Interactions

- Players see coordinates
- Players target coordinates
- Players move to coordinates

### System Requirements

- System must support X,Y coordinates
- System must convert between position formats
- System must validate coordinates
- System must handle coordinate calculations

### Dependencies

- **Pathfinding**: Uses coordinates
- **Distance Calculation**: Uses coordinates

### Data Model Requirements

- Coordinate data structures
- Position conversion logic

---

## Map Sprites

### Functional Description

Visual representation system with sprites. Sprites represent buildings, units, and other map elements.

### Business Rules

- Sprites are placed on layer 2
- Sprites represent visual elements
- Sprites update when objects change
- Sprites are removed when objects are destroyed
- Sprite system supports different sprite types

### Player Interactions

- Players see sprites on map
- Players identify objects through sprites
- Players see sprite updates

### System Requirements

- System must place sprites on map
- System must update sprites
- System must remove sprites
- System must support sprite types

### Dependencies

- **Building System**: Building sprites
- **Military System**: Unit sprites
- **Map Layers**: Sprites on layer 2

### Data Model Requirements

- Sprite definitions
- Sprite placement logic

---

## Map Updates

### Functional Description

Dynamic map updates during turn resolution. Map changes are applied each turn.

### Business Rules

- Map updates occur each turn
- Updates include terrain changes, sprite changes
- Updates are applied during normalization
- Updates reflect game state changes
- Updates are synchronized

### Player Interactions

- Players see map updates
- Players see changes reflected on map

### System Requirements

- System must update map each turn
- System must apply changes efficiently
- System must synchronize updates

### Dependencies

- **Map Normalization**: Performs updates
- **All Systems**: Changes affect map

### Data Model Requirements

- Map update logic
- Update synchronization

---

## Terrain Types

### Functional Description

Various terrain types (land, water, mountains, etc.). Terrain affects movement and construction.

### Business Rules

- Multiple terrain types exist
- Terrain types affect movement
- Terrain types affect construction
- Terrain validation: getMap(1, pos) > 19 for land
- Terrain is stored on layer 1

### Player Interactions

- Players see terrain types
- Players consider terrain for actions
- Players see terrain restrictions

### System Requirements

- System must support terrain types
- System must validate terrain
- System must apply terrain effects

### Dependencies

- **Map Layers**: Terrain on layer 1
- **Movement System**: Terrain affects movement

### Data Model Requirements

- Terrain type definitions
- Terrain validation logic

---

## Obstacles

### Functional Description

Obstacles on map (trees, buildings, etc.). Obstacles block movement and affect pathfinding.

### Business Rules

- Obstacles are on layer 2
- Obstacles block movement
- Obstacles affect pathfinding
- Obstacles can be removed
- Obstacles include trees, buildings, etc.

### Player Interactions

- Players see obstacles
- Players navigate around obstacles
- Players remove obstacles (if possible)

### System Requirements

- System must track obstacles
- System must block movement through obstacles
- System must support obstacle removal

### Dependencies

- **Map Layers**: Obstacles on layer 2
- **Pathfinding**: Obstacles affect paths

### Data Model Requirements

- Obstacle definitions
- Obstacle blocking logic

---

## Resource Nodes

### Functional Description

Natural resources on map. Resource nodes provide access to specific resources.

### Business Rules

- Resource nodes are placed on map
- Nodes provide specific resources
- Nodes may be limited
- Nodes are tracked in MAP_SPECIAL table
- Nodes affect production

### Player Interactions

- Players see resource nodes
- Players access resources from nodes
- Players benefit from nodes

### System Requirements

- System must place resource nodes
- System must track node availability
- System must support node access

### Dependencies

- **Production System**: Uses resource nodes
- **Map System**: Nodes on map

### Data Model Requirements

- Resource node definitions
- Node placement logic

---

## Special Locations

### Functional Description

Special locations for exploration. Locations provide unique content and rewards.

### Business Rules

- Special locations are placed on map
- Locations can be explored
- Locations provide unique content
- Locations are tracked in LIEUX table
- Locations may recharge

### Player Interactions

- Players discover locations
- Players explore locations
- Players receive location rewards

### System Requirements

- System must place special locations
- System must track location data
- System must support location exploration

### Dependencies

- **Exploration System**: Explores locations
- **Map System**: Locations on map

### Data Model Requirements

- Location definitions
- Location data tracking

---

## Treasure Spawning

### Functional Description

Random treasure placement on map. Treasures provide rewards for discovery.

### Business Rules

- Treasures spawn randomly
- Treasure placement occurs during normalization
- Treasures provide rewards
- Treasures may be limited
- Treasure spawning is random

### Player Interactions

- Players discover treasures
- Players collect treasures
- Players receive treasure rewards

### System Requirements

- System must spawn treasures
- System must place treasures on map
- System must track treasure locations

### Dependencies

- **Map Normalization**: Spawns treasures
- **Exploration System**: Discovers treasures

### Data Model Requirements

- Treasure spawning logic
- Treasure placement algorithms

---

## Map Normalization

### Functional Description

Map cleanup and normalization each turn. Normalization updates map state and spawns dynamic elements.

### Business Rules

- Normalization occurs each turn
- Normalization removes workers, plants trees, spawns animals
- Normalization updates map state
- Normalization is called from server loop
- Normalization maintains map consistency

### Player Interactions

- Players see normalized map
- Players benefit from normalization

### System Requirements

- System must normalize map each turn
- System must perform normalization tasks
- System must maintain map consistency

### Dependencies

- **All Map Features**: Normalization affects all features

### Data Model Requirements

- Normalization logic
- Normalization task definitions

---

## Sprite Management

### Functional Description

Sprite placement and removal on map. Sprites are managed dynamically as objects change.

### Business Rules

- Sprites are placed when objects are created
- Sprites are removed when objects are destroyed
- Sprites update when objects change
- Sprite management is automatic
- Sprites are on layer 2

### Player Interactions

- Players see sprite changes
- Players see updated sprites

### System Requirements

- System must place sprites
- System must remove sprites
- System must update sprites
- System must manage sprite lifecycle

### Dependencies

- **Map Sprites**: Manages sprites
- **All Object Systems**: Objects have sprites

### Data Model Requirements

- Sprite lifecycle management
- Sprite update logic

---

## Case Locking

### Functional Description

Case locking for construction sites. Prevents conflicts during construction.

### Business Rules

- Construction sites lock map tiles
- Locked tiles use sprites 254 and 255
- Locked tiles prevent other actions
- Locks are released when construction completes
- Locks prevent tile conflicts

### Player Interactions

- Players see locked tiles
- Players cannot use locked tiles
- Players see construction progress

### System Requirements

- System must lock tiles during construction
- System must release locks on completion
- System must prevent actions on locked tiles

### Dependencies

- **Construction System**: Locks tiles
- **Map System**: Provides tile locking

### Data Model Requirements

- Tile locking logic
- Lock management

---

## Pathfinding

### Functional Description

Pathfinding for unit movement. Calculates paths avoiding obstacles and respecting terrain.

### Business Rules

- Pathfinding finds valid paths
- Pathfinding avoids obstacles
- Pathfinding respects terrain restrictions
- Pathfinding uses hexagonal movement
- Pathfinding is efficient

### Player Interactions

- Players see movement paths
- Players move units along paths
- Players see path restrictions

### System Requirements

- System must calculate paths
- System must avoid obstacles
- System must respect terrain
- System must be efficient

### Dependencies

- **Hexagonal Map**: Provides grid
- **Obstacles**: Affects paths
- **Terrain Types**: Affects paths

### Data Model Requirements

- Pathfinding algorithms
- Path calculation logic

---

## Distance Calculation

### Functional Description

Distance calculations between points. Used for movement, combat range, and other mechanics.

### Business Rules

- Distance uses Euclidean formula: Sqr((nx * nx) + (ny * ny))
- Distance calculations are efficient
- Distance affects movement time
- Distance affects combat range
- Distance is calculated on hexagonal grid

### Player Interactions

- Players see distances
- Players consider distances for actions

### System Requirements

- System must calculate distances efficiently
- System must support distance queries
- System must handle hexagonal distances

### Dependencies

- **Map Coordinates**: Provides coordinates
- **Movement System**: Uses distances

### Data Model Requirements

- Distance calculation formulas
- Distance query mechanisms

---

## Tree Growth

### Functional Description

Trees grow over time on map. Tree growth maintains forests and provides resources.

### Business Rules

- Trees grow during normalization
- Tree growth maintains forests
- Trees provide wood resources
- Tree growth is gradual
- Tree growth occurs on suitable terrain

### Player Interactions

- Players see tree growth
- Players benefit from forests
- Players harvest trees

### System Requirements

- System must grow trees
- System must place trees on map
- System must track tree growth

### Dependencies

- **Map Normalization**: Grows trees
- **Forest System**: Trees form forests

### Data Model Requirements

- Tree growth logic
- Tree placement algorithms

---

## Forest Regeneration

### Functional Description

Forest regeneration system maintains forest resources. Forests regrow over time.

### Business Rules

- Forests regenerate during normalization
- Regeneration maintains forest density
- Regeneration uses tree placement algorithms
- Regeneration occurs gradually
- Regeneration maintains resource availability

### Player Interactions

- Players see forest regeneration
- Players benefit from regeneration
- Players maintain forests

### System Requirements

- System must regenerate forests
- System must maintain forest density
- System must support regeneration algorithms

### Dependencies

- **Tree Growth**: Regenerates forests
- **Map Normalization**: Performs regeneration

### Data Model Requirements

- Forest regeneration algorithms
- Regeneration logic

---

## Animal Spawning

### Functional Description

Wild animals spawn on map. Animals provide hunting resources.

### Business Rules

- Animals spawn during normalization
- Spawning uses getCaseLibreSauvage() to find locations
- Animals spawn on suitable terrain
- Animal spawning maintains wildlife
- Animals provide hunting resources

### Player Interactions

- Players see animals
- Players hunt animals
- Players benefit from wildlife

### System Requirements

- System must spawn animals
- System must find spawn locations
- System must track animals

### Dependencies

- **Map Normalization**: Spawns animals
- **Hunting System**: Uses animals

### Data Model Requirements

- Animal spawning logic
- Spawn location finding

---

## Monster Spawning

### Functional Description

Monsters spawn on map. Monsters provide challenges and combat opportunities.

### Business Rules

- Monsters spawn from events
- Monsters are added by addMonstre()
- Monsters are placed on map
- Monsters move and attack
- Monsters provide combat challenges

### Player Interactions

- Players see monsters
- Players fight monsters
- Players see monster threats

### System Requirements

- System must spawn monsters
- System must place monsters on map
- System must track monsters

### Dependencies

- **Event System**: Spawns monsters
- **Monster System**: Provides monsters

### Data Model Requirements

- Monster spawning logic
- Monster placement algorithms

---

## Fire Propagation

### Functional Description

Forest fires spread across map. Fires damage forests and may affect structures.

### Business Rules

- Fires start in forests
- Fires spread to adjacent areas
- Fire propagation uses spread logic
- Fires are generated by generateIncendies()
- Fires are started by allumeIncendie()

### Player Interactions

- Players see fires
- Players try to extinguish fires
- Players see fire damage

### System Requirements

- System must generate fires
- System must spread fires
- System must handle fire damage

### Dependencies

- **Event System**: Generates fires
- **Forest System**: Fires affect forests

### Data Model Requirements

- Fire propagation algorithms
- Fire spread logic

---

## Weather Effects on Map

### Functional Description

Weather affects map elements. Weather modifies terrain, obstacles, and other map features.

### Business Rules

- Weather affects map during normalization
- Weather modifies terrain appearance
- Weather affects obstacle visibility
- Weather effects are temporary
- Weather varies by season

### Player Interactions

- Players see weather effects
- Players adapt to weather
- Players see weather changes

### System Requirements

- System must apply weather effects
- System must modify map for weather
- System must handle weather changes

### Dependencies

- **Weather System**: Provides weather
- **Map Normalization**: Applies effects

### Data Model Requirements

- Weather effect definitions
- Weather application logic

---

## Feature Interactions

### Internal Interactions

- **Hexagonal Map** provides foundation for **Map Layers**
- **Map Coordinates** enable **Pathfinding** and **Distance Calculation**
- **Map Normalization** performs **Tree Growth** and **Animal Spawning**
- **Terrain Types** affect **Pathfinding**
- **Obstacles** block **Pathfinding**

### External System Interactions

- **Construction System**: Places buildings on map
- **Military System**: Units move on map
- **Production System**: Workers placed on map
- **Exploration System**: Explores special locations
- **Event System**: Spawns monsters and fires
- **Territory System**: Tracks ownership on layer 3

---

## Technical Considerations

### Performance Requirements

- Map queries must be efficient
- Pathfinding must be fast
- Sprite rendering must be performant
- Map updates must be efficient

### Scalability Requirements

- System must support large maps
- Map processing must scale with size
- Sprite management must be efficient
- Pathfinding must handle many units

### Data Persistence

- Map data must persist
- Layer data must be saved
- Sprite positions must persist
- Map state must be saved

### Real-time Requirements

- Map updates occur per turn
- Sprite updates are immediate
- Pathfinding should be fast for planning

### Validation Requirements

- All map operations must validate coordinates
- Terrain validation must be consistent
- Obstacle placement must be validated
- Map updates must maintain consistency

