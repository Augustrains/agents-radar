# AI CLI Tools Community Digest 2026-07-02

> Generated: 2026-07-02 02:00 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Date:** 2026-07-02 | **Prepared for:** Technical Decision-Makers

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem on July 2, 2026, reflects a landscape in active maturation, with eight major tools undergoing distinct phases of development. Claude Code and OpenAI Codex dominate community activity and issue volume, while Gemini CLI and OpenCode are in rapid feature-development sprints. A clear bifurcation is emerging: established tools (Claude Code, Codex) are grappling with quality regressions and security calibration post-feature bloat, while mid-tier tools (Gemini CLI, OpenCode, Qwen Code) are investing in foundational architecture — sandboxing, multi-agent orchestration, and V2 migrations. Emerging tools like Pi and CodeWhale are gaining traction through extension ecosystems and constitution-based safety models, signaling a shift toward user-configurable agent governance. Windows reliability remains the single largest cross-cutting pain point, with every tool reporting platform-specific failures that undermine developer trust.

---

## 2. Activity Comparison

| Tool | Open Issues (approx.) | PRs (24h) | Release Status | Community Signal |
|------|----------------------|-----------|----------------|------------------|
| **Claude Code** | 10 highlighted + duplicates | 2 open | v2.1.198 shipped | 📉 High friction (safety, Windows, regression wave) |
| **OpenAI Codex** | 10 highlighted, ~73000 total | 10 active | Two Rust alpha releases | 📈 Heavy security hardening, Windows crisis |
| **Gemini CLI** | 10 highlighted | 10 open | v0.51.0-nightly (symlink escape fix) | 📈 Active security/architecture work |
| **GitHub Copilot CLI** | 10 highlighted | 0 new | v1.0.69-0 shipped | 📉 Quiet release, stable but slow iteration |
| **Kimi Code** | 8 highlighted | 1 open (PR #2481) | None in 24h | 📉 Low activity, branding migration incomplete |
| **OpenCode** | 10 highlighted | 10 active | v1.17.13 shipped | 📈 V2 migration sprint, high feature velocity |
| **Pi** | 10 highlighted | 10 merged/active | None in 24h | 📈 AOT compilation, extension infrastructure |
| **Qwen Code** | 10 highlighted | 10 active | v0.19.4 + nightly | 📈 High PR throughput, channel adapter focus |
| **CodeWhale (DeepSeek TUI)** | 10 highlighted | 10 active | Pre-v0.8.67 | 📈 Heavy setup-wizard/cleanup before release |

**Key Observations:**
- **Highest issue volume:** OpenAI Codex (~73,000 total issues) and Claude Code show the most community friction.
- **Highest PR velocity:** Qwen Code, OpenCode, and Gemini CLI each have 10 active PRs.
- **Lowest activity:** Copilot CLI (0 PRs) and Kimi Code (1 PR) — both appear to be in maintenance or slow-iteration phases.
- **Release cadence leader:** Qwen Code shipped two releases today; Claude Code and OpenCode each shipped one.

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating genuine market demand:

### a) Windows Platform Parity
- **Affected tools:** Claude Code, OpenAI Codex, Copilot CLI, Kimi Code, OpenCode, CodeWhale
- **Common issues:** Orphan process locks, path separator mismatches (OpenCode #21340), terminal flickering (Copilot CLI #3984), sandbox launch failures (Codex #29072), WSL focus-stealing (Claude Code #73075), clipboard binary loss (Kimi Code PR #2481)
- **Signal:** Windows is universally treated as a second-class platform; this is the #1 cross-tool developer pain point.

### b) Multi-Agent Orchestration & Subagent Transparency
- **Affected tools:** Claude Code, Gemini CLI, Kimi Code, OpenCode, CodeWhale
- **Common needs:** Per-subagent model configuration (Claude Code #73072), subagent success-reporting accuracy (Gemini #22323), API key pooling for parallel agents (Kimi PR #2369), sub-agent state persistence (CodeWhale #3864)
- **Signal:** Multi-agent is moving from feature to reliability problem — tools need transparent lifecycle and honest termination reports.

### c) MCP (Model Context Protocol) Ecosystem Maturity
- **Affected tools:** Claude Code, Copilot CLI, OpenCode, Pi, Qwen Code
- **Common issues:** OAuth flow mismatches (Copilot CLI #3982), SSRF gaps in discovery (Gemini #28112), broken connectors after patch releases (Claude Code #73081), dynamic MCP server startup from chat (CodeWhale PR #3866)
- **Signal:** MCP is becoming the standard integration layer, but implementations are fragile and authentication patterns are inconsistent.

### d) Safety/Filter Calibration for Legitimate Work
- **Affected tools:** Claude Code (AUP false positives, ~10 duplicates in one day), Gemini CLI (thought leakage, #27971), OpenCode, CodeWhale (constitution-based permission models)
- **Common demand:** Better override mechanisms for authorized security audits, reverse-engineering, and self-hosted infrastructure work.
- **Signal:** One-size-fits-all safety filtering is breaking legitimate use cases; users want context-aware, configurable guardrails.

### e) Long-Running Task & Goal Management
- **Affected tools:** Claude Code, Kimi Code, Copilot CLI, OpenCode
- **Common needs:** Auto-saving long goals to file (Kimi #2482), persistent long-running agent sessions, goal length limits, pause/resume capabilities
- **Signal:** As agents tackle more complex tasks, session survivability and goal persistence become critical.

---

## 4. Differentiation Analysis

| Tool | Core Differentiator | Target User | Technical Approach |
|------|--------------------|-------------|-------------------|
| **Claude Code** | Anthropic safety architecture + Claude in Chrome GA | Enterprise developers, security-conscious teams | Proprietary model + MCP connectors + Cowork collaboration |
| **OpenAI Codex** | GPT-5.x model access + Rust toolchain alpha | Power users, early adopters of latest OpenAI models | Multi-language agent runtime, sandboxed execution |
| **Gemini CLI** | Google ecosystem integration + AST-aware tooling | Cloud-native developers, GCP users | Multi-agent orchestration, memory import/export, Caretaker automation |
| **GitHub Copilot CLI** | GitHub ecosystem lock-in | GitHub-heavy development teams | Plugin architecture, sandbox mode, model flexibility |
| **Kimi Code** | Moonshot AI (Chinese market) | Asian developer ecosystem | API key pooling for parallelism, goal-based workflows |
| **OpenCode** | Copilot-compatible, open-codebase alternative | Community-driven devs, V2 migration adopters | Promise-based client, progressive agent loading, customizable review panel |
| **Pi** | TypeScript extension system + multi-provider support | Extension developers, local-model users | AOT compilation (esbuild), SQLite storage, provider catalogue |
| **Qwen Code** | Channel adapters (Telegram, WeChat, QQ Bot) | Multi-platform developers, messaging-first workflows | Daemon architecture, channel-specific lifecycle, tool execution timeouts |
| **CodeWhale (DeepSeek TUI)** | Constitution-based safety + rebrand momentum | Privacy-conscious users, TUI enthusiasts | Staged permission model, ModalShell UI, dynamic MCP |

**Strategic Takeaways:**
- **Model differentiation is commoditizing** — nearly every tool supports multiple model providers (BYOK, Copilot, Ollama, Bedrock).
- **Platform differentiation is the new battleground** — OpenCode (Copilot-compatible alternative), Pi (extension ecosystem), Qwen Code (channel adapters), and CodeWhale (constitution-first) each compete on architecture and workflow philosophy, not model exclusivity.
- **Enterprise readiness cluster vs. indie/power-user cluster** — Claude Code, Codex, Gemini, and Copilot target structured teams; Kimi, Pi, Qwen, and CodeWhale target individual power users and niche workflows.

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
| Tool | Signal |
|------|--------|
| **OpenCode** | V2 migration with ~20 new feature issues in 72 hours; 10 active PRs; rapid response to Windows path bugs (2 PRs merged today) |
| **Qwen Code** | Two releases today; 50 issues + 50 PRs updated in 24h; channel adapter specialization attracting multi-platform developers |
| **CodeWhale** | Heavy pre-release activity (10+ PRs); constitution-first safety model generating strong community engagement (14 comments on #3275) |
| **Pi** | AOT compilation for extensions (#6213) landed; 10 PRs closed/active; extension ecosystem momentum |

### Stable / Mature
| Tool | Signal |
|------|--------|
| **GitHub Copilot CLI** | Two releases this week but 0 PRs today; feature requests slow; community primarily filing bugs, not shaping direction |
| **Claude Code** | High issue volume but low PR activity (2 open); project in bugfix/maintenance phase rather than feature expansion |
| **OpenAI Codex** | Heavy security patch series from internal team; community participation is report-driven, not contribution-driven |

### Struggling / In Transition
| Tool | Signal |
|------|--------|
| **Kimi Code** | Half-done brand migration (#2483); 0 releases; only 1 external PR; long-standing bug #640 (6 months) unresolved — risk of community attrition |
| **Gemini CLI** | Active but P1 bugs (subagent false success #22323, agent hangs #21409) remain open; security fixes are emergency-driven rather than proactive |

**Community Maturity Index (Qualitative):**
1. **OpenCode** — Highest velocity; clear V2 roadmap; responsive PR merging
2. **Qwen Code** — Strong PR throughput; growing adapter ecosystem
3. **Claude Code** — Largest community but highest frustration; maintenance mode
4. **Codex** — Most issues; internal security focus; external contribution low
5. **Pi** — Extension ecosystem growing; contributor-friendly
6. **Gemini CLI** — Active but P1 bugs linger
7. **Copilot CLI** — Steady but quiet; no community-driven PRs today
8. **CodeWhale** — Pre-release surge; high engagement on constitution model
9. **Kimi Code** — At risk of stalling without maintainer intervention

---

## 6. Trend Signals

### For Developers Evaluating Tools

1. **Windows is still an afterthought.** Every major tool has Windows-specific reliability issues that are months old. If you develop on Windows, expect friction — prioritize tools with explicit Windows fixes in their changelogs (Copilot CLI v1.0.69-0, OpenCode's path normalization PRs).

2. **Multi-agent orchestration is becoming table stakes, but reliability is poor.** False success reports (Gemini #22323), hanging agents (Claude #21409), and silent failures are common. Tools that solve subagent transparency will win trust. OpenCode's progressive `AGENTS.md` loading and Pi's `excludeFromContext` are promising architectural approaches.

3. **Safety/security calibration is the most urgent unsolved problem.** Claude Code's AUP false-positive wave (10+ duplicates in hours) and CodeWhale's constitution-first approach represent opposite ends of the spectrum — one too restrictive, one empowering the user. The industry needs a middle ground: context-aware, policy-driven safety that respects authorized work.

4. **MCP is standardizing but fragile.** Every tool implements MCP slightly differently; OAuth patterns, SSRF protection, and connector reliability vary widely. Expect consolidation to a standard (likely Anthropic's or OpenCode's V2 implementation) within 6-12 months.

5. **Rust and TypeScript are the implementation languages of choice.** Codex (Rust alpha), CodeWhale (Rust), and Pi (TypeScript/AOT) show a move toward compiled or AOT-compiled tooling for performance. This will accelerate as context windows grow and latency becomes the differentiator.

6. **Local/first-class model support is bifurcating the market.** Pi and Qwen Code support local models (Ollama, llama.cpp) natively; Claude Code and Codex are cloud-only. The market is splitting between "agent-as-service" and "agent-as-toolkit" philosophies.

7. **Brand migration friction is real.** Kimi Code's incomplete rebrand and CodeWhale's lingering `.deepseek/` paths show that renaming tools mid-stream creates real developer confusion and state corruption. If you're evaluating a recently renamed tool, budget for migration cleanup.

8. **The gap between "feature-rich" and "reliable" is widening.** Claude Code and Codex ship features rapidly but accumulate regression debt (broken `/dataviz`, stale reply ordering, Windows sandbox crashes). Qwen Code and OpenCode prioritize reliability with slower feature adds. Choose based on your tolerance for churn vs. stability.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-02** | Source: [github.com/anthropics/skills](https://github.com/anthropics/skills)

---

## 1. Top Skills Ranking

The following pull requests have drawn the most community discussion and represent the most closely watched Skill submissions:

### #1 — skill-creator bugfix: `run_eval.py` always reports 0% recall
- **PR**: [#1298](https://github.com/anthropics/skills/pull/1298)
- **Author**: MartinCajiao | **Status**: OPEN
- **Description**: Identifies that the core evaluation script for the skill-creator toolchain (`run_eval.py`) reports `recall=0%` for every description, effectively rendering the description-optimization loop (used by `run_loop.py` and `improve_description.py`) noise-driven. Fixes include installing the eval artifact as a real skill, correcting Windows stream reading, trigger detection logic, and parallel worker handling. This is the most critical infrastructure fix in the repository, referenced across multiple related issues (#556, #1169, and 10+ independent reproductions).

### #2 — `document-typography` skill: typographic quality control
- **PR**: [#514](https://github.com/anthropics/skills/pull/514)
- **Author**: PGTBoos | **Status**: OPEN
- **Description**: Addresses orphan word wrap (1–6 words on a new line), widow paragraph headers, and numbering misalignment in AI-generated documents. The discussion highlights that these visual defects are pervasive across all Claude-generated documents and that users rarely request fixes explicitly.

### #3 — `odt` skill: OpenDocument text creation and template filling
- **PR**: [#486](https://github.com/anthropics/skills/pull/486)
- **Author**: GitHubNewbie0 | **Status**: OPEN
- **Description**: Provides full round-trip support for OpenDocument Format files (.odt, .ods), including creation, template filling, and conversion to HTML. Discussion centers on the demand for LibreOffice-compatible document workflows that do not depend on proprietary formats.

### #4 — `self-audit` skill: mechanical verification + four-dimension reasoning quality gate
- **PR**: [#1367](https://github.com/anthropics/skills/pull/1367)
- **Author**: YuhaoLin2005 | **Status**: OPEN (most recent top PR)
- **Description**: A universal skill that audits AI output before delivery. Step 0 performs mechanical file verification (ensuring all claimed output files exist). Step 1 executes a four-dimension reasoning audit in damage-severity priority order. Discussion emphasizes its model-agnostic design and applicability across any project or tech stack.

### #5 — `skill-quality-analyzer` and `skill-security-analyzer`
- **PR**: [#83](https://github.com/anthropics/skills/pull/83)
- **Author**: eovidiu | **Status**: OPEN
- **Description**: Two meta-skills for the marketplace: (1) a comprehensive quality analyzer evaluating Structure & Documentation (20%), (2) a security analyzer. Community interest reflects demand for governance and quality gates on the Skills ecosystem itself.

### #6 — `testing-patterns` skill
- **PR**: [#723](https://github.com/anthropics/skills/pull/723)
- **Author**: 4444J99 | **Status**: OPEN
- **Description**: Covers the full testing stack: Testing Trophy model philosophy, AAA pattern for unit tests, React Testing Library patterns, and what to test vs. what not to test. The broad scope and practical examples drove significant discussion.

### #7 — `sensory` skill: native macOS automation via AppleScript
- **PR**: [#806](https://github.com/anthropics/skills/pull/806)
- **Author**: AdelElo13 | **Status**: OPEN
- **Description**: Teaches Claude to use `osascript` (AppleScript) for native macOS automation as an alternative to screenshot-based computer use. Features a two-tier permission system (Tier 1: direct app scripting, Tier 2: Accessibility permissions). Discussion focused on platform-native automation strategies.

---

## 2. Community Demand Trends

Analysis of the most active **Issues** reveals the following concentrated demand directions:

### 🔴 **Critical: Skill-Creator Toolchain Reliability** (Issues #556, #1169, #1061)
The single most-reported problem: `run_eval.py` consistently reports 0% trigger/recall rates, making the description-optimization loop non-functional. Multiple users across platforms (Windows, macOS, Linux) have independently reproduced this. Windows compatibility issues compound the problem with subprocess, encoding, and pipe-handling failures. **This is the blocking issue for the entire skill-authoring workflow.**

### 🛡️ **Security & Governance** (Issue #492)
A high-impact concern: community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability where users may grant elevated permissions to skills they believe are official. This issue has the highest comment count (34) and reflects growing ecosystem maturity requirements.

### 🏢 **Enterprise & Organizational Features** (Issue #228)
Demand for org-wide skill sharing within Claude.ai (7 👍). Currently, users must manually download `.skill` files and share via Slack/Teams. A shared skill library or direct sharing link is the most requested enterprise feature.

### 🔄 **Duplicate Skill Conflicts** (Issue #189)
Installing both `document-skills` and `example-skills` plugins results in identical content, causing duplicate skills in the context window. This points to a need for better dependency management and deduplication in the plugin system.

### 🧠 **Agent Memory Optimization** (Issue #1329)
A proposal for `compact-memory`: symbolic notation to compress long-running agent notes and persistent memory, reducing context consumption while preserving state.

### 📋 **Other Notable Demands**
- **Bedrock compatibility** (Issue #29): Running Skills with AWS Bedrock
- **MCP exposure** (Issue #16): Exposing Skills as Model Context Protocol endpoints
- **SharePoint Online security** (Issue #1175): Security and context window concerns when handling SPO documents

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to land soon:

| Skill | PR | Description |
|-------|-----|-------------|
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Universal output auditing with mechanical verification + reasoning quality gate (v1.3.0) |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Comprehensive color knowledge: naming systems, color spaces (OKLCH, OKLAB, CAM16), accessibility |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full testing stack coverage: unit, React, integration, philosophy |
| **sensory** | [#806](https://github.com/anthropics/skills/pull/806) | Native macOS automation via AppleScript with tiered permissions |
| **skill-quality-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skill for quality and security analysis of other Skills |

The **self-audit** skill (#1367) is the most recently submitted and potentially most impactful, as it addresses the ecosystem's need for output verification that scales across any project and model.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for toolchain reliability — specifically fixing the skill-creator's evaluation loop (`run_eval.py`) which consistently reports 0% recall — and for security governance to prevent trust boundary abuse from community skills distributed under the official `anthropic/` namespace, followed by enterprise sharing capabilities and platform compatibility (Windows/Bedrock).**

---

# Claude Code Community Digest — 2026-07-02

## Today's Highlights
v2.1.198 ships with Claude in Chrome GA, background agent notifications, and a new `/dataviz` skill — but the `/dataviz` skill appears non-functional for some users, and a wave of false-positive safety blocks on legitimate security audits is generating significant community friction. Desktop SSH reconnection failures and a focus-stealing regression on Windows WSL are also drawing attention.

---

## Releases

### v2.1.198
- **Claude in Chrome** is now generally available
- **Background agent notifications** — sessions that need input or finish now fire the `Notification` hook (`agent_needs_input` / `agent_completed`)
- **`/dataviz` skill** for chart and dashboard design guidance

> ⚠️ **Community note:** Multiple users report that `/dataviz` doesn't appear in their skills list despite being advertised in release notes and startup screen ([#73078](https://github.com/anthropics/claude-code/issues/73078)). Likely a rollout or activation issue.

---

## Hot Issues

1. **[#42776](https://github.com/anthropics/claude-code/issues/42776) — Windows desktop relaunch broken by orphaned process file lock (96 comments, 👍39)**  
   *Long-standing bug:* After a crash or manual close, a stale process holds a file lock preventing relaunch. Highest-comment issue on the board, still unresolved after 3 months.

2. **[#38993](https://github.com/anthropics/claude-code/issues/38993) — Cowork: virtiofs FUSE mount serves stale files (34 comments, 👍25)**  
   *Linux VM pain:* Host-side file changes aren't reflected in the VM. A top-voted bug blocking Cowork adoption for Linux devs.

3. **[#38005](https://github.com/anthropics/claude-code/issues/38005) — RTL support for Hebrew & Arabic in Desktop/Cowork (31 comments, 👍66)**  
   *Most-upvoted enhancement:* Community strongly desires proper bidirectional text rendering. Labeled duplicate, but support continues to grow.

4. **[#61682](https://github.com/anthropics/claude-code/issues/61682) — GitHub connector "Connected" but no tools exposed in Cowork (11 comments)**  
   *Windows 11 gap:* The GitHub MCP connector shows green but offers zero tools — a blocking issue for workflow integration.

5. **[#73068](https://github.com/anthropics/claude-code/issues/73068) — AUP false positive blocks self-audit of own web server config (new today, 4 comments)**  
   Part of a **large cluster of ~10+ duplicate reports** from user `sworrl` today (e.g., [#73082](https://github.com/anthropics/claude-code/issues/73082), [#73065](https://github.com/anthropics/claude-code/issues/73065)). All describe legitimate security audits on the user's own infrastructure being halted by AUP or safety filters. **Severity: session-halted**. This is an emerging pattern.

6. **[#72423](https://github.com/anthropics/claude-code/issues/72423) — Desktop file viewer blocks files in `permissions.additionalDirectories` (👍3, closed)**  
   *Regression:* A recent change broke the ability to view files explicitly allowed in user config. Was closed, but the 👍 count suggests frustration.

7. **[#68992](https://github.com/anthropics/claude-code/issues/68992) — Background tasks stuck "running" forever in CLI (1 comment)**  
   *Windows CLI issue:* Background commands can hang permanently, blocking new messages and breaking `/feedback`. No response yet from maintainers.

8. **[#73080](https://github.com/anthropics/claude-code/issues/73080) — Model confabulates non-existent user request (new today)**  
   *Alarming hallucination:* `claude-opus-4-8` invented a user message and responded to it in Chinese after a long thinking cycle. Raises trust concerns.

9. **[#73079](https://github.com/anthropics/claude-code/issues/73079) — Desktop SSH remote stuck in permanent reconnect loop (new today)**  
   After auto-update to 1.17377.2 on macOS, SSH sessions enter an infinite `Unauthorized request: method=server.ping` loop. Wiping remote state doesn't help.

10. **[#73081](https://github.com/anthropics/claude-code/issues/73081) — Hosted MCP connectors broken in VS Code extension after v2.1.195 (new today)**  
    *Windows regression:* Slack/M365 connectors stopped injecting into VS Code chat. Broad impact for enterprise users relying on these connectors.

---

## Key PR Progress

*(Note: Only 2 open PRs at time of data collection)*

1. **[#72866](https://github.com/anthropics/claude-code/pull/72866) — Fix "Github" → "GitHub" typo in README**  
   Small docs fix. Low complexity, no tests needed.

2. **[#72543](https://github.com/anthropics/claude-code/pull/72543) — Create Cha**  
   Title is truncated/ambiguous. Likely a newbie PR. No description or comments.

> **Observation:** The PR queue is nearly empty. This may indicate the project is in a heavy bugfix/maintenance phase, or that the community is primarily reporting issues rather than contributing code.

---

## Feature Request Trends

1. **Per-subagent advisor configuration** ([#73072](https://github.com/anthropics/claude-code/issues/73072)) — Users want to assign different `advisorModel` to different subagents in multi-agent orchestration, rather than a single session-level advisor.

2. **RTL/BiDi text support** ([#38005](https://github.com/anthropics/claude-code/issues/38005), 👍66) — Strong demand for Hebrew, Arabic, and other right-to-left language rendering in both Desktop and Cowork modes.

3. **Localization of permission dialogs** ([#73076](https://github.com/anthropics/claude-code/issues/73076)) — Permission prompts always in English even when VS Code locale is Japanese. Signals demand for i18n beyond the UI chrome.

4. **Better safety filter calibration** — The flood of AUP/cyber false-positive reports today indicates users want clearer override mechanisms for authorized security work, and fewer false positives on self-audit and reverse-engineering tasks.

---

## Developer Pain Points

- **Safety filter false positives** — Multiple users (notably `sworrl`) report legitimate security audits of their own websites being session-halted. This is the **single biggest frustration of the day**, with ~10+ duplicate issues filed in hours. The community is raising the alarm that safety filters are too aggressive for legitimate work.

- **Windows-specific reliability:** Orphan process locks (#42776), WSL focus-stealing (#73075), GitHub connector failures (#61682), and stuck background tasks (#68992) paint a picture of Windows as a second-class platform.

- **SSH remote session fragility** — The permanent reconnect loop after auto-update (#73079) erodes trust in the remote workflow, which is critical for cloud/VM-based development.

- **Missing or delayed features** — `/dataviz` advertised but unavailable (#73078), MCP connectors broken by patch release (#73081), and model hallucination (#73080) all indicate quality regression in v2.1.198.

- **Long-standing bugs unresolved** — Issue #42776 (Windows relaunch) is 3 months old with 96 comments but no fix in sight. Community patience may be wearing thin for foundational platform issues.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — July 2, 2026

## Today's Highlights
A significant security-focused patch series is unfolding across the Codex codebase, with five PRs from a single author targeting Git filter, merge driver, and worktree containment vulnerabilities. Windows users continue to face the brunt of stability issues, including sandbox launch failures and persistent "Something went wrong" errors in the latest MSIX build. The long-standing request for a Linux desktop app (#11023) remains the most-upvoted open issue, now with 674 reactions and 138 comments.

---

## Releases
Two Rust alpha releases landed in the last 24 hours:

- **[rust-v0.143.0-alpha.32](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.32):** Base alpha release.
- **[rust-v0.143.0-alpha.33](https://github.com/openai/codex/releases/tag/rust-v0.143.0-alpha.33):** Subsequent alpha release with no detailed changelog.

Both appear to be incremental Rust toolchain builds without user-facing feature notes.

---

## Hot Issues (Top 10)

1. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)**  
   *Enhancement, App* | **674 👍, 138 comments**  
   The most-requested feature on the repository. Users report the macOS app is unusable due to power consumption (linked to #10432) and want a native Linux build. Community sentiment: high urgency for Linux-first developers.

2. **[#2847 — A way to exclude sensitive files](https://github.com/openai/codex/issues/2847)**  
   *Enhancement, Sandbox* | **456 👍, 91 comments** *(CLOSED)*  
   Request for `.codexignore`-style mechanisms to prevent agents from reading/sending sensitive files. Although closed, it set the precedent for the security-focused PRs appearing today.

3. **[#9203 — Please make "/undo" back](https://github.com/openai/codex/issues/9203)**  
   *Enhancement, TUI, Session* | **312 👍, 54 comments**  
   Users strongly miss the `/undo` command after unintentional file deletions/modifications in non-git-tracked contexts. High frustration: "It bites me several times in recent days."

4. **[#8648 — Codex replies to earlier messages instead of latest](https://github.com/openai/codex/issues/8648)**  
   *Bug, Context, Agent* | **55 👍, 71 comments**  
   A perplexing conversation-ordering bug where the assistant responds to stale messages in multi-turn conversations. Affects Pro users on GPT-5.2-xhigh.

5. **[#29072 — apply_patch fails on Windows sandbox](https://github.com/openai/codex/issues/29072)**  
   *Bug, Windows, Sandbox* | **22 👍, 31 comments**  
   Every `apply_patch` call fails because `codex-windows-sandbox-setup.exe` cannot launch from the MSIX package path. Critical for Windows Pro users.

6. **[#4003 — Patched files have mixed line endings on Windows](https://github.com/openai/codex/issues/4003)**  
   *Bug, Windows* | **66 👍, 22 comments**  
   Long-standing CRLF/LF corruption when applying patches. A fix PR (#30882) arrived today, suggesting this is finally being addressed.

7. **[#29320 — Codex app only displays "Something went wrong"](https://github.com/openai/codex/issues/29320)**  
   *Bug, Windows, App* | **2 👍, 28 comments**  
   Windows Store/MSIX v26.616.6631.0 shows only an error screen after update. Low reaction count but high comment volume signals widespread silent breakage.

8. **[#29000 — Codex CLI crashes with SIGTRAP on Intel macOS](https://github.com/openai/codex/issues/29000)**  
   *Bug, CLI* | **16 👍, 20 comments** *(CLOSED)*  
   CLI v0.141.0 crashes immediately on Intel Macs. Now closed, suggesting a fix shipped.

9. **[#20880 — App silently creates empty ~/Documents/Codex on every launch](https://github.com/openai/codex/issues/20880)**  
   *Bug, App* | **31 👍, 10 comments**  
   Minor but persistent UX annoyance. Every app launch creates an empty `~/Documents/Codex` folder, irking users who prefer organized home directories.

10. **[#26869 — Desktop app-server leaks child processes after crash](https://github.com/openai/codex/issues/26869)**  
    *Bug, App, Performance* | **3 👍, 10 comments**  
    macOS: Codex loses track of tool child processes across threads, leading to stale processes and excessive log writes. Signals reliability issues in the app-server architecture.

---

## Key PR Progress (Top 10)

1. **[#30850 — Block selected Git filters before staging patch paths](https://github.com/openai/codex/pull/30850)**  
   *bookholt-oai* | Prevents patch staging from invoking repository-configured Git clean/process filters, closing a sandbox-escape vector.

2. **[#30883 — Emit per-request TTFT completion telemetry](https://github.com/openai/codex/pull/30883)**  
   *xli-oai* | Adds client-observed time-to-first-token tracking per request. Requested by NVIDIA for performance analysis.

3. **[#30882 — Preserve line endings when applying patches](https://github.com/openai/codex/pull/30882)**  
   *charliemarsh-oai* | Fixes the long-standing issue #4003: patches now respect LF/CRLF of original source lines.

4. **[#30880 — Detect Codex installs managed by Vite+](https://github.com/openai/codex/pull/30880)**  
   *charliemarsh-oai* | Improves update/doctor paths for Vite+ global installations, a growing installation method.

5. **[#30879 — Handle mixed-case URLs in Windows command safety](https://github.com/openai/codex/pull/30879)**  
   *charliemarsh-oai* | Case-insensitive detection of HTTP(S) URLs in Windows dangerous-command checks (e.g., `Start-Process`).

6. **[#30872 — Log multi-agent communication lifecycle](https://github.com/openai/codex/pull/30872)**  
   *bolinfest* | Adds structured TRACE-level logging for multi-agent v2 communication, aiding debugging of agent orchestration.

7. **[#30867 — Consolidate multi-agent v2 communication sends](https://github.com/openai/codex/pull/30867)**  
   *bolinfest* | Unifies outbound paths for direct messages, follow-ups, spawns, and completions through a single sink.

8. **[#30876 — Support interleaved response items](https://github.com/openai/codex/pull/30876)**  
   *alexi-openai* | Preserves reasoning-item IDs across interleaved events, fixing TUI output when reasoning and final answer overlap.

9. **[#30315 — Add generated token auth to app-server WebSockets](https://github.com/openai/codex/pull/30315)**  
   *mikhail-oai* | Introduces 256-bit connection tokens for app-server WebSockets with optional enforcement flag.

10. **[#30848/#30854/#30833 — Git executable filter & merge driver lockdown](https://github.com/openai/codex/pull/30848)**  
    *bookholt-oai* | Three-part patch: block executable filters before patch application, block merge drivers before `--3way`, and bind worktree helpers to a trusted executable.

---

## Feature Request Trends

1. **Linux Desktop App** (Issue #11023, 674 👍): Dominant platform request. Users cite macOS power issues and desire native Linux support.
2. **Undo/Rollback Capabilities** (Issue #9203, 312 👍): Strong demand for `/undo` restoration after accidental file operations.
3. **Sensitive File Exclusion** (Issue #2847, 456 👍): Cleaned ignore mechanisms for secrets, credentials, and `node_modules`.
4. **Context/Token Management** (Issues #20582, #30875): Users want dynamic context editing, better token usage, and resolution of context window oscillation.
5. **Rate Limit Transparency** (Issue #30686): Confusion and frustration around inconsistent "reset limit" quotas among Plus subscribers.
6. **MCP Auth Reliability** (Issue #24103): External MCP (e.g., Meta Ads) login flows failing during OAuth registration.

---

## Developer Pain Points

- **Windows Reliability Crisis:** At least 10 Windows-specific issues in the top 30, spanning sandbox crashes (#29072, #30009), post-update blank screens (#29320), mixed line endings (#4003), slow Defender scans (#29911), and app-server crashes (#30884). Windows users are clearly underserved.
- **Conversation Ordering Bugs:** Issue #8648 describes models replying to stale messages, undermining trust in multi-turn sessions.
- **Performance Regressions:** CLI/TUI slowdown from v0.116→v0.117 (Issue #16335), excessive inotify watches on Linux (Issue #23574), and input freezes with large session directories (Issue #28109).
- **MCP Tool Auto-Cancellation:** Issue #29857 reveals `codex exec` ignores `default_tools_approval_mode` config, silently cancelling MCP calls.
- **Update Friction:** Windows CLI users cannot `codex update` (Issue #30015), and Vite+ install detection is only now being patched (PR #30880).

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-02

## Today's Highlights
A critical **symbolic link directory escape vulnerability** in the JIT Memory Import Processor was patched in today's nightly release (v0.51.0-nightly.20260702). Meanwhile, the community continues to surface deep agent orchestration issues: subagents falsely reporting success after hitting turn limits, and generalist agents hanging indefinitely on simple tasks. A significant CI supply chain vulnerability fix is also under review, splitting eval workflows to prevent fork-based RCE attacks.

## Releases
- **[v0.51.0-nightly.20260702.gff00dacd9](https://github.com/google-gemini/gemini-cli/releases/tag/v0.51.0-nightly.20260702.gff00dacd9)** — Emergency fix for a high-severity **symbolic link directory escape** in the memory import processor (PR [#28233](https://github.com/google-gemini/gemini-cli/pull/28233)). An attacker could craft a malicious repository with symlinks pointing outside the workspace to read/write arbitrary files. Full changelog: [v0.51.0-nightly.20260701...v0.51.0-nightly.20260702](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260701.g7f00c5fe5...v0.51.0-nightly.20260702.gff00dacd9)

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)**  
   *Status: OPEN | Priority: P1 | Comments: 9 | 👍: 2*  
   The `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even when it hit its max turn limit without doing any analysis. This masks real failures from users and downstream orchestrators. A stealth bug that erodes trust in agent reliability.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)**  
   *Status: OPEN | Priority: P1 | Comments: 7 | 👍: 8*  
   Users report `gemini-cli` hangs indefinitely when deferring to the generalist agent — even for simple folder creation. Workaround: explicitly instruct the model not to use subagents. High community upvote count signals widespread frustration.

3. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)**  
   *Status: OPEN | Priority: P1 | Comments: 4 | 👍: 3*  
   Simple CLI commands that should terminate cleanly instead hang, showing "Awaiting user input" despite the command having finished. Core shell execution regression affecting daily workflows.

4. **[#19873 — Leverage model's bash affinity via OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)**  
   *Status: OPEN | Priority: P2 | Comments: 8 | 👍: 1*  
   A major enhancement proposal: Gemini 3 models are natively trained for POSIX tool chaining. Suggests a "Zero-Dependency OS Sandboxing" approach to unlock native bash capabilities without compromising security. If implemented, could dramatically reduce token waste from edit tools.

5. **[#26525 — Add deterministic redaction in Auto Memory](https://github.com/google-gemini/gemini-cli/issues/26525)**  
   *Status: OPEN | Priority: P2 | Comments: 5 | 👍: 0*  
   Auto Memory sends local transcripts to the model for extraction *before* redacting secrets. The extraction prompt asks the model to redact, but content is already in model context — a privacy architecture concern that needs pre-send redaction.

6. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)**  
   *Status: OPEN | Priority: P2 | Comments: 6 | 👍: 0*  
   Users define custom skills (gradle, git) with clear descriptions, but the model rarely invokes them autonomously. Anecdotal but consistent: it only uses them when explicitly instructed, defeating the purpose of skill registration.

7. **[#22745 — Assess AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)**  
   *Status: OPEN | Priority: P2 | Comments: 7 | 👍: 1*  
   Epic tracking investigations into AST-aware tools for precise method-bound reads and codebase navigation. Could significantly reduce turn counts from misaligned line-based reads and token noise.

8. **[#26522 — Auto Memory retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)**  
   *Status: OPEN | Priority: P2 | Comments: 5 | 👍: 0*  
   Sessions the extraction agent skips (low signal) remain unprocessed and get re-surfaced infinitely. No backoff or deduplication for low-value sessions — wasteful API calls and noise.

9. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)**  
   *Status: OPEN | Priority: P2 | Comments: 3 | 👍: 0*  
   Gemini CLI hits a 400 error when more than ~128 tools are available. Users expect smarter tool selection/scoping rather than a hard crash.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)**  
    *Status: OPEN | Priority: P2 | Comments: 3 | 👍: 1*  
    Model occasionally uses `git reset` or `--force` when safer alternatives exist. Community asking for destructive operation guards, especially for database and branch management operations.

---

## Key PR Progress

1. **[#28233 (CLOSED) — Fix symlink directory escape in memory import processor](https://github.com/google-gemini/gemini-cli/pull/28233)**  
   *Size: M*  
   Patched a high-severity vulnerability where crafted repos could escape the workspace via symlinks. Included in today's nightly release.

2. **[#28232 (OPEN) — Fix supply chain RCE in eval workflow](https://github.com/google-gemini/gemini-cli/pull/28232)**  
   *Size: L*  
   Splits the eval CI workflow into `pull_request` + `workflow_run` to prevent fork PRs from executing with `GEMINI_API_KEY` and `GITHUB_TOKEN` in scope. Critical supply-chain hardening.

3. **[#28223 (OPEN) — Bypass LLM correction for JSON/IPYNB files](https://github.com/google-gemini/gemini-cli/pull/28223)**  
   *Size: M*  
   Surgical fix for `write_file` and `replace` tools corrupting `.ipynb` and `.json` files. The LLM correction pass was mangling structured data; this PR skips it for recognized formats.

4. **[#27971 (OPEN) — Strip thoughts from scrubbed history turns](https://github.com/google-gemini/gemini-cli/pull/27971)**  
   *Size: M/L*  
   Resolves **thought leakage** — the model's internal monologue leaking into plain-text history turns, causing confusion and infinite loop monologues in subsequent turns.

5. **[#28103 (OPEN) — Avoid keep-alive socket reuse during OAuth](https://github.com/google-gemini/gemini-cli/pull/28103)**  
   *Size: M | Area: Security*  
   Fixes OAuth failures on Node.js v24.17.0+/22.23.0+/26.3.0+ after the CVE-2026-48931 security fix for HTTP response queue poisoning. Connection reuse was poisoning OAuth token exchange.

6. **[#28167 (CLOSED) — Caretaker egress Cloud Run service skeleton](https://github.com/google-gemini/gemini-cli/pull/28167)**  
   *Size: L/XL*  
   Implements the Egress Cloud Run Service for the Caretaker Agent — receives verified action events from Pub/Sub and decouples action execution from triage. Part of a larger agent ops infrastructure push.

7. **[#28163 (OPEN) — Triage worker core foundational modules](https://github.com/google-gemini/gemini-cli/pull/28163)**  
   *Size: L*  
   First half of the Caretaker Agent Triage Worker implementation. Introduces core modules for CI/CD-driven automated issue triage.

8. **[#28094 (OPEN) — Deep-merge user and workspace settings in A2A server](https://github.com/google-gemini/gemini-cli/pull/28094)**  
   *Size: M | Area: Core*  
   `loadSettings()` was using shallow spread, causing nested configs (tools, telemetry, fileFiltering) in workspace settings to wipe out user defaults. Now uses deep merge.

9. **[#28068 (OPEN) — Guard message inspectors against empty parts arrays](https://github.com/google-gemini/gemini-cli/pull/28068)**  
   *Size: M | Area: Agent*  
   `isFunctionCall()` and `isFunctionResponse()` returned `true` for messages with empty `parts` arrays due to JavaScript's vacuous `.every()` on empty arrays. Caused misclassification of empty model messages.

10. **[#28112 (OPEN) — Add SSRF protection to OAuth metadata discovery](https://github.com/google-gemini/gemini-cli/pull/28112)**  
    *Size: L | Area: MCP*  
    OAuth discovery in MCP was fetching URLs from server responses without SSRF validation. Adds the same `isLoopbackHost()` and DNS validation used by `web-fetch.ts`.

---

## Feature Request Trends

1. **AST-aware Code Navigation** — Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) call for AST-aware file reads, search, and codebase mapping to replace noisy line-based reads with precise method/function boundary reads.

2. **Subagent Transparency & Debugging** — Requests for subagent trajectories in `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)), subagent context in bug reports ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)), and agent self-awareness of its own flags/hotkeys ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)).

3. **Memory System Improvements** — The `SandyTao520` issue cluster ([#26516](https://github.com/google-gemini/gemini-cli/issues/26516), [#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) collectively demands: pre-send secret redaction, infinite retry backoff for low-signal sessions, and quarantining invalid memory patches.

4. **Component-Level Evaluations** — [#24353](https://github.com/google-gemini/gemini-cli/issues/24353) tracks scaling behavioral evals from 76 to a robust component-level evaluation framework across all 6 supported models.

5. **Native Bash Affinity Exploitation** — [#19873](https://github.com/google-gemini/gemini-cli/issues/19873) advocates for OS sandboxing to let Gemini 3 use native POSIX tools directly, reducing edit tool overhead and token waste.

---

## Developer Pain Points

- **False Agent Success Reports** — Subagents report `GOAL` / `success` even when they hit turn limits or failed silently ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). Makes debugging agent failures nearly impossible.

- **Agent Hangs & Stalls** — Generalist agents hang indefinitely ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands get stuck on "Waiting input" after completion ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and the model gets stuck at interactive prompts like `vite create` ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)).

- **Tool & Agent Ignorance** — The model ignores user-defined skills and sub-agents ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)), the browser agent ignores `settings.json` overrides ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), and subagents run without permission after updates ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)).

- **File Corruption & Workspace Clutter** — Models create temp scripts in random directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)), corrupt JSON/IPYNB files with LLM correction ([#28223](https://github.com/google-gemini/gemini-cli/pull/28223)), and use destructive git flags instead of safe alternatives ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).

- **Security Gaps** — Symlink directory escape in memory import ([#28233](https://github.com/google-gemini/gemini-cli/pull/28233)), thought leakage into plain-text history ([#27971](https://github.com/google-gemini/gemini-cli/pull/27971)), pre-redaction secret exposure in Auto Memory ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), and SSRF gaps in MCP OAuth ([#28112](https://github.com/google-gemini/gemini-cli/pull/28112)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-02

---

## Today's Highlights

The team pushed two releases yesterday, with **v1.0.69-0** bringing a practical improvement to sandbox workflows by adding file and folder tab-completion for `/sandbox` path entries. Meanwhile, the community is actively discussing project-scoped plugins (**#1665**, 👍18) and multi-model BYOK support (**#3282**, 👍12) as the top feature requests. A fresh wave of triage issues highlights ongoing Windows-specific bugs, clipboard problems in browser environments, and accessibility gaps.

## Releases

**v1.0.69-0** *(2026-07-02)*
- **Added:** File and folder tab-completion for `/sandbox` path entries (smoother sandbox configuration).
- **Fixed:** Backgrounded session branch labels now update correctly in the Sessions split view when the working directory changes.
- **Fixed:** Unnecessary MCP reloads are skipped when returning to an already-loaded session.
- **Fixed:** Prevented the `tgrep` indexer from running under certain conditions (fix was truncated in changelog).

**v1.0.68** *(2026-07-01)*
- **Added:** Support for the **kimi-k2.7-code** model.
- **Improved:** The focused field in `/mcp` config forms is now visually indicated with a `❯` chevron (accessibility win).
- **Fixed:** IDE tools remain available during transient IDE disconnects, returning a clear error until reconnection.

## Hot Issues

1. **#1665 – Project/Repository-Scoped Plugins** [OPEN]  
   *Why it matters:* Plugins are currently global per-user, making team collaboration awkward.  👍18  
   `github/copilot-cli Issue #1665`

2. **#3596 – Session Resume Breaks Authentication** [OPEN]  
   *Bug:* `/model` fails with "Not authenticated" when resuming a specific session, forcing session restarts.  👍11  
   `github/copilot-cli Issue #3596`

3. **#1504 – Custom Theme Support** [OPEN]  
   *Feature:* Users want shareable JSON custom themes beyond the built-in options.  👍20 (highest 👍)  
   `github/copilot-cli Issue #1504`

4. **#3282 – Multiple BYOK Models** [OPEN]  
   *Pain point:* Only one Bring-Your-Own-Key model is supported; switching models requires restarting the session.  👍12  
   `github/copilot-cli Issue #3282`

5. **#2958 – Per-Mode Default Model Configuration** [OPEN]  
   *Request:* Allow separate default models for plan mode vs. autopilot mode.  👍15  
   `github/copilot-cli Issue #2958`

6. **#3997 – Model "gpt-5.3-codex" Not Available** [OPEN]  
   *Triage:* User cannot run Copilot as agent due to an unavailable model error. Fresh report (2026-07-01).  
   `github/copilot-cli Issue #3997`

7. **#3948 – web_fetch Always Fails** [OPEN]  
   *Bug:* Every `web_fetch` tool call returns `TypeError: fetch failed` despite proper network connectivity.  
   `github/copilot-cli Issue #3948`

8. **#3982 – OAuth Flow Mismatch for MCP Servers** [OPEN]  
   *Bug:* Copilot ignores `grant_types_supported`, forcing interactive auth on `client_credentials`-only MCP servers.  
   `github/copilot-cli Issue #3982`

9. **#3331 – Auto-Update Plugins from Marketplace** [OPEN]  
   *Feature:* No mechanism to auto-upgrade marketplace plugins, requiring manual updates.  👍4  
   `github/copilot-cli Issue #3331`

10. **#3984 – Windows Terminal Flickering Regression** [CLOSED]  
    *Bug:* Flickering during "thinking" phase on Windows, re-introducing a previously fixed issue (#158).  
    `github/copilot-cli Issue #3984`

## Key PR Progress

*No pull requests were updated in the last 24 hours.* Active development appears focused on the release track rather than open PRs.

## Feature Request Trends

- **Plugin Scoping & Lifecycle:** Strong demand for project/repository-scoped plugins (**#1665**) and automatic plugin updates from marketplaces (**#3331**).
- **Model Flexibility:** Users want **multiple BYOK models** (#3282) and **per-mode model defaults** (#2958) for plan vs. autopilot modes.
- **Theming & Accessibility:** Customizable themes (#1504) remain the highest-voted request. Accessibility issues around screen-reader echo (#3993) and cursor style (#2507, now closed) are also recurring themes.
- **Sandbox & Permissions:** Persistent deny-rules for commands (#3995) and better Windows sandbox support (#3653, closed) show growing sandbox adoption.

## Developer Pain Points

- **Windows Reliability:** Multiple issues plague Windows users: clipboard copy breaks while Copilot runs (#3981), terminal flicker (#3984), plugin caching problems (#3627), and `.claude/settings.json` hooks failing due to PowerShell vs. bash execution (#4001).
- **Session & Authentication Friction:** Resuming sessions loses authentication (#3596) and discards usage metrics without a `session.shutdown` event (#3994).
- **Tool Reliability:** `web_fetch` is consistently broken (#3948), and IDE connections to IntelliJ on Windows are unreliable (#2891).
- **MCP Integration Issues:** OAuth flow mismatches (#3982) and unnecessary MCP reloads (addressed in v1.0.69-0) show integration still maturing.
- **CLI Stability:** Plan→Compact re-plan infinite loops (#3158) and background agent termination on Esc-cancel (#3980) indicate edge-case robustness gaps.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-02

## Today's Highlights
The repository is undergoing a significant **brand migration** from "Kimi CLI" to "Kimi Code," but the transition is only half-complete, leading to widespread naming inconsistencies across the ecosystem. A long-standing file-reading loop bug (#640, opened in January) finally received an update after months of silence, suggesting potential progress. Two new feature requests emphasize better support for **long-running goals** and **Windows clipboard handling for media**.

---

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

1. **#640 — [bug] Kimi CLI stuck in reading one file repeatedly in a loop**  
   *Author: isbafatima90-arch* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/640)  
   **Why it matters:** This bug has been open since January 2026 with 15 comments but zero 👍. It affects users on Linux with custom Anthropic endpoints. The loop behavior suggests a fundamental issue in the streaming/context management logic. Community frustration is high due to lack of resolution.

2. **#2483 — [branding] "Kimi CLI" → "Kimi Code" migration is half-done — downstream references inconsistent**  
   *Author: counterfactual5* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2483)  
   **Why it matters:** Exposes a critical organizational problem: the repo description, README, Zed extension, VS Code extension, SDK, binary paths, and PyPI package name all use different naming conventions. This creates confusion for developers integrating with the ecosystem.

3. **#2482 — Feature suggestion: auto-save long goals to goal.md with CLI editing**  
   *Author: HePudding* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2482)  
   **Why it matters:** Currently, the `/goal` command has a 4000-byte limit. The request proposes file-based fallback and in-CLI editing, inspired by Codex workflows. No community reaction yet (0 comments), but the proposal is well-structured.

4. **#1938 — [CLOSED] Add push notification to Kimi-CLI-Web**  
   *Author: zpljd258* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/1938)  
   **Why it matters:** Closed without implementation. The request for mobile/web push notifications was popular (0 👍, 1 comment) but appears to have been deprioritized. The author specifically requested macOS + Safari support.

5. **#2368 — (Referenced in PR #2369) API key pooling for parallel subagents**  
   *Author: (issue author unknown)* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2368)  
   **Why it matters:** This issue is the driving force behind PR #2369 (closed). It addresses a key limitation: parallel subagent execution was bottlenecked by a single API key. The round-robin pool solution is now merged.

6. **#2376 — Documentation banner updates for Kimi Code**  
   *Author: counterfactual5* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2376)  
   **Why it matters:** Partially addressed in #2483's tracking. This issue handled the low-hanging fruit (banner) but left the deeper naming split unresolved.

7. **#2381 — Strategic concern about kimi-cli / kimi-code split**  
   *Author: (potential same author as #2483)* | [Link](https://github.com/MoonshotAI/kimi-cli/issues/2381)  
   **Why it matters:** Raised the original concern about the brand split. The community and maintainers need to decide on a unified direction.

8. **(Implied) File-reading loop — potential context management bug**  
   *Related to #640*  
   **Why it matters:** The loop behavior could indicate a bug in how Kimi Code handles file context or streaming responses, especially with custom models like mimo-v2-flash. No fix has been publicly shared.

9. **Windows terminal clipboard limitations**  
   *Related to PR #2481*  
   **Why it matters:** Windows users (especially on VS Code integrated terminal and Windows Terminal) cannot paste images via Ctrl+V because the terminal emits BracketedPaste events that lose binary content. This is a core UX issue for Windows developers.

10. **Goal length limitation as a bottleneck**  
    *Related to #2482*  
    **Why it matters:** Complex, long-running tasks are constrained by the 4000-byte limit. The community is asking for a pattern already proven in Codex, indicating a desire for more robust long-horizon agent capabilities.

---

## Key PR Progress

1. **#2369 — [CLOSED] feat(subagent): add API key pool for parallel subagent execution**  
   *Author: Liewzheng* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2369)  
   **Feature:** Introduces `APIKeyPool` (round-robin allocator) in `src/kimi_cli/llm_key_pool.py`. Closes #2368. Enables true parallel subagent execution without API key contention. Merged after ~1 month of development.

2. **#2481 — [OPEN] fix(shell): read clipboard media on BracketedPaste for Windows terminals**  
   *Author: redjade75723* | [Link](https://github.com/MoonshotAI/kimi-cli/pull/2481)  
   **Fix:** Modifies `_handle_bracketed_paste()` to attempt reading clipboard media when text paste fails. Targets Windows Terminal and VS Code integrated terminal users. Not yet reviewed/merged.

3. **(New issue #2483 — no PR yet)**  
   A potential PR will likely be needed to align naming across the ecosystem. No code changes available yet.

4. **(#640 — no PR yet)**  
   The file-loop bug has no associated PR. Community is awaiting maintainer intervention.

5. **(#2482 — no PR yet)**  
   The goal.md feature request has no PR. Low community engagement so far.

6. **(#1938 — CLOSED, no PR)**  
   Web push notifications were not acted upon. Likely deprioritized vs. core CLI improvements.

7. **(Potential: naming migration PRs)**  
   Expected to stem from #2483 and #2381. No code has been opened yet.

8. **(Potential: Windows media paste fix iteration)**  
   PR #2481 may need refinement based on reviewer feedback. It's the only Windows-specific fix in the recent window.

9. **(No new releases — no PRs merged today)**  
   Merged activity appears to have stalled in the last 24 hours.

10. **(Community PR gap)**  
    No external contributor PRs were opened today besides #2481. Indicates a quiet period or blocker for community contributions.

---

## Feature Request Trends

1. **Brand consistency** — The top request is to unify "Kimi CLI" vs. "Kimi Code" naming across all downstream assets (SDK, binary, docs, IDE extensions). This is a structural blocker for ecosystem growth.

2. **Long-running goal support** — Users want automatic file-based storage for goals exceeding 4000 bytes, plus in-CLI editing and pause/resume. This aligns with demand for complex, long-horizon agent tasks.

3. **Mobile/web push notifications** — Though the issue (#1938) was closed, the request for push notifications from Kimi-CLI-Web remains relevant for developers working across devices.

4. **Parallel subagent execution** — The merged PR #2369 addresses this, but the community may want further API key management features (e.g., rate limiting, key rotation).

5. **Windows clipboard media paste** — PR #2481 addresses a narrow but critical UX gap for Windows users. Similar fixes for other platforms may follow.

---

## Developer Pain Points

1. **Stuck file-reading loop with no ETA** — Issue #640 has been open for 6 months with no fix. Affected users (especially on Linux) cannot use the CLI reliably. Lack of maintainer communication is a major frustration.

2. **Naming inconsistency across ecosystem** — Developers integrating with Kimi Code face confusion over which name to use for binary paths, SDK imports, and IDE extensions. This slows down plugin development and onboarding.

3. **Goal length cap blocking complex workflows** — The 4000-byte limit is a hard ceiling for long-running tasks. Users must either truncate their goals or manage context manually, which erodes the value of an "agentic" tool.

4. **No push notifications for web/CLI** — Developers who run long tasks via Kimi-CLI-Web must poll for completion. The closed issue suggests limited commitment to this feature.

5. **Windows clipboard binary content loss** — Ctrl+V fails silently for images on Windows Terminal and VS Code's integrated terminal. This is a daily annoyance for Windows-based developers.

6. **Lack of recent releases** — No releases in the last 24 hours and sparse activity overall. The community may perceive the project as low-priority or under-resourced.

7. **Single API key bottleneck for parallel execution** — Before PR #2369, parallel subagent execution was impossible without multiple manual configurations. The fix is merged but not yet released.

8. **Documentation lagging behind features** — The brand migration is documented in the banner (#2376) but not in README, SDK, or extensions. Developers relying on documentation face mismatches.

9. **Limited community contribution velocity** — Only 2 PRs in 24h, zero from external contributors. The project may benefit from clearer contribution guidelines or issue triage for new contributors.

10. **Long-tail bugs with low community votes** — Issue #640 has only 1 👍 despite 15 comments. This may cause maintainers to deprioritize it, but the frequency of comments indicates high individual frustration.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**2026-07-02**

---

## Today's Highlights

The v1.17.13 patch ships with critical fixes for OpenAI-compatible reasoning models and stale Copilot response handling, while the V2 migration sprint continues at full pace with nearly 20 open feature issues filed in the last 72 hours. A long-standing Windows path separator bug—affecting session visibility across the entire web UI—finally sees multiple converging fixes land in PRs today.

---

## Releases

**v1.17.13** ([Release](https://github.com/anomalyco/opencode/releases/tag/v1.17.13)) — Two core bugfixes:
- **Force reasoning mode for OpenAI-compatible reasoning models**: Ensures reasoning settings apply reliably on custom deployments, not just first-party OpenAI endpoints.
- **Stop replaying stale GitHub Copilot response item IDs**: Eliminates follow-up request failures caused by the SDK re-emitting expired item identifiers.

Desktop fix: **Question prompts can now be minimized**, restoring expected UX for multi-turn interactions.

---

## Hot Issues

1. **[#34813](https://github.com/anomalyco/opencode/issues/34813) — Homebrew publish is stopped** (3 comments, just filed)
   Latest Homebrew formula is stuck at v1.17.10 while upstream is at v1.17.13. Community quickly flagged the gap; maintainers will need to unblock the brew release pipeline.

2. **[#34820](https://github.com/anomalyco/opencode/issues/34820) — Persistent "keep alert" error despite reinstall** (3 comments, just filed)
   User reports a non-dismissable error alert that survives app updates and full reinstalls. No plugins listed; likely a core state corruption or entitlement issue. Tagged `needs:compliance` for investigation.

3. **[#34804](https://github.com/anomalyco/opencode/issues/34804) — Chat history goes blank, reloads scrolled to oldest** (2 comments)
   Cross-version bug where final response rendering triggers a blank canvas, then a reload that loses scroll position. Directly impacts daily workflow trust.

4. **[#34359](https://github.com/anomalyco/opencode/issues/34359) — Track TUI migration to `@opencode-ai/client`** (8 comments, 🔥)
   The V2 TUI migration epic—8 comments in 3 days. Tracks all call-site renames and shape migrations needed to move from legacy `@opencode-ai/sdk/v2` to the generated Promise-based client. The central coordination issue for the V2 frontend push.

5. **[#34341](https://github.com/anomalyco/opencode/issues/34341) — Progressive `AGENTS.md` loading via read-tool plugin context** (5 comments)
   Proposes a V2-native approach: instead of loading all `AGENTS.md` files upfront, the read tool progressively discovers and admits them into system context. Clean separation of concerns—plugins discover, core system context admits.

6. **[#34765](https://github.com/anomalyco/opencode/issues/34765) — ChatGPT OAuth not routed to codex backend (HTTP 401)** (3 comments)
   V2 regression: users with ChatGPT Plus/Pro subscriptions get `missing api.responses.write` when trying to use OpenAI models. Authentication routing for consumer subscriptions appears broken on the v2 branch.

7. **[#34492](https://github.com/anomalyco/opencode/issues/34492) — Unified file watching and hot reload service** (3 comments)
   V2 feature request for a single file-watching service covering config files, agent definitions, and related hot-reload needs. Currently every subsystem implements its own watcher—this would consolidate into a shared, debounced service.

8. **[#21340](https://github.com/anomalyco/opencode/issues/21340) — Windows: Web UI sessions missing due to path separator mismatch** (8 comments, 👍 2)
   The root cause issue for today's Windows fix avalanche. Database stores `SessionTable.directory` with POSIX forward slashes (`D:/Workspace`), but web API queries arrive with Windows backslashes (`D:\Workspace`). SQLite exact-match fails; UI shows empty session list.

9. **[#34435](https://github.com/anomalyco/opencode/issues/34435) — Port MCP lifecycle and elicitation APIs to V2** (3 comments)
   The V2 TUI migration depends on MCP status/elicitation APIs being available under the new client. Blocks the TUI from showing MCP server health and tool listing.

10. **[#34766](https://github.com/anomalyco/opencode/issues/34766) — V2 TUI: follow-up prompts should render optimistically** (2 comments)
    Queued prompts work silently in V2—the TUI should show a pending/queued indicator so users know their input was accepted. V1 had this; V2 lost it.

---

## Key PR Progress

1. **[#34806](https://github.com/anomalyco/opencode/pull/34806) — `fix: normalize Windows paths in session directory SQL queries`** (just merged)
   Adds `dbDir()` normalization to SQL query parameters on Windows. Closes the exact-match gap when web-frontend paths use forward slashes but DB uses backslashes. Quick, targeted fix.

2. **[#30367](https://github.com/anomalyco/opencode/pull/30367) — `fix(session): normalize Windows directory paths in session list`** (merged)
   Broader approach: normalizes paths at the session list API layer. Closes #30374. Multiple contributors converging on the same bug family.

3. **[#31882](https://github.com/anomalyco/opencode/pull/31882) — `feat(app): v2 review panel overhaul`** (open, 22 days active)
   Major V2 UI feature: complete new review panel with updated UI and functionality. Duplicates some V1 components to avoid destabilizing the stable release. Signals the V2 frontend is nearing functional parity.

4. **[#32398](https://github.com/anomalyco/opencode/pull/32398) — `feat(app): add session file list and desktop backgrounds`** (open, 17 days)
   Adds a Files tab to the session side panel for browsing workspace files alongside review/context tools. Improves session workspace navigation without leaving the chat interface.

5. **[#34815](https://github.com/anomalyco/opencode/pull/34815) — `feat(opencode): support per-variant limit overrides`** (just opened)
   Models can now carry `limit` overrides per variant—e.g., a 200k-context preset next to the default. Essential for users who switch between token budgets depending on task complexity.

6. **[#34814](https://github.com/anomalyco/opencode/pull/34814) — `fix(agent): remove alphabetical sort to preserve insertion order for primary agents`** (just opened)
   Removes the alphabetical secondary sort that was scrambling user-defined agent order (e.g., "Home" sorting before "plan"). Restores natural insertion order. Closes #7372.

7. **[#34810](https://github.com/anomalyco/opencode/pull/34810) — `docs: add Composio MCP server example`** (just opened)
   Small but welcome docs addition: adds Composio to the MCP servers examples list. Lowers friction for new users evaluating MCP integrations.

8. **[#34809](https://github.com/anomalyco/opencode/pull/34809) — `fix(tui): restore terminal title after PowerShell paste on Windows`** (just opened)
   PowerShell 5.1 overwrites the TUI's custom terminal title (`OC | <session>`) when pasting images via Ctrl+V. This fix restores the title after the paste completes. Niche but classic Windows pain point.

9. **[#34242](https://github.com/anomalyco/opencode/pull/34242) — `fix(tui): prevent piped stdin from breaking UI and keyboard input`** (open, 5 days)
   Closes four issues (#28538, #24195, #3871, #6220). Piped stdin was corrupting terminal state and breaking keyboard input. A long-standing TUI bug that multiple users independently reported.

10. **[#33875](https://github.com/anomalyco/opencode/pull/33875) — `fix(app): preserve session scroll position`** (open, 7 days)
    Session tabs now save scroll position in a store. When toggling between sessions, the viewport stays where you left off instead of jumping to top. Directly addresses #34804's reload-scroll bug.

---

## Feature Request Trends

**V2 Migration Dominates —** The overwhelming majority of feature requests today target the V2 codebase: TUI migration to `@opencode-ai/client` ([#34359](https://github.com/anomalyco/opencode/issues/34359)), progressive `AGENTS.md` loading ([#34341](https://github.com/anomalyco/opencode/issues/34341)), file watching service ([#34492](https://github.com/anomalyco/opencode/issues/34492)), tool plugin architecture ([#34489](https://github.com/anomalyco/opencode/issues/34489)), `@`-tagged file resolution ([#34387](https://github.com/anomalyco/opencode/issues/34387)), file attachments ([#34497](https://github.com/anomalyco/opencode/issues/34497)), reasoning options ([#34488](https://github.com/anomalyco/opencode/issues/34488)), model variant selection ([#34487](https://github.com/anomalyco/opencode/issues/34487)), MCP APIs ([#34435](https://github.com/anomalyco/opencode/issues/34435)), command ports ([#34685](https://github.com/anomalyco/opencode/issues/34685)), and session fork API ([#34430](https://github.com/anomalyco/opencode/issues/34430)). Every major V1 subsystem is being systematically reimplemented with feature requests tracking the gap.

**MCP Ecosystem Growth —** Continued interest in MCP server support: HTTP Streamable transport ([#8058](https://github.com/anomalyco/opencode/issues/8058)), async prompt updates ([#34541](https://github.com/anomalyco/opencode/issues/34541)), and Composio documentation ([#34810](https://github.com/anomalyco/opencode/pull/34810)). The ecosystem is demanding first-class MCP integration, not just SSE.

**Session Portability and Persistence —** Requests for saving sessions to project folders ([#14292](https://github.com/anomalyco/opencode/issues/14292), 18 👍), session-scoped keyed context ([#34380](https://github.com/anomalyco/opencode/issues/34380)), and progressive agent loading all point toward making session data self-contained and portable across environments.

---

## Developer Pain Points

**Windows Path Separator Hell (🔥 highest frequency today)** — At least 7 issues/PRs today trace to this single bug family: `SessionTable.directory` stores paths with inconsistent separators (POSIX vs Windows) across DB writes, web API queries, and client-side normalization. Symptoms range from empty session lists ([#21340](https://github.com/anomalyco/opencode/issues/21340), [#23864](https://github.com/anomalyco/opencode/issues/23864), [#31597](https://github.com/anomalyco/opencode/issues/31597), [#30374](https://github.com/anomalyco/opencode/issues/30374), [#17183](https://github.com/anomalyco/opencode/issues/17183)) to disappearing sidebar sessions ([#34723](https://github.com/anomalyco/opencode/issues/34723)). Two PRs merged today ([#34806](https://github.com/anomalyco/opencode/pull/34806), [#30367](https://github.com/anomalyco/opencode/pull/30367)) suggest maintainers are converging on a normalization-at-query-layer solution, but the root cause—multiple code paths writing different formats—remains.

**Scroll Position Loss in Chat** — Three reports today: blank canvas on final response ([#34804](https://github.com/anomalyco/opencode/issues/34804)), inability to scroll up to view previous AI outputs ([#11298](https://github.com/anomalyco/opencode/issues/11298), open since January), and a fix PR for session tab scroll preservation ([#33875](https://github.com/anomalyco/opencode/pull/33875)). This is a fundamental UX issue that erodes user trust in conversation continuity.

**V2 Authentication Regressions** — The ChatGPT OAuth routing failure ([#34765](https://github.com/anomalyco/opencode/issues/34765)) is a blocker for users trying V2 with existing subscriptions. Compounded by the TUI onboarding fix PR ([#34819](https://github.com/anomalyco/opencode/pull/34819)) which suggests the V2 auth flow is still incomplete.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-02

## Today's Highlights

The Pi project saw a burst of activity around **service-provider model updates** and **extension infrastucture** improvements. GitHub Copilot's GA launch of Claude Sonnet 5 drove three separate issues/PRs to backfill provider catalogues. A major contributor landed **AOT compilation for TypeScript extensions**, promising startup-time reductions from seconds to milliseconds. On the bug front, a critical `pi update` regression on version 0.80.3 due to an unpinned `@smithy/node-http-handler` dependency was quickly reported and closed.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **#5653 — Move off Shrinkwrap [OPEN]**  
   Two identical copies of `pi-ai` on disk (one hoisted, one nested) because `@earendil-works/pi-ai` is pulled in as a transitive dependency via `pi-coding-agent`. The module-level `Map` registry means these are separate instances, breaking API provider identity.  
   *Why it matters:* A fundamental packaging bug that breaks provider configuration when both packages are direct deps. 18 comments, no resolution yet.  
   **[View Issue](https://github.com/earendil-works/pi/issues/5653)**

2. **#2870 — Follow XDG Base Directory [CLOSED]**  
   Application was cluttering `$HOME` with `.pi/` directory. Community demanded XDG compliance for Linux. Was left open for 3 months, but closed yesterday with 34 👍.  
   *Impact:* Filesystem hygiene for Linux users.  
   **[View Issue](https://github.com/earendil-works/pi/issues/2870)**

3. **#6187 — Pi login hangs in WSL after Copilot device auth [CLOSED]**  
   Browser-based Copilot auth completes, but the WSL terminal never detects it and hangs.  
   *Why it matters:* Blocks Windows+WSL users from using GitHub Copilot authentication. 6 comments.  
   **[View Issue](https://github.com/earendil-works/pi/issues/6187)**

4. **#5501 — Tolerate extra keys on edit tool edits[] items [CLOSED]**  
   Models occasionally append stray keys like `newText_2` after long `newText` blocks. The schema validation was rejecting these.  
   *Why it matters:* This is a recurring class of model-format brittleness — models emit slightly off-spec JSON, and Pi was too strict.  
   **[View Issue](https://github.com/earendil-works/pi/issues/5501)**

5. **#5536 — Split-turn compaction sends parallel summarization requests [CLOSED]**  
   Single-slot local backends (e.g., `llama.cpp`) get 429 errors when split-turn compaction launches two summarization requests simultaneously.  
   *Impact:* Local model users can't use auto-compaction.  
   **[View Issue](https://github.com/earendil-works/pi/issues/5536)**

6. **#6202 — Kitty inline image preview renders blank [CLOSED]**  
   In Kitty terminal (not tmux), image previews reserve vertical space but are invisible. The model still receives the image, but the TUI shows only blank space.  
   *Why it matters:* Core visual feature broken on a popular terminal.  
   **[View Issue](https://github.com/earendil-works/pi/issues/6202)**

7. **#6222 — Failed to load extension [CLOSED]**  
   Catch-22: a broken extension prevents `pi extension list` from working, so the user can't identify or remove the offending extension. No error context provided.  
   *Why it matters:* Zero-recovery path for extension failures.  
   **[View Issue](https://github.com/earendil-works/pi/issues/6222)**

8. **#6215 — pi update fails on 0.80.3 due to @smithy/node-http-handler@^4.9.1 [CLOSED]**  
   A dependency resolution failure blocking all upgrades to 0.80.3. Upstream package missing from registry.  
   *Impact:* Version-pinned users stuck on older release.  
   **[View Issue](https://github.com/earendil-works/pi/issues/6215)**

9. **#6206 — Clamping to context window prevents artificial context limits [OPEN]**  
   Recent fix clamped `max_tokens` to the model's context window, which breaks cases where users want a smaller artificial limit.  
   *Why it matters:* Regression in user-configurable context management. 2 comments.  
   **[View Issue](https://github.com/earendil-works/pi/issues/6206)**

10. **#6234 — Escape leaves Pi stuck in Working when extension hook never settles [CLOSED]**  
    Pressing Escape during an active run doesn't properly abort if an extension context hook hangs. Double-Escape is swallowed by the streaming-abort handler.  
    *Why it matters:* Extension hangs lead to unrecoverable TUI state.  
    **[View Issue](https://github.com/earendil-works/pi/issues/6234)**

## Key PR Progress

1. **#5678 — Add `excludeFromContext` for custom messages [CLOSED]**  
   Merged yesterday. Adds `excludeFromContext?: boolean` to custom messages via `sendMessage()`, mirroring bash-execution messages. Compaction and branch summarization also skip flagged messages.  
   **[View PR](https://github.com/earendil-works/pi/pull/5678)**

2. **#6213 — AOT compilation for TypeScript extensions [CLOSED]**  
   Landed. Compiles TS extensions to JS using esbuild during `pi install`/`pi update`. Reduces startup from seconds to milliseconds. This was the third attempt at this PR (see #6218, #6219, #6220 which were all closed/replaced).  
   **[View PR](https://github.com/earendil-works/pi/pull/6213)**

3. **#6207 — Add Claude Sonnet 5 to GitHub Copilot provider [CLOSED]**  
   Backfills Sonnet 5 into the Copilot provider catalogue, routed through the OpenAI-compatible `/chat/completions` endpoint.  
   **[View PR](https://github.com/earendil-works/pi/pull/6207)**

4. **#6225 — Infer toolUse when provider omits finish_reason [CLOSED]**  
   Nvidia NIM for GLM-5.1 sends tool_call chunks with `finish_reason=null` and never sends a `"tool_calls"` finish_reason. This PR handles that by inferring tool use from chunk content.  
   **[View PR](https://github.com/earendil-works/pi/pull/6225)**

5. **#6230 — Preserve first path segment when find relativizes from bare root [CLOSED]**  
   Fixes #6104. `path.resolve` keeps trailing separator on bare root (`/`, `C:\`). The `find` command's `slice(searchPath.length + 1)` was eating the first character of paths.  
   **[View PR](https://github.com/earendil-works/pi/pull/6230)**

6. **#6227 — SQLite session storage [OPEN]**  
   New feature: under `PI_SQLITE_SESSION_STORAGE=1`, Pi writes session transcripts to SQLite in parallel to jsonl. Exposes `NodeSqliteStatement` for extension access.  
   **[View PR](https://github.com/earendil-works/pi/pull/6227)**

7. **#5509 — Amazon Bedrock Mantle OpenAI Responses provider [CLOSED]**  
   Adds GPT 5.5/5.4 support through Bedrock Mantle's OpenAI Responses API. Modelled after the Azure OpenAI responses provider.  
   **[View PR](https://github.com/earendil-works/pi/pull/5509)**

8. **#6216 — Amazon Bedrock Mantle OpenAI Responses provider (v2) [OPEN]**  
   Supersedes #5509, using OpenAI SDK's Bedrock provider instead of a custom client. Still open.  
   **[View PR](https://github.com/earendil-works/pi/pull/6216)**

9. **#2780 — Argument-hint frontmatter for prompt templates [CLOSED]**  
   Long-running PR (April→July) finally merged. Parses `argument-hint` from prompt template frontmatter and displays it in autocomplete dropdown: `<angle brackets>` for required, `[square brackets]` for optional.  
   **[View PR](https://github.com/earendil-works/pi/pull/2780)**

10. **#5262 — Anthropic Vertex provider [OPEN]**  
    Still open since May 31. Adds a built-in `anthropic-vertex` provider for Claude on GCP Vertex AI. Reuses Anthropic Messages streaming path.  
    **[View PR](https://github.com/earendil-works/pi/pull/5262)**

## Feature Request Trends

Three clear feature directions emerged from this week's issues:

- **Provider/model catalogue parity.** Users consistently file issues when a model goes GA on a provider (e.g., Sonnet 5 on Copilot, GLM 5.2 Fast on Fireworks) but isn't reflected in Pi's built-in provider configs. Community expectation is tight synchronization with provider announcements.
- **Extension API surface expansion.** Multiple requests for extensions to be able to invoke tools by name, set theme color overrides, and participate more deeply in the agent loop. The AOT compilation PR (#6213) and the `excludeFromContext` PR (#5678) address infrastructure, but users want richer semantic APIs.
- **SQLite-backed storage and structured data access.** PR #6227 for SQLite session storage points to demand for queryable, programmatic access to conversation history beyond JSONL.

## Developer Pain Points

- **Dependency resolution fragility.** The `@smithy/node-http-handler@^4.9.1` regression (#6215) shows that Pi's dependency graph is sensitive to upstream registry availability. This blocks upgrades and wastes developer time.
- **Extension error recovery vacuum.** Issue #6222 highlights a critical UX gap: a broken extension can prevent all `pi extension` commands from working, leaving users with no recovery path. No error logging or safe-mode fallback exists.
- **Local/offline model friction.** Issues #5536 (parallel summarization 429s on local backends) and #6231 (auth blocking local models) reveal that local-model users face a disproportionate number of blockers — both from assumptions about cloud API availability and from auth gatekeeping.
- **TUI rendering edge cases.** Blank Kitty image previews (#6202), stuck "Working..." spinners after escape (#6234), and scrollback artifact leakage (#3083) suggest the terminal rendering layer is accumulating debt across terminal emulators.
- **Config sync incompleteness.** Issue #6214 reports that `pi update --extensions` doesn't install missing packages when syncing `.pi` config between machines, making multi-machine setups unreliable.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-02

## Today's Highlights

Two nightly releases shipped today: **v0.19.4-nightly** with daemon channel worker hardening and web-shell session lifecycle fixes, and the stable **v0.19.4** release bundling recent daemon documentation refresh and auto-compact threshold configurability. Community activity remains high with 50 issues and 50 PRs updated in the last 24 hours, highlighting growing interest in channel adapters, tool execution timeouts, and daemon performance optimization.

---

## Releases

**v0.19.4-nightly.20260702.46814e4f1**
- `feat(cli): Harden daemon-managed channel worker` — improves restart supervision, IPC heartbeat, and stderr forwarding with credential redaction ([PR #6098](https://github.com/QwenLM/qwen-code/pull/6098))
- `fix(web-shell): defer session creation until` — prevents premature session initialization in web-shell contexts

**v0.19.4**
- `docs(daemon): refresh daemon docs for recent PRs (wave 2)` ([PR #5954](https://github.com/QwenLM/qwen-code/pull/5954))
- `feat(core): add configurable auto-compact threshold and Stop` — introduces tunable thresholds for automatic context compaction

---

## Hot Issues

| # | Issue | Why It Matters | Community Reaction |
|---|-------|----------------|-------------------|
| 1 | [#61](https://github.com/QwenLM/qwen-code/issues/61) — Qwen Code FAQ | Long-standing documentation hub with 30 comments, covers API key setup and quick-start | 👍4, closed but actively referenced |
| 2 | [#4888](https://github.com/QwenLM/qwen-code/issues/4888) — IDEA plugin `ask_user_question` not showing text/inputs | Blocks interactive workflows in JetBrains IDEs | 11 comments, closed with need-info status |
| 3 | [#1281](https://github.com/QwenLM/qwen-code/issues/1281) — Ollama-deployed model returns JSON responses | Affects users running local Qwen3-Coder via Ollama | 7 comments, closed |
| 4 | [#5080](https://github.com/QwenLM/qwen-code/issues/5080) — API key mixing between Standard and Token Plan providers | Causes 401 errors when switching model providers | 6 comments, closed after investigation |
| 5 | [#6094](https://github.com/QwenLM/qwen-code/issues/6094) — QQ Bot cron/blockStreaming interaction issues | Streaming mode bugs affecting bot reliability on non-Reply channels | 5 comments, open; follow-up from PR #5902 review |
| 6 | [#4748](https://github.com/QwenLM/qwen-code/issues/4748) — Optimize daemon cold start latency (2.5s → ~1.5s) | Performance improvement target for daemon-first workflows | 5 comments, open enhancement |
| 7 | [#6077](https://github.com/QwenLM/qwen-code/issues/6077) — Follow-up suggestion filters sentences with abbreviations | False-positive "multiple sentences" detection on normal text like "Weeds vs. Wildflowers" | 4 comments, welcome-pr tagged |
| 8 | [#5979](https://github.com/QwenLM/qwen-code/issues/5979) — `/auth` changes not persisting to new sessions | New sessions after provider config change still return 401 | 3 comments, open with in-review status |
| 9 | [#6119](https://github.com/QwenLM/qwen-code/issues/6119) — `list_directory` and `read_file` inconsistent git-ignore handling | Leads to unexpected file access results between tools | 3 comments, open, needs-triage |
| 10 | [#6116](https://github.com/QwenLM/qwen-code/issues/6116) — Fallback model chain on overload/rate-limit | Feature request for automatic backup model switching on 429/503/529 errors | 3 comments, open |

---

## Key PR Progress

| # | PR | Description | Status |
|---|----|-------------|--------|
| 1 | [#5902](https://github.com/QwenLM/qwen-code/pull/5902) — QQ Bot streaming improvements | Replaces BlockStreamer coalescing with 2-second idle flush, removes 2000-char split, adds reply TTL, fixes markdown table detection | Open |
| 2 | [#6123](https://github.com/QwenLM/qwen-code/pull/6123) — Prune ignored directories during glob traversal | Applies `.gitignore`/`.qwenignore` rules during traversal, not post-filter — reduces I/O in large repos | Open |
| 3 | [#5847](https://github.com/QwenLM/qwen-code/pull/5847) — Runtime context injection for per-turn system reminders | Adds key-value RuntimeContext store for dynamic system-reminder injection (daemon API/SDK) | Open |
| 4 | [#6098](https://github.com/QwenLM/qwen-code/pull/6098) — Harden daemon-managed channel worker | Adds bounded restart supervision, IPC heartbeat, stderr redaction, richer status fields | **Merged** (in v0.19.4-nightly) |
| 5 | [#6114](https://github.com/QwenLM/qwen-code/pull/6114) — Show lifecycle status in channel adapters | Maps task lifecycle to Telegram typing, Weixin indicators, DingTalk reactions | Open |
| 6 | [#6128](https://github.com/QwenLM/qwen-code/pull/6128) — Web-shell list-dialog overhaul | Full keyboard navigation, IME-safe search, ARIA roles, consistent visual language | Open |
| 7 | [#6124](https://github.com/QwenLM/qwen-code/pull/6124) — Per-tool-call execution timeout | Opt-in timeout via `QWEN_CODE_TOOL_EXECUTION_TIMEOUT_MS` at CoreToolScheduler layer | Open |
| 8 | [#6096](https://github.com/QwenLM/qwen-code/pull/6096) — Add `zvec-grep` bundled skill | Guides Qwen Code to use `zg` CLI for semantic workspace search | Open |
| 9 | [#6138](https://github.com/QwenLM/qwen-code/pull/6138) — Leader approval for plan-required teammates | Plan-required teammates submit plans that wait for leader resolution before execution | **Merged** |
| 10 | [#6142](https://github.com/QwenLM/qwen-code/pull/6142) — Mobile UX fixes (safe areas, overscroll, native feel) | Fixes safe-area insets, pull-to-refresh, and theme-colored backgrounds for iPhone | Open |

---

## Feature Request Trends

1. **Resilient model switching & fallback chains** — Multiple requests (e.g., [#6116](https://github.com/QwenLM/qwen-code/issues/6116)) for auto-fallback on rate limits/overload, plus cleaner separation between API key types and provider connections
2. **Hot-reload for skills, extensions, MCP, and config** — [#3696](https://github.com/QwenLM/qwen-code/issues/3696) tracking issue shows strong community demand for runtime config changes without session restarts
3. **Portable chat history & export** — [#2373](https://github.com/QwenLM/qwen-code/issues/2373) requests project-local `.qwen/chat-history/` storage and per-chat export commands for cross-machine portability
4. **Channel adapter enhancements** — Growing interest in lifecycle status visibility, identity metadata, and per-turn injection across Telegram, Weixin, DingTalk, and QQ Bot adapters (PRs #6114, #6105, #5902)

---

## Developer Pain Points

- **Authentication/configuration stickiness** — `/auth` changes not propagating to new sessions ([#5979](https://github.com/QwenLM/qwen-code/issues/5979)) and API key mixing between Standard and Token Plan providers ([#5080](https://github.com/QwenLM/qwen-code/issues/5080)) continue to frustrate users
- **File system inconsistency** — Git-ignore handling diverges between `list_directory` and `read_file` ([#6119](https://github.com/QwenLM/qwen-code/issues/6119)), and `.gitignore`/`.qwenignore` respect flags don't behave as documented ([#1093](https://github.com/QwenLM/qwen-code/issues/1093))
- **Context window misconfiguration** — [#6144](https://github.com/QwenLM/qwen-code/issues/6144) reports incorrect context window calculations when using custom model configurations
- **Terminal UI flickering** — [#6137](https://github.com/QwenLM/qwen-code/issues/6137) describes flickering in xterm, tmux, and Alacritty environments, particularly with pane resizing

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-02

**Project:** Hmbown/CodeWhale (formerly DeepSeek-TUI)  
**Snapshot:** v0.8.67 pre-release, heavy setup-wizard and cleanup activity

---

## 1. Today's Highlights

The CodeWhale (rebranded DeepSeek TUI) community is deep in v0.8.67 release prep, with the constitution-first setup wizard as the central focus. A major bug surfaced where CodeWhale enters self-driven modification loops without user confirmation (Issue #3275), drawing 14 comments and triggering security/reliability concerns. The community is also cleaning up codebase cruft — three PRs merged today removing dead MCP, approval-cache, and model-registry code — while a new dynamic MCP server tool (PR #3866) hints at expanded LLM capability.

---

## 2. Releases

No new releases in the last 24 hours. The current stable tag remains v0.8.66. Activity is concentrated on v0.8.67 pre-release issues and PRs.

---

## 3. Hot Issues (10 selected)

### 1. [#3275 — CodeWhale overly involved in modifications, deviating from user intent](https://github.com/Hmbown/CodeWhale/issues/3275)
**Type:** Bug / Security / Reliability | **Comments:** 14  
A regression from issue #3061. CodeWhale enters a self-driven loop of proposing, answering, and executing without user confirmation. This undermines trust in agent autonomy and is the most commented issue this cycle. Community wants a hard stop-gap before v0.8.67 ships.

### 2. [#3406 — Runtime posture card with constitution boundary](https://github.com/Hmbown/CodeWhale/issues/3406)
**Type:** Enhancement / Security | **Comments:** 13  
Proposes a posture selector (ask-first / normal agent / high-trust local) during setup, preventing the constitution from silently changing runtime security. Shows strong community interest in auditable security boundaries.

### 3. [#3736 — Separate work mode from approval policy](https://github.com/Hmbown/CodeWhale/issues/3736)
**Type:** Enhancement / Reliability | **Comments:** 12  
Identifies four overlapping knobs (`allow_shell`, `approval_mode`, `trust_mode`, `auto_approve`) as a structural source of UI/mode mismatch. Community strongly supports a cleaner permission model.

### 4. [#3793 — Guided localized constitution creator](https://github.com/Hmbown/CodeWhale/issues/3793)
**Type:** Enhancement / UX | **Comments:** 10  
Replaces the blank prompt editor with a guided, language-first constitution creator. Includes key principle: autonomy/risk posture must not directly flip runtime settings from within the constitution.

### 5. [#2870 — EPIC: staged command-boundary refactor](https://github.com/Hmbown/CodeWhale/issues/2870)
**Type:** Documentation / Cleanup | **Comments:** 10  
Tracking epic for a multi-layer command-boundary refactor. 10 comments suggest broad community investment in how commands scope and interact.

### 6. [#3806 — /constitution as primary management surface](https://github.com/Hmbown/CodeWhale/issues/3806)
**Type:** Enhancement / UX | **Comments:** 8  
Proposes `/constitution` replace `/context report` as the main user-facing surface. Signals a shift toward discoverable, non-diagnostic configuration.

### 7. [#3412 — Docs for constitution-first setup, localization](https://github.com/Hmbown/CodeWhale/issues/3412)
**Type:** Documentation / UX | **Comments:** 8  
Community feedback: documentation should focus on v0.8.67 setup wizard and constitution, deferring hotbar and advanced features. Localization is requested.

### 8. [#3829 — Ship ModalShell v1 for release-blocking menus](https://github.com/Hmbown/CodeWhale/issues/3829)
**Type:** Bug / Enhancement | **Comments:** 6  
Critical: unstable popups block v0.8.67 release. Proposal for minimal shared modal structure to fix four linked issues (#3732, #3791, #3830, #3831).

### 9. [#3830 — Configured-provider route manager for /provider and /model](https://github.com/Hmbown/CodeWhale/issues/3830)
**Type:** Enhancement / UX | **Comments:** 5  
Current flat list implementation breaks down when users have multiple providers. Community wants a structured route manager.

### 10. [#3864 — Sub-agent state persists to .deepseek/ instead of .codewhale/](https://github.com/Hmbown/CodeWhale/issues/3864)
**Type:** Bug / Branding | **Comments:** 3  
Lingering pre-rebrand path creates two hidden directories and breaks state persistence. Immediately actionable — a fix PR (#3865) was opened concurrently.

---

## 4. Key PR Progress (10 selected)

### 1. [#3578 — Preserve Windows SDK env roots for shell](https://github.com/Hmbown/CodeWhale/pull/3578)
**Author:** nightt5879 | **Status:** CLOSED  
Fixes #3572. Recovers Windows SDK/toolchain path variables from registry before shell launch, fixing build toolchain issues on Windows.

### 2. [#3574 — Address context window review feedback](https://github.com/Hmbown/CodeWhale/pull/3574)
**Author:** nightt5879 | **Status:** CLOSED  
Fixes two edge cases: negative `max_tokens` with tiny context budgets, and restoration of `active_context_window_override` on provider-switch auth rollback.

### 3. [#3861 — v0.8.67 constitution-first setup foundation](https://github.com/Hmbown/CodeWhale/pull/3861)
**Author:** Hmbown | **Status:** OPEN (Draft)  
Landing the shared model/persistence/renderer in `crates/config`. The foundation for all v0.8.67 setup wizard work.

### 4. [#3866 — LLM can start MCP servers from chat context](https://github.com/Hmbown/CodeWhale/pull/3866)
**Author:** bistack | **Status:** OPEN  
Adds `start_mcp_server` tool supporting stdio (local) and HTTP (remote) transports. Enables dynamic tool extension from conversation.

### 5. [#3869 — Dynamic MCP server infrastructure for McpPool](https://github.com/Hmbown/CodeWhale/pull/3869)
**Author:** bistack | **Status:** CLOSED  
Foundation for runtime-started MCP servers. Uses `parking_lot::RwLock` for thread-safe dynamic server management.

### 6. [#3879 — Prune dead fleet runtime helpers](https://github.com/Hmbown/CodeWhale/pull/3879)
**Author:** cyq1017 | **Status:** OPEN  
Fixes #3843. Removes legacy fleet compatibility helpers that no longer have call sites.

### 7. [#3865 — Persist sub-agent state to .codewhale/](https://github.com/Hmbown/CodeWhale/pull/3865)
**Author:** yekern | **Status:** OPEN  
Closes #3864. Fixes pre-rebrand path fallback that created duplicate hidden directories.

### 8. [#3748 — Add Sakana AI Fugu provider](https://github.com/Hmbown/CodeWhale/pull/3748)
**Author:** lerugray | **Status:** CLOSED  
Adds Sakana provider following the moonshot/minimax pattern. Supports `FUGU_API_KEY` auth and `fugu` reasoning model.

### 9. [#3782 — Clarify Hotbar help shortcuts](https://github.com/Hmbown/CodeWhale/pull/3782)
**Author:** roian6 | **Status:** OPEN  
Documents Hotbar chord limitations (only Alt+1 through Alt+8 when no modal owns input) directly in help UI.

### 10. [#3789 — Show safety policy in /status](https://github.com/Hmbown/CodeWhale/pull/3789)
**Author:** cyq1017 | **Status:** OPEN  
Refs #3406. Adds safety posture row to `/status` reporting sandbox/network mode (Plan/Agent/Auto/Yolo).

---

## 5. Feature Request Trends

| Trend | Evidence | Priority |
|-------|----------|----------|
| **Constitution-first setup wizard** | #3402, #3793, #3806, #3792, #3404 | Highest — release-blocking for v0.8.67 |
| **Guided, not blank-slate, configuration** | #3793, #3406, #3830 | High — recurrent user frustration |
| **Clean separation of mode/permission knobs** | #3736, #3275, #3406 | High — structural security concern |
| **Dynamic MCP server startup from chat** | #3866, #3869 | Medium — enabling community extensions |
| **Localization / multi-language support** | #3412, #3402, #3793 | Medium — growing community interest |
| **Modal/popup UI overhaul** | #3829, #3831 | Medium — release-blocking but narrow scope |

---

## 6. Developer Pain Points

1. **Agent autonomy without guardrails** — Issue #3275 shows CodeWhale making unsolicited modifications. Community wants explicit confirmation steps before any code change.

2. **Overlapping permission models** — Four overlapping knobs (Issue #3736) cause confusion and potential security bypass. Devs want a unified, auditable policy.

3. **Pre-rebrand path contamination** — Issue #3864: lingering `.deepseek/` paths break state management. Simple fix, but reflects broader migration friction.

4. **Stale/frozen UI state** — Issue #3837: Agents sidebar doesn't reflect real-time sub-agent completion. Users can't trust the UI during multi-agent workflows.

5. **Windows-specific breakage** — Copy/paste GUI override (Issue #3868) and SDK path issues (PR #3578) suggest ongoing platform parity gaps.

6. **Dead code accumulation** — Multiple cleanup PRs (#3879, #3872, #3871, #3845, #3837) indicate the codebase has accumulated significant dead weight since the rebrand.

7. **Fleet complexity** — Issue #3863 highlights that Fleet/workflow orchestration lacks a natural-language entry point, requiring manual JSON editing in an AI-agent era.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*