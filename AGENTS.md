# Cyberpunk TTRPG Web App

## Purpose

Private web application for a Cyberpunk RED tabletop campaign.

The application represents an in-world operating system that players
interact with primarily from their phones.

## Technology

Backend:
- Java
- Spring Boot

Frontend:
- React
- TypeScript
- Node.js tooling

Database:
- PostgreSQL

Deployment:
- Web-hosted application
- Eventually accessible through a custom domain such as ncagent.com

## MVP

- Daily four-character A-Z/0-9 device access code; persistent authorization cookie; current code always visible in GM panel
- GM-created profiles; players select their name and set a password on first use
- One character per player; GM account has no player character
- One campaign
- Player-to-player messages
- Player-to-NPC messages
- GM-controlled NPC responses and NPC-to-NPC conversations
- Player-created groups with transferable group-admin permissions and controlled history sharing
- Fictional email addresses with predefined/custom domains and GM-obfuscated senders; no real email or phone required
- GM can read all messages
- Messages are delivered instantly
- Shared plain-text datashards with GM edits/revocation and per-player deletion
- GM-managed contacts; player contact sharing deferred
- GM can adopt individual account/character perspectives
- Primarily mobile interface
- Desktop supported
- No character sheet
- No campaign time tracking
- No web-page system in MVP

## Development Philosophy

Build the project incrementally.

Do not implement functionality outside the current development phase
unless specifically requested.

Prefer simple implementations appropriate for the MVP over abstractions
for hypothetical future functionality.

Before making major architectural decisions, explain the proposed
approach and tradeoffs.

Do not silently change previously established requirements.