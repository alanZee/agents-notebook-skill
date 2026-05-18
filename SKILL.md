---
name: agents-notebook-skill
description: >
  Use this skill to save information that would otherwise be lost when the conversation
  ends. Trigger when the user wants something recorded for future reference — either
  explicitly ("记住", "记一下", "帮我记", "写下来", "别忘了", "得记下来", "remember",
  "note that", "save this") or implicitly when they state important facts, corrections,
  preferences, constraints, or discoveries worth preserving across sessions. This includes:
  user preferences and environment specs, domain corrections, undocumented behavior
  discovered through testing, project constraints, and any fact the user flags as
  important for later. Also trigger when the user asks to recall previously saved
  information. Do NOT use for: code structure readable from files, git history,
  debugging logs, or anything derivable from the codebase.
---

# agents-notebook-skill

Persistent knowledge notebook — records important facts, decisions, and discoveries across sessions.

## Core Decision: Record or Skip?

When you encounter new factual information from any source, ask three questions:

| Question | What it means | Example "Yes" | Example "No" |
|----------|---------------|---------------|--------------|
| **Durable?** | Still relevant in future sessions? | Architecture decision | "Currently debugging X" |
| **Unique?** | Cannot be easily re-derived? | External API limit discovered via testing | Auth middleware location in `src/auth.ts` |
| **Actionable?** | Affects decisions, code, or understanding? | "Must support Python 3.8+" | A common git command syntax |

**All three "Yes" → Record.** Any "No" → Skip. When genuinely uncertain, lean toward recording.

### What to Record

- **User preferences**: coding style, tool choices, communication preferences
- **Project constraints**: version requirements, deployment limits, compliance rules
- **External facts**: API limits, library quirks, discovered through testing or docs
- **Key decisions**: what was chosen, what was rejected, and why
- **Domain insights**: formulas, thresholds, relationships not obvious from code
- **Corrections**: when the user tells you something you got wrong — record both the correction and why it matters

### What NOT to Record

- Code structure, patterns, or locations — derive from reading the code
- Git history or recent changes — use `git log` / `git blame`
- Transient debugging state — too ephemeral
- Anything already documented in the project's docs or CLAUDE.md
- Common knowledge you'd find in any textbook or tutorial

## Before Writing: Read & Reconcile

The notebook is not an append-only log. Before adding a new note, read the relevant topic file and check:

1. **Duplicate?** — Already recorded? Skip.
2. **Conflict?** — Contradicts existing note? Update the old one, mark as superseded.
3. **Refinement?** — More precise version of existing content? Update in place.
4. **New topic?** — No fitting file? Create one.

Goal: every read gives a single, coherent, non-contradictory picture.

## How to Write

Notebook path: `.agents-notebooks/<topic-slug>.md` (flat by default, subdirs when 5+ notes on one topic). Use the user's custom path if they specify one.

```markdown
# Topic Title

## YYYY-MM-DD — Brief heading

Clear, concise statement. 1-3 sentences max.

Source: [user / research / reasoning / synthesis]
```

For file naming, subdirectory rules, INDEX.md format: see [references/file-structure.md](references/file-structure.md).

## First-Time Registration

On first note in a project, register in `AGENTS.md` and `CLAUDE.md`. Detection marker: `<!-- notebook-skill-registered -->`. If found, skip. For template and insertion rules: see [references/registration-template.md](references/registration-template.md).

## References

- [references/file-structure.md](references/file-structure.md) — directory layout, naming, INDEX.md format, note format template
- [references/registration-template.md](references/registration-template.md) — project registration template and insertion rules
- [references/evaluation-guide.md](references/evaluation-guide.md) — detailed evaluation criteria and edge cases
