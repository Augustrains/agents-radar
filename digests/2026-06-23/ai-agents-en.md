# OpenClaw Ecosystem Digest 2026-06-23

> Issues: 261 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-23 01:58 UTC

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

Here is the OpenClaw project digest for **2026-06-23**.

---

## OpenClaw Project Digest — 2026-06-23

### 1. Today's Overview
Project activity remains extremely high, with 261 issues and 500 PRs updated in the last 24 hours, signaling a mature but fast-moving codebase. A new beta release (`v2026.6.10-beta.2`) was cut, introducing automatic fast mode for talks and more reliable model routing. However, the project continues to wrestle with a cluster of critical **P0/P1 stability bugs**, particularly around session locking, memory leaks, and delivery failures. While maintainer throughput appears strong (58 merged/closed PRs today), the volume of open items (442 open PRs) suggests a backlog that could risk slowing down future iteration.

### 2. Releases
- **v2026.6.10-beta.2** ([openclaw/openclaw releases](https://github.com/openclaw/openclaw/releases)):
    - **Highlights:**
        - **Automatic fast mode for talks:** OpenClaw can now enable fast mode for short conversational turns, then return to normal mode for longer runs with bounded fallback and delivery behavior. (#85104)
        - **More reliable model routing:** Improvements to routing logic, reducing fallback failures.
    - **No breaking changes or migration notes** have been called out in the release body.

### 3. Project Progress
In the last 24 hours, **58 PRs were merged or closed**, advancing work across several areas:
- **CI/Infrastructure:** PR #95909 fixed Android CI by switching to the available SDK platform. PR #95898 simplified the maturity scorecard QA evidence inputs, and PR #95901 restored the maturity scorecard renderer.
- **Memory Core:** PR #95916 improved error guidance when `node:sqlite` is unavailable, steering users toward a Node runtime with SQLite support rather than misdirecting them to provider config.
- **Platform/Fixes:** PR #95914 fixed a WhatsApp reply-to-bot flow where the bot accidentally replied to the wrong native message. PR #95697 landed a major performance improvement that reduces hot-path linear scans and redundant I/O.
- **Safety Monitoring:** PR #95911 added a new continuous safety monitor for long-lived Codex sessions, capable of stopping unsafe turns via app-server APIs (pilot/internal feature).

### 4. Community Hot Topics
The community is heated about two recurring failure modes: **session write-locks** and the **gateway memory leak**.

- **#91588 (P0): Critical: Gateway Memory Leak** ([link](https://github.com/openclaw/openclaw/issues/91588)) — 13 comments, 1 👍. RSS growth from 350MB to 15.5GB over days, causing repeated OOM crashes. This is the highest-severity open bug and is blocking stable operation for self-hosted users. No fix PR linked yet.
- **#88312 (P1): Regression: Codex turn-completion stall** ([link](https://github.com/openclaw/openclaw/issues/88312)) — 17 comments, 4 👍. A regression that began in 2026.5.27, where multi-tool agent turns fail with "Codex stopped before confirming the turn was complete." This is a regression of a previously fixed issue (#84076 / #85107).
- **#88838 (P1): SQLite migration via accessor seam** ([link](https://github.com/openclaw/openclaw/issues/88838)) — 34 comments, 1 👍. A deep, ongoing technical discussion about migrating session/transcript storage to SQLite. It is the most-commented issue, indicating a high level of maintainer and contributor engagement on core architecture.
- **#86538 (P1): Session write-lock timeouts** ([link](https://github.com/openclaw/openclaw/issues/86538)) — 13 comments, 1 👍. A persistent frustration where Session JSONL write-lock timeouts block delivery lanes, causing surface-level failures without clear diagnostics.

### 5. Bugs & Stability
Several impactful bugs were reported or remain active, with a high concentration of session-state and message-loss impacts.

| Issue ID | Severity | Title | Fix PR Exists? |
|----------|----------|-------|----------------|
| #91588 | **P0 (Critical)** | Gateway Memory Leak — RSS grows to 15.5GB | No |
| #88312 | **P1** | Codex turn-completion stall (regression) | No (linked PR #85107 was previous fix) |
| #95833 | **P1** | Subagent abort-settle fails to release `.jsonl.lock`, permanently breaking session | No |
| #95760 | **P1** | NVIDIA Build provider stream cuts mid-tool-calls, session enters zombie state | No |
| #95623 | **P1** | tool_use.id sanitizer misses OpenAI-responses composite id → bricks session on failover | No |
| #95495 | **P1** | 2026.6.9 silently relocates memory store with no migration, forcing full re-embed | No (linked PR open) |
| #94251 | **P1** | Ollama remote provider streaming not consumed — model_call never progresses | No |
| #90288 | **P1** | Non-Anthropic models output tool calls as plain text instead of `tool_use` blocks | No |

### 6. Feature Requests & Roadmap Signals
- **#90370 (P3): Support PostgreSQL instead of SQLite as internal storage** ([link](https://github.com/openclaw/openclaw/issues/90370)) — 11 comments, 2 👍. The most active feature request. Users running Postgres want to avoid managing two databases. Given the ongoing SQLite migration work (#88838) and the architectural complexity, this is **unlikely** to appear in the next minor release, but the high engagement suggests it will make the roadmap eventually.
- **#95724 (P2): Index memory by source directory, not by agent** ([link](https://github.com/openclaw/openclaw/issues/95724)) — 5 comments, 1 👍. Users with multiple agents sharing a workspace are forced to maintain duplicate vector stores. This is a smaller, more targeted performance fix and could land in a **.10.x or .11.x** hotfix.
- **#92516 (P1): Containerized deploys can't use externalized channel plugins** ([link](https://github.com/openclaw/openclaw/issues/92516)) — 6 comments. A blocker for self-hosted container users. Since channel unbundling is recent, a fix is likely prioritized for the next cycle.

### 7. User Feedback Summary
- **Pain Point — Session reliability:** Multiple users report "Something went wrong" errors after subagent timeouts because `.jsonl.lock` files are not released (#95833, #86538). This is eroding trust in the subagent/long-run paradigm.
- **Pain Point — Silent regressions:** Users express frustration that upgrades like 2026.6.9 can silently relocate memory stores (#95495) or break Codex usage UI (#93041) without warnings. The community is calling for better upgrade-time validation.
- **Pain Point — Diagnostics:** Operators of the gateway memory leak (#91588) are forced to build custom OOM monitoring because built-in diagnostics do not surface the leak path. The request for owner diagnostics in #86538 echoes this need.
- **Use Case — Multi-platform:** Users on Discord, Telegram, and Slack all report lane retention and delivery failures (#85822, #95248), suggesting a systemic issue with the delivery pipeline that affects all platforms equally.

### 8. Backlog Watch
The following high-severity items have not received a fix PR and need maintainer escalation:

- **#91588 (P0): Gateway Memory Leak** ([link](https://github.com/openclaw/openclaw/issues/91588)) — 14 days since opening, still no fix PR. This is the most critical open bug.
- **#88312 (P1): Codex turn-completion stall** ([link](https://github.com/openclaw/openclaw/issues/88312)) — 24 days since opening. A regression of a previously fixed issue, indicating the fix may have been incomplete.
- **#86538 (P1): Session write-lock timeouts** ([link](https://github.com/openclaw/openclaw/issues/86538)) — 29 days since opening. A chronic failure pattern with no fix PR.
- **#52951 (P1): `tools.fs.roots` — per-agent filesystem roots** ([link](https://github.com/openclaw/openclaw/pull/52951)) — 3 months old open PR. Huge feature (XL size) with high merge-risk flags. Needs maintainer review to decide if it progresses or is closed.
- **#85822 (P1): Silent 48s post-run retention on Discord** ([link](https://github.com/openclaw/openclaw/issues/85822)) — 31 days since opening. Performance issue with no fix PR and a "needs-live-repro" label, suggesting it is difficult to diagnose.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

**Cross-Project Ecosystem Report: AI Agent Open-Source Landscape**
**Date:** 2026-06-23

### 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is experiencing a period of **intense, multi-front development**, characterized by high community engagement and a clear shift from experimental prototypes toward production-grade reliability. Projects are converging on a common set of architectural challenges—including session state durability, multi-channel delivery reliability, and plugin/tool security—while diverging in their core philosophies (monolithic reference stacks vs. modular, extensible frameworks). Activity levels are uneven: a few projects dominate the conversation with hundreds of daily updates, while others have stalled. The landscape is mature enough for users to form strong preferences on stability, which is becoming a key differentiator as bug regressions erode trust in rapidly iterating codebases.

### 2. Activity Comparison

The following table summarizes the last 24 hours of activity across all tracked projects. "Health Score" is an inferred qualitative measure based on PR closure rate, severity of open bugs, and release cadence (Scale: 🔴 Critical Risk, 🟡 Needs Attention, 🟢 Stable, 🟣 Mature).

| Project | Issues Updated | PRs Updated | Release Today | Health Score |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 261 | 500 | v2026.6.10-beta.2 | 🟡 Needs Attention |
| **Hermes Agent** | 50 | 50 | None | 🟡 Needs Attention |
| **ZeroClaw** | 50 | 50 | None | 🟢 Stable (High Velocity) |
| **CoPaw** | 22 | 50 | None | 🟡 Needs Attention |
| **NanoBot** | - | 27 | v0.2.2 🎉 | 🟢 Stable |
| **IronClaw** | 18 | 23 | None | 🟢 Stable (Intense Dev) |
| **PicoClaw** | 3 | 17 | None | 🟢 Stable |
| **LobsterAI** | 5 | 14 | None | 🔴 Critical Risk |
| **NanoClaw** | 0 | 6 | None | 🟢 Stable |
| **NullClaw** | 0 | 2 | None | 🟣 Mature (Low Activity) |
| **TinyClaw** | 0 | 0 | None | 🟣 Mature (Dormant) |
| **Moltis** | 0 | 0 | None | 🟣 Mature (Dormant) |
| **ZeptoClaw** | 0 | 0 | None | 🟣 Mature (Dormant) |

### 3. OpenClaw’s Position

OpenClaw remains the **undisputed center of gravity** in the ecosystem, functioning as the core reference implementation. Its advantages are clear: community engagement is an order of magnitude larger than any peer, attracting the most bug reports, feature requests, and outside contributions. This centrality, however, is a double-edged sword. The project's 24-hour update volume (500 PRs, 261 issues) indicates a system under constant stress. While peers like NanoBot and IronClaw can ship "stable" releases with high confidence, OpenClaw must manage a **growing list of critical (P0/P1) stability bugs**—memory leaks, session lock timeouts, and silent regressions—that erode user trust and block stable operation for self-hosted users. Its technical approach is the most monolithic, serving as the integration reference for all others, which makes its stability problems ecosystem-wide problems.

### 4. Shared Technical Focus Areas

Several recurring requirements are emerging independently across multiple projects, indicating foundational gaps in the current architecture:

- **Session State & Storage Migration (OpenClaw, Hermes, ZeroClaw, LobsterAI):** Projects are actively debating or implementing migration from flat file storage to SQLite (or PostgreSQL). The core driver is reliability—preventing JSONL write-lock contention, data corruption on crash, and silent state loss.
- **Channel Reliability & Multi-Platform Delivery (OpenClaw, Hermes, NanoBot, IronClaw, ZeroClaw):** Persistent failures in Telegram, Discord, and WhatsApp are a cross-cutting concern. Issues around duplicate messages, infinite loops (e.g., Telegram's 4096-char overflow), and silent delivery failures suggest the delivery pipeline needs a fundamental redesign.
- **Plugin/Tool Security (ZeroClaw, IronClaw, PicoClaw):** A strong push toward signed plugins, capability enforcement (Wasm sandboxing), and per-tool permission models is underway. This is driven by user security incidents and the need to support enterprise deployments.
- **Context Budget / Memory Management (OpenClaw, IronClaw, CoPaw):** Users consistently hit hard limits on context windows, leading to perpetual trim cycles or complete freezes. This is a manifestation of the broader challenge of managing long-running, stateful agent sessions.

### 5. Differentiation Analysis

The ecosystem is segmenting along lines of architectural philosophy and target user:

- **Reference Stack (OpenClaw):** Maximum features, complex configuration, serves as the integration testbed for all others. Suited for developers and researchers who need the latest capabilities, even at the cost of stability.
- **Developer Toolkit (ZeroClaw, NanoBot):** Focus on modularity, easy installation (`pip install`), and deep plugin support. Targets independent developers and sysadmins who want a reliable, extensible agent they can customize.
- **Enterprise & Workflow (IronClaw, NanoClaw):** Emphasis on approvals, delegation, automation lifecycles (pause/resume/delete), and scalable deployment (Postgres profiles). Suited for teams needing multi-agent collaboration and audit trails.
- **Hardware / Edge (PicoClaw):** Focus on lightweight deployments, ADB tooling, and decentralized protocols (SimpleX/Tox). Targets IoT and privacy-conscious users.
- **Consumer / Phone UI (CoPaw, Hermes):** Emphasis on mobile-responsive UI, intuitive onboarding, and personal knowledge bases. Favors a polished user experience over deep configurability.

### 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration (High churn, high engagement)**
- **OpenClaw:** Dominates activity volume. Surging, but risk of burnout and stability crisis.
- **ZeroClaw:** Very high velocity with a strong focus on future-facing architecture (Wasm, supply chain security). Healthy despite high volume.
- **IronClaw:** Intense, planned development of the "Reborn" architecture with a disciplined, engineering-driven cadence.
- **CoPaw:** High activity but with a noticeable tail of regressions, indicating a "stabilization through fire" phase.
- **Hermes Agent:** High volume of incoming bug reports with low closure rate. A project struggling to maintain quality as feature velocity outpaces testing.

**Tier 2: Steady Ship (Stable, predictable releases)**
- **NanoBot:** Healthy, high-quality releases (v0.2.2). Low bug count. A model for sustainable development.
- **PicoClaw:** Moderate activity with a clear focus on hardening (type assertions, auth). Steady progress.
- **NanoClaw:** Steady, if lower-volume, contribution pipeline. Solid health.

**Tier 3: Dormant / Stalled**
- **LobsterAI:** Critical risk. An 80-day silence on major bugs and open PRs indicates active abandonment.
- **NullClaw, TinyClaw, Moltis, ZeptoClaw:** Effectively dormant. Indicate project fatigue or completion of a primary development phase.

### 7. Trend Signals

Several market signals emerge from a synthesis of community feedback across all projects:

1.  **"Plug-and-Play" is Not a Reality:** The single biggest source of user frustration is the **configuration and onboarding friction**. The "smooth start" experience is production–quality in almost no project, representing a major opportunity for differentiation.
2.  **OpenRouter Dependency is a Bottleneck:** Users across Hermes and other projects are explicitly demanding direct provider integrations to avoid the reliability and cost issues of routing proxies. This aligns with the broader industry trend of models becoming a commodity.
3.  **The "Long-Running Agent" Problem is Unsolved:** Session state loss, context budget exhaustion, process freezes, and silent re-syncs are the dominant source of P0/P1 bugs. The ecosystem is proving that naive SQLite/JSONL storage is insufficient.
4.  **Security is Shifting from "Add-On" to "Core":** The emphasis on signed plugins, Wasm sandboxing, and approval policies signals a maturation of the user base from hobbyists to professionals who must secure agent deployments.
5.  **Convergence on Mobile:** While the desktop/TUI is the dominant interface, a wave of mobile-first contributions (CoPaw, Hermes) and PWA support requests (NanoBot) suggests the agent interface is moving to the phone, driven by the need for always-on, push-based interaction.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **2026-06-23**.

---

## NanoBot Project Digest — 2026-06-23

### 1. Today's Overview
The project is in a **high-velocity release cycle**, closing a significant **v0.2.2** release. Activity is extremely high: **27 pull requests** were updated in the last 24 hours, with **13 merged or closed** (a 48% closure rate). Core stability and gateway durability remain the dominant themes, with a clear focus on fixing shutdown races, WebUI session corruption, and MCP transport edge cases. The **4 open issues** reflect a healthy shift toward feature requests (PWA, Telegram rich messages) rather than critical bug reports, suggesting the recent release has addressed several major pain points.

### 2. Releases
**`v0.2.2`** (released today) — A major stability and durability release.
- **Key changes:** WebUI conversation transcripts are now segmented (no single fragile file); forked chat replies are preserved reliably during history refreshes; gateway shutdown is now robust against signal handling edge cases.
- **Breaking changes:** None explicitly reported, though the segmented transcript format is a new artifact structure.
- **Migration notes:** Users are advised to upgrade via `pip install --upgrade nanobot`. No manual migration steps are required, but if users rely on the raw single-file transcript format, they should backup before upgrading.

### 3. Project Progress
**13 PRs merged/closed today** (all closed items are stability fixes):
- **Gateway stability (high priority):** `#4456` (tolerate cancelled channel tasks during shutdown), `#4454` (stabilize foreground gateway shutdown & WebUI fork reply replay), `#4450` (close MCP stdio transports from agent task to avoid task-scope crashes).
- **WebUI fixes:** `#4455` (preserve fork replies during history refresh), `#4453` (follow active turn output after send), `#4451` (stabilize sent turn layout and dev reloads).
- **Release & docs:** `#4461` (add v0.2.2 release news to README), `#4445` (chore: prepare v0.2.2).
- **Code quality:** `#4452` (enforce MCP enabledTools for resources/prompts — merged).

### 4. Community Hot Topics
The most active discussions revolve around **gateway lifecycle management** and **multi-platform integrations**:

1. **#1461 (CLOSED) — Unified daemon gateway semantic layer**  
   [Link](https://github.com/HKUDS/nanobot/issues/1461)  
   *4 comments, 0 reactions.* This long-running proposal (from March) has been closed, likely implemented in v0.2.2's gateway refactor. The "daemon" architecture (two-layer mode with background process) appears to be the foundation of the current gateway changes.

2. **#4413 (OPEN) — Telegram Bot API 10.1 rich messages**  
   [Link](https://github.com/HKUDS/nanobot/issues/4413)  
   *2 comments.* A user request to support Telegram's new rich message format. No PR yet, but the feature request is specific and well-defined — likely to be picked up soon given the project's focus on channel support.

3. **#4376 (CLOSED) — User-friendly wizard**  
   [Link](https://github.com/HKUDS/nanobot/issues/4376)  
   *1 comment, 1 reaction.* Closed as "won't do" or "already implemented"? The single comment (from author chengyongru) suggests the wizard was improved as part of v0.2.2.

### 5. Bugs & Stability
**Severity: High**
- **MCP shutdown crashes (`RuntimeError` in cancel-scope)** — Reported in multiple PRs (#4441, #4450). The root cause is an AnyIO task-group mismatch when closing MCP stdio transports. **Fix exists:** `#4450` (merged) and `#4441` (open, awaiting review).  
- **WebUI fork reply disappearance** — Rare but severe: an already-rendered assistant reply can vanish after a history refresh. **Fix exists:** `#4455` (merged).  
- **Duplicate tool_use IDs bricking sessions** — Streaming providers can emit duplicate `tool_use` blocks, permanently breaking the session. **Fix exists:** `#4443` (open, under review).

**Severity: Medium**
- **Pairing store sender ID type-coercion inconsistency** — Silent denial of service for non-string sender IDs. **Fix exists:** `#4433` (open).  
- **MCP enabledTools bypass** — Resources/prompts were registered even if `enabledTools` denied them. **Fix exists:** `#4436` and `#4452` (both merged).

### 6. Feature Requests & Roadmap Signals
Three strong signals for **v0.2.3 or v0.3.0**:

1. **Progressive Web App (PWA) support** — **#4457 (OPEN)**, with a parallel PR **#4458 (OPEN)**. This is a clean, well-scoped enhancement for mobile users. Likely to land in the next minor release.
2. **Mattermost channel integration** — **#4459 (OPEN)**. A complete new channel backend with WebSocket + REST API. Ready for review and merging.
3. **Telegram rich messages** — **#4413 (OPEN)**. No PR yet, but the community has clear demand for improved Telegram formatting.
4. **DingTalk improvements** — **#4446 (OPEN)**. Private chat gating and group reply mention. A targeted enhancement for specific platform users.

### 7. User Feedback Summary
- **Pain point (addressed):** The "gateway daemon" feature (#1461) was a long-standing request for OS-managed background execution. v0.2.2's gateway refactor closes this.
- **Pain point (addressed):** WebUI conversation fragility (fork reply loss, transcript corruption) was a top user frustration. Multiple merged PRs fix this.
- **Satisfaction signal:** The `v0.2.2` release notes highlight "sturdier agent" and "survive more of real life" — positive language from maintainers suggesting user feedback was heard.
- **Pain point (ongoing):** The wizard (#4376) still assumes technical knowledge. While closed, the user feedback "not user-friendly for new or non-technical users" remains valid. A low-code/UI-based onboarding has not been proposed.

### 8. Backlog Watch
- **#1461 — Unified daemon gateway** (CLOSED today after 3+ months). This was the most significant "sleeping giant" issue. Its closure signals architectural completion.
- **#4441 — MCP reconnect crash** (OPEN). Still awaiting review despite being a high-severity fix for gateway stability. Should be prioritized alongside the merged `#4450`.
- **#4447 — Gateway lifecycle edge cases** (OPEN). Addresses remaining edge cases for daemon state management. Linked to the v0.2.2 release, so likely to be merged quickly.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-23

## Today's Overview

The Hermes Agent project is experiencing **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. The open-to-closed ratio remains elevated at approximately 4:1 for issues (41 open vs. 9 closed) and roughly 3:1 for PRs (37 open vs. 13 merged/closed), indicating a **sustained development surge** that is outpacing the project's ability to resolve incoming work. No new releases were cut today, which is notable given the volume of fixes in flight. The community is highly engaged, contributing both bug reports and feature requests across nearly all subsystems—gateways (Telegram, Discord), desktop clients, provider integrations, and the agent core itself.

## Releases

No new releases were published today. The latest release remains v0.17.0 (implied by recent changelogs). This is a significant observation: despite dozens of PRs being merged and critical bugs being reported, no patch release has been cut. Organizations relying on stable deployments should monitor for an imminent v0.17.1 or v0.18.0.

## Project Progress

Today's merged/closed PRs (13 items) show important progress:

- **Discord reliability**: PR [#48685](https://github.com/NousResearch/hermes-agent/pull/48685) (merged) fixes auto-thread creation race conditions where `message.create_thread()` loses a race to another bot/client.
- **Live voice sessions**: PR [#45614](https://github.com/NousResearch/hermes-agent/pull/45614) (merged) adds a platform-neutral `gateway.voice_sessions` backend for live voice lifecycle/state management, wiring Discord `/voice live` integration.
- **CLI and cron fixes**: PR [#45608](https://github.com/NousResearch/hermes-agent/pull/45608) (merged) preserves non-zero exit codes from argparse subcommand handlers.
- **Gateway restart resilience**: PR [#39817](https://github.com/NousResearch/hermes-agent/pull/39817) (merged) persists in-flight gateway user requests before agent execution to prevent replay on restart.
- **Cross-platform contributors**: PR [#51138](https://github.com/NousResearch/hermes-agent/pull/51138) (merged, titled "Lazy exports/qq yuanbao") suggests continued expansion of internationalized provider support, though details are sparse.
- **Windows fixes**: PR [#51113](https://github.com/NousResearch/hermes-agent/pull/51113) resolves Windows path corruption and test collection crashes (ACP adapter).

Notably, many of these merged PRs were opened days ago and are only now being closed, suggesting maintainers are processing a large backlog.

## Community Hot Topics

The most actively discussed issues today reveal deep user concerns:

1. **[Issue #12639](https://github.com/NousResearch/hermes-agent/issues/12639) — Native Google/Vertex AI Provider** (11 comments, 10 👍)
   Users are frustrated with OpenRouter's 402 errors and rate limits when routing `google/gemini-3.1-pro-preview`. This is the **oldest high-engagement issue** still open (since April 19). The community is signaling a clear need for direct provider integration as a reliability and cost-control measure. The author notes that Hermes "tries to... [charge a markup]" via OpenRouter.

2. **[Issue #37505](https://github.com/NousResearch/hermes-agent/issues/37505) — Intel Mac DMG failure** (7 comments, 1 👍)
   The official macOS DMG ships as `arm64`-only, causing launch failures on Intel MacBooks. This is a **basic distribution issue** affecting desktop adoption on older hardware.

3. **[Issue #48648](https://github.com/NousResearch/hermes-agent/issues/48648) — Telegram message duplication loop** (4 comments, 1 👍)
   A critical Telegram bug where messages exceeding 4096 characters trigger an infinite nested reply loop. The community has identified the root cause in the gateway stream handler.

4. **[Issue #46515](https://github.com/NousResearch/hermes-agent/issues/46515) — Telegram rich message fallback** (1 comment, 3 👍)
   Despite high 👍 counts, this issue has minimal maintainer engagement. Rich message drafts render correctly during streaming, but the final persisted message falls back to plain MarkdownV2.

5. **[Issue #51057](https://github.com/NousResearch/hermes-agent/issues/51057) — Discord double-dispatch** (1 comment, 0 👍)
   A single Discord message launched two independent agent runs, producing duplicate responses. Reported on v0.17.0.

## Bugs & Stability

Today's bug reports span **critical to low severity**, with several having active fix PRs:

**Critical (P1):**
- **[Issue #51057](https://github.com/NousResearch/hermes-agent/issues/51057) — Discord message double-dispatch** (P1): A single message triggers two agent runs. Root cause suspected in the Discord adapter's event handler. **No fix PR yet.**
- **[Issue #30636](https://github.com/NousResearch/hermes-agent/issues/30636) — `state.db` corruption on SIGTERM during high load** (P1): Three corruption events in 48h on macOS under launchd. Root cause: asynchronous write buffering in SQLite. **No fix PR yet.** This is 32 days old with no resolution.

**High (P2):**
- **[Issue #50765](https://github.com/NousResearch/hermes-agent/issues/50765) — ACP session/prompt hangs on Windows after conversation turn** (P2): Regression in v0.17.0; v0.16.0 worked. Community has identified the log line where progress stops. **PR [#51113](https://github.com/NousResearch/hermes-agent/pull/51113) is open** with Windows path fixes that may address this.
- **[Issue #48648](https://github.com/NousResearch/hermes-agent/issues/48648) — Telegram infinite message loop on 4096-char overflow** (P2): Root cause identified in gateway code. **No fix PR yet.**
- **[Issue #51089](https://github.com/NousResearch/hermes-agent/issues/51089) — Session resume loses tool-loop/compression state** (P2): Process interrupts can drop in-memory tool-call results. **No fix PR yet.**
- **[Issue #50199](https://github.com/NousResearch/hermes-agent/issues/50199) — Delegation `base_url` ignored at runtime** (P2): `_load_config()` returns empty CLI_CONFIG block over correct config.yaml. Blocks cross-host delegation entirely. **No fix PR yet.**
- **[Issue #51141](https://github.com/NousResearch/hermes-agent/issues/51141) — `write_file` secret redaction mangles Python variable assignments** (P2): Overly aggressive redaction makes it impossible to write API-client scripts. **No fix PR yet.**

**Medium (P3):**
- **[Issue #50755](https://github.com/NousResearch/hermes-agent/issues/50755) — Photon iMessage AuthenticationError after secret rotation** (P3): Outbound sends fail after `hermes photon setup` second run.
- **[Issue #51045](https://github.com/NousResearch/hermes-agent/issues/51045) — Nous Portal Azure backend errors for `openai/gpt-5.5`** (P3): Service-side regression, retries don't help.
- **[Issue #51139](https://github.com/NousResearch/hermes-agent/issues/51139) — `computer_use` missing wrappers for page/hotkey/move_cursor** (P3): cua_backend lacks most action wrappers, contrary to earlier claims. **PR [#51137](https://github.com/NousResearch/hermes-agent/pull/51137) is open** to add `launch_app`/`list_apps`.

**Closed today:**
- **[Issue #50090](https://github.com/NousResearch/hermes-agent/issues/50090)** — Windows: bootstrap-installer kills Gateway without respawning (P1, closed). Telegram bot permanently dead until manual intervention after skill updates. Likely fixed via related infrastructure PRs.

## Feature Requests & Roadmap Signals

Several feature requests this week point toward **platform expansion and UX improvements**:

1. **[Issue #51069](https://github.com/NousResearch/hermes-agent/issues/51069) — Support project-local `.mcp.json` MCP server configs** (P3): Users want Hermes to read MCP servers from standard project files, not just its own config. This aligns with developer workflow conventions.

2. **[Issue #51046](https://github.com/NousResearch/hermes-agent/issues/51046) — i18n support for Telegram BotCommand menu descriptions** (P3): Despite having a locale system, Telegram bot commands remain in English. Low-hanging fruit for international users.

3. **[Issue #50885](https://github.com/NousResearch/hermes-agent/issues/50885) — Create/delete workspace folders from Desktop app remotely** (P3): Users are asking the Discord for basic filesystem management via the GUI.

4. **[Issue #41044](https://github.com/NousResearch/hermes-agent/issues/41044) — Windows `computer_use` support** (closed today with comment): Multiple solutions proposed (pyautogui, Windows-specific backends). Community wants parity with existing macOS implementation.

**Likely to be in next release (v0.17.1 or v0.18.0):**
- Spanish locale for Desktop app (PR [#49036](https://github.com/NousResearch/hermes-agent/pull/49036) open)
- GLM-5.2 reasoning effort controls (PR [#51108](https://github.com/NousResearch/hermes-agent/pull/51108) open)
- Kanban in-app dialog migration (PR [#51118](https://github.com/NousResearch/hermes-agent/pull/51118) open)
- Discord typing indicator fixes (PR [#51140](https://github.com/NousResearch/hermes-agent/pull/51140) open)
- Multiple Windows and encoding fixes (PRs [#51113](https://github.com/NousResearch/hermes-agent/pull/51113), [#51119](https://github.com/NousResearch/hermes-agent/pull/51119))

## User Feedback Summary

**Satisfaction indicators:**
- High engagement with the project's open-source model—users are filing detailed bug reports with root cause analysis (e.g., issue #48648 identifies exact code paths).
- Community members are contributing fixes across platforms (Windows, macOS Intel, Discord, Telegram).
- Feature requests are thoughtful and well-researched (e.g., `.mcp.json` support references existing tool conventions).

**Pain points:**
- **OpenRouter dependency is a reliability bottleneck** (Issue #12639): Users are hitting 402/rate-limit errors consistently and want direct provider support.
- **macOS Intel support regression** (Issue #37505): The DMG shipping arm64-only is a regression, not a design choice—users expect universal binaries.
- **Telegram rich messaging is unreliable** (Issues #48648, #46515): Rich message streaming breaks on common 4096-char overflow; final messages degrade to plain text. This is a core Telegram UX problem.
- **Delegation/cross-host workflows are broken** (Issue #50199): Users cannot run worker models on separate machines due to config loading bugs. This limits scalability.
- **Session state loss on restart** (Issue #30636, #51089): SQLite corruption and tool-loop state loss create data-loss risk for long-running agent sessions.
- **Windows is still rough** (Issue #50765, #50090): ACP hangs on 0.17.0; installer kills gateways without respawning. Windows users continue to experience second-class support.

**Satisfaction rating (inferred):** Moderate. The community is engaged and contributing, but the high volume of open bugs (especially P1/P2 regressions in 0.17.0) and lack of a patch release suggest frustration may be building.

## Backlog Watch

Several important issues and PRs require maintainer attention:

1. **[Issue #12639](https://github.com/NousResearch/hermes-agent/issues/12639) — Native Google/Vertex AI Provider** (open since April 19, 11 comments, 10 👍)
   The most-upvoted issue still open. 65+ days without a meaningful response. This is the community's top unmet need.

2. **[Issue #30636](https://github.com/NousResearch/hermes-agent/issues/30636) — `state.db` corruption on SIGTERM** (open since May 22, 32 days, P1)
   No maintainer response despite three confirmed occurrences. Data-loss severity.

3. **[Issue #37505](https://github.com/NousResearch/hermes-agent/issues/37505) — Intel Mac DMG failure** (open since June 2, 21 days)
   A distribution issue that should be straightforward to fix (shipping universal binary). No action taken.

4. **[Issue #44183](https://github.com/NousResearch/hermes-agent/issues/44183) — Desktop session lost after sleep/wake** (open since June 11, 12 days, P3)
   WebSocket orphan reap grace period (20s) is too short for Mac sleep cycles. Minor fix, no engagement.

5. **[Issue #42448](https://github.com/NousResearch/hermes-agent/issues/42448) — OIDC WebAuthn/Touch ID failure** (open since June 8, 15 days, P3)
   Passwordless authentication fails in Hermes Desktop embedded browser. Blocks enterprise SSO adoption.

6. **PR [#50540](https://github.com/NousResearch/hermes-agent/pull/50540) — Unicode corruption fix in patch/write_file tools** (open since June 22, P1)
   Fixes a bug where patches silently corrupt Unicode characters and line numbers. **Critical for code editing workflows.** No activity since submission.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-23

## 1. Today's Overview
PicoClaw shows **moderate-to-high activity** today, with 17 pull requests updated in the last 24 hours and 3 new issues. The project is in a **healthy development phase**, with significant focus on security hardening (cross-site request protection), new platform tooling (Android ADB), and LLM integration stability (Doubao Seed tool call leak fix). Six PRs were merged or closed, indicating steady progress. No new releases were published today, but the codebase is clearly evolving toward v0.3.0.

## 2. Releases
**None** — No new releases were published in the last 24 hours. The latest available version based on issue reports is **v0.2.9** (referenced in Issue #3159). Users running v0.2.8 should be aware of the Doubao Seed tool call leak bug documented in Issue #3153.

## 3. Project Progress
Six PRs were merged or closed in the last 24 hours:

- **#3155** [Merged] *feat(spawn): add direct_reply parameter with SkipInboundTurn support* — by @v2up-32mb. Fixes duplicate message problem (Issue #3094) by providing two clear behavior paths via `ToolResult.SkipInboundTurn`.
- **#3053** [Closed] *fix(evolution): add ok check for LoadOrStore type assertion in lockStoreFile* — by @chengzhichao-xydt. Prevents panic from unchecked type assertion in `sync.Map.LoadOrStore`.
- **#3091** [Closed] *fix(openai_compat): add ok check for native_search type assertion* — by @chengzhichao-xydt. Prevents silent disable of native search when a non-bool value is passed.
- **#3101** [Closed] *build(deps-dev): bump vite from 8.0.13 to 8.0.16* — Dependabot dependency update.
- **#3105** [Closed] *build(deps-dev): bump eslint from 10.2.1 to 10.4.1* — Dependabot dependency update.
- **#3152** [Closed] *add installation instructions to picoclaw skills search* — by @phoeagon. Improves UX by showing how to install found skills.

**Key feature advances that remain open:**
- **#3160** — Cross-site launcher setup request protection (critical security)
- **#3157** — Experimental Android ADB remote operations tool
- **#3156** — Per-turn LLM token usage emission for Pico channel
- **#3154** — Doubao Seed tool call leak recovery

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#3093 – SimpleX/tox gateway feature request](https://github.com/sipeed/picoclaw/issues/3093) | 3 | 1 👍 | Adding decentralized messaging gateways |

**Analysis:** The request for SimpleX or Tox gateway integration (Issue #3093) signals growing interest in **privacy-preserving, decentralized communication** channels for PicoClaw. The single upvote suggests early-stage demand, but the explicit naming of specific protocols indicates users want alternatives to centralized platforms like Slack/Telegram. This aligns with broader PicoClaw trends toward multiple channel backends.

**#3154** (Doubao Seed fix) and **#3153** (the bug report it references) are also attracting attention as they impact users of Chinese LLM providers — a significant user segment.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **High** | [#3153 – Doubao Seed tool call leak](https://github.com/sipeed/picoclaw/issues/3153) | Raw `<seed:tool_call>` XML exposed to user instead of being executed | Fix PR [#3154](https://github.com/sipeed/picoclaw/pull/3154) open, not yet merged |
| **Medium** | [#3159 – Duplicate task execution](https://github.com/sipeed/picoclaw/issues/3159) | When asking sequential questions (e.g., US news then France news), the second answer re-executes the first task | No known fix PR yet |
| **Low-Medium** | [#3053](https://github.com/sipeed/picoclaw/pull/3053) / [#3091](https://github.com/sipeed/picoclaw/pull/3091) | Unchecked type assertions causing potential panics | Both merged today |

**Additional stability improvements in progress:**
- **#3131** — Type assertion safety in tool registry (open)
- **#3128** — Proper error handling in search provider response body closing (open)

## 6. Feature Requests & Roadmap Signals

| Feature | Issue | Likely Version |
|---------|-------|----------------|
| **SimpleX / Tox gateway** | [#3093](https://github.com/sipeed/picoclaw/issues/3093) | v0.3.0+ (low priority, needs more demand) |
| **Android ADB remote operations** | PR [#3157](https://github.com/sipeed/picoclaw/pull/3157) | v0.2.10 (experimental, disabled by default) |
| **Per-turn LLM token usage** | PR [#3156](https://github.com/sipeed/picoclaw/pull/3156) | v0.2.10 (already implemented, awaiting merge) |
| **Remote agent mode (WebSocket)** | PR [#3118](https://github.com/sipeed/picoclaw/pull/3118) | v0.2.10 (open, stale) |

**Prediction:** The next release (likely **v0.2.10** or **v0.3.0**) will include:
- The Doubao Seed tool call fix (#3154)
- Cross-site auth protection (#3160)
- Token usage emission (#3156)
- Possibly the Android ADB tool (#3157) in experimental state

The remote WebSocket agent mode (#3118) has been stale for 11 days, suggesting it may be pushed to a later release unless maintainers prioritize it.

## 7. User Feedback Summary

**Pain Points:**
1. **Doubao Seed model users** report broken tool calling (#3153) — raw XML leaked, breaking workflows. Workaround: avoid tool-heavy prompts with this model.
2. **Sequential task duplication** (#3159) — users asking multiple questions in one session get redundant task execution. No workaround documented.
3. **Spawning agent duplicate messages** (Issue #3094, now fixed by #3155) — async callbacks caused double delivery. Fix merged today.

**Positive Signals:**
- The community is actively contributing security and stability fixes (3 type-assertion safety PRs merged this week).
- User @phoeagon contributed a UX improvement (#3152) — skill search now shows installation instructions, addressing a common frustration.

**Satisfaction Trends:**
- Users running v0.2.9 on Debian 13 (Issue #3159) suggest a technically adept user base comfortable with Linux and open-source models.
- The diversity of feature requests (ADB, WebSocket remote mode, gateway protocols) shows PicoClaw is being adopted in **devops, automation, and edge device** use cases.

## 8. Backlog Watch

| Item | Type | Days Stale | Attention Needed |
|------|------|------------|------------------|
| [#3118 – Remote WebSocket agent mode](https://github.com/sipeed/picoclaw/pull/3118) | Feature PR | 11 days | Waiting for maintainer review; significant new capability |
| [#3131 – Tool schema type assertions](https://github.com/sipeed/picoclaw/pull/3131) | Fix PR | 8 days | Part of broader type-safety campaign; should merge soon |
| [#3128 – Response body Close() handling](https://github.com/sipeed/picoclaw/pull/3128) | Fix PR | 8 days | Low-risk; ready to merge |
| [#3104 – shadcn dependency bump](https://github.com/sipeed/picoclaw/pull/3104) | Dependabot | 12 days | Routine; should merge to keep frontend tooling current |
| #3100, #3103 | Dependabot (Vite, ESLint) | 12 days | Routine; some already closed |

**Maintainer attention required:** The **remote WebSocket agent mode** (#3118) is the most significant stalled feature. If maintainers are interested in supporting remote agent control (which aligns with the IoT/edge use case), this PR needs active review. The three type-safety fix PRs (#3131, #3128, and already-merged #3053/#3091) indicate a systematic effort to harden the codebase — these should be prioritized to completion.

---

*Digest generated 2026-06-23 23:00 UTC. Data source: github.com/sipeed/picoclaw.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-23

## Today's Overview
Project activity remains steady with 6 pull requests updated in the last 24 hours, though no new issues were opened today. The community is actively contributing features and fixes, with notable additions in email integration (IMAP/SMTP), Telegram channel support, and approval workflow enhancements. A critical fix for cleaning up stale peer service registrations was also advanced. The single merged PR today—Telegram integration—signals continued momentum in expanding communication channels. Overall project health appears solid, with sustained contributor engagement across both features and maintenance.

## Releases
No new releases were published today.

## Project Progress
One pull request was merged today:
- **[#2831] feat: add Telegram integration (verified working on v2.1.1)** — Closed/merged (Author: aarchh). Adds Telegram as a channel for NanoClaw agents, confirmed compatible with the current v2.1.1 release. This represents the sole completion in the last 24 hours.

Additionally, the following open PRs saw updates but remain unmerged:
- **#1235**: IMAP/SMTP email integration (discussed further below)
- **#2795**: New `/add-clidash` CLI-derived dashboard skill
- **#2832**: Reject with reason for approvals
- **#2830**: Fix for stale peer service registration cleanup
- **#2531**: Fix for duplicate text suppression in poll-loop

## Community Hot Topics
The most active items based on update frequency and discussion volume:

1. **[#1235] feat: add IMAP/SMTP email integration** (Author: aronjanosch)
   - *URL: [nanocoai/nanoclaw PR #1235](https://github.com/nanocoai/nanoclaw/pull/1235)*
   - **Status**: Open since March 18, last updated yesterday
   - **Analysis**: This large feature adds IMAP email as both a channel (inbox polling → agent messages) and a toolset (agent reads/composes/manages email on demand) with 6 MCP tools exposed. The long gestation (3+ months) suggests complex integration work. The underlying need is clear: enterprises and power users need email as a primary interaction channel for AI agents—a high-value capability currently missing.

2. **[#2832] feat(approvals): reject with reason** (Author: moshe-nanoco)
   - *URL: [nanocoai/nanoclaw PR #2832](https://github.com/nanocoai/nanoclaw/pull/2832)*
   - **Status**: Opened yesterday, still fresh
   - **Analysis**: Addresses a common human-in-the-loop pain point—when an approver declines an agent action, the agent receives only "declined" with no context. Adding optional rejection reasons lets agents adapt their next attempt intelligently. This signals growing sophistication in approval workflows.

3. **[#2830] fix(setup): reap dead peer service registrations** (Author: amit-shafnir)
   - *URL: [nanocoai/nanoclaw PR #2830](https://github.com/nanocoai/nanoclaw/pull/2830)*
   - **Status**: Opened June 21, last updated yesterday
   - **Analysis**: Documents a real operational pain—deleting a NanoClaw checkout without running the uninstaller leaves orphaned launchd/systemd entries, accumulating stale registrations (6 on one machine). This fix automatically detects and cleans dead binary references.

## Bugs & Stability
No new bugs were reported via issues today. However, the following fix PRs address real-world stability concerns:

| PR | Issue Description | Severity | Status |
|---|---|---|---|
| [#2830](https://github.com/nanocoai/nanoclaw/pull/2830) | Stale peer service registrations accumulate when checkouts are deleted without uninstall | Medium | Open, fix proposed |
| [#2531](https://github.com/nanocoai/nanoclaw/pull/2531) | Duplicate text appears when `send_message` fires mid-turn in poll-loop | Medium | Open, fix proposed (since May 18) |

**Severity Ranking**: Both are medium severity—the first causes accumulating OS-level cruft on developer machines, the second degrades conversation quality. Neither appears to cause crashes or data loss.

## Feature Requests & Roadmap Signals
Features currently in development or proposed via active PRs:

| Feature | PR | Stage | Likely for Next Release |
|---|---|---|---|
| IMAP/SMTP email integration | [#1235](https://github.com/nanocoai/nanoclaw/pull/1235) | Open, 3+ months old | Possible if finalized soon |
| Telegram channel | [#2831](https://github.com/nanocoai/nanoclaw/pull/2831) | Merged today | Already in main |
| `/add-clidash` CLI dashboard skill | [#2795](https://github.com/nanocoai/nanoclaw/pull/2795) | Open (1 week old) | Likely |
| Reject with reason in approvals | [#2832](https://github.com/nanocoai/nanoclaw/pull/2832) | Fresh (1 day old) | Possible |

**Prediction**: The merged Telegram integration (#2831) and the evolving approvals workflow (#2832) are strong candidates for the next minor release. The IMAP/SMTP integration (#1235) may require additional review cycles given its scope.

## User Feedback Summary
While no direct user comments were available in this data snapshot, the following pain points can be inferred from the PRs:

- **Pain Point**: Agents receiving "declined" without explanation when approval is denied → **Addressed by PR #2832** (reject with reason)
- **Pain Point**: Stale launchd/systemd registrations from incomplete uninstall → **Addressed by PR #2830** (auto-cleanup of dead binary references)
- **Pain Point**: Duplicate message text in conversations → **Addressed by PR #2531** (poll-loop suppression)
- **Pain Point**: Need for email-based agent interaction → **Being addressed by PR #1235**
- **Pain Point**: Need for Telegram as an interaction channel → **Resolved by merged PR #2831**

## Backlog Watch
The following items warrant maintainer attention due to age or inactivity:

1. **[#1235] IMAP/SMTP email integration** — Open since March 18, 2026 (3+ months). This is a substantial feature but has received no comments or reactions. May need maintainer review to unblock or provide guidance on next steps.
   - *URL: [nanocoai/nanoclaw PR #1235](https://github.com/nanocoai/nanoclaw/pull/1235)*

2. **[#2531] fix(poll-loop): suppress duplicate text** — Open since May 18, 2026 (5+ weeks). A straightforward conversational quality fix that has not yet been merged. May be waiting on review bandwidth.
   - *URL: [nanocoai/nanoclaw PR #2531](https://github.com/nanocoai/nanoclaw/pull/2531)*

Both items show no maintainer activity or comments, suggesting they may be in a review queue or awaiting additional testing.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-06-23**.

---

### NullClaw Project Digest – 2026-06-23

**Project:** NullClaw (github.com/nullclaw/nullclaw)
**Analyst:** AI Agent & Personal Assistant OSS Analyst

---

### 1. Today's Overview

The NullClaw project is in a low-activity maintenance phase today, with no new issues, releases, or merged pull requests in the last 24 hours. Two pull requests remain open, one of which is a critical bug fix for the Matrix bridge’s sync persistence that is awaiting review. The project shows healthy dependency hygiene via an automated Docker base image update (Alpine 3.23 → 3.24). The absence of community issues suggests a stable user base, though the lack of maintainer activity on the open bug fix may be a concern.

### 2. Releases

**None.**  
No new releases have been published. The latest available release remains the previous version.

### 3. Project Progress

**No pull requests were merged or closed in the last 24 hours.**  
Two PRs remain open:
- **PR #968** (awaiting review): Critical bug fix for Matrix sync persistence (see Bugs & Stability).
- **PR #956** (waiting on CI): Automated dependency bump for the Docker image base (`alpine` from 3.23 to 3.24).

### 4. Community Hot Topics

There are no community discussions or issues active today. The two open PRs represent the only current focus areas:

- **PR #968 – `fix(matrix): persist next_batch across restart + test env isolation`** ([link](https://github.com/nullclaw/nullclaw/pull/968))  
  *Author: addadi* | *Updated: 2026-06-22* | *👍: 0*  
  This is the most significant technical contribution in the window. The underlying need is clear: preventing repeated Matrix initial syncs on every NullClaw restart, which is a data-loss and performance regression for production users.

- **PR #956 – `ci(deps): bump alpine from 3.23 to 3.24`** ([link](https://github.com/nullclaw/nullclaw/pull/956))  
  *Author: dependabot[bot]* | *Updated: 2026-06-22* | *👍: 0*  
  Routine dependency hygiene. No controversy.

### 5. Bugs & Stability

**One bug fix is proposed but not yet merged.**

- **Severity: High** – **Matrix sync state lost on restart** (PR #968).  
  **Problem:** The Matrix bridge stores the `/sync` cursor only in RAM. Every restart causes a full initial sync (wasting bandwidth and time) and forces the client to re-process all messages.  
  **Fix exists:** PR #968 introduces persistence of the `next_batch` token across restarts and adds test environment isolation to prevent regressions.  
  **Status:** Open, no maintainer review yet.  
  **Impact:** Users with long-running Matrix integrations experience disruptive "cold starts" and may miss messages during re-sync.

No new bugs, crashes, or regressions were reported in the last 24 hours.

### 6. Feature Requests & Roadmap Signals

**No new feature requests or roadmap signals were observed in the last 24 hours.**  
The project appears focused on stabilization rather than new functionality. The next version will likely include:
- The Matrix sync persistence fix (PR #968)
- Updated Docker base image (Alpine 3.24, PR #956)
- No breaking changes are anticipated.

### 7. User Feedback Summary

**No user feedback, complaints, or testimonials were posted in the last 24 hours.**  
Given the low number of open items, the user base appears either satisfied or inactive. The lack of community issues may also indicate that users have not yet encountered significant problems (or that feedback channels are underutilized).

### 8. Backlog Watch

**No long-unanswered issues or PRs currently require maintainer attention beyond PR #968.**  
- **PR #968** (opened 2026-06-22) is the most time-sensitive item—it addresses a production bug and has received no maintainer review after 1 day. Continued inactivity could frustrate the contributor and leave users exposed to the restart bug.  
- **PR #956** (opened 2026-06-15) is a routine dependency bump that has been open for 8 days; it is non-critical but should be merged or closed to keep the CI pipeline clean.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-23

## Today's Overview

IronClaw remains in a period of intense development activity on the **Reborn** architecture, with 18 issues and 23 PRs updated in the last 24 hours. The project is shipping steadily (8 PRs merged/closed) while actively investigating a **critical regression** in web/research task execution that has zeroed LLM call volume on a significant portion of the PinchBench benchmark. A new weekly performance-focused tracker (#5125) has been opened, signaling that user-facing latency is a top concern. Overall project health is robust—core contributors are landing features for automation lifecycle management, concurrent turn execution, and a major god-crate decomposition—but the regression and a body of dogfooding findings indicate the Reborn stack still needs hardening before broader rollout.

**Activity level:** *High* — 18 issues and 23 PRs updated, 8 PRs merged/closed, 0 new releases.

## Releases

**None.** No new releases were published in the last 24 hours. The last release remains unreported in this period.

## Project Progress

### Merged/Closed PRs Today (8 total)

| PR | Summary | Impact |
|---|---|---|
| [#5140](https://github.com/nearai/ironclaw/pull/5140) — `fix(triggers): surface trigger input errors` | Carries structured repair details from `trigger_create` failures through runtime | **Fixes opaque errors** for invalid automation trigger inputs |
| [#5085](https://github.com/nearai/ironclaw/pull/5085) — `feat(reborn): concurrent turn execution via TurnRunScheduler` | Replaces serial run execution with concurrent, per-user/per-type capped scheduling | **Major architectural upgrade** — unlocks parallel LLM inference across conversations |
| [#5063](https://github.com/nearai/ironclaw/pull/5063) — `feat(reborn): per-turn auto-approve resolution` | DB-backed global auto-approve toggle with never-auto-approve hard floor | **User-facing approval policy** fix (#4959) — changes take effect without restart |
| [#5062](https://github.com/nearai/ironclaw/pull/5062) — `feat(approvals): per-tool permission override model` | Adds `always_allow`/`ask_each_time`/`disabled` per-tool states and store | **Permission model foundation** for Reborn (#4958) |
| [#5135](https://github.com/nearai/ironclaw/pull/5135) — `refactor(reborn): decompose composition god-crate` | Splits 132k-line crate into 6 focused crates | **Codebase maintainability** — reduces build time and merge conflicts |
| [#5081](https://github.com/nearai/ironclaw/pull/5081) — `[codex] Add hosted single-tenant Postgres profile` | New deployment profile with PostgreSQL-backed durable state | **Hosted preview path** — local-dev surface with production-grade storage |
| [#4985](https://github.com/nearai/ironclaw/pull/4985) — `Engine V2: persist LLM usage` | Fixes empty `/api/admin/usage` on Engine V2 deployments | **Admin visibility fix** — usage tracking now works for Web UI and Responses API |
| [#5116](https://github.com/nearai/ironclaw/pull/5116) — `build(deps): bump everything-else group` | 44 dependency updates across agent-client-protocol, rustls, etc. | **Supply chain hygiene** — keeps dependencies current |

### Notable Open PRs Advancing

- **[#5137](https://github.com/nearai/ironclaw/pull/5137)** — First incremental extraction of `ironclaw_reborn_http_kit` from the composition god-crate
- **[#5133](https://github.com/nearai/ironclaw/pull/5133)** — Adds automation delete support for Reborn automations
- **[#5131](https://github.com/nearai/ironclaw/pull/5131)** — Adds automation pause/resume support
- **[#5061](https://github.com/nearai/ironclaw/pull/5061)** — Hermes-style skill extraction and self-evolution for Reborn (large feature from new contributor)

## Community Hot Topics

### Most Active Discussions

1. **[#5139 — `reborn regression: web/research tasks hang at init (0 LLM calls)`](https://github.com/nearai/ironclaw/issues/5139)** (1 comment)
   - **What:** Critical regression on `main` HEAD — 21/147 PinchBench tasks fail with zero LLM/tool calls, timing out before producing any output.
   - **Underlying need:** The community urgently needs a stable development baseline. This regression blocks all Reborn evaluation work that uses web/research capabilities.

2. **[#4879 — `IronClaw Reborn Local Dogfooding Findings 06/15-06/21`](https://github.com/nearai/ironclaw/issues/4879)** (2 comments)
   - **What:** Cumulative tracker for local-first-run issues: WebUI startup, configuration, model-provider setup.
   - **Underlying need:** First-time user onboarding remains rough. The dogfooding process surfaces that the "smooth start" experience is not yet production-quality.

3. **[#5129 — `Investigate Always approve not working for outbound_delivery_target_set`](https://github.com/nearai/ironclaw/issues/5129)** (1 comment)
   - **What:** Approval bypass not functioning for a specific capability setter—exact failure mode unknown.
   - **Underlying need:** Approval policy consistency is critical for users who rely on auto-approve for routine operations. Inconsistency undermines trust in the policy system.

4. **[#4925 — `NEAR AI MCP shows "SETUP NEEDED" despite being ready`](https://github.com/nearai/ironclaw/issues/4925)** (1 comment, closed)
   - **What:** UI state mismatch—pre-configured MCP server falsely reports needing configuration.
   - **Underlying need:** Users need clear, honest UI state indication. False "SETUP NEEDED" warnings erode confidence in the extension/MCP system.

## Bugs & Stability

### High Severity — Critical Regressions

| Issue | Description | Impact | Fix Status |
|---|---|---|---|
| [#5139](https://github.com/nearai/ironclaw/issues/5139) | `main` HEAD (704fcd43) introduces web/research task hang — zero LLM calls, zero tool calls, 21/147 PinchBench tasks timeout | **Blocks benchmarking & evaluation** on latest code. Bisected to a 10-commit range. | No fix PR yet; author plans controlled experiment. |
| [#5129](https://github.com/nearai/ironclaw/issues/5129) | `Always approve` not working for `outbound_delivery_target_set` — exact failure mode unclear | **Breaks auto-approve workflow** for delivery target configuration. | Needs reproduction and diagnosis. |
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | Nightly E2E scheduled run failed — `Full E2E / E2E (v2-engine)` | **CI pipeline instability** — ongoing since 2026-05-27 with no resolution. | Long-standing flakiness; no fix PR attached. |

### Medium Severity — Functional Defects

- **Engine V2 `/api/admin/usage` empty** — Fixed by [#4985](https://github.com/nearai/ironclaw/issues/4985) (merged)
- **`trigger_create` opaque errors** — Fixed by [#5140](https://github.com/nearai/ironclaw/pull/5140) (merged)

### Low Severity — Usability / UI

- **NEAR AI MCP false "SETUP NEEDED"** — Closed as fixed ([#4925](https://github.com/nearai/ironclaw/issues/4925))

## Feature Requests & Roadmap Signals

### Likely to Land in Next Release

| Feature | Tracker | Status | Why Likely |
|---|---|---|---|
| **Telegram channel support** | [#5124](https://github.com/nearai/ironclaw/issues/5124) | New (today) | Parent of Reborn dogfooding sprint; explicit goal. |
| **Automation pause/resume** | [#5121](https://github.com/nearai/ironclaw/issues/5121) | Open PR [#5131](https://github.com/nearai/ironclaw/pull/5131) | PR already submitted. |
| **Automation delete** | [#5122](https://github.com/nearai/ironclaw/issues/5122) | Open PR [#5133](https://github.com/nearai/ironclaw/pull/5133) | PR already submitted. |
| **Perf: Latency logging + turn timing** | [#5126](https://github.com/nearai/ironclaw/issues/5126) | New (today) | Foundational for all other performance work. |
| **Skill extraction & self-evolution** | PR [#5061](https://github.com/nearai/ironclaw/pull/5061) | Open from new contributor | Major new capability — Hermes-style learning. |

### Longer-Range Signals

- **Concurrent turn execution** — PR [#5085](https://github.com/nearai/ironclaw/pull/5085) merged today, enabling parallel LLM inference
- **Composition god-crate decomposition** — PR [#5135](https://github.com/nearai/ironclaw/pull/5135) merged, PR [#5137](https://github.com/nearai/ironclaw/pull/5137) in progress
- **Hosted single-tenant Postgres profile** — PR [#5081](https://github.com/nearai/ironclaw/pull/5081) merged — path to production deployments
- **/v1/models & external-tool gate** — PR [#5094](https://github.com/nearai/ironclaw/pull/5094) open — OpenAI-compatible surface work
- **Unified gate declined semantics** — [#5120](https://github.com/nearai/ironclaw/issues/5120) — tidying auth/approval/projection language

## User Feedback Summary

### Pain Points (from issues and dogfooding trackers)

1. **Performance / Latency** — Users report local Reborn "feels slow." Performance tracker [#5125](https://github.com/nearai/ironclaw/issues/5125) was created specifically to address this, with sub-issues for inference latency ([#5127](https://github.com/nearai/ironclaw/issues/5127)), unnecessary runtime steps ([#5128](https://github.com/nearai/ironclaw/issues/5128)), and missing timing attribution ([#5126](https://github.com/nearai/ironclaw/issues/5126)).

2. **First-run & Configuration** — Dogfooding findings ([#4879](https://github.com/nearai/ironclaw/issues/4879), [#5119](https://github.com/nearai/ironclaw/issues/5119)) consistently highlight WebUI startup, model-provider setup, and configuration friction. This is a repeated pattern across the past two weeks.

3. **Approval Policy Inconsistency** — [#5129](https://github.com/nearai/ironclaw/issues/5129) shows that even after the global auto-approve feature landed ([#4959](https://github.com/nearai/ironclaw/issues/4959), PR [#5063](https://github.com/nearai/ironclaw/pull/5063)), specific capabilities still fail to respect the policy. Users need consistent, predictable approval behavior.

4. **UI State Trust** — The NEAR AI MCP false "SETUP NEEDED" bug ([#4925](https://github.com/nearai/ironclaw/issues/4925)) shows users are sensitive to UI signals that conflict with actual system state.

### Satisfaction Signals

- **Concurrent execution** landed to a warm reception — the serial runner was a known pain point
- **Per-tool permission model** (#4958) and **auto-approve without restart** (#4959) both closed today, addressing long-standing approval workflow gaps
- Active dogfooding cadence (weekly trackers) shows disciplined internal use and direct feedback loop

## Backlog Watch

### Stale Issues Needing Maintainer Attention

| Issue | Age | Why Concerning |
|---|---|---|
| [#4108 — `Nightly E2E failed`](https://github.com/nearai/ironclaw/issues/4108) | 27 days (since 2026-05-27) | **CI is persistently broken** for `v2-engine` E2E. No fix or PR attached. Indicates possible test infrastructure debt or flaky test acceptance. |
| [#4032 — `build(deps): bump the wasm group`](https://github.com/nearai/ironclaw/pull/4032) | 29 days (since 2026-05-25) | Stale Dependabot PR. WASM toolchain updates may be blocked by compatibility or merge conflicts. |

### Long-Running Open PRs

| PR | Age | Status |
|---|---|---|
| [#4787 — `[NO MERGE] - Barcelona Hackathon`](https://github.com/nearai/ironclaw/pull/4787) | 11 days | Deliberately not mergeable — fork for stable hackathon track. |
| [#4712 — `Move Slack setup into WebUI`](https://github.com/nearai/ironclaw/pull/4712) | 13 days | Open, being reviewed. Large feature for Slack channel management. |
| [#4969 — `fix(google-wasm): auth required errors`](https://github.com/nearai/ironclaw/pull/4969) | 7 days | Google tooling fix — awaiting merge or further testing. |

### New Contributor PRs Needing Review

- **[#5132 — `fix(webui-v2): redirect invalid chat thread routes`](https://github.com/nearai/ironclaw/pull/5132)** — From rafly-habibi (new contributor), L-sized fix for chat route edge cases. No comments yet.
- **[#5134 — `[codex] add GitHub bug workflow design docs`](https://github.com/nearai/ironclaw/pull/5134)** — From BenKurrek (regular contributor), adds engineering design docs for a GitHub bug-fix workflow MVP.

---

*Generated from IronClaw GitHub data for 2026-06-23. All URLs are under `https://github.com/nearai/ironclaw`.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

LobsterAI Project Digest — 2026-06-23
1. Today’s Overview
The project shows moderate activity today with 5 updated issues (all open, all stale) and 14 updated pull requests, of which 6 were merged or closed. The burst of merged PRs (7 in the last 24 hours) indicates a focused sprint of fixes and features, particularly around the OpenClaw plugin system, the new Cowork Plan Mode, and test alignment. Notably, no new releases were cut, suggesting the team is consolidating code before a potential version bump. The high number of open issues marked as “stale” (many from early April) signals a growing backlog of unresolved user-facing bugs.

2. Releases
None.

3. Project Progress
The following PRs were merged or closed today, representing significant forward motion:

- #2183 (feat(cowork): add plan mode workflow) — A major new feature merging Plan Mode, which adds a structured planning step to the composer, including interactive blocks for proposed plans, the ability to copy/download/expand/collapse plans, and a safety gate that prevents mutating tool calls while planning.
- #2187 (test: align OpenClaw metadata expectations) — Updated renderer and history reconciliation tests to support reasoning-capable model metadata; 146 tests passed.
- #2186 (fix(openclaw): compile NIM plugin runtime entry) — Extracted shared TypeScript plugin preparation scripts and fixed the NIM channel’s runtime entry compilation before OpenClaw CLI installation.
- #2185 (fix(openclaw): include cwd in reply options patch) — Fixed a missing field in the OpenClaw v2026.6.1 run-cwd patch, unblocking plugin SDK declaration generation.
- #2184 (docs(agents): update repository guidance) — Refreshed AGENTS.md with current Cowork/OpenClaw architecture and new contribution quality gates (Codex scope, changed-file lint policy).
- #2182 (fix(openclaw): support upgraded im plugin installs) — Upgraded preinstalled IM plugins (DingTalk, Lark/Feishu, WeCom, POPO) and aligned with OpenClaw 2026.6.1 plugin install layouts.

All merged PRs are linked to the same author (btc69m979y-dotcom, liuzhq1986), indicating a coordinated push.

4. Community Hot Topics
All current open issues and PRs have zero reactions and minimal comments, suggesting low community engagement on the tracker. The most “active” items by recent update are the stale issues from April, but none show discussion depth. The notable exception by impact is:

- #1414 (Bug: “总会话数”始终显示为0) — A clear data inconsistency bug (total session count stuck at 0) with supporting evidence (total API calls = 432, real usage visible). This has high user visibility on the profile page.
- #1411 (Bug: 概览页时间维度筛选器点击无响应) — A UI interaction block that makes the profile page’s time range filter non-functional.

Both issues have been open for 2.5 months without resolution.

5. Bugs & Stability
Two new bugs were not reported today, but 5 stale bugs remain open. Ranked by severity:

1. #1414 (总会话数始终为0) — HIGH. A key metric on the profile page is broken, undermining trust in usage statistics.
2. #1416 (英文切换UI布局错乱) — MEDIUM. Text overlap after locale switch degrades the UX for English users.
3. #1411 (时间维度筛选器无响应) — MEDIUM. A clickable element that does nothing is a basic interaction failure.
4. #1409 (定时任务未生成历史记录) — MEDIUM. Scheduled tasks silently fail to produce expected outputs.
5. #1413 (Skills较多时页面展示不友好) — LOW. A layout issue that is cosmetic but annoying for power users.

No fix PRs exist for any of these bugs in today’s activity. The only stability-related work today was on DB performance (PR #1410, #1415, #1421) and concurrency safety (PR #1420), but those are still open (stale).

6. Feature Requests & Roadmap Signals
No formal feature requests were filed today. However, the merged #2183 (Plan Mode) signals a major roadmap item: adding structured, multi-step agent workflows to Cowork. This suggests the team is investing in making the AI agent more deliberative and less reactive. The OpenClaw plugin infrastructure work (#2182, #2185, #2186) indicates a push toward improved third-party integration and IM channel support. These are strong candidates for inclusion in the next version (v2026.7?).

7. User Feedback Summary
Direct user feedback is sparse. The existing bug reports paint a picture of dissatisfaction with the Profile/Overview page:
- Users cannot trust the session count (#1414).
- Users cannot change the time range filter (#1411).
- English-speaking users encounter broken layouts (#1416).

These are “last mile” UI polish issues that, while not crashing the app, erode user confidence. The lack of comments on the open PRs suggests either that the community is small or that users are not engaging via GitHub. There is no evidence of missing or wanted features from user comments today.

8. Backlog Watch
The following items have been open for over 2.5 months and are marked as “stale”:

- #1409 (定时任务未生成历史记录) — No movement since creation.
- #1411, #1413, #1414, #1416 (profile/bugs) — All from 2026-04-03, no maintainer responses in 80 days.
- #1407, #1408, #1410, #1415, #1419, #1420, #1421 (Open PRs) — All from 2026-04-03, no reviewer activity in 80 days. These include critical concurrency and performance fixes (#1420, #1410) that remain unmerged.

This 80-day silence on significant fixes (especially the cron concurrency issue #1420 and the SQLite write bottleneck #1410) is a red flag for the project’s velocity on stability work. Maintainer attention is urgently needed on these PRs.

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

Here is the structured CoPaw project digest for 2026-06-23.

---

# CoPaw Project Digest: 2026-06-23

## Today's Overview
Activity remains very high, with 50 PRs and 22 Issues updated in the last 24 hours. The project is currently in a "stabilization and polish" phase: while major features (mobile adaptation, context management) are landing, a significant volume of bug reports and regressions (particularly around model configuration, session switching, and cron jobs) indicate that the `v1.1.12.post1` release introduced several quality issues. The community is actively contributing, with a high number of first-time contributors submitting mobile-responsive UI fixes.

## Releases
**No new releases were published today.** The current stable version remains `v1.1.12.post1`.

## Project Progress
20 PRs were merged or closed today, signaling strong forward momentum on both bug fixes and features.

- **Context & Model Fixes:**
    - [#5306](https://github.com/agentscope-ai/QwenPaw/pull/5306): Fixed the context usage popover displaying the wrong context window size.
    - [#5386](https://github.com/agentscope-ai/QwenPaw/pull/5386): Fixed the context usage ring not updating the denominator after a user switches the active model mid-session.
- **Security & Infrastructure:**
    - [#5028](https://github.com/agentscope-ai/QwenPaw/pull/5028): Fixed a security issue where the keychain master key was shared across all installs on a machine, isolating it per install path.
    - [#5027](https://github.com/agentscope-ai/QwenPaw/pull/5027): Stopped backend warmup sessions from polluting the user’s chat console and added session resume functionality.
- **Community Contributions (Mobile Adaptation):**
    - First-time contributor [yaozy2020](https://github.com/yaozy2020) merged fixes for session switching stuck states ([#5357](https://github.com/agentscope-ai/QwenPaw/pull/5357)).

## Community Hot Topics
The community is deeply engaged, with several issues sparking detailed technical discussion.

- **#5218: Sub-Agent Context Compaction Freeze** (17 comments, Open)
    - *Link:* [Issue #5218](https://github.com/agentscope-ai/QwenPaw/issues/5218)
    - *Analysis:* This is the most discussed bug. A user reports that the entire QwenPaw process freezes when a sub-agent triggers context compression, requiring a manual restart. The high activity suggests this is a critical pain point for users running multi-agent workflows. No fix PR is open yet, making this a top priority.
- **#5262: Disabled Skills Re-enable After Upgrade** (9 comments, Open)
    - *Link:* [Issue #5262](https://github.com/agentscope-ai/QwenPaw/issues/5262)
    - *Analysis:* A persistent regression across versions (1.1.9 → 1.1.11). Users are frustrated that disabled built-in skills (e.g., `docx`, `xlsx`) are re-enabled after every update. This is a classic configuration persistence bug that impacts user trust in upgrades.
- **#5345: Custom OpenAI-compatible Providers Don't Support Function Calling** (5 comments, Open)
    - *Link:* [Issue #5345](https://github.com/agentscope-ai/QwenPaw/issues/5345)
    - *Analysis:* A power user reports that custom OpenAI-compatible providers (like OMLX) fail to call tools, while native Ollama works fine. This highlights a gap in the provider abstraction layer that limits model choice for advanced users.

## Bugs & Stability
Several significant regressions and stability issues were reported today, primarily targeting the `v1.1.12.post1` release.

| Severity | Issue | Description | Fix PR? |
| :--- | :--- | :--- | :--- |
| **Critical** | [#5218](https://github.com/agentscope-ai/QwenPaw/issues/5218) | Process freeze on sub-agent context compression. | No |
| **High** | [#5398](https://github.com/agentscope-ai/QwenPaw/issues/5398) | Cron scheduler stops dispatching enabled jobs while app is alive. | No |
| **High** | [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401) | Frontend crashes (white screen) when rendering large tool-use history. | No |
| **Medium** | [#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403) | Browser autofill hijacks search input on Model Config page. | No |
| **Medium** | [#5378](https://github.com/agentscope-ai/QwenPaw/issues/5378) | Adding a custom model corrupts the model page, breaking usage. | No |
| **Medium** | [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) | `Internal Server Error` on fresh install via Python. | No |
| **Low** | [#5370](https://github.com/agentscope-ai/QwenPaw/issues/5370) | `send_file_to_user` results in HTTP 404 (closed/resolved). | Yes (Closed) |

**Analysis:** The prevalence of regressions in the latest `.post1` release suggests the testing pipeline may need strengthening. The cron scheduler (Issue #5398) and frontend rendering crash (Issue #5401) are particularly damaging to core functionality.

## Feature Requests & Roadmap Signals
User requests today point towards greater flexibility and persistence.

- **Agent-Workspace Decoupling ([#5392](https://github.com/agentscope-ai/QwenPaw/issues/5392)):** A detailed request to decouple agents from workspaces, allowing an agent to be reused and switched between different workspaces. This is a significant architectural ask that aligns with enterprise usage patterns.
- **Personal Knowledge Base ([#2969](https://github.com/agentscope-ai/QwenPaw/issues/2969)):** A long-standing request (since April) with 2 👍. Users want a built-in knowledge base UI to combine CoPaw’s task execution with personal documents.
- **Recall-Aware Memory Consolidation ([#5387](https://github.com/agentscope-ai/QwenPaw/issues/5387)):** A sophisticated feature request to use recall frequency as a signal for what memories to consolidate, rather than just recency.
- **Import from OpenClaw/Hermes ([#5254](https://github.com/agentscope-ai/QwenPaw/issues/5254)):** A user migration request, indicating CoPaw is attracting users from competing projects.

**Prediction:** The mobile-responsive PRs from first-time contributors and the "Scroll" context manager ([#5321](https://github.com/agentscope-ai/QwenPaw/pull/5321)) are likely candidates for the next minor release.

## User Feedback Summary
- **Pain Points:**
    - **Update Fatigue:** Users are frustrated by regressions that break configuration persistence (disabled skills, corrupted model pages) after every update.
    - **Model Compatibility:** Users with custom or less common providers (Zhipu, OMLX) are hitting inconsistent API support, breaking trust in the "custom provider" feature.
    - **Stability:** The "Dream Task" feature (scheduled memory summaries) is failing for multiple users, and session switching is "sticky" and confusing.
- **Satisfaction Indicators:**
    - The new message queue feature ([#5354](https://github.com/agentscope-ai/QwenPaw/issues/5354)) was praised as a "great improvement" for efficiency, even though it introduced a session-switching bug.
    - The community is actively contributing code, with several first-time contributors submitting valuable mobile adaptation PRs, indicating a healthy and engaged developer ecosystem.

## Backlog Watch
- **Issue #2969: Personal Knowledge Base** (Created: April 5, Last updated: June 22)
    - *Link:* [Issue #2969](https://github.com/agentscope-ai/QwenPaw/issues/2969)
    - *Status:* Open, 5 comments, 2 👍.
    - *Action:* This feature has been open for over 2 months with no maintainer response. It is a high-value feature request gaining community traction. A status update or "under consideration" label from the team would improve community sentiment.
- **PR #5097: Fix Shield icon centering** (Created: June 11, Last updated: June 22)
    - *Link:* [PR #5097](https://github.com/agentscope-ai/QwenPaw/pull/5097)
    - *Status:* Open, 0 comments.
    - *Action:* A simple UI fix PR that has been waiting for review for 12 days. Stale UI PRs can discourage future contributions.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-23

## 1. Today's Overview

ZeroClaw continues at very high engineering velocity, with 50 issues and 50 PRs updated in the last 24 hours — consistent with the sustained surge seen over the past several days. Closed issue volume (8) and merged/closed PR volume (7) remain healthy, indicating the maintainers are actively merging fixes and closing tracked work while the open queue grows. Activity centers on three major fronts: hardening the runtime and plugin systems (MCP tool delivery, signature enforcement, session TTL), a sweeping infrastructure modernization push toward WebAssembly-first architecture and supply-chain security, and ongoing channel reliability fixes (WhatsApp, Telegram, Discord, and keybinding conflicts on macOS). The project hosts a lively RFC-driven design culture, with several high-risk RFCs in active review this cycle.

## 2. Releases

**No new releases today.** The most recent release remains v0.8.1 (Debian container). The milestone tracker for v0.8.3 (runtime stability) holds 1 open issue, and the larger v0.9.0 milestone (auth, security, breaking changes) contains 134 open items.

## 3. Project Progress

Seven PRs were closed/merged in the last 24 hours, reflecting significant forward movement:

- **#8097** (*fix(model_switch): resolve list_models from live models.dev catalog*) — Merged. Model switching now queries a live catalog instead of relying on a stale hardcoded list, with the offline list as fallback.
- **#8191** (*docs(rustdoc): quiet warning links*) — Merged. Reduces documentation build noise by fixing intra-doc link resolution and localization handling.
- **#8200** (*Integration branch for all singlerider open PRs [QA - DO NOT MERGE]*) — New throwaway QA integration branch, merging all open PRs by @singlerider for pre-release testing.
- Several other PRs merged with smaller scope: #7688 (hook panic recovery tests), #6371 (WhatsApp group allowlist), #6037 (cron job duplicate launch fix), #8013 (Discord channel disable fix).

## 4. Community Hot Topics

The most active discussions reflect deep architectural debates and blockers:

- **#8193** — *bug(zerocode): MCP tools/tool_search missing from TUI sessions while gateway sees them* (3 comments, 24h old). A critical S1 workflow blocker: MCP servers connect and tools register, but the Zerocode TUI never receives them. A fix PR (#8199) was opened the same day by @OmkumarSolanki, initializing MCP for Chat TUI sessions. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8193)

- **#8177** — *RFC: Supply chain signing - hardware PGP, hermetic builds, and SLSA provenance* (3 comments, 24h old). Expands the hardened CI pipeline (Phase 3) with hardware-backed signing and offline multi-party quorum. Reflects ZeroClaw's growing maturity posture. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8177)

- **#8132** — *RFC: Replace React/Vite web UI build with Rust→Wasm framework* (2 comments, 1 reaction 👍). Proposes eliminating the npm toolchain entirely by replacing the React SPA with Dioxus/Leptos/Yew compiled to Wasm. Part of a larger zero-Node.js vision. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8132)

- **#8135** — *RFC: Wasm-first plugin runtime — default-on, capability enforcement, signed distribution* (1 comment, 24h old). Proposes making Wasm the default plugin runtime with signed, capability-declaring modules. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8135)

## 5. Bugs & Stability

Several high-severity bugs were reported or had progress made today:

**S1 (workflow blocked):**
- **#8193** — MCP tools missing from TUI sessions (see above). Fix PR #8199 exists.
- **#8154** — Kimi Code (Moonshot) endpoint returns HTTP 404; the correct URL is `https://api.kimi.com/coding/v1`. Reported by @jparga. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/8154)

**S0 (data loss / security risk) — resolved:**
- **#8013** — Disabling an agent no longer stops its Discord channel. Previously closed, but the fix appears to have been merged today.

**Ongoing S1 bugs with active fix PRs:**
- **#7756** — MCP tools unavailable on OpenAI Responses/Anthropic reasoning turns (2 comments today). [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7756)
- **#5808** — Default 32k context budget exceeded on iteration 1, causing perpetual trim. @JordanTheJet's report is 68 days old but still open. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)

**New fix PRs addressing known bugs:**
- **#8172** — *feat(plugins): honor configured signature policy when loading plugin tools* — Fixes a security gap where the runtime hardcoded `SignatureMode::Disabled` and an empty trusted-key store, bypassing user-configured plugin security policy.
- **#8203** — *fix(channel): `refreshed_new_session_system_prompt` load bundled_skill* — Silently omitted bundled skills from channel session system prompts.
- **#8166** — *fix(zerocode): change browse enter/exit from ctrl+up/down to alt+up/down* — Resolves macOS keybinding conflict with Mission Control (#8075).

## 6. Feature Requests & Roadmap Signals

Several user-requested features show clear roadmap intent:

- **#8125** — *Automatically set risk profile to yolo in quickstart* (@singlerider). Proposes auto-applying the "yolo" risk preset during onboarding to prevent new users from unintentionally hitting restrictive defaults. A companion PR (#8133) redefines "Balanced" as the trusted-local daily driver. Likely for v0.8.3.

- **#8138** — *Support OpenRouter model fallbacks array* (@vinitasher). Users want automatic model failover when the primary model is rate-limited or down. Easily configurably addition — possible for v0.8.3 or v0.9.0.

- **#8075/#8166** — macOS keybinding fixes for Zerocode TUI. Merged today.

- **#8134** — *session_ttl_hours - Auto-truncate stale session history* (@jokewithme110). Adding implementation for an already-existing config parameter; likely for v0.8.3.

- **#8170** — *In-app upgrade with optional supervised restart from web dashboard* (@NiuBlibing). A larger feature likely targeting v0.9.0 or later.

## 7. User Feedback Summary

Real user pain points surfaced this cycle reflect two primary axes of dissatisfaction:

1. **Configuration complexity and unexpected defaults:** Multiple reports around risk profiles confusing new users (#8125), context budget defaults causing perpetual trimming (#5808), and the "yolo" preset wanting parity with "unbounded" runtime profiles.

2. **Tool delivery inconsistency:** Users report that MCP tools work in the gateway and via CLI but vanish in the TUI (#8193), and that native tools don't reach OpenAI/Anthropic reasoning turns (#7756). This undermines the core value proposition of a universal tool platform.

3. **Channel operational friction:** Discord channels not stopping when agents are disabled (#8013, now fixed), stale session history consuming tokens (#8134), and missing attachment references in cached history (#8153).

Positive signals: the community is actively contributing fix PRs, and the integration QA branch (#8200) suggests the maintainers are preparing a coordinated release.

## 8. Backlog Watch

Several important items remain open with maintainer attention needed:

- **#5808** (68 days old, S1, priority: P1) — Default 32k context budget exceeded on iteration 1. Despite being marked `status:accepted` and `status:in-progress`, no fix PR has appeared. This remains the longest-standing workflow blocker and should be a priority for v0.8.3. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)

- **#7462** (13 days old, S2, 74 test failures on Windows) — No PR exists. Maintainers have not engaged on platform parity despite the open bug being tagged `status:accepted`. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)

- **#6943** (28 days old, P2) — RFC to deconflict plugin system goals in FND-001 by replacing Extism with a direct wasmtime Component Model host. Multiple RFCs (#8135, #7674) now overlap with or supersede this proposal — maintainers should clarify whether this RFC is superseded. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/6943)

- **#7269** (18 days old, P3) — Docs build warning noise. Low priority but easy to fix and would improve contributor experience. [View Issue](https://github.com/zeroclaw-labs/zeroclaw/issues/7269)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*