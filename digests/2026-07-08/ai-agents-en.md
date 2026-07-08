# OpenClaw Ecosystem Digest 2026-07-08

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-08 01:21 UTC

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

# OpenClaw Project Digest — 2026-07-08

## Today's Overview

OpenClaw continues to show high community engagement with 500 issues and 500 PRs updated in the last 24 hours, though the project is currently in a maintenance-heavy phase with no new releases. The open-to-closed ratio for issues (379 open vs 121 closed) and PRs (358 open vs 142 merged/closed) indicates a growing backlog that maintainers are actively processing but not fully clearing. Several critical stability issues — including session-state corruption, silent message loss, and race conditions — remain open with Diamond Lobster severity ratings, suggesting that core reliability and security concerns are the project's current bottleneck. The high volume of PR activity (500 updated) and new PRs being filed hourly (at least 30 new today) shows a healthy contributor base, but many are marked with status labels like `📣 needs proof` and `⏳ waiting on author`, indicating a review bottleneck.

## Releases

No new releases were published today. The latest available version remains the previously reported build.

## Project Progress

**Merged/Closed PRs Today (out of 142):**

- **Refactoring & Cleanup:**
  - **#101941** `refactor(gateway): localize terminal helper types` — Cleans up gateway API surface by internalizing eight type aliases that had no cross-module consumers.
  - **#101937** `fix(status): remove dead-code || 1 fallback` — Removes impossible-branch fallback values from channel status display logic.

- **Infrastructure:**
  - **#68936** `Autofix: add PR review autofix pipeline + Windows daemon` — Adds Claude-powered automated PR review response pipeline and Windows background daemon for gateway supervision (merged from shadowleaf-studios).
  - **#90370** `[Feature Request] Support PostgreSQL as alternative to SQLite` — Closed, likely as design decision not to pursue.

- **UX Improvements:**
  - **#52972** `Fix: Incorrect 'I did not schedule a reminder' note` — Fixes spurious negation message appended after successful cron scheduling.
  - **#45388** `TUI --session mode doesn't live-stream messages` — Closed, fix deployed.

- **New Fixes in Review Pipeline:**
  - **#40418** `Feature Request: Automated Session Memory Preservation & Synthesis` — Closed with implementation.

## Community Hot Topics

### Most Active Issues (by comments)

1. **#25592** — *Text between tool calls leaks to messaging channels* (33 comments, Diamond Lobster)
   - Core UX problem: agent internal processing text exposed to users as visible messages
   - 🔗 [openclaw/openclaw Issue #25592](https://github.com/openclaw/openclaw/issues/25592)

2. **#44925** — *Subagent completion silently lost — no retry, no notification* (21 comments, Diamond Lobster)
   - Multiple failure modes where subagent results vanish without operator awareness
   - 🔗 [openclaw/openclaw Issue #44925](https://github.com/openclaw/openclaw/issues/44925)

3. **#11829** — *Security Roadmap: Protecting API Keys from Agent Access* (20 comments)
   - Foundational security concern: LLM provider keys, model catalog serialization exposes secrets
   - 🔗 [openclaw/openclaw Issue #11829](https://github.com/openclaw/openclaw/issues/11829)

4. **#22676** — *Signal daemon stop() race condition on SIGUSR1 restart* (17 comments, Diamond Lobster)
   - Orphaned processes and send failures during gateway restarts
   - 🔗 [openclaw/openclaw Issue #22676](https://github.com/openclaw/openclaw/issues/22676)

5. **#22438** — *Tiered bootstrap file loading for progressive context control* (17 comments, Diamond Lobster)
   - Token waste reduction proposal; high demand for context window optimization
   - 🔗 [openclaw/openclaw Issue #22438](https://github.com/openclaw/openclaw/issues/22438)

### Most Upvoted Requests (by 👍)

| Issue | Title | 👍 | Status |
|-------|-------|----|--------|
| #39604 | `tools.web.fetch.allowPrivateNetwork` | 11 | Open |
| #42840 | MathJax/LaTeX support in Control UI | 9 | Open |
| #37634 | Sandbox workspace writable when workspaceAccess=none | 7 | Open |
| #20786 | Telegram Business Bot support | 6 | Open |
| #27445 | `announceTarget` option for sub-agent routing | 5 | Open |

## Bugs & Stability

### Critical (Diamond Lobster / P1)

1. **#25592** — **Text between tool calls leaks to messaging channels** (P1)
   - Agent internal text (error handling, processing notes) sent as visible messages
   - ⚠️ Fix PR not yet identified

2. **#44925** — **Subagent completion silently lost** (P1)
   - Results vanish on timeout, no retry, no notification
   - Multiple failure patterns documented (E31, E42, E45)
   - ⚠️ Linked PR open

3. **#22676** — **Signal daemon race condition on SIGUSR1 restart** (P1)
   - Orphaned processes, port conflicts, file locks
   - ⚠️ Linked PR open, updated today

4. **#85333** — **`openclaw doctor --fix` 4-5x slower** (P1, Performance Regression)
   - 55s → 229s+ on production VPS
   - Session snapshot path traversal bottleneck
   - ☣️ Needs live repro

5. **#38327** — **"Cannot convert undefined or null to object"** (P1, Regression)
   - Breaks Google Vertex / Gemini models on 2026.3.2
   - Blocks all embedded agent usage
   - ☣️ Source repro available

6. **#31583** — **`exec` tool ignores `skills.entries.*.env`** (P1, Regression)
   - Environment variables not passed to subprocesses
   - Blocks secret injection (GOG_KEYRING_PASSWORD pattern)
   - ☣️ Linked PR open

7. **#99241** — **Tool outputs render as image attachments, agent blind** (P1)
   - ANSI-heavy workflows produce `(see attached image)` placeholders
   - Agent cannot read original stdout
   - ☣️ Needs live repro

8. **#41165** — **Telegram DMs pollute heartbeat/main session** (P1)
   - DM routing still incorrect after #40519 fix
   - ☣️ Linked PR open

### High (Platinum Hermit / P1)

- **#89041** — Discord WS 8.21.0 receiver limits cause disconnections (Fix PR: #89041, `👀 ready for maintainer look`)
- **#38439** — Webchat avatar 404 regression (Fix PR linked)
- **#41199** — Agent-to-Agent communication parameter conflicts (Updated today)
- **#41744** — Feishu image tool result loss (Linked PR open)

### Notable New Bugs Filed Today

- **#101932** — Session stalls when parent token probing hangs (Fix: #101932, `📣 needs proof`)
- **#101926** — Native `/think` menus unresponsive on slow model discovery (Fix: #101926)
- **#101939** — False "Response body truncated" warning on exact-size streams (Fix: #101939)
- **#101940** — `media://` references bypass image compression, causing provider errors (Fix: #101940)

## Feature Requests & Roadmap Signals

### High-Impact Requests Likely for Next Release

1. **#39604** — **`tools.web.fetch.allowPrivateNetwork`** (11 👍)
   - Opt-in private network access for `web_fetch`
   - Strong community demand; relatively simple config change
   - ⏳ High likelihood for next patch release

2. **#22438** — **Tiered bootstrap file loading** (17 comments)
   - Progressive context control to save token budget
   - Multiple design discussions, product decision pending
   - ⏳ Moderate likelihood, needs design finalization

3. **#42840** — **MathJax/LaTeX rendering in Control UI** (9 👍)
   - Display mathematical formulas properly
   - Strong academic/scientific user demand
   - ⏳ Moderate likelihood

4. **#42475** — **Per-agent cost budget enforcement** (12 comments)
   - Daily/monthly cost caps at gateway level
   - Critical for production operators
   - ⏳ Likely in next minor release

5. **#20786** — **Telegram Business Bot support** (6 👍)
   - Enable Business-connected personal chat handling
   - ⏳ Needs product decision

### Architectural Signals

- **#42026** — RFC: Distributed Agent Runtime (7 comments)
  - Split gateway into control plane + agent runtime
  - Major architectural shift, long-term roadmap item
- **#35203** — Multi-Agent Collaboration Enhancement RFC (10 comments)
  - Capability profiling, shared blackboard, token governance
  - Active design discussion

## User Feedback Summary

### Pain Points (Frequently Reported)

1. **Message Loss & Visibility**
   - "Text between tool calls leaks to channels" (#25592)
   - "Tool outputs become image attachments, agent blind" (#99241, #96857)
   - "Subagent results silently lost" (#44925)
   - Multiple overlapping reports of agent blindness to its own tool outputs

2. **Session & State Instability**
   - "Telegram DMs pollute main heartbeat session" (#41165)
   - "Multi-agent orchestration: config overwrites, lock failures" (#43367)
   - "Memory management is in chaos — different behavior across users" (#43747)
   - Users reporting unpredictable, non-deterministic memory behavior

3. **Security Anxiety**
   - "API keys leak to LLM / chat" (#11829)
   - "Exec tool doesn't inherit env secrets" (#31583)
   - "No exclude patterns for backup — sensitive data exposure risk" (#40786)
   - Strong demand for sandbox and secret management improvements

4. **Configuration Frustration**
   - "Bootstrap files in agentDir silently ignored" (#29387, 5 👍)
   - "Write tool lacks append mode — cron sessions overwrite files" (#40001)
   - "Docker + Sandbox workspace binding broken" (#31331, 4 👍)
   - "Slack tool-level progress not shown" (#33413, 3 👍)

### Satisfaction Signals

- **ClawSweeper automation** (#101748) being documented suggests maintainers are investing in developer workflow
- **PR #101927** (Android app session binding) shows mobile surface getting attention
- **Multiple fix PRs** reaching `👀 ready for maintainer look` status indicates community confidence in patches
- **Theme customization system** (#28300, 5 👍) and **reasoning stream** (#42276) show UI polish is valued

### User Sentiment

The community appears **frustrated but engaged** — high issue and PR volume with many detailed, well-documented bug reports (source-repro, linked PRs) suggests users are invested in making the project better but hitting real reliability walls. The Diamond Lobster severity concentration on message-loss, session-state corruption, and security issues indicates these are the top barriers to production deployment.

## Backlog Watch

### High-Priority Issues Needing Maintainer Attention

| Issue | Title | Age | Status | Concern |
|-------|-------|-----|--------|---------|
| #11829 | Security Roadmap: API Keys protection | Created 2026-02-08 | Needs product decision | 5 months without clear progress |
| #85333 | `doctor --fix` 4-5x regression | Created 2026-05-22 | Needs live repro | Marked stale, P1 performance bug |
| #38439 | Webchat avatar 404 regression | Created 2026-03-07 | Needs live repro | Regression affecting UI |
| #41199 | A2A parameter conflicts | Created 2026-03-09 | Needs live repro | Blocks agent-to-agent communication |
| #40678 | TUI cross-channel visibility | Created 2026-03-09 | Needs live repro | Stable maturity, unresolved |

### Stale Items Requiring Review

- **#85334** — `doctor --fix` injects circular plugin path (Created 2026-05-22, stale)
- **#41744** — Feishu image tool loss (Created 2026-03-10, stale)
- **#49931** — Configurable shell override for exec tool (Created 2026-03-18, stale)
- **#39406** — Suppress transient tool error warnings (Created 2026-03-08, mature/stable)

### PRs Waiting on Maintainers

- **#89041** — Discord WS limit fix (`👀 ready for maintainer look`)
- **#89038** — QQbot reconnection fix (`👀 ready for maintainer look`)
- **#101598** — Microsoft Foundry `az login` stream errors (`👀 ready for maintainer look`)
- **#100845** — One-shot agent OTel diagnostics export (`🚀 automerge armed`)

**Overall Assessment:** OpenClaw is in a **stability crunch** — the project has rich features and strong community adoption, but fundamental reliability issues (message loss, session corruption, race conditions) are accumulating faster than fixes are being merged. The maintainer review bottleneck (many PRs labeled `needs proof` or `waiting on author`) suggests that while the community is producing fixes, throughput to merge is constrained. Until the P1 Diamond Lobster issues are resolved, production deployments will require careful workarounds and monitoring.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the daily digests for July 8, 2026.

---

### 1. Ecosystem Overview

The open-source personal AI agent ecosystem is characterized by high velocity and a sharp divide between stability and innovation. Projects like OpenClaw, Hermes Agent, and ZeroClaw show massive daily throughput (50+ PRs), but their communities are heavily concentrated on bug-fixing and reliability issues, signaling a "stability crunch" in the wake of rapid feature expansion. Concurrently, a coordinated wave of critical security disclosures hit the ecosystem's smaller players (LobsterAI, TinyClaw), indicating a growing security researcher focus and surface area. The dominant themes across the landscape are an urgent need for hardened session/state management, user demand for granular safety controls, and a push toward modularity and minimal defaults.

### 2. Activity Comparison

| Project | Issues (Updated/24h) | PRs (Updated/24h) | Releases | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 (121 closed) | 500 (142 closed) | None | 6/10 (High backlog, P1 bugs) |
| **NanoBot** | 12 (3 closed) | 31 (11 closed) | None | 7/10 (High velocity, security spikes) |
| **Hermes Agent** | 50 (22 closed) | 50 (16 closed) | **v0.18.1** | 8/10 (Strong throughput, patch release) |
| **PicoClaw** | 7 | 4 | None | 5/10 (Low activity, critical bug unaddressed) |
| **NanoClaw** | 1 (new) | 24 (9 closed) | None | 7/10 (Security focus, doc overhaul) |
| **NullClaw** | 0 | 0 | None | N/A |
| **IronClaw** | 31 (9 closed) | 50 (8 closed) | None | 7/10 (Steady bug-bash, integration gaps) |
| **LobsterAI** | ~5 (5 closed) | 16 (14 closed) | **2026.7.7** | 8/10 (High merge rate, major security discl.) |
| **TinyClaw** | 9 (0 closed) | 0 | None | 2/10 (Zero dev activity, 9 crit vulns) |
| **Moltis** | 0 | 0 | None | N/A |
| **CoPaw** | 17 (10 closed) | 38 (15 closed) | **v2.0.0-beta.3** | 7/10 (Pre-release bugs, high velocity) |
| **ZeptoClaw** | 0 | 0 | None | N/A |
| **ZeroClaw** | 23 | 50 (4 closed) | None | 8/10 (Safety focus, good bug closure rate) |

### 3. OpenClaw's Position

**Advantages:**
- **Community Scale:** With 500 issues and PRs updated daily, OpenClaw has the largest community by a significant margin, dwarfing competitors like Hermes Agent (50/50).
- **Feature Richness:** The project supports a vast array of integrations (Telegram, Feishu, Discord) and advanced features (sub-agents, cron scheduling, TUI) that create inertia for its user base.

**Technical Approach:** OpenClaw uses a plugin-based architecture with a central gateway, different from Hermes Agent's deeply integrated stack or ZeroClaw's Rust-based, safety-oriented core.

**Differentiation vs. Peers:**
- *vs. Hermes Agent:* OpenClaw has a larger community but a lower health score due to a larger, aging backlog. Hermes is more responsive, releasing patches more frequently.
- *vs. NanoBot:* OpenClaw is more "enterprise/community" scale, whereas NanoBot focuses on a lean, maintainer-driven core. OpenClaw's backlog is much more severe.
- *vs. LobsterAI:* LobsterAI (from NetEase) has a more polished, consumer-oriented UI (desktop client) and is better at shipping releases. OpenClaw is more about infrastructure and raw capability.

**Key Risk:** OpenClaw's primary advantage (volume) is also its primary risk. The growing backlog of open issues (379) and PRs (358) relative to closed items indicates a maintenance bottleneck that could drive contributors to less congested projects like ZeroClaw or Hermes Agent.

### 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects, indicating top-of-mind industry needs:

- **Security & Secret Management:** A universal, critical need. **OpenClaw** (#11829) and **IronClaw** (Slack unmount) struggle with secret exposure, while **LobsterAI** (#2286), **NanoClaw** (#2970), and **TinyClaw** (#286-294) were hit by severe API/token disclosure vulns.
- **Granular Safety & Approval Controls:** Users want more than global "allow/deny" toggles. **ZeroClaw** (#7155 - per-execution tier for shell), **OpenClaw** (#39604 - `allowPrivateNetwork`), and **Hermes Agent** (#51221 - approval policies) all see demand for configurable risk boundaries.
- **Session & State Reliability:** Non-deterministic memory behavior (**OpenClaw** #43747), context erasure on interruption (**ZeroClaw** #8794), and stale session restoration (**Hermes Agent** #60541) are widespread pain points.
- **Modularity & Minimal Defaults:** Users want to reduce bloat. **Hermes Agent** (#19986 - optional skills), **OpenClaw** (#22438 - tiered bootstrap), and **IronClaw** (composition refactoring) all work toward smaller, opt-in installs.
- **Chat Platform Reliability:** Specific integration issues are common. **NanoBot** (WhastApp groups broken), **IronClaw** (Slack pairing lock-in), **PicoClaw** (NanoKVM fails), and **CoPaw** (DingTalk cross-user `stop`) highlight the difficulty of maintaining stable multi-channel support.

### 5. Differentiation Analysis

- **Stability Champions (Hermes Agent, ZeroClaw):** These projects prioritize a robust core and frequent, safe releases. ZeroClaw focuses on safety (SOP gates, tool filters) and memory sanitation. Hermes Agent has the most impressive issue closure rate.
- **Security Emergencies (TinyClaw, LobsterAI):** These projects are currently in crisis mode, having received a coordinated batch of severe security reports. Their immediate roadmap is dominated by patching fundamental auth/input-validation flaws.
- **Feature Innovators (CoPaw, ZeroClaw):** CoPaw is the most feature-aggressive, pushing a pre-release cycle with major UX overhauls (scheduled tasks UI). ZeroClaw is building SOP visual authoring, a clear differentiator for complex workflows.
- **Maintainer-Bottleneck Projects (OpenClaw, PicoClaw):** These have large feature sets and user bases but are showing signs of stress where maintainer capacity is the limiting factor for progress. OpenClaw has the largest gap between incoming contributions and merged fixes.
- **Lean & Focused (NanoBot, NanoClaw):** NanoBot is highly responsive to its core set of bugs and features, while NanoClaw is operating efficiently with a low issue count and a focus on docs/infrastructure.

### 6. Community Momentum & Maturity

**Tier 1 (Rapid Iteration & High Maturity):**
- **Hermes Agent** & **ZeroClaw:** These projects demonstrate the best balance of velocity and maturity. They process high volumes of work with clear prioritization (bug bash, safety focus) and release regularly.
- **CoPaw:** Despite being in pre-release, it shows exceptional velocity and a large pool of first-time contributors. It is rapidly iterating towards a GA release.

**Tier 2 (High Velocity, Managing Backlogs):**
- **OpenClaw:** The largest community, but maturity is constrained by a growing and aging backlog. The project is stuck in a "stability crunch."
- **IronClaw:** Strong engineering throughput with a visible bug-bash discipline, but lacks the same community-scale as the top tier. Integration stability (GitHub/Slack) is a weak point.

**Tier 3 (Stabilizing / Security Response):**
- **NanoBot, LobsterAI:** These projects have good developer responsiveness and release cadence, but are currently context-switching to address critical security disclosures.
- **NanoClaw:** A mature, low-volume project, but the critical unauthenticated webhook vulnerability requires an immediate response.

**Tier 4 (Dormant / Critical Risk):**
- **PicoClaw, TinyClaw, NullClaw, Moltis, ZeptoClaw:** These projects show very low or zero activity. TinyClaw is the most dangerous, with 9 high/critical vulnerabilities open and no fixes in sight. PicoClaw has a critical rate-limiting bug unresolved.

### 7. Trend Signals

1.  **Security Hardening is the Primary Development Bottleneck:** The wave of `CWE-22` (path traversal) and unauthenticated API disclosures is not a coincidence. As agents gain more system access, attackers are probing the control-plane boundaries. Projects that fail to sandbox these APIs (e.g., TinyClaw) are at severe risk.
2.  **The "Safety Sandwich" is an Industry Standard:** The combination of Tool-Filter Groups (ZeroClaw), Approval Gates (Hermes Agent), and Prompt Injection Overrides is emerging as a required feature set. Users are no longer satisfied with a single "dangerous tool" toggle.
3.  **Agent Memory is the Weakest Link:** The persistent reports of non-deterministic memory behavior, silent context loss (ZeroClaw #8794), and session corruption (OpenClaw) indicate that reliable, long-term memory remains an unsolved engineering problem in this ecosystem.
4.  **SOPs (Standard Operating Procedures) are the Next Frontier:** ZeroClaw’s investment in visual SOP authoring and CoPaw’s focus on plan-mode workflows suggest the community is outgrowing simple chat and demanding structured, repeatable, and auditable agent workflows.
5.  **Niche Hardware Integration is Growing:** PicoClaw’s ADB tool and NanoKVM support signal a demand for agents that control physical devices and embedded system. This is a new, non-chat-based use case gaining traction.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-07-08

## Today's Overview

NanoBot had a **highly active development day** with 31 PRs and 12 issues updated in the last 24 hours, driven primarily by the maintainer team and external contributors. Activity is concentrated on critical bug fixes, security hardening, and stabilization across multiple channels (WhatsApp, Telegram, QQ, Slack). While no new releases were published today, the project processed 11 merged/closed PRs and closed 3 issues, reflecting strong maintenance velocity. The issue tracker shows a **concerning spike in security reports** (3 newly filed) alongside regression bugs in messaging channels and core agent tooling.

## Releases

No new releases today. The latest versions remain `0.2.0` and `0.2.2`, with users in issues reporting regressions compared to `0.1.5post2`.

## Project Progress

**11 PRs were merged or closed today**, representing substantive progress across multiple areas:

- **Provider-Hosted Web Search** — PR [#3743](https://github.com/HKUDS/nanobot/pull/3743) (merged): Adds opt-in support for provider-native web search tools (e.g., Azure OpenAI Responses API), with configurable local fallback behavior. This closes the related feature request [#3741](https://github.com/HKUDS/nanobot/issues/3741).
- **Camera Capture Tool** — PR [#3378](https://github.com/HKUDS/nanobot/pull/3378) (merged): New `camera_capture` tool using OpenCV for webcam photo capture (disabled by default).
- **WeChat Token Fix** — PR [#3517](https://github.com/HKUDS/nanobot/pull/3517) (merged): Fixes silent message drops from cron jobs due to stale `context_token`.
- **Agent Callback Simplification** — PR [#3232](https://github.com/HKUDS/nanobot/pull/3232) (merged): Simplifies task done-callback logic and restores deleted code from upstream sync.
- **Feishu Session Divider** — PR [#4763](https://github.com/HKUDS/nanobot/pull/4763) (merged): Adds new session divider for authorized Feishu p2p messages.

Additional open PRs advancing toward merge include fixes for MCP shutdown crashes ([#4842](https://github.com/HKUDS/nanobot/pull/4842)), multimodal message handling and tool validation ([#4837](https://github.com/HKUDS/nanobot/pull/4837)), and WhatsApp group allowlists ([#4834](https://github.com/HKUDS/nanobot/pull/4834)).

## Community Hot Topics

**Most active discussions (by comments):**

1. **Issue #4013** — *"Error calling LLM: stream stalled for more than 90 seconds"* (6 comments, CLOSED). User reported a regression when upgrading from `0.1.5post2` to `0.2.0`, with the AI assistant providing unhelpful guidance about hardcoded `/goal` references. The error made "any real work useless" per the reporter. Now closed, indicating a fix was deployed.

2. **Issue #4823** — *"WhatsApp groups — group allow is broken"* (3 comments, OPEN). User reports that post-`0.2.2`, WhatsApp group responses arrive in every group, and `allowFrom` group ID filtering is non-functional. A fix PR ([#4834](https://github.com/HKUDS/nanobot/pull/4834)) is already open to restore this behavior.

3. **Issue #4829** — *"aiohttp missing in the slack dependencies"* (2 comments, OPEN). A packaging dependency issue preventing Slack plugin enablement. A fix PR ([#4830](https://github.com/HKUDS/nanobot/pull/4830)) is open to add the missing `aiohttp` dependency.

**Underlying needs**: The community is signaling strong demand for **reliable messaging integrations** (especially WhatsApp and Slack), **stable upgrade paths** between versions, and **better error transparency** — the "stream stalled" error and the suppressed tool validation path ([#4805](https://github.com/HKUDS/nanobot/issues/4805)) show users want clarity when things fail.

## Bugs & Stability

**High Severity:**

- **WhatsApp group allowlist regression** [#4823](https://github.com/HKUDS/nanobot/issues/4823) — CRITICAL: Groups feature completely broken post-0.2.2. Fix PR [#4834](https://github.com/HKUDS/nanobot/pull/4834) is open with priority p1.
- **`msg.content.strip()` crashes on multimodal messages** [#4800](https://github.com/HKUDS/nanobot/issues/4800) — CRITICAL: Unconditional `.strip()` call crashes on list-form content (multimodal). Fix PR [#4837](https://github.com/HKUDS/nanobot/pull/4837) is open.
- **Tool validation errors silently swallowed** [#4805](https://github.com/HKUDS/nanobot/issues/4805) — HIGH: `suppress(Exception)` in `prepare_call` masks critical validation failures, leading to confusing fallback behavior. Fix included in PR [#4837](https://github.com/HKUDS/nanobot/pull/4837).

**Medium Severity:**
- **Slack dependency missing `aiohttp`** [#4829](https://github.com/HKUDS/nanobot/issues/4829) — HIGH: Plugin cannot be enabled. Fix PR [#4830](https://github.com/HKUDS/nanobot/pull/4830) is open.
- **WebUI landing message misrouted to unrelated chat** [#4835](https://github.com/HKUDS/nanobot/issues/4835) — MEDIUM: Race condition in new chat creation. Fix PR [#4836](https://github.com/HKUDS/nanobot/pull/4836) is open.
- **MCP IDLE timeout reconnect crashes gateway** (PR [#4764](https://github.com/HKUDS/nanobot/pull/4764)) — MEDIUM: Shutdown crash when browser-agent subprocess times out. PR [#4842](https://github.com/HKUDS/nanobot/pull/4842) adds CancelledError handling.
- **Matrix E2EE "untrusted" device** [#4841](https://github.com/HKUDS/nanobot/issues/4841) — MEDIUM: No cross-signing or SAS verification path available, leaving bot device permanently untrusted in Element clients.
- **Shell subprocess zombie leak** [#4840](https://github.com/HKUDS/nanobot/pull/4840) — MEDIUM: Zombie processes from subprocess exit paths; fix PR adds zombie reaper.
- **Telegram HTML parse_mode for overflow chunks** [#4839](https://github.com/HKUDS/nanobot/pull/4839) — MEDIUM: Streaming overflow chunks get incorrect parse mode. Fix PR open.

**Low Severity (Non-critical UX):**
- **QQ reconnect lacks exponential backoff** (PR [#4838](https://github.com/HKUDS/nanobot/pull/4838)) — LOW: Spammy reconnection attempts; fix PR adds 2s→60s backoff.
- **CLI Shift+Enter dumps raw escapes** (PR [#4832](https://github.com/HKUDS/nanobot/pull/4832)) — LOW: Regression from multiline input fix, terminal-specific.
- **Narrow prompt rail in WebUI** (PR [#4831](https://github.com/HKUDS/nanobot/pull/4831)) — LOW: Layout issue on narrow chat columns.

**Security Vulnerabilities (CRITICAL — NEW TODAY):**

Three closely related security issues were filed by YLChen-007:
1. **#4825** — Unauthenticated localhost callers can mint WebUI API tokens via `/webui/bootstrap` (OPEN, 0 comments)
2. **#4826** — WebUI bootstrap issues API-capable bearer tokens to any localhost process without prior authentication (OPEN, 0 comments)
3. **#4827** — Embedded WebUI bootstrap issues API bearer tokens to unauthenticated localhost callers (OPEN, 0 comments)

These represent a **token issuance vulnerability** when no `tokenIssueSecret` or static token is configured. Any unprivileged local process can obtain authenticated WebUI API tokens. No fix PRs open yet.

Additionally, a previously filed security issue **#4611** (DNS rebinding TOCTOU in SSRF validation) was closed with a fix, indicating the project is actively addressing security concerns.

## Feature Requests & Roadmap Signals

**New features merged today:**
- **Provider-hosted web search** ([#3743](https://github.com/HKUDS/nanobot/pull/3743)) — Likely to appear in the next release, enabling native `web_search` tool integration for compatible providers.
- **Camera capture tool** ([#3378](https://github.com/HKUDS/nanobot/pull/3378)) — Adds physical webcam interaction capability.

**Open feature PRs in progress:**
- **WebUI file edit diff view** ([#4828](https://github.com/HKUDS/nanobot/pull/4828)) — Unified diff visualization for file edits in WebUI.
- **MCP server idle timeout auto-kill** ([#4506](https://github.com/HKUDS/nanobot/pull/4506)) — Prevents resource leaks by auto-terminating idle MCP servers.
- **Gate sustained goals behind explicit runtime mode** ([#4833](https://github.com/HKUDS/nanobot/pull/4833)) — Moves `long_task`/`complete_goal` to runtime-gated tools, only injected during `/goal` turns.

**Predictions for v0.2.3**: Given the volume of p1-priority fixes queued with open PRs, the next release will likely include: WhatsApp group allowlist fix, Slack aiohttp dependency fix, multimodal content crash fix, MCP shutdown crash fix, and the three security token issuance fixes.

## User Feedback Summary

**Satisfaction indicators:**
- User mxnbf explicitly praised v0.1.5post2 ("it's been very good, way to say ty") while expressing frustration with v0.2.0 regression.
- Multiple contributors are actively submitting fixes, indicating a healthy contributor ecosystem.
- The security issues (#4825-4827) were reported with detailed, professional advisory formatting, suggesting engaged security-focused users.

**Pain points (by frequency):**
1. **Upgrade regressions** — v0.2.0 and v0.2.2 introduced breaking changes in WhatsApp groups, LLM streaming, and CLI input, frustrating users who had stable setups on v0.1.5post2.
2. **Silent failures** — Tool validation errors being swallowed ([#4805](https://github.com/HKUDS/nanobot/issues/4805)) and the LLM "stalled" error without actionable diagnostics ([#4013](https://github.com/HKUDS/nanobot/issues/4013)) erode user trust.
3. **Config complexity** — WhatsApp group allowlist behavior changed without clear documentation, and the Matrix E2EE untrusted device has no configured resolution path.
4. **Security concern** — Three unauthenticated token issuance reports filed today suggest users are actively probing attack surfaces.

**Underlying user needs**: Users want **backward-compatible upgrades**, **transparent error messaging** (not suppressed exceptions), and **documented configuration changes** between versions.

## Backlog Watch

**Issues needing maintainer attention:**
- **#4825, #4826, #4827** (Security: WebUI token issuance) — Filed today, no fix PRs yet. Critical severity, especially since WebUI is bound to loopback and could be exploited by local malware.
- **#4841** (Matrix E2EE untrusted device) — Filed today, no fix PR open. Important for Matrix-using installations with E2EE enabled.
- **#4805** (Tool validation errors suppressed) — Fix included in [#4837](https://github.com/HKUDS/nanobot/pull/4837) but PR is still open; needs review and merge.
- **#4611** (DNS rebinding TOCTOU) — Now CLOSED with a fix, good to see this addressed, though the vulnerability was open for 7 days.

**Long-standing items:**
- **PR #4506** (MCP idle timeout auto-kill, opened 2026-06-25) — Still open with no comments; may need maintainer feedback to move forward.
- **PR #4764** (MCP reconnect cancel scopes, opened 2026-07-05) — Still open; author notes it's "not the most elegant way to fix this," suggesting maintainer review is needed to accept or request improvements.

**Recommendation**: The three security token issues should be **prioritized for immediate fix** given their critical severity and potential exploitability by local processes. The maintainer team should consider coordinated disclosure if a patch is in progress.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — July 8, 2026

## Today's Overview

Hermes Agent maintains very high development velocity with 50 issues and 50 PRs updated in the last 24 hours, plus a new patch release. The project has 28 open active issues and 34 open PRs, indicating a healthy pipeline of ongoing work. The v0.18.1 patch release rolls up approximately 660 PRs from the past week, reflecting rapid iteration focused on bug fixes, hardening, and stability improvements. Activity levels suggest a well-maintained project with strong community engagement and responsive maintainers.

## Releases

**v0.18.1 (v2026.7.7)** — *Patch Release, July 7, 2026*

This tag aggregates ~660 PRs merged since v0.18.0 (July 1) into a stable release for downstream consumers. Changes include bug fixes, hardening improvements, and in-progress feature work. No breaking changes or migration notes are documented. This release is intended for Docker images, hosted deployments, and PyPI distribution.

## Project Progress

Today 16 PRs were closed/merged and 22 issues were closed. Notable merged/closed items include:

- **PR #60595** (merged): Release v0.18.1 patch tag (chore/refactor)
- **PR #60599** (merged): Fail-closed syntax gate for JSON/YAML/TOML writes — fixes issue #60525 where invalid content was written to disk before syntax validation
- **PR #60380** (merged): Suppressed "Event loop is closed" traceback floods during MCP shutdown
- **Issue #50199** (closed): Root-caused and fixed `delegation.base_url` being ignored at runtime due to stale CLI_CONFIG cache
- **Issue #18946** (closed): Fixed `hermes config set delegation.*` having no effect on running processes (same config cache staleness pattern)
- **Issue #60584** (closed): Fixed one-shot chat mode clearing screen and scrollback before displaying summaries
- **Issue #59349** (closed): Fixed gateway leaking stdio-MCP subprocesses and file descriptors on failed initialization (unbounded retry loop → EMFILE)

## Community Hot Topics

### Most Active Issues

1. **#19986 — [OPEN] Make non-core bundled skills optional** ([Link](https://github.com/NousResearch/hermes-agent/issues/19986))
   - 8 comments, 3 👍
   - **Need:** Users want a minimal default install footprint. Shipping all bundled skills into every profile creates update bloat, larger deployment sizes, and maintenance burden for unused content. This has been open since May 5 and reflects a long-standing desire for modularity.

2. **#6838 — [CLOSED] MiniMax provider connection drops** ([Link](https://github.com/NousResearch/hermes-agent/issues/6838))
   - 7 comments
   - **Need:** Reliable third-party provider connectivity. After switching from OpenClaw to Hermes, users experienced `RemoteProtocolError` and connection drops specifically with MiniMax. This was fixed on main and is now closed, demonstrating responsive provider support.

3. **#55790 — [OPEN] Stale credential pool entries persist in model picker** ([Link](https://github.com/NousResearch/hermes-agent/issues/55790))
   - 6 comments
   - **Need:** After removing a provider via Desktop UI settings, it continues appearing in the model picker dropdown. This spans two components (desktop and dashboard) and creates user confusion about what providers are actually active.

4. **#51221 — [CLOSED] User-configurable runtime approval for external actions** ([Link](https://github.com/NousResearch/hermes-agent/issues/51221))
   - 6 comments, 2 👍
   - **Need:** Users want fine-grained control over which dangerous actions require manual approval. The current system is limited, and this feature request for configurable approval policies was implemented (closed with sweeper tag indicating risk-security-boundary).

### Most Active PRs

*No PRs have comment counts listed (all show "undefined"), but the most recently updated include:*

- **PR #60610** — Fix `killpg` guard against killing own process group ([Link](https://github.com/NousResearch/hermes-agent/pull/60610))
- **PR #60146** — Discord `/branch` and `/merge` thread management ([Link](https://github.com/NousResearch/hermes-agent/pull/60146))
- **PR #60567** — Accept "auto" as alias for "smart" approval mode ([Link](https://github.com/NousResearch/hermes-agent/pull/60567))

## Bugs & Stability

### Critical (P1)

- **#60525 — [OPEN] `write_file()` commits to disk before syntax check runs** ([Link](https://github.com/NousResearch/hermes-agent/issues/60525))
  - **Impact:** Invalid JSON/YAML/TOML content is written to disk and reported as successful — the syntax check runs after commit and only attaches a result, never setting the error key. **⚠️ Data corruption risk.**
  - **Fix:** PR #60599 was merged today, implementing a fail-closed syntax gate that blocks invalid writes.

### High Priority (P2)

- **#60543 — [OPEN] `/steer` race condition between tool batch drain and next API call** ([Link](https://github.com/NousResearch/hermes-agent/issues/60543))
  - Out-of-band steer messages can be silently lost or redelivered as raw command text. Requires session-state handling fix.

- **#60597 — [OPEN] Gemini provider UI crash on streaming response** ([Link](https://github.com/NousResearch/hermes-agent/issues/60597))
  - Desktop wrapper crashes with "Attempted to access streaming response content, without having called read()" when using workspace tools with Gemini provider.

- **#60551 — [OPEN] Config write guard and `hermes config set` string scalar bug** ([Link](https://github.com/NousResearch/hermes-agent/issues/60551))
  - Agent cannot edit its own config file, and `config set` writes strings for list keys. Blocks users from managing secrets through config.

- **#42248 — [OPEN] Kanban workers deadlock with custom local model providers** ([Link](https://github.com/NousResearch/hermes-agent/issues/42248))
  - Workers systematically deadlock in `__psynch_cvwait` within minutes when using OpenAI-compatible local models. Process shows 0% CPU but dispatcher heartbeats continue.

- **#60572 — [OPEN] Dashboard spawns MCP server processes unnecessarily** ([Link](https://github.com/NousResearch/hermes-agent/issues/60572))
  - Starting dashboard with `--open-profile` launches MCP processes even though the web UI doesn't use MCP tools, causing duplicates when a gateway is also running.

- **#60541 — [OPEN] Desktop cold boot restores stale session** ([Link](https://github.com/NousResearch/hermes-agent/issues/60541))
  - App navigates to localStorage-pinned session ID without backend validation, stranding users on deleted/rotated sessions.

- **#60536 — [OPEN] Windows desktop bug (logs attached)** ([Link](https://github.com/NousResearch/hermes-agent/issues/60536))
  - Symptoms described only through pastebin logs. Needs reproduction to identify severity.

- **#60542 — [OPEN] One-directional GUI-backend version check** ([Link](https://github.com/NousResearch/hermes-agent/issues/60542))
  - Old GUI on modern backend passes silently — no warning when desktop app lags behind the engine. PR #60608 addresses this with a reverse contract check.

### Medium (P3)

- **#60603 — [OPEN] `/compress` command not recognized in desktop** ([Link](https://github.com/NousResearch/hermes-agent/issues/60603))
- **#45454 — [OPEN] Gateway crashes with `SystemExit: 75` on Telegram polling** ([Link](https://github.com/NousResearch/hermes-agent/issues/45454))
- **#60566 — [OPEN] MCP catalog git clone operations lack timeouts** ([Link](https://github.com/NousResearch/hermes-agent/pull/60566)) — Fix PR exists

## Feature Requests & Roadmap Signals

### Likely for Next Release

1. **Zulip integration** — PR #3335 adds Zulip as a bundled platform plugin ([Link](https://github.com/NousResearch/hermes-agent/pull/3335))
   - Has been open since March 27 and is still being updated. Likely nearing completion.

2. **Discord thread branching** — PR #60146 adds `/branch` and `/merge` commands for thread management ([Link](https://github.com/NousResearch/hermes-agent/pull/60146))
   - Allows creating sub-threads for parallel conversations and merging results back.

3. **Desktop imprints (thumbs up/down)** — PR #60581 adds one-tap feedback that Hermes remembers ([Link](https://github.com/NousResearch/hermes-agent/pull/60581))
   - Provides persistent user preference signals straight from chat interface.

4. **Optional non-core skills** — Issue #19986 proposes making bundled skills optional ([Link](https://github.com/NousResearch/hermes-agent/issues/19986))
   - Users want minimal default installs. This has 3 👍 and has been open since May — likely to be implemented given community interest.

### Longer-Term Signals

- **User-configurable runtime approval** (now closed/implemented) indicates movement toward more granular permission systems
- **Persistent session support** (Issue #22027) for tasks continuing when browser tab closes — users want background task execution
- **Zulip integration** suggests expansion beyond Discord and Telegram into enterprise/team chat platforms

## User Feedback Summary

### Pain Points

- **Config management friction**: Users report that `hermes config set` changes silently don't take effect in running processes, requiring restarts. Multiple related bugs (#18946, #50199, #57930, #51435) indicate systemic config caching issues.
- **Provider reliability**: Connection drops with MiniMax (#6838) and deadlocks with custom local models (#42248) frustrate users who depend on specific providers.
- **UI inconsistencies**: Windows users report chat alignment issues (#60596), and desktop users encounter crashes with Gemini streaming (#60597).
- **Session state fragility**: Lost `/steer` messages (#60543), stale session restoration (#60541), and session loss on tab close (#22027) degrade the conversation experience.
- **MCP subprocess leaks**: Multiple reports (#59349, #57228, #57355) of zombie/orphan subprocesses accumulating, leading to FD exhaustion (EMFILE) and resource issues in long-running deployments.

### Positive Signals

- **Responsive bug fixing**: The rapid closure of MCP subprocess leak issues and the v0.18.1 patch release demonstrate strong maintainer responsiveness.
- **Feature development**: Discord thread branching and desktop imprints show active feature development alongside bug fixes.
- **Community contributions**: Many PRs come from external contributors (trac3r00, Vencounsel, whichguy, etc.), indicating a healthy contributor ecosystem.

## Backlog Watch

### Long-Unanswered Issues Needing Attention

1. **#19986 — Make non-core bundled skills optional** ([Link](https://github.com/NousResearch/hermes-agent/issues/19986))
   - Open since May 5 (64 days). 3 👍, 8 comments. No maintainer response visible. Significant community interest.

2. **#42248 — Kanban workers deadlock with custom local model providers** ([Link](https://github.com/NousResearch/hermes-agent/issues/42248))
   - Open since June 8 (30 days). No fix PR identified. Blocks users running local models with Kanban.

3. **#45454 — Gateway crashes with SystemExit: 75 on macOS** ([Link](https://github.com/NousResearch/hermes-agent/issues/45454))
   - Open since June 13 (25 days). No maintainer response. Affects Telegram polling on Apple Silicon.

4. **#3335 — Zulip integration PR** ([Link](https://github.com/NousResearch/hermes-agent/pull/3335))
   - Open since March 27 (103 days). Still receiving updates but lacks final review/merge. Significant feature addition stalled.

5. **#60572 — Dashboard spawns MCP processes unnecessarily** ([Link](https://github.com/NousResearch/hermes-agent/issues/60572))
   - Open since yesterday but PR #60602 already submitted — good turnaround.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-08

Generated from sipeed/picoclaw GitHub data (updated in last 24h: 7 issues, 4 PRs, 0 releases)

---

## 1. Today's Overview

Project activity remains moderate, with 7 issues and 4 PRs updated in the last 24 hours. A new critical bug (#3232) was opened today regarding rate limiting failures when no fallback models are configured, affecting all users relying on single-model setups. Two feature PRs are advancing—an experimental Android ADB tool just merged, and a major DeltaChat refactor (−320 LOC) is under review. The backlog shows 5 stale open issues (2+ weeks without response) and several duplicate reports around Codex/Antigravity OAuth login failures, suggesting potential maintainer bandwidth constraints. No new releases were published today.

---

## 2. Releases

**No new releases today.** Latest stable remains v0.3.1 (implied by Issue #3232 reporter). No release notes, changelogs, or migration guides to report.

---

## 3. Project Progress

### Merged/Closed PRs (1):
- **#3157 [CLOSED] feat: add Android ADB remote operations tool**  
  Author: danmobot | Updated: 2026-07-07  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3157)  
  ✅ **Significant new capability.** Adds an experimental Android ADB-backed tool providing primitives for device listing, status inspection, screenshots, UI hierarchy summaries, tap, swipe, text input, key events, and wake. Does *not* expose arbitrary shell execution—a safety-conscious design.

### Open Under Review (3):
- **#3222 [OPEN] refactor(deltachat): cleanup implementation, documentation -320LOC**  
  Author: trufae | Updated: 2026-07-07  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3222)  
  Large cleanup: drops legacy features, removes fallbacks and outdated tests, replaces hardcoded relay list with official website reference, removes password-based email config, renames `invite_link` → `join_invite_link`, adds `show_invite_link`, and adds a full deltachat section. **Key architectural improvement.**

- **#3226 [OPEN] fix(tools): stop write_file from coaching destructive overwrite (#3150)**  
  Author: ACMYuechen | Updated: 2026-07-07  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3226)  
  Addresses behavioral bug where `write_file` guided agents toward destructive file replacement (e.g., overwriting `memory/MEMORY.md`). Now aims to prevent accidental data loss.

- **#3233 [OPEN] Fix pr 3222 backward compat**  
  Author: yaotukeji | Updated: 2026-07-07  
  [GitHub](https://github.com/sipeed/picoclaw/pull/3233)  
  Likely a companion fix to ensure PR #3222 does not break existing configurations.

---

## 4. Community Hot Topics

### Most Active Issues:
1. **#3093 — “I need SimpleX or tox”**  
   Author: Damian-o2 | Comments: 5 | 👍: 1 | [CLOSED]  
   [GitHub](https://github.com/sipeed/picoclaw/issues/3093)  
   User requesting SimpleX, Wire, or Tox gateway support. Closed as stale. Underlying need: desire for decentralized/encrypted messaging integration beyond current protocols.

2. **#3153 — “Volcengine Doubao Seed tool calls occasionally leak as <seed:tool_call> text”**  
   Author: ms8great | Comments: 3 | 👍: 0  
   [GitHub](https://github.com/sipeed/picoclaw/issues/3153)  
   **Reliability issue.** With `doubao-seed-2.0-pro`, tool calls sometimes appear as raw XML in user output instead of being executed. Remains open and stale.

3. **#3195 — “OpenAI GPT does not work on NanoKVM with default config”**  
   Author: rtadams89 | Comments: 2  
   [GitHub](https://github.com/sipeed/picoclaw/issues/3195)  
   New NanoKVM 2.4.0 integration fails with default GPT configuration. User followed official docs but all interactions return errors.

### Unusual Pattern:
Issues #3196 and #3197 (both by nyawitniorang) are **identical in title and content**—both report “Codex and antygravity oauth login not working.” Likely a duplicate submission, but suggests a real authentication blocker for those services.

---

## 5. Bugs & Stability

### Critical — Active, No Fix PR Yet:
- **#3232 [BUG] Rate limiting doesn't work if no fallback models is configured**  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3232)  
  🔴 **Highest severity.** User reports RPM config has no effect when only `agents.defaults.model_name` is set (no fallback). Affects all single-model deployments (v0.3.1). No comments or fix PR yet.

### Medium — Open, Stale:
- **#3153 — Tool call leakage with Volcengine Doubao Seed**  
  See above. Stale for 2 weeks despite being a functional bug.

### Medium — Open, Recent:
- **#3195 — OpenAI GPT fails on NanoKVM with default config**  
  See above. Could be a config or hardware compatibility issue.

### Low — Closed/Stale:
- **#3159 — “经常重复任务” (Frequent task repetition)**  
  [GitHub](https://github.com/sipeed/picoclaw/issues/3159)  
  Closed as stale. User reported that AI repeats previous tasks (e.g., asking for US news, then French news results in US news being re-executed). Root cause unclear.

### Non-Bug Duplicate:
- **#3196, #3197 — Codex/Antigravity OAuth login failure**  
  Duplicate reports; suggests a systematic auth integration problem.

---

## 6. Feature Requests & Roadmap Signals

### Signals for Next Release:
1. **Android ADB tool (PR #3157)** — Just merged. Will likely ship in next release (v0.3.2?). Opens the door for physical device automation.
2. **DeltaChat refactor (PR #3222)** — Under review. Would modernize and simplify DeltaChat integration, dropping legacy patterns. High chance of inclusion.
3. **Write_file safety guard (PR #3226)** — Behavioral improvement. Likely to be merged soon given the clear UX benefit.

### User-Requested Features (not yet acted on):
- **Decentralized messaging gateways** (Issue #3093): SimpleX, Tox, Wire. Closed as stale but may resurface.
- **OAuth login fixes for Codex/Antigravity** (Issues #3196, #3197): Explicit demand for third-party auth reliability.

### Predicted Next Version (v0.3.2 or v0.4.0):
- ADB tool (merged)
- Write_file overwrite guard (open, likely to merge)
- Rate limiting fix (critical, currently no PR)
- Possibly DeltaChat refactor if review completes quickly

---

## 7. User Feedback Summary

### Pain Points:
1. **Rate limiting silently broken** with single-model setups (#3232) — undermines core reliability.
2. **NanoKVM integration failure** (#3195) — new feature not working out of the box; hurts early adoption.
3. **Tool call leakage** with Volcengine (#3153) — confusing, unreliable UX.
4. **OAuth login failures** for Codex/Antigravity (#3196, #3197) — blocks access to specific AI services.
5. **Task repetition** (#3159) — agent behavior anomalies waste user time.

### Satisfaction Signals:
- Active development on ADB tool (merged) shows expansion into physical device control.
- DeltaChat refactor indicates ongoing maintenance investment.
- write_file fix shows responsiveness to behavioral safety concerns.

### Overall Sentiment:
Mixed. Users are encountering functional regressions in production (rate limiting, tool call leaks), but the project continues to add meaningful features. The stale backlog (5+ open issues untouched for 2+ weeks) suggests maintainer resources are stretched.

---

## 8. Backlog Watch

### Issues Requiring Maintainer Attention (All Stale >7 Days):

| Issue | Age | Priority | Reason |
|-------|-----|----------|--------|
| #3153 🔴 | 2 weeks | Medium | Tool call leak in production; open, no fix |
| #3195 🟡 | 1 week | Medium | New NanoKVM feature broken; first-time user blocker |
| #3196 🟡 | 1 week | Medium | OAuth login failure; duplicate reports |
| #3197 🟡 | 1 week | Medium | Same as #3196; needs deduplication & triage |
| #3159 🟢 | 2 weeks | Low | Closed as stale; may warrant re-examination if still reproducible |

### PRs Awaiting Review:
- **#3222** (DeltaChat refactor) — no comments from maintainers in 4 days
- **#3226** (write_file fix) — no comments in 3 days
- **#3233** (backward compat fix for #3222) — just opened today, no review yet

**Recommendation:** Prioritize triage on #3232 (critical rate limiting bug dropped today), review/write_file and DeltaChat refactor PRs, and either close or assign owners to stale issues #3153 and #3195 to reduce backlog bloat. The duplicate OAuth issues should be merged into a single canonical report.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-08

---

## 1. Today's Overview

NanoClaw experienced a **high-activity day** with 24 pull requests touched in the last 24 hours (9 merged/closed, 15 still open) and 1 new security vulnerability issue filed. The project is in a **documentation and stability consolidation phase**: a coordinated sweep of stale docs was merged across four PRs (architecture, DB schema, SDK deep-dive, and README/CONTRIBUTING corrections). Critical security fixes for path-traversal (`CWE-22`) and race-condition approval claiming are under active review. No new releases were published. The community submitted two new utility and operational skills (ncc CLI, add-rtk RTK mount fix) and one large Teams integration skill rebuild.

---

## 2. Releases

**None.** No new versions were cut in the last 24 hours. The most recent tagged release is `v2.1.38` (referenced in the documentation sweep PRs as the base commit).

---

## 3. Project Progress

**9 PRs were merged/closed today**, reflecting meaningful forward motion:

**Documentation Overhaul (4 PRs merged):**
- **#2961** — Stale claims fixed across README, CONTRIBUTING, CLAUDE.md, and operational docs (removed `/add-signal` and `/add-matrix` from solicited skills list)
- **#2962** — DB schema and entity docs synced with migrations 010–018 (entity definitions, foreign keys, column types)
- **#2963** — `architecture.md` and `agent-runner-details.md` rewritten to match current code; key fixes include schema container names, mount types, and polling mechanics
- **#2964** — SDK deep-dive doc updated from SDK `0.2.x` to `0.3.197` (~6700-line `sdk.d.ts`)

**Bug Fixes/Infrastructure (3 PRs merged):**
- **#2804** — Fixed `ncl messaging-groups create` which always threw `NOT NULL constraint failed: messaging_groups.instance` (CLI create path was completely dead)
- **#2965** — Fixed rate-limit event matching in `ClaudeProvider.translateEvents`; SDK `0.3.x` ships rate limits as top-level `SDKRateLimitEvent` instead of nested under `system` type
- **#2922** — Discord forwarded-message snapshots now unwrapped so agents see actual forwarded content

**Test/Process (1 PR):**
- **#2919** — Large-scale test PR (PR-Test2-LargePRTest, merged as test artifact)

**Skill Fix (1 PR):**
- **#2873** — Split pre-flight checks from credentials in skill refresh path, allowing `/update-skills` to re-fetch skill code without affecting credential validity

---

## 4. Community Hot Topics

**Most Active Issue:**
- **#2970** — [Security] Local action forgery via unauthenticated forwarded gateway loopback webhook  
  *Filed 2026-07-07, 0 comments, 0 reactions*  
  **Analysis:** This is a **critical security disclosure** describing an unauthenticated localhost webhook that accepts forwarded gateway events. The webhook does not authenticate the sender before trusting payloads. Despite zero comments, this is the **only open issue** and represents a significant attack surface. The community has not yet engaged in discussion.

**Most Active PRs by Age/Scope (high-priority attention):**
- **#2974** (open) — `fix(approvals): claim pending approvals before running the handler`  
  Adds atomic compare-and-set row claiming to prevent race conditions in approval flows. Filed yesterday.
- **#2800** (open, 3 weeks old) — `fix(security): validate folder + restrict --image-tag in ncl groups create/update`  
  Addresses CWE-22 path traversal (`--folder ../../etc` bypasses `GROUPS_DIR` validator) and unconstrained image tags. **Longest-standing security fix PR.**
- **#2973** (open) — `fix(supply-chain): activate the minimumReleaseAge gate`  
  Fixes `minimumReleaseAge` being placed under a `pnpm:` key where pnpm ignores it; moves to top level in workspace config.
- **#1598** (open, **3 months old**) — `feat: add-remote-storage skill (WebDAV/S3 via rclone + systemd)`  
  Long-standing feature skill adding remote storage mounts and `ncl groups config add-mount/remove-mount`. Has not been merged but continues to be updated.

---

## 5. Bugs & Stability

**Critical Severity:**

1. **Local action forgery (#2970)** — Unauthenticated localhost webhook for forwarded gateway events. An attacker who can reach `localhost` can forge gateway interaction events. **No fix PR yet.** This is the highest-priority vulnerability on the tracker.

2. **Path traversal in `ncl groups create/update` (#2800)** — The `--folder` argument bypasses `assertValidGroupFolder` validator when using the generic resource create path (`genericCreate` does raw INSERT). Fixed in open PR #2800 (not yet merged). **Potentially exploitable for file system access.**

3. **Approval race condition (#2974)** — Multiple handlers can approve the same pending approval record simultaneously because the row is not claimed before handler execution. Open fix PR #2974 adds `claimPendingApproval()` with atomic compare-and-set delete.

**Medium Severity:**

4. **CLI `messaging-groups create` dead (#2804)** — The CLI create path was completely broken (`NOT NULL constraint failed` on `instance` column). **Already fixed** and merged as PR #2804.

5. **Discord forwarded messages invisible to agents (#2922)** — Forwarded-message snapshots were not unwrapped, so agents never saw forwarded content. **Already fixed** and merged as PR #2922.

**Low Severity:**

6. **Rate-limit events not detected (#2965)** — SDK version bump from 0.2.x to 0.3.x changed the event structure; rate limits were not being parsed. **Already fixed** and merged as PR #2965.

---

## 6. Feature Requests & Roadmap Signals

**Near-term flagship features with active PRs:**

1. **Agent Templates (PR #2909)** — Part 2 of the template system: setup wizard now asks "How should we create your first agent?" offering Fresh agent or Template selection, with first-agent stamping from templates. **Very likely to merge next release.**

2. **Teams-CLI-first credentials (PR #2958)** — Complete rebuild of the `add-teams` skill using structured-skill-format (SSF). Replaces the 7-step Azure portal walk with `teams login` + `teams app create --json`. Also updates the setup wizard to use this single authentication path. **High priority—directly impacts enterprise onboarding experience.**

3. **Wizard UX improvements + Slack Socket Mode fixes (PR #2972)** — Adds pairing cards, either/or selects, step-children silence, async `hostExec` for spinner animation, and restores bot-event subscription for Slack Socket Mode. **Polishing the setup flow—likely to merge alongside #2909.**

**New Skills (waiting review):**
- **#2971** — `ncc` utility skill: host operational and health CLI (standalone tool, no source changes)
- **#2969** — Fix for `add-rtk` mount rejected on v2: relative `containerPath` + `PATH` configuration
- **#1598** — Remote storage mount skill (WebDAV/S3 via rclone + systemd) — **3 months open**, may need maintainer decision

---

## 7. User Feedback Summary

**Pain Points (inferred from PRs):**

- **Setup wizard friction** — Multiple PRs (#2909, #2972, #2958) all touch the setup flow, suggesting users found the initial agent creation confusing, the pairing status blocks mislabeled, and the Teams credential flow overly complex.
- **Broken CLI commands** — The discovery that `ncl messaging-groups create` always throws `NOT NULL` (PR #2804) indicates users could not create messaging groups via CLI at all. This was **fixed today**.
- **Documentation staleness** — The coordinated documentation sweep (4 PRs merged today) suggests users were confused by outdated architecture diagrams, incorrect column names, and stale SDK references.

**Satisfaction Signals:**
- **Active skill contributions** — Two new skills (ncc utility, add-rtk fix) submitted by community members demonstrate continued contributor engagement.
- **Large PRs from first-time contributors** — PR #2922 from `OowhitecatoO` (Discord fix) and PR #2873 from `glifocat` (skill refresh) show a healthy contributor pipeline.

---

## 8. Backlog Watch

**Critical Security Issue Needing Attention:**
- **#2970** — Local action forgery via unauthenticated webhook (filed today, no discussion yet, needs triage and fix)

**Longest-Overdue PRs:**
- **#1598** (3 months open) — `add-remote-storage skill` (WebDAV/S3 via rclone). Updated as recently as yesterday (2026-07-07) but has not received maintainer review in weeks. Needs a decision to merge, request changes, or close.

**Security Fix Awaiting Merge:**
- **#2800** (3 weeks open) — `fix(security): validate folder + restrict --image-tag`. This is a CWE-22 path traversal fix with a complete implementation. No comments from maintainers since mid-June. Should be prioritized alongside #2970.

**Documentation PR with Maintenance Risk:**
- **#2729** (nearly 1 month open) — `docs(add-telegram): match pairing status-block names to the setup step; fix adapter pin`. Updated 2026-07-07 but no maintainer engagement. The documentation guide itself is being actively reworked (PR #2961), so this may conflict.

**Metrics at a Glance:**
| Metric | Value |
|---|---|
| Open issues (active) | 1 (security critical) |
| Open PRs | 15 |
| Longest open PR | #1598 — 97 days |
| PRs merged/closed today | 9 |
| Skills submitted today | 3 (ncc utility, add-rtk fix, add-teams rebuild) |

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-08

## Today's Overview

IronClaw saw moderate activity over the past 24 hours with 31 issues updated (22 open, 9 closed) and 50 pull requests updated (42 open, 8 merged/closed). No new releases were published. The project remains in active development, with significant work flowing through the Reborn stack — particularly around tool installation, user management, and prompt-context infrastructure. A notable daily failure taxonomy report ([#5788](https://github.com/nearai/ironclaw/issues/5788)) was filed, flagging persistent integration test failures that will require maintainer attention. Overall project health is stable, though the bug bash backlog (P2/P3 items) continues to accumulate alongside the core engineering velocity.

## Releases

No new releases were published in the last 24 hours.

## Project Progress

Eight PRs were merged or closed today, reflecting steady forward motion:

- **[#5694](https://github.com/nearai/ironclaw/pull/5694) [CLOSED]** — Fixed `clientActionId()` throwing on insecure origins (HTTP), which was breaking all mutating requests in self-hosted deployments. *(bug_bash_P2)*
- **[#5698](https://github.com/nearai/ironclaw/pull/5698) [CLOSED]** — Surface tool permission save failures in WebUI v2 Settings Tools tab, exposing silent mutation errors to users. *(bug_bash_P3)*
- **[#5696](https://github.com/nearai/ironclaw/pull/5696) [CLOSED]** — Hid unsupported operator-config fields (Embeddings, Temperature) from WebUI v2 Inference settings to prevent invalid POST requests. *(bug_bash_P2)*
- **[#5554](https://github.com/nearai/ironclaw/pull/5554) [CLOSED]** — Fixed mobile chat layout horizontal overflow issue. *(bug_bash_P2)*
- **[#5572](https://github.com/nearai/ironclaw/pull/5572) [CLOSED]** — Fixed `HookedLoopCheckpointPort` not forwarding `stage_checkpoint_payload`/`load_checkpoint_payload`, which was causing hooks-enabled coordinator turns to fail at the Checkpoint stage.
- **[#5466](https://github.com/nearai/ironclaw/pull/5466) [CLOSED]** — Fixed parallel same-tenant turn-runs CAS race condition against `FilesystemTurnStateStore`/libsql backend (~10% failure rate).
- **[#5467](https://github.com/nearai/ironclaw/pull/5467) [CLOSED]** — Fixed in-memory `ApprovalRequestStore::discard_pending` diverging from filesystem implementation (missing tombstone → id reuse allowed).
- **[#3083](https://github.com/nearai/ironclaw/pull/3083) [CLOSED]** — Fixed duplicate user creation in User Management due to missing loading state and submission debounce. *(bug_bash_P2)*

Major open PRs advancing features include:
- **Trace Commons enrollment** ([#5280](https://github.com/nearai/ironclaw/pull/5280)) — instance-wide enrollment, per-user profiles, and trace inspection (XL, DB migration required)
- **Private installs of tools** ([#5525](https://github.com/nearai/ironclaw/pull/5525)) — SSO users can install tools privately without admin intervention
- **WASM tool install from zip** ([#5499](https://github.com/nearai/ironclaw/pull/5499)) — admin import and tenant-shared credentials foundation
- **Admin user-management API + UI** ([#5779](https://github.com/nearai/ironclaw/pull/5779)) — end-to-end surface through all five stack layers
- **LFD infrastructure** ([#5778](https://github.com/nearai/ironclaw/pull/5778)) — reusable infrastructure for feature-specific LFD packages
- **Composition god-crate refactor** — multiple dissection steps ([#5783](https://github.com/nearai/ironclaw/pull/5783), [#5785](https://github.com/nearai/ironclaw/pull/5785)) grouping Slack and extension-host modules

## Community Hot Topics

The most active discussions in the last 24 hours:

- **[#5702](https://github.com/nearai/ironclaw/issues/5702) — GitHub issue search and create fail with HTTP 403** (4 comments, bug_bash_P2): Agent's GitHub integration cannot search or create issues, returning `operation_failed` status despite configured integration. This is a high-impact workflow blocker for users relying on GitHub automation.

- **[#5747](https://github.com/nearai/ironclaw/issues/5747) — No way to unpair Slack on built-in host-beta mount** (2 comments): Users who pair Slack to IronClaw cannot disconnect — `/pair` refuses with "You're already connected" and the UI has no disconnect button. This creates a permanent binding with no escape hatch.

- **[#5704](https://github.com/nearai/ironclaw/issues/5704) — Image preview becomes transparent during active chat** (2 comments, bug_bash_P3): Image thumbnails lose opacity while the agent is processing, returning to normal only after completion. Cosmetic but visually disorienting.

- **[#5701](https://github.com/nearai/ironclaw/issues/5701) — Activity panel hides tool details during active run** (2 comments, bug_bash_P2): The activity panel collapses tool call details into "Activity - N tools" without showing what tools were called or returned. No real-time updates during active runs — users must wait for completion.

- **[#5788](https://github.com/nearai/ironclaw/issues/5788) — Daily failure taxonomy 2026-07-08** (new, 0 comments): This automated report flags that all 4 pinchbench integration tasks score 0, with the dominant cause being a persistent issue (detailed further in the Bugs section).

**Underlying needs**: Community members are expressing frustration with integration reliability (GitHub 403s, Slack pairing lock-in), UI feedback gaps (activity panel opacity, tool call visibility), and missing user control (no disconnect, no icon hiding). These point to a need for more robust error handling, user-facing configuration options, and real-time UI state management.

## Bugs & Stability

### Critical/P2 (High Impact)

1. **[#5702](https://github.com/nearai/ironclaw/issues/5702) — GitHub issue search/create HTTP 403** *(bug_bash_P2)*: Agent cannot perform GitHub issue operations despite configured integration. No known fix PR exists. **Severity: High** — blocks core workflow.

2. **[#5776](https://github.com/nearai/ironclaw/issues/5776) — Long-output prompt causes repeated model timeouts** *(bug_bash_P2)*: Extreme prompts cause NEAR AI completion calls to exceed timeout, then Reborn degrades into generic "invalid result" error. Agent does not break the prompt into smaller chunks. No fix PR identified.

3. **[#5553](https://github.com/nearai/ironclaw/issues/5553) — Approval notifications disappear** *(bug_bash_P2)*: Running automations requiring user approval do not reliably show notifications — may flash once or never appear. No fix PR identified.

4. **[#5701](https://github.com/nearai/ironclaw/issues/5701) — Activity panel hides tool details** *(bug_bash_P2)*: Panel collapses tool calls into summary line, no real-time updates. No fix PR identified.

5. **[#5708](https://github.com/nearai/ironclaw/issues/5708) — Error banners outside chat message stream** *(bug_bash_P2)*: Error banners render as floating elements detached from conversation, allowing stacking. No fix PR identified.

6. **[#5787](https://github.com/nearai/ironclaw/issues/5787) — Flaky slack pairing test** *(new)*: `slack_pairing_redeem_rejects_expired_code` intermittently fails in CI due to tokio paused clock vs chrono wall-clock TTL race. PR [#5789](https://github.com/nearai/ironclaw/pull/5789) is open to fix with deterministic clock injection.

7. **[#5788](https://github.com/nearai/ironclaw/issues/5788) — Daily failure taxonomy** *(new)*: All 4 pinchbench integration tasks score 0. Dominant cause is a "persistent issue requiring investigation." This is an automated alert demanding maintainer attention.

### Cosmetic/P3 (Low Impact)

- **[#5704](https://github.com/nearai/ironclaw/issues/5704) — Image preview transparent during active chat** *(P3)*
- **[#5705](https://github.com/nearai/ironclaw/issues/5705) — Terminal icon no disable option** *(P3)*
- **[#5706](https://github.com/nearai/ironclaw/issues/5706) — Sidebar shows raw thread ID under load** *(P3)*
- **[#5557](https://github.com/nearai/ironclaw/issues/5557) — Logs deep link requires two clicks** *(P3)*
- **[#5419](https://github.com/nearai/ironclaw/issues/5419) — No option to rename automations** *(P3)*

### Closed Bug Fixes (Today)
- [#5694](https://github.com/nearai/ironclaw/pull/5694) — `clientActionId()` on insecure origins (P2, fix merged)
- [#5696](https://github.com/nearai/ironclaw/pull/5696) — Unsupported operator-config fields (P2, fix merged)
- [#5554](https://github.com/nearai/ironclaw/pull/5554) — Mobile chat overflow (P2, fix merged)
- [#5466](https://github.com/nearai/ironclaw/pull/5466) — Parallel turn-run CAS race (fix merged)
- [#5467](https://github.com/nearai/ironclaw/pull/5467) — In-memory approval store tombstone divergence (fix merged)
- [#5572](https://github.com/nearai/ironclaw/pull/5572) — Checkpoint port forwarding failure (fix merged)

## Feature Requests & Roadmap Signals

Several feature requests and improvement signals emerged today:

1. **[#5786](https://github.com/nearai/ironclaw/issues/5786) — Expose OpenRouter upstream provider** *(new)*: Request to expose the `provider` field returned by OpenRouter (naming the upstream model host) in `ToolCompletionResponse`. This enables users to see which provider actually served their request when using OpenRouter routing.

2. **[#5770](https://github.com/nearai/ironclaw/issues/5770) — Custom dropdown for tool permissions** *(new)*: Replace browser-native `<select>` in Reborn Settings > Tools with a custom dropdown that matches the WebUI v2 design system, especially in dark mode.

3. **[#5768](https://github.com/nearai/ironclaw/issues/5768) — Reborn Projects page i18n coverage** *(new)*: Several visible UI strings on the Projects page remain hardcoded in English when the interface is set to Chinese. Request to complete localization coverage.

4. **[#5762](https://github.com/nearai/ironclaw/issues/5762) — Row-store materializer throughput recovery** *(new, performance)*: After the materializer starvation fix, throughput is still below the earlier high-water mark. Request to optimize row-store materialization without weakening the correctness fix.

5. **[#5419](https://github.com/nearai/ironclaw/issues/5419) — Automation rename** *(bug_bash_P3, open since June 29)*: Users cannot edit auto-generated automation names that are too long or unclear. Simple quality-of-life feature.

6. **[#3081](https://github.com/nearai/ironclaw/issues/3081) — Portfolio extension misleading "Configure" button** *(bug_bash_P2, open since April 29)*: Shows a "Configure" action for Portfolio tool when no configuration is needed. UI misdirection that has been open for over 2 months.

**Prediction for next version**: The tool installation stack ([#5499](https://github.com/nearai/ironclaw/pull/5499), [#5525](https://github.com/nearai/ironclaw/pull/5525)) and admin user management ([#5779](https://github.com/nearai/ironclaw/pull/5779)) are near-term candidates for merging, along with the composition refactor steps. The Trace Commons enrollment ([#5280](https://github.com/nearai/ironclaw/pull/5280)) is XL with a DB migration, likely targeting the release after next.

## User Feedback Summary

**Pain points expressed today:**

- **GitHub integration broken (HTTP 403)** ([#5702](https://github.com/nearai/ironclaw/issues/5702)): Users cannot search or create GitHub issues despite having the integration configured — a core workflow failure with no workaround.

- **Slack pairing lock-in** ([#5747](https://github.com/nearai/ironclaw/issues/5747)): Once paired, users are permanently bound to a Slack identity with no disconnect mechanism. The `/pair` command is a dead end and the UI has no unpair option.

- **Missing real-time feedback** ([#5701](https://github.com/nearai/ironclaw/issues/5701)): The activity panel provides no visibility into ongoing tool calls, forcing users to wait blindly for completion.

- **Error messages out of context** ([#5708](https://github.com/nearai/ironclaw/issues/5708)): Errors like "out of credits" appear as floating banners detached from the relevant chat message, making troubleshooting harder.

- **Approval notifications unreliable** ([#5553](https://github.com/nearai/ironclaw/issues/5553)): Automation approval requests may flash once or never appear, which undermines trust in the automation system.

**Satisfaction signals**: The steady cadence of PR merges (8 today, including 4 P2 bug fixes) shows responsiveness to the bug bash program. The composition refactor and infrastructure work (LFD, Trace Commons) indicate continued investment in platform scalability.

## Backlog Watch

Several important issues remain open with no recent maintainer activity:

- **[#3535](https://github.com/nearai/ironclaw/issues/3535) — UI Timestamps incorrect for conversations** *(bug_bash_P1, opened May 12, 2026)*: Conversations show incorrect timestamps. Despite P1 severity and 57 days open, no fix PR has been filed. Users cannot trust conversation chronology.

- **[#4338](https://github.com/nearai/ironclaw/issues/4338) — Disconnected state shows misleading execution driver error** *(bug_bash_P2, opened June 2, 2026)*: When connection drops during agent execution, users see a confusing "MiniMax-M2.7" driver error instead of a clear disconnection message.

- **[#4108](https://github.com/nearai/ironclaw/issues/4108) — Nightly E2E failed** *(opened May 27, 2026)*: Automated nightly E2E test suite is persistently failing. This has been open for 42 days across multiple attempts — suggests a chronic stability issue in the E2E pipeline.

- **[#3081](https://github.com/nearai/ironclaw/issues/3081) — Portfolio extension "Configure" button misleading** *(bug_bash_P2, opened April 29, 2026)*: 70 days open with no fix. Minor but confusing UI element.

- **[#5419](https://github.com/nearai/ironclaw/issues/5419) — No option to rename automations** *(bug_bash_P3, opened June 29, 2026)*: 9 days open. Simple feature request that may be quick to address.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the project digest for **LobsterAI** on **2026-07-08**.

---

## LobsterAI Project Digest – 2026-07-08

### 1. Today's Overview
Project activity is high, driven by a major release (`2026.7.7`) and a surge in security reports. In the last 24 hours, **16 Pull Requests** were updated, with an exceptional **14 merged/closed**, alongside **5 closed Issues**. A new version was cut, focusing on UI redesigns for scheduled tasks and new provider OAuth support. However, a **significant cluster of 3 critical security vulnerabilities** was opened today regarding local file disclosure and token proxy authentication, indicating a new security audit is underway. The community is also actively discussing a configuration bug affecting multi-agent workflows.

### 2. Releases
- **New Version:** `LobsterAI 2026.7.7`
- **Release Date:** 2026-07-07
- **Key Changes:**
  - **Feat (Scheduled Tasks):** Task list card has been redesigned with status chips, toggles, search functionality, and optimistic UI feedback for the renderer.
  - **Feat (Providers):** Added **xAI (Grok) OAuth login** support.
- **Migration Notes:** No specific breaking changes or migration steps were mentioned in the release notes.

### 3. Project Progress
The project completed **14 PRs** (merged/closed) today, with major work in several feature areas:

- **Cowork (Collaboration):** Significant stabilization work was merged:
  - **#2292:** Fix for steer follow-up routing to prevent stale input state.
  - **#2289:** Fix for clearing stalled compaction retry maintenance.
- **Email Skill:** **#2275** added multi-account support for the built-in IMAP/SMTP email skill, including account management UI and legacy config compatibility.
- **Analytics:** **#2245** fixed several edge cases in usage event reporting for skills, settings toggles, and scheduled tasks.
- **Scheduled Tasks:** **#2290** added the ability to make the notify target user-selectable.
- **Stale Bug Fixes (Merged Today):** A batch of technical debt and old bugs were closed, including fixes for:
  - OpenClaw Token Proxy memory limits (**#1407**).
  - MCP Bridge Server async error handling (**#1408**).
  - SQLite synchronous disk write performance (**#1410**).
  - NIM group type enum mapping (**#1419**).
  - Cron job concurrency/ghost events (**#1420**).

### 4. Community Hot Topics
- **User Memory Synchronization (Issue #2293):** This newly opened issue is the most active, with the author reporting that modifying the "About You" profile or `USER.md` in one Agent synchronizes changes across all other Agents.
  - **Analysis:** This reveals a user expectation for **isolated per-agent identities**. Currently, the system treats user profiles as a global resource, which is a pain point for users managing distinct personas (e.g., a "Work" agent vs. a "Personal" agent).
  - **Link:** [Issue #2293](https://github.com/netease-youdao/LobsterAI/issues/2293)

### 5. Bugs & Stability
Three **high-severity security vulnerabilities** were reported today, all by the same researcher (YLChen-007). No fix PRs exist yet.

- **Critical: Local File Disclosure via Symlinks (Issue #2288):** The HTML preview server follows in-root symlinks, allowing an attacker to read arbitrary local files outside the designated preview directory.
  - **Link:** [Issue #2288](https://github.com/netease-youdao/LobsterAI/issues/2288)
- **Critical: Local File Exfiltration via Assistant (Issue #2287):** The NIM integration treats assistant-generated absolute file paths as outbound media, allowing a malicious remote AI assistant to exfiltrate files from the host machine.
  - **Link:** [Issue #2287](https://github.com/netease-youdao/LobsterAI/issues/2287)
- **Critical: Unauthenticated Token Proxy (Issue #2286):** The `lobsterai-server` provider starts an unauthenticated HTTP token proxy, allowing any local process to steal and replay the user's server API tokens.
  - **Link:** [Issue #2286](https://github.com/netease-youdao/LobsterAI/issues/2286)

### 6. Feature Requests & Roadmap Signals
- **Delegated Subagent Collaboration (PR #2285):** An open PR introduces the ability for users to configure which Agents can be delegated to, creating child Cowork sessions. This directly addresses the need for complex, multi-agent workflows.
  - **Prediction:** Given this is an open PR with significant feature scope (including allowlists and session state), it is **likely to be a core feature of the next minor release**, following the `2026.7.7` stability release.
  - **Link:** [PR #2285](https://github.com/netease-youdao/LobsterAI/pull/2285)

### 7. User Feedback Summary
- **Pain Points:**
  - **Multi-Agent Identity Isolation:** Users want Agent-specific identities (USER.md) but find them globally synced (Issue #2293).
  - **UI Layout in English:** A user reported that after switching to English, the "Usage Overview" text and numbers overlap (Issue #1416).
  - **Inaccurate Statistics:** Multiple dashboard bugs (sessions showing 0, filter not working) were reported recently, though many have been fixed (Issues #1411, #1414).
- **Workarounds & Use Cases:**
  - The new **Email Skill (PR #2275)** suggests users are demanding fully-integrated personal assistant capabilities (email management).
  - The **xAI OAuth (Release v2026.7.7)** support indicates a user base wanting access to the Grok model.

### 8. Backlog Watch
- **Dependency Update (PR #1277):** This PR, which bumps `electron` from v40 to v43 and `electron-builder`, has been open since **April 2, 2026**, and is now over **3 months old**. While security fixes are likely included in the electron upgrade, the long delay could be due to breaking changes in the new Electron version.
  - **Link:** [PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

# TinyAGI Project Digest — 2026-07-08

## Today's Overview

The TinyAGI project experienced a concentrated security review on 2026-07-07, with **9 new security-focused issues opened**, all still open with no corresponding PRs or releases yet. There were **no merged PRs, no releases, and no code changes** in the last 24 hours, indicating a day dedicated to vulnerability disclosure rather than active development. The project is currently in a **critical security assessment phase**, with all 9 issues filed by the same author (YLChen-007) targeting unauthenticated control-plane exposure, path traversal, and terminal injection vectors. The absence of any closed PRs or fixes suggests the project maintainers have not yet responded to these disclosures.

## Releases

**No new releases** in the last 24 hours. The latest release remains unknown (no data provided beyond "None").

## Project Progress

**No pull requests were merged or closed** in the last 24 hours. No feature development or bugfix activity was recorded.

## Community Hot Topics

All 9 open issues are equally active (0 comments, 0 reactions each), all filed by **YLChen-007** on 2026-07-07. These represent a coordinated security audit rather than community discussion:

- **#286** — [Security] Unauthenticated Local Control API Allows Persistent Settings Mutation, Agent Prompt Overwrite, and Event Stream Access  
  [Link](https://github.com/TinyAGI/tinyagi/issues/286)
- **#287** — [Security] Unauthenticated Pairing Management API Allows Arbitrary Approval of Pending Channel Senders  
  [Link](https://github.com/TinyAGI/tinyagi/issues/287)
- **#288** — [Security] Unauthenticated local control plane leaks live events and allows persistent settings modification  
  [Link](https://github.com/TinyAGI/tinyagi/issues/288)
- **#289** — [Security] Unauthenticated API callers can exfiltrate arbitrary local files via outbound channel attachments  
  [Link](https://github.com/TinyAGI/tinyagi/issues/289)
- **#290** — [Security] Terminal Escape Injection via `POST /api/message` Allows Operator Log Spoofing  
  [Link](https://github.com/TinyAGI/tinyagi/issues/290)
- **#291** — [Security] Anthropic Adapter Disables Claude Dangerous-Tool Confirmation for Unauthenticated Requests  
  [Link](https://github.com/TinyAGI/tinyagi/issues/291)
- **#292** — [Security] Unauthenticated administrative API allows persistent settings and agent prompt modification  
  [Link](https://github.com/TinyAGI/tinyagi/issues/292)
- **#293** — [Security] Unauthenticated agent ID path traversal escapes configured workspace root  
  [Link](https://github.com/TinyAGI/tinyagi/issues/293)
- **#294** — [Security] Unauthenticated control-plane routes allow system prompt overwrite and daemon restart  
  [Link](https://github.com/TinyAGI/tinyagi/issues/294)

**Underlying need**: The collective disclosure suggests a **systemic failure in API authorization design** — the project lacks authentication across its control-plane, pairing, and message endpoints, exposing operators to remote code execution, data exfiltration, and privilege escalation.

## Bugs & Stability

All 9 issues are **critical-severity security vulnerabilities**, ranked by exploit potential:

1. **Critical — Remote Code Execution / Privilege Escalation** (Issues #286, #287, #288, #294): Unauthenticated control-plane APIs allow arbitrary settings mutation, agent prompt overwrite, daemon restart, and event stream access. These are the most severe as they provide attacker control over the service.

2. **Critical — Data Exfiltration** (Issue #289): Unauthenticated callers can submit arbitrary local file paths in `files[]` to exfiltrate data via outbound channel attachments — direct data breach vector.

3. **Critical — Path Traversal** (Issue #293): Agent ID `..` allows escape from configured workspace root, enabling arbitrary file access on the host.

4. **High — Supply Chain / LLM Abuse** (Issue #291): Anthropic adapter unconditionally passes `--dangerously-skip-permissions`, disabling Claude's dangerous-tool confirmation for all unauthenticated message requests.

5. **High — Log Injection** (Issue #290): Terminal escape injection via `POST /api/message` allows log spoofing and potential terminal command injection.

**No fix PRs exist** for any of these issues as of this digest.

## Feature Requests & Roadmap Signals

No feature requests were filed in the last 24 hours. The sole signal is a **systemic security hardening requirement** — any next release will likely need to address the complete lack of API authentication and input validation before new features can be safely prioritized.

## User Feedback Summary

No user feedback (comments, reactions, or feature requests) was recorded. The security disclosures appear to come from an external security researcher, not a regular user reporting pain points. The **primary user risk signal** is that anyone running TinyAGI with exposed endpoints is vulnerable to complete service compromise.

## Backlog Watch

**All 9 issues are urgent and require immediate maintainer attention**, ranked by severity:

| Issue | Summary | Days Open | Risk |
|-------|---------|-----------|------|
| [#286](https://github.com/TinyAGI/tinyagi/issues/286) | Unauthenticated local control API | 1 | Critical |
| [#287](https://github.com/TinyAGI/tinyagi/issues/287) | Unauthenticated pairing approval | 1 | Critical |
| [#288](https://github.com/TinyAGI/tinyagi/issues/288) | Unauthenticated control plane leaks | 1 | Critical |
| [#289](https://github.com/TinyAGI/tinyagi/issues/289) | File exfiltration via attachments | 1 | Critical |
| [#290](https://github.com/TinyAGI/tinyagi/issues/290) | Terminal escape injection | 1 | High |
| [#291](https://github.com/TinyAGI/tinyagi/issues/291) | Anthropic dangerous-tool bypass | 1 | High |
| [#292](https://github.com/TinyAGI/tinyagi/issues/292) | Unauthenticated admin API | 1 | Critical |
| [#293](https://github.com/TinyAGI/tinyagi/issues/293) | Path traversal via agent ID | 1 | Critical |
| [#294](https://github.com/TinyAGI/tinyagi/issues/294) | Control-plane prompt overwrite | 1 | Critical |

**Recommendation**: Maintainers should prioritize reviewing these advisories and issuing a security patch (e.g., implementing API authentication, input sanitization, and removing `--dangerously-skip-permissions`) as an emergency hotfix before any feature development.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-08

## Today's Overview
CoPaw remains in an active pre-release cycle, with v2.0.0-beta.3 released today and **10 open bug reports** filed or updated in the last 24 hours. The project shows **high engineering velocity**: 38 pull requests updated, of which 15 were merged or closed, and 13 open issues are being actively triaged. The release pipeline is fully automated, with both beta (v2.0.0-beta.3) and stable patch (v1.1.12.post3) verification duties running concurrently. However, the number of **untriaged security-related bugs** (sandbox ACE pollution, file guard bypass) and **frontend stability issues** (large session crashes, large tool-use history rendering failures) suggest the pre-release quality bar needs tightening before GA.

## Releases
**v2.0.0-beta.3** was published today (type: Beta). Changes include:
- **CI fix**: Guard empty `extra_flags` expansion for bash 3.2 on macOS
- **Auth enhancement**: Multi-dimensional rate limiting with better protection against abuse
- No migration notes or breaking changes documented in the release notes.
- *Note*: The release commit message mentions `QwenPaw` but the release tag is under `CoPaw`/`agentscope-ai` — likely a branding/copying artifact.

## Project Progress
**Merged/Closed PRs today (15 total):**
- **feat(memory)**: Usage-aware auto search and backend-specific embeddings (#5820) — synthetic auto memory search accounting, memory query simplification centered on latest user intent
- **feat(plugin)**: Schema-driven config UI for plugin-registered custom channels (#4693) — replaces legacy `custom_channels/` directory mechanism
- **feat(channels)**: Matrix streaming mode (like Discord) (#5585) — reduces time-to-first-token perception in Matrix channel
- **fix**: Three-bug patch (#5786) — frontend agent config model matching by `provider_id`, memory compression rendering fix, and another stability fix
- **chore**: Version bump to 2.0.0b4 (#5837) — though `2.0.0-beta.3` was the release, the branch is already preparing for b4
- **release duty**: v1.1.12.post3 installation verification passed (#5819)

## Community Hot Topics
1. **[Issue #5401] Console crash with large tool-use history** (15 comments) — High-impact frontend bug: `DataContent` type mismatch between backend and frontend rendering. Backend emits `type: "data"` but frontend expects `type: "tool_use"`. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5401)*

2. **[Issue #5273] v2.0.0 Pre-release Bug Tracker** (10 comments, 1 👍) — Central tracking issue for all pre-release bugs. Currently the main triage hub for beta issues. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5273)*

3. **[Issue #5479] Large session file (>500KB) crash** (6 comments) — Another frontend crash: sessions >500KB cause unrecoverable rendering errors. User strongly requests progressive loading. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5479)*

4. **[Issue #5797] Scheduled task notification toggle** (4 comments) — Community divided: some users want toast notifications for scheduled tasks, some hate them. Current solution (PR #4803) disabled all toasts; user requests per-task opt-in toggle. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5797)*

5. **[PR #5836] Auto-detect local paths in Desktop chat** — User-facing feature: clickable file paths in chat output open system explorer. Closes #4830. *Link: [PR](https://github.com/agentscope-ai/CoPaw/pull/5836)*

*Analysis*: Most community energy is concentrated on **frontend stability** (2 of top 3 issues) and **user customization** (notification behavior, file path interaction). The pre-release tracker indicates active community beta testing.

## Bugs & Stability

### Critical Severity (active exploitation risk or data loss)
1. **[#5829] Windows AppContainer sandbox ACE pollution** — `icacls /grant` adds inheritable ACEs to `C:\`, `C:\Users` causing Hermes Desktop GPU process crash. System integrity issue. *No fix PR yet. Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5829)*

2. **[#5842] `find -delete` bypasses file deletion guard** — File guard only blocks `rm` but not `find ... -delete`, allowing out-of-workspace file deletion when `allow_preview_outside_workspace: true`. *Fix PR #5843 exists (detect `find -delete` as dangerous). Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5842)*

### High Severity (crash, incorrect behavior)
3. **[#5401] Console crash on large tool-use history** — Backend/frontend type mismatch. No fix PR yet. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5401)*

4. **[#5479] >500KB session crash** — Frontend fails to render large sessions. Progressive loading requested. *No fix PR yet. Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5479)*

5. **[#5789] Context compression crashes on JSON Schema maxLength violation** — Model output >200 char for `next_steps` field causes `jsonschema.validate()` failure, crashing compression. *No fix PR yet. Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5789)*

### Medium Severity
6. **[#5775] Auto-memory interval never triggers** — MemoryMiddleware state lost across per-request agent rebuilds; `auto_memory_interval > 1` non-functional. *Closed as fixed? (status: closed). Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5775)*

7. **[#5759] Plan mode reads same file repeatedly** — Same file read 5× in a single sub-task chain with no content changes. *No fix PR yet. Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5759)*

8. **[#5835] `/stop` lacks user-level isolation in DingTalk DM** — Users sharing same bot get identical session IDs, causing cross-user task cancellation. *No fix PR yet. Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5835)*

## Feature Requests & Roadmap Signals

### Likely for v2.0.0 GA or v2.0.1
1. **Scheduled task notification toggle** ([#5797](https://github.com/agentscope-ai/CoPaw/issues/5797)) — Per-task opt-in/out + configurable toast duration. PR #4803 already present but overly aggressive.

2. **Desktop close → system tray** ([#5312](https://github.com/agentscope-ai/CoPaw/issues/5312)) — 2 comments, likely low-effort Electron config change. Popular in desktop apps.

3. **Hidden folder selection in coding mode** ([#5785](https://github.com/agentscope-ai/CoPaw/issues/5785), closed) — Already resolved; user wanted dot-prefix folder visibility.

4. **Per-media-type `rejects_media` capability** ([#5821](https://github.com/agentscope-ai/CoPaw/issues/5821)) — Granular media rejection instead of all-or-nothing. Clear win for multi-modal workflows.

5. **Clickable local paths in Desktop chat** ([PR #5836](https://github.com/agentscope-ai/CoPaw/pull/5836)) — Already implemented, likely in next beta.

### Speculative / Longer-term
- **Qwen3-rerank in memory search** ([PR #5669](https://github.com/agentscope-ai/CoPaw/pull/5669)) — First-time contributor, under review. DashScope rerank integration for ReMe memory. Default off, toggle-based.

- **Windows desktop GUI automation** ([PR #5187](https://github.com/agentscope-ai/CoPaw/pull/5187)) — UIA + Tauri control mode for computer-use tool. Large, complex PR still open since June 14.

- **Bundled Node.js for ACP desktop** ([PR #5814](https://github.com/agentscope-ai/CoPaw/pull/5814)) — Bundle Node with Tauri desktop so ACP agents work without separate Node install.

## User Feedback Summary

### Pain Points (repeated themes)
- **Frontend stability is the #1 complaint**: Large sessions, large tool-use history, and large file handling all cause unrecoverable crashes. Users expect progressive loading.
- **One-size-fits-all UX decisions frustrate**: The toast notification debate (no toasts vs. some toasts) shows users want **per-task configurability**, not developer-chosen defaults.
- **Security footguns on Windows**: The sandbox ACE pollution is particularly alarming — it modifies system ACLs with inheritance, affecting non-QwenPaw applications.
- **File guard bypass is known and exploitable**: The `find -delete` bypass (#5842) is a concrete security gap that impacts workspace isolation promises.

### Positive Signals
- **First-time contributors are active**: 4 PRs today are labeled `first-time-contributor` (hehuang139, slashchenxiaojun, iluv7, hehuang139 again) — healthy community onboarding.
- **Automated release verification works**: Both beta.3 and post3 had dedicated release duty issues with clear pass/fail criteria.
- **grep_search improvements**: Two separate first-time-contributor PRs improving grep_search (pipe-separated literals, show_file option) — indicates active tooling pain being addressed.

## Backlog Watch

### High-priority issues needing maintainer response
- **[Issue #5829] Windows AppContainer ACE pollution** — **No maintainer comment since opened today.** This is a critical security/system integrity bug. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5829)*

- **[Issue #5842] `find -delete` bypass** — Has a fix PR (#5843) opened by same author, but no maintainer review yet. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5842)*

- **[Issue #5835] Cross-user `/stop` in DingTalk** — Opened today, no assignee. Regex conflict creates production issue in multi-tenant bot scenarios. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5835)*

### Long-unanswered issues (pre-release tracker)
- **[Issue #5273] v2.0.0 Pre-release Bug Tracker** — 10 comments, last updated yesterday. Should be updated with beta.3 known issues. *Link: [Issue](https://github.com/agentscope-ai/CoPaw/issues/5273)*

### Stale PRs needing attention
- **[PR #5187] Windows desktop GUI automation** — Open since June 14 (24 days), no maintainer review. Large feature, likely needs architectural sign-off. *Link: [PR](https://github.com/agentscope-ai/CoPaw/pull/5187)*

- **[PR #5669] Qwen3-rerank in memory search** — Open since June 30 (8 days), labeled "Under Review" but no reviewer assigned. *Link: [PR](https://github.com/agentscope-ai/CoPaw/pull/5669)*

---

*Generated 2026-07-08 from CoPaw GitHub activity — 38 PRs, 17 issues, 1 release.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-08

## Today's Overview

ZeroClaw shows high-velocity, mature-project activity with **23 issues updated** and **50 PRs updated** in the last 24 hours. Engineering focus is concentrated on _safety and correctness_ — three critical bug fixes landed or are in-flight for the SOP approval-gate bypass (#8678), the tool-filter no-op on real MCP tools (#6699), and the unbounded RSS growth from MCP schema cloning (#8642). A major cross-cutting `feat/sop-authoring` branch (#8590) with visual workflow editing is actively being reviewed and tested, signaling a significant feature delivery in progress. Community contributions remain strong, with several first-time bug reporters surfacing Windows stability issues and documentation discrepancies. No new releases were cut today.

## Releases

**No new releases today.** The last known release is v0.8.2 (visible in the web dashboard version label from #8791).

## Project Progress

**4 PRs merged/closed today:**
- [#8815](https://github.com/zeroclaw-labs/zeroclaw/pull/8815) — **Feature closed**: Adds a `skill_manage.create` action so agents can save new skills as bundles, not loose `.md` files (maksyms)
- [#8782](https://github.com/zeroclaw-labs/zeroclaw/pull/8782) — **Fix closed**: Bumps `crossbeam-epoch` 0.9.18 → 0.9.20 to clear RUSTSEC-2026-0204 (wangmiao0668000666)
- [#8678](https://github.com/zeroclaw-labs/zeroclaw/pull/8678) — **Bug closed**: `advance_step` had no run-status guard — a driver could bypass approval gates via `sop_advance` (Stalesamy)
- [#6970](https://github.com/zeroclaw-labs/zeroclaw/pull/6970) — **Tracker closed**: v0.8.1 integration/channel/provider/tool queue and history (Audacity88)

**Notable open PRs advancing today:**
- [#8817](https://github.com/zeroclaw-labs/zeroclaw/pull/8817) — Arc-share tool schemas to stop per-iteration clone churn (fixes OOM root cause #8642)
- [#8816](https://github.com/zeroclaw-labs/zeroclaw/pull/8816) — Hot-reload log persistence and rotation config (fixes #8314)
- [#8819](https://github.com/zeroclaw-labs/zeroclaw/pull/8819) — Classify `tool_filter_groups` targets by MCP origin (fixes #6699)
- [#8806](https://github.com/zeroclaw-labs/zeroclaw/pull/8806) — `run_model_query` metered provider seam (S21 P1) landed for review
- [#8805](https://github.com/zeroclaw-labs/zeroclaw/pull/8805) — Align skill prompt callable-tool set with registry (fixes #8804)
- [#8788](https://github.com/zeroclaw-labs/zeroclaw/pull/8788) — Apply `excluded_tools` denylist to skill-registered tools (fixes #8787)
- [#8784](https://github.com/zeroclaw-labs/zeroclaw/pull/8784) — Split-history loop contract for Agent entry points (PR-1 of #7846 rework)

## Community Hot Topics

**Most active issues today:**

1. [#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) — **tool_filter_groups is a no-op for real MCP tools** (9 comments)
   - Two distinct bugs identified: prefix mismatch in the filter gate, plus no integration with deferred_loading. A fix PR [#8819](https://github.com/zeroclaw-labs/zeroclaw/pull/8819) was opened today. Underlying need: operators configuring tool access policies expect them to work correctly with MCP-managed tools, not just built-in tools.

2. [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) — **RFC: Add a per-execution confirmation tier for high-risk shell commands** (6 comments)
   - Users want a "confirm every time" middle tier between "always allow" and "always deny" for high-risk shell commands, plus pattern-matching policy. This is a Claude Code-style safety feature. Community clearly wants more granular safety controls without disabling functionality entirely.

3. [#7952](https://github.com/zeroclaw-labs/zeroclaw/issues/7952) — **Publish full-channel prebuilt assets** (5 comments)
   - Currently blocked, needs-maintainer-review. Users configuring non-default channels find the lean default build doesn't include their desired channel. Underlying need: making channel experimentation frictionless for power users.

4. [#8642](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) — **MCP/tool-schema cloning drives unbounded RSS growth** (1 comment, but associated fix PR [#8817](https://github.com/zeroclaw-labs/zeroclaw/pull/8817) is large and cross-cutting)
   - User @andreymaznyak reported OOM in WSL2. Split from multi-root-cause tracker #5542. The fix changes schema ownership from per-iteration deep clones to `Arc`-shared references. Underlying need: long-running agent sessions must not leak memory.

## Bugs & Stability

**New bugs reported today (ranked by severity):**

**S1 — Workflow blocked:**
- [#8794](https://github.com/zeroclaw-labs/zeroclaw/issues/8794) — **Stopping the agent mid-work erases tool calls and thinking from context**. Next user message loses all context from the interrupted turn. No fix PR yet. (susyabashti)

**S2 — Degraded behavior:**
- [#8800](https://github.com/zeroclaw-labs/zeroclaw/issues/8800) — **Windows: killed zeroclaw process leaves port bound** (zombie LISTENING/CLOSE_WAIT). New daemon fails to start. Windows 11 25H2, Edge 150. (NiuBlibing)
- [#8810](https://github.com/zeroclaw-labs/zeroclaw/issues/8810) — **Documentation is wrong — Telegram example**. Setup instructions reference unknown config properties; example output appears incorrect. (cr3a7ure)
- [#8797](https://github.com/zeroclaw-labs/zeroclaw/issues/8797) — **bind-telegram setup instructions reference unknown configuration property** (Moulde)
- [#8804](https://github.com/zeroclaw-labs/zeroclaw/issues/8804) — **Skills prompt advertises callable-tool set that doesn't match the registry** (MCP missing, target-less elevation over-listed). Fix PR [#8805](https://github.com/zeroclaw-labs/zeroclaw/pull/8805) open. (Nillth)
- [#8787](https://github.com/zeroclaw-labs/zeroclaw/issues/8787) — **Skill-registered tools bypass `allowed_tools`/`excluded_tools`** (#6959 class, missed for skills). Fix PR [#8788](https://github.com/zeroclaw-labs/zeroclaw/pull/8788) open. (Nillth)

**S3 — Minor:**
- [#8791](https://github.com/zeroclaw-labs/zeroclaw/issues/8791) — **Left sidebar has incorrect width causing horizontal scrollbar** in web dashboard (NiuBlibing)
- [#8792](https://github.com/zeroclaw-labs/zeroclaw/issues/8792) — **Left sidebar is missing a Skills navigation entry** (NiuBlibing)

**Existing critical bugs with fix PRs today:**
- [#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699) (tool_filter_groups no-op, risk:high) → Fix PR [#8819](https://github.com/zeroclaw-labs/zeroclaw/pull/8819) opened
- [#8642](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) (MCP schema clone OOM, risk:high) → Fix PR [#8817](https://github.com/zeroclaw-labs/zeroclaw/pull/8817) opened
- [#8678](https://github.com/zeroclaw-labs/zeroclaw/issues/8678) (SOP approval gate bypass, risk:high) → **CLOSED** with fix merged
- [#6698](https://github.com/zeroclaw-labs/zeroclaw/issues/6698) (Fluent locale files lag English sources) — No fix PR yet

**Security dependencies:**
- [#8519](https://github.com/zeroclaw-labs/zeroclaw/issues/8519) (wasmtime-wasi CVE reconciliation, risk:high) — Still in-progress, 22 RustSec advisories not yet addressed
- [#8782](https://github.com/zeroclaw-labs/zeroclaw/issues/8782) (crossbeam-epoch RUSTSEC-2026-0204) — **CLOSED** with fix merged via PR [#8818](https://github.com/zeroclaw-labs/zeroclaw/pull/8818)

## Feature Requests & Roadmap Signals

**New feature requests today:**
- [#8803](https://github.com/zeroclaw-labs/zeroclaw/issues/8803) — **Collapse completed turn's intermediate steps into a single group** in the web dashboard chat. User wants the transcript to remain readable across many turns. This is a UI polish item that would improve long-session usability. (NiuBlibing)
- [#8798](https://github.com/zeroclaw-labs/zeroclaw/issues/8798) — **RFC: Consolidate /ws/chat and /acp onto a single wire protocol**. Proposes merging two parallel WebSocket channels into one, reducing gateway complexity. This is a significant architectural RFC that would touch 2132+ lines in `ws.rs`. (NiuBlibing)

**Features likely for v0.8.3 (from tracker #8073):**
- Hot-reload log persistence config (#8314 → PR #8816 open)
- Per-cron-job `uses_memory` flag (#8676 → PR open)
- MSRV bump to 1.96.1 (#8801 → PR open)
- Herdr agent reporting integration (#8337 → PR open, needs-author-action)
- Native Inkbox channel (#8384 → PR open, needs-author-action)
- Runtime-profile `prompt_injection_mode` override (#8235 → PR open)

**Features likely for v0.9 (from SOP authoring work):**
- SOP visual authoring with node-graph editor (#8590 → PR open, XL size)
- TodoWrite tracker for ZeroCode (#8639 → PR open, XL size)
- Per-execution confirmation tier for high-risk shell commands (#7155 → RFC accepted)

## User Feedback Summary

**Pain points expressed today:**
1. **Windows stability**: A user reports that killing ZeroClaw on Windows 11 leaves the port bound (zombie LISTENING/CLOSE_WAIT), preventing daemon restart (#8800). This is a regression-level UX issue for Windows users.
2. **Workflow disruption**: Stopping the agent mid-work erases all intermediate tool calls and thinking from context (#8794). This is rated S1 (workflow blocked) — the most severe user-facing bug reported today.
3. **Documentation mismatches**: Multiple users reporting Telegram setup instructions reference unknown config properties (#8797, #8810). The Telegram documentation and CLI behavior are inconsistent, wasting setup time.
4. **Security policy bypasses**: Skill-registered tools ignoring `excluded_tools` (#8787) and the prompt advertising wrong callable tool sets (#8804) — users configuring access controls cannot trust the system's tool exposure.
5. **Memory growth**: Long-running OOM issues in WSL2 being addressed by the schema-clone fix (#8642), but the user experience of having to restart the daemon periodically is a known pain point.

**Positive signals:**
- The SOP visual authoring PR (#8590) explicitly calls for beta testers, indicating the maintainers are confident enough in the feature to seek real-world validation.
- Multiple first-time issue reporters (Moulde, cr3a7ure, susyabashti) are finding ZeroClaw and taking the time to file detailed bug reports — a sign of growing, invested community.
- The MSRV bump to 1.96.1 (#8801) signals the project is keeping current with Rust toolchain for safety and feature access.

## Backlog Watch

**Issues needing maintainer attention:**

1. [#6698](https://github.com/zeroclaw-labs/zeroclaw/issues/6698) — **Fluent locale files lag English sources** (opened 2026-05-16, 3 comments). `zh-CN` has only `cli.ftl` while English has both `cli.ftl` and `tools.ftl`. This is a localization health issue that has been open for 53 days without a fix PR. Non-English users are getting a degraded experience.

2. [#7952](https://github.com/zeroclaw-labs/zeroclaw/issues/7952) — **Publish full-channel prebuilt assets** (opened 2026-06-19, 5 comments). Tagged `needs-maintainer-review` and `blocked`. This blocks users who need non-default channels from using prebuilt binaries.

3. [#8337](https://github.com/zeroclaw-labs/zeroclaw/pull/8337) — **Herdr agent reporting integration** (opened 2026-06-26, L size). Tagged `needs-author-action`. The herdr sidebar integration for agent lifecycle visibility has been sitting for 12 days awaiting author updates.

4. [#8384](https://github.com/zeroclaw-labs/zeroclaw/pull/8384) — **Native Inkbox channel** (opened 2026-06-27, XL size). Tagged `needs-author-action`. Significant new channel adding email, SMS, voice, and iMessage support — has been pending for 11 days.

5. [#8519](https://github.com/zeroclaw-labs/zeroclaw/issues/8519) — **wasmtime-wasi CVE reconciliation** (opened 2026-06-30, 1 comment). Priority P1, risk high, 22 RustSec advisories not yet addressed. The audit.toml/deny.toml drift means CI is failing on master, and this has been open for 8 days without a fix PR.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*