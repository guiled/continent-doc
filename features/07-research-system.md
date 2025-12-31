---
layout: default
title: Research System
parent: Features
nav_order: 7
---

# Research System

## Overview

The Research System allows players to conduct scientific research that provides permanent bonuses to various game systems. Research progresses over time, costs money and resources, and grants bonuses upon completion. Research affects combat power, production efficiency, movement speed, and other game mechanics.

## Feature List

1. [Research Progress](#research-progress)
2. [Research Levels](#research-levels)
3. [Research Costs](#research-costs)
4. [Research Bonuses](#research-bonuses)
5. [Research Completion](#research-completion)
6. [Combat Sciences](#combat-sciences)
7. [Production Sciences](#production-sciences)
8. [Navigation Sciences](#navigation-sciences)
9. [Magic Sciences](#magic-sciences)
10. [Specialized Production](#specialized-production)
11. [Automatic Updates](#automatic-updates)
12. [Combat Power Updates](#combat-power-updates)
13. [Movement Updates](#movement-updates)
14. [Reputation Gain](#reputation-gain)
15. [Rank Increase](#rank-increase)

---

## Research Progress

### Functional Description

Research tasks progress over time based on worker assignment, morale, and bonuses. Progress is tracked as a percentage toward completion.

### Business Rules

- Research progress advances each turn
- Progress depends on: number of researchers, morale, research level, work cost
- Progress formula: base_progress × morale_factor × bonuses
- Progress is cumulative (0% to 100%)
- Research completes when progress reaches 100%
- Higher research levels require more progress

### Player Interactions

- Players assign researchers to research tasks
- Players see research progress
- Players receive notifications when research completes

### System Requirements

- System must calculate progress increment per turn
- System must track progress percentage
- System must handle progress with variable factors
- System must trigger completion at 100%

### Dependencies

- **Population System**: Provides researchers
- **Morale System**: Affects research speed
- **Economy System**: Provides research funding

### Data Model Requirements

- Progress percentage storage (0-100)
- Progress calculation formulas
- Turn-based progress tracking

---

## Research Levels

### Functional Description

Each science has multiple levels. Higher levels provide better bonuses but require more research to complete.

### Business Rules

- Sciences have levels (1, 2, 3, etc.)
- Each level must be researched separately
- Higher levels provide better bonuses
- Higher levels require more work to complete
- Research level affects progress calculation

### Player Interactions

- Players see current research levels
- Players research next level
- Players benefit from higher levels

### System Requirements

- System must track research level per science per player
- System must support level progression
- System must apply level-based bonuses

### Dependencies

- **Research Completion**: Increases levels
- **Research Bonuses**: Levels affect bonus values

### Data Model Requirements

- Research level tracking per science
- Level progression logic

---

## Research Costs

### Functional Description

Research requires money (researcher salaries) and may require other resources. Costs are paid during research.

### Business Rules

- Research costs money (écus) for researcher salaries
- Costs are calculated per researcher per turn
- Costs may include other resources
- Insufficient funds may pause research
- Costs are deducted during research progress

### Player Interactions

- Players must provide research funding
- Players see research costs
- Players receive warnings for insufficient funds

### System Requirements

- System must calculate research costs
- System must validate fund availability
- System must deduct costs during research

### Dependencies

- **Economy System**: Provides research funding
- **Resource System**: May require resources

### Data Model Requirements

- Research cost formulas
- Cost calculation logic

---

## Research Bonuses

### Functional Description

Various bonuses affect research speed. Bonuses come from morale, previous research, and other sources.

### Business Rules

- Bonuses increase research speed
- Morale provides research bonus
- Previous research may provide bonuses
- Bonuses are multiplicative
- Different sciences may have different bonus sources

### Player Interactions

- Players benefit from bonuses automatically
- Players can improve morale to boost research
- Players see bonus effects on research speed

### System Requirements

- System must calculate research bonuses
- System must apply bonuses to progress
- System must support multiple bonus sources

### Dependencies

- **Morale System**: Provides morale bonus
- **Research System**: Previous research may provide bonuses

### Data Model Requirements

- Research bonus calculation formulas
- Bonus source tracking

---

## Research Completion

### Functional Description

When research reaches 100% progress, it completes. Completion grants permanent bonuses and increases research level.

### Business Rules

- Research completes at 100% progress
- Completion increases science level by 1
- Completion grants permanent bonuses
- Completion increases player reputation
- Completion increases player rank/noblesse
- Completion triggers notifications

### Player Interactions

- Players receive completion notifications
- Players see new bonuses
- Players see reputation and rank increases

### System Requirements

- System must detect research completion
- System must apply completion bonuses
- System must update reputation and rank
- System must generate completion events

### Dependencies

- **Research Progress**: Triggers completion
- **Bonus System**: Applies completion bonuses
- **Reputation System**: Increases reputation
- **Rank System**: Increases rank

### Data Model Requirements

- Completion detection logic
- Bonus application logic
- Reputation/rank update logic

---

## Combat Sciences

### Functional Description

Military research improves combat capabilities. Combat sciences increase unit power and effectiveness.

### Business Rules

- Combat sciences improve military units
- Research provides combat power bonuses
- Bonuses apply to all units
- Higher levels provide better bonuses
- Combat research affects battle outcomes

### Player Interactions

- Players research combat sciences
- Players benefit from combat bonuses
- Players see improved unit power

### System Requirements

- System must support combat science research
- System must apply combat bonuses
- System must update unit power calculations

### Dependencies

- **Military System**: Applies combat bonuses
- **Combat Power Updates**: Updates unit power

### Data Model Requirements

- Combat science definitions
- Combat bonus application logic

---

## Production Sciences

### Functional Description

Production research improves resource production efficiency. Production sciences increase output and reduce costs.

### Business Rules

- Production sciences improve production
- Research provides production efficiency bonuses
- Bonuses apply to all production types
- Higher levels provide better bonuses
- Production research affects resource output

### Player Interactions

- Players research production sciences
- Players benefit from production bonuses
- Players see improved production output

### System Requirements

- System must support production science research
- System must apply production bonuses
- System must update production calculations

### Dependencies

- **Production System**: Applies production bonuses
- **Production Efficiency**: Updates efficiency

### Data Model Requirements

- Production science definitions
- Production bonus application logic

---

## Navigation Sciences

### Functional Description

Navigation research improves movement speed and naval capabilities. Navigation sciences increase unit movement speed.

### Business Rules

- Navigation sciences improve movement
- Research provides movement speed bonuses
- Bonuses apply to all units
- Higher levels provide better bonuses
- Navigation research affects travel time

### Player Interactions

- Players research navigation sciences
- Players benefit from movement bonuses
- Players see improved unit speed

### System Requirements

- System must support navigation science research
- System must apply movement bonuses
- System must update speed calculations

### Dependencies

- **Military System**: Applies movement bonuses
- **Movement Updates**: Updates unit speed

### Data Model Requirements

- Navigation science definitions
- Movement bonus application logic

---

## Magic Sciences

### Functional Description

Magical research provides special abilities and effects. Magic sciences have levels 600-999 and provide unique bonuses.

### Business Rules

- Magic sciences are special research (levels 600-999)
- Magic research provides unique bonuses
- Magic research may have special requirements
- Magic research provides special abilities
- Magic research is more advanced

### Player Interactions

- Players research magic sciences
- Players benefit from magic bonuses
- Players gain special abilities

### System Requirements

- System must support magic science research
- System must apply magic bonuses
- System must handle special magic mechanics

### Dependencies

- **Research System**: Magic research mechanics
- **Bonus System**: Applies magic bonuses

### Data Model Requirements

- Magic science definitions
- Magic bonus application logic

---

## Specialized Production

### Functional Description

Specialized production research improves specific production types. Provides targeted bonuses for particular resources.

### Business Rules

- Specialized research targets specific productions
- Research provides bonuses for specific resource types
- Bonuses are more focused than general production research
- Different specialized research for different resources
- Higher levels provide better specialized bonuses

### Player Interactions

- Players research specialized production
- Players benefit from specialized bonuses
- Players see improved specific production

### System Requirements

- System must support specialized production research
- System must apply specialized bonuses
- System must target specific production types

### Dependencies

- **Production System**: Applies specialized bonuses
- **Production Sciences**: Specialized variant

### Data Model Requirements

- Specialized production science definitions
- Specialized bonus application logic

---

## Automatic Updates

### Functional Description

Research bonuses automatically update unit stats and capabilities. No manual intervention required.

### Business Rules

- Research bonuses apply automatically
- Unit stats update when research completes
- Updates occur immediately upon completion
- Updates affect all relevant units
- Updates are permanent

### Player Interactions

- Players benefit from automatic updates
- Players see improved unit capabilities
- Players don't need to manually apply bonuses

### System Requirements

- System must apply bonuses automatically
- System must update unit stats
- System must handle bonus updates

### Dependencies

- **Research Completion**: Triggers updates
- **Unit System**: Receives updates

### Data Model Requirements

- Automatic update logic
- Stat update mechanisms

---

## Combat Power Updates

### Functional Description

Combat research automatically updates unit combat power. Units become more effective in battle.

### Business Rules

- Combat research increases unit power
- Power updates apply to all units
- Updates are immediate upon research completion
- Power increases are permanent
- Power formula includes research bonus

### Player Interactions

- Players see improved unit power
- Players benefit from combat research
- Players win more battles

### System Requirements

- System must update unit power calculations
- System must apply combat research bonuses
- System must recalculate power when research completes

### Dependencies

- **Combat Sciences**: Provides combat bonuses
- **Unit Power**: Receives power updates

### Data Model Requirements

- Power update logic
- Combat bonus application

---

## Movement Updates

### Functional Description

Navigation research automatically updates unit movement speed. Units can move faster across the map.

### Business Rules

- Navigation research increases movement speed
- Speed updates apply to all units
- Updates are immediate upon research completion
- Speed increases are permanent
- Speed formula includes navigation bonus

### Player Interactions

- Players see improved unit speed
- Players benefit from navigation research
- Players move units faster

### System Requirements

- System must update unit speed calculations
- System must apply navigation research bonuses
- System must recalculate speed when research completes

### Dependencies

- **Navigation Sciences**: Provides movement bonuses
- **Unit Speed**: Receives speed updates

### Data Model Requirements

- Speed update logic
- Movement bonus application

---

## Reputation Gain

### Functional Description

Research completion increases village reputation. Reputation affects various game mechanics.

### Business Rules

- Research completion increases reputation
- Reputation gain depends on research level
- Higher level research provides more reputation
- Reputation gain is calculated by formula
- Reputation affects player status

### Player Interactions

- Players see reputation increases
- Players benefit from higher reputation
- Players gain status from research

### System Requirements

- System must calculate reputation gains
- System must update reputation on completion
- System must apply reputation effects

### Dependencies

- **Research Completion**: Triggers reputation gain
- **Reputation System**: Receives reputation updates

### Data Model Requirements

- Reputation gain formulas
- Reputation update logic

---

## Rank Increase

### Functional Description

Research completion increases player rank/noblesse. Rank affects player status and capabilities.

### Business Rules

- Research completion increases rank/noblesse
- Rank gain depends on research level
- Higher level research provides more rank
- Rank gain is calculated by formula
- Rank affects player status and titles

### Player Interactions

- Players see rank increases
- Players benefit from higher rank
- Players gain titles from rank

### System Requirements

- System must calculate rank gains
- System must update rank on completion
- System must apply rank effects

### Dependencies

- **Research Completion**: Triggers rank gain
- **Rank System**: Receives rank updates

### Data Model Requirements

- Rank gain formulas
- Rank update logic

---

## Feature Interactions

### Internal Interactions

- **Research Progress** leads to **Research Completion**
- **Research Completion** increases **Research Levels**
- **Research Levels** affect **Research Bonuses**
- **Research Bonuses** provide **Automatic Updates**
- **Combat Sciences** provide **Combat Power Updates**

### External System Interactions

- **Population System**: Provides researchers
- **Economy System**: Provides research funding
- **Morale System**: Affects research speed
- **Military System**: Receives combat and movement bonuses
- **Production System**: Receives production bonuses
- **Reputation System**: Receives reputation from research
- **Rank System**: Receives rank from research
- **Bonus System**: Applies research bonuses

---

## Technical Considerations

### Performance Requirements

- Research progress calculations must be efficient
- Bonus lookups must be fast
- Stat updates must be performant

### Scalability Requirements

- System must support many concurrent research tasks
- Research processing must scale with player count
- Bonus application must be efficient at scale

### Data Persistence

- Research progress must persist
- Research levels must be saved
- Bonus data must persist

### Real-time Requirements

- Research progress updates occur per turn
- Bonus application is immediate upon completion
- Stat updates are immediate

### Validation Requirements

- All research actions must validate requirements
- Research costs must be validated
- Research completion must be validated

