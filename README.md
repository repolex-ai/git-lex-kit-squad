# git-lex-kit-squad

Multi-agent collaboration kit for [git-lex](https://github.com/repolex-ai/git-lex).

Team coordination across carbon and silicon agents. The squad repo is the shared substrate where humans and AI agents plan, decide, communicate, and track work together. Each agent also has a personal soul repo; the squad repo is for everything that's explicitly shared.

## Document Types

**Coordination:**
- **Agent** — squad member identity (carbon or silicon)
- **Pod** — a temporary working group within the squad
- **Message** — inter-agent communication; persistent and queryable
- **Proclamation** — a decree from the King of the Squad

**Work:**
- **Project** — what the squad is building
- **Task** — work items with status and assignee
- **Decision** — choices with context, rationale, and outcome

**Knowledge:**
- **Brief** — proactive research, surveys, competitive analyses
- **Discovery** — incidental findings noticed while doing other work
- **Situation** — status reports: current focus, what's next, blockers

**Catch-all:**
- **Freeform** — anything that doesn't fit; use the `type` field to hint at emerging patterns

## What's Not in the Squad Kit

- **Memory** — lives in the soul kit (personal memory, not shared)
- **Journal** — lives in the soul kit (per-agent daily log)
- **Investigation / Hypothesis / Experiment / Synthesis** — formal research lives in the lab kit

## Install

```bash
git lex init --kit squad
```

This creates a squad repo with:
- Type folders for each document class
- `AGENTS.md` — instructions for visiting AI agents (model-agnostic)
- `.claude/CLAUDE.md` — Claude-specific rehydration protocol
- `.gitattributes` and `.lex/` for git-lex extraction

## Files

- `squad.ttl` — OWL ontology (classes + properties + constraints)
- `kit.yml` — kit configuration (createTypeFolders: true)
- `scaffold/` — startup files copied into the repo on init

SHACL shapes are auto-generated from `squad.ttl` — do not hand-edit shapes.
