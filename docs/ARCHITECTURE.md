# Cyberpunk TTRPG Web App — Architecture

## Overview

The Cyberpunk TTRPG Web App will use a conventional web application architecture:

```text
Browser / Mobile Browser
        |
        v
React Frontend
        |
        | HTTP / JSON API
        v
Spring Boot Backend
        |
        v
PostgreSQL Database
```

The application is intended to be hosted remotely so players can access it from their phones or computers through a normal web browser.

---

## Architectural Goals

The MVP architecture should prioritize:

- Simplicity
- Maintainability
- Clear separation between frontend and backend
- Mobile accessibility
- Reliable persistence
- Easy local development
- Straightforward future deployment

The architecture does not need to support large-scale multi-tenant usage during the MVP.

---

## Backend

### Technology

- Java
- Spring Boot

### Responsibilities

The backend will handle:

- Authentication and authorization
- User accounts
- Character ownership
- NPC data
- Messaging
- Datashards
- GM permissions
- Business rules
- Database access
- API endpoints

The backend should expose a JSON-based HTTP API for the frontend.

---

## Suggested Backend Structure

A conventional layered Spring Boot structure is appropriate.

Example:

```text
backend/
└── src/
    └── main/
        └── java/
            └── com/
                └── project/
                    ├── controller/
                    ├── service/
                    ├── repository/
                    ├── model/
                    ├── dto/
                    ├── config/
                    └── security/
```

### Controller Layer

Responsible for:

- Receiving HTTP requests
- Validating request structure
- Returning API responses
- Delegating business logic to services

Controllers should remain thin.

### Service Layer

Responsible for:

- Business rules
- Permission checks
- Messaging behavior
- GM actions
- Datashard distribution
- Coordination between repositories

### Repository Layer

Responsible for:

- Database access
- Entity persistence
- Queries

Spring Data JPA is a natural choice unless a later requirement justifies something else.

### Model / Entity Layer

Represents persisted domain objects such as:

- User
- Character
- NPC
- Message
- Datashard

Entity structure should remain minimal during the MVP.

### DTO Layer

DTOs should be used where API contracts should differ from persistence entities.

Avoid exposing database entities directly when doing so would create unnecessary coupling or leak internal fields.

---

## Frontend

### Technology

- React
- TypeScript
- Node.js tooling

### Responsibilities

The frontend will handle:

- Application navigation
- Authentication UI
- Mobile-first presentation
- Message views
- NPC interactions
- Datashard views
- GM interfaces
- In-world operating-system presentation

---

## Suggested Frontend Structure

Example:

```text
frontend/
├── src/
│   ├── components/
│   ├── pages/
│   ├── features/
│   ├── services/
│   ├── hooks/
│   ├── context/
│   ├── assets/
│   └── styles/
├── package.json
└── ...
```

The exact structure should be introduced gradually as features are implemented.

Avoid creating large abstraction hierarchies before they are needed.

---

## Frontend Communication with Backend

The React frontend will communicate with the Spring Boot backend using HTTP requests.

Typical API pattern:

```text
/api/auth/...
/api/users/...
/api/characters/...
/api/npcs/...
/api/messages/...
/api/datashards/...
```

Exact endpoint design should be created feature-by-feature.

JSON should be used as the default request and response format.

---

## Database

### Technology

PostgreSQL

### Responsibilities

PostgreSQL will persist application data including:

- Users
- Characters
- NPCs
- Messages
- Datashards
- Relationships between these entities

---

## Initial Domain Model

The exact schema should be finalized during implementation, but the MVP will likely include the following core concepts.

### User

Represents a person who can authenticate into the application.

MVP direction:

- The GM assigns each player one character. The GM account has no character and uses a separate GM interface.
- GM permissions may be represented by a role or equivalent authorization mechanism.

Avoid unnecessary fields such as `active` or `createdAt` unless a concrete feature requires them.

### Character

Represents the player's in-world character.

MVP direction:

- One character belongs to one user.
- Character data should remain lightweight.
- No Cyberpunk RED character sheet is required.

### NPC

Represents a GM-controlled in-world person or entity.

Players may send messages to NPCs.

The GM controls NPC responses.

### Message

Represents communication between characters and/or NPC identities.

A message will likely require concepts such as:

- Sender
- Recipient
- Content
- Message presentation type
- Read state follows the selected perspective: opening content as an NPC affects only that NPC. Global inspection does not mark a group read for all NPCs. Opening content while adopting a PC perspective marks it read for that player, just as opening it as an NPC marks it read for that NPC. Global GM inspection without an adopted perspective changes neither. The GM can deliberately use this read-state change as an in-world indication of hacking; no hacking system is required.

Message delivery is immediate in the MVP.

The application does not need campaign-clock scheduling. Groups support PCs and NPCs as members and admins. Admins can rename groups, manage membership, transfer admin permissions, and share all earlier history. Removal revokes all group-history access. Rejoining starts fresh at the new join time with no inherited grants; earlier history requires sharing again. Enforce access limits on API responses and live updates. The GM can create NPC-to-NPC conversations.

### Datashard

Represents an in-world document or information object.

A datashard may be visible to:

- One player
- Multiple players
- All players

The visibility implementation should use the simplest relationship that satisfies the feature.

---

## Authentication and Authorization

Authentication will be handled by the Spring Boot backend.

The exact authentication mechanism has not yet been finalized. The GM creates player profiles, assigns characters, and preloads contacts. First use is Enter daily access code > Select Player > Select player name > Set password > Open character interface. New browsers/devices must enter the current daily four-character code (A-Z and 0-9) at the landing screen before profile selection. A successful entry issues a server-verifiable device-authorization cookie that bypasses this gate on later visits. Daily code rotation does not invalidate already authorized devices. Account passwords and GM authentication remain separate requirements. The current code is always visible in a corner of the GM panel and updates automatically when it rotates. Claimed profiles require their password; the GM can reset it. The GM has no player character and uses authenticated administrative access. Store account credentials as hashes; the shared device code permits onboarding but does not identify an individual player. The authenticated GM/admin can list accounts and NPC identities and adopt a selected character's view and permissions, then return to administration. The selected perspective remains visible. Switching requires GM authority and does not require disclosing player credentials.

The authorization model must distinguish at minimum between:

- Regular players
- Game Master

### Player Permissions

Players should only be able to perform actions allowed to their own account and character.

### GM Permissions

The GM should be able to:

- Read all player-to-player messages
- Manage NPCs
- Send messages as NPCs
- Create datashards
- Control content distribution

Authorization rules should be enforced by the backend, not only hidden in the frontend.

---

## Messaging Architecture

Messaging is a central feature of the application.

The MVP requires automatic updates for connected recipients without manual refresh. The live-update transport has not been chosen.

The required behavior is:

```text
Frontend sends message
        |
        v
POST /api/messages
        |
        v
Backend validates sender and recipient
        |
        v
Message stored in PostgreSQL
        |
        v
Connected recipient sees message automatically
```

Choose an appropriate live-update mechanism during messaging implementation. Reconnection retrieves persisted messages; PostgreSQL remains the source of truth.

Do not introduce real-time infrastructure during Phase 0 unless it becomes necessary.

---

## Datashard Architecture

Datashards should be treated as persisted content objects.

GM edits update the shared plain-text datashard for all recipients who retain access without resetting read state. The GM can revoke access. Player deletion removes only that player's access; the document remains for the GM and other authorized recipients.

A separate recipient entity should only be created if the relational model genuinely needs it.

A direct many-to-many relationship may be sufficient for the MVP.

---

## API Design Principles

The API should:

- Use clear resource-oriented routes
- Return consistent JSON
- Use appropriate HTTP status codes
- Validate input on the backend
- Enforce permissions on the backend
- Avoid exposing unnecessary internal fields

Example:

```text
GET    /api/messages
POST   /api/messages
GET    /api/messages/{id}

GET    /api/npcs
POST   /api/npcs

GET    /api/datashards
POST   /api/datashards
```

Exact routes should be determined when each feature is implemented.

---

## Deployment Architecture

Deployment has not yet been selected.

The intended production model is:

```text
Custom Domain
     |
     v
Hosted Web Application
     |
     +--> React Frontend
     |
     +--> Spring Boot Backend
                |
                v
          PostgreSQL Database
```

The final application should eventually be reachable through a custom domain such as:

```text
https://ncagent.com
```

Potential hosting choices should be evaluated later based on:

- Cost
- Ease of deployment
- PostgreSQL support
- Java/Spring Boot support
- HTTPS
- Custom-domain support
- Backup options
- Maintenance requirements

No hosting provider should be treated as selected until explicitly decided.

---

## Development Environment

The project is expected to be developed using:

- VS Code
- Git
- GitHub
- Java development tooling
- Node.js
- PostgreSQL tooling

Local development will eventually require both frontend and backend processes.

Example future workflow:

```text
Terminal 1:
Run Spring Boot backend

Terminal 2:
Run React development server

Local PostgreSQL:
Run development database
```

Exact commands will depend on the project scaffolding chosen later.

---

## Repository Structure

The repository is currently in Phase 0 and should remain simple.

A likely future structure is:

```text
cyberpunk-ttrpg/
├── README.md
├── AGENTS.md
├── docs/
│   ├── PROJECT_CONTEXT.md
│   ├── ARCHITECTURE.md
│   └── DECISIONS.md
├── backend/
├── frontend/
└── .gitignore
```

This structure is directional rather than mandatory.

Do not create empty folders solely to match the diagram before the relevant project components are initialized.

---

## Phase 0 Architecture Status

Currently decided:

- Backend: Java with Spring Boot
- Frontend: React with TypeScript
- Frontend tooling: Node.js
- Database: PostgreSQL
- Primary target: mobile browser
- Desktop browser support: yes
- Deployment: hosted web application
- Custom domain: eventual goal
- Specific host: undecided

Still to be decided during later setup:

- Java version
- Spring Boot version
- React build tooling
- Authentication implementation
- Database migration tool
- Local development strategy
- Production hosting provider
- CI/CD workflow
- Production secrets management

These decisions should be made only when the project reaches the stage where they are needed.

---

## Architecture Principles

1. Keep the MVP small.
2. Prefer conventional technologies over custom infrastructure.
3. Keep frontend and backend responsibilities clearly separated.
4. Enforce permissions on the backend.
5. Avoid premature abstraction.
6. Avoid premature optimization.
7. Avoid infrastructure that does not yet solve a real requirement.
8. Document decisions that materially affect future development.
9. Keep mobile usability as a first-class requirement.
10. Treat PostgreSQL as the authoritative persistent data store.

## Email Addresses and Contacts

Players can choose predefined or custom fictional email domains. They learn addresses in person or from received mail and can email a known address without a managed contact entry. Only the GM changes contacts. The GM can conceal a sender address using an encrypted-address presentation; these emails are one-way, with reply and reply all unavailable and reply attempts rejected by the backend. Concealed addresses must not leak through player API responses, thread metadata, or reply controls. Address discovery does not grant contact-management permissions.

## Device Authorization

The daily access code is checked by the backend before player profile discovery/onboarding. On success, issue a persistent Secure, HttpOnly cookie with an appropriate SameSite policy containing a server-verifiable token, not the daily code or a client-controlled authorized flag. Token storage/signing details are not selected yet. Keep this authorization separate from the account session and enforce both where required.

Generate the daily A-Z/0-9 code on the server, rate-limit verification attempts, and restrict retrieval of the active code to authenticated GM access. The GM panel displays it continuously and refreshes automatically at rotation. Daily rotation uses real-world time and preserves valid device authorizations. Log the currently valid code to the server console at startup and log the newly active code on every rotation. This gives the GM access to the code before authorizing their first browser. Startup logging does not itself trigger an additional rotation. Rotate at midnight America/Chicago using timezone-aware calendar boundaries rather than a fixed 24-hour interval. Device authorization has no application-imposed expiry; browser cookie retention limits or deletion can still require reauthorization. Account-session expiry is separate. Any administrative device-revocation mechanism remains to be defined during implementation.
