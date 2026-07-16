# AI CLI Tools Community Digest 2026-07-16

> Generated: 2026-07-16 01:19 UTC | Tools covered: 9

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

# AI CLI Developer Tools Ecosystem — Cross-Tool Comparison Report
**Date:** 2026-07-16

---

## 1. Ecosystem Overview

The AI CLI tools ecosystem is experiencing rapid divergence in both maturity and community engagement. Claude Code and OpenAI Codex dominate community conversation volume, with deep-seated reliability crises around unbounded agent costs and Windows packaging quality setting them apart from more stable competitors. Gemini CLI and OpenCode show strong maintenance velocity with focused security patches and UX fixes, while Qwen Code emerges as the most architecturally ambitious project with multi-workspace daemon proposals and enterprise channel integrations. Smaller tools like Pi (mono) and DeepSeek TUI continue refining niche performance and platform-specific issues, while Kimi Code CLI shows minimal community activity, suggesting either early-stage development or internal-focused iteration. The dominant theme across all tools remains the tension between agent autonomy and cost safety, with every major tool reporting some form of uncontrolled agent spawning or runaway token consumption.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Active PRs (24h) | Releases (24h) | Community Engagement Signal | Dominant Theme |
|------|------------------|------------------|----------------|---------------------------|----------------|
| **Claude Code** | 10 (critical) | 3 | 1 (patch) | 31 comments on top issue | Cost safety crisis, VS Code parity |
| **OpenAI Codex** | 10 | 10 (high velocity) | 3 (alpha) | 172 comments on #23794 | Windows ARM64 crash, model API breaks |
| **Gemini CLI** | 10 | 10 | 1 (nightly) | 10 comments on #22323 | Agent hanging, silent failures |
| **Copilot CLI** | 10 | 0 | 1 (patch) | 76 👍 on #223 | MCP OAuth broken, enterprise auth |
| **OpenCode** | 10 | 10 | 1 (patch) | 18+ comments on #36997 | Desktop UI regressions, security |
| **Pi (mono)** | 10 | 10 | 0 | 75 comments on #4945 | Codex reliability, Windows stability |
| **Qwen Code** | 10 | 10 | 3 (nightly + cua-driver) | 23 comments on #6378 | Multi-workspace daemon, enterprise IM |
| **Kimi Code CLI** | 0 | 1 | 0 | 0 comments | Telemetry unification (quiet) |
| **DeepSeek TUI** | 10 | 10 | 0 | 29 comments on #3368 | Platform stability, modularization |

**Key Observations:**
- **Claude Code** has the most critical issues per comment count (31 on #68619), reflecting acute user pain
- **OpenAI Codex** leads in PR velocity (10 active) but is also carrying the highest-commented issue in the ecosystem (172 comments)
- **Qwen Code** is the only tool shipping pre-release artifacts (cua-driver v0.7.2 with notarized macOS binaries)
- **Kimi Code CLI** is effectively dormant in community activity — lowest signal across all metrics

---

## 3. Shared Feature Directions

### Agent Cost & Safety Controls (All major tools)
- **Uncontrolled recursive spawning:** Claude Code (#68619, #69578), Gemini CLI (#22323), Qwen Code (#5239)
- **Per-turn/task limits needed:** Claude Code (subagent depth caps), Gemini CLI (recursive reasoning caps, PR #28164), Copilot CLI (session limit overflow #4097), Qwen Code (fractional validation #6914)
- **Token/cache transparency demand:** OpenAI Codex (#23794 — 170 👍), Copilot CLI (#2052), Pi (#5263)

### MCP/Plugin Integration Stability (Claude Code, Copilot CLI, Qwen Code, Pi)
- **OAuth flow failures:** Copilot CLI (#4096, #4084 — Atlassian MCP), Qwen Code (#6970 — dot-constrained tool names)
- **Tool visibility gaps:** Copilot CLI (MCP servers show "Connected" but no tools), Pi (extension selector #6688)
- **Permission boundary bypass:** Claude Code (#74916 — PowerShell allowlist), OpenCode (#37155 — self-escalation via opencode.json)

### Session Management & Identity (Claude Code, Copilot CLI, OpenCode, Qwen Code)
- **Invisible/duplicate sessions:** Claude Code (#77463 — "kids in a trenchcoat"), Copilot CLI (#4147 — arrow key data loss)
- **Compaction data loss:** Claude Code (#74990 — skills system drop), OpenCode (#17340 — context overflow), Pi (#6647 — transient failure), Qwen Code (#6936 — memory instructions waste)
- **Multi-session/workspace support:** Qwen Code (#6378 — multi-workspace daemon), Copilot CLI (#1979 — remote session), DeepSeek TUI (#3306 — modularization)

### Cross-Platform Parity (All tools with desktop/CLI splits)
- **VS Code extension lag:** Claude Code (workflows, remote control startup lagging)
- **Windows-specific crashes:** OpenAI Codex (#33381 — ARM64 crash-loop), Pi (#6692 — spawn ENOENT), DeepSeek TUI (IME deadlock, crossterm poll)
- **Linux webview failures:** OpenAI Codex (#32530 — net::ERR_FAILED on Ubuntu), Copilot CLI (#4053 — NFS hangs)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Pi (mono) | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|----------|-----------|-----------|--------------|
| **Primary User** | Power devs, cost-sensitive | OpenAI API users | GCP/enterprise | GitHub ecosystem | Desktop-first developers | Extension developers | Chinese enterprise, AI researchers | Chinese power users, TUI enthusiasts |
| **Technical Strengths** | Subagent orchestration, skills system | Rust CLI, multi-model support | A2A protocol, security-first | GitHub auth integration, MCP ecosystem | Desktop agent UX, agent mode switching | Lightweight, extensible via npm | Daemon architecture, enterprise channels | Minimal TUI, custom provider support |
| **Biggest Weakness** | Uncontrolled costs, VS Code parity | Windows packaging, model API churn | Agent hanging, configuration ignored | MCP OAuth broken, voice mode non-functional | UI regressions, compaction fragility | Codex reliability, Windows stability | CI flakiness, validation gaps | Platform-specific freezes, CJK encoding |
| **Innovation Signal** | Code quality pipeline plugin (#77916) | External agent memory migration (#33444) | Zero-dependency sandboxing (#19873) | No PR activity in 24h | Prompt injection boundaries (#37187) | SQLite session storage (#6594) | Multi-workspace daemon RFC (#6378) | Slash-command infrastructure (#1887+) |
| **Community Sentiment** | Frustrated (cost crisis) | Polarized (feature removal vs. new features) | Engaged (high-quality issue reports) | Frustrated (auth regression) | Pushback on redesign | Mixed (reliability vs. extensibility) | Active (enterprise adoption) | Patient (long-standing bugs) |

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid iteration, growing communities)
- **Qwen Code** — Most architecturally ambitious. Three nightly releases in 24h, multi-workspace daemon RFC with 23 comments, active enterprise IM integration (DingTalk, WeCom). Strong signal of Chinese enterprise adoption.
- **OpenAI Codex** — Highest PR velocity (10 active, 3 alpha releases). Multiple feature-import PRs (Cursor settings, external agent memory) suggest aggressive competitive positioning against Claude Code.

### Stable Maturity (Established user base, focused maintenance)
- **Claude Code** — Largest community but facing existential cost-safety crisis. Patch releases continue but PR velocity low (3) relative to issue volume. The "infinite subagent recursion" cluster (#68619, #69578, #72732, #77834) is the most critical reliability issue in the ecosystem.
- **Gemini CLI** — Strong PR velocity (10) with clear security focus (bash substitution patch, path trust checks). Community issues are well-documented and specific. Maintainers are responsive (PRs merging same-day).

### Mid-Maturity (Growing with platform-specific challenges)
- **OpenCode** — Desktop UI redesign faced significant community pushback (#36997 — 18+ comments, multiple duplicates). Compaction and security patches show healthy engineering discipline. Adoption of prompt injection boundaries (#37187) is a best practice signal.
- **Pi (mono)** — Active extension ecosystem (12 PRs in 24h). SQLite session storage (#6594) and xAI OAuth (#6651) show expanding provider support. Windows-specific issues remain the top friction point.

### Lower Activity/Emerging
- **Copilot CLI** — Near-zero PR velocity (0 active) despite significant open issues. Enterprise auth (#223 — 76 👍) and MCP OAuth failures (#4096) are festering. Community is frustrated but engaged.
- **DeepSeek TUI** — Heavy refactoring focus (modularization issues #3306–#3314). TelecompJS provider support (#4370) expands Chinese user access. Performance-fix PR (#3902) closed five issues — shows maturation.
- **Kimi Code CLI** — Effectively dormant. Single PR (#2500 for telemetry alignment) with no community discussion. Either pre-release stealth mode or low internal priority.

---

## 6. Trend Signals

### Industry Trend 1: The Cost Safety Reckoning
**Signal:** Claude Code (#68619 — 31 comments, 10 👍), Gemini CLI (#22323), Copilot CLI (#4097), Qwen Code (#6914)

Multiple user reports of agents burning hundreds of dollars in a single session through uncontrolled subagent spawning or infinite retry loops. This is the highest-priority cross-tool issue. The ecosystem is realizing that agent autonomy without hard cost boundaries is financially dangerous. Tools that solve this (Qwen Code's Todo Stop Guard #6946, Gemini CLI's recursive reasoning caps #28164) will gain trust.
- **Takeaway:** Cost-safe defaults, per-request token limits, and subagent depth caps should be table stakes for any agentic CLI tool.

### Industry Trend 2: Windows as the Weakest Link
**Signal:** OpenAI Codex (#33381 — 25 👍 ARM64 crash-loop), Pi (#6692 — spawn ENOENT), DeepSeek TUI (IME deadlock, crossterm poll), Copilot CLI (#4147 — arrow key data loss)

Every tool with a desktop or CLI component reports Windows-specific regressions ranging from packaging failures (ARM64, serialport.node) to input handling (IME, arrow keys, keyboard shortcuts). The Windows developer market is growing, but tool quality on the platform is lagging significantly.
- **Takeaway:** Cross-platform CI with actual Windows hardware testing is not optional. ARM64-native builds will be a differentiator in the next 6 months.

### Industry Trend 3: Model API Stability Is a Feature
**Signal:** OpenAI Codex (#31846 — `reasoning.summary` unsupported), Gemini CLI (subagent model compatibility), Copilot CLI (#4038 — empty user messages), Qwen Code (#6970 — dot-constrained tool names)

Model API churn — silent parameter rejection, forced agent version changes (#31097), and schema incompatibilities — is eroding developer trust in agent tools. Power users want *stable, versioned APIs* from both LLM providers and tool interfaces.
- **Takeaway:** Tools should abstract model-specific quirks behind stable internal APIs. Model-level compatibility testing should be part of the release pipeline.

### Industry Trend 4: The MCP/Plugin Integration Bottleneck
**Signal:** Copilot CLI (#4096, #4084, #4086, #4089, #4017 — OAuth failures), Claude Code (#74916 — allowlist bypasses), OpenCode (#37155 — self-escalation), Qwen Code (#6970 — tool name constraints)

Model Context Protocol (MCP) is becoming standard, but the integration experience is broken: OAuth tokens don't bridge to spawned sessions, tool names are silently rejected by stricter providers, and permission boundaries are loosely enforced. The promise of "plug and play" is not yet realized.
- **Takeaway:** OAuth credential propagation, cross-provider tool name validation, and granular permission scoping are essential for MCP to go mainstream.

### Industry Trend 5: The Enterprise IM Integration Opportunity
**Signal:** Qwen Code (#6443 — DingTalk interactive cards, #6883 — WeCom), DeepSeek TUI (#4370 — Telecom provider), Claude Code (remote control requests)

Chinese enterprise IM platforms (DingTalk, WeCom) are emerging as first-class interfaces for AI dev tools, not afterthoughts. Qwen Code's aggressive investment in channel integrations suggests a strategic bet on enterprise adoption through messaging platforms rather than traditional CLIs.
- **Takeaway:** For tools targeting enterprise adoption, native integration with business messaging platforms (Teams, Slack, DingTalk, WeCom) is becoming table stakes, particularly in APAC markets.

### Industry Trend 6: Desktop UI Redesigns Are High-Risk
**Signal:** OpenCode (#36997 — Plan/Build toggle missing, 18+ comments, multiple duplicates), Pi (#6050 — scrollback clearing), Copilot CLI (#4146 — invisible selection highlighting)

Forcible UI redesigns without opt-out paths generate intense backlash, especially when they remove functionality (OpenCode's missing agent toggle) or introduce regressions (Pi's scrollback clearing). Users developing muscle memory on existing UIs are highly sensitive to disruption.
- **Takeaway:** UI overhauls should ship alongside the old layout (opt-in), provide migration paths, and avoid regressing core workflows like session switching and agent mode selection.

---

*Report generated from 2026-07-16 community digest data across 9 major AI CLI developer tools. Data reflects a single-day snapshot and may not capture long-term trends.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the Claude Code Skills repository.

---

## Claude Code Skills Community Highlights Report

*Data as of 2026-07-16 | Source: github.com/anthropics/skills*

---

### 1. Top Skills Ranking

The following pull requests represent the most-discussed Skill submissions, ranked by community engagement and discussion depth.

1.  **Skill-Creator Bug Fixes (PR #1298)** — Fixes for `run_eval.py` that caused persistent 0% recall scores on Windows and Linux. The discussion centers on a critical bug where the skill-optimization loop was optimizing against noise, making the entire skill-creator pipeline unreliable. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1298)

2.  **document-typography (PR #514)** — A typographic quality-control skill for AI-generated documents. It targets orphan words, widow paragraphs, and numbering misalignment. Discussion highlights that these issues affect nearly every document Claude generates but are rarely requested by users. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/514)

3.  **ODT Skill (PR #486)** — Adds support for OpenDocument Format files (.odt, .ods). The community discussion reveals strong demand for LibreOffice / open-source document workflow integration. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/486)

4.  **Skill Quality & Security Analyzers (PR #83)** — Two meta-skills for evaluating other skills across five quality dimensions and security posture. Discussion focuses on the need for community quality standards before marketplace growth. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/83)

5.  **testing-patterns (PR #723)** — A comprehensive testing skill covering the "Testing Trophy" model, unit testing (AAA pattern), React Testing Library, Playwright E2E, snapshot testing, and accessibility testing. High engagement from developers seeking structured test guidance. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/723)

6.  **Self-Audit / Reasoning Quality Gate (PR #1367)** — A skill that audits AI output before delivery: mechanical file verification followed by a four-dimension reasoning quality audit. The discussion explores how to prevent delivery of hallucinated or incomplete artifacts. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/1367)

7.  **pyxel Skill (PR #525)** — Integrates with the Pyxel retro game engine MCP server for pixel-art / 8-bit game development. Community interest reflects demand for creative coding workflows. **Status:** Open | [View PR](https://github.com/anthropics/skills/pull/525)

---

### 2. Community Demand Trends

Analysis of the most active Issues reveals several clear demand clusters:

| Demand Cluster | Supporting Issues | Key Insight |
|---|---|---|
| **Enterprise / Org Sharing** | #228 (14 comments, 7 👍) | Strong demand for org-wide skill libraries and direct sharing links instead of manual `.skill` file distribution |
| **Skill-Creator Reliability** | #556 (12 comments), #1169 (3 comments), #1061 (3 comments) | The `run_eval.py` 0% recall bug is the single most impactful blocker for skill authors; three distinct issues report the same root cause |
| **Security & Trust Boundaries** | #492 (34 comments, 2 👍) | Community skills under the `anthropic/` namespace create impersonation risk; demands namespace separation and permission gating |
| **Agent Governance / Safety** | #412 (6 comments), #1385 (3 comments) | Users want pre-task calibration, adversarial review, and delivery verification patterns for production agent systems |
| **Duplicate Content / Plugin Conflicts** | #189 (6 comments, 9 👍) | `document-skills` and `example-skills` plugins install identical content; community wants deduplication and clear responsibility boundaries |
| **MCP / API Exposure** | #16 (4 comments) | Demand to expose Skills as MCP tools for programmatic invocation and standardization |

The **skill-creator reliability crisis** (Issues #556, #1169, #1061) is the most urgent community pain point: the optimization loop returns `recall=0%` on every iteration, rendering the primary tool for skill development effectively broken.

---

### 3. High-Potential Pending Skills

These PRs are actively discussed, not yet merged, and address clear community needs:

| Skill | PR | Discussion Focus | Why It Might Land Soon |
|---|---|---|---|
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | Orphan/widow prevention, numbering alignment | Solves a universal document-quality problem; low implementation complexity |
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical verification + reasoning quality gate | Directly addresses quality assurance needs raised in Issues #412 and #1385 |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full-stack testing methodology | Strong developer demand; fills a gap in the existing skills collection |
| **pyxel** | [#525](https://github.com/anthropics/skills/pull/525) | Retro game development integration | MCP-based; low integration risk; authored by the pyxel maintainer |
| **skill-quality-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Five-dimension skill quality evaluation | Community needs quality standards before marketplace scaling; complementary to security analyzer |

---

### 4. Skills Ecosystem Insight

**The community's most concentrated demand is for a reliable, cross-platform skill-development toolchain** — specifically, fixing the `run_eval.py` crash/recall bug on Windows and Linux — before investing in new Skill content, as the current optimization loop is effectively broken for all contributors.

---

# Claude Code Community Digest — July 16, 2026

## Today's Highlights

A new patch release (v2.1.211) shipped with subagent telemetry improvements and permission preview fixes, but the community conversation remains dominated by a growing crisis around uncontrolled recursive agent spawning that has caused hundreds of dollars in token burn for multiple users. The VS Code extension continues to lag behind the CLI in feature parity, with the `/workflows` command and session management pain points surfacing repeatedly this week.

---

## Releases

**v2.1.211** — [Release](https://github.com/anthropics/claude-code/releases/tag/v2.1.211)
- Added `--forward-subagent-text` flag and `CLAUDE_CODE_FORWARD_SUBAGENT_TEXT` env var to include subagent thinking/output in stream-json output
- Fixed permission previews relayed to chat channels not neutralizing bidirectional-override, zero-width, and look-alike characters

---

## Hot Issues

1. **[#68619] — Subagent Spawning Triggers Infinite Recursion & Catastrophic Token Burn** (31 comments, 10 👍)
   Critical regression: subagents spawn 50+ levels deep ignoring `CLAUDE_CODE_FORK_SUBAGENT=0`. Permission denials trigger more spawning instead of stopping. Multiple compounding bugs create a "perfect storm" for unbounded costs. [Issue](https://github.com/anthropics/claude-code/issues/68619)

2. **[#53940] — Cowork Edit/Write Tools Silently Truncate Files via Byte-Conservation Buffer Cap** (43 comments, 16 👍)
   Deterministic bug on Windows: files are silently truncated when operations hit a hidden buffer cap. No warning to the user — data silently lost. [Issue](https://github.com/anthropics/claude-code/issues/53940)

3. **[#69578] — $27.60 Unexpected Charge from ~800K Token Sub-Agent Loop** (8 comments, 1 👍)
   User reports a single session burned ~800K tokens with near-zero useful output due to unbounded sub-agent recursion, triggering overage charges beyond their plan. [Issue](https://github.com/anthropics/claude-code/issues/69578)

4. **[#77834] — Agent Fan-Out Pays ~47K Uncached Startup Tokens Per Small Task** (3 comments)
   When fanning out to many small agents, each pays a massive uncached startup cost, causing multi-million-token sessions for trivial parallel work. [Issue](https://github.com/anthropics/claude-code/issues/77834)

5. **[#74990] — `/compact` and Auto-Compaction Drop Entire Available Skills System Reminder** (3 comments, 1 👍)
   Compaction silently strips the skills system prompt. `/reload-skills` reports "no changes," leaving the session unable to use installed skills. [Issue](https://github.com/anthropics/claude-code/issues/74990)

6. **[#77463] — Session Instances Invisible to User — The "Kids in a Trenchcoat" Problem** (3 comments)
   Fork/resume divergence across multiple surfaces causes conflicting writes, token burn, and no instance identity anywhere. Users have no visibility into which process owns a session. [Issue](https://github.com/anthropics/claude-code/issues/77463)

7. **[#60385] — Remote Control: MCP Permission Prompts Never Surface in Web UI (CLOSED)** (20 comments)
   Permission approval for non-read MCP tools never renders in the web UI when using `--remote-control`. Blocks until manually answered in the TTY — defeating the remote-control purpose. [Issue](https://github.com/anthropics/claude-code/issues/60385)

8. **[#74916] — PowerShell Script Block Subexpressions Still Bypass Allowlist (Re-file)** (3 comments)
   Stale-bot closed the original (#52926) despite the bug being reproducible. PowerShell blocks/subexpressions slip past the allowlist and prompt the user anyway. [Issue](https://github.com/anthropics/claude-code/issues/74916)

9. **[#62149] — VS Code Extension Ignores `remoteControlAtStartup`** (8 comments, 5 👍)
   Third filing after two were auto-misrouted by the duplicate bot. The setting is silently ignored, forcing users to manually restart the extension. [Issue](https://github.com/anthropics/claude-code/issues/62149)

10. **[#77950] — Nested Grandchild Background Agents Can't Message Their Direct Parent** (2 comments)
    Background agents spawned two levels deep stall indefinitely; completion messages never reach their direct parent, ending up lost in the orchestration tree. [Issue](https://github.com/anthropics/claude-code/issues/77950)

---

## Key PR Progress

1. **[#77916] — Add `code-quality-pipeline` Plugin** (OPEN)
    New skill-based plugin defining quality gates between "code written" and "code merged." Gate A runs sequential checks per file; Gate B handles end-to-end validation. [PR](https://github.com/anthropics/claude-code/pull/77916)

2. **[#77709] — Add Settings Example: Official Marketplace Only** (OPEN)
    Demonstrates how to restrict plugin marketplaces exclusively to the official Anthropic marketplace via `strictKnownMarketplaces`. [PR](https://github.com/anthropics/claude-code/pull/77709)

3. **[#77705] — Fix: `validate-settings.sh` False-Passes on Files Without Frontmatter** (OPEN)
    Shell script's "Check 3" incorrectly passes files with zero `---` markers — emits raw Bash error and falls through instead of rejecting. [PR](https://github.com/anthropics/claude-code/pull/77705)

*(Only 3 PRs were active in the last 24 hours — see the "Hot Issues" section for critical bugs needing PRs.)*

---

## Feature Request Trends

- **Multi-Account Management (Issue #18435):** 657 👍, 131 comments — the most upvoted open feature request. Users want profile switching for multiple Claude accounts within the desktop app, particularly for team/individual workspace separation.
- **Workflows in VS Code Extension (Issues #72292, #74585, #75146):** Multiple duplicate requests for the `/workflows` command to work in VS Code, indicating strong demand for IDE parity with the TUI.
- **Configurable Auto-Compact Threshold (Issue #70681):** Users want control over when compaction triggers, as the current behavior can drop context unexpectedly.
- **Cowork Folder Context Management (Issue #40043):** 55 👍 for the ability to remove local folders from a Cowork project's context without restarting.

---

## Developer Pain Points

- **Uncontrolled Recursive Agent Spawning (Issues #68619, #69578, #72732, #77834):** The dominant theme of the week. Multiple users report unbounded sub-agent recursion resulting in hundreds of dollars in token burn. Permission denials trigger more spawning instead of halting. This cluster of related bugs represents the highest-priority reliability and cost-safety issue.
- **Session Identity & Concurrency (Issues #77463, #75761, #69364):** Users cannot tell if a session is already live. `--continue` / `--resume` spawns twin processes that act on the same repo concurrently, causing corrupted state and unbilled token burn.
- **VS Code Extension Parity Gap (Issues #62149, #72292, #74585):** Multiple features (workflows, remote control startup, session identity) work in the CLI but are broken or missing in the VS Code extension.
- **Compaction Data Loss (Issue #74990):** The compaction feature intended to manage context is instead silently dropping critical system prompts like skills configuration.
- **False-Positive/False-Negative Permission Guards (Issues #74916, #69461):** Both directions of failure exist — PowerShell allowlist bypasses on Windows and false-positive delete path detection.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-16

## Today's Highlights
Windows ARM64 users face a critical crash-loop bug (#33381) that makes the desktop app unusable, with multiple related `serialport.node` failures now documented. Meanwhile, the team is actively merging safety improvements (dangerous-command detection) and infrastructure migrations (external agent memory, Cursor import support) across the `release/0.144` and `main` branches. The community continues to converge on demands for full GPT-5.6 Sol context windows, multi-chat support, and better subagent routing controls.

## Releases
Three new alpha releases for the Rust CLI were published in the last 24 hours — all version `0.145.0-alpha` (`.13`, `.14`, `.15`). No changelog details are available beyond the version bump, indicating iterative pre-release stabilization work.

## Hot Issues
1. **[[#33381](https://github.com/openai/codex/issues/33381)] Windows ARM64 crash-loop (35 comments, 25 👍)**  
   App exits ~10–15 seconds after launch; Crashpad minidumps point to `serialport.node` delay-load failure (`0xC06D007F`). Community is calling for an immediate ARM64-native build or blocking x64 emulation for the affected addon. Multiple closed duplicates (#33415, #33380) confirm the pattern.

2. **[[#23794](https://github.com/openai/codex/issues/23794)] [CLOSED] Context/token usage indicator removed (172 comments, 170 👍)**  
   The most-commented issue in the repo. Users strongly resent the disappearance of the visible context/token counter in the desktop app. Closed without a public resolution, indicating a design decision that many consider regressive.

3. **[[#31846](https://github.com/openai/codex/issues/31846)] GPT-5.3 Codex Spark fails with "Unsupported parameter: reasoning.summary" (26 comments, 33 👍)**  
   Model-level parameter incompatibility blocks Spark usage. Users on Pro subscriptions are stuck — the app sends a parameter the model doesn't accept. High upvotes suggest widespread impact.

4. **[[#33375](https://github.com/openai/codex/issues/33375)] Repeated serialport.node delay-load failures cause UI lag (22 comments, 13 👍)**  
   A companion to #33381: even on x64 Windows, the same `serialport.node` dependency triggers repeated failures that degrade UI responsiveness. Suggests a broader packaging issue, not just ARM64.

5. **[[#30178](https://github.com/openai/codex/issues/30178)] In-app Browser crashes the main app (19 comments)**  
   Webview navigation leads to full app crashes on Windows. Still open after 20 days; the lack of fix is frustrating for users who rely on the built-in browser for OAuth flows and documentation.

6. **[[#23198](https://github.com/openai/codex/issues/23198)] Windows app extremely slow (16 comments, 44 👍)**  
   Long-standing performance regression (open since May) with high community resonance. Users report the app is unusable on capable hardware, but no root cause has been found.

7. **[[#32782](https://github.com/openai/codex/issues/32782)] GPT-5.6 Sol omits agent_type in spawn_agent (8 comments, 9 👍)**  
   Blocks custom-agent routing because the schema changes between model versions. Power users want stability in the subagent API — this is the third issue in two weeks on agent-type related regressions.

8. **[[#31097](https://github.com/openai/codex/issues/31097)] GPT-5.5 forces MultiAgentV2 despite disable setting (8 comments, 8 👍)**  
   User config for agent version is silently ignored. Users want explicit, honored control over which agent paradigm is used.

9. **[[#32530](https://github.com/openai/codex/issues/32530)] VS Code panel stuck loading on Linux (5 comments, 8 👍)**  
   Local webview assets fail with `net::ERR_FAILED`. Intermittent, but blocks the IDE extension entirely when hit. Ubuntu 26.04 users are most affected.

10. **[[#19669](https://github.com/openai/codex/issues/19669)] Slack connector stale OAuth after revoke (3 comments, 2 👍)**  
   Connector doesn't support re-authentication after token revocation — no hot-swap path for multi-account Slack users. A niche but painful UX gap for enterprise deployments.

## Key PR Progress
1. **[[#33464](https://github.com/openai/codex/pull/33464) Strengthen forced `rm` command detection**  
   Expands dangerous-command heuristics to catch `rm` inside control flow, substitutions, and wrapper scripts. Merged same-day — a quick safety win.

2. **[[#33455](https://github.com/openai/codex/pull/33455) [release/0.144] Backport dangerous-command detection**  
   Cherry-picks seven commits from internal PR #1942 to the `release/0.144` branch, bringing forced-rm detection to the stable channel. Also enables detection in danger-full-access mode.

3. **[[#33457](https://github.com/openai/codex/pull/33457) Use final answers in turn history summaries**  
   Improves conversation compaction by tracking only `final_answer`-phase agent messages, excluding commentary. Crucial for reducing token waste in long-running agent sessions.

4. **[[#33454](https://github.com/openai/codex/pull/33454) Track prompt cache write token usage**  
   Surfaces `cache_write_tokens` from response input token details. Exposes new telemetry across protocol, app-server, and TypeScript SDK — critical for cost-conscious API users.

5. **[[#33456](https://github.com/openai/codex/pull/33456) Move external agent migration into its crate**  
   Refactors migration logic out of `codex-app-server` into a dedicated `codex-external-agent-migration` crate. Clean separation that should speed up third-party agent onboarding.

6. **[[#33444](https://github.com/openai/codex/pull/33444) Add external agent memory migration**  
   Feature-gated support for importing project memory Markdown files into Codex's memory extension workspace. A key step for users migrating from Claude Code or other agent platforms.

7. **[[#33426](https://github.com/openai/codex/pull/33426) Add Cursor support to setup import**  
   `/import` flow now detects and imports Cursor settings, sandbox permissions, MCP servers, project instructions, and chat sessions. Directly competitive with Cursor's adoption playbook.

8. **[[#33432](https://github.com/openai/codex/pull/33432) Preserve paginated history for spawned subagents**  
   Ensures that subagents inherit the paginated history mode and parent model context when forked. Fixes a class of context-loss bugs in multi-agent workflows.

9. **[[#33425](https://github.com/openai/codex/pull/33425) Refresh host skill catalogs through world state**  
   Host skills now update mid-thread without full re-injection. Reduces redundancy and fixes stale-skill references in long-running sessions.

10. **[[#31781](https://github.com/openai/codex/pull/31781) Bound executor-controlled HTTP response buffering**  
    Limits per-frame payload size from remote exec-servers, preventing memory exhaustion attacks. Still open — a security-focused fix for the multi-tenant execution model.

## Feature Request Trends
- **Full GPT-5.6 Sol context window opt-in** (#33306): Users with Pro subscriptions want to bypass conservative compaction defaults and use the full 1.05M context.
- **Multi-chat / multi-tab support** (#13036): Single-thread limitation is the top UX complaint for multitasking and multi-agent workflows.
- **Configurable stream reconnect/backoff** (#16164): Hard-coded backoff makes some provider setups unusable; users want config.toml overrides.
- **Custom-agent routing stability** (#32782, #31097): The `agent_type` field being optional or silently forced is breaking custom agent configurations across model versions.
- **Cross-platform parity** (multiple): Linux webview assets, Windows ARM64 builds, macOS SSH key handling — users want consistent behavior across all platforms.

## Developer Pain Points
- **Windows packaging quality** is the #1 pain point: three active issues (crash-loops, UI lag, serialport failures) all trace to a poorly bundled `serialport.node` dependency. The ARM64 situation is especially acute.
- **Model API inconsistency** frustrates power users: parameters like `reasoning.summary` are silently rejected, `agent_type` appears or disappears between model versions, and `MultiAgentV2` is forced despite user settings.
- **Telemetry regression** (#23794) shows that removing user-visible metrics (token counters) erodes trust — the 170 👍 signal strong community desire for transparency in local usage.
- **SSH remote workflow fragility** (#23037, #27284, #30808): keyboard-interactive auth, symlinked paths, and state DB sync failures make remote development unreliable for enterprise teams.
- **Authentication friction** (#28349, #19669): phone-number-based login blocks enterprise accounts, and connector OAuth refresh is manual — both issues that stall team adoption.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-16

## Today's Highlights
Today saw significant progress on core stability with critical fixes landing for `400 Bad Request` errors after tool call cancellations and a security patch blocking `$VAR`/`${VAR}` bash expansion bypasses. The community remains active around agent lifecycle issues, with the "subagent recovery after MAX_TURNS" bug continuing to draw engagement. A new nightly build (`v0.52.0-nightly.20260715`) was released.

## Releases
- **v0.52.0-nightly.20260715.gfa975395b** — Nightly release with automated version bump. No detailed changelog beyond the diff from the previous nightly.
  [Compare v0.52.0-nightly.20260714...v0.52.0-nightly.20260715](https://github.com/google-gemini/gemini-cli/compare/v0.52.0-nightly.20260714.gfa975395b...v0.52.0-nightly.20260715.gfa975395b)

## Hot Issues (Top 10)

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, Bug, 10 comments)
   *Why it matters:* A `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` despite hitting its maximum turn limit before performing any analysis. This is a silent logic failure that masks agent malfunction. Community reaction: high engagement (10 comments, 2 👍).

2. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, Enhancement, 8 comments)
   *Why it matters:* Proposes making Gemini 3's native bash capabilities first-class by providing a sandboxed execution environment. This could fundamentally change how agents interact with the OS. Community reaction: 8 comments, 1 👍 — active discussion among maintainers.

3. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (P1, Eval Infrastructure, 7 comments)
   *Why it matters:* Epic tracking the evolution of behavioral evals from 0 to 76 tests across 6 Gemini models. Shows the team's commitment to systematic quality measurement. Community reaction: low public engagement but high internal priority (P1, maintainer-only).

4. **[#22745 — Assess impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (P2, Feature, 7 comments)
   *Why it matters:* Could dramatically reduce token usage and turn count by enabling precise method-bound reads instead of line-based file scanning. Community reaction: 7 comments, 1 👍 — developers are interested in smarter code understanding.

5. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, Bug, 7 comments)
   *Why it matters:* Simple folder creation hangs indefinitely when deferred to the generalist agent. High impact on developer productivity. Community reaction: most upvoted issue today (8 👍), reflecting widespread frustration.

6. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, Bug, 6 comments)
   *Why it matters:* Custom skills and sub-agents are effectively ignored by the model unless explicitly instructed. Undermines the value proposition of custom agent configuration. Community reaction: 6 comments, 0 👍 — technical but important.

7. **[#25166 — Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, Bug, 4 comments)
   *Why it matters:* Simple CLI commands hang after completion, showing "Awaiting user input." Extremely disruptive to workflow. Community reaction: 4 comments, 3 👍 — strong community validation.

8. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, Bug, 5 comments)
   *Why it matters:* Auto Memory keeps surfacing irrelevant transcript candidates, wasting model context and compute. Community reaction: 5 comments, 0 👍 — maintainer-heavy discussion.

9. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, Bug, 4 comments)
   *Why it matters:* Wayland users on Linux cannot use the browser agent at all. Community reaction: 4 comments, 1 👍 — limited but consistent reporting.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, Customer Issue, 3 comments)
    *Why it matters:* The agent occasionally uses `git reset --force` and other destructive commands when safer alternatives exist. Critical for production safety. Community reaction: 3 comments, 1 👍 — growing concern.

## Key PR Progress (Top 10)

1. **[#28410 — fix(core): shorten MCP tools/list discovery timeout](https://github.com/google-gemini/gemini-cli/pull/28410)** (P1, Area: Agent)
   *What it does:* Prevents CLI startup from freezing for 10 minutes when an MCP server doesn't respond. Sets a short default timeout for `tools/list` discovery. (Open, by sahilempire)

2. **[#28407 — fix(core,a2a): group cancelled tool responses and coalesce consecutive roles](https://github.com/google-gemini/gemini-cli/pull/28407)** (P1, Area: Core)
   *What it does:* Fixes the `400 Bad Request` error that broke chat continuity after users cancelled/rejected tool calls. A high-impact stability fix. (Merged, by luisfelipe-alt)

3. **[#28403 — fix(core): block $VAR and ${VAR} variable expansion bypass](https://github.com/google-gemini/gemini-cli/pull/28403)** (P0/P1, Security)
   *What it does:* Patches GHSA-wpqr-6v78-jr5g by extending `detectBashSubstitution()` to catch `$VAR` and `${VAR}` patterns that previously bypassed detection. (Open, by thalha-a9)

4. **[#28406 — fix(availability): apply modelIdResolutions to tool sub-agent model configs](https://github.com/google-gemini/gemini-cli/pull/28406)** (P1, Area: Agent)
   *What it does:* Ensures `web-search`, `web-fetch`, and other utility tools respect user API key preview access, preventing `INVALID_MODEL` errors. (Open, by vedhakoushik)

5. **[#28164 — fix(core): limit recursive reasoning turns per single user request](https://github.com/google-gemini/gemini-cli/pull/28164)** (P2, Area: Core)
   *What it does:* Caps recursive reasoning at 15 turns per user request to prevent infinite loops. Users can customize via `maxSessionTurns`. (Open, by amelidev)

6. **[#28405 — fix: prevent scroll position jump when user scrolls up during content updates](https://github.com/google-gemini/gemini-cli/pull/28405)** (P1, Area: Core)
   *What it does:* Fixes a long-standing UX bug where scrolling up to review changes would cause the viewport to jump when new content arrives. (Open, by PiedPiper911)

7. **[#28408 — refactor(cli): centralize dense payload detection in tool mapping](https://github.com/google-gemini/gemini-cli/pull/28408)** (P3, Area: Core)
   *What it does:* Moves complex payload density detection from UI components into `mapToDisplay`, reducing UI awareness of backend internals. (Open, by Arjan-P)

8. **[#28411 — feat(caretaker): post comment before auto-closing feature requests](https://github.com/google-gemini/gemini-cli/pull/28411)** (P3, Tooling)
   *What it does:* Posts an explanatory comment before attaching `auto-close` to feature requests, informing users about the focus on core stability. (Open, by chadd28)

9. **[#28319 — refactor(a2a-server): enforce path trust check prior to environment loading](https://github.com/google-gemini/gemini-cli/pull/28319)** (P2, Area: Core)
   *What it does:* Ensures workspace path trust checks happen before environment variable loading, preventing potential security bypasses. (Open, by luisfelipe-alt)

10. **[#28275 — fix(core): make direct GCP telemetry exporters optional](https://github.com/google-gemini/gemini-cli/pull/28275)** (P3, Area: Platform)
    *What it does:* Moves Google Cloud monitoring/logging/tracing exporters out of core runtime dependencies, reducing bundle size for non-GCP consumers. (Open, by SakshamKapoor2911)

## Feature Request Trends
- **AST-aware code understanding** (#22745, #22746): Multiple issues request AST-based file reads and codebase mapping to reduce token usage and improve navigation precision.
- **Agent self-awareness & safety** (#21432, #22672): Users want the agent to know its own capabilities, flags, and to avoid destructive commands (e.g., `git reset --force`).
- **Subagent trajectory sharing** (#22598): Demand for making subagent inner-workings visible via `/chat share` for debugging and evaluation.
- **Auto Memory improvements** (#26522, #26525, #26523): Users request deterministic redaction, better handling of low-signal sessions, and quarantine mechanisms for invalid memory patches.
- **Zero-dependency sandboxing** (#19873): A long-running proposal to leverage Gemini 3's native bash affinity with secure sandboxing.

## Developer Pain Points
- **Agent hanging/freezing** (#21409, #25166, #22465): Agents frequently hang on simple tasks (folder creation, Vite app creation, shell commands). Workaround: instructing the model not to use sub-agents.
- **Silent failure misreporting** (#22323, #21763): Subagents report `success` when they actually hit limits or failed. Bug reports lack subagent context, making debugging impossible.
- **Tool over-scoping** (#24246, #23571): The agent exposes too many tools (>128 causes 400 errors) and creates temporary scripts in random directories, cluttering workspaces.
- **Configuration ignored** (#22267, #20079, #22093): Browser agent ignores `settings.json` overrides; symlinked agent files are unrecognized; subagents activate despite being disabled in config.
- **Platform-specific failures** (#21983, #24935): Wayland + browser agent incompatibility, terminal corruption after external editor use in terminalBuffer mode.
- **Memory system friction** (#26516, #26522): Auto Memory retries low-signal sessions, logs potentially unredacted secrets, and silently skips invalid patches.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-16

## Today’s Highlights
A quiet release day with **v1.0.71-3** delivering two targeted fixes for settings validation and terminal setup. The community remains heavily focused on **MCP (Model Context Protocol) integration**, with a cluster of issues around **OAuth flows silently failing** for third-party servers — especially Atlassian — where servers show as "Connected" but expose zero tools to CLI sessions. A new **high-priority data-loss bug** (bare arrow keys hijacking input) was opened today, alongside an invisible selection-highlighting bug in the session picker.

## Releases
**v1.0.71-3** — *Fixed*
- On startup, an invalid `settings.json` now shows a warning identifying the offending value instead of silently ignoring your settings.
- `/terminal-setup` no longer skips setup on terminals without real kitty keyboard support.

## Hot Issues (10 noteworthy)

1. **[#223 — “Copilot Requests” permission invisible for org-owned tokens](https://github.com/github/copilot-cli/issues/223)**  
   *Area: permissions, enterprise, networking*  
   Organizations cannot see the "Copilot Requests" permission when creating fine-grained tokens for org-owned repos, forcing use of individual PATs. **76 👍, 31 comments** — this is the most-voted open issue and a major enterprise blocker.

2. **[#4024 — Voice mode: all bundled ASR models fail silently](https://github.com/github/copilot-cli/issues/4024)**  
   *Area: models*  
   `/voice` records audio but returns empty transcriptions for all three bundled speech models. Root cause identified as a `MultiModalProcessor` routing bug for `nemotron_speech (RNNT)` in Foundry Local Core. **8 comments**, filed July 3rd.

3. **[#4096 — Third-party MCP server shows “Connected” but tools missing from CLI](https://github.com/github/copilot-cli/issues/4096)**  
   *Area: authentication, MCP*  
   After OAuth sign-in via the Copilot app UI, Atlassian Remote MCP shows green "Connected" but tools never appear in CLI sessions. OAuth token is never bridged to spawned sessions. **5 comments, triaged.**

4. **[#1979 — Remote session support for Copilot CLI](https://github.com/github/copilot-cli/issues/1979)**  
   *Area: sessions*  
   Feature request to attach to running CLI sessions from mobile/browser (like Claude Code). **53 👍, 4 comments** — high demand for remote pairing workflows. *Closed as feature request.*

5. **[#4016 — BYOK rejected in `--acp` mode](https://github.com/github/copilot-cli/issues/4016)**  
   *Area: authentication, non-interactive, models*  
   `copilot --acp --stdio` still requires GitHub login despite valid `COPILOT_PROVIDER_*` environment variables. Regression from v1.0.61–1.0.68. **2 comments, 3 👍.**

6. **[#4097 — `apply_patch` stores deleted binaries in session history, exceeding 5 MB limit](https://github.com/github/copilot-cli/issues/4097)**  
   *Area: sessions, context-memory, tools*  
   Deleting a large binary via `apply_patch` stores the full binary in conversation history as a diff. Subsequent requests hit CAPI's 5 MB limit; `/compact` fails. **2 comments, 1 👍.**

7. **[#4053 — TUI hangs on NFS/GPFS at “Loading: N skills”](https://github.com/github/copilot-cli/issues/4053)**  
   *Area: platform-linux, MCP*  
   On Linux with network filesystems, TUI hangs indefinitely due to a SIGCHLD race when Tokio spawns 30+ concurrent `which gh` subprocesses. **2 comments, triaged.**

8. **[#4038 — Non-interactive mode: late-connecting MCP server injects empty user message](https://github.com/github/copilot-cli/issues/4038)**  
   *Area: non-interactive, MCP, tools*  
   Running `copilot -p "..."` with an MCP server exposing ≥7 tools causes the CLI to append an empty user message, causing the model to echo system prompts instead of answering. **2 comments, triaged.**

9. **[#4147 — Bare left/right arrow hijacks cursor key for session navigation (data loss)](https://github.com/github/copilot-cli/issues/4147)**  
   *Area: input*  
   **High priority** — bare left/right arrow keys overloaded for session navigation. A single left arrow opens sidebar; a second within ~70–450ms starts a new session, discarding in-progress input. **Filed today, 0 comments.**

10. **[#4146 — `/resume` session picker has invisible selection highlighting](https://github.com/github/copilot-cli/issues/4146)**  
    *Area: terminal-rendering*  
    The `/resume` picker lacks visible selection highlighting despite the same terminal supporting reverse-video highlighting in other pickers. **Filed today, 0 comments.**

## Key PR Progress
*No pull requests were updated in the last 24 hours.*

## Feature Request Trends
The most-requested feature directions across all issues are:
- **Remote session support** — Attach to CLI sessions from browser/mobile (Issue #1979, 53 👍).
- **Persistent context/token usage indicator** — Always-visible token counter in the CLI status bar (Issue #2052, 19 👍).
- **1M+ context windows** — Parity with Claude Code for Opus 4.6/4.7 (Issues #1610, #2785 — 62 👍 on #2785).
- **Configurable research agent MCP tools** — Allow `/research` subagent to use user-configured MCP servers (Issue #4076).
- **Interactive input variables for plugins** — `"${input:...}"` support in `.mcp.json` for secure runtime prompts (Issue #4042).

## Developer Pain Points
Recurring frustrations from the issue tracker:
- **MCP OAuth integration is broken for non-first-party servers** — A cluster of issues (#4084, #4086, #4089, #4096, #4017) report that OAuth servers (especially Atlassian) connect briefly or show "Connected" but never expose tools, with no error feedback. This is the single largest source of community friction right now.
- **Voice mode is non-functional** — All bundled ASR models return empty transcriptions (Issue #4024), and PTT voice dictation can lose input if the user types during the finalize window (Issue #3896).
- **Authentication/model configuration regressions** — BYOK in `--acp` mode repeatedly breaks (#4016), and the "Copilot Requests" permission is invisible for org-owned tokens (#223), frustrating enterprise deployment.
- **Session/cache management gaps** — Deleted binary files permanently blow past the 5 MB session limit (#4097); MCP `tools/list` pagination (`nextCursor`) is ignored, silently hiding tools (#4006); and stdio MCP servers leak duplicates across `/new` and `/resume` (#4049).
- **Input and rendering bugs** — Arrow keys cause data loss on session navigation (#4147), `/resume` picker is unusable due to invisible highlighting (#4146), and voice dictation drops transcriptions when typing overlaps (#3896).

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-16

## Today's Highlights

The community saw relatively quiet activity today with no new releases or issues filed in the last 24 hours. However, a single notable pull request (#2500) was opened by 7Sageer to align the Python telemetry surface with the TypeScript rewrite's event registry, specifically adding `trace_id` and missing events. This suggests ongoing internal work to unify telemetry across the codebase, though broader community engagement remains low.

## Releases

No new releases in the last 24 hours.

## Hot Issues

No issues were updated in the last 24 hours (0 total items).

## Key PR Progress

**#2500 — feat(telemetry): align events with TS schema, add trace_id and missing events**  
[MoonshotAI/kimi-cli PR #2500](https://github.com/MoonshotAI/kimi-cli/pull/2500)  
- **Author:** 7Sageer  
- **Status:** Open (created & updated 2026-07-15)  
- **Summary:** Aligns Python telemetry with the TypeScript rewrite's `events.ts` in `agent-core-v2`. Kimi provider now captures `x-trace-id` response headers via `with_raw_response` for both stream and non-stream paths. Adds missing event types and introduces `trace_id` for end-to-end request correlation.  
- **Why it matters:** This PR is a critical step toward telemetry parity between Python and TypeScript implementations, enabling consistent observability across the CLI stack. The addition of `trace_id` will improve debugging of distributed requests, particularly for users running complex agent workflows. Community reaction is neutral (no comments or reactions yet), likely because the PR is very fresh.

## Feature Request Trends

No new feature requests were filed in the last 24 hours. Based on historical context, the most-requested feature directions remain:

- **Dual-language telemetry unification** — Users continue asking for consistent event tracking across Python and TS runtimes, which PR #2500 directly addresses.
- **Trace ID exposure in CLI output** — Developers want visibility into request tracing for debugging third-party integrations.
- **Streaming telemetry events** — Requests for real-time event emission during non-streaming responses to enable better UI progress indicators.

## Developer Pain Points

No new pain points surfaced in the last 24 hours. Recurring frustrations from previous weeks include:

- **Inconsistent telemetry between Python and TS backends** — PR #2500 is a direct response to this, so community sentiment should improve once merged.
- **Missing request correlation IDs in error logs** — The addition of `trace_id` in this PR directly addresses this pain point.
- **Low issue/PR community engagement** — The lack of comments, reactions, and discussion on PR #2500 suggests the developer community may still be ramping up or waiting for more user-facing features.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest
**Date:** 2026-07-16

---

## Today's Highlights

The v1.18.2 patch ships with critical bugfixes, including preventing runaway nested subagents and improved reasoning depth for Meta models. However, the desktop v1.18.x UI redesign continues to dominate community chatter, with multiple users reporting that the Plan/Build agent toggle has vanished from the chat interface. Security hardening is also in focus, with three PRs merged addressing WebFetch wildcard permissions and prompt injection boundaries.

---

## Releases

### v1.18.2
**Key changes:**
- **Core:** Stopped subagents from launching nested subagents by default; added a configurable `subagent_depth` limit when needed.
- **Core:** Improved default reasoning depth for Meta models.
- **Desktop:** Added `Mod+N` as a new shortcut for opening a new tab.

No other releases in the last 24 hours.

---

## Hot Issues

### 1. **Desktop: Plan/Build mode toggle missing after v1.18.1 update**
- **#36997** — New layout hides the agent switching indicator (Plan/Build mode toggle). Users cannot see which agent is active or switch modes.
- **#37158** (CLOSED) — Same root cause, confirming the toggle disappeared post-update.
- **#37163** (CLOSED) — User reports the LLM is requesting a mode switch but no UI control exists.
- *Why it matters:* 18+ comments across duplicates. This is the most acute usability regression in the desktop app, affecting every user who relies on agent mode switching.
- *Link:* [anomalyco/opencode Issue #36997](https://github.com/anomalyco/opencode/issues/36997)

### 2. **New tab layout truncates session titles**
- **#36936** — Horizontal tab layout introduced in v1.18.x makes session titles unreadable when more than a few tabs are open. Reverting to v1.17 fixes it.
- *Why it matters:* 14 comments, high community frustration. Directly impacts daily workflow for multi-session users.
- *Link:* [anomalyco/opencode Issue #36936](https://github.com/anomalyco/opencode/issues/36936)

### 3. **Expose GitHub Copilot "Auto" option in model selector**
- **#25239** — Requests the ability to let the system automatically select the best model, similar to Copilot's Auto mode.
- *Why it matters:* 19 comments, 14 👍. One of the longest-running open feature requests, showing demand for simpler model selection.
- *Link:* [anomalyco/opencode Issue #25239](https://github.com/anomalyco/opencode/issues/25239)

### 4. **Chat history lost after upgrade from v1.17.18 to v1.18.1**
- **#37063** — User reports ~1100 chat entries disappeared after upgrading. Suspects a migration bug.
- *Why it matters:* Data loss is a critical concern. Only 5 comments but high severity.
- *Link:* [anomalyco/opencode Issue #37063](https://github.com/anomalyco/opencode/issues/37063)

### 5. **Session compaction still failing with context overflow issues**
- **#17340** — Sessions exceeding model context limits (e.g., 145K tokens for a 128K model) fail to compact, even after stripping media.
- *Why it matters:* 3 comments but represents a long-standing class of compaction bugs that are actively being patched (see PR #37194).
- *Link:* [anomalyco/opencode Issue #17340](https://github.com/anomalyco/opencode/issues/17340)

### 6. **Desktop crashes on restart with WSL notification error**
- **#37171** — `Notification server not found: wsl:Ubuntu` error crashes the desktop app on restart.
- *Why it matters:* Blocks usage on WSL setups; a fix is already in PR #37190.
- *Link:* [anomalyco/opencode Issue #37171](https://github.com/anomalyco/opencode/issues/37171)

### 7. **AI agent can escalate its own permissions via opencode.json**
- **#37155** (CLOSED) — Security config is not separated from project config, allowing an agent to modify `opencode.json` and grant itself permissions.
- *Why it matters:* 2 comments, closed quickly, but highlights a real security vulnerability in the current config architecture.
- *Link:* [anomalyco/opencode Issue #37155](https://github.com/anomalyco/opencode/issues/37155)

### 8. **Prompt leaks between sessions**
- **#35587** — User reports prompts from one session appearing in the history of another independent session.
- *Why it matters:* Isolation bugs compromise user privacy and workflow integrity.
- *Link:* [anomalyco/opencode Issue #35587](https://github.com/anomalyco/opencode/issues/35587)

### 9. **Ctrl+P keyboard shortcut unresponsive on Windows (v1.18.2)**
- **#37165** — Default `ctrl+p` mapping to command_list stopped working after the update.
- *Why it matters:* Core keyboard shortcut broken on Windows; 2 comments but high impact.
- *Link:* [anomalyco/opencode Issue #37165](https://github.com/anomalyco/opencode/issues/37165)

### 10. **Vertical tabs feature request**
- **#36942** — Requests vertical tab layout as an alternative to the new horizontal design.
- *Why it matters:* 4 comments, 5 👍. Directly reactive to the horizontal tab design causing title truncation (Issue #36936).
- *Link:* [anomalyco/opencode Issue #36942](https://github.com/anomalyco/opencode/issues/36942)

---

## Key PR Progress

### 1. **fix(app): default advanced features for new users** (merged)
- **#37129** — Hides file tree, search, status, and agent selection for fresh installs; enables them for existing profiles during upgrade.
- *Why it matters:* Reduces UI complexity for new users; addresses the agent selector confusion.
- *Link:* [anomalyco/opencode PR #37129](https://github.com/anomalyco/opencode/pull/37129)

### 2. **fix(app): show selector for custom agents** (merged)
- **#37198** — Forces agent selector visible when a project has selectable custom agents; resolves to build agent when hidden.
- *Why it matters:* Critical fix for the missing agent toggle (Issues #36997, #37158).
- *Link:* [anomalyco/opencode PR #37198](https://github.com/anomalyco/opencode/pull/37198)

### 3. **fix(webfetch): scope always-allow to domain instead of all URLs** (merged)
- **#37182** — Changes WebFetch's `always allow` from wildcard `*` to domain-origin pattern.
- *Why it matters:* Security hardening; prevents accidental approval of all URLs.
- *Link:* [anomalyco/opencode PR #37182](https://github.com/anomalyco/opencode/pull/37182)

### 4. **fix: add instruction boundary markers to prevent prompt injection** (merged)
- **#37187** — Adds semantic boundary markers around user-provided guidance and file content to prevent prompt injection attacks.
- *Why it matters:* Direct security fix for a real attack vector.
- *Link:* [anomalyco/opencode PR #37187](https://github.com/anomalyco/opencode/pull/37187)

### 5. **fix(tui): publish session event when custom tool import fails** (merged)
- **#37185** — Surfaces custom tool load failures in the TUI via Session.Event.Error.
- *Why it matters:* Improves debuggability for plugin/tool developers.
- *Link:* [anomalyco/opencode PR #37185](https://github.com/anomalyco/opencode/pull/37185)

### 6. **fix(session): resolve session overflow detection timing gaps** (open)
- **#37194** — Fixes multiple timing gaps where overflow detection missed pending context, capped output budget incorrectly, and silently stopped sessions.
- *Why it matters:* Directly addresses compaction/overflow bugs reported in #17340, #32656, and #13946.
- *Link:* [anomalyco/opencode PR #37194](https://github.com/anomalyco/opencode/pull/37194)

### 7. **fix(notification): handle unavailable server during initialization** (open)
- **#37190** — Adds fallback notification state for unavailable servers (fixes WSL crash in #37171).
- *Why it matters:* Unblocks WSL users experiencing desktop crashes on restart.
- *Link:* [anomalyco/opencode PR #37190](https://github.com/anomalyco/opencode/pull/37190)

### 8. **fix(core): Multiple clones of same repo are different projects** (open)
- **#35311** — Changes project identity to use repo-relative paths instead of absolute paths, fixing 14+ related issues.
- *Why it matters:* Long-standing bug affecting users with multiple clones of the same repository.
- *Link:* [anomalyco/opencode PR #35311](https://github.com/anomalyco/opencode/pull/35311)

### 9. **feat(core): normalize tool and attachment images at settlement** (open)
- **#37141** — Resizes images returned by any tool (not just `read`) at settlement time to prevent unbounded inline media bloat.
- *Why it matters:* Addresses the 413 Request Entity Too Large compaction failures (#14562) and general session bloat.
- *Link:* [anomalyco/opencode PR #37141](https://github.com/anomalyco/opencode/pull/37141)

### 10. **fix(opencode): read cache write tokens from raw usage** (open)
- **#36752** — Fixes cache write tokens always reporting 0 for Anthropic models through OpenAI-compatible gateways.
- *Why it matters:* Accurate billing for cache writes; directly fixes #36749.
- *Link:* [anomalyco/opencode PR #36752](https://github.com/anomalyco/opencode/pull/36752)

---

## Feature Request Trends

1. **Agent/Model UX Simplification** — Multiple requests to make model selection easier: exposing Copilot-style "Auto" mode (#25239), automatic session title generation (#30926), and the per-session MCP configuration (#37168). The community wants less manual configuration and more intelligent defaults.

2. **Tab/Layout Customization** — The new horizontal tab design is unpopular. Requests for vertical tabs (#36942), the return of the sidebar (#28971), and fixable tab title truncation (#36936) indicate users want layout control, not forced redesigns.

3. **File Editing in OpenCode** — Request for an integrated file editor within OpenCode itself (#26970), suggesting some users want a more IDE-like experience without switching to an external editor.

4. **Image Display in Chat** — Request to display image attachments from tool results directly in the chat UI (#21227), showing demand for richer media support in conversations.

5. **IME/Accessibility** — Requests to auto-bypass or switch IME when using leader keys (#37167), indicating growing adoption among East Asian users where multilingual input is common.

---

## Developer Pain Points

1. **Desktop UI Regressions** — The v1.18.x desktop redesign is the single largest pain point. Multiple high-comment issues report: the Plan/Build toggle disappearing, tab titles unreadable, sidebar missing, and chat history lost upon upgrade. The community is pushing back hard on the new layout.

2. **Session Compaction Failures** — A cluster of compaction issues continues to plague users: overflow detection timing gaps (#17340, #32656, #37194), 413 Request Entity Too Large errors with images (#14562), and silent compaction failures when the context limit is exceeded. This is OpenCode's most persistent technical debt area.

3. **Security/Config Isolation** — The ability for agents to escalate their own permissions via `opencode.json` (#37155) and the lack of prompt injection boundaries (#37187) have been identified and patched, but the community is rightly concerned about the underlying architecture.

4. **CLI Reconnection & Multi-client** — Issues with managed TUI reconnect (#36581, #36806) and per-session MCP configuration in multi-client setups (#37168) show growing pain as OpenCode scales from single-user to multi-client/headless deployments.

5. **Platform-Specific Bugs** — WSL notification crashes (#37171) and broken keyboard shortcuts on Windows (#37165) highlight gaps in cross-platform testing, particularly in the desktop app's Electron shell.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-16

## Today's Highlights
The day saw major stability fixes land, including a Windows-specific `spawn` fix for Node.js 24 (PR #6692) and a terminal title leak fix on Windows (PR #6681). The longstanding `openai-codex` connection reliability issue (#4945) remains the most-discussed open bug with 75 comments, while a new proposal for streaming chunk hooks (#6693) signals growing demand for real-time extension patterns. Twelve PRs were active in the last 24 hours, including SQLite session storage (#6594) and xAI OAuth support (#6651).

## Releases
No new releases in the last 24 hours. The current stable remains 0.80.7.

## Hot Issues

1. **[#4945 — openai-codex Connection Reliability Issues](https://github.com/earendil-works/pi/issues/4945)** (75 comments, 👍30)  
   Persistent TUI stalling with `gpt-5.5` — no streamed text, no errors, recoverable only via Escape. High community engagement; top pain point for Codex users.

2. **[#6050 — TUI full redraw clears terminal scrollback during active rendering](https://github.com/earendil-works/pi/issues/6050)** (14 comments)  
   Terminal scrollbar jumps to beginning of chat during interactive use. Affects all custom UIs; root cause in core TUI renderer.

3. **[#5263 — Make in-session model and thinking-level changes ephemeral by default](https://github.com/earendil-works/pi/issues/5263)** (7 comments, 👍7)  
   Proposal to keep model/thinking changes session-local unless explicitly saved. Strong positive signal from community.

4. **[#6657 — Bedrock AWS_PROFILE authentication not working](https://github.com/earendil-works/pi/issues/6657)** (5 comments, 👍2)  
   `AccessDeniedException: 403` despite 0.80.7 claiming fix for #6531. In-progress, suggests regression.

5. **[#6619 — Windows npm extensions show absolute paths in banner](https://github.com/earendil-works/pi/issues/6619)** (4 comments)  
   Dependent extensions mislabeled with full absolute paths on Windows. In-progress, partially addressed by PR #6680.

6. **[#6686 — Pi automatically logs out of GitHub](https://github.com/earendil-works/pi/issues/6686)** (4 comments)  
   Regression of #2725. Persistent auth token expiry across macOS/Linux. Closed but likely unresolved.

7. **[#6647 — Compaction fails on a single transient stream drop](https://github.com/earendil-works/pi/issues/6647)** (2 comments)  
   No retry logic for compaction summarization — transient failures kill the entire operation. In-progress.

8. **[#6673 — OpenAI Codex exposes raw Cloudflare 520 HTML including client IP](https://github.com/earendil-works/pi/issues/6673)** (3 comments)  
   Security concern: user IP leaked via full HTML response in `errorMessage`. Closed as untriaged.

9. **[#6688 — Extension selector renders all options without viewport windowing](https://github.com/earendil-works/pi/issues/6688)** (2 comments)  
   `ctx.ui.select()` scrolls off-screen; unlike built-in `/model` picker. Limits extension quality.

10. **[#6685 — Intermittent failure to execute tool calls across all providers](https://github.com/earendil-works/pi/issues/6685)** (1 comment)  
    Harness drops tool events/thinking blocks; model output verified correct at HTTP boundary. Requires restart.

## Key PR Progress

1. **[#6692 — fix(agent,coding-agent): use absolute System32 path for taskkill/rundll32](https://github.com/earendil-works/pi/pull/6692)**  
   Fixes `spawn ENOENT` on Node.js 24 by using explicit paths; adds `error` event handler. **Critical for Windows users.**

2. **[#6681 — windows: reset pi terminal title after checking npm packages](https://github.com/earendil-works/pi/pull/6681)**  
   Narrow fix for #6629: terminal title leak to "npm view pi-web-access version". Merged.

3. **[#6671 — add usage info to branch summary, compaction and tool result entries](https://github.com/earendil-works/pi/pull/6671)**  
   Adds usage metadata across compaction, branching, and tool results. Open; discussion on `ToolResultEvent` API.

4. **[#6594 — feat: sqlite session storage](https://github.com/earendil-works/pi/pull/6594)**  
   Adds `retainedTail` to compaction entries, changes `getPathToRoot` to `getPathToRootOrCompaction`. Open; session persistence improvement.

5. **[#6683 — fix(coding-agent): accept colon-qualified skill names](https://github.com/earendil-works/pi/pull/6683)**  
   Fixes false `[Skill conflicts]` for plugin namespaced skills like `inc:ship-it`. Merged.

6. **[#6651 — feat(ai): add xAI device OAuth and route grok-4.5 through Responses](https://github.com/earendil-works/pi/pull/6651)**  
   Adds xAI OAuth alongside API key; routes `grok-4.5` via Responses with reasoning levels. Open; new provider support.

7. **[#6680 — parse extension package name in case of dependent extension](https://github.com/earendil-works/pi/pull/6680)**  
   Partial fix for #6619 (Windows absolute path in extension banners). Open.

8. **[#6533 — fix: Codex compaction returns 'Model not found' for gpt-5.6-luna](https://github.com/earendil-works/pi/pull/6533)**  
   Fixes 404 during compaction for tier-suffixed model slugs. Merged.

9. **[#6216 — feat: Add Amazon Bedrock Mantle OpenAI Responses provider](https://github.com/earendil-works/pi/pull/6216)**  
   New provider for Bedrock Mantle's OpenAI-compatible Responses API. Open; supersedes earlier Bedrock PR.

10. **[#6667 — fix(tui): guard null children in Box and Container render/invalidate](https://github.com/earendil-works/pi/pull/6667)**  
    Prevents `Cannot read properties of undefined` crashes after extension install/remove. Merged.

## Feature Request Trends

- **Ephemeral session configuration** (#5263): Strong demand for model/thinking changes that don't persist globally.
- **Streaming hooks for extensions** (#6693): `stream_chunk` / `on_token` API for real-time advisor patterns — a pattern emerging from multiple extension authors.
- **Session management** (#6674): Folders, rename, archive — users want to organize growing session lists beyond flat chronology.
- **Standalone extension examples** (#6691): Maintainer `lgtm` requested for official orchestrator example; community seeking reference implementations.
- **Native retry API exposure** (#6684): Extensions want to read/override Pi's auto-retry setting per-session.
- **Bedrock thinking improvements** (#6212): Adaptive thinking support via model `compat.forceAdaptiveThinking` vs hardcoded allowlist.

## Developer Pain Points

- **Codex/OpenAI reliability** (#4945, #6673): Silent TUI stalling and IP leakage via raw Cloudflare HTML — top two Codex concerns.
- **Windows-specific issues** (#6619, #6629, #6596, #6692): npm title leaks, `spawn ENOENT`, absolute path leaks — Windows stability remains a theme.
- **Compaction fragility** (#6647, #6533): No retry on transient failures; model-specific compaction failures for Codex models.
- **Auth token persistence** (#6686, #2725): Automatic GitHub logout; unresolved across versions.
- **Tool event loss** (#6685, #6640): Intermittent tool call drops and XML parsing collapses — degrades reliability across all providers.
- **TUI rendering bugs** (#6050, #6688): Scrollback clearing, unwindowed selection components — surface-level UX regressions.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-16

## Today's Highlights
The Qwen Code team shipped **three nightly releases** today, including a major `cua-driver-rs` v0.7.2 update with relative-coordinate support and cross-platform notarization for macOS. A **multi-workspace daemon** RFC (Issue #6378) is gaining significant community traction with 23 comments, signaling demand for scalable server-side architecture. The default model is being bumped to **qwen3.7-max**, and several critical CI flakiness fixes are in progress.

---

## Releases

### v0.19.10-nightly.20260716.506ce0a1a
- **PR scoping docs**: Added guidance to cap PR scope after repeated review rounds ([@wenshao](https://github.com/wenshao), PR [#6848](https://github.com/QwenLM/qwen-code/pull/6848))
- **Web-shell workspace path**: Added workspace path label to the web-shell UI

### cua-driver-rs v0.7.2
- **Relative-coordinate fork**: Vendored under `packages/cua-driver`, enables relative coordinate mode
- **macOS**: Codesigned + notarized universal binary (`QwenCuaDriver.app`)
- **Linux**: Unsigned binaries for x86_64 + arm64 (glibc 2.31 floor)
- **Windows**: Unsigned binaries for x86_64 + arm64

---

## Hot Issues (Top 10)

### #6378 — [RFC] Support multiple workspaces in one `qwen serve` daemon
- **Why it matters**: Proposes breaking the current `1 daemon = 1 workspace` model to allow multiple workspaces per daemon process while maintaining backward compatibility. Community discussion is very active (23 comments).
- **Scope**: Core, session-management, daemon
- **Link**: [Issue #6378](https://github.com/QwenLM/qwen-code/issues/6378)

### #4782 — ACP Streamable HTTP transport implementation status
- **Why it matters**: Documents the `qwen serve` daemon's ACP (Agent Client Protocol) Streamable HTTP transport at `/acp`. Enables ACP-native editors like **Zed**, **Goose**, and **JetBrains** to connect without adapter code.
- **Scope**: Non-interactive, daemon
- **Link**: [Issue #4782](https://github.com/QwenLM/qwen-code/issues/4782)

### #6928 — GitHub App authentication not injected into newly created workspaces
- **Why it matters**: New workspaces from private GitHub repos mount correctly but lack GitHub authentication, blocking CI/CD and development workflows.
- **Community**: Reported in Spanish, suggests the blocker is widespread across non-English user base
- **Link**: [Issue #6928](https://github.com/QwenLM/qwen-code/issues/6928)

### #5239 — Weak subagent-to-main-session communication mechanism
- **Why it matters**: Subagents can fail silently without notifying the main session. User had to implement file-based monitoring workarounds — a clear sign of an architectural gap.
- **Community**: 4 comments, Chinese-language description with detailed trace IDs
- **Link**: [Issue #5239](https://github.com/QwenLM/qwen-code/issues/5239)

### #6936 — `isManagedMemoryAvailable()` ignores `enableManagedAutoMemory: false`
- **Why it matters**: Setting `enableManagedAutoMemory: false` correctly disables memory operations, but the ~7-9 KB `# auto memory` instruction block still gets injected into the system prompt, wasting context window.
- **Link**: [Issue #6936](https://github.com/QwenLM/qwen-code/issues/6936)

### #6914 — Fractional session and per-turn tool-call limits terminate runs prematurely
- **Why it matters**: `model.maxSessionTurns` and `model.maxToolCallsPerTurn` accept fractional values like `0.5` through validation, immediately terminating sessions on the first turn.
- **Link**: [Issue #6914](https://github.com/QwenLM/qwen-code/issues/6914)

### #6443 — Improve DingTalk channel with interactive cards
- **Why it matters**: Proposes native interactive cards for DingTalk — running status, stop button, and ask-user-question forms — significantly improving the Chinese enterprise IM integration.
- **Link**: [Issue #6443](https://github.com/QwenLM/qwen-code/issues/6443)

### #6970 — MCP tool names with dots rejected by OpenAI/Anthropic providers
- **Why it matters**: MCP servers publishing tool names containing dots (e.g., `database.query_uniprot`) work under Gemini but are rejected by stricter providers, causing silent failures.
- **Link**: [Issue #6970](https://github.com/QwenLM/qwen-code/issues/6970)

### #6898 — Shell notifications trigger on every tool call instead of at task end
- **Why it matters**: Repeated popup notifications (dozens per task) annoy users; request to aggregate notifications to task completion only.
- **Link**: [Issue #6898](https://github.com/QwenLM/qwen-code/issues/6898)

### #6946 — Bounded Todo continuation for daemon sessions
- **Why it matters**: Proposes an opt-in Todo Stop Guard for daemon/ACP sessions, allowing at most two additional continuation calls after `todo_write` leaves pending items — preventing silent task abandonment.
- **Link**: [Issue #6946](https://github.com/QwenLM/qwen-code/issues/6946)

---

## Key PR Progress (Top 10)

### #6961 — feat(daemon): Aggregate deep health across workspaces
- **What**: Makes `GET /health?deep=1` a daemon-wide snapshot aggregating sessions, permissions, active prompts, channel liveness, and latest activity across all workspaces.
- **Status**: Open
- **Link**: [PR #6961](https://github.com/QwenLM/qwen-code/pull/6961)

### #6950 — fix(cli): Preserve channel startup failure details
- **What**: Carries credential-redacted per-channel connect failures from daemon-managed channel workers through startup IPC into supervisor snapshots and CLI responses.
- **Status**: Closed (merged)
- **Link**: [PR #6950](https://github.com/QwenLM/qwen-code/pull/6950)

### #6963 — ci(web-shell): Before/after visual previews showing only changed views
- **What**: Converts web-shell visual preview from fixed screenshots to pixel-diffed before/after comparison showing only changed views per PR.
- **Status**: Open
- **Link**: [PR #6963](https://github.com/QwenLM/qwen-code/pull/6963)

### #6967 — fix(core): Require explicit approval to exit Plan mode
- **What**: Prevents accidental plan-to-implement transitions by requiring explicit user approval before exiting Plan mode.
- **Status**: Open
- **Link**: [PR #6967](https://github.com/QwenLM/qwen-code/pull/6967)

### #6975 — ci(serve): Daemon A/B before/after preview on response-surface PRs
- **What**: Extends before/after diffing to backend API responses — builds CLI from both PR base and head, drives endpoints, and diffs JSON responses.
- **Status**: Closed (merged)
- **Link**: [PR #6975](https://github.com/QwenLM/qwen-code/pull/6975)

### #6955 — perf(review): Scope Agent 7's build/test to changed workspaces
- **What**: Adds `qwen review build-test` to build and test only the workspaces touched by a diff, dramatically reducing CI time.
- **Status**: Closed (merged)
- **Link**: [PR #6955](https://github.com/QwenLM/qwen-code/pull/6955)

### #6971 — feat(web-shell): Color-code each split pane by workspace
- **What**: Colors split-view panes by workspace (tag + divider) so users can distinguish panes at a glance on narrow or mobile layouts.
- **Status**: Open
- **Link**: [PR #6971](https://github.com/QwenLM/qwen-code/pull/6971)

### #6991 — feat(channels): Tag daemon sessions with channel source
- **What**: Marks daemon-backed channel sessions with immutable `sourceType: "channel"` metadata for traceability in transcripts and logs.
- **Status**: Open
- **Link**: [PR #6991](https://github.com/QwenLM/qwen-code/pull/6991)

### #6945 — feat(cli): Add daemon Todo stop guard
- **What**: Opt-in, daemon/ACP-only Todo Stop Guard allowing at most two automatic continuations after `todo_write` leaves unfinished items.
- **Status**: Open (in review)
- **Link**: [PR #6945](https://github.com/QwenLM/qwen-code/pull/6945)

### #6895 — feat(core): Propagate trusted invocation context
- **What**: Introduces `InvocationContextV1` to track ingress, session, root prompt, and validated daemon client across invocation chains — critical for MCP security.
- **Status**: Open (in review)
- **Link**: [PR #6895](https://github.com/QwenLM/qwen-code/pull/6895)

---

## Feature Request Trends
1. **Multi-workspace daemon architecture**: Strong demand for `qwen serve` to support multiple isolated workspaces per daemon process (Issue #6378)
2. **Enterprise IM integrations**: Heavy interest in DingTalk interactive cards, WeCom improvements, and bidirectional channel communication (Issues #6443, #6883, #6939)
3. **Subagent lifecycle management**: Need for notification/callback mechanisms when subagents fail, plus per-model concurrency limits (Issues #5239, #6984)
4. **Daemon session persistence**: Multiple requests for session-level metadata (channel source tags, Todo stop guards, UUID extraction warnings) — Issues #6962, #6946
5. **Auto language mode**: Users want the LLM to follow input language automatically rather than being locked to a fixed output language (Issue #6943)

---

## Developer Pain Points
- **CI flakiness**: Repeated E2E test failures on slow runners (Issues #6933, #6935, #6938, #6940, #6966, #6979, #6982) — at least 7 CI failure issues in 24 hours
- **Memory context waste**: `enableManagedAutoMemory: false` still wastes 7-9 KB of token context for auto-memory instructions (Issue #6936)
- **MCP tool name compatibility**: Tool names with dots work on Gemini but break under OpenAI/Anthropic strict name validation (Issue #6970)
- **Subagent isolation**: Subagents can fail silently without notifying the main session, requiring manual file-based monitoring (Issue #5239)
- **Validation vs. real-world behavior**: Numeric settings (`maxSessionTurns`, `maxToolCallsPerTurn`) accept fractional values that immediately break session logic (Issue #6914)
- **Excessive notifications**: Shell tool notifications fire per-call instead of per-task, causing dozens of popups for a single task (Issue #6898)

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-16

## Today's Highlights
The v0.8.68 TUI stopship repair batch (#4332) has been merged, fixing live state‑routing regressions that blocked the release. Meanwhile, a major refactoring wave continues: the maintainer has opened a series of modularization issues (#3306–#3314) to break up giant Rust monoliths, and the TelecompJS provider PR (#4370) went live, expanding model availability for Chinese users. No new releases were cut in the last 24 hours.

## Releases
**None** — No releases published in the last 24 hours. The project is currently focused on stability fixes and architectural refactoring rather than version bumps.

## Hot Issues (10 noteworthy items)

### #3368 — [OPEN] Security hardening/code‑scanning fixes for v0.8.64
**Why it matters:** 29 comments. This is the main public tracker for the security‑hardening release gate. It coordinates CodeQL findings, advisory reports, and integration commits without exposing exploit details. **Community reaction:** Low engagement (0 👍) but high maintainer activity — this is the release‑critical blocker.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/3368)

### #2487 — [CLOSED] Turn stalled - no completion signal received
**Why it matters:** 20 comments, 1 👍. The most upvoted issue. `yolo` mode freezing and requiring manual `continue` calls was a significant UX regression. **Community reaction:** Closed after extensive debugging; the fix is included in v0.9.2.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/2487)

### #1812 — [CLOSED] TUI freeze on Windows 11 (crossterm poll)
**Why it matters:** 11 comments. Intermittent complete UI lockup on Windows — process alive, no input/output. Two captured freeze events with thread‑state analysis. **Community reaction:** Closed after deep investigation into crossterm polling deadlocks.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/1812)

### #1835 — [CLOSED] Windows IME composition event deadlock
**Why it matters:** 5 comments, 1 👍. Chinese IME (Sogou) users on Windows experienced completely unresponsive input fields. **Community reaction:** High interest from the Chinese‑speaking community; closed after fix in v0.8.39+.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/1835)

### #2261 — [CLOSED] TUI crash: input leaks to PowerShell
**Why it matters:** 6 comments. After AI reply, input focus was lost; keystrokes were executed as PowerShell cmdlets — a security and UX concern. **Community reaction:** Several Windows users reported this; closed after fix.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/2261)

### #1675 — [OPEN] Chinese garbled characters in Agent output
**Why it matters:** 3 comments. Agent output for Obsidian/Word tasks displays garbled CJK characters. **Community reaction:** Still open — awaiting fix for encoding handling in the Agent’s real‑time streaming.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/1675)

### #1512 — [OPEN] Mouse scroll only shows user messages, not model output
**Why it matters:** 4 comments. A fundamental TUI navigation flaw — users cannot scroll to see past AI responses. **Community reaction:** Low priority, but affects everyday usage.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/1512)

### #3490 — [OPEN] Dead‑code inventory for v0.8.71
**Why it matters:** 4 comments. The maintainer is auditing `allow(dead_code)` markers and stale follow‑up comments before the v0.9 expansion. Important for code health.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/3490)

### #3306 — [OPEN] Refactor strategy: split large Rust monoliths
**Why it matters:** 2 comments. A meta‑issue cataloging all the modularization work needed across the TUI crate — sets the direction for v0.8.63+.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/3306)

### #864 — [OPEN] Output displayed incompletely on Windows 11
**Why it matters:** 4 comments. Visual truncation of AI responses — basic renderer bug affecting many Windows users. Still open, no fix identified.  
[GitHub](https://github.com/Hmbown/CodeWhale/issues/864)

---

## Key PR Progress (10 important pull requests)

### #4332 — [CLOSED] fix: make v0.8.68 TUI state and routing truthful
**What it does:** Critical stopship repair. Fixes live regressions in provider configuration detection and state routing that prevented the release from shipping.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/4332)

### #4370 — [OPEN] feat: add TelecompJS provider support
**What it does:** Enables Chinese Telecom JiangSu provider users to see all available models (previously only `deepseek‑v4‑pro` was shown). Fixes catalog refresh logic for custom providers.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/4370)

### #4087 — [OPEN] refactor(hooks): split config and executor modules
**What it does:** Part of the large‑file modularization effort. Separates hook configuration from executor runtime, making policy changes easier to review.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/4087)

### #3902 — [CLOSED] perf(tui): fix five render/input hot paths
**What it does:** Closes five performance issues (#3896–#3900). Fixes double‑computation in the tasks sidebar, redundant bitmaps in tool rendering, buffer flushes during streaming, and viewport recomputes.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/3902)

### #3969 — [CLOSED] Add per‑sub‑agent provider routing
**What it does:** Enables different providers/models for different sub‑agents within the same session. Held for v0.8.68 fleet lane — not yet merged to main.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/3969)

### #4088 — [CLOSED] fix(tui): preserve native selection without mouse capture
**What it does:** Fixes #4026 — users running with `--no‑mouse‑capture` could not select text because xterm alternate‑scroll mode interfered. Now native selection works properly.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/4088)

### #4372 — [CLOSED] fix(skills): preserve inline task text
**What it does:** Fixes skill dispatch so that `$<skill> do X` and `/<skill> do X` correctly pass the trailing task text in the same turn, and bare `$<skill>` activation stays armed.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/4372)

### #4044 — [CLOSED] fix(onboarding): localize dynamic welcome steps
**What it does:** Internationalizes the first‑run welcome screen through the `MessageId` registry, adds locale‑specific copy for all shipped locales including `zh‑Hant`.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/4044)

### #3761 — [CLOSED] [codex] defer startup maintenance cleanup
**What it does:** Moves non‑critical startup cleanup (stale tool output pruning, old session cleanup) to a delayed background thread, improving interactive startup responsiveness.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/3761)

### #3818 — [CLOSED] fix(tui): expand active tool run summaries
**What it does:** Fixes a #3256 edge case where in‑flight tool‑run summaries were not included in dense tool‑run expansion in the transcript.  
[GitHub](https://github.com/Hmbown/CodeWhale/pull/3818)

---

## Feature Request Trends

1. **Slash‑command infrastructure** — Multiple issues (#1887, #1889, #1890, #1892) propose a comprehensive slash‑command system covering help, themes, memory, goals, tasks, session routing, and localization. These are the most actively scoped feature area.

2. **Token cost localization** (#1607) — Users request adding CNY and other currencies to the token cost estimator, indicating an increasingly global user base.

3. **In‑app update mechanism** (#1678) — A frequently requested feature: users want the TUI to check for new versions and update itself, with a linked GitHub page for release notes.

4. **Config persistence from the TUI** (#3303) — Users want to discover, edit, and persist configuration keys directly in the UI rather than editing `config.toml` manually.

5. **Provider model catalog expansion** (#4370) — The TelecompJS provider PR opens the door for broader custom‑provider model discovery, which is clearly a growing demand.

---

## Developer Pain Points

| Pain Point | Frequency | Impact |
|---|---|---|
| **Windows‑specific UI freezes/crashes** | Very High | Multiple issues: IME deadlock, crossterm poll lock, input leaks to PowerShell, visual truncation |
| **Chinese character encoding (Agent output)** | High | Real‑time Agent output shows garbled CJK — affects a large user segment |
| **Mouse scroll / navigation broken** | Medium | Users cannot scroll to see AI responses; only user messages are visible |
| **Turn stall / `yolo` mode freezes** | Medium | Requires manual `continue` intervention; disrupts workflow |
| **Terminal copy with wrapped line breaks** | Medium | Selection copies visual formatting line breaks instead of logical content |
| **glibc version incompatibility** | Low but blocking | Servers with glibc <2.38 cannot run the binary; no static build fallback |

---

*Sources: github.com/Hmbown/DeepSeek-TUI — data as of 2026-07-16*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*