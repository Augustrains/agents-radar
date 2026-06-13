# AI CLI Tools Community Digest 2026-06-13

> Generated: 2026-06-13 02:03 UTC | Tools covered: 9

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
**Date:** 2026-06-13

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing rapid divergence in both maturity and architectural ambition. **Claude Code** and **OpenAI Codex** lead in release velocity and community engagement, though both grapple with scaling pains around autonomous agent safety and platform reliability. **Gemini CLI** and **Qwen Code** are closing feature gaps aggressively, particularly in daemon/server modes and multi-provider support. A second tier of tools—**OpenCode**, **Pi**, and **CodeWhale (DeepSeek TUI)**—demonstrate strong niche adoption but face fundamental stability and documentation hurdles. **Kimi Code CLI** lags in release cadence and community activity, with unresolved billing and reliability issues that risk user attrition. Across all tools, the dominant themes are agent safety, model routing transparency, cross-platform reliability, and the tension between rapid feature shipping and production-grade stability.

---

## 2. Activity Comparison

| Tool | Issues Updated (24h) | PRs Active (24h) | Releases Today | Community Engagement Signal |
|---|---|---|---|---|
| **Claude Code** | 10+ hot issues, 30+ total | 2 significant | 3 patches (v2.1.175–177) | Very high — 37👍 top issue, 26-comment feature debates |
| **OpenAI Codex** | ~20+ hot issues (Windows sandbox crisis) | 10 significant | 4 alpha releases (v0.140.0-alpha.14–.17) | Very high — 111👍 top issue, 78 comments |
| **Gemini CLI** | 10 hot issues | 10 significant | 1 nightly (v0.48.0) | Moderate — 8👍 top issue, P1 agent hangs dominate |
| **GitHub Copilot CLI** | 10 hot issues | 1 (low impact) | 1 patch (v1.0.62-1) | Moderate — 75👍 long-running issue #53 (9 months no response) |
| **Kimi Code CLI** | 3 hot issues | 1 (open) | None | Low — 7👍 top issue, limited community breadth |
| **OpenCode** | 10 hot issues | 10 significant | 1 (v1.17.4) | High — 22👍 top feature, active PR pipeline |
| **Pi** | 50 issues updated | 15 PRs | 1 (v0.79.2) | High — 30👍 top issue (Codex reliability), very active |
| **Qwen Code** | 10 hot issues | 10 significant | 1 (v0.18.0) | Very high — 127 comments on #3203 (free tier policy), Chinese + English |
| **CodeWhale (DeepSeek TUI)** | ~10 issues | 15+ PRs (mostly closed) | 1 (v0.8.59 rebrand) | Moderate — brand migration, roadmap-driven activity |

**Key observation:** OpenAI Codex and Claude Code have the highest raw issue volume, but Pi (50 issues/15 PRs in 24h) and CodeWhale (15+ PRs) show remarkable per-repo activity density relative to their community size.

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities:

### a) Hierarchical/Tiered Agent Architectures
- **Claude Code** (#56913): Opus for planning, Sonnet for execution, persistent state
- **Gemini CLI** (#21968, #22323): Subagent orchestration, skill auto-selection
- **OpenCode** (#12716, #18108): Doom loop detection, agent-switch reliability  
- **Qwen Code** (#5018, #5019): Long-context degradation with multi-agent workflows
- **CodeWhale** (#2656, #2657): Subagent session conflicts, tool availability signaling

**Common need:** Multi-model orchestration with persistent memory, safety limits, and graceful degradation. No tool has fully solved this.

### b) Model Routing Transparency & Control
- **Claude Code** (#68076, #67688): Fable classifier false positives, enforceAvailableModels
- **OpenAI Codex** (#27970): Rate limit false positives for high-tier subscribers
- **Gemini CLI** (#24246): 128-tool cap, model selection commands (PR #27848)
- **Qwen Code** (#5039): id+baseUrl for precise model identity
- **CodeWhale** (#3018): Un-hardcode DeepSeek from auto-router

**Common need:** Users demand visibility into *which* model is servicing *which* task, configurable routing rules, and protection against unexpected cost escalation.

### c) Cross-Platform Reliability
- **Claude Code** (#49917): Windows installer fails (0x80073CF6)
- **OpenAI Codex** (#24391 cluster): Windows sandbox `spawn setup refresh` crisis (20+ issues)
- **GitHub Copilot CLI** (#3784): Linux ARM64 Tokio panic
- **Kimi Code CLI** (#2435): Windows WebSocket daemon failure
- **Qwen Code** (#5010): Windows `cmd.exe` printf missing
- **Pi** (#5667): macOS `$TMPDIR` crash

**Common need:** Windows remains the weakest platform across *all* tools. macOS and Linux are prioritized; Windows users face installer hangs, UAC elevation errors, and missing command support.

### d) Context/Memory Management
- **Claude Code** (#56913): Persistent state across sessions
- **OpenAI Codex** (#9046): Context overflow on fresh threads
- **Gemini CLI** (#26522): Auto Memory retrying low-signal sessions
- **OpenCode** (#12716, #18108): Doom loops from truncated tool calls
- **Qwen Code** (#5018, #5019): Long-context degradation, tool call repetition
- **CodeWhale** (#1722): Context saturation unresponsiveness at 99.6%

**Common need:** Context window management is *the* fundamental unsolved problem. Tools either overflow, loop, degrade in quality, or hang. No tool has a robust solution for long-running autonomous sessions.

### e) CI/CD & Autonomous Execution
- **Claude Code** (#50911): Durable scheduled tasks silently ignored
- **OpenAI Codex** (#22335): Remote compaction fails, breaks task continuity
- **Gemini CLI** (#22323): Subagent MAX_TURNS reports false success
- **GitHub Copilot CLI** (#3782): MCP stdio server unbounded respawn loops
- **CodeWhale** (#3042): CLI flags for unattended CI/benchmark use

**Common need:** Tools are being pushed toward headless, autonomous, scheduled execution. Current implementations lack proper durability, failure signaling, and cost controls.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Qwen Code | OpenCode | Pi | CodeWhale |
|---|---|---|---|---|---|---|---|---|
| **Primary LLM** | Anthropic Claude | OpenAI GPT | Google Gemini | GitHub Copilot (GPT-based) | Qwen (Alibaba) | Provider-agnostic | Provider-agnostic | DeepSeek → multi-provider |
| **Target User** | Enterprise dev teams | Pro/individual devs | Google Cloud devs | GitHub ecosystem | Chinese/global devs | Individual power users | Individual devs | CLI-first individual devs |
| **CLI Architecture** | Monolithic + plugins | Rust rewrite (alpha) | Node.js + daemon | Node.js | Node.js + daemon | TypeScript | TypeScript | TypeScript |
| **Agent Autonomy** | Highest (sub-agents, cron) | High (sandboxed exec) | Moderate (sub-agents, skills) | Low (session-based) | Moderate (daemon agents) | Moderate (warp, sub-agents) | Low (streaming focus) | Moderate (sub-agents) |
| **Enterprise Controls** | Strongest (managed settings, model enforcement) | Moderate (team plans, rate limits) | Moderate (Vertex AI, ADC auth) | Weak (enterprise auth issues) | Weak | Moderate (permissions) | Weak | Minimal |
| **Platform Support** | macOS, Linux, Windows (fragile) | macOS, Linux, Windows (crisis) | macOS, Linux, Windows | macOS, Linux, Windows, ARM64 (crash) | macOS, Linux, Windows (weak) | macOS, Linux | macOS, Linux, Windows | macOS, Linux |
| **MCP Ecosystem** | Mature (bundles, footer badges) | Plugins (bundled, fragile) | Growing (MCP discovery fix) | Growing (respawn loops) | Growing | Moderate (session recovery) | Minimal | Moderate (declarative definitions) |
| **Open Source** | No | No | Yes (Apache 2.0) | Yes (MIT) | Yes (Apache 2.0) | Yes (MIT) | Yes (MIT) | Yes (MIT) |

**Key differentiators:**
- **Claude Code** leads in enterprise controls and agent autonomy but has the highest cost ceiling (recursive sub-agent risk).
- **OpenAI Codex** is in a heavy Rust rewrite transition — high potential but current Windows instability is a major liability.
- **Gemini CLI** and **Qwen Code** are racing to close parity with Claude Code, with Qwen showing stronger Chinese-language community engagement.
- **Pi** is unique in its provider-agnostic, lightweight streaming focus — least ambitious in autonomy, most reliable for basic use.
- **CodeWhale (DeepSeek TUI)** executed a clean rebrand and is methodically building multi-provider support; strongest feature roadmap clarity.

---

## 5. Community Momentum & Maturity

### High Momentum / Rapid Iteration
- **OpenAI Codex** — 4 alpha releases/day signals intense development, but the Windows sandbox crisis (20+ issues) suggests testing/release processes need tightening.
- **Claude Code** — 3 patches/day, strong feature velocity (enforceAvailableModels, footer badges). Community is vocal and engaged but frustrated by false-positive classification and recursive agent costs.
- **Pi** — 50 issues + 15 PRs in 24h indicates a highly active maintainer. The Codex reliability issue (#4945, 55 comments) is the single biggest pain point.
- **OpenCode** — Steady release cadence (v1.17.4), active PR pipeline (10 significant), permission system and doom loop detection are clear growth areas.

### Moderate Momentum / Consolidating
- **Gemini CLI** — Nightly releases, P1 agent hangs being addressed (zero-quota fix merged), but community engagement is lower (8👍 top issue vs. 111👍 for Codex). Team appears methodical, not frantic.
- **CodeWhale (DeepSeek TUI)** — Brand migration completed, 15+ PRs in 24h, but many issues were closed rather than new features. The rebrand may have temporarily slowed community contributions.
- **Qwen Code** — v0.18.0 minor release, but the free-tier policy controversy (#3203, 127 comments) dominates discourse. Chinese-language community is active; English-language participation is lower.

### Lower Momentum / At Risk
- **Kimi Code CLI** — No new release, only 3 issues updated, 1 PR open. The billing transparency issue (#1994) and WebSocket failure (#2435) are unresolved pain points. Lowest activity of all tools tracked.
- **GitHub Copilot CLI** — Only 1 PR active (scaffolding), 75👍 issue #53 untouched for 9 months, terminal rendering regressions (#3749, #3755) unresolved. The release v1.0.62-1 added features, but the PR pipeline is anemic.

---

## 6. Trend Signals for Developers

### For Tool Builders (Product Managers & Engineers)

1. **"Agent safety" is table stakes, not a differentiator.** Recursive sub-agent spawning (Claude Code #68110, Qwen Code #5019), doom loops (OpenCode #12716), and unbounded cost escalation are driving user distrust. Any tool enabling autonomous execution *must* ship depth limits, budget controls, and fail-fast mechanisms before marketing agent features.

2. **Model routing transparency is the next API gateway.** The pattern of "model classification false positives" (Claude Code, Gemini CLI) and "hardcoded model IDs breaking multi-provider setups" (CodeWhale #3018) shows that users want configurable, observable, auditable model routing — not black-box classifiers. This is a platform opportunity akin to API gateways for microservices.

3. **Windows is the "last mile" problem no one is solving.** Every tool tracks macOS and Linux first. OpenAI Codex's Windows sandbox crisis (20+ issues) is a cautionary tale: as tools add sandboxing and plugin systems, Windows UAC, EFS, and packaging differences create disproportionate support burden. Expect a Windows-focused startup to emerge targeting this gap.

4. **Context window management is the fundamental unsolved AI engineering challenge.** Every tool hits context overflow, quality degradation, token waste, or hallucination under extended sessions. Solutions like non-AI context compression (Qwen Code #4264) and AST-aware file reads (Gemini CLI #22745) represent a new category of "context engineering" tools.

5. **The "Claude Code compatibility layer" is becoming a de facto standard.** Qwen Code (#4845), CodeWhale (#3018), and others explicitly target Claude Code's config format for migration. This suggests Claude Code's developer experience patterns (`.claude/` directory, MCP server definitions, custom slash commands) are becoming the industry reference architecture.

### For Tool Users (Developers & Team Leads)

6. **OpenAI Codex is in a high-risk transition.** The Rust rewrite is ambitious, but the Windows sandbox crisis and rapid alpha releases (4/day) suggest instability. Proceed with caution for production workflows; keep v0.132.0 as a rollback target.

7. **Claude Code offers the richest autonomous agent features but requires cost governance.** The `enforceAvailableModels` setting (v2.1.175) is a step in the right direction, but teams should set token budgets, disable the `Agent` tool for sub-agents, and monitor for recursive spawning.

8. **For cross-provider flexibility, Pi and CodeWhale are worth watching.** Pi's provider-agnostic streaming and CodeWhale's newly un-hardcoded multi-provider support offer escape paths from single-vendor lock-in. However, both are lower in community maturity and agent autonomy.

9. **GitHub Copilot CLI's stagnation is a risk for GitHub ecosystem users.** Issue #53 (75👍, 9 months no response) and the anemic PR pipeline suggest the team is either resource-constrained or deprioritizing the CLI. The terminal rendering regressions (#3749, #3755) are particularly concerning for daily drivers.

10. **The free-tier economics are shifting.** Qwen Code's proposed 100→0 daily quota reduction (127 comments) and Claude Code's 20x Max plan requests (#47509, 37👍) indicate that sustainable pricing models are still being figured out. Expect more tools to follow Qwen's path of tightening free tiers and pushing paid plans.

---

**Bottom Line:** The AI CLI tools ecosystem is past the "demo-friendly" phase and entering the "production-hardening" phase. The winners will be those who solve agent safety, cross-platform reliability, and context management — not those who ship features fastest. Windows users, enterprise compliance teams, and cost-conscious autonomous workflow builders are the key constituencies whose needs are currently underserved.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Snapshot: 2026-06-13** | Source: github.com/anthropics/skills

---

## 1. Top Skills Ranking

The following PRs have attracted the most community discussion and represent the most significant skill developments in the ecosystem.

### 1. **document-typography** (#514)
- **Functionality**: Provides typographic quality control for AI-generated documents, preventing orphan word wrap, widow paragraphs, and numbering misalignment—issues pervasive across all Claude-generated documents.
- **Discussion Highlights**: Received strong community validation for solving a universal pain point. Users noted that "every document Claude generates" suffers from these issues, and the skill directly addresses an unmet need without requiring user prompting.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/514)

### 2. **ODT (OpenDocument Text)** (#486)
- **Functionality**: Enables creation, reading, template filling, and conversion of OpenDocument Format files (.odt, .ods), targeting LibreOffice/ISO-standard document workflows.
- **Discussion Highlights**: Significant interest from enterprise users reliant on open-source office suites. The ISO standard compliance angle attracted attention from government and EU institutional users.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/486)

### 3. **frontend-design** (#210)
- **Functionality**: Revises the existing frontend-design skill for improved clarity and actionability, ensuring instructions are executable within a single conversation.
- **Discussion Highlights**: Community debate centered on balancing specificity vs. generality in design prompts. The PR represents a "second generation" approach to skill authoring, focusing on operational precision over educational tone.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/210)

### 4. **skill-quality-analyzer & skill-security-analyzer** (#83)
- **Functionality**: Meta-skills for evaluating other skills across five dimensions (structure, documentation, resources, content quality, security), with security analysis covering code execution risks and data leakage vectors.
- **Discussion Highlights**: Generated discussion about the need for a quality bar in the skills marketplace. Some argued these should be required tooling rather than optional skills.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/83)

### 5. **testing-patterns** (#723)
- **Functionality**: Comprehensive testing skill covering the full stack—unit testing (AAA pattern), React component testing (Testing Library), end-to-end flows, and testing philosophy (Testing Trophy model).
- **Discussion Highlights**: Strong interest from CI/CD-oriented teams. Discussion focused on whether testing patterns should be framework-agnostic or include framework-specific reference implementations.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/723)

### 6. **faf-expert / n8n-builder / n8n-debugger** (#190)
- **Functionality**: Four production-tested skills: faf-expert for persistent project context management, n8n-builder and n8n-debugger for workflow automation, plus additional community skills.
- **Discussion Highlights**: Highest active-comment count among skill proposals. The n8n workflow automation skills received particular attention from the growing no-code automation community.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/190)

### 7. **SAP-RPT-1-OSS predictor** (#181)
- **Functionality**: Enables predictive analytics on SAP business data using SAP's open-source tabular foundation model (Apache 2.0), released at SAP TechEd 2025.
- **Discussion Highlights**: Niche but highly engaged audience from the SAP ecosystem. Discussion centered on integration patterns between Claude Skills and enterprise SAP systems.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/181)

### 8. **agent-creator** (#1140)
- **Functionality**: Meta-skill for generating task-specific agent sets, with fixes for multi-tool evaluation and Windows compatibility.
- **Discussion Highlights**: Represents a "skill for creating skills" approach to agent orchestration. Community feedback requested clearer separation between agent definitions and skill definitions.
- **Status**: Open | [GitHub Link](https://github.com/anthropics/skills/pull/1140)

---

## 2. Community Demand Trends

Analysis of the most-commented Issues reveals five concentrated demand areas:

| Demand Direction | Key Issue | Signal Strength |
|---|---|---|
| **Org-wide skill sharing & distribution** | #228 (14 comments, 7 👍) | **Highest** — Enterprise teams need centralized skill management, direct sharing links, and shared skill libraries instead of file-based manual distribution. |
| **Skill creator/optimizer reliability** | #556 (12 comments, 7 👍), #1169 (3 comments), #1061 (3 comments) | **Critical** — The `run_eval.py` tool consistently reports 0% recall, breaking the description-optimization loop. This is blocking skill authors from improving their skills. |
| **Windows compatibility** | #1061 (3 comments), plus PRs #1099, #1050 | **High** — Path handling, subprocess encoding, and pipe reading all fail on Windows. Multiple independent reproductions suggest significant Windows user base being underserved. |
| **Security & trust boundaries** | #492 (7 comments, 2 👍), #1175 (3 comments) | **Growing** — Community skills distributed under `anthropic/` namespace create trust vulnerability. Users demand official verification or namespace separation. |
| **Skill quality & deduplication** | #189 (6 comments, 8 👍), #62 (10 comments) | **Persistent** — Duplicate skills from overlapping plugin installations, and unexplained skill disappearance, erode user confidence in the ecosystem. |

**Emerging theme**: The community is shifting from *individual skill creation* toward *ecosystem infrastructure*—tooling, distribution, security, and cross-platform support.

---

## 3. High-Potential Pending Skills

These active PRs show sustained community engagement and are likely to land soon:

| Skill | PR | Key Innovation | Status Signal |
|---|---|---|---|
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | Typographic quality control for AI documents | High community interest; addresses universal pain point |
| **ODT skill** | [#486](https://github.com/anthropics/skills/pull/486) | ISO-standard OpenDocument format support | Enterprise demand; low competition |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full-stack testing methodology | Strong tooling ecosystem alignment |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Color naming systems & space selection | Niche but authoritative; from domain expert |
| **faf-expert / n8n-builder / n8n-debugger** | [#190](https://github.com/anthropics/skills/pull/190) | Workflow automation + context management | Highest comment activity; production-tested |
| **skill-quality-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skill for skill evaluation | Foundational for ecosystem quality |

---

## 4. Skills Ecosystem Insight

**The Claude Code Skills community's most concentrated demand is for *operational reliability infrastructure*—skill optimizer tools that work cross-platform, org-wide distribution mechanisms, quality verification standards, and trust-boundary security—rather than for any single domain-specific skill.** The volume of comments on tooling issues (#556, #1061, #1169) now exceeds that of any feature skill proposal, signaling that the community has matured past initial skill creation and is now demanding production-grade ecosystem stability.

---
*Report generated from github.com/anthropics/skills data. All links reference the official Anthropic Skills repository.*

---

# Claude Code Community Digest
**Date:** 2026-06-13

---

## Today's Highlights

Three minor patch releases landed in the last 24 hours, bringing session title language localization, new managed model enforcement controls, and regex-based footer link badges. The community conversation is dominated by two themes: the desire for hierarchical agent architectures (tiered models with persistent state) and mounting frustration around model classification false positives that incorrectly downgrade legitimate security tools. A significant new bug report about unbounded recursive sub-agent spawning highlights growing pains in the autonomous agent features.

---

## Releases

Two new versions shipped since yesterday:

- **`v2.1.177`** — No release notes provided (likely a hotfix or infrastructure-only change).

- **`v2.1.176`** — Three notable additions:
  - **Session titles now respect conversation language**: Titles auto-generate in the language you're speaking. Can be overridden via the `language` setting for multi-language teams.
  - **`footerLinksRegexes` setting**: Adds regex-matched link badges to the terminal footer row, configurable via user or managed settings — useful for compliance tagging, ticket links, or environment badges.
  - **Improved Bedrock credentials handling** (notes truncated in source).

- **`v2.1.175`** — Managed model enforcement:
  - New **`enforceAvailableModels`** managed setting: When enabled, the `availableModels` allowlist also constrains the Default model. If the Default resolves to a disallowed model, it falls back to the first allowed model. Importantly, user or project settings can no longer override managed model restrictions — a win for enterprise compliance teams.

---

## Hot Issues

### 1. **#56913 — Autonomous Claude Code: Tiered Opus Brains + Sonnet Workers + Persistent State**
- *Author: ThatDragonOverThere | Comments: 26*
- **Summary:** The top-voted feature pitch proposes making Claude Code viable as a long-running orchestrator — using Opus for high-level planning, Sonnet for task execution, and persistent state across sessions. The community sees this as unlocking "the operating system for AI development."
- **Why it matters:** This directly addresses the gap between Claude Code as a pair-programming assistant versus an autonomous agent platform.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/56913)**

### 2. **#49917 — Windows Desktop Installer Fails with Inconsistent Package State**
- *Author: ARHAEEM | Comments: 26 | 👍: 6*
- **Summary:** The Windows installer (`AddPackage`) fails with `HRESULT 0x80073CF6` after a partially successful install leaves the package in an inconsistent state. No recovery path is offered.
- **Why it matters:** Installation reliability is a basic hygiene factor. This has been open for nearly two months, suggesting a deep-rooted issue with the Windows packaging pipeline.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/49917)**

### 3. **#16294 — API Error 400 "no low surrogate in string" from Invalid Unicode in Bash Output**
- *Author: coygeek | Comments: 16 | 👍: 1*
- **Summary:** When bash tools return output containing invalid UTF-8 sequences (common with binary files or edge-case character sets), the API rejects the entire response with a 400 error. No graceful fallback or sanitization is applied.
- **Why it matters:** This has been open since January 2026 and affects reliability in CI/CD pipelines where unpredictable command output is common.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/16294)**

### 4. **#68076 — Claude Code Incorrectly Downgrades Legitimate Privacy Scanner to Opus**
- *Author: FabioLeitao | Comments: 5 | 👍: 1*
- **Summary:** The Fable classifier flags `data-boar`, an open-source privacy compliance scanner (LGPD/GDPR/CCPA), as an "offensive" tool, forcing downgrade to Opus. The author is a Senior SRE and the tool is explicitly blue-team by design.
- **Why it matters:** False-positive model downgrades are a serious trust issue — they hamper legitimate security workflows and erode confidence in the model routing system.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/68076)**

### 5. **#67688 — Fable Classifier "Completely Broken" on Linux**
- *Author: michael-greider | Comments: 5 | 👍: 1*
- **Summary:** The Fable model classification system is reportedly non-functional on Linux. The issue doesn't provide extensive detail, but the "completely broken" language suggests a total failure in model routing logic.
- **Why it matters:** Model routing is critical for cost management. A broken classifier could silently switch all Linux users to more expensive models (or break workflows entirely).
- **[View Issue →](https://github.com/anthropics/claude-code/issues/67688)**

### 6. **#47509 — Team Plan Needs Max 20x Equivalent Tier for Power Users**
- *Author: marcoantoniofassa | Comments: 8 | 👍: 37*
- **Summary:** The Team plan's Premium tier (6.25x Pro usage) is insufficient for heavy CLI users — CTOs, tech leads, and senior devs doing agentic coding. Request for a Max 20x equivalent on the Team plan.
- **Why it matters:** This is the highest-reacted issue in this digest (37 upvotes). Organizations want to consolidate billing without capping their heaviest users.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/47509)**

### 7. **#68110 — Sub-Agents Recursively Spawn Unbounded Child Agents (Exponential Fan-Out)**
- *Author: jeffreese | Comments: 2*
- **Summary:** When a `general-purpose` sub-agent has access to the `Agent` tool, it recursively spawns its own child agents, which can also spawn agents — creating an exponential fan-out tree with no depth or count limits. Massive token burn.
- **Why it matters:** This is a critical safety issue for any autonomous agent deployment. Without depth limits, a single research task could theoretically consume unlimited credits.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/68110)**

### 8. **#50911 — `CronCreate durable:true` Silently Ignored, Tasks Die on Session End**
- *Author: sanikaram | Comments: 7 | 👍: 1*
- **Summary:** The `CronCreate` tool accepts a `durable: true` parameter but silently treats every call as session-only. No `.claude/scheduled_tasks.json` is ever written. Scheduled tasks vanish when the session ends.
- **Why it matters:** Durable scheduled tasks are fundamental for background automation — without them, Claude Code cannot serve as a reliable automation platform.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/50911)**

### 9. **#67865 — Claude Desktop Hangs Installing MCP Bundles with Large Deflated Entries**
- *Author: ddmitov | Comments: 3*
- **Summary:** Installing any local `.mcpb` file with a deflated entry larger than ~16 KB causes Claude Desktop to silently hang on Windows. No timeout, no error — just a frozen installer.
- **Why it matters:** The MCP ecosystem is growing, and installer reliability is table-stakes. A silent hang creates a terrible first impression for plugin developers.
- **[View Issue →](https://github.com/anthropics/claude-code/issues/67865)**

### 10. **#44902-44912 (Cluster) — Documentation Gaps Across Permissions, Hooks, SDK, VS Code, MCP, and Environment Variables**
- *Author: coygeek (multiple)*
- **Summary:** A prolific community member has filed a cluster of documentation issues covering missing `sessionTitle` support in hooks, undocumented `ExitWorktree` tool, remote control session archiving behavior, and more.
- **Why it matters:** While individually minor, the volume suggests the docs have not kept pace with features shipped in the last 2-3 months. This erodes developer trust in the documentation as a source of truth.
- *Sample: [#32682](https://github.com/anthropics/claude-code/issues/32682), [#36856](https://github.com/anthropics/claude-code/issues/36856), [#44902](https://github.com/anthropics/claude-code/issues/44902)*

---

## Key PR Progress

### 1. **#26360 — Fix Issues Being Auto-Closed Despite Human Activity**
- *Author: chrislloyd | Status: CLOSED | ⚡ claude-code-assisted*
- **Summary:** Fixes the triage bot's `closeExpired()` logic: the bot now recognizes `stale` and `autoclose` labels, and humans commenting on stale issues triggers automatic label removal. Prevents legitimate issues from being silently auto-closed.
- **Why it matters:** A triage bot that ignores human activity is worse than no bot. This fix restores trust in the issue management process.
- **[View PR →](https://github.com/anthropics/claude-code/pull/26360)**

### 2. **#67753 — Case-Insensitive Completion Promise Matching**
- *Author: nahrinoda | Status: OPEN*
- **Summary:** Completion promise matching now uses case-insensitive comparison with whitespace normalization. Uses portable `tr` instead of `${var,,}` for shell compatibility. Prevents false negatives when Claude outputs differ in casing (e.g., `Complete` vs `COMPLETE`).
- **Why it matters:** This reduces friction in automated agent workflows where output formatting varies.
- **[View PR →](https://github.com/anthropics/claude-code/pull/67753)**

---

*Note: Only 2 PRs were updated in the reporting window. No additional pull requests with significant activity were identified.*

---

## Feature Request Trends

1. **Autonomous Agent Architecture (Tiered Models + Persistent State)** — Issue #56913 is the clearest signal. The community wants Claude Code to graduate from "pair programmer" to "autonomous orchestrator" with **hierarchical model tiers** (Opus for planning, Sonnet for execution), **persistent memory** across sessions, and **durable background tasks**. This is the single most impactful feature direction.

2. **Team/Max Plan Cross-Pollination** — Issue #47509 (37 upvotes): Organizations want the **Max plan's usage limits** available on the Team plan's seats. The gap between 6.25x and 20x Pro usage leaves power users stranded between plans.

3. **Enterprise Model Enforcement Controls** — The `enforceAvailableModels` setting in v2.1.175 directly responds to demand for **managed model routing**. Expect continued demand for more granular controls (per-project, per-user-group) and better error surfaces when routing decisions are made.

4. **MCP Ecosystem Maturity** — Documentation gaps (#56154, #56161), installer reliability (#67865), and reserved name conflicts point to demand for a more **production-ready MCP plugin system**. The ecosystem is growing faster than the infrastructure can support it.

---

## Developer Pain Points

1. **Model Classification False Positives** — Issues #68076 and #67688 both report the **Fable classifier incorrectly downgrading or breaking model routing**. For a tool where model choice directly affects cost and capability, false positives are unacceptable — they block legitimate security tooling and undermine trust in the routing system.

2. **Recursive Agent Spawning / Cost Explosion** — Issue #68110 highlights a **critical safety gap**: sub-agents with access to the `Agent` tool can spawn unlimited child agents. For teams running autonomous workflows, this represents an unbounded cost risk. The lack of depth limits or budget controls is a systemic concern.

3. **Durable vs Non-Durable Ambiguity** — Issue #50911: `CronCreate` accepts a `durable: true` flag but silently ignores it. This pattern — **accepting a parameter without honoring it** — is particularly frustrating for developers who trust the API surface. It suggests insufficient validation at the API layer.

4. **Windows Installation Fragility** — Issue #49917 (open since April) and #67865 (silent hangs on MCP install) paint a picture of **Windows as a second-class platform**. For a developer tool targeting CLI-first workflows, macOS and Linux are clearly the priority, leaving Windows users with persistent reliability issues.

5. **Documentation Obsolescence** — The cluster of documentation issues from a single diligent contributor (coygeek) covers **10+ separate feature gaps** in the official docs. Features like `ExitWorktree`, worktree session resumption, and stream-json input formats shipped without corresponding documentation updates. This suggests the documentation pipeline is either slow or lacks dedicated ownership for keeping pace with releases.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-13

## Today's Highlights
The Codex team shipped four rapid Rust alpha releases (v0.140.0-alpha.14 through .17), signaling intense iteration on the CLI's new architecture. A massive Windows sandbox reliability crisis dominates the issue tracker, with over 20 related bug reports filed in the last two weeks, all sharing the same `spawn setup refresh` and `os error 740` root cause. Meanwhile, a flurry of pull requests around `PathUri` and cross-OS execution infrastructure suggests an upcoming breakthrough for heterogenous app-server/exec-server deployments.

---

## Releases
Four Rust CLI alpha releases in 24 hours:
- **[rust-v0.140.0-alpha.14](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.14)** through **[rust-v0.140.0-alpha.17](https://github.com/openai/codex/releases/tag/rust-v0.140.0-alpha.17)**

These are version bumps with no changelog details published. The rapid cadence (4 versions/day) likely reflects hotfixes or CI packaging refinements for the Rust-based CLI rewrite.

---

## Hot Issues

1. **[#12564 — Allow renaming task/thread titles](https://github.com/openai/codex/issues/12564)** (CLOSED, 78 comments, 111 👍)
   The most-upvoted issue this period. Users strongly desire the ability to rename conversation threads for better navigation. Closed, suggesting a fix shipped or is planned.

2. **[#24391 — Windows sandbox: spawn setup refresh fails](https://github.com/openai/codex/issues/24391)** (CLOSED, 46 comments)
   First major report of the `spawn setup refresh` failure on CLI 0.133.0. Established the pattern that dozens of later issues trace back to.

3. **[#9046 — Context window overflow on fresh threads](https://github.com/openai/codex/issues/9046)** (OPEN, 25 comments)
   Users report hitting context limits immediately, even with a single question. Suggests aggressive prompt stuffing or broken context management.

4. **[#25243 — macOS relaunch loop exhausts syspolicyd](https://github.com/openai/codex/issues/25243)** (OPEN, 20 comments)
   A macOS-specific crash loop that starves system file-descriptor resources, blocking all app launches. High severity for Apple Silicon users.

5. **[#25220 — EFS-encrypted WindowsApps breaks bundled plugins](https://github.com/openai/codex/issues/25220)** (OPEN, 16 comments)
   Windows users with EFS encryption on WindowsApps cannot use Computer Use, Browser, Chrome, or LaTeX plugins. Affects Chinese-market Windows 11 Home users.

6. **[#27175 — Desktop crashes after update 26.602.71036](https://github.com/openai/codex/issues/27175)** (OPEN, 15 comments)
   Pro ($200/mo) subscribers report the app becomes inaccessible post-update even with empty sessions. Critical regression.

7. **[#22335 — CLI remote compaction fails, breaks task continuity](https://github.com/openai/codex/issues/22335)** (OPEN, 6 comments, 8 👍)
   Remote compaction for resumed threads silently drops task context. Affects Pro users on gpt-5.5 high/xhigh reasoning.

8. **[#27979 — Windows App 26.609.4994.0 fails to open](https://github.com/openai/codex/issues/27979)** (OPEN, 6 comments)
   Fresh regression: the latest Windows Store update completely prevents the app from launching.

9. **[#27694 — macOS DockTilePlugin recursion crash](https://github.com/openai/codex/issues/27694)** (OPEN, 4 comments, 3 👍)
   `CodexDockTilePlugin setDockTile` enters infinite recursion, crashing the app on macOS. Affects Pro Max subscribers.

10. **[#27970 — HTTP 429 despite available quota](https://github.com/openai/codex/issues/27970)** (CLOSED, 2 comments)
    Pro x20 subscribers hit rate limits incorrectly. Closed quickly, likely a server-side fix or configuration change.

---

## Key PR Progress

1. **[#28007 — shell: reject foreign environments before host execution](https://github.com/openai/codex/pull/28007)**
   Prevents shell commands from running on the wrong OS host. Critical safety guard for the cross-OS execution model.

2. **[#28006 — core: retain executor environment identity](https://github.com/openai/codex/pull/28006)**
   Preserves cwd, path convention, and shell across turns/resume/fork without projecting foreign paths onto the host.

3. **[#27937 — Add hermetic Wine exec-server test](https://github.com/openai/codex/pull/27937)**
   Enables cross-OS app-server/exec-server testing using Wine. Foundation for Windows exec-server on Linux orchestrators.

4. **[#28002 — Send turn state through compact requests](https://github.com/openai/codex/pull/28002)**
   Ensures inline compaction carries the active turn's state through sampling requests. Fixes context corruption during compaction.

5. **[#27819 — path-uri: render native paths across platforms](https://github.com/openai/codex/pull/27819)**
   Translates PathUri to user-visible native paths at the app-server API boundary. Key UX piece for cross-OS support.

6. **[#27713 — Prototype multi-provider workload identity auth](https://github.com/openai/codex/pull/27713)**
   Replaces Azure-only auth with a multi-provider system. Marked "do not merge" but represents major infrastructure change.

7. **[#28001 — Package Windows ARM64 on x64](https://github.com/openai/codex/pull/28001)**
   Parallelizes Windows packaging to eliminate the ARM64 build as a release bottleneck. CI optimization.

8. **[#27955 — retain resolved turn environments in session state](https://github.com/openai/codex/pull/27955)**
   Eliminates redundant re-resolution of execution environments on every turn. Performance improvement and correctness fix.

9. **[#27995 — preserve explicit environment cwd](https://github.com/openai/codex/pull/27995)**
   Stops `TurnEnvironmentSelections::new` from overwriting the selected environment's explicit working directory with the legacy fallback.

10. **[#27977 — Show standalone image generation as active TUI status](https://github.com/openai/codex/pull/27977)**
    Adds `Generating image` status header to the TUI during image generation. Small UX improvement.

---

## Feature Request Trends

- **Thread/task management**: Renaming threads (#12564, 111 👍) is the most-requested feature. Users need better history navigation and organizational control.
- **Cross-OS execution**: The entire PathUri and environment identity PR stack signals strong demand for running exec-servers on different OSes than the orchestrator.
- **Multi-provider authentication**: PR #27713 and related issues suggest enterprise users need workload identity federation beyond Azure.
- **Plugin isolation and reliability**: Repeated plugin failures (bundled plugins, MCP servers, node_repl) indicate users want more robust plugin sandboxing and configuration persistence.

---

## Developer Pain Points

1. **Windows sandbox crisis**: The `spawn setup refresh` / `os error 740` / `ERROR_ELEVATION_REQUIRED` failure cluster is the single biggest pain point. Over 20 issues filed in 2 weeks, affecting CLI (0.133.0+), Desktop (Store and standalone), and all sandbox-dependent features (Computer Use, Browser, Chrome, node_repl, LaTeX). The root cause traces to UAC elevation requirements for `codex-windows-sandbox-setup.exe` in AppData runtime cache. Multiple issues report successful rollback to CLI 0.132.0.

2. **Crash loops after updates**: Both macOS (#25243) and Windows (#27175, #27979) exhibit relaunch loops or complete app inaccessibility after updates. These affect paying subscribers (Pro $20, Pro $200) and erode trust in the update pipeline.

3. **Context window mismanagement**: Issue #9046 (25 comments) shows users hitting context limits on brand-new threads with single questions. This suggests either aggressive prompt construction or broken context accounting.

4. **Rate limiting false positives**: Issue #27970 confirms that even high-tier subscribers (Pro x20) hit HTTP 429 errors with ample remaining quota. While closed, it indicates flaky rate-limit enforcement.

5. **Configuration non-determinism**: Multiple Windows reports (#25090, #26530, #24727) describe node_repl MCP config being regenerated or overwritten on restart, breaking user customizations.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-13

## Today's Highlights

A large nightly release (v0.48.0) lands with a critical fix for MCP tool discovery atomicity and a Vertex AI model mapping correction. Agent reliability remains the community's top concern, with ongoing discussions around hangs, subagent recovery failures, and tool overload (400 errors with >128 tools). The team is actively merging PRs to cap oversized tool responses and harden shell command parsing.

## Releases

**v0.48.0-nightly.20260613.g9e5599c32** — [Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.48.0-nightly.20260613.g9e5599c32)
- `fix(core): implement atomic update in MCP tool discovery` – prevents race conditions when discovering MCP tools
- `Vertex AI model mapping fix` – corrects model routing for Vertex AI deployments
- `Add documentation and migration command` – improves onboarding for new version upgrades

## Hot Issues (10 notable)

1. **#24353** — [Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353) (7 comments, P1)
   *Why it matters:* Follow-up to behavioral evals (#15300). With 76 tests spanning 6 Gemini models, this EPIC drives systematic quality measurement. Community silence suggests broad consensus.

2. **#22745** — [AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745) (7 comments, P2)
   *Why it matters:* Could dramatically reduce token usage and turn count by reading method bounds in a single call. One 👍 indicates developer interest in efficiency gains.

3. **#21409** — [Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409) (7 comments, P1, 8 👍)
   *Community reaction:* Most-voted issue. Users report CLI hanging indefinitely on simple tasks (folder creation). Workaround exists (disable sub-agents), but the hang is blocking adoption.

4. **#22323** — [Subagent recovery after MAX_TURNS reports GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323) (6 comments, P1)
   *Why it matters:* Misleading `status: "success"` when subagent actually hit turn limits. Breaks trust in agent completion signals for CI/automation workflows.

5. **#21968** — [Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968) (6 comments, P2)
   *Why it matters:* Custom skills (gradle, git) are ignored unless explicitly told to use them. Reduces value of skill ecosystem for power users.

6. **#26525** — [Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525) (5 comments, P2, security)
   *Why it matters:* Secrets sent to model before redaction happens. Auto Memory's background extraction agent reads transcripts that may contain credentials. Security-sensitive fix.

7. **#26522** — [Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522) (5 comments, P2)
   *Why it matters:* Auto Memory only marks sessions as processed when read successfully. Low-signal sessions get re-surfaced endlessly, wasting API calls and compute.

8. **#25166** — [Shell command execution stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166) (4 comments, P1, 3 👍)
   *Community reaction:* Simple CLI commands (no prompts) hang post-execution. High frustration for daily shell-driven workflows.

9. **#24246** — [Gemini CLI encounters 400 error with >128 tools](https://github.com/google-gemini/gemini-cli/issues/24246) (3 comments, P2)
   *Why it matters:* MCP + custom skills quickly exceed 128-tool limit. Users want smarter tool selection/scoping rather than a hard cap.

10. **#22672** — [Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672) (2 comments, P2, 1 👍)
    *Why it matters:* Models occasionally use `git reset --force` or destructive DB commands when safer alternatives exist. Safety net needed for production repos.

## Key PR Progress (10 important)

1. **#27870** — [fix(core): cap pending tool responses](https://github.com/google-gemini/gemini-cli/pull/27870)
   *Open, P1, size/m.* Fixes #27738 — prevents extremely large tool results from exceeding context limits by capping pending `functionResponse`. Directly addresses the `>128 tools` issue.

2. **#27867** — [fix(a2a-server): prevent crash when tasks metadata endpoint returns 501](https://github.com/google-gemini/gemini-cli/pull/27867)
   *Open, P1, help wanted.* Fixes #21729 — graceful handling of unimplemented A2A endpoints.

3. **#27698** — [fix(core): Ensure zero-quota limits fail fast to prevent retry loop hang](https://github.com/google-gemini/gemini-cli/pull/27698)
   *Closed.* Fixes critical bug where unbilled accounts get stuck in 10-attempt retry loop. Directly related to #21409 (generalist agent hangs).

4. **#27873** — [fix(core): improve SKILL.md frontmatter parsing robustness](https://github.com/google-gemini/gemini-cli/pull/27873)
   *Closed, size/m.* Resolves #25693 — adds BOM support, trims trailing whitespace on frontmatter markers, normalizes YAML values.

5. **#27872** — [fix(core): strip line/range suffix from at-command paths to avoid CLI hang](https://github.com/google-gemini/gemini-cli/pull/27872)
   *Closed, size/m.* Fixes #19985 and #19239 — `@file:12` patterns were causing hangs. Also updates `/clear` command docs.

6. **#27871** — [fix(core): merge existing refresh token when caching credentials](https://github.com/google-gemini/gemini-cli/pull/27871)
   *Closed.* Fixes #21691 — prevents credential cache corruption on token refresh.

7. **#27856** — [fix: upgrade shell-quote to 1.8.4 (CVE-2026-9277)](https://github.com/google-gemini/gemini-cli/pull/27856)
   *Open, security.* Critical severity CVE. Trivy scanner flagged shell-quote vulnerability. Must-merge for security-conscious deployments.

8. **#27848** — [feat(cli): add 'models' command to list available Gemini models](https://github.com/google-gemini/gemini-cli/pull/27848)
   *Open, P3, size/l.* Adds `gemini models` with context window limits, tiers, and JSON output. Useful for model selection scripts.

9. **#27863** — [fix(core): prioritize structured display titles in tool invocation](https://github.com/google-gemini/gemini-cli/pull/27863)
   *Open, P1, help wanted.* Fixes #23018 — ensures tool titles render correctly in non-interactive mode.

10. **#27862** — [fix(cli): preserve executing subagent tool calls in UI](https://github.com/google-gemini/gemini-cli/pull/27862)
    *Open, P2, help wanted.* Fixes #22589 — subagent tool calls disappearing from UI during execution.

## Feature Request Trends

1. **AST-aware tooling** — Multiple issues (#22745, #22746, #22747) ask for syntax-tree aware file reads, searches, and codebase mapping. Goal: reduce token usage and improve read precision.

2. **Better subagent/skill orchestration** — Users want the agent to *automatically* select appropriate skills and sub-agents (#21968). Current behavior requires explicit prompting, defeating the purpose of skill definitions.

3. **Agent safety controls** — Calls for guards against destructive commands (#22672), better tool scoping (>128 tool limit, #24246), and fail-fast on permission issues (#22093).

4. **Memory system maturity** — Auto Memory improvements (deterministic redaction #26525, skip low-signal sessions #26522, quarantine invalid patches #26523) dominate the memory feature requests.

## Developer Pain Points

- **Agent hangs & stuck states** (#21409, #25166, #22323) — Top frustration. Users report indefinite hangs on simple tasks, and misleading success reports when agents actually hit limits.
- **Configuration ignored** — Subagent/browser settings overrides are silently ignored (#22267, #22093). Leads to unexpected agent behavior after upgrades.
- **Tool overload** — System breaks at 128+ tools (#24246) with no graceful degradation. MCP heavy users hit this quickly.
- **UI/terminal issues** — Corruption after external editors (#24935), flicker on resize (#21924), incorrect escape handling (#22466). Worsens with complex workflows.
- **Security concerns** — Secrets sent to model before redaction (#26525), CVE in shell-quote (#27856), symlinks not recognized as agents (#20079). Erosion of trust for production use.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-06-13

## Today's Highlights

A new patch release `v1.0.62-1` landed with session-scoped extensions, YOLO-mode indicators, and GitHub search support from the CLI footer. However, the community is grappling with a burst of terminal rendering regressions and MCP server reliability bugs in the latest builds. The long-running issue #53 (Bring back Copilot CLI commands) remains the most-reacted open issue at 75 👍, with no official response after 9 months.

---

## Releases

**v1.0.62-1** — Patch release with several notable additions:
- **YOLO mode indicator** — visual footer cue and `allow-all` state in custom `statusLine.command`
- **GitHub search** — press `/` on Issues or Pull Requests tabs for server-side filtered search
- **Session-scoped extensions & canvases** — improved isolation for multi-session workflows
- **Configurable session memory threshold** — SDK clients can now tune compaction behavior

---

## Hot Issues (Top 10 by Community Interest)

### #53 — [OPEN] Bring back GitHub Copilot CLI commands to not break workflows
**Author:** EDM115 | **👍 75** | **💬 37**
The most upvoted open issue. After 9 months of silence, the community has forked alternatives like `shell-ai`. Poses existential risk to CLI adoption if workflows remain broken.
[🔗 Issue #53](https://github.com/github/copilot-cli/issues/53)

### #618 — [CLOSED] Support custom slash commands from .github/prompts directory
**Author:** AungMyoKyaw | **👍 99** | **💬 31**
Highly requested feature parity with Claude Code. Now closed, suggesting possible implementation in a recent build. Signals growing demand for customization parity.
[🔗 Issue #618](https://github.com/github/copilot-cli/issues/618)

### #1481 — [CLOSED] SHIFT+ENTER should spawn line break, but executes prompt
**Author:** mithunshanbhag | **👍 15** | **💬 26**
Standard UX expectation broken. Closed, likely fixed in recent builds. Represents ergonomic friction that frustrates daily drivers.
[🔗 Issue #1481](https://github.com/github/copilot-cli/issues/1481)

### #3749 — [OPEN] Terminal streaming renderer corrupts output — characters doubled/truncated
**Author:** Richard-Marlow | **👍 7** | **💬 5**
Critical rendering bug affecting all users with streaming output. Duplicates characters, truncates tokens, repeats lines. Serious quality-of-life regression.
[🔗 Issue #3749](https://github.com/github/copilot-cli/issues/3749)

### #3755 — [OPEN] Reasoning/thinking display garbles streamed text with duplicated overlapping chunks
**Author:** corinex-spencer | **👍 2** | **💬 5**
Related to #3749. "from" renders as "fromply from", "number" as "numbnumber". Raises questions about regression testing on the streaming renderer.
[🔗 Issue #3755](https://github.com/github/copilot-cli/issues/3755)

### #2627 — [OPEN] Configurable system prompt — allow users to slim down fixed token overhead
**Author:** ronkeele | **👍 17** | **💬 2**
~20,500 token system prompt overhead before any user input. Concerns about wasted context window, especially for users on smaller models. Power-user request.
[🔗 Issue #2627](https://github.com/github/copilot-cli/issues/2627)

### #1999 — [OPEN] Cannot enter @ on German keyboard (Alt-Gr + q)
**Author:** marcschier | **👍 1** | **💬 9**
Long-standing internationalization bug. Makes CLI unusable for German keyboard users. Recurring issue (# also affected). Simple fix with high usability impact.
[🔗 Issue #1999](https://github.com/github/copilot-cli/issues/1999)

### #2306 — [OPEN] Enterprise auth: intermittent "not authorized" errors
**Author:** stewartadvt | **👍 3** | **💬 6**
Intermittent authorization failures (2-3 times/week). Enterprise users lose productivity to flaky auth. No permanent resolution visible.
[🔗 Issue #2306](https://github.com/github/copilot-cli/issues/2306)

### #3782 — [OPEN] MCP stdio server respawned in unbounded tight loop (no backoff) in 1.0.61
**Author:** carlosmayol | **👍 0** | **💬 0**
Fresh regression: unbounded MCP server process spawning causes runaway resource consumption. Dangerous for production environments.
[🔗 Issue #3782](https://github.com/github/copilot-cli/issues/3782)

### #3784 — [OPEN] Copilot CLI v1.0.62-1 aborts with Tokio reactor panic on Linux ARM64
**Author:** kyle-mccarthy | **👍 0** | **💬 0**
Critical crash on latest patch for ARM64 (Apple Silicon, Raspberry Pi). WebSocket panic after first message. Blocks new installs on ARM.
[🔗 Issue #3784](https://github.com/github/copilot-cli/issues/3784)

---

## Key PR Progress

Only one PR was updated in the last 24 hours, limiting coverage:

### #3771 — [OPEN] Initial project setup
**Author:** limenpchuolto112-creator  
Basic scaffolding PR. No substantive changes yet. Low impact.
[🔗 PR #3771](https://github.com/github/copilot-cli/pull/3771)

*Note: No significant feature or bug-fix PRs were active in this window. Most development activity appears concentrated on the release v1.0.62-1 rather than open PRs.*

---

## Feature Request Trends

1. **Customizability & Configuration** — Strong demand for configurable system prompts (#2627), custom slash commands (#618, now closed), and per-repo/global long-running goals (#3364). Users want control over token budgets and behavior without modifying core code.

2. **Enterprise & Auth Robustness** — Intermittent authorization failures (#2306), ACP custom provider support (#3048), and enterprise MCP policy enforcement (#3756) signal enterprise adoption hitting friction points.

3. **Session & Memory Management** — Auto-compaction loops (#3621), session switching shortcuts (#3779), and chronicle reindex issues (#3777) indicate that the session model needs UX and reliability polish.

4. **Plugin Ecosystem** — Auto-update plugins on startup (#3331) suggests growing adoption of the plugin marketplace with desire for seamless updates.

5. **Observability & Cost Tracking** — OpenTelemetry cost metrics (#3778) mirrors parity requests with Claude Code’s cost reporting.

---

## Developer Pain Points

1. **Terminal Rendering Regressions (CRITICAL)** — Multiple reports (#3749, #3755, #3769, #3780, #982) of corrupted streaming output across platforms. Characters doubled, truncated, or overlapping. This is the top pain point affecting all users.

2. **MCP Server Stability** — Unbounded respawn loops (#3782), fetch failures on Windows (#3455), and third-party MCP policy blocks (#3756) undermine MCP reliability.

3. **International Keyboard Input** — German (#1999) and Polish (#2920) AltGr combinations untypeable. Essential characters like `@` and `#` blocked. Makes CLI non-functional for European users.

4. **Platform-Specific Crashes** — Linux ARM64 Tokio panic (#3784) on the latest release. Windows scroll bar alignment (#3501). Platform parity remains fragile.

5. **Session Compaction & Hangs** — 8-minute freezes after compaction (#1614), infinite compaction loops with large instruction files (#3621). Users lose confidence in session reliability.

6. **Silent Failures / No Feedback** — Session hangs without timeout (#1614), MCP server loops without backoff (#3782). Lack of user-visible progress indicators for background operations.

7. **Inconsistent Configuration Resolution** — Custom agents resolved from git root but skills/MCP from cwd (#3688). Leads to confusing behavior for monorepos and complex setups.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

Here is the **Kimi Code CLI Community Digest** for **2026-06-13**.

---

## Kimi Code CLI Community Digest
**Date:** 2026-06-13
**Data Source:** [github.com/MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

### 1. Today's Highlights
No new releases landed in the last 24 hours, but the community is actively discussing two persistent pain points: a severe token billing discrepancy for the K2.6 model and a looping bug that traps the CLI in an infinite file read cycle on Arch Linux. Additionally, a critical WebSocket initialization failure is rendering the "Work" tab completely unusable for Windows users on v1.41.0.

---

### 2. Releases
**None.** No new versions were published in the last 24 hours.

---

### 3. Hot Issues
*Picked from 3 issues updated in the last 24h.*

1.  **[Bug] Kimi CLI stuck in reading one file again and again (Issue #640)**
    - **Summary:** The CLI enters an infinite loop, repeatedly reading the same file. The user is running v0.76 on Arch Linux with a custom Anthropic endpoint and the `mimo-v2-flash` model.
    - **Why it matters:** This is a severe workflow blocker that halts all productivity. The 8 comments indicate active debugging but no resolution yet.
    - **Community Reaction:** Low engagement (1 👍), but high urgency for the reporter.
    - **Link:** [Issue #640](https://github.com/MoonshotAI/kimi-cli/issues/640)

2.  **[Bug] kimiCode用量计算有问题 / Usage calculation problem (Issue #1994)**
    - **Summary:** A user reports that their 2-hour subscription quota is consumed after only 2 tasks because the K2.6 model's excessively long "thought chain" (思维链) burns through tokens. The user expected billing per API request, not per token.
    - **Why it matters:** This is a core economic friction point for the platform. Users feel misled about the "300–1200 requests per 5 hours" promise, which does not account for K2.6’s high token consumption.
    - **Community Reaction:** High (7 👍), indicating broad agreement and frustration.
    - **Link:** [Issue #1994](https://github.com/MoonshotAI/kimi-cli/issues/1994)

3.  **[Bug] Work tab: "Daimon control WS not ready" + infinite reload (Issue #2435)**
    - **Summary:** On Windows 10/11 with Kimi CLI v1.41.0, the `kimi web` Work tab fails to load due to a WebSocket daemon initialization error, causing a continuous 99% reload loop.
    - **Why it matters:** The Work tab is a primary interface for many users. A broken WebSocket handshake makes an entire frontend feature non-functional.
    - **Community Reaction:** Very new (created 2026-06-06), only 1 comment but represents a critical Windows-specific regression.
    - **Link:** [Issue #2435](https://github.com/MoonshotAI/kimi-cli/issues/2435)

---

### 4. Key PR Progress

1.  **fix: guard trafilatura import to prevent cascading tool load failure on Python 3.13 (PR #1597)**
    - **Description:** Fixes a compatibility issue where `charset-normalizer` ships incompatible `.so` binaries on Python 3.13, causing `trafilatura` (and thus the entire `web` tool module) to fail.
    - **Impact:** Directly unblocks users on the latest Python runtime.
    - **Status:** Still Open (updated 2026-06-12).
    - **Link:** [PR #1597](https://github.com/MoonshotAI/kimi-cli/pull/1597)

---

### 5. Feature Request Trends
*Based on analysis of all open issues:*

- **Usage Transparency & Fair Billing:** The top recurring request is for transparent token-to-request mapping. Users are frustrated that "API request" limits are effectively meaningless when a single request can cost as many tokens as 50 requests when using models like K2.6. A dashboard or real-time quota estimator is implicitly demanded.
- **Model-Agnostic Quota Consumption:** Users want the billing system to either cap long context windows or offer a fixed-cost "per request" tier, separate from token-based billing.
- **Resilience & Error Recovery:** The #640 infinite loop and #2435 WebSocket hang point to a broader need for better error handling and watchdog timers to prevent the CLI from entering unrecoverable states.

---

### 6. Developer Pain Points
- **Mismatched Billing Expectations:** The gap between "5 hours = 300–1200 requests" marketing and the reality of 2 tasks draining the quota is the single loudest complaint right now (Issue #1994).
- **Infinite Loops & Stalls:** The CLI entering a file-read loop on Linux (Issue #640) is a hard crash that requires manual process killing—no graceful timeout exists.
- **Frontend State Corruption:** WebSocket daemon failures on Windows (Issue #2435) completely brick the web UI with no user-facing recovery mechanism other than reinstall or restart.
- **Python 3.13 Runtime Incompatibility:** Though a PR exists (PR #1597), the fact that a core dependency (`trafilatura`) fails silently on the latest Python version highlights fragility in the web fetching tool chain.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — June 13, 2026

## Today's Highlights

The v1.17.4 release landed with improved local MCP server support (workspace-relative `cwd`) and connector-based authentication flows, while the community grappled with persistent permission system bugs and doom loop detection gaps. A major PR adds database doctor/repair CLI commands to address SQLite corruption issues, and documentation cleanup is underway following the removal of the scout agent.

---

## Releases

### [v1.17.4](https://github.com/anomalyco/opencode/releases/tag/v1.17.4)
- **Core improvements:** Added `cwd` support for local MCP servers to start from workspace-relative directories (@Grantmartin2002)
- Added connector-based authentication flows with stored provider credentials support
- Added v2 API endpoints for session creation and listing

---

## Hot Issues (Top 10 by Community Activity)

1. **[#27436 — Permission required cannot select](https://github.com/anomalyco/opencode/issues/27436)**  
   *16 comments, 11 👍* — Users report the permission dialog is stuck in a loop: "Allow once" is unclickable, "Allow always" keeps re-prompting, and "Reject" blocks content submission. This blocks basic workflow and has attracted significant frustration.

2. **[#31996 — Invalid JSON Schema due to unsupported regex lookaround on GPT 5.5](https://github.com/anomalyco/opencode/issues/31996)**  
   *11 comments, 5 👍* — Recently closed. Requests fail before reaching OpenAI-compatible models because OpenCode generates regex patterns with lookarounds in fileKey patterns, which the JSON Schema validator rejects. A compatibility blocker for GPT 5.5 users.

3. **[#12716 — Doom loop not caught during reasoning or output](https://github.com/anomalyco/opencode/issues/12716)**  
   *9 comments, 3 👍* — Long-standing issue (since Feb). Agents can enter infinite reasoning loops without detection, burning API credits. The doom loop detection system misses cases where the model cycles through internal reasoning rather than tool calls.

4. **[#14187 — Add markdown preview toggle in file viewer sidebar](https://github.com/anomalyco/opencode/issues/14187)**  
   *8 comments, 22 👍* — Heavily upvoted feature request. Users want rendered markdown previews (`.md`, `.mdx`) instead of raw syntax-highlighted source when browsing files. Strong community appetite.

5. **[#16885 — JSON→SQLite migration reruns on channel-specific DBs](https://github.com/anomalyco/opencode/issues/16885)**  
   *8 comments, 8 👍* — Startup migration runs on every launch for non-`latest` channels (dev/local builds). A related PR (#21056) has been merged today to fix this.

6. **[#16610 — OpenCode hangs at startup with .git repo and exhausted inotify instances](https://github.com/anomalyco/opencode/issues/16610)**  
   *8 comments, 7 👍* — Linux users with low `inotify.max_user_instances` hit a hard hang. No graceful fallback or error message.

7. **[#24335 — Permission wildcard `*` overwrites lower permissions](https://github.com/anomalyco/opencode/issues/24335)**  
   *7 comments, 4 👍* — Despite documentation saying "last matching rule wins," wildcard rules override more specific rules placed after them. Permission system inconsistency.

8. **[#31204 — `session_message.seq NOT NULL constraint failed` on agent-switched sessions](https://github.com/anomalyco/opencode/issues/31204)**  
   *6 comments, 2 👍* — After latest DB migrations (June 3-5), any session triggering an agent switch crashes with a SQLite NOT NULL error. Broke session continuity for multi-agent workflows.

9. **[#18108 — Truncated tool calls misclassified as invalid, causing unrecoverable doom loops](https://github.com/anomalyco/opencode/issues/18108)**  
   *6 comments, 2 👍* — When LLM output exceeds `maxOutputTokens` mid-JSON, OpenCode misclassifies it as "invalid tool call" with no truncation signal. Session exits silently or enters doom loop.

10. **[#27302 — Warp mode + Q&A captures all input, user must force-close terminal](https://github.com/anomalyco/opencode/issues/27302)**  
    *3 comments, 6 👍* — In warp mode (`/warp`), interactive Q&A captures mouse clicks, Enter, and Ctrl+C — no escape possible. High frustration for warping users.

---

## Key PR Progress (Top 10)

1. **[#32128 — fix(app): reconcile session_status in bootstrap so stale busy clears](https://github.com/anomalyco/opencode/pull/32128)**  
   Fixes the "working" indicator that never clears. Bootstrap used `setStore` instead of `reconcile`, leaving sessions permanently stuck in "working" state. *(Closes #17657)*

2. **[#32093 — feat(opencode): add db doctor and repair commands](https://github.com/anomalyco/opencode/pull/32093)**  
   Native CLI tooling to diagnose and repair SQLite database issues. Addresses 10+ related issues including NOT NULL constraint failures and inconsistent session data.

3. **[#32130 — feat(tui): Use opencode-specific tmp filename for 'editor_open'](https://github.com/anomalyco/opencode/pull/32130)**  
   Allows personal editor configs to detect and apply custom behaviors (snippets, formatting) specifically to OpenCode prompt buffers.

4. **[#32129 — fix(mcp): refresh prompt slash commands](https://github.com/anomalyco/opencode/pull/32129)**  
   Ensures MCP-provided slash commands are refreshed properly without stale cache.

5. **[#21056 — fix(opencode): DB migrating on every run for non-latest channels](https://github.com/anomalyco/opencode/pull/21056)**  
   **Merged today.** Fixes #16885 — channel-specific DB paths no longer re-run startup migrations on every launch.

6. **[#32115 — Add TrustedRouter provider](https://github.com/anomalyco/opencode/pull/32115)**  
   New provider profile for TrustedRouter, backed by OpenAI-compatible API at `https://api.trustedrouter.com/v1`. Includes tests and exports.

7. **[#32125 — fix(sdk): normalize scheme-less base URLs so location query params apply](https://github.com/anomalyco/opencode/pull/32125)**  
   Fixes `opencode attach localhost:4096` where scheme-less URLs caused query parameters from location to be lost.

8. **[#31529 — fix(plugin): prevent spinner garbage output in non-TTY environments](https://github.com/anomalyco/opencode/pull/31529)**  
   Spinner animation now suppresses correctly in CI/CD and PowerShell — no more `◓ ◑ ◒ ◐` garbage on each line.

9. **[#32088 — fix(opencode): recover expired MCP sessions](https://github.com/anomalyco/opencode/pull/32088)**  
   Patches `@modelcontextprotocol/sdk` to reinitialize Streamable HTTP sessions after 404 responses, with coalesced retry logic for concurrent failures.

10. **[#32123 — docs: remove references to deleted scout agent](https://github.com/anomalyco/opencode/pull/32123)**  
    Cleans up documentation following scout agent removal (#30435). Updates subagent count and environment variable references.

---

## Feature Request Trends

1. **Markdown rendering in file viewer** — #14187 (22 👍) demands rendered preview for `.md`/`.mdx` files instead of raw source.
2. **Dynamic window title** — #31423 requests session+project name in browser tab title for multi-project users.
3. **Token throughput telemetry** — #30164 (open PR) adds live token-per-second estimates in TUI footer.
4. **Human-readable task IDs** — #32122 (open PR) allows slugs like `"explore-auth"` instead of opaque UUIDs for task tool invocations.
5. **Ads/kickback integration** — #32106 proposes ad revenue sharing for brand partnerships, though early stage (2 comments).
6. **Winget upgrade support** — #30026 requests `opencode upgrade` to use `winget upgrade --id SST.opencode` for Windows users.

---

## Developer Pain Points

1. **Permission system unreliability** — Multiple issues (#27436, #24335, #18441, #24429) show the permission dialog is stuck in loops, wildcard logic is inverted, and `external_directory: "allow"` overrides explicit `edit: "deny"` rules. This is the most frequent source of workflow-blocking bugs.

2. **Doom loop detection gaps** — Issues #12716, #18108, #25254, #17169 all describe infinite retry/prompt loops that go undetected, burning API credits ($15+ per subagent invocation reported). Detection fails for reasoning-only loops, cross-message repetitions, and truncated tool calls.

3. **SQLite database fragility** — Migration reruns (#16885), NOT NULL constraint failures (#31204), missing session data — multiple issues point to an overly complex migration system that breaks on channel-specific installations and after agent switches.

4. **Startup hangs and resource exhaustion** — inotify limits (#16610) and .git watchers cause hard hangs with no error message. No graceful degradation path for resource-constrained environments.

5. **Session state inconsistencies** — Stale "working" indicators (#32127/#32128), truncated subagent output (#32131), and input capture in warp mode (#27302) erode trust in session management. These bugs make it hard to know whether an agent is actually working or stuck.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-13

## Today's Highlights
The repository saw a burst of activity with **50 updated issues and 15 PRs** in 24 hours. A critical fix landed for `pi update` triggering project trust dialogs, and a significant new `AiGameAgent` package was integrated for HTML5/WeChat game development workflows. Community frustration is mounting around **OpenAI Codex connection reliability** (55 comments) and **streaming hang/deadlock issues** across multiple providers.

## Releases
**v0.79.2** — New release bundled improved Amazon Bedrock validation guidance with clearer error links to AWS data retention docs.
- [Release v0.79.2](https://github.com/earendil-works/pi/releases/tag/v0.79.2)

## Hot Issues

1. **#4945 — OpenAI Codex Connection Reliability** (55 comments, 30 👍)  
   `openai-codex` / `gpt-5.5` TUI hangs on "Working..." with no output; only Escape recovery works. Persistent over days. **Major community pain point.**  
   [Issue](https://github.com/earendil-works/pi/issues/4945)

2. **#5363 — Amazon Bedrock Mantle Provider Request** (12 comments)  
   Existing `amazon-bedrock` provider uses Converse API; Mantle models need OpenAI-compatible endpoint. Community wants support added.  
   [Issue](https://github.com/earendil-works/pi/issues/5363)

3. **#5653 — Shrinkwrap Causes Duplicate Provider Registries** (5 comments)  
   Two copies of `pi-ai` on disk due to `npm-shrinkwrap.json` split the provider registry Map. **Core architectural bug flagged for fix.**  
   [Issue](https://github.com/earendil-works/pi/issues/5653)

4. **#5667 — Bash Overflow Spill Crashes on macOS TMPDIR** (6 comments)  
   When bash output exceeds truncation limits, Pi crashes with `EACCES` if `$TMPDIR` is macOS placeholder path. Freshly reported and critical for macOS users.  
   [Issue](https://github.com/earendil-works/pi/issues/5667)

5. **#5657 — Single `+` Rendered as `-` in TUI** (3 comments)  
   Purely cosmetic but bizarre bug: lone plus signs display as minus signs in message history. Data integrity is fine.  
   [Issue](https://github.com/earendil-works/pi/issues/5657)

6. **#5673 — vLLM DeepSeek Thinking Format** (3 comments)  
   Need `chat_template_kwargs: { thinking: true }` for DeepSeek models behind vLLM proxies. Corporate deployment request.  
   [Issue](https://github.com/earendil-works/pi/issues/5673)

7. **#5595 — maxTokens Not Passed Through for OpenAI Completions** (4 comments)  
   Together.ai / DeepSeek v4pro users hit output token caps regardless of settings; `maxTokens` parameter is ignored.  
   [Issue](https://github.com/earendil-works/pi/issues/5595)

8. **#5654 — `excludeFromContext` for Custom Messages** (3 comments)  
   Feature request to mirror bash execution flags for custom messages, enabling status displays without bloating LLM context.  
   [Issue](https://github.com/earendil-works/pi/issues/5654)

9. **#5677 — OpenAI-Compatible Context Overflow Not Detected** (2 comments)  
   `isContextOverflow()` misses OpenAI's error format: `Input length (265330) exceeds model's maximum context length (262144)`. Causes cascading failures.  
   [Issue](https://github.com/earendil-works/pi/issues/5677)

10. **#5670 — Tab Completion Grabs First Item on Narrow** (2 comments)  
    Editor tab completion applies first suggestion instead of keeping menu open when user types to narrow ambiguous results.  
    [Issue](https://github.com/earendil-works/pi/issues/5670)

## Key PR Progress

1. **#5681 — feat: Integrate AiGameAgent** (merged)  
   New `packages/aigameagent` for HTML5/WeChat/Douyin minigame workflow with OpenAI-compatible HTTP API. 263 boss working-tree edits captured from `.claude/*`.  
   [PR](https://github.com/earendil-works/pi/pull/5681)

2. **#5674 — fix: Avoid Project Trust Prompt for Update** (merged)  
   Prevents `pi update` from triggering trust dialog when run from home folder with overlapping config directories.  
   [PR](https://github.com/earendil-works/pi/pull/5674)

3. **#5678 — feat: `excludeFromContext` for Custom Messages** (open)  
   Adds context-exclusion flag for custom messages, preserved through persistence and compaction.  
   [PR](https://github.com/earendil-works/pi/pull/5678)

4. **#5675 — fix: Stabilize Compaction After Reload** (closed)  
   Fixes `prevCompaction is not defined` errors. Preserves token boundaries and routes queued messages correctly after reload.  
   [PR](https://github.com/earendil-works/pi/pull/5675)

5. **#5679 — feat: Anthropic Vertex Provider** (closed)  
   Adds built-in provider for Claude on Google Cloud Vertex AI using ADC/ambient Google auth. Wired through model registration and UI.  
   [PR](https://github.com/earendil-works/pi/pull/5679)

6. **#5660 — fix: Prevent Uppercase Header Values Treated as Env Vars** (merged)  
   Legacy migration regex falsely rewrote `"BEARER"` → `"$BEARER"`. Fixed to avoid env var resolution of literal uppercase header values.  
   [PR](https://github.com/earendil-works/pi/pull/5660)

7. **#5666 — fix: Preserve Anthropic Refusal Details** (merged)  
   Propagates `stop_details` explanation to `errorMessage` when Anthropic returns `stop_reason: "refusal"`.  
   [PR](https://github.com/earendil-works/pi/pull/5666)

8. **#5634 — fix: Normalize Generated Model Costs** (merged)  
   Rounds OpenRouter/Vercel gateway prices to eliminate floating-point artifacts in generated cost tables.  
   [PR](https://github.com/earendil-works/pi/pull/5634)

9. **#5526 — Require Terminal Events for OpenAI Responses Streams** (open)  
   Fixes random stream stoppage and context counter corruption by enforcing terminal response events before marking stream complete.  
   [PR](https://github.com/earendil-works/pi/pull/5526)

10. **#5600 — fix: Honor Codex SSE Header Timeout Setting** (merged)  
    Hardcoded 10s SSE timeout replaced with configurable `timeoutMs`/`httpIdleTimeoutMs` for slow/unstable connections.  
    [PR](https://github.com/earendil-works/pi/pull/5600)

## Feature Request Trends
- **Provider Expansion**: Strong demand for Amazon Bedrock Mantle (OpenAI-compatible), Anthropic Vertex, and vLLM-specific DeepSeek thinking formats.
- **Context Control**: Recurring requests for `excludeFromContext` flags on custom messages and session metadata, mirroring existing bash execution behavior.
- **Model Registry Fixes**: Users consistently report mismatched context windows (GPT 5.5, Kimi K2.6) and missing thinking formats in model definitions.
- **Persona Overrides**: Growing desire for configurable system prompt personas for non-coding use cases (security, QA, research, video editing).

## Developer Pain Points
- **Stream Reliability**: OpenAI Codex `Working...` hangs (55 comments), Anthropic streams waiting for transport EOF after `message_stop`, and general lack of inactivity/deadline timeouts on streaming calls.
- **Configuration Surprises**: Uppercase header values silently rewritten as env vars, macOS `$TMPDIR` crashes, and project trust prompts appearing unexpectedly on `pi update`.
- **Compaction & Persistence**: Compaction failing after reload, broken `parentId` chains after `/fork` with labels, and duplicate provider registries due to npm shrinkwrap.
- **Tab Completion UX**: Ambiguous narrowing results in premature first-item selection, inconsistent with expected autocomplete behavior.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-13

## Today's Highlights
Qwen Code released **v0.18.0** with minor fixes, while community attention remains heavily focused on the **OAuth free tier policy adjustment (Issue #3203)** — the most commented issue in the repository history (127 comments). The daemon mode continues to mature with several PRs improving web-shell interactions, prompt queue backpressure, and background agent persistence. Multiple bug reports around tool call repetition and long-context degradation signal growing pains as users push Qwen Code into longer, more complex workflows.

---

## Releases
**v0.18.0** — Minor release containing two changes:
- chore(release): v0.17.1 ([#4742](https://github.com/QwenLM/qwen-code/pull/4742))
- fix(cli): skip thought parts in copy output ([by @he-yufeng](https://github.com/QwenLM/qwen-code/pull/4742))

> **Note:** No major feature additions in this release; likely a stabilization patch.

---

## Hot Issues (Top 10)

1. **[#3203 — Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** (127 comments, 🏆 most commented)
   - *Proposes*: Reduce daily free quota from 1,000 to 100 requests/day immediately, then close free tier entirely on June 20.
   - *Why it matters*: This is the dominant community discussion — heavy backlash expected from free-tier users who rely on daily coding workflows. The sheer comment count (127) indicates a highly controversial change.

2. **[#4514 — tracking(serve): daemon capability gaps & prioritized backlog](https://github.com/QwenLM/qwen-code/issues/4514)** (15 comments)
   - *Status*: Tracks remaining gaps in `qwen serve` HTTP/SSE surface after slash-command passthrough.
   - *Why it matters*: Daemon mode is a critical infrastructure piece for CI/CD and headless integrations. This issue is the canonical backlog for what's missing.

3. **[#4488 — qwen code插件(v0.16.0)在vscode左侧栏不显示](https://github.com/QwenLM/qwen-code/issues/4488)** (7 comments)
   - *Bug*: VSCode extension icon flashes and disappears on newer VSCode versions (1.120.0), while working on 1.95.3.
   - *Community reaction*: Multiple Chinese-speaking users reporting this UI regression; likely a VSCode API compatibility issue.

4. **[#5018 — 长程任务注意力不集中，出现大量的遗忘等](https://github.com/QwenLM/qwen-code/issues/5018)** (3 comments, opened today)
   - *Badcase*: Long-duration tasks suffer from attention loss and forgetting context.
   - *Why it matters*: Indicates model-level context management issues under extended sessions — a core quality problem for power users.

5. **[#5015 — Qwen Code executes repeated identical tool calls](https://github.com/QwenLM/qwen-code/issues/5015)** (2 comments, priority/P1)
   - *Bug*: Repeated identical tool-call streams cause execution of duplicate calls; reproducible with deterministic mock endpoints.
   - *Severity*: P1 — can waste API quotas and corrupt state.

6. **[#5019 — 长程任务下，出现大量工具重复调用情况](https://github.com/QwenLM/qwen-code/issues/5019)** (2 comments)
   - *Bug*: Under long context, the model emits identical tool calls repeatedly, hitting `Repetitive tool calls detected` API error and terminating sessions.
   - *Related*: Likely same root cause as #5015 — duplicates under long-context pressure.

7. **[#5067 — Focus-jump gates count retained terminal agents, not the panel's rendered roster](https://github.com/QwenLM/qwen-code/issues/5067)** (2 comments, opened today)
   - *Bug*: Keyboard focus navigation can target hidden LiveAgentPanel entries, creating phantom selection slots.
   - *Why it matters*: Affects multi-agent workflows where focus-jumping becomes unpredictable.

8. **[#4821 — feat(agents): support declarative agent definitions via frontmatter files](https://github.com/QwenLM/qwen-code/issues/4821)** (6 comments, CLOSED)
   - *Feature request*: Define custom agents via Markdown+YAML frontmatter (Claude Code pattern).
   - *Community reaction*: Positive — closed as implemented; the pattern is now available.

9. **[#4845 — feat: add /import-config for Claude user config migration](https://github.com/QwenLM/qwen-code/issues/4845)** (3 comments, welcome-pr)
   - *Feature request*: One-click import from Claude Code/Desktop configs (MCP servers, instructions, permissions).
   - *Why it matters*: Reduces migration friction for the many developers using both tools.

10. **[#5055 — Trojan:JS/ShaiWorm.DBA!MTB](https://github.com/QwenLM/qwen-code/issues/5055)** (2 comments, priority/P1)
    - *Security*: Antivirus flags the VSCode `.vsix` package as a Trojan.
    - *Severity*: P1 — false positive or supply chain concern. Needs immediate investigation to reassure users.

---

## Key PR Progress (Top 10)

1. **[#5066 — feat(web-shell): daemon web-shell improvements](https://github.com/QwenLM/qwen-code/pull/5066)** (OPEN)
   - *Adds*: Token usage tracking, settings panel with i18n (Chinese+English), theme/language pickers, compact mode, retry, streaming metrics, hidden commands.
   - *Why it matters*: Major UX upgrade for the daemon web shell — brings it closer to parity with the CLI TUI.

2. **[#5070 — fix(cli): ignore expired live agents in focus navigation](https://github.com/QwenLM/qwen-code/pull/5070)** (OPEN)
   - *Fixes*: [#5067](https://github.com/QwenLM/qwen-code/issues/5067) — stale terminal agents appearing in focus navigation after visibility window.
   - *Why it matters*: Clean keyboard navigation is essential for multi-agent workflows.

3. **[#5033 — fix(serve): Add prompt queue backpressure](https://github.com/QwenLM/qwen-code/pull/5033)** (OPEN)
   - *Adds*: Backpressure to the daemon prompt queue to prevent memory exhaustion under high load.
   - *Why it matters*: Critical for production deployments of `qwen serve`.

4. **[#5060 — Add TrustedRouter provider preset](https://github.com/QwenLM/qwen-code/pull/5060)** (OPEN)
   - *Adds*: Third-party provider preset for TrustedRouter.
   - *Why it matters*: Expands model provider ecosystem for enterprise users.

5. **[#5057 — fix(core): Persist file history snapshot updates](https://github.com/QwenLM/qwen-code/pull/5057)** (OPEN)
   - *Fixes*: In-memory file history snapshots lost on crash or restart.
   - *Why it matters*: `/rewind` file restoration reliability — a core undo feature.

6. **[#5062 — fix(core): keep token escalation warm across agent rounds](https://github.com/QwenLM/qwen-code/pull/5062)** (OPEN)
   - *Fixes*: `maxOutputTokens` cap resetting after tool calls, causing truncated responses.
   - *Why it matters*: Fixes [#4964](https://github.com/QwenLM/qwen-code/issues/4964) – improves long-form generation stability for agents.

7. **[#5061 — fix(core): preserve background agent launch flags](https://github.com/QwenLM/qwen-code/pull/5061)** (CLOSED)
   - *Fixes*: Background agent runtime flags (approval mode, bare mode) lost after process restart.
   - *Why it matters*: Ensures background agent behavior is consistent across daemon restarts.

8. **[#5039 — fix(cli): use id+baseUrl for precise model identity](https://github.com/QwenLM/qwen-code/pull/5039)** (OPEN)
   - *Fixes*: Ambiguous model selection when multiple providers share the same model ID.
   - *Why it matters*: Resolves a common configuration headache for multi-provider setups.

9. **[#4598 — feat(tui): collapsible thinking blocks with duration timer](https://github.com/QwenLM/qwen-code/pull/4598)** (OPEN)
   - *Adds*: Collapsible reasoning display with streaming window and duration tracking.
   - *Why it matters*: Major UI improvement — reduces visual clutter from long chain-of-thought outputs.

10. **[#5002 — refactor(serve): unify session title/displayName](https://github.com/QwenLM/qwen-code/pull/5002)** (OPEN)
    - *Refactors*: Bridge session schema — unifies `title` and `displayName` fields; persists across daemon restarts.
    - *Why it matters*: Cleaner daemon API surface, more predictable session metadata behavior.

---

## Feature Request Trends

1. **Claude Code Config Migration** — Multiple issues request import tools for Claude Code/Desktop configs (`/import-config`, #4845), MCP server definitions (#4821 declarative agents via YAML frontmatter), and workspace-level `.mcp.json` gating (#4713). **Direction**: *Qwen Code is actively closing the parity gap with Claude Code's developer experience.*

2. **Daemon/Server Mode Maturation** — Persistent demand for production-grade `qwen serve` capabilities: prompt queue backpressure (#5033), OpenTelemetry telemetry (#4554, closed), web-shell improvements (#5066), and structured session listing (#4825). **Direction**: *The daemon is transitioning from prototype to production-ready.*

3. **Dynamic Multi-Model Support** — Ongoing requests (#1206, #4813) for shared `baseUrl` configuration across models and dynamic model switching from API endpoints. **Direction**: *Users want flexible provider-agnostic model selection without per-model URL duplication.*

4. **Non-AI Context Compression** — Requests (#4264) for `/compress-fast` — context reduction without LLM calls, using deterministic trimming of tool calls/thinking blocks. **Direction**: *Power users want lightweight context management to avoid API costs and latency.*

5. **Config Auto-Reload** — PR #4933 implements file change detection via chokidar for settings files. **Direction**: *Developer experience expectation — hot-reload config without restart.*

---

## Developer Pain Points

1. **Long-Context Degradation** — Multiple reports (#5018, #5019, #5029, #4976) of quality loss, repetition, and tool call loops under extended sessions. Users describe "feeling dumber" and "attention not focused." This is the **top negative experience pattern** this week.

2. **Free Tier Limitations** — Issue #3203 (127 comments) overshadows everything. The proposed 100→0 daily quota reduction is causing significant community distress. Users are requesting usage dashboards (#3267) and clearer visibility into remaining quota.

3. **Tool Call Execution After Cancellation** — #5016: SIGINT during streaming still triggers tool execution. Combined with #5015's repeated tool calls, this creates a **safety/cost concern** — users may be billed for work they explicitly cancelled.

4. **Windows Compatibility** — #5010: `printf` command missing in Windows `cmd.exe` causes startup failures. #5055: Antivirus false-positive on `.vsix` package. Qwen Code's Windows story remains weak.

5. **VSCode UI Instability** — #4488: Extension icon disappearing on newer VSCode builds. Multiple Chinese-speaking users affected. Core UX regression that erodes trust in the IDE companion.

6. **Focus Navigation in Multi-Agent** — #5067: Keyboard focus jumps into hidden/stale agent panels. As multi-agent workflows grow, UI state management is struggling to keep pace.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI (CodeWhale) Community Digest — 2026-06-13

## Today's Highlights

The project completed a major **branding migration**: the canonical name is now **CodeWhale**; the legacy `deepseek-tui` npm package is deprecated and receives no further releases (v0.8.59). A significant wave of 15+ pull requests landed in the last 24 hours, focusing on provider-agnostic model support, sidebar UX improvements, and a new Anthropic Messages API adapter. The v0.9.0 roadmap is increasingly visible, with multiple open EPICs for a web UI scaffold, VS Code extension, and configurable keymaps.

## Releases

**v0.8.59** — *CodeWhale rename release*
- The canonical project, command, npm package, and release-asset name is now **CodeWhale**.
- Legacy npm package `deepseek-tui` is deprecated and receives no further releases.
- Users migrating from v0.8.x legacy names (`deepseek` / `deepseek-tui`) should follow `docs/REBRAND.md`.
- *(No other changelog details in release notes.)*

## Hot Issues

1. **[#2584] [CLOSED] Bug: Cannot upload local images** — `IcedOranges` reported that using `/attach` to upload a local image to a multimodal model only passes the filepath, not the base64 encoding. The model fails to see the image content. *8 comments, high signal for multimodal workflows.*

2. **[#1871] [CLOSED] QoL: Taskbar progress, animated title spinner, configurable completion sound** — Three UX enhancements that give visual and audible feedback when the user alt-tabs away. *Community enthusiastically upvoted (+1); closed as implemented in later PRs.*

3. **[#431] [OPEN] Bundled Exa web-search route** — If `EXA_API_KEY` is set, route `web_search` through Exa MCP instead of the existing DDG/Bing path. *Fallback design keeps zero-config users unaffected. Part of v0.9.0 roadmap.*

4. **[#1722] [CLOSED] Configurable auto-compact threshold with Ctrl+L** — At ~99.6% context saturation, the TUI became completely unresponsive. The root cause was two independent guardrails starving the event loop. *Fix included a new keybinding and configurable threshold.*

5. **[#2606] [CLOSED] Sidebar "Work" panel checklist status not updating** — After the model completes all checklist items, the sidebar shows stale data ("Work state updating..."). *Root cause: sidebar refresh not triggered after `checklist_write` results.*

6. **[#2787] [CLOSED] TUI status bar displays incorrect MCP count** — When both a global and project-local MCP config exist, the status bar shows a wrong tool count. *Fixed in v0.9.0-stewardship branch.*

7. **[#3018] [CLOSED] Un-hardcode DeepSeek from auto-router and subagent model selection** — Auto-model mode and per-role subagent models only worked on DeepSeek. Other providers received hardcoded `deepseek-v4-flash` (guaranteed 400 error). *Critical for multi-provider adoption.*

8. **[#2656] [CLOSED] Sub-agent session name conflicts** — Agents cannot easily diagnose and recover from session-name conflicts during orchestration. *The agent believed a name was new, but the system returned a conflict.*

9. **[#2657] [CLOSED] Agents cannot easily tell why a tool is unavailable** — Tool availability changes across modes/permission gates. *In Plan Mode, shell execution was blocked; the agent had to ask the user to switch modes.*

10. **[#471] [OPEN] EPIC: Web UI scaffold (Option A)** — SolidJS or React+Vite chat UI served from `deepseek serve --http`. *Umbrella for 10+ sub-issues; part of v0.9.0 major feature track.*

## Key PR Progress

1. **[#3045] [CLOSED] Fix: Un-hardcode DeepSeek from subagent model validation** — Non-DeepSeek providers (Moonshot, Ollama, OpenAI) can now use their own model IDs for sub-agent roles. *Directly addresses #3018.*

2. **[#3054] [CLOSED] Feat: Native Anthropic Messages API adapter** — Adds a third wire dialect with `cache_control`, `thinking` blocks, and tool streaming. Supports `codewhale --provider anthropic`. *Major expansion of provider support.*

3. **[#3035] [CLOSED] Fix: Throttle AgentProgress redraws under subagent load** — When 4+ sub-agents run concurrently, full terminal redraw on every progress event saturated the render loop. *Throttling prevents UI freeze.*

4. **[#3040] [CLOSED] Feat: Clickable sidebar rows** — Mouse-click dispatch for Tasks and Agents panels: click a job label to view it, click detail row to cancel. *Significant UX improvement for mouse users.*

5. **[#3042] [CLOSED] Feat: New CLI flags for `codewhale exec`** — Adds `--allowed-tools`, `--disallowed-tools`, `--max-turns`, `--append-system-prompt` for unattended CI/benchmark use. *Targets autonomous and testing workflows.*

6. **[#3049] [CLOSED] Feat: JSON decision contract, glob matchers, project-local hooks** — Three improvements to the hooks control plane: JSON decision output for `tool_call_before` hooks, glob pattern support, and per-project hook files. *Enables fine-grained policy control.*

7. **[#3036] [CLOSED] Fix: Hide internal IDs from normal UI** — Replaces raw UUIDs, hex agent IDs, and sentinels with stable user-facing labels. Full identifiers remain accessible in hover/detail text.

8. **[#3047] [CLOSED] Fix: Model-based lookups for Moonshot/OpenAI/Atlascloud/Ollama capabilities** — Routes provider capability reporting through generic model-based lookup instead of hardcoded values. *Enables accurate streaming/thinking detection.*

9. **[#3048] [CLOSED] Feat: Parameterize model-specific facts in prompts** — Substitutes model-specific context window, pricing, and thinking capabilities from runtime lookups instead of hardcoded V4 claims. *Makes prompts accurate for non-DeepSeek models.*

10. **[#3043] [CLOSED] Feat: Agent-task issue template and runner protocol** — Adds GitHub issue form and runner protocol so remote agents can autonomously execute milestone issues. *Infrastructure for distributed AI development.*

## Feature Request Trends

The v0.9.0 roadmap dominates feature requests, with several clear themes:

- **Multi-provider parity**: Un-hardcoding DeepSeek specifics from auto-router, subagent validation, reasoning-effort wiring, and capability detection. (#3018, #3024, #3025)
- **Web UI & IDE integration**: EPICs for a local web UI (SolidJS/React+Vite), a VS Code extension scaﬀold, and share-link mode. (#471, #481, #461) — these are the largest feature umbrella.
- **Agent lifecycle & permissions**: Subagent permission auto-derivation, external-directory permission gates, reject-with-feedback, question tool for model-to-user queries. (#414, #411, #413, #424)
- **Configurability**: Configurable keymaps (`~/.codewhale/keybinds.toml`), configurable auto-compact threshold, configurable completion sound. (#436, #1722)
- **Remote/autonomous execution**: CLI flags for CI/unattended use, agent-task issue templates, runner protocols, remote-smoke infrastructure. (#3042, #3043, #3044)

## Developer Pain Points

- **Context saturation unresponsiveness**: At ~99.6% context, the TUI event loop starves completely — no keypresses or UI updates. (#1722 — closed with throttling fix)
- **Subagent orchestration fragility**: Session-name conflicts are hard for agents to diagnose (#2656); agents cannot easily tell why a tool is unavailable across mode switches (#2657).
- **Double-invocation required for `agent_eval`**: The first call returns "deferred and now loaded"; only the second invocation succeeds with identical parameters. (#2605)
- **Multimodal image upload broken**: Local image attachments pass filepaths instead of base64, making multimodal models blind to uploaded content. (#2584)
- **Stale sidebar state**: Checklist completion status and MCP tool counts display incorrectly after async updates. (#2606, #2787)
- **Provider lock-in**: Auto-router and subagent model selection hardcoded to DeepSeek model IDs; other providers (Moonshot, OpenAI, Ollama) received invalid model names, causing 400 errors. (#3018)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*