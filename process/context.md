# Context Loading Protocol

Commands integrate with one line in their Context block:

> *Read `.claude/process/context.md` and follow the protocol.*

---

## Universal (All Commands)

**Date:** Run `python3 -c "from datetime import date;print(date.today().isoformat(),end='')"`
If that fails, determine today's date in YYYY-MM-DD via any available command. Use this date in all output filenames and document timestamps.

**Project familiarity:** Silently explore the project structure before starting. Commands with specific focus areas note them in their Context block.

---

## Per-Command Loading

Read each listed file if it exists. Skip silently if missing. Skip any file already read in this conversation.

| Command | Load at start |
|---------|--------------|
| `/product-vision` | `docs/product/vision.md` |
| `/personas` | `docs/product/vision.md`, `docs/product/design-brief.md` |
| `/design-brief` | `docs/product/vision.md`, `docs/product/personas.md` |
| `/problem-space` | `docs/product/vision.md`, `docs/product/problem-space.md` |
| `/business-plan` | `docs/product/vision.md`, `docs/product/business-plan.md` |
| `/positioning` | `docs/product/vision.md`, `docs/product/positioning.md` |
| `/validation-plan` | `docs/product/vision.md`, `docs/product/validation-plan.md` |
| `/product-coach` | `docs/product/vision.md`, `docs/product/README.md` |
| `/art-director` | `docs/product/vision.md` |
| `/brainstorm` | `docs/product/vision.md` |
| `/plan` | `docs/product/vision.md` |
| `/review-plan` | `docs/product/vision.md` |
| `/implement` | `docs/product/vision.md` |
| `/review` | `docs/product/vision.md` |
| `/ui-review` | `docs/product/vision.md`, `docs/product/personas.md`, `docs/product/design-brief.md`, `.claude/principles/ui-design.md` |
| `/new-command` | `.claude/principles/prompt-engineering.md` |
| `/review-command` | `.claude/principles/prompt-engineering.md` |
| `/improve-command` | `.claude/principles/prompt-engineering.md` |
| `/investigate` | — |
| `/document` | — |
| `/guidelines` | — |
| `/docker-setup` | — |
| `/dot` | — |

---

## Guidelines (Engineering commands, after scope is clear)

For `/brainstorm`, `/plan`, `/review-plan`, `/implement`, `/review`, `/ui-review`:

1. Read `docs/guidelines/README.md` as navigation — do not load all guideline files.
2. Load only guidelines matching the current scope:
   - File extensions in play (e.g., `.ts` → typescript.md)
   - Paths involved (e.g., `Frontend/` → angular.md)
   - Concepts being touched (e.g., auth changes → authentication.md)
3. If `docs/guidelines/` doesn't exist, skip silently.
