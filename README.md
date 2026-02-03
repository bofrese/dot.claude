# dot.claude

A collection of Claude Code slash commands for software development workflows. Language-agnostic, platform-agnostic, designed to work across Swift, Python, PHP, JavaScript/Angular, and any other stack.

## Installation

### Option 1: Git Submodule (recommended for teams)

Add as a submodule in your project root:

```bash
git submodule add https://github.com/bofrese/dot.claude.git .claude
```

To update later:

```bash
git submodule update --remote .claude
```

When cloning a project that uses this as a submodule:

```bash
git clone --recurse-submodules <your-project-url>
# or if already cloned:
git submodule init && git submodule update
```

### Option 2: Direct Copy

Copy the contents directly into your project's `.claude/` folder:

```bash
# Clone and copy
git clone https://github.com/bofrese/dot.claude.git
cp -r dot.claude/commands your-project/.claude/commands
rm -rf dot.claude
```

Or download and extract from GitHub.

### Option 3: User-Level (available in all projects)

Copy to your home directory:

```bash
git clone https://github.com/bofrese/dot.claude.git ~/.claude
```

## Commands Overview

All commands follow a coaching/mentoring style — they work as thinking partners, not just executors. They ask questions, challenge assumptions, and guide you through structured processes.

### Ideation & Planning

| Command | Purpose | Output |
|---------|---------|--------|
| `/brainstorm` | Guided ideation for new features. Diverge → converge → detail → validate against codebase → commit. | `ai/ideas/{date}-brainstorm-{slug}.md` |
| `/plan` | Turn an idea into a concrete implementation plan. Analyzes codebase, plans steps, identifies refactoring needs. | `ai/plans/{date}-{slug}.md` |
| `/review-plan` | Critically review an implementation plan. Find gaps, simpler solutions, security issues, codebase misalignment. | `ai/reviews/{date}-review-{slug}.md` |

### Documentation

| Command | Purpose | Output |
|---------|---------|--------|
| `/document` | Generate or update developer documentation for a concept/subsystem. Detects doc drift. | `docs/{concept}.md` |

### DevOps

| Command | Purpose | Output |
|---------|---------|--------|
| `/docker-setup` | Set up or maintain Docker dev environment. Creates Dockerfile, Makefile, docs. Verifies everything works. | `Dockerfile`, `Makefile`, `docs/install.md`, `ai/docker/{date}-docker-setup.md` |

## Workflow

The commands are designed to flow together:

```
/brainstorm  →  /plan  →  /review-plan  →  implement  →  /document
     ↓
  ai/ideas/      ai/plans/    ai/reviews/                  docs/
```

1. **Brainstorm** an idea until you commit to a direction
2. **Plan** the implementation (or receive a plan from someone else)
3. **Review** the plan critically before implementation
4. After implementation, **document** the new concepts

The `/docker-setup` command stands alone — use it whenever you need to set up or update the dev environment.

## Report Locations

| Folder | Contents |
|--------|----------|
| `ai/ideas/` | Brainstorm session reports |
| `ai/plans/` | Implementation plans |
| `ai/reviews/` | Plan reviews |
| `ai/docker/` | Docker setup logs |
| `docs/` | Developer documentation |

All dated reports use `{YYYY-MM-DD}-{slug}.md` naming.

## Cross-Platform Date Handling

Commands use Python for cross-platform date resolution:

```
`python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
```

Works on macOS and Linux. On Windows (where `python3` may not exist), commands include a fallback instruction for Claude to determine the date using whatever method works.

## Design Principles

These commands are built around several core principles:

- **Coaching, not executing.** Commands guide you through structured thinking, one question at a time. They challenge assumptions and suggest alternatives.
- **Simplicity first.** Always look for the simpler, more generic solution. Code full of exceptions and complex logic means we haven't found the right abstraction.
- **Architectural coherence.** Changes should keep the system clean. No bolted-on features, no legacy fallbacks, no hacks to clean up later.
- **Honest documentation.** Document current state, not aspirations. If something is messy, say so.
- **Standalone outputs.** Reports should be complete enough that someone not present for the conversation can pick them up and proceed.

## Contributing

See [CLAUDE.md](CLAUDE.md) for guidelines on creating new commands or modifying existing ones.

## License

MIT
