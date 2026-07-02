# OpenClaw Ecosystem Digest 2026-07-02

> Issues: 277 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-02 02:00 UTC

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

# OpenClaw Project Digest — 2026-07-02

## Today's Overview
Project activity remains at an elevated level with 277 issues updated and 500 PRs updated in the last 24 hours, indicating a high-velocity development cycle. The open-to-closed ratio for issues (168:109) suggests the maintainer team is actively triaging but the backlog continues to grow, particularly for higher-severity items. Notably, 438 of 500 PRs remain open, pointing to a significant review bottleneck. No new releases were made today, but the volume of regression-related reports (at least 5 in the last 48 hours) suggests the community is actively testing `v2026.6.11` and encountering post-release issues. The project appears to be in a stabilization phase following the recent major release, with memory subsystem, session initialization, and provider integration issues dominating the bug landscape.

## Releases
No new releases were published today. The most recent version remains **2026.6.11**, which appears to have introduced several regressions now being actively investigated.

## Project Progress
In the last 24 hours, **62 PRs were merged or closed**, demonstrating steady maintenance throughput. Key merged/closed items include:
- **[PR #98244](https://github.com/openclaw/openclaw/pull/98244)** — fix for 120-second timeout in OpenAI Responses API streaming
- **[PR #98467](https://github.com/openclaw/openclaw/pull/98467)** — file descriptor leak fix in `readUtterancesFromDir` stream cleanup
- **[PR #98745](https://github.com/openclaw/openclaw/pull/98745)** — fix for "reply session initialization conflicted" with GLM-5.2 cloud model (closed as completed)
- **[PR #98834](https://github.com/openclaw/openclaw/pull/98834)** — bounded OAuth token JSON reads for OpenAI Codex paths
- Multiple "bound JSON response reads to prevent OOM" PRs across Feishu, Google Meet, HuggingFace, and Discord integrations (open, awaiting review)

Several significant open PRs are progressing through review:
- **[PR #98236](https://github.com/openclaw/openclaw/pull/98236)** — large refactor to flip sessions and transcripts to SQLite storage (marked "do not merge," awaiting author)
- **[PR #61306](https://github.com/openclaw/openclaw/pull/61306)** — "Claw: add mission control backbone" — stalled for months, still needs proof
- **[PR #98239](https://github.com/openclaw/openclaw/issues/98239)** — fix for `/pair qr` breaking Tailscale Serve webchat (linked PR #98239 closed, but issue remains open)

## Community Hot Topics

### Most Active Issues
| Issue | Title | Comments | Reactions |
|-------|-------|----------|-----------|
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | Embedded runner: freshly streamed thinking signatures intermittently invalid on replay (Anthropic) | 17 | 1 👍 |
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | Memory Trust Tagging by Source | 13 | 0 |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | Pre-reset agentic memory flush | 11 | 4 👍 |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | "Cannot convert undefined or null to object" regression with google-vertex/gemini-3.1-pro-preview | 10 | 3 👍 |
| [#94228](https://github.com/openclaw/openclaw/issues/94228) | Native Anthropic: replaying historical thinking blocks bricks long tool-use threads | 10 | 2 👍 |

**Underlying needs analysis:**
1. **Memory system reliability** dominates across all hot topics. Issues #7707, #45608, and #40418 all touch on trustworthiness and persistence of agentic memory — users need memory that is both persistent across sessions and resistant to poisoning from untrusted sources. The community is signaling that OpenClaw's memory architecture, while powerful, lacks sufficient safety rails for production use.
2. **Anthropic provider stability** (#92201, #94228) represents a critical integration pain point. Users relying on Anthropic's thinking blocks face intermittent signature validation failures that brick long-running sessions. The root cause appears to be in the replay/serialization layer, not the provider API itself.
3. **Session lifecycle management** (#45608) continues to be a theme — users want `/new` and resets to trigger proper memory flush before destroying context, mirroring behavior that already exists for compaction.

## Bugs & Stability

### Critical/High Severity (P1 — new or still open)

| Issue | Summary | Has Fix PR? | Status |
|-------|---------|-------------|--------|
| [#98672](https://github.com/openclaw/openclaw/issues/98672) | Sessions breaking constantly after 2026.6.11 upgrade | **PR #98835** open | Needs proof |
| [#98416](https://github.com/openclaw/openclaw/issues/98416) | v2026.6.11 published dist missing reentrancy guard — reply session conflicts | No | Needs review |
| [#98528](https://github.com/openclaw/openclaw/issues/98528) | Tool output returns empty after first call per turn (2026.6.11 regression) | No | Needs info |
| [#98740](https://github.com/openclaw/openclaw/issues/98740) | Mattermost native slash commands return 401 after 6.11 plugin externalization | No | Needs review |
| [#98565](https://github.com/openclaw/openclaw/issues/98565) | Container image upgrades skip openclaw upgrade migrations | No | Needs decision |
| [#97983](https://github.com/openclaw/openclaw/issues/97983) | iOS/WebChat messages append but don't trigger assistant replies | No | Needs review |
| [#98239](https://github.com/openclaw/openclaw/issues/98239) | `/pair qr` changes gateway.bind and breaks Tailscale Serve webchat | Closed PR | Needs security review |

### Notable Regressions (from 2026.6.11 launch)
- **#98672, #98416, #98528** — All surfaced within the last 24 hours and appear to be distinct issues, suggesting incomplete testing coverage before the `v2026.6.11` release.
- **#98740** — The Mattermost plugin externalization (a breaking change) did not coordinate slash command token registration properly.
- **#98528** — Tool output regression may be related to PR #98236's SQLite storage flip, though that PR is marked "do not merge."

### Emerging Pattern: OOM Prevention Fixes
A concerning trend: at least **8 PRs** in the last 24 hours address unbounded JSON response reads across different integrations (Feishu, Google Meet, HuggingFace, OpenAI Codex, browser CDP, Voyage, Nextcloud Talk, Discord). This suggests a systematic security review uncovered a class of memory exhaustion vulnerabilities, and the project is now applying fixes across the codebase.

## Feature Requests & Roadmap Signals

### High-Impact Feature Suggestions
1. **[Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)** (#7707, Diamond Lobster rating) — Tag agent memory by trust level based on origin. This addresses a fundamental security concern and is likely to be prioritized given the recent focus on memory system hardening.

2. **[Automated Session Memory Preservation & Synthesis](https://github.com/openclaw/openclaw/issues/40418)** (#40418) — Automatic memory preservation across session resets. This is a natural companion to #45608 (pre-reset memory flush) and could appear together in a future memory lifecycle improvement release.

3. **[Topic-session families](https://github.com/openclaw/openclaw/issues/90916)** (#90916) — Multiple named context lanes for one assistant. This is a significant architectural change that would address a common user pain point of losing context when switching topics, but likely late-stage given the complexity.

### Predictions for Next Release
Based on PR velocity and maintainer attention patterns:
- **Likely in v2026.6.12:** The reentrancy guard fix (#98416), reply-session initialization conflict fix (#98835/preview), and the batch of OOM prevention PRs across integrations.
- **Possible but not guaranteed:** Memory flush on reset (#45608) if maintainers prioritize it as a security fix for memory poisoning vectors.
- **Unlikely:** The SQLite storage flip (PR #98236) is massive and still awaiting author updates.

## User Feedback Summary

### Pain Points (high dissatisfaction signals)
1. **Post-6.11 instability** — Multiple users reporting sessions "breaking constantly" (#98672), tool outputs empty after first call (#98528), and reply initialization conflicts (#98416). These are *new* regressions that degrade the core experience.
2. **Memory trust deficit** — Users are concerned about memory poisoning (#7707, #84466). One report documents MEMORY.md loading in Discord guild channels despite documentation stating it shouldn't (#84466), violating user expectations.
3. **Mobile/native experience gap** — iOS/WebChat users report messages not triggering replies (#97983, 4 days old, still unaddressed). This affects the growing mobile user base.
4. **Subagent/MCP tool isolation** — Users investing in the MCP ecosystem are hitting walls where tools don't propagate to subagent sessions (#85030), limiting composability.

### Positive Signals
- High community engagement with 277 issues updated in 24h shows a healthy, active user base.
- Multiple users are contributing fix PRs, indicating strong community developer participation (e.g., PR #98840 by solodmd, PR #98711 by ZengWen-DT).
- The rapid response to the OOM vulnerability class (8+ PRs in 24h) suggests maintainers are taking security seriously.

## Backlog Watch

### Critical Long-Open Issues Awaiting Maintainer Review
| Issue | Age | Severity | Last Update | Status |
|-------|-----|----------|-------------|--------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) | ~5 months | Diamond Lobster (P2) | 2026-07-01 | Needs maintainer review, needs product decision, needs security review |
| [#20935](https://github.com/openclaw/openclaw/issues/20935) | ~4.5 months | Diamond Lobster (P2) | 2026-07-01 | Needs maintainer review, needs product decision, needs security review |
| [#38327](https://github.com/openclaw/openclaw/issues/38327) | ~4 months | Platinum Hermit (P1) | 2026-07-02 | Needs maintainer review, needs product decision, needs live repro |
| [#45608](https://github.com/openclaw/openclaw/issues/45608) | ~3.5 months | Diamond Lobster (P2) | 2026-07-01 | Needs maintainer review, needs product decision, needs security review |
| [#40418](https://github.com/openclaw/openclaw/issues/40418) | ~3.5 months | Diamond Lobster (P2) | 2026-07-01 | Needs maintainer review, needs product decision, needs security review |

All five of these top-backlog issues carry `clawsweeper:no-new-fix-pr`, `clawsweeper:needs-maintainer-review`, and `clawsweeper:needs-product-decision` labels — meaning they are stuck in a review/decision bottleneck despite being rated as high-impact. This pattern suggests that the maintainer team is prioritizing incoming critical bugs over long-standing feature requests and improvements, which is rational given the current regression wave but leaves users who invested time in these requests without visibility on timelines.

### PRs Stale for >30 Days Awaiting Maintainer Action
- **[PR #73199](https://github.com/openclaw/openclaw/pull/73199)** (104 days, hook capability smoke gate) — status: "waiting on author"
- **[PR #55596](https://github.com/openclaw/openclaw/pull/55596)** (97 days, CJK markdown table columns) — status: "waiting on author"
- **[PR #55901](https://github.com/openclaw/openclaw/pull/55901)** (97 days, IRC markdown support) — status: "waiting on author"
- **[PR #54724](https://github.com/openclaw/openclaw/pull/54724)** (99 days, agent model selection fix) — status: "waiting on author"

These PRs all carry the `waiting on author` status, but given the age, it's unclear whether authors have been asked for revisions recently or if these have simply been deprioritized. The project could benefit from a stale PR cleanup policy to either close or re-engage these contributors.

### Honorable Mentions
- **[Issue #13615](https://github.com/openclaw/openclaw/issues/13615)** (142 days, rate limiting/throttling for external API calls) — Diamond Lobster, 2 👍, still no PR. Given the growing reliance on external APIs (Anthropic, OpenAI, MCP servers), this is a production-readiness gap.
- **[Issue #87058](https://github.com/openclaw/openclaw/issues/87058)** (37 days, Android node connects but advertises zero commands) — Diamond Lobster P1, needs security review. This affects the mobile ecosystem expansion goal.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided digests.

---

### Cross-Project Comparison Report: Personal AI Agent Ecosystem

**Date:** 2026-07-02

---

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem is characterized by intense, high-velocity development focused on stabilizing core architectures after a wave of major releases. The landscape is bifurcated between a dominant, complex platform (OpenClaw and its direct derivatives) and a set of smaller, more experimental projects (NanoBot, Hermes Agent) that are innovating in specific areas like memory and autonomy. A common thread across nearly all projects is the pressure to move from interactive chat to reliable, autonomous task execution, with significant pain points emerging around memory management, provider reliability, and security hardening. The community is sophisticated, actively contributing both bug fixes and substantial architectural RFCs, signaling a mature and committed user base that is pushing the boundaries of what these agents can do.

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 277 (168 open) | 500 (438 open) | **v2026.6.11** (recent, regressions) | 🟡 **Moderate** (High activity, severe review bottleneck, post-release regressions) |
| **NanoBot** | 8 (5 open) | 47 (22 merged) | Last release pre-dates report | 🟢 **Strong** (High throughput, rapid bug fixes, clear roadmap) |
| **Hermes Agent** | 50 (44 open) | 50 (42 open) | **v0.18.0** (Jul 1, major release) | 🟢 **Strong** (Post-release stabilization, fast fix turnaround, high community involvement) |
| **PicoClaw** | 2 | 11 (2 merged) | **Nightly** (v0.3.1-nightly) | 🟡 **Moderate** (Healthy, but critical bugs lack PRs; security hardening in progress) |
| **NanoClaw** | 6 | 12 (6 merged) | None | 🟢 **Strong** (Consolidation phase, high contributor reward, critical UX bugs surfaced) |
| **NullClaw** | 0 | 0 | **v2026.4.17** | 🔴 **Stagnant** (No activity for 24h; sole open issue is 2+ months old) |
| **IronClaw** | 24 (17 open) | 50 (28 merged) | Release PR open | 🟡 **Moderate** (Intense bug-bash, high merge rate, but multiple P1/P2 failures) |
| **LobsterAI** | Data missing (4 open) | 25 (21 merged) | None | 🟢 **Strong** (High activity, major backlog clearance, engaged power users) |
| **CoPaw** | 22 (17 open) | 50 (27 merged) | **v1.1.12 / v2.0.0b2** | 🟢 **Strong** (High merge cadence, v2.0 converging, active community contributions) |
| **ZeroClaw** | 50 (84 total) | 50 (44 open) | Unchanged | 🟡 **Moderate** (Intense development, 5 S1 bugs open, security hardening active) |

### 3. OpenClaw's Position

- **Advantages & Scale:** OpenClaw is the clear center of gravity, with a community and activity level (500 PRs, 277 issues in 24h) that dwarfs all other projects by an order of magnitude. Its rich feature set and extensive integration ecosystem make it the most versatile platform.
- **Technical Approach:** The project is in a stabilization phase following its major `v2026.6.11` release. It is grappling with the complexity of its own success, facing a significant review bottleneck (87% of PRs remain open) and a wave of post-release regressions that are degrading the core experience.
- **Community vs. Peers:** OpenClaw's community is the most active, but also the most stressed. While NanoBot and Hermes Agent show higher per-contributor productivity and faster response times on specific issues, OpenClaw's maintainer team is spread thin, leading to a backlog of critical, long-unaddressed feature requests (e.g., memory trust tagging). Its ecosystem includes both direct derivatives (PicoClaw, NanoClaw) and conceptual peers (IronClaw, ZeroClaw) that are building complementary or competitive architectures.

### 4. Shared Technical Focus Areas

A consensus on key challenges is emerging across the ecosystem:

- **Memory System Reliability:** **OpenClaw (#7707, #45608)** and **NanoBot (#4621, #4626)** are both redesigning memory architectures for trustworthiness, persistence, and session lifecycle management. The community demands fail-safe mechanisms against memory poisoning and reliable flush on reset.
- **Provider & API Stability:** **OpenClaw** (Anthropic thinking blocks, Google Vertex), **NanoBot** (OpenAI Response API), and **CoPaw** (9router proxy) all report significant integration pain with specific commercial model providers. This is a universal friction point.
- **Tool/Agent Isolation & Security:** **ZeroClaw** (MCP tool visibility, zip-bomb vulnerability), **PicoClaw** (exec sandbox deny-pattern bypass), and **Hermes Agent** (silent terminal tool loss) are all hardening their tool execution environments and governance boundaries.
- **Post-Release Regression Management:** **OpenClaw**, **Hermes Agent**, and **IronClaw** are all in a "bug bash" phase following major releases, with the community actively testing and reporting regressions. This indicates a cycle of rapid feature development followed by stabilization sprints.
- **Privilege Escalation & User Control:** **CoPaw** (approval popups despite disable), **Hermes Agent** (denylist bypass), and **IronClaw** (self-referential routine prompts) all point to an urgent need for robust, user-understandable governance models that can prevent autonomous agents from surprising their owners.

### 5. Differentiation Analysis

| Feature / Target | OpenClaw | NanoBot | Hermes Agent | ZeroClaw | CoPaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Target User** | Power users, integrators | Claude-centric power users | Autonomy-focused developers | Rust-backend enthusiasts | Enterprise, cross-platform |
| **Core Architecture** | Monolithic (Node.js) | Modular, high-velocity | Monolithic, feature-rich | Rust core, WASM plugins | Dual-track (v1/v2), MCP-heavy |
| **Primary Innovation** | Ecosystem scale, integrations | Subagent orchestration, memory | True autonomy, cron-to-chat | Durable memory, OCI plugins | Governance, loop engineering |
| **Key Weakness** | Review bottleneck, regression cycle | Release cadence unknown | Windows stability, Discord TTS | Web UI gaps, S1 bugs | Feishu integration maturity |
| **Language / Stack** | Node.js | Node.js | Node.js | Rust | Python / Node.js |

### 6. Community Momentum & Maturity

- **Tier 1: High-Velocity Iteration (Rapidly Evolving)**
    - **NanoBot** and **Hermes Agent** are in an intensive phase of feature development and infrastructure hardening, with high PR merge rates and fast response times to critical bugs. Their roadmaps are aggressive and executing.
- **Tier 2: Stabilization & Consolidation (Scaling to Production)**
    - **OpenClaw**, **IronClaw**, **ZeroClaw**, and **CoPaw** are dealing with the hangover of rapid growth or major releases. Activity is high, but the focus is shifting from adding features to fixing regressions, hardening security, and addressing review backlogs. This is a necessary maturation step.
- **Tier 3: Niche & Stagnant (Lower Activity)**
    - **PicoClaw** and **NanoClaw** show healthy but lower activity, focusing on targeted improvements and platform-specific fixes (mobile, first-run experience). **NullClaw** is effectively stagnant, a potential risk for users relying on it.

### 7. Trend Signals

1.  **From Interactive Chat to Autonomous Execution:** The highest-value feature requests are no longer about better chat UI, but about reliable background execution. The demand for "True Autonomy" (**Hermes Agent #5712**), "Goal Mode" (**ZeroClaw #8303**), and automated session memory (**OpenClaw #40418**) signals that the industry is pivoting from co-pilots to persistent auto-pilots.

2.  **The "LLM-as-OS" Convergence:** The concept of AI models as a new operating system layer is becoming concrete. **LobsterAI (#2239)** explicitly discusses "OpenClaw-ification" of coding tools. **ZeroClaw (#8568)** proposes a "Mixture-of-Agents," treating models as components to be composed. Developers are building orchestration layers on top of models, not just chatting with them.

3.  **Security is the Onboarding Wall:** The ecosystem is collectively realizing that agent trust and safety are the biggest barriers to production deployment. Issues like memory poisoning (**OpenClaw #7707**), governance bypass (**CoPaw #5703**), and zip-bomb vulnerabilities (**ZeroClaw #8554**) show that the industry is moving from "can it do this?" to "can it do this *safely*?"

4.  **Performance is a Feature, Not a Bug:** Users are starting to push back on token waste and latency. **Hermes Agent (#13983)** complains about "16K tokens for 'who u?'" and **LobsterAI (#2243)** tracks a file watcher causing "massive token waste." The next competitive differentiator will be efficiency, not just capability.

5.  **The Rise of the "Self-Hosted" Developer:** The critical bugs in **NanoClaw (#2903, #2902)** specifically target first-run experience in Docker, and **PicoClaw (#3164)** is blocking all mobile users. This reveals a large, underserved, and demanding user base that wants to own and control their agent infrastructure, a segment that will reward projects that prioritize ease of deployment and robust error handling.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-02

## 1. Today's Overview

NanoBot is experiencing a **high-activity day** with a surge in development output: **47 Pull Requests** were updated in the last 24 hours, of which **22 were merged or closed** alongside **8 Issues** (5 active, 3 closed). The project shows strong momentum in infrastructure hardening, memory subsystem improvements, and test coverage expansion. A notable security vulnerability (MCP deny-all bypass, issue #4434) was closed, indicating recent security-focused maintenance. With **no new releases** but heavy PR activity across multiple domain areas, the project is in a **intensive development phase** with visible progress toward stability and feature completeness.

## 2. Releases

**No new releases today.** The last tagged release predates this reporting period. The high volume of merged PRs (22) suggests a release may be approaching as maintainers finalize features and fixes.

## 3. Project Progress

**22 PRs merged/closed today**, representing significant forward progress:

### Testing & Quality Infrastructure
- **#3982 / #4631** — Scripted agent runner harness (merged, re-opened new version)
- **#3983 / #4630** — Runner coverage for blocked tool-call finish reasons (merged)
- **#4193 / #4628** — Memory lifecycle harness for end-to-end session testing (merged)
- **#4633** — Regression test for cron multi-instance stale snapshot consistency

### Security & Reliability
- **#4119 / #4629** — Block relative symlink workspace escapes in exec (merged, re-opened)
- **#4434** [CLOSED] — MCP `enabledTools` deny-all bypass vulnerability fix (security advisory closed)
- **#4490** [CLOSED] — Require auth when OpenAI-compatible API binds to all interfaces
- **#4615** [CLOSED] — Gateway crash fix for `os.fsync()` on parent directory (CronService)

### Feature Development
- **#4632** [OPEN] — Add Anthropic OAuth provider support
- **#4623** [OPEN] — Subagent spawn model override
- **#4621** [OPEN] — Gate archive facts with provenance context in memory
- **#4626** [OPEN] — Opt-in eager memory consolidation
- **#4620** [OPEN] — Heartbeat trigger command for LLM-driven scheduled tasks

## 4. Community Hot Topics

**Most Active Issues:**

- **#4604** [OPEN] **Anthropic OAuth** — Feature request with 3 comments. Discussion references a community discussion (#4593). Shows demand for OAuth-based Anthropic access alongside traditional API keys. Likely connected to PR #4632 which adds this exact feature.

- **#4615** [CLOSED] **Gateway crash on `os.fsync()`** — 2 comments, resolved quickly. Users reported startup crash on Windows/Unix systems where `fsync()` on parent directory FD fails. Fix was merged same day.

- **#4434** [CLOSED] **MCP security bypass** — 2 comments. Security advisory with likely high impact. The bypass exposed MCP resources and prompts to the model even with `enabledTools: []`. Now closed, indicating remediation.

**Analysis:** The community is actively engaged with security reports and feature requests. Response time to critical bugs (like #4615) appears rapid. OAuth-based authentication is the most requested non-bug feature, suggesting user base includes individual Claude subscribers who want OAuth convenience.

## 5. Bugs & Stability

| Severity | Issue | Status | Details |
|----------|-------|--------|---------|
| **Critical** | #4434 — MCP security bypass | **CLOSED** | `enabledTools: []` deny-all policy bypass exposed resources/prompts. Fix merged. |
| **High** | #4615 — Gateway crash on startup (CronService `os.fsync()`) | **CLOSED** | Crashed during `os.fsync()` on parent directory FD after `os.replace()`. Cross-platform OS error. Fix merged. |
| **Medium** | #4637 — Telegram long message rendering failure | **OPEN** | Long markdown messages split into trunks; prior trunks cannot render. Platform-specific rendering issue. |
| **Low** | #4634 — `edit_file` target disambiguation failures | **OPEN** | Wrong occurrence edits dominate benchmark failures. Fix PR #4635 in progress with line guards. |

**Security note:** The #4434 MCP bypass is a serious vulnerability — it allowed unrestricted resource/prompt access despite explicit deny configuration. The prompt closure (within 11 days of opening) suggests appropriate priority.

## 6. Feature Requests & Roadmap Signals

**User-requested features in open issues:**

- **#4604** — **Anthropic OAuth** (3 comments, PR #4632 exists) — Most requested; likely in next release
- **#4612** — **OpenAI Response API support** — User cannot connect via compatible API path; wants native Response API
- **#4619** — **Feishu/Lark "New Session" system messages** — Wants visual separation (`msg_type system`) instead of text-only for `/new`

**Detectable roadmap signals from current PRs:**

- **Memory subsystem overhaul** — Multiple PRs (#4626, #4621, #4627) indicate memory consolidation is being redesigned with eager/archive improvements
- **Subagent capabilities expanding** — PRs #4623 (model override) and #4624 (aggregated result mode) suggest subagents gaining production-grade orchestration
- **Authentication maturity** — PR #4632 (Anthropic OAuth) plus closed #4490 (API auth guard) shows platform-level auth standardization
- **Cron system hardening** — PR #4622 (model presets for cron jobs) and testing improvements

**Prediction for next version:** OAuth provider support, eager memory consolidation, subagent aggregated mode, and the heartbeat trigger command have high merge probability.

## 7. User Feedback Summary

**Pain Points Expressed:**

1. **"Cannot use OpenAI Response API"** (#4612) — User is blocked from integration with certain ChatGPT models that only support the Response API path. Indicates a platform gap.
2. **"Long Telegram messages break visually"** (#4637) — Trunked markdown messages cause prior segments to vanish, degrading UX. User submitted a screenshot clearly showing the rendering failure.
3. **"Feishu new session not visually distinct"** (#4619) — The text-only "New session started." is insufficient; users want visual dividers (system messages) for conversation separation.
4. **"edit_file edits wrong occurrence"** (#4634) — Dominant failure mode in edit benchmarks. Developer frustration with exact-match edits hitting wrong targets.

**Satisfaction Signals:**
- Rapid triage and fix of the gateway crash (#4615) suggests operational stability is valued
- Security vulnerability (#4434) was addressed and closed within normal timeframe
- Community engagement on discussions (#4593) indicates active, participatory user base

## 8. Backlog Watch

**High-importance items requiring attention:**

- **#4637** — **Telegram long message rendering** (1 comment, 2 days open) — Affects user experience on Telegram; no fix PR yet
- **#4612** — **OpenAI Response API support** (1 comment, 2 days open) — Platform integration gap that could be a competitive disadvantage
- **#4634** — **edit_file target disambiguation** (0 comments, 1 day open) — Critical for code-writing accuracy; PR #4635 exists but is new

**Long-standing items (older than 7 days):**
- **#4604** — Anthropic OAuth (created 2026-06-30) — Now has PR #4632, so effectively addressed
- **#4434** — MCP security bypass (created 2026-06-21) — Now closed

**Maintainer attention needed:** The Telegram rendering issue (#4637) and OpenAI Response API (#4612) are the most visible open pain points without clear resolution paths. The edit_file benchmark failure (#4634) has a PR but no comments, suggesting it may lack validation.

---

*Project health assessment: **Green/Active**. High contributor velocity, rapid bug fixes, clear roadmap direction in memory/authentication/subagents, and engaged community. Risk factors: No release cadence visible (last release unknown), and some user-facing issues lack maintainer response.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-02  
**Data Snapshot:** GitHub Issues (50 updated in 24h) · PRs (50 updated in 24h) · 1 new release

---

## 1. Today's Overview

Hermes Agent is in a period of **intense, healthy activity**: 50 issues and 50 pull requests were updated in the last 24 hours, reflecting a vibrant open-source community responding to both user feedback and internal roadmap goals. The project just shipped **v0.18.0 ("The Judgment Release")** on July 1st, featuring **949 closed issues** and contributions from **370+ community contributors** — a testament to sustained momentum. However, the volume of open items (44 open issues, 42 open PRs) suggests the team is now in a **consolidation and bug-fixing phase** following the major release, with several regression reports and PRs targeting post-launch stability. The community remains highly engaged, with feature requests around true autonomy and observability drawing the most discussion.

---

## 2. Releases

### Hermes Agent v0.18.0 (v2026.7.1) — The Judgment Release
**Released:** July 1, 2026 | **Commits since v0.17.0:** ~1,720 · **Merged PRs:** 998 · **Files changed:** 2,215 (+251K/-41K) · **Issues closed:** 949 · **Community contributors:** 370+

**Key Changes:**
- Major milestone release with significant scale (nearly 1,000 PRs merged)
- Likely includes the judgment/autonomy features hinted in the release name
- Substantial codebase growth (251K insertions)

**Breaking/Migration Notes:**
- Release notes truncated in data — check full changelog for migration instructions
- Given the volume, users upgrading from v0.17.x should expect config/storage schema changes
- Docker users should note the Exa search backend fix (#49445) was closed on July 2nd, suggesting it was addressed in v0.18.0 or a hotfix

**Recommendation:** Review [full release notes](https://github.com/nousresearch/hermes-agent/releases/tag/v2026.7.1) before upgrading, especially for custom provider and plugin configurations.

---

## 3. Project Progress

### Merged/Closed PRs Today (8 items — fixes and features now live)

| PR# | Type | Description | Component | Impact |
|-----|------|-------------|-----------|--------|
| [#19996](https://github.com/nousresearch/hermes-agent/pull/19996) | Bug Fix | Live model fetching, sorted buttons, dedup, and config fixes for `/model` picker | CLI, Gateway, Discord | Better UX for users with many models (e.g. NVIDIA NIM) |
| [#56734](https://github.com/nousresearch/hermes-agent/pull/56734) | Bug Fix | Disable MSYS path conversion on Windows | Terminal, Windows | Fixes path mangling in Git Bash on Windows CI |
| [#56735](https://github.com/nousresearch/hermes-agent/pull/56735) | Bug Fix | Restore terminal toolset on api_server and acp composites | CLI, Tools | Fixes silent tool loss (#56732) |
| [#56736](https://github.com/nousresearch/hermes-agent/pull/56736) | Refactor | Replace `assert` with explicit check in Codex app-server session | Agent | Production safety with `-O` flag |
| [#56737](https://github.com/nousresearch/hermes-agent/pull/56737) | Bug Fix | Honor configured `auxiliary.<task>.timeout` in `run_oneshot` | Agent, Config | Fixes residual timeout bug from #56322 |
| [#56738](https://github.com/nousresearch/hermes-agent/pull/56738) | Bug Fix | Detect Scoop-installed Git Bash in desktop findGitBash() | Desktop, Windows | Broader Windows compatibility |
| [#56740](https://github.com/nousresearch/hermes-agent/pull/56740) | Bug Fix | Add missing `is_reconnect` parameter to QQ bot adapter | QQ Bot, Gateway | Fixes reconnect crash on QQ platform |
| [#56724](https://github.com/nousresearch/hermes-agent/pull/56724) | Feature | Surface all xAI TTS params in desktop GUI config | Desktop, TTS, xAI | More complete voice configuration UI |

**Notable pattern:** Today's merges focus heavily on **Windows compatibility**, **toolset restoration**, and **platform adapter reliability** — reflecting post-release stabilization priorities.

---

## 4. Community Hot Topics

### Most Active Discussions (by comments & reactions)

| Issue/PR | Comments | 👍 | Topic | Community Sentiment |
|----------|----------|----|-------|--------------------|
| [#5712](https://github.com/nousresearch/hermes-agent/issues/5712) — Feature: True Autonomy — Inject Cron Results into Live Gateway Chat Sessions | 11 | 11 | Desired feature: cron-to-chat bridge | **High demand** — users want background cron results surfaced in real-time chat |
| [#13983](https://github.com/nousresearch/hermes-agent/issues/13983) — Bug: 16K Tokens consumption by default | 6 | 1 | Token bloat concern | **Moderate concern** — users feel base overhead is excessive |
| [#18019](https://github.com/nousresearch/hermes-agent/issues/18019) — Bug: Stream stalled mid tool-call | 5 | 0 | Stream reliability | **Persistent pain point** — regression claimed fixed but still present |
| [#49445](https://github.com/nousresearch/hermes-agent/issues/49445) — Bug: Exa search non-functional in Docker | 4 | 0 | Docker image regression | **Critical for Docker users** — now closed, suggesting fix is live |
| [#56533](https://github.com/nousresearch/hermes-agent/issues/56533) — Bug: `/journey` leaks raw ANSI codes in TUI/Desktop | 4 | 0 | UI rendering bug | **Annoying cosmetic issue** — now closed |

### Analysis of Underlying Needs
1. **True Autonomy (#5712, 11👍):** The community strongly desires **persistent, context-aware background agents** that can bridge cron outputs into ongoing conversations. This signals a pivot from "scheduled tasks" to "always-on assistants."
2. **Performance Transparency (#13983):** Users want **visibility into token consumption composition** — the "why am I burning 16K tokens for a hello?" sentiment is common across LLM tools.
3. **Streaming Reliability (#18019):** Despite a claimed fix, streaming interruptions during large file writes remain a frustration, indicating the fix was incomplete or regression-prone.

---

## 5. Bugs & Stability

### New Bugs Reported Today (high severity)

| Issue | Severity | Component | Description | Fix PR Exists? |
|-------|----------|-----------|-------------|----------------|
| [#56732](https://github.com/nousresearch/hermes-agent/issues/56732) | **P2** | CLI, Tools | API server & ACP composites **silently lose all terminal tools** | ✅ [#56735](https://github.com/nousresearch/hermes-agent/pull/56735) **(merged)** |
| [#56727](https://github.com/nousresearch/hermes-agent/issues/56727) | **P2** | Agent, Kimi | Kimi `/coding` endpoint thinking **incorrectly blocked** for all Kimi endpoints | ✅ [#56730](https://github.com/nousresearch/hermes-agent/pull/56730) |
| [#56717](https://github.com/nousresearch/hermes-agent/issues/56717) | **P2** | CLI | Non-default profile **keeps stale runtime** after update → `ImportError` | ⏳ Open |
| [#56704](https://github.com/nousresearch/hermes-agent/issues/56704) | **P2** | Tools, Linux | `computer_use` capture **crashes on Linux/WSL** — `int(None)` on `pid/window_id` | ⏳ Open |
| [#56733](https://github.com/nousresearch/hermes-agent/issues/56733) | **P2** | Agent, CLI | Deleting sessions can **leave 0-message placeholder rows** | ⏳ Open |
| [#56739](https://github.com/nousresearch/hermes-agent/issues/56739) | **P2** | Telegram | Voice messages **ignored** while `clarify` tool waits for user response | ⏳ Open |
| [#56726](https://github.com/nousresearch/hermes-agent/issues/56726) | **P2** | Desktop, Windows | Desktop app **blank screen, renderer crash loops** on Windows | ⏳ Open |
| [#56673](https://github.com/nousresearch/hermes-agent/issues/56673) | **P2** | MCP, OAuth | Headless MCP OAuth **reconnect hangs** on no-refresh-token credentials | ⏳ Open |
| [#55416](https://github.com/nousresearch/hermes-agent/issues/55416) | **P3** | Plugins, iMessage | Photon iMessage **persistent gRPC RST_STREAM** errors | ⏳ Open |
| [#56729](https://github.com/nousresearch/hermes-agent/issues/56729) | **P3** | TUI | TUI gateway **fails to register shell hooks** and discover plugins | ✅ [#56729](https://github.com/nousresearch/hermes-agent/pull/56729) |

### Key Observations
- **Windows stability** is a recurring theme: 3 of today's high-severity bugs are Windows-specific (terminal path conversion, desktop crashes, Scoop detection)
- **Model provider regressions** (Kimi thinking guard, FIPS crashes) suggest the v0.18.0 release introduced provider-specific regressions
- **Silent tool loss** (#56732) is particularly dangerous — users may not notice until terminal-dependent workflows fail
- **Many new bugs already have fix PRs**, indicating the team is actively triaging post-release regressions

---

## 6. Feature Requests & Roadmap Signals

### User-Requested Features (today)

| Feature | Issue | 👍 | Likelihood for Next Release |
|---------|-------|----|---------------------------|
| **True Autonomy:** Inject cron results into live chat sessions | [#5712](https://github.com/nousresearch/hermes-agent/issues/5712) | 11👍 | **High** — 11 reactions, explicitly requested, aligns with "Judgment Release" theme |
| **Task-aware per-turn model routing** via `pre_llm_call` plugin hook | [#56655](https://github.com/nousresearch/hermes-agent/issues/56655) | 1👍 | **Medium** — sophisticated feature, plugin hook already exists |
| **Worker tool for re-parenting dependencies** before self-closing (kanban pattern) | [#56204](https://github.com/nousresearch/hermes-agent/issues/56204) | 1👍 | **Low-Medium** — niche use case but well-articulated |
| **Desktop App:** Live message sync from other platforms (Telegram, Discord) | [#43625](https://github.com/nousresearch/hermes-agent/issues/43625) | 1👍 | **Medium** — cross-platform UX is strategic |
| **Dashboard font customization** (system fonts as option) | [#54393](https://github.com/nousresearch/hermes-agent/issues/54393) | 0👍 | **Low** — cosmetic, low engagement |

### Prediction for v0.18.1 / v0.19.0
The **True Autonomy** feature (#5712) has strong community resonance and likely aligns with the project's autonomy vision. A **task-aware model routing** plugin hook (#56655) is a natural evolution of the existing plugin system and could ship as experimental. **Windows desktop fixes** are almost certain given the volume of Windows-specific bugs.

---

## 7. User Feedback Summary

### Pain Points (strong signal)
1. **"The default token overhead is insane — 16K for 'who u?'"** (#13983) — Multiple users echoing bloat complaints; suggests per-turn baseline optimization is a priority.
2. **"Stream stalls mid-tool-call are back even though you said it was fixed."** (#18019) — Trust erosion when regressions are re-reported as "already fixed."
3. **"The Docker image Exa search just doesn't work out of the box, and there's no documented workaround."** (#49445) — Now closed, but the frustration of zero-function search in the official image was significant.
4. **"I can bypass the dangerous-command denylist with trivial shell escapes."** (#36846) — Closed, but the severity (P0 security, silent RCE) is concerning — users want robust guardrails.
5. **"Custom providers with self-signed certs fail silently."** (#28260) — Closed, but reflects enterprise users' need for private CA support.

### Positive Signals
- **370+ community contributors** for v0.18.0 — indicates strong health and contributor enthusiasm
- **11 upvotes on True Autonomy feature** — users are investing in Hermes as their long-term agent platform
- **Fast fix turnaround** — several today's bugs already have merged fix PRs (e.g., terminal tool loss fixed same day)

---

## 8. Backlog Watch

### Long-Unanswered Important Issues (need maintainer attention)

| Issue | Created | Age | Last Update | Severity | Why It Matters |
|-------|---------|-----|-------------|----------|----------------|
| [#16693](https://github.com/nousresearch/hermes-agent/issues/16693) — Discord VC TTS plays but user hears nothing | 2026-04-27 | **~66 days** | 2026-07-01 | P2 | Core Discord TTS functionality broken; ffmpeg succeeds but audio silent — likely a Discord API interaction bug |
| [#21710](https://github.com/nousresearch/hermes-agent/issues/21710) — WhatsApp bridge cannot be disabled in Docker + Telegram Forbidden on Windows | 2026-05-08 | **~55 days** | 2026-07-01 | P2 | Docker users stuck with unwanted WhatsApp bridge + cross-platform brokenness |
| [#35527](https://github.com/nousresearch/hermes-agent/issues/35527) — Discord tools silently missing when using `hermes-discord` composite | 2026-05-30 | **~33 days** | 2026-07-01 | P2 | Silent tool loss — users assume tools work but they don't |
| [#44668](https://github.com/nousresearch/hermes-agent/issues/44668) — Windows Desktop stuck at CONNECTING, repair works temporarily | 2026-06-12 | **~20 days** | 2026-07-01 | P2 | Recurring Windows desktop startup failure — core UX issue |
| [#54393](https://github.com/nousresearch/hermes-agent/issues/54393) — Dashboard font customization | 2026-06-28 | **~4 days** | 2026-07-02 | P3 | Lower priority but has no response — user just wants a "system fonts" option |

### Critical Attention Item
The **Discord VC TTS bug (#16693)** is **66 days old with no fix PR** — a core platform feature (Discord voice TTS) remains broken with no visible progress. Given Hermes' heavy Discord user base, this should be prioritized.

---

## Project Health Summary

| Metric | Value | Assessment |
|--------|-------|------------|
| **Recent release** | v0.18.0 (Jul 1) | Major milestone, healthy |
| **Open Issues (24h delta)** | 44 open / 6 closed | Slight backlog growth post-release |
| **Open PRs** | 42 open | Active development, but merging bottleneck |
| **Community contributors** | 370+ (v0.18.0) | Excellent community engagement |
| **Bugs with fix PRs (today)** | 5 of 10 new bugs | Good triage velocity |
| **Long-unanswered P2 bugs** | 4 (avg 44 days) | Needs maintainer attention |
| **Windows stability** | Multiple P2 bugs | Weakest platform support |
| **Security posture** | 1 P0 fixed (#36846), 1 new FIPS crash (#56719) | Generally strong, but ongoing vigilance needed |

**Bottom line:** Hermes Agent v0.18.0 shipped with strong community involvement, but post-release regressions are accumulating. The team's fast fix response (same-day PRs for many new bugs) is commendable. **Windows stability** and **Discord TTS** are the clearest pain points requiring strategic attention. The community's appetite for **true autonomy features** (#5712) signals where the next major focus should be.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-02

## Today's Overview
Project activity is **moderate**, with 11 pull requests and 2 issues updated in the last 24 hours, along with a new nightly release. The project appears healthy, with a balance of feature development, regression fixes, and community-driven quality improvements. A **new nightly build (v0.3.1-nightly)** was published, though flagged as potentially unstable. Key areas of focus include Android/Termux stability, streaming support for the QQ channel, ID normalization, and execution sandboxing. While 9 PRs remain open, several long-standing PRs have seen maintainer attention after periods of inactivity.

## Releases
**New release:** `nightly` — Nightly Build v0.3.1-nightly.20260702.2cf030d2 ([view release](https://github.com/sipeed/picoclaw/releases/tag/v0.3.1-nightly.20260702.2cf030d2))

This is an automated nightly build. No breaking changes or migration notes are provided. Full changelog between v0.3.1 and main is available [here](https://github.com/sipeed/picoclaw/compare/v0.3.1...main). Users are advised to use with caution due to potential instability.

## Project Progress
Two PRs were **merged or closed** today:

- **PR #3116** — [fix(pico): complete turn.done lifecycle signaling](https://github.com/sipeed/picoclaw/pull/3116) (closed, stale). Fixes three gaps in Pico lifecycle: preserves `request_id` for queued steering/follow-up messages, ensuring every inbound Pico request receives proper lifecycle signaling. Addresses [issue #2984](https://github.com/sipeed/picoclaw/issues/2984).
- **PR #2975** — [feat(telegram): treat reply to bot message as mention in group chats](https://github.com/sipeed/picoclaw/pull/2975) (closed, stale). Enhances Telegram group chat UX by allowing users to trigger bot responses by replying to a bot message (equivalent to @mention). Previously required explicit @mention.

No other PRs were merged today. The closed PRs had been open for 19 and 33 days respectively before maintainer action.

## Community Hot Topics
**Most discussed:**

- **Issue #3164** — [BUG: Process hooks crash gateway on Android/Termux](https://github.com/sipeed/picoclaw/issues/3164) — 1 comment. This is a high-impact bug for mobile users. The gateway crashes within 2 seconds of startup when running any JSON-RPC hook, even trivial "hello world" scripts. No fix PR yet.

- **Issue #3201** — [Feature: Support streaming output for QQ channel](https://github.com/sipeed/picoclaw/issues/3201) — 0 comments, newly filed. Requests token-by-token streaming for QQ channel, noting Telegram and Pico WebSocket already support `StreamingCapable`. Signals growing demand for consistent multi-channel streaming.

**Most active PRs (updated today):**

- **PR #3165** — [fix(openai_compat): recover Seed XML tool calls](https://github.com/sipeed/picoclaw/pull/3165) — Open 8 days, maintains activity. Restores Volcengine Doubao Seed XML tool call extraction from OpenAI-compatible responses.
- **PR #3161** — [fix(exec): keep deny patterns active for custom allow rules](https://github.com/sipeed/picoclaw/pull/3161) — Open 9 days. Security fix preventing allow-rule bypass of deny patterns.
- **PR #3160** — [fix(auth): reject cross-site launcher setup requests](https://github.com/sipeed/picoclaw/pull/3160) — Open 9 days. Adds browser provenance checks against CSRF-style attacks on auth setup.

**Underlying need:** Community is prioritizing **security hardening** (cross-site protection, exec sandbox enforcement) and **platform parity** (Android stability, QQ streaming).

## Bugs & Stability
**Critical:**
- **Issue #3164** — [Process hooks crash gateway on Android/Termux](https://github.com/sipeed/picoclaw/issues/3164) — **Critical severity.** Any process hook (JSON-RPC over stdio) crashes the gateway within 2 seconds on Android/Termux. Affects v0.2.9 with config v3. No fix PR exists. This blocks all hook functionality for mobile users.

**High:**
- **PR #3161** — [fix(exec): keep deny patterns active for custom allow rules](https://github.com/sipeed/picoclaw/pull/3161) — **Security regression fix.** Previously, custom allow rules like `^jq\b` could allow dangerous payloads (e.g., reading process environment variables) because deny patterns were skipped entirely. Fix ensures deny patterns are always enforced. Currently open, not yet merged.

**Medium:**
- **PR #3160** — [fix(auth): reject cross-site launcher setup requests](https://github.com/sipeed/picoclaw/pull/3160) — Potential CSRF vulnerability. Adds browser provenance checks to prevent cross-origin setup of launcher passwords. Open, not merged.

**Low:**
- **PR #3158** — [test: cover sandbox fs Windows path handling](https://github.com/sipeed/picoclaw/pull/3158) — Regression test coverage for sandbox filesystem rejecting valid workspace-relative paths due to platform-specific path separators. Not a live bug but prevents future regressions.

**Note:** The critical Android crash (Issue #3164) has **no associated fix PR**, which is concerning given it has been open for 9 days.

## Feature Requests & Roadmap Signals
**New features requested today:**
- **Issue #3201** — [Support streaming output for QQ channel](https://github.com/sipeed/picoclaw/issues/3201) — High demand signal. User explicitly notes Telegram and Pico WebSocket already support this. Likely candidate for next minor release given existing pattern.

**PRs adding significant features (still open):**
- **PR #3200** — [feat(models): add configurable default fallback chain](https://github.com/sipeed/picoclaw/pull/3200) — Adds fallback model configuration in web UI with backend persistence. Users can set default model, add fallbacks, reorder, and save. This is a **high-value UX improvement** likely targeted for next stable release.

**PRs on road to merge (maintainer attention evident):**
- **PR #3165** — Seed XML tool call recovery (critical for Doubao users)
- **PR #3161** — Exec security fix
- **PR #3202** — ID normalization fix ([view PR](https://github.com/sipeed/picoclaw/pull/3202))

**Prediction for next version:** v0.4.0 or v0.3.2 will likely include the fallback chain feature, exec security hardening, identity normalization fix, and possibly QQ streaming support.

## User Feedback Summary
**Pain points:**
1. **Android mobile users** are completely blocked from using process hooks (Issue #3164). This is a severe quality gap for mobile-first workflows.
2. **QQ channel users** experience poor UX waiting for full LLM responses (Issue #3201). Telegram and WebSocket users have streaming; QQ users do not.
3. **Security-conscious users** want stronger enforcement of exec deny patterns (PR #3161). Current behavior allows bypass via custom allow rules.

**Satisfaction signals:**
- Telegram group chat reply-as-mention (PR #2975 closed) was positively received; reduces friction for group interactions.
- Fallback chain configuration (PR #3200) addresses long-standing UX issue of manual model fallback setup.

## Backlog Watch
**Long-unanswered high-importance items:**

1. **Issue #3164** — [Process hooks crash on Android/Termux](https://github.com/sipeed/picoclaw/issues/3164) — **9 days, no maintainer response, no fix PR.** This is the most critical open issue. Mobile users cannot use hooks at all. Needs immediate triage.

2. **PR #3165** — [fix(openai_compat): recover Seed XML tool calls](https://github.com/sipeed/picoclaw/pull/3165) — Open **10 days** with no feedback. Affects all Doubao/Seed model users on the OpenAI compat path.

3. **PR #3161** — [fix(exec): keep deny patterns active for custom allow rules](https://github.com/sipeed/picoclaw/pull/3161) — Open **9 days**, security regression fix. Delaying merge leaves users exposed to allow-rule bypass.

4. **PR #3160** — [fix(auth): reject cross-site launcher setup requests](https://github.com/sipeed/picoclaw/pull/3160) — Open **9 days**, security hardening for auth setup.

5. **Dependency bump PRs** — Three stale dependabot PRs ([#3104](https://github.com/sipeed/picoclaw/pull/3104) shadcn, [#3103](https://github.com/sipeed/picoclaw/pull/3103) typescript-eslint, [#3100](https://github.com/sipeed/picoclaw/pull/3100) @vitejs/plugin-react) have been open **21 days** without review. These affect the web frontend build chain and may accumulate security vulnerabilities.

**Maintainer attention needed:** The Android crash (Issue #3164) and three stale security/regression fix PRs (#3165, #3161, #3160) represent the most urgent backlog items. These are all 9-10 days old and have received no maintainer feedback.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-02

---

## Today's Overview

NanoClaw shows **high activity** with 6 new open issues and 12 PRs updated in the last 24 hours—a strong pulse for a self-hosted AI agent platform. The project is in a **consolidation phase**: 6 PRs were merged or closed today (some dating back months), while 6 new PRs remain open, indicating steady maintenance alongside feature development. A **cluster of infrastructure bugs** surfaced around webhook configuration, Docker networking, and silent message failures, suggesting the project is addressing real-world self-hosting pain points. No new releases were published today.

---

## Releases

**None.** No new versions were tagged in the last 24 hours. The last releases (if any) predate this window.

---

## Project Progress

**6 PRs merged/closed today**, spanning critical fixes and long-awaited features:

| PR | Title | Status |
|----|-------|--------|
| [#2905](https://github.com/nanocoai/nanoclaw/pull/2905) | fix(whatsapp): end the old socket on reconnect (host memory leak) | **Merged** |
| [#2677](https://github.com/nanocoai/nanoclaw/pull/2677) | fix(scheduling): retry pre-task script once on failure with diagnostics | **Merged** |
| [#1716](https://github.com/nanocoai/nanoclaw/pull/1716) | feat: add /check-contribution operational skill for PR pre-flight checks | **Merged** |
| [#1257](https://github.com/nanocoai/nanoclaw/pull/1257) | feat: support custom API endpoints (e.g., z.ai) | **Merged** |
| [#1693](https://github.com/nanocoai/nanoclaw/pull/1693) | feat: add /add-backup utility skill for automated state backup | **Merged** |
| [#1597](https://github.com/nanocoai/nanoclaw/pull/1597) | feat: add QMD skill for semantic conversation search | **Merged** |

**Notable advances:**
- **WhatsApp memory leak fixed** — `connectSocket()` now properly closes old sockets on reconnect, preventing Baileys socket graph accumulation
- **Custom API endpoint support** (PR #1257, from March) finally merged, enabling third-party Anthropic-compatible APIs at sub-paths (e.g., z.ai)
- **New operational skills**: automated state backup (`/add-backup`) and semantic conversation search (`QMD`) are now in mainline
- **PR contribution pipeline** improved via `/check-contribution` skill for automated pre-flight checks

---

## Community Hot Topics

**Most active items today all relate to the OneCLI setup breakage** — these are likely the highest-urgency discussions in the community:

### 🔴 #2903 — OneCLI setup broken: gateway binds 127.0.0.1 but clients target 10.0.0.1
[Issue #2903](https://github.com/nanocoai/nanoclaw/issues/2903)
- **0 comments** (newly filed), but this is the most impactful open issue: new users hitting a fresh install get **zero agent responses** due to a Docker bridge IP mismatch
- Underlying need: first-run experience reliability — this blocks any new deployment

### 🔴 #2902 — Silent message swallowing on agent failure
[Issue #2902](https://github.com/nanocoai/nanoclaw/issues/2902)
- Messages accepted on Telegram but silently dropped when the agent container fails to spawn — user never sees an error
- Underlying need: **observability and user feedback** — self-hosted users cannot debug failures without server logs

### 🟡 #2899 — Discord DM button rejection (all buttons route to "reject")
[PR #2899](https://github.com/nanocoai/nanoclaw/pull/2899) (fix PR open)
- Newline character in Discord `custom_id` causing every button tap to reject — a UX-breaking bug for any Discord integration
- Fix PR is **open** and actively being reviewed

---

## Bugs & Stability

**6 new bugs reported today, all open.** Ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| 🔴 **Critical** | [#2903](https://github.com/nanocoai/nanoclaw/issues/2903) | OneCLI setup: agents never respond due to Docker bridge bind mismatch | No |
| 🔴 **Critical** | [#2902](https://github.com/nanocoai/nanoclaw/issues/2902) | Silent message swallowing — user sees no error on agent failure | No |
| 🟠 **High** | [#2901](https://github.com/nanocoai/nanoclaw/issues/2901) | `WEBHOOK_PORT` ignored when set in `.env` — documented config path broken | No |
| 🟠 **High** | [#2900](https://github.com/nanocoai/nanoclaw/issues/2900) | Webhook EADDRINUSE kills entire host daemon (no graceful degradation) | No |
| 🟢 **Low** | [#2897](https://github.com/nanocoai/nanoclaw/issues/2897), [#2898](https://github.com/nanocoai/nanoclaw/issues/2898) | E2E test probes (Matt Pocock skills) — safe to close | N/A |

**Pattern:** All "critical" bugs relate to **new user onboarding and reliability** — the project is seeing an influx of first-time self-hosters hitting configuration edge cases.

---

## Feature Requests & Roadmap Signals

**From open PRs (not yet merged):**

| Feature | PR | Stage | Predicted Next Version |
|---------|----|-------|----------------------|
| Instance-wide default agent provider | [#2906](https://github.com/nanocoai/nanoclaw/pull/2906) | Open, needs review | ✅ Likely v0.8.x |
| Agent template system (from library, git, local) | [#2890](https://github.com/nanocoai/nanoclaw/pull/2890) | Open, substantial code | ✅ Likely v0.8.x |
| Local voice transcription (Whisper backends) | [#2317](https://github.com/nanocoai/nanoclaw/pull/2317) | Open since May, needs review | 🟡 Possible but stale |
| Configurable `--shm-size` and `--init` for browser agents | [#2771](https://github.com/nanocoai/nanoclaw/pull/2771) | Open, waiting attention | ✅ Likely v0.8.x |
| Slack thread history reload on @mention | [#2904](https://github.com/nanocoai/nanoclaw/pull/2904) | Open, fix PR | ✅ Should ship with next patch |

**Prediction:** The **agent template loader** (#2890) and **default agent provider** (#2906) together suggest the v0.8 roadmap is moving toward **easier multi-agent setup** — reducing per-group boilerplate.

---

## User Feedback Summary

**Pain points expressed in today's issues:**

1. **"Out of the box, nothing works"** (Issue #2903) — fresh Docker install fails silently due to network config, leaving users with non-responsive agents
2. **"My messages disappear"** (Issue #2902) — no feedback when agent container fails to start; users only see silent failure
3. **"I set WEBHOOK_PORT in .env and it does nothing"** (Issue #2901) — documented configuration path is broken, causing confusion
4. **"Webhook crash takes down everything"** (Issue #2900) — an optional webhook server kills the entire daemon if port is taken; users want graceful degradation

**Satisfaction signals:**
- 6 long-standing PRs merged today, including features from March and April — contributor patience is being rewarded
- WhatsApp memory leak fix (#2905) shows responsiveness to channel-level stability issues

**Common theme:** Self-hosters want **reliable first-run experience** and **clear error feedback** — these are the top friction points for adoption.

---

## Backlog Watch

**Items needing maintainer attention:**

| Item | Issue/PR | Age | Risk |
|------|----------|-----|------|
| 🔴 Local voice transcription skill | [#2317](https://github.com/nanocoai/nanoclaw/pull/2317) | 56 days (since May 7) | Stale — may need rebasing; community may lose interest |
| 🟡 Configurable shm-size for browser agents | [#2771](https://github.com/nanocoai/nanoclaw/pull/2771) | 17 days (since June 15) | Low conflict risk but no recent maintainer activity |
| 🟡 All 4 critical/high bugs from today | Issues #2900–#2903 | 1 day | **High** — these block new user adoption; no fix PRs exist yet |

**Recommendation:** The **OneCLI setup bug** (#2903) and **silent message swallowing** (#2902) should receive maintainer attention within 48 hours, as they represent the biggest barrier to new deployments and user trust.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for 2026-07-02.

---

## NullClaw Project Digest – 2026-07-02

### 1. Today's Overview
The NullClaw project is currently in a period of low activity. In the last 24 hours, no new releases, pull requests, or merges were recorded. Activity is confined to a single open issue, #868, which was updated yesterday. While the project appears stable with no new regressions introduced, the lack of PR traffic suggests a potential pause in feature development or maintainer bandwidth. The community's focus remains on a persistent cross-platform build failure on Android.

### 2. Releases
No new releases were published on 2026-07-02. The latest stable version remains **v2026.4.17** (referenced in issue #868).

### 3. Project Progress
No pull requests were updated, merged, or closed in the last 24 hours. **Zero** features or fixes advanced today.

### 4. Community Hot Topics
**#868 – [bug] zig build fails on Android/Termux (aarch64)**
- **Status:** Open | **Updated:** 2026-07-01 | **Comments:** 6 | **Link:** [Issue #868](https://github.com/nullclaw/nullclaw/issues/868)
- This is the sole point of community discussion. The issue concerns a build failure when compiling NullClaw via `zig build -Doptimize=ReleaseSmall` on Termux (Android aarch64). The error `AccessDenied on options.zig linkat` indicates a permission or filesystem compatibility issue with Zig’s linker on the Android environment.
- **Underlying need:** Users on mobile Linux environments (Termux) are seeking reliable build support. This is likely a blocking pain point for Android-based contributors or users who want to run NullClaw locally on their devices using the latest Zig toolchain (0.16.0).

### 5. Bugs & Stability
- **Severity: Moderate** – Issue #868 ([Link](https://github.com/nullclaw/nullclaw/issues/868)): Build failure on Android/Termux (aarch64) when using `zig build -Doptimize=ReleaseSmall`. The error is a linker access denial, which stops compilation entirely. This is not a runtime crash but prevents users on that platform from building the project at all. No fix PR currently exists.

### 6. Feature Requests & Roadmap Signals
No explicit feature requests were logged in the last 24 hours. However, the existence of Issue #868 signals a latent demand for better **cross-platform build compatibility**, specifically for **Android (Termux) and aarch64 architecture**. If the maintainer addresses this, it may lead to improvements in the Zig build configuration or build system documentation.

### 7. User Feedback Summary
- **Pain Points:** The primary user pain point is the inability to build NullClaw on a standard Android device using Termux. The user (NOTJuangamer10) provided a detailed environment description and error log, showing investment in resolving the issue but frustration with the failure.
- **Use Cases:** Running NullClaw directly on a Xiaomi Redmi Note 9 (LineageOS 22.2) suggests a mobile-first or offline-First use case.
- **Satisfaction:** Not directly measured, but the single open issue indicates a quiet but possibly stagnant community engagement.

### 8. Backlog Watch
The only item currently requiring maintainer attention is **Issue #868** ([Link](https://github.com/nullclaw/nullclaw/issues/868)), opened on April 23, 2026, and last updated on July 1, 2026. It has remained open for over two months with 6 comments but no pull request attached. This issue is important because it blocks the entire build pipeline for a specific platform (Android aarch64) and is the only open item in the project, making it a clear signal that maintainer intervention is needed.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-02

## Today's Overview

IronClaw is in an intense bug-bash and stabilization cycle, with 24 issues updated in the last 24 hours (17 open) and 50 PRs updated (28 merged/closed). The project is actively addressing a cluster of P1/P2 regressions surfaced during the June 30–July 1 QA testing, particularly around routine execution, runner leases, and Slack/Google integration reliability. No new releases were published today, but a release PR (#5311) is open with breaking API changes across several crates. The Reborn backend is seeing heavy investment in integration test coverage, seam constructors, and credential injection verification, signaling maturation toward production stability.

## Releases

**No new releases today.** The open release PR #5311 (`chore: release`) proposes bumping multiple crate versions with breaking changes, but has not yet been merged.

## Project Progress

**28 PRs merged or closed today**, advancing the following areas:

### Reborn Backend Integration & Testing
- **PR #5482 (closed)** — Added int-tier coverage for all five trigger-management verbs (`trigger_create`/`list`/`pause`/`resume`/`remove`) through the real agent-loop path
- **PR #5481 (closed)** — System-prompt capture seam for asserting model-visible prompt content in integration tests
- **PR #5483 (closed)** — Proved credential injection reaches the wire (T0-SECRET-INJECT coverage)
- **PR #5434 (closed)** — Added `memory_search`/`memory_tree` int-tier scenarios

### Tooling & Slack
- **PR #4941 (closed)** — New `slack_user_tool` WASM tool enabling IronClaw to act as the user via personal user tokens (message search, reactions, cross-workspace capabilities)

### Refactoring & Architecture
- **PR #5137 (closed)** — Extracted `ironclaw_reborn_http_kit` as the first decomposition of the ~132k-line `ironclaw_reborn_composition` god-crate

### Bug Fixes
- **Issue #5443 (closed)** — Added header notifications for newly triggered automation tasks
- **Issue #5458 (closed)** — Fixed double header rendering on Logs page
- **Issue #5457 (closed)** — Fixed Logs page remaining empty indefinitely
- **Issue #5289 (closed)** — Fixed generic "driver protocol error" hiding underlying `invalid_input` failures
- **Issue #5246 (closed)** — Added global auto-approve shortcut text under approval checkbox
- **Issue #5488 (closed)** — Hid skill activation system messages from chat transcript
- **Issue #5333 (closed)** — Fixed composer keeping submitted message visible briefly after sending

## Community Hot Topics

### Most Active Issues (by comments/reactions)

- **[Issue #5459 — Configurable skills and tools](https://github.com/nearai/ironclaw/issues/5459)** (1 comment, authored June 30) — This foundational feature request is driving two open PRs (#5499, #5513) for WASM tool installation from zip and tenant-shared credential management. Strong signal that configuration flexibility is a priority for admins.

- **[Issue #5507 — Failed routine "No thread attached"](https://github.com/nearai/ironclaw/issues/5507)** (1 comment) — Blocks debugging for failed routine runs, a P2 bug-bash item affecting inspection of execution threads.

- **[Issue #5456 — Runner lease expiration](https://github.com/nearai/ironclaw/issues/5456)** (1 comment) — P1 regression where 90-second inactivity threshold is too aggressive for multi-tool routines. Dominant failure pattern during July 1 testing.

### Most Active Pull Requests

- **[PR #5517 — C-SAFETY + C-WEBACCESS int-tier coverage](https://github.com/nearai/ironclaw/pull/5517)** (opened today) — Safety ingress and web-access MCP test coverage from core contributor
- **[PR #4927 — Credential-free hosted MCP dispatch](https://github.com/nearai/ironclaw/pull/4927)** (open since June 15, experienced contributor) — Unblocking hosted MCP providers with no credentials

**Underlying need**: The community is clearly focused on stabilizing routine/automation execution while simultaneously building out the Reborn integration test harness to prevent regression. The volume of seam constructors and test PRs suggests a systematic approach to quality assurance.

## Bugs & Stability

### Critical/P1 Severity

1. **[Issue #5456 — Runner lease expiration (P1)](https://github.com/nearai/ironclaw/issues/5456)** — Multi-tool routines consistently fail due to 90-second inactivity timeout. Dominant failure pattern affecting email + sheets workflows.

2. **[Issue #5504 — Routine creation hangs indefinitely (P1)](https://github.com/nearai/ironclaw/issues/5504)** — Chat shows planning message but never returns result or error.

3. **[Issue #5505 — Self-referential routine prompts (P1)](https://github.com/nearai/ironclaw/issues/5505)** — Created routines contain instructions to "create a routine" instead of just executing. **Fix PR #5515 opened today** to restrict trigger-mutator tools during scheduled fires.

4. **[Issue #5415 — Google Sheets protocol violation (P1)](https://github.com/nearai/ironclaw/issues/5415)** — Consistent failure on 18–25 tool call workflows. Open since June 29.

### High/P2 Severity

5. **[Issue #5507 — Failed routine "No thread attached"](https://github.com/nearai/ironclaw/issues/5507)** — Blocks debugging of failed executions.
6. **[Issue #5508 — Slack delivery target not found](https://github.com/nearai/ironclaw/issues/5508)** — Despite active connection, new routines cannot deliver via Slack DM.
7. **[Issue #5506 — Slack bot redirects to WebUI](https://github.com/nearai/ironclaw/issues/5506)** — Async tasks redirect to WebUI instead of delivering in Slack.
8. **[Issue #5509 — Chat creation latency grows with history](https://github.com/nearai/ironclaw/issues/5509)** — Frontend introduces delay scaling with accumulated conversations.
9. **[Issue #5457 (closed) — Logs page empty](https://github.com/nearai/ironclaw/issues/5457)** — Fixed today.
10. **[Issue #5458 (closed) — Double header on Logs](https://github.com/nearai/ironclaw/issues/5458)** — Fixed today.

### Medium/P3 Severity

11. **[Issue #5510 — Cannot delete old routines](https://github.com/nearai/ironclaw/issues/5510)** — No deletion mechanism, compounds Slack delivery issues.

## Feature Requests & Roadmap Signals

### Likely in Next Version

- **Configurable skills and tools** (#5459) — Two open PRs (#5499 for WASM install, #5513 for admin UI) suggest this will land imminently with tenant-shared credentials and admin/user installation distinction
- **Progressive tool disclosure** (PR #5149) — Flag-gated feature to cut per-call tokens from ~25.8k to manageable size, addressing timeout failures
- **Context management** — The size-XL PR #5149 addresses foundational context efficiency for production scaling
- **Google compact capabilities** (PR #5503) — Adds efficient Gmail/Calendar/Drive operations to reduce token consumption

### On the Horizon

- **SSO re-login token replacement** (PR #5511) — Allows WebUI to replace stale tokens via OAuth login tickets
- **No run-borking failures** (PR #4841) — Long-running effort to ensure every run-terminal error is recovered or explained
- **E-MULTIUSER seam** (#5479) — Multi-actor thread support blocked by one-runtime group harness issues

## User Feedback Summary

### Pain Points (from bug-bash QA)

- **Routine reliability is poor** — Multiple P1 failures during testing (lease expiration, hanging creation, self-referential prompts) indicate automation is not ready for production use
- **Debugging is blocked** — "No thread attached" error on failed runs prevents investigation; Logs page (now fixed) was empty
- **Slack integration is confusing** — Bot redirects to WebUI for long tasks; new routines can't find Slack delivery despite existing connections working
- **Privilege escalation confusion** — Contradictory Google connection state messages erode user trust
- **Performance degradation** — Chat creation slows with history accumulation; routine creation hangs

### Satisfaction Indicators

- **Header notifications for automations** (closed) addresses a key usability gap
- **Skill activation noise removed from chat** (closed) shows attention to UX polish
- **Slack user-token tool** (merged) enables new capabilities beyond bot limitations

## Backlog Watch

### Long-unanswered Issues Needing Attention

- **[Issue #4108 — Nightly E2E failure](https://github.com/nearai/ironclaw/issues/4108)** — Open since **May 27, 2026** (over 5 weeks). Nightly E2E continues to fail, suggesting unresolved infrastructure or regression issues. No comments since initial automated report.

### Stalled PRs

- **[PR #4787 — Barcelona Hackathon fork](https://github.com/nearai/ironclaw/pull/4787)** — Open since June 12, marked `[NO MERGE]`. May need resolution or closure.
- **[PR #4841 — No run-borking failures](https://github.com/nearai/ironclaw/pull/4841)** — Open since June 13, critical for production stability but has not advanced in weeks.
- **[PR #4927 — Credential-free hosted MCP](https://github.com/nearai/ironclaw/pull/4927)** — Open since June 15, experienced contributor, may be blocked by credential injection refactors now landing.

### Open Reborn Seam Issues

- **[Issue #5479 — One-runtime group harness failure](https://github.com/nearai/ironclaw/issues/5479)** — Deterministic failure on E-MULTIUSER seam since rebase, blocks multi-user thread support. Opened July 1 with detailed diagnostic context but no fix yet.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **2026-07-02**.

---

## LobsterAI Project Digest – July 2, 2026

### 1. Today's Overview
The project saw extremely high activity, with **25 Pull Requests** updated in the last 24 hours—a massive spike largely due to a **mass merge of stale PRs** from April and March (21 closed/merged). This cleanup significantly reduces technical debt. There are **4 open issues**, including a major architectural suggestion regarding "tool convergence." No new releases were published today. The project is in a **healthy maintenance and consolidation phase**, focusing on bug fixes, performance, and improved developer experience (DX).

### 2. Releases
**None.** No new versions were released today.

### 3. Project Progress (Merged/Closed PRs)
A total of **21 PRs** were merged or closed, indicating a significant backlog clearance effort. Key feature advancements and fixes include:

- **Subagents & Artifacts (PR #2249)**: New "Subagents" tab in the artifact panel, including list/detail views, and removal of redundant sidebar rows.
- **MCP Ecosystem (PR #2244)**: Added **Qichacha** (enterprise data) integration to the MCP marketplace, plus improvements to grouped server management.
- **Artifact Auto-Preview (PR #2248)**: New logic automatically opens generated preview cards (local services, HTML, images) to reduce user friction.
- **Share Deployment (PR #2251)**: Uses an isolated Node tool environment to execute deploy commands, improving reliability.
- **Timer & UX (PR #1242 & PR #1548)**: Added "clear all attachments" and "clear input" buttons, and streaming activity timers.
- **Import/Export Features (PR #1291, #1366, #1355)**: Major data portability improvements with scheduled task and Agent import/export in `.lobstertasks` / JSON formats.
- **Sidebar & Navigation (PR #1253, #1171)**: Sidebar now retains an icon bar when collapsed, and Agent sidebar shows task count badges.
- **Bug Fixes**: Fixed Windows drag-drop for `.pptx`/`.docx` files (PR #1355); fixed macOS fullscreen black screen on quit (PR #2246); fixed analytics reporting edge cases (PR #2245); fixed cowork plan recovery conflicts (PR #2247).
- **Documentation**: README updated (PR #2250).

### 4. Community Hot Topics
- **#2239 – Trend Analysis: "OpenClaw-ization" of Programming Tools (OPEN)**
  - *User*: woxinsj | *Comments*: 0 | *Reactions*: 0
  - **Analysis**: This is the most strategically significant issue today. The author argues that AI coding tools are becoming OS-level agents, and vice-versa. They propose LobsterAI (a general assistant) deepen integration with coding tools via the **MCP protocol** to achieve "full-process automation." This signals a demand for **cross-domain orchestration** (IDE + OS + Office).
  - **Link**: [Issue #2239](https://github.com/netease-youdao/LobsterAI/issues/2239)

- **#2243 – Skills Load Watch: Performance & UI (OPEN)**
  - *User*: woxinsj | *Comments*: 0 | *Reactions*: 0
  - **Analysis**: A detailed performance report from a power user with **174 skills**. Highlights three issues: (1) file watcher overhead causing massive token waste, (2) a persistence bug where `skills.load.watch` is a protected path with no UI toggle, (3) lack of a manual on/off switch. This indicates a need for **observability and control over background processes**.
  - **Link**: [Issue #2243](https://github.com/netease-youdao/LobsterAI/issues/2243)

- **#1361 – Agent Detail: "Delete" Button in English (OPEN)**
  - *User*: devilszy | *Comments*: 1 | *Reactions*: 0
  - **Analysis**: A localization bug. The "delete" button on custom Agent detail pages shows the English word "delete" instead of the Chinese equivalent. Minor but important for daily UX in a Chinese-dominant user base.
  - **Link**: [Issue #1361](https://github.com/netease-youdao/LobsterAI/issues/1361)

### 5. Bugs & Stability
*Ranked by severity:*

| Severity | Issue ID | Description | Status | Related Fix PR |
|----------|----------|-------------|--------|----------------|
| **High** | #1425 | No validation for duplicate shortcut keys (regression) | CLOSED (Stale) | N/A (closed) |
| **High** | #2243 | File watcher causes performance degradation & token waste | OPEN | None yet |
| **Medium** | #1361 | "Delete" button showing English (localization) | OPEN | None yet |
| **Medium** | #2252 | Deleting active custom model causes white screen crash | OPEN | PR #2252 (fix proposed) |
| **Low-Med** | #2247 | Abort/finish race condition causing session file lock collisions | FIXED | PR #2247 |
| **Low** | #2246 | macOS fullscreen black screen on `Cmd+Q` | FIXED | PR #2246 |

### 6. Feature Requests & Roadmap Signals
The most clear roadmap signals come from **Issue #2239**. The user’s call for "OpenClaw-ification" suggests the following features may be prioritized in the next version (e.g., v2026.7 or v2026.8):

- **Deeper MCP Integration with IDEs**: LobsterAI already supports MCP; the next step is bi-directional communication with coding tools like **OpenCode** or **CodeBuddy**.
- **System-Level Orchestration**: Automating sequences like "write code → run test → commit → deploy" entirely within LobsterAI.
- **Skills UI Management**: A toggle to enable/disable file watchers (from #2243), likely entering a "Performance > Skills" settings panel.
- **Multi-Server MCP Management**: Following the Qichacha integration (PR #2244), expect a "Grouped Server" UI for managing multiple MCP providers.

### 7. User Feedback Summary
Users are generally power users and developers. Key sentiments observed today:

- **Satisfaction**: The mass merge of old import/export features (PR #1291, #1366) suggests user demand for **data portability** is being met. The "ESC to close permission modal" patch (PR #1362) indicates value on minor UX polish.
- **Dissatisfaction / Pain Points**:
  - **Performance hotspots** are the top concern. User *woxinsj* explicitly calls out "wasting token and I/O," which is a direct cost issue for users on API-based models.
  - **Localization gaps**: Minor English strings persist in the UI (Issue #1361), indicating incomplete i18n coverage.
  - **Lack of user control**: Users want **on/off switches** for background processes they can't otherwise configure (e.g., file watchers).

### 8. Backlog Watch
The following items have received no maintainer response for 90+ days and are at risk of becoming stale or blocking users:

- **Issue #1361** – Agent "delete" button localization (Updated 2026-07-01, but no label change or assignment). **Low effort fix, high daily visibility.**
- **PR #1362** – ESC key close for permission modal (Open since April). **Small UX win, should be fast to review.**
- **PR #1364** – Model selector in new-task input toolbar (Open since April). **Conflicts with current UI architecture? Needs discussion.**
- **PR #1367** – Duplicate task name validation (Open since April). **Regression risk for scheduled tasks; good candidate for review.**

**Maintainer attention required**: The community is actively filing strategic requests (#2239) and performance reports (#2243). A response from maintainers—even just a "we are considering this"—would be valuable.

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

# CoPaw Project Digest — 2026-07-02

## 1. Today's Overview

CoPaw is in a period of **high activity** this week, with **22 issues updated** (17 open/active) and **50 PRs touched** in the last 24 hours — 27 of which were merged or closed. While no new releases dropped today, the project is processing a substantial bug-fix and feature merge wave, particularly around the v2.0.0 pre-release track (tracking issue [#5273](https://github.com/agentscope-ai/QwenPaw/issues/5273)). The community is submitting deep architectural critiques and detailed bug reports, especially around the Feishu channel, context compression, and security hardening. Overall project health appears **robust but under strain**: the merge cadence is strong, but several long-standing bugs (e.g., subagent polling loops, channel reconnection crashes) remain unresolved.

## 2. Releases

**No new releases today.** The latest tagged versions remain **v1.1.12.post2** (stable) and **v2.0.0b2** (beta).

## 3. Project Progress

**27 PRs merged/closed today.** Key highlights:

| Area | PR / Issue | Summary |
|------|-----------|---------|
| **Loop Engineering** | [#5665](https://github.com/agentscope-ai/QwenPaw/pull/5665) (merged) | Composable gate-based loop architecture + frontend settings UI for granular control of agent loop behavior |
| **TUI** | [#5673](https://github.com/agentscope-ai/QwenPaw/pull/5673) (merged) | Added live context-usage bar to TUI status bar — shows real-time context fullness vs auto-compaction threshold |
| **Governance** | [#5682](https://github.com/agentscope-ai/QwenPaw/pull/5682) (merged) | `strict` mode now correctly overrides ALLOW rules; tool calls require approval even for builtin rules |
| **Plugins** | [#5568](https://github.com/agentscope-ai/QwenPaw/pull/5568) (merged) | Fixed all 5 official plugins failing to install from CDN catalog on QwenPaw 2.0 (agent‑scope 2.x migration regressions) |
| **Plugin Market** | [#5612](https://github.com/agentscope-ai/QwenPaw/pull/5612) (merged) | Version-routed plugin downloads to prevent v1.x users getting incompatible v2.x plugins |
| **Documentation** | [#5653](https://github.com/agentscope-ai/QwenPaw/pull/5653) (merged) | Added Architecture page (EN + ZH) explaining Agent OS, workspace boundary, staged lifecycle |
| **Various fixes** | [#5454](https://github.com/agentscope-ai/QwenPaw/pull/5454), [#5457](https://github.com/agentscope-ai/QwenPaw/pull/5457), [#5500](https://github.com/agentscope-ai/QwenPaw/pull/5500), [#5641](https://github.com/agentscope-ai/QwenPaw/pull/5641), [#5645](https://github.com/agentscope-ai/QwenPaw/pull/5645) | macOS sandbox close-bracket fix, file size cap for `send_file_to_user`, detector cache key fix, desktop screenshot fix, coding mode project_dir read-write fix |

## 4. Community Hot Topics

| Issue | Comments | Summary |
|-------|----------|---------|
| [#5630](https://github.com/agentscope-ai/QwenPaw/issues/5630) | 8 | **Custom BaseURL for Telegram** — users behind reverse proxies need custom `base_url`. PR [#5651](https://github.com/agentscope-ai/QwenPaw/pull/5651) is already open by a first-time contributor. |
| [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | 8 (closed) | **Headroom context compression integration** — achieved 60–95% token reduction. Closed, indicates planned or experimental implementation. |
| [#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873) | 4 | **Subagent polling loop** — two subagents cause infinite rapid polling; Feishu side cannot interrupt. Active with PR [#5637](https://github.com/agentscope-ai/QwenPaw/pull/5637) proposing an event-driven fix. |
| [#5701](https://github.com/agentscope-ai/QwenPaw/issues/5701) | 3 | **Concurrent access deadlock** — multiple browser tabs to same agent cause hangs at v1.1.10. |
| [#5703](https://github.com/agentscope-ai/QwenPaw/issues/5703) | 2 | **Approval window still pops up** even after disabling all tool approval — user in sandboxed container cannot bypass. |

**Underlying need analysis:** The Telegram BaseURL request ([#5630](https://github.com/agentscope-ai/QwenPaw/issues/5630)) highlights the growing demand for **deployment flexibility** behind corporate proxies. The subagent polling bug ([#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873)) points to a **core runtime regression** in background task lifecycle management, which PR [#5637](https://github.com/agentscope-ai/QwenPaw/pull/5637) directly addresses. The approval bypass issue ([#5703](https://github.com/agentscope-ai/QwenPaw/issues/5703)) reveals a **governance gap** where sandbox detection failure falls back to user approval.

## 5. Bugs & Stability

**High severity:**

| Issue | Component | Description | Fix PR Exists? |
|-------|-----------|-------------|----------------|
| [#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873) | Core/Runtime | Two subagents cause infinite polling loop; Feishu cannot interrupt | ✅ [#5637](https://github.com/agentscope-ai/QwenPaw/pull/5637) (open) |
| [#5701](https://github.com/agentscope-ai/QwenPaw/issues/5701) | Core/Backend | Concurrent agent page access deadlock (v1.1.10) | ❌ |
| [#5696](https://github.com/agentscope-ai/QwenPaw/issues/5696) | QQ Channel | `self._http` becomes `None` after websocket reconnect → `AttributeError` | ❌ |
| [#5658](https://github.com/agentscope-ai/QwenPaw/issues/5658) | Provider | Cannot connect to model via 9router proxy (400 errors) — persistent across versions | ❌ |

**Medium severity:**

| Issue | Component | Description | Fix PR Exists? |
|-------|-----------|-------------|----------------|
| [#5710](https://github.com/agentscope-ai/QwenPaw/issues/5710) | Context Management | Context compression has no protected anchors — key messages truncated | ❌ |
| [#5709](https://github.com/agentscope-ai/QwenPaw/issues/5709) | Feishu Channel | Bot messages hard-dropped (`is_bot` filter); cross-agent @mentions lost | ❌ |
| [#5708](https://github.com/agentscope-ai/QwenPaw/issues/5708) | Feishu Channel | Interactive card messages not parsed; card user input invisible to agent | ❌ |
| [#5689](https://github.com/agentscope-ai/QwenPaw/issues/5689) | Plugins | Remote SSH plugin removal leaves dangling import → module error | ❌ |
| [#5676](https://github.com/agentscope-ai/QwenPaw/issues/5676) | Agent Prompt (v2.0.0b2) | Available skills not listed in system prompt; agent unaware of its tools | ❌ |

**Notable:** Three high-quality Feishu channel bugs were filed by the same user ([#5708](https://github.com/agentscope-ai/QwenPaw/issues/5708), [#5709](https://github.com/agentscope-ai/QwenPaw/issues/5709), [#5710](https://github.com/agentscope-ai/QwenPaw/issues/5710)) — indicating a **systematic audit** of the Feishu integration.

## 6. Feature Requests & Roadmap Signals

High-value feature requests raised or discussed today:

| Issue | Feature | Potential Impact |
|-------|---------|-----------------|
| [#5630](https://github.com/agentscope-ai/QwenPaw/issues/5630) | Custom Telegram BaseURL | Essential for deployments behind reverse proxies. PR [#5651](https://github.com/agentscope-ai/QwenPaw/pull/5651) already submitted. Likely **v1.1.13**. |
| [#5705](https://github.com/agentscope-ai/QwenPaw/issues/5705) | Secret key redaction (env var refs + log sanitization) | Security-critical. Duplicates [#5704](https://github.com/agentscope-ai/QwenPaw/issues/5704). **High priority for next release.** |
| [#5711](https://github.com/agentscope-ai/QwenPaw/issues/5711) | Comprehensive capability gap analysis vs competitors | Deep architectural review of tool calling, memory, rules enforcement. Could shape **v2.1 roadmap**. |
| [#5715](https://github.com/agentscope-ai/QwenPaw/issues/5715) | Web console password protection | Severe security gap — console is currently open-access. **Urgent fix expected.** |
| [#5670](https://github.com/agentscope-ai/QwenPaw/issues/5670) | Remove input character limit (currently 10k) | Low-effort, high-impact UX improvement for long-text workflows. |
| [#5712](https://github.com/agentscope-ai/QwenPaw/issues/5712) | Selectable text in chat messages + auto-copy | Desktop UX polish; prevents friction for copying code/output. |

**Prediction for next version (v1.1.13 / v2.0.0rc):** Telegram BaseURL, secret key redaction, web console auth, and tool result size caps are strong candidates. The loop engineering and governance PRs merged today indicate v2.0 is converging on GA.

## 7. User Feedback Summary

**Pain points (explicit):**
- "Concurrent access causes complete lockup when opening multiple tabs" ([#5701](https://github.com/agentscope-ai/QwenPaw/issues/5701)) — a stability **blocker** for team deployments.
- "Stopped all tool approval but still get approval popups" ([#5703](https://github.com/agentscope-ai/QwenPaw/issues/5703)) — governance **confusion**; user correctly diagnosed sandbox detection fallback.
- "Text can't be selected in desktop chat; must copy button every time" ([#5712](https://github.com/agentscope-ai/QwenPaw/issues/5712)) — **UX friction** in daily use.
- "10k character input limit cripples long-text workflows" ([#5670](https://github.com/agentscope-ai/QwenPaw/issues/5670)) — **missed capability** given model context windows of 256K+.
- "Feishu card messages invisible to agent; feedback system broken" ([#5708](https://github.com/agentscope-ai/QwenPaw/issues/5708)) — **integration defect** blocking enterprise adoption.

**Satisfaction signals:**
- Active first-time contributors submitting PRs: Telegram BaseURL ([#5651](https://github.com/agentscope-ai/QwenPaw/pull/5651)) and Generic Webhook channel ([#5716](https://github.com/agentscope-ai/QwenPaw/pull/5716)).
- Detailed architecture analysis submitted by community member ([#5711](https://github.com/agentscope-ai/QwenPaw/issues/5711)) — indicates invested power users who care about the project's direction.

## 8. Backlog Watch

Items needing maintainer attention:

| Issue / PR | Age | Problem |
|------------|-----|---------|
| [#4224](https://github.com/agentscope-ai/QwenPaw/pull/4224) (PR) | 52 days open | Memory index refresh after auto-summary — first-time contributor, under review. No maintainer comments since May. |
| [#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873) | 31 days open | Subagent infinite polling — root cause unsolved despite active discussion; PR [#5637](https://github.com/agentscope-ai/QwenPaw/pull/5637) under review. |
| [#5658](https://github.com/agentscope-ai/QwenPaw/issues/5658) | 2 days open | Proxy routing failure (9router) — user reports "persistent across versions." Needs reproduction from maintainers. |
| [#5688](https://github.com/agentscope-ai/QwenPaw/issues/5688) | 1 day open | CSS selector prefix mismatch (`ant-` vs `qwenpaw-`) — indicates CSS may be partially broken in production. Low-priority but suggests test gap. |

**Action recommended:** The 52-day-old first-time contributor PR [#4224](https://github.com/agentscope-ai/QwenPaw/pull/4224) risks contributor attrition if left unreviewed. The subagent polling bug ([#4873](https://github.com/agentscope-ai/QwenPaw/issues/4873)) should be resolved before v2.0.0 GA as it directly impacts multi-agent usability.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-02

## Today's Overview

ZeroClaw shows high activity with 50 issues and 50 PRs updated in the last 24 hours, indicating a period of intense development and community engagement. The project has 84 open issues and 44 open PRs, with 4 issues and 6 PRs resolved during this window. No new releases were published today. The project is in a stabilization and feature-expansion phase for the v0.8.3 milestone, with significant attention on MCP tool visibility, security hardening, and gateway API compatibility. Multiple high-severity bugs (S1 - workflow blocked) remain open, signaling ongoing reliability challenges in production workflows.

## Releases

None today. The latest tagged version remains unchanged.

## Project Progress

Six PRs were merged or closed in the last 24 hours:

- **PR #8255** [CLOSED] (`test`): Added unit coverage for tool-IO capture truncation edge cases, including UTF-8 char-boundary handling — testing-only change with no production impact.
- **PR #8552** [CLOSED] (`fix`): Fixed `CARGO_MANIFEST_DIR` resolution in the gateway build script, switching from compile-time macro to runtime environment variable lookup — fixes a build-time path regression.
- **PR #8575** [CLOSED] (`fix`): Removed stale `RUSTSEC-2024-0370` advisory ignore after removal of the Tauri desktop app — cleans up security posture.
- **Issue #8585** [CLOSED] (`ci`): Automated dependency-outage detection run — identified crate and toolchain updates available, closed once spotted.

Key advancements today include:
- **Security hardening**: A fix PR (#8574) addresses the zip-bomb vulnerability in `extract_zip_secure` (linked to Issue #8554), adding decompression-side guards for entry count, ratio, and uncompressed size.
- **Channel message metadata**: PR #8596 adds structured reply-scope metadata for WeCom channel, removing marker-text injection workarounds.
- **Memory trait extension**: PR #8570 (XL-sized) introduces a durable memory store seam with supersede, dedup, budget, and policy-gate capabilities — a foundational architecture change for persistent memory.

## Community Hot Topics

**Most Active Issues:**

1. **#8193** (13 comments) — *bug(zerocode): MCP tools/tool_search missing from TUI sessions while gateway sees them*  
   *Why it matters*: This S1 blocking bug affects core workflow — MCP servers connect and expose tools, but Zerocode TUI sessions don't receive them. Two users independently confirmed in discussion #8045. Fixing this is critical for v0.8.3 stability.

2. **#6808** (13 comments) — *RFC: Work Lanes, Board Automation, and Label Cleanup*  
   *Why it matters*: A governance RFC still in progress after a month-high comment count, showing community investment in project organization. Proposes routing workflows without manual overhead.

3. **#8226** (5 comments) — *[Feature]: support per-agent custom environment variables configuration*  
   *Why it matters*: Non-secret `runtime_context` and masked `runtime_secrets` blocks requested for multi-tenancy across process lanes and MCP instances. Blocked awaiting author action.

4. **#8043** (4 comments) — *RFC: Retire the standalone aardvark-sys crate (fold into zeroclaw-hardware)*  
   *Why it matters*: Accepted architecture simplification — reducing crate count and maintenance surface.

5. **#8303** (3 comments, 1 👍) — *RFC: Goal mode for bounded autonomous session work*  
   *Why it matters*: Users want a first-class durable mode for pursuing objectives until completion, pause, or budget exhaustion — not just interactive turns and cron.

**Underlying needs**: Users are demanding better MCP tool visibility, autonomous session modes, per-agent environment isolation, and more robust security boundaries. The community is actively contributing architecture RFCs (goal mode, compression decorators, OCI plugin storage), indicating a sophisticated user base with strong engineering backgrounds.

## Bugs & Stability

**S1 (Workflow Blocked) — Active:**

- **#8193** (high risk, accepted): MCP tools missing from TUI sessions — *no fix PR yet*
- **#8553** (high risk, accepted): Agent cannot use environment variables as `http_request` secrets — *no fix PR yet*
- **#6891** (medium risk, accepted): Scheduled Jobs edit error returns API 422 — *no fix PR yet*
- **#8559** (high risk, accepted): Agents stop working when exiting web dashboard chat window — *no fix PR yet*
- **#8563** (high risk, accepted): SOPs not available to agents through web dashboard chat session — *no fix PR yet*

**S2 (Degraded Behavior) — Active:**

- **#8302** (medium risk, in-progress): Configured MCP server tools not shown in web dashboard tools list — related to #8193
- **#8554** (high risk, in-progress): Zip-bomb vulnerability in skill extractor — **fix PR #8574 exists**
- **#5269** (medium risk, accepted): Installation documentation needs improvement for `cargo binstall zeroclaw` workflow

**Security Fixes Today:**
- PR #8574 hardens `extract_zip_secure` against zip-bomb inflation (#8554)
- PR #8575 removes stale advisory ignore for `RUSTSEC-2024-0370` after Tauri desktop removal

**Worth noting**: Three of the five S1 bugs directly involve web dashboard or gateway protocol gaps, suggesting the web UI layer needs more investment in the next release cycle.

## Feature Requests & Roadmap Signals

**High-Impact Requests:**

1. **#8568** (1 comment, just opened today): *Mixture-of-Agents (MoA) virtual model provider* — aggregator/judge model pattern with parallel reference models feeding analysis. *Prediction:* Likely to be deferred to v0.8.4 given v0.8.3's focused trackers.

2. **#8602** (0 comments, just opened today): *Enhance `file_read` — line cap, charset detection, paged PDF, notebook awareness, chunked binary* — battle-tested patterns from Claude Code's `Read` tool. *Prediction:* High community demand; could land in v0.8.3 as a tool improvement.

3. **#8550** (blocked, needs-maintainer-review): *OpenAI-compatible chat completions endpoint* — **fix PR #8486 exists** (XL-size, needs-author-action). *Prediction:* Strong candidate for v0.8.3 given existing PR and community demand for OpenAI SDK compatibility.

4. **#8424** (blocked, needs-author-action): *.ignore File Mechanism for Workspace File Protection* — workspace-internal file protection beyond existing `forbidden_paths`. *Prediction:* Likely for v0.8.3 or v0.8.4 due to security implications.

5. **#8309** (2 comments): *SkillForge (#144) is orphaned — wire up with safe defaults or remove* — an engine that's wired to nothing. *Prediction:* Likely to be wired with safe defaults in v0.8.3 to avoid dead code.

**Roadmap signals**: The three v0.8.3 trackers (#7314: WASM plugin program, #8360: provider/tool message serialization, #8071: runtime execution) are all accepted and active. WASM plugin infrastructure (#8551) and durable memory (#8570) are progressing as large PRs. The MoA provider (#8568) and OpenAI endpoint (#8550) indicate growing demand for API compatibility and advanced orchestration.

## User Feedback Summary

**Pain Points (high frequency):**
- MCP tool discovery in TUI vs. gateway inconsistency (#8193, #8302) — multiple users confirm the workflow break
- Agent termination on web dashboard exit (#8559) — users want background-able agents
- SOPs not detected in web sessions (#8563) — workflow configuration gap
- Environment variable injection for tools (#8553) — blocking authenticated HTTP requests
- Zip-bomb security gap (#8554) — concern about skill installation safety

**Satisfaction Signals:**
- High community contributor activity (multiple authors across PRs: Audacity88, wangmiao0668000666, NiuBlibing, Papilionidae, REL-mame, Nillth, etc.)
- Technical depth of RFC submissions (MoA, goal mode, compression decorators) suggests a sophisticated user base actively shaping the product

**Use Cases Emerging:**
- Autonomous bounded sessions (goal mode) for production workload execution
- Multi-tenant agent deployments with per-agent environment isolation
- OpenAI-compatible API consumption by third-party tools (LangChain, Continue.dev)
- WASM plugin channels for extensible networking without recompiling core

## Backlog Watch

**Issues Needing Maintainer Attention:**

1. **#7497** (blocked, needs-maintainer-review, since 2026-06-11): *OCI-Compliant Container Registries as Plugin Storage* — 3 comments, high-risk RFC. Creator bheatwole awaits maintainer evaluation. Could reshape the plugin distribution architecture.

2. **#7673** (blocked, needs-author-action, since 2026-06-15): *Native context compression as a provider pipeline decorator* — author ConYel has not responded to maintainer follow-up in 17 days.

3. **#8424** (blocked, needs-author-action, since 2026-06-28): *.ignore File Mechanism* — author rakaarwaky needs to address maintainer questions.

4. **#8132** (blocked, needs-author-action, since 2026-06-22): *Replace React/Vite web UI with Rust→Wasm framework* — creator ConYel has not responded to split-from-#7674 discussion.

5. **#8550** (blocked, needs-maintainer-review, since 2026-06-30): *OpenAI-compatible chat completions endpoint* — despite an existing PR (#8486), maintainer review still needed.

6. **#6074** (2 comments, since 2026-04-24): *Track 153 commits lost in bulk revert for recovery* — aging audit issue with no resolution path, still in-progress and accepted.

7. **#5269** (2 comments, since 2026-04-04): *Improve Installation Documentation* — oldest open issue in the top-30, accepted with medium risk but no apparent movement.

**Key observation**: Several important RFCs (OCI registries, context compression, Wasm UI) have been blocked for 1-3+ weeks awaiting maintainer or author action. This suggests maintainer bandwidth may be stretched across the v0.8.3 milestone priorities.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*