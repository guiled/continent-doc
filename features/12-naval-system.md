---
layout: default
title: Naval System
parent: Features
nav_order: 12
---

# Naval System

## Overview

The Naval System manages maritime operations including ship construction, naval movement, naval combat, ship maintenance, and deep sea fishing. Ships function as military units with special water-only movement and combat mechanics. The system includes ship durability, sinking mechanics, weather effects, and naval bonuses.

## Feature List

1. [Deep Sea Fishing](#deep-sea-fishing)
2. [Naval Travel](#naval-travel)
3. [Naval Combat](#naval-combat)
4. [Ship Maintenance](#ship-maintenance)
5. [Ship Durability](#ship-durability)
6. [Weather Effects](#weather-effects)
7. [Ship Sinking](#ship-sinking)
8. [Naval Experience](#naval-experience)
9. [Fishing Results](#fishing-results)
10. [Naval Bonuses](#naval-bonuses)

---

## Deep Sea Fishing

### Functional Description

Extended fishing campaigns using naval vessels. Produces larger quantities of food through maritime operations.

### Business Rules

- Deep sea fishing requires naval vessels
- Fishing campaigns last multiple turns
- Production results vary based on conditions
- Naval vessels must be available and operational
- Fishing is handled by action type 'peche-%'

### Player Interactions

- Players initiate deep sea fishing campaigns
- Players assign naval vessels to fishing
- Players receive fishing results after campaigns

### System Requirements

- System must support naval fishing campaigns
- System must track campaign progress
- System must calculate fishing results

### Dependencies

- **Naval Construction**: Provides naval vessels
- **Production System**: Fishing produces food
- **Military System**: Vessels are military units

### Data Model Requirements

- Deep sea fishing campaign definitions
- Campaign progress tracking
- Fishing result calculations

---

## Naval Travel

### Functional Description

Ship movement across water tiles. Naval travel is restricted to water and may be affected by weather.

### Business Rules

- Ships can only move on water tiles
- Naval movement uses navigation actions
- Movement is handled by processArmeeTask()
- Movement may be affected by weather
- Ships follow pathfinding on water

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
- **Military System**: Ships are military units

### Data Model Requirements

- Water movement validation
- Naval pathfinding logic

---

## Naval Combat

### Functional Description

Naval battle system for ship-to-ship combat. Naval combat follows similar mechanics to land combat but with naval-specific factors.

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
- **Military System**: Ships are military units

### Data Model Requirements

- Naval combat resolution logic
- Ship condition in combat calculations

---

## Ship Maintenance

### Functional Description

Ship repair and maintenance system. Repairs restore ship condition and prevent sinking.

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
- **Construction System**: Ship repair mechanics

### Data Model Requirements

- Ship repair task tracking
- Repair resource requirements

---

## Ship Durability

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
- **Military System**: Ships are units

### Data Model Requirements

- Ship condition tracking
- Degradation formulas

---

## Weather Effects

### Functional Description

Weather affects naval operations. Weather modifies movement speed and may cause damage.

### Business Rules

- Weather affects naval movement
- Weather may reduce movement speed
- Weather may cause ship damage
- Weather effects are temporary
- Weather varies by season

### Player Interactions

- Players see weather effects on ships
- Players adapt to weather conditions
- Players receive weather warnings

### System Requirements

- System must apply weather effects to naval operations
- System must modify movement for weather
- System must handle weather damage

### Dependencies

- **Weather System**: Provides weather
- **Naval Travel**: Weather affects movement

### Data Model Requirements

- Weather effect definitions
- Weather application logic

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
- **Military System**: Ships are units

### Data Model Requirements

- Sinking detection logic
- Sinking consequence handling

---

## Naval Experience

### Functional Description

Ships gain experience from naval operations. Experience improves ship effectiveness.

### Business Rules

- Ships gain experience from naval operations
- Experience increases ship combat power
- Experience improves ship capabilities
- Experience is tracked per ship
- Experience is cumulative

### Player Interactions

- Players see ship experience
- Players benefit from experienced ships
- Players prioritize experienced ships

### System Requirements

- System must track ship experience
- System must calculate experience gains
- System must apply experience bonuses

### Dependencies

- **Naval Combat**: Provides experience
- **Naval Operations**: Experience from operations
- **Military System**: Ships are units

### Data Model Requirements

- Ship experience tracking
- Experience gain calculations

---

## Fishing Results

### Functional Description

Variable fishing results based on conditions. Deep sea fishing produces variable amounts of food.

### Business Rules

- Fishing results vary based on conditions
- Results are calculated by PROD_ResultatPechehauturiere()
- Results depend on vessel condition
- Results depend on weather
- Results may include random factors

### Player Interactions

- Players see fishing results
- Players receive variable food amounts
- Players benefit from good conditions

### System Requirements

- System must calculate fishing results
- System must apply condition modifiers
- System must handle result variations

### Dependencies

- **Deep Sea Fishing**: Produces results
- **Production System**: Results are food production

### Data Model Requirements

- Fishing result calculation formulas
- Result variation logic

---

## Naval Bonuses

### Functional Description

Navigation bonuses affect naval operations. Research and other bonuses improve naval capabilities.

### Business Rules

- Navigation research bonuses affect naval speed
- Naval construction bonuses (NAVAL_ACC) affect ship building
- Bonuses are retrieved by getBonus()
- Bonuses improve naval operations
- Bonuses stack multiplicatively

### Player Interactions

- Players benefit from naval bonuses
- Players research navigation for bonuses
- Players see improved naval capabilities

### System Requirements

- System must apply naval bonuses
- System must calculate bonus effects
- System must support multiple bonus sources

### Dependencies

- **Research System**: Provides navigation bonuses
- **Naval Travel**: Bonuses affect movement
- **Naval Construction**: Bonuses affect building

### Data Model Requirements

- Naval bonus definitions
- Bonus application logic

---

## Feature Interactions

### Internal Interactions

- **Ship Durability** affects **Ship Sinking** risk
- **Ship Maintenance** restores **Ship Durability**
- **Naval Travel** enables **Naval Combat** encounters
- **Naval Combat** provides **Naval Experience**
- **Weather Effects** affect **Naval Travel** and **Ship Durability**

### External System Interactions

- **Construction System**: Creates naval vessels through boat building
- **Military System**: Ships are military units
- **Map System**: Provides water tiles for movement
- **Weather System**: Affects naval operations
- **Production System**: Deep sea fishing produces food
- **Research System**: Provides naval bonuses
- **Event System**: Generates sinking events

---

## Technical Considerations

### Performance Requirements

- Naval movement calculations must be efficient
- Ship condition updates must be performant
- Fishing result calculations must be fast

### Scalability Requirements

- System must support many ships
- Naval operations must scale with player count
- Ship tracking must be efficient

### Data Persistence

- Ship data must persist
- Ship condition must be saved
- Naval experience must persist

### Real-time Requirements

- Naval movement occurs per turn
- Ship condition degrades per turn
- Weather effects apply per turn

### Validation Requirements

- All naval actions must validate ship availability
- Movement must validate water tiles
- Combat must validate ship condition

