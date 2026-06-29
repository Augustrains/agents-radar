# OpenClaw Ecosystem Digest 2026-06-29

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-29 02:06 UTC

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

Here is the OpenClaw project digest for 2026-06-29, based on the provided GitHub data.

---

## OpenClaw Project Digest — 2026-06-29

### 1. Today's Overview
The OpenClaw project is experiencing a high-traffic, healthy, but strained development cycle. There is significant activity across a broad surface area, with 500 updated issues and 500 updated pull requests in the last 24 hours, indicating a high volume of community engagement, bug reporting, and ongoing development work. While a new beta release was published, the project’s health is tempered by a large, persistent backlog of complex, long-standing issues (many from months ago) and a high number of open PRs that appear stalled or awaiting maintainer review. Session state integrity, security, and data loss remain the dominant themes driving the most urgent work.

### 2. Releases
- **v2026.6.11-beta.2** (openclaw 2026.6.11-beta.2) was published.
  - **Highlights:**
    - **Enhanced Channel Control:** Adds Slack relay mode, a native `/oc_queue` command for Mattermost, and per-DM model overrides, improving automation and configuration flexibility for chat operations.
    - **Richer Operational...** (details cut off in original data).

### 3. Project Progress
- **Merged/Closed PRs & Issues:** 71 issues and 86 PRs were closed or merged today. This shows active resolution effort.
- **Key Fixes Advanced:**
    - **Critical Model Failover:** PR #97619 (`fix(agents): escalate model_not_found to fallback when fallbacks are configured`) addresses a critical resilience gap where a decommissioned primary model would cause a hard error instead of engaging configured fallbacks.
    - **OOM Prevention in Plugins:** PR #97620 (`fix(google-meet): bound Drive document export reads to prevent OOM`) adds a 16 MiB cap to file reads from Google Drive to prevent out-of-memory crashes.
    - **Platform Parity:** PR #59859 (`feat: cute GTK-native Linux App`), linked to the long-standing Issue #75, is progressing as an open PR, aiming to bring a first-class desktop client to Linux users.
    - **Plugin Improvements:** PR #97598 and #97595 fix UTF-16 truncation bugs in iMessage and Feishu channels, preventing malformed data. PR #97617 fixes a bug where plugin debug logging would stop working after a runtime level change.

### 4. Community Hot Topics
The community is most engaged with critical issues affecting core functionality and security.

- **[Issue #75: Linux/Windows Clawdbot Apps](https://openclaw/openclaw Issue #75)** (110 comments, 81 👍)
    - **Analysis:** This is the most active issue by a wide margin, reflecting intense and sustained demand for official desktop clients on major operating systems (beyond macOS/iOS/Android). This is a top-tier feature gap for the project.
- **[Issue #88838: Track core session/transcript SQLite migration](https://openclaw/openclaw Issue #88838)** (36 comments, 3 👍)
    - **Analysis:** A high-priority maintainer issue tracking a complex, months-long architectural migration to a new SQLite-based storage backend. The high comment count indicates significant technical complexity and coordination required for this critical infrastructure change.
- **[Issue #88312: Codex app-server turn-completion stall regression](https://openclaw/openclaw Issue #88312)** (18 comments, 4 👍)
    - **Analysis:** A P1 regression where a previously fixed bug has resurfaced, affecting users of the Codex (ChatGPT Plus) integration. The user frustration is clear, and the label "regression" signals a high-priority for re-investigation.
- **[Issue #77598: Track live dev agent behavior and trajectory](https://openclaw/openclaw Issue #77598)** (22 comments, 1 👍)
    - **Analysis:** A unique maintainer-led observational study of a live development agent. The high engagement suggests the community is deeply interested in agent behavior, reliability, and observability.

### 5. Bugs & Stability
The project is struggling with a significant number of P1 and P2 bugs, many of which are regressions or have remained open for long periods.

**Critical / P1 Regressions:**
- **[Regression] Codex turn-completion stall (Issue #88312):** A P1 regression where the agent fails to confirm task completion. No fix PR is currently linked.
- **[Regression] Bare `/new` & `/reset` no longer trigger persona greetings (Issue #77733):** This regression in v2026.5.3 disrupts a core user experience flow.
- **[Regression] Discord channel not loaded (multiple versions) (Issue #77930):** A complex regression that appears to have been introduced and then partially fixed across different beta versions.

**Critical / P1 Non-Regressions:**
- **[Issue #86538: Session write-lock timeouts:** Blocks subagent delivery lanes and causes lifecycle failures. A linked PR is open, indicating active work.
- **[Issue #76038: Stuck Session Recovery 双重失效:** (Stuck Session Recovery dual failure + high latency). A P1 bug causing gateway unresponsiveness and systemd kills, particularly under heavy load.
- **[Stable] Issue #78493: `sudo openclaw update` creates mixed ownership:** This P1 bug can corrupt user configs and cause startup failures for a wide range of users.

**High-Severity Stability Issues (Impact: message-loss, crash-loop, data-loss):**
- **Issue #83184 (Closed):** Heartbeat-driven replies causing delivery blocks. This was fixed, but shows the sensitivity of the session management system.
- **Issue #86827 (Closed):** Group chat sessions stuck in 'failed' state dropping all subsequent messages. Another resolved issue in this fragile area.
- **Issue #76171 (Closed):** Stale worker processes accumulating and causing high host load. A resolved performance/availability bug.
- **Issue #55334 (Open):** Unbounded `sessions.json` growth leading to gateway OOM. A long-standing P1 memory leak.

### 6. Feature Requests & Roadmap Signals
- **High Demand (Likely in Next Release):**
    - **Desktop Client Parity:** Issue #75 (Linux/Windows apps) is the highest-demand feature. The existence of PR #59859 strongly suggests a Linux app is a top priority for the next major release.
    - **Platform/Channel Feature Parity:**
        - **Telegram Bot-to-Bot (Issue #79077):** High community demand (8 👍) for new Telegram features. Likely to be tackled soon given the platform's popularity.
        - **Control UI i18n & UX (Issue #79034, #79458):** Multiple requests for localization (e.g., Chinese, Swedish) and friendlier session identifiers (PR #96998) indicate a push to make the web UI usable for a global audience.
- **Medium Term (On the Roadmap):**
    - **Architectural Foundations:**
        - **SQLite Transcript SDK (Issues #79902, #79903, #79904, #79905):** A set of related features to build a robust, queryable SDK on top of the new SQLite runtime. This is essential for plugin and app developers.
        - **Gateway-Lite Mode (Issue #86881):** A request for a deterministic, headless deployment mode, which would broaden OpenClaw's use case to more DevOps-style automation.
    - **Security Enhancements:**
        - **MCP Tool Approval (Issue #78308):** Extending the existing channel-mediated approval pipeline to MCP tools is a clear security priority, even if progress is currently slow.

### 7. User Feedback Summary
- **Pain Points (Dissatisfaction):**
    - **Instability & Regressions:** Users are experiencing frequent regressions, particularly in session handling, channel delivery (Discord, Telegram), and core agent behavior (greetings, `/new`). The "bug, regression" label is common.
    - **High Latency & OOMs:** Issues like #86538 (write-lock timeouts), #55334 (OOM from unbounded growth), and #76038 (stuck sessions) point to significant performance and reliability problems under load, leading to user frustration.
    - **Complex Debugging:** Users are spending hours debugging issues caused by silent plugin loader failures (Issue #78301) and confusing config errors (Issue #77802).
    - **Lack of Transparency:** The "reasoning default silently flipped to on" bug (Issue #73182) highlights user anger at UI/UX changes that increase cost without clear communication.
- **User Use Cases (Satisfaction Drivers):**
    - **Multi-Platform Messaging:** The core use case is clearly deploying an AI agent across multiple chat platforms (Discord, Telegram, Slack, etc.).
    - **Advanced Workflows:** Users are heavily leveraging features like subagents, MCP tools, cron jobs, and developer agents, indicating a sophisticated user base building complex autonomous systems.
    - **Desktop Presence:** The intense demand for Linux/Windows apps shows users want to move beyond a purely CLI/server experience and manage their agents from dedicated desktop workflows.

### 8. Backlog Watch
Several high-impact issues and PRs have been open for weeks or months without resolution, posing a growing risk to project stability.

- **Issue #55334 (Mar 26 — P1):** `[perf]: sessions.json unbounded growth causes gateway OOM`. This is a critical, long-standing memory leak that can crash the entire gateway. Despite being P1, it lacks an associated fix PR.
- **Issue #74484 (Apr 29 — P1):** `Gateway pairing scope deadlock`. A security/authentication issue that can lock users out of their own CLI. A complex, multi-area issue needing cross-team attention.
- **Issue #74586 (Apr 29 — P1):** `AM embedded run aborts memory_search tool calls`. A P1 bug in a major plugin (`active-memory`) that mis-classifies tool completions as timeouts.
- **Issue #73182 (Apr 28 — P1):** `Reasoning default silently flipped to on for Claude models`. A P1 financial and UX bug that has been open for over two months without a fix, suggesting deep architectural complexity or lack of priority.
- **Long-Standing PRs:** Many PRs with labels like `needs-proof` and `waiting-on-author` (e.g., #58421, #59214) have been open since March or April, indicating a bottleneck in the review and merge process for community contributions.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report on the AI agent and personal AI assistant open-source ecosystem.

---

## Cross-Project Comparison Report: AI Agent Open-Source Ecosystem

**Date:** 2026-06-29
**Analyst:** Senior Ecosystem Analyst

### 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by a high-velocity, multi-threaded development cycle, with projects grappling with the tension between rapid feature iteration and fundamental stability. The ecosystem is bifurcating into two dominant patterns: monolithic, all-in-one platforms (OpenClaw, ZeroClaw) and modular, embeddable runtimes (NanoBot, Hermes Agent). A universal emphasis on multi-channel support (Discord, Telegram, Slack, Matrix) is now table stakes, with the competitive frontier shifting to session reliability, agent-to-agent delegation, granular security controls, and deterministic workflow execution. The community is increasingly vocal about production-grade concerns—data integrity, memory management, and observable behavior—indicating a maturation from experimental toys to operational tools.

### 2. Activity Comparison

| Project | Issues (Updated 24h) | PRs (Updated 24h) | Release Today | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | Yes (beta) | 🟡 Strained |
| **ZeroClaw** | 50 | 50 | No | 🟢 Active |
| **Hermes Agent** | 50 | 50 | No | 🟢 Active |
| **IronClaw** | 3 | 43 | No | 🟢 Active |
| **NanoBot** | 7 | 24 | No | 🟢 Very Active |
| **NanoClaw** | 1 | 6 | No | 🟡 Moderate |
| **CoPaw** | 6 | 8 | No | 🟡 Moderate |
| **LobsterAI** | 5 (stale) | 5 (stale) | No | 🔴 Low |
| **Moltis** | 1 | 2 | No | 🔴 Low |
| **PicoClaw** | 1 | 2 | No | 🔴 Maintenance |
| **NullClaw** | 1 (closed) | 0 | No | 🟢 Quiet |
| **TinyClaw** | 0 | 0 | No | 🔴 Inactive |
| **ZeptoClaw** | 0 | 0 | No | 🔴 Inactive |

### 3. OpenClaw's Position

OpenClaw remains the **reference implementation** and **largest ecosystem**, evidenced by its dominant volume of 500 issues and 500 PRs updated in a single day. Its advantages include the most extensive channel integration set (Discord, Slack, Mattermost, iMessage, Feishu) and the deepest community engagement, exemplified by Issue #75 (Linux/Windows desktop apps) with 110 comments and 81 upvotes—the highest-demand feature across any project.

**Technical Approach Differences:**
- **Architecture:** OpenClaw’s "thick client" architecture (local SQLite runtime for transcripts, gateway-lite mode) contrasts with Hermes Agent's containerized sandbox model or ZeroClaw's WASM plugin system.
- **Stability Cost:** OpenClaw’s breadth comes at a cost. It is battling a significant number of P1 regressions (session stalls, greeting failures, Discord channel loading) and a massive backlog of complex, long-standing issues. The ecosystem perceives OpenClaw as *powerful but fragile*.
- **Community Size:** On sheer volume alone, OpenClaw’s community is an order of magnitude larger than any other project. However, ZeroClaw and Hermes Agent show higher *per-contributor throughput*, suggesting more efficient core teams.

### 4. Shared Technical Focus Areas

A set of common requirements is emerging across multiple projects, indicating the maturation of the platform layer:

- **Session State Integrity:** OpenClaw (SQLite migration, write-lock timeouts), NanoBot (corrupt session file repair), and ZeroClaw (cron "NO_REPLY" sentinel) all struggle with reliable session persistence and recovery. This is the #1 source of critical bugs.
- **Security Hardening:** NanoClaw (symlink CVE-59), ZeroClaw (MCP scoping silent no-op), Hermes Agent (WhatsApp CVE, Matrix room isolation), and OpenClaw (path traversal) all received security patches this period. Security is no longer an afterthought.
- **Deterministic Workflows:** Hermes Agent (Issue #5354, "Lobster-style" deterministic engine), ZeroClaw (SOP step schema enforcement, goal mode runtime), and OpenClaw (cron jobs, developer agents) are all building structured, non-LLM-dependent execution paths.
- **Multi-Platform Desktop Parity:** OpenClaw (Linux/Windows demand via Issue #75), Hermes Agent (Windows console flash, macOS recovery screen bugs), and NanoClaw (Discord, Telegram integration PRs) all highlight the gap between powerful server components and polished desktop clients.
- **Platform-Specific Bugs:** Windows users are disproportionately affected: OpenClaw (mixed ownership), ZeroClaw (UTF-8 BOM), Hermes Agent (console flash), and LobsterAI (DB lock on Windows) all show lower parity on non-macOS platforms.

### 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | Hermes Agent | NanoBot | IronClaw |
|---|---|---|---|---|---|
| **Primary Target User** | Power users, multi-platform teams | Developers, DevOps workflows | Hobbyists, single-user desktop | Minimalists, 1:1 chat | Enterprise, regulated workflows |
| **Key Architecture** | Monolithic, SQLite-based | WASM plugin engine, SOP engine | Container sandbox, TUI-focused | "Keep it tiny," skill files | Crate-based, multi-tenant |
| **Differentiator** | Widest channel support | Structured goal/workflow modes | Desktop-first, local-first | Simplicity, low overhead | Capability policies, OAuth |
| **Stability Philosophy** | "Ship fast, fix regressions" | "Incremental, version-tracked" | "Community-driven, reactive" | "Minimal surface, high reliability" | "Feature-gated, core-contributor" |

**Key Insights:**
- **ZeroClaw is the most architecturally ambitious**, investing heavily in WASM component models and structured SOP engines. This positions them as the "developer platform" for agent workflows.
- **NanoBot is the reliability leader** in its segment, with all merged bug fixes today addressing real end-user pain points (stuck WebUI, relay crashes) rather than architectural debt.
- **IronClaw is the only project with explicit multi-tenant capability policies** and production-grade OAuth flows, signaling a focus on enterprise and regulated environments.
- **Hermes Agent has the lowest barrier to entry** for individual users (TUI, desktop app) but suffers the most from platform-specific bugs (Windows, macOS).

### 6. Community Momentum & Maturity

- **Tier 1 - High Velocity / Feature-Heavy:**
    - **ZeroClaw** (50 issues, 50 PRs, 10+ distinct authors) is clearly in an intense pre-release sprint (v0.8.3 and v0.9.0). Its structured RFC process (Issue #6808) indicates a maturing governance model.
    - **Hermes Agent** (50 issues, 50 PRs) matches ZeroClaw in raw volume but is more focused on bug-fixing and security hardening than new features.
    - **IronClaw** (43 PRs) is dominated by core contributors and is preparing for a significant version jump (0.24.0 → 0.29.1) with breaking changes and a major test framework.

- **Tier 2 - Stable Iteration:**
    - **NanoBot** (24 PRs) shows the highest per-PR *impact* on user experience, with all merged fixes directly addressing reported bugs. This project balances feature velocity with reliability best.
    - **OpenClaw** (500 each) is paradoxically both the most active and the most strained. The sheer volume of activity is a double-edged sword—while it enables breadth, it creates a perception of instability.

- **Tier 3 - Maintenance / Low Activity:**
    - **LobsterAI**, **Moltis**, **PicoClaw**, and **NullClaw** show minimal community engagement. LobsterAI is notable for a critical bug (#2216) with no response and a long-stalled feature PR (#1488), indicating potential maintainer bandwidth issues.
    - **TinyClaw** and **ZeptoClaw** are effectively inactive.

- **Risk Flags:**
    - **OpenClaw**'s backlog (P1 issues open for months, stalled community PRs) is a structural risk. If left unaddressed, it could erode contributor trust.
    - **IronClaw**'s 33-day-old nightly E2E failure (#4108) with no fix PR is a release-blocking risk for its planned version jump.
    - **LobsterAI**'s lack of response to a critical blocking bug (#2216) is a community-health red flag.

### 7. Trend Signals

1.  **The "Agentic OS" is the Endgame.** Projects are no longer just chat wrappers. ZeroClaw (WASM plugins, SOP engines), OpenClaw (cron, subagents, developer agents), and Hermes Agent (deterministic workflows) are all building toward a vision of the agent as an *operating system* for autonomous tasks, not a conversational interface.

2.  **Security Posture is Becoming a Differentiator.** The ecosystem is moving beyond "harden at the end." IronClaw’s capability policies (owner/admin/member), ZeroClaw’s per-agent env vars, and NanoClaw’s community-driven CWE-59 fixes all show security is being treated as a first-class architectural concern, particularly for multi-tenant deployments.

3.  **The "Async Agent" Pattern is Emerging.** The most requested features across projects—deterministic workflows (Hermes Agent), goal mode (ZeroClaw), cron and SOP triggers (OpenClaw)—point to a shift from synchronous, chat-based interaction to asynchronous, task-driven execution. Users want agents that *act*, not just *converse*.

4.  **Cross-Platform is a Constant Liability.** Windows and Linux remain second-class citizens. The recurring bugs (BOM, console flashing, package manager parity) represent a significant drag on ecosystem growth, especially as the "everything app" vision demands seamless operation across all user environments.

5.  **The "Keep it Tiny" Philosophy is Gaining Traction.** NanoBot's explicit minimalism stands in contrast to the monolithic platforms. Its high user satisfaction and rapid bug-fix turnaround suggest there is a large, underserved market for simple, reliable agents that just work, without the complexity of full-platform solutions.

**Value for AI Agent Developers:** The ecosystem is mature enough that developers should no longer build from scratch. Instead, they should evaluate their deployment topology—single-user vs. multi-tenant, synchronous vs. asynchronous—and select a platform accordingly. For reliability and simplicity, **NanoBot** is the best foundation. For multi-platform enterprise deployments, **IronClaw** or a carefully hardened **ZeroClaw** are better bets. **OpenClaw** remains the most feature-complete, but its stability issues require significant operational overhead. The trajectory of the entire space is toward deterministic, secure, and observable agent runtimes, with chat interfaces becoming just one input/output mode among many.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-29

## Today's Overview

NanoBot shows **very high development activity** with 24 pull requests updated in the last 24 hours and 7 issues touched, signaling a major push to close out June with numerous quality-of-life fixes and feature additions. The project merged or closed **10 PRs** today (including critical bug fixes), while 14 remain open for review. A total of 6 issues are actively open, with one bug closed. **No new releases** were tagged, but the sheer volume of merged changes suggests a release candidate may be close. The community is contributing heavily, with multiple contributors landing non-trivial patches across session handling, WebUI stability, provider integration, and memory/skill management.

## Releases
**None.** The latest tagged release remains v0.2.2. Given the 10 merged PRs today (including fixes for WebUI stuck-streaming, malformed relay responses, corrupt session files, and cron protection), a v0.2.3 or minor release is likely imminent.

## Project Progress

**10 PRs merged/closed today** — key advances:

- **#4565 — WebUI stuck-streaming fix (merged)** — Resolves a critical bug (#4500) where self-restart left the UI in a perpetual "processing" state and the stop button reported "No active task to stop." This fix clears in-memory turn state on reconnect.
- **#4566 — Corrupt legacy-session repair (merged)** — Fixed `list_sessions()` silently dropping corrupt session files with legacy non-base64 filename stems; repair path now correctly re-encodes fallback keys.
- **#4569 — Malformed relay tool-call hardening (merged)** — Agent loop now guards against null/empty tool names from upstream relays, preventing crashes and infinite replay loops.
- **#4564 — Cron API guard for unavailable store (merged)** — Added protection against cron operations when the persistent store is missing or unavailable.
- **#4542 — MCP image content delivery (merged)** — MCP tools returning `ImageContent` blocks now deliver base64 payloads as proper artifacts instead of embedding raw strings in tool results.
- **#4504 — Skills subdirectory support (merged)** — Optional directory grouping enabled under `~/.nanobot/workspace/skills/` for better skill organization.
- **#2120 — Contrib docs (merged)** — New `CONTRIBUTORS.md` and README updates for community documentation.

## Community Hot Topics

- **#4010 — Text-to-Speech / Voice Output** (open, 2 👍) — The top-voted feature request. With voice input already supported, users want the full conversational loop: agent speech output, especially on channels that natively support voice notes. Likely a major roadmap item.
  → https://github.com/HKUDS/nanobot/issues/4010

- **#4580 — Conda environment for subprocesses** (open, 1 comment) — User wants virtual environment support for `exec` subprocesses, citing real-world need for isolated Python environments.
  → https://github.com/HKUDS/nanobot/issues/4580

- **#4578 — Codex OAuth proxy handling** (open PR) —  A provider-level fix for explicit proxy configuration during Codex OAuth login, addressing enterprise/user environments behind corporate proxies.
  → https://github.com/HKUDS/nanobot/pull/4578

- **#4192 — Subagent MCP tool inheritance** (open PR, 2 comments) — Opt-in config to allow spawned subagents to inherit live MCP tools from the main agent. Addresses a common team-collaboration pattern.
  → https://github.com/HKUDS/nanobot/pull/4192

**Underlying need:** Users are pushing NanoBot toward **full conversational parity** (voice in/out), **better tool composition** (MCP inheritance, conda envs), and **production-grade networking** (proxy support). The community is also systematically hardening against relay/edge-case failures.

## Bugs & Stability

| Severity | Issue | Status | Fix PR |
|----------|-------|--------|--------|
| **Critical** | #4500 — WebUI stuck-streaming after self-restart, stop button broken | **Closed** | ✅ #4565 merged |
| **High** | #4569 — Malformed relay tool-call (null tool name) causes crashes/infinite loops | **Closed** | ✅ #4569 merged |
| **High** | #4222 — `max_messages` truncation continuously invalidates prefix/prompt caching | Open | #4568 open (fixes half) |
| **Medium** | #4566 — Corrupt legacy-session files silently dropped by `list_sessions()` | **Closed** | ✅ #4566 merged |
| **Medium** | #4567 — WeChat silent streaming config drop (pydantic ignored `streaming` field) | Open | #4567 open |
| **Low** | #4574 — `retain_recent_legal_suffix()` returns confusing bare tuple | Open | #4574 open (refactor) |

**Key observation:** The community is deeply focused on **WebSocket/streaming reliability** and **session data integrity**. Every merged bug fix today addresses a real end-user pain point.

## Feature Requests & Roadmap Signals

**Likely for next release (v0.2.3):**

- **TTS/voice output** (#4010) — Strong community demand, closes the voice loop.
- **Per-subagent model override** (#4231) — PR #4570 already submitted; allows different models for different subagent tasks.
- **Subagent MCP tool inheritance** (#4192) — PR in review, opt-in config.
- **Skills subdirectory grouping** (already merged in #4504).
- **Codex explicit proxy** (#4578) — PR in review.
- **Prefix caching fix** (#4222) — PR #4568 addresses the `max_messages` half.

**Lower probability this cycle:**
- **Group chat message buffering/debounce** (#3938) — Lower urgency, no PR yet.
- **Native A2A peer delegation** (PR #4571) — Ambitious refactor, likely needs more review.

## User Feedback Summary

- **Satisfaction:** The rapid turnaround on #4500 (stuck WebUI) and #4569 (relay crashes) signals maintainers listen to critical issues. Users appreciate the "keep it tiny" philosophy (#4579).
- **Pain Points:**
  - "WebUI session management is bare" — no timestamps in sidebar, no markdown export (#4579).
  - "Can't use conda environments for subprocesses" (#4580) — real developer workflow blocker.
  - "Subagents can't use different models" (#4231) — limits hierarchical task routing.
  - "Group chat flooding" (#3938) — each message triggers a separate agent call, disruptive to collaborators.
- **Use Cases Excelling:** Personal 1:1 chat, code execution via shell, skill-based workflows.
- **Room for Growth:** Multi-agent team collaboration (A2A delegation), enterprise proxy/network configuration, voice output.

## Backlog Watch

- **#3938 — Group chat message buffering/debounce** (open since May 20) — 0 maintainer comments. Growing pain for team deployments on Telegram/Feishu.
  → https://github.com/HKUDS/nanobot/issues/3938

- **#4222 — Prefix caching invalidation** (open since June 6) — Performance-critical for heavy users; only half-fixed by #4568 (the `microcompact` half remains).
  → https://github.com/HKUDS/nanobot/issues/4222

- **#4192 — Subagent MCP tool inheritance** (open PR since June 4) — Awaiting review/merge despite being a clear community need linked to #4166.
  → https://github.com/HKUDS/nanobot/pull/4192

- **#2120 — Contributors documentation** (merged today after 3 months open) — Highlights that documentation PRs can languish; maintainer bandwidth is focused on code.

---

**Project Health Assessment:** 🔵 **Very Active** — High throughput, responsive to critical bugs, strong community contribution. The project is maturing from a single-agent chat tool into a multi-agent, multi-channel platform with robust error handling. The main risks are documentation lag and feature request triage (some issues untouched for weeks).

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-29

## Today's Overview

Hermes Agent is experiencing **very high community activity** with 50 issues and 50 PRs updated in the last 24 hours — marking an exceptionally busy day for the project. The open issue count remains high at 46, suggesting the maintainer team is working through a substantial backlog. Notably, the Windows desktop app has become the primary source of new bug reports, with multiple users reporting console window flashing, IME input issues, and settings access problems. A coordinated batch of security and stability fixes was merged today, including path traversal vulnerability patches and gateway error sanitization, reflecting active triage from the core team. No new releases were published today.

## Releases

No new releases were published today. The latest available version remains v0.17.0 (referenced in issue #54049).

## Project Progress

**18 PRs were merged or closed today**, including several critical security and stability fixes:

- **Security**: Multiple PRs addressed path traversal vulnerabilities in profile aliases ([#54476](https://github.com/NousResearch/hermes-agent/pull/54476), [#3962](https://github.com/NousResearch/hermes-agent/pull/3962), [#6205](https://github.com/NousResearch/hermes-agent/pull/6205)) — all closing the same class of arbitrary-file-clobber footgun
- **Gateway hardening**: Error messages no longer leak raw exception details to users ([#54481](https://github.com/NousResearch/hermes-agent/pull/54481)); webhook GitHub args are now validated before shelling out
- **Agent loop**: Anthropic interrupt handling fixed to prevent hangs; oversized vision data-URLs are now rejected to prevent OOM ([#54484](https://github.com/NousResearch/hermes-agent/pull/54484))
- **Docker sandbox**: Container spawning now works on hosts without full cgroup v2 controller delegation ([#54478](https://github.com/NousResearch/hermes-agent/pull/54478))
- **Approval flow**: Unknown `approvals.mode` config values now fail safe instead of silently behaving like `manual` ([#54469](https://github.com/NousResearch/hermes-agent/pull/54469))
- **Deduplication**: Streaming tool call names no longer double from providers that resend complete names in every delta ([#6661](https://github.com/NousResearch/hermes-agent/pull/6661))

## Community Hot Topics

1. **[Windows Desktop GUI: console windows flash on subprocess spawns](https://github.com/NousResearch/hermes-agent/issues/54220)** (7 comments, tracking issue) — The most-reported active bug, affecting Windows users system-wide. Users report cmd/conhost windows blinking every 5-10 seconds, worsening when clicking "Messaging." The project is treating this as umbrella issue for action.

2. **[Deterministic Workflow Engine Feature Request](https://github.com/NousResearch/hermes-agent/issues/5354)** (8 comments, 8 👍) — Strong community desire for a Lobster-style deterministic workflow engine that avoids LLM re-planning for repetitive tasks. Signals demand for more predictable, lower-cost task execution.

3. **[NeuTTS Installation Failure](https://github.com/NousResearch/hermes-agent/issues/3002)** (12 comments, 4 👍) — Long-standing bug (since March) where clean installs fail to enable text-to-speech because the venv lacks pip. Community frustration is building as the issue ages.

4. **[Telegram typing indicator stuck indefinitely](https://github.com/NousResearch/hermes-agent/issues/28004)** (7 comments) — Race condition in `_keep_typing` cleanup causes permanent "typing..." indicator on Telegram users' screens. Has a root cause analysis but no fix PR yet.

## Bugs & Stability

**High Priority (P1/P2, active):**

- **Windows console flash** (P2, #54220) — Most impactful Windows bug. Associated duplicate #54506 reports worsening with Messaging button. **No fix PR yet** — tracking issue open.
- **Config priority: OpenRouter overrides explicit custom provider** (P2, #39753, CLOSED) — Fixed today, but major impact: user-configured `base_url` was silently overridden when model names matched OpenRouter catalog entries.
- **DeepSeek chunked streaming drops** (P2, #54049) — OpenResty reverse proxy disconnects when custom httpx transport has socket options. Workaround exists (default transport). **No fix PR yet.**
- **WhatsApp bridge critical CVE** (P2, #44983) — Unfixed vulnerability in `@whiskeysockets/baileys` (GHSA-qvv5-jq5g-4cgg) involving message spoofing. **No fix PR yet.**
- **Matrix multi-profile room isolation bypass** (P2, #54461) — Security boundary issue where profiles sharing one Matrix account can bypass allowed-room isolation. Filed yesterday, **no fix PR yet**.
- **CLI one-shot model config staleness** (P2, #54147) — `hermes chat -m <model>` uses stale `api_mode` from config default, causing 404s. **No fix PR yet.**

**Medium Priority (P3):**
- **Desktop/TUI regression** (#54473) — Desktop shipped with 30x the feature rate of TUI, leaving three concrete regressions from the same root cause.
- **Dashboard scrollback drift** (#53641) — New input/output invisible in long sessions, scales with transcript size.
- **Remote TTS audio broken** (#46135) — TTS files created on server but rendered as 0-second on Desktop.
- **Settings unreachable during startup error** (#54545) — macOS recovery screen blocks the only in-app path to Settings.

## Feature Requests & Roadmap Signals

**Strong community demand (P2, 8 👍):**
- **Deterministic Workflow Engine** (#5354) — User wants LLM-free task execution for repetitive operations. Likely candidate for next minor release given community enthusiasm.

**Active feature PRs in review:**
- **Local-first telemetry & observability** ([#51714](https://github.com/NousResearch/hermes-agent/pull/51714)) — Records agent workflows, model calls, errors locally. Default-on, nothing leaves machine unless exported.
- **Multi-gateway connections with per-gateway tabs** (#45779, 2 👍) — Request to manage multiple Hermes agents across machines from one Desktop UI.
- **Edge-based vertical packs for PM/analyst workflows** (#54463) — Reusable bundles of role guidance, templates, and tool expectations.
- **Honcho compartment routing** ([#54534](https://github.com/NousResearch/hermes-agent/pull/54534)) — Adds explicit workspace/key-file config compartment selection for Honcho tools.
- **Update-proof user locale overrides** ([#54557](https://github.com/NousResearch/hermes-agent/pull/54557)) — Prevents app updates from reverting user-edited translation catalogs.

**Long-standing feature (since March):**
- **Persistent User Workspace & Knowledge Base** (#531, 2 👍) — No persistent document storage; files auto-clean after 24 hours. Still not addressed.

## User Feedback Summary

**Pain Points:**
1. **Windows Desktop is the #1 frustration** — Console flashing, IME input broken, model picker incomplete, settings unreachable. Multiple users call this "the most-reported active bug."
2. **TTS installation blocks new users** — Issue #3002 has been open since March 25 with no resolution timeline.
3. **Config surprise** — Users report their explicit custom provider configurations being silently overridden by OpenRouter's catalog auto-picks.
4. **Email gateway breaks sessions** — New subject lines interrupt running tasks instead of creating isolated sessions (#27804).
5. **Desktop/TUI gap** — Users explicitly note that desktop features landed at 30x the rate of TUI features, creating a "gap to the existing reference experience."

**Satisfaction Signals:**
- Community members are actively contributing feature PRs (backend backup import, Honcho routing, i18n overrides).
- Security researchers are actively auditing and submitting vulnerability fixes — indicating trust in the project's responsiveness.
- The maintainer team (teknium1, aaronlab, OutThisLife) is actively triaging and merging fixes today.

## Backlog Watch

**Issues needing maintainer attention:**

1. **[#3002](https://github.com/NousResearch/hermes-agent/issues/3002) — NeuTTS install fails (12 comments, since March 25)** — 3+ months old, popular feature blocked for new users. No fix PR or maintainer reassignment visible.

2. **[#531](https://github.com/NousResearch/hermes-agent/issues/531) — Persistent Knowledge Base (4 comments, since March 6)** — Core architectural gap; no persistent user document storage exists. Featured but not addressed.

3. **[#28004](https://github.com/NousResearch/hermes-agent/issues/28004) — Telegram typing indicator stuck (7 comments, since May 18)** — Root cause analyzed; no fix PR despite being a visible UX bug for Telegram users.

4. **[#44983](https://github.com/NousResearch/hermes-agent/issues/44983) — WhatsApp CVE (critical, 2 comments, since June 12)** — Known unfixed critical vulnerability. Fix PR #44980 exists but this CVE remains unfixed after `npm audit fix`.

5. **[#39136](https://github.com/NousResearch/hermes-agent/issues/39136) — Stale dashboard processes accumulate (1 comment, since June 4)** — Old CLI processes from prior versions consume ports 9120-9126 and can't be cleaned by new CLI.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-29

## Today's Overview
PicoClaw shows low activity today with only 1 closed issue and 2 PRs updated in the last 24 hours—one closed and one open. No new releases are available. The project remains in a maintenance phase, with a stale issue being closed and two PRs receiving updates, indicating steady but unremarkable progress. Overall, the project appears stable with no major new developments reported today.

## Releases
None. No new releases were published in the last 24 hours.

## Project Progress
Today's merged/closed PR:
- **PR #2964 (Merged)** — *Feat/image input compression* — Adds configurable inbound image compression for PicoClaw's vision pipeline. Previously, inbound images were only constrained by `max_media_size`; this introduces multi-level compression policies before building the model payload, reducing bandwidth and processing overhead for vision-heavy channels.
  - GitHub: [sipeed/picoclaw PR #2964](https://github.com/sipeed/picoclaw/pull/2964)

## Community Hot Topics
- **Issue #2984 (Closed)** — *[Feature][Protocol] Add explicit turn completion signal for Pico WebSocket clients* — This stale issue was closed today after receiving 4 comments and 2 👍 reactions. The request centered on adding a deterministic end-of-turn signal for WebSocket clients, which currently rely on inference from event streams like `typing.stop` or `message.create`. The underlying need is for cleaner client-side state management, especially for UI indicators or conversational turn tracking.
  - GitHub: [sipeed/picoclaw Issue #2984](https://github.com/sipeed/picoclaw/issues/2984)

## Bugs & Stability
No bugs, crashes, or regressions were reported today. The closed stale issue (#2984) was a feature request, not a bug. Overall stability appears good.

## Feature Requests & Roadmap Signals
- **Turn completion signal** (Issue #2984, closed) — Though this issue was closed as stale, it signals a real developer desire for explicit turn-level protocol signals. This may reappear in a future protocol revision or as a plugin.
- **Simplex channel type** (PR #3193, open) — A new channel type is being added, likely for one-way communication flows. This could be useful for notification or broadcast use cases in upcoming versions.
- **Image compression** (PR #2964, merged today) — This feature is now part of the codebase, improving vision pipeline efficiency.

**Prediction**: The simplex channel type (PR #3193) is likely to be merged soon, and protocol-level turn completion signaling may resurface as a community-driven enhancement in a future minor release.

## User Feedback Summary
- **Pain point** (Issue #2984): WebSocket clients experience ambiguity in determining when an agent has fully finished processing a user message. Developers want an explicit signal rather than inferring from event sequences.
- **Use case**: External clients consuming PicoClaw's WebSocket protocol require deterministic state management for UI and conversation flow.
- **Satisfaction**: The closure of Issue #2984 (as stale) may indicate the team chose not to act at this time, which could leave some developers dissatisfied. No other direct user sentiment is available from today's data.

## Backlog Watch
No backlog items requiring maintainer attention were identified today. The only stale item (Issue #2984) was closed. PR #3193 (simplex channel type) is open since 2026-06-27 and appears to be progressing normally. No long-unanswered issues or PRs were noted.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-29

## Today's Overview
NanoClaw shows a moderately active development day with 6 pull requests updated in the last 24 hours, though only one was closed/merged. A single open issue was filed, and no new releases were published. The project's focus today has been on security hardening and integration fixes, with three PRs addressing a symlink-based host file write vulnerability (CWE-59) across different attack vectors. The open issue reports a critical runtime failure when agents are configured with OpenAI as their provider, blocking a key user-facing feature. Overall, the project is in a maintenance-and-patch cycle, with community contributions continuing to flow in for channel integrations and security.

## Releases
*No new releases were published today. The latest available version remains NanoClaw 2.1.1.*

## Project Progress
One pull request was closed/merged today:
- **#2879** — **fix(agent-to-agent): containment-check target inbox in forwardAttachedFiles**  
  *Merged by johnmathews*  
  This fix addresses the same symlink containment vulnerability (CWE-59) as #2880 but on the agent-to-agent attachment forwarding path. It adds `lstat` rejection of pre-existing symlinks, `mkdir` before write, `realpath` resolution, `isPathInside` containment checks, and exclusive write flags. This mirrors the defensive pattern already used in `session-manager.ts` for saving attachments.  

  **Link:** https://github.com/nanocoai/nanoclaw/pull/2879

## Community Hot Topics
No issues or PRs received any comments or reactions (👍) in the last 24 hours, indicating low community engagement on existing threads today. The most notable PRs remain:
- **#2881** — Discord `custom_id` delimiter fix (jeevesforjoel) — addresses a parsing bug where button actions failed when values contained newlines.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2881
- **#2877** — Telegram native rich rendering via Bot API 10.1 (robbyczgw-cla) — a feature addition for richer message rendering.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2877

*Underlying need:* The community is actively contributing integration fixes (Discord, Telegram) and security hardening. The lack of comments may indicate that reviewers/maintainers haven't yet engaged with the newer PRs.

## Bugs & Stability
**High severity:**
- **#2876 [OPEN]** — **OpenAI provider crashes agent container on spawn**  
  *Reported by MJDemarcus, no comments*  
  Critical: The CLI accepts `--provider openai --model gpt-4o` configuration, persists it in the central DB, but when the agent receives a message and spawns a container, it crashes. This blocks users from running agents with OpenAI, a core use case. No fix PR exists yet.  
  **Link:** https://github.com/nanocoai/nanoclaw/issues/2876

**Medium severity:**
- **#2878 [OPEN]** — **Codex reconnect fails on stale OpenAI secrets**  
  *Reported by glifocat, fix PR exists*  
  `runCodexAuthStep()` returns success for any matching OneCLI secret even when the credential is stale/revoked, causing mid-conversation authentication failures. A fix PR (#2878) is open.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2878
- **#2881 [OPEN]** — **Discord button actions misparsed due to newline delimiter in custom_id**  
  *Reported by jeevesforjoel, fix PR exists*  
  `handleForwardedEvent` parses the raw encoded string containing `\n` delimiter, causing `tail` to contain `'0\n0'` instead of `'0'`, breaking `resolveSelectedOption`. Fix PR #2881 is open.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2881

**Low severity:**
- **#2880 [OPEN]** — **Symlink escape vulnerability in inbox attachment writes**  
  *Reported by johnmathews, fix PR exists*  
  A host file write vector where a compromised agent pre-places symlinks in its session directory. Fix PR #2880 is open.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2880

## Feature Requests & Roadmap Signals
- **#2877 [OPEN]** — **feat(telegram): native rich rendering via Bot API 10.1 sendRichMessage**  
  *Reported by robbyczgw-cla*  
  A new feature skill enabling Telegram's native rich message rendering (tables, lists, code blocks, etc.) using the latest Bot API. This is a clear user-facing capability improvement likely to be reviewed and merged in a future release (possibly 2.2.0).  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2877

- **#2875 [OPEN]** — **Deploy/coolify**  
  *Reported by zczDief*  
  An operational/container skill contribution following the project's contribution guidelines. Likely adds deployment support for Coolify, a self-hosted PaaS. No specific details in the summary.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2875

## User Feedback Summary
- **Pain point (critical):** Users on NanoClaw 2.1.1 cannot configure agents to use OpenAI's provider — the CLI accepts the configuration but the container crashes on spawn, making OpenAI effectively unusable. (Issue #2876)
- **Pain point (moderate):** Codex authentication silently accepts stale OpenAI credentials, causing agents to fail mid-conversation with unrecoverable "Your access token could not be refreshed" errors. (PR #2878)
- **Use case (integration):** Two channel integration PRs (Discord button parsing fix, Telegram rich messages) indicate active use of NanoClaw's multi-channel capabilities and a desire for richer user experiences.
- **Security concern (community-driven):** Three PRs (#2878, #2879, #2880) all addressing the same core vulnerability (CWE-59 symlink escape) suggest the security issue was discovered independently by the community, with maintainer johnmathews leading the fix.

## Backlog Watch
- **#2876 [OPEN]** — **OpenAI provider crash** (created 2026-06-28)  
  This is the most critical open issue and has received zero comments. It needs immediate maintainer attention to either reproduce, triage, or assign to a contributor.  
  **Link:** https://github.com/nanocoai/nanoclaw/issues/2876

- **#2875 [OPEN]** — **Deploy/coolify** (created 2026-06-27, updated 2026-06-28)  
  A contribution that follows the contribution guidelines but has not received any maintainer review or labeling. Could become stale if unaddressed.  
  **Link:** https://github.com/nanocoai/nanoclaw/pull/2875

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the project digest for **NullClaw** for **2026-06-29**.

---

## NullClaw Project Digest – 2026-06-29

### 1. Today's Overview
The NullClaw project is currently in a **low-activity maintenance state**. Over the past 24 hours, only one issue was updated, and it was closed—indicating a resolution of a long-standing community question. There were zero new pull requests, zero merged changes, and zero releases. While the project is not stalled, the lack of commits or PRs suggests the core development cycle is paused or focused on planning for the next milestone. The closing of the last active historical issue brings the open issue tracker to zero.

### 2. Releases
**No new releases** were published today. The project remains without a formal release tag on this date.

### 3. Project Progress
- **Merged/Closed PRs:** 0
- **Features Advanced:** None. No PRs were updated, opened, or merged today. No new code was integrated into the main branch.

### 4. Community Hot Topics
Only one issue was active in the last 24 hours:

- **[#50 – Can this run on an Esp32?](https://github.com/nullclaw/nullclaw/issues/50)** (CLOSED)
    - *Author:* ngantrandev | *Created:* 2026-02-21 | *Updated:* 2026-06-28 | *Comments:* 4
    - *Analysis:* This was the **most (and only) active discussion** today. The issue was **closed** as of yesterday (June 28th). With 4 comments, the community discussed the feasibility of running NullClaw on an ESP32 microcontroller, likely involving memory constraints (RAM/Flash) and architectural compatibility. The closure suggests the maintainer either provided a definitive answer (e.g., "not feasible without major porting") or the project is officially not targeting embedded MCUs.

### 5. Bugs & Stability
- **New bugs reported today:** 0
- **Critical regressions:** None detected.
- **Stability assessment:** With zero open bugs and no crash reports today, the project is currently considered **stable** but also **inactive** in terms of fixes.

### 6. Feature Requests & Roadmap Signals
- **User-requested features today:** None specific were opened today.
- **Signal from closed Issue #50:** The query regarding ESP32 support indicates a **latent demand for edge/embedded device compatibility**. If the maintainer closed this issue without implementing the feature, it is unlikely for the next version. However, if the closure was a "deferred" or "tracked" label, a future roadmap item might involve a lightweight runtime for IoT devices. **Prediction:** The next version (if any) will likely focus on core debugging or documentation, not ESP32 support.

### 7. User Feedback Summary
- **Pain Points:** The primary user question raised (Issue #50) revolves around **hardware constraints** – specifically, whether the software stack is lightweight enough to run on 240MHz dual-core MCUs with limited RAM (512KB+). This suggests users find the current project valuable but desire lower-level deployment options.
- **Satisfaction/Dissatisfaction:** The single issue was closed, implying the user received a satisfactory answer or the question was resolved. No complaints or negative feedback was visible in the 24-hour window. The project's current state of zero open bugs and zero open PRs signals either high satisfaction or low engagement.

### 8. Backlog Watch
- **Long-unanswered Issues:** **None.** The last remaining issue (#50) has been closed. The open issue backlog is effectively **empty**.
- **Maintainer Attention Needed:** With zero open issues and zero open PRs, there are no items requiring immediate maintainer attention. The project is in a "clean" state.

**Project Health Rating:** 🟢 **Quiet / Maintenance Mode** (Low activity, no technical debt backlog).

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-29

## Today's Overview

IronClaw shows **very high activity** this period, with 43 PRs updated in the last 24 hours and 18 merged/closed. The project is in a major feature delivery phase, particularly around the **Reborn** integration-test framework (slices 3–9), Slack pairing flows, capability policy implementation, and WebUI v2 QA infrastructure. Three issues were updated, including a new feature request for fine-grained capability policy configuration and a long-standing nightly E2E test failure that continues unresolved. No new releases were published today, though a release preparation PR (#5311) is open with breaking API changes across `ironclaw_common` and `ironclaw_skills` crates. Overall project health is strong, with core contributors dominating the commit log and a clear focus on hardening production-grade integrations.

## Releases

**No new releases today.** The last release remains 0.24.0. A release preparation PR (#5311) is open, proposing `ironclaw` bump from 0.24.0 to 0.29.1 with breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), alongside minor bumps for `ironclaw_safety` and `ironclaw_skill_learning`.

## Project Progress

**18 PRs merged/closed today.** Key advances:

- **Capability Policy (Issue #5385 → PR #5394):** Core contributor `zetyquickly` addressed the newly opened capability policy issue with an XL-sized PR implementing owner/admin/member user types with fine-grained configuration.
- **Reborn Integration-Test Framework:** Three slices closed:
  - **Slice 4 (PR #5387):** URL-keyed HTTP matcher + egress assertion API merged.
  - **Slice 9 (PR #5386):** Descoped embeddings fake after determining the seam is unreachable — pragmatic "STOP" verdict.
  - **Slices 3–9 bulk (PR #5392):** Large combined PR now open covering LibSql matrix, egress/HTTP matcher, inert process port, MCP/OAuth/refresh.
- **Slack Integration:**
  - **/pair command (PR #5377, merged):** New Slack slash command force-mints pairing codes ephemerally, never DM'd or logged. Invalid-code redeem errors now point users to `/pair`.
  - **Google OAuth fix (PR #5388, merged):** Fixed Reborn WebUI Google SSO `id_token` decoding for real RS256 tokens after `jsonwebtoken` 10.x bump. Canonicalized OAuth redirect URLs for Railway preview domains.
- **Web Access / Exa content fetch (PR #5395):** Updated `get_content` to fetch through Exa directly, with tightened input/output schemas.
- **Dependency updates:** Multiple dependabot PRs merged across wasm, serialization, and other groups.
- **Benchmark validation (PR #5393, merged):** Throwaway PR validated `/benchmark` builds against current main after upstream toml_parser lock bump.

Still open and active: context management with progressive tool disclosure (PR #5149, flag-gated), Slack host conversation binding persistence (PR #5252), ask-each-time approval resume loop fix (PR #5306), surface real failure details in Reborn (PR #5338), and WebUI v2 live QA canary (PR #5354).

## Community Hot Topics

| Issue/PR | Type | Comments | Activity |
|----------|------|----------|----------|
| **#5385 — Add Capability Policy** | Issue (Open) | 0 comments | Created 2026-06-27, last updated 2026-06-28 |
| **#5392 — Integration-test framework slices 3–9** | PR (Open) | 0 comments | Created 2026-06-28, last updated 2026-06-29 |
| **#5377 — /pair Slack slash command** | PR (Merged) | 0 comments | Created 2026-06-27, merged 2026-06-29 |
| **#4108 — Nightly E2E failed** | Issue (Open) | 0 comments | Created 2026-05-27, last updated 2026-06-28 |

*Note: Comment counts appear as `undefined` in data, suggesting they were not tracked or zero.*

**Analysis:** The project is primarily core-contributor driven with little community discussion. The most significant topic is the **Capability Policy** feature (#5385 → #5394), which addresses a need for multi-tenant and fine-grained access control. This is a user-facing governance feature that signals growing enterprise use cases. The **Nightly E2E failure (#4108)** has been open for over a month with no resolution, which is a growing concern for stability.

## Bugs & Stability

| Severity | Issue | Status | Fix PR | Notes |
|----------|-------|--------|--------|-------|
| **Critical** | Nightly E2E failure (#4108) | Open, 33 days old | None | Scheduled full E2E test suite failing nightly. Reported at commit `6a3b10fa58`. No fix PR exists. |
| **Medium** | Vague "driver protocol error" in Reborn (#5338 → PR) | Fix PR open | #5338 | Tool errors showed generic "invalid_input" instead of real failure detail. PR surfaces end-to-end failure details. |
| **Medium** | Google OAuth RS256 token decode failure (#5388) | **Fixed** | #5388 | Merged today. RS256 tokens broke after jsonwebtoken 10.x bump. |
| **Low** | Slack pairing code expiry handling (#5362, #5377) | PRs open/merged | #5362, #5377 | Multiple PRs hardening stale/expired code paths and ephemeral code generation. |

**Key finding:** The nightly E2E failure (#4108) remains the most concerning stability issue — open for over a month without a fix PR. This is a red flag for release readiness, especially given the planned 0.24.0 → 0.29.1 jump.

## Feature Requests & Roadmap Signals

| Feature | Source | Status | Prediction |
|---------|--------|--------|------------|
| **Capability Policy (user types)** | #5385 | PR #5394 open | **Likely next release** — core feature with active PR |
| **Context management / progressive tool disclosure** | #5149 | Open, flag-gated | **Next release candidate** — addresses token/timeout issues |
| **Slack /pair command** | #5377 | **Merged** | Already shipped in working branch |
| **Reborn integration-test framework** | #5387, #5392 | Slices merging | Foundational for release quality |
| **WebUI v2 live QA canary** | #5354 | Open | Infrastructure for release stability |

**Prediction:** The next release (0.29.1 per #5311) will likely include capability policy, context management, Slack pairing hardening, and the Reborn integration-test framework. The E2E nightly failure must be resolved before release.

## User Feedback Summary

User-facing improvements visible in today's data:

- **Pain point: Vague error messages** — PR #5338 directly addresses users seeing generic "invalid_input" instead of real failure diagnostics after tool errors. This was a real usability issue.
- **Pain point: Slack pairing friction** — Multiple PRs (#5377, #5362, #5252) address issues with stale/expired pairing codes, lost conversation bindings, and unclear error recovery paths. The new `/pair` command is a direct response to user confusion.
- **Pain point: Google OAuth login failures** — PR #5388 fixed broken SSO on Railway preview domains, which would have blocked users on custom domains.
- **Pain point: Slow model calls / timeouts** — PR #5149 (context management) reduces per-call token count from ~25.8k to address NEAR AI 120s timeouts. This was causing retry exhaustion and silent failures.

No explicit user satisfaction signals (reactions, thanks, or praise) appear in the data, though the rapid fix turnaround on reported issues suggests responsiveness.

## Backlog Watch

| Item | Type | Age | Priority | Concern |
|------|------|-----|----------|---------|
| **#4108 — Nightly E2E failure** | Issue | 33 days | **Critical** | No assignee, no fix PR. Scheduled run failing nightly. Blocking release confidence. |
| **#4002 — actions group dependency bump** | PR | 36 days | Medium | 16 updates stalled on CI. If merged out of order, could break build. |
| **#4032 — wasm group dependency bump** | PR | 35 days | Medium | Outdated wasm dependencies (wit-component 0.245.1 → 0.252.0). Potential security surface. |
| **#5114 — tokio-ecosystem group bump** | PR | 8 days | Medium | Tokio ecosystem updates pending. |
| **#4498 — serde_yml bump** | PR | 24 days | Low | Minor serialization update. |

**Most critical:** The **Nightly E2E failure (#4108)** is the single biggest backlog risk. It has no assignee, no linked fix PR, and has been failing for over a month. Combined with the planned major version release, this represents a significant quality gate that must be addressed.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured digest for **LobsterAI** for **2026-06-29**, based on the provided GitHub data.

---

# LobsterAI Project Digest – 2026-06-29

## 1. Today's Overview
The project shows **low activity** over the last 24 hours, with no new releases and zero fresh issues or PRs. All 5 updated Issues and all 5 updated PRs are stale items from April that were batch-closed or updated yesterday (2026-06-28). The only truly new item is a single open Issue (#2216) filed on 2026-06-28, which indicates a serious blocking bug. The maintenance pace appears minimal, suggesting the team may be in a stabilization or planning phase.

## 2. Releases
**None.**  
No new releases were published in the last 24 hours or within the visible dataset.

## 3. Project Progress (Merged/Closed PRs)
Three PRs were closed (all stale, merged earlier):
- **[PR #1440](https://github.com/netease-youdao/LobsterAI/pull/1440)** – **feat(cowork):** Moved active skill badges from the bottom toolbar to above the textarea, improving UI clarity when many skills are selected.
- **[PR #1441](https://github.com/netease-youdao/LobsterAI/pull/1441)** – **feat(artifacts):** Added an extensible preview pipeline for HTML, React, and Mermaid artifacts. This was a conflict-resolved re-merge of a prior PR.
- **[PR #1445](https://github.com/netease-youdao/LobsterAI/pull/1445)** – **fix(skills):** Added validation to prevent duplicate skill imports and fixed zip import producing random directory names.

**Two PRs remain open (stale, updated yesterday):**
- **[PR #1488](https://github.com/netease-youdao/LobsterAI/pull/1488)** – **feat(scheduledTask):** UI overhaul of the scheduled task module to card-grid layout, plus search and history filters.
- **[PR #1494](https://github.com/netease-youdao/LobsterAI/pull/1494)** – **fix(cowork):** Skill selection state moved to per-session management, preventing cross-session interference.

## 4. Community Hot Topics
The most active issue is the **newly filed #2216** (1 comment, high urgency). Other stale issues have only 2–3 comments each.

| Issue / PR | Comments | Key Topic |
|---|---|---|
| [#2216](https://github.com/netease-youdao/LobsterAI/issues/2216) | 1 | Memory Search provider locked to OpenAI; DB lock blocks rebuild |
| [#1443](https://github.com/netease-youdao/LobsterAI/issues/1443) | 3 | Request for openclaw v2026.3.24 compatibility |
| [#1437](https://github.com/netease-youdao/LobsterAI/issues/1437) | 2 | UI bug: scheduled task creation button unresponsive |

**Underlying need:** Users are hitting hard walls with OpenAI dependency and version lock-in (openclaw breaking changes). The community would benefit from more flexible provider selection and clearer version upgrade guidance.

## 5. Bugs & Stability
Only **one new bug** reported today (filed 2026-06-28):

- **[CRITICAL] Issue #2216: Memory Search cannot switch to local embedding provider; index rebuild blocked by DB lock (EBUSY)**  
  *Environment:* Windows 11, Node v24.11.1, LobsterAI v2026.6.1.  
  *Impact:* When OpenAI API quota runs out, Memory Search is completely unusable. User cannot switch to a local provider in the UI, and the index rebuild fails due to a database lock.  
  *Status:* Open, no fix PR linked. **Highest priority bug** in the last 24h.

**Other stale bugs (closed, but relevant):**
- [#1437](https://github.com/netease-youdao/LobsterAI/issues/1437) (scheduled task creation button dead) – closed as stale, likely fixed.
- [#1439](https://github.com/netease-youdao/LobsterAI/issues/1439) (disabled skill still callable in chat) – closed as stale.
- [#1442](https://github.com/netease-youdao/LobsterAI/issues/1442) (agent skill display inconsistent after conversation) – closed as stale.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. Based on the stale PRs and issues:

- **Openclaw v2026.3.24 support** (Issue #1443) – a significant upgrade request that is likely being worked on or blocked.
- **Memory Search provider flexibility** (Issue #2216) – user explicitly requests the ability to select local/local embedding providers, which is a roadmap-relevant feature.
- **PR #1488 (scheduled task UI overhaul)** – this is a large, unmerged feature that may land in the next minor release (v2026.7.x).
- **PR #1494 (per-session skill state)** – a UX fix that aligns with ongoing cowork improvements.

**Prediction:** Version v2026.7.0 will likely include the scheduled task grid UI, per-session skill state, and possibly openclaw compatibility fixes.

## 7. User Feedback Summary
- **Pain point (high):** OpenAI API dependency is locking users out of core Memory Search functionality when quota is exhausted. Users want local alternatives (Issue #2216).
- **Pain point (medium):** Skill import and management still had duplication and naming bugs, although these were fixed in #1445.
- **Usability confusion:** The role of agent skill selection in conversations is unclear – skills disappear after first interaction (Issue #1442). This suggests documentation or UX clarity is needed.
- **Version anxiety:** Upgrading openclaw is breaking, and users are waiting for official compatibility (Issue #1443).

Overall sentiment: **Mixed** – the project is stable for most users, but power users hitting edge cases (API quotas, DB locks, openclaw breaking changes) are experiencing blocked workflows.

## 8. Backlog Watch
| Item | Age (approx.) | Notes |
|---|---|---|
| [#1443](https://github.com/netease-youdao/LobsterAI/issues/1443) (openclaw support) | 87 days | Closed as stale, but no public resolution. A high-value upgrade. |
| [#1488](https://github.com/netease-youdao/LobsterAI/pull/1488) (scheduled task UI) | 85 days | Open, no activity since June 28 (stale update). Needs maintainer review. |
| [#1494](https://github.com/netease-youdao/LobsterAI/pull/1494) (per-session skills) | 84 days | Open, stale. Small UX fix with high user impact. |
| [#2216](https://github.com/netease-youdao/LobsterAI/issues/2216) (Memory Search lock) | 1 day | Critical bug, needs immediate maintainer attention. |

**Recommendation:** The maintainers should prioritize **Issue #2216** (blocking bug) and merge **PR #1494** (small, clear fix) to reduce technical debt and improve user trust.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-29

## Today's Overview
Moltis shows a **low-activity day** with just 1 open bug issue updated and 2 open pull requests (none merged). No new releases have been published. The project is in a **maintenance-and-bugfix phase**, with both PRs targeting critical stability concerns — one fixing a build dependency leak and another preventing context-budget overflows caused by oversized images. Community engagement is minimal, with only 1 comment across all open items.

## Releases
**None.** No new versions have been published today or in the recent past.

## Project Progress
**No PRs were merged or closed today.** However, two open PRs signal ongoing improvements:
- **PR #1139** (fix-gateway): Corrects the `metrics` feature to avoid force-enabling the `matrix-sdk` dependency when Matrix is disabled — a **build hygiene fix** that prevents unnecessary compilation bloat.
- **PR #1138** (fix-agents): Automatically downscales oversized images (e.g., 4032×3024 photos) before they enter the model context, preventing prompt rejection caused by token budgets being exceeded.

## Community Hot Topics
The **only active issue** is driving attention this cycle:
- **Issue #1137** [bug – Apple Container ID exceeds name limit](https://github.com/moltis-org/moltis/issues/1137) — Reported 2 days ago, 1 comment. The user hit a platform-specific naming constraint on Apple devices when using container IDs. This suggests **Apple sandboxing or containerization limits** are surfacing in real-world deployments, likely affecting users running Moltis in macOS/iOS environments.

The two open PRs (#1138, #1139) have 0 comments each — no community discussion has occurred.

## Bugs & Stability
**One active bug, medium severity:**
- **Issue #1137** – Apple Container ID exceeds name limit. This is a **platform-specific crash** under macOS/iOS container environments. No associated fix PR exists yet. Risk: users on Apple platforms may be blocked. Fix urgency: moderate, as it affects a specific deployment context.

Both open PRs (#1138, #1139) address **pre-existing stability issues** (token overflow, build bloat) but are not directly linked to today's bug report.

## Feature Requests & Roadmap Signals
No new feature requests were filed today. The current activity is purely **defensive** — fixing regressions and build problems. Predictions for the next minor release:
1. **Automatic image downscaling** (PR #1138) will likely land, as it unblocks users whose prompts are rejected due to high-resolution image tokens.
2. **Cleaner feature-gating** (PR #1139) will likely land as a quality-of-life improvement for developers building custom images with optional Matrix support.

No major roadmap expansions are visible from today's data.

## User Feedback Summary
The single bug report reveals a **real pain point**:
- **Apple platform compatibility** – a user hit a hard crash when a container ID exceeded the system's name length limit. This indicates that Moltis may not be fully validated on recent Apple deployment environments (macOS container extensions, iOS app sandboxing). No positive or negative sentiment can be extracted from a single silent issue.

## Backlog Watch
**No long-unanswered items** currently flagged. The oldest open item (Issue #1137) is only 2 days old. Both open PRs (#1138, #1139) were submitted yesterday and have no maintainer response yet — this is within normal turnaround but bears watching if no merge activity occurs in the next 48 hours. The project maintainer should:
- **Review/merge PR #1138** (image downscaling) — directly fixes the most disruptive user-facing bug (token overflow).
- **Review/merge PR #1139** (metrics feature gate) — low-risk build fix.
- **Investigate Issue #1137** (Apple container ID) — platform-specific bug may require upstream Apple API documentation changes.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-29

## 1. Today's Overview
CoPaw shows balanced development activity with 6 issues and 8 PRs updated in the last 24 hours. One issue was closed, while 10 open items remain in active development. The team is advancing testing infrastructure for the Agentscope 2.0 migration, with three PRs delivering 120 unit tests across the crons, chats, and app-infra modules. Community engagement is moderately high, with new feature requests for DingTalk mentions and memory search improvements. No new releases were published today.

## 2. Releases
No new releases today. The latest available version is v1.1.12.post2 (referenced in recent issues).

## 3. Project Progress
No PRs were merged or closed today. The following PRs remain open and under development:

- **#5586** — `fix(context): prioritize runtime model over static config for compaction threshold` — First-time contributor submission, under review.
- **#5581** — `test(unit): app-infra backend unit tests — W3 sprint (31 cases, Agentscope 2.0)` — Completes three-week test infrastructure push.
- **#5422** — `test(unit): chats module unit tests — W2 sprint (38 cases, Agentscope 2.0)` — Chat-layer tests re-adapted to Agentscope 2.0.2.
- **#5423** — `test(unit): crons module unit tests — W1 sprint (51 cases, Agentscope 2.0)` — Cron backend tests re-adapted.
- **#5568** — `fix(plugins): fix official plugin installation failures on QwenPaw 2.0` — Critical plugin compatibility fix under review.
- **#5515** — `[Under Review] enable latest chat beta UI capabilities` — Pins chat UI to beta version for new features.
- **#5590** — `feat(channels): support dingtalk mentions in proactive sends` — New feature PR created today.
- **#5321** — `feat(context): scroll context manager — durable history + recall REPL` — Novel context management strategy.

## 4. Community Hot Topics
- **#5204** (3 comments) — *[CLOSED] Infinite loop when two QwenPaw Agents chat via Matrix* — This was the most discussed issue. The root cause (cross-agent reciprocal wake chain) was identified as distinct from single-agent ReAct loops. Closed between data collection and digest generation.
- **#5564** (2 comments) — *Support DingTalk @mention in channels send CLI and API* — Generated an immediate implementation PR (#5590) from contributor `wananing`, showing fast community-driven development.
- **#5591** (1 comment, created today) — *Excessive log output flooding terminal with inbox/events polling* — Fresh report from UOS user with 40,000+ identical log lines in one evening.

## 5. Bugs & Stability
**High Severity:**
- **#5587** — `[Bug] Qwen-Image Tool install error` — Reported on v1.1.12.post2, affects image generation tool installation. No fix PR yet.
- **#5591** — `Too many same log info` — Log spam issue (40,000+ lines in a night) on UOS, indicates polling behavior may need rate-limiting or debug-level filtering.

**Medium Severity:**
- **#5586** — Compaction threshold ignores conversation-level model override — Fix PR submitted by first-time contributor, under review.

**Low Severity:**
- **#5568** — Official plugin installation failures on QwenPaw 2.0 — Fix PR under review, affects 5 plugins (3 tools + CloudPaw bundle).

## 6. Feature Requests & Roadmap Signals
- **#5588** — *Memory search with dedicated Reranker model* — Proposes two-stage retrieval for memory search (embedding → reranker). If implemented, would replace single-stage Chroma similarity with embedding + dedicated reranker or LLM-based rerank. Moderate complexity, could appear in next minor release.
- **#5589** — *Input box multi-skill selection* — UX enhancement request to allow continuous `/`-triggered skill selection without re-typing the slash character. Low complexity, likely targeted for next patch.
- **#5564** (already PR'd as #5590) — *DingTalk @mention support* — PR created same day as feature request, likely landing in next release.

## 7. User Feedback Summary
- **Pain Points:** The most reported pain point is **logging verbosity** (#5591) on Linux (UOS), with console polling logs drowning out useful output. Users also report **plugin installation failures on v2.0** (#5568) and **tool installation errors** (#5587).
- **Use Cases:** Multi-agent collaboration via Matrix remains a key use case, as shown by the infinite loop issue (#5204) — users are deploying multiple agents to chat with each other in group contexts.
- **Satisfaction:** No direct satisfaction signals. The rapid response to feature requests (DingTalk mention → same-day PR) suggests the community appreciates responsiveness. The first-time contributor PRs (#5586, #5321) indicate a healthy on-ramp for new developers.

## 8. Backlog Watch
- **#5321** — `feat(context): scroll context manager` — Created June 19, under review. This is a significant new feature (SQLite-based context management instead of compression), but has been in review for 10 days without merge. May need maintainer attention to push to completion.
- **#5515** — `enable latest chat beta UI capabilities` — Under review since June 25, has no merged status. Beta UI features may be blocked on upstream chat library changes.
- **#5581, #5422, #5423** — Three test PRs awaiting merge, representing 120 unit tests for Agentscope 2.0. These are blocking broader v2.0 stability validation — prioritization could unblock the next release.

*All links: github.com/agentscope-ai/CoPaw*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — June 29, 2026

## 1. Today's Overview

ZeroClaw is in an **intense development sprint** (v0.8.3 and v0.9.0 trackers active, 50 issues and 50 PRs updated in the last 24 hours). Activity is exceptionally high, with 39 open/active issues and 46 open PRs indicating a heavy feature-development and bug-fixing cycle. The project has 11 closed issues and 4 merged/closed PRs today. **No new releases** were published, but infrastructure for the next release (release pipeline hardening with cosign signing, SLSA provenance, SBOM) advanced significantly. The project shows healthy contributor diversity with 10+ distinct authors active in the last day.

## 2. Releases

No new releases today. The project appears to be between releases (latest stable is v0.8.x series), with v0.8.3 and v0.9.0 content being actively developed and tracked in issues #8071, #7314, #7852, #8073, and #7432.

## 3. Project Progress

**Merged/Closed PRs today (4 total):**

- **[#8436](https://github.com/zeroclaw-labs/zeroclaw/pull/8436)** — `docs(runtime): document max_history_messages hard cap alongside whole-turn trim` (merged). Fixes documentation inconsistency where the history-management docs claimed only one history-bounding mechanism existed when two were actually in use.
- **[#8326](https://github.com/zeroclaw-labs/zeroclaw/pull/8326)** — `fix(acp-bridge): strip UTF-8 BOM from config.toml before TOML parsing` (closed/merged). Fixes an issue where Notepad on Windows produced unparseable config files due to UTF-8 BOM.
- **[#8350](https://github.com/zeroclaw-labs/zeroclaw/pull/8350)** — `perf(web-search): cache strip_tags regex in a LazyLock static` (closed/merged). Performance fix: regex was being recompiled on every invocation.
- **[#8432](https://github.com/zeroclaw-labs/zeroclaw/pull/8432)** — `bug(ci): package publish tokens fail late when push access is missing` (closed). Prevents late-stage CI failures for Homebrew/Scoop publishing.

**Features that advanced (open PRs with significant work):**

- **[#8420](https://github.com/zeroclaw-labs/zeroclaw/pull/8420)** — SOP step schema enforcement at engine boundary (XL-sized)
- **[#8428](https://github.com/zeroclaw-labs/zeroclaw/pull/8428)** — Plugin registry suggestion system for missing capabilities
- **[#8419](https://github.com/zeroclaw-labs/zeroclaw/pull/8419)** — Calendar no-show SOP triggers (L-sized)
- **[#8393](https://github.com/zeroclaw-labs/zeroclaw/pull/8393)** — Goal mode runtime implementation
- **[#8368](https://github.com/zeroclaw-labs/zeroclaw/pull/8368)** — WASMtime component-model host (XL-sized, supersedes earlier work)

## 4. Community Hot Topics

**Most active discussions (by comment count):**

1. **[RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** (12 comments) — A governance RFC being rolled out (Rev. 5, status: accepted). This is the project's process-improvement backbone, showing the maintainers are actively refining how work gets triaged and routed.

2. **[Bug: Code help/keybindings misleading on macOS](https://github.com/zeroclaw-labs/zeroclaw/issues/7800)** (4 comments, updated today) — Usability pain point for macOS users. Still open with no assignee.

3. **[RFC: Deconflict Plugin System Goals in FND-001](https://github.com/zeroclaw-labs/zeroclaw/issues/6943)** (4 comments) — Directly related to the WASM plugin direction. This RFC proposes replacing Extism with direct wasmtime component model hosting, which would be a significant architectural change.

4. **[Feature: per-agent custom environment variables](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)** (4 comments) — Addresses multi-tenancy for tool configuration and secrets. This is a high-demand feature for users running multiple agents with different credentials.

**Underlying needs:** The community is intensely focused on:
- **Plugin/SOP architecture** (multiple concurrent RFCs and large PRs)
- **Cross-platform usability** (macOS keybindings, Windows BOM, Chinese locale failures)
- **Multi-agent security isolation** (per-agent env vars, MCP scoping)

## 5. Bugs & Stability

**Critical (P1) bugs active:**

| Issue | Component | Status | Summary |
|-------|-----------|--------|---------|
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | tooling/ci | Open, accepted | **74 test failures on Windows** — Unix-only commands, path semantics, console encoding. No Windows CI coverage. |
| [#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733) | tools (MCP) | Open, in-progress | **`mcp_bundles` is parsed but never enforced** — per-agent MCP scoping is a silent no-op, a security-relevant gap. |
| [#8386](https://github.com/zeroclaw-labs/zeroclaw/issues/8386) | config/onboarding | Open | **SQLite default memory backend silently degrades** — hybrid search falls back to keyword-only because onboarding never prompts for an embedding model. |

**High-severity (P2) bugs active:**

- [#2128](https://github.com/zeroclaw-labs/zeroclaw/issues/2128) — Cron/heartbeat sends literal "NO_REPLY" text to channels (noisy, in-progress)
- [#8366](https://github.com/zeroclaw-labs/zeroclaw/issues/8366) — Heartbeat engine reads from wrong directory (closed, fix merged via #8436 documentation correction)
- [#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800) — macOS keybinding usability (open, no fix PR yet)

**Notable CI/security fixes merged today:**
- [#8326](https://github.com/zeroclaw-labs/zeroclaw/pull/8326) — BOM stripping for Windows users
- [#8404](https://github.com/zeroclaw-labs/zeroclaw/pull/8404) — Cosign signing, SLSA provenance, SBOM for release pipeline (open PR)

## 6. Feature Requests & Roadmap Signals

**High-demand features likely for v0.8.3 or v0.9.0:**

| Feature | Priority | Likelihood |
|---------|----------|------------|
| **Per-agent custom env vars** ([#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)) | P2, needs-author-action | High — directly requested, RFC ready |
| **Telegram multi-message mode** ([#8445](https://github.com/zeroclaw-labs/zeroclaw/issues/8445), new today) | P2, no priority label | Medium — common UX request |
| **Telegram Bot API 10.1 rich messages** ([#8415](https://github.com/zeroclaw-labs/zeroclaw/issues/8415)) | P2 | Medium — improves Telegram UX |
| **Matrix single-message streaming** ([#8442](https://github.com/zeroclaw-labs/zeroclaw/issues/8442)) | P2 | Low — early stage |
| **WhatsApp passive group context** ([#8379](https://github.com/zeroclaw-labs/zeroclaw/issues/8379)) | P2, in-progress | High — feature has a PR path |
| **`zeroclaw.ignore` file mechanism** ([#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424), new RFC) | P2, needs-author-action | Medium — RFC under discussion |

**Roadmap signals:**
- **v0.8.3** is now a major coordination point with 4 active trackers (#8071 runtime/agent/tools, #7314 WASM plugins, #7852 skills platform, #8073 observability/CI/docs)
- **v0.9.0** (#7432) is the auth/security/gateway/breaking-change queue with 101 open issues and 10 PRs as of last refresh
- The **WASM plugin system** is undergoing major restructuring: [#8368](https://github.com/zeroclaw-labs/zeroclaw/pull/8368) replaces Extism with direct wasmtime component model, superseding work from #6943

## 7. User Feedback Summary

**Real user pain points expressed in recent issues:**

1. **macOS usability degradation** ([#7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800)) — "Code/Chat help and keybinding behavior can advertise actions that are hard to discover, especially misleading on macOS." No resolution yet.

2. **Telegram prompt caching broken** ([#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360), closed) — Claude user reported that Telegram forces full prompt reprocessing while CLI works correctly. This was fixed but took 7 weeks from creation to closure.

3. **Windows on-boarding friction** ([#8326](https://github.com/zeroclaw-labs/zeroclaw/issues/8326), fixed today) — Notepad users on Windows couldn't parse config files due to UTF-8 BOM. Quick fix was merged.

4. **Chinese locale test failures** ([#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462)) — "Running the workspace test suite on Windows 11 (Simplified Chinese, console code page 936) yields 74 failing tests." No Linux CI catch. User (NiuBlibing) explicitly filed this — it's a real deployment blocker.

5. **Silent security no-op** ([#7733](https://github.com/zeroclaw-labs/zeroclaw/issues/7733)) — "`mcp_bundles` is parsed and shown in Config but never enforced at runtime — per-agent MCP scoping is a silent no-op." User metalmon expressed concern that maintainers "may want to bump" severity.

**Satisfaction signals:** The volume of active contributors (multiple first-time authors like wangmiao0668000666, Alix-007) and the quick turnaround on some bugs (BOM fix filed 4 days ago, merged today) suggest a healthy, responsive project.

## 8. Backlog Watch

**Long-unanswered issues needing maintainer attention:**

| Issue | Age | Last Activity | Status |
|-------|-----|---------------|--------|
| [#2128](https://github.com/zeroclaw-labs/zeroclaw/issues/2128) — Cron "NO_REPLY" sentinel | 4 months (Feb 27) | Updated June 28 | Open, in-progress — appears to be a stubborn problem |
| [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) — 153 commits lost in bulk revert | 2 months (Apr 24) | Updated June 28 | Open, in-progress — recovery tracking continues |
| [#6360](https://github.com/zeroclaw-labs/zeroclaw/issues/6360) — Telegram prompt caching | 2 months (May 4) | Closed June 28 | Resolved after 7 weeks |
| [#7462](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) — 74 Windows test failures | 19 days (Jun 10) | Updated June 28 | Open, accepted — no fix PR yet |
| [#6943](https://github.com/zeroclaw-labs/zeroclaw/issues/6943) — Plugin system goals deconfliction | 34 days (May 26) | Updated June 28 | Open, accepted — partially addressed by [#8368](https://github.com/zeroclaw-labs/zeroclaw/pull/8368) |

**Unanswered issues from today (zero comments):**
- [#8462](https://github.com/zeroclaw-labs/zeroclaw/issues/8462) — RFC: LLM content capture for observability (new, 0 comments)
- [#8453](https://github.com/zeroclaw-labs/zeroclaw/issues/8453) — `write_lock` dead code cleanup (new, 0 comments)
- [#8442](https://github.com/zeroclaw-labs/zeroclaw/issues/8442) — Matrix streaming mode (new today, 0 comments)

**PRs needing review:** With 46 open PRs, the review queue is substantial. Notable large PRs awaiting review include [#8033](https://github.com/zeroclaw-labs/zeroclaw/pull/8033) (onboarding tree, XL, created 9 days ago) and [#8239](https://github.com/zeroclaw-labs/zeroclaw/pull/8239) (delegate targets, XL, created 6 days ago).

---

**Project Health Assessment:** 🟢 **Active and healthy** — High contributor engagement, responsive maintainers (50 issues/50 PRs updated daily), clear roadmap with incremental version trackers. Risks include: (1) growing PR review backlog (46 open), (2) Windows/Linux parity gaps (74 test failures, silent no-op of security features), and (3) the architectural complexity of the WASM plugin rewrite (risk:high on multiple RFCs).

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*