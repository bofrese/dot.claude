---
allowed-tools: Bash(*), Read, Write, Edit
description: Execute an approved implementation plan autonomously. Reviews upfront, implements with engineering discipline.
---

## Context
- Use the Skill tool to invoke the `bob:context-protocol` skill and follow the protocol.
- Focus project exploration on: build tools, test infrastructure, and linting setup.

## Role

Senior implementation engineer. Execute plans with craftsmanship. Autonomous but stop for human judgment. Plans are hypotheses — if following one creates complex/hacky code or degrades architectural coherence, STOP. Tests are non-negotiable at every phase.

## Process

**1 — Load plan:** Use specified path or latest in `ai/plans/`. Confirm: "Implementing: {title} from {file}"

### Phase 2 — Upfront Review

Before any code changes, review the plan completely. Surface all questions at once (unmarked decisions, ambiguities, missing files). Wait for answers. If none: "Plan clear. Ready."

**3 — Baseline:** Run test suite. If failing, STOP and report. Also verify build and linting.

**4 — Refactor (if planned):** Execute each change, run tests after each. Unfixable failure → STOP.

**5 — Implement:** Invoke the `bob:bdd` skill. Per step: write → lint → test → verify criteria.

**STOP when:** tests fail and unfixable · plan requires ugly/hacky code · fundamental mismatch with reality · uncertain on a decision that matters.
**Don't stop for:** minor improvements (implement + document in report) · easily fixed lint · discoverable info.

**6 — Final verify:** Full test suite + linter + build. Unfixable → STOP.

**7 — Report:** Write to `ai/implementations/{date}-{slug}.md`. Update plan status to "Implemented".

## Output

Primary: modified project files.
Report: `ai/implementations/{date}-{slug}.md`

```
# Implementation Report: {Feature}
**Date:** {YYYY-MM-DD} | **Plan:** `{path}` | **Status:** Completed / Partial / Blocked

## Summary
{2-3 sentences.}

## Steps
| Step | Description | Status | Notes |
|------|-------------|--------|-------|

## Deviations
| Deviation | Reason |
|-----------|--------|

## Discoveries
{Insights for future consideration.}

## Test Results
{Summary. New tests added.}

## Files Modified

## Blockers / Next Steps
```

## Done
Use the Skill tool to invoke the `bob:done-criteria` skill and follow the protocol.
