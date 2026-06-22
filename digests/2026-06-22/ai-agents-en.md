# OpenClaw Ecosystem Digest 2026-06-22

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-22 02:30 UTC

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

Based on the provided GitHub data for the OpenClaw project on 2026-06-22, here is the project digest.

## OpenClaw Project Digest — 2026-06-22

### 1. Today's Overview

OpenClaw is in an **intense cycle of high-velocity development and critical bug fixing**. Activity is extremely high, with 500 issues and 500 PRs updated in the last 24 hours, indicating a very active maintainer and community response. However, the dominant narrative is a **stability crisis** following recent releases. The sheer volume of open, high-severity issues (P1/P2) related to session state loss, message delivery failures, and regressions suggests the project is currently prioritizing stability over new features. A new beta release (`v2026.6.10-beta.1`) was published today, specifically targeting "more reliable agent turns and session state," which directly addresses the most critical cluster of bugs.

### 2. Releases

- **v2026.6.10-beta.1**: A new beta release is available.
    - **Changes**: This release specifically targets core reliability:
        - Preserves pending subagent completion announcements.
        - Keeps chat history transcripts non-empty.
        - Maintains media index alignment.
        - Restarts dormant follow-up drains.
        - Resolves compaction model aliases consistently.
    - **Breaking Changes**: None specified.
    - **Migration Notes**: Standard beta upgrade procedure is assumed.

### 3. Project Progress

Today saw a significant push in open pull requests, indicating rapid iteration on fixes. Notable activity includes:

- **Critical Bug Fixes (P1)**:
    - PRs addressing the critical `tool_use.id` sanitizer bug for cross-provider failover (PR #95634) and stream abort error classification for Bedrock (PR #95632) were created.
    - A fix for the compaction timeout issue was proposed (PR #95580), ensuring preflight compaction respects the configured timeout instead of a shorter reply signal.
- **Platform Stability**:
    - A PR to fix the Telegram silent crash loop after network timeouts was submitted (PR #95626).
    - CI was updated to smooth PR runner registration bursts (PR #95625).
- **Plugin/Provider Fixes**:
    - Fixes to the OTLP log exporter (PR #95635, PR #95636) and Gemini web search handling (PR #95628) were submitted.
    - A fix for the `openclaw doctor` command in Nix mode was proposed (PR #95456).
- **Long-Running Work**:
    - Large PRs from April (#66150, #70046) and March (#46303) were updated, suggesting maintainers are integrating long-standing feature and stability work.

### 4. Community Hot Topics

The community is highly engaged, primarily reporting and discussing severe regressions and stability blockers. The most resonant topics are:

- **Session State & Message Loss (The Core Crisis)**: Issues like **#86538** (Session write-lock timeouts block subagent lanes) and **#86519** (Agent repeats identical replies on Telegram after update) have the highest comment counts (12 and 10, respectively). The high engagement signals this is the community's primary source of frustration.
- **Compaction Timeouts**: Issue **#92043** (180s compaction timeout is a single wall clock) has 8 comments and significant traction. Users are reporting that recent timeout reductions are too aggressive for complex setups.
- **Silent Data Loss**: Issue **#95495** (Silent memory store relocation forcing full re-embed) is a major concern (7 comments) as it involves data loss without warning during a routine upgrade. This is a top anxiety for operators.
- **Channel-Specific Failures**: Issues affecting **Matrix** (#90325), **Telegram** (#93375, #93905), and **Feishu** (#90595) channels have high engagement, indicating that channel stability is a widespread pain point.

### 5. Bugs & Stability

Stability is the single biggest concern, with a large cluster of P1/P2 regressions.

**P1 / Critical (Potential for major session loss or crashes):**
- **Session Write-Lock Timeouts (#86538)**: Blocks subagent delivery lanes. **No fix PR.**
- **Agent Repeats Messages on Telegram (#86519)**: A severe regression after a recent update. **No fix PR.**
- **Memory Store Relocation (#95495)**: Silent full re-embedding of data. **No fix PR.**
- **Compaction Timeout (#92043)**: Single wall-clock timeout causes repeated failures. **Fix PR #95580 submitted.**
- **Tool ID Sanitizer Failure (#95623)**: Cross-provider failover bricks sessions. **Fix PR #95634 submitted.**
- **Telegram Polling Crash Loop (#93375)**: Network timeouts cause unrecoverable crash loops. **Fix PR #95626 submitted.**
- **Subagent Completion Delivery Failure (#92076)**: Subagent results are lost. **No fix PR.**
- **Internal Reasoning Leakage (#91804)**: User privacy/data leak. **No fix PR.**
- **Cron Completion Delivery Fails (#92460)**: Channel is "required" error. **No fix PR.**
- **OAuth Timeout Blocks Cron (#89278)**: Timeout causes cron failures. **No fix PR.**

**P2 / High (Disruptive but less catastrophic):**
- **Active Memory Breaks Prompt Cache (#91223)**: Cache hit rate collapses from ~99.9% to ~22%. **No fix PR.**
- **Stuck-Session Recovery Aborts Long Runs (#88870)**: Aborts legitimate work. **No fix PR.**
- **LLM Request Failed for Isolated Cron (#91363)**: Prevents cron from working. **No fix PR.**
- **Matrix Channel Dispatch Broken (#90325)**: A full channel regression. **No fix PR.**
- **Config Validate Rejects Plugin Extensions (#92884)**: Blocks plugin development. **No fix PR.**
- **`/usage` command broken on Telegram (#93905)**: Latest regression. **No fix PR.**

### 6. Feature Requests & Roadmap Signals

Despite the focus on stability, several feature requests signal the community's future needs:

- **Topic-Session Families (#90916)**: A high-desire feature for advanced users wanting to manage multiple conversation contexts for a single assistant. This is a complex, architectural change.
- **Bounded Memory Flush (#90354)**: A feature to add guardrails to the pre-compaction memory flush, indicating a desire for predictable and safe memory behavior.
- **Documentation Update for Kubernetes (#91455)**: A P3 request, but with 7 comments, it shows growing demand for production-grade, non-trivial deployment documentation.

**Prediction for next version:** The next stable release will likely be **entirely consumed by fixes** for the P1 regressions listed above. Feature work (#90916, #90354) is unlikely to land until the current stability crisis is resolved.

### 7. User Feedback Summary

The user sentiment is currently **strained and frustrated**, driven by repeated regressions that degrade core functionality.

- **Pain Points:**
    - **"The update broke my setup"** is the dominant theme, with multiple reports of major features (Telegram reply, OAuth, cron, Matrix) being broken by upgrades.
    - **Silent failures and data loss** are causing high anxiety, especially the memory store relocation (#95495) and the "delivery-recovery" issue (#91212) which loses messages without notification.
    - **Diagnostic tools are ineffective:** Users report that `stuck-session` diagnostics kill long-running tasks (#88870) and `delivery-recovery` fails silently (#91212).
- **Use Cases at Risk:**
    - **Cron/Automation:** Cron jobs are consistently failing, which is a core use case for many users.
    - **Multi-Channel Assistants:** Users relying on Telegram, Matrix, and Feishu are experiencing broken behavior.
    - **Complex Agent Workflows:** Subagents and sessions are unstable, hampering advanced orchestration.
- **Satisfaction:** Low in the short term. The rapid iteration and creation of fix PRs (#95634, #95626) may restore some confidence, but the project has a steep hill to climb to regain trust.

### 8. Backlog Watch

Several issues and PRs with high priority have been waiting for maintainer attention for an extended period.

- **Issue #67915 (Created Apr 17)**: Local attachments shown as "Unavailable" despite correct config. A P2 bug that has been open for over two months.
- **Issue #86023 (Created May 24)**: Codex long-running sessions need semantic thread cache. This is a performance/correctness issue that has not seen a fix.
- **PR #46303 (Created Mar 14)**: A major fix to prevent message loss during SIGUSR1 reload. This is an XL PR with immense impact that has been in review for 3+ months.
- **PR #59898 (Created Apr 2)**: Fixes for empty tool lists in system prompts. A long-standing issue that could affect agent behavior.
- **PR #67080 (Created Apr 15)**: Narrows gateway plugin routes from manifests. This foundational feature has been waiting for author updates for over 2 months.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the community digest summaries for 2026-06-22.

---

## Cross-Project Ecosystem Report: Personal AI Agent Open-Source Landscape
**Date:** 2026-06-22 & 2026-06-22 (Analysis Date)

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem is characterized by high-velocity development, but the dominant theme is a **crisis of stability**—particularly in the largest projects (OpenClaw, ZeroClaw). While sophisticated features like MCP tooling, agentic memory, and multi-channel support are being rapidly integrated, core reliability is suffering from widespread regressions, memory leaks, and critical bugs in session management, message delivery, and authentication. Security hardening is now a top priority across multiple projects, driven by both external audits and community-reported vulnerabilities. A secondary, yet powerful, trend is the demand for **mobile and cross-platform user experience**, with several projects launching dedicated sprints to improve responsiveness and onboarding.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release (24h) | Health Score | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **ZeroClaw** | 50 | 50 | No | **Stable/High** | Multi-track release planning, high throughput, security hardening |
| **OpenClaw** | 500 | 500 | Yes (beta) | **Crisis/Strained** | Extreme activity prioritizing critical bug fixes & regressions |
| **Hermes Agent** | 50 | 50 | No | **Transitional/High** | Google provider breakage, security patch, high contributor velocity |
| **NanoBot** | 10 | 35 | No | **Healthy/High** | Security patch phase, responsive maintainer, strong community |
| **CoPaw** | 18 | 36 | No | **Active/Healthy** | Mobile sprint, tool scoping, active community with feedback |
| **PicoClaw** | *Moderate* | 32 | Yes (Nightly) | **Stabilizing** | Merging feature series for v0.3.0, high cleanup velocity |
| **IronClaw** | 5 | 29 | No | **Stabilizing** | CI resilience, dependency hygiene, learning system stack |
| **NanoClaw** | 2 | 6 | No | **Maintenance/Security** | Security audit active, patching installation edge cases |
| **LobsterAI** | 15 | 0 | No | **Low/Maintenance** | Stale issue cleanup, one critical security issue |
| **ZeptoClaw** | 1 | 1 | No | **Quiet/Stable** | CI-focused maintenance, no feature development |
| **NullClaw** | 1 | 0 | No | **Low/Stable** | Single bug report, no contributions |
| **TinyClaw** | 0 | 0 | No | **Inactive** | No activity in 24 hours |
| **Moltis** | 0 | 0 | No | **Inactive** | No activity in 24 hours |

### 3. OpenClaw's Position

OpenClaw maintains its position as the **most active and largest project** in the ecosystem by volume, but this activity is currently a double-edged sword. Its advantages are clear: an enormous community and broadest provider/channel support. However, it is currently in a **major stability crisis**, with 500 issues updated daily. The project’s technical approach is highly ambitious, integrating complex agent orchestration (subagents, cron, session state), which is directly causing its current pain points.

- **Advantages vs. Peers:** Unmatched community size (hundreds of issues/PRs), broadest platform support, and frequent beta releases.
- **Technical Approach:** Features a highly complex, stateful architecture (write-lock, compaction, subagent lanes) that enables powerful workflows but is currently fragile.
- **Community Size Comparison:** OpenClaw's community is an order of magnitude larger than any other project (500+ items monthly vs. ~50 for Hermes/ZeroClaw). This creates immense pressure to fix regressions but also provides a massive testing and feedback loop.
- **Key Vulnerability:** The "update broke my setup" sentiment is the highest in the ecosystem, directly threatening user trust.

### 4. Shared Technical Focus Areas

Multiple projects are converging on solving the same core challenges, indicating industry-wide pain points.

1.  **Security Hardening (Critical):**
    - **Projects:** NanoClaw (A2A symlink traversal, approval smuggling), Hermes Agent (cross-session credential leak), OpenClaw (SSRF guards in LobsterAI), ZeroClaw (SSRF, env allowlist, weak pairing codes).
    - **Need:** External security audits are driving immediate fixes for agent-to-agent communication, tool approval flows, and plugin sandboxing.

2.  **MCP (Model Context Protocol) Tooling & Scoping:**
    - **Projects:** NanoBot (allowlist bypass), ZeroClaw (per-agent denylist, tool leakage), IronClaw (MCP "SETUP NEEDED" false positive), OpenClaw (tool ID sanitizer).
    - **Need:** As MCP becomes a standard, projects are struggling with reliable tool registration, security scoping, and avoiding false-positive setup flags.

3.  **Streaming & Session State Reliability:**
    - **Projects:** OpenClaw (session write-lock timeouts, message loss), NanoBot (duplicate `tool_use` ids streaming desync), ZeroClaw (context compression dropping tool results), CoPaw (DeepSeek agent hangs).
    - **Need:** The core chat loop is unstable. Projects are investing heavily in fixing race conditions, desyncs, and state corruption to prevent "agent bricking."

4.  **Mobile & Multi-Platform UX:**
    - **Projects:** CoPaw (dedicated mobile responsiveness sprint), PicoClaw (Safari compatibility issue), Hermes Agent (TUI/Desktop session management pain points).
    - **Need:** Users are accessing agents from mobile browsers and diverse platforms, exposing gaps in UI scaling, channel compatibility (OneBot/NapCat), and device-specific bugs.

### 5. Differentiation Analysis

| Factor | OpenClaw | Hermes Agent | ZeroClaw | NanoBot | CoPaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Target User** | Power user, complex orchestration | Multi-platform, automation-focused | Developer/Operator, WASM plugin oriented | Performance-sensitive, MCP integrator | Broad user, mobile-first, Chinese-speaking |
| **Key Feature Focus** | Agent orchestration, session management, broadest channels | Provider resilience, desktop/TUI, memory plugins | WASM plugin program, security hardening, skills platform | MCP security, streaming reliability, high performance | Mobile UX, message queue management, file sharing |
| **Architecture** | Highly complex, stateful, monolithic | Plugin-based, multi-channel, OAuth-heavy | WASM plugins, multi-track releases, strong API | Plugin-based, config-driven, env-var templating | Message queue, Tauri-based, Chinese cloud providers |
| **Community Demographics** | Massive, global, frustrated | Active, i18n, provider-focused | Active, developer-centric, governance-aware | Smaller, responsive, performance-focused | Active, Chinese, mobile-reporting |

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating / High Momentum (Stressed)**
- **OpenClaw & Hermes Agent:** Both have extremely high issue/PR volumes, driven by crisis (OpenClaw) or major provider transitions (Hermes). They are shipping many fixes but are perceived as unstable.
- **ZeroClaw:** High, organized momentum. The multi-track release strategy and structured backlog suggest strong project management, even while battling P1 bugs.

**Tier 2: Stabilizing / Feature Integration**
- **PicoClaw & CoPaw:** These projects are merging large feature batches (model config, mobile UI). They are in a "sprint" phase, cleaning up for a stable release.
- **IronClaw:** Focused on CI resilience and stabilizing the Reborn runtime after a wave of failures. This is a classic post-release stabilization phase.

**Tier 3: Maintenance / Low Activity**
- **NanoBot, NanoClaw, LobsterAI, NullClaw, ZeptoClaw:** These projects are in a security patch or maintenance mode with low feature velocity. They may be waiting for upstream changes or are in a natural lull.

### 7. Trend Signals for AI Agent Developers

- **The Agent Stability Crisis is Real:** The most advanced features (subagents, cron, complex memory) are introducing unacceptable failure rates. For production deployments, developers should **prioritize projects or versions that explicitly advertise stability patches over new features.**
- **Security is No Longer Optional:** Frequent CVEs and external security audits (e.g., NanoClaw) mean that agent-to-agent communication and tool approval flows must be hardened from the start. **Expect security to be a major differentiator in the next 6 months.**
- **The “Mobile Agent” is the Next Battleground:** Community feedback across CoPaw, PicoClaw, and Hermes strongly indicates users want to interact with agents from their phones. **Projects investing in responsive web UIs or mobile clients will gain a significant user base.**
- **MCP Tooling is Maturing, but Fragile:** The ecosystem is converging on MCP (Context Protocol), but issues with tool scoping, allowlists, and provider-specific bugs are rampant. **Developers must plan for robust MCP error handling and security scoping now.**
- **Provider Lock-in is a Major Risk:** The Google Gemini sunset (Hermes Agent) and OpenAI API changes are causing massive disruption. **Projects that support easy model/provider fallover, or are fully agnostic, are attracting users fleeing this risk.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the project digest for **NanoBot** (github.com/HKUDS/nanobot) for **2026-06-22**.

---

## NanoBot Project Digest – 2026-06-22

### 1. Today's Overview
NanoBot is seeing a **very high level of maintenance activity**, with 35 PRs and 10 Issues updated in the last 24 hours. The project is currently in a **security and stability patch phase**, with multiple concurrent fixes addressing MCP allowlist bypasses, streaming desync issues, and concurrency safety. Community engagement remains strong, driven by Telegram API updates and performance optimization requests. Two critical security vulnerabilities have been reported, indicating a need for urgent maintainer response.

### 2. Releases
**None.** No new releases were published in this period.

### 3. Project Progress
A total of **14 PRs were merged or closed** in the last 24 hours, indicating significant clean-up and feature integration:
- **[PR #4323] – fix(transcription): resolve env vars before transcription config lookup** (Merged by tobrien) – Resolved silent transcription failures by ensuring environment variable templates are resolved before config checks.
- **[PR #4325] – fix(webui): resolve env-var templates in settings update paths** (Merged by tobrien) – Fixed settings API updates that could overwrite credentials with raw `${VAR}` strings.
- **[PR #4324] – fix(webui): resolve env-var templates in settings read paths** (Merged by tobrien) – Ensured read endpoints display resolved credentials rather than raw templates.
- **[PR #4316] – feat(tts): add TTS configuration system with multi-provider support** (Merged by tobrien) – Added a new configurable TTS system supporting OpenAI, Groq (Orpheus), and ElevenLabs, with full WebUI settings integration.

### 4. Community Hot Topics
- **[Issue #1011] – Mattermost Bot (4 👍, Stale)** – A long-standing request for Mattermost integration remains the most upvoted open issue. The community is clearly seeking an open-source alternative to Discord/Telegram/Slack.
- **[Issue #4408] – Concurrency safety bug in Nanobot.run() hooks (CLOSED)** – The most commented issue (2 comments) in the last 24h, resolved quickly by the author. This signals a responsive maintainer team.
- **[Issue #4422] – Telegram Bot API 10.1 sendRichMessage support (CLOSED)** – A fast-moving feature request: opened as an issue but immediately resolved via PR, showing strong maintainer alignment with Telegram API updates.

**Underlying need:** Users are demanding better support for **enterprise/team chat platforms** (Mattermost) and **modern messaging features** (Telegram rich messages). The quick resolution of the Telegram issue suggests this is a high-priority feature area.

### 5. Bugs & Stability
Three bugs and two security issues were reported in the last 24h:

- **[CRITICAL] Issue #4434 & #4435 – MCP `enabledTools` allowlist bypass** – Two related security issues where setting `enabledTools: []` fails to block access to MCP resources and prompts, exposing server capabilities. **Fix PR #4436** exists (open) to gate resource/prompt registration.
- **[HIGH] Issue #4442 – Duplicate tool_use ids in streamed responses** – A streaming desync bug that permanently bricks an Anthropic session with HTTP 400 errors. **Fix PR #4444** (open) and **PR #4443** (open) both target this issue.
- **[MEDIUM] Issue #4408 – Nanobot.run() concurrency (CLOSED)** – A concurrency bug where shared `_extra_hooks` was clobbered under parallel calls. Already fixed.
- **[MEDIUM] Issue #4420 – Redundant tiktoken encoding in `estimate_prompt_tokens`** – A performance regression causing slow response times. Already closed via PR.

**Assessment:** The MCP security bypass is the most critical item. The duplicate `tool_use` bug will affect all streaming Anthropic users and requires immediate attention.

### 6. Feature Requests & Roadmap Signals
- **[Issue #4413] – Telegram Bot API 10.1 rich messages** – Already implemented in PR #4422. Likely to land in the next patch release.
- **[Issue #4440] – Read-only `search_history` tool** – A proposal to expose memory/history.jsonl to the agent without loading it into context. **PR #4439** exists and is open, suggesting this will ship soon.
- **[Issue #4431] – Heartbeat-specific model override** – Request to allow cheaper/dedicated models for the Heartbeat service instead of using the main agent model. No PR yet.

**Predictions:** The `search_history` tool and Telegram rich messages are near-certain for the next release. The heartbeat model override is likely for a minor release after.

### 7. User Feedback Summary
- **Pain Points:**
  - *Concurrency safety*: Users running parallel operations hit shared-state bugs (Issue #4408).
  - *Streaming reliability*: Anthropic sessions can be permanently bricked by stream desync (Issue #4442).
  - *Configuration complexity*: Environment variable templates in config cause silent credential failures (PRs #4323-4325).
- **Satisfaction Signals:**
  - The Telegram API 10.1 feature was requested and implemented almost immediately (Issue #4413 -> PR #4422).
  - Performance optimization (tiktoken caching, Issue #4420) was accepted and closed quickly.
- **Use Cases:**
  - *Performance-sensitive deployments*: Users like `codeLong1024` are building production "digital employees" and hitting tokenization performance bottlenecks.
  - *MCP integration*: Users are deploying NanoBot with MCP servers and relying on the allowlist for security isolation.

### 8. Backlog Watch
- **[Issue #1011] – Mattermost Bot** *(Created 2026-02-22, 4 👍)* – The most stale high-value request. 4 months without maintainer response. This is a significant gap in the project's communication channel strategy. **Needs maintainer triage.**
- **[PR #3869] – DeepSeek message hardening** *(Created 2026-05-16, open)* – An open PR fixing null content errors with DeepSeek providers. No comments from maintainers. This provider-specific fix is languishing despite being ready.
- **[PR #4092] – OpenAI-compatible tool call parsing** *(Created 2026-05-29, open)* – Fixes multiple tool-call parsing bugs. No maintainer review in ~24 days.

**Warning:** The Mattermost and DeepSeek items represent **unmet user demand** and **unmerged fixes** that could harm the project's reputation for provider neutrality and responsiveness.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — June 22, 2026

## 1. Today's Overview

Hermes Agent is experiencing **extraordinary community activity** with 50 issues and 50 PRs updated in the last 24 hours — the highest observed volume in recent weeks. The project is in a **critical transition phase** as Google's Gemini CLI/Code Assist sunset (June 18) has broken a core provider, triggering a wave of bug reports, duplicate issues, and urgent fix PRs. A major **security vulnerability** (cross-session credential leak, P1) was disclosed and promptly patched. The community is highly engaged around provider migration, TUI/Desktop session management, and memory plugin improvements. Despite the turbulence, maintainers are merging fixes at a healthy pace, with 11 PRs closed/merged today.

## 2. Releases

**No new releases today.** The last tagged release remains `v2026.4.3` (April 2026). Given the severity of the Google provider breakage and the security fix merged today, an emergency patch release is likely imminent.

## 3. Project Progress

**11 PRs were merged or closed today**, covering:

| Area | PR | Description |
|------|-----|-------------|
| Security | [#50531](https://github.com/NousResearch/hermes-agent/pull/50531) | Fixes two vectors leaking `HERMES_SESSION_*` env vars across concurrent sessions (P1) |
| CLI | [#50497](https://github.com/NousResearch/hermes-agent/pull/50497) | Banner now only advertises tools/skills actually given to the agent |
| Agent Process | [#50489](https://github.com/NousResearch/hermes-agent/pull/50489) | SIGTERM→SIGKILL escalation for stuck host daemons (from #15008) |
| WhatsApp | [#41866](https://github.com/NousResearch/hermes-agent/pull/41866) | Phone number normalization to full JID for outgoing sends |
| Browser Tool | [#15008](https://github.com/NousResearch/hermes-agent/pull/15008) | SIGTERM→SIGKILL escalation + periodic orphan reaping |
| Provider | [#50492](https://github.com/NousResearch/hermes-agent/pull/50492) | Removes `google-gemini-cli` and `google-antigravity` OAuth providers (accounts being banned) |
| Cron | [#50538](https://github.com/NousResearch/hermes-agent/pull/50538) | Better cron session title reliability with race fix |

A custom dev PR ([#50532](https://github.com/NousResearch/hermes-agent/pull/50532)) was closed as invalid.

## 4. Community Hot Topics

The most active discussions reveal a community **deeply affected by the Google provider shutdown** and **eager for new capabilities**:

1. **[#45500](https://github.com/NousResearch/hermes-agent/issues/45500) — Matrix: text bypasses E2EE (CLOSED, 6 comments)**  
   A security bug where text messages in Matrix rooms skip encryption checks entirely, unlike file attachments. Critical for enterprise Matrix deployments.

2. **[#8950](https://github.com/NousResearch/hermes-agent/issues/8950) — Missing messaging channels (OPEN, 5 comments, 2 👍)**  
   Users want IRC, Google Chat, LINE, Nostr, Twitch, QQBot — comparing feature parity with OpenClaw. Indicates demand for broader platform support.

3. **[#14327](https://github.com/NousResearch/hermes-agent/issues/14327) — Per-platform model config (OPEN, 4 comments, 2 👍)**  
   Users want different LLMs per platform (e.g., Mimo on Feishu, Gemini on Discord). A high-value feature for multi-platform deployments.

4. **[#29294](https://github.com/NousResearch/hermes-agent/issues/29294) — Gemini CLI sunset (CLOSED, 3 comments, 8 👍)**  
   The highest-reacted issue today. Users are anxious about the forced migration to AntiGravity CLI.

5. **[#50530](https://github.com/NousResearch/hermes-agent/issues/50530) — google-antigravity P2 integration bugs (OPEN, 3 comments)**  
   Even the replacement provider has critical issues: delegate crashes, forced re-auth, broken session recovery.

**Underlying need:** The community is demanding **provider resilience** — either stable Google support or graceful fallback mechanisms when providers sunset.

## 5. Bugs & Stability

### Critical (P1)
- **Cross-session credential leak** — [#50531 (PR)](https://github.com/NousResearch/hermes-agent/pull/50531) fixes two vectors where `HERMES_SESSION_*` env vars leaked across concurrent sessions (e.g., Discord `/bug` reading another session's ticket). **Fix merged today.**

### High Priority (P2)
- **google-antigravity P2 integration bugs** — [#50530](https://github.com/NousResearch/hermes-agent/issues/50530): Delegate crashes, forced re-auth, broken session recovery. No fix PR yet.
- **OpenRouter free tier broken** — [#49983](https://github.com/NousResearch/hermes-agent/issues/49983): HTTP 404 on free models due to tool calling not supported. New issue, no fix.
- **Codex image gen plugin 400 error** — [#49008](https://github.com/NousResearch/hermes-agent/issues/49008): `tool_choice` parameter rejected. No fix.
- **MCP OAuth timeout** — [#50485](https://github.com/NousResearch/hermes-agent/issues/50485): 40s connect timeout too short for interactive browser OAuth. Fix needed.
- **TUI sessions don't record cwd** — [#50438](https://github.com/NousResearch/hermes-agent/issues/50438): Desktop can't group TUI sessions by workspace. No fix.
- **Desktop Thinking toggle snaps back** — [#50449](https://github.com/NousResearch/hermes-agent/issues/50449): Config writes stranded `reasoning` key. No fix.
- **Matrix E2EE bypass** — [#45500](https://github.com/NousResearch/hermes-agent/issues/45500): Text messages skip encryption. **Closed but no fix PR linked — may need re-opening.**

### Medium Priority (P3)
- **Duplicate session titles crash** — [#50537](https://github.com/NousResearch/hermes-agent/issues/50537): `ValueError` silently swallowed. No fix.
- **Unicode corruption in patch tool** — [#50540 (PR)](https://github.com/NousResearch/hermes-agent/pull/50540): Fixes Unicode corruption and line-number corruption. **Open PR.**

## 6. Feature Requests & Roadmap Signals

**Likely in next release:**
- **Provider removal/cleanup** — PR [#50492](https://github.com/NousResearch/hermes-agent/pull/50492) removes both Google OAuth providers. This will land soon given Google's active account bans.
- **Per-platform model config** — [#14327](https://github.com/NousResearch/hermes-agent/issues/14327) has maintainer attention and multiple PRs in flight.
- **Dynamic thinking toggle** — [#50293](https://github.com/NousResearch/hermes-agent/issues/50293) and [#50240](https://github.com/NousResearch/hermes-agent/issues/50240) propose self-detecting when deep reasoning is needed. Strong community interest.

**Longer-term roadmap signals:**
- **Self-hosted Mem0 memory** — [#31135](https://github.com/NousResearch/hermes-agent/issues/31135): Add `MEM0_HOST` config for local OSS instance. Stale PRs, but demand exists.
- **Desktop app strategy** — [#41180](https://github.com/NousResearch/hermes-agent/issues/41180): A strategic discussion on whether the desktop GUI risks dumbing down Hermes. No decision yet.
- **More messaging channels** — [#8950](https://github.com/NousResearch/hermes-agent/issues/8950): IRC, LINE, Nostr, Twitch — comparing to OpenClaw's broader support.
- **Human-readable API errors** — [#50460](https://github.com/NousResearch/hermes-agent/issues/50460): Users want usage limit errors translated from raw JSON.

## 7. User Feedback Summary

**Pain points being voiced:**
- **Provider instability is the #1 frustration** — Google's Gemini sunset broke a core provider, and the replacement (AntiGravity) has its own critical bugs. Users feel stuck.
- **Configuration confusion** — Custom provider config ignored ([#8919](https://github.com/NousResearch/hermes-agent/issues/8919)), per-platform settings missing ([#14327](https://github.com/NousResearch/hermes-agent/issues/14327)), home channel setup confusing ([#50541](https://github.com/NousResearch/hermes-agent/pull/50541)).
- **Desktop/TUI unpolished** — Session switching crashes ([#49614](https://github.com/NousResearch/hermes-agent/issues/49614)), wrong session rendering, Thinking toggle snaps, no system tray minimize ([#50167](https://github.com/NousResearch/hermes-agent/issues/50167)).
- **Windows/Matrix setup friction** — [#47759](https://github.com/NousResearch/hermes-agent/issues/47759): Installing Matrix E2EE on Windows has errors.

**Satisfaction signals:**
- **High engagement** — 50+ items updated daily indicates a healthy, active community.
- **Contributor velocity** — 11 PRs merged today, including security fixes and new features.
- **i18n contributions** — Thai translation PRs ([#15151](https://github.com/NousResearch/hermes-agent/issues/15151)) show international community growth.

## 8. Backlog Watch

**Issues needing maintainer attention (age + impact):**

| Issue | Age | Priority | Problem |
|-------|-----|----------|---------|
| [#8919](https://github.com/NousResearch/hermes-agent/issues/8919) | 70 days | P1 | Custom provider config ignored at runtime |
| [#14073](https://github.com/NousResearch/hermes-agent/issues/14073) | 61 days | P1 | Browser orphan reaper can SIGTERM arbitrary processes (closed but root cause unclear) |
| [#45500](https://github.com/NousResearch/hermes-agent/issues/45500) | 9 days | P1 | Matrix E2EE text bypass (closed — verify fix exists) |
| [#8950](https://github.com/NousResearch/hermes-agent/issues/8950) | 70 days | P3 | Missing messaging channels (no maintainer response) |
| [#14327](https://github.com/NousResearch/hermes-agent/issues/14327) | 60 days | P3 | Per-platform model config (no maintainer response) |
| [#31135](https://github.com/NousResearch/hermes-agent/issues/31135) | 30 days | P3 | Self-hosted Mem0 (stale PRs, no action) |
| [#47759](https://github.com/NousResearch/hermes-agent/issues/47759) | 5 days | P2 | Windows Matrix setup error (needs repro) |

**Key concern:** Several high-severity issues (P1/P2) have been open for weeks without maintainer comment. The project's rapid activity is positive, but backlog management is uneven.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is your PicoClaw project digest for the week of 2026-06-22.

---

## PicoClaw Project Digest for 2026-06-22

### 1. Today's Overview
The PicoClaw project is in a period of **intense and mature development**, with 32 pull requests (PRs) updated and a new nightly release pushed in the last 24 hours. The *extremely high* PR activity (29 merged/closed) signals a major push to integrate and finalize a large batch of features and fixes ahead of a stable v0.3.0. The active merger of large feature series (specifically the model configuration and streaming UX overhauls) indicates that the core team is in a "feature freeze" or "stabilization sprint." While community activity is moderate, the maintainers are aggressively clearing the development backlog.

### 2. Releases
- **Nightly Build (v0.3.0-nightly.20260622.287853ab)**: An automated build was released today. It is marked as potentially unstable.
- **Significance**: This nightly is the culmination of the latest batch of merged PRs, including the model configuration suite and streaming improvements. Users testing this version can expect those features, but should be aware of potential instability.
- **Changelog**: [Compare v0.3.0...main](https://github.com/sipeed/picoclaw/compare/v0.3.0...main)

### 3. Project Progress (Merged PRs)
The project made **major strides** in reliability, user experience, and configuration management. Key completed work includes:

- **Model Configuration Overhaul (Merged)**: The massive three-part feature (PRs #2831, #2832, #2833) for improved model configuration is now fully merged. This introduces a new API for fetching models from providers, real connectivity testing, and a foundational model form UI.
- **End-to-End Streaming (Merged)**: PR #2587, a long-running feature for web chat streaming and improved scrolling UX, has been merged, bringing a significant upgrade to the web interface.
- **Core Resilience Fixes**: Several critical bug fixes were merged, including:
    - Crash consistency in the JSONL memory store (PR #2907).
    - Backpressure handling in the message bus (PR #2906).
    - Proper handling of expired contexts in the fallback provider chain (PR #2905).
    - Fixing session index performance issues (PR #2913).
- **New Features**: Added "Reset to Factory Defaults" (PR #2891) and cross-platform serial tool support (PR #2673).

### 4. Community Hot Topics
- **[Feature] I need SimpleX or tox (Issue #3093)**: This open feature request has the most community engagement (2 comments, 1 👍). The user requests gateway support for the SimpleX, Wire, or Tox protocols. This suggests a demand for high-privacy, decentralized communication channels beyond Matrix and Telegram.
    - [Link](https://github.com/sipeed/picoclaw/issue/3093)
- **[BUG] Continuous consumption of tokens every minute when evolution is enabled (Issue #3012)**: An open, high-severity bug report involving the "Evolution" feature causing constant API token consumption. The issue is likely causing unexpected costs for users running this feature.
    - [Link](https://github.com/sipeed/picoclaw/issue/3012)

### 5. Bugs & Stability
**High Priority**:
- **[Open] Continuous token consumption with Evolution (Issue #3012)**: A clear and serious cost/usage bug. Users must disable the "Evolution" feature to avoid unexpected charges.
    - [Link](https://github.com/sipeed/picoclaw/issue/3012)
- **[Open] Panel incompatible with Safari < 16.4 (Issue #3090)**: A significant compatibility issue blocking iOS users on older devices or those who defer OS updates.
    - [Link](https://github.com/sipeed/picoclaw/issue/3090)

**Resolved**:
- **Matrix `allow_from` parsing (Issue #3041)**: Fixed a bug where Matrix user IDs with colons were not being correctly parsed.
- **`mcp add` flag parsing (Issue #3041)**: Fixed a CLI bug where global flags were misinterpreted when adding MCP servers.

### 6. Feature Requests & Roadmap Signals
The biggest roadmap signal is the **recent merge of the massive model configuration improvements (PRs #2752, #2831-2833)**, which is likely the foundation for the upcoming `v0.3.0` stable release.

- **High Probability for Next Release**: The **SimpleX/Tox gateway request (#3093)** aligns with a growing trend toward decentralized and privacy-first communications. Given its community support and the project's existing multi-channel architecture, this is a strong candidate for the next minor version (`v0.4.0`).
- **Speculative**: The extensive work on the web UI streaming (PR #2587) and thought bubble toggling (PR #2661) suggests the team is prioritizing the web chat experience as a competitive feature. Future refinements, such as voice/video or richer message formatting, are likely.

### 7. User Feedback Summary
- **Pain Points**: The primary pain point is the **cost/usage bug with the Evolution feature (Issue #3012)**. This directly impacts users' wallets and is a top-tier stability concern. The **Safari compatibility issue (#3090)** is also dissuading a segment of mobile users.
- **Use Cases**: The request for **SimpleX/Tox (#3093)** and the recent serial tool support (PR #2673) paint a picture of a user base that is not just running a chat bot, but building resilient, private, and hardware-integrated systems.
- **Satisfaction**: The massive volume of merged PRs indicates the team is effectively addressing the community's reported bugs (e.g., Matrix parsing, MCP adds), which builds user trust.

### 8. Backlog Watch
- **[Open - 12 days] Token Drain Bug (Issue #3012)**: This is the **most critical item in the backlog**. It has been open for over a week and involves a core feature (Evolution) draining user credits. No fix PR is linked yet. The community is patiently waiting for a resolution.
    - [Link](https://github.com/sipeed/picoclaw/issue/3012)
- **[Open - 12 days] Safari Compatibility Bug (Issue #3090)**: While lower severity than the token drain, this bug excludes a notable user segment. It is flagged as `stale`, which suggests it might not be a priority for the current v0.3.0 sprint.
    - [Link](https://github.com/sipeed/picoclaw/issue/3090)

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-22

## Today's Overview
Project activity is **moderate-high** today with 2 new security issues opened and 6 PRs updated. The project is in a **maintenance and security-hardening phase**, with no new releases but significant attention to edge-case bugs and vulnerability disclosure. Two critical security advisories (symlink traversal in A2A attachment forwarding, and approval smuggling in `add_mcp_server`) were filed by a security researcher, indicating active external auditing. Three PRs were merged/closed, including an important fix for the setup boot process that had caused first-chat hangs. Total open issues remain stable, but the two security advisories raise the severity profile of the project's open queue.

## Releases
**No new releases** today. The last tagged release remains unchanged.

## Project Progress
Three PRs were merged or closed today:

- **[#2825 — fix(setup): wait for the host socket before failing the first chat](https://github.com/nanocoai/nanoclaw/pull/2825)** — *Merged*. Solves a race condition where the installer's "first chat" test would ping the CLI socket before the host process had fully bound to it, causing false setup failures. Now polls for socket readiness before proceeding.
- **[#2829 — [follows-guidelines] eee](https://github.com/nanocoai/nanoclaw/pull/2829)** — *Closed* (likely test/placeholder PR, no substantive changes).
- **[#2168 — fix(container): pin host.docker.internal to OneCLI's bridge IP in rootless Docker](https://github.com/nanocoai/nanoclaw/pull/2168)** — *Merged*. A long-running fix (opened May 1) that addresses a connectivity issue in rootless Docker environments where `host.docker.internal` would not resolve correctly. Introduces a fallback to pin the mapping directly to OneCLI's bridge IP at container spawn time.

Additionally, two new open PRs were introduced:
- **[#2830 — fix(setup): reap dead peer service registrations whose binary is gone](https://github.com/nanocoai/nanoclaw/pull/2830)** — Proposes cleaning up orphaned launchd/systemd service entries after a NanoClaw checkout is deleted without running the uninstaller.
- **[#2826 — fix(update-skills): nudge into skill updates, rebuild container on re-apply](https://github.com/nanocoai/nanoclaw/pull/2826)** — Changes `/update-nanoclaw` to make skill updates non-optional (previously they were framed as "safe to skip"), and forces container rebuild on re-apply to ensure skill fixes are applied.

## Community Hot Topics
- **No comments or reactions on any items today** — the project sees low community discussion volume, with issues and PRs having 0 comments and 0 reactions each.
- **Longest-running active PR**: **[#2795 — feat: add /add-clidash](https://github.com/nanocoai/nanoclaw/pull/2795)** (6 days since creation) proposes a read-only CLI-derived dashboard utility skill. Still open with no maintainer review.
- **Security researcher activity**: Both new issues (#2827, #2828) were filed by YLChen-007, indicating an external security audit is underway or has been completed. While no comments have been posted, the detailed advisory formatting suggests this is a coordinated vulnerability disclosure effort.

**Underlying needs**: The community appears to be primarily security-focused and seeking better installation reliability. The silent accumulation of orphaned service registrations (PR #2830) and the first-chat boot race (PR #2825) suggest real-world pain around setup friction.

## Bugs & Stability
Two **critical-severity** security bugs were disclosed today:

1. **Critical** — **[#2828: A2A attachment forwarding follows a symlinked inbox and writes outside the target session root](https://github.com/nanocoai/nanoclaw/issues/2828)**  
   *Impact*: A compromised or prompt-injected target agent can place a symlink in its mounted `inbox/` directory. When another agent forwards an attachment, the file is written to the symlink target — potentially outside the session root. This is a path traversal through symlink following.  
   *Status*: No fix PR yet. Requires immediate attention.

2. **Critical** — **[#2827: `add_mcp_server` approval flow hides runtime `args` and `env`, enabling approval smuggling](https://github.com/nanocoai/nanoclaw/issues/2827)**  
   *Impact*: The self-modification approval card for `add_mcp_server` displays only the MCP server name and basic parameters, but hides the `args` and `env` fields. A malicious or pwned agent could inject arbitrary environment variables or arguments (e.g., `--dangerous-flag` or `STEAL_API_KEY=1`) without the user seeing them in the approval prompt.  
   *Status*: No fix PR yet. Requires immediate attention.

3. **Medium** — **[#2830: Dead peer service registrations accumulate when binary is deleted](https://github.com/nanocoai/nanoclaw/pull/2830)** — A fix PR exists but is still open. The problem itself (orphaned launchd/systemd entries) is a reliability issue, not a security vulnerability, but causes silent failure on subsequent installations.

4. **Medium** — **[#2825: First-chat setup failure due to socket race condition](https://github.com/nanocoai/nanoclaw/pull/2825)** — Already merged today. Affects new installations, causing false failures.

## Feature Requests & Roadmap Signals
- **Skill update UX improvement**: PR #2826 signals that the project team recognizes the current skill update flow is too easy to skip. Expect `/update-nanoclaw` to become stricter about applying skill updates in the next patch release.
- **CLI-based dashboard**: PR #2795 requests a read-only dashboard skill derived from CLI commands. This is a low-complexity utility skill and may be merged as-is if maintainers review it.
- **Rootless Docker compatibility**: PR #2168 (now merged) indicates ongoing attention to container networking edge cases. Rootless Docker users can expect improved reliability.
- **Service lifecycle management**: PR #2830 proposes automated cleanup of orphaned service registrations. If merged, this would reduce state corruption from incomplete uninstalls.

**Prediction for next release**: The next patch version will likely include (a) fixes for both security advisories (#2827 and #2828), (b) the socket-wait fix (#2825), and (c) the orphaned service cleanup (#2830). A minor release might include the skill update enforcement (#2826).

## User Feedback Summary
**Pain points detected**:
1. **Installation reliability**: First-time setup failures due to socket race conditions (addressed in #2825).
2. **Incomplete uninstall cleanup**: Deleting a checkout without running uninstaller leaves broken service registrations (PR #2830 addresses this).
3. **Skill update opacity**: Users may unknowingly skip critical skill fixes during host updates (PR #2826 makes updates non-optional).
4. **Container networking**: Rootless Docker users face `host.docker.internal` resolution failures (fixed in #2168).
5. **Security awareness**: Two critical vulnerabilities disclosed suggest that agent self-modification approval flows and cross-agent file sharing need hardened guardrails.

**Satisfaction signals**: No positive user feedback appears in today's data. The project is in a defensive posture — fixing bugs and closing security gaps rather than shipping new features.

**Underlying user behavior**: The issues filed by YLChen-007 (likely a security researcher) suggest that external parties are actively poking at agent-to-agent communication and self-modification surfaces. This is a mature security posture indicator but also implies these features may have been shipped without sufficiently hardened approval prompts.

## Backlog Watch
- **[#2795 — feat: add /add-clidash](https://github.com/nanocoai/nanoclaw/pull/2795)** — Open for 6 days, 0 maintainer comments. A low-risk utility skill. Risk of staling out if not reviewed soon.
- **[#2826 — fix(update-skills): nudge into skill updates, rebuild container on re-apply](https://github.com/nanocoai/nanoclaw/pull/2826)** — Open for 1 day, no maintainer review yet. Addresses a real user-facing UX issue.
- **[#2830 — fix(setup): reap dead peer service registrations](https://github.com/nanocoai/nanoclaw/pull/2830)** — Open for 1 day, no maintainer review yet. Important for install/uninstall hygiene.
- **Both security advisories (#2827, #2828)** — No fix PRs exist yet. These should be the project's highest-priority items, but no maintainer response has been recorded as of this digest. If not addressed promptly, they may become public CVEs bearing on the project's security reputation.

---

*Digest generated 2026-06-22 based on public GitHub activity from nanocoai/nanoclaw.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the project digest for NullClaw, generated from the provided GitHub data for **2026-06-22**.

---

# NullClaw Project Digest – 2026-06-22

## 1. Today's Overview
NullClaw is currently in a **low-activity period** with no new releases, closed pull requests, or merges in the last 24 hours. The project health is stable but quiet, with the primary signal being a single open bug report. The lack of any merged PRs suggests that maintainer focus may be on preparation for a future release or handling incoming issues rather than active feature development. The single issue submitted by a user indicates community engagement is present, though limited.

## 2. Releases
None. No new releases were published in the last 24 hours.

## 3. Project Progress
**Merged/Closed PRs today:** 0
No code contributions or fixes were merged or closed in this period. The project did not advance any features or fix any bugs through PRs.

## 4. Community Hot Topics
- **Issue #967 – [bug] error: NoResponseContent** – *Open | Author: svier0*
  - Comments: 1 | Reactions: 0
  - [Link to Issue](https://github.com/nullclaw/nullclaw/issues/967)
  - **Analysis:** This is the only active discussion point. The user reports a high-frequency (>50%) failure when using a specific model (Agnes-2.0-Flash) with the program version v2026.5.29 on Windows 11. The error `NoResponseContent` appears after a 27-second delay. The underlying need is a **stable output path for the `agent` command**, likely pointing to a regression in the inferencing pipeline or API response handling for that model family.

## 5. Bugs & Stability
- **High Severity: Issue #967 – `error: NoResponseContent`**
  - **Status:** Open, no linked fix PRs.
  - **Impact:** Critical for users of the Agnes-2.0-Flash model on Windows. >50% failure rate in conversations makes the agent unusable for the reporter. The 27-second response time suggests a timeout or malformed response from the inference backend.
  - **Workaround:** Not provided by maintainers; user mentions the same model/API key works in other tools (e.g., picocla... - truncated).

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the underlying signal from Issue #967 is a demand for **robust retry logic or error handling** for model responses. This necessity, combined with the high failure rate, suggests the next release should prioritize improving the stability of the inference client, possibly adding automatic retries on `NoResponseContent` errors or better timeout handling.

## 7. User Feedback Summary
The single user report provides a clear pain point: **unreliable output from a specific model version under Windows**. The user is actively comparing NullClaw to another tool (picocla...) where the same model works, indicating dissatisfaction with NullClaw's current stability. The primary use case is interactive chat (calling `nullclaw agent -m "你好！"`), where consistency is critical.

## 8. Backlog Watch
- **Issue #967** – This is the most pressing item in the backlog. It has been open for 2 days and has yet to receive a maintainer response or a `needs-more-info` label. Given its high severity, it warrants attention. No other long-unanswered issues or PRs were present in this data window.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-22

## 1. Today's Overview

IronClaw Reborn is in an intense phase of **stabilization and feature integration**, with 29 PRs updated in the last 24 hours—two-thirds of which closed or merged. The team is heavily focused on **CI resilience, dependency hygiene, and Reborn runtime improvements** after a recent wave of nightly E2E failures. Five issues were updated, including a new weekly dogfooding tracker for local usability testing. The Reborn learning system stack (WS-1 through WS-3) continues to advance, alongside infrastructure work on concurrent turn execution and hosted Postgres profiles. No new releases were published today.

## 2. Releases

**No new releases.** The latest published version remains unchanged from prior periods.

## 3. Project Progress (Merged/Closed PRs Today)

14 PRs were merged or closed in the last 24 hours. Key advancements:

- **CI Infrastructure (major cleanup):**  
  - `#5118` — Merged: Shared Rust cache across CI closures to prevent per-crate LRU eviction, solving re-download issues.  
  - `#5115` — Merged: Added `CARGO_NET_RETRY` for crates.io network failures in the closure workflow.  
  - `#5113` — Merged: Extracted cross-cutting platform/compatibility jobs into a dedicated `platform-and-compat.yml` workflow.  
  - `#4830` — Merged: Reborn E2E now runs in the merge queue with internal scope gating.  

- **Reborn Runtime & UX Fixes:**  
  - `#4990` — Merged: Fixed NEAR AI MCP ready-state projection so `nearai.web_search` no longer shows "SETUP NEEDED" when properly configured.  
  - `#5065` — Merged: Added one-shot scheduled triggers (`TriggerSchedule::Once{at}`) for fire-once automations.  

- **Dependency Updates (closing stale Dependabot PRs):**  
  - `#4876` — Closed: Bumped 43 dependencies across the everything-else group.  
  - `#4499` — Closed: Updated tokio-ecosystem (tokio-tungstenite, hyper, tokio-postgres-rustls).  
  - `#2927` — Closed: Fixed channel activation on clean installs by wiring `load_startup_active_channels`.  

## 4. Community Hot Topics

**#4925 — [CLOSED] NEAR AI MCP shows "SETUP NEEDED" despite being ready**  
*Author: sunglow666 | 1 comment*  
Summarizes a core UX bug where `nearai.web_search` MCP correctly installed but the WebUI flagged it as requiring setup. This was **resolved by PR #4990** (merged today), which centralizes the NEAR AI host-managed extension identity.  

**#5119 — [NEW] IronClaw Reborn Local Dogfooding Findings (06/22–06/28)**  
*Author: think-in-universe | 0 comments*  
A new weekly tracker launched today to systematically capture first-run usability issues, WebUI startup problems, and model-provider configuration friction. Signals a **proactive shift toward structured UX testing** during the Reborn development cycle.  

**#4108 — [STALE] Nightly E2E failed (open since May 27)**  
*Author: github-actions[bot] | 0 comments*  
This persistent nightly failure for extensions-e2e remains open for 26 days, with no diagnostic comments. Given the CI improvements in today's merges (shared cache, retry logic, merge-queue E2E), this may see resolution soon, but maintainer attention is overdue.

## 5. Bugs & Stability

### High Severity
- **#5071 — [CLOSED] Google OAuth tokens not proactively refreshed before expiry**  
  *Risk: HIGH | Scope: worker, secrets, reborn, OAuth*  
  Resolved in a prior update. Users were forced to re-authenticate hourly; the fix uses refresh tokens to proactively refresh before expiry.

### Medium Severity
- **#4925 — [CLOSED] MCP "SETUP NEEDED" false positive**  
  Fixed by `#4990` — credential prompts suppressed for runtime-managed MCPs.  

- **#4108 — [OPEN] Nightly E2E failing (extensions scope)**  
  Open 26 days with no resolution. The closure of `#4830` (merge-queue E2E) and `#5118` (shared cache) should improve detection, but the root cause remains unaddressed.

### CI Instability (addressed today)
- **Cargo component installer failures** were swallowing errors in live-canary lanes—fixed by `#5101` (reuse of composite action).  
- **Per-crate cache LRU eviction** causing re-downloads—fixed by `#5118`.  
- **crates.io network flakes** in closure jobs—mitigated by `#5115` (retry logic).

## 6. Feature Requests & Roadmap Signals

### Likely in Next Release
1. **One-shot scheduled triggers** (#5065, merged today) — Users can now schedule automations that fire once at a specific datetime, alongside recurring cron. Expect integration into the `/v2/automations` UI.  
2. **Concurrent turn execution** (#5085, open) — `TurnRunScheduler` with per-user/per-type caps to replace the serial turn runner. High priority given LLM inference scalability needs.  
3. **Reborn learning system (WS-3)** (#4975, open) — Turn-completed background reflection that converts failures into memory documents with confidence scoring. Building toward "learn from mistakes, never repeat" capability.  

### Community Requests
- **#5117 — [OPEN] Automation "Completed" summary card** — User requested a **COMPLETED** card in the automation summary strip showing a server-side count of fired one-shots. Complements the **Completed** filter tab from #5065. Low effort, high UX value—likely lands next sprint.  
- **Composio connector route for Workbench** (#5109, open) — An in-gateway route for live connected-account data in the Desktop Workbench. Draft PR from a new contributor; broad utility for third-party integrations.

## 7. User Feedback Summary

- **Satisfaction**: The closure of #4925 (MCP "SETUP NEEDED" false positive) resolves a reported pain point where correctly configured extensions showed unnecessary setup prompts. Users should now see a cleaner MCP management experience.  
- **Pain Points**: Nightly E2E failures (#4108) remain uncommented, leaving contributors without diagnostic context. The new weekly dogfooding tracker (#5119) should surface more structured feedback.  
- **Use Cases**: The learning system stack (#4937, #4975) is designed for Hermes-parity "learn from mistakes" behavior—a direct response to power users needing persistent memory across sessions. Concurrent turn execution (#5085) addresses multi-conversation workloads.

## 8. Backlog Watch

### High Priority (Needs Maintainer Attention)
- **#4108 — Nightly E2E failed** (Open since May 27, 26 days)  
  Stale nightly failure with **zero diagnostic comments**. With CI improvements shipped today, maintainers should: (a) inspect the failing extensions job, (b) add a comment with root-cause analysis, (c) either fix or disable the test.  
  *Link: [nearai/ironclaw Issue #4108](https://github.com/nearai/ironclaw/issue/4108)*  

- **#4002 — Dependabot: bump actions group (16 updates)** (Open since May 24, 29 days)  
  Stale dependency update for GitHub Actions, blocked by merge conflicts. CI will drift without resolution.  
  *Link: [nearai/ironclaw PR #4002](https://github.com/nearai/ironclaw/pull/4002)*  

### Medium Priority
- **#4032 — Dependabot: bump wasm group (wit-component, wit-parser)** (Open since May 25, 28 days)  
  WASM tooling updates; low risk but stale.  
  *Link: [nearai/ironclaw PR #4032](https://github.com/nearai/ironclaw/pull/4032)*  

- **#4498 — Dependabot: bump serde_yml** (Open since June 5, 17 days)  
  Serialization dependency; small scope.  
  *Link: [nearai/ironclaw PR #4498](https://github.com/nearai/ironclaw/pull/4498)*  

### Note
The dependabot staleness pattern (multiple PRs >2 weeks old) suggests a need for **automated merge-queue or batching strategy** for low-risk dependency updates—especially given today's merges of #4876 and #4499 (both old dependabot PRs). Merging #5116 and #5114 would clear the backlog.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Based on the GitHub data provided for **LobsterAI** (github.com/netease-youdao/LobsterAI), here is the project digest for **2026-06-22**.

---

## LobsterAI Project Digest: 2026-06-22

### 1. Today's Overview
The LobsterAI project appears to be in a period of **low activity** regarding new contributions, with zero Pull Requests updated in the last 24 hours and no new releases. However, the community is actively cleaning up the backlog, as evidenced by a flurry of activity closing **14 stale issues**. The sole new issue today is a high-severity security vulnerability report (Issue #2181), which demands immediate attention. Overall, the project is showing signs of maintenance mode with a focus on old issue resolution rather than active feature development.

### 2. Releases
**None.** There are no new releases recorded in the last 24 hours.

### 3. Project Progress
**No Pull Requests were updated (merged, closed, or opened) in the last 24 hours.**

The majority of project progress was the automated or manual closure of **14 stale issues**, primarily related to UI/UX bugs reported in early April. While these closures suggest a cleanup effort, the lack of linked fix PRs for these issues means that the underlying problems may still exist in the codebase.

### 4. Community Hot Topics
The most active issue by comments is a **Security vulnerability** report.

- **Issue #2181: [Security] LobsterAI restores private-network browser access by default and weakens the bundled OpenClaw SSRF guard**
  - **Comments:** 0 (most recent, opened today)
  - **Reactions:** 0
  - **Summary:** A critical security flaw where the browser settings layer defaults to a `ProxyCompatible` mode that disables SSRF protection, potentially exposing private network hosts.
  - **Link:** [Issue #2181](https://github.com/netease-youdao/LobsterAI/issues/2181)

**Analysis:** Despite having no comments or reactions yet, this issue is the most significant as it was opened today. This signals a newly identified security risk that the community and maintainers should prioritize immediately.

### 5. Bugs & Stability
**No new bugs were opened today.** The 14 issues closed were all **stale** bugs from April, including:
- **Disabling skills still active** ( #1500 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1500)
- **Agent setting sync failure** ( #1502 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1502)
- **GitHub Copilot OAuth token loss** ( #1516 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1516)

**Severity Note:** While these bugs have been closed, there is no evidence of associated fix PRs. The underlying issues are likely **unresolved** in the current codebase.

### 6. Feature Requests & Roadmap Signals
Today’s closure of 7 feature request issues (all marked as stale) suggests that the **roadmap for these features has not been prioritized**. These include:
- **Session color coding** ( #1525 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1525)
- **Batch export of sessions** ( #1528 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1528)
- **Local usage statistics** ( #1532 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1532)
- **Message bookmarking** ( #1537 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1537)
- **Session tag/filter system** ( #1541 ) - [Link](https://github.com/netease-youdao/LobsterAI/issues/1541)

**Prediction:** Given the absence of development activity and the closure of these requests, it is **unlikely** these features will appear in the next version. The focus is shifting to security and maintenance.

### 7. User Feedback Summary
The closed issues provide a snapshot of past user dissatisfaction, mainly centered on **poor user experience and incomplete workflows**:
- **Lack of feedback:** Users reported frustration when long-running tasks (skill generation) blocked progress with no visible feedback ( #1509 ).
- **Sync/State issues:** The most common complaints involved state not syncing between UI settings and actual functionality ( #1500 , #1502 ), requiring workarounds like switching agents.
- **Missing validations:** Form submissions that save empty or invalid data (e.g., missing IM session selection, missing AES Key) lead to silent failures ( #1504 , #1506 ).

### 8. Backlog Watch
The single most critical item needing urgent attention is:

- **Issue #2181: Security Vulnerability (SSRF)** - [Link](https://github.com/netease-youdao/LobsterAI/issues/2181)
  - **Status:** Open, unassigned, no comments
  - **Risk:** **Critical.** This affects the core security model of the bundled browser access.
  - **Recommendation:** The maintainer should assign this immediately, acknowledge it, and provide a timeline for a fix or disable the vulnerable mode.

There are no other long-unanswered issues in the current data, as the recent sweep cleared the backlog of stale items.

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

# CoPaw Project Digest — 2026-06-22

**Generated from:** github.com/agentscope-ai/CoPaw

---

## Today's Overview

CoPaw saw high activity over the past 24 hours with **18 issues updated** (15 open, 3 closed) and **36 PRs updated** (32 open, 4 merged/closed). There were **no new releases** today. The project is in an active development and bug-fixing phase, with significant community engagement around stability issues (message queue cross-talk, file preview regressions, and model provider compatibility). A notable cluster of **mobile responsiveness PRs** (6+ PRs from multiple contributors) suggests a coordinated push to improve the mobile experience. The high open-PR count (32) indicates a healthy contribution pipeline but also potential reviewer bottleneck.

## Releases

**No new releases today.** The latest known release is `v1.1.12.post1` (referenced across multiple issues).

## Project Progress

**PRs merged/closed today (4):**

- **#3831** [CLOSED] `Add vector model connection test feature` (by no-teasy) — Adds ability to test vector model connections in the provider configuration UI. *(Under review since April, finally closed)*
- **#5270** [CLOSED] `Sprint 3.1-3.4 integration tests` (by yutai78786) — Large test suite (64 cases) covering ACP Runner interop, Plugin system, Security, and cross-cutting concerns. Signals maturation of testing infrastructure.
- **#5320** [CLOSED] `send_file_to_user image not displayed` — Bug report diagnosed and fixed in PR #5324 (still open).
- **#5353** [CLOSED] `Feishu group chat @-mention requirement` — Bug confirmed and closed; likely a configuration documentation issue.

**Features that advanced (open PRs with recent updates):**

- **#5371** (fix/queue): Binds agent ID at enqueue time to prevent cross-agent message delivery — directly targets the "queue cross-talk" bug (#5354).
- **#5357** (fix/session-switch): Releases session switch lock in embedded mode — addresses session switching getting stuck.
- **#5321** (scroll context manager): New retrieval-driven context management strategy using SQLite — durable conversation history with on-demand recall via REPL.
- **#5347** (fix/crons): Drops invalid jobs.json entries on startup — defensive migration for malformed job configs.

## Community Hot Topics

### Most Active Issues (by comment count):

1. **#5262** [OPEN] `[Bug]: 每次升级之后，被禁用的内置技能又会重新变回启用2.0` — **8 comments**  
   *Author: daigoopautoy*  
   **Summary:** Repeated regression across versions (1.1.9→1.1.10→1.1.11): disabled built-in skills (docx, xlsx) re-enable after every upgrade. User reports this is the **second time filing this issue** (#4807 was the first).  
   **Link:** [Issue #5262](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5262)  
   **Analysis:** This is a persistent quality-of-life bug that frustrates power users. The fact it's been reported twice suggests either the fix was incomplete or the skill state persistence mechanism is fundamentally fragile.

2. **#5329** [OPEN] `[Feature]: 在左边的侧边栏进入简介模式后，添加一个切换agent的按钮` — **5 comments**  
   *Author: bob-geek11*  
   **Summary:** Mobile browser user requests an agent-switching button in collapsed sidebar mode. Also requests moving "view chat history" and "new chat" buttons from top to sidebar to avoid clipping on small screens.  
   **Link:** [Issue #5329](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5329)  
   **Analysis:** Directly tied to the mobile responsive push. PR #5334 already addresses the agent-switching button gap.

3. **#5354** [OPEN] `[Bug]: 消息发送队列容易串台；切换对话时切不回去` — **4 comments**  
   *Author: renzhong424*  
   **Summary:** Message queue "cross-talk" — messages typed in Agent A's queue but sent to Agent B after switching agents. Also: session switching can get stuck (conversation grays out and becomes unswitchable).  
   **Link:** [Issue #5354](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5354)  
   **Analysis:** **Critical usability bug.** A fix PR (#5371) was opened today — binding agent ID at enqueue time — which suggests the root cause is a race condition in the queue's agent-scoping logic.

### Most Active PRs (by comment count):

None of today's PRs had explicit comment counts recorded. However, the following PRs have been "Under Review" for extended periods:

- **#4622** (datapaw plugin, 12 BI skills) — Open since May 22, still under review. Large feature addition.
- **#5321** (scroll context manager) — Open since June 19, under review. Significant architectural change.
- **#5040** (cron job tolerance) — Open since June 9, under review. Alternative approach to #5347.

## Bugs & Stability

### Critical:
- **#5370** [NEW] `send_file_to_user results in HTTP 404` — FileBlock generates `file:///` URL; frontend strips absolute path, only preserves filename when constructing preview URL.  
  **Fix PR:** None yet.  
  **Severity:** High — breaks file preview for users on v1.1.12.post1.  
  **Link:** [Issue #5370](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5370)

- **#5354** [NEW] `Message queue cross-talk; session switch gets stuck` — **See Community Hot Topics.**  
  **Fix PR:** #5371 (opened today)  
  **Link:** [Issue #5354](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5354)

### High:
- **#5344** [UPDATED] `POST /api/console/chat returns 200 but silently drops messages when agent busy` — Silent data loss is dangerous.  
  **Fix PR:** None yet.  
  **Link:** [Issue #5344](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5344)

- **#5345** [OPEN] `Custom OpenAI-compatible providers (OMLX) don't support function calling` — Models return text only, never call tools.  
  **Fix PR:** None yet. Likely need to inspect how custom provider headers/handlers are passed.  
  **Link:** [Issue #5345](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5345)

### Medium:
- **#5358** [NEW] `TypeError: Cannot read properties of null (reading 'object')` in UI bundle during session switch — Frontend crash.  
  **Fix PR:** #5357 (opened today) partially addresses the session switch lock but may not solve this exact TypeError.  
  **Link:** [Issue #5358](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5358)

- **#5328** [OPEN] `DeepSeek agent hangs during thinking; needs manual stop+continue` — Occurs across web, console, and Tauri.  
  **Fix PR:** None yet. Likely LLM-specific timeout or streaming issue.  
  **Link:** [Issue #5328](https://github.com/agentscope-ai/QwenPaw%20Issue%20#5328)

### Lower Severity / Regressions:
- **#5262** (skills re-enable on upgrade) — Persistent regression, second report.
- **#5330** (Zhipu provider: API-level test passes, model-level tests fail) — Setup/debugging friction.
- **#5320** (send_file_to_user image not displayed) — Closed; fix in PR #5324.

## Feature Requests & Roadmap Signals

**Likely in next version:**

1. **Mobile responsiveness (6+ PRs today):** PRs #5361–#5369 adapt Settings/Models, Security, CronJobs, Sessions, Channels, Agent Config pages for narrow viewports. This is a **coordinated sprint** — highly likely to land in next release.

2. **Sidebar collapsed mode agent switching:** Issue #5329 → PR #5334. Directly addresses user complaint.

3. **Scroll context manager (PR #5321):** SQLite-backed conversation history with REPL recall. If reviews are positive, could be an experimental feature toggle in next release.

**Future roadmap signals:**

4. **Model failover (Issue #5351):** User requests automatic failover between local/cloud models. The `RoutingChatModel` class exists but is never instantiated — this is a gap between design and implementation.

5. **Recency-aware memory search (Issue #5316):** User wants recent daily notes to rank higher in `memory_search` results.

6. **Agent office interaction (Issue #5327):** User wants "💬 Chat" button on agent cards in the Agent Office page to start conversations directly.

7. **Real-time UI update for API messages (Issue #5322):** `POST /api/console/chat` messages don't appear in the UI until manual refresh; user wants SSE/WebSocket push.

8. **Hard cap on tool result size (Issue #5342):** Defense-in-depth against context explosion when LLM calls fail and the pruning hook is skipped.

## User Feedback Summary

**Satisfaction indicators:**
- The message queue feature (Issue #5354) is welcomed — user says it's a "great improvement that greatly improves efficiency." However, the cross-talk bug is a significant pain point.
- Mobile browser access is being actively used — multiple users report accessing QwenPaw via phone browsers, indicating real demand for mobile support.

**Pain points:**
- **Stability on DeepSeek models** (Issue #5328, #5333): Agents hang during thinking, requiring manual intervention. This affects user trust in the system.
- **Upgrade friction** (Issue #5262): Skills re-enable on every upgrade — users feel punished for upgrading.
- **Silent failures** (Issue #5344): API returns 200 but message is dropped when agent busy — no feedback to user.
- **Custom provider incompatibility** (Issue #5345): Users who want to use non-standard OpenAI-compatible backends (OMLX) hit a wall.
- **Mobile UX gaps** (Issue #5329): Critical buttons (chat history, new chat) are off-screen on mobile.

**Quoteworthy feedback:**
- Issue #5360 (by Jailtonfonseca): *"Before adding new features, it would be fundamental to make the app fully functional and resolve existing core stability/usability problems."* — A clear signal from the community that stability should take priority over new features.

## Backlog Watch

**Issues needing maintainer attention:**

1. **#5262** (skills re-enable on upgrade) — **Second report** (first was #4807). Needs a permanent fix. Age: 5 days. Severity: P2.

2. **#5040** (cron job tolerance) — Open PR since June 9, still "Under Review." An alternative PR (#5347) was opened today with a different approach. Decision needed on which to merge.

3. **#4622** (datapaw plugin) — Open since May 22 (31+ days). Large feature PR. If no maintainer bandwidth, should communicate timeline to contributor.

4. **#5322** (real-time UI update for API messages) — Closed without merging the feature; user requested it but no PR followed. If the team rejects this design, should explain why.

**PRs needing review:**

- **#5371** (fix queue cross-talk) — **High priority:** Critical bug fix.
- **#5357** (fix session switch lock) — **High priority:** Addresses UI freezing bug.
- **#5324** (fix file preview download vs. inline) — **High priority:** Regression fix for image display.

**Note:** The backlog of 32 open PRs is growing. The team should consider a review throughput improvement (e.g., triage sessions, clearer acceptance criteria, or more reviewers).

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-06-22

## Today's Overview
ZeptoClaw shows a quiet maintenance day with no new releases and low activity across the board. One issue and one PR were both closed within the last 24 hours, reflecting steady CI-focused stewardship rather than feature development. The project's strategic emphasis remains on binary size control, with today's completed work tightening the CI gating mechanism. Overall project health appears stable, with critical infrastructure improvements being finalized rather than new functionality being introduced.

## Releases
<!-- No new releases recorded today. -->

## Project Progress
- **#611 [CLOSED]** `chore(ci): promote binary-size to PR gate at 7.5MB` — This PR merged the final step to make binary size enforcement a hard gate on pull requests, not just a post-merge check. It removes the `if:` guard that restricted the size check to main-only, and lowers the threshold from 7MB to 7.5MB. This creates a proactive CI guardian against binary bloat.

## Community Hot Topics
No issues or PRs with significant comments or reactions were active today. The single closed issue (#537) and PR (#611) generated zero discussion, suggesting the community accepts these CI changes as uncontroversial maintenance.

## Bugs & Stability
No new bugs, crashes, or regressions were reported today. The single closed issue (#537) was a chore/CI task, not a stability defect.

## Feature Requests & Roadmap Signals
No user-requested features appeared in today's activity. The CI gate changes reflect a proactive infrastructure concern (binary size) that the maintainer appears to prioritize, likely to preserve ZeptoClaw's suitability for embedded/robot deployments where every megabyte matters.

## User Feedback Summary
With no issues or PRs containing user commentary today, explicit user feedback is absent. The maintainer's actions imply a tacit assumption that users value keeping the agent's binary as small as possible—consistent with ZeptoClaw's positioning for resource-constrained environments.

## Backlog Watch
No long-unanswered issues or PRs were flagged today. The project's backlog appears well-tended, with the oldest updated item being the now-closed issue #537 from April 2026. No items currently require maintainer attention.

*All data sourced from [github.com/qhkm/zeptoclaw](https://github.com/qhkm/zeptoclaw).*

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-22

## Today's Overview

ZeroClaw is in a period of **intense stabilization and planning** for the v0.8.x release line. Activity is **very high**: 50 issues and 50 PRs were updated in the last 24 hours, with 14 issues closed and 11 PRs merged. The project has no new releases today, but maintainers are actively tracking **four parallel milestone trackers** (v0.8.1, v0.8.2, and two v0.8.3 child trackers), indicating a multi-track release strategy. The community is deeply engaged on long-running RFCs, security hardening, and MCP tool integration, while the core team is systematically closing out v0.8.0 blockers and v0.8.1 integration work. Project health appears **stable with high throughput**, though several P1 bugs remain open and the 153-commit revert audit (#6074) signals some past turbulence.

## Releases

**No new releases today.** The project appears to be between versions, with v0.8.0 recently shipped (tracker #7112 closed today) and v0.8.1/v0.8.2/v0.8.3 in active development.

## Project Progress

**11 PRs were merged or closed today**, reflecting meaningful forward motion:

- **WASM/Plugin Security**: #5918 (SSRF protection for `zc_http_request`) and #5919 (`zc_env_read` allowlist) remain open P1 security features being actively discussed, indicating the plugin security model is under final design.
- **ZeroCode UX**: #7857 (skip queue-paused hint when backlog empty) and #7999 (surface active config directory) merged — both improve the ZeroCode web dashboard's usability.
- **Channel Fixes**: #7912 (WhatsApp storage mutation-MAC fix) merged, fixing a critical pairing failure in WhatsApp channel.
- **Observability**: #8065 (correlate logs by `trace_id` + `cost_usd`) and #8066 (opt-in LLM request payload capture) are open but moving — these represent a significant observability upgrade for v0.8.2/0.8.3.
- **MCP Tool Scoping**: #8120 (scope MCP tools per-agent with denylist) — open, addressing a reported tool-leak bug from Discord.
- **Cross-Platform CI**: #7486 (non-required cross-platform Clippy) closed — a maintenance win for catching macOS/Windows lint regressions.

The **v0.8.0 release tracker (#7112)** closed today, signaling that v0.8.0 is considered shipped and the team has pivoted fully to v0.8.1+ work.

## Community Hot Topics

### Most Active Issues (by comments)

1. **#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup** (11 comments)  
   [zeroclaw-labs/zeroclaw Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)  
   *Analysis*: A governance RFC proposing automated routing of work across lanes. With 11 comments over a month, this is the community's most-discussed meta-process topic. The RFC is "accepted/rollout in progress," suggesting the community is actively shaping how ZeroClaw's own development workflow is managed.

2. **#2503 — "where is napcat channel"** (9 comments)  
   [zeroclaw-labs/zeroclaw Issue #2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503)  
   *Analysis*: A long-running feature request (since March) for OneBot/NapCat protocol support. The user cannot find the option to connect OneBot bots. This reflects a real gap in channel coverage — the community wants broader IM protocol support beyond the current Telegram/WhatsApp/Discord set.

3. **#2467 — Webhook transforms** (6 comments)  
   [zeroclaw-labs/zeroclaw Issue #2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467)  
   *Analysis*: A feature request for custom webhook path transforms and payload inspection. The user specifically cites GitHub webhooks not working with arbitrary payloads. This is a key gateway integration gap — accepted but not yet implemented.

4. **#4760 — Tool-calling for memory consolidation** and **#6289 — Prompt-triggered install suggestions** (4 comments each)  
   [zeroclaw-labs/zeroclaw Issue #4760](https://github.com/zeroclaw-labs/zeroclaw/issues/4760)  
   [zeroclaw-labs/zeroclaw Issue #6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)  
   *Analysis*: Both are accepted enhancement RFEs. #4760 would replace fragile JSON parsing in memory consolidation with proper tool-calling — a reliability win. #6289 would surface installable skills when users ask for missing capabilities — a discoverability win.

### Most Active PRs (by commit activity)

All 20 top PRs by comment count show `undefined` comments in the data (likely a metric collection issue), but the following stand out for being actively updated:
- **#7836** (fix channels/orchestrator tool parsing config) — P1 fix updated today
- **#7945** (xAI OAuth login support) — large feature PR, 2 days old
- **#8119** (apply MCP policy to channel tool prompts) — security fix opened today
- **#8120** (scope MCP tools per-agent) — opened today, addresses tool leak

## Bugs & Stability

### Critical / S1-S2 Bugs Open

| Issue | Severity | Component | Summary | Fix PR? |
|-------|----------|-----------|---------|---------|
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) | S1 | Gemini CLI OAuth | Authentication fails immediately after success, blocking all Gemini usage | No fix PR |
| [#6361](https://github.com/zeroclaw-labs/zeroclaw/issues/6361) | S1 | Context compression (MiniMax) | Tool results dropped during compression, causing tool loops and invalid messages | No fix PR |
| [#7756](https://github.com/zeroclaw-labs/zeroclaw/issues/7756) | S1 | MCP tools on OpenAI Responses/Anthropic | Tools registered but not received by model, blocking MCP workflows | No fix PR |
| [#8094](https://github.com/zeroclaw-labs/zeroclaw/issues/8094) | S0 | Quickstart/Anthropic | New provider unusable until reset — labeled S0 (data loss/security risk) | No fix PR |
| [#5918](https://github.com/zeroclaw-labs/zeroclaw/issues/5918) | P1 | SSRF protection | Plugins can reach internal networks via HTTP tool | Open discussion |
| [#5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919) | P1 | Env var allowlist | Plugins with `env_read` can read any environment variable | Open discussion |
| [#6613](https://github.com/zeroclaw-labs/zeroclaw/issues/6613) | P1 | Weak pairing code | 6-digit numeric pairing codes are too weak | Accepted, no PR |
| [#7038](https://github.com/zeroclaw-labs/zeroclaw/issues/7038) | P2 | WebSocket 401 | `zeroclaw check` fails auth despite valid config | Blocked, needs repro |

### New Bugs Today

- **#8094** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/8094)) — Anthropic provider added in Quickstart unavailable until reset (S0 severity, open)
- **#8089** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/8089)) — Docker build fails due to missing `aardvark-sys/build.rs` (CLOSED, likely quick fix)
- **#7756** ([link](https://github.com/zeroclaw-labs/zeroclaw/issues/7756)) — MCP tools unavailable on OpenAI Responses/Anthropic (S1, accepted)

### Fixes in Flight

- **#7836** (fix channels/orchestrator tool parsing config) — addresses config resolution bug affecting all channels
- **#8048** (keep tool-result content under context pressure) — fixes history pruning override bug
- **#8119** (apply MCP policy to channel tool prompts) — security fix for tool leakage
- **#7485** (fix doctor validation of custom providers) — fixes false-positive validation errors

## Feature Requests & Roadmap Signals

### Likely for v0.8.2 (WASM Plugin Program + Skills Platform)

The **#7314 tracker** (WASM plugin program) and **#7852 tracker** (skills platform) are both active with child issues. WASM plugin security is the critical prerequisite: #5918 (SSRF) and #5919 (env allowlist) must land before plugins can ship safely. The skills platform tracker **#7852** suggests missing-capability suggestions and skill-audit visibility are planned.

### Likely for v0.8.3 (Gateway, Web, ZeroCode, Onboarding)

Three child trackers opened June 20:
- **#8072** — Channels, providers, config behavior
- **#8071** — Runtime, agent, tools, execution stability
- **#8070** — Gateway, web, ZeroCode, onboarding surfaces

These signal that v0.8.3 will focus on operator-facing polish: web dashboard improvements, ZeroCode UX, and onboarding flow enhancements.

### Community-Requested Features Gaining Traction

- **xAI/Grok OAuth** (#7945) — Large PR adding first-class Grok support, likely for v0.8.2
- **Turn-level OTel traces** (#6641, #6642) — Observability improvements for debugging
- **Local-First Mode for small models** (#5287) — 2 👍, accepted, in-progress
- **Stronger pairing codes** (#6613) — Accepted P1, security-critical
- **Webhook transforms** (#2467) — Accepted but no implementation yet

## User Feedback Summary

### Pain Points

1. **Authentication failures**: Multiple users report OAuth and auth token issues — Gemini CLI (#4879), WebSocket 401 (#7038), and the new Quickstart Anthropic bug (#8094) suggest the auth system has systemic fragility.

2. **Channel gaps**: Users want OneBot/NapCat (#2503, 9 comments) and report that Telegram prompt caching doesn't work (#6360). The LINE channel contributor (#7768) is actively improving that channel, suggesting community-driven channel development.

3. **MCP Tool Visibility**: Perlowja (#7756) reports that MCP tools are registered but models don't see them on certain providers — a fundamental reliability issue for the MCP integration strategy.

4. **Context compression bugs**: Ralfbawg (#6361) reports that context compression drops tool results entirely on OpenAI-compatible providers, making multi-turn tool conversations unusable with MiniMax.

### Positive Signals

- **Active community contributors**: Multiple PRs from non-core contributors (ZOOWH, legokichi, dvgamerr, Nillth, danielO99, chengzhichao-xydt, hanZeng-08, crh-code, Pick-cat) demonstrate a healthy contributor base.
- **Observability investment**: Users JordanTheJet and alexandme are driving OTel trace integration (#6641, #6642), suggesting power users value debuggability.
- **Plugin ecosystem anticipation**: The WASM plugin program (#7314) and SSRF/env discussions show the community is actively shaping plugin security before launch.

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Status | Age | Why It Matters |
|-------|--------|-----|----------------|
| [#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) — NapCat/OneBot channel | Accepted, no-stale | ~3.5 months | 9 comments, active user demand, no implementation assigned |
| [#2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467) — Webhook transforms | Accepted | ~3.5 months | 6 comments, core gateway feature, no PR |
| [#4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721) — Log to stderr | Accepted, no-stale | ~3 months | 3 comments, breaks CLI piping |
| [#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074) — 153-commit revert audit | In-progress | ~2 months | 2 comments, needs sustained attention — 153 lost commits is a large debt |
| [#7038](https://github.com/zeroclaw-labs/zeroclaw/issues/7038) — WebSocket 401 | Blocked, needs repro | ~22 days | User cannot use `zeroclaw check` at all |

### PRs Needing Review

| PR | Age | Component | Risk |
|----|-----|-----------|------|
| [#7945](https://github.com/zeroclaw-labs/zeroclaw/pull/7945) — xAI OAuth | ~4 days | Auth | `size: XL`, new provider integration needs careful security review |
| [#8066](https://github.com/zeroclaw-labs/zeroclaw/pull/8066) — Opt-in LLM payload capture | ~2 days | Observability | Privacy-sensitive feature, default-off but needs data-handling audit |
| [#7985](https://github.com/zeroclaw-labs/zeroclaw/pull/7985) — Image generation attachment paths | ~3 days | Tools | Automated PR, trivial but touches asset path resolution |

The 153-commit revert audit (#6074) is a **chronic risk** — incomplete recovery of lost commits means bugfixes and features from a 2-month window may be silently missing. This should be prioritized as it undermines confidence in the git history.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*