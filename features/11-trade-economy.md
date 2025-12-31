# Trade & Economy

## Overview

The Trade & Economy System manages currency, resource trading, market prices, inventory, trade routes, convoys, banking, loans, and taxes. The system includes dynamic pricing, supply/demand mechanics, guild commerce, and economic interactions between players.

## Feature List

1. [Currency System](#currency-system)
2. [Resource Trading](#resource-trading)
3. [Market Prices](#market-prices)
4. [Price Fluctuations](#price-fluctuations)
5. [Stock Management](#stock-management)
6. [Guild Commerce](#guild-commerce)
7. [Market Updates](#market-updates)
8. [Trade Routes](#trade-routes)
9. [Convoys](#convoys)
10. [Black Market](#black-market)
11. [Interest System](#interest-system)
12. [Loan System](#loan-system)
13. [Tax System](#tax-system)
14. [Reputation Effects](#reputation-effects)

---

## Currency System

### Functional Description

Gold/écus currency system for economic transactions. Currency is stored in village treasury and used for purchases, payments, and transactions.

### Business Rules

- Currency is stored in village treasury (tresor field)
- Currency is used for all economic transactions
- Currency can be earned through production, trade, taxes
- Currency can be spent on construction, research, maintenance
- Treasury is managed by handleTresor()

### Player Interactions

- Players see treasury balance
- Players spend currency on actions
- Players earn currency from various sources

### System Requirements

- System must track currency per village
- System must handle currency transactions
- System must validate currency availability

### Dependencies

- **Economy System**: Core currency mechanics
- **Tax System**: Provides currency income

### Data Model Requirements

- Currency storage (treasury)
- Transaction tracking

---

## Resource Trading

### Functional Description

Trading of various resources between players. Resources can be exchanged for currency or other resources.

### Business Rules

- Resources can be traded between players
- Trading requires diplomatic permission
- Trading may have restrictions based on relations
- Resources are stored in inventory
- Trading affects resource availability

### Player Interactions

- Players initiate trades
- Players negotiate trade terms
- Players exchange resources

### System Requirements

- System must support trade transactions
- System must validate trade permissions
- System must handle resource exchange

### Dependencies

- **Inventory System**: Stores resources
- **Diplomacy System**: Affects trade permissions

### Data Model Requirements

- Trade transaction tracking
- Resource exchange logic

---

## Market Prices

### Functional Description

Dynamic market prices for resources. Prices fluctuate based on supply, demand, and market conditions.

### Business Rules

- Prices are calculated dynamically
- Prices vary by resource type
- Prices are updated regularly
- Prices affect trade decisions
- Prices are managed by updateCours()

### Player Interactions

- Players see market prices
- Players make trading decisions based on prices
- Players benefit from favorable prices

### System Requirements

- System must calculate market prices
- System must update prices regularly
- System must support price queries

### Dependencies

- **Market Updates**: Updates prices
- **Price Fluctuations**: Prices change

### Data Model Requirements

- Price calculation formulas
- Price data storage

---

## Price Fluctuations

### Functional Description

Prices change based on supply/demand. Market conditions cause price variations.

### Business Rules

- Prices fluctuate based on supply/demand
- High supply reduces prices
- High demand increases prices
- Fluctuations occur regularly
- Fluctuations affect all markets

### Player Interactions

- Players see price changes
- Players adapt to price fluctuations
- Players benefit from favorable fluctuations

### System Requirements

- System must calculate supply/demand
- System must apply fluctuations
- System must update prices

### Dependencies

- **Market Prices**: Prices fluctuate
- **Market Updates**: Applies fluctuations

### Data Model Requirements

- Supply/demand calculations
- Fluctuation formulas

---

## Stock Management

### Functional Description

Inventory management system tracks player resources. Stocks are stored and managed per player.

### Business Rules

- Resources are stored in inventory
- Inventory tracks quantities per resource type
- Inventory is managed by addEntreeStocks()
- Inventory supports getVal() and setVal() operations
- Inventory limits may exist

### Player Interactions

- Players see inventory
- Players manage resources
- Players track stock levels

### System Requirements

- System must track inventory per player
- System must support inventory operations
- System must handle inventory limits

### Dependencies

- **Resource System**: Defines resource types
- **Production System**: Adds to inventory

### Data Model Requirements

- Inventory data structure
- Inventory operation logic

---

## Guild Commerce

### Functional Description

Trade through guilds provides commercial services. Commerce guild facilitates trading.

### Business Rules

- Commerce guild provides trading services
- Guild level affects commerce capabilities
- Commerce is handled by processGuildeTask()
- Guild commerce may have fees
- Guild commerce provides safe trading

### Player Interactions

- Players use guild commerce
- Players see guild commerce options
- Players benefit from guild services

### System Requirements

- System must support guild commerce
- System must handle commerce transactions
- System must apply guild fees

### Dependencies

- **Guild System**: Provides commerce services
- **Trade System**: Uses commerce

### Data Model Requirements

- Commerce transaction tracking
- Guild commerce logic

---

## Market Updates

### Functional Description

Regular market price updates. Markets are updated periodically to reflect current conditions.

### Business Rules

- Markets update regularly (each turn or cycle)
- Updates recalculate prices
- Updates occur in server loop
- Updates affect all markets
- Updates are automatic

### Player Interactions

- Players see market updates
- Players adapt to price changes

### System Requirements

- System must update markets regularly
- System must recalculate prices
- System must apply updates

### Dependencies

- **Market Prices**: Updates prices
- **Price Fluctuations**: Applies fluctuations

### Data Model Requirements

- Market update logic
- Update scheduling

---

## Trade Routes

### Functional Description

Trade route system establishes commercial connections. Routes enable resource transport between locations.

### Business Rules

- Trade routes connect locations
- Routes enable resource transport
- Routes may require maintenance
- Routes are tracked in ARMEES table
- Routes may be protected

### Player Interactions

- Players establish trade routes
- Players see route status
- Players protect routes

### System Requirements

- System must track trade routes
- System must handle route transport
- System must support route protection

### Dependencies

- **Military System**: Routes tracked as actions
- **Trade System**: Routes enable trade

### Data Model Requirements

- Trade route tracking
- Route transport logic

---

## Convoys

### Functional Description

Trade convoy system transports resources. Convoys move resources between locations with military escort.

### Business Rules

- Convoys transport resources
- Convoys are tracked as actions (CONVOI-%)
- Convoys may have escorts
- Convoys can be attacked
- Convoys complete when reaching destination

### Player Interactions

- Players create convoys
- Players escort convoys
- Players protect convoys

### System Requirements

- System must track convoys
- System must handle convoy movement
- System must support convoy protection

### Dependencies

- **Military System**: Convoys are military actions
- **Trade System**: Convoys transport resources

### Data Model Requirements

- Convoy tracking
- Convoy movement logic

---

## Black Market

### Functional Description

Black market trading through shadow guild. Provides access to restricted goods and services.

### Business Rules

- Black market accessed through shadow guild
- Black market offers restricted items
- Black market prices may be higher
- Black market access requires guild level
- Black market operations are secret

### Player Interactions

- Players access black market
- Players buy restricted goods
- Players see black market offerings

### System Requirements

- System must provide black market access
- System must track black market inventory
- System must handle black market transactions

### Dependencies

- **Shadow Guild**: Provides black market
- **Trade System**: Black market is trade variant

### Data Model Requirements

- Black market inventory
- Black market transaction tracking

---

## Interest System

### Functional Description

Bank interest on deposits. Players earn interest on money deposited in banks.

### Business Rules

- Interest is calculated on deposits
- Interest rate is configurable (BANQUE_TAUX_INTERET)
- Interest is paid regularly
- Interest compounds over time
- Interest is handled by processGuildeTask()

### Player Interactions

- Players deposit money in banks
- Players receive interest payments
- Players see interest earnings

### System Requirements

- System must calculate interest
- System must pay interest regularly
- System must track deposits

### Dependencies

- **Banking System**: Provides interest
- **Currency System**: Interest paid in currency

### Data Model Requirements

- Interest calculation formulas
- Deposit tracking

---

## Loan System

### Functional Description

Loan and debt system. Players can borrow money with repayment obligations.

### Business Rules

- Players can take loans
- Loans have repayment schedules
- Loans accrue interest
- Default on loans may have penalties
- Loans are handled by processGuildeTask()

### Player Interactions

- Players request loans
- Players make loan repayments
- Players see loan balances

### System Requirements

- System must track loans
- System must calculate repayments
- System must handle loan defaults

### Dependencies

- **Banking System**: Provides loans
- **Currency System**: Loans use currency

### Data Model Requirements

- Loan tracking
- Repayment schedule calculations

---

## Tax System

### Functional Description

Tax collection from population. Taxes provide currency income to players.

### Business Rules

- Taxes are collected from population
- Tax rate is stored in taxe field
- Taxes are collected by handleTresor()
- Tax collection uses getBonus(joueur, "TAXE_ACC") for bonuses
- Taxes provide regular income

### Player Interactions

- Players set tax rates
- Players receive tax income
- Players see tax collections

### System Requirements

- System must collect taxes regularly
- System must calculate tax amounts
- System must apply tax bonuses

### Dependencies

- **Population System**: Provides tax base
- **Currency System**: Taxes provide currency
- **Bonus System**: Tax bonuses affect collection

### Data Model Requirements

- Tax calculation formulas
- Tax collection logic

---

## Reputation Effects

### Functional Description

Reputation affects economic opportunities. Higher reputation provides economic benefits.

### Business Rules

- Reputation affects guild services
- Reputation affects market income
- Higher reputation provides better opportunities
- Reputation affects trade permissions
- Reputation is stored in reputation field

### Player Interactions

- Players see reputation effects
- Players benefit from high reputation
- Players work to improve reputation

### System Requirements

- System must apply reputation effects
- System must calculate reputation bonuses
- System must track reputation

### Dependencies

- **Reputation System**: Provides reputation
- **Guild System**: Reputation affects services
- **Market System**: Reputation affects income

### Data Model Requirements

- Reputation effect calculations
- Reputation bonus definitions

---

## Feature Interactions

### Internal Interactions

- **Currency System** enables **Resource Trading**
- **Market Prices** affect **Price Fluctuations**
- **Stock Management** tracks **Resource Trading**
- **Guild Commerce** uses **Market Prices**
- **Tax System** provides **Currency System** income

### External System Interactions

- **Guild System**: Provides commerce and banking services
- **Diplomacy System**: Affects trade permissions
- **Military System**: Protects trade routes and convoys
- **Production System**: Provides resources for trade
- **Reputation System**: Affects economic opportunities
- **Population System**: Provides tax base

---

## Technical Considerations

### Performance Requirements

- Market price calculations must be efficient
- Trade transactions must be fast
- Inventory operations must be performant

### Scalability Requirements

- System must support many concurrent trades
- Market updates must scale with player count
- Inventory tracking must be efficient

### Data Persistence

- Currency data must persist
- Trade history must be saved
- Inventory data must persist
- Loan data must be saved

### Real-time Requirements

- Market updates occur per turn
- Tax collection occurs per turn
- Interest payments occur per turn

### Validation Requirements

- All trade actions must validate permissions
- Currency transactions must validate funds
- Inventory operations must validate availability

