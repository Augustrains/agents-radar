# OpenClaw Ecosystem Digest 2026-07-19

> Issues: 412 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-19 01:20 UTC

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

Here is the OpenClaw project digest for July 19, 2026.

---

## OpenClaw Project Digest – 2026-07-19

### 1. Today's Overview

Activity remains very high, with 412 issues and 500 PRs updated in the last 24 hours. The project is in a heavy development cycle, evidenced by the release of `v2026.7.2-beta.3` and a massive influx of new pull requests, many targeting stability and security. The community is focused on a core set of recurring themes: session state reliability, provider credential management, and securing the agent runtime against edge-case vulnerabilities (e.g., SSRF, unbounded reads). While a large number of issues are open (257 active), maintainer attention is engaged on P0/P1 blockers, with several critical PRs submitted for review.

### 2. Releases

**v2026.7.2-beta.3** was published. This is a minor beta release.

- **New Feature:** Remote coding sessions have been significantly enhanced. Users can now run Control UI sessions on cloud workers, open Codex and Claude catalog sessions in terminals on their host machines, and resume OpenCode and Pi sessions directly from a terminal. (Related PRs: #107670, #107086, #107200)
- **Migration Notes:** As with any beta, users should expect potential instability and breaking changes. The release notes mention "Native automation and nodes" (text truncated), suggesting further deep integration of the agent runtime.

### 3. Project Progress

In the last 24 hours, **closed/merged PRs totaled 245**.

Key closures and advancements include:
- **Compatibility & Credentials:** PR #110878 (Nostr relay connection reporting) was closed, and PR #110948 (markdown stripping before TTS) merged, improving user experience on voice surfaces.
- **Bug Fixes:** A significant number of fixes targeted the CLI and core gateway. Notable examples include PR #109775 (surfacing Anthropic HTTP error bodies), PR #110755 (bounding file read size in `exec approvals`), and #111102 (fixing a DNS SSRF bypass in the Codex extension's WebSocket URL validation).
- **Refactoring:** Maintainer `steipete` is leading a major refactoring effort to centralize bounded file reads (`/fs-safe`, PR #111104) and unify tool-call ID resolvers (#111103), indicating a push for better code quality and security.

### 4. Community Hot Topics

The most active discussions reflect deep user concern with session reliability and security.

- **[#75: Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75) – (113 comments, 81 👍)**: This is the most active issue by far. The community is persistently requesting desktop client support for Windows and Linux. The overwhelming demand and 6-month lifespan of this issue indicate it is a major barrier to adoption.
- **[#88312: Codex turn-completion stall regression](https://github.com/openclaw/openclaw/issues/88312) – (21 comments, Closed)**: A high-severity regression that caused multi-tool agent turns in the Codex app-server to stall. The issue was closed, suggesting a fix was released, but the discussion highlights fragility in the Codex integration.
- **[#7707: Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) – (17 comments)**: A high-reaction feature request for memory security. Users are concerned about prompt injection and "memory poisoning" from untrusted sources (web pages, third-party skills), indicating a sophisticated user base aware of advanced security threats.
- **[#91009: CPU-bound hooks process stalls gateway](https://github.com/openclaw/openclaw/issues/91009) – (14 comments)**: A critical P1 bug where Codex's `pre_tool_use` hook creates CPU-spinning processes, crashing the gateway. This is a clear stability pain point for users running complex agent workflows.
- **[#79077: Telegram bot-to-bot & guest modes](https://github.com/openclaw/openclaw/issues/79077) – (11 comments, 8 👍)**: The community is actively requesting support for new Telegram features. This signals a desire for multi-agent, inter-operable systems.

### 5. Bugs & Stability

Stability is a primary focus, driven by a cluster of P0/P1 regressions.

- **Critical (P0):**
    - **[#109867: State migration blocks gateway startup](https://github.com/openclaw/openclaw/issues/109867)**: A regression in the `beta.2` state migration where a database index is created before its required column, preventing the gateway from starting. A fix is pending.
    - **[#108435: Gateway fails to start on v2026.7.1](https://github.com/openclaw/openclaw/issues/108435)**: A regression causing a crash loop on startup, potentially related to the Ollama integration. The root cause is being investigated.
- **High (P1):**
    - **Codex Integration Issues:** Multiple critical P1 bugs relate to the Codex app-server. [#109490](https://github.com/openclaw/openclaw/issues/109490) documents a bug where agent turns are interrupted after a delegated tool call, preventing promised follow-up work. [#91009](https://github.com/openclaw/openclaw/issues/91009) (CPU-bound hooks) and [#95121](https://github.com/openclaw/openclaw/issues/95121) (leg latency for small replies) highlight ongoing performance and reliability issues.
    - **Session State Corruption:** [#96242](https://github.com/openclaw/openclaw/issues/96242) reports Telegram duplicate messages due to multiple independent paths. [#86684](https://github.com/openclaw/openclaw/issues/86684) describes a dangerous bug where parent sessions are prematurely compacted by subagent activity.
    - **Security Fix PRs:** Several important fixes have been submitted, including PRs [#111098](https://github.com/openclaw/openclaw/pull/111098) and [#111102](https://github.com/openclaw/openclaw/pull/111102) which address DNS SSRF bypass vulnerabilities, showing a proactive security posture.

### 6. Feature Requests & Roadmap Signals

The user community is clearly pushing for an enterprise-grade, secure, and multi-platform agent platform.

- **Security & Trust:** Features like **Masked Secrets** ([#10659](https://github.com/openclaw/openclaw/issues/10659)), **Memory Trust Tagging** ([#7707](https://github.com/openclaw/openclaw/issues/7707)), and a **Skill Permission Manifest** ([#12219](https://github.com/openclaw/openclaw/issues/12219)) are all high-engagement. This will likely lead to a "security hardening" release in the near future.
- **Platform Expansion:** The enduring demand for **Linux/Windows Apps** ([#75](https://github.com/openclaw/openclaw/issues/75)) makes this a top candidate for the next major version.
- **Developer Tooling:** Features like a **Model Fallback Test command** ([#6599](https://github.com/openclaw/openclaw/issues/6599)) and **Dynamic Model Discovery** ([#10687](https://github.com/openclaw/openclaw/issues/10687)) point to a user base that wants more control and debuggability, a likely focus for v2026.8.

### 7. User Feedback Summary

- **Pain Points:**
    - **Stability:** The most frequent feedback concerns session failures, stalls, and duplicate messages, particularly with the Codex app-server and Telegram integrations.
    - **Security Anxiety:** Users are explicitly requesting features to mitigate prompt injection and credential leaks, indicating a sophisticated but cautious user base.
    - **Missing Platforms:** A persistent, high-volume request for Windows and Linux desktop clients.
- **Satisfaction Drivers:**
    - **Rapid Iteration:** The high velocity of PRs and releases is a clear positive, signaling a responsive team.
    - **Power-User Focus:** Features like headless approval resolution (PR #111060) and remote sessions (v2026.7.2-beta.3) are well-received by the developer-heavy community.
- **Overall Sentiment:** The sentiment is cautiously optimistic. Users are excited about the features but are facing real-world stability bumps that slow down adoption.

### 8. Backlog Watch

The following issues and PRs have been open for an extended period and are important for project health:

- **[#75: Linux/Windows Clawdbot Apps](https://github.com/openclaw/openclaw/issues/75)**: Open for over 6 months with 113 comments. A massive blocker for many users.
- **[#7707: Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)**: Open since February, this high-priority security feature needs a maintainer decision.
- **PRs Stuck in "Needs Proof":** Several critical PRs related to security (e.g., [#111098](https://github.com/openclaw/openclaw/pull/111098)) and stability (e.g., [#103793](https://github.com/openclaw/openclaw/pull/103793) on channel health) are still awaiting final review or proof of concept. These represent a bottleneck in the development cycle.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report you requested.

---

## Cross-Project Ecosystem Report: Personal AI Agent Open-Source Landscape
**Date:** 2026-07-19

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem is in a phase of intense maturation, characterized by a split between projects focused on **production-grade stability and security** (e.g., OpenClaw, ZeroClaw) versus those prioritizing **rapid feature iteration and developer experience** (e.g., NanoClaw, CoPaw). A clear trend is the move toward hardened security postures—encompassing memory trust tagging, credential injection prevention (SSRF), and supplier-chain signing—as user bases expand from hobbyists to production deployments. Most projects are wrestling with the fundamental challenge of **session and memory reliability**, especially in multi-turn, multi-tool, and multi-channel workflows. The landscape is becoming more stratified, with a few dominant references (OpenClaw, ZeroClaw) setting the architectural pace, while smaller players (Moltis, PicoClaw) carve out niches in specific communication protocols or deployment simplicity.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release (24h) | Health Score* |
| :--- | :--- | :--- | :--- | :--- |
| **ZeroClaw** | 50 | 50 | None | **Very High** – Sustained high velocity; deep architecture work |
| **OpenClaw** | 412 | 500 | `v2026.7.2-beta.3` | **Very High** – Massive throughput; major refactoring |
| **Hermes Agent** | 50 | 50 | None | **High** – Fast triage; high closure rate on critical bugs |
| **IronClaw** | 1 | 50 | None | **High** – Major internal refactoring; low community engagement |
| **NanoClaw** | 18 | 16 | None | **High** – Focused bug-fix velocity; good responsiveness |
| **CoPaw** | 11 | 6 | None | **Moderate** – Active bug fixes; healthy contributor pipeline |
| **NanoBot** | 7 | 30 | None | **Moderate** – Rapid PR merges; good community maintenance |
| **PicoClaw** | 3 | 12 | None | **Moderate** – Healthy maintenance; low community volume |
| **Moltis** | 0 | 3 | None | **Low-Moderate** – Steady, low-volume progress |
| **LobsterAI** | 0 | 2 | `v2026.7.17` | **Low** – Stale issues; low community activity |
| **NullClaw** | 1 | 0 | None | **Low** – Minimal activity; one unresolved blocker |
| **TinyClaw** | 0 | 0 | None | **Inactive** – No activity in 24 hours |
| **ZeptoClaw** | 0 | 0 | None | **Inactive** – No activity in 24 hours |

*\*Health Score is a qualitative assessment based on development velocity, community engagement, and responsiveness to issues.*

### 3. OpenClaw's Position

OpenClaw is the ecosystem's **core reference implementation** and by far the most active project, with 412 issues and 500 PRs in a single day—an order of magnitude more than its nearest competitor (ZeroClaw at 50/50). Its advantages over peers include:

- **Architecture & Security Leadership:** OpenClaw is driving the most advanced security work, including proactive DNS SSRF fixes (PR #111098, #111102), centralized bounded file reads (PR #111104), and high up-vote features like Memory Trust Tagging (#7707). This gives it a clear lead in enterprise-grade security.
- **Community Scale & Feedback:** With 113 comments on a single issue (#75 for Windows/Linux apps), OpenClaw’s community is larger, louder, and more demanding. This creates a feedback loop that drives rapid iteration, but also exposes more pain points.
- **Technical Approach:** OpenClaw is focusing on a **highly modular, gateway-centric architecture** with deep integrations (Codex, Telegram). Its primary challenge is managing the complexity of this integration, as evidenced by a cluster of P0/P1 stability regressions in the Codex app-server and session state.
- **Risk:** While OpenClaw leads in volume, it is also the most unstable project during this heavy development cycle, with 257 active issues and multiple P0 startup blockers (#108435, #109867). For developers, it offers the most power but demands the most tolerance for breakage.

### 4. Shared Technical Focus Areas

A set of common challenges is emerging across the ecosystem:

- **Session & State Reliability (All Major Projects):** The single biggest pain point. OpenClaw faces session corruption ([#86684](https://github.com/openclaw/openclaw/issues/86684)), NanoBot has legacy metadata loss ([#4940](https://github.com/HKUDS/nanobot/issues/4940)), NanoClaw fixed double-delivery ([#3083](https://github.com/nanocoai/nanoclaw/pull/3083)), and CoPaw deals with session-blocking deadlocks ([#6245](https://github.com/agentscope-ai/QwenPaw/issues/6245)). **Every project is actively debugging its turn lifecycle.**
- **Security Hardening (OpenClaw, ZeroClaw, NanoClaw, IronClaw):** There is a clear industry pivot toward proactive security. **Password/credential injection** (IronClaw #6247, bearer tokens in plaintext), **memory poisoning** (OpenClaw #7707), and **timing attack vulnerabilities** (ZeroClaw #9110) are all being addressed.
- **Multi-Platform Support & Desktop Clients (OpenClaw #75, Hermes Agent, NanoBot, CoPaw):** The community is demanding first-class desktop support (Windows, Linux) and better mobile/headless Linux workflows.
- **Channel Integration Polish (All):** Projects are refining messaging integrations. **WhatsApp** is a major focus (PicoClaw #3242, NanoClaw #3085/#3086), along with **Telegram** (OpenClaw, NanoClaw, ZeroClaw) and **Discord** (Hermes Agent, ZeroClaw).

### 5. Differentiation Analysis

| Axis | OpenClaw | ZeroClaw | NanoClaw/Hermes | CoPaw | IronClaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Target User** | Heavy power user, developer | Production/enterprise operator | Hobbyist-to-power-user, Chinese-speaking | Developer, open-source researcher | Rust-heavy, core developer |
| **Architecture** | Modular, gateway+extensions | Plugin-based, security-first | Lightweight, channel-aggregator | Agent-centric, memory focused | Monorepo, trait-object heavy |
| **Feature Focus** | Codex integration, remote sessions | WASM plugins, cron/scheduling | IM integration (WhatsApp, Signal) | Shell command robustness | Architecture simplification, MCP |
| **Stability** | High feature velocity, frequent bugs | High stability, slower feature growth | Moderate; relies on rapid bug fixes | Moderate; stable base with regressions | High; internal refactoring focus |
| **Community** | Largest, most demanding | Active, more formal RFC process | Growing, responsive maintainers | Good, first-time contributors | Low community engagement |

### 6. Community Momentum & Maturity

- **Tier 1 – Rapidly Iterating (High Velocity, Some Instability):**
    - **OpenClaw** (412 issues, 500 PRs) and **ZeroClaw** (50/50) are the clear leaders in raw development output. Both are deep in architectural overhauls (security, plugins). They offer the most advanced features but require a higher tolerance for breaking changes.
    - **Hermes Agent** (50/50) is rapidly closing bugs, especially on Windows and Desktop, indicating a push for stability.

- **Tier 2 – Stabilizing & Mature (Good Velocity, Stable Core):**
    - **IronClaw** (1/50) is in a heavy internal refactoring phase (arch-simplification slices B & C), moving toward a closed-enum architecture. Low community noise suggests a focus on code quality.
    - **NanoBot** (7/30) and **NanoClaw** (18/16) are settling into a healthy maintenance rhythm, rapidly merging bug fixes from a growing contributor base.
    - **PicoClaw** (3/12) is in a healthy maintenance cycle with focused dependency bumps and targeted bug fixes.

- **Tier 3 – Low Activity / Stale:**
    - **LobsterAI** has a stale issue backlog (108 days old) and a low PR velocity, signaling a project that may be deprioritized by its maintainer.
    - **NullClaw**, **TinyClaw**, and **ZeptoClaw** show minimal to no activity, indicating these projects may be dormant or solely for personal use.

### 7. Trend Signals

The following industry trends emerge from community feedback and development focus:

1.  **Security is Shifting from "Nice-to-Have" to "Table Stakes":** Users are no longer just asking for features; they are demanding protection against prompt injection, credential leaks, and memory poisoning. Projects like OpenClaw (#7707, #10659) and ZeroClaw (#9127, #9110) are leading this charge. **For developers:** Building an agent today requires a first-class security model from day one.

2.  **The "Local-First" Revolution is Real:** The demand for local LLM support (Ollama, LM Studio) is high, with users explicitly stating systems are "totally unusable" with poor local performance (NanoBot #4867). **Signal:** Projects that optimize for local inference (pipeline caching, prompt prefix optimization) will win the home-lab and privacy-conscious developer segments.

3.  **Session Reliability is the "Quiet Killer":** Duplicate messages, dropped turns, and infinite loops are the most cited user frustrations across every single active project. The core AI agent loop—particularly with multi-tool, multi-turn interactions—remains brittle. **Opportunity:** A project that solves "turns that always work, no matter what" will leapfrog the competition.

4.  **Enterprise Integration is Driving Feature Work:** Configurable Slack URLs (Moltis #1159), SMTP cron channels (ZeroClaw #5573), and OAuth provider compliance (PicoClaw #3241) show that agents are being deployed in corporate environments behind proxies and with specific compliance needs.

5.  **The "Agent SDK" War is Coming to Open Source:** OpenClaw's Codex integration and Hermes Agent's Claude SDK Provider (PR #65982) signal a future where open-source agents must interoperate with or replace proprietary agent SDKs. **Prediction:** Expect a major effort to standardize an "Agent Runtime Protocol" across these projects in the next 6-12 months.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-19

## Today's Overview

The project remains highly active with **30 PRs updated** in the last 24 hours (16 merged/closed, 14 open) alongside **7 issues updated** (4 closed, 3 open). No new releases were published today. The maintainers are processing a substantial backlog of bug fixes and feature work across multiple subsystems, particularly in **session management, CLI/exec stability, and memory persistence**. The rapid PR velocity—especially from contributors `santhreal`, `kuchazi-yy`, and `KDB-Wind`—signals a healthy open-source cycle of bug reporting, rapid patching, and collaborative review. No security-critical incidents appear in today's activity, though several reliability-focused patches are in flight.

## Releases

*No new releases were published on 2026-07-19.*

## Project Progress

The following **16 PRs were merged or closed** in the last 24 hours, representing significant forward progress:

- **Memory and Context Management:**
  - [#4627](https://github.com/HKUDS/nanobot/pull/4627) *(merged)* — Preserves delivery context during memory consolidation, fixing a regression where channel delivery messages could be lost during replay-window archival.
  - [#4626](https://github.com/HKUDS/nanobot/pull/4626) *(merged)* — Adds opt-in eager consolidation that archives completed conversation slices into `memory/history.jsonl` after responses (disabled by default, append-only initially).
  - [#4621](https://github.com/HKUDS/nanobot/pull/4621) *(merged)* — Gates archive facts with provenance context, including bounded `MEMORY.md` excerpts in Consolidator archive prompts to reduce duplicate fact storage and enable earlier correction detection.

- **Agent and Tool Execution:**
  - [#4925](https://github.com/HKUDS/nanobot/pull/4925) *(merged)* — Fixes recovery from oversized tool results by bounding tool output before calling the provider, replacing oversized results with actionable instructions for the model to retry with narrower scope.

- **Infrastructure and Deployment:**
  - [#4937](https://github.com/HKUDS/nanobot/pull/4937) *(merged)* — Adds one-click deploy to Render support via a Render Blueprint (gateway + bundled WebUI as single web service with persisted session history and memory).

- **Subagent Improvements:**
  - [#4624](https://github.com/HKUDS/nanobot/pull/4624) *(merged)* — Adds aggregated result mode for subagents, buffering results by session_key in aggregated mode and publishing one combined `subagent_result` after the task set drains.

- **Closed Bug Reports (with actionable fixes):**
  - [#2343](https://github.com/HKUDS/nanobot/issues/2343) *(closed)* — Context window token overflow bug now resolved (reported by `jermeyhu`).
  - [#4867](https://github.com/HKUDS/nanobot/issues/4867) *(closed)* — Ollama caching performance issue (60s extra per turn) now addressed.
  - [#4886](https://github.com/HKUDS/nanobot/issues/4886) *(closed)* — Docker Compose container confinement security issue (SYS_ADMIN + disabled AppArmor/seccomp) fixed.
  - [#4786](https://github.com/HKUDS/nanobot/issues/4786) *(closed)* — `SessionManager._cache` resource leak (unbounded growth without TTL/LRU eviction) resolved.

## Community Hot Topics

**Most active discussions (by comment count):**

1. **[#2343](https://github.com/HKUDS/nanobot/issues/2343) — Context window token overflow** (15 comments, closed)
   - *Analysis:* This high-engagement thread captured a core user frustration: the LLM's maximum context length (32768 tokens) was being exceeded despite explicit `contextWindowTokens` and `maxTokens` configuration. The user's desperation ("how do I reduce chat history data?") reflects a broader need for better automatic context window management and user-facing tools to trim history.

2. **[#4867](https://github.com/HKUDS/nanobot/issues/4867) — Ollama caching: 60-second overhead per turn** (5 comments, closed)
   - *Analysis:* Reported by a user with 32GB VRAM who describes the system as "totally unusable" with Ollama. The root cause was Nanobot not preserving exact prompt prefixes to enable Ollama's prompt caching. This signals strong demand for local-model-first optimizations in the project.

3. **[#4940](https://github.com/HKUDS/nanobot/issues/4940) — Legacy session metadata lost after restart** (1 comment, open)
   - *Analysis:* Sessions created with legacy filename formats lose their `workspace_scope` metadata after restart. Though comments are few, the issue has an associated fix PR ([#4977](https://github.com/HKUDS/nanobot/pull/4977)) already submitted, indicating maintainers recognize its importance.

**Underlying community needs:** Users are increasingly running Nanobot in production-like settings (persistent deployments on Render, local Ollama setups, multi-workspace configurations) and encountering edge cases around state persistence, resource management, and compatibility with local LLM serving tools.

## Bugs & Stability

**Critical/High Severity (P1):**

- **GitStore workspace mismatch** ([#4980](https://github.com/HKUDS/nanobot/issues/4980)) — `GitStore` fails to initialize when workspace differs from process working directory. Relative paths passed to Dulwich's `porcelain.add()` cause failures in automatic commits. **Fix PR:** [#4979](https://github.com/HKUDS/nanobot/pull/4979) *(open, submitted by same reporter)*.

- **Null JSON fields crash trigger/cron stores** — Three concurrent PRs address `TypeError` caused by `null` millisecond fields in JSON storage:
  - [#4986](https://github.com/HKUDS/nanobot/pull/4986) — Local triggers store `null` in `runAtMs`/`createdAtMs` fields.
  - [#4985](https://github.com/HKUDS/nanobot/pull/4985) — Cron jobs store `null` in `runAtMs`/`durationMs` fields.
  - [#4983](https://github.com/HKUDS/nanobot/pull/4983) — String millisecond fields in jobs.json not coerced to integers, causing comparison errors.

- **Atomic config write failure** ([#4984](https://github.com/HKUDS/nanobot/pull/4984)) — `save_config` writes in-place, risking truncated config files on crash. Fix routes through atomic `temp+replace`.

- **Session message cap enforcement** ([#4956](https://github.com/HKUDS/nanobot/pull/4956)) — The 2,000-message file cap was not enforced at the persistence boundary, risking unbounded file growth. Fix pending review.

- **Exec session process tree cleanup** ([#4978](https://github.com/HKUDS/nanobot/pull/4978)) — Long-running exec sessions had no lifecycle management during shutdown, leaving orphan processes. Fix terminates process trees and rejects new sessions during shutdown.

**Medium Severity (P2):**

- **CLI/Windows UTF-8 subprocess output** ([#4975](https://github.com/HKUDS/nanobot/issues/4975), [#4976](https://github.com/HKUDS/nanobot/pull/4976)) — On Windows with non-UTF-8 locales (e.g., CP936/GBK), CLI apps lose UTF-8 subprocess output due to missing explicit encoding in `subprocess.run`. Fix PR submitted.

- **Telegram/Feishu message split hangs** ([#4982](https://github.com/HKUDS/nanobot/pull/4982), [#4981](https://github.com/HKUDS/nanobot/pull/4981)) — Infinite loops in message splitting functions when `limit`/`max_len` is zero or negative. Fix PRs submitted.

- **Legacy session metadata fallback** ([#4940](https://github.com/HKUDS/nanobot/issues/4940), [#4977](https://github.com/HKUDS/nanobot/pull/4977)) — Sessions stored with legacy filename format lose `workspace_scope` on restart. Fix PR submitted.

## Feature Requests & Roadmap Signals

**Recently implemented (merged in last 24h):**
- **One-click Render deployment** ([#4937](https://github.com/HKUDS/nanobot/pull/4937)) — Likely to attract more production and cloud-first users.
- **Subagent aggregated result mode** ([#4624](https://github.com/HKUDS/nanobot/pull/4624)) — Reduces message noise from subagent task completion.
- **Opt-in eager memory consolidation** ([#4626](https://github.com/HKUDS/nanobot/pull/4626)) — Prepares the ground for token-aware automatic memory management.

**In-flight features (open PRs):**
- **Session-local triggers** ([#4942](https://github.com/HKUDS/nanobot/pull/4942)) — Agents can manage triggers scoped to the current conversation (create, list, enable, disable, remove). This opens up agent-driven automation use cases.
- **RTK command rewriter for exec** ([#4854](https://github.com/HKUDS/nanobot/pull/4854)) — Opt-in `rtk` command rewriting for exec sandbox, with environment variable setup and noise filtering.
- **WebUI polish: unified activity language** ([#4963](https://github.com/HKUDS/nanobot/pull/4963)) — Replaces raw, nested tool logs with human-readable single-line activity descriptions covering reasoning, web search, shell, file ops, memory, CLI apps, MCP tools, images, subagents, automations, and goals.

**Predictions for next release:** The session-local triggers feature is likely to land soon given its integration with the existing trigger system. The RTK rewriter and WebUI polish PRs are mid-to-late stage and could both ship in the next minor version. Memory consolidation features will likely remain opt-in for at least one more release cycle.

## User Feedback Summary

**Pain Points:**
- **Context window management** (#2343) — Users configuring explicit token limits still hit LLM provider errors, with no graceful truncation or history trimming tools.
- **Local model performance** (#4867) — "Totally unusable with Ollama and 32GB of VRAM" — a strong signal that local-model workflows are a key but under-optimized use case.
- **Session metadata survivability** (#4940) — User reports that project path scopes are "silently lost" after restart, undermining workspace isolation.
- **Windows locale friction** (#4975) — UTF-8 output from CLI apps breaks on non-UTF-8 Windows locales, a barrier for Windows-based developers.

**Satisfaction Signals:**
- Rapid closure of issues like the Docker security hardening (#4886) and the session cache resource leak (#4786) demonstrates responsive maintainership.
- Multiple contributors are submitting both bug reports and fix PRs (notably `kuchazi-yy`, `santhreal`), indicating a healthy contributor ecosystem.
- The Render deployment PR (#4937) received a direct maintainer CC for review, showing structured review processes.

## Backlog Watch

**Issues needing maintainer attention:**

- **[#4975](https://github.com/HKUDS/nanobot/issues/4975) — Windows UTF-8 subprocess output bug** (0 comments, open since 2026-07-18) — Fix PR [#4976](https://github.com/HKUDS/nanobot/pull/4976) has been submitted by the reporter, awaiting review/merge.

**Open PRs with potential for conflict or requiring careful review:**

- **[#4942](https://github.com/HKUDS/nanobot/pull/4942) — Session-local triggers** (tagged `[conflict]`, open since 2026-07-15) — A substantial feature addition that could conflict with existing trigger management code. Requires maintainer review to ensure backward compatibility.
- **[#4854](https://github.com/HKUDS/nanobot/pull/4854) — RTK command rewriter** (tagged `[priority: p2]`, `[conflict]`, open since 2026-07-08) — Opt-in exec enhancement with sandbox integration concerns. Has been open for 11 days without comment, suggesting maintainer bandwidth constraints.

**Legacy issues without recent activity:**
- No long-dormant issues with maintainer tags were identified in the 24-hour update window. The project appears to be actively triaging its backlog.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for July 19, 2026.

---

## Hermes Agent Project Digest — 2026-07-19

### 1. Today's Overview

The Hermes Agent project is in a state of **very high activity**, with 50 issues and 50 pull requests updated in the last 24 hours. The core focus is on stabilizing the codebase, with a significant 34 out of 50 issues being closed, indicating a highly responsive triage and fix cycle. A critical volume of **P0 severity** issues surfaced on Windows, but were closed rapidly. The community is actively contributing fixes, especially for the Desktop app, Windows compatibility, and provider support, while the team manages a large volume of duplicates and feature requests requiring triage.

### 2. Releases

**No new releases were published today.** The latest public build remains Hermes Desktop v40.9.3 and CLI v0.18.2.

### 3. Project Progress

A high number of PRs were merged or closed today. Key fixes that advanced include:

- **Session State & Desktop**: Fixes landed for session branching (issue #66685), slow session switching (#66667), and lineage deduplication (#66664), all reflecting a push to mature the Desktop core UX.
- **Telegram & Gateway**: Critical thread isolation was fixed for the `terminal` tool (PR #67083, merged), and the `/queue` command now accepts images in Discord (PR #67041, merged).
- **Provider/API Compatibility**: The `_resolve_task_provider_model` bug ignoring `key_env` for auxiliary providers (#66641) was closed. A fix was merged for multimodal content causing a crash in `_interim_assistant_visible_text` (#66755).
- **Platform/Windows**: A P0 installer crash (#66994) and a CLI rendering artifact bug (#67159) were both merged and closed today.

### 4. Community Hot Topics

The most active discussions highlight core user struggles with configuration and model reliability:

- **[#66829](https://github.com/NousResearch/hermes-agent/issues/66829) (Open, 7 comments)**: Users are frustrated that the Desktop app forces image preprocessing through an auxiliary vision model, even when the main model is fully capable of visual processing. This indicates a deep desire for a more intelligent, "smart" routing feature at the vision level.
- **[#66891](https://github.com/NousResearch/hermes-agent/issues/66891) (Closed, 3 comments)**: A detailed report on data corruption in the Obsidian memory MCP server, causing malformed facts and truncated entities. This underscores the importance users place on data integrity when integrating with note-taking tools.
- **[#66950](https://github.com/NousResearch/hermes-agent/issues/66950) (Closed, 5 comments)**: A power user report that identity and memory files load but are ignored by the model. This validates a common pain point: "personality" and rules are probabilistic, not enforced, a feature gap vs. other agent frameworks.

### 5. Bugs & Stability

Stability remains a primary concern, with issues spanning critical installers to subtle runtime regressions.

| Severity | Issue | Component | Summary | Fix Status |
| :--- | :--- | :--- | :--- | :--- |
| **P0** | [#66994](https://github.com/NousResearch/hermes-agent/issues/66994) | Desktop/Win | Installer fails on Windows 11 at `install.ps1` line 1619. | **Closed** (Fixed) |
| **P0** | [#67000](https://github.com/NousResearch/hermes-agent/issues/67000) | CLI/Win | Installer logging error, likely related to #66994. | **Closed** (Duplicate) |
| **P1** | [#38216](https://github.com/NousResearch/hermes-agent/issues/38216) | Desktop/Win | v40.9.3 crashes on startup with 0x80000003 exception (AMD X3D CPU). | **Closed** (Age: 46 days) |
| **P2** | [#67187](https://github.com/NousResearch/hermes-agent/issues/67187) | MCP Tools | Parked MCP server reconnects but does not re-register tools, leading to silent failures. | **Open** (No fix PR) |
| **P2** | [#67233](https://github.com/NousResearch/hermes-agent/issues/67233) | Telegram/CMCC | Image send fails; model claims lack of `vision_analyze` tool. | **Open** (Needs repro) |
| **P2** | [#65631](https://github.com/NousResearch/hermes-agent/issues/65631) | Agent/Provider | Provider error (HTTP 400) inside a 200 SSE stream is misclassified as an "empty stream," causing infinite retries. | **Open** |

### 6. Feature Requests & Roadmap Signals

Several feature requests point toward the next release's likely capabilities:

- **Adaptive Thinking for More Providers**: Multiple PRs (#67228, #67231) propose adding Anthropic-style "adaptive thinking" (thinking with configurable effort) to Kimi and Moonshot endpoints. Given the multiple implementations, this is **highly likely** for the next release.
- **Smart Model Routing ([#66860](https://github.com/NousResearch/hermes-agent/issues/66860))**: A request to auto-select the model based on task complexity (e.g., simple chat vs. deep research). This was marked `not-planned`, suggesting team is focusing on the "one model" reliability first.
- **Claude Agent SDK as a Provider ([PR #65982](https://github.com/NousResearch/hermes-agent/pull/65982))**: A major PR to use Anthropic's official Agent SDK inside Hermes, billed via subscription. This is still open with `needs-decision`, indicating high interest but caution around scope and licensing.
- **Kanban Dashboard Plugin ([PR #67186](https://github.com/NousResearch/hermes-agent/pull/67186))**: This is the first "manifest-driven dashboard plugin" for the Desktop app, meaning a flexible plugin system is arriving for the UI layer.

### 7. User Feedback Summary

- **Windows Users**: Expressed high frustration (P0/P1 bugs) with installers and crashes. While fixes are rapid, the recurrence of setup issues (reported by @aarsantrital-lab, @jbermudeznic) suggests a need for better edge-case testing on Windows 11.
- **MCP Users**: Bug reports around MCP server lifecycle (#67187) and data corruption in `obsidian_mem` (#66891) reveal that while the MCP framework is powerful, its reliability is a top pain point for those integrating with external tooling.
- **Power/Heavy Users**: Requests for identity enforcement (#66950) and model routing (#66860) show that as users build workflows (e.g., rental management, custom scripts), they need more deterministic agent behavior and tool orchestration. The pushback on "probabilistic rules" is a clear signal for a more structured agent loop.
- **Positive Signals**: The community is actively opening PRs for niche platform support (Discord, Telegram, Matrix) and proxy configurations, indicating a healthy and invested user base.

### 8. Backlog Watch

The following items have been open for an extended period without a resolution and may require maintainer attention:

- **[#38216](https://github.com/NousResearch/hermes-agent/issues/38216) (P1, 46 days old)**: Hermes Desktop crash on Windows 11 (AMD X3D). Despite being "Closed," the root cause may not be fully resolved, as this is a long-standing issue.
- **[#51448](https://github.com/NousResearch/hermes-agent/issues/51448) (P2, 26 days old)**: LM Studio connection fails on native Windows but works on WSL. This platform-specific networking bug remains open with no linked fix PR.
- **[#40933](https://github.com/NousResearch/hermes-agent/pull/40933) (P3, 42 days old)**: The "smart reply modality" PR for LINE has been open for over a month with no merge or rejection, potentially blocking other LINE adapter improvements.
- **[#43252](https://github.com/NousResearch/hermes-agent/pull/43252) (P2, 39 days old)**: A long-standing PR to fix Windows job-object issues with cron scripts. This is a critical stability concern for Windows server users running Hermes as a daemon.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date: 2026-07-19**

## Today's Overview
PicoClaw shows moderate activity over the past 24 hours with 3 issues updated (1 open, 2 closed) and 12 pull requests updated (4 open, 8 merged/closed). The project is in a healthy maintenance cycle, with several dependency bumps and bug fixes being merged, alongside the closure of two stale issues that were resolved by recent PRs. The open bug (#3264) regarding a segmentation fault in channel splitting represents the most critical piece of work in flight. No new releases were published today.

## Releases
No new releases were published in the last 24 hours. The current release version remains unchanged.

## Project Progress
Eight merged/closed PRs advanced the project in the last 24 hours, spanning bug fixes, features, and dependency maintenance:

- **#3242** (closed) — `feat(whatsapp): add native typing presence`: Implements `channels.TypingCapable` on `WhatsAppNativeChannel`, sending `composing` immediately, refreshing every 10 seconds during long replies, and sending `paused` when finished. This directly resolves issue #3240.
- **#3241** (closed) — `fix(auth): make OAuth refresh provider-correct and concurrency-safe`: Makes OpenAI refresh requests use JSON body, keeps Google on form encoding, omits scopes during refresh, and adds a 30-second hop-by-hop timeout. Resolves #3239.
- **#2937** (closed) — `Feat/agent collaboration`: Introduces an internal Agent Collaboration Bus with per-agent mailboxes, collaboration threads, structured message envelopes, and permission-aware delivery.
- **#3165** (closed) — `fix(openai_compat): recover Seed XML tool calls`: Recovers Volcengine Doubao Seed XML tool call blocks from OpenAI-compatible responses, strips them from user-visible content, and suppresses leaked XML from streaming chunks.
- **#3225** (closed) — `Support agent-specific runtime overrides`: Allows `agents.list` entries to define `max_tokens`, summarization thresholds, and `split_on_marker`, applied per-agent when building `AgentInstance`.
- **#3200** (closed) — `feat(models): add configurable default fallback chain`: Adds a dedicated default-chain workflow on the models page in the web UI, persisted through the backend API.
- **#3208** (closed) — `build(deps): bump maunium.net/go/mautrix from 0.27.0 to 0.28.1`
- **#3211** (closed) — `build(deps-dev): bump eslint from 10.4.1 to 10.6.0 in /web/frontend`

## Community Hot Topics
- **Issue #3264** ([sipeed/picoclaw#3264](https://github.com/sipeed/picoclaw/issues/3264)) — *[BUG] SplitMessage hangs on an oversized fenced-code info string*: This is the only open/recent issue, filed yesterday with no comments yet. It describes a serious infinite-loop bug in `channels.SplitMessage` where excessively long fenced code block info strings cause a hang. The rarity of this specific scenario may explain the lack of discussion, but it represents a high-risk stability concern.
- **PR #3193** ([sipeed/picoclaw#3193](https://github.com/sipeed/picoclaw/pull/3193)) — *Added simplex channel type*: Still open after 22 days with undefined comments, this PR introduces a new channel type. The silence around it suggests either maintainer bandwidth constraints or unresolved technical considerations.

## Bugs & Stability
- **HIGH — Issue #3264** — `SplitMessage` infinite loop on oversized fenced-code info strings: This bug can cause the system to hang indefinitely when processing messages with large code fence headers near a split boundary. No fix PR exists yet. **Severity: Critical** (potential service denial).
- **FIXED — Issue #3239** — OAuth refresh race condition and incompatible provider semantics: Closed as stale, resolved by PR #3241. The fix introduces provider-specific body formats (JSON for OpenAI, form for others) and a 30-second hop-by-hop timeout.
- **FIXED — Issue #3240** — Missing WhatsApp typing presence: Closed as stale, resolved by PR #3242.
- **FIXED — GO-2026-5856 / GO-2026-4970** — Go stdlib vulnerabilities: Addressed by PR #3248 (open, bumping Go to 1.25.12).

## Feature Requests & Roadmap Signals
The following features have been recently closed or remain open, indicating direction:

- **Agent Collaboration Bus** (#2937) — A major new inter-agent communication system was merged. This is likely foundational for upcoming multi-agent orchestration features.
- **Simplex Channel** (#3193) — An open PR adding a simplex channel type (one-way communication). If merged, it would enable broadcast-only interaction patterns.
- **Configurable Default Model Fallback Chain** (#3200) — Merged, allowing users to set, reorder, and save model fallbacks through the web UI.
- **Agent-Specific Runtime Overrides** (#3225) — Merged, enabling per-agent `max_tokens`, summarization, and split settings.

**Prediction for next release**: The three open features (Go version bump #3248, 9router gateway support #3205, and ID normalization fix #3202) plus the simplex channel (#3193) are likely candidates. The critical bug #3264 may also be fast-tracked.

## User Feedback Summary
Pain points and use cases observed from recent issues and PRs:

- **OAuth provider incompatibility** (#3239/#3241): Users hitting the runtime error "refresh expects a JSON body" when using OpenAI OAuth highlights the need for provider-aware authentication logic.
- **WhatsApp typing feedback** (#3240/#3242): Users reported degraded UX with no visual feedback between sending a message and receiving a reply, especially on slower connections or long processing times.
- **Raspberry Pi / ARM deployment** (#3205): A user running PicoClaw on a Raspberry Pi 3 B+ reported two blockers — missing ARM build target and incompatible 9router gateway response parsing. This signals demand for edge/embedded deployments.
- **Stale issue closures**: Two issues (#3239, #3240) were automatically closed as stale after being fixed by recent PRs. This pattern suggests maintainers may be clearing backlog, but the stale-bot can confuse users whose bugs have been addressed.

## Backlog Watch
- **PR #3193** ([sipeed/picoclaw#3193](https://github.com/sipeed/picoclaw/pull/3193)) — *Added simplex channel type*: Open for 22 days with no maintainer comments. This feature could expand PicoClaw's communication patterns significantly (e.g., broadcast-only channels, one-way notifications). Lack of engagement may need maintainer attention to either merge or provide feedback.
- **Issue #3264** ([sipeed/picoclaw#3264](https://github.com/sipeed/picoclaw/issues/3264)) — *SplitMessage hangs on oversized fenced-code info string*: Filed yesterday with zero comments. Given the severity (infinite loop), this should be prioritized for triage even without community discussion, as it could affect any user sending large code blocks.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date:** 2026-07-19

---

## Today's Overview

NanoClaw saw elevated maintainer activity on 2026-07-19, with **18 issues updated** (16 closed) and **16 PRs updated** (7 merged/closed, 9 open). The project closed several longstanding bugs in the Slack adapter, WhatsApp messaging, and SDK event handling, while introducing new security hardening and architectural fixes. Activity was concentrated in the **agent-runner, session management, and channel adapter** areas, with multiple core-team PRs merged today. No new releases were published. The high closure rate (89% of issues, 44% of PRs) indicates a focused triage and bug-fix push.

---

## Releases

*No new releases were published on 2026-07-19.* The latest available version remains unchanged.

---

## Project Progress

**7 PRs merged/closed today**, reflecting significant bug-fix velocity:

| PR | Description | Impact |
|---|---|---|
| [#3083](https://github.com/nanocoai/nanoclaw/pull/3083) (merged) | **fix(agent-runner): compact_boundary must not surface as a result** — SDK context compaction events were being delivered as synthetic agent replies, causing **double-delivery** of messages to users. | Critical fix for duplicate message bug. |
| [#3084](https://github.com/nanocoai/nanoclaw/pull/3084) (merged) | **test(runner): drop temporary diagnostics from /clear-abort test** — Cleanup of temporary debugging instrumentation from PR #3083. | Housekeeping/CI quality. |
| [#3077](https://github.com/nanocoai/nanoclaw/pull/3077) (merged) | **fix(claude): only abort on a rejected rate_limit_event; split rate_limit vs quota** — Stops false "quota exceeded" errors that appeared on every normal turn. Fixes issue [#3016](https://github.com/nanocoai/nanoclaw/issues/3016). | Reduces noise in agent-runner logs. |
| [#3086](https://github.com/nanocoai/nanoclaw/pull/3086) (merged) | **fix(whatsapp): validate recipient exists before sending** — Prevents silent message loss to unregistered WhatsApp numbers. | Reliability improvement for WhatsApp adapter. |
| [#3062](https://github.com/nanocoai/nanoclaw/pull/3062) (merged) | **fix(signal): send read receipts** — Enables `--send-read-receipts` in signal-cli daemon so senders see messages marked read. | User-facing UX improvement for Signal. |
| [#2702](https://github.com/nanocoai/nanoclaw/pull/2702) (closed) | **fix(slack): switch adapter to Socket Mode** — Replaces HTTP webhook mode (requires public URL) with Socket Mode for simpler self-hosted deployment. | Deployment simplification. |
| [#2496](https://github.com/nanocoai/nanoclaw/pull/2496) (closed) | **fix: open outbound DB with write access in writeOutboundDirect** — Fixes silent failure of command-gate deny responses (SQLITE_READONLY bug). | Fixes silent user notification failures. |

**Key feature advances still in open PRs:**
- [#2999](https://github.com/nanocoai/nanoclaw/pull/2999) + [#3076](https://github.com/nanocoai/nanoclaw/pull/3076) — Dual PRs to unify iMessage into a single channel with local+hosted backends (both open, may need consolidation)
- [#3087](https://github.com/nanocoai/nanoclaw/pull/3087) — Fix WhatsApp mention engagement for typed @-mentions (core-team PR, likely to merge soon)

---

## Community Hot Topics

### Most Active Discussions

1. **Issue [#3085](https://github.com/nanocoai/nanoclaw/issues/3085) - WhatsApp engage_mode=mention fails on typed @-mentions** (open, 1 comment)
   - *User pain:* Users who type `@agent name` without picking an autocomplete suggestion never trigger agent engagement. The `accumulate` policy masks the failure by silently storing messages.
   - *Status:* Fix PR [#3087](https://github.com/nanocoai/nanoclaw/pull/3087) already submitted by core team.

2. **Issue [#3016](https://github.com/nanocoai/nanoclaw/issues/3016) - Every rate_limit_event logged as quota error** (closed, 3 comments, 👍0)
   - *User pain:* Allowed rate_limit events were incorrectly logged as "quota" errors, generating 82 false error logs in one week. PR [#3077](https://github.com/nanocoai/nanoclaw/pull/3077) fixed this today.

3. **Issue [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) - send_message dedup drops responses for rapid turns** (closed, 4 comments)
   - *User pain:* Agent responses silently dropped when two turns complete within 60 seconds, or when follow-up arrives mid-stream. The poll-loop routes follow-ups into the same `processQuery` call, causing client timeouts.

4. **Issue [#2482](https://github.com/nanocoai/nanoclaw/issues/2482) - Wizard falsely detects "no systemd" under su -** (closed, 3 comments)
   - *User pain:* On Debian 13 Proxmox LXCs with healthy systemd session, setup wizard fell back to nohup wrapper. Environment variables not populated in `su -` context.

5. **Issue [#1981](https://github.com/nanocoai/nanoclaw/issues/1981) - v2 setup: systemd misdetected on headless Linux** (open, 1 comment)
   - *User pain:* Same root cause as #2482 — systemd detection fails in SSH sessions on Hetzner/Ubuntu. Still open from April 2026, related to #2482 which was closed today.

### Analysis
The community is disproportionately affected by **setup wizard and channel integration reliability** issues. The systemd detection bug (#1981) has been acknowledged since April, and while #2482 was closed, the underlying detection logic may still be fragile. WhatsApp engagement bugs (#3085) and Signal read receipts (#3062) show active community interest in polish of existing channels.

---

## Bugs & Stability

### Bugs Fixed Today (6 critical/medium issues closed)

| Bug | Severity | Fix PR | Notes |
|---|---|---|---|
| **Double message delivery** from SDK compaction events [#3083](https://github.com/nanocoai/nanoclaw/pull/3083) | **Critical** | PR [#3083](https://github.com/nanocoai/nanoclaw/pull/3083) (merged) | The `compact_boundary` event was surfacing as a synthetic agent result, causing every turn with context compaction to be delivered twice. |
| **False quota errors** on every normal turn [#3016](https://github.com/nanocoai/nanoclaw/issues/3016) | **Medium** | PR [#3077](https://github.com/nanocoai/nanoclaw/pull/3077) (merged) | Rate limit telemetry events with `status="allowed"` were treated as terminal quota errors. |
| **Silent message drop** for rapid turns [#2506](https://github.com/nanocoai/nanoclaw/issues/2506) | **High** | Fix merged indirectly | Send_message dedup drops responses within 60-second window. |
| **WhatsApp message loss** to unregistered recipients [#3086](https://github.com/nanocoai/nanoclaw/pull/3086) | **Medium** | PR [#3086](https://github.com/nanocoai/nanoclaw/pull/3086) (merged) | `sendMessage` "succeeds" but message vanishes. |
| **Command-gate deny responses never delivered** [#2496](https://github.com/nanocoai/nanoclaw/pull/2496) | **High** | PR [#2496](https://github.com/nanocoai/nanoclaw/pull/2496) (merged) | SQLITE_READONLY prevented INSERT of deny messages. |
| **WhatsApp media silently dropped** on CDN fetch failure [#2894](https://github.com/nanocoai/nanoclaw/issues/2894) | **Medium** | No fix PR yet | Baileys CDN fetch failures caught but not retried/reuploaded. |

### Active/Open Bugs

1. **WhatsApp engage_mode=mention fails on typed @-mentions** [#3085](https://github.com/nanocoai/nanoclaw/issues/3085) — Fix PR [#3087](https://github.com/nanocoai/nanoclaw/pull/3087) submitted, awaiting merge.
2. **Systemd detection fails on headless Linux (v2 setup)** [#1981](https://github.com/nanocoai/nanoclaw/issues/1981) — Open since April, related to #2482 which was closed today. May need a more robust detection approach.
3. **Scheduled task cross-session visibility issues** [#2992](https://github.com/nanocoai/nanoclaw/issues/2992) — Fix PR [#3068](https://github.com/nanocoai/nanoclaw/pull/3068) open since July 16.
4. **Session resolution picks newest session, causing multi-session forks** — Fix PR [#3078](https://github.com/nanocoai/nanoclaw/pull/3078) open since yesterday.

### Regression Risk
The flurry of agent-runner fixes today (double-delivery, quota errors, compact_boundary) touches core message delivery logic. While tests were cleaned up in PR [#3084](https://github.com/nanocoai/nanoclaw/pull/3084), the CI-realistic time budget changes warrant monitoring for edge cases in rapid-turn scenarios.

---

## Feature Requests & Roadmap Signals

### Features in Active Development (Open PRs)

| Feature | PR | Status | Likely Next Version? |
|---|---|---|---|
| **Unified iMessage channel** (local+hosted) | [#2999](https://github.com/nanocoai/nanoclaw/pull/2999), [#3076](https://github.com/nanocoai/nanoclaw/pull/3076) | Open since July 10/17 | ✅ High probability — two competing PRs suggest strong community demand |
| **NCC utility skill** — host operational CLI | [#2971](https://github.com/nanocoai/nanoclaw/pull/2971) | Open since July 7 | 🔶 Medium — awaits review |
| **Telegram message_reaction + callback_query** support | [#2544](https://github.com/nanocoai/nanoclaw/pull/2544) | Open since May 18 | ❌ Stale (2 months) — needs maintainer attention |
| **Loopback webhook authentication** (security) | [#3065](https://github.com/nanocoai/nanoclaw/pull/3065) | Open since July 16 | ✅ High probability — security fix (GHSA-h9g4-589h-68xv) |
| **Discord attachment handling** (URL-based inbound) | [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) | Open since June 12 | 🔶 Medium — improving channel parity |
| **Scheduled task visibility fix** | [#3068](https://github.com/nanocoai/nanoclaw/pull/3068) | Open since July 16 | ✅ Likely — bug fix for cross-session task management |

### User-Requested Features (from closed issues)

- **Keyword-based pre-turn model routing** (Issues [#1679](https://github.com/nanocoai/nanoclaw/issues/1679), [#1681](https://github.com/nanocoai/nanoclaw/issues/1681)) — Both closed, suggesting the feature was implemented. Config allows routing code review to Claude, research to Gemini, etc.
- **ncl CLI for scheduled tasks** (Issue [#2397](https://github.com/nanocoai/nanoclaw/issues/2397)) — Closed, likely already implemented.
- **ncl groups config add-mount / remove-mount** (Issue [#2395](https://github.com/nanocoai/nanoclaw/issues/2395)) — Closed, presumably shipped.

### Predicted Next Release Content
Based on today's velocity and open PR maturity, the next release (v2.0.x) likely includes:
1. Agent-runner double-delivery fix [#3083](https://github.com/nanocoai/nanoclaw/pull/3083)
2. WhatsApp typed mention fix [#3087](https://github.com/nanocoai/nanoclaw/pull/3087) + recipient validation [#3086](https://github.com/nanocoai/nanoclaw/pull/3086)
3. Security: loopback webhook auth [#3065](https://github.com/nanocoai/nanoclaw/pull/3065)
4. Slack Socket Mode migration [#2702](https://github.com/nanocoai/nanoclaw/pull/2702) (already closed)
5. Signal read receipts [#3062](https://github.com/nanocoai/nanoclaw/pull/3062)

---

## User Feedback Summary

### Pain Points (High Confidence)

1. **Rapid-turn message loss** (Issue [#2506](https://github.com/nanocoai/nanoclaw/issues/2506)) — Users submitting follow-up messages within 60 seconds or mid-stream lose responses silently.
2. **False error noise** (Issue [#3016](https://github.com/nanocoai/nanoclaw/issues/3016)) — One user reported 82 false "quota" errors in a week; fix merged today.
3. **WhatsApp engagement friction** (Issue [#3085](https://github.com/nanocoai/nanoclaw/issues/3085)) — Typed @-mentions don't work unless user picks autocomplete. Fix pending merge.
4. **Setup failures on headless Linux** (Issue [#1981](https://github.com/nanocoai/nanoclaw/issues/1981)) — Persistent since April; systemd detection fails in SSH/non-interactive contexts.
5. **Silent message delivery failures** — Multiple channels affected: WhatsApp unregistered recipients (fixed), command-gate denies (fixed), Discord attachments (open), WhatsApp media CDN failures (open).

### Satisfaction Signals
- High **community engagement velocity** — 18 issues + 16 PRs in 24h suggests active, invested user base.
- Quick **fix turnaround** on reported bugs — #3016 (quota errors) had a fix merged within 8 days of report; #2506 (rapid-turn drops) was filed May 16 and closed July 19 with an indirect fix.
- **Core-team responsiveness** — Multiple core-team PRs (#3083, #3084, #3087) submitted today for critical agent-runner bugs.

### Dissatisfaction Signals
- **Double-delivery bug** (#3083) — If this affected users in production, it would erode trust in message reliability.
- **Stale feature PRs** — Telegram reactions (#2544) and Discord attachments (#2752) have been open 2+ months and 1+ month, respectively, without maintainer review.

---

## Backlog Watch

### Critical Items Needing Maintainer Attention

| Item | Age | Priority | Reason |
|---|---|---|---|
| **Issue [#1981](https://github.com/nanocoai/nanoclaw/issues/1981) — systemd detection on headless Linux** | 87 days (since Apr 24) | **High** | Related bug #2482 closed today, but root cause persists. v2 setup wizard broken for Hetzner/Ubuntu users. |
| **PR [#2544](https://github.com/nanocoai/nanoclaw/pull/2544) — Telegram reactions + callback_query** | 62 days (since May 18) | **Medium** | Clean feature enhancement, no review activity. |
| **PR [#2752](https://github.com/nanocoai/nanoclaw/pull/2752) — Discord inbound attachments** | 37 days (since Jun 12) | **Medium** | Channel parity issue — Discord users can't send images or files to agent. |
| **PR [#3078](https://github.com/nanocoai/nanoclaw/pull/3078) — Session resolution anchor fix** | 1 day | **High** | Fixes multi-session fork issue in agent-shared wirings. Fresh submission. |
| **PR [#2971](https://github.com/nanocoai/nanoclaw/pull/2971) — NCC utility skill** | 12 days (since Jul 7) | **Low-Medium** | New utility skill; no review yet. |

### Duplicate/Redundant PRs
- **iMessage unification**: Two PRs ([#2999](https://github.com/nanocoai/nanoclaw/pull/2999) by `underthestars-zhy`, [#3076](https://github.com/nanocoai/nanoclaw/pull/3076) by `invisicat`) both target the same unified iMessage feature. Needs maintainer consolidation to avoid merge conflicts.

### Observation: MGA/Agent Groups Reference Issue
Issue [#2517](https://github.com/nanocoai/nanoclaw/issues/2517) (closed), about MGA rows referencing archived `agent_groups`, was discovered during a cross-check audit. While closed, the underlying data integrity pattern (reference to archived groups without unarchive-on-reference + GC) may warrant automated tooling in a future release to prevent stale references from accumulating.

---

**Summary:** NanoClaw had a high-velocity bug-fix day on July 19, 2026, resolving critical issues in message delivery (double-delivery, quota errors, silent drops) and channel polish (WhatsApp recipient validation, Signal read receipts, Slack Socket Mode). The project remains healthy with active community engagement, though two key areas need continued attention: **setup reliability on headless Linux** (a longstanding v2 blocker) and **consolidation of competing iMessage unification PRs**. The agent-runner stability work today significantly improves trust in message delivery reliability for production deployments.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-19

## Today's Overview
The NullClaw project shows minimal activity in the last 24 hours, with only one issue (already open) receiving an update and no new pull requests or releases. This reflects a low-activity period for the project. The sole active issue, #868, involves a platform-specific build failure on Android/Termux that has been open since late April and has accumulated 7 comments. No code changes, merges, or new commits were observed today. Overall project health appears stable but with a notable unresolved blocker for ARM64 Android users.

## Releases
No new releases were published today or in the recent period. The latest available release remains **nullclaw v2026.4.17**, which is referenced in the open issue.

## Project Progress
No pull requests were updated, merged, or closed in the last 24 hours. No features or fixes advanced during this period.

## Community Hot Topics
- **Issue #868** — [Bug] zig build fails on Android/Termux (aarch64) with AccessDenied on options.zig linkat  
  [GitHub](https://github.com/nullclaw/nullclaw/issues/868)  
  **Stats:** 7 comments, opened 2026-04-23, last updated today.  
  **Analysis:** This is the most active and only discussed issue. The user is trying to build NullClaw on a modern Android device under Termux using Zig 0.16.0 but encounters a filesystem permission error during linking (`linkat`). The environment is a standard LineageOS 22.2 installation. The underlying need is **cross-platform build support**, specifically enabling successful builds on Android without requiring elevated privileges or filesystem workarounds. This issue has been open for nearly 3 months without resolution, indicating it may be a challenging platform-specific problem.

## Bugs & Stability
One bug is actively tracked:
- **Issue #868** — Build failure on Android/Termux (aarch64)  
  **Severity:** Medium (blocks a major class of devices from building; does not affect desktop builds)  
  **Symptoms:** `AccessDenied` error during `zig build`, specifically when attempting to link temporary files into the output path.  
  **Status:** Open, no associated fix PR.  
  **Potential cause:** Likely related to Android's restrictive filesystem permissions (e.g., lack of `linkat` support in Termux's proot or FUSE layer, or missing `/proc/self/exe` permission).  
  **Recommendation:** This warrants further investigation, possibly by a maintainer testing on a similar environment or by adding a documentation workaround.

## Feature Requests & Roadmap Signals
No explicit feature requests were submitted today. However, the existence of Issue #868 signals a **strong user demand for Android build compatibility**. If resolved, this could broaden NullClaw's user base significantly among mobile/Linux enthusiasts. No roadmap signals (e.g., PRs or maintainer comments about upcoming features) were visible.

## User Feedback Summary
- **Pain points:** The primary frustration is the inability to build NullClaw on Android devices (aarch64) using the standard Zig toolchain. The user has provided detailed environment specs, suggesting they are invested in getting it to work.
- **Use cases:** Building NullClaw on a phone/tablet under Termux, likely for personal AI agent experimentation without a desktop computer.
- **Satisfaction:** Mixed — the issue is acknowledged but unresolved for 3 months, which may cause dissatisfaction among Android users.

## Backlog Watch
**Issue #868** is the only open item in the backlog requiring maintainer attention. It has been open for 87 days without a maintainer response or fix attempt. Important details to note:
- **Reproducer:** The user provides exact steps and environment.
- **No assignee:** No maintainer has been assigned.
- **Risk:** If unresolved, this bug may discourage contributions from mobile/ARM users and could be seen as a lack of support for non-standard environments.  
  **GitHub:** [nullclaw/nullclaw Issue #868](https://github.com/nullclaw/nullclaw/issues/868)

**Overall project health rating:** Calm / Low activity — stable but has an open platform-specific blocker that deserves attention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-19

## Today's Overview
IronClaw maintains high development velocity with 50 PRs updated in the last 24 hours and 29 merged/closed. The project is deep in a major **architecture simplification** effort (`arch-simplification §1–§10`), with core contributors systematically collapsing trait-object dispatch, eliminating dead code, and migrating the Reborn runtime toward a closed-enum architecture. Community activity is modest (5 open issues, none with high user engagement), suggesting the team is focused on internal quality improvements rather than urgent user-facing breakage. The single closed issue (#6143) signals progress on promoting Reborn to become the canonical CLI.

## Releases
No new releases published in the last 24 hours. The last pending release PR (#5598) remains open, proposing version bumps across multiple crates including breaking changes to `ironclaw_common` (0.4.2→0.5.0) and `ironclaw_skills` (0.3.0→0.4.0). When merged, this will drop the main `ironclaw` binary to 0.29.1 from the current 0.24.0.

## Project Progress — Merged/Closed PRs (29 total)
The majority of closed PRs today came from **ilblackdragon**'s architecture simplification effort (Slice B, Slice C series):

- **Architecture simplification foundational work:**
  - [#6235](https://github.com/nearai/ironclaw/pull/6235) — **Slice B**: Collapse `LocalDev*` family into `DeploymentConfig` — deployment mode is now config data, not a kernel type.
  - [#6234](https://github.com/nearai/ironclaw/pull/6234) — Deleted the dead `trust_decision` field from `RuntimeCapability*Request` family (dead code cleanup).
  - [#6233](https://github.com/nearai/ironclaw/pull/6233) — **Slice C W1a**: Activated `Authorized` seal + `RuntimeLane::from_runtime_kind` — first wiring step toward routing capability path through `authorize()`/`dispatch()`.
  - [#6237](https://github.com/nearai/ironclaw/pull/6237) — **Result-record vocabulary**: `GateRecord`/`DenyRecord` + `OutcomeRefs` for the capability-result collapse.
  - [#6238](https://github.com/nearai/ironclaw/pull/6238) — Anti-slippage ratchet for capability-path DTO collapse (type count expected to rise 14→18→11).
  - [#6236](https://github.com/nearai/ironclaw/pull/6236) — Deduplicated `SafeSummary` redaction rules into a single `ironclaw_host_api::SafeSummary`.
  - [#6229](https://github.com/nearai/ironclaw/pull/6229) — **Slice C.6**: Introduced closed `RuntimeLane` enum replacing `RuntimeAdapter`'s open trait + `dyn`.
  - [#6237](https://github.com/nearai/ironclaw/pull/6237) & [#6236](https://github.com/nearai/ironclaw/pull/6236), [#6234](https://github.com/nearai/ironclaw/pull/6234) — Additional refactoring and vocabulary additions.

- **Bug fixes:**
  - [#6250](https://github.com/nearai/ironclaw/pull/6250) — Fixed libSQL descendant queries replacing `LIKE 'prefix/%'` scans with indexed half-open range (`[prefix/, prefix0)`) — addresses a QA profiling regression.

- **CI / Infrastructure:**
  - [#6199](https://github.com/nearai/ironclaw/pull/6199) — Benchmark run against latest main (throwaway PR for dispatch testing).

## Community Hot Topics
Issue/PR activity is dominated by core contributors; community participation is low. Active items of note:

- **#6158 — [OPEN] Add zh-TW Traditional Chinese localization** ([Issue](https://github.com/nearai/ironclaw/issues/6158)) — Only community-facing issue with any discussion (2 comments). Author requests Traditional Chinese locale for WebUI v2 which currently offers zh-CN only. Low urgency but signals user demand for internationalization breadth.

- **#6249 — [OPEN] Reborn: extensions-management API parity for MCP servers** ([Issue](https://github.com/nearai/ironclaw/issues/6249)) — Filed by kirikov, tracks missing API surface (`/api/extensions/install`, `/api/extensions/{name}/activate`, `PATCH`) in the `ironclaw-reborn` binary vs. v1 gateway. Identifies a concrete feature gap.

- **#6244 — [OPEN] Agent-market deploy branch: thread-scoped MCP sessions** ([PR](https://github.com/nearai/ironclaw/pull/6244)) — Large PR (size: XL) from kirikov upstreaming programmatic MCP config, SEP-414 context propagation, and PATCH endpoint. Scope spans channel/cli, channel/web, tool/mcp, extensions, and sandbox — significant surface area.

## Bugs & Stability
One functional bug reported/fixed today:

- **[HIGH] #6247 — MCP server headers persist bearer tokens in plaintext** ([Issue](https://github.com/nearai/ironclaw/issues/6247)) — `McpServerConfig.headers` containing `Authorization: Bearer` tokens is serialized into: (1) the unencrypted `mcp_servers` settings DB row (included in backups/exports) via `add_mcp_server`/`update_mcp_server`, (2) per-job worker mounts. This is a **security-in-plaintext** regression — credentials leak into persistent storage and export files. **No fix PR linked yet**; filed by kirikov (who authored the MCP deploy branch #6244), so likely the reporter has awareness of the code path.

- **[MEDIUM] #6250 — libSQL descendant listing regression** ([PR](https://github.com/nearai/ironclaw/pull/6250)) — Already fixed via merged PR. QA profiling identified `LIKE 'prefix/%'` scans causing slow index behavior; replaced with indexed half-open range to match PostgreSQL backend behavior.

## Feature Requests & Roadmap Signals
- **#6143 — Promote Reborn to canonical CLI** ([Issue](https://github.com/nearai/ironclaw/issues/6143), closed) — Staged transition plan: rename v1 to `ironclaw-v1`, promote Reborn as `ironclaw`. Now closed, suggesting the plan is approved or in progress.

- **#6248 — Credential preflight before approval/sandbox** ([Issue](https://github.com/nearai/ironclaw/issues/6248)) — Blocked on `auth_resume` design. Would probe `RuntimeCredentialAccountResolver::has_account` for each required `ProductAuthAccount` before user approval gates. Likely a next-version feature given the auth infrastructure work underway.

- **#6246 — `config set CX` CLI capability configuration** ([PR](https://github.com/nearai/ironclaw/pull/6246)) — Post-onboarding UX: connect Google/Gmail, set LLM credentials, toggle Slack, rotate WebUI token without editing `config.toml`. Open PR targeting the user experience gap identified during local onboarding work.

## User Feedback Summary
Limited user signals in this window:

- **Positive signal**: The zh-TW localization request (#6158) suggests users are actively using WebUI v2 and care about their browser locale preference being respected. No frustration expressed, but the lack of Traditional Chinese option where Simplified Chinese exists is a parity gap.

- **Pain point (security)**: The bearer-token-in-plaintext issue (#6247) represents real security friction for MCP users — credentials leaking into unencrypted DB rows and export files is a serious operational concern. No user complaints have appeared yet likely because the feature is still in deploy-branch state.

- **Operational friction**: The libSQL descendant listing performance fix (#6250) emerged from QA profiling, suggesting users or testers hit slow queries — now patched.

## Backlog Watch
- **#5598 — Release PR (open since 2026-07-03)** ([PR](https://github.com/nearai/ironclaw/pull/5598)) — Stale for 16 days despite including breaking changes across multiple core crates. The `ironclaw` version jump (0.24.0→0.29.1) is significant. This is the single largest blocker for downstream consumers — no published release means all these architecture improvements are unavailable to end-users. Given the volume of code changing daily, release managers may be waiting for the architecture simplification to stabilize before cutting a release.

- **No long-unanswered community issues**: All open issues are recent (last 72 hours) with no older than 3 days. The project is responsive to filed concerns.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for 2026-07-19.

---

## LobsterAI Project Digest — 2026-07-19

### 1. Today's Overview
Project activity is moderate. While no new issues were created in the last 24 hours, the maintainers have been active with a new release (v2026.7.17) and two merged pull requests. The open issue queue is entirely composed of "stale" items, suggesting a backlog of unresolved bugs and feature requests. The community is showing engagement through PR contributions, but concern is warranted for the 18 critical and untriaged bugs that have seen no resolution in over three months.

### 2. Releases
**[LobsterAI 2026.7.17](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.7.17)** was released on July 17, 2026.

**Key Changes:**
- `feat(cowork)`: Structured run failure details are now surfaced in the error UI, improving debugging for users when workflows fail.
- `feat(service)`: Service deployment data now has persistence, ensuring configuration and state are retained across restarts.
- `feat(skin)`: A new skin-related feature was added (description truncated in source data).

**Migration Notes:** No breaking changes or specific migration steps were mentioned in the changelog.

### 3. Project Progress
Two pull requests were merged/closed in the last 24 hours, indicating progress in the Agent and IM (Instant Messaging) modules:

- **Merged: [PR #1353](https://github.com/netease-youdao/LobsterAI/pull/1353)** — `feat(agent)`: Agent skill selector now includes "Select All" and "Clear" buttons, improving the user experience when managing agent capabilities.
- **Merged: [PR #1464](https://github.com/netease-youdao/LobsterAI/pull/1464)** — `fix(im)`: Added duplicate validation for instance names and credential IDs across DingTalk, Feishu, and QQ platforms. This prevents creation of duplicate bot instances and reduces the risk of message processing conflicts.

**Open PR: [PR #2358](https://github.com/netease-youdao/LobsterAI/pull/2358)** — An in-progress fix to show localized feedback when a session rename fails, addressing a long-standing usability issue (Issue #670).

### 4. Community Hot Topics
No single issue has drawn significant recent comment or reaction volume. However, four issues are notable for being directly linked to the application's core usability:

- **[Issue #1293](https://github.com/netease-youdao/LobsterAI/issues/1293)** — **Custom MCP not working.** Users report that custom MCP services are not being updated in the OpenClaw engine, rendering them unusable. This is a critical feature for developers extending the agent's capabilities.
- **[Issue #1296](https://github.com/netease-youdao/LobsterAI/issues/1296)** — **Uploading a 3MB long image crashes the page.** A severe stability issue that makes the system "completely unavailable" after the error occurs.
- **[Issue #1298](https://github.com/netease-youdao/LobsterAI/issues/1298)** — **False "input too long" error.** A model that passes a connection test immediately rejects a two-character query, indicating a flawed token count or context window estimation.
- **[Issue #1307](https://github.com/netease-youdao/LobsterAI/issues/1307)** — **Cannot edit model provider config after closing edit panel.** A significant UX regression where the settings panel becomes permanently read-only after opening and closing it once.

**Analysis:** The underlying user need is clear: there is a strong desire for stability and core functionality over new features. The community is actively testing the system, but their feedback is hitting a wall of open, unanswered reports.

### 5. Bugs & Stability
Six open issues were updated today, all of which are "stale" (created April 2, 2026). No new bugs were filed. The severity of the existing backlog is high:

- **Critical (High Severity):**
    - **[Issue #1296](https://github.com/netease-youdao/LobsterAI/issues/1296)** — Page crash on image upload. No fix PR exists.
    - **[Issue #1293](https://github.com/netease-youdao/LobsterAI/issues/1293)** — Custom MCP broken. Blocks core agent customization features.
- **Major (Medium Severity):**
    - **[Issue #1298](https://github.com/netease-youdao/LobsterAI/issues/1298)** — False input length error. Anti-feature preventing normal use.
    - **[Issue #1307](https://github.com/netease-youdao/LobsterAI/issues/1307)** — Settings panel lock-up. A clear UI regression.
    - **[Issue #1305](https://github.com/netease-youdao/LobsterAI/issues/1305)** — Wrong title in scheduled task history. A data display error.
- **Minor (Low Severity):**
    - **[Issue #1302](https://github.com/netease-youdao/LobsterAI/issues/1302)** — Feature request for line numbers in code blocks (classified as a bug/UX improvement).

### 6. Feature Requests & Roadmap Signals
The main signals for future development come from the merged PRs and a single feature request issue:

- **Agent Configuration UX (High Likelihood):** The merger of [PR #1353](https://github.com/netease-youdao/LobsterAI/pull/1353) (Select All/Clear for Agent skills) suggests the team is actively polishing the Agent management interface.
- **IM Platform Robustness (High Likelihood):** [PR #1464](https://github.com/netease-youdao/LobsterAI/pull/1464) (duplicate validation for IM instances) indicates a focus on stabilizing multi-instance support for enterprise chat platforms.
- **Code Display Enhancement (Medium Likelihood):** [Issue #1302](https://github.com/netease-youdao/LobsterAI/issues/1302) is a clear feature request for adding line number toggles to code blocks. Given the project's focus on AI-assisted coding ("cowork"), this is a strong candidate for a future release.

**Prediction:** The next version will likely continue the "cowork" stability theme and may include a fix for the session rename feedback (PR #2358) and the code line number feature.

### 7. User Feedback Summary
User feedback is overwhelmingly negative, focused on functionality breakdowns and lack of response.

- **Pain Points:**
    - **System Crashes:** A user reports that uploading a 3MB image makes the entire application "completely unusable" on subsequent tasks ([Issue #1296](https://github.com/netease-youdao/LobsterAI/issues/1296)).
    - **Useless Errors:** Users are frustrated by system errors that do not reflect actual problems (e.g., "input too long" for two-character queries) ([Issue #1298](https://github.com/netease-youdao/LobsterAI/issues/1298)).
    - **UI Blockers:** A user is unable to edit model provider settings after simply opening a panel, forcing a likely app restart ([Issue #1307](https://github.com/netease-youdao/LobsterAI/issues/1307)).
    - **Data Inconsistency:** Deleted scheduled tasks show incorrect names in history logs, eroding trust in data integrity ([Issue #1305](https://github.com/netease-youdao/LobsterAI/issues/1305)).
- **Satisfaction Indicators:** The existence of community PRs (e.g., #1353, #2358) shows that developers outside the core team are willing to invest time to fix problems, indicating a technically invested community that values the project enough to contribute directly.

### 8. Backlog Watch
The entire current open issue set is in the backlog. The following are the most critical items that have received no response from maintainers in over three months:

- **[Issue #1293](https://github.com/netease-youdao/LobsterAI/issues/1293) — Custom MCP Unusable (Age: 108 days)**
    A core extensibility feature is completely broken with no acknowledgment.
- **[Issue #1296](https://github.com/netease-youdao/LobsterAI/issues/1296) — Upload Crash (Age: 108 days)**
    A data-loss-level crash bug that is blocking a user entirely.
- **[Issue #1298](https://github.com/netease-youdao/LobsterAI/issues/1298) — False Token Limit (Age: 108 days)**
    A fundamental model interaction bug that makes the system appear faulty.
- **[Issue #1305](https://github.com/netease-youdao/LobsterAI/issues/1305) — Task History Display Bug (Age: 108 days)**
    A data integrity issue that degrades trust in the product's reliability.

**Action Required:** The maintainers should triage these "stale" items. At a minimum, each should receive a label clarifying its status (e.g., "needs-repro," "confirmed-bug," "planned") to reduce community frustration from silence.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-19

## Today's Overview
The Moltis project shows moderate activity today, with three pull requests updated in the last 24 hours and no new issues opened or releases published. Two PRs were successfully closed (one merged fix, one resolved enhancement), while one new feature PR remains open for review. The absence of new issues suggests either low user bug reporting activity or that recent fixes have addressed existing concerns. Overall, the project is progressing steadily with focused feature additions and stability improvements.

## Releases
No new releases were published today. The latest releases remain unchanged from previous periods.

## Project Progress
Two pull requests were merged or closed today:

- **#1157 [CLOSED] fix(web): support ACP-only chat setup** (by penso) — This fix enables the web UI to operate correctly when only ACP (Agent Communication Protocol) agents are configured, without requiring an LLM backend. It updates onboarding flows, session headers, and model selectors to gracefully handle ACP-only environments. ([PR #1157](https://github.com/moltis-org/moltis/pull/1157))

- **#1159 [CLOSED] feat(slack): support configurable API base URL** (by penso) — Adds a configurable `api_base_url` for Slack integration (defaulting to `https://slack.com/api`), allowing deployment behind proxies or custom endpoints. This affects client construction, Socket Mode, Events API auth, outbound replies, and streaming. Also adds corresponding fields to onboarding configuration. ([PR #1159](https://github.com/moltis-org/moltis/pull/1159))

## Community Hot Topics
The most notable item today is the open PR:

- **#1158 [OPEN] feat(memory): add zvec vector database memory backend** (by demyanrogozhin) — This PR introduces an experimental vector database memory backend using Zvec and Redb, gated behind the `zvec` feature flag (included in the `full` feature set). The author describes it as a "vibe-coded" experiment for use with an external llama.cpp embedding server. Despite zero comments or reactions, this represents a significant new memory backend option that could expand Moltis's offline/self-hosted capabilities. ([PR #1158](https://github.com/moltis-org/moltis/pull/1158))

**Underlying need**: There is a desire among developers for alternative, lightweight, local-first vector storage backends that can operate without cloud dependencies, enabling fully offline agent memory and embedding workflows.

## Bugs & Stability
No new bugs, crashes, or regressions were reported in issues today. The closed fix PR #1157 addresses a specific stability concern where ACP-only setups (without LLM models) would fail during onboarding and session initialization — this is now resolved.

## Feature Requests & Roadmap Signals
Based on today's activity:
- **Configurable Slack API base URL** (PR #1159) suggests enterprise/proxy deployments are a growing use case, likely to be included in the next release.
- **Zvec memory backend** (PR #1158) is experimental but could be promoted if community testing validates stability and performance. It signals interest in diverse vector store options.
- **ACP-only deployment support** (PR #1157) indicates that users want to run Moltis purely as a multi-agent coordination layer without requiring an LLM, opening up use cases where agents handle specialized tasks independently.

Prediction: The next release will likely include the Slack URL configurability and the ACP-only fix, while the Zvec backend may incubate for one more cycle.

## User Feedback Summary
No explicit user feedback or pain points were logged in issues today. However, the two closed PRs hint at user needs:
- Users deploying Moltis behind corporate proxies or self-hosted Slack alternatives need configurable API endpoints.
- Users running agent-only environments (without LLM access) need full support without workarounds.

These indicate a user base that values deployment flexibility and offline capabilities.

## Backlog Watch
No long-unanswered issues or PRs were identified. The open PR #1158 (Zvec backend) has been open for 2 days without maintainer comments or reviews, but this is within normal review timelines for experimental features. No backlog items require immediate maintainer attention.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-19

## 1. Today's Overview
CoPaw shows **moderate activity** with 11 issues updated and 6 PRs updated in the last 24 hours. No new releases were published today. The community reports **concentrated bugfix activity** — several critical regressions are being addressed, including a session-blocking deadlock when shell commands exceed coordinator deadlines, a PATH corruption issue on Windows, and a memory recall crash from excessively long file names. Notably, **two first-time contributors** submitted PRs, indicating healthy community engagement. Three of today's five open PRs are fix-oriented, suggesting the project is in a **stabilization phase** following the recent v2.0.0.post3 release.

## 2. Releases
**None** — No releases were published in the last 24 hours. The most recent release remains **QwenPaw v2.0.0.post3** (Post release from 2026-07-17).

## 3. Project Progress
Only **one PR was merged/closed today**:

- **[PR #1071](https://github.com/agentscope-ai/QwenPaw/pull/1071) (CLOSED)** — *feat: Introduce Mattermost channel integration for message* — A first-time contributor's feature adding Mattermost channel integration, related to issue #621. This had been open since March 2026 and was finally closed, though it is unclear if it was merged or simply closed without merge.

**Notable open PRs advancing today:**
- **[PR #6248](https://github.com/agentscope-ai/QwenPaw/pull/6248)** — Fixes the critical session-blocking regression from #6056, distinguishing between user cancel (kill subprocess) and deadline offload (keep subprocess running).
- **[PR #6238](https://github.com/agentscope-ai/QwenPaw/pull/6238)** — Performance improvement: initializing driver handlers concurrently, reducing startup time for multi-MCP setups.

## 4. Community Hot Topics
The most active discussions in the last 24 hours:

- **[Issue #6240](https://github.com/agentscope-ai/QwenPaw/issues/6240) (3 comments)** — *[Bug]: 末尾出现注释显示* — User reports that after normal chat, memory annotation text (e.g., `<!-- ⟦ NEXT_RID 改为 1003...`) appears at the end of conversation output. Three comments indicate active triage, with uncertainty whether the bug is in model output formatting or web UI filtering.

- **[Issue #6245](https://github.com/agentscope-ai/QwenPaw/issues/6245) (2 comments)** — *Session permanently blocked when shell command exceeds coordinator deadline* — A regression from a previous fix (#6056). The session deadlocks until restarted. **A fix PR (#6248) already exists**, suggesting maintainers are prioritizing this.

- **[Issue #4641](https://github.com/agentscope-ai/QwenPaw/issues/4641) (2 comments, open since May)** — *qwenpaw env set → subprocess can't see it* — A long-standing request for dynamic environment variable injection into shell subprocesses. Updated today with additional discussion.

**Analyzed needs:** The community is expressing two clear themes: (1) **session reliability** — users cannot tolerate permanent blocks or output corruption during long conversations; (2) **environmental configurability** — users need runtime control over subprocess environments without restarts.

## 5. Bugs & Stability
**High Severity:**

- **[#6245](https://github.com/agentscope-ai/QwenPaw/issues/6245)** — **CRITICAL:** Session permanently blocked when shell command exceeds coordinator deadline. **Fix PR #6248 exists.** Regression from #6056.
- **[#6240](https://github.com/agentscope-ai/QwenPaw/issues/6240)** — **HIGH:** Unwanted memory annotation text appearing in conversation output. Affects UI display quality.
- **[#6239](https://github.com/agentscope-ai/QwenPaw/issues/6239)** — **HIGH:** Windows PATH concatenation drops `;` separator between User and Machine PATH, causing child processes to lose npm globals. Affects all Windows users with npm setups.
- **[#6246](https://github.com/agentscope-ai/QwenPaw/issues/6246)** — **HIGH:** `recall_history` crashes with `OSError: [Errno 36] File name too long`. **Fix PR #6247 exists** (from same author).

**Medium Severity:**

- **[#6242](https://github.com/agentscope-ai/QwenPaw/issues/6242)** — Console embedding dimension setting not sent to OpenAI-compatible APIs because `use_dimensions` is not exposed. **Fix PR #6243 exists** (first-time contributor).
- **[#6241](https://github.com/agentscope-ai/QwenPaw/issues/6241)** — Agent produces repeated output in consecutive rounds; `memory_search` may enter infinite loop. Framework-level duplicate detection is missing.
- **[#6250](https://github.com/agentscope-ai/QwenPaw/issues/6250)** — Sandbox fallback hardcodes approval prompt with no configuration to bypass. Workaround exists (`approval_level: NONE`) but is considered too heavy-handed.
- **[#6249](https://github.com/agentscope-ai/QwenPaw/issues/6249)** — TUI stuck in "warming" state when started from source. No obvious errors in logs.

**Fix PRs available for:** #6245 (PR #6248), #6246 (PR #6247), #6242 (PR #6243). This is a **strong signal of maintainer responsiveness** to recent regressions.

## 6. Feature Requests & Roadmap Signals

- **[#6244](https://github.com/agentscope-ai/QwenPaw/issues/6244)** — **Memory isolation by project.** User requests introducing "project" concepts to isolate memories between different tasks, improving retrieval accuracy. This aligns with known industry trends toward structured memory management.

- **[#4641](https://github.com/agentscope-ai/QwenPaw/issues/4641)** — **Dynamic environment variable injection into subprocesses.** Request for `env get KEY` or `--json` flag on `env list`. This is a **strong candidate for the next minor release** (v2.0.x) given it has been open since May and was updated today.

- **[PR #6237](https://github.com/agentscope-ai/QwenPaw/pull/6237)** — **Improved history recall with date-aware queries and complete conversational turns.** This enhancement to Scroll memory is still open and would improve memory retrieval quality.

**Prediction:** The next version (likely v2.0.0.post4 or v2.1.0) will likely include the memory isolation feature (#6244) and the env set subprocess fix (#4641), as both address common user pain points identified in recent weeks.

## 7. User Feedback Summary
- **Pain point: Session reliability** — Users report that a single hung shell command can permanently lock a session (#6245). This is a fundamental UX issue.
- **Pain point: Cross-platform PATH handling** — Windows users are losing npm and other global tool paths due to semicolon concatenation bugs (#6239). This affects developer workflows.
- **Pain point: Memory corruption in UI** — Users see raw internal annotation text (`<!-- ⟦ ...`) in their chat output, breaking the illusion of a clean assistant experience (#6240).
- **Pain point: Sandbox inflexibility** — When sandbox is unavailable, users cannot bypass the approval prompt without disabling all approvals (`approval_level: NONE`) (#6250). Users want granular control.
- **Positive signal:** Two first-time contributors submitted PRs (#6243, #1071), indicating the project has good onboarding and documentation for new developers.
- **Negative signal:** Issue #6249 reports that source-based TUI startup is stuck in "warming" state. This suggests potential documentation gaps or environment-specific issues for developers.

## 8. Backlog Watch
- **[Issue #4641](https://github.com/agentscope-ai/QwenPaw/issues/4641) (open since 2026-05-23, updated today)** — *qwenpaw env set → subprocess can't see it* — Important configuration feature request that has been open for nearly 2 months. Updated today with additional discussion, suggesting community interest remains high. **Needs maintainer prioritization.**

- **[Issue #6241](https://github.com/agentscope-ai/QwenPaw/issues/6241) (v1.1.12, older version user)** — *Agent repeated output + memory_search infinite loop* — User on an older version (v1.1.12.post2) reports a duplicate detection gap. While the system has a warning log, it does not prevent the loop. **Potential regression from v2.0.0 series that may affect older version users migrating.**

- **[Issue #6223](https://github.com/agentscope-ai/QwenPaw/issues/6223) (updated today)** — *Release Duty: v2.0.0.post3 Installation Verification* — Automated release verification issue that has passed its deadline (2026-07-17). This is an internal process item, not a user-facing concern, but may indicate verification delays.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-19

## Today's Overview

ZeroClaw shows **sustained high development velocity** with 50 issues and 50 PRs updated in the last 24 hours, concentrated across security infrastructure, plugin architecture, and channel reliability. The project closed 11 issues and 3 PRs while maintaining 39 open active issues and 47 open PRs — a healthy ratio indicating both steady triage and ambitious feature work. A notable structural shift is underway: a series of stacked PRs by `JordanTheJet` (PRs #9137–#9142) are laying foundational WASM plugin infrastructure (egress policies, event routing, durable schedulers, TLS profiles, scoped secrets), suggesting ZeroClaw is nearing a major plugin capabilities milestone. No new releases were cut today, but the breadth of in-flight RFCs and merged PRs signals a significant version uplift likely in the coming weeks.

## Releases

No new releases were published in the last 24 hours. The latest available version remains unchanged.

## Project Progress

**Merged/Closed PRs (3 total):**
- **#9055** — `fix(docs): make translation refresh reproducible` (merged): Standardizes mdBook generation so clean checkouts no longer depend on build artifacts, improving CI reliability for documentation refreshes.
- Two additional PRs were closed/merged but did not appear in the top-20 by comment count; full triage details are limited without complete PR listings.

**Key closed issues:**
- **#5862** — Fixed: ZeroClaw not recognizing its own `cron` capability. Agent now knows it can schedule recurring tasks.
- **#8177** — RFC closed as `wontfix`: Supply chain signing with hardware PGP and SLSA provenance was proposed but not accepted in its current form.
- **#2079** — Feature completed: GitHub is now a native channel (agent can observe and act on repos).
- **#6378** — Feature completed: Discord bot can now be restricted to specific channels via `allowed_channels` config.
- **#6672** — Bug fixed: `reasoning_content` now properly forwarded in tool-call loops with Xiaomi thinking models.
- **#7248** — Feature completed: Cached input tokens persisted and included in cost accounting.
- **#5573** — Feature completed: SMTP email sending as a cron-enabled channel for scheduled reports.
- **#8056** — CI enhancement merged: Cargo audit, lockfile check, and npm dependency review now gate PR merges.

## Community Hot Topics

The most active discussions reveal deep engagement with security architecture and channel reliability:

1. **#9127 — RFC: Abstract a `KeySource` trait for master-key material** (6 comments, updated today)
   *Link: zeroclaw-labs/zeroclaw Issue #9127*
   Proposes classifying how master encryption keys are sourced across deployment forms (env vars, files, hardware-backed). Builds on ZeroClaw's existing ChaCha20-Poly1305 AEAD infrastructure. The 6 comments suggest strong maintainer interest in formalizing this abstraction.

2. **#8424 — RFC: Workspace-relative forbidden path patterns and `.zeroclawignore`** (7 comments, needs-author-action)
   *Link: zeroclaw-labs/zeroclaw Issue #8424*
   Requests that forbidden paths block AI agent access to sensitive *workspace-internal* files (`.env`, `rust-toolchain.toml`, configs). Current mechanism only blocks outside-workspace paths. Blocked on author response.

3. **#6293 — RFC: Air-gapped execution mode with companion daemon over Unix socket** (6 comments, blocked)
   *Link: zeroclaw-labs/zeroclaw Issue #6293*
   Proposes splitting ZeroClaw into offline agent + online companion daemon connected via Unix socket for enclave/high-security deployments. Blocked status suggests unresolved architectural complexity.

4. **#8600 — Feature: Easy per-chat model switching for multi-model providers** (3 comments, 1 👍)
   *Link: zeroclaw-labs/zeroclaw Issue #8600*
   User migrating from moltis wants to switch between any model a provider supports at runtime. The single 👍 and short thread suggest broad interest but early-stage design.

5. **#7759 — Feature: Decouple gateway WebSocket lifetime from agent turn lifecycle** (4 comments, in-progress)
   *Link: zeroclaw-labs/zeroclaw Issue #7759*
   Client disconnects should not cancel in-flight agent turns. Related to **#8559** (agents stop when exiting chat window). These two issues signal a critical UX pain point being actively addressed.

## Bugs & Stability

**High-Severity Bugs (P1, active):**
- **#8559** (P1, severity S1) — Agents stop working when user exits web dashboard chat window. *Status: in-progress.* Related PR #7759 aims to decouple WebSocket from turn lifecycle.
  *Link: zeroclaw-labs/zeroclaw Issue #8559*

- **#8505** (P1, severity S1) — Telegram channel cannot be configured; `channels doctor` reports not set up even after quickstart. Agent only responds in CLI.
  *Link: zeroclaw-labs/zeroclaw Issue #8505*

**Medium-Severity Bugs (P2-P3, active or stale):**
- **#6002** (P2, severity S1, stale) — Telegram channel message not clearly addressed to assistant; bot responds to all messages.
- **#6724** (P3, severity unrated) — Enabling Signal/Voice Call channels with empty credentials causes supervisor crashloop (~2s restart cycle).
- **#7911** (P2) — `install.sh` selects generic Linux binary on Android/Termux instead of `aarch64` variant.
- **#6517** (P2, severity S2) — Context overflow causes hallucination/topic drift in long conversations (Discord/Kimi). Closed.

**Today's fix PRs (new):**
- **#9157** — Fixes hardware serial response frame desynchronization (stale frames poisoning later requests).
- **#9090** — Enforces tool-call pairing at a single chokepoint, fixing Anthropic 400 errors from mismatched `tool_use`/`tool_result` blocks.
- **#9102** — Strips unhandled non-image media markers (`[AUDIO:]`, `[VIDEO:]`, etc.) before provider dispatch.
- **#9110** — Closes timing-attack vulnerability in Lark channel verification token comparison (uses `constant_time_eq`).
- **#9113** — Adds idle `read_timeout` to streaming HTTP clients (OpenAI/Compatible) to prevent hangs.
- **#9140** — Clears branch-isolated clippy warnings in Telegram and Mattermost channel code.

## Feature Requests & Roadmap Signals

**High-probability near-term features (based on in-progress status and maintainer activity):**

1. **WASM Plugin Ecosystem** — The stacked PR series #9137–#9142 (all by `JordanTheJet`, all sized XL) delivers: egress policy authorization, typed event routing, durable cron scheduler outbox, TLS profile materialization, and scoped secrets for plugins. This is the most significant architectural initiative visible and will likely be in the next release.

2. **Gateway OpenAI-compatible endpoint** — PR #8486 (XL, in-progress) adds a RESTful OpenAI Chat Completions endpoint to the gateway, enabling integration with LangChain, Continue.dev, Aider, and SDK clients. Strong user demand signal.

3. **SearXNG Search Support** — Issue #5316 (in-progress, 5 comments) adds privacy-focused search provider with DuckDuckGo CAPTCHA detection improvements.

4. **Telegram Multi-Message Mode** — Issue #8445 (in-progress) sends each agent turn as a separate message instead of concatenating all turns into one.

5. **Slack Thread Context Hydration** — Issue #6055 (in-progress) backfills prior thread history on first bot mention, eliminating re-@mention requirement.

**Longer-term roadmap signals (accepted/blocked RFCs):**
- Air-gapped enclave mode (#6293)
- OCI-compliant registries for WASM plugin distribution (#7497)
- Cross-turn OTel conversation correlation (#8933)
- Pre-turn natural language routing extraction (#7431)

## User Feedback Summary

**Satisfaction signals:**
- Users successfully deploying cron-based email reports (closed #5573) and Discord channel-restricted bots (closed #6378).
- Cost accounting improvements (closed #7248) praised via cached token persistence.
- GitHub native channel (closed #2079) reduces need for custom webhook glue.

**Pain points:**
- **Web UI turn cancellation** — Exiting the web dashboard kills agent tasks, preventing background work. Multiple related issues (#7759, #8559) with active fix PRs.
- **Telegram configuration confusion** — Quickstart leaves bot non-functional on Telegram despite CLI working (#8505). User frustration evident.
- **Slack thread UX friction** — Must re-@mention bot on every message in thread mode (#6055). Workaround exists but degraded experience.
- **Android/Termux installation broken** — Incorrect binary selection (#7911).
- **Multi-model switching** — Former moltis user finds per-chat model selection difficult (#8600).
- **Context overflow hallucination** — Long conversations degrade quality (#6517, now closed but fix details unclear).
- **OpenRouter model fallbacks unsupported** — Single-model string prevents automatic failover (#8138).

## Backlog Watch

**Issues needing maintainer response (stale or awaiting triage):**

1. **#8424 — Workspace-relative forbidden paths** (updated 2026-07-18, `needs-author-action`) — User proposed `.zeroclawignore` to protect internal workspace files. Blocked on author providing requested clarifications. High-value security feature.

2. **#6002 — Telegram not clearly addressed to assistant** (updated 2026-07-18, stale since May) — Workflow-blocking behavior on Telegram. Marked stale; no resolution path visible.

3. **#8138 — OpenRouter model fallbacks** (updated 2026-07-18, blocked) — Simple config addition (`fallback_models`) awaiting maintainer review. Low implementation complexity, high user value.

4. **#9127 — KeySource trait RFC** (updated today, `needs-author-action`) — Authored by REL-mame who is also driving PR #8486. Likely awaiting their continued engagement; not genuinely abandoned.

5. **#7497 — OCI registries for WASM plugins** (updated 2026-07-18, blocked) — Might be superseded by JordanTheJet's in-progress plugin infrastructure (PRs #9137–#9142), which appears to address similar concerns through a different architecture. Potentially deprecated.

6. **#4853 — Installing skills from `.well-known` URI** (updated 2026-07-18, accepted) — Important cross-project standardization effort. Waiting for external standards body (agentskills/agentskills PR #254) to finalize spec. No ZeroClaw action item yet.

**Recommendation:** The stale Telegram issues (#6002, #8505) and blocked OpenRouter feature (#8138) represent the highest-impact backlog items for user experience. The WASM plugin work (#9137–#9142) appears to be absorbing significant architectural attention, which may delay smaller but high-user-value features like model fallbacks and path-based security controls.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*