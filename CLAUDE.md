# CLAUDE.md — Command Development Guidelines

This file guides Claude (and human contributors) in creating new commands and maintaining existing ones for this repository.

## Repository Structure

```
.claude/
├── commands/
│   ├── brainstorm.md
│   ├── plan.md
│   ├── review-plan.md
│   ├── document.md
│   └── docker-setup.md
├── CLAUDE.md          ← You are here
└── README.md          ← User-facing documentation
```

## When Modifying This Repository

**Always keep README.md in sync.** When you add, remove, or significantly change a command:
- Update the Commands Overview table
- Update the Workflow section if the command fits into the flow
- Update Report Locations if the command writes to a new folder
- Update any other affected sections

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
| Docker/DevOps logs | `ai/docker/` |
| Documentation | `docs/` |

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

Some commands only analyze and produce reports:
- `/brainstorm` — produces an idea report
- `/plan` — produces an implementation plan
- `/review-plan` — produces a review report
- `/document` — produces/updates documentation (but doesn't change application code)

Some commands actually modify the project:
- `/docker-setup` — creates/modifies Dockerfile, Makefile, etc.

For implementing commands:
- Include verification steps (did it actually work?)
- Handle failures gracefully (diagnose, fix, or ask for help)
- Be explicit about what files were created/modified

For planning/analysis commands:
- Include a clear "DO NOT IMPLEMENT" guardrail
- Reports should be actionable but not action-taking
