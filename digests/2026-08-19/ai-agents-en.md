# OpenClaw Ecosystem Digest 2026-08-19

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-19 00:30 UTC

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

Based on the provided GitHub data for OpenClaw (github.com/openclaw/openclaw) on 2026-08-19, here is the project digest:

---

## OpenClaw Project Digest - 2026-08-19

### 1. Today's Overview

OpenClaw is in a period of intense stabilization and hardening following the recent 7.x release cycle. The project shows very high activity with 500 open issues and 500 open PRs, indicating a large community and significant ongoing development. The focus is squarely on resolving regressions from recent updates, particularly around session-state management, data integrity (SQLite), and channel-specific delivery reliability. While there were no new releases today, the sheer volume of high-priority (P0/P1) bug reports and a steady stream of open pull requests suggest a proactive, if overloaded, maintenance effort. The "clawsweeper" bot automation is heavily involved in triage, but a large number of issues are stuck waiting on maintainer review and product decisions, indicating a critical bottleneck.

### 2. Releases

No new releases were published on 2026-08-19.

### 3. Project Progress

Despite no new releases, numerous Pull Requests were updated and closed, indicating active progress towards the next patch release.

- **Merged/Closed PRs:** 119 PRs were in the closed/merged state.
- **Key Fixes and Features (from recently updated PRs):**
    - **Performance:** `fix(sessions): prevent gateway stalls during large session cleanup` (#126035) directly addresses the critical bug #112423 about SQLite transcript cleanup blocking the event loop. This is a major stability fix.
    - **Security:** `fix: add ssrf protection to Beam fetches` (#123848) is a significant security hardening step for the Beam plugin.
    - **Stability:** `fix: restart-recovered turns no longer show fatal errors` (#126087) improves the recovery experience and user trust after gateway restarts.
    - **New Features:** `feat(security): require acknowledgement for install policy warnings` (#116489) is a significant security and UX feature that was closed, adding a layer of human-in-the-loop control for plugin installs.
    - **Refactoring:** A major refactor, `refactor(canvas): make the panel a widget presenter` (#126030), has been opened, suggesting ongoing improvements to the UI architecture.

### 4. Community Hot Topics

The most active discussions highlight deep concurrency, state management, and provider interoperability problems:

- **#77598 "Track live dev agent behavior and trajectory" (23 comments):** A meta-issue where the community is observing a developer agent in real-time. This unique activity shows the forward-thinking and curious nature of the community, tracking agent behavior for learning and improvement.
- **#112423 "[Bug]: Large SQLite transcript cleanup blocks the gateway event loop" (17 comments):** This is a highly impactful performance bug affecting stability. The high engagement and the existence of related PR #126035 show it's a top priority for the community and maintainers.
- **#38327 "[Bug] 'Cannot convert undefined or null to object' in 2026.3.2 with google-vertex/gemini-3.1-pro-preview" (14 comments):** A long-standing regression with a major provider (Google), causing frustration. The 3+ month lifespan of this issue underscores a potential weakness in regression testing for specific providers.
- **#101290 "CLI startup preflight can corrupt the live state DB" (15 comments):** A P0 data-corruption issue, even though marked as closed, the intense discussion reflects the severity of the concern for users.

### 5. Bugs & Stability

The project is facing a significant number of high-severity bugs, many of which are regressions from recent updates.

**Critical (P0):**
- **#112395 "[Bug]: Startup migration preflight blocks gateway after upgrade from 6.11 to 7.1"** - Regression preventing upgrades.
- **#101290 "CLI startup preflight can corrupt the live state DB"** - Data corruption (Closed, but concerning).

**High (P1 - pending review, links to related PRs):**
- **#113306 "SQLite snapshot restore lacks end-to-end crash and identity guarantees"** - Data integrity concerns.
- **#114211 "Matrix room agents can loop on visible no-reply output, restart recovery, and stale session replay"** - Complex session state and behavioral loop bug.
- **#111498 "Main agent blocked by persistent workspace-state migration after Anthropic auth recovery"** - Auth and session state regression.
- **#114234 "Usage-cost refresh lock is never releasable after a restart that reuses the owner PID (containers)"** - A specific container-environment bug causing a permanently frozen cache.
- **#94939 "[Bug]: 6.x state migration leaves channel conversation-store SQLite empty (0 bytes)"** - A data loss bug on migration, particularly impacting MS Teams users.

**Notable Backend/Channel Bugs with Active PRs:**
- **#88657 "DeepSeek V4 Flash incomplete turn"** (P1) - Model-specific turn failure.
- **#91144 "[Bug]: Windows native CLI gateway Scheduled Task does not stay running"** (P1) - Platform-specific stability issue.

### 6. Feature Requests & Roadmap Signals

Several requests hint at where OpenClaw is heading next:

- **Enhanced Agent Autonomy:** Requests like **#6757 "Agent-triggered context compaction (self-compact tool)"** and **#96975 "Isolate subagent completion from parent context"** indicate a push towards more autonomous, self-managing agents.
- **Dynamic and Configurable Models:** **#10687 "fully dynamic model discovery (OpenRouter + beyond)"** is a popular request that would drastically improve the user experience and address many configuration-related issues. It's likely a major feature for an upcoming release.
- **Voice and Companion Support:** The feature request **#45508 "Self-hosted STT/TTS provider support in webchat"** and the PR for an experimental **FaceTime bridge (#119291)** show growing interest in real-time voice and multi-modal interactions.
- **Hosting and Form-Factor Expansion:** An official Android surface (**#46058**) and **Kubernetes documentation improvement (#91455)** are signals that the project is maturing beyond just a desktop/server tool.

### 7. User Feedback Summary

- **High Frustration with Update Migrations:** Users are repeatedly hitting broken upgrade paths, facing data loss, and blocked gateways after updating. The issues with SQLite migrations (#94939, #90378) are a significant source of dissatisfaction.
- **Cost and Performance Concerns:** Users are experiencing severe regressions such as a dramatic drop in prompt cache hit rate (#91223) and high latency in channel-specific features (#91941). These issues directly impact the cost and usability of the platform.
- **Desire for Reliability:** The volume of issues with "recovery-stuck" labels suggests users feel trapped when the agent or gateway encounters errors. They seek smoother self-recovery and less manual intervention. There is also a clear request for configurability to reduce noise, like suppressing transient tool error warnings (#39406).

### 8. Backlog Watch

A large number of issues are blocked on maintainer review, indicating a need for more maintainers or a streamlined focus. Several important, long-lived issues (3+ months old) remain unresolved.

- **#38327 (2026-03-06):** Google Vertex/Gemini regression remains unresolved after over 5 months, indicating a gap in provider-specific testing.
- **#77598 (2026-05-05):** The "live dev agent" watch is still active, potentially providing valuable data to the maintainers but also taking up community focus.
- **#43374 (2026-03-11):** The "All LLM API calls time out simultaneously" bug has been open for over 5 months, which is a core reliability problem for multi-agent usage.
- **#79614 (2026-05-09):** The issue regarding "stale-reply re-anchoring" was closed as stale but is a complex conversational bug that likely needs a more robust solution.
- **@openclaw/codex plugin failure (#112248, 2026-07-21):** The codex plugin, which is being actively developed, still has a blocking registration bug awaiting a maintainer review.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date: 2026-08-19**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is in a **post-major-release stabilization phase**, with the leading projects (OpenClaw, Hermes Agent, CoPaw, ZeroClaw) consolidating gains from recent version launches while addressing migration regressions, session-state reliability, and multi-backend architecture complexity. Development activity remains exceptionally high—over 700 issues and 600 PRs were touched across surveyed projects in a single 24-hour window—indicating robust community engagement. The ecosystem is converging on **several core architectural priorities**: database portability, provider abstraction, cost-control mechanisms, and cross-channel session consistency. Notably, **Windows platform support has emerged as a recurring weakness** across multiple projects, while MCP protocol compliance and memory reliability are becoming competitive differentiators. The landscape shows clear tiering: mature, overloaded core platforms (OpenClaw); rapidly-iterating mid-tier challengers (Hermes, CoPaw, ZeroClaw); and smaller specialized tools stabilizing after feature pushes (PicoClaw, NanoBot, Moltis).

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score | Activity Phase |
|---------|-------------|-----------|----------------|--------------|----------------|
| **OpenClaw** | 500 open (high churn) | 500 open (~119 merged/closed) | No release; pre-patch | 6/10 (overloaded, critical bugs) | Stabilization/hardening |
| **Hermes Agent** | 50 updated (9 closed) | 50 updated (9 merged/closed) | **v0.20.4 released** | 8/10 (responsive, healthy) | Stable iteration |
| **NanoBot** | 9 updated (3 closed) | 26 updated (6 merged/closed) | No release; pre-cut | 7/10 (active, small scale) | Feature accumulation |
| **PicoClaw** | 6 updated | 4 updated (2 merged/closed) | v0.3.1 (no new release) | 6/10 (moderate, stale PRs) | Maintenance + Web UI push |
| **NanoClaw** | 3 updated (2 closed) | 39 updated (16 merged/closed) | No release; mid-refactor | 8/10 (focused refactor) | Major refactor |
| **IronClaw** | 22 updated (6 closed) | 39 updated (15 merged/closed) | **v1.3.0-rc.2 released** (fix) | 7/10 (active, solid) | Release validation |
| **LobsterAI** | 9 (all stale, ~4mo) | 20 updated (17 merged/closed) | **2026.8.18 released** | 5/10 (strong dev, stale issues) | Feature shipping |
| **Moltis** | 2 issues closed | 5 merged/closed + 1 open | **2 releases (20260818.06/.08)** | 9/10 (excellent responsiveness) | Steady growth |
| **CoPaw** | 46 updated (16 closed) | 50 updated (19 merged/closed) | v2.1.0 (no new release) | 7/10 (post-2.1.0 hardening) | Stabilization |
| **ZeroClaw** | 50 updated | 50 updated (4 merged/closed) | No release; heavy review phase | 5/10 (bottlenecked merges) | Review-blocked accumulation |
| **NullClaw / TinyClaw / ZeptoClaw** | 0 | 0 | — | N/A | Dormant (24h window) |

---

## 3. OpenClaw's Position

**Advantages:**
- **Largest community by order of magnitude** — 500 open issues/PRs dwarfs all peers; the de facto reference implementation with the widest channel adapter coverage (Slack, Discord, Teams, Matrix, IRC, Webhook)
- **Maturity of architecture** — session-state management, SQLite persistence, and multi-channel delivery are battle-tested at scale; the `clawsweeper` bot automation for triage is the most sophisticated in the ecosystem
- **Ecosystem gravity** — PicoClaw, NanoClaw, and ZeroClaw are explicitly forks/satellites, extending OpenClaw's reach; LobsterAI builds directly on the OpenClaw core
- **Recovery features** — restart-recovered turns, migration preflight, and session cleanup demonstrate depth of operational experience

**Technical approach differences:**
- OpenClaw uses a **gateway-centric monolithic core** with plugin extensions, while Hermes Agent emphasizes **multiplex profiles and multi-backend routing** and CoPaw focuses on **desktop-first experience with distributed sessions**
- OpenClaw's **SQLite-centric storage** (currently synchronous) is being challenged by NanoClaw's async, driver-portable DB abstraction—a signal that OpenClaw's architecture may face pressure to modernize storage layers
- OpenClaw's **context compaction and session management** remain more granular than most peers, though Hermes's goal-continuation logic and CoPaw's task pipeline are competitive

**Community size comparison:**
- OpenClaw's issue volume (500) is ~10x Hermes (50) and CoPaw (46), and ~100x smaller projects (2-9)
- However, **maintainer bandwidth is a critical constraint** — OpenClaw has 119 PRs merged/closed (good) but hundreds of issues awaiting triage, while Moltis (9/10 health) and Hermes (8/10) demonstrate what a more contained scale enables: same-day fix PRs and responsive maintainers

**Strategic recommendation:** OpenClaw's position is secure but vulnerable to community fatigue from migration bugs and review bottlenecks. Competitors are winning on responsiveness and modern architecture (async DB, provider abstraction). OpenClaw should invest in maintainer capacity or automated triage to prevent churn.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Windows platform support** | OpenClaw, NanoBot, Hermes, CoPaw, ZeroClaw | Test suite failures (74 in ZeroClaw), venv/PID handoff bugs, Scheduled Task issues, console encoding, native notifications |
| **Database portability / async migration** | OpenClaw (SQLite sync), NanoClaw (async drivers), ZeroClaw | Move off `better-sqlite3` toward driver-portable abstraction; OpenClaw's SQLite transcript cleanup blocking event loop is the canonical bug |
| **MCP protocol compliance & resilience** | OpenClaw, Hermes, CoPaw, PicoClaw | `streamable_http` not honored (CoPaw), SSE hardcoding, session eviction, OAuth2 refresh persistence, health-probe interference |
| **Cost control & usage observability** | OpenClaw, NanoBot, Hermes, IronClaw, PicoClaw, LobsterAI | Hybrid spend firewalls, credential pool cooldowns, prompt-cache token logging, budget ledger refinements, provider attempt accounting |
| **Multi-backend / profile identity routing** | OpenClaw, Hermes, CoPaw, ZeroClaw | Profile identity late-binding, connection×profile route preservation, session isolation across UI/channel boundaries |
| **Memory reliability** | OpenClaw (compaction), IronClaw, Hermes, NanoBot | Cross-conversation recall failures, compaction preserving concurrent state, MCP schema budget for context bloat |
| **Configuration fragmentation** | OpenClaw, ZeroClaw, CoPaw, Hermes | Silent no-op configs, settings split across surfaces, unified slash-command registry, UI clobbering unknown config keys |
| **Security hardening** | OpenClaw (SSRF), NanoBot (resource limits), ZeroClaw (credential URLs, browser auto-approve), CoPaw (malware false-positive) | Sandbox escapes, unbounded subprocesses, fail-open stored credentials, API key leakage via URLs |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architecture |
|---------|--------------|-------------|--------------|
| **OpenClaw** | Universal channel gateway | Power users, self-hosters, multi-platform | Monolithic core + plugins; SQLite sync; extensive channel adapters |
| **Hermes Agent** | Multi-profile/multi-backend agent runtime | Advanced users managing multiple providers/identities | Multiplex profiles; goal-driven loops; MCP-first |
| **CoPaw** | Desktop-first intelligent assistant | Desktop productivity users, enterprise pilots | Console + desktop app; Feishu/DingTalk channels; Qwen partner ecosystem |
| **ZeroClaw** | Daemon-centric automation (fork of OpenClaw) | Automation-heavy users, cron/CI jobs | Daemon + web/TUI; heavy on observability and security controls |
| **IronClaw** | Enterprise automation (Reborn runtime) | Enterprise QA/automation pipelines | Model-agnostic runtime; PinchBench load tests; capability-outcome processing |
| **LobsterAI** | Desktop UI over OpenClaw | Non-technical OpenClaw users | Electron wrapper + OpenClaw backend; multi-engine (dsh, OpenClaw) |
| **NanoClaw** | OpenClaw fork with async DB + drivers | Developers needing portable storage | Async DB seam; driver abstraction; session-runtime drivers (Docker) |
| **NanoBot** | Lightweight agent runner | TUI/CLI users, lightweight deployments | Python; TUI + exec tools; Windows-focused fixes |
| **PicoClaw** | Lightweight OpenClaw fork | Raspberry Pi, resource-constrained users | Minimal; IRC-first; Web UI roadmap |
| **Moltis** | Containerized agent platform | Self-hosting developers | Podman/Docker containers; managed files library; connector snapshots |

**Key architectural tension:** **Monolithic vs. modular** — OpenClaw's monolithic core benefits from integration but suffers from migration regressions. NanoClaw's async DB refactor and Moltis's container-native design represent the modular future. **Desktop vs. web/CLI** — CoPaw and LobsterAI bet on desktop, OpenClaw/Hermes on web/CLI, Moltis on containerized web. **Provider breadth vs. depth** — OpenClaw/Hermes chase many providers; IronClaw focuses on automation outcomes; Moltis curates connectors (Tesla).

---

## 6. Community Momentum & Maturity

**Tier 1 — High-velocity, mature (leading edge):**
- **OpenClaw**: Massive, extremely active, but overloaded — 500 open issues, 119 PRs merged/closed in 24h, yet critical migration bugs persist (P0 blockers on upgrade). Health: 6/10 — volume is a double-edged sword.
- **Hermes Agent**: Excellent momentum — weekly patch releases, same-day fix PRs, 9/10 health. Demonstrates what a disciplined, well-scoped project achieves at 1/10th the issue volume.
- **CoPaw**: Post-2.1.0 hardening, strong contributor cadence (6+ first-time PRs), but MCP debt and UX regressions accumulating. Health: 7/10.

**Tier 2 — Active, focused (mid-tier):**
- **ZeroClaw**: Highest review-bottleneck risk — 12 PRs marked `do-not-merge`, only 4 merged/closed in 24h. Heavy feature accumulation outpacing delivery. Health: 5/10.
- **IronClaw**: Solid release validation (rc.2 crash fix), evidence-based automation improvements. Health: 7/10.
- **NanoClaw**: Focused refactor (async DB) with excellent momentum — 16/39 PRs merged. Health: 8/10.
- **Moltis**: Small but excellent — 2 releases/day, same-day bug fixes, strong maintainer responsiveness. Health: 9/10 (best ratio per issue volume).

**Tier 3 — Maintenance/small-scale:**
- **NanoBot**: Healthy but small; Windows fixes dominate; accumulating code pre-cut. Health: 7/10.
- **PicoClaw**: Moderate activity; Web UI refactor pending; stale PRs need attention. Health: 6/10.
- **LobsterAI**: Dev-strong (17 PRs merged) but issue queue stale (~4 months untouched, no maintainer responses). Health: 5/10.
- **NullClaw / TinyClaw / ZeptoClaw**: Dormant in 24h window.

**Bottom line:** Hermes, Moltis, and NanoClaw show what **disciplined responsiveness** looks like; OpenClaw and ZeroClaw risk churn from their own success. LobsterAI's stale issue queue is a community-experience liability.

---

## 7. Trend Signals

**1. Cost-Exposure Anxiety is Mainstream**
The most emotionally-charged community feedback across NanoBot ("Prevent Margin Leaks & Surprise LLM Bills"), IronClaw (BudgetLedger accounting), ZeroClaw (provider attempt accounting), and Hermes (quota-aware credential pooling) signals that **unbounded LLM costs are the #1 operational risk** for agent deployments. Expect: hybrid spend firewalls, per-task budgets, and prompt-cache optimization to become default features.

**2. Windows is the New Frontier**
Seventeen-comment threads in ZeroClaw, rapid-fire Windows fixes in NanoBot, Hermes's terminal/env probe deadlocks, and CoPaw's task-continuity issues on Windows 11 collectively point to a **strategic platform gap**. The ecosystem's Linux/macOS-first mindset is colliding with a Windows-heavy user base. Expect: Windows-specific regression test suites and cross-platform CI hardening to emerge as a differentiator.

**3. MCP Protocol Compliance is Table Stakes**
CoPaw (SSE hardcoded, failed reconnection), Hermes (OAuth client ID), and Moltis (Responses API routing) all show the ecosystem is **struggling to keep pace with MCP's evolving spec**. Projects that honor `streamable_http`, implement OAuth2 refresh persistence, and handle session eviction gracefully will win enterprise trust.

**4. Memory Reliability is the Competitive Moat**
IronClaw's champions program reporting memory recall failures, OpenClaw's compaction goals, Hermes's goal-continuation fix, and NanoBot's persistent-memory proposals all point to **memory as the key differentiator between "chatbot" and "agent"**. The Mnesis spike in IronClaw is the most concrete signal of a new architecture investment.

**5. Multi-Engine is the Future**
LobsterAI's dsh integration, OpenClaw's plugin ecosystem, and Hermes's multiplex profiles all show that **locking users into a single model or provider is a losing strategy**. The ability to route across engines (OpenClaw + dsh + hermes-agent) with unified session management will be a key migration driver.

**6. Review Bottlenecks Threaten Community Health**
ZeroClaw's 12 `do-not-merge` PRs, OpenClaw's 500 open issues, and LobsterAI's 4-month-stale issues all signal **maintainer bandwidth as the ecosystem's scarce resource**. Projects investing in automation (OpenClaw's clawsweeper), bots (Hermes's agent-authored issues), and delegation (Moltis's community contributors) are the ones likely to retain contributor trust.

**7. Security Conscious by Default**
SSRF protection (OpenClaw), resource limits (NanoBot), fail-closed auth (NanoClaw), and browser tool opt-in (ZeroClaw) indicate a shift from "agent does everything" to **"agent does everything safely by default."** Security posture is becoming a documented purchase criterion for enterprise adoption.

---

**For AI agent developers:** Prioritize cost-control primitives, Windows cross-platform testing, MCP spec compliance, and memory-as-a-feature. OpenClaw remains the safest community bet for breadth, but Hermes/Moltis show the responsiveness that wins enterprise pilots. ZeroClaw's review bottleneck is an opportunity—contributors who help clear it will gain influence. The ecosystem is consolidating around "safe-by-default, provider-agnostic, memory-consistent agents," and the next 6-12 months will reward projects that ship those three pillars.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-19

## Today's Overview

NanoBot is in a highly active development phase, with 26 pull requests and 9 issues updated in the last 24 hours. The project shows a healthy mix of bug fixes, feature development, and community engagement; the issue tracker maintains a solid open-to-closed ratio (6 open vs. 3 closed today), while PR activity skews toward open items (20 open vs. 6 merged/closed), indicating a strong development pipeline awaiting review. Notably, a recurring theme of Windows-specific stability fixes and proxy/network compatibility improvements indicates an active user base on diverse platforms. No new releases were published this period, suggesting code is accumulating ahead of a version cut.

## Releases

No new releases or version tags were published in the last 24 hours.

## Project Progress

Six PRs were merged or closed today, highlighting recent progress in several areas:

- **TUI Stability Improvements**: [PR #5427](https://github.com/HKUDS/nanobot/pull/5427) and [PR #5432](https://github.com/HKUDS/nanobot/pull/5432) (both by chengyongru) were closed with fixes for TUI composer focus/visibility and API credential refreshing after HTTP 401s, respectively. These represent meaningful quality-of-life improvements for the terminal UI.
- **Cross-Session Messaging**: [PR #5358](https://github.com/HKUDS/nanobot/pull/5358) (chengyongru) was merged, adding lightweight cross-session messaging with stable, server-owned `@handle` identities. This is a notable architecture feature for multi-session workflows.
- **Test Reliability**: [PR #5433](https://github.com/HKUDS/nanobot/pull/5433) (chengyongru) was closed, introducing output-aware waiting in exec tests to fix a flaky Windows CI job, an important step toward stable cross-platform test suites.
- **Windows Handoff**: [PR #5415](https://github.com/HKUDS/nanobot/pull/5415) (chengyongru) is another Windows-focused fix (still open) addressing the venv child process PID handoff, indicating an ongoing campaign to harden Windows support.

## Community Hot Topics

The most active community discussions focus on **cost control and system safety**, echoing underlying worries about agent autonomy cost exposure:

- **[Issue #5409](https://github.com/HKUDS/nanobot/issues/5409) "Prevent Margin Leaks & Surprise LLM Bills"** (sophieamoure2026-ui, created 2026-08-17) proposes a "Hybrid Spend Firewall" to cap runaway LLM costs. This is a strong signal that commercial users are concerned about operational cost risks of open-ended agent loops.
- **[Issue #4797](https://github.com/HKUDS/nanobot/issues/4797) "No resource limits on shell subprocesses"** (hamb1y, created 2026-07-06) remains open with a low comment count but is a long-standing security/safety liability. It pairs naturally with [PR #4880](https://github.com/HKUDS/nanobot/pull/4880), which proposes defaulting `restrict_to_workspace` to `True` — both point to a community push for safer-by-default sandboxing.
- **[Issue #5372](https://github.com/HKUDS/nanobot/issues/5372)**, a closed partnership proposal from a memory-solution vendor (ViBo), received zero comments but signals external interest in persistent memory capabilities for agents.

## Bugs & Stability

Several bugs were reported or updated today, ranked by severity and impact:

1.  **[#4797](https://github.com/HKUDS/nanobot/issues/4797) — Unbounded shell subprocesses (Security, High)**: No `ulimit`, CPU, or memory caps on `ExecTool._spawn()`. An LLM could fork-bomb the host. Fix PR exists ([#4880](https://github.com/HKUDS/nanobot/pull/4880)) but is blocked by conflicts and is still open.
2.  **[#5429](https://github.com/HKUDS/nanobot/issues/5429) — Background task exceptions consumed silently (Reliability, Medium)**: `AgentLoop.schedule_background()` drops exceptions, hiding failures. Fix PR [#5431](https://github.com/HKUDS/nanobot/pull/5431) is open.
3.  **[#5428](https://github.com/HKUDS/nanobot/issues/5428) — Memory leak in `AgentLoop` task groups (Performance, Medium)**: Empty sets are retained after task completion. Fix PR [#5430](https://github.com/HKUDS/nanobot/pull/5430) is open.
4.  **[#5149](https://github.com/HKUDS/nanobot/issues/5149) — WhatsApp audio files not sent (Functionality, Medium)**: Long-running issue (created 2026-07-28, 6 comments) with no linked fix PR yet.
5.  **[#5425](https://github.com/HKUDS/nanobot/issues/5425) — Legacy `socks://` proxy URLs fail (Compatibility, Low)**: Two competing fix PRs exist: [#5426](https://github.com/HKUDS/nanobot/pull/5426) and [#5435](https://github.com/HKUDS/nanobot/pull/5435), which need maintainer triage.
6.  **[#5417](https://github.com/HKUDS/nanobot/issues/5417) — Windows WebUI exits on PID handoff (Platform, Closed)**: Marked closed, suggesting the issue was resolved or stale, but linked PR [#5415](https://github.com/HKUDS/nanobot/pull/5415) is still pending merge.

## Feature Requests & Roadmap Signals

User requests clustering around enhanced visibility, cost control, and memory suggest "safety rails" as a key design tension for autonomous agents:

- **Agent Memory (Persistent)**: External proposal for ViBo memory integration ([#5372](https://github.com/HKUDS/nanobot/issues/5372)) and an in-house design question about compaction preserving concurrent state ([#5421](https://github.com/HKUDS/nanobot/issues/5421)) both gesture toward richer session persistence. High likelihood for a follow-up feature or documented contract for memory plugins.
- **WebUI Observability**: [PR #5420](https://github.com/HKUDS/nanobot/pull/5420) adds turn observability and safe recovery; [PR #5408](https://github.com/HKUDS/nanobot/pull/5408) proposes follow-up suggestions. These point to more interactive, human-in-the-loop control surfaces.
- **Metasearch Provider**: [PR #5234](https://github.com/HKUDS/nanobot/pull/5234) integrates the MST metasearch tool, broadening provider diversity; it remains open.
- **Music Generation**: [PR #5212](https://github.com/HKUDS/nanobot/pull/5212) adds MiniMax music guidance, showing a roadmap beyond text/chat into multi-modal output.
- **MCP Schema Budgeting**: [PR #5388](https://github.com/HKUDS/nanobot/pull/5388) proposes opt-in byte budgets for model-visible tool schemas, a feature to manage token bloat in complex agent setups.

## User Feedback Summary

Community sentiment is a mix of frustration with cross-platform quirks and enthusiastic contributions from power users:

- **Windows Frustration**: Multiple issues and a coordinated set of fixes (TUI focus, credential refresh, venv handoff, weather skill curl alias) reflect a real user pain point. The rapid-fire PRs by chengyongru indicate a responsive maintainer community but also that Windows was a weak spot.
- **Cost Anxiety**: The "Spend Firewall" proposal and resource-limit issues resonate with users running production workloads who fear unbounded LLM bills. This is a primary anxiety point for those moving beyond experimentation.
- **Feature Appetite**: Users are actively building memory, observability, and meta-search integrations, signaling a desire for a more "product-like" agent runner rather than just a framework.
- **Missing Audio Support**: Issue [#5149](https://github.com/HKUDS/nanobot/issues/5149) is the oldest, still-unresolved functional gap in the latest 24h dataset, implying possible dissatisfaction among WhatsApp channel users.

## Backlog Watch

The following items require maintainer attention due to their age, severity, or conflicting states:

1.  **[PR #4880](https://github.com/HKUDS/nanobot/pull/4880) — Default restrict_to_workspace to True (Security)**: Open since 2026-07-11 with persistent merge conflicts. This is a high-priority security hardening item that keeps stalling; maintainer time is needed to resolve conflicts and land it.
2.  **[PR #5426](https://github.com/HKUDS/nanobot/pull/5426) vs. [PR #5435](https://github.com/HKUDS/nanobot/pull/5435) — Duplicate socks:// proxy fixes**: Both submitted within 24 hours for the same issue. Maintainers should pick one, merge, and close a duplicate to avoid confusion.
3.  **[Issue #5421](https://github.com/HKUDS/nanobot/issues/5421) — Idle Compaction vs. Concurrent State**: An ASK-FIRST design question that has not received a maintainer response, potentially blocking a contributor from submitting a PR for a race-condition-adjacent design.
4.  **[Issue #5149](https://github.com/HKUDS/nanobot/issues/5149) — WhatsApp Audio Not Sent**: An open bug since late July with 6 comments and no linked fix; this is a widening user-facing gap worth a maintainer triage or a "help wanted" label.

---
*Analysis based on GitHub activity data as of 2026-08-19.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-19

## 1. Today's Overview

Hermes Agent shows **sustained high-velocity development** with 50 issues and 50 PRs updated in the last 24 hours, and a fresh patch release (v0.20.4) rolling up ~74 merged PRs. The project demonstrates **healthy responsiveness to community feedback** — several issues filed today already have dedicated fix PRs (e.g., #89576 → #89581, #89546 → #89572, #89561 → PR pending). Activity spans **desktop UX polish, MCP protocol compliance, credential pool optimization, and multi-profile architecture hardening**. The release cadence (roughly weekly patches with clear semver tracking) and the presence of automated sweeper labels (`risk-*`, `ci-reviewed`) indicate mature engineering practices. Signal of note: **a cluster of issues around profile/connection routing identity** (#88715, #89131, #88680, #89304) suggests a deliberate architectural push on multi-backend support.

## 2. Releases

**v2026.8.18 — Hermes Agent v0.20.4** (August 18, 2026)

> Patch release rolling up ~74 PRs merged since v0.20.3 into a stable tagged build for Docker images, hosted deploys, and fresh installs.

No breaking changes or migration notes were documented in the release body. This is a stability consolidation release.

## 3. Project Progress

Today's merged/closed PRs (9 total) represent **targeted fixes across core subsystems**:

- **[#89580] [CLOSED] — `fmt(js): npm run fix auto-fix`** — Automated lint/formatting sync; auto-merges on green CI.
- **[#89572] [CLOSED] — Desktop: SESSIONS/BOTS tabs lose the ✕** — Salvages #89551; tabs are now shown/hidden via right-click and ⌘K, with persisted preference. Fixes #89546.
- **[#89551] [CLOSED] — Hide hover close buttons on persistent navigation tabs** — Superseded by #89572 but merged in part (cherry-picked).
- **[#89580] [CLOSED] — Auto-fix bot run** — CI hygiene.

The remaining merged/closed items visible in the top-20 PR list are all labeled as closed but appear to be recent; however, the **9 merged/closed PRs today are dominated by desktop UX and CI automation**. The **substantive open PRs** (listed below in Hot Topics) carry the feature momentum.

## 4. Community Hot Topics

The most active discussions reveal **three underlying themes**:

**A. Architecture: Profile identity and connection routing** (highest engagement)
- **[#88715] [3 comments] — Multiplex: profile identity is late-bound across transport, session, storage, and control paths** — [Link](https://github.com/NousResearch/hermes-agent/issues/88715). User `andrexibiza` synthesizes a systemic issue: profile isolation exists but lacks a canonical, immutable point of determination. P2, `needs-decision`, with 3 sweeper labels.
- **[#88680] [1 comment] — [Architecture] Desktop: preserve connection × profile route identity end-to-end** — [Link](https://github.com/NousResearch/hermes-agent/issues/88680). Companion piece arguing desktop identity is now a "route" (source + profile), not just an active profile.

**Analysis:** These aren't bugs — they're **architectural design-pattern requests** from power users running complex multi-backend setups. The maintainers' `needs-decision` label indicates they're engaging but haven't committed to a design direction. This is the **most strategically important thread** in the project right now.

**B. Desktop CPU/performance regression** (highest raw impact)
- **[#88275] [8 comments] — Renderer process burns 40-70% CPU at idle since early August; thermal throttling on macOS Intel** — [Link](https://github.com/NousResearch/hermes-agent/issues/88275). Rich detail from `yuhengliuleo`: Electron 40.10.2, GPU disabled via config partially mitigates. A **fix PR #89578** (star map render loop sleeps when hidden) was opened today, suggesting maintainers are actively tracing this regression.

**C. Skills index freshness/monitoring** (automated visibility)
- **[#66616] [54 comments] — Skills index is stale or degraded** — [Link](https://github.com/NousResearch/hermes-agent/issues/66616). This is an automated freshness probe (`sweeper:risk-automation`) flagging that `skills-index.json` exceeded its 26h freshness limit (29.8h observed). The unusually high comment count (54) reflects **bot-driven status updates**, not human engagement — but it's a visible sign of the project's own health monitoring working.

**D. MCP health probe session eviction** (new, fast-moving)
- **[#89576] [1 comment] — Desktop MCP health probe opens a second HTTP session and evicts the live one (Slack MCP)** — [Link](https://github.com/NousResearch/hermes-agent/issues/89576). Filed today; **fix PR #89581 opened the same day** reusing the live session. Excellent turnaround.

## 5. Bugs & Stability

Ranked by severity; fix PRs noted where they exist:

**High (P2, functional impact):**
- **[#89576] — MCP health probe evicts live session** → Fix PR #89581 (same-day). Desktop health sweep opens a second Streamable HTTP session, breaking hosts with one-session-per-token limits.
- **[#89579] — Startup notification to home channel not sent after server reboot** → [Link](https://github.com/NousResearch/hermes-agent/issues/89579). Marked duplicate; likely same root cause as planned-restart path but triggered by power-cycled reboots. Gateway must detect "unclean" startup.
- **[#89561] — `hermes config set` stores composite values (lists/mappings) as strings** → [Link](https://github.com/NousResearch/hermes-agent/issues/89561). Scriptability gap: config keys with list/dict values cannot be set via CLI — blocks agent-driven config automation.
- **[#89346] — Shared primary profile routes reload session history from root store after #88734** → [Link](https://github.com/NousResearch/hermes-agent/issues/89346). Session-state split when `multiplex_profiles` routes to a secondary profile; DB scoping regression from a prior fix.
- **[#88895] — gateway.error.log grows unbounded (141MB, 268k occurrences)** → [Link](https://github.com/NousResearch/hermes-agent/issues/88895). No rotation + Slack Socket Mode reconnect traceback spam. Production-affecting on macOS launchd.

**Medium (P3, UX/edge-case):**
- **[#89111] — Gateway approval prompts time out on remote Windows desktop** → [Link](https://github.com/NousResearch/hermes-agent/issues/89111). Approval propagation from Windows desktop to remote gateway broken.
- **[#89516] — `minimax-oauth` provider missing `api_key_env_vars`; error messages reference wrong env var name** → [Link](https://github.com/NousResearch/hermes-agent/issues/89516). Confusing DX.
- **[#89415] — Credential pool caches provider cooldown; mid-cooldown credit top-up never re-probed** → [Link](https://github.com/NousResearch/hermes-agent/issues/89415). Stale `last_error_reset_at` prevents failback after manual credit top-up.

**Notable closed today:**
- **[#62202] — Gateway doesn't call `_post_turn_goal_continuation` after each turn** (P2, fixed/closed) — Goal loop was effectively dead. This was a **critical logic bug** now resolved.
- **[#89175] — Goals bootstrap grace window drops first write on slow disks** (closed) — Flaky CI tests addressed.

## 6. Feature Requests & Roadmap Signals

Strongest signals for next release:

| Feature | Issue/PR | Signal Strength | Likelihood |
|---|---|---|---|
| **1080p xAI video-gen support** | Issue #89549 + PR #89569 (same-day) | High — PR already implements; provider docs support it; low risk | **Very likely (next patch)** |
| **Persistent Project Agents (Desktop)** | PR #89567 | High — substantial PR with session reuse and prompt-cache preservation; aligns with Desktop multi-backend push | **Likely (next minor)** |
| **Codex quota-aware credential pooling** | PR #89573 | Medium-High — addresses real cost-control pain; additive strategy flag | **Likely (next minor)** |
| **MCP server catalog expansion** (Pin Seeker) | PR #89583 | Medium — trivial addition, but currently a single MCP without clear demand | **Possible (next patch)** |
| **CIMD client identification for OAuth MCP** | PR #89566 | Medium — required for compliance with MCP 2026-07-28 spec; fallback DCR preserved | **Likely (next minor)** |
| **Per-job `allow_memory` flag for cron** | Issue #18885 (open since May, 5 comments) | Awaits maintainer decision; has clear use case from `ar-nim` | **Uncertain — watch for `needs-decision` resolution** |
| **Inbound message hook with sender/message IDs** | Issue #84580 | Medium — security-conscious request from WhatsApp bot operators; multi-sweeper labels | **Possible (design needed)** |

## 7. User Feedback Summary

**Pain points expressed today:**

- **Desktop regression anxiety:** CPU burn at idle on Intel Macs (#88275) with thermal throttling — users are troubleshooting config workarounds, indicating real friction with Electron packaging.
- **Multi-backend complexity is real:** Power users routing through multiplex profiles, remote gateways, and SSH report **identity fragmentation** (#88715, #88680, #89131) — the mental model of "one app, many backends" isn't yet seamless.
- **Self-hosted pain:** Windows users hit terminal/env probe deadlocks (#73403, #89495); macOS launchd users face unbounded log growth (#88895). The **non-Linux, non-Docker experience is rougher**.
- **MCP ecosystem friction:** Slack MCP session eviction (#89576) shows the tension between Hermes's health-probe patterns and third-party MCP servers' session limits.

**Positive signals:**
- Fast fix turnaround on filed bugs (same-day PRs on #89576, #89546) suggests **maintainers are actively triaging**.
- The presence of intelligent bot-authored issues (e.g., #89549 filed by "Hermes Agent acting on behalf of user") shows **dogfooding** — the agent files its own reports.
- No complaints about release stability in today's data; v0.20.4 is a quiet consolidation.

## 8. Backlog Watch

Issues that need maintainer attention (open >30 days, unresolved, high relevance):

- **[#18885] [OPEN since May 2] — Allow memory provider tools in cron jobs via per-job `allow_memory` flag** — [Link](https://github.com/NousResearch/hermes-agent/issues/18885). 5 comments, clear use case, P3. Marked `needs-decision`? (labels not shown). **~110 days stale** — deserves a decision or a "won't fix / future" tag.
- **[#66118] [OPEN since July 17] — Profile SOUL.md/AGENTS.md identity ignored with custom Ollama provider** — [Link](https://github.com/NousResearch/hermes-agent/issues/66118). P2, `needs-repro`, but reflects a **core provider-compatibility gap**. The project now has a "provider compatibility" sweeper — this should be pinned to it.
- **[#59030] [OPEN since July 5] — `no_agent` cron jobs deliver with stale `os.environ` credentials** — [Link](https://github.com/NousResearch/hermes-agent/issues/59030). P2, affects production watchdog jobs. Root cause identified; no fix PR shows.
- **[#73403] [OPEN since July 28] — Windows ACP adapter hangs on terminal tool** — [Link](https://github.com/NousResearch/hermes-agent/issues/73403). P2, marked duplicate of #89495 (which was closed). The fix PR #69083 is referenced in the issue body — **verify it's merged**.
- **[#84580] [OPEN since Aug 12] — Supported inbound message hook with sender and message IDs** — [Link](https://github.com/NousResearch/hermes-agent/issues/84580). P3, `needs-decision`, multiple risk sweepers. Security-relevant for production bots; needs a maintainer call.

**Also notable:** The `needs-decision` label appears on **5 of the top active items** (#88715, #88680, #84580, #84178, #89582) — a **decision backlog is forming** around architecture (profile routing) and security (spillover capability binding, OAuth client ID). These are healthy discussions, but maintainers should consider explicit "decided → planned for X.Y.Z" tags to keep momentum.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-19

## Today's Overview

PicoClaw is in a period of moderate activity with 6 issues and 4 PRs updated in the last 24 hours. The project maintains a healthy pulse of community engagement, though much of the recent activity appears to be routine maintenance and staleness cleanup rather than major feature development. Two PRs were closed/merged (including the long-running `anthropic-messages` protocol feature) and two remain open. No new releases have been published, with the project still on version 0.3.1. The most significant ongoing effort remains the high-priority Web UI roadmap item (#806) which has been open since February and is now explicitly described as "refactoring now" — indicating active development. A mix of new bugs, feature requests, and configuration-level issues suggest the project is receiving real-world usage across multiple channels (IRC, LINE, Discord, Telegram, web).

## Releases

No new releases were published in the last 24 hours. The most recent version referenced across issues remains **v0.3.1**. No changelog or migration notes are available for this period.

## Project Progress

Two PRs were merged/closed in the last 24 hours:

1. **[#1158 — feat: add anthropic-messages protocol for native Anthropic API format](https://github.com/sipeed/picoclaw/pull/1158)** *(closed)* — This long-open PR (merged after 5+ months) adds support for the `anthropic-messages` protocol prefix, enabling PicoClaw to work with Anthropic-compatible API services that only support the native `/v1/messages` endpoint format. This directly addresses issue #269 and expands provider compatibility — a notable infrastructure improvement.

2. **[#3317 — feat(providers): log prompt cache tokens in LLM response debug output](https://github.com/sipeed/picoclaw/pull/3317)** *(closed)* — This PR enhances the gateway's LLM response debug logging to include prompt cache token metadata (e.g., from DeepSeek via Cloudflare AI Gateway). This is a diagnostic/observability improvement that will help users better understand token usage and caching behavior.

Additionally, two open PRs advanced in discussion:
- **[#3329](https://github.com/sipeed/picoclaw/pull/3329)** — Fix: warn on inert `webhook_host` / `webhook_port` config instead of seeding them (fixes #3328)
- **[#3314](https://github.com/sipeed/picoclaw/pull/3314)** — Fix: agent not able to execute shell commands in `customAllowPatterns` due to deny-pattern precedence

## Community Hot Topics

The most active discussions this week center on three themes:

1. **[#806 — Web UI support (roadmap, high priority)](https://github.com/sipeed/picoclaw/issues/806)** — 9 comments, 8 👍 reactions. This is the highest-signal item in the project backlog. The community strongly wants a browser-based interface to lower the entry barrier for non-technical users. The issue's metadata now explicitly states "Refactoring now," suggesting maintainers are actively working on it. This is the clearest indicator of where the project is heading next.

2. **[#3287 — Better support for long messages in IRC](https://github.com/sipeed/picoclaw/issues/3287)** — 6 comments. IRC's 512-byte limit causes PicoClaw to incorrectly split long messages into multiple pieces. The community wants PicoClaw to recognize IRCv3 message splitting and reassemble them as a single cohesive message. This is a practical usability issue for IRC users.

3. **[#3301 — /clear and auto-compression broken with dispatch rules](https://github.com/sipeed/picoclaw/issues/3301)** — 4 comments. A functional bug affecting users who route chats to non-default agents via dispatch rules. The `/clear` command and session auto-compression silently fail in these configurations.

## Bugs & Stability

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **High** | [#3301](https://github.com/sipeed/picoclaw/issues/3301) | `/clear` and session auto-compression broken for chats routed via dispatch rules (Discord/Telegram on Raspberry Pi) | Open, no fix PR yet |
| **Medium** | [#3339](https://github.com/sipeed/picoclaw/issues/3339) | Google Antigravity returns generic 429 (RESOURCE_EXHAUSTED) on every generation despite valid OAuth scopes and successful model discovery | Open, 1 comment, new (Aug 17) |
| **Medium** | [#3328](https://github.com/sipeed/picoclaw/issues/3328) | `line.settings.webhook_host` / `webhook_port` config keys are declared, defaulted, documented, but never read — silent no-op for users | Open, fix PR exists ([#3329](https://github.com/sipeed/picoclaw/pull/3329)) |
| **Low** | [#3292](https://github.com/sipeed/picoclaw/issues/3292) | High CPU usage when chat input box is focused (web frontend in Firefox) | Closed (resolved or stale-cleaned) |

The most critical outstanding bug is **#3301**, which affects core chat management functionality (session clearing and memory compression) under a common configuration (dispatch rules). The `webhook_host`/`webhook_port` issue (#3328) is a configuration trap — users set values that silently do nothing. The fix PR is ready but not yet merged.

## Feature Requests & Roadmap Signals

- **[Web UI (Issue #806)](https://github.com/sipeed/picoclaw/issues/806)** — The dominant roadmap item. Actively being refactored per issue metadata. Expect this to be the next major release feature. A web UI would dramatically expand the project's accessibility to non-terminal users.

- **[IRCv3 long-message reassembly (Issue #3287)](https://github.com/sipeed/picoclaw/issues/3287)** — Practical usability fix for IRC channels. Should be relatively contained in scope and is likely to land soon if maintainers prioritize protocol correctness.

- **[Prompt cache token logging (PR #3317, merged)](https://github.com/sipeed/picoclaw/pull/3317)** — Already merged. Costs and caching visibility is a growing user need, especially with DeepSeek and other providers exposing cache metadata.

- **Anthropic native Messages API support (PR #1158, merged)** — Already merged. Expands the ecosystem of compatible providers — likely to attract Claude-focused users.

## User Feedback Summary

**Pain points surfacing this week:**
- **Configuration silent no-ops** (#3328): Users encounter settings that appear valid but do nothing. This erodes trust in configuration discovery and is frustrating to debug.
- **IRL usability on constrained devices** (#3301): Running PicoClaw on Raspberry Pi with dispatch rules reveals that session management (clear/cleanup) silently fails — memory bloat concerns for long-running deployments.
- **IRC message fragmentation** (#3287): For IRC-centric users, long-message handling is a daily annoyance that breaks message continuity.
- **Provider-specific quirks** (#3339): Even with proper auth and model discovery, quota/429 errors from new providers (Antigravity) present opaque failures — the error messages offer no actionable path forward.

**Satisfaction signals:**
- The community continues to submit well-structured issues with environment details and reproduction steps — a sign of an engaged and technically capable user base.
- The 8 👍 on the Web UI issue indicate strong consensus on the project's direction.

## Backlog Watch

The following items need maintainer attention:

1. **[PR #3314 — customAllowPatterns shell command fix](https://github.com/sipeed/picoclaw/pull/3314)** — Open for 16 days, flagged as stale, no maintainer response. This is a genuine functional bug (config is respected by tests but not by actual behavior) that blocks agent usage of shell commands.

2. **[PR #3329 — webhook config warning fix](https://github.com/sipeed/picoclaw/pull/3329)** — Open for 8 days, addresses the no-op config issue in #3328. Small, safe change that should be reviewed promptly.

3. **[Issue #3287 — IRC long message support](https://github.com/sipeed/picoclaw/issues/3287)** — Open for 4 weeks with 6 comments and no maintainer response. Active user interest, clear scope, good candidate for community PR contribution.

4. **[Issue #806 — Web UI](https://github.com/sipeed/picoclaw/issues/806)** — The longest-open and highest-reaction issue. Metadata claims "Refactoring now" but there are no linked PRs or branch indicators. Community would benefit from maintainer transparency on timeline and architecture decisions.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date: 2026-08-19**

---

## 1. Today's Overview

NanoClaw is experiencing a significant development surge, with **39 PRs updated in the last 24 hours** — 23 still open and 16 merged or closed. The core team is driving a major architectural refactor around **database driver abstraction and async migration**, with a substantial stack of PRs (mostly by contributor `moshe-nanoco`) progressing through review. Activity is heavily concentrated on internal infrastructure improvements rather than user-facing features, suggesting a period of consolidation and hardening. One new open issue was reported regarding Codex WebSocket timeout visibility, while two older bugs were closed. No new releases were cut today, indicating the project is mid-cycle on a substantial refactor effort.

---

## 2. Releases

**No new releases were published today.** However, the PR activity strongly suggests an upcoming release featuring the async central database seam and portable database drivers, which carries breaking-change implications (see PRs #3334 and #3325, both marked `[BREAKING]`).

---

## 3. Project Progress

The most significant advancement today is the **database infrastructure refactor**, with **8 merged/closed PRs** from `moshe-nanoco` building toward portable, async database drivers:

- **[#3321](https://github.com/nanocoai/nanoclaw/pull/3321)** — Centralized the central database path
- **[#3323](https://github.com/nanocoai/nanoclaw/pull/3323)** — Made central SQL portable
- **[#3324](https://github.com/nanocoai/nanoclaw/pull/3324)** — Added async central database seam
- **[#3325](https://github.com/nanocoai/nanoclaw/pull/3325)** — **[BREAKING]** Adopted async central database seam
- **[#3326](https://github.com/nanocoai/nanoclaw/pull/3326)** — Fixed async concurrency races
- **[#3330](https://github.com/nanocoai/nanoclaw/pull/3330)** — Ran central test suites through the driver

Two **bug fixes** were also closed today:

- **[#2868](https://github.com/nanocoai/nanoclaw/issues/2868)** — `/update-skills` silent no-op for installed channels (skill-maintenance bug)
- **[#3194](https://github.com/nanocoai/nanoclaw/issues/3194)** — `/update-nanoclaw` stamping success without recoverable cutover

In addition, the **session-runtime driver seam** architecture is taking shape with PRs [#3306](https://github.com/nanocoai/nanoclaw/pull/3306) (drivers seam) and [#3307](https://github.com/nanocoai/nanoclaw/pull/3307) (host routing through the seam), positioning Docker as the built-in realization.

---

## 4. Community Hot Topics

- **[Issue #3338](https://github.com/nanocoai/nanoclaw/issues/3338) — Codex WebSocket idle retry hidden (2 comments):** The most active new issue. Reporter `ionescu77` describes a **10-minute silent failure** when the Codex Responses WebSocket stalls: Codex CLI detects its own 5-minute idle timeout and retries internally, but `codex app-server` doesn't surface that to NanoClaw, leaving users with no feedback. This reflects a broader need for **better observability and propagation of underlying service failures** to the user interface.

- **Database refactor PR stack (multiple comments distributed across ~12 PRs):** The `moshe-nanoco` PR series is the most heavily discussed work today. The stack moves the central database from synchronous `better-sqlite3` toward an **async, driver-portable abstraction**, with multiple review iterations — closed PRs #3321/#3323/#3324/#3325 were superseded by open PRs #3332/#3333/#3334/#3335/#3337, indicating active review feedback loops and refinement.

- **PR #3306/[#3307](https://github.com/nanocoai/nanoclaw/pull/3307) — Session runtime driver seam:** A purely additive architectural change introducing a seam between "what a session is" and "how it runs," with Docker as the first realization. Clean separation with no call-site changes and a fully green suite (128 files / 1,672 tests) suggests careful engineering and review.

---

## 5. Bugs & Stability

| Severity | Issue | Status | Analysis |
|----------|-------|--------|----------|
| 🔴 High | [#3338](https://github.com/nanocoai/nanoclaw/issues/3338) — Codex WebSocket idle retry hidden | Open | **10-minute silent timeouts** on Telegram requests due to undisclosed Codex WebSocket retries. No fix PR attached yet. |
| 🟠 Medium | [#3194](https://github.com/nanocoai/nanoclaw/issues/3194) — `/update-nanoclaw` success without recoverable cutover | Closed | Four failure windows where the update stamps success but the rollback point doesn't protect SQLite config, gitignored config, or external components. **Fix was closed, suggesting resolution.** |
| 🟠 Medium | [#2868](https://github.com/nanocoai/nanoclaw/issues/2868) — `/update-skills` silent no-op | Closed | Already-installed channels never refresh adapter code or pinned dependencies. **Closed, suggesting resolution.** |
| 🟢 Low | [#3340](https://github.com/nanocoai/nanoclaw/pull/3340) — `pending_approvals` instance column | Open fix | Ensures OneCLI credential cards are posted/edited by the same bot identity that owns the DM — an approval-delivery correctness fix. |
| 🟢 Low | [#3341](https://github.com/nanocoai/nanoclaw/pull/3341) — Slack service derived from credential issuer | Open fix | Pairs install-token issuer with the managed-Slack service — prevents cross-deployment auth failures. |
| 🟢 Low | [#3339](https://github.com/nanocoai/nanoclaw/pull/3339) — Fail closed on unverifiable stored sign-in | Open fix | A stored credential that can't be checked is treated as passed — a security-relevant fail-open bug. |

---

## 6. Feature Requests & Roadmap Signals

- **Session-runtime driver seam (PRs [#3306](https://github.com/nanocoai/nanoclaw/pull/3306)/[#3307](https://github.com/nanocoai/nanoclaw/pull/3307)):** The new `src/drivers/` directory explicitly positions Docker as "the built-in realization" of a session-runtime abstraction. This signals **future non-Docker session runtimes** (e.g., bare-metal processes, external orchestrators, or cloud containers) are planned. Stacked on #3306, the host now routes all session lifecycle through this seam.

- **Async, portable database drivers (PRs #3332–#3337):** The refactor's stated goal — "prepare the central database for portable drivers" — indicates support for **non-SQLite backends** (remote/installed backends are mentioned in #3330). This is a prerequisite for horizontally scaled or managed deployments.

- **New channel adapter: Webex polling ([#3343](https://github.com/nanocoai/nanoclaw/pull/3343)):** Cisco Webex support via REST polling (no inbound webhook required) — targeting enterprise Slack alternatives. Enterprise users without public webhook endpoints are a clear use case.

- **You.com MCP tools skill ([#3322](https://github.com/nanocoai/nanoclaw/pull/3322)):** A utility skill adding You.com MCP tools, continuing the pattern of expanding MCP-based skill integrations.

---

## 7. User Feedback Summary

- **Frustration with silent failures:** The newest issue (

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-19

## 1. Today's Overview

IronClaw is in a high-velocity release-validation phase, with the `1.3.0-rc.2` release addressing a critical upgrade crash-loop while 22 issues and 39 PRs churned over the past 24 hours. The project shows strong forward momentum across multiple fronts: a major refactor consolidating capability-outcome processing, a new tool-surface experiment replacing first-party coding tools, and a substantial WebUI design-system initiative. However, recurring themes around memory reliability, automation execution, and small-model failures indicate production-readiness gaps that the team is actively tackling. Overall health is solid — bugs are being closed at a good clip (6 closed issues, 15 merged/closed PRs), with significant architectural work underway.

## 2. Releases

**ironclaw-v1.3.0-rc.2** (2026-08-18)

This release candidate specifically addresses a boot-blocking regression:
- **Fixed:** Upgrades from `1.2.x` now accept and preserve the released extension `activation_state` field instead of crash-looping during startup (resolves the `1.3.0-rc.1` failure reported in [#7720](https://github.com/nearai/ironclaw/issues/7720)).
- **Fixed:** The canonical Reborn runtime image supports opt-in, public-key-only worker SSH on port 2222 while running.

**Migration Note:** Users upgrading from `1.2.x` should be able to upgrade directly to `1.3.0-rc.2` without the crash-loop seen in `rc.1`. No breaking changes called out.

## 3. Project Progress

**Merged/Closed PRs (15 total):**

- **[#7734](https://github.com/nearai/ironclaw/pull/7734) — refactor(loop): finish two abandoned test-module extractions** — Relocated 317 tests from inline modules to sibling `tests/` directories with zero production-line changes; reduces maintainability debt significantly.
- **[#7713](https://github.com/nearai/ironclaw/pull/7713) — test: exercise /benchmark on qa-automation-preview** — First end-to-end run of an `enterprise`-type suite through the `/benchmark` path on the new QA automation preview environment.

**Other activity from top PRs:**

- **[#7686](https://github.com/nearai/ironclaw/pull/7686) — refactor(runtime): centralize capability outcome processing** — PR 1 of the capability-response-normalization plan; consolidates fresh invocation, approval resume, and auth resume into a single `capability_response_processor`, replacing error-prone scattered logic.
- **[#7650](https://github.com/nearai/ironclaw/pull/7650) — feat(automations): derive run outcomes from runtime evidence** — Replaces answer-only semantic judging with deterministic, evidence-backed run assessment; makes `required_capability_ids` optional advanced verification only.
- **[#7491](https://github.com/nearai/ironclaw/pull/7491) — feat(coding): omp core-tool contract + engines + benchmark arm** — Models now get six bare-name coding tools (`read`, `write`, `edit`, `glob`, `grep`, `bash`); old file tools and derived spellings removed entirely.

## 4. Community Hot Topics

- **[#7185 — Memory not reliably recalled across conversations](https://github.com/nearai/ironclaw/issues/7185)** (CLOSED, 2 comments) — Multiple testers in the weekly champions check-in independently observed that context established in one conversation isn't reliably carried into later ones. Closed, but this remains a **critical user-facing concern**; watch for follow-up verification in `v1.3.0` or `v1.4.0`.

- **[#6879 — Automation runs are hit-or-miss](https://github.com/nearai/ironclaw/issues/6879)** (OPEN, epic for v1.3.0/v1.4.0, 1 comment) — Same stored prompt sometimes succeeds, sometimes produces nothing; audit shows structural issues: trigger fires execute as plain interactive chat turns, especially on small models (DeepSeek V4 Flash). This connects to PR [#7650](https://github.com/nearai/ironclaw/pull/7650) above, suggesting the fix is in flight.

- **[#7673 — BudgetLedger accounting refinements](https://github.com/nearai/ironclaw/issues/7673)** (OPEN, 1 comment) — Two bounded gaps in accounting: truncated launch windows double-charge, and charge durability concerns. Both err conservative (over-count → earlier stop), so no risk of cap-exceed, but users may be charged for runs that didn't complete.

- **[#7720 — 1.3.0-rc.1 crash-loops on boot after 1.2.x upgrade](https://github.com/nearai/ironclaw/issues/7720)** (OPEN, 0 comments) — Unknown field `activation_state` causes process exit 1 during composition; HTTP and SSH ports go dead. **Fixed in rc.2** — release note confirms `activation_state` preservation.

## 5. Bugs & Stability

**High severity:**

1. **[#7720 — `1.3.0-rc.1` crash-loops on upgrade from 1.2.x](https://github.com/nearai/ironclaw/issues/7720)** — Boot failure, service dead. **Fix shipped in `1.3.0-rc.2`** ✅

2. **[#7714 — libSQL shared write connection starves resource-governor journal](https://github.com/nearai/ironclaw/issues/7714)** (CLOSED) — Under PinchBench load, journal stalls ~40s waiting for writes → authority invalidation → permanent reservation leaks. Closed, presumably fixed.

**Medium severity:**

3. **[#7727 — Catalog `capabilities` artifact is mandatory but never read](https://github.com/nearai/ironclaw/issues/7727)** — Downloaded, digest-verified, written into the installed package — but never consumed. Silent dead weight; could mask security-relevant metadata.

4. **[#7726 — `IRONHUB_MANIFEST_URL` hardcoded in practice](https://github.com/nearai/ironclaw/issues/7726)** — Config knob exists but compile-time allowlist rejects any self-hosted catalog. Blocks self-hosting; contradicts configuration expectations.

5. **[#7736 — Daily failure taxonomy: weak model dominates enterprise failures](https://github.com/nearai/ironclaw/issues/7736)** — 10 non-pass tasks dominated by Qwen/Qwen3.8-27B failing multi-step completions. Model-related, but reveals the automation pipeline isn't resilient to weak models — connects to [#6879](https://github.com/nearai/ironclaw/issues/6879).

6. **[#7447 — Agent fails after calling too many tools](https://github.com/nearai/ironclaw/issues/7447)** — Redundant fetch-retry loops burn the tool-call/turn budget instead of paginating. Open; related to the omp tool-surface experiment ([#7392](https://github.com/nearai/ironclaw/issues/7392)).

**Low severity:**

- **[#7638](https://github.com/nearai/ironclaw/issues/7638) / [#7639](https://github.com/nearai/ironclaw/issues/7639)** — WebUI UX consistency (toast vs alert, shared InlineNotice); closed.

## 6. Feature Requests & Roadmap Signals

**High-likelihood for v1.4.0:**

- **[#7467 — Epic: Make Reborn durable state profile-agnostic](https://github.com/nearai/ironclaw/issues/7467)** — Profile changes shouldn't strand conversation history/secrets; migration of legacy roots needed. High-risk, high-value.
- **[#7731 — Mnesis Spike](https://github.com/nearai/ironclaw/issues/7731)** — Integrate Mnesis as a memory provider; likely aimed at fixing the memory recall issue from [#7185](https://github.com/nearai/ironclaw/issues/7185).
- **[#7732 — Sandboxing Solution with CLIs](https://github.com/nearai/ironclaw/issues/7732)** — E2E sandboxing; complements the omp tool contract.
- **[#7392 — Replace first-party coding tools with omp surface](https://github.com/nearai/ironclaw/issues/7392)** — PR [#7491](https://github.com/nearai/ironclaw/pull/7491) already implements slices 1-4; appears close to shipping.
- **[#6837 — Minimal info-level logging for growth/usage stats](https://github.com/nearai/ironclaw/issues/6837)** — Zero `info!` calls in analytics currently; small but needed for observability.

**Mid-term:**

- **[#7354 — Extensions vNext: Unified Channels, Rich Messaging, Signal](https://github.com/nearai/ironclaw/issues/7354)** — Web push and Telegram delegated-device split into separate programs.
- **[#7038 — Storybook + AI-first Design System](https://github.com/nearai/ironclaw/issues/7038)** — Being executed via PRs [#7257](https://github.com/nearai/ironclaw/pull/7257) and [#7043](https://github.com/nearai/ironclaw/pull/7043) (docs/governance), plus [#7733](https://github.com/nearai/ironclaw/issues/7733) (phases 2-3).
- **[#7681 — Slack: private unlinked-user connect + one-click link](https://github.com/nearai/ironclaw/issues/7681)** — PR [#7682](https://github.com/nearai/ironclaw/pull/7682) addresses; UX and privacy win.

**User-visible web features in flight:**

- **[#7724 — Voice-to-text in composer via NEAR AI Whisper](https://github.com/nearai/ironclaw/pull/7724)** — Browser never holds inference credential; never auto-sends.
- **[#7697 — Durable user notification inbox](https://github.com/nearai/ironclaw/pull/7697)** — Typed contracts, pagination, unread counts, read/archive lifecycle.
- **[#7735 — Run timing evidence in downloadable artifacts](https://github.com/nearai/ironclaw/pull/7735)** — Per-iteration inference duration, per-tool duration, tool-call counts in bug reports.
- **[#6994 — OOBE automation-tasks prototype](https://github.com/nearai/ironclaw/pull/6994)** — First-run onboarding; off-by-default flag.
- **[#7728 — Google Docs semantic editing tools](https://github.com/nearai/ironclaw/pull/7728)** — Structured inspection, anchored batch edits, populated tables.

## 7. User Feedback Summary

- **Memory reliability is the #1 voiced pain point** — Multiple testers in the champions program independently confirmed cross-conversation context loss ([#7185](https://github.com/nearai/ironclaw/issues/7185)). The Mnesis spike may be the direct response.
- **Automation trust is shaky** — Users report the same prompt yielding nothing useful, especially on smaller models ([#6879](https://github.com/nearai/ironclaw/issues/6879)); evidence-based judging (PR [#7650](https://github.com/nearai/ironclaw/pull/7650)) directly addresses this.
- **Upgrade confidence dented by rc.1 boot failure** — The crash-loop on 1.2.x→1.3.0 upgrade is exactly the kind of issue that erodes trust in release candidates. rc.2's prompt fix is good, but QA on upgrade paths needs strengthening.
- **Chat UX polish requests are being cheerfully addressed** — Thread-deletion toasts, shared InlineNotice, private Slack connection nudge, one-click connect links — small but visible improvements that indicate an actively-listening team.
- **Self-hosting friction** — The `IRONHUB_MANIFEST_URL` hardcode despite a config knob suggests self-hosting is a documented-but-untested path; worth prioritizing.

## 8. Backlog Watch

**Long-standing open items needing attention:**

- **[#3676 — docs: rework the security section](https://github.com/nearai/ironclaw/pull/3676)** — Original branch written in May against the `src/` monolith; rebuilt from current `main` but still open since May 15. Security documentation is critical for adoption; should be prioritized for merge.

- **[#6994 — OOBE automation-tasks prototype](https://github.com/nearai/ironclaw/pull/6994)** — Open since August 1; gated behind off-by-default flag, so low risk, but the design+plan docs may be blocked waiting on the design-system work ([#7038](https://github.com/nearai/ironclaw/issues/7038)).

- **[#6837 — Minimal info-level logging for analytics](https://github.com/nearai/ironclaw/issues/6837)** — Zero `info!` calls in the analytics crate; small scope but vital for production observability. Unanswered since July 29.

- **[#7447 — Agent fails after too many tools](https://github.com/nearai/ironclaw/issues/7447)** — Related to the omp tool-surface replacement ([#7392](https://github.com/nearai/ironclaw/issues/7392)); may be superseded once that ships.

- **[#7165 — Customer Feedback Remediation (CLOSED)](https://github.com/nearai/ironclaw/issues/7165)** — Closed with summary "TBF" — **the epic was closed without a real writeup**. If this was intentional, fine; if not, it may indicate a triage gap where feedback-driven work lost documentation.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-19

## 1. Today's Overview

LobsterAI shipped a new release (2026.8.18) centered on DeepSeek Harness (dsh) engine integration, marking the project's first experimental alternative AI engine beyond OpenClaw. Activity is high: 20 PRs were updated in the last 24 hours, with 17 merged/closed and 3 still open. The merged work spans UI refinements (sidebar search, task filtering, sites alignment), scheduled-task reliability fixes, SQLite cascade-delete corrections, and a P0 OpenClaw gateway blocker fix. The 9 active issues are all stale (last updated ~4 months ago) and remain unaddressed, representing a notable backlog of user-reported bugs. Overall project health is good on the development front, but the aging issue queue warrants maintainer attention.

**Stats:** 9 issues updated (9 open, 0 closed) · 20 PRs updated (17 merged/closed, 3 open) · 1 new release

---

## 2. Releases

### LobsterAI 2026.8.18 (2026-08-18)

- **feat: dsh engine integration** — Opt-in experimental DeepSeek Harness engine support (PR #2502)
- **feat: update dsh to rc.7** — Dependency bump to release candidate 7 (PR #2509)
- **feat: dsh process launcher** — Process lifecycle management for the dsh engine (PR #2502)
- Release branch merged into main with 23 commits, 57 files changed, +7,004/−39 (PR #2510)

**Breaking changes:** None documented. dsh is opt-in and experimental.

**Migration notes:** Users on OpenClaw should be unaffected; dsh engine is additive. Users who previously had gateway startup failures (P0 blocker, PR #1626) should upgrade — the fix removes invalid `skipMissedJobs` config fields incompatible with newer OpenClaw versions.

---

## 3. Project Progress

**Merged/Closed PRs (17 total):**

| Area | PR | Summary |
|---|---|---|
| **Release** | [#2510](https://github.com/netease-youdao/LobsterAI/pull/2510) | Merged release/2026.8.17 into main (23 commits, +7,004/−39) |
| **Engine** | [#2509](https://github.com/netease-youdao/LobsterAI/pull/2509) | Updated dsh engine to rc.7 |
| **Engine** | [#2502](https://github.com/netease-youdao/LobsterAI/pull/2502) | dsh engine integration + process launcher |
| **Auth/Models** | [#2508](https://github.com/netease-youdao/LobsterAI/pull/2508) | Retry server model load after transient failures; avoid clearing model list on reload failure |
| **Scheduled Tasks** | [#2507](https://github.com/netease-youdao/LobsterAI/pull/2507) | Cap cron run history page size to gateway max; internal pagination |
| **Settings** | [#2425](https://github.com/netease-youdao/LobsterAI/pull/2425) | Artifact auto-preview toggle (default preserves current behavior) |
| **Sidebar** | [#2481](https://github.com/netease-youdao/LobsterAI/pull/2481) | Move task search to header actions; icon-only entry |
| **Sidebar** | [#2418](https://github.com/netease-youdao/LobsterAI/pull/2418) | Multi-agent task activity filter (Codex-inspired) |
| **Sites** | [#2410](https://github.com/netease-youdao/LobsterAI/pull/2410) | Align Sites page layout with Skills/MCP views |
| **Sites** | [#2417](https://github.com/netease-youdao/LobsterAI/pull/2417) | Copy success feedback for site URLs and share codes |
| **Scheduled Task** | [#1621](https://github.com/netease-youdao/LobsterAI/pull/1621) | OS-native notifications after scheduled task completion (default off, closes #1620) |
| **Skills** | [#1583](https://github.com/netease-youdao/LobsterAI/pull/1583) | Recently used tab with usage count tracking; fixed auto-routing detection bug |
| **SQLite** | [#1597](https://github.com/netease-youdao/LobsterAI/pull/1597) | Enable `PRAGMA foreign_keys`; fix broken cascade deletes |
| **Export** | [#1615](https://github.com/netease-youdao/LobsterAI/pull/1615) | Improved session export: localized role titles, timestamps, metadata, copy-to-clipboard |
| **OpenClaw** | [#1626](https://github.com/netease-youdao/LobsterAI/pull/1626) | P0 fix: gateway startup failure from invalid `skipMissedJobs` field; modal flicker fix |
| **Avatar** | [#1629](https://github.com/netease-youdao/LobsterAI/pull/1629) | User avatar settings: presets, local upload, compression |
| **MCP** | [#1631](https://github.com/netease-youdao/LobsterAI/pull/1631) | Quick-add templates for File System, SQLite, Brave Search |
| **Docs** | [#2506](https://github.com/netease-youdao/LobsterAI/pull/2506) | DeepSeek Harness runtime setup instructions |

**Open PRs (3):**
- [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — Dependabot: electron group bump (40.2.1 → 43.4.0), open since April
- [#1628](https://github.com/netease-youdao/LobsterAI/pull/1628) — Model selector UI refactor + supplier icons + dropdown portal fix
- [#1634](https://github.com/netease-youdao/LobsterAI/pull/1634) — Global search bug fix (was agent-scoped) + UX upgrade

---

## 4. Community Hot Topics

**Most-discussed issues (all have 2 comments, no reactions):**

- **[#1614 — Add hermes-agent as optional AI engine](https://github.com/netease-youdao/LobsterAI/issues/1614)** — Request to support hermes-agent alongside OpenClaw. Notably, the project just shipped dsh engine integration, suggesting the architecture is becoming pluggable; this issue may now be actionable.

- **[#1622 — Cannot add custom model](https://github.com/netease-youdao/LobsterAI/issues/1622)** — Custom model test fails after adding; user included a screenshot but no logs. No maintainer response visible.

- **[#1627 — Client crashes on moderately complex tasks](https://github.com/netease-youdao/LobsterAI/issues/1627)** — Includes OpenClaw stdout logs showing websocket events; crash likely tied to gateway or memory pressure. This is a stability red flag.

- **[#1632 — Skills unavailable after switching to local model](https://github.com/netease-youdao/LobsterAI/issues/1632)** — After switching to a local model, previously installed skills stop working; user asks how to reinstall.

- **[#1620 — Scheduled task completion notification](https://github.com/netease-youdao/LobsterAI/issues/1620)** — Feature request that **was implemented** in PR #1621 and shipped. Good example of community-driven development.

**Hot PR threads:** The dsh engine PRs (#2502, #2509) and release PR (#2510) attracted the most attention, given the scale of the change (+7,004 lines).

---

## 5. Bugs & Stability

All 9 open issues are stale (untouched since ~2026-04), meaning **none were newly reported in the last 24h**, but all remain unfixed. Ranked by severity:

| Severity | Issue | Description | Fix Status |
|---|---|---|---|
| **P0 — Crash** | [#1627](https://github.com/netease-youdao/LobsterAI/issues/1627) | Client crashes on moderately complex tasks (OpenClaw ws logs included) | No fix PR |
| **P0 — Crash** | [#1587](https://github.com/netease-youdao/LobsterAI/issues/1587) | First-launch crash after updating to latest version (Intel Mac, screenshot + full logs attached) | No fix PR |
| **High — Core broken** | [#1589](https://github.com/netease-youdao/LobsterAI/issues/1589) | Session and scheduled-task functions both fail (Intel Mac, 2026.4.8) | No fix PR |
| **High — Data loss** | [#1617](https://github.com/netease-youdao/LobsterAI/issues/1617) | Deleted skills persist in UI; "Skill not found" on re-delete; survives restart | No fix PR |
| **High — Regression** | [#1632](https://github.com/netease-youdao/LobsterAI/issues/1632) | Skills unusable after switching to local model | No fix PR |
| **Medium — Config** | [#1622](https://github.com/netease-youdao/LobsterAI/issues/1622) | Custom model add + test fails | No fix PR |
| **Medium — UX** | [#1586](https://github.com/netease-youdao/LobsterAI/issues/1586) | Language switch incomplete (Terms, tool style sections remain Chinese) | No fix PR |

**Notable:** Today's merged PRs fixed a P0 OpenClaw gateway blocker (#1626) and SQLite foreign-key cascade deletion bug (#1597) — the latter likely relates to the skill-deletion issue (#1617), but no explicit link exists.

---

## 6. Feature Requests & Roadmap Signals

**Shipped in this release cycle:**
- ✅ **Alternative AI engine (dsh / DeepSeek Harness)** — Positioned as experimental; architecture is becoming multi-engine. Likely the foundation for supporting more engines (hermes-agent per #1614).
- ✅ **Scheduled task notifications** — Implemented from community request #1620.
- ✅ **Multi-agent task activity filter** — Codex-inspired; improves multi-agent workflow visibility.
- ✅ **Artifact auto-preview toggle** — User control over automatic preview behavior.
- ✅ **MCP quick-add templates** — Lowers barrier for common MCP setups.

**Likely next-version candidates (open PRs):**
- [#1634](https://github.com/netease-youdao/LobsterAI/pull/1634) — Global search fix + UX upgrade (addresses a real bug: search was agent-scoped)
- [#1628](https://github.com/netease-youdao/LobsterAI/pull/1628) — Model selector UI overhaul with supplier icons

**In-demand but unaddressed (from stale issues):**
- hermes-agent as an AI engine (#1614) — now more plausible given dsh precedent
- Local-model skill compatibility (#1632)

---

## 7. User Feedback Summary

**Satisfaction drivers (recently shipped):**
- Scheduled-task notifications (user-requested, delivered in ~4 months)
- Improved session export quality: localized titles, timestamps, no forced truncation (#1615)
- Fix for OpenClaw gateway startup crash — a P0 that blocked all users (#1626)

**Pain points (recurring themes):**
- **Stability on Intel Macs:** Two crash reports (#1587, #1589) on Intel Mac with the same author, suggesting platform-specific regressions.
- **Local model support is fragmented:** Users report skills breaking after switching to local models (#1632), and custom model setup fails (#1622). The local-model story feels incomplete.
- **UI state sync issues:** Skill deletion not reflecting in UI (#1617), incomplete i18n (#1586) — both suggest frontend state management gaps.
- **Complex task crashes (#1627):** Unclear if this is a memory leak, gateway issue, or OpenClaw interaction bug.

**Silence on stale issues:** None of the 9 open issues have maintainer responses. The April backlog has gone ~4 months untouched while the team focused on release work. This is the single biggest community-experience risk.

---

## 8. Backlog Watch

Issues/PRs that have been open for extended periods and need maintainer attention:

| Item | Age | Why It Matters |
|---|---|---|
| [#1614](https://github.com/netease-youdao/LobsterAI/issues/1614) — hermes-agent engine request | ~4 months | Architecture now supports dsh; this request is feasible and signals user appetite for engine choice |
| [#1627](https://github.com/netease-youdao/LobsterAI/issues/1627) — Crash on complex tasks | ~4 months | P0 stability issue; may affect many users silently |
| [#1587](https://github.com/netease-youdao/LobsterAI/issues/1587) — First-launch crash on update | ~4 months | Update-path regression on Intel Mac; high user impact |
| [#1589](https://github.com/netease-youdao/LobsterAI/issues/1589) — Sessions + scheduled tasks broken | ~4 months | Core functionality failure on Intel Mac |
| [#1617](https://github.com/netease-youdao/LobsterAI/issues/1617) — Skill deletion UI bug | ~4 months | Data-consistency bug; SQLite FK fix (#1597) may help but not confirmed |
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — Electron bump (dependabot) | ~4.5 months | Security/maintenance debt; major version bump (40→43) needs review |
| [#1632](https://github.com/netease-youdao/LobsterAI/issues/1632) — Skills break with local models | ~4 months | Local-model experience is a key differentiator; broken skills undermine it |

**Recommendation:** Prioritize a triage pass on the April backlog, confirm whether #1617 is resolved by the SQLite FK fix, and add Intel Mac stability to the regression test matrix.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Based on the GitHub data from Moltis (moltis-org/moltis) for 2026-08-19, here is the project digest:

---

# Moltis Project Digest — 2026-08-19

## 1. Today's Overview

Moltis is showing strong, sustained momentum with 8 items updated in the last 24 hours: two issues closed, five PRs merged/closed, and one new feature PR still open. The project shipped two new releases today, indicating an active release cadence. Core work this cycle focused on critical infrastructure fixes: a Podman sandbox bug (issue #1095) finally closed after two months, a settings UI data-loss bug fixed via PR #1209, and a substantial new "Files library" feature merged in PR #1206. The maintainer team appears highly responsive, with the heartbeat bug (filed 2026-08-09) being fixed within nine days by a community contributor. Overall, the project is in a healthy state with clear momentum on both feature development and bug stabilization.

## 2. Releases

Two new releases were published today:

- **20260818.08**: Latest bugfix release, likely containing the Podman sandbox fix (#1106), the heartbeat settings patch (#1209), and the OpenAI reasoning tool-call routing (#1198) that were all merged on the same day. No breaking changes noted.
- **20260818.06**: Companion release published earlier in the day, likely containing the initial batch of the day's merges. Versioning suggests a continuous-delivery pipeline rather than feature-locked milestones.

**Note for users:** If you are running Podman with Moltis, upgrading is strongly recommended to pick up the host-socket passthrough and rootless diagnostics fixes in #1106. No migration steps are indicated in the release notes.

## 3. Project Progress

Five PRs were merged/closed in the last 24 hours, spanning both infrastructure fixes and new features:

- **#1206 — Add managed Files library and Settings browser** (merged, by penso): This is the largest change of the cycle. It adds a persistent, data-directory-backed files API (list/upload/download/create/move/delete), a Finder-style settings browser, `MOLTIS_FILES_DIR` environment discovery, and read-only-by-default mounts for Docker, Podman, and Apple containers. Notably, mounts are opt-in and read-only by default — a strong security posture.
- **#1106 — fix(sandbox): support Podman escape hatches** (merged, after 2+ months open): Adds explicit, mutually exclusive escape hatches for validated Linux host-socket passthrough and privileged nested Podman. Sandboxes are recreated when mode changes, fail closed on unavailable sockets, and rootless Podman diagnostics are improved.
- **#1198 — Route OpenAI reasoning tool calls through Responses API** (merged): Built-in OpenAI requests combining function tools with `reasoning_effort` now route through the Responses API, with Chat Completions preserved when tools/reasoning are absent, including for OpenAI-compatible providers.
- **#1209 — fix(gateway): treat heartbeat.update params as a patch** (merged, by Lstarsky0): Fixes issue #1187 by ensuring heartbeat config updates merge into the existing config rather than resetting unspecified fields to defaults.
- **#1211 — fix(readme): restore broken star history chart** (merged, by CrustyMozarella): Replaces the README star chart source with a working provider that doesn't require a GitHub token.

**Open PR:** #1210 (Tesla Fleet API connector) is the only open PR and is in active review.

## 4. Community Hot Topics

The most active discussions in the last 24 hours:

- **Issue #1095 — "Podman is not working via Moltis"** (closed, 2 comments, open for ~2.5 months): The most significant community pain point resolved this cycle. The underlying need was support for users who already have Podman running on their host and want Moltis to work with it rather than requiring a nested/separate container runtime. The fix (#1106) provides explicit escape hatches for host-socket passthrough, which directly addresses this use case. The two-month duration suggests this was a hard problem involving both security validation and rootless Podman quirks.
- **Issue #1187 — "Heartbeat settings UI silently resets fields not represented by the form"** (closed, no comments): A data-loss bug where saving heartbeat settings via the UI would silently reset any config keys not present in the form to defaults. This is a classic "UI is not the source of truth" failure mode — the community expectation is that saving a form should never clobber unrelated or unknown config keys.
- **PR #1210 — Tesla Fleet API connector** (open, new today): While this is a maintainer-authored PR, it signals a growing ecosystem direction toward concrete integrations (vehicle data sync) rather than just core agent infrastructure.

## 5. Bugs & Stability

Two bugs were addressed this cycle, both resolved with fix PRs:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **High** | #1095 | Podman completely non-functional in Moltis. Blocking for all Podman-based users. | Fixed by #1106 (merged today) |
| **Medium** | #1187 | Heartbeat settings UI silently resets config fields not present in the form, causing unexpected configuration loss. | Fixed by #1209 (merged today) |

Both were fixed in the same 24-hour window, indicating strong regression-control discipline. The Podman fix was open since June 3rd (~2.5 months) — the long tail suggests this was a deliberately careful security-sensitive fix rather than neglect, given that the PR description explicitly mentions "fail closed on unavailable sockets" and "validated" host-socket passthrough.

## 6. Feature Requests & Roadmap Signals

Several signals point to near-term roadmap direction:

- **Managed Files library (#1206)** — merged today: A persistent, data-directory-backed file system with authenticated APIs and a Finder-style browser. This is a foundational feature that the Tesla connector (#1210) will likely build upon for its "local copy of vehicle data" approach, suggesting a broader pattern of "connectors keep local snapshots."
- **Tesla Fleet API connector (#1210)** — open: Read-only vehicle data sync with two dataset shapes and automatic retirement of stale items. If merged, this opens the door for more third-party data connectors (the PR description references a "connector snapshot store" as a shared mechanism).
- **OpenAI Responses API routing (#1198)** — merged: Explicit support for `reasoning_effort` with tool calls via the Responses API. This suggests the team is tracking OpenAI's API evolution closely and may deprecate Chat Completions support for reasoning workloads in future versions.
- **Community demand for Podman escape hatches (#1095, fixed)**: The explicit "privileged nested Podman" hatch suggests user demand for CI-style environments where nested containers are expected.

**Prediction for next release:** Expect the Tesla connector (#1210) to land within a week, and a minor-version bump when the Files library settles. The "connector snapshot store" pattern suggests a public API for community connectors may be on the roadmap.

## 7. User Feedback Summary

**Pain points expressed this cycle:**
- **Podman performance/functionality gap (issue #1095):** Users want Moltis to respect their existing container runtime choice. The fix was careful and security-conscious, but the two-month lead time likely frustrated affected users.
- **Config data loss (issue #1187):** The Heartbeat settings UI erasing fields is a trust-damaging bug — users found their configurations silently altered. The quick patch (nine days) likely restored confidence.
- **README star chart broken (#1211):** Minor but visible — a broken chart on the project homepage suggests tooling drift.

**Positive signals:**
- Community contributors are actively submitting fixes (Lstarsky0 for #1209, CrustyMozarella for #1211), indicating a healthy contributor funnel and onboarding process.
- Maintainer (penso) is highly active, authoring the two largest changes of the cycle (#1206, #1198) and responding quickly to community-reported issues.

**Satisfaction trajectory:** Net positive — both real bugs fixed same-day, new features merged, and the release cadence is steady.

## 8. Backlog Watch

**Issues/PRs needing maintainer attention:**

- **PR #1210 — Tesla Fleet API connector** (open, created today): Currently the only open PR. It introduces a new connector type and a "snapshot store" pattern, which likely warrants careful review before merge. No maintainer response within the last 24h — needs review or feedback.

**No long-stale issues are visible in this data window.** The oldest closed item (#1095, June 3rd) was resolved today. Given that both closing items were bugs that took between 9 days and 2.5 months to resolve, the project does not appear to be accumulating a large stale backlog. No blocked or unaddressed community PRs are evident in this window.

---

**Overall project health: Strong.** Active maintainers, responsive triage, steady release cadence, growing feature surface, and a contributing community. The main risk is scope creep from a large feature like the Files library plus connectors; watch for documentation and stability follow-ups.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-19

## 1. Today's Overview

CoPaw (QwenPaw) is showing elevated but **healthy** activity with 46 issues and 50 PRs updated in the last 24 hours — a ratio suggesting active community engagement paired with a responsive maintainer team. The project is in a **post-2.1.0 stabilization phase**: no new releases today, but 19 PRs were merged/closed (38% closure rate) while 31 remain open. Notably, several `first-time-contributor` PRs are in the pipeline, indicating healthy external contribution inflow. **Key concern signals**: multiple open bugs around MCP transport resilience (issues #6470, #5900, #7053) and agent task auto-stopping (#6921) are accumulating without confirmed fixes in the merge queue. No critical security advisories were published today, though a MalwareBytes false-positive concern (#6775) remains unresolved and could impact Windows user trust.

---

## 2. Releases

**No new releases today.** The latest published version remains **v2.1.0** (Desktop & core). No migration notes or breaking-change announcements to report.

---

## 3. Project Progress

**Merged/Closed PRs (19 total)** — the most substantive advances:

| PR | Title | Signal |
|----|-------|--------|
| [#7069](https://github.com/agentscope-ai/QwenPaw/pull/7069) | fix(console): render data-URL images in historical messages on session reload | Fixes #7051; addresses a UI regression where historical images were broken after session reopen |
| [#7064](https://github.com/agentscope-ai/QwenPaw/pull/7064) | fix(cli): sync top-level text on cron update --text for agent jobs | Fixes #7048; a CLI consistency fix for agent-type cron jobs |
| [#7072](https://github.com/agentscope-ai/QwenPaw/pull/7072) | feat(console): add background chat task list API | Implements part of proposal #7056; enables multi-agent coordination visibility — a first step toward better task observability |
| [#6617](https://github.com/agentscope-ai/QwenPaw/pull/6617) | fix(providers): honor the Retry-After cap on the streaming retry path | Under Review, now closed/merged; improves rate-limit handling on streaming paths — relevant to #6921's auto-stop symptoms |
| [#7046](https://github.com/agentscope-ai/QwenPaw/pull/7046) | execute_shell_command mangles heredoc/multi-line commands (closed as fixed) | Shell command fidelity fix — important for developer-heavy workloads |

**Notable open PRs under active review (signal: likely to merge soon):**
- [#7087](https://github.com/agentscope-ai/QwenPaw/pull/7087) — localize remote media URLs client-side before model requests (directly addresses #7110's unreachable-image hang)
- [#7057](https://github.com/agentscope-ai/QwenPaw/pull/7057) — add user-local bin dirs to subprocess PATH (fixes a common systemd/Docker pain)
- [#7066](https://github.com/agentscope-ai/QwenPaw/pull/7066) — persist rotated refresh_token for OAuth2 MCP providers (fixes #7053)

---

## 4. Community Hot Topics

**Most active issues by engagement:**

1. **[#6684 — Channel retry feature (10 comments)](https://github.com/agentscope-ai/QwenPaw/issues/6684)** — *Enhancement request.* Using self-hosted Matrix, QwenPaw races ahead of the Matrix service on startup, failing without retry/health-check. **Underlying need**: resilience for self-hosted federated infrastructure. The user must manually re-save channels after every server start.

2. **[#6921 — Agent stops mid-task without notice (8 comments)](https://github.com/agentscope-ai/QwenPaw/issues/6921)** — *Bug.* On Windows 11 / v2.1beta2, multi-step tasks stop after the model outputs a plan ("Now 2.1, 3.1, 3.2. Let me do all three.") with no visible error; user must say "continue" to resume. **Underlying need**: task continuity and explicit completion signaling — a UX-critical issue for agent trust.

3. **[#7102 — Freeze longer than 10 minutes (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/7102)** — *Bug.* QwenPaw Desktop 2.1.0 freezes (no tokens, no thinking output) for 5–10+ minutes with GLM 5.3. User speculates provider issue but notes it happens across models. **Underlying need**: visual progress or cancellation options during long provider stalls.

4. **[#7011 — Console stop cancels active Feishu session (7 comments)](https://github.com/agentscope-ai/QwenPaw/issues/7011)** — *Bug.* Session identity values crossed between two UI sessions; a Console stop request killed an active Feishu conversation. **Underlying need**: proper session isolation across UI/channel boundaries.

5. **[#6470 — MCP driver hardcodes SSE client (5 comments)](https://github.com/agentscope-ai/QwenPaw/issues/6470)** — *Bug.* MCP driver ignores `transport: streamable_http` config, hardcoding `sse_client`. **Underlying need**: protocol-configuration fidelity for MCP servers — critical for enterprise integrations.

---

## 5. Bugs & Stability

**Ranked by severity:**

| Severity | Issue | Description | Fix status |
|----------|-------|-------------|------------|
| 🔴 **Critical** | [#7110](https://github.com/agentscope-ai/QwenPaw/issues/7110) | Unreachable image URLs in conversation history permanently break the session — `/clear` is the only remedy | PR [#7087](https://github.com/agentscope-ai/QwenPaw/pull/7087) open (media URL localization) |
| 🔴 **Critical** | [#7102](https://github.com/agentscope-ai/QwenPaw/issues/7102) | 5–10+ min freeze with no output across models | No confirmed fix; possibly provider-side (GLM) but needs client resilience |
| 🟠 **High** | [#7074](https://github.com/agentscope-ai/QwenPaw/issues/7074) | High-frequency crashes requiring page refresh; session state JSON loading issues | No fix PR yet — needs maintainer triage |
| 🟠 **High** | [#7082](https://github.com/agentscope-ai/QwenPaw/issues/7082) | `_StructuredOutputDynamicClass` Pydantic error on console channel init (v2.1.0) | No fix PR — Pydantic rebuild needed |
| 🟠 **High** | [#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) | Agent stops after planning without executing; no user-visible notice | Could be related to [#6617](https://github.com/agentscope-ai/QwenPaw/pull/6617) retry logic; needs verification |
| 🟡 **Medium** | [#6470](https://github.com/agentscope-ai/QwenPaw/issues/6470) | MCP transport config ignored; SSE hardcoded | Open; no PR referencing |
| 🟡 **Medium** | [#7053](https://github.com/agentscope-ai/QwenPaw/issues/7053) | OAuth2 refresh token rotation not persisted — MCP permanently degrades | PR [#7066](https://github.com/agentscope-ai/QwenPaw/pull/7066) under review |
| 🟡 **Medium** | [#5900](https://github.com/agentscope-ai/QwenPaw/issues/5900) | streamable_http MCP session termination → client permanently skipped | Open since July 9 — **needs maintainer attention** |
| 🟢 **Low** | [#7121](https://github.com/agentscope-ai/QwenPaw/issues/7121) | Flaky nightly test on macOS timing assertion | CI flake; maintainers aware |

**Regression watch**: [#7065](https://github.com/agentscope-ai/QwenPaw/issues/7065) — after 7 rounds of discussion, chat history truncates to last 3–4 messages (v2.1.0 regression, closed?). [#7039](https://github.com/agentscope-ai/QwenPaw/issues/7039) — v2.1.0 creates duplicate/phantom sessions spontaneously (closed, but worth verifying the fix).

---

## 6. Feature Requests & Roadmap Signals

**Requests with strong community pull (by engagement/comments):**

| Request | Issue | Likelihood in next version |
|---------|-------|---------------------------|
| **Channel retry & health-check** (esp. Matrix) | [#6684](https://github.com/agentscope-ai/QwenPaw/issues/6684) | **High** — core reliability gap, 10 comments |
| **Manual single-message deletion in chat** | [#4001](https://github.com/agentscope-ai/QwenPaw/issues/4001) | **Medium-High** — long-standing (since May), closed, 5 comments; UX parity with WeChat/slack |
| **Per-agent/per-session reasoning_effort override** | [#7062](https://github.com/agentscope-ai/QwenPaw/issues/7062) | **High** — aligns with multi-agent workflows; likely config-layer change |
| **Background task list API** | [#7056](https://github.com/agentscope-ai/QwenPaw/issues/7056) → PR [#7072](https://github.com/agentscope-ai/QwenPaw/pull/7072) | **In progress** — merged; expect console UI in next minor |
| **Collapsible thinking/tool-call traces in results** | [#6260](https://github.com/agentscope-ai/QwenPaw/issues/6260) | **Medium** — UX polish; user explicitly requested "show results first, process second" |
| **Search/filter in skill pool import page** | [#7090](https://github.com/agentscope-ai/QwenPaw/issues/7090) | **High** — trivial to implement, strong UX win for power users |
| **Plugin API system_prompt permission** | [#7052](https://github.com/agentscope-ai/QwenPaw/issues/7052) | **Medium** — enterprise-facing; privacy/security sensitive |
| **Turn-off option for file preview** | [#7039](https://github.com/agentscope-ai/QwenPaw/issues/7039) (second part) | **High** — simple toggle, frequent pain |

**Roadmap signal from PRs**: [#7112](https://github.com/agentscope-ai/QwenPaw/pull/7112) — *"isolated local QwenPaw Pro control plane"* (multi-user, tenant-scoped) is a **draft** PR, signaling a **Pro/Enterprise tier direction**. Also [#6515](https://github.com/agentscope-ai/QwenPaw/pull/6515) adds Volcengine MiMo V2.5 providers — provider breadth expansion continues.

---

## 7. User Feedback Summary

**Expressed pain points (frequency-weighted):**

- **Task continuity trust** — #6921's "stops mid-task without saying anything" is the single most trust-damaging bug reported; users must manually prompt "continue" to resume. This erodes confidence in unattended operations.
- **Self-hosted / Matrix reliability** — #6684: users on self-hosted infra feel punished — no retry, no health-check, manual reconnect required. *"每次服务器启动后都需要手动重新保存一次频道"* (must manually re-save channels after every server start).
- **MCP integration frustration** — #6470, #5900, #7053 collectively describe a pattern: *config not honored*, *reconnection not attempted*, *auth permanently degrades*. Enterprise users (XMind, custom servers) are hitting walls.
- **UI / session hygiene** — #7110 (one bad image kills a session), #7074 (random crashes needing refresh), #7039 (phantom sessions), #7065 (history truncation) — all contribute to a sense that **v2.1.0 regressed some UX fundamentals** despite the feature wins (LaTeX rendering praised in #7039).
- **Security anxiety** — #6775: MalwareBytes flagged the Windows Desktop build; the user said *"I'm uninstalling until I hear back."* This is a trust emergency vector. Even if a false positive, the communication gap is damaging.

**Positive signals**: #7039 explicitly praises v2.1.0's formula rendering ("公式显示正常了！"). The "first-time-contributor" PR pipeline (6+ PRs) suggests the project is **welcoming and contributors see quick momentum**.

---

## 8. Backlog Watch

**Issues/PRs needing maintainer attention:**

| Item | Age | Why it matters |
|------|-----|----------------|
| [#5900](https://github.com/agentscope-ai/QwenPaw/issues/5900) — MCP streamable_http no auto-reconnect | Since **July 9** | 40+ days open; core MCP reliability; no assignee visible |
| [#6775](https://github.com/agentscope-ai/QwenPaw/issues/6775) — MalwareBytes Trojan false-positive | Since **Aug 7** | User-facing trust issue; user may churn; needs official statement |
| [#6470](https://github.com/agentscope-ai/QwenPaw/issues/6470) — MCP driver ignores transport config | Since **July 26** | Protocol-level bug; directly contradicts documented config surface |
| [#7005](https://github.com/agentscope-ai/QwenPaw/issues/7005) — Sandbox breaks `uv run` (~/.cache/uv) | Since **Aug 13** | Docs-recommended workaround fails; PR [#7116](https://github.com/agentscope-ai/QwenPaw/pull/7116) addresses it — **needs expedited review** |
| [#7121](https://github.com/agentscope-ai/QwenPaw/issues/7121) — Flaky macOS nightly test | Since **Aug 18** | Test-stability debt; watch for growing flake count |
| [#6764](https://github.com/agentscope-ai/QwenPaw/pull/6764) — CI gate on main mergeability | Open since **Aug 6** | Directly addresses a past incident (#6418 merged with failing tests); needs final review — this is *process-level* health |

---

**Overall assessment**: CoPaw is in a **post-2.1.0 hardening phase** with a healthy contributor cadence and responsive triage (16 closed issues in 24h), but carries **accumulating MCP-layer technical debt** (#5900 is oldest at 40+ days) and a **few high-severity UX regressions** in v2.1.0 (session hangs, phantom sessions, history truncation) that are eroding user confidence. The "Pro control plane" draft PR signals strategic expansion toward enterprise multi-tenancy — early days, but a significant direction indicator.

*Project health score: 7/10 — strong momentum, moderate backlog debt, two trust-risk vectors (security communication + task continuity).*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-19

## 1. Today's Overview

ZeroClaw shows a highly active but **stalled merge pipeline** as of 2026-08-19. While the project saw 50 issues and 50 PRs updated in the last 24 hours, only 4 PRs were merged or closed, and **0 new releases were published** — suggesting a maintenance backlog is accumulating. The project is in a **heavy review phase**: 12 PRs are explicitly marked `do-not-merge` and 16 carry `needs-maintainer-review`, indicating significant work is ready but bottlenecked on maintainer bandwidth. The issue tracker is dominated by **accepted, no-stale enhancement requests** (25+ items), pointing to a feature-rich roadmap that is outpacing delivery. Despite this, the community remains engaged with substantive technical discussions around architecture consolidation, security hardening, and Windows platform support.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release activity appears to be trailing behind the large volume of merged code awaiting versioning. Users tracking stable builds should monitor the `[channels.session_ttl_hours]`, provider credential rotation, and Windows self-update fixes (see PRs #10009, #10003, #7853) for inclusion in the next cut.

## 3. Project Progress

Only 4 PRs merged/closed in the last 24 hours, with the most notable being:

- **#10009** *(merged)* — [fix(memory): key conversation autosave suppression on turn origin](https://github.com/zeroclaw-labs/zeroclaw/pull/10009) by JordanTheJet. Fixes a critical bug where synthetic heartbeat/cron prompts bypassed conversation autosave suppression filters, potentially polluting persistent memory with redundant context. This is a `priority:p1` fix with `risk:high`.
- **#10097** *(closed)* — [ci: Advisory scan failed — 2026-08-18](https://github.com/zeroclaw-labs/zeroclaw/issues/10097) by Audacity88. Automated dependency-scan failure tracker closed, indicating a temporary security-scan alert was resolved or acknowledged.

**Also closed (pre-existing issue trackers):** #8563 (SOPs not available in web dashboard — resolved), #7415 (RFC for unified turn engines — executed via PR #7540), #8059 (policy cleanup for deny.toml/audit.toml — completed), #3542 (webhook agent mode — shipped), #5833 (session ownership model — implemented).

**Key architectural progress visible in open PRs (blocked on review):**
- **#10003** — [fix(providers): account Reliable rejected attempts exactly](https://github.com/zeroclaw-labs/zeroclaw/pull/10003) (XL, `do-not-merge`): Precise accounting for rejected vs. accepted provider attempts, preserving exact configured usage across retries/failover.
- **#9420** — [fix(anthropic): support stored OAuth profiles](https://github.com/zeroclaw-labs/zeroclaw/pull/9420) (XL, `do-not-merge`): Adds explicit `auth_mode = "oauth"` for Anthropic aliases via stored profiles.
- **#9013** — [refactor(config)!: move TodoWrite display config from the daemon into zerocode](https://github.com/zeroclaw-labs/zeroclaw/pull/9013): Breaking config change moving display concerns to the client layer.
- **#9451** — [refactor(observability)!: retire dormant DORA telemetry](https://github.com/zeroclaw-labs/zeroclaw/pull/9451): Removes unused DORA collector and Prometheus deployment metrics.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal deeper community concerns:

1. **[#8303 — RFC: Goal mode v1 (22 comments, 1 👍)](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)**: The community is actively debating the scope of bounded, multi-turn foreground objectives. The RFC trimmed initial scope, and the 22-comment thread suggests users are pushing for durable task execution. Expect this to shape v0.9+ agent capabilities.

2. **[#7462 — 74 test failures on Windows (17 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)**: This is the single most-discussed *bug* in the project. The Windows platform story is a recurring community pain point (see also #7910 for Windows self-update test coverage, #9291 for AppImage detection). The comment count signals strong demand for first-class Windows support.

3. **[#7929 — Unify slash-command registries (8 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/7929)**: Users are frustrated with UX fragmentation across web UI, TUI, and channel runtimes. This is a "quality of life" issue that, if resolved, will significantly improve multi-surface consistency.

4. **[#8519 — Reconcile cargo-audit ignores and remediate wasmtime-wasi CVEs (6 comments)](https://github.com/zeroclaw-labs/zeroclaw/issues/8519)**: Security-conscious users are tracking dependency hardening. The recent CI advisory-scan failure (#10097) adds urgency to this thread.

## 5. Bugs & Stability

**Critical (S1/priority:p1):**
- **[#7462 — 74 Windows test failures](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)**: Unix-only test commands, path semantics, console encoding (code page 936). **No fix PR yet** — this is the highest-severity unresolved bug.
- **[#8563 — SOPs unavailable in web dashboard](https://github.com/zeroclaw-labs/zeroclaw/issues/8563)**: S1 workflow blocker; **CLOSED as resolved**.
- **[#8642 — MCP/tool-schema cloning drives unbounded RSS growth](https://github.com/zeroclaw-labs/zeroclaw/issues/8642)**: Memory leak in agent loop causing OOM in WSL2. Split from #5542; **no fix PR yet**.
- **[#10009 — Conversation autosave suppression bypass](https://github.com/zeroclaw-labs/zeroclaw/pull/10009)** *(merged yesterday)*: Fixed heartbeat/cron prompts bypassing memory filters.

**High (S2, priority:p1/p2):**
- **[#8410 — Channel tasks need intentional no-reply outcome](https://github.com/zeroclaw-labs/zeroclaw/issues/8410)**: Conditional tasks still send unwanted visible responses.
- **[#10107 — Google STT API keys in URLs](https://github.com/zeroclaw-labs/zeroclaw/pull/10107)** *(open, fresh)*: Security fix moving API keys to headers; critical for proxy-log hygiene.
- **[#9402 — Docker sandbox nested inside Docker runtime](https://github.com/zeroclaw-labs/zeroclaw/pull/9402)**: Container boundary violation risk; `do-not-merge` pending review.
- **[#9830 — Full browser automation not opt-in](https://github.com/zeroclaw-labs/zeroclaw/pull/9830)**: `browser` tool force-merged into auto-approve list — unauthorized automation risk.

## 6. Feature Requests & Roadmap Signals

High-priority accepted features (`status:accepted`, `no-stale`) likely for next release:

1. **#8303 — Goal mode v1 (RFC)**: Bounded foreground Matrix work. The 22-comment engagement suggests maintainers will prioritize this for the next major release.
2. **#8134 — Channel session TTL reset**: Existing config param (`session_ttl_hours`) waiting on implementation. Low-risk, high-value token reduction.
3. **#7929 — Unified slash-command registries**: Clear UX win across all surfaces. Predicted for next minor release given architectural alignment.
4. **#8367 — Derived capability readiness for agent guidance**: Lets agents distinguish "unsupported" from "disabled" capabilities. Advanced, p3 but architecturally significant.
5. **#9998 — Session-scoped persistent prompt attachments (RFC)**: Newest RFC (Aug 14), addresses objective loss after history trimming. Watch for scope discussions.

**Emerging signals:** The cluster of Zerocode-related feature requests (#8383, #8650, #9341) indicates the project is investing heavily in the TUI/dashboard experience. The zerorelay milestone (#8358) suggests upcoming NAT-traversal capabilities for daemon access.

## 7. User Feedback Summary

**Most vocal pain points:**
- **Windows support deficiency**: The 74-failure test suite (#7462) plus #7910, #9291 show users are actively running ZeroClaw on Windows and hitting real regressions. Repeated "Distinguished Contributor" activity from Windows testers (NiuBlibing) indicates this is a strategic gap.
- **Configuration fragmentation**: Multiple issues (#7929, #8584, #9013) reflect user frustration with settings split across web, TUI, channels, and daemon. The community is pushing for a unified configuration surface.
- **Provider reliability**: PRs #10003, #9419, #9420 (Reliable attempts, credential rotation, OAuth profiles) address user pain around retries, rate limits, and auth complexity. The comment volume on #8519 shows security-sensitive users are watching dependency hygiene closely.
- **Operational UX gaps**: Requests for active log paths (#8650), runtime context display (#8383), and no-reply outcomes (#8410) show users want more introspection and control over agent behavior.

**Satisfaction signals:** The high ratio of `status:accepted` issues (≈50%) plus the density of `distinguished contributor` / `trusted contributor` tags suggests a healthy, engaged core community. The RFC process (#8303, #9998, #7415) shows maintainers are consulting the community for architecture decisions. The wave of 46 dependency bumps in #9808 indicates active maintenance by maintainers responding to security concerns.

## 8. Backlog Watch

**Long-unanswered or at-risk items needing maintainer attention:**

- **[#7462 — Windows test failures](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)**: Created June 10, 17 comments, still unassigned. The project is shipping Windows fixes (#7853) without regression coverage — this needs a dedicated owner.
- **[#8519 — wasmtime-wasi CVE remediation](https://github.com/zeroclaw-labs/zeroclaw/issues/8519)**: Accepted but no `priority` label change in a month. The CI scan failure (#10097) will force escalation.
- **[#8642 — MCP memory leak](https://github.com/zeroclaw-labs/zeroclaw/issues/8642)**: p1, help-wanted, but no linked PR. OOM issues degrade trust quickly.
- **[#8309 — Remove orphaned SkillForge engine](https://github.com/zeroclaw-labs/zeroclaw/issues/8309)**: Unwired feature from Feb landing; decision pending for over a month.
- **[#5833 — Session ownership model (closed but lingering)](https://github.com/zeroclaw-labs/zeroclaw/issues/5833)**: Closed as implemented but the mitigation described is "tools not registered by default" — a band-aid that should be revisited.
- **Biggest concern — the `do-not-merge` pile**: 12 PRs (incl. #10003, #9013, #9104, #9194, #9203, #9402, #9419, #9420, #9451, #9515, #9609, #9748, #9772, #9830) have been waiting for maintainer review for up to 3 weeks. These represent significant security, provider, and channel improvements that are stuck. Maintainers should triage this queue as a top priority to unblock the roadmap.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*