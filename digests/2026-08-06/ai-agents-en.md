# OpenClaw Ecosystem Digest 2026-08-06

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-06 01:16 UTC

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

Based on the GitHub data for OpenClaw (github.com/openclaw/openclaw) on 2026-08-06, here is the project digest:

---

## OpenClaw Project Digest: 2026-08-06

### 1. Today's Overview
OpenClaw remains a highly active project with a significant volume of community engagement. The triage and maintainer team processed a heavy load of over 500 issues and 500 PRs updated in the last 24 hours. A concerning high number of these issues (443) remain open, indicating a substantial backlog and sustained pressure on maintainers, despite a healthy stream of 57 closures. Activity is centered on addressing critical stability bugs (P0/P1), particularly around session state management, message delivery, and provider auth, with many issues tagged as `needs-maintainer-review` and `needs-product-decision`. While no new releases were published today, the volume of linked PRs and active triage suggests a large, imminent release or a period of intense stabilization.

### 2. Releases
No new releases were published in the last 24 hours.

### 3. Project Progress
While no releases were cut, several pull requests were merged or closed, indicating progress on important fixes and internal processes.

- **Bug Fixes & Enhancements (Merged/Closed):**
    - **Core Stability:** A long-standing issue [#92369](https://github.com/openclaw/openclaw/issues/92369) regarding subagent orchestration in cron isolated sessions was closed as `already-fixed`.
    - **Critical Data-Loss Fix:** A P0 issue, [#119090](https://github.com/openclaw/openclaw/issues/119090), involving permanent deletion of media due to a failure in cleanup logic, was closed with a fix likely identified.
    - **Feature Completion:** A PR for a new OTel root span trace context, [#112278](https://github.com/openclaw/openclaw/issues/112278), was closed after a linked PR was merged.
    - **Developer Experience:** A release-blocking auto-fix PR, [#118796](https://github.com/openclaw/openclaw/pull/118796), which required a real context snapshot for CLI usage, was closed as superseded by a more comprehensive fix.

### 4. Community Hot Topics
The most active discussions revolve around session-state corruption and data loss, highlighting major user pain points.

- **[#116201](https://github.com/openclaw/openclaw/issues/116201) (59 comments):** A P1 bug detailing unbounded state retention in realtime voice work, causing resource leaks and instability. The high comment count indicates significant user impact and a complex debugging process.
- **[#7707](https://github.com/openclaw/openclaw/issues/7707) (27 comments):** A long-standing (since February) feature request for Memory Trust Tagging by source. The community is actively discussing this security enhancement, pushing for protection against memory poisoning attacks.
- **[#44925](https://github.com/openclaw/openclaw/issues/44925) (25 comments):** A critical bug where subagent completions are silently lost with no retry or notification. This erodes user trust in automation and is a top priority for improvement.
- **Duplicate Message Regressions:** Issues about the agent repeating replies on Telegram ([#86519](https://github.com/openclaw/openclaw/issues/86519), 13 comments) and QQ ([#77306](https://github.com/openclaw/openclaw/issues/77306), 6 comments) continue to be hot topics, indicating a systemic issue with message delivery after the 5.20 update.

### 5. Bugs & Stability
The project is facing a significant number of high-severity bugs, with the most critical being:

- **P0 - Release Blockers:**
    - **[#119263](https://github.com/openclaw/openclaw/issues/119263):** Agent DB v14->v15 migration fails on `entry_valid` column, preventing the gateway from starting. A critical upgrade blocker with a linked PR open.
    - **[#70903](https://github.com/openclaw/openclaw/issues/70903):** Persistent provider cooldown blocks users for hours even after billing recovery. A long-standing P0 issue still without a fix PR.
    - **[#119090](https://github.com/openclaw/openclaw/issues/119090):** (Closed) Managed media cleanup fails open, permanently deleting session data.

- **P1 - Critical Session/Messaging Failures:**
    - **[#44925](https://github.com/openclaw/openclaw/issues/44925):** Silent loss of subagent completion results.
    - **[#85251](https://github.com/openclaw/openclaw/issues/85251):** Codex app-server goes silent, wedging sessions for 6 minutes.
    - **[#118846](https://github.com/openclaw/openclaw/issues/118846):** Gateway main thread saturated by plugin-metadata snapshot, killing local RPC. (Closed).
    - **[#116022](https://github.com/openclaw/openclaw/issues/116022):** `/new` command fails to recover a retired Codex binding tombstone, leaving sessions permanently unusable.

### 6. Feature Requests & Roadmap Signals
Several issues point towards upcoming features and enhancements:

- **Security & Trust:** The push for **Memory Trust Tagging by Source** ([#7707](https://github.com/openclaw/openclaw/issues/7707)) and **labeling voice transcripts as untrusted** (PR [113111](https://github.com/openclaw/openclaw/pull/113111)) signals a strong roadmap focus on security and mitigating prompt-injection-like risks.
- **Platform Reliability:** There is a repeated request for a comprehensive **AWS deployment guide** ([#13597](https://github.com/openclaw/openclaw/issues/13597)), which could signal a growing push for enterprise cloud adoption.
- **Session & Context Management:** The desire for **loop-aware compaction guards** ([#48238](https://github.com/openclaw/openclaw/issues/48238)) and fixes for **session context bloat** ([#67419](https://github.com/openclaw/openclaw/issues/67419)) points to a focus on optimizing long-running session efficiency.

### 7. User Feedback Summary
- **Pain Points:** Users are frustrated by silent failures, such as lost subagent results ([#44925](https://github.com/openclaw/openclaw/issues/44925)) and undelivered messages ([#96692](https://github.com/openclaw/openclaw/issues/96692)). The `clawsweeper` bot seems to have a large backlog of issues needing `product-decision`, indicating that maintainers are finding it difficult to resolve issues without further product input.
- **Language Barriers:** The presence of issues in Chinese (e.g., [#51429](https://github.com/openclaw/openclaw/issues/51429), [#77306](https://github.com/openclaw/openclaw/issues/77306)) indicates a global user base, and bug reports are being translated.
- **Satisfaction:** Users express dissatisfaction with regressions, particularly the duplicate message bugs on Telegram ([#86519](https://github.com/openclaw/openclaw/issues/86519)) and Discord ([#77930](https://github.com/openclaw/openclaw/issues/77930)) which broke previously working functionality.

### 8. Backlog Watch
These items are flagged for maintainer attention due to their high priority and unresolved status.

- **[#51429](https://github.com/openclaw/openclaw/issues/51429) (P2):** A hardcoded user home directory path (`/Users/wangtao`) was merged and released. This is a severe code-quality and security issue that has been open for 5 months with 12 comments, yet still requires a decision.
- **[#113306](https://github.com/openclaw/openclaw/issues/113306) (P1):** SQLite snapshot restore lacks end-to-end crash and identity guarantees. A critical data-integrity concern for backups.
- **[#97616](https://github.com/openclaw/openclaw/issues/97616) (P1):** Leaking unreaped hook/tool child processes, leading to zombie accumulation and runtime degradation over time.
- **[#53540](https://github.com/openclaw/openclaw/issues/53540) (P1):** Embedded runner fails with "Network connection lost" on large tool calls, a frustrating limit on agent capability.
- **[#46031](https://github.com/openclaw/openclaw/issues/46031) (P2):** The `auth.order` setting is ignored for the GitHub Copilot provider. An outstanding auth-parity gap.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: AI Agent & Personal Assistant Open-Source Ecosystem
**Date:** 2026-08-06

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape continues to broaden and differentiate. The core reference project, **OpenClaw**, is under heavy load, processing 500+ issues/PRs daily, with a substantial backlog of 443 open issues—signaling both widespread adoption and maintainer strain. Meanwhile, a dynamic tier of actively developing projects (**IronClaw**, **ZeroClaw**, **CoPaw**, **Hermes Agent**) demonstrates high-velocity iteration around channel reliability, MCP integration, and session-state integrity. A maturation trend is evident: many projects are shifting focus from foundational feature builds to robustness, security hardening, and enterprise-grade concerns (auth, observability, config-as-code). Cross-cutting requirements such as memory integrity against attacks, model fallback chains, and self-healing channel supervision are emerging across multiple codebases. The ecosystem is consolidating around **MCP as a universal tool standard**, while confidence-based agent behavior (e.g., *not* hallucinating state) is becoming a critical quality bar. Several smaller projects sit in maintenance mode (PicoClaw, NullClaw, TinyClaw, Moltis, ZeptoClaw), representing a long tail of specialist or dormant efforts.

---

## 2. Activity Comparison

| Project | Issues (24h Update / Open) | PRs (24h Update / Open) | Releases (24h) | Health Score (1–5) | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 500+ updated / **443 open** | 500+ updated / ~50+ open | None (recent large release) | **2.5** | Overwhelmed backlog; critical P0/P1 bugs active; high volume, slow closure |
| **IronClaw** | 43 updated / 10 closed | 50 updated / 20 merged | `v1.1.0-rc.1` (3 days ago) | **4.0** | Healthy velocity; bug-bash QA cycle; release candidate hardening |
| **ZeroClaw** | 50 updated / ~40 open | 50 updated / 15+ open | None (v0.8.5 line, intake frozen) | **3.5** | Maintainer-constrained; RFC queue backlog; strong security work |
| **CoPaw** | 75 updated / ~30 open | 75 updated / ~30 open | None (v2.0.1, v2.1.0-beta out) | **3.5** | High velocity; β-regression wave; responsive triage |
| **Hermes Agent** | 50 updated / 50 open | 50 updated / 50 open (0 merged) | None | **3.0** | Review bottleneck; epic refactoring; active feature campaigns |
| **NanoBot** | 4 tracked open | 8 merged / 8 open | None | **4.0** | Healthy, small scale; consistent feature/bug-fix pipeline |
| **NanoClaw** | 2 open (both stale) | 12 updated / 10 open | None | **3.0** | Contributor-friendly; stale issues remain; skill ecosystem growing |
| **NullClaw** | 0 open | 2 open (1 day old) | None | **4.0** | Stable, small; proactive bug fixing; low community volume |
| **PicoClaw** | 0 new (0 open) | 4 updated / 3 open | None | **3.5** | Mature; quiet; one long-pending PR merged today |
| **LobsterAI** | ~3 active | 13 updated / 12 merged | **2026.8.5** (yesterday) | **4.0** | High closure rate (92%); new UX holes (#2440/#2441) |
| **TinyClaw / Moltis / ZeptoClaw** | 0 | 0 | None | 2.0 | Dormant/inactive |

---

## 3. OpenClaw's Position

**Advantages:**
- **Massive community mindshare** — The scale of daily interaction (500+ issues/PRs) makes it the de facto reference implementation and the largest contributor base in the ecosystem. It's the project others measure against (e.g., CoPaw explicitly compares to OpenClaw gateways).
- **Deep platform coverage** — Active fixes span Telegram, Discord, QQ, Matrix, Codex, and more, showing an unmatched breadth of channel integrations.
- **Fast critical-fix turnaround** — Despite backlog, the team closes P0 data-loss and migration-blocker bugs responsively (e.g., #119090, #92369).

**Technical Approach:**
- OpenClaw relies on a **plugin/metadata-snapshot** architecture that, while flexible, is creating systemic performance issues (e.g., main-thread saturation from plugin-metadata snapshots, #118846). This is a key differentiator vs. younger projects that build on smaller, cleaner cores (e.g., NanoBot, NullClaw).
- Uses **cron-isolated sessions** and **subagent orchestration** for multi-tenant workflows.

**Community Size Comparison:**
- OpenClaw's issue volume is roughly 10–15× that of its nearest peers (ZeroClaw, CoPaw, Hermes each hover around 50/day). This suggests a large install base, but also a **signal-to-noise problem**: 443 open issues with 57 closings/day indicates a widening gap. The volume of issues tagged `needs-product-decision` shows the maintainers are struggling to keep up with demand for product-level direction.

**Strategic Advice:** OpenClaw's leadership position is secure, but its advantage is eroding as users express frustration with regressions and unresolved long-standing bugs (e.g., duplicate message regressions, provider cooldown #70903). The next 6 months are critical for the team to shift from feature velocity to **stability and backlog reduction**, or risk losing power users to cleaner, more reliable alternatives like IronClaw or ZeroClaw.

---

## 4. Shared Technical Focus Areas

**Requirements emerging across multiple projects:**

| Trend | Projects | Specific Needs (Quotes from data) |
|---|---|---|
| **Session-state integrity / data-loss prevention** | OpenClaw, Hermes, IronClaw, CoPaw | "Silent loss of subagent completion results"; "Agent DB v14→v15 migration fails"; "SessionDB WAL reader accumulation"; "Fresh-tail context overflow retry loops" |
| **Memory & trust / security hardening** | OpenClaw, ZeroClaw, IronClaw | "Memory Trust Tagging by source"; "Label voice transcripts as untrusted"; "Verifiable-intent evaluates constraints without verifying credential chain"; "Agent hallucinates automation status" |
| **MCP integration robustness** | NanoBot, CoPaw, NanoClaw, IronClaw | "MCP tool returns 'data not found' envelope"; "MCP Tools Fail Periodically (not registered)"; "MCP servers don't inherit HTTPS_PROXY/CA-trust"; "Agent guesses MCP Auth Type" |
| **Channel reliability (silent drops, retry)** | NullClaw, CoPaw, ZeroClaw, OpenClaw | "Channel pollers silently die after idle periods"; "Matrix connects faster than service, no retry"; "Silently drops inbound Signal envelopes wh. sourceUuid-only"; "Undelivered messages" |
| **Model fallback chains / routing** | CoPaw, PicoClaw, OpenClaw (implied) | "Request automatic model routing"; "Configurable default fallback chain for models"; "Persistent provider cooldown blocks users for hours" |
| **Config/UX reliability** | LobsterAI, ZeroClaw, Hermes | "openclaw.json being overwritten wholesale"; "config set rejected cron keys with hyphens"; "Provider/model switching quirks lose provider on resume" |
| **God-file sharding / maintainability** | Hermes, IronClaw, ZeroClaw | "Shard all 20 god files"; "Extract Gateway Platform Routing from run.py" (858KB) |

---

## 5. Differentiation Analysis

| Project | Feature Focus | Target Users | Technical Architecture |
|---|---|---|---|
| **OpenClaw** | Breadth-first: everything for everyone; heavy platform/channel integration | General users, hobbyists; enterprise pilots | Large, plugin-heavy binary; cron-isolated session architecture; metadata-snapshot overhead |
| **IronClaw** | "Reborn" architecture; skills ecosystem, MCP customization, WebUI; config-as-code | DevOps and enterprise pilots; developers | Host-owned standardized messaging framework; sandboxing; web-driven management, design-system investment |
| **ZeroClaw** | Security-first: RBAC, OAuth, shell policy, forbidden paths, verifiable intent | Security-conscious operators; self-hosters | Rust-based (gateway); RFC-driven governance; strict stabilization cycles; contributor-role taxonomy |
| **CoPaw** | Desktop-first, cross-platform; agent orchestration, artifacts canvas; Chinese user base | Desktop power users; WeChat users (China) | Qt-like desktop shell; console, cowork apps; browser SDK; Windows/WebView integration; active bug-bash on β |
| **Hermes Agent** | Platform parity (Telegram Bot API 10.2), repo-scale hygiene, state-risk mitigation | Developers running multiplexed fleets; API-parity-sensitive ops | God-file decomposition; sweeper-risk labeIing; TUI/desktop sessions |
| **NanoBot** | Lightweight, fast channel integration (WhatsApp/Matrix/Mattermost); WebUI simplicity | Individuals and small teams; quick deploys | Go-based (implied), compact core, MCP-app rendering ambition |
| **NullClaw / PicoClaw** | Runtime stability; provider auth (Anthropic OAuth); channel poller supervision | Advanced self-hosters; minimalists | Small codebase, reactive bug fixing |
| **LobsterAI** | Enterprise auth isolation; daily check-in campaigns; NIM/SuperTeam | Enterprise users; Chinese enterprise community | Desktop-frontend heavy (renderer/cowork); relies on OpenClaw gateway |
| **NanoClaw** | Community-skill focus (Tavily, Dial, why); architectural correctness (single-writer) | Contributors; community-driven skill builders | Lightweight container approach, host seams for skill-owned capabilities |

---

## 6. Community Momentum & Maturity

**Tier 1: High-Velocity, Actively Shipping**
- **IronClaw** — Rapid iteration on the Reborn architecture, with an RC out and a defined roadmap. Healthiest development loop (10 issues closed, 20 PRs merged in 24h).
- **CoPaw** — Extremely active (75 updates/day), fast fix turnaround, but beta-quality desktop experience currently in flux. Growth likely to continue post-v2.1.0-stable.
- **LobsterAI** — Shipping stable releases weekly; high PR closure rate (92%); but new external-facing bugs emerging means the bar is rising.

**Tier 2: Busy but Bottlenecked**
- **OpenClaw** — Highest raw activity, but 443 open issues and closure rates not keeping pace. Visibility is high, but risk of contributor fatigue and user churn.
- **ZeroClaw** — Active, security-driven, but maintainer-constrained. The decision queue (#8692) is the critical bottleneck; if decisions flow, this project could accelerate quickly.
- **Hermes Agent** — Very active repo, but zero merges in 24h indicates a review bottleneck. Epic refactoring is in-flight, which will pay dividends, but contributors may grow frustrated.

**Tier 3: Steady, Low-Key, or Specialized**
- **NanoBot, NanoClaw, NullClaw, PicoClaw** — Smaller communities, healthy for their size. NanoClaw shows strong community contribution (skill PRs), but stale issues signal a support gap. NullClaw is tiny but responsive.

**Tier 4: Dormant** — TinyClaw, Moltis, ZeptoClaw (no activity for 24h; likely stagnant).

---

## 7. Trend Signals

**High-Value Trends for AI Agent Developers:**

1. **The "honest agent" bar is rising.** Multiple projects (IronClaw P1s, ZeroClaw verifiable intent) are being pushed to eliminate agent hallucination of system state—whether it's inventing automation status, falsely claiming connections, or delivering wrong-channel results. Trust in agent reporting is now a competitive differentiator.

2. **Session-state management is the new frontier.** With long-running, always-on agents, the failure modes are performance (context bloat, WAL leaks, resource growth) and correctness (silent loss, stale state). Developers who crack durable, self-healing session management will have a significant edge.

3. **Security is becoming first-class, not an afterthought.** The volume of security-specific RFCs (shell policies, forbidden paths, OAuth flows, verifiable intent) signals a growing enterprise appetite. Agent security tooling (memory trust tagging, prompt-injection mitigation) is a clear market whitespace.

4. **MCP needs an ecosystem-layer fix.** MCP is universally embraced but lacks robust error-handling and environment-forwarding conventions. Both agent projects and tool developers should expect this to be a recurring integration pain point for the next year.

5. **Multiplexing and multi-profile deployment is a real pain.** Users running fleets (cron across profiles, per-profile adapters, credential conflicts) are hitting architectural walls. The project that makes multi-identity multi-channel management seamless will win power users.

6. **Model routing is becoming more sophisticated.** Beyond fallback chains, users want automatic model selection per request (small for simple, large for reasoning). This implies agent frameworks must support more intelligent model orchestration and telemetry-driven decisions.

7. **Long-tail QA and tooling needs are emerging.** High-reliability CI gates, IDE-like debugging (Web Debug Inspector), and transparent traceability (OpenTelemetry root spans) are increasingly part of the agent framework package, not optional extras.

---

*Report generated 2026-08-06 from community digest summaries.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-06

## 1. Today's Overview

NanoBot is in an active development phase with 8 PRs merged/closed and 8 PRs currently open in the last 24 hours. The project saw significant progress across channels (WhatsApp, Matrix, Mattermost), the WebUI (Temporary Chat mode, visual refinements, interactive terminal), and provider integrations (metasearch, provider-native request switches). No new releases were published, and all 4 tracked issues remain open. The overall project health is strong, with a steady stream of bug fixes and feature development; however, the volume of WebUI-related PRs from a single contributor (chengyongru) warrants attention for maintainer bandwidth.

## 2. Releases

No new releases were published in this period. The project continues to operate on its existing version; users should track the main branch for upcoming features.

## 3. Project Progress

The following PRs were merged or closed in the last 24 hours, representing completed work:

- **`#5234`** — **Meta-Search Tool provider** (goodtiding5): Integrated `mst-python` as a new web search provider, aggregating results from DuckDuckGo, Google, Brave, Bing, etc., with Reciprocal Rank Fusion (RRF) for richer coverage.
- **`#5249`** — **WebUI visual consistency** (chengyongru): Solid surfaces with a two-level elevation system, flattened Skills/Channels layouts, unified segmented controls, removed replay animations, and automatic timezone detection.
- **`#5250`** — **WebUI activity-edge feathering** (chengyongru): Direction-aware fades for clipped agent activity panes with correct auto-follow behavior.
- **`#5238`** — **Session access-grant removal** (chengyongru): Deleted request-scoped `Tool.available()` layer and `SessionAccessScope` abstraction; session tools now directly read all persisted sessions. This resolves a regression introduced by PR #5211.
- **`#5203`** — **WhatsApp outbound media fix** (chengyongru): Detects media by file contents (libmagic) rather than filename extension; keeps supported audio on the inline path and falls back to document sending for ambiguous formats.
- **`#5184`** — **Quick Chat and Temporary Chat WebUI destinations** (Re-bin): Persistent Quick Chat with stable identity, plus opt-in Temporary Chat with connection-owned in-memory history; superseded by the more focused #5252 (still open).
- **`#5233`** — **Mattermost thread group policy** (goodtiding5): Added `groupPolicyInThread` config field for separate mention requirements in threads vs. main channels, exposed via the WebUI.
- **`#5254`** — **Provider-native request switches** (chengyongru): WebUI toggles for OpenAI Codex Fast mode, OpenAI/DeepSeek web search, and xAI Grok X Search via `extraBody` modifications.

## 4. Community Hot Topics

- **Issue `#5149` — "no audio?"** (4 comments): Users report that NanoBot receives but does not send audio messages on WhatsApp. The underlying issue appears related to the ffmpeg/neonize integration and is likely addressed by PR `#5203` (detecting outbound media content before dispatch), which was merged today.
- **Issue `#5237` — "MCP tool returns 'data not found' envelope"** (2 comments): When an MCP server returns a business error inside `CallToolResult.content` with `isError = False`, the agent treats it as success and stalls until timeout. This exposes a design limitation in MCP error-handling conventions.

## 5. Bugs & Stability

Issues ranked by severity:

1. **`#5237` — MCP error-envelope misdetection (High)**: Agent cannot distinguish a successful tool call from a business error envelope; causes wasted tokens and timeouts. No fix PR yet — this is a correctness issue in the tool-call evaluation path.
2. **`#5256` — Goal-loop reply explosion (Medium)**: A single `/goal` message causes dozens of near-identical replies while waiting for user input. PR `#5257` (bound sustained-goal continuation) directly addresses this; the PR is open and waiting for review.
3. **`#5149` — WhatsApp audio not sent (Medium)**: Lacks a fix PR in the issue thread, but PR `#5203` (merged today) addresses the outbound media detection logic.
4. **`#5248` — Matrix room join fails on Continuwuity (Low-Medium)**: Empty POST body on room join is rejected by Continuwuity homeservers with `M_BAD_JSON`. PR `#5248` sends a non-empty POST body for compatibility; it is open.

## 6. Feature Requests & Roadmap Signals

- **`#5251` — MCP Apps host support in WebUI (new)**: User requests rendering MCP Apps (`io.modelcontextprotocol/ui`) artifacts inside the WebUI rather than just text/image results. This is a forward-looking WebUI enhancement aligned with the MCP ecosystem's evolution; likely materializes in a future release after the current WebUI feature wave settles.
- **Temporary Chat mode (PR `#5252`, `#5259`)**: Opt-in in-memory-only sessions — currently in review, likely slated for the next minor release.
- **Shared interactive project terminal (PR `#5253`)**: Persistent project-scoped PTY in the WebUI with xterm.js; indicates a push toward richer developer workflows.

## 7. User Feedback Summary

- **Channels**: WhatsApp media handling remains the most complained-about area; users expect parity in send/receive behavior for audio.
- **MCP ecosystem**: Users are pushing NanoBot toward more robust MCP error handling and app-like rendering in the WebUI.
- **Agent behavior**: The `/goal` loop shows that sustained-goal injection can spiral out of control; users expect the agent to respect turn boundaries when waiting for input.
- **WebUI UX**: Multiple merged UI polish PRs suggest iterative refinement based on real usage feedback around visual consistency and readability.

## 8. Backlog Watch

- **`#5149` — WhatsApp audio sending** remains open (9 days) despite a likely fix in `#5203`; maintainers should close or link the issue to the fix PR.
- **PR `#5255` (Draft) — Truthful API service status**: Unreviewed draft; externally-managed `nanobot serve` instances are misreported as Off in the WebUI. This is a correctness/truthfulness gap in observability that could undermine user trust if left unaddressed.
- **`#5237` — MCP error-envelope handling** has no associated fix PR; maintainers should triage and either provide guidance or accept a proper error-propagation mechanism for MCP tools.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-06

## 1. Today's Overview

Hermes Agent is in a period of **high-intensity active development**, with 50 open issues and 50 open PRs updated in the last 24 hours and **zero closed or merged** items—indicating a heavy review/iteration load rather than a delivery day. The dominant signal is a **repo-wide architectural cleanup campaign**: a huge cluster of Telegram feature-parity issues (#78773–#78791, ~20 open issues) and a parallel "god-file decomposition" refactoring effort (epic #78647) are driving most issue and PR volume. Meanwhile, **session-state integrity is the top technical risk area**, with multiple `sweeper:risk-session-state` PRs aimed at persistence, WAL-reader cleanup, and context-overflow retry loops. No new releases shipped today.

## 2. Releases

**No new releases** in the last 24 hours. The last notable dependency bumps are inbound via PRs (#79809), not published tags.

## 3. Project Progress

No PRs were merged or closed today (all 50 updated PRs remain open), so "progress" is defined by **what's in the active pipeline**:

- **God-file decomposition wave**: PR #79127 (web_server.py custom-endpoints slice R3-C1), PR #79708 (cli.py shard S2), and PR #79800 (slack adapter.py messaging mixin) continue breaking down massive files per epic #78647. These are byte-fidelity extractions with zero behavior change.
- **Provider-persistence fix**: PR #79811 ensures the provider is persisted alongside the model in `model_config` on switch (#79536), fixing session-resume misrouting.
- **Desktop session handling**: PR #73608 fixes silent failures of refresh/regenerate/restore-checkpoint when an active runtime ID exists (#68734); PR #77857 makes "New session" land in Home project; PR #79805 recovers attach and `/compress` after stale-session drop.
- **Platform parity**: PR #79808 enforces cron `required_skills` at job creation; PR #73363 fixes multiplex-profile cron delivery through per-profile adapters; PR #79799 adds Slack free-response channel acks.
- **Windows/en-US test fixes**: PR #79810 makes TUI terminal-setup and desktop tests pass on Windows and non-en-US locales.

## 4. Community Hot Topics

The most-discussed items reveal two **campaign-style efforts**:

- **Epic #78647 — "Shard all 20 god files"** (14 comments): The standing 2026-08 policy that god files *must* be sharded and never reverted. This is the umbrella for a wave of mechanical extraction PRs. The heated conversation likely centers on how to validate zero-behavior-change extraction at scale. [Link](https://github.com/NousResearch/hermes-agent/issues/78647)

- **Bug #77780 — `lifecycle_guard` crashes on `ValueError: embedded null byte`** (12 comments): A gateway lifecycle guard crashes when scanning terminal commands with heredoc/`-c` payloads, breaking *all* terminal commands. High severity, high engagement. [Link](https://github.com/NousResearch/hermes-agent/issues/77780)

- **Refactor #54962 — Extract Gateway Platform Routing from run.py** (11 comments): The 858KB `gateway/run.py` is a prime sharding target; this issue is likely co-opted by the epic above. [Link](https://github.com/NousResearch/hermes-agent/issues/54962)

- **Bug #71941 — Delegated child context persists through shared terminal snapshots** (5 comments): Terminal env caching leaks `HERMES_DELEGATED_CHILD_CONTEXT` into non-delegated invocations; a classic state-leak class. [Link](https://github.com/NousResearch/hermes-agent/issues/71941)

The **Telegram meta-issue #78791** (5 comments) aggregates ~20 smaller feature-gap issues, all authored by the same contributor (`andrexibiza`), signaling an organized API-parity campaign targeting Bot API 10.2.

## 5. Bugs & Stability

Ranked by severity (all open, fix PRs noted where present):

**High**
- **`lifecycle_guard` null-byte crash** (#77780): Unhandled `ValueError` from `os.open` crashes all terminal commands during path scanning. **No fix PR yet** — 12 comments, 3 days old.
- **Delegated child context leaked via terminal snapshots** (#71941): Shared terminal env caches persist `HERMES_DELEGATED_CHILD_CONTEXT` into non-child commands—state-boundary violation. **No fix PR yet**.

**Medium**
- **Desktop session-not-found after sleep/restart** (PR #79805): Attach and `/compress` fail while plain text works; fix retries a one-time session resume. This PR is the fix.
- **SessionDB WAL reader accumulation** (PR #75352): Long-lived `SessionDB` retains one SQLite/WAL file-descriptor per finished thread until shutdown; fix reclaims finished-thread readers.
- **Fresh-tail context overflow retry loops** (PR #79717): Compression can't shrink protected recent messages enough to fit context, causing repeated compression loops; root cause behind #64382.
- **MiniMax OpenAI-compatible tool-schema rejection** (PR #73093): MiniMax M3 rejects `boolean`, `default`, `anyOf`/`null`; sanitization added.
- **Multiplex-cron misdelivery** (PR #73363): All profile crons delivered via default profile's adapter, breaking per-profile replies/failures.
- **Discord slash-command profile routing** (PR #69242): Native `/profile` and `/model` fall back to `default` profile under multiplex; two independent causes fixed.

**Low**
- **Cost label at 2dp** (#79220): Sub-cent per-turn costs render as `$0.00`; pure display bug, no calc impact.
- **Stale LSP clients** (PR #79801): Race in `_get_or_spawn` spawning duplicate processes; atomic check-and-claim added.

## 6. Feature Requests & Roadmap Signals

Two clear roadmap signals dominate:

- **Telegram Bot API 10.2 full parity** (meta #78791): ~20 issues cover gaps from callback-query answering (#78788) and inline mode (#78774) to payments/Stars (#78775), gifts (#78776), games (#78777), Passport (#78779), business-account management (#78786), and managed-bot APIs (#78785). This reads like a **v-next marketing/differentiation push** toward monetized surfaces (Stars, gifts, paid broadcasts). Most are tagged P3 but the breadth strongly suggests a coordinated release.
- **Repo-wide god-file decomposition** (epic #78647): Not a user feature but an engineering-health mandate. PRs are landing daily; expect a flurry of mechanical extraction merges in coming weeks.

Smaller signals: cron `required_skills` enforcement (PR #79808) and outbound Telegram UTF-8 BOM normalization for Cyrillic attachments (PR #79694) suggest **hardening of user-facing polish**, not just plumbing.

**Prediction**: The next minor release will likely bundle Telegram 10.2 parity (inline mode, callback fixes, menu-button APIs) plus the first wave of god-file shards. Session-state "risk-session-state" fixes may land as patch releases first given their P2 + blast labels.

## 7. User Feedback Summary

Pain points visible from issue/PR context:

- **Multiplex-profile confusion**: Users running `multiplex_profiles` hit misrouted crons (#73363), misplaced Discord slash commands (#69242), and hard-to-attribute credential-lock conflicts (#78130). The system delivers output on the wrong identity—high friction for fleet operators.
- **Windows & locale friction**: Non-en-US/Windows developers fail on TUI tests (#79810) and encounter UTF-8 mojibake sending Cyrillic text to Telegram (#79694). Suggests a growing Windows user base.
- **Session-state fragility**: Desktop users lost attach/compress after sleep (#79805) and silently failing refresh/regenerate (#73608) — "it just doesn't work" class bugs that erode trust.
- **Provider/model switching quirks**: Switching models across providers loses the provider on resume (#79811), and MiniMax custom endpoints reject standard schemas (#73093).
- **Satisfaction signal**: The organized campaign issues and quick, specific bug reports (cost formatting, callback spinners) indicate **engaged, technically sophisticated users** who file high-quality reports. Zero merged PRs today despite heavy activity may frustrate contributors awaiting review.

## 8. Backlog Watch

Issues/PRs needing maintainer attention (oldest, high-traffic, or high-risk):

- **#54962 — Extract Gateway Platform Routing from run.py** (opened 2026-06-29, 11 comments): The 858KB `gateway/run.py` remains the biggest god file; the epic references 20 files but this one is the 800-pound gorilla. Needs assignment to a shard wave. [Link](https://github.com/NousResearch/hermes-agent/issues/54962)
- **#77780 — lifecycle_guard null-byte crash** (opened 2026-08-03, 12 comments): P2, breaks all terminal commands, 3 days old, **no fix PR yet**. This is the top stability debt. [Link](https://github.com/NousResearch/hermes-agent/issues/77780)
- **#73363 — cron multiplex misdelivery** (opened 2026-07-28): P2 with `sweeper:risk-message-delivery` and `blast-moderate`, open for 9 days; a correctness bug affecting multi-profile deployments.
- **#75352 — WAL reader accumulation** (opened 2026-07-31): P2 `risk-session-state`; long-lived FD leak — silent resource exhaustion.
- **#71941 — delegated context leak** (opened 2026-07-26, 5 comments): State-boundary bug with security implications (`HERMES_DELEGATED_CHILD_CONTEXT` persisting where it shouldn't); 11 days open without a fix PR.

---

**Project health assessment**: Actively maintained and well-organized (clean issue labeling, sweeper tags, epic-driven refactors), but **stuck in a review bottleneck** — 50 open PRs, zero merges today. The Telegram parity campaign risks flooding maintainers with P3 feature requests while critical P2 stability fixes (null-byte crash, session leaks) wait in the wings.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-06

## 1. Today's Overview

PicoClaw activity today is moderate, driven primarily by pull request updates rather than issue traffic. The project is in a mature phase with **zero new issues** opened or updated in the last 24 hours, suggesting a relatively stable issue backlog. However, **4 PRs** were active, signaling ongoing development work. Notably, one older PR (#926, open since February) was finally **merged/closed today**, which is a positive sign that long-pending contributions are being resolved. The oldest open PR now dates back to March 2026 (#1951), which is starting to age and may need attention. No new releases were published in this period.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

**Merged/Closed PRs (1):**

- **[PR #926](https://github.com/sipeed/picoclaw/pull/926)** — **[CLOSED]** *(enhancement, provider domain)*: Added **Anthropic OAuth setup-token login** (`sk-ant-oat01-*` tokens) as an alternative to traditional API keys. This includes a new `--setup-token` CLI flag, an interactive login menu, integration of Anthropic's usage endpoint to show 5-hour and 7-day utilization in `auth status`, and streaming support for OAuth tokens. *This is a significant provider enhancement that finally landed after ~5 months.*

**Open PRs with activity (3, no merge today):**
- **[PR #3318](https://github.com/sipeed/picoclaw/pull/3318)** — *(fix, web)*: Repairs a broken `web/frontend/pnpm-lock.yaml` where `semver@7.8.5` was duplicated under both `packages:` and `snapshots:`, making the lockfile unparseable by pnpm (`ERR_PNPM_BROKEN_LOCKFILE`).
- **[PR #3200](https://github.com/sipeed/picoclaw/pull/3200)** — *(feat, models)*: Adds a **configurable default fallback chain** for models in the web UI, with full CRUD and reordering persisted through the backend API.
- **[PR #1951](https://github.com/sipeed/picoclaw/pull/1951)** — *(chore, build)*: Moves installation scripts from a separate docs repo into the main repository to centralize install tooling.

## 4. Community Hot Topics

No issues or PRs received notable comment/reaction activity in the last 24 hours (all show 0 comments and 0 reactions). The project's community interaction appears quiet this period, with development happening primarily through direct PR submissions rather than discussion threads.

The most interesting *technical* conversations, however, revolve around:

- **Model fallback chain configuration** ([PR #3200](https://github.com/sipeed/picoclaw/pull/3200)): An active feature request to allow users to define ordered fallback models in the web UI, which addresses reliability concerns when primary models fail.
- **Anthropic OAuth support** ([PR #926](https://github.com/sipeed/picoclaw/pull/926)): The closure of this PR demonstrates continued investment in provider flexibility and a modern authentication path for Anthropic users.

## 5. Bugs & Stability

**1 bug reported/active today** (severity: medium):

- **Broken pnpm lockfile** ([PR #3318](https://github.com/sipeed/picoclaw/pull/3318)): A duplicated mapping key in `web/frontend/pnpm-lock.yaml` prevents `pnpm install` from working, producing a hard failure (`ERR_PNPM_BROKEN_LOCKFILE`). This blocks anyone trying to install the frontend from source. A fix PR exists and is open; no severity label provided.

*No crashes, regressions, or security-related issues reported.*

## 6. Feature Requests & Roadmap Signals

- **Model fallback chains** ([PR #3200](https://github.com/sipeed/picoclaw/pull/3200)): Higher-priority user demand for resilience — allowing users to define and persist an ordered list of fallback models. This strongly signals a reliability focus for multi-model workflows.
- **Provider auth flexibility** (now merged in [#926](https://github.com/sipeed/picoclaw/pull/926)): The Anthropic OAuth setup-token path reduces dependence on API keys and improves usage visibility; similar patterns may be extended to other providers.

**Prediction:** The model fallback chain feature ([PR #3200](https://github.com/sipeed/picoclaw/pull/3200)) is the most likely candidate for the next minor release, as it's been open for over a month and addresses a clear reliability use case.

## 7. User Feedback Summary

There were no new user issues, comments, or reactions in the last 24 hours, so no fresh direct pain points were captured. However, indirect signals from submitted PRs indicate the following ongoing user needs:

- **Reproducible builds**: The broken lockfile PR (#3318) reflects developer friction when trying to set up the frontend.
- **Dependency installation centralization**: PR #1951 suggests users prefer installation scripts living in the main repo rather than in separate docs.
- **Provider authentication flexibility & reliability**: The Anthropic OAuth merge (#926) and fallback chain proposal (#3200) point to growing concerns around API keys and model reliability in production use.

## 8. Backlog Watch

The following PRs have been open for an extended period and may need maintainer attention:

- **[PR #1951](https://github.com/sipeed/picoclaw/pull/1951)** *(open since 2026-03-24, ~135 days)* — Installation scripts relocation. No comments, no review activity visible. Should either be reviewed for merge, requested for changes, or explicitly closed with guidance.
- **[PR #3200](https://github.com/sipeed/picoclaw/pull/3200)** *(open since 2026-07-01, ~36 days)* — Model fallback chain feature. A valuable feature that appears to be waiting for a maintainer review; it should remain on the near- term review radar.

No long-unanswered *issues* currently exist, as the open issue backlog is at zero.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-06

## 1. Today's Overview

NanoClaw shows moderate activity with 12 PRs updated in the last 24 hours, of which 2 were merged/closed and 10 remain open, alongside 2 active issues (both unresolved). The project is in a healthy development rhythm — the merged PRs focus on architectural correctness (single-writer DB invariants) and agent-to-agent messaging semantics, while new work streams target channel reliability (WhatsApp timeouts), container environment forwarding (MCP proxy/CA-trust), and a steady flow of community skill contributions (Tavily, Dial, add-why). No new releases were published, indicating the project is in a consolidation phase between versions. The PR-to-issue ratio (12:2) suggests a contributor-friendly culture, though the two lingering issues (both 2-3 months old) signal some gaps in the support/maintenance loop.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release tag was not included in the data window.

## 3. Project Progress

**2 PRs merged/closed today:**

- **#3187 [CLOSED/merged] — `fix(agent-runner): disallow built-in SendMessage so agent-to-agent messaging works`** by `dim0627`. This fix removes the built-in `SendMessage` tool, preventing the agent from using it as a shortcut and thereby forcing/ enabling proper agent-to-agent messaging flows. This is a behavioral change that impacts how agents communicate internally.

- **#3175 [CLOSED] — `fix: route command-gate denials through the delivery adapter, not outbound.db`** by `Joi`. This is a duplicate/earlier version of open PR #3192. It addressed the same issue: the host was inserting rows into a container-owned `outbound.db` (violating the project's single-writer rule). The newer PR #3192 supersedes it.

**Key architectural progress signaled by open PRs (not yet merged):**
- **#3192** — The refined version of the command-gate denial fix (see above). This is the one to watch.
- **#3186** — `refactor: add host seams for skill-owned capabilities` by `zvi-fried`. This is a significant architectural refactor to give skills a clean interface for host-level capabilities (likely filesystem, network, process control).
- **#3156** — `fix(agent-runner): carry channel attachments to providers as structured parts` by `glifocat`. Directly addresses the image/PDF attachment issue reported in issue #2528 (Signal attachments unreachable from agent container).

## 4. Community Hot Topics

The most active items (by comments/reactions, limited data — most have 0-1 comments):

- **Issue #2528 — Signal channel: image/PDF attachments unreachable from agent container** (1 comment, opened 2026-05-18). This is a long-running bug that now has an open fix PR (#3156) in flight. The community interest is implied by the issue's age and the dedicated fix.

- **Issue #2006 — Fresh install on Debian 12 LXC: docker socket permission denied** (1 comment, opened 2026-04-25). A fresh-install blocker on a very common platform (Proxmox VE LXC). No fix PR is currently open.

- **PR #3172 — chore(skills): remove stale qodo and Google MCP skills** by core-team member `glifocat`. A housekeeping PR that signals skill maintenance/cleanup is now a team priority, likely responding to user confusion or breakage with dead MCP integrations.

**Underlying needs:** Users are struggling with two practical issues: (1) getting media attachments (images/PDFs) from chat channels into the agent's context, and (2) friction-free installs on containerized environments (LXC) where Docker socket permissions are notoriously tricky.

## 5. Bugs & Stability

Ranked by severity:

1.  **[HIGH] Issue #2006 — Docker socket permission denied on fresh Debian 12 LXC install (open since 04-25).** The setup script adds the user to the `docker` group, but subsequent steps fail — likely because group membership requires a re-login or newgrp, or the `install-docker.sh` script has a race condition on LXC's cgroup-less environment. **No fix PR open.** This is a first-run experience breaker.

2.  **[HIGH] Issue #2528 — Signal image/PDF attachments unreachable from agent container (open since 05-18).** Attachments arrive at the host but the agent inside the container cannot access them (permission or mount-path issue). **Fix PR #3156 is open** — the community is actively working this.

3.  **[MEDIUM] PR #3191 — WhatsApp `setup()` can hang host startup indefinitely** if the linked session is logged out (Baileys never fires `connection: open`). This is an acknowledged bug with a targeted fix (bound to a timeout).

4.  **[MEDIUM] PR #3188 — MCP servers spawned as stdio children don't inherit `HTTPS_PROXY`/CA-trust env vars.** This breaks MCP usage in proxied/enterprise environments. Fix is open.

5.  **[LOW/ARCHITECTURAL] PR #3192/#3175 — Command-gate denial writes to `outbound.db` from the host.** This is a data-corruption risk (violates single-writer invariant). Fix is open.

## 6. Feature Requests & Roadmap Signals

- **New skill additions (signal: community wants more tools):** Three new skills are in flight:
  - **#3190 — Tavily MCP tool** (web search API) — likely to land.
  - **#3189 — `add-why` skill** (explain what happened to one message) — a debugging/transparency tool.
  - **#3050 — Dial channel integration** (with setup wizard support) — a significant feature.

- **Skill/host capability seams (#3186):** The refactor to add host seams for skill-owned capabilities is a foundational change. It suggests the roadmap includes more powerful skills that need explicit access to host resources (which is also necessary to fix the attachment issues). This is likely part of the next minor release (v2.x).

- **MCP environment forwarding (#3188):** Fixing proxy/CA-trust for MCP servers points to enterprise/proxy-heavy usage as a target user segment.

**Prediction for next version:** Expect the next release to include the channel-attachment fix (#3156), the skill/host seam refactor (#3186), the WhatsApp timeout fix (#3191), and possibly the Dial channel (if #3050 gets merged in time).

## 7. User Feedback Summary

- **Pain point — install friction on LXC/Proxmox:** User `dooha333` reports a complete setup failure on Debian 12 LXC. The install script's Docker group handling is insufficient for non-interactive/containerized shells. This is a significant onboarding blocker for homelab/self-hoster users.

- **Pain point — media in chat channels:** User `brentkearney` cannot get the agent to "see" images/PDFs sent over Signal, though the files reach the host. This breaks a core "show the agent what I see" workflow, affecting trust in the channel integration.

- **Satisfaction signal:** The high volume of skill submissions (Tavily, why, Dial) and the number of `[PR: Skill]` labeled PRs indicates a healthy, engaged contributor community that values extensibility.

- **Frustration signal:** The stale issues (2006, 2528) with very low comment counts and long resolution time may indicate the maintainer team is PR-focused (12 PRs vs 2 issues) and may need more time triaging and communicating on bug reports.

## 8. Backlog Watch

Items needing maintainer attention:

1.  **Issue #2006 (open since 2026-04-25, ~103 days):** Fresh install on Debian 12 LXC fails — **no fix PR, no maintainer comment since the initial report.** This is a critical on-ramp bug that should be prioritized or at least acknowledged with a workaround.

2.  **Issue #2528 (open since 2026-05-18, ~79 days):** Signal attachments unreachable — **fix exists in PR #3156 (open since 07-30).** Maintainers should nudge/review/merge this PR to close the loop. It's the most user-visible outstanding issue.

3.  **PR #3050 (open since 2026-07-14):** Dial channel feature — a substantial feature PR with no visible maintainer activity in the last 24h. Needs review or explicit deferral to keep the contributor motivated.

4.  **PR #2346 (open since 2026-05-08, ~90 days):** `fix(formatter): treat unknown slash commands as normal chat` — a small, user-facing fix that has been sitting unreviewed for 3 months. The lack of attention to this low-risk PR suggests a review bottleneck for older PRs.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-06

## 1. Today's Overview

NullClaw is in a **quiet but focused maintenance phase**. There were **no new issues, releases, or merged PRs** in the last 24 hours, indicating a temporary lull in community engagement. However, the maintainer team is active, with **two open pull requests** submitted yesterday (both authored by *raskevichai*) targeting critical runtime stability and channel connectivity bugs. The absence of new bug reports suggests the project is stable, while the PR queue points to **proactive hardening of the agent execution environment and gateway supervision**. With zero open issues and two targeted fixes in flight, the project health looks good, though the low issue volume may also reflect a smaller active user base.

## 2. Releases

**No new releases** were published in the last 24 hours. The project remains on its previously established version.

## 3. Project Progress

No PRs were merged or closed in the last 24 hours. However, two **open PRs** indicate work in progress on the following areas:

- **[#985 — fix(runtime): give the agent turn path a 16 MiB stack](https://github.com/nullclaw/nullclaw/pull/985)**: Addresses a memory/stack-size configuration issue. The PR identifies that `SESSION_TURN_STACK_SIZE` was incorrectly aliased to a 2 MiB heavy runtime stack size, which is insufficient for the `SessionManager.processMessage*()` and `Agent.turn()` execution paths. This fix increases the stack to 16 MiB, likely preventing deep-recursion stack overflows.

- **[#984 — fix(channels): let poll failures age out a dead polling thread](https://github.com/nullclaw/nullclaw/pull/984)**: Fixes a critical connectivity bug where Telegram and Matrix channel pollers silently die after idle periods (e.g., overnight), requiring a full gateway restart. The PR restructures the `supervisionLoop` so it can detect and retire dead polling threads.

## 4. Community Hot Topics

No issues or PRs today had significant comments or reactions (both PRs show 0 comments and 0 👍). Activity is limited to the two open PRs. Analysis of the underlying needs:

- **[PR #985](https://github.com/nullclaw/nullclaw/pull/985)** and **[PR #984](https://github.com/nullclaw/nullclaw/pull/984)** both reflect **production reliability concerns** from the author: agents crashing mid-conversation and channels silently dropping after idle. The community (or at least this contributor) is prioritizing stability for hands-off, always-on agent deployments.

## 5. Bugs & Stability

No new bugs were reported today. However, the **two open PRs are directly fixing previously reported bugs** from 2026-08-05, and both are noteworthy:

| Severity | Bug Description | Status |
|----------|-----------------|--------|
| **High** | **Channel Poller Death (PR #984, closes #972)**: Telegram and Matrix go silent after idle periods. A full gateway restart is required to recover. This is a serious reliability bug for long-running instances. | Fix proposed, open. |
| **Medium** | **Agent Turn Stack Overflow (PR #985, closes #976)**: Agent execution path uses an undersized 2 MiB stack, risking crashes on complex turns. | Fix proposed, open. |

No regressions were reported.

## 6. Feature Requests & Roadmap Signals

No new feature requests were filed today. **Implicit roadmap signals** from the pending PRs:

- **Adaptive runtime configuration**: PR #985 suggests future work on **configurable stack sizes** based on execution path complexity, not a single global constant.
- **Self-healing supervision**: PR #984 indicates a move toward **more robust health checks and automatic thread resurrection** in the gateway, which could lead to more resilient channel integrations.
- **Predictions**: The next minor release will likely contain both of these fixes. Expect a follow-up issue to introduce **configurable stack sizes** and potentially **more granular supervision controls** (e.g., poll intervals, health check thresholds).

## 7. User Feedback Summary

With zero issues and zero comments on PRs in the last 24 hours, there is no direct user feedback to summarize. However, the **existence of PRs #984 and #985 implies the author (likely a power user or internal team member) experienced the following pain points**:

- **Reliability pain**: Feeling the need to manually restart the gateway after an idle night is a significant workflow interruption.
- **Performance concerns**: The stack overflow bug indicates users are hitting complex, deep-conversation scenarios that stress the runtime.

Satisfaction appears **neutral-to-positive**: these are bug fixes being proactively submitted, not complaints. The project responds to bugs within a day (issues #972 and #976 were reported 08-05, fixes proposed 08-05), showing strong maintainer responsiveness.

## 8. Backlog Watch

There are **no long-unanswered issues** in the backlog (0 open issues). The two open PRs (#984, #985) are **new (1 day old)** and actively maintained. No items require maintainer attention at this time; the queue is clean.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-06

## Today's Overview

IronClaw is in a period of intense, healthy development activity. The project is processing a substantial volume of work: 43 issues and 50 pull requests updated within the last 24 hours, with a balanced mix of open work, closures, and merges (10 closed issues, 20 merged/closed PRs). While a single release candidate (`v1.1.0-rc.1`) was published three days ago, the current focus is clearly on hardening and expanding the "Reborn" architecture — evidenced by a wave of bug-bash QA reports (7+ filed in the last day), large refactoring efforts, and several major cross-cutting epics in flight. The concurrent activity on skills management, MCP integration, sandboxing, and the WebUI signals a maturing platform shifting from foundational build-out to robustness and user-facing polish. Notably, a QA dogfooding cadence is visible, with quality-focused epics being opened and closed, suggesting a cyclical bug-fixing workflow. The presence of a new design-system proposal and governance documentation work indicates long-term architectural and product thinking.

## Releases

The project released `ironclaw-v1.1.0-rc.1` on 2026-08-03, the first release candidate since `1.0.0`. This is an early-version release candidate, so specifics on breaking changes and migration paths are limited. However, the release notes highlight four headline features:

- **Extension Reach:** The ability to register arbitrary hosted MCP servers, which is a core part of the extensibility strategy. The notes explicitly mention the capability to install via IronHub deep links.
- **Durable File Attachments:** Attachments now persist across channels, fixing a key gap in multi-channel workflows.
- **Slack `/ironclaw` Slash Commands:** Native integration for Slack users to interact with the agent directly.
- **Legibility Pass:** A broad effort focused on making failures more understandable to users.

This release is closely tied to the active work on MCP customization, with several PRs in flight that are directly backporting fixes to the release branch (e.g., PR #7260). Teams should monitor this RC for issues, as the high number of recent bug reports from the QA instance suggests potential stability concerns to be addressed before the final release.

## Project Progress

The most significant merged pull requests today are primarily focused on dependencies, release stabilization, and a foundational architecture piece. Key items include:

- **Standardized Messaging Framework (PR #6831, CLOSED):** This is a major architectural merge. It introduces a host-owned standardized messaging framework with 16 core operations, canonical input/output JSON schemas, and a 12-code canonical error taxonomy in `ironclaw_host_api::messaging`. This is foundational for the long-term stability of agent-host communication.
- **Release Canary Fix (PR #7261, CLOSED):** A critical fix resolving a zero-job failure in the tag-only release workflow, ensuring that release builds have proper verification gates.
- **MCP Egress & Log Backports (PR #7260, CLOSED):** Merged backports to the release branch that ensure dynamically discovered hosted MCP tools retain their HTTPS endpoints as network targets, and fix a file-write bug after read-before-edit checks.
- **Dependency Updates:** Multiple Dependabot PRs updating the `wasm` group (#7196 CLOSED) and the "everything-else" group (#7237 OPEN). Keeping dependencies current is a sign of good maintenance hygiene.

Other open PRs showing significant progress include the effort to make model-selected skills work correctly (PR #6938) and a substantial sandboxing feature PR (#7214). The overall project progress is forward-looking and focused on a robust, extensible core with strong developer experience.

## Community Hot Topics

The most active discussions, which often reveal strategic priorities, are centered on configuration management and the evolution of the agent's core capabilities.

- **Configuration-as-Code for IronClaw Reborn (Issue #3036):** With 7 comments and 1 reaction over several months, this open EPIC outlines the need for tenant blueprints and use-case harnesses. This is a highly requested feature from operators who want declarative configuration and audit trails, signaling a need for enterprise-grade manageability.
  - [Link](https://github.com/nearai/ironclaw/issues/3036)

- **Admin-Allowed Shared Channel as Outbound Target (Issue #7194):** The 3 comments on this new issue highlight a gap in the delivery system — the inability to route an agent's final reply to an arbitrary shared channel. It shows a desire for more flexible outbound communication workflows.
  - [Link](https://github.com/nearai/ironclaw/issues/7194)

- **PDF Attachment MIME-Type Error (Issue #6257):** With 2 comments, this bug is a user-facing blocker that touched on core "send and generate PDF" functionality. The details are somewhat sparse, which may be causing some back-and-forth.
  - [Link](https://github.com/nearai/ironclaw/issues/6257)

- **The Skills Ecosystem (PR #6938 & #6745):** These large PRs on skill selection and installation are generating significant discussion due to their scope. They represent a shift in the philosophy of how skills are utilized — moving from a host-determined scoring system to a model-driven choice. This highlights the tension between deterministic control and agent autonomy.
  - [PR #6938](https://github.com/nearai/ironclaw/pull/6938) | [PR #6745](https://github.com/nearai/ironclaw/pull/6745)

## Bugs & Stability

During the bug-bash, several high-priority (P1/P2) bugs were reported, indicating a strong QA process. The most severe are listed below, ranked by priority:

**High Severity (Risk: High / Priority: P1):**

- **Agent Hallucinates Automation Status (Issue #7246, P1):** A critical reliability and trust issue where the agent invented the status of an automation ("running and sending to Telegram") when none existed. This directly impacts user trust in the system's core reporting functions. *(No linked fix PR yet.)*
  - [Link](https://github.com/nearai/ironclaw/issues/7246)

- **False Claims of Successful Connections (Issue #7247, P1):** The agent incorrectly states integrations (e.g., GitHub) are connected without verifying authentication. This leads users to believe a connection is operational when it is not, causing subsequent workflow failures. *(No linked fix PR yet.)*
  - [Link](https://github.com/nearai/ironclaw/issues/7247)

**Medium Severity (Risk: Medium / Priority: P2):**

- **Invalid MCP Endpoint Acceptance (Issue #7248, P2):** The system accepts and registers an invalid endpoint as successful, then fails during use. Poor input validation leads to a confusing user experience.
  - [Link](https://github.com/nearai/ironclaw/issues/7248)

- **Cross-Channel Delivery of Execution Results (Issue #7249, P2):** A run triggered via a Slack DM delivers its final summary to a Telegram chat. This is a severe routing bug that could leak sensitive information to the wrong channel.
  - [Link](https://github.com/nearai/ironclaw/issues/7249)

- **Misleading MCP Authentication Guidance (Issue #7250, P2):** When network errors occur, the agent speculates about the cause (e.g., authentication) instead of reporting the actual error. This misdirects user troubleshooting efforts.
  - [Link](https://github.com/nearai/ironclaw/issues/7250)

- **Cross-Channel Delivery of Execution Results (Issue #7249):** Runs that trigger in one channel are delivering results to a completely different channel (Telegram vs. Slack). This is a critical routing bug with privacy implications.
  - [Link](https://github.com/nearai/ironclaw/issues/7249)

- **Agent Guesses MCP Auth Type (Issue #7251, P2):** Instead of discovering the authentication method, the agent forces the user to guess or choose. This highlights a lack of tool introspection capability.
  - [Link](https://github.com/nearai/ironclaw/issues/7251)

- **Inability to Access Slack Feedback Files (Issue #7254):** A bug preventing the agent from reading files attached to a Slack feedback thread.
  - [Link](https://github.com/nearai/ironclaw/issues/7254)

**Lower Severity (Frontend/CI):**

- **Composer Focus/Accent Ring (Issue #7204, CLOSED):** A UX papercut fixed and closed.
- **CI Regression Gate (Issue #7209):** A CI bug preventing frontend PRs from being tested correctly.

These issues collectively point to a need for better tool/endpoint discovery and a more assertive "I don't know" behavior from the agent when encountering state mismatches or failures.

## Feature Requests & Roadmap Signals

The roadmap is actively signaling a shift towards a more self-contained and adaptable system. The most prominent signals for future versions are:

1.  **Self-Creating and Selecting Skills (Epic #6941):** This is a major upcoming feature. It focuses on letting the model itself find, choose, and use skills that are proven to be valuable. A brand-new proposal (Issue #7203) suggests that skills should be accessible as a real mountable filesystem rather than being copied, enabling direct execution. The merging of the PR on standardized messaging (#6831) is a likely prerequisite for this to work smoothly.
    - [Epic #6941](https://github.com/nearai/ironclaw/issues/6941) | [Issue #7203](https://github.com/nearai/ironclaw/issues/7203)

2.  **Admin-Managed Agents (Epic #6578):** The concept of creating non-human subjects for automations and integrations, managed by administrators, is percolating. This suggests a move towards more production-scale, agent-operated workflows with a need for proper identity management.

3.  **AI-First Design System (Epic #7038):** The effort to build a Storybook-based design system with comprehensive theming is a strong signal that the WebUI is becoming a critical, polished product surface. This will likely improve the consistency and quality of the frontend experience.

4.  **Web Debug Inspector (Epic #7218):** An operator-only tool for investigating prompt construction and tool execution in real-time. This is a clear signal of a move towards supporting production debugging and observability, which is crucial for complex agent deployments.

**Predictions for the next minor release:** We can expect further hardening of the MCP experience based on the P2 bug reports, continued work on the skills management system (PR #6745 and #6938), and likely the integration of the new design-system PRs. The `v1.1.0` release will likely be a significant milestone showcasing these new extensibility and customization features.

## User Feedback Summary

The adoption of an explicit bug-bash process is yielding a wealth of user feedback that points to several key pain points:

- **Biggest Pain Point — State Verification:** Users are reporting that the agent confidently fabricates system state (e.g., automation status, connection status). Instead of checking the actual condition, it provides guesses or false confirmations. This is the most damaging trust issue reported today.
- **MCP Customization Confusion:** Users are experiencing friction when setting up custom MCP endpoints. The agent does not properly introspect endpoints, fails to initiate authentication flows, improperly validates URLs, and provides misleading guidance on errors.
- **Channel Routing Reliability:** There is a desire for the ability to route final results to shared channels (#7194), but the system is also suffering from incorrect cross-channel delivery of results (#7249), which is a severe regression in the core messaging flow.
- **Asset Management:** A clear gap exists where users are unable to access files from some channels to use in other workflows (#7254), and there are bugs in processing PDFs (#6257).
- **High Signal-to-Noise in Development:** The community also faces development-side friction. One major issue highlights that an "APPROVE" verdict in a PR comment does not trigger a real GitHub approval, blocking the merge queue (Issue #7231). A CI gate bug also misjudges frontend tests (Issue #7209), mistakenly failing valid PRs.

The users are expressing a strong desire for an agent that is factually grounded, honest about its limitations, and offers robust, predictable behavior with external systems.

## Backlog Watch

This section highlights important items that may be at risk of stalling or require maintainer attention.

- [ **Idle Time > 3 Months** ] **Configuration-as-Code for IronClaw Reborn (Issue #3036):** This epic was created in late April and, despite having the most comments, has seen no recent activity since its last update on August 5th. Given its status as an epic and its high community engagement, this is a strategic priority that needs resourcing or at least a clear status update to avoid losing momentum.
  - [Link](https://github.com/nearai/ironclaw/issues/3036)

- [ **Needs Review** ] **PR Review Approval System Bug (Issue #7231):** This is a process-blocking bug with a clear root cause (no real GitHub approval submitted). It doesn't require a large code change but a fix is crucial for maintainer and contributor sanity, as it falsely holds up otherwise-approved work. It needs a champion to drive the fix.
  - [Link](https://github.com/nearai/ironclaw/issues/7231)

- [ **Potential Risk** ] **Broken CI Regression Gate (Issue #7209):** The CI implementation is flawed and blocks valid frontend PRs, creating a negative work experience and slowing down the team. This process issue should be escalated to keep the development workflow efficient.
  - [Link](https://github.com/nearai/ironclaw/issues/7209)

- [ **New, Needs Verification** ] **PDF MIME-Type Bug (Issue #6257):** While updated recently, the lack of diagnostic detail in the report might lead to it being deprioritized. Given the criticality of document-based workflows, a maintainer should proactively seek a reproducible case to keep this from becoming a long-standing, low-priority item.
  - [Link](https://github.com/nearai/ironclaw/issues/6257)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-06

## 1. Today's Overview
LobsterAI shows a **high-velocity, engineering-healthy** profile today with 13 PRs touched in 24 hours, of which 12 were closed/merged (92% closure rate). The project shipped release **2026.8.5** featuring native daily check-in and enterprise auth isolation. While activity is concentrated in the renderer/cowork/main areas, three open bugs were actively discussed, including two fresh reports highlighting **system prompt duplication** and **skill toggle silent failure** — suggesting real deployment friction for power users. No security advisories or dependency crises were recorded. Overall, the project is shipping steadily but must address a growing backlog of UX-critical defects.

## 2. Releases
**LobsterAI 2026.8.5** was released yesterday.
- **Key changes:**
  - `feat(activity)`: Added native daily check-in experience (PR #2408).
  - `feat(enterprise)`: Isolated account-scoped auth and service flows (PR #2409).
- **Breaking changes:** None documented.
- **Migration notes:** None surfaced. The release appears additive, formalizing the daily-check-in UI and enterprise tenant separation.

## 3. Project Progress
Seven substantive PRs merged today, focused primarily on **stability hardening** and **UX polish**:
- **Window lifecycle harden** (PR #2437): OpenAI-compat proxy and HTML preview shutdown bounded with drain timers + hard deadline — prevents quit hangs from lingering keep-alive sockets.
- **Gateway lock poisoning fixed** (PR #2436): Two races (force-kill during lock write; gateway-initiated self-restart) could poison the OpenClaw single-instance lock. Now handled.
- **Title-bar conversation search** (PR #2435): Added search entry point beside artifact panel toggle, reusing sidebar search infrastructure.
- **Activity campaign polish** (PR #2433, #2438, #2439, #2432): Poster assets updated, white gutter cropped, claim failure messaging localized, final reward auto-popup disabled.
Dependency bumps for `cross-env`, `react-dom`, and `vite` were also merged (PR #1279–#1281).

## 4. Community Hot Topics
Most comments/reactions today were captured by issue **#1200** (NIM superTeam type bug) — one comment, stale 4 months, but clearly still relevant. However, the **real signal** comes from two issues opened yesterday by `fujingzhai` with zero comments yet — indicating a gap between community pain and discussion:
- **[Issue #2441 — Skill toggle silent failure](https://github.com/netease-youdao/LobsterAI/issues/2441)** (0 comments, but high impact): Config writes skill entries by *directory name* while OpenClaw matches by *frontmatter name*; mismatch means switches silently die. Also flags `openclaw.json` being overwritten wholesale.
- **[Issue #2440 — System prompt duplicate injection](https://github.com/netease-youdao/LobsterAI/issues/2440)** (0 comments): 78% of the injected `[LobsterAI system instructions]` block duplicates `AGENTS.md` content verbatim; every new desktop session pays ~4.4k chars of redundant context.
- **[Issue #1200 — NIM superTeam type hardcoded](https://github.com/netease-youdao/LobsterAI/issues/1200)** (1 comment): `teamTypeNum` hardcoded wrong at `nimGateway.ts:917`; superTeam/p2p correctly swapped, breaking group name resolution on @-mention.

**Underlying need:** Users want predictable, configurable system prompt construction and bug-free group-name rendering. The lack of discussion on #2440/#2441 suggests these were possibly *closed-by-stale* candidates or simply underexplored by maintainers — raising retention risk.

## 5. Bugs & Stability
Three bugs active today, ranked by severity:
1. **HIGH — Skill toggle silent failure** ([#2441](https://github.com/netease-youdao/LobsterAI/issues/2441)): User-configured skill exclusions ignored; toggling appears to work but produces no change. **No fix PR yet.**
2. **HIGH — System prompt duplication** ([#2440](https://github.com/netease-youdao/LobsterAI/issues/2440)): Models receive ~4.4k duplicated chars per session — cost/latency impact and potential instruction-conflict risk. **No fix PR yet.**
3. **MEDIUM — NIM superTeam name bug** ([#1200](https://github.com/netease-youdao/LobsterAI/issues/1200)): One-line fix proposed in PR #1201 (still open from April). Group name shows as raw ID in superTeam/regular groups when @-mentioning bot. **Fix PR exists but stale.**

**Stability wins today:** Window shutdown hang and OpenClaw lock poisoning — both solved (PR #2437, #2436).

## 6. Feature Requests & Roadmap Signals
Several explicit and implicit requests surfaced today:
- **Persistent user control over system prompt** (from #2441): Users want a durable, non-sparse way to trim the context injected into every session — suggests a "prompt profile" or "skill-level exclusion" feature.
- **Native daily check-in** (shipped in 2026.8.5): Now deployed; expect feedback on whether the UI is discoverable enough.
- **Title-bar search** shipped — signals cowork-focused ergonomics becoming a priority.
- **Declarative config preservation** (implied by `openclaw.json` overwrite complaint): Expect a request for a user-owned config overlay file — possible v2026.8.6 feature.
- **Stale bug fix for NIM** likely to be greenlit given it's a one-liner with PR ready.

**Prediction:** The next release will likely include a system-prompt deduplication/dedup control and possibly a fix for the skill-match bug, given they are fresh and touch the core UX loop.

## 7. User Feedback Summary
- **Pain points:** Users cannot reliably control what goes into their system prompt (duplicated instructions, broken skill toggle); config file is not user-honoring (overwritten without merge).
- **Frustration signals:** The `fujingzhai` issues were filed *with reproducible evidence* (trajectory JSONL, version numbers) — an expert-user profile, indicating friction at the power-user tier.
- **Satisfaction:** Positive momentum in release cadence and quality of lifecycle fixes (quit hangs, lock poisoning) suggests reliability improvements are appreciated.
- **Use cases observed:** Enterprise isolation (auth flows), community campaign engagement (startup credit), and day-to-day cowork interactions (search, activity).

## 8. Backlog Watch
- **[Issue #1200 / PR #1201 — NIM teamTypeNum bug](https://github.com/netease-youdao/LobsterAI/issues/1200)**: Open since April 1, 2026; fix PR stale. **Needs maintainer attention** — one-line change, prevents group-name regression in NIM gateways.
- **[Dependency PRs #1279–#1281]** — all merged today, so no longer in backlog, but worth noting they took months to land (created April, merged August) — signal of periodic dependency hygiene rather than continuous.
- **No other long-tail PRs** appear abandoned at this snapshot, which is a health marker — the team is closing out merged work promptly.

---
**Overall Project Health:** Strong, active, and shipping. Main risk: silent UX bugs (#2440/#2441) touching the core prompt pipeline may erode power-user trust if not triaged soon.

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

# CoPaw Project Digest — 2026-08-06

## 1. Today's Overview

CoPaw (QwenPaw) is in a period of **high development velocity**, with 75 issues/PRs updated in the last 24 hours. The project is actively processing a large batch of bug reports and feature requests from a diverse user base, with a significant portion focused on the **2.0.x stable line** and the **2.1.0-beta** desktop builds. Activity is not currently bottlenecked on maintainer responses; many issues have 1–4 comments indicating active triage. The issue tracker shows a healthy mix of bug reports (13), feature requests (9), and questions (3). While there are no new releases today, multiple rapid-fire bug fixes (e.g., `#6714`, `#6727`, `#6729`) have been merged, pointing to a fast iteration cycle. However, the volume of desktop-specific regressions in the 2.1.0 beta (PYTHONHOME injection, browser SDK crashes, WeChat channel approval flow issues) suggests the beta is encountering a predictable wave of integration bugs that will need to be resolved before a stable v2.1.0 release. Overall, the project health is **strong**: high contributor engagement, cross-platform test coverage being actively fixed, and a clear, steady stream of feature and stability work.

## 2. Releases

No new releases were published in the last 24 hours. The most recent known versions in circulation are **v2.0.1** and **v2.1.0-beta.1/b2**, with a number of issues filed against both.

## 3. Project Progress

Today's merged/closed PRs demonstrate consistent progress across the backend, console, and testing infrastructure. Key achievements include:

- **LLM Model Fallback (merged)**: PRs `#5597` (backend) and `#5598` (console UI) were merged after a ~6-week review cycle. This flagship feature now allows users to define backup model lists per-agent or globally, with retry logic remaining within a model before attempting automatic fallback.
- **Console Channel Fix (merged)**: PR `#5447` fixed a critical UX blocker where the console channel would leave the UI in a perpetual waiting state on model or runtime errors.
- **Responsive Utilities (merged)**: PR `#5462` added reusable responsive design utility classes for the console, improving the mobile experience across pages.
- **Testing Infrastructure (merged/updated)**:
  - PR `#6727` fixed a Windows path separator bug in test auto-marking that was silently skipping **66 integration test cases**.
  - PR `#6729` corrected an integration test to work with the new pool skill detail endpoint after a refactor split the API into list/detail views.
- **DeepSeek Reasoning Content (merged)**: PR `#6675` (first-time contributor) forces relay of `reasoning_content` for DeepSeek models, fixing multi-turn conversation failures when context compaction strips historical thinking blocks.
- **Audit Visibility (merged)**: PR `#6713` added audit records for when the router excludes sensitive directories.
- **App Market Unification (merged)**: PR `#6718` unified the app market listings, addressing fragmented UI/backend presentation.
- **Desktop Stabilization (open)**: PR `#6669` is in review to fix Chrome native messaging host and Windows restore locking failures.
- **SSE Error Retry (open)**: PR `#6714` adds retry logic for OpenAI-compatible SSE in-stream errors that carry status codes in messages (addressing issue `#6708`).
- **Fork Finalization Reporting (open)**: PR `#6725` (first-time contributor) correctly reports failures in background forked subagent finalization (addressing issue `#6722`).

## 4. Community Hot Topics

The most actively discussed issues highlight both **real user pain** and **advanced usage patterns**:

- **[#6684 — Channel Retry Functionality (QwenPaw)](https://github.com/agentscope-ai/QwenPaw/issues/6684)** (4 comments): A user setting up a self-hosted Matrix channel finds that QwenPaw connects faster than the Matrix service, leading to connection failure with no retry or health-check mechanism. The user must manually re-save the channel after every server restart. This is a highly practical reliability complaint.

- **[#6436 — Automatic Model Routing](https://github.com/agentscope-ai/QwenPaw/issues/6436)** (3 comments): A power user requests automatic model routing, where each request is sent to the most suitable model (small/fast for simple turns, vision model for images, large model for reasoning) instead of pinning an agent to a single model. This is a forward-looking architectural feature.

- **[#6480 — `nohup` Command Hangs Agent](https://github.com/agentscope-ai/QwenPaw/issues/6480)** (2 comments): A critical shell-command bug where a process detached via `nohup` or `&` never returns the agent to an idle state. This affects a common administrative workflow.

- **[#6696 — WeChat iLink Context Token Bug](https://github.com/agentscope-ai/QwenPaw/issues/6696)** (2 comments): A detailed bug report on the WeChat channel where a one-time `context_token` is consumed by the typing indicator, causing the actual reply to be rejected and leaving the "working" indicator stuck. The report demonstrates deep integration knowledge.

- **[#6716 — Deterministic Nightly Test Failure](https://github.com/agentscope-ai/QwenPaw/issues/6716)** (Closed as invalid): A reported flaky test turned out to be a deterministic failure across all platforms (`KeyError: 'auto_update_targets'`), though closed as invalid, it was already addressed by test refactoring PRs.

The presence of detailed, well-researched bug reports with environment specifics indicates a sophisticated and engaged user/developer community.

## 5. Bugs & Stability

A wide range of bugs were filed in the last 24 hours, ranked by severity:

**Critical (Crashes / Core Functionality Broken)**:
- **[#6697 — Desktop Injects `PYTHONHOME` into Child Env (Windows)](https://github.com/agentscope-ai/QwenPaw/issues/6697)**: Every Python subprocess crashes with `encodings ModuleNotFoundError` in v2.1.0-beta.1 desktop builds. This is a release-blocker for any user relying on Python tools on Windows.
- **[#6698 — Browser SDK `open()` Fails with `Target crashed`](https://github.com/agentscope-ai/QwenPaw/issues/6698)**: Browser tool is completely non-functional in v2.1.0-beta.1 on Windows 11, despite successful connection. Another beta blocker.
- **[#6732 — MCP Tools Fail Periodically](https://github.com/agentscope-ai/QwenPaw/issues/6732)**: MCP tools become unavailable ("not registered") after several hours, requiring a Docker container restart to recover. A serious reliability issue for MCP-dependent workflows.
- **[#6731 — `execute_shell_command` Crash with `sandbox_config`](https://github.com/agentscope-ai/QwenPaw/issues/6731)**: Model passing a valid argument from the schema causes a `TypeError`. **Fix: None yet.**
- **[#6700 — Large Tool Output Freezes Session](https://github.com/agentscope-ai/QwenPaw/issues/6700)**: A tool call producing multi-MB output causes the console to hang and can blow past the context window. **Status: Closed** (likely addressed by related output truncation work).

**Major (Core Feature Broken / Data Loss)**: 
- **[#6707 — 400 Error with Thinking-Mode Upstream](https://github.com/agentscope-ai/QwenPaw/issues/6707)**: Session history mixing tool calls and reasoning blocks causes permanent 400 errors. **Related PR: #6721 (open)**.
- **[#6726 — Tool/Result Pair Overflow](https://github.com/agentscope-ai/QwenPaw/issues/6726)**: Long sessions with 20-30+ tool calls fail with "Messages with role 'tool' must be a response to a preceding message with 'tool_calls'".
- **[#6722 — Forked Subagent False Completion](https://github.com/agentscope-ai/QwenPaw/issues/6722)**: Background forked subagents report completion even when the worktree finalization fails. **Fix PR: #6725 (open)**.
- **[#6696 — WeChat Approval Prompts Unreachable](https://github.com/agentscope-ai/QwenPaw/issues/6696)**: Gated shell commands and console-only approval dialogs make agent use impossible via WeChat/iLink channel. **Status: Closed, feature added in follow-up request #6728.**
- **[#6690 — Cron Pause/Resume Not Persistent](https://github.com/agentscope-ai/QwenPaw/issues/6690)**: Users lose all cron job enabled states after a restart. **Status: Closed.**

**Moderate (Specific Feature Broken / Minor Impact)**:
- **[#6708 — SSE 503 Errors Not Retried](https://github.com/agentscope-ai/QwenPaw/issues/6708)**: In-stream SSE errors from upstream gateway are not retried. **Fix PR: #6714 (open)**.
- **[#6687 — OpenRouter Multimodal Probe Overwrites Capabilities](https://github.com/agentscope-ai/QwenPaw/issues/6687)**: Probe results for OpenRouter models overwrite documented capabilities with false positives/negatives.
- **[#6480 — `nohup` Shell Command Hang](https://github.com/agentscope-ai/QwenPaw/issues/6480)**: Shell commands using `&` never return the agent to idle state.

## 6. Feature Requests & Roadmap Signals

The community is actively shaping the roadmap with several high-value requests:

- **Smart Model Routing (#6436)**: Automatic model selection per-request is a highly logical next step given the recent model fallback feature (#5597). It aligns with the project's "agent-first" philosophy and could be a major v2.2+ feature.
- **Live Artifact Canvas (#6730)**: Render agent-generated HTML deliverables (dashboards, reports, demos) directly in a side panel in the Console. This strongly correlates with the merged PR #6719 which adds persistent workspace artifact cards — a strong sign this is on the roadmap.
- **On-Demand Skill Loading (#6699)**: Currently, all enabled skills are injected into the system prompt, consuming 8-10k tokens with 27+ skills. Users want dynamic/on-demand skill loading to keep context lean. This is a significant efficiency improvement with clear user demand.
- **MCP Tool Timeout Configuration (#6724)**: A per-client configurable timeout for MCP tool calls plus a call-level guard to prevent stalled turns. A robust, developer-focused request.
- **Channel Retry Functionality (#6684)**: Built-in retry and health-check for messaging channels (specifically Matrix).
- **WeChat Approval in Chinese (#6728)**: Following the approval feature fix (#6695), the interaction labels ("Approve"/"Deny") should be localized for Chinese-speaking users.
- **Agent-Level Token Statistics (#6392)**: Detailed per-agent token usage tracking; more fine-grained accounting than the current global stats.

**Prediction**: The **Live Artifact Canvas** (#6730) and **On-Demand Skill Loading** (#6699) are the most likely candidates for next-version inclusion, as they directly respond to demonstrable user pain (context bloat, viewing deliverables) and have supporting infrastructure already being built (#6719).

## 7. User Feedback Summary

Real user pain points in this cycle revolve around **stability and reliability**:

- **Beta is breaking core workflows**: The `PYTHONHOME` injection bug (#6697) and Browser SDK crash (#6698) on Windows v2.1.0b1 are severe, rendering the desktop app partially non-functional for Python subprocesses and web automation. Users upgrading to the beta are experiencing clear regressions.
- **Operation frustration**: The Matrix channel connection loss (#6684) requires a manual re-save on every server start; the lack of retry/health-check is a daily annoyance. Similarly, cron pause/resume state loss (#6690) is a persistent governance issue.
- **Power users are pushing for efficiency**: Users managing 20-30+ skills feel the token bloat of loading everything into context (#6699) and want automatic model routing (#6436) to optimize cost/latency.
- **Active and helpful community**: The influx of first-time contributor bug reports (e.g., #6725, #6675) and fix PRs indicates a healthy, technically skilled community willing to both deeply diagnose and fix issues.

**Satisfaction signals**: The quick closure of several issues (cron persistence, approval prompts, UI simplification) suggests maintainers are responsive, which likely satisfies users. However, the **beta regression wave** may be a point of friction until v2.1.0 stable is released.

## 8. Backlog Watch

The following items require maintainer attention due to age, a lack of response, or criticality:

- **[#6480 — `nohup`/`&` Command Hangs Agent](https://github.com/agentscope-ai/QwenPaw/issues/6480)** (10 days old): A core shell-execution bug that breaks a common Linux/CI workflow. No linked fix PR. High priority.
- **[#6436 — Automatic Model Routing](https://github.com/agentscope-ai/QwenPaw/issues/6436)** (13 days old): A high-concept feature request with no maintainer engagement yet; needs a triage response on whether this is planned or should be plugined.
- **[#6392 — Agent-Level Token Statistics](https://github.com/agentscope-ai/QwenPaw/issues/6392)** (14 days old): A feature request asking for more granular token usage reporting, also unanswered. Needs a maintainer disposition.
- **[#6627 — Loongsuite Tracing Integration](https://github.com/agentscope-ai/QwenPaw/issues/6627)** (5 days old): A question about using Alibaba's `loongsuite-python` for LLM tracing with QwenPaw; the existing AgentScope docs are not directly applicable. Needs a community/maintainer answer.
- **[#5603 — Large Tool Output Freezing](https://github.com/agentscope-ai/QwenPaw/issues/6700)**: While marked closed, the user community may expect a documented solution or longer-term fix for output truncation/pagination, given the severity.

**Blockers for v2.1.0 stable**: The Windows `PYTHONHOME` injection (#6697) and Browser SDK (#6698) crashes must be fixed before any stable v2.1.0 release, as they break the core desktop experience on a major platform.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-06

## 1. Today's Overview

ZeroClaw is in a sustained high-activity period with 50 issues and 50 PRs updated in the last 24 hours. The project is currently executing a finite v0.8.5 stabilization line (intake frozen August 4) while simultaneously shepherding a large batch of RFCs through maintainer review, with at least ten open RFCs awaiting decisions. The backlog is dominated by security/architecture work: authentication, shell policy, path forbidden patterns, and channel authorization dominate both issues and PRs. A significant cluster of `needs-author-action` PRs (roughly 15 of the top 30) suggests contributor responsiveness is becoming a bottleneck. Notably, one merged/closed PR today indicates the project is moving on at least one front, while the zero new releases confirms we are mid-stabilization rather than at a release boundary.

## 2. Releases

**No new releases in the last 24 hours.** The last known milestone context is v0.8.5 (stabilization line through August 30, 2026) and v0.9.0 (auth, security, gateway, and breaking-change queue).

---

## 3. Project Progress

One PR merged/closed in the last 24 hours:

- **[#9750 (merged) fix(service): bound launcher-owned daemon logs**](https://github.com/zeroclaw-labs/zeroclaw/pull/9750) — Replaces unbounded fixed-file daemon redirection with a shared service supervisor using bounded 8 MiB nonblocking queues. This addresses a stability/disk-exhaustion class of bug. **Follow-up:** [#9773](https://github.com/zeroclaw-labs/zeroclaw/pull/9773) applies the same bounded-log approach to macOS launchd specifically.

**Actively advancing (open, but with forward motion):**

- **[#9777 fix(channels): accept Signal source UUID senders**](https://github.com/zeroclaw-labs/zeroclaw/pull/9777) — New fix (created today) for the S1 signal-channel silent-drop bug #9774. Small PR, addresses `sourceUuid`-only senders.
- **[#9776 feat(security): extend forbidden_paths with workspace-relative glob patterns**](https://github.com/zeroclaw-labs/zeroclaw/pull/9776) — New feature (created today) referencing RFC #8424, adding `ForbiddenPatternSet` categorization of globs, exact paths, directory prefixes, and basenames.
- **[#9748 fix(runtime): prevent stale provider refreshes from mutating replacement sessions**](https://github.com/zeroclaw-labs/zeroclaw/pull/9748) — Generation-counter approach for #9719 session replacement races.
- **[#9420 fix(anthropic): support stored OAuth profiles](https://github.com/zeroclaw-labs/zeroclaw/pull/9420)** — Large XL PR adding explicit `auth_mode = "oauth"` for Anthropic with revocation and per-alias credential resolution.

**Docs/CI:** [#9778](https://github.com/zeroclaw-labs/zeroclaw/pull/9778) (reconcile FND docs revision histories, small), [#9717](https://github.com/zeroclaw-labs/zeroclaw/pull/9717) (release attestation action pin), [#9755](https://github.com/zeroclaw-labs/zeroclaw/pull/9755) (workspace-wide no-default-features warnings enforcement).

---

## 4. Community Hot Topics

| Issue | Comments | Topic |
|---|---|---|
| [#6808 RFC: Work Lanes, Board Automation, Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) | 18 | Governance RFC — routing work without adding maintainer overhead. In "ratification deferred / rollout in progress" state. |
| [#8303 RFC: Goal mode v1 — bounded foreground Matrix work](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) | 18 | Durable multi-turn user objective pursuit; earlier coupling with restart handoff / Web / async child work was too broad. |
| [#8603 RFC: ZeroClaw Chat Completions profile](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) | 16 | OpenAI-compatible REST surface for Open WebUI, LobeChat, Aider, LangChain; 2 weeks old, high demand signal. |
| [#7155 RFC: per-execution confirmation for high-risk shell + allow/ask/deny policy](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) | 16 | Claude Code-style command-policy. Scope narrowed to shell-policy contract at Rev 3 (2026-08-05). |
| [#7141 RFC: Pluggable inbound authentication and canonical principals](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) | 12 | Rev 8 — security/architecture core for v0.9.0 identity milestone. |
| [#8692 Tracker: Maintainer decision queue for RFCs and design issues](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) | 11 | The central decision backlog; updated today (2026-08-06). |
| [#9487 RFC: Runtime-owned conversation sessions + transport surface adapters](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) | 10 | Rev 2 (2026-08-03): ratifies #9487/#9488/#9600 ownership boundary; all entry points submit `InboundAction`. |

**Analysis:** The community is actively pushing on three fronts: (1) **security posture** (shell policy, auth, forbidden paths) — these are the most commented RFCs; (2) **compatibility surface** (Chat Completions profile) — strong eco-system demand; (3) **governance/process** — the maintainer decision queue (#8692) and work-lane RFC (#6808) show a community trying to manage its own throughput. The decision queue is the single most important issue right now; every open RFC is waiting there.

---

## 5. Bugs & Stability

**New today (2026-08-05/06):**

| # | Sev | Component | Summary | Fix PR |
|---|---|---|---|---|
| [#9775](https://github.com/zeroclaw-labs/zeroclaw/issues/9775) | S1 — workflow blocked | Provider (OpenRouter) | `stream_chat` serializes `NativeChatRequest` directly, skipping `merge_extra_body`; configured `provider_extra` dropped on all streaming requests. | **No PR yet — open.** |
| [#9774](https://github.com/zeroclaw-labs/zeroclaw/issues/9774) | S1 — workflow blocked | Signal channel | Silently drops inbound envelopes where sender is `sourceUuid`-only (both `source` and `sourceNumber` null). | **PR #9777** (open today) |
| [#9768](https://github.com/zeroclaw-labs/zeroclaw/issues/9768) | S2 — degraded | Runtime/daemon (SIGUSR1) | `daemon reload` not on SIGUSR1; degraded-security warning tells operators to send a signal that actually kills the daemon. | **No PR yet — open.** |
| [#9771](https://github.com/zeroclaw-labs/zeroclaw/issues/9771) | Tooling | zeroclaw-gateway | Clippy `-D warnings` fails on default feature surface — test helpers gated `#[cfg(test)]` but call sites behind `#[cfg(feature = "channel-linq")]` → dead code. | **No PR yet — one-line fix identified.** |

**Highly active bug trackers:**

- **[#8642 MCP/tool-schema cloning drives unbounded RSS growth**](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) (S1, accepted, in-progress) — OOM class bug; split from #5542. Requires tool-policy + memory-delivery predicates applied to pipeline children (PR #9737 may be partial fix).
- **[#9697 ZeroCode cannot connect to daemon launched by Windows Task Scheduler**](https://github.com/zeroclaw-labs/zeroclaw/issues/9697) (S3, accepted) — persistent Windows environment issue from #9117.
- **[#9462 zeroclaw-plugins lib unit tests behind plugins-wasmtime feature never execute in CI**](https://github.com/zeroclaw-labs/zeroclaw/issues/9462) — **CLOSED today** with 3 comments (likely fixing action).
- **[#9328 verifiable-intent evaluates constraints without verifying credential chain**](https://github.com/zeroclaw-labs/zeroclaw/issues/9328) (accepted, risk-high) — `vi_verify`'s `evaluate_constraints` checks L2 constraints against caller-provided fulfillment without cryptographic chain verification. Related follow-up #9769 (withheld-capability notice not visible when log persistence off).

**Vulnerability-adjacent security bugs:** [#9428](https://github.com/zeroclaw-labs/zeroclaw/pull/9428) (Bluesky/Reddit senders never authorizing — P1, needs-author-action), [#9678](https://github.com/zeroclaw-labs/zeroclaw/pull/9678) (Git shell policy argument hardening — P1), [#8826](https://github.com/zeroclaw-labs/zeroclaw/pull/8826) (image_gen SSRF — P2).

---

## 6. Feature Requests & Roadmap Signals

**Likely v0.9.0 (per #7432 tracker and RFC momentum):**

- **Pluggable inbound authentication + canonical principals** [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) — OIDC and pluggable providers. Rev 8, high-priority P1, still `needs-maintainer-review`.
- **Per-execution shell confirmation / pattern policy (allow/ask/deny)** [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) — Claude Code-style policy; scope final narrowing at Rev 3. P1.
- **Empty WhatsApp Web `allowed_groups` = permit-none** [#9397](https://github.com/zeroclaw-labs/zeroclaw/issues/9397) — small P1 security default change, in-progress, likely to land soon.
- **Anthropic stored-profile OAuth alias contract** [#9464](https://github.com/zeroclaw-labs/zeroclaw/issues/9464) — recorded contract for #9420; in-progress.

**High-demand features that could land in v0.8.5/v0.9.0:**

- **OpenAI Chat Completions profile** [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) — 16 comments in a month. If accepted, opens the door for the entire OpenAI-API ecosystem tooling. Strong candidate (P2, no-stale).
- **Stable `session_id` for OpenRouter prompt caching** [#9631](https://github.com/zeroclaw-labs/zeroclaw/issues/9631) — cost-saving, concrete win for heavy OpenRouter users. P2.
- **Goal mode v1 (bounded foreground Matrix work)** [#8303](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) — durable multi-turn objectives; v1 is intentionally bounded (no restart handoff, no async child work). P2.
- **Data-wrapped OpenAI-compatible responses** [#9335](https://github.com/zeroclaw-labs/zeroclaw/issues/9335) — **CLOSED**, implying implementation completed or accepted.

**Watch: workspace-relative forbidden paths** [#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) — fix PR #9776 opened today. This was `needs-author-action`; now has a concrete implementation to review.

---

## 7. User Feedback Summary

**Pain points expressed (unfiltered):**

- **Signal channel drops messages silently** (#9774, S1): operator "nothing happens" scenario — the worst kind of channel failure.
- **OpenRouter streaming silently ignores `provider_extra`** (#9775, S1): users paying for streaming get different (unconfigured) behavior vs. non-streaming — configuration surprise costs money.
- **SIGUSR1 reload traps** (#9768): the error message actively instructs operators to perform a **destructive** action (kill daemon) instead of reload — this is an active operator trust hazard.
- **Windows Task Scheduler daemon connection** (#9697): recurring pain on Windows (third instance of this class).
- **ZeroCode string editing** [#7467](https://github.com/zeroclaw-labs/zeroclaw/issues/7467) — CLOSED today — fixed; users can now navigate with arrow keys while editing strings.
- **Config CLI hyphen-alias bug** [#9652](https://github.com/zeroclaw-labs/zeroclaw/issues/9652) — CLOSED today — `config set` rejected cron keys with hyphens while `list`/`get` read them.

**Satisfaction signals:** the high volume of RFC activity (18+ comments on several) and the fact that users are proactively drafting RFCs (many with "drafted with Claude/Codex, sponsored by X") suggests a healthy, engaged, governance-aware community. The existence of a maintainer decision queue (#8692) and contributor-role taxonomy (distinguished contributor, principal contributor, trusted contributor) further suggests a maturing contributor funnel.

**Frustration (implicit):** the sheer number of `needs-author-action` PRs (~15 of top 30) suggests contributors are abandoning or paused on their work — likely a maintainer-review or response-time bottleneck; the RFC queue being "ratification-deferred" (e.g., #6808) compounds this.

---

## 8. Backlog Watch

Items needing maintainer attention (long-quiet or high-risk open):

| # | Item | Age | Why it matters |
|---|---|---|---|
| [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) | Maintainer decision queue | Updated today | The single coordination point for ~15 open RFCs; was "accepted" and updated today — watching whether decisions start flowing. |
| [#6909 RFC: Computer-use (desktop) support](https://github.com/zeroclaw-labs/zeroclaw/issues/6909) | Since 2026-05-25 | 10+ weeks, `needs-author-action` — desktop screen interaction is a major capability gap vs. competitive agents. |
| [#6954 RFC: Provenance/reply contract for internal turns](https://github.com/zeroclaw-labs/zeroclaw/issues/6954) | Since 2026-05-26 | Rev 2 with 4 boundary clarifications; critical for cron/scheduled agent work correctness. |
| [#8832 RFC: Plugin-owned Kanban board](https://github.com/zeroclaw-labs/zeroclaw/issues/8832) | Since 2026-07-08 | Cross-cutting agent-work coordination feature, still `needs-maintainer-review`. |
| [#9487 RFC: Runtime-owned conversations](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) | Since 2026-07-28 | Rev 2 ratified ownership boundary with #9488/#9600; still no decision. |
| [#8424 RFC: Workspace forbidden paths](https://github.com/zeroclaw-labs/zeroclaw/issues/8424) | Since 2026-06-28 | Now has a **new fix PR #9776** — highest-priority review item from this digest, as a merge would close both the RFC and the feature gap. |
| [#8907 (implied from #8603)](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) | n/a | Chat Completions profile remains undecided — this is the single most externally-visible compatibility ask. |

**Long-waiting PRs (stale `needs-author-action` — risk of rot):**

- [#9443 / #9548 / #9477 / #8496 / #8826](https://github.com/zeroclaw-labs/zeroclaw/pull/9548) — all have been idle for 7+ days; all are security-relevant (Codex CLI args, tool-call parsing, MCP access, SSRF). These should be pulled into the v0.8.5 finish line if maintainer bandwidth allows.

---

**Overall Health Assessment:** ZeroClaw is healthy but **maintainer-constrained**. The community is producing high-quality RFCs, security fixes, and channel fixes at a rate that outstrips review capacity. The immediate watch item is the decision queue (#8692) and whether the RFC wave results in acceptances (driving to v0.9.0) or deferrals (risking contributor burnout). The security posture is improving measurably (Signal UUID fix, Bluesky/Reddit auth, Git shell hardening, SSRF gating), which is good news for a project with a high-surface runtime. The v0.8.5 stabilization line (frozen intake, weekly cuts) is discipline the project clearly needs.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*