# Done Criteria — Protocol

This file does two jobs: it defines **how commands interact with the done system**, and it contains the **bootstrap template** that seeds a fresh project.

Commands integrate this with one line in their process:

> *Read `.claude/process/done-criteria.md` and follow the protocol.*

---

## The Protocol — Four Behaviours

### 1. Bootstrap if missing

At the start of your command, check whether `docs/process/done-criteria.md` exists.

If it does **not** exist:
- Create `docs/process/` if needed.
- Copy the **Bootstrap Template** (below) into `docs/process/done-criteria.md`.
- Replace `{date}` with today's date.
- Continue with your command as normal.

If it **does** exist: do nothing. It's already bootstrapped.

### 2. Check before finishing

Before you consider your output complete, read `docs/process/done-criteria.md` and check every item that applies to your command type. If anything isn't satisfied, flag it explicitly in your output rather than shipping incomplete work.

Which items apply:
- `/implement` → Code changes section
- `/plan` → Plans section
- `/review`, `/review-plan` → Reviews section
- `/document` → Documentation section
- Product-tier commands (`/product-vision`, `/design-brief`, `/personas`) → check that output is self-contained and readable without prior context

### 3. Register new artifact types

If your command introduces an artifact type that isn't already tracked in `docs/process/done-criteria.md`, add a new subsection under DONE with the appropriate criteria. This is how the list grows as a project adopts more commands.

**The golden rule:** criteria must be generic, not feature-specific. "Tests must pass" — yes. "The login tests must pass" — no. Feature-specific dependencies belong in the plan.

### 4. Flag decisions for persistence

Before finishing, consider whether important decisions or conventions emerged
during this session that aren't already in your output artifact. If so, flag
them briefly and suggest the user runs `/document` to persist them.

If nothing to flag: skip silently.

---

## Bootstrap Template

Everything below the `---` is the template. Copy it verbatim into `docs/process/done-criteria.md` when bootstrapping. Replace `{date}` with today's date.

---

# Done Criteria

> This file is maintained by commands and humans alike.
> Commands add entries when they introduce new artifact types.
> Humans can add, remove, or edit entries at any time.

---

## READY — Before work starts

These must be true before `/implement` (or any execution command) begins:

- [ ] A plan exists and has been reviewed (`ai/plans/` + `ai/reviews/`)
- [ ] Tests pass at baseline (green before any changes)
- [ ] Applicable guidelines have been read (`docs/guidelines/`)

---

## DONE — Before output is considered complete

Every command checks applicable items before finishing.

### Code changes (`/implement`)
- [ ] All tests pass (existing and new)
- [ ] Linter/formatter clean on modified files
- [ ] No hardcoded secrets or debug code

### Documentation (`/document`)
- [ ] `docs/README.md` index is up to date
- [ ] Related docs cross-referenced

### Plans (`/plan`)
- [ ] Plan is self-contained (readable without prior context)
- [ ] Testing strategy defined
- [ ] Questions & Decisions table populated

### Reviews (`/review`, `/review-plan`)
- [ ] Findings categorised by severity
- [ ] Action items are actionable and prioritised

---

*Last updated: {date}*
*Maintained by: commands and humans*
