---
layout: default
title: Events & Random Events
parent: Features
nav_order: 9
---

# Events & Random Events

## Overview

The Events & Random Events System generates various random and scheduled events that affect gameplay. Events include diseases, monster attacks, revolts, weather effects, building collapses, fires, and role-playing events. Events add unpredictability and challenge to the game.

## Feature List

1. [Disease System](#disease-system)
2. [Disease Contagion](#disease-contagion)
3. [Disease Treatment](#disease-treatment)
4. [Disease Mortality](#disease-mortality)
5. [Disease Recovery](#disease-recovery)
6. [Monster Attacks](#monster-attacks)
7. [Monster Raids](#monster-raids)
8. [Monster Movement](#monster-movement)
9. [Monster Aggressiveness](#monster-aggressiveness)
10. [Monster Escarmouches](#monster-escarmouches)
11. [Revolt System](#revolt-system)
12. [Revolt Causes](#revolt-causes)
13. [Revolt Resolution](#revolt-resolution)
14. [Revolt Effects](#revolt-effects)
15. [Planned Revolts](#planned-revolts)
16. [Building Collapse](#building-collapse)
17. [Fires](#fires)
18. [Weather Effects](#weather-effects)
19. [RP Events](#rp-events)
20. [Scheduled Events](#scheduled-events)

---

## Disease System

### Functional Description

Epidemic system with multiple disease types that can affect populations. Diseases spread, cause mortality, and can be treated with medicine.

### Business Rules

- Multiple disease types exist
- Diseases are generated randomly
- Diseases affect population
- Diseases can spread between villages
- Diseases have different characteristics

### Player Interactions

- Players see disease outbreaks
- Players treat diseases with medicine
- Players see disease effects

### System Requirements

- System must generate diseases randomly
- System must track disease status
- System must handle disease progression

### Dependencies

- **Population System**: Diseases affect population
- **Disease Treatment**: Medicine treats diseases
- **Disease Contagion**: Diseases spread

### Data Model Requirements

- Disease type definitions
- Disease status tracking
- Disease generation logic

---

## Disease Contagion

### Functional Description

Diseases spread through population and between villages. Contagion parameters control spread rate.

### Business Rules

- Diseases spread through population
- Contagion rate varies by disease type
- Contagion parameters (MALADIE_CONTAGION_*) control spread
- Diseases can spread to nearby villages
- Contagion is calculated each turn

### Player Interactions

- Players see disease spread
- Players try to contain diseases
- Players see contagion warnings

### System Requirements

- System must calculate contagion
- System must spread diseases
- System must handle contagion parameters

### Dependencies

- **Disease System**: Diseases spread
- **Population System**: Contagion affects population

### Data Model Requirements

- Contagion calculation formulas
- Contagion parameter definitions

---

## Disease Treatment

### Functional Description

Medicine consumption treats diseases. Treatment reduces disease severity and mortality.

### Business Rules

- Medicine (denree=10) treats diseases
- Treatment reduces disease effects
- Treatment improves recovery rates
- Medicine is consumed during treatment
- Treatment effectiveness varies

### Player Interactions

- Players provide medicine for treatment
- Players see treatment effects
- Players benefit from treatment

### System Requirements

- System must consume medicine
- System must apply treatment effects
- System must handle treatment calculations

### Dependencies

- **Disease System**: Treatment affects diseases
- **Resource System**: Provides medicine
- **Disease Recovery**: Treatment improves recovery

### Data Model Requirements

- Treatment calculation logic
- Medicine consumption tracking

---

## Disease Mortality

### Functional Description

Diseases can kill population. Mortality depends on disease type and treatment availability.

### Business Rules

- Diseases cause population deaths
- Mortality is calculated each turn
- Mortality depends on disease severity
- Treatment reduces mortality
- Mortality affects population counts

### Player Interactions

- Players see population losses
- Players try to reduce mortality
- Players see mortality reports

### System Requirements

- System must calculate mortality
- System must reduce population
- System must handle mortality effects

### Dependencies

- **Disease System**: Diseases cause mortality
- **Population System**: Mortality affects population
- **Disease Treatment**: Treatment reduces mortality

### Data Model Requirements

- Mortality calculation formulas
- Population reduction logic

---

## Disease Recovery

### Functional Description

Natural and medical recovery from diseases. Recovery rates depend on treatment and disease type.

### Business Rules

- Diseases can be recovered from naturally
- Medical treatment improves recovery
- Recovery rates vary by disease (MALADIE_GUERISON_*)
- Recovery removes disease effects
- Recovery is calculated each turn

### Player Interactions

- Players see recovery progress
- Players benefit from treatment
- Players see disease clearance

### System Requirements

- System must calculate recovery
- System must remove diseases on recovery
- System must handle recovery rates

### Dependencies

- **Disease System**: Recovery removes diseases
- **Disease Treatment**: Treatment improves recovery

### Data Model Requirements

- Recovery calculation formulas
- Recovery rate definitions

---

## Monster Attacks

### Functional Description

Random monster attacks on villages. Monsters spawn and attack player settlements.

### Business Rules

- Monsters attack villages randomly
- Attacks can cause damage and losses
- Monsters are added to map
- Attacks occur periodically
- Attack strength varies

### Player Interactions

- Players defend against attacks
- Players see attack warnings
- Players engage monsters in combat

### System Requirements

- System must generate monster attacks
- System must spawn monsters on map
- System must handle attack resolution

### Dependencies

- **Monster System**: Provides monsters
- **Combat System**: Resolves attacks
- **Map System**: Places monsters

### Data Model Requirements

- Monster attack generation logic
- Attack strength calculations

---

## Monster Raids

### Functional Description

Monster raids with pillaging. Raids cause resource loss and damage.

### Business Rules

- Monsters conduct raids on villages
- Raids pillage resources
- Raids cause infrastructure damage
- Raids are more severe than attacks
- Raids can be defended against

### Player Interactions

- Players defend against raids
- Players lose resources from raids
- Players see raid damage

### System Requirements

- System must generate raids
- System must pillage resources
- System must cause damage

### Dependencies

- **Monster Attacks**: Raids are special attacks
- **Resource System**: Raids pillage resources

### Data Model Requirements

- Raid generation logic
- Pillaging calculations

---

## Monster Movement

### Functional Description

Monsters move across the map. Movement brings monsters to player territories.

### Business Rules

- Monsters move on map
- Movement brings monsters to villages
- Movement is tracked each turn
- Monsters may have movement patterns
- Movement updates monster positions

### Player Interactions

- Players see monster movement
- Players track monster positions
- Players prepare for monster arrival

### System Requirements

- System must move monsters
- System must update positions
- System must handle movement patterns

### Dependencies

- **Map System**: Provides movement space
- **Monster System**: Monsters move

### Data Model Requirements

- Monster movement logic
- Position update tracking

---

## Monster Aggressiveness

### Functional Description

Monster activity increases in winter. Seasonal effects affect monster behavior.

### Business Rules

- Winter increases monster activity
- Aggressiveness varies by season
- Seasonal effects affect attack frequency
- Monsters are more dangerous in winter
- Seasonal behavior is automatic

### Player Interactions

- Players see increased activity in winter
- Players prepare for winter monsters
- Players see seasonal warnings

### System Requirements

- System must apply seasonal effects
- System must increase activity in winter
- System must handle seasonal variations

### Dependencies

- **Seasonal System**: Provides season information
- **Monster Attacks**: Activity affects attacks

### Data Model Requirements

- Seasonal modifier definitions
- Aggressiveness calculation logic

---

## Monster Escarmouches

### Functional Description

Random skirmishes with monsters. Escarmouches are smaller encounters than full attacks.

### Business Rules

- Escarmouches are random skirmishes
- Skirmishes are smaller than attacks
- Combat resolution determines outcomes
- Escarmouches occur randomly
- Skirmishes may provide experience

### Player Interactions

- Players engage in skirmishes
- Players see skirmish results
- Players gain experience from skirmishes

### System Requirements

- System must generate skirmishes
- System must resolve combat
- System must handle skirmish outcomes

### Dependencies

- **Combat System**: Resolves skirmishes
- **Monster System**: Provides monsters

### Data Model Requirements

- Skirmish generation logic
- Skirmish resolution mechanics

---

## Revolt System

### Functional Description

Population revolts against players. Revolts reduce production and affect reputation.

### Business Rules

- Populations can revolt
- Revolts are triggered by various causes
- Revolts reduce production
- Revolts affect reputation
- Revolts can be resolved

### Player Interactions

- Players see revolts
- Players resolve revolts
- Players see revolt effects

### System Requirements

- System must trigger revolts
- System must handle revolt effects
- System must support revolt resolution

### Dependencies

- **Revolt Causes**: Triggers revolts
- **Revolt Resolution**: Resolves revolts
- **Production System**: Affected by revolts

### Data Model Requirements

- Revolt trigger logic
- Revolt effect definitions

---

## Revolt Causes

### Functional Description

Various causes trigger revolts. Causes include external influence, poor conditions, and other factors.

### Business Rules

- Multiple causes can trigger revolts
- External influence causes revolts
- Poor conditions increase revolt risk
- Causes are tracked and calculated
- Different causes have different effects

### Player Interactions

- Players see revolt causes
- Players try to prevent revolts
- Players address causes

### System Requirements

- System must track revolt causes
- System must calculate revolt risk
- System must trigger revolts from causes

### Dependencies

- **Political Influence**: Causes revolts
- **Revolt System**: Causes trigger revolts

### Data Model Requirements

- Revolt cause definitions
- Revolt risk calculations

---

## Revolt Resolution

### Functional Description

Revolts can be resolved diplomatically or by force. Resolution removes revolt effects.

### Business Rules

- Revolts can be resolved diplomatically
- Revolts can be resolved by force
- Resolution removes revolt effects
- Different resolution methods have different costs
- Resolution success depends on factors

### Player Interactions

- Players choose resolution method
- Players resolve revolts
- Players see resolution results

### System Requirements

- System must support resolution methods
- System must handle resolution
- System must remove revolt effects

### Dependencies

- **Revolt System**: Revolts are resolved
- **Diplomacy System**: Diplomatic resolution
- **Military System**: Force resolution

### Data Model Requirements

- Resolution method definitions
- Resolution logic

---

## Revolt Effects

### Functional Description

Revolts affect production and reputation. Effects persist until revolt is resolved.

### Business Rules

- Revolts reduce production
- Revolts reduce reputation
- Effects persist during revolt
- Effects are removed on resolution
- Effect severity varies

### Player Interactions

- Players see revolt effects
- Players suffer from effects
- Players resolve revolts to remove effects

### System Requirements

- System must apply revolt effects
- System must reduce production
- System must reduce reputation

### Dependencies

- **Production System**: Affected by revolts
- **Reputation System**: Affected by revolts
- **Revolt Resolution**: Removes effects

### Data Model Requirements

- Revolt effect definitions
- Effect application logic

---

## Planned Revolts

### Functional Description

Revolts can be planned by external influence. Planned revolts are triggered by political influence.

### Business Rules

- External influence can plan revolts
- Planned revolts occur at scheduled times
- Planning requires influence buildup
- Planned revolts are more severe
- Planning can be detected and prevented

### Player Interactions

- Players may detect planned revolts
- Players try to prevent planned revolts
- Players see planning warnings

### System Requirements

- System must support revolt planning
- System must schedule planned revolts
- System must handle planning detection

### Dependencies

- **Political Influence**: Plans revolts
- **Revolt System**: Planned revolts trigger

### Data Model Requirements

- Revolt planning logic
- Planning schedule tracking

---

## Building Collapse

### Functional Description

Buildings collapse if not maintained. Collapse causes population loss and reputation penalties.

### Business Rules

- Buildings collapse when state reaches 0%
- Collapse causes population deaths
- Collapse reduces reputation
- Collapse reduces morale
- Collapse removes buildings

### Player Interactions

- Players see building collapses
- Players suffer from collapse effects
- Players prevent collapses through maintenance

### System Requirements

- System must detect collapse conditions
- System must apply collapse effects
- System must remove collapsed buildings

### Dependencies

- **Building System**: Buildings collapse
- **Population System**: Affected by collapse
- **Reputation System**: Affected by collapse

### Data Model Requirements

- Collapse detection logic
- Collapse effect calculations

---

## Fires

### Functional Description

Forest fires that spread across the map. Fires damage forests and may affect nearby structures.

### Business Rules

- Fires start in forests
- Fires spread to adjacent areas
- Fires damage forests
- Fires may affect nearby buildings
- Fires can be extinguished

### Player Interactions

- Players see fires
- Players try to extinguish fires
- Players see fire damage

### System Requirements

- System must generate fires
- System must spread fires
- System must handle fire damage

### Dependencies

- **Map System**: Fires spread on map
- **Forest System**: Fires affect forests

### Data Model Requirements

- Fire generation logic
- Fire spread calculations

---

## Weather Effects

### Functional Description

Weather affects various game mechanics. Weather events modify production, naval operations, and other systems.

### Business Rules

- Weather events occur periodically
- Weather affects production
- Weather affects naval operations
- Weather affects fires
- Weather effects are temporary

### Player Interactions

- Players see weather events
- Players adapt to weather
- Players see weather effects

### System Requirements

- System must generate weather events
- System must apply weather effects
- System must handle weather changes

### Dependencies

- **Production System**: Affected by weather
- **Naval System**: Affected by weather
- **Seasonal System**: Weather varies by season

### Data Model Requirements

- Weather event definitions
- Weather effect calculations

---

## RP Events

### Functional Description

Role-playing events system provides narrative elements. Events can be random or scheduled.

### Business Rules

- RP events provide narrative
- Events can be random or scheduled
- Events have scripts and effects
- Events enhance gameplay narrative
- Events can be customized

### Player Interactions

- Players see RP events
- Players interact with events
- Players experience narrative

### System Requirements

- System must generate RP events
- System must execute event scripts
- System must handle event effects

### Dependencies

- **Event System**: RP events are events
- **Message System**: Events generate messages

### Data Model Requirements

- RP event definitions
- Event script execution

---

## Scheduled Events

### Functional Description

Events scheduled for specific cycles/turns. Scheduled events occur at predetermined times.

### Business Rules

- Events can be scheduled
- Scheduling specifies turn/cycle
- Scheduled events occur automatically
- Events can be one-time or recurring
- Scheduling allows event planning

### Player Interactions

- Players may see scheduled events
- Players prepare for scheduled events
- Players experience scheduled events

### System Requirements

- System must track scheduled events
- System must trigger events at scheduled times
- System must handle event scheduling

### Dependencies

- **Event System**: Scheduled events are events
- **Turn System**: Provides turn/cycle tracking

### Data Model Requirements

- Event scheduling logic
- Schedule tracking

---

## Feature Interactions

### Internal Interactions

- **Disease Contagion** spreads **Disease System**
- **Disease Treatment** improves **Disease Recovery**
- **Disease Mortality** affects **Population System**
- **Monster Attacks** trigger **Combat System**
- **Revolt Causes** trigger **Revolt System**
- **Revolt Resolution** removes **Revolt Effects**

### External System Interactions

- **Population System**: Affected by diseases and revolts
- **Production System**: Affected by revolts and weather
- **Combat System**: Resolves monster encounters
- **Reputation System**: Affected by revolts and collapses
- **Building System**: Buildings collapse
- **Map System**: Fires spread, monsters move
- **Naval System**: Affected by weather
- **Message System**: Generates event notifications

---

## Technical Considerations

### Performance Requirements

- Event generation must be efficient
- Disease calculations must be performant
- Monster movement must be fast

### Scalability Requirements

- System must support many concurrent events
- Event processing must scale with player count
- Disease tracking must be efficient

### Data Persistence

- Event data must persist
- Disease status must be saved
- Scheduled events must persist

### Real-time Requirements

- Event generation occurs per turn
- Event effects apply per turn
- Scheduled events trigger at scheduled times

### Validation Requirements

- All events must validate conditions
- Event effects must be validated
- Event scheduling must be validated

