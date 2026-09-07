# Night City Agent — Terminology and Core Relationships

## Status

Phase 0 planning draft based on [product-requirements.md](product-requirements.md). These terms describe the product; they do not prescribe database tables or implementation classes.

## Vocabulary

| Term | Meaning |
| --- | --- |
| Player | A real person participating in the campaign. |
| Account | The authentication and permission identity used to access the application. Player accounts are prepared by the GM; the GM has a separate account. |
| Player profile | The GM-created entry that connects a player's selectable name to their assigned character. It exists before the player sets a password. |
| Claim / first-use setup | Selecting an unclaimed player profile and setting its initial password after device authorization. This does not create a new character. |
| PC / player character | The fictional person assigned to one player, such as FNX (pronounced Phoenix). One per player in MVP. |
| NPC | A fictional person or entity controlled by the GM, such as Se7ens (pronounced sevens). An NPC needs no human login account. |
| GM / Game Master | The person with authority over profiles, NPCs, contacts, communications, and datashards. The GM account has no assigned PC. |
| Admin GUI / GM panel | The administrative interface used by the GM. A separate developer role is not established for MVP. |
| Adopted perspective | A PC or NPC view selected by the authenticated GM. Actions use that character's permissions and read state; the GM can return to administration. |
| Group admin | A participant with management permissions for one group conversation. This does not confer GM privileges. An NPC may hold this position. |
| Landing screen / device gate | The entrance screen that requests the daily code from an unauthorized browser. Distinct from the character's app home screen. |
| Daily access code | The shared four-character A-Z/0-9 code that rotates at midnight America/Chicago. Displayed in the GM panel and logged at server startup and rotation. |
| Device authorization | Permission for a browser to pass the entrance gate, remembered with a server-verifiable cookie. It has no application-imposed expiry and is separate from account login. |
| Account session | The authenticated account's current login state. Its lifetime is separate from device authorization and remains a technical decision. |
| Player OS / app home | The character-facing interface for launching Messages, Mail, Contacts, and Datashards. |
| Contact | A PC/NPC entry made available to a character by the GM. Only the GM adds or removes entries in MVP. |
| Fictional email address | An internal Mail address using a predefined or custom fictional domain. It is not a real-world email account and does not require a managed contact entry to address mail. |
| Encrypted sender address | A GM-obfuscated sender address. These emails are one-way and cannot be replied to; this is not real cryptographic email. |
| Conversation | A direct or group text conversation. Email replies also form conversations, but the two interfaces remain distinct. |
| Group membership | A character's current participation in a group, including the join boundary that controls visible history. Removal revokes all group-history access; rejoining starts fresh. |
| Share History | A group-admin action granting a selected current participant access to all earlier history. Prior grants do not survive removal/rejoining. |
| Datashard | A shared plain-text document created and edited by the GM, accessible to selected characters. |
| Datashard deletion | A player giving up their own access to a shard. Other authorized recipients and the GM retain the document. |
| Datashard revocation | The GM removing a selected recipient's access to a shard. |
| Read state | Whether a recipient has opened content. Opening through an adopted perspective marks it read for that character. Global GM inspection does not change recipient read states. |
| Live update | New content appearing automatically while connected, without manual refresh. Persistence allows retrieval after reconnecting. |
| MVP | Minimum Viable Product: the scoped first usable campaign release. |
| MVF | Maximum Valued Feature: the user's label for the post-MVP datashard encryption minigame. |

## Core Relationships

| Relationship | Established product rule |
| --- | --- |
| Player profile → PC | The GM prepares the association before first use. Each player controls exactly one assigned PC. |
| GM account → PC | No assigned PC. GM access enables oversight and adopted perspectives. |
| GM → NPCs | The GM creates and controls NPCs without assigning them human passwords. |
| Browser → device authorization → account session | Passing the gate permits login/onboarding; it does not authenticate an account. A remembered browser can still require a player password. |
| Character → contacts | A character has a GM-managed set of known contacts. Adding Se7ens to FNX's list does not imply any automatic reciprocal contact grant. Reciprocal defaults remain a flow detail. |
| Character → fictional address | PCs/NPCs communicate through fictional email addresses. Address setup timing and uniqueness rules are still open. |
| Conversation → participants → messages | A sender must be a participant. The GM can inspect all conversations. Groups may contain PCs and NPCs. |
| Group participant → history access | Default access starts at the current join time. Sharing grants all earlier history; removal revokes access. |
| Email → sender and To/CC recipients | Recipients may be identified by known fictional addresses without being managed contacts. Obfuscated senders cannot receive replies to those messages. |
| Datashard → recipient access and read state | One shared document can have multiple recipients. Edits affect everyone retaining access without resetting read state. Removing one recipient does not remove the document. |
| GM session → adopted perspective | The selected character changes the view, permitted character actions, and read-state target. GM authority remains necessary for switching and returning to administration. |

Account, profile, character, and identity are conceptual distinctions here. Decide their persistence representation during schema planning; this document does not require separate entities for every term.

## Example

The GM prepares Matt's player profile, assigns FNX, creates Se7ens as an NPC, and puts Se7ens in FNX's contacts. Matt authorizes his browser, selects Matt, and sets his password. His app opens as FNX. Selecting Matt never creates FNX or grants control over Se7ens.

The GM can separately adopt FNX's perspective and open content as FNX, changing FNX's read state. Returning to the global GM view restores administrative oversight without marking other recipients' content read.
