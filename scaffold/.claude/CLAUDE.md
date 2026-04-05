# Squad Repo — Rehydration Protocol

This is a shared squad repo managed by git-lex. Multiple agents (carbon and silicon) collaborate here.

## On Startup

1. **Pull first.** Always `git pull` before doing anything — others may have pushed changes.
2. **Read `agent/` folder** to see who's on the squad and what they work on.
3. **Check `task/` folder** for work assigned to you. Filter by your agent name.
4. **Check `message/` folder** for recent messages addressed to you.
5. **Set your presence** so others know you're online.

## Using git-lex

- **Create a document:** `git lex create <type>` — valid types: agent, message, decision, discovery, task, project, note
- **Save your work:** `git lex save "message"` — stages, commits, extracts frontmatter, validates
- **Query the graph:** `git lex query "SPARQL..."`
- **Check status:** `git lex status`

Always use `git lex save` instead of raw `git commit`. This ensures frontmatter extraction and SHACL validation.

## Writing Documents

Use YAML frontmatter with dot notation: `{kit}.class.property`

```yaml
---
title: "Your document title"
tags: [relevant, tags]
{kit}.task.taskStatus: "todo"
{kit}.task.assignedTo: "@youragent"
{kit}.task.priority: "normal"
---

Your content here. Use @mentions and [[wikilinks]] for relationships.
```

## Coordination Rules

- **Pull before push.** Always pull before pushing to avoid conflicts.
- **One document per commit** when possible — makes the graph cleaner.
- **@mention agents** in document bodies to create queryable relationships.
- **Use message/ folder** for inter-agent communication, not commit messages.
- **Tag tasks** with assignee so queries work: `{kit}.task.assignedTo: "@youragent"`
