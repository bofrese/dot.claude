# Context Loading Protocol

This file defines what commands load at session start. Commands integrate it with one line in their Context block:

> *Read `.claude/process/context.md` and follow the protocol.*

---

## Loading Rules

| Tier | Commands | Load at start | Load after scope is clear |
|---|---|---|---|
| Discovery | `/product-vision`, `/personas`, `/design-brief` | Vision (if exists) | — |
| Engineering | `/brainstorm`, `/plan`, `/review-plan`, `/implement`, `/review` | Vision (if exists) | Guidelines matching scope |
| Knowledge | `/document`, `/guidelines` | — | — |
| Meta | `/new-command`, `/review-command` | — | — |
| DevOps | `/docker-setup` | — | — |

### Vision

If `docs/product/vision.md` exists, read it. If not, skip silently.

### Guidelines (Engineering commands only, after scope is clear)

1. Read `docs/guidelines/README.md` as navigation — do not load all guideline files.
2. Load only guidelines that match the current scope:
   - File extensions being worked with (e.g., `.ts` → typescript.md)
   - Paths involved (e.g., `Frontend/` → angular.md)
   - Concepts being touched (e.g., auth changes → authentication.md)
3. If `docs/guidelines/` doesn't exist, skip silently.

### Guard

Skip any file already read in this conversation. Do not re-read.
