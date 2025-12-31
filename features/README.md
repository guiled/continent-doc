---
layout: default
title: Feature Documentation Index
parent: Features
---

# Feature Documentation Index

This directory contains comprehensive documentation for all features in the Renaissance project. Each document describes features from a functional and business rule perspective, focusing on what the system needs to support rather than current implementation details.

## Purpose

These documents are designed to:
- Be understandable by both humans and AI agents
- Describe **what** features do, not **how** they're implemented
- Document business rules that must be preserved during refactoring
- Provide technical requirements at a high level (use-case based)
- Help future developers choose appropriate technologies

## Documentation Structure

Each feature document follows this structure:
1. **Overview** - High-level description of the feature category
2. **Feature List** - Table of contents for all features
3. **Feature Details** - For each feature:
   - Functional Description
   - Business Rules
   - Player Interactions
   - System Requirements
   - Dependencies
   - Data Model Requirements
4. **Feature Interactions** - How features interact with each other
5. **Technical Considerations** - High-level technical requirements

## Feature Documents

1. [Construction & Building System](01-construction-building-system.md)
   - Building construction, upgrades, maintenance, terrain modification, naval construction

2. [Production System](02-production-system.md)
   - Resource production, worker management, production types, seasonal effects, visualization

3. [Military System](03-military-system.md)
   - Unit formation, combat, movement, sieges, naval military, portal teleportation

4. [Diplomacy System](04-diplomacy-system.md)
   - Nation relations, player relations, alliances, ambassadors, pariah status, non-aggression pacts

5. [Guild System](05-guild-system.md)
   - Commerce, shadow, saffron, and church guilds; banking, loans, artifact markets, alchemy

6. [Exploration System](06-exploration-system.md)
   - Location discovery, treasure finding, monster encounters, exploration mechanics

7. [Research System](07-research-system.md)
   - Science research, research types, bonuses, automatic updates, reputation and rank gains

8. [Feudalism & Vassalage](08-feudalism-vassalage.md)
   - Vassalization, suzerain authority, protection requirements, taxes, influence system

9. [Events & Random Events](09-events-random-events.md)
   - Diseases, monster attacks, revolts, building collapses, fires, weather, RP events

10. [Map & Territory Management](10-map-territory-management.md)
    - Hexagonal map, map layers, terrain types, pathfinding, seasonal effects, map normalization

11. [Trade & Economy](11-trade-economy.md)
    - Currency system, resource trading, market prices, trade routes, banking, loans, taxes

12. [Naval System](12-naval-system.md)
    - Deep sea fishing, naval travel, naval combat, ship maintenance, ship durability, weather effects

13. [Heroes System](13-heroes-system.md)
    - Hero recruitment, maintenance, resurrection, requirements, salaries, sacrifices

14. [Swag System](14-swag-system.md)
    - Team competitions, match resolution, strategies, rounds, arenas, portals, prize money

15. [Pacts & Treaties](15-pacts-treaties.md)
    - Pariah status, non-aggression pacts, vassal pacts, duration, modification, inheritance, conflicts

16. [Infrastructure & Utilities](16-infrastructure-utilities.md)
    - Server infrastructure, configuration, database, logging, messaging, administrative tools

## How to Use This Documentation

### For Developers

- **Understanding Features**: Read feature documents to understand what each system does
- **Business Rules**: Pay special attention to "Business Rules" sections - these must be preserved
- **Dependencies**: Check "Dependencies" to understand feature relationships
- **Technical Requirements**: Review "Technical Considerations" for implementation guidance

### For AI Agents

- **Feature Discovery**: Use feature documents to understand system capabilities
- **Business Logic**: Extract business rules from "Business Rules" sections
- **System Design**: Use "System Requirements" and "Technical Considerations" for architecture decisions
- **Data Modeling**: Reference "Data Model Requirements" for database design

### For Refactoring

- **Preserve Business Rules**: All business rules documented must be maintained
- **Technology Choice**: Use "System Requirements" to choose appropriate technologies
- **Feature Completeness**: Ensure all documented features are implemented
- **Interactions**: Consider "Feature Interactions" when refactoring

## Key Principles

1. **Feature-Focused**: Documents describe what features do, not how they're coded
2. **Business Rules Preserved**: Game logic documented here must be maintained
3. **Technology-Agnostic**: Requirements are described, not technology choices
4. **AI-Friendly**: Clear structure, consistent formatting, explicit relationships
5. **Human-Readable**: Clear language, examples, comprehensive coverage

## Implementation Status

For implementation status of features in the Renaissance codebase, see:
- [Features Implementation Checklist](../features-implementation-checklist.md)

For the original feature extraction from Continent:
- [Features Extracted from Continent](../features-extracted-from-continent.md)

## Notes

- These documents focus on **functional requirements** and **business rules**
- Technical implementation details are described only in terms of **final use-cases**
- The next development team should use these documents to choose appropriate technologies
- All business rules documented here must be preserved during refactoring
- Feature interactions are documented to help understand system dependencies

