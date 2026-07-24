# OpenClaw Ecosystem Digest 2026-07-24

> Issues: 331 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-24 01:21 UTC

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

# OpenClaw Project Digest — 2026-07-24

## 1. Today's Overview

OpenClaw remains under extreme development velocity with **331 issues** and **500 pull requests** updated in the last 24 hours. Activity levels are exceptionally high, reflecting a project in active crisis-management mode following the 2026.7.1 release. The lion's share of activity centres on **regression fixes**, **session-state corruption bugs**, and **provider compatibility patches**. A significant cluster of **P0/P1 bugs** involves message loss, silent subagent failures, and database write contention — symptoms of architectural strain under scale. No new releases were published today, suggesting maintainers are consolidating fixes for the next patch.

---

## 2. Releases

**No new releases today.** The last published version is 2026.7.1 (July 15), with a 2026.7.2-beta.3 in testing. Users continue to experience regressions on 2026.7.1 (see Bugs & Stability).

---

## 3. Project Progress

Today's merged/closed PRs (187 of 500) and closed issues (95 of 331) indicate steady fix throughput:

- **Telegram DM fallback fix (frontier):** PR #113152 (`fix(feishu): settle outbound lifecycle after delivery`) addresses lifecycle settlement in Feishu/Lark — likely to be replicated across channels.
- **Cron tool schema compatibility:** Multiple PRs (#112661, #108580) are in flight to fix cron tool GBNF grammar failures on llama.cpp and senderless cron run authorization loss.
- **MCP transport resilience:** PR #98435 investigation is active, with #102128 fixing `pendingFinalDelivery` write failures that cause silent reply loss.
- **UI polish:** PR #113184 (`chore(ui): refresh control ui locales`) keeps localization synchronized.
- **Security posture:** PR #92307 (`Warn when host approvals clamp exec security at startup`) nears readiness for maintainer review, adding startup-time safety warnings.
- **State DB robustness:** PR #113185 (`fix(state): add PRAGMA busy_timeout`) addresses SQLite `SQLITE_BUSY` errors under high concurrent write contention.

---

## 4. Community Hot Topics

The most active discussions reveal deep frustration with **silent data loss** and **non-deterministic failures**:

- **[#44925 — Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925)** (22 comments, 🦞 diamond lobster) — Four months old, still open. User reports subagent orchestration fails silently with no retry, notification, or auto-restart on timeout. Multiple failure patterns (E31, E42, E45) with no resolution. Community sentiment: **critical trust issue** — users cannot rely on multi-agent workflows.

- **[#102020 — Second message fails with "reply session initialization conflicted"](https://github.com/openclaw/openclaw/issues/102020)** (15 comments) — Freshly reported (July 8), cross-channel (Signal + daemon). The first message works; every subsequent message fails. Highly reproducible. Community is actively reproducing and narrowing.

- **[#94228 — Native Anthropic thinking blocks brick tool-use threads](https://github.com/openclaw/openclaw/issues/94228)** (14 comments, 🐚 platinum hermit) — Long-running Anthropic tool-use sessions brick permanently with `Invalid signature in thinking block` 400 error. Affects users with complex multi-turn tasks. No fix PR open despite P1 severity.

- **[#92043 — 180s compaction timeout breaks legitimate compaction](https://github.com/openclaw/openclaw/issues/92043)** (13 comments, 🦞 diamond lobster) — The lowered compaction timeout (900s → 180s) is a single wall clock — no partial progress reuse. Users with long histories are stuck in infinite fail-retry loops. PR #89040 (event-loop stall fix) is related but the timeout issue is unresolved.

- **[#108435 — Gateway fails to start after 2026.7.1 update](https://github.com/openclaw/openclaw/issues/108435)** (10 comments, P0, regression) — Update to 2026.7.1 causes gateway crash on startup across systemd, Ollama, and manual launch. A **release-blocker** regression.

**Underlying theme:** Users report **loss of confidence** in multi-turn sessions, MCP tool reliability, and upgrade safety. The community is demanding better error handling, partial progress recovery, and regression testing.

---

## 5. Bugs & Stability

**Critical (P0):**

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#108435](https://github.com/openclaw/openclaw/issues/108435) | Gateway fails to start after 2026.7.1 update (regression) | No PR open |
| [#90378](https://github.com/openclaw/openclaw/issues/90378) | Cron store migration JSON→SQLite silently breaks channel delivery | PR #112661 in review |
| [#103532](https://github.com/openclaw/openclaw/issues/103532) | Novita LLM provider model list retrieval broken (CLOSED) | Fixed |

**High (P1):**

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | Subagent completion silently lost (4 months open) | No |
| [#108580](https://github.com/openclaw/openclaw/issues/108580) | Cron tool schema incompatible with llama.cpp grammar (2026.7.1 regression) | #112661 |
| [#98435](https://github.com/openclaw/openclaw/issues/98435) | MCP loopback transport no auto-reconnect after gateway restart (misleading `recovered=1`) | No |
| [#111519](https://github.com/openclaw/openclaw/issues/111519) | Telegram DM replies fall back after stale DM-scope cleanup (2026.7.2-beta.3 regression) | #113152 |
| [#102081](https://github.com/openclaw/openclaw/issues/102081) | Exec allowlist matches never auto-execute on darwin | No |
| [#101814](https://github.com/openclaw/openclaw/issues/101814) | All channels enter broken state after 2026.6.11 update | No |

**Widespread regression pattern:** Multiple users report **one-message-then-silent** behaviour across channels (WebChat, WhatsApp, Telegram) after recent updates, suggesting a systemic session-state or write-lock issue.

---

## 6. Feature Requests & Roadmap Signals

Top community-requested features, ranked by engagement:

1. **[#110950 — Unify automation around cron jobs](https://github.com/openclaw/openclaw/issues/110950)** (9 comments, CLOSED) — Unify heartbeat, watchers, and scheduled automation into one cron primitive. **Closed by maintainer** — likely targeted for a near-term release.

2. **[#67419 — Session context bloat: bootstrap files re-injected every turn](https://github.com/openclaw/openclaw/issues/67419)** (9 comments, 🦞 diamond lobster) — 20-30% token waste per turn from re-injecting MEMORY.md, SOUL.md, etc. High impact on cost and latency. Simple fix but needs product decision.

3. **[#38568 — Inject context window % into system prompt](https://github.com/openclaw/openclaw/issues/38568)** (6 comments) — Agents need awareness of context usage to self-regulate. Quick UX win.

4. **[#8299 — Config option to suppress sub-agent announce](https://github.com/openclaw/openclaw/issues/8299)** (8 comments) — Sub-agent announce step is unreliable; models frequently ignore `ANNOUNCE_SKIP`. Users want a config flag.

5. **[#41418 — Global --dry-run mode for tool calls](https://github.com/openclaw/openclaw/issues/41418)** (5 comments) — Risk-free preview of agent actions. Shows maturity of user base (production deployments).

**Roadmap prediction:** The **cron unification** (#110950) is most likely next — closed by maintainer suggests internal development is underway. **Context bloat** (#67419) and **suppress announce** (#8299) are low-hanging fruit that could ship in 2026.7.2 or 2026.7.3.

---

## 7. User Feedback Summary

**Pain points (repeated across issues):**

- **"Silent failure is the worst failure"** — Multiple users emphasize that invisible message loss (no notification, no retry) destroys trust. Issue #44925 sums it up: "Subagent completion silently lost — no retry, no notification, no auto-restart."
- **"Upgrading is risky"** — Users report regressions on every recent point release (6.11 → 7.1 → 7.2-beta.3). The cron store migration (#90378) and gateway crash (#108435) are cited as upgrade barriers.
- **"Compaction is a black box"** — The 180s timeout issue (#92043) shows users feel punished for legitimate long-running workflows. "It converts a slow-but-recoverable compaction into a permanent fail-retry loop."
- **"MCP tooling is fragile"** — Discord agents can't access MCP tools (#91799), MCP loopback doesn't reconnect (#98435), and cron tools break with local models (#108580). Users running custom MCP servers are particularly affected.

**Positive signals:**
- Community is actively reproducing and narrowing bugs (see #102020 with 15 comments in 2 weeks).
- Users appreciate the transparency of the issue tracking system — many issues include detailed reproduction steps and logs.
- Feature requests show sophistication: RBAC, deployment manifests, memory ingestion pipelines, Azure Foundry support.

---

## 8. Backlog Watch

Long-open or neglected issues requiring maintainer attention:

| Issue | Age | Status | Priority |
|-------|-----|--------|----------|
| [#44925](https://github.com/openclaw/openclaw/issues/44925) | 133 days (March 13) | No fix PR, needs product decision | **P1** — Subagent silent loss |
| [#43374](https://github.com/openclaw/openclaw/issues/43374) | 135 days (March 11) | Stale, no live repro, needs maintainer review | **P1** — All LLM calls time out simultaneously |
| [#42273](https://github.com/openclaw/openclaw/issues/42273) | 136 days (March 10) | Stale, no live repro | **P2** — `backup create` stalls on large installations |
| [#41372](https://github.com/openclaw/openclaw/issues/41372) | 137 days (March 9) | Stale, field report with 25 findings | **P2** — Comprehensive user field report with actionable fixes |
| [#48641](https://github.com/openclaw/openclaw/issues/48641) | 129 days (March 17) | Stale, needs security review | **P2** — Discord DMs silently dropped |
| [#7524](https://github.com/openclaw/openclaw/issues/7524) | 172 days (Feb 2) | Feature request, needs product decision | **P2** — Group session consolidation (5 👍) |
| [#12219](https://github.com/openclaw/openclaw/issues/12219) | 166 days (Feb 9) | Feature request, needs security review | **P2** — Skill Permission Manifest Standard |
| [#43673](https://github.com/openclaw/openclaw/issues/43673) | 134 days (March 12) | Stale, needs security review | **P2** — org/team deployment scaffolding |

**Most concerning backlog item:** [#44925](https://github.com/openclaw/openclaw/issues/44925) (subagent silent loss) is 4+ months old, P1, diamond lobster rating, with **no fix PR open**. The underlying architecture (subagent orchestration without retry/notification) may require significant refactoring. Three related issues (#8299 suppress announce, #38520 pre-compaction notification, #67419 context bloat) all touch the same subsystem, suggesting a systemic gap in agent lifecycle management.

**Second concern:** The **backlog of stale "needs-live-repro" issues** (10+ items) suggests maintainers are struggling to reproduce complex production failures. Users with high-volume deployments (Telegram forums, multi-agent setups) continue to encounter unreproducible crashes.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — 2026-07-24

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is experiencing intense fragmentation and maturation simultaneously. Projects are converging on core requirements—session reliability, multi-channel delivery, MCP tooling, and provider interoperability—while diverging sharply in architectural philosophy (monolithic vs. modular, SQLite vs. PostgreSQL, agent-as-service vs. agent-as-IDE). The ecosystem is post-hype, with users demanding production-grade reliability: silent failures, data loss, and upgrade regressions are consistently the top pain points across all active projects. A clear stratification is emerging: two dominant reference implementations (OpenClaw, Hermes Agent), a fast-following cluster (ZeroClaw, CoPaw, IronClaw), and several specialized or smaller projects serving niche deployment scenarios.

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Assessment |
|---|---|---|---|---|
| **OpenClaw** | 331 | 500 | No | 🔴 Crisis mode – regression flood, P0 bugs, community trust eroding |
| **CoPaw** | 35 | 50 | v2.0.1-beta.2 ⬆️ | 🟡 Volatile – rapid iteration, v2.0 regressions, active response |
| **ZeroClaw** | 50 | 50 | No | 🟡 Stretched – high throughput, severe review bottleneck (48/50 PRs open) |
| **Hermes Agent** | 50 | 50 | No | 🟡 Guarded – high maintenance activity, strong community engagement |
| **IronClaw** | 32 | 50 | No | 🟢 Pre-launch – disciplined stabilization, v1 blockers being methodically closed |
| **NanoBot** | 8 | 37 | No | 🟢 Healthy – fast maintenance sprint, responsive to regressions |
| **PicoClaw** | 1 | 15 | No | 🟢 Moderate maintenance – Dependabot-heavy, 2 meaningful feature PRs |
| **NanoClaw** | 1 | 10 | No | 🟢 Healthy – active stabilization sprint, 4 PRs merged today |
| **Moltis** | 1 | 5 | 2 releases ⬆️ | 🟢 Healthy – focused security+UX push |
| **LobsterAI** | 3 | 1 (Dependabot) | No | 🟠 Stale – 3 bugs unacknowledged for 3+ months |
| **ZeptoClaw** | 2 | 1 | No | 🟢 Minimal – maintainer-only, 2 critical bugs with fix in progress |
| **TinyClaw** | 0 | 0 | No | ⚪ Inactive |
| **NullClaw** | 0 | 0 | No | ⚪ Inactive |

## 3. OpenClaw's Position

**Advantages vs. peers:**
- Largest contributor base and community engagement by 10x (331 issues, 500 PRs daily)
- Most mature MCP transport implementation and multi-channel support (Feishu/Lark, Telegram, Signal, Discord)
- Most comprehensive feature surface: cron automation, subagent orchestration, session state management
- Diamond lobster user rating system indicates sophisticated, high-volume deployments

**Technical approach differences:**
- SQLite-centric with aggressive compaction; peers (ZeroClaw) moving toward PostgreSQL
- Monolithic core reference design vs. modular approaches (NanoBot, ZeptoClaw)
- MCP loopback transport as primary integration pattern vs. direct SDK integrations in Hermes Agent

**Community size comparison:**
- OpenClaw's daily activity exceeds the next 4 projects combined
- However, this correlates with **crisis**, not health: 187/500 PRs merged, 331 issues, P0 regressions in every recent release
- Community sentiment is negative: "Upgrading is risky," "Silent failure is the worst failure," "Compaction is a black box"

**OpenClaw's peer comparison:** It is the most feature-rich but the **least reliable** project in the ecosystem. Its community is demanding the stability that ZeroClaw and IronClaw are prioritizing from the start.

## 4. Shared Technical Focus Areas

**Session State Reliability** (all active projects)
- OpenClaw: Session corruption, reply session initialization conflicts, subagent silent loss
- Hermes Agent: Session cost resets on restart, context compression permanent failure
- ZeroClaw: Telegram/WeChat update offset persistence results in message loss
- CoPaw: Context corruption from ReAct agent merging tool_call + tool_result
- NanoClaw: Duplicate container spawn race, unknown slash commands dropped

**Multi-Channel Delivery** (OpenClaw, ZeroClaw, Hermes, NanoClaw, Moltis, CoPaw)
- Telegram thread support (NanoClaw, Hermes), DM fallback (OpenClaw), unauthorized sender handling (ZeroClaw)
- Silent reply loss across channels is the most consistent failure pattern

**MCP/Provider Interoperability** (OpenClaw, CoPaw, Hermes, ZeroClaw)
- MCP tools broken after v2.0 upgrades (CoPaw #6405)
- MCP loopback transport auto-reconnection failure (OpenClaw #98435)
- Cron tool schema incompatible with local models (OpenClaw, ZeroClaw)

**Security Hardening** (ZeroClaw, Moslits, IronClaw, ZeptoClaw)
- Subprocess credential scrubbing (ZeptoClaw, ZeroClaw)
- TOTP for cross-channel approval (ZeroClaw #3767)
- Slack allowlist bypass fixes (Moltis #1163, #1164)

**Windows Platform Gaps** (Hermes, CoPaw, ZeroClaw)
- Console window flashes, path resolution, PowerShell script collapse
- All projects treat Windows as second-class, users frustrated

**Performance Overhead** (OpenClaw, CoPaw, Hermes)
- 2s fixed overhead in CoPaw v2.0 (#6307)
- 20-30% token waste from context bloat in OpenClaw (#67419)
- Session cost persistence adding latency in Hermes (#67762)

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | Hermes Agent | CoPaw | IronClaw |
|---|---|---|---|---|---|
| **Target User** | Power users, multi-agent orchestrators | Security-conscious operators | Desktop developers, macOS | Content creators, Docker users | Enterprise deployments |
| **Core Architecture** | Monolithic, SQLite-based | Modular, PostgreSQL-ready | Desktop-native, gateway | Plugin-based, Docker-first | Rust, hermetic testing |
| **Primary Channels** | Feishu/Lark, Telegram | Telegram, WeChat, Matrix | Desktop GUI, WhatsApp | WebChat, Desktop | Slack, Telegram, WebChat |
| **Differentiating Feature** | Subagent orchestration | Landlock sandbox, TOTP | Cursor SDK integration | Creator App, ReMe memory | V1 launch discipline |
| **Community Style** | High-volume, frustrated | Architectural, security-focused | Multi-platform, enterprise | Active, fast iteration | QA-driven, methodical |
| **Risk Profile** | High – regression-prone | Medium – review bottleneck | Medium – Windows gaps | High – v2.0 instability | Low – pre-launch control |

**Architectural spectrum:**
- **OpenClaw** is the "full-stack" reference: everything included, trade stability for features
- **ZeroClaw** is the "security-first" option: sandboxing, TOTP, multi-instance mesh
- **Hermes Agent** is the "developer desktop" agent: deep IDE integration (Cursor), local-first
- **CoPaw** is the "content creation" agent: script-to-video, memory editing, multi-model testing
- **IronClaw** is the "enterprise rollout": v1 launch discipline, deterministic testing, multi-tenant

## 6. Community Momentum & Maturity

**Tier 1: Crisis-High Velocity (rapidly iterating, unstable)**
- **OpenClaw**: Highest raw activity but negative sentiment. 331 issues, P0/P1 bugs, regression in every point release. Users losing trust.
- **CoPaw**: v2.0 transition creating volatility but contributors are fixing fast (21 PRs merged today). Performance regression (#6307) is the top worry.
- **ZeroClaw**: High throughput with 10 PRs blocked in `needs-author-action`. Review bottleneck risks contributor burnout.

**Tier 2: Healthy-Responsive (stable cadence, active community)**
- **Hermes Agent**: 50 PRs/50 issues updated, 16 merged today. Strong multi-platform engagement (Windows, macOS, WSLg). Good fix turnaround (same-day PRs for reported bugs).
- **NanoBot**: 37 PRs updated, 30 merged. Fast maintenance sprint, security hardening, WebUI polish. Responsive to regressions.
- **NanoClaw**: 10 PRs, 4 merged. Focused stabilization: container runtime, Matrix E2EE, typing indicators.
- **Moltis**: 5 PRs, 5 merged. Security-first, clean backlog. 2 releases today.

**Tier 3: Pre-Launch or Maintenance (controlled velocity)**
- **IronClaw**: 50 PRs but deliberate v1 launch focus. Daily failure taxonomy, hermetic test migration. Disciplined.
- **PicoClaw**: 15 PRs but 10 are Dependabot. 2 meaningful feature PRs progressing slowly.
- **ZeptoClaw**: 2 issues, 1 PR. Maintainer-only, critical safety fixes in progress.
- **Moltis**: Clean backlog, rapid security fixes.

**Tier 4: Stale or Inactive**
- **LobsterAI**: 3 bugs unacknowledged for 3+ months, including critical sql.js crash with data loss risk. Community trust eroding.
- **TinyClaw, NullClaw**: Zero activity.

## 7. Trend Signals

**1. Users demand reliability over features.** Every active project with >50 daily issues has "silent failure," "data loss," or "upgrade regression" as the top pain point. The ecosystem is moving from "can agents do X?" to "can agents reliably do X without losing my data?" This is a maturation signal—users are deploying agents in production.

**2. Multi-agent orchestration is the killer use case.** OpenClaw's subagent feature (#44925, 133 days open) and ZeroClaw's A2A protocol tracker (#3566, 7 👍) are the most-requested architectural features. Users need agents that delegate, aggregate, and coordinate—not just single-turn chat.

**3. Security is becoming a differentiator.** ZeroClaw (Landlock, TOTP), Moltis (Slack allowlist hardening), ZeptoClaw (credential scrubbing), and IronClaw (admin-managed subjects) are all investing in security as a feature. Projects without security hardening (LobsterAI, OpenClaw's subagent credential exposure) are losing credibility.

**4. The Windows experience gap is a persistent problem.** Hermes, CoPaw, ZeroClaw all have active Windows bugs (console flashes, missing DLLs, path issues). No project treats Windows as a first-class platform. This limits the ecosystem's enterprise adoption potential.

**5. Model diversity is straining tool-calling reliability.** CoPaw's v2.0 MCP regression (#6405) and cross-model tool_call parsing issues (#6363) highlight that tool-calling behavior varies significantly by provider. Projects investing in robust provider-agnostic parsing (ZeroClaw's unified SSE, IronClaw's hermetic testing) are better positioned.

**6. Configuration management is the new reliability bottleneck.** ZeroClaw has 4 concurrent config bugs (dot-key resolution, save_dirty corruption, set_prop masking, fresh alias dropping). NanoClaw has config-scope conflicts. OpenClaw's cron store migration silently breaks delivery. As projects add features, config surfaces grow without commensurate testing.

**7. Desktop vs. Gateway is an open architecture question.** Hermes (Desktop-native) and IronClaw (gateway-first) represent opposite approaches. Hermes has better UX (Cursor integration, project management) but narrower deployment. IronClaw has better multi-channel but weaker desktop experience. The ecosystem hasn't settled on a dominant architecture.

**Value for AI agent developers:**
- **Build for reliability first.** Users will tolerate fewer features more than unreliable features. Silent message loss destroys trust.
- **Invest in configuration testing.** Config bugs are the most insidious—they manifest as intermittent failures that are hard to reproduce.
- **Assume multi-agent orchestration will be your killer feature.** Design your session state, tool lifecycle, and messaging infrastructure to support delegation and aggregation from day one.
- **Do not ignore Windows.** Enterprise deployments run on Windows. Every omission in Windows support is a lost contract.
- **Make security observable.** Users cannot assess safety without clear logging. ZeroClaw's credential encryption logging and IronClaw's failure taxonomy are models to follow.
- **Plan for model diversity.** The model landscape will not consolidate. Build parsers, fallback chains, and test harnesses that handle multiple providers gracefully.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-24

## 1. Today's Overview

NanoBot saw very high contributor activity today, with **37 pull requests updated** in the last 24 hours and 30 of those merged or closed — a clear sign of an active maintenance sprint. Eight issues were updated (4 closed), and while no new releases were published, the volume of merged PRs across security, WebUI, channel infrastructure, and tooling suggests a coordinated push toward stability ahead of a future release. The project is in a **healthy, fast-moving phase** with strong community contributions.

## 2. Releases

**No new releases** were published today. The latest available release remains `nanobot-ai==0.2.2` (referenced in issue #5051). Given the high volume of merged fixes, a patch or minor release may be imminent.

## 3. Project Progress

The following major merged/closed PRs advanced the project today:

**Security & Workspace Integrity**
- [#4889](https://github.com/HKUDS/nanobot/pull/4889) — Authorized destructive priority commands (`/restart`, `/stop`) behind an explicit allowlist (`channels.admin_senders`). Merged.
- [#4594](https://github.com/HKUDS/nanobot/pull/4594) — Fixed shell workspace guard path extraction after `=` signs (e.g., `curl --output=/etc/passwd`). Merged.
- [#5065](https://github.com/HKUDS/nanobot/pull/5065) — WebUI file preview now respects `media` directory when `restrictToWorkspace` is enabled. Merged.

**WebUI & UX**
- [#5061](https://github.com/HKUDS/nanobot/pull/5061) — Simplified model preset settings: replaced "current configuration" workflow with reusable presets and explicit model call order. Merged.
- [#5017](https://github.com/HKUDS/nanobot/pull/5017) — WebUI now shows per-turn model fallback indicator in composer badge. Merged.
- [#5060](https://github.com/HKUDS/nanobot/pull/5060) — Polished responsive layouts and settings search. Merged.
- [#5058](https://github.com/HKUDS/nanobot/pull/5058) — Unified settings and dark mode surfaces. Merged.
- [#5067](https://github.com/HKUDS/nanobot/pull/5067) — Composer model badge now stays in sync with active settings. Merged.

**Channel Infrastructure**
- [#5055](https://github.com/HKUDS/nanobot/pull/5055) — Fixed Telegram markdown split hang on long single-line fenced code blocks. Merged.

**Document Processing & Sessions**
- [#5039](https://github.com/HKUDS/nanobot/pull/5039) — DOCX document parsing now preserves table content. Merged.
- [#5066](https://github.com/HKUDS/nanobot/pull/5066) — Stale exec sessions retained after cleanup failure for retry. Merged.
- [#5068](https://github.com/HKUDS/nanobot/pull/5068) — Session listing tolerates files removed during enumeration. Merged.

**Core Agent Fixes**
- [#5056](https://github.com/HKUDS/nanobot/pull/5056) — AgentRunner length recovery now preserves output across segments. Open.

## 4. Community Hot Topics

The most active discussions today were:

- **Issue #4253** ([link](https://github.com/HKUDS/nanobot/issues/4253)) — *"Support overriding model per conversation"* — 6 comments. This popular enhancement request (from June) seeks per-conversation model selection, allowing users to switch between fast online models and private local models depending on privacy/time needs. Closed today. This was a **long-running, high-impact feature request** that gained maintainer attention.

- **Issue #5059** ([link](https://github.com/HKUDS/nanobot/issues/5059)) — *"What browser versions are supported?"* — 4 comments. A Chinese-language user asking for explicit browser compatibility documentation. Closed quickly with likely a direct answer.

- **Issue #5028** ([link](https://github.com/HKUDS/nanobot/issues/5028)) — *"Media path and workspace restriction conflict"* — 1 comment. A Feishu integration bug where uploaded files in the `media` directory become inaccessible when `restrictToWorkspace` is on. Already partially addressed by PR #5065.

**Underlying need**: Users are demanding **greater model flexibility** (per-conversation model switching) and **clearer documentation** of supported environments. The workspace-vs-media path conflict is a recurring friction point for enterprise users with strict file access controls.

## 5. Bugs & Stability

**High Severity (P1)**
- **Issue #5062** ([link](https://github.com/HKUDS/nanobot/issues/5062)) — Test uses `python` command, fails on Debian/Ubuntu without `python-is-python3`. Fix PR [#5064](https://github.com/HKUDS/nanobot/pull/5064) open. **Quick fix available.**
- **Issue #5051** ([link](https://github.com/HKUDS/nanobot/issues/5051)) — `AgentRunner` length recovery loses earlier output segments; `final_content` only contains last continuation. Fix PR [#5056](https://github.com/HKUDS/nanobot/pull/5056) open.
- **Issue #4592** ([link](https://github.com/HKUDS/nanobot/issues/4592)) — ExecTool path extraction misses absolute paths after `=` sign. Already fixed by PR [#4594](https://github.com/HKUDS/nanobot/pull/4594) (merged).
- **Issue #4940** ([link](https://github.com/HKUDS/nanobot/issues/4940)) — Legacy session filenames lose `workspace_scope` on restart. Already fixed.

**Medium Severity**
- **Issue #5028** ([link](https://github.com/HKUDS/nanobot/issues/5028)) — Media directory access blocked by workspace restriction. Addressed by PR [#5065](https://github.com/HKUDS/nanobot/pull/5065).
- **Issue #5042** ([link](https://github.com/HKUDS/nanobot/pull/5042)) — Null cron schedule raises `TypeError`, dropping all sibling jobs. Fix PR open.

**Test Infrastructure**
- **Issue #5062** — Portability bug in test suite, already with a fix PR.

## 6. Feature Requests & Roadmap Signals

**Top user feature requests still open or recently closed:**
- **Per-conversation model override** (Issue #4253, closed) — Users want to switch models mid-conversation based on privacy/time. Now **merged into the model preset simplification** (PR #5061), likely landing in next release.
- **Browser version support documentation** (Issue #5059, closed) — Community requesting explicit compatibility matrix for WebUI.
- **Per-turn model fallback indication** (PR #5017, merged) — Already implemented; WebUI now shows fallback model in composer badge.

**Predictions for next release:**
- Model preset simplification (PR #5061) will be the headline feature.
- Length recovery preservation (PR #5056) will fix a critical truncation bug.
- Security hardening around `/restart`/`/stop` commands (PR #4889) and workspace path extraction (PR #4594) will ship.
- DOCX table support (PR #5039) and MCP schema normalization (PR #5057) will improve document handling and provider compatibility.

## 7. User Feedback Summary

**Pain points expressed:**
- *"I work mainly with two model presets... would like to alternate them"* — Per-conversation model switching was the most upvoted request (#4253, 6 comments).
- *"Uploaded files cannot be read when workspace restriction is enabled"* — Confusing access control for media files (#5028).
- *"On systems where only python3 is available... tests fail"* — Developer experience friction on Linux (#5062).
- *"Model output truncated; earlier segments lost"* — Length recovery is broken in production (#5051).

**Satisfaction signals:**
- Active community contributions (37 PRs updated today, many from first-time contributors like `flyzstu`, `martin1847`, `KDB-Wind`).
- Multiple Chinese-language contributors (`qteamo`, `KuruZaphkiel`, `cms19859230182-lang`) — indicating strong adoption in East Asian markets.

## 8. Backlog Watch

**Issues needing maintainer attention (open > 1 week, no maintainer response):**

- **Issue #4858** ([link](https://github.com/HKUDS/nanobot/issues/4858)) — *"Refactor dynamic tool provider lifecycle out of AgentLoop"* — Opened July 9, 1 comment. This P2 refactor request (about MCP tool lifecycle) has languished for 15 days. The author correctly identifies that MCP state is "leaking" into `AgentLoop` and proposes cleaner separation. Should be prioritized as MCP support expands.

**Open PRs with merge conflicts:**
- **PR #4987** ([link](https://github.com/HKUDS/nanobot/pull/4987)) — *"Fix(filesystem): bind workspace checks to opened files"* — Opened July 19, P0 priority, but marked with conflict. This is a security-critical PR (TOCTOU race in file access). Needs maintainer conflict resolution.
- **PR #5042** ([link](https://github.com/HKUDS/nanobot/pull/5042)) — *"Fix(cron): default null schedule when loading jobs.json"* — Marked with conflict. Important for cron reliability.
- **PR #5017** ([link](https://github.com/HKUDS/nanobot/pull/5017)) — Model fallback feature, already merged today. Resolved.

**Key observation**: No open issues older than 30 days remain unaddressed, indicating good maintainer responsiveness. The backlog is minimal.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-24

## Today's Overview

Hermes Agent is in a period of **high maintenance activity**, with 50 issues and 50 PRs updated in the last 24 hours. The project has 32 open/active issues and 34 open PRs, with 18 issues and 16 PRs resolved or merged today. A significant concentration of activity centers on **session state reliability** (session cost persistence, compression stability, MoA fault tolerance) and **Windows platform fixes** (console window flashes, WSLg compatibility, Git path resolution). The project is not shipping a new release today, but the volume of merged PRs suggests incremental stabilization is being actively prioritized over new features. Overall project health is **guarded** — high issue volume with several P1/P2 blockers open, but strong community engagement and rapid PR response.

## Releases

**No new releases today.** The latest available version remains v0.19.0 (2026.7.20) as noted in bug reports. Several open issues target gaps in the current release, including the Desktop SSH profile bug (#69551) and WebSocket reconnection issues in the Desktop GUI (#69930).

## Project Progress

**16 PRs merged/closed today.** Key advancements:

- **Windows platform stabilization (3 PRs merged):**
  - [#64339](https://github.com/NousResearch/hermes-agent/pull/64339) — Suppresses black console window flash when gateway spawns child processes on Windows (merged)
  - [#47971](https://github.com/NousResearch/hermes-agent/pull/47971) — Suppresses console-window flashes from gateway subprocesses + caches `nearest_root` (merged)
  - [#70264](https://github.com/NousResearch/hermes-agent/pull/70264) — Salvages remaining console flash fixes for `platform.win32_ver()`, env probes, and lazy installs (merged)

- **Anthropic provider fix** [#69512](https://github.com/NousResearch/hermes-agent/issues/69512) — Sanitizes empty/whitespace-only text blocks to prevent permanent HTTP 400 after compression (closed)

- **Gemini/MoA fix** [#65092](https://github.com/NousResearch/hermes-agent/issues/65092) — Missing `thought_signature` in Gemini aggregator MoA mode (closed)

- **Documentation** [#70389](https://github.com/NousResearch/hermes-agent/issues/70389) — Improved Setup Guide for WhatsApp platform (closed)

- **Auto-fix formatting** [#70417](https://github.com/NousResearch/hermes-agent/pull/70417) — Automated JS lint/formatting fix (merged)

## Community Hot Topics

**Most active issues (by comments):**

1. **[#67762 — Session cost resets on gateway restart](https://github.com/NousResearch/hermes-agent/issues/67762)** (6 comments, P2 bug) — `agent.session_estimated_cost_usd` not rehydrated from SQLite when gateway restarts mid-session. Blocking any feature displaying running session cost. **Underlying need:** Users need accurate, persistent billing telemetry across gateway restarts.

2. **[#30640 — RFC: Cursor SDK integration](https://github.com/NousResearch/hermes-agent/issues/30640)** (6 comments, P3 feature, closed) — Proposal to add Cursor Agent SDK support in two phases: bounded coding delegation via `cursor_agent` tool, and optional integration bridge. **Underlying need:** Power users want Hermes to delegate complex IDE-native coding tasks to Cursor while keeping Hermes as the orchestrator.

3. **[#70294 — Cron delegate_task results silently dropped](https://github.com/NousResearch/hermes-agent/issues/70294)** (6 comments, P2 bug) — When model calls `delegate_task` inside a cron job, delegation results are dropped while job reports `last_status: ok`. **Underlying need:** Scheduled automations must reliably propagate subagent outputs.

4. **[#513 — Two-phase context management](https://github.com/NousResearch/hermes-agent/issues/513)** (5 comments, P3 feature, closed) — Inspired by Kilocode: prune tool outputs before full compaction to reduce costs and improve compression quality. **Underlying need:** Users want cheaper, smarter context management that doesn't interrupt conversation flow.

## Bugs & Stability

**Critical/High-severity bugs reported today:**

| Issue | Severity | Summary | Fix PR? |
|-------|----------|---------|---------|
| [#67762](https://github.com/NousResearch/hermes-agent/issues/67762) | **BLOCKER** (P2) | Session cost resets to $0 on gateway restart — breaks billing display | No |
| [#70294](https://github.com/NousResearch/hermes-agent/issues/70294) | **HIGH** (P2) | Cron `delegate_task` results silently dropped | No |
| [#70328](https://github.com/NousResearch/hermes-agent/issues/70328) | **HIGH** (P2) | Images priced flat at 1500 tokens, causing provider 400s before compaction can fire on vision-heavy sessions | No |
| [#14694](https://github.com/NousResearch/hermes-agent/issues/14694) | **HIGH** (P1) | Anti-thrashing protection permanently disables auto-compression with no recovery | No |
| [#70411](https://github.com/NousResearch/hermes-agent/issues/70411) | **MEDIUM** (P3) | Hermes Desktop `git-review` errors on Windows — wrong Git bin path | No |
| [#70422](https://github.com/NousResearch/hermes-agent/issues/70422) | **LOW** (P3) | Desktop composer accidental drag/pop-out when selecting text | No |
| [#70424](https://github.com/NousResearch/hermes-agent/issues/70424) | **LOW** (P3) | Desktop: clicking chat session from Kanban/Artifacts does not return to chat | No |

**Notable regressions:** The session cost rehydration issue (#67762) is particularly concerning as it undermines billing accuracy for enterprise users. The vision image token pricing bug (#70328) impacts users on 64K local models who encounter provider errors before compression can help — a critical path failure for self-hosted deployments.

**New fix PRs submitted today** addressing open bugs:
- [#70412](https://github.com/NousResearch/hermes-agent/pull/70412) (P1) — Breaks unbounded 401 retry loop in credential pool OAuth path
- [#70413](https://github.com/NousResearch/hermes-agent/pull/70413) (P2) — MCP: skip dynamic tool refresh when session is closed or superseded
- [#70415](https://github.com/NousResearch/hermes-agent/pull/70415) (P3) — Approval: recognize raw temp-dir alias in verification cleanup
- [#70416](https://github.com/NousResearch/hermes-agent/pull/70416) (P3) — Gemini: bump native provider aux default to `gemini-3.6-flash`
- [#70418](https://github.com/NousResearch/hermes-agent/pull/70418) — Bootstrap installer: quote `$UV_CMD` for paths with spaces
- [#70419](https://github.com/NousResearch/hermes-agent/pull/70419) — Desktop: fall through to create when branch draft resume fails
- [#70420](https://github.com/NousResearch/hermes-agent/pull/70420) — Feishu: fail-closed approval card operator authorization
- [#70425](https://github.com/NousResearch/hermes-agent/pull/70425) — Providers: classify code-only failover errors

## Feature Requests & Roadmap Signals

**Most notable feature signals from today's issues:**

1. **[#70423](https://github.com/NousResearch/hermes-agent/issues/70423) — Show target project when clicking New session** (Desktop parity with Claude macOS) — User requests instant project/workspace confirmation before starting a new chat. *Likely for next patch release (v0.19.1) given it's a small UI enhancement.*

2. **[#70421](https://github.com/NousResearch/hermes-agent/issues/70421) — Show all chats under a project (remove 3-session preview cap)** — Users in multi-project setups find the 3-session cap in sidebar obstructive. *Probably v0.20.0 given scope.*

3. **[#59363](https://github.com/NousResearch/hermes-agent/issues/59363) — Add idle time-gap pre-compression** (closed, P3) — Compress stale sessions near limit before user returns. *Valuable UX improvement for long-running gateway sessions.*

4. **[#30640](https://github.com/NousResearch/hermes-agent/issues/30640) — Cursor SDK integration** (closed, P3) — Two-phase proposal for IDE-native coding delegation. *Likely being evaluated for v0.20.0 planning.*

**Roadmap prediction:** The next minor release (v0.19.1) will likely focus on:
- Session state persistence fixes (#67762, #70294)
- Windows platform stabilization (PRs merged today)
- Desktop UI paper cuts (#70422, #70423, #70424)

The next major release (v0.20.0) may include:
- Two-phase context management (#513)
- Cursor SDK integration (#30640)
- MoA fault tolerance improvements (#70281, still open as PR)
- Comprehensive streaming for WeCom (#41771, still open as PR)

## User Feedback Summary

**Pain points (high frequency):**

- **Session state unreliability** — Multiple reports of session cost not persisting across restarts (#67762), cron delegate results dropping (#70294), and context compression failing to recover (#14694). These are confidence-eroding for users relying on Hermes for production automation.
- **Windows experience gaps** — Console window flashes (#64339, #67690, #47971), Git binary path errors (#70411), and missing window controls on WSLg (#70400) indicate Windows remains a second-class platform.
- **Desktop GUI friction** — Users report confusing navigation (Kanban/Artifacts trapping users away from chat, #70424), accidental composer drag/pop-out (#70422), and unclear project targeting when creating new sessions (#70423).
- **MoA provider confusion** — `hermes doctor` incorrectly reporting `moa` as unrecognized (#58759) forces users to dig into internals to understand valid configurations.

**Positive signals:**

- Strong community engagement: 50 issues + 50 PRs updated in 24h indicates a healthy, active contributor base.
- Quick fix turnaround: Multiple PRs submitted on the same day bugs were reported (e.g., #70412 fixes #70401 same day).
- Multi-platform enthusiasm: Users actively testing on Windows, macOS, WSLg, and SSH remote modes indicate broad adoption.

## Backlog Watch

**Long-unanswered issues needing maintainer attention:**

| Issue | Age | Summary | Last Update |
|-------|-----|---------|-------------|
| [#30640](https://github.com/NousResearch/hermes-agent/issues/30640) | **63 days** | RFC: Cursor SDK integration (6 comments, closed) — No maintainer response evident | 2026-07-23 |
| [#64488](https://github.com/NousResearch/hermes-agent/issues/64488) | **10 days** | Dashboard TUI sessions leak processes, memory, and DB rows (P2, 4 comments) | 2026-07-23 |
| [#50101](https://github.com/NousResearch/hermes-agent/issues/50101) | **33 days** | `mnemosyne_diagnose` reports `fastembed` MISSING despite successful install (P3, 1 comment) | 2026-07-24 |
| [#47359](https://github.com/NousResearch/hermes-agent/issues/47359) | **38 days** | Desktop: backend update reports failure even when update succeeds (P3, 2 comments) | 2026-07-24 |
| [#61003](https://github.com/NousResearch/hermes-agent/issues/61003) | **16 days** | `shutdown_forensics`: false-positive "Stale systemd unit" warning (P3, 1 comment) | 2026-07-24 |

**PRs needing attention:**

| PR | Age | Summary | Last Update |
|----|-----|---------|-------------|
| [#37980](https://github.com/NousResearch/hermes-agent/pull/37980) | **51 days** | feat: add `--warm` flag to skip cold start via Gateway API Server (P3) | 2026-07-24 |
| [#41771](https://github.com/NousResearch/hermes-agent/pull/41771) | **46 days** | feat(wecom): native reply streaming (P3) | 2026-07-24 |
| [#57113](https://github.com/NousResearch/hermes-agent/pull/57113) | **22 days** | fix(billing): improve model pricing coverage and cache token accounting (P2) | 2026-07-24 |

The `--warm` flag PR (#37980) and native WeCom streaming PR (#41771) have been open for over 45 days with no reviewer activity — these represent substantial community contributions that may be at risk of stalling without maintainer attention.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-24

## Today's Overview
PicoClaw shows moderate activity with 15 PRs updated in the last 24 hours, split evenly between open (8) and merged/closed (7) items. One stale bug issue was closed. No new releases occurred today. The project appears to be in a maintenance phase with heavy dependency updates (10 of 15 PRs are Dependabot-driven), but meaningful feature work continues with a refactoring of the DeltaChat module and a new configurable model fallback chain nearing completion. The lone closed bug—an OpenAI GPT integration issue on NanoKVM—was resolved (likely stale-closed), suggesting some user-facing issues may lack active debugging.

## Releases
No new releases today. The latest release remains unknown from this data window.

## Project Progress
Seven PRs were merged or closed in the last 24 hours:
- **#3286** *(fix: update Go and x/text for govulncheck)* — merged. A security/bug fix addressing Go vulnerability scanner findings, updating Go version and `x/text` dependencies. Author: imguoguo.
- **#3118** *(Add remote Pico WebSocket mode to picoclaw agent)* — closed/stale. Proposed a new `--remote` flag for the agent command to connect via WebSocket. Stale-closed without merge.
- **#3115** *(Fix inline data URL media extraction for generic tool output)* — closed/stale. Fixed a session-history corruption bug where `data:image/...;base64` strings in tool output (e.g., from `read_file`, `exec`) were incorrectly treated as media attachments. Stale-closed without merge.
- **#3237, #3236, #3238, #3235** — four dependency bump PRs from Dependabot (Go sync, Copilot SDK, AWS config, Pion RTP) closed as stale, likely superseded by newer bumps (#3291, #3290, #3289, #3288).

**Key takeaway**: Two substantial feature/fix PRs (#3118 and #3115) were closed as stale without merging, which may indicate review bottlenecks or shifting priorities.

## Community Hot Topics
The most active item today is a single closed issue:
- **#3195** [CLOSED] *OpenAI GPT does not work on NanoKVM with default config* (4 comments) — User rtadams89 reported that PicoClaw on NanoKVM 2.4.0 fails to work with gpt-5.4 despite following official docs. No 👍 reactions. The issue was closed as stale on 2026-07-23 after 23 days without resolution, suggesting either a workaround was found or the report was abandoned.  
  *URL*: [sipeed/picoclaw Issue #3195](https://github.com/sipeed/picoclaw/issues/3195)

No other issues or PRs have meaningful comments or reactions in this window. The lack of community engagement beyond this single bug report may reflect a quiet period or a user base that primarily interacts elsewhere.

## Bugs & Stability
One bug was addressed in the last 24 hours:
- **#3286** *(fix: update Go and x/text for govulncheck)* — **Merged**. Severity: Medium. Fixes Go vulnerability scanner (govulncheck) findings by updating Go and `x/text` dependencies. This is a proactive security/stability fix rather than a user-facing regression.

**Stale bug of concern**: Issue #3195 (OpenAI GPT on NanoKVM) remains unresolved—closed due to staleness, not a verified fix. If this is a real compatibility issue with NanoKVM 2.4.0, it may resurface. Consider re-opening or documenting a known limitation.

No new bugs, crashes, or regressions were reported today.

## Feature Requests & Roadmap Signals
Two significant feature PRs are still open and progressing:
- **#3200** *(feat(models): add configurable default fallback chain)* — **Open**. PR by lc6464 (created 2026-07-01, last updated 2026-07-23). Adds a UI and backend API for configuring a default fallback chain for models. This enables users to set a primary model, add fallbacks, reorder, and persist the chain. Likely candidate for the next minor release.  
  *URL*: [sipeed/picoclaw PR #3200](https://github.com/sipeed/picoclaw/pull/3200)
- **#3222** *(refactor(deltachat): cleanup implementation, documentation -200LOC)* — **Open**. PR by trufae (created 2026-07-03, last updated 2026-07-23). Drops legacy features, removes hardcoded relay list, eliminates password-based email config, renames `invite_link` → `join_invite_link`, adds `show_invite_link`, and adds full DeltaChat documentation. Net -200 LOC.  
  *URL*: [sipeed/picoclaw PR #3222](https://github.com/sipeed/picoclaw/pull/3222)

**Prediction**: #3200 (fallback chain) is likely the next major UI feature to ship, as it has been actively updated. #3222 (DeltaChat refactor) is a maintenance improvement that may merge alongside.

## User Feedback Summary
Minimal direct user feedback in this window. The lone issue (#3195) reveals a pain point:
- **NanoKVM + OpenAI compatibility**: User attempted to use gpt-5.4 on a NanoKVM device following official docs but encountered failures. The issue was closed without a clear resolution. This suggests either:
  - Documentation may be incomplete for NanoKVM-specific setup.
  - There is an undiscovered incompatibility between PicoClaw's default config and NanoKVM's environment.
  
No positive feedback or feature praise was captured in this window.

## Backlog Watch
Several open PRs need attention:
- **#3263** & **#3262** *(actions/setup-node 6→7, actions/setup-go 6→7)* — Both stale (labeled `stale`), last updated 2026-07-23. These are CI dependency bumps that are low risk but have been waiting 8 days. Likely need manual review or stale-closure.
- **#3291, #3290, #3289, #3288** — Four fresh Dependabot PRs created today (2026-07-23) bumping Copilot SDK, AWS config, Pion RTP, and Bedrock Runtime. These are the latest versions superseding the now-closed stale ones. Maintainers should review promptly to prevent another accumulation of stale bumps.

**No long-unanswered issues** were identified in this window—the only issue (#3195) was closed. However, the fact that two significant feature/fix PRs (#3118, #3115) were stale-closed without merge suggests a potential backlog of unaddressed community contributions.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-24

## 1. Today's Overview
NanoClaw is experiencing a surge in maintenance activity, with **10 PRs updated in 24 hours** (6 open, 4 merged/closed) and **1 open bug issue** receiving recent attention. The project shows healthy parallel work across three core areas: **container runtime stability** (duplicate spawn prevention, orphan reconciliation), **messaging reliability** (typing indicators, reaction delivery), and **platform compatibility** (Matrix E2EE, Telegram threads, Gmail API blocks). There are no new releases today, but the high PR velocity suggests a stabilization sprint is underway following recent feature work.

## 2. Releases
**No new releases.** The `Latest Releases` section shows no entries. The project may be in a pre-release stabilization phase given the number of open fix PRs.

## 3. Project Progress
Four PRs were merged or closed today:

- **PR #2892** `fix(telegram): enable thread support` (by @avri-schneider, closed) — Sets `supportsThreads: true` for Telegram adapter, enabling forum/topic thread tracking. The bridge already threaded `message_thread_id`; this flips the capability flag. [Link](https://github.com/nanocoai/nanoclaw/pull/2892)

- **PR #2844** `feat(matrix): native persistent E2EE adapter via matrix-bot-sdk` (by @avri-schneider, closed) — Major rewrite replacing the `@beeper/chat-adapter-matrix` bridge with a native `matrix-bot-sdk` + Rust crypto binding (`@matrix-org/matrix-sdk-crypto-nodejs`). Addresses WASM crypto limitations of previous approach. [Link](https://github.com/nanocoai/nanoclaw/pull/2844)

- **PR #3120** `Keep typing indicator alive through a single long tool call` (by @vlsmt, closed) — Prevents typing indicator from timing out during extended single tool execution, improving user feedback during long-running operations. [Link](https://github.com/nanocoai/nanoclaw/pull/3120)

- **PR #3115** `fix(onecli): block legacy Gmail API routes` (by @Koshkoshinsk, closed) — Adds idempotent Gmail traffic blocks for legacy paths (`www.googleapis.com`, batch, upload) to prevent bypass of `gmail.googleapis.com` policies, with verification and reconciliation docs. [Link](https://github.com/nanocoai/nanoclaw/pull/3115)

## 4. Community Hot Topics
**Most active:**
- **Issue #2466** `Duplicate container spawn race on wakeContainer` — 2 comments, last updated yesterday. [Link](https://github.com/nanocoai/nanoclaw/issues/2466)
  - Root cause analysis: concurrent `scripts/inject-gamma-brief.ts` and host `*/15` sweep cause dual container spawns for same agent group.
  - The community is engaged because a fix PR (#3119, see Bugs & Stability) directly addresses this.

- **PR #3122** `fix(opencode): main compatibility, custom-endpoint transport, memory parity` (by @glifocat, open) — Large PR updating OpenCode integration for main branch compatibility. [Link](https://github.com/nanocoai/nanoclaw/pull/3122)

- **PR #2971** `Add ncc utility skill: host operational and health CLI` (by @zivisaiah, open) — New CLI tool for host operations and health checks. [Link](https://github.com/nanocoai/nanoclaw/pull/2971)

**Underlying needs:** The community is prioritizing **operational stability** (duplicate container prevention, typing feedback) and **broadening platform support** (Matrix E2EE, Telegram threads, OpenCode compatibility).

## 5. Bugs & Stability
**Active Bugs (ranked by severity):**

1. **HIGH — Duplicate container spawn race (Issue #2466)**: Core race condition where concurrent `wakeContainer` calls spawn duplicate containers for same agent group. A fix PR **#3119** is open (by @robbyczgw-cla) that reconciles untracked orphan containers. This is the most impactful stability issue today.
   - Issue: [Link](https://github.com/nanocoai/nanoclaw/issues/2466)
   - Fix PR: [Link](https://github.com/nanocoai/nanoclaw/pull/3119)

2. **MEDIUM — Unknown slash commands dropped (PR #2346, open)**: Unknown slash commands were classified as `passthrough`, causing Agent SDK to produce invalid responses. Fix changes categorization to `'none'`.
   - PR (fix): [Link](https://github.com/nanocoai/nanoclaw/pull/2346)

3. **LOW — Reaction delivery failures (PR #3121, open)**: Proposal to make reaction delivery best-effort to prevent failures from blocking message flow.
   - PR: [Link](https://github.com/nanocoai/nanoclaw/pull/3121)

4. **LOW — Typing indicator timeout (PR #3120, closed)**: Fixed bug where long single tool calls caused typing indicator to disappear. Already merged.

5. **LOW — Gmail legacy route bypass (PR #3115, closed)**: Legacy Gmail API paths could bypass blocks. Already merged with verification.

## 6. Feature Requests & Roadmap Signals
**Notable feature signals from today's PRs:**

- **Matrix native E2EE (PR #2844, merged)** — Major signaling that NanoClaw is investing in secure, persistent messaging for decentralized platforms. Likely foundational for future Matrix-based multi-agent collaborations.

- **OpenCode main compatibility (PR #3122, open)** — Suggests upcoming support for OpenCode's latest transport layer and memory system, important for extensibility.

- **Host operational CLI (PR #2971, open)** — Indicates user demand for better operator tooling, likely for production deployments and troubleshooting.

**Prediction for next version:**
- Container runtime hardening (reconciling orphans, preventing race conditions)
- Matrix E2EE by default (replacing WASM crypto bridge)
- Improved Telegram support (threads, typing indicators)
- Host management CLI for operators

## 7. User Feedback Summary
**Pain points addressed today:**
- Duplicate container spawning on long-running hosts (5d uptime, 3 concurrent containers for one agent) — users need reliable single-container-per-group behavior
- Typing indicator disappearing during long tool calls — users want accurate real-time feedback
- Legacy Gmail route bypass — users with Gmail integrations need reliable blocking
- Telegram forum/thread tracking — users want structured conversations preserved
- Matrix WASM crypto limitations — users need persistent E2EE that survives restarts

**Satisfaction signals:** High contributor activity (4 closed PRs, 6 open) suggests the community is actively engaged and maintainers are responsive to reported issues.

**Dissatisfaction signals:** The duplicate container bug persisted for over 2 months (Issue #2466 opened 2026-05-14) before a fix PR emerged, indicating possible friction in prioritizing stability bugs over features.

## 8. Backlog Watch
**Oldest open issue needing attention:**
- **Issue #2466** `Duplicate container spawn race` — Open since **2026-05-14** (71 days), finally has a fix PR (#3119) open as of today. Was the longest-unresolved stability issue. [Issue Link](https://github.com/nanocoai/nanoclaw/issues/2466)

**Oldest open PR needing attention:**
- **PR #2346** `fix(formatter): treat unknown slash commands as normal chat` — Open since **2026-05-08** (77 days). No maintainer comments or activity beyond last update. This fix prevents silent message drops for unknown commands, making it a significant UX bug. [PR Link](https://github.com/nanocoai/nanoclaw/pull/2346)

**Recommendation:** The maintainers should prioritize reviewing PR #2346 given its age and the fact it fixes a bug that causes user messages to be silently discarded.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-24

## Today's Overview

IronClaw is in an intense **pre-launch stabilization phase**, with 50 PRs and 32 Issues updated in the last 24 hours, reflecting a project at peak velocity toward a v1 launch. The team is simultaneously addressing critical live-incident bugs (Telegram silent death, WebChat disconnection lockout, Windows serve failures), executing a major architectural cleanup (retiring legacy extension sources, renaming internal Reborn crates to neutral IronClaw names), and expanding testing coverage (hermetic E2E migration, heartbeat scheduling MVP). Two v1-launch-checklist epic tracks dominate activity: **hosted deployment operability** (Slack/Telegram/Google OAuth config persistence, CLI availability on staging) and **extension lifecycle correctness** (PR #6520 merged, fixing channel delivery after uninstall). The project shows strong discipline—every merged PR includes hermetic test reconciliation, and a daily failure taxonomy (Issue #6572) is being tracked openly.

## Releases

No new releases today. The last release candidate (`1.0.0-rc.1`) is still active. A release PR (#5598) remains open, proposing breaking changes to `ironclaw_common` (v0.4.2→0.5.0) and `ironclaw_skills` (v0.3.0→v0.4.0), but has not been merged.

## Project Progress

**Merged/Closed PRs (17 total):**

| PR | Description | Impact |
|---|---|---|
| [#6603](https://github.com/nearai/ironclaw/pull/6603) | [CLOSED] Test reconciliation after #6520 merge | Fixed 3 Playwright shards red on main; surfaced 2 product defects |
| [#6602](https://github.com/nearai/ironclaw/pull/6602) | [CLOSED] Fix live-QA Slack bootstrap (422 error) | Unblocked 8 Slack-dependent QA shards |
| [#6601](https://github.com/nearai/ironclaw/pull/6601) | [CLOSED] Admin-config-preserving extension reset script | Safe state-reset tool for operators |
| [#6594](https://github.com/nearai/ironclaw/pull/6594) | [CLOSED] Retire legacy extension sources | Removed `tools-src/` and `channels-src/` trees |
| [#6592](https://github.com/nearai/ironclaw/pull/6592) | [CLOSED] Fix WebChat 'Disconnected' lockout | Rate-limit budget fix + navigation-race SSE thrash fix |
| [#6520](https://github.com/nearai/ironclaw/pull/6520) | [CLOSED] Fix extension readiness & channel delivery | Collapsed extension lifecycle to 3 states; separated admin vs. user config |
| [#6543](https://github.com/nearai/ironclaw/pull/6543) | [CLOSED] Move ProductSurface contract to host_api | Collapsed product crates into `ironclaw_product` |
| [#6582](https://github.com/nearai/ironclaw/pull/6582) | [CLOSED] Dummy PR to verify /benchmark canary | Fixed silent benchmarking infrastructure failure |

**Key Feature Advances (Open PRs):**
- [#6604](https://github.com/nearai/ironclaw/pull/6604) — Fix for Telegram delivery failure after extension uninstall (live incident fix)
- [#6559](https://github.com/nearai/ironclaw/pull/6559) — Make `IRONCLAW_*` environment variables canonical (neutral names replacing `IRONCLAW_REBORN_*`)
- [#6597](https://github.com/nearai/ironclaw/pull/6597) — Instruct model to review available skills before answering (skill routing improvement)
- [#6599](https://github.com/nearai/ironclaw/pull/6599) — Hermetic E2E test for scheduled trigger delivery (Trigger → Run → Slack DM)
- [#6598](https://github.com/nearai/ironclaw/pull/6598) — Rename `Filesystem*Store` types to plain `*Store` names

## Community Hot Topics

### Most Active Issue
**[#6389](https://github.com/nearai/ironclaw/issues/6389) — Phase 4: collapse build_local_runtime + build_production_shaped into one build_runtime(cfg)**
- 11 comments, closed. Architectural simplification of the runtime assembly paths in `factory.rs`. The high comment count reflects deep technical discussion about merging two long diverged code paths into a single backend-parameterized function—a classic sign of the team prioritizing maintainability over feature velocity.

### Most Active PRs (all from core team)
- **[#6604](https://github.com/nearai/ironclaw/pull/6604)** — Fix: Telegram silent death after extension uninstall (live incident, opened today)
- **[#6606](https://github.com/nearai/ironclaw/pull/6606)** — Fix: Map setup values onto declared admin-group handles (Slack QA shard fix)
- **[#6520](https://github.com/nearai/ironclaw/pull/6520)** — Extension lifecycle redesign (XL, 62 files changed, closed after 2 days)

### Underlying Needs
The community and QA team are intensely focused on **hosted deployment reliability** for multi-channel agents (Slack, Telegram, WebChat). The recurring pattern: integration channels fail in subtle ways under real-world conditions (webhook delivery through auth walls, silent config persistence failures, mid-run channel removal). These are not theoretical—they block the v1 launch.

## Bugs & Stability

### Critical (blocking v1 launch)
1. **Telegram inbound silently dead after extension reinstall** — [#6605](https://github.com/nearai/ironclaw/issues/6605)  
   If Telegram is reinstalled without full setup, `telegram_webhook_secret` is missing. Fix ongoing via [#6604](https://github.com/nearai/ironclaw/pull/6604).
   
2. **WebChat 'Disconnected' lockout under normal usage** — [#6581](https://github.com/nearai/ironclaw/issues/6581) (429 Too Many Requests on SSE)  
   **Fix landed today** via [#6592](https://github.com/nearai/ironclaw/pull/6592) (rate-limit + navigation-race fix).

3. **WebUI constantly reconnecting** — [#6541](https://github.com/nearai/ironclaw/issues/6541)  
   Persistent confusing UI feedback. Likely related to the SSE issue above.

4. **Hosted staging auth wall blocks webhook delivery** — [#6548](https://github.com/nearai/ironclaw/issues/6548) (Telegram, Slack)  
   Preview-auth middleware intercepts webhook callbacks before reaching IronClaw.

5. **Windows serve fails: workspace root overlap** — [#6590](https://github.com/nearai/ironclaw/issues/6590)  
   Path validation prevents `ironclaw serve` on Windows. No fix PR yet.

### High Severity
6. **Agent creation fails when testing flag is set** — [#6523](https://github.com/nearai/ironclaw/issues/6523)  
   During onboarding with "test build" flag selected.

7. **Google OAuth config can't be applied in hosted deployments** — [#6534](https://github.com/nearai/ironclaw/issues/6534)  
   Config saves locally but not on hosted staging; team attributes to environment isolation issue.

8. **`systemd` service error after `ironclaw onboard`** — [#6575](https://github.com/nearai/ironclaw/issues/6575)  
   Post-onboard `systemctl status` fails (Ubuntu).

### Medium Severity
9. **CLI unavailable on agent staging** — [#6521](https://github.com/nearai/ironclaw/issues/6521)  
   `ironclaw` not in PATH on hosted VMs; restart requires UI workaround.

10. **Duplicate `model` field in DeepSeek requests** — [#4548](https://github.com/nearai/ironclaw/issues/4548)  
    Open since June 2026; impacts DeepSeek 400 error when using tools.

### Stability Assessment
The daily failure taxonomy [#6572](https://github.com/nearai/ironclaw/issues/6572) reports **77 non-passing clawbench tests**, dominated by model shortfalls (partial-credit). The team is actively migrating from legacy E2E infrastructure to IronClaw-native hermetic tests (tracked by [#6560](https://github.com/nearai/ironclaw/issues/6560), [#6561](https://github.com/nearai/ironclaw/issues/6561), [#6562](https://github.com/nearai/ironclaw/issues/6562)).

## Feature Requests & Roadmap Signals

### Strong Signals (likely next release)
- **Heartbeat scheduling MVP** — Issues [#6569](https://github.com/nearai/ironclaw/issues/6569), [#6570](https://github.com/nearai/ironclaw/issues/6570), [#6571](https://github.com/nearai/ironclaw/issues/6571) define the contract, implementation, and delivery suppression for periodic heartbeats through the existing trigger pipeline. This is clearly on the near-term roadmap.
- **Canonical IronClaw configuration** — PR [#6559](https://github.com/nearai/ironclaw/pull/6559) and Issue [#6551](https://github.com/nearai/ironclaw/issues/6551) push to rename `IRONCLAW_REBORN_*` → `IRONCLAW_*` and `~/.ironclaw` as default home. This is a deliberate branding/architecture step pre-launch.
- **Renaming Reborn codename from internal architecture** — Issue [#6552](https://github.com/nearai/ironclaw/issues/6552) proposes removing the "Reborn" codename from crates, types, and docs after establishing a compatibility layer. This signals readiness to treat previous architecture phases as legacy.

### Early Signals (next 1-2 releases)
- **Admin-Managed Agents as UserId Subjects** — Epic [#6578](https://github.com/nearai/ironclaw/issues/6578) proposes tenant-admin-created non-human subjects for product agents, automations, and integrations. This would enable multi-tenant SaaS deployment with identity isolation.
- **Reliable Skill Discovery, Routing, and Activation** — Epic [#6565](https://github.com/nearai/ironclaw/issues/6565) targets making skill selection less model-directed and more deterministic. PR [#6597](https://github.com/nearai/ironclaw/pull/6597) (instruct model to review available skills) is the first concrete step.
- **Hermetic Capability and Journey Testing Platform** — Epic [#6524](https://github.com/nearai/ironclaw/issues/6524) aims to mechanically verify every supported capability has deterministic coverage. Indicates the team wants testing to be as rigorous as production code.

### Less Likely (v1+)
- **Telegram setup instructions** — Issue [#6522](https://github.com/nearai/ironclaw/issues/6522) requests user-facing documentation for Telegram configuration (blocked by v1 launch).

## User Feedback Summary

### Real Pain Points (from v1-launch-checklist issues)
1. **"I cannot complete Slack/Telegram/Google OAuth setup reliably"** — Users face 503 errors (redirect URI not saved, Issue [#6544](https://github.com/nearai/ironclaw/issues/6544)), 422 errors (wrong config format, fixed in [#6602](https://github.com/nearai/ironclaw/pull/6602)), and 400 errors (bare setup-source names, fixed in [#6606](https://github.com/nearai/ironclaw/pull/6606)).
2. **"The agent appears to work but keeps showing 'Reconnecting'"** — Confusing UI that undermines user confidence even when functionality is intact (Issues [#6541](https://github.com/nearai/ironclaw/issues/6541), [#6581](https://github.com/nearai/ironclaw/issues/6581)).
3. **"I can't restart the agent from the command line on hosted staging"** — `ironclaw` CLI not available, forcing users to use a web UI workaround (Issues [#6521](https://github.com/nearai/ironclaw/issues/6521), [#6591](https://github.com/nearai/ironclaw/issues/6591)).
4. **"Creating a new agent fails if I check 'test build'"** — Onboarding regression blocking evaluation of new builds (Issue [#6523](https://github.com/nearai/ironclaw/issues/6523)).

### Satisfaction/Needs
- **Strong focus on deterministic testing** — The team's openness about failure taxonomy and systematic E2E migration (Issues [#6560](https://github.com/nearai/ironclaw/issues/6560)–[#6562](https://github.com/nearai/ironclaw/issues/6562)) signals a culture that values reliability over speed.
- **No visible frustration in community** — All issues are filed with clear reproduction steps and expected behaviors. The QA team (sergeiest, thisisjoshford, joe-rlo) is methodically filing blockers, not complaints.

## Backlog Watch

### Long-Open Items Needing Maintainer Attention
- **[#4548](https://github.com/nearai/ironclaw/issues/4548) — DeepSeek duplicate `model` field (Open since June 8)** — This bug has been open for 46 days and breaks all tool-using requests to DeepSeek. Despite being lower priority than v1 blockers, it affects a meaningful subset of users and could become a support headache post-launch.
- **[#5598](https://github.com/nearai/ironclaw/pull/5598) — Release PR with breaking changes (Open since July 3)** — Proposes breaking changes to `ironclaw_common` and `ironclaw_skills`. The PR is 21 days old with no recent activity. The team may be waiting until after v1 launch to land breaking changes, but the drift from `main` is growing.
- **[#3997](https://github.com/nearai/ironclaw/pull/3997) — Attested-signing (PR13, Open since May 24)** — This large PR stack was re-ported onto current main after 1184 commits of drift. A companion PR [#4015](https://github.com/nearai/ironclaw/pull/4015) (PR14) is also open. The signing infrastructure is a major feature but appears to be blocked behind v1 launch priorities.

### Stale Items
- **[#6428](https://github.com/nearai/ironclaw/pull/6428) — tokio-ecosystem deps bump (Open since July 21)** — Risk: low, but 4 dependencies are now outdated.
- **[#6361](https://github.com/nearai/ironclaw/pull/6361) — serialization deps bump (Open since July 20)** — Updated serde and serde_json. Dependabot PRs are piling up, suggesting the team is intentionally deferring minor dep updates.

---

*Digest generated from IronClaw GitHub data snapshot, 2026-07-24 23:59 UTC.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-24**.

---

## LobsterAI Project Digest — 2026-07-24

### 1. Today's Overview
Project activity is low, with no new releases or merges today. Three stale issues remain open without resolution, indicating a potential backlog in triage. The only closed PRs (#2379, #2378) were merged yesterday (2026-07-23), pushing through a minor release (2026.7.20) and a UI polish for the "AI Skin" feature. A single open PR (#1277) is a routine dependency bump by Dependabot. Overall, the project is in a maintenance phase with underlying concerns about database stability and scaling multi-agent configurations.

### 2. Releases
**None.** No new releases were published in the last 24 hours. The latest release remains the **2026.7.20** build merged yesterday.

### 3. Project Progress
Two PRs were **closed/merged** yesterday (2026-07-23), advancing the codebase:
- **PR #2379** (merged) — Release/2026.7.20: A comprehensive release touching the renderer, build, docs, main, OpenClaw, Cowork, Windows platform, and artifacts areas.
- **PR #2378** (merged) — feat(skin): Polish AI skin appearance behavior: This PR aligns artifact add-tab and task-search surfaces with the AI skin presentation, enforces mutual exclusivity between standard themes and AI skins, and simplifies the AI skin settings flow.

### 4. Community Hot Topics
The three currently open issues have all been idle for months, yet remain the focus of community attention:
- **#1263** — [Bug] Duplicate scheduled tasks showing "API rate limit exceeded". The user reports that the UI shows two identical tasks and that only one session exists on the backend. *Root cause: Likely a race condition in task scheduling/dedup logic.*
- **#1265** — [Feature Request] Bind different IM bots and models to different agents. The user (neoliuhua) argues for per-agent model/bot binding to enable agent specialization (e.g., a dispatcher vs. a slide generator). *This is the most strategically significant request for multi-agent orchestration.*
- **#1273** — [Bug] `sql.js` (WASM) memory access out of bounds crash + database corruption risk. The reporter describes fatal crashes under high-frequency writes (Cowork sessions), and notes `save()` uses non-atomic `fs.writeFileSync`. *This is a critical stability concern.*

### 5. Bugs & Stability
| Issue | Severity | Summary | Fix PR exists? |
|-------|----------|---------|----------------|
| #1273 | **Critical** | WASM memory access out of bounds + risk of permanent DB corruption under high write load | No PR identified |
| #1263 | **Medium** | Duplicate scheduled tasks causing recurring API rate limit errors | No PR identified |

The **#1273** sql.js crash is the highest priority bug due to data loss potential. No fix PRs or maintainer responses are visible on any of these issues.

### 6. Feature Requests & Roadmap Signals
- **Agent→IM/Model binding (Issue #1265):** This is the strongest roadmap signal. If implemented, it would unlock true agent specialization (e.g., coding vs. reasoning models), making LobsterAI suitable for production multi-agent teams.
- **AI Skin polish (PR #2378, merged):** The team is actively investing in user-facing customization (skins vs. themes), suggesting a near-term focus on UX improvements over backend stability.

### 7. User Feedback Summary
- **Pain point: Scheduled task duplication (Issue #1263).** Users are frustrated by ghost tasks that cannot be removed, compounded by uninformative API rate-limit errors.
- **Use case: Multi-agent orchestration (Issue #1265).** A clear demand for heterogeneous agents—different models (e.g., GPT-4 for reasoning, Claude for writing) and different IM integrations—is emerging.
- **Dissatisfaction: Database fragility (Issue #1273).** The sql.js crash is a stability blocker for power users running long Cowork sessions. No acknowledgment from maintainers increases uncertainty.

### 8. Backlog Watch
All three open issues are **stale** (last updated April 2, 2026) and have received *zero* maintainer comments or labels. This is a significant concern:
- **#1273** (sql.js crash) — Unacknowledged for 3+ months; data corruption is a showstopper.
- **#1265** (multi-agent IM/model binding) — Unacknowledged; represents a key roadmap gap.
- **#1263** (duplicate tasks) — Unacknowledged; trivial UX regression left unresolved.

**Recommendation:** The maintainers should prioritize triaging these issues, especially #1273, before the next release cycle.

---

*Data sourced from [github.com/netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI). Generated 2026-07-24.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-24

## 1. Today's Overview
Moltis shows **moderate activity** with 5 PRs closed and 2 new releases in the last 24 hours, indicating a focused push on quality-of-life fixes and security hardening. The project closed one bug (session date display) and merged two Slack-related security patches, alongside a documentation dependency bump. One open bug (Podman compatibility, #1095) remains unresolved. The cadence suggests a maintenance sprint with emphasis on Slack integration reliability.

## 2. Releases
Two new releases were published today:
- **20260723.03** (latest)
- **20260723.02**

No release notes, changelogs, or migration guides were linked. Based on merged PRs, these likely contain:
- The session date display fix in the web UI
- Slack API base URL allowlisting improvements
- Slack OTP self-approval for non-allowlisted DM users
- Dependency updates (Astro 7.0.9 → 7.1.3)

No breaking changes or migration steps are documented.

## 3. Project Progress
All 5 PRs updated in the last 24 hours were **merged/closed**:

| PR | Title | Type | Author |
|----|-------|------|--------|
| [#1124](https://github.com/moltis-org/moltis/pull/1124) | Add context command support for chat turns | Feature | gptme-thomas |
| [#1161](https://github.com/moltis-org/moltis/pull/1161) | chore(deps): bump astro from 7.0.9 to 7.1.3 in /docs | Dependencies | dependabot[bot] |
| [#1162](https://github.com/moltis-org/moltis/pull/1162) | fix(web): show dates for older sessions | Bugfix | shixi-li |
| [#1164](https://github.com/moltis-org/moltis/pull/1164) | fix(slack): allow operator-approved api base hosts | Security | penso |
| [#1163](https://github.com/moltis-org/moltis/pull/1163) | fix(slack): challenge unknown allowlist DMs with OTP | Security | penso |

**Notable advances:**
- **Feature**: `chat.context_command` support (#1124) enables automatic injection of runtime context before each chat turn, useful for deployments needing dynamic context without manual pasting.
- **Bugfix**: Web UI session list now properly shows dates for sessions older than today (#1162).
- **Security**: Slack integration hardened against bypass vulnerabilities — empty allowlists no longer grant open access, and OTP self-approval is enforced for non-allowlisted DMs (#1163, #1164).

## 4. Community Hot Topics
**Most active (by comments/reactions):**

- **[Issue #1095](https://github.com/moltis-org/moltis/issues/1095) [Bug] Podman is not working via Moltis**  
  *1 comment, updated 2026-07-23*  
  Reported by RokkuCode on 2026-06-03. The user confirmed using latest Moltis. No reaction count, but this is the **only open bug** and has been unresolved for 7 weeks, suggesting it may be a niche environment issue or low priority.

- **[Issue #1108](https://github.com/moltis-org/moltis/issues/1108) [Bug] Session list shows times but not dates** (CLOSED)  
  Fixed by PR #1162 today. No additional comments — resolved cleanly.

**Analysis**: Community discussion is minimal; the project appears to maintain a focused, small set of contributors. The Podman bug (#1095) remains the community's primary unresolved pain point.

## 5. Bugs & Stability
**Open bugs:**
| Severity | Issue | Status |
|----------|-------|--------|
| Medium | [#1095](https://github.com/moltis-org/moltis/issues/1095) — Podman not working | Open, no fix PR yet |
| Low | [#1108](https://github.com/moltis-org/moltis/issues/1108) — Session date display | **FIXED** (PR #1162) |

**Security fixes merged today** (PRs #1163, #1164) address:
- Empty allowlists granting unintended access in Slack, Teams, Signal, and Matrix
- Missing OTP challenge for new DM users in Slack
- Unrestricted Slack API base URL usage

No regressions were reported today.

## 6. Feature Requests & Roadmap Signals
**Newly shipped in today's releases:**
- `chat.context_command` (#1124) — enables dynamic context injection per chat turn. This signals Moltis is moving toward **deployment-friendly automation** for self-hosted setups.

**Predicted next feature area:**  
Given the Slack security hardening (allowing operator-controlled API base URLs with `MOLTIS_SLACK_API_BASE_URL_ALLOWLIST`), the project may soon add similar configurability for other chat backends (Teams, Discord, Matrix). The Podman bug (#1095) may be addressed if user demand increases.

## 7. User Feedback Summary
**Pain points expressed:**
- **Podman compatibility** (Issue #1095): A user running Moltis with Podman (Docker alternative) cannot get it to work. No workaround provided, and no maintainer response in 7 weeks.
- **Session date visibility** (now fixed): Users could not distinguish sessions from yesterday vs. older days in the web UI.

**Satisfaction signals:**
- The **quick turnaround** on the date display bug (filed June 5, fixed July 23) demonstrates responsive maintenance.
- Security patches for Slack integration were released the same day they were authored, suggesting rapid iteration.

**Underlying need:**  
Users want **reliable container runtime support** (Podman) and **clear session history** for daily workflows. Security-conscious administrators appreciate fine-grained control over Slack API endpoints.

## 8. Backlog Watch
**Issues requiring maintainer attention:**
| Issue | Age | Last Update | Priority |
|-------|-----|-------------|----------|
| [#1095](https://github.com/moltis-org/moltis/issues/1095) — Podman not working | 51 days | 2026-07-23 | Medium — only open bug, no maintainer response |
| *(No other open issues unanswered)* | | | |

**PRs awaiting review:** None — all 5 PRs updated in the last 24h were merged.

**Assessment:** The backlog is clean; the sole unresolved issue (#1095) has no maintainer engagement. If Podman support is in scope, a status update or workaround would improve community trust.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-24

## Today's Overview

Project activity remains very high, with 35 issues updated and 50 PRs updated in the last 24 hours, indicating a healthy and responsive development cycle. A new pre-release, **v2.0.1-beta.2**, was published, primarily focused on CI orchestration and runtime fixes. The community is highly engaged, reporting real-world regressions from the v2.0 upgrade, particularly around performance overhead and tool execution breakage, while contributors are actively submitting fixes across multiple areas including Windows compatibility, memory management, and provider integrations. Overall, the project is in a vigorous but volatile state, typical of a major version transition being rapidly iterated.

## Releases

### [v2.0.1-beta.2](https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.0.1-beta.2)

**What's Changed:**
- `feat(ci): unified release orchestrator gating web on desktop build` — Improves CI reliability by gating web asset publishing behind desktop build success.
- `fix(runtime): rotate text message on new reasoning block` — Fixes a runtime issue where text messages were not properly rotated when a new reasoning block was received.

**Notes:** This is a pre-release. No breaking changes or migration notes documented. The release primarily targets CI pipeline stability and a runtime display bug. Users on v2.0.0.post4 may upgrade to test the fixes, but the performance regression reported in [#6307] is not addressed in this release.

## Project Progress

The following **21 PRs were merged or closed** today. Key achievements include:

- **Graceful Desktop Shutdown** ([#6225](https://github.com/agentscope-ai/QwenPaw/pull/6225)) — Merged. Replaces force-kill of Python backend sidecar with a graceful shutdown sequence, resolving a long-standing issue where backend state could be corrupted or plugins left in an inconsistent state.
- **Memory Edit Recovery** ([#6351](https://github.com/agentscope-ai/QwenPaw/pull/6351)) — Merged. Fixes infinite retry loops when MEMORY.md edits fail by instructing agents to reload and rewrite rather than repeating failed replacements.
- **Console Performance Stabilization** ([#6393](https://github.com/agentscope-ai/QwenPaw/pull/6393)) — Merged. Reduces React re-renders and SSE re-parsing in the chat UI, improving frontend responsiveness for users with long conversations.
- **Governance Policy Audit Fix** ([#6368](https://github.com/agentscope-ai/QwenPaw/pull/6368)) — Merged. Honors `audit_level=none` by skipping SQLite inserts, reducing I/O overhead for users who disable auditing.
- **Tool Guard → Governance Bridge** ([#6390](https://github.com/agentscope-ai/QwenPaw/pull/6390)) — Merged. Phase 1 of bridging tool_guard detection rules into the governance policy system, enabling more precise tool execution controls.
- **New Provider: AIOnly** ([#6268](https://github.com/agentscope-ai/QwenPaw/pull/6268)) — Merged. Adds AIOnly as a built-in model provider, giving users access to 190+ aggregated models.

**Notable Open PRs Under Review:**
- **[QwenPaw Creator App](https://github.com/agentscope-ai/QwenPaw/pull/6284)** — Adds a script-to-storyboard-to-video creation workflow as an app-type plugin.
- **[Unified Browser SDK](https://github.com/agentscope-ai/QwenPaw/pull/6276)** — A major architecture change for browser automation with a control/execution plane split.
- **[Third-Party Agent Backends (Codex/Qoder)](https://github.com/agentscope-ai/QwenPaw/pull/6397)** — Extensible third-party agent support, decoupling from Coding Mode.

## Community Hot Topics

1. **[#6307 — v2.0 Performance Overhead](https://github.com/agentscope-ai/QwenPaw/issues/6307) (6 comments)**
   - **Reaction:** 0 👍
   - **Analysis:** The most commented issue today. A user reports a ~2-second *fixed overhead* per simple reply in v2.0, independent of model latency. This suggests an architectural regression in the request pipeline (possibly the new governance or ReAct loop). Given no fix PR exists yet, this is likely a top priority for maintainers. *Underlying need: Users expect linear performance scaling, not a fixed penalty per interaction.*

2. **[#6344 — Docker Hot-Reload Feature Request](https://github.com/agentscope-ai/QwenPaw/issues/6344) (3 comments)**
   - **Reaction:** 0 👍
   - **Analysis:** Docker users face 1.5-hour update cycles because containers are destroyed and rebuilt, losing runtime tool environments. The user references a mature pattern from the AstrBot project. *Underlying need: Users want OTA-style updates for Docker without data/tool loss, indicating a desire for container lifecycle independence from application updates.*

3. **[#6405 — MCP Tool NotFound](https://github.com/agentscope-ai/QwenPaw/issues/6405) (2 comments)**
   - **Reaction:** 0 👍
   - **Analysis:** Post-v2.0 upgrade, MCP tool resolution is broken — tools with `[mcp-key]__[tool_name]` naming are not found despite correct prefixes. Likely a regression in tool namespace resolution. *Underlying need: MCP integration is critical for users with custom tool chains; this breakage blocks daily workflows.*

4. **[#6363 — Tool Call Arguments Polluted](https://github.com/agentscope-ai/QwenPaw/issues/6363) (3 comments, CLOSED)**
   - **Reaction:** 0 👍
   - **Analysis:** Models (GLM-5-Turbo, DeepSeek-V3) wrapping tool_call JSON in markdown fences or XML tags cause `JSONDecodeError`. The issue was closed, implying a fix was merged. *Underlying need: Multi-model support requires robust parsing against model-specific output formats.*

5. **[#6408 — Undo/Redo Feature Request (New)](https://github.com/agentscope-ai/QwenPaw/issues/6408) (1 comment)**
   - **Reaction:** 0 👍
   - **Analysis:** A user requests `/undo` command to re-edit the previous user+assistant turn, referencing Cherry Studio and ChatGPT patterns. *Underlying need: Users want conversational flexibility to correct mistakes without polluting context with workarounds like "ignore my previous message."*

## Bugs & Stability

Ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **Critical** | [#6407](https://github.com/agentscope-ai/QwenPaw/issues/6407) | ReAct Agent corrupts context by merging tool_call + tool_result into a single `role:assistant` message, causing OpenAI API 400 errors on session restore. | No |
| **Critical** | [#6307](https://github.com/agentscope-ai/QwenPaw/issues/6307) | ~2s fixed overhead per reply in v2.0, independent of model latency. | No |
| **High** | [#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405) | MCP tools always report "Tool not found" after v2.0 upgrade. | No |
| **High** | [#6401](https://github.com/agentscope-ai/QwenPaw/issues/6401) | Cron tasks using `share_session: true` overwrite and lose full conversation history. | No |
| **High** | [#6406](https://github.com/agentscope-ai/QwenPaw/issues/6406) | Windows `execute_shell_command` collapses multiline PowerShell scripts into one line. | Yes: [#6412](https://github.com/agentscope-ai/QwenPaw/pull/6412) |
| **Medium** | [#6372](https://github.com/agentscope-ai/QwenPaw/issues/6372) | Idle queue cleanup can remove a newly recreated queue state (race condition). | No |
| **Medium** | [#6362](https://github.com/agentscope-ai/QwenPaw/issues/6362) | MiniMax-M3 vision model cannot recognize images via built-in provider. | No |
| **Low** | [#6386](https://github.com/agentscope-ai/QwenPaw/issues/6386) | Tool `edit_file` is called repeatedly in a loop for file operations. | No |

**Bugs introduced in v2.0:** Issues [#6307], [#6405], and [#6401] are all v2.0-specific regressions, confirming user reports of architectural instability post-upgrade.

## Feature Requests & Roadmap Signals

**High Signal (likely in next minor release):**
- **Reranker support for ReMe memory** ([#6398](https://github.com/agentscope-ai/QwenPaw/pull/6398) + [#6399](https://github.com/agentscope-ai/QwenPaw/pull/6399)) — Two PRs (backend + UI) adding reranker configuration for memory search. Likely targets v2.0.2.
- **RobotFramework syntax highlighting** ([#6403](https://github.com/agentscope-ai/QwenPaw/issues/6403)) — Low effort, high value for test automation users.
- **On-demand channel dependency installation** ([#6387](https://github.com/agentscope-ai/QwenPaw/pull/6387)) — Reduces core install size; likely to merge soon.

**Medium Signal:**
- **Agent-level token statistics** ([#6392](https://github.com/agentscope-ai/QwenPaw/issues/6392)) — User requests granular token tracking per agent. Could be a plugin feature.
- **Docker hot-update** ([#6344](https://github.com/agentscope-ai/QwenPaw/issues/6344)) — Community demand is high, but architectural complexity is significant. Unlikely in immediate roadmap.
- **Undo/Redo for conversations** ([#6408](https://github.com/agentscope-ai/QwenPaw/issues/6408)) — High user demand pattern, but implementation touches conversation DB and UI. Considered for a future UX improvement.

**Prediction for v2.1.0:** The `QwenPaw Creator` app ([#6284](https://github.com/agentscope-ai/QwenPaw/pull/6284)) and the `Unified Browser SDK` ([#6276](https://github.com/agentscope-ai/QwenPaw/pull/6276)) are likely candidates for a feature release, though both are under review and may not merge until v2.1.0 or a dedicated v2.2.0.

## User Feedback Summary

**Pain Points:**
1. **v2.0 upgrade instability** — Users report performance regression ([#6307]), broken MCP tools ([#6405]), and context corruption ([#6407]). Several users express frustration that v2.0 feels like a downgrade: "*发布前不能测试一些么，最好压力测试一些啊*" (Why not test before release? Do some stress testing!) — [#6376].
2. **Windows compatibility issues** — PATH concatenation drops semicolons ([#6239]), multiline PowerShell commands collapse ([#6406]), and the `execute_shell_command` tool breaks common script patterns.
3. **Docker update pain** — HDD users report 1.5-hour update cycles with full rebuilds ([#6380], [#6344]), making iterative updates impractical.
4. **Safety/Policy confusion** — Users find the tool approval UI dangerous (bright "Always Allow" button) ([#6354]) and the governance policy system opaque ([#6379]).

**Satisfaction Signals:**
- Users are actively contributing: three first-time contributor PRs ([#6412], [#6351]) were opened/merged today.
- Feature requests show deep engagement: reranker, RobotFramework, custom APIs ([#6377]), token statistics — users are building production systems on QwenPaw.
- The quick iteration cadence is acknowledged: "*迭代速度非常快，仅7月就已经发布十余个小版本*" (Very fast iteration, already over a dozen minor versions in July alone) — [#6344].

**Use Cases Emerging:**
- **API-first agents** — Users want to expose QwenPaw agents as HTTP APIs with specific request/response schemas ([#6377]).
- **Professional content creation** — The new Creator app ([#6284]) signals a push into script-to-video workflows.
- **Multi-model testing** — Users are running diverse models (GLM, DeepSeek, Qwen, Gemini, MiniMax) and encountering tool-calling inconsistencies ([#6363], [#6362]).

## Backlog Watch

The following items require maintainer attention:

1. **[#6239 — Windows PATH semicolon drop](https://github.com/agentscope-ai/QwenPaw/issues/6239) (Updated: 2026-07-23, Comments: 2)**
   - **Status:** Open, no assignee, no PR. Affects all Windows users running npm/node tools. The bug is severe (child processes cannot find npm globals) but has been open since July 18 with no maintainer response. This is a **high-priority** bug for the Windows user segment.

2. **[#3015 — MEMORY.md infinite write retry](https://github.com/agentscope-ai/QwenPaw/issues/3015) (Updated: 2026-07-23, Comments: 2)**
   - **Status:** CLOSED, but the root cause (agents retrying failed edits) was only partially addressed by [#6351] fix. The original issue reports that writing in the correct position (front) is not followed by the agent. This should be re-evaluated.

3. **[#5187 — Windows Desktop GUI Automation (UIA + Tauri)](https://github.com/agentscope-ai/QwenPaw/pull/5187) (Updated: 2026-07-23)**
   - **Status:** Open PR since June 14. This is a major feature (computer-use for Windows) but has been open for over 5 weeks. If maintainers intend to include it, it needs review.

4. **[#6302 — Safe Model Discovery Infrastructure](https://github.com/agentscope-ai/QwenPaw/pull/6302) (Updated: 2026-07-23)**
   - **Status:** Open, under review. This PR is foundational for the provider ecosystem but has been open since July 21 with no merge. Blocking downstream provider additions.

5. **[#6276 — Unified Browser SDK](https://github.com/agentscope-ai/QwenPaw/pull/6276) (Updated: 2026-07-23)**
   - **Status:** Open, under review. A high-impact refactor of browser automation. With 40+ files changed and no comments from maintainers since July 20, this may need re-prioritization or grooming.

**Recommendation:** Maintainers should prioritize triage on [#6239] (Windows PATH) and [#6307] (v2.0 performance regression) as they affect the largest user bases. The backlog of large PRs ([#5187], [#6276], [#6302]) should be reviewed for merge conflicts and technical feasibility before the next minor release.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-07-24

## Today's Overview
The ZeptoClaw project is in a moderately active maintenance cycle with 2 open issues and 1 open pull request updated in the last 24 hours, all created by the primary maintainer (qhkm). No new releases were published today, and no community contributions were merged or closed. Activity is concentrated on critical safety and CI infrastructure improvements, indicating a focused push toward hardening the runtime environment before any feature work. The absence of external contributions or comments suggests the project is currently in a maintainer-driven cleanup phase.

## Releases
No new releases were published today. The latest available release remains the previous version.

## Project Progress
No pull requests were merged or closed today. The single open PR #645 remains under review:

- **PR #645** [OPEN] `fix(runtime): scrub subprocess secrets and reap timed-out process trees` — This fix directly targets the two safety gaps detailed in issue #644: environment variable leakage to subprocesses and incomplete process tree cleanup on timeout. The PR also aligns with `cargo-deny` compliance requirements mentioned in issue #646.

## Community Hot Topics
No issues or pull requests received any comments or reactions today. The two open issues and one open PR are all authored by the project maintainer (qhkm) with zero community engagement. This may reflect either (a) a low overall contributor base, (b) that these internal improvements have not yet been socialized, or (c) that the project is in a pre-release stabilization phase where external feedback is minimal.

The underlying need behind these items is clear: users (or the maintainer) are experiencing real operational risk from credential leakage and orphaned processes when running model-authored shell commands during tool use sessions.

## Bugs & Stability
Two critical-severity bugs were reported today, both with corresponding fix PRs in progress:

1. **[P1-critical] Issue #644** `bug(safety): scrub subprocess environments and terminate process trees on timeout` — **Severity: Critical**. The full host environment is inherited by runtime subprocesses, exposing provider API keys and other secrets to model-driven shell commands. Additionally, timeout wrappers around `Command::output()` leave spawned process trees un-reaped, which can lead to resource exhaustion and zombie processes. A fix is proposed in PR #645.

2. **[P1-critical] Issue #646** `chore(ci): restore Clippy and cargo-deny checks on current toolchain` — **Severity: Critical for CI pipeline**. Two CI failures were exposed by PR #645: five new Clippy warnings triggered by Rust 1.97.1 in existing channel, provider, and binary-plugin code; and `cargo-deny` rejecting vulnerable versions of `quick-xml 0.39.2` and `lopdf 0.40.0`. This prevents CI from passing even for unrelated changes. No separate fix PR exists yet; the maintainer appears to be assessing whether to fix these separately or incorporate into PR #645.

## Feature Requests & Roadmap Signals
No feature requests were submitted today. However, the architectural direction signalled by issues #644 and #646—environment scrubbing, process tree management, and vulnerability-based dependency pinning—suggests the next release will focus heavily on security hardening. Users should anticipate changes to the runtime execution model, removal of credential exposure vectors, and updated dependency minimum versions.

## User Feedback Summary
No user feedback, comments, or reactions were recorded today. The absence of community interaction may indicate that ZeptoClaw is currently used primarily by its maintainer or a very small early-adopter base. No new pain points, use cases, or satisfaction/dissatisfaction signals are available from this data sample.

## Backlog Watch
No long-unanswered issues or PRs were identified. All open items (2 issues, 1 PR) were created on 2026-07-23 and remain actively maintained by the project lead. No stale items requiring maintainer attention exist at this time.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-24

## Today's Overview

ZeroClaw's development activity remains intense, with 50 issues and 50 pull requests updated in the last 24 hours—sustained high velocity typical of a project deep in a pre-release hardening cycle. Open issues outnumber closed ones 40:10, and only 2 PRs were merged or closed against 48 still open, indicating a significant review bottleneck. No new releases were published today, but the tracker for v0.9.0 (#7432) shows substantial infrastructure progress in authentication, security hardening, and multi-agent boundaries. A coordinated batch of bug fixes (telegram, cron, config, desktop, sandbox) arrived mid-week, with several contributors submitting PRs that are pending review. The project's pulse remains healthy, but the widening gap between incoming contributions and completed reviews suggests maintainer bandwidth is stretched.

## Releases

No new releases today. The latest version remains v0.8.3. The v0.9.0 milestone is being tracked in Issue #7432 and accumulating breaking changes, security hardening, and new gateway features.

## Project Progress

Two pull requests were merged or closed today:

- **#9320** (merged) — `fix(cron): bound agent job runs with a wall-clock timeout that releases the lock`. This closes a S1-severity blocker where cron agent jobs could hang indefinitely, holding SQLite locks until daemon restart. Author: IftekharUddin.
- **#9321** (merged) — `fix(telegram): send the unauthorized notice for processable media messages`. Unauthorized senders of voice/audio/document/photo media were silently ignored instead of receiving the expected `SkipPermanent` notice. Author: IftekharUddin.

Notable new PRs opened today that are still open:
- **#9310** — `fix(config): propagate nested set_prop value errors instead of masking as unknown property` (IftekharUddin)
- **#9297** — `fix(config): save_dirty resolves map keys containing dots` (IftekharUddin)
- **#9299** — `fix(config): default context_compression.enabled to false` (IftekharUddin)
- **#9319** — `refactor(runtime): seal the engine tool registry as ScopedToolRegistry` (Nillth)
- **#9317** — `fix(zerocode): render transient frames as a viewport slice instead of full history` (IftekharUddin)

## Community Hot Topics

The most active discussions reflect the community's focus on security, configuration reliability, and protocol interoperability:

- **#3566** (9 comments, 7 👍) — **[Tracker] A2A protocol interoperability** — ZeroClaw's most-watched open issue. The community is pushing hard for native Agent2Agent protocol support to enable communication between ZeroClaw instances, NanoClaw, OpenClaw, and any A2A-compliant agent over HTTP. This is a foundational architectural change that would unlock multi-instance agent mesh deployments. *https://github.com/zeroclaw-labs/zeroclaw/issues/3566*

- **#9127** (7 comments) — **RFC: Abstract a `KeySource` trait — classify master-key material by source / deployment form** — A deep architectural RFC received substantive engagement. The proposal addresses ZeroClaw's credential encryption system (ChaCha20-Poly1305 AEAD over 93 secret fields) by introducing a `KeySource` trait to classify key material by deployment form (file, env, TPM, KMS). *https://github.com/zeroclaw-labs/zeroclaw/issues/9127*

- **#2767** (7 comments, 9 👍) — **[Feature] Multi-Agent Routing** — Despite being closed (the feature landed), it remains a highly-referenced issue. The community continues following multi-agent routing patterns and the "Multi-Profile Workspace Management" design that enables multiple isolated agents, multiple channel accounts, and inbound routing via bindings in a single running Gateway. *https://github.com/zeroclaw-labs/zeroclaw/issues/2767*

- **#6378** (8 comments) — **[CLOSED] Discord Bot respond only in specific Discord channels** — The closed issue saw renewed recent activity, indicating operators are actively deploying the `allowed_channels` feature, consistent with the `allowed_rooms` pattern used by Matrix and Nextcloud Talk. *https://github.com/zeroclaw-labs/zeroclaw/issues/6378*

- **#4721** (5 comments) — **[CLOSED] zeroclaw should log to stderr instead of stdout** — Closed but still generating discussion: users piped CLI output like `zeroclaw config schema` and found logs contaminating structured output, requiring manual redirection workarounds. *https://github.com/zeroclaw-labs/zeroclaw/issues/4721*

## Bugs & Stability

Today's bug landscape is dominated by **4 S0/S1 severity issues reported in the last 72 hours**, all with in-progress or merged fix PRs:

**S0 - Data loss / security risk:**
- **#9188** — **Telegram long-poll advances update offset before successful inbound delivery**: Update offset is incremented before voice/attachment parsing succeeds. If download fails, messages are lost permanently. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9188*
- **#9187** — **WeChat sync cursor persisted before message enqueue — crash loses inbound messages**: In-memory cursor gets saved before messages are processed. A crash between save and enqueue loses inbound messages permanently. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9187*

**S1 - Workflow blocked:**
- **#9207** — **web_fetch returns garbage for compressed responses (gzip, brotli, deflate)**: Agents cannot parse compressed responses (e.g., fetching `https://fetch-favicon.zeroclawlabs.ai`). No response decompression in `web_fetch`. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9207*
- **#9191** — **Cron agent jobs have no wall-clock timeout; in-flight locks only cleared at process start**: This was fixed today in PR #9320 (merged). Agent cron jobs now have a wall-clock timeout that releases the SQLite lock. *https://github.com/zeroclaw-labs/zeroclaw/issues/9191*
- **#9204** — **Landlock sandbox restricts the ZeroClaw daemon itself**: Prior issue #5153 resurfaced. When landlock sandbox executes shell commands, it locks the daemon itself, breaking SQLite memory access and other operations. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9204*
- **#9236** — **Fresh Telegram aliases are dropped after config reload**: Setting `channels.telegram.main.enabled true` reports success, but the alias is silently dropped on the next config load. Reproducible on `master`. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9236*
- **#9290** — **Windows desktop installer fails at launch with missing TaskDialogIndirect**: v0.8.3 Windows installer crashes on launch. A new issue reported today. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9290*
- **#9284** — **config flush can overwrite concurrent writes**: `RpcDispatcher::flush_config` does a read-modify-write without a write lock, risking concurrent write corruption. Fix PR not yet observed. *https://github.com/zeroclaw-labs/zeroclaw/issues/9284*

**S2 - Degraded behavior:**
- **#8999** — **ZeroCode streamed user turns look like log/API payloads to small local models**: Ollama with `llama3.2:latest` interprets greetings as protocol or log data instead of ordinary conversation. *https://github.com/zeroclaw-labs/zeroclaw/issues/8999*
- **#9092** — **ZeroCode keystrokes lag in long sessions because active frames render full history**: Both Code pane and Chat pane become slow in long sessions. Fix PR #9317 opened today by IftekharUddin. *https://github.com/zeroclaw-labs/zeroclaw/issues/9092*

**S3 - Minor issues:**
- **#9285** — **nested set_prop masks invalid values as unknown properties**: Config set with invalid values returns confusing path-resolution errors instead of value errors. Fix PR #9310 opened today. *https://github.com/zeroclaw-labs/zeroclaw/issues/9285*
- **#9202** — **`zeroclaw desktop` command uses dead download URL and does not detect installed AppImage on Linux**: Fix PR #9291 opened today by minato32. *https://github.com/zeroclaw-labs/zeroclaw/issues/9202*

## Feature Requests & Roadmap Signals

Several feature requests with high community engagement signal likely v0.9.0 or near-term roadmap items:

- **#3566 — A2A protocol interoperability** (9 comments, 7 👍, priority:p2, risk:high): The most-requested architectural feature. Would enable ZeroClaw instances to form a mesh of interoperable agents. Likely targeted for v0.9.0 given its position in the security/architecture tracker #7432.

- **#3767 — Require TOTP for cross-channel approval of critical tools** (4 comments, priority:p1, risk:high): Demanded by operators who need 2FA for destructive commands (shell access) across all channels. Extending existing `[security.otp]` TOTP enforcement. Likely v0.9.0.

- **#3672 — Workspace file and memory change history** (3 comments, priority:p2, risk:high): Agents are instructed to self-modify files like `SOUL.md` and `AGENTS.md`, but there is no versioning or rollback mechanism. Community wants git-like history for agent self-evolution.

- **#4760 — Use schema-validated tool calls for memory consolidation** (4 comments, priority:p2, risk:high): Proposes replacing prompt-constrained JSON parsing with tool-calling for memory consolidation, improving reliability with smaller models that struggle with structured JSON output.

- **#3696 — Configure external commands for message lifecycle hooks** (4 comments, priority:p2, risk:high): Community wants shell hooks for pre/post message processing to enable memory integration, logging, and context injection without modifying agent prompts.

- **#9228 — Eval results dashboard and trend tracking** (2 comments, priority:p3): Deferred from #7065. The harness already emits per-run data, but there's no longitudinal view for pass-rate trends over time. Likely post-v0.9.0.

## User Feedback Summary

**Pain points expressed today:**

1. **Telegram data loss** (#9188, #9321): Users reporting silent message loss for media and unauthorized sender scenarios. "Update offset is incremented before parsing success" is a recurring pattern affecting multiple channels (Telegram, WeChat).

2. **Configuration reliability** (#9285, #9236, #9284, #9297): Multiple users reporting config settings silently lost, value errors masked as unknown properties, and concurrent write corruption. The `set_prop` and `save_dirty` path is clearly fragile.

3. **Desktop experience** (#9202, #9290): Linux users cannot reliably launch the companion app because AppImage detection is broken and download URLs are stale. Windows users cannot start v0.8.3 at all due to a TaskDialogIndirect crash.

4. **Web fetching broken** (#9207): Agents cannot process compressed responses from modern websites (gzip, brotli, deflate). S1 severity blocks workflows relying on web content.

5. **Sandbox conflicts** (#9204): Security sandbox (Landlock) interferes with daemon operations. Users deploying sandboxing are hitting blocking issues.

**Satisfaction signals:**

- The cron agent timeout fix (#9320) was positively received, addressing a long-standing S1 issue.
- The A2A protocol tracker (#3566) continues to gather reactions (7 👍), indicating strong community alignment behind the roadmap direction.
- Multi-agent routing (#2767) is still being referenced positively as a closed feature that met its goals.

## Backlog Watch

The following important items need maintainer attention:

- **#8746** — `fix(goal): stop active goal self-resume loops` (vrurg, opened 2026-07-05, needs-author-action, risk:high, size:XL, 16 components affected). Critical fix for goal system loops, blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8746*

- **#8838** — `fix(providers): idle-bound SSE streaming on one shared transport` (singlerider, opened 2026-07-08, needs-author-action, risk:high, size:XL). Unifies SSE parsing across OpenAI, Anthropic, and compatible providers with a 90-second idle guard. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8838*

- **#8741** — `fix(browser): validate screenshot destination path against workspace policy` (wangmiao0668000666, opened 2026-07-05, needs-author-action, risk:high, size:XL). Browser screenshot tool writes files without workspace path validation—a security bypass. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8741*

- **#8713** — `fix(tools): add allowed_private_hosts opt-in to file_download SSRF gate` (wangmiao0668000666, opened 2026-07-04, needs-author-action, risk:high, size:XL). Third remaining SSRF surface from July 2026 security audit; `file_download` has no host classifier. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8713*

- **#8689** — `feat(channels): add goal command admission` (vrurg, opened 2026-07-04, needs-author-action, risk:high, size:XL). Adds `/goal` command admission to channels. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8689*

- **#8438** — `feat(cron): add shell_output_format config for raw stdout output` (Project516, opened 2026-06-28, principal contributor, needs-author-action, risk:high, size:L). Adds operator-requested raw stdout output mode for cron shell jobs. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8438*

- **#8561** — `feat(channels/telegram): add multi_message streaming mode` (metalmon, opened 2026-06-30, trusted contributor, needs-author-action, risk:high, size:XL). Adds paced multi-message delivery to Telegram, matching Discord/Matrix. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/8561*

- **#9251** — `feat(infra): PostgreSQL as the first supported session backend` (perlowja, opened 2026-07-22, needs-author-action, risk:high, size:XL). Major infrastructure change to replace SQLite-backed sessions with PostgreSQL. Blocked on author action. *https://github.com/zeroclaw-labs/zeroclaw/pull/9251*

**Total blocked in `needs-author-action`**: 10 PRs. This is a concerning backlog that suggests contributors may be waiting for maintainer feedback before proceeding. The `needs-author-action` label may be masking PRs where maintainers requested changes but contributors have not responded.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*