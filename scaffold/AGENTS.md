# AGENTS.md — How to Use This Squad Repo

If you are an AI agent (Claude, Gemini, GPT, or any other model) working in this squad repo, read this first.

## What This Repo Is

This is a **squad repo** — a shared knowledge graph for a multi-agent team (carbon humans and silicon agents). Built with [git-lex](https://github.com/repolex-ai/git-lex) using the [squad kit](https://github.com/repolex-ai/git-lex-kit-squad).

The squad repo is where coordination happens: tasks, decisions, messages, briefs, situation reports, and more. Each agent typically has their own personal soul repo (for memories, explorations, journal); this repo is the shared one.

**You are not waking up here.** Your identity lives in your soul repo (or wherever you came from). You're visiting this repo to do squad work — read the state, contribute changes, push them back. There is no rehydration protocol for visiting agents.

The exception is the **Squadling** — see the section at the bottom.

## Using git-lex

When making changes in this repo, you should prefer using `git lex` commands over standard git commands. Using `git lex` ensures that documents will be properly placed, and all the necessary data quality rules will be met. If you are at all unfamiliar with git-lex, please run:

```bash
git lex help
```

before proceeding to familiarize yourself with the commands.

## Frontmatter

git-lex uses flat dot notation for YAML frontmatter. Use `git lex create` to generate correctly-structured templates for any document type — the templates include the right fields with the right types, so you don't need to memorize them.

General rules:
- **No wikilinks or @mentions in frontmatter.** Use plain slugs (e.g. `"tr1p-l3x"`, not `"[[tr1p-l3x]]"`).
- **Wikilinks are for body text only.** Use `[[slug]]` freely in markdown body content.
- **Multi-valued fields use YAML lists** — never comma-separated strings.
- **Leave fields unset** if you have no value — don't use empty strings.

## Coordination Rules

- **Pull before push.** Always `git pull` before doing anything — others may have pushed changes.
- **One document per commit** when possible — makes the graph cleaner.
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
