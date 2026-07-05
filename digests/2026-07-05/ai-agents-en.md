# OpenClaw Ecosystem Digest 2026-07-05

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-05 01:46 UTC

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

Here is the OpenClaw project digest for July 5, 2026.

---

## OpenClaw Project Digest — 2026-07-05

### 1. Today's Overview
The OpenClaw project continues at an extremely high velocity, with **500 Issues updated and 500 PRs updated in the last 24 hours**. The 453 open/active issues and 349 open PRs indicate a massive, engaged community. Despite the high volume, no new releases are recorded for today. The focus remains on stabilizing the core agent orchestration and gateway reliability, with critical bugs around silent failures and session management dominating the conversation. The "ClawSweeper" backlog management system appears heavily utilized, but a significant number of issues are stuck awaiting maintainer review or product decisions.

### 2. Releases
- **Latest Releases:** None.

### 3. Project Progress
While specific merged/closed counts are high (47 Issues, 151 PRs), the data shows progress in several key areas:
- **Bug Fixes (Critical):** Several P0/P1 fixes are moving through the pipeline.
    - **PR #100104** (fix: suggest auth check for bundled provider model-not-found errors) addresses a critical startup brickwall for users with legacy API aliases.
    - **PR #100134** (fix(node-host): use truncateUtf16Safe in truncateOutput to avoid splitting surrogate pairs) fixes a potential data corruption issue.
    - **PR #100088** (fix(ui): chat workspace panel leaves an empty gap when collapsed) ships a UI polish fix.
- **Feature Advancement:** The large refactors continue to progress.
    - **PR #99059** (refactor: extract reusable AI runtime package) is a major architectural change to modularize model protocol adapters.
    - **PR #93313** (refactor(codex): simplify app-server runtime ownership) continues a complex Codex integration refactor.

### 4. Community Hot Topics
- **Critical Session Reliability:** The top three most active issues all relate to agents losing state or failing silently.
    - [#44925 - Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925) (20 comments): The community is deeply frustrated with agents that timeout or fail without any notification or retry.
    - [#48788 - Centralized filename encoding](https://github.com/openclaw/openclaw/issues/48788) (18 comments): Users are advocating for a robust, architectural solution to handle diverse filename encodings across channels, rather than piecemeal fixes.
    - [#22676 - Signal daemon stop() race condition](https://github.com/openclaw/openclaw/issues/22676) (17 comments): This long-standing issue resurfaces as a major pain point for gateway operators, leading to orphaned processes.
- **Security & Policy:** High interest in hardening the agent.
    - [#13583 - Pre-response enforcement hooks](https://github.com/openclaw/openclaw/issues/13583) (12 comments, 2 👍): The demand for "hard gates" against LLM disobedience in high-stakes use cases is clear.
    - [#7722 - Filesystem Sandboxing Config](https://github.com/openclaw/openclaw/issues/7722) (9 comments, 4 👍): This long-standing feature request continues to attract support for better access control.

### 5. Bugs & Stability
- **Priority P0 / Crashing:**
    - [#99414 (likely #99594) - Cloud instance "out of credits" with $109 balance](https://github.com/openclaw/openclaw/issues/99594): A severe billing/access bug affecting cloud users. This is a major trust and reliability issue.
    - [#54155 - Gateway memory leak: 389MB → 14.7GB over 4 days](https://github.com/openclaw/openclaw/issues/54155): A critical resource leak that will cause failovers or crashes for long-running gateways.
- **Priority P1 / Data Loss & Session Hangs:**
    - [#44925 - Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925): Remains the top-rated bug. No linked fix PR is evident, indicating a deeply complex issue.
    - [#52249 - ACP parent session stuck](https://github.com/openclaw/openclaw/issues/52249) / [#47975 - Subagent sessions persist](https://github.com/openclaw/openclaw/issues/47975): Core orchestration is fragile, with parent sessions becoming unresponsive.
    - [#53408 - Write/exec tool parameters silently dropped](https://github.com/openclaw/openclaw/issues/53408): A bizarre and dangerous regression where core tool parameters vanish in long conversations.
- **Prioritized Fixes in Progress:**
    - A fix for the **subagent announce recovery cascade** is in review (**PR #97932**).
    - A potential fix for **cron hallucinated output** is linked (**PR #99864**).

### 6. Feature Requests & Roadmap Signals
- **Predicted for Next Release:**
    - **Reusable AI Runtime (#99059):** This architectural refactoring is likely to be merged soon, enabling better plugin ecosystems and third-party use.
    - **Multi-Account Channels (#97340):** The Microsoft Teams multi-account PR is a large feature that has been in development for a while and is nearing readiness.
    - **Gateway Lifecycle Hooks (#43454):** Multiple requests for hooks at `onSubagentComplete`, `onToolCallThreshold`, etc., signal a strong roadmap push for an event-driven architecture.
- **Long-Term Signals:**
    - **"ClawHub" Community Ecosystem (#50090):** The discussion around skills is shifting from a technical "how-to" to a "business" issue, with users asking for discovery, quality ratings, and installation management.
    - **Unbypassable Outbound Policy (#56349):** The user base shows a growing demand for "insurance-grade" agent safety, moving beyond prompt engineering to immutable enforcement.

### 7. User Feedback Summary
- **Dissatisfaction (High Pain):**
    - **Silent Failure is the #1 complaint:** Users are not just filing bugs; they are reporting real-world trust erosion. They cannot rely on the agent to complete tasks without manual intervention and constant monitoring.
    - **"It used to work" Regressions:** Many reports (e.g., [#32473](https://github.com/openclaw/openclaw/issues/32473), [#45765](https://github.com/openclaw/openclaw/issues/45765)) indicate a perception of instability, where new releases break previously working functionality.
    - **Confusing Configuration:** The hardcoded path bug ([#51429](https://github.com/openclaw/openclaw/issues/51429)) and the nested directory issue ([#45765](https://github.com/openclaw/openclaw/issues/45765)) highlight a poor out-of-the-box experience.
- **Satisfaction & Use Cases:**
    - **Advanced Automation:** Users are pushing the limits in complex, multi-agent, and multi-step scenarios. The "Browser tool field report" ([#44431](https://github.com/openclaw/openclaw/issues/44431)) shows active, advanced usage.
    - **Community-Driven Development:** The high volume of high-quality feature requests and PRs demonstrates a strong, technically capable community that is invested in the project's direction.

### 8. Backlog Watch
- **Critical Issues Stuck Awaiting Maintainer Review:**
    - [#22676 - Signal daemon race condition](https://github.com/openclaw/openclaw/issues/22676) (Feb 21): This P1 bug has been open for over 4 months and is a critical reliability issue for gateway operators. A fix is likely non-trivial.
    - [#7722 - Filesystem Sandboxing Config](https://github.com/openclaw/openclaw/issues/7722) (Feb 3): This is a top-voted feature request with a clear initial implementation that has been pending for 5+ months.
    - [#13583 - Pre-response enforcement hooks](https://github.com/openclaw/openclaw/issues/13583) (Feb 10): A high-impact security feature that is deeply desired by the power-user community.
- **Long-Standing, Unmerged PR:**
    - [#89040 - Avoid event-loop stall during embedded_run](https://github.com/openclaw/openclaw/pull/89040) (Jun 1): A P1 fix for message loss due to 14-22 second stalls. It is "ready for maintainer look" but has been waiting for over a month. This is a classic sign of a complex change needing careful review but falling through the cracks.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the July 5, 2026 community digest data.

---

## Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem
**Date:** 2026-07-05

### 1. Ecosystem Overview
The personal AI agent open-source ecosystem on July 5, 2026, is characterized by extreme velocity and a clear bifurcation between mature, community-driven platforms (OpenClaw) and specialized, rapidly iterating tools. The dominant themes are **agent reliability** (combating silent failures and state loss) and **security hardening** (credential injection, display spoofing, and outbound policy enforcement). While the "big three" projects—OpenClaw, Hermes Agent, and ZeroClaw—drive the majority of architectural change, smaller projects like NanoClaw and PicoClaw demonstrate healthy niche innovation in containerization and mobile support. The ecosystem is moving from a "can it work?" phase to a "can we trust it in production?" phase.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases Today | Health Score & Notes |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500+ | 500+ | None | **High Velocity / High Risk.** Massive volume, but critical session reliability and billing bugs (P0) are unresolved. |
| **NanoBot** | 2 (Critical) | 13 (7 merged) | None | **Stable / Healthy.** Excellent bug-to-fix turnaround. All recent P0/P1 bugs resolved within 48 hours. |
| **Hermes Agent** | 50 | 50 (10 merged) | None | **High Activity / Productive.** Strong merge rate for security (iron-proxy) and new features (Fable copilot). |
| **PicoClaw** | 4 | 7 (2 merged) | None | **Moderate / Consolidating.** Healthy fixes, but a critical Android launch blocker remains unaddressed. |
| **NanoClaw** | 1 (Security) | 39 (22 merged) | None | **Very High Velocity / Hardening.** Highest PR merge rate today, focused on security docs and dead code removal. |
| **NullClaw** | 0 | 0 | N/A | **Inactive.** |
| **IronClaw** | 9 | 44 (16 merged) | None | **High Velocity / Feature Stacking.** Deep in a coordinated Slack OAuth migration and CI hardening sprint. |
| **LobsterAI** | 1 | 3 (2 merged) | None | **Stable / Low Activity.** Quiet day with a focus on minor bug fixes. |
| **TinyClaw** | 0 | 0 | N/A | **Inactive.** |
| **Moltis** | 0 | 0 | N/A | **Inactive.** |
| **CoPaw** | 11 | 3 (0 merged) | None | **Moderate / Bug-Stabilization.** High community frustration over memory regressions in the `2.0.0b3` release. |
| **ZeptoClaw** | 0 | 0 | N/A | **Inactive.** |
| **ZeroClaw** | 50 | 50 (2 merged) | None | **Very High Velocity / Pre-Release Sprint.** Intense feature development for v0.8.3, but with a backlog of critical (S1) runtime panics and security bypasses. |

### 3. OpenClaw's Position

- **Advantages vs. Peers:** OpenClaw commands the largest and most engaged community by a significant margin (500+ issues/PRs daily vs. ~50 for the next tier). This results in a massive feature surface area, including advanced multi-agent orchestration (subagent management), a rich plugin ecosystem (ClawHub), and deep integrations. Its core architectural work on a reusable AI runtime (#99059) is a strategic advantage for future modularity.
- **Technical Approach Differences:** OpenClaw appears to have a more ambitious, "kitchen sink" architecture aimed at enterprise-grade automation. This contrasts with the more focused approaches of, for example, NanoBot (high reliability for specific providers) and ZeroClaw (goal-mode and visual SOPs). OpenClaw's "ClawSweeper" backlog management system is a unique, high-volume maintenance process.
- **Community Size Comparison:** OpenClaw's community is an order of magnitude larger than all other projects combined, based on raw activity metrics. However, this scale introduces coordination problems, as evidenced by many high-impact issues (e.g., #22676, #7722) stuck awaiting maintainer review for months. The high volume masks a growing trust deficit caused by unresolved P0 bugs around data loss and silent failures.

### 4. Shared Technical Focus Areas

Several requirements are emerging independently across multiple projects, indicating core pain points for the entire ecosystem.

- **Agent Memory & Context Reliability:**
    - *CoPaw*: Critical regression in `2.0.0b3` causing memory state loss and "scroll" compression destroying context (#5775, #5778).
    - *Hermes Agent*: Prior-turn reasoning stripped on replay with vLLM (#56004). Long-standing feature request for a formal RAG system (#844).
    - *ZeroClaw*: Context compression dropping `tool_calls` for OpenAI-compatible providers (#6361, now fixed).
    - *Need*: A robust, standardized approach to managing long-term memory and context windows that prevents silent data loss.

- **Tool & Plugin Management in Multi-Agent Scenarios:**
    - *OpenClaw*: Subagents lack access to MCP tools, forcing workarounds (#4697).
    - *ZeroClaw*: MCP tools exposed to gateway but not to TUI sessions (#8193, now fixed).
    - *PicoClaw*: Support for agent-specific runtime overrides, including tool thresholds (PR #3225).
    - *Need*: A consistent pattern for inheriting and scoping tools across subagents and different user interfaces (TUI, gateway, Slack).

- **Security & Outbound Policy Enforcement:**
    - *OpenClaw*: Demand for "hard gates" against LLM disobedience (#13583) and unbypassable outbound policy (#56349).
    - *Hermes Agent*: Merged "iron-proxy" for credential injection in sandboxes (#30179).
    - *NanoClaw*: Security documentation rewrite (#2945) and a report of approval-card display spoofing (#2923).
    - *ZeroClaw*: SOP `advance_step` bypassing security gates (#8678) and high-entropy token redaction issues (#8722).
    - *Need*: A shift from prompt-based safety to **immutable, infrastructure-level policy enforcement** that cannot be bypassed by the agent or its tools.

- **WebUI & Desktop UX Parity:**
    - *Hermes Agent*: Top-reacted feature request is for per-session workspace switching (#40297).
    - *NanoBot*: Smooth Markdown streaming and viewport fixes (PR #4696, #4694).
    - *PicoClaw*: Android launch failure blocking mobile users (#3182).
    - *Need*: A unified, high-quality user experience across desktop and mobile that matches the power of the CLI and API.

### 5. Differentiation Analysis

- **OpenClaw:** The **generalist powerhouse**. Targets advanced developers and enterprise teams building complex, multi-agent workflows. Its biggest strength (massive feature set) is also its biggest weakness (risk of instability and complexity).
- **Hermes Agent:** The **security and research-focused platform**. Strong emphasis on sandbox security (iron-proxy) and high-stakes reasoning (Fable copilot). Appeals to organizations requiring auditability and "insurance-grade" safety.
- **ZeroClaw:** The **visual workflow orchestrator**. Focuses on the "Goal Mode" and "SOP (Standard Operating Procedure)" engine, making complex agent workflows more manageable and auditable. Its target user is the power user who needs to build and enforce structured processes.
- **NanoBot & NanoClaw:** The **reliable utilities module**. NanoBot excels at provider-specific reliability (fixing Copilot/MCP crashes), while NanoClaw is a lean, container-first agent focused on CLI and mounting. They serve users who need a dependable, low-friction machine for specific tasks.
- **IronClaw:** The **Rust-native performance core**. Indicated by the move to Rust (`ironclaw_common` crate), this project focuses on high-performance agent infrastructure. Its Slack OAuth migration suggests a focus on enterprise-grade team collaboration. Currently in a "refactor or rebuild" phase on the Reborn substrate.
- **CoPaw:** The **experimental pre-release platform**. The user base is actively testing the `2.0.0b3` architecture, finding critical memory bugs. This project is for early adopters willing to tolerate instability for a peek at the next generation of agent architecture.

### 6. Community Momentum & Maturity

- **Tier 1: Rapidly Iterating / High Feature Churn (Pre-Release or Active Sprint)**
    - **OpenClaw, Hermes Agent, ZeroClaw, NanoClaw, IronClaw.** These projects have the highest volume of new features and PRs. They are in a constant state of major development, which brings innovation but also significant regressions and stability risks (e.g., OpenClaw's P0 bugs, ZeroClaw's SIGSEGV panics).

- **Tier 2: Stabilizing & Maintenance Phase**
    - **NanoBot.** Excellent hygiene. The project is focused on fixing bugs quickly and maintaining platform parity. The low issue count and high closure rate signal a mature, stable codebase.
    - **PicoClaw.** Moderate activity with a focus on session fixes and infrastructure polish (Docker updates). It is in a consolidation phase between patches.
    - **CoPaw.** In a bug-stabilization cycle following a major pre-release. The community is actively debugging, but the project is not shipping new features.

- **Tier 3: Inactive / Low Activity**
    - **NullClaw, TinyClaw, Moltis, ZeptoClaw.** No activity in the last 24 hours, suggesting either dormancy or very long development cycles.

### 7. Trend Signals

- **The "Trust Erosion" Risk:** The single most significant trend is the shift from "making agents work" to **"making agents trustworthy."** The community is explicitly demanding that agents not fail silently, not lose data, and not bypass security rules. Projects that fail to address this (e.g., OpenClaw with its growing backlog of critical reliability bugs) are at risk of losing their power-user base to more reliable alternatives.

- **The Rise of Infrastructure-Level Safety:** Agents are being deployed in production and for insurance-grade use cases. This is driving demand for **immutable policy enforcement** (hooks, proxies, sandboxing) over "advisory" prompt engineering. This is a clear maturation signal—the ecosystem is moving beyond MVPs to real-world deployment requirements.

- **Unified UX is the Next Frontier:** While CLI and API power exist, the demand for beautiful, functional **WebUI and desktop apps** is exploding (e.g., Hermes Agent's workspace switching, NanoBot's Markdown rendering). The next competitive battleground will be the user experience for non-CLI operators.

- **Subagent Standards are Needed:** The universal struggle to get subagents to inherit tools, memory, and context (across OpenClaw, ZeroClaw, and PicoClaw) points to a need for a **formal standard for subagent lifecycle and capability inheritance**. This is a core architecture problem that the ecosystem has not yet solved.

- **Value for Developers:** The current landscape offers a choice between **power and stability**. For production pipelines, NanoBot or IronClaw’s Rust core offer high reliability. For complex, experimental workflows, ZeroClaw’s visual SOP engine is a unique differentiator. OpenClaw remains the platform of choice for maximum flexibility and community support, but developers must budget for stability overhead and contribute to fixing its critical gaps.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

NanoBot Project Digest – 2026-07-05
=========================================

1. Today's Overview
-------------------
The NanoBot project is in a **high-activity, stable maintenance phase**. Over the past 24 hours, 13 pull requests were updated (7 merged/closed), and 2 critical issues were resolved. While no new releases were cut, the merge velocity and bug-fix churn are strong. The project continues to receive robust community contributions across platform stability, WebUI polish, and provider reliability. No regressions from recent upstream merges were observed, signaling good code hygiene.

2. Releases
-----------
**None** – No releases were published today.

3. Project Progress (Merged/Closed PRs)
-----------------------------------------
The following 7 PRs were merged or closed, advancing core stability and platform support:

- **#4695** (Merge/upstream 2026-06-26) – Routine upstream merge to keep the fork aligned.
- **#4690** – Fix `nanobot gateway stop` crash on Windows (OSError fallback) – improves Windows parity.
- **#4666** – ✅ **Fixes #4652**: Contain malformed MCP tool results; surfaces structured errors for timeouts, cancellations, and execution exceptions.
- **#4653** – Restore crash-durable atomic writes in `pairing._save()` – a regression fix for data integrity.
- **#4684** – ✅ **Fixes #4677**: Guards Copilot token refresh with `asyncio.Lock` to prevent race conditions under concurrent requests.
- **#4692** – Serialize model presets as `modelPresets` (camelCase) for consistency with documentation.
- **#4646** – Fix DingTalk channel shutdown: ensures stream websocket is properly closed to avoid runtime leaks.

4. Community Hot Topics
------------------------------
- **#4677 (Issue – Closed)** – *GitHub Copilot: token refresh race condition under concurrent requests*. This issue drew community attention (1 comment) because it affected a widely-used provider. The associated fix PR **#4684** was merged, resolving the root cause cleanly.
- **#4652 (Issue – Closed)** – *Nanobot crashes on MCP tool call exception*. Although low in engagement (3 comments), this fix (PR #4666) was a high priority because it prevented complete process crashes in production environments. Underlying need: graceful error handling in MCP toolchains.

5. Bugs & Stability
-------------------
All reported bugs from the active period have been resolved:

| Severity | Issue | Description | Fix PR |
|----------|-------|-------------|--------|
| **P0** (Critical) | #4652 | Process crash on MCP tool call exception | #4666 (merged) |
| **P1** (High) | #4677 | Copilot token refresh race condition (concurrent requests) | #4684 (merged) |
| **P1** (High) | #4653 | Lost atomic writes in pairing module (data integrity) | #4653 (merged) |
| **P2** (Medium) | #4690 | `nanobot gateway stop` crash on Windows | #4690 (merged) |
| **P2** (Medium) | #4646 | DingTalk stream task not cancelled on shutdown | #4646 (merged) |

**No unresolved bugs** remain in the active window.

6. Feature Requests & Roadmap Signals
--------------------------------------
- **#4697 (PR – Open)** – *Configurable MCP inheritance for specialist subagents*. This feature allows spawned subagents to inherit selected MCP servers from the main agent. This addresses a clear user need: subagents currently lack database/search tools, forcing raw shell workarounds. This is likely to be merged into the next minor version.
- **#4696 (PR – Open)** – *Smooth WebUI streaming Markdown reveal*. Adds buffered rendering with reading-speed pacing and code-block animations. This is a quality-of-life UX improvement likely to ship soon given the WebUI focus.
- **#4459 (PR – Open, stale)** – *Mattermost channel support* (since 2026-06-22). A substantial new integration addition that may land in a future release, though maintenance attention may be slowing it.

7. User Feedback Summary
-------------------------
- **Pain points addressed**: Users reported two critical stability issues (MCP crash, Copilot race condition) – both were fixed within 48 hours. This indicates high maintainer responsiveness.
- **Use case evolution**: PRs show increasing demand for **multi-platform provider reliability** (Copilot, DingTalk, Mattermost) and **WebUI mobile UX** (#4694 – narrow viewport fix).
- **Satisfaction indicators**: Rapid turnaround on P0/P1 bugs, plus community-authored PRs (e.g., #4697 subagent config, #4696 streaming animation) suggest a healthy contributor ecosystem.

8. Backlog Watch
-----------------
- **PR #4459** – *Mattermost channel support* (last updated 2026-07-04, open since 2026-06-22). This is a large feature PR with no recent maintainer comment or merge update. If the team plans to support Mattermost, this needs a review pass to avoid bit-rot.
- **No orphaned issues** – all open issues from the past 48 hours have been closed or have active fix PRs. No long-neglected support requests were identified.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the **Hermes Agent Project Digest** for **2026-07-05**.

---

## Hermes Agent Project Digest — 2026-07-05

### 1. Today's Overview
Project activity is **very high**, with 50 issues and 50 PRs updated in the last 24 hours. While no new releases were cut, the project is processing a significant volume of community contributions and bug fixes. The community is actively discussing a long-standing Knowledgebase RAG feature request, while maintainers are merging critical fixes for vision fallback, desktop onboarding, and credential handling. The 7-day moving average of open issues has likely jumped due to the high volume of new reports, but the closure rate (10 merged/closed PRs) remains healthy.

### 2. Releases
**None.** No new releases were published today. The last stable version remains **0.18.0**.

### 3. Project Progress
**Merged/Closed PRs today:** 10 (out of 50 updated). Notable closed PRs and their impact:

- **#30179 (Merged):** `feat(egress): iron-proxy credential-injection firewall for sandboxes` — A major security feature adding an optional TLS-intercepting proxy for remote terminal sandboxes. This prevents leaked provider API keys even if a sandbox is compromised.
- **#58575 (Closed):** `fix(lazy_deps): use sentinel package for active-feature detection` — Fixes false positives where shared dependency pins made inactive backends appear "active," causing Windows build failures.
- **#58370 (Closed):** `Implement Fable copilot for critical planning and critique` — Adds an expensive-model copilot path for high-stakes reasoning without changing the default model.
- **#58518 (Closed):** `fix(gateway): WebUI resume list can hide active CLI sessions` — Ensures all persisted sessions are visible in the WebUI immediately.

### 4. Community Hot Topics
The following issues and PRs generated the most discussion and reactions:

- **#844 (Feature, 7 comments, 4 👍):** *"Feature: Knowledgebase RAG System"* — The most popular open feature request. The user wants a plug-and-play directory-based RAG pipeline. This has been open since March, indicating high demand but complex implementation considerations.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/844)

- **#42864 (RFC, 6 comments):** *"scope-recall standalone memory provider"* — A community maintainer proposes integrating a turn-recall and auditable local memory plugin. This represents organic ecosystem growth, but maintainers have not yet responded with a decision.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/42864)

- **#40297 (Feature, 5 comments, 9 👍):** *"Desktop: make workspace selectable per session"* — The top-reacted issue today. Users want a long-lived desktop app that allows switching workspaces without restarting. This is a clear UX pain point for power users.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/40297)

- **#56004 (Bug, 3 comments, 2 👍):** *"Qwen3.6 / vLLM: prior-turn reasoning stripped on replay"* — Multi-turn reasoning context is lost when using vLLM, breaking agent memory continuity. Strong interest from Qwen users.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/56004)

### 5. Bugs & Stability
**New bugs reported today (ranked by severity):**

- **P1 (Security):** `#58583` — Discord adapter regression in v0.18.0 silently blocks ALL messages when no allowlists are configured. **Fix PR exists:** `#58583`.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/58583)

- **P2 (Critical):** `#58596` — `DaemonThreadPoolExecutor` crashes on Python 3.14 due to removed internal attributes. Breaks all concurrent features (delegation, skills, memory). **Fix PR exists:** `#58598`.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/58596)

- **P2 (Functionality):** `#58581` — `vision_analyze` fails to fallback to `auxiliary.vision` when the primary model lacks vision support. **Fix PR exists:** `#58600`.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/58581)

- **P2 (Stability):** `#58484` — Telegram polling enters an infinite reconnect loop because the retry counter never increments. **No fix PR yet.**
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/58484)

- **P2 (Desktop):** `#58498` — Hermes Desktop ignores the OpenAI Codex provider and routes requests through the Nous Portal instead, causing auth failures.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/58498)

- **P3 (Numerous):** Existing issues with Matrix build failures on Windows (`#58458`), TUI resize issues (`#35530`), and Secret Profile auth staleness (`#34143`) remain open.

### 6. Feature Requests & Roadmap Signals
High-demand features likely to land in the next release (v0.19.0):

| Feature | Issue | Likelihood | Rationale |
|---|---|---|---|
| **Knowledgebase RAG System** | [#844](https://github.com/NousResearch/hermes-agent/issues/844) | High | Most popular request; persisted memory and workspace features are prerequisites. |
| **Per-session workspace switching** | [#40297](https://github.com/NousResearch/hermes-agent/issues/40297) | High | 9 👍, clear UX improvement, aligns with ongoing desktop enhancements. |
| **WhatsApp setup wizard** | [#58041](https://github.com/NousResearch/hermes-agent/issues/58041) | Medium | Repeated user complaints about complexity; a wizard would reduce support queries. |
| **Free LLM provider profiles (Groq, Cerebras, Mistral)** | PR [#58586](https://github.com/NousResearch/hermes-agent/pull/58586) | High (already a PR) | Directly improves adoption for cost-sensitive users. |
| **Voice wake word for Desktop** | [#49383](https://github.com/NousResearch/hermes-agent/issues/49383) | Low-Medium | Niche but growing interest in hands-free interaction. |

### 7. User Feedback Summary
- **Pain Points (High Satisfaction Negative):**
  - **Desktop Workspace Limitation:** Users repeatedly ask for the desktop app to allow folder/project switching mid-session without restarting (`#40297`). This is a top friction point for knowledge workers.
  - **Skill Enforcement:** A user reports that skilled instructions are treated as "advisory" and ignored (`#58569`). This undermines trust in deterministic skill execution.
  - **First-call Vision Failures:** Multiple users report that the first vision call always fails if the primary model is text-only (`#57948`, `#58581`), degrading the out-of-box experience.
- **Satisfaction Signals:**
  - The **scope-recall memory provider** (`#42864`) shows a healthy plugin ecosystem with active third-party maintainers.
  - The **Fable copilot** (`#58370`) and **iron-proxy** (`#30179`) features demonstrate active investment in both advanced reasoning and security.

### 8. Backlog Watch
Issues and PRs that require maintainer attention due to age or impact:

- **#844 (Feature, opened 2026-03-10):** *Knowledgebase RAG* — 4 months old, the most commented/reactioned issue, yet no official design RFC or milestone assignment.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/844)

- **#42864 (RFC, opened 2026-06-09):** *scope-recall memory provider* — 26 days with no maintainer response. The author is asking for a decision before further development.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/42864)

- **#21709 (Bug, opened 2026-05-08):** *Hindsight memory stores novel content causing identity confusion* — Long-standing bug affecting literary analysis use cases. No PR or triage label update in 2 months.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/21709)

- **#34143 (Bug, opened 2026-05-28):** *Profile Codex auth can ignore global credential pool* — Staleness issue causing auth failures for profile users. Labeled P2 but no assignee.
  [View Issue](https://github.com/NousResearch/hermes-agent/issues/34143)

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for **2026-07-05**.

---

## PicoClaw Project Digest — 2026-07-05

### 1. Today's Overview
PicoClaw shows **moderate, healthy activity** today with 4 issues and 7 pull requests updated in the last 24 hours. The project closed 2 PRs and 1 issue, indicating steady forward momentum, particularly around **session management fixes** and **infrastructure polish** (Docker base image bumps, gitignore cleanup). However, a notable **stability bug** surrounding encrypted Matrix messages remains unaddressed, and a **critical Android launch issue** persists without a linked fix. No new releases were published today, suggesting a **consolidation phase** between patches.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
Two pull requests were **merged or closed** today, advancing stability and code quality:

- **[PR #3221 (Closed – Revert)]** – Reverted a Windows sandbox filesystem path handling test (`#3158`) due to an import error in `provider.go`. This indicates the original test introduced a regression or compile failure; reverting restores stability.
- **[PR #3224 (Closed – Merged)]** – **`fix(agent): clear routed agent session`** — Fixes a bug where the `/clear` command cleared the *default* agent’s session instead of the *routed* agent’s session when multiple agents were configured. This is a **user-facing fix** for multi-agent workflows.

### 4. Community Hot Topics
The most active discussions today center on **cryptography and multi-agent routing**:

- **[Issue #3088](https://github.com/sipeed/picoclaw/issues/3088) – [Feature] Use vodozemac instead of libolm** (👍2, 4 comments) — The community is pushing to replace the unmaintained, insecure `libolm` with `vodozemac`. This is a **security-driven feature request** that aligns with industry best practices. The issue is tagged `help wanted` and `priority: high`, but remains open with no linked PR.
- **[Issue #3150](https://github.com/sipeed/picoclaw/issues/3150) (Closed) – [BUG] 它给自己整失忆了** (4 comments) — Closed as stale. The Chinese title roughly translates to "it gave itself amnesia," likely a session or context-loss bug. No resolution was recorded beyond staleness.
- **[PR #3225](https://github.com/sipeed/picoclaw/pull/3225) (Open) – Support agent-specific runtime overrides** — This new PR proposes per-agent overrides for `max_tokens`, summarization thresholds, and `split_on_marker`. It reflects **growing demand for fine-grained agent control**.

### 5. Bugs & Stability
Three bugs were reported or updated today, ranked by severity:

1. **HIGH – [Issue #3182](https://github.com/sipeed/picoclaw/issues/3182) – Android version cannot launch service** — User reports inability to launch the service despite full permissions, and cannot change paths from settings. No linked fix PR exists. This blocks Android users entirely.
2. **MEDIUM – [Issue #3194](https://github.com/sipeed/picoclaw/issues/3194) – Received encrypted message but crypto is not enabled** — User running `v0.2.4` on `go1.25.8` receives log messages about encrypted content but crypto is disabled. This is a **configuration/detection gap** — either the user needs guidance or the gateway should offer a clearer warning. No fix PR.
3. **LOW – [PR #3189](https://github.com/sipeed/picoclaw/pull/3189) (Open) – Explicitly ignore `resp.Body.Close()` errors in LINE channel** — A cosmetic/stability fix for error handling in the LINE channel. Not a crash, but improves Go static analysis compliance.

### 6. Feature Requests & Roadmap Signals
Two feature requests stand out with strong roadmap implications:

- **[Issue #3088](https://github.com/sipeed/picoclaw/issues/3088) – Use vodozemac instead of libolm** — High priority, 2 reactions. This is likely to land in the **next minor release** (v0.2.5 or v0.3.0) given the security urgency.
- **[PR #3225](https://github.com/sipeed/picoclaw/pull/3225) – Support agent-specific runtime overrides** — Submitted today. If merged, this would be a **targeted feature addition** without a full release, possibly shipped as a patch. It addresses a common ask from power users running multiple agents.
- **[PR #3190](https://github.com/sipeed/picoclaw/pull/3190) – i18n sync (bn-in, cs)** — Ongoing internationalization efforts suggest the team is preparing for **broader locale support**, possibly ahead of a stable release.

### 7. User Feedback Summary
- **Satisfaction:** No strong positive feedback in today’s data, though the quick revert of a broken test (`#3221`) and the session clear fix (`#3224`) indicate responsive maintenance.
- **Pain Points:**
  - **Android launch failure** (Issue #3182) is a **blocking issue** for mobile users.
  - **Encrypted Matrix message confusion** (Issue #3194) — users expect transparent crypto handling; current behavior is opaque and frustrating.
  - **Multi-agent /clear bug** (fixed in #3224) was causing confusion for users with multiple agents configured.
- **Unmet Needs:** The **vodozemac replacement** (Issue #3088) has 2 upvotes but no work started, signaling a gap between community urgency and engineering bandwidth.

### 8. Backlog Watch
The following items require maintainer attention:

- **[Issue #3088](https://github.com/sipeed/picoclaw/issues/3088) (Open, 27 days, 4 comments, 2 👍, `help wanted`, `priority: high`)** — No assignee; no linked PR. This security-critical task is at risk of stalling.
- **[Issue #3182](https://github.com/sipeed/picoclaw/issues/3182) (Open, 9 days, 2 comments, 0 👍)** — Android launch bug with no response from maintainers. User likely needs either a fix or a workaround.
- **[PR #3192](https://github.com/sipeed/picoclaw/pull/3192) (Open, 8 days, stale)** — Docker base image bump from Alpine 3.21 to 3.23. Simple chore, waiting for review.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-05

## Today's Overview
NanoClaw had a **highly active day** with 39 pull requests updated in the last 24 hours—of which 22 were merged or closed—and 1 new security issue opened. The project remains in a **sustained cleanup and hardening phase**, with significant attention to security documentation rewrites, dead code removal, and mounting/perimeter refinements. The maintainer team (led by gavrielc) drove aggressive technical debt reduction across 18 merged PRs, while community contributors (javexed, dim0627, stumpjumper) brought in skills and fixes. No new releases were published.

## Releases
**No new releases** in the last 24 hours. The project appears to be building toward a v2.1.39 or v2.2 milestone based on the volume of merged fixes.

## Project Progress
**22 PRs merged/closed today** — the highest single-day merge velocity observed in recent weeks. Key areas of progress:

- **Security perimeter hardening (4 PRs):** Rewritten `docs/SECURITY.md` to match the v2 container perimeter (#2945), added Phase-1 security reporting/triage policy (#2954, new), made security env vars (`NANOCLAW_EGRESS_LOCKDOWN`, etc.) reachable under the shipped service (#2934), and fixed mount allowlist `readOnly` key handling (#2943)
- **Dead code & config cleanup (4 PRs):** Removed v1 config knobs and broken pnpm auth script (#2935), cleaned up dead `ncl` CLI protocol vocabulary (#2936), deleted deprecated session-DB split shims (#2940), removed dead `data/env/env` secrets mirror (#2946)
- **Mount & container fixes (3 PRs):** Added `ncl groups config add-mount/remove-mount` verbs (#2939), fixed stale mount topology docs (#2953), made `buildAgentGroupImage` asynchronous instead of blocking the host (#2931)
- **Cross-process fix:** Fixed agent-to-agent `in_reply_to` stamp that was a no-op across processes (#2942)
- **Session resilience:** Session folders are now re-provisioned on write to support documented `rm -rf` reset (#2937)
- **Doc refresh:** Corrected stale architecture, scheduling, provider-config, and overlay docs (#2948)
- **Feature:** Colored buttons (primary/danger) on Slack approval cards (#2933)

## Community Hot Topics
The **most active** items (by comment count, though all shown here had undefined comment counts) were:

- **#2923** `[Security] ask_user_question card defacement` (OPEN) — The sole open issue. Reports that a forged button click can overwrite displayed text on approval cards even when the underlying response is correctly rejected. This is a display/integrity spoof vulnerability. [(Link)](https://github.com/nanocoai/nanoclaw/issues/2923) — *Underlying need: approval-card UI integrity guarantees during the origin-auth race window*

- **#2956** `fix(agent-runner): suppress duplicate delivery` (OPEN) — Fixes agents that send via `send_message` tool *and* repeat text in final output delivering duplicate messages. [(Link)](https://github.com/nanocoai/nanoclaw/pull/2956) — *Underlying need: deduplication logic in the result delivery path*

- **#2955** `fix(router): mention-sticky must not subscribe channel root` (OPEN) — Fixes a case where session existence (without engagement) causes incorrect subscription state in mention-sticky routing. [(Link)](https://github.com/nanocoai/nanoclaw/pull/2955) — *Underlying need: routing correct behavior for unengaged mentions*

- **#2952 / #2951 / #2949** (OPEN) — Three PRs from javexed adding operational skills: OpenCode stack integration, `OPENCODE_BASE_URL` config fix with `NO_PROXY`, and `/add-litellm` minimal model router for local servers. [(Link to #2952)](https://github.com/nanocoai/nanoclaw/pull/2952) — *Signals growing community interest in local/self-hosted model routing*

## Bugs & Stability
**1 security bug reported today**, ranked by severity:

1. **[HIGH] Issue #2923** — `ask_user_question` card display defacement. A forged click before origin authorization can overwrite card text with an attacker's label. This is **not** a full response injection (the origin check correctly rejects it), but it is a **display spoof** that could mislead users about who is responding. No fix PR exists yet. [(Link)](https://github.com/nanocoai/nanoclaw/issues/2923)

## Feature Requests & Roadmap Signals
- **Local model routing** — The `/add-litellm` skill PR (#2949) and OpenCode integration (#2952, #2951) signal strong community demand for running NanoClaw agents against local/self-hosted LLM backends instead of only Anthropic-hosted models. Likely to land in v2.2.
- **Colored approval buttons** — Already merged (#2933), this user-visible feature improves operator UX for approval workflows.
- **Mount management from CLI** — The `add-mount/remove-mount` verbs (#2939) are now available for host-only `ncl` commands, enabling easier container storage configuration.

## User Feedback Summary
- **Pain point (solved):** Agent output duplication — agents using `send_message` tool were delivering identical content twice; fix in #2956 addresses this.
- **Pain point (solved):** Docker builds freezing host — `execSync` during agent image builds blocked the single-threaded host; now async (#2931).
- **Pain point (solved):** Session reset not working — documented `rm -rf` session folder approach failed silently; now re-provisions missing folders (#2937).
- **Pain point (open):** Approval card UI can be spoofed — operator trust in visual approval indicators is compromised (#2923).
- **Satisfaction signal:** High merge velocity (22 closed PRs) and participation from 4+ distinct contributors indicates healthy community engagement.

## Backlog Watch
No long-unanswered issues currently stand out. The open issue (#2923) was created yesterday (2026-07-04) and is still fresh. Notable open PRs that may need attention:
- **#2956** (stumpjumper) — Delivery deduplication fix, 0 comments, opened today. Likely needs review from a maintainer familiar with `dispatchResultText`.
- **#2952 / #2951 / #2949** (javexed) — Three skill additions, all opened 2026-07-04, awaiting maintainer sign-offs after the Phase-1 security policy (#2954) merges.
- **#2955** (dim0627) — Routing fix for mention-sticky behavior, opened 2026-07-04, no comments.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-05

## Today's Overview

High-velocity day with **44 PRs** updated in the last 24 hours (16 merged/closed) and **9 issues** active, signaling a major feature stack in motion. The team is deep in a coordinated **Slack personal OAuth** rollout (4-PR stack: #5643→#5644→#5645→#5646) alongside quality-infrastructure hardening (wiring-parity guards, coverage ratcheting, error-swallowing prevention). CI reliability remains a friction point, with Railway deployment blocks from skipped jobs (#5636) and a recent main-branch greenness regression (#5590) that has been closed. No new releases today.

## Releases

**None** — no new releases published in the last 24 hours. The `chore: release` PR #5598 (bumping `ironclaw_common` 0.4.2→0.5.0 with breaking changes, `ironclaw` 0.24.0→0.29.1) remains open.

## Project Progress

**16 PRs merged/closed today.** Notable advances:

- **Slack OAuth stack** — The 4-part migration from pairing codes to personal OAuth saw all pieces land as open PRs. `PR #5644` (foundations, 77 files), `PR #5645` (swap, 121 deletion-dominated files), `PR #5646` (breaking config reject), and `PR #5643` (CI for webui_v2 JS tests) are all open and under active review. A companion codex PR `#5604` (Remove Slack pairing flow) was also submitted.
- **State migration tool** — `PR #5627` (closed) adds `ironclaw_reborn_migration` crate to convert v1/engine-v2 persisted state to Reborn substrate without silent loss.
- **Error handling** — `PR #5652` (open) promotes `unused_must_use` to workspace-wide deny; `PR #5651` (open) adds static enforcement against swallowed errors. This follows the design audit document `PR #5383` (closed).
- **CI optimization** — `PR #5635` (closed) benchmarked bucketed crate tests; `PR #5648` (open) benchmarks narrower test targets; `PR #5606` (closed) added OVH sccache to gateway smoke (baseline improvement from 48→? min).
- **Ingress routes from manifest** — `PR #5626` (open) makes Slack ingress contract manifest-driven instead of hand-written Rust policy literals.
- **Subagent fix** — `PR #5170` (open) adds `LoopInlineMessageBody` for host-approved inline prompts, fixing subagent spawn failures.
- **Final-answer nudge** — `PR #5304` (open) enables final-answer nudge for interactive runs to prevent empty-turn exits.

## Community Hot Topics

- **`PR #5645` — Swap Slack pairing codes for personal OAuth** ([link](https://github.com/nearai/ironclaw/pull/5645)) — XL-sized, risk: medium, spans 7 scopes (channel/cli, channel/web, tool, tool/builtin, pairing, docs). The core architectural change of the day, deleting pairing code in favor of OAuth. Underlying need: user-owned, revocable, capability-scoped Slack access without shared secrets.

- **`PR #5644` — Slack personal OAuth foundations** ([link](https://github.com/nearai/ironclaw/pull/5644)) — Companion 77-file additive layer with OAuth primitives, dormant until paired with PR #5645. Active review discussion on scope split (see Issue #5650).

- **`Issue #5636` — CI job-level skips block Railway deploys** ([link](https://github.com/nearai/ironclaw/issues/5636)) — Railway's "Wait for CI" blocks on intentionally-skipped jobs. Underlying need: deployment pipeline must distinguish "skipped intentionally" from "skipped due to failure."

- **`PR #5550` — Dependabot bulk update** ([link](https://github.com/nearai/ironclaw/pull/5550)) — 13 dependency bumps including a `0.10.4→1.0.1` major jump for `agent-client-protocol`. High attention due to API-breaking semver risk.

## Bugs & Stability

| Severity | Issue/PR | Description | Fix Status |
|----------|----------|-------------|------------|
| **Medium** | `#5647` | Bridged tool disclosure + narrowed allowlist strips bridge meta-tools — found via REBORN_TOOL_DISCLOSURE=Bridged testing | Open, no fix PR |
| **Medium** | `#5640` | Harness gap: `hook_security_audit_sink` always `None` in integration harness, production uses `TracingSecurityAuditSink` | Open, upstream of wiring-parity guard #5637 |
| **Low** | `#5641` | `EXPECTED_PRODUCTION_SHAPE` hand-derived — needs production-side accessor to prevent silent drift | Open, identified in #5637 follow-up |
| **Low** | `#4108` | Nightly E2E failing since May 27 (stale, 39 days open) | Open, root cause unknown |
| **Closed** | `#5590` | Main branch CI checks not green across workflows — sampled failures include code style, live QA | Closed (resolved) |

The wiring-parity guard `#5637`/#5642 is a systematic fix: it will catch production/harness shape drift at test time rather than relying on manual transcription.

## Feature Requests & Roadmap Signals

- **Slack personal OAuth** — Four-PR stack ready: foundations (#5644), swap (#5645), CLI config rejection (#5646), JS CI (#5643). Likely to land early next week.
- **Coverage ratcheting** — `#5638` asks to flip integration coverage from informational to a hard ratchet (fail CI when coverage drops). A coverage-exemptions list and explicit crate thresholds must be seeded.
- **Manifest-driven ingress** — `#5626` projects Slack routes from manifest instead of hand-written Rust policy. Pattern could extend to other channel providers.
- **Error recoverability audit** — `#5651` and `#5652` implement compile-time enforcement from `#5383`'s remediation plan. Likely to land next release cycle.
- **Final-answer nudge** — `#5304` enables synthesized closing answers for interactive runs. Small, low-risk, could ship quickly.
- **Subagent spawn fix** — `#5170` adds `LoopInlineMessageBody` validation. Critical for subagent reliability; open since June 23.

**Prediction for next version (post-0.29.x):** Slack OAuth complete migration, coverage ratcheting active, error-swallowing compile-time enforcement, manifest-driven ingress for Slack.

## User Feedback Summary

No direct user-submitted issues or feature requests in today's data. All activity is internal/developer-driven. The Slack OAuth work (#5644, #5645, #5646) suggests an enterprise/team-use-case need: per-user revocable tool identity with granular scope control (`read` vs `chat:write`). The CI reliability issues (#5636, #5590) indicate developer frustration with flaky deployment pipelines—Railway blocking on skipped jobs is a recognizable pain point for any team with conditional CI workflows. The nightly E2E failure (#4108, open 39 days) represents a silent stability risk that has not yet been prioritized.

## Backlog Watch

| Issue/PR | Age | Problem | Status |
|----------|-----|---------|--------|
| `#4108` Nightly E2E failure | 39 days (May 27) | Scheduled runs failing silently | No assignee, no fix |
| `#5170` Subagent spawn fix | 12 days (Jun 23) | Subagent tasks/handoffs fail | Open, under review |
| `#5550` Dependabot bulk update | 3 days (Jul 2) | 13 bumps including `agent-client-protocol` 0.10.4→1.0.1 | Open, no merge |
| `#5304` Final-answer nudge | 9 days (Jun 26) | Interactive runs can end empty | Open, under review |

The nightly E2E failure (#4108) is the most concerning backlog item—39 days without resolution for a scheduled reliability check suggests either low priority or complex root cause. The subagent spawn fix (#5170) has been open for 12 days and is critical for subagent task reliability.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-05

## Today's Overview
Activity was moderate today with 3 PRs updated and 1 issue updated, but no new releases. Two PRs were merged/closed, focusing on critical bug fixes and documentation cleanup, while one longstanding open issue remains active. The project appears to be in a stabilization phase with no new features shipped. Community discussion is low overall, though a few older issues are receiving updates, indicating some lingering pain points.

## Releases
None.

## Project Progress
Two pull requests were merged/closed today:
- **PR #2272** (closed) — *fix(agent): migrate legacy AGENTS.md identity blocks to IDENTITY.md*  
  Detects and removes legacy identity content from `AGENTS.md` to avoid conflicts with the managed `IDENTITY.md` file. Includes backup and safe failure reporting per agent.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/2272)
- **PR #2271** (closed) — *fix: propagate system proxy to managed browser*  
  Ensures that system-level proxy settings are correctly forwarded to the managed browser instance, improving network compatibility.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/2271)

## Community Hot Topics
The most active discussion is on **Issue #1352**:
- **Issue #1352** — "任务对话框，任务运行中，附件无法上传（点击上传附件无反应）" — Updated 2026-07-04, 1 comment  
  Reports that during a running task, the attachment upload button fails to respond. Likely a UI interaction blocking bug.  
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1352)

This issue has been stale for several months but was recently re-updated, suggesting users are still encountering the problem. The lack of reactions or detailed reproduction steps limits impact assessment.

## Bugs & Stability
One bug was actively discussed today:
- **Issue #1352** — **[Stale, Severity: Medium]** Attachment upload fails when task is running. No error feedback visible.  
  No fix PR is linked yet. The bug is user-reported and has been re-updated after a long period of inactivity.

**PR #1350** (still open) also describes a related stability issue:
- **PR #1350** — **[Severity: High]** Skills file generation blocks indefinitely with no progress feedback; same model shows inconsistent behavior across LobsterAI and OpenClaw. This implies a deeper logic issue in the task pipeline or model interface.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1350)

## Feature Requests & Roadmap Signals
No explicit feature requests were filed in the last 24h. However, **Issue #1350** implicitly requests:
1. Progress indicators or intermediate status display during long-running `skills` generation tasks.
2. Cross-model consistency — users expect same model to produce same results in both LobsterAI and OpenClaw.

These may become higher priority if user complaints persist in upcoming releases.

## User Feedback Summary
- **Pain points**: Users report task progress invisibility and model response inconsistency — leading to confusion about whether the system is still working.
- **Use cases**: Primarily `skills` generation, file attachment during tasks, and proxy/browser configuration for managed browsing.
- **Satisfaction**: Mixed — recent proxy fix (PR #2271) addresses a specific connectivity complaint, but long-standing UX issues (e.g., hidden generation state) remain unaddressed.
- **Dissatisfaction**: No way to monitor or cancel blocking operations; missing feedback loops.

## Backlog Watch
Two items require maintainer attention due to age and recent updates:
- **Issue #1352** — Open since 2026-04-02, updated 2026-07-04. Attachment upload blocked during task mode. Lacks response or fix assignment.  
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1352)
- **Issue/PR #1350** — Open since 2026-04-02, updated 2026-07-04. Describes a serious stability and consistency bug in skills generation. No merged fix yet.  
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1350)

Both are stale for ~3 months and could benefit from a maintainer response or reproduction triage.

---

**Overall assessment**: Project health is stable but quiet — two important fixes were merged today, but unresolved UX bugs and a lack of progress visibility remain key community concerns. No new releases suggest the team is focusing on maintenance and internal stability rather than feature expansion.

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

Here is the **CoPaw Project Digest** for **2026-07-05**.

---

## CoPaw Project Digest – 2026-07-05

### 1. Today's Overview
The project experienced moderately high activity today, with 11 Issues and 3 PRs updated in the last 24 hours. However, only 2 Issues were resolved, while the remaining 9 remain open. No new releases were published. The focus of the community remains on debugging the `2.0.0b3` pre-release and addressing a critical regression in the Auto-memory and Scroll compression systems. A significant new PR (#5777) aims to fix the core state-loss issue in the Memory middleware, indicating a proactive maintenance cycle.

### 2. Releases
**None.** No new versions were released in the last 24 hours. The latest major version remains `2.0.0b3`.

### 3. Project Progress
No Pull Requests were merged or closed today. However, one significant PR is actively open and moving toward integration:
- **PR #5777 (feat/memory)**: Addresses the "auto-memory interval never triggers" bug by adding turn-state management to `BaseMemoryManager`. This is a critical fix for the `2.0.0b3` regression.

### 4. Community Hot Topics
- **Memory & Context Loss (#5775, #5778):** The most heated discussion revolves around the `2.0.0b3` pre-release. Two related bugs are causing severe user dissatisfaction:
    - **#5775**: Auto-memory never triggers because state is lost across requests. Users report that long-running sessions lose context entirely.
    - **#5778**: The new "Scroll" compression strategy destroys context, causing models to "forget" the task and produce off-track responses.
    - *Analysis:* The underlying need is **reliable long-term memory**. Users expect AI agents to maintain coherent, persistent context across sessions. The transition from "native" to "scroll" compression has broken this trust.
- **Stale Context in IM Sessions (#5776):** A user reports that in QQ/IM, a pin message from June 28 was still treated as the current task on July 3, highlighting a critical flaw in context window management for social platforms.

### 5. Bugs & Stability
**Severity: High.**

- **Memory State Loss (Severity: Critical)** [#5775](https://github.com/agentscope-ai/QwenPaw/issue/5775)
    - *Problem:* Auto-memory never triggers in `2.0.0b3` because `MemoryMiddleware` state is lost during agent rebuild.
    - *Status:* Open. Fix PR #5777 is open and targets this exact issue.
- **Scroll Compression Context Loss (Severity: Critical)** [#5778](https://github.com/agentscope-ai/QwenPaw/issue/5778)
    - *Problem:* The "scroll" compression strategy causes severe context loss, leading to garbled responses. It also breaks `reasoning_content` for thinking models.
    - *Status:* Open. No fix PR yet.
- **Cron API Timezone Bug (Severity: Medium)** [#5779](https://github.com/agentscope-ai/QwenPaw/issue/5779)
    - *Problem:* `last_run_at` / `next_run_at` hardcoded to UTC, ignoring job timezone.
    - *Status:* Open. Root cause identified (line 566 in `manager.py`).
- **HTTP 400 Cache Poisoning (Severity: Medium)** [#5772](https://github.com/agentscope-ai/QwenPaw/issue/5772)
    - *Problem:* `_is_bad_request_or_media_error()` incorrectly marks all HTTP 400 errors as media rejection, poisoning the capability cache.
    - *Status:* Closed. Fix implemented.
- **Log Spam & Channel Errors (Severity: Low/Medium)** [#5774](https://github.com/agentscope-ai/QwenPaw/issue/5774), [#5771](https://github.com/agentscope-ai/QwenPaw/issue/5771)
    - *Problem:* Log spam from `model_factory.py` and a specific error with Google Gemini channel.
    - *Status:* Open. Easily reproducible.

### 6. Feature Requests & Roadmap Signals
- **QwenPaw 2.0 Anticipation (#5770):** A community member expressed high hopes for the official `2.0` release. This signals strong platform dependency on the stability of the new architecture.
- **System Tray/Hidden-to-Tray Feature (#2830):** A long-standing request to add a "minimize to system tray" option for the desktop client was closed today. This is a sign that the development team is cleaning up old, minor feature requests, likely focusing on core stability before adding UX polish.
- **PRs Ready for Merge:** The three PRs (#5597, #5598, #5597) related to **LLM fallback configuration** (backend + UI) are all open and waiting. These are likely to land in the next minor release (`2.0.0b4` or `1.1.13`).

### 7. User Feedback Summary
- **Frustration:** Users of the `2.0.0b3` pre-release are frustrated by the memory/context regression. The experience is described as "the model forgets the task and acts like a different person."
- **Satisfaction:** There is quiet satisfaction regarding the direction of `2.0`, but it is contingent on these stability fixes.
- **Tension:** There is a clear tension between the "new scroll compression" strategy and the "low version (native) strategy." Users are asking for the option to disable compression if it breaks functionality.

### 8. Backlog Watch
- **Issue #2865 (Feature - Custom Agent Avatars):** Created in April 2026, updated recently but with no milestone. While not critical, this is a UI/UX quality-of-life feature that has been sitting for over 3 months.
- **PRs #5597 & #5598 (LLM Fallback):** These have been open since June 29. They are substantial backend + UI changes that are awaiting final review or merge. They represent a significant improvement to reliability (fallback on model failure) and should be prioritized for integration.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-05

## Today's Overview

ZeroClaw remains in an intense development sprint toward v0.8.3, with **50 active issues** and **50 pull requests** updated in the past 24 hours. Maintainer activity is extremely high, driven primarily by the **goal-mode implementation split stack** (#8681) and the **SOP engine expansion** (#8590). The project is shipping new feature PRs at a rapid cadence, but the bug tracker shows concerning **S1 (workflow-blocked) issues** around runtime panics (#8654) and security bypasses (#8678) that have not yet been resolved. The **v0.8.3 release candidates** are clearly in active preparation, with three dedicated tracker issues (#8360, #8071, #8073) coordinating the effort. **No new releases were cut today.**

## Releases

No new releases were published on 2026-07-05. The project appears to be in a pre-release stabilization phase for v0.8.3.

## Project Progress

**Merged/closed PRs today: 2**
- No specific merged PRs are listed among the top 20 by comment count, suggesting today's merged items were smaller fixes not captured in the high-traffic set.

**Major feature advances visible in open PRs:**
- **Goal-mode system** (vrurg): Three stacked PRs — #8689 (goal command admission across channels), #8688 (trusted goal tools with delegation boundaries), #8687 (goal controller/verifier with cost attribution) — represent a **large coordinated feature landing** touching agent, channel, runtime, and daemon layers.
- **SOP visual authoring** (PR #8590, singlerider): A massive XL-sized PR adding visual SOP editing surfaces with channel fan-in, CI tests, and documentation. Now calling for beta testers.
- **OpenAI-compatible bridge channel** (PR #8710, titilambert): Adds OpenAI-format HTTP endpoints exposing models and chat completions, enabling Home Assistant / third-party tool integration.
- **Context window usage bar** (PR #7946, eugeneb50): Adds model context window visualization to all chat surfaces (TUI, gateway, CLI).
- **cron uses_memory flag** (PR #8676, databillm): Exposes the existing `uses_memory` flag through CLI tools and gateway API.
- **Anthropic refusal handling** (PR #8721, IftekharUddin): Detects Claude 4+ safety refusals that return HTTP 200 with empty content, forwarding as a proper error.
- **Gitea/Forgejo forge provider** (PR #8611, Nillth): Second of three stacked PRs adding Git forge channel support.

## Community Hot Topics

**#8193 — MCP tools/TUI session disconnect** (CLOSED, 15 comments)
*URL: https://github.com/zeroclaw-labs/zeroclaw/issues/8193*
The most-discussed issue: MCP servers connect and expose tools to the gateway, but TUI sessions don't receive them. This was a **workflow-blocking S1** that has now been closed, suggesting a fix was shipped.

**#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup** (OPEN, 13 comments)
*URL: https://github.com/zeroclaw-labs/zeroclaw/issues/6808*
A governance RFC from May that remains active with 13 comments. Proposes routing automation, label standardization, and multi-lane boards. This is a maintainer-facing meta-process discussion, not a feature request.

**#8681 — Goal mode implementation split stack tracker** (OPEN, 7 comments)
*URL: https://github.com/zeroclaw-labs/zeroclaw/issues/8681*
The coordination point for splitting the goal-mode feature into reviewable PRs. With 7 comments in a single day, this is the hottest active tracker.

**#6361 — context_compression drops tool_calls for OpenAI-compatible providers** (CLOSED, 5 comments)
*URL: https://github.com/zeroclaw-labs/zeroclaw/issues/6361*
Addressed a critical bug where context compression was stripping tool call/result messages entirely for providers like MiniMax, causing infinite loops. Now closed.

**#8654 — skill-review fork panics with out-of-range slice → daemon SIGSEGV** (OPEN, 2 comments)
*URL: https://github.com/zeroclaw-labs/zeroclaw/issues/8654*
A **critical S1** runtime panic that takes down the whole agent process (exit code 139/SIGSEGV) after tool-heavy turns. Severity escalation is likely needed — this is a crash, not just degraded behavior.

*Underlying needs analysis:* The community is split between (1) power users hitting real stability problems (MCP tool visibility, runtime panics, provider serialization bugs) and (2) maintainers coordinating a massive v0.8.3 feature drop (goal-mode, SOP authoring, new channels). The comment patterns show maintainers (Audacity88, vrurg, singlerider) are extremely responsive, often closing issues the same day they're reported.

## Bugs & Stability

### Critical (S1 — workflow blocked)
| Issue | Component | Status | Fix PR? |
|-------|-----------|--------|---------|
| #8654: skill-review fork panics → SIGSEGV | runtime/skills | OPEN, in-progress | Not yet identified |
| #8678: SOP advance_step has no run-status guard → bypass approval gates | runtime/daemon (SOP) | OPEN, accepted | Not yet identified |
| #8675: Malformed native tool-call arguments sent unvalidated → provider 400 → empty reply | provider/OpenAI-compat | OPEN, accepted | Not yet identified |
| #8193: MCP tools missing from TUI sessions | zerocode/tui | **CLOSED** (fixed) | Shipment confirmed |

### High (S2 — degraded behavior)
| Issue | Component | Status | Details |
|-------|-----------|--------|---------|
| #8695: Cron jobs recall memory despite uses_memory=false | memory | OPEN, in-progress | Stateless scheduled runs bypassed; fix PR #8676 exists |
| #8664: ZeroCode code-block Copy includes Markdown fences | zerocode/tui | OPEN, accepted | UX polish issue |
| #8646: ZeroCode Logs detail hides event attributes | zerocode/tui | OPEN, accepted | UX polish issue |
| #8644: ZeroCode completes Code turn with no visible output | zerocode/tui | OPEN, accepted | UX/interaction bug |
| #8615: Compatible provider silently deletes content via `<think>` tag stripping | provider | OPEN, accepted | Silent content loss |
| #8722: High-entropy detector redacts legitimate filenames | security/sandbox | OPEN (today) | Fix PR #8723 submitted same day |
| #7862: Empty tools list with tool_choice=auto → vLLM HTTP 400 | provider/compat | CLOSED | Fixed |
| #8359: Memory embeddings don't refresh provider profile changes | memory/config | CLOSED | Fixed |

### Medium (S3 — uneven localization / minor)
| Issue | Component | Status |
|-------|-----------|--------|
| #8587: Adding more SOP examples to docs | docs/sop | OPEN, accepted |
| #7917: file_download tool strings untranslated | runtime/i18n | CLOSED |

## Feature Requests & Roadmap Signals

**Likely for v0.8.3 (based on active trackers #8360, #8071, #8073, #7314):**
- **Goal-mode execution** — coordinated in #8681, PRs #8687/#8688/#8689. User-controlled goal admission with budget, pause/resume, and verifier gates.
- **Visual SOP authoring** — PR #8590, adding a graphical editor for SOPs with channel fan-in for approval workflows.
- **OpenAI-compatible bridge channel** — PR #8710, exposing agents as OpenAI-compatible endpoints.
- **New forge provider (Gitea/Forgejo)** — PR #8611, adding self-hosted Git forge support.
- **WASM plugin program** — tracker #7314 continues, though no new plugin PRs were updated today.
- **Turn-level OTel trace correlation** — #6641 accepted, with PR likely in preparation.

**Future roadmap signals:**
- **OCI registries for WASM plugins** (#7497, RFC, blocked): A proposal to replace JSON index files with OCI-compliant container registries for plugin distribution. This is a big architectural shift — watch for it in v0.9 or later.
- **SOP routing — false `when` fallthrough** (#8719, new today): User requests that multi-phase SOPs allow a false condition to advance to the next step rather than ending the run.
- **LeakDetector disable config** (#4832, accepted since March): User request for a config option to disable high-entropy token redaction. Despite being accepted, no PR has shipped — it may be a candidate for v0.8.3 if #8722 (today's false positive bug) drives urgency.

## User Feedback Summary

**Pain points (explicit user reports):**
- *"MCP tools connect and expose but TUI sessions don't receive them"* — #8193 (now fixed)
- *"Cron jobs with uses_memory=false still recall memory"* — #8695: A user reports the flag is documented but doesn't actually work; fix is in review
- *"I am trying to use Bedrock Nova 2 Lite but getting a caching error I cannot disable"* — #8720: A user wants a config file knob to disable cachePoint
- *"SOP routing false when ends the run instead of advancing"* — #8719: Multi-phase SOPs are unusable without proper fallthrough
- *"SOP syntax has no detailed examples"* — #8587: Documentation gap for an otherwise well-received feature
- *"vLLM HTTP 400 with empty tools list"* — #7862: Provider-specific breakage with spec-compliant backends

**Satisfaction signals:**
- High maintainer responsiveness: bugs are being closed same-day (e.g., #8193, #6891, #8359)
- Beta tester call for SOP visual authoring (#8590) suggests user engagement is being sought early
- The goal-mode system has enough community trust for maintainer vrurg to land three stacked PRs totaling thousands of lines

## Backlog Watch

**Issues needing maintainer attention:**
- **#4832** (March 27): "Add config option to disable LeakDetector high-entropy token redaction" — **accepted status since March, no PR**. Today's #8722 (false positive bug) and its companion fix PR #8723 renew urgency. This should be reopened for prioritization.
- **#7497** (June 11): "OCI-Compliant Container Registries as Plugin Storage" — blocked RFC with high risk. No maintainer reply since opening. With WASM plugin program (#7314) being an active v0.8.3 tracker, this RFC deserves a status update.
- **#6717** (May 16): "Integrate arch-review artifact into PR review session" — skill enhancement PR that hasn't received a maintainer review in 50 days.

**PRs needing review:**
- **#8710** (titilambert): OpenAI channel — large XL PR with the `needs-maintainer-review` label. This could unblock significant third-party integrations but hasn't been reviewed yet.
- **#8546** (ConYel): CLI localization — small S-sized fix that's been waiting since June 30. Low risk, should be quick to merge.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*