---
layout: default
title: Feudalism & Vassalage
parent: Features
nav_order: 8
---

# Feudalism & Vassalage

## Overview

The Feudalism & Vassalage System manages hierarchical relationships between players. Players can become vassals of other players (suzerains), creating feudal relationships with obligations, taxes, and protection requirements. The system includes vassalization, suzerain authority, protection requirements, tax collection, and influence mechanics.

## Feature List

1. [Vassalization](#vassalization)
2. [Suzerain System](#suzerain-system)
3. [Vassal Protection](#vassal-protection)
4. [Required Garrison](#required-garrison)
5. [Vassal Tax](#vassal-tax)
6. [Suzerain Authority](#suzerain-authority)
7. [Vassal Loss Penalties](#vassal-loss-penalties)
8. [Feudal Reputation](#feudal-reputation)
9. [Vassal Independence](#vassal-independence)
10. [Feudal Relations](#feudal-relations)
11. [Political Influence](#political-influence)
12. [Influence Resistance](#influence-resistance)
13. [Influence Effects](#influence-effects)
14. [Revolt Management](#revolt-management)

---

## Vassalization

### Functional Description

Players can become vassals of other players, creating a feudal relationship. Vassalization establishes hierarchy and obligations.

### Business Rules

- Players can become vassals through various means (conquest, agreement, etc.)
- Vassalization creates suzerain-vassal relationship
- Relationship includes tax obligations
- Relationship includes protection requirements
- Vassalization can be broken

### Player Interactions

- Players become vassals
- Players see vassal status
- Players fulfill vassal obligations

### System Requirements

- System must track vassal relationships
- System must handle vassalization creation
- System must support relationship breaking

### Dependencies

- **Suzerain System**: Creates relationships
- **Vassal Tax**: Establishes tax obligations

### Data Model Requirements

- Vassal relationship tracking
- Relationship creation/breaking logic

---

## Suzerain System

### Functional Description

Suzerains are players who have vassals. Suzerains have authority over vassals and obligations to protect them.

### Business Rules

- Suzerains have vassals
- Suzerains have authority over vassals
- Suzerains must protect vassals
- Suzerains receive taxes from vassals
- Suzerains can lose vassals

### Player Interactions

- Players become suzerains
- Players manage vassals
- Players see suzerain status

### System Requirements

- System must track suzerain relationships
- System must manage suzerain authority
- System must handle vassal management

### Dependencies

- **Vassalization**: Creates suzerain relationships
- **Vassal Protection**: Suzerain obligations

### Data Model Requirements

- Suzerain relationship tracking
- Authority management logic

---

## Vassal Protection

### Functional Description

Suzerains must protect their vassals by maintaining military presence. Insufficient protection may allow vassals to break free.

### Business Rules

- Suzerains must maintain military presence at vassal locations
- Protection is measured by military power
- Insufficient protection allows vassal independence
- Protection requirements vary by vassal size and relations
- Protection is checked regularly

### Player Interactions

- Suzerains maintain protection forces
- Suzerains see protection status
- Vassals see protection levels

### System Requirements

- System must calculate required protection
- System must check protection levels
- System must handle insufficient protection

### Dependencies

- **Required Garrison**: Defines protection requirements
- **Military System**: Provides protection forces

### Data Model Requirements

- Protection requirement calculations
- Protection status tracking

---

## Required Garrison

### Functional Description

Minimum military presence required for suzerains to maintain authority over vassals. Garrison requirements vary based on multiple factors.

### Business Rules

- Required garrison depends on vassal population (peons, bourgeois)
- Required garrison depends on vassal title level
- Required garrison depends on diplomatic relations
- Required garrison depends on tax rate
- Required garrison is calculated by formula

### Player Interactions

- Suzerains see required garrison
- Suzerains maintain required forces
- Vassals see protection requirements

### System Requirements

- System must calculate required garrison
- System must validate garrison presence
- System must handle garrison changes

### Dependencies

- **Vassal Protection**: Uses garrison requirements
- **Population System**: Affects requirements
- **Diplomacy System**: Affects requirements

### Data Model Requirements

- Garrison requirement formulas
- Requirement calculation logic

---

## Vassal Tax

### Functional Description

Tax system between suzerain and vassal. Vassals pay taxes to suzerains based on tax rate.

### Business Rules

- Vassals pay taxes to suzerains
- Tax rate is defined in vassal relationship
- Taxes are collected from vassal treasury
- Tax collection occurs regularly
- Tax rate affects protection requirements

### Player Interactions

- Suzerains receive taxes
- Vassals pay taxes
- Players see tax rates and collections

### System Requirements

- System must track tax rates
- System must collect taxes regularly
- System must handle tax collection failures

### Dependencies

- **Economy System**: Handles tax payments
- **Vassalization**: Defines tax relationships

### Data Model Requirements

- Tax rate tracking
- Tax collection logic

---

## Suzerain Authority

### Functional Description

Suzerains have authority over vassals. Authority is maintained through military presence and proper protection.

### Business Rules

- Authority depends on protection level
- Full authority requires sufficient protection
- Insufficient protection reduces authority
- Authority affects vassal obligations
- Authority can be lost

### Player Interactions

- Suzerains exercise authority
- Suzerains see authority status
- Vassals see authority level

### System Requirements

- System must calculate authority level
- System must apply authority effects
- System must handle authority changes

### Dependencies

- **Vassal Protection**: Maintains authority
- **Required Garrison**: Affects authority

### Data Model Requirements

- Authority calculation logic
- Authority level tracking

---

## Vassal Loss Penalties

### Functional Description

Suzerains suffer penalties when they lose vassals. Penalties include reputation and rank reductions.

### Business Rules

- Losing vassals causes penalties
- Penalties include reputation reduction
- Penalties include rank/noblesse reduction
- Penalties scale with vassal importance
- Penalties are applied when vassalage breaks

### Player Interactions

- Suzerains suffer penalties
- Suzerains see penalty effects
- Players avoid losing vassals

### System Requirements

- System must calculate penalties
- System must apply penalties
- System must update reputation and rank

### Dependencies

- **Vassal Independence**: Triggers penalties
- **Reputation System**: Receives penalties
- **Rank System**: Receives penalties

### Data Model Requirements

- Penalty calculation formulas
- Penalty application logic

---

## Feudal Reputation

### Functional Description

Reputation is affected by feudal management. Good vassal management improves reputation, poor management reduces it.

### Business Rules

- Reputation changes based on vassal management
- Good protection improves reputation
- Poor protection reduces reputation
- Losing vassals reduces reputation
- Reputation affects player status

### Player Interactions

- Players see reputation changes
- Players manage vassals to maintain reputation
- Players benefit from good reputation

### System Requirements

- System must calculate reputation changes
- System must update reputation
- System must apply reputation effects

### Dependencies

- **Reputation System**: Receives updates
- **Vassal Management**: Affects reputation

### Data Model Requirements

- Reputation change calculations
- Reputation update logic

---

## Vassal Independence

### Functional Description

Vassals can break free from suzerains. Independence can occur through various means including insufficient protection.

### Business Rules

- Vassals can break vassalage
- Independence can occur from insufficient protection
- Independence can occur through player action
- Independence triggers penalties for former suzerain
- Independence removes vassal obligations

### Player Interactions

- Vassals break free
- Suzerains lose vassals
- Players see independence events

### System Requirements

- System must support vassalage breaking
- System must handle independence
- System must apply independence consequences

### Dependencies

- **Vassal Protection**: Insufficient protection allows independence
- **Vassal Loss Penalties**: Triggers penalties

### Data Model Requirements

- Independence logic
- Independence consequence handling

---

## Feudal Relations

### Functional Description

Diplomatic relations affect vassal requirements. Relations between nations affect protection requirements.

### Business Rules

- Diplomatic relations affect protection requirements
- Alliance relations reduce requirements
- War relations increase requirements
- Peace relations have moderate requirements
- Relations are considered in requirement calculations

### Player Interactions

- Players see relation effects on requirements
- Players manage relations to affect requirements

### System Requirements

- System must consider relations in calculations
- System must apply relation modifiers
- System must handle relation changes

### Dependencies

- **Diplomacy System**: Provides relations
- **Required Garrison**: Relations affect requirements

### Data Model Requirements

- Relation modifier calculations
- Requirement adjustment logic

---

## Political Influence

### Functional Description

Players can influence other players' populations. Influence can cause various effects including revolts.

### Business Rules

- Players can exert influence on other players
- Influence affects population loyalty
- Influence can cause revolts
- Influence can be resisted
- Influence is tracked over time

### Player Interactions

- Players exert influence
- Players see influence effects
- Players resist influence

### System Requirements

- System must track influence
- System must calculate influence effects
- System must handle influence application

### Dependencies

- **Influence Resistance**: Resists influence
- **Revolt Management**: Influence causes revolts

### Data Model Requirements

- Influence tracking
- Influence calculation logic

---

## Influence Resistance

### Functional Description

Players can resist political influence. Resistance reduces influence effectiveness.

### Business Rules

- Players can resist influence
- Resistance reduces influence effects
- Resistance may depend on various factors
- Resistance is calculated automatically
- Higher resistance reduces influence success

### Player Interactions

- Players benefit from resistance
- Players see resistance levels
- Players may improve resistance

### System Requirements

- System must calculate resistance
- System must apply resistance to influence
- System must track resistance levels

### Dependencies

- **Political Influence**: Resistance affects influence
- **Influence Effects**: Resistance reduces effects

### Data Model Requirements

- Resistance calculation formulas
- Resistance application logic

---

## Influence Effects

### Functional Description

Influence affects various game mechanics. Influence can cause revolts, affect loyalty, and other effects.

### Business Rules

- Influence affects population loyalty
- Influence can trigger revolts
- Influence affects various game mechanics
- Effects depend on influence strength
- Effects are applied over time

### Player Interactions

- Players see influence effects
- Players are affected by influence
- Players may counter influence

### System Requirements

- System must apply influence effects
- System must handle effect calculations
- System must trigger effect events

### Dependencies

- **Political Influence**: Provides influence
- **Revolt Management**: Influence triggers revolts

### Data Model Requirements

- Influence effect definitions
- Effect application logic

---

## Revolt Management

### Functional Description

Influence can cause or stop revolts. Revolts affect production, reputation, and player control.

### Business Rules

- Influence can cause planned revolts
- Revolts reduce production
- Revolts affect reputation
- Revolts can be resolved diplomatically or by force
- Revolts can be prevented or stopped

### Player Interactions

- Players see revolts
- Players resolve revolts
- Players prevent revolts

### System Requirements

- System must trigger revolts from influence
- System must handle revolt resolution
- System must apply revolt effects

### Dependencies

- **Political Influence**: Causes revolts
- **Production System**: Affected by revolts
- **Reputation System**: Affected by revolts

### Data Model Requirements

- Revolt trigger logic
- Revolt resolution mechanics
- Revolt effect definitions

---

## Feature Interactions

### Internal Interactions

- **Vassalization** creates **Suzerain System** relationships
- **Suzerain Authority** depends on **Vassal Protection**
- **Vassal Protection** requires **Required Garrison**
- **Vassal Tax** is collected from vassals
- **Vassal Independence** triggers **Vassal Loss Penalties**

### External System Interactions

- **Diplomacy System**: Relations affect protection requirements
- **Military System**: Provides protection forces
- **Economy System**: Handles tax collection
- **Reputation System**: Affected by vassal management
- **Rank System**: Affected by vassal loss
- **Population System**: Affects protection requirements
- **Event System**: Generates vassal-related events

---

## Technical Considerations

### Performance Requirements

- Protection calculations must be efficient
- Tax collection must be performant
- Influence calculations must be fast

### Scalability Requirements

- System must support many vassal relationships
- Protection checking must scale with player count
- Influence tracking must be efficient

### Data Persistence

- Vassal relationships must persist
- Tax rates must be saved
- Protection status must persist
- Influence data must be saved

### Real-time Requirements

- Protection checking occurs per turn
- Tax collection occurs per turn
- Influence effects apply per turn

### Validation Requirements

- All vassal actions must validate relationships
- Protection requirements must be validated
- Tax collection must validate funds

