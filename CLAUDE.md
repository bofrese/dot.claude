# CLAUDE.md — Command Development Guidelines

This file guides Claude (and human contributors) in creating new commands and maintaining existing ones for this repository.

## Repository Structure

```
.claude/
├── commands/                  ← all slash commands (flat — no subfolders)
│   ├── product-vision.md      ← Discovery tier
│   ├── design-brief.md        ← Discovery tier
│   ├── personas.md            ← Discovery tier
│   ├── brainstorm.md          ← Engineering tier
│   ├── plan.md                ← Engineering tier
│   ├── review-plan.md         ← Engineering tier
│   ├── implement.md           ← Engineering tier
│   ├── review.md              ← Engineering tier
│   ├── document.md            ← Knowledge tier
│   ├── guidelines.md          ← Knowledge tier
│   ├── new-command.md         ← Meta
│   ├── review-command.md      ← Meta
│   └── docker-setup.md        ← DevOps
├── principles/                ← on-demand knowledge frameworks (see below)
│   ├── bdd.md
│   └── ddd.md
├── process/                   ← interaction protocols (see below)
│   └── done-criteria.md       ← the done system protocol + bootstrap template
├── docs/                      ← user guide and documentation
│   └── user-guide.md
├── CLAUDE.md                  ← You are here
├── README.md                  ← User-facing documentation
└── LICENSE
```

## When Modifying This Repository

**Always keep README.md in sync.** When you add, remove, or significantly change a command:
- Update the Commands Overview table
- Update the Workflow section if the command fits into the flow
- Update Report Locations if the command writes to a new folder
- Update any other affected sections

## The Two Tiers

Commands fall into two conceptual tiers. Both live in the same `commands/` folder. The distinction is about what they're concerned with, not where they live.

**Discovery** — What to build and why. Output is product artifacts: vision, personas, design briefs. These live in `docs/product/` (authoritative, updated in place).

**Engineering** — How to build it. Output is plans, code, reviews, documentation. Session artifacts live in `ai/` (disposable). Authoritative docs live in `docs/`.

The key connection: **Discovery output is input to Engineering.** A product vision grounds a brainstorm. A design brief informs a plan. Engineering commands know to look for relevant Discovery artifacts at well-known paths in `docs/product/`.

## Principles — On-Demand Knowledge

Small files in `principles/` that encode core thinking frameworks. Not tutorials — just enough that when a command loads one, it applies the framework consistently.

**How commands use them:** A command loads a principle at the specific point in its process where the framework applies. Example: `/plan` loads `bdd.md` when defining the testing strategy. `/brainstorm` loads `ddd.md` when decomposing a problem.

**What goes here vs `docs/guidelines/`:**
- `principles/` = generic frameworks. "How to think about BDD." Works for any project. Travels with the submodule.
- `docs/guidelines/` = project-specific application. "How we do BDD in this Angular/PHP project." Specific to the codebase.

## Done Criteria Protocol

Every output-producing command participates in the done system. The integration is a single line at the end of the command:

> *Read `.claude/process/done-criteria.md` and follow the protocol.*

The protocol file (`.claude/process/done-criteria.md`) contains everything: the bootstrap template AND the three behaviours commands follow (bootstrap the project file if missing, check criteria before finishing, register new artifact types). Commands don't each carry their own copy of the logic — they load the protocol.

The project's live instance (`docs/process/done-criteria.md`) is bootstrapped automatically the first time any command runs in a fresh project. It grows as the project adopts more commands.

**When creating a new command:** include the done-criteria protocol line. `/new-command` enforces this. `/review-command` flags its absence.

## Command File Structure

Every command follows this structure:

```markdown
---
allowed-tools: Bash(*), Read, Write, Edit
description: One-line description of what this command does.
---

## Context
- Today's date: `python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
- If the date above is blank, determine today's date in YYYY-MM-DD format using any available command.
- This is an existing project. Silently familiarize yourself with the project structure, key architectural patterns, and UI conventions before starting.

## Role
Who Claude is in this context. Senior architect, coach, reviewer, etc.

## Core Principles (or similar)
The guiding principles for this specific command.

## Process
Step-by-step phases the command goes through.

## Rules
Behavioral rules and constraints.

## Output
Where files are written and what format they follow.
Include a template for any generated reports.
```

### Frontmatter

```yaml
---
allowed-tools: Bash(*), Read, Write, Edit
description: Brief description shown in command listings.
---
```

- `allowed-tools`: Almost always `Bash(*), Read, Write, Edit` for full capability.
- `description`: Keep it short — this appears in `/help` or command listings.

### Date Handling

Always use Python for cross-platform compatibility:

```markdown
- Today's date: `python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
- If the date above is blank, determine today's date in YYYY-MM-DD format using any available command.
```

The fallback instruction handles Windows where `python3` doesn't exist.

### Context Block

Every command should include:
- The date resolution (as above)
- Instruction to silently analyze the project before starting

This ensures Claude has context before engaging with the user.

## Design Principles for Commands

### Coaching Style

Commands act as mentor/coach/thinking partner, not just executor:
- Ask questions one at a time
- Challenge assumptions
- Suggest alternatives
- Come up with own ideas
- Guide through structured phases

### Simplicity First

Always push toward simpler solutions:
- Challenge requirements if it unlocks a cleaner approach
- Look for generic solutions over special-cased ones
- Prefer existing patterns over new abstractions

### Architectural Coherence

The codebase must stay clean after any change:
- No bolted-on features
- No legacy fallbacks or backward compatibility hacks
- No "clean up later" technical debt
- Refactoring is a first-class phase, not an afterthought

### Honest Assessment

- Document current state, not aspirations
- If something is messy, say so
- If a plan has problems, flag them directly
- Don't soften critical findings

### Standalone Outputs

Reports must be complete enough that someone not present for the conversation can:
- Understand what was discussed/decided
- Proceed with the next step (implementation, review, etc.)
- Maintain the code confidently

### Target Audience

- Experienced developers and AI agents
- Explain the *what* and *why* clearly
- Don't over-explain implementation mechanics
- Don't skip architectural context

## Output Locations

Commands write to specific folders by convention:

| Command Type | Output Folder |
|--------------|---------------|
| Ideation | `ai/ideas/` |
| Planning | `ai/plans/` |
| Reviews | `ai/reviews/` |
| Implementation reports | `ai/implementations/` |
| Docker/DevOps logs | `ai/docker/` |
| Product artifacts | `docs/product/` |
| Process contracts | `docs/process/` |
| Documentation | `docs/` |
| Guidelines | `docs/guidelines/` |

File naming: `{YYYY-MM-DD}-{slug}.md` for dated reports.

Commands should create their output folder if it doesn't exist.

## Report Templates

Every command that generates a report should include a template in its Output section. Templates should:
- Start with a title and date
- Include a status or verdict where appropriate
- Use tables for structured data
- Use Mermaid diagrams for architecture/flow visualization
- Include clear sections that match the command's process phases

## Testing Considerations

Commands that involve implementation (like `/plan` or `/docker-setup`) should include testing checkpoints:
- Verify baseline (tests pass before changes)
- Verify after refactoring (behavior unchanged)
- Define test strategy for new features
- Verify after implementation (all tests pass)

## Creating a New Command

1. **Identify the need.** What workflow gap does this fill? How does it relate to existing commands?

2. **Define the output.** What does the command produce? Where does it go?

3. **Design the process.** What phases does the user go through? Keep it conversational.

4. **Write the command file.** Follow the structure above. Include:
   - Clear role definition
   - Core principles specific to this command
   - Step-by-step process
   - Behavioral rules
   - Output template
   - Done-criteria protocol line at the end: *Read `.claude/process/done-criteria.md` and follow the protocol.*

5. **Test it.** Run the command on a real project. Does it flow well? Are the outputs useful?

6. **Update README.md.** Add to the Commands Overview table and any other affected sections.

## Modifying an Existing Command

1. **Understand the current design.** Read the whole command file. Understand the phases and principles.

2. **Make targeted changes.** Don't rewrite unnecessarily. Extend, don't replace.

3. **Preserve the style.** Match the existing tone, structure, and level of detail.

4. **Update the README.md** if the change affects:
   - Command description
   - Output location
   - How it fits in the workflow

5. **Test the modified command** on a real project.

## Style Guidelines

- Use second person ("You are...") for role definitions
- Use imperative mood for instructions ("Ask me...", "Walk me through...")
- Use Markdown formatting consistently
- Keep sections focused — if a section is getting long, consider splitting it
- Use tables for structured information
- Use code blocks for templates, commands, and file examples
- Use Mermaid for diagrams where visual representation helps

## Commands That Implement vs. Commands That Plan

Some commands only analyze and produce reports or artifacts:
- `/product-vision` — produces/updates the product vision (`docs/product/`)
- `/design-brief` — produces/updates the design brief (`docs/product/`)
- `/personas` — produces/updates personas (`docs/product/`)
- `/brainstorm` — produces an idea report
- `/plan` — produces an implementation plan
- `/review-plan` — produces a review report
- `/review` — produces a code review report
- `/document` — produces/updates documentation (but doesn't change application code)
- `/guidelines` — produces/updates best practice guidelines (but doesn't change application code)

Some commands actually modify the project:
- `/implement` — writes code, runs tests, modifies project files
- `/docker-setup` — creates/modifies Dockerfile, Makefile, etc.

For implementing commands:
- Include verification steps (did it actually work?)
- Handle failures gracefully (diagnose, fix, or ask for help)
- Be explicit about what files were created/modified

For planning/analysis commands:
- Include a clear "DO NOT IMPLEMENT" guardrail
- Reports should be actionable but not action-taking
