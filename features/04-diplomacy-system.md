---
layout: default
title: Diplomacy System
parent: Features
nav_order: 4
---

# Diplomacy System

## Overview

The Diplomacy System manages relations between nations and players. It includes diplomatic status tracking, alliance management, ambassador systems, pariah status, and non-aggression pacts. The system affects military actions, trade, and other player interactions.

## Feature List

1. [Nation Relations](#nation-relations)
2. [Player Relations](#player-relations)
3. [Diplomatic Status Matrix](#diplomatic-status-matrix)
4. [Alliance System](#alliance-system)
5. [Pact Effects](#pact-effects)
6. [Ambassadors](#ambassadors)
7. [Embassy Management](#embassy-management)
8. [Pariah Status](#pariah-status)
9. [Non-Aggression Pacts](#non-aggression-pacts)
10. [Diplomatic Override](#diplomatic-override)

---

## Nation Relations

### Functional Description

Nations have diplomatic status with each other: War, Hostile, Neutral, Peace, or Alliance. These relations affect player interactions and military permissions.

### Business Rules

- Relations are defined between all nation pairs
- Status levels: War < Hostile < Neutral < Peace < Alliance
- National relations provide base diplomatic status
- Relations can be changed through diplomatic actions
- Relations affect what actions players can take

### Player Interactions

- Players see nation relations
- Players are affected by their nation's relations
- Players may influence nation relations (if supported)

### System Requirements

- System must store relation matrix for all nations
- System must provide relation lookup
- System must support relation changes

### Dependencies

- **Nation System**: Defines nations
- **Player Relations**: National relations affect player relations

### Data Model Requirements

- Nation relation matrix storage
- Relation status definitions

---

## Player Relations

### Functional Description

Players/fiefs have diplomatic relations with each other. These relations are calculated from nation relations, alliances, and pacts.

### Business Rules

- Player relations are calculated from multiple factors
- Alliances override national relations
- Pacts affect player relations
- Relations determine combat permissions
- Relations affect trade and other interactions

### Player Interactions

- Players see relations with other players
- Players can form alliances to override relations
- Players are affected by relation status

### System Requirements

- System must calculate player relations dynamically
- System must consider all relation factors
- System must provide relation lookup

### Dependencies

- **Nation Relations**: Base relation source
- **Alliance System**: Overrides relations
- **Pact System**: Modifies relations

### Data Model Requirements

- Player relation calculation logic
- Relation factor tracking

---

## Diplomatic Status Matrix

### Functional Description

A matrix stores diplomatic relations between all nations. The matrix is initialized from database and used for efficient relation lookups.

### Business Rules

- Matrix contains relations for all nation pairs
- Matrix is symmetric (A->B = B->A, or directional if asymmetric)
- Matrix is initialized at server start
- Matrix can be updated during gameplay
- Matrix provides O(1) relation lookup

### Player Interactions

- Players benefit from matrix lookups (performance)
- Players see relation information derived from matrix

### System Requirements

- System must maintain relation matrix
- System must provide efficient matrix lookup
- System must update matrix when relations change

### Dependencies

- **Nation Relations**: Populates matrix

### Data Model Requirements

- Matrix data structure
- Matrix update logic

---

## Alliance System

### Functional Description

Players can form military alliances that override national diplomatic status. Alliances provide mutual protection and cooperation.

### Business Rules

- Alliances are formed between players
- Alliances override national relations (allies even if nations are enemies)
- Alliances provide mutual defense benefits
- Alliances may have requirements or costs
- Alliances can be broken

### Player Interactions

- Players form alliances with other players
- Players see alliance status
- Players benefit from alliance protection

### System Requirements

- System must track alliance relationships
- System must override relations for allies
- System must handle alliance formation and breaking

### Dependencies

- **Player Relations**: Alliances override relations
- **Military System**: Alliances affect combat permissions

### Data Model Requirements

- Alliance relationship tracking
- Alliance override logic

---

## Pact Effects

### Functional Description

Various pacts (pariah, non-aggression) affect diplomatic relations. Pacts modify how players interact with each other.

### Business Rules

- Pacts modify diplomatic relations
- Different pacts have different effects
- Pacts can be temporary or permanent
- Pacts may conflict with each other
- Pact effects are applied when calculating relations

### Player Interactions

- Players are affected by pact status
- Players may create or break pacts
- Players see pact effects on relations

### System Requirements

- System must track pact status
- System must apply pact effects to relations
- System must handle pact conflicts

### Dependencies

- **Pact System**: Provides pact definitions
- **Player Relations**: Pacts affect relations

### Data Model Requirements

- Pact status tracking
- Pact effect application logic

---

## Ambassadors

### Functional Description

Ambassador system allows players to send diplomatic representatives. Ambassadors affect relations and provide diplomatic benefits.

### Business Rules

- Players can send ambassadors to other players
- Ambassadors improve relations
- Ambassadors may provide information
- Ambassadors can be recalled
- Number of ambassadors may be limited

### Player Interactions

- Players send ambassadors
- Players receive ambassadors
- Players see ambassador counts
- Players can recall ambassadors

### System Requirements

- System must track ambassador assignments
- System must count ambassadors per player
- System must apply ambassador effects

### Dependencies

- **Player Relations**: Ambassadors affect relations

### Data Model Requirements

- Ambassador assignment tracking
- Ambassador counting logic

---

## Embassy Management

### Functional Description

Embassy system tracks friendly and enemy ambassadors. Embassy counts affect diplomatic status and benefits.

### Business Rules

- Embassies track ambassador counts
- Friendly ambassadors improve relations
- Enemy ambassadors may indicate hostility
- Embassy counts affect diplomatic calculations
- Embassies may provide bonuses

### Player Interactions

- Players see embassy counts
- Players benefit from friendly embassies
- Players may be concerned by enemy embassies

### System Requirements

- System must count ambassadors per embassy
- System must categorize ambassadors (friendly/enemy)
- System must apply embassy effects

### Dependencies

- **Ambassadors**: Provides ambassador data

### Data Model Requirements

- Embassy counting logic
- Ambassador categorization

---

## Pariah Status

### Functional Description

Players can be declared pariahs by nations. Pariah status affects relations with all players of that nation.

### Business Rules

- Nations can declare players as pariahs
- Pariah status affects relations with all nation members
- Pariah status may have penalties
- Pariah status can be removed
- Pariah status is stored as a pact (PDR)

### Player Interactions

- Players may be declared pariahs
- Players see pariah status
- Players suffer penalties from pariah status

### System Requirements

- System must track pariah status
- System must apply pariah effects to relations
- System must support pariah declaration and removal

### Dependencies

- **Pact System**: Pariah is a pact type
- **Player Relations**: Pariah affects relations

### Data Model Requirements

- Pariah status tracking
- Pariah effect application

---

## Non-Aggression Pacts

### Functional Description

Players can form non-aggression pacts (PNA) that prevent military actions between signatories.

### Business Rules

- Non-aggression pacts prevent attacks
- Pacts are mutual agreements
- Pacts may have duration
- Pacts can be broken (with consequences)
- Pacts override normal relations for aggression

### Player Interactions

- Players form non-aggression pacts
- Players cannot attack pact partners
- Players see pact status
- Players can break pacts

### System Requirements

- System must track non-aggression pacts
- System must enforce pact restrictions
- System must handle pact breaking

### Dependencies

- **Military System**: Pacts restrict military actions
- **Pact System**: PNA is a pact type

### Data Model Requirements

- Non-aggression pact tracking
- Pact enforcement logic

---

## Diplomatic Override

### Functional Description

Alliances override national diplomatic status. Player-to-player relations can override nation-to-nation relations.

### Business Rules

- Alliances take precedence over national relations
- Player relations are calculated: Alliance > Pact > Nation
- Overrides allow cooperation despite national hostility
- Overrides are checked first in relation calculations

### Player Interactions

- Players benefit from alliance overrides
- Players can cooperate with allies despite nation relations

### System Requirements

- System must check overrides first
- System must apply override hierarchy
- System must support multiple override types

### Dependencies

- **Alliance System**: Provides overrides
- **Player Relations**: Overrides affect relations

### Data Model Requirements

- Override hierarchy logic
- Override application order

---

## Feature Interactions

### Internal Interactions

- **Nation Relations** provide base for **Player Relations**
- **Alliance System** overrides **Nation Relations**
- **Pact Effects** modify **Player Relations**
- **Ambassadors** affect **Player Relations**
- **Diplomatic Override** applies **Alliance System** priority

### External System Interactions

- **Military System**: Relations affect combat permissions
- **Trade System**: Relations may affect trade
- **Pact System**: Provides pact definitions
- **Nation System**: Defines nations
- **Message System**: Diplomatic notifications

---

## Technical Considerations

### Performance Requirements

- Relation lookups must be fast (O(1) with matrix)
- Relation calculations must be efficient
- Ambassador counting must be performant

### Scalability Requirements

- System must support many nations and players
- Relation matrix must scale efficiently
- Ambassador tracking must handle many assignments

### Data Persistence

- Diplomatic relations must persist
- Alliance data must be saved
- Ambassador assignments must persist
- Pact status must be saved

### Real-time Requirements

- Relation lookups should be immediate
- Relation changes take effect immediately
- Alliance formation is immediate

### Validation Requirements

- All diplomatic actions must validate permissions
- Relation changes must be validated
- Alliance formation must validate requirements

