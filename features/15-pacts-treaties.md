---
layout: default
title: Pacts & Treaties
parent: Features
nav_order: 15
---

# Pacts & Treaties

## Overview

The Pacts & Treaties System manages various diplomatic pacts between players and nations. Pacts include pariah status (PDR), non-aggression pacts (PNA), and vassal pacts (PSV). Pacts have duration, can be modified, inherited, and may conflict with each other.

## Feature List

1. [Pariah Status (PDR)](#pariah-status-pdr)
2. [Non-Aggression Pacts (PNA)](#non-aggression-pacts-pna)
3. [Vassal Pacts (PSV)](#vassal-pacts-psv)
4. [Pact Duration](#pact-duration)
5. [Pact Modification](#pact-modification)
6. [Pact Inheritance](#pact-inheritance)
7. [Pact Conflicts](#pact-conflicts)

---

## Pariah Status (PDR)

### Functional Description

Outcast status with nations. Players can be declared pariahs by nations, affecting relations with all nation members.

### Business Rules

- Pariah status is a pact type (PDR)
- Nations can declare players as pariahs
- Pariah status affects relations with all nation members
- Pariah status may have penalties
- Pariah status can be removed

### Player Interactions

- Players may be declared pariahs
- Players see pariah status
- Players suffer penalties from pariah status

### System Requirements

- System must track pariah status
- System must apply pariah effects to relations
- System must support pariah declaration and removal

### Dependencies

- **Diplomacy System**: Pariah affects relations
- **Nation System**: Nations declare pariahs

### Data Model Requirements

- Pariah status tracking
- Pariah effect application

---

## Non-Aggression Pacts (PNA)

### Functional Description

Non-aggression agreements between players. PNA pacts prevent military actions between signatories.

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
- **Diplomacy System**: Pacts affect relations

### Data Model Requirements

- Non-aggression pact tracking
- Pact enforcement logic

---

## Vassal Pacts (PSV)

### Functional Description

Temporary vassal pacts after capture. PSV pacts are created when players capture territories.

### Business Rules

- PSV pacts are created on capture
- Pacts are temporary
- Pacts establish vassal relationships
- Pacts may have duration
- Pacts are managed by pact system

### Player Interactions

- Players receive PSV pacts on capture
- Players see pact status
- Players manage pact relationships

### System Requirements

- System must create PSV pacts on capture
- System must track PSV pacts
- System must handle pact expiration

### Dependencies

- **Military System**: Captures create pacts
- **Vassal System**: PSV are vassal pacts

### Data Model Requirements

- PSV pact creation logic
- PSV pact tracking

---

## Pact Duration

### Functional Description

Time-limited pacts. Pacts have duration and expire after time passes.

### Business Rules

- Pacts have duration stored in duree field
- Duration is tracked per turn
- Pacts expire when duration reaches zero
- Expired pacts are removed
- Duration can be extended (if supported)

### Player Interactions

- Players see pact duration
- Players know when pacts expire
- Players may extend pacts (if supported)

### System Requirements

- System must track pact duration
- System must decrement duration over time
- System must remove expired pacts

### Dependencies

- **Pact System**: Tracks duration
- **Turn System**: Provides time tracking

### Data Model Requirements

- Duration tracking per pact
- Expiration handling logic

---

## Pact Modification

### Functional Description

Pacts modified on suzerain change. When vassal suzerain changes, pacts are updated accordingly.

### Business Rules

- Pacts are modified when suzerain changes
- Modification handled by PAC_ModifPactesSurChangeSuzerain()
- Modification occurs in changeSuzerain()
- Pacts may be transferred to new suzerain
- Pacts may be cancelled on suzerain change

### Player Interactions

- Players see pact modifications
- Players are affected by modifications
- Players see updated pact status

### System Requirements

- System must detect suzerain changes
- System must modify pacts accordingly
- System must handle pact transfers

### Dependencies

- **Vassal System**: Suzerain changes trigger modifications
- **Pact System**: Pacts are modified

### Data Model Requirements

- Pact modification logic
- Suzerain change detection

---

## Pact Inheritance

### Functional Description

Vassals inherit suzerain pacts. When becoming vassal, players inherit certain pacts from suzerain.

### Business Rules

- Vassals inherit suzerain pacts
- PNA and Pariah pacts are inherited
- Inheritance handled by PAC_ModifPactesSurChangeSuzerain()
- Inherited pacts affect vassal relations
- Inheritance occurs automatically

### Player Interactions

- Players inherit pacts as vassals
- Players see inherited pact status
- Players are affected by inherited pacts

### System Requirements

- System must detect vassalization
- System must inherit pacts
- System must apply inherited pact effects

### Dependencies

- **Vassal System**: Vassalization triggers inheritance
- **Pact System**: Pacts are inherited

### Data Model Requirements

- Pact inheritance logic
- Inheritance rule definitions

---

## Pact Conflicts

### Functional Description

Pacts can conflict with each other. Conflict detection prevents incompatible pacts.

### Business Rules

- Pacts can conflict with each other
- Conflicts are detected in PAC_setPNA()
- Conflicts are resolved in getDiploJoueur()
- Conflicting pacts may be invalid
- Conflict resolution determines which pact applies

### Player Interactions

- Players see pact conflicts
- Players resolve conflicts
- Players see conflict warnings

### System Requirements

- System must detect pact conflicts
- System must resolve conflicts
- System must handle conflict resolution

### Dependencies

- **Diplomacy System**: Conflicts affect relations
- **Pact System**: Pacts can conflict

### Data Model Requirements

- Conflict detection logic
- Conflict resolution rules

---

## Feature Interactions

### Internal Interactions

- **Pact Duration** manages **Pact System** lifecycle
- **Pact Modification** updates **Pact System** on suzerain change
- **Pact Inheritance** transfers **Pact System** to vassals
- **Pact Conflicts** resolve **Pact System** incompatibilities

### External System Interactions

- **Diplomacy System**: Pacts affect relations
- **Military System**: Pacts restrict actions
- **Vassal System**: Pacts created and modified
- **Nation System**: Pariah status with nations

---

## Technical Considerations

### Performance Requirements

- Pact lookups must be efficient
- Conflict detection must be fast
- Pact modification must be performant

### Scalability Requirements

- System must support many pacts
- Pact processing must scale with player count
- Conflict detection must be efficient

### Data Persistence

- Pact data must persist
- Pact duration must be saved
- Pact status must persist

### Real-time Requirements

- Pact expiration occurs per turn
- Pact modifications are immediate
- Conflict detection is immediate

### Validation Requirements

- All pact actions must validate permissions
- Pact creation must validate conflicts
- Pact modification must validate suzerain changes

