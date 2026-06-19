# OpenClaw Ecosystem Digest 2026-06-19

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-19 02:44 UTC

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

# OpenClaw Project Digest — 2026-06-19

## Today's Overview

OpenClaw shows **extremely high activity** with 500 issues and 500 PRs updated in the last 24 hours—an extraordinary volume indicative of a major release cycle or intensive bug-fix sprint. Of those, 474 issues remain open/active and 441 PRs are open, while only 26 issues and 59 PRs were closed/merged. No new releases were published today. The project is clearly in a **stabilization and bug-fix phase**, with dozens of critical (P1) and high-severity issues active, many carrying "platinum hermit" ratings (highest impact). Approximately 20–30% of top issues involve message delivery failures, session state corruption, or provider/auth integration problems, suggesting the core messaging pipeline is under intense debugging and refactoring.

---

## Releases

No new releases were published on 2026-06-19.

---

## Project Progress

Today **59 PRs were merged or closed**, though specific merged PRs aren't individually itemized in the available data. Based on open PRs that are close to landing (status: "ready for maintainer look"), the following features or fixes are progressing:

- **Codex app-server timeout fix** ([PR #94685](https://github.com/openclaw/openclaw/pull/94685)): Releases timed-out app-server lanes to prevent stuck sessions.
- **Feishu p2p DM routing fix** ([PR #94761](https://github.com/openclaw/openclaw/pull/94761)): Routes direct message replies to `open_id` instead of p2p group `chat_id`.
- **Note box wrapping fix** ([PR #94746](https://github.com/openclaw/openclaw/pull/94746)): Prevents `openclaw doctor` from mangling long file paths in terminal notes.
- **Model catalog addition** ([PR #94726](https://github.com/openclaw/openclaw/pull/94726)): Adds `gemini-3.5-flash` to the Google model catalog with correct 1,048,576-token context window.
- **Session compaction hardening** ([PR #94704](https://github.com/openclaw/openclaw/pull/94704)): Downgrades post-turn compaction failures from fatal errors to warnings, avoiding discarded replies.
- **Per-agent bootstrap file loading** ([PR #94341](https://github.com/openclaw/openclaw/pull/94341)): Fixes bug where per-agent `agentDir` bootstrap files (SOUL.md, AGENTS.md) were silently ignored.

---

## Community Hot Topics

### Most Active Issues (by comments)

| Issue | Comments | Description |
|-------|----------|-------------|
| [#80319](https://github.com/openclaw/openclaw/issues/80319) | 17 | QA tool-defaults suite conflates Codex-native tools with OpenClaw dynamic tool parity |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) | 11 | Long agent replies silently truncated at ~1000 characters (stop=null, aborted=false) |
| [#54531](https://github.com/openclaw/openclaw/issues/54531) | 11 | Force reply to originating channel (Telegram/Discord/WhatsApp) |
| [#80520](https://github.com/openclaw/openclaw/issues/80520) | 11 | Telegram messages silently dropped, no sendMessage logged |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) | 10 | Model fallback chain not triggered on provider-wide quota exhaustion |
| [#59330](https://github.com/openclaw/openclaw/issues/59330) | 9 (👍14) | Control UI Raw mode permanently disabled since 2026.3.31 — most upvoted open bug |

### Underlying Needs Analysis

**1. Message delivery reliability** (Issues #80520, #84516, #54531, #84569, #82002, #79308, #81484):
Multiple issues report messages dropped, truncated, routed to wrong chat, or lost entirely across Telegram, Discord, WhatsApp, and Feishu. This is the single largest pain point cluster. Users need **guaranteed delivery** regardless of provider, session state, or platform quirks.

**2. Provider failover and auth resilience** (Issues #85103, #80040, #85126, #81607):
Users with multi-provider fallback chains report that quota exhaustion, OAuth invalidation, or wrong auth profile selection cause silent failures or duplicate tool executions. Need for **graceful degradation** and **precise auth profile inference** is clear.

**3. Session isolation and event loop health** (Issues #84903, #84536, #84771, #84610):
One stalled session can block the entire Gateway. Event loop saturation on startup causes 28–64 second delays. Users need **per-session fault isolation** and **non-blocking startup initialization**.

**4. MCP and subagent tool injection** ([#85030](https://github.com/openclaw/openclaw/issues/85030), 👍3):
MCP tool schemas not injected into subagent sessions despite explicit configuration. Power users building multi-agent workflows need reliable tool propagation to child sessions.

### Most Active PRs

| PR | Comments | Description |
|----|----------|-------------|
| [#94685](https://github.com/openclaw/openclaw/pull/94685) | — (code changes only) | fix(codex): release timed-out app-server lanes |
| [#94761](https://github.com/openclaw/openclaw/pull/94761) | — | fix(feishu): route p2p DM replies to user open_id |
| [#94759](https://github.com/openclaw/openclaw/pull/94759) | — | fix(inbound): increase system-event body preview from 160 to 500 chars |
| [#94704](https://github.com/openclaw/openclaw/pull/94704) | — | fix(agents): downgrade post-turn compaction failure from fatal to warning |
| [#94342](https://github.com/openclaw/openclaw/pull/94342) | — | fix(hooks): wire message:sending internal hook to user-defined hooks |

---

## Bugs & Stability

### P0 (Critical) — Data Loss

- **[#84882](https://github.com/openclaw/openclaw/issues/84882) — memory-core Dreaming silently deletes daily memory files (P0, 👍2)**  
  The `normalized recall artifacts` pipeline step deletes `memory/YYYY-MM-DD.md` files without warning. **No fix PR open.** This is the highest-severity issue today due to silent data destruction.

### P1 (High Severity) — Crash Loops, Message Loss, Isolation Failures

| Issue | Type | Has Fix PR? |
|-------|------|-------------|
| [#84903](https://github.com/openclaw/openclaw/issues/84903) — Stalled agent blocks entire Gateway event loop | Isolation failure | No |
| [#84516](https://github.com/openclaw/openclaw/issues/84516) — Long replies silently truncated | Message loss | No |
| [#80520](https://github.com/openclaw/openclaw/issues/80520) — Telegram messages silently dropped | Message loss | No |
| [#84583](https://github.com/openclaw/openclaw/issues/84583) — Cron announce triggers session takeover error | Session state corruption | No |
| [#84610](https://github.com/openclaw/openclaw/issues/84610) — Gateway loops with SIGTERM every ~90s (WSL2) | Crash loop | No |
| [#83968](https://github.com/openclaw/openclaw/issues/83968) — Gateway crashes on macOS with AssertionError | Crash loop | No (rollback to 2026.5.12 works) |
| [#85027](https://github.com/openclaw/openclaw/issues/85027) — macOS upgrade leaves Gateway unrecoverable | Unrecoverable state | No (Time Machine restore required) |
| [#84771](https://github.com/openclaw/openclaw/issues/84771) — 28–64 second event loop saturation on startup | Performance/crash | No |
| [#84536](https://github.com/openclaw/openclaw/issues/84536) — Preemptive context overflow kills embedded sessions silently | Data loss | No |
| [#85103](https://github.com/openclaw/openclaw/issues/85103) — Fallback chain not triggered on quota exhaustion | Degraded operation | No |
| [#85030](https://github.com/openclaw/openclaw/issues/85030) — MCP tools not injected into subagent sessions | Feature broken | No |
| [#94750](https://github.com/openclaw/openclaw/issues/94750) — Discord channel sessions lose recent context after reset | Context loss | No |

### P1 — Auth & Provider Issues

- [#85126](https://github.com/openclaw/openclaw/issues/85126) — Control UI auto-selects wrong auth profile (deepseek instead of minimax)
- [#81607](https://github.com/openclaw/openclaw/issues/81607) — Minimax "No text output returned" when response has thinking blocks
- [#79752](https://github.com/openclaw/openclaw/issues/79752) — Gzip not decompressed under Node v26 on macOS (affects Discord)
- [#82070](https://github.com/openclaw/openclaw/issues/82070) — CLI commands ~14s cold-start regression after 2026.5.12

### P2 — Security & Stability

- [#7722](https://github.com/openclaw/openclaw/issues/7722) — Filesystem sandboxing config requested (👍4)
- [#83736](https://github.com/openclaw/openclaw/issues/83736) — Gateway hard-rejects subordinate nodes with minor version skew
- [#81917](https://github.com/openclaw/openclaw/issues/81917) — Dashboard logs bare token URL despite auto-auth
- [#84256](https://github.com/openclaw/openclaw/issues/84256) — `plugins update --all` downgrades manually-updated npm plugins (👍3)

### Regressions (worked before, now fails)

- [#59330](https://github.com/openclaw/openclaw/issues/59330) — Control UI Raw mode disabled since 2026.3.31 (most upvoted: 👍14)
- [#81484](https://github.com/openclaw/openclaw/issues/81484) — Discord guild reply regression in 2026.5.7
- [#82662](https://github.com/openclaw/openclaw/issues/82662) — Isolated cron agentTurn fails on 2026.5.12 (setup timeout)
- [#94131](https://github.com/openclaw/openclaw/issues/94131) — Telegram iOS font size ignored in v2026.6.8

---

## Feature Requests & Roadmap Signals

### Likely Landing in Next Version

1. **MCP tool injection into subagent sessions** ([#85030](https://github.com/openclaw/openclaw/issues/85030))  
   High-priority fix for multi-agent workflows. Essential for production deployments.

2. **Session isolation / per-session gateway event loop** ([#84903](https://github.com/openclaw/openclaw/issues/84903))  
   Architectural change to prevent one stalled agent from blocking all others. Critical for multi-agent deployments.

3. **Filesystem sandboxing** ([#7722](https://github.com/openclaw/openclaw/issues/7722), 👍4)  
   User-requested security feature for restricting tool file access. Already has discussion traction.

4. **Pre-routing inbound message hook** ([#81061](https://github.com/openclaw/openclaw/issues/81061), 👍3)  
   Enables channel bridging/proxying before routing decisions. Important for enterprise deployments.

5. **Skill author-defined setup scripts** ([#80213](https://github.com/openclaw/openclaw/issues/80213), 👍4)  
   Closes gap between predefined install kinds and custom setup needs. Strong community support.

### Lower Probability but Notable

- Webhook session reuse for multi-turn conversations ([#11665](https://github.com/openclaw/openclaw/issues/11665))
- Plugin SDK surface for skill workflows ([#81913](https://github.com/openclaw/openclaw/issues/81913))
- NEAR AI Cloud provider (PR [#84997](https://github.com/openclaw/openclaw/pull/84997))
- `/new` command at top of native command menu (PR [#85034](https://github.com/openclaw/openclaw/pull/85034))

---

## User Feedback Summary

### Pain Points (High Frequency)

- **Message delivery unreliability** — Users across Telegram, Discord, WhatsApp, and Feishu report messages silently dropped, sent to wrong chat, or truncated mid-sentence. This is the #1 source of user frustration.
- **Crash loops after upgrades** — Multiple macOS and WSL2 users report unrecoverable gateways after upgrading to 2026.5.18–2026.5.19. Rollback to 2026.5.12 is the only known workaround.
- **Data loss in memory subsystem** — The P0 memory-core Dreaming issue ([#84882](https://github.com/openclaw/openclaw/issues/84882)) silently deletes daily memory files. Users who rely on persistent memory are at risk.
- **Authentication/profile confusion** — Wrong auth profile selection, invalidated OAuth tokens, and missing provider fallback chains cause confusing failures. Multi-provider users are disproportionately affected.

### Satisfaction Signals

- Active contribution of fixes from the community (e.g., liuhao1024, mazhuima, Monkey-wusky have multiple PRs today)
- Strong engagement on feature requests (👍4 for filesystem sandboxing, 👍4 for skill setup hooks)
- Users reporting specific downgrade workarounds (2026.5.12 stable for macOS/WSL2 users) suggests awareness of version quality

### Notable Use Case

- **Multi-agent workflows** are clearly in production use. Issues about subagent tool injection ([#85030](https://github.com/openclaw/openclaw/issues/85030)), session isolation ([#84903](https://github.com/openclaw/openclaw/issues/84903)), and cross-agent communication ([#84139](https://github.com/openclaw/openclaw/issues/84139)) all point to sophisticated deployments with multiple collaborating agents.

---

## Backlog Watch

### Long-Unanswered High-Importance Issues

| Issue | Age | Status | Reason for Alert |
|-------|-----|--------|------------------|
| [#54531](https://github.com/openclaw/openclaw/issues/54531) | ~86 days | stale, P1 | Force reply to originating channel (👍1, 11 comments). Stale despite being P1 and having cross-platform impact. |
| [#11665](https://github.com/openclaw/openclaw/issues/11665) | ~131 days | stale, P2 | Webhook session reuse broken (9 comments). Core functionality not working as documented. |
| [#7722](https://github.com/openclaw/openclaw/issues/7722) | ~136 days | stale, P2 | Filesystem sandboxing request (👍4, 8 comments). High user interest, no clear progress. |
| [#81061](https://github.com/openclaw/openclaw/issues/81061) | ~38 days | stale, P2 | Pre-routing hook for channel bridging (👍3, 7 comments). Blocking enterprise adoption. |
| [#80040](https://github.com/openclaw/openclaw/issues/80040) | ~40 days | stale, P2 | Cascading auth/tool/context failures (👍1, 6 comments). Three distinct failure modes unresolved. |
| [#81525](https://github.com/openclaw/openclaw/issues/81525) | ~37 days | stale, P2 | Media routing to vision models without validation (👍1, 5 comments). |

### PRs Needing Maintainer Attention

| PR | Status | Reason | 
|----|--------|--------|
| [#94685](https://github.com/openclaw/openclaw/pull/94685) | 👀 ready for maintainer look | Fixes critical session stall issue (#84569). High priority. |
| [#94746](https://github.com/openclaw/openclaw/pull/94746) | 👀 ready for maintainer look | Fixes terminal display corruption. Low risk. |
| [#94704](https://github.com/openclaw/openclaw/pull/94704) | 📣 needs proof | Changes compaction failure to warning. Addresses data loss risk. |
| [#84978](https://github.com/openclaw/openclaw/pull/84978) | ⏳ waiting on author | Discord desktop proof workflow — first draft needs testing. |
| [#84896](https://github.com/openclaw/openclaw/pull/84896) | ⏳ waiting on author | LanceDB artifacts for wiki bridge — large PR affecting multiple channels. |

---

*Digest generated from OpenClaw project data, GitHub.com/openclaw/openclaw, as of 2026-06-19. All linked issues and PRs are real.*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the 2026-06-19 community digest summaries.

---

## Cross-Project Comparison Report: Personal AI Agent Ecosystem
**Date:** 2026-06-19

### 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is in a high-velocity stabilization phase, characterized by massive bug-fix sprints (OpenClaw, Hermes Agent) and rapid iteration toward feature completeness (ZeroClaw, NanoBot). The ecosystem is consolidating around three core challenges: achieving reliable multi-agent workflows, ensuring message delivery fidelity across fragmented channel backends (Telegram, Discord, Feishu, Signal), and managing context window/memory state without data loss. While OpenClaw remains the dominant core reference by issue and PR volume, the ecosystem is diversifying quickly, with projects like Hermes Agent, NanoBot, and IronClaw carving out distinct niches in enterprise deployment, cost optimization, and security hardening. The landscape is healthy but noisy, with significant user pain around stability regressions after major upgrades.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today? | Health Score (Qualitative) |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | No | **Intensive Bug-fix Sprint** – High severity P0/P1 issues across core pipeline |
| **NanoBot** | 5 (collected) | 24 | No | **Rapid Feature Iteration** – 19 open PRs, strong maintainer velocity |
| **Hermes Agent** | 50 | 50 | No | **Extremely High Activity** – Healthy merge/close ratio (6 issues, 10 PRs) |
| **PicoClaw** | 2 | 14 | Yes (Nightly) | **Stable Maintenance** – Dependency updates dominate; one critical bug open |
| **NanoClaw** | 4 (collected) | 21 | No | **Security-Focused Active** – 6 PRs merged, multiple security patches |
| **NullClaw** | 4 | 4 | No | **Stable/Slow** – No merge activity; 4 open PRs awaiting review |
| **IronClaw** | 32 | 43 | No | **High Velocity (Reborn Focus)** – 17 PRs merged, strong feature delivery |
| **LobsterAI** | 2 | 15 | Yes (<24h ago) | **Stable Release Cycle** – 14 PRs merged, new release shipped |
| **TinyClaw** | 3 | 0 | No | **Security Triage** – No PR activity; 3 critical CVEs unpatched |
| **Moltis** | 1 | 0 | No | **Low Activity** – Single bug report, no code changes |
| **CoPaw** | 50 | 28 | Yes (Patch) | **High Activity** – Strong triage (34/50 issues closed); critical bugs persist |
| **ZeptoClaw** | 0 | 0 | No | **Inactive** – No activity in 24h |
| **ZeroClaw** | 50 | 50 | Yes (v0.8.1) | **Very High Activity** – Mature release cycle; rapid patch iteration |

**Health Score Notes:**
- *Intensive Bug-fix Sprint*: High volume but dominated by unresolved P0/P1 issues.
- *Rapid Iteration*: High open PR count with good maintenance responsiveness.
- *Stable Maintenance*: Low churn but occasional unresolved critical bugs.
- *Security Triage*: Recent vulnerability reports with no fix activity.
- *Inactive/Low Activity*: Minimal to no developer or community engagement in the observed period.

### 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale & Community:** Unmatched issue/PR volume (500 each in 24h) indicates the largest development and user community. This attracts more contributors and faster bug identification.
- **Cross-Platform Coverage:** Explicitly addresses Telegram, Discord, WhatsApp, and Feishu, matching Hermes Agent and exceeding NanoBot/CoPaw in breadth.
- **MCP Ecosystem Leadership:** Advanced MCP server pool design (e.g., `SharedMCPPool` in CoPaw), with PRs adding LUMEN binary protocol (Hermes Agent).
- **Ecosystem Reference:** "OpenClaw" is the core reference; other projects (PicoClaw, NanoClaw, NullClaw) fork or derive from it.

**Technical Approach Differences:**
- **Architecture:** Centralized Gateway with event-loop-based session management, whereas Hermes Agent emphasizes a more modular CLI/gateway split and NanoBot focuses on workspace sandboxing.
- **Security:** OpenClaw has **weaker built-in sandboxing** than NanoClaw (which patches `send_file` path traversal) or CoPaw (Bubblewrap Linux sandbox PR). OpenClaw's filesystem sandboxing feature request (#7722) has been stale for 136 days.
- **Stability:** OpenClaw's P0 memory deletion bug (#84882) is the **most severe data-loss issue** across all projects today, highlighting that its core subsystem is under more extreme stress than smaller projects.

**Community Size Comparison:**
- OpenClaw's 500 issues/PRs dwarfs all others. The next closest are Hermes Agent and ZeroClaw at 50. This likely reflects 10-20x the user base of any other project.

### 4. Shared Technical Focus Areas

**1. Message Delivery Reliability (Critical)**
- **Affected Projects:** OpenClaw, NanoBot, Hermes Agent, PicoClaw, NanoClaw, CoPaw, ZeroClaw
- **Specific Need:** Guaranteed delivery across provider boundaries, session state preservation, and graceful handling of silent drops/truncation.
- **Common Symptoms:** Messages sent to wrong chat, truncated replies, silent failures, duplicate delivery from async sub-agents.

**2. Multi-Agent / Multi-Profile Orchestration (High)**
- **Affected Projects:** Hermes Agent, ZeroClaw, NanoClaw, CoPaw, NullClaw
- **Specific Need:** Sub-agent tool injection, cross-profile provider isolation, per-agent memory, session fault isolation.
- **Common Symptoms:** Profile data loss, cron jobs ignoring profile settings, MCP tools not injected into subagents.

**3. Provider Failover & Auth Resilience (High)**
- **Affected Projects:** OpenClaw, Hermes Agent, ZeroClaw, CoPaw, NanoBot
- **Specific Need:** Graceful degradation on quota exhaustion, correct auth profile inference, circuit breakers.
- **Common Symptoms:** Quota exhaustion not triggering fallback chains, wrong auth profile auto-selected, OAuth token invalidation causing silent failures.

**4. Context/Memory Management (High)**
- **Affected Projects:** OpenClaw, NanoBot, CoPaw, ZeroClaw, IronClaw
- **Specific Need:** Non-destructive memory compaction, context window management, long-session delivery context preservation.
- **Common Symptoms:** Memory files silently deleted, delivery context lost on consolidation, process-freeze during compaction.

**5. MCP Integration & Protocol Support (Medium)**
- **Affected Projects:** OpenClaw, Hermes Agent, ZeroClaw, CoPaw
- **Specific Need:** Reliable tool injection into subagents, resource/prompt support, streaming tool-calls.
- **Common Symptoms:** MCP tools discovered but not exposed in TUI, Authorization header stripping, missing streaming support.

### 5. Differentiation Analysis

| Feature | OpenClaw | Hermes Agent | NanoBot | ZeroClaw | CoPaw |
|---|---|---|---|---|---|
| **Target User** | Developers / Power users | Production multi-tenant | Enterprise / Managed | Full-stack developers | Developers w/AgentScope |
| **Primary Architecture** | Centralized Gateway | Modular CLI/Gateway split | Agent with Workspace sandbox | Multi-agent runtime | AgentScope 2.0 native |
| **Key Differentiator** | Largest ecosystem, most channels | Robust cron & gateway reliability | Cost optimization, normie UX | Feature velocity, provider coverage | Context compression innovation |
| **Channel Breadth** | Telegram, Discord, WhatsApp, Feishu | Telegram, Gateway, Desktop UI | Feishu, WhatsApp | Signal, Telegram, WhatsApp, Matrix | DingTalk, Feishu, Discord |
| **Security Maturity** | Moderate (stale sandbox requests) | Moderate (gateway FD leaks) | High (workspace sandboxing) | High (security trackers, MQTT CVE) | Moderate (Bubblewrap PR incoming) |
| **Release Cadence** | Major cycle (bug-fix sprint) | Minor releases (v0.16.x) | Continuous (19 open PRs) | Fast patch (v0.8.1) | Steady (v1.1.12+patch) |

**Key Takeaways:**
- **OpenClaw** = the "Linux kernel" of the ecosystem — everyone builds on it, but it carries the most technical debt.
- **Hermes Agent** = the "production server" option — strongest at cron, gateway scalability, and multi-profile.
- **NanoBot** = the "managed service" option — focused on operator UX, cost optimization, and sandboxing.
- **ZeroClaw** = the "feature factory" — highest velocity of new features and bug fixes, but risk of fragmentation.
- **CoPaw** = the "context innovator" — leading on compression algorithms and AgentScope integration.

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High Velocity, Many Open Issues/PRs)**
- **OpenClaw** (500 issues/PRs) — Massive community, but struggling with stability. The most "noisy" ecosystem.
- **Hermes Agent** (50/50) — Strong balance of feature delivery and bug fixing. Likely the most reliable for production.
- **ZeroClaw** (50/50) — Extremely fast release cadence (v0.8.1 after v0.8.0). Attracting many contributors (45 in last patch).

**Tier 2: Active Development (Moderate Velocity, Clear Focus)**
- **NanoBot** (24 PRs) — Focused on memory consolidation and enterprise UX. Healthy maintainer presence.
- **IronClaw** (32/43) — Focused on "Reborn" platform stabilization. Good velocity but high absolute bug count.
- **CoPaw** (50/28) — Strong triage rate but critical unresolved bugs. Context compression work shows roadmap ambition.
- **PicoClaw** (14 PRs) — Maintenance mode with one critical bug. Dependency updates dominate.

**Tier 3: Stable/Foundational (Low Velocity, Low Churn)**
- **NullClaw** (4/4) — Slow but steady. Documentation improvements and targeted fixes.
- **Moltis** (1 issue) — Minimal activity. Single bug report indicates low community engagement.
- **ZeptoClaw** (0/0) — Inactive in the observed period.

**Tier 4: Security Response (No Feature Activity, Unpatched CVEs)**
- **TinyClaw** (3 issues, 0 PRs) — Three critical security advisories with no fixes. **Highest risk project.**

### 7. Trend Signals

**1. The "Normie" Shift (Enterprise UX)**
Multiple projects (NanoBot's `#4390 — Multi-instances for normies`, Hermes Agent's hidden settings PR) indicate a clear pivot toward making AI agents accessible to non-technical users. Expect **managed deployment tooling** and **UI simplification** to be a major theme in Q3 2026.

**2. Multi-Agent as a Requirement, Not a Niche**
Issues about subagent tool injection (#85030 in OpenClaw, #41889 in Hermes Agent, #190 in NullClaw) are no longer experimental — they reflect **production multi-agent deployments**. Developers need robust cross-agent communication, per-agent provider selection, and session fault isolation.

**3. Context Explosion is the #1 Deployment Blocker**
Across all high-activity projects, users are hitting context limits, data loss during compaction, and memory management failures. The demand for **Headroom-style compression** (CoPaw #5063), **eager consolidation** (NanoBot #4402), and **persistent delivery context** (NanoBot #4307) signals that naive context window management is unsustainable for real-world use.

**4. Provider Fragmentation is Getting Worse**
Gemini's strict turn ordering (#6302, ZeroClaw), Anthropic's tool schema requirements (#7961, ZeroClaw), and Groq's tool-call rejection (#7896, ZeroClaw) create an **increasing maintenance burden** for multi-provider agents. Projects that invest in a **unified tool serialization layer** will have a competitive advantage.

**5. Channel Inconsistencies Erode User Trust**
The recurring theme of silent message failures (Telegram drops in OpenClaw #80520, Discord truncation in NanoClaw #2812, Feishu routing in CoPaw #5264) shows that **multi-channel support is still immature**. Users expect the same reliability across all platforms — a gap that remains the single largest source of frustration.

**6. Security is Becoming a Differentiator**
Projects with active security hardening (NanoClaw's `send_file` sandbox fix, CoPaw's Bubblewrap PR, ZeroClaw's route-layer auth trackers) are gaining credibility. In contrast, projects with unpatched CVEs (TinyClaw #282-#284) face existential risk. **Security maturity will increasingly separate valuable projects from experimental ones.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-06-19 | **Source:** github.com/HKUDS/nanobot

---

## 1. Today's Overview

NanoBot is in an **intense development sprint** with 24 PRs updated in the last 24 hours — the highest activity indicator on record for this digest. The maintainer team (notably `yu-xin-c`, `chengyongru`, `franciscomaestre`, and `waelantar`) is closing long-standing bugs and shipping concurrent fixes across memory, security, WebUI, and channel subsystems. Five PRs were merged or closed today, including the critical workspace sandbox fix for git execution (#4380) and a UI performance optimization. While no new releases were cut, the sheer volume of open PRs (19) suggests a **major release candidate is being assembled**, likely addressing memory consolidation correctness, concurrency safety, and multi-instance UX — the three hottest pain points emerging from community issues. Community engagement is moderate; the most-discussed issue has only 3 comments, indicating most development is currently internal/team-driven rather than contentious.

---

## 2. Releases

**No new releases today.** The last release was prior to 2026-06-12. Given the 19 open PRs targeting memory, security, and UX improvements, a 0.3.x or 0.2.2 release appears imminent in the coming weeks.

---

## 3. Project Progress

**5 PRs merged or closed today:**

| PR | Title | Type | Author |
|---|---|---|---|
| [#1391](https://github.com/HKUDS/nanobot/pull/1391) | feat: add consolidation_model for cheaper memory consolidation | Feature (merged) | dgross13 |
| [#4400](https://github.com/HKUDS/nanobot/pull/4400) | ci: skip docs-only changes | CI/CD (merged) | chengyongru |
| [#4403](https://github.com/HKUDS/nanobot/pull/4403) | feat(webui): make Firecrawl a keyless Web Data app | Feature (merged) | Re-bin |
| [#4391](https://github.com/HKUDS/nanobot/pull/4391) | feat(feishu): add QR scan-to-create bot CLI login | Channel (merged) | bllackhu |
| [#4375](https://github.com/HKUDS/nanobot/issues/4375) | [bug] Git Command Execution Blocked by Workspace Security Policy | Bug (resolved) | jjmanrique (reporter) |

**Key advances:**
- **Memory consolidation model routing** (#1391): A long-awaited feature that allows consolidation to use a cheaper model than the primary agent — critical for deployments using expensive models like Claude Opus.
- **Workspace sandbox fix** (#4375 closed + expected #4380): Git operations in workspace subdirectories are no longer blocked, restoring dev workflows.
- **Firecrawl simplified** (#4403): The web data extraction app no longer requires an API key for the hosted endpoint, lowering the barrier for new users.
- **Feishu/Lark channel** (#4391): Added device-code QR flow for automated bot creation, expanding the Asian market channel support.

---

## 4. Community Hot Topics

*No issue or PR has more than 3 comments*, suggesting focused, non-contentious discussion. The most active items are:

### Most Discussed Issue
**[#4307](https://github.com/HKUDS/nanobot/issues/4307) — Post-turn consolidation wipes the agent's own delivery message** (3 comments, open since 2026-06-12)
- **Underlying need:** Users running long multi-iteration turns with constrained context windows (40k tokens) lose the assistant's own delivery message after consolidation. The fix PR [#4373](https://github.com/HKUDS/nanobot/pull/4373) by `yu-xin-c` directly addresses this — it preserves the `_channel_delivery` message during replay-window consolidation. This is the most critical memory bug being actively resolved.

### Most Noteworthy Open Feature PR
**[#4399](https://github.com/HKUDS/nanobot/pull/4399) — Configurable hidden settings sections** (3-day active discussion pattern)
- **Underlying need:** For multi-instance deployments with non-technical users ("normies"), administrators need to hide complex settings. This PR, combined with issue [#4390](https://github.com/HKUDS/nanobot/issues/4390) ("Multi-instances for normies"), signals a **clear product shift toward managed/enterprise deployments**.

---

## 5. Bugs & Stability

### Critical: 1 new bug reported, 1 fix-PR in progress

| Severity | Issue | Status | Fix PR |
|---|---|---|---|
| **High** | [#4408](https://github.com/HKUDS/nanobot/issues/4408) — `Nanobot.run()` per-run hooks **concurrency race condition** (`_extra_hooks` clobbered) | Open (1 comment) | [#4409](https://github.com/HKUDS/nanobot/pull/4409) — draft PR by same reporter |
| **Medium** | [#4374](https://github.com/HKUDS/nanobot/issues/4374) — Project workspace read/write asymmetry (SOUL.md/USER.md written to wrong workspace) | Open (2 comments) | [#4387](https://github.com/HKUDS/nanobot/pull/4387) — fallback fix in review |
| **Medium** | [#4307](https://github.com/HKUDS/nanobot/issues/4307) — Delivery context lost during consolidation | Open (3 comments) | [#4373](https://github.com/HKUDS/nanobot/pull/4373) — open |

**Analysis:**
- The **concurrency bug** (#4408) is the most serious: `run()` mutates shared loop state, meaning any concurrent or interleaved `run()` calls will corrupt hooks. The fix in [#4409](https://github.com/HKUDS/nanobot/pull/4409) passes per-run hooks via `process_direct` instead — but the author marked it as a draft due to public API signature changes, suggesting **maintainer review is still pending**.
- The workspace asymmetry bug (#4374) has a fix (#4387) that falls back to the default workspace for missing files while preferring project-local ones — a pragmatic middle ground.

### Resolved Today
- **Git workspace sandbox** (#4375) closed; fix confirmed by reporter. The regression test PR [#4393](https://github.com/HKUDS/nanobot/pull/4393) by `yu-xin-c` adds end-to-end coverage for git subdirectory commands.

---

## 6. Feature Requests & Roadmap Signals

### Top Predictions for Next Release (0.3.x or 0.2.2)

1. **Eager memory consolidation** (PR [#4402](https://github.com/HKUDS/nanobot/pull/4402)): Archives completed conversation slices without trimming the live session. Likely to ship — closes issue #2604 (a 4-month-old request).
2. **Hidden settings sections** (PR [#4399](https://github.com/HKUDS/nanobot/pull/4399)) + **Multi-instance normie UX** (issue [#4390](https://github.com/HKUDS/nanobot/issues/4390)): The "normies" narrative appears in multiple PRs/issues — a strong signal that the next release will include UI simplification for non-technical users.
3. **Serper.dev search provider** (PR [#4406](https://github.com/HKUDS/nanobot/pull/4406)): A new Google Search API provider, expanding from the existing Keenable/Exa ecosystem.
4. **WhatsApp LID fanout** (PR [#4407](https://github.com/HKUDS/nanobot/pull/4407)): Seeds LID→phone mappings on startup, fixing a first-contact resolution bug.

### Likely Deferred (No Active Fix PR)
- **Post-turn consolidation delivery bug** (#4307) — PR #4373 is open, but the fix changes consolidation boundaries and may need more testing before a release.

---

## 7. User Feedback Summary

**Pain Points Expressed:**
- Consultants and advanced users running high-turn-count conversations are **losing assistant delivery context** (#4307, #4373) — a reliability blocker for production use.
- Developers using Git in workspace subdirectories hit a **security policy regression** (#4375, resolved today) — their feedback confirms the fix works.
- Multi-instance operators want **simpler UI to hide complexity from end users** (#4390, PR #4399) — this is a recurring theme from community operators, not end users themselves.

**Use Cases Driving Development:**
- **Enterprise/managed deployments:** The "normies" story (#4390, #4396, #4399) suggests NanoBot is being deployed at organizations where a single admin manages many instances for non-technical team members.
- **Expensive model optimization:** PR #1391 (consolidation_model) and PR #4402 (eager consolidation) cater to cost-conscious users running Claude Opus or GPT-4-class models.
- **WhatsApp integration at scale:** PR #4407 and PR #4353 (audio transcription fix) indicate active WhatsApp-based deployments encountering real-world edge cases.

**Satisfaction Signals:**
- The workspace security fix (#4375) was closed with a single comment — likely a satisfied user confirming the fix.
- No vocal complaints or frustrated "please fix" comments across open issues.

---

## 8. Backlog Watch

### Issues Needing Maintainer Attention
| Issue | Age | Status | Why It Matters |
|---|---|---|---|
| [#4307](https://github.com/HKUDS/nanobot/issues/4307) | 7 days | Open, fix PR exists | Memory-critical bug affecting long sessions; fix PR #4373 has been open 3 days without merge — may need final review |
| [#4408](https://github.com/HKUDS/nanobot/issues/4408) | 1 day | Open, draft PR | Concurrency safety is a hard blocker for parallel usage; author is waiting for guidance on API signature approach |
| [#4374](https://github.com/HKUDS/nanobot/issues/4374) | 3 days | Open, fix PR #4387 in review | Read/write asymmetry in workspace files; fix is non-breaking but needs sign-off |

### Stale PRs (>3 days without maintainer activity)
- [#4373](https://github.com/HKUDS/nanobot/pull/4373) — Delivery consolidation fix (no merge activity since 2026-06-16)
- [#4353](https://github.com/HKUDS/nanobot/pull/4353) — Audio transcription WAV conversion (since 2026-06-15, marked as draft)

**Recommendation:** Given the 19 open PRs and 0 releases, the maintainer team should **prioritize merging #4373** (memory fix for #4307) and **reviewing #4409** (concurrency fix) before cutting a release, as both are stability blockers.

---

*Digest generated from GitHub data snapshot at 2026-06-18 23:59 UTC. All links are permanent to individual issues/PRs on github.com/HKUDS/nanobot.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date**: 2026-06-19

---

## 1. Today's Overview

Hermes Agent is experiencing **extremely high activity**, with 50 issues and 50 pull requests updated in the last 24 hours, indicating a project in rapid development with strong community engagement. The project maintains a healthy pipeline of 44 open issues and 40 open PRs, with 6 issues and 10 PRs closed/merged today. The community is heavily focused on **multi-profile/multi-tenant enhancements**, **reliability hardening**, and **cross-platform support**, with significant contributions around gateway stability and TUI parity. Two P1 (critical) bugs were reported today, balanced by numerous P2/P3 fixes in the PR pipeline.

---

## 2. Releases
**No new releases today.** The latest stable release remains v0.16.0 (2026-06-05). Several bugs reported over the past few weeks reference v0.16.0 regressions (e.g., #47002, #37369), suggesting a v0.16.1 patch release may be forthcoming.

---

## 3. Project Progress

**10 PRs merged/closed today**, demonstrating steady feature advancement and bugfix velocity:

### Merged/Closed PRs of Note:
- **[#47740] feat(mcp): add LUMEN binary protocol transport support** — New MCP transport offering 32–80% wire compression, multi-agent sharing, and native streaming with 34 tools across 3 reference servers. Significant infrastructure upgrade for MCP users.
- **[#48561] fix(dashboard): resolve chat TUI argv off event loop** — Fixes a synchronous npm install call inside a WebSocket handler that could block the event loop. Rebased from an older PR with hardening.
- **[#48769] feat: add investment assistant plugin** — New plugin introducing Futu screener catalog artifacts, research skills, and workflow tickets for financial analysis use cases.
- **[#47740]** (MCP LUMEN) merged — Major MCP protocol addition.

### Features Advanced:
- **Desktop UI enhancements**: In-app browser side panel (#48760), working folder display in composer (#48749)
- **Cron system overhaul**: Pluggable CronScheduler interface with Chronos managed-cron provider (#48275)
- **Gemini compliance**: Required `x-goog-api-client` header now sent on Gemini API calls (#48761)
- **Guardrails**: No-progress loop detection expanded to cover `terminal` and `execute_code` tools (#48766)

---

## 4. Community Hot Topics

### Most Active Issues

**#34592 — [经验分享] Doer/Reviewer 双角色并行编排实践** (5 comments, open 22 days)
*User "crayfish-ai" shares a detailed production deployment of a Doer/Reviewer dual-role parallel orchestration system with Hindsight shared memory, running for a month across dozens of tasks. Represents advanced production usage at scale.*
📎 https://github.com/NousResearch/hermes-agent/issues/34592

**#41625 — MCP tools discovered but not exposed in TUI mode** (5 comments, 1 👍)
*MCP server tools pass `hermes mcp test` but remain invisible to the agent in TUI sessions. This blocks MCP adoption for TUI users.*
📎 https://github.com/NousResearch/hermes-agent/issues/41625

**#47477 — WhatsApp Group Sending with Hermes Skill (Termux)** (5 comments, closed)
*Comprehensive one-file guide for sending WhatsApp messages via Hermes on Termux. Represents strong community demand for messaging/collaboration integrations.*
📎 https://github.com/NousResearch/hermes-agent/issues/47477

**#33314 — Post-update check hooks for skill/profile drift** (4 comments, open 23 days)
*Request for native hooks that detect skill overlay drift after `hermes update`. Users want automated drift detection rather than manual auditing.*
📎 https://github.com/NousResearch/hermes-agent/issues/33314

**#37369 — FD leak: response_store.db multiple SQLite connections** (4 comments, closed)
*P1 bug: Telegram gateway process hits ulimit after ~2 days due to unclosed SQLite connections. Fixed before today but generated significant discussion around gateway reliability.*

### Analysis of Community Needs
The community is converging on **three themes**:
1. **Multi-tenant/profile isolation**: Users want profiles to work consistently across cron, gateway, delegate tasks, and Desktop sessions
2. **MCP ecosystem integration**: Strong demand for MCP tools to work seamlessly across all UI modes (CLI, TUI, Desktop)
3. **Production reliability**: Users running long-lived gateways and complex multi-agent pipelines are hitting resource leaks and state consistency issues

---

## 5. Bugs & Stability

### P1 (Critical) Bugs Reported Today

| Issue | Component | Description | Has Fix PR? |
|-------|-----------|-------------|-------------|
| **[#48746]** | comp/cli, comp/gateway | Gateway on macOS exits with code 75 but launchd treats it as permanent failure, leaving zombie "running" state | ❌ No |
| **[#48721]** | comp/cli | `hermes update` on system Python targets wrong interpreter, hits PEP 668 on Homebrew Python 3.14 | ❌ No |

### P2 (High) Bugs Reported Today

| Issue | Component | Description | Has Fix PR? |
|-------|-----------|-------------|-------------|
| **[#48731]** | comp/cli, area/auth | `/model` switch prefers native provider over current reseller, causing auth failures | ❌ No |
| **[#48702]** | comp/gateway, comp/tui | Desktop app doesn't show Telegram session messages in real-time | ❌ No |
| **[#48519]** | comp/gateway | Sub-profile gateway: sessions.json populated but state.db empty — complete session data loss | ❌ No |

### P2 Bugs with Fix PRs Open

| Issue | PR | Description |
|-------|-----|-------------|
| **[#48759]** | PR #48759 | File tools resolve `~` using wrong HOME under gateway/cron |
| **[#48770]** | PR #48770 | Shell hooks silently ignored in TUI path |
| **[#48768]** | PR #48768 | Linux copy/paste broken in web dashboard terminal |
| **[#48762]** | PR #48762 | TUI composer garbles input from cursor position reports |
| **[#48763]** | PR #48763 | Windows hermes launchers broken after uv installs |
| **[#48764]** | PR #48764 | Un-persisted messages lost on `/resume` and `/branch` |

### P2 Issues Reported Earlier (still open)

| Issue | Component | Description |
|-------|-----------|-------------|
| **[#47868]** | comp/agent | Timestamp metadata leaked into chat completions payload, rejected by strict providers |
| **[#48689]** | comp/cli, provider/gemini | `hermes doctor` false-positive gemini API key and stale npm vulnerability report |
| **[#48649]** | comp/cli, comp/cron | Cron jobs not profile-aware: use global paths instead of profile paths |
| **[#45245]** | comp/cron | Cron scheduler omits `target_model` when resolving runtime provider |

### Regression Note
Issue **[#47002]** (closed today) confirms a v0.16.0 regression where `SessionDB.__init__()` crashes on SQLite builds without the `trigram` tokenizer. Fix was merged.

---

## 6. Feature Requests & Roadmap Signals

### High-Impact Feature Requests

| Issue | Feature | Likelihood for Next Release |
|-------|---------|----------------------------|
| **[#48716]** | Windows Native Integration Package — run without Docker/WSL2 | **Medium** — strong demand, multiple PRs touching Windows |
| **[#48011]** | First-class Mission/Project source-of-truth primitive | **Low** — requires significant architectural design |
| **[#47058]** | Dashboard config hot-reload / polling for live changes | **Medium** — DevOps oriented, practical to implement |
| **[#43784]** | Shareable Profile Templates | **Medium** — aligns with multi-profile emphasis |
| **[#41889]** | Cross-profile subagent support in delegate_task | **High** — directly relates to active PRs/pipeline |
| **[#41190]** | Unified plugin route selector for per-turn provider/model override | **Medium** — addresses fragmented routing |
| **[#35409]** | Profile/model override parameter for delegate_task | **High** — many duplicates, clear use case |
| **[#31621]** | Web tools support for Gemini & OpenRouter | **Medium** — provider parity request |

### Predictions for Next Release (v0.16.1 or v0.17.0)
1. **Profile-aware cron** — multiple issues (#48649, #45245) indicate this is a critical gap with clear fix path
2. **delegate_task profile/model override** — #35409 and #41889 show consistent demand, solution is well-scoped
3. **Windows native support** — #48716 + PR #48763 (Windows launcher fix) suggest Windows is gaining prioritization
4. **TUI/CLI parity for MCP and hooks** — #41625 and #48770 are clean bugs with identified root causes

---

## 7. User Feedback Summary

### Pain Points
- **"MCP tools work in CLI test but not in TUI"** (#41625) — impedes MCP adoption in the more popular UI mode
- **"Session data loss with sub-profiles"** (#48519) — critical trust issue for multi-tenant deployments
- **"Cron jobs ignore my profile settings"** (#48649) — multi-profile advanced users hit consistency issues
- **"Model switch breaks auth when names collide"** (#48731) — provider routing ambiguity frustrates power users
- **"Desktop doesn't show Telegram live updates"** (#48702) — real-time UX gap between platforms
- **"Can't override provider/model per delegate_task"** (#35409, #41889) — advanced orchestration blocked

### Positive Use Cases Shared
- **Production dual-role orchestration** (#34592) — user "crayfish-ai" successfully ran Doer/Reviewer pattern for a month, demonstrating advanced Hermes capabilities
- **WhatsApp integration** (#47477) — creative Termux-based WhatsApp sending shows platform flexibility
- **Investment assistant plugin** (PR #48769) — community building financial analysis workflows

### Dissatisfaction Signals
- **Recurring v0.16.0 regressions** — #47002 (trigram tokenizer), #37369 (FD leak) suggest testing gaps in the last release
- **macOS launchd integration** (#48746) — self-restart mechanism not properly configured for Apple's service manager

---

## 8. Backlog Watch

### Long-Standing Unresolved Issues (maintainer attention needed)

| Issue | Created | Days Open | Component | Why It Matters |
|-------|---------|-----------|-----------|----------------|
| **[#34592]** | 2026-05-29 | 21 | comp/agent, tool/delegate | Detailed production deployment with concrete improvement suggestions — prime candidate for maintainer feedback |
| **[#33314]** | 2026-05-27 | 23 | comp/cli, tool/skills | Post-update drift detection — affects all users who modify skills or profiles |
| **[#31621]** | 2026-05-24 | 26 | tool/web, provider/gemini | Provider parity request for Gemini web tools — no maintainer response visible |
| **[#30594]** | 2026-05-22 | 28 | comp/cli, python:uv | PEP 668 fix regression — blocks users on Debian/Ubuntu system Python |

### Stale PRs Needing Review

| PR | Created | Days Open | Component | Description |
|----|---------|-----------|-----------|-------------|
| **[#38997]** | 2026-06-04 | 15 | comp/gateway | Stream session tool lifecycle events — significant gateway enhancement, no recent updates |
| **[#48275]** | 2026-06-18 | 1 | comp/cron | Pluggable CronScheduler + Chronos — very recent, but high impact |

### Risk Items
1. **macOS launchd reliability** (#48746) — P1 bug with no fix PR, affects all macOS production deployments
2. **Sub-profile data loss** (#48519) — P1 severity, undermines the entire multi-profile architecture for gateway users
3. **v0.16.0 regression trend** — three regressions reported since release (trigram tokenizer, FD leak, live-only prompts) suggests need for more thorough CI coverage before next release

---

*Digest generated 2026-06-19. Data source: github.com/nousresearch/hermes-agent*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-19

## Today's Overview
PicoClaw shows moderate activity on 2026-06-19, with a new nightly build pushed and a significant volume of dependency updates (14 PRs in 24 hours, 7 merged/closed). Two issues were updated, one being a critical duplicate-message bug from async sub-agents that remains open. The project is actively maintaining its Go backend and web frontend dependencies, but an ongoing stale dependency PR backlog suggests some automation maintenance lag. Overall, the project is in a stable maintenance phase with one notable bug requiring attention.

## Releases
- **Nightly Build v0.3.0-nightly.20260619.287853ab** released as automated nightly.
  - Full changelog: [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)
  - ⚠️ Labeled as potentially unstable — use with caution.
  - No breaking changes or migration notes documented.

## Project Progress
Seven PRs merged/closed today:

- **#3144** — Bumped `actions/checkout` from v6 to v7 (CI pipeline update)
- **#3146** — Bumped `golang.org/x/term` to v0.44.0
- **#3147** — Bumped `Azure/azidentity` Go SDK to v1.14.0
- **#3148** — Bumped `golang.org/x/sys` to v0.46.0
- **#3149** — Bumped `anthropic-sdk-go` from v1.46.0 to v1.50.2 (Anthropic API compatibility)
- **#3107** — Bumped `copilot-sdk/go` from v0.2.0 to v1.0.1 (major version jump)
- **#3141** — **Bug fix**: Added diagnostic logging for Brave Search API silent empty results (`web_search` tool)

Notably, **PR #3141** (`jincheng-xydt`) directly addresses issue **#3125** (Brave API silent failure), adding logging to diagnose when Brave returns HTTP 200 with zero results — signaling that response parsing changes may be needed.

## Community Hot Topics
- **#3094** — [OPEN] [Bug] Async sub-agent (spawn) duplicate messages ([link](https://github.com/sipeed/picoclaw/issues/3094))
  - 2 comments, high-impact UX bug: user gets two identical messages from sub-agent + main agent aggregation.
  - Strong candidate for next point release fix.

- **#3143** — [OPEN] fix(web): block private IPv4 embeds in ISATAP literals ([link](https://github.com/sipeed/picoclaw/pull/3143))
  - SSRF guard bypass fix for `web_fetch`, addressing issue #3074. Shows ongoing security hardening.

- **#3125** — [CLOSED] [BUG] web_search tool fails silently with Brave API ([link](https://github.com/sipeed/picoclaw/issues/3125))
  - Closed after fix PR #3141 was merged. Users noted silent `"No results for: [query]"` responses after `.security.yml` migration.

**Underlying need**: Users are encountering real message delivery issues and tool failures that degrade the assistant reliability — both require prompt resolution.

## Bugs & Stability
| Severity | Issue | Status | PR for Fix |
|----------|-------|--------|------------|
| **High** | #3094 — Duplicate messages from async sub-agents (spawn) in Feishu/Telegram | Open (active) | None yet |
| **Medium** | #3125 — Brave web_search silent failure after `.security.yml` migration | Closed (fix merged) | [#3141](https://github.com/sipeed/picoclaw/pull/3141) |
| **Low** | #3143 — SSRF bypass via ISATAP IPv6 literal embeddings | Open (PR active) | [#3143](https://github.com/sipeed/picoclaw/pull/3143) |

No new crashes or regressions reported today.

## Feature Requests & Roadmap Signals
No explicit feature requests were made today. However, the **Anthropic SDK bump from v1.46.0 to v1.50.2** (PR #3149) suggests upstream API changes being tracked. The **copilot-sdk major version jump (v0.2.0 → v1.0.1/1.0.2)** (PRs #3107, #3145) signals that PicoClaw is evolving its GitHub Copilot integration — likely for next minor release (v0.3.x).

## User Feedback Summary
- **Pain point**: Duplicate message delivery from async sub-agents is actively disrupting user experience on messaging channels (#3094).
- **Pain point**: Silent `web_search` failures waste user time — no error message, just empty results (#3125). This is now diagnosable after fix PR #3141.
- **Satisfaction**: Users who rely on web fetching should feel more secure with the upcoming ISATAP SSRF guard fix (#3143). No explicit praise or complaints were observed today beyond issue reports.

## Backlog Watch
- **#3105** — [OPEN] Dependabot PR: eslint bump from v10.2.1 → v10.4.1 (stale since 2026-06-11) — possible merge conflict risk
- **#3104** — [OPEN] Dependabot PR: shadcn bump from v4.7.0 → v4.11.0 (stale since 2026-06-11) — LTS compatibility concern for web frontend
- **#3103** — [OPEN] Dependabot PR: typescript-eslint bump (stale, 8.59.3 → 8.61.0)
- **#3101** — [OPEN] Dependabot PR: vite bump from v8.0.13 → v8.0.16 (stale, build tooling)
- **#3100** — [OPEN] Dependabot PR: @vitejs/plugin-react bump (stale)

These automated PRs have been open for 8 days without attention — may delay web frontend CI or introduce unmerged security patches. Maintainer review recommended.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for June 19, 2026.

---

## NanoClaw Project Digest — 2026-06-19

**Repository:** [github.com/nanocoai/nanoclaw](https://github.com/nanocoai/nanoclaw)

### 1. Today's Overview
Project activity is **high**, with a significant spike in pull requests (21 updated in 24h) and ongoing security-focused development. While no new releases were cut today, the community is contributing rapidly, with 6 PRs merged/closed and 3 issues resolved. The core team appears focused on security hardening and infrastructure fixes, as evidenced by multiple PRs addressing sandbox escapes and input validation. Overall, the project is in a healthy state of active maintenance, though the open PR count (15) suggests the review queue is building.

### 2. Releases
**None.** No new releases were published in the last 24 hours. The latest referenced version in the repository is v2.1.18.

### 3. Project Progress
Six pull requests were merged or closed today, driving tangible improvements:

- **Agent-to-Agent Approval (PR #2793):** Closed. Merged a feature adding per-message approval policies for connected agents. This allows an optional gate on A→B communication, holding messages for approval before delivery. Fully backward-compatible; no policy = free flow.
- **Agent Provider Selection (PR #2811):** Closed. Merged a fix allowing the agent provider (e.g., OpenAI, Anthropic) to be selected via environment variable during setup, improving deployment flexibility.
- **Skills Symlink Refactor (PR #2810):** Closed. Merged a refactor that creates symlinks from `.agents/skills` and `AGENTS.md` back to `.claude/skills` and `CLAUDE.md`, allowing external harnesses like Codex to read the same configuration.
- **Dead Code Removal (PR #2803):** Closed. Removed the obsolete `resolveGroupIpcPath` function, which had zero production callers following the v2 architecture change.
- **Korean README (PR #2806):** Closed. Added a full Korean translation of the README (`README_ko.md`), following the existing i18n pattern.
- **Security Fix Pipeline (PRs #2817, #2818, #2814, #2815, #2816, #2813):** A series of replacement PRs from `mksocial19-code` were opened (see Bugs & Stability), effectively superseding earlier attempts by other contributors with stricter validation and regression tests.

### 4. Community Hot Topics
- **Issue #957: Podman Support (CLOSED):** The most active issue with 10 comments and 7 👍. User @fuyb requested that Podman be documented as an alternative to Docker. Despite being created in March, it was finally closed today, suggesting the maintainers either decided against it or merged a documentation change.
- **Issue #29: Signal Messaging Channel (CLOSED):** Another long-standing enhancement (7 comments, 4 👍) from February. The request to add Signal as a communication channel was closed today. The underlying community need for diverse, privacy-focused messaging backends is clear.
- **Issue #2807: Security - Non-owner Agent Creation (OPEN):** A critical vulnerability report from @YLChen-007 filed just yesterday. It details a privilege escalation flaw where non-owner members can create persistent child agents without approval. This is a **zero-day** report with zero comments yet, indicating the maintainers likely became aware of it today.

### 5. Bugs & Stability
Security and stability fixes dominate the PR list. No crashes were reported, but several critical bugs are being patched:

- **🔴 Critical - Path Traversal in `send_file` (PR #2818):** Replaces #2817. A fix to confine `send_file` reads strictly to the agent's workspace (`/workspace/agent`), rejecting sibling mounts and lookalike paths. This closes a potential sandbox escape.
- **🔴 Critical - Non-owner Agent Creation (Issue #2807):** An un-patched security vulnerability allowing privilege escalation. No fix PR exists yet, but given the severity, a hotfix is expected imminently.
- **🟡 High - CLI Create Command Broken (PR #2804):** Every `ncl messaging-groups create` command throws `NOT NULL constraint failed`. The CLI create path is completely dead. Fix is in review.
- **🟡 High - Discord Reply Truncation (PR #2812 / #2816):** Long Discord replies (>2000 chars) were silently truncated. The fix sets `maxTextLength: 2000` on the Discord bridge, enabling automatic chunking.
- **🟡 Medium - Session Source Staleness (Issue #2784):** The container runner only watches `index.ts` for changes, missing modifications in files like `ipc-mcp-stdio.ts`. This could cause stale code to run in container sessions.
- **🟡 Medium - Router Primitive JSON Parsing (PR #2801 / #2815):** `safeParseContent` returned non-object JSON (e.g., raw `"5"`) as-is, causing downstream callers to fail. Fix treats primitives as raw text.
- **🟢 Low - Socket Client Timeout (PR #2802 / #2813):** The `ncl` socket transport had no request timeout or buffer limit, risking hanging promises and memory exhaustion.
- **🟢 Low - iMessage Setup Failure (PR #2792):** `add-imessage` script failed on fresh checkouts without pre-existing `src/channels/` directory. Fix adds `mkdir -p`.

### 6. Feature Requests & Roadmap Signals
- **Container Runtime Expansion (PR #2809):** A new PR adds support for **Apple Container** as an alternative runtime to Docker on macOS, plus a remote OneCLI gateway. This signals a roadmap expansion toward platform-native containers.
- **Dashboard Skill (PR #2795):** A community contribution (`/add-clidash`) adds a read-only CLI-derived dashboard. This is a utility skill, not a core change.
- **Owned Issues:** The recent closure of the Podman (#957) and Signal (#29) enhancement issues suggests the maintainers are clearing a backlog, possibly to focus on v2.1.x stability rather than new channel integrations in the short term.

### 7. User Feedback Summary
- **Positive:** Users continue to praise the project’s design and utility (#957: "very useful and well designed"). The community is actively contributing detailed bug reports and fix PRs, demonstrating a healthy, engaged user base.
- **Pain Points:**
    - **Security Concerns:** The discovery of a privilege escalation flaw (#2807) is a significant negative signal for trust, especially in group/team deployments.
    - **Platform Lock-in:** Users are actively requesting non-Docker runtime alternatives (#957, #2809).
    - **CLI Dead Paths:** The 5-month-old bug preventing `messaging-groups create` (#2804) indicates that some CLI paths receive minimal testing, frustrating administrators.
    - **Channel Consistency:** Users report inconsistent behavior between messaging channels (e.g., Discord truncation vs. Telegram chunking).

### 8. Backlog Watch
- **Issue #2632: Telegram Swarm / Multi-Bot Identity (OPEN, 2 comments):** Created May 28, updated June 18. A user is planning a v1→v2 migration and cannot determine the status of the old swarm feature. The maintainers have not yet clarified whether this is deprecated or will be re-added. This ambiguity blocks a real user migration.
- **Issue #2784: Container Runner Staleness (OPEN, 1 comment):** Created June 16. A clear, reproducible bug report showing that the session source sync misses non-`index.ts` files. No maintainer response or fix PR yet.
- **PR #2804: CLI Create Broken (OPEN):** Despite a correct diagnosis, this fix has not been merged. The dead CLI path is a high-impact bug for anyone using the command line for group management.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-19

## 1. Today's Overview

NullClaw saw moderate activity today with 4 open issues and 4 open pull requests updated in the last 24 hours—none were closed or merged. No new releases were published. The project appears to be in a stable but slow development phase, with community discussion focused on platform compatibility (ESP32, WeChat integration) and architectural enhancements (subagent spawning, streaming improvements). Two documentation PRs from a new contributor suggest growing interest in better onboarding and configuration clarity. The lack of merged PRs or closed issues indicates maintainers may be reviewing contributions or prioritizing deeper architectural work.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release information is unavailable from the provided data.

## 3. Project Progress

No pull requests were merged or closed today. All four PRs remain open:

- **#965** — Proposal for structured streaming tool-call support in the SSE parser (companion to root fix)
- **#964** — Enables native API-level tool calls during streaming by fixing `agent/root.zig` behavior
- **#963** — Documentation for WeChat QR code login channel (addresses Issue #817)
- **#962** — Documentation for native Anthropic provider with API key and OAuth support (closes Issue #767)

These PRs represent documentation improvements and a bug fix for streaming tool calls, but none have been merged yet.

## 4. Community Hot Topics

The most active discussions by comment count:

- **Issue #50 — "Can this run on an Esp32?"** (4 comments) — [Link](https://github.com/nullclaw/nullclaw/issues/50)
  - User eager to run NullClaw on ESP32 hardware; potential embedded/IoT use case
- **Issue #817 — "Does nullclaw support WeChat QR code login?"** (2 comments) — [Link](https://github.com/nullclaw/nullclaw/issues/817)
  - Feature request for WeChat QR authentication; a PR (#963) has been opened to address this
- **Issue #190 — "Subagent spawn"** (2 comments) — [Link](https://github.com/nullclaw/nullclaw/issues/190)
  - User asking about multi-agent spawning with different providers per agent; architectural scaling interest
- **Issue #913 — "a2a performance?"** (1 comment) — [Link](https://github.com/nullclaw/nullclaw/issues/913)
  - User reports A2A protocol slower than raw messaging; requests benchmarks

**Underlying needs:** Users want broader platform support (ESP32, WeChat), better multi-agent orchestration, and performance validation of the A2A protocol. Documentation gaps are being addressed via PRs.

## 5. Bugs & Stability

**No new bugs, crashes, or regressions were reported today.** The open issue #913 mentions A2A performance concerns but is presented as a question/observation, not a confirmed bug.

**Related fix PR:** #964 directly addresses a known bug where native tool calls were disabled during streaming in `agent/root.zig` — this is a functional fix for tool-using workflows.

**Severity:** Medium (streaming tool support is a core feature gap being actively patched).

## 6. Feature Requests & Roadmap Signals

User-requested features visible in today's data:

1. **ESP32 support** (#50) — Running NullClaw on low-power microcontrollers; unlikely in next release but could influence edge deployment roadmap
2. **WeChat QR code login** (#817) — PR #963 is open; likely to be merged soon, possibly in next minor release
3. **Subagent spawning with per-agent providers** (#190) — Architectural feature for multi-agent systems; not yet addressed but relevant to scaling
4. **A2A performance improvements** (#913) — User feedback without explicit improvement request; may trigger optimization work
5. **Structured streaming tool-call support** (#965) — Enhancement to SSE parser, companion to the root fix in #964

**Prediction for next version:** WeChat QR documentation (#963) and Anthropic provider docs (#962) are likely to merge first. The streaming tool-call fix (#964) addresses a known limitation and is a strong candidate for the next patch release.

## 7. User Feedback Summary

**Pain points:**
- A2A protocol slower than raw messaging (Issue #913)
- Lack of WeChat QR login support (Issue #817) — dissatisfaction, but being addressed
- Streaming disables native tool calls (PR #964 fix) — functional gap identified by contributor

**Use cases expressed:**
- Embedded/IoT deployment on ESP32 (Issue #50)
- Multi-agent systems with different LLM providers per agent (Issue #190)
- WeChat-based personal assistant integration (Issue #817)

**Satisfaction signals:**
- New contributor (vernonstinebaker) submitted two documentation PRs, suggesting positive onboarding experience and desire to improve the project
- Active community engagement with constructive issues and proposals

## 8. Backlog Watch

**Issues needing maintainer attention (long-unanswered):**

- **Issue #50** — "Can this run on an Esp32?" — Created 2026-02-21 (almost 4 months ago), last updated yesterday, no maintainer response visible. *Priority: Medium* — IoT interest should at least receive a "not currently planned" or "likely never" response.
- **Issue #190** — "Subagent spawn" — Created 2026-03-01 (3.5 months ago), no maintainer response. *Priority: Medium* — Architectural question that affects planning for multi-agent users.

Both issues have recent activity but lack official maintainer acknowledgment. A brief response setting expectations would improve community satisfaction.

**PRs awaiting review:**
- #965, #964, #963, #962 — All created yesterday (2026-06-18), recently enough that delay is not critical. Maintainer review expected within the week.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for June 19, 2026.

---

## IronClaw Project Digest: 2026-06-19

### 1. Today's Overview
The project is in a state of high activity, focusing heavily on stabilizing the "Reborn" engine and WebUI v2, with 32 issues and 43 PRs updated in the last 24 hours. Development velocity is robust, highlighted by the merging of 17 PRs, including significant work on Projects support, trigger systems, and CI infrastructure. The "Reborn" distribution is the clear focus of current development, with a surge of bug reports and UX feedback related to automations, OAuth flows, and approval modals. While no new releases were cut today, the volume of merged PRs suggests a significant release is imminent.

### 2. Releases
No new releases were published today.

### 3. Project Progress
This period saw significant progress on the "Reborn" platform, with 17 PRs merged/closed. Key advancements include:
- **Projects Feature (Finalized):** The core team merged the final two PRs in a stack of five to launch the "Projects" page: PR [#5018](https://github.com/nearai/ironclaw/pull/5018) (backend endpoints) and PR [#5019](https://github.com/nearai/ironclaw/pull/5019) (WebUI frontend wiring).
- **Automations & Triggers:** A new "fire-once" scheduled trigger was merged ([#5065](https://github.com/nearai/ironclaw/pull/5065)), and automation run errors were softened to a yellow "Needs attention" state in the UI ([#5055](https://github.com/nearai/ironclaw/pull/5055)).
- **OAuth & Auth UX:** Workflow for Google OAuth was improved by keeping auth gates visible when URLs are unavailable ([#5067](https://github.com/nearai/ironclaw/pull/5067)). A critical bug where canceling an auth prompt could lead to OAuth loops and running activities was also fixed ([#5070](https://github.com/nearai/ironclaw/pull/5070)).
- **LLM Stability:** Two fixes address a critical "auto model retry hang" issue that stalled agent execution when an invalid model configuration was supplied ([#5043](https://github.com/nearai/ironclaw/pull/5043), [#5045](https://github.com/nearai/ironclaw/pull/5045)).
- **Administration:** LLM usage for the Engine v2 is now being tracked, allowing for accurate cost aggregation ([#4989](https://github.com/nearai/ironclaw/pull/4989)).

### 4. Community Hot Topics
The following issues and PRs generated the most discussion and reactions, signaling key areas of community interest:

- **[Issue #4761](https://github.com/nearai/ironclaw/issue/4761) (Closed): Agent stops after repeated tool failures. (5 comments):** This bug, where an agent would halt instead of recovering from a failed tool call, was the most commented-on issue. The user expectation is for a robust agent that can handle transient errors gracefully, indicating a high priority for resilience.
- **[Issue #4907](https://github.com/nearai/ironclaw/issue/4907) (Closed): Google OAuth run failure.** (3 comments): A critical workflow issue where successful OAuth flow leads to a failed execution rather than resumption. This is a major friction point for users integrating GSuite.
- **[Issue #4942](https://github.com/nearai/ironclaw/issue/4942) (Closed): Tool call failures not showing in UI without reload.** (3 comments): A significant UX pain point where the WebUI does not reflect tool call status in real-time, requiring a manual page refresh to see failures.
- **[Issue #1520](https://github.com/nearai/ironclaw/issue/1520) (Open): Qwen model error.** (3 comments): A long-standing issue regarding compatibility with Alibaba’s Qwen model, specifically a `405 Method Not Allowed` error when using a coding plan endpoint. This remains a barrier for users in certain regions.

### 5. Bugs & Stability
Multiple bugs were reported, with a focus on the "Reborn" platform. Severity is ranked as High, Medium, or Low.

- **High:**
    - **[Issue #5060](https://github.com/nearai/ironclaw/issue/5060) (Closed):** GitHub analysis workflows entering an infinite approval loop. This is a critical failure for automation. *A fix appears to have been merged (status: Closed).*
    - **[Issue #5070](https://github.com/nearai/ironclaw/issue/5070) (Closed):** Auth gate cancel can replay OAuth prompt and leave activity "running." A severe UX and state management issue. *Merged PR #5070 fixes this.*
    - **[Issue #5071](https://github.com/nearai/ironclaw/issue/5071) (Open):** Google OAuth tokens are not proactively refreshed, causing user frustration. This is a high-priority stability issue for long-running sessions.
    - **[Issue #4704](https://github.com/nearai/ironclaw/issue/4704) (Closed):** `builtin.http` tool enters an approval loop after an `invalid_input` failure. *This was closed, suggesting a fix was applied.*

- **Medium:**
    - **[Issue #4992](https://github.com/nearai/ironclaw/issue/4992) (Open):** Local-dev SSO access mismatch causes Railway automations to fail before thread creation. This impacts development and testing workflows.
    - **[Issue #5078](https://github.com/nearai/ironclaw/issue/5078) (Open):** Approval modal becomes unreadable with large tool commands. A fix PR ([#5082](https://github.com/nearai/ironclaw/pull/5082)) is already open.
    - **[Issue #5083](https://github.com/nearai/ironclaw/issue/5083) (Open):** Active automations list scans an unbounded completed-row prefix. A performance/database scalability issue.

- **Low:**
    - **[Issue #5077](https://github.com/nearai/ironclaw/issue/5077) (Open):** Invalid chat URLs show errors instead of redirecting to a new chat.
    - **[Issue #5076](https://github.com/nearai/ironclaw/issue/5076) (Open):** Sidebar incorrectly highlights a chat thread on non-chat pages.

### 6. Feature Requests & Roadmap Signals
The data clearly indicates the "Reborn" platform is the primary development track. Key signals for the next release include:

- **Approval UX Overhaul:** Two related PRs are open: one for bounding approval command previews ([#5082](https://github.com/nearai/ironclaw/pull/5082)) and another for per-turn auto-approve resolution ([#5063](https://github.com/nearai/ironclaw/pull/5063)). This suggests a major improvement to user-interaction flow is coming.
- **Concurrency & Scalability:** A PR for concurrent turn execution ([#5085](https://github.com/nearai/ironclaw/pull/5085)) is open, indicating a move to handle multiple LLM runs in parallel for improved performance.
- **Projects Feature Launch:** With the final PR merged, the "Projects" page is likely to be a headline feature in the next release, enabling better organization and collaboration.
- **Automation UX Redesign:** A dedicated issue ([#5069](https://github.com/nearai/ironclaw/issue/5069)) is open, and a redesign PR ([#5084](https://github.com/nearai/ironclaw/pull/5084)) is already in progress, pointing to a significant UI/UX improvement for the automations page.

### 7. User Feedback Summary
User feedback, primarily from the core QA team and developers, highlights a mix of satisfaction and frustration.

- **Satisfaction:** The new approval dialogs showing the actual command being executed are seen as helpful. The ongoing work to get "Projects" and other new features live is a positive signal.
- **Pain Points:** The most significant pain points are related to reliability and UX friction in the "Reborn" WebUI. Users are reporting:
    - **OAuth flow fragility:** Successful login can still break the agent's execution flow.
    - **Stalled automations:** Automations silently failing or entering infinite approval loops renders the feature unreliable.
    - **Poor feedback loops:** The UI failing to show tool call results without a manual refresh is a major source of confusion.
    - **Overbearing modals:** Approval dialogs for complex tasks (like large shell commands) are difficult to read and manage.

### 8. Backlog Watch
Several long-standing open issues with significant relevance remain unaddressed:

- **[Issue #1012](https://github.com/nearai/ironclaw/issue/1012) (Open, since March 12):** Alibaba Coding Plan incompatibility with `openai_compatible` mode. This has been open for over 3 months with one thumbs-up reaction. It blocks a specific but vocal user segment.
- **[Issue #1520](https://github.com/nearai/ironclaw/issue/1520) (Open, since March 21):** The related "Qwen error" issue mentioned in Community Hot Topics. The status of "Coding Plan" compatibility is a recurring theme. These two issues suggest a lack of formal support for Alibaba's LLM ecosystem, which could be a blocker for adoption in certain markets.
- **[Issue #4500](https://github.com/nearai/ironclaw/issue/4500) & [Issue #4502](https://github.com/nearai/ironclaw/issue/4502) (Open, since June 5):** These "sub-issue" bugs regarding WeCom channel onboarding and approval functionality are critical for users of that platform. The ongoing lack of a fix suggests the WeCom channel may be a lower priority relative to the "Reborn" core and Google integrations.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-19

## 1. Today's Overview
The LobsterAI project shows **very high activity** today, with **15 PRs updated** in the last 24 hours, **14 of which were merged or closed**. A new **release (2026.6.18)** was published, bundling artifact sharing upgrades and voice input refinements. Community engagement is moderate (2 open issues, 1 new feature request). The project is in a **stable release cycle** phase, with significant momentum around **artifact sharing expansion** and **voice input streaming optimization**.

## 2. Releases
### LobsterAI 2026.6.18 (Released 2026-06-18)
**What's Changed:**
- **Artifact sharing upgrade**: Now supports sharing Word, PPT, Excel, PDF, Markdown, and Mermaid files, greatly expanding collaboration capabilities.
- **Voice input simplification**: Removed the legacy short-ASR upload flow; realtime ASR is now the only voice input mode.
- Multiple bug fixes and UI refinements for voice input, computer use, and kit controls.

**Breaking Changes:**
- The legacy `asr:recognize` IPC surface has been removed.
- Settings `voiceInput.recognitionMode` config option no longer exists.
- Users who relied on the non-realtime ASR upload mode must switch to realtime ASR.

**Migration Notes:**
- Update voice input integration code to use only the WebSocket-based realtime ASR client.
- Remove any calls to the removed `asr:recognize` IPC handler.

[View Release](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.6.18)

## 3. Project Progress
**Merged/Closed PRs Today (14 total):**
- **Artifact sharing expansion** ([#2178](https://github.com/netease-youdao/LobsterAI/pull/2178)): Added Markdown and Mermaid file sharing support, including zip packaging for Mermaid single files and Markdown resource handling.
- **Release merge** ([#2179](https://github.com/netease-youdao/LobsterAI/pull/2179)): Merged release/2026.6.11 into main, bringing all recent improvements.
- **Voice input refinements**: Many PRs refining the realtime ASR experience:
  - [#2163](https://github.com/netease-youdao/LobsterAI/pull/2163): Dictation recording UI improvements and ASR quota handling.
  - [#2177](https://github.com/netease-youdao/LobsterAI/pull/2177): Renamed "dictation" to "voice input" throughout the UI.
  - [#2160](https://github.com/netease-youdao/LobsterAI/pull/2160): Removed legacy short-ASR upload flow.
  - [#2155](https://github.com/netease-youdao/LobsterAI/pull/2155): Fixed duplicate realtime ASR start race condition.
- **Computer use** ([#2156](https://github.com/netease-youdao/LobsterAI/pull/2156)): Bumped runtime to 1.0.7 with UIA breadcrumbs for diagnostics.
- **Kit controls** ([#2150](https://github.com/netease-youdao/LobsterAI/pull/2150)): Kept expert suite toolbar sticky across pages.

## 4. Community Hot Topics
- **#1422** ([Issue](https://github.com/netease-youdao/LobsterAI/issues/1422)) [stale, 1 comment]: UI issue in MCP custom pages where long service names overflow the delete dialog. This is a **long-standing usability problem** (~2.5 months old) with no fix PR yet. Users likely find this frustrating when managing many MCP services.

- **#2180** ([Issue](https://github.com/netease-youdao/LobsterAI/issues/2180)) [NEW, 0 comments]: A major feature proposal to upgrade OpenClaw from a toolset to an "AI Collaborator" platform targeting non-elite programmers, featuring a natural language command bar and task dispatch console for cross-model orchestration. This signals growing community interest in **higher-level orchestration abstractions** beyond the current MCP/skill paradigm.

## 5. Bugs & Stability
**No new bugs reported today.** The only open issue ([#1422](https://github.com/netease-youdao/LobsterAI/issues/1422)) is a pre-existing UI rendering bug that persists without a fix.

**Stability improvements in recent release:**
- Fixed duplicate realtime ASR start requests ([#2155](https://github.com/netease-youdao/LobsterAI/pull/2155))
- Resolved voice input mode switch regressions by simplifying to realtime-only ([#2160](https://github.com/netease-youdao/LobsterAI/pull/2160))
- Computer use runtime bumped to 1.0.7 with diagnostic improvements ([#2156](https://github.com/netease-youdao/LobsterAI/pull/2156))

**Severity ranking:** Low — no critical regressions or crash bugs observed today.

## 6. Feature Requests & Roadmap Signals
- **AI Collaborator/Orchestration Platform** ([#2180](https://github.com/netease-youdao/LobsterAI/issues/2180)): The most forward-looking feature request this week. It proposes cross-model task dispatch and project-level memory. Given the project's trajectory (OpenClaw, MCP, Computer Use), this aligns well — likely appears on the roadmap within 1–2 releases.
- **Artifact sharing expansion** (shipped in 2026.6.18): Community demand for richer file type support is being actively addressed.
- **Voice input streaming** (fully shipped): The project pivoted heavily to realtime ASR, likely satisfying requests for lower-latency interaction.

**Prediction for next version:** Continued refinement of the Computer Use MVP, deeper MCP integration with the new artifact sharing flows, and potentially initial scaffolding for the "AI Collaborator" concept.

## 7. User Feedback Summary
**From Issue #1422 (MCP UI overflow):** Users are experiencing **diminished usability** when managing MCP services with long names. The delete confirmation dialog truncates text, making it hard to identify which service is being removed. This is a **recurring pain point** (~2.5 months unresolved) for power users who heavily use MCP custom pages.

**From PR activity patterns:**
- **Positive signal**: Artifact sharing for Word/PPT/Excel/PDF/Markdown/Mermaid directly addresses a major collaboration use case. The high number of related PRs suggests strong team focus on this.
- **Mixed reaction**: The removal of non-realtime ASR may upset users with unstable network connections who preferred the upload-based approach. No direct complaints in issues yet.

**User personas observed:**
- Power users managing custom MCP services (pain: UI overflow)
- Developers using artifact sharing for cross-format collaboration (mostly satisfied)
- Non-elite programmers seeking higher-level orchestration tools (emerging demand)

## 8. Backlog Watch
- **Issue #1422** ([Link](https://github.com/netease-youdao/LobsterAI/issues/1422)) — **High priority attention needed**. Opened 2026-04-03 (2.5+ months ago), UI overflow for long MCP service names in delete dialog. Stale, no assignee, no linked PR. This is the **longest-standing open issue** and directly impacts day-to-day usability for MCP users. Recommend the maintainers label it and assign a fix.

- **PR #1277** ([Link](https://github.com/netease-youdao/LobsterAI/pull/1277)) — Dependencies update (electron 40→42). Still open after 2.5 months. While auto-generated by Dependabot, the **eleven-week gap** to merge electron updates is a security/maintainability concern — especially as electron 42 has been available since at least April 2026.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

Here is the project digest for **TinyAGI (TinyClaw)** as of **2026-06-19**.

---

## TinyAGI Project Digest – 2026-06-19

### 1. Today's Overview
The project is currently under active security review, with three high-severity security advisories filed within the last 24 hours. No new releases or pull requests were recorded today, indicating a maintenance-focused or triage-heavy period. The community engagement is low (zero comments on the new issues), but the nature of the vulnerabilities suggests immediate attention from the core maintainers. Overall, project health is stable but strained by three open, unpatched attack vectors.

### 2. Releases
**None.** No new versions or release artifacts were published in the last 24 hours. The last recorded release remains unchanged.

### 3. Project Progress
- **Pull Requests Merged/Closed Today:** 0
- **Features Advanced/Fixed:** None. There was no PR activity (open, merged, or closed) in the last 24 hours.

### 4. Community Hot Topics
No issues or PRs have accumulated significant reactions or comments today. However, the three new security issues represent the highest-priority discussion points by default:

- **#284 – Unauthenticated API message invocation of Claude** (▲ Critical)  
  Link: [Issue #284](https://github.com/TinyAGI/tinyagi/issues/284)  
  *Underlying need:* Immediate requirement for authentication middleware and permission checks on the `/api/message` endpoint.

- **#283 – Unauthenticated `prompt_file` local file disclosure** (▲ Critical)  
  Link: [Issue #283](https://github.com/TinyAGI/tinyagi/issues/283)  
  *Underlying need:* Input sanitization and authorization on agent-configuration APIs to prevent server-side file leaks.

- **#282 – Untrusted `[send_file: ...]` tag attachment delivery** (▲ Critical)  
  Link: [Issue #282](https://github.com/TinyAGI/tinyagi/issues/282)  
  *Underlying need:* Output validation to prevent attacker-influenced response tags from exfiltrating arbitrary files.

### 5. Bugs & Stability
| Issue ID | Severity | Summary | Fix PR Exists? |
|----------|----------|---------|----------------|
| #284 | **Critical** | Unauthenticated `/api/message` allows invoking Claude without permission checks | No |
| #283 | **Critical** | Unauthenticated agent config allows arbitrary local file disclosure via `prompt_file` | No |
| #282 | **Critical** | Untrusted `[send_file: ...]` tags allow arbitrary host file attachment delivery | No |

All three bugs are newly reported, unpatched, and involve remote exploitation without authentication. No stability or crash-related bugs were reported today.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the security issues strongly signal that the next version (when released) will likely include:
- **Mandatory authentication/authorization middleware** for all API endpoints.
- **Strict validation and sanitization** of `prompt_file` paths (blocking directory traversal).
- **Response output filtering** to prevent untrusted tags like `[send_file: ...]` from executing.

These changes are likely to land as patches rather than new feature releases.

### 7. User Feedback Summary
No user feedback (comments, reactions, or use-case descriptions) was posted on today’s issues. However, the fact that three independent security reports were filed by the same author (YLChen-007) suggests an external researcher actively auditing the project—indicating a perception of insufficient security maturity. General satisfaction/dissatisfaction data is unavailable today.

### 8. Backlog Watch
No long-unanswered or stale issues or PRs were identified today. The three open issues are all new (created 2026-06-18). No PRs are awaiting maintainer attention. The backlog is clean, though the security stack requires immediate triage.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for **2026-06-19**, based on the provided GitHub data.

---

## Moltis Project Digest – 2026-06-19

### 1. Today's Overview
Project activity is minimal, with only a single open Issue updated in the last 24 hours and no Pull Requests or new releases. The repository appears to be in a low-activity state, potentially indicating a pause in development cycles or a focus on internal tasks. The sole update is a bug report regarding core session management. Overall project health is stable but quiet, with no immediate signs of major regression or feature churn.

### 2. Releases
**None.** No new releases were published in the last 24 hours. The latest version of Moltis remains unchanged.

### 3. Project Progress
**No Pull Requests were merged or closed today.** There are currently 0 open, merged, or closed PRs in the last 24 hours. No features or fixes advanced via code merges.

### 4. Community Hot Topics
The only active discussion is related to the latest bug report:

- **[Issue #1132](https://github.com/moltis-org/moltis/issues/1132) (OPEN - [Bug]: "main" session can't be deleted/archived)** – Filed by @vvuk. The issue is brand-new with 0 comments, indicating it has not yet been triaged or discussed. The user confirms they are on the latest version and have searched existing bugs.

**Analysis:** While low in engagement right now, this issue touches on a fundamental user interaction (session management). If the "main" session is truly undeletable, it could block users who want to reset their workspace. This has the potential to become a high-interest topic once maintainers respond.

### 5. Bugs & Stability
**1 bug report today (Medium-high severity pending confirmation):**
- **[#1132](https://github.com/moltis-org/moltis/issues/1132):** "main" session can't be deleted/archived.
  - **Severity:** Medium-High. The inability to delete or archive a primary session could lead to data clutter and workflow friction. This appears to be a UX/data management bug rather than a crash.
  - **Fix PRs:** None yet in the last 24 hours.

**No crashes, regressions, or security bugs were reported.**

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed in the last 24 hours. However, the underlying need in **Issue #1132** suggests a user expectation for full control over session lifecycle. Based on this signal, the next version might include:
- **Session management improvements:** Adding safeguards or disabling the "delete" button for the mandatory "main" session, or allowing users to rename/repurpose it.
- **Clearer UI/UX warnings:** Implementing a confirmation dialog for permanent deletions.

### 7. User Feedback Summary
**Pain Points:**
- A user reports that they cannot delete or archive the persistent "main" session, indicating a possible limitation in Moltis’s session management design.

**Use Cases:**
- Users appear to be attempting to organize or clean up their conversation history, suggesting they are actively using Moltis for extended chat sessions.

**Satisfaction/Dissatisfaction:**
- No positive feedback was captured. The single interaction indicates mild dissatisfaction due to a blocked workflow. The user did not escalate (e.g., no emoji reactions or multiple tags), suggesting a moderate response.

### 8. Backlog Watch
**No backlog items to highlight today.** There are no long-unanswered Issues or PRs that require maintainer attention based on the 24-hour data scope. The project’s open Issue queue appears well-contained, though the low activity could mean older items are parked. Continued monitoring of **Issue #1132** is recommended to ensure it gets a timely triage response.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-19

## Today's Overview

CoPaw shows **high activity** today with 50 issues updated in the last 24 hours and 28 pull requests cycled, reflecting strong community engagement. A patch release (v1.1.12.post1) was published addressing a memory subsystem naming fix and CI script correction. The project maintains a healthy balance of open and closed work items (16 open vs 34 closed issues; 14 open vs 14 merged/closed PRs), indicating steady triage throughput. However, several **critical user-facing bugs** persist — including a process-freeze during context compaction, attachment download failures, and channel routing regressions — that remain unresolved and warrant maintainer priority.

## Releases

- **v1.1.12.post1** [🔗](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12.post1)
  - **Changes:** Fixes prerelease arguments expansion in build scripts; renames ChromaDB probe collection from default to `'probe-test'` to avoid collision in vector stores.
  - **Breaking Changes:** None.
  - **Migration Notes:** No migration required; this is a patch-only fix on post-release.

## Project Progress

**14 PRs were merged or closed today**, reflecting active feature and fix delivery:

- **Context Management Overhaul:** PR [#5309](https://github.com/agentscope-ai/QwenPaw/pull/5309) migrated from `LightContextManager` to AgentScope 2.0 native compression, deprecating the old module. This aligns with recent user complaints about context compaction instability (see Bugs section).
- **Chat UI Improvement:** PR [#5293](https://github.com/agentscope-ai/QwenPaw/pull/5293) changed the history chat list from a drawer pop-up to a permanent right-side embedded panel, improving chat-switching UX.
- **Token Usage Fix:** PR [#5303](https://github.com/agentscope-ai/QwenPaw/pull/5303) fixed context usage display to use the active model's `max_input_length` instead of `agent.running.max_input_length`, correcting context ratio indicators in Web chat.
- **DingTalk SSL Fix:** PR [#5291](https://github.com/agentscope-ai/QwenPaw/pull/5291) explicitly configures SSL certificates for the DingTalk HTTP client, resolving a connectivity failure when installed via `uv tool install`.
- **Windows Build Verification Fix:** PR [#5298](https://github.com/agentscope-ai/QwenPaw/pull/5298) handles Windows certificate store SSL errors in the build verification script.
- **MCP Server Pooling:** PR [#4849](https://github.com/agentscope-ai/QwenPaw/pull/4849) merged into a feature branch, adding `SharedMCPPool` to reuse MCP server processes across 300+ agents instead of spawning one per agent.
- **Plugin Infrastructure:** PR [#5008](https://github.com/agentscope-ai/QwenPaw/pull/5008) and [#4794](https://github.com/agentscope-ai/QwenPaw/pull/4794) contributed uninstall hooks, validator import fixes, and skill provider API exposure.
- **Windows Stale Directory Cleanup:** PR [#4860](https://github.com/agentscope-ai/QwenPaw/pull/4860) actively removes `~`-prefixed ghost skill directories left behind by Windows `pip upgrade`.

## Community Hot Topics

| Issue/PR | Type | Comments | Summary |
|---|---|---|---|
| [#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) | Bug (Open) | 16 | Sub-agent triggers context compaction → **process freeze** requiring manual restart. **Most commented issue.** |
| [#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) | Bug (Open) | 8 | Context compression drops all content when persona file exceeds token threshold → task interruption |
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) | Bug (Closed) | 8 | Attachment download fails for `.docx`/`.pdf` (404 error); plain text works |
| [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | Enhancement (Open) | 7 | Request to integrate [Headroom](https://github.com/chopratejas/headroom) for 60-95% context compression |
| [#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) | Bug (Open) | 7 | Upgrades re-enable previously disabled built-in skills — persisted from earlier issue [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807) |
| [#5264](https://github.com/agentscope-ai/QwenPaw/issues/5264) | Bug (Open) | 4 | Feishu group replies misdirected to private chat when user also has direct session |
| [#3854](https://github.com/agentscope-ai/QwenPaw/issues/3854) | Bug (Closed) | 6 | ChromaDB Rust binding SIGSEGV kills entire process — previously severe |

**Underlying needs:** Users are hitting hard limits on context management — both crashes (#5218) and information loss (#5171) — indicating that the native compression migration (PR #5309) is **urgently needed** but not yet released. The attachment download regression (#5140, now fixed in closed state) and Feishu routing issue (#5264) highlight channel integration fragility. The Headroom integration request (#5063) suggests users want **optional, high-ratio compression** as an alternative to the existing compaction logic.

## Bugs & Stability

### Critical (active, process-killing)

- **[#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) — Process freeze during sub-agent context compaction.** No workaround except restart. **No fix PR yet.** *Severity: Critical.*
- **[#5319](https://github.com/agentscope-ai/QwenPaw/issues/5319) — Console channel always shows "Answers have stopped" even on successful responses.** UI bug replacing actual assistant reply with misleading message. *Severity: High.*

### High (data loss, functionality broken)

- **[#5171](https://github.com/agentscope-ai/QwenPaw/issues/5171) — Context compression drops all content when persona exceeds token threshold**, causing complete task interruption. *Severity: High.*
- **[#5264](https://github.com/agentscope-ai/QwenPaw/issues/5264) — Feishu group replies misdirected to private chat** when user has concurrent private session. *Severity: High.*

### Medium (regression, workarounds available)

- **[#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262) — Disabled skills re-enable on upgrade.** Recurring issue from [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807). *Severity: Medium.*
- **[#5253](https://github.com/agentscope-ai/QwenPaw/issues/5253) — custom_channel listener crashes after any save action** — requires re-saving channel config. *Severity: Medium.*
- **[#5313](https://github.com/agentscope-ai/QwenPaw/issues/5313) — MCP `streamable_http` Authorization header loses `"Bearer"` prefix** on config conversion. *Severity: Medium.*

### Closed/Resolved Today

| Issue | Fix PR |
|---|---|
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) (docx/pdf download 404) | Closed as resolved (no explicit PR linked, but status changed to closed) |
| [#3821](https://github.com/agentscope-ai/QwenPaw/issues/3821) (backup never succeeds) | Closed after 2 months |
| [#5290](https://github.com/agentscope-ai/QwenPaw/issues/5290) (discord.py SSL import error) | PR [#5298](https://github.com/agentscope-ai/QwenPaw/pull/5298) merged today |

## Feature Requests & Roadmap Signals

| Issue | Feature | Likelihood for Next Release |
|---|---|---|
| [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | Integrate Headroom as optional context compression (60-95% reduction) | **High** — PR [#5244](https://github.com/agentscope-ai/QwenPaw/pull/5244) is open & under review |
| [#3940](https://github.com/agentscope-ai/QwenPaw/issues/3940) | Separate vision model routing for image inputs | **Medium** — backlogged since April, no active PR |
| [#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321) | "Scroll" context manager — durable history + recall REPL (first-time contributor) | **High** — open PR, filed today, aligns with context strategy migration |
| [#5310](https://github.com/agentscope-ai/QwenPaw/pull/5310) | Bubblewrap Linux sandbox with mount namespace isolation (first-time contributor) | **Medium** — new feature, needs review |
| [#5304](https://github.com/agentscope-ai/QwenPaw/pull/5304) | `qwenpaw terminal` — terminal coding mode with daemon autostart | **High** — open PR, filed today, may align with CLI enhancements |
| [#5314](https://github.com/agentscope-ai/QwenPaw/pull/5314) | Discord streaming responses via message edit + typing indicator | **Medium** — open PR, filed today |
| [#3768](https://github.com/agentscope-ai/QwenPaw/issues/3768) | Command auto-reject (no approval required) | **Low** — backlogged since April, but has maintainer attention in past |

**Prediction:** The next minor release (v1.1.13) will likely ship the **Headroom integration** and the **new context manager migration** (#5309), addressing the most vocal user pain points around compaction crashes.

## User Feedback Summary

**Pain Points:**
- **Context compaction instability** dominates user sentiment — multiple bugs showing process freezes (#5218) and catastrophic information loss (#5171) when compaction triggers. Users are forced to restart or lose task continuity.
- **Channel routing regressions** in Feishu (#5264) and DingTalk (#5237) erode trust in multi-platform support.
- **Upgrade fatigue** — built-in skills re-enable on every upgrade (#5262), forcing manual reconfiguration.
- **MCP header stripping** (#5313) breaks authentication for remote MCP servers using Bearer tokens.
- **Backup reliability** remains questioned (#3821, closed after 2 months but no root-cause fix documented).

**Positive Signals:**
- **Windows build verification** SSL fix (#5298) and DingTalk SSL fix (#5291) show maintainers are actively addressing platform-specific deployment issues.
- **First-time contributors** are submitting quality PRs (#5321, #5310, #5287, #5244), indicating the project has a healthy onboarding experience.
- **UI improvements** (history panel #5293, context usage display fix #5303) show attention to daily user experience.

**Satisfaction Indicators:**
- High issue closure rate (34/50 issues closed today) suggests active triage.
- Merge/close ratio of 14/14 on PRs indicates efficient review pipeline.

## Backlog Watch

| Issue/PR | Age | Problem | Needed Action |
|---|---|---|---|
| [#3940](https://github.com/agentscope-ai/QwenPaw/issues/3940) — Vision model routing | 52 days (since Apr 29) | Users must manually switch models for image input | Feature request with 5 comments, no PR |
| [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) — DataPaw plugin (12 BI skills) | 29 days (since May 22) | Large plugin bundle awaiting review | Under review, first-time contributor — needs review completion or feedback |
| [#4900](https://github.com/agentscope-ai/QwenPaw/pull/4900) — Decouple plugin loader from agent startup | 18 days (since Jun 2) | Plugin system never initializes in PyInstaller/Tauri builds | Open PR, no recent activity — fixes critical packaging bug |
| [#5265](https://github.com/agentscope-ai/QwenPaw/pull/5265) — Force vector index rebuild on Windows local backend | 2 days (since Jun 17) | Memory store not persisting vector index on Windows | Open PR under review — affects Windows memory reliability |
| [#2265](https://github.com/agentscope-ai/QwenPaw/issues/2265) — Tool call returning `APITimeoutError` | 87 days (since Mar 25) | User reports tool calls never work; model says "no tools available" | Stale; no maintainer response since March |

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-19

## Today's Overview

ZeroClaw shows very high activity today with **50 updated issues** (48 open, 2 closed) and **50 updated PRs** (48 open, 2 merged/closed), signaling a mature project undergoing intensive stabilization and feature development. The v0.8.1 patch release landed recently with 207 commits from 45 contributors, focusing on multi-agent runtime, channels, and provider stack fixes. The project is actively addressing a broad range of high-severity bugs (at least 10+ P1 issues) while simultaneously advancing substantial feature work across channels, providers, and security. Today's PR pipeline is particularly strong, with 11 new PRs opened on June 19 alone, primarily bug fixes with some feature additions.

## Releases

**v0.8.1** was released (the first patch on the v0.8.x line):
- **Scope:** Multi-agent runtime, channels, and provider stack stabilization (v0.8.0 follow-up)
- **Commits:** 207 from 45 contributors
- **Breakdown:** 123 bug fixes, 46 new features
- **No breaking changes or migration notes** documented in the release
- URL: https://github.com/zeroclaw-labs/zeroclaw/releases/tag/v0.8.1

The v0.8.1 release queue tracker (#6970) has been closed, and the project has already started v0.8.3 and v0.9.0 planning trackers (#7320, #7432), indicating rapid iteration.

## Project Progress

Today's merged/closed PRs (2 total):

1. **#7953** (CLOSED) — `fix(cost): capture model cost for RPC/zerocode-TUI and standalone ACP turns` — Fixes #5221, a longstanding bug where model costs were not tracked for non-web-agent interactions (schedules, CLI, RPC). Now costs are captured across all invocation paths.
   URL: https://github.com/zeroclaw-labs/zeroclaw/pull/7953

2. **#7957** (OPEN — note: status mismatch with issue count) — `fix(runtime): persist agent turn costs` — Initializes daemon RPC cost tracking and threads cost contexts through session/prompt turns so costs survive spawned task boundaries.
   URL: https://github.com/zeroclaw-labs/zeroclaw/pull/7957

**Key new PRs today addressing bugs:**
- **#7960** — Pipeline sub-tool execution now respects per-agent ToolAccessPolicy (fixes #7947)
- **#7959** — Auto-approved tools now work on channels at non-Full autonomy levels (fixes #4083)
- **#7958** — Telegram replies to bot messages bypass mention_only gate (fixes #5866)
- **#7909** — Groq native tool calling fixed by adding tool name to tool-result messages (fixes #7896)
- **#7908** — WebDriver browser tool snapshot and CSS selector fixes (fixes #7898)
- **#7942** — Memory embedding decoupled from chat provider API credentials; embed failures survive gracefully
- **#7940** — Agent rename now persists config before moving owned state (fixes #7907)
- **#7936** — CLI approvals read from controlling tty instead of stdin
- **#7847** — Per-sender session persistence serialized to prevent race conditions (fixes #7753)
- **#7961** — Anthropic provider now cleans tool schemas before native serialization (fixes #7900)

## Community Hot Topics

1. **#4467** — **MCP Resource & Prompt Support** (👍 4, comments: 2)
   *Status: OPEN, in-progress*
   ZeroClaw currently supports MCP tools but not resources/prompts. This is a high-value feature for MCP ecosystem integration.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/4467

2. **#5844** — **"Too much emphasis on memory"** (comments: 6)
   *Status: OPEN, P1*
   Users report system prompts over-prioritize memory vs current context, especially in cron jobs. This indicates the memory system lacks proper context-window management.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/5844

3. **#6067** — **Configurable channel reply-intent precheck** (comments: 5)
   *Status: OPEN, P2*
   Request for lighter-weight pre-check model + timeout for channel reply classification, to avoid blocking full agent turns on expensive models.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/6067

4. **#6002** — **"Not clearly addressed to the assistant"** (comments: 5)
   *Status: OPEN, P2, needs-author-action*
   Container-based deployment with llama.cpp local model experiencing Telegram message routing issues.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/6002

5. **#6302** — **Gemini 400 — tool_call before user turn** (comments: 4)
   *Status: OPEN, P1*
   Conversation history serializer places assistant tool_calls before the first user turn, violating Gemini's strict turn ordering requirement.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/6302

**Analysis:** The community is focused on three themes: (1) MCP ecosystem expansion, (2) provider compatibility issues (especially with Gemini, Anthropic, Groq), and (3) context/memory management for cron and long-running agents.

## Bugs & Stability

**Critical / P1 bugs (active):**

| Issue | Title | Fix PR? |
|-------|-------|---------|
| #5844 | Too much emphasis on memory (memory over-system-prompt) | No |
| #6302 | Gemini 400 — tool_call before user turn | No |
| #5808 | Default 32k context budget exceeded 3.3x on iteration 1 | No |
| #5869 | MQTT dependency holds back vulnerable TLS crates (rumqttc) | No (blocked) |
| #6434 | Shell tool calls refused at Full autonomy level | No |
| #6350 | WhatsApp LID-based contact bypasses allowed-numbers | No (in-progress) |
| #6037 | Cron jobs launched repeatedly while still running | No |
| #6841 | vision_provider silently ignored for inbound images | No |
| #7756 | Native/MCP tools unavailable on OpenAI Responses and Anthropic | No (new, today) |
| #7881 | Provider fallback circuit breakers (feature, but safety-related) | No |
| #7148 | (not listed but implied by tracker) | - |

**Issues with associated fix PRs today:**
- #7753 (race condition in session persistence) → PR #7847
- #7896 (Groq tool calling rejection) → PR #7909
- #7898 (browser tool WebDriver bugs) → PR #7908
- #5866 (Telegram mention_only gate too strict) → PR #7958
- #4083 (auto-approved tools blocked on channels) → PR #7959
- #7947 (pipeline sub-tools ignoring agent policies) → PR #7960

**Regression risk:** #7756 (tools unavailable on Anthropic/OpenAI) is a high-severity bug reported just 3 days ago affecting the core agent capability.

## Feature Requests & Roadmap Signals

**Likely for v0.8.3 (tracker #7320):**
- MCP dashboard and web/plugin-management surfaces
- MCP resource and prompt support (#4467 — already in-progress)

**Likely for v0.9.0 (tracker #7432):**
- Authentication middleware refactoring (#6250 — extract require_auth to route-layer)
- Security hardening, per-principal authorization and isolation
- Breaking changes deferred from v0.8.x

**New feature requests today:**
1. **#7891** — Signal media attachment support (P2)
2. **#7890** — Signal outbound Markdown rendering (P3)
3. **#7886** — Telegram per-channel inbound debounce (P3)
4. **#7881** — Provider fallback circuit breakers (P2 — safety critical)
5. **#7875** — RunPod/ComfyUI image generation provider (P3)
6. **#7776** — Free-form ask_user over gateway WebSocket (P2)
7. **#7769** — Wire recovered Matrix room-management APIs to real caller (P2)
8. **#7762** — Cron documentation + per-cron model selection (P2)

**Prediction:** v0.8.3 will likely include MCP dashboards, MCP resource/prompt support, the Signal channel media improvements, and provider circuit breakers. v0.9.0 will be auth/security-focused.

## User Feedback Summary

**Satisfaction signals:**
- The rapid release cycle (v0.8.1 within weeks of v0.8.0) and high fix rate show responsiveness to community issues.
- 45 contributors in a single patch release indicates strong community engagement.

**Pain points (recurring):**
1. **Memory management** (#5844, #5808): System prompt/memory context balancing is a top complaint — agents over-prioritize memory, and default token budgets are too small for tool-heavy agents.
2. **Provider fragmentation** (#6302, #7756, #6841, #7961): Each provider (Gemini, Anthropic, Groq, OpenAI) has unique tool schema and turn-ordering requirements, causing serialization bugs.
3. **Cost tracking** (#5221, fixed by #7953): Users need per-invocation-path cost visibility, especially for cron/CLI/RPC modes.
4. **Channel inconsistencies** (#6002, #6350, #5866, #5514): Telegram, WhatsApp, and Signal all have distinct edge cases around mentions, threading, and media that require channel-specific fixes.
5. **Configuration complexity** (#6067, #7886): Users want more granular, per-channel/per-provider configuration for debouncing, pre-check models, and fallback behavior.
6. **Documentation gaps** (#7762): Cron documentation is missing entirely, and there's no way to specify per-cron models.

**Notable use case:** The cron job use case appears frequently — users want scheduled, cheap model execution with proper memory management (#5844, #7762, #6037).

## Backlog Watch

**Issues needing maintainer attention:**

1. **#5869** — **MQTT security advisory** (P1, blocked) — `rumqttc v0.25.1` pins vulnerable TLS crates. Blocked status means no resolution path is identified despite being critical for production security. Low community engagement (2 comments, 0 👍).
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/5869

2. **#4721** — **Log to stderr instead of stdout** (P2, 3 comments, 0 👍) — Open since March, labeled `no-stale` but no fix PR. Affects CLI usability for piping/redirection.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/4721

3. **#5514** — **Telegram multi-image duplication** (P2, 2 comments, 0 👍) — `no-stale` but no fix PR since April. Image requests duplicated per-image, causing excess LLM calls.
   URL: https://github.com/zeroclaw-labs/zeroclaw/issues/5514

4. **#7215** — **Quickstart wizard missing port field** (P1, needs-author-action) — PR has been open since June 4 without resolution, blocking FTUE for webhook channels.
   URL: https://github.com/zeroclaw-labs/zeroclaw/pull/7215

**Takeaway:** The biggest backlog risk is #5869 (blocked security advisory) and #4721 (long-standing stdout issue). The project handles most new issues quickly, but some older `no-stale` issues could use prioritization.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*