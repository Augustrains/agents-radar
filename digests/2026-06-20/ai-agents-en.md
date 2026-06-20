# OpenClaw Ecosystem Digest 2026-06-20

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-20 02:03 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

Here is the OpenClaw project digest for June 20, 2026.

---

## OpenClaw Project Digest — 2026-06-20

### 1. Today's Overview
Project activity remains at a **critical high**, with 500 issues and 500 PRs updated in the last 24 hours, reflecting sustained community engagement and developer velocity. While new feature development continues, the project is currently **struggling with a severe stability debt**: a majority of the most-commented issues are P0/P1 regressions involving memory leaks, session isolation failures, and data loss. The release of `v2026.6.9-beta.1` yesterday offers a mix of delivery fixes but does not directly address the most critical memory or crash-loop bugs, indicating ongoing triage. Overall, the project is **healthy in terms of throughput** but **fragile in terms of reliability**, with users experiencing recurring runtime failures.

### 2. Releases
**New Version:** `v2026.6.9-beta.1` (openclaw 2026.6.9-beta.1)

**Key Changes:**
- **Richer Telegram Delivery:** Telegram messages now render with proper HTML, markdown, sticker paths, and progress drafts. Improved handling for mentions and spooled delivery paths. (PRs #93286, #93164, #93124, #93364, #9313)

**Migration Notes:**
No breaking changes or specific migration steps were mentioned in the current release notes. However, given the high volume of session-state and SQLite migration issues reported in the community (see Bugs & Stability), users are advised to back up their `openclaw.json` and session history before upgrading.

### 3. Project Progress
Today, **51 pull requests were merged or closed**, a high number indicating active resolution of pending work.

**Highlights of merged/closed work:**
- **Claude-CLI Permission Schema:** A critical fix (PR #95174, PR #95172) was merged to address a breaking change in Claude Code 2.1.x, where the `PermissionResult` schema was tightened, causing all tool approvals to fail silently. The fix restores the correct `updatedInput` shape.
- **Anthropic Socket Retry:** A fix for `UND_ERR_SOCKET` keep-alive failures was delivered (PR #95176), preventing silent mid-turn model switching caused by stale pooled sockets in Node.js undici.
- **Mobile Exec Approvals:** A new fix (PR #95175) now routes mobile chat-triggered exec approvals to the correct reviewer device, preventing cross-device approval confusion.
- **False-Positive Doctor Warnings:** A fix (PR #95177) suppresses a false-positive warning from `openclaw doctor` that incorrectly flagged local embeddings as unready when a gateway probe was skipped.
- **Plugin Update Alignment:** The `openclaw plugins update --all` command now correctly syncs official plugins and respects the configured `update.channel` (fix via PR #94084).
- **Documentation:** A new Kubernetes manifest path was added (PR #93544), moving away from the previously confusing Helm-focused guide.

### 4. Community Hot Topics
The following issues and PRs are generating the most community discussion (by comments/reactions).

- **[Issue #88838 (31 comments)] Track core session/transcript SQLite migration via accessor seam** - [Link](https://github.com/openclaw/openclaw/issues/88838)
  - **Analysis:** This is a deep, architectural discussion on how to migrate the core session/transcript runtime state to SQLite using a "branch-by-abstraction" pattern. It is a high-risk, high-reward feature that aims to prevent a single massive, destabilizing rewrite. The 31 comments suggest careful code review and maintainer coordination, reflecting the project's awareness of preventing future regressions.

- **[Issue #91588 (13 comments)] Critical: Gateway Memory Leak (350MB to 15.5GB)** - [Link](https://github.com/openclaw/openclaw/issues/91588)
  - **Analysis:** **The single most critical stability issue in flight.** A P0 diamond lobster issue. Users report that the gateway process grows uncontrollably over days, leading to OOM kills and crash loops. The 13 comments indicate active investigation into heap allocation patterns. This is a top priority for the maintainers.

- **[Issue #85333 (13 comments)] `openclaw doctor --fix` 4-5x slower regression** - [Link](https://github.com/openclaw/openclaw/issues/85333)
  - **Analysis:** A significant performance regression in a core maintenance command. The user demonstrated a reproducible path-traversal bottleneck. The 13 comments show community effort in profiling and isolating the root cause in the session snapshot logic.

- **[Issue #63829 (10 comments)] Per-agent memory-wiki vault configuration** - [Link](https://github.com/openclaw/openclaw/issues/63829)
  - **Analysis:** A high-demand feature for multi-agent setups. Users want isolated knowledge bases per agent, rather than a single shared vault. The 9 upvotes indicate strong community interest.

### 5. Bugs & Stability
The project is facing a **stability crisis** with numerous high-severity bugs open, many linked to a common root cause of session-state corruption, memory pressure, and delivery failures.

**Critical (P0/P1, active):**
- **Gateway Memory Leak (Issue #91588):** RSS grows 44x over days to 15.5GB, causing OOM kills. *Fix PR status:* Unknown, actively under investigation.
- **EPERM on Windows (Issue #78640):** Persistent file permission errors on Windows 11 during memory index operations. *Fix PR status:* Open (seeking review).
- **Silent Memory File Deletion (Issue #84882):** The `memory-core` `Dreaming` pipeline silently deletes daily memory files (`memory/YYYY-MM-DD.md`). *Fix PR status:* Open, linked PR pending.

**High (P1, active regressions):**
- **Matrix Channel Broken (Issue #90325):** `TypeError: Cannot read properties of undefined (reading 'run')` on every inbound message in v2026.6.1. *Fix PR status:* Needs live repro.
- **Subagent Delivery Failure (Issue #90840):** Raw worker output delivered to user instead of a parent summary in QQBot sessions. *Fix PR status:* Open.
- **Cron Store Migration Data Loss (Issue #90378):** Migration from JSON to SQLite silently changes defaults, causing channel delivery errors. *Fix PR status:* Open, linked PR.
- **Event Loop Saturation (Issue #84771):** Synchronous startup prewarm blocks the event loop for 28-64 seconds. *Fix PR status:* Needs live repro.

**Resolved or In-Flight:**
- **Telegram Web Support (Issue #93794, Closed):** A regression causing "Message not supported" on Telegram Web was **closed**, suggesting a fix was successfully applied or the issue was related to a configuration that has been clarified.

### 6. Feature Requests & Roadmap Signals
The community is pushing for several deep architectural changes that will likely define the next major release.

- **Topical Session Families (Issue #90916):** Users want "topic-session families" that allow one assistant to maintain multiple isolated conversation lanes (e.g., "Work" vs "Personal") while sharing durable memory. This is a fundamental UX shift. *Risk:* High complexity.
- **Per-Channel/Group Model Override (Issue #53638):** A highly requested config feature to assign different LLMs to different Telegram groups or channels without runtime manual overrides. *Predict:* Likely to land in the next minor release (v2026.7.x).
- **Webchat Inline Buttons (Issue #46656):** Parity with Telegram for inline keyboard buttons on the Control UI. *Predict:* Likely for imminent release given the recent Control UI fixes.
- **Per-Agent Memory-Wiki Vault (Issue #63829):** Isolated knowledge bases for multi-agent setups. *Predict:* This is a major feature; it may be gated behind the broader memory-wiki plugin refactor (see PR #93843).

### 7. User Feedback Summary
- **Pain Points:**
  - **Stability Anxiety:** Users are frustrated by recurring OOM crashes (Issue #91588) and session isolation failures (Issue #84903) that block all agents.
  - **Data Loss:** Several users report silent data loss—either from memory files being deleted (Issue #84882) or delivery-recovery failing silently after restarts (Issue #91212).
  - **Configuration Confusion:** The "doctor" tool falsely reports healthy states as broken (Issue #92582), and the Kubernetes documentation was confusing enough to warrant a full rewrite (Issue #91455).
  - **Feature Gaps:** Users want better model selection granularity (Issue #53638) and isolated memory spaces (Issue #63829).

- **Satisfaction Indicators:**
  - The rapid response to the Claude-CLI permission schema breakage (PR #95174, #95172) suggests a responsive developer community.
  - The extensive documentation update for Kubernetes (PR #93544) shows the team is listening to deployment pain points.

### 8. Backlog Watch
The following issues have been open for over a month and have not seen recent maintainer triage, despite high impact:

- **Issue #53638 (Feature: per-channel model override)** - [Link](https://github.com/openclaw/openclaw/issues/53638)
  - **Status:** Open for 3 months. Linked PR is open. *Why it matters:* This is a top-voted feature that is blocking multi-tenant/household deployments.

- **Issue #46656 (Webchat inline buttons)** - [Link](https://github.com/openclaw/openclaw/issues/46656)
  - **Status:** Open for 3 months. *Why it matters:* Parity with Telegram; a fundamental UX gap for Control UI users.

- **Issue #78640 (EPERM on Windows)** - [Link](https://github.com/openclaw/openclaw/issues/78640)
  - **Status:** Open for 45 days, marked `no-stale`. *Why it matters:* Blocks all memory index operations for a significant user base.

**Maintainer Attention Required:**
- **Issue #85333 (`doctor --fix` slowness)** has a clear repro but lacks a `fix-shape-clear` label, indicating the fix strategy is not yet approved.
- **Issue #84882 (Memory file deletion)** remains open with a linked PR, but the PR status is `needs-info`, meaning the maintainers need more data from the reporter before proceeding.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-06-20  
**Scope:** 11 projects in the personal AI assistant / agent open-source ecosystem

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing an **extraordinary development surge**, with six projects showing extremely high activity and three others maintaining moderate momentum. The landscape is bifurcating: mature projects like OpenClaw (500 daily issues/PRs) and IronClaw (30+ PRs/day) are pushing toward production-grade reliability, while smaller projects like PicoClaw and NanoClaw focus on platform expansion and bugfix consolidation. A clear **"Reborn" architectural wave** is sweeping the ecosystem, with IronClaw and to a lesser extent OpenClaw investing heavily in next-generation runtimes that emphasize concurrent execution, multi-platform ingress, and API compatibility with commercial providers (OpenAI, Claude). The community is signaling strong demand for **cross-model orchestration**, **session persistence**, and **mobile/edge deployment** — areas where the current state of the art remains fragmented across projects.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Today | Health Score | Dominant Activity |
|---|---|---|---|---|---|
| **OpenClaw** | 500 updated | 500 updated | ✅ v2026.6.9-beta.1 | 🟡 Fragile (high throughput, stability crisis) | Bug triage, memory leak investigation |
| **Hermes Agent** | 50 updated | 50 updated | ✅ v0.17.0 (yesterday) | 🟡 Concerning (5 P1 bugs, regression management) | Post-release regression fixes, i18n |
| **IronClaw** | 4 updated | 30 updated | ❌ | 🟢 Active & Shipping | Reborn architecture feature stack, CI optimization |
| **CoPaw** | 11 updated | 17 updated | ❌ | 🟢 Good | ChromaDB fix, DeepSeek freeze, Zhipu provider |
| **NanoBot** | 10 touched | 33 updated | ❌ | 🟢 Good | Feature iteration (SuspendTurn, subagent aggregation) |
| **ZeroClaw** | 50 active | 49 open | ❌ | 🟡 Moderate (high churn, binary regression) | Discord interaction components, OIDC |
| **PicoClaw** | 4 updated | 7 active | ✅ Nightly (unstable) | 🟡 Stable with debt | Identity parsing, SSRF guard, memory loss bug |
| **NanoClaw** | 0 new | 5 open | ❌ | 🟢 Stable (low activity) | Approval persistence, Discord chunking |
| **NullClaw** | 1 closed | 1 new | ❌ | 🟢 Stable | Android/Termux network fix, Ollama bug resolved |
| **LobsterAI** | 1 new | 0 merged | ✅ 2026.6.18 | 🟢 Stable | Maintenance phase, artifact sharing feature |
| **TinyClaw** | 0 | 0 | ❌ | ⚪ Inactive | — |
| **Moltis** | 0 | 0 | ❌ | ⚪ Inactive | — |
| **ZeptoClaw** | 0 | 0 | ❌ | ⚪ Inactive | — |

**Health Score Key:** 🟢 Good / 🟡 Concern / 🔴 Critical / ⚪ Inactive

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Community Scale:** OpenClaw's 500 daily issue/PR updates dwarfs all competitors (Hermes: 100, IronClaw: 34). This is a 5-15x multiplier in community engagement, reflecting the largest user base and contributor pool.
- **Delivery Infrastructure:** The richest platform-specific features — Telegram HTML/markdown/sticker support, mobile exec approvals, plugin update alignment — are more mature than any peer. Only Hermes Agent matches Telegram richness.
- **Reactive Maintenance:** PRs #95174/#95172 fixed a Claude-CLI permission schema break within 24 hours of detection, demonstrating world-class incident response.

### Technical Approach Differences
- **Monolithic Reference Architecture:** OpenClaw is the "core reference" — it provides a complete, out-of-the-box agent with memory, plugins, multi-channel delivery. Projects like IronClaw are building modular, API-compatible runtimes (OpenAI Responses), while NanoBot emphasizes lightweight multi-provider abstraction.
- **Plugin Ecosystem:** OpenClaw's plugin update system (`openclaw plugins update --all`) and memory-wiki vault are more structured than nanoBot's tool-based extensions or PicoClaw's configuration-driven model.

### Community Size Comparison
| Metric | OpenClaw | Runner-Up |
|---|---|---|
| Daily Issue/PR Volume | 500+ | Hermes (100) |
| Contributors (v0.17) | N/A | Hermes (245) |
| Stale Backlog Items | ~3 long-standing | ZeroClaw (~2), CoPaw (~1) |
| First-time Contributors (24h) | High | CoPaw (4 new contributors) |

**Conclusion:** OpenClaw has the largest absolute community but is struggling with **stability debt** (memory leaks, session corruption) that smaller, more focused projects are avoiding. Hermes Agent has higher contributor density per feature shipped.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging **independently across multiple projects**, indicating ecosystem-wide demand:

| Requirement | Projects Involved | Specific Needs |
|---|---|---|
| **Cross-Model Orchestration** | LobsterAI (#2180), NanoBot (#4419, #4414), Hermes (#32159), CoPaw (#5327) | Users want agents that coordinate multiple models for subtasks, with fallback chains and aggregated results |
| **Session Persistence / Isolation** | OpenClaw (#88838, #63829), ZeroClaw (#6893), NanoBot (#4246), PicoClaw (#3150) | Common pain: memory loss, session corruption, lack of isolated conversation lanes per topic/agent |
| **Approval & Permission UX** | IronClaw (#5088, #5062), OpenClaw (#95175), NanoClaw (#2820), Hermes (#49283) | Improving tool approval clarity, cross-device routing, per-tool configurations, silent failures |
| **Mobile / Edge Deployment** | PicoClaw (#2472), NullClaw (#966/#868), ZeroClaw (#7996), CoPaw (#5329) | Android/Termux support, Windows path issues, responsive web UIs, temp file management on constrained hardware |
| **Multi-Platform Ingress** | IronClaw (#5093/#5100), OpenClaw (#90325 Matrix), ZeroClaw (#7787 Discord/Slack), NanoBot (#4413 Telegram) | Simultaneous connectivity across Slack, Telegram, Discord, Matrix, Signal, Feishu, webhooks |
| **Memory Scaling & Compaction** | OpenClaw (#91588 memory leak), CoPaw (#4795 37GB ChromaDB), Hermes (#39691 tool-level compression), ZeroClaw (#5844 memory dominance) | Uncontrolled memory growth is the #1 stability threat ecosystem-wide |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architectural Distinction |
|---|---|---|---|
| **OpenClaw** | Full-featured personal assistant | Power users, self-hosters | Monolithic reference; richest plugin ecosystem; largest community |
| **Hermes Agent** | Desktop-first "Reach" assistant | Desktop users, multiplatform | v0.17 "The Reach": desktop app, 15-language i18n, projects backend |
| **IronClaw** | Reborn next-gen agent runtime | Developers, API-compatible services | OpenAI Responses API drop-in; concurrent execution; Rust-based infrastructure |
| **CoPaw** | Agent collaboration with memory | Multi-agent collaboration teams | ChromaDB-based memory; agent office UI; Zhipu/DeepSeek support (Chinese ecosystem) |
| **NanoBot** | Lightweight multi-provider agent | Developers, multi-model users | Provider abstraction; MCP transport; subagent orchestration; reasoning effort escalation |
| **ZeroClaw** | High-performance Rust agent | Performance-sensitive deployers | Rust-based; OIDC auth; multi-DB backends; Discord-native interactions |
| **PicoClaw** | Lightweight embedded agent | Embedded/RISC-V users | Minimal footprint; nightly builds; Windows/Matrix compatibility |
| **NanoClaw** | Enterprise agent hierarchy | Multi-tenant organizations | Parent permission inheritance; Apple Container runtime; approval audit trails |
| **NullClaw** | Zig-based minimalist agent | Build-from-source enthusiasts | Zig ecosystem; Ollama/local model focus; Android/Termux support |
| **LobsterAI** | Document generation & orchestration | Productivity users, non-programmers | Multi-format artifact sharing (Word, PPT, Excel); "AI Collaborator" vision |
| **TinyClaw / Moltis / ZeptoClaw** | Inactive — no recent development | — | Dormant |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (High Risk/High Reward)
- **OpenClaw** — Massive throughput, but stability crisis (P0 memory leak, data loss bugs). Critical mass of community fixes, but core maintainers are stretched.
- **Hermes Agent** — v0.17 shipped with impressive scope (800 PRs, 245 contributors), but 5 P1 bugs and Gemma 4 regression recovery undermines confidence. Users re-filing bugs because fixes don't stick.
- **IronClaw** — Most disciplined feature delivery: 12 PRs merged/closed in 24h on Reborn. Strong CI hygiene (mold linker, sccache). Nightly E2E failure (#4108) is the main quality risk.

### Tier 2: Stabilizing (Core Fixes + Platform Expansion)
- **CoPaw** — Excellent balance: 6 PRs merged addressing critical bugs (ChromaDB, cron misfire, DeepSeek freeze), 4 new contributors. Likely v1.1.13 patch imminent.
- **NanoBot** — Active feature iteration (SuspendTurn, subagent aggregation, cron model presets) with well-maintained issue tracker (6/10 issues closed). Stream stall regression (#4013) and heartbeat semantics are top pain points.
- **ZeroClaw** — High-velocity feature landing (Discord interactions, OIDC) but binary regression (#7787) creates immediate user friction. Need to consolidate v0.8.x before v0.9.0.

### Tier 3: Modest Activity
- **PicoClaw** — Nightly release pipeline healthy, but 3 critical PRs stale for 12+ days. Memory loss bug (#3150) needs urgent triage.
- **NanoClaw** — 5 PRs in review, no new bugs. Lowest churn in the active set. Parent permission inheritance (#2605) aging for 27 days.
- **NullClaw** — One bug fixed (Ollama incomplete answers), one new PR (Android network fix). Tiny but focused.
- **LobsterAI** — Maintenance phase after v2026.6.18 release. Single feature request (#2180) signals next direction.

### Tier 4: Inactive
- **TinyClaw, Moltis, ZeptoClaw** — No activity in 24h. Likely dormant or in extended hiatus.

---

## 7. Trend Signals for AI Agent Developers

### Strong Signal (Appearing in 4+ Projects)
1. **Memory/Context Management is the #1 Reliability Problem** — Uncontrolled growth (37GB ChromaDB), silent deletion, agent "amnesia" (PicoClaw #3150), and dominance over user intent (ZeroClaw #5844) are the most critical issues across the ecosystem. Any agent development framework should prioritize bounded memory with compaction and user-visible management.

2. **Multi-Model Orchestration is the #1 Feature Request** — Users want agents that can intelligently route sub-tasks to different models, escalate reasoning effort, aggregate outputs, and maintain fallback chains. Projecting this onto a single LLM call is insufficient for production agents.

3. **Production-Grade Authentication & Authorization** — OIDC (ZeroClaw), per-tool permissions (IronClaw, NanoClaw), credential proxies (Hermes), and cross-device approval routing (OpenClaw) are converging on a standard pattern: agents need enterprise-grade credential management to be deployable beyond individual use.

### Weak Signal (Appearing in 1-2 Projects but Potentially Transformative)
4. **AI Self-Evolution / Skill Extraction** — IronClaw PR #5061 (skill extraction from successful turns) and LobsterAI's "AI Collaborator" vision (#2180) represent a radical shift: agents that improve their own knowledge base over time without human programming. This is where the ecosystem may differentiate from commercial assistants (ChatGPT, Claude).

5. **Edge/Native Deployment** — Apple Container (NanoClaw), Android/Termux (NullClaw #868/#966), RISC-V (PicoClaw core), and system tray minimization (CoPaw #5326) signal demand for agent software that runs reliably on low-power, offline, or non-cloud environments. This is a gap that commercial providers cannot easily fill.

### Developer Implications
- **Stability first, features second**: Every high-activity project is shipping regressions alongside new features. Developers building on these projects should budget for frequent patch releases and maintain rollback capability.
- **Cross-platform is non-negotiable**: The ecosystem has users on Windows, macOS, Linux, Android, Termux, and potentially RISC-V. A deployment that works on only one OS will fragment the community.
- **API compatibility with commercial providers is table stakes**: OpenAI Responses API (IronClaw), Claude Code permission schema (OpenClaw), and Gemini fallback chains (NanoBot) are all required integration points. Projects ignoring these risk isolation from the broader LLM ecosystem.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-20

## Today's Overview
NanoBot shows **high development activity** with 33 pull requests updated in the last 24 hours and 10 issues touched. The project is in a **rapid feature iteration phase** following the v0.2.x releases, with maintainers actively merging contributions — 19 PRs were merged or closed today. The community is highly engaged, submitting sophisticated feature requests around reasoning models, heartbeat reliability, and subagent orchestration. The issue tracker is well-maintained, with most bugs receiving prompt closure (6 of 10 updated issues were closed). Notably, there were **no new releases** today, suggesting the team may be accumulating features for a v0.3.0 milestone.

## Releases
**No new releases today.** The latest available version remains v0.2.x (referenced as v0.2.1 in recent issues). Users migrating from v0.1.5post2 should note the stream stall regression (see #4013) and the heartbeat behavior change (see #4410) before upgrading.

## Project Progress
**19 PRs were merged or closed today**, spanning bug fixes, infrastructure hardening, and platform support:

- **MCP/Transport fixes**: `#4230` (closed) sets proper httpx timeouts for streamable HTTP transport, preventing indefinite hangs; `#4342` (closed) fixes Feishu WebSocket card rendering with proper nested list handling
- **Session management**: `#4246` (closed) prevents history revival by ensuring `delete_session` also removes legacy path files
- **Provider fixes**: `#4394` (closed) correctly routes OpenAI image reference edits to `/images/edits` endpoint
- **Tool system improvements**: `#4411` (open) introduces `SuspendTurn` — a sentinel for tools to pause turns for async or human-in-the-loop continuations without producing final messages
- **Infrastructure testing**: `#4417` (open) improves MCP timeout regression tests to use resolvable URLs; `#4393` (open) adds end-to-end git command tests in workspace subdirectories
- **Major overhauls**: `#2655` (closed) delivers a complete Discord channel rewrite with `discord.py 2.x`, slash commands, UI components, and agent tools

## Community Hot Topics
The most discussed items reveal **two major community concerns**:

**1. Fallback model reliability** — Multiple issues cluster around model fallback behavior:
- `#4287` ([bug](https://github.com/HKUDS/nanobot/issues/4287)): Empty model responses not triggering fallback — **2 comments**, resolved
- `#4389` ([feature request](https://github.com/HKUDS/nanobot/issues/4389)): Per-model `contextWindowTokens` needed for fallback models — **2 comments**, resolved
- `#4345` ([bug](https://github.com/HKUDS/nanobot/issues/4345)): Image-strip fallback makes model act as if it saw images it never received, leaking file paths — resolved

The underlying need: users running multiple models (primary + fallbacks) want NanoBot to intelligently handle provider-specific degradation without breaking agent behavior.

**2. Cron/heartbeat delivery semantics** — Two open issues and one PR address this:
- `#4418` ([open](https://github.com/HKUDS/nanobot/issues/4418)): Heartbeat tasks deliver results to wrong channel
- `#4410` ([open](https://github.com/HKUDS/nanobot/issues/4410)): Even with "don't send message" instructions, heartbeat sends after upgrade
- `#4412` ([open PR](https://github.com/HKUDS/nanobot/pull/4412)): Suppress routine cron job notifications

Community consensus: cron/heartbeat results should respect channel context and suppress routine outputs.

## Bugs & Stability
**Severity: Medium-High**

| Issue | Severity | Status | Description |
|-------|----------|--------|-------------|
| [#4410](https://github.com/HKUDS/nanobot/issues/4410) | **High** | Open | Heartbeat sends unwanted messages after v0.15 upgrade — regression affecting cron-based automation |
| [#4345](https://github.com/HKUDS/nanobot/issues/4345) | High | Closed (no fix PR linked) | Image-strip fallback leaks file paths and creates false image attribution |
| [#4287](https://github.com/HKUDS/nanobot/issues/4287) | Medium | Closed | Empty model responses not triggering fallback — critical for production reliability |
| [#4013](https://github.com/HKUDS/nanobot/issues/4013) | Medium | Closed | "stream stalled for more than 90 seconds" error after v0.2.0 upgrade — likely connection timeout configuration issue |
| [#4052](https://github.com/HKUDS/nanobot/issues/4052) | Low | Closed | MCP `notifications/progress` messages rejected as invalid literal by Pydantic validator |

**Regression pattern observed**: Multiple users report behavior changes between v0.1.5post2 and v0.2.x (stream stalls, unwanted heartbeat messages). A controlled migration guide may reduce friction.

## Feature Requests & Roadmap Signals
**High-value features likely to land in next version (v0.3.0):**

1. **Automatic reasoning effort escalation** ([#4419](https://github.com/HKUDS/nanobot/issues/4419)) — Configurable "default + escalated" `reasoningEffort` levels would let agents use stronger reasoning for complex prompts without manual intervention. Given NanoBot already supports `reasoningEffort` as a config field, this is an incremental enhancement.

2. **Subagent aggregated results** ([#4414](https://github.com/HKUDS/nanobot/pull/4414), open PR) — New `aggregated` mode for subagent results buffers completed subagent outputs and publishes one combined message. This solves the "noisy subagent stream" problem for complex workflows.

3. **Cron job model presets** ([#4416](https://github.com/HKUDS/nanobot/pull/4416), open PR) — Allows per-cron-job model overrides without mutating the live agent, enabling specialized scheduled tasks with cheaper/faster models.

4. **Subagent spawn model override** ([#4415](https://github.com/HKUDS/nanobot/pull/4415), open PR) — Enables spawning subagents with different models, critical for multi-agent architectures.

5. **SuspendTurn tool** ([#4411](https://github.com/HKUDS/nanobot/pull/4411), open PR) — Tool-driven turn suspension for async/human-in-the-loop patterns, enabling more complex interactive workflows.

6. **Inline TUI** ([#4329](https://github.com/HKUDS/nanobot/pull/4329), open PR) — New terminal UI for `nanobot agent` command with JetBrains-inspired palette, likely to ship alongside a refined onboarding flow ([#4395](https://github.com/HKUDS/nanobot/pull/4395), open PR).

7. **Telegram rich messages** ([#4413](https://github.com/HKUDS/nanobot/issues/4413)) — Support for Telegram Bot API 10.1 rich message format, requested by community.

## User Feedback Summary
- **Satisfaction areas**: Users praise v0.1.5post2 WebUI stability ("it's been very good"), the new project workspaces feature, and the general direction of multi-provider support. The `SuspendTurn` PR and subagent improvements address power-user needs for complex orchestration.
- **Pain points**: 
  - **Migration friction**: Several issues stem from v0.2.0 upgrades breaking previously working setups (stream stalls, unwanted heartbeat messages). Users need clearer upgrade guides.
  - **Model fallback gaps**: Empty responses and context window mismatches are the top operational complaint among multi-model users.
  - **Workspace asymmetry**: Project workspaces read bootstrap files from project root but write them to default workspace — a UX inconsistency reported in [#4374](https://github.com/HKUDS/nanobot/issues/4374) (closed).

## Backlog Watch
**Items requiring maintainer attention:**

1. **[High Priority] XMPP channel PR** ([#1945](https://github.com/HKUDS/nanobot/pull/1945)) — Open since **March 12, 2026** (100 days). The author notes "it works for me, might work for you too" with no maintainer review history. XMPP is a notable gap in channel support that some community members likely need.

2. **Dream update scope controls** ([#3591](https://github.com/HKUDS/nanobot/pull/3591)) — Open since **May 2** (49 days). Would let users control Dream's automatic consolidation scope to prevent unwanted skill drift. No maintainer comments.

3. **Manual heartbeat trigger** ([#3590](https://github.com/HKUDS/nanobot/pull/3590)) — Open since **May 2** (49 days). On-demand heartbeat trigger for dry-running Phase 1 decisions. No maintainer engagement.

4. **Token estimation without network loads** ([#3662](https://github.com/HKUDS/nanobot/pull/3662)) — Open since **May 6** (43 days). Avoids calling `tiktoken.get_encoding` unless cached, with offline fallback. Important for air-gapped deployments. No maintainer review.

5. **Feat(dream): add update scope controls** ([#3591](https://github.com/HKUDS/nanobot/pull/3591)) — 49 days stale with zero maintainer interaction, despite addressing a real concern about automatic consolidation causing unwanted agent behavior drift.

**Pattern**: Community-contributed features from mid-spring 2026 remain unreviewed, particularly around Dream/heartbeat mechanics. As the project accelerates toward v0.3.0, a backlog grooming pass on these 45-100 day old PRs would be valuable.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — June 20, 2026

## 1. Today's Overview

Hermes Agent is exhibiting **extremely high development velocity**, with 50 issues and 50 PRs updated in the last 24 hours. The project just shipped **v0.17.0 ("The Reach Release")** on June 19, representing ~1,475 commits, 800+ merged PRs, and contributions from 245 community members. However, this rapid growth has surfaced **significant quality and regression challenges**: 41 of 50 active issues remain open, with multiple P1-critical bugs (context compression corruption, credential proxy gaps, authentication failures) and 6 duplicate bug reports filed within the last 48 hours. The community is highly engaged but increasingly frustrated with regressions in Gemma 4 support, desktop UI stability, and gateway reliability across platforms.

## 2. Releases

### v0.17.0 (v2026.6.19) — "The Reach Release"
- **Release Date:** June 19, 2026
- **Since v0.16.0:**
  - ~1,475 commits · ~800 merged PRs · 1,693 files changed
  - 235,390 insertions · 50,730 deletions · 300+ issues closed
  - 245 community contributors

**Key Changes (inferred from release title "v0.17.0 — The Reach Release"):**
- v0.16.0 brought Hermes to desktop; v0.17 expands platform reach and agent capabilities
- PR #49037 indicates first-class **Projects** backend-authoritative session tree
- PR #38846 shows 15-language i18n support with 861 translation keys
- Significant gateway/desktop infrastructure (WhatsApp, Signal, webhook sessions)
- New tooling: xAI image edit/refresh, web backend failover chains

**Breaking Changes / Migration Notes:**
- None explicitly documented in the release notes collected
- Large-scale refactors (projects model, i18n skeleton) may require config migration
- Desktop app users should expect UI/UX changes in dashboard and profile management

## 3. Project Progress

**Today's Merged/Closed PRs (11 total):**
- [#45971](https://github.com/NousResearch/hermes-agent/pull/45971) — **fix(agent): return anthropic partial stream stubs** — fixes partial delivery failures for Anthropic streams
- [#47070](https://github.com/NousResearch/hermes-agent/pull/47070) — **Fix stale bootstrap update failures** — macOS app rebuild detection, skip redundant installs
- [#49260](https://github.com/NousResearch/hermes-agent/issues/49260) — **Closed: Live adapter delivers silently for Signal cron jobs** (P1) — acknowledged and likely fixed
- 8 additional PRs merged/closed impacting cron, desktop, web-server, and authentication

**Features that Advanced Today:**
- **Webhook persistent sessions** ([PR #49353](https://github.com/NousResearch/hermes-agent/pull/49353)) — session_key routing for repeated external events into one Hermes session
- **Chinese (Simplified) dashboard i18n** ([PR #49339](https://github.com/NousResearch/hermes-agent/pull/49339)) — 42 missing translation keys, 8 new i18n sections
- **Declarative reasoning_effort_max** ([PR #49355](https://github.com/NousResearch/hermes-agent/pull/49355)) — support for Z.AI/GLM-5.2 deep reasoning tier
- **Nous Portal access token resilience** ([PR #49351](https://github.com/NousResearch/hermes-agent/pull/49351)) — rotating OAuth tokens, fallback sync
- **Animated mascot pets** ([PR #46464](https://github.com/NousResearch/hermes-agent/pull/46464)) — sprite mascots across CLI, TUI, and desktop

## 4. Community Hot Topics

| Issue/PR | Type | Comments | Reaction | Description |
|----------|------|----------|----------|-------------|
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | Feature | 11 | 👍1 | **Credential proxy daemon** — zero-knowledge HTTP/HTTPS broker for agent credentials. Long-running (since April 2) but gaining traction. Addresses fundamental limitation: PID namespace isolation (#4432) still leaves config-based credentials vulnerable. |
| [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) | Feature | 6 | 👍9 | **Headroom-ai tool output compression** — user requests tool-level (not conversation-level) compression. High community interest (9 thumbs up). |
| [#45924](https://github.com/NousResearch/hermes-agent/issues/45924) | Bug | 5 | 👍1 | **Gemma 4 12B on Ollama fails** — immediate error on "hello" with `NoneType` object. Active and escalating. |
| [#39281](https://github.com/NousResearch/hermes-agent/issues/39281) | Bug (closed) | 4 | 👍0 | **Original Gemma 4 bug** — "Response truncated" warnings. Closed with PR #41694, but user re-filed as [#49297](https://github.com/NousResearch/hermes-agent/issues/49297) claiming fix didn't work. |
| [#49297](https://github.com/NousResearch/hermes-agent/issues/49297) | Bug | 3 | 👍0 | **Recreated Gemma 4 issue** — user explicitly says "updated to v0.17.0 and issue still persists." Maintainer attention needed. |

**Analysis:** The community's core concern is **regression management** — the Gemma 4 saga (3 related issues: #39281 closed, #45924 open, #49297 open) shows the fix shipped in v0.17.0 didn't actually resolve the problem. Users are re-filing bugs and expressly doubting whether closed issues are seen by maintainers.

## 5. Bugs & Stability

### Critical (P1)
| Issue | Summary | Fix PR Exists? |
|-------|---------|----------------|
| [#49307](https://github.com/NousResearch/hermes-agent/issues/49307) | **Context compression causes answer repetition + instruction loss** — documented with reproduction files | No |
| [#49260](https://github.com/NousResearch/hermes-agent/issues/49260) | **Signal cron: silent delivery failure** — status ok/null error but messages never reach user | Closed (fix assumed) |
| [#46718](https://github.com/NousResearch/hermes-agent/pull/46718) | **Email gateway spoofing vulnerability** — allowlist checks trust spoofable From header instead of authenticated sender | Open PR [#46718](https://github.com/NousResearch/hermes-agent/pull/46718) |
| [#49356](https://github.com/NousResearch/hermes-agent/pull/49356) | **Anthropic OAuth token exchange broken** — 404 on platform.claude.com | Open PR [#49356](https://github.com/NousResearch/hermes-agent/pull/49356) |
| [#49351](https://github.com/NousResearch/hermes-agent/pull/49351) | **Nous Portal access token churn** — token refresh writes to wrong store | Open PR [#49351](https://github.com/NousResearch/hermes-agent/pull/49351) |

### High (P2)
| Issue | Summary | Fix PR Exists? |
|-------|---------|----------------|
| [#39281](https://github.com/NousResearch/hermes-agent/issues/39281) / [#49297](https://github.com/NousResearch/hermes-agent/issues/49297) / [#45924](https://github.com/NousResearch/hermes-agent/issues/45924) | **Gemma 4 on Ollama — multiple open failures** | PR #41694 (didn't work) |
| [#47868](https://github.com/NousResearch/hermes-agent/issues/47868) | **Strict providers reject leaked message metadata (timestamp)** — breaks OpenCode Go compatibility | No |
| [#48523](https://github.com/NousResearch/hermes-agent/issues/48523) | **Gateway: `convert_messages` doesn't strip internal metadata** — 400 errors with strict providers | No |
| [#47795](https://github.com/NousResearch/hermes-agent/issues/47795) | **Desktop chat scroll jumps/bounces after streaming stops** — reading impossible | No |
| [#47500](https://github.com/NousResearch/hermes-agent/issues/47500) | **Desktop app auto-previews links triggering custom protocol handlers** — Windows popups | No |
| [#33327](https://github.com/NousResearch/hermes-agent/issues/33327) | **BlueBubbles webhook conflicts** — duplicate/interrupted replies | Local fix exists but not upstreamed |
| [#49345](https://github.com/NousResearch/hermes-agent/issues/49345) | **Desktop GUI: 'Start Gateway' button has no effect** | No |
| [#49332](https://github.com/NousResearch/hermes-agent/issues/49332) | **`delegate_task` model override ignored** — subagents use wrong model, consume unauthorized credits | No |
| [#48991](https://github.com/NousResearch/hermes-agent/issues/48991) | **auxiliary.vision provider=auto doesn't inherit base_url/api_key** — connection failures with custom providers | No |
| [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) | **CLI --global model switch doesn't persist base_url/api_mode** — configuration loss | No |
| [#23802](https://github.com/NousResearch/hermes-agent/issues/23802) | **Plugins CLI filters out entry-point-discovered plugins** — invisible plugins | No |
| [#49283](https://github.com/NousResearch/hermes-agent/issues/49283) | **execute_code consent gate ignores explicit chat consent** — desktop GUI blocks approved tool execution | No |
| [#49354](https://github.com/NousResearch/hermes-agent/pull/49354) | **SQLite WAL state handling repair** — state-store corruption | Open PR [#49354](https://github.com/NousResearch/hermes-agent/pull/49354) |

**Assessment:** The bug situation is **concerning**. 5 P1 bugs exist simultaneously, including one security vulnerability (email gateway spoofing [#46718](https://github.com/NousResearch/hermes-agent/pull/46718)). The Gemma 4 regression has been "fixed" once but the fix was incomplete. Desktop UX regressions (scroll jumping, button non-functional, protocol handler issues) suggest insufficient testing on v0.17.0.

## 6. Feature Requests & Roadmap Signals

### High Community Interest
| Issue | Description | Likelihood for Next Release |
|-------|-------------|----------------------------|
| [#39691](https://github.com/NousResearch/hermes-agent/issues/39691) | **Headroom-ai tool-level compression** (👍9) | **High** — addresses a key pain point and aligns with v0.17's performance focus |
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | **Credential proxy daemon** (11 comments) | **Medium** — fundamental architecture change, likely v0.18 |
| [#32159](https://github.com/NousResearch/hermes-agent/issues/32159) | **Ordered web backend failover chains** | **Medium** — incremental improvement |
| [#49279](https://github.com/NousResearch/hermes-agent/issues/49279) | **GLM-5.x reasoning support in OpenCodeGo** (👍1) | **High** — quick fix, PR likely incoming |

### Strong Roadmap Signals
- **Pets/mascots** ([PR #46464](https://github.com/NousResearch/hermes-agent/pull/46464)) — whimsical but shows investment in UX delight across all surfaces
- **15-language i18n** ([PR #38846](https://github.com/NousResearch/hermes-agent/pull/38846)) — strategic global expansion, 861 translation keys
- **Projects backend** ([PR #49037](https://github.com/NousResearch/hermes-agent/pull/49037)) — major architectural shift in session management
- **xAI image editing** ([PR #41356](https://github.com/NousResearch/hermes-agent/pull/41356)) — expanding vision capabilities
- **Zulip platform adapter** ([#49229](https://github.com/NousResearch/hermes-agent/issues/49229)) — already submitted as PR #3335

**Prediction for v0.18.0:** Projects backend, i18n finalization, credential proxy daemon MVP, and significant bugfix stabilization. The team appears to be in "feature push" mode for v0.17, with v0.18 likely focused on hardening.

## 7. User Feedback Summary

### Pain Points (High Frequency)
| Issue | User Sentiment |
|-------|----------------|
| **Gemma 4 / Ollama broken** | **Frustrated** — "updated to v0.17.0 and issue still persists." User re-filed because "unsure if closed issues are seen by maintainers." |
| **Desktop chat scroll jumping** | **Angry** — "reading is impossible." User reports scroll continues bouncing even after streaming stops. |
| **Windows: background actions spawn console windows** | **Irritated** — multiple PRs (#49352, #49357, #49242) address aspect of this on Windows |
| **Context compression corrupts output** | **Critical** — "answer repetition + new instruction loss." Attached reproduction files + screenshots. |
| **Chinese input method triggers settings page** | **Frustrated** — comma/period input triggers unintended navigation. Affects Core user experience for Chinese users. |
| **Duplicate bug reporting** | **Exhaustion** — users are tracking their own issue continuity (see #49297: "Re-creating issue as I'm unsure if closed issues are seen by maintainers") |

### Satisfaction Signals
- 245 community contributors for v0.17 shows strong engagement
- PR #38846 (15-language i18n) and PR #46464 (animals/pets) receive consistent positive attention
- Community proactively contributes fixes (11 PRs merged/closed today from diverse authors)

### Notable Request
[#46199](https://github.com/NousResearch/hermes-agent/issues/46199) asks for **portable/isolated deployment guidance on Windows** — security-conscious user evaluating Hermes but concerned about global PATH writes and system modifications. This signals an underserved **enterprise/security** user segment.

## 8. Backlog Watch

### Long-Standing Open Issues Without Maintainer Response
| Issue | Age | Summary |
|-------|-----|---------|
| [#4656](https://github.com/NousResearch/hermes-agent/issues/4656) | 79 days (Apr 2) | **Credential proxy daemon** — 11 comments, 0 maintainer response in 2.5 months |
| [#25106](https://github.com/NousResearch/hermes-agent/issues/25106) | 38 days (May 13) | **CLI --global model switch doesn't persist base_url/api_mode** — configuration loss, no maintainer response |
| [#23802](https://github.com/NousResearch/hermes-agent/issues/23802) | 40 days (May 11) | **Plugins CLI filters out discovered plugins** — invisible plugins, no response |
| [#21788](https://github.com/NousResearch/hermes-agent/issues/21788) | 43 days (May 8) | **Dashboard /chat: gateway exited** when `.venv` coexists with `venv` — closed without discussion |

### Critical Attention Needed
| Issue | Priority | Reason |
|-------|----------|--------|
| [#49297](https://github.com/NousResearch/hermes-agent/issues/49297) / [#45924](https://github.com/NousResearch/hermes-agent/issues/45924) | **P1-P2** | User explicitly says v0.17.0 didn't fix the Gemma 4 bug. Three related issues now exist. |
| [#49307](https://github.com/NousResearch/hermes-agent/issues/49307) | **P1** | Context compression corrupts agent output. Single most critical functional bug. |
| [#46718](https://github.com/NousResearch/hermes-agent/pull/46718) | **P1** | Email gateway spoofing vulnerability — security issue with open PR needing review |

**Notable Pattern:** Several issues (e.g., #4656, #25106) have sat unanswered for over a month while similar new issues receive immediate PRs. This suggests maintainers are prioritizing feature development over backlog cleanup, which risks alienating existing users and creating technical debt.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-20

## 1. Today's Overview
Project activity remains **moderate**, with 4 issues updated in the last 24 hours and 7 pull requests showing activity. One new **nightly build** (v0.3.0-nightly) was released, though marked as unstable. No merged PRs were recorded for today; however, one PR was closed (#2956). The backlog contains several **stale** PRs awaiting review, particularly around identity parsing, MCP argument handling, and a large agent collaboration feature. Community engagement is mixed, with a critical memory-loss bug (#3150) appearing recently and a high-priority attachment support enhancement (#348) lingering since February. Overall health is **stable but with growing technical debt in review turnaround**.

## 2. Releases
**New Release:** `nightly` (v0.3.0-nightly.20260620.287853ab)  
- Automated build from `main` branch; may be unstable.  
- Full changelog: [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)  
- No breaking changes or migration notes provided; users should exercise caution.

## 3. Project Progress
**Merged/Closed PRs (last 24h):**  
- **PR #2956** (closed) – `fix: preserve channel enabled state when merging security.yml`  
  - Fixed a bug where channels configured as `enabled: true` in `config.json` were being disabled after loading `.security.yml` due to merge overwrites.  
  - Author: yuxuan-7814  

No other PRs were merged today. Six open PRs remain stale (no update in 12+ days), including critical fixes for SSRF guard bypass (#3143), identity parsing for Matrix (#3045), and a major agent collaboration bus (#2937).

## 4. Community Hot Topics
- **Issue #3150** (`[BUG]它给自己整失忆了`) – Created 2026-06-19, 2 comments, 0 reactions.  
  - User reports the agent "loses memory" (likely context/session loss). Minimal details provided.  
  - [Link](https://github.com/sipeed/picoclaw/issues/3150)

- **Issue #2472** (`[BUG] list_dir returns "invalid argument" on Windows`) – 6 comments, 1 👍.  
  - Long-standing cross-platform compatibility issue affecting file listing on Windows.  
  - [Link](https://github.com/sipeed/picoclaw/issues/2472)

- **Issue #3114** (`[Future Request] Telegram 渠道按对话类型权限分级控制`) – 1 comment, 1 👍.  
  - User requests Telegram channel permission levels by chat type (private/group/channel).  
  - [Link](https://github.com/sipeed/picoclaw/issues/3114)

**Underlying needs:** Windows compatibility, memory/context persistence, and chat-specific permission granularity are the most pressing community concerns.

## 5. Bugs & Stability
| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| 🔴 Critical | #3150 | Agent memory loss ("失忆") – likely context/session corruption | No |
| 🟠 High | #2472 | `list_dir` fails on Windows due to path separator mismatch | No |
| 🟡 Moderate | #3044 (fixed by #3045) | Matrix `allow_from` parsing fails for standard user IDs (`@user:domain`) | ✅ PR #3045 (stale) |
| 🟡 Moderate | #3074 (fixed by #3143) | SSRF guard bypass via ISATAP IPv6 literals | ✅ PR #3143 (open) |

**Worst bug:** Issue #3150 – agent memory loss. No fix proposed yet. Could indicate a fundamental issue in context management.

## 6. Feature Requests & Roadmap Signals
- **High-priority roadmap item:** Issue #348 – General Attachment Support (files, documents, multimedia across channels) – opened Feb 2026, labeled `type: roadmap`, `priority: high`.  
  - Likely candidate for v0.4.0 given its roadmap designation and long duration.

- **Feature request #3114:** Telegram channel permission levels by conversation type. Moderate interest (1 👍).

- **PR #2937 – Agent Collaboration Bus:** Still open and stale since May 24. If merged, could be a major v0.4.0 feature enabling multi-agent workflows.

- **Prediction:** v0.3.0 (stable) will likely include the memory-loss fix (#3150), per-channel security merge fix (#2956), and SSRF guard improvement (#3143). Attachment support (#348) may slip to v0.4.0.

## 7. User Feedback Summary
- **Pain points:** Windows path handling (Issue #2472), memory/context loss (Issue #3150), Telegram permission inflexibility (Issue #3114).  
- **Positive signals:** The `list_dir` bug has been reported with detailed reproduction steps (6 comments), indicating an engaged, technically proficient user base.  
- **Satisfaction:** Mixed – the nightly release pipeline shows active development, but staleness of high-impact PRs (e.g., #3045, #2937) may frustrate contributors.

## 8. Backlog Watch
| Issue/PR | Days Open | Last Updated | Type | Reason for Watch |
|----------|-----------|--------------|------|------------------|
| **Issue #348** | 123 days | 2026-06-19 | Feature (roadmap, high priority) | Core roadmap item with no progress since Feb 2026 |
| **PR #2937** | 27 days | 2026-06-19 | Feature (agent collaboration) | Large, complex PR; needs maintainer review |
| **PR #3045** | 13 days | 2026-06-19 | Bug fix (Matrix identity) | Fixes real bug (#3044); stale without comments |
| **PR #3091** | 10 days | 2026-06-19 | Bug fix (OpenAI compat) | Small fix; low review effort needed |
| **Issue #2472** | 71 days | 2026-06-19 | Bug (Windows) | Long-standing cross-platform issue; no fix PR |

**Call to action:** Maintainers should prioritize review of PRs #3045 (Matrix fix) and #3143 (SSRF guard) as they address actively reported bugs. The roadmap feature #348 and collaborative agent PR #2937 need roadmap decisions to avoid indefinite stalling.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

## NanoClaw Project Digest — 2026-06-20

### 1. Today's Overview
Project activity is **moderate**, with **5 open pull requests** updated in the last 24 hours and **no new releases**. No issues were reported or resolved today, suggesting the current maintenance focus is on integration improvements rather than bug triage. The PR pipeline is actively processing three fixes and two feature additions, indicating a healthy but deliberate development cadence. Maintainers appear to be balancing infrastructure work (container runtime support) with targeted bug fixes (Discord chunking, approval persistence).

---

### 2. Releases
**No new releases** today. The last structured release remains the previous stable version.

---

### 3. Project Progress
**No PRs were merged or closed today.** All 5 open PRs remain in review/development status:

- **#2820** — `fix(approvals): persist delivery target on pending_approvals rows` — Critical fix for approval workflow data integrity, ensuring `channel_type`, `platform_id`, and `platform_message_id` are recorded.
- **#2812** — `fix(discord): chunk replies over 2000 chars instead of truncating` — Addresses Discord message truncation by enabling the existing `splitForLimit` chunker in the Discord adapter.
- **#2809** — `feat(apple-container): Apple Container runtime + remote OneCLI gateway` — Adds macOS-native container runtime support with remote gateway configuration.
- **#2605** — `feat: inherit parent agent permissions via OneCLI` — Extends permission management, likely enabling hierarchical agent authorization.
- **#2819** — `Add MseeP.ai badge` — A README metadata addition for a third-party security directory.

---

### 4. Community Hot Topics
**No PRs or Issues have exceptional engagement metrics** (all have 0 comments and 0 reactions). The most substantial contributions are structural:

- **[PR #2809](https://github.com/nanocoai/nanoclaw/pull/2809)** — Apple Container runtime support is the most ambitious PR, potentially enabling macOS-native deployments. The lack of community discussion may indicate early-stage review or niche audience interest.
- **[PR #2605](https://github.com/nanocoai/nanoclaw/pull/2605)** — Parent agent permission inheritance suggests growing enterprise use cases where agent hierarchy management is needed.

**Underlying need:** The approvals fix (#2820) and Discord chunking (#2812) both address silent data loss — approval metadata disappears and long replies get truncated. This hints at **production reliability gaps** in two core features.

---

### 5. Bugs & Stability
**No new bugs reported today.** The three open fix PRs target known issues:

| Severity | Bug | Fix PR | Status |
|----------|-----|--------|--------|
| **High** | Approval workflow rows missing delivery metadata (`channel_type`, `platform_id`, `platform_message_id` are NULL) | [#2820](https://github.com/nanocoai/nanoclaw/pull/2820) | Open |
| **Medium** | Discord replies over 2000 characters are silently truncated instead of split into multiple messages | [#2812](https://github.com/nanocoai/nanoclaw/pull/2812) | Open |

**Stability note:** The approvals bug (#2820) is the highest priority — it corrupts the `pending_approvals` table for every approved request, breaking downstream queries and audit trails.

---

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the open PRs reveal two clear roadmapped improvements:

- **Apple Container runtime** ([PR #2809](https://github.com/nanocoai/nanoclaw/pull/2809)) — Likely for **next minor version**, enabling macOS-native deployments via env-gated `CONTAINER_RUNTIME=container`. This appears to be a formally developed feature, not a community request.
- **Parent agent permission inheritance** ([PR #2605](https://github.com/nanocoai/nanoclaw/pull/2605)) — Signals growing demand for **multi-agent governance**; likely targeted for an upcoming feature release.

**Prediction for next version:** Both `apple-container` and `parent-permission-inheritance` are strong candidates for inclusion. The approvals and Discord fixes are blockers for stable release.

---

### 7. User Feedback Summary
**No direct user feedback was collected today** (0 issue comments, 0 reactions). Indirect signals from PR content:

- **Pain point:** Discord users experiencing truncated AI responses — the chunking fix (#2812) suggests dissatisfaction with message completeness.
- **Pain point:** Approval process users unable to retrieve where a card was actually delivered — the approvals metadata fix (#2820) points to a broken audit trail.
- **Use case:** macOS operators seeking native container support — the Apple Container PR (#2809) indicates a demand for non-Docker deployment.

---

### 8. Backlog Watch
**No long-untouched Issues or PRs** are currently outstanding. The oldest open PR is:

- **[PR #2605](https://github.com/nanocoai/nanoclaw/pull/2605)** (created 2026-05-24, 27 days old) — `feat: inherit parent agent permissions via OneCLI`. This is a significant feature PR that has not been merged or received maintainer comments in nearly a month. **Requires attention** to avoid feature branch divergence or contributor frustration.

**Maintainer note:** The approvals fix (#2820) and Discord fix (#2812) are both a day old — timely review would prevent accumulation of unmerged bug fixes.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 20, 2026, based on the provided GitHub data.

---

### NullClaw Project Digest – 2026-06-20

**1. Today's Overview**
The project shows moderate activity today, with one issue closed and a new pull request opened, though no new releases were cut. The primary focus is on improving platform stability, specifically for users running NullClaw on Android via Termux with aarch64 architecture. While general community engagement remains low (no high-traffic threads), the maintainer team is actively resolving a previously reported bug regarding incomplete answers from local Ollama models. The project's health is stable, with a clear signal of effort toward expanding platform compatibility.

**2. Releases**
No new releases were published today. The project remains on the last known version (v2026.4.17), as referenced in a bug report.

**3. Project Progress**
- **Merged/Closed PRs (Today):** 0 merged PRs.
- **Closed Issues (Today):** 1
    - **#952 [CLOSED]** [bug] Local model using ollama returns incomplete answers: A bug where the agent failed to return complete sentences when using a local Gemma model via Ollama has been resolved. The fix was likely included in a recent commit, as the issue was closed without a specific release.
    - **PR #966** (Open): A new contribution is aiming to fix HTTP connectivity on aarch64-linux-android.

**4. Community Hot Topics**
No issues or PRs generated significant community attention (comments or reactions) today. The most active item in the last 24 hours is the newly opened PR #966, which addresses a critical connectivity bug.

**5. Bugs & Stability**
- **High Severity (Fix in Progress):**
    - **#868 [OPEN]** [bug] zig build fails on Android/Termux (aarch64) with AccessDenied: This bug prevents users on Xiaomi Redmi Note 9 (LineageOS/Termux) from compiling NullClaw. The error occurs during the link phase of the Zig build process.
    - **PR #966** (Open) directly addresses the root cause of this issue by routing HTTP through `curl` on that specific platform. This is a strong signal that a fix is imminent.
- **Medium Severity (Unresolved):**
    - **#484 [OPEN]** 飞书无法联网查询 (Feishu cannot connect to the internet): A long-standing issue (since March) where the Feishu/Lark integration fails to perform network lookups. No fix PR is currently attached.

**6. Feature Requests & Roadmap Signals**
No new feature requests were logged today. The activity strongly signals that the development roadmap is currently prioritizing **cross-platform compatibility** and **network stack reliability**. The incoming fix for Android (PR #966) suggests the next minor release will likely target Termux/aarch64 stability.

**7. User Feedback Summary**
- **Pain Point (Addressed):** A user (bloodgroup-cplusplus) using Ollama with Gemma reported the agent "cutting off" sentences. The closing of Issue #952 suggests this text truncation bug has been resolved.
- **Pain Point (Resistance):** User NOTJuangamer10 is unable to compile the project on their Android device (Termux). The barrier is a low-level system linker issue (`AccessDenied on linkat`).
- **Satisfaction Signal:** The existence of PR #966 from a contributor (vernonstinebaker) indicates that community developers are actively invested in solving the Android build/network problems.

**7. Backlog Watch**
- **#484 [OPEN]** 飞书无法联网查询 (Feishu cannot connect to the internet): Created 2026-03-13, updated 2026-06-19. This issue has been open for over three months and involves a core integration (Feishu/Lark). It has received no apparent maintainer response or fix attempt. **Recommendation:** Requires maintainer triage—either a workaround, a request for more logs, or an acknowledgment that this platform is unsupported.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-20

## 1. Today's Overview

IronClaw is in an intense development sprint, with **30 pull requests** updated in the last 24 hours (12 merged/closed, 18 still open) and **4 issues** updated (3 open, 1 closed). Activity is heavily concentrated on the **Reborn** architecture—the project's next-generation AI agent runtime—with major feature stack landings in Projects (5/5 fully merged), external-tool API compatibility, Slack/Telegram ingress, and concurrent turn execution. No new releases were cut today, indicating the team is consolidating multiple feature branches before a planned version bump. CI infrastructure improvements (mold linker adoption, sccache A/B testing) suggest the team is actively optimizing build times to support this high-velocity development cycle.

## 2. Releases

**None.** No new versions were published in the last 24 hours.

## 3. Project Progress — Merged/Closed PRs Today (12 items)

### Core Reborn Features
- **#5019 [MERGED]** — `feat(reborn): Projects — light up the Projects page (5/5)` — Final stack layer that wires real CRUD endpoints to WebChat v2 frontend, replacing all stubs. This completes the 5-PR Projects rollout, enabling real project management in the Reborn UI.
  - *Link:* [PR #5019](https://github.com/nearai/ironclaw/pull/5019)

- **#5064 [MERGED]** — `fix(reborn): Projects — address leftover review comments` — Resolved unaddressed review feedback from the merged Projects PRs: typed timestamps, correct project deletion behavior, and refined webhook wiring.
  - *Link:* [PR #5064](https://github.com/nearai/ironclaw/pull/5064)

### CI & Developer Experience
- **#5090 [MERGED]** — `perf(ci): extend mold linker to reborn-e2e and replay-gate Rust jobs` — Extends the proven mold linker recipe (previously showed ~40% improvement) to additional CI jobs, reducing overall build latency.
  - *Link:* [PR #5090](https://github.com/nearai/ironclaw/pull/5090)

- **#5092 [MERGED]** — `ci(spike): A/B sccache (GHA) vs rust-cache on a heavy Reborn build` — Adds an experimental workflow to compare sccache vs Swatinem/rust-cache performance, informing future CI caching strategy.
  - *Link:* [PR #5092](https://github.com/nearai/ironclaw/pull/5092)

- **#5097 [MERGED]** — `docs: add Reborn QA guidance to agent rules` — Added AGENTS.md guidance for cross-layer and user-visible Reborn behavior testing.
  - *Link:* [PR #5097](https://github.com/nearai/ironclaw/pull/5097)

- **#5095 [MERGED]** — `test(reborn-qa): add recorded fixtures` — Committed Reborn QA LLM trace fixtures for connection, routine, and web-fetch scenarios, with recording/replay support for HTTP exchanges.
  - *Link:* [PR #5095](https://github.com/nearai/ironclaw/pull/5095)

- **#5096 [MERGED]** — `test(reborn-qa): port project-setup automation-workflow benchmarks` — Ported all seven automation-workflow benchmarks into the Reborn QA recorded trace harness, expanding test coverage.
  - *Link:* [PR #5096](https://github.com/nearai/ironclaw/pull/5096)

### Issue Resolution
- **#5078 [CLOSED]** — Approval modal becomes difficult to review when displaying large tool commands — Closed as addressed (likely by UI improvements or truncation logic).
  - *Link:* [Issue #5078](https://github.com/nearai/ironclaw/issues/5078)

## 4. Community Hot Topics

### Most Active Pull Requests

1. **#5061 — Skill extraction & self-evolution with activation controls** — Open XL PR by a new contributor (krishna-505) that adds Hermes-style skill extraction to Reborn: background distillation of successful turns into reusable `SKILL.md` files, with prompt-injection safety scanning. This is one of the most feature-dense contributions and touches `scope: docs, dependencies`.
   - *Link:* [PR #5061](https://github.com/nearai/ironclaw/pull/5061)

2. **#5087 — Proactive Google OAuth token refresh** — Open XL PR by core contributor henrypark133. Implements dual-mechanism token refresh (access token on-demand, refresh token proactive by TTL) to keep Google credentials usable without manual reconnection. Addresses a real user-reported pain point (#5071).
   - *Link:* [PR #5087](https://github.com/nearai/ironclaw/pull/5087)

3. **#5100 — Telegram ingress from extension state** — Open XL PR by new contributor abbyshekit. The Telegram analogue of the Slack ingress work (#5093), allowing Telegram bot updates to be projected from enabled extension state. Signals growing interest in multi-platform ingress support.
   - *Link:* [PR #5100](https://github.com/nearai/ironclaw/pull/5100)

4. **#5099 — External-tool Responses round-trip (Phase 4b-4f)** — Open XL PR by ilblackdragon completing the OpenAI-compatible Responses external-tool flow: declare client tools, surface parked tool calls, and resume from submitted outputs. This is core infrastructure for making Reborn a drop-in replacement for OpenAI's API.
   - *Link:* [PR #5099](https://github.com/nearai/ironclaw/pull/5099)

### Most Active Issues

1. **#5091 — Unified feature-flag system for Reborn** — Open enhancement issue by ilblackdragon. Proposes replacing ad-hoc `std::env::var` checks with a proper system supporting per-tenant targeting, gradual rollout, and A/B testing. This is a foundational architectural concern as Reborn scales to multi-tenant deployments.
   - *Link:* [Issue #5091](https://github.com/nearai/ironclaw/issues/5091)

2. **#5088 — Shell approval prompt asks to approve read commands as "reads"** — Open bug report about misleading approval UI. Part of the larger approval UX improvement initiative (#4879). User confusion indicates the approval system needs clearer labeling.
   - *Link:* [Issue #5088](https://github.com/nearai/ironclaw/issues/5088)

**Underlying needs:** The community is pushing for production-grade Reborn features: multi-platform ingress (Slack/Telegram), proper API compatibility (OpenAI Responses), user-configurable tool permissions, and robust CI/CD. New contributors are actively joining the feature development, suggesting good project onboarding and mentorship practices.

## 5. Bugs & Stability

### Active Bugs (Ranked by Severity)

1. **#4108 — Nightly E2E failed** — 🔴 **Critical (ongoing)** — Nightly end-to-end tests have been failing since May 27, with no root cause discussion in the issue. The commit `0a4d1cf82f038f996ca0c115c43bea1bfaf60525` may be a suspect. This is the highest-priority stability concern as it blocks automated quality verification.
   - *Status:* Open, unassigned, no comments since creation (23 days)
   - *Link:* [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

2. **#5088 — Shell approval prompt mislabels read commands as "reads"** — 🟡 **Medium** — UX confusion where read-only commands are presented for approval with misleading labels. While not a crash, it undermines user trust in the approval system. No fix PR yet; tracking under parent #4879.
   - *Status:* Open, no PR referenced
   - *Link:* [Issue #5088](https://github.com/nearai/ironclaw/issues/5088)

3. **#5078 — [CLOSED] Approval modal too large for big commands** — 🟢 **Resolved** — The approval modal displaying large shell commands was unmanageably long. Now closed, suggesting a fix was merged or the issue was addressed in related UI work.
   - *Link:* [Issue #5078](https://github.com/nearai/ironclaw/issues/5078)

### Stability Observations
- The **mold linker adoption** (#5090) and **sccache A/B experiment** (#5092) suggest the team is proactively addressing CI stability and build times—good hygiene for a project at this velocity.
- No regressions or crashes were reported in the last 24 hours beyond the pre-existing E2E failure.

## 6. Feature Requests & Roadmap Signals

### Strong Signals for Next Release

1. **Unified Feature-Flag System (#5091)** — Proposal from ilblackdragon (core contributor) suggests this is being actively planned. Expect implementation in the next 1-2 releases as Reborn scales to multi-tenant.
   - *Link:* [Issue #5091](https://github.com/nearai/ironclaw/issues/5091)

2. **External-Tool API Compatibility (#5094, #5099)** — Phase 4 of the OpenAI-compatible Responses API is landing now. `/v1/models` endpoint and tool catalog are live; round-trip execution is in review. This strongly signals IronClaw is positioning Reborn as an OpenAI API drop-in.
   - *Link:* [PR #5094](https://github.com/nearai/ironclaw/pull/5094)
   - *Link:* [PR #5099](https://github.com/nearai/ironclaw/pull/5099)

3. **Concurrent Turn Execution (#5085)** — Removing the serial execution bottleneck in Reborn runtime. With per-user/per-type concurrency caps, this is a major scalability improvement.
   - *Link:* [PR #5085](https://github.com/nearai/ironclaw/pull/5085)

4. **Per-Tool Permission Override Model (#5062)** — Users will be able to configure `always_allow` / `ask_each_time` / `disabled` per tool. This addresses a key adoption barrier for power users.
   - *Link:* [PR #5062](https://github.com/nearai/ironclaw/pull/5062)

5. **One-Shot Scheduled Triggers (#5065)** — Adding `TriggerSchedule::Once { at }` alongside recurring Cron. Useful for delayed tasks and timed reminders.
   - *Link:* [PR #5065](https://github.com/nearai/ironclaw/pull/5065)

6. **Hosted Single-Tenant Postgres Profile (#5081)** — A hosted preview path for Reborn using PostgreSQL-backed durable state. This is likely the deployment model for early external previews.
   - *Link:* [PR #5081](https://github.com/nearai/ironclaw/pull/5081)

### Likely Roadmap Direction
The pattern of PRs suggests the next stable release will focus on:
- **API compatibility** (OpenAI Responses standard)
- **Multi-platform ingress** (Slack, Telegram)
- **Scalability** (concurrent turns, feature flags, Postgres backend)
- **User controls** (per-tool permissions, smarter approval UI)
- **Self-evolution** (skill extraction from successful interactions)

## 7. User Feedback Summary

### Pain Points Expressed

- **Approval UI confusion** — Users report being asked to approve "reads" commands they don't recognize nor understand. The approval modal's handling of large commands was also problematic (now closed). *Indicates trust/usability gap in the safety mechanism.*
  - *Source:* [Issue #5088](https://github.com/nearai/ironclaw/issues/5088)

- **Google OAuth token expiration** — Users experience forced reconnection when Google tokens expire mid-session. The fix in #5087 addresses this by proactively refreshing tokens before expiry.
  - *Source:* [PR #5087](https://github.com/nearai/ironclaw/pull/5087)

- **E2E test reliability** — The long-standing nightly E2E failure (#4108, 23 days open without resolution) suggests automated quality assurance is broken, which may limit confidence in new releases.

### Positive Signals

- **New contributors** are actively submitting substantial features (skill extraction #5061 by krishna-505, Telegram ingress #5100 by abbyshekit), indicating good project health and developer experience.
- **Core team responsiveness** is high: 12 PRs merged/closed in 24 hours, with rapid follow-up on review comments (#5064).

## 8. Backlog Watch

### High Priority — Requires Maintainer Attention

1. **#4108 — Nightly E2E failed** — **23 days unresolved** 🔴 — No comments, no assignment, no linked PR. This is the only blocking CI issue and prevents reliable automated testing. The team has been focused on feature work, but this should be triaged this week.
   - *Link:* [Issue #4108](https://github.com/nearai/ironclaw/issues/4108)

2. **#4002 — Dependabot PR: bump actions group** — **27 days open** 🟡 — This PR bumps 16 GitHub Actions dependencies (including `actions/checkout` from 4.3.1 to 7.0.0). It's blocked on updates across the directory with risk level "medium." Waiting 27 days for dependency updates raises security concerns.
   - *Link:* [PR #4002](https://github.com/nearai/ironclaw/pull/4002)

### Moderate Priority

3. **#4829 — CI: retire dormant reborn-integration workflow** — **8 days open** 🟡 — While not urgent, this PR deletes a dead workflow and consolidates CI. It has been open since June 12 but may be waiting on the broader CI restructuring (#5098).
   - *Link:* [PR #4829](https://github.com/nearai/ironclaw/pull/4829)

### Emerging Watch Items

- **#5088 — Shell approval prompt mislabeling** — If this issue gains community traction (it's linked to the broader approval UX parent), it may need prioritization. Currently no fix PR exists.
- **#5091 — Unified feature-flag system** — Will likely generate significant discussion as it's a foundational architectural change. No comments yet, but core team authorship suggests it will be implemented soon.

---

**Overall Project Health: 🟢 Active & Shipping** — IronClaw is in a high-velocity feature development phase for its Reborn architecture. The project shows strong core contributor leadership, welcoming new contributors, and clear roadmap direction. The main risk is the unresolved nightly E2E failure, which should be addressed before the next release to ensure quality gates are operational.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-20**.

---

## LobsterAI Project Digest – June 20, 2026

### 1. Today's Overview
The project shows **moderate activity** today, primarily driven by the closure of three stale, non-critical bugs and a significant new release. A single **ambitious feature request** (#2180) was opened, signaling strong community interest in higher-level orchestration capabilities. No pull requests were merged or updated in the last 24 hours, indicating a lull in active development work on the core codebase. Overall, the project appears stable but is currently in a maintenance and planning phase rather than a sprint.

### 2. Releases
A new version, **LobsterAI 2026.6.18**, was released on June 18, 2026. The key change is an upgrade to the **Artifact sharing feature**, now supporting a wide range of file types including **Word, PPT, Excel, PDF, Markdown, and Mermaid**. This significantly expands the interoperability of the platform. A minor fix was also included to limit voice input to real-time ASR only, removing non-realtime options.

- **Breaking Changes:** None indicated in the release notes.
- **Migration Notes:** None required.
- **Changelog Link:** [LobsterAI 2026.6.18 Release](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.18)

### 3. Project Progress
**No pull requests were merged or closed today.** The most recent code contribution was the artifact sharing feature (PR #2159) which was included in the 2026.6.18 release. No new features were advanced via PRs in the last 24 hours.

### 4. Community Hot Topics
The only actively discussed item today is a new, detailed feature proposal:

- **#2180 [OPEN] Build "AI Collaborator" Form:** Introduce Natural Language Command Bar and Task Dispatch Console for Cross-Model Orchestration and Project-Level Memory.
    - **Author:** woxinsj
    - **Relevance:** This is a significant community-driven proposal to transform LobsterAI from a low-level toolset into a full "AI Collaborator" platform for non-expert programmers.
    - **Link:** [Issue #2180](https://github.com/netease-youdao/LobsterAI/issues/2180)
    - **Analysis:** The underlying need is clear: users want a more intuitive, higher-level interface that can orchestrate multiple models and maintain persistent project memory. This signals a desire for the project to move beyond chat interfaces toward a more structured agentic framework.

### 5. Bugs & Stability
**No new bugs were reported today.** The three previously open issues were closed as stale, likely due to no recent activity or resolution. They represent low-severity, historical bugs that have been cleaned up.

- **#1487 [CLOSED]** Python script invocation issues in sessions. (Low Severity)
- **#1471 [CLOSED]** Input draft content loss due to debounce timing on view switch. (Medium Severity, UX)
- **#1472 [CLOSED]** Re-editing history messages silently overwrites current input. (Medium Severity, UX)

**No fix PRs exist** for these issues; they were closed due to staleness.

### 6. Feature Requests & Roadmap Signals
One major feature request surfaced today:

- **Feature:** AI Collaborator Platform (Issue #2180)
- **Signal:** This feature request is very detailed (includes an attached proposal document) and is the **only open issue**. It strongly suggests that the user community is looking for **cross-model orchestration and persistent memory**, moving beyond simple chat.
- **Prediction:** While this is a large feature, the maintainers may begin a design discussion or seek further community feedback in the coming weeks. The artifact sharing feature released yesterday aligns with making LobsterAI more capable of handling complex workflows, which is a stepping stone toward this vision.

### 7. User Feedback Summary
- **Satisfaction:** The release of multi-format artifact sharing (Word, PPT, Excel, PDF) is likely a high-satisfaction feature, addressing a key pain point for users who need to generate and share professional documents.
- **Pain Points (Resolved):** Historical bugs regarding input data loss (draft persistence, overwriting on edit) have been acknowledged and remain in the closed backlog. Users may still encounter these in older versions.
- **Unmet Needs:** The opening of Issue #2180 highlights that advanced users are pushing for a **unified command interface and task-based agent orchestration**, which is not currently available.

### 8. Backlog Watch
**No critical, unanswered Issues or PRs require immediate maintainer attention today.**

- **Notable Watch:** Issue **#2180** (the AI Collaborator proposal) is brand new and has received no maintainer response yet. As the only open issue, it should be triaged promptly to acknowledge the community investment in the proposal.
- **No stale PRs** require attention.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-20

## 1. Today's Overview

CoPaw shows **very high activity** with 11 issues and 17 PRs updated in the last 24 hours, indicating a major development sprint is underway. The project accepted **6 closed/merged PRs** addressing critical stability bugs (ChromaDB memory bloat, cron job misfires, agent reply timeouts) while 11 PRs remain open. **No new releases** were cut today, suggesting the team is consolidating fixes from the v1.1.12.post1 release cycle. A notable influx of **first-time contributors** (4 distinct new authors) submitted quality PRs, signaling healthy community engagement. The most concerning trend is **4 separate bug reports** around DeepSeek agent freezes and UI state inconsistencies, which appear to be the team's top priority.

## 2. Releases

**No new releases today.** The latest tagged version remains v1.1.12.post1. Given the volume of fixes in the PR pipeline—especially ChromaDB index management, Zhipu provider fixes, and UI stuck-state corrections—a **v1.1.13 patch release** is likely imminent within 3–5 days.

## 3. Project Progress

**6 PRs were merged or closed today:**

| PR | Author | Summary |
|----|--------|---------|
| [#5242](https://github.com/agentscope-ai/CoPaw/pull/5242) | lecheng2018 | **fix(compaction):** Added timeout protection to `agent.reply()` in `_compact_context()` to prevent UI freezes during LLM API hangs |
| [#5241](https://github.com/agentscope-ai/CoPaw/pull/5241) | lecheng2018 | **fix(cron):** Increased `misfire_grace_seconds` from 60→3600 to prevent APScheduler silently skipping jobs during long agent tasks |
| [#5179](https://github.com/agentscope-ai/CoPaw/pull/5179) | nguyenthanhthe | **fix(skills):** Expanded trigger keywords for multi-agent collaboration so "团队协作" and related phrases reliably activate teamwork mode |
| [#5332](https://github.com/agentscope-ai/CoPaw/pull/5332) | lecheng2018 | **fix(memory):** Added ChromaDB index maintenance (`compact_index`, `purge_index`, timeout protection) solving the 37GB unbounded growth bug (#4795) |
| [#5338](https://github.com/agentscope-ai/CoPaw/pull/5338) | nguyenthanhthe | **fix(providers):** Zhipu model connection test fix (closed-and-replaced by #5339) |
| [#5337](https://github.com/agentscope-ai/CoPaw/pull/5337) | nguyenthanhthe | **fix(providers):** Alternative Zhipu connection test fix (closed-and-replaced by #5339) |

The ChromaDB fix (#5332) and cron misfire fix (#5241) are the most impactful—they address **persistent crash bugs** that have affected users for weeks.

## 4. Community Hot Topics

### Most Active Discussion
- **[#5329](https://github.com/agentscope-ai/CoPaw/issues/5329) — Mobile sidebar agent switching** (3 comments, 1 day old)
  - User `bob-geek11` accessed QwenPaw backend via mobile browser and found the collapsed sidebar has no agent-switching capability. Immediate follow-up PR [#5334](https://github.com/agentscope-ai/CoPaw/pull/5334) was opened by lecheng2018.
  
- **[#4795](https://github.com/agentscope-ai/CoPaw/issues/4795) — ChromaDB 37GB memory bloat** (3 comments, 22 days old)
  - Long-standing critical issue finally resolved by PR #5332. Root cause identified: ChromaDB `link_lists` growing unbounded. Fix adds index compaction, purging, and timeout protection.

- **[#5328](https://github.com/agentscope-ai/CoPaw/issues/5328) — DeepSeek agent thinking freeze** (2 comments)
  - User reports agents consistently freeze during DeepSeek's "thinking" phase, requiring manual stop+retry. Occurs across web, console, and Tauri. Related to PR #5335 (SSE error event handling).

- **[#5317](https://github.com/agentscope-ai/CoPaw/issues/5317) — Tauri Python path loss** (2 comments)
  - After Tauri update, Conda's built-in Python became inaccessible, breaking custom skill execution. No fix PR yet.

### Underlying Needs
The community is heavily focused on **mobile UX** (sidebar switching, responsive design), **reliability with DeepSeek/third-party providers** (thinking freezes, Zhipu incompatibility), and **long-term memory scaling** (ChromaDB index management).

## 5. Bugs & Stability

### Critical (system crashes or data loss)
| Issue | Summary | Status |
|-------|---------|--------|
| [#4795](https://github.com/agentscope-ai/CoPaw/issues/4795) | ChromaDB index grows to 37GB → memory_search crashes every 30 min | **FIXED** in PR #5332 ✅ |
| [#5328](https://github.com/agentscope-ai/CoPaw/issues/5328) | DeepSeek agent freezes mid-thinking across all channels | **Fix pending** PR #5335 addresses related SSE issue |

### High (functional regressions)
| Issue | Summary | Status |
|-------|---------|--------|
| [#5333](https://github.com/agentscope-ai/CoPaw/issues/5333) | After submitting instruction, agent freezes but textbox stays active (not pause button) | **Fix in PR #5335** (yield failed response event) |
| [#5320](https://github.com/agentscope-ai/CoPaw/issues/5320) | v1.1.12 regression: `send_file_to_user` shows "sent" but no image displayed | **Fix in PR #5324** (inline content-disposition) |
| [#5330](https://github.com/agentscope-ai/CoPaw/issues/5330) | Zhipu provider API test passes but all model connection tests fail | **Fix in PR #5339** (plain string content) |

### Medium (usability impact)
| Issue | Summary | Status |
|-------|---------|--------|
| [#5319](https://github.com/agentscope-ai/CoPaw/issues/5319) | Console always shows "Answers have stopped" | **CLOSED** — resolved by reinstall/restart |
| [#5317](https://github.com/agentscope-ai/CoPaw/issues/5317) | Tauri loses Python path from Conda | **No fix PR yet** |

## 6. Feature Requests & Roadmap Signals

### Likely in v1.1.13
| Feature | Issue/PR | Why likely |
|---------|----------|------------|
| **Mobile sidebar agent switch** | [#5329](https://github.com/agentscope-ai/CoPaw/issues/5329) / [#5334](https://github.com/agentscope-ai/CoPaw/pull/5334) | PR already open, authored by lecheng2018 (core contributor) |
| **Custom model ordering** | [#5267](https://github.com/agentscope-ai/CoPaw/issues/5267) / [#5336](https://github.com/agentscope-ai/CoPaw/pull/5336) | PR open by lecheng2018, aligns with provider config improvements |
| **Real-time SSE push notifications** | [#5322](https://github.com/agentscope-ai/CoPaw/issues/5322) / [#5331](https://github.com/agentscope-ai/CoPaw/pull/5331) | Addresses core UX feedback, PR ready |
| **System tray minimize** | [#5326](https://github.com/agentscope-ai/CoPaw/pull/5326) | Windows UX improvement, PR open |

### Possible Future Features
| Feature | Issue | Notes |
|---------|-------|-------|
| **Agent Office — direct conversation** | [#5327](https://github.com/agentscope-ai/CoPaw/issues/5327) | User wants per-agent chat buttons on agent office page; no PR yet |
| **Todo/Plan progress panel** | [#5323](https://github.com/agentscope-ai/CoPaw/pull/5323) | PR open for native todo_write progress UI during multi-step tasks |
| **Recency-aware memory search** | [#5325](https://github.com/agentscope-ai/CoPaw/pull/5325) | PR adds exponential temporal decay to daily note ranking |

### Roadmap Signal
The pattern of **3 first-time contributors** submitting production-quality fixes (ChromaDB, Zhipu, compaction) suggests the project's architecture is maturing to the point where external developers can debug effectively. The team is prioritizing **stability and provider compatibility** over new features.

## 7. User Feedback Summary

### Pain Points
- **Mobile experience gap**: Users accessing via phone browser (back-alley workaround) find essential features missing (agent switching, compressed sidebar)
- **DeepSeek incompatibility**: Recurring theme — "thinking" freezes, UI state confusion, workaround requires manual stop+continue
- **v1.1.12 regressions**: Image sending broke after upgrade; Zhipu provider broken despite passing API tests
- **Windows Tauri issues**: Python path detection unreliable between Conda environments
- **Long-term scaling anxiety**: 37GB ChromaDB bloat erodes trust in memory system for heavy users

### Satisfaction Signals
- Users proactively attempting **mobile workarounds** (accessing backend via phone browser) shows high engagement
- Multiple users reporting bugs with **detailed reproduction steps and screenshots** (bob-geek11, hyper0x) indicates invested community
- The Zhipu provider bug (#5330) had **3 competing PRs** in one day — shows strong contributor motivation

### Notable Quote
> *"没升级前都是可以正常显示要发送图片的"* (Issue #5320) — User expressing clear expectation that upgrades should not break existing functionality.

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Priority | Reason |
|-------|-----|----------|--------|
| [#4795](https://github.com/agentscope-ai/CoPaw/issues/4795) | 22 days | **Critical** | ChromaDB blight — **FIXED today in #5332** ⚠️ (needs merge and release) |
| [#5267](https://github.com/agentscope-ai/CoPaw/issues/5267) | 3 days | Medium | Custom model ordering has open PR (#5336) but no merge yet |
| [#5317](https://github.com/agentscope-ai/CoPaw/issues/5317) | 2 days | High | Tauri Python path loss blocks skill execution — **no fix PR exists** |
| [#5327](https://github.com/agentscope-ai/CoPaw/issues/5327) | 1 day | Low-Medium | Agent Office UX improvement — no contributor assigned |

### PRs Awaiting Review

| PR | Age | Risk |
|----|-----|------|
| [#5339](https://github.com/agentscope-ai/CoPaw/pull/5339) | 1 day | Low — replaces closed duplicates #5337/#5338; clean fix for Zhipu |
| [#5335](https://github.com/agentscope-ai/CoPaw/pull/5335) | 1 day | **High** — fixes UI freeze bug (#5333) affecting DeepSeek users; should merge ASAP |
| [#5324](https://github.com/agentscope-ai/CoPaw/pull/5324) | 1 day | Medium — restores v1.1.11 image display behavior; regression fix |
| [#5321](https://github.com/agentscope-ai/CoPaw/pull/5321) | 2 days | Medium — new "scroll" context management strategy; needs architectural review |

### Project Health Assessment
**🟢 Good** — Activity metrics are excellent (11 open issues, 11 open PRs, 4 new contributors). However, the **fix pipeline needs consolidation**: 3 PRs address the same Zhipu bug (ended up in 2 close-and-replace cycles), suggesting need for better coordination. The DeepSeek freeze issue (#5328/#5333) is the most urgent unaddressed problem affecting real users. A **patch release (v1.1.13) is warranted within the week** to ship the ChromaDB fix, Zhipu fix, and image regression fix before accumulating more regressions.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-06-20**.

---

## ZeroClaw Project Digest — 2026-06-20

### 1. Today's Overview
The ZeroClaw project is currently in a high-velocity development cycle with significant churn. There are **50 active issues** and **49 open PRs**, indicating a massive amount of concurrent work. Activity is heavily skewed toward the next major milestones (`v0.8.x` and the planned `v0.9.0`), with a strong focus on security (OIDC), infrastructure (multi-DB session backends), and user experience (Discord features, context bars). However, the high number of open items and a regression in prebuilt binaries signal that the project is currently prioritizing new feature development over stability. The lack of a new release this week suggests maintainers are consolidating these large feature branches.

### 2. Releases
**None.** No new releases were created in the last 24 hours. The most recent reference version is **v0.8.0**, which currently has a confirmed regression (see Bugs section).

### 3. Project Progress
Only **1 PR was merged/closed** in the last 24 hours:
- **#7965 (CLOSED)** — A massive PR ([`feat(channels/discord): interaction components`](https://github.com/zeroclaw-labs/zeroclaw/pull/7965)) was closed, completing the Discord interaction surface. This adds buttons, selects, modals, and autocomplete to the Discord channel. This is a major feature landing.

### 4. Community Hot Topics
The most active discussions reveal deep integration and stability concerns:

- **#7787 ([Bug] Prebuilt v0.8.0 binaries ship without Slack/Discord channel features)** — The top issue by comments (6) and reactions. Users are blocked on a regression where the official binaries are compiled without Slack/Discord support. This is causing immediate friction for anyone using the standard distribution. ([Link](https://github.com/zeroclaw-labs/zeroclaw/issues/7787))
- **#5844 ([Bug]: Too much emphasis on memory)** — A long-running discussion (6 comments) about agent behavior where system prompts are dominated by historical memory over immediate user intent. This points to a core UX frustration. ([Link](https://github.com/zeroclaw-labs/zeroclaw/issues/5844))
- **#7141 ([Feature]: OIDC Authentication Provider support)** — A high-value feature request (5 comments) for enterprise-grade authentication. This is a key blocker for production deployments. ([Link](https://github.com/zeroclaw-labs/zeroclaw/issues/7141))

### 5. Bugs & Stability
Bugs are the dominant concern, with multiple S1 (workflow blocked) issues active.

**High Severity (S1/Degraded):**
- **#7787 (OPEN)** — [Prebuilt v0.8.0 binaries ship without Slack/Discord features](https://github.com/zeroclaw-labs/zeroclaw/issues/7787). This is the most critical bug today, effectively breaking the core channel functionality for binary users.
- **#6037 (OPEN)** — [Cron jobs launched repeatedly while still running](https://github.com/zeroclaw-labs/zeroclaw/issues/6037). A runtime reliability issue causing burst executions of scheduled tasks.
- **#7907 (OPEN)** — [Agent rename moves state before config persistence](https://github.com/zeroclaw-labs/zeroclaw/issues/7907). Data loss risk during agent management operations.
- **#7941 (OPEN)** — [Agent delete purges state before config persistence](https://github.com/zeroclaw-labs/zeroclaw/issues/7941). Mirror of #7907, same data loss pattern.

**Medium Severity (S2):**
- **#5869 (OPEN)** — [Security advisory cluster from rumqttc dependency](https://github.com/zeroclaw-labs/zeroclaw/issues/5869). Blocked by upstream library, but flagged as critical for security compliance.
- **#5808 (OPEN)** — [Default context budget exceeded immediately](https://github.com/zeroclaw-labs/zeroclaw/issues/5808). System prompt + tools exceed the 32k default budget by 3.3x, causing perpetual trimming.

**Notable fix PRs exist for:**
- **#8004** actively addresses the budget config being frozen at boot.
- **#8009** fixes tool receipts not being wired through non-channel turn paths.

### 6. Feature Requests & Roadmap Signals
The roadmap is clearly visible in the tracker issues and large RFCs:

**Likely for v0.8.3 / v0.9.0:**
- **[#7141] OIDC Authentication Provider** — High probability of landing in v0.9.0 given the dedicated tracker ([#7432](https://github.com/zeroclaw-labs/zeroclaw/issues/7432)).
- **[#7759] Decouple WebSocket from agent turn lifecycle** — Critical for web UI stability; listed as P1.
- **[#7929] Unified slash-command registries** — A significant architectural improvement to reduce code duplication across the web, TUI, and channel runtime.
- **[#7996] Configurable temporary-file cleanup** — A practical feature for low-end device deployments.

**Speculative / Long-Term:**
- **[#7950] Include docs in Docker images** — A user request suggesting current agents can't answer setup questions, implying a desire for offline documentation.
- **[#6893] Multi-database session backends (Postgres, Oracle, MySQL)** — An XL PR that is still open, indicating a complex infrastructure feature likely targeted for a later major release.

### 7. User Feedback Summary
User sentiment reflects a mix of enthusiasm for new features and frustration with stability:

- **Pain Point (High Impact):** The `v0.8.0` binary regression (`#7787`) is causing the most immediate dissatisfaction, forcing users to compile from source or downgrade.
- **Pain Point (UX):** The "memory over current prompt" issue (`#5844`) suggests that the agent's core reasoning logic needs tuning, especially for cron jobs where context switching is poor.
- **Use Case (Enterprise):** Requests for OIDC support (`#7141`) and multi-DB backends (`#6893`) indicate growing enterprise interest, but these users are likely blocked by the lack of auth and production-ready databases.
- **Use Case (Embedded/Edge):** Issues regarding Android Termux (`#7911`) and Temp File Cleanup (`#7996`) show a push for running ZeroClaw on constrained hardware.

### 8. Backlog Watch
Several important items risk falling through the cracks:

- **#5869 (OPEN)** — [`security: rumqttc v0.25.1 pins vulnerable dependencies`](https://github.com/zeroclaw-labs/zeroclaw/issues/5869). Tagged as **P1** and **blocked**, but this is a compliance risk (4 RUSTSEC advisories). It requires a library replacement or upstream fix.
- **#6037 (OPEN)** — [`[Bug] Cron jobs can be launched repeatedly`](https://github.com/zeroclaw-labs/zeroclaw/issues/6037). An S1 bug that has only 1 comment and no assigned PR. Given the emphasis on cron in the community, this is under-prioritized.
- **#6893 (OPEN)** — [`feat(infra): multi-database session backends`](https://github.com/zeroclaw-labs/zeroclaw/pull/6893). An XL PR requiring significant review capacity. It has no recent maintainer activity, suggesting it may be stalled or de-prioritized despite being open for a month.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*