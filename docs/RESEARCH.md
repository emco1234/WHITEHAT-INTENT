# Research Sources

This document details the empirical research that informs WHITEHAT-INTENT's design decisions.

---

## 1. Where Do AI Coding Agents Fail? (Ehsani et al., 2026)

**Citation**: Ehsani, R., Pathak, S., Rawal, S., Al Mujahid, A., Imran, M. M., & Chatterjee, P. (2026). Where Do AI Coding Agents Fail? An Empirical Study of Failed Agentic Pull Requests in GitHub. *MSR '26: Proceedings of the 23rd International Conference on Mining Software Repositories*.

**Link**: https://arxiv.org/abs/2601.15195

**Scale**: 33,596 agent-authored PRs across 5 coding agents (OpenAI Codex, GitHub Copilot, Devin, Cursor, Claude Code) on GitHub projects with 100+ stars.

### Key Findings Applied to WHITEHAT-INTENT

| Finding | Data | How WHITEHAT-INTENT Addresses It |
|---|---|---|
| Documentation/CI/build tasks have highest merge rates (74-84%) | Quantitative analysis across task types | Coordinator prioritizes clear, well-scoped tasks |
| Performance/bug-fix tasks have lowest merge rates (55-64%) | Same analysis | Root-cause preflight mandatory for bug fixes |
| Not-merged PRs have larger code changes (Cliff's delta = 17%) | Effect size analysis | Max 5 files, 200 LOC per wave enforced |
| Not-merged PRs touch more files (Cliff's delta = 10%) | Same | Same enforcement |
| Not-merged PRs have more CI failures (Cliff's delta = 24%) | Same | Biome post-edit gate mandatory |
| Each additional failed CI check decreases merge odds by ~15% | Logistic regression | Biome gate blocks progression until clean |
| **Reviewer abandonment is #1 rejection pattern (38%)** | 600 PR qualitative analysis | Living spec provides context for reviewers |
| **Duplicate PRs account for 23% of rejections** | Same | Duplicate check before every task |
| Unwanted features account for 4% of rejections | Same | Scope boundary enforcement in Implementor |
| CI/test failures account for 17% of rejections | Same | Biome + project test gates |
| Incorrect implementation: 3%, Incomplete: 2% | Same | Bidirectional spec-to-code traceability |
| Agent misalignment: 1% (ignoring reviewer instructions) | Same | Spec as single source of truth |
| Maintainers prefer "small, focused, limited to single coherent change" | Reviewer feedback analysis | Single purpose per wave rule |

### Rejection Taxonomy (from paper)

```
Reviewer Level (38%)
├── Abandoned/Not Reviewed (228 PRs)

Pull Request Level (31%)
├── Duplicate PR (142 PRs)
├── Unwanted Feature (24 PRs)
├── Non-Functional PR (13 PRs)
├── Wrong Task Description (7 PRs)
└── Wrong Branch (2 PRs)

Code Level (22%)
├── CI/Test Failure (99 PRs)
├── Incorrect Implementation (19 PRs)
└── Incomplete Implementation (15 PRs)

Agentic Level (2%)
├── Misalignment (9 PRs)
└── License Issues (4 PRs)
```

---

## 2. Understanding Spec-Driven-Development (Böckeler, 2025)

**Citation**: Böckeler, B. (2025). Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl. *Thoughtworks Exploring Gen AI series*.

**Link**: https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html

### Key Findings Applied to WHITEHAT-INTENT

| Finding | How WHITEHAT-INTENT Addresses It |
|---|---|
| Three SDD maturity levels: spec-first, spec-anchored, spec-as-source | WHITEHAT-INTENT implements spec-as-source: spec is primary artifact, code generated downstream |
| Problem-size adaptability is critical | MICRO/MEDIUM/MACRO classification with scaled ceremony |
| Verbose specs create "review overload" | Spec quality control: max 200 lines, concise requirement |
| Tools using one workflow for all sizes fail | Three distinct workflow levels |
| "False sense of control" from excessive checklists | Focused, actionable gates (Context7 + Biome) not verbose checklists |
| Functional vs technical spec separation is hard | Coordinator separates functional intent from implementation |
| MDD (Model-Driven Development) lessons: flexibility + non-determinism tradeoffs | Spec auto-updates to match reality, not rigid |
| Small iterative steps are safer than big upfront design | Wave-based execution with per-wave spec updates |

### SDD Maturity Levels (from paper)

```
Spec-First:     Spec → Code → [Spec deleted]
Spec-Anchored:  Spec → Code → [Spec kept, updated during evolution]
Spec-as-Source: Spec → Code → [Human never touches code, only edits spec]
                              ↑ WHITEHAT-INTENT targets this level
```

---

## 3. Using Git Worktrees for Multi-Feature Development with AI Agents (Mitchinson, 2025)

**Citation**: Mitchinson, N. (2025). Using Git Worktrees for Multi-Feature Development with AI Agents.

**Link**: https://www.nrmitchi.com/2025/10/using-git-worktrees-for-multi-feature-development-with-ai-agents/

### Key Findings Applied to WHITEHAT-INTENT

| Finding | How WHITEHAT-INTENT Addresses It |
|---|---|
| Worktrees provide isolation for parallel agents | Coordinator plans waves to minimize file overlap |
| Clear worktree boundaries prevent agent confusion | Scope boundary enforcement: only touch assigned files |
| Safe git operations per worktree | Permission system restricts dangerous git operations |
| Context pollution between features | Each wave has explicit file scope bounds |
| Agent stepping on each other's toes | Single purpose per wave, no unrelated edits combined |
| Merge at integration time, not during development | Integration planning in Coordinator maps cross-wave dependencies |

---

## 4. The End of Linear Work / Intent Manifesto (Intent Team, 2026)

**Citation**: Intent Team. (2026). The End of Linear Work. *Intent blog*.

### Key Findings Applied to WHITEHAT-INTENT

| Finding | How WHITEHAT-INTENT Addresses It |
|---|---|
| "The spec becomes the coordination layer" | Living spec is canonical, all agents read from it |
| "Tickets don't describe agent work" | Structured specs with GIVEN/WHEN/THEN acceptance criteria |
| "Agents don't share intuition or negotiate ambiguity" | Explicit constraints, done criteria, and scope bounds in spec |
| "Make intent explicit and constraints clear" | Problem-size detection, anti-pattern prevention, spec quality control |
| "Review moves earlier and gets cheaper" | Verification gates at every wave, not just at the end |
| "The plan becomes the product" | Spec auto-updates to reflect reality; spec IS the deliverable |
| "Implementation is becoming inexpensive; defining 'done' is the constraint" | Testable acceptance criteria required before any implementation |
| Coordination is the hard problem, not execution | Coordinator handles task decomposition, dependency graph, conflict detection |

---

## Summary: Research-to-Feature Mapping

| Research Insight | WHITEHAT-INTENT Feature |
|---|---|
| 23% of agent PRs are duplicates | Duplicate work prevention (git log, branches, issues check) |
| Larger changes = lower merge rate | Max 5 files, 200 LOC per wave |
| CI failures = 15% lower merge odds per failure | Biome post-edit gate (hard block) |
| Vague tickets cause agent misalignment | Root-cause preflight for ambiguous requests |
| Reviewer abandonment (38%) | Living spec provides context and progress visibility |
| One workflow doesn't fit all sizes | MICRO/MEDIUM/MACRO classification |
| Verbose specs = review overload | Spec quality control (200 line limit) |
| Specs should be source of truth | Spec-as-source philosophy |
| Agents need explicit "done" definition | Testable GIVEN/WHEN/THEN acceptance criteria |
| Parallel agents need coordination | Spec as coordination layer, integration planning |
| Small iterative steps beat big upfront design | Wave-based execution with per-wave updates |
