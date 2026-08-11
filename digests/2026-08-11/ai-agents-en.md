# OpenClaw Ecosystem Digest 2026-08-11

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-11 00:45 UTC

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

# OpenClaw Project Digest
**Date:** 2026-08-11

---

## 1. Today's Overview

OpenClaw is experiencing a high-volume activity period, with 500 issues and 500 PRs updated in the last 24 hours. A significant portion of the open issue backlog (403 issues) remains actively discussed, indicating a large and engaged community. The project is in a heavy refactoring phase, with maintainer `steipete` driving multiple large-scale codebase improvements (export name collisions, coercion helpers, session accessors). No new official releases were cut today, but a release candidate PR (`#121743`) is awaiting approval for 2026.8.1 beta.2. Message-delivery reliability and session-state consistency remain the most prevalent areas of concern across both issues and PRs.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent release track visible in the PR queue is `2026.8.1 beta.2`, with a candidate currently undergoing CI evaluation ([PR #121743](https://github.com/openclaw/openclaw/pull/121743)). Given the extensive refactoring landing across core, gateway, and agents, the next release may carry a notable upgrade review burden, particularly around compatibility and session-state.

---

## 3. Project Progress

Several closed or ready-for-review PRs indicate forward progress on stabilization and developer experience:

- **Message Delivery Fix Under Contention** ([PR #121662](https://github.com/openclaw/openclaw/pull/121662), closed): Prevents cross-session sends from failing with a false `GatewayDrainingError` when lanes inherit another entry's lifecycle context.
- **Durable State Stall Fix** ([PR #121647](https://github.com/openclaw/openclaw/pull/121647), ready for review): Resolves a blocker where context engines froze after transcripts exceeded 20,000 events or 8 MiB, wrongly classifying small turns as too-large.
- **Subagent State Cleanup** ([PR #121631](https://github.com/openclaw/openclaw/pull/121631), closed): Removes dead `retry-limit` and `lost-execution-context` state variants that production code could not actually generate.
- **UI Improvements** ([PR #121692](https://github.com/openclaw/openclaw/pull/121692), [PR #121682](https://github.com/openclaw/openclaw/pull/121682)): Adds in-place editing and reordering of queued chat messages in the Control UI composer.

A large wave of maintainer-driven refactors is underway (`#121768`, `#121366`, `#121536`, `#121715`), aimed at consolidating helper logic, eliminating export collisions, and migrating internal callers to typed facades—improving codebase maintainability ahead of future feature work.

---

## 4. Community Hot Topics

The following issues attracted the most discussion (high comment counts) and reveal core pain points around reliability and UX:

- **Silent Reply Failures Persist** ([Issue #121058](https://github.com/openclaw/openclaw/issues/121058), 47 comments, open): Despite issue #116277 being closed, the monitoring cron continues to log silent-reply failures. The issue was reopened today with new evidence. This is a high-visibility trust problem for users relying on notification channels.

- **Memory Trust Tagging by Source** ([Issue #7707](https://github.com/openclaw/openclaw/issues/7707), 33 comments, open): A well-articulated feature request to tag memory entries by provenance (user commands vs. web scrapes) to prevent memory poisoning attacks. This reflects a growing security awareness in the community.

- **Tiered Bootstrap File Loading** ([Issue #22438](https://github.com/openclaw/openclaw/issues/22438), 18 comments, open): Users with large workspaces want to control context-window bloat by tiering which bootstrap files load into sessions vs. sub-agents vs. cron jobs. This is a pragmatic cost-control request.

- **Duplicate Telegram Replies** ([Issue #86519](https://github.com/openclaw/openclaw/issues/86519), 15 comments, **closed**): The recurring duplicate-reply regression after 5.20 appears to have been resolved, but users noted residual severity reduction only, suggesting the fix may be partial.

---

## 5. Bugs & Stability

Ranked by severity as reported today:

| Severity | Issue | Title | Notes |
| :--- | :--- | :--- | :--- |
| High (P1) | [#119087](https://github.com/openclaw/openclaw/issues/119087) | Gateway cold start regressed ~2.5x on 1-vCPU | Open; needs maintainer review |
| High (P1) | [#115908](https://github.com/openclaw/openclaw/issues/115908) | Transcript projection livelock blocks main thread | Open; source repro available |
| High (P1) | [#40001](https://github.com/openclaw/openclaw/issues/40001) | Write tool overwrites shared cron files (data loss) | Open; no new fix PR |
| High (P1) | [#111010](https://github.com/openclaw/openclaw/issues/111010) | Detached Codex subagents lose tools on parent release | Open; needs security review |
| Medium (P2) | [#119796](https://github.com/openclaw/openclaw/issues/119796) | Windows vitest teardown EBUSY on sqlite | Open; linked PR open |
| Medium (P2) | [#120735](https://github.com/openclaw/openclaw/issues/120735) | Telegram stickers unusable as file refs | Open; source repro, fix PR linked |
| Medium (P2) | [#119119](https://github.com/openclaw/openclaw/issues/119119) (inferred from [#121647](https://github.com/openclaw/openclaw/pull/121647)) | Durable context stall in long sessions | Fix PR ready for review |

**Signal:** The silent-reply failure ([#121058](https://github.com/openclaw/openclaw/issues/121058)) is the most severe recurring bug, as it directly undermines user confidence in autonomous operation. Duplicate Telegram messages remain a recurring theme despite prior closures, indicating a hard-to-catch race condition.

---

## 6. Feature Requests & Roadmap Signals

- **`announceTarget` for sub-agent routing** ([#27445](https://github.com/openclaw/openclaw/issues/27445), 12 comments, +5 👍): Strong demand for main-agent orchestration of multi-step sub-agent flows. This is a likely next-version candidate.
- **Per-agent cost budget enforcement** ([#42475](https://github.com/openclaw/openclaw/issues/42475), 14 comments): Operators want gateway-level spend caps to prevent runaway costs.
- **Per-spawn tool restrictions for sub-agents** ([#15032](https://github.com/openclaw/openclaw/issues/15032), 7 comments): The "DMZ Web Search" use case underlines security-driven demand for sub-agent sandboxing.
- **Configurable agent identity preamble** ([#43562](https://github.com/openclaw/openclaw/issues/43562), 4 comments): Users want to replace the hardcoded "personal assistant" identity—a small change with significant UX impact.
- **Context window % in system prompt** ([#38568](https://github.com/openclaw/openclaw/issues/38568), 6 comments): Agents could self-manage context if they knew their usage percentage.

**Prediction:** The 2026.8.x releases will likely include the sub-agent orchestration features (`announceTarget`) and the consolidation refactors that pave the way for safer plugin and sub-agent execution.

---

## 7. User Feedback Summary

- **Dissatisfaction:** Silent reply failures and duplicate Telegram messages are eroding trust in delivery reliability. Users are actively monitoring and reopening issues when fixes fail to hold, which is a strong signal of dissatisfaction.
- **Pain Points:** Context-window management is a recurring theme—users feel the agent burns tokens on irrelevant bootstrap files and want more control over session initialization and tool access.
- **Positive Signals:** Users are requesting advanced features (theme customization, UI polish, cost controls) which indicate a maturing product with a committed user base. The high volume of PRs from maintainers suggests active investment in code quality and debt reduction.
- **Frustration:** Users (e.g., during onboarding) find TUI defaults confusing ([#33102](https://github.com/openclaw/openclaw/issues/33102)), suggesting documentation and default-config UX need improvement.

---

## 8. Backlog Watch

The following items have been open for a long time with no new fix PR and require product decisions or maintainer attention:

- **[#7707](https://github.com/openclaw/openclaw/issues/7707) (since Feb 2026)** – Memory Trust Tagging by Source: High-value security feature, still in discussion.
- **[#83598](https://github.com/openclaw/openclaw/issues/83598) (since May 2026)** – `anthropic:claude-cli` OAuth refresh dead-ends: A critical auth bug for macOS users, still open.
- **[#100941](https://github.com/openclaw/openclaw/issues/100941) (since Jul 2026)** – WebSocket drops under parallel tool fan-out: Performance/availability issue, still open.
- **[#47975](https://github.com/openclaw/openclaw/issues/47975) (since Mar 2026)** – Subagent sessions persist and block main session: Core session-state bug, no new fix PR.
- **[#45494](https://github.com/openclaw/openclaw/issues/45494) (since Mar 2026)** – Cron jobs silently time out during API outages: Need for fast-fail behavior, unresolved.

These items represent unresolved technical debt that could erode user trust if not addressed soon.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-11
**Scope:** 13 AI agent / personal assistant open-source projects

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a **rapid consolidation and hardening phase**, characterized by intense refactoring, security hardening, and reliability fixes across nearly all major projects. Development velocity remains exceptionally high—flagship projects like OpenClaw and ZeroClaw are processing 500+ issues/PRs per 24-hour window—but the focus has shifted from feature velocity to **stability, security-by-default, and architectural debt reduction**. A universal theme across projects is **message-delivery reliability and silent failure elimination**, with nearly every digest highlighting user frustration over silently dropped messages, unreported errors, or resource-exhaustion loops. The ecosystem is also converging on **MCP (Model Context Protocol) as the standard integration layer**, with multiple projects actively migrating to SDK v2, adding OAuth support, and expanding remote server capabilities. Governance and process maturity are emerging as differentiators, with projects like ZeroClaw formalizing RFC processes while others struggle with contributor bottlenecks.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score | Notes |
|---------|:---:|:---:|:---:|:---:|-------|
| **OpenClaw** | 500+ | 500+ | 2026.8.1 beta.2 (RC) | **7/10** | Heavy refactoring; reliability concerns persist |
| **ZeroClaw** | 50 | 50 | 0.8.3 (current) | **6/10** | Security audit wave; RFC process bottleneck |
| **IronClaw** | 50 | 50 | v1.1.1-rc.1 | **8/10** | Strong quality discipline; rapid patch cadence |
| **Hermes Agent** | 50+ | 50+ | v2026.8.3 (desktop) | **7/10** | Dual-track dev; EMFILE/Windows issues |
| **CoPaw (QwenPaw)** | 40 | 50 | v2.1.0b2 (pre-release) | **7/10** | Pre-release stabilization; Docker/MCP issues |
| **NanoBot** | ~4 | 23 | No new release | **9/10** | Fast, responsive maintainers; security-focused |
| **NanoClaw** | 3 | 20 | v2 (June) | **8/10** | Active sprint; session-DB focus |
| **LobsterAI** | 1 | 20+ | 2026.4.1 | **7/10** | UI polish + gateway fixes |
| **PicoClaw** | 4 | 9 | v0.3.1 | **7/10** | Moderate velocity; PR merge lag |
| **Moltis** | 3 | 1 | No new release | **6/10** | Quiet; large PR in limbo |
| **TinyClaw** | 0 | 0 | — | **5/10** | No activity |
| **ZeptoClaw** | 0 | 0 | — | **5/10** | No activity |
| **NullClaw** | 1 | 1 | No new release | **6/10** | Maintenance phase; low bandwidth |

---

## 3. OpenClaw's Position

**Advantages vs. peers:**
- **Scale:** 500+ issues/PRs per day dwarfs all competitors—a clear signal of the largest user base and most active contributor community.
- **Ecosystem gravity:** The consistent stream of maintainer-driven refactors (export collisions, coercion helpers, session accessors) shows a maturing codebase being prepared for long-term extensibility.
- **Breadth of channels:** Telegram, Slack, Matrix, WeChat, and more—the breadth of integrations is a major differentiator for users needing multi-platform presence.

**Technical approach differences:**
- **Typed facades and session-state architecture:** The session-accessor migration is a deliberate architectural investment that competitors haven't matched at the same scale.
- **Sub-agent orchestration:** `announceTarget` feature demand and Codex sub-agent support indicate a more sophisticated multi-agent orchestration model than peers' simpler delegation patterns.
- **Tiered bootstrap loading** (being debated) would give OpenClaw a cost-control advantage for large workspaces that competitors lack.

**Community size comparison:**
- OpenClaw's community is **10-20x larger** than mid-tier projects (NanoBot, PicoClaw, Moltis) and **2-5x larger** than the next tier (ZeroClaw, IronClaw, CoPaw).
- The sheer volume of bug reports and reopenings (e.g., #121058 with 47 comments) indicates a deeply engaged, long-tail user base.

**Key risk:** The silent-reply failure cron job is a trust-destroying bug that could drive users to competitors if not resolved soon.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|-----------|----------|----------------|
| **Message Delivery Reliability** | OpenClaw (silent replies), NanoClaw (message-ID reuse drops), Hermes (cron delivery), IronClaw (connect-nudges), PicoClaw (tool-failure loops) | No silent failures; deduplication; visible error states |
| **MCP Standardization** | NanoBot (SDK v2 migration, OAuth), NanoClaw (Streamable HTTP), CoPaw (tool failures), ZeroClaw (custom CA trust) | OAuth for remote servers; type-safe args; SSRF validation |
| **Session-State Consistency** | OpenClaw (state stall >20k events), Hermes (EMFILE leaks), CoPaw (SIGBUS), ZeroClaw (daemon reload) | Durable state; long-uptime stability; crash recovery |
| **Cost/Resource Governance** | OpenClaw (cost budgets), NanoBot (token usage records), PicoClaw (max_tokens), Moltis (resource limits), IronClaw (tool-call budgets) | Spending caps; token metering; runaway-loop prevention |
| **Security Hardening** | ZeroClaw (S0 audit findings), NanoBot (WebSocket-only mutations), IronClaw (approval transparency), CoPaw (plugin sandboxing) | Per-agent isolation; provenance tagging; sandbox escapes |
| **Windows Desktop Support** | Hermes (React crashes), CoPaw (installer, IME), LobsterAI (pip shims), PicoClaw (Docker) | Crash-free UX; IME handling; reliable installation |
| **Context-Window Management** | OpenClaw (tiered bootstraps), ZeroClaw (per-model config), CoPaw (memory system) | Token efficiency; model capability accuracy; memory quality |

---

## 5. Differentiation Analysis

| Project | Feature Focus | Target Users | Architecture |
|---------|--------------|--------------|--------------|
| **OpenClaw** | Breadth + deep integrations | Power users, heavy automation | Modular, multi-agent orchestration, typed facades |
| **ZeroClaw** | Security, governance, RFC process | Enterprise, security-conscious | Gateway + runtime + channels, extensive governance |
| **IronClaw** | Channel UX, WebUI polish, extensions | SMB, teams needing chat-first | IronHub skill packages, extensions vNext |
| **Hermes Agent** | Desktop app (Tauri-like), skills, Kanban | Individual power users | Desktop + Gateway + SessionDB, god-file sharding |
| **NanoBot** | Lightweight, security, MCP OAuth | Developers, MCP-heavy workflows | Fast Python core, WebSocket mutations, MCP SDK v2 |
| **CoPaw** | Memory (ReMe), rich UI, multi-modal | Chinese-speaking users, heavy chat | Console + memory + provider-federation |
| **NanoClaw** | Session-DB integrity, privacy (DM logs) | Privacy-sensitive operators | Host/module lifecycle, per-turn scoped messaging |
| **LobsterAI** | Desktop-app parity, Cowork UI | Desktop users | OpenClaw gateway + React frontend |
| **PicoClaw** | Lightweight, Telegram-native | Raspberry Pi, hobbyists | Small footprint, i18n-friendly |
| **Moltis** | Sandboxed containers, Apple Container | Developers needing isolation | Container backends, CDP browser viewing |
| **NullClaw** | A2A protocol, agent federation | Multi-instance operators | Minimalist, protocol-focused |

---

## 6. Community Momentum & Maturity

**Tier 1 — High-Velocity Sprint (daily releases, heavy activity):**
- **NanoBot** — Exceptional responsiveness (bugs fixed same-day); security-forward culture; highest health score (9/10).
- **OpenClaw** — Massive activity but burdened by legacy debt; RC cadence indicates approaching stability.
- **ZeroClaw** — Velocity suppressed by RFC governance; security audit wave shows active hardening.

**Tier 2 — Rapid Iteration (weekly/minor releases):**
- **IronClaw** — Best discipline: self-aware architecture audits; rapid patch releases (1.1.1-rc.1).
- **CoPaw** — Pre-release stabilization for v2.1.0; high feature momentum with mixed stability.
- **Hermes Agent** — Dual desktop/core tracks; fix-forward cadence but EMFILE/Windows issues linger.
- **NanoClaw** — Active core-team sprint; session-DB and MCP-follow-on work shipping fast.
- **LobsterAI** — UI polish and gateway fixes landing daily.

**Tier 3 — Moderate/Slow (maintenance-plus):**
- **PicoClaw** — Steady but slower; PR merge latency is a concern.
- **Moltis** — Mostly quiet; single large PR in review for 4 months.
- **NullClaw** — Low bandwidth; single issue closure today; Dependabot PR two months stale.

**Tier 4 — Inactive:**
- **TinyClaw**, **ZeptoClaw** — Zero activity; likely dormant.

---

## 7. Trend Signals

### Industry Trends for AI Agent Developers

1. **Silent failure is the #1 trust killer.** Across all projects, users are more frustrated by messages that silently vanish than by any feature gap. Expect all major agent frameworks to invest in delivery receipts, error surfacing, and observability tooling in the next 6-12 months.

2. **Security-by-default is becoming table stakes.** ZeroClaw's S0 audit wave, NanoBot's WebSocket-only mutations, and PicoClaw's remote exec hardening all point to a market shift: agents that can execute code, access files, and send messages must ship with secure defaults and per-call approval.

3. **MCP is winning the integration battle.** The ecosystem is consolidating on MCP v2 with OAuth, remote servers, and Streamable HTTP. Projects without MCP support (or still on v1) risk being orphaned from the tool ecosystem.

4. **Cost governance is an emerging competitive lever.** Token-burn incidents (NanoBot's 10M-token runaway loop) and user demands for budgets/tiered bootstraps indicate that agent economics—not just features—will differentiate platforms going forward.

5. **Session-state durability is the scalability bottleneck.** Long-running agents (40+ hours) inevitably hit key collisions, file-descriptor exhaustion, or log corruption. The projects that solve this (IronClaw's lease isolation, NanoClaw's dedup, OpenClaw's context fix) will win enterprise workloads.

6. **Desktop-experience quality is a differentiator for power users.** Windows/macOS crashes (Hermes React #310, CoPaw SIGBUS), Chinese IME handling (CoPaw), and hidden-file toggles (CoPaw) show that UX polish is as important as agent capability for retention.

7. **Governance processes impact velocity.** ZeroClaw's RFC bottleneck and PicoClaw's stale PRs show that process design directly affects delivery velocity. Multi-agent teams need lean decision-making—NanoBot's same-day fixes are the benchmark.

8. **Plugin/extension ecosystems are maturing.** IronClaw's Extensions vNext and NanoClaw's Agent Plugins 1.0 indicate a shift toward versioned, hardened plugin APIs—the natural next step for platforms seeking ecosystem lock-in.

---

*Prepared for technical decision-makers and developers evaluating the personal AI assistant / agent open-source landscape as of 2026-08-11.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**2026-08-11 | Generated from HKUDS/nanobot GitHub Activity**

---

## 1. Today's Overview

NanoBot is experiencing a high-velocity development cycle, with 23 pull requests updated in the last 24 hours and 10 merged/closed — suggesting a well-maintained and actively governed codebase. Activity is clustered around several major themes: security hardening (WebSocket-only mutations, Docker privilege drops, reflective state access removal), provider extensibility (new OrcaRouter gateway, MCP SDK v2 migration, OAuth support for remote MCP servers), and a substantial WebUI refactoring effort. A P0-severity bug fix for session data corruption is in flight, and two open bugs regarding duplicate message output and provider argument encoding are awaiting resolution. No new releases were published during this window.

---

## 2. Releases

No new releases were published in the last 24 hours. The project remains between release cycles.

---

## 3. Project Progress

Ten PRs were merged or closed, reflecting significant forward momentum:

### Features & Enhancements
- **[PR #5316 — feat(mcp): add browser OAuth for remote servers](https://github.com/HKUDS/nanobot/pull/5316)** *(merged)* — Adds browser-based OAuth for remote Streamable HTTP and SSE MCP servers via the official MCP SDK. Includes one-click presets for Xmind, Notion, and Linear, plus OAuth support for imported/custom MCP configs. This directly addresses the [feature request in Issue #5297](https://github.com/HKUDS/nanobot/issues/5297).

### Security & Stability
- **[PR #5317 — fix(webui): move mutations to authenticated WebSocket requests](https://github.com/HKUDS/nanobot/pull/5317)** *(merged, priority: p1)* — State-changing WebUI operations moved from GET/query-string/custom-header HTTP calls to correlated request/reply frames on the authenticated WebSocket connection, with an allowlisted bridge and rejection of unauthenticated mutations.
- **[PR #5319 — refactor(agent): replace reflective runtime state access](https://github.com/HKUDS/nanobot/pull/5319)** *(merged)* — Replaces `MyTool`'s reflective loop-state wrapper with an explicit `RuntimeControl` protocol and `AgentRuntimeControl` adapter, exposing exact allowlisted snapshots and redacting credential-bearing configuration fields.
- **[PR #5318 — refactor(webui): extract deterministic event projection helpers](https://github.com/HKUDS/nanobot/pull/5318)** *(merged)* — Cleaner event-stream handling with deterministic, reusable projections and explicit reasoning-completion timing.

### UX & Polish
- **[PR #5315 — fix(webui): improve UX recovery and empty states](https://github.com/HKUDS/nanobot/pull/5315)** *(merged)* — Preserves the first prompt and rejected project path on workspace-scoped chat creation failure; simplifies the auth challenge UI.
- **[PR #5325 — fix(files): reject no-op edits](https://github.com/HKUDS/nanobot/pull/5325)** *(merged)* — Directly addresses the [infinite-loop bug in Issue #5324](https://github.com/HKUDS/nanobot/issues/5324) by rejecting `edit_file` calls with identical `old_text`/`new_text`.
- **[PR #5310 — fix(weixin): honor forced QR login](https://github.com/HKUDS/nanobot/pull/5310)** *(merged)* — WeChat integration now performs a fully fresh QR flow when forced login is triggered.
- **[PR #5321 — refactor(webui): make gateway own settings services](https://github.com/HKUDS/nanobot/pull/5321)** *(merged)* — Gateway-owned WebUI settings service with atomic read-modify-write operations.

### Config & Refactoring
- **[PR #5326 — fix(webui): soften form control focus rings](https://github.com/HKUDS/nanobot/pull/5326)** *(merged)* — Subdued 2px inset focus treatment across form controls.

---

## 4. Community Hot Topics

The most active discussions this cycle, ranked by engagement:

1. **[Issue #5297 — MCP OAuth web authorization (3 comments, closed)](https://github.com/HKUDS/nanobot/issues/5297)** → **Featured in this digest's top topic.** Users need to connect to MCP servers requiring OAuth web flows (e.g., Xmind) but are blocked because the current CLI/WebUI flow does not support remote HTTP-based authorization. The proposal suggests using a gateway to fetch authorization info, enabling remote access via IP/domain. **This issue was resolved by PR #5316, which shipped OAuth presets for Xmind, Notion, and Linear.**

2. **[Issue #5324 — Dream memory consolidation infinite loop (2 comments, closed)](https://github.com/HKUDS/nanobot/issues/5324)** → A severe resource drain: the Dream memory task ran for 23 minutes consuming >10M tokens (half a month's quota) because `edit_file` accepted no-op edits, triggering an unbounded retry loop. **Fixed by PR #5325.**

3. **[PR #5179 — Migrate MCP integration to SDK v2 (open, long-running)](https://github.com/HKUDS/nanobot/pull/5179)** → This is the largest ongoing migration, touching core MCP client infrastructure while preserving SSRF validation, redirect checks, DNS pinning, proxy routing, and finite timeouts. Its duration (since July 30) reflects its complexity and importance.

4. **[PR #5328 — feat(providers): add OrcaRouter as a named gateway provider](https://github.com/HKUDS/nanobot/pull/5328)** → A new gateway aggregating 150+ models from OpenAI, Anthropic, Google, DeepSeek, Qwen, MiniMax and xAI with zero-trust security for AI agents — a strong signal of the ecosystem's push toward multi-provider routing.

The underlying need across these topics is clear: **users want broader model provider access, simpler connectivity to third-party MCP ecosystems, and protection from runaway resource consumption.**

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **P0** | [Issue — stale background task session overwrites](https://github.com/HKUDS/nanobot/pull/5271) | Background tasks (`maybe_generate_webui_title`) hold stale `Session` references across awaits; user-initiated `/new` can cause old tasks to overwrite fresh session data. | **Fix PR #5271 open** — waits for task completion before session invalidation, or cancels the old turn. |
| **P1** | [Issue #5324 — Dream infinite loop](https://github.com/HKUDS/nanobot/issues/5324) | `edit_file` accepting no-op edits caused an unbounded 10M+ token burn in 23 minutes. | **Fixed in PR #5325 (merged)**. |
| **P1** | [PR #5320 — Docker privilege drop regression](https://github.com/HKUDS/nanobot/pull/5320) | Docker image starts as root; `cap_drop: ALL` broke the root bootstrap path (entrypoint ownership fix). | **Fix PR #5320 open** — restores the three required capabilities. |
| **P2** | [Issue #5300 — MCP anyio cancel scope crash](https://github.com/HKUDS/nanobot/issues/5300) | Remote MCP returning HTTP 530 caused `RuntimeError: Attempted to exit cancel scope in a different task`, crashing the gateway and causing CPU spikes from leaked tasks. | **Closed, no fix PR identified in this window.** |
| **P2** | [Issue #5327 — Duplicate reasoning messages](https://github.com/HKUDS/nanobot/issues/5327) | Nanobot randomly repeats the same message multiple times while reasoning. | **Open, no fix PR yet.** |
| **P2** | [Issue #5311 — Agnes AI double-encodes nested tool args](https://github.com/HKUDS/nanobot/issues/5311) | Provider encodes nested object/array tool arguments as JSON strings, causing MCP validation errors (-32602). | **Fix PR #5314 open** — proposes schema-aware decoding. |

---

## 6. Feature Requests & Roadmap Signals

| Request | Status | Likelihood of Landing |
|---------|--------|-----------------------|
| **OAuth support for remote MCP servers** (Issue #5297) | **Already shipped** in PR #5316 | ✅ Done — expect it in the next release. |
| **OrcaRouter as a named gateway provider** (PR #5328) | Open, ready for review | High — completes the "named provider" pattern already present for other gateways. |
| **Structured token usage records** (PR #5299) | Open, ready for review | High — the API layer (`GET /api/settings/usage/records`) is well-specified and adds real operational value. |
| **Tabbed-pane workbench WebUI** (PR #5322) | Open, ready for review | Medium — substantial UX surface change; may take additional review cycles. |
| **Agent Plugins with CLI Apps** (PR #5288) | Open, ready for review | Medium — depends on the plugin ecosystem stabilizing around Agent Plugins v1. |
| **Gateway-owned settings services** (PR #5323) | Open, flagged `conflict` | Medium — needs reconciliation with the merged PR #5321 to avoid merge conflicts. |

**Roadmap signal:** The burst of WebUI refactoring (deterministic event projection, gateway-owned settings, tabbed panes) points to a **major WebUI overhaul** in upcoming releases, with a focus on multi-session workbenches and cleaner architecture.

---

## 7. User Feedback Summary

### Pain Points
- **Resource exhaustion risk:** The Dream infinite-loop bug (Issue #5324) caused half a month's token quota loss in 23 minutes — users feel the impact of unbounded retry loops in both cost and availability.
- **Provider fragmentation:** Users report friction with non-OpenAI-compatible providers (Agnes AI double-encoding, Issue #5311; Xmind's OAuth wall, Issue #5297) — the ecosystem is hitting the limits of strict OpenAI-shape assumptions.
- **Distraction during reasoning:** Duplicate message repetition (Issue #5327) degrades the interaction experience, particularly on longer investigation tasks.

### Positive Signals
- **Active maintainer response:** Bugs filed on 2026-08-08/08-10 are being addressed the same day (PR #5325 fixing Issue #5324; PR #5316 fulfilling Issue #5297's feature request). This responsiveness is a strong health indicator.
- **Security-focused development:** The WebSocket-only mutation change and gateway-owned settings point to proactive security hardening rather than reactive patching.

---

## 8. Backlog Watch

| Item | Age | Why It Needs Attention |
|------|-----|------------------------|
| [PR #5179 — MCP SDK v2 migration](https://github.com/HKUDS/nanobot/pull/5179) | ~12 days | Long-running, core-infrastructure PR that touches transport, SSRF validation, redirect handling, and DNS pinning. It's marked `conflict` — needs maintainer review or explicit deferral decision. |
| [PR #5257 — Bound sustained-goal continuation](https://github.com/HKUDS/nanobot/pull/5257) | ~5 days | Addresses unbounded goal-continuation nudges. Marked `conflict`; given the token-burn incident in Issue #5324, this should be prioritized to prevent another runaway-loop scenario. |
| [Issue #5300 — MCP anyio cancel scope crash](https://github.com/HKUDS/nanobot/issues/5300) | 3 days | Closed but without a referenced fix PR. Given the severity (gateway crash, CPU spikes), maintainers should verify a regression test exists or the fix is tracked elsewhere. |
| [PR #5299 — Structured token usage records](https://github.com/HKUDS/nanobot/pull/5299) | 3 days | Ready for review; valuable for diagnosing the resource-consumption incidents users are hitting. |

---

**Overall health assessment:** NanoBot is in a healthy, actively-maintained state — merging roughly half of all open PRs within 24 hours, shipping fixes and features in tight cycles, and avoiding regressions. The project's biggest risk exposure is in the MCP transport and provider-compatibility layers, where several P1/P2 bugs are still awaiting merge. Maintainers are responsive, and the roadmap is clearly converging on a more secure, provider-agnostic, and WebUI-rich experience.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the GitHub data provided for Hermes Agent (github.com/nousresearch/hermes-agent) on 2026-08-11, here is the project digest:

---

### 1. Today's Overview

As of 2026-08-11, the Hermes Agent project is in a phase of intense, dual-track development: active stabilization of the desktop experience across platforms and a massive, structured refactoring effort. A high volume of open issues (44 of 50 active) is matched by an equally high volume of merged/closed items (18 of 50 PRs closed/merged today), indicating a strong "fix-forward" cadence. The most pressing and frequently reported problem class remains **file descriptor exhaustion (EMFILE)** across Desktop, Gateway, and SessionDB components, alongside recurring Windows-specific desktop crashes. Simultaneously, the maintainers have initiated a repository-wide "god-file" decomposition epic, with three byte-verbatim extraction PRs merged or opened today, signaling a firm architectural commitment to breaking down large, monolithic modules. The project is healthy but strained, with clear priorities on reliability (file handles, Windows behavior) and maintainability (refactoring) over new features this week.

### 2. Releases

No new releases were published in the last 24 hours. The most recent versions referenced in the data are `v2026.7.1` (from bug reports) and `v0.20.0 (2026.8.3)` and `v2026.8.3` (from desktop-related bug reports), indicating that the desktop release cadence is slightly ahead of the core runtime.

### 3. Project Progress

**Merged/Closed PR Highlights (18 total closed/merged):**

- **EMFILE & Stability Cluster** (Merged today): [#83542](https://github.com/NousResearch/hermes-agent/pull/83542) by teknium1 closes the "surviving halves of the EMFILE follow-up cluster after #83406." It addresses orphaned gateway reaping on restart, Desktop-owned gateway child termination, SSH-spawned remote backend ulimit increases, and `scandir` improvements. This is a direct countermeasure to the highest-severity bug class reported.
- **Core Stability** (Closed today): PR #83545 by wsotuo (closed) makes Windows sandbox routing reliable by keeping SSH-backed file paths in the POSIX namespace and making OpenSSH ControlMaster configurable. This is a companion to the EMFILE cluster.
- **Refactoring (Feature-adjacent)**: Three PRs by andrexibiza are part of the huge god-file sharding epic (#78647). While open, they were created today and are likely to be merged soon:
  - [#83547](https://github.com/NousResearch/hermes-agent/pull/83547): Extracts content-policy blocked-result helper from `conversation_loop` (7,306-line file).
  - [#83546](https://github.com/NousResearch/hermes-agent/pull/83546): Extracts idempotency cluster from `api_server.py` (7,188-line file).
  - [#83541](https://github.com/NousResearch/hermes-agent/pull/83541): Extracts s6 dispatch helper from `hermes_cli/gateway.py` (7,461-line file).
- **Automation**: The auto-merge workflow for JS formatting (#83539) was closed, indicating `main` moved and/or formatting was applied.

### 4. Community Hot Topics

The most active discussions center around **reliability and user experience**, not new features:

1.  **God-File Sharding Epic** — [#78647](https://github.com/NousResearch/hermes-agent/issues/78647) (64 comments) by andrexibiza remains the most commented issue. This is a structural/architectural debate endorsed by maintainers as the "only correct answer." It has spawned over 5 individual sub-issues (for files like `conversation_loop.py`, `api_server.py`, and `mcp_tool.py`), signaling a major, long-running effort that will be central to the project's short-term health.
2.  **EMFILE / File Descriptor Exhaustion** — Two issues are duplicates of the same root cause and have drawn significant attention:
    - [#83512](https://github.com/NousResearch/hermes-agent/issues/83512) (1 comment) and [#75269](https://github.com/NousResearch/hermes-agent/issues/75269) (9 comments, closed) describe a leak of one read-only SQLite connection per agent thread, leading to `Too many open files` after ~40 hours. The closure of #75269 and the merge of #83542 indicate that a fix has been shipped.
3.  **Windows Desktop React Crash** — [#80560](https://github.com/NousResearch/hermes-agent/issues/80560) (3 comments) and [#79428](https://github.com/NousResearch/hermes-agent/issues/79428) (1 comment) both hit the "Minified React error #310" ("Rendered more hooks"). The issue, occurring on Windows with v0.20.0, is a P2 with high community interest, and a fix PR (#83540) was opened today to address an "occluded-window" freeze that may be a related or identical cause.

### 5. Bugs & Stability

The bug report landscape is dominated by **session-state and file-descriptor issues**, followed by **Windows-specific crashes**. Most have active fix PRs, suggesting a responsive maintainer team.

**High Severity (P1):**
- **Kanban Database Regression** — [#83445](https://github.com/NousResearch/hermes-agent/issues/83445) by wkuntner (P1): A regression in Desktop 0.17.0 where `kanban.db` is created but never populated with schemas/tables, making the Kanban UI permanently empty even after restarts. This is a P1 functional loss for a core feature.
- **Silent CLI Queue Feedback** — [#83209](https://github.com/NousResearch/hermes-agent/issues/83209) (P1): Skill commands with instructions are silently queued when the agent is busy, causing user confusion and duplicate input replay. A fix PR is open today ([#83538](https://github.com/NousResearch/hermes-agent/pull/83538)).
- **Title Generation Failure** — [#82816](https://github.com/NousResearch/hermes-agent/issues/82816) by ilsunyan (P1): Fails 100% of the time on OpenAI-compatible providers that reject `response_format: json_schema`. This is a silent feature failure for users of vLLM/xgrammar backends.

**Medium Severity (P2) — Most with Active Fixes:**
- **EMFILE / Orphaned Backends** (macOS): [#78872](https://github.com/NousResearch/hermes-agent/issues/78872) (Closed, Fixed) and [#80898](https://github.com/NousResearch/hermes-agent/issues/80898) (Open). The fix in #83542 directly addresses these.
- **Windows Freeze** — [#83420](https://github.com/NousResearch/hermes-agent/issues/83420) (P1, Fix in PR #83540).
- **Cron Delivery Failures** — [#69304](https://github.com/NousResearch/hermes-agent/issues/69304) (deliver=origin for API sessions) and [#83484](https://github.com/NousResearch/hermes-agent/issues/83484) (indefinite retries for closed API sessions). A systemic issue with stateless delivery contexts.
- **Linux GUI Issues**: HUD mode is broken on X11/Xfce (band won't re-arm, input wedges) — [#83473](https://github.com/NousResearch/hermes-agent/issues/83473); Artifacts page timestamp bug (shows 1970) — [#83380](https://github.com/NousResearch/hermes-agent/issues/83380).

**Severity Regression Watch:**
- **uv sync --locked fails daily** — [#79434](https://github.com/NousResearch/hermes-agent/issues/79434) (P2): A persistent issue with lockfile staleness involving `defusedxml`/`python-olm`/`unpaddedbase64` packages. A P2 compatibility issue that will break installation/autoupdate for users on non-default platforms.

### 6. Feature Requests & Roadmap Signals

The maintainers are moving forward on several quality-of-life and platform-specific features:

- **Desktop Session Navigation** (Likely to ship next version): A series of PRs by cspiritsong are set to drastically improve the sidebar UX: [#82821](https://github.com/NousResearch/hermes-agent/pull/82821) adds a Sessions/Projects/Profiles view switcher bar; [#82822](https://github.com/NousResearch/hermes-agent/pull/82822) adds up/down stepper buttons; [#82823](https://github.com/NousResearch/hermes-agent/pull/82823) fixes per-profile project state clearing.
- **Gateway Runtime Transparency** (Likely to ship soon): [#83553](https://github.com/NousResearch/hermes-agent/pull/83553) adds opt-in `tokens_in`, `tokens_out`, and `effort` fields to the gateway runtime footer, enhancing cost transparency and control.
- **Kanban Concurrency** (Merged today): [#83552](https://github.com/NousResearch/hermes-agent/pull/83552) enforces a global Kanban worker concurrency cap, fixing `max_in_progress` boundary violations across boards.
- **Approval Transparency** (Open): [#83551](https://github.com/NousResearch/hermes-agent/pull/83551) aims to explain (via logs) why dangerous commands were auto-approved, improving auditability and trust in the approval mechanism.
- **Large New Feature** (Still being discussed): [#9485](https://github.com/NousResearch/hermes-agent/issues/9485) proposes "HermesClaw," a CRM frontend for the agent. This remains in the discussion phase (2 comments) and seems far from any roadmap commitment without maintainer signals.

### 7. User Feedback Summary

- **Pain Point (Highest Frequency):** **Desktop instability on macOS and Windows**. Users report very specific, reproduction-heavy bugs (file descriptor exhaustion, orphaned `serve` processes, React #310 crashes, HUD mode failure, artifacts timestamp mismatch). The comments indicate frustration with long-lived sessions degrading into unusable states (`EMFILE` / `Too many open files`) and requiring full process restarts.
- **Use Case:** **Power users pushing the system to its limits**. They run long-lived sessions (40+ hours), use Kanban boards, and rely on scheduled cron jobs for delivery to Matrix/Telegram. Their pain points are systemic resource leaks and edge-case delivery failures rather than basic functionality.
- **Satisfaction:** High satisfaction with desktop feature direction (the new session/project switcher PRs address direct user complaints), but clear dissatisfaction with the **stability slider** — the flurry of EMFILE and React #310 fixes suggests these issues have been frequently hit in the wild. The fact that fixes are landing within hours/days of reports (e.g., #83542 today for #83512 from yesterday) is a strong positive signal for user trust.

### 8. Backlog Watch

- **"[Feature]: HermesClaw — A CRM Frontend for Hermes Agent"** ([#9485](https://github.com/NousResearch/hermes-agent/issues/9485)) — Created 2026-04-14, has only 2 comments after 4 months. This is a massive feature request that has not received any maintainer response or reaction, indicating it's not on the roadmap.
- **"Session auto-title generation fails 100% of the time"** ([#82816](https://github.com/NousResearch/hermes-agent/issues/82816)) — Created 2026-08-10 (P2). While it has 1 comment and a label for P2, the silent failure nature and OpenAI-compatibility relevance make it a critical candidate for a quick fix. It’s a P1 per the bug ticket and needs prompt attention from maintainers.
- **"uv sync --locked fails daily"** ([#79434](https://github.com/NousResearch/hermes-agent/issues/79434)) — Created 2026-08-05 (P1). This is a P1 for installation stability but currently only has 1 comment from the reporter. It references 3 related issues (#75992 #76020 #78227), suggesting a longer-running family of problems. This blocks installs/updates for affected users and deserves a maintainer triage.
- **"kimi-coding credential pool base_url not re-resolved"** ([#5908](https://github.com/NousResearch/hermes-agent/issues/5908)) — Created 2026-04-07, has 2 👍 and 2 comments. This is a 4-month-old bug affecting a specific provider. It's a P2 credential management issue that hasn't been resolved, indicating lower priority for edge-case provider compatibility.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-11

## Today's Overview
PicoClaw shows solid maintenance velocity with 9 PRs updated in the last 24 hours (7 merged/closed, 2 open) and 4 issues touched (2 resolved). Two important bug fixes — one addressing silent tool failure loops and another targeting shell command authorization overrides — are both merged and remain open, suggesting active review cycles. Community contributions continue to broaden the project's surface area, with internationalization (Czech) and UX improvements (Telegram native table rendering, config deduplication) landing this week. The project appears healthy and responsive, though the rising number of stale-labelled items (6 of 13 tracked items) signals that triage may be slowing for older threads.

## Releases
No new releases were published in this window. The last known version referenced in issues remains **v0.3.1 (2cf030d2)**.

## Project Progress
Today saw productive closing of 7 PRs, spanning bug fixes, features, and housekeeping:

**Merged/Closed:**
- **#3297** – `fix(security): harden remote prompt and exec boundaries` (security hardening: normalized sender metadata, remote exec disabled by default with per-call approval, schema v4 migration for configs)
- **#3296** – `i18n: complete Czech code wrap labels` (community translation completion)
- **#3295** – `fix(channels): prevent SplitMessage hang on oversized fence headers` (crash/hang fix for long code fences in channel messages, with regression tests)
- **#3327** – `feat(telegram): render tables with native rich messages` (functional upgrades: proper GFM/HTML table rendering on Telegram instead of monospaced blocks)
- **#3326** – `fix(web): remove duplicate pnpm lock entries` (build-blocking duplicate keys in lockfile removed)
- **#2132** – `feat(config): support model-specific max_tokens and fix config key co…` (decouples lookup key from runtime ID, enabling per-model max_tokens overrides)
- **#1547** – `fix: merge PR #1466 #1465` (long-standing merge to close out old fix branches)

**Still Open:**
- **#3314** – critical fix for `customAllowPatterns` being ignored in `guardCommand` (default deny patterns took precedence)
- **#3312** – fix to stop turn early on repeated identical tool failure (addresses the silent-loop bug from #3311)

## Community Hot Topics
The most active threads concentrate on two pain points: **execution safety and tool reliability**.

- **#3311 [OPEN] – "Repeated identical tool failure loops silently to max_tool_iterations"** — Only 1 comment, but tied to PR #3312. This describes a real production-impacting failure (agent never responds to user on Telegram), implying high frustration despite low comment counts.
- **#3301 [OPEN] – "/clear and session auto-compression don't work in chats routed to non-default agent via dispatch rules"** — 3 comments. Functionality gaps for routing features; users on Raspberry Pi with Discord/Telegram channels affected.

The lack of reactions or higher comment counts across issues suggests users and maintainers prefer PR-based discussion over issue chatter. The underlying needs: **predictable command behavior per-agent** and **failures that communicate themselves rather than silently burning cycles**.

## Bugs & Stability
Two issues, ranked by severity:

1. **High: Silent tool-failure loops (#3311)** — Agent spins up to `max_tool_iterations` with identical errors, never delivering user an answer. Production impact is severe (unresponsive bot). Fix exists: PR #3312 (open, needs review/merge).
2. **Medium: `/clear` and auto-compression broken for dispatch-routed chats (#3301)** — Session management fails when dispatching to non-default agents. No fix PR visible yet.

Both bugs touch core loop reliability and configuration-routing edge cases, suggesting a focus area for hardening in 0.3.2.

## Feature Requests & Roadmap Signals
Two notable asks in the last 24 hours:

1. **#3298 (closed) – AI Router as OpenAI-compatible provider preset** — Maintainer of AI Router wants a named preset for their service. Closed without merge, but it's a multi-line open-source integration path; likely to surface again once maintainers clarify preset naming conventions.
2. **#3294 (closed) – `/list models` should list all configured models, not just current** — Small UX gap but points toward **broader configuration introspection expectations**.

Predictions for next version (0.3.2): model-specific `max_tokens` support (#2132), Telegram native table rendering (#3327), and hardened remote prompt boundaries (#3297) are merged and likely to ride in the next minor release.

## User Feedback Summary
Real user voices this cycle include:
- **Desire for concise status visibility** — `2suige-coder` expected `/list models` to enumerate all configured models; the command's current single-model output is a cognitive mismatch.
- **Smooth contributor experience** — Czech translator `KrtCZ` submitted a clean i18n PR that was merged; positive signal for localization community.
- **Frustration over silent failures** — `lucapette`'s production report highlights **lack of error surfacing** as a significant dissatisfaction point; users want clear feedback when tools fail.
- **Security-over-usability tradeoff** — Exec-boundary hardening (#3297) forces per-call approval for remote exec; users may push for selective toggles in follow-up feedback.

Satisfaction appears moderate: users are actively contributing fixes but also hitting edge cases around agents, routing, and permissions.

## Backlog Watch
Long-open threads needing maintainer attention:

- **PR #3314 (open, 8 days)** — Critical bugfix for `customAllowPatterns` being ignored; blocker for users relying on custom exec permissions. **Merging this should be a priority.**
- **PR #3312 (open, 9 days)** — Fixes the #3311 loop bug; ties into a severe production issue in the same window. Needs maintainer decision.
- **Issue #3301 (open, 13 days)** — Dispatch-routing bug; lacks a PR or workaround. Will likely attract duplicates if unaddressed.
- **Old merges (#1547) and long-lived model-config PRs (#2132)** — Both mostly closed, but the 5-month lifetime hints that some fixes were blocked for long stretches; possibly worth auditing why trivially-mergeable PRs sat untouched.

Overall backlog hygiene is acceptable but trending toward staleness. The two open bug-fix PRs are critical-path items to keep the next release cycle trustworthy.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-11

## 1. Today's Overview

NanoClaw saw a burst of activity on August 10–11, with 20 pull requests touched in the last 24 hours (10 merged/closed, 10 open) — a significant increase from recent days, indicating an active core-team sprint. The focus is clearly on hardening: session-database integrity, Telegram pairing-code security, DM log privacy, and multi-provider MCP support. Three issues are open, all centered on silent message loss or unrouteable errors — a recurring reliability theme the maintainers are actively addressing. The host-refactor and provider-support threads suggest a period of architectural consolidation after feature velocity earlier in the year.

## 2. Releases

No new releases were cut in this window. The most recent version remains v2 (commit 2d937553, June 6, 2026), with the last tagged release still pending an aggregation of the many fixes and refactors merged since that date.

## 3. Project Progress

Ten pull requests were merged or closed today, spanning fixes, refactors, and docs:

- **Session-DB integrity fix**: [#3228 – fix: deduplicate turn-scoped chat delivery](https://github.com/nanocoai/nanoclaw/pull/3228) — John Mu merged a fix that prevents duplicate chat delivery within a single turn, directly addressing overlapping message-loss scenarios.
- **Privacy hardening**: [#3222 – feat(permissions): add opt-in privacy-safe DM logs](https://github.com/nanocoai/nanoclaw/pull/3222) and [#3215 – fix(permissions): redact DM resolution logs](https://github.com/nanocoai/nanoclaw/pull/3215) — both merged. Zvi Fried's pair of changes gives operators a privacy-safe logging mode for DMs and redacts sensitive resolution details by default.
- **Docs clarity**: [#3216 – docs(hardened-image): note that install_packages covers apt and npm only](https://github.com/nanocoai/nanoclaw/pull/3216) closes a documentation gap that caused user confusion around custom Dockerfile edits.
- **Architecture refactors (all zvi-fried)**: [#3211 – docs(skills): single-responsibility integration rule](https://github.com/nanocoai/nanoclaw/pull/3211), [#3212 – refactor(db): module migration registry](https://github.com/nanocoai/nanoclaw/pull/3212), [#3213 – refactor(channels): register question renderers](https://github.com/nanocoai/nanoclaw/pull/3213), [#3214 – refactor(host): unify module lifecycle hooks](https://github.com/nanocoai/nanoclaw/pull/3214), [#3186 – refactor: host seams for skill-owned capabilities](https://github.com/nanocoai/nanoclaw/pull/3186) — a systematic cleanup of the host/module lifecycle, channel rendering, and database migration scaffolding. These are preparatory refactors signaling a more disciplined extension API ahead.
- **Environment cleanup**: [#3219 – Telegram and container env](https://github.com/nanocoai/nanoclaw/pull/3219) closed, fixing an environment plumbing issue for Telegram in containers.

Collectively, these merges advance the project toward a more maintainable, privacy-conscious core and prepare the ground for the streamable-HTTP MCP work awaiting in open PRs.

## 4. Community Hot Topics

The highest-engagement item this window is a long-lived issue that has now become a thematic cluster:

- **[#3075 – Silent log loss + inbound message duplicate-insert errors after long uptime](https://github.com/nanocoai/nanoclaw/issues/3075)** — 1 comment; open since July 17 and still active. The reporter describes two coupled failures: logs silently stop and inbound messages throw duplicate-insert errors after extended uptime. Commenters have linked this to the session-db primary-key architecture — the same root cause now addressed by PR #3224 (still open) and #3228 (merged).
- **[#3226 – Inbound messages silently dropped when a platform reuses a message id](https://github.com/nanocoai/nanoclaw/issues/3226)** — filed by core team member dweekly, zero comments because it was immediately followed by fix PR [#3224](https://github.com/nanocoai/nanoclaw/pull/3224). The issue and PR form a tight loop: dweekly identified the root cause, opened the bug, and proposed the fix in the same session.
- **[#3223 – Scheduled-task turns that error produce an unroutable error message](https://github.com/nanocoai/nanoclaw/issues/3223)** — zero comments; the reporter notes that scheduled-task failures produce a chat message with no routing fields, so the operator never sees the error. No PR exists yet — this is a candidate for the next sprint.

The underlying need across all three: **operators cannot afford silent failure**. Whether it's a dropped inbound message, a lost log line, or an unroutable error, the community is signaling that observability and delivery guarantees are the #1 reliability concern right now.

## 5. Bugs & Stability

Three distinct bugs are on the table, ranked by severity:

1. **HIGH — Silent inbound message loss on message-ID reuse** ([#3226](https://github.com/nanocoai/nanoclaw/issues/3226), open, no comments). A platform restart/reuse of a message ID causes the primary-key insert to throw, and the inbound message is dropped *before* the agent ever sees it. User-visible as "the agent ignored me." **Fix exists**: PR [#3224 – fix(session-db): preserve inbound messages across platform ID reuse](https://github.com/nanocoai/nanoclaw/pull/3224) is open and awaiting review.

2. **MEDIUM-HIGH — Silent log loss + duplicate-insert after long uptime** ([#3075](https://github.com/nanocoai/nanoclaw/issues/3075), open, 1 comment). Long-running instances lose logging silently and begin throwing duplicate-insert errors. Related to #3226's root cause (session-db key collisions) but broader, implying a leak or state corruption over time. No dedicated fix PR yet; #3228's turn-scoped deduplication may partially mitigate, but the logging loss suggests a separate issue.

3. **MEDIUM — Unrouteable errors from scheduled-task turns** ([#3223](https://github.com/nanocoai/nanoclaw/issues/3223), open, 0 comments). Scheduled tasks that throw generate a chat message with no routing fields, so the error is silently dropped. The operator never learns the task failed. **No fix PR yet**; the reporter notes task messages carry no routing fields "by design," so the fix likely requires a routing-fallback mechanism or a distinct error channel.

A second Telegram security fix is pending review: [#3225 – harden pairing code generation and store permissions](https://github.com/nanocoai/nanoclaw/pull/3225) (CSPRNG + permission hardening), plus an open fix at [#3229](https://github.com/nanocoai/nanoclaw/pull/3229) covering the same area from a different author.

## 6. Feature Requests & Roadmap Signals

The strongest roadmap signal is **[PR #3092 – feat: support remote Streamable HTTP MCP servers](https://github.com/nanocoai/nanoclaw/pull/3092)**, opened July 19, still open, now joined by **[PR #3221 – remote Streamable HTTP MCP servers for codex and opencode](https://github.com/nanocoai/nanoclaw/pull/3221)** (core-team, opened August 10). This is a two-part feature: engine + Claude provider support (#3092) and then wiring the same config shape into codex and opencode providers (#3221). The fact that the core team is actively building follow-on support suggests #3092 is close to merge — expect this in a near-term release (v2.1 or v3).

Other signals:

- **[PR #3220 – Agent templates become Agent Plugins 1.0.0](https://github.com/nanocoai/nanoclaw/pull/3220)** (core-team, open). This renames and re-architects agent templates into a versioned plugin format, with stamp-time symlink/caps/secret hardening. Combined with [#2909 – template setup flow in the wizard](https://github.com/nanocoai/nanoclaw/pull/2909), the project is maturing its agent-provisioning story significantly. A breaking change is implied (template → plugin format), so watch for migration notes.
- **[PR #3218 – feat(cli): accept bounded JSON from stdin](https://github.com/nanocoai/nanoclaw/pull/3218)** (open). A generically useful CLI enhancement allowing structured input without disturbing the request frame — likely to land soon and enable more scriptable operator workflows.
- **[PR #3193 – fix(telegram): update Chat SDK for rich messages](https://github.com/nanocoai/nanoclaw/pull/3193)** (open). Telegram rich-message support is being modernized; this plus the pairing-code hardenings suggest Telegram is getting a quality pass.

**Prediction for the next release**: Streamable HTTP MCP support (engine + all three providers) and the Agent Plugin migration are the two headline features most likely to land together, plus the session-db durability fixes. If those merge this week, a v2.1 tag is plausible by month-end.

## 7. User Feedback Summary

The dominant voice this window is **frustration with silent failures**. Three separate issues all describe the same class of pain: "nothing reaches the agent," "no user-visible sign anything was lost," and "the operator never learns the task failed." This is a reliability trust issue — operators cannot tell whether the system is working or quietly degrading.

Secondary themes:

- **Long-uptime degradation** (#3075): users report the system works fine for days, then starts dropping messages and logs without warning. This erodes confidence in unattended deployments.
- **Documentation gaps** (addressed by #3216): the hardened-image guide implied `install_packages` was a general-purpose hook; the merge clarifies it only handles apt/npm, preventing a class of "why did my custom Dockerfile change vanish" confusion.
- **Privacy awareness** (addressed by #3222/#3215): a user explicitly requested the ability to run DMs with non-identifying logs — a signal that NanoClaw is being used in privacy-sensitive deployments (healthcare, legal, enterprise).

On the positive side, the core team's responsiveness this week (bugs → fixes within hours, e.g., #3226 → #3224) is a strong satisfaction signal; users filing issues see rapid engagement.

## 8. Backlog Watch

Items that need maintainer attention, ranked by how long they've waited and how central they are:

- **[#3075 – Silent log loss + inbound duplicate-insert errors after long uptime](https://github.com/nanocoai/nanoclaw/issues/3075)** — open since July 17 (25 days), 1 comment. The core team has acknowledged the related root cause in #3226/#3224, but this issue covers a broader failure (log loss). Needs either a dedicated fix or explicit closure as a duplicate with a pointer to #3224's scope.

- **[#3092 – Remote Streamable HTTP MCP servers](https://github.com/nanocoai/nanoclaw/pull/3092)** — open since July 19. It now has a dependent PR (#3221), so the merge path is actively being built, but given how long this has waited, a reviewer should be explicitly assigned and a merge target communicated.

- **[#2909 – Template setup flow in wizard and first-agent stamping](https://github.com/nanocoai/nanoclaw/pull/2909)** — open since July 2 (40 days). This is part 2 of the agent-template work, now likely to be reshaped by #3220's plugin-format migration. Maintainers should reconcile the two PRs to avoid duplicate/conflicting work — the longer this sits, the more painful the rebase.

- **[#3193 – Telegram Chat SDK update for rich messages](https://github.com/nanocoai/nanoclaw/pull/3193)** — open since August 6; no comments on the PR. A straightforward dependency update that's been silent for 4 days; a maintainer nudge (or close) would help.

- **[#3223 – Unrouteable scheduled-task errors](https://github.com/nanocoai/nanoclaw/issues/3223)** — filed August 10, no response yet. This is a real bug with no PR; it deserves triage and, ideally, a fix in the same sprint as the other delivery-guarantee work.

---

*Digest generated 2026-08-11 from GitHub activity in the preceding 24 hours.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for 2026-08-11.

---

# NullClaw Project Digest — 2026-08-11

## 1. Today's Overview
NullClaw is currently in a **low-activity maintenance phase**. In the last 24 hours, only one issue was closed and one dependency update PR was touched, with zero new releases or merges. The project appears stable but is not currently shipping new features, with the main focus being on routine housekeeping (Docker base image upgrades). The closure of a long-standing feature request (#700) signals that the maintainers are actively triaging and finalizing the backlog, even if bandwidth is limited. Overall, project health is stable, with a clear emphasis on incremental infrastructure updates rather than rapid feature iteration.

## 2. Releases
**None.**
No new versions were released in the last 24 hours. The most recent release remains unspecified.

## 3. Project Progress
There were **no merged pull requests** in the last 24 hours. However, the **closure of Issue #700** ([link](https://github.com/nullclaw/nullclaw/issues/700)) represents significant progress on the `a2a_call` client tool. This feature, originally requested in March, adds client-side A2A (Agent-to-Agent) protocol support, allowing NullClaw agents to send `message/send` JSON-RPC requests to remote agents. The closure suggests the implementation has either been completed and merged in a prior cycle, or the maintainers have decided to archive the request.

## 4. Community Hot Topics
The most active item is the now-closed Issue **#700: "Add a2a_call client tool for calling remote agents"** ([link](https://github.com/nullclaw/nullclaw/issues/700)). With 1 comment and 1 👍 reaction, it is the primary focus of community engagement today. The underlying need here is **interoperability**—users want to run multiple NullClaw instances (e.g., a public-facing "doorman" and a private "personal" agent) and have them communicate seamlessly using the standard A2A protocol. The lack of a client-side implementation was a functional gap in this multi-agent workflow.

## 5. Bugs & Stability
**No new bugs, crashes, or regressions** were reported or updated in the last 24 hours. The project appears to be in a stable state with no immediate stability concerns on the horizon.

## 6. Feature Requests & Roadmap Signals
The closing of Issue **#700** ([link](https://github.com/nullclaw/nullclaw/issues/700)) is the strongest roadmap signal today. It indicates that **full A2A protocol support (both server and client) is now a reality**. Given that the community explicitly requested this in March and it has now been resolved, future updates will likely focus on enhancing this client capability—such as adding support for streaming responses, tool discovery on remote agents, or security/authentication layers for inter-agent communication. We predict that these A2A enhancements will be a core part of the next minor version release.

## 7. User Feedback Summary
The primary user request (Issue #700) highlights a specific pain point: **the inability to federate multiple agent instances**. The user (georgeglarson) successfully built a workaround themselves, indicating a high level of technical proficiency within the community and a desire for more built-in "mesh" capabilities. The single 👍 reaction suggests moderate interest, but the fact that the user took the time to develop the feature themselves shows strong commitment to the use case. The overall sentiment is neutral-positive, with no negative feedback or complaints logged in this period.

## 8. Backlog Watch
**PR #956: "ci(deps): bump alpine from 3.23 to 3.24"** ([link](https://github.com/nullclaw/nullclaw/pull/956)) is the item most in need of maintainer attention. This Dependabot PR has been open for **nearly two months** (since June 15) without being merged. While a base image bump is low-risk, prolonged delays can lead to security vulnerabilities or compatibility drift. This should be reviewed and merged promptly. No other long-unanswered issues or PRs appear to require immediate attention.

---

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-11

## 1. Today's Overview

IronClaw is in a period of intense, high-quality maintenance and feature velocity. Activity is exceptionally high: 50 issues and 50 PRs were updated in the last 24 hours, with a nearly even split between open and closed items, indicating a well-balanced flow of new work and completed work. A critical patch candidate, `ironclaw-v1.1.1-rc.1`, was released to address urgent channel delivery, MCP compatibility, and WebUI streaming stability issues. The project is showing strong discipline in auditing its own architecture, with multiple issues filed by core maintainer BenKurrek specifically to tighten CI gates, ratchets, and dependency boundaries after deep documentation and soundness audits. This "know what green means" approach signals a mature project focused on long-term maintainability over raw feature count.

## 2. Releases

**ironclaw-v1.1.1-rc.1** (2026-08-10) — This is an urgent patch candidate for the 1.1 line. Key focus areas:
- **Channel delivery and pairing**
- **IronHub/custom MCP compatibility**
- **WebUI streaming stability**
- **Durable retrieval**
- **Safe upgrades** from both supported stable predecessors

**Migration Note:** The release notes explicitly call out that users upgrading from 1.0.0 must **stop all writers** before performing the upgrade, indicating a breaking change or necessary quiesce for data safety.

## 3. Project Progress

The last 24 hours saw 17 PRs merged or closed, with significant feature and fix work landing:

- **📦 Package Installation** (PR #7442, closed): Installs every companion file published for an IronHub skill, superseding #7076. Includes normalized-path validation, digest verification, and aggregation. Notably, this is a takeover that preserves the original author's commit, showing good open-source collaboration.
- **🔄 Steering Replay Dedup** (PR #7336, closed): `fix(loop-host)` preserves a bounded durable identity window for consumed steering messages, preventing duplicate model iterations and assistant replies from delayed queued-message replays.
- **💬 Rich Working Indicator** (PR #7446, closed): Replaces the single "Ironclaw is thinking..." line with a rotation of warm notices, and adds reactions, failure states, and progress nudges to Slack and Telegram channel runs.
- **📝 Docs Truth Audit** (PR #7376, open): Extends the `check-guidance.py` path-reference gate to cover the `docs/` surface, which previously had zero path validation. This is part of a larger "doc-truth" initiative.

## 4. Community Hot Topics

**#7137 — Live-Canary Artifact Bloat (12 comments)**
[Issue Link](https://github.com/nearai/ironclaw/issues/7137) — The live-canary workflow uploads 700MB–1.5GB of artifacts per shard, totaling over 5GB. This is an infrastructure efficiency problem that slows downloads and burns GitHub Actions storage quota.

**#7145 — Extension Host Re-layer Sizing (4 comments)**
[Issue Link](https://github.com/nearai/ironclaw/issues/7145) — A closed issue that succeeded #7092, discussing how the `ironclaw_extension_host` `products → loops` flip should be sized. The key insight: file count is not the constraint; the four-port residue is.

**#6257 — PDF MIME Type Error (3 comments)**
[Issue Link](https://github.com/nearai/ironclaw/issues/6257) — Users report `Invalid value (attachments.mime_type)` when sending/generating PDF files. This is an active user-facing bug that has been open since July 19.

**#7147 — Architecture Ratchet Drift (3 comments)**
[Issue Link](https://github.com/nearai/ironclaw/issues/7147) — Three open PRs hold three different values of the same architecture baseline, exposing untracked slack in the shrink-only ratchets.

**#5882 — Slack Reconnect Auth Breakage (3 comments)**
[Issue Link](https://github.com/nearai/ironclaw/issues/5882) — Repeated Slack reconnect attempts leave the auth flow in a permanently broken state, requiring extension reinstall. This is a QA-flagged P2 bug.

## 5. Bugs & Stability

**High Severity:**
- **#7447 — Agent tarpit on tool-call budget** ([Issue](https://github.com/nearai/ironclaw/issues/7447)): Agent gets stuck in redundant fetch-retry loops (4 near-duplicate GitHub queries) instead of paginating, burning through the tool-call budget and failing tasks. This is a quality-of-result regression.
- **#5882 — Slack auth permanent breakage** ([Issue](https://github.com/nearai/ironclaw/issues/5882)): Repeat reconnects break the auth flow irrecoverably. **Fix PR #7475 exists** (open) that addresses the root cause by not collapsing "delivered with no vendor ref" into "not delivered."

**Medium Severity:**
- **#6257 — PDF MIME type rejection** ([Issue](https://github.com/nearai/ironclaw/issues/6257)): PDFs rejected with `Invalid value (attachments.mime_type)`. Likely a validation rule rigidity issue.
- **#7471 — Process lease expirations** ([Issue](https://github.com/nearai/ironclaw/issues/7471) and [PR](https://github.com/nearai/ironclaw/pull/7471)): Hosted runs die with `lease_expired` because the process-journal heartbeat shares a max-size-2 Postgres pool with data-plane traffic, which can starve it during bursts. The PR isolates a dedicated heartbeat pool.

**Low/Structural:**
- **#7470 — Unprojected thread index rows invisible** ([Issue](https://github.com/nearai/ironclaw/issues/7470)): Threads with durable rows but no ordered-projection metadata are absent from the sidebar's `list_threads`. Fix PR #7470 is open.
- **#7473 — Duplicate connect-nudge notices** ([Issue](https://github.com/nearai/ironclaw/issues/7473)): The anti-duplicate throttle releases when a notice was genuinely delivered but without a vendor ref, causing a second nudge. **Fix PR #7475 is open.**

## 6. Feature Requests & Roadmap Signals

**Strong Signals for v1.3.0:**
- **#3762 — AGENTS.md web UI edits. . .** ([Issue](https://github.com/nearai/ironclaw/issues/3762)), a suggested P1: Editing identity files in the web UI doesn't update the system prompt. This has been open since May — the customer-facing impact is high.
- **#7046 — Admin configuration via AI chat** ([Issue](https://github.com/nearai/ironclaw/issues/7046)): Configure tools, channels, and extensions from chat — a major UX initiative aligned with channel-first onboarding (#7044).
- **#7038 — AI-first Design System** ([Issue](https://github.com/nearai/ironclaw/issues/7038)): Storybook-backed design system with theming and a full proposal package (PR #7257) — signals an investment in WebUI polish.

**Next-Generation Extensions (targeting 2026-08-14):**
- **#7354 — Extensions vNext** ([Issue](https://github.com/nearai/ironclaw/issues/7354)): Web push notifications, rich messaging, delegated Telegram user sessions, and a production-ready Signal channel. The Telegram linked-device work is already landing (PR #7464).

**Architectural Signals:**
- **#7467 — Profile-agnostic durable state** ([Issue](https://github.com/nearai/ironclaw/issues/7467)): Storage indexed by deployment profile creates dangerous data "disappearance" on profile change. Fix PR #7456 is open — this is high risk and high value.
- **#7151 — Composition budget poisoning** ([Issue](https://github.com/nearai/ironclaw/issues/7151)): A share-based gate on the god crate is gameable by feature inflow, allowing re-accretion. A systemic CI soundness issue.

## 7. User Feedback Summary

**Pain Points:**
- **Setup friction is real.** [#6834](https://github.com/nearai/ironclaw/issues/6834) (Slack setup fails) and [#5882](https://github.com/nearai/ironclaw/issues/5882) (reconnect breaks auth) both point to Slack onboarding as a weak spot.
- **Artifact generation is unreliable.** [#6257](https://github.com/nearai/ironclaw/issues/6257) — PDF uploads failing is a concrete blocker for users who want to share documents.
- **Agent loops are wasteful.** [#7447](https://github.com/nearai/ironclaw/issues/7447) — the agent's redundant query loops burn budgets and produce no better outcome, frustrating users watching from WebUI.
- **Configuration is undiscoverable.** The push for chat-first admin (#7046) and channel-first onboarding (#7044) reflects feedback that the blank-slate WebUI doesn't guide users to value.

**Positive Signals:**
- The project's response to **#7246/#7247/#7294** (agent asserting unverified state) shows a commitment to making agent behavior honest about what it knows — this addresses trust in AI agents.
- The dense release cadence and rapid patch landing (e.g., #7336, #7446) indicate the team is responsive to channel reliability feedback.

## 8. Backlog Watch

- **#3762 — AGENTS.md edits not picked up** ([Issue](https://github.com/nearai/ironclaw/issues/3762)): Open since **May 18**, a suggested P1 with high user impact. The issue is clearly scoped; it needs a maintainer to own it. This is a candidate for v1.3.0 but has sat for three months.
- **#6257 — PDF MIME type rejections** ([Issue](https://github.com/nearai/ironclaw/issues/6257)): Open since **July 19**. This is a simple user-facing bug with low complexity; silence here may indicate prioritization issues.
- **#5101 — CI cargo-component installer reuse** ([Issue](https://github.com/nearai/ironclaw/issues/5101)): PR open since **June 20**, flagged as `contributor: new` and `scope: ci`. This is a small, safe refactor that has languished. It relates directly to #7137 artifact bloat; maintainers may want to review and shepherd this through.
- **#6994 — OOBE automation-tasks prototype** ([PR](https://github.com/nearai/ironclaw/pull/6994)): A code-free design+integration-plan package that's been open since **August 1**. The WebUI redesign direction may be blocked on design decisions; worth a maintainer nudge.

---

**Overall Health:** Excellent. The project is self-aware, with active architecture audits feeding a steady stream of corrective issues. The 1.1.1-rc.1 release cadence and the density of "risk: low" PRs indicate a stable core with active hardening. The main risks are the accumulation of long-standing user-facing bugs (#3762, #6257) and the CI artifact bloat that slows down the development loop itself.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-08-11**, generated from the provided GitHub data:

---

## 1. Today's Overview
**Activity Level: Very High.** The project saw intense development on **2026-08-10/11**, with **20 pull requests merged or closed** and **14 remaining open**. The primary focus was on stabilizing the **OpenClaw gateway** (fixes for tool-loop guards, provider failures, and Python runtime shims) and enhancing the **Cowork UI** (file attachment cards, context menus, and keyboard shortcuts). The dependency update pipeline (Dependabot) processed a backlog of major version bumps (Vite, React, React-DOM), indicating proactive maintenance. Only one issue was active, which was closed as stale, suggesting the bug backlog is being cleared. Overall, this is a healthy, fast-moving project finally consolidating stability after a feature push.

## 2. Releases
**None.** No new releases were published in the last 24 hours. The last known version remains at **2026.4.1** (referenced in the Issue). Note: The project is merging major dependency upgrades (Vite 8, React 19), which will likely be included in the next official release.

## 3. Project Progress
Merged/Closed PRs (20) focused on significant feature completion and critical fixes.

- **Cowork UX Enhancements:**
   - **#2471 [Merged]:** Render submitted non-image file attachments as clickable, rich file-type cards instead of raw text.
   - **#2472 [Merged]:** Added activity group collapse functionality for the Cowork UI.
   - **#2468 [Merged]:** Refactored and unified streaming loading indicators into a single component.
   - **#2469 [Merged]:** Added a "collapse-agent-tasks" shortcut and allowed modifier shortcuts while typing.
- **Stability & Core Logic Fixes:**
   - **#2454 [Merged]:** Fixed the OpenClaw tool-loop guard so it no longer kills legitimate polling operations.
   - **#2470 [Merged]:** Addressed a critical bug where late chat errors were swallowed, hiding real provider/LLM runtime failures (e.g., idle timeout failover).
   - **#2467 [Merged]:** Repaired stale/outdated pip shims on Windows Python runtime upgrades.
   - **#2466 [Merged]:** Fixed a renderer init IPC stall and added retry logic.
- **Dependency & Tooling:** Closed out multiple stale Dependabot PRs (e.g., Vite 8.0.13, React-DOM 19.2.6, plugin-react 6.0.1) and opened fresh ones for the latest versions.

## 4. Community Hot Topics
The `qwen-portal-auth` plugin bug was the only active issue in the last 24 hours, but it wasn't heavily discussed (only 2 comments). The real activity driver is the PR pipeline, particularly from contributor **fisherdaddy**, who dominates the fix/feature work.

- **Open [PR #2452]:** Fix to preserve the provider prefix for slashed model IDs (e.g., `deepseek-ai/DeepSeek-V4-Flash`). This addresses a parsing ambiguity between the backend and renderer.
- **Open [PR #2473]:** A substantial feature adding a rich right-click context menu for local file links (open-with, save-as, copy-path, reveal-in-folder). This signals a push toward desktop-app parity.

## 5. Bugs & Stability
While the `qwen-portal-auth` issue was closed as stale, the PR activity reveals (and fixes) recent temporary regressions.

- **Resolved – High:** **Late Chat Error Swallowing** ([PR #2470]) – This was a silent failure mode where real provider failures crash the session without user notification. Fixed.
- **Resolved – Medium:** **Tool-Loop Guard Hanging** ([PR #2454]) – The guard was killing legitimate polling, potentially causing interrupted agent workflows. Fixed.
- **Resolved – Medium:** **Windows Pip Shims** ([PR #2467]) – Runtime upgrades could leave broken pip shims, breaking environment setups. Fixed.
- ****Resolved – Medium:** **Renderer IPC Stall** ([PR #2466]) – The renderer could hang during initialization; retry logic was added.
- **Closed as Stale:** **[Issue #1243]** reported persistent gateway restarts every 5-20 minutes due to config loops. This was closed but is a high-severity issue that may require re-opening if it resurfaces.

## 6. Feature Requests & Roadmap Signals
There are no direct user feature requests in this batch, but the merged PRs reveal the roadmap direction:

- **Desktop-App File Management:** The new context menu ([PR #2473]) and file attachment cards ([PR #2471]) show a clear focus on making the web UI feel like a local desktop application with full file system integration.
- **Asynchronous Session Management:** The "collapse-agent-tasks" and shortcut enhancements ([PR #2469]) suggest improvements to managing long-running multi-agent sessions.
- **Model Identifier Flexibility:** The fix for slashed model IDs ([PR #2452]) indicates support for a wider variety of model providers and naming conventions, crucial for custom domains.

## 7. User Feedback Summary
Direct user feedback (from issues) is sparse this period, but some signals exist:

- **Pain Point (Historical):** Users on Windows were experiencing severe instability with `qwen-portal-auth` causing frequent restarts ([Issue #1243]). While closed as stale, the volume of recent fixes to the OpenClaw layer suggests maintainers are actively rooting out these instability causes.
- **UX Satisfaction:** The heavy investment in UI/UX (file cards, context menus, shortcuts) suggests maintainers are prioritizing polish and feel valued by the community.
- **Community Structure:** The project appears to be largely driven by a small core team (e.g., `fisherdaddy`) rather than a wide external contributor base, given the concentration of commits.

## 8. Backlog Watch
These items require maintainer attention or monitoring:

- **[Issue #1243] [Stale] Bug: `qwen-portal-auth` Gateway Restart Loop** – Closed as stale but previously caused major user disruption (reboots every 5-20 min). Given the similarities to recent fixes, maintainers should ensure a regression test exists.
- **[PR #2452] [Open] Provider Prefix Fix** – Critical for correct model identification in custom setups. It has been open for 4 days; should be prioritized for merge to avoid state corruption.
- **Dependency Upgrade Cluster (Pr #2465, #2464, #2463, #2462, #2461, #2460, #2459)** – A wave of major version bumps (Vite 8.2, React 19.2.8, Mermaid 11) is pending. These carry breaking-change risks; the team should ensure thorough QA before accepting them.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-11

## 1. Today's Overview
Moltis is in a **quiet but active stabilization phase**. Over the last 24 hours, the project saw 3 open issues (no closures) and 1 open PR (no merges), with **no new releases**. Activity is concentrated on the **Apple Container backend**, which accounts for 2 of the 3 open bugs, suggesting recent work on that backend may have introduced regressions or exposed gaps. The single open PR (#531) — a large browser viewing UI feature — has been in flight for over four months and was updated yesterday, indicating continued (if slow) progress on a significant user-facing capability. Overall, the project is healthy but would benefit from a focused bug-fix push on the Apple Container path.

## 2. Releases
**No new releases in the last 24 hours.** The most recent release remains the prior version (not specified in this data window). No migration notes, breaking changes, or changelog entries to report.

## 3. Project Progress
**No PRs were merged or closed in the last 24 hours.** The only active PR is:

- **[#531 — feat(browser): interactive browser viewing UI with CDP screencast](https://github.com/moltis-org/moltis/pull/531)** *(updated 2026-08-10)* — This long-running PR (created March 31) adds live browser session viewing via CDP screencast, mouse/keyboard/scroll interaction, session history with action logs, and per-agent cookie isolation. Its update yesterday suggests the author is actively iterating, likely in response to review feedback. This will be a significant UX upgrade for the Settings > Browser page when it lands.

## 4. Community Hot Topics
The most active discussion in the last 24 hours is:

- **[Issue #1185 — [Bug]: Apple Container 1.x sandbox starts but Moltis treats it as not running](https://github.com/moltis-org/moltis/issues/1185)** *(author: mikz, created 2026-08-08, 3 comments, updated 2026-08-10)* — This is the **only issue with substantive discussion** in the window. The core problem: the sandbox process is actually running, but Moltis's health-check/detection logic incorrectly reports it as down. The 3 comments suggest maintainers or community members are actively diagnosing. The underlying need is **reliable backend state detection** — a critical trust factor for users running containerized sandboxes.

The other two issues (#1188, #1189) are brand new (created 2026-08-10) with zero comments, so they haven't yet generated discussion.

## 5. Bugs & Stability
Three bugs were reported or updated in the last 24 hours, ranked by severity:

1. **High — [Issue #1185: Apple Container sandbox false-negative detection](https://github.com/moltis-org/moltis/issues/1185)** *(updated 2026-08-10, 3 comments)* — The tool reports a running sandbox as not running, which likely breaks workflow automation and user trust. No fix PR exists yet. This is the most severe because it's a **correctness bug in core state management**, not just a missing feature.

2. **Medium — [Issue #1188: Resource limits not applied for apple-container backend](https://github.com/moltis-org/moltis/issues/1188)** *(created 2026-08-10, author: holgzn)* — Resource limits (CPU/memory) are silently ignored on the Apple Container backend. This is a **safety/compliance concern** for users relying on caps to prevent runaway resource consumption. No fix PR yet.

3. **Low-Medium — [Issue #1189: Sandbox build failing due to wrong gogcli GitHub URL](https://github.com/moltis-org/moltis/issues/1189)** *(created 2026-08-10, author: holgzn)* — An infrastructure/build issue: a dependency (gogcli) is referenced at an incorrect GitHub URL, breaking sandbox builds. Likely a straightforward fix once the correct URL is identified. No fix PR yet.

**Pattern:** Two of the three bugs target the Apple Container backend, and two are from the same reporter (holgzn), suggesting that backend is receiving fresh user adoption but also has rough edges.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed in the last 24 hours. However, the active PR **[#531 (browser viewing UI)](https://github.com/moltis-org/moltis/pull/531)** signals the next major feature on the roadmap: **interactive browser sessions with CDP-based live screencasting and per-agent cookie isolation**. Given it was updated yesterday after four months, a merge may be imminent (weeks, not days). This will likely appear in the next minor release (e.g., 1.x).

Secondary roadmap signal: the cluster of Apple Container issues suggests the backend is in active use; expect a **stabilization-focused patch release** (e.g., 0.x.y or 1.x.y) addressing issues #1185 and #1188 before the browser feature ships.

## 7. User Feedback Summary
Real user pain points surfaced in the last 24 hours:

- **Broken trust in backend state reporting** (#1185): Users cannot rely on Moltis's status output when it contradicts reality (sandbox runs but UI says otherwise). This erodes confidence in automation and UI-driven workflows.
- **Missing resource guarantees** (#1188): Users expect declared resource limits to be enforced; silent ignoring could lead to host resource exhaustion in multi-sandbox setups.
- **Build friction** (#1189): A simple misconfigured dependency URL breaks sandbox builds; this reflects a need for more robust CI/dependency pinning in the project's build tooling.

Satisfaction signals: The sustained activity on PR #531 and the fact that users are actively testing Apple Container (rather than abandoning it) suggest general engagement is positive, but the backend needs a hardening pass.

## 8. Backlog Watch
The following items need maintainer attention but have not seen recent activity:

- **[PR #531 — Browser viewing UI (open since 2026-03-31)](https://github.com/moltis-org/moltis/pull/531)** — Over 4 months in review. Updated yesterday, which is a good sign, but this is a large PR that will need focused review bandwidth. Maintainers should prioritize a review session to avoid further staleness.
- **[Issue #1185 (Apple Container false-negative)](https://github.com/moltis-org/moltis/issues/1185)** — Has 3 comments but no assignee or linked fix PR visible in the data. If unresolved, this will accumulate user frustration as it blocks reliable sandbox usage.
- **No other long-pending items were visible** in the 24-hour window; the backlog appears generally well-maintained apart from the two items above.

---

*Generated from GitHub data as of 2026-08-11. All links refer to [moltis-org/moltis](https://github.com/moltis-org/moltis).*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the GitHub data provided for CoPaw (github.com/agentscope-ai/CoPaw, with the agent project referred to as QwenPaw), here is the project digest for 2026-08-11.

---

### 1. Today's Overview

CoPaw (QwenPaw) is experiencing a high level of activity as it approaches a major release milestone (v2.1.0). The project saw substantial engagement in the last 24 hours, with 40 issues and 50 PRs updated, indicating a vibrant community and an active development cycle. While no new official releases were cut, the repository is buzzing with pre-release preparations, including a PR dedicated to finalizing v2.1.0 release notes. The community is actively reporting bugs from the current v2.0.1 stable and v2.1.0 beta versions, while the maintainer team is simultaneously merging fixes for provider compatibility, memory system improvements, and developer experience enhancements. Overall, the project demonstrates a healthy, fast-moving development cadence focused on stabilizing new features and addressing a wide range of user feedback.

### 2. Releases

No official new releases were published today (2026-08-11). The most recent version remains the v2.1.0 beta cycle (v2.1.0b2), which is currently being prepared for general availability. A PR (#6875) titled "chore: update release notes for v2.1.0" is open, indicating an imminent stable release.

### 3. Project Progress

Based on the merged/closed PRs today, the team is focusing on hardening the platform and resolving critical bugs.

- **Provider Compatibility & Sanitization:** PR #6809 ("fix(providers): sanitize Chat Completions content for strict providers") was closed, directly addressing issues with strict OpenAI-compatible providers like StepFun that were rejecting requests due to internal runtime fields. This is a key fix for interoperability.
- **Config Resilience:** PR #6615 ("fix(config): handle corrupted agent config and invalid JSON in load_agent_config") was closed, adding robustness against corrupted user configuration files, which prevents crashes and cryptic errors.
- **Memory System Enhancement:** PR #6398 ("feat: add reranker support for ReMe memory search (backend)") was closed. This is a significant backend feature for the ReMe memory subsystem, allowing for improved search quality through re-ranking.
- **Console Usability:** PR #6878 ("feat(console): add hidden-folders toggle to project directory picker") was closed, adding a new UI control to the file picker to simplify navigating between hidden and non-hidden files.

### 4. Community Hot Topics

The most active discussions highlight concerns around the Docker experience, the stability of MCP tool calls, and the new memory system's reliability.

- **Docker Version Instability (Issue #6782):** The most commented-on issue (9 comments) is a bug report from `Sakura7301` stating that in the 2.0.1 Docker version, the plugin and app markets show as "under maintenance" and are unusable. This is a significant blocker for Docker users and likely the most critical community concern today. [Link](agentscope-ai/QwenPaw Issue #6782)
- **MCP Tool Failures (Issue #6405, #6839):** Two related issues are in the top 10: "Tool notfound" errors after upgrading to 2.0 (4 comments) and a bug where MCP tool calls incorrectly type numeric-looking strings, causing failures (3 comments). This suggests that while the MCP tooling is powerful, it remains a fragile point for users.
- **OpenAI Responses API Issues (Issue #6803, #6811, #6821):** A cluster of issues revolves around the OpenAI Responses API integration, including a closed bug about rejected content types, an open bug about continuation summaries ignoring `disable_thinking`, and an open bug about `reasoning_content` not being relayed back correctly.

### 5. Bugs & Stability

Multiple bugs and stability concerns were reported today, ranked by severity:

- **High: SIGBUS Crash on macOS (Issue #6814):** A crash with a `SIGBUS` signal in SQLite WAL mode while opening the Scroll history database on macOS. This is a hard crash that prevents the app from starting or loading history. No fix PR is currently referenced. [Link](agentscope-ai/QwenPaw Issue #6814)
- **High: Console UI Crash with Chinese IME (Issue #6885):** A new bug in v2.1.0b2 where using a Chinese IME during an agent run makes the message queue completely unusable. This severely impacts a large segment of the user base. A fix PR, #6889 ("fix(console): preserve textarea target for IME events"), is already open. [Link](agentscope-ai/QwenPaw Issue #6885)
- **High: Idle CPU Usage Spike (Issue #6828):** Users report the console frontend repaints continuously at idle, holding the CPU at ~20%, causing UI jank. The report points to infinite CSS animations as the root cause. [Link](agentscope-ai/QwenPaw Issue #6828)
- **Medium: Memory/Agent Clogging (Issue #6780):** Users report that after 2.0.1 is idle for tens of minutes, it freezes and requires a process restart. [Link](agentscope-ai/QwenPaw Issue #6780)
- **Medium: Platform-Specific Plugin Failures (Issue #6806, #6807):** The `qwenpaw-creator` plugin fails on Windows, with the inability to save model configs ("Internal Server Error") and issues with video generation and publishing.
- **Medium: Incorrect Timing Display (Issue #6826):** The UI incorrectly displays the assistant's reply time, showing only seconds even when the actual thinking time takes minutes.

### 6. Feature Requests & Roadmap Signals

The community is pushing for more granular control and observability.

- **In-Chat Observability (Issue #4237):** A long-standing request (created 2026-05-12) for a panel to see, kill, and extend timeouts for running shell commands. This is a strong signal for enhanced agent control and debugging.
- **Memory System Enhancements (Issue #6840, #6841):** Users are actively inquiring about the roadmap for the ReMe4 memory architecture (Auto-Link, tri-modal search). An issue also requests more resilience in the Auto-Dream integration, where one failure unit marks the entire task as an error. A fix PR (#6884) for this resilience issue is already open.
- **UI/UX Refinements (Issue #6876, #6585, #6881):** There is a clear desire for a cleaner UI. Requests include making the background task panel collapsible, adding a toggle to disable the dynamic character-count display in the chatbox, and auto-refreshing session titles after memory updates.
- **Installation Reliability (Issue #6810):** A detailed report about installer failures on Windows due to file-locking issues during updates. This points to a need for more robust installer logic.

### 7. User Feedback Summary

User pain points this week revolve around the friction between the powerful new features and their stability.

- **Pain Points:** The most significant issues are instability in specific environments (Docker, macOS, Windows), broken MCP tooling, and the performance of the console UI. Users are also frustrated by seemingly simple issues like window size not being remembered (Issue #4634) and persistent UI jank.
- **Mixed Sentiment on Memory System:** While there is excitement about the ReMe memory backend, users are finding it opaque. One user noted that prompts lie about functionality ("prompts.py lies to agents: Dream writes to digest/ not MEMORY.md," Issue #6853), and another asks for clearer roadmap details.
- **Dissatisfaction with Background Tasks:** The prominent display of background tasks in the chat window is a point of annoyance, with users feeling it clutters the main interface and hides the actual conversation. The request to fold or move it to a separate area (#6876) highlights this issue.
- **Security/Stability Concerns:** A user reported that their antivirus software heavily interferes with QwenPaw during tasks, calling it a stark contrast to another agent tool. This is a serious trust issue.

### 8. Backlog Watch

Several important issues and PRs require maintainer attention to keep momentum and community trust high.

- **Critical Backlog Issues:** The long-standing issue #4237 about in-chat shell command observability has had no maintainer response since its creation in May. This feature would significantly enhance the product's usability.
- **Awaiting Merge/Review:** PR #5992 ("Add per-session model overrides") has been open since 2026-07-12 with no recent comments. This is a major feature request, and a lack of feedback could be discouraging to new contributors. [Link](agentscope-ai/QwenPaw PR #5992)
- **High-Severity Windows Installer Bug (Issue #6810):** This issue details a broken update path that forces users to manually uninstall, which is a poor experience and needs a maintainer response to either fix, document, or provide a workaround. [Link](agentscope-ai/QwenPaw Issue #6810)
- **Community Questions:** Several questions remain unanswered, such as #6585 about the character count display toggle, which, while minor, affects daily usability.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**Date:** 2026-08-11

---

## 1. Today's Overview

ZeroClaw is in a period of sustained, high-intensity development and hardening, with 50 issues and 50 PRs receiving updates in the last 24 hours. The project is currently navigating a significant governance transition, as evidenced by the extensive `status:accepted` labeling on RFCs and the pending ratification of RFC #6808, which seeks to overhaul work routing and label management. Activity is heavily weighted towards security audits and fixes, with a notable batch of newly filed critical vulnerabilities (S0/S1 severity) and an impressive series of RFCs moving towards acceptance. While the project has zero closed issues and only one merged/closed PR today, the pipeline is full, with 49 open PRs waiting for review, many flagged with `needs-author-action`, indicating a potential bottleneck in the contribution lifecycle. The maintainer team is clearly focused on consolidating governance processes and addressing systemic security gaps before the next release.

---

## 2. Releases

No new releases were published in the last 24 hours. The project is currently in the `0.8.x` series, with the latest version being `0.8.3`.

---

## 3. Project Progress

Only one PR was closed/merged today:

- **#8301** [CLOSED]: **test(hardware): cover catalog tool name format** — A test-only PR adding regression tests to ensure tool names follow lower_snake_case conventions. This is a small, quality-of-life fix that helps maintain codebase consistency.

While no major features landed today, several large, long-running PRs remain active and are progressing towards merge:
- **#8486**: **feat(gateway): add OpenAI chat completions endpoint** — This is a massive, `size:XL` PR that would add a highly requested OpenAI-compatible REST endpoint to the gateway, enabling compatibility with tools like LangChain and Continue.dev.
- **#9182**: **feat(runtime): support PowerShell as the native shell on Windows** — Another large PR that would significantly improve the Windows experience.
- **#9867**: **ci(labels): automate PR size labels** — A CI improvement aimed at automating label maintenance, directly addressing workflow pain points raised in issue #9345.

---

## 4. Community Hot Topics

The most active discussions this week are centered on governance and architectural decisions:

- **#6808**: **RFC: Work Lanes, Board Automation, and Label Cleanup** (23 comments) — The most active thread, this RFC is a comprehensive proposal to streamline the project's work-tracking process. It has been in discussion for over two months and is currently in "ratification deferred / rollout in progress" status. The community seems invested in this as a foundational change.
- **#7100**: **RFC: Per-model capability & context-window config** (13 comments) — A technical RFC addressing the problem of misreported model capabilities (e.g., vision support) and incorrect context-window fallbacks. This is a high-priority (P1) issue that impacts core agent functionality.
- **#8692**: **[Tracker]: Maintainer decision queue for RFCs and design issues** (12 comments) — A meta-issue acting as a queue for pending maintainer decisions. Its high activity level suggests it is being actively used to triage and manage the flood of RFCs.
- **#9397**: **RFC: Treat an empty WhatsApp Web `allowed_groups` as permit-none** (12 comments) — A high-priority security RFC proposing a breaking change to default behavior to fix a dangerous security hole.

The underlying need here is clear: ZeroClaw is growing rapidly, and the community is actively participating in shaping the processes and technical foundations that will scale with it. There is a strong focus on security-by-default and improving developer experience.

---

## 5. Bugs & Stability

This week sees a significant number of critical security and stability bugs reported, several with S0 (data loss/security risk) severity. The majority of these are from a security audit and have open PRs or are `in-progress`.

**Critical (S0 - Data Loss / Security Risk):**
- **#9647**: **Knowledge graph has no per-agent attribution** — Any agent can read/mutate another's knowledge. Fundamental isolation flaw, `risk:high`.
- **#9855**: **Matrix channel fails to resolve homeserver via `.well-known` delegation** — Bypasses standard discovery, potentially leading to connection failures or security misconfigurations.
- **#9627**: **git write verbs bypass the risk classifier** — Significant sandbox escape via `git -C` flag. `S0` security risk with an `in-progress` fix.

**High (S1 - Workflow Blocked):**
- **#9207**: **web_fetch returns garbage for compressed responses** — Tool unusable for many websites. `In-progress`.
- **#9425**: **Running SOP jobs have no operator cancellation path** — Operational control gap.
- **#9035**: **Docker Compose gateway can remain loopback-bound** — Deployment issue causing connection refused errors.
- **#9393**, **#9392**, **#9389**, **#9395**, **#9391**: A wave of security audit findings for missing authorization on Bluesky/Reddit/LINE channels, an authentication lockout bypass, and non-functional audit logging. All are `in-progress` and `risk:high`.

**Medium (S2 - Degraded Behavior):**
- **#9768**: **daemon reload is not on SIGUSR1, and the degraded-security warning tells operators to send a signal that kills the daemon** — Dangerous documentation/implementation mismatch.

A common theme is a batch of security bugs filed by a single user (`belumume`), indicating a thorough security audit is underway. The project is responding by tagging these as `in-progress` and `risk:high`.

---

## 6. Feature Requests & Roadmap Signals

The active RFCs provide a strong signal for the project's roadmap:

- **Streamlined RFC Process (#9496)**: The community acknowledges the current RFC process is too slow. This is a strong signal that the project will adopt a more agile decision-making model in the near term, likely simplifying governance.
- **Per-model capability config (#7100)**: This is a user-facing feature that will improve reliability when using diverse models (especially local ones like Ollama) and prevent subtle failures.
- **Automated PR labeling (#9345, #9867)**: The project is actively working on workflow automation to reduce maintainer overhead.
- **Custom CA Trust for MCP Servers (#9339)**: This `risk:high` feature addresses a real-world enterprise need for private/self-hosted MCP servers and is likely to be prioritized.
- **OpenAI Chat Completions Endpoint (#8486)**: This is arguably the most anticipated feature, and its eventual merge will be a major milestone, opening the gateway to a vast ecosystem of tools.

---

## 7. User Feedback Summary

The user feedback this week is overwhelmingly focused on **security** and **data integrity**.
- Several issues (#9393, #9392, #9389) were filed by a user who explicitly states they audited the codebase line-by-line, reflecting a high level of trust and engagement. The community is actively contributing to making the platform safer.
- There is clear dissatisfaction with the **lack of per-agent isolation** in the knowledge graph (#9647), signaling that multi-tenant or multi-agent deployments require stronger security boundaries.
- On the usability front, users are blocked by the **`web_fetch` compression bug** (#9207) and the **docker-compose loopback issue** (#9035), which disrupt basic workflows.
- Contributors are closely watching the **RFC process**, with #6808 accumulating 23 comments. There's a desire for a more efficient, less cumbersome workflow.
- The **large number of `needs-author-action` PRs** (e.g., #8486, #8561) suggests that contributors may be struggling to keep up with maintainer feedback, or that the review process is slow, potentially causing frustration and stalling progress.

---

## 8. Backlog Watch

Several important issues and PRs are in danger of stalling and need maintainer attention:

- **#5842**: **[Feature]: warn when Codex CLI extra_args weaken sandbox or policy boundaries** — An old (April) `P2` security enhancement with no recent activity. It remains relevant and needs to be either picked up or formally closed.
- **#8576**: **fix(channels): add env-var fallback for OpenAI STT credentials** — A `P3` bug fix that has been open since July and is currently a `stale-candidate`. It needs a decision to keep or close.
- **#8655**: **refactor(zerocode): consolidate Code pane, rails, and prompt drafts** — A large, `size:XL` refactoring PR from an experienced contributor that is also tagged as a `stale-candidate`. This significant change needs a clear path forward.
- **#9867**: **ci(labels): automate PR size labels** — This new PR directly implements the accepted feature request #9345. It should be prioritized for review to keep the RFC-to-implementation pipeline moving.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*