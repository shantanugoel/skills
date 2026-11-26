# Architecture folder (`docs/architecture/`)

Keep architecture in `docs/architecture/` instead of one growing file:
- `README.md`: concise system overview and index (~1 screen) linking to every topic doc.
- `<topic>.md` (e.g., `data.md`, `<part>.md`): focused doc per major part or cross-cutting concern. Create only what needs detail now; split out a new file before any doc grows past ~1–2 screens.

## `docs/architecture/README.md`

````markdown
# Architecture

<One paragraph: the shape of the system and the main reason for it.>

## Context

A small Mermaid diagram showing the system, its users, and external systems.

```mermaid
flowchart LR
  user[User] --> app[The system]
  app --> ext[External service]
```

## Parts

| Part | What it does | Technology | Status | Doc |
| --- | --- | --- | --- | --- |
| <part> | <one line> | <language, framework, library> | planned | [<part>.md](<part>.md) |

## Choices

Cross-cutting decisions that are hard to reverse, with rationale and the best rejected alternative (part-specific choices live in that part's doc).

- **<Choice>.** <Reason.> We did not use <option>, because <reason>.

## Unknowns

Open technical questions live in "Open questions" in `docs/vision.md`, each linked to its spike.
````

## `docs/architecture/<topic>.md`

```markdown
# <Topic / Part>

<One sentence: scope and status (`planned` | `active`).>

## Responsibilities

What this part owns and what it explicitly does not own.

## Interfaces and flows

Boundaries, APIs, stored formats, and data flows (use a small Mermaid diagram or table when helpful).

## Choices

Decisions local to this part, with rationale and the best rejected alternative.

- **<Choice>.** <Reason.> We did not use <option>, because <reason>.
```
