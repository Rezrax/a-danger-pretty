# Night City Agent — Product Requirements

## Purpose and Status

Night City Agent is a private web application for one Cyberpunk RED tabletop campaign. Players use an in-world operating-system interface inspired by Cyberpunk 2077 to communicate as their characters and receive GM-created information. The application is intended for use during and between sessions, primarily through phone browsers, with desktop support.

This document consolidates the agreed MVP scope during Phase 0. Requirements describe intended behavior, not implemented features. Unresolved details are listed separately below. The [README roadmap](../README.md#development-roadmap) defines development phases; detailed stories and acceptance criteria belong in [mvp-backlog.md](mvp-backlog.md).

## Users and Access

- **Player:** A person with an account controlling exactly one player character in the single campaign.
- **Game Master (GM):** A person with an account authorized to oversee all conversations, control NPC communications, and create and distribute datashards.
- **Player character (PC):** The player's in-world identity, used to identify them in communications.
- **NPC:** A GM-controlled in-world contact that can send and receive communications without a separate human login.

The GM can read all player communications, including player-only conversations. Players may only access authorized conversation history and datashards made available to their character; group membership and history-sharing rules further limit which messages they can read. NPC responses are written by the GM.

## MVP Functional Requirements

### Accounts and Character Ownership

- **AUTH-01:** The GM and players can log in and log out using individual accounts.
- **AUTH-02:** Authentication persists across ordinary page refreshes until logout or session expiry.
- **AUTH-03:** The GM creates player profiles, assigns each player exactly one character, and preconfigures their contacts. Each player controls their assigned character. Players can act only as their own character. The GM account has no player character and uses a separate GM interface.
- **AUTH-04:** First use follows Enter daily access code > Select Player > Select pre-created player name > Set password > Open the assigned character interface. Players cannot create profiles. New browsers/devices must enter the current daily four-character code (A-Z and 0-9) at the landing screen before profile selection. A successful entry issues a server-verifiable device-authorization cookie that bypasses this gate on later visits. Daily code rotation does not invalidate already authorized devices. Account passwords and GM authentication remain separate requirements. Once claimed, the profile requires its password, with recovery handled by the GM. Selecting a GM role never grants GM privileges without GM authentication.
- **AUTH-05:** Protected data and actions require authentication and appropriate backend-enforced permissions.

- **AUTH-06:** A player who forgets their password/PIN asks the GM for help. The GM can assign a replacement credential; existing credentials are stored as hashes and cannot be retrieved for disclosure.

### Device Access Gate

- **GATE-01:** A browser without valid device authorization sees a landing screen requesting the current code before it can access profile selection or player onboarding. The code is exactly four uppercase alphanumeric characters, using A-Z and 0-9.
- **GATE-02:** The shared code changes at midnight in America/Chicago each real-world day, following that timezone including daylight-saving changes, regardless of the server host timezone. The backend accepts the current day's code and rejects expired codes for new device authorization. This does not introduce campaign time tracking.
- **GATE-03:** Correct entry issues a persistent, server-verifiable authorization cookie for that browser/device. Device authorization has no application-imposed expiry. Later visits bypass the code screen while the browser retains a valid cookie, including after daily code rotation. Browser deletion or retention limits can still remove the cookie; this policy does not change account-session expiry. A new browser, private-browsing session, or cleared cookie requires authorization again.
- **GATE-04:** Device authorization only bypasses the entrance gate. It does not log in a player, replace their password, grant GM privileges, or allow access to another player's data. The backend enforces the gate on protected onboarding/profile-list endpoints as well as the UI.
- **GATE-05:** Invalid or forged cookies do not authorize a browser. Rate-limit failed code attempts on the backend. Midnight America/Chicago rotation and no application-imposed device-authorization expiry are settled. Any administrative revocation mechanism remains an implementation detail to define.

- **GATE-06:** At server startup, log the currently valid access code to the server console. Whenever the daily code rotates, log the newly active code. The GM can obtain the code from the console to authorize a first device before accessing the GM panel. Startup logging reports the valid code; it does not independently require code rotation.

The cookie remembers a successful device authorization rather than storing yesterday's code for comparison. Daily code changes therefore do not force all previously authorized devices to re-enter it.

### Player Operating-System Interface

- **UI-01:** Players access Messages, Mail, Contacts, and Datashards through a unified operating-system shell and home navigation.
- **UI-02:** Each app has clear navigation, including a consistent way to return home or to its preceding view.
- **UI-03:** Primary workflows work on phone screens with touch controls and an on-screen keyboard, and remain usable in desktop browsers.
- **UI-04:** In-world styling supports readable content and quick interactions during play. Exact navigation patterns and visual treatments will be defined through wireframes.

### NPCs and Contacts

- **CONTACT-01:** The GM can create and manage NPC identities for communication.
- **CONTACT-02:** Players can view contacts available to their character and identify who they are communicating with.
- **CONTACT-03:** The GM can clearly select and see the NPC identity used when sending a communication.
- **CONTACT-04:** Players cannot act as NPCs or manage NPC identities.

- **CONTACT-05:** Only the GM can add or remove contacts in MVP, including preloading contacts before first login. Knowing an email address or receiving an email does not automatically add a managed contact.

Example: the GM creates Matt's player profile linked to FNX (Phoenix), with Se7ens (sevens) already in FNX's contacts. Matt selects Player, selects Matt, sets his password, and enters FNX's interface with Se7ens available.

Player-to-player contact sharing is a very-low-priority post-MVP backlog item.

### Text Messaging

- **MSG-01:** Players can send and receive direct text messages with other PCs and NPCs.
- **MSG-02:** Players can create group conversations containing PCs and NPCs. The creator is labeled the group admin and can rename the conversation, add or remove characters, and transfer admin permissions to another participant.
- **MSG-03:** Players can message NPCs at any time without waiting for the GM to be online or approve delivery. A response depends on the GM replying.
- **MSG-04:** Messages are delivered without intentional delay. Connected recipients see new messages and conversation updates without manually refreshing the page.
- **MSG-05:** Conversations and message history persist and can be reopened after refresh, logout, or a later session, subject to membership and history-access rules.
- **MSG-06:** The GM can read every direct and group conversation, including conversations containing only PCs.
- **MSG-07:** The GM can initiate NPC communications and reply as an NPC participating in a conversation. The backend verifies authority to use that sender.
- **MSG-08:** The backend enforces conversation membership, group-admin permissions, and per-participant history access. Players cannot send as another character or send while outside the conversation.
- **MSG-09:** Participants see messages from their current join time onward by default. Removal revokes all access to that group history. Rejoining starts a new membership with no inherited history grants; messages from the new join time are visible, and earlier history requires the admin to share it again. Share History reveals all earlier history to the selected participant.

Instant delivery describes the user experience, not a selected transport or a guaranteed latency. A disconnected recipient can retrieve persisted messages when they reconnect. There is no campaign-clock scheduling or simulated delivery delay.

- **MSG-10:** Admin permissions may be transferred to an NPC participant; the GM exercises those permissions through that NPC's perspective.

### In-World Email

- **MAIL-01:** Players can send and receive in-world emails with PCs and NPCs through a distinct Mail interface.
- **MAIL-02:** Players can view received and sent mail, open an email, compose with To and CC recipients, subject, and body, reply to the sender, and reply all to the sender and other To/CC recipients. Multiple recipients are supported and replies are grouped into conversations.
- **MAIL-03:** Emails persist between sessions and become available to recipients without intentional delay.
- **MAIL-04:** The GM can read all email conversations and send or reply as NPCs.
- **MAIL-05:** Email access is restricted to the relevant senders, recipients, and GM.
- **MAIL-06:** Email stays within the application. It does not require players' real email addresses, phone numbers, or integration with external email services.

Players can choose from predefined fictional email domains or invent a custom domain. When the address is selected in the revised GM-created-profile flow remains to be specified. These names route only inside the application and do not need real domain registration. The MVP email actions are compose, reply, and reply all. Forward, drafts, BCC, archive, and deletion are outside the current MVP controls. Recipients can be addressed using a known fictional address, even without a managed contact entry. Players learn addresses through in-person exchanges or received emails. Address uniqueness and NPC address setup remain to be specified. Text and email may share implementation where useful, while retaining their separate player-facing presentations.

- **MAIL-07:** The GM can send an email from an encrypted address, concealing the underlying sender address from players. This is sender-address obfuscation, not real email encryption. Player-visible API data and thread metadata must not expose the concealed address. These emails are one-way: reply and reply all are unavailable, and the backend rejects reply attempts to these messages.

### Datashards

- **SHARD-01:** The GM can create and edit plain-text datashards with a title and body, including datashards already distributed. Edits update the shared document for every recipient who retains access and do not mark it unread again.
- **SHARD-02:** The GM can distribute a datashard to one player, several players, or all players.
- **SHARD-03:** Selected players can find delivered datashards in their library, open them, and read them on mobile or desktop.
- **SHARD-04:** Delivered datashards persist and can be reopened while the player retains access.
- **SHARD-05:** Players cannot retrieve datashards that have not been made available to their character, including through direct API requests.
- **SHARD-06:** The GM controls creation and distribution and can revoke a player's access.
- **SHARD-07:** Players can delete a shard from their own library, giving up their own read access. This does not delete the underlying document or affect other players who retain access; the GM can still see it. This is per-player access removal, not global document deletion.

Datashards replace the originally proposed news app. Draft/publish states, metadata, formatting tools, and a dedicated recipient entity are not prerequisites; their need must be established before adding them.

A datashard encryption minigame is recorded in [the backlog](mvp-backlog.md#future-01--datashard-encryption-minigame-mvf) as a post-MVP MVF (Maximum Valued Feature).

### Notifications and GM Dashboard

- **NOTIFY-01:** Players receive consistent in-app indications of new messages, emails, and delivered datashards, including unread indicators.
- **NOTIFY-02:** Connected players receive updates without manual refresh. After refresh or reconnection, displayed unread information is reconciled with persisted data.
- **GM-01:** A separate GM interface displays all NPCs, datashards, and conversations, supports NPC management and datashard editing/distribution, and lets the GM create conversations between NPCs. The GM does not need a player character.
- **GM-04:** The current daily access code is always visible in a persistent corner of the GM panel, including while using its account-perspective controls. It updates automatically at rotation without manual refresh and its panel/API retrieval requires GM authorization. The server console also reports it at startup and rotation for operator access.
- **GM-02:** GM controls are available only to the GM. The interface makes the selected account/character perspective clear.
- **GM-03:** The authenticated GM/admin can list all player accounts and NPC identities, select one, and adopt that character's view and permissions without entering that player's password. The GM can return to the administrative view and switch perspectives. NPC perspectives do not require human login accounts. These actions require GM authority on the backend; ordinary players cannot switch accounts.

- **NOTIFY-03:** Content is unread until opened by the player, and becomes read when opened. Read state belongs to the relevant recipient.
- **NOTIFY-04:** Opening content while adopting a PC or NPC perspective marks it read for that selected character only. Global GM inspection without an adopted perspective does not change player or NPC read state. The GM may deliberately mark a player's content read this way as an in-world sign of hacking; no separate hacking mechanic is required.

Live updates and necessary GM controls are built with their respective features. Later roadmap phases consolidate those capabilities. Closed-browser push notifications and external notification services are not required for MVP.

## Quality and Operational Requirements

- **QUALITY-01 — Persistence:** Accounts, character and NPC data, communications, datashard visibility, and required read state persist in PostgreSQL across application restarts.
- **QUALITY-02 — Availability:** The deployed application is intended to be available during and between sessions, with near-24/7 access. No numerical uptime guarantee has been established.
- **QUALITY-03 — Hosting:** Players access the hosted application through a normal browser over HTTPS and an eventual custom domain. The hosting provider and domain have not been selected.
- **QUALITY-04 — Credentials and permissions:** Store passwords/PINs securely as hashes, protect authenticated sessions, and enforce ownership and GM permissions on the backend. Hiding controls alone is insufficient.
- **QUALITY-05 — Validation and rendering:** Validate submitted data and render user-authored text safely. Reject unauthorized actions without exposing protected content.
- **QUALITY-06 — Errors and recovery:** Clearly communicate failed operations, expired sessions, and connection problems. Persisted communications remain retrievable after a connection interruption.
- **QUALITY-07 — Usability:** Keep text readable and navigation usable on actual phones. Visual effects must not interfere with reading or sending communications.
- **QUALITY-08 — Backups:** Production data has a backup and tested restoration process before campaign use.

Specific limits, session duration, browser support targets, and operational procedures will be defined with the relevant features and deployment work.

## Scope Boundaries

The MVP excludes:

- Multiple campaigns, multiple characters per player, and commercial multi-tenant administration.
- Character sheets, inventory, combat tracking, and broader campaign-management systems.
- Campaign time tracking, scheduled delivery, and simulated delays.
- Fictional browser apps, web-page builders, player-created websites, and a separate news system.
- File uploads, portraits, and message/email attachments.
- Real-world phone numbers or email addresses as required profile information, and real-world email or SMS delivery. Fictional email addresses are included.
- Autonomous or AI-controlled NPC responses.
- Message editing and deletion tools.
- Hacking minigames, encryption puzzles, and other advanced narrative systems.
- Native mobile applications, external notification integrations, and closed-browser push notifications.
- Player-created profiles and arbitrary new accounts. First-use claiming of GM-created profiles is included behind the daily device access gate.

Do not require speculative profile fields or audit metadata solely for future flexibility. In particular, user `active`/`createdAt`, character/NPC portrait and real contact-information fields, and datashard `createdBy`/`createdAt`/`status` were removed from the proposed MVP requirements. Fictional email addresses have now been explicitly added for in-world Mail. Technical timestamps needed for ordering communications or read state do not imply a campaign clock.

## Established Technical Constraints

- Backend: Java with Spring Boot.
- Frontend: React with TypeScript, supporting practical experience relevant to the developer's professional work.
- Frontend tooling: Node.js for package management, development, and builds.
- Database: PostgreSQL.
- Delivery: A hosted browser application for mobile and desktop.

Framework versions, authentication mechanism, migration tool, live-update transport, and hosting remain implementation decisions. The schema must support the product rules without assuming that every domain concept requires its own table or abstraction.

## Details to Resolve During Planning

These items need decisions or more detailed acceptance criteria; they do not expand MVP scope:

1. **Account setup details:** Define initial GM setup and credential rules. The product flow is settled: GM creates profiles and contacts; players authorize their device with the daily code, select their profile, and set a password. Rotation is midnight America/Chicago and device authorization has no application-imposed expiry. Administrative revocation behavior can be specified with authentication implementation. First-device access is resolved: the GM reads the code from the server console.
2. **Contact removal:** Does removing a contact affect existing direct conversations or only the contact list? Group removal is a separate action with its own established access rules.
3. **Email setup:** When do players choose their fictional address in the revised onboarding flow, and how are NPC addresses assigned? Define address uniqueness and unknown-address behavior. Predefined and custom domains, address-based recipients, To/CC, threading, and compose/reply/reply-all are established.
4. **Datashard redistribution:** Can the GM restore access after player deletion or GM revocation, and if so does the shard return as read or unread? Shared edits, unchanged read state on edit, and per-player deletion are established.
5. **Open-reader behavior:** How is newly arriving content treated while a reader is already open? Read-state changes from adopting a character perspective are resolved.
Live-update behavior is resolved: connected recipients receive automatic updates without manual refresh. Selecting the transport is deferred technical work and does not require another product-scope decision.

## MVP Validation Scenarios

The eventual MVP should demonstrate these complete workflows:

1. A player logs in on a phone, accesses their character's apps, refreshes successfully, and logs out.
2. Two players exchange direct messages and create a group conversation; connected recipients see updates without manual refresh.
3. A player messages an NPC; the GM reads the conversation and replies with the correct NPC identity. The GM can also inspect a player-only conversation.
4. Players and GM-controlled NPCs exchange in-world emails, and permitted users can reopen them later.
5. The GM distributes a datashard to selected players; those players can read it and other players cannot retrieve it.
6. New-content and unread indications remain consistent after refresh or reconnection, and saved data survives an application restart.
7. Ordinary-player attempts to impersonate another character, act as an NPC, switch account perspectives, or access GM-only actions are rejected. The authenticated GM can switch perspectives and return to administration.
8. Core workflows work on desktop as well as actual phones, and deployed campaign data can be restored from backup.
9. Matt enters the daily code on a new browser, claims his pre-created profile, sets a password, and opens FNX with Se7ens already in Contacts. Later login requires the password; first-use setup cannot overwrite it.
10. Removing a group member revokes history access; rejoining exposes only messages from the new join time until Share History grants all earlier messages.
11. Datashard edits reach remaining recipients without resetting read state. Player deletion or GM revocation removes only the relevant access, leaving other recipients unaffected.
12. Players can address mail using a learned fictional address. GM-obfuscated sender addresses remain concealed in player-visible responses and conversation metadata; encrypted-sender emails cannot be replied to through the UI or API.
13. Opening content while the GM adopts a PC or NPC perspective marks it read only for that character. Global GM inspection leaves all recipient read states unchanged.

14. A new browser cannot retrieve the player list before entering the valid daily code. Correct entry issues device authorization; invalid codes and forged cookies fail. An authorized browser bypasses the gate after a daily rotation but still requires account authentication.
15. The GM panel displays the current code continuously and updates at the daily boundary. The previous code no longer authorizes new browsers. Server startup logs the currently valid code; rotation logs the new code, matching the code accepted by the gate and displayed in the panel.

These scenarios guide later acceptance criteria and testing. Completing this document alone does not finish Phase 0: terminology, relationships, flows, wireframes, and backlog refinement still remain.
