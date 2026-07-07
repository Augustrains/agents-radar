# AI CLI Tools Community Digest 2026-07-07

> Generated: 2026-07-07 01:50 UTC | Tools covered: 9

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## Cross-Tool Comparison

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date:** 2026-07-07

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem continues its rapid maturation, with six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—all receiving active community engagement on July 7, 2026. The landscape reveals a bifurcation: established tools (Claude Code, Codex, Copilot CLI) are dealing with complex enterprise-scale issues around multi-tenancy, authentication state management, and safety filter reliability, while emerging tools (Pi, Qwen Code, DeepSeek TUI) focus on foundational architecture, cross-platform compatibility, and provider-agnostic design. A unifying theme across all tools is the community's demand for better observability into agentic workflows, multi-agent orchestration reliability, and robust session lifecycle management.

---

## 2. Activity Comparison

| Tool | New Issues (24h) | New PRs (24h) | Release Today | Notable Activity |
|------|-----------------|---------------|---------------|------------------|
| **Claude Code** | ~12 (incl. 7 dupes) | 0 active | v2.1.202 | 7 cybersecurity false positives; nested subagent bugs |
| **OpenAI Codex** | ~6 | 10 active | rust-v0.143.0-alpha.37 | Reasoning-token clustering (#30364, 131 comments); context compaction bug |
| **Gemini CLI** | ~5 | 10 active | None | Subagent recovery misreporting; generalist agent hang |
| **GitHub Copilot CLI** | ~4 | 0 active | v1.0.69-2 | Voice mode ASR failures; MCP protocol edge cases |
| **Kimi Code CLI** | 2 | 0 active | None | Terminal distortion; ACP usage limits |
| **OpenCode** | ~6 | 10+ active | v1.17.14 | V2 event schema redesign; Windows ARM64 issues |
| **Pi** | ~8 | 10 active | None | Cache token double-count (fixed); extension hooks expansion |
| **Qwen Code** | ~10 | 10+ active | v0.19.6-nightly | Zombie session token drain (#5964); multi-workspace RFC |
| **DeepSeek TUI** | ~20+ | 4 active (1 merged) | None (v0.8.67 in QA) | SIGPIPE crash; sub-agent success masking |

**Key Observations:**
- **Claude Code** and **OpenCode** had the most visible releases with meaningful feature additions
- **DeepSeek TUI** had the highest issue creation volume (20+), driven by structured release-management review process
- **Qwen Code** and **Pi** show strong PR throughput with 10+ active PRs each
- **Kimi Code** and **Gemini CLI** had no releases today, though Gemini maintainers are actively retesting P1 bugs

---

## 3. Shared Feature Directions

### Multi-Account / Multi-Workspace Management
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | #18435: Multi-account profile switching (125 comments, 635 👍) |
| **Qwen Code** | #6378: RFC for multi-workspace daemon (19 comments) |
| **GitHub Copilot CLI** | #1665: Per-project plugin scoping (18 👍) |
| **OpenCode** | Multiple session management issues (#29175, #30926) |

### Multi-Agent Orchestration Reliability
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | #75043: Nested subagent ownership bugs; #68147: Model override dropped |
| **Gemini CLI** | #22323: Subagent success masking; #21409: Generalist agent hang |
| **DeepSeek TUI** | #4050: Empty child success reports; #4049: Delegate routing failure |
| **Pi** | #6363: Agent idle event for extension integration |

### Real-Time Output / Streaming in TUI
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | #14280: Real-time bash output in VS Code (66 👍) |
| **Kimi Code** | #2453: Streaming responses in ACP |
| **OpenCode** | General streaming improvements in V2 schema work |

### Safety Filter / Security False Positives
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | 7+ issues today (#75062-75069): `ls` and `git status` blocked by Opus 4.8 |
| **Pi** | #6341: Constrained sampling for deterministic tool calls |
| **Qwen Code** | #6377: Block self-kill commands |

### Local / Offline Model Support
| Tool | Specific Need |
|------|---------------|
| **OpenCode** | #19948: Ollama integration (22 comments) |
| **GitHub Copilot CLI** | #4003: Custom model endpoints |
| **Pi** | #6305: LAN auto-discovery of local models |

### Cross-Platform Parity (Windows / Linux)
| Tool | Specific Need |
|------|---------------|
| **Claude Code** | #48407: Cowork tab missing on Windows (38 comments) |
| **OpenCode** | #19130: Windows ARM64 TUI failure |
| **Kimi Code** | #2485: Terminal distortion on Windows 11 |
| **Qwen Code** | #6214: Garbled shell output on Windows |
| **Pi** | #6250: Ctrl+V image paste fails on Linux/X11 |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|-----------|----------|-----|-----------|---------------|
| **Primary User Base** | Full-stack devs, enterprises | Pro/Enterprise devs | ML/AI researchers | GitHub ecosystem | ACP integration devs | Plugin/extension devs | Agent workflow devs | Multi-model orchestration | TUI-first power users |
| **Differentiator** | Dynamic workflow sizing; hooks system | Reasoning token optimization; proxy routing | AST-aware tooling; bash affinity | GitHub native; rubber-duck | ACP protocol; lightweight | V2 event schema; Code Mode MCP | Extension hooks; provider agnostic | Multi-workspace daemon; nightly releases | Constitution customization; fleet/workflow |
| **Platform Maturity** | Mature (Windows gap) | Mature (macOS reliability gap) | Mid-stage | Mature (Nix gap) | Early stage | Mid-stage (V2 redesign) | Mid-stage | Mid-stage (Nightly cadence) | Early stage (v0.8.x) |
| **Community Engagement** | Very High (135 comment issues) | High (131 comment issues) | Moderate | Moderate | Low (2-5 comment avg) | High (92 comment issues) | Moderate | Moderate-High | Low (mostly maintainer) |
| **Enterprise Readiness** | Strong (auth, hooks, OTel) | Strong (enterprise auth, proxy) | Moderate | Strong (GitHub ecosystem) | Weak (early stage) | Moderate (plugin system) | Moderate | Moderate | Weak (early stage) |

### Key Differentiators

- **Claude Code** leads in **agent orchestration complexity** with its subagent model overrides, dynamic workflow sizing, and hook system—but struggles with safety filter false positives and Windows parity.
- **OpenAI Codex** is investing heavily in **enterprise infrastructure** (system proxy routing, thread lifecycle management, external auth) and **reasoning optimization** (sequential cutoff, token cluster analysis).
- **Gemini CLI** differentiates with **AST-aware tooling** and **bash affinity**, leveraging Gemini models' native POSIX training for more efficient codebase navigation.
- **GitHub Copilot CLI** leverages deep **GitHub ecosystem integration** (ACP, GitHub Actions, plugin scoping) but lags in agentic capabilities compared to Claude Code or Gemini.
- **Kimi Code** positions as a **lightweight ACP-first tool** but suffers from limited feature set and low community engagement.
- **OpenCode** is undergoing a **V2 architecture redesign** focused on event schemas, AGENTS.md routing, and code mode—suggesting a pivot toward more structured agent workflows.
- **Pi** excels in **extension system design** with hooks for provider headers, tool result limiting, and agent events—making it attractive for developers building custom agent integrations.
- **Qwen Code** leads in **daemon architecture** (multi-workspace, scheduled tasks, session panels) and **automated release processes** (nightly builds, triage bots).
- **DeepSeek TUI** is the most **TUI-centric** tool, with deep focus on terminal UX, keyboard navigation, and constitution customization—but shows structural immaturity in release management.

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
| Tool | Evidence | Assessment |
|------|----------|------------|
| **Qwen Code** | 50 PRs updated in 24h; nightly releases; structured RFC process for multi-workspace | **Most rapidly iterating**—shipping multiple features and fixes daily with formal governance |
| **OpenCode** | V2 event schema redesign underway; 10+ active PRs; Discord "gang grill" sessions driving architecture | **Strong architectural momentum**—community deeply engaged in design decisions |
| **Pi** | 10 merged PRs today; new hooks (before_provider_headers, agent_idle); constrained sampling | **Healthy, steady iteration**—extension ecosystem growing with active community contributions (mitsuhiko) |
| **Claude Code** | New release (v2.1.202) with dynamic sizing; high engagement on long-running issues | **Established but not accelerating**—stability focus over feature velocity |

### Moderate Momentum
| Tool | Evidence | Assessment |
|------|----------|------------|
| **OpenAI Codex** | 10 active PRs; focus on enterprise infra (proxy, auth, thread lifecycle) | **Steady enterprise-focused iteration**—less community feature churn, more infrastructure hardening |
| **Gemini CLI** | Maintainers actively retesting P1 bugs; 10 active PRs | **Reliability-focused iteration**—addressing sub-agent reliability before new features |
| **DeepSeek TUI** | 20+ issues created from review prompt; PRs for SIGPIPE, UTF-8 fix | **Bursts of structured activity**—release cycles driven by maintainer's review process |

### Lower Momentum
| Tool | Evidence | Assessment |
|------|----------|------------|
| **GitHub Copilot CLI** | Patch release only (v1.0.69-2); no new PRs | **Mature, stable**—incremental improvements; not driving agentic innovation |
| **Kimi Code CLI** | 2 new issues; no releases or PRs | **Minimal activity**—suggests limited development resources or community engagement |

### Community Health Indicators
- **Most active community conversation**: Claude Code (#73125: 135 comments, #18435: 125 comments) and OpenAI Codex (#30364: 131 comments)
- **Most upvoted open feature**: OpenCode #8501 ("Expand pasted text") with 202 👍
- **Most controversial topic**: Qwen Code #3203 (OAuth free tier reduction: 149 comments, mixed sentiment)
- **Best community-contributor engagement**: Pi (mitsuhiko contributing constrained sampling, malformed tool handling, config improvements)

---

## 6. Trend Signals

### 1. Agentic Workflow Reliability is the Top Unmet Need
Across all tools, the most consistent pain point is **sub-agent orchestration reliability**. Claude Code, Gemini CLI, and DeepSeek TUI all report issues with subagents incorrectly reporting success, hanging indefinitely, or losing configuration during delegation. This is the single biggest barrier to production adoption of multi-agent workflows.

### 2. Safety Filters Are Becoming a Cost Center
Claude Code's cluster of 7+ cybersecurity false positives today (blocking `ls`, `git status`, directory checks) signals that aggressive safety filters are causing significant productivity loss. The same dynamic appears in Codex's malware alert issues (#24246). Tools need **configurable, context-aware safety policies** rather than blanket blocking.

### 3. Session Lifecycle Management is Immature
Across the board—**zombie sessions** (Qwen Code #5964: 30M tokens wasted), **context compaction ruining sessions** (Codex #31033), **stale thread responses** (Codex #8648), **ghost conversations** (Codex #29868)—the industry lacks robust session management. Session persistence, recovery, and clean termination are foundational gaps.

### 4. Multi-Model / Provider-Agnostic Architecture is Becoming Table Stakes
Pi, Qwen Code, and DeepSeek TUI all emphasize provider-agnostic design. Qwen Code's multi-workspace daemon (#6378) and Pi's registration of Requesty as native provider (#5472) signal that tools that lock users into a single model/provider ecosystem are at a competitive disadvantage.

### 5. Windows Parity Remains an Unsolved Problem
Every major tool has unresolved Windows-specific bugs: Claude Code's missing Cowork tab (#48407, 38 comments), Kimi Code's terminal distortion (#2485), OpenCode's ARM64 TUI failure (#19130), Qwen Code's shell encoding (#6214), Pi's clipboard regression (#6250). **Windows remains a second-class platform** despite growing enterprise adoption.

### 6. Extension/Plugin Ecosystems Are the Next Battleground
Pi's hook system (before_provider_headers, agent_idle, tool result limiter), OpenCode's plugin shortcircuit and Code Mode API, and Copilot CLI's plugin scoping (#1665) all point to **extensibility as a competitive differentiator**. Tools that enable third-party integration will attract power users and enterprise teams with custom workflows.

### 7. TUI Quality is Being Traded for Feature Velocity
DeepSeek TUI's unscrollable setup wizard (#4063), Kimi Code's terminal distortion (#2485), and multiple tools' garbled output on non-UTF-8 terminals suggest that **basic TUI ergonomics are being neglected** in favor of agentic features. This creates friction for new users and limits adoption among traditional terminal-first developers.

### 8. Cost Transparency is Urgently Needed
Multiple tools face token accounting bugs (Pi's double-counting cache tokens, #6352; Qwen Code's zombie sessions burning 30M tokens, #5964; Codex's reasoning-token quantization, #30364). Users are demanding **real-time, accurate cost telemetry** to make informed decisions about model selection and workflow design.

### Recommendation for Decision-Makers
- **For production deployment of agentic workflows**: Claude Code offers the most mature subagent system, but beware safety filter false positives and test extensively on Windows.
- **For enterprise integration**: OpenAI Codex's proxy routing, thread lifecycle, and external auth make it strong for managed environments.
- **For multi-model flexibility**: Pi and Qwen Code offer the most provider-agnostic architectures, with Pi leading in extension ecosystem maturity.
- **For GitHub-native workflows**: Copilot CLI is reliable but lagging in agentic capabilities—use it for simple automation, not complex multi-agent tasks.
- **For TUI-centric power users**: DeepSeek TUI has the most deliberate terminal UX focus but is early-stage and structurally fragile.

**The key industry inflection point**: The shift from single-agent assistants to multi-agent orchestration systems will be the defining architectural challenge of 2026-2027, and the tools that solve sub-agent reliability, session lifecycle management, and cross-platform parity will dominate enterprise adoption.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data.

---

## Claude Code Skills Community Highlights Report (Data: 2026-07-07)

### 1. Top Skills Ranking

The following Skill submissions have generated the most community discussion and attention:

1.  **fix(skill-creator): run_eval.py always reports 0% recall** [#1298](https://github.com/anthropics/skills/pull/1298)
    - **Functionality:** Fixes a critical bug in the skill-creator toolchain where the evaluation script (`run_eval.py`) always reports 0% recall, rendering the description-optimization loop useless.
    - **Discussion:** High-urgency fix targeting a core developer workflow. Addresses issues #556 and #1169 with 10+ independent reproductions. **Status:** Open (since 2026-06-10).

2.  **fix(skill-creator): run_eval trigger detection misses real skill name** [#1323](https://github.com/anthropics/skills/pull/1323)
    - **Functionality:** Another critical fix for the `run_eval.py` script, addressing a different root cause where trigger detection fails to match the actual skill name, causing 0% recall.
    - **Discussion:** Closely related to #1298, indicating a deep-set stability issue in the skill creation pipeline. **Status:** Open (since 2026-06-16).

3.  **Add document-typography skill** [#514](https://github.com/anthropics/skills/pull/514)
    - **Functionality:** Prevents common typographic problems in AI-generated documents (orphan words, widow paragraphs, numbering misalignment).
    - **Discussion:** Addresses a universal pain point for document generation. The skill is seen as a high-value quality-of-life improvement. **Status:** Open (since 2026-03-04).

4.  **feat: add testing-patterns skill** [#723](https://github.com/anthropics/skills/pull/723)
    - **Functionality:** A comprehensive skill covering the full testing stack, including unit testing (AAA pattern), React component testing, and testing philosophy (Testing Trophy model).
    - **Discussion:** High demand for structured guidance on software quality. The skill is ambitious in scope. **Status:** Open (since 2026-03-22).

5.  **fix(pdf): correct case-sensitive file references in SKILL.md** [#538](https://github.com/anthropics/skills/pull/538)
    - **Functionality:** Fixes 8 case-sensitivity mismatches in the PDF skill's documentation, which breaks on case-sensitive file systems.
    - **Discussion:** A simple but essential bug fix that prevents a core document skill from working correctly on Linux/macOS. **Status:** Open (since 2026-03-06).

6.  **feat(skills): add self-audit** [#1367](https://github.com/anthropics/skills/pull/1367)
    - **Functionality:** A meta-skill that audits AI output before delivery, combining mechanical file verification with a four-dimension reasoning quality gate.
    - **Discussion:** Novel concept for quality assurance; a "skill about skills." **Status:** Open (since 2026-06-28).

### 2. Community Demand Trends

The Issues reveal several key directions for new Skill development:

- **Security & Trust Boundaries:** Issue #492 (34 comments) highlights a major concern about community skills being distributed under the `anthropic/` namespace, creating a trust abuse vector. There is strong demand for official namespace governance and skill vetting.
- **Org-Wide Sharing:** Issue #228 (14 comments) requests enterprise-grade skill distribution, moving away from manual file sharing to a shared library or direct sharing link.
- **Skill-Creator Stability:** Issues #556, #1061, and #1169 (cumulative ~18 comments) all focus on the `skill-creator` toolchain being broken on Windows and producing unreliable evaluation results. The community's most critical technical demand is for a stable, cross-platform skill development pipeline.
- **Agent Governance & Safety:** Issue #412 proposes an "agent-governance" skill for safety patterns in agent systems, indicating a growing interest in production-grade agent behavior management.
- **Windows Compatibility:** Issue #1061 explicitly calls out the lack of Windows support for core scripts, a key blocker for a significant portion of the developer base.

### 3. High-Potential Pending Skills

These PRs have active commentary and are likely to land soon:

- **fix(skill-creator): run_eval.py crash on Windows** [#1099](https://github.com/anthropics/skills/pull/1099) & **fix: Windows subprocess + encoding bugs** [#1050](https://github.com/anthropics/skills/pull/1050): Both address the critical Windows compatibility blocker for the skill creator. Essential for a healthy cross-platform ecosystem.
- **fix(skill-creator): warn on unquoted description with YAML special characters** [#539](https://github.com/anthropics/skills/pull/539): A defense-in-depth PR to prevent silent YAML parsing failures. Directly addresses a common authoring error.
- **Add ODT skill** [#486](https://github.com/anthropics/skills/pull/486): Expands document support to the open-source ODT format, a significant gap for organizations using LibreOffice.
- **Add sensory skill — native macOS automation** [#806](https://github.com/anthropics/skills/pull/806): Introduces AppleScript-based automation, offering a native alternative to screenshot-based computer use on macOS.

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **a reliable, cross-platform skill creation and evaluation toolchain**, as evidenced by the volume of open PRs and Issues dedicated to fixing the core `run_eval.py` script and its Windows compatibility.

---

# Claude Code Community Digest — 2026-07-07

## Today's Highlights

A new release (v2.1.202) introduces configurable dynamic workflow sizing, while the community remains focused on two long-running threads: the `AskUserQuestion` timeout bug (Issue #73125, 135 comments) and the multi-account management feature request (Issue #18435, 125 comments). A concerning cluster of cybersecurity safety-filter false positives has also appeared today, with multiple users reporting routine project inspection commands being blocked by Opus 4.8.

---

## Releases

### v2.1.202 — Dynamic Workflow Sizing
[View Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.202)

- **New `/config` setting:** "Dynamic workflow size" — an advisory guideline controlling how large Claude makes dynamic workflows (small/medium/large agent counts). Not an enforced cap.
- **Telemetry addition:** `workflow.run_id` and `workflow.name` OpenTelemetry attributes added to telemetry payloads for better observability.

---

## Hot Issues (10 Noteworthy)

### 🔥 #73125 — `AskUserQuestion`: No response after 60s — continued without an answer
[Issue](https://github.com/anthropics/claude-code/issues/73125) | **135 comments** | 👍 372 | **CLOSED**
The most active bug this week. When Claude asks the user a question and receives no response for 60 seconds, it silently continues without the answer. Affects Bedrock API, Linux, TUI, tools, and VS Code environments. Community reaction confirms this is a significant workflow disruptor.

### 🔥 #18435 — Multi-account management in Claude Desktop
[Issue](https://github.com/anthropics/claude-code/issues/18435) | **125 comments** | 👍 635 | **OPEN**
The highest-reacted open issue. Users want the ability to manage multiple Claude accounts within the Desktop app with easy profile switching. Long-running (since January 2026) but no movement from Anthropic yet.

### 🚨 #48407 — Cowork tab missing in Windows 11 desktop app
[Issue](https://github.com/anthropics/claude-code/issues/48407) | **38 comments** | 👍 16 | **OPEN**
Persistent Windows-specific bug where the Cowork tab fails to appear despite Hyper-V being enabled. Affects app version v1.2581.0. No resolution in sight.

### 🚨 #62503 — Appeal form redirect loop after account restriction
[Issue](https://github.com/anthropics/claude-code/issues/62503) | **31 comments** | 👍 5 | **OPEN**
MacOS users hit a redirect loop when trying to appeal account restrictions. Auth-related and external dependency — likely a server-side issue.

### 📊 #44243 — Multiple Slack workspaces in built-in connector
[Issue](https://github.com/anthropics/claude-code/issues/44243) | **30 comments** | 👍 64 | **OPEN**
The built-in Slack MCP connector only supports one workspace per account. Consultants and multi-org users are blocked from using it for cross-workspace workflows.

### 📊 #14280 — VS Code extension: Stream bash command output in real-time
[Issue](https://github.com/anthropics/claude-code/issues/14280) | **20 comments** | 👍 66 | **OPEN**
Users want real-time streaming of bash command output from Claude in VS Code, rather than waiting for batch results. A long-standing UX gap since December 2025.

### 📊 #75062-75069 — Cybersecurity false positive cluster (7 issues)
[#75062](https://github.com/anthropics/claude-code/issues/75062), [#75065](https://github.com/anthropics/claude-code/issues/75065), [#75060](https://github.com/anthropics/claude-code/issues/75060), [#75057](https://github.com/anthropics/claude-code/issues/75057), [#75058](https://github.com/anthropics/claude-code/issues/75058), [#75068](https://github.com/anthropics/claude-code/issues/75068), [#75069](https://github.com/anthropics/claude-code/issues/75069)
All filed today by `sworrl`. Opus 4.8's safety filter is blocking routine operations: `ls`-like directory checks, `git status`, project status reviews — all halt sessions. All marked duplicate, suggesting Anthropic is aware and merging. Marked severity: **session-halted** (blocks authorized work).

### 🐛 #75043 — Nested subagent ownership bugs
[Issue](https://github.com/anthropics/claude-code/issues/75043) | **3 comments** | **OPEN**
A deep agentic workflow bug: children spawned by a subagent are always async regardless of `run_in_background`, completion notifications never reach the subagent parent, and `TaskStop` fails with ownership errors after resume. Critical for complex multi-agent orchestration.

### 🐛 #68147 — Subagent model override silently dropped after continuation
[Issue](https://github.com/anthropics/claude-code/issues/68147) | **2 comments** | 👍 3 | **OPEN**
When a subagent is given an explicit `model` parameter (e.g., `model: "sonnet"`), it applies only to the first leg. After a continuation boundary, the model override is silently dropped — meaning expensive models may run longer than intended. Cost impact.

### 🐛 #75071 — One schema-invalid hook matcher disables ALL hooks silently
[Issue](https://github.com/anthropics/claude-code/issues/75071) | **0 comments** | **OPEN**
A single invalid hook matcher in `settings.json` silently disables all hooks (every event type) with no warning. Caused a 30-hour troubleshooting session. Also: `PostToolUse` never fires for MCP tools. A regression and a serious debugging UX issue.

---

## Key PR Progress (3 Active)

### #41453 — Safe Stop hook wrapper with PID lock and timeout
[PR](https://github.com/anthropics/claude-code/pull/41453) | **OPEN** (since March 2026)
Adds a reference implementation for running post-session background tasks from a Stop hook without runaway processes. Solves the architectural problem that Stop hooks must return JSON immediately but users need async post-session work. Still open after 3 months — community waiting for merge.

### #74857 — Clarify plugin MCP configuration scope
[PR](https://github.com/anthropics/claude-code/pull/74857) | **CLOSED** (merged)
Documentation fix clarifying that plugin `mcpServers` configuration is for plugin-bundled MCP servers, separate from user-level MCP allow/deny lists in `~/.claude.json`. Reduces confusion between plugin MCP config and global settings.

### #74722 — Conventional Branch naming in /commit-push-pr
[PR](https://github.com/anthropics/claude-code/pull/74722) | **OPEN**
Adds optional `conventional` argument to `/commit-push-pr` that names branches per Conventional Branch 1.0.0 spec (`feature/`, `bugfix/`, `hotfix/`, etc.), inferred from diff content. Useful for teams enforcing branch naming conventions.

---

## Feature Request Trends

1. **Multi-account/workspace management** — The #1 request by reaction count (Issue #18435). Users want profile switching, household plans (Issue #75063), and multi-workspace Slack support (Issue #44243). Clear unmet need for power users with multiple organizational affiliations.

2. **Workflow/agent visibility improvements** — Multiple requests: consolidated progress views (Issue #63982), subagent model exposure in statusline (Issue #73654), persistent active model display (Issue #75047), and distinct notification sounds for "waiting for input" vs "done" (Issue #73384). Users want better observability into multi-agent orchestration.

3. **External integrations & signaling** — External wake signals for interactive sessions (Issue #60943), real-time bash output in VS Code (Issue #14280), and session group reordering/pinning (Issue #70104). Demand for less blocking, more asynchronous UX.

4. **Post-workflow hooks and automation** — Consolidation of workflow hooks (Issue #63982) and safe hook wrappers (PR #41453). Users want to run cleanup, notification, or CI tasks after sessions complete without fragile workarounds.

5. **Local MCP parity in VS Code** — Issue #75072 reports that the VS Code extension doesn't load local MCPs added via `claude mcp add` (stored in `.claude.json`) into its own chat panel — only built-in `claude.ai` connectors come through. This creates a gap between CLI and VS Code experiences.

---

## Developer Pain Points

- **Safety filter false positives are blocking work** — The cluster of 7+ issues today from one user shows Opus 4.8's cybersecurity filter is aggressively blocking mundane `ls`, `git status`, and directory inspection commands. Marked severity "session-halted" — users cannot continue without restarting sessions.

- **Agent orchestration is fragile** — Nested subagents break in multiple ways: ownership errors on resume (Issue #75043), model override silently dropped across continuation boundaries (Issue #68147), and background agent tasks persisting as "running" after restart (Issue #65925). Multi-agent workflows are not production-reliable yet.

- **Hook system has silent failure modes** — A single schema-invalid matcher disables all hooks with no warning (Issue #75071). Successful hooks display "Failed with non-blocking status code" messages (Issue #66952). The hook system lacks validation and clear error reporting, costing developers hours of debugging.

- **Windows continues to be a second-class platform** — The Cowork tab missing bug (Issue #48407) has 38 comments and no resolution since April. Background agent task persistence (Issue #65925) also affects Windows. Linux, macOS, and Windows get inconsistent feature parity.

- **No easy way to know what model is active** — Multiple issues (#75047, #73654) highlight that users can't see which model (Opus, Sonnet, etc.) is currently running, especially in subagents. This causes confusion about cost and capability.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-07

## Today's Highlights

The Codex community remains laser-focused on two critical issues: **GPT-5.5 reasoning-token clustering** (Issue #30364, 131 comments, 228 👍) and a **persistent context compaction bug** that users report "ruins sessions." On the engineering side, OpenAI is making progress on system proxy routing for inference traffic (PR #31335) and a structured `UserInstructions` hook system (PRs #30138–#30141) that will give deterministic provider precedence for managed configurations.

## Releases

- **rust-v0.143.0-alpha.37**: Released today. No changelog beyond the version bump. This is an alpha patch likely containing minor fixes or pre-release infrastructure work.

## Hot Issues

1. **[#30364] GPT-5.5 Codex reasoning-token clustering at 516/1034/1552 may degrade complex task performance**  
   *Author: vguptaa45 | 131 comments | 228 👍*  
   A data-driven discovery that `gpt-5.5` responses cluster at fixed `reasoning_output_tokens` boundaries (516, 1034, 1552). Users suspect this artificial quantization reduces reasoning depth on complex tasks. This is the highest-engagement issue on the board and suggests a model-serving optimization that may be hurting output quality.  
   [Link](https://github.com/openai/codex/issues/30364)

2. **[#8648] Codex replies to earlier messages instead of latest one in conversations**  
   *Author: BobbyWang0120 | 87 comments | 55 👍*  
   A seven-month-old bug where Codex loses conversation thread context and responds to stale messages. Still open with active reproduction reports. This undermines trust in multi-turn workflows for Pro users on `gpt-5.2-xhigh`.  
   [Link](https://github.com/openai/codex/issues/8648)

3. **[#31033] Context automatically compacted / "RUINS SESSIONS"**  
   *Author: nikkapet22-bot | 5 comments | 0 👍*  
   Despite low engagement, the title telegraphs high severity. A user on the latest release (26.623) reports Codex consuming two resets and 50% of monthly credits from aggressive, unwanted context compaction. No official response yet.  
   [Link](https://github.com/openai/codex/issues/31033)

4. **[#31322] Usage limits normalized then regressed ~5x faster in one day**  
   *Author: in0vik | 3 comments | 0 👍*  
   A fresh report of limit instability: normalized in the morning, reverted to 5x consumption by evening. References a prior issue (#30939) that was presumably closed as resolved. Suggests a systemic rate-limit accounting problem, not a one-off spike.  
   [Link](https://github.com/openai/codex/issues/31322)

5. **[#24246] macOS "Malware Blocked" alert for Codex helper**  
   *Author: GGBondBlueWhale | 14 comments | 10 👍*  
   Users seeing macOS Gatekeeper warnings about Codex containing malware. Likely a code-signing or notarization issue rather than actual malware, but the UX is alarming and damages trust.  
   [Link](https://github.com/openai/codex/issues/24246)

6. **[#23574] VS Code extension allocates ~1M inotify watches on Linux**  
   *Author: interconnectedMe | 8 comments | 9 👍*  
   A filesystem watcher explosion that can hit Linux’s `inotify` watch limit, crashing the extension on large workspaces. Critical for Linux-based developers using VS Code with Codex.  
   [Link](https://github.com/openai/codex/issues/23574)

7. **[#29408] Windows Desktop leaves repeated/stuck git.exe polling processes**  
   *Author: maplel | 9 comments | 2 👍*  
   Multi-repo workspace users on Windows see `git.exe` processes accumulate and never terminate. Likely a polling loop without proper process lifecycle management.  
   [Link](https://github.com/openai/codex/issues/29408)

8. **[#28330] VS Code extension crashes on curated plugin with >128 char defaultPrompt**  
   *Author: SEngelnkemper | 5 comments | 5 👍*  
   A regression in newer extensions: a bundled skill (`ngs-analysis`) has a `defaultPrompt` exceeding 128 characters, crashing the extension on install. This is a trivial validation gap with a significant user impact.  
   [Link](https://github.com/openai/codex/issues/28330)

9. **[#16933] CLI renders hook additionalContext as visible developer message**  
   *Author: FasterPHP | 14 comments | 3 👍*  
   Hooks returning `additionalContext` for auto-recall leak that context into the visible transcript, contradicting documented "invisible" behavior. Privacy/transparency issue for Hindsight Codex integrations.  
   [Link](https://github.com/openai/codex/issues/16933)

10. **[#31243] Local file edits accidentally rewrite whole files, overwriting changes**  
    *Author: bryanxtong | 5 comments | 0 👍*  
    CLI users on `gpt-5.4-mini` report file edits that obliterate existing changes by rewriting the entire file. A destructive tool-call bug with no rollback safety.  
    [Link](https://github.com/openai/codex/issues/31243)

## Key PR Progress

1. **[#31335] core: route Responses API through system proxy**  
   A first-class fix for users behind OS-managed proxies who can log in but cannot send inference requests. This is the production version of the already-working auth proxy path, now extended to the main inference path.  
   [Link](https://github.com/openai/codex/pull/31335)

2. **[#31333] core: track thread publication lifecycle**  
   A robust thread lifecycle system: registers threads under stable IDs, retains parent relationships, and prevents stale handles from mutating replaced threads. Targets the "ghost conversation" bug (#29868).  
   [Link](https://github.com/openai/codex/pull/31333)

3. **[#31331] Migrate direct HTTP consumers to codex-http-client**  
   Cleanup PR extracting shared HTTP transport into `codex-http-client` (already introduced in #31323). Enables consistent proxy, CA, and retry behavior across all Codex crates.  
   [Link](https://github.com/openai/codex/pull/31331)

4. **[#31334] Align skill creator paths with supported locations**  
   Documents and enforces the three-tier skill storage hierarchy: project-level (`.agents/skills`), user-level (`~/.agents/skills`), and admin-level (`/etc/codex/skills`). Reduces confusion about where custom skills should live.  
   [Link](https://github.com/openai/codex/pull/31334)

5. **[#31306] Support sequential cutoff reasoning summaries**  
   Adds a `sequential_cutoff` delivery mode for reasoning summaries, bypassing partial summary events. Improves deterministic rendering of model reasoning output in the UI.  
   [Link](https://github.com/openai/codex/pull/31306)

6. **[#30141] core: load aggregated hook-backed user instructions**  
   Resolves all configured `UserInstructions` hooks during fresh session construction, concatenating outputs alongside global `AGENTS.md`. This is the runtime activation piece for the new instruction hook system.  
   [Link](https://github.com/openai/codex/pull/30141)

7. **[#30139] config: add repeatable UserInstructions declarations**  
   Models user instructions as an ordered list of command handlers rather than matcher groups. Allows deterministic combination of multiple instruction providers, including managed requirements.  
   [Link](https://github.com/openai/codex/pull/30139)

8. **[#30138] hooks: define UserInstructions execution contract**  
   The foundational contract: thread-scoped events, repeatable command runners, ordered output preservation, and status-only lifecycle events. Groundwork for the entire hook-based instruction system.  
   [Link](https://github.com/openai/codex/pull/30138)

9. **[#31274] Add externally provided Codex auth**  
   An in-memory externally provided auth snapshot with explicit runtime capabilities, installable through the existing `ExternalAuth` provider path. Supports enterprise auth workflows without persistent storage.  
   [Link](https://github.com/openai/codex/pull/31274)

10. **[#31332] ci: route build IO through shared setup**  
    Optimizes Windows CI by moving Cargo/Bazel filesystem work behind a shared setup with a Dev Drive-backed build root. Targets the longest-running CI jobs.  
    [Link](https://github.com/openai/codex/pull/31332)

## Feature Request Trends

- **Event-driven session wake primitives** (#20312, 9 comments): Developers want Codex to react to external events (chat mentions, file changes, MCP pushes) without requiring a manual turn. This is the most commonly requested architectural change, enabling agent-style continuous operation.
- **Dynamic nested AGENTS.md loading** (#12115, 23 comments, 83 👍): Users want on-demand loading of agent configuration from subdirectories, mirroring Claude Code’s `CLAUDE.md` behavior. Currently all config must be hoisted to the root.
- **`--worktree` and `--tmux` CLI flags** (#12862, 19 comments, 85 👍): Developers want first-class support for isolated git worktrees and tmux sessions in one command, replacing manual shell scripting.
- **Detailed rate-limit reset credit exposure** (#29618, 5 comments): Users want visible expiry dates for earned reset credits, not just available count. Requests transparency in the rate-limit accounting system.

## Developer Pain Points

1. **Rate-limit instability**: The cluster of rate-limit issues this week (#30364, #31322, #27142, #29618, #31033) points to a systemic problem with token accounting, reset credits, and aggressive context compaction. Users report unpredictable consumption patterns that burn through monthly quotas.
2. **Context/session corruption**: Multiple reports of ghost conversations (#29868), stale thread responses (#8648), automatic context compaction (#31033), and failed archiving (#28276) suggest the session management subsystem is brittle under normal usage.
3. **Desktop reliability on macOS**: Malware alerts (#24246), database access failures (#24006), and Computer Use crashes (#20683) on macOS make the desktop app feel unstable for Pro/Enterprise users on the platform.
4. **Destructive file edits**: The CLI’s tool-call implementation can rewrite entire files (#31243) with no undo safety. Combined with the "manual approval auto-cancel" bug (#29627), users lack confidence in autonomous edit workflows.
5. **Windows-specific process leaks**: Stuck `git.exe` processes (#29408) and failing memory consolidation (#23129) show that Windows continues to be a second-class platform for Codex, despite growing enterprise adoption.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-07

## Today's Highlights
No new releases landed today, but the community remains deeply engaged on long-standing agent reliability issues. The **Subagent recovery misreporting** (MAX_TURNS reported as GOAL success) and **Generalist agent hang** continue to attract the most attention, with maintainers actively retesting. Three Pull Requests were closed, including a fix for escape-sequence corruption in string literals and a macOS sandbox hardening patch for `~/.gitconfig`.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues (Top 10)

1. **[#22323 – Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *10 comments, 2 👍*  
   The `codebase_investigator` subagent reports `status: "success"` with `Termination Reason: "GOAL"` after hitting the maximum turn limit with zero analysis done. This masks a critical failure as a success, degrading trust in agent telemetry. High-priority P1 and flagged for retesting.

2. **[#21409 – Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *7 comments, 8 👍*  
   One of the most upvoted bugs right now. When Gemini CLI defers to the generalist subagent, it hangs indefinitely (up to an hour). Workaround: instructing the model to avoid subagents entirely. Maintainers are retesting.

3. **[#24353 – Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)**  
   *7 comments*  
   Epic tracking 76 behavioral eval tests across 6 Gemini models. Aims to build systematic component-level evaluations to prevent regressions in subagent behavior — a foundational quality initiative.

4. **[#22745 – Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *7 comments, 1 👍*  
   Investigates whether AST-aware tools (e.g., reading method bounds in one call) can reduce token waste, misaligned reads, and total turns. Could significantly improve codebase investigator efficiency.

5. **[#21968 – Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *6 comments*  
   Users report the model rarely invokes custom skills or sub-agents autonomously, even when highly relevant. Suggests a gap in the model's tool-selection reasoning.

6. **[#19873 – Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)**  
   *8 comments, 1 👍*  
   Gemini 3 models are natively trained on POSIX toolchains. This enhancement proposes sandboxing to safely unlock native bash capabilities without compromising security. Large effort, high impact.

7. **[#25166 – Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *4 comments, 3 👍*  
   After simple CLI commands finish, the tool hangs showing "Awaiting user input." Extremely disruptive for automated workflows. P1, medium effort.

8. **[#26522 – Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *5 comments*  
   The background memory extraction agent keeps revisiting sessions it already deemed low-signal, wasting quota and compute. Needs a processed-state marker.

9. **[#26525 – Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *3 comments*  
   Security concern: Auto Memory sends local transcripts to the model before redacting secrets, and logs existing skill content. Redaction should happen pre-transmission.

10. **[#22267 – Browser Agent ignores settings.json overrides (e.g., maxTurns)](https://github.com/google-gemini/gemini-cli/issues/22267)**  
    *3 comments*  
    Configuration overrides for the browser subagent are read by the registry but silently discarded during execution. Undermines user control over agent behavior.

---

## Key PR Progress (Top 10)

1. **[#28223 – fix(core-tools): bypass LLM correction for JSON and IPYNB files](https://github.com/google-gemini/gemini-cli/pull/28223)**  
   *Open*  
   Surgical fix for `write_file` and `replace` corrupting `.ipynb` and `.json` files. Prevents the LLM from "correcting" structured data it doesn't understand.

2. **[#28244 – docs(policy-engine): use a safe test command instead of rm -rf /](https://github.com/google-gemini/gemini-cli/pull/28244)**  
   *Open*  
   Replaces the dangerously instructive `rm -rf /` example in policy engine docs with a safe command. Lowers the barrier for new users while preventing copy-paste disasters.

3. **[#27971 – fix(core): strip thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971)**  
   *Open*  
   Resolves "Thought Leakage" — the model's internal monologue leaking into history, causing confusion and infinite loops in subsequent turns.

4. **[#28216 – Refactor: exclude transient CI config from workspace context](https://github.com/google-gemini/gemini-cli/pull/28216)**  
   *Open*  
   Excludes `gha-creds-*.json` from workspace context. Prevents accidental exposure of CI credentials to the model.

5. **[#28299 – fix(core): preserve escape sequences in string literals](https://github.com/google-gemini/gemini-cli/pull/28299)**  
   *Closed*  
   Fixes the "newline-in-string" bug where `\n` and `\t` inside string literals were converted to literal characters. Applied to all modern Gemini models.

6. **[#28221 – fix(sandbox): make ~/.gitconfig read-only in macOS sandbox](https://github.com/google-gemini/gemini-cli/pull/28221)**  
   *Closed*  
   Hardens the macOS Seatbelt sandbox by making `~/.gitconfig` read-only. Prevents sandboxed processes from modifying git config that could enable command execution.

7. **[#28089 – feat(core): implement MCP elicitation (form + url)](https://github.com/google-gemini/gemini-cli/pull/28089)**  
   *Open*  
   Implements MCP Elicitation spec (form and URL modes), enabling dynamic user input collection and external URL invocation from MCP tools.

8. **[#28068 – fix(core): guard message inspectors against empty parts arrays](https://github.com/google-gemini/gemini-cli/pull/28068)**  
   *Closed*  
   Fixes a subtle bug where empty `parts: []` arrays were misclassified as function calls/responses due to JavaScript's vacuous `[].every()` truthiness.

9. **[#22093 – (Sub)agents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)**  
   *Open*  
   Users report subagents activating despite being disabled in config. Root cause likely a registry loading regression.

10. **[#21763 – Bugreport doesn't provide subagent context](https://github.com/google-gemini/gemini-cli/issues/21763)**  
    *Open*  
    `/bug` reports only capture the main session — no subagent internals. Makes debugging agent failures nearly impossible.

---

## Feature Request Trends

- **AST-aware tooling**: Multiple issues (e.g., #22745, #22746) advocate for AST parsing in file reads, codebase mapping, and search to reduce token waste and turn counts.
- **Agent self-awareness**: Users want the CLI to know its own flags, hotkeys, and capabilities — and be able to execute itself autonomously (#21432).
- **Subagent trajectory sharing**: Explicit demand for `/chat share` to include subagent traces for debugging and eval review (#22598).
- **MCP elicitation**: The recently merged PR #28089 formalizes support for dynamic form and URL elicitation in MCP tools.
- **Policy engine hardening**: Documentation fixes and sandbox patches reflect growing emphasis on safe default behaviors.

---

## Developer Pain Points

1. **Subagent reliability**: Hangs (#21409), false success reports (#22323), ignored config (#22267), and unauthorized launches (#22093) erode trust in agent orchestration.
2. **Shell execution fragility**: Commands get stuck on "Waiting input" (#25166), temporary scripts litter workspaces (#23571), and the model executes destructive git/db commands (#22672).
3. **Memory system issues**: Auto Memory retries low-signal sessions (#26522), sends unredacted content to models (#26525), and silently skips invalid patches (#26523).
4. **Escape sequence corruption**: Newline and escape handling bugs in file writes (#22466, #28299) cause data integrity issues, especially for structured files like JSON.
5. **Tool overload**: With >128 tools, the CLI returns 400 errors (#24246); a tool-selection strategy is needed to scope available tools per task.
6. **History and state leakage**: Model thoughts leaking into history (#27971), and `/bug` reports omitting subagent context (#21763), impede debugging.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date: 2026-07-07**

---

## Today's Highlights

A new patch release (v1.0.69-2) landed with fixes for MCP server OAuth sign-in and terminal UI clipping, alongside improved `/rubber-duck` discoverability. The community is actively discussing enterprise plugin scoping (#1665) and authentication state bugs in ACP mode (#3902), while new triage issues around voice mode failures and MCP server protocol edge cases demand attention.

---

## Releases

**v1.0.69-2** — [Release Link](https://github.com/github/copilot-cli/releases/tag/v1.0.69-2)

- **Added:** `/rubber-duck` command now appears in pre-auth help and self-documentation
- **Improved:** Sign-in to MCP servers through the CLI OAuth callback flow
- **Improved:** Full `/user` switch picker now revealed when timeline is full — hint bar no longer clipped below terminal
- **Fixed:** Files inside `n` directory are now properly included

---

## Hot Issues (10 Noteworthy)

1. **[#1665 – Support Copilot CLI Plugins Scoped to Project or Repository](https://github.com/github/copilot-cli/issues/1665)** (CLOSED, 👍18)
   *Why it matters:* Currently plugins are global per-user; teams need per-repo/project plugin configurations for consistent tooling across environments. High community demand (18 upvotes).

2. **[#3596 – Error loading model list: Not authenticated on session resume](https://github.com/github/copilot-cli/issues/3596)** (CLOSED, 👍11)
   *Why it matters:* A critical authentication regression that blocks model selection when resuming sessions. 11 developers hit this since v1.0.56.

3. **[#3028 – MCP permissions configuration](https://github.com/github/copilot-cli/issues/3028)** (OPEN, 👍5)
   *Why it matters:* Users need granular allow/deny lists for MCP server tools — similar to `trustedFolders`. Enterprise security teams are watching.

4. **[#1428 – Bash tool incompatible with Nix shell environment](https://github.com/github/copilot-cli/issues/1428)** (CLOSED, 👍7)
   *Why it matters:* Nix users report all bash commands hang indefinitely in Nix develop shells. A significant blocker for the Nix/declarative development community.

5. **[#4003 – Support custom model endpoint in Copilot CLI](https://github.com/github/copilot-cli/issues/4003)** (OPEN)
   *Why it matters:* Users want to bring their own local/private models (as VS Code already supports). Enterprise and offline development use cases depend on this.

6. **[#4024 – Voice mode: all bundled ASR models fail silently](https://github.com/github/copilot-cli/issues/4024)** (OPEN)
   *Why it matters:* A critical bug in `/voice` — audio captures but transcriptions return empty for all three ASR models. Newly reported and blocking voice functionality.

7. **[#3074 – Add `/effort` command to switch reasoning effort](https://github.com/github/copilot-cli/issues/3074)** (OPEN, 👍6)
   *Why it matters:* Power users want a quick command to adjust reasoning effort mid-session without the multi-step `/model` workflow. 6 upvotes in a month.

8. **[#4034 – Hook subprocess stdin write-end left open — `$(cat)` pattern hangs](https://github.com/github/copilot-cli/issues/4034)** (CLOSED)
   *Why it matters:* A subtle but painful hook bug where tool-use hooks never close stdin, causing documented `$(cat)` patterns to hang indefinitely.

9. **[#4038 – Non-interactive mode: late-connecting MCP server injects empty user message](https://github.com/github/copilot-cli/issues/4038)** (OPEN)
   *Why it matters:* When using MCP servers with 7+ tools in `-p` mode, the model sees an empty prompt and echoes tool lists instead of answering. A protocol-level regression.

10. **[#1389 – Multi-Agent Workflow System](https://github.com/github/copilot-cli/issues/1389)** (CLOSED, 👍17)
    *Why it matters:* Community clamors for multi-agent orchestration with specialized roles (architecture, dev, research). 17 upvotes — this is the most-requested feature overall.

---

## Key PR Progress

No pull requests were updated in the last 24 hours.

---

## Feature Request Trends

1. **Plugin Scoping & Management** — Multiple requests for per-project/repository plugin configurations (#1665, #4032). Users want plugins to be installable at the project level, not just globally.

2. **Multi-Agent / Collaborative Workflows** — #1389 (multi-agent teams) and #2367 (subagent waiting) reflect a strong desire for Copilot to orchestrate specialized agents for complex workflows.

3. **Custom Model & Endpoint Support** — #4003 and #4037 (BYOK for ACP) show demand for bring-your-own-model capabilities, mirroring VS Code's custom endpoints.

4. **Voice & Multimodal** — #4024 (ASR failures) and #4035 (voice installer 401) highlight growing voice mode usage with infrastructure gaps.

5. **Local Memory / Auto-Memory** — #2930 and #3945 (memory leaking between repos) indicate users want persistent context without cloud dependencies, but the current implementation has leakage issues.

---

## Developer Pain Points

1. **Authentication State Management** — #3596 and #3902 describe a persistent auth bug where session resume or ACP mode fails to refresh credentials. This is a high-frequency pain point affecting daily workflow.

2. **Nix / Unconventional Shell Environments** — #1428 (bash tool hangs in Nix shells) shows Copilot CLI has limited compatibility with declarative development environments.

3. **MCP Server Protocol Edge Cases** — #4038 (empty user message injection) and #4034 (hook stdin not closed) represent growing pains as MCP adoption increases.

4. **Windows Compatibility Gaps** — #4001 (hooks run via PowerShell not bash on Windows) and #4001 (`$CLAUDE_PROJECT_DIR` not set) make cross-platform hooks unreliable.

5. **Enterprise Configuration Sync** — #4039 (enterprise plugins marked installed but never synced to disk) undermines managed deployments and trust in enterprise features.

6. **Voice Mode Infrastructure Fragility** — #4024 (all ASR models fail) and #4035 (private Azure feed 401) suggest voice mode reached users before the runtime dependency chain was hardened.

---

*Digest generated from github.com/github/copilot-cli activity on 2026-07-07*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-07

## Today's Highlights
No new releases or pull requests were published in the last 24 hours, indicating a stable development pause. Two new issues emerged: a terminal display corruption bug on Windows 11 (#2485) and a feature request to expose usage limits via ACP (#2486). The community is still waiting for fixes on several long-standing issues, particularly around tool selection and ACP reliability.

## Releases
*No new releases in the last 24 hours.*

## Hot Issues
1. **#2485 — [Bug] CLI terminal distortion after prolonged use**  
   *Author: mynameiscuining | Windows 11, Kimi Code CLI 0.22.0, Moderato subscription*  
   The first menu option disappears and rendering becomes garbled over time. This is a critical UX regression affecting Windows users.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2485)

2. **#2486 — [Enhancement] Expose usage limits and reset times via ACP**  
   *Author: jgiacomini | Building ACP client for Visual Studio 2026*  
   IDEs need programmatic access to `/usage` data. Currently no ACP endpoints expose this, limiting third-party integrations.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2486)

3. **#2480 — [Bug] `kimi` tool selection persists across sessions unexpectedly**  
   High community interest. Users expect tool choices (e.g., "read_file") to reset or be configurable per session. Current behavior causes unintended repeated actions.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2480)

4. **#2475 — [Bug] ACP mode fails to reconnect after network interruption**  
   Multiple users report that ACP connections hang permanently after temporary network loss, requiring manual restart.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2475)

5. **#2469 — [Feature] Add `--json` flag for machine-readable output**  
   Requested by CI/CD pipeline users. Without structured output, automating Kimi Code in scripts remains painful.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2469)

6. **#2465 — [Bug] Memory usage grows unbounded in long sessions**  
   Users on 16GB machines report OOM after 2–3 hours of continuous use. Relates to unreleased conversation context accumulation.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2465)

7. **#2460 — [Bug] `kimi` command ignores `--model` flag when ACP is active**  
   Workaround: users must set the model via `KIMI_MODEL` environment variable. Flag parsing order is incorrect.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2460)

8. **#2453 — [Enhancement] Support streaming responses in ACP for real-time UX**  
   ACP currently delivers complete responses only. IDEs want progressive output for better user experience.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2453)

9. **#2448 — [Bug] Non-ASCII characters garbled in terminal output on macOS**  
   Specifically affects CJK and emoji characters. Related to UTF-8 encoding handling in the output renderer.  
   [URL](https://github.com/MoonshotAI/kimi-cli/issues/2448)

10. **#2440 — [Feature] Add `kimi config` command for persistent settings**  
    Users want a `~/.kimi/config.yaml` management interface. Currently must hand-edit config files.  
    [URL](https://github.com/MoonshotAI/kimi-cli/issues/2440)

## Key PR Progress
*No pull requests were updated in the last 24 hours.*

## Feature Request Trends
- **ACP integration parity**: Multiple requests (e.g., #2486, #2453, #2460) show a clear demand for full ACP feature parity with the CLI, including streaming, usage stats, and flag handling.
- **Config management**: Requests for `kimi config` (#2440) and session persistence controls (#2480) highlight a need for declarative, file-based configuration.
- **Structured output**: `--json` flag (#2469) and machine-readable error codes are recurring asks from DevOps teams embedding Kimi Code in pipelines.

## Developer Pain Points
- **Memory leaks & stability**: Unbounded memory growth (#2465) and terminal corruption (#2485) are the top two blockers for daily driving the CLI, especially on resource-constrained Windows machines.
- **ACP fragility**: Network interruption handling (#2475) and model flag conflicts (#2460) undermine confidence in ACP as a reliable IDE integration protocol.
- **Localization**: Non-ASCII rendering issues (#2448) persist, affecting non-English-speaking developers disproportionately.
- **Lack of introspection**: Users cannot programmatically query their plan/usage limits (#2486) or configure defaults (#2440), forcing manual workarounds.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**Date:** 2026-07-07

---

## Today's Highlights

OpenCode shipped **v1.17.14** with a new Code Mode MCP adapter and critical fixes for paginated MCP catalogs. The community is rallying around **V2 event schema refinements** stemming from a Discord "gang grill" session, with multiple tracking issues and follow-up PRs moving through the pipeline. A surge of **Windows ARM64 native support** and **session UI usability** issues dominated new bug reports, while the **#8501 feature request** for expanding pasted text continues to attract intense community support.

---

## Releases

### v1.17.14
[View Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.14)

**Core Improvements:**
- Added a Code Mode MCP adapter for running confined orchestration scripts against connected MCP tools
- Hid the `execute` tool unless code mode is enabled

**Bugfixes:**
- Fixed paginated MCP tool catalogs losing tool metadata and output schema validation
- Preserved list truncation stability improvements

---

## Hot Issues

1. **[#28846] Adjust Go usage limits after DeepSeek V4 Pro 75% price reduction** *(CLOSED)*
   - **Author:** icocoon | **Comments:** 92 | **👍:** 82
   - **Link:** [Issue #28846](https://github.com/anomalyco/opencode/issues/28846)
   - **Why it matters:** The most-commented issue today reflects the userbase aggressively pushing for subscription cost adjustments after a massive provider price cut. The high number of upvotes signals strong demand for pricing transparency.

2. **[#4276] Is zen/big-pickle glm 4.6?** *(CLOSED)*
   - **Author:** aziham | **Comments:** 31 | **👍:** 3
   - **Link:** [Issue #4276](https://github.com/anomalyco/opencode/issues/4276)
   - **Why it matters:** A long-running question about model identity that refuses to die. Users are still investigating whether OpenCode's internal models match well-known open-source architectures.

3. **[#8501] Allow to expand the pasted text** *(OPEN)*
   - **Author:** berenar | **Comments:** 28 | **👍:** 202
   - **Link:** [Issue #8501](https://github.com/anomalyco/opencode/issues/8501)
   - **Why it matters:** The **most-upvoted open feature request** in the repository. Users love the paste-summarization feature but want the ability to inspect and edit the collapsed content before sending it to the model.

4. **[#19948] Integration with Ollama Local** *(OPEN)*
   - **Author:** TheTwinEsper | **Comments:** 22 | **👍:** 4
   - **Link:** [Issue #19948](https://github.com/anomalyco/opencode/issues/19948)
   - **Why it matters:** A recurring pain point for local-first users — Ollama models return malformed JSON in the desktop app on Windows, preventing local model adoption.

5. **[#31119] Error: no such column: name** *(OPEN)*
   - **Author:** AndrewShear | **Comments:** 10 | **👍:** 8
   - **Link:** [Issue #31119](https://github.com/anomalyco/opencode/issues/31119)
   - **Why it matters:** A database migration bug that completely blocks usage after upgrading from older versions. Affects returning users who may have skipped several versions.

6. **[#19130] Windows ARM64 native: OpenTUI fails to initialize** *(OPEN)*
   - **Author:** Carliquiss | **Comments:** 8 | **👍:** 7
   - **Link:** [Issue #19130](https://github.com/anomalyco/opencode/issues/19130)
   - **Why it matters:** Windows on ARM users cannot use the TUI at all — the native ARM64 binary works for non-interactive commands but fails with `bun:ffi dlopen TinyCC error`.

7. **[#34754] The opencode funneling scam** *(CLOSED)*
   - **Author:** Pachinko0 | **Comments:** 7 | **👍:** 0
   - **Link:** [Issue #34754](https://github.com/anomalyco/opencode/issues/34754)
   - **Why it matters:** A controversial UX/billing complaint about users being charged for Zen when they intended to subscribe to Go. This issue highlights a serious UX trust concern.

8. **[#34341] V2: route progressive AGENTS.md through System Context** *(OPEN)*
   - **Author:** opencode-agent[bot] | **Comments:** 6 | **👍:** 0
   - **Link:** [Issue #34341](https://github.com/anomalyco/opencode/issues/34341)
   - **Why it matters:** A core V2 design decision — fixing sticky instructions from `AGENTS.md` files that currently appear as synthetic user messages with accidental lifetimes.

9. **[#35021] V2: event audit tracker** *(CLOSED)*
   - **Author:** opencode-agent[bot] | **Comments:** 3 | **👍:** 0
   - **Link:** [Issue #35021](https://github.com/anomalyco/opencode/issues/35021)
   - **Why it matters:** The mega-tracker for the V2 event schema redesign from a Discord community session. This issue links all related V2 schema improvements.

10. **[#35611] Go models inference slow/stuck on Windows after v1.17.14** *(OPEN)*
    - **Author:** Kuromi-zyzy | **Comments:** 2 | **👍:** 0
    - **Link:** [Issue #35611](https://github.com/anomalyco/opencode/issues/35611)
    - **Why it matters:** A regression in the latest release — Go subscription models stall on Windows in existing sessions, requiring new session creation as a workaround.

---

## Key PR Progress

1. **[#35637] fix(tui): align switch reminders** *(OPEN)*
   - **Author:** opencode-agent[bot]
   - **Link:** [PR #35637](https://github.com/anomalyco/opencode/pull/35637)
   - **Summary:** Fixes indentation alignment for agent/model/variant switch reminders to match instruction reminders, with a renderer test.

2. **[#35634] fix(provider): ensure required array is present in object schemas** *(OPEN)*
   - **Author:** ViNull008
   - **Link:** [PR #35634](https://github.com/anomalyco/opencode/pull/35634)
   - **Summary:** Closes #35528 — Fixes tool schemas with `additionalProperties: false` but no `required` field that fail strict JSON Schema validators.

3. **[#35636] fix(core): preserve compaction work details** *(OPEN)*
   - **Author:** opencode-agent[bot]
   - **Link:** [PR #35636](https://github.com/anomalyco/opencode/pull/35636)
   - **Summary:** Improves session compaction output by using subheadings for completed/active/blocked work and restoring the dedicated relevant-files section.

4. **[#35371] feat(core): add durable compaction barrier** *(CLOSED)*
   - **Author:** kitlangton
   - **Link:** [PR #35371](https://github.com/anomalyco/opencode/pull/35371)
   - **Summary:** Generalizes session input into a typed durable inbox, admits manual compaction barriers, and blocks unpromoted queue entries behind the barrier.

5. **[#35617] feat(codemode): support promise chaining** *(OPEN)*
   - **Author:** rekram1-node
   - **Link:** [PR #35617](https://github.com/anomalyco/opencode/pull/35617)
   - **Summary:** Adds `then`, `catch`, `finally` support to sandbox promises, plus chainable return from `all`, `allSettled`, and `race`.

6. **[#35635] feat(desktop): support RTL direction and alignment** *(OPEN)*
   - **Author:** majidasgari
   - **Link:** [PR #35635](https://github.com/anomalyco/opencode/pull/35635)
   - **Summary:** Implements dynamic Right-to-Left text rendering for Persian, Arabic, Hebrew, and other RTL scripts in the desktop app's markdown and editor.

7. **[#35613] feat(plugin): tool.execute.before can shortcircuit** *(CLOSED)*
   - **Author:** jackieju
   - **Link:** [PR #35613](https://github.com/anomalyco/opencode/pull/35613)
   - **Summary:** Adds an optional `shortcircuit` field to the plugin hook output, allowing plugins to skip real tool execution and return canned results.

8. **[#35629] feat(core): expose OpenCode API in Code Mode** *(OPEN)*
   - **Author:** rekram1-node
   - **Link:** [PR #35629](https://github.com/anomalyco/opencode/pull/35629)
   - **Summary:** Registers the full OpenAPI-supported V2 API under `tools.opencode.v2.*` for every server-backed location, extending Code Mode registration.

9. **[#35311] fix(core): Multiple clones of same repo are different projects** *(OPEN)*
   - **Author:** belisoful
   - **Link:** [PR #35311](https://github.com/anomalyco/opencode/pull/35311)
   - **Summary:** Closes ~15 related issues by fixing project tracking for multiple clones of the same repository. A long-standing bug fix affecting many users.

10. **[#35633] fix(app): load capped review patches** *(OPEN)*
    - **Author:** Hona
    - **Link:** [PR #35633](https://github.com/anomalyco/opencode/pull/35633)
    - **Summary:** Handles review files where aggregate patches were omitted by the 10 MB cap, reloading them through the directory-scoped VCS diff API.

---

## Feature Request Trends

| Trend | Evidence | Community Signal |
|-------|----------|-----------------|
| **V2 event schema redesign** | Issues #34341, #35017, #35019, #35020, #35021 | Strong collaborative effort from Discord "gang grill" sessions |
| **Desktop session titles** | #30926, #35627, #35592 | Recurring demand for auto-generated session titles instead of "New session" |
| **Local model support** | #19948 (Ollama), ongoing | Users want robust local-first workflows on Windows |
| **i18n and accessibility** | #35601 (zh-CN menus), #35635 (RTL support) | Growing international user base pushing for localization |
| **Paste text expandability** | #8501 — 202 upvotes | The most-demanded single feature — users want to edit collapsed paste |
| **Code Mode API exposure** | #35617, #35629 | Active development toward sandbox scripting and internal API access |

---

## Developer Pain Points

- **Windows ARM64 TUI failure:** Native ARM64 binary exits with `bun:ffi dlopen TinyCC error` during TUI initialization (#19130) — a blocker for Qualcomm/Apple Silicon Windows users.
- **Session UI confusion:** Invisible child sessions (#29175), no session titles (#30926/#35627/#35592), prompt leaking between sessions (#35587) — basic session management frustrating users.
- **Go model performance regression:** v1.17.14 introduced slow/stuck inference for Go subscription models on Windows (#35611), requiring session restarts.
- **Database migration fragility:** Users who skipped several versions encounter schema errors (#31119) that completely block the application.
- **Config instruction precedence:** Global `opencode.jsonc` instructions are silently ignored when `~/.claude/CLAUDE.md` exists (#35552) — a confusing behavior for users migrating from Claude Code.
- **Restart and folder management:** No CLI restart functionality (#35593) and no way to change working folder from CLI (#35594) — missing basic QOL features for terminal-first developers.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-07

**Repository:** [github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)

---

## 1. Today's Highlights

The Pi ecosystem saw active triage across caching, clipboard, and extension lifecycle issues. A critical cache token double-count bug was fixed (PR #6352), while the long-standing empty tool result mislabel bug (#6103) was finally closed. Extension developers received new hooks for provider header manipulation (#6350) and an idle agent event proposal (#6363). Two prominent PRs from community contributor mitsuhiko—on constrained sampling (#6341) and malformed tool call handling (#6285)—remain open for discussion.

---

## 2. Releases

No new versions were published in the last 24 hours.

---

## 3. Hot Issues

### #6234 — Escape leaves Pi stuck in Working when extension hook never settles
- **Author:** xz-dev | **Comments:** 8 | **Status:** CLOSED
- **Summary:** Pressing Escape to abort an active run leaves the TUI stuck in "Working..." if an extension context hook never resolves. Double-Escape is swallowed by streaming abort logic.
- **Why it matters:** Fundamental flow-control bug affecting all extension users—any runaway hook permanently freezes the interface.
- [GitHub](https://github.com/earendil-works/pi/issues/6234)

### #6103 — OpenAI Responses API mislabels empty tool results as "(see attached image)"
- **Author:** highlyunavailable | **Comments:** 6 | **Status:** CLOSED
- **Summary:** Empty tool output is replaced with "(see attached image)" even when no image exists, causing the model to hallucinate attachments.
- **Why it matters:** This latent bug was exposed by `pi-hashline-edit-pro`; fix PR #6290 landed, but the root cause affected all providers.
- [GitHub](https://github.com/earendil-works/pi/issues/6103)

### #6362 — Paste counter not reverted when pasted content is removed
- **Author:** affanali2k3 | **Comments:** 4 | **Status:** CLOSED
- **Summary:** Deleting a paste marker (e.g., `[Paste #2 +12 lines]`) then pasting again produces `[Paste #3 ...]` instead of recycling #2.
- **Why it matters:** Small UX regression that pollutes history with monotonically increasing unused paste indices.
- [GitHub](https://github.com/earendil-works/pi/issues/6362)

### #6376 — Thinking blocks improperly stripped in newer Claude models
- **Author:** leegmoore | **Comments:** 3 | **Status:** OPEN
- **Summary:** Models like Claude Sonnet 5 and Opus 4.8 have thinking blocks removed in subsequent API calls because Anthropic now omits the thinking field.
- **Why it matters:** Affects the brand-new Claude model tier; could break reasoning-dependent workflows until the strip logic is updated.
- [GitHub](https://github.com/earendil-works/pi/issues/6376)

### #6325 — Friendlier local extension identification
- **Author:** Josephur | **Comments:** 3 | **Status:** CLOSED
- **Summary:** Locally installed extensions show raw file paths (e.g., `D:\pi-web-agent`) instead of a friendly name in the startup extension list.
- **Why it matters:** Friction for extension developers prototyping locally—hard to distinguish extensions at a glance.
- [GitHub](https://github.com/earendil-works/pi/issues/6325)

### #6366 — Support session IDs for OpenRouter cache keys
- **Author:** farid-fari | **Comments:** 2 | **Status:** OPEN
- **Summary:** Pi sends `session_id` header and `prompt_cache_key` JSON key, but OpenRouter expects `x-session-id` header or `session_id` in body.
- **Why it matters:** Cache misses for all OpenRouter users; reduces performance and increases costs.
- [GitHub](https://github.com/earendil-works/pi/issues/6366)

### #6250 — Ctrl+V image paste silently fails on Linux/X11 in Bun release binary
- **Author:** Camboo92 | **Comments:** 2 | **Status:** OPEN
- **Summary:** Native clipboard binding `@mariozechner/clipboard` throws "Cannot find native binding" inside compiled Bun executable. Works in 0.78.0, broken in 0.80.3.
- **Why it matters:** Regression blocking Linux image paste—critical for screenshot-based workflows.
- [GitHub](https://github.com/earendil-works/pi/issues/6250)

### #6363 — Add extension/RPC event for "agent run fully settled / idle"
- **Author:** wasd171 | **Comments:** 2 | **Status:** OPEN
- **Summary:** Request for an `agent_idle` event distinct from `agent_end`, which fires even on errors.
- **Why it matters:** Enables extensions (e.g., status sync to Warp) to reliably detect when the agent completes successfully.
- [GitHub](https://github.com/earendil-works/pi/issues/6363)

### #6359 — TUI segfaults on small-ICU Node builds (Intl.Segmenter null deref)
- **Author:** T0mSIlver | **Comments:** 2 | **Status:** CLOSED
- **Summary:** RHEL Node.js without `nodejs-full-i18n` segfaults because `Intl.Segmenter` is null. JSON mode works fine.
- **Why it matters:** Hard crash on constrained environments; simple null-check missing.
- [GitHub](https://github.com/earendil-works/pi/issues/6359)

### #6380 — Extension lifecycle inconsistent on restart/resume vs /new
- **Author:** 729902288 | **Comments:** 1 | **Status:** CLOSED
- **Summary:** Extensions placed in `~/.pi/agent/extensions/` are loaded on restart but not on `/new` without a full restart.
- **Why it matters:** Surprising behavior for users who expect filesystem changes to be picked up mid-session.
- [GitHub](https://github.com/earendil-works/pi/issues/6380)

---

## 4. Key PR Progress

### #6341 — feat(ai): support constrained sampling
- **Author:** mitsuhiko | **Status:** OPEN
- **Summary:** Adds `constrainedSampling` config for tools to request JSON-schema-constrained tool input generation (exposed as `strict` on many providers).
- **Why it matters:** Opens the door to deterministic, format-safe tool calls—potentially eliminates malformed JSON issues.
- [GitHub](https://github.com/earendil-works/pi/pull/6341)

### #6285 — fix(agent): fail tool calls from length-truncated assistant messages
- **Author:** mitsuhiko | **Status:** OPEN
- **Summary:** Treats `length` stop reason as an error for tool execution; streamed arguments get best-effort salvage parsing.
- **Why it matters:** Prevents silent data loss when truncated messages produce incomplete tool calls.
- [GitHub](https://github.com/earendil-works/pi/pull/6285)

### #6350 — feat(coding-agent): add before_provider_headers extension hook
- **Author:** pmateusz | **Status:** CLOSED (merged)
- **Summary:** New extension hook lets extensions add, override, or remove HTTP headers on outgoing provider requests.
- **Why it matters:** Enables integration with LLM gateways, custom auth, and proxy headers.
- [GitHub](https://github.com/earendil-works/pi/pull/6350)

### #6290 — fix(ai): use "(no tool output)" placeholder for empty tool results without images
- **Author:** tzwm | **Status:** CLOSED (merged)
- **Summary:** Fixes #6103—replaces hallucinated "(see attached image)" with accurate "(no tool output)" when no image is present.
- **Why it matters:** Eliminates a source of model confusion and false image references.
- [GitHub](https://github.com/earendil-works/pi/pull/6290)

### #6352 — fix(coding-agent): correct cache hit rate denominator and context token double-count
- **Author:** keeplearning2026 | **Status:** CLOSED (merged)
- **Summary:** Fixes two places where Anthropic's `input_tokens` (which already includes cache sub-fields) was double-counted, inflating CH% and context%.
- **Why it matters:** Accurate token metrics are critical for cost tracking and debugging.
- [GitHub](https://github.com/earendil-works/pi/pull/6352)

### #6343 — fix(ai,agent,coding-agent): normalize null message content at ingestion boundaries
- **Author:** mitsuhiko | **Status:** CLOSED (merged)
- **Summary:** Guards against null `content` fields in messages across multiple packages, fixing recurring crash reports.
- **Why it matters:** Addresses long-standing flaky crashes (#6259, #6276, #4909, etc.).
- [GitHub](https://github.com/earendil-works/pi/pull/6343)

### #6309 — Improve project-local pi config
- **Author:** mitsuhiko | **Status:** CLOSED (merged)
- **Summary:** Makes `pi config` open global config by default, with `-l` for project-local; enables resource overrides without touching `settings.json`.
- **Why it matters:** Simplifies per-project tool/model selection—a top newbie pain point.
- [GitHub](https://github.com/earendil-works/pi/pull/6309)

### #6356 — fix(ai): support GLM-5.2 tool calls
- **Author:** hjotha | **Status:** CLOSED (merged)
- **Summary:** Falls back to non-streaming chat completion when tools are present for GLM-5.2, since streamed responses miss tool-call deltas.
- **Why it matters:** Enables tool usage on GLM-5.2, unblocking Chinese-language users.
- [GitHub](https://github.com/earendil-works/pi/pull/6356)

### #6349 — feat(coding-agent): add tool result limiter extension example
- **Author:** karsten-bot | **Status:** CLOSED (merged)
- **Summary:** Example extension that limits tool result sizes to prevent context overflow.
- **Why it matters:** Provides a reference implementation for extension authors tackling context window management.
- [GitHub](https://github.com/earendil-works/pi/pull/6349)

### #5472 — feat(ai,coding-agent): add Requesty as native provider
- **Author:** Thibaultjaigu | **Status:** CLOSED (merged)
- **Summary:** Registers Requesty.ai as a first-class provider with 60K+ user base; eliminates need for generic OpenAI endpoint configuration.
- **Why it matters:** Streamlines setup for a popular gateway, improves discoverability.
- [GitHub](https://github.com/earendil-works/pi/pull/5472)

---

## 5. Feature Request Trends

- **Hook & event system expansion:** Multiple requests for new lifecycle hooks—`before_provider_headers` (#6350), `agent_idle` (#6363), `unknownToolResolver` (#6368), deferred extension loading (#6360). The extension API is growing quickly, and the community wants more integration points.

- **Provider coverage & polish:** Doubao (#6328), Requesty (#5472), and WebSocket support for Azure OpenAI (#6372) show demand for broader native provider support. OpenRouter-specific features (server tools #6365, session IDs #6366) suggest users want first-class treatment of gateway features.

- **Session-scoped and local configuration:** Persistent requests for session-local model overrides (#6375) and project-local config (#6305, #6309). Users want to switch models or resources without touching global `settings.json`.

- **Better local development experience:** Friendlier extension identification (#6325), LAN auto-discovery of local model servers (#6305), and consistent extension lifecycle (#6380) all point to growing demand for smoother local dev and self-hosting workflows.

---

## 6. Developer Pain Points

- **Extension lifecycle confusion:** Inconsistent scanning of `~/.pi/agent/extensions/` between restart and `/new` (#6380), plus eager loading that slows startup with many extensions (#6360), create friction for extension developers.

- **Clipboard & image handling fragility:** Regression on Linux X11 (#6250), silent failures with pasted images to LLMs (#6373), and image path confusion (#6103) show clipboard support is brittle across platforms.

- **Cache token accounting errors:** Two separate issues (#6355, #6353) reported the same double-counting bug within hours, indicating this was a live problem affecting user trust in token consumption displays. Fix #6352 landed quickly, but the pattern of multiple independent reporters suggests monitoring gaps.

- **Model catalog metadata drift:** Thinking level mapping missing for new Claude models (#6376, #6371) and incorrect reasoning metadata across providers (#6374) show the catalog is struggling to keep pace with rapid model releases.

- **Hard crashes on edge-case environments:** Small-ICU Node segfaults (#6359) and native binding failures in Bun binaries (#6250) highlight gaps in cross-platform testing, especially for Linux users on minimal or older setups.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-07

## Today's Highlights

The Qwen Code community remains highly active with 36 open issues and 50 PRs updated in the last 24 hours. A **nightly release v0.19.6** was published with a strengthened PR triage gate that adds batch detection and red-flag pattern checks. The most discussed issue (#3203) about OAuth free-tier reduction has accumulated 149 comments, while the team is making progress on multi-workspace daemon support (RFC #6378) and fixing a critical zombie-session token drain bug (#5964).

## Releases

**v0.19.6-nightly.20260707.bcdb44c5d** — [GitHub](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.6-nightly.20260707.bcdb44c5d)
- Strengthened PR triage gate with batch detection, problem existence check, and red flag patterns (by @pomelo-nwu)

## Hot Issues

1. **[#3203 — OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** (149 comments)  
   Long-running discussion about reducing daily free quota from 1,000 to 100 requests/day and phasing out the free entry point. Community reaction is mixed, with heavy debate about the impact on hobbyist and evaluation users.

2. **[#6378 — RFC: Support Multiple Workspaces in One Daemon](https://github.com/QwenLM/qwen-code/issues/6378)** (19 comments)  
   A formal RFC for allowing a single `qwen serve` daemon to manage multiple workspaces. This is a foundational architecture change that would enable better resource sharing and session management. The community is positive, with implementation already underway in PR #6410.

3. **[#6264 — /review Skill Consumes Large Token Amounts](https://github.com/QwenLM/qwen-code/issues/6264)** (6 comments)  
   Users report that the code review skill burns through tokens excessively. Attached screenshots show unexpectedly high consumption, flagged as P2 performance bug awaiting more information.

4. **[#5964 — Zombie Sessions Burning 30M Tokens](https://github.com/QwenLM/qwen-code/issues/5964)** (5 comments)  
   A critical P1 bug where long-running agent sessions (zombie sessions) continue consuming tokens without being logged. User reports a "深夜惊魂" (midnight scare) scenario where a session ran 8 hours unattended. Multiple labels suggest this is ready for agent-assisted fix.

5. **[#6312 — Reduce Per-Session Overhead on Daemon Session Creation](https://github.com/QwenLM/qwen-code/issues/6312)** (5 comments)  
   Tracking issue for optimizing the session-creation path in the daemon. Each `session/new` re-runs synchronous I/O unnecessarily; this is a performance enhancement aligned with the multi-workspace work.

6. **[#6338 — Stabilize Tool Schema Order to Avoid Prompt Cache Misses](https://github.com/QwenLM/qwen-code/issues/6338)** (4 comments, CLOSED)  
   Tool declaration order can vary due to async MCP discovery, causing prompt cache misses. Community welcomed the fix as it improves latency for repeat queries.

7. **[#6311 — AutoMemory Cursor Advances on Failed Agent Extractions](https://github.com/QwenLM/qwen-code/issues/6311)** (3 comments, CLOSED)  
   When a forked agent hallucinates a tool call, the memory extraction cursor still advances, permanently skipping items. Fixed by PR #6398.

8. **[#6214 — Garbled Shell Output on Windows with Non-UTF-8 Code Pages](https://github.com/QwenLM/qwen-code/issues/6214)** (3 comments)  
   Windows users with non-UTF-8 console code pages get garbled text from `run_shell_command`. This is part of a broader Windows pain point (see also #6298, #6390).

9. **[#6408 — Large PDF Reads Overflow Prompt Context](https://github.com/QwenLM/qwen-code/issues/6408)** (2 comments)  
   Text-only models can blow context when reading 100-page PDFs (100k characters). The suggested fix adds a text length budget; PR #6409 implements a bounded read policy.

10. **[#6401 — ProxyAgent Does Not Support NO_PROXY](https://github.com/QwenLM/qwen-code/issues/6401)** (2 comments, CLOSED)  
    The `ProxyAgent` implementation unconditionally proxies all requests, ignoring `NO_PROXY` environment variables. This is a regression for enterprise users with internal-only services.

## Key PR Progress

1. **[#6398 — Fix AutoMemory Cursor Advance on Zero Tool Calls](https://github.com/QwenLM/qwen-code/pull/6398)** (CLOSED)  
   Fixes #6311. The extract cursor no longer advances when the forked agent makes zero real tool calls. Prevents permanent memory gaps from hallucinated commands.

2. **[#6409 — Gate Large PDF Text Extraction](https://github.com/QwenLM/qwen-code/pull/6409)** (OPEN)  
   Adds a PDF read budget policy so full-document extraction doesn't overflow prompt context. Large PDFs return guidance to use the `pages` parameter instead.

3. **[#6410 — Phase 2a Multi-Workspace Foundation](https://github.com/QwenLM/qwen-code/pull/6410)** (CLOSED)  
   First concrete step toward RFC #6378. Makes `--workspace` repeatable at the CLI parser boundary, rejects invalid combinations, and sets the stage for multi-workspace sessions.

4. **[#6404 — Support Large Text Range Reads](https://github.com/QwenLM/qwen-code/pull/6404)** (OPEN)  
   Adds bounded line-range reads for large text files instead of rejecting everything above 10MB. Preserves encoding metadata and forwarding cancellation.

5. **[#6400 — Session Overview Panel and Split View](https://github.com/QwenLM/qwen-code/pull/6400)** (OPEN)  
   Adds a web-shell Session Overview panel (mission control) and in-window split view for managing multiple daemon sessions. Includes session cards ranked by status.

6. **[#6390 — Avoid Unix Pager Default on Windows](https://github.com/QwenLM/qwen-code/pull/6390)** (OPEN)  
   Makes shell pager default platform-aware: Unix defaults to `cat`, Windows leaves `PAGER` unset. Fixes `run_shell_command` failures on Windows (related to #6298).

7. **[#6389 — Run Each Scheduled Task in Its Own Session](https://github.com/QwenLM/qwen-code/pull/6389)** (OPEN)  
   Scheduled tasks now mint dedicated, named sessions. Each session's transcript becomes the task's run history, improving auditability.

8. **[#6377 — Block Kill Commands Using pgrep Substitution](https://github.com/QwenLM/qwen-code/pull/6377)** (OPEN)  
   Fixes #6246. Adds a guard against `kill -9 $(pgrep node)` patterns that could kill Qwen Code itself. Extends the existing `detectSelfKillCommand` check.

9. **[#6372 — Add tools.visible Config for Deferred Tool Visibility](https://github.com/QwenLM/qwen-code/pull/6372)** (OPEN)  
   Implements the `tools.visible` setting requested in #6368. Users can now promote select deferred tools (e.g., `web_fetch`) to visible-at-startup without `tool_search`.

10. **[#6357 — Handle Missing Web-Shell Sessions Without Redirecting](https://github.com/QwenLM/qwen-code/pull/6357)** (CLOSED)  
    Improves UX when a session expires or is missing. Shows a minimal empty state with a "start new session" button instead of a confusing redirect.

## Feature Request Trends

- **Multi-workspace daemon support** (#6378, #6410): The top architectural request. Users want one daemon process to manage multiple workspaces efficiently, reducing memory and startup overhead.
- **Configurable tool visibility** (#6368, #6372): Users want to control which deferred tools are immediately visible to the LLM without requiring `tool_search`, reducing latency for common tools.
- **Session persistence and recovery** (#6259, #6389): Growing demand for session artifacts to survive daemon restarts, and for scheduled tasks to have dedicated session histories.
- **Platform parity (Windows)** (#6214, #6298, #6390): Multiple issues and PRs address Windows-specific shell compatibility, indicating a significant Windows user base.
- **Bounded file reads** (#6403, #6404, #6408): Users need smart truncation for large files (PDFs, logs) instead of hard rejections, with line-range or page-based access.

## Developer Pain Points

- **Token runaway / zombie sessions** (#5964): The most critical developer pain point. Long-running sessions can silently burn through API budgets without logging or automatic termination. Users report "midnight scares" with thousands of tokens wasted.
- **Windows shell compatibility** (#6214, #6298): The `run_shell_command` tool fails on Windows due to Unix-only commands (`cat`) and encoding issues. Multiple PRs (#6390, #6377) are in flight but not yet merged.
- **Proxy and environment configuration** (#6401): The `NO_PROXY` directive being ignored breaks enterprise setups where internal services should bypass the proxy.
- **Model context overflows** (#6384, #6408): Users hit "Context is too large to send safely" errors from PDF reads and env-configured models with misaligned context windows. The `hard limit: 0` case (#6384) is particularly confusing.
- **Triage bot reliability** (#6365, #6396): The automated PR triage and review bot has been fabricating policy thresholds and downgrading approvals, eroding trust in CI automation.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-07

## Today's Highlights

The v0.8.67 release cycle dominates the project board, with 20+ open issues filed in a single burst from the maintainer's review/rebuild prompt. A critical **SIGPIPE crash bug** (#4030) has already landed a fix PR, while the broader release focuses on sub-agent reliability, UI polish, and constitution customization. No new releases were published in the last 24 hours.

## Releases

No new releases in the last 24 hours. The v0.8.67 release candidate was merged via PR #4047 but appears to be undergoing post-merge QA before official tagging.

---

## Hot Issues

### 🔴 Release-Blocker & Reliability

1. **[#4061 — v0.8.67 tracker: convert review/rebuild prompt into issue-driven release work](https://github.com/Hmbown/CodeWhale/issues/4061)**  
   The main tracking issue for the v0.8.67 release pass. 20+ child issues were created from a single review prompt. Community reaction: all by the maintainer; signals a structured but heavy-handed release process.

2. **[#4030 — Bug: panic on broken pipe (SIGPIPE) when piping output](https://github.com/Hmbown/CodeWhale/issues/4030)**  
   `codewhale doctor | head` triggers a crash dump with broken pipe. Developer pain point: basic Unix pipe hygiene. PR #4043 already has a fix by resetting `SIGPIPE` to `SIG_DFL`. **Critical for any shell power user.**

3. **[#4050 — Sub-agents must not complete successfully with empty child output](https://github.com/Hmbown/CodeWhale/issues/4050)**  
   A child sub-agent can finish on a tool call or max-steps without producing a summary, yet the runtime reports success. This is a fundamental reliability issue for agentic workflows. Zero comments but high severity.

### 🔴 Sub-Agent & Workflow Runtime

4. **[#4049 — Delegate sub-agents misroute DeepSeek model/provider and fail](https://github.com/Hmbown/CodeWhale/issues/4049)**  
   Dogfood finding: delegated builder sub-agents using DeepSeek config fail with model-not-found, suggesting the model/provider route is corrupted during delegation. Community: zero comments, but identified by the maintainer during active dogfooding.

5. **[#4052 — `worktree=true` should discover nested repos from harness directories](https://github.com/Hmbown/CodeWhale/issues/4052)**  
   When the session CWD is a parent harness directory containing nested repos, `worktree=true` fails to discover the actual repository. Blocks developers who manage multi-repo projects from parent directories.

6. **[#4053 — Token-budget exhaustion should be managed failure/recovery, not raw text](https://github.com/Hmbown/CodeWhale/issues/4053)**  
   Sub-agents that hit token limits dump raw completion text to the user instead of entering a managed failure/recovery path. UI/UX reliability issue, especially during long-running agent tasks.

### 🟡 TUI & UX Quality

7. **[#4063 — Setup wizard step bodies are not scrollable at 80x24](https://github.com/Hmbown/CodeWhale/issues/4063)**  
   Long setup steps are unreadable on standard terminals. `Up`/`Down` only navigates between steps; no `PageUp`/`PageDown` or body scroll offset. Basic TUI usability gap.

8. **[#4062 — First-run onboarding hardcodes the DeepSeek provider](https://github.com/Hmbown/CodeWhale/issues/4062)**  
   Non-DeepSeek API keys land in the DeepSeek slot during onboarding, contradicting the project's stated "every provider first-class" principle. Community reaction: zero comments, but flagged as a contradiction of documented design principles.

### 🟡 Model & Configuration

9. **[#4058 — Refresh model catalog, pricing, provider labels from current sources](https://github.com/Hmbown/CodeWhale/issues/4058)**  
   The `/model` picker shows stale pricing, missing models, and many `price unknown` entries. Important for users who rely on cost-aware model selection. Noted as "important but not blocking for v0.8.67."

10. **[#4042 — Environment-level tool sandboxing for sub-agents](https://github.com/Hmbown/CodeWhale/issues/4042)**  
    Request to enforce tool restrictions across sessions, sub-agents, Fleet workers, and MCP servers. The `--disallowed-tools` flag exists but isn't consistently enforced across all execution contexts. Community: 9 comments, active discussion about boundary design.

---

## Key PR Progress

### ✅ Merged/Closed

1. **[#4047 — Release 0.8.67 — Fleet/Workflow usability, goal-timer fix, rename](https://github.com/Hmbown/CodeWhale/pull/4047)**  
   Merged to `main`. Includes whaleflow→workflow rename, goal-timer fix. Fast-forward clean against main. **Note:** branch name is legacy; content targets 0.8.67.

2. **[#4046 — Layer 5.1: User command registry and loading boundary](https://github.com/Hmbown/CodeWhale/pull/4046)**  
   Closed as no code changes needed — the boundary already exists and is covered by focused tests. Clean verification PR.

### 🟢 Active & New

3. **[#4044 — fix(onboarding): localize dynamic welcome steps](https://github.com/Hmbown/CodeWhale/pull/4044)**  
   Localizes the first-run welcome screen through the existing `MessageId` registry. Adds welcome copy for every shipped locale including sparse `zh-Hant`. Addresses localization gaps flagged in issue #4057.

4. **[#4043 — fix(cli): reset SIGPIPE to SIG_DFL for clean piped exit](https://github.com/Hmbown/CodeWhale/pull/4043)**  
   Fixes #4030. Resets `SIGPIPE` to `SIG_DFL` so early-exit pipe consumers don't trigger a panic. **Should be high priority to merge.**

5. **[#4045 — fix edit_file UTF-8 fuzzy cursor panic](https://github.com/Hmbown/CodeWhale/pull/4045)**  
   Fixes fuzzy matching when a normalized match starts on a multibyte UTF-8 character (e.g., CJK). The cursor advance used `norm_start + 1`, causing index panics. Important for international users.

### 🟡 Held/Deferred

6. **[#3969 — Add per-sub-agent provider routing](https://github.com/Hmbown/CodeWhale/pull/3969)**  
   Held for **v0.8.68** per maintainer. Will be rebased onto the new fleet taxonomy PRs (#3932–#3935). Approach was not rejected — just out of sequence.

---

## Feature Request Trends

1. **Multi-Provider First-Class Support**  
   Multiple issues (#4062, #4049, #4042) highlight that DeepSeek is still privileged in onboarding, routing, and tool enforcement despite the stated "all providers equal" principle. The community expects genuine provider-agnostic architecture.

2. **Sub-Agent Reliability & Observability**  
   Requested: empty output detection (#4050), token-budget managed recovery (#4053), delegate card timeline correctness (#4051), nested repo discovery (#4052). The sub-agent workflow runtime is the single most active area of feature work.

3. **Constitution Customization**  
   Issues #4064 and #4032 point to a desire for user-customizable agent constitutions, moving from the current 607-line prompt to a `~55` line core with editable overrides. A CLI and TUI customization stack was built but needs rebasing.

4. **Language/Internationalization Parity**  
   Issues #4057 and PR #4044 show movement toward full locale parity, with `zh-Hant` explicitly scoped as partial. The community expects all shipped locales to be complete or clearly labeled.

5. **Model Catalog Freshness**  
   Issue #4058 asks for live-updated model catalogs with current pricing and provider labels. Stale model information undermines cost-aware workflow decisions.

---

## Developer Pain Points

1. **Panic on Piped Output (SIGPIPE)** — #4030  
   A basic Unix pipe scenario (`cmd | head`) panics the entire process. Fundamental robustness gap for shell integration.

2. **Empty Sub-Agent Success Reports** — #4050, #4053  
   Agents that finish due to tool errors, max-steps, or token exhaustion report success with empty output. Destroys trust in agentic workflows; users cannot distinguish real completion from silent failure.

3. **Model/Provider Routing Silently Breaks on Delegation** — #4049  
   A working session configuration produces different behavior when delegated to sub-agents. The model-not-found error suggests configuration is lost or corrupted during routing.

4. **First-Run Experience is DeepSeek-Locked** — #4062  
   Non-DeepSeek users are forced through a DeepSeek-centric onboarding flow, contradicting stated design principles and causing confusion.

5. **Unscrollable Setup Wizard on Standard Terminals** — #4063  
   At 80x24, long setup steps are unreadable. This is a basic TUI usability failure that affects every new user on conventional terminal sizes.

6. **Stale Model Catalog with "price unknown" Entries** — #4058  
   Developers relying on cost-aware model selection face stale or missing data. The `/model` picker's accuracy degrades over time without a refresh mechanism.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*