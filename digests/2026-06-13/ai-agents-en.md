# OpenClaw Ecosystem Digest 2026-06-13

> Issues: 500 | PRs: 486 | Projects covered: 13 | Generated: 2026-06-13 02:03 UTC

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

# OpenClaw Project Digest — 2026-06-13

## Today's Overview

OpenClaw continues to show extremely high activity, with **500 issues** and **486 pull requests** updated in the last 24 hours, reflecting a deeply engaged community and rapid development pace. The project shipped **two new releases** today (v2026.6.6 and v2026.6.6-beta.2), both focused on comprehensive security hardening across transcripts, sandbox boundaries, MCP stdio, Codex HTTP access, and multiple chat platforms. While the volume of open items remains high (408 open issues, 344 open PRs), the team is actively processing work — 92 issues and 142 PRs were closed or merged today. A critical **P0 memory leak** (#91588) and several P1 bugs remain open with active PRs in progress, indicating the maintainers are prioritizing stability alongside feature work.

## Releases

### v2026.6.6 (stable) — openclaw 2026.6.6
- **Security hardening** substantially tightened across: transcripts, sandbox binds, host environment inheritance, MCP stdio, Codex HTTP access, native search policy, elevated sender checks, deleted-agent ACP bypasses, loopback tools, Discord moderation, and Teams group actions
- `exec` command security boundaries reinforced
- No migration notes or breaking changes documented in the release summary

### v2026.6.6-beta.2 (beta)
- Identical security hardening scope to the stable release

*No detailed changelog or migration guide was included in the release data provided.*

## Project Progress

**142 PRs merged/closed today**, with the following notable fixes and features advancing:

### Merged Fixes
- **#92566** — Lifecycle timeout cleanup after leader exit (RomneyDa)
- **#92565** — DeepSeek prompt cache key enabled in model catalog (fsdwen) — fixes prompt caching for DeepSeek models
- **#92435** — Gateway skip SIGUSR1 restart for `browser.profiles` config changes (liuhao1024) — fixes #43803
- **#92427** — Skill workshop description limit increased from 160 to 500 characters (liuhao1024)
- **#92396** — Moonshot/Kimi `reasoning_content` backfilled on assistant tool-call replay messages (xialonglee)
- **#92390** — Outbound routing fix for direct-only plugin bare targets (liuhao1024) — fixes #92384
- **#92368** — Warning emitted for empty `allOf`/`anyOf` availability groups (liuhao1024)
- **#92357** — Memory hybrid search now preserves keyword-only results when chunk IDs don't overlap (liuhao1024) — fixes #92337
- **#92348** — Feishu channel ignores `bot_p2p_chat_entered_v1` events to prevent gateway restarts (liuhao1024)
- **#92335** — Exec-approvals YOLO fast path works with socket tokens (liuhao1024)
- **#92319** — Workboard delete tool and CLI command added (liuhao1024)
- **#92308** — Windows absolute paths preserved in QMD command resolution (liuhao1024)
- **#92229** — Doctor preview channel SecretRef resolution fixed (joshavant)

### Still Open / In Review
- **#92557** — ClawHub plugin metadata validation in PRs (Patrick-Erichsen)
- **#92570** — Browser cache/profile directories excluded from live auth staging (zenglingbiao)
- **#92568** — Cron active task ledger cancellation (leno23)
- **#92558** — QA scorecard mapping shape simplified (RomneyDa)
- **#92550** — Telegram RTT sampling folded into QA evidence (RomneyDa)
- **#92571** — Duplicate cleaned assistant transcript entries deduplicated for session memory (arkyu2077)

## Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Comments | Summary |
|-------|----------|---------|
| **#25592** — [P1, Security] Text between tool calls leaks to messaging channels | 32 👍1 | Internal processing output leaks to Slack/iMessage — **critical UX/security issue** |
| **#9443** — [Enhancement, P2] Prebuilt Android APK releases | 25 👍2 | Community request for downloadable APK builds |
| **#32473** — [Bug, Regression] Control UI requires device identity (HTTPS/localhost) | 17 👍5 | Docker VPS users blocked by secure context requirement |
| **#22438** — [P2] Tiered bootstrap file loading for progressive context control | 17 👍0 | Token waste from loading all bootstrap files on every session |
| **#22676** — [P1] Signal daemon `stop()` race condition on SIGUSR1 restart | 17 👍0 | Orphaned processes on gateway restart |
| **#32296** — [P1] Agent replies to previous message instead of current | 15 👍1 | Session context confusion — core UX regression |
| **#29387** — [P1] Bootstrap files in agentDir silently ignored | 14 👍5 | Per-agent directories don't load bootstrap files |
| **#18160** — [P2] Direct Exec Mode for Cron Jobs | 13 👍11 | **Most upvoted open feature** — cron jobs need direct execution without LLM |
| **#57326** — [P1] CLI-backed helper paths bypass CLI dispatch | 13 👍1 | Remaining surface area of CLI backend fix |
| **#12602** — [P2] Slack Block Kit support | 13 👍0 | Richer Slack message formatting |
| **#74484** — Gateway pairing scope deadlock | 12 👍2 | CLI stuck in scope escalation loop |
| **#31583** — [P1] `exec` tool doesn't inherit skill env variables | 12 👍2 | Regression — secrets not passed to subprocesses |

### Analysis
The community is clearly focused on **reliability and security**. The top-voted active feature request (#18160, 11 👍) asks for direct execution in cron jobs, indicating frustration with LLM-based cron reliability. The #25592 "text leakage" issue (32 comments) is the most discussed, reflecting high concern about privacy/security boundaries. Multiple threads about session context confusion (#32296) and agent directory configuration (#29387, 14 comments) suggest configuration and state management are significant pain points.

## Bugs & Stability

### Critical (P0)
- **#91588** — **Gateway Memory Leak** — RSS grows 350MB → 15.5GB over 2-3 days, causing OOM kills and restart loops. **Open, no fix PR yet.** Labeled `clawsweeper:needs-maintainer-review`. This is the highest-severity active issue.

### High Priority (P1) — Open
| Issue | Category | Fix PR? | Summary |
|-------|----------|---------|---------|
| **#25592** | Security/Message Loss | No | Text between tool calls leaks to channels |
| **#22676** | Crash Loop/Message Loss | No | Signal daemon race condition on restart |
| **#32296** | Session State | No | Agent replies to wrong message (context confusion) |
| **#29387** | Session State/Security | No | Bootstrap files in agentDir silently ignored |
| **#57326** | Security/Auth | No | CLI helper paths still bypass dispatch |
| **#31583** | Security/Auth | No | `exec` tool ignores skill env variables |
| **#29736** | Security | No | Exec approvals writes to wrong path |
| **#38327** | Auth/Crash Loop | No | `Cannot convert undefined or null to object` on Gemini |
| **#83184** | Session State/Message Loss | No | Heartbeat replies stuck on pendingFinalDelivery |
| **#92043** | Session State/Crash Loop | No | 180s compaction timeout too short, fails identically every turn |
| **#91778** | Session State | No | `memory_search` index metadata missing since v2026.6.1 (French reporter) |
| **#88951** | Message Loss | No | Duplicate message content 2-4× per message |
| **#86538** | Session State/Message Loss | No | Session write-lock timeouts block subagent delivery |
| **#89039** | Message Loss | **PR #89039 open** | Silent message loss from `EmbeddedAttemptSessionTakeoverError` |
| **#89041** | Availability | **PR #89041 open** | Discord WS 8.21.0 receiver part limits |

### Regressions
- **#32473** — Control UI requires HTTPS/Docker secure context (regression)
- **#31583** — `exec` tool env variable inheritance (regression)
- **#38327** — Gemini model crash on v2026.3.2 (regression)
- **#38439** — Webchat avatar endpoint returns 404 (regression)
- **#84644** — Windows node-host connects but reports no commands (regression)

### Notable: Memory Search Broken
**#91778** (P0-level severity report from a French-speaking user) reports `memory_search` vector index metadata has been missing since v2026.6.1, affecting all agents. **No fix PR yet.** This is a significant functionality regression.

## Feature Requests & Roadmap Signals

### Most Requested New Features
1. **#18160** — Direct Exec Mode for Cron Jobs (11 👍) — bypass LLM for simple cron commands
2. **#6615** — Denylist support for exec-approvals (7 👍) — "allow everything except X" policy
3. **#20786** — Telegram Business Bot support (6 👍)
4. **#27445** — `announceTarget` option for sub-agent completion routing (5 👍)
5. **#29387** — Agent directory bootstrap file loading (5 👍, also a bug report)
6. **#32473** — HTTPS/localhost workaround for control UI (5 👍, also a bug)
7. **#37634** — Writable workspace in isolation mode (6 👍)

### Predictions for Next Release
Based on current PR activity and issue prioritization:
- **Memory search fix** (#91778) — likely to ship quickly given P0 severity
- **CLI dispatch bypass fix** (#57326) — remaining surface area of already-patched issue
- **Feishu event handling** (#42351, fixed by #92348) — already merged
- **Workboard delete tool** (#92319, #92314) — already merged
- **DeepSeek prompt caching** (#92565) — already merged
- **Gateway restart on browser config** (#43803, fixed by #92435) — already merged
- **Browser profile directory exclusion from auth staging** (#91893, PR #92570) — in review

### Long-term Signals
The **#35203 RFC** (8 comments) for multi-agent collaboration with capability profiling, shared blackboard, and token governance suggests users are hitting limits of the current sub-agent architecture. The **#40418** proposal for automated session memory preservation across `/new` resets indicates users want persistent learning.

## User Feedback Summary

### Pain Points
1. **Memory search broken** (#91778) — "All agents are blind" since v2026.6.1, French user report with strong emotional language
2. **Gateway memory leak** (#91588) — OOM kills every 2-3 days, production users affected
3. **Message duplication** (#88951) — Responses duplicated 2-4× since v2026.5.27 upgrade
4. **Cron job unreliability** (#18160, 11 👍) — LLM interpretation of cron commands causes timeouts and failures
5. **Session context confusion** (#32296) — Agent responds to wrong messages, disorienting for users
6. **Configuration complexity** (#32473, #29387, #57326) — Docker users blocked, per-agent configs ignored, CLI scope deadlocks
7. **Tool call privacy** (#25592) — Internal processing text leaking to public channels

### Satisfaction Signals
- High engagement from contributors (142 PRs merged today)
- Users actively filing detailed bug reports with reproduction steps
- Multiple users contributing fixes (liuhao1024 alone merged 8 PRs today)
- Feature requests show sophisticated understanding of the platform

### Language & Accessibility
- #91778 filed in French by "Mami-Nora" — suggests non-English-speaking user base
- #9443 filed via AI assistant on behalf of another user ("Lysen, by his AI assistant QING") — indicates AI-mediated workflows

## Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Age | Label | Why Stalled |
|-------|-----|-------|-------------|
| **#9443** — Prebuilt Android APK (25 comments) | Since 2026-02-05 | `needs-product-decision`, `needs-security-review` | 4 months old, community strongly desires |
| **#10687** — Dynamic model discovery (9 comments) | Since 2026-02-06 | `needs-product-decision` | 4 months, no maintainer review |
| **#7707** — Memory trust tagging by source (8 comments) | Since 2026-02-03 | `needs-maintainer-review`, `needs-product-decision` | Security feature, 4+ months |
| **#13610** — Native secrets management (7 comments) | Since 2026-02-10 | `needs-security-review` | Security infrastructure, 4 months |
| **#14785** — Reduce tool schema overhead (7 comments) | Since 2026-02-12 | `needs-maintainer-review`, `needs-product-decision` | Token optimization, 4 months |
| **#16670** — Memory setup in onboarding wizard (8 comments) | Since 2026-02-15 | `needs-maintainer-review`, `needs-product-decision` | UX improvement, 4 months |
| **#20786** — Telegram Business support (8 comments, 6 👍) | Since 2026-02-19 | `needs-maintainer-review`, `needs-product-decision` | 4 months, popular request |
| **#22358** — Post-subagent completion hook (12 comments) | Since 2026-02-21 | `needs-maintainer-review`, `needs-product-decision`, `needs-security-review` | 3.5 months, all three review stages |
| **#91588** — Critical memory leak (9 comments, P0) | Since 2026-06-09 | `needs-maintainer-review`, `needs-info` | 4 days old but P0 — needs immediate triage |
| **#91778** — memory_search broken (7 comments, reporter calls P0) | Since 2026-06-09 | `needs-live-repro` | French user, P0 severity claim, no fix |

### PRs Needing Review
| PR | Age | Risk Tags | Status |
|----|-----|-----------|--------|
| **#81957** — CI supply-chain hardening | Since 2026-05-14 (30 days) | 🚨 automation, compatibility, security-boundary | Open, proof supplied |
| **#89799** — Skip compile cache on Node 24.x | Since 2026-06-03 (10 days) | 🚨 compatibility, availability | Open, proof supplied |
| **#89039** — Prevent silent message loss | Since 2026-06-01 (12 days) | 🚨 compatibility, availability | Open, proof supplied, P1 |
| **#89041** — Discord WS limits fix | Since 2026-06-01 (12 days) | 🚨 availability | Open, proof supplied, P1 |
| **#90231** — Subagent WeChat callback routing | Since 2026-06-04 (9 days) | 🚨 session-state, message-delivery | Open, proof supplied |
| **#90610** — Codex final answer candidates in activity | Since 2026-06-05 (8 days) | 🚨 session-state | Open, proof supplied |
| **#92251** — Subagent provenance carry-through | Since 2026-06-11 (2 days) | 🚨 session-state | Open, proof supplied |
| **#92422** — Cron yield/AbortError fix | Since 2026-06-12 (1 day) | 🚨 session-state, message-delivery | Open, proof supplied, P1 |
| **#92568** — Cancel active task ledger runs | Since 2026-06-13 (today) | None noted | Open, needs review |

---

*Generated from OpenClaw GitHub data. All links: https://github.com/openclaw/openclaw/issues/* and https://github.com/openclaw/openclaw/pull/*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digests.

---

## Cross-Project Ecosystem Comparison Report: 2026-06-13

### 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is characterized by extreme fragmentation and rapid, high-velocity iteration. The landscape ranges from core monolithic frameworks (OpenClaw) to specialized desktop clients (CoPaw), mobile-first agents (PicoClaw), and experimental "agent operating systems" (Claw-ecosystem variants). A clear schism is emerging between projects prioritizing large-scale production stability (OpenClaw) and those focused on rapid feature experimentation and novel UX (NanoBot, Hermes Agent). The ecosystem is currently grappling with common pain points around memory persistence, session management, and security boundaries, while the underlying trend points toward multi-agent collaboration, local-first inference, and enhanced observability as key differentiators.

### 2. Activity Comparison

| Project | Issues (Updated 24h) | PRs (Updated 24h) | Release Status (Today) | Health Score* |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 486 | Stable (v2026.6.6) + Beta | B+ (High throughput, critical P0 bugs) |
| **Hermes Agent** | 50 | 50 | No new release (v2026.5.28+) | B (High activity, many closed issues) |
| **IronClaw** | 50 | 50 | No new release | B (High activity, CI blocked) |
| **NanoBot** | 6 | 30 | No new release | A- (Good velocity, focused issues) |
| **CoPaw (QwenPaw)** | 23 | 25 | Beta preparation (v1.1.12b1) | B (Maintenance heavy, mixed stability) |
| **ZeroClaw** | 14 | 33 | No new release (v0.8.0) | B- (High dev activity, significant regressions) |
| **LobsterAI** | 1 | 17 | Pending release (v2026.6.11 merged) | A (Consolidating, few open bugs) |
| **PicoClaw** | 6 | 14 | Nightly (v0.2.9-nightly) | B+ (High velocity, diverse contributors) |
| **Moltis** | 3 | 0 | No new release | C+ (Discussions only, no code merges) |
| **NullClaw** | 1 | 3 | No new release | C+ (Focused maintenance, slower cycle) |
| **NanoClaw** | 5 | 9 | No new release (v2.0.64+) | C+ (High PR backlog, no merges today) |
| **ZeptoClaw** | 0 | 0 | No activity | D (Inactive) |
| **TinyClaw** | 0 | 0 | No activity | D (Inactive) |

***Health Score is a qualitative assessment based on throughput, bug severity, release cadence, and contributor engagement.**

### 3. OpenClaw's Position

OpenClaw maintains its position as the ecosystem's **core reference architecture** by a significant margin, driven by massive scale and robust governance.

- **Advantages vs. Peers:**
    - **Maturity & Scale:** With ~500 issues and ~486 PRs updated daily, OpenClaw's developer mindshare is an order of magnitude larger than any other project. It is the clear "standard" to build upon.
    - **Comprehensive Security:** The v2026.6.6 stable release focused on systemic security hardening (transcripts, sandbox, MCP, chat platforms), a depth of safety review not seen in other projects.
- **Technical Approach Differences:**
    - OpenClaw’s architecture is monolithic and deeply integrated, contrasting with more modular approaches like IronClaw’s Reborn WebUI or NanoBot’s provider-agnostic runtime. This provides consistency but increases the blast radius of bugs (e.g., the critical P0 memory leak #91588).
- **Community Size Comparison:**
    - OpenClaw’s community is not just larger but also more **generative**. A single contributor (liuhao1024) merged more PRs in one day than most entire projects had updates. This creates a virtuous cycle of contributions but also a high noise-to-signal ratio.

### 4. Shared Technical Focus Areas

Several cross-cutting themes are emerging as universal requirements, indicating key pain points for developers building AI agents.

1.  **Memory & Contextual Persistence (Critical Gap):**
    - **Projects Affected:** OpenClaw, NanoBot, Hermes Agent, PicoClaw, NanoClaw.
    - **Specific Needs:** Fixing "memory search broken" (#91778 in OpenClaw), "short-term memory loss" (#4044 in NanoBot), "post-turn consolidation wipes delivery" (#4307 in NanoBot), and "session DB drops messages" (#44837 in Hermes Agent). All projects are struggling to maintain coherent agent state across turns and sessions.
2.  **Session & Lifecycle Management (Reliability):**
    - **Projects Affected:** OpenClaw, NanoBot, Hermes Agent, CoPaw, ZeroClaw.
    - **Specific Needs:** Leaks (OpenClaw #91588), premature job completion (NanoBot #4304), orphaned subprocesses (Hermes #22676), silent task failures (CoPaw #5064), and first-run setup failures (ZeroClaw #7537). The ecosystem is struggling with the basic "operating system" functions of managing agent processes.
3.  **Security & Sandbox Hardening (Trust & Safety):**
    - **Projects Affected:** OpenClaw, NanoBot, PicoClaw, NanoClaw.
    - **Specific Needs:** Preventing internal processing text from leaking to channels (OpenClaw #25592), blocking symlink workspace escapes (NanoBot #4119), gating dangerous MCP tools with RBAC (NanoClaw #2711), and fixing "exec" tool environment variable inheritance (OpenClaw #31583).
4.  **Channel Integration Fidelity (Platform Complexity):**
    - **Projects Affected:** OpenClaw, Hermes Agent, PicoClaw, CoPaw, ZeroClaw.
    - **Specific Needs:** Telegram forum topic routing (PicoClaw #3110), rich table formatting (Hermes #45323), Signal adapter enhancements (Hermes #39043), and streaming message support for Asian platforms (ZeroClaw #7531).

### 5. Differentiation Analysis

| Feature/User Focus | OpenClaw | IronClaw / NanoBot | Hermes Agent | CoPaw (QwenPaw) |
| :--- | :--- | :--- | :--- | :--- |
| **Core Target User** | Enterprise / Power Developer | Hobbyist / UX-focused Developer | Desktop User / Explorer | Chinese-speaking Desktop User |
| **Differentiating Feature** | Production-grade security & config | Modularity & modern UX (WebUI) | Human-like memory architecture | Deep integration with AgentScope 2.0 & Alibaba cloud |
| **Architecture Strength** | Monolithic stability & scale | Composable, API-first design | Fast feature iteration on desktop | Strong AI-driven agent autonomy (scheduling) |
| **Weakness** | High complexity, slow to fix P0 bugs | Infrastructure stability (CI, security) | Session state management gaps | Regression fatigue & Windows/Docker stability |
| **Community Language** | English (global) | English (global) | English (global) | Primarily Chinese |
| **Release Cadence** | Stable + Beta (frequent) | Slower, feature-packed | Stable with patch bursts | Point releases (fast, buggy) |

This analysis highlights a core tension: **OpenClaw is the "Linux kernel"**, while **IronClaw and NanoBot are the "Ubuntu Desktops"** of this ecosystem. This implies different risk profiles for developers building on top of each.

### 6. Community Momentum & Maturity

- **Tier 1 (Rapidly Iterating / High Risk-Reward):** **OpenClaw, NanoBot, Hermes Agent, ZeroClaw.** These projects have high throughput, active maintainers, and significant community engagement. However, they also show the highest number of critical open bugs, suggesting velocity sometimes outpaces stability.
- **Tier 2 (Consolidating / Stabilizing):** **LobsterAI, PicoClaw, CoPaw.** These projects are in a phase of integrating features and fixing bugs before a major release. LobsterAI, in particular, appears to be successfully closing out technical debt.
- **Tier 3 (Mature / Slow Iteration):** **IronClaw, NullClaw, Moltis.** These projects have steady, lower-velocity development. They are either awaiting architectural decisions (IronClaw, blocked CI) or operating in a review-oriented phase (Moltis).
- **Tier 4 (Inactive / Frozen):** **ZeptoClaw, TinyClaw.** These projects show zero activity and are effectively dead or stagnant.

### 7. Trend Signals

Analysis of user feedback and issue content reveals several key industry trends for AI agent developers:

1.  **Local-First Inference is a Major Unmet Need:** User complaints about local model integration (NullClaw #952, CoPaw #5163) and requests for local STT (Moltis #1102) and model routers (ZeroClaw #7539) signal a strong market segment that wants to avoid cloud API dependence for cost, privacy, and latency reasons.
2.  **Demand for "Agent Observability" is Surging:** The push for audit subsystems (NanoBot #4319), session traces (CoPaw #5127), and turn-completion lifecycle signals (PicoClaw #2984) indicates that as agents become more autonomous, developers need better tools to understand and debug their behavior.
3.  **Reliability Trumps Features:** The most upvoted feature requests are not for new capabilities, but for reliability improvements: "Direct Exec Mode for Cron Jobs" (OpenClaw #18160) and "Persistent Approvals" (IronClaw #4825). Users are frustrated with agents that "smell" smart but fail unpredictably.
4.  **The "Silent Failure" is the Worst Bug:** The highest-impact bugs across the ecosystem are those where an agent fails without user-visible errors (e.g., silent message drops, tasks that don't trigger). This erodes user trust faster than a crash.

**Value for AI Agent Developers:** The data suggests the ecosystem is in a "trough of disillusionment" regarding agent autonomy. The winning projects will be those that invest heavily in **session state resilience, security boundaries, and platform-specific integration testing** rather than adding more "agentic superpowers." For developers choosing a platform, OpenClaw provides the most foundational layer for enterprise risk, while IronClaw or NanoBot offer a simpler path to a working demo but with higher operational risk.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — June 13, 2026

## Today's Overview

NanoBot shows **high development velocity** with 30 PRs updated in the last 24 hours and 6 issues active, signaling a mature project undergoing substantial feature expansion and stabilization. The community and core team are converging on three major themes: **audit/observability** (three related audit PRs from a single author), **memory and context management** (multiple fixes for history corruption, cursor monotonicity, and consolidation), and **WebUI/config parity** (a large settings unification PR). Three open bugs (short-term memory loss, post-turn consolidation wipes, zero usage tokens) remain active and indicate ongoing reliability work. No new releases were cut today.

## Releases

No new releases were published in this period.

## Project Progress

**9 PRs were merged or closed today**, advancing several key areas:

| PR | Summary | Impact |
|----|---------|--------|
| [#4319](https://github.com/HKUDS/nanobot/pull/4319) [CLOSED] | `feat(audit): Add tools.audit for agent action observability` | New audit module for tool invocations with 4 transport backends |
| [#4318](https://github.com/HKUDS/nanobot/pull/4318) [CLOSED] | `feat(audit): Add tools.audit for agent action observability` | Duplicate/early version of audit feature |
| [#4304](https://github.com/HKUDS/nanobot/pull/4304) [CLOSED] | `fix(cron): wait for spawned subagents before marking cron job complete` | Critical cron reliability fix — prevents premature job completion |
| [#4203](https://github.com/HKUDS/nanobot/pull/4203) [CLOSED] | Bug: `find_legal_message_start` discards all messages on orphaned tool results | Core session logic bug squashed |
| [#4006](https://github.com/HKUDS/nanobot/pull/4006) [CLOSED] | Orphaned tool results in conversation history | API compliance fix for OpenAI/Anthropic |
| [#4305](https://github.com/HKUDS/nanobot/pull/4305) [CLOSED] | Multiple custom providers enhancement | Infrastructure for multi-provider setups |

Key improvements include:
- **Audit subsystem** reaches merged status across two PRs
- **Cron/subagent lifecycle** fixed — prevents race conditions where jobs marked complete while subagents still execute
- **Session management** hardened against orphaned tool results causing message loss
- **Config schema** decoupled from tool runtimes (PR [#4314](https://github.com/HKUDS/nanobot/pull/4314)) — important architectural cleanup

## Community Hot Topics

**High-engagement discussions (by comment count):**

| Issue/PR | Comments | Topic | Analysis |
|----------|----------|-------|----------|
| [#4044](https://github.com/HKUDS/nanobot/pull/4044) [OPEN] | 5 comments | **Short-term memory loss bug** — Root cause analysis links to context window pressure from system prompts (SOUL.md, USER.md, MEMORY.md). Community actively debugging. | *Critical UX issue: users experience conversational amnesia, destroying trust in the agent.* |
| [#4203](https://github.com/HKUDS/nanobot/pull/4203) [CLOSED] | 3 comments | Orphaned tool result bug — `find_legal_message_start` discards entire message sequence | *Closed with fix, but 3 comment threads show community engagement in diagnosing root cause.* |
| [#4006](https://github.com/HKUDS/nanobot/pull/4006) [CLOSED] | 2 comments | Orphaned tool results violating API specs | *Closed; shows community cares about strict API compliance.* |

**Underlying need**: Users are experiencing **conversation coherence failures** — the agent's inability to maintain context across turns. The community is actively contributing root-cause analysis, suggesting a sophisticated user base willing to debug core issues.

## Bugs & Stability

**Active bugs ranked by severity:**

| Severity | Issue | Description | Fix PR Exists? |
|----------|-------|-------------|----------------|
| **Critical** | [#4044](https://github.com/HKUDS/nanobot/pull/4044) | **Short-term memory loss** — Agent asks question, forgets answer; conversational thread snaps | No PR identified |
| **Critical** | [#4307](https://github.com/HKUDS/nanobot/pull/4307) | **Post-turn consolidation wipes agent's delivery message** — With modest `context_window_tokens` (e.g., 40k), long turns accumulate 100k+ tokens; consolidation archives assistant's own delivery, breaking user follow-up references | No PR identified |
| **High** | [#4309](https://github.com/HKUDS/nanobot/pull/4309) | `/v1/chat/completions` always returns zero usage tokens — OpenAI-compatible endpoint broken for token accounting | No PR identified |

**Recent fixes (closed today):**
- PR [#4203](https://github.com/HKUDS/nanobot/pull/4203) — `find_legal_message_start` discarding all messages (now fixed)
- PR [#4304](https://github.com/HKUDS/nanobot/pull/4304) — Cron jobs not waiting for spawned subagents (now fixed)

**Regression risk**: The three open critical bugs all relate to **memory and context management**, suggesting the recent feature velocity may have outrun stability in this subsystem. Consolidation logic, cursor management, and context window pressure are recurring themes across 6+ PRs in flight.

## Feature Requests & Roadmap Signals

**User-requested features with high community interest:**

| Request | Issue/PR | Likelihood for Next Release |
|---------|----------|----------------------------|
| **Multiple custom providers** | [#4305](https://github.com/HKUDS/nanobot/pull/4305) [CLOSED] | **High** — Already merged as enhancement; community can now define >1 custom provider |
| **WebUI/config.json parity** | [#4313](https://github.com/HKUDS/nanobot/pull/4313) [OPEN] | **High** — Large PR with write endpoints for temperature, tool limits, dream, channels, memory fields |
| **TTS multi-provider** | [#4316](https://github.com/HKUDS/nanobot/pull/4316) [OPEN] | **Medium-High** — OpenAI, Groq (Orpheus), ElevenLabs support added; needs review/merge |
| **Agent action audit/observability** | [#4320](https://github.com/HKUDS/nanobot/pull/4320) [OPEN] | **High** — Three iterations landed today; minimal, unopinionated audit module |
| **Python SDK expansion** | [#4296](https://github.com/HKUDS/nanobot/pull/4296) [OPEN] | **Medium** — Adds `RunResult` metadata, stable session/memory/runtime controls |

**Prediction**: The **audit subsystem** and **WebUI settings parity** are likely to land in the next release (both have active, large PRs). The **TTS system** may ship as a minor feature. The **multiple custom providers** enhancement is already closed and should appear in the next version.

## User Feedback Summary

**Pain points (recurring themes across 6 issues):**

1. **Conversation memory loss (Critical)** — Users report the agent cannot maintain context across turns, destroying conversational coherence. One user reports: *"It has no memory of asking. The conversational thread snaps between its turn and yours."*
2. **Context window pressure** — System prompts (SOUL.md, USER.md, MEMORY.md) consume context, pushing out user interactions. Sophisticated users are digging into `context_window_tokens` settings.
3. **Post-turn consolidation data loss** — With modest context windows, long turns result in assistant delivery messages being archived, breaking follow-up references.
4. **Zero usage tokens** — The OpenAI-compatible endpoint returns `"usage": { "prompt_tokens": 0, "completion_tokens": 0, "total_tokens": 0 }`, breaking billing and monitoring integrations.
5. **Orphaned tool results** (now fixed) — Previously caused API rejections from strict API validators.

**Satisfaction indicators**: Despite bugs, the community is actively contributing PRs (30 in 24h) and detailed root-cause analysis, indicating a **highly engaged, technically sophisticated user base** that sees value in the platform.

## Backlog Watch

**Items requiring maintainer attention:**

| Item | Age | Status | Concern |
|------|-----|--------|---------|
| [#4044](https://github.com/HKUDS/nanobot/pull/4044) — Short-term memory loss | **16 days** (since May 28) | OPEN, 5 comments | **Critical UX bug** unaddressed; no fix PR exists; community asking for maintainer guidance |
| [#4307](https://github.com/HKUDS/nanobot/pull/4307) — Post-turn consolidation wipes delivery | **1 day** | OPEN, 1 comment | Newly reported but critical — maintainers should prioritize triage |
| [#3983](https://github.com/HKUDS/nanobot/pull/3983) — Runner blocked tool-call finish reasons | **20 days** (since May 24) | OPEN | Test coverage PR; no activity or merge despite age |
| [#3982](https://github.com/HKUDS/nanobot/pull/3982) — Scripted agent runner harness | **20 days** (since May 24) | OPEN | Companion test infrastructure PR; stale without review |
| [#4119](https://github.com/HKUDS/nanobot/pull/4119) — Block relative symlink workspace escapes | **13 days** (since May 31) | OPEN | **Security fix** — prevents symlink-based workspace escapes; needs urgent review |
| [#4053](https://github.com/HKUDS/nanobot/pull/4053) — Keep read-only roots out of write paths | **15 days** (since May 29) | OPEN | **Security fix** — prevents write tools from inheriting read-only path access; stale |

**Key risk**: Two **security-relevant PRs** ([#4119](https://github.com/HKUDS/nanobot/pull/4119) and [#4053](https://github.com/HKUDS/nanobot/pull/4053)) have been open for 13 and 15 days respectively without maintainer review. Meanwhile, the **critical memory loss bug** (#4044) has gone 16 days without a fix PR. The backlog of test infrastructure PRs ([#3983](https://github.com/HKUDS/nanobot/pull/3983), [#3982](https://github.com/HKUDS/nanobot/pull/3982), [#4193](https://github.com/HKUDS/nanobot/pull/4193)) from contributor `yu-xin-c` indicates substantial testing investment that needs maintainer bandwidth to merge.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-13

## Today's Overview

Hermes Agent shows **very high activity** today with 50 issues and 50 PRs updated in the last 24 hours, though only 6 issues and 5 PRs were closed/merged. The project is processing a surge of bug reports — particularly around the Minimax provider, Windows crashes, and desktop GPU issues — while maintainers are actively merging fixes for critical memory and delegation bugs. No new releases are published today, but the PR pipeline suggests multiple fixes are heading toward the next patch. The community continues to drive feature requests around session unification, UI polish, and multi-platform improvements.

## Releases

No new releases today. The latest stable version remains **v2026.5.28+** (per issue references).

## Project Progress

**5 PRs merged/closed today:**
- [#44890](https://github.com/NousResearch/hermes-agent/pull/44890) — **Closed** (duplicate): Fix compression chain in session resume for Desktop gateway
- [#45242](https://github.com/NousResearch/hermes-agent/issues/45242) — **Closed** (duplicate): `auxiliary_client.py` unhandled `oauth_minimax` auth type
- [#38389](https://github.com/NousResearch/hermes-agent/issues/38389), [#38391](https://github.com/NousResearch/hermes-agent/pull/38391), [#38392](https://github.com/NousResearch/hermes-agent/pull/38392) — **Closed** (duplicate): Context compression summaries polluting visible conversation (P1)
- [#44837](https://github.com/NousResearch/hermes-agent/issues/44837) — **Closed**: Session DB turn-end flush dropping assistant messages

**Active PRs advancing features/fixes today:**
- [#44897](https://github.com/NousResearch/hermes-agent/pull/44897) — Adds **human-like memory architecture** layers (working memory, semantic records, episodic recall)
- [#44891](https://github.com/NousResearch/hermes-agent/pull/44891) — Structured key naming helpers for **Kanban swarm blackboard**
- [#44886](https://github.com/NousResearch/hermes-agent/pull/44886) — **Feishu** group chat fix (read `group_policy` from config + WS fallback)
- [#44887](https://github.com/NousResearch/hermes-agent/pull/44887) — **Curator review iteration cap** (was looping 4 hours on 26 symlinked skills)
- [#44896](https://github.com/NousResearch/hermes-agent/pull/44896) — **WhatsApp debounce** lowered from 5s/10s → 0.3s/2.0s (matches Telegram cadence)
- [#45341](https://github.com/NousResearch/hermes-agent/pull/45341) — **Windows GPU crash fix** (`--no-angle` flag + `HERMES_DESKTOP_DISABLE_GPU`)

## Community Hot Topics

- [#7237](https://github.com/NousResearch/hermes-agent/issues/7237) **[CLOSED] [Bug]** — *"Response truncated due to output length limit"* — **41 comments, 5 👍** — The highest-engagement issue. Users across CLI, Telegram, Discord, and Slack all hit output truncation mid-stream when generating long responses. This is a recurring pain point that affects all long-form use cases. **Status: Closed** (fix presumably applied upstream).

- [#41222](https://github.com/NousResearch/hermes-agent/issues/41222) **[OPEN] [Feature]** — *"Integrate Kanban Board into Desktop App"* — **2 comments, 1 👍** — Multi-agent workflow users want the Kanban board (currently CLI-only) embedded in the Desktop GUI to avoid context-switching.

- [#44140](https://github.com/NousResearch/hermes-agent/issues/44140) **[OPEN] [Feature]** — *"Desktop GUI — auto-scroll, sidebar overlap fix, custom session groups"* — **2 comments, 2 👍** — Three specific Desktop UX improvements requested: chat auto-scroll during streaming, sidebar/scrollbar overlap, and custom session grouping.

- [#45336](https://github.com/NousResearch/hermes-agent/issues/45336) **[OPEN] [Bug]** — *"TUI routes follow-up prompts into delegated child sessions"* — Newly reported: child/subagent sessions can accidentally become the active conversation in TUI, causing user prompts to go to the wrong agent.

## Bugs & Stability

### High Severity (P1)
- [#23473](https://github.com/NousResearch/hermes-agent/issues/23473) **[OPEN]** — **Gateway leaks VIRTUAL_ENV into subprocesses** — Running `uv sync` inside any project bricks Hermes' own venv. Last updated May 11 — **no maintainer response**. This is a **blocker** for any agent that needs to install dependencies.
- [#44837](https://github.com/NousResearch/hermes-agent/issues/44837) **[CLOSED]** — **Session DB drops assistant messages** on turn-end flush after `repair_message_sequence` compaction. **Fixed and closed** today.

### Medium Severity (P2)
- [#44976](https://github.com/NousResearch/hermes-agent/issues/44976) **[OPEN]** — **Minimax-M3 provider collapses nested single-element arrays** into `{"item": ...}` — breaks MCP tool calls. Reported yesterday, **no fix PR yet**.
- [#45323](https://github.com/NousResearch/hermes-agent/issues/45323) **[OPEN]** — **Telegram rich tables rewritten as bullets** by shared formatter — tables lose native rendering in Telegram. **Fix PR [#45343](https://github.com/NousResearch/hermes-agent/pull/45343) addresses related streaming lag** but not this specific issue.
- [#43936](https://github.com/NousResearch/hermes-agent/issues/43936) **[OPEN]** — **State.db drops assistant messages on interrupt** — `.jsonl` fallback was removed, so session data is lost. **No fix PR**.
- [#30091](https://github.com/NousResearch/hermes-agent/issues/30091) **[OPEN]** — **Slack bot-to-bot messages dropped** in shared threads even with `allow_bots=all`. Reported May 21 — **stale, no maintainer response**.
- [#17999](https://github.com/NousResearch/hermes-agent/issues/17999) **[OPEN]** — **Windows `read_file` tool cannot access D: drive** — "File not found" for valid paths. Reported April 30 — **stale, no response**.
- [#44763](https://github.com/NousResearch/hermes-agent/issues/44763) **[OPEN]** — **`computer_use` element bounds are always zero** on macOS — breaks spatial grounding. **No fix PR**.
- [#44866](https://github.com/NousResearch/hermes-agent/issues/44866) **[OPEN]** — **MCP OAuth polls 30s on probe failure** instead of returning immediately. **No fix PR**.
- [#45308](https://github.com/NousResearch/hermes-agent/issues/45308) **[OPEN]** — **BlueBubbles webhook breakage** — `127.0.0.1` → `localhost` normalization breaks IPv4 delivery on macOS. **No fix PR**.
- [#45226](https://github.com/NousResearch/hermes-agent/issues/45226) **[OPEN]** — **Windows Desktop crashes** with GPU process error (`exit_code=-2147483645`). **Fix PR [#45341](https://github.com/NousResearch/hermes-agent/pull/45341) submitted today** (adds `--no-angle` flag).

### Low Severity (P3)
- [#45342](https://github.com/NousResearch/hermes-agent/issues/45342) — **Desktop Language switcher row missing** in Appearance settings (component doesn't render).
- [#45307](https://github.com/NousResearch/hermes-agent/issues/45307) — `_find_skill()` fails to resolve `category/skill` path format — only compares last directory component.
- [#45335](https://github.com/NousResearch/hermes-agent/issues/45335) — `hermes cron edit --profile <name>` returns "Job not found" for all jobs.
- [#45272](https://github.com/NousResearch/hermes-agent/issues/45272) — CLI streaming breaks words mid-character due to terminal soft-wrap.
- [#45328](https://github.com/NousResearch/hermes-agent/issues/45328) — Auxiliary client cache eviction calls `async close` without awaiting — generates warnings in long-running sessions.

## Feature Requests & Roadmap Signals

**Most actionable features from today:**

1. **Unified cross-platform session history** ([#45275](https://github.com/NousResearch/hermes-agent/issues/45275)) — User wants Telegram conversations to appear in Desktop app session list. Very likely to be prioritized as it enhances the multi-platform story.

2. **Desktop Kanban integration** ([#41222](https://github.com/NousResearch/hermes-agent/issues/41222)) — Bring Kanban board into Desktop GUI. With PRs already improving Kanban internals ([#44891](https://github.com/NousResearch/hermes-agent/pull/44891), [#44893](https://github.com/NousResearch/hermes-agent/pull/44893), [#44895](https://github.com/NousResearch/hermes-agent/pull/44895), [#44899](https://github.com/NousResearch/hermes-agent/pull/44899)), the foundational work is underway.

3. **Desktop auto-scroll and sidebar fixes** ([#44140](https://github.com/NousResearch/hermes-agent/issues/44140)) — Three specific UI bugs: no auto-scroll during streaming, sidebar covering scrollbar, custom session groups. Performance fix PR [#45343](https://github.com/NousResearch/hermes-agent/pull/45343) improves streaming lag, suggesting the team is actively polishing Desktop UX.

4. **Human-like memory architecture** ([#44897](https://github.com/NousResearch/hermes-agent/pull/44897)) — Major PR in active development adding working memory, semantic records, and episodic recall. This is a **significant roadmap signal** — Hermes is investing in persistent, structured memory beyond simple context compression.

5. **Signal adapter enhancements** ([#39043](https://github.com/NousResearch/hermes-agent/issues/39043)) — Request for native quote/reply, edit, and remote-delete. Indicates growing Signal user base.

## User Feedback Summary

**Pain points expressed today:**
- **"Long responses get cut off mid-stream"** — #7237 (41 comments) is the loudest single issue; this affects all platforms and all use cases involving long-form generation.
- **"Windows Desktop keeps crashing"** — #45226 reports repeated crashes on Windows with Intel integrated graphics. Fix PR [#45341](https://github.com/NousResearch/hermes-agent/pull/45341) offers a workaround.
- **"My Telegram sessions don't show up in the Desktop app"** — #45275 user wants unified history across platforms.
- **"Slack bot conversations silently fail"** — #30091 bot-to-bot messages dropped despite `allow_bots=all`.
- **"Context compression pollutes the chat"** — #38389/#38391/#38392 (all closed as duplicates): compressed summaries injected as regular messages, creating walls of confusing text.
- **"The Kanban board is hard to reach"** — #41222 user wants it in Desktop GUI instead of separate terminal.

**User satisfaction signals:**
- The PR pipeline is actively addressing multiple P1/P2 bugs reported in the last week.
- Desktop streaming performance fix ([#45343](https://github.com/NousResearch/hermes-agent/pull/45343)) shows 2x FPS improvement and 60% less blocked time.
- WhatsApp debounce reduction ([#44896](https://github.com/NousResearch/hermes-agent/pull/44896)) directly addresses user pain ("5 seconds of dead silence").

## Backlog Watch

**Issues needing maintainer attention (no response, >30 days old):**

| Issue | Age | Severity | Last Activity |
|-------|-----|----------|---------------|
| [#17999](https://github.com/NousResearch/hermes-agent/issues/17999) — Windows `read_file` fails on D: drive | **44 days** | P2 | 2026-06-12 (user bump) |
| [#23473](https://github.com/NousResearch/hermes-agent/issues/23473) — `VIRTUAL_ENV` leaked into subprocesses | **33 days** | P1 | 2026-06-12 (user bump) |
| [#30091](https://github.com/NousResearch/hermes-agent/issues/30091) — Slack bot-to-bot messages dropped | **23 days** | P2 | 2026-06-12 (user bump) |

**Stale PRs needing review:**
- [#16769](https://github.com/NousResearch/hermes-agent/pull/16769) — **Nostr NIP-17 adapter** — Open for **46 days**, no maintainer review. This is a complete feature with architecture, installation instructions, and test coverage. If the project intends to ship multi-platform support, this deserves attention.

**Observation:** The three oldest unaddressed issues are all **Windows-specific** and **subprocess/sandboxing related**. This pattern suggests the team may lack Windows CI/testing infrastructure or is prioritizing Linux/macOS platforms. The new Windows GPU crash fix ([#45341](https://github.com/NousResearch/hermes-agent/pull/45341)) is a positive sign, but the staleness of these platform bugs remains a concern for Windows users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-13

## Today's Overview

PicoClaw shows **very high development velocity** today, with **14 pull requests** updated in the last 24 hours (11 open, 3 merged/closed) and **6 issues** updated (5 open, 1 closed). A new **nightly build (v0.2.9-nightly.20260613.c362114c)** was published, though marked as unstable. The project is undergoing **intensive cross-domain work**: protocol enhancements for WebSocket signaling, Google Gemini 3.5 Flash compatibility fixes, Telegram forum topic handling, and multiple JSON error-safety patches land simultaneously. Five contributors submitted fixes today, and three PRs were cleanly merged — suggesting healthy review throughput. However, one open bug (token consumption with Evolution) has been stale for 8 days, and several PRs remain open for 2–4 weeks.

## Releases

A **single nightly release** was published today:

- **v0.2.9-nightly.20260613.c362114c** — automated build, potentially unstable. Includes all changes merged to `main` since v0.2.9. No manual changelog beyond the auto-generated diff; users should test before deploying in production. **No breaking changes or migration notes** accompany this release.

## Project Progress

**Merged/closed PRs today (3):**

| PR | Author | Summary |
|----|--------|---------|
| [#3113](https://github.com/sipeed/picoclaw/pull/3113) | chengzhichao-xydt | `fix(channels): check json marshal/unmarshal errors in toChannelHashes` — three silent JSON serialization failures in channel config hashing are now explicitly caught |
| [#3112](https://github.com/sipeed/picoclaw/pull/3112) | chengzhichao-xydt | `fix(tools): handle json.Marshal error in toolloop tool call arguments` — prevents data loss when tool arguments contain non-serializable values |
| [#2551](https://github.com/sipeed/picoclaw/pull/2551) | cytown | `refactor: standardize channel identification and decouple name from provider type` — long-running refactor allowing multiple instances of the same provider, merged after 57 days open |

**Key fix merged:** The channel identification refactor ([#2551](https://github.com/sipeed/picoclaw/pull/2551)) is a significant architectural change — it decouples channel config keys from provider type IDs, enabling multiple Telegram/Discord/etc. instances per bot. This unblocks multi-account setups.

## Community Hot Topics

**Most commented/reactive issue:**
- **[#2984](https://github.com/sipeed/picoclaw/issues/2984)** — "Add explicit turn completion signal for Pico WebSocket clients" (2 comments, **2 thumbs up**) — users want deterministic `turn.done` lifecycle signaling. This is the **highest community demand signal** this week. A corresponding fix PR [#3116](https://github.com/sipeed/picoclaw/pull/3116) was opened today by afjcjsbx, directly addressing the three gaps in the initial implementation (missing `request_id` preservation for queued messages, absent lifecycle signal for steering/follow-up messages, missing force-reply propagation). This issue is likely to close within days.

**Second most popular:**
- **[#3109](https://github.com/sipeed/picoclaw/pull/3109)** — "Channel-level permission scoping" (closed/merged today) — generated significant cross-dependency: user v2up-32mb immediately filed **issue [#3114](https://github.com/sipeed/picoclaw/issues/3114)** (in Chinese) requesting Telegram-specific conversation-type permission tiers (private/group/channel), showing the community sees this as an incomplete solution.

**Underlying need:** The community is pushing for **finer-grained security boundaries** — distinguishing *who* can use the bot from *where* they can use it, especially in group/channel contexts where dangerous tools (exec, file I/O) should be restricted.

## Bugs & Stability

**Ranked by severity:**

1. **[#3012](https://github.com/sipeed/picoclaw/issues/3012) [CRITICAL]** — "Continuous consumption of tokens every minute when evolution is enabled" (stale since June 5, 8 days old). **No fix PR exists.** This is a cost-impacting bug affecting production deployments with Evolution mode. Author xpader reports steady token drain on FreeBSD with MiniMax provider. **Needs maintainer attention.**

2. **[#3111](https://github.com/sipeed/picoclaw/issues/3111) [HIGH]** — "Tool execution fails with Gemini 3.5 Flash (Missing thought_signature in schema)" — new bug reported today. The Google API now requires Agentic `thought_signature` in tool schemas, and PicoClaw's response schema doesn't include it, causing 400 Bad Request failures. **No fix PR yet** — this blocks all Gemini 3.5 Flash users.

3. **[#3110](https://github.com/sipeed/picoclaw/issues/3110) [MEDIUM]** — "Telegram adapter ignores message_thread_id in Forum topics" — bot replies to wrong thread in Telegram Forum supergroups. Typing indicator works in correct thread, but final message lands in #General. **No fix PR yet.**

4. **PR [#3115](https://github.com/sipeed/picoclaw/pull/3115) [MEDIUM] (fix pending)** — "Fix inline data URL media extraction for generic tool output" — session-history corruption when `read_file`/`exec` tools return base64-encoded strings in plain text. A fix is already contributed by jp39.

5. **PR [#3091](https://github.com/sipeed/picoclaw/pull/3091) [LOW]** — "fix(openai_compat): add ok check for native_search type assertion" — non-bool `native_search` values silently disable search; fix open but unmerged.

## Feature Requests & Roadmap Signals

**Most actionable feature signals from today:**

- **DeltaChat integration** — PR [#3063](https://github.com/sipeed/picoclaw/pull/3063) (open 5 days) adds a new DeltaChat gateway, expanding PicoClaw's channel reach into the federated messaging world. Moderate complexity, likely to merge within 1–2 weeks.

- **Remote Pico WebSocket agent mode** — PR [#3118](https://github.com/sipeed/picoclaw/pull/3118) by jp39 adds `picoclaw agent --remote ws://...` allowing the CLI agent to connect over WebSocket to a remote PicoClaw instance. This enables headless remote control and CI/CD integration.

- **Shift+Enter hint in Web UI** — PR [#3097](https://github.com/sipeed/picoclaw/pull/3097) adds a visible keyboard shortcut hint — small UX win, likely to merge soon.

- **Image input compression pipeline** — PR [#2964](https://github.com/sipeed/picoclaw/pull/2964) (stale, 16 days open) adds configurable multi-level inbound image compression. Still open with no comments — may need a rebase.

- **NEAR AI Cloud provider** — PR [#2917](https://github.com/sipeed/picoclaw/pull/2917) (open 23 days) adds NEAR AI Cloud as an OpenAI-compatible provider with TEE-capable models. Long-open but no maintainer feedback.

**Prediction for v0.3.0:** The `turn.done` lifecycle ([#2984](https://github.com/sipeed/picoclaw/issues/2984) / [#3116](https://github.com/sipeed/picoclaw/pull/3116)) and the remote agent mode ([#3118](https://github.com/sipeed/picoclaw/pull/3118)) are strong candidates for inclusion. The Gemini 3.5 Flash fix ([#3111](https://github.com/sipeed/picoclaw/issues/3111)) is likely to be prioritized as a blocker for a major model provider.

## User Feedback Summary

**Pain points expressed today:**

- **"Token drain bug has been open for 8 days"** — user xpader on [#3012](https://github.com/sipeed/picoclaw/issues/3012). No maintainer acknowledgment, causing frustration for production Evolution users.

- **"Gemini 3.5 Flash is completely broken"** — user Giordano10 on [#3111](https://github.com/sipeed/picoclaw/issues/3111). Unable to use the latest Google model; affects multi-provider deployments.

- **"Telegram Forum replies silently go to wrong thread"** — same user on [#3110](https://github.com/sipeed/picoclaw/issues/3110). The bug is reproducible but hasn't received a fix yet.

- **"Cannot restrict dangerous tools in Telegram groups"** — user v2up-32mb on [#3114](https://github.com/sipeed/picoclaw/issues/3114) (in Chinese). The channel permission scoping fix from [#3109](https://github.com/sipeed/picoclaw/pull/3109) was merged, but the user immediately identified it doesn't address Telegram's conversation-type security model. This suggests the implementation lacks conversation-type granularity.

**Satisfaction signals:** jp39 and afjcjsbx are actively contributing multiple fixes (media routing, WebSocket lifecycle, data URL corruption) — indicating engaged, technically capable users who trust the project enough to submit PRs.

## Backlog Watch

**Items needing maintainer attention:**

1. **[#3012](https://github.com/sipeed/picoclaw/issues/3012) [CRITICAL, 8 days stale]** — Evolution token drain bug. No PRs, no maintainer comment. **Highest priority** — this is a production-affecting cost bug.

2. **[#2964](https://github.com/sipeed/picoclaw/pull/2964) [16 days stale]** — Image compression PR. No maintainer review at all. May need rebase.

3. **[#2917](https://github.com/sipeed/picoclaw/pull/2917) [23 days stale]** — NEAR AI Cloud provider. No maintainer feedback. Could be deprioritized but deserves a status comment.

4. **[#3045](https://github.com/sipeed/picoclaw/pull/3045) [6 days open]** — Matrix user ID `allow_from` fix. Single reviewer needed; addresses a clear bug ([#3044](https://github.com/sipeed/picoclaw/issues/3044)).

5. **[#3053](https://github.com/sipeed/picoclaw/pull/3053) [5 days open]** — Evolution lockStoreFile panic fix. Clean fix; awaiting merge.

**Overall project health:** Green with amber warnings. The project is highly active with strong contributor diversity (6+ unique authors this week), but the **stale critical bug** and **lack of maintainer responses on several long-open PRs** suggest maintainers may be bandwidth-constrained. The Gemini 3.5 Flash regression is a new blocker that should be addressed within days to prevent user migration.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the project digest for **NanoClaw** for **2026-06-13**.

---

## NanoClaw Project Digest: 2026-06-13

### 1. Today's Overview
The project is in a heavy development sprint with significant activity across security, stability, and feature seams, though no new releases were cut today. **9 open Pull Requests** were updated in the last 24 hours, indicating a high volume of pending contributions, while **5 Issues** saw activity, with 4 remaining open. The maintainer team appears responsive, with several PRs addressing recently filed bugs (e.g., Issue #2668 and #2516). The project's health is robust but carries a growing risk of technical debt if the current PR backlog is not merged or trimmed soon.

### 2. Releases
**None.** No new releases or tags were recorded during the reporting period. The latest public version implied by code references is approximately v2.0.64.

### 3. Project Progress
No Pull Requests were merged or closed today, meaning no new features or fixes landed in the `main` branch. However, several critical functional areas advanced via new PR submissions:
- **Memory Scaffold (PR #2745):** A new opt-in persistent memory scaffold for providers is proposed, allowing agents to maintain state across sessions.
- **Agent-Surfaces (PR #2746):** A capability seam for providers was submitted, allowing them to declare features (e.g., memory, UI surfaces) to the host.
- **OneCLI SDK Bump (PR #2747):** Updates the OneCLI SDK to v2.2.1, introducing credential-stub mounts and machine-checkable pins for cloud identity.
- **Poisoned-Resume Fix (PR #2670):** A self-heal mechanism for agent runner crash loops caused by corrupt transcripts was updated.

### 4. Community Hot Topics
- **#2506: Silent Response Drops on Fast Turns** ([Link](https://github.com/nanocoai/nanoclaw/issues/2506)) — *3 Comments*. The community is deeply concerned about a bug where agent responses are silently dropped if two turns complete within 60 seconds of each other or if a follow-up message arrives during a streaming query. Users report client timeouts and no error feedback. This is the most discussed open bug today.
- **#2711: Ungated `create_agent` MCP Tool** ([Link](https://github.com/nanocoai/nanoclaw/issues/2711)) — *1 Comment*. A user flagged a security loophole where the `create_agent` tool, documented as admin-only, is accessible to any container. The underlying need is for robust role-based access control (RBAC) in MCP tool exposure, a critical governance feature for multi-tenant deployments.
- **#2632: Telegram Swarm Migration Ambiguity** ([Link](https://github.com/nanocoai/nanoclaw/issues/2632)) — *1 Comment*. A user is blocked on migrating a fork that used the old Telegram swarm feature, as the current documentation does not clarify whether the feature exists in v2 or how to re-implement it.

### 5. Bugs & Stability
- **High Severity (New):** **#2751** (*Closed*) — Budget-exhausted LLM turns are silently dropped. The user gets no reply. This was quickly closed, likely via a fix or documentation update, but the pattern is dangerous for production users.
- **High Severity:** **#2506** — Silent drops on fast turns (see Hot Topics). No fix PR exists yet; this is a high-impact data-loss bug.
- **Medium Severity:** **#2668** — No per-tool timeout for MCP tools. A hung MCP tool blocks the session for up to 30 minutes. A fix PR (**#2670**) exists and is actively being reviewed, aiming to self-heal the session.
- **Medium Severity:** **#2711** — Ungated `create_agent` MCP tool. No fix PR exists yet, but the security implications are clear.
- **Stability Fix Submitted:** **#2750** — Addresses stale `outbound.db` journals after container kills and hot-journal poll races (fixes #2516 and #2640). This targets a hard-to-reproduce data corruption issue.

### 6. Feature Requests & Roadmap Signals
- **Persistent Agent Memory (PR #2745):** This is the strongest road-signal today. The "opt-in persistent memory scaffold" suggests the core team is building infrastructure for long-term agent memory, likely landing in the next minor version (v2.1).
- **Agent Capacity Seam (PR #2746):** The "agent-surfaces" capability seam indicates a push toward modular provider feature discovery. This could unlock custom UI surfaces or specialized toolkits per provider.
- **Security Hardening (PR #2748 & #2749):** Two security-focused PRs (agent container drop-capabilities and npm package age gating) signal that the maintainers are prioritizing supply chain security and container isolation, likely in response to the growing number of enterprise/users.
- **Telegram Swarm (Issue #2632):** User demand for the old `add-telegram-swarm` feature is high. If not already planned, this will likely become a feature request for a new "multi-agent identity" skill.

### 7. User Feedback Summary
- **Pain Points:** The most vocal user pain points involve **silent failures** (#2506, #2751) and **blocking sessions** (#2668). Users are frustrated by the lack of error feedback (timeouts vs. dropped messages). Another clear pain point is **security ambiguity** (#2711, #2632) regarding access controls and feature migration paths.
- **Satisfaction:** Users submitting PRs (e.g., sturdy4days, boazdori) indicate a healthy contributor community that is engaged and able to self-heal issues. The quick closure of #2751 shows maintainer responsiveness to critical issues.
- **Use Cases:** The active issues reveal two dominant use cases: **production cloud deployments** (budget caps, session timeouts) and **multi-tenant/team forks** (RBAC, swarm migration).

### 8. Backlog Watch
- **Issue #2632** ([Link](https://github.com/nanocoai/nanoclaw/issues/2632)) — *Telegram Swarm Migration*: Open since May 28 with zero maintainer response. A user is explicitly blocked on migration; this needs a roadmap answer or a documentation link.
- **Issue #2506** ([Link](https://github.com/nanocoai/nanoclaw/issues/2506)) — *Silent Drops on Fast Turns*: Updated yesterday but no fix PR exists. This is the highest-severity open bug without an assignee.
- **Issue #2711** ([Link](https://github.com/nanocoai/nanoclaw/issues/2711)) — *Ungated MCP Tool*: The reporter explicitly called out a security vulnerability. If no PR or comment is made soon, this could be considered a security report needing disclosure.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-13

## 1. Today's Overview
Project activity remains moderate with 3 pull requests and 1 issue updated in the last 24 hours. No new releases were published. The development cadence shows focused maintenance work, particularly around Discord gateway reliability and configuration improvements, all from contributor *vernonstinebaker*. A single open bug regarding incomplete Ollama model responses represents the most pressing user-facing issue. Overall, project health appears stable with ongoing community contributions, though the lack of merged PRs today suggests review/merge cycles may be slower than development activity.

## 2. Releases
No new releases were published in the last 24 hours. The latest release remains unknown.

## 3. Project Progress
No PRs were merged or closed today. All 3 open PRs remain under review:

- **#949** — *fix: make queue_mode configurable from config.json* — Adds a `agent.default_queue_mode` field to configuration, refactors the `QueueMode` enum to `config_types.zig`, and parses it from `config.json` with appropriate fallback.
- **#951** — *fix(agent_runner): suppress stderr initialization logs on agent failure* — Prevents initialization logs (memory plan, MCP server registration, channel startup) from being posted as agent responses when the agent child process exits non-zero.
- **#953** — *fix(discord): recover closed gateway sockets* — Closes active Discord gateway sockets before joining heartbeat threads during reconnect cleanup, adds bounded grace window for stalled pre-HELLO reconnects, and includes regression coverage.

## 4. Community Hot Topics
The most active item is **Issue #952**, which has attracted user attention despite having 0 comments and 0 reactions—its recent creation and clear reproduction steps make it a likely focus for discussion.

**Top Issue:**
- **#952** [OPEN] *[bug] Local model using ollama returns incomplete answers* — [Link](https://github.com/nullclaw/nullclaw/issues/952)
  - Reported by **bloodgroup-cplusplus** (created 2026-06-11, updated 2026-06-12)
  - **Underlying need:** Users running local models (e.g., Gemma via Ollama) need reliable, complete sentence-level responses from the agent. The screenshot suggests the agent is truncating output mid-sentence, indicating a potential buffering, timeout, or stream termination issue specific to local model orchestration.

**Top PRs:**
- **#953** [OPEN] *fix(discord): recover closed gateway sockets* — [Link](https://github.com/nullclaw/nullclaw/pull/953)
  - Most recently updated (2026-06-12)
  - **Underlying need:** Discord users experiencing gateway disconnections during extended sessions need automatic recovery without manual intervention. The fix targets a specific race condition in socket cleanup.

## 5. Bugs & Stability
One bug reported today:

**Severity: High** — **Issue #952** — *Local model using ollama returns incomplete answers*
- Reported by **bloodgroup-cplusplus**
- Agent fails to produce complete sentences when using Gemma via Ollama
- Screenshot evidence shows truncated output
- **No fix PR exists yet**; likely requires investigation into Ollama integration layer (stream handling, completion detection, or response buffering)

No crashes, regressions, or stability issues were reported beyond this single bug.

## 6. Feature Requests & Roadmap Signals
While no explicit feature requests were filed today, the open PRs signal near-term roadmap direction:

- **Configurable queue mode (#949):** Likely to land shortly, enabling users to set default queue behavior (`latest`, `parallel`, `fifo`) via `config.json` without per-session setup.
- **Discord gateway resilience (#953):** Indicates ongoing investment in Discord integration robustness, possibly in response to user reports of disconnections during long-running sessions.

**Prediction for next version:** Expect `default_queue_mode` configuration and Discord gateway recovery improvements to be included.

## 7. User Feedback Summary
- **Pain point:** Local model users on Ollama are encountering truncated responses (Issue #952), disrupting basic usability for those preferring local inference over cloud APIs.
- **Use case highlighted:** Running Gemma locally via Ollama for privacy/offline use cases—a growing segment as open-weight models mature.
- **Satisfaction indicators:** The three open PRs from *vernonstinebaker* (all configuration/fixes) suggest engaged contributor satisfaction, though no explicit positive feedback was recorded in the last 24 hours.

## 8. Backlog Watch
No long-unanswered issues or PRs were identified in this 24-hour window. The most recent open items are less than 3 days old:

- **Issue #952** (created 2026-06-11) — needs maintainer reproduction and triage
- **PRs #949, #951, #953** (created 2026-06-10 to 2026-06-12) — awaiting maintainer review and merge

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for 2026-06-13.

---

## IronClaw Project Digest — 2026-06-13

### 1. Today's Overview
Project activity is **very high**, with 50 issues and 50 PRs updated in the last 24 hours, driven largely by a post-merge review cycle for the **DeferredBusy drain** system and ongoing work on **attachment support** and **channel state**. The maintainer team (henrypark133, serrrfirat, ilblackdragon, zmanian) is dominant, closing 17 PRs and resolving 20 issues. A notable shift occurred today: a new PR (#4838) replaces the complex deferred-drain mechanism with a simpler user-facing retry model, indicating rapid iteration based on internal architecture reviews. The only significant drag on velocity is a **global CI failure** caused by new RUSTSEC advisories blocking all builds.

### 2. Releases
- **No new releases** were published today. The last release candidate (PR #3708, `ironclaw_common` v0.5.0, `ironclaw_skills` v0.4.0) remains open.

### 3. Project Progress
The following major features and fixes were merged or closed today:

- **DeferredBusy Drain (Replaced):** PR #4812 ([link](https://github.com/nearai/ironclaw/pull/4812)) was closed. While it previously completed the "blocked-thread UX" arc, a subsequent PR (#4838) now supersedes it with a simpler "reject and notify" contract for busy threads.
- **Persistent Approvals:** PR #4835 ([link](https://github.com/nearai/ironclaw/pull/4835)) is open, implementing a fix for issue #4825 to persist "always allow" approvals across threads by dropping `thread_id` from the approval scope.
- **Security & Hooks (Closed):** Three hooks PRs were closed, adding audit events for MCP lease denials (#4561 closed, [link](https://github.com/nearai/ironclaw/pull/4561)), auth continuation failures (#4562 closed, [link](https://github.com/nearai/ironclaw/pull/4562)), and fan-out caps for BeforeCapability hooks (#4568 closed, [link](https://github.com/nearai/ironclaw/pull/4568)).
- **Performance & CI:** PR #4829 ([link](https://github.com/nearai/ironclaw/pull/4829)) opened to split long CI jobs into smaller shards and retire a dormant workflow.
- **Test Infrastructure:** PR #4773 ([link](https://github.com/nearai/ironclaw/pull/4773)) was closed, adding record/replay machinery for QA testing of the Reborn runtime.

### 4. Community Hot Topics
- **#4817 ([OPEN] DeferredBusy drain follow-ups:** [Link](https://github.com/nearai/ironclaw/issues/4817)) - 3 comments. This issue tracks the three deferred design decisions (trusted resubmit seam, stale-intent policy, startup sweep) from the now-superseded drain PR.
- **#4825 ([OPEN] Persistent approval scope:** [Link](https://github.com/nearai/ironclaw/issues/4825)) - 3 comments. This is a high-value UX issue: users who grant "always allow" for a capability in one Reborn thread are re-prompted in every new thread. A fix is already in flight (#4835).
- **#4703 ([CLOSED] Model picker saves display name:** [Link](https://github.com/nearai/ironclaw/issues/4703)) - 3 comments. A configuration bug where the UI saved the model's display name instead of its ID, causing downstream failures.

**Analysis:** The most active discussions center on the **Reborn thread/approval UX**. Users are hitting friction with inconsistent state persistence (approvals, slack connections, conversation pinning), and the project team is rapidly iterating to resolve the architectural seams.

### 5. Bugs & Stability
Several user-facing bugs in the Reborn WebUI were reported and closed. A **critical** infrastructure issue is blocking CI.

- **CRITICAL - RUSTSEC Advisories:** Issue #4824 ([link](https://github.com/nearai/ironclaw/issues/4824)) reports that `cargo-deny` fails on `main` due to three new RUSTSEC advisories against postgres crates. This blocks all PRs and the main branch.
- **HIGH - SSO Setup Failure:** Issue #4705 (closed, [link](https://github.com/nearai/ironclaw/issues/4705)). GitHub and Google SSO fail in the local Reborn environment with `Invalid frontend_callback`.
- **MEDIUM - Conversation Flickering:** Issue #4719 (closed, [link](https://github.com/nearai/ironclaw/issues/4719)). Navigating back to a conversation triggers a visible flicker/reload.
- **MEDIUM - Inconsistent Active Provider:** Issue #4697 ([link](https://github.com/nearai/ironclaw/issues/4697)). The Inference settings page shows one provider as active (e.g., Ollama) while chat requests use a different one (e.g., `llama3`).
- **LOW - Light Theme Contrast:** Issue #4819 ([link](https://github.com/nearai/ironclaw/issues/4819)). The attachment warning banner has unreadable text in the Light theme.

### 6. Feature Requests & Roadmap Signals
- **Reborn Attachment Support (Predicting Next Release):** A massive six-PR stack (#4654, #4655, #4668, #4670, #4738) is aiming to deliver full attachment upload and display support for the Reborn WebChat v2 SPA. PR #4738 ([link](https://github.com/nearai/ironclaw/pull/4738)) specifically wires the frontend upload UX. This is the single largest feature push and is highly likely to land in the next version.
- **Channel & Delivery State Awareness:** PR #4836 ([link](https://github.com/nearai/ironclaw/pull/4836)) solves issue #4828 and gives the model runtime context about which channels (e.g., Slack) are connected, where delivery goes, and how a run started. This fixes a common tester failure point where the model was blind to its own connectivity.
- **LLM Time Awareness:** Issue #4796 ([link](https://github.com/nearai/ironclaw/issues/4796)) requests that the LLM be made aware of the current date/time without requiring an explicit tool call. This is a UX polish request for scheduling and calendar workflows.

### 7. User Feedback Summary
User-reported pain points from the last 24 hours are heavily concentrated on the **Reborn WebUI v2** and indicate a product in active development with rough edges:

- **Persistence Failures:** Users are frustrated that "always allow" approvals do not persist across threads (#4825), and that unsent drafts are lost when leaving a new conversation (#4724, closed).
- **Confusing State:** The UI is inconsistent regarding which provider is active (#4697) and what a "pinned" conversation means (#4721, closed). One tester was stuck in a Slack reconnect loop (#4777).
- **Blocked Workflows:** Authorization flows fail to recover gracefully from cancelled sign-ins (#4706, closed), and failed tool workflows cause the conversation ordering to become inconsistent (#4762).
- **Positive Signal:** The rapid triage of these UI bugs (17 UX issues closed today) shows a clear commitment to polish.

### 8. Backlog Watch
- **Issue #4824 - cargo-deny failing:** [Link](https://github.com/nearai/ironclaw/issues/4824). This is the single highest-impact open issue as it is blocking all CI and PR merges. It was opened yesterday and has no comments from maintainers yet, suggesting the fix may be awaiting a dependency update.
- **PR #3708 - Release candidate:** [Link](https://github.com/nearai/ironclaw/pull/3708). This release PR has been open for nearly a month. With the attachment stack closing in on merge, it is likely being held to ship a bigger release including those features.
- **Issue #4697 - Inconsistent Active Provider:** [Link](https://github.com/nearai/ironclaw/issues/4697). This is an older UI bug (3 days) regarding provider state that has received no assignee or triage comment, despite being a confusing user experience.
- **Issue #4561 - MCP Lease Denial Audit:** [Link](https://github.com/nearai/ironclaw/pull/4561). While the PR is closed, the parent issue #3959 remains open, indicating the full security audit story is unfinished.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-13

## Today's Overview

LobsterAI is in a high-activity phase today, with **17 pull requests updated** in the last 24 hours, of which **11 were merged or closed**, signaling a strong development cadence. One issue was closed, and no new issues were opened, indicating a net reduction in open concerns. The project appears to be consolidating recent feature work (including Computer Use MVP and realtime ASR) into a stable release while continuing to address technical debt and bug fixes from previous months. Overall, project health is solid with active maintainer engagement.

---

## Releases

**No new releases today.** The most recent release was `2026.6.11`, which was merged into `main` via PR #2158 for the upcoming `2026.6.12` release. Highlights from that pending release include:
- **Computer Use MVP** with a built-in kit
- **Realtime ASR voice input** for cowork prompts
- **HTML artifact public sharing** mode selection
- **Image and SVG artifact sharing** support

---

## Project Progress

### Merged/Closed PRs Today (11 items)

| PR | Area | Type | Summary |
|----|------|------|---------|
| [#2158](https://github.com/netease-youdao/LobsterAI/pull/2158) | renderer, docs, main, openclaw, skills, cowork, artifacts | chore(release) | Merge `release/2026.6.11` into `main` for v2026.6.12 |
| [#2156](https://github.com/netease-youdao/LobsterAI/pull/2156) | main, openclaw | fix(computer-use) | Bump Computer Use runtime to 1.0.7 with UIA breadcrumbs |
| [#2157](https://github.com/netease-youdao/LobsterAI/pull/2157) | main | fix(media) | Fix image extension detection during save (PNG→.jpg issue) |
| [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155) | renderer, docs, cowork | fix(voice-input) | Prevent duplicate realtime ASR start requests |
| [#2154](https://github.com/netease-youdao/LobsterAI/pull/2154) | renderer, main | fix(cowork) | Show model metadata after stopped streams |
| [#2153](https://github.com/netease-youdao/LobsterAI/pull/2153) | renderer, main, openclaw, cowork | fix(cowork) | Preserve same-name package model selection |
| [#1473](https://github.com/netease-youdao/LobsterAI/pull/1473) | — | fix | Agent creation modal: add unsaved changes confirmation |
| [#1474](https://github.com/netease-youdao/LobsterAI/pull/1474) | — | fix | Agent settings panel: add unsaved changes confirmation |
| [#1475](https://github.com/netease-youdao/LobsterAI/pull/1475) | — | fix | MCP server config modal: add unsaved changes confirmation |
| [#1476](https://github.com/netease-youdao/LobsterAI/pull/1476) | — | fix | Cowork input: persist draft on session/navigation switch |
| [#1477](https://github.com/netease-youdao/LobsterAI/pull/1477) | — | fix | Re-edit history messages: add overwrite confirmation dialog |

**Key advances today:**
- **Computer Use runtime** was updated to v1.0.7 with diagnostic improvements (UIA breadcrumbs for crash investigation)
- **Media pipeline**: Fixed a bug where generated images in PNG format were incorrectly saved with `.jpg/.jpeg/.webp` extensions
- **Voice input stability**: Duplicate realtime ASR start requests are now prevented
- **UX consistency**: Six older PRs (from April) were finally merged, adding unsaved-changes confirmation dialogs to multiple modals and preventing content loss during session switches

### Open PRs (6 items — all stale)

The following PRs remain open for over 2 months and have not been merged:

| PR | Issue | Summary |
|----|-------|---------|
| [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446) | #1400 | Fix gateway infinite restart loop (race condition) |
| [#1448](https://github.com/netease-youdao/LobsterAI/pull/1448) | — | Agent settings i18n: "delete" and "No matching skills" in English |
| [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449) | — | Fold/group timed task execution records in sidebar |
| [#1453](https://github.com/netease-youdao/LobsterAI/pull/1453) | #1439 | Disabled skills still injected into conversation prompts |
| [#1454](https://github.com/netease-youdao/LobsterAI/pull/1454) | #1437 | Silent failure: create task button unresponsive with empty date |
| [#1456](https://github.com/netease-youdao/LobsterAI/pull/1456) | — | Shortcut key conflict detection missing |

---

## Community Hot Topics

**Most active issue:**
- [#1](https://github.com/netease-youdao/LobsterAI/issues/1) — **API Error with OpenAI API Type** (CLOSED, 7 comments)
  - User on Mac OS 13.7.8 configured MiniMaxi API key (test passed) but when switching to OpenAI message type, receives `400 {"type":"error","error":{"type":"api_error","message":"invalid params, inv..."`
  - This was the **only issue tracked** today and has been closed, suggesting the maintainers resolved or addressed it.

**No new community issues or feature requests** were opened in the last 24 hours, indicating either a satisfied user base or a lull in external engagement. No reactions (👍) were recorded on any items.

---

## Bugs & Stability

### Severity: Medium

| Bug | PR/Issue | Status | Description |
|-----|----------|--------|-------------|
| Image file extension mismatch | [#2157](https://github.com/netease-youdao/LobsterAI/pull/2157) | Merged fix | PNG content saved as `.jpg/.jpeg/.webp` due to trusting server-provided extension |
| Duplicate ASR start requests | [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155) | Merged fix | Real-time voice input could be started multiple times simultaneously |
| Stream metadata missing after stop | [#2154](https://github.com/netease-youdao/LobsterAI/pull/2154) | Merged fix | Model metadata not preserved when user manually stops a streaming response |
| Model selection lost for same-name packages | [#2153](https://github.com/netease-youdao/LobsterAI/pull/2153) | Merged fix | Models with identical names from different packages were not properly distinguished |

**No new crashes or regressions reported today.** The above bugs were all found and fixed internally during the release cycle.

---

## Feature Requests & Roadmap Signals

**No new feature requests were opened today.** However, based on the merged `release/2026.6.11` branch (PR #2158), the following features are expected in the next release:

- **Computer Use MVP** — likely a foundational capability for AI-operated desktop actions
- **Realtime ASR voice input** for cowork prompts — enhances voice UX
- **HTML artifact public sharing** with mode selection — improves collaboration
- **Image/SVG artifact sharing** — expands artifact support

Additionally, the **6 stale open PRs** (#1446–#1456) represent significant feature requests and improvements that are pending review/merge:
- Scheduled task grouping in sidebar
- Shortcut conflict detection
- Disabled skills cleanup from active prompts
- I18n gaps in Agent settings

---

## User Feedback Summary

| Pain Point | Evidence | Satisfaction Signal |
|------------|----------|---------------------|
| **File extension confusion** when saving generated images | PR #2157 | ✅ Fix merged |
| **Voice input race condition** — duplicate starts | PR #2155 | ✅ Fix merged |
| **Stream interruption data loss** — model metadata gone | PR #2154 | ✅ Fix merged |
| **Model selection confusion** with same-named models | PR #2153 | ✅ Fix merged |
| **API compatibility issues** with OpenAI-type endpoints | Issue #1 (closed) | ✅ Resolved |
| **Unsaved content loss** in modals (Agent creation, settings, MCP, draft, re-edit) | PRs #1473–#1477 (all merged) | ✅ Long-standing UX gap closed |

**Overall sentiment**: The project appears to be in a **stabilization and polish phase**, with multiple UX quality-of-life fixes landing. No major user complaints surfaced today.

---

## Backlog Watch

The following **high-importance PRs** have been open for over 2 months without maintainer action:

| PR | Area | Since | Risk |
|----|------|-------|------|
| [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446) — **Gateway infinite restart loop** | openclaw | Apr 3, 2026 (71 days) | **Critical**: Could cause app unavailability for users with unstable gateways |
| [#1453](https://github.com/netease-youdao/LobsterAI/pull/1453) — **Disabled skills still injected** | skills | Apr 3, 2026 (71 days) | **High**: Users believe a skill is disabled but it still affects conversation |
| [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449) — **Sidebar clutter from scheduled tasks** | cowork | Apr 3, 2026 (71 days) | **Medium**: Degrades UX for users with many automated tasks |
| [#1454](https://github.com/netease-youdao/LobsterAI/pull/1454) — **Create task button silent failure** | scheduled-tasks | Apr 3, 2026 (71 days) | **High**: User action has no feedback |
| [#1448](https://github.com/netease-youdao/LobsterAI/pull/1448) — **i18n gaps in Agent settings** | i18n | Apr 3, 2026 (71 days) | **Medium**: Non-English users see English text |
| [#1456](https://github.com/netease-youdao/LobsterAI/pull/1456) — **Shortcut conflict detection missing** | shortcuts | Apr 3, 2026 (71 days) | **Medium**: Silent binding conflicts break user expectations |

**Recommendation**: These PRs have all received the `stale` label. The project maintainers should prioritize reviewing them, as they represent the **largest open backlog of known issues**. The gateway restart loop (PR #1446) is particularly concerning given its potential to cause complete application failure.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-13

## Today's Overview
The Moltis project shows light to moderate activity over the past 24 hours, with three open issues updated and no pull requests or new releases. No work has been merged or closed in this window, indicating a period of review and discussion rather active development. The project remains healthy but is currently in a slower cycle, likely focused on triaging incoming feedback. No releases occurred; the latest version remains unreleased or unchanged. The issue tracker reflects meaningful discussions around infrastructure (Kubernetes sandboxing), integrations (Fastmail authentication), and local speech-to-text capabilities.

## Releases
**None.** No new releases were published in the last 24 hours. The project may still be in a pre-release or inter-release phase for upcoming features.

## Project Progress
**No pull requests were merged or closed in the last 24 hours.** No PRs were updated. This suggests no code changes were integrated today; the project is currently in a discussion and issue-grooming phase.

## Community Hot Topics
Three issues received updates in the last 24 hours, each with at least one comment:

- **#1115 — [Bug]: Fastmail MCP Authorisation**  
  *Author: kmath313 | Updated: 2026-06-12 | Comments: 2*  
  [View Issue](https://github.com/moltis-org/moltis/issues/1115)  
  This bug report involves authorization flow issues with Fastmail's MCP integration, still under investigation. Two comments suggest some discussion around reproduction or root cause. No fix PR is linked yet.

- **#1118 — [Feature]: Add Kubernetes-native sandbox backend with runtimeClassName support**  
  *Author: AzgadAGZ | Updated: 2026-06-12 | Comments: 1*  
  [View Issue](https://github.com/moltis-org/moltis/issues/1118)  
  A substantial feature request proposing a new sandbox backend using ephemeral Kubernetes pods with VM-level isolation via Kata Containers or gVisor. The request highlights security concerns for executing LLM-generated code and commands. This topic is likely to attract further discussion given the security implications.

- **#1102 — [Feature]: Add FunASR/SenseVoice as local STT engine**  
  *Author: LauraGPT | Updated: 2026-06-12 | Comments: 1*  
  [View Issue](https://github.com/moltis-org/moltis/issues/1102)  
  Suggests integrating FunASR or SenseVoice for ultra-fast, streaming local speech-to-text (70ms for 10s audio). The longevity of this issue (created June 4) and its recent update indicate maintainers are still evaluating or seeking additional input.

**Underlying needs:** The community is pushing for (1) stronger isolation/security for agent command execution, (2) better integration reliability with third-party services like Fastmail, and (3) full on-device voice capabilities without cloud dependency.

## Bugs & Stability
Only one bug-related issue was active in the last 24 hours:

- **#1115 — [Bug]: Fastmail MCP Authorisation** — **Medium severity**  
  This is a user-facing authentication failure. It blocks integration with the Fastmail service. No fix PR exists yet, and the bug is still open with no assigned label or milestone. Given its single integration scope, severity is moderate and not systemic.

No crashes, regressions, or zero-day severity bugs were reported today.

## Feature Requests & Roadmap Signals
Two feature requests stood out:

1. **#1118 — Kubernetes-native sandbox backend**  
   This is a significant architectural proposal. If implemented, it would allow Moltis to run untrusted LLM-generated code in ephemeral pods with VM-level isolation (e.g., Kata Containers, gVisor). This aligns with broader trends in secure AI agent sandboxing. **Prediction:** Likely to be considered for the next major version, possibly as an experimental backend.

2. **#1102 — Local STT with FunASR/SenseVoice**  
   A performance-focused request for local, streaming speech recognition. Given the age (June 4) and recent maintainer attention, a response or experimental integration may appear in the next release cycle.

**Other signals:** No roadmap documents were updated. Both features require non-trivial engineering effort; scope suggests they are mid-to-long-term candidates.

## User Feedback Summary
- **Pain points:** Fastmail MCP authorization failure (#1115) is concretely blocking one user's workflow. No workaround is documented yet.  
- **Use cases:** The Kubernetes sandbox request (#1118) directly addresses a production security concern — users want to run LLM-generated code safely, likely for automation or DevOps use.  
- **Satisfaction / Dissatisfaction:** No overt dissatisfaction expressed. Feature requests are constructive and detailed. The project appears responsive (issues are updated, comments are acknowledged), which suggests decent maintainer engagement.

## Backlog Watch
- **#1102 — Feature: Add FunASR/SenseVoice as local STT engine** (Created June 4, last updated June 12)  
  This issue has been open for 9 days with only one comment and no maintainer label or milestone assignment. If the project intends to pursue local STT, clearer triage or a status update would be helpful.  
  [View Issue](https://github.com/moltis-org/moltis/issues/1102)

- **#1115 — [Bug]: Fastmail MCP Authorisation**  
  This bug is newly reported and should be monitored. Without a fix PR or assignment, it risks lingering if not triaged soon.  
  [View Issue](https://github.com/moltis-org/moltis/issues/1115)

- **#1118 — Kubernetes-native sandbox backend**  
  Not a backlog issue per se, but it represents a high-effort feature. If it receives no maintainer response within the next week, it may become a backlog item.

No issues older than 30 days are currently stalled without updates.

---

*Generated from GitHub data on 2026-06-13. Project health: stable, low activity, actively triaging feedback.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest – 2026-06-13

## Today's Overview
CoPaw (QwenPaw) shows **high activity** over the past 24 hours, with 23 issues and 25 PRs updated. The community is actively reporting bugs and requesting features, while the core team is pushing multiple fixes and a beta release preparation. No new releases were published today, but version bump PRs to `1.1.12b1` indicate an imminent beta. Mixed signals on stability: several regressions between `v1.1.10` and `1.1.11.post2` are being reported and investigated. Overall, the project is in a **maintenance-heavy cycle** with a notable focus on desktop client, memory system, and channel integration issues.

## Releases
**No new releases today.** The latest published version remains **v1.1.11.post2** (as referenced in several bug reports). Two version-bump PRs were closed today:
- [#5157 [CLOSED] chore(release): bump version to 1.1.12.beta1](https://github.com/agentscope-ai/QwenPaw/pull/5157)
- [#5159 [CLOSED] fix(release): switch version to 1.1.12b1](https://github.com/agentscope-ai/QwenPaw/pull/5159)

These suggest **1.1.12beta1** is being prepared for release. No breaking change or migration notes are documented yet for the upcoming version.

## Project Progress
11 PRs were **merged/closed** in the last 24 hours, representing meaningful progress:

**Bug Fixes:**
- [#5144 [CLOSED] fix(console): force render Collapse panels to prevent memory config loss](https://github.com/agentscope-ai/QwenPaw/pull/5144) — Fixes a UI bug where collapsed memory/vector config panels would lose user settings on save (fixes [#5137](https://github.com/agentscope-ai/QwenPaw/issue/5137))
- [#5147 [CLOSED] fix(console): fixed session redirection when switching code mode](https://github.com/agentscope-ai/QwenPaw/pull/5147) — Fixes Coding Mode session loss on page refresh
- [#5154 [CLOSED] refactor(console): Refactor the result style of the memory search tool](https://github.com/agentscope-ai/QwenPaw/pull/5154) — Fixes empty/corrupt memory search results in UI (fixes [#5098](https://github.com/agentscope-ai/QwenPaw/issue/5098))
- [#4144 [CLOSED] fix(cli): use loopback for desktop wildcard readiness checks](https://github.com/agentscope-ai/QwenPaw/pull/4144) — Fixes desktop startup when binding to `0.0.0.0`

**CI & Infrastructure:**
- [#5121 [CLOSED] feat(ci): add release verification gate between build and publish](https://github.com/agentscope-ai/QwenPaw/pull/5121) — Adds end-to-end verification before publishing to PyPI/DockerHub
- [#5022 [CLOSED] [codex] Guard agent workspace restore targets](https://github.com/agentscope-ai/QwenPaw/pull/5022) — Security hardening for agent workspace path validation

**Features:**
- [#5078 [CLOSED] [Breaking Change, Under Review] feat(runtime): Runtime 2.0 modular architecture with enhanced tool-call coordination](https://github.com/agentscope-ai/QwenPaw/pull/5078) — Major architecture change, merging monolithic Runner into composable Runtime 2.0

## Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#5064 [Bug] Agent-created scheduled tasks not triggering](https://github.com/agentscope-ai/QwenPaw/issue/5064) | 11 | 0 | Scheduled tasks created by agents execute without error but never fire at the set time |
| [#4727 [Breaking Change] Migrate backend from AgentScope 1.x → 2.0](https://github.com/agentscope-ai/QwenPaw/issue/4727) | 10 | 👍2 | Major architectural migration plan — users eagerly asking for timeline |
| [#5140 [CLOSED] Attachment download broken for docx/pdf (404)](https://github.com/agentscope-ai/QwenPaw/issue/5140) | 6 | 0 | Regression: non-text file downloads return 404 in v1.1.11.post2 |

**Underlying Need Analysis:** The community is deeply concerned with reliability of agent-created artifacts (tasks, file downloads). The #5064 issue about scheduled tasks reveals a core trust issue: agents appear to complete actions but fail silently. The AgentScope 2.0 migration (#4727) is the most anticipated feature, with users repeatedly asking "when?" (#5149). The attachment bug shows frustration with regression between minor versions.

## Bugs & Stability

**Critical Severity:**
1. **[#5064] Agent-created scheduled tasks not triggering** — Tasks created by agents show as "created" but never execute. No error/warning. Blocks all timer-based agent workflows. **No fix PR yet.**
2. **[#5138] Windows client process keeps increasing, memory >90%** — Memory leak in desktop client on Windows. **No fix PR yet.**
3. **[#5163] Gemini tool calling regression in v1.1.11.post2** — Confirmed regression from v1.1.10. **No fix PR yet.** Author reports "last known good" version.

**High Severity:**
4. **[#5155] v1.1.11 auto-crash and restart in Docker** — Docker container crashes periodically. **No fix PR yet.**
5. **[#5161] Long conversation → QwenPaw stops responding** — Hallucination/freeze after many turns. **No fix PR yet.**
6. **[#5162] Conversation thinking logic enters infinite loop** — Agent stuck in reasoning cycle. **No fix PR yet.**
7. **[#5140 [CLOSED]] Attachment download 404 for docx/pdf** — Fixed in a closed PR (not confirmed in wild).

**Medium Severity:**
8. **[#5137] Memory vector config lost on save** — Fixed by [#5144](https://github.com/agentscope-ai/QwenPaw/pull/5144) (merged today).
9. **[#5098] Memory search results display empty** — Fixed by [#5154](https://github.com/agentscope-ai/QwenPaw/pull/5154) (merged today).
10. **[#5148] Math formula rendering: sqrt symbol broken** — UI rendering issue. Fix submitted via [#5143](https://github.com/agentscope-ai/QwenPaw/issue/5143).

**Low Severity:**
11. **[#5165] Packaged Windows installer results in white screen** — Build script references non-existent modules. **No fix PR yet.**
12. **[#5127] Langfuse traces fragmented across ReAct loop** — Observability/telemetry issue. **No fix PR yet.**

## Feature Requests & Roadmap Signals

| Issue | Feature | Community Interest | Likely Timeline |
|-------|---------|-------------------|-----------------|
| [#5139] | Native agent team/swarm collaboration (like WorkBuddy/JiuwenSwarm) | Moderate (3 comments) | Future major release |
| [#5152] | Slack channel support | Moderate | Unknown |
| [#5156] | Support `kimi-for-coding` + `uv` allowlist | Low (3 comments) | Unlikely near-term |
| [#5164] | Desktop tray, autostart, background service management | Low | Possible next beta |
| [#5167] | Feishu CardKit streaming card optimization for long replies | Low | Under discussion |

**Predictions:** The swarm collaboration (#5139) and AgentScope 2.0 migration (#4727) are aligned with ongoing PRs like [#5078 (Runtime 2.0)](https://github.com/agentscope-ai/QwenPaw/pull/5078). Expect the AgentScope 2.0 migration to be the **headline feature of v1.1.12 or v1.2.0**. Desktop system tray and Slack channel could follow in subsequent releases.

## User Feedback Summary
**Satisfaction Signals:**
- Users value the rapid patch cycle (e.g., v1.1.10 → v1.1.11.post2 fixes for text downloads)
- Memory search tool refactoring (#5154) addressed UI rendering complaints promptly
- The community actively contributes PRs and plugins (DataPaw plugin #4622, Driver abstraction #5067)

**Dissatisfaction Signals:**
- **Regression fatigue:** Users report "Bug reproduced on v1.1.11.post2, last known good on v1.1.10" (#5163) — trust in point releases is eroding
- **Silent failures:** Agent-created timers (#5064) and memory config loss (#5137) frustrate because no error messages are shown
- **Desktop stability:** Windows memory leak (#5138) and Docker crash (#5155) impact production use
- **Missing features:** Kimi coding plan subscribers can't use existing subscriptions (#5156); no Slack support (#5152)
- **UI polish:** Math rendering (#5148), collapsed details (#5145), and Feishu CardKit latency (#5167) degrade UX

**Real Use Cases:**
- *Development:* Docker deployment for agent automation (#5155, #5064)
- *Data Analysis:* DataPaw plugin for BI (#4622)
- *Enterprise:* Workspace restore security (#5022), Langfuse observability (#5127)
- *Education:* Math formula display (#5148, #5143)
- *Multi-channel:* Yuanbao/WeCom integration (#5160, #5150)

## Backlog Watch

| Issue | Created | Last Updated | Days Open | Status |
|-------|---------|--------------|-----------|--------|
| [#4727] Migrate backend to AgentScope 2.0 | 2026-05-27 | 2026-06-12 | **17 days** | OPEN, no assigned milestone |
| [#5064] Agent-created scheduled tasks not triggering | 2026-06-10 | 2026-06-12 | **3 days** | OPEN, no fix PR |
| [#5138] Windows client memory leak | 2026-06-12 | 2026-06-12 | **1 day** | OPEN, no fix PR |
| [#5163] Gemini tool calling regression | 2026-06-12 | 2026-06-12 | **1 day** | OPEN — confirmed regression, needs urgent attention |

**Critical attention needed:**
- **#4727 (AgentScope 2.0 migration)** is the most awaited change (👍2, 10 comments) but has no visible progress beyond a tracking issue. Users are asking directly (#5149). This needs a milestone or status update.
- **#5064 (scheduled tasks)** blocks all timer-based agent workflows and has zero developer response yet.
- **#5138 (Windows memory leak)** and **#5163 (Gemini regression)** are new regressions that require immediate triage to prevent further user loss.

**Open PRs needing review:**
- [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) — Agent OS Driver (under review for 3 days)
- [#5088](https://github.com/agentscope-ai/QwenPaw/pull/5088) — Governance & sandbox interface (under review for 3 days)
- [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) — Decouple plugin loader from startup (open 11 days, critical for frozen environments)
- [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) — DataPaw plugin (open 22 days, first-time contributor)

---

*Digest generated 2026-06-13 from CoPaw GitHub data (agentscope-ai/QwenPaw)*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-13

## 1. Today's Overview

ZeroClaw shows **high development activity** with 33 PRs updated in the last 24 hours (29 open) and 14 issues updated (11 open), indicating a project in an intense active development cycle. The team is executing on several major architectural consolidations, particularly around the core agent turn engine runtime, while also addressing a wave of bug reports from the recently released v0.8.0. No new releases were cut today — the focus is on stabilization and feature integration ahead of what appears to be a v0.8.1 milestone. The v0.8.0 release queue tracker (#7112) was closed, suggesting that release has shipped, though user feedback indicates some significant regressions and setup issues.

## 2. Releases

No new releases were published on 2026-06-13. The most recent release is v0.8.0, which appears to have shipped with schema/config breaking changes (including the `workspace_dir` → `data_dir` rename) and a new multi-agent architecture. Users are reporting installation and first-run issues with this version (see Bugs & Stability).

---

## 3. Project Progress

**Merged/Closed PRs (4 total):**

- **#7548** (closed) — `Chore/01.5 cargo cleanup` — A large cross-cutting dependency and CI cleanup touching nearly every subsystem, merged to master
- **#7545** (closed) — `fix(runtime): auto-include discovered MCP tools in risk_profile allowed_tools` — A high-risk fix for MCP tool visibility that was closed (likely superseded by #7547, still open)
- **Two additional PRs** merged without comment records

**Key Advances:**
- **#7540** (open) — **Major architectural refactor**: Implements RFC #7415 to consolidate the three agent turn engines (`run_tool_call_loop`, `turn_streamed`, `Agent::turn`) onto a single unified engine. This is the most consequential code change in the current pipeline
- **#7549** (open, new today) — Fixes a silent bug where `zeroclaw plugin install` wrote to the wrong directory, making WASM plugins invisible to the runtime
- **#7245** (open, needs-author-action) — Fixes `read_skill` to properly load plugin-bundled skills
- **#7429** (open) — Adds wasmtime dependency preparation for deprecating Extism (the existing WASM runtime)

---

## 4. Community Hot Topics

**Most Active Discussion:**

- **#7415** — *RFC: Unify the three agent turn engines* — 3 comments, 0 👍  
  The RFC is now in implementation (PR #7540). Community conversation has shifted from debate to execution tracking.  
  [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)

- **#7112** — *[CLOSED] v0.8.0 release queue and Stable-tier blockers* — 3 comments  
  This tracker was closed, indicating the v0.8.0 release has shipped. The discussion around schema/config breaking changes and Stable-tier promotion has been resolved.  
  [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7112)

**Underlying Need Analysis:**
The combination of #7415/#7540 and the MCP tool visibility fixes (#7547) reveals a community push for **runtime stability and predictable agent behavior**. Users are hitting configuration edge cases (MCP tools not appearing, CWD inheritance bugs) that make the v0.8.0 experience unreliable. The turn engine consolidation is a recognition that three parallel implementations created a maintenance burden and behavioral inconsistencies.

---

## 5. Bugs & Stability

**Today's New Bug Reports (Ranked by Severity):**

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **S1** | #7537 | `zeroclaw quickstart` fails on Windows 10: "no map-keyed/list section at peer-groups" — blocks new user onboarding | ❌ No fix yet |
| **S1** | #7533 | Docker build fails: `cargo web build` needs C++ compiler (missing `g++` in Dockerfile) | ✅ #7534 (open) |
| **S1** | #7527 | macOS app: after install, cannot detect permissions, displays blank page, then window disappears | ❌ No fix yet |
| **S1** | #7523 | `zeroclaw gateway` shows no web dashboard on v0.8.0; `cargo web build` required but not mentioned | ✅ #7529 (open, partial UX fix) |
| **S1** | #7542 | `ask_user` tool fails with "Channel closed" in gateway web dashboard WebSocket sessions | ❌ No fix yet |
| **S1** | #7263 (closed) | Subagents don't inherit `cwd` in ACP sessions — *was* closed, but underlying V3 path bug persists (see #7541) | ❌ |
| **S2** | #7541 | V3 schema rename broke paths: gateway WS sessions use shared `data_dir` as per-agent workspace, causing collisions | ❌ No fix yet |
| **S2** | #7537 (#7541 related) | Windows quickstart failure may be related to V3 config path issues | See above |

**Regression Pattern:**
The v0.8.0 release shows **significant regressions** in:
1. **First-run experience** (#7523, #7537, #7527) — new users on macOS/Windows cannot even complete setup
2. **Path configuration** (#7541) — the `workspace_dir` → `data_dir` rename broke per-agent directory isolation
3. **Infrastructure** (#7533) — Docker builds are broken without a documented workaround

Multiple S1 bugs have open fix PRs, indicating fast team response, but several remain unaddressed.

---

## 6. Feature Requests & Roadmap Signals

**Today's Top User-Requested Features:**

1. **#7539** — *llama.cpp model router*: Quick switching between local models without restarting the daemon  
   *Likelihood:* High — aligns with the local-first LLM trend and existing llama.cpp provider support

2. **#7543** — *Multi-session support in gateway web chat*: Session sidebar with new/switch/rename/delete  
   *Likelihood:* Medium — UX polish for the web dashboard, which is currently single-session per agent

3. **#7531** — *Streaming card messages for QQ/DingTalk/WeChat/Feishu*: Reduce user wait time for rich messages  
   *Likelihood:* High — addresses a common pain point in Asian messaging channels (popular in ZeroClaw's community)

4. **#6970** — *v0.8.1 integration/channel/provider/tool PR queue* (tracker): Operational tracker for additive work  
   *Likelihood:* Certain — this is the formal v0.8.1 roadmap tracker

**Prediction for v0.8.1:**
Based on tracker #6970 and today's activity, the next release will likely include:
- Turn engine consolidation (PR #7540)
- MCP tool visibility fixes
- WASM plugin path fixes
- Docker build fix
- Streaming card message support for Asian channels
- macOS app stability fixes

---

## 7. User Feedback Summary

**Real Pain Points (from today's issues):**

- **"broken out of the box" sentiment**: Multiple new users (#7523, #7537, #7527) report that the v0.8.0 installation path fails on first run
  > *"Your agent was not created — and nothing on disk was changed"* (#7537)
  > *"after install, the zeroclaw app can't detect granted permissions"* (#7527)

- **Workflow blocking** for power users:
  - MCP tools are enumerated but invisible (#7547)
  - Subagent development patterns broken by CWD inheritance bug (#7263, now closed but replaced by #7541)
  - `ask_user` tool is completely broken in web dashboard sessions (#7542)

- **Build infrastructure friction**:
  - Docker builds fail without manual fixes (#7533)
  - CI/CD pipeline has cross-platform asset detection bugs (#7528, #7530)

**Satisfaction Indicators:**
Users are investing in feature requests with detailed requirements (#7531, #7543, #7539), suggesting the project is solving real problems despite the current instability. The llama.cpp model router request specifically praises the app for "smaller tasks with small local models" (#7539).

---

## 8. Backlog Watch

**Long-Unanswered Items Needing Maintainer Attention:**

- **#6970** — *v0.8.1 integration tracker* (created 2026-05-27, last updated 2026-06-12)  
  No maintainer action in 17 days. As the coordination hub for the next release, this needs triage to route PRs.
  [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6970)

- **#6842** — *Add NEAR AI Cloud provider* (PR, created 2026-05-21, last updated 2026-06-12)  
  23 days open with no maintainer review. Adds a new provider slot with TEE-backed inference support.
  [View PR](https://github.com/zeroclaw-labs/zeroclaw/pull/6842)

- **#7245** — *fix(read_skill): cannot load plugin-bundled skills* (open, created 2026-06-05)  
  Needs-author-action — the author needs to respond to review feedback before this can merge. Blocks skill system reliability.
  [View PR](https://github.com/zeroclaw-labs/zeroclaw/pull/7245)

- **#7415** — *RFC: Unify agent turn engines* (created 2026-06-09)  
  **Update**: This is now being executed via PR #7540 (single consolidation PR per maintainer guidance). The RFC is technically no longer waiting — but the implementation PR needs close review as it touches the core agent runtime.
  [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)

**Overall Backlog Health:**
The oldest open item (#6842) is at 23 days without review — moderate but not critical. The v0.8.0 release wave is creating a surge of new issues that are being addressed quickly (multiple fix PRs filed same day as bug reports), but the existing backlog of integration work is not receiving proportional attention. The maintainer team appears to be prioritizing stability fixes over new features in response to the v0.8.0 regression reports.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*