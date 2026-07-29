# Night City Agent
A Cyberpunk RED campaign web application for PC<->PC, PC<->NPC, and GM Handout interactions.

Terminology:

* **PC** - Player character
* **GM** - Gamemaster
* **NPC** - Non-player character
* **Datashard** - essentially just a text document

## Minimum Viable Product
- [ ] **1.** The GM and several players should be able to log in.
- [ ] **2.** Each player account controls one character.
- [ ] **3.** Players can navigate a mobile-first web application interface.
- [ ] **4.** Players can send and receive direct messages from NPCs and other PCs.
- [ ] **5.** Players can create group conversations.
- [ ] **6.** The GM can read every conversation.
- [ ] **7.** The GM can send messages to PCs as NPCs.
- [ ] **8.** Players can send and receive fake in-world "emails".
- [ ] **9.** The GM can create and distribute datashards.
- [ ] **10.** Players can view their contacts.
- [ ] **11.** Persistent data - near 24/7 access.

### Possible future implementations
- Multiple campaigns with a different set of permissions and structures. It would be cool to have this work such that I can use this for fantasy campaign handouts as well, but fantasy campaigns don't have peer-to-peer messaging capabilities.
- Character sheets. There is an app that already does this, so this is extremely low priority
- Inventory. See above.
- In-world web pages. There are example pages in the game and in the rulebook, so that would be cool.
- Hacking minigames. Having to solve a puzzle for an encrypted datashard would be ***very*** cool.
- Editing/deletion of messages. Useful tool to have, unnecessary for MVP.

## Stack
**Backend**: Java with Spring Boot

**Frontend**: React with JavaScript

**Frontend tooling**: Node.js for pckage management, development tooling, and builds

**Database**: PostgreSQL

**Deployment**: Browser-based web application hosted on a custom domain (e.g. `ncagent.com`), accessible from mobile and desktop devices.

## Development Status
0% complete. Currently in phase 0. Nothing has been implemented, just setting the project up.