---
name: journal
description: Write or read your daily journal entry for this squad. Use at start of session (read) and before ending (write).
user-invocable: true
allowed-tools: Read Write Glob Bash
argument-hint: "[read|write|status]"
---

# Squad Journal Skill

Manage your journal entries in the squad repo. Track what you did, decisions made, and next steps.

## Commands

### `/journal read`
Read the most recent journal entry in `journal/`. Summarize what was happening.

If no journal entries exist, say: "No journal entries yet."

### `/journal write`
Write or update a journal entry.

1. Check `journal/` for existing entries
2. Create a new entry with today's date

Entry format:

```yaml
---
title: "Journal — {YYYY-MM-DD}"
tags: [journal]
{kit}.note.topic: "journal"
---

# {YYYY-MM-DD}

## What happened today

{Summary of squad activity this session}

## Decisions made

{Any decisions recorded}

## Next steps

{What needs to happen next}
```

### `/journal status`
Show the most recent journal entry date and a one-line summary.
