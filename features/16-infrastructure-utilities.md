# Infrastructure & Utilities

## Overview

The Infrastructure & Utilities System provides core server infrastructure, configuration management, database connectivity, logging, error handling, messaging, and administrative tools. This system supports all other game systems and provides essential services for game operation.

## Feature List

1. [Multi-Server Support](#multi-server-support)
2. [Configuration Files](#configuration-files)
3. [Database Connection](#database-connection)
4. [Logging System](#logging-system)
5. [Error Handling](#error-handling)
6. [Message System](#message-system)
7. [Gazette System](#gazette-system)
8. [Shadow Log](#shadow-log)
9. [Chronicles](#chronicles)
10. [Rank System](#rank-system)
11. [Reputation System](#reputation-system)
12. [Database Dumps](#database-dumps)
13. [Server Tools](#server-tools)
14. [Map Tools](#map-tools)
15. [Image Generation](#image-generation)

---

## Multi-Server Support

### Functional Description

Support for multiple server configurations. System can run different server instances with different configurations.

### Business Rules

- Multiple server configurations supported
- Each server has its own configuration
- Server configurations are stored separately
- Server parameters are managed per instance
- Servers can run independently

### Player Interactions

- Players connect to specific servers
- Players see server-specific content

### System Requirements

- System must support multiple server instances
- System must manage server configurations
- System must isolate server data

### Dependencies

- **Configuration Files**: Provides server configs
- **Database Connection**: Per-server connections

### Data Model Requirements

- Server configuration storage
- Server parameter management

---

## Configuration Files

### Functional Description

Configuration system for server settings. Configurations define server parameters and behavior.

### Business Rules

- Configurations stored in files (INI or JSON)
- Configurations define server parameters
- Configurations are loaded at startup
- Configurations can be modified
- Configurations affect server behavior

### Player Interactions

- Administrators manage configurations
- Players are affected by configurations

### System Requirements

- System must load configurations
- System must parse configuration files
- System must apply configurations

### Dependencies

- **Multi-Server Support**: Configurations per server
- **Server Tools**: Manages configurations

### Data Model Requirements

- Configuration file format
- Configuration parsing logic

---

## Database Connection

### Functional Description

Database connectivity for data persistence. System connects to database for all data operations.

### Business Rules

- Database connection is established at startup
- Connection is maintained during operation
- Connection handles all data operations
- Connection may use ORM or direct SQL
- Connection supports transactions

### Player Interactions

- Players benefit from data persistence
- Players see data saved automatically

### System Requirements

- System must establish database connections
- System must handle connection failures
- System must support data operations

### Dependencies

- **All Systems**: Use database for persistence

### Data Model Requirements

- Database connection management
- Connection pooling (if supported)

---

## Logging System

### Functional Description

Comprehensive logging system for debugging and monitoring. Logs record system events and errors.

### Business Rules

- Logging records system events
- Logs are written to files
- Logs include errors and information
- Logs can be filtered by level
- Logs are stored in logs directory

### Player Interactions

- Administrators view logs
- Logs help diagnose issues

### System Requirements

- System must write logs
- System must manage log files
- System must support log levels

### Dependencies

- **Error Handling**: Logs errors
- **All Systems**: Generate log entries

### Data Model Requirements

- Log file management
- Log format definitions

---

## Error Handling

### Functional Description

Error handling and reporting system. System handles errors gracefully and reports issues.

### Business Rules

- Errors are caught and handled
- Errors are logged
- Errors may trigger safe mode
- Error handling prevents crashes
- Errors are reported to administrators

### Player Interactions

- Players see error messages (if appropriate)
- Administrators see error reports

### System Requirements

- System must catch errors
- System must handle errors gracefully
- System must report errors

### Dependencies

- **Logging System**: Logs errors
- **All Systems**: May generate errors

### Data Model Requirements

- Error handling logic
- Error reporting mechanisms

---

## Message System

### Functional Description

In-game messaging system for player communication. Messages are generated for events and player actions.

### Business Rules

- Messages are created for events
- Messages are stored in message system
- Messages are delivered to players
- Messages can be formatted with templates
- Messages include event information

### Player Interactions

- Players receive messages
- Players read messages
- Players see event notifications

### System Requirements

- System must create messages
- System must store messages
- System must deliver messages

### Dependencies

- **Event System**: Generates messages
- **All Systems**: Create messages

### Data Model Requirements

- Message storage
- Message delivery logic

---

## Gazette System

### Functional Description

News and announcements system. Gazette provides public information and news to all players.

### Business Rules

- Gazette entries are public announcements
- Entries are added by AddEncartGazette()
- Entries are stored in ENCARTS_GAZETTE table
- Entries are visible to all players
- Entries may be time-limited

### Player Interactions

- Players read gazette
- Players see announcements
- Players stay informed

### System Requirements

- System must store gazette entries
- System must display gazette
- System must manage entry lifecycle

### Dependencies

- **Message System**: Gazette is public messaging

### Data Model Requirements

- Gazette entry storage
- Entry management logic

---

## Shadow Log

### Functional Description

Secret log of player actions. Shadow log records sensitive actions for administrative review.

### Business Rules

- Shadow log records secret actions
- Log entries are stored in LOG_OMBRE table
- Log is accessible to administrators
- Log records sensitive operations
- Log is separate from regular logs

### Player Interactions

- Administrators view shadow log
- Players' actions are logged secretly

### System Requirements

- System must record shadow log entries
- System must store shadow log
- System must provide admin access

### Dependencies

- **Military System**: Logs military actions
- **Diplomacy System**: Logs diplomatic actions

### Data Model Requirements

- Shadow log storage
- Log entry recording logic

---

## Chronicles

### Functional Description

Historical record of fief events. Chronicles provide narrative history of player actions.

### Business Rules

- Chronicles record fief events
- Entries are stored in HISTOIRE table
- Chronicles are generated by chroniclesLog()
- Chronicles provide historical narrative
- Chronicles are visible to players

### Player Interactions

- Players read chronicles
- Players see fief history
- Players track events

### System Requirements

- System must generate chronicle entries
- System must store chronicles
- System must display chronicles

### Dependencies

- **Event System**: Events generate chronicles
- **All Systems**: May generate chronicle entries

### Data Model Requirements

- Chronicle storage
- Chronicle generation logic

---

## Rank System

### Functional Description

Player rank and title system. Ranks affect player status and capabilities.

### Business Rules

- Players have ranks/titles
- Ranks are stored in rang field
- Ranks are calculated by getRang()
- Ranks increase through achievements
- Ranks affect player status

### Player Interactions

- Players see their rank
- Players work to increase rank
- Players benefit from higher rank

### System Requirements

- System must track player ranks
- System must calculate rank levels
- System must apply rank effects

### Dependencies

- **Research System**: Research increases rank
- **All Systems**: May affect rank

### Data Model Requirements

- Rank tracking
- Rank calculation logic

---

## Reputation System

### Functional Description

Reputation tracking and effects. Reputation affects various game mechanics and player status.

### Business Rules

- Reputation is stored in reputation field
- Reputation affects economic opportunities
- Reputation affects guild services
- Reputation is managed by reputation system
- Reputation changes from various actions

### Player Interactions

- Players see reputation
- Players work to improve reputation
- Players benefit from high reputation

### System Requirements

- System must track reputation
- System must calculate reputation changes
- System must apply reputation effects

### Dependencies

- **All Systems**: May affect reputation

### Data Model Requirements

- Reputation tracking
- Reputation calculation logic

---

## Database Dumps

### Functional Description

Database backup and restore tools. Enables data backup and recovery.

### Business Rules

- Database can be dumped to files
- Dumps can be restored
- Dumps preserve game state
- Dumps are used for backups
- Dumps can be used for migration

### Player Interactions

- Administrators create dumps
- Administrators restore dumps

### System Requirements

- System must support database dumps
- System must support restore operations
- System must handle dump files

### Dependencies

- **Database Connection**: Dumps database

### Data Model Requirements

- Dump file format
- Restore logic

---

## Server Tools

### Functional Description

Various server administration tools. Tools provide administrative functions for server management.

### Business Rules

- Server tools provide admin functions
- Tools are used by administrators
- Tools support server management
- Tools may have security restrictions
- Tools are accessible through admin interface

### Player Interactions

- Administrators use tools
- Tools support server operation

### System Requirements

- System must provide server tools
- System must secure tool access
- System must support tool operations

### Dependencies

- **All Systems**: Tools manage systems

### Data Model Requirements

- Tool definitions
- Tool access control

---

## Map Tools

### Functional Description

Map generation and manipulation tools. Tools support map creation and modification.

### Business Rules

- Map tools generate maps
- Tools manipulate map data
- Tools support map editing
- Tools are used by administrators
- Tools handle map files

### Player Interactions

- Administrators use map tools
- Tools create game world

### System Requirements

- System must support map generation
- System must handle map manipulation
- System must manage map files

### Dependencies

- **Map System**: Tools manipulate maps

### Data Model Requirements

- Map tool definitions
- Map file handling

---

## Image Generation

### Functional Description

Automatic image generation for units and other game elements. Images are generated dynamically.

### Business Rules

- Images are generated automatically
- Unit images are created from composition
- Images are stored in pics directory
- Image generation uses batch processing
- Images support game visualization

### Player Interactions

- Players see generated images
- Images represent game elements

### System Requirements

- System must generate images
- System must handle image processing
- System must store images

### Dependencies

- **Military System**: Generates unit images
- **All Systems**: May need images

### Data Model Requirements

- Image generation logic
- Image storage management

---

## Feature Interactions

### Internal Interactions

- **Multi-Server Support** uses **Configuration Files**
- **Database Connection** enables **Database Dumps**
- **Logging System** records **Error Handling**
- **Message System** delivers **Gazette System** content
- **Rank System** and **Reputation System** affect all game systems

### External System Interactions

- **All Systems**: Use infrastructure services
- **All Systems**: Generate logs and messages
- **All Systems**: May affect rank and reputation

---

## Technical Considerations

### Performance Requirements

- Database operations must be efficient
- Logging must not impact performance
- Message delivery must be fast

### Scalability Requirements

- Infrastructure must scale with player count
- Database must handle many connections
- Logging must handle high volume

### Data Persistence

- All data must persist through database
- Logs must be saved
- Configurations must persist

### Real-time Requirements

- Messages should be delivered promptly
- Logs should be written immediately
- Errors should be handled immediately

### Validation Requirements

- All configurations must be validated
- Database operations must be validated
- Tool access must be secured

