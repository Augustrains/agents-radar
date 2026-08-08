# OpenClaw Ecosystem Digest 2026-08-08

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-08 00:41 UTC

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

Based on the GitHub data provided for OpenClaw (github.com/openclaw/openclaw) on 2026-08-08, here is the project digest:

---

## OpenClaw Project Digest — 2026-08-08

### 1. Today's Overview
OpenClaw is experiencing a period of very high activity and intense maintainer engagement. With 500 issues and 500 PRs updated in the last 24 hours, the project is in a heavy development and triage cycle. A clear focus is on critical stability and data-integrity issues marked as P0 and P1, particularly concerning session state, memory leaks, and database corruptions. The maintainers are actively reviewing a large volume of PRs, many requiring more proof or waiting on the author, indicating a rigorous quality bar. Notably, there is a prolific 12-layer "Code Mode frontier stack" of PRs being pushed by a single author, suggesting a major feature is being landed piecemeal.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
The project is heavily focused on bug fixes and stability improvements rather than new features. Key areas of progress visible through open PRs include:
- **UI/UX Fixes:** Multiple PRs address Web UI issues, such as clearing stale error highlights (#120391), settling stale `hasActiveRun` rows (#120396), and refreshing attributed message avatars (#120381).
- **Channel-Specific Fixes:** Significant work is going into fixing regressions and behavior bugs, including handling Slack Enterprise Grid workspace routing (#120087) and preserving channel context in Slack bot-opened threads (#119023).
- **Agent/Backend Reliability:** A large series of PRs (e.g., #119892, #119833, #119813) are part of a "Code Mode frontier stack," which aims to expose auditable traces and improve execution accounting for the agent runtime. Other PRs focus on retrying the same auth profile before rotating (#95676) and preventing premature compaction (#95885).
- **Gateway & CLI Stability:** PRs are in progress to recover the managed gateway after a failed CLI update (#119516) and to scope launchd ownership checks to avoid false failures (#117616).

### 4. Community Hot Topics
The most active discussions highlight severe pain points, but several have actionable fixes in progress:

- **[#116277]** **DeepSeek v4 Flash silent reply failure** (128 comments) - This high-severity bug, marked as `diamond lobster`, has the highest engagement. Users are clearly frustrated by silent failures with no observability. This is a critical UX issue.
- **[#91588]** **Gateway Memory Leak (15.5GB RSS)** - This critical P0 bug has been open since June. The community is closely watching this issue, as OOM crashes and restart cycles severely impact reliability for those running the gateway long-term.
- **[#101290]** **CLI startup corrupting live state DB** - Another P0 regarding data loss (`database disk image is malformed`). This is a major concern for users on macOS. The fact that it's tagged `clawsweeper:no-new-fix-pr` and `needs-product-decision` suggests a complex problem with no clear solution yet.
- **[#45608]** **Pre-reset agentic memory flush** - This feature request with 4 👍 has a healthy discussion about preserving memory across session resets.

### 5. Bugs & Stability
There is a significant backlog of critical and high-severity bugs, with many new ones reported today. The most critical themes are data loss, crash loops, and silent message loss.

**P0 (Critical) Issues:**
- **[#119263]** **Agent DB v14->v15 migration fails**, blocking gateway startup entirely. (New)
- **[#118772]** **Embedded-agent-runner totalTokens inflation causing premature compaction**, resulting in data loss. (New)
- **[#91588]** **Gateway memory leak** leading to OOM crashes (Long-standing).

**P1 (High) Issues:**
- **[#119411]** **Memory file watcher never reindexes**, silently freezing the memory index. (New)
- **[#119333]** **`request_user_input` tool exposed in Default mode but rejected at runtime.** (New)
- **[#119009]** **Runaway model-call retry loop incurred a $204 cost** without being detected by observability tools. (Closed today).
- Many other P1s are updated, including issues with message loss on LINE (#86012), silent failures with the `claude-cli` backend (#90789), and session state corruption (#86684).

A positive sign is that many of these issues have linked open PRs (e.g., #118772, #119263, #119009), indicating the maintainers are actively working on fixes.

### 6. Feature Requests & Roadmap Signals
While bugs dominate the current activity, several feature requests point toward future enhancements:
- **[#99583]** **Intelligent Session Auto-Titling** - A proposal to automatically title sessions, indicating a push for more proactive/intelligent session management.
- **[#95516]** **Skill Lifecycle Management** - Suggests a move toward more autonomous self-optimization, including auto-retirement of unused skills.
- **[#13219]** **Per-model usage logging** - A common and practical request for better cost tracking and observability.
- **[#81061] & [#87362]** **Hook/Event system enhancements** - Requests to expose more lifecycle events to enable custom plugins and observability.

**Likely Next Version:** Given the sheer volume of P0/P1 bug fixes in flight (especially around state management and stability), the next release will likely be a critical stability patch focused on fixing the database migration error, the token inflation bug, and the gateway memory leak. The massive "Code Mode" PR stack suggests a major feature for auditable agent execution is also on the horizon.

### 7. User Feedback Summary
User sentiment is polarized. The most vocal users are reporting severe stability and reliability issues, often with financial or data-loss implications (e.g., $204 billing runaway in #119009). There is a clear demand for more observable behavior, as many bugs manifest as "silent failures" with no diagnostics. The project’s own labeling system (e.g., `diamond lobster`, `recovery-stuck`) reflects the high impact of these issues. However, the active engagement and the fact that users are filing and commenting on issues suggests a strong, deeply technical user base that depends on the project and is willing to invest time in reporting issues.

### 8. Backlog Watch
Several important issues remain open for a long time without a clear fix path, requiring maintainer attention:
- **[#30381]** **`chatCompletions` ignoring request model when agent-id header is present** - Open since March, this API behavior issue has low community engagement but represents a core logic bug for API users.
- **[#13219]** **Per-model usage logging** - An open feature request from February that remains a popular ask for better cost tracking.
- **[#52186]** **TTS provider conflict (ElevenLabs vs OpenAI)** - Open since March, this is a confusing UX bug where the wrong voice is played, indicating a deeper routing issue.
- **[#74378]** **CLI processes remain alive as node.exe on Windows** - A regression from April that continues to plague Windows users, potentially affecting their workflow on every command execution.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-08 | **Scope:** 12 projects in the personal AI assistant / agent open-source ecosystem

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a **stabilization phase following rapid feature expansion**. Across all active projects, the dominant theme is **reliability engineering**: fixing silent failures, memory leaks, session-state corruption, and tool-execution bugs that erode user trust. A second major trend is **security hardening**—workspace isolation, sandboxing, SSRF guards, and path-containment validation appear across NanoBot, Hermes, OpenClaw, ZeroClaw, and IronClaw simultaneously. Projects are converging on shared architectural patterns (session persistence, plugin/skill systems, multi-channel adapters) while differentiating on platform focus (desktop vs. headless, consumer vs. enterprise, cloud vs. edge). The ecosystem shows healthy community engagement with sophisticated users filing detailed bug reports, contributing code reviews, and proposing architectural RFCs. Notably, **no project published a stable release today**, suggesting a coordinated pre-release stabilization window across the ecosystem.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Merged/Closed PRs | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | Not specified | No new release | 3.5/5 — High activity, critical P0/P1 backlog |
| **NanoBot** | 10 | 21 | 11 | No new release | 4.0/5 — Strong velocity, responsive maintainers |
| **Hermes Agent** | 50 | 50 | 3 | v0.20.0 (recent) | 3.5/5 — High activity, quick fix turnaround |
| **PicoClaw** | 4 | 14 | 2 | No new release | 2.5/5 — Moderate, stale-label concerns |
| **NanoClaw** | 0 | 10 | 2 | No new release | 2.5/5 — Steady, review bottleneck |
| **NullClaw** | 0 | 0 | 0 | — | 1/5 — Inactive |
| **IronClaw** | 50 | 50 | 12 | No new release | 3.5/5 — High-intensity hardening |
| **LobsterAI** | 7 | 7 | 6 | **2026.8.7 published** | 4.0/5 — Healthy cadence, responsive |
| **TinyClaw** | 0 | 0 | 0 | — | 1/5 — Inactive |
| **Moltis** | 0 | 0 | 0 | — | 1/5 — Inactive |
| **CoPaw** | 31 | 49 | 22 | v2.1.0-beta.2 (recent) | 4.0/5 — Very high merge velocity |
| **ZeroClaw** | 50 | 50 | 3 | No new release | 3.0/5 — High activity, heavy review load |
| **ZeptoClaw** | 0 | 0 | 0 | — | 1/5 — Inactive |

*Health score: composite of activity level, responsiveness, community engagement, and stability indicators.

---

## 3. OpenClaw's Position

### Advantages vs. Peers
- **Scale of community engagement:** With 500 issues and 500 PRs updated in 24 hours, OpenClaw's community is an order of magnitude larger than any peer. This provides extensive test coverage, rapid bug discovery, and a deep contributor pool.
- **Ecosystem gravity:** The prevalence of "OpenClaw-compatible" configuration and plugin patterns in peer projects (LobsterAI explicitly integrates OpenClaw config, PicoClaw and NanoClaw carry the "Claw" naming lineage) indicates OpenClaw has become the **de facto reference implementation**.
- **Multi-platform depth:** Active work on Slack Enterprise Grid routing, LINE, WeChat, and other channels shows breadth unmatched by peers.

### Technical Approach Differences
- **Agentic memory architecture:** OpenClaw's focus on "Code Mode frontier stack" (auditable traces, execution accounting) suggests a more rigorous approach to agent observability than peers.
- **State management complexity:** The high volume of session-state, DB migration, and memory-leak issues indicates OpenClaw operates at a **scale of data complexity** (500+ concurrent issues) that smaller projects haven't reached.

### Community Size Comparison
| Metric | OpenClaw | Next Largest (Hermes/IronClaw) |
|---|---|---|
| Issues updated/24h | 500 | 50 |
| PRs updated/24h | 500 | 50 |
| Longest-running critical bug | June 2026 | June 2026 |
| New feature PR stack | 12-layer stack | 1-3 layer stacks |

**Verdict:** OpenClaw is the **ecosystem leader by community size and activity**, but this scale brings coordination costs—visible in the P0/P1 backlog and "needs-product-decision" tagged items.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging **independently across multiple projects**, signaling ecosystem-level needs:

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **Token/Cost Transparency** | OpenClaw (#13219), NanoBot (#5266), Hermes (#65365), IronClaw (#6989) | Per-model usage logging, cost burn detection, budget enforcement, runaway-loop prevention |
| **Session State Integrity** | OpenClaw, Hermes, NanoBot, IronClaw | Cross-platform session continuity, compression safety (don't drop in-flight tools), state DB corruption prevention |
| **Security Isolation** | NanoBot (#5278, #5276), ZeroClaw (#9815), Hermes (#80847), IronClaw (#7214) | Workspace isolation, per-session sandboxing, path-containment validation, SSRF guards, approval-bypass prevention |
| **Tool-Call Reliability** | OpenClaw, ZeroClaw (#9820, #9821), CoPaw (#6803), PicoClaw (#3279) | Models emitting pseudo-tool-call syntax, silent tool failures, strict provider schema validation |
| **Channel Parity** | PicoClaw (#3307), Hermes (#4335), NanoClaw (#3199), IronClaw (#7344) | Session management across all channels, WhatsApp/Telegram feature parity, unified state across platforms |
| **Observability/Debugging** | OpenClaw, IronClaw (#7369), ZeroClaw (#8933), NanoBot | Trace capture on error, OTel correlation, failure-reason display, auditable agent execution |
| **Provider Breadth** | CoPaw (#6490), LobsterAI (#2443), PicoClaw (#3271), OpenClaw | More built-in providers, slashed-model-ID support, dynamic model catalogs, provider schema validation |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architecture Strengths | Key Differentiator |
|---|---|---|---|---|
| **OpenClaw** | Full-featured universal assistant | Developers, power users | Multi-channel, agentic memory, plugin ecosystem | **Ecosystem leadership, community scale** |
| **NanoBot** | Lightweight, secure assistant | Privacy-conscious users, edge deployments | Per-session sandboxing, workspace isolation, security-first design | **Security architecture** |
| **Hermes Agent** | Orchestration and delegation | Teams, Kanban workflow users | Kanban workers, delegation, multi-profile collaboration | **Multi-agent organizational model** |
| **PicoClaw** | Low-resource assistant | Budget-conscious, embedded ($10 hardware) | Lightweight, goroutine-based, edge-optimized | **Resource efficiency** |
| **NanoClaw** | Channel-extensible assistant | Multi-platform integrators | v2 ChannelAdapter architecture, skill system | **Channel abstraction layer** |
| **IronClaw** | Production hardening | Enterprise, automation-heavy | Tool disclosure, doc-truth pipeline, sandbox profiles | **Quality gates, security posture** |
| **LobsterAI** | Desktop/IDE-integrated assistant | ML/LLM researchers (Chinese market) | Electron desktop, OpenClaw config compatibility, IM analytics | **Desktop UX, Chinese ecosystem integration** |
| **CoPaw** | Mobile/consumer assistant | Consumer users, multi-platform | ReMe memory, mailbox assistant, OneBot/WeChat integration | **Consumer accessibility, memory innovation** |
| **ZeroClaw** | Rust-based headless automation | Automation engineers, cron workflows | SOP execution, daemon architecture, security containment | **Rust performance, headless-first design** |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (High Velocity, High Responsiveness)
| Project | Signals |
|---|---|
| **CoPaw** | 22 PRs merged/closed in 24h, 11 issues closed, new contributors onboarding |
| **NanoBot** | 11 PRs merged, 24h turnaround on reported regressions, security-conscious community |
| **LobsterAI** | 6 of 7 PRs merged, release published today, immediate fix PRs for reported bugs |

### Tier 2: High Activity, Stabilizing
| Project | Signals |
|---|---|
| **OpenClaw** | Massive activity, but P0/P1 backlog and "needs-product-decision" tags suggest coordination overhead |
| **Hermes** | 50/50 issues/PRs, quick fixes for P1s, but Windows reliability cluster unresolved |
| **IronClaw** | 12 PRs merged, bug_bash_P1 QA process, doc-truth pipeline — structured hardening |
| **ZeroClaw** | High activity, 47 open PRs, heavy review load, P1 bug cluster — validating architectural phase |

### Tier 3: Moderate, Review-Bottlenecked
| Project | Signals |
|---|---|
| **PicoClaw** | Community contributions high-quality, but stale-labeling and unaddressed PRs (38-day old #3200) block momentum |
| **NanoClaw** | 8 open PRs awaiting review, 3-month-old silent-failure fix unaddressed |

### Tier 4: Inactive
| Project | Signals |
|---|---|
| **NullClaw, TinyClaw, Moltis, ZeptoClaw** | No activity in 24h; may be dormant or in long-cycle development |

---

## 7. Trend Signals

### Signal 1: The "Silent Failure" Crisis
Across **five projects** (OpenClaw, NanoBot, Hermes, ZeroClaw, CoPaw), the most damaging bugs are **failures with no observable signal**: messages dropped, tokens burned, models hallucinating connectivity status, tools silently mis-executing. Users are demanding **observability as a feature**, not an afterthought.

**Value for developers:** Build activity/telemetry into the agent core from day one—per-call token logs, error traces, state-change audit trails. Users will trust agents that explain themselves.

### Signal 2: Security Is Now a User-Led Requirement
Multiple security issues were **raised by end users, not maintainers**: NanoBot's session-history leak (#5278), ZeroClaw's forbidden_paths bypass (#9815), IronClaw's sandbox escape concerns. The community is threat-modeling their own deployments and demanding defense-in-depth.

**Value for developers:** Treat workspace isolation, path validation, and permission boundaries as first-class features with explicit documentation, not implicit implementation details.

### Signal 3: The Cost-Control Imperative
"Millions of tokens in 2 hours" (NanoBot), "$204 runaway retry loop" (OpenClaw), "$0.00 spend reporting" (ZeroClaw)—**users cannot manage what they cannot measure**. Cost transparency is becoming a competitive differentiator.

**Value for developers:** Implement per-call token accounting, budget caps, and anomaly detection as core features. Users will choose agents they can afford to run unattended.

### Signal 4: Tool-Calling Contract Instability
Multiple models (Llama via NIM, Gemini, StepFun) are **rejecting or misinterpreting tool schemas** across ZeroClaw, CoPaw, and IronClaw. The tool-calling contract is not yet stable across the model ecosystem.

**Value for developers:** Build provider-agnostic tool-schema validation, test against strict API vendors, and implement graceful fallback when models emit non-standard tool-call syntax.

### Signal 5: The "Unattended Autonomy" Wall
Cron-triggered SOPs stalling (ZeroClaw), background agents burning tokens (NanoBot), Kanban zombies (Hermes), runaway retry loops (OpenClaw)—**the ecosystem is hitting the reliability wall of true unattended operation**.

**Value for developers:** The next competitive frontier is **dependable background execution**: health checks, keep-alives, dead-man switches, and automated recovery. Users want agents that work while they sleep.

### Signal 6: Channel Parity Is Table Stakes
Users are demanding **consistent session management, media support, and access control across every channel** (Telegram, WhatsApp, Slack, WeChat, Discord, Mattermost). Siloed channel experiences are no longer acceptable.

**Value for developers:** The channel abstraction layer is the new API surface. Invest in uniform channel capabilities and parity testing.

---

## Summary

The ecosystem is **consolidating around OpenClaw as the reference** while specialized projects (NanoBot security, ZeroClaw Rust performance, CoPaw consumer UX, LobsterAI desktop) carve out niches. The immediate technical priorities across the board are **reliability, observability, security, and cost control in unattended operation**. Projects that solve the silent-failure and cost-transparency problems will gain disproportionate user trust, while those that maintain developer velocity without accumulating P0 backlogs will set the standard for sustainable growth.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-08

## 1. Today's Overview

NanoBot is experiencing a high-activity development cycle, with 21 pull requests updated in the last 24 hours (11 merged/closed) and 10 issues touched (8 still open). The project shows a strong focus on security hardening, channel-specific reliability fixes, and session/persistence architecture improvements. Notable themes include per-session sandboxing and workspace isolation (PRs #5279, #5283, #5276), which indicate a deliberate push toward a more secure, multi-tenant-ready design. The merge velocity is high, with maintainers closing out numerous WebUI regressions and dependency documentation fixes, while longer-running feature work (computer use tools, Telegram polling recovery) continues to mature.

## 2. Releases

No new releases were published in the last 24 hours. The project appears to be in a pre-release stabilization phase, with multiple security and bug-fix PRs landing concurrently.

## 3. Project Progress

**Merged/Closed PRs (11 total)** — key items that advanced the codebase:

- **Session & Memory Integrity**: 
  - [#5272](https://github.com/HKUDS/nanobot/pull/5272) — Fixed session retention trimming dropping proactive channel delivery messages (fixes #5273). Critical for cron notifications and job deliveries.
  - [#5280](https://github.com/HKUDS/nanobot/pull/5280) and [#5231](https://github.com/HKUDS/nanobot/pull/5231) — Archive short idle sessions for Dream, ensuring the memory agent gets input from otherwise-invisible short sessions.
- **WebUI Fixes**: 
  - [#5285](https://github.com/HKUDS/nanobot/pull/5285) — Preserves newly created topic route, fixing a regression where optimistic UI updates could lose the current topic.
  - [#5284](https://github.com/HKUDS/nanobot/pull/5284) — Removed the legacy `/api/sessions/{key}/messages` route (no longer has a supported caller).
  - [#5281](https://github.com/HKUDS/nanobot/pull/5281) — Crisper activity text in the WebUI with better edge fading.
  - [#5268](https://github.com/HKUDS/nanobot/pull/5268) — Fixed `media_urls` not being staged for out-of-media-root attachments on history reads (fixes #5264).
  - [#5277](https://github.com/HKUDS/nanobot/pull/5277) — Inline model preset editor expansion.
- **Channel Stability**: 
  - [#5263](https://github.com/HKUDS/nanobot/pull/5263) — Hardened WeChat protocol delivery, streaming, and login against the upstream `openclaw-weixin` 2.4.6. Significant reliability investment.
  - [#5287](https://github.com/HKUDS/nanobot/pull/5287) — Preserved global `sendProgress`/`sendToolHints` defaults for channels without explicit overrides.
- **Docs/Onboarding**: 
  - [#5282](https://github.com/HKUDS/nanobot/pull/5282) — Modernized dependency recovery guidance to use `nanobot plugins enable ...` instead of stale direct-package installs.

**PRs with Notable Behavior Changes** (merged yesterday but impact today):
- [#5280](https://github.com/HKUDS/nanobot/pull/5280) — **Behavioral change**: idle session archiving now runs even when the entire session fits inside the protected suffix window, meaning Dream will now process more short sessions than before.

## 4. Community Hot Topics

- **[#5266 — Token consumption logging](https://github.com/HKUDS/nanobot/issues/5266)** (10 comments) ⭐ **Hottest Issue**: User reports millions of tokens consumed in 2 hours with no visible activity. This is a significant trust/operational concern. Request is for detailed per-call token logging. *Underlying need*: Cost transparency and debugging tool for unexpected usage. No linked PR yet — a strong candidate for a near-term feature.

- **[#5288 — Agent Plugins integration with CLI Apps](https://github.com/HKUDS/nanobot/pull/5288)** (0 comments, but architecturally significant): Introduces a unified package boundary for portable Agent Skills and MCP servers, replacing ad hoc workspace skills from CLI-Anything catalog installs. This is a major architecture evolution and likely to generate discussion once reviewers engage.

- **[#5149 — No audio on WhatsApp](https://github.com/HKUDS/nanobot/issues/5149)** (5 comments): Persistent channel bug — bot receives but cannot send audio via WhatsApp. Includes a `neonize.utils.ffmpeg` warning, suggesting a codec/ffmpeg pipeline issue. Unresolved for 11 days.

- **[#5198 — Model switching in-session broken](https://github.com/HKUDS/nanobot/issues/5198)** (3 comments): `/model` command seemingly does not switch models; fallback-only behavior confuses users. Core UX issue for power users.

- **[#5256 — `/goal` message loop](https://github.com/HKUDS/nanobot/issues/5256)** (1 comment): Dozens of near-identical replies generated while waiting for user input. Suggests a loop-detection weakness in the agent loop.

**Security-adjacent topics gaining traction**:
- **[#5278 — Session history inside workspace](https://github.com/HKUDS/nanobot/issues/5278)** and **[#5276 — Per-session temporary file isolation](https://github.com/HKUDS/nanobot/issues/5276)**: Both flagged by the same reporter (`whisperity`/`lmzopq`), these highlight a real security design flaw: agent workspace contains session history readable by the agent itself. Fix PRs exist (#5279, #5283).

## 5. Bugs & Stability

Ranked by severity:

1. **HIGH — Session history reachable by agent** ([#5278](https://github.com/HKUDS/nanobot/issues/5278)): With `restrict_to_workspace` enabled, an agent can read session history files including potentially sensitive prior conversations, API keys in prompts, or tool outputs. **Fix PR exists**: [#5279](https://github.com/HKUDS/nanobot/pull/5279) moves session storage outside the workspace. **Mitigation needed urgently** for any deployment relying on workspace isolation as a security boundary.

2. **HIGH — Token burning without visible activity** ([#5266](https://github.com/HKUDS/nanobot/issues/5266)): Million-token burns in hours with no user interaction suggest a background loop, possibly related to the `/goal` loop issue (#5256) or background agents. **No fix yet** — needs immediate maintainer investigation.

3. **MEDIUM — `/goal` message flooding** ([#5256](https://github.com/HKUDS/nanobot/issues/5256)): Dozens of repeated replies while waiting for user input. Likely loop-detection logic failure. **No fix PR yet.**

4. **MEDIUM — Session trimming drops proactive delivery** ([#5273](https://github.com/HKUDS/nanobot/issues/5273)): Cron notifications and job deliveries lost when retention trimming runs. **Fixed** in [#5272](https://github.com/HKUDS/nanobot/pull/5272) (merged).

5. **MEDIUM — WhatsApp audio send broken** ([#5149](https://github.com/HKUDS/nanobot/issues/5149)): 11 days open, no fix PR. ffmpeg pipeline issue likely.

6. **LOW-MEDIUM — Server-side model switching broken** ([#5198](https://github.com/HKUDS/nanobot/issues/5198)): `/model` command seems non-functional; contradicts user's mental model of explicit override.

7. **LOW — Matrix thread isolation** ([#5286](https://github.com/HKUDS/nanobot/pull/5286)): **Fix PR open**; threads currently share sessions, causing context bleed.

## 6. Feature Requests & Roadmap Signals

**Clear "next version" signals** (PRs already in flight):
- **Per-session sandbox isolation** ([#5283](https://github.com/HKUDS/nanobot/pull/5283)): Opt-in `per_session_sandbox` mode giving each non-WebUI session a private filesystem. Complements #5279. Expect this in the next minor release.
- **Session history outside workspace** ([#5279](https://github.com/HKUDS/nanobot/pull/5279)): Security-driven relocation of session storage.
- **Agent Plugins + CLI Apps unification** ([#5288](https://github.com/HKUDS/nanobot/pull/5288)): A single package boundary for skills/MCP servers. This is a substantial architecture change that likely lands in a major version.
- **Subagent transcript persistence** ([#5291](https://github.com/HKUDS/nanobot/pull/5291)): Background subagent conversations will be reviewable — valuable for debugging and auditing.

**User-requested with no PR yet (roadmap candidates)**:
- **Token consumption logging** ([#5266](https://github.com/HKUDS/nanobot/issues/5266)): Per-call token usage in logs. High-value observability feature.
- **Session-level file isolation** ([#5276](https://github.com/HKUDS/nanobot/issues/5276)): Beyond sandboxing, users want per-session file namespaces.

**Long-running feature work still open**:
- [#4276](https://github.com/HKUDS/nanobot/pull/4276) — Computer use + browser tools (58 days open, low review engagement).
- [#5252](https://github.com/HKUDS/nanobot/pull/5252) — Temporary chat mode in WebUI (non-persistent chats).

## 7. User Feedback Summary

**Pain points expressed**:
- **Cost anxiety**: "Million tokens in 2 hours" without visible activity — most alarming feedback this cycle. Users need cost controls and telemetry.
- **Security consciousness**: Two separate users (`whisperity`, `lmzopq`) independently raised workspace/session isolation concerns. This is a power-user segment that understands the threat model and wants defense-in-depth.
- **Channel reliability**: WhatsApp audio send is a long-standing gap; Telegram polling stalls cause silent message loss ([#5156](https://github.com/HKUDS/nanobot/pull/5156) fixes this, but for how long?).
- **Model control frustration**: Explicit user intent to switch models is ignored in favor of fallback behavior — UX mismatch with cloud AI expectations.

**Satisfaction signals**:
- High merge velocity and quick turnarounds on reported regressions (e.g., #5273 → fix within 24 hours; #5264 → fix within 24 hours).
- Maintainers are actively closing WebUI regressions, suggesting strong QA coverage post-refactor.

## 8. Backlog Watch

**Issues needing maintainer attention** (open > 7 days, unresolved):
- **[#5149 — WhatsApp audio send](https://github.com/HKUDS/nanobot/issues/5149)** (11 days, 5 comments): Channel capability gap; users on WhatsApp cannot receive audio responses. Needs a maintainer to triage the ffmpeg/codec path.
- **[#5198 — In-session model switching](https://github.com/HKUDS/nanobot/issues/5198)** (8 days, 3 comments): Core feature expectation vs. actual behavior. If `/model` is not supported as an override, documentation should say so; if it is, this needs a fix.

**PRs needing review engagement**:
- **[#4276 — Computer use/browser tools](https://github.com/HKUDS/nanobot/pull/4276)** (58 days open, unanswered review requests): Large, complex feature (PyAutoGUI backend, Playwright browser). Risk of bit-rotting; maintainers should either commit to reviewing or explicitly defer.
- **[#5156 — Telegram polling recovery](https://github.com/HKUDS/nanobot/pull/5156)** (10 days open): Fixes silent production issue (permanently stalled polling). **This should be prioritized** — silent message loss is a trust killer.

**Data hygiene opportunity**:
- **[#5290 — Deduplicate atomic JSONL write idiom](https://github.com/HKUDS/nanobot/issues/5290)**: Three copies of the same code pattern. Low-risk refactor; signals good code quality awareness from the community.

---

**Overall assessment**: NanoBot is in a healthy, security-conscious iteration phase. The community is engaged, maintainers respond quickly to critical bugs, and architectural improvements (sandboxing, session isolation, plugin format) are being driven by real user needs. The two highest-priority actions for the maintainer team this week: (1) investigate the token-burning issue (#5266) as a potential background-loop bug, and (2) merge the Telegram polling recovery PR (#5156) to prevent silent channel failures.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-08  
**Source:** GitHub (NousResearch/hermes-agent)

---

## 1. Today's Overview

Hermes Agent is showing **high-velocity development** with 50 issues and 50 PRs updated in the last 24 hours. Activity is concentrated on **stability fixes** (particularly around session state management, Kanban worker lifecycle, and gateway crash prevention) alongside **security hardening** (SSRF guards, approval prompt visibility, tool-result storage protection). The project is actively processing a wave of **bug reports from the v0.20.0 release** (dated 2026.08.x), with maintainers responding quickly—multiple P1/P2 severity issues received fix PRs within 1-2 days of reporting. Feature development continues across **WhatsApp parity**, **Teams/multi-profile collaboration**, and **cron job enhancements**, though no new stable release was published today. The issue tracker shows healthy triage with several duplicates being identified (Telegram rich_message handling, TUI gateway crash on Windows), indicating maturing QA processes.

---

## 2. Releases

**No new releases published today.** The most recent version referenced in issue reports is **v0.20.0 (2026.08.x)** and **v2026.8.3**, suggesting an active release cadence within the past week. Issues filed against v0.20.0 (Windows multiple startup entries, Kanban timed-out workers leaving process groups) indicate the latest release is under community validation.

---

## 3. Project Progress

**Merged/Closed PRs Today (3):**

- [#81412 — Add policy fallback delegation to local Qwen](https://github.com/NousResearch/hermes-agent/pull/81412) *(Closed)*: Adds policy-only fallback routing from the primary orchestrator to a local Qwen subagent, including model-reported policy restriction distinction and persistent fallback job states.
- [#74452 — Python 3.14 compatibility for DaemonThreadPoolExecutor](https://github.com/NousResearch/hermes-agent/pull/74452) *(Closed)*: Fixes `_adjust_thread_count()` referencing removed `_initializer`/`_initargs` API, ensuring Python 3.14 compatibility.
- [PR #81411 — Kanban process group termination](https://github.com/NousResearch/hermes-agent/pull/81411) *(Open, addressing #80280)*: The most significant fix in flight today — corrects worker termination paths from `os.kill(pid)` to signaling the entire POSIX process group, addressing the "timed-out workers leave descendant process groups alive" issue.

**Key Advances:**
- Active PRs for **browser CDP SSRF guard** ([#80847](https://github.com/NousResearch/hermes-agent/pull/80847)), **delegation cost reporting** for failed children ([#81397](https://github.com/NousResearch/hermes-agent/pull/81397)), and **multi-frontend session event fan-out** ([#81395](https://github.com/NousResearch/hermes-agent/pull/81395))
- Closed issues include **Telegram batch/media-group split** ([#46100](https://github.com/NousResearch/hermes-agent/issues/46100)) and **Discord docs drift** ([#11349](https://github.com/NousResearch/hermes-agent/issues/11349))

---

## 4. Community Hot Topics

**Most Active Issues:**

- **[#4335 — Cross-platform session context sharing (CLI ↔ Telegram)](https://github.com/NousResearch/hermes-agent/issues/4335)** *(12 comments, 3👍)*: Long-running feature request (since March) for unified session state across messaging platforms. Community interest is significant — users want continuity between CLI and Telegram conversations.

- **[#79278 — Context compression can drop in-flight tool chain](https://github.com/NousResearch/hermes-agent/issues/79278)** *(10 comments)*: **High-severity P1 bug** where compression races with executing tools, causing non-idempotent operations to replay. This is a critical safety issue with active community scrutiny.

- **[#11349 — Discord docs drift + `/voice join` missing](https://github.com/NousResearch/hermes-agent/issues/11349)** *(9 comments, CLOSED)*: A thorough audit of six documentation mismatches plus a small UI bug. Closed today, showing maintainers are responsive to documentation quality issues.

- **[#65365 — OAuth Claude Pro/Max HTTP 400 with memory tools](https://github.com/NousResearch/hermes-agent/issues/65365)** *(8 comments)*: P1 billing/session bug — Anthropic rejectssessions exposing `memory`/`session_search` tools on subscription OAuth. Affects paying users and blocks core memory features.

**Emerging Pattern:** The community is heavily engaged with **session state integrity** — cross-platform continuity (#4335), compression safety (#79278), and session persistence bugs (#54523, #81267) dominate discussion. Users want Hermes to be a **reliable continuity layer** across platforms and sessions.

---

## 5. Bugs & Stability

**Critical (P1):**

- **[#79278 — Compression drops in-flight tool chain](https://github.com/NousResearch/hermes-agent/issues/79278)**: Data-loss risk for non-idempotent ops. **No fix PR identified yet.**
- **[#79624 — Gateway exit(1) on preflight compaction](https://github.com/NousResearch/hermes-agent/issues/79624)**: Oversized session (>98K tokens) crashes gateway on restart. **No fix PR identified yet.**
- **[#81267 — Cron + delegate_task: SessionDB use-after-close](https://github.com/NousResearch/hermes-agent/issues/81267)**: Child transcripts silently dropped; completions unroutable. Complex multi-fault issue.
- **[#65365 — OAuth Claude HTTP 400](https://github.com/NousResearch/hermes-agent/issues/65365)**: Subscription users cannot use memory tools.

**High (P2):**

- **Windows reliability cluster**: [#80968 TUI crash](https://github.com/NousResearch/hermes-agent/issues/80968), [#81290 black secondary window](https://github.com/NousResearch/hermes-agent/issues/81290), [#80569 duplicate startup entries](https://github.com/NousResearch/hermes-agent/issues/80569), [#80184 WSL noise](https://github.com/NousResearch/hermes-agent/issues/80184)
- **[#22418 — macOS desktop-gateway conflicts with CLI](https://github.com/NousResearch/hermes-agent/issues/22418)**: Discord token lock contention.

**Kanban Lifecycle Bugs (P2/P3 cluster):** Multiple reports of **zombie workers** ([#80512](https://github.com/NousResearch/hermes-agent/issues/80512), [#80280](https://github.com/NousResearch/hermes-agent/issues/80280)), **auto-decomposer loops** ([#79728](https://github.com/NousResearch/hermes-agent/issues/79728), [#75444](https://github.com/NousResearch/hermes-agent/issues/75444), [#79738](https://github.com/NousResearch/hermes-agent/issues/79738)), and **parent turn budget exhaustion** ([#80507](https://github.com/NousResearch/hermes-agent/issues/80507)). **Fix PR #81411 for #80280 is in review.**

**Telegram Delivery (P2/P3):** Rich message copy affordance ([#79331](https://github.com/NousResearch/hermes-agent/issues/79331), CLOSED), top-level rich_message ignored ([#63485](https://github.com/NousResearch/hermes-agent/issues/63485), duplicate #81368), batch splitting (#46100, CLOSED).

**With Fix PRs:** #80280 → [#81411](https://github.com/NousResearch/hermes-agent/pull/81411); #81286 → [#81395](https://github.com/NousResearch/hermes-agent/pull/81395); #74399 → [#81400](https://github.com/NousResearch/hermes-agent/pull/81400)

---

## 6. Feature Requests & Roadmap Signals

**Strong Momentum:**

- **First-class Teams** ([#81405](https://github.com/NousResearch/hermes-agent/issues/81405)) — **New today**: A comprehensive proposal for persistent multi-profile teams with Quick Chat, Managed Work, channels, and shared capabilities, built on existing Profiles and Kanban primitives. This signals evolution toward **multi-agent organizational units**.

- **WhatsApp parity campaign** ([#79890](https://github.com/NousResearch/hermes-agent/issues/79890), [#69659](https://github.com/NousResearch/hermes-agent/issues/69659)) — Meta-issue consolidating platform alignment requests, with separate PRs/requests for message history/contacts exposure.

- **Realtime voice provider contract** ([PR #81404](https://github.com/NousResearch/hermes-agent/pull/81404)) — **New today**: Draft PR for typed voice provider extension, building on community RFC. Signals imminent voice capability expansion.

- **Cron full-prompt access** ([#18374](https://github.com/NousResearch/hermes-agent/issues/18374), [PR #81408](https://github.com/NousResearch/hermes-agent/pull/81408)) — 5-upvote issue addressed by PR today; likely to land soon.

**Projected Next Version Features:** (a) `cronjob(action="get")` for prompt access, (b) Kanban process-group termination fix, (c) SSRF hardening for cron monitoring, (d) terminal activity stamp fix, (e) realtime voice provider groundwork.

---

## 7. User Feedback Summary

- **Pain Point — Windows Desktop reliability:** Multiple reports of black windows ([#81290](https://github.com/NousResearch/hermes-agent/issues/81290)), stuck embeds ([#79833](https://github.com/NousResearch/hermes-agent/issues/79833)), and noisy startup ([#80184](https://github.com/NousResearch/hermes-agent/issues/80184)). User experience on Windows is notably worse than macOS/Linux — likely a v0.20.0 regression.

- **Pain Point — Session/data loss risks:** Users report **actual data loss incidents** — dropped transcripts ([#81267](https://github.com/NousResearch/hermes-agent/issues/81267)), replayed non-idempotent ops ([#79278](https://github.com/NousResearch/hermes-agent/issues/79278)), and stuck UI timestamps ([PR #80832](https://github.com/NousResearch/hermes-agent/pull/80832)).

- **Satisfaction:** Positive signals include maintainers closing issues quickly when duplicates are found, documentation fixes being actioned, and the community engaging deeply with roadmap proposals (Teams #81405, WhatsApp #79890) — indicates engaged power users who see Hermes as a long-term platform.

- **Feature Gaps:** Users want **cross-platform session continuity** (#4335), **confirmation prompts before destructive actions** (#81356), **localization for Telegram bot commands** (#65765), and **failure-routing for cron** ([PR #77866](https://github.com/NousResearch/hermes-agent/pull/77866)).

---

## 8. Backlog Watch

**Long-unanswered High-Value Items:**

- **[#4335 — Cross-platform session sharing](https://github.com/NousResearch/hermes-agent/issues/4335)** — Created 2026-03-31, 12 comments, 3 upvotes, tagged `needs-decision`. **No maintainer response visible; ~4 months old.** This is a flagship feature request with no decision on approach (shared store vs. sync layer).

- **[#65365 — OAuth Claude memory tool rejection](https://github.com/NousResearch/hermes-agent/issues/65365)** — Created 2026-07-16, P1 severity, 8 comments. **No fix PR or confirmed root-cause note in accessible data.** Blocked paying users (Claude Pro/Max) from using memory features.

- **[#22418 — macOS desktop/CLI gateway conflict](https://github.com/NousResearch/hermes-agent/issues/22418)** — Created 2026-05-09, P2, 5 comments. **~3 months without resolution.** Affects an edge case, but a fundamental architecture question (desktop vs. CLI gateway ownership of tokens).

**Newest Items at Risk of Attention Starvation:**
- [#80968 — Windows TUI crash](https://github.com/NousResearch/hermes-agent/issues/80968) (P2, created 2026-08-07, marked duplicate — but root cause and fix unclear)
- [#81290 — Black secondary window](https://github.com/NousResearch/hermes-agent/issues/81290) (P2, needs-repro) and [#80569 — duplicate startup entries](https://github.com/NousResearch/hermes-agent/issues/80569) (P2) — Windows issues cluster that needs a dedicated owner.

---

*Digest generated 2026-08-08 from GitHub activity data. Project health: **active and responsive**, with a clear focus on stabilizing Windows, session-state, and Kanban lifecycle ahead of the next release.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-08

## 1. Today's Overview

PicoClaw's development activity shows a moderate, healthy pulse with 14 pull requests and 4 issues updated in the last 24 hours. While no new releases shipped today, the project saw two PRs closed/merged—including the significant GitHub Copilot SDK bump from v0.2.0 to v1.0.8—and two fresh PRs opened, indicating active maintenance. All open issues carry the `stale` label, suggesting the maintainers are actively pruning unaddressed threads but some items may be losing momentum. Dependabot automation accounts for the majority of PR activity (8 of 14), while community contributions continue to deliver substantial feature work, particularly around messaging channels and tool reliability. Several week-old important PRs and all three open feature-request issues remain without maintainer response, suggesting a backlog that may need attention.

## 2. Releases

No new releases were published in this reporting window. The last known release predates this digest period.

## 3. Project Progress

**Merged/Closed (2):**
- [#3291](https://github.com/sipeed/picoclaw/pull/3291): **GitHub Copilot SDK jump (v0.2.0 → v1.0.8)** — Merged. This is a major jump across semver boundaries and likely brings breaking changes; the close status indicates the dependency pipeline is moving forward successfully.
- [#3289](https://github.com/sipeed/picoclaw/pull/3289): **Pion RTP bump (v1.10.2 → v1.10.5)** — Merged. Routine patch-level update for RTP handling.

**Newly Opened (today, 2):**
- [#3321](https://github.com/sipeed/picoclaw/pull/3321): **Fix agent dynamic context placement** — Moves per-request dynamic context blocks (time, runtime, session, sender) after conversation history to preserve prefix caching. This is a thoughtful caching optimization by user `grrowl` that could meaningfully improve performance on repeated requests.
- [#3320](https://github.com/sipeed/picoclaw/pull/3320): **Fix WhatsApp client outdated (405) error** — Bumps `whatsmeow` because WhatsApp is rejecting the currently pinned client version. This unblocks a **dead WhatsApp channel** — a critical connectivity fix.
- [#3319](https://github.com/sipeed/picoclaw/pull/3319): **Honor exec tool timeout and boolean run options** — Community contributor `MrTreasure` continues to improve execution control by honoring per-run `timeout`, `background`, and `pty` parameters.

---

## 4. Community Hot Topics

**Top Activity:**
- [#3093](https://github.com/sipeed/picoclaw/issues/3093) — "SimpleX or tox" (6 comments, 1 👍) — **[CLOSED as stale]** After ~2 months, the maintainers closed this feature request. Underlying need: users want **more privacy-focused chat gateways** beyond mainstream ones.
- [#3302](https://github.com/sipeed/picoclaw/issues/3302) — "Support OAuth 2.1 for MCP servers" (2 comments) — Follow-up to #2546; asks for modern OAuth support in MCP integrations. No maintainer response yet.
- [#3308](https://github.com/sipeed/picoclaw/issues/3308) — "Code review: concurrency hazards, goroutine leaks, and memory/speed optimizations" (1 comment) — A contributor took the initiative to **voluntarily review the codebase** with specific concerns. This signals strong community investment in quality.
- [#3307](https://github.com/sipeed/picoclaw/issues/3307) — "Session list/switch for Telegram" (1 comment) — Requests parity between Web UI session management and Telegram channels.

**Pattern:** The community is pushing for **multi-channel parity** (Telegram sessions, Facebook, WhatsApp) and **modern protocol support** (OAuth 2.1, privacy messaging). The fact that users are submitting full code-review write-ups (#3308) suggests a technically sophisticated and engaged user base.

---

## 5. Bugs & Stability

**Newly Reported Today:** None in the issue tracker. However, the following issues remain **open and are now stale**:

1. **WhatsApp channel dead ("client outdated 405")** — [PR #3320](https://github.com/sipeed/picoclaw/pull/3320) explicitly states the native WhatsApp channel is unresponsive. **Fix exists and is open.** *Severity: High — channel outage.*
2. **Tool-call format leakage into LLM summaries** — [PR #3279](https://github.com/sipeed/picoclaw/pull/3279) addresses a bug class where tool-call formatting leaks into user-visible messages via seahorse. *Severity: Medium — data corruption in chat UX.*
3. **DingTalk inbound images unsupported** — [PR #3283](https://github.com/sipeed/picoclaw/pull/3283) adds image support; also includes token-caching improvements. *Severity: Medium — missing feature/bug in production channel.*
4. **[Issue #3308](https://github.com/sipeed/picoclaw/issues/3308) — Concurrency hazards and goroutine leaks** — Tagged `[BUG]` by the reporter but reads more like an unsolicited code review. *Severity: Unconfirmed; needs a maintainer triage.*

---

## 6. Feature Requests & Roadmap Signals

**Active requests (all stale, all unanswered by maintainers):**
- **OAuth 2.1 for MCP servers** ([#3302](https://github.com/sipeed/picoclaw/issues/3302))
- **Session list/switch command for Telegram and other channels** ([#3307](https://github.com/sipeed/picoclaw/issues/3307))
- **Privacy-first gateways (SimpleX, Tox, Wire)** ([#3093](https://github.com/sipeed/picoclaw/issues/3093)) — closed as stale

**Strong signals from open PRs awaiting review:**
- **Model fallback chains in UI** ([#3200](https://github.com/sipeed/picoclaw/pull/3200)) — long-pending (since July 1)
- **DashScope TTS + WeChat audio** ([#3270](https://github.com/sipeed/picoclaw/pull/3270)) — adds Chinese-market critical features
- **Current model list refresh across 9 providers** ([#3271](https://github.com/sipeed/picoclaw/pull/3271)) — typically merged quickly once reviewed

**High confidence for next release:** The exec tool fix (#3319), WhatsApp fix (#3320), and copilot SDK bump (#3291, already merged) are all candidate lockdown items. Community feature PRs (#3270, #3271, #3200) are mature and may land if the maintainers do a big merge pass.

---

## 7. User Feedback Summary

**Pain points expressed in this window:**
- **Telegram users feel like second-class citizens** — Web UI has session management but Telegram does not (#3307).
- **WhatsApp connectivity is broken; users can't rely on the channel** (via #3320).
- **Model naming confusion** — one contributor made it their mission to refresh model names across 9 providers to match reality (#3271), implying the defaults were outdated.
- **Technical debt concerns** — a community developer flagged goroutine leaks, memory usage, and concurrency hazards (#3308), implying that while the project runs on $10 hardware, there may be room for optimization.

**Sentiment:** The community is **proactive**, contributing high-quality fixes (MrTreasure alone has 3 open PRs and multiple closed ones). The "stale" labeling of thoughtful issues (#3093, #3308) may frustrate users who offered ideas but got no response before closure.

---

## 8. Backlog Watch

**Long-unanswered items needing maintainer attention:**

| Item | Created | Days Open | Why It Matters |
|------|---------|-----------|----------------|
| [#3200](https://github.com/sipeed/picoclaw/pull/3200) — Model fallback chain | July 1 | 38 days | Significant UI/backend feature; no comments at all from maintainers |
| [#3270](https://github.com/sipeed/picoclaw/pull/3270) — DashScope TTS + WeChat audio | July 20 | 19 days | Major feature for Chinese users; 3 PRs from same author sit unaddressed |
| [#3279](https://github.com/sipeed/picoclaw/pull/3279) — Tool-call leakage fix | July 21 | 18 days | Fixes a known bug class; contributor reported same symptoms as other fix |
| [#3302](https://github.com/sipeed/picoclaw/issues/3302) — OAuth 2.1 for MCP | July 30 | 8 days | In-demand protocol support; no maintainer triage |
| [#3308](https://github.com/sipeed/picoclaw/issues/3308) — Concurrency review | July 30 | 8 days | Community member did free code review; deserves acknowledgment even if not acted on |

**Recommendation:** The `stale` label is being applied broadly (including to a bug ticket and an unsolicited code review). Weekly triage of community PRs would prevent the "open PR limbo" that currently affects high-quality contributions like those from `MrTreasure` and `lc6464`.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-08

## Today's Overview

NanoClaw shows moderate activity today with 10 pull requests updated in the last 24 hours, though no issues were updated and no releases were cut. The project is currently processing 8 open PRs and closed 2 today, with a notable split between new feature/skill additions and targeted bug fixes. The absence of open issue updates suggests either a healthy triage queue or a temporary lull in user-reported problems. Channel integrations (Mattermost, Dial) and utility skills (Tavily MCP, AnyDoc) dominate the feature pipeline, while several fixes target database migrations and formatter behavior. Overall, the project appears in a steady development phase with active community contributions, though maintainer review capacity may be a constraint given 8 open PRs awaiting attention.

## Releases

No new releases were published in the last 24 hours. The most recent release history is not available in this data snapshot, so no changelog, breaking change, or migration notes can be provided.

## Project Progress

Two PRs were closed today:

- **[#3197 — fix(progress): display specific failure reasons](https://github.com/nanocoai/nanoclaw/pull/3197)** (closed, by tier2tech-tian): This fix addresses a UX issue where process-card failure titles only showed generic tool-action labels (e.g., "system check failed") despite the agent-runner already reporting specific errors in `resultSummary`. The PR extracts the first valid reason from the failure summary, scrubs exit-code boilerplate and empty messages, reuses existing redaction logic, caps at 38 characters per line, and adds reducer unit tests plus Feishu card JSON cross-layer tests. Test results: 274 targeted tests passed, 1427 full suite passed.

- **[#546 — Add Mattermost channel skill (/add-mattermost)](https://github.com/nanocoai/nanoclaw/pull/546)** (closed, by wakqasahmed): This long-running PR (originally opened 2026-02-26) was closed as superseded by [#3199](https://github.com/nanocoai/nanoclaw/pull/3199), which is a fresh implementation against the current `ChannelAdapter` architecture. The original targeted the pre-v2 `Channel`/`registry.ts` design that no longer exists on `main`. Closure of this stale PR is a hygiene improvement, clearing the way for the new implementation.

No other PRs were merged today, meaning 2 of 10 updates resulted in closure while 8 remain open.

## Community Hot Topics

The most actively discussed (and potentially contentious) item today is:

- **[#3199 — Add Mattermost channel integration (v2 ChannelAdapter)](https://github.com/nanocoai/nanoclaw/pull/3199)** (open, by wakqasahmed): This PR supersedes #546 with a fresh implementation against the v2 architecture using `registerChannelAdapter` and `channel-registry.ts`. Comments and reactions are minimal (0 👍), but the need to rewrite a previously-blocked integration for the new architecture suggests possible friction between contributor assumptions and the evolving codebase—a signal that migration documentation for the v2 channel system could be valued by the community.

Other PRs with updated activity but no comment/reaction data shown include the feature-rich batch:

- **[#3190 — Tavily MCP tool skill](https://github.com/nanocoai/nanoclaw/pull/3190)** (open)
- **[#2909 — Template setup flow + first-agent stamping](https://github.com/nanocoai/nanoclaw/pull/2909)** (open, core-team)
- **[#3198 — AnyDoc document conversion skill](https://github.com/nanocoai/nanoclaw/pull/3198)** (open, core-team)
- **[#3050 — Dial channel integration with runChannelSkill model](https://github.com/nanocoai/nanoclaw/pull/3050)** (open)

These feature PRs collectively suggest strong community interest in extensibility: more channel adapters and reusable skills.

## Bugs & Stability

No new bug reports were filed in the last 24 hours (0 issues updated). However, two fix-related PRs are in flight:

- **[#3197 — fix(progress): show specific failure reasons](https://github.com/nanocoai/nanoclaw/pull/3197)** (closed): Already covered above; this is a UX/bug fix that resolved a real user-facing issue where error details were hidden behind generic labels. Severity: Medium (user-confusing but not data-loss).

- **[#2346 — fix(formatter): treat unknown slash commands as normal chat](https://github.com/nanocoai/nanoclaw/pull/2346)** (open, by SidhayaPravda618): This fix addresses a silent-response bug where unknown slash commands were classified as `passthrough`, causing the Agent SDK to interpret them as Claude Code commands, producing output without `<message>` blocks and dropping the response. Severity: Medium-High (silent failure for any user typing an unrecognized slash command). This PR has been open since 2026-05-08 (3 months) and deserves maintainer attention.

- **[#3145 — fix(db): backfill destinations for existing wirings](https://github.com/nanocoai/nanoclaw/pull/3145)** (open, by tlysanhuo): Adds migration 021 to provision missing channel destinations for existing messaging-group wirings, preserving all existing destinations and custom local names. Severity: Medium (data completeness issue after schema change).

- **[#3196 — Fix/add mount readonly](https://github.com/nanocoai/nanoclaw/pull/3196)** (open, by teran13): A container/operational fix; details partial in the snippet but appears to address mount permissions. Severity: Low-Medium (environment/security hardening).

None of these have confirmed regressions reported, and fix PRs exist for all known issues. The silent-drop bug in #2346 is the highest-priority item.

## Feature Requests & Roadmap Signals

The strongest roadmap signals come from the open PRs, which look ready for review:

1. **Channel adapter expansion**: [Mattermost v2 integration (#3199)](https://github.com/nanocoai/nanoclaw/pull/3199) and [Dial channel (#3050)](https://github.com/nanocoai/nanoclaw/pull/3050) both target the new `ChannelAdapter` model, indicating that the v2 channel system is maturing and that external collaboration platforms beyond the current set are in demand.

2. **Onboarding experience**: [#2909 — template setup flow and first-agent stamping](https://github.com/nanocoai/nanoclaw/pull/2909) (core-team) adds setup-wizard flows for creating the first agent, signaling investment in new-user experience for the next release.

3. **Utility skills as a trend**: [Tavily MCP (#3190)](https://github.com/nanocoai/nanoclaw/pull/3190) and [AnyDoc (#3198)](https://github.com/nanocoai/nanoclaw/pull/3198) both add standalone utility tools (web search via MCP, document conversion). The volume of "Utility skill" PRs suggests the skill system is becoming a primary extension mechanism and that the community values agent capabilities beyond messaging.

**Prediction**: The next minor release will likely bundle the v2 channel integration (Mattermost, Dial), the setup-wizard flow, and at least one utility skill. The migration 021 backfill (#3145) is a strong candidate for the same release to avoid data-completeness issues.

## User Feedback Summary

While no explicit issue comments or reactions are available in this snapshot, several signals of user pain points and needs can be inferred from PR motivations:

- **Confusing failure messages**: The #3197 fix directly addresses user frustration with opaque error titles in the UI—users had to dig through internal `resultSummary` to understand what went wrong. This improves transparency and debuggability.

- **Silent response drops**: The #2346 fix addresses a scenario where user inputs vanished without output—a critical usability defect for anyone typing an unrecognized slash command.

- **Integration breadth**: The demand for Mattermost (superseding an older attempt), Dial, and Tavily MCP suggests users want NanoClaw to work with their existing toolchains rather than forcing a particular stack.

- **Onboarding friction**: The setup-wizard template flow (#2909) implies new users struggle with first-agent creation—the wizard directly targets that friction.

Overall, the feedback pattern suggests a user base that values clarity, reliability, and extensibility, with some frustration around configuration and setup complexity.

## Backlog Watch

The following items warrant maintainer attention:

- **[#2346 — fix(formatter): treat unknown slash commands as normal chat](https://github.com/nanocoai/nanoclaw/pull/2346)** ⚠️ High Priority: Open since 2026-05-08 (~3 months). This is a silent-failure bug fix with no maintainer response visible in the snapshot. Users hitting unknown slash commands lose responses entirely. This should be reviewed and either merged or given explicit guidance.

- **[#546 — Mattermost skill (closed as superseded)](https://github.com/nanocoai/nanoclaw/pull/546)** — Now resolved via #3199, but attention should go to the new PR.

- **[#3145 — db migration backfill](https://github.com/nanocoai/nanoclaw/pull/3145)** — Open since 2026-07-28 (~11 days). Migration 021 is important for data completeness; if the schema change shipped without it, existing wirings lack destinations. Recommend fast-tracking.

- **[#3199 — Mattermost v2 integration](https://github.com/nanocoai/nanoclaw/pull/3199)** — Fresh PR (created yesterday) that directly supersedes a blocked item. Early review would prevent another 5-month stall like #546.

No issues with zero responses appear in the data (0 total issues updated today), so community questions may be circulating elsewhere or are handled quickly.

---

*Digest generated from GitHub activity data on 2026-08-08. All links point to the nanocoai/nanoclaw repository.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Based on the provided GitHub data for IronClaw (github.com/nearai/ironclaw), here is the project digest for 2026-08-08.

---

# IronClaw Project Digest — 2026-08-08

## 1. Today's Overview
IronClaw is in a period of high-intensity stabilization and hardening. Activity is extremely high, with 50 issues and 50 PRs updated in the last 24 hours, indicating a very active development cycle with multiple parallel workstreams. The project is currently addressing a significant cluster of QA-found bugs (from "bug_bash_P1" events), a major initiative to fix documentation drift (the "Doc-Truth" pipeline), and multiple architectural improvements aimed at performance and reliability. While no new releases were published today, the sheer volume of merged/closed items and the creation of epic-level tracking issues show a project aggressively pushing toward a stable release candidate.

## 2. Releases
None. No new releases were published for IronClaw in the last 24 hours.

## 3. Project Progress
Despite no new releases, this was a substantial day for code advancement, with 12 PRs merged or closed. Key progress areas include:

- **Channel Delivery & Permissions:** The "two-lane" channel delivery tool was merged in PR #7157. This establishes explicit notification channels and delivers final replies to conversation threads. Building on this, a follow-up PR #7377 is moving towards a model where "a run acts as its invoker," removing shared-route subject binding to fix permission boundary issues.
- **Infrastructure & Security:** PR #7214 was a significant merge, adding explicit Docker and Railway user-sandbox profiles. This scopes workspaces and checkpoints more strictly to "tenant plus user" and runs commands in fresh, non-root workers, representing a major security hardening step.
- **Tool Disclosure & Performance:** PR #7372 merged to lock in schema-token reduction floors for the progressive tool disclosure system, making any performance regressions visible via tests.
- **Documentation & Quality Gates:** A major "Doc-Truth" pipeline is being built to fix the persistent drift between documentation and actual code behavior. Four related PRs (#7375, #7376, #7378, #7379) were opened, implementing contract tests and a new `docs-live` deployment branch to ensure the public docs always match the release artifacts.
- **Maintenance:** A routine dependency bump for `dompurify` (a JavaScript sanitization library) was merged in PR #7386 to address a security fix.

## 4. Community Hot Topics
The most active discussions reveal a focus on user experience and data integrity.

- **#7340 - "No way to reset model settings to factory defaults"** (6 comments) is the most active issue. A user changed their model/provider settings and was completely locked out of restoring the original configuration. The underlying need is for a safety net: users want the ability to revert configuration changes, especially ones that break their ability to use the tool. This is a clear UX gap.
- **#6989 - "Token accounting: hybrid provider-usage + tail estimates"** (4 comments) is a technical bug showing deep engineering focus. It deals with incorrect token estimation, which can lead to unexpected costs for users. While technical, it highlights the project's commitment to cost accuracy and transparency.
- **#7317 - "Proposal: Doc-Truth Verification Pipeline"** (3 comments) is not just a bug report but a proposal for a systemic solution. It points to multiple instances where docs and code diverged, causing user confusion and model refusals. The community (and maintainers) are rallying around this to prevent future drift.
- **#7360 - "Expand stress coverage across built-in and durable write paths"** (2 comments) shows a focus on reliability. The issue identifies a gap where regressions in tool-write paths could go undetected by the current stress tests, prompting a push for stronger E2E coverage.

## 5. Bugs & Stability
The project experienced a high bug influx, primarily from `bug_bash_P1` QA sessions. The most severe issues involve agent hallucinations and incorrect state awareness.

- **Critical / High Severity (Hallucination & State Mismatch):** A major cluster of bugs shows the model fabricating statuses or not recognizing actual system states.
  - #7247 (Agent falsely claims GitHub is connected) and #7246 (Agent hallucinates automation status) are prime examples. The agent is not verifying state via tools before responding.
  - #7344 (Assistant denies Slack is connected despite ACTIVE status) shows the inverse problem.
  - **Fix Status:** These is no single fix, but PR #7377 ("a run acts as its invoker") and PR #7365 (memory-save guidance) are directly aimed at improving agent state-awareness and memory, which should address the root causes of many of these hallucinations.
- **High Severity (Infrastructure):**
  - #7298 (Runner loses contact with monitoring system) and #5456 (Runner lease expiration) point to systemic execution reliability issues.
  - **Fix Status:** PR #7131 (delivering triggered run failures) is a partial fix.
- **High Severity (Data Accuracy):**
  - #7295 (Agent leaks/confuses Slack user identity) is a severe security and trust issue.
  - #7185 (Memory not reliably recalled across conversations) is a core functionality bug affecting memory.
  - **Fix Status:** PR #7365 addresses #7185 directly.
- **Medium Severity:** Bugs like #6590 (Windows serve fails), #7292 (Installed tool cannot be used), and #7074 (multi-tool meeting research fails) remain open without a clear fix PR yet.

## 6. Feature Requests & Roadmap Signals
The roadmap appears focused on robustness, observability, and quality-of-life.

- **Doc-Truth Pipeline:** Rather than just fixing bugs, the project is building a systemic solution with contract tests and deployment changes (PRs #7375-#7379). This is likely a major feature for the next release, signaling a strong commitment to developer/user trust.
- **Performance & Observability:** There is a strong push for better metrics and observability.
  - PR #7385 seeks to add "durable, queryable tool-disclosure rollout metrics," giving operators insight into the performance of the new disclosure system.
  - Issue #7224 asks for an "Activity timeline and turn navigation" in the Inspector, showing a move towards fine-grained debugging tools.
  - Issue #7369 requests a way to capture traces when an agent hits an error, the absence of which is a major UX frustration.
- **Config & UX Improvements:** Issue #7340 (Reset to defaults) is a strong candidate for the next release. It’s a simple, high-value addition that would resolve a very common user frustration.

## 7. User Feedback Summary
Real user pain points are heavily concentrated around trust and reliability.

- **Hallucinations are damaging trust:** The most significant feedback is the cluster of bugs where the agent confidently reports false states (e.g., "GitHub is connected," "You have this automation set up"). This indicates a fundamental issue where the model relies on assumptions rather than fetching the real state, which leads to strong user dissatisfaction and distrust.
- **Lack of "Undo" or "Reset":** The #7340 issue shows that configuration changes are destructive without a clear path back. Users feel trapped when they make a change they can't revert.
- **Channel Integration Pain:** The series of Telegram bugs (#6475, #6643, #6644) shows deep friction in setting up and using messaging channels, which are core to the agent's value. While many are closed, new ones like #7368 (High latency) suggest the experience is not yet polished.
- **Memory Inconsistency:** Feedback from the "IronClaw Champions" group confirms that the agent's failure to recall context across conversations is a major blocker, making the agent feel non-continuous and unreliable for real work.
- **Observability Gaps:** The inability to capture traces on error (#7369) is a direct complaint from a user, hindering their ability to understand failures and report issues effectively.

## 8. Backlog Watch
Several significant issues and PRs have been open for a while and require attention.

- **Issue #5456 - [P1] Routine runs fail with runner lease expiration:** Open since **2026-06-30** (over a month). This is labeled a high-priority bug that affects core functionality and remains unresolved, impacting "email routines" and other multi-tool workflows.
- **PR #5503 - [Experiment] Add compact Google extension capabilities:** Open since **2026-07-01** (over a month). A large, core-authored PR that appears stalled. If this capability is needed, it needs maintainer push; if not, it should be explicitly closed to clear the queue.
- **Issue #6590 - serve fails on Windows:** Open since **2026-07-23**. This is a platform blocker for Windows developers, making local development and testing impossible on that OS. It's critical for expanding the contributor base.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-08

## 1. Today's Overview

LobsterAI is in a steady release cadence with the 2026.8.5 merge completed and 2026.8.7 published. Activity is moderate: 7 issues and 7 PRs were touched, with most PRs merged (6 of 7) and 3 of 7 issues closed. The team is actively addressing bug reports tied to the new release, particularly around custom model providers with slashed IDs (SiliconFlow) and Windows installer reliability. Community engagement is modest, with most issues receiving only 1–2 comments, and several older stale issues were swept (closed) in the last 24h. Overall project health appears good: release-oriented work is moving quickly, and critical-reported bugs are receiving immediate fix PRs.

## 2. Releases

**[2026.8.7 — LobsterAI 2026.8.7](https://github.com/netease-youdao/LobsterAI/releases)** 

Changes:
- **feat(cowork):** title-bar conversation search (PR [#2435](https://github.com/netease-youdao/LobsterAI/pull/2435))
- **feat:** Markdown LaTeX math delimiters support (PR [#2449](https://github.com/netease-youdao/LobsterAI/pull/2449))
- **fix(win-installer):** rescue null watchdog exit code

This is a patch-level release with no breaking changes or migration steps required.

## 3. Project Progress

Six PRs were merged/closed, representing the bulk of the 2026.8.5 release and hotfixes:

- **[#2451](https://github.com/netease-youdao/LobsterAI/pull/2451) — Release/2026.8.5 merge to main:** Adds in-conversation search to Cowork, improves math rendering, IM analytics, OpenClaw configuration and plugin installation, and Windows installation/update reliability.
- **[#2450](https://github.com/netease-youdao/LobsterAI/pull/2450) — fix(cowork):** Restore fullscreen code toolbar clicks on Windows (overlay outside Electron title bar drag regions).
- **[#2449](https://github.com/netease-youdao/LobsterAI/pull/2449) — fix: Markdown LaTeX math delimiters** rendered correctly.
- **[#2448](https://github.com/netease-youdao/LobsterAI/pull/2448) — fix: Chat search** in Cowork (follow-up on title-bar search).
- **[#2445](https://github.com/netease-youdao/LobsterAI/pull/2445) — fix(openclaw):** Strip plugin-index-managed keys from `config.set` to prevent conflicting writes.
- **[#2446](https://github.com/netease-youdao/LobsterAI/pull/2446) — fix(win-installer):** Rescue null watchdog exit code via extractor.

**In progress:** [#2452](https://github.com/netease-youdao/LobsterAI/pull/2452) — fix(openclaw): preserve provider prefix for model IDs containing slashes; directly addresses the SiliconFlow bug reported in Issue [#2443](https://github.com/netease-youdao/LobsterAI/issues/2443).

## 4. Community Hot Topics

The most active threads (2 comments each, no reactions reported):

- **[#2443](https://github.com/netease-youdao/LobsterAI/issues/2443) — Bug: Custom Provider with slashed model ID unusable (SiliconFlow):** Open, created 2026-08-06. Core storage/parsing issue: `custom_0` + `deepseek-ai/DeepSeek-V4-Flash` loses the provider prefix. **Actively addressed by PR #2452.** High relevance to any OpenAI-compatible provider with slashed model IDs.
- **[#2447](https://github.com/netease-youdao/LobsterAI/issues/2447) — Execution returns no result and no error:** Open, created 2026-08-07. A screenshot-only report; minimal context provided. Maintainers may need reproduction steps.
- **[#2444](https://github.com/netease-youdao/LobsterAI/issues/2444) — Feature request: Input box editing mode:** Open. Pain point: Shift+Enter for newline is error-prone (accidental sends). Suggesting Enter-to-newline toggle or an "edit mode" button with an expanded input area and optional WYSIWYG Markdown. This is a UX-quality-of-life request likely to gather support.

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|---|---|---|---|
| **High** | [#2443](https://github.com/netease-youdao/LobsterAI/issues/2443) — Model ID with slash breaks interface selection (SiliconFlow) | Open | Fix PR [#2452](https://github.com/netease-youdao/LobsterAI/pull/2452) open; affects all OpenAI-compatible providers with slashed model IDs |
| **Medium** | [#2447](https://github.com/netease-youdao/LobsterAI/issues/2447) — Execution silently returns nothing | Open | Insufficient detail; needs repro steps |
| **Medium** | [#2445](https://github.com/netease-youdao/LobsterAI/pull/2445) — OpenClaw `config.set` writing plugin-index-managed keys (merged fix) | Fixed | Prevented overwriting/managed-key conflicts |
| **Low** | [#2450](https://github.com/netease-youdao/LobsterAI/pull/2450) — Windows: fullscreen code toolbar clicks unresponsive | Fixed | Title bar drag region conflict resolved |
| **Low** | [#2446](https://github.com/netease-youdao/LobsterAI/pull/2446) — Windows installer: null watchdog exit code hang | Fixed | Rescue path via extractor |

Older stale issues closed (not re-verified): [#1263](https://github.com/netease-youdao/LobsterAI/issues/1263) (duplicate scheduled tasks, API limit spam), [#1273](https://github.com/netease-youdao/LobsterAI/issues/1273) (sql.js WASM high-frequency crash risk).

## 6. Feature Requests & Roadmap Signals

- **[#2444](https://github.com/netease-youdao/LobsterAI/issues/2444) — Input box editing mode (Enter-to-newline toggle):** Well-scoped, user-facing UX improvement. Could land in a minor release given the project's fast iteration pace.
- **[#1265](https://github.com/netease-youdao/LobsterAI/issues/1265) — Per-agent IM bot and model binding:** Closed (stale) but represents a clear architectural desire for multi-agent setups (e.g., different bots/roles with different models). Not in current release notes — likely a future major feature if re-opened or continued in design discussions.

## 7. User Feedback Summary

- **Dissatisfaction driver:** Custom provider compatibility is the top current pain point — specifically, model IDs containing slashes (SiliconFlow, `deepseek-ai/...`) render unusable in the UI. Fix is in progress, so confidence in responsiveness is high.
- **Satisfaction signals:** Release 2026.8.5/2026.8.7 bundles several requested enhancements (Cowork search, LaTeX delimiters, IM analytics, plugin install fixes), indicating the team is listening to niche power-user needs.
- **Community responsiveness:** Low engagement on issues (sparse comments), suggesting most users are passive consumers; however, reports are detailed and technical — indicating a technically sophisticated user base (ML/LLM-heavy workflows).

## 8. Backlog Watch

- **[#1195](https://github.com/netease-youdao/LobsterAI/issues/1195) — [OPEN, stale since 2026-04-01]** Self-created skill installs to OpenClaw directory but doesn't show in LobsterAI skills panel. Still an unresolved bug affecting a core workflow (skill installation). Updated 2026-08-07 — likely did not receive maintainer response in over 4 months. Candidates for next-milestone cleanup.

**No other long-unanswered items are currently flagged.**

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

# CoPaw Project Digest — 2026-08-08

## 1. Today's Overview

CoPaw (QwenPaw) is in an active development and stabilization phase, with **31 issues** and **49 PRs** updated in the last 24 hours, indicating a healthy, high-velocity maintenance cycle. Notably, **11 issues were closed** and **22 PRs were merged/closed today**, demonstrating the maintainers' strong responsiveness. The release of **v2.1.0-beta.2** represents continued progress toward a stable 2.1.0, though beta testing is surfacing a steady stream of edge-case bugs, particularly around Windows platform issues, provider compatibility with strict API vendors, and desktop-mode UX regressions. The **high proportion of first-time contributors** (7 of the top 20 PRs) signals good community health onboarding, but also indicates that core maintainers may be stretched thin reviewing incoming code. Overall, the project shows high velocity and healthy community engagement, with a focus on hardening stability for the upcoming 2.1.0 release.

## 2. Releases

**[v2.1.0-beta.2](https://github.com/agentscope-ai/QwenPaw/releases)** — Released 2026-08-07

Changes include:
- **Fix (CI):** Fence-aware section extraction in real-behavior-proof (fixes #6626) by @hanson-hex
- **Fix (checkpoints):** Restore auto snapshots in web workspace bootstrap by @qbc2016

**Migration/Breaking Changes:** This is a beta release with no documented breaking changes. It includes minor bug fixes and continues the 2.1.0-beta line. Users of the beta channel should note the community-reported issues in desktop mode text selection (#6797) and double-click-to-open behavior (#6790), which are actively being addressed in open PRs.

## 3. Project Progress

**Merged/Closed PRs (notable from the 22 closed):**
- **[#4694](https://github.com/agentscope-ai/QwenPaw/pull/4694) — feat(website): downloads UI Refactoring and opt** (merged, by yuluo1007) — Concludes a long-running website improvement effort (May–Aug).

**Actively advancing (open PRs with meaningful progress):**
- **Memory/ReMe enhancements** — [#6772](https://github.com/agentscope-ai/QwenPaw/pull/6772) by jinliyl significantly enhances ReMe Light with embedding model factory support (OpenAI-compatible, DashScope), Daily Paper capability, and a Console memory config page rebuild.
- **Shell execution hardening** — [#6799](https://github.com/agentscope-ai/QwenPaw/pull/6799) by first-time contributor lllyfff addresses a **26 GB temp file leak** on Windows — a severe but invisible production issue.
- **ACP reliability** — [#6623](https://github.com/agentscope-ai/QwenPaw/pull/6623) by cocoakekeyu prevents final-text loss when notifications race prompt responses.
- **Browser resilience** — [#6776](https://github.com/agentscope-ai/QwenPaw/pull/6776) by lllyfff adds self-healing for dead Playwright driver connections ("die once, dead forever").
- **Strict provider compatibility** — [#6809](https://github.com/agentscope-ai/QwenPaw/pull/6809) by axelray-dev sanitizes Chat Completions content, directly fixing the StepFun 400 errors reported in #6803.
- **Telegram access control** — [#6788](https://github.com/agentscope-ai/QwenPaw/pull/6788) by niuda-kok fixes ACL resets when multica spawns per-task workspaces.
- **Desktop UI fixes** — Two independent PRs ([#6801](https://github.com/agentscope-ai/QwenPaw/pull/6801), [#6802](https://github.com/agentscope-ai/QwenPaw/pull/6802)) restore text selection/copy in desktop mode.
- **OneBot media support** — [#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715) by GMsure handles remote URL-based voice/image media in OneBot.

## 4. Community Hot Topics

- **[#6116](https://github.com/agentscope-ai/QwenPaw/issues/6116) — [CLOSED] Doom loop: agent repeatedly triggers same tool call** (8 comments, by feng183043996). The user reports the system eventually detects ~6 consecutive repetitions, but only after wasted API calls/tokens. This touches on core safety and budget-control concerns; the related thread continues in #6768. The closure suggests a fix or workaround was accepted.
- **[#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) — [OPEN] 2.0.1 Docker: plugin/app marketplace always says "maintenance"** (8 comments, by Sakura7301). A highly disruptive issue for Docker users unable to use any plugins. High urgency.
- **[#6732](https://github.com/agentscope-ai/QwenPaw/issues/6732) — [OPEN] MCP tools fail regularly after idle** (6 comments, by 70995781). A deterministic failure after hours of inactivity, requiring container restart. Points to a health-check/keep-alive gap.
- **[#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) — [Feature] Add Volcengine Agent Plan and Xiaomi MiMo Standard API built-in providers** (4 comments, by TinyBai). Provider breadth is a recurring theme this week, alongside the Gemini schema issue (#6812) and StepFun strict validation (#6803).
- **[#6786](https://github.com/agentscope-ai/QwenPaw/issues/6786) — [OPEN] Telegram whitelist resets when multica starts new task** (4 comments, by niudakok). The user was blocked by access-control loss; an associated fix PR #6788 is already open, showing a positive loop.

## 5. Bugs & Stability

**Ranked by severity:**

1. **[#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) — Docker plugin/app marketplaces permanently "in maintenance"** — Blocks core functionality for all Docker 2.0.1 users. No fix PR yet; requires immediate maintainer attention.
2. **[#6780](https://github.com/agentscope-ai/QwenPaw/issues/6780) — Process freezes/hangs after ~30 mins idle; requires restart** — Affects unattended deployments; likely related to connection/session timeout handling. No fix PR on file.
3. **[#6811](https://github.com/agentscope-ai/QwenPaw/issues/6811) — OpenAI Responses continuation summary blocks main thread; ignores `disable_thinking` and misreports 60-sec cancellation as an error** — Blocks the primary conversation during Scroll eviction, affecting responsiveness with reasoning models.
4. **[#6813](https://github.com/agentscope-ai/QwenPaw/issues/6813) — `consume_model_response` raises `KeyError: '__aiter__'` on agentscope 2.x ChatResponse** — Chat auto-title generation consistently fails; a compatibility regression with agent scope changes.
5. **[#6803](https://github.com/agentscope-ai/QwenPaw/issues/6803) — OpenAI-compatible requests rejected by strict providers (StepFun 400)** — Fix PR #6809 is open.
6. **[#6812](https://github.com/agentscope-ai/QwenPaw/issues/6812) — Gemini provider sends `$schema` field in tool schemas; other extra fields rejected** — API-incompatible tool schemas; no fix PR yet.
7. **[#6775](https://github.com/agentscope-ai/QwenPaw/issues/6775 ) — MalwareBytes flags Trojan Loader in Windows desktop build** — Whether false positive or packaging regression, this destroys user trust; needs a public response.
8. **[#6768](https://github.com/agentscope-ai/QwenPaw/issues/6768) — [need-info] Agent enters infinite loop after multi-step task; session blocked for hours** — Related to the doom-loop family (#6116) but not resolved for all scenarios.
9. **[#6785](https://github.com/agentscope-ai/QwenPaw/issues/6785) — Profile category hides custom persona .md files (regression)** — Fix PR #6808 is open.
10. **Windows update/install file-lock issues** ([#6810](https://github.com/agentscope-ai/QwenPaw/issues/6810)) — NSIS installer fails/locks during updates; needs a pre-install process kill step.

## 6. Feature Requests & Roadmap Signals

- **[#6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) — Volcengine Agent Plan + Xiaomi MiMo Standard built-in providers**: Provider breadth continues to be a top request (joined by Gemini + StepFun fixes this week). Likely accepted for 2.1.0.
- **[#6285](https://github.com/agentscope-ai/QwenPaw/issues/6285) — Add `qwen3.8-max-preview` to Aliyun Token Plan model list**: The model list is hardcoded; users expect dynamic/sync-able provider model catalogs. A refactor toward dynamic model discovery would solve this class of requests.
- **[#6770](https://github.com/agentscope-ai/QwenPaw/issues/6770) — Make user Chrome tab lifetime configurable across response cycles**: Addresses a real workflow gap for browser automation.
- **[#6800](https://github.com/agentscope-ai/QwenPaw/pull/6800) — Mailbox assistant with real-time monitoring and access control** by first-time contributor Luohh5: A new capability PR; signals community interest in autonomous email management.
- **[#6804](https://github.com/agentscope-ai/QwenPaw/pull/6804) — WeChat Chinese approval replies (`允许`/`拒绝`)**: Localization UX is being actively addressed.
- **[#6715](https://github.com/agentscope-ai/QwenPaw/pull/6715) — OneBot remote media (voice/image over HTTP)**: Improves cross-platform OneBot compatibility.

## 7. User Feedback Summary

- **Language barrier friction on Windows**: Users on Windows with Chinese-language (and English-speaking users in #6775) are experiencing instability, installation issues, and confusing security warnings. The MalwareBytes Trojan false-positive (#6775) is severe and likely driving uninstalls; a clear public communication or packaging fix is urgently needed.
- **Memory/Context management is a top pain point**: Multiple issues around doom loops, infinite loops after tasks, shell process hangs with `nohup`/`&` (#6480), and session blocking (#6768) indicate users rely on long-running autonomous operations that sometimes stall without recovery.
- **Provider diversity is incomplete**: Users are hitting hard failures with Gemini (#6812) and StepFun (#6803), and requesting new providers (#6490). This suggests the provider layer needs better schema validation and broader vendor coverage.
- **Docker users feel left behind**: The marketplace "maintenance" bug (#6782) and disconnect/restart bugs (#6732, #6780) erode confidence in the Docker distribution.
- **Desktop mode UX regressions**: Text-selection loss (#6797) and double-click-to-open (#6790) are minor but widely noticed by desktop users, with fix PRs in flight.
- **Positive signals**: New contributors (lllyfff, ump45nose, Luohh5, jesseedcp) are filing quality fixes and features, and leadership is participating in issue triage (hanson-hex, qbc2016 in beta fixes).

## 8. Backlog Watch

- **[#6615](https://github.com/agentscope-ai/QwenPaw/pull/6615) — [Under Review] fix(config): handle corrupted agent config and invalid JSON** — Open since July 31; small, safety-relevant fix with no reviews yet. Needs a maintainer look.
- **[#6617](https://github.com/agentscope-ai/QwenPaw/pull/6617) — [Under Review] fix(providers): honor Retry-After cap on streaming retry path** — Open since July 31; rate-limit/backoff correctness has production cost. Also un-reviewed.
- **[#6564](https://github.com/agentscope-ai/QwenPaw/pull/6564) — [Under Review] fix(memory): flush pending turns before compression** — Open since July 30; addresses Scroll compression data loss. Blocked or under-reviewed for over a week; part of a multi-PR memory reliability sequence.
- **[#6688](https://github.com/agentscope-ai/QwenPaw/pull/6688) — [Under Review] fix(plugins): isolate bare absolute imports per plugin namespace** — Open since Aug 4; fixes plugin installation failures from App Center. Community-submitted with no maintainer response yet.
- **[#4694](https://github.com/agentscope-ai/QwenPaw/pull/4694) — feat(website): downloads UI Refactoring and opt** (merged) — A long-term issue, newly merged; one to watch for website stability.

---

*Data window: 2026-08-07 to 2026-08-08. All links point to https://github.com/agentscope-ai/QwenPaw, mirroring the CoPaw repository.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-08

## 1. Today's Overview

ZeroClaw shows a highly active development cycle with 50 issues and 50 PRs updated in the last 24 hours, though only 3 PRs were merged/closed, suggesting a heavy review load on the maintainers. The project is progressing through a significant architectural consolidation phase, addressing structural gaps around SOP (Standard Operating Procedure) execution, security policy hardening, and cross-cutting observability. A wave of high-severity (P1) bug reports was filed in the past 24 hours, covering budget tracking failures, security policy bypasses, and daemon runtime integrity issues. Notably, multiple contributions are targeting the same core problems (SOP headless execution, security containment), indicating good collaboration but also exposing deep systemic issues in the runtime daemon and provider layers. No new releases were published, but the volume and quality of incoming RFCs (e.g., Agent Plugins support) suggest a feature-rich upcoming milestone.

## 2. Releases

**No new releases were published in the last 24 hours.** The most recent version referenced in issues is v0.8.4 (prebuilt binaries/aarch64).

## 3. Project Progress

The project saw **3 PRs merged/closed** out of 50 updated:

- **[PR #9836 (CLOSED/MERGED) — fix(transcription): make local_whisper bearer_token optional](https://github.com/zeroclaw-labs/zeroclaw/pull/9836)** — Resolves a configuration bug where the `local_whisper` backend hard-failed when `bearer_token` was absent, a condition that is normal for whisper.cpp's loopback server. This is a functional fix for the transcription pipeline.

The remaining 47 PRs remain open, with several substantial changes in flight that have seen significant review activity:

- **[PR #9494 (OPEN) — fix(sop): drive cron-started headless runs](https://github.com/zeroclaw-labs/zeroclaw/pull/9494)** — This represents a major fix for cron-triggered SOPs being stranded. It has a follow-up branch, **[PR #9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841)**, which adds fixes for four blocking review findings plus an additional defect.

- **[PR #9384 (OPEN) — fix(security): resolve shell command path arguments to block symlink escapes](https://github.com/zeroclaw-labs/zeroclaw/pull/9384)** — A critical security hardening PR for the shell/skill path guard, though the author notes it is a partial mitigation.

- **[PR #9827 (OPEN) — fix(security): stop shell children from escaping their validated confinement](https://github.com/zeroclaw-labs/zeroclaw/pull/9827)** — Addresses three related shell-containment fixes, including sandbox working directory issues.

- **[PR #9838 (OPEN) — fix(channel/telegram): authorize the account that taps an approval button](https://github.com/zeroclaw-labs/zeroclaw/pull/9838)** — Fixes a security gap where the approval button callback path skipped the allowlist check.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal a focus on architectural RFCs and security-critical bugs:

- **[Issue #8933 (CLOSED, 13 comments) — RFC: Add cross-turn conversation correlation to OTel export](https://github.com/zeroclaw-labs/zeroclaw/issues/8933)** — The most discussed topic. The community is converging on a standard for correlating conversations in OpenTelemetry, aligned with upstream semantic conventions. This was accepted, indicating a roadmap commitment to mature observability.

- **[Issue #9246 (CLOSED, 12 comments) — RFC: Preserve Todo tracker configuration during ZeroCode ownership migration](https://github.com/zeroclaw-labs/zeroclaw/issues/9246)** — Focuses on preserving configuration during a migration, a sign of user concern about data integrity during transitions.

- **[Issue #5937 (OPEN, 12 comments) — refactor: Unify providers architecture and reqwest client management](https://github.com/zeroclaw-labs/zeroclaw/issues/5937)** — A long-standing architectural RFC (April 2026) highlighting technical debt in provider modules. With the recent P1 cost-tracking bug on Anthropic (#9816), this refactor is becoming more urgent.

- **[Issue #8424 (OPEN, 10 comments) — RFC: Workspace-relative forbidden path patterns and optional .zeroclawignore](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)** — Directly related to the newly filed critical security gap in `forbidden_paths` (#9815), shaping the solution roadmap for file access protection.

The underlying need across these threads is a desire for a more robust, production-ready runtime with cleaner boundaries between components (providers, security, observability).

## 5. Bugs & Stability

The last 24 hours produced a significant cluster of **P1 (high) severity bugs**, signaling a potential stability crunch in the runtime and provider layers:

- **[Issue #9840 (OPEN) — daemon steals daemon.sock on start and unlinks it on exit, stranding a live daemon](https://github.com/zeroclaw-labs/zeroclaw/issues/9840)** — **Critical runtime integrity issue.** The daemon can unlink the socket of a legitimate active daemon, breaking RPC for all clients. The report suggests a clear fix (check socket ownership before removal). *Fix PR: None yet.*

- **[Issue #9816 (OPEN) — anthropic provider reports $0.00 spend, budget caps never fire](https://github.com/zeroclaw-labs/zeroclaw/issues/9816)** — **Cost management is broken for Anthropic.** Every usage record has `cost_usd: 0.0`, meaning daily/monthly budget protections are silently non-functional. *Fix PR: None yet.*

- **[Issue #9815 (OPEN) — forbidden_paths is unreachable for paths under allowed_roots](https://github.com/zeroclaw-labs/zeroclaw/issues/9815)** — **Security policy bypass.** The path validation logic returns early on allowed roots, never reaching the forbidden-path check within those roots. *Relevant RFC: #8424.* *Fix PR: None yet.*

- **[Issue #9825 (OPEN) — leak detection redacts public blockchain addresses](https://github.com/zeroclaw-labs/zeroclaw/issues/9825)** — False positive in the leak detector breaking payment URLs. Severity not set, but it affects usability.

- **[Issue #9805 (OPEN) — SOP: auto-mode runs from channel/cron triggers never execute](https://github.com/zeroclaw-labs/zeroclaw/issues/9805)** — **Core SOP execution failure.** Runs block forever, consuming concurrency slots. *Fix PR: [#9494](https://github.com/zeroclaw-labs/zeroclaw/pull/9494) / [#9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841).*

- **[Issue #9786 (OPEN) — malformed SOP.toml silently dropped](https://github.com/zeroclaw-labs/zeroclaw/issues/9786)** — **Diagnostics gap.** A malformed config file is indistinguishable from a missing one, causing misleading validation success.

- **[Issue #9821 (OPEN) — cron tool: agent never invokes it, always falls back to shell](https://github.com/zeroclaw-labs/zeroclaw/issues/9821)** — Tool definition/instruction issue; model bypasses the native tool.

- **[Issue #9820 (OPEN) — calculator tool: model emits literal `<TOOLCALL>` pseudo-syntax](https://github.com/zeroclaw-labs/zeroclaw/issues/9820)** — Tool calling contract issue, likely affecting multiple models.

- **[Issue #9832 (OPEN) — zeroclaw-hardware fails to compile with --features hardware on aarch64](https://github.com/zeroclaw-labs/zeroclaw/issues/9832)** — Build break for a hardware feature, a regression flagged by a user.

- **[Issue #9834 (OPEN) — intermittent test failures from shared process-global state](https://github.com/zeroclaw-labs/zeroclaw/issues/9834)** — Flaky test suite affecting CI, reducing stability signals.

## 6. Feature Requests & Roadmap Signals

Several significant feature requests and RFCs signal the roadmap direction:

- **[Issue #9810 (OPEN) — RFC: Load Agent Plugins 1.0 skill and MCP packages](https://github.com/zeroclaw-labs/zeroclaw/issues/9810)** — Support for the vendor-neutral Agent Plugins standard is a major ecosystem play. It's a high-risk RFC marked as "needs-maintainer-review." This likely targets a future minor release (0.9.x).

- **[Issue #9346 (OPEN) — RFC: Define the unified package/capability/config/runtime-state catalog contract](https://github.com/zeroclaw-labs/zeroclaw/issues/9346)** — This is the consolidation effort for the catalog, building on the plugin work. It addresses architectural debt around how the system knows what it has. A longer-term effort.

- **[Issue #9824 (OPEN) — Feature: Simplify the default web-tool surface to web_fetch + web_research + http_request](https://github.com/zeroclaw-labs/zeroclaw/issues/9824)** — This is complemented by **[PR #9833](https://github.com/zeroclaw-labs/zeroclaw/pull/9833)**, which adds the `web_research` delegate sub-agent. This consolidation is likely to land in the next version.

- **[PR #9828 (OPEN) — feat(tools): agent-facing config authoring with operator-approved policy previews](https://github.com/zeroclaw-labs/zeroclaw/pull/9828)** — Gives agents a validated path to edit config, a major UX improvement for autonomous operation.

- **[PR #8337 (OPEN) — feat(observability): herdr agent reporting integration](https://github.com/zeroclaw-labs/zeroclaw/pull/8337)** — A large integration (size:XL) for Herdr status reporting, pending review.

- **[PR #8965 (OPEN) — feat(skills): declarative auto-activation with provider switch](https://github.com/zeroclaw-labs/zeroclaw/pull/8965)** — A large, stacked PR that has been open for a month; it depends on #9563. This is a long-running feature effort.

**Prediction:** The next minor release is likely to include the `web_research` tool, the headless SOP driver fix, and the `local_whisper` bearer token fix. The Agent Plugins RFC is a strong candidate for the subsequent release if maintainer review proceeds swiftly.

## 7. User Feedback Summary

User reports in the last 24 hours highlight several real-world pain points:

- **Configuration and Security Friction:** The `forbidden_paths` being unreachable (#9815) undermines user trust in the security model. Users are also hitting issues with the leak detector's false positives on blockchain addresses (#9825), indicating the heuristic is too aggressive for legitimate use cases.

- **Headless Automation Frustration:** Issues with cron-triggered SOPs and cron tools not working as documented (#9805, #9780, #9821) point to a mismatch between promised automation capabilities and actual runtime behavior. Users are trying to build watch-loops and unattended workflows and are hitting hard walls.

- **Observability Gaps:** The $0.00 spend reporting on Anthropic (#9816) is a serious problem for cost control; users cannot enforce budgets. The SOP silent-drop behavior (#9786) makes debugging difficult.

- **Model Tool-Calling Reliability:** Issues #9820 and #9821 show models (e.g., Llama 3.3 via NIM) failing to use the correct tool-calling syntax, indicating either insufficient tool schemas or model compatibility issues.

- **Build and Portability Concerns:** User on aarch64 flagged a compile failure (#9832), highlighting a lack of CI coverage for that platform.

Overall, users are attempting to use ZeroClaw for serious, production-like workflows (autonomous cron jobs, API integrations, budget controls) and are reporting that the current version (0.8.4) has too many rough edges in these areas.

## 8. Backlog Watch

Several important issues and PRs have been open for an extended period and are likely awaiting maintainer attention:

- **[Issue #8043 (OPEN, high risk, since 2026-06-20) — RFC: Retire the standalone aardvark-sys crate](https://github.com/zeroclaw-labs/zeroclaw/issues/8043)** — An architectural cleanup RFC with 9 comments. It has the `needs-author-action` tag, suggesting the author needs to address review feedback.

- **[PR #8948 (OPEN, since 2026-07-10) — fix(tools): reap exited stdio MCP server processes](https://github.com/zeroclaw-labs/zeroclaw/pull/8948)** — This P1 bug fix (zombie processes) has been open for a month. A rewrite (#9418) landed and may have superseded it, but this PR is still open. Needs a decision on closure or rebase.

- **[Issue #7130 (OPEN, since 2026-06-03) — Feature: forbid(unsafe_code) workspace-wide](https://github.com/zeroclaw-labs/zeroclaw/issues/7130)** — A security hardening issue open for over two months. It has `status:accepted` and `status:no-stale`, but no visible progress. This is a radar signal for overall security posture.

- **[Issue #9821 and #9820 (OPEN, new) — cron/calculator tool-calling failures](https://github.com/zeroclaw-labs/zeroclaw/issues/9821)** — While new, these should be prioritized due to their impact on core usability and prevalence across models.

- **[PR #9757 (OPEN, needs-author-action) — fix(providers/anthropic): deliver tool-result images as nested blocks](https://github.com/zeroclaw-labs/zeroclaw/pull/9757)** — A functional fix for multimodal input on the Anthropic provider, waiting for the author to respond to review.

- **[PR #8337 (OPEN, since 2026-06-26) — feat(observability): herdr agent reporting integration](https://github.com/zeroclaw-labs/zeroclaw/pull/8337)** — A size:XL PR that has been open for over a month, which can be a signal of review bottlenecks for large contributions.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*