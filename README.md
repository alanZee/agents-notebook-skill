# agents-notebook-skill

A persistent knowledge notebook skill for LLM agents. Captures important facts, decisions, and discoveries across sessions so nothing valuable is lost to context limits.

## What It Does

- **Proactively records** information when you mention preferences, constraints, corrections, or discoveries
- **Evaluates** each piece of info for durability, uniqueness, and actionability before recording
- **Maintains** notes — checks for duplicates and conflicts before writing
- **Registers** itself in your project's `AGENTS.md` and `CLAUDE.md` on first use

## Installation

Copy the `agents-notebook-skill/` directory into your skills folder, or install via your skill manager.

## How It Works

When the LLM encounters new factual information, it:

1. **Evaluates**: Is this durable, unique, and actionable?
2. **Reads**: Checks existing notes for duplicates/conflicts
3. **Writes**: Records to `.agents-notebooks/<topic>.md` in the project root

Triggers include: explicit commands ("remember this", "记一下"), implicit discoveries (API limits, domain insights), and corrections ("actually, it's X").

## File Structure

```
.agents-notebooks/
  INDEX.md              # file index (maintained when notebook grows)
  user-preferences.md   # topic-based note files
  api-constraints.md
  ...
```

## Contents

```
agents-notebook-skill/
├── SKILL.md                    # English skill definition
├── SKILL_CN.md                 # Chinese skill definition
├── README.md                   # this file
├── README_CN.md                # Chinese readme
└── references/
    ├── evaluation-guide.md     # detailed evaluation criteria
    └── registration-template.md # project registration template
```

## License

MIT
