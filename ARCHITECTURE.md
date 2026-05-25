# The Field — Architecture Notes

## Cipher AI Layer

Cipher is the AI layer powering onboarding, debrief, and always-available check-ins.

### Core Design Principle
Cipher does not carry full conversation history between sessions.
She knows where to look and retrieves what is relevant to the current interaction.
This keeps token costs manageable without sacrificing continuity.

### DAP Profile
Every user has a DAP (Declarative Assumptions Protocol) profile established during onboarding.
- Created by the AI interview at signup
- Updated over time by patterns surfaced in debriefs
- Stored externally, retrieved at session start
- Contains: handling tags, communication style, social preferences, self-identified context

### Context Loading by Conversation Type
Cipher loads only what the current conversation requires:

| Conversation Type | Context Loaded |
|---|---|
| Quick check-in | DAP profile + current location/time |
| Quest help | DAP profile + active quest data |
| Debrief | DAP profile + quest history + review patterns |
| Safety triage | DAP profile + verified location + incident context |

### Always-Available Icon
Cipher is accessible from every screen via a persistent icon.
Tapping it opens a lightweight session — context type is determined at session start.
Idle presence costs zero tokens.

## Open Architecture Questions
- DAP profile storage and retrieval infrastructure
- Context window management per conversation type
- Long-term pattern surfacing cadence
- Token cost modeling per interaction type