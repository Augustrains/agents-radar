# AI CLI Tools Community Digest 2026-06-27

> Generated: 2026-06-27 01:56 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem Cross-Tool Comparison Report
**Date:** 2026-06-27

---

## 1. Ecosystem Overview

The AI CLI developer tools ecosystem is experiencing a period of rapid maturation and concurrent growing pains. Six major tools—Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI—are actively shipping releases while contending with significant reliability regressions. The dominant themes across the ecosystem include agent reliability/stability (false success reports, hangs, state desynchronization), credential and authentication persistence issues (particularly on Windows), sandbox and proxy compatibility fractures, and growing demand for sub-agent orchestration control, memory lifecycle management, and cross-platform parity. Rate-limit and token-cost surges are causing acute user frustration at OpenAI Codex, while false-positive termination signals undermine trust in autonomous agent workflows at Gemini CLI and DeepSeek TUI.

---

## 2. Activity Comparison

| Tool | Open Issues (Selected) | PRs Active (24h) | Release Status (24h) | Top-Voted Issue Score (👍) |
|------|----------------------|------------------|----------------------|---------------------------|
| **Claude Code** | 10 high-signal bugs | 2 | **v2.1.195** (shipped) | #36351: 11 |
| **OpenAI Codex** | 10 hot issues | 10 | **rust-v0.142.3, v0.143.0-a.26** | #28879: 326 |
| **Gemini CLI** | 10 hot issues | 10 | **None** | #21409: 8 |
| **GitHub Copilot CLI** | 10 hot issues | 0 (stale only) | **v1.0.66-1** (shipped) | #2082: 10 |
| **Kimi Code CLI** | 3 active | 2 | **None** (latest: v0.20.0) | #2425: 3 |
| **OpenCode** | 10 hot issues | 10 | **None** | #28846: 82 |
| **Pi** | 10 hot issues | 10 | **None** (latest: v0.80.2) | #5825: ~0 (narrow issue) |
| **Qwen Code** | 10 hot issues | 10 | **2 nightlies** (v0.19.2-n, cua-driver v0.6.8) | #4175: ~42 comments |
| **DeepSeek TUI** | 10 hot issues | 10 | **v0.8.59** (tracker closed) | #3568: 1 |

**Key observations:**
- **OpenAI Codex** dominates raw community engagement (326 upvotes on #28879, 624 comments on #14593) driven by a rate-limit crisis.
- **OpenCode** leads in community support volume (82 upvotes on price-adjustment request).
- **Qwen Code** and **DeepSeek TUI** are shipping the most code: Qwen with two nightlies + 10 active PRs, DeepSeek with a completed release tracker and 10 PRs.
- **Kimi Code CLI** shows the lowest community activity, suggesting a smaller userbase or slower development cadence.
- **Gemini CLI** and **Pi** show high PR velocity (10 each) but no releases, indicating infrastructure/refactoring work in progress.

---

## 3. Shared Feature Directions

Requirements appearing across **multiple tool communities**:

### Agent Reliability & Transparency
| Requirement | Tools Affected | Specific Needs |
|------------|----------------|----------------|
| Subagent false-success detection | Gemini CLI (#22323), DeepSeek TUI (#3568) | Agents report "GOAL" when hitting turn limits; model fails to recognize plan/agent mode switches |
| Subagent execution control | Claude Code (#69691), Copilot CLI (#1928) | Unpredictable sync/async behavior; no pause/resume mid-execution |
| Subagent transcript management | Copilot CLI (#3944) | Bloat from verbatim subagent transcripts in parent exports |

### Memory & Context Lifecycle
| Requirement | Tools Affected | Specific Needs |
|------------|----------------|----------------|
| Context/memory leakage prevention | Copilot CLI (#3945), OpenCode (#23114) | Memory cross-contamination between repositories; injected summaries polluting title generation |
| Deterministic memory redaction | Gemini CLI (#26525), OpenCode (#34006) | Secrets exposed to extraction model before redaction; inconsistent path pasting |
| Compaction control | Claude Code (#65585), OpenCode (#31152), Pi (#5676) | Compaction ignores `auto: false`; runs unconditionally |

### Cross-Platform Parity
| Requirement | Tools Affected | Specific Needs |
|------------|----------------|----------------|
| Windows credential persistence | Claude Code (#71717), OpenAI Codex (#18357) | OAuth tokens not written to disk; subscription state desync |
| macOS-specific gaps | OpenAI Codex (#27536), Copilot CLI (#3955) | Silent disk-space leaks; drag-and-drop regression |
| Linux terminal input handling | Kimi Code CLI (#2477), Pi (#6050) | Double-Enter key; TUI scroll-jumps in tmux |

### Sandbox & Network Compatibility
| Requirement | Tools Affected | Specific Needs |
|------------|----------------|----------------|
| Proxy/SSH git operations | Claude Code (#70684), Gemini CLI (#27966) | SOCKS5 auth negotiation failure; sandbox path blocklist case-sensitivity |
| MCP tool serialization | Qwen Code (#4218), Claude Code (#71717) | Connected MCP servers but tools never reach model; OAuth credential persistence |

### Model & Provider Management
| Requirement | Tools Affected | Specific Needs |
|------------|----------------|----------------|
| Rate-limit/cost transparency | OpenAI Codex (#14593, #28879), Qwen Code (#5819) | 5–20× token burn increase; silent model upgrade to expensive tier |
| Custom provider endpoints | OpenCode (#29392), Pi (#5363) | BYO-model with auto-discovery; missing provider integrations |
| Vision model fallback | Qwen Code (#5778), Pi (#6097) | Configurable vision-capable fallback; `max` thinking level support |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|------------|-------------|------------|-------------------|-----------|-----------|-----|-----------|--------------|
| **Primary User** | Pro devs, agent-intensive workflows | Enterprise teams, plugin ecosystem | Google Cloud devs, multi-model | GitHub ecosystem devs | Chinese-language devs | Open-source, crypto-friendly | Terminal power users, library embedders | Multi-platform, Chinese-first | DeepSeek model users |
| **Language Approach** | Hook-based, sub-agent pipelines | Remote plugins, turn tracking | AST-aware, subagent orchestration | Skills/chronicle system, custom agents | Plan mode, session management | Plugin async, child agents | TUI-focused, extension runtime | Daemon mode (serve), ACP streams | Terminal + Telegram bridges |
| **Platform Maturity** | macOS-focused; Windows gaps | macOS/Windows; Windows auth gaps | Linux-first; Wayland gaps | Linux/Windows; clipboard regressions | Linux-focused; terminal issues | Cross-platform; Desktop vs Terminal parity | Unix-focused; Windows path gaps | Cross-platform; Windows process leak | macOS/Windows; installation failure |
| **Unique Strength** | Sub-agent orchestration, sandboxing | Plugin architecture, event-driven monitor | Google Cloud integration, caretaker agent | GitHub ecosystem, usage-based billing | Plan mode simplicity | Crypto payments, model discovery | Embedded library, AI provider abstraction | ACP resumable streams, multiplayer agents | Moraine memory integration, Telegram bridge |
| **Key Vulnerability** | Memory context instability, Windows auth | Rate-limit crisis, SQLite corruption | Subagent false-success, CLI hangs | Keyboard regression, context leakage | Low community activity, state inconsistency | Silent failures, compaction bugs | TUI scroll-jumps, extension lifecycle | Process leaks, silent cost escalation | Mode confusion, editor crashes |

**Strategic divergence:**
- **OpenAI Codex** is betting on a **plugin/remote-execution architecture** but is undermined by a systemic rate-limit crisis that erodes user trust.
- **Gemini CLI** is investing heavily in **AST-aware tooling and automated issue triage** (Caretaker Agent), but subagent reliability remains the top community pain point.
- **Qwen Code** is building toward **daemon/serve mode productionization** with ACP resumable streams—a differentiator for long-lived agent sessions.
- **Pi** uniquely targets **library embedding use cases**, but the recent issues (#6101, #6102) show this path is architecturally immature.
- **DeepSeek TUI** focuses on **multi-platform bridge support** (Telegram, WeCom) but struggles with mode-switching confusion.

---

## 5. Community Momentum & Maturity

### High-Momentum Tools (Rapid Iteration)
- **OpenAI Codex** — 10 active PRs across core infrastructure (WebSocket auth, remote plugins, environment RPC, token refresh storms). Shipping 2 releases in 24h despite the rate-limit crisis. Community engagement is the highest in the ecosystem (624 comments on a single issue).
- **Qwen Code** — 10 active PRs + 2 nightlies. Shipping security fixes (path traversal), infrastructure (resumable ACP streams), and feature PRs (multiplayer agent, hot-reload). High velocity across security, performance, and feature work.
- **DeepSeek TUI** — 10 active PRs + release tracker closed. Strong contributor community (noaft, cyq1017, pkeging) shipping provider support, memory integration, and bridge docs.
- **Gemini CLI** — 10 active PRs, mostly infrastructure for the Caretaker Agent and recursive reasoning limits. Heavy on internal platform investment rather than user-facing features.

### Moderate-Momentum Tools
- **Claude Code** — 2 PRs and 1 release (v2.1.195). Bug-fix focused. Community frustration is building around 1M context window instability and Windows-specific issues. Release cadence appears to have slowed.
- **Copilot CLI** — 1 release (v1.0.66-1) with significant feature additions (subagent concurrency, chronicle skills review, desktop notifications), but 0 active PRs. Community reports regressions without quick fixes.
- **Pi** — 10 active PRs (mostly cleanup and provider additions), but the TUI scroll-jump family and library embedding blockers suggest technical debt accumulation.

### Low-Momentum Tools
- **Kimi Code CLI** — Only 3 active issues and 2 PRs. Low community engagement. The state inconsistency in plan mode (#2478) is a critical UX bug with little visible developer attention.
- **OpenCode** — 10 active PRs (mostly cleanup queue), but the "Thinking → No response" regression (#32149, #34087) is a critical silent failure with no fix visible. Community energy is high (82 upvotes) but developer response appears slow.

---

## 6. Trend Signals

### Industry Trends Visible in Community Feedback

1. **Agent Reliability is the #1 Cross-Tool Crisis**
   - False-positive termination reports (Gemini, DeepSeek), silent failures (OpenCode), sub-agent hang (Gemini, Claude Code), and mode-switching confusion (DeepSeek) all point to an industry-wide problem: **autonomous agents are not yet reliable enough for production use**. The community is demanding *transparency* (visible subagent trajectories) and *control* (pause/resume, forced sync execution, turn limits).

2. **Rate-Limit and Cost Transparency Crisis at OpenAI Codex**
   - The 5–20× per-token cost surge since mid-June, affecting Plus, Business, and Pro 20x plans, is the highest-signal event in this dataset. It suggests either a deliberate server-side recalibration or a bug in rate-limit accounting. The lack of official root-cause communication is amplifying community frustration. Other tools (Qwen Code #5819) suffer from similar silent cost escalation on model auto-upgrade.

3. **Windows Remains a Second-Class Platform Across the Ecosystem**
   - Every tool in this report has Windows-specific bugs: credential persistence (Claude Code, OpenAI Codex), process leaks (Qwen Code), clipboard/input handling (Kimi Code, Copilot CLI), and path normalization (Pi, OpenCode). This is a structural gap that limits enterprise adoption in Windows-dominant organizations.

4. **Plugin/Extension Ecosystem Is Fragile**
   - Copilot CLI plugins disappearing after updates, Pi extension lifecycle races (#6101, #6102), MCP tool serialization failures (Qwen Code #4218), and Claude Code hook matcher bugs all indicate that **plugin/extensions architecture across these tools is immature and undermaintained**.

5. **Memory and Context Management Is an Emerging Category**
   - Compaction control, context leakage prevention, memory lifecycle inspection, and deterministic redaction are being requested across Claude Code, Gemini CLI, Copilot CLI, OpenCode, and Pi. This is becoming a **must-have feature category** for any AI CLI tool targeting power users.

### Reference Value for Developers

- **If building autonomous multi-agent workflows**: Gemini CLI's Caretaker Agent and Qwen Code's ACP resumable streams are forward-looking, but reliability is not yet production-grade. Consider Claude Code's sub-agent API with explicit sync/async flags *if* the unpredictability bug (#69691) is fixed.
- **If deploying in enterprise/Windows environments**: Expect friction. No tool currently offers first-class Windows support. Claude Code and Qwen Code are investing most heavily in cross-platform parity but remain incomplete.
- **If optimizing for cost predictability**: OpenAI Codex's rate-limit crisis and Qwen Code's silent model upgrades are cautionary tales. OpenCode's enthusiasm for crypto payments (#23153) hints at alternative billing models gaining traction.
- **If building on the agent plugin/skills ecosystem**: The `.github/skills/` convention (Claude Code #16345) and custom agent skill scoping (Copilot CLI #3940) are converging toward a **standardized agent skills directory format**—worth watching for interoperability standards.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data snapshot:** 2026-06-27 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

The most-discussed Pull Requests reveal sharp community focus on document processing, skill creator tooling fixes, and quality-of-life improvements. Below are the 5–8 most active Skills by comment/attention volume:

| Rank | Skill / PR | Functionality | Discussion Highlights | Status |
|------|------------|---------------|----------------------|--------|
| 1 | **skill-creator fix** — [`#1298`](https://github.com/anthropics/skills/pull/1298) | Fixes `run_eval.py` 0% recall bug, Windows stream issues, trigger detection, and parallel workers. | Long-running debate about root cause (eval artifact vs. subprocess). MartinCajiao submitted detailed reproduction steps. | **Open** since 2026-06-10 |
| 2 | **document-typography** — [`#514`](https://github.com/anthropics/skills/pull/514) | Typographic quality control: orphan words, widow paragraphs, numbering misalignment in AI-generated documents. | Highly practical; users noted this addresses a universal pain point in Claude outputs. No strong objections. | **Open** since 2026-03-04 |
| 3 | **ODT skill** — [`#486`](https://github.com/anthropics/skills/pull/486) | Creates, fills, reads, and converts OpenDocument (.odt, .ods) files; includes HTML conversion. | Community welcomed LibreOffice interoperability. Some discussion about template-filling edge cases. | **Open** since 2026-03-01 |
| 4 | **skill-quality-analyzer** — [`#83`](https://github.com/anthropics/skills/pull/83) | Meta-skill: evaluates skills across Structure (20%), Security (20%), Coverage (20%), Performance (20%), Compatibility (20%). | First meta-skill in the repo; received broad interest as a quality gate for submissions. | **Open** since 2025-11-06 |
| 5 | **SAP-RPT-1-OSS predictor** — [`#181`](https://github.com/anthropics/skills/pull/181) | Integrates SAP's open-source tabular foundation model for predictive analytics on SAP business data. | Niche but high-engagement from enterprise users; discussion about model size and API requirements. | **Open** since 2025-12-28 |
| 6 | **testing-patterns** — [`#723`](https://github.com/anthropics/skills/pull/723) | Full testing stack: philosophy (Trophy model), unit testing (AAA), React Testing Library, Cypress, Playwright. | Strong approval for comprehensive coverage; minor concerns about token length. | **Open** since 2026-03-22 |
| 7 | **appdeploy** — [`#360`](https://github.com/anthropics/skills/pull/360) | Deploys and manages full-stack web apps directly from Claude via AppDeploy.ai. | Community excited about deployment-as-a-skill. Discussion focused on security boundaries. | **Open** since 2026-02-09 |
| 8 | **codebase-inventory-audit** — [`#147`](https://github.com/anthropics/skills/pull/147) | 10-step workflow: orphaned code detection, unused files, documentation gaps, infrastructure bloat. | Multiple +1s from engineering teams; some requested smaller standalone variants. | **Open** since 2025-12-16 |

---

## 2. Community Demand Trends

Analysis of the most-commented Issues reveals five clear demand clusters:

| Trend | Key Issue(s) | Signal |
|-------|--------------|--------|
| **🔐 Security & Trust Boundaries** — Skills distributed under `anthropic/` namespace risk impersonation. Community wants namespace verification and permission scoping. | [`#492`](https://github.com/anthropics/skills/issues/492) (21 comments, 👍2) | **Highest urgency:** trust boundary abuse is the #1 issue by comment volume. |
| **🏢 Enterprise & Org-Wide Sharing** — Users want shared skill libraries, not manual `.skill` file distribution. Org-level deployment is a blocker for adoption. | [`#228`](https://github.com/anthropics/skills/issues/228) (14 comments, 👍7) | **Strong demand:** 7 upvotes — the highest in any open issue. |
| **🐛 skill-creator Tooling Reliability** — `run_eval.py` returns 0% recall on every query, making the optimization loop useless. Multiple independent reproductions. | [`#556`](https://github.com/anthropics/skills/issues/556) (12 comments, 👍7), [`#1169`](https://github.com/anthropics/skills/issues/1169), [`#1061`](https://github.com/anthropics/skills/issues/1061) | **Critical bug:** blocks skill improvement workflow entirely. |
| **📄 Document & Office Format Interoperability** — ODT, enhanced PDF, DOCX tracked-changes fixes. Users want ISO-standard formats alongside Markdown. | [`#486`](https://github.com/anthropics/skills/pull/486), [`#538`](https://github.com/anthropics/skills/pull/538), [`#541`](https://github.com/anthropics/skills/pull/541) | **Consistent demand:** multiple format-specific PRs and fixes. |
| **♻️ Duplicate Skills & Plugin Hygiene** — `document-skills` and `example-skills` plugins install identical content, wasting context window. | [`#189`](https://github.com/anthropics/skills/issues/189) (6 comments, 👍9) | **High impact:** 9 upvotes — users want deduplication and plugin namespacing. |

**Emerging direction:** *Agent governance* ([`#412`](https://github.com/anthropics/skills/issues/412)) and *compact-memory* ([`#1329`](https://github.com/anthropics/skills/issues/1329)) signal early interest in safety patterns and context-efficiency for long-running agents.

---

## 3. High-Potential Pending Skills

These PRs have active comment threads and are likely to merge soon:

| PR | Skill | Why It May Land Soon |
|----|-------|----------------------|
| [`#1298`](https://github.com/anthropics/skills/pull/1298) | **skill-creator fix** (eval recall bug) | Core tooling bug affecting all skill authors. Multiple maintainers engaged. |
| [`#1323`](https://github.com/anthropics/skills/pull/1323) | **skill-creator trigger detection fix** | Direct follow-up to #1298; addresses same 0% recall root cause. Recent activity (2026-06-25). |
| [`#514`](https://github.com/anthropics/skills/pull/514) | **document-typography** | Low controversy, high practical value. No blocking objections. |
| [`#723`](https://github.com/anthropics/skills/pull/723) | **testing-patterns** | Comprehensive, well-structured. Minor token length concern is manageable. |
| [`#1099`](https://github.com/anthropics/skills/pull/1099) | **Windows subprocess pipe fix** | Multiple confirmed reproductions; clear 1-line fix approach. |
| [`#1050`](https://github.com/anthropics/skills/pull/1050) | **Windows subprocess + encoding fix** | Companion to #1099; both address `PATHEXT` and encoding issues blocking Windows users. |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliable skill-creator tooling infrastructure (particularly Windows compatibility and the 0% recall evaluation bug) — until these foundational issues are resolved, every other skill contribution is optimized against noise.**

---

# Claude Code Community Digest — 2026-06-27

## Today's Highlights

Release v2.1.195 ships with a quality-of-life improvement for fullscreen mode (disabling mouse clicks) and a critical fix for MCP hook matchers. Meanwhile, the community is amplifying a cluster of bugs around missing 1M context window options for Opus 4.8 on Max plans, and a concerning Windows kernel memory leak (now closed) that drew significant attention. A fresh wave of reports highlights persistent issues with OAuth credential persistence, sub-agent execution control, and sandbox proxy compatibility.

---

## Releases

**[v2.1.195](https://github.com/anthropics/claude-code/releases/tag/v2.1.195)**

- **New env var**: `CLAUDE_CODE_DISABLE_MOUSE_CLICKS` — disables mouse click/drag/hover in fullscreen mode while preserving scroll-wheel behavior.
- **Bug fix**: Hook matchers with hyphenated identifiers (e.g., `code-reviewer`, `mcp__brave-search`) now perform **exact matching** instead of substring matching, preventing false positives.

---

## Hot Issues

1. **[#50674 — Cowork fails on ARM64 (Snapdragon X) despite passing readiness check](https://github.com/anthropics/claude-code/issues/50674)**
   *30 comments, open since April*  
   A persistent blocker for Windows on ARM users. Cowork mode passes its own preflight checks yet fails at runtime, suggesting a deeper platform compatibility gap. No assignee or fix in sight, which is worrying for Snapdragon X adopters.

2. **[#36351 — 1M context window removed from Desktop Code tab model picker after v1.1.7714 on Max plan](https://github.com/anthropics/claude-code/issues/36351)**
   *17 comments, 👍 11*  
   Long-running complaint (since March) that the 1M context option for Opus 4.8 vanished from the model picker. Multiple duplicates filed (#68287, #69109, #69444) — community frustration is building.

3. **[#63604 — Opus 4.8 repeatedly emits malformed `tool_use` blocks, entire response discarded](https://github.com/anthropics/claude-code/issues/63604)**
   *11 comments, 👍 14*  
   A concerning model-side regression: Opus 4.8 produces broken tool call structures, forcing the entire response to be thrown away. Downgrading to 4.7 works fine. High engagement suggests this is affecting production workflows.

4. **[#45889 — Claude Desktop (Electron) causes NTFS NonPaged Pool kernel memory leak (~0.5GB/min)](https://github.com/anthropics/claude-code/issues/45889) — **CLOSED****
   *10 comments*  
   A severe Windows kernel memory leak, now closed (presumably fixed). The ~0.5 GB/min rate would crash systems rapidly. Worth verifying the fix holds in the latest release.

5. **[#71729 — `</> Code` conversation history silently lost on restart (Windows Desktop)](https://github.com/anthropics/claude-code/issues/71729)**
   *6 comments, filed today*  
   Fresh report: all conversation history in the Desktop app’s embedded Code tab disappears on restart, with no error message. Data loss bugs of this kind erode user trust quickly.

6. **[#65585 — Auto-compact stopped working for third-party API providers since v2.1.161](https://github.com/anthropics/claude-code/issues/65585)**
   *6 comments, 👍 4*  
   A recent regression affecting users who route through non-Anthropic providers. Auto-compaction is critical for staying within context limits — this is a workflow blocker for power users.

7. **[#70684 — Sandbox SOCKS5 proxy requires auth that BSD `nc` cannot negotiate, breaking SSH git operations](https://github.com/anthropics/claude-code/issues/70684)**
   *3 comments, 👍 12*  
   High upvote count for a niche but painful issue: macOS sandbox mode injects a `GIT_SSH_COMMAND` that calls BSD netcat, which can’t handle SOCKS5 authentication. Blocks all SSH git operations under sandbox.

8. **[#69691 — Sub-agent sync-vs-async is session-host-dependent with no documented way to force sync](https://github.com/anthropics/claude-code/issues/69691)**
   *4 comments*  
   A deep API design issue: the behavior of `Agent()` sub-agents (inline vs. background execution) is unpredictable and not controllable via documented flags. Makes building reliable multi-agent pipelines risky.

9. **[#71726 — Desktop app cannot inject queued messages mid-task between tool calls](https://github.com/anthropics/claude-code/issues/71726)**
   *2 comments, filed today*  
   CLI/TUI users can "steer" Claude mid-turn by typing while it works; the Desktop app’s Code window discards messages until the turn completes. A parity gap that hurts the Desktop experience.

10. **[#71717 — OAuth login succeeds but `.credentials.json` never written on Windows, causing permanent 401 loop](https://github.com/anthropics/claude-code/issues/71717)**
    *2 comments, filed today*  
    A fresh Windows-specific auth bug: OAuth flow completes successfully, but the credential file is never persisted, forcing re-authentication on every request. Critical for any MCP or API-driven workflow on Windows.

---

## Key PR Progress

*Only 2 PRs were active in the last 24 hours; this section reflects the full set.*

1. **[#71627 — docs(sandbox): note that prompt-approved hosts are session-scoped](https://github.com/anthropics/claude-code/pull/71627)**
   *Open, no comments yet*  
   Adds a documentation note clarifying that `sandbox.network.allowedDomains` approvals granted at prompt-time are lost on session restart. Small but important clarity for users building sandboxed workflows.

*PR [#71530](https://github.com/anthropics/claude-code/pull/71530) is a trivial merge from a fork and does not warrant analysis.*

---

## Feature Request Trends

- **Standardized `agents`/`skills` directory support** ([#16345](https://github.com/anthropics/claude-code/issues/16345), 👍 32): Strong demand for Claude Code to recognize the `.github/skills/` convention used by the agentskills.io ecosystem, reducing fragmentation between CLI and web-agent tooling.
- **Remote session control** ([#71731](https://github.com/anthropics/claude-code/issues/71731)): Users want the ability to enable remote access to Claude Code sessions without pre-configuring on the host machine — a common request for headless/cloud development setups.
- **Custom voice dictation vocabulary** ([#71721](https://github.com/anthropics/claude-code/issues/71721)): A new accessibility-focused request for user-defined acronyms and accent adaptation, signaling growing adoption among non-native English speakers.
- **Disable prompt suggestions** ([#66117](https://github.com/anthropics/claude-code/issues/66117)): Users of the web/app interface want to turn off inline suggestions — a UX customization request.

---

## Developer Pain Points

1. **1M context window instability on Max plans**: Multiple open issues ([#36351](https://github.com/anthropics/claude-code/issues/36351), [#68287](https://github.com/anthropics/claude-code/issues/68287), [#69109](https://github.com/anthropics/claude-code/issues/69109), [#69444](https://github.com/anthropics/claude-code/issues/69444)) report that the 1M context option for Opus 4.8 is missing from the model picker. The clustering of reports across Desktop, CLI, and third-party providers suggests a systemic issue, not an isolated UI glitch.

2. **Windows-specific auth and credential persistence**: Two new bugs today ([#71717](https://github.com/anthropics/claude-code/issues/71717), [#71675](https://github.com/anthropics/claude-code/issues/71675)) involve OAuth and MCP authentication failures on Windows — credentials not written to disk, or MCP servers prompting for auth with no UI to complete it. Windows remains a second-class platform for auth flows.

3. **Sub-agent execution unpredictability** ([#69691](https://github.com/anthropics/claude-code/issues/69691), [#71644](https://github.com/anthropics/claude-code/issues/71644)): Developers building multi-agent systems cannot reliably control whether sub-agents execute synchronously or asynchronously, and reports of sub-agents "going idle" suggest deeper runtime bugs.

4. **Sandbox proxy incompatibility** ([#70684](https://github.com/anthropics/claude-code/issues/70684)): The sandbox feature on macOS breaks SSH git operations by injecting an incompatible SOCKS5 proxy command. For a tool that markets agentic git workflows, this is a significant regression.

5. **Desktop ↔ CLI parity gaps** ([#71726](https://github.com/anthropics/claude-code/issues/71726), [#71729](https://github.com/anthropics/claude-code/issues/71729)): The Desktop app continues to lag behind the CLI in both interactive steering and conversation persistence, fragmenting the user experience across surfaces.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-06-27

## Today's Highlights
The Codex community is experiencing a major rate-limit crisis, with users on Plus and Pro plans reporting 10–20x increases in per-token cost since mid-June, draining premium budgets in as few as 2–3 prompts. Simultaneously, the team merged a foundational feature enabling remote plugins by default and is shipping substantial improvements to turn tracking, sandbox networking, and WebSocket authentication. Two maintenance releases landed today, while the most-heated bug thread (#14593) on token burning has amassed 624 comments since March.

---

## Releases
- **rust-v0.142.3** — Maintenance-only patch with no user-facing changes. [Changelog](https://github.com/openai/codex/compare/rust-v0.142.2...rust-v0.142.3)
- **rust-v0.143.0-alpha.26** — Alpha release, no detailed changelog provided.

---

## Hot Issues (10 selected)

1. **[#14593 — Burning tokens very fast](https://github.com/openai/codex/issues/14593)** — 624 comments, 274 👍. The longest-running rate-limit thread (since March). Users on Business plan report token budgets consumed far faster than expected. Community frustration is extremely high; this remains the top-voted open issue.

2. **[#28879 — Rate-limit cost per token jumped ~10–20x since June 16](https://github.com/openai/codex/issues/28879)** — 175 comments, 326 👍. The most recent and most-voted rate-limit report. Users show session logs where `limit-% consumed per token` spiked dramatically with no model or plan change. Primary suspect: server-side rate-limit recalibration.

3. **[#30224 — "This model is not supported" with X-OpenAI-Internal-Codex-Responses-Lite](https://github.com/openai/codex/issues/30224)** — 11 comments, 3 👍. Critical for custom-model users: the `Responses-Lite` header returns a blocking error for certain models, preventing use of the lightweight response mode.

4. **[#27536 — macOS: code_sign_clone grows unbounded (62 GB+)](https://github.com/openai/codex/issues/27536)** — 10 comments, closed. A silent disk-space leak on macOS where Electron auto-updates leave behind massive `code_sign_clone` directories. Resolution involved cleanup logic but no root-cause fix confirmed.

5. **[#18357 — "You're out of Codex messages" after upgrading to PRO](https://github.com/openai/codex/issues/18357)** — 9 comments, 5 👍. Subscription state desync: users who paid for higher-tier plans see the cap from their previous tier. Causes account-level frustration and support escalations.

6. **[#30212 — 5-hour allowance consumed in ~1 hour](https://github.com/openai/codex/issues/30212)** — 6 comments, 8 👍. Newer variant of the rate-limit bug, on Pro 20x plan. User reports allowance draining 5× faster than expected, reinforcing that the issue isn't isolated to Plus.

7. **[#27752 — 403 Forbidden / Cloudflare blocking CLI](https://github.com/openai/codex/issues/27752)** — 4 comments, 3 👍. WSL2 + Cloudflare IP blocks make Codex CLI unusable from certain cloud environments. No workaround documented; blocks remote development setups.

8. **[#29922 — Feature: agent-callable `monitor` tool for background events](https://github.com/openai/codex/issues/29922)** — 4 comments. High-value enhancement request: Codex currently cannot react to logs, file changes, or build failures without user prompting. Proposal adds an event-driven `monitor` capability across all surfaces.

9. **[#30305 — Image paste fails: "no image on clipboard"](https://github.com/openai/codex/issues/30305)** — 4 comments. Windows TUI bug: screenshots copied to clipboard are not recognized, breaking an essential debugging workflow. Reproduction steps are clear.

10. **[#30105 — Desktop fails to launch when another app-server holds logs_2.sqlite](https://github.com/openai/codex/issues/30105)** — 3 comments. Concurrent access to the SQLite state file blocks launch entirely, common when IDE extension and desktop app run simultaneously — particularly painful for multi-surface users.

---

## Key PR Progress (10 selected)

1. **[#30297 — Enable remote plugins by default](https://github.com/openai/codex/pull/30297)** — Promotes remote plugin support from experimental to stable. Existing `features.remote_plugin` override retained for opt-out. Major milestone for plugin architecture.

2. **[#30315 — Add generated token auth to app-server WebSockets](https://github.com/openai/codex/pull/30315)** — Generates 256-bit connection tokens with optional `--no-token-check` bypass. Improves security posture for WebSocket listeners.

3. **[#30269 — Gate Rendezvous TCP_NODELAY by signed path](https://github.com/openai/codex/pull/30269)** — Experimental latency optimization for exec-server Rendezvous using signed URLs, with harness-level TCP_NODELAY support.

4. **[#30314 — Structure and test JSON shutdown logs](https://github.com/openai/codex/pull/30314)** — Adds formal testing for `LOG_FORMAT=json` output in app-server, validating actual JSONL produced by both entry points. Improves observability reliability.

5. **[#30291 — Expose environment info RPC](https://github.com/openai/codex/pull/30291)** — Adds experimental `environment/info` RPC exposing shell/cwd metadata; surfaces connection failures as JSON-RPC errors. Enables richer environment introspection.

6. **[#30319 — Add retired model compaction repro](https://github.com/openai/codex/pull/30319)** — Integration test for model-switch compaction when the previous model slug was retired. Catches a `400` failure path that could silently break thread continuity.

7. **[#30286 — Overlap diff root discovery with world state](https://github.com/openai/codex/pull/30286)** — Performance optimization: remote diff-root discovery now runs concurrently with world-state construction, reducing cold-turn latency by avoiding serial I/O waits.

8. **[#30273 — Consume pushed exec-server process events](https://github.com/openai/codex/pull/30273)** — Moves from polling-style `process/read` to event-driven process completion with sandbox-denial state reporting. Reduces latency and improves reliability for unified-exec flows.

9. **[#30302 — Preserve namespaces on custom tool calls](https://github.com/openai/codex/pull/30302)** — Fixes namespace stripping during response deserialization and replay. Namespace-aware streaming and dispatch with regression tests.

10. **[#30201 — Fix remote-control server token refresh retry storms](https://github.com/openai/codex/pull/30201)** — Prevents cascading 502 errors from discarding still-valid tokens, stopping refresh storms that caused repeated WebSocket reconnection failures.

---

## Feature Request Trends
- **Event-driven agent reactivity**: Multiple requests for background monitoring — users want Codex to wake on file changes, build failures, or log patterns without polling.
- **Configurable provider endpoints**: `amazon-bedrock` lacks `base_url` configuration; users need proxy-compatible routing for enterprise deployments.
- **Memory management CLI**: Developers want official commands to inspect, prune, and scope accumulated memory entries, which grow to hundreds of KB in long-running sessions.
- **Sandbox networking improvements**: Requests for macOS appshot support on Intel Macs and durable Windows sandbox state files that survive updates without corruption.

---

## Developer Pain Points
1. **Rate-limit crisis** — The #1 pain point across all issue categories. Users on multiple tiers (Plus, Business, Pro 20x) report allowances draining 5–20× faster than expected since mid-June. The issue has 626+ combined comments and 600+ upvotes across the two main threads. No official root cause or resolution has been communicated.

2. **SQLite state corruption / lock contention** — Frequent failures from concurrent `logs_2.sqlite` access between IDE extension and desktop app, plus NUL-byte corruption in Windows sandbox state files. Blocks basic app startup.

3. **Cross-platform model / sandbox gaps** — Intel Mac users cannot use "Attach App Snapshot" (Computer Use service missing from x64 package); WSL-agent mode breaks Chrome control due to native-messaging host path translation errors. Fragmentation slows debugging workflows.

4. **Plugin / browser extension instability on Windows** — Bundled Chrome and Computer Use plugins disappear after Windows app updates, and browser plugins are removed on startup after a successful UI install. Recurring across multiple update cycles.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-06-27

## Today's Highlights
No new releases landed today, but the team is actively shipping infrastructure for the **Caretaker Agent** (an automated issue triage system) across three parallel PRs. On the bug front, critical fixes for **recursive reasoning loops**, **path resolution for `@`-prefixed files**, and **OAuth token exchange failures** are nearing completion. The community remains most vocal about agent reliability issues—particularly subagents reporting false success and the CLI hanging after shell commands.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

### 1. Subagent recovery after MAX_TURNS reported as GOAL success
[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — `priority/p1`
The `codebase_investigator` subagent reports `Termination Reason: "GOAL"` even when it hit its turn limit without doing any real analysis. This is a dangerous false-positive that erodes trust in autonomous workflows. 2 👍, 8 comments.

### 2. Generalist agent hangs forever
[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — `priority/p1`
The generalist agent hangs indefinitely when invoked, requiring manual cancellation after up to an hour. Users report that instructing the model not to use sub-agents resolves the issue, indicating a sub-agent orchestration bug. 8 👍, 7 comments.

### 3. Robust component-level evaluations
[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — `priority/p1`
Tracks the evolution from 76 behavioral eval tests toward a comprehensive component-level evaluation framework across 6 supported models. A foundational EPIC for quality assurance. 7 comments.

### 4. Shell command gets stuck with "Waiting input" after completion
[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — `priority/p1`
Extremely simple shell commands hang after finishing, showing "Awaiting user input." This is a high-friction issue for daily use. 3 👍, 4 comments.

### 5. AST-aware file reads, search, and mapping
[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — `priority/p2`
Investigates whether AST-aware tools can improve precision of file reads, reduce turn count from misaligned reads, and decrease token usage. 1 👍, 7 comments.

### 6. Memory system: deterministic redaction and logging reduction
[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) — `priority/p2`
Auto Memory sends secrets to the extraction model before redaction, and logs skill content. Community wants secrets redacted before any model exposure. 5 comments.

### 7. Auto Memory retrying low-signal sessions indefinitely
[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — `priority/p2`
Low-signal sessions are never marked as processed, so they get re-read on every extraction cycle, wasting tokens and time. 5 comments.

### 8. Gemini doesn't use skills and sub-agents enough
[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — `priority/p2`
Despite having custom skills with explicit descriptions ("gradle", "git"), Gemini rarely invokes them autonomously. Users must explicitly instruct the model to use them. 6 comments.

### 9. Browser subagent fails on Wayland
[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — `priority/p1`
The browser subagent terminates with `Termination Reason: GOAL` (false success) when running under Wayland display servers. 1 👍, 4 comments.

### 10. 400 error with >128 tools
[#24246](https://github.com/google-gemini/gemini-cli/issues/24246) — `priority/p2`
Gemini CLI returns a 400 error when more than 400 tools are available. Users expect smarter tool scoping rather than a hard crash. 3 comments.

---

## Key PR Progress

### 1. Egress Cloud Run Service
[#28167](https://github.com/google-gemini/gemini-cli/pull/28167) — `size/xl`
New automated caretaker service that receives verified action events via Pub/Sub and executes GitHub operations (merge, label, close). Foundation for autonomous issue triage. chadd28.

### 2. Limit recursive reasoning turns per user request
[#28164](https://github.com/google-gemini/gemini-cli/pull/28164) — `size/m`
Hard limit of 15 recursive reasoning turns per user request (configurable via `maxSessionTurns`). Protects local CPU and API credits from infinite loops. amelidev.

### 3. Fix thought leakage in scrubbed history turns
[#27971](https://github.com/google-gemini/gemini-cli/pull/27971) — `size/l`
Resolves a critical bug where the model's internal reasoning thoughts leaked into plain-text history, causing the model to mimic scratchpad patterns or enter infinite loops. amelidev.

### 4. Defensive path resolution for `@`-prefixed files
[#28053](https://github.com/google-gemini/gemini-cli/pull/28053) — `size/xl`
Fixes "File not found" errors when the model passes paths like `@policies/new-policies.txt` to `read_file`/`write_file`/`replace`. Also fixes macOS tests. luisfelipe-alt.

### 5. Case-insensitive sensitive path blocklist
[#27966](https://github.com/google-gemini/gemini-cli/pull/27966) — `size/m` (CLOSED)
Enforces case-insensitive blocklist for `.git`, `.env`, `node_modules` to prevent prompt-injection bypasses. Includes VS Code HITL integration. luisfelipe-alt.

### 6. Triage Worker core foundation (Part 1/2)
[#28163](https://github.com/google-gemini/gemini-cli/pull/28163) — `size/l`
Core modules for the caretaker's triage worker, split into two PRs for focused review. chadd28.

### 7. Webhook ingestion service for Caretaker Agent
[#28015](https://github.com/google-gemini/gemini-cli/pull/28015) — `size/xl`
Cloud Run service that ingests GitHub webhooks, verifies signatures, stores issues via Firestore, and publishes sanitized metadata to Pub/Sub. chadd28.

### 8. Trust dialog now discloses actual hooks
[#27915](https://github.com/google-gemini/gemini-cli/pull/27915) — `priority/p1`, `size/m`
Fixes the workspace-trust dialog showing the **inverse** of hooks that actually run. A project with a `SessionStart` hook previously ran shell without disclosure. magudeshhmw.

### 9. Don't let unreadable `.env` break extension loading
[#28059](https://github.com/google-gemini/gemini-cli/pull/28059) — `priority/p2`, `size/m`
Fixes extension loading failure when workspace `.env` has `EACCES` permissions (common under sandboxed environments). manumishra12.

### 10. OAuth keep-alive socket reuse fix
[#28103](https://github.com/google-gemini/gemini-cli/pull/28103) — `priority/p2`, `size/m`
Fixes "Premature close" errors during OAuth token exchange on Node.js 24.17.0, 22.23.0, and 26.3.0 due to CVE-2026-48931's socket reuse fix. ryium.

---

## Feature Request Trends

**1. Agent reliability and transparency** (most requested)
- Subagent trajectories should be visible via `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598))
- Bug reports need subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763))
- CLI should expose its own mechanics for self-guidance ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432))

**2. AST-aware code understanding**
- Request to make file reads, search, and codebase mapping AST-aware to improve precision and reduce token waste ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746))

**3. Safety and guardrails**
- "Don't use `git reset` or `--force` when safer alternatives exist" ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672))
- Destructive behavior prevention system

---

## Developer Pain Points

1. **Subagent reliability** is the #1 frustration. Subagents report "GOAL success" when they actually hit turn limits or crashed (issues [#22323](https://github.com/google-gemini/gemini-cli/issues/22323), [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)). This false-positive pattern undermines the entire autonomous workflow value proposition.

2. **CLI hangs and freezes** after command execution (issues [#25166](https://github.com/google-gemini/gemini-cli/issues/25166), [#21409](https://github.com/google-gemini/gemini-cli/issues/21409), [#22465](https://github.com/google-gemini/gemini-cli/issues/22465)). The model gets stuck at interactive prompts or "Awaiting input" states, forcing manual kills.

3. **Settings and configuration overrides ignored** by sub-agents (issues [#22267](https://github.com/google-gemini/gemini-cli/issues/22267), [#22093](https://github.com/google-gemini/gemini-cli/issues/22093)). Sub-agents run with defaults even when `settings.json` or agent mode flags say otherwise, breaking user expectations.

4. **Memory system inefficiencies** waste tokens by reprocessing low-signal sessions and exposing secrets before redaction (issues [#26516](https://github.com/google-gemini/gemini-cli/issues/26516), [#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date: 2026-06-27**

---

## Today's Highlights

A significant v1.0.66-1 release landed, introducing subagent concurrency controls for usage-based billing users, a powerful `/chronicle skills review` command for managing draft skill changes, and desktop notifications for idle sessions. The community is actively reporting several regressions in keyboard shortcuts and clipboard functionality across Linux and Windows, alongside growing concerns about context leakage between repositories and subagent transcript bloat in session exports.

---

## Releases

**v1.0.66-1** – [Release Page](github.com/github/copilot-cli/releases/tag/v1.0.66-1)

**Added:**
- **Subagent concurrency & depth limits** in `/settings` (available to usage-based billing users), giving developers granular control over parallel agent execution and recursion depth.
- **`/chronicle skills review`** command for reviewing proposed draft skill changes, with options to accept, reject, or defer each draft — streamlining the skill iteration workflow.
- **Desktop notifications** for attention prompts and idle sessions, improving awareness of long-running or paused agent operations.

---

## Hot Issues

1. **#2082 – `ctrl+shift+c` no longer copies to clipboard on Linux (Ubuntu 24.04)** – [Link](github.com/copilot-cli/issues/2082)  
   *Area: platform-linux, input-keyboard* | 👍 10 | 💬 22  
   A long-standing regression (since v1.0.4) breaking the standard terminal copy shortcut. The community notes `ctrl+c` and right-click still work for copying, but the muscle-memory disruption is frustrating. High engagement suggests this is a widespread workflow blocker.

2. **#1928 – Allow to pause copilot work** – [Link](github.com/copilot-cli/issues/1928)  
   *Area: sessions* | 👍 4 | 💬 10  
   Users want the ability to pause an active session mid-execution to inject additional context or correct direction. The current workaround (typing mid-conversation) is unreliable. This remains a top quality-of-life request.

3. **#3944 – Subagent transcripts inlined verbatim and uncapped into parent session export** – [Link](github.com/copilot-cli/issues/3944)  
   *Area: sessions, agents* | 💬 2 | ⚠️ New  
   Subagent tool-call outputs are embedded in full into parent exports with no summarization or size bound. For complex multi-agent sessions, this creates enormous, unreadable transcripts. No workaround exists.

4. **#3951 – PowerShell CLI friendliness** – [Link](github.com/copilot-cli/issues/3951)  
   *Area: platform-windows* | 💬 2 | ⚠️ New  
   Developer requests native PowerShell cmdlets instead of relying on the CLI shim, citing PowerShell's dominance in Windows automation and scripting workflows.

5. **#3947 – Theme system regression in 1.0.64** – [Link](github.com/copilot-cli/issues/3947)  
   *Area: theming-accessibility* | 👍 1 | 💬 2  
   All five theme options (`default`, `github`, `dim`, `high-contrast`, `colorblind`) unconditionally paint the alt-screen background, preventing terminal host background from showing through. Users cannot customize background transparency.

6. **#3906 – CVE assignment request** – [Link](github.com/copilot-cli/issues/3906)  
   *Area: triage* | 💬 2  
   A security researcher reports having submitted a security report via GitHub Security Advisories (GHSA) and requests CVE assignment after a code audit. No public details on the vulnerability yet.

7. **#3940 – Custom agent support for `skills` field** – [Link](github.com/copilot-cli/issues/3940)  
   *Area: agents, plugins* | 💬 2 | ⚠️ New  
   Users creating custom agents (e.g., `.github/agents/dotnet-developer.md`) want a `skills` field to limit which skills are preloaded into context, reducing noise and improving relevance for specialized agents.

8. **#3773 – Broken light theme: black background on user prompts** – [Link](github.com/copilot-cli/issues/3773)  
   *Area: theming-accessibility* | 💬 1  
   Low-contrast text rendering on light backgrounds, with black backgrounds on user prompts making text nearly unreadable. Affects selection highlight visibility too.

9. **#3945 – Memories leaking between repositories** – [Link](github.com/copilot-cli/issues/3945)  
   *Area: context-memory* | 💬 1 | ⚠️ New  
   A fresh git repository with no memory history had Copilot referencing "facts stored in memory" from unrelated repos. Suggests memory bucket isolation is broken.

10. **#3955 – Drag-and-drop file attachment broken on macOS (regression)** – [Link](github.com/copilot-cli/issues/3955)  
    *Area: triage* | ⚠️ New, critical  
    Dragging files from Finder into the Copilot app no longer attaches them to prompts. No attachment chip or file path appears — a clear regression from previous behavior.

---

## Key PR Progress

No notable pull requests were updated in the last 24 hours beyond the stale **[#570 – Add macOS installation instructions to README.md](github.com/copilot-cli/pull/570)** (last updated 2026-06-26, opened 2025-11-15). This PR remains in WIP state with no recent commits.

---

## Feature Request Trends

The community is converging on several clear feature directions:

- **Agent/Session Control**: Pause/resume sessions mid-execution (#1928), subagent concurrency limits (just shipped in v1.0.66-1), and custom agent skill scoping (#3940)
- **Context Isolation**: Better memory scoping to prevent leakage between repositories (#3945) and custom instructions contaminating repo analysis (#3946)
- **Platform Parity**: Native PowerShell support (#3951), macOS drag-and-drop restoration (#3955), and Windows clipboard verification (#3949)
- **Export/Transcript Management**: Summarization or truncation of subagent transcripts in session exports (#3944)

---

## Developer Pain Points

1. **Keyboard Shortcut Regressions** – `ctrl+shift+c` on Linux (#2082) and copy on Windows (#3949) are broken, with no official acknowledgment of fixes in recent releases.
2. **Theme/Accessibility Degradation** – Both the light theme (#3773) and the broader theme system (#3947) have regressed, with user backgrounds being overridden and low-contrast text.
3. **Context Leakage** – Multiple reports (#3945, #3946) of memory and custom instructions leaking across repositories, undermining trust in isolated project contexts.
4. **Subagent Transcript Bloat** – No built-in mechanism to cap or summarize subagent activity in parent exports (#3944), making session logs unwieldy for debugging.
5. **Proxy/Network Fetch Failures** – The `web_fetch` tool (#3948) consistently fails with `TypeError: fetch failed` on standard URLs, even when other network functionality works, suggesting a deep HTTP stack issue.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-06-27

## Today's Highlights
No new releases were published in the last 24 hours, but the community flagged two important bugs: a persistent state inconsistency in Plan mode (Issue #2478) where the system reminder claims plan mode is active while exit commands fail, and a terminal interaction issue causing double-sensing of the Enter key and loss of `/sessions` feedback on Linux (Issue #2477). A pull request (#2476) was also opened to fix a serialization issue when reasoning effort is turned off, which could silently break API compatibility for some users.

## Releases
No new releases in the last 24 hours. The latest stable version remains **0.20.0**.

## Hot Issues (3 of 3 active items)

1. **#2425 — `403` Error: Coding Agent Access Denied for Kimi CLI Users** [CLOSED]
   - Author: zhongyr | Updated: 2026-06-26 | 10 comments | 👍 3
   - **Summary:** Every message returns a `403` error, indicating the user's API token lacks permission for `kimi-for-coding` model access. This appears to be a subscription/entitlement mismatch.
   - **Why it matters:** Multiple users likely impacted; closed resolution not documented.
   - [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2425)

2. **#2478 — ExitPlanMode reports "Not in plan mode" while system reminder claims plan mode is active** [OPEN]
   - Author: proccl | Created: 2026-06-26 | 1 comment | 👍 0
   - **Summary:** The system prompt shows "Plan mode is active" and provides a plan file path, but calling `ExitPlanMode` fails with "Not in plan mode. ExitPlanMode is only available during plan mode." This creates a deadlock for the assistant.
   - **Why it matters:** Directly blocks users from exiting plan mode, effectively trapping them in a broken state. Critical UX bug.
   - [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2478)

3. **#2477 — Double Enter Key & `/sessions` Feedback Loss on Linux** [OPEN]
   - Author: iqre8 | Created: 2026-06-26 | 0 comments | 👍 0
   - **Summary:** On Ubuntu 24.04, pressing Enter once sends the input twice, and `/sessions` lists the correct sessions but entering a session ID yields no response.
   - **Why it matters:** Affects core terminal interaction; Linux users may face severe usability degradation.
   - [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/2477)

## Key PR Progress (2 of 2 active items)

1. **#2287 — docs(readme): add prerequisites list to Development section** [OPEN]
   - Author: ktwu01 | Updated: 2026-06-26 | Comments: N/A | 👍 0
   - **Summary:** Adds a `### Prerequisites` subsection to the README Development section, listing dependencies needed before `make prepare` runs.
   - **Why it matters:** Reduces friction for new contributors who have encountered missing dependency errors.
   - [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2287)

2. **#2476 — fix(kosong): omit reasoning_effort instead of sending null when thinking is off** [OPEN]
   - Author: logicwu0 | Created: 2026-06-26 | Comments: N/A | 👍 0
   - **Summary:** Fixes a bug where `thinking_effort_to_reasoning_effort("off")` maps to Python `None`, which the OpenAI SDK serializes as `"reasoning_effort": null` instead of omitting the field. This could cause API errors or unexpected behavior.
   - **Why it matters:** Prevents potential API failures when reasoning is disabled, improving stability across Azure/OpenAI endpoints.
   - [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/2476)

## Feature Request Trends
No new feature requests were observed in the last 24 hours. However, based on the broader issue history, the most frequently requested directions remain:
- **Better API entitlement/error messaging** – Users want clearer feedback when their subscription doesn't include `kimi-for-coding` (cf. #2425).
- **Improved terminal/REPL reliability** – Consistent demand for fixing input debouncing, session selection, and escape sequences.
- **Plan mode state management** – A growing need for robust session-aware state tracking to avoid mode mismatches.

## Developer Pain Points
- **State inconsistency in Plan mode** – Issue #2478 highlights a fundamental flaw: the system prompt and actual state diverge, trapping users. This is a high-severity frustration for anyone using the planning workflow.
- **Terminal input handling on Linux** – Issue #2477 (double Enter key, `/sessions` dead zone) suggests lower-level TTY handling issues that affect daily CLI usage.
- **Silent API failures from null fields** – PR #2476 addresses a subtle bug where `reasoning_effort: null` gets passed through, potentially causing cryptic errors when reasoning is off. This indicates the SDK integration layer needs more rigorous null-field handling.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-06-27

## Today's Highlights
A wave of bugfix PRs from the automated cleanup queue landed today, addressing compaction bypasses, tool-call repair, and session persistence. The community is actively debating a crypto payment feature for OpenCode Go, while two separate reports of "thinking then silent" failures on v1.16.2 worry users. A notable fork of PRs also modernizes the question/prompt UX and strips invalid Gemini schemas.

## Releases
No new releases in the last 24 hours.

---

## Hot Issues

### 1. [#28846 — Adjust Go usage limits after DeepSeek V4 Pro permanent 75% price reduction](https://github.com/anomalyco/opencode/issues/28846)
**Closed. 84 comments, 82 👍.**
Massive community support for passing DeepSeek's price cut to users. The closure suggests a resolution may already be in progress or a policy response was posted.

### 2. [#23153 — Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)
**Open. 12 comments, 23 👍.**
Persistent demand for cryptocurrency payments in OpenCode Go. Gaining traction as an alternative to traditional billing.

### 3. [#32149 — Opencode stops processing requests without response](https://github.com/anomalyco/opencode/issues/32149)
**Open. 6 comments.**
User reports the app enters a "thinking" state then goes silent. Echoed by #34087 — suggests a regression in v1.16.2 that halts output for both Go and Zen models.

### 4. [#34087 — Opencode not returning responses](https://github.com/anomalyco/opencode/issues/34087)
**Open. 3 comments.**
Same symptom as #32149, isolated to desktop app. "Input → Thinking → No response" — no plugins installed. Critical for debugging the silent-failure pattern.

### 5. [#31152 — Infinite compaction loop on every response even with empty session](https://github.com/anomalyco/opencode/issues/31152)
**Open. 4 comments.**
Every message triggers a compaction cycle. Pairs with #33128 and #32385 where compaction ignores `auto: false` and env vars. Users managing context externally are disrupted.

### 6. [#28202 — Plugin async prompts overlap with Web prompt_async](https://github.com/anomalyco/opencode/issues/28202)
**Closed. 7 comments.**
Race condition in `opencode web` produces duplicate assistant siblings under a single user message. Persisted incorrectly, breaking session integrity.

### 7. [#33618 — Qwen 3.7 Plus/Max via OpenRouter unknown/invalid tool calls](https://github.com/anomalyco/opencode/issues/33618)
**Open. 3 comments.**
Newer Qwen models emit tool calls with empty names (`✗ "" failed`), causing infinite retries. Blocks anyone using these increasingly popular models through OpenRouter.

### 8. [#23114 — Session title agent generates title from injected memory/system context](https://github.com/anomalyco/opencode/issues/23114)
**Open. 3 comments.**
Memory MCP servers inject summaries that pollute the title-generation prompt, producing irrelevant session names. Subtle but confusing for heavy memory users.

### 9. [#34006 — Pasting local file paths inconsistent between Desktop and Terminal](https://github.com/anomalyco/opencode/issues/34006)
**Open. 3 comments.**
Neither mode supports pasting a path as plain text (e.g., `C:\Users\...`). Desktop app treats it as a file attachment; Terminal lacks a plain-text paste command. Addressed by PR #34123.

### 10. [#34048 — GitHub Copilot provider lists models but every inference fails](https://github.com/anomalyco/opencode/issues/34048)
**Open. 2 comments.**
Authentication succeeds, models visible, but all requests fail with "The requested model is not supported." Breaks the entire GitHub Copilot provider flow.

---

## Key PR Progress

### 1. [#34129 — Strip required from type-less Gemini schemas](https://github.com/anomalyco/opencode/pull/34129)
Fixes Google's function-calling schema validation. When Effect Schema generates nullable unions, the required field leaks, causing API rejects. Targeted fix for Gemini provider reliability.

### 2. [#34119 — Refactor: separate out location node functionality into v2](https://github.com/anomalyco/opencode/pull/34119)
**Open.**
Core refactor extracting location-node logic from the legacy codebase into the v2 architecture. Enables cleaner session localization and future geo-aware features.

### 3. [#34127 — Add child agent session picker](https://github.com/anomalyco/opencode/pull/34127)
**Closed.**
Replaces the composer with an on-demand child agent picker. Running sessions first, arrow-key navigation, focus restoration. Improves multi-agent UX significantly.

### 4. [#33918 — Include v2 plugin skills in legacy list](https://github.com/anomalyco/opencode/pull/33918)
**Open.**
Fixes `/skills` and the instance skill API to show v2 plugin-registered skills. Previously invisible to users relying on the legacy skill interface.

### 5. [#34125 — Request refresh token scope for MCP](https://github.com/anomalyco/opencode/pull/34125)
**Open.**
Backports MCP SEP-2207 scope negotiation to the stable SDK. Prevents unnecessary `offline_access` requests and aligns with OAuth best practices for refresh tokens.

### 6. [#34116 — Question UX fixes and improvements](https://github.com/anomalyco/opencode/pull/34116)
**Open.**
Closes four tickets (#14924, #32791, #15896, #15353) with whitespace-hidden diff. A broad sweep of question-prompt UI polish.

### 7. [#29457 — Don't carry plan model into build agent on plan_exit](https://github.com/anomalyco/opencode/pull/29457)
**Closed (cleanup).**
Prevents `plan_exit` from stamping the plan model onto build-agent messages, fixing a long-standing bug (#9296) where wrong model metadata leaked between modes.

### 8. [#29446 — Bound codex stream stalls](https://github.com/anomalyco/opencode/pull/29446)
**Closed (cleanup).**
Fixes ChatGPT/Codex OAuth sessions hanging forever when upstream SSE stalls. Sets a timeout instead of indefinite wait.

### 9. [#29412 — Repair common tool-input shape failures before retry](https://github.com/anomalyco/opencode/pull/29412)
**Closed (cleanup).**
Adds a validate-then-repair layer for tool-call arguments. When LLM emits malformed JSON, the parser now fixes common shapes instead of failing outright.

### 10. [#29392 — Endpoint-based custom providers and model discovery](https://github.com/anomalyco/opencode/pull/29392)
**Closed (cleanup).**
Lets users enter an API endpoint directly for custom providers, with automatic model discovery. Greatly simplifies BYO-model workflows.

---

## Feature Request Trends

- **Crypto payments for Go subscriptions** — #23153 continues to gain upvotes, reflecting user desire for non-traditional billing.
- **Persistent model-per-chat** — #17873 (preserve model selection per chat) resurfaces as users juggle multiple models across sessions.
- **Expose coding agent marker to shell commands** — #34065 wants an environment variable so downstream CLIs know they're running inside OpenCode.
- **Clickable file paths** — #19005: plain-text file paths in terminal output should be hyperlinked for one-click opening.
- **Bring back removed desktop features** — #34100 expresses frustration with the desktop app losing functionality over recent releases.

---

## Developer Pain Points

1. **Silent "Thinking → No response" failures** — #32149 and #34087 report the same regression in v1.16.2. No error output, no logs — a top-priority bug for the team.
2. **Compaction ignores disabling** — #31152, #33128, and #32385 all describe automatic compaction running despite `auto: false` config and env vars. Compaction is a recurring stability sore spot.
3. **Model-specific tool-call failures** — #33618 (Qwen empty tool names), #34048 (GitHub Copilot inference fails), and #34126 (Kimi standalone `</think>`) show that provider compatibility is a continuous maintenance burden.
4. **Session corruption on model switch** — #31606: switching mid-session triggers a SQLite NOT NULL constraint error, ruining the session entirely.
5. **Inconsistent path pasting** — #34006: Desktop treats paths as attachments; Terminal has no plain-text paste. Basic UX friction that blocks a common workflow.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-06-27

## 1. Today's Highlights
This week's activity is dominated by a coordinated burst of TUI rendering fixes and extension lifecycle stability work. A critical bug where **streaming markdown forces scroll-to-bottom** (#5825) when `clear on shrink` is enabled has a fix-in-progress PR (#6026), while a constellation of related viewport-jump issues (#6050, #6073) in terminal multiplexers surfaced alongside. Meanwhile, the embedded library use case sees significant attention: two newly filed, well-written issues (#6101, #6102) document that `@earendil-works/pi-coding-agent` is effectively broken for multi-session library embedding due to stale extension contexts and an uninitialized theme system. The community is also actively contributing new AI provider integrations (Friendli, Amazon Bedrock Mantle) and a speculative `pi orchestrator` daemon.

## 2. Releases
No new releases were published in the last 24 hours. The latest available version appears to be **v0.80.2**, referenced in bug reports.

## 3. Hot Issues

| Issue | Title & Summary | Why It Matters |
|-------|----------------|----------------|
| [#5825](https://github.com/earendil-works/pi/issues/5825) 🔥 | **streaming markdown forces scroll to bottom** — With `clear on shrink` enabled, streamed output pulls the viewport down faster than users can read. 33 comments, 0 upvotes (likely because it's a narrow-but-annoying regression). | Affects heavy reading UX. xl0 is actively working on a fix in #6026. |
| [#4877](https://github.com/earendil-works/pi/issues/4877) | **Session folder collision** — Paths like `/a/b/c/d` and `/a-b/c-d` hash to the same session folder due to simplistic path-to-folder encoding. 19 comments, 2 👍. | A latent data integrity bug that could cause cross-path session corruption. Already has a fix PR (#5675) that was auto-closed. |
| [#5363](https://github.com/earendil-works/pi/issues/5363) | **Add amazon-bedrock-mantle provider** — Bedrock Mantle models use an OpenAI-compatible API that's incompatible with the existing Converse-based `amazon-bedrock` provider. 15 comments, 4 👍. | High-value request for AWS users; missing provider blocks a major model family. |
| [#6050](https://github.com/earendil-works/pi/issues/6050) 🆕 | **TUI full redraw clears terminal scrollback** — While Pi is processing, the terminal scrollbar jumps to the beginning of the chat. 11 comments. | A flagship UX regression for terminal-heavy workflows. Community identifies root cause is `destructive full redraw` paths. |
| [#6073](https://github.com/earendil-works/pi/issues/6073) 🆕 | **TUI viewport jumps when expanding tool output inside tmux** — `Ctrl+O` causes visible jumps inside tmux but not outside. 4 comments. | Tmux-specific variant of the scroll-jump bug family; suggests TUI renderer has multiplexer-specific fallback behavior. |
| [#5886](https://github.com/earendil-works/pi/issues/5886) 🔥 | **AgentSession settlement/continuation and assistant-tail lifecycle bugs** — Meta-issue from mitsuhiko describing a class of post-run continuation bugs. 3 comments, 2 👍. | Expert-level analysis of a deep architectural bug; touches `pkg:agent` and `pkg:coding-agent`. |
| [#6105](https://github.com/earendil-works/pi/issues/6105) 🆕 | **User messages escape incorrectly** — Typing `"\"` displays as `""`. Reproducible with `--no-extensions`. 1 comment. | Simple but annoying input-handling regression in v0.80.2. |
| [#6101](https://github.com/earendil-works/pi/issues/6101) 🆕 | **Shared extension runtime poisoned across sessions by dispose()** — Creating multiple `AgentSession`s sequentially in the same process throws "stale ctx" errors. 1 comment. | Blocks library embedding entirely for multi-session hosts. Well-documented by wloonis. |
| [#6102](https://github.com/earendil-works/pi/issues/6102) 🆕 | **Embedded library: theme Proxy throws "Theme not initialized"** — `initTheme()` is only called by the TUI, so library consumers can't use any code path touching `theme`. 1 comment. | Another library embedding blocker; pairs with #6101. |
| [#6097](https://github.com/earendil-works/pi/issues/6097) 🆕 | **Add support for 'max' thinking level** — GPT-5.6 Sol introduced a sixth `max` thinking level; Pi's model config schema doesn't include it. 0 comments. | Example request ahead of a major model release; shows Pi's prompt-config abstraction is non-extensible. |

## 4. Key PR Progress

| PR | Title & Summary | Status |
|----|----------------|--------|
| [#6026](https://github.com/earendil-works/pi/pull/6026) 🔥 | **fix(tui): stabilize working status row** — xl0's fix for the scroll-jump bug (#5825). Refactors the working status component to avoid full redraws. | OPEN — reviewed, awaiting merge |
| [#6099](https://github.com/earendil-works/pi/pull/6099) | **Rename model key from 'gpt-5.2-chat-latest' to 'gpt-5.2-chat'** — OpenAI's actual API doesn't serve a `-latest` variant. | CLOSED — merged quickly (typofix) |
| [#6064](https://github.com/earendil-works/pi/pull/6064) | **feat(experimental): pi orchestrator** — cristinaponcela adds an experimental `@earendil-works/pi-orchestrator` package exposing a local daemon over Unix sockets for lifecycle management. | CLOSED — merged as experimental |
| [#6087](https://github.com/earendil-works/pi/pull/6087) | **fix(coding-agent): remove hardcoded RPC wait timeout** — mizuikki resolves #6088 by removing implicit 60s cap in `waitForIdle()`, `collectEvents()`, `promptAndWait()`. | CLOSED — merged |
| [#6090](https://github.com/earendil-works/pi/pull/6090) | **feat(ai): add Friendli provider** — Lee-Si-Yoon adds Friendli as a built-in OpenAI-compatible provider, mirroring the Ant Ling/NVIDIA NIM pattern. | CLOSED — merged |
| [#6092](https://github.com/earendil-works/pi/pull/6092) | **draft: hosted websearch** — ahxxm adds always-on hosted search tool; the PR description explicitly says "this PR doesn't mean to be merged." | CLOSED — draft/not for merge |
| [#5676](https://github.com/earendil-works/pi/issues/5676) | **Compaction can fail after reload** — Issue documenting a fix PR (#5675) that was auto-closed by contributor gate. | CLOSED — fix exists but needs re-opening |
| [#4990](https://github.com/earendil-works/pi/issues/4990) | **Edits failing** — "Validation failed for tool 'edit': edits: must have required properties edits". Reported after a Pi update. | CLOSED — likely a schema regression |
| [#5438](https://github.com/earendil-works/pi/issues/5438) | **Clipboard image paste only submits a temp file path** — Ctrl+V in interactive mode saves to `/tmp/pi-clipboard-....png` but never sends the bytes. | CLOSED — fixed |
| [#5944](https://github.com/earendil-works/pi/issues/5944) | **Print mode hangs after completion** — The `streamTimeoutMs` fix for #5778 didn't cover post-completion non-exit. | CLOSED — no action (likely wontfix) |

## 5. Feature Request Trends

1. **New AI Provider Integrations** — Four requests in the last 48 hours alone: Amazon Bedrock Mantle (#5363), Friendli (#6091), generic payload transforms for provider overrides (#6089), and `max` thinking level support (#6097). The community is actively building against the `pi-ai` provider abstraction, but finding it insufficient for non-standard API patterns (OAuth detection, scoped keys).

2. **Embedded Library Usability** — A sharp spike in issues from a single contributor (wloonis, #6101, #6102) documenting that `@earendil-works/pi-coding-agent` is not usable as a library for multi-session or non-TUI embedding. The two issues together suggest the package was never designed for programmatic use, and the "fix" would require architectural changes to how `theme`, extension runtime, and `AgentSession` lifecycle are initialized.

3. **Extension Lifecycle & Plan Mode Robustness** — Issues #6095, #6096, #6098, #6088 reveal a pattern: extension authors are hitting hardcoded assumptions (RPC timeout, `ctx.compact()` calling conventions, missing extension references) that the core team hasn't documented well. The `plan-mode` extension in particular is causing model confusion when optional tools (`brave-search`, `questionnaire`) are missing.

## 6. Developer Pain Points

- **TUI random scroll-jumps** — The cluster of issues #5825, #6050, #6073 share a root cause: Pi's TUI renderer falls back to destructive full redraws in certain user-interface edge cases (tmux, `clear on shrink`, tool output expansion). These have been reported across multiple sessions and platforms, suggesting the TUI renderer needs a comprehensive re-audit rather than point fixes.

- **Extension ecosystem friction** — The `turn_end` + `ctx.compact()` interaction (#6096) and the `stale ctx` error after session replacement (#6101) indicate that the extension lifecycle model is undertested and underdocumented. Developers who write extensions beyond simple `turn_end` hooks are discovering race conditions and state leaks.

- **Cross-platform path bugs** — The session folder collision (#4877) and the Windows `find` path corruption bug (#6104, "first character dropped on bare drive roots") show that Pi's path normalization logic has platform-specific gaps. Windows users in particular face a disproportionately high number of path-related bugs.

- **API key/handshake fragmentation** — Issues #5871 and #6093 document that Pi's Anthropic OAuth token detection is hardcoded to `sk-ant-oat` prefix, but Claude Code scoped keys use the `sk-ant-api03-` prefix. Users must dig into internals to fix authentication. The problem is emblematic: Pi's provider abstraction hardcodes conventions that model providers are actively changing.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-06-27

## Today's Highlights
A security-focused day for the Qwen Code project, with three related path-traversal fixes (#5829, #5908, #5909) merged around source slug validation. Two nightlies dropped: `v0.19.2-nightly` with a JSON fallback fix for `web_fetch`, and `cua-driver-rs v0.6.8` bringing signed macOS binaries. A hotfix for the Powershell-leaking-powershell bug (#5873) is also shipping, and notable feature work continues on resumable ACP streams (#5852) and a multiplayer channel agent (#5888).

## Releases
- **[v0.19.2-nightly.20260627.d93bec905](https://github.com/QwenLM/qwen-code/releases/tag/v0.19.2-nightly.20260627.d93bec905)** — Fix: `web_fetch` now falls back to JSON parsing when standard response extraction fails. Code authored by @tt-a1i.
- **[cua-driver-rs v0.6.8](https://github.com/QwenLM/qwen-code/releases/tag/cua-driver-rs-v0.6.8)** — Prebuilt binaries for all platforms: macOS (codesigned + notarized universal binary + `.app`), Linux (unsigned x86_64 + arm64, glibc 2.31), Windows (unsigned x86_64 + arm64). Enables relative coordinate mode.

## Hot Issues (Top 10)

1. **[[OPEN] #4175 — Mode B feature-priority roadmap toward v0.16](https://github.com/QwenLM/qwen-code/issues/4175)** (42 comments) — A comprehensive tracking issue for `qwen serve` (daemon mode) production readiness. Covers remaining gaps in auth, workspace management, and API parity. High engagement suggests strong community interest in server-mode maturity.

2. **[[CLOSED] #4493 — Rider cannot log in to Qwen Code](https://github.com/QwenLM/qwen-code/issues/4493)** (11 comments) — Chinese-localized login loop bug on JetBrains Rider. Redirect chain never resolves when user is already authenticated via web. Status: closed, likely fixed.

3. **[[CLOSED] #5055 — Trojan:JS/ShaiWorm.DBA!MTB false positive in VSIX](https://github.com/QwenLM/qwen-code/issues/5055)** (7 comments) — Windows Defender flagged the VSIX package. Community concern around trust, though likely a false positive. Closed without further escalation visible.

4. **[[OPEN] #5083 — TUI freeze due to unreaped zombie child processes](https://github.com/QwenLM/qwen-code/issues/5083)** (6 comments) — Zombie bash processes (Z state) accumulating under the main process after child tools exit. Blocks TUI input in long sessions. Affects Linux. No fix yet.

5. **[[CLOSED] #5873 — Powershell leak: one new shell per tool call until OOM](https://github.com/QwenLM/qwen-code/issues/5873)** (5 comments) — Explosive Powershell process leak on Windows: every tool invocation spawns a new `powershell.exe` that is never closed, leading to out-of-memory crashes. High emotional response from reporter. Closed — likely fixed in nightly.

6. **[[OPEN] #4218 — MCP Server "filesystem" shows connected but tools unavailable](https://github.com/QwenLM/qwen-code/issues/4218)** (6 comments) — Model never receives tool definitions from a successfully connected MCP server on Windows. Points to a protocol serialization or capability negotiation bug.

7. **[[OPEN] #5819 — Silent model upgrade to more expensive model after update](https://github.com/QwenLM/qwen-code/issues/5819)** (4 comments) — `setting.json` model parameter auto-changed from `DeepSeek-4 flash` to `DeepSeek-4 pro` after pulling v0.19, causing unexpected token costs. User also reports Chinese→Traditional Chinese output regression.

8. **[[OPEN] #5756 — 8K default output cap truncates large write_file outputs](https://github.com/QwenLM/qwen-code/issues/5756)** (2 comments) — `CAPPED_DEFAULT_MAX_TOKENS=8000` silently caps all outputs unless `max_tokens` is explicitly set. Leads to truncated file generations and retry loops.

9. **[[OPEN] #5823 — /loop cron tasks fire silently with no model visibility](https://github.com/QwenLM/qwen-code/issues/5823)** (2 comments) — Cron tasks scheduled via `/loop` persisted across sessions with no user awareness. Model auto-started work in fresh chats. Feature request for task listing and cancellation.

10. **[[CLOSED] #5834 — Path traversal in source deletion](https://github.com/QwenLM/qwen-code/issues/5834)** (2 comments) — Crafted `sourceSlug` (e.g., `../sessions`) could escape the workspace sources directory during deletion. Fixed in #5829. Critical security fix, now merged.

## Key PR Progress (Top 10)

1. **[#5869 — Stream-highlight code blocks and fix fence-language aliases](https://github.com/QwenLM/qwen-code/pull/5869)** — Eliminates flicker during streaming code block rendering in the web shell by re-highlighting incrementally. Also normalizes fenced language identifiers.

2. **[#5911 — Normalize source slug validation errors](https://github.com/QwenLM/qwen-code/pull/5911)** — Follow-up to the security fix in #5829. Makes every path where untrusted slugs become filesystem paths return structured validation errors instead of generic exceptions.

3. **[#2652 — Replace shell-utils string parsing with tree-sitter AST](https://github.com/QwenLM/qwen-code/pull/2652)** — Long-running refactor (since March) to replace fragile string-based shell parsing with tree-sitter AST for heredocs, quoted strings, and nested conditionals. Still open after 3 months — likely large.

4. **[#5910 — Fix /acp permission votes across connections](https://github.com/QwenLM/qwen-code/pull/5910)** — Stacks on #5852's resumable-stream plumbing. Fixes permission vote state not being shared across multiple SSE connections to the same session.

5. **[#5890 — Inject .qwen/loop.md task file at fire time](https://github.com/QwenLM/qwen-code/pull/5890)** — Enables durable, user-editable task lists for `/loop` via sentinel prompts. Addresses the "silent cron" problem from #5823.

6. **[#5852 — Resumable /acp session stream with Last-Event-ID](https://github.com/QwenLM/qwen-code/pull/5852)** — Wires SSE `id:` lines into the daemon's event-replay engine so reconnecting ACP clients can resume where they left off. Foundation for reliable long-lived agent sessions.

7. **[#5847 — Per-turn runtime context injection via system-reminder blocks](https://github.com/QwenLM/qwen-code/pull/5847)** — External callers can inject session-scoped key-value pairs that become `<system-reminder>` blocks on every turn. Useful for passing file paths, credentials, or dynamic instructions without modifying the system prompt.

8. **[#5888 — RFC + Phase 0: qwen tag multiplayer channel agent](https://github.com/QwenLM/qwen-code/pull/5888)** — Introduces a channel-resident agent that lives in DingTalk groups, built on the existing channel adapters and daemon. Phase 0 includes basic presence and message relay.

9. **[#5778 — Add /model --vision for fallback vision model](https://github.com/QwenLM/qwen-code/pull/5778)** — Mirrors the existing `/model --fast` UX: users can configure a vision-capable fallback model used when the main model receives an image. Interactive picker when called without arguments.

10. **[#5829 — Reject unsafe source slugs before deletion](https://github.com/QwenLM/qwen-code/pull/5829)** — Merged security fix that blocked path traversal in desktop source deletion by adding slug validation before resolving delete targets. Closed CVE-22 vector.

## Feature Request Trends

- **Mode B / Serve productionization** (#4175, #5677) — The largest ongoing feature thread. Community is pushing for `qwen serve` (daemon mode) to reach v0.16 production-readiness, covering ACP parity, permissions, LSP over ACP, and GitHub integration.
- **Hot-reload for skills, MCP, and config** (#3696) — High priority feature request for live reloading without session restart. Partially implemented; remaining work includes extension hot-reload and config validation on change.
- **Plan Approval Gate expansion** (#5881) — Community wants the Plan Approval Gate (a draft/review model that checks plan quality before execution) to fire on all plan-mode entries, not just model-initiated ones.
- **Multiplayer agents** (#5888, #5907) — Two related threads: a DingTalk agent (qwen tag) and Telegram bot command completion. Both aim to extend Qwen Code's presence into chat platforms as first-class agents.
- **Virtualized terminal history by default** (#5738) — Making in-app scrollable history the default for CLI users, with an opt-out for host-terminal purists.

## Developer Pain Points

- **Process leaks on Windows** (#5873, #5083) — Two distinct leaks: Powershell processes per tool call (closed, but serious) and zombie bash children causing TUI freezes on Linux. Both point to weak child-process lifecycle management.
- **Silent model/cost escalation** (#5819) — Auto-upgrading to more expensive models and silently persisting cron tasks (#5823) erodes user trust. Recurring theme: autoupdates with no audit trail.
- **Output truncation without warning** (#5756) — The 8K default `max_tokens` cap silently truncates large outputs, causing retry loops that waste tokens and time. Suggests the cap should either be documented, user-configurable, or surfaced as a warning.
- **MCP tool serialization issues** (#4218) — Connected MCP servers whose tools never reach the model. Likely a provider-negotiation or capability-forwarding bug in the session management layer.
- **False positive antivirus alerts** (#5055) — Windows Defender flagging the VSIX package as a trojan creates an immediate trust barrier. Community expects code signing or publisher verification to resolve this.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-06-27

## Today's Highlights
The v0.8.59 release tracker (#3063) was closed today, shipping the long-awaited TUI mouse-report input leak fix for macOS alongside runtime safety improvements. Community contributor **noaft** landed OpenModel provider support (#3585, harvested as #3677), while a new Editor Freeze bug (#3657) was reported, crashing the entire application on editor launch.

## Releases
No new versions were cut in the last 24 hours. The v0.8.59 release tracker (#3063) was finalized; a formal release tag is expected shortly.

## Hot Issues

1. **[#3063 — v0.8.59: release tracker](https://github.com/Hmbown/CodeWhale/issues/3063)** [CLOSED]
   The stabilization release for the v0.8.58 train. Fixes a macOS TUI mouse-report input leak and addresses the current issue/PR queue. 11 comments, community sign-off complete.

2. **[#3657 — Editor Freezes and Crashes Codewhale](https://github.com/Hmbown/CodeWhale/issues/3657)** [OPEN]
   Typing `d` and pressing `Ctrl-O` to open the editor causes the entire application to freeze, requiring a process kill. 3 comments, no workaround identified yet.

3. **[#3568 — Plan and agent mode mixed up](https://github.com/Hmbown/CodeWhale/issues/3568)** [OPEN]
   Persistent regression where the AI fails to recognize `plan`/`agent` mode switches. The model attempts file modifications using agent methods while in plan mode. 5 comments, 1 👍, uploaded chat export provided.

4. **[#1186 — Typed persistent permission rules](https://github.com/Hmbown/CodeWhale/issues/1186)** [OPEN]
   Long-running enhancement to add `allow`/`deny`/`ask` permission rules scoped by tool name, command prefix, and workspace path. 10 comments, targets v0.9.0.

5. **[#861 — Thinking collapse root causes](https://github.com/Hmbown/CodeWhale/issues/861)** [CLOSED]
   Four root causes of reasoning block freezing, silent truncation, and drop issues — all critical for DeepSeek-family API compatibility. 8 comments, fixed via #3016.

6. **[#3582 — install.sh returns HTML](https://github.com/Hmbown/CodeWhale/issues/3582)** [CLOSED]
   The recommended `curl -fsSL https://codewhale.net/install.sh | sh` command fails because the endpoint returns a Next.js HTML page instead of a shell script. 4 comments, resolved.

7. **[#3537 — Replace hard-coded localization with i18n library](https://github.com/Hmbown/CodeWhale/issues/3537)** [CLOSED]
   Proposal to replace the 5,000+ line `localization.rs` with a dedicated i18n library for better maintainability and compilation speed. 3 comments.

8. **[#3490 — v0.8.71: Legacy follow-up and dead-code inventory](https://github.com/Hmbown/CodeWhale/issues/3490)** [OPEN]
   Systematic cleanup of `allow(dead_code)` markers and stale "follow-up" comments before v0.9 expansion. 4 comments.

9. **[#2870 — Staged command-boundary refactor](https://github.com/Hmbown/CodeWhale/issues/2870)** [OPEN]
   EPIC splitting the command-boundary refactor into mergeable layers. 7 comments, refs #2791 and #2851.

10. **[#3638 — Exposed main prompt for broader use cases](https://github.com/Hmbown/CodeWhale/issues/3638)** [OPEN]
    Feature request to make the default prompt configurable for non-software-engineering use cases like creative writing. 1 comment.

## Key PR Progress

1. **[#3585 / #3677 — OpenModel provider support](https://github.com/Hmbown/CodeWhale/pull/3585)**
   Community PR by **noaft** adding OpenModel as a first-class Anthropic Messages provider; harvested and polished by **Hmbown**. Routes through `deepseek-v4-flash` by default.

2. **[#3575 — Wire moraine-mcp as recall tool source](https://github.com/Hmbown/CodeWhale/pull/3575)**
   **pkeging** integrates Moraine memory recall tools (searchsessions, open, list_sessions) as an MCP source, with a fallback config gate.

3. **[#3665 — Debounce Telegram turn sequence writes](https://github.com/Hmbown/CodeWhale/pull/3665)**
   By **cyq1017**; part of #2967 Telegram bridge hardening. Debounces `lastSeq` writes and ensures a final flush on stream exit.

4. **[#3584 — Audit/memory verify gates](https://github.com/Hmbown/CodeWhale/pull/3584)**
   **pkeging** adds verification gates for the Moraine/memory integration.

5. **[#3607 — Reactivate stale issue cleanup](https://github.com/Hmbown/CodeWhale/pull/3607)**
   **Hmbown** recreates missing stale-policy labels and configures `bug+needs-info` issues to age out unless blocked by release/security/pinned labels.

6. **[#3674 — Extract auth helpers](https://github.com/Hmbown/CodeWhale/pull/3674)**
   **cyq1017** refactors runtime API auth/token/cookie helpers into `runtime_api/auth.rs`, keeping the main file focused on routing.

7. **[#3668/#3675 — rusqlite dependency bump](https://github.com/Hmbown/CodeWhale/pull/3668)**
   Dependabot proposed bump from 0.32.1 to 0.40.1; **Hmbown** landed a safer 0.39.0 bump that passes local stable validation.

8. **[#3670/#3672/#3673 — Dependency bumps](https://github.com/Hmbown/CodeWhale/pull/3670)**
   Updates for `toml_edit`, `sha2`, `rustls`, and `axum`, with a companion fix for `sha2` 0.11 digest hex formatting.

9. **[#3640/#3678 — WeCom Bridge deployment guide](https://github.com/Hmbown/CodeWhale/pull/3640)**
   **pkeging** contributed initial WeCom Bridge docs; **Hmbown** harvested the useful content and fixed accuracy blockers.

10. **[#3621/#3676 — Fix provider links docs fallback](https://github.com/Hmbown/CodeWhale/pull/3621)**
    **noaft** updated the stale fallback URL; harvested by **Hmbown** with Qianfan-specific link and regression coverage.

## Feature Request Trends

The most commonly requested features this week center on **runtime customization** and **AI behavior control**. Multiple issues ask for configurable prompts for non-engineering use cases (#3638), typed persistent permission rules (#1186), and a unified setup wizard for tools/MCP/skills/plugins (#3407). The **memory integration** trend continues with Moraine MCP tooling (#3575). Localization maintainability (#3537) and prompt token optimization (#2953, #2956, #2957) remain active discussion topics.

## Developer Pain Points

The highest-pain recurring issues are: **mode switching confusion** (plan/agent mixed up despite previous fixes, #3568), **editor crashes** on launch (#3657), **thinking block instability** affecting all reasoning models (#861, now fixed in v0.8.59), **installation failures** from the HTML endpoint (#3582), and **IME composition conflicts** with CJK input (#2612, closed). The 45-second SSE multi-agent timeout on Windows (#1679) and the non-streaming `app-server --stdio` thread (#1490) continue to surface as integration blockers.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*