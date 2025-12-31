# Guild System

## Overview

The Guild System provides specialized services through different guild types (Commerce, Shadow, Saffron, Church). Guilds offer banking, loans, artifact markets, auctions, delivery services, and alchemical effects. Players build reputation with guilds to access higher-level services.

## Feature List

1. [Commerce Guild](#commerce-guild)
2. [Shadow Guild](#shadow-guild)
3. [Saffron Guild](#saffron-guild)
4. [Church Guild](#church-guild)
5. [Banking](#banking)
6. [Loans](#loans)
7. [Artifact Market](#artifact-market)
8. [Auction System](#auction-system)
9. [Delivery Service](#delivery-service)
10. [Black Market](#black-market)
11. [Guild Reputation](#guild-reputation)
12. [Guild Levels](#guild-levels)
13. [Lottery](#lottery)
14. [Artifact Valuation](#artifact-valuation)
15. [Market Updates](#market-updates)
16. [Alchemical Effects](#alchemical-effects)
17. [Alchemical Cancellation](#alchemical-cancellation)
18. [Alchemical Duration](#alchemical-duration)

---

## Commerce Guild

### Functional Description

Trade and economic guild providing commercial services including banking, loans, and market access.

### Business Rules

- Commerce guild level tracked per player
- Higher levels unlock better services
- Commerce guild provides economic benefits
- Special buildings (halls) may boost commerce guild level

### Player Interactions

- Players interact with commerce guild
- Players build reputation to access services
- Players see commerce guild level

### System Requirements

- System must track commerce guild level per player
- System must provide commerce services
- System must support level progression

### Dependencies

- **Guild Reputation**: Tracks reputation with commerce guild
- **Building System**: Special buildings affect guild level

### Data Model Requirements

- Commerce guild level tracking
- Commerce service definitions

---

## Shadow Guild

### Functional Description

Secret operations guild providing covert services including black market and shadow operations.

### Business Rules

- Shadow guild level tracked per player
- Higher levels unlock secret services
- Shadow guild provides covert benefits
- Shadow guild operations may be hidden

### Player Interactions

- Players interact with shadow guild
- Players build reputation for secret services
- Players see shadow guild level

### System Requirements

- System must track shadow guild level per player
- System must provide shadow services
- System must support level progression

### Dependencies

- **Guild Reputation**: Tracks reputation with shadow guild

### Data Model Requirements

- Shadow guild level tracking
- Shadow service definitions

---

## Saffron Guild

### Functional Description

Specialized guild providing unique services. Guild level determines service access.

### Business Rules

- Saffron guild level tracked per player
- Higher levels unlock specialized services
- Saffron guild provides unique benefits

### Player Interactions

- Players interact with saffron guild
- Players build reputation for specialized services
- Players see saffron guild level

### System Requirements

- System must track saffron guild level per player
- System must provide saffron services
- System must support level progression

### Dependencies

- **Guild Reputation**: Tracks reputation with saffron guild

### Data Model Requirements

- Saffron guild level tracking
- Saffron service definitions

---

## Church Guild

### Functional Description

Religious guild providing spiritual services. Special buildings (cathedrals) may boost church guild level.

### Business Rules

- Church guild level tracked per player
- Higher levels unlock religious services
- Cathedrals boost church guild level
- Church guild provides spiritual benefits

### Player Interactions

- Players interact with church guild
- Players build reputation for religious services
- Players see church guild level

### System Requirements

- System must track church guild level per player
- System must provide church services
- System must support level progression

### Dependencies

- **Guild Reputation**: Tracks reputation with church guild
- **Building System**: Cathedrals affect guild level

### Data Model Requirements

- Church guild level tracking
- Church service definitions

---

## Banking

### Functional Description

Interest-bearing bank accounts allow players to deposit money and earn interest over time.

### Business Rules

- Players can deposit money in bank accounts
- Interest is calculated and paid regularly
- Interest rate is configurable (BANQUE_TAUX_INTERET)
- Interest compounds over time
- Banking requires commerce guild access

### Player Interactions

- Players deposit money in banks
- Players receive interest payments
- Players withdraw money from accounts
- Players see account balances

### System Requirements

- System must track bank account balances
- System must calculate interest payments
- System must process interest regularly
- System must support deposits and withdrawals

### Dependencies

- **Commerce Guild**: Provides banking services
- **Economy System**: Manages currency

### Data Model Requirements

- Bank account tracking
- Interest calculation formulas
- Transaction history

---

## Loans

### Functional Description

Debt system allows players to borrow money with repayment obligations. Loans must be repaid over time.

### Business Rules

- Players can take loans from guilds
- Loans have repayment schedules
- Loans accrue interest
- Default on loans may have penalties
- Loan amounts may be limited by guild level

### Player Interactions

- Players request loans
- Players make loan repayments
- Players see loan balances and schedules
- Players may default on loans

### System Requirements

- System must track loan balances
- System must calculate repayment schedules
- System must process repayments
- System must handle loan defaults

### Dependencies

- **Commerce Guild**: Provides loan services
- **Economy System**: Manages currency

### Data Model Requirements

- Loan tracking
- Repayment schedule calculations
- Default handling logic

---

## Artifact Market

### Functional Description

Market for magical artifacts where players can buy and sell special items. Artifact values fluctuate based on market conditions.

### Business Rules

- Artifacts are traded on market
- Artifact values are dynamic
- Market updates regularly
- Artifact availability varies
- Market access may require guild level

### Player Interactions

- Players browse artifact market
- Players buy artifacts
- Players sell artifacts
- Players see artifact values

### System Requirements

- System must track artifact market data
- System must calculate artifact values
- System must update market regularly
- System must handle buy/sell transactions

### Dependencies

- **Artifact System**: Defines artifacts
- **Economy System**: Handles transactions

### Data Model Requirements

- Artifact market data
- Artifact value calculations
- Market update logic

---

## Auction System

### Functional Description

Auction system for artifacts where players bid on items. Highest bidder wins the auction.

### Business Rules

- Artifacts are auctioned periodically
- Players place bids
- Highest bid wins
- Auctions have time limits
- Auction prices update dynamically
- Auction access may require guild level

### Player Interactions

- Players view auctions
- Players place bids
- Players win auctions
- Players see auction results

### System Requirements

- System must track auctions
- System must process bids
- System must determine winners
- System must update auction prices

### Dependencies

- **Artifact Market**: Uses artifact system
- **Economy System**: Handles bid payments

### Data Model Requirements

- Auction tracking
- Bid processing logic
- Winner determination

---

## Delivery Service

### Functional Description

Guild delivery service transports goods between locations. Provides safe transport of resources.

### Business Rules

- Guilds deliver goods between locations
- Delivery requires payment
- Delivery is safer than player transport
- Delivery time depends on distance
- Delivery access may require guild level

### Player Interactions

- Players request deliveries
- Players pay delivery fees
- Players receive delivered goods
- Players track delivery progress

### System Requirements

- System must track delivery requests
- System must calculate delivery costs
- System must process deliveries
- System must handle delivery completion

### Dependencies

- **Trade System**: Delivers trade goods
- **Economy System**: Handles delivery fees

### Data Model Requirements

- Delivery request tracking
- Delivery cost calculations
- Delivery processing logic

---

## Black Market

### Functional Description

Black market operations through shadow guild. Provides access to restricted goods and services.

### Business Rules

- Black market accessed through shadow guild
- Black market offers restricted items
- Black market prices may be higher
- Black market access requires shadow guild level
- Black market operations may be secret

### Player Interactions

- Players access black market
- Players buy restricted goods
- Players see black market offerings

### System Requirements

- System must provide black market access
- System must track black market inventory
- System must handle black market transactions

### Dependencies

- **Shadow Guild**: Provides black market access
- **Economy System**: Handles transactions

### Data Model Requirements

- Black market inventory
- Black market transaction tracking

---

## Guild Reputation

### Functional Description

Players build reputation levels with different guilds. Higher reputation unlocks better services and higher guild levels.

### Business Rules

- Reputation tracked per guild per player
- Reputation increases through interactions
- Higher reputation unlocks higher guild levels
- Reputation may decrease from negative actions
- Reputation affects service access

### Player Interactions

- Players see reputation with each guild
- Players work to improve reputation
- Players benefit from high reputation

### System Requirements

- System must track reputation per guild per player
- System must calculate reputation changes
- System must unlock services based on reputation

### Dependencies

- **Guild Levels**: Reputation affects levels
- **Guild Services**: Reputation affects access

### Data Model Requirements

- Reputation tracking per guild
- Reputation change calculations

---

## Guild Levels

### Functional Description

Guild level progression determines service access. Levels increase based on reputation and other factors.

### Business Rules

- Guild levels range from 0 to maximum
- Levels increase based on reputation
- Special buildings may boost guild levels
- Higher levels unlock better services
- Levels are normalized/updated regularly

### Player Interactions

- Players see guild levels
- Players work to increase levels
- Players benefit from higher levels

### System Requirements

- System must track guild levels per player
- System must calculate level progression
- System must normalize levels regularly
- System must unlock services based on levels

### Dependencies

- **Guild Reputation**: Affects level progression
- **Building System**: Special buildings boost levels

### Data Model Requirements

- Guild level tracking
- Level progression calculations
- Level normalization logic

---

## Lottery

### Functional Description

Guild-run lottery system where players can purchase tickets for chances to win prizes.

### Business Rules

- Lotteries run periodically
- Players purchase lottery tickets
- Winners selected randomly
- Prizes vary by lottery
- Lottery access may require guild level

### Player Interactions

- Players purchase lottery tickets
- Players see lottery results
- Players claim prizes

### System Requirements

- System must track lottery tickets
- System must select winners randomly
- System must distribute prizes

### Dependencies

- **Economy System**: Handles ticket purchases and prizes

### Data Model Requirements

- Lottery ticket tracking
- Winner selection logic
- Prize distribution

---

## Artifact Valuation

### Functional Description

Dynamic artifact pricing system calculates artifact values based on market conditions, rarity, and other factors.

### Business Rules

- Artifact values calculated dynamically
- Values fluctuate based on market
- Rarity affects value
- Market conditions affect value
- Values update regularly

### Player Interactions

- Players see artifact values
- Players benefit from value changes
- Players use values for trading

### System Requirements

- System must calculate artifact values
- System must update values regularly
- System must consider multiple factors

### Dependencies

- **Artifact Market**: Uses values for trading

### Data Model Requirements

- Artifact value calculation formulas
- Value update logic

---

## Market Updates

### Functional Description

Regular market updates cause price fluctuations. Market conditions change over time affecting prices.

### Business Rules

- Markets update regularly (each turn or cycle)
- Prices fluctuate based on supply/demand
- Market updates affect all market prices
- Updates occur automatically
- Market conditions vary

### Player Interactions

- Players see price changes
- Players adapt to market conditions
- Players benefit from favorable markets

### System Requirements

- System must update markets regularly
- System must calculate price changes
- System must apply updates to all markets

### Dependencies

- **Artifact Market**: Markets update prices
- **Economy System**: Price changes affect economy

### Data Model Requirements

- Market update logic
- Price fluctuation calculations

---

## Alchemical Effects

### Functional Description

Temporary magical effects created through alchemy. Effects provide bonuses or special abilities for limited duration.

### Business Rules

- Alchemical effects are temporary
- Effects provide bonuses or abilities
- Effects have duration (time-limited)
- Effects can be created through alchemy tasks
- Effects may require resources

### Player Interactions

- Players create alchemical effects
- Players benefit from active effects
- Players see effect duration

### System Requirements

- System must track active alchemical effects
- System must apply effect bonuses
- System must handle effect expiration

### Dependencies

- **Guild System**: Alchemy through guilds
- **Bonus System**: Effects provide bonuses

### Data Model Requirements

- Alchemical effect tracking
- Effect duration management
- Effect bonus application

---

## Alchemical Cancellation

### Functional Description

Players can cancel active alchemical effects before they expire naturally.

### Business Rules

- Active effects can be cancelled
- Cancellation may have costs
- Cancellation is immediate
- Some effects may not be cancellable

### Player Interactions

- Players cancel unwanted effects
- Players pay cancellation costs (if any)
- Players see effect removal

### System Requirements

- System must support effect cancellation
- System must remove effects immediately
- System must handle cancellation costs

### Dependencies

- **Alchemical Effects**: Cancels active effects

### Data Model Requirements

- Effect cancellation logic

---

## Alchemical Duration

### Functional Description

Alchemical effects have time-limited duration. Effects expire automatically after duration ends.

### Business Rules

- Effects have defined duration
- Duration is tracked per effect
- Effects expire when duration ends
- Duration may be extended (if supported)
- Expired effects are removed automatically

### Player Interactions

- Players see effect duration
- Players know when effects expire
- Players may extend effects (if supported)

### System Requirements

- System must track effect duration
- System must decrement duration over time
- System must remove expired effects

### Dependencies

- **Alchemical Effects**: Tracks duration

### Data Model Requirements

- Duration tracking per effect
- Expiration handling logic

---

## Feature Interactions

### Internal Interactions

- **Guild Reputation** affects **Guild Levels**
- **Guild Levels** unlock **Guild Services**
- **Artifact Valuation** affects **Artifact Market** prices
- **Market Updates** change **Artifact Valuation**
- **Alchemical Duration** manages **Alchemical Effects**

### External System Interactions

- **Building System**: Special buildings boost guild levels
- **Economy System**: Handles banking, loans, and transactions
- **Artifact System**: Provides artifacts for market
- **Bonus System**: Alchemical effects provide bonuses
- **Message System**: Guild notifications

---

## Technical Considerations

### Performance Requirements

- Guild service processing must be efficient
- Market updates must be performant
- Interest calculations must be fast
- Artifact value calculations must be efficient

### Scalability Requirements

- System must support many players using guild services
- Market updates must scale with player count
- Bank account tracking must handle many accounts

### Data Persistence

- Guild levels and reputation must persist
- Bank accounts and loans must be saved
- Artifact market data must persist
- Alchemical effects must be saved

### Real-time Requirements

- Guild service access should be immediate
- Market updates occur per turn (not real-time)
- Interest payments occur per turn

### Validation Requirements

- All guild actions must validate guild level requirements
- Service access must validate reputation
- Transactions must validate funds availability

