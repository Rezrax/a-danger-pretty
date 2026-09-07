# Cyberpunk TTRPG Web App — Project Context

## Project Purpose

The Cyberpunk TTRPG Web App is a private web application intended to support a Cyberpunk RED tabletop role-playing campaign.

The application should feel like an in-world digital operating system that players can access from their phones or desktop browsers. It is not intended to replace the Cyberpunk RED character sheet or the tabletop game itself. Its purpose is to provide immersive communication, information delivery, and GM-controlled digital content.

The initial version is being developed for a single private campaign and is not intended as a public commercial platform.

---

## Core Product Concept

The application is structured as a collection of in-world apps presented through a unified interface.

Examples include:

- Messages
- Text-style conversations
- Email-style conversations
- Datashards
- GM-delivered information
- NPC communications

The interface should support the feeling that players are using a device or operating system inside the game world rather than simply viewing a generic campaign-management website.

---

## Primary Users

### Players

Players should be able to:

- Log in to their account.
- Access their associated character.
- Send messages to other player characters.
- Send messages to NPCs.
- Receive messages from player characters and NPCs.
- Read datashards that have been made available to them.
- Use the application primarily from a mobile device.

### Game Master

The GM should be able to:

- View all player-to-player messages.
- View player-to-NPC messages.
- Send messages as NPCs.
- Create NPC identities.
- Deliver information to players.
- Create and distribute datashards.
- Broadcast content when needed.

The GM acts as the controlling authority for in-world digital information.

---

## MVP Scope

The MVP is intentionally limited.

### Included

- User accounts
- One character per user
- One campaign
- Player-to-player messaging
- Player-to-NPC messaging
- NPC-to-player messaging controlled by the GM
- Instant message delivery
- GM visibility into all player-to-player messages
- Datashards
- Mobile-first interface
- Desktop browser support
- Unified in-world operating-system-style interface

### Not Included in the MVP

- Multiple campaigns
- Multiple characters per user
- Cyberpunk RED character sheets
- Campaign time tracking
- Scheduled message delivery
- Delayed message delivery
- Player-created profiles; first-use claiming of GM-created profiles is included
- Public-facing campaign websites
- General-purpose web pages
- Advanced campaign management
- Commercial multi-tenant support

These features may be reconsidered after the MVP is complete.

---

## Messaging Rules

### Player-to-Player Messaging

Players may send messages directly to other player characters.

Messages are delivered immediately and appear automatically for connected recipients without manual refresh.

The GM can read all player-to-player messages.

### Player-to-NPC Messaging

Players may message NPCs at any time.

NPC responses are controlled by the GM.

NPCs are not autonomous AI agents in the MVP.

### Groups and Read State

Groups support PCs and NPCs as members and admins. Admins can rename groups, manage membership, transfer admin permissions, and share all earlier history. Removal revokes all group-history access. Rejoining starts fresh at the new join time with no inherited grants; earlier history requires sharing again.

Read state follows the selected perspective: opening content as an NPC affects only that NPC. Global inspection does not mark a group read for all NPCs. Opening content while adopting a PC perspective marks it read for that player, just as opening it as an NPC marks it read for that NPC. Global GM inspection without an adopted perspective changes neither. The GM can deliberately use this read-state change as an in-world indication of hacking; no hacking system is required. The authenticated GM/admin can list accounts and NPC identities and adopt a selected character's view and permissions, then return to administration. The selected perspective remains visible. Switching requires GM authority and does not require disclosing player credentials.

Only the GM adds or removes contacts in MVP, including presets before first login. Player contact sharing is a very-low-priority post-MVP feature.

### Message Types

The interface may represent communications using different in-world presentation styles, including:

- Text messages
- Emails

Mail supports fictional character email addresses, multiple recipients, CC, and replies grouped into conversations. MVP actions are compose, reply, and reply all; forward, drafts, BCC, archive, and deletion are outside the current MVP controls. These apps may share underlying infrastructure while appearing differently in the user interface.

---

## Character Model

For the MVP:

- The GM creates player profiles, assigns characters, and preloads contacts. First use is Enter daily access code > Select Player > Select player name > Set password > Open character interface. New browsers/devices must enter the current daily four-character code (A-Z and 0-9) at the landing screen before profile selection. A successful entry issues a server-verifiable device-authorization cookie that bypasses this gate on later visits. Daily code rotation does not invalidate already authorized devices. Account passwords and GM authentication remain separate requirements. The current code is always visible in a corner of the GM panel and updates automatically when it rotates. Claimed profiles require their password; the GM can reset it. The GM has no player character and uses authenticated administrative access.
- Each character belongs to the single campaign.
- Character data exists primarily to identify the player inside the application's fictional world.
- The application does not include a full Cyberpunk RED character sheet.

Players can choose predefined or custom fictional email domains. They learn addresses in person or from received mail and can email a known address without a managed contact entry. Only the GM changes contacts. The GM can conceal a sender address using an encrypted-address presentation; these emails are one-way, with reply and reply all unavailable and reply attempts rejected by the backend. Address selection timing in onboarding remains open. No real email, phone, or portraits are required.

---

## NPC Model

NPCs are GM-controlled identities that players can interact with.

NPCs may:

- Send messages
- Receive messages
- Represent fictional contacts, organizations, or individuals

NPCs do not require autonomous behavior.

Portraits and real-world contact details are not required. NPC fictional email-address setup will be defined with Mail.

---

## Identity Concept

The application may distinguish between an underlying character or NPC and the identity presented inside a specific communication channel.

This concept should remain simple during the MVP.

Avoid adding identity abstractions unless they are required by an implemented feature.

---

## Datashards

Datashards are in-world documents or information drops that the GM can provide to players.

They serve the role that news articles, files, lore entries, mission information, or found digital documents might otherwise serve.

GM edits update the shared plain-text datashard for all recipients who retain access without resetting read state. The GM can revoke access. Player deletion removes only that player's access; the document remains for the GM and other authorized recipients. The encryption minigame remains a post-MVP MVF in mvp-backlog.md.

Previously considered fields such as:

- createdBy
- createdAt
- status

are not required unless implementation needs later justify them.

A dedicated DatashardRecipient entity may also be unnecessary if a simpler relationship can represent visibility.

---

## Web Pages

A general in-world web-page system is not part of the MVP.

The initial application should focus on messaging and datashards before expanding into broader fictional internet functionality.

---

## Time Model

Campaign time is not tracked by the application in the MVP.

Messages are treated as immediately delivered.

No simulated delay, scheduling, or historical campaign-clock system is required.

---

## Mobile-First Requirement

The application is expected to be used primarily from players' phones during or around game sessions.

The UI should therefore be designed mobile-first.

Desktop access should still work well, but desktop-only navigation patterns should be avoided.

For example, large horizontal tab bars that work well on desktop may not be appropriate as the primary navigation model on mobile.

---

## User Experience Direction

The application should feel like a cohesive fictional operating system with multiple apps rather than a collection of unrelated pages.

The interface should prioritize:

- Fast access
- Clear navigation
- Good mobile usability
- In-world immersion
- Minimal friction during a tabletop session

Visual complexity should not interfere with usability.

---

## Development Philosophy

Development should proceed incrementally.

Priorities:

1. Build the smallest useful version of each feature.
2. Avoid designing for hypothetical future scale before it is needed.
3. Prefer simple data models.
4. Keep MVP scope controlled.
5. Document architectural decisions when they materially affect future work.
6. Avoid silently introducing requirements that have not been discussed.
7. Treat the repository as the source of truth for what has actually been implemented.

---

## Current Development Phase

The project is currently in Phase 0 / project setup.

At the time this context was established, the repository contained:

- `.gitignore`
- `README.md`

The core stack has been selected, but the application structure has not yet been fully implemented.

---

## Current Technology Decisions

### Backend

Java with Spring Boot

### Frontend

React with TypeScript

### Frontend Tooling

Node.js for:

- Package management
- Development tooling
- Frontend builds

### Database

PostgreSQL

### Deployment

Deployment has not yet been finalized.

The intended end state is a publicly reachable web application hosted on the internet and accessible through a custom domain such as:

- `ncagent.com`

The specific hosting provider, infrastructure, CI/CD workflow, and production architecture will be selected later.

---

## Source of Truth

Long-term project knowledge should be stored in the repository rather than relying only on chat history.

Recommended documentation roles:

- `README.md` — developer-facing overview and setup instructions
- `PROJECT_CONTEXT.md` — product goals, scope, and gameplay behavior
- `ARCHITECTURE.md` — technical structure and implementation direction
- `DECISIONS.md` — durable architectural and product decisions
- `AGENTS.md` — instructions and project context for coding agents

These documents should be updated as major decisions change.

## Access Code Console Logging

The server logs the currently valid device access code to its console at startup and the new code whenever it rotates. The GM can use the console to authorize a first device before opening the GM panel. Logging at startup does not itself require a new code.

## Device Authorization Duration

The access code rotates at midnight America/Chicago, following local calendar days and daylight-saving changes. Device authorization has no application-imposed expiry and survives daily rotation. Browser cookie loss or deletion requires the current code again. Account authentication and session lifetime are separate.
