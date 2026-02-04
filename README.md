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
| `/implement` | Execute an approved plan autonomously. Reviews upfront, implements with engineering discipline, stops only on blockers. | `ai/implementations/{date}-{slug}.md` |
| `/review` | Review code changes critically. Auto-detects scope, checks guidelines, assesses system health, enables ownership transfer. | `ai/reviews/{date}-review-{slug}.md` |

### Command Development

| Command | Purpose | Output |
|---------|---------|--------|
| `/new-command` | Create a new slash command. Guides through design, creates the file, updates README. | `.claude/commands/{name}.md` |
| `/review-command` | Review a Claude command for AI optimization — token efficiency, clarity, actionability. | `ai/reviews/{date}-command-review-{slug}.md` |

### Documentation & Guidelines

| Command | Purpose | Output |
|---------|---------|--------|
| `/document` | Generate or update developer documentation for a concept/subsystem. Detects doc drift. | `docs/{concept}.md` |
| `/guidelines` | Create and maintain project-specific best practice guidelines for languages, frameworks, and concepts. | `docs/guidelines/{topic}.md` |

### DevOps

| Command | Purpose | Output |
|---------|---------|--------|
| `/docker-setup` | Set up or maintain Docker dev environment. Creates Dockerfile, Makefile, docs. Verifies everything works. | `Dockerfile`, `Makefile`, `docs/install.md`, `ai/docker/{date}-docker-setup.md` |

## Workflow

The commands are designed to flow together:

```
/brainstorm  →  /plan  →  /review-plan  →  /implement  →  /review  →  /document
     ↓            ↓            ↓               ↓              ↓           ↓
  ai/ideas/    ai/plans/    ai/reviews/   ai/implementations/ ai/reviews/  docs/
```

1. **Brainstorm** an idea until you commit to a direction
2. **Plan** the implementation (or receive a plan from someone else)
3. **Review the plan** critically before implementation
4. **Implement** the approved plan autonomously
5. **Review the code** — assess what was built, check system health, enable ownership transfer
6. After review, **document** the new concepts

The `/docker-setup` command stands alone — use it whenever you need to set up or update the dev environment.

The `/new-command` and `/review-command` are meta-commands for extending and maintaining the command toolkit itself.

## Report Locations

| Folder | Contents |
|--------|----------|
| `ai/ideas/` | Brainstorm session reports |
| `ai/plans/` | Implementation plans |
| `ai/reviews/` | Plan reviews, command reviews, and code reviews |
| `ai/implementations/` | Implementation execution reports |
| `ai/docker/` | Docker setup logs |
| `docs/` | Developer documentation |
| `docs/guidelines/` | Best practice guidelines |

All dated reports use `{YYYY-MM-DD}-{slug}.md` naming.

## Cross-Platform Date Handling

Commands use Python for cross-platform date resolution:

```
`python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
```

Works on macOS and Linux. On Windows (where `python3` may not exist), commands include a fallback instruction for Claude to determine the date using whatever method works.

## Guidelines Integration

When using this command set, you can maintain project-specific guidelines in `docs/guidelines/`. The `/guidelines` command helps create and maintain them.

**To enable automatic guideline loading**, add this to your project's `CLAUDE.md`:

```markdown
## Guidelines

Before starting work, check `docs/guidelines/README.md` for applicable guidelines.
Load guidelines that match:
- File extensions you're working with (e.g., `.ts` → typescript.md)
- Paths involved (e.g., `Frontend/` → angular.md)
- Concepts being touched (e.g., login flow → authentication.md)
```

This makes guidelines ambient context for all commands without modifying each command file.

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
