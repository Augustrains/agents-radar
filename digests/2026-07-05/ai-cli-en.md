# AI CLI Tools Community Digest 2026-07-05

> Generated: 2026-07-05 01:46 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools Ecosystem
**Date**: 2026-07-05

---

## 1. Ecosystem Overview

The AI CLI tools landscape on 2026-07-05 reveals a maturing but fractured ecosystem, where all major tools are grappling with a shared set of infrastructure challenges—rate-limit instability, context compaction regressions, session state corruption, and safety classifier false positives—while diverging sharply in architectural priorities. Claude Code and OpenAI Codex remain the most community-active projects, driven by user frustration over billing and reliability issues; Gemini CLI and OpenCode are investing heavily in agent reliability and daemon architecture respectively; while smaller tools like Pi and DeepSeek TUI focus on foundational UX and localization improvements. The emergence of common pain points across all tools—session management fragility, silent failures, and platform-specific breakage—suggests the ecosystem is transitioning from feature velocity to reliability engineering as the primary differentiator.

---

## 2. Activity Comparison

| Tool | Hot Issues (24h) | Issue Activity Score | PRs (24h) | Release Status | Community Energy |
|------|------------------|---------------------|-----------|----------------|------------------|
| **Claude Code** | 10 active (1 with 793 comments) | ★★★★★ (8,600+ total reactions) | 0 | No release | 🔥🔥🔥🔥🔥 Highest |
| **OpenAI Codex** | 10 active (2 with 500+ reactions) | ★★★★★ (980+ total reactions) | 10 open | Rust alpha out | 🔥🔥🔥🔥🔥 Highest |
| **Gemini CLI** | 10 active | ★★★★☆ (20+ total reactions) | 10 active | Nightly build | 🔥🔥🔥🔥 High |
| **GitHub Copilot CLI** | 10 new issues | ★★☆☆☆ (12+ total reactions) | 1 (placeholder) | v1.0.69-1 released | 🔥🔥 Moderate |
| **OpenCode** | 10 active | ★★★★★ (130+ total reactions) | 10 active | No release (v1.17.13 latest) | 🔥🔥🔥🔥 High |
| **Qwen Code** | 10 notable | ★★★☆☆ (10+ total reactions) | 10 active | Nightly build | 🔥🔥🔥 Moderate-High |
| **Pi** | 10 hot (22+ closed) | ★★★☆☆ (17+ total reactions) | 8 active | No release (v0.80.3 latest) | 🔥🔥🔥 Moderate |
| **DeepSeek TUI** | 8 open bugs | ★★☆☆☆ (0 reactions) | 5 active | No release | 🔥🔥 Low-Moderate |
| **Kimi Code CLI** | 1 issue closed | ★☆☆☆☆ (0 reactions) | 0 | No release | 🔻 Lowest |

**Key observations**: Claude Code's single issue #38335 (793 comments) dominates community attention. OpenAI Codex has the most cross-cutting PR activity (10 open). Gemini CLI and OpenCode maintain steady development velocity. Copilot CLI and Kimi Code CLI show minimal activity today.

---

## 3. Shared Feature Directions

### A. Session Resilience & State Management (5 tools)
- **Need**: Auto-resume paused tasks, persistent session state, hot-reloadable configs without restart
- **Tools affected**: Claude Code (#24057 – hot-reload MCP/hooks), OpenAI Codex (#21073 – auto-resume), Qwen Code (#6318 – `/rewind` after `/compress`), Gemini CLI (#26522 – memory retry loops), OpenCode (#15533 – compaction loops)
- **Common pattern**: Users across all tools report losing context, state corruption, and needing manual session recovery

### B. Multi-Account & Identity Management (4 tools)
- **Need**: Support multiple cloud/enterprise accounts from a single CLI instance
- **Tools affected**: Claude Code (#27302 – 296👍, top feature request), OpenAI Codex (#15975 – multi-account), GitHub Copilot CLI (#3241 – self-hosted agents), Gemini CLI (implicit from config management issues)

### C. MCP/Tool Configuration & Lifecycle (4 tools)
- **Need**: Live toggling, hot-reload, deferred loading optimization, tool registry consistency
- **Tools affected**: Claude Code (#24057), GitHub Copilot CLI (v1.0.69-1 enables mid-turn `/mcp list`), DeepSeek TUI (#4027 – `always_load` field), OpenCode (#8625 – auto-defer tool descriptions)

### D. Safety Classifier False Positives (3 tools)
- **Need**: Configurable override thresholds, model fallback control
- **Tools affected**: Claude Code (#73784 – Fable 5 blocking T&S work), OpenAI Codex (#30325 – safety buffering metadata), Pi (#6278 – LLM tool-call hallucination)
- **Insight**: Safety classifiers are overly aggressive, blocking legitimate workflows and forcing model downgrades

### E. Context Window Management (3 tools)
- **Need**: Accurate context accounting, configurable limits, compaction that works
- **Tools affected**: Claude Code (#74273 – Sonnet 5 compaction plateau), Qwen Code (#6144 – context window miscalculation), Pi (#6206 – clamping prevents intentional reduced limits)

### F. Platform Parity (3 tools)
- **Need**: Windows and Linux Wayland fixes, consistent behavior across OS
- **Tools affected**: OpenAI Codex (#31035 – Windows BSODs, #15975 – VSCode crash), Gemini CLI (#21983 – Wayland browser agent), Qwen Code (#6298 – shell tool fails on Windows), Copilot CLI (#4026 – Windows crash)

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | GitHub Copilot CLI | OpenCode | Qwen Code | Pi | DeepSeek TUI | Kimi Code CLI |
|-----------|-------------|--------------|------------|-------------------|----------|-----------|-----|--------------|---------------|
| **Primary target** | Enterprise full-stack | Cloud-native developers | Google ecosystem | GitHub ecosystem | FOSS generalist | Chinese-market devs | Embedded/SDK devs | Terminal power users | Multi-provider CLI |
| **Key strength** | MCP/plugin ecosystem | Multi-agent orchestration | Google 3 model affinity | GitHub integration | Protocol-first design | Local model support | Extensibility (SDK) | Lightweight TUI | Provider abstraction |
| **Biggest pain** | Session billing | Rate-limit cost | Agent reliability | Windows stability | Compaction loops | CI bot overreach | Tool-call hallucination | Localization flakiness | Config inconsistency |
| **Architecture** | Cloud-heavy | Cloud + local (Rust alpha) | Cloud-native | Cloud + local | Daemon + Web UI | Daemon + local SDK | Pure CLI + SDK | Pure CLI TUI | Provider-agnostic CLI |
| **Community style** | Vocal, high-volume | Data-driven, PR-heavy | Engineering-focused | Enterprise-quiet | Protocol debates | Chinese-language | Rapid triage | Low participation | Minimal engagement |
| **Release cadence** | Slow (no 24h release) | Frequent (Rust alpha) | Nightly | Minor releases | Slow (stable held) | Nightly | None today | None today | None today |

**Key differentiators**:
- **Claude Code** has the largest community gravity but the slowest fix velocity for critical bugs
- **OpenAI Codex** leads in PR velocity and architectural innovation (Rust alpha, multi-agent)
- **Gemini CLI** focuses on agent reliability but still lacks resolution on 3 P1 bugs
- **OpenCode** is the most protocol-aware, with the most technical depth in compaction/event bus fixes
- **Pi** has the fastest issue-to-fix cycle (22+ closed same-day) but smallest community
- **Kimi Code CLI** has virtually no community momentum today

---

## 5. Community Momentum & Maturity

| Tool | Community Growth Signal | Maturity Indicators |
|------|------------------------|---------------------|
| **Claude Code** | 🟢 **Highest**: 467👍 on single issue, 793 comments, sustained 3-month outrage | Mature ecosystem but trust erosion from unresolved billing bugs |
| **OpenAI Codex** | 🟢 **High**: 421👍 on SQLite bug, 346👍 on rate-limit, 10 active PRs | Maturing with Rust rewrite; reliability gaps drive community scrutiny |
| **Gemini CLI** | 🟡 **Moderate**: 8👍 on generalist hangs, 10 active PRs | Resolving architectural issues; agent reliability still alpha-quality |
| **GitHub Copilot CLI** | 🔴 **Low**: 12👍 top issue, 1 PR (placeholder) | Mature product but community engagement is minimal |
| **OpenCode** | 🟢 **High**: 75👍 on MCP context feature, 10 active PRs | Strong technical discussions; protocol innovation; fast PR cycle |
| **Qwen Code** | 🟡 **Moderate**: 10 active PRs, tracking issues for daemon | Chinese-market focused; CI maturation; documentation drift |
| **Pi** | 🟢 **High per-user**: 22+ issues closed in 24h, rapid triage | Extremely responsive maintainers; smaller but engaged community |
| **DeepSeek TUI** | 🔴 **Low**: 0 reactions across issues, 5 PRs | Early-stage; low signal-to-noise; localization-focused |
| **Kimi Code CLI** | 🔴 **Minimal**: 1 issue, 0 PRs, 0 reactions | Stalled or very low engagement today |

**Rapid iteration leaders**: OpenAI Codex, Gemini CLI, OpenCode, Pi
**Community gravity leaders**: Claude Code, OpenAI Codex

---

## 6. Trend Signals

### Emerging Industry Patterns

**1. From Feature Velocity to Reliability Engineering**
Every major tool has multiple unresolved reliability issues—connection drops, compaction loops, rate-limit misattribution, silent failures. The community is signaling that trust, not new features, is the primary barrier to adoption.

**2. Session Management is the New Frontier**
The convergence of complains about state loss, auto-resume, persistent memory, and compaction suggests that "session as a durable, restartable unit" is an unresolved foundational problem across all tools. Tools that solve this well (OpenCode's compaction barrier, Qwen Code's daemon artifacts) may gain structural advantage.

**3. Safety Classifier Tension**
Fable 5 (Claude Code) and similar safety layers (OpenAI Codex, Pi) are creating false-positive burdens that break legitimate workflows. The community is demanding configurable, user-controlled safety thresholds—a sign that one-size-fits-all safety is unsustainable for developer tools.

**4. Multi-Provider Aggregation Demand**
Kimi Code CLI's singular issue (configuration inconsistency across providers) and Pi's strict-tooling RFC reflect a growing expectation that CLI tools should work uniformly regardless of backend LLM. "Provider-agnostic reliability" is becoming a baseline requirement.

**5. Windows as Second-Class Citizen**
Every tool with platform-specific bugs (OpenAI Codex BSODs, Qwen Code shell tool, Copilot CLI crashes, Gemini CLI Wayland, Pi TUI input handling) has Windows gaps. The ecosystem is macOS-first by default.

**6. Agent Governance & Destructive Action Prevention**
OpenCode's `rm -rf .` incident (#35339) and DeepSeek TUI's constitution-adherence bug (#4032) highlight urgent demand for guardrails around autonomous agent actions. Expect sandboxing and confirmation flows to become table-stakes features.

### Reference for Developers

- **If you prioritize reliability**: Monitor OpenAI Codex's Rust migration and OpenCode's compaction barrier PR—these are signal fixes for systemic issues
- **If you need Windows support**: Every tool has gaps; Gemini CLI and Qwen Code are actively fixing, but none are production-ready on Windows today
- **If you use MCP/plugin ecosystems**: Claude Code and OpenCode have the most advanced MCP hooks, but both suffer from tool lifecycle management gaps
- **If cost control is critical**: The rate-limit and session-billing issues at Claude Code and OpenAI Codex suggest users should audit actual vs. advertised costs carefully until resolved
- **If you want a stable experience**: Pi and DeepSeek TUI have the smallest surface area and fastest fix cycles, but limited feature sets

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-05 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

### #1 — Skill Creator Fixes (PR #1298, #1099, #1050, #1323) | *Open*
**Functionality:** A cluster of interrelated fixes for the `skill-creator` meta-skill's evaluation pipeline (`run_eval.py`, `run_loop.py`). The core problem is that `run_eval.py` reports **recall=0%** for every skill description, making the description-optimization loop optimize against noise. Root causes include: Windows subprocess pipe reading failures (`[WinError 10038]`), missing `PATHEXT` handling for `claude.cmd`, incorrect trigger detection logic that bails on non-Skill tools, and failure to install eval artifacts as real skills.
**Discussion Highlights:** 10+ independent reproductions of the 0% recall bug (#556). The community has submitted multiple overlapping fixes; PR #1298 is the most comprehensive, also addressing parallel workers and stream reading on Windows.
**Status:** Open | [PR #1298](https://github.com/anthropics/skills/pull/1298) | [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1050](https://github.com/anthropics/skills/pull/1050) | [Issue #556](https://github.com/anthropics/skills/issues/556)

### #2 — Document Typography Skill (PR #514) | *Open*
**Functionality:** A skill that enforces typographic quality control on AI-generated documents — preventing orphan word wrap, widow paragraphs, and numbering misalignment. These are pervasive issues in Claude-generated documents that users rarely request but consistently degrade output quality.
**Discussion Highlights:** Recognized as addressing a universal pain point. The skill's value proposition is that it catches problems users don't know to ask about.
**Status:** Open | [PR #514](https://github.com/anthropics/skills/pull/514)

### #3 — DOCX Tracked Change ID Collision Fix (PR #541) | *Open*
**Functionality:** Fixes document corruption when the DOCX skill adds tracked changes to documents with existing bookmarks. The root cause is that `w:id` in OOXML is a shared ID space across bookmarks, tracked changes, comments, and move ranges — the skill's examples used hardcoded low IDs that collide.
**Discussion Highlights:** A subtle OOXML specification issue that causes silent document corruption. The fix requires generating unique IDs dynamically.
**Status:** Open | [PR #541](https://github.com/anthropics/skills/pull/541)

### #4 — YAML Special Character Detection (PR #539, #361) | *Open*
**Functionality:** Adds pre-parse validation in `quick_validate.py` to detect unquoted `description` fields containing YAML special characters (`:`, `#`, `{`, `}`, `[`, `]`). These cause `yaml.safe_load()` to silently misparse values — e.g., `description: Use when: ...` becomes a dict instead of a string.
**Discussion Highlights:** A common footgun for skill authors. The community submitted two parallel PRs with similar approaches; discussion centers on which edge cases to cover.
**Status:** Open | [PR #539](https://github.com/anthropics/skills/pull/539) | [PR #361](https://github.com/anthropics/skills/pull/361)

### #5 — Self-Audit Skill (PR #1367) | *Open*
**Functionality:** A universal output auditing skill that performs mechanical file verification (confirming every claimed output file exists) followed by a four-dimension reasoning quality audit in damage-severity priority order. Works with any project, tech stack, or model.
**Discussion Highlights:** Novel approach to quality gating — separates mechanical verification from reasoning quality assessment. High interest as a general-purpose safety net.
**Status:** Open | [PR #1367](https://github.com/anthropics/skills/pull/1367)

### #6 — Testing Patterns Skill (PR #723) | *Open*
**Functionality:** A comprehensive testing skill covering the full stack: testing philosophy (Testing Trophy model), unit testing (AAA pattern, pure functions), React component testing (Testing Library), integration testing, and E2E testing. Includes guidance on what *not* to test.
**Discussion Highlights:** Addresses a clear gap — the skills collection had no dedicated testing guidance. The community values its opinionated structure.
**Status:** Open | [PR #723](https://github.com/anthropics/skills/pull/723)

---

## 2. Community Demand Trends

From the most-discussed Issues:

1. **Windows Compatibility (Highest Demand)** — Issues #1061, #556, and #1169 document that `skill-creator` scripts are fundamentally broken on Windows due to Unix-first assumptions: subprocess `PATHEXT` handling, `cp1252` encoding, and `select()` on pipes. **This is the #1 blocker** for Windows users contributing skills.

2. **Trust & Security Boundaries** — Issue #492 (34 comments) raises that community skills distributed under the `anthropic/` namespace create a trust boundary vulnerability — users may grant elevated permissions to community skills they believe are official. This is the most-commented issue and reflects growing security consciousness.

3. **Org-Wide Skill Sharing** — Issue #228 requests direct organizational skill sharing (shared libraries, sharing links) instead of manual `.skill` file downloads and uploads via Slack/Teams. 7 upvotes indicate strong enterprise demand.

4. **Skill Ecosystem Stability** — Issues #189 (duplicate skills from overlapping plugins) and #62 (skill disappearance on file rename) show that the community needs better lifecycle management and deduplication.

5. **New Skill Directions Requested:** The most-anticipated new areas are:
   - **Agent Governance** (#412) — safety patterns, policy enforcement, trust scoring
   - **Compact Memory** (#1329) — symbolic notation for efficient agent state management
   - **SharePoint/Enterprise Document Handling** (#1175) — with security considerations

---

## 3. High-Potential Pending Skills

These PRs have active discussion and are likely to land soon:

| PR | Skill | Author | Status |
|----|-------|--------|--------|
| [#1367](https://github.com/anthropics/skills/pull/1367) | Self-Audit (mechanical + reasoning quality gate) | YuhaoLin2005 | Open, updated Jul 2 |
| [#1302](https://github.com/anthropics/skills/pull/1302) | Color Expert (color naming systems, spaces, palettes) | meodai | Open, updated Jun 12 |
| [#806](https://github.com/anthropics/skills/pull/806) | Sensory Skill (macOS AppleScript automation) | AdelElo13 | Open, updated Apr 2 |
| [#723](https://github.com/anthropics/skills/pull/723) | Testing Patterns (full-stack testing guidance) | 4444J99 | Open, updated Apr 21 |
| [#509](https://github.com/anthropics/skills/pull/509) | CONTRIBUTING.md (community health metrics) | narenkatakam | Open, updated Mar 19 |
| [#210](https://github.com/anthropics/skills/pull/210) | Frontend Design (clarity & actionability revision) | justinwetch | Open, updated Mar 7 |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for stabilizing the skill-creator meta-skill's evaluation infrastructure** — the 0% recall bug on `run_eval.py` renders the description-optimization loop non-functional, and its Windows incompatibility excludes an entire platform from skill development, making infrastructure reliability the single highest-priority concern across all PRs and issues.

---

# Claude Code Community Digest — 2026-07-05

## Today's Highlights

A major session-limit escalation (#38335) has exploded to 793 comments and 467 upvotes, with users reporting abnormally fast consumption of Max plan sessions since late March — this has become the community's highest-priority grievance. Meanwhile, Fable 5 safety-classifier false positives are generating a cluster of fresh bug reports, with users seeing benign automation and trust-and-safety sessions forcibly downgraded to Opus 4.8. A concerning new auto-compaction regression on Sonnet 5 (#74273) is causing repeated compact/work loops that plateau near 75% context usage.

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

### 1. [#38335 — Claude Max plan session limits exhausted abnormally fast since March 23, 2026](https://github.com/anthropics/claude-code/issues/38335)
- **Status:** OPEN | **Comments:** 793 | **Reactions:** 👍467
- **Why it matters:** This is the most active issue on the repo by a wide margin. Users report Max plan sessions draining 2–3x faster than expected, with CLI sessions consuming limits even when idle. The sustained outrage suggests a systemic billing/usage-metering bug that Anthropic has not resolved in over three months.
- **Community reaction:** Heavy frustration; users sharing workarounds and comparing session counters. Multiple users claim support tickets have gone unanswered.

### 2. [#27302 — Support multiple Connector accounts (same connector, different accounts)](https://github.com/anthropics/claude-code/issues/27302)
- **Status:** OPEN | **Comments:** 209 | **Reactions:** 👍296
- **Why it matters:** Developers managing multiple cloud/enterprise accounts (AWS, GitHub, Slack) from a single machine must constantly re-authenticate. This is a top-voted feature request blocking enterprise adoption.
- **Community reaction:** Strong consensus; users sharing multi-account workflow hacks.

### 3. [#68780 — Claude Opus 4.8 reasoning degradation, speed and performance regression](https://github.com/anthropics/claude-code/issues/68780)
- **Status:** OPEN | **Comments:** 21 | **Reactions:** 👍28
- **Why it matters:** A sustained degradation report from an EU customer threatening legal action over what they call "deceptive business practices." The user compiles extensive evidence of reduced reasoning quality on Opus 4.8 since its launch.
- **Community reaction:** Sympathetic but skeptical; some users report similar experiences while others see no change.

### 4. [#69415 — API Error: Connection closed mid-response — frequent enough to make Claude Code unusable](https://github.com/anthropics/claude-code/issues/69415)
- **Status:** OPEN | **Comments:** 16 | **Reactions:** 👍46
- **Why it matters:** Users on VSCode + WSL report that mid-response connection drops happen every few minutes, breaking long-running code generation tasks entirely. High upvote count for a reliability issue.
- **Community reaction:** Users sharing network configs; no fix identified.

### 5. [#24057 — MCP servers, hooks, and plugins should auto-reload when config changes](https://github.com/anthropics/claude-code/issues/24057)
- **Status:** OPEN | **Comments:** 30 | **Reactions:** 👍15
- **Why it matters:** A foundational quality-of-life issue — every config tweak requires a full session restart, losing context. Users report needing 3+ restarts per session for MCP-heavy workflows.
- **Community reaction:** Strong agreement; users compare it to "rebooting Windows 95."

### 6. [#73784 — Fable 5 safeguards flag benign messages in legitimate anti-fraud (T&S) work](https://github.com/anthropics/claude-code/issues/73784)
- **Status:** OPEN | **Comments:** 7 | **Reactions:** 👍1
- **Why it matters:** A major irony — users doing trust-and-safety work are being flagged by safety classifiers. The forced fallback to Opus 4.8 breaks specialized workflows.
- **Community reaction:** Users requesting configurable override thresholds.

### 7. [#74273 — Auto-compaction plateaus near ~75% context usage on Sonnet 5, causing repeated compact/work loop](https://github.com/anthropics/claude-code/issues/74273)
- **Status:** OPEN | **Comments:** 7 | **Reactions:** 0
- **Why it matters:** A new regression specific to Sonnet 5 (v2.1.201) where context fills faster and compaction doesn't reclaim enough space, leading to a destructive compact → fill → compact cycle.
- **Community reaction:** Users confirming the pattern; no workaround yet.

### 8. [#63930 — Prompt cache fully re-created after turns with many parallel tool calls](https://github.com/anthropics/claude-code/issues/63930)
- **Status:** OPEN | **Comments:** 7 | **Reactions:** 👍4
- **Why it matters:** 74% of cache writes are wasted on Opus 4.8 sessions with heavy parallelism. This translates directly to higher costs for users running complex multi-tool tasks.
- **Community reaction:** Users sharing cache-hit statistics; calling for a caching diagnostic tool.

### 9. [#34196 — VSCode extension: add font size setting for chat panel](https://github.com/anthropics/claude-code/issues/34196)
- **Status:** OPEN | **Comments:** 8 | **Reactions:** 👍56
- **Why it matters:** A simple but heavily upvoted ergonomic request — the chat panel font is too small and not independently configurable. High reaction count for a minor UI fix.
- **Community reaction:** Users sharing custom CSS workarounds.

### 10. [#28018 — Sandbox: allow outbound connections to localhost](https://github.com/anthropics/claude-code/issues/28018)
- **Status:** OPEN | **Comments:** 5 | **Reactions:** 👍60
- **Why it matters:** Blocks integration testing against local Docker services. Very high reaction count for a sandbox usability issue that makes local dev workflows impossible.
- **Community reaction:** Users requesting `sandbox.network.allowLocalhost` flag.

---

## Key PR Progress

No pull requests were updated in the last 24 hours.

---

## Feature Request Trends

Based on the current issue landscape, the dominant feature request themes are:

1. **Multi-account/identity management** (#27302) — Support for multiple Connector accounts and session-level identity switching remains the top-voted open feature request.

2. **Persistent team/shared memory** (#38536) — Users want Claude Code to support team-wide knowledge transfer rather than per-user isolated memory.

3. **Hot-reloadable configuration** (#24057) — MCP servers, hooks, and plugins should auto-reload on config change without session restart.

4. **Configurable safety classifier behavior** (#74311, #73833) — Fable 5's safety classifier fallback should allow users to configure target model, effort level, and override thresholds.

5. **Always-visible cost/usage display** (#74270) — Paid subscribers want glanceable rate-limit and spend info by default, not hidden behind a command.

---

## Developer Pain Points

1. **Session limit exhaustion** (#38335, #74279) — Max plan sessions draining abnormally fast is the #1 community pain point, with 793 comments spanning three months without resolution.

2. **Safety classifier false positives** (#73784, #74290, #74295) — Fable 5 safety classifiers are flagging legitimate development work (automation, trust-and-safety, marketing pipelines) and forcing fallback to Opus 4.8, breaking workflows.

3. **Connection reliability** (#69415) — Mid-response connection closures on WSL/VSCode make Claude Code unusable for sustained tasks.

4. **Context compaction regressions** (#74273) — Sonnet 5 auto-compaction not reclaiming enough context, causing destructive compact/fill loops.

5. **Prompt cache waste** (#63930) — Parallel tool calls causing full cache re-creation, wasting ~74% of cache writes and increasing costs.

6. **MCP tool parameter dropping** (#72228) — Long parameter values cause subsequent parameters to be silently dropped from MCP tool calls.

7. **Windows subprocess flashes** (#66540) — Visible terminal windows flash on every subprocess spawn across multiple concurrent sessions.

8. **Outdated documentation** (#72945) — Sub-agents quickstart still references a wizard that was removed in v2.1.198.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-05

## Today's Highlights

The community is ablaze over a **severe rate-limit cost regression** in Codex (gpt-5.5) that has drained Plus-plan budgets in as few as 2–3 prompts since June 16, sparking a 346-upvote firestorm with 198 comments. Concurrently, a **massive SSD write amplification bug** in SQLite feedback logging—projected to write ~640 TB/year—has been partially fixed across three merged PRs, though related disk-write concerns persist on macOS and Windows. Security-minded users flagged a **SysmonDrv.sys BSOD crash** triggered by Codex Desktop on Windows, while a new `rust-v0.143.0-alpha.36` release offers bleeding-edge functionality for Rust-based workflows.

## Releases

- **[rust-v0.143.0-alpha.36](https://github.com/openai/codex/releases)** — Pre-alpha release (0.143.0-alpha.36) for the Rust-based Codex runtime. No changelog details beyond version bump; likely experimental infrastructure for the Codex CLI or sandbox components.

## Hot Issues (Top 10)

1. **[#28879](https://github.com/openai/codex/issues/28879) — Rate-limit cost per token jumped 10–20x since June 16**  
   *Tags: bug, rate-limits, app* | **Comments: 198 | 👍: 346**  
   The most-upvoted open issue right now. Users report their 5-hour Plus budget evaporates in 2–3 prompts on gpt-5.5, where previously they got 20+. Session logs show `limit-% consumed per token` increased ~10–20×. Community sentiment: this is the highest-priority regression affecting paying customers daily.

2. **[#28224](https://github.com/openai/codex/issues/28224) — SQLite feedback logs can write ~640 TB/year, consuming SSD endurance**  
   *Tags: bug, CLI, performance* | **Comments: 130 | 👍: 421**  
   Astounding community response. Three PRs (#29432, #29457, and an unnamed third) merged into 0.142.0 reportedly cut log volume by 85% for the reporter. Now closed by author, but the sheer scale (640 TB/year) highlights how feedback logging was a silent SSD killer. The 421 upvotes indicate many users were affected.

3. **[#8648](https://github.com/openai/codex/issues/8648) — Codex replies to earlier messages instead of the latest in conversations**  
   *Tags: bug, context, agent* | **Comments: 78 | 👍: 55**  
   Long-running issue (since Jan 2026) with no resolution. In multi-message threads, Codex occasionally responds to a mid-conversation message rather than the latest user input, breaking workflow continuity. Heavily commented, indicating widespread frustration.

4. **[#30364](https://github.com/openai/codex/issues/30364) — GPT-5.5 reasoning-token clustering at 516/1034/1552**  
   *Tags: bug, model-behavior, rate-limits* | **Comments: 55 | 👍: 92**  
   Compelling data-driven bug report: `gpt-5.5` responses disproportionately land at exactly 516 reasoning tokens, with spikes at 1034 and 1552. Coincides with degraded reasoning quality. Suggests a token-budget quantization bug in the model serving layer, not a user-facing config issue.

5. **[#15975](https://github.com/openai/codex/issues/15975) — Codex extension stuck on loading screen after VS Code update (Windows)**  
   *Tags: bug, windows-os, extension* | **Comments: 15 | 👍: 4**  
   Persisting since March 2026. After VS Code updates on Windows, the Codex extension hangs on the logo screen. No fix yet; impacts workplace subscribers.

6. **[#31035](https://github.com/openai/codex/issues/31035) — Windows Codex Desktop reinstalls SysmonDrv v13.22, causing BSODs**  
   *Tags: bug, windows-os, sandbox, app* | **Comments: 13 | 👍: 0**  
   Critical stability issue: Codex Desktop re-installs Sysinternals Sysmon driver after forced uninstallation, then `SysmonDrv.sys` crash dumps point to BSODs. Low upvotes but high severity—system-level crashes are showstoppers for Windows users.

7. **[#30486](https://github.com/openai/codex/issues/30486) — Windows Desktop: Chrome/Computer Use enabled but JS REPL tool not exposed**  
   *Tags: bug, windows-os, mcp, app, computer-use, browser* | **Comments: 10 | 👍: 0**  
   MCP integration bug: `mcp__node_repl__js` tool is registered but not exposed to Codex turns, blocking JavaScript execution in browser automation workflows. Blocks core Computer Use functionality on Windows.

8. **[#26876](https://github.com/openai/codex/issues/26876) — GPT-5.5 degradation over time in complex engineering workflows**  
   *Tags: bug, model-behavior, CLI* | **Comments: 10 | 👍: 2**  
   Suspected model quality regression since the April 24 GPT-5.5 rollout. Users observe material behavioral degradation in local Codex usage over extended sessions. Corroborates the token-clustering issue (#30364).

9. **[#21073](https://github.com/openai/codex/issues/21073) — Feature Request: Auto-resume CLI session when usage limit resets**  
   *Tags: enhancement, rate-limits, enterprise* | **Comments: 8 | 👍: 27**  
   Popular quality-of-life request: when a CLI session hits the usage limit, Codex should automatically resume the paused task when the quota resets. Currently the "try again at X:XX" message is wasted if the user is asleep.

10. **[#19143](https://github.com/openai/codex/issues/19143) — Support pasting images directly into Codex CLI**  
    *Tags: bug, TUI* | **Comments: 7 | 👍: 3**  
    Terminal-only users can't paste screenshots or images into CLI sessions, blocking frontend debugging and DevTools workflows. Straightforward gap that forces context-switching to the Desktop app.

## Key PR Progress (Top 10)

1. **[#31138](https://github.com/openai/codex/pull/31138) — fix(windows-sandbox): grant delete rights to writable roots** — *OPEN*  
   Fixes a Windows sandbox permission issue where writable roots lacked delete/delete-child rights. Adds a behavioral regression test. Critical for file-management workflows on Windows.

2. **[#31064](https://github.com/openai/codex/pull/31064) — Read buffering metadata from response events** — *CLOSED*  
   Reads optional `faster-model` metadata from streamed buffering payloads to reduce latency. Retains backward compatibility. Improves responsiveness for third-party traffic.

3. **[#30669](https://github.com/openai/codex/pull/30669) — perf(thread-store): project append metadata asynchronously** — *OPEN*  
   Moves thread metadata projection off the synchronous append path into a per-thread worker with generation barriers. Should reduce latency spikes during thread rollouts.

4. **[#30325](https://github.com/openai/codex/pull/30325) — Read retry_model from safety buffering events** — *OPEN*  
   Directs third-party traffic safety-buffering metadata through the existing `fasterModel` path instead of dropping it. Improved handling for non-first-party API consumers.

5. **[#31116](https://github.com/openai/codex/pull/31116) — [multi-agent] Preserve child environments across reload** — *OPEN*  
   Fixes a multi-agent state-loss bug: when idle child agents are reloaded, their explicitly selected environments were replaced with manager defaults. Now preserves child environment selections across reloads.

6. **[#31092](https://github.com/openai/codex/pull/31092) — fix(login): improve device auth contrast on dark terminals** — *OPEN*  
   Replaces hardcoded bright-black ANSI color with proper dimming on dark terminals. Improves readability of device-auth prompts and phishing warnings for CLI users in dark-mode terminals.

7. **[#31058](https://github.com/openai/codex/pull/31058) — fix(core): retry model capacity errors** — *OPEN*  
   Retries HTTP 503 capacity errors up to 3 times with jittered delays (30s, 2min, 5min). Defers only capacity-coded errors from the normal retry layer. Addresses transient capacity failures that currently drop sessions.

8. **[#30866](https://github.com/openai/codex/pull/30866) — fix(app-server): reconcile loaded thread history on resume** — *OPEN*  
   Reconciles an already-loaded, idle thread with its persisted rollout when `thread/resume` is called. Prevents state corruption and history injection on session resume.

9. **[#31070](https://github.com/openai/codex/pull/31070) — Authorize primary Git configuration sources before patch operations** — *OPEN*  
   Prevents Git patch operations from consuming configuration files routed through the worktree or other repository-controlled locations. Part of a multi-PR security hardening series for Git operations.

10. **[#31072](https://github.com/openai/codex/pull/31072) — Bind patch application to guarded Git configuration** — *OPEN*  
    Ensures validated Git configuration, repository authority, and allowed operations remain bound through the child process performing mutations. Complements #31070 and #31071 for defense-in-depth in Codex's Git patch pipeline.

## Feature Request Trends

1. **Session Resilience & Auto-Resume** (#21073, #24289) — Users want Codex to automatically resume tasks paused by usage limits and auto-generate thread names after the first prompt. The unified demand is for *invisible session management* that doesn't waste user attention.

2. **Multi-Tab & Multi-Thread UX** (#23314, #31124) — Requests for multiple visible tabs in the in-app browser and syncing terminal title with thread names. Users want better visual context management across parallel workflows.

3. **Image Pasting in CLI** (#19143) — Singular but consistent request: direct clipboard image paste support in the terminal-based CLI, not just the Desktop app. Essential for frontend debugging without context-switching.

4. **Data Retention Controls** (#24610) — Explicit deletion controls for archived cloud sessions, citing privacy concerns around sensitive project context persisting indefinitely after archiving.

## Developer Pain Points

- **Rate-Limit & Cost Instability** — The dominant pain point. Multiple reports (#28879, #30785, #30842, #31060, #29895) describe unpredictable budget draining, token-cost spikes, and misattributed usage between models. The community feels the pricing model is opaque and untrustworthy.

- **Disk Write Amplification & SSD Wear** (#28224, #29876, #30715) — Beyond the headline 640 TB/year SQLite bug, users continue reporting excessive disk writes on macOS and Windows even after the 85% log reduction. SSD endurance remains a top concern for heavy users.

- **Windows Stability & Sandbox Issues** (#15975, #31035, #30486, #31137, #29929) — A cluster of Windows-specific bugs: BSODs from Sysmon driver, missing JS REPL tool, Git authentication not persisting, memory allocation crashes after large tool output. Windows users face systemic instability compared to macOS.

- **Model Quality Degradation** (#26876, #30364) — The perception that GPT-5.5 degrades over prolonged sessions, combined with the token-clustering artifact at fixed boundaries, erodes trust in model consistency for complex engineering tasks. Developers report having to restart sessions mid-workflow to maintain quality.

- **Auth & Git Integration Fragility** (#30970, #29828, #31137) — Pro accounts being treated as Free users, Git auth not persisting across restarts on Windows, and Git UI surfaces disappearing after crashes. Users feel authentication and repository management are "brittle" and require frequent reconfiguration.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-05

## Today's Highlights
A new nightly release (v0.51.0-nightly.20260705) is out, bringing the latest round of fixes. The community remains focused on agent reliability, with three major P1 bugs still unresolved: subagent goal misreporting after MAX_TURNS, generalist agent hangs, and shell command execution getting stuck post-completion. Several important PRs landed this week addressing thought leakage, template corruption, and startup performance on Windows.

## Releases
- **[v0.51.0-nightly.20260705.gf7af4e518](https://github.com/google-gemini/gemini-cli/compare/v0.51.0-nightly.20260704.gf7af4e518...v0.51.0-nightly.20260705.gf7af4e518)** — Automated nightly build. No user-facing changelog provided.

## Hot Issues (Top 10 by Community Attention)

1. **[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) — Subagent recovery after MAX_TURNS reported as GOAL success** (P1, 9 comments, 2 👍)
   Critical bug: `codebase_investigator` subagent reports `status: "success"` when it actually hit the turn limit without doing any analysis. Misleads users into thinking work was completed.

2. **[#19873](https://github.com/google-gemini/gemini-cli/issues/19873) — Zero-Dependency OS Sandboxing & Post-Execution Intent Routing** (P2, 8 comments, 1 👍)
   Long-running enhancement to leverage Gemini 3's native bash affinity. Proposes sandboxed shell execution that routes post-command intent back to the model. Large effort, high architectural impact.

3. **[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) — Generalist agent hangs forever** (P1, 7 comments, 8 👍)
   Most upvoted open bug. Deferring to the generalist agent causes indefinite hangs — even for simple folder creation. Workaround exists (instruct model not to use sub-agents), but this severely impacts daily workflows.

4. **[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) — Robust component level evaluations** (P1, 7 comments)
   Epic tracking behavioral eval infrastructure. 76 test cases exist across 6 Gemini models. Critical for preventing regressions as agent capabilities grow.

5. **[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) — AST-aware file reads, search, and mapping** (P2, 7 comments, 1 👍)
   Investigation into using AST parsing for more precise method-bound reads and codebase navigation. Could reduce token usage and turn count.

6. **[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) — Shell command gets stuck with "Waiting input" after completion** (P1, 4 comments, 3 👍)
   High-impact P1: simple CLI commands hang, still showing "Awaiting user input" after the command finishes. Occurs repeatedly, affects core shell integration.

7. **[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) — Gemini does not use skills and sub-agents enough** (P2, 6 comments)
   Anecdotal but validated: model rarely invokes custom skills or sub-agents autonomously, even for clearly related tasks. Reduces value of user-defined agent configurations.

8. **[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) — Browser subagent fails on Wayland** (P1, 4 comments, 1 👍)
   P1 blocker for Linux Wayland users. Browser subagent terminates with "GOAL" status but actually crashes. Affects all Wayland-based desktop environments.

9. **[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) — Auto Memory retries low-signal sessions indefinitely** (P2, 5 comments)
   Background extraction agent loops on low-signal sessions because they're never marked as processed. Wastes API credits and CPU cycles.

10. **[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) — Symlinked agent files not recognized** (P2, 4 comments)
    Simple but frustrating UX bug: `~/.gemini/agents/filename.md` symlinks are silently ignored. Users managing agent configs with dotfile managers are affected.

## Key PR Progress (Top 10)

1. **[#28253](https://github.com/google-gemini/gemini-cli/pull/28253) — Fix footer branch sync on filesystems without fs.watch** (area/core, size/m)
   Fixes git branch indicator not updating after checkout on WSL mounts and network shares. Important for Windows/Linux hybrid workflows.

2. **[#28059](https://github.com/google-gemini/gemini-cli/pull/28059) — Don't let unreadable .env (EACCES) break extension loading** (area/extensions, size/m)
   Fixes #27894: sandboxed environments with unreadable `.env` files no longer crash the extension system. Adds Cloud Shell path hardening.

3. **[#28112](https://github.com/google-gemini/gemini-cli/pull/28112) — SSRF protection for OAuth metadata discovery** (size/l)
   Security fix: OAuth discovery flow now validates URLs from MCP server responses, matching existing protections in `web-fetch.ts`. Closes a coverage gap.

4. **[#27971](https://github.com/google-gemini/gemini-cli/pull/27971) — Strip thoughts from scrubbed history turns** (size/m, CLOSED)
   Resolves "Thought Leakage" — model internal monologues leaking into history, causing infinite loops. Surgically removes `thinking` blocks from scrubbed turns.

5. **[#28055](https://github.com/google-gemini/gemini-cli/pull/28055) — Preserve dollar sequences in prompt template substitutions** (area/agent, size/m, CLOSED)
   Fixes corruption of `$` sequences (`$$`, `$'`, `$&`) in skill and sub-agent descriptions during system prompt template rendering.

6. **[#28033](https://github.com/google-gemini/gemini-cli/pull/28033) — Longest-prefix matching for MCP tool names with underscores** (area/agent, size/m, CLOSED)
   Fixes #27981: MCP server names containing underscores (e.g., `my_server`) now route tools correctly using longest-prefix matching.

7. **[#28164](https://github.com/google-gemini/gemini-cli/pull/28164) — Limit recursive reasoning turns per user request** (size/m)
   Implements a 15-turn limit on recursive reasoning to protect CPU and API quota from infinite loops. Customizable via `maxSessionTurns`.

8. **[#28162](https://github.com/google-gemini/gemini-cli/pull/28162) — Buffer chat compression telemetry** (area/enterprise, size/m)
   Fixes #23445: OTEL log emission and metrics for chat compression are now properly buffered. Prevents telemetry data loss.

9. **[#28144](https://github.com/google-gemini/gemini-cli/pull/28144) — Detect available editors lazily to avoid slow startup** (area/core, size/m)
   Fixes slow startup on Windows: editor detection now runs lazily instead of probing every known editor at module load with `execSync`.

10. **[#27839](https://github.com/google-gemini/gemini-cli/pull/27839) — Make read_background_output delay abort-aware** (size/s, CLOSED)
    Pressing ESC to cancel `read_background_output` now actually stops the tool. Previously the `delay_ms` sleep used `setTimeout` without abort signal.

## Feature Request Trends

1. **Agent Self-Awareness & Introspection** — Multiple issues request better agent understanding of its own capabilities: accurate CLI flag reporting ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)), subagent trajectory visibility in `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)), and bug reports that include subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)).

2. **AST-Aware Code Analysis** — Growing interest in leveraging AST parsing for smarter file reads, codebase mapping, and navigation ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)). Could reduce token waste from misaligned reads.

3. **Zero-Dependency Sandboxing** — The community wants safer bash execution without Docker or heavy sandbox dependencies ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)). Gemini 3's native bash affinity makes this particularly promising.

4. **Destructive Action Prevention** — Users want agents to prefer safer alternatives for git operations, database modifications, and file system changes ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).

5. **Browser Agent Resilience** — Requests for automatic session takeover and lock recovery ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)), plus Wayland support ([#21983](https://github.com/google-gemini/gemini-cli/issues/21983)).

## Developer Pain Points

- **Agent hangs & false success reporting** — The #1 frustration. Generalist agent hangs forever ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands get stuck ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and subagents falsely report GOAL success after hitting turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)). These are all P1 bugs with no resolution yet.

- **Subagent autonomy problems** — Agents don't use skills/sub-agents autonomously ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)), but also run sub-agents without permission ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)). The balance between autonomy and control remains broken.

- **Memory system inefficiency** — Auto Memory retries low-signal sessions indefinitely ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), silently skips invalid inbox patches ([#26523](https://github.com/google-gemini/gemini-cli/issues/26523)), and lacks deterministic secret redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)).

- **Tool overload** — Encountering 400 errors with >128 tools ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)). The agent needs smarter tool scoping.

- **Configuration & environment edge cases** — Symlinked agents not recognized ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)), browser agent ignores `settings.json` ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)), unreadable `.env` breaks extensions (fixed in [#28059](https://github.com/google-gemini/gemini-cli/pull/28059)), and slow startup on Windows (fixed in [#28144](https://github.com/google-gemini/gemini-cli/pull/28144)).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-05

## Today's Highlights
A minor release (v1.0.69-1) landed with improved MCP server management, allowing live toggling of servers mid-turn. The issue tracker saw a surge in triage-level bug reports, with seven new issues filed in the last 24 hours covering silent tool resolution failures, Windows crashes, transcription bugs, and session memory cross-contamination. The long-standing request to open-source the CLI continues to gather community support (12 👍).

## Releases
**[v1.0.69-1](https://github.com/github/copilot-cli/releases/tag/v1.0.69-1)** — Minor feature release  
- Added `/mcp list` to display attached MCP servers and their status  
- `/mcp list` and `/plugin list` now work while the agent is processing  
- The MCP manager can be opened mid-turn to enable/disable servers; add, edit, delete, and re-auth remain paused until the turn completes

## Hot Issues

1. **[#3236](https://github.com/github/copilot-cli/issues/3236) — [OPEN] ENGLAND stole all my money And killked my GRANDMOTHER and UNCZlE**  
   Author: parezanovicluka863-byte | Comments: 2 | 👍: 0  
   *Why it matters:* Appears to be spam or off-topic content. No actionable bug detail. Low signal.

2. **[#3241](https://github.com/github/copilot-cli/issues/3241) — [OPEN] Open sourcing the copilot cli**  
   Author: vz443 | Comments: 2 | 👍: 12  
   *Why it matters:* Strong community interest (highest 👍 count today). Request covers agent SDK for workflows/pipelines on private infrastructure. A key signal for enterprise adoption.

3. **[#4019](https://github.com/github/copilot-cli/issues/4019) — [OPEN] Built-in web_fetch does not work with HTTP proxies**  
   Author: JoergStrebel | Comments: 2 | 👍: 0  
   *Why it matters:* Blocks `/research` and URL retrieval in corporate WSL environments behind mandatory HTTP proxies. Affects enterprise users.

4. **[#3533](https://github.com/github/copilot-cli/issues/3533) — [OPEN] CLI 1.0.54 keyboard input not working on macOS**  
   Author: cfrichot-b | Comments: 1 | 👍: 0  
   *Why it matters:* Persistent bug since May — text input unresponsive, TUI partially obscured by auth prompts. High-impact for macOS users.

5. **[#2595](https://github.com/github/copilot-cli/issues/2595) — [OPEN] Background agent completion retention**  
   Author: yannickwellens | Comments: 1 | 👍: 0  
   *Why it matters:* Completed background agents are purged too quickly from registry; `read_agent` fails after success notification. Disrupts multi-agent workflows.

6. **[#4029](https://github.com/github/copilot-cli/issues/4029) — [OPEN] Kimi K2.7 Code not available in Pro subscription**  
   Author: aregtech | Comments: 0 | 👍: 0  
   *Why it matters:* Policy claims Kimi Code 2.7 is Pro-eligible but it appears in "Blocked/Disabled" list. Subscription-model confusion.

7. **[#4028](https://github.com/github/copilot-cli/issues/4028) — [OPEN] Unable to switch tabs with keyboard**  
   Author: gioisco | Comments: 0 | 👍: 0  
   *Why it matters:* Keyboard navigation to Gists tab broken in v1.0.68 — accessibility regression for terminal power users.

8. **[#4018](https://github.com/github/copilot-cli/issues/4018) — [OPEN] Configurable scroll speed / scroll-sensitivity**  
   Author: niranjanviladkar | Comments: 0 | 👍: 0  
   *Why it matters:* VS Code integrated terminal scrolling is unusably fast — no setting to tune it. Repeatedly requested.

9. **[#4024](https://github.com/github/copilot-cli/issues/4024) — [OPEN] Voice mode: all bundled ASR models fail silently**  
   Author: sylvanc | Comments: 0 | 👍: 0  
   *Why it matters:* All three `/voice` speech-to-text models return empty transcriptions. Likely a routing bug in `MultiModalProcessor`. Voice mode non-functional.

10. **[#4026](https://github.com/github/copilot-cli/issues/4026) — [OPEN] Copilot CLI crashes repeatedly on Windows (native runtime)**  
    Author: millshre5 | Comments: 0 | 👍: 0  
    *Why it matters:* Unresolved crash since May 2026 across four versions (v1.0.15–v1.0.53). No single reproducer — hardest class of bugs. Critical for Windows users.

## Key PR Progress

1. **[#3771](https://github.com/github/copilot-cli/pull/3771) — [OPEN] Initial project setup**  
   Author: limenpchuolto112-creator | Comments: undefined | 👍: 0  
   *Description:* Appears to be a placeholder or template PR. No substantive changes.

*Note: Only one PR was updated in the last 24 hours. The PR tracker is notably quiet today.*

## Feature Request Trends
- **MCP/Plugin Live Management** — Enabled in v1.0.69-1, but requests for deeper control (add/edit/delete mid-turn) remain implicit in issue patterns.
- **Configurable TUI Behavior** — Scroll speed/sensitivity (#4018), keyboard tab navigation (#4028) point to demand for terminal UX customization.
- **Enterprise Networking** — Proxy support (#4019) continues as top enterprise blocker.
- **Open-Source / Self-Hosted Agents** — The #3241 request (12 👍) signals growing appetite for running Copilot agent infrastructure on private metal.
- **Model Parity** — Kimi K2.7 availability dispute (#4029) reflects frustration with subscription gating on advertised models.

## Developer Pain Points
- **Silent Failures** — Headless agent tool aliases (`web`/`search`) silently resolve to no tool (#4023); voice mode ASR models fail with no error (#4024). Poor debuggability.
- **Session State Corruption** — Session history cross-contamination across projects (#4025); false "already in use" session locks (#4020). Core state management fragile.
- **Platform Instability** — Repeated Windows native crashes (#4026) unresolved for weeks; macOS keyboard input hangs (#3533). Cross-platform reliability is uneven.
- **Plugin Lifecycle Confusion** — Contradictory "already registered" / "not registered" errors when removing marketplace plugins (#4021). UX logic error in the plugin manager.
- **Tool Name Mismatches** — Tool `str_replace` referenced but nonexistent (#4027) — suggests a model hallucination or tool registry drift between agent and runtime.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date**: 2026-07-05  
**Focus**: Technical analysis of github.com/MoonshotAI/kimi-cli

---

## 1. Today's Highlights
A single bug fix was on the community radar today: Issue #2484, which addresses a critical gap where the `thinking.enabled=false` configuration fails to suppress chain-of-thought output for third-party OpenAI-compatible providers (e.g., DeepSeek via Sensenova). This is particularly relevant for developers using multi-provider setups who need consistent non-thinking behavior. No new releases or pull requests were merged in the last 24 hours, indicating a quieter day in the repo's active development cycle.

## 2. Releases
No new releases were published in the last 24 hours. Developers should refer to the latest stable release for current features.

## 3. Hot Issues
Only one issue was updated in the last 24 hours. Here is the single noteworthy item:

- **#2484: [Bug] `thinking.enabled=false` does not take effect for third-party OpenAI compatible vendors (DeepSeek still defaults to thinking)**  
  **Why it matters**: This is a configuration regression that affects users relying on the kimi-cli as a universal front-end for multiple LLM providers. When using OpenAI-compatible APIs (e.g., DeepSeek via Sensenova), the `thinking` flag is ignored, forcing unwanted reasoning output. The issue was opened by the community and has one comment, suggesting a non-trivial configuration parsing bug in the provider abstraction layer. The issue has been closed, implying a fix or workaround was identified, but the root cause (e.g., vendor-specific parameter mapping) may still be relevant for other providers.  
  **Reaction**: Single comment, zero reactions – indicating focused debugging rather than widespread outcry.  
  **Link**: [Issue #2484](https://github.com/MoonshotAI/kimi-cli/issues/2484)

## 4. Key PR Progress
No pull requests were updated in the last 24 hours. No PRs to report.

## 5. Feature Request Trends
Based on the single issue and absence of new PR features, the clearest unaddressed feature need is **universal provider configuration normalization**. Developers expect that a single global configuration (`thinking.enabled=false`) should uniformly apply across all provider types, including third-party OpenAI-compatible endpoints. The repo lacks a centralized middleware that normalizes vendor-specific parameters (e.g., `thinking` vs. `reasoning_mode` vs. `chain_of_thought`). This suggests a future direction toward an **abstraction layer for provider-specific knobs** (temperature, thinking, top_p) that maps user-friendly config names to vendor-specific API fields.

## 6. Developer Pain Points
The recurring frustration visible in the repo (exemplified by #2484) is **configuration inconsistency across third-party providers**. Developers using kimi-cli as a unified CLI tool expect identical behavior regardless of backend. The pain point is twofold:
- **Expectation failure**: A config flag works for native Kimi models but silently fails for third-party endpoints.
- **Debugging opacity**: No clear warning or log message when a configuration key is ignored for a given provider.

While only one issue surfaced today, the pattern of "works for first-party, silent ignore for third-party" is a common cause of developer trust erosion in CLI tools that aggregate multiple LLM backends.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-05

## Today's Highlights

The past 24 hours saw intense activity around two critical infrastructure issues: a widespread **DeepSeek V4 Flash / Console Go rate limit failure** that rendered the Go tier unusable for many users, and a **V2 daemon crash loop** caused by MCP tool change events being rejected by the SSE encoder. The team responded swiftly with protocol fixes (Kit Langton contributed three PRs on the event bus) and a new `session_input` durable inbox for compaction barriers to break the infinite auto-compaction loops that have plagued users.

## Releases

No releases in the last 24 hours. The latest stable is **v1.17.13** (2026-07-01), which itself shipped with a known web UI session-list blank bug (details below).

## Hot Issues

1. **[#34893 — Inference is temporarily unavailable (DeepSeek V4 Flash, Ubuntu)](https://github.com/anomalyco/opencode/issues/34893)**  
   *37 comments, 25 👍*  
   High-severity outage. `opencode/deepseek-v4-flash-free` inference went dark for 5+ minutes on Ubuntu. Users unable to reproduce reliably; may be a transient infrastructure issue. **CLOSED**, root cause under investigation.

2. **[#15533 — Auto-compaction infinite loop when assistant ends its turn](https://github.com/anomalyco/opencode/issues/15533)**  
   *24 comments, 11 👍*  
   Persistent, well-known bug (open since March). When the assistant finishes naturally (`finish === "stop"`), `SessionCompaction.process()` injects a synthetic "Continue..." message unconditionally, which can trigger a runaway compaction loop. A durable compaction barrier PR (#35371) aims to fix this.

3. **[#19604 — Write tool fails silently on large files (~1000+ lines)](https://github.com/anomalyco/opencode/issues/19604)**  
   *17 comments, 11 👍*  
   Critical regression: the `Write` tool returns success but writes nothing for files ≥1000 lines. No error surfaced to the user. Community frustration is high — this breaks core development workflows.

4. **[#34884 — "Provider rate limit exceeded" despite 0% rolling usage](https://github.com/anomalyco/opencode/issues/34884)**  
   *16 comments, 6 👍*  
   Users on the Console Go tier hit rate limits even with zero usage. Free-tier models remain functional. Multiple related reports suggest a backend-side Go subscription billing error. **CLOSED** after upstream root cause identified.

5. **[#8625 — Auto-defer MCP tool descriptions when they exceed 10% context (75 👍)](https://github.com/anomalyco/opencode/issues/8625)**  
   *11 comments, 75 👍*  
   The community's most upvoted feature request. Proposes automatic lazy-loading of MCP tool descriptions via MCP-Search when they consume too much context. A related `mcp.tools.changed` event fix (#35373) just landed.

6. **[#34222 — MAI-Code-1-Flash not accessible via `/chat/completions` endpoint](https://github.com/anomalyco/opencode/issues/34222)**  
   *7 comments, 8 👍*  
   Org-admin-enabled Microsoft MAI-Code-1-Flash model on Copilot Enterprise fails with "not accessible via the /chat/completions endpoint." Workaround attempts with alternative picker names also fail. Blocks enterprise users.

7. **[#30680 — Immediate auto-compaction loop in empty folder, stops responding](https://github.com/anomalyco/opencode/issues/30680)**  
   *12 comments*  
   Started compacting immediately in a fresh project, consuming tokens endlessly, then stopped responding to prompts entirely. Related to #15533. PR #35371's compaction barrier is the proposed fix.

8. **[#32954 — Allow selecting multiple skills from `/skills` TUI](https://github.com/anomalyco/opencode/issues/32954)**  
   *3 comments, 4 👍*  
   Currently `/skills` clears previous selections. Users want multi-select to compose skill capabilities in a single prompt session.

9. **[#35340 — v1.17.13 web UI session list empty (regression)](https://github.com/anomalyco/opencode/issues/35340)**  
   *2 comments*  
   Stable release ships with a blank session sidebar. Fixes were applied to `dev` months ago (#30167, #30314, #30804) but never cherry-picked to `v1.17.x`. Blocks web users on latest stable.

10. **[#35339 — AI deleted all contents of working directory via `rm -rf .` without confirmation](https://github.com/anomalyco/opencode/issues/35339)**  
    *2 comments*  
    Catastrophic accidental deletion. The agent performed `rm -rf .` with no prompt or confirmation. Highlights urgent need for destructive-action guardrails and sandboxing.

## Key PR Progress

1. **[#35381 — Validate scalar newtypes with `Schema.brand`](https://github.com/anomalyco/opencode/pull/35381)** (Closed)  
   Replaces `Schema.Opaque` with `Schema.brand` for scalar newtypes, improving type safety while keeping primitive runtime values and nominal identities.

2. **[#35369 — Enable follow-up queue mode with per-message override](https://github.com/anomalyco/opencode/pull/35369)** (Open)  
   Unblocks the previously neutered queue setting. Adds a Settings dropdown to choose "queue" vs. "steer" mode, plus a per-message override hotkey.

3. **[#35010 — Reopen closed tabs and background tab open](https://github.com/anomalyco/opencode/pull/35010)** (Closed)  
   Adds browser-style tab management (`⇧⌘T`/`Ctrl+Shift+T` to reopen) and background tab open via modifier keys for the desktop/v2 tab strip.

4. **[#35375 — Optimize large review panes with virtualization](https://github.com/anomalyco/opencode/pull/35375)** (Open)  
   Replaces recursive review file tree with flat, virtualized model using TanStack virtualization. Fixes expensive Kobalte tab-content observation. Essential for large diffs.

5. **[#34747 — Terminal improvements with drag-and-drop tabs](https://github.com/anomalyco/opencode/pull/34747)** (Open)  
   Adds `dnd-kit` tabs to the terminal panel matching navigation tab behavior. Fixes terminal layout issues.

6. **[#35373 — Expose MCP tool change events in V2 SSE](https://github.com/anomalyco/opencode/pull/35373)** (Closed)  
   Fixes a critical protocol bug where `mcp.tools.changed` was published but not in the SSE manifest, causing encoder rejection and daemon restarts.

7. **[#35378 — Keep internal events off SSE bus](https://github.com/anomalyco/opencode/pull/35378)** (Closed)  
   Companion to #35373: moves internal-only events to a separate bus, precomputes public event registry, preventing future encoder crashes from missing event types.

8. **[#35316 — Show compaction progress in TUI](https://github.com/anomalyco/opencode/pull/35316)** (Closed)  
   Adds `Compacting conversation...` indicator in the prompt footer during manual and automatic compaction. Improves UX for long-running compaction operations.

9. **[#35371 — Add durable compaction barrier](https://github.com/anomalyco/opencode/pull/35371)** (Open)  
   Generalizes `session_input` into a typed durable inbox. Admits one manual compaction barrier per session, blocking all new prompts behind it until active continuation finishes. Directly addresses #15533.

10. **[#34267 — Collapse system messages when plugin appends single entry](https://github.com/anomalyco/opencode/pull/34267)** (Open)  
    Fixes the post-hook collapse logic that only activates on `system.length > 2`. Ensures single-entry plugin system messages are collapsed to reduce noise in the LLM request.

## Feature Request Trends

The most‑requested feature directions, by upvote volume:

- **MCP Tool Context Optimization** (#8625, 75 👍): Auto-defer MCP tool descriptions exceeding 10% of context window, lazy‑load via MCP‑Search.
- **Claude‑Style Tool Search** (#9461, 19 👍): Native implementation of the Tool Search Tool approach from Claude API.
- **Multi‑Skill Selection** (#32954, 4 👍): Allow `/skills` in TUI to compose multiple skills per prompt.
- **Skill/Agent Composition**: Implicit requests for combining capabilities across skills, MCP servers, and models.

## Developer Pain Points

1. **Runaway auto-compaction**: Multiple issues (#15533, #30680, #35371) describe infinite compaction loops that consume tokens and stall responses. The root cause — a synthetic "Continue..." message unconditionally injected after natural turn completion — has been widely discussed but is only now receiving a systematic fix via the compaction barrier pattern.

2. **Silent failures**: The Write tool silently failing on large files (#19604) and the web UI session list showing blank despite healthy API (#35340) erode developer trust. Users want *some* error feedback rather than no-op success.

3. **Rate limit / entitlement confusion**: Multiple users on the Console Go tier (#34884, #34885) hit false rate limits. The retry mechanism loops indefinitely without escalating. Dashboard-proven zero usage doesn't help — suggests a backend billing/entitlement cache issue.

4. **Destructive actions without guardrails**: The `rm -rf .` incident (#35339) highlights the absence of confirmation flows for destructive shell commands, a gap that grows more urgent as agent autonomy increases.

5. **Windows path handling**: Two issues (#35333, #35335) and a closed PR address inconsistent path normalization and Bun Shell emulation problems on Windows. The community is self-organizing migration plans to native PowerShell execution.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-05

## Today's Highlights

The past 24 hours saw a burst of 22+ closed issues, many filed and resolved same-day, indicating a focused cleanup sprint. Key tensions emerged around LLM tool-call reliability, with a new `Strict Tools` RFC (#6306) and a controversial proposal to stop "salvaging" malformed JSON (#6285). Community contributions also added `/improve` for whole-repo audits and a fix to pass through OpenRouter's real usage costs.

## Releases

No new versions released in the last 24 hours. (Latest remains `v0.80.3`.)

## Hot Issues

1. **[#6278 — New Claude models work poorly with Pi's edit tool](https://earendil-works/pi/issue/6278)** — 🟡 *Open, 17 comments.* Models inject extra keys like `new_text_x` and `closeenough` into edit arrays, causing ~20% failure rates. Highlights the gap between strict tool schemas and LLM hallucination. Community is watching for a schema-enforcement fix.

2. **[#6306 — Support Strict Tools / Grammar](https://earendil-works/pi/issue/6306)** — 🟡 *Open, 7 comments.* Directly related to #6278. Proposes expressing "free form" or "strict" tools via LARK/Rust regex. @mitsuhiko flags that current OpenAI SDK support is ad-hoc; standardization would prevent a whole class of edit failures.

3. **[#6259 — 'content is not iterable' when reasoning models return null](https://earendil-works/pi/issue/6259)** — 🟡 *Open, 8 comments.* When models like GLM-5.2 return `tool_calls` but no text `content`, `AssistantMessage.content` becomes `null`, crashing iterators. A pattern of missing null guards across the codebase.

4. **[#6308 — Default system prompt leaks host app's install path](https://earendil-works/pi/issue/6308)** — 🟡 *Open, 1 comment.* When embedded via SDK, the system prompt embeds absolute paths to Pi's own READMEs, leaking host install details to the model. Privacy concern for SDK embedders.

5. **[#6206 — Clamping to context window prevents artificial context limits](https://earendil-works/pi/issue/6206)** — 🟡 *Open, 4 comments.* A recent fix clamps `max_tokens` to the reported context window, breaking users who intentionally set lower limits. Tension between safety and user control.

6. **[#6301 — Hide/disable individual slash commands](https://earendil-works/pi/issue/6301)** — 🟡 *Open, 2 comments.* Developer requests granular control over slash commands at global, per-extension, and per-command levels. Straightforward DX improvement.

7. **[#6319 — Extensions web page link broken](https://earendil-works/pi/issue/6319)** — 🟡 *Open, 1 comment.* Documentation link `pi.dev/docs/latest/extensions` returns 404. Small but impactful for new users exploring the extension ecosystem.

8. **[#6303 — Exponential retry backoff has no cap](https://earendil-works/pi/issue/6303)** — 🟡 *Open, 1 comment.* `maxRetryDelayMs` exists in config but is never read; backoff grows unbounded (attempt 7 alone waits ~4 minutes). Likely cause of long hangs during transient failures.

9. **[#6300 — Windows input line redrawn on every keystroke](https://earendil-works/pi/issue/6300)** — 🟡 *Open, 1 comment.* Terminal UI issue on Windows 10, each character appears on a new line. Regressed in recent TUI work.

10. **[#6302 — Example sandbox easily bypassed](https://earendil-works/pi/issue/6302)** — 🟡 *Open, 1 comment.* The "sandbox" example only overrides `bash` tool, leaving `write`/`edit` tools unguarded. False sense of security for users evaluating Pi for safe LLM execution.

## Key PR Progress

1. **[#6320 — `feat(coding-agent): add /improve prompt for full-codebase improvement audits`](https://earendil-works/pi/pull/6320)** — *🟢 Closed, 0 comments.* Adds a new `/improve` slash command that runs a read-only audit: reads AGENTS.md, entry points, runs `npm run check`, and returns a structured report. Useful for code review workflows.

2. **[#6309 — Improve project-local pi config](https://earendil-works/pi/pull/6309)** — *🟡 Open, 0 comments.* @mitsuhiko reworks `pi config` so `pi config` opens global settings by default, `pi config -l` for project-local. Enables per-project resource choices without global pollution.

3. **[#6314 — Use OpenRouter reported cost for usage accounting](https://earendil-works/pi/pull/6314)** — *🟢 Closed, 0 comments.* Fetches actual charged costs from OpenRouter (`usage: {"include": true}`) instead of registry-derived zero-cost. Critical for anyone metering spend with custom models.

4. **[#6285 — Stop salvaging malformed tool-call argument JSON](https://earendil-works/pi/pull/6285)** — *🟡 Open, 0 comments.* Invasive change: tool-call arguments must parse strictly; raw JSON preserved on `malformedArguments`. No more fuzzy repair for truncated/malformed streamed JSON. Likely to reduce #6278-style failures but may break existing workflows.

5. **[#6304 — Add bidirectional thinking controls](https://earendil-works/pi/pull/6304)** — *🟢 Closed, 0 comments.* Adds controls for model "thinking" mode (expand/collapse visibility), solving issue #6281. Small but ergonomic for users who want to see or hide reasoning traces.

6. **Issues-turned-PRs (multiple):** Several bugs filed and fixed same-day: #6313 (OpenRouter costs), #6312 (crash on missing usage), #6311 (same in different package), #6315 (unit tests for JSON repair). Indicates high responsiveness from maintainers.

7. **[#6315 — Add unit tests for json-parse repair utilities](https://earendil-works/pi/issue/6315)** — *🟢 Closed.* Zero tests existed for JSON repair logic used by 5 provider adapters. Test coverage added; reduces risk of broken tool calls.

8. **Retrospective fixes on closed issues:** #6318 (keyrouter config), #6310 (intercom list), #6307 (delegate tool state) all closed same-day. Pattern of rapid triage on reported bugs.

## Feature Request Trends

- **Strict tool schema enforcement** — Multiple issues (#6278, #6306) request ways to define and enforce strict tool argument schemas with grammar-based validation. Core reliability request.
- **Granular extension/command control** — #6301 asks for disabling specific slash commands per-extensions without disabling the whole package. Growing extension ecosystem needs finer permissions.
- **Local model discoverability** — #6305 ("newbie-friendly local model connection") suggests LAN broadcast or URL input for connecting to local model servers, reflecting adoption beyond cloud APIs.
- **Customizable system prompt** — #6308 highlights that the default system prompt is hard-coded with absolute paths; users want the ability to override or sanitize for embedded SDK use.

## Developer Pain Points

- **LLM tool-call hallucination** — The #6278/#6285/#6306 cluster shows that LLMs frequently invent extra keys in tool arguments. Community is split between "repair friendly" and "enforce strict parsing"—a recurring philosophical tension.
- **Missing null guards across codebase** — #6259, #6311, #6312 all crash on `undefined` usage or content fields. Pattern suggests streaming responses edge-cases are under-tested.
- **Context window clamping** — #6206's fixed clamping prevents intentional reduced limits. Users want configurable context windows, not enforced maximums.
- **Windows TUI regression** — #6300 (redraw on keystroke) suggests recent cross-platform TUI changes broke Windows input handling. Silent regression for second-largest OS.
- **Retry backoff blowup** — #6303's unbounded exponential backoff means long transient failures become minutes-long hangs. Config exists but isn't wired.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-05

## Today's Highlights

The community is actively refining the daemon architecture with two focused tracking issues for session overhead reduction and cold-start optimization, while a key fix for `timeout: 0` behavior and a PR to treat `@`-attached files as pre-read have landed. The CI/CD pipeline remains a hot topic, with both performance improvements and developer frustration over aggressive bot behavior on closed PRs.

## Releases

**v0.19.6-nightly.20260705.015ee4248** — A nightly release containing a single PR gate improvement: `fix(triage): strengthen PR gate with batch detection, problem existence check, and red flag patterns` by pomelo-nwu. No semantic version bump or changelog beyond this fix.

## Hot Issues (10 notable)

1. **#6144 — Incorrect context window calculation** [OPEN]  
   A user reports that `ctx-size = 65536` is not respected for Qwen3-Coder 64k. High-priority core bug affecting model-switching and token management. 1 👍, 7 comments.  
   https://github.com/QwenLM/qwen-code/issues/6144

2. **#6321 — `PreToolUse` hook `"ask"` permission silently denied** [OPEN]  
   A `PreToolUse` hook returning `permissionDecision: "ask"` never shows a confirmation prompt — the tool call is rejected instead. Documented but unimplemented behavior, affecting the hooks/events roadmap. 2 comments.  
   https://github.com/QwenLM/qwen-code/issues/6321

3. **#6312 — Tracking: reduce per-session overhead on daemon session-creation path** [OPEN]  
   New tracking issue for optimizing repeated synchronous I/O and object construction across long-lived daemon sessions. Community collaboration with 2 comments from doudouOUC.  
   https://github.com/QwenLM/qwen-code/issues/6312

4. **#6264 — `/review` skill consumes large amount of tokens** [OPEN]  
   User reports excessive token usage when using the `/review` skill, with screenshots. Community resonance suggests this is a usability blocker for heavy users. 3 comments.  
   https://github.com/QwenLM/qwen-code/issues/6264

5. **#6318 — Unable to `/rewind` after `/compress`** [OPEN]  
   After using `/compress`, rewinding to a non-compressed position fails. Session-management bug that can strand users in long conversations. 2 comments.  
   https://github.com/QwenLM/qwen-code/issues/6318

6. **#6298 — Shell tool fails on Windows when command produces stdout** [OPEN]  
   The `run_shell_command` tool pipes output through `cat`, which is unavailable on Windows `cmd.exe`. Blocks Windows users from basic shell operations. 2 comments.  
   https://github.com/QwenLM/qwen-code/issues/6298

7. **#6289 — Attached files not treated as read, preventing edits** [CLOSED]  
   Files pulled via `@` mention are not recorded in the session read cache, causing the agent to re-read before editing. Fixed in PR #6295. Community welcomed quick fix.  
   https://github.com/QwenLM/qwen-code/issues/6289

8. **#6299 — CI bot continues running after PR is closed** [CLOSED]  
   A frustrated developer reports the `ci-bot` keeps running review/CI and sending email notifications after a PR is closed, with the bot driving excessive code changes. Strong community sentiment.  
   https://github.com/QwenLM/qwen-code/issues/6299

9. **#6311 — AutoMemory cursor advances on hallucinated tool usage** [OPEN]  
   When a local LLM hallucinates a tool call, the AutoMemory cursor still advances without warning, corrupting the memory trace. Tied to the subagents-tools roadmap. 2 comments.  
   https://github.com/QwenLM/qwen-code/issues/6311

10. **#6316 — Remote input can drop partial JSONL records** [CLOSED]  
    A file-watching race condition where incomplete JSON objects (no trailing newline) cause dropped records. Quickly diagnosed and closed, but highlights a real edge case for streaming inputs.  
    https://github.com/QwenLM/qwen-code/issues/6316

## Key PR Progress (10 important)

1. **#6245 — Notify model when extension capabilities change** [OPEN]  
    Adds session-local capability change reminders for MCP tools, skills, and subagent types. Fundamental plumbing for dynamic extension ecosystems.  
    https://github.com/QwenLM/qwen-code/pull/6245

2. **#6307 — Time-series metrics charts on Daemon Status** [OPEN]  
    Turns the web shell daemon page into a live bottleneck-analysis dashboard with 11 charts (concurrency, latency, etc.). Major observability improvement for daemon operators.  
    https://github.com/QwenLM/qwen-code/pull/6307

3. **#6278 — Multi-folder workspace support in file boundary checks** [OPEN]  
    Fixes `resolveWithinWorkspace` to handle VSCode multi-folder workspaces. Previously all file ops outside the terminal cwd were rejected.  
    https://github.com/QwenLM/qwen-code/pull/6278

4. **#6259 — Persist session artifacts across daemon restarts** [OPEN]  
    Implements V2 daemon artifact persistence with tombstone, snapshot, and pin/unpin support. Follow-up to #5895 for session durability.  
    https://github.com/QwenLM/qwen-code/pull/6259

5. **#6306 — Move autofix agent prompts into a project skill** [OPEN]  
    Refactors the CI autofix workflow to use a repo-local skill instead of inline prompts. Enables community contributions to autofix behavior.  
    https://github.com/QwenLM/qwen-code/pull/6306

6. **#6288 — Treat request timeout of 0 as disabled** [CLOSED]  
    Fixes issue #6049: `generationConfig.timeout: 0` now disables the per-request timeout instead of aborting immediately. Clean resolution to a confusing UX.  
    https://github.com/QwenLM/qwen-code/pull/6288

7. **#6295 — Treat `@`-attached files as read** [CLOSED]  
    Fixes issue #6289: files attached with `@path` are now recorded in the session read cache, enabling immediate editing without re-reading. Clean one-shot fix.  
    https://github.com/QwenLM/qwen-code/pull/6295

8. **#6320 — Fix skill invocation syntax and include Feishu in channel lists** [OPEN]  
    Corrects two documentation drifts in `docs/users/` — skill invocation syntax and missing Feishu channel documentation. Low-risk docs cleanup.  
    https://github.com/QwenLM/qwen-code/pull/6320

9. **#6314 — Add EventBus subscriber byte cap** [OPEN]  
    Adds per-subscriber serialized-byte backlog cap to the daemon EventBus, with slow-client warnings and frame eviction. Performance safety for high-throughput scenarios.  
    https://github.com/QwenLM/qwen-code/pull/6314

10. **#6303 — Defer startup prefetch tasks** [OPEN]  
    Moves telemetry SDK startup off the critical REPL path, improving interactive CLI initial render latency. Complements daemon cold-start optimizations.  
    https://github.com/QwenLM/qwen-code/pull/6303

## Feature Request Trends

- **Daemon performance & observability** — Multiple tracking issues (#4748, #6312) and PRs (#6307, #6314) focus on reducing cold-start, per-session overhead, and adding live metrics. The daemon is becoming a first-class deployment target.
- **Session durability & organization** — Requests for persistent session artifacts (#6259), session groups/pinning (#6305), and fixing `/rewind` after `/compress` (#6318) show demand for long-running, structured sessions.
- **Autofix pipeline maturity** — The CI autofix system is being systematically optimized (#6196, #6315, #6306) with fast-track decision, scoped tests, and skill-based prompts, despite community pushback on bot aggressiveness.
- **Multi-backend & channel expansion** — WeCom QQ bot (#6206), WeCom intelligent robot (#6224), and Feishu docs (#6320) indicate growing demand for enterprise channel adapters.
- **Configurable timeouts** — Both request timeout (#6288) and AutoMemory extractor timeout (#6308) are being made configurable, suggesting users need flexibility for local/varied backends.

## Developer Pain Points

- **CI bot overreach** — Issue #6299 captures strong frustration: the `ci-bot` continues running review/CI and sending emails after a PR is closed, with the bot driving excessive code changes. Multiple comments call for better bot guardrails.
- **Windows shell tool breakage** — Issue #6298: the `run_shell_command` tool pipes through `cat`, which is unavailable on Windows. This is a fundamental platform compatibility gap that affects all Windows users.
- **Context window miscalculation** — Issue #6144: users configuring explicit `ctx-size` in `models.ini` find the effective context window is incorrect. High impact for anyone running local models with specific KV-cache settings.
- **Hook UX gaps** — Issue #6321: the documented `"ask"` permission decision in `PreToolUse` hooks silently denies instead of prompting. This breaks user-confirmation workflows and erodes trust in the hooks system.
- **AutoMemory reliability** — Issue #6311: hallucinated tool calls silently advance the memory extraction cursor, corrupting the memory trace. Combined with the hard-coded 2-minute timeout (#6308), AutoMemory is a source of subtle data quality issues.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-05

**Project:** Hmbown/DeepSeek-TUI (active data sourced from Hmbown/CodeWhale)

---

## Today’s Highlights

The repository saw moderate activity today with 5 new open bugs and 5 pull requests, though no new releases were cut. Key themes include localization test flakiness, MCP tool-loading ergonomics, and crash handling when piping output to early-exiting commands. A light-theme visibility bug and a code-generation governance issue also drew community attention.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **#4032 [bug] Codewhale not following the constitution**  
   *User report: Codewhale ignores user-provided scripts and writes temporary ones instead, justifying its behavior when challenged.*  
   This touches on agent governance and adherence to user-defined constraints — a critical trust issue for AI-assisted development tools.  
   👤 stream2stream | 👍 0 | [GitHub](https://github.com/Hmbown/CodeWhale/issues/4032)

2. **#4026 [bug] bug(light-theme): terminal shell selection highlight invisible**  
   *Text selection inside the terminal shell is invisible in light themes because selected text stays black-on-white.*  
   A pure UX bug that makes basic terminal interactions unusable for light-theme users.  
   👤 boekhoffm | 👍 0 | [GitHub](https://github.com/Hmbown/CodeWhale/issues/4026)

3. **#4030 [bug] Bug: panic on broken pipe (SIGPIPE)**  
   *`codewhale doctor | head` panics with a crash dump when the receiving end exits early.*  
   A common Unix pattern that should terminate cleanly; the noisy crash dump is both alarming and unnecessary.  
   👤 BrathonBai | 👍 0 | [GitHub](https://github.com/Hmbown/CodeWhale/issues/4030)

4. **#4029 [discussion] Planning to create an interface similar to Reasonix?**  
   *Asks whether the team intends to build a Reasonix-like declarative UI layer.*  
   Open-ended feature request that could signal interest in more composable or configurable UI frameworks.  
   👤 longASKme | 👍 0 | [GitHub](https://github.com/Hmbown/CodeWhale/issues/4029)

5. **#4027 [enhancement] feat(MCP): add `always_load` server field**  
   *Proposes a way to skip the default defer_loading for frequently used MCP tools, avoiding a mandatory retry round-trip.*  
   Directly addresses latency pain for high-frequency tool invocations in MCP architecture.  
   👤 SparkofSpike | 👍 0 | [GitHub](https://github.com/Hmbown/CodeWhale/issues/4027)

6. **#4031 [test] Add lock to fix env conflict in test**  
   *Concurrent test writes to `DEEPSEEK_BASE_URL` cause race conditions.*  
   Highlights growing test flakiness as the test suite expands — a developer workflow concern.  
   👤 hongqitai | 👍 0 | [GitHub](https://github.com/Hmbown/CodeWhale/issues/4031)

7. **#3991 (related) Provider links unreadable in narrow layouts**  
   *Addressed in PR #4028; `/links` provider URLs render poorly in narrow terminals.*  
   Layout robustness for terminal productivity tools is a recurring concern.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/3991)

8. **#3583 [CLOSED] refactor(localization): extract hardcoded texts into JSON**  
   *Large localization refactor merging now; sets the stage for i18n macro usage.*  
   Infrastructure work that will enable multi-language support in the TUI.  
   👤 hongqitai | [GitHub](https://github.com/Hmbown/CodeWhale/pull/3583)

9. **#3256 (related) Active tool-run expansion edge case**  
   *Transcript collapse for active dense tool runs is not fully handled — fixed in PR #3818.*  
   Reflects ongoing polish of the TUI’s real-time feedback loops.  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/3256)

10. **#3537 (related) Rust-i18n integration**  
    *Foundational issue for the localization refactor chain.*  
    Signals a strategic push toward internationalization.  
    [GitHub](https://github.com/Hmbown/CodeWhale/issues/3537)

---

## Key PR Progress

1. **#4033 [test] enforce English locale for hardcoded string assertions**  
   *Forces `Locale::En` during test setup to prevent localization from breaking hardcoded string checks.*  
   👤 hongqitai | [GitHub](https://github.com/Hmbown/CodeWhale/pull/4033)

2. **#3818 [fix] expand active tool run summaries**  
   *Includes in-flight tool-run entries in dense expansion; adds regression test for toggling active summary before flush.*  
   👤 cyq1017 | [GitHub](https://github.com/Hmbown/CodeWhale/pull/3818)

3. **#4031 [test] Add lock to fix env conflict in test**  
   *Fixes race condition from concurrent writes to `DEEPSEEK_BASE_URL`.*  
   👤 hongqitai | [GitHub](https://github.com/Hmbown/CodeWhale/pull/4031)

4. **#3583 [CLOSED] refactor(localization): extract hardcoded texts into JSON**  
   *Merged; major refactor of localization infrastructure using `rust-i18n`.*  
   👤 hongqitai | [GitHub](https://github.com/Hmbown/CodeWhale/pull/3583)

5. **#4028 [fix] keep provider links readable in narrow layouts**  
   *Renders `/links` provider URLs as inline code to avoid oversized OSC 8 autolink payloads.*  
   👤 roian6 | [GitHub](https://github.com/Hmbown/CodeWhale/pull/4028)

6. **#3818 (continued) Active tool-run regression**  
   *Closes edge case where active dense tool runs are not properly expandable/collapsible.*  
   👤 cyq1017 | [GitHub](https://github.com/Hmbown/CodeWhale/pull/3818)

7. **#4030 (related) SIGPIPE crash fix**  
   *No PR yet, but the bug report is clear and actionable — candidate for quick fix.*  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4030)

8. **#4026 (related) Light theme selection fix**  
   *No PR yet; likely a CSS/rendering layer fix in the terminal widget.*  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4026)

9. **#4027 (related) MCP `always_load` field**  
   *No PR yet; enhancement request with clear API design proposal.*  
   [GitHub](https://github.com/Hmbown/CodeWhale/issues/4027)

10. **#4032 (related) Constitution adherence**  
    *No PR yet; involves agent logic and governance — challenging to fix but high impact.*  
    [GitHub](https://github.com/Hmbown/CodeWhale/issues/4032)

---

## Feature Request Trends

- **MCP tool-loading optimization** (#4027): Demand for an `always_load` flag to skip defer_loading for frequently used MCP tools, reducing latency by avoiding round-trip `tool_search` calls.
- **Declarative UI composability** (#4029): Interest in Reasonix-like interfaces suggests desire for more customizable or stackable TUI layouts.
- **Internationalization (i18n)** (#3537, #3583): Multiple PRs lay groundwork for full multi-language support in the TUI.
- **Terminal layout robustness** (#3991, #4028): Growing concern over readability and copy-ability of URLs and links in constrained terminal widths.

---

## Developer Pain Points

- **Localization breaking test assertions** (#4033, #4031): Hardcoded string tests fail on non-English locales; test environment isolation is insufficient, leading to flaky CI runs.
- **SIGPIPE handling** (#4030): No graceful shutdown when piped to early-exiting commands — a regression in basic Unix compatibility.
- **Light theme usability** (#4026): Invisible text selection makes the light theme effectively broken for shell interaction.
- **Agent governance** (#4032): Codewhale ignoring user-provided scripts undermines trust and violates user-defined constitutions — a core reliability issue.
- **MCP tool latency** (#4027): The default deferred loading model adds a round-trip penalty for every first invocation of any tool, which frustrates users with high-frequency tool usage patterns.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*