<div align="center">

# WHITEHAT-INTENT

**The Research-Backed Spec-Driven Development System for OpenCode**

> *"The plan becomes the product."*

The living spec is the source of truth. Code is generated downstream. The spec auto-updates to reflect what was actually built. Every failure mode from 33,000+ real agent PRs is addressed with a guardrail.

[![OpenCode Compatible](https://img.shields.io/badge/OpenCode-Compatible-blue)](https://opencode.ai)
[![Research-Backed](https://img.shields.io/badge/Research--Backed-33k%2B%20PRs%20Studied-brightgreen)](docs/RESEARCH.md)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![5 Agents](https://img.shields.io/badge/Agents-5%20Specialists-orange)](#-multi-agent-architecture)

[Installation](#-installation--5-minutes) · [Features](#-features-14-research-backed-capabilities) · [Architecture](#-multi-agent-architecture) · [Research](#-built-on-science-not-opinions) · [Configuration](#-configuration)

Created by **[Krypto Whitehat](https://x.com/Krypto_Whitehat)**

</div>

---

## Why WHITEHAT-INTENT?

AI coding agents generate code fast. But speed without coordination produces **pull requests that get rejected**.

Researchers analyzed **33,596 agent-authored PRs** across GitHub. The result:

| #1 Failure | #2 Failure | #3 Failure | #4 Failure |
|---|---|---|---|
| **Reviewer abandonment** | **Duplicate PRs** | **CI failures** | **Scope creep** |
| 38% | 23% | 17% | 4% |

*Source: Ehsani et al., MSR '26 — [arxiv.org/abs/2601.15195](https://arxiv.org/abs/2601.15195)*

**WHITEHAT-INTENT is the only OpenCode agent system built to prevent every single one of these failures.**

Each guardrail is derived from empirical data — not opinions. Each feature maps to a specific finding from peer-reviewed research.

---

## Features (14 Research-Backed Capabilities)

### Spec-Driven Development Core

<details>
<summary><b>1. Living Specs — The Source of Truth</b></summary>

The spec is the **primary artifact**. Code is generated downstream. After every implementation wave, the spec auto-updates to reflect what was **actually built** — not what was planned.

- Spec drift detection: planned vs. actual outcomes are compared automatically
- Spec-as-source philosophy: you edit the spec, agents edit the code
- Bidirectional spec-to-code traceability ensures nothing falls through the cracks

*Based on: Intent Manifesto — "The spec becomes the coordination layer"*

</details>

<details>
<summary><b>2. Problem-Size Detection — Right-Sized Workflow</b></summary>

One workflow doesn't fit all. WHITEHAT-INTENT classifies every request automatically and scales ceremony accordingly:

| Size | Criteria | Workflow |
|---|---|---|
| **MICRO** | <3 files, <50 LOC | Inline spec, single wave, no ceremony overhead |
| **MEDIUM** | 3-8 files, 50-300 LOC | Focused spec with acceptance criteria, 1-3 waves |
| **MACRO** | >8 files, >300 LOC | Full spec-driven workflow, multi-wave planning, integration checkpoints |

Never over-specify a small bug. Never under-specify a large feature.

*Based on: Böckeler (Thoughtworks) — "Tools using one workflow for all sizes fail"*

</details>

### Coordination & Planning

<details>
<summary><b>3. Duplicate Work Prevention</b></summary>

Before any task starts, WHITEHAT-INTENT scans:
- Git log (last 30 days) for related changes
- Open branches for overlapping work
- Existing issues and PRs

If overlap is found, the agent **flags it immediately** instead of silently creating duplicate work.

*Based on: Ehsani et al. — 23% of agent PR rejections are duplicates*

</details>

<details>
<summary><b>4. Intelligent Task Decomposition</b></summary>

The Coordinator breaks work into tasks that actually get merged:

- **Max 5 files per task** — maintainers reject large-scope PRs
- **Max 200 LOC per task** — larger changes have 17% lower merge rate
- **Single responsibility per task** — "small, focused, limited to single coherent change"
- **Dependency graph** with parallelizable task identification
- **Integration checkpoints** between dependent waves

*Based on: Ehsani et al. — "Maintainers prefer small, focused changes"*

</details>

<details>
<summary><b>5. Integration Risk Mapping</b></summary>

Before execution begins, the system maps:
- Cross-wave file dependencies (merge conflict prediction)
- Files with high change frequency (hotspot detection)
- API contract changes (breaking change risk)
- Shared module boundaries (interface conflict risk)

Waves are ordered to minimize merge complexity.

*Based on: Mitchinson — "Clear boundaries prevent agent coordination failures"*

</details>

### Quality Enforcement

<details>
<summary><b>6. Hard Pre-Edit Gate — Context7 Stack Guidance</b></summary>

**No edit is allowed until professional guidance is captured.** Before every implementation wave:

1. Build a stack map from touched files (language, framework, CMS, runtime)
2. Query Context7 for stack-specific best practices
3. Record distilled guidance into the spec wave notes
4. Apply guidance to all edits

Special handling for: WordPress plugins (hooks, nonce/capability checks), HTML5 (semantics, ARIA, SEO renderability), JavaScript/CSS frameworks (correctness, performance, security).

If Context7 is unavailable, execution **stops**. No guessing.

</details>

<details>
<summary><b>7. Hard Post-Edit Gate — Biome Lint (Every Single Edit)</b></summary>

After **every single edit operation** — not at the end, not per wave, per edit:

1. `biome check --write <touched files>`
2. `biome check <touched files>`

The next edit is **blocked** until Biome is clean. If Biome can't run, the agent stops and reports the blocker.

*Based on: Ehsani et al. — "Each additional failed CI check decreases merge odds by ~15%"*

</details>

<details>
<summary><b>8. Anti-Pattern Prevention</b></summary>

Research shows specific agent behaviors that get PRs rejected. WHITEHAT-INTENT prevents all of them:

| Anti-Pattern | Frequency in Research | Guardrail |
|---|---|---|
| Unrelated edits combined | Common in rejected PRs | Single coherent purpose per wave |
| Vague task descriptions | 7% of rejections | Clarification request before proceeding |
| Scope creep | 4% "unwanted features" | Automatic task splitting when boundary exceeded |
| Wrong branch submission | 1% of rejections | Branch target validation in Verifier |
| Large diffs | 17% effect size difference | Max 5 files / 200 LOC per wave (hard limit) |

</details>

### Verification & Traceability

<details>
<summary><b>9. Bidirectional Spec-to-Code Traceability</b></summary>

Every acceptance criterion maps to code. Every code change maps to a spec requirement. The system detects:

- **Code without spec coverage** → scope creep detected
- **Spec requirements without implementation** → incomplete work detected

Neither direction can drift without being caught.

</details>

<details>
<summary><b>10. PR Readiness Assessment</b></summary>

Before any work is marked complete, the Verifier runs a full PR readiness check:

| Check | Threshold | Source |
|---|---|---|
| Total files changed | Flag if >10 | Ehsani et al. |
| Total LOC delta | Flag if >500 | Ehsani et al. |
| CI/Biome status | Must pass | Ehsani et al. — 17% rejection |
| Branch target | Must be correct | Ehsani et al. — wrong branch pattern |
| Scope creep | Zero unrelated changes | Ehsani et al. — unwanted features |
| Duplicate overlap | Must not overlap existing PRs | Ehsani et al. — 23% duplicates |

</details>

<details>
<summary><b>11. Integration Regression Detection</b></summary>

Cross-wave verification catches what single-wave testing misses:

- End-to-end flows that span multiple waves
- Broken imports, missing exports, type mismatches
- Parallel wave outputs that conflict at integration points

</details>

### Context & Investigation

<details>
<summary><b>12. Existing Work Detection & Project Norms Mapping</b></summary>

Before any implementation, the Context agent produces:

- **Existing work scan**: recent commits, branches, issues, PRs related to the task
- **Project norms**: contribution guidelines, code style, branch naming, CI requirements
- **Architecture map**: folder structure, module boundaries, naming conventions
- **Test patterns**: framework, coverage expectations, test location conventions

*Based on: Ehsani et al. — "Agents need to identify existing work and adhere to contribution norms"*

</details>

<details>
<summary><b>13. Root-Cause Preflight for Ambiguous Requests</b></summary>

Vague bug reports are the #1 cause of incorrect implementations (3% of rejections). WHITEHAT-INTENT enforces:

1. For ANY vague or underspecified request → investigation wave fires FIRST
2. WHITEHAT-CONTEXT investigates: symptoms → suspect files → Read evidence → confidence level
3. WHITEHAT-VERIFIER cross-checks the investigation
4. Evidence is written into the spec BEFORE any code edit

**No guessing from user wording alone.**

</details>

<details>
<summary><b>14. Spec Quality Control</b></summary>

Verbose specs create "review overload" — agents and humans stop reading carefully. WHITEHAT-INTENT enforces:

- **Max 200 lines** per spec — trimmed if exceeded
- **GIVEN/WHEN/THEN** acceptance criteria format — testable and measurable
- **Functional intent separated** from technical implementation details
- **Every criterion** maps to verifiable code behavior

*Based on: Böckeler — "Reviewing markdown is worse than reviewing code when specs are verbose"*

</details>

---

## Multi-Agent Architecture

Five specialized agents, one coordinated workflow.

```
                         ┌─────────────────────────┐
                         │    WHITEHAT-INTENT       │
                         │  ◆ Spec-Driven Orchestrator  │
                         │  Problem-size detection │
                         │  Duplicate prevention   │
                         │  Anti-pattern guardrails │
                         └────────────┬────────────┘
                                      │
                   ┌──────────────────┼──────────────────┐
                   │                  │                  │
         ┌─────────▼────────┐ ┌──────▼────────┐ ┌───────▼──────────┐
         │ WHITEHAT-CONTEXT  │ │  COORDINATOR  │ │ WHITEHAT-VERIFIER│
         │ ◆ Investigation  │ │ ◆ Planning    │ │ ◆ Quality Gate   │
         │                  │ │               │ │                  │
         │ • Duplicate scan │ │ • Task decom- │ │ • PR readiness   │
         │ • Project norms  │ │   position    │ │ • Spec ↔ Code    │
         │ • Integration    │ │ • Spec quality│ │   traceability   │
         │   risk mapping   │ │ • Dependency  │ │ • Integration    │
         │ • Root-cause     │ │   graph       │ │   regression     │
         │   triage         │ │ • Wave order  │ │ • Severity report│
         └──────────────────┘ └───────┬───────┘ └──────────────────┘
                                     │
                           ┌─────────▼──────────┐
                           │ WHITEHAT-          │
                           │ IMPLEMENTOR        │
                           │ ◆ Execution Engine  │
                           │                    │
                           │ • Atomic commits   │
                           │ • Scope boundaries │
                           │ • Context7 gate    │
                           │ • Biome gate       │
                           │ • Wave logging     │
                           └────────────────────┘
```

| Agent | Mode | Specialization |
|---|---|---|
| **WHITEHAT-INTENT** | `primary` | Orchestrator — classifies, coordinates, prevents anti-patterns |
| **WHITEHAT-CONTEXT** | `subagent` | Investigation — duplicate detection, norms mapping, risk assessment |
| **WHITEHAT-COORDINATOR** | `subagent` | Planning — task decomposition, spec quality, integration planning |
| **WHITEHAT-IMPLEMENTOR** | `subagent` | Execution — atomic changes, scope boundaries, quality gates |
| **WHITEHAT-VERIFIER** | `subagent` | Quality — PR readiness, traceability, integration regression |

---

## How It Works

### The Execution Loop

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  PLAN    │───>│ CONTEXT  │───>│ EXECUTE  │───>│  VERIFY  │───>│  UPDATE  │
│          │    │          │    │          │    │          │    │          │
│ Classify │    │ Scan for │    │ Atomic   │    │ PR ready?│    │ Spec     │
│ size     │    │ dupes    │    │ edits    │    │ Trace    │    │ reflects │
│ Delegate │    │ Map norms│    │ Context7 │    │ code     │    │ reality  │
│ plan     │    │ Map risks│    │ + Biome  │    │ Regression│   │          │
└──────────┘    └──────────┘    └──────────┘    └──────────┘    └──────────┘
     │                                                                              │
     └──────────────────── Loop until all acceptance criteria met ──────────────────┘
```

### Example Session

```
You: "Add a dark mode toggle to the settings page"

WHITEHAT-INTENT:
  [1/7] Problem-size detection → MEDIUM (estimated 4 files, ~120 LOC)
  [2/7] Duplicate check → No overlapping branches or PRs found
  [3/7] Living spec → Updated with acceptance criteria (GIVEN/WHEN/THEN)
  [4/7] Context7 → Retrieved CSS custom properties + React state management guidance
  [5/7] Coordinator → Decomposed into 2 tasks with dependency graph
  [6/7] Implementor → Wave 1 complete (theme context + toggle component)
        → Wave 2 complete (CSS variables + persistence)
        → Biome clean on all 4 files ✓
  [7/7] Verifier → All 3 acceptance criteria met ✓
        → Spec-to-code traceability: 100% coverage ✓
        → PR readiness: PASS (4 files, 118 LOC, correct branch)
  → Living spec updated to reflect actual implementation
```

---

## Built on Science, Not Opinions

Every feature maps to a specific finding from peer-reviewed research:

| Research | Scale | Key Finding | WHITEHAT-INTENT Feature |
|---|---|---|---|
| [Ehsani et al., MSR '26](https://arxiv.org/abs/2601.15195) | **33,596 PRs**, 5 agents | 23% of agent PRs are duplicates | Duplicate work prevention |
| Same | Same | Larger changes = 17% lower merge rate | Max 5 files / 200 LOC per wave |
| Same | Same | Each CI failure = 15% lower merge odds | Biome hard post-edit gate |
| Same | Same | 38% of PRs fail from reviewer abandonment | Living spec as context provider |
| Same | Same | Vague descriptions cause misalignment | Root-cause preflight |
| [Böckeler, Thoughtworks](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) | 3 SDD tools analyzed | One workflow doesn't fit all sizes | MICRO/MEDIUM/MACRO detection |
| Same | Same | Verbose specs create review overload | 200-line spec limit |
| Same | Same | Iterative beats big-upfront design | Wave-based execution |
| [Mitchinson](https://www.nrmitchi.com/2025/10/using-git-worktrees-for-multi-feature-development-with-ai-agents/) | Multi-agent patterns | Clear boundaries prevent coordination failures | Scope boundary enforcement |
| [Intent Manifesto](https://intent.dev) | SDD philosophy | "The plan becomes the product" | Spec-as-source architecture |

See [`docs/RESEARCH.md`](docs/RESEARCH.md) for the full analysis.

---

## Installation (5 Minutes)

### Prerequisites

| Tool | Purpose | Install |
|---|---|---|
| [OpenCode](https://opencode.ai) | Agent runtime | `go install github.com/opencode-ai/opencode@latest` |
| [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode) | Plugin system | See their README |
| [Context7 MCP](https://github.com/upstash/context7-mcp) | Stack guidance | Configured via MCP |
| [Biome](https://biomejs.dev/) | Linting | `npm install -g @biomejs/biome` |

### Quick Install

```bash
# 1. Clone the repo
git clone https://github.com/emco1234/WHITEHAT-INTENT.git /tmp/whitehat-intent

# 2. Back up your existing config
cp ~/.config/opencode/opencode.json ~/.config/opencode/opencode.json.backup 2>/dev/null
cp ~/.config/opencode/oh-my-opencode.json ~/.config/opencode/oh-my-opencode.json.backup 2>/dev/null

# 3. Install the living spec template
mkdir -p ~/.intent/specs
cp /tmp/whitehat-intent/intent-specs/template.md ~/.intent/specs/template.md

# 4. Restart OpenCode
opencode
```

### Merge Into Your Config

**Step 1** — Add agents to `~/.config/opencode/opencode.json`:

Copy the 5 agent entries from [`config/opencode/agents.json`](config/opencode/agents.json) into your `"agent"` section. Replace `"CHANGE_ME_TO_YOUR_MODEL"` with your model.

**Step 2** — Add categories to `~/.config/opencode/oh-my-opencode.json`:

Copy the 4 category entries from [`config/oh-my-opencode/categories.json`](config/oh-my-opencode/categories.json) into your `"categories"` section.

**Step 3** — Set as default agent:

```json
{
  "default_agent": "WHITEHAT-INTENT"
}
```

**Step 4** — Add Context7 MCP (required):

```json
{
  "mcp": {
    "context7": {
      "type": "local",
      "command": ["npx", "-y", "@upstash/context7-mcp", "--transport", "stdio"],
      "enabled": true,
      "timeout": 20000
    }
  }
}
```

**Step 5** — (Optional) Add browser verification MCP for frontend work:

```json
{
  "chrome-devtools": {
    "type": "local",
    "command": ["npx", "-y", "chrome-devtools-mcp@latest"],
    "enabled": true,
    "timeout": 10000
  }
}
```

Done. Restart OpenCode.

---

## Configuration

### Works With Any Model

WHITEHAT-INTENT is model-agnostic. Use any OpenCode-compatible provider:

```json
{
  "WHITEHAT-INTENT": {
    "model": "anthropic/claude-sonnet-4-5",
    ...
  }
}
```

### Tunable Thresholds

| Setting | Default | Where |
|---|---|---|
| Max files per wave | 5 | Orchestrator §4 |
| Max LOC per wave | 200 | Orchestrator §4 |
| Max files per PR (warning) | 10 | Verifier §1 |
| Max LOC per PR (warning) | 500 | Verifier §1 |
| Spec max lines | 200 | Coordinator §2 |
| Duplicate scan depth | 30 days | Context prompt |
| Context7 timeout | 20000ms | MCP config |

### Custom Constraints

Add project-specific rules to your spec template at `.intent/specs/template.md` under the `Constraints` section.

---

## File Structure

```
WHITEHAT-INTENT/
├── README.md                              ← You are here
├── LICENSE                                ← MIT
├── INSTALL.md                             ← Quick-install reference
│
├── config/
│   ├── opencode/
│   │   └── agents.json                    ← 5 agent definitions (merge into opencode.json)
│   └── oh-my-opencode/
│       └── categories.json                ← 4 category definitions (merge into oh-my-opencode.json)
│
├── intent-specs/
│   ├── template.md                        ← Living spec template
│   └── current.md                         ← Working example spec
│
└── docs/
    └── RESEARCH.md                        ← Full research analysis with data tables
```

---

## Troubleshooting

| Problem | Solution |
|---|---|
| Agent doesn't appear | Close OpenCode fully, edit config, restart |
| JSON parse error | Validate: `node -e "JSON.parse(require('fs').readFileSync('~/.config/opencode/opencode.json','utf8'))"` |
| Context7 not connecting | Run `opencode mcp list` and verify npx is in PATH |
| Biome not found | `npm install -g @biomejs/biome` |
| Spec not found | `mkdir -p .intent/specs && cp intent-specs/template.md .intent/specs/template.md` |

---

## Comparison

| Feature | WHITEHAT-INTENT | Standard OpenCode | Cursor Rules | .cursorrules |
|---|---|---|---|---|
| Living spec as source of truth | **Spec-as-source** | No spec system | File-based rules | File-based rules |
| Problem-size detection | **MICRO/MEDIUM/MACRO** | One-size-fits-all | No | No |
| Duplicate work prevention | **Automatic** | No | No | No |
| Change size enforcement | **Hard limits** | No | Soft | No |
| Pre-edit Context7 gate | **Hard block** | No | No | No |
| Post-edit lint gate | **Per-edit** | No | Manual | Manual |
| Spec-to-code traceability | **Bidirectional** | No | No | No |
| PR readiness assessment | **Automated** | No | No | No |
| Multi-agent coordination | **5 agents** | Single agent | Single agent | N/A |
| Research-backed | **33k+ PRs** | No | No | No |
| Integration regression | **Cross-wave** | No | No | No |

---

## License

[MIT](LICENSE) — Free to use, modify, and distribute.

---

<div align="center">

**Created by** [Krypto Whitehat](https://x.com/Krypto_Whitehat)

Built on [OpenCode](https://opencode.ai) + [oh-my-opencode](https://github.com/code-yeongyu/oh-my-opencode)

Research-backed: [Ehsani et al.](https://arxiv.org/abs/2601.15195) · [Böckeler](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) · [Mitchinson](https://www.nrmitchi.com/2025/10/using-git-worktrees-for-multi-feature-development-with-ai-agents/) · [Intent](https://intent.dev)

</div>
