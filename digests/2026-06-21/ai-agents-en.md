# OpenClaw Ecosystem Digest 2026-06-21

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-21 02:16 UTC

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

# OpenClaw Project Digest — 2026-06-21

## Today's Overview

OpenClaw is in a high-activity maintenance and stabilization cycle with 500 active issues and 461 open pull requests, reflecting strong community engagement concurrent with substantial ongoing engineering work. The project released v2026.6.9, which focused on Telegram delivery quality improvements. However, the project continues to grapple with a significant backlog of P1 regression bugs and session-state integrity issues, many of which remain open pending product decisions or maintainer review. The most pressing cluster of problems involves session/transcript SQLite migration, compaction timeouts, subagent orchestration failures, and channel-specific delivery regressions across Telegram, Feishu, Matrix, and Slack. Despite this, the volume of active PRs (~39 merged/closed today) shows steady forward momentum in addressing systemic issues.

## Releases

**v2026.6.9 (openclaw 2026.6.9)** — New release

**Key Changes:**
- Richer Telegram delivery: rich HTML, rich markdown and sticker path preservation, improved progress drafts and command output rendering, safe HTML table normalization, correct mention and spooled handler delivery
- Underlying PRs: #93286, #93164, #9

**Migration Notes:** No breaking changes or migration notes specified in this release.

## Project Progress

**Merged/Closed PRs Today:** 39 PRs were merged or closed.

**Notable closed/merged PRs (recently active):**
- [#68936 — Autofix: add PR review autofix pipeline + Windows daemon](https://github.com/openclaw/openclaw/pull/68936) (CLOSED) — Large PR (XL) adding a Claude Agent SDK-powered review autofix pipeline and Windows background daemon for gateway supervision

**Active PRs nearing completion (status: "ready for maintainer look"):**
- [#95386 — Generic JSONL line-parsing hook for CliBackendPlugin (fixes #95351)](https://github.com/openclaw/openclaw/pull/95386) — Extends CLI backend plugin support beyond claude-stream-json, enabling third-party CLI tool-card event paths
- [#92495 — fix(opencode): restore Zen model catalog](https://github.com/openclaw/openclaw/pull/92495) — Fixes the opencode Zen provider that required hand-registration; restores provider-owned catalog
- [#84288 — fix(discord): avoid duplicate typing keepalive for tool replies](https://github.com/openclaw/openclaw/pull/84288) — Fixes Discord showing stale "bot is typing" for message-tool-only replies
- [#93198 — fix #80933: honor claude-cli contextTokens](https://github.com/openclaw/openclaw/pull/93198) — Fixes claude-cli sessions ignoring configured contextTokens cap
- [#93655 — fix(agent): classify stuck recovery as idle timeout](https://github.com/openclaw/openclaw/pull/93655) — Prevents stuck-session watchdog from marking active runs as externally aborted
- [#95436 — fix #91171: sub-agent model routing ignores model parameter](https://github.com/openclaw/openclaw/pull/95436) — Forward resolved provider/model into child gateway launch

## Community Hot Topics

**Most Active Issues (by comment count):**

1. **[#88838 — Track core session/transcript SQLite migration via accessor seam](https://github.com/openclaw/openclaw/issues/88838)** (31 comments)
   - **Author:** jalehman | **Created:** 2026-06-01 | **Status:** OPEN, P1
   - **Summary:** Breaking a full session/transcript migration into small reviewable PRs via branch-by-abstraction seam. This is the highest-comment-count issue and reflects deep architectural debate about the migration approach.
   - **Underlying Need:** The community and maintainers want to avoid a high-risk monolithic rewrite of session/transcript storage, preferring incremental, reviewable changes.

2. **[#85333 — openclaw doctor --fix 4-5x slower on 2026.5.20 vs 2026.5.19](https://github.com/openclaw/openclaw/issues/85333)** (13 comments)
   - **Author:** samson1357924 | **Created:** 2026-05-22 | **Status:** OPEN, P1
   - **Summary:** Performance regression: `doctor --fix` went from 55s to 229s+ due to session snapshot path traversal bottleneck
   - **Underlying Need:** Users need predictable CLI tooling performance for production operations.

3. **[#92201 — Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic)](https://github.com/openclaw/openclaw/issues/92201)** (11 comments)
   - **Author:** CarlCapital | **Created:** 2026-06-11 | **Status:** OPEN, P1
   - **Summary:** Anthropic thinking blocks with invalid signatures cause unrecoverable errors; recovery wrapper never fires
   - **Underlying Need:** Anthropic provider path reliability is critical for users relying on streaming thinking blocks.

4. **[#86519 — Agent repeats identical replies 2-10x on Telegram after 5.20 update](https://github.com/openclaw/openclaw/issues/86519)** (10 comments)
   - **Author:** w3-design1 | **Created:** 2026-05-25 | **Status:** OPEN, P1
   - **Summary:** Duplicate reply regression on Telegram, partially mitigated in 5.22 but not fully fixed
   - **Underlying Need:** Telegram channel reliability remains a pain point with long-standing regressions.

5. **[#84583 — cron announce delivery triggers EmbeddedAttemptSessionTakeoverError](https://github.com/openclaw/openclaw/issues/84583)** (9 comments, 3 👍)
   - **Author:** jonah791 | **Created:** 2026-05-20 | **Status:** OPEN, P2
   - **Summary:** Cron job completion delivery conflicts with active user sessions, causing session takeover errors
   - **Underlying Need:** Reliable cron job completion delivery without disrupting active user conversations.

## Bugs & Stability

### P1 Bugs (Critical)

| Issue | Description | Has Fix PR? |
|-------|-------------|-------------|
| [#85333](https://github.com/openclaw/openclaw/issues/85333) | `doctor --fix` 4-5x slower (55s → 229s+) | No |
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | Anthropic thinking signature invalid on replay; recovery wrapper never fires | No |
| [#86519](https://github.com/openclaw/openclaw/issues/86519) | Agent repeats replies 2-10x on Telegram (regression since 5.20) | No |
| [#92043](https://github.com/openclaw/openclaw/issues/92043) | 180s compaction timeout is wall-clock over whole pipeline — legitimately long compactions fail identically every turn | No (linked PR open) |
| [#92460](https://github.com/openclaw/openclaw/issues/92460) | Isolated cron completion announcer drops explicit `delivery.channel` | No (linked PR open) |
| [#92415](https://github.com/openclaw/openclaw/issues/92415) | `AgentSession.this.model` snapshot never refreshed after `/model` switch | No (linked PR open) |
| [#90325](https://github.com/openclaw/openclaw/issues/90325) | Matrix channel dispatch broken — `Cannot read properties of undefined (reading 'run')` | No |
| [#91009](https://github.com/openclaw/openclaw/issues/91009) | Codex PreToolUse hook spawns CPU-bound processes, stalls gateway RPC | No (linked PR open) |
| [#91363](https://github.com/openclaw/openclaw/issues/91363) | Isolated cron consistently fails with "LLM request failed" — model requests never reach provider | No |
| [#91804](https://github.com/openclaw/openclaw/issues/91804) | Internal reasoning leakage exposed to users (v2026.6.5 regression) | No |
| [#90925](https://github.com/openclaw/openclaw/issues/90925) | Subagent announce compaction falls into openai-responses API-key route | No |
| [#88870](https://github.com/openclaw/openclaw/issues/88870) | Stuck-session recovery aborts long-but-active runs at warnMs×3 with misleading "user abort" message | No (linked PR open) |
| [#94228](https://github.com/openclaw/openclaw/issues/94228) | Native Anthropic path: replaying historical thinking blocks bricks long tool-use threads (HTTP 400) | No (linked PR open) |

### P2 Bugs (Significant)

| Issue | Description | Has Fix PR? |
|-------|-------------|-------------|
| [#94032](https://github.com/openclaw/openclaw/issues/94032) | `exec` private-LAN access fails while same user GUI succeeds | No (linked PR open) |
| [#93375](https://github.com/openclaw/openclaw/issues/93375) | Telegram polling enters silent crash loop after transient network timeout | No (linked PR open) |
| [#90711](https://github.com/openclaw/openclaw/issues/90711) | launchd plist hardcodes StandardErrorPath to /dev/null (5.28 regression) | No (linked PR open) |
| [#91223](https://github.com/openclaw/openclaw/issues/91223) | Active memory injection breaks prompt cache hit rate (99.9% → 22%) | No |
| [#91212](https://github.com/openclaw/openclaw/issues/91212) | Delivery recovery starts before channel transport ready — 0 recovered / N failed | No |
| [#92094](https://github.com/openclaw/openclaw/issues/92094) | `message` tool `action=send` returns "unsupported channel: telegram" | No (linked PR open) |
| [#90595](https://github.com/openclaw/openclaw/issues/90595) | Cron run "failed" notifications fire during hot reload/retries (alert fatigue) | No |
| [#92433](https://github.com/openclaw/openclaw/issues/92433) | Subagent completion silently dropped when announce steers into ending requester run | No (linked PR open) |

**Key Stability Insight:** The project is handling a significant volume of P1 regressions, particularly around session-state management, compaction, cron delivery, and channel-specific issues. Many of these have fix PRs in progress but are waiting on maintainer review or product decisions. The number of "needs-live-repro" tagged issues indicates the maintainers need better reproduction paths.

## Feature Requests & Roadmap Signals

**High-Impact Feature Requests:**

1. **[#90354 — Add bounded/validated append semantics for pre-compaction memory flush](https://github.com/openclaw/openclaw/issues/90354)** (P2, 8 comments)
   - Adding guardrails for memory-flush append size and post-write validation
   - **Prediction:** Likely to land in next minor version given its relationship to ongoing memory stability work

2. **[#90916 — Topic-session families for one assistant across multiple named context lanes](https://github.com/openclaw/openclaw/issues/90916)** (P2, 7 comments)
   - One assistant with multiple named topic lanes, isolated context, shared memory
   - **Prediction:** Medium-term roadmap item — would require substantial session architecture changes

3. **[#14785 — Reduce tool schema token overhead (~3,500 tok/session)](https://github.com/openclaw/openclaw/issues/14785)** (P2, 8 comments)
   - Reducing fixed per-session cost from tool schema loading
   - **Prediction:** High-value optimization candidate; could land in next 1-2 releases

4. **[#91455 — Documentation update for Kubernetes](https://github.com/openclaw/openclaw/issues/91455)** (P3, 7 comments)
   - Improving K8s deployment documentation and Helm chart
   - **Prediction:** Quick win, likely addressed soon given community interest

5. **[#86023 — Codex long-running sessions should use semantic thread/bootstrap cache ownership](https://github.com/openclaw/openclaw/issues/86023)** (P2, 5 comments)
   - Better context cache management for long-running Discord/Codex sessions
   - **Prediction:** Important for production deployments but complex; next major release candidate

## User Feedback Summary

**Pain Points:**
- **Telegram delivery reliability** is the most vocal frustration — duplicate replies (#86519), silent crash loops (#93375), message tool sends failing (#92094), and worker-spooled updates not draining
- **Cron job unreliability** — isolated cron consistently fails (#91363), delivery conflicts with active sessions (#84583), alert fatigue from false failures (#90595)
- **Session state fragility** — compaction timeouts kill legitimate work (#92043), model changes not propagating (#92415), stuck recovery aborts active runs (#88870)
- **Channel-specific regressions** — Matrix broken entirely (#90325), Feishu recovery problems (#91212), Discord typing issues (#84288)
- **Performance degradation** — `doctor --fix` 4-5x slower (#85333), gateway slowdowns under multi-session load (#92057)
- **Configuration friction** — Zen models require hand-registration (#92479), doctor auto-injects bad plugin paths (#85334), config validate rejects plugin extensions (#92884)

**Positive Signals:**
- Rich Telegram delivery improvements in v2026.6.9 are well-received
- Active community engagement with detailed bug reports and reproduction steps
- Multiple "ready for maintainer look" PRs suggest engineering backlog is being actively processed
- Users are providing real production deployment feedback (VPS, multi-session, multi-agent)

## Backlog Watch

**Critical Items Needing Maintainer Attention:**

1. **[#85333 — doctor --fix performance regression](https://github.com/openclaw/openclaw/issues/85333)** (P1, 13 comments)
   - Open since 2026-05-22 (31 days)
   - Tagged: needs-maintainer-review, needs-live-repro
   - No fix PR attached

2. **[#86519 — Telegram duplicate replies](https://github.com/openclaw/openclaw/issues/86519)** (P1, 10 comments)
   - Open since 2026-05-25 (27 days)
   - Tagged: needs-maintainer-review, needs-product-decision
   - No fix PR attached; partial mitigation in 5.22 was insufficient

3. **[#84583 — Cron session takeover errors](https://github.com/openclaw/openclaw/issues/84583)** (P2, 9 comments, 3 👍)
   - Open since 2026-05-20 (32 days)
   - Tagged: needs-product-decision, linked-pr-open
   - High community upvote count

4. **[#90325 — Matrix channel dispatch broken](https://github.com/openclaw/openclaw/issues/90325)** (P1, 7 comments, 2 👍)
   - Open since 2026-06-04 (17 days)
   - Tagged: needs-maintainer-review, needs-product-decision, needs-live-repro
   - Complete channel functionality broken — should be high priority

5. **[#91363 — Isolated cron LLM failures](https://github.com/openclaw/openclaw/issues/91363)** (P1, 6 comments, 4 👍)
   - Open since 2026-06-08 (13 days)
   - Tagged: needs-maintainer-review, needs-product-decision, needs-live-repro
   - Highest 👍 count among open bugs — significant user impact

**Long-Standing Open PRs Requiring Review:**
- [#85403 — fix(telegram): suppress message-tool reply previews](https://github.com/openclaw/openclaw/pull/85403) (P1, 30 days open, "waiting on author")
- [#86655 — feat(claude): add claude-bridge app-server harness extension](https://github.com/openclaw/openclaw/pull/86655) (P2, 27 days open, "waiting on author")
- [#88504 — feat(memory): add multi-slot memory role architecture](https://github.com/openclaw/openclaw/pull/88504) (P2, 21 days open, "waiting on author")

**⚠️ Watch Item:** Issue [#88838](https://github.com/openclaw/openclaw/issues/88838) (SQLite migration seam, 31 comments) has been open since June 1 and is the highest-engagement open issue. This architectural debate could significantly shape the project's direction for session/transcript storage — maintainer decision is overdue.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digest data for June 21, 2026.

---

## Cross-Project Comparison Report: AI Agent Open-Source Ecosystem

### 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is currently characterized by a high degree of **fragmentation and active churn**, with projects rapidly iterating across channels, memory architectures, and core runtime stability. A clear distinction is emerging between **mature, production-focused platforms** (e.g., OpenClaw, IronClaw) that are grappling with regression management and enterprise features, and **emerging, high-velocity projects** (e.g., NanoBot, ZeroClaw) that are aggressively expanding capabilities. A shared, critical pain point across the board is **token overhead and prompt caching**, with users demanding more efficient and cost-effective model interactions. The breadth of channel integrations (from Telegram and Discord to iMessage and QQ) signals a market expectation for omnichannel availability, while the persistent P1 regressions among the most popular projects indicate that stability remains an elusive goal.

### 2. Activity Comparison

| Project | Issues (Open) | PRs (24h Updated) | Release Status (24h) | Health Score & Notes |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 39 (Merged/Closed) | **Released** v2026.6.9 | **Maintenance Mode / Stabilizing.** High volume of activity, but focused on managing a large P1 regression backlog. |
| **NanoBot** | 4 | 4 (Merged) | None | **High-Velocity Growth.** Surge in PRs indicates a release candidate may be approaching. |
| **Hermes Agent** | 44 | 11 (Merged/Closed) | None | **Active & Balancing.** High activity, but bug backlog is outpacing triage. Core community concern is token efficiency. |
| **IronClaw** | 1 | 9 (Merged/Closed) | None | **High-Velocity / Consolidating.** Extremely high PR count for a project with a clean issue tracker. Consolidating major architectural features (Manifest-driven channels, Reborn runtime). |
| **ZeroClaw** | 44 | 9 (Merged/Closed) | None | **Intense Sprint Execution.** Heavy pipeline with concurrent work on skills platform (v0.8.2) and auth (v0.9.0). |
| **CoPaw** | 7 | 1 (Merged) | None | **Stable & Healthy.** Strong community engagement with first-time contributors and responsive maintainers. |
| **PicoClaw** | 2 | 0 (Open) | **Released** v0.3.0-nightly | **Low Activity / Stalled.** Maintenance period with 2 stale items needing maintainer attention. |
| **NanoClaw** | 1 | 0 (Open) | None | **Fix & Documentation Cycle.** 6 open PRs with no merges; may be bottlenecked on review capacity. |
| **NullClaw** | 1 | 0 | None | **Stalled.** Zero PR activity. A single high-severity bug (50% failure rate) threatens user trust. |
| **LobsterAI** | 0 | 0 | None | **Idle.** Activity limited to stale-closing old bugs. No substantive development. |
| **TinyClaw** | 1 | 0 | None | **Low Activity.** Paused on feature dev, awaiting a critical security patch response. |
| **Moltis** | 0 | 0 | None | **Maintenance Mode.** Stable but idle; only activity is a merged Dependabot update. |
| **ZeptoClaw** | 0 | 0 | None | **Inactive.** No activity in the last 24 hours. |

### 3. OpenClaw's Position

OpenClaw maintains its position as the **largest and most stable reference implementation** in the ecosystem, evidenced by the highest absolute volume of community engagement (500 issues, 39 PRs merged/closed). Its primary advantage is **maturity and breadth**, with a proven multi-channel delivery system that spans Telegram, Feishu, Matrix, and Slack.

However, this position comes with significant trade-offs. Its technical approach is **heavier and more monolithic** than newer Rust-based peers like IronClaw or NanoBot. The project is currently bogged down by a **substantial P1 regression backlog** (13+ critical bugs) related to session-state management, SQLite migration, and compaction timeouts, reflecting the cost of maintaining a large, long-lived codebase. While its community is the most vocal and detailed in bug reporting, the velocity of new feature introduction is lower than high-growth peers like **ZeroClaw** and **NanoBot**, which are adding iMessage channels and skills platforms. OpenClaw's current focus is clearly on **stabilization and debt repayment** rather than pioneering new capabilities.

### 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects:

| Shared Need | Affected Projects | Specific Requirement |
| :--- | :--- | :--- |
| **Token Efficiency & Prompt Caching** | **OpenClaw, Hermes Agent, ZeroClaw, PicoClaw, NanoClaw** | Users are demanding lazy tool schema loading, proactive prompt caching (e.g., for Claude), and better visibility into token consumption (73% fixed overhead). |
| **Concurrency & Session State Safety** | **NanoBot, OpenClaw, ZeroClaw** | Race conditions in `Nanobot.run()`, session takeover errors, and compaction timeouts highlight the need for robust, thread-safe session management. |
| **Unified / Pluggable Routing** | **OpenClaw, Hermes Agent, PicoClaw** | Community wants a single, extensible hook for provider/model selection to reduce configuration complexity. |
| **Channel Integration Breadth** | **NanoBot, Hermes Agent, OpenClaw, ZeroClaw** | The ecosystem is racing to support iMessage, Telegram, Discord, WhatsApp, and regional channels like QQ. |
| **Self-Discovery of Capabilities** | **ZeroClaw, Hermes Agent** | Users expect agents to know and advertise their own capabilities (e.g., adding cron jobs). |
| **Native Memory & Learning** | **ZeroClaw, Moltis** | "Dream Mode" features and periodic consolidation are being explored to reduce reliance on external memory tools. |
| **Security Hardening** | **TinyClaw, NanoClaw** | Two separate CVEs (path traversal, unauthenticated file read) indicate a growing need for robust API security. |

### 5. Differentiation Analysis

| Project | Primary Feature Focus | Target User | Technical Architecture |
| :--- | :--- | :--- | :--- |
| **OpenClaw** | **Stability & Channel Delivery** | Production ops, multi-platform deployment | **Python/Rust** (heavy, monolithic) |
| **IronClaw** | **Enterprise Features, Channel Ingress** | Enterprise, scale-up deployments | **Rust** (high-performance, manifest-driven) |
| **Hermes Agent** | **Token Efficiency & Kanban Systems** | Power users, local model users | **Python** (flexible, high internal complexity) |
| **ZeroClaw** | **Skills Platform & Auth (v0.8.2/v0.9.0)** | Developer-first, extensibility | **Rust** (modular with plugin system) |
| **NanoBot** | **Channel Expansion & Performance** | Hackers, integrators | **Python** (lightweight, SDK-focused) |
| **CoPaw** | **Observability & Proxy Compatibility** | Developer tooling, cron automation | **Python** (stable, responsive maintainers) |
| **PicoClaw / NanoClaw** | **Lightweight / Embedded** | Single-user, mobile, embedded devices | **Go** (lightweight, protocol-focused) |

### 6. Community Momentum & Maturity

**Tier 1: High-Velocity / Intense Sprint Execution**
- **ZeroClaw, IronClaw, NanoBot**: These projects are iterating the fastest. They are accepting and implementing major new features (skills platform, iMessage channels, OIDC auth) in parallel with fixing bugs. They have high PR churn and a large number of open issues, but momentum is strongly positive.

**Tier 2: Active & Balancing**
- **OpenClaw, Hermes Agent, CoPaw**: These are established projects with large user bases. They are actively managing substantial regression backlogs while processing a steady stream of community contributions. The focus is on **quality improvement** over feature velocity.

**Tier 3: Low Activity / Stalled**
- **PicoClaw, NanoClaw, NullClaw, TinyClaw, LobsterAI, Moltis, ZeptoClaw**: These projects show minimal to no development activity. Two (NullClaw, TinyClaw) have critical open bugs that threaten user confidence. PicoClaw and NanoClaw have pending PRs but appear to be in a maintenance-only cycle.

### 7. Trend Signals

From the community feedback across these projects, the following industry trends are evident for AI agent developers:

1.  **The "Token Tax" is the #1 Pain Point**: The dominant concern is not latency or accuracy, but **cost and efficiency**. 73% fixed overhead on API calls is common. The ecosystem will prioritize tool-schema lazy loading, prompt caching, and efficient context management.

2.  **Self-Discovering Agents are Become a Requirement**: Users expect their agents to know their own capabilities. A single feature request ("agent doesn't know it can add cron") from ZeroClaw signals a shift from "declarative configuration" to "introspective action."

3.  **Concurrency is the New Frontier of Agent Reliability**: As agents move from single-user toys to production multi-session deployments, race conditions in runtime hooks (`NanoBot`), session takeover errors (`OpenClaw`), and stuck-session watchdog issues (`ZeroClaw`) are emerging as the primary class of hard-to-find bugs.

4.  **Security is Shifting Left, but Unevenly**: The disclosure of basic path traversal and unauthenticated file read vulnerabilities in smaller projects (TinyClaw, NanoClaw) indicates that while major projects are hardening, the ecosystem's security baseline is still low.

5.  **Rust is the New Standard for High-Performance Agents**: The most active projects with the cleanest issue trackers (IronClaw, ZeroClaw) are written in Rust. This offers a performance advantage but creates a higher barrier to entry for contributors compared to the Python-based peers (OpenClaw, Hermes Agent).

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-21

## Today's Overview

NanoBot is experiencing a **significant surge in development activity**, with 18 pull requests updated in the last 24 hours—the highest daily volume observed this quarter. Four issues remain actively open, all filed within the past 3 days, indicating a healthy flow of community-reported bugs and feature requests. The project has **no new releases** today, but the intense PR activity suggests a release candidate may be approaching. The community is especially focused on **concurrency safety**, **performance optimization**, and **new channel integrations**, reflecting both production hardening and platform expansion priorities.

## Releases

No new releases today. The last release remains the prior stable version. With numerous fix and feature PRs open or recently merged, a patch or minor release may be imminent.

## Project Progress

Four PRs were merged or closed in the last 24 hours:

- **#4426** `[CLOSED] [channel]` — **feat(channels): add iMessage channel via Photon Spectrum** (morandot). Adds an iMessage bridge using the Photon Spectrum service, following the WhatsApp sidecar pattern. This enables iMessage integration without a Mac relay, expanding NanoBot's channel ecosystem significantly.
- **#4427** `[CLOSED]` — **fix(webui): prevent iOS Safari auto-zoom on textarea focus** (axelray-dev). Fixes a mobile UX bug where focusing input fields triggered unwanted page zoom on iOS Safari, a common pain point.
- **#4303** `[CLOSED]` — **fix(mcp): close tracked generators in _close_server to prevent GC crash** (michaelxer). Resolves a runtime crash (`RuntimeError: Attempted to exit cancel scope in a different task`) when MCP server sessions reconnect.
- **#4321** `[CLOSED]` — **fix: advance dream cursor when Dream is disabled to prevent prompt bloat** (michaelxer). Fixes a bug where disabling Dream mode would cause unbounded history accumulation, inflating prompts over time.

Additionally, several high-impact PRs advanced toward acceptance (see Bugs & Stability and Feature Requests sections).

## Community Hot Topics

1. **#4408** `[OPEN]` **Nanobot.run() per-run hooks are not concurrency-safe** — 2 comments. This bug report has spawned **two competing fix PRs** (#4425 by michaelxer using `contextvars`, and #4409 by waelantar passing hooks via `process_direct`), making it the most active discussion. The underlying concern is production-grade concurrency safety for multi-session deployments.

2. **#4420** `[OPEN]` **Performance: estimate_prompt_tokens redundant tiktoken encoding** — 1 comment. User `codeLong1024` reports a real-world slowdown in their "nanobee" project, with `estimate_prompt_tokens` being called up to 3 times per agent turn. This has already triggered **two optimization PRs** (#4421 and #4428) from different contributors.

3. **#4429** `[OPEN]` **feat: Allow custom provider to configure thinking style** — 1 comment. User `gkd2323c` requests support for non-standard thinking/reasoning parameters (e.g., VolcEngine/Doubao), signaling demand for broader model compatibility.

## Bugs & Stability

| Severity | Issue | Description | Fix Available? |
|----------|-------|-------------|----------------|
| **High** | #4408 | Concurrency race condition in `Nanobot.run()` — shared `_extra_hooks` clobbered under concurrent use | ✅ PR #4425 (`contextvars` approach) and #4409 (pass-through approach), both open |
| **Medium** | #4420 | `estimate_prompt_tokens` redundant tiktoken encoding degrades agent loop performance | ✅ PR #4421 (cache tool-definition JSON) and #4428 (bounded identity cache), both open |
| **Low** | #4423 (PR) | Telegram `_is_rich_capability_error` too broad — `"chat not found"` would permanently disable rich send | ✅ PR #4423 open, narrows error matching |
| **Low** | #4321 (merged) | Dream cursor not advanced when Dream disabled → prompt bloat | ✅ Fixed in #4321 |

The **#4408 concurrency bug** is the most critical open stability issue, with two fix strategies under review.

## Feature Requests & Roadmap Signals

1. **iMessage Channel** — PR #4426 (merged) adds Photon Spectrum-backed iMessage support. Predict: **available in next release**.
2. **Custom Provider Thinking Style** — Issue #4429 requests configurable reasoning parameters for non-OpenAI providers. Likely to be implemented soon given concurrency with the custom provider system.
3. **Telegram sendRichMessage** — Issue #4422 + PR #4423 add native rendering for tables, task lists, and math blocks. Predict: **next release**.
4. **Subagent Aggregated Result Mode** — PR #4414 adds buffered subagent result collection. Under review.
5. **Memory: Archive Facts with Provenance Context** — PR #4424 improves fact deduplication and source tracking during consolidation. Under review.
6. **Cron Job Model Presets** — PR #4416 allows per-job model/context overrides for cron tasks. Fixes #4378.
7. **Python SDK Runtime Controls** — PR #4296 (large, 9 days open) expands the SDK with `RunResult` metadata, session/memory clients, and Cursor support. May require significant review.

## User Feedback Summary

- **Performance pain point**: User `codeLong1024` (Issue #4420) reports noticeable slowness in their production "nanobee" project, traced to redundant tokenization of tool definitions. The community has responded quickly with two optimization PRs.
- **Concurrency concerns**: User `waelantar` (Issue #4408) discovered a race condition affecting any multi-session or concurrent usage of `Nanobot.run()`. This reflects real production deployment needs.
- **Model compatibility gap**: User `gkd2323c` (Issue #4429) needs VolcEngine/Doubao thinking support, indicating demand for broader LLM provider support beyond OpenAI-compatible APIs.
- **Mobile UX satisfaction**: The WebUI zoom fix (PR #4427, merged) directly addresses user frustration with iOS Safari, a common complaint for mobile-accessed AI assistants.

## Backlog Watch

| Item | Days Open | Type | Reason for Attention |
|------|-----------|------|---------------------|
| **#4296** feat(sdk): expand Python SDK runtime controls | 10 days | Enhancement (Large PR) | Could introduce breaking changes; needs timely review to avoid merge conflicts with concurrent PRs |
| **#4256** fix(memory): keep history cursor monotonic | 13 days | Bug Fix | Memory store correctness issue; has no maintainer response since creation |
| **#4395** Improve onboard wizard setup flow | 3 days | Enhancement | Calms TUI workflow; may need integration testing with other CLI changes (#4329) |
| **#4329** feat(cli): add inline TUI for nanobot agent | 8 days | Enhancement | Large UI feature; overlaps with #4395 onboard wizard; potential merge conflicts |

The **#4296 SDK expansion PR** is the highest-risk backlog item due to its size, age, and potential to conflict with newer concurrency fixes (#4425, #4409) that also touch the SDK layer. **Maintainer attention is advised.**

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-21

## Today's Overview
Hermes Agent shows **high community activity** with 50 issues and 50 PRs updated in the last 24 hours, indicating an actively maintained project. The open/closed ratio (44 open issues vs 6 closed; 39 open PRs vs 11 merged/closed) suggests the maintainers are processing contributions but the bug backlog is growing faster than triage can keep up. A flurry of 8 PRs were opened today alone (June 21), spanning Kanban fixes, desktop UI, gateway resource leaks, and memory provider improvements. No new releases today. The token overhead theme continues to dominate community concern, with two of the top three most commented issues (#6839, #4379) focused on the same root problem.

## Releases
No new releases today. The last known release is **Hermes Agent v0.17.0** (referenced in Issue #49831).

## Project Progress
**11 PRs were merged or closed today**, reflecting active maintenance. Notable closed work includes:

- **Kanban system fixes**: [PR #49816](https://github.com/NousResearch/hermes-agent/pull/49816) resolved a critical CPU busy-loop in the dashboard PTY reader and Windows test compatibility (closes #49768). [PR #49853](https://github.com/NousResearch/hermes-agent/pull/49853) made profile-wrapper alias tests OS-aware. [PR #49854](https://github.com/NousResearch/hermes-agent/pull/49854) documented the `kanban_complete` artifacts parameter. [PR #49855](https://github.com/NousResearch/hermes-agent/pull/49855) fixed per-task worktree materialization — a long-standing Kanban defect where workers ran in the main repo checkout instead of isolated worktrees.

- **Worktree improvements**: [PR #37316](https://github.com/NousResearch/hermes-agent/pull/37316) and [PR #44844](https://github.com/NousResearch/hermes-agent/pull/44844) and [PR #45503](https://github.com/NousResearch/hermes-agent/pull/45503) all closed today, fixing worktree provisioning to create proper isolated git worktrees per task.

- **Bug fix**: [Issue #47868](https://github.com/NousResearch/hermes-agent/issues/47868) (leaked timestamp metadata rejected by strict providers) was closed — a significant fix for compatibility with OpenAI-compatible backends.

## Community Hot Topics

1. **[Issue #6839 — Lazy Tool Schema Loading](https://github.com/NousResearch/hermes-agent/issues/6839)** (26 comments, 13 👍)
   *Proposal to inject only needed tool schemas per conversation turn. Currently Hermes injects all ~50+ enabled tool schemas (3,500-5,000 tokens) on every API call. The author suggests a two-pass system: first pass loads minimal schemas, second pass fetches full schemas only when a tool is invoked. This would dramatically reduce token waste, especially on local models.* **Community need: Token efficiency is the #1 pain point.**

2. **[Issue #4379 — Token Overhead Analysis](https://github.com/NousResearch/hermes-agent/issues/4379)** (15 comments)
   *Quantitative analysis showing 73% of every API call (~13.9K tokens) is fixed overhead. The author built a monitoring dashboard to profile a production Telegram+WhatsApp+Cron deployment. This corroborates the anecdotal "16K tokens for 'who u?'" report in Issue #13983.* **Community need: Users demand visibility into what consumes their tokens.**

3. **[Issue #41190 — Unified Plugin Route Selector](https://github.com/NousResearch/hermes-agent/issues/41190)** (5 comments, 1 👍)
   *Fragmented routing logic for provider/model selection across config, heuristics, and failure recovery paths. A single plugin-accessible hook is needed to override provider and model for every LLM call site.* **Community need: Configuration complexity is harming user experience.**

4. **[Issue #37619 — Windows Desktop Zoom Support](https://github.com/NousResearch/hermes-agent/issues/37619)** (2 comments, 6 👍)
   *Despite low discussion, this is the most-upvoted open feature request today. Windows desktop app lacks zoom/UI scaling entirely. Ctrl+/Ctrl- don't work, and no setting exists.* **Community need: Desktop app UX parity across platforms.**

## Bugs & Stability

**Severity P1 (Critical):**
- **[Issue #48061](https://github.com/NousResearch/hermes-agent/issues/48061)** — Hermes Agent v0.16.0 sends empty runtime model/provider on Linux pipx install, causing `max_retries_exhausted` failures. No fix PR yet. This blocks all API calls, making the agent non-functional on fresh pipx installs.

**Severity P2 (High):**
- **[Issue #49852](https://github.com/NousResearch/hermes-agent/issues/49852)** — TUI `session.close` can leak an `AIAgent` that finishes building concurrently, retaining process/sandbox/browser resources until gateway restart. Fix PR [PR #49886](https://github.com/NousResearch/hermes-agent/pull/49886) opened today.
- **[Issue #49793](https://github.com/NousResearch/hermes-agent/issues/49793)** — Photon iMessage streaming cursor renders as white square/tofu in outbound messages (already has a fix in progress).
- **[Issue #47048](https://github.com/NousResearch/hermes-agent/issues/47048)** — Telegram double-renders tables: legacy MarkdownV2 version overlays the rich-message version, producing unreadable output.
- **[Issue #47867](https://github.com/NousResearch/hermes-agent/issues/47867)** — MCP `isError` responses with JSON bodies are double-encoded, hiding actionable error messages from the model.
- **[Issue #47804](https://github.com/NousResearch/hermes-agent/issues/47804)** — Feishu platform ignores `config.yaml enabled: false` when env vars are present — configuration precedence bug.
- **[Issue #49831](https://github.com/NousResearch/hermes-agent/issues/49831)** — WhatsApp bridge path resolution off-by-one breaks on editable/git source installs.
- **[Issue #42685](https://github.com/NousResearch/hermes-agent/issues/42685)** — macOS launchd gateway crashes into a permission denied loop due to root-owned `gateway.lock`.
- **[Issue #49569](https://github.com/NousResearch/hermes-agent/issues/49569)** — WhatsApp Docker bridge completely blocked by EACCES npm install + wrong log path.
- **[Issue #49765](https://github.com/NousResearch/hermes-agent/issues/49765)** — Desktop app profile selector doesn't actually switch profiles — sessions always start under `default`.
- **[Issue #47077](https://github.com/NousResearch/hermes-agent/issues/47077)** — `/model` picker for opencode-go shows only 13 of 19 available models, hiding 6 models including MiniMax and GLM.

**Severity P3 (Medium):**
- **[Issue #47826](https://github.com/NousResearchhermes-agent/issues/47826)** — Desktop app crashes with `TypeError: Object has been destroyed` from zombie timer in title resolution.
- **[Issue #47822](https://github.com/NousResearch/hermes-agent/issues/47822)** — macOS install fails when `HERMES_HOME` path contains spaces (e.g., `/Volumes/Envoy APFS/...`).
- **[Issue #47865](https://github.com/NousResearch/hermes-agent/issues/47865)** — `hermes update` fails noisily on non-admin macOS accounts when cua-driver can't write to `/Applications`.
- **[Issue #49867](https://github.com/NousResearch/hermes-agent/issues/49867)** — Windows Desktop app takes excessively long to start.

**Regression Note:** The P2 WhatsApp Docker bridge bug (#49569) is a new deployment blocker, but [PR #49890](https://github.com/NousResearch/hermes-agent/pull/49890) fixes the `hermes doctor` audit path for WhatsApp in Docker (follow-up to #49561).

## Feature Requests & Roadmap Signals

**High-probability next-version features:**
1. **Tool schema lazy loading** (#6839) — The overwhelming community demand. With 26 comments and 13 upvotes, and two separate issues (#6839 and #4379) quantifying the same problem, this is likely the top roadmap priority.
2. **Unified plugin route selector** (#41190) — Fragmented routing is a documented pain point for multi-provider deployments.
3. **Multi-directory HERMES_WRITE_SAFE_ROOT** — [PR #49557](https://github.com/NousResearch/hermes-agent/pull/49557) already implements this with `:`-separated paths. Likely to land soon.
4. **Desktop zoom/scaling** (#37619) — Highest upvoted open feature, but no PR yet.

**Other signals:**
- WhatsApp Cloud API message template support (#45935) — Requested by a production user running an engine-machining business. Real business use case behind the feature request.
- Rich `/context` and `/usage` slash commands (#10617) — To surface prompt composition and token efficiency breakdown per-model.
- Per-task routing for `delegate_task` ([PR #31537](https://github.com/NousResearch/hermes-agent/pull/31537)) — Still open, would allow model/provider override per delegated subtask.
- Unified numeric approval shortcuts across all platforms ([PR #49881](https://github.com/NousResearch/hermes-agent/pull/49881)) — 1=/approve, 2=/approve session, etc.

## User Feedback Summary

**Positive signals:** Users express love for the project ("I really love Hermes Agent and use it everywhere ❤️" — #49867). The Kanban and worker systems are being actively used in production, evidenced by multiple worktree fixes and documentation improvements.

**Pain points (ranked by frequency):**
1. **Token overhead** — Dominant theme. "16K+ tokens per 'who u?' prompt" (#13983), "73% fixed overhead" (#4379). Users are actively building monitoring dashboards to understand consumption.
2. **Configuration complexity** — Multiple issues about profile/providers/models not working as expected, env vars overriding config, symlinks breaking installs.
3. **Desktop app stability** — Windows startup slow, macOS electron crashes, zoom missing, profile selector broken.
4. **Docker deployment friction** — WhatsApp bridge broken in Docker (#49569), root-owned files (#17144).
5. **Cross-platform inconsistencies** — macOS vs Linux install paths, space-in-path bugs on both platforms.

**Use cases reflected:**
- Production multi-platform deployments (Telegram + WhatsApp + Cron)
- Business operations (engine-machining business via WhatsApp)
- Enterprise/strict environments (OpenAI-compatible provider compatibility)
- Local model users (more sensitive to token waste)

## Backlog Watch

**Issues needing maintainer attention:**
1. **[Issue #13983 — 16K Token Bloat](https://github.com/NousResearch/hermes-agent/issues/13983)** — Created April 22, 2026. Two months old, only 4 comments. A simple "who u?" consuming 16K tokens is the most visceral example of the token overhead problem. This should be a high-priority triage item.
2. **[Issue #17144 — Docker Root-Owned Files](https://github.com/NousResearch/hermes-agent/issues/17144)** — Created April 28, 2026. Docker deployment blocker where tool/memory writes create root-owned files. Only 3 comments, no fix PR. With Docker being a primary distribution method, this affects a significant user base.
3. **[Issue #32528 — QQ Bot C2C Button Approval Rejection](https://github.com/NousResearch/hermes-agent/issues/32528)** — Created May 26, 2026. QQ Bot private chat button approvals always rejected due to `chat_type` mismatch. No fix PR. This makes the QQ platform integration partially non-functional.
4. **[Issue #39308 — Windows Installer 8.3 Short Name Failure](https://github.com/NousResearch/hermes-agent/issues/39308)** — Closed today but resolved via workaround investigation only. The underlying issue (spaces in usernames breaking Electron install) affects many Windows users and may resurface.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-21

## Today's Overview
PicoClaw shows **moderate community activity** with 1 new nightly release, 2 open issues, and 1 open pull request updated in the last 24 hours. No issues or PRs were closed or merged today, indicating a maintenance-focused period rather than active feature integration. The project continues to evolve with a v0.3.0 nightly pipeline active, though the stale labels on both items suggest a need for more maintainer engagement on long-standing concerns. The community remains active in discussion, with 7 total comments across the tracked items.

## Releases
**New: Nightly Build `v0.3.0-nightly.20260621.287853ab`**
- **Status:** Automated build, may be unstable
- **Full Changelog:** [v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)
- **Breaking Changes:** None specified in release notes
- **Migration Notes:** No migration instructions provided; users on stable v0.2.9 should exercise caution before using nightly builds in production

## Project Progress
**No PRs merged or closed today.** The sole open PR (#2964) remains in review since May 28, showing no forward movement.

## Community Hot Topics

**Most Discussed Issue:**
- [#3012 – Continuous token consumption with Evolution enabled](https://github.com/sipeed/picoclaw/issues/3012) (4 comments)
  - **Underlying Need:** Users running PicoClaw with Evolution mode (Draft/Code Path) report unexpected ongoing API token usage every minute, even without active interactions. This points to a runtime loop bug where the agent’s self-triggering mechanism or background polling does not respect idle states. The user is running v0.2.9 on FreeBSD with MiniMax provider.

**Most Highly Voted Issue:**
- [#2984 – Add explicit turn completion signal for WebSocket clients](https://github.com/sipeed/picoclaw/issues/2984) (2 👍, 3 comments)
  - **Underlying Need:** External protocol implementers lack a deterministic signal to know when the agent finishes processing a message. Current events (`message.create`, `typing.stop`) are ambiguous. This reflects a design gap in the Pico WebSocket protocol for client integration, suggesting the community wants clearer lifecycle events for building reliable integrations.

## Bugs & Stability

**High Severity:**
- **[#3012] Continuous token consumption every minute (Evolution enabled)** — Open since June 5
  - **Impact:** Direct financial cost via API token waste; potential infinite loop
  - **Status:** No fix PR exists; community discussion ongoing
  - **Environment:** v0.2.9, Go 1.25.10, MiniMax provider, FreeBSD, Web channels

**No new bugs reported in the last 24 hours.** The token consumption bug is the only active stability concern.

## Feature Requests & Roadmap Signals

**Current Feature PR (Long-standing):**
- [#2964 – Configurable image input compression for vision pipeline](https://github.com/sipeed/picoclaw/pull/2964) (Open since May 28)
  - **Prediction:** Likely candidate for v0.3.0 stable if merged. Addresses user need for multi-level compression policies beyond `max_media_size` constraint.

**Requested Protocol Feature:**
- [#2984 – Turn completion signal](https://github.com/sipeed/picoclaw/issues/2984)
  - **Prediction:** Likely to be implemented as a protocol extension in a future minor release, possibly v0.3.1 or v0.4.0, given the high community interest (2 👍).

## User Feedback Summary
- **Pain Points:**
  - Token waste in Evolution mode (#3012) — users on free/minimax plans are experiencing unbilled/over-limit costs
  - Integration difficulty for WebSocket clients (#2984) — lack of explicit turn completion makes building reliable frontends harder
- **Use Cases:** Users are integrating PicoClaw as a real-time agentic assistant (Web channels) and building third-party WebSocket clients on top of the Pico Protocol
- **Satisfaction:** No explicit praise or complaints beyond these two issues; moderate but engaged community

## Backlog Watch

**Stale Items Requiring Maintainer Attention:**

1. **PR #2964 – Image input compression** (Open 24 days, last updated 1 day ago)
   - **Action Needed:** Review and merge or provide feedback; stale label not yet applied but inactivity is concerning
   
2. **Issue #2984 – Turn completion signal** (Open 19 days, last updated 1 day ago)
   - **Action Needed:** Official response on protocol roadmap; highest community demand (2 👍)

Both items have seen recent activity but remain unresolved. The project maintainers should prioritize reviewing #2964 and providing a timeline or acceptance of the protocol change in #2984 to maintain community momentum. The token consumption bug (#3012) also warrants a prompt fix or workaround guide.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-21

## Today's Overview
NanoClaw shows **moderate activity** today with 1 open issue and 6 open pull requests updated in the last 24 hours, but no new releases or merges occurred. The project is in a **fix-and-documentation cycle**, with all 6 PRs still open and awaiting review or merge. The single active issue (#2768) highlights a meaningful performance concern around prompt caching in the Claude provider. The absence of any merged PRs or closed issues suggests the maintainer team may be bottlenecked on review capacity, though the volume of well-structured contributions is positive.

## Releases
No new releases were published today. The latest release remains unchanged; no upgrade notes or migration guidance is needed at this time.

## Project Progress
**No pull requests were merged or closed today.** All 6 open PRs remain under review. Notable open contributions include:
- **#2824** (CutSnake01) — Fix: drop stale "Global Memory" instruction from main seed prompt
- **#2823** (CutSnake01) — Fix: remove groups/global/CLAUDE.md (host deletes it on every startup)
- **#2822** (CutSnake01) — Refactor: drop dead `/workspace/global` mount from container-runner
- **#2821** (chandrameenamohan) — Docs: document assistant-name environment variables
- **#2799** (sturdy4days) — Security fix: confine `send_file` reads to `/workspace` (CVE-2026-29611)
- **#2801** (sturdy4days) — Fix: guard `safeParseContent` against non-object JSON

These contributions span **code cleanup, security hardening, and documentation improvements**, indicating healthy community engagement in maintenance and hardening.

## Community Hot Topics
**#2768** [OPEN] — *Enable prompt caching by default in Claude provider*  
- 1 comment, 0 reactions | Author: galmorduku  
- URL: https://github.com/nanocoai/nanoclaw/issues/2768  
- **Analysis:** This issue identifies that `sdkQuery()` in the Claude provider does not enable prompt caching, causing the full system prompt to be resent on every turn. For agents with large prompts (e.g., rich system instructions, tool definitions), this creates unnecessary latency and cost. The underlying need is **performance optimization for production agent deployments** — users want cheaper, faster agent turns without code changes. This is a low-effort, high-impact change that could be a quick win.

No issues or PRs today show heavy comment or reaction volume; the project remains low-signal but focused.

## Bugs & Stability
**No new bugs or crashes were reported today.** The open issue #2768 is a performance enhancement request, not a stability bug. However, two security-related PRs are pending:
- **#2799** (CVE-2026-29611) — Path traversal vulnerability in `send_file`: a compromised agent could read arbitrary container-visible files. **High severity.** Fix PR exists but is unmerged.
- **#2801** — `safeParseContent` returns `undefined` for primitive JSON payloads instead of a fallback. **Medium severity.** May cause silent failures in agent communication.

**Recommendation:** Review and merge #2799 as a priority given the explicit CVE assignment and security implications.

## Feature Requests & Roadmap Signals
The only feature-adjacent signal today is **#2768** (prompt caching by default in Claude provider). This is a low-risk optimization that aligns with Anthropic's SDK defaults. We predict this will be implemented in the **next patch release (v0.x.x)** given its simplicity and community support.

No other explicit feature requests were submitted today. The project appears focused on **hardening and cleanup** rather than new capability introduction.

## User Feedback Summary
No direct user feedback (comments, support requests) was captured today beyond the prompt caching issue. The open PRs suggest contributors are proactively addressing:
- **Developer experience pain point:** Stale "Global Memory" instructions in seed prompts (#2824)
- **Operational friction:** CLAUDE.md being deleted on startup (#2823)
- **Security concern:** File read boundary enforcement (#2799)
- **Reliability issue:** JSON parsing edge cases in agent content (#2801)

These indicate users and contributors are experiencing subtle but recurring issues in production-like usage, particularly around prompt correctness, container lifecycle, and input validation.

## Backlog Watch
**No items currently require urgent maintainer attention beyond the 6 open PRs.** All open PRs are under 4 days old, so no items are critically stale. However, **#2799** (security CVE fix) and **#2801** (JSON parsing guard) have been open since June 17 — 4 days without merge — which is notable given their stability/security nature. Maintainers should prioritize reviewing these to reduce project risk.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 21, 2026.

---

## NullClaw Project Digest – 2026-06-21

### 1. Today's Overview
The project currently shows very low activity, with no new releases or pull requests in the last 24 hours. A single open bug issue was created today, indicating that while the community is actively using the software, development velocity appears stalled. The zero PR activity suggests maintainers are either focused on internal work or the project is in a low-maintenance phase. The sole open issue reports a critical reliability problem, which represents the most significant signal for project health today.

### 2. Releases
No new releases were published today. The latest available release remains **v2026.5.29**.

### 3. Project Progress
No pull requests were merged or closed today. There is no evidence of active feature development or bug fixes landing in the repository within the reporting period.

### 4. Community Hot Topics
The only active item is a single bug report:

- **[BUG] error: NoResponseContent** (Issue [#967](https://github.com/nullclaw/nullclaw/issues/967))
  - *Author:* svier0
  - *Summary:* The agent frequently fails with `error: NoResponseContent` on Windows 11 (v2026.5.29) when using the **Agnes-2.0-Flash** model. The error occurs in over 50% of conversations (12 out of 21 attempts), with a 27-second response time before failure. The user notes the same model and API key works fine in picocla (likely another client), suggesting a NullClaw-specific integration issue.
  - *Analysis:* This issue highlights a core reliability problem with the agent’s HTTP/streaming response handling. The user is experiencing a near 50% failure rate, which severely undermines trust in the application. The lack of comments or reactions suggests the community has not yet validated the bug, but the detailed reproduction steps indicate a genuine protocol-level issue.

### 5. Bugs & Stability
**High Severity**
- **NoResponseContent on Windows 11** (Issue [#967](https://github.com/nullclaw/nullclaw/issues/967)): A critical reliability bug causing the agent to fail silently in over 50% of interactions. The model (Agnes-2.0-Flash) works in other clients, pointing to a potential issue with NullClaw’s response parsing or timeout handling. No associated fix PR exists yet. **Impact:** High – makes the agent unusable for frequent use.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were opened today. The only signal from the community is a demand for **basic stability and error handling** rather than new features. The repeated failure with a specific model suggests that robust error recovery and retry logic (or a fix for empty response handling) will be a priority in the next patch release.

### 7. User Feedback Summary
The sole user report today (Issue [#967](https://github.com/nullclaw/nullclaw/issues/967)) expresses clear **dissatisfaction** with reliability. The user carefully compared behavior across clients (NullClaw vs. picocla), indicating a technically competent user who expects the tool to work. The sentiment is one of frustration: the software fails more often than it succeeds for this model. There is no positive feedback in this window.

### 8. Backlog Watch
No long-unanswered issues or PRs were identified in today’s data. However, the active bug (Issue [#967](https://github.com/nullclaw/nullclaw/issues/967)) is now 1 day old with zero maintainer response. If this remains unanswered for another 48 hours, it will become a backlog item that could erode community confidence. The maintainer should prioritize a response or reproduction attempt.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-21

## 1. Today's Overview

IronClaw is experiencing a period of extremely high development velocity, with **21 PRs updated in the last 24 hours** — a marked spike in activity. Nine PRs were merged or closed today, predominantly authored by core contributors. The project is consolidating several major architectural initiatives simultaneously: a manifest-driven channel ingress system, concurrent turn execution for the Reborn runtime, and Google OAuth token lifecycle management. Despite this surge in code motion, only **one open issue** exists in the tracker (a nightly E2E failure from nearly a month ago), indicating strong issue hygiene. No new releases were tagged today, but the volume of merged work suggests a significant release may be imminent.

## 2. Releases

**None.** No new releases were published in the last 24 hours.

## 3. Project Progress

Nine PRs were closed or merged today, spanning several focus areas:

### Manifest-Driven Channel Ingress (Consolidation)
- **#5107** (OPEN, XL, serrrfirat) — The unifying PR that folds four prior stacked proposals into a single, self-contained integration. Makes channel/extension ingress, auth, transport, secrets, and connect onboarding manifest-defined rather than provider-specific Rust code. Likely the capstone of a multi-PR stack.
- **#5103** (CLOSED, XL, serrrfirat) — Core ingress policy + typed auth + transport discriminator as manifest data. The keystone of the manifest-driven-channels work.
- **#5104** (CLOSED, L, serrrfirat) — Move 2: fail-close auth verifier + transport discriminator, net −54 lines.
- **#5102** (CLOSED, L, serrrfirat) — Move 3: cross-contract credential coherence invariant for v2 extension-manifest projection.
- **#5106** (CLOSED, XL, serrrfirat) — Move 4: collapses per-channel host-ingress mount sprawl into a single generic plan in `serve.rs`.

### Test & CI Infrastructure
- **#4829** (CLOSED, L, serrrfirat) — Retired the dormant `reborn-integration` workflow, added Reborn suites to nightly deep CI.
- **#5105** (CLOSED, S, serrrfirat) — Fixed three stale provider/OAuth guard tests that were failing on `main` due to pre-change assertions.
- **#5086** (CLOSED, XL, serrrfirat) — Experimental full-suite CI gate using nextest archive + mold linker + sccache + sharding. Contains real performance measurement data.

### Slack Connectivity
- **#4777** (CLOSED, XL, serrrfirat) — Fixes Slack reconnect loop in Use Case 3 by making WebUI/channel state reflect existing Slack delivery connections.

### Workspace Entities
- **#2548** (CLOSED, XL, standardtoaster) — Long-running workspace entities PR (originally #1734) with DB-backed workspaces, membership, cross-workspace sharing. Includes `DB MIGRATION` tag. This was rebased and completed onto current staging.

## 4. Community Hot Topics

All current open PRs have zero comments, suggesting discussion occurs synchronously or outside the GitHub issue tracker. The only issue with any engagement is:

- **#4108 — Nightly E2E Failed** (OPEN, 0 comments, 0 reactions) — A bot-reported nightly CI failure from 2026-05-27 that remains open. The lack of any human discussion or reaction may indicate that the team either accepts this as a known intermittent failure or has resolved it elsewhere without updating the tracker.

**Analysis:** The community engagement metric is effectively zero across Issues and PRs. This is unusual for an actively developed project with 21 daily PRs. It may indicate: (a) team communication via Slack/Discord, (b) a tight core team that doesn't solicit public discussion, or (c) automated tooling that does not capture reactions.

## 5. Bugs & Stability

### Active Bug Reports
- **#4108 — Nightly E2E Failed** (Severity: Medium-High) — The only open issue. A bot-reported nightly E2E workflow failure on `full E2E / E2E (features)`. Created 2026-05-27, last updated 2026-06-20. **No fix PR identified.** The 25-day gap without closure is concerning for CI reliability.

### Fixed Bugs (Merged Today)
- **#5105 — Stale provider/OAuth guard tests** (Severity: Medium) — Three security-relevant guard tests were failing on `main` but went undetected because the crates were outside the reborn CI closure. Confirmed as stale test assertions, not guard regressions.
- **#5108 — Reborn dependency-closure tail failures** (OPEN, serrrfirat) — Automated agent-authored fix for three remaining CI closure failures, including a real security-relevant over-exposure bug in GitHub manifest visibility.
- **#4777 — Slack reconnect loop** (Severity: Medium) — Users experiencing infinite reconnect loops in Slack delivery channel. Fixed by making WebUI reflect actual connection state.

### Regression Risk
- **#5081 — Hosted single-tenant Postgres profile** (OPEN, XL, DB MIGRATION) — Adding a new DB profile carries risk of schema migration conflicts or unintended data path changes.

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release

The following merged/advanced features form a coherent "Manifest-Driven Channels + Reborn Runtime" release:

1. **Manifest-driven channel ingress** (#5107) — Makes all channel configuration manifest-defined. This is a foundational architecture change that affects every channel provider.
2. **Concurrent turn execution** (#5085) — `TurnRunScheduler` with per-user/per-type caps lifts the Reborn runtime from strictly serial turn execution to concurrent. A major LLM inference throughput improvement.
3. **One-shot scheduled triggers** (#5065) — Adds `TriggerSchedule::Once { at }` alongside recurring cron. Enables single-use future triggers.
4. **Google OAuth proactive refresh** (#5087) — Automatic token refresh before expiry, preventing manual reconnect.
5. **Workspace entities with sharing** (#2548) — DB-backed workspaces, cross-workspace sharing, scoped access. This is a significant enterprise feature.
6. **Postgres hosted single-tenant profile** (#5081) — A new deployment profile for hosted previews.

### Earlier-Stage Signals
- **Reborn Learning System (WS-1)** (#4937) — Memory learning semantics with A/B gate. Still open, suggesting it's a multi-sprint effort. This is Hermes-parity for "learn from mistakes, never repeat."
- **CI full-suite gate** (#5086) — Experimental workflows using nextest archive + mold + sccache. If adopted, this would dramatically change the CI experience.

## 7. User Feedback Summary

**No direct user feedback is captured in the GitHub issues or PRs** for today's window. However, user pain points can be inferred from the PRs that address them:

- **Pain: Slack reconnection issues** — Addressed by #4777, which fixed an infinite reconnect loop. Users were experiencing a broken Slack delivery experience that always showed "disconnected."
- **Pain: Google OAuth token expiry** — Addressed by #5087. Users were being forced to manually reconnect Google credentials every hour.
- **Pain: Slow turn execution** — Addressed by #5085. Users running LLM inference in the Reborn runtime were experiencing serial execution bottlenecks.

## 8. Backlog Watch

| Issue/PR | Author | Age | Status | Concern |
|----------|--------|------|--------|---------|
| **#4108 — Nightly E2E Failed** | github-actions[bot] | 25 days | OPEN, 0 comments | Long-unresolved CI failure with no human triage visible. The E2E pipeline is a critical quality gate. |
| **#4002 — CI dependency bumps** | dependabot[bot] | 28 days | OPEN, 0 comments | 16 GitHub Actions dependency updates pending. Dependabot PRs are typically auto-merged; the 28-day latency suggests manual review is blocked or deferred. |
| **#4765 — Subagent inline prompt body budget** | serrrfirat | 10 days | OPEN, 0 comments | Fix for subagent goals constrained by 512-byte budget. This blocks subagent functionality for complex prompts. |

**Notable:** The absence of any older (>30 day) unresolved issues is a strong positive signal for project health. The three items above represent the entire backlog requiring attention.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-21

## Today's Overview

The project shows a quiet day with no new pull requests or releases, and all five recently updated issues have been closed as stale. This indicates that the maintainer team is actively cleaning up old, unaddressed bug reports rather than introducing new features or fixes. The closed issues (all from early April) were updated in the last 24h but without new comments, suggesting they may have been auto-closed or batch-closed due to inactivity. Overall, project velocity is low, and the community appears to be in a passive state with no visible development activity in the past day.

## Releases

No new releases were published today. The last release remains unknown from this data snapshot.

## Project Progress

No pull requests were updated, merged, or closed today. There is no visible evidence of ongoing feature work, bug fixes, or code changes being integrated into the codebase.

## Community Hot Topics

The most active issues today are all stale-closed bugs from early April, each with 2-3 comments and zero reactions except for one. Key topics:

- **#1495 — “无缘无故中断进程” (Unexpected process termination)** — [Link](https://github.com/netease-youdao/LobsterAI/issues/1495) — 2 comments, 1 👍. The reporter describes receiving unexplained interruption messages and questions whether the issue stems from the client or the large language model. This reflects user frustration with reliability.
- **#1496 — “任务显示完成，但是没有返回” (Task shows completed but no result returned)** — [Link](https://github.com/netease-youdao/LobsterAI/issues/1496) — 3 comments, 0 👍. A user reports that a submitted task appears as "complete" but yields no output. This indicates a possible logic bug in task pipeline or result propagation.
- **#1468, #1469, #1470 — Silent data loss on modal/panel close** — All three issues ([#1468](https://github.com/netease-youdao/LobsterAI/issues/1468), [#1469](https://github.com/netease-youdao/LobsterAI/issues/1469), [#1470](https://github.com/netease-youdao/LobsterAI/issues/1470)) report the same UX bug: users lose unsaved changes when closing Agent creation, Agent settings, or MCP server configuration dialogs without confirmation. These issues all have 2 comments each. The community clearly expects a "dirty form" confirmation prompt, a standard UX pattern.

**Underlying need:** Users are demanding better data persistence and confirmation mechanisms across multiple modal interfaces. This signals a desire for a more polished, professional-grade UI.

## Bugs & Stability

All reported bugs today are stale-closed, meaning they were **not fixed** but rather closed without resolution. Prioritized by severity:

| Severity | Issue | Summary |
|----------|-------|---------|
| High | #1495 | Process interruption without clear cause — impacts core usage reliability |
| High | #1496 | Task completion without returning results — breaks core AI task execution |
| Medium | #1468, #1469, #1470 | Silent data loss in modals — poor UX but not data integrity loss (only unsaved edits) |

**No fix PRs exist** for any of these bugs. The community will need new issues or maintainer intervention to address them.

## Feature Requests & Roadmap Signals

No explicit feature requests were submitted today. However, the pattern of issues (especially #1468–#1470) strongly implies a user desire for **unsaved-changes confirmation dialogs** across the entire application, specifically in modal-based configuration interfaces. Given that three separate issues were filed for the same UX pattern, it is likely that the maintainers will prioritize a "dirty form" guard (or perhaps a global `beforeunload` / modal close guard) in the next version.

## User Feedback Summary

User sentiment is mixed, with pain points centered on:

- **Reliability:** The process interruption (#1495) and missing task output (#1496) erode trust in the AI agent's ability to complete tasks consistently.
- **UX polish:** Silent data loss is a recurring frustration; users expect the application to protect their inputs, especially when configuring system prompts and environment variables (e.g., API keys).
- **Accountability:** Users are unsure whether bugs originate from the client or the underlying LLM (#1495), indicating a need for better error reporting and diagnostic information.
- **Satisfaction:** No positive feedback or praise was recorded. The overall tone is that of bug reporting and troubleshooting.

## Backlog Watch

All five stale-closed issues represent **long-unanswered bugs** that were ignored for over two months (created April 4–7, updated June 20 but only to close). No maintainer responses are visible in the summaries. These are critical to revisit:

- **#1495**: Process termination — no solution, no comment from maintainers.
- **#1496**: Missing task output — no solution, no comment from maintainers.
- **#1468–#1470**: UX data loss — no solution, no comment from maintainers.

These issues should be reopened, triaged, and assigned if the project intends to maintain user trust. Their closure without resolution is a concerning sign for project health.

---

*Digest generated from GitHub data snapshot of `netease-youdao/LobsterAI` on 2026-06-21.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

Here is the TinyClaw project digest for **2026-06-21**.

---

## TinyClaw Project Digest: 2026-06-21

### 1. Today's Overview
The project is currently in a **low-activity state** with zero new releases or merged pull requests in the last 24 hours. The primary focus is a single, high-severity security issue that was filed yesterday and remains open. While the lack of movement on pull requests suggests a pause in feature development, the swift reporting of a critical vulnerability indicates active community vigilance. Maintainer attention is urgently required to triage the reported security flaw.

### 2. Releases
**No new releases today.** The latest available version remains v0.0.20.

### 3. Project Progress
- **Merged/Closed PRs:** 0
- **Features Advanced:** None today. No code changes were merged.

### 4. Community Hot Topics
- **#285 (Open) [Security] Unauthenticated `prompt_file` update allows arbitrary local file read**
    - **Comments/Reactions:** Low activity (0 comments, 0 👍).
    - **Analysis:** This is the only active item today. Although engagement is low, this issue represents the most critical topic in the project. It details a vulnerability in the HTTP management API that could allow attackers to read arbitrary local files by manipulating the `prompt_file` parameter. This touches on core security concerns regarding the agent configuration endpoint.
    - **Link:** [Issue #285](https://github.com/TinyAGI/tinyagi/issues/285)

### 5. Bugs & Stability
| Severity | Issue ID | Description | Status | Fix PR? |
| :--- | :--- | :--- | :--- | :--- |
| **Critical** | #285 | **Unauthenticated `prompt_file` update** – allows arbitrary local file read into provider-bound prompts. | Open | None yet |

**Analysis:** This is a high-impact bug affecting all versions <= 0.0.20. It requires immediate maintainer review to prevent potential data exfiltration. No fix PRs are currently associated with this issue.

### 6. Feature Requests & Roadmap Signals
- **Implicit Requests:** The reporting of Issue #285 strongly signals an unspoken demand for **input validation** and **authentication hardening** on the management API. Users are interacting with the API in ways that expose a lack of path sanitization.
- **Prediction:** The next version (v0.0.21) is highly likely to include a security patch that restricts which paths can be set via the `prompt_file` parameter or adds authentication to that specific endpoint.

### 7. User Feedback Summary
- **Pain Points:** The primary user pain point evident today is **security uncertainty**. The disclosure of an unauthenticated file read vulnerability suggests users are concerned about the safety of running TinyAgents with their local filesystem exposed.
- **Use Case:** The report itself originates from a **security researcher** (YLChen-007) stress-testing the project's attack surface.
- **Satisfaction:** There is no positive feedback or new feature requests in the current window, indicating that the community is currently in a "watch and wait" mode regarding the security response.

### 8. Backlog Watch
- **#285 (Critical Security Issue):** With no comments or maintainer response since creation (2026-06-20), this is the top priority item needing attention. A request for reproduction steps or a confirmation of the vulnerability is needed from the maintainer to prevent project stagnation.
    - **Link:** [Issue #285](https://github.com/TinyAGI/tinyagi/issues/285)

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for June 21, 2026.

---

## Moltis Project Digest – 2026-06-21

### 1. Today's Overview
The Moltis project experienced very low development activity in the last 24 hours. No new issues were created, no releases were published, and no feature-related pull requests were merged. The only activity consisted of two automated dependency update PRs by Dependabot, one of which has already been merged. While the project remains stable, this indicates a quiet maintenance period with no active community bug reports or feature discussions.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
No substantive features or bug fixes were merged today. The only merged pull request was an automated dependency update:

- **PR #1133 (Closed/Merged):** chore(deps): bump astro from 6.3.3 to 6.4.8 in /docs. This updates a documentation framework dependency with no changes to core project functionality.

### 4. Community Hot Topics
There were no active community discussions or high-engagement issues/PRs in the last 24 hours. The only open PR (#1134) is a Dependabot maintenance update with zero comments or reactions. The community appears dormant on this date.

### 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project maintains a clean bug slate for today.

### 6. Feature Requests & Roadmap Signals
No new feature requests were submitted. No roadmap signals or user suggestions were detected in the tracked activity.

### 7. User Feedback Summary
No explicit user feedback, pain points, or satisfaction indicators were recorded in the last 24 hours. The lack of issue creation suggests either high user satisfaction or low usage frequency on this date.

### 8. Backlog Watch
No issues or PRs are flagged as requiring maintainer attention. The only open item is a standard Dependabot PR (#1134) bumping dependencies across two directories, which is routine and non-blocking.

---

**Project Health Verdict:** *Maintenance mode.* Moltis is stable but idle, with no community engagement or development progress beyond routine dependency updates. Maintainers have no outstanding action items from the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw** (github.com/agentscope-ai/CoPaw) based on data from **2026-06-21**.

---

## CoPaw Project Digest — 2026-06-21

### 1. Today's Overview
Activity remains **high and stable**, with 7 issues and 9 PRs updated in the last 24 hours. The project shows a healthy **4:3 open-to-closed ratio** on issues and a strong **8 open PRs** indicating active development. No new releases were cut today, but the pipeline is dense with feature work, critical bug fixes, and infrastructure improvements. Community engagement is solid, with first-time contributors driving 5 of the 9 active PRs.

### 2. Releases
**None.** No new versions were published in the last 24 hours.

### 3. Project Progress
The following **PRs were merged or closed** today:
- **PR #5128 (CLOSED, Merged)** – [Group Langfuse observations by agent loop](https://github.com/agentscope-ai/CoPaw/pull/5128) *(first-time-contributor, totoyang)*: Improves observability by grouping one full agent ReAct loop into a single Langfuse trace, solving the problem of disconnected traces per LLM call.

**Key open PRs advancing the project:**
- **PR #5349** – [Migrate memory runtime to ReMe4](https://github.com/agentscope-ai/CoPaw/pull/5349) (WIP): Upgrades the legacy memory stack to ReMe4 while preserving backward compatibility.
- **PR #5348** – [Freeze session date for KV cache](https://github.com/agentscope-ai/CoPaw/pull/5348) *(first-time-contributor)*: Prevents cache invalidation at midnight by freezing the system prompt date per session.
- **PR #5347** – [Drop invalid cron jobs on startup](https://github.com/agentscope-ai/CoPaw/pull/5347): Adds startup validation to clean malformed `jobs.json` entries before loading.
- **PR #5321** – [Scroll context manager](https://github.com/agentscope-ai/CoPaw/pull/5321) *(first-time-contributor, Under Review)*: Adds a retrieval-driven alternative to native context compression with durable history and recall REPL.

### 4. Community Hot Topics
- **Issue #5329** *(4 comments)* – [Feature: Add agent-switch button in collapsed sidebar](https://github.com/agentscope-ai/CoPaw/issues/5329) (OPEN): User requests a mobile-accessible agent switch when the left sidebar is in "intro mode." An active discussion about mobile browser UX.

- **Issue #5208** *(6 comments)* – [Bug: Assistant message count mismatch with `reasoning` block type](https://github.com/agentscope-ai/CoPaw/issues/5208) (CLOSED): Community reported that models returning `"reasoning"` block type (vs. `"thinking"`) cause warnings and skipped content injection. Closed after resolution.

**Underlying needs**: Users are pushing for better **mobile UX** (sidebar, agent switching) and demanding **compatibility with non-standard OpenAI API providers** that use differing response schemas (e.g., reasoning block types).

### 5. Bugs & Stability
**High Severity:**
- **Issue #5344** – [`/api/console/chat` drops messages silently when agent is busy](https://github.com/agentscope-ai/CoPaw/issues/5344) (OPEN): HTTP 200 returned but messages are discarded. A **data-loss** bug. A duplicate closed issue (#5343) suggests a fix PR may be incoming.
- **Issue #5345** – [Custom OpenAI providers (OMLX) don't support function calling](https://github.com/agentscope-ai/CoPaw/issues/5345) (OPEN): Model returns text only, no tool calls. Blocks third-party integration.

**Medium Severity:**
- **Issue #5250** – [Cron tasks interrupt main chat](https://github.com/agentscope-ai/CoPaw/issues/5250) (CLOSED): Scheduled task descriptions injected into active chat, confusing the agent.
- **Issue #5342** – [Hard cap on tool result size needed](https://github.com/agentscope-ai/CoPaw/issues/5342) (OPEN): Context explosion when LLM calls fail (502 errors) — pruning hook is skipped.

**Fix PRs exist for:**
- **PR #5341** – Fixes file tools escaping the agent workspace (path traversal).
- **PR #5339** – Fixes Zhipu AI provider connection test failures (array vs string content).
- **PR #5340** – Fixes empty message handling when user interrupts generation (stop button).

### 6. Feature Requests & Roadmap Signals
**User-requested features:**
- **Agent-switch button in collapsed sidebar** (Issue #5329) — likely slated for next minor release given traction.
- **Custom provider full function-calling support** (Issue #5345) — a blocker for adoption with non-Ollama local models.
- **Mobile-friendly UI improvements** (Issue #5329 continuation) — chat history and new-chat buttons need repositioning.

**Roadmap indicators from PRs:**
- **Memory migration to ReMe4** (PR #5349) — indicates a strategic memory stack upgrade.
- **Scroll context manager** (PR #5321) — suggests a move toward retrieval-augmented context management as a first-class strategy.
- **KV cache optimizations** (PR #5348) — performance engineering for long-running sessions.

### 7. User Feedback Summary
- **Pain points**: Mobile browser users cannot navigate or switch agents; chat history buttons get cut off on small screens. Custom API providers (e.g., OMLX) fail to invoke tools, forcing users back to supported platforms. Silent message drops when agents are busy erode trust in the API.
- **Satisfaction**: High developer engagement — 5 first-time contributors submitted PRs this cycle alone. Quick turnaround on cron task interruption (Issue #5250) and reasoning block mismatch (Issue #5208) shows responsive maintainers.
- **Use cases**: Mobile backend access, cron-driven automation, local model testing via custom providers, and observability with Langfuse.

### 8. Backlog Watch
- **PR #5349** (Memory → ReMe4) – WIP since 2026-06-20 with no maintainer comments yet. Requires review to avoid blocking downstream memory-dependent features.
- **Issue #5345** (Custom provider function calling) – 1 comment, no maintainer response yet. Could stall third-party integrations.
- **PR #5321** (Scroll context manager, *Under Review*) – Updated 2 days ago, still awaiting final approval. This is a substantial feature addition.

No critical long-unanswered items are outstanding, but the **silent message drop bug** (#5344) and **custom provider tooling gap** (#5345) require prioritized maintainer attention to close.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-21

## Today's Overview

ZeroClaw shows **high-intensity development activity** today with 50 issues and 50 PRs updated in the last 24 hours, reflecting a project in active sprint execution. The maintainer team is processing multiple concurrent workstreams across observability, authentication, skills platform (v0.8.2), and the upcoming v0.9.0 breaking-change cycle. Open issues outnumber closed ones by roughly 7:1 (44 vs 6), while PRs show a ~4.5:1 open-to-merged ratio (41 vs 9), indicating a heavy review pipeline still in progress. No new releases were cut today, but milestone-tracked work toward **v0.8.2 (skills platform)** and **v0.9.0 (auth/security/gateway)** is clearly advancing through merged PRs and accepted RFCs.

## Releases

**None** — No new releases published in the last 24 hours.

## Project Progress

Nine PRs were merged or closed today. Notable advancements include:

- **Cost configuration fix** — PR #8004 (`singlerider`) made `CostConfig` dynamically reloadable instead of frozen at boot, fixing a latent configuration staleness bug.
- **Yanked dependency resolution** — PR #7992 (`singlerider`) updated `Cargo.lock` to replace yanked `bitcoin-io 0.1.100` and `bitcoin_hashes 0.14.100` transitive dependencies.
- **External tool working_directory fix** — Issue #7877 (closed) discovered external coding tools resolve relative `working_directory` from the daemon cwd; fix merged.
- **Voice peer SSOT violation** — Issue #7795 (closed) fixed a latent single-source-of-truth violation in Telegram's `static_voice_peers` caching.
- **Android infinite loop** — Issue #6036 (closed) resolved an infinite tool-call loop on Termux/Android.

Substantial open PRs still in review include critical runtime fixes for streamed narration duplication (#8014), skill read path misdirection (#8047), and manual cron trigger persistence (#7893).

## Community Hot Topics

The following issues generated the most community discussion:

1. **[Feature]: Dream Mode — Periodic Memory Consolidation & Reflective Learning** ([#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)) — 18 comments  
   *Analysis:* The highest-engagement issue reflects deep user desire for autonomous memory management during idle periods. Users want ZeroClaw to self-improve between interactions, reducing reliance on external memory tools. This has been accepted and is `in-progress`.

2. **[Bug]: zeroclaw does not know it can add cron** ([#5862](https://github.com/zeroclaw-labs/zeroclaw/issues/5862)) — 13 comments  
   *Analysis:* A fundamental usability gap — the agent is unaware of its own capabilities. Users expect agentic self-discovery of available tools. The `needs-author-action` label suggests maintainers are waiting for repro steps.

3. **RFC: Work Lanes, Board Automation, and Label Cleanup** ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) — 11 comments  
   *Analysis:* Community interest in project governance and workflow automation indicates a maturing contributor base wanting clearer contribution paths. Accepted and in rollout.

## Bugs & Stability

**High-severity bugs reported today:**

- **[#8047] ReadSkillTool looks in `data_dir` but skills live in agent workspace** (risk:high, priority:p2) — Skills tool returns "Unknown skill" because it searches the wrong directory. **No fix PR yet** but clearly related to active v0.8.2 work.

- **[#8075] Zerocode keybinds vs. OS globals** (risk:medium, priority:p2) — MacOS keyboard conflicts (`ctrl+up`); PC keybinds forbidden in terminal. No fix PR filed.

**Critical existing bugs still open:**

- **[#5808] Default context budget exceeded on iteration 1** (risk:high, priority:p1, in-progress) — 32k token budget is ~3.3x oversubscribed by system prompt + tools before any user message. Perpetual preemptive trimming degrades conversation quality.

- **[#6037] Cron jobs launched repeatedly while still running** (risk:high, priority:p1, accepted) — No concurrency guard causes burst execution of same cron job.

- **[#5844] Too much emphasis on memory** (risk:high, priority:p1, accepted) — Memory context dominates system prompt, especially in cron jobs, degrading current-task focus.

**Fix PRs in flight for active bugs:** PR #8014 (streamed narration duplication, risk:high), PR #7940 (gateway agent rename persist ordering, risk:high), PR #7893 (manual cron trigger persistence, risk:high).

## Feature Requests & Roadmap Signals

**High-priority accepted features likely shipping in next release:**

- **v0.9.0 auth work** ([#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)) — OIDC Authentication Provider support is the marquee feature for v0.9.0, with child issue [#8076](https://github.com/zeroclaw-labs/zeroclaw/issues/8076) adding local username/password IdP-less login.

- **v0.8.2 skills platform** ([#7852](https://github.com/zeroclaw-labs/zeroclaw/issues/7852)) — Registries, effective-skill resolution, plugin-bundled skills, missing-capability suggestions, and operator-visible skill facts.

- **Structured observability** ([#7232](https://github.com/zeroclaw-labs/zeroclaw/issues/7232), accepted, in-progress) — Rich event context, OTel trace correlation, bridge refactoring. PRs [#8066](https://github.com/zeroclaw-labs/zeroclaw/pull/8066) and [#8065](https://github.com/zeroclaw-labs/zeroclaw/pull/8065) land opt-in LLM payload capture and trace_id + per-call cost correlation.

**User-requested features with strong momentum:**

- **Streaming card messages** ([#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)) — Reduce user wait anxiety on QQ/DingTalk/WeChat/Feishu.
- **Voice satellite hardware** ([#7944](https://github.com/zeroclaw-labs/zeroclaw/issues/7944)) — ESP32/browser PWA with approval buttons over voice-host contract.
- **Docker docs inclusion** ([#7950](https://github.com/zeroclaw-labs/zeroclaw/issues/7950)) — Enable agents to answer ZeroClaw usage questions from within the image.

## User Feedback Summary

**Pain points expressed by users:**

1. **Capability self-discovery failure** — The agent doesn't know it can add cron jobs ([#5862]), reflecting broader expectations that ZeroClaw should introspect its own toolset.

2. **Memory flooding** — Users report that memories dominate context windows, drowning out current prompt intent, especially in cron jobs ([#5844], [#5808]).

3. **Context overflow hallucination** — Long conversations drift off-topic as context windows fill ([#6517]), with no graceful truncation strategy.

4. **Infinite loops and hangs** — Termux/Android infinite tool-call loops ([#6036], now closed) and streaming error hangs ([#6243], closed) erode trust in reliability.

5. **Configuration friction** — Users struggle with provider endpoint configuration ([#6558]), service installation on macOS ([#5883]), and budget config freezing at boot ([#8004], fix merged).

**Satisfaction signals:** The community is actively contributing detailed RFCs (#6808, #7232, #5907) and submitting well-structured bug reports with reproduction steps, indicating a technically sophisticated user base invested in the project's direction. The Dream Mode feature (#5849) with 18 comments shows genuine excitement around autonomous agent improvement.

## Backlog Watch

**Issues needing maintainer attention (stale/blocked):**

- **[#6672] reasoning_content not passed back with Xiaomi thinking mode** (risk:high, priority:p2, blocked/stale since May 15) — S0 severity (data loss) but blocked awaiting author action. No progress in 5+ weeks.

- **[#6558] providers error — custom API 405** (risk:low, priority:p3, blocked/stale since May 10) — User reported S0 severity but labeled low risk and stale.

- **[#6517] Context overflow hallucination** (risk:medium, priority:p2, blocked/stale since May 7) — Degraded behavior but no repro steps from author.

- **[#5907] Opt-in LSP support RFC** (risk:high, priority:p2, blocked since April 19) — Accepted RFC but blocked with no clear blocker documented. Could accelerate coding workflows.

**PRs needing review attention:**

- **[#6297] Expose poll-vote/interactive-reply events** (enhancement, size:L, risk:high, open since May 3) — Adds Signal/WhatsApp interactive reply support. Large, complex, no maintainer activity in weeks.

- **[#7094] Fix CLI models set persistence** (bug, size:XS, risk:medium, open since June 2) — Simple fix but `zeroclaw models set` remains non-functional.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*