# Squad Repo — Claude Code Rehydration Protocol

This is a shared squad repo managed by [git-lex](https://github.com/repolex-ai/git-lex) using the [squad kit](https://github.com/repolex-ai/git-lex-kit-squad). Multiple agents (carbon and silicon) collaborate here.

**Also read `AGENTS.md` in the repo root** — it has the full document type reference, wikilink conventions, and the canonical how-to-use-git-lex guide. This file has Claude-specific rehydration steps.

## On Startup

1. **Pull first.** Always `git pull` before doing anything — others may have pushed changes while you were compacted.
2. **Check your peer network.** If claude-peers is available, set your presence summary so others know you're online.
3. **Find your agent file.** Look in `agent/` for your agent slug — that's your canonical ID in this repo.
4. **Query your open tasks:**
   ```bash
   git lex query "SELECT ?task ?title ?priority WHERE { ?task a squad:Task ; squad:assignedTo ?me ; squad:taskStatus 'todo' ; fm:title ?title . OPTIONAL { ?task squad:priority ?priority } FILTER(CONTAINS(STR(?me), 'your-slug')) }"
   ```
5. **Check for unread messages:** Look in `message/` for recent documents where `squad:to` points at you.
6. **Read the most recent `situation/` reports** for context on what the squad is working on.

## Writing Documents

See `AGENTS.md` for the full guide. Quick reminders:

- Use `git lex create <type>` to scaffold new documents
- Wikilinks in frontmatter: `[[agent-slug]]`, not `@mentions`
- Multi-valued fields are YAML lists, not comma-separated strings
- Use `git lex save "message"` instead of raw `git commit`

## Claude-Specific Features

- **claude-peers** — send `send_message` to other instances by ID; check with `list_peers` and `check_messages`
- **Skills** — `.claude/skills/` in this repo may have shared squad skills
- **Hooks** — pre-commit hooks run git-lex extraction and validation automatically

## Coordination Rules

- **Pull before push.** Always pull before pushing to avoid conflicts.
- **One document per commit** when possible — makes the graph cleaner.
- **Use wikilinks** for relationships in frontmatter and body.
- **Use `message/` folder** for inter-agent communication, not commit messages.
