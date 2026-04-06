# Living Spec Template

## Meta
- Spec ID: `intent-YYYYMMDD-HHMM`
- Workspace: `<path-or-repo>`
- Branch: `<branch>`
- Status: `active`
- Last Updated: `<ISO-8601>`

## Task Classification
- Size: `MICRO | MEDIUM | MACRO`
- Rationale: `<why this classification>`
- Workflow: `inline-spec | focused-spec | full-spec`
- Estimated files: `<number>`
- Estimated LOC: `<number>`

## Intent
Short statement of what should be built/fixed and why.

## Duplicate Check
- Date checked: `<ISO-8601>`
- Git log (last 30 days): `<related commits found or none>`
- Open branches: `<overlapping branches or none>`
- Open issues/PRs: `<overlapping items or none>`
- Overlap found: `yes | no`
- If yes, user decision: `<proceed/merge/defer>`

## Constraints
- Architecture constraints
- Style/convention constraints
- Risk constraints
- Context7 lookup required per request and before each edit wave
- Biome lint required after every edit on touched files
- No script-based file rewrites; manual edit/patch only
- File comparisons/layout diagnosis must be Read-based, not shell diff/cat-based
- For frontend work, verify in browser with Playwright MCP first (Chrome DevTools MCP fallback)
- Record this verification line in the wave evidence:
  - `I'll verify the fixes in the browser using the Playwright MCP tools.`

## Change Scope Bounds
- Max files per wave: 5
- Max LOC per wave: 200
- Files in scope: `<list>`
- Files explicitly excluded: `<list>`
- If exceeded: decompose into sub-waves before proceeding

## Acceptance Criteria
Each criterion must be testable and measurable:
- [ ] Criterion 1 (GIVEN ... WHEN ... THEN ...)
- [ ] Criterion 2 (GIVEN ... WHEN ... THEN ...)
- [ ] Criterion 3 (GIVEN ... WHEN ... THEN ...)

## Task Checklist
Each task: single responsibility, max 5 files, max 200 LOC:
- [ ] Task 1 (files: `<list>`, estimated LOC: `<n>`)
- [ ] Task 2 (files: `<list>`, estimated LOC: `<n>`)
- [ ] Task 3 (files: `<list>`, estimated LOC: `<n>`)

## Integration Risk
- Cross-wave file dependencies: `<list overlapping files between waves>`
- High-conflict files (frequently changed): `<list>`
- Breaking change potential: `low | medium | high`
- Integration checkpoints: `<list validation points between waves>`

## Execution Waves
### Wave N
- Owner: `<agent>`
- Purpose: `<single coherent purpose>`
- Scope: `<files and LOC bounds>`
- Context7 guidance: `<recorded guidance or BLOCKER>`
- Result: `pending | done | failed`
- Evidence: `<verification evidence>`
- Spec updated: `yes | no`

## Spec-to-Code Traceability
| Acceptance Criterion | Code Changes (file:line) | Status |
|---------------------|-------------------------|--------|
| AC 1                |                         | mapped |
| AC 2                |                         | mapped |

| Code Change         | Spec Requirement         | Status |
|---------------------|-------------------------|--------|
| file:line           | AC / Task               | justified |

## Verification
- [ ] Spec-to-code traceability: every AC maps to code, every code change maps to spec
- [ ] Change size within bounds (files <= 10, LOC <= 500 total)
- [ ] No unrelated changes included
- [ ] Tests pass for implementation waves
- [ ] Diagnostics clean for changed files
- [ ] Context7 guidance applied for touched stack
- [ ] Biome clean for edited files
- [ ] Integration regression: cross-wave flows verified
- [ ] Browser verification evidence recorded for frontend changes
- [ ] Branch targets correct base
- [ ] Acceptance criteria satisfied

## PR Readiness
- Total files changed: `<n>`
- Total LOC delta: `<n>`
- CI status: `passing | failing | not run`
- Branch target: `<branch>`
- Scope creep detected: `yes | no`
- Duplicate overlap: `yes | no`
- Ready for merge: `yes | no`
- Blockers: `<list>`

## Wave Log
Chronological record of what was ACTUALLY built vs planned:
- Wave N: `<summary of what happened, any deviations from plan>`
