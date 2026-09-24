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
The GM creates player profiles, assigns characters, and preloads contacts. First use is Enter daily access code > Select Player > Select player name > Set password > Choose fictional email address > Open character interface. New browsers/devices must enter the current daily four-character code (A-Z and 0-9) at the landing screen before profile selection. A successful entry issues a server-verifiable device-authorization cookie that bypasses this gate on later visits. Daily code rotation does not invalidate already authorized devices. Account passwords and GM authentication remain separate requirements. The current code is always visible in a corner of the GM panel and updates automatically when it rotates. Claimed profiles require their password; the GM can reset it. The GM has no player character and uses authenticated administrative access. This replaces the earlier player-created-account/character flow. Hashed credentials are reset, not retrieved.

## ADR-009 — Group Administration and History
Groups support PCs and NPCs as members and admins. Admins can rename groups, manage membership, transfer admin permissions, and share all earlier history. Removal revokes all group-history access. Rejoining starts fresh at the new join time with no inherited grants; earlier history requires sharing again.

## ADR-010 — Fictional Email
Players can choose predefined or custom fictional email domains. They learn addresses in person or from received mail and can email a known address without a managed contact entry. Only the GM changes contacts. The GM can conceal a sender address using an encrypted-address presentation; these emails are one-way, with reply and reply all unavailable and reply attempts rejected by the backend. Players choose their fictional email address during first-use setup after selecting their assigned profile, before entering the character interface. MVP email actions are compose, reply, and reply all; forward, drafts, BCC, archive, and deletion are outside the current MVP controls. Mail supports multiple recipients, CC, and threaded replies without real email delivery or real personal contact information.

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

## ADR-016 — Messaging Navigation and Read State

Messages lists existing direct and group conversations. Starting a direct conversation uses Contacts > Select Contact > Message; no New Message > Select Contact flow is included. Opening a conversation marks available messages read for the active Character. Incoming messages become read while that reader is open and visible; otherwise they remain unread until opened. Global GM inspection does not alter recipient read state.

## ADR-017 — Fictional Address Fields and Email Entry Points

First-use address setup clearly identifies the address as fictional. Its three fields are Email (before @), Domain name, and Domain suffix. Suffixes are limited to .gen, .open, .pub, and .atd; the nine initial preset domains are listed in MAIL-08, and custom names are supported. Compose from Mail > Create Email or Contacts > Select Contact > Email. Both lead to the same compose/send behavior; encrypted-sender emails remain one-way.

## ADR-018 — Text Messaging Visual Design

**Status:** Selected design direction for the Text Messaging feature only, including direct and group conversation readers. This does not establish styling for Mail, Datashards, Contacts, the central hub, or the GM panel.

**Reference:** [cyberpunk-message-generator](https://github.com/daming98/cyberpunk-message-generator), specifically the `PALETTE`, `CONFIG`, and drawing functions in [cyber-message.html](https://github.com/daming98/cyberpunk-message-generator/blob/HEAD/cyber-message.html).

### Colors

Use the reference's near-black base, cyan incoming-message treatment, green outgoing-message treatment, and header accents as the starting palette:

| Role | Color |
| --- | --- |
| Base | #050505 |
| Header icons, title, name, and underline | #7ee2f8 |
| Incoming bubble fill | #181c1d |
| Incoming bubble border | #56e9e3 |
| Incoming text | #66cecd |
| Outgoing bubble fill | #1e4e3e |
| Outgoing bubble border | #4bdfad |
| Outgoing text | #49e0ad |
| Small decorative header text | #621914 |
| Decorative header line extension | #a43a2e |
| Divider text | #8fa3bd |
| Divider line | #3a4a5a |

The red background gradient is not an adopted design choice; background gradient treatment remains undecided. Red header accents do not imply a red background. Verify readability at mobile sizes when applying the palette, particularly decorative dark text.

### Message Bubbles

Use angled/beveled corners, outlined borders, mirrored tails, and distinct incoming/outgoing alignment and colors. Bubble dimensions and wrapping must adapt to phone screens and message length. Group messages must still identify their sender clearly.

### Headers

Use the reference's envelope icon, angular arrow, underlines, uppercase header labels, and small decorative metadata treatment. Adapt proportions and spacing to mobile layouts; the reference's fixed canvas dimensions are not layout requirements. Decorative metadata is visual detail, not a requirement for new stored fields.

### Typography

- **Rajdhani:** Character/contact names and message-body Latin text. It supports Latin letterforms as well as Devanagari; the intended use here is its Latin styling.
- **Play:** Small decorative header/metadata text.
- **Blender Pro:** Reference treatment for the MESSAGES header, with Rajdhani as the fallback. Use of the bundled Blender Pro font file remains subject to confirming suitable font licensing; recording the design direction does not authorize copying that font asset.

Keep message content readable and preserve its authored capitalization; uppercase treatment applies to header labels/names. Final font sizes, weights, and spacing will be refined in wireframes and mobile review.

### Implementation Boundary

The reference draws its conversation display with Canvas. Adapt the selected design into responsive React/TypeScript components with CSS/SVG as appropriate; do not treat the generator's export canvas or editor layout as the messaging implementation. Retain the repository's MIT notice if copying substantial code. Avatars and image attachments remain outside MVP.
