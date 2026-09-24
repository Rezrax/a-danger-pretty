# Night City Agent — Initial User Flows

## Status and Reading Guide

Phase 0 draft covering GM preparation, first player access, returning access, GM perspective switching, direct/group messaging, and email setup and use. Based on [product-requirements.md](product-requirements.md) and [terminology.md](terminology.md). This is the first set of flows, not completion of Phase 0 or the full MVP workflow catalog.

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

**Example:** Prepare the Player → the Character; create 7s; add 7s to the Character's contacts. Other PCs can also be added according to the GM's intended starting relationships.

**Result:** The Player can claim their prepared profile and enter a populated character interface. NPCs do not require human account setup.

**Exceptions and recovery:** Wrong code keeps the browser at the gate; wrong GM credentials keep the user out of administration. Failed saves must not be displayed as completed. An ordinary player cannot invoke preparation actions through direct API requests.

**Open decisions:** Initial GM provisioning; minimum character/profile fields; name uniqueness; whether the contact editor offers an explicit reciprocal-add option. Only GM-managed contacts are established, not automatic reciprocity.

**Review checks:** Profiles and assigned contacts survive reload/restart; a new browser cannot retrieve the player list before authorization; the corner code agrees with the console and gate at rotation.

## UF-02 — Player's First Visit

**Actor:** Player. **Requirements:** AUTH-01 through AUTH-05, GATE-01 through GATE-05, UI-01 through UI-04, CONTACT-02.

**Entry conditions:** The GM has prepared the player's profile, character, and initial contacts; the profile has no initial password yet.

1. The Player opens the site on their phone.
2. If the browser is not authorized, the landing screen asks for the four-character code. The Player obtains it from the GM and submits it.
3. The backend validates the current code and issues device authorization. The code alone gives no access to character content.
4. The Player selects the Player role, then selects their own name from the prepared player list.
5. Because the Player's profile is unclaimed, they set its initial password.
6. The Player creates their fictional email address using UF-08: Email, Domain name, and Domain suffix. The setup explains that this address works only inside the application.
7. After password and email-address setup succeed, the app opens the Character's home with Messages, Mail, Contacts, and Datashards.
8. The Player opens Contacts and finds 7s already present. Opening character content changes the Character's read state as appropriate.

**Result:** The Player's profile is claimed and password-protected, and the Character has the fictional email address the Player selected; their browser remembers passing the entrance gate. Neither the player profile nor the Character is created by these steps.

**Exceptions and recovery:**

- An invalid or yesterday's code fails. If midnight occurs before submission, obtain the current code; an already-authorized browser is unaffected.
- A claimed profile offers password authentication instead of initial password setup. First-use setup cannot overwrite an existing password, including if another request claims the profile concurrently.
- If the Player chooses the wrong name before setting a password, they can return to profile selection. Recovery after claiming the wrong profile is a GM-assisted action; its exact controls remain to be designed.
- On a failed or uncertain setup request, do not assume the password was saved. Re-check the profile state before retrying setup or logging in.
- If the expected player profile is absent, ask the GM to prepare it; there is no player-created-profile fallback.

**Established decision:** Address selection is part of first-use onboarding after selecting the assigned profile, before entering the character interface. It is not deferred until opening Mail.

**Open details:** Address validation/uniqueness and recovery when first-use setup is interrupted between password creation and address selection. Previously saved credentials must not be overwritten while completing address setup.

**Review checks:** First-use setup saves the selected fictional address before entering the character interface; both predefined and custom domains are available. The Player reaches the Character, not another character; 7s appears from the preset contacts; another claimed profile still requires its own password; profile claiming cannot be repeated to overwrite a credential.

## UF-03 — Returning Player and Credential Recovery

**Actor:** Returning player. **Requirements:** AUTH-01/02/04/06, GATE-03/04, QUALITY-06.

1. The Player opens the site.
2. The browser's device authorization is checked. A valid cookie skips code entry even if the daily code has changed. A new browser or missing cookie requires the current code.
3. If the Player still has a valid account session, the app can resume the Character's interface. Otherwise they select the Player role and their own name, then enter their password.
4. The app retrieves current permitted content and unread state, including changes since the last visit.
5. The Player uses the apps and can log out, ending account authentication.

| Device authorization | Account authentication | Required next step |
| --- | --- | --- |
| Missing/invalid | Missing/expired | Enter daily code, then authenticate the account. |
| Valid | Missing/expired | Authenticate the account; no daily code needed. |
| Valid | Valid | Resume the authenticated character interface. |
| Missing/invalid | Otherwise valid | Restore device authorization before protected use; a valid account session does not replace the gate. |

Device authorization has no application-imposed expiry. Browser storage loss may still require another code. Account session duration is a separate technical decision.

**Forgotten password branch:** The Player asks the GM for help. The GM authenticates, selects the Player's profile, and assigns a replacement credential. The Player uses that replacement to authenticate. The old password is not retrieved or disclosed.

**Exceptions and recovery:** Incorrect passwords do not grant access or reopen first-use setup. An expired account session returns to authentication. A connection interruption does not erase saved messages or datashards; reconnecting retrieves current state.

**Open implementation details:** Account-session lifetime, credential validation, and session invalidation after a GM reset. Define whether ordinary logout also removes device authorization; retaining it is the proposed default because it represents a separate gate.

**Review checks:** Midnight rotation does not force a remembered browser through the code screen; logging out prevents account access; GM reset allows recovery without retrieving the old password.

## UF-04 — GM Adopts a Character Perspective

**Actor:** Authenticated GM. **Requirements:** GM-01 through GM-04, NOTIFY-03/04, MSG-08/09/10.

1. The GM opens the panel's list of player accounts and NPC identities.
2. The GM selects the Character, 7s, or another character and opens that perspective.
3. The interface clearly identifies the active character. The GM's return/switch controls and current daily code remain available in the administrative shell.
4. Character-facing content and actions use that character's permissions. Global GM visibility is accessed through administration, not silently mixed into the adopted view.
5. Opening content marks it read for the selected character only. Opening the Character's mail can deliberately suggest that someone has accessed their account inside the fiction.
6. The GM may use the character's permitted actions. If 7s is a group admin, the GM can exercise that group's admin controls as 7s.
7. The GM returns to the global panel or selects another perspective without entering a player's password.

**Result:** The GM has acted through the selected character while remaining authenticated as GM for administrative switching. Read changes persist for that character.

**Global inspection branch:** The GM opens a conversation directly in the global panel without adopting a perspective. This provides oversight but does not mark messages read for PCs or NPCs.

**Exceptions and recovery:** Ordinary players cannot use switching endpoints. An expired GM session requires GM authentication again. Data from a previous perspective must not remain mixed into the new view, including live updates. A removed group member's perspective cannot display revoked history; rejoining starts at the new membership boundary until history is shared.

**Read behavior:** Incoming messages are marked read for the adopted Character while that conversation is open and visible. Otherwise they remain unread until opened. Switching itself does not imply that all content has been opened.

**Review checks:** Opening as the Character affects only the Character's read state; opening as 7s affects only 7s; global inspection changes neither. Adopted views respect current group-history and datashard-access rules. Returning to administration restores GM oversight.

## UF-05 — Read and Send in a Direct Conversation

**Actor:** Authenticated Player, or GM using an adopted Character/NPC perspective. **Requirements:** MSG-01/03 through MSG-08, NOTIFY-03/04/05, UI-02, QUALITY-06.

**Entry conditions:** Device authorization and account authentication are valid. A direct conversation already exists and is accessible to the active Character.

1. The Player opens the site and selects Messages from the Character's home.
2. Messages lists existing accessible direct and group conversations.
3. The Player selects the conversation with a PC or NPC, such as 7s.
4. The conversation opens with its available message history. Opening it marks the available messages read for the active Character.
5. The Player composes a message and sends it. The backend verifies the sender's access and validates and saves the message before treating it as sent.
6. Connected recipients receive the message automatically. New incoming messages in this conversation become read while its reader is open and visible; otherwise they remain unread until opened.
7. The Player can return to Messages or the Character's home.

**NPC behavior:** Delivery does not wait for GM approval or presence. A reply from 7s waits for the GM to write it. Sending a message does not itself mark it read for the recipient.

**Exceptions and recovery:** Failed sends display an error rather than claiming success. After a connection interruption, retrieve persisted history and current read state. Lost authentication requires login again. Opening the conversation list, a background tab, or another app does not mark this conversation's new messages read.

**Review checks:** A permitted conversation reopens with saved history; connected recipients receive updates without refresh; read state changes only for the active Character. Global GM inspection remains exempt from marking content read. Unauthorized requests cannot retrieve or send messages.

## UF-06 — Open a Direct Conversation from Contacts

**Actor:** Authenticated Player, or GM using an adopted Character/NPC perspective. **Requirements:** CONTACT-02/05, MSG-01/03/07/08/11, NOTIFY-03/04/05.

**Entry conditions:** The GM has added the intended PC/NPC to the active Character's contacts.

1. The Player selects Contacts from the Character's home.
2. The Player selects a contact, such as 7s.
3. The contact view presents a Message action.
4. The Player selects Message and enters the direct conversation with that contact. If a conversation already exists, its history is available; otherwise the reader has no earlier messages.
5. The Player reads available history, composes a message, and sends it using UF-05's permission, persistence, delivery, and read-state rules.

**Result:** The Player can start communicating with a GM-assigned contact or return to their existing conversation. This action does not add, remove, or share contacts.

**Navigation decision:** There is no New Message > Select Contact flow in Messages. New direct communications start through Contacts > Select Contact > Message; existing conversations are accessible from Messages.

**Exceptions and recovery:** An empty contacts list does not offer player-created contacts; the GM manages it. If a contact is removed during navigation, refresh its availability. The effect of contact removal on an existing direct conversation remains an open product decision.

**Implementation detail to refine:** Whether the empty conversation is persisted on opening or only when the first message is sent. Reopening a contact's conversation should resume its existing history rather than create duplicate threads.

**Review checks:** Selecting 7s opens the correct conversation and sender identity; a first message persists and can subsequently be reopened from Messages. Contacts contains no player-facing add/remove controls.

## UF-07 — Read and Send in a Group Conversation

**Actor:** Authenticated Player, or GM using an adopted Character/NPC perspective. **Requirements:** MSG-02/04/05/08/09, NOTIFY-03/04/05.

**Entry conditions:** The active Character is a current group participant. Group creation and administration are separate flows still to be drafted.

1. The Player opens the site and selects Messages.
2. The Player selects an accessible group conversation.
3. The reader shows messages from the Character's most recent addition to the group onward. If the group admin has shared history with this current membership, all earlier history is also available.
4. Opening the reader marks available messages read for this Character only. Inaccessible history is neither exposed nor marked read.
5. The Player composes and sends a message. The backend verifies current membership and saves it; connected authorized participants receive it automatically.
6. Incoming messages become read for the active Character while this group's reader is open and visible. They remain unread when the Player leaves the reader or the page is hidden.

**Removal and rejoining:** Removal revokes all group-history access and sending permissions, including while the reader is open. Stop displaying the revoked conversation and delivering new group updates to that Character. Rejoining creates fresh membership: old history grants do not return, and messages before the new join time remain inaccessible unless the admin shares history again.

**GM behavior:** In an adopted perspective, these rules apply to the selected Character/NPC and only that recipient's read state changes. Global GM inspection can see the conversation but does not mark it read for any participant.

**Exceptions and recovery:** A removed participant opening an old link receives no group history. Reconnection reloads current membership and history permissions before displaying content. Failed sends are not presented as successful.

**Review checks:** Default visibility begins at the latest join boundary; Share History grants all earlier history; removal revokes access; rejoining restores no earlier grant automatically. Other participants' unread state is unchanged when this Character opens the group.

## UF-08 — Create a Fictional Email Address During First Use

**Actor:** Player completing UF-02. **Requirements:** AUTH-04, MAIL-06/08.

**Entry conditions:** The Player has authorized their browser, selected their GM-created profile and assigned Character, and set their password. Address creation completes onboarding before entering the central hub.

1. The setup screen explains: "This is a fictional address for your Character inside Night City Agent. It cannot send or receive real-world email."
2. The Player enters the address name in the Email field (the part before @).
3. The Player chooses a preset domain or supplies their own domain name and selects one of the allowed suffixes.
4. The screen previews the assembled address as `email@domain.suffix`.
5. The Player submits the address. After successful validation and saving, the app opens the Character's central hub with the address ready for Mail.

| Field | Meaning | Example |
| --- | --- | --- |
| Email | Address name before @ | runner |
| Domain name | Name between @ and the suffix | ncmail |
| Domain suffix | One of .gen, .open, .pub, .atd | .pub |

Preset choices populate the domain name and suffix together:

- ncmail.pub
- arasaka.gen
- militech.gen
- zetatech.gen
- biotechnica.open
- ncorp.pub
- kangtao.open
- kiroshi.atd
- dynalar.atd

Custom domain names still use one of the four allowed suffixes. For example, `runner@afterlife.open` is assembled from `runner`, `afterlife`, and `.open`. These examples are fictional internal routing choices, not links or registered external services.

**Exceptions and recovery:** Missing fields or an unsupported suffix keep the Player in setup with clear feedback. A failed save must not be shown as successful. If password setup already succeeded before interruption, authenticate the claimed profile and resume incomplete address setup without replacing its password or creating a new Character.

**Open details:** Address-name/domain validation, uniqueness and case handling, and NPC address provisioning. These need precise rules before implementation.

**Review checks:** The fictional nature is clear; all nine presets are available; custom names use only allowed suffixes; the preview matches the saved address; successful setup assigns the address to the selected Character.

## UF-09 — Compose and Send from Mail

**Actor:** Authenticated Player, or GM using an adopted Character/NPC perspective. **Requirements:** MAIL-01/02/03/05/06/09, QUALITY-06.

**Entry conditions:** Device authorization and account authentication are valid; the active Character has a fictional email address. Mail is the Emails app on the central hub, not Messages.

1. The Player opens Mail from the central hub.
2. The Player selects Create Email.
3. The composer shows the active Character as sender. The Player enters a known fictional address in To and may add further To or CC recipients.
4. The Player writes a subject and body, reviews the recipients, and selects Send.
5. The backend validates the request and sender authority, saves the email, and makes it available to its recipients without intentional delay.
6. The sent email is available in Sent; connected recipients receive live updates and unread indications.

**Recipient discovery:** An address may have been provided in person or learned from received mail. A managed contact entry is not required, and sending or receiving email does not add a contact.

**Exceptions and recovery:** Validation or connection failures are displayed without falsely reporting success. Reconcile an uncertain send with persisted mail before retrying to avoid duplicate delivery. Persistent draft saving is outside MVP; this does not prevent retaining current composer input while displaying an error.

**Open detail:** Define unknown-address behavior, including a submission containing both valid and unknown recipients. Do not silently assume partial delivery or delivery to an external email service.

**Review checks:** Sender identity comes from the active perspective; To/CC recipients receive the saved email; unrelated players cannot retrieve it; the sender can reopen it in Sent. Sending does not mark mail read for its recipients.

## UF-10 — Compose an Email from Contacts

**Actor:** Authenticated Player, or GM using an adopted Character/NPC perspective. **Requirements:** CONTACT-02/05, MAIL-02/05/09.

**Entry conditions:** The GM has made the contact available, and that contact has a known fictional email address.

1. The Player opens Contacts from the central hub.
2. The Player selects a contact, such as 7s.
3. The Player selects Email.
4. The composer opens with that contact's known address already entered in To and the active Character as sender.
5. The Player adds any other known To/CC addresses, writes the subject and body, and sends using UF-09.

**Exceptions and recovery:** If the contact has no available email address, show that email is unavailable rather than inventing an address or sending. A concealed address learned only through an encrypted-sender email must not be exposed by this shortcut. The normal sender/contact permissions still apply.

**Review checks:** The correct known address is prefilled, the sender remains the active Character, and sending uses the same delivery and validation behavior as composing from Mail. The action does not change the contact list.

## UF-11 — Read Email and Reply

**Actor:** Authenticated Player, or GM using an adopted Character/NPC perspective. **Requirements:** MAIL-01 through MAIL-07, NOTIFY-03/04.

1. The Player opens Mail from the central hub and selects a received email conversation from the inbox.
2. The reader displays permitted emails with their sender, To/CC recipients, subject, and body. Replies are grouped in the same conversation; grouping must not expose messages the Character was not authorized to receive.
3. Opening the content marks the opened emails read for the active Character. Merely listing the inbox does not mark its contents read.
4. For an ordinary email, the Player chooses Reply to address its sender or Reply All to address its sender and other To/CC recipients.
5. The Player composes their response and sends it. Delivery follows UF-09, and the response remains grouped with the conversation.
6. The Player can return to the inbox or view Sent to reopen sent emails.

**Encrypted sender branch:** An email from a GM-obfuscated address displays an encrypted-sender indication without revealing the underlying address. Reply and Reply All are unavailable; backend reply attempts are rejected. This email is one-way even though ordinary Mail supports replies.

**GM behavior:** The GM may read mail globally without changing recipient read states. Reading through an adopted Character/NPC perspective changes that selected recipient's state only.

**Open detail:** Whether newly arriving email in an already-open reader becomes read immediately; the existing visible-reader rule is currently established for text messaging. Also define how recipient changes affect thread presentation while retaining per-email access checks.

**Review checks:** Ordinary Reply/Reply All target the intended recipients; responses remain threaded; opening marks only the active Character's content read. Encrypted sender addresses remain hidden in UI and player-visible API data, and those emails cannot be replied to.

## UF-12 — GM Sends Email as an NPC

**Actor:** Authenticated GM. **Requirements:** GM-03, MAIL-04/07.

1. The GM adopts an NPC perspective, such as 7s, using UF-04.
2. The GM opens Mail and Create Email, or selects Email from an available contact.
3. The GM enters recipients, subject, and body as in UF-09. The administrative controls allow selecting an encrypted sender presentation for this email.
4. The GM sends the email. Ordinary mail shows the NPC's fictional address and supports replies; encrypted-sender mail conceals the address and is one-way.
5. The GM can return to administration or switch perspective. The current daily access code remains visible in the GM shell.

**Review checks:** Only the GM can use NPC senders and encrypted-sender controls. The recipient receives the correct sender presentation without leaked address metadata. Reading received mail follows UF-11's perspective rules.

## Initial Screen Inventory for Wireframes

| Working screen | Flow coverage | Essential content |
| --- | --- | --- |
| Device gate | UF-01/02/03 | Four-character code entry, submit, validation/failure feedback. |
| Access selection | UF-01/02/03 | Player and GM paths; selection alone grants no role. |
| Player selection | UF-02/03 | GM-prepared player names and a way to return. |
| Initial password setup | UF-02 | Selected player/character identity, password entry, submit/back. |
| Fictional email setup | UF-02/08 | Fictional-address explanation, Email/Domain name/Domain suffix, nine presets, custom name, preview, validation. |
| Player login | UF-03 | Selected profile, password entry, GM-assisted recovery guidance. |
| Player app home | UF-02/03/04 | Character identity, four app launchers, home/navigation conventions, logout. |
| GM login | UF-01 | GM authentication. Initial provisioning is outside this screen's settled scope. |
| GM panel | UF-01/04 | Current code in a persistent corner, profiles/NPCs, contacts, conversations, datashards, perspective controls. |
| GM profile/contact editor | UF-01 | Player-character association and starting contacts; exact fields remain to be defined. |
| Adopted character view | UF-04 | Character apps with clear perspective indicator and return/switch controls. |
| GM credential reset | UF-03 | Target profile and replacement credential action. |
| Messages list | UF-05/07 | Existing accessible direct/group conversations and unread indicators. |
| Contacts list and contact view | UF-06/10 | GM-assigned contacts, selected identity, Message and Email actions. |
| Direct conversation reader | UF-05/06 | Contact identity, available history, composer, send feedback, back navigation. |
| Group conversation reader | UF-07 | Group identity, permitted history, composer, send/access feedback, back navigation. |
| Mail inbox and Sent | UF-09/11 | Received/sent conversations, unread indicators, Create Email. |
| Email composer | UF-09/10/11/12 | Sender, To, CC, subject, body, Send; GM-only encrypted-sender control. |
| Email reader | UF-11 | Permitted thread content, sender/recipients, Reply/Reply All for ordinary mail, one-way indication for encrypted mail. |

Screen separation and placement are provisional. Wireframes may combine steps without changing access rules.

## Remaining Flow Work

After reviewing these initial flows, document:

- Group creation and admin controls for transfer, removal, rejoining, and Share History; basic reading/sending is covered by UF-07.
- Refine Mail edge cases: NPC address setup, uniqueness, unknown recipients, and open-reader behavior; primary email flows are covered by UF-08 through UF-12.
- Datashard creation/distribution/editing, player deletion, GM revocation, and possible redistribution.
- GM contact removal and its effect on existing direct conversations.
- Feature-specific recovery for Mail and Datashards; messaging delivery and open-reader read behavior are covered by UF-05 through UF-07.

Then sketch the remaining MVP screens, turn the reviewed flows into backlog stories with acceptance criteria, and review the architecture against those stories. The existing [requirements open items](product-requirements.md#details-to-resolve-during-planning) remain authoritative until decisions are made.
