# Swag System

## Overview

The Swag System is a competitive team-based system where players form teams to compete in matches. Teams use strategies, compete in rounds, and gain experience. Matches require arenas and portals, and victories provide prize money and reputation benefits.

## Feature List

1. [Team System](#team-system)
2. [Match Resolution](#match-resolution)
3. [Strategy System](#strategy-system)
4. [Round System](#round-system)
5. [Victory/Defeat](#victorydefeat)
6. [Arena Requirements](#arena-requirements)
7. [Portal Requirements](#portal-requirements)
8. [Reputation Effects](#reputation-effects)
9. [Prize Money](#prize-money)
10. [Experience System](#experience-system)

---

## Team System

### Functional Description

Teams compete in swag matches. Teams are formed by players and compete against other teams.

### Business Rules

- Teams are formed by players
- Teams compete in matches
- Teams have strategies
- Teams gain experience
- Teams track wins and losses

### Player Interactions

- Players form teams
- Players see team status
- Players compete in matches

### System Requirements

- System must track teams
- System must support team formation
- System must handle team data

### Dependencies

- **Match Resolution**: Teams compete in matches
- **Strategy System**: Teams use strategies

### Data Model Requirements

- Team data structure
- Team tracking

---

## Match Resolution

### Functional Description

Match results are determined based on strategies. Matches are resolved using strategy-based calculations.

### Business Rules

- Matches are resolved based on strategies
- Strategy combinations affect outcomes
- Match resolution uses resolveSwagMatch()
- Matches have winners and losers
- Match results affect teams

### Player Interactions

- Players see match results
- Players benefit from victories
- Players see match outcomes

### System Requirements

- System must resolve matches
- System must calculate strategy effects
- System must determine winners

### Dependencies

- **Strategy System**: Strategies affect results
- **Round System**: Matches have rounds

### Data Model Requirements

- Match resolution logic
- Strategy calculation formulas

---

## Strategy System

### Functional Description

Different strategies for matches. Strategies affect match outcomes through combinations and bonuses.

### Business Rules

- Teams select strategies
- Strategies are stored in strategie field
- Strategy combinations provide bonuses
- Bonuses are calculated by swagGetBonusCombinaison()
- Strategies affect match outcomes

### Player Interactions

- Players select strategies
- Players see strategy effects
- Players benefit from good strategies

### System Requirements

- System must support strategy selection
- System must calculate strategy bonuses
- System must apply strategy effects

### Dependencies

- **Match Resolution**: Strategies affect results
- **Round System**: Strategies used in rounds

### Data Model Requirements

- Strategy definitions
- Strategy bonus calculations

---

## Round System

### Functional Description

Multiple rounds per match. Rounds progress through match phases.

### Business Rules

- Matches have multiple rounds
- Rounds are tracked in SWAG_POULES table
- Round progression determines match flow
- Rounds may have different rules
- Round results accumulate

### Player Interactions

- Players see round progress
- Players see round results
- Players benefit from round wins

### System Requirements

- System must track rounds
- System must progress rounds
- System must handle round results

### Dependencies

- **Match Resolution**: Rounds are part of matches
- **Victory/Defeat**: Round results affect match

### Data Model Requirements

- Round tracking
- Round progression logic

---

## Victory/Defeat

### Functional Description

Win/loss tracking for teams. Victories and defeats are recorded and affect team status.

### Business Rules

- Teams track victories and defeats
- Wins and losses stored in victoires and defaites fields
- Win/loss records affect team ranking
- Victories provide rewards
- Defeats may have penalties

### Player Interactions

- Players see win/loss records
- Players benefit from victories
- Players see team rankings

### System Requirements

- System must track wins and losses
- System must update records
- System must calculate rankings

### Dependencies

- **Match Resolution**: Determines wins/losses
- **Reputation Effects**: Wins affect reputation

### Data Model Requirements

- Win/loss tracking
- Ranking calculations

---

## Arena Requirements

### Functional Description

Matches require arenas. Arenas are special buildings needed for swag competitions.

### Business Rules

- Matches require arenas
- Arenas are special buildings
- Arena validation occurs before matches
- Multiple arenas may be needed
- Arena destruction prevents matches

### Player Interactions

- Players construct arenas
- Players see arena requirements
- Players maintain arenas

### System Requirements

- System must validate arena availability
- System must check arena status
- System must handle arena requirements

### Dependencies

- **Building System**: Arenas are buildings
- **Construction System**: Constructs arenas

### Data Model Requirements

- Arena requirement validation
- Arena status tracking

---

## Portal Requirements

### Functional Description

Portals needed for matches. Portals enable team travel to match locations.

### Business Rules

- Matches require portals
- Portals enable team travel
- Portal validation occurs before matches
- Portals must be functional
- Portal destruction prevents matches

### Player Interactions

- Players construct portals
- Players see portal requirements
- Players maintain portals

### System Requirements

- System must validate portal availability
- System must check portal status
- System must handle portal requirements

### Dependencies

- **Building System**: Portals are buildings
- **Construction System**: Constructs portals

### Data Model Requirements

- Portal requirement validation
- Portal status tracking

---

## Reputation Effects

### Functional Description

Swag results affect reputation. Victories increase reputation, defeats may decrease it.

### Business Rules

- Swag victories increase reputation
- Reputation updates from swag results
- Reputation affects player status
- Reputation changes are calculated
- Reputation is stored in reputation field

### Player Interactions

- Players see reputation changes
- Players benefit from victories
- Players work to improve reputation

### System Requirements

- System must calculate reputation changes
- System must update reputation
- System must apply reputation effects

### Dependencies

- **Reputation System**: Receives updates
- **Victory/Defeat**: Results affect reputation

### Data Model Requirements

- Reputation change calculations
- Reputation update logic

---

## Prize Money

### Functional Description

Financial rewards for victories. Winners receive prize money from matches.

### Business Rules

- Victories provide prize money
- Prize money is awarded by addEntreeTresor()
- Prize amounts vary by match
- Prize money is added to treasury
- Prize money is calculated in resolveSwagMatch()

### Player Interactions

- Players receive prize money
- Players see prize amounts
- Players benefit from victories

### System Requirements

- System must calculate prize money
- System must award prizes
- System must add money to treasury

### Dependencies

- **Currency System**: Prize money is currency
- **Victory/Defeat**: Victories provide prizes

### Data Model Requirements

- Prize money calculations
- Prize award logic

---

## Experience System

### Functional Description

Teams gain experience from matches. Experience improves team capabilities.

### Business Rules

- Teams gain experience from matches
- Experience is stored in experience field
- Experience improves team performance
- Experience is calculated in resolveSwagMatch()
- Experience is cumulative

### Player Interactions

- Players see team experience
- Players benefit from experienced teams
- Players see improved performance

### System Requirements

- System must track team experience
- System must calculate experience gains
- System must apply experience bonuses

### Dependencies

- **Match Resolution**: Provides experience
- **Team System**: Teams gain experience

### Data Model Requirements

- Experience tracking
- Experience gain calculations

---

## Feature Interactions

### Internal Interactions

- **Team System** competes in **Match Resolution**
- **Strategy System** affects **Match Resolution** outcomes
- **Round System** progresses through **Match Resolution**
- **Victory/Defeat** determines **Reputation Effects** and **Prize Money**
- **Arena Requirements** and **Portal Requirements** enable matches

### External System Interactions

- **Building System**: Provides arenas and portals
- **Currency System**: Provides prize money
- **Reputation System**: Receives updates from swag
- **Event System**: May generate swag events

---

## Technical Considerations

### Performance Requirements

- Match resolution must be efficient
- Strategy calculations must be fast
- Team tracking must be performant

### Scalability Requirements

- System must support many teams
- Match processing must scale
- Team tracking must be efficient

### Data Persistence

- Team data must persist
- Match results must be saved
- Experience must persist

### Real-time Requirements

- Match resolution occurs per turn
- Experience updates occur per match
- Prize awards are immediate

### Validation Requirements

- All swag actions must validate requirements
- Arena and portal availability must be validated
- Strategy selection must be validated

