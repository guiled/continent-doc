# Heroes System

## Overview

The Heroes System allows players to recruit and maintain powerful hero units. Heroes are special military units (composition > 9999) that require palaces, regular payment or sacrifices, and can be resurrected. Heroes provide significant military advantages but have high maintenance costs.

## Feature List

1. [Hero Recruitment](#hero-recruitment)
2. [Hero Maintenance](#hero-maintenance)
3. [Hero Resurrection](#hero-resurrection)
4. [Hero Requirements](#hero-requirements)
5. [Hero Departure](#hero-departure)
6. [Hero Salaries](#hero-salaries)
7. [Hero Sacrifices](#hero-sacrifices)
8. [Hero Resurrection Cost](#hero-resurrection-cost)
9. [Hero Experience Loss](#hero-experience-loss)
10. [Hero Reputation](#hero-reputation)

---

## Hero Recruitment

### Functional Description

Players can recruit powerful hero units. Heroes are identified by composition > 9999 and provide significant military advantages.

### Business Rules

- Heroes are special units (composition > 9999)
- Heroes are recruited through special means
- Heroes have exceptional combat power
- Heroes require palaces for recruitment
- Heroes are stored with special composition IDs

### Player Interactions

- Players recruit heroes
- Players see hero capabilities
- Players benefit from hero power

### System Requirements

- System must identify heroes (composition > 9999)
- System must support hero recruitment
- System must create hero units

### Dependencies

- **Military System**: Heroes are military units
- **Hero Requirements**: Requires palaces
- **Building System**: Palaces required

### Data Model Requirements

- Hero identification logic
- Hero recruitment mechanics

---

## Hero Maintenance

### Functional Description

Heroes require payment (money or sacrifices) to remain in service. Maintenance must be provided regularly.

### Business Rules

- Heroes require regular payment
- Some heroes require population sacrifices
- Maintenance must be provided each turn
- Failure to provide maintenance causes hero departure
- Maintenance costs vary by hero

### Player Interactions

- Players provide hero maintenance
- Players see maintenance requirements
- Players manage maintenance costs

### System Requirements

- System must track maintenance requirements
- System must process maintenance payments
- System must handle maintenance failures

### Dependencies

- **Hero Salaries**: Money payment
- **Hero Sacrifices**: Population payment
- **Currency System**: Provides money
- **Population System**: Provides sacrifices

### Data Model Requirements

- Maintenance requirement tracking
- Maintenance payment processing

---

## Hero Resurrection

### Functional Description

Heroes can be resurrected with special items after death. Resurrection restores heroes to service.

### Business Rules

- Heroes can be resurrected after death
- Resurrection requires special items (blue stones)
- Resurrection restores hero to service
- Resurrection may reduce hero experience
- Resurrection items are consumed

### Player Interactions

- Players resurrect heroes
- Players provide resurrection items
- Players see resurrection results

### System Requirements

- System must support hero resurrection
- System must validate resurrection items
- System must restore heroes

### Dependencies

- **Hero Resurrection Cost**: Requires items
- **Inventory System**: Stores resurrection items
- **Military System**: Heroes are units

### Data Model Requirements

- Resurrection logic
- Item requirement validation

---

## Hero Requirements

### Functional Description

Heroes require palaces to be maintained. Palaces are special buildings that support heroes.

### Business Rules

- Heroes require palaces
- Palaces must be functional (not destroyed)
- Palace destruction causes hero departure
- Multiple heroes may require multiple palaces
- Palace validation occurs regularly

### Player Interactions

- Players construct palaces for heroes
- Players see palace requirements
- Players maintain palaces

### System Requirements

- System must validate palace availability
- System must check palace status
- System must handle palace destruction

### Dependencies

- **Building System**: Palaces are buildings
- **Construction System**: Constructs palaces

### Data Model Requirements

- Palace requirement validation
- Palace status tracking

---

## Hero Departure

### Functional Description

Heroes leave if not paid or if palace is destroyed. Departure results in hero loss.

### Business Rules

- Heroes leave if maintenance not provided
- Heroes leave if palace is destroyed
- Departure is permanent (unless resurrected)
- Departure may affect reputation
- Departure triggers notifications

### Player Interactions

- Players see hero departures
- Players lose heroes from departure
- Players can prevent departure through maintenance

### System Requirements

- System must detect departure conditions
- System must remove departing heroes
- System must generate departure events

### Dependencies

- **Hero Maintenance**: Failure causes departure
- **Hero Requirements**: Palace destruction causes departure
- **Event System**: Generates departure events

### Data Model Requirements

- Departure detection logic
- Departure handling

---

## Hero Salaries

### Functional Description

Heroes require regular payment in currency. Salaries must be paid from treasury.

### Business Rules

- Heroes require salary payments
- Salaries are paid from village treasury
- Salaries must be paid regularly
- Salary amounts vary by hero
- Insufficient funds cause hero departure

### Player Interactions

- Players pay hero salaries
- Players see salary requirements
- Players manage treasury for salaries

### System Requirements

- System must track salary requirements
- System must process salary payments
- System must handle payment failures

### Dependencies

- **Currency System**: Provides salary funds
- **Economy System**: Manages treasury

### Data Model Requirements

- Salary requirement tracking
- Salary payment processing

---

## Hero Sacrifices

### Functional Description

Some heroes require population sacrifices instead of or in addition to money. Sacrifices reduce population.

### Business Rules

- Some heroes require population sacrifices
- Sacrifices reduce village population
- Sacrifices must be provided regularly
- Sacrifice amounts vary by hero
- Failure to provide sacrifices causes departure

### Player Interactions

- Players provide sacrifices
- Players see sacrifice requirements
- Players manage population for sacrifices

### System Requirements

- System must track sacrifice requirements
- System must process sacrifices
- System must reduce population

### Dependencies

- **Population System**: Provides sacrifices
- **Hero Maintenance**: Sacrifices are maintenance

### Data Model Requirements

- Sacrifice requirement tracking
- Sacrifice processing logic

---

## Hero Resurrection Cost

### Functional Description

Resurrection requires special items (blue stones). Items are consumed during resurrection.

### Business Rules

- Resurrection requires blue stones
- Blue stones are special items
- Items are consumed during resurrection
- Items may be rare or expensive
- Multiple items may be required

### Player Interactions

- Players acquire blue stones
- Players use stones for resurrection
- Players see resurrection costs

### System Requirements

- System must validate resurrection items
- System must consume items
- System must track item availability

### Dependencies

- **Inventory System**: Stores blue stones
- **Hero Resurrection**: Uses items

### Data Model Requirements

- Resurrection item requirements
- Item consumption logic

---

## Hero Experience Loss

### Functional Description

Heroes lose experience on death. Resurrection may restore heroes but with reduced experience.

### Business Rules

- Heroes lose experience on death
- Experience loss is permanent
- Resurrection may restore hero but not experience
- Experience affects hero power
- Experience loss reduces hero effectiveness

### Player Interactions

- Players see experience loss
- Players try to prevent hero death
- Players see reduced hero power

### System Requirements

- System must track hero experience
- System must reduce experience on death
- System must apply experience effects

### Dependencies

- **Hero Resurrection**: May restore hero but not experience
- **Military System**: Experience affects power

### Data Model Requirements

- Experience loss calculations
- Experience tracking

---

## Hero Reputation

### Functional Description

Hero management affects reputation. Good hero management improves reputation, poor management reduces it.

### Business Rules

- Hero management affects reputation
- Maintaining heroes improves reputation
- Losing heroes reduces reputation
- Hero departure causes reputation loss
- Reputation effects are calculated

### Player Interactions

- Players see reputation effects
- Players manage heroes to maintain reputation
- Players benefit from good hero management

### System Requirements

- System must calculate reputation effects
- System must update reputation
- System must apply reputation changes

### Dependencies

- **Reputation System**: Receives updates
- **Hero Management**: Affects reputation

### Data Model Requirements

- Reputation effect calculations
- Reputation update logic

---

## Feature Interactions

### Internal Interactions

- **Hero Requirements** (palaces) enable **Hero Recruitment**
- **Hero Maintenance** prevents **Hero Departure**
- **Hero Resurrection** restores **Hero Recruitment** after death
- **Hero Salaries** and **Hero Sacrifices** are **Hero Maintenance** types
- **Hero Departure** affects **Hero Reputation**

### External System Interactions

- **Military System**: Heroes are military units
- **Building System**: Provides palaces
- **Currency System**: Provides hero salaries
- **Population System**: Provides hero sacrifices
- **Inventory System**: Stores resurrection items
- **Reputation System**: Affected by hero management
- **Event System**: Generates hero departure events

---

## Technical Considerations

### Performance Requirements

- Hero maintenance processing must be efficient
- Hero validation must be fast
- Resurrection processing must be performant

### Scalability Requirements

- System must support many heroes
- Hero processing must scale with player count
- Hero tracking must be efficient

### Data Persistence

- Hero data must persist
- Hero experience must be saved
- Maintenance status must persist

### Real-time Requirements

- Hero maintenance occurs per turn
- Hero validation occurs per turn
- Hero departure is immediate

### Validation Requirements

- All hero actions must validate requirements
- Maintenance must validate funds/population
- Resurrection must validate items

