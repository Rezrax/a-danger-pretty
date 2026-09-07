# Night City Agent
A Cyberpunk RED campaign web application for PC<->PC, PC<->NPC, and GM Handout interactions.

Terminology:

* **PC** - Player character
* **GM** - Gamemaster
* **NPC** - Non-player character
* **Datashard** - essentially just a text document

## Minimum Viable Product
- [ ] **1.** New browsers enter a daily four-character uppercase alphanumeric code; a device-authorization cookie remembers access. The current code stays visible in the GM panel. The GM pre-creates player profiles. Players select their name and set a password on first use; later access requires that password, with GM-assisted reset.
- [ ] **2.** Each player controls one GM-created character with a fictional email address. The GM uses a separate interface without a player character.
- [ ] **3.** Players can navigate a mobile-first web application interface.
- [ ] **4.** Players can send and receive direct messages from NPCs and other PCs.
- [ ] **5.** Players can create PC/NPC group conversations with transferable admin permissions, membership controls, and controlled history sharing.
- [ ] **6.** The GM can read every conversation and switch to individual character perspectives through the admin interface.
- [ ] **7.** The GM can send messages to PCs as NPCs.
- [ ] **8.** Players can send and receive fictional in-world emails with multiple recipients, CC, and threaded replies.
- [ ] **9.** The GM can create, edit, distribute, and revoke plain-text datashards. Players can delete their own access without affecting other recipients.
- [ ] **10.** Players can view preset contacts; only the GM adds or removes contacts in MVP.
- [ ] **11.** Persistent data - near 24/7 access.

### Possible future implementations
- Multiple campaigns with a different set of permissions and structures. It would be cool to have this work such that I can use this for fantasy campaign handouts as well, but fantasy campaigns don't have peer-to-peer messaging capabilities.
- Character sheets. There is an app that already does this, so this is extremely low priority
- Inventory. See above.
- In-world web pages. There are example pages in the game and in the rulebook, so that would be cool.
- Datashard encryption minigame — post-MVP MVF (Maximum Valued Feature). See [the backlog](docs/mvp-backlog.md#future-01--datashard-encryption-minigame-mvf).
- Editing/deletion of messages. Useful tool to have, unnecessary for MVP.

## Stack
**Backend**: Java with Spring Boot

**Frontend**: React with TypeScript

**Frontend tooling**: Node.js for pckage management, development tooling, and builds

**Database**: PostgreSQL

**Deployment**: Browser-based web application hosted on a custom domain (e.g. `ncagent.com`), accessible from mobile and desktop devices.

## Development Status

**Phase 0 — Project definition is in progress.** The repository and initial documentation exist; no application code has been implemented.

## Development Roadmap

Phases describe the intended build order. Feature epics, user stories, and acceptance criteria will be maintained in [the MVP backlog](docs/mvp-backlog.md). Later phases remain planned until their requirements are refined.

| Phase | Focus | Intended outcome |
| --- | --- | --- |
| 0 — In progress | Project definition | Agreed MVP requirements, terminology, core entities and relationships, player and GM flows, rough wireframes, architecture overview, and prioritized backlog. |
| 1 — Planned | Application skeleton | Spring Boot and React with TypeScript run locally, PostgreSQL is available, and the frontend can call a backend health endpoint. |
| 2 — Planned | Database and migrations | Version-controlled schema changes and repeatable development seed data. |
| 3 — Planned | Authentication and authorization | GM and players can log in and out; sessions and backend-enforced permissions protect private data. |
| 4 — Planned | Characters and NPCs | Each player has one character; the GM can manage NPCs and clearly select which NPC they are acting as. |
| 5 — Planned | Player operating-system shell | Shared app navigation and layout work on phones and desktop browsers. |
| 6 — Planned | Contacts | The GM preloads and manages contacts; players view their assigned contacts. |
| 7 — Planned | Text messaging | Direct and player-created group conversations persist and update instantly; the GM can read all conversations and reply as NPCs. |
| 8 — Planned | Datashards | The GM can create and distribute documents to selected players, who can reopen them later. |
| 9 — Planned | In-world email | Players can send and receive emails; the GM can inspect conversations and send as NPCs. |
| 10 — Planned | Unified notifications | Consistent in-app notifications and unread indicators cover messages, emails, and datashards. |
| 11 — Planned | GM dashboard | A consolidated interface brings together NPC communications and content management. |
| 12 — Planned | Reliability and security review | Review validation, authorization, content rendering, error handling, and connection recovery across the MVP. |
| 13 — Planned | MVP validation | Verify complete player and GM workflows, including actual-phone usability and interrupted connections. |
| 14 — Planned | Deployment | Deploy the stable MVP with HTTPS, a custom domain, persistent PostgreSQL storage, and tested backup restoration. |

This roadmap adapts the earlier conversation's phases to the current MVP: the fictional browser phase has been removed and subsequent phases renumbered. Detailed implementation choices will be made when needed.

Build each feature end to end, including its database changes, backend behavior, frontend interface, permissions, and appropriate tests. Security and testing are part of every feature; the later review phases check the integrated application. Basic live updates and GM controls belong with the features that need them before the notification and dashboard phases consolidate them.

### Next Step: Complete Phase 0

The MVP requirements are documented in [product-requirements.md](docs/product-requirements.md). Initial [terminology and core relationships](docs/terminology.md) and [four access/preparation flows](docs/user-flows.md) are drafted for review. Next, review those drafts and their open decisions, then document messaging, email, and datashard flows. Then sketch the primary screens and turn the requirements into backlog stories with acceptance criteria. Review the architecture against those flows before beginning application scaffolding.