# Night City Agent — Initial User Flows

## Status and Reading Guide

Phase 0 draft covering GM preparation, first player access, returning access, and GM perspective switching. Based on [product-requirements.md](product-requirements.md) and [terminology.md](terminology.md). This is the first set of flows, not completion of Phase 0 or the full MVP workflow catalog.

Numbered steps describe established behavior. **Open decisions** identify incomplete details. **Proposals for review** are suggestions, not accepted requirements. Screen names are working labels for wireframing.

## UF-01 — GM Prepares the Campaign

**Actor:** GM. **Requirements:** AUTH-03/06, CONTACT-01/05, GM-01/04, GATE-01 through GATE-06.

**Entry conditions:** The server is running and the initial GM account has been provisioned. The provisioning mechanism remains undecided.

1. The server logs the current daily code to its console.
2. On a browser without device authorization, the GM enters that code at the landing screen. A valid remembered browser skips this step.
3. The GM chooses GM access and authenticates with GM credentials. Role selection alone does not authorize access.
4. The GM panel opens, keeping the current code visible in a corner. It updates automatically at midnight America/Chicago.
5. The GM creates a player profile with a selectable player name and assigns its character. The GM does not set the player's initial password through this preparation flow.
6. The GM creates the NPCs needed for the campaign and assigns each character's starting contacts.
7. The prepared profile becomes available for first-use selection behind the device gate.

**Example:** Prepare Matt → FNX; create Se7ens; add Se7ens to FNX's contacts. Other PCs can also be added according to the GM's intended starting relationships.

**Result:** Matt can claim his prepared profile and enter a populated character interface. NPCs do not require human account setup.

**Exceptions and recovery:** Wrong code keeps the browser at the gate; wrong GM credentials keep the user out of administration. Failed saves must not be displayed as completed. An ordinary player cannot invoke preparation actions through direct API requests.

**Open decisions:** Initial GM provisioning; minimum character/profile fields; name uniqueness; whether the contact editor offers an explicit reciprocal-add option. Only GM-managed contacts are established, not automatic reciprocity.

**Review checks:** Profiles and assigned contacts survive reload/restart; a new browser cannot retrieve the player list before authorization; the corner code agrees with the console and gate at rotation.

## UF-02 — Player's First Visit

**Actor:** Player. **Requirements:** AUTH-01 through AUTH-05, GATE-01 through GATE-05, UI-01 through UI-04, CONTACT-02.

**Entry conditions:** The GM has prepared the player's profile, character, and initial contacts; the profile has no initial password yet.

1. Matt opens the site on his phone.
2. If the browser is not authorized, the landing screen asks for the four-character code. Matt obtains it from the GM and submits it.
3. The backend validates the current code and issues device authorization. The code alone gives no access to character content.
4. Matt selects Player, then selects Matt from the prepared player list.
5. Because Matt's profile is unclaimed, he sets its initial password.
6. After successful setup, the app opens FNX's home with Messages, Mail, Contacts, and Datashards.
7. Matt opens Contacts and finds Se7ens already present. Opening character content changes FNX's read state as appropriate.

**Result:** Matt's profile is claimed and password-protected; his browser remembers passing the entrance gate. Neither the player profile nor FNX is created by these steps.

**Exceptions and recovery:**

- An invalid or yesterday's code fails. If midnight occurs before submission, obtain the current code; an already-authorized browser is unaffected.
- A claimed profile offers password authentication instead of initial password setup. First-use setup cannot overwrite an existing password, including if another request claims the profile concurrently.
- If Matt chooses the wrong name before setting a password, he can return to profile selection. Recovery after claiming the wrong profile is a GM-assisted action; its exact controls remain to be designed.
- On a failed or uncertain setup request, do not assume the password was saved. Re-check the profile state before retrying setup or logging in.
- If the expected player profile is absent, ask the GM to prepare it; there is no player-created-profile fallback.

**Open decision:** The point at which Matt chooses his fictional email address is not settled by the revised onboarding flow.

**Proposal for review:** Put address selection in Mail on first opening. This preserves the short first-login flow and lets Matt choose a predefined or custom domain. It requires defining what Mail shows before an address is chosen and whether the GM can provision one in advance. Do not assume this proposal is approved.

**Review checks:** Matt reaches FNX, not another character; Se7ens appears from the preset contacts; another claimed profile still requires its own password; profile claiming cannot be repeated to overwrite a credential.

## UF-03 — Returning Player and Credential Recovery

**Actor:** Returning player. **Requirements:** AUTH-01/02/04/06, GATE-03/04, QUALITY-06.

1. Matt opens the site.
2. The browser's device authorization is checked. A valid cookie skips code entry even if the daily code has changed. A new browser or missing cookie requires the current code.
3. If Matt still has a valid account session, the app can resume FNX's interface. Otherwise he selects Player and Matt, then enters his password.
4. The app retrieves current permitted content and unread state, including changes since the last visit.
5. Matt uses the apps and can log out, ending account authentication.

| Device authorization | Account authentication | Required next step |
| --- | --- | --- |
| Missing/invalid | Missing/expired | Enter daily code, then authenticate the account. |
| Valid | Missing/expired | Authenticate the account; no daily code needed. |
| Valid | Valid | Resume the authenticated character interface. |
| Missing/invalid | Otherwise valid | Restore device authorization before protected use; a valid account session does not replace the gate. |

Device authorization has no application-imposed expiry. Browser storage loss may still require another code. Account session duration is a separate technical decision.

**Forgotten password branch:** Matt asks the GM for help. The GM authenticates, selects Matt's profile, and assigns a replacement credential. Matt uses that replacement to authenticate. The old password is not retrieved or disclosed.

**Exceptions and recovery:** Incorrect passwords do not grant access or reopen first-use setup. An expired account session returns to authentication. A connection interruption does not erase saved messages or datashards; reconnecting retrieves current state.

**Open implementation details:** Account-session lifetime, credential validation, and session invalidation after a GM reset. Define whether ordinary logout also removes device authorization; retaining it is the proposed default because it represents a separate gate.

**Review checks:** Midnight rotation does not force a remembered browser through the code screen; logging out prevents account access; GM reset allows recovery without retrieving the old password.

## UF-04 — GM Adopts a Character Perspective

**Actor:** Authenticated GM. **Requirements:** GM-01 through GM-04, NOTIFY-03/04, MSG-08/09/10.

1. The GM opens the panel's list of player accounts and NPC identities.
2. The GM selects FNX, Se7ens, or another character and opens that perspective.
3. The interface clearly identifies the active character. The GM's return/switch controls and current daily code remain available in the administrative shell.
4. Character-facing content and actions use that character's permissions. Global GM visibility is accessed through administration, not silently mixed into the adopted view.
5. Opening content marks it read for the selected character only. Opening FNX's mail can deliberately suggest that someone has accessed his account inside the fiction.
6. The GM may use the character's permitted actions. If Se7ens is a group admin, the GM can exercise that group's admin controls as Se7ens.
7. The GM returns to the global panel or selects another perspective without entering a player's password.

**Result:** The GM has acted through the selected character while remaining authenticated as GM for administrative switching. Read changes persist for that character.

**Global inspection branch:** The GM opens a conversation directly in the global panel without adopting a perspective. This provides oversight but does not mark messages read for PCs or NPCs.

**Exceptions and recovery:** Ordinary players cannot use switching endpoints. An expired GM session requires GM authentication again. Data from a previous perspective must not remain mixed into the new view, including live updates. A removed group member's perspective cannot display revoked history; rejoining starts at the new membership boundary until history is shared.

**Open decision:** How new messages are marked while their reader is already open remains a general read-state question. Switching itself does not imply that all content has been opened.

**Review checks:** Opening as FNX affects only FNX's read state; opening as Se7ens affects only Se7ens; global inspection changes neither. Adopted views respect current group-history and datashard-access rules. Returning to administration restores GM oversight.

## Initial Screen Inventory for Wireframes

| Working screen | Flow coverage | Essential content |
| --- | --- | --- |
| Device gate | UF-01/02/03 | Four-character code entry, submit, validation/failure feedback. |
| Access selection | UF-01/02/03 | Player and GM paths; selection alone grants no role. |
| Player selection | UF-02/03 | GM-prepared player names and a way to return. |
| Initial password setup | UF-02 | Selected player/character identity, password entry, submit/back. |
| Player login | UF-03 | Selected profile, password entry, GM-assisted recovery guidance. |
| Player app home | UF-02/03/04 | Character identity, four app launchers, home/navigation conventions, logout. |
| GM login | UF-01 | GM authentication. Initial provisioning is outside this screen's settled scope. |
| GM panel | UF-01/04 | Current code in a persistent corner, profiles/NPCs, contacts, conversations, datashards, perspective controls. |
| GM profile/contact editor | UF-01 | Player-character association and starting contacts; exact fields remain to be defined. |
| Adopted character view | UF-04 | Character apps with clear perspective indicator and return/switch controls. |
| GM credential reset | UF-03 | Target profile and replacement credential action. |

Screen separation and placement are provisional. Wireframes may combine steps without changing access rules.

## Remaining Flow Work

After reviewing these initial flows, document:

- Direct messaging and group creation, admin transfer, removal, rejoining, and Share History.
- Mail setup, known-address composition, CC/replies, and one-way encrypted senders.
- Datashard creation/distribution/editing, player deletion, GM revocation, and possible redistribution.
- GM contact removal and its effect on existing direct conversations.
- Live updates, open-reader read state, and recovery during feature use.

Then sketch the remaining MVP screens, turn the reviewed flows into backlog stories with acceptance criteria, and review the architecture against those stories. The existing [requirements open items](product-requirements.md#details-to-resolve-during-planning) remain authoritative until decisions are made.
