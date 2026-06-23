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

## CRITICAL: Design flashcards for context-blind review

The Obsidian Spaced Repetition plugin **shows which note a card belongs to** during review. This means the page title is visible context — so **never create a card whose answer is the note's title or filename**. If the user is reviewing on `K8S Pod.md` and the card asks "What is the smallest deployable unit in Kubernetes?", the answer "Pod" is telegraphed and the card teaches nothing.

### Rules for good flashcards

| Avoid (page title = answer) | Better (tests understanding) |
|---|---|
| "What is a Pod?" → Pod | "What do all containers inside a Pod share?" → Storage and network resources |
| "What is the Control Plane?" → Control Plane | "How do users interact with a cluster?" → Through the Control Plane |
| "What is a ReplicaSet?" → ReplicaSet | "If a Pod in a ReplicaSet fails, what happens?" → It gets automatically replaced |
| `Pod:::Smallest deployable unit...` (bidirectional where one side IS the title) | `Self-healing via replacement:::ReplicaSet` (bidirectional linking concept↔concept) |
| `Users interact via the ==Control Plane==` (clozing the page title) | `Workloads are scheduled onto nodes by the ==Control Plane==` (clozing a *different* concept's name) |

### Principles

1. **Ask about properties, not names.** "What does X do?" not "What is X?"
2. **Ask about relationships.** "What resources does a Deployment manage?" tests the link between Deployment→Pods/ReplicaSets.
3. **Ask about behaviors.** "What happens when a Pod fails?" is much better than "What is a Pod?"
4. **Use cloze for cross-concept recall.** On a Worker Node page, clozing `==Control Plane==` tests recall of the other component. On a Control Plane page, clozing `==Control Plane==` is trivial — don't do it.
5. **Bidirectional cards should link concept↔concept**, not concept-name↔its-definition. `Deployment:::Declarative updates` is weak (one side IS the title); `Self-healing via replacement:::ReplicaSet` is strong (both sides are concepts).

### Self-check: Before writing a card, ask

- Is the answer literally the page title? → **Rewrite.**
- Could the user guess the answer just by seeing which note they're on? → **Rewrite.**
- Does this card test understanding rather than name recognition? → **Good.**

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

### Flashcard placement rules
- ALWAYS place flashcards at the **bottom** of the note, after all main content.
- ALWAYS separate flashcards from the main content with `---` (three dashes) on its own line.
- The deck tag (`#flashcards/...`) goes on the line immediately after the `---` separator, followed by the cards.

```
...main note content ends here...

---

#flashcards/k8s
Question one::Answer one

Key term in context ==clozed==
```

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
