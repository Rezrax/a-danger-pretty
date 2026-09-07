# Architectural Decisions

## ADR-001 — Backend Language
Java with Spring Boot.

## ADR-002 — Frontend
React with TypeScript.

TypeScript replaces the original JavaScript choice to align this project with the developer's professional work and deepen practical TypeScript experience.

## ADR-003 — Database
PostgreSQL.

## ADR-004 — Character Ownership
The GM creates and assigns exactly one character per player for the MVP. The GM account has no player character and uses a separate GM interface.

## ADR-005 — Message Visibility
The GM can read all player-to-player messages.

## ADR-006 — NPC Messaging
Players may message NPCs at any time.

## ADR-007 — Campaign Time
Campaign time will not be tracked in the MVP.
## ADR-008 — Player Onboarding and Credential Recovery
The GM creates player profiles, assigns characters, and preloads contacts. First use is Enter daily access code > Select Player > Select player name > Set password > Open character interface. New browsers/devices must enter the current daily four-character code (A-Z and 0-9) at the landing screen before profile selection. A successful entry issues a server-verifiable device-authorization cookie that bypasses this gate on later visits. Daily code rotation does not invalidate already authorized devices. Account passwords and GM authentication remain separate requirements. The current code is always visible in a corner of the GM panel and updates automatically when it rotates. Claimed profiles require their password; the GM can reset it. The GM has no player character and uses authenticated administrative access. This replaces the earlier player-created-account/character flow. Hashed credentials are reset, not retrieved.

## ADR-009 — Group Administration and History
Groups support PCs and NPCs as members and admins. Admins can rename groups, manage membership, transfer admin permissions, and share all earlier history. Removal revokes all group-history access. Rejoining starts fresh at the new join time with no inherited grants; earlier history requires sharing again.

## ADR-010 — Fictional Email
Players can choose predefined or custom fictional email domains. They learn addresses in person or from received mail and can email a known address without a managed contact entry. Only the GM changes contacts. The GM can conceal a sender address using an encrypted-address presentation; these emails are one-way, with reply and reply all unavailable and reply attempts rejected by the backend. Address selection timing remains open after the onboarding change. MVP email actions are compose, reply, and reply all; forward, drafts, BCC, archive, and deletion are outside the current MVP controls. Mail supports multiple recipients, CC, and threaded replies without real email delivery or real personal contact information.

## ADR-011 — Datashards and GM Tools
The authenticated GM/admin can list accounts and NPC identities and adopt a selected character's view and permissions, then return to administration. The selected perspective remains visible. Switching requires GM authority and does not require disclosing player credentials. The GM can see all NPCs, datashards, and conversations and create NPC-to-NPC conversations. GM edits update the shared plain-text datashard for all recipients who retain access without resetting read state. The GM can revoke access. Player deletion removes only that player's access; the document remains for the GM and other authorized recipients. The encryption minigame remains a post-MVP MVF.

## ADR-012 — Read State and Live Updates
Read state follows the selected perspective: opening content as an NPC affects only that NPC. Global inspection does not mark a group read for all NPCs. Opening content while adopting a PC perspective marks it read for that player, just as opening it as an NPC marks it read for that NPC. Global GM inspection without an adopted perspective changes neither. The GM can deliberately use this read-state change as an in-world indication of hacking; no hacking system is required. Connected recipients receive automatic updates; transport is undecided.

## ADR-013 — GM-Managed Contacts
Only the GM adds or removes contacts in MVP, including presets before first use. Player contact sharing is a very-low-priority post-MVP feature.

## ADR-014 — Daily Device Access Code
New browsers/devices must enter the current daily four-character code (A-Z and 0-9) at the landing screen before profile selection. A successful entry issues a server-verifiable device-authorization cookie that bypasses this gate on later visits. Daily code rotation does not invalidate already authorized devices. Account passwords and GM authentication remain separate requirements. The GM panel continuously shows the current code in a corner and updates at rotation. This supersedes the earlier no-gate decision. Rotate at midnight America/Chicago, following daylight-saving changes. Device authorization survives rotation and has no application-imposed expiry; browser cookie retention or deletion can still require reauthorization. This does not determine account-session lifetime.

## ADR-015 — Access Code Console Logging

The server logs the currently valid device access code to its console at startup and the new code whenever it rotates. The GM can use the console to authorize a first device before opening the GM panel. Logging at startup does not itself require a new code.
