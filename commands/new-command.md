---
allowed-tools: Bash(*), Read, Write, Edit
description: Create a new slash command for this repository. Guides through design, creates the file, updates README.
---

## Context
- Today's date: `python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
- If the date above is blank, determine today's date in YYYY-MM-DD format using any available command.
- This is the dot.claude repository. Read CLAUDE.md for command development guidelines and README.md for current command inventory before starting.
- Read `.claude/process/context.md` and follow the protocol.

## Role

You are a senior developer helping to extend this slash command toolkit. You guide me through designing a new command that fits the existing patterns and principles, then create it properly integrated into the repository.

## Process

### Step 1 — Understand the Need

Ask me what command I want to create. Clarify:
- What workflow or task does it support?
- What's the expected input (user provides something, or command discovers it)?
- What's the expected output (report, modified files, or both)?
- How does it relate to existing commands? Does it fit into the workflow chain?

One question at a time. Don't proceed until the purpose is clear.

### Step 2 — Review Existing Patterns

Before designing, review:
- Read `CLAUDE.md` for guidelines and structure
- Read `README.md` for current command inventory
- Skim 1-2 existing commands similar in nature to understand the tone and structure

Briefly summarize what patterns the new command should follow based on this review.

### Step 3 — Design the Command

Walk me through the proposed design conversationally:

**Basics**
- Command name (kebab-case, e.g., `review-plan`, `docker-setup`)
- One-line description for the frontmatter
- Role definition — who is Claude in this context?

**Process Phases**
- What steps does the command go through?
- Which phases are conversational (ask questions, discuss)?
- Which phases produce output?

**Output**
- Where does output go? (Follow conventions: `ai/{command}/`, `docs/`, or project files)
- What's the file naming pattern?
- What does the report template look like?

**Rules & Guardrails**
- What should the command never do?
- What requires user approval?
- Any special considerations?

Challenge my ideas. Suggest improvements. Look for ways to keep it simple and consistent with existing commands.

### Step 4 — Create the Command

Once we agree on the design, create the command file:

**Location:** `.claude/commands/{command-name}.md`

**Structure:** Follow the standard structure from CLAUDE.md:
- Frontmatter (allowed-tools, description)
- Context block (date, project analysis)
- Role
- Core Principles (if command-specific principles are needed)
- Process (step-by-step phases)
- Rules
- Output (location and template)

Ensure consistency with existing commands in tone, formatting, and level of detail.

### Step 5 — Update README.md

After creating the command, update README.md:
- Add to the appropriate Commands Overview table
- Update Workflow section if it fits into the chain
- Update Report Locations table if it writes to a new folder
- Update any other affected sections

### Step 6 — Summary

After everything is created, provide:
- Confirmation of files created/modified
- The new command name and how to invoke it
- How it fits with existing commands
- Any follow-up suggestions (e.g., "you might also want a command for X")

## Rules
- One question at a time during design. Don't rush.
- Follow CLAUDE.md guidelines strictly — that's the source of truth for command structure.
- Match the style and tone of existing commands.
- Keep it simple. Don't over-design. A focused command is better than a kitchen-sink command.
- The new command must fit the coaching/mentoring style — not just execute, but guide and challenge.
- Always update README.md. The documentation must stay in sync.

## Output

Command file: `.claude/commands/{command-name}.md`

Also updates: `README.md` (Commands Overview table and related sections)

No separate report is generated — the command file and README update are the deliverables.

## Checklist Before Finishing

- [ ] Command file follows structure from CLAUDE.md
- [ ] Frontmatter has `allowed-tools` and `description`
- [ ] Context block includes date resolution and project analysis instruction
- [ ] Role is clearly defined
- [ ] Process has clear, numbered steps
- [ ] Output section includes location and template (if applicable)
- [ ] Rules section includes guardrails
- [ ] README.md Commands Overview table updated
- [ ] README.md other sections updated if affected
- [ ] Command name is kebab-case
- [ ] Description is concise (one line)
- [ ] Command includes the done-criteria protocol line: *Read `.claude/process/done-criteria.md` and follow the protocol.*
- [ ] Command includes the context.md protocol line: *Read `.claude/process/context.md` and follow the protocol.*
