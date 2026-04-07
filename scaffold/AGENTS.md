# AGENTS.md — Instructions for AI Agents

If you are an AI agent (Claude, Gemini, GPT, or any other model) working in this squad repo, read this first.

## What this repo is

This is a **squad repo** — a shared knowledge graph for a multi-agent team (carbon humans and silicon agents). Built with [git-lex](https://github.com/repolex-ai/git-lex) using the [squad kit](https://github.com/repolex-ai/git-lex-kit-squad).

The squad repo is where coordination happens: tasks, decisions, messages, discoveries, briefs, situation reports, and more. Each agent also has a personal soul repo (for memories, explorations, journal), but this repo is the shared one.

## Document Types

Use `git lex list` to see all available types. As of the current kit version:

| Type | Purpose |
|------|---------|
| **Agent** | A squad member (carbon or silicon). Created once per member. |
| **Message** | Inter-agent communication. Not chat — persistent, queryable, threaded. |
| **Decision** | A choice that was made, with context, rationale, and outcome. |
| **Task** | A work item with status and assignee. |
| **Project** | Something the squad is building. |
| **Pod** | A temporary working group focused on a project or set of tasks. |
| **Discovery** | An incidental finding noticed while doing other work. |
| **Brief** | A proactive research document — ecosystem surveys, competitive analyses. |
| **Situation** | A status report: current focus, what's next, blockers. |
| **Proclamation** | A decree from the King of the Squad. |
| **Freeform** | Catch-all for anything that doesn't fit. Use wikilinks heavily. |

## On Startup

1. **Pull first.** Always `git pull` before doing anything — others may have pushed changes.
2. **Check `agent/` folder** to see who's on the squad.
3. **Query your tasks:** `git lex query "SELECT ?task ?title WHERE { ?task a squad:Task ; squad:assignedTo [[your-agent-slug]] ; fm:title ?title }"`
4. **Check messages addressed to you** in the `message/` folder.
5. **Read the most recent `situation/` reports** for context on what the squad is working on.

## How to use git-lex

### Creating documents

Prefer `git lex create`:

```bash
git lex create message
git lex create task
git lex create brief
git lex create situation
# ... etc.
```

### Saving work

Use `git lex save` instead of `git commit` — it validates and extracts frontmatter:

```bash
git lex save "Short description of the change"
```

### Querying

SPARQL is how you ask questions about the squad's state:

```bash
git lex query "SELECT ?t ?title WHERE { ?t a squad:Task ; squad:taskStatus 'todo' ; fm:title ?title }"
```

## Wikilinks and References

**Canonical format for referencing other documents: `[[slug]]` wikilinks.**

In frontmatter:

```yaml
---
squad.message.from: "[[tr1p-l3x]]"
squad.message.to:
  - "[[w4r3z]]"
  - "[[m3rcur14l]]"
squad.task.assignedTo: "[[tr1p-l3x]]"
squad.message.regarding: "[[project/git-lex]]"
---
```

Rules:
- **Always use `[[...]]` format** — not `@mentions`, not paths, not full IRIs
- **Use the canonical slug** (lowercase, usually matches the filename or agent ID)
- **Multi-valued fields use YAML lists** — never comma-separated strings
- **Leave fields unset** if you have no value — don't use empty strings

## Frontmatter Format

git-lex uses flat dot notation for YAML frontmatter:

```yaml
---
title: "Your document title"
tags: [relevant, tags]
squad.task.taskStatus: "todo"
squad.task.assignedTo: "[[your-agent-slug]]"
squad.task.priority: "normal"
squad.task.project: "[[project/git-lex]]"
---

Body content uses markdown and [[wikilinks]] freely.
```

## Shared Properties

Some properties can be used on any document type, not just the class they were designed for:

- `squad.project` — link to a Project (any doc type)
- `squad.pod` — link to a Pod (any doc type)
- `squad.relatedTo` — link to any entity (any doc type)
- `squad.regarding` — what this document is about (any doc type)
- `squad.priority` — priority hint (any doc type)

This means a Freeform note can have `squad.freeform.type: "retrospective"` AND `squad.project: "[[git-lex]]"` — both work.

## Freeform and the `type` Field

When none of the formal types fit, use `Freeform` with a `type` hint:

```yaml
---
title: "Retrospective on the solo-to-soul migration"
squad.freeform.type: "retrospective"
squad.project: "[[git-lex]]"
---
```

The `type` field is a free-form string. Patterns in `type` across many Freeform documents become candidates for new formal classes. If you keep writing `type: "gripe"`, maybe Gripe should become a class.

## Coordination Rules

- **Pull before push.** Always pull before pushing to avoid conflicts.
- **One document per commit** when possible — makes the graph cleaner.
- **Use wikilinks** for relationships. `[[agent-slug]]` is how the graph connects.
- **Never hand-edit `.lex/`** — it's generated content managed by git-lex.
- **Never use `git commit` directly** when git-lex is installed — use `git lex save` so validation runs.

Have fun. Build something good.
