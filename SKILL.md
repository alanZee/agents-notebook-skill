---
name: notebook
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

# Notebook

A persistent directory of markdown notes that captures important information across conversations, preventing valuable knowledge from being lost to context limits or conversation endings.

## Why This Exists

Conversations are ephemeral. Important facts — a user's preference, a discovered API constraint, a key domain insight — can vanish when the context window fills or the session ends. The notebook provides a lightweight, always-on capture mechanism so nothing valuable slips through.

## Quick Start

0. **First time in a project**: Register the notebook in `AGENTS.md` and `CLAUDE.md` (see [First-Time Registration](#first-time-registration))
1. **Find or create notebook**: Default to `.agents-notebooks/` in the current working directory. Use subdirectories like `.agents-notebooks/<topic>/` to organize when needed.
2. **When you learn something**: Evaluate durability, uniqueness, and actionability (see below)
3. **Before writing**: Read existing notes in the relevant topic file to check for duplicates or conflicts
4. **Write or update**: Add the note, or update/merge with existing content if overlapping
5. **When you need past knowledge**: Read from the notebook, starting with `INDEX.md` if one exists

## Core Decision: Record or Skip?

When you encounter new factual information from any source (user, research, reasoning, synthesis), ask three questions:

| Question | What it means | Example "Yes" | Example "No" |
|----------|---------------|---------------|--------------|
| **Durable?** | Still relevant in future sessions? | Architecture decision | "Currently debugging X" |
| **Unique?** | Cannot be easily re-derived? | External API limit discovered via testing | Auth middleware location in `src/auth.ts` |
| **Actionable?** | Affects decisions, code, or understanding? | "Must support Python 3.8+" | A common git command syntax |

**All three "Yes" → Record.** Any "No" → Skip. When genuinely uncertain, lean toward recording — a lightweight note costs little, but a lost insight can be expensive to rediscover.

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

The notebook is not an append-only log. Before adding a new note, read the relevant topic file (or scan `INDEX.md` to find it) and check:

1. **Duplicate?** — Is this exact fact already recorded? If yes, skip. Don't create redundant entries.
2. **Conflict?** — Does this contradict an existing note? If yes, update the old note with the new information and mark it as superseded (e.g., append "(updated YYYY-MM-DD)" to the heading). A contradictory notebook is worse than no notebook.
3. **Refinement?** — Is this a more precise version of something already there (e.g., a vague preference becomes specific)? If yes, update the existing note in place rather than adding a new one.
4. **New topic?** — If no existing file fits, create a new one.

The goal: every read of the notebook should give a single, coherent, non-contradictory picture — not a chronological mess of overlapping entries.

## First-Time Registration

When creating the first note in a project, register the notebook in `AGENTS.md` and `CLAUDE.md` so future sessions can discover it. This only happens once per project.

### Detection

Search file content for the exact marker `<!-- notebook-skill-registered -->`. If found in either file, skip that file — already registered.

### Template

Insert this block (exact content, no modifications):

```markdown
<!-- notebook-skill-registered -->

## Notebook

- **Skill**: `notebook` — 持久化知识笔记本，跨对话记录重要事实、决策和发现
- **笔记目录**: `.agents-notebooks/`（当前工作目录下）
- **用途**: 记录用户偏好、项目约束、外部事实、关键决策、领域洞察等
- **使用**: 当获得值得记住的新信息时自动触发；也可手动触发记录或回忆已有笔记
```

### Insertion Rules

1. If file doesn't exist → create it with just the template block above.
2. If file has a trailing `---` separator → insert template **before** the separator, with blank lines around it.
3. Otherwise → **append** template at end of file, with a blank line from existing content.
4. **Never modify existing content** — only append/insert.

*Full template and examples: [references/registration-template.md](references/registration-template.md)*

## How to Write Notes

### File Structure

```
.agents-notebooks/
  INDEX.md              # one-line summary per file (maintain when notebook grows)
  user-preferences.md   # topic-based files
  api-constraints.md
  fluid-sim/            # subdirectory for complex topics (use when 5+ notes)
    numerics.md
    boundary-conditions.md
```

**File naming**: `<topic-slug>.md` — lowercase, hyphens, descriptive.

**Subdirectories**: Flat files by default. Add subdirectories only when a topic naturally splits into 5+ distinct notes. Don't over-organize early.

### Note Format

```markdown
# Topic Title

## YYYY-MM-DD — Brief descriptive heading

The fact or insight, stated clearly and concisely. Include enough context that future-you understands why it matters, without re-explaining what's already in the codebase.

Source: [user / research / reasoning / synthesis]
```

Keep entries scannable — 1-3 sentences per note. A note you can't skim in 5 seconds is too long.

### INDEX.md Format

When the notebook grows beyond 10 files, maintain an index:

```markdown
# Notebook Index

- user-preferences.md — coding style, tool choices, communication preferences
- api-constraints.md — external API limits and quirks discovered during development
- fluid-sim/ — numerical methods, boundary conditions, turbulence models
```

## Notebook Location Strategy

| Context | Location | Why |
|---------|----------|-----|
| Default | `.agents-notebooks/` in current working directory | Colocated with the project, easy to find |
| User-specified | Whatever the user says | Always defer to user preference |

## Maintaining Notebook Health

- **Update stale notes**: When you notice a note is outdated, fix or remove it. A wrong note is worse than no note.
- **Merge related notes**: If two notes cover the same topic, combine them.
- **Prune occasionally**: On long projects, review and remove notes that are no longer relevant.

---

*For detailed evaluation criteria and edge cases, see [references/evaluation-guide.md](references/evaluation-guide.md).*
