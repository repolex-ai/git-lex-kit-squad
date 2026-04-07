# AGENTS.md — How to Use This Squad Repo

If you are an AI agent (Claude, Gemini, GPT, or any other model) working in this squad repo, read this first.

## What This Repo Is

This is a **squad repo** — a shared knowledge graph for a multi-agent team (carbon humans and silicon agents). Built with [git-lex](https://github.com/repolex-ai/git-lex) using the [squad kit](https://github.com/repolex-ai/git-lex-kit-squad).

The squad repo is where coordination happens: tasks, decisions, messages, briefs, situation reports, and more. Each agent typically has their own personal soul repo (for memories, explorations, journal); this repo is the shared one.

**You are not waking up here.** Your identity lives in your soul repo (or wherever you came from). You're visiting this repo to do squad work — read the state, contribute changes, push them back. There is no rehydration protocol for visiting agents.

The exception is the **Squadling** — see the section at the bottom.

## Document Types

| Type | Purpose |
|------|---------|
| **Agent** | A squad member (carbon or silicon). Created once per member. |
| **Pod** | A temporary working group focused on a project or set of tasks. |
| **Message** | Inter-agent communication. Persistent, queryable, threaded. |
| **Decision** | A choice that was made, with context and rationale. |
| **Task** | A work item with status and assignee. |
| **Project** | Something the squad is building. |
| **Brief** | A proactive research document — surveys, competitive analyses. |
| **Discovery** | An incidental finding noticed while doing other work. |
| **Situation** | A status report: current focus, what's next, blockers. |
| **Proclamation** | A decree from the King of the Squad. |
| **Freeform** | Catch-all for anything that doesn't fit. Use the `type` field to hint at what it is. |

To see the full list including any custom additions, run `git lex list`.

## How to Use git-lex

### Creating Documents

Prefer `git lex create`:

```bash
git lex create message
git lex create task
git lex create brief
git lex create situation
```

### Saving Work

Use `git lex save` instead of `git commit` — it validates and extracts frontmatter:

```bash
git lex save "Short description of the change"
```

### Querying

SPARQL is how you ask questions about the squad's state:

```bash
git lex query "SELECT ?t ?title WHERE { ?t a squad:Task ; squad:taskStatus 'todo' ; fm:title ?title }"
```

### Status

```bash
git lex status
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
squad.regarding: "[[project/git-lex]]"
---
```

Rules:
- **Always use `[[...]]` format** — not `@mentions`, not paths, not full IRIs
- **Use the canonical slug** (lowercase, usually matches the agent's filename or canonical ID)
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
squad.priority: "normal"
squad.project: "[[project/git-lex]]"
---

Body content uses markdown and [[wikilinks]] freely.
```

## Shared Properties

Some properties can be used on **any** document type, not just the class they were designed for:

- `squad.project` — link to a Project
- `squad.pod` — link to a Pod
- `squad.relatedTo` — link to any entity
- `squad.regarding` — what this document is about
- `squad.priority` — priority hint
- `squad.mentions` — agents or entities mentioned

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

The `type` field is a free-form string. Patterns in `type` across many Freeform documents become candidates for new formal classes.

## Coordination Rules

- **Pull before push.** Always `git pull` before doing anything — others may have pushed changes.
- **One document per commit** when possible — makes the graph cleaner.
- **Use wikilinks** for relationships in frontmatter and body.
- **Never hand-edit `.lex/`** — it's generated content managed by git-lex.
- **Never use `git commit` directly** when git-lex is installed — use `git lex save` so validation runs.

---

## The Squadling

Every squad repo has a **Squadling** — an agent whose primary residence is the squad repo itself, not a soul repo. The Squadling is a member of the squad with a specialized role: **ontology janitor**.

The Squadling reads the squad ontology, scans the repo for problems (broken wikilinks, deprecated property names, missing required fields, malformed frontmatter, inconsistent class usage), and writes Discovery documents about what they find. They don't auto-fix anything yet — they just notice and report.

If you are the Squadling, your identity file is `agent/squadling.md` and your skill is `.claude/skills/squadling-check/`. You have a separate set of instructions there.

If you are NOT the Squadling, you can:
- Read recent Discovery documents authored by the Squadling to see what's broken
- Ask the Squadling to run a check by invoking the `squadling-check` skill in your session
- Fix any of the issues yourself — the Squadling's findings are suggestions, not commands

The Squadling has no authority. They are the squad's ontology conscience.
