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

## The Full Picture

For a detailed walkthrough of the vision, the philosophy, how commands connect, and how to use the toolkit across an entire product lifecycle — read the [User Guide](docs/user-guide.md).

> **Note:** The user guide describes the complete vision, including commands and systems that are still being built. Not everything documented there is implemented yet. It reflects where this project is heading, not just where it is today.

---

## Commands Overview

All commands follow a coaching/mentoring style — they work as thinking partners, not just executors. They ask questions, challenge assumptions, and guide you through structured processes.

### Discovery — What to Build and Why

| Command | Purpose | Output |
|---------|---------|--------|
| `/product-vision` | Establish or refine the product vision. The single source of truth for what, who, and why. | `docs/product/vision.md` |
| `/personas` | Define user personas grounded in the product vision. | `docs/product/personas.md` |
| `/design-brief` | Create the design brief from vision and personas. | `docs/product/design-brief.md` |

### Engineering — How to Build It

| Command | Purpose | Output |
|---------|---------|--------|
| `/brainstorm` | Guided ideation for features. Diverge → converge → detail → validate against codebase → commit. | `ai/ideas/{date}-brainstorm-{slug}.md` |
| `/plan` | Turn an idea into a concrete, self-contained implementation plan. | `ai/plans/{date}-{slug}.md` |
| `/review-plan` | Critically review a plan. Checks assumptions against the actual codebase. | `ai/reviews/{date}-review-{slug}.md` |
| `/implement` | Execute an approved plan. Tests at every step. Stops when human judgment is needed. | `ai/implementations/{date}-{slug}.md` |
| `/review` | Code review. Auto-detects scope, checks guidelines, assesses system health. | `ai/reviews/{date}-review-{slug}.md` |

### Knowledge — Documentation & Guidelines 

| Command | Purpose | Output |
|---------|---------|--------|
| `/document` | Generate or update developer documentation. Detects doc drift. | `docs/{concept}.md` |
| `/guidelines` | Create and maintain best practice guidelines. Research-first. | `docs/guidelines/{topic}.md` |

### Meta — The Toolkit Maintains Itself

| Command | Purpose | Output |
|---------|---------|--------|
| `/new-command` | Create a new slash command. Guides through design, creates the file, updates README. | `.claude/commands/{name}.md` |
| `/review-command` | Review a command for token efficiency, clarity, actionability. | `ai/reviews/{date}-command-review-{slug}.md` |



### DevOps

| Command | Purpose | Output |
|---------|---------|--------|
| `/docker-setup` | Set up or maintain Docker dev environment. Creates Dockerfile, Makefile, docs. Verifies everything works. | `Dockerfile`, `Makefile`, `docs/install.md`, `ai/docker/{date}-docker-setup.md` |

## Workflow

Three layers, not three stages. They form a cycle:

```
Discovery          →  grounds  →  Engineering pipeline
  /product-vision                   /brainstorm  →  /plan  →  /review-plan
  /personas                         /implement   →  /review
  /design-brief                            ↓
                                     Knowledge
                                       /document  ←→  /guidelines
                                            ↑
                                     guides future Engineering
```

**Discovery** establishes what you're building and why. **Engineering** turns ideas into reviewed, tested code. **Knowledge** accumulates the wisdom that makes every future session better. Each layer feeds the others.

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
| `docs/product/` | Product vision, personas, design brief |
| `docs/process/` | Done criteria and process contracts |
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

---

## License

This project is licensed under the **Apache License 2.0**.

Apache 2.0 means you can use, modify, and distribute this toolkit — commercially or otherwise — for any project. The one thing that must travel with it: the copyright and attribution notice. That's it. No copyleft. No share-alike. No restrictions on what you build with it.

See the [LICENSE](LICENSE) file for the full legal text.

---

## Attribution

Created by **[Bo Frese](https://bofrese.dk)** — [bofrese.dk](https://bofrese.dk)

---

## About the Author

Bo works at the intersection of software development and agile process design — with a particular focus on how teams can integrate AI tools effectively into their workflows without losing the things that make good development good: human judgment, architectural discipline, and the ability to actually understand what you're shipping.

If you're looking for hands-on development help, or if your team wants to think more carefully about how AI fits into your process, Bo is available for both. More at [bofrese.dk](https://bofrese.dk) and [agilecoach.dk](https://agilecoach.dk).
