# OpenClaw Ecosystem Digest 2026-06-24

> Issues: 187 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-24 01:58 UTC

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

Based on the GitHub data from OpenClaw for 2026-06-24, here is the project digest.

## OpenClaw Project Digest — 2026-06-24

### 1. Today's Overview
The project is in a period of high-intensity maintenance and stabilization. Very high pull request volume (500 updated in 24 hours) indicates significant parallel development, though a low merge rate (34 closed/merged out of 500) suggests a bottleneck in code review and merging. Issue activity is also high (187 updated), with a strong focus on session state integrity, message delivery reliability, and regression triage from recent v2026.6.x upgrades. Despite the lack of new releases today, the volume of `P1` labeled issues and linked build-up of fix PRs suggests a significant patch release is likely imminent.

### 2. Releases
**No new releases today.** The last known release baseline is v2026.6.9, with the latest issues referencing v2026.6.10-alpha.2.

### 3. Project Progress
In the last 24 hours, **34 PRs were merged or closed**, indicating stability patches and small fixes were landed. Notable progress points include:
- **ACP Runtime Fixes:** PR #93465 (Windows ACPX spawn failure) was closed, likely fixing a critical Windows blocker for the embedded ACP runtime.
- **Model Compatibility:** Issue #88657 (DeepSeek V4 Flash incomplete turns) has been closed, suggesting a fix was applied for the regressed model compatibility.
- **Session Integrity:** Multiple link-less fix PRs are queued for sticky session locks (#95833), compaction timeouts (#92043), and subagent delivery (#92076), indicating a large batch of session-state fixes is ready for merge.
- **Platform Tooling:** PR #96175 (fix memory index backup) provides a fix for the `openclaw memory` CLI tool.

### 4. Community Hot Topics
The most active community engagements (sorted by comments) highlight deep, systemic issues:

- **#88838 - SQLite Migration Seam (35 comments):** [Issue Link](openclaw/openclaw Issue #88838)
  A critical Path 3 initiative to move session/transcript storage behind an accessor seam. This is a foundational refactor to solve session-state corruption and migration failures. Users are heavily engaged in validating the new seam behavior.
- **#96148 - iMessage Source-Reply Latency (17 comments):** [Issue Link](openclaw/openclaw Issue #96148)
  A high-interest performance investigation into iMessage response delays. Users are analyzing tracing data from patched worktrees, suggesting a complex, real-world performance issue affecting Mac users.
- **#92201 - Invalid Anthropic Thinking Signatures (14 comments):** [Issue Link](openclaw/openclaw Issue #92201)
  An intermittent but severe bug where streaming `thinking` blocks have invalid signatures on replay. The frustration is high because the error recovery wrapper is silently failing, making the system appear to work incorrectly.
- **#90991 - Cron Triggers Cause System Overload (14 comments, Closed):** [Issue Link](openclaw/openclaw Issue #90991)
  A major bug where a cron-scheduled trigger contaminated global state, causing "system-wide overload failures." The closure suggests a fix was applied, offering relief to users experiencing transient outages.

**Underlying Needs:** Users are deeply concerned with data integrity (session loss, lock exhaustion), performance under load (cron & multi-session slowdowns), and the reliability of mission-critical integrations (iMessage, Anthropic).

### 5. Bugs & Stability
Reported bugs are dominated by session state corruption and provider incompatibilities. Ranked by severity:

- **Critical (P1, Diamond Lobster):**
  - **Session Lock Deadlock (#95833):** Subagent abort-settle fails to release `.jsonl.lock`, permanently breaking the session until manual intervention. **Fix PR exists (linked).**
  - **Thinking Signature Brick (#94228):** Long tool-use threads on native Anthropic path brick permanently with `Invalid signature` errors. **Fix PR exists.**
  - **Compaction Timeout Crash (#92043):** 180s single-wall-clock timeout causes legitimate compactions to fail every turn. Wastes user time and resources. **Fix PR exists.**
  - **Ollama Stream Never Consumed (#94251):** Remote Ollama provider streaming fails silently—no model output is ever consumed. This is a beta release blocker for self-hosted users.
- **High (P1, Platinum Hermit):**
  - **DeepSeek Cache Hit Rate <10% (#94518):** A severe regression in prompt caching after the 6.x upgrade, drastically increasing costs for DeepSeek users.
  - **6.x State Migration Orphans References (#94939):** SQLite migration leaves conversation store empty (0 bytes), breaking proactive sends in MS Teams.
- **Medium (P2):**
  - **Telegram Rich Messages Broken (#95554):** v2026.6.9 regression causes paragraph breaks and table rendering to fail in Telegram.
  - **Dreams Not Promoting (#96118, Closed):** BUG in v6.9 where memory promotion is completely broken, resulting in a dash in the Dreams UI.

### 6. Feature Requests & Roadmap Signals
The following user-requested features indicate the likely direction for upcoming releases:

- **MCP as Compaction Provider (#96156):** [Issue Link](openclaw/openclaw Issue #96156)
  A highly agile request to allow any MCP tool to serve as a compaction engine. This would dramatically expand customization for third-party and local summarization tools. **Prediction:** High probability for next minor release due to the platform's heavy focus on plugin extensibility.
- **Session Naming & Slash Commands (#93422):** [Issue Link](openclaw/openclaw Issue #93422)
  Users want `/label` and `/new` commands for session management in the WebChat UI. This is a high-quality-of-life change. **Prediction:** Likely for next release given the UI-focused PRs in the queue.
- **Global SSRF Policy (#93068):** [Issue Link](openclaw/openclaw Issue #93068)
  Request for a single, unified policy for private network access instead of per-subsystem opt-in. This is a security-adjacent feature. **Prediction:** Likely blocked on security review, but conceptually accepted.
- **Agent-Facing Scheduling API (#71712):** [Issue Link](openclaw/openclaw Issue #71712)
  An RFC to allow agents to manage their own cron jobs. This is a heavy architectural change and remains backlogged, but the discussion is ongoing.

### 7. User Feedback Summary
- **Pain Points:** The overriding theme is "loss of trust in state." Users report sessions becoming permanently locked (#95833), messages showing up out of order (#95566), and recovery mechanisms misleadingly reporting "aborted by user" (#88870). The stability regression in DeepSeek caching (#94518) is causing significant cost anxiety.
- **Use Cases:** 80% of issues relate to production-level deployments: multi-session operation (#92057), cross-platform delivery (Telegram, Discord, Feishu), and long-running agent workflows (compaction, subagents).
- **Dissatisfaction:** The frequency of regression bugs (e.g., Dreams UI in v6.9, Telegram rendering in v6.9) is causing friction. Several users explicitly note issues "worked before 6.x upgrade" (#94518).
- **Satisfaction:** Active engagement in issue threads and code tracing (e.g., #96148) shows a technically sophisticated, invested user base willing to debug and propose fixes.

### 8. Backlog Watch
Several high-signal items remain stagnant and require maintainer attention:

- **#46284 (Stale): MathJax/LaTeX Support (8 comments, 7 👍):** [Issue Link](openclaw/openclaw Issue #42840)
  A top-voted feature request with no movement. Users are frustrated showing raw LaTeX to non-technical users.
- **#49931 (Stale): Configurable Shell Override (6 comments):** [Issue Link](openclaw/openclaw Issue #49931)
  Windows users are stuck with PowerShell and cannot use `jq`, regex, or complex pipes. A security review is pending, blocking a significant platform parity fix.
- **#73910 (Stale): Codex ACP Auth Bridge (4 comments, P1):** [Issue Link](openclaw/openclaw Issue #73910)
  OpenClaw-managed Codex sessions are still broken due to an isolated auth environment. This bug impacts the primary Codex ACP integration path and has been open since April.
- **#46548 (Stale): Tool Error Messages Silently Fail (5 comments):** [Issue Link](openclaw/openclaw Issue #46548)
  Users receive only "Edit failed" with no reason. This has been open since March and directly reduces trust in the agent's actions.
- **PR Backlog:** Notable large PRs like #79882 (shared MCP runtime scope) and #77492 (pre-auth CPU DoS fix) have been "waiting on author" for weeks, holding up critical performance and security improvements.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report as requested.

---

## Cross-Project Comparison Report: Personal AI Assistant Ecosystem
**Analysis Date:** 2026-06-24

### 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is in a state of **high-velocity maturation**, characterized by a shift from proof-of-concept projects to production-focused engineering. The dominant themes across all projects are **security hardening**, **token/cost efficiency**, and **platform reliability** (Windows, Android, Docker). While several projects (OpenClaw, Hermes Agent, CoPaw) are experiencing intense development cycles with hundreds of PRs, they are also grappling with the growing pains of regression bugs in complex features like session state, cron scheduling, and multi-provider support. The ecosystem is bifurcating between **general-purpose orchestration platforms** (Hermes, OpenClaw) and **specialized or lightweight agents** (NanoBot, PicoClaw), with a clear demand for mobile support and enterprise-grade credential management emerging as cross-cutting requirements.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | Release Today | Health Score | Key Signal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 187 | 500 | 34 | No | **Green** | High PR volume but low merge ratio (6.8%); bottleneck in review |
| **Hermes Agent** | 50 | 50 | 8 | No | **Green** | Healthy balance of triage and PR throughput |
| **CoPaw** | 38 | 50 | 28 | **Yes (v1.1.12.post2)** | **Green** | High merge throughput; focused on clearing backlog |
| **IronClaw** | 21 | 42 | 19 | No | **Green** | Strong architectural feature development (Reborn) |
| **NanoBot** | 11 | 39 | 7 | No | **Green** | High velocity on provider compatibility and PWA |
| **PicoClaw** | 2 | 17 | 6 | No | **Green** | Security and platform bug fixing focus |
| **ZeroClaw** | 39 | 50 | 5 | No | **Yellow** | High engagement but low merge rate; heavy RFC focus |
| **LobsterAI** | 1 | 11 | 5 | No | **Yellow** | Active feature work but critical bug from April unresolved |
| **NanoClaw** | 1 | 12 | 8 | No | **Yellow** | High merge ratio but almost no community discussion |
| **Moltis** | 0 | 1 | 1 | No | **Green** | Very low activity but fully cleared backlog |
| **NullClaw** | 1 | 1 | 0 | No | **Green** | Quiet maintenance phase |
| **TinyClaw** | 0 | 0 | 0 | No | **Low** | Inactive |
| **ZeptoClaw** | 0 | 0 | 0 | No | **Low** | Inactive |

### 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale & Community:** OpenClaw has the largest activity footprint by far (500 PRs, 187 issues), indicating the largest contributor base and the most widespread adoption. No other project approaches this volume.
- **Systemic Issue Focus:** The community is tackling foundational problems (SQLite migration seam, session lock deadlocks, compaction timeouts) that other projects are not yet addressing, suggesting a more mature user base running production deployments.
- **Platform Extensibility:** The MCP as Compaction Provider feature request (#96156) and the ACP runtime hints at a plugin-first architecture that is more advanced than peers like NullClaw or PicoClaw.

**Technical Approach:**
- OpenClaw relies on a **heavy core** (Java/Go) with complex session state management and a `openclaw memory` CLI. This contrasts with NanoBot's lightweight TypeScript approach and PicoClaw's Go-based single-binary delivery. The overhead is a source of its session-locking bugs.

**Community Size & Weaknesses:**
- The community is technically sophisticated but frustrated by regression frequency. The 6.8% merge rate (34 merged out of 500 updated) is the lowest among active projects, signaling a **severe bottleneck in code review** that could demotivate contributors. This contrasts with CoPaw (56% merge rate) and NanoClaw (67%).

### 4. Shared Technical Focus Areas

The following cross-cutting requirements are emerging from user feedback and bug reports across multiple projects:

1.  **Credential & Token Security** — Multiple projects are struggling with the security-vs-usability tradeoff.
    - *Hermes Agent*: Password redaction (`***`) breaks second tool calls (#43083).
    - *IronClaw*: Google OAuth buttons show false "success" toasts for invalid tokens (#3733).
    - *PicoClaw*: Fixed cross-site launcher hijacking and exec allow-rule bypass (#3160, #3161).

2.  **Reliable Cron & Scheduling** — A critical feature for production deployments, currently fragile.
    - *OpenClaw*: Cron triggers cause system overload (#90991, closed).
    - *CoPaw*: Agent-created cron tasks fail to trigger; scheduler stops dispatching (#5064, #5398).
    - *IronClaw*: Scheduler heartbeat self-deadlocks (#5148).

3.  **Mobile & Cross-Platform Parity** — Users demand consistent experiences on mobile OSes.
    - *NanoBot*: PWA support and iOS Safari composer zoom fix in active development (#4457, #4471).
    - *Hermes Agent*: Termux OOM fixes for Android (#51601).
    - *PicoClaw*: Process hooks crash on Android/Termux (#3164).
    - *CoPaw*: Mobile responsiveness PRs under review (#5368, #5394).

4.  **Token Efficiency & Cost Control** — Users are actively measuring and demanding optimizations.
    - *Hermes Agent*: User-measured 73% fixed overhead (~13.9K tokens per call) (#4379); Lazy Tool Schema Loading proposal (#6839).
    - *OpenClaw*: DeepSeek cache hit rate regression to <10% (#94518).
    - *PicoClaw*: AWS Bedrock prompt caching (#3163).
    - *IronClaw*: Progressive tool disclosure to cut prompt size from 25.8K tokens (#5149).

### 5. Differentiation Analysis

| Project | Primary Focus | Target User | Tech Stack | Key Differentiator |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | Production-grade core | Enterprise ops teams | Java/Go, heavy core | Session state management, ACP runtime, MCP extensibility |
| **Hermes Agent** | Orchestration & security | Power developers | Python, multi-agent | ACP client for multi-agent orchestration; Tirith approval gates |
| **CoPaw** | Rich UI & skill ecosystem | Desktop power users | Python (Tauri/WebUI) | Feature-rich console, skill marketplace, plugin system |
| **IronClaw** | Platform (Reborn) | Devs building on NEAR | Rust, WASM plugins | WASM-based tool execution; ongoing from-scratch rewrite |
| **NanoBot** | Lightweight & fast | Individual tinkerers | TypeScript, WebUI | PWA mobile support, rapid provider compatibility (OpenCode, Kimi) |
| **PicoClaw** | Channel connectivity | Multi-channel users | Go, single binary | Extensive channel support (WhatsApp, QQ, Telegram); security-first |
| **ZeroClaw** | Supply-chain security | Security-aware users | Rust, WASM + CUDA | Hardware PGP, SLSA provenance, hermetic builds, cosign signing |
| **LobsterAI** | Gateway & coworkers | Chinese-speaking users | TypeScript, Electron | LiteLLM provider support; cowork session management |
| **NullClaw** | Automation | Automation engineers | Python | Cron subagent engine with DB-backed scheduler and JSON CLI |
| **NanoClaw** | Chat SDK integration | Developers | TypeScript, Chat SDK | Slack Socket Mode, approval workflow extension points |

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High Velocity, High Maturity)**
- **OpenClaw**: Despite low merge ratio, the sheer volume and system-level focus signal a mature project with a large, technically capable user base.
- **Hermes Agent**: The most **balanced** ecosystem. High PR throughput, deep performance analysis from users, and clear architectural direction (multi-agent orchestration, lazy loading).
- **CoPaw**: Highest merge throughput of any major project. The release of v1.1.12.post2 today demonstrates a reliable release cadence. The community is productive and vocal, though bug count is rising.

**Tier 2: Actively Building (High Velocity, Still Maturing)**
- **IronClaw**: Strong architectural focus with the Reborn rewrite, but the high number of open PRs (23) and long-standing Google auth issues (38 days) suggest a project still stabilizing its new core.
- **ZeroClaw**: High community engagement on architectural RFCs (supply chain, WASM) but very low merge rate (10%). The project is more focused on design decisions than shipping features.
- **NanoBot**: High development velocity but a small community dialogue. Provider compatibility and PWA are the main drivers.

**Tier 3: Stabilizing / Low Activity**
- **PicoClaw**: Quiet but effective. Focused on bug fixing and security hardening with a small, core team.
- **NanoClaw**: High code output but almost no community discussion. Features (Slack Socket Mode) are being built in silence.
- **Moltis**: Clearing its backlog and entering a maintenance phase. Healthy but dormant.
- **NullClaw**: Single-PR development pipeline. Quiet maintenance.
- **LobsterAI**: Active development is happening, but **a critical, 82-day-old bug** (Issue #1400) with no maintainer response is a major red flag for community trust.

### 7. Trend Signals for AI Agent Developers

1.  **From Single-Agent to Multi-Agent Orchestration**: Hermes Agent's generalized ACP client (#5257, 16 👍) and IronClaw's "delegate mode" (#8238) signal an ecosystem shift where agents act as managers for other agents (Claude Code, Cline, Goose). Value: **Build your agent to be both a tool and a controller.**

2.  **Mobile-First is No Longer Optional**: PWA support (NanoBot), Termux fixes (Hermes), mobile UI PRs (CoPaw), and Zoom Safari fixes are appearing across the board. Desktop-only agents are being left behind. Value: **Invest in mobile web or PWA for your agent's frontend.**

3.  **Security is Becoming a Differentiator (and a Pain Point)**: Credential redaction breaking workflows (Hermes), false success toasts (IronClaw), and supply-chain hardening (ZeroClaw) show that security is no longer a checkbox but a **core UX issue**. Value: **Invest in credential lifecycle management (revocation, refresh, audit) and explicit user confirmation for sensitive operations.**

4.  **Token Efficiency is a Measurable KPI**: Users are no longer just complaining—they are building monitoring dashboards (#4379, Hermes) and proposing specific architectural changes (lazy loading, progressive disclosure). Value: **Measure and communicate token overhead to your users; make efficiency a product feature, not an internal metric.**

5.  **Cron/Scheduler Reliability is a Maturity Gate**: The fact that three major projects (OpenClaw, CoPaw, IronClaw) all have active, high-severity cron bugs suggests that background execution is the hardest problem to solve in agent systems. Value: **Treat scheduling as a first-class, stateful system with health checks, not a simple timer.**

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-06-24  
**Source:** github.com/HKUDS/nanobot

---

## 1. Today's Overview

NanoBot shows extremely high development velocity with **39 PRs updated in the last 24 hours** (7 merged/closed), signaling a deeply active maintainer and contributor community. However, only 4 of 11 issues were resolved in the same period, suggesting the project is currently prioritizing feature development and infrastructure fixes over bug triage. The absence of any new releases indicates the project may be accumulating changes for a significant upcoming version. The community is highly engaged, with particular focus on provider compatibility fixes, PWA support, and Telegram integration improvements.

---

## 2. Releases

**No new releases today.** The last release appears to be v0.2.2 (referenced in issue #4470). Given the volume of merged PRs and new features (PWA, new providers, memory systems), a release may be imminent.

---

## 3. Project Progress

**7 PRs merged/closed today**, representing significant forward momentum:

| PR | Title | Status | Impact |
|---|---|---|---|
| [#4443](https://github.com/HKUDS/nanobot/pull/4443) | fix: guard against duplicate tool_use ids in streamed responses | **Merged** | Critical fix preventing session-bricking HTTP 400 errors with Anthropic-family providers |
| [#4474](https://github.com/HKUDS/nanobot/pull/4474) | fix(provider): deduplicate parallel tool_use ids in AnthropicProvider | **Merged** | Complementary fix for Kimi Coding endpoint compatibility |
| [#4393](https://github.com/HKUDS/nanobot/pull/4393) | test(exec): cover git commands in workspace subdirectories | **Merged** | Regression test coverage for workspace restriction |
| [#4387](https://github.com/HKUDS/nanobot/pull/4387) | fix(context): fall back to default memory bootstrap | **Merged** | Memory loading reliability improvement |
| [#4417](https://github.com/HKUDS/nanobot/pull/4417) | test(mcp): use resolvable timeout regression URL | **Merged** | CI stability fix |
| [#4458](https://github.com/HKUDS/nanobot/pull/4458) | feat(webui): add PWA support for mobile home screen installation | **Closed (invalid)** | Superceded by #4480 |
| [#4457](https://github.com/HKUDS/nanobot/pull/4457) | feat(webui): add PWA support | **Closed** | Issue closed alongside PR |

**Key advancements:**
- **Anthropic/Kimi provider stability** now has multiple merged fixes for tool call ID deduplication
- **Context/memory system** received fallback improvements for bootstrap loading
- **WebUI PWA support** is actively in development (see open PR #4480)

---

## 4. Community Hot Topics

| Item | Type | Comments | 🔥 | Summary |
|---|---|---|---|---|
| [#2298](https://github.com/HKUDS/nanobot/issues/2298) | Issue (OPEN) | 5 | 0 | **Breaking endless tool calling loops** — A long-standing (3 months) pain point where smaller/local models enter infinite tool call loops. The author proposes loop detection logic. **High interest given 5 comments** |
| [#4470](https://github.com/HKUDS/nanobot/issues/4470) | Issue (OPEN) | 1 | 0 | **Telegram display bug** — Two regressions: newlines ignored (text as single block) and message flickering/constant editing. Directly affects user experience |
| [#4473](https://github.com/HKUDS/nanobot/issues/4473) | Issue (CLOSED) | 1 | 0 | **Parallel tool_use ids duplicate in AnthropicProvider** — Root cause analysis of Kimi Coding endpoint issue, now fixed in PR #4474 |
| [#4465](https://github.com/HKUDS/nanobot/issues/4465) | Issue (OPEN) | 1 | 0 | **`<thinking/>` tags rendered as visible text** — WebUI leaks model control text to users instead of rendering as reasoning blocks |
| [#4433](https://github.com/HKUDS/nanobot/issues/4393) | PR (MERGED) | - | 0 | Test coverage for git commands — community contributor yu-xin-c providing quality assurance |

**Analysis:** The community is most concerned about three categories:
1. **Provider compatibility** — Anthropic/Kimi streaming issues dominate
2. **UI/UX regressions** — Telegram and WebUI rendering problems
3. **Model loop detection** — A 3-month-old feature request still unanswered

---

## 5. Bugs & Stability

### Critical Severity
- **[#4470](https://github.com/HKUDS/nanobot/issues/4470) — Telegram display bug** (OPEN)
  - _Impact:_ Two regressions (newlines ignored, message flickering) in Telegram integration
  - _Fix:_ [PR #4472](https://github.com/HKUDS/nanobot/pull/4472) exists — skips `sendRichMessage` when streaming preview is present

- **[#4465](https://github.com/HKUDS/nanobot/issues/4465) — `<thinking/>` tags rendered as visible text** (OPEN)
  - _Impact:_ Model control text leaks to users in WebUI
  - _Fix:_ [PR #4466](https://github.com/HKUDS/nanobot/pull/4466) exists — normalizes thinking block handling

### High Severity
- **[#4410](https://github.com/HKUDS/nanobot/issues/4410) — Unwanted messages after upgrade** (CLOSED)
  - _Impact:_ Cron/heartbeat agent sending messages when it shouldn't (regression from v0.15)
  - _Status:_ Closed, presumably fixed

### Medium Severity
- **[#4478](https://github.com/HKUDS/nanobot/pull/4478) — Dream cron config silently removed on save** (OPEN)
  - _Impact:_ User-provided cron overrides lost on config save
  - _Fix:_ PR exists, awaiting merge

- **[#4441](https://github.com/HKUDS/nanobot/pull/4441) — MCP gateway crash on reconnection** (OPEN)
  - _Impact:_ `RuntimeError: Attempted to exit cancel scope in a different task` — crashes gateway
  - _Fix:_ Force-close streamable HTTP generator

### Low Severity
- **[#4471](https://github.com/HKUDS/nanobot/pull/4471) — iOS Safari composer zoom** (OPEN)
  - _Impact:_ Visual distortion on mobile WebUI
  - _Fix:_ Fix exists (16px font-size enforcement)

---

## 6. Feature Requests & Roadmap Signals

### High Likelihood for Next Release

| Feature | Issue/PR | Signal |
|---|---|---|
| **PWA Support** | [#4457](https://github.com/HKUDS/nanobot/issues/4457), [#4480](https://github.com/HKUDS/nanobot/pull/4480) | Two PRs in 24h, active development with mobile swipe gestures |
| **OpenCode Zen & Go Providers** | [#4475](https://github.com/HKUDS/nanobot/issues/4475), [#4476](https://github.com/HKUDS/nanobot/pull/4476) | Complete PR ready, adds two new provider endpoints |
| **Kimi Coding Plan Support** | [#4463](https://github.com/HKUDS/nanobot/issues/4463) | PR #4464 exists, critical for paid subscription users |
| **Custom Provider Thinking Style** | [#4482](https://github.com/HKUDS/nanobot/pull/4482) | Enables non-standard thinking parameters (e.g., VolcEngine/Doubao) |

### Medium Likelihood

| Feature | Issue/PR | Signal |
|---|---|---|
| **Lifecycle Wiki Memory Writer** | [#4477](https://github.com/HKUDS/nanobot/pull/4477) | Adds Dream-only memory with expiry, corrections, forgetting |
| **Eager Memory Consolidation** | [#4402](https://github.com/HKUDS/nanobot/pull/4402) | Opt-in archival of completed conversations |
| **Hide Reasoning Steps Toggle** | [#2305](https://github.com/HKUDS/nanobot/issues/2305) | 3-month-old request but recently activity (closed 6/23) suggests it's being addressed via normalization of `<thinking/>` tags |

### Low Likelihood / Long-Term

| Feature | Issue/PR | Signal |
|---|---|---|
| **Dream Skill Update (No Duplicates)** | [#4467](https://github.com/HKUDS/nanobot/issues/4467) | Enhancement request, no PR yet |
| **Endless Tool Call Loop Detection** | [#2298](https://github.com/HKUDS/nanobot/issues/2298) | 3 months old, no maintainer response |

**Prediction:** The next version will likely include PWA support, OpenCode providers, Kimi Coding integration, and the Telegram/webui fixes bundle.

---

## 7. User Feedback Summary

### Pain Points (Dissatisfaction)

1. **"Telegram is broken after upgrade"** — Two distinct regressions in Telegram display, direct user frustration (#4470)
2. **"Dream creates duplicate skills"** — User maintains custom workspace skills, Dream overwrites them (#4467): *"I'm always frustrated when Dream creates new skills under `skills/` every time it runs"*
3. **"Upgrade sent unwanted messages"** — Cron agent behavior changed silently (#4410)
4. **"Smaller models loop endlessly"** — No mitigation for infinite tool call loops (#2298)
5. **"Thinking tags leak to UI"** — Technical users noticing model artifacts in chat (#4465)

### Positive Signals (Satisfaction)

- Contributor **zpljd258** is actively adding provider support (OpenCode, Kimi, PWA) — indicates the ecosystem is growing
- **yu-xin-c** is providing extensive test coverage and memory fixes — suggests the testing infrastructure is maturing
- Multiple contributors filing and fixing bugs (michaelxer, axelray-dev, chengyongru, ZhouJ-sh) — healthy community

### Use Case Patterns

| Use Case | Evidence |
|---|---|
| **Telegram as primary interface** | #4470, #4472 — users expect reliable mobile messaging |
| **Paid model providers** | #4463 — Kimi Coding Plan, users paying for subscriptions |
| **Custom/local models** | #2298 — smaller models popular but problematic |
| **Coding agents** | #4475, #4476 — OpenCode providers specifically for coding |
| **Mobile web access** | #4457, #4479, #4480 — PWA and swipe gestures for on-the-go use |

---

## 8. Backlog Watch

### Critical Unanswered Issues

| Issue | Age | Problem | Status |
|---|---|---|---|
| [#2298](https://github.com/HKUDS/nanobot/issues/2298) — Endless tool call loops | **3 months** | Smaller models infinite loop with tool calls | **No maintainer response**, 5 comments from community |
| [#2305](https://github.com/HKUDS/nanobot/issues/2305) — Hide reasoning steps toggle | **3 months** | Request to hide reasoning display | **Recently closed** (6/23) via thinking tag normalization, but the toggle feature itself has no PR |

### Open PRs Needing Attention

| PR | Age | Issue | Risk |
|---|---|---|---|
| [#3732](https://github.com/HKUDS/nanobot/pull/3732) — Require api_base before local provider wins | **6 weeks** | Cleanest local provider match | Silent hijacking of cloud models — high impact if defective |
| [#4373](https://github.com/HKUDS/nanobot/pull/4373) — Preserve delivery context during consolidation | **8 days** | Memory loss during consolidation | Could lead to lost conversation context |
| [#4441](https://github.com/HKUDS/nanobot/pull/4441) — MCP force-close on reconnect failure | **3 days** | Gateway crash | RuntimeError crash, needs expedited review |

### Recommendations for Maintainers

1. **Address [#2298](https://github.com/HKUDS/nanobot/issues/2298)** — The endless loop issue has been open for 3 months with no official response. This appears to be a widely experienced pain point for local model users.
2. **Merge Telegram fix ([#4472](https://github.com/HKUDS/nanobot/pull/4472))** — Telegram regressions are causing immediate user dissatisfaction
3. **Review MCP crash fix ([#4441](https://github.com/HKUDS/nanobot/pull/4441))** — RuntimeErrors in MCP can cause production instability
4. **Consider a patch release** — With 7+ fixes ready, a v0.2.3 could resolve many open bugs before the larger feature release

---

*Generated from 11 issues, 39 PRs, 0 releases. Data reflects activity from 2026-06-23 to 2026-06-24 UTC.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-06-24

---

## Today's Overview

Hermes Agent is experiencing a high-activity period with **50 issues and 50 pull requests updated in the last 24 hours**, reflecting sustained community engagement and rapid development velocity. The project maintains a healthy balance of active issue triage (41 open/active, 9 closed) and PR progress (42 open, 8 merged/closed). No new releases were cut today, but the volume of contributions suggests a forthcoming release may incorporate several of the merged fixes—particularly around Windows platform stability, security hardening, and core agent token efficiency. The community is deeply engaged in both bug reporting and feature prototyping, with several discussions reaching double-digit comment counts on complex architectural topics.

---

## Releases

No new releases were published today.

---

## Project Progress

**8 pull requests merged or closed today**, indicating active advancement across multiple subsystems:

- **[PR #51621]** – `fix: require explicit URL intent for browser tools` (merged) – Adds a shared URL-intent guard for `browser_navigate` and `web_extract` tools, blocking passive pasted URLs unless the current user turn explicitly authorizes the exact target. This is a significant **security boundary hardening** that closes potential injection vectors via browser tools. [View PR](https://github.com/NousResearch/hermes-agent/pull/51621)

- **[PR #51601]** – `fix(update): reuse an existing uv on Termux instead of source-building` (merged) – Addresses a critical Termux usability issue where `hermes update` could OOM-kill low-memory Android devices by compiling uv from source. Now reuses system-installed uv from PATH. [View PR](https://github.com/NousResearch/hermes-agent/pull/51601)

- **[PR #51295]** – `fix(computer_use): adapt cua-driver backend to 0.6.x capture API` (merged) – Fixes broken `computer_use` tool captures on macOS with cua-driver 0.6.x where vision mode returned zero-width/zero-height captures and SOM mode produced empty labels. [View PR](https://github.com/NousResearch/hermes-agent/pull/51295)

- **[PR #51125]** – `feat(session_search): semantic/hybrid search with sqlite-vec` (closed as duplicate, but likely superseded by #44093 which remains open and progressing) – Signals strong community desire for semantic search capabilities.

- **[PR #49615]** – `fix(gateway): eliminate console window on uv-venv Windows gateway launches` (merged) – Resolves a long-standing Windows UX issue where gateway processes opened persistent console windows.

- **[PR #48626]** – `fix(update): reuse an existing uv on Termux instead of source-building` (merged) – Earlier iteration of the Termux fix, now superseded by #51601.

- **[PR #39152]** – `fix(update): avoid source-building uv on Termux` (merged) – Another Termux uv resolution improvement, demonstrating sustained effort on mobile platform support.

---

## Community Hot Topics

### 🔥 Issue #5257 – Generalized ACP client for multi-agent CLI orchestration
**Comments: 11 | 👍: 16**
*User request:* Generalize the ACP client beyond Copilot-only support to orchestrate all ACP-compatible coding agents (Claude Code, Cline, Goose, OpenHands, aider).
**Underlying need:** Users want Hermes to act as an **orchestrator for a heterogeneous multi-agent environment**, not just a single-agent assistant. The reaction count (16 👍) indicates strong demand for Hermes as a "hub" for other coding agents.
[View Issue](https://github.com/NousResearch/hermes-agent/issues/5257)

### 🔥 Issue #6839 – Feature: Lazy Tool Schema Loading
**Comments: 26 | 👍: 14**
*Performance proposal:* Two-pass tool injection to reduce token overhead—only inject tool schemas for tools actually needed in the current conversation turn.
**Underlying need:** Token efficiency is the #1 community concern. With 50+ tools consuming 3,500-5,000 tokens per call even when unused (per the issue author), this is a **critical optimization for both cost and latency**, especially for local model users with limited context windows.
[View Issue](https://github.com/NousResearch/hermes-agent/issues/6839)

### 🔥 Issue #4379 – Token overhead analysis: 73% fixed overhead (~13.9K tokens)
**Comments: 15 | 👍: 0**
*Data-driven analysis:* User-built monitoring dashboard shows 73% of every API call is fixed overhead.
**Underlying need:** Empirical validation of the token waste problem, providing concrete metrics (~13.9K tokens per call of overhead) to justify the lazy loading proposals. Community want **measurable efficiency improvements**, not just theoretical optimizations.
[View Issue](https://github.com/NousResearch/hermes-agent/issues/4379)

### 🔥 Issue #43083 – Passwords replaced by `***` but model fails on second tool call
**Comments: 8 | 👍: 0**
*Priority P1 bug:* Defence-in-depth credential redaction causes model to fail when reading back its own conversation history due to redacted fields.
**Underlying need:** Users are hitting a **real security-vs-functionality tradeoff** where safety measures break operational workflows. Needs a decision on redaction approach that preserves both security and agent functionality.
[View Issue](https://github.com/NousResearch/hermes-agent/issues/43083)

---

## Bugs & Stability

### Critical (P1) Issues Reported/Updated Today

- **Issue #43083 – Password redaction breaks second tool call (P1, needs-decision)**
  Security mechanism (`***` replacement) prevents model from correctly re-parsing conversation history for follow-up tool calls. **Fix PR exists?** Not identified. Maintainer decision required on redaction strategy. [View Issue](https://github.com/NousResearch/hermes-agent/issues/43083)

- **Issue #48648 – Telegram infinite streamed message duplication loop on 4096-char overflow (P1)**
  Gateway enters infinite nested reply loop when streamed content exceeds Telegram's character limit. **Fix PR?** Not identified. Active investigation with 6 comments. [View Issue](https://github.com/NousResearch/hermes-agent/issues/48648)

- **Issue #19566 – OpenAI-Codex credential pool drops newly added credentials during rotation (P1, sweeper:risk-session-state, sweeper:risk-security-boundary)**
  Stale `auth.json` rewrite during credential rotation can silently drop recently added credentials. **Fix PR?** Not identified. Affects credential management reliability. [View Issue](https://github.com/NousResearch/hermes-agent/issues/19566)

- **Issue #47237 – Gateway persists duplicate user turns after transient provider failures (P1)**
  Telegram sessions get duplicate/stale user turns after provider/auth failures recover. **Fix PR?** Not identified. Causes agent to "fall behind" in conversation. [View Issue](https://github.com/NousResearch/hermes-agent/issues/47237)

- **Issue #51579 – `gateway run` auto-migration strips `$HERMES_HOME/.env` on every Docker container start (P1, regression of #26804)**
  Docker image rewrites config and strips `.env` on every startup, killing Telegram connectivity. **Fix PR?** Not identified. Critical regression for Docker users. [View Issue](https://github.com/NousResearch/hermes-agent/issues/51579)

- **Issue #51587 – MCP server tools never surface into agent's session toolset (P1, needs-repro)**
  Connected MCP servers fail to expose tools in WebUI/CLI sessions. **Fix PR?** Not identified. P1 because MCP integration is a major feature pillar. [View Issue](https://github.com/NousResearch/hermes-agent/issues/51587)

### High (P2) Issues Reported/Updated Today

- **Issue #38387 – Windows gateway leaves blank console window (P2, platform/windows)**
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/38387)
  *Fix progress:* PR #41028 and #49615 both address this Windows console issue.

- **Issue #28004 – Telegram typing indicator stuck indefinitely (P2)**
  Race condition in `_keep_typing` cleanup. [View Issue](https://github.com/NousResearch/hermes-agent/issues/28004)

- **Issue #50005 – Desktop non-functional on WebSocket disconnect (P2)**
  No offline mode or reconnection backoff. [View Issue](https://github.com/NousResearch/hermes-agent/issues/50005)

- **Issue #47368 – Desktop "Delete profile" silently fails (P2)**
  Profile reappears after app restart. [View Issue](https://github.com/NousResearch/hermes-agent/issues/47368)

- **Issue #25758 – `reasoning_effort: none` silently ignored on Ollama (P2)**
  Model thinks anyway, causing up to 65K tokens / 28 min on background fork. [View Issue](https://github.com/NousResearch/hermes-agent/issues/25758)

- **Issue #51560 – `fallback_providers` as JSON string silently empties fallback chain (P2)**
  Config set stores as string, parser silently drops it. [View Issue](https://github.com/NousResearch/hermes-agent/issues/51560)

- **Issue #51607 – Session billing fields don't reflect mid-session model switches (P2, area/billing)**
  Tokens from switched model attributed to initial model, skewing billing metrics. [View Issue](https://github.com/NousResearch/hermes-agent/issues/51607)

### Regressions Noted

- **Issue #51579** is flagged as a regression of **#26804**, indicating the Docker `.env` stripping issue has resurfaced.
- **Issue #38387** (Windows console window) has been addressed by multiple PRs (#41028, #49615) but the open status suggests the fix may not be complete or merged.

---

## Feature Requests & Roadmap Signals

### High-Community-Interest Features Likely for Next Release

1. **Generalized ACP Client (#5257, 16 👍)** – Orchestration of Claude Code, Cline, etc. via Hermes. Predict **next or subsequent release** given strong community support and already-existing Copilot ACP client as foundation.

2. **Lazy Tool Schema Loading (#6839, 14 👍)** – Two-pass tool injection for token efficiency. Predict **next release candidate** if maintainers prioritize performance improvements in response to community token overhead analysis (#4379).

3. **Vertex AI Provider for Gemini (#8427, open PR)** – Adds GCP enterprise access for Gemini models. PR has been open since April 12, but recent activity suggests it may be close to merge as a first-class provider.

4. **Semantic Session Search (#44093, open PR)** – Hybrid BM25 + sqlite-vec semantic search. Two competing PRs (#44093, #51125) indicate active development; likely **next or subsequent release** given the duplicate indicates maintainer interest.

5. **Ollama Cloud as Plugin-Based Web Search Provider (#22648, open PR)** – Extends web search capabilities for Ollama users. Long-running PR (since May 9) but recently rebased onto main.

### Emerging Feature Themes

- **Token Efficiency** – Multiple issues (#6839, #4379) and the URL-intent guard PR (#51621) all point to reducing token waste as a top priority.
- **Multi-Agent Orchestration** – ACP generalization (#5257) and the delegation toolset suggest Hermes is evolving from single-agent to orchestration platform.
- **Platform Parity** – Ongoing Windows (console windows, Scheduled Tasks) and Termux (uv source builds) fixes indicate effort to close platform gaps.
- **Gateway Resilience** – Multiple P1 Telegram/Email/Feishu bugs indicate gateway reliability is a continuing challenge, especially around streaming and reconnection.

---

## User Feedback Summary

### Common Pain Points

1. **Token Waste** – "73% of every API call is fixed overhead" (#4379) and "3,500-5,000 tokens per call regardless of need" (#6839) dominate performance concerns. Users are measuring, monitoring, and demanding optimization.

2. **Windows UX** – Blank console windows (#38387), non-surviving gateways (#45599), broken Scheduled Tasks, and missing type declarations (#38146) make Windows a second-class experience.

3. **Gateway Reliability** – Telegram infinite loops (#48648), stuck typing indicators (#28004), duplicate turns (#47237), and Docker `.env` stripping (#51579) erode trust in gateway operations.

4. **Security vs. Usability** – Password redaction breaking tool calls (#43083), non-shell tools bypassing Tirith approval gates (#35357), and silent fallback model identity (#51573) represent unresolved design tensions.

5. **Desktop App Fragility** – WebSocket disconnects freeze the app (#50005), profile deletion is non-functional (#47368), long prompts consume viewports (#39721), and stop buttons reference nonexistent commands (#51575, #51576).

### Satisfaction Signals

- High community engagement (16 👍 on #5257, 14 👍 on #6839) suggests users are invested enough to propose sophisticated features.
- Duplicate PRs for semantic search (#44093, #51125) and Termux uv fixes (#39152, #48626, #51601) indicate enthusiastic contribution even when coordination could be better.
- The user-built monitoring dashboard in #4379 demonstrates the kind of dedicated power-user community that builds tooling around Hermes.

---

## Backlog Watch

### Issues Requiring Maintainer Attention

- **Issue #6839 – Lazy Tool Schema Loading (P3, 26 comments, 14 👍)**
  High-engagement feature with significant impact. Needs maintainer decision on design approach and priority assignment. [View Issue](https://github.com/NousResearch/hermes-agent/issues/6839)

- **Issue #43083 – Password redaction breaks second tool call (P1, needs-decision)**
  Critical P1 bug tagged `needs-decision`. Security-vs-functionality tradeoff requires architectural decision. [View Issue](https://github.com/NousResearch/hermes-agent/issues/43083)

- **Issue #35357 – Tirith approval gate bypassed by non-shell tools (P3, security)**
  Human-in-the-loop bypass for `send_message`, `write_file`, `delete_resource`. Security concern flagged over 3 weeks ago with no fix PR identified. [View Issue](https://github.com/NousResearch/hermes-agent/issues/35357)

- **Issue #51587 – MCP tools never surface (P1, needs-repro)**
  Critical for MCP ecosystem adoption. Tagged `needs-repro`—maintainer reproduction and investigation needed. [View Issue](https://github.com/NousResearch/hermes-agent/issues/51587)

### Long-Standing Feature PRs

- **PR #8427 – Vertex AI provider for Gemini (open since April 12)**
  No comments from maintainers. Enterprise feature may need product decision. [View PR](https://github.com/NousResearch/hermes-agent/pull/8427)

- **PR #22648 – Ollama Cloud web search plugin (open since May 9)**
  Recently rebased but still unmerged. May need design review alignment. [View PR](https://github.com/NousResearch/hermes-agent/pull/22648)

### Unresolved Duplicates

- **PR #51125 vs. #44093** – Both implement semantic session search. #51125 was closed as duplicate, but #44093 remains open. Community confusion risk—clear direction would help contributors.

---

**Overall Project Health:** Green with caution flags. Development velocity is high with 8 PRs merged/closed today, and the community is actively contributing features, performance analyses, and comprehensive bug reports. Key risk areas are **(1) Windows platform experience**, **(2) gateway reliability under production loads** (especially Telegram), and **(3) security boundary hardening** for non-shell tools and credential management. The token efficiency conversation (#6839, #4379) may define the next major release's headline improvement.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-24

## Today's Overview
PicoClaw sees elevated maintenance activity today with **17 PRs updated** in 24 hours (6 merged/closed, 11 open) and **2 issues** (1 closed, 1 open/new). The project's velocity remains high, driven by security hardening, platform bug fixes (Android/Termux, Windows), and new feature integration (AWS Bedrock caching, Android ADB tooling). A stale bot closure marks long-idle issues being actively cleaned up, but the volume of open PRs signals significant engineering throughput. No new releases are cut today, though the accumulated fixes and features suggest a v0.3.0 may be approaching.

## Releases
No new releases were published in the last 24 hours.

## Project Progress
Six PRs were merged or closed today, spanning cross-cutting improvements:

- **Security & Authentication:** PR [#3160](https://github.com/sipeed/picoclaw/pull/3160) adds `Sec-Fetch-Site`, `Origin`, and `Referer` checks to reject cross-site launcher setup requests, hardening the first-run dashboard password store. PR [#3161](https://github.com/sipeed/picoclaw/pull/3161) fixes a critical security gap where custom allow rules for `exec` could bypass deny patterns entirely—any matched command previously skipped deny-pattern enforcement entirely, allowing e.g. `jq` to read environment variables. Deny patterns now remain active even after allow-rule matches.

- **Platform Stability:** PR [#3162](https://github.com/sipeed/picoclaw/pull/3162) adds exponential backoff reconnection, pong handling, and async goroutine message processing to the WhatsApp channel, fixing automatic WebSocket disconnection issues.

- **API Compatibility:** PR [#3154](https://github.com/sipeed/picoclaw/pull/3154) fixes a Doubao Seed model bug where tool calls leaked as raw `<seed:tool_call>` XML inside `message.content` (instead of using standard OpenAI `tool_calls`), restoring proper tool call extraction for Volcengine's model.

- **Housekeeping:** Two stale PRs—explicitly ignored `Close()` errors (PR [#3059](https://github.com/sipeed/picoclaw/pull/3059)) and unchecked `sync.Map` type assertions in LINE channel (PR [#3054](https://github.com/sipeed/picoclaw/pull/3054))—were closed. PR [#3047](https://github.com/sipeed/picoclaw/pull/3047) restored full JSONL history visibility in session detail without bloating list pagination.

## Community Hot Topics
The most active discussion in the past 24 hours centers on **Android/Termux stability**:

- **Issue #3164** ([link](https://github.com/sipeed/picoclaw/issues/3164)) — *"Process hooks crash gateway on Android/Termux (v0.2.9, config v3)"* — Zero comments but filed today, reporting that even a minimal "hello world" hook causes gateway death within 2 seconds on Android/Termux. This is the only open, unaddressed bug, suggesting the reporter may be waiting for acknowledgment.

The **closed issue #3015** ([link](https://github.com/sipeed/picoclaw/issues/3015)) had the most comments (4) in 24 hours but was closed as stale. It documents a Windows-specific QQ channel token retrieval timeout, with Pico channel working normally, indicating a platform-specific integration issue rather than a core gateway flaw.

## Bugs & Stability
**Critical severity:**
- **Issue #3164** — *Process hooks crash gateway on Android/Termux* — **No fix PR exists yet.** Gateway crashes within 2 seconds of startup when any hook is active. Given the gateway's role as the central process manager, this is the highest-priority active bug. The reporter used v0.2.9, commit 29. No maintainer response visible.

**High severity (fixed in flight):**
- **Issue #3015** (stale-closed) — QQ channel token retrieval timeout on Windows — Was symptomatic of broader Windows-specific network or DNS configuration issues. No reproduction fix was merged; closed via stale bot.

**Medium severity (fixed):**
- PR [#3154](https://github.com/sipeed/picoclaw/pull/3154) — Doubao Seed model leaking tool calls as raw XML in `message.content` — a data corruption bug for OpenAI-compatible API users, now merged.
- PR [#3160](https://github.com/sipeed/picoclaw/pull/3160) — Cross-site launcher setup hijacking — security regression now patched.
- PR [#3161](https://github.com/sipeed/picoclaw/pull/3161) — `exec` deny patterns bypassed by custom allow rules — security regression now patched.

## Feature Requests & Roadmap Signals
Several forward-looking PRs are open and active:

1. **AWS Bedrock prompt caching** (PR [#3163](https://github.com/sipeed/picoclaw/pull/3163)) — Adds `cachePoints` to Converse API calls, reducing input token costs to ~0.1× for cached prefixes. A clear cost-optimization feature likely to land soon given it's freshly filed by a regular contributor (loafoe).

2. **Remote Pico WebSocket mode** (PR [#3118](https://github.com/sipeed/picoclaw/pull/3118)) — Allows `picoclaw agent --remote ws://...` for remote agent operation, preserving local behavior. This extends the agent from local-only to a distributed architecture, a major capability step.

3. **Android ADB remote operations tool** (PR [#3157](https://github.com/sipeed/picoclaw/pull/3157)) — Adds experimental ADB-backed tool for device listing, screenshots, UI hierarchy, tap/swipe/text input. Explicitly does *not* expose arbitrary shell execution. May be bundled in v0.3.0 given the Android/Termux bug attention.

4. **Telegram reply-to-mention** (PR [#2975](https://github.com/sipeed/picoclaw/pull/2975), open since May 30) — Treats reply-to-bot as @mention in group chats.

**Prediction for next release:** AWS Bedrock caching (PR #3163), exec deny pattern fix (PR #3161), cross-site auth fix (PR #3160), and Doubao Seed tool call fix (PR #3154) are all merged and likely candidates. The ADB tool (PR #3157) and remote agent (PR #3118) may follow if testing completes.

## User Feedback Summary
**Pain points (reported today):**
- **Android/Termux is broken** for the use case of running hooks: users cannot run even trivial process hooks without gateway crash (Issue #3164). This impacts mobile/edge deployment.
- **QQ channel unreliable on Windows** (Issue #3015): token retrieval timeout persists, but no reproduction fix was provided before stale closure. The reporter confirmed Pico channel works, narrowing the issue to QQ integration.
- **WhatsApp disconnections** (PR #3162 fix): previously, automatic WebSocket drops required manual reconnects; now resolved.

**Satisfaction signals:**
- The Doubao Seed fix (PR #3154) was requested via Issue #3153 and resolved within 1 day, demonstrating responsive maintainer turnaround for API compatibility issues.

## Backlog Watch
**Items needing maintainer attention (unanswered >24h):**

1. **Issue #3164** ([link](https://github.com/sipeed/picoclaw/issues/3164)) — Android/Termux hook crash, filed today, no maintainer response. **Action needed: ack + triage prioritization.** Could be related to stdio handling on Termux's pseudo-terminal layer.

2. **PR #2975** ([link](https://github.com/sipeed/picoclaw/pull/2975)) — Telegram reply-to-mention feature, open since May 30, 2026 (25 days). No recent maintainer activity. Low risk of merge conflict but signals bottleneck on Telegram channel reviewer bandwidth.

3. **Three dependency bumps** (PRs [#3104](https://github.com/sipeed/picoclaw/pull/3104), [#3103](https://github.com/sipeed/picoclaw/pull/3103), [#3100](https://github.com/sipeed/picoclaw/pull/3100)) — shadcn, typescript-eslint, @vitejs/plugin-react — all open since June 11 (13 days). Dependency updates accumulate risk for security vulnerabilities; periodic batch merging recommended.

4. **PR #3115** ([link](https://github.com/sipeed/picoclaw/pull/3115)) — Fixes session-history corruption when tools return `data:image/...;base64,...` in plain text output. Open since June 12 (12 days). This is a data integrity bug affecting all users who run `read_file` or `exec` with output containing base64 image strings. **Merge priority: high.**

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for 2026-06-24.

---

## NanoClaw Project Digest: 2026-06-24

### 1. Today's Overview
**Status: Very High Activity**

NanoClaw saw a burst of engineering activity today, with **12 pull requests (PRs) updated** and **8 of those merged or closed**. The core focus was a coordinated, multi-branch dependency bump of the Chat SDK to version **4.29.0**, ensuring the `main`, `channels`, and `providers` branches remain synchronized. The most significant feature work involved landing **Slack Socket Mode** (allowing bot connections without a public HTTPS endpoint) and a **new "reject with reason" capability** for human-in-the-loop approval cards. Despite the high code volume, only **one new issue was opened**, suggesting the release velocity is currently outpacing user-reported bugs.

### 2. Releases
**None**
No new releases were cut today. The project appears to be in a high-velocity development phase, merging features into the main branch before tagging a new release.

### 3. Project Progress
**8 PRs were Merged/Closed today.**

- **Slack Socket Mode:** **[#2837 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2837)** adds a new adapter that allows Slack connections via an outbound WebSocket (using a `SLACK_APP_TOKEN`). This is a significant stability/security feature as it bypasses the need for a public-facing webhook, ideal for local development or users behind NAT. A follow-up chore **[#2839 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2839)** backported this feature into the `channels` branch.
- **Chat SDK 4.29.0 Bump:** A coordinated, multi-repository version bump was completed:
    - **[#2834 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2834)**: Updated the core `main` branch.
    - **[#2835 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2835)**: Updated the `channels` registry branch.
    - **[#2836 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2836)**: Updated the `providers` registry branch.
- **Approval Workflow Improvement:** **[#2832 (Open)](https://github.com/nanocoai/nanoclaw/pull/2832)** introduces a third "Reject with reason…" button for approval cards, allowing human reviewers to relay feedback to agents.
- **Extension-Point Seams:** **[#2841 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2841)** introduces a pattern (`registerX`/`applyX`) for generic extension points. This creates a framework for future plugins/customizations without changing existing behavior.
- **Update UX Fix:** **[#2826 (Merged)](https://github.com/nanocoai/nanoclaw/pull/2826)** fixes the `/update-nanoclaw` flow to prevent users from silently missing upstream fixes to installed skills, and ensures containers are rebuilt on re-apply.

### 4. Community Hot Topics
**Low Engagement.** The primary issue and the open PRs have zero comments and zero reactions, indicating the community is not actively discussing current development items.

- **Issue: Slack Port Collision** **[#2840 (Open)](https://github.com/nanocoai/nanoclaw/issues/2840)**
    - **Analysis:** This is the most potentially disruptive user-facing issue. The user reports that the standard Slack installation guide instructs users to create a secure tunnel to port 3000, but NanoClaw is already binding this port on the external IP. This breaks the security model and is a fundamental configuration/setup problem. This issue directly conflicts with the newly merged Slack Socket Mode (#2837), which was designed to eliminate this exact requirement. **It remains to be seen if the user’s problem is solved by the new Socket Mode, or if the webhook setup instructions still need fixing.**

### 5. Bugs & Stability
**Severity: Medium.** No crashes or regressions were reported.

- **[#2840 (Open)](https://github.com/nanocoai/nanoclaw/issues/2840)**: The Slack port binding issue is a **medium-severity configuration bug**. While not a crash, it invalidates the intended security of the tunnel setup for all users following the default Slack instructions. A fix may involve either updating the installation documentation or adjusting the default binding behavior, but the merge of Slack Socket Mode (PR #2837) offers an alternative that makes this issue obsolete for users who adopt the new mode.

### 6. Feature Requests & Roadmap Signals
- **Extension-Point Architecture (Merged):** PR [#2841](https://github.com/nanocoai/nanoclaw/pull/2841) is a roadmap signal towards a more modular and extensible NanoClaw. This likely paves the way for third-party plugins or complex custom behaviors without forking the core codebase.
- **"Reject with Reason" (Open):** PR [#2832](https://github.com/nanocoai/nanoclaw/pull/2832) is likely to be merged soon, signaling a focus on improving the human-agent feedback loop.
- **Manifest Model Router (Open):** PR [#2838](https://github.com/nanocoai/nanoclaw/pull/2838) is a feature skill that adds a new provider, suggesting continued expansion of model integration options.
- **Prediction for Next Version:** The next release will almost certainly contain the Slack Socket Mode as a headline feature, along with the upgraded Chat SDK and the improved approval rejection UX.

### 7. User Feedback Summary
**Data is very thin.** The only direct user pain point is the **Slack port collision** reported in Issue [#2840](https://github.com/nanocoai/nanoclaw/issues/2840). This highlights a gap between the security advice given to users and the actual default behavior of the application. The Project's heavy focus on the new Slack Socket Mode appears to be a direct response to this class of infrastructure friction (setting up tunnels, NAT, public IPs).

### 8. Backlog Watch
- **Agent Container Performance** **[#2771 (Open)](https://github.com/nanocoai/nanoclaw/pull/2771)** (Created 9 days ago): This PR proposes adding `--shm-size=1g` and `--init` flags to agent Docker containers to prevent Chromium crashes. This is a **tangible stability improvement for all users running agent browser capabilities**. While it has received a recent comment, it has not been merged. The longer it remains open, the more users may be experiencing silent browser failures.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-24

## 1. Today's Overview
Project activity is low today, with only one issue updated (closed) and one pull request updated (still open). No new releases were published. A bug affecting Windows users with the Agnes-2.0-Flash model was resolved, while a long-running feature PR (#783) for cron subagent and JSON output continues to attract updates. Overall, the project appears to be in a quiet maintenance phase, with community contributions slowly advancing feature work.

## 2. Releases
No new releases were published today. The latest available version remains **v2026.5.29** (released 2026-05-29). No migration notes or breaking changes to report.

## 3. Project Progress
- No pull requests were merged or closed today.
- **PR #783** (open, updated today) by **yanggf8** continues to progress: a large feature adding a cron subagent engine with DB-backed scheduler, run history, JSON CLI output, and security hardening. This PR has been open since April 7 and is actively receiving attention, suggesting significant new scheduling and automation capabilities may be incoming.

## 4. Community Hot Topics
- **Issue #967** [CLOSED] — [bug] error: NoResponseContent by **svier0** (2 comments)  
  [Link](https://github.com/nullclaw/nullclaw/issues/967)  
  *Analysis:* This was the most active issue, reporting a >50% failure rate on Windows (Win11) with the Agnes-2.0-Flash model. The error `NoResponseContent` occurred despite the same model+API key working in PicoCla. This suggests a platform-specific integration bug, possibly in HTTP response handling or model output parsing. The issue was closed today, indicating a fix has been applied.

- **PR #783** [OPEN] by **yanggf8** (0 comments, but updated today)  
  [Link](https://github.com/nullclaw/nullclaw/pull/783)  
  *Analysis:* Although comment count is missing in data, the PR's size and continued updates suggest high maintainer/contributor interest in cron scheduling, operator alerts, and structured JSON output. This feature is likely a priority for power users needing task automation.

## 5. Bugs & Stability
- **Issue #967** (CLOSED) — **Severity: High**  
  *Bug:* `NoResponseContent` error on Windows 11 with Agnes-2.0-Flash model, occurring in >50% of conversations (12 out of 21).  
  *Status:* Closed, so a fix was applied sometime between creation (2026-06-20) and today's update (2026-06-23). Users on Windows should update to the latest nightly/build to resolve. No related fix PR was visible in today's data, suggesting the fix may have been committed directly.

No other crashes, regressions, or new bugs were reported today.

## 6. Feature Requests & Roadmap Signals
- **PR #783** signals a clear roadmap direction toward **cron-based automation** (DB-backed scheduling, job types for skills/agents/shell commands), **operator alerting**, and **structured output** (JSON CLI). These features suggest NullClaw is evolving from a conversational agent into a programmable automation platform.
- The closing of Windows-specific bugs (Issue #967) suggests ongoing investment in **cross-platform reliability**, likely a prerequisite for broader enterprise adoption.

Predicted next-version inclusions: cron subagent with history, JSON output for CLI, security hardening (PR #783). No new feature requests in issues today.

## 7. User Feedback Summary
- **Pain point:** Windows users face inconsistent model response reliability (Issue #967). The error `NoResponseContent` with >50% occurrence is a major usability blocker.
- **Use case:** Users rely on NullClaw for interactive agent conversations (e.g., "你好！") and expect deterministic behavior across platforms.
- **Satisfaction:** The bug was fixed and acknowledged, which should improve user confidence. However, the high frequency of failure indicates a need for more robust error handling and platform-specific testing.
- **Dissatisfaction:** No direct negative feedback was left, but the severity of the bug (50%+ failure rate) likely frustrated affected users before the fix.

## 8. Backlog Watch
- **PR #783** (open since April 7, 2026) — **Needs attention**  
  Despite being updated today, this PR has been open for nearly 3 months with no comments or merge activity visible. It is a large feature that could benefit from maintainer review, especially given the extended development time. Risk of drift or conflict with main branch is increasing.

No long-unanswered issues were identified in today's data.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-24

## Today's Overview

IronClaw remains in a high-velocity development phase, with 42 pull requests updated and 21 issues active or closed in the last 24 hours. The project shows strong forward momentum on the **Reborn** architecture overhaul, with multiple large-feature PRs landing or nearing completion across automation management, Slack integration, Google credential handling, and skill-learning systems. A notable **19 PRs were merged or closed** today, while 23 remain open — indicating sustained, healthy review throughput. No new releases were cut, suggesting the team is consolidating toward a future milestone rather than shipping hotfixes. Activity is concentrated on core infrastructure work rather than end-user features, consistent with a platform still under heavy construction.

## Releases

No new releases were published today. The project is in an active development cycle without a versioned release.

## Project Progress

19 pull requests were merged or closed today, reflecting substantial progress across several key areas:

- **Reborn Automation Lifecycle**: Two foundational automation management PRs landed — `#5133` (Add Reborn automation delete support) and `#5121` (Add Reborn automation pause/resume support) — both by **italic-jinxin**. These wire the WebUI v2 API routes and trigger repository operations for delete and pause/resume flows.

- **Slack Integration Overhaul**: A coordinated set of Slack-related PRs closed today: `#5152` (move setup into WebUI), `#5164` (restore Slack routine outbound targets), `#5166` (wire dynamic Slack routine delivery), and `#4969` (fix Google WASM auth required errors). These represent a significant refactor of Slack from TOML-based configuration to WebUI-managed setup, with secrets stored in the Reborn secret store.

- **Google Auth Reliability**: PR `#4969` (merged) by **serrrfirat** addresses a critical bug where Google API 401 responses in bundled Drive/Docs/Sheets/Slides WASM tools were returning generic failures. The fix returns structured `auth_required` guest errors and adds host-runtime regression tests.

- **Skill-Learning Infrastructure**: PR `#5156` (open, large) lands the approval gate for freshly-learned skills, saving them as inactive and `pending_review` until human approval. This closes a safety gap from earlier work.

- **Memory System Refactor**: PR `#5163` (open, large) lifts the Reborn memory layer out of the kernel into provider-neutral contract and native provider crates, with `#5165` adding optional native memory seeding on the composition build path.

## Community Hot Topics

The most active discussions today centered on two persistent infrastructure themes:

- **Gmail/Google Auth UI Consistency** (`#3732`, `#3733`): Opened over a month ago by **sunglow666**, these long-standing bugs continue to receive attention. Issue `#3733` (Invalid Gmail token shows success/activated toast) and `#3732` (Inconsistent auth gate UI across conversations) highlight fundamental UX problems with Google OAuth integration. The underlying need is for a **single, reliable authentication pathway** that handles token validation, UI consistency, and error recovery — a prerequisite for Google extension reliability.

- **Bundled Skills Vocabulary Denylist** (`#5169`): Opened today by **zetyquickly**, this issue reports that bundled skill instructions containing ordinary API vocabulary ("Authorization", "Bearer", "access token") trip the prompt-safety denylist on clean setups, causing benign requests to fail with a misleading "temporary system issue." The user frustration is palpable — the system rejects valid, safe prompts and hides the real cause behind a vague error. This is a **high-severity UX regression** for users relying on first-party extensions.

## Bugs & Stability

| Severity | Issue | Summary | Fix Status |
|----------|-------|---------|------------|
| **Critical** | `#5148` | Scheduler heartbeat can self-deadlock while a run holds transition state, causing turns to get stuck forever | Open, no fix PR |
| **Critical** | `#5169` | Bundled skills trip prompt-safety denylist with benign API vocabulary → misleading "temporary system issue" | Open, no fix PR |
| **High** | `#5147` | Flaky test `trigger_poller_does_not_submit_turn_for_unpaired_actor` intermittently fails (~1 in 3), blocking merge queue | Open, blocks merges |
| **High** | `#4640` | Reborn google-calendar `list_events` returns oldest/unordered events with no timeMin or ordering defaults | Open, no fix PR |
| **Medium** | `#5157` | Inference section sometimes missing from Settings on Railway hosting | Open, tracked under #5119 |
| **Medium** | `#4991` | WASM google-drive auth failures dead-end as generic `operation_failed` without refresh-retry or AuthRequired gate | Closed with PR `#4969` (merged today) |
| **Low** | `#5146` | No button to deactivate an extension on Extensions page | Open, tracked under #5119 |

The **most concerning bugs** are `#5148` (self-deadlocking scheduler) and `#5169` (safety denylist false positives) — both can render the system unusable for affected workflows. The scheduler deadlock is particularly dangerous because it's silent and permanent for the affected turn. The flaky test `#5147` is a **blocker for the merge queue**, actively preventing PRs from landing.

## Feature Requests & Roadmap Signals

Several signals point toward what's coming next:

1. **Full Google Auth Recovery Pipeline**: With `#4969` merged for structured auth errors and `#5172` (Credential delete and reauth) open, the project is clearly building a comprehensive credential lifecycle for Google services. Expect `AuthRequired` gates, token refresh retries, and credential revocation in the next release.

2. **Context Efficiency via Progressive Tool Disclosure**: PR `#5149` (open, large by **serrrfirat**) proposes cutting per-call prompt size from ~25.8k tokens to a fraction by shipping only relevant tool schemas per turn. This directly addresses the NEAR AI timeout limit of 120s — a **critical performance bottleneck** in production.

3. **Memory as Userland Extension**: PR `#5163` and `#5165` (both open) refactor memory from a kernel component to a provider-neutral contract with native filesystem provider. This architectural shift enables third-party memory backends and more flexible memory seeding — likely part of a broader extensibility push.

4. **Skill-Learning Safety Gate**: PR `#5156` lands the approval gate for learned skills, requiring human review before untrained transcripts can become active automations. Expect this to ship soon given it's flagged as "residual risk" closing.

5. **GitHub API Fixes**: PRs `#5171` and `#5168` (both focused on correcting Reborn GitHub API request shapes) indicate the GitHub extension is being hardened for production use.

## User Feedback Summary

Real user pain points surfaced today include:

- **Critical UX Failure**: The prompt-safety denylist (`#5169`) rejects legitimate API vocabulary, misleading users into believing there's a transient system issue. This erodes trust and creates debugging nightmares for anyone using bundled Google skills.

- **Long-Standing Gmail Frustrations**: Issues `#3732` and `#3733` (open since May 17) describe deeply inconsistent OAuth experiences — invalid tokens showing success toasts, different auth UIs in different conversations, and repeated re-authorization loops. These bugs make Gmail integration feel unreliable and amateurish.

- **Calendar Data Quality**: Issue `#4640` (open since June 9) reports that "what are my upcoming meetings?" returns the *oldest* events without default date bounds or sorting. This is a clear failure of sensible defaults — users reasonably expect recency ordering.

- **Extension Management Gaps**: Issue `#5146` and the Settings Inference section issue (`#5157`) point to incomplete WebUI surfaces that force users to fall back to TOML editing or accept missing configuration.

- **Dogfooding Evidence**: Several issues tracked under `#5119` (dogfooding umbrella) show that even on Railway hosting, the team encounters missing settings sections and incomplete UI controls — indicating the WebUI v2 system is not yet production-ready for all deployment scenarios.

## Backlog Watch

| Issue | Age | Last Update | Priority Assessment |
|-------|-----|-------------|---------------------|
| `#3732` (Gmail auth UI inconsistency) | 38 days | 2026-06-23 | **High** — blocks Google extension reliability |
| `#3733` (Invalid Gmail token toast) | 38 days | 2026-06-23 | **High** — UX misleading to point of being dangerous |
| `#4640` (Calendar list_events ordering) | 15 days | 2026-06-23 | **Medium** — makes calendar effectively unusable for "upcoming" queries |
| `#4108` (Nightly E2E failure) | 28 days | 2026-06-23 | **Medium** — recurring nightly failure indicates systemic instability |
| `#5120` (Unify gate declined semantics) | 2 days | 2026-06-23 | **Low** — naming consistency issue, not user-facing |

The **Google authentication issues** (`#3732`, `#3733`) are the most critical backlog items — they've been open for over a month with minimal visible progress. Given that `#4991` (drive auth failures) was closed today with a structured error fix, there may be unblocked capacity to address these older UX issues. The **nightly E2E failure** (`#4108`) has been failing for 28 days without resolution, suggesting either test flakiness acceptance or a deeper infrastructure problem that isn't being prioritized.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-24

## Today's Overview
Project activity is **high**, with 11 pull requests updated in the last 24 hours, of which 5 were merged or closed. A single open issue remains active, flagged as stale. No new releases were published. The development velocity is strong, particularly around the OpenClaw gateway, scheduled-task stability, and cowork session management. However, a critical user-reported bug from early April remains unresolved, indicating a possible gap in issue triage.

## Releases
*None.* No new releases were published in the last 24 hours. The last stable release remains unknown from this data.

## Project Progress
The team merged or closed 5 PRs today, all authored or contributed by core developers:

- **[#2192] feat(cowork): add persistent plan confirmation flow** (merged) — Keeps Plan Mode active per draft/session until user confirms or disables execution. Adds "Confirm execution" and "Adjust plan" actions. Routes confirmed execution through default mode with restored skill/kit context. *(liuzhq1986)*
- **[#2191] fix(scheduled-task): clarify startup state** (merged) — Distinguishes startup, loading, ready, and error states in task/history tabs. Refreshes cron data immediately after OpenClaw gateway handshake instead of waiting for next polling interval. Documents one-shot task deletion behavior. *(btc69m979y-dotcom)*
- **[#2190] fix(openclaw): sync cron run sessions** (merged) — Recognizes OpenClaw run-scoped cron session keys (e.g., `agent:{agentId}:cron:{jobId}:run:{runId}`). Normalizes run-scoped keys to stable per-agent/per-job cache keys, allowing repeated runs to reuse one local Cowork session. Resolves scheduled-task conversation views through normalized cron keys. *(btc69m979y-dotcom)*
- **[#2189] fix(openclaw): migrate legacy cron storage on startup** (merged) — Detects legacy OpenClaw cron JSON/run-log storage before gateway startup. Runs the official OpenClaw doctor migration with minimal temporary cron config. Explicitly syncs `cron.store` and documents the upgrade migration design. *(btc69m979y-dotcom)*
- **[#2188] Liuzhq/rlog** (closed) — Branch/PR title only, no summary. Likely a cleanup or merge preparation by liuzhq1986.

One significant open PR was also introduced today:
- **[#2193] feat: add LiteLLM as AI gateway provider** (open) — Adds LiteLLM (litellm.ai) as an AI gateway provider, allowing users to point the base URL at a LiteLLM proxy to access 100+ LLM providers through a single OpenAI-compatible endpoint. No new dependencies—reuses existing `chatWithOpenAICompatible` handler. *(RheagalFire)*

## Community Hot Topics
- **[Issue #1400] "4.1版本严重bug，网关反复启动失败，反复重启，无限循环！"** (6 comments, created 2026-04-03, updated 2026-06-23) — **Most active issue.** User reports critical crash: upgrading from 3.30 to 4.1 causes infinite restart loop. Also reports misconfiguration conflict: custom LLM (qwen3.5-plus) cannot start due to "web-extractor cannot start without web-search" error, possibly conflicting with LobsterAI's auto-configured qwen3.5. User provided contact info. **No maintainer response visible in this digest.** [link](https://github.com/netease-youdao/LobsterAI/issues/1400)

- **[PR #2193] feat: add LiteLLM as AI gateway provider** (0 comments) — New feature PR, no discussion yet. Represents significant architectural expansion. [link](https://github.com/netease-youdao/LobsterAI/pull/2193)

## Bugs & Stability
**Severity: Critical**

- **[Issue #1400] 4.1版本严重bug，网关反复启动失败，反复重启，无限循环！** — **Critical severity.** Application fails to start after upgrading from 3.30 to 4.1. Repeated restart loops. Also, custom LLM (qwen3.5-plus) fails with "web-extractor cannot start without web-search" error, possibly due to conflict with built-in auto-configuration. **No fix PR exists.** This is a **production-blocking issue** that has been open since April 3, 2026 (82 days). User provided direct contact. This issue should be a top priority for maintainers.

**Severity: Moderate**

- **[PR #1401] fix: 请求安全性问题** (open, stale) — Fixes request ID predictability vulnerability. `Math.random()` is replaced with `crypto.randomUUID()` for cryptographically secure SSE stream request IDs. Protects against potential data stream subscription attacks. *(liulingfeng)* — Open since April 3, not yet merged.

- **[PR #1402] fix(cowork): keep all files from multi-select attachment picker** (open, stale) — Multi-file selection in one dialog only showed the last file due to `addAttachment` closing over the same `attachments` array. *(kayo5994)* — Open since April 3.

- **[PR #1403] fix(i18n): add delete translation key** (open, stale) — `i18nService.t('delete')` returns key string "delete" in Chinese UI due to missing translation entry. *(kayo5994)* — Open since April 3.

## Feature Requests & Roadmap Signals
- **[PR #2193] LiteLLM AI gateway provider** — Strong candidate for next release. Adds flexibility to use 100+ LLM providers through one OpenAI-compatible endpoint. No new dependencies. Likely approved soon.
- **[PR #2192] Persistent plan confirmation flow** — Just merged. Expected in next release. Enhances cowork session UX with persistent Plan Mode and execution confirmation.
- **[PR #1404] Scheduled tasks time picker UI optimization** (open, stale) — User requests improvement to time picker and dropdown styling in scheduled task creation. Native HTML inputs don't match app theme in Electron. Community-driven UX request.
- **[Issue #1329-related, PR #1406] Fallback notify channel list when IM filter is empty** (open, stale) — Fixes empty dropdown issue in scheduled task notification channel list. Community-identified edge case.

## User Feedback Summary
- **Significant dissatisfaction:** Issue #1400 user reports complete application crash after upgrade, with no apparent resolution path. User provided email and WeChat contact, suggesting urgent need for personal support. This represents a **trust-eroding experience** for upgrading users.
- **Functional gaps:** Users are encountering configuration conflicts between custom LLM providers and LobsterAI's auto-detected defaults. The "web-extractor cannot start without web-search" error suggests unresolved dependency chain in gateway initialization.
- **Positive signal:** The volume of merged PRs and new feature work (LiteLLM, Plan Mode) suggests active development addressing both infrastructure and UX concerns.

## Backlog Watch
**Attention Required — No Maintainer Response**

- **[Issue #1400] 4.1版本严重bug** — **Critical.** Open since April 3, 2026. 6 comments. User provided direct contact. No maintainer reply visible. Application-crashing bug. **Should be escalated.** [link](https://github.com/netease-youdao/LobsterAI/issues/1400)

- **[PR #1401] fix: 请求安全性问题** — **High importance.** Open since April 3, 2026. Fixes security vulnerability (predictable request IDs). No merge activity. *(liulingfeng)* [link](https://github.com/netease-youdao/LobsterAI/pull/1401)

- **[PR #1402] fix(cowork): keep all files from multi-select attachment picker** — Open since April 3, 2026. Community-submitted fix for multi-file attachment bug. *(kayo5994)* [link](https://github.com/netease-youdao/LobsterAI/pull/1402)

- **[PR #1403] fix(i18n): add delete translation key** — Open since April 3, 2026. Simple translation fix for Chinese UI. *(kayo5994)* [link](https://github.com/netease-youdao/LobsterAI/pull/1403)

- **[PR #1404] feat(scheduledTasks): 定时任务创建界面时间控件优化** — Open since April 3, 2026. UX improvement for time picker and dropdown styling. *(flowell)* [link](https://github.com/netease-youdao/LobsterAI/pull/1404)

- **[PR #1406] fix(scheduled-task): fallback notify channel list when IM filter is empty** — Open since April 3, 2026. Simple fallback logic fix. *(kayo5994)* [link](https://github.com/netease-youdao/LobsterAI/pull/1406)

*Note: All stale items share the same creation date (2026-04-03), suggesting a bulk submission or triage bottleneck on that date. These may have been overlooked during subsequent development sprints.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-24

## 1. Today's Overview
Moltis experienced a quiet development day, with no new issues opened or modified in the last 24 hours. One pull request (#215) was closed/merged, representing the only activity on the repository. No new releases were published. The overall project pulse is low, consistent with a mature feature set or a period of lower contributor activity.

## 2. Releases
None. No releases were published in the last 24 hours.

## 3. Project Progress
One pull request was merged today:

- **#215 feat(tools): add send_image tool for channel image delivery** ([PR link](https://github.com/moltis-org/moltis/pull/215))
  - **Author:** maximilize | **Created:** 2026-02-23 | **Merged:** 2026-06-23
  - **What advanced:** A new `send_image` tool was added to the skills toolkit, enabling skills to send local image files (PNG, JPEG, GIF, WebP) to channel targets such as Telegram. The implementation reuses the existing screenshot pipeline and returns a `data:` URI in the `screenshot` key, which the chat runner automatically picks up. Optional `caption` parameter support was also included.
  - **Impact:** This closes a notable gap in Moltis's tool ecosystem, allowing direct image sharing from skills without requiring manual file uploads or external integrations.

## 4. Community Hot Topics
No issues or PRs had significant comment or reaction activity in the last 24 hours. The sole PR (#215) was merged with zero comments and zero reactions, suggesting it was uncontroversial and received minimal community engagement during final review.

## 5. Bugs & Stability
No bugs, crashes, or regressions were reported in the last 24 hours. The project shows no new stability concerns.

## 6. Feature Requests & Roadmap Signals
No new feature requests were submitted today. The merged `send_image` tool (#215) had been open for approximately four months, indicating that image delivery to channels was a long-standing desired capability. This suggests the development team may be systematically addressing gaps in the tool API. The reuse of the existing screenshot pipeline hints at an architectural principle of building on stable foundations rather than introducing new dependencies.

## 7. User Feedback Summary
No direct user feedback, pain points, or use case descriptions were recorded in the last 24 hours. The absence of any open issues or discussions suggests either high user satisfaction with the current state or low active usage of the project's issue tracker.

## 8. Backlog Watch
No long-unanswered issues or PRs requiring maintainer attention were identified in the last 24 hours. The repository currently has zero open issues and zero open pull requests, indicating the maintainers have fully cleared the backlog. This is a strong signal of project health and maintainer responsiveness.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — June 24, 2026

## Today's Overview
CoPaw (QwenPaw) continues as a highly active open-source personal AI assistant project, with **38 issues** and **50 PRs** updated in the last 24 hours. A new patch release **v1.1.12.post2** was published today, primarily fixing a chat session navigation bug and enhancing file preview functionality. Project maintainers have been clearing a substantial backlog of older PRs (28 merged/closed today vs. 22 still open), many dating back to May, suggesting a focused cleanup effort. The community is both productive and vocal, with pressing stability concerns around cron scheduling, agent thinking deadlocks, and memory usage beginning to surface as recurring themes.

## Releases
- **[v1.1.12.post2](https://github.com/agentscope-ai/QwenPaw/releases/tag/v1.1.12.post2)** — Patch release containing:
  - **fix:** Navigate to new chat after deleting the current session (@zhaozhuang521, [#5376](https://github.com/agentscope-ai/QwenPaw/pull/5376))
  - **feat(console, chat):** Enhance file preview to support relative paths (@zhijianma, [#5377](https://github.com/agentscope-ai/QwenPaw/pull/5377))
  - **fix(q…** — additional fix (truncated in changelog)

**Migration notes:** No breaking changes; this is a direct upgrade from v1.1.12.post1.

## Project Progress
Today saw **28 PRs merged/closed**, representing substantial project advancement:
- **Session/Cron fixes:** Merged [#4303](https://github.com/agentscope-ai/QwenPaw/pull/4303) (isolating non-shared cron runs), [#4304](https://github.com/agentscope-ai/QwenPaw/pull/4304) (serializing shared-session cron jobs), and [#4331](https://github.com/agentscope-ai/QwenPaw/pull/4331) (injecting request context into shell subprocesses).
- **Console improvements:** Merged [#4345](https://github.com/agentscope-ai/QwenPaw/pull/4345) (collapsible code blocks for long output), [#4326](https://github.com/agentscope-ai/QwenPaw/pull/4326) (markdown rendering in user messages), [#4297](https://github.com/agentscope-ai/QwenPaw/pull/4297) (hide built-in chat drawer toggle).
- **API pagination:** Two new merged features — [#4336](https://github.com/agentscope-ai/QwenPaw/pull/4336) (paginate chat history) and [#4338](https://github.com/agentscope-ai/QwenPaw/pull/4338) (paginate chat list).
- **Provider fixes:** [#4296](https://github.com/agentscope-ai/QwenPaw/pull/4296) (annotate extra models), [#4293](https://github.com/agentscope-ai/QwenPaw/pull/4293) (normalize reasoning content for OpenAI-compatible streams).
- **File handling:** [#4357](https://github.com/agentscope-ai/QwenPaw/pull/4357) (reject raw reads of Excel/binary spreadsheets).
- **Plugin system:** [#4327](https://github.com/agentscope-ai/QwenPaw/pull/4327) (add session lifecycle hooks for plugins).

**New open PRs** under active review include mobile responsive UI work for Skill Pool ([#5368](https://github.com/agentscope-ai/QwenPaw/pull/5368)) and Plugin Manager ([#5394](https://github.com/agentscope-ai/QwenPaw/pull/5394)), plus the critical Windows `ProactorEventLoop` fix ([#5417](https://github.com/agentscope-ai/QwenPaw/pull/5417)).

## Community Hot Topics

**Most active issues by comment count:**

1. **[#5262 — Bug: Disabled built-in skills re-enable after upgrade](https://github.com/agentscope-ai/QwenPaw/issues/5262)** (12 comments)
   - *Author:* daigoopautoy — Persistent bug across versions (1.1.9→1.1.10→1.1.11). User manually disables `docx`, `xlsx` skills after each upgrade but they revert. This is a known regression from an earlier issue [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807). **Community sentiment:** High frustration — the workaround (manual re-disabling) is tiresome. **Underlying need:** Config persistence across upgrades.

2. **[#5064 — Bug: Agent-created cron tasks fail to trigger](https://github.com/agentscope-ai/QwenPaw/issues/5064)** (12 comments, CLOSED)
   - *Author:* tina0501853 — Agent successfully creates tasks, but they never fire at the scheduled time. Also cannot be manually edited. **Resolution:** Likely fixed by today's merged cron fixes ([#4303](https://github.com/agentscope-ai/QwenPaw/pull/4303), [#4304](https://github.com/agentscope-ai/QwenPaw/pull/4304)). Community waited ~2 weeks for this fix.

3. **[#5345 — Custom OpenAI-compatible providers don't support function calling](https://github.com/agentscope-ai/QwenPaw/issues/5345)** (6 comments)
   - *Author:* qiyuanlicn — OMLX provider (OpenAI-compatible) fails to invoke tool calls despite working in other tools. User has verified API compatibility. **Underlying need:** Better provider abstraction layer — many users want to BYO models.

4. **[#5317 — Tauri/Windows: Python environment lost after upgrade](https://github.com/agentscope-ai/QwenPaw/issues/5317)** (6 comments)
   - *Author:* HQ1363 — Conda-built Python disappears after updates, breaking custom skills. **Underlying need:** Environment isolation/persistence for skill execution.

**Notable PR discussion:** [#5368](https://github.com/agentscope-ai/QwenPaw/pull/5368) (mobile Skill Pool layout) references the broader mobile responsiveness issue [#4635](https://github.com/agentscope-ai/QwenPaw/issues/4635) — a long-standing request with 3 comments.

## Bugs & Stability

### High Severity

| Issue | Description | Status | Fix in Progress? |
|-------|-------------|--------|------------------|
| [#5456](https://github.com/agentscope-ai/QwenPaw/issues/5456) | Wrong agent identity (`default` instead of active) for channel-built requests in v2.0.0b1 | OPEN (1 day old) | N/A — root cause identified |
| [#5416](https://github.com/agentscope-ai/QwenPaw/issues/5416) | `thinking`/`reasoning_content` responses with empty `content` — users see blank messages | OPEN (1 day old) | Related fix merged ([#4293](https://github.com/agentscope-ai/QwenPaw/pull/4293)) |
| [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) | `Internal Server Error` on Windows — `get_remote_addr` crash on Python 3.12+ | OPEN (1 day old) | **Yes** — PR [#5417](https://github.com/agentscope-ai/QwenPaw/pull/5417) |
| [#5328](https://github.com/agentscope-ai/QwenPaw/issues/5328) | DeepSeek agent freezes during thinking — requires manual stop+continue | OPEN (4 days old) | Not yet |
| [#5398](https://github.com/agentscope-ai/QwenPaw/issues/5398) | Cron scheduler stops dispatching while app stays alive (v1.1.12.post1) | **CLOSED** (fixed) | Fixed via [#4303](https://github.com/agentscope-ai/QwenPaw/pull/4303) |
| [#5402](https://github.com/agentscope-ai/QwenPaw/issues/5402) | Dream task execution failed for all 3 agents (v1.1.12.post1) | **CLOSED** (fixed) | Likely same root cause |

### Medium Severity

| Issue | Description | Status |
|-------|-------------|--------|
| [#5403](https://github.com/agentscope-ai/QwenPaw/issues/5403) | Browser autofill hijacks "Search providers" input (confuses with credential field) | OPEN (1 day old) |
| [#5373](https://github.com/agentscope-ai/QwenPaw/issues/5373) | Shell command execution fails on special characters (pipes, redirection, `>` `2>&1`) | OPEN (1 day old) |
| [#5378](https://github.com/agentscope-ai/QwenPaw/issues/5378) | Custom model endpoint auto-written into search box, making page unusable | OPEN (1 day old) |
| [#5401](https://github.com/agentscope-ai/QwenPaw/issues/5401) | Console frontend crashes on sessions with heavy tool-use history (`type: "data"` blocks) | OPEN (1 day old) |
| [#5421](https://github.com/agentscope-ai/QwenPaw/issues/5421) | Severe lag switching between agents/chat windows | OPEN (1 day old) |

### Low Severity

| Issue | Description | Status |
|-------|-------------|--------|
| [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) | TeamChat plugin fails on Python 3.13 (`No module named 'imghdr'`) | OPEN (11 days old) |
| [#5295](https://github.com/agentscope-ai/QwenPaw/issues/5295) | Subagent approval requests not pushed to external (QQ) channel | OPEN (5 days old) |

**Notable stability concern:** The memory occupation issue ([#5441](https://github.com/agentscope-ai/QwenPaw/issues/5441), [#5439](https://github.com/agentscope-ai/QwenPaw/issues/5439)) — user reports **1.4 GB RAM** immediately on startup with no workload. This is the second user reporting the same issue in consecutive issues, indicating a systemic memory leak or initialization overhead problem that could affect adoption, particularly on lower-end hardware.

## Feature Requests & Roadmap Signals

### Strongly Supported / Likely for Next Version

- **Mobile responsiveness** ([#5368](https://github.com/agentscope-ai/QwenPaw/pull/5368), [#5394](https://github.com/agentscope-ai/QwenPaw/pull/5394)) — Two PRs under review for mobile-friendly Plugin Manager and Skill Pool. Referenced from long-standing issue [#4635](https://github.com/agentscope-ai/QwenPaw/issues/4635). **Probability: High** — moving to review indicates maintainer buy-in.

- **Recency-aware memory search** ([#5316](https://github.com/agentscope-ai/QwenPaw/issues/5316)) — User requests that daily notes with similar relevance rank recent entries higher. **Probability: Medium** — no PR yet but well-defined scope.

- **KaTeX/LaTeX rendering** ([#5453](https://github.com/agentscope-ai/QwenPaw/issues/5453)) — User requests formula rendering in desktop app. **Probability: Low-Medium** — only 1 comment, but a common expectation for technical users.

### Longer-Term Signals

- **Memory management overhaul** ([#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995), open since May 1) — Comprehensive request for memory lifecycle (auto-archive), conflict detection on writes, configurable retention. **Probability: Medium** — actively commented (3 comments), but no concrete PR.

- **Stabilize core before new features** ([#5360](https://github.com/agentscope-ai/QwenPaw/issues/5360)) — User explicitly asks to fix mobile responsiveness, agent interaction reliability, and general stability before adding new features. This community sentiment is echoed in the memory/RAM complaints.

- **Kimi K2 Coding Plan support** ([#5427](https://github.com/agentscope-ai/QwenPaw/issues/5427)) — User needs Anthropic-compatible provider support (Kimi uses a different endpoint format than OpenAI). **Probability: Medium** — niche use case but growing provider ecosystem.

## User Feedback Summary

**What works well:**
- Cron/automation capabilities are valued — despite recent bugs, users actively create Dream Tasks and scheduled jobs.
- The skill ecosystem (despite upgrade persistence issues) is a core differentiator.
- Matrix E2EE support is being actively improved ([#5059](https://github.com/agentscope-ai/QwenPaw/pull/5059)).

**Pain points (frequency-coded):**
- **Recurring:** "Disabled skills re-enable after every upgrade" — appears in two separate issues months apart ([#5262](https://github.com/agentscope-ai/QwenPaw/issues/5262), [#4807](https://github.com/agentscope-ai/QwenPaw/issues/4807)); users are frustrated by the lack of finality.
- **Critical:** Agent thinking deadlocks (DeepSeek) — one user reports this across *all* interfaces (web, console, Tauri); severe to usability.
- **Systemic:** High memory usage (1.4 GB at idle) reported by at least two users in separate issues ([#5441](https://github.com/agentscope-ai/QwenPaw/issues/5441), [#5439](https://github.com/agentscope-ai/QwenPaw/issues/5439)).
- **Provider friction:** Custom OpenAI-compatible providers don't work for tool calling; agent thinking content is lost for reasoning models.
- **Windows-specific:** Internal Server Error on Python 3.12+ ([#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379)) and Python path issues in Tauri ([#5317](https://github.com/agentscope-ai/QwenPaw/issues/5317)).
- **Mobile:** Still not usable on phones despite being a top-voted issue since May.

**Satisfaction signals:**
- Community is **contributing actively** — multiple first-time PRs for bug fixes (Windows `ProactorEventLoop`, Matrix encrypted media).
- Users who report bugs also suggest concrete fixes (e.g., [#5379](https://github.com/agentscope-ai/QwenPaw/issues/5379) included logs attached, [#5456](https://github.com/agentscope-ai/QwenPaw/issues/5456) identified root cause).
- The frontend testing PRs ([#5437](https://github.com/agentscope-ai/QwenPaw/issues/5437), [#5433](https://github.com/agentscope-ai/QwenPaw/issues/5433)) indicate active investment in code quality.

## Backlog Watch

| Item | Age | Why It Needs Attention |
|------|-----|----------------------|
| [#3995](https://github.com/agentscope-ai/QwenPaw/issues/3995) — Memory management enhancement | 54 days (since May 1) | Core feature request affecting daily usability; lacks maintainer response. |
| [#4635](https://github.com/agentscope-ai/QwenPaw/issues/4635) — Mobile-friendly client | 33 days (since May 22) | Popular feature request; mobile PRs are under review but the parent issue is closed prematurely (resolution unknown). |
| [#5166](https://github.com/agentscope-ai/QwenPaw/issues/5166) — Python 3.13 incompatibility | 11 days (since June 12) | Blocks users on the latest Python — `imghdr` was removed in 3.13. No workaround documented. |
| [#5059](https://github.com/agentscope-ai/QwenPaw/pull/5059) — Matrix encrypted media fix | 15 days (since June 9) | Important for E2EE users; still under review with no maintainer merge despite passing checks. |

**Notable gap:** Several May PRs were merged today in a batch — this suggests maintainers have been focusing on clearing accumulated technical debt. However, the mobile responsiveness issue and memory management feature remain untouched despite being high-request items.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for 2026-06-24, generated from the provided GitHub data.

---

### ZeroClaw Project Digest: 2026-06-24

#### 1. Today's Overview
Project activity is very high, with 39 issues and 50 PRs updated in the last 24 hours. The core development team (e.g., `Audacity88`, `singlerider`, `JordanTheJet`) is heavily focused on security hardening and architectural improvements, particularly around WASM plugins and supply chain integrity. A significant cluster of activity revolves around implementing RFCs for gateways, channels, and security policies, signaling a mature push toward a v0.9.0 release. While no new releases were published today, the volume of merged PRs and closed issues indicates rapid internal iteration.

#### 2. Releases
- **New Releases:** None

#### 3. Project Progress (Merged/Closed PRs Today)
Today, **5 PRs** were merged or closed out of 50 updated. Key advances include:
- **Gateway/Web Dashboard:** PR [#8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173) turns the version tag in the web dashboard into a full in-app upgrade with auto-restart, implementing RFC [#8170](https://github.com/zeroclaw-labs/zeroclaw/issues/8170).
- **Channels:** PR [#8145](https://github.com/zeroclaw-labs/zeroclaw/issues/8145) moved the "ack" reaction earlier in the response cycle and added explicit typing stubs for 19+ channels, improving perceived responsiveness (linked to task [#8142](https://github.com/zeroclaw-labs/zeroclaw/issues/8142)).
- **Matrix Channel:** Issue [#7769](https://github.com/zeroclaw-labs/zeroclaw/issues/7769) was closed, confirming that recovered Matrix room-management APIs have been successfully wired to a caller.
- **CI/Release Pipeline:** RFC [#8058](https://github.com/zeroclaw-labs/zeroclaw/issues/8058) was accepted, covering cosign signing, SLSA provenance, and SBOM publication for release tags.

#### 4. Community Hot Topics
- **Supply Chain Security (RFC #8177):** With 4 comments, this RFC on hardware PGP, hermetic builds, and SLSA provenance is the most discussed open issue. It signals strong community interest in hardened release engineering.
    - [Issue #8177](https://github.com/zeroclaw-labs/zeroclaw/issues/8177) *Needs Maintainer Review*
- **Plugin Environment Variable Lockdown (Issue #5919):** This high-risk security issue, now *closed*, shows the community's sensitivity to plugin permissions. The `zc_env_read` function was restricted to an allowlist, preventing plugins from reading arbitrary environment variables.
    - [Issue #5919](https://github.com/zeroclaw-labs/zeroclaw/issues/5919)
- **Self-Signed Certificates (Issue #551):** A user request to allow insecure HTTPS requests to OpenAI-compatible endpoints, closed as `wontfix`, sparked a discussion about security posture vs. flexibility. This highlights a pain point for users with custom infrastructure.
    - [Issue #551](https://github.com/zeroclaw-labs/zeroclaw/issues/551)

#### 5. Bugs & Stability
- **High Severity (S1 - Workflow Blocked):**
    - **[Bug #8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193) (CLOSED):** MCP tools were missing from TUI sessions while visible to the gateway. A fix was confirmed, resolving a blocker for users of MCP server integrations.
    - **[Bug #8151](https://github.com/zeroclaw-labs/zeroclaw/issues/8151) (OPEN):** Deferred image attachments lose their re-loadable reference in cached history. A fix is in progress via PR [#8153](https://github.com/zeroclaw-labs/zeroclaw/pull/8153).
- **Medium Severity (S2 - Degraded Behavior):**
    - **[Bug #8236](https://github.com/zeroclaw-labs/zeroclaw/issues/8236) (OPEN):** A missing `subject` field in `voice_wake.rs` breaks `--all-features` builds. This is a low-risk compile-time regression.
    - **[Bug #7800](https://github.com/zeroclaw-labs/zeroclaw/issues/7800) (OPEN):** Misleading or unreachable keybindings in ZeroCode, particularly on macOS, continue to degrade the user experience for TUI users.

#### 6. Feature Requests & Roadmap Signals
Strong candidates for the next version (likely v0.9.0) emerge from the active RFCs and PRs:
- **Gateways/Upgrades:** The in-app upgrade feature (RFC [#8170](https://github.com/zeroclaw-labs/zeroclaw/issues/8170)) is already implemented in PR [#8173](https://github.com/zeroclaw-labs/zeroclaw/pull/8173). **Prediction:** Included in next release.
- **Security/Plugins:** Capability-gated WASI hardware access (RFC [#8187](https://github.com/zeroclaw-labs/zeroclaw/issues/8187)) and enforced plugin signature policies (PR [#8172](https://github.com/zeroclaw-labs/zeroclaw/pull/8172)) are being reviewed. **Prediction:** Likely for v0.9.0.
- **Channels:** Streaming message support for DingTalk (Issue [#8228](https://github.com/zeroclaw-labs/zeroclaw/issues/8228)) and QQ/WeChat (Issue [#7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531), closed) are moving forward. **Prediction:** These will improve the user experience on Chinese messaging platforms in the next release.
- **Config/Runtime:** Per-agent environment variables (Issue [#8226](https://github.com/zeroclaw-labs/zeroclaw/issues/8226)) and an independent delegate mode for specialists (Issue [#8238](https://github.com/zeroclaw-labs/zeroclaw/issues/8238)) are in active discussion, indicating a push for more granular and flexible agent configuration.

#### 7. User Feedback Summary
- **Pain Points:**
    - **Configuration Friction:** Users find the ZeroCode config editor misleading (Issue [#7814](https://github.com/zeroclaw-labs/zeroclaw/issues/7814)), as it appears editable before pressing Enter.
    - **Out-of-the-Box Experience:** Users report a "bad experience" with restrictive default risk profiles during quickstart (Issue [#8125](https://github.com/zeroclaw-labs/zeroclaw/issues/8125)), leading to a proposed "yolo" default.
    - **Response Time Anxiety:** The perceived silence while waiting for agents to respond is a significant pain point across all channels (Issue [#8142](https://github.com/zeroclaw-labs/zeroclaw/issues/8142)), driving the work on early ack reactions.
- **Satisfaction Signals:**
    - The community is actively contributing to high-level architectural RFCs (supply chain, hardware, WASM), suggesting a high degree of trust and engagement from advanced users and enterprise contributors.

#### 8. Backlog Watch
- **RFC: Unify Slash-Command Registries ([#7929](https://github.com/zeroclaw-labs/zeroclaw/issues/7929)):** This accepted RFC has 2 comments and is `needs-maintainer-review`. It proposes a significant architectural change to unify slash commands across web, TUI, and channels. It has not yet been discussed for implementation.
- **Audit: Track Lost Commits ([#6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)):** This important housekeeping task to recover 153 commits lost in a bulk revert has been open since April and is marked `in-progress`. It remains a silent blocker for some unreleased features.
- **Bug: System Prompt Tool-Availability Mismatch ([#8054](https://github.com/zeroclaw-labs/zeroclaw/issues/8054)):** This P1, `status:blocked` bug highlights that the fix for the runtime agent path needs to be replicated across all entry points (WebSocket, multimodel, etc.). It requires a meta-architectural fix beyond the initial patch.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*