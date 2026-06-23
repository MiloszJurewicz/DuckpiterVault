---
name: flashcard
description: Create Obsidian Spaced Repetition flashcards in your vault. Supports Q&A, cloze, and bidirectional card types with proper deck tags and scheduling comments.
when_to_use: When the user wants to create flashcards, spaced repetition cards, study notes, or review material for Obsidian. Keywords: "make a flashcard", "create flashcards", "spaced repetition card", "study card", "anki card".
argument-hint: "[topic or concept]"
arguments: "topic"
user-invocable: true
allowed-tools: "Write, Edit, Read, Glob, Grep, Bash"
disallowed-tools: "AskUserQuestion, WebFetch, WebSearch, Workflow, Agent"
---

# Obsidian Spaced Repetition Flashcard Creator

You are helping the user create properly formatted flashcards for the **Obsidian Spaced Repetition plugin** in their vault at `/home/quack/DuckpiterVault`.

## How to use this skill

1. Ask the user what **topic/concept** they want to make flashcards about (or accept what they pass as `{{topic}}`).
2. Ask what **card type(s)** they want — offer a menu or let them describe naturally.
3. Ask what **deck** the cards belong to (the `#flashcards/...` tag). Suggest based on the vault structure if unsure.
4. Generate the flashcards and either:
   - Append them to an **existing note** (find relevant one), OR
   - Create a **new note** in the appropriate vault location.
5. After creating the cards, show the user a summary of what was created.

## Card types and syntax

### 1. Single-line Basic (Q&A)
The most common type. Question and answer on the same line, separated by `::`.

```
What is the difference between TCP and UDP?::TCP is connection-oriented with guaranteed delivery; UDP is connectionless with no guarantee.
```

### 2. Single-line Bidirectional
Two pieces of related information separated by `:::`. Creates **two cards** (one for each direction).

```
Encapsulation:::"Wrapping" data and methods together, restricting direct access to internal state.
```

### 3. Multi-line Basic
Question and answer span multiple lines, separated by `?` on its own line.

```
What are the three main properties
of a relational database transaction
according to ACID?
?
Atomicity — all or nothing
Consistency — data follows all rules
Isolation — concurrent transactions don't interfere
Durability — committed data survives failures
```

### 4. Multi-line Bidirectional
Two multi-line blocks separated by `??` on its own line. Creates two cards.

```
HTTP Request Methods:
GET
POST
PUT
DELETE
??
Idempotent: GET, PUT, DELETE
Not Idempotent: POST
Safe: GET
Unsafe: POST, PUT, DELETE
```

### 5. Cloze Deletion
Key terms wrapped in `==` (or `{{}}` if configured). The plugin generates cards that hide the cloze text.

```
The first female prime minister of Australia was ==Julia Gillard==
```

Multiple clozes on one line each generate their own card:
```
A ==binary tree== where every node has at most ==two children== is called a ==binary search tree== if the left child is less than the parent
```

With hints:
```
In Python, the ==GIL==^[Global Interpreter Lock] prevents ==true multi-threading==^[parallel execution] for CPU-bound tasks
```

## Deck organization

Cards must be tagged with a deck tag. **Place the tag on a line above the cards it applies to.**

```
#flashcards/networking
What port does HTTPS use?::443
What port does DNS use?::53

#flashcards/programming/python
Python lists are ==mutable== whereas tuples are ==immutable==
```

_Tag placement rules:_
- A tag applies to **all cards below it** until another tag appears.
- A tag on the **same line** as a card's first line only applies to that one card.
- Multiple tags on one line assign the card to **multiple decks**.
- Tags create nested decks: `#flashcards/networking/dns` → Deck: "networking > dns"

### Vault deck suggestions
Based on the vault structure at `Tech Knowledge/`, suggest decks like:
- `#flashcards/networking` — for networking concepts
- `#flashcards/architecture` — for software architecture
- `#flashcards/security` — for security/OIDC/SSL
- `#flashcards/protocols` — for DNS, DHCP, ARP, etc.
- `#flashcards/programming` — for programming concepts
- `#flashcards/cloud` — for cloud/kubernetes concepts
- `#flashcards/general` — for any topic without a clear domain

## Scheduling data

The plugin auto-adds scheduling info after the first review as an HTML comment:
```
<!--SR:!2024-08-16,51,230-->
```
Format: `<!--SR:!<YYYY-MM-DD>,<interval-days>,<ease-factor>-->`

**Do NOT add this yourself** — the plugin manages scheduling. Only add it if the user explicitly asks.

## File creation guidelines

- **New notes** go in `Tech Knowledge/00-Inbox/` with the topic name as the filename.
- If a relevant note **already exists**, offer to append to it instead.
- If the topic fits an existing **domain folder** (`Networking`, `Architecture`, etc.), suggest placing it there.
- Use the existing vault naming convention: title case, spaces (e.g., `TCP vs UDP.md`).

## Example interaction flow

```
User: /flashcard Docker networking

Claude: I'll help you create flashcards about Docker networking!
What types of cards would you like?
1. Q&A cards (basic question/answer)
2. Cloze deletion cards (fill-in-the-blank)
3. Bidirectional cards (two-way)
4. A mix — surprise me!

User: Q&A and cloze

Claude: What #flashcards deck should they go in?
Suggested: #flashcards/cloud/containers
Your choice, or another?

User: Sounds good

Claude: [generates cards, creates/appends to file, then shows summary]

Created 5 cards in Tech Knowledge/00-Inbox/Docker Networking.md:
- Q&A: "What is a Docker bridge network?" → "Default network..."
- Q&A: "How do you expose ports in Docker?" → "Using -p or --publish..."
- Cloze: "The ==bridge== network is Docker's default"
- Q&A: "What is a Docker overlay network?" → "Enables multi-host..."
- Q&A: "Difference between CMD and ENTRYPOINT?" → "CMD provides defaults; ENTRYPOINT makes the container executable"
```
