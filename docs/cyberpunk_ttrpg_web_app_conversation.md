# Cyberpunk TTRPG Web App --- Conversation Export

## User

This will be a rather big project. I would like to make a web
application for me and my friends for use during a cyberpunk red ttrpg
taking massive inspiration from Cyberpunk 2077. This is not a commercial
product, and so there will be no need to worry about Copyright or
trademarks. The web application should be able to have and store
credentials so each player could have their own account, and will be
hosted on a custom domain. The players should be able to write and
receive both "emails" and "text messages" to one another and to NPCs,
such that they can communicate with one another and receive
communications alike. In CDProjekt Red's Cyberpunk 2077, while checking
computers they can also access web portals, which have news articles and
websites alike.

Don't start coding yet. Help me organize these thoughts into discrete
features so that through the software engineering and development
process we can complete this.

## Assistant

# Cyberpunk TTRPG Web App --- Feature Breakdown

## 1. Product Vision

A private, immersive companion application for a Cyberpunk RED campaign,
styled after the digital interfaces of *Cyberpunk 2077*.

Players should feel as though they are using an in-world operating
system rather than a conventional campaign-management website. They can
log into character-specific accounts, exchange messages, browse
fictional websites, receive news updates, and interact with NPCs
controlled by the Game Master.

The application should support two distinct layers:

-   **In-world layer:** Messages, emails, news, websites, files, and
    character-accessible information.
-   **Game-management layer:** GM controls, permissions, content
    creation, scheduling, and campaign administration.

Keeping those layers separate will be important. Players should only see
what their characters are allowed to see.

------------------------------------------------------------------------

# 2. User Roles

## Player

A player operates one or more characters and can:

-   Log into their account.
-   Access their character's in-world devices.
-   Send and receive text messages.
-   Send and receive emails.
-   Browse in-world websites.
-   Read available news articles.
-   View files, images, contacts, and other unlocked content.
-   Receive communications from NPCs.
-   Participate in group conversations.

## Game Master

The GM has full campaign control and can:

-   Create and manage players and characters.
-   Create NPC identities.
-   Send messages and emails as NPCs.
-   Build websites and news articles.
-   Control who can access specific content.
-   Schedule communications for later delivery.
-   Create hidden content and reveal it during play.
-   Review player interactions when appropriate.
-   Manage the campaign timeline and world state.

## Administrator

Initially, the GM and administrator can be the same role.

Administrative capabilities include:

-   Managing accounts and passwords.
-   Configuring the custom domain.
-   Managing backups.
-   Reviewing errors and system activity.
-   Setting global application preferences.
-   Managing storage and uploaded files.

A separate administrator role may only become necessary if someone other
than the GM maintains the server.

------------------------------------------------------------------------

# 3. Major Feature Groups

## Epic A: Accounts and Authentication

This provides the foundation for every other system.

### Core features

-   Account registration or GM-created accounts.
-   Secure login and logout.
-   Password reset.
-   Persistent sessions.
-   Player profile.
-   Role-based permissions.
-   Account activation and deactivation.

### Character access

A player account should not necessarily be identical to an in-world
identity.

A player could have:

-   One real account.
-   One or more campaign characters.
-   A separate in-world email address for each character.
-   A separate phone number or messaging identity for each character.

This separation would allow a player to participate in multiple
campaigns or operate temporary characters without needing multiple login
accounts.

### Later features

-   Two-factor authentication.
-   Login history.
-   Social login through Google or Discord.
-   Campaign invitations.
-   Multiple campaigns under one account.

------------------------------------------------------------------------

## Epic B: Campaign Management

The campaign should be the main container for all data.

Each campaign could contain:

-   Players.
-   Player characters.
-   NPCs.
-   Messages.
-   Emails.
-   Websites.
-   News articles.
-   Files.
-   Factions.
-   Locations.
-   Campaign dates.
-   Permissions.
-   GM notes.

### Core features

-   Create a campaign.
-   Edit campaign name and description.
-   Add and remove players.
-   Assign characters to players.
-   Archive a campaign.
-   Configure campaign-wide visual styling.

### Campaign membership

Each player should only see campaigns they have joined.

A campaign could also have statuses such as:

-   Preparation.
-   Active.
-   Paused.
-   Completed.
-   Archived.

------------------------------------------------------------------------

## Epic C: Character Profiles and In-World Identities

Each character needs a digital identity within the application.

### Character information

-   Legal name.
-   Alias or handle.
-   Portrait.
-   Role or class.
-   Affiliation.
-   Biography.
-   Email address.
-   Phone number.
-   Contact list.
-   Public profile information.
-   Private GM notes.

### Optional game information

The application could eventually include:

-   Humanity.
-   Reputation.
-   Street Cred.
-   Eurobucks.
-   Inventory.
-   Cyberware.
-   Weapons.
-   Injuries.
-   Character statistics.
-   Active jobs or quests.

These RPG-management features should probably remain outside the initial
version unless they directly support the messaging and web experience.

------------------------------------------------------------------------

## Epic D: NPC Identity System

NPCs should function like real users inside the fictional world without
needing actual login accounts.

### NPC features

-   Name.
-   Alias.
-   Portrait.
-   Email address.
-   Phone number.
-   Organization.
-   Faction.
-   Personality notes.
-   Relationship to player characters.
-   Public profile.
-   GM-only notes.

### NPC communication

The GM should be able to:

-   Send messages as an NPC.
-   Send emails as an NPC.
-   Add an NPC to group chats.
-   Reply to existing conversations.
-   Schedule NPC responses.
-   Save draft responses.
-   quickly switch between NPC identities.

The GM interface should always make it obvious which identity is
currently selected to prevent accidentally sending a message as the
wrong NPC.

------------------------------------------------------------------------

# 4. Communication Systems

## Epic E: Text Messaging

This system should resemble an in-world phone or messaging application.

### Core features

-   One-to-one conversations.
-   Player-to-player messaging.
-   Player-to-NPC messaging.
-   NPC-to-player messaging.
-   Conversation history.
-   Message timestamps.
-   Unread message indicators.
-   Notifications.
-   Character portraits or contact icons.

### Group conversations

-   Create group chats.
-   Add or remove participants.
-   Group chat name.
-   Group chat image.
-   Messages from both players and NPCs.
-   GM-controlled NPC participation.

### Message content

Initial support:

-   Plain text.
-   Basic line breaks.
-   Links to internal content.

Later support:

-   Images.
-   Attachments.
-   Voice-message simulations.
-   Location pins.
-   Contact cards.
-   Reactions.
-   Deleted or edited messages.
-   Glitched, corrupted, or intercepted messages.

### In-world behavior options

The GM could optionally control:

-   Delayed delivery.
-   Failed delivery.
-   Unknown sender.
-   Spoofed sender identity.
-   Blocked contacts.
-   Signal loss.
-   Read receipts.
-   Character-specific phone numbers.

These would provide strong narrative tools but should come after the
basic messaging system works reliably.

------------------------------------------------------------------------

## Epic F: Email

Email should feel more formal and information-heavy than text messaging.

### Core features

-   Inbox.
-   Sent folder.
-   Drafts.
-   Archived messages.
-   Trash.
-   Compose email.
-   Reply.
-   Reply all.
-   Forward.
-   Unread indicators.
-   Sender and recipient fields.
-   Subject line.
-   Message body.
-   Timestamp.

### Recipients

Emails could be sent to:

-   Individual player characters.
-   NPCs.
-   Multiple recipients.
-   Organizations.
-   Mailing lists.

### Attachments

Later versions could support:

-   Images.
-   PDFs.
-   Text files.
-   Contracts.
-   Maps.
-   Schematics.
-   Audio files.
-   Encrypted files.
-   Links to internal websites.

### GM tools

-   Send email as any NPC.
-   Schedule email delivery.
-   Create drafts.
-   Clone an existing email.
-   Send the same email to multiple characters.
-   Personalize an email for each recipient.
-   Mark email as urgent, corporate, spam, or encrypted.

------------------------------------------------------------------------

## Epic G: Notifications

Players should be alerted when something changes.

### In-app notifications

-   New text message.
-   New email.
-   New group-chat message.
-   New article.
-   New website access.
-   Newly available file.
-   Campaign announcement.

### External notifications

Possible later options:

-   Browser push notifications.
-   Email notifications to the player's real email address.
-   Discord notifications.
-   Mobile push notifications if the application later becomes a
    Progressive Web App.

Players should be able to control which external notifications they
receive.

------------------------------------------------------------------------

# 5. The In-World Internet

## Epic H: Web Browser Interface

Players should have an in-world browser where they can access fictional
websites.

The browser does not need to behave like a real unrestricted browser. It
can display pages created and hosted inside the application.

### Core browser features

-   Homepage.
-   Address bar.
-   Bookmarks.
-   Browser history.
-   Back and forward navigation.
-   Search page.
-   Internal URLs.
-   Access-denied pages.
-   Not-found pages.

Example fictional addresses:

-   `www.n54news.com`
-   `nightcitytransit.com`
-   `trauma-team.net`
-   `afterlife.board`
-   `citynet/local/news`

The application could translate these fictional addresses into internal
page IDs.

------------------------------------------------------------------------

## Epic I: Website Builder

The GM needs a way to create fictional websites without writing code.

### Website structure

A website could contain:

-   Website name.
-   Domain or fictional URL.
-   Logo.
-   Header.
-   Navigation menu.
-   Multiple pages.
-   Images.
-   Text sections.
-   Links.
-   Contact information.
-   Downloadable files.

### Website templates

Useful templates could include:

-   Corporate website.
-   News outlet.
-   Personal blog.
-   Government website.
-   Nightclub.
-   Restaurant.
-   Store.
-   Gang or faction site.
-   Message board.
-   Darknet portal.
-   Classified advertisements.
-   Medical provider.
-   Police database.

### Access controls

A site or page could be:

-   Public.
-   Available only to selected characters.
-   Password protected.
-   Unlocked after a campaign event.
-   Hidden until the GM reveals it.
-   Accessible only through a direct link.
-   Available only from a certain fictional device or network.

------------------------------------------------------------------------

## Epic J: News System

News should function as a specialized type of website content.

### Article features

-   Headline.
-   Subheading.
-   Author.
-   Publication.
-   Publication date.
-   Article body.
-   Images.
-   Video placeholder.
-   Related articles.
-   Tags.
-   Comments, if enabled.

### News feeds

-   Global news.
-   Local news.
-   Corporate news.
-   Entertainment.
-   Crime.
-   Weather.
-   Sports.
-   Financial markets.
-   Faction-specific feeds.

### Narrative controls

The GM should be able to:

-   Publish immediately.
-   Schedule publication.
-   Backdate an article.
-   Target an article to selected characters.
-   Update an article after publication.
-   Publish contradictory versions through different news outlets.
-   Mark an article as propaganda or unreliable in GM-only metadata.

------------------------------------------------------------------------

# 6. Content and Information Systems

## Epic K: Files and Attachments

The campaign will likely need a central file system.

### Supported content

-   Images.
-   PDFs.
-   Text documents.
-   Audio.
-   Video links.
-   Maps.
-   Schematics.
-   Contracts.
-   Personnel records.
-   Evidence.
-   Character dossiers.

### File properties

-   File name.
-   File type.
-   Description.
-   Uploaded by.
-   Created date.
-   In-world date.
-   Access permissions.
-   Related character, message, email, website, or mission.
-   GM-only notes.

### Narrative states

Files could optionally be:

-   Encrypted.
-   Corrupted.
-   Partially recovered.
-   Classified.
-   Redacted.
-   Locked behind a password.
-   Revealed after a successful game action.

The application does not initially need to perform real encryption.
These can be story states controlled by the GM.

------------------------------------------------------------------------

## Epic L: Contacts and Directory

Each character should have an in-world contact list.

### Contact information

-   Name.
-   Alias.
-   Portrait.
-   Phone number.
-   Email.
-   Organization.
-   Notes.
-   Favorite status.
-   Blocked status.

### Contact visibility

A contact can be:

-   Known from the beginning.
-   Added automatically after receiving a message.
-   Manually added by the player.
-   Hidden until revealed by the GM.
-   Shared by another character.

------------------------------------------------------------------------

## Epic M: Search

As campaign content grows, search will become essential.

Players could search:

-   Messages.
-   Emails.
-   Contacts.
-   News articles.
-   Websites.
-   Files.

The GM could search across the entire campaign, including hidden
content.

Search results must respect character permissions. A player should never
discover hidden content through search results, previews, URLs, or
metadata.

------------------------------------------------------------------------

# 7. Game Master Control Center

## Epic N: GM Dashboard

The GM dashboard should be the administrative center of the application.

### Dashboard overview

-   Recent player activity.
-   Unread NPC conversations.
-   Scheduled messages.
-   Draft content.
-   Recently published articles.
-   Active players.
-   Upcoming campaign events.
-   Content waiting to be revealed.

### Quick actions

-   Send text as NPC.
-   Send email as NPC.
-   Publish article.
-   Reveal website.
-   Upload file.
-   Create NPC.
-   Schedule communication.

------------------------------------------------------------------------

## Epic O: Content Scheduling

Scheduling would greatly reduce the GM's workload during sessions.

The GM could schedule:

-   Text messages.
-   Emails.
-   News articles.
-   Website changes.
-   File availability.
-   Notifications.

### Scheduling methods

-   Real-world date and time.
-   Manual release button.
-   Campaign date and time.
-   Triggered by a campaign event.

The first version should support real-world scheduling and manual
release. Event-triggered automation can be added later.

------------------------------------------------------------------------

## Epic P: Content Permissions and Reveals

Every major content type should share the same permission model.

Possible visibility rules:

-   GM only.
-   All campaign players.
-   Specific players.
-   Specific characters.
-   Members of a group.
-   Characters with a particular tag.
-   Anyone possessing a direct link.
-   Public after a scheduled date.
-   Hidden until manually released.

This permission system should be designed early rather than added
separately to every feature.

------------------------------------------------------------------------

## Epic Q: Campaign Timeline

A timeline would help synchronize communications and events.

### Timeline features

-   Real-world timestamp.
-   In-world timestamp.
-   Campaign event name.
-   Related messages.
-   Related emails.
-   Related articles.
-   Related websites.
-   GM notes.

This could eventually allow players to review the campaign
chronologically.

------------------------------------------------------------------------

# 8. Immersion and Visual Design

## Epic R: Cyberpunk User Interface

The application should have a consistent fictional operating-system
style.

### Visual elements

-   Neon accents.
-   Dark backgrounds.
-   Industrial typography.
-   Glitch effects.
-   Scan lines.
-   Animated panels.
-   Device boot screens.
-   Fictional network indicators.
-   Character portraits.
-   Corporate branding.

### Accessibility requirements

Immersion should not make the application difficult to use.

Include:

-   Reduced-motion mode.
-   High-contrast mode.
-   Adjustable text size.
-   Keyboard navigation.
-   Screen-reader-friendly structure.
-   Option to disable visual distortion.
-   Clear mobile layouts.

Glitch effects and animations should be decorative, not required for
understanding content.

------------------------------------------------------------------------

## Epic S: Device Simulation

A later version could present different content through simulated
devices.

Examples:

-   Agent or smartphone.
-   Desktop computer.
-   Public terminal.
-   Corporate workstation.
-   Vehicle interface.
-   Encrypted shard reader.

A device could determine which applications and websites are accessible.
This would be highly immersive but considerably increases complexity, so
it should not be part of the initial release.

------------------------------------------------------------------------

# 9. Technical and Operational Features

## Epic T: Data Storage

The application will need persistent storage for:

-   Accounts.
-   Campaigns.
-   Characters.
-   NPCs.
-   Messages.
-   Emails.
-   Websites.
-   Articles.
-   Permissions.
-   Attachments.
-   Notifications.
-   Activity records.

The system should be designed so content is never tied only to a browser
or device.

------------------------------------------------------------------------

## Epic U: Security

Even though the application is private, it will store credentials and
private conversations.

Required security features include:

-   Password hashing.
-   HTTPS.
-   Secure session handling.
-   Permission checks on every protected request.
-   Protection against common web attacks.
-   File-upload validation.
-   Login rate limiting.
-   Secure password resets.
-   Restricted GM routes.
-   Environment-based secret storage.

One especially important rule: hiding something in the user interface is
not sufficient. The server must independently verify that the user has
permission to access each piece of content.

------------------------------------------------------------------------

## Epic V: Backups and Recovery

The campaign could represent hundreds of hours of work.

Required features:

-   Automated database backups.
-   Uploaded-file backups.
-   Manual campaign export.
-   Campaign restore.
-   Recovery documentation.
-   Backup retention policy.

A future export package could contain campaign data in JSON plus
uploaded media files.

------------------------------------------------------------------------

## Epic W: Hosting and Custom Domain

Infrastructure requirements include:

-   Production server or managed hosting provider.
-   Custom domain.
-   DNS configuration.
-   HTTPS certificate.
-   Database hosting.
-   File storage.
-   Environment variables and secrets.
-   Deployment process.
-   Error logging.
-   Uptime monitoring.

The application should have separate development and production
environments so testing does not damage the live campaign.

------------------------------------------------------------------------

## Epic X: Audit and Activity Logs

The application should record important actions, especially GM actions.

Examples:

-   Account created.
-   Character assigned.
-   Message sent.
-   Article published.
-   Permission changed.
-   File revealed.
-   Content deleted.
-   Login attempt.
-   Scheduled event executed.

These logs will help diagnose mistakes and restore campaign continuity.

------------------------------------------------------------------------

# 10. Recommended Development Phases

## Phase 0: Product Definition

Before coding:

-   Define the initial campaign workflow.
-   Create interface sketches.
-   Decide how accounts, players, and characters relate.
-   Define the permission model.
-   Decide whether multiple campaigns must be supported immediately.
-   Select a technology stack.
-   Define deployment and backup plans.

### Deliverables

-   Feature specification.
-   Basic data model.
-   Wireframes.
-   Technical architecture.
-   Prioritized backlog.

------------------------------------------------------------------------

## Phase 1: Foundation

Build:

-   User accounts.
-   Authentication.
-   Player and GM roles.
-   Campaign creation.
-   Character creation.
-   NPC creation.
-   Basic permissions.
-   Production database.
-   Custom-domain deployment.

At the end of this phase, users should be able to securely log in and
access the correct campaign.

------------------------------------------------------------------------

## Phase 2: Text Messaging MVP

Build:

-   Contacts.
-   Player-to-player messages.
-   Player-to-NPC messages.
-   GM replies as NPCs.
-   Conversation history.
-   Unread counts.
-   Basic notifications.
-   Group chats, if time permits.

At the end of this phase, messaging should be fully usable during a
session.

------------------------------------------------------------------------

## Phase 3: Email MVP

Build:

-   Inbox.
-   Compose.
-   Reply.
-   Forward.
-   Sent mail.
-   Drafts.
-   NPC email identities.
-   Attachments.
-   Unread indicators.

------------------------------------------------------------------------

## Phase 4: In-World Web

Build:

-   Fictional browser.
-   Internal URLs.
-   Website builder.
-   Website templates.
-   Page permissions.
-   Links between websites.
-   News article system.

This phase creates the strongest *Cyberpunk 2077*-style experience.

------------------------------------------------------------------------

## Phase 5: GM Automation

Build:

-   Scheduled messages.
-   Scheduled emails.
-   Scheduled articles.
-   Manual content reveals.
-   Draft queue.
-   GM activity dashboard.
-   Campaign timeline.

------------------------------------------------------------------------

## Phase 6: Immersion and Polish

Build:

-   Cyberpunk visual theme.
-   Mobile optimization.
-   Device simulation.
-   Glitch and boot effects.
-   Browser push notifications.
-   Audio cues.
-   Reduced-motion and accessibility settings.

------------------------------------------------------------------------

## Phase 7: Advanced Narrative Systems

Possible features:

-   Encrypted messages.
-   Spoofed identities.
-   Hacking interfaces.
-   Password-protected websites.
-   Searchable databases.
-   Public message boards.
-   Classified advertisements.
-   Reputation system.
-   Jobs and quest tracking.
-   Eurodollar accounts.
-   Corporate and faction portals.
-   Automated NPC behavior.
-   AI-assisted NPC responses with GM approval.

------------------------------------------------------------------------

# 11. Proposed MVP

The first playable release should include only the features required to
support an actual game session:

1.  Secure player and GM login.
2.  One campaign.
3.  Player characters and NPC identities.
4.  One-to-one text conversations.
5.  Group text conversations.
6.  Email inbox and composition.
7.  GM ability to send as NPCs.
8.  Simple fictional websites.
9.  News articles.
10. Character-based access permissions.
11. Mobile-friendly interface.
12. Database backups.

The MVP should deliberately exclude:

-   Full character sheets.
-   Combat tracking.
-   Inventory management.
-   Real encryption.
-   AI-generated NPC responses.
-   Complex hacking minigames.
-   Multiple device simulations.
-   Native mobile applications.
-   Advanced automation.

Those features would be valuable later, but they could delay the core
application substantially.

------------------------------------------------------------------------

# 12. Initial Data Model

These are likely to become the main entities in the system:

``` text
User
Campaign
CampaignMembership
Character
NPC
Identity
Contact
Conversation
ConversationParticipant
TextMessage
EmailThread
EmailMessage
Website
WebPage
NewsPublication
NewsArticle
File
Notification
Permission
ScheduledEvent
CampaignTimelineEvent
AuditLog
```

The concept of an **Identity** may be especially useful. Both player
characters and NPCs could communicate through identities, allowing the
messaging systems to treat them consistently.

For example:

``` text
User Robert
└── controls Character Morgan
    └── uses Identity morgan@nightmail.net

GM
└── controls NPC Rogue
    └── uses Identity rogue@afterlife.nc
```

The text and email systems would communicate between identities rather
than directly between user accounts.

------------------------------------------------------------------------

# 13. Suggested Product Backlog Structure

Each feature should eventually be converted into a user story.

Example:

> As a player, I want to receive text messages from NPC contacts so that
> campaign information can reach my character through an immersive
> interface.

Each story should include:

-   User role.
-   Desired action.
-   Narrative or gameplay value.
-   Acceptance criteria.
-   Permission requirements.
-   Mobile behavior.
-   Error states.
-   Testing requirements.

Example acceptance criteria:

``` text
Given that a player controls Character A,
and NPC B sends Character A a message,
when the player opens the messaging application,
then the conversation with NPC B appears,
the message is marked unread,
and no other player can access the conversation.
```

------------------------------------------------------------------------

# 14. Important Design Decisions to Make Early

Before implementation begins, the project needs firm decisions on these
questions:

-   Can one user control multiple characters?
-   Will the application support multiple campaigns?
-   Can the GM read all player-to-player messages?
-   Can players message NPCs at any time?
-   Should messages appear instantly or wait for GM approval?
-   Will in-world time differ from real-world time?
-   Can players create their own group chats?
-   Can players upload files?
-   Can players create websites or articles?
-   Should deleted messages remain visible to the GM?
-   Will the site be primarily mobile, desktop, or equally both?
-   Is the experience presented as one unified operating system or
    several independent applications?
-   How much of the Cyberpunk RED character sheet should eventually be
    included?

The most consequential decisions are the relationship between **users,
characters, identities, and campaigns**, and the rules governing **who
can see each piece of content**. Those should be resolved before the
database or interface is designed.

## User

I'll go through these questions from number 14 one by one.

1.) One user in theory *should* be able to control multiple characters,
but for the minimum viable product a user need only access to one
character. 2.) The application should not be able to support multiple
campaigns. 3.) The GM should be able to read all player-to-player
messages. 4.) Players should be able to message NPCs at any time in
theory. 5.) Messages should appear instantly. 6.) In-world time will in
fact differ from real-world time. That being said, for an MVP it will
not even be necessary to track time at all. 7.) Yes. 8.) No. 9.) No.
10.) No, although I'm not sure. My instinct says no. 11.) I imagine it
to be primarily used on mobile, but it should be accessible via desktop.
12.) If I understand the question, it's several independent applications
accessible on one unified operating system. 13.) MVP will have no RED
character sheet information.

## Assistant

These are excellent constraints because they significantly narrow the
scope of the MVP. More importantly, they establish a philosophy for the
application: **this is an immersive communications operating system**,
not a virtual tabletop or character manager.

Below are my thoughts on each decision and what they imply
architecturally.

------------------------------------------------------------------------

# Decisions Locked In

## 1. One User → One Character (for MVP)

**Decision**

-   Future: one account may own multiple characters.
-   MVP: exactly one account controls exactly one character.

I would still design the database as though multiple characters are
possible.

Instead of

``` id="q8adpd"
User
```

think

``` id="1315cp"
User
    ↓
Character
```

rather than

``` id="eqjbeb"
User
    ↓
Messages
```

This tiny decision saves us from a painful database migration later.

------------------------------------------------------------------------

## 2. Single Campaign

Excellent.

This simplifies literally every system.

Instead of

``` id="lstt2w"
Campaign
    Characters
    Messages
    Websites
```

everything simply exists globally.

You can always introduce Campaign later.

------------------------------------------------------------------------

## 3. GM Can Read Everything

I actually like this.

This isn't WhatsApp.

It's a storytelling tool.

Therefore the GM becomes almost like the operating system administrator.

That means the GM dashboard can have things like

``` id="80750m"
Recent Messages

Player A
↓

Player B

"Meet me behind Totentanz."
```

which could become very useful.

------------------------------------------------------------------------

## 4. Players Can Message NPCs Anytime

Good.

This means NPCs are "offline" only because the GM hasn't answered yet.

The application doesn't need to know whether Rogue is "online."

------------------------------------------------------------------------

## 5. Instant Delivery

Very good.

This means we don't need message queues for MVP.

Player hits Send.

Database stores message.

Recipient receives notification.

Done.

------------------------------------------------------------------------

## 6. Ignore Time

Perfect.

Time systems explode in complexity.

Don't build one until you actually need it.

------------------------------------------------------------------------

## 7. Player-created Group Chats

I like this.

That means group chats behave exactly like Discord.

Examples

``` id="ff9cjs"
Edgerunners

Morgan
Rogue
Panam
Dex
```

or

``` id="2lyqz9"
Team Alpha

Player A
Player B
Player C
```

------------------------------------------------------------------------

## 8. No Player File Uploads

Huge simplification.

Only the GM creates content.

That means there are no concerns over

-   malicious uploads
-   storage quotas
-   moderation
-   inappropriate content

------------------------------------------------------------------------

## 9. No Player Websites

Again, good.

The Internet becomes a curated world.

Players consume.

GM creates.

------------------------------------------------------------------------

## 10. Deleted Messages

I agree with your instinct.

I'd actually recommend **never deleting messages**.

Instead:

``` id="1zhb5q"
Visible

Hidden

Archived
```

Internally everything remains.

This is much easier than true deletion.

------------------------------------------------------------------------

## 11. Mobile First

This is probably the most important answer.

Everything should be designed like a phone OS.

Not like Gmail.

Not like Outlook.

Think...

``` id="usc95e"
Cyberpunk Phone

Messages

Mail

Browser

Contacts

News
```

Desktop merely stretches the interface.

------------------------------------------------------------------------

## 12. One Operating System

This is actually my favorite answer.

I think of it like this.

``` id="s2tcxe"
NightOS

Home Screen

──────────────

Messages

Mail

Browser

Contacts

News

Settings
```

Each icon launches its own app.

Exactly like an iPhone.

Not one giant webpage.

------------------------------------------------------------------------

## 13. No Character Sheet

I strongly agree.

Character sheets already exist.

Dice rollers already exist.

Inventory managers already exist.

Your application becomes something unique.

It becomes the **digital world**.

------------------------------------------------------------------------

# What I Think This Project Actually Is

This answer changed how I think about the application.

Originally I pictured

``` id="kbpb18"
Campaign Manager
```

Now I picture

``` id="hg7ner"
Cyberpunk Smartphone Simulator
```

Those are very different.

Instead of asking

> "How do we manage a campaign?"

we ask

> "What software would exist on an Agent in Night City?"

That's a much more focused design lens.

------------------------------------------------------------------------

# I Would Actually Rename Several Epics

Instead of

``` id="ztsopp"
Messaging
Email
Browser
News
```

I'd think in terms of installed applications.

``` id="r3ie0c"
NightOS

├── Messages
├── Mail
├── Browser
├── Contacts
├── News
├── Settings
└── Home Screen
```

Everything becomes an app.

That makes future expansion extremely easy.

For example later you can add

``` id="b3kl0j"
Banking

Maps

Trauma Team

Taxi

Police Scanner

NetWatch

NCPD Database

Auction House

Music

Camera

Gallery
```

without changing the overall architecture.

------------------------------------------------------------------------

# One Additional Design Principle I'd Establish Early

I would add a guiding principle to the project documentation:

> **Everything the player interacts with should feel like software
> running on their character's personal Agent, not like pages on a
> traditional website.**

That single sentence answers hundreds of future design questions. If a
feature feels like opening an app on a futuristic smartphone, it's
probably aligned with the vision. If it feels like navigating an admin
website, it probably belongs behind the GM interface instead.

------------------------------------------------------------------------

## Revised MVP

With your answers, I'd actually trim the MVP even further:

1.  Login
2.  Home screen (NightOS)
3.  Messages app
4.  Mail app
5.  Browser app
6.  Contacts app
7.  News app
8.  GM Control Panel
9.  NPC management
10. Website/page editor
11. Mobile-responsive UI
12. Permissions system

Everything else---including scheduling, timelines, character sheets,
inventories, and advanced automation---can wait until after the core
experience is enjoyable. If the application nails the feeling of pulling
out your Agent during a session to check a message from a fixer or
browse a corporation's website, it will already accomplish something few
Cyberpunk RED tools currently offer.

## User

Moving forward within the context of this project, avoid using general
references to "yourself" as though you are a person, and overly flagrant
and flattering statements like "this isn't X. It's Y." I find those
things distracting rather than useful, so do not do it again.

## Assistant

Understood. That preference has been saved and will be applied going
forward.

Specifically, future responses in this project will: - Avoid referring
to the assistant as though it were a person when that wording isn't
necessary. - Avoid rhetorical constructions like "this isn't X. It's Y."
and similar emphatic contrasts. - Avoid unnecessary praise or framing
that doesn't add technical value. - Favor direct, matter-of-fact
explanations focused on design decisions, tradeoffs, and implementation
details.

For a software architecture project like this, the goal will be to keep
discussions closer to an engineering design review than a motivational
conversation.

## User

\[Two images attached.\]

In the previous MVP, let's replace the news app with a datashard app.
This will be easier to implement and use. Also, I have a pretty clear
vision of what the end product will look like in my head, so let's focus
on that.

The first photo is of what a datashard looks like. The idea here is that
I can push a datashard to one or more players and they'll be capable of
reading it easily. This would be analogous to me giving the players a
handout during the session.

The second photo is similar to how I imagine the final product to look,
with tabs that access the different apps. Some notable differences
exist, such as how I think in a mobile format the horizontal tabs
selection is not the way to go.

## Assistant

Replacing **News** with **Datashards** in the MVP is a good change. It
removes a fair amount of complexity while preserving one of the most
useful pieces of tabletop functionality: delivering information to
players in a way that feels native to the world.

Looking at the two reference images, they suggest two separate design
directions:

-   **Datashards** define how individual pieces of information are
    presented.
-   **The terminal interface** defines how the operating system is
    organized.

Those should remain separate concepts in the application architecture.

------------------------------------------------------------------------

# Revised MVP

Instead of:

-   Messages
-   Mail
-   Browser
-   Contacts
-   News

the MVP becomes:

-   Messages
-   Mail
-   Browser
-   Contacts
-   **Datashards**

The GM Panel remains outside of the player-facing operating system.

------------------------------------------------------------------------

# Datashards

From a software perspective, a datashard is not just a text document. It
is a distinct content type.

It should have its own model.

``` id="yxi0th"
Datashard
----------
Title
Body
Author (optional)
Icon
Color Theme
Created Date
Created By
Recipients
Visibility
Tags
```

Later, additional fields could be added without affecting the basic
reader:

-   Image
-   Audio log
-   Embedded file
-   Corruption effects
-   Encryption state
-   Required password
-   Linked website
-   Linked NPC
-   Mission association

For the MVP, however, a datashard can simply be a formatted document.

------------------------------------------------------------------------

# Delivering Datashards

One workflow that feels natural is:

``` id="il2y53"
GM creates Datashard

↓

Select recipients

↓

Push

↓

Recipients receive notification

↓

Datashard appears inside Datashards app
```

This mirrors handing players a physical note during a session.

Importantly, a datashard should **persist** after being delivered.
Players can reopen it later rather than losing it after dismissal.

------------------------------------------------------------------------

# Datashard Organization

The app itself does not need to be complicated.

Think of it like a document library.

``` id="ps6zb7"
DATASHARDS

> Militech Briefing

> Recorded Conversation

> Apartment Lease

> Fixer's Instructions

> Corpo Security Report

> Unknown Encrypted File
```

Selecting one opens the reading view similar to your first reference
image.

------------------------------------------------------------------------

# Datashard Reader

The first image already demonstrates a layout that translates well to
both desktop and mobile.

``` id="77im5t"
────────────────────────────

◈ TITLE

────────────────────────────

Document contents...

Document contents...

Document contents...

────────────────────────────
```

The visual treatment can imitate Cyberpunk's UI without reproducing it
exactly.

For example:

-   Accent color
-   Decorative corners
-   Thin borders
-   Custom scrollbar
-   Monospaced or futuristic font
-   Slight scanline texture

The actual reader should remain extremely readable.

One lesson from Cyberpunk 2077 is that some datashards sacrifice
readability for style. Since this is intended for use during a live
game, readability should take priority.

------------------------------------------------------------------------

# The Operating System

The second image reinforces a design direction that has been emerging
throughout this discussion.

Rather than thinking in terms of webpages, think in terms of
applications running inside an operating system.

For example:

``` id="ttd0jk"
NightOS

Home

Messages

Mail

Browser

Contacts

Datashards

Settings
```

Each application owns its own navigation and state.

------------------------------------------------------------------------

# Mobile Navigation

This is one place where departing from Cyberpunk 2077's interface is
likely the right decision.

Horizontal tabs work well on a 16:9 monitor.

They are much less comfortable on a phone.

A mobile-first approach suggests a persistent bottom navigation bar.

For example:

``` id="nv65hm"
────────────────────────

 Messages

 Mail

 Home

 Browser

 More

────────────────────────
```

Where **More** opens:

``` id="unp74g"
Contacts

Datashards

Settings
```

Alternatively, if the home screen resembles a smartphone, there may be
**no persistent navigation bar at all**. Instead:

1.  User logs in.
2.  User arrives at a home screen.
3.  Icons launch individual apps.
4.  Every app has a consistent back/home mechanism.

That approach more closely matches the mental model of using an actual
device.

------------------------------------------------------------------------

# Home Screen

One addition worth considering---even for the MVP---is a simple home
screen.

Instead of logging directly into Messages, users would see something
like:

``` id="mo8k5z"
09:42

──────────────

Messages

Mail

Browser

Contacts

Datashards

Settings

──────────────

New Message

1 New Datashard
```

This provides a single place for notifications and application
launching.

------------------------------------------------------------------------

# GM Workflow

The GM interface should remain completely separate from the in-world
operating system.

For example:

``` id="2enudu"
GM Dashboard

Characters

NPCs

Messages

Mail

Datashards

Browser Pages

Settings
```

Creating a datashard might look like:

``` id="85ommk"
New Datashard

Title

Body

Recipients

[ ] Morgan

[ ] Alice

[ ] James

Push

Save Draft
```

The players never see this interface.

------------------------------------------------------------------------

# A Principle Worth Adopting

One architectural principle would simplify future expansion:

> Every item a player can open should be treated as an application or a
> document, not as a special case.

For example:

-   Messages opens conversations.
-   Mail opens emails.
-   Browser opens web pages.
-   Datashards opens documents.

Each application owns its own data model and interface, but they all fit
within the same operating system framework. That consistency will make
it much easier to add future applications---such as Maps, Banking, or a
Police Scanner---without redesigning the rest of the system.

## User

Alright, so insofar as getting started, here's the truth - I have never
been part of a software engineering team, nor have I ever created an
architecture from the ground up. I have not decided what to use for
backend or frontend, but I think what makes the most sense to me is Java
backend with a JavaScript React Node.js frontend. This is something I've
some amount of experience in and I could deepen that.

Let's split this project into discrete features from the ground up so
that we have a process to bring us from nothing to the MVP. Don't start
writing code yet.

## Assistant

A sensible starting stack is:

-   **Backend:** Java with Spring Boot
-   **Frontend:** React with JavaScript or TypeScript
-   **Frontend tooling:** Node.js for package management, development
    tooling, and builds
-   **Database:** PostgreSQL
-   **Deployment:** decided later, after the application works locally

One terminology adjustment: Node.js would not normally be the frontend
itself. React runs in the browser; Node.js supports the React
development and build process.

The project should be organized around small, testable vertical features
rather than building the entire backend first and then the entire
frontend.

# 1. Define the MVP Precisely

The MVP should allow:

1.  A GM and several players to log in.
2.  Each player account to control one character.
3.  Players to navigate a mobile-first operating-system interface.
4.  Players to send and receive direct messages.
5.  Players to create group conversations.
6.  Players to send messages to NPCs.
7.  The GM to read every conversation.
8.  The GM to respond using NPC identities.
9.  Players to send and receive in-world emails.
10. The GM to create and distribute datashards.
11. Players to browse GM-created in-world web pages.
12. Players to view their contacts.
13. Data to persist between sessions.

Explicitly excluded from the MVP:

-   Multiple campaigns
-   Character sheets
-   Inventory
-   In-world time
-   Scheduling
-   Player file uploads
-   Player-created websites
-   AI-controlled NPCs
-   Native mobile apps
-   Hacking minigames
-   Full deletion of messages
-   Complex notification services

That scope becomes the boundary for every later decision.

------------------------------------------------------------------------

# 2. High-Level System Shape

The application can initially be divided into four major parts.

``` text
Browser
   |
React frontend
   |
Spring Boot REST API
   |
PostgreSQL database
```

A real-time messaging component will eventually be added:

``` text
Browser
   |
React frontend
   |
Spring Boot REST API + WebSocket connection
   |
PostgreSQL database
```

The REST API handles ordinary data operations. WebSockets handle instant
message delivery and live notifications.

The two main interfaces are:

``` text
Player Interface
GM Interface
```

They can be part of the same React application, with different routes
and permissions.

------------------------------------------------------------------------

# 3. Core Domain Concepts

Before designing screens, define the primary things the application
stores.

## User

Represents a person who can log in.

Fields will eventually include:

``` text
id
username
passwordHash
role
active
createdAt
```

Roles:

``` text
PLAYER
GM
```

## Character

Represents the player's in-world identity.

``` text
id
userId
name
handle
portrait
emailAddress
phoneNumber
```

For the MVP, one user controls one character. The relationship should
still be designed so multiple characters can be supported later.

## NPC

Represents a GM-controlled in-world identity.

``` text
id
name
handle
portrait
emailAddress
phoneNumber
notes
```

## Conversation

Represents a direct or group text conversation.

``` text
id
name
type
createdAt
```

Types:

``` text
DIRECT
GROUP
```

## Conversation Participant

Connects characters and NPCs to conversations.

``` text
conversationId
identityId
```

## Text Message

``` text
id
conversationId
senderIdentityId
body
createdAt
```

## Email

``` text
id
senderIdentityId
subject
body
createdAt
```

Emails also require recipient records so one email can go to multiple
identities.

## Datashard

``` text
id
title
body
createdBy
createdAt
status
```

## Datashard Recipient

``` text
datashardId
characterId
deliveredAt
readAt
```

## Web Page

``` text
id
title
slug
body
published
```

## Contact

``` text
ownerCharacterId
contactIdentityId
displayName
notes
```

## Identity

A useful abstraction may be introduced early:

``` text
Identity
---------
id
type
characterId
npcId
displayName
portrait
emailAddress
phoneNumber
```

Then messages and emails reference an identity rather than separately
supporting characters and NPCs.

This avoids logic such as:

``` text
message sender is either a player character or an NPC
```

Instead:

``` text
message sender is always an identity
```

That is likely the cleanest long-term design.

------------------------------------------------------------------------

# 4. Development Strategy

The application should be developed through **vertical slices**.

A vertical slice includes:

-   Database changes
-   Backend endpoint
-   Business logic
-   Frontend screen
-   Permissions
-   Validation
-   Tests

For example, "Create a datashard" should not be divided into unrelated
backend and frontend projects. It should be completed end-to-end:

``` text
Database table
→ Java entity
→ service
→ API endpoint
→ GM form
→ recipient view
→ tests
```

Each slice should leave the application in a working state.

------------------------------------------------------------------------

# 5. Phase 0 --- Project Definition

No production code should begin until the basic rules are documented.

## Feature 0.1: Product Requirements

Create a short requirements document containing:

-   Purpose of the application
-   User roles
-   MVP applications
-   Out-of-scope features
-   Basic security expectations
-   Mobile-first requirement
-   Single-campaign limitation

## Feature 0.2: Terminology

Agree on consistent terms.

Recommended vocabulary:

``` text
User       = person with login credentials
Character  = player-controlled in-world person
NPC        = GM-controlled in-world person
Identity   = messaging/email identity used by either a character or NPC
App        = player-facing OS application
GM Panel   = administrative interface
Datashard  = GM-created handout
Web Page   = page displayed in the fictional browser
```

## Feature 0.3: User Flows

Document the main actions.

Example player flow:

``` text
Open site
→ Log in
→ See home screen
→ Open Messages
→ Select conversation
→ Send message
→ Receive reply instantly
```

Example GM datashard flow:

``` text
Log in
→ Open GM Panel
→ Create datashard
→ Select recipients
→ Publish
→ Players receive notification
→ Players open datashard
```

## Feature 0.4: Rough Wireframes

Create simple layouts for:

-   Login
-   Player home screen
-   Messages list
-   Message conversation
-   Mail inbox
-   Email reader
-   Datashard list
-   Datashard reader
-   Browser
-   Contacts
-   GM dashboard
-   GM NPC management
-   GM datashard editor

These should be basic boxes and labels, not polished artwork.

## Completion Criteria

Phase 0 is complete when:

-   The MVP is written down.
-   Important terminology is stable.
-   Major user flows are documented.
-   Every primary screen has a rough wireframe.

------------------------------------------------------------------------

# 6. Phase 1 --- Repository and Application Skeleton

This phase creates a running but mostly empty system.

## Feature 1.1: Source-Control Repository

Create a Git repository.

A straightforward structure would be:

``` text
cyberpunk-ttrpg-app/
├── backend/
├── frontend/
├── docs/
├── README.md
└── .gitignore
```

A single repository is easier for one developer than separate frontend
and backend repositories.

## Feature 1.2: Backend Skeleton

Create a Spring Boot project with:

-   Web support
-   Validation
-   Spring Data JPA
-   PostgreSQL driver
-   Security
-   Database migrations
-   Testing dependencies

The initial backend only needs:

``` text
GET /api/health
```

Response:

``` json
{
  "status": "ok"
}
```

## Feature 1.3: Frontend Skeleton

Create the React project.

Recommended additions:

-   TypeScript
-   React Router
-   API client wrapper
-   Basic component folder structure
-   Basic CSS strategy

TypeScript is worth considering even with limited experience because the
application will contain many structured data objects.

## Feature 1.4: Local Database

Run PostgreSQL locally, likely through Docker Compose.

The development environment becomes:

``` text
React development server
Spring Boot application
PostgreSQL container
```

## Feature 1.5: Frontend-to-Backend Connection

The frontend should call the backend health endpoint and display a
development status indicator.

## Completion Criteria

-   One command or documented process starts the database.
-   Spring Boot starts successfully.
-   React starts successfully.
-   React can call the backend.
-   The project is committed to Git.

------------------------------------------------------------------------

# 7. Phase 2 --- Database and Migration Foundation

Database changes should be version-controlled from the start.

## Feature 2.1: Database Migration Tool

Use either:

-   Flyway
-   Liquibase

Flyway is likely simpler for this project.

Each schema change becomes a numbered migration.

Example:

``` text
V1__create_users.sql
V2__create_characters.sql
V3__create_identities.sql
```

## Feature 2.2: Base Audit Fields

Most records should have:

``` text
createdAt
updatedAt
```

Some may also need:

``` text
createdBy
```

## Feature 2.3: Development Seed Data

Provide test data for local development:

-   One GM
-   Two players
-   Two characters
-   Several NPCs

This prevents manually recreating test users every time.

## Completion Criteria

-   A completely empty database can be created from migrations.
-   Development test data can be loaded reliably.
-   Database structure is documented at a basic level.

------------------------------------------------------------------------

# 8. Phase 3 --- Authentication and Authorization

Authentication should be completed before private application data is
added.

## Feature 3.1: User Accounts

The GM can initially create accounts manually through seed data or a
temporary administrative process.

MVP account data:

``` text
username
password
role
active
```

Public self-registration is unnecessary.

## Feature 3.2: Login

Player enters:

-   Username
-   Password

The backend verifies the credentials.

## Feature 3.3: Session Strategy

Two common choices are:

-   Secure server-side session cookies
-   JWT access tokens

For a private browser-based application, secure HTTP-only cookies are
often simpler and safer than storing JWTs in browser storage.

## Feature 3.4: Current User Endpoint

``` text
GET /api/me
```

Returns information about the logged-in user and their assigned
character.

## Feature 3.5: Route Protection

Frontend routes:

``` text
/login
/app/*
/gm/*
```

Rules:

-   Unauthenticated users go to login.
-   Players cannot enter GM routes.
-   GM-only backend endpoints independently verify the GM role.

## Feature 3.6: Logout

The session is invalidated and the user returns to login.

## Completion Criteria

-   GM and player accounts can log in.
-   Sessions persist across page refreshes.
-   Players cannot access GM routes.
-   Backend permission checks are tested.

------------------------------------------------------------------------

# 9. Phase 4 --- Character, Identity, and NPC Foundation

Every communication feature depends on identities.

## Feature 4.1: Character Profile

A logged-in player can retrieve their character profile.

MVP profile:

``` text
name
handle
portrait
emailAddress
phoneNumber
```

Editing may initially be GM-only.

## Feature 4.2: Identity Model

Create an identity for every character and NPC.

Communications should reference identity IDs.

## Feature 4.3: GM NPC Management

GM can:

-   View NPC list
-   Create NPC
-   Edit NPC
-   Activate or deactivate NPC

MVP NPC fields:

``` text
name
handle
portrait
emailAddress
phoneNumber
```

## Feature 4.4: Identity Selector

The GM interface should have a clear selector when acting as an NPC.

Example:

``` text
Currently acting as:
[ Dakota Smith ▼ ]
```

The active identity should always be visible when sending
communications.

## Completion Criteria

-   Every character has an identity.
-   GM can create an NPC identity.
-   Backend can return identities safely.
-   Players cannot alter NPCs.

------------------------------------------------------------------------

# 10. Phase 5 --- Player Operating-System Shell

Before building each app, build the shared container.

## Feature 5.1: Mobile Layout

The interface should prioritize narrow screens.

The shared shell includes:

-   Application header
-   Current app title
-   Back navigation
-   Home navigation
-   Notification indicator
-   Main content area

## Feature 5.2: Home Screen

The player sees application launchers:

``` text
Messages
Mail
Browser
Contacts
Datashards
```

Settings may be omitted from the first version unless needed.

## Feature 5.3: App Navigation

A mobile-friendly approach could use:

-   Home-screen icons
-   A persistent home button
-   A compact bottom navigation bar
-   An app drawer

A practical MVP option is:

``` text
Bottom navigation:
Home | Messages | Mail | Datashards | More
```

The More menu contains:

``` text
Browser
Contacts
Logout
```

## Feature 5.4: Desktop Adaptation

Desktop uses the same application structure with:

-   Wider content panels
-   Optional sidebar
-   More room for split views

Avoid creating separate mobile and desktop applications.

## Feature 5.5: Shared Visual Components

Create reusable components:

-   Panel
-   App header
-   List item
-   Empty-state view
-   Loading indicator
-   Error message
-   Notification badge
-   Confirmation dialog

## Completion Criteria

-   User can navigate between empty apps.
-   Navigation works on mobile and desktop widths.
-   Routes survive page refreshes.
-   Shared visual components are established.

------------------------------------------------------------------------

# 11. Phase 6 --- Contacts

Contacts are a smaller feature and provide useful groundwork for
messaging.

## Feature 6.1: Contact List

Player can view available contacts.

Each entry displays:

-   Name
-   Handle
-   Portrait
-   Contact type

## Feature 6.2: Contact Details

Selecting a contact displays:

-   Name
-   Portrait
-   Phone number
-   Email address
-   Optional short description

## Feature 6.3: Start Communication

From a contact, a player can later:

-   Start a text conversation
-   Compose an email

These buttons can initially route to unfinished placeholder screens
until those apps exist.

## Feature 6.4: GM Contact Assignment

The GM determines which NPC contacts each character knows.

Players should not automatically see every NPC.

## Completion Criteria

-   Players only see assigned contacts.
-   GM can assign and remove contacts.
-   Contact data supports later messaging and email workflows.

------------------------------------------------------------------------

# 12. Phase 7 --- Text Messaging

This should be the first major interactive application.

## Feature 7.1: Conversation List

Player sees conversations ordered by most recent activity.

Each item shows:

-   Conversation name
-   Last sender
-   Message preview
-   Timestamp
-   Unread count

## Feature 7.2: Direct Conversation

A direct conversation contains two participants.

Players can start conversations with known contacts.

## Feature 7.3: Group Conversations

Players can:

-   Create a group
-   Choose contacts
-   Name the group
-   Send messages

NPCs may be added when they are valid contacts.

## Feature 7.4: Send Message

Message requirements:

-   Non-empty body
-   Maximum length
-   Sender must belong to conversation
-   Message saved before delivery notification

## Feature 7.5: Conversation Reader

The player sees:

-   Participants
-   Ordered message history
-   Sender distinction
-   Composer
-   Automatic scroll behavior

## Feature 7.6: Instant Delivery

Add WebSocket support.

When a message is created:

1.  Backend saves it.
2.  Backend publishes an event.
3.  Connected recipients receive it.
4.  Conversation list updates.
5.  Unread count updates.

## Feature 7.7: Read State

Track whether each player has read each message or conversation.

A simpler MVP design is to track:

``` text
participant.lastReadAt
```

rather than a separate read receipt for every message.

## Feature 7.8: GM Conversation Oversight

GM can:

-   View all conversations
-   Search or filter conversations
-   Open any conversation
-   Read full message history

The interface should indicate when a conversation is player-only versus
involving an NPC.

## Feature 7.9: GM NPC Reply

GM selects an NPC identity and sends a reply in a conversation
containing that NPC.

Backend rules must confirm:

-   The selected NPC belongs to the conversation.
-   The sender is a GM.
-   The message is recorded under the NPC identity.

## Feature 7.10: Message Retention

For MVP:

-   Players cannot delete messages.
-   GM cannot permanently delete messages through the normal interface.
-   Optional hiding or archiving can be added later.

## Completion Criteria

-   Players can message each other.
-   Players can message NPCs.
-   Groups work.
-   Messages appear instantly.
-   GM can read everything.
-   GM can respond as valid NPC participants.

------------------------------------------------------------------------

# 13. Phase 8 --- Datashards

Datashards are a contained feature and should follow messaging.

## Feature 8.1: GM Datashard List

GM can view:

-   Draft datashards
-   Published datashards
-   Recipient count
-   Creation date

## Feature 8.2: Datashard Editor

MVP editor fields:

``` text
Title
Body
Recipients
```

Optional simple metadata:

``` text
Category
Author
```

Plain text or limited Markdown is sufficient initially.

## Feature 8.3: Draft and Publish States

States:

``` text
DRAFT
PUBLISHED
```

Drafts are invisible to players.

## Feature 8.4: Recipient Selection

GM can send to:

-   One character
-   Several characters
-   All players

## Feature 8.5: Datashard Delivery

Publishing creates recipient records and generates live notifications
for connected players.

## Feature 8.6: Player Datashard Library

Players see only datashards delivered to their character.

The list displays:

-   Title
-   Delivery date
-   Read/unread status

## Feature 8.7: Datashard Reader

The reader should support:

-   Clear title
-   Scrollable body
-   Mobile-readable typography
-   Read state
-   Back navigation

The visual style can draw from the first reference image while keeping
text readable.

## Completion Criteria

-   GM can draft and publish a datashard.
-   Selected players receive it instantly.
-   Datashards persist in each player's library.
-   Read status works.
-   Unauthorized players cannot access another player's datashards.

------------------------------------------------------------------------

# 14. Phase 9 --- Email

Email can reuse many identity and notification concepts from messaging.

## Feature 9.1: Mailbox

Player views:

-   Inbox
-   Sent

Drafts can be omitted initially if necessary.

## Feature 9.2: Compose Email

Fields:

``` text
To
Subject
Body
```

Recipients must be known contacts unless a later design allows arbitrary
addresses.

## Feature 9.3: Send Email

Email is stored immediately and appears in recipients' inboxes.

## Feature 9.4: Email Reader

Displays:

-   Sender
-   Recipients
-   Subject
-   Body
-   Timestamp

## Feature 9.5: Reply

Reply creates a new email connected to the original thread.

## Feature 9.6: Email Threads

Emails with replies should be grouped.

Potential model:

``` text
EmailThread
EmailMessage
EmailRecipient
```

## Feature 9.7: GM Oversight

GM can read all email threads, matching the message oversight rule.

## Feature 9.8: GM Sends as NPC

The GM selects an NPC identity and sends an email.

## Feature 9.9: Email Notifications

Connected recipients receive an immediate notification.

## Completion Criteria

-   Players can send and receive email.
-   NPC email works.
-   Replies remain grouped.
-   GM can inspect all email.
-   Inbox and unread state update correctly.

------------------------------------------------------------------------

# 15. Phase 10 --- Fictional Browser

Keep the first browser implementation deliberately simple.

## Feature 10.1: GM Page List

GM can:

-   Create page
-   Edit page
-   Publish page
-   Unpublish page

## Feature 10.2: Page Model

MVP fields:

``` text
Title
Slug
Body
Published
```

Example slug:

``` text
n54-news/local/arasaka-incident
```

## Feature 10.3: Simple Page Editor

Use either:

-   Plain text with Markdown
-   A constrained rich-text editor

Markdown is easier to store, validate, and render safely.

## Feature 10.4: Internal Browser Address Bar

Players can enter a fictional address or navigate through page links.

The application translates fictional paths into database pages.

## Feature 10.5: Links Between Pages

GM can create internal links in page content.

## Feature 10.6: Access Rules

For MVP, choose one of two levels:

### Simplest version

Pages are either:

``` text
PUBLISHED
UNPUBLISHED
```

### Slightly richer version

Pages can also be assigned to selected characters.

The simpler version is preferable unless restricted web pages are needed
during the first campaign sessions.

## Feature 10.7: Browser History

Browser history can be local to the frontend for MVP.

Bookmarks and search can wait.

## Completion Criteria

-   GM can publish a web page.
-   Players can open it through the Browser app.
-   Internal links work.
-   Unpublished pages are inaccessible.
-   Page content is rendered safely.

------------------------------------------------------------------------

# 16. Phase 11 --- Unified Notifications

Notifications should become a shared system rather than each app
inventing its own.

## Feature 11.1: Notification Model

``` text
id
recipientUserId
type
title
relatedEntityId
createdAt
readAt
```

Types:

``` text
NEW_MESSAGE
NEW_EMAIL
NEW_DATASHARD
```

## Feature 11.2: Notification Center

Player can view recent notifications.

## Feature 11.3: App Badges

Examples:

``` text
Messages: 3
Mail: 1
Datashards: 2
```

## Feature 11.4: Live Notification Events

Use the existing WebSocket connection.

## Feature 11.5: Reconnection

When a player reconnects, the application retrieves unread data from the
server. WebSockets should improve responsiveness but should not be the
only source of truth.

## Completion Criteria

-   All three communication systems use one notification model.
-   Badges remain correct after refresh.
-   Temporary connection loss does not lose notifications.

------------------------------------------------------------------------

# 17. Phase 12 --- GM Dashboard

By this point, the GM needs a consolidated interface.

## Feature 12.1: Dashboard Summary

Display:

-   Recent conversations
-   Unread NPC conversations
-   Recent emails
-   Draft datashards
-   Published pages
-   Active users

## Feature 12.2: NPC Inbox

Show conversations and emails awaiting an NPC response.

This is especially useful because players may message NPCs at any time.

## Feature 12.3: Quick Identity Switching

The GM should be able to choose an NPC and see:

-   That NPC's text conversations
-   That NPC's emails
-   Known player contacts

## Feature 12.4: Global Activity Feed

Show recent activity such as:

``` text
Player A messaged Player B
Player C opened Datashard X
Player B emailed NPC Y
```

Care should be taken not to turn this into a complex audit system yet.

## Completion Criteria

-   GM can find outstanding player-to-NPC communications.
-   GM can manage content without navigating through player screens.
-   Selected NPC identity remains clear.

------------------------------------------------------------------------

# 18. Phase 13 --- Reliability and Security

This phase should happen continuously, but it also needs a focused
review before deployment.

## Feature 13.1: Input Validation

Validate:

-   Usernames
-   Message length
-   Email subject length
-   Datashard length
-   Page slugs
-   Recipient lists

## Feature 13.2: Content Sanitization

Rendered page and datashard content must not allow unsafe scripts.

## Feature 13.3: Authorization Tests

Test that:

-   Players cannot access other characters' private data.
-   Players cannot use NPC identities.
-   Players cannot call GM endpoints.
-   Players cannot retrieve unpublished datashards.
-   Players cannot inspect hidden pages.
-   GM can inspect permitted global communications.

## Feature 13.4: Error Handling

Frontend should provide consistent responses for:

-   Network failure
-   Expired session
-   Validation errors
-   Not found
-   Permission denied
-   Server failure

## Feature 13.5: Logging

Backend logs should record:

-   Startup errors
-   Authentication failures
-   Unexpected exceptions
-   WebSocket failures

Avoid logging passwords or complete private message bodies
unnecessarily.

## Feature 13.6: Rate Limits

At minimum, rate-limit:

-   Login attempts
-   Message sending
-   Expensive search endpoints

## Completion Criteria

-   Important authorization behavior has automated tests.
-   Unsafe content cannot execute.
-   Errors are understandable.
-   Logs are useful without exposing secrets.

------------------------------------------------------------------------

# 19. Phase 14 --- Testing

Testing should be introduced with each feature, not saved entirely for
the end.

## Backend Tests

### Unit tests

Test business rules in isolation.

Examples:

-   Player cannot send as NPC.
-   Datashard recipient must exist.
-   Conversation sender must be a participant.

### Integration tests

Test:

-   Database behavior
-   REST endpoints
-   Authentication
-   Permission enforcement

## Frontend Tests

Test important components and flows:

-   Login form
-   Conversation list
-   Message composer
-   Datashard reader
-   Protected routes

## End-to-End Tests

Automate a few critical workflows:

``` text
Player logs in and sends message
GM reads conversation and replies as NPC
GM publishes datashard
Player opens datashard
```

## Manual Mobile Testing

Use:

-   Browser responsive mode
-   Actual phone
-   Slow or interrupted connection
-   Long messages
-   Small-screen keyboard behavior

------------------------------------------------------------------------

# 20. Phase 15 --- Deployment

Deployment should wait until the local MVP is stable.

## Feature 15.1: Production Configuration

Separate:

``` text
Development configuration
Test configuration
Production configuration
```

Secrets should not be committed to Git.

## Feature 15.2: Hosted Database

Use managed PostgreSQL if possible.

## Feature 15.3: Application Hosting

Possible structures include:

### Single-server deployment

``` text
Reverse proxy
Spring Boot backend
React static files
PostgreSQL or hosted PostgreSQL
```

### Managed deployment

``` text
Frontend hosting
Backend hosting
Managed PostgreSQL
```

For a small private project, operational simplicity should take priority
over elaborate cloud architecture.

## Feature 15.4: Custom Domain

Configure:

-   Domain records
-   HTTPS
-   Backend routing
-   Frontend routing

## Feature 15.5: Backups

Back up:

-   PostgreSQL database
-   Uploaded NPC and character images

Even without player uploads, portraits and future content assets need
storage protection.

## Feature 15.6: Initial Accounts

Create the GM and player accounts through a controlled deployment
process.

## Completion Criteria

-   Application is accessible through HTTPS.
-   Custom domain works.
-   Database survives application restarts.
-   Backups exist and can be restored.
-   Player accounts are ready.

------------------------------------------------------------------------

# 21. Recommended Implementation Order

The practical build order is:

``` text
1. Requirements and wireframes
2. Repository and local environment
3. Database migrations
4. Authentication
5. Characters, identities, and NPCs
6. Player OS shell
7. Contacts
8. Text messaging
9. Datashards
10. Email
11. Browser
12. Unified notifications
13. GM dashboard
14. Security review
15. End-to-end testing
16. Deployment
```

This order minimizes rework because later features depend on earlier
concepts.

------------------------------------------------------------------------

# 22. Feature Backlog Format

Each feature should be documented using the same structure.

## Example: Publish Datashard

### User Story

> As the GM, I need to publish a datashard to selected characters so
> they can receive an in-world handout during a session.

### Acceptance Criteria

``` text
Given that the GM is logged in
and a datashard draft exists,
when the GM selects one or more recipients
and publishes the datashard,
then the datashard becomes visible to those recipients,
the recipients receive an unread notification,
and characters who were not selected cannot access it.
```

### Backend Work

-   Create publish service
-   Validate recipient identities
-   Create recipient records
-   Generate notifications
-   Return published datashard

### Frontend Work

-   Recipient selector
-   Publish button
-   Success state
-   Datashard list update
-   Notification badge

### Tests

-   GM can publish
-   Player cannot publish
-   Recipient can retrieve
-   Non-recipient receives forbidden response
-   Duplicate publishing does not duplicate recipient records

### Definition of Done

-   Acceptance criteria pass
-   Automated tests pass
-   Mobile layout tested
-   Error handling added
-   Documentation updated

Every meaningful feature should follow this format.

------------------------------------------------------------------------

# 23. Suggested First Planning Milestone

Before creating the Spring Boot or React projects, the first milestone
should produce these documents:

``` text
docs/
├── product-requirements.md
├── terminology.md
├── user-flows.md
├── mvp-backlog.md
├── architecture-overview.md
└── wireframes/
```

The first backlog should contain roughly these epics:

``` text
EPIC-01 Project Foundation
EPIC-02 Authentication
EPIC-03 Identity and NPC Management
EPIC-04 Player Operating System
EPIC-05 Contacts
EPIC-06 Messaging
EPIC-07 Datashards
EPIC-08 Email
EPIC-09 Browser
EPIC-10 Notifications
EPIC-11 GM Dashboard
EPIC-12 Security and Deployment
```

The next planning step should be to turn **EPIC-01 through EPIC-04**
into individual user stories and acceptance criteria. That provides a
concrete path from an empty repository to the first usable authenticated
player screen.

## User

Points on this all: 3. User fields do not need active or createdAt
fields. Unnecessary for players to see if anyone is active as this will
ideally be a 24/7 service. Character fields do not need portrait,
emailAddress, or phoneNumber. Portraits are unavailable as for the MVP,
no file uploads are possible. Email addresses and phone numbers are
unavailable as this shouldn't tie in to any of my players' physical
data. NPC fields do not need the portrait, emailAddress, or phoneNumber
for the MVP for the same reasons. Datashard fields do not need
createdBy, createdAt, or status fields. Datashard Recipient field
doesn't need to exist? Web Pages are not part of the MVP. Identity
fields do not need portrait, emailAddress, or phoneNumber datafields for
the reasons stated above.

Respond succinctly. I would like to get started. Is my first step to
open a new Github repo?

## Assistant

Yes. Start with a new GitHub repository.

Use a single repository for the full project:

``` text
cyberpunk-ttrpg-app/
├── backend/
├── frontend/
├── docs/
├── README.md
└── .gitignore
```

Before generating Spring Boot or React projects, add a short `README.md`
containing:

-   Project purpose
-   MVP feature list
-   Chosen stack
-   Current development status

Your field corrections make sense for the MVP.

One note: `DatashardRecipient` is still useful if one datashard can be
pushed to selected players. It records which characters can access each
datashard. It can be very small:

``` text
datashardId
characterId
read
```

Without it, datashards would either need to be visible to everyone or
store recipient information awkwardly inside the datashard itself.

The immediate steps are:

1.  Create the GitHub repository.
2.  Clone it locally.
3.  Add the folder structure and README.
4.  Make the first commit.
5.  Then create the Spring Boot backend skeleton.

## User

while setting up the repository, I unticked a box that left out the
.gitignore. How do I fix my mistake

## Assistant

Create the `.gitignore` manually in the repository root.

For this project, add:

``` gitignore
# Java / Spring Boot
backend/target/
*.class
*.jar
*.war
*.log

# Node / React
frontend/node_modules/
frontend/dist/
frontend/build/
frontend/.env
frontend/.env.*

# IDEs
.idea/
.vscode/
*.iml

# Operating systems
.DS_Store
Thumbs.db

# Environment files
.env
.env.*

# Local database or Docker data
docker-data/
```

Then commit it:

``` bash
git add .gitignore
git commit -m "Add project gitignore"
git push
```

If files such as `node_modules` or `target` were already committed,
`.gitignore` will not automatically remove them. Remove them from Git
tracking with:

``` bash
git rm -r --cached frontend/node_modules
git rm -r --cached backend/target
```

Then commit again.

## User

currently the only two files in the repo are the .gitignore and the
README.md.

## Assistant

That's actually a good place to be. Since nothing has been committed
besides those two files, you don't need to fix anything else.

Your repository is essentially clean.

The next commit can introduce the initial project structure:

`text id="d4208p" cyberpunk-ttrpg-app/ ├── backend/ ├── frontend/ ├── docs/ ├── README.md └── .gitignore`

I also recommend creating a few placeholder files so Git tracks the
directories:

\`\`\`text id="51if9z" backend/ .gitkeep

frontend/ .gitkeep

docs/ .gitkeep


    Then commit:

    ```bash id="vyyytu"
    git add .
    git commit -m "Initialize project structure"
    git push

After that, the repository is ready for Phase 1: creating the Spring
Boot backend. There's no need to recreate the repository or worry about
the missing `.gitignore` option---you've already corrected it.

## User

Don't we have more to do for Phase 0?

## Assistant

Yes. Creating the repository is only the setup for Phase 0.

Before starting Spring Boot or React, Phase 0 should produce:

``` text
docs/
├── product-requirements.md
├── terminology.md
├── user-flows.md
├── mvp-backlog.md
├── architecture-overview.md
└── wireframes/
```

The practical order should be:

1.  Finalize the MVP scope.
2.  Define the core data entities and relationships.
3.  Document player and GM user flows.
4.  Create rough wireframes for each MVP screen.
5.  Break the MVP into epics and user stories.
6.  Write a basic architecture overview.
7.  Review the scope for anything missing or unnecessary.

For this project, the MVP currently includes:

-   Login
-   Player operating-system shell
-   Contacts
-   Text messaging
-   Email
-   Datashards
-   GM dashboard
-   NPC management
-   Notifications
-   Mobile-first responsive design

Web pages are no longer part of the MVP.

The best next step is to create `docs/product-requirements.md` and write
the agreed MVP scope into it.

## User

earlier for the tech stack you said that the stack would be backend,
frontend, frontend tooling, database, and deployment. What is
deployment? Is it essentially how the program will be used by other
people? If that's the case, the eventual goal is to purchase a domain
such as ncagent.com or something so that they can get to this from their
phones easily. What would that look like in the context of writing the
README.md file? This is what I have so far:

## Stack

**Backend**: Java with Spring Boot

**Frontend**: React with JavaScript

**Frontend tooling**: Node.js for pckage management, development
tooling, and builds

**Database**: PostgreSQL

**Deployment**:

## Assistant

That's exactly what deployment refers to.

Development is how **you** run the application on your own machine.
Deployment is how the application is made available for **everyone
else** to access over the internet.

For your project, the eventual architecture will look something like
this:

`text id="ecne2m" Player's Phone         │         ▼ https://ncagent.com         │         ▼ Web Server         │  ┌──────┴──────┐  ▼             ▼ React App   Spring Boot API                  │                  ▼             PostgreSQL`

A player opens a browser on their phone, visits `https://ncagent.com`,
logs in, and interacts with the application. They don't install
anything; it's just a website optimized for mobile.

------------------------------------------------------------------------

For the README, it doesn't need to specify *how* you'll deploy yet (AWS,
DigitalOcean, Railway, Render, etc.). It only needs to state the
intended deployment target.

I would write it like this:

\`\`\`markdown id="gk4ie0" \## Stack

**Backend:** Java with Spring Boot

**Frontend:** React with JavaScript

**Frontend Tooling:** Node.js for package management, development, and
builds

**Database:** PostgreSQL

**Deployment:** Browser-based web application hosted on a custom domain
(e.g. `ncagent.com`), accessible from desktop and mobile devices.


    That's enough for Phase 0.

    Later, once the application is ready to go online, you can replace that last line with something more specific, for example:

    ```markdown id="vxxs09"
    **Deployment:** Docker containers hosted on a Linux server behind Nginx with a PostgreSQL database and HTTPS served through a custom domain.

At this stage, keeping it at the level of the application's intended
deployment is the right amount of detail.

## User

Export this entire conversation into a Markdown file, preserving every
user and assistant message in chronological order.
