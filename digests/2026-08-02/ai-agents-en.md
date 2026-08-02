# OpenClaw Ecosystem Digest 2026-08-02

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-02 01:25 UTC

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

# OpenClaw Project Digest — 2026-08-02

---

## 1. Today's Overview

OpenClaw is in a period of **intense maintenance and stabilization activity**. The project saw 500 issues and 500 PRs updated in the last 24 hours, with 38 issues closed and 100 PRs merged/closed, indicating a healthy, active triage and fix pipeline. The single new release (v2026.7.2-beta.6) is squarely focused on **state safety and crash recovery**, addressing a cluster of high-severity data-corruption and session-state bugs that have dominated recent community reports. While the volume of open P0/P1 issues (two P0s, ~15 P1s in the top 50) remains a concern, the rapid pace of incoming fixes—particularly from maintainers like steipete and vincentkoc—suggests the team is actively converging on the most critical stability hotspots. The community remains highly engaged, with several issues exceeding 20 comments and reflecting deep, real-world usage across Telegram, Slack, Discord, and other channels.

---

## 2. Releases

**v2026.7.2-beta.6** (`openclaw 2026.7.2-beta.6`)

This is a **stability-focused beta release** centered on data safety and recovery. The headline highlights all relate to protecting persisted state:

- **Quarantine store**: Persisted data is now protected by a quarantine mechanism that survives primary-database damage.
- **Crash-recoverable SQLite snapshots**: Snapshots can now be recovered after a crash.
- **Crash-durable filesystem publication**: File writes are made durable across crashes.
- **Schema-upgrade data-loss rejection**: The system will reject schema upgrades that would result in data loss.
- **Rollback-writer snapshot recovery**: Adds recovery support for the rollback-writer snapshot mechanism.

**Breaking Changes / Migration Notes:** None explicitly detailed in the release notes. However, given the focus on state recovery, users on previous 6.x or 7.x versions should back up their `~/.openclaw/` directory before upgrading. The schema-upgrade rejection logic implies that **downgrading after upgrade is no longer safe** and may trigger quarantine/recovery flows, as highlighted by Issue #115421.

---

## 3. Project Progress

The last 24 hours show strong momentum in fixing long-standing bugs and addressing community pain points. Key merged/closed PRs and their impact:

- **Telegram Dedup Fix (#117506)**: A fix for safely deduplicating resumed conversation context, preventing silent message drops in group chats with pinned messages. *High impact for Telegram users.*
- **Slack Semantic Progress Cards (#116671)**: Shifts Slack default from noisy partial answer streaming to concise semantic progress cards, improving UX for unconfigured workspaces.
- **Teams-Meetings Probe Deadline (#111455)**: Fixes stalled setup probes in Microsoft Teams `chrome-node` talk-back prerequisites, preventing synchronous blocks beyond the 10-second budget.
- **Plugin Catalog Refresh (#117724)**: Fixes a bug where a marketplace refresh didn't update the already-running Gateway's cached catalog until restart.
- **Media Scratch Cleanup (#117716)**: Cleans up `openclaw-media-cli` scratch directories after setup failures, preventing temp-file accumulation.
- **Stream-Error History Repair (#117699)**: Hides synthetic "[assistant turn failed]" rows when later content repairs the turn, cleaning up session history display.

**Still open but progressing (with fix PRs linked):**
- **Memory-Flush Token Estimation (#83178)**: Fixes `totalTokens` staying undefined when providers like MiniMax don't return usage data.
- **Per-Candidate Compaction Timeout (#115968)**: Addresses a 100% failure rate for CLI-budget compaction on large sessions due to a shared timeout across fallback candidates.
- **Auth Key Retention for Non-Default Agents (#116248)**: Fixes the default agent losing API keys after a secondary `paste-api-key` operation.

---

## 4. Community Hot Topics

The most-discussed issues reveal deep user engagement and critical production pain points:

### [🔴 #116277 — DeepSeek v4 Flash Silent Reply Failure (73 comments)](https://github.com/openclaw/openclaw/issues/116277)
**Underlying need:** **Reliability of model fallback.** Users rely on OpenClaw to gracefully handle model failures. This issue shows a silent failure with a generic fallback message, highlighting a desire for transparent error reporting and robust retry/fallback logic when a primary model glitches. The "platinum hermit" rating and "needs-live-repro" tags indicate this is a flaky, high-priority issue for maintainers.

### [🟠 #25592 — Text Between Tool Calls Leaks to Messaging Channels (39 comments)](https://github.com/openclaw/openclaw/issues/25592)
**Underlying need:** **A clean, controlled user interaction model.** Users are frustrated by internal agent narration/processing leaking into public channels (Slack, iMessage). The demand is for stricter separation between internal reasoning and user-facing output. This is a long-standing UX/fidelity issue with security implications (internal state exposure).

### [🟠 #116201 — Realtime Voice State Leak (36 comments)](https://github.com/openclaw/openclaw/issues/116201)
**Underlying need:** **Resource safety for long-running/realtime sessions.** This issue highlights that realtime voice sessions can retain unbounded state (provider frames, pre-ready audio, superseded consult work), pointing to a need for robust lifecycle management and hard ownership bounds to prevent memory leaks and stalls.

### [🟡 #99241 — Tool Outputs Rendered as Unreadable Images (26 comments, Closed)](https://github.com/openclaw/openclaw/issues/99241)
**Underlying need:** **Agent self-awareness and debuggability.** When tool output becomes an image attachment, the agent loses the textual evidence it needs to continue its work. This was a P1 "platinum hermit" bug that has been **closed**, suggesting a fix has been identified.

---

## 5. Bugs & Stability

This is the dominant theme of the current development cycle. Ranked by severity:

### P0 (Critical) — Data Loss & Corruption
- **[#101290 — CLI Preflight Corrupts Live State DB](https://github.com/openclaw/openclaw/issues/101290)**: "database disk image is malformed" errors on macOS leading to repeated DB corruption. No fix PR linked yet. **Highest severity.**
- **[#115421 — Schema Downgrade Recovery Wipes State DB](https://github.com/openclaw/openclaw/issues/115421)**: Recovery logic for a schema downgrade leaves an empty DB, losing cron jobs. The new quarantine store in v2026.7.2-beta.6 is likely a direct response to this class of issues. No specific fix PR linked.

### P1 (High) — State Corruption, Message Loss, Security
- **[#116010 — Persistent Sessions Capped at 128k Context](https://github.com/openclaw/openclaw/issues/116010)**: Incorrectly limited context window, degrading agent performance.
- **[#94939 — 6.x Migration Leaves Conversation Store Empty](https://github.com/openclaw/openclaw/issues/94939)**: Data loss for MS Teams Bot Framework sends after migration.
- **[#25592 — Text Leaks Between Tool Calls](https://github.com/openclaw/openclaw/issues/25592)**: Security/UX issue, still open with no fully merged fix.
- **[#114234 — Usage-Cost Lock Never Releasable in Containers](https://github.com/openclaw/openclaw/issues/114234)**: A stuck PID lock permanently freezes the cache. *Has an open PR (#116248 is different, but this has a linked PR per the data).*
- **[#115908 — Transcript Projection Livelock](https://github.com/openclaw/openclaw/issues/115908)**: A livelock in the session transcript projection that can stall the entire main thread and all channel transports.
- **[#115326 — Crash-Loop Breaker Suppresses Channels Permanently](https://github.com/openclaw/openclaw/issues/115326)**: Documented recovery path fails with WebSocket 1006, leaving Discord/WhatsApp permanently disabled.

### P2 (Medium) — UX Friction & Regressions
- **[#112906 — Rich Messages Regression (`` broken)](https://github.com/openclaw/openclaw/issues/112906)**: Collapsible sections render as flat text.
- **[#90711 — launchd plist Hides stderr](https://github.com/openclaw/openclaw/issues/90711)**: macOS `launchd` setup discards all logs, hampering debugging.
- **[#74378 — CLI Processes Remain Alive on Windows](https://github.com/openclaw/openclaw/issues/74378)**: Zombie `node.exe` processes consume resources.

---

## 6. Feature Requests & Roadmap Signals

Despite the focus on stability, several feature requests signal where the project is heading:

- **[#113251 — Image Viewing in Webchat File Viewer](https://github.com/openclaw/openclaw/issues/113251)**: Users want better in-browser preview of images. Likely a quick win for a future version, given the high number of comments (10) and clear screenshots.
- **[#17840 — Opt-in Reaction-Triggered Agent Turns](https://github.com/openclaw/openclaw/issues/17840)**: This opens up new interactive patterns (e.g., emoji polling). This feels like a natural progression for chat-based agents and could be a candidate for a minor version.
- **[#110171 — Voice Chat Context Parity with Text](https://github.com/openclaw/openclaw/issues/110171)**: A strong signal from the community that voice mode is important but lacks the full context of text mode (memory files, history). This is a strategic feature request for parity and likely on the roadmap.
- **[#95724 — Memory Indexing by Source Directory](https://github.com/openclaw/openclaw/issues/95724)**: Eliminating duplicate vector stores for multiple agents in the same workspace is an efficiency and consistency improvement. This is a meaningful architectural change suggested by users.

**Prediction:** The next minor version (v2026.8.x) will likely continue the stability streak, but we can expect **image viewing in WebChat** and possibly **reaction-triggered turns** as relatively low-risk feature additions. The groundwork for `memory` improvements may be laid out over the next few releases.

---

## 7. User Feedback Summary

The chatter around the project reveals a mix of deep appreciation and high expectations:

- **Positive Sentiment:** Users like those from Issue #73537 ("Thank you for OpenClaw... genuinely become part of our daily workflow") highlight the value of OpenClaw as a critical tool for family/business automation.
- **Primary Pain Points:**
    - **Reliability & Failures:** Silent failures (like the DeepSeek issue) and unhelpful generic error messages are the most significant frustrations.
    - **State Management:** Users are hitting walls with session context limits, compaction failures, and data loss on migrations.
    - **UX Fidelity:** Leaking internal reasoning, broken rich messages, and misclassified inbound messages degrade trust in the assistant's responses.
    - **Configuration Visibility:** Issues like the API key loss and environment variable scoping (`exec` missing `skills.env`) show that configuration management is a source of confusion and failure.
- **Advanced User Needs:** Reports on `before_agent_run` input provenance (#107069) and ACP session issues (#115847) show that power users are building sophisticated integrations and need more granular control and visibility.

---

## 8. Backlog Watch

These items are critical but appear to be without a clear fix PR, needing focused maintainer attention:

1.  **[#101290 (P0) — CLI Preflight DB Corruption](https://github.com/openclaw/openclaw/issues/101290)**: The most critical open bug. Data loss is the highest-priority issue for any data-management tool.
2.  **[#115421 (P0) — Schema Downgrade Wipes State DB](https://github.com/openclaw/openclaw/issues/115421)**: Directly related to release safety and upgrade/downgrade paths. The new quarantine logic should be validated against this.
3.  **[#25592 (P1) — Internal Text Leaks](https://github.com/openclaw/openclaw/issues/25592)**: A long-standing (since Feb) yet critical UX/security issue that has seen active discussion (39 comments) but no merged fix.
4.  **[#31583 (P1) — `exec` Doesn't Inherit Skill Env Vars](https://github.com/openclaw/openclaw/issues/31583)**: A regression that breaks secret injection into subprocesses. It's been open since March and has a linked, open PR.
5.  **[#48920 (P1) — Live Docs Ahead of Release](https://github.com/openclaw/openclaw/issues/48920)**: A process issue; documentation referencing unreleased features causes user confusion and configuration errors.
6.  **[#74378 (P2) — Zombie CLI Processes on Windows](https://github.com/openclaw/openclaw/issues/74378)**: A platform-specific bug for a major OS that likely affects many users, causing resource leaks over time.

---

**Overall Health Assessment:** OpenClaw is a **thriving but strained project**. The incredibly high volume of issues, particularly around state safety, points to growing pains from a rapidly expanding user base. However, the team's fast response time (many P1s have open PRs) and the targeted new release are strong signals of a capable and responsive maintainer group. The immediate roadmap is dictated by stability, but the thoughtful feature requests and power-user bugs will shape the platform's evolution. The project is in a "stabilize and harden" phase, which is both necessary and promising.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-02
**Scope:** 13 projects in the AI agent / personal assistant open-source ecosystem

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by **intense stability-focused maintenance**, with the most active projects (OpenClaw, Hermes Agent, NanoBot) investing heavily in crash recovery, data integrity, and state management rather than new features. A clear **platform consolidation trend** is emerging: projects are unifying fragmented channel integrations (NanoClaw's iMessage consolidation, OpenClaw's channel deduplication) and standardizing provider abstractions (OrcaRouter appearing as a built-in provider in IronClaw, CoPaw, and PicoClaw simultaneously). **Security hardening** is a rising priority, particularly around credential isolation, permission boundaries, and approval flows (ZeroClaw's RFC-based security architecture, Hermes Agent's cross-profile credential leaks, Moltis's operators list). The ecosystem is bifurcating into **general-purpose orchestration platforms** (OpenClaw, Hermes Agent) and **specialized/vertical agents** (LobsterAI, Moltis), with several projects entering **consolidation or potential maintenance-risk phases** (PicoClaw's stale critical bug, LobsterAI's auto-closed stale issues).

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Releases | Closures (24h) | Health Score | Overall Phase |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 updated | 500 updated | 1 (beta) | 38 issues, 100 PRs | **8.5/10** — High velocity, active triage, but P0 data-loss bugs open | Stabilize & Harden |
| **Hermes Agent** | 50 updated | 50 updated | 0 | 17 issues, 13 PRs | **8/10** — Rapid fix turnaround, strong community, Windows gaps | Consolidation |
| **NanoBot** | 5 updated | 25 updated | 0 | 0 issues, 13 PRs | **8/10** — Fast bug-fix cycle, responsive maintainers, stale PRs | Steady Development |
| **CoPaw** | 9 updated | 13 updated | 0 | 0 issues, 1 PR | **7.5/10** — Same-day fixes for critical bugs, growing contributor base | Active Growth |
| **Moltis** | 0 new | 3 updated | 0 | 0 issues, 2 PRs | **7/10** — Stable, clean backlog, no new bugs | Stabilizing |
| **IronClaw** | 18 updated | 24 updated | 0 | 0 issues, 8 PRs | **7/10** — Strong architecture discipline, but core-team concentrated, release-starved | Architectural Refactor |
| **NanoClaw** | 2 updated | 16 updated | 1 (v2.1.54) | 0 issues, 6 PRs | **7/10** — Responsive to issues, breaking change risk | Feature + Harden |
| **ZeroClaw** | 50 updated | 50 updated | 0 | 3 issues, 0 PRs | **6/10** — Deep RFC engagement, but massive review bottleneck | Design & Security RFC |
| **PicoClaw** | 1 updated | 3 updated | 0 | 0 issues, 1 PR | **5/10** — Contributor momentum, but critical stale bug unfixed (31 days) | Moderate / Risk |
| **LobsterAI** | 7 updated | 2 updated | 0 | 6 issues (stale-closed) | **3.5/10** — Stale-closure sweep, 4-month-old unmerged PRs, maintainer disengagement | Stagnation Risk |
| **NullClaw** | — | — | — | — | **N/A** — No activity | Dormant |
| **TinyClaw** | — | — | — | — | **N/A** — No activity | Dormant |
| **ZeptoClaw** | — | — | — | — | **N/A** — No activity | Dormant |

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale dominance:** 500 issues and 500 PRs in 24 hours exceeds the combined activity of all other active projects (roughly 10x the next busiest). This indicates the largest user base and community feedback loop in the ecosystem.
- **Rapid fix velocity:** 100 PRs merged/closed in 24 hours — more than most projects process in a week. Maintainers (steipete, vincentkoc) are actively converging on critical stability hotspots.
- **Proactive state-safety innovation:** The quarantine store, crash-recoverable SQLite snapshots, and schema-upgrade data-loss rejection (v2026.7.2-beta.6) are **ahead of peers** — no other project has shipped equivalent data-protection mechanisms.

**Technical Approach Differences:**
- OpenClaw uses a **monolithic, channel-agnostic core** with unified state persistence. Peers like NanoBot (Python) and CoPaw (Qwen-specialized) are narrower in scope.
- OpenClaw's **schema-upgrade rejection** is uniquely strict — it prefers refusing upgrades over risking data loss. Hermes and NanoClaw handle migrations more permissively, trading safety for flexibility.
- OpenClaw's **multi-channel parity** (Telegram, Slack, Discord, Teams, WhatsApp) is broader than any peer. Hermes Agent has strong Desktop/multiplex focus; NanoBot leads on webui UX; ZeroClaw is RFC-heavy but shipping less.

**Community Size Comparison:**
- OpenClaw's 73-comment issue threads and deep real-world usage reports indicate a **production-grade user base**. Hermes Agent shows strong community engagement (50+ issues/day, root-cause analyses in bug reports) but is ~10x smaller in volume. NanoBot and CoPaw show healthy but smaller communities. LobsterAI's auto-closed stale issues indicate community disengagement.

**Key Risks:**
- Two P0 data-loss bugs remain open (#101290, #115421) with no fix PRs. While the new quarantine store is a mitigation, the underlying corruption paths are unaddressed.
- OpenClaw's sheer issue volume risks **triaging fatigue** — the project must continue converting issue-reporting momentum into merged fixes to avoid a perception of unresponsiveness.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|---|---|---|
| **State Persistence & Crash Recovery** | OpenClaw, NanoBot, NanoClaw, Hermes Agent | Crash-durable snapshots, quarantine stores, rollback recovery, journal recovery after kills, migration safety, schema-downgrade protection |
| **Silent Failure Elimination** | OpenClaw, CoPaw, PicoClaw, LobsterAI, NanoClaw | Transparent error reporting, fallback logic visibility, empty-response surfacing, health-check signals, no silent data loss |
| **Session/Context Management** | OpenClaw, NanoBot, IronClaw, ZeroClaw, CoPaw | Context-window accuracy, compaction reliability, per-session model switching, memory lifecycle separation, context-budget correctness |
| **Credential & Secret Isolation** | OpenClaw, Hermes Agent, ZeroClaw, Moltis, NanoClaw | Per-profile token scoping, no cross-profile leaks, credential expiry alerts, operators/privilege separation, secret injection into subprocesses |
| **Provider Ecosystem Expansion** | IronClaw, CoPaw, PicoClaw, ZeroClaw | OrcaRouter as built-in provider, web-search provider abstraction, multi-vendor routing, failover strategies |
| **Channel Reliability & Permissions** | OpenClaw, ZeroClaw, NanoBot, CoPaw | Per-sender rate limiting, allowlist enforcement, mention-only handling, deduplication, no internal-text leakage |
| **WebUI/UX Fidelity** | NanoBot, CoPaw, OpenClaw, Hermes Agent | Image preview, quick-chat, per-session model switcher, sidebar plugin slots, global hotkey input |
| **CI & Release Pipeline Reliability** | IronClaw, OpenClaw, CoPaw, ZeroClaw | False-red CI gates, release safety gaps, stale release PRs, version-tag correctness |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Core Architecture | Key Differentiator |
|---|---|---|---|---|
| **OpenClaw** | General-purpose orchestration | Production users, family/business automation | Monolithic core, channel adapters, unified state DB | Unmatched channel breadth + state-safety investment |
| **Hermes Agent** | Desktop + multiplex profiles | Multi-machine, multi-profile power users | Profile-scoped, multiplex gateways, desktop app | Profile isolation & Desktop-first UX |
| **NanoBot** | Lightweight personal agent | Python/developer community | Python, extensible channels, webui | Clean webui, fast bug-fix cycle |
| **CoPaw** | Qwen/Alibaba ecosystem | Qwen-model users, Chinese-speaking | Qwen-optimized, ACP support | Deep Qwen integration, growing contributor base |
| **IronClaw** | Enterprise agent framework | Systems/ops teams | Rust, dependency-inverted modules, CI-gated | Architecture discipline, pi-harness performance work |
| **NanoClaw** | Consumer-friendly multi-channel | Non-technical users | Simplified setup, unified channels | iMessage unification, credential alerts |
| **ZeroClaw** | Security-centric agent platform | Enterprise/security-sensitive | RFC-driven design, sandboxing | Security-first roadmap (v0.9.0) |
| **PicoClaw** | Embedded/Edge agent | SBC/edge deployments | Lightweight, provider plug-ins | Provider expansion (Exa, OrcaRouter) |
| **Moltis** | Multi-tenant agent service | Teams/orgs | Per-account operators, instrumentation | Security boundaries + observability infrastructure |
| **LobsterAI** | Chinese-market agent UI | Chinese-speaking users | UI-layer, OpenClaw-engine compatible | i18n and UX polish (currently stalled) |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration / High Momentum:**
- **OpenClaw:** 500/500 issues/PRs per day, 100 PRs merged daily — the ecosystem's engine room. Maturing but straining under user-growth pressure (P0s remain).
- **Hermes Agent:** 50/50 issues/PRs per day, 13 merged — high developer throughput, sub-48h fix PRs for P2s. Consolidation phase after release pull-back.
- **NanoBot:** 25 PRs/day, steady cadence, healthy maintainer response. Maturing webui + agent features.

**Tier 2 — Active Growth / Feature Push:**
- **CoPaw:** Same-day fix PRs for critical bugs, 4 first-time contributors — strong growth signal.
- **NanoClaw:** Shipping features (iMessage unification) + responsive to issues — consumer-friendly momentum.
- **IronClaw:** Deep architecture refactor (Wave 2), but core-team concentrated — high quality, lower community surface.

**Tier 3 — Stabilizing / Holding:**
- **Moltis:** Clean backlog, no new bugs, merging foundation features (instrumentation, security).
- **ZeroClaw:** High RFC engagement but **shipping bottleneck** (0 merged PRs, 50 open, many `needs-author-action`).

**Tier 4 — Risk / Stagnation:**
- **PicoClaw:** Contributor momentum (2 new provider PRs) undermined by 31-day-old stale critical bug.
- **LobsterAI:** **Concerning** — 4-month-old unmerged PRs, 6 stale-auto-closed bugs, zero merges in 24h. Signals maintainer disengagement or bandwidth crisis.
- **NullClaw / TinyClaw / ZeptoClaw:** Dormant — no activity observed.

---

## 7. Trend Signals

1. **State Safety is the #1 Ecosystem Priority:** Across OpenClaw, NanoBot, NanoClaw, and Hermes, crash recovery, journal repair, and migration safety dominate. The industry has learned that agent state is the product — users trust assistants only when conversations and memory survive failures. **Value for developers:** Invest in crash-durable persistence, quarantine mechanisms, and schema-downgrade protection early.

2. **Provider Abstractions Are Consolidating on OpenAI-Compatible Contracts:** OrcaRouter is being added as a built-in provider simultaneously in IronClaw, CoPaw, and PicoClaw. The `vendor/model` addressing pattern (routing via a single OpenAI-compatible endpoint) is becoming the de facto standard. **Value for developers:** Build to the OpenAI Chat Completions contract with a routing layer, not to individual vendor SDKs.

3. **Security Credential Isolation Is a Non-Negotiable:** Hermes's token leaks, ZeroClaw's WhatsApp permission bypass, OpenClaw's internal-text leakage, and Moltis's operators list all signal that **multi-tenant and multi-profile deployments are mainstream**. Empty-allowlist-should-mean-deny-all is becoming the expected secure default. **Value for developers:** Default-deny permissions, per-profile credential scoping, and explicit operators/privilege separation from the start.

4. **Silent Failures Erode Trust Fastest:** The most-engaged issues across projects (DeepSeek silent reply, PicoClaw silent Matrix death, CoPaw empty-response, OpenClaw tool-output unreliability) are all **silent failure modes**. Users tolerate explicit errors; they do not tolerate invisible ones. **Value for developers:** Surface every failure explicitly, provide health-check signals for supervised daemons (systemd/docker), and never swallow errors.

5. **WebUI / UX Parity with Chat Apps Is the New Battleground:** Quick Chat, Temporary Chat (NanoBot), global hotkey quick-input (CoPaw), image preview (OpenClaw, NanoBot), per-session model switching — the "modern chat UX" bar is rising. Users expect consumer-grade interfaces for agent platforms. **Value for developers:** Budget for UX iteration alongside agent logic — discoverability and low-friction interaction drive adoption.

6. **Performance = Cost Optimization:** IronClaw's pi-harness program (cache-efficiency, token-accounting fixes) and ZeroClaw's prompt-caching complaint (#9631) show that **cache-aware token accounting is the next performance frontier**. Users are measuring cost per interaction, not just latency. **Value for developers:** Implement byte-stable prompt prefixes, explicit cache_control breakpoints, and content-reference-based token estimation (not string-length heuristics).

7. **CI False-Reds Are a Contributor Tax:** IronClaw's roll-up failure and CoPaw's evidence-fence stripping both block contributors. Every false-red burns contributor goodwill. **Value for developers:** Ensure CI gates are provably correct before enforcing them on community PRs.

---

**Bottom Line:** The ecosystem is **healthiest at the core** (OpenClaw, Hermes, NanoBot) where maintenance velocity matches user growth, and **risk concentrates at the edges** (PicoClaw, LobsterAI) where maintainer bandwidth lags community expectations. For technical decision-makers: OpenClaw remains the safest bet for production deployment due to its scale and state-safety investment; Hermes Agent for multi-profile/multi-machine desktops; NanoBot for lightweight Python-based deployment; and ZeroClaw for security-first enterprise rollouts once the v0.9.0 RFC backlog ships.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-02

## Today's Overview

NanoBot shows strong, sustained development activity with **25 PRs and 5 issues updated in the last 24 hours**, indicating a healthy, actively maintained project. Notable progress was made across multiple fronts: the WebUI received UX improvements (Quick/Temporary Chat, model switching discoverability), critical bug fixes landed for cron execution state, streamed response logging, and proxy authentication. The community is highly engaged, with one open issue about model selection flexibility and a long-running PR about DeepSeek hardening still awaiting maintainer attention. Overall, the project is in a strong state with a steady cadence of fixes and features, though somewhat fewer external contributions than average — on a scale of 1–10, I'd rate community engagement at 5.

## Releases

No new releases were published in the last 24 hours.

## Project Progress

**13 PRs were merged or closed today**, covering important areas across the codebase:

- **[#5183](https://github.com/HKUDS/nanobot/pull/5183) fix(cron): preserve manual run completion state** (merged) — Fixes a race condition where manually triggered cron jobs lost their completion state when the WebUI polled the store concurrently. This resolves the widely reported [#5163](https://github.com/HKUDS/nanobot/issues/5163).

- **[#5208](https://github.com/HKUDS/nanobot/pull/5208) fix(dream): advance cursor when durable changes were made** (merged) — Fixes the Dream cron job repeatedly reprocessing the same history batches.

- **[#5153](https://github.com/HKUDS/nanobot/pull/5153) fix(memory): handle non-string timestamp and missing role in raw_archive** (merged) — Directly addresses the KeyError bug reported in [#4801](https://github.com/HKUDS/nanobot/issues/4801).

- **[#5200](https://github.com/HKUDS/nanobot/pull/5200) fix(exec): preserve wait targets across response truncation** (merged) — Fixes `write_stdin(wait_for=...)` failing when the target is omitted by head/tail response truncation.

- **[#5201](https://github.com/HKUDS/nanobot/pull/5201) fix(session): tolerate malformed persisted session summary** (merged) — Hardens `AutoCompact.prepare_session()` against malformed persisted metadata.

- **[#5172](https://github.com/HKUDS/nanobot/pull/5172) feat: preserve Responses reasoning state and compact context** (merged) — Adopts OpenAI's ARC-AGI-3 Responses API capabilities, preserving complete opaque output-item chains including encrypted reasoning.

- **[#5108](https://github.com/HKUDS/nanobot/pull/5108) fix(channels): add per-sender message rate limiting** (merged) — Adds per-user/per-chat rate limiting across all channel adapters, a significant security hardening.

- **[#5209](https://github.com/HKUDS/nanobot/pull/5209) refactor(webui): reuse sidebar selection highlight** (merged) — WebUI UX polish, extracting selection highlighting into a shared component.

- **[#5199](https://github.com/HKUDS/nanobot/pull/5199) refactor(cli): narrow Pyright suppressions** (merged) — Code quality improvement for type-checking.

- **[#3732](https://github.com/HKUDS/nanobot/pull/3732) fix(providers): require api_base before local provider wins on keyword match** (merged) — Fixes silent hijacking of cloud-hosted models by local providers. Notably, this PR was created on May 11 and finally merged after ~2.5 months — a potential sign of stalled reviews.

## Community Hot Topics

- **[#5198](https://github.com/HKUDS/nanobot/issues/5198) [OPEN] Not possible to change models in a specific session** — This bug report is the only open issue today and touches on a core UX limitation: users cannot switch models per-session via the UI or the `/model` command. Counterpoints suggest it may be a config issue rather than a product limitation. The community is clearly asking for more flexible per-session model selection. A related **[PR #5202](https://github.com/HKUDS/nanobot/pull/5202)** makes model preset switching discoverable in the WebUI, which may address much of this pain.

- **[#5185](https://github.com/HKUDS/nanobot/issues/5185) Nanobot returning tool calls code in responses** — This issue received 4 comments and was closed as invalid (likely user misconfiguration or provider-format mismatch). It signals a potential area for better provider fallback documentation.

## Bugs & Stability

| Severity | Issue | Status | Fix |
|----------|-------|--------|-----|
| **High** | [#5163](https://github.com/HKUDS/nanobot/issues/5163) Cron job completion state lost on WebUI polling race | Closed | [#5183](https://github.com/HKUDS/nanobot/pull/5183) merged |
| **High** | [#4801](https://github.com/HKUDS/nanobot/issues/4801) Unprotected `message['role']` dict access — KeyError on malformed sessions | Closed | [#5153](https://github.com/HKUDS/nanobot/pull/5153) merged |
| **Medium** | [#5205](https://github.com/HKUDS/nanobot/issues/5205) `No module named ensurepip` when enabling feishu channel | Closed | Likely a uv/environment issue; see workaround |
| **Low** | [#5185](https://github.com/HKUDS/nanobot/issues/5185) Tool call code leaking into responses | Closed as invalid | N/A — may need docs |

All high-severity bugs reported over the past week have **fix PRs merged within days of reporting**, showcasing a responsive maintainer team.

## Feature Requests & Roadmap Signals

Several notable feature additions are in-flight:

- **[#5210](https://github.com/HKUDS/nanobot/pull/5210) Trusted proxy bootstrap auth** — Opt-in support for Cloudflare Tunnel + Cloudflare Access authentication for `/webui/bootstrap`. Very relevant for production deployments behind reverse proxies.

- **[#5211](https://github.com/HKUDS/nanobot/pull/5211) Cross-session search and mentions** — Adding `search_sessions` and `read_session` tools with `@`-mention support in WebUI chat. This is a significant capability for users with many conversations.

- **[#5184](https://github.com/HKUDS/nanobot/pull/5184) Quick Chat and Temporary Chat** — First-class Quick Chat destination with a stable session identity, plus opt-in Temporary Chat with in-memory history. This mirrors modern chat-app UX and should attract new users.

- **[#5207](https://github.com/HKUDS/nanobot/pull/5207) Model preset support for subagents** — The `spawn` tool will accept a named model preset, giving users finer control over subagent behavior.

- **[#5186](https://github.com/HKUDS/nanobot/pull/5186) Well-known skills.sh sources** — Expanding skill discovery beyond `owner/repo` to include well-known discovery hosts.

These features, if merged, will likely appear in the next minor release, touching the WebUI and agent capabilities.

## User Feedback Summary

- **Satisfaction is high**: The bug-fix cycle is fast. Issues like [#5163](https://github.com/HKUDS/nanobot/issues/5163) and [#4801](https://github.com/HKUDS/nanobot/issues/4801) were resolved in 2–3 days.
- **Per-session model flexibility is the top recurring request**: Multiple issues and PRs touch on this. Users want to switch models without reconfiguring the whole instance. The `/model` command's behavior is confusing, and the UI affordance is hidden ([PR #5202](https://github.com/HKUDS/nanobot/pull/5202) tries to fix this).
- **Deployment ergonomics** are a recurring theme: users want trusted-proxy auth and better skill discovery.
- **Documentation gaps exist** — some closed-as-invalid issues and config-related bugs suggest that users are sometimes confused by configuration semantics rather than hitting actual product defects.

## Backlog Watch

- **[#3869](https://github.com/HKUDS/nanobot/pull/3869) [OPEN] DeepSeek message hardening — preserve content, sanitize null/empty** — Open since **May 16, 2026** (~2.5 months) and flagged with a `conflict` label. This PR addresses real API-compatibility issues with DeepSeek (400 errors on null content, placeholder leakage, unconditional dropping of assistant text). It has not been updated since August 1, and needs a maintainer to resolve conflicts and make a decision.

- **[#5139](https://github.com/HKUDS/nanobot/pull/5139) [OPEN] Preserve media paths during session consolidation** — Open since July 28 with `conflict` and `p1` priority labels. This fixes losing uploaded media paths during archiving (issues [#5118](https://github.com/HKUDS/nanobot/issues/5118), [#5135](https://github.com/HKUDS/nanobot/issues/5135)). This is a data-loss-affecting fix that has been waiting nearly a week.

- **[#5194](https://github.com/HKUDS/nanobot/pull/5194) [OPEN] perf(webui): accelerate JSONL session list and thread loading** — Indexing-related performance work that has not received comments but has a solid design. Maintainers should review and consider merging.

The `conflict` label on two long-standing PRs suggests maintainers may need help with rebasing — a good opportunity for community contributors to step in.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-08-02

---

## 1. Today's Overview

Hermes Agent is demonstrating high-velocity development with 50 issues and 50 PRs updated in the last 24 hours, indicating a very active project with strong community engagement. The issue tracker shows a healthy triage pipeline: 17 issues were closed and 33 remain open, while the PR queue has 37 open PRs against 13 merged/closed. Notably, all recent releases appear to have been pulled (zero new releases reported today), suggesting the maintainers are consolidating after a busy development cycle. A significant cluster of activity centers on Windows platform stability, profile isolation/security boundaries, and desktop-specific UX bugs, with multiple dedicated fix PRs already in flight. The community is actively filing well-structured bug reports with root-cause analyses, and maintainers are responding with matching PRs — the median time from issue filing to a fix PR appears to be under 24 hours for critical P2 items.

---

## 2. Releases

**No new releases today.** The last known release was v0.19.1 (commit `7f4d155`, 2026-08-01). The project appears to be in a consolidation phase, with several important fixes (npm engine constraint, Windows installers, TTS sample rate, plugin lifecycle) merged or pending that will likely form the next patch/minor release.

---

## 3. Project Progress

**13 PRs were merged/closed today:**

**Major fixes landed:**
- **#76498** — `fmt(js): npm run fix auto-fix` (bot-maintained auto-formatting PR, auto-merged).
- **#76492** — `feat(gateway): support session-scoped toolsets` — accept optional `enabled_toolsets` on `session.create` for per-session tool control.
- **#76493** — `fix(managed_uv): keep project uv config on the candidate locked sync` — fixes SQLite WAL-reset repair failure on checkouts with `exclude-newer` uv.lock.
- **#76484** — `[Bug]: Bootstrap installer fails on desktop stage due to npm version requirement mismatch (EBADENGINE)` — closed as implemented (linked to PR #76499 allowing Node 22/npm 11).

**Feature/behavioral fixes merged:**
- **#76482** — `kanban notifier silently skips all subscriptions` — closed as implemented on main.
- **#76352** — `[Bug]: Local custom-provider MCP tool result (oversized list_entities) exceeds context` — closed as implemented on main.
- **#76448** — `gateway lifecycle guard false-positives` — closed (marked cannot-reproduce).

**Active feature development continues on open PRs (not yet merged):**
- **#76490** — plugin ownership ledger + comprehensive unload lifecycle (matches issue #64229).
- **#76488** — dashboard sidebar/footer plugin slot rendering (fixes #76381).
- **#76501** — TTS sample-rate from endpoint (fixes #76466).
- **#76499** — npm engine constraint relaxation (fixes #76486).

---

## 4. Community Hot Topics

**Most active discussions (by comment count):**

1. **[#69551 — Desktop SSH remote mode broken with non-default profiles (12 comments, CLOSED)**](https://github.com/NousResearch/hermes-agent/issues/69551)** — The most active issue involves a fundamental design conflict between Desktop's hardcoded `~/.hermes/desktop-ssh` and profile-scoped `HERMES_HOME`. The underlying need: **users with multi-profile and multi-machine setups cannot rely on Desktop SSH; profile-token validation must be relative to the active profile structure.** The issue is closed, suggesting a fix landed, but the cluster of similar SSH/issues indicates this remains a chronic pain point.

2. **[#75598 — "issue with updates" — multiple conflicting gateways from profiles (7 comments, CLOSED)**](https://github.com/NousResearch/hermes-agent/issues/75598)** — User reports unstable updates causing multiple conflicting gateways across profiles. The underlying need is **cleaner profile isolation during updates**; switching profiles should fully deactivate orphaned processes.

3. **[#65274 — Desktop project-scoped fresh sessions fall back to home cwd on Windows (6 comments, OPEN, +1)**](https://github.com/NousResearch/hermes-agent/issues/65274)** — Windows-specific Desktop cwd regression. Users expect a fresh session in a Project to start in the Project's primary path. The `+1` indicates community resonance.

4. **[#51603 — Anthropic token cross-profile credential leak in multiplex mode (5 comments, CLOSED)**](https://github.com/NousResearch/hermes-agent/issues/51603)** — Critical security concern: `resolve_anthropic_token()` bypasses profile secret scope. Closed but worryingly recent (updated 08-01) — users are very concerned about credential isolation in multiplex deployments.

**PRs with community attention:**
- **[#71996 — Hardline approval floor bypassed by absolute-path spellings](https://github.com/NousResearch/hermes-agent/pull/71996) (OPEN, P2, security)** — open for 8 days; a security-critical PR that keeps `shutdown`/`rm` blocked as `/sbin/shutdown` or `C:\Windows\...\shutdown.exe` variants. Implies **active discussion on surface-area vs. day-one installers (Windows).**
- **[#76459 — Managed Node/uv resolve first everywhere; require Node 26](https://github.com/NousResearch/hermes-agent/pull/76459)** — large cross-cutting change (3 stacked fixes) addressing toolchain consistency; notable friction around the version-bump pin (Node 26) possibly conflicting with community preference for standard Node 22 LTS.

---

## 5. Bugs & Stability

**Critical/High severity:**

1. **#76481 — [BUG] OpenRouter xAI `:online` duplicates web_search tool (P2, OPEN)** — **Duplicate tool name rejected: HTTP 400 kills the model call.** Root cause: Hermes client + OpenRouter server both expose `web_search`. **Fix PR #76496 exists** — high confidence of landing next release.

2. **#76486 — npm engine `>=12.0.0` blocks Node 22/npm 11 installs (P2, OPEN)** — fresh installs fail for all Node 22 users; only workaround is editing package.json. **Multifix PRs #76484 and #76499 ready** — likely merged imminently.

3. **#76484 — Bootstrap `.exe` fails on Windows desktop install (P2, CLOSED)** — same npm engine root cause; closed as implemented (fix merged).

4. **#76469 — Termux install: `nemo-relay<0.7,>=0.6.0` unsatisfiable (P2, OPEN)** — mobile/Linux-on-Android path blocked by dependency pin; needs-repro label but user provided logs.

5. **#76435 — Gateway reconnect loop (1000+ attempts) plus unusable desktop updater (P2, OPEN)** — Discord token reset after flood; also reports Desktop update dialog shows `managed outside...` (issue split into two). No fix PR yet — **watch this**; the updater break is arguably P1 for Desktop distribution.

**Medium severity:**
- **#76487 — Telegram topic mode not namespaced by profile under multiplex (P2, OPEN)** — cross-profile data bleed in `state.db`; **fix PR #76487 exists**, P2 risk-message-delivery flagged.
- **#76489 — MSYS drive-path media delivery failure on Windows (P2, OPEN)** — Git Bash produces `/c/...` paths that break `Path()` handling; **fix PR #76489 exists**.
- **#76485 — Event hooks registered but never fired inside Desktop agent (P3, OPEN)** — includes a `duplicate` label; needs triage to confirm the primary issue.
- **#76414 — `hermes honcho peers` misreports non-default profiles (P3, OPEN)** — root cause is `.` vs `_` in host-key building.
- **#76381 — Sidebar/footer plugin slots declared but never rendered (P3, OPEN)** — silent no-op config validation gap; **fix PR #76488 exists**.

---

## 6. Feature Requests & Roadmap Signals

| Feature | Issue/PR | Signal | Likelihood |
|---|---|---|---|
| **Plugin lifecycle: ownership ledger, on_unload, supervised tasks** | [#64229](https://github.com/NousResearch/hermes-agent/issues/64229) / [PR #76490](https://github.com/NousResearch/hermes-agent/pull/76490) | Open issue since 07-14, matching PR submitted today by a separate author | **Very high** — in review now |
| **Policy/audit authorization layer for tools** | [#34992](https://github.com/NousResearch/hermes-agent/issues/34992) | P3, open, but aligns with ongoing security hardening (PRs #71996, #69490) | Medium — roadmap synergy |
| **Font selector (family/size/color) in Desktop** | [#37566](https://github.com/NousResearch/hermes-agent/issues/37566) (CLOSED) + duplicate [#64790](https://github.com/NousResearch/hermes-agent/issues/64790) (CLOSED) | Both closed; unclear if feature shipped or rejected | Uncertain — check release notes |
| **Breathing light wake indicator (MacBook notch)** | [#74590](https://github.com/NousResearch/hermes-agent/issues/74590) (CLOSED) | Closed without PR; possibly niche/out of scope for v0.x | Low standalone; may wait for plugins |
| **Endpoint-returned TTS sample rate** | [#76466](https://github.com/NousResearch/hermes-agent/issues/76466) / [PR #76501](https://github.com/NousResearch/hermes-agent/pull/76501) | Fix PR in review | **High** — local-TTS usability enhancer |
| **Per-provider reasoning_echo opt-in** | [PR #76503](https://github.com/NousResearch/hermes-agent/pull/76503) | New feature PR, custom provider parity | **Medium** — depends on maintainer interest |
| **`EMAIL_ACCOUNT` separate from `EMAIL_ADDRESS`** | [#25849](https://github.com/NousResearch/hermes-agent/issues/25849) | Open since May (P3) | Low — old, no movement |

---

## 7. User Feedback Summary

**Pain Points (recurring themes):**
- **Profile isolation (6+ issues/PRs this week):** The single most-cited source of frustration — token leaks (#51603), foreign `.env` imports (#62935), Telegram topic cross-talk (#76487), SSH profile-name assumptions (#74776), and update-time gateway conflicts (#75598). Users with multi-profile, multi-machine, or multiplexed setups are disproportionately affected.
- **Windows is the "second-class citizen":** IME/caret composer bugs (#75960), MSYS path failures (#76489), installer `EBADENGINE` (#76484), project-cwd fallback (#65274), destructive-command approval gaps (#69490). Desktop-on-Windows users consistently report friction in every area.
- **Install/update friction:** npm 12-vs-11 constraint (#76486), Termux dependency hell (#76469), Desktop updater showing "managed outside" and not actually updating (#76435). These are **high-visibility user-facing failures** that erode trust even when core agent logic is fine.

**Satisfaction signals:**
- **Rapid fix turnaround for P2 bugs.** Many issues reported 07-31/08-01 (<=48h old) already have linked PRs (#76481→#76496, #76486→#76499, #76466→#76501).
- **Community feature requests actively acknowledged** — several long-standing feature requests (#37566, #64790) were closed, indicating maintainer response, though we cannot confirm whether they shipped.

---

## 8. Backlog Watch

**High-priority long-open items needing maintainer attention:**

| Issue | Age | Severity | Why it matters |
|---|---|---|---|
| **#32887 — `gateway_state.json` heartbeat tick missing (OPEN)** | ~10 weeks (since 05-27) | P3 | Breaks cross-container WebUI liveness; deployment infra relies on documented behavior. Needs a decision (implement or update docs). |
| **#43757 — Responses API: `function_call_output` stripped (OPEN)** | ~8 weeks (since 06-10) | P2 | Core API compatibility gap; tool results lost across turns — silently corrupts memory for `/v1/responses` clients. |
| **#25849 — `EMAIL_ACCOUNT` vs `EMAIL_ADDRESS` (OPEN)** | ~12 weeks (since 05-14) | P3 | IMAP/SMTP username semantics wrong for non-email accounts; long-dormant core-platform gap. |
| **#60845 — Queued Telegram follow-ups lose MEDIA extraction (OPEN)** | ~4 weeks (since 07-08) | P2 | Message-delivery correctness in busy mode; attachment delivered as plain text path — high visibility on Telegram. |

**Long-open security PRs:**
- **#71996 (approval floor absolute-path bypass)** — open 8 days, P2 security; needs review/merge or explicit rejection.
- **#51432 (private-network CIDR allowlist)** — open 6 weeks; needs a decision on SSRF scope vs. local-DNS-resolver environments.

---
*End of digest. All times in UTC; data current as of 2026-08-02.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-02

## 1. Today's Overview

PicoClaw is in a **moderate activity phase** with 4 items updated in the last 24 hours (1 open issue, 3 PRs). The project shows healthy community contribution momentum with **two new feature PRs** added in the past week (Exa web search provider, OrcaRouter provider) and **one merged PR** for Traditional Chinese localization. However, a **stale critical bug** in the Matrix sync loop has gone unfixed for over a month, suggesting maintainer bandwidth may be strained. No new releases were published, and the project appears to be accumulating feature work ahead of its next version bump. The overall health is **stable but with a growing backlog of unaddressed correctness issues**.

## 2. Releases

No new releases were published in the last 24 hours. The latest known version remains **v0.2.9**, which was referenced in the open Matrix sync bug report. Users on v0.2.9 are currently affected by the unresolved reconnection issue (see Bugs & Stability).

## 3. Project Progress

**Merged/Closed PRs (1):**

- **[#3261 — Add zh-TW locale and Traditional Chinese translations](https://github.com/sipeed/picoclaw/pull/3261)** *(closed/merged)* — This PR was authored by PeterDaveHello and adds Taiwanese terminology consistency across the WebUI and documentation, extending localization coverage to setup and channel guidance flows. This represents the project's continued investment in internationalization.

**Open PRs advancing features:**

- **[#3299 — Add native Exa web search provider](https://github.com/sipeed/picoclaw/pull/3299)** *(open)* — Adds Exa as a native `tools.web` / `web_search` provider with `POST /search` API support, `X-Api-Key` authentication, and range filter support. This expands PicoClaw's web search backend options.
- **[#3309 — Add OrcaRouter as an OpenAI-compatible provider](https://github.com/sipeed/picoclaw/pull/3309)** *(open)* — Introduces `orcarouter` as a first-class provider, supporting multi-vendor routing via the OpenAI Chat Completions contract at `https://api.orcarouter.ai/v1`, addressing upstream models as `vendor/model` IDs. This strengthens provider ecosystem breadth.

## 4. Community Hot Topics

The most active discussion this cycle is the **[#3203 — Matrix sync loop has no reconnection logic](https://github.com/sipeed/picoclaw/issues/3203)** issue:

- **7 comments**, **2 👍 reactions**, open for **31 days** and marked as **stale**
- **Underlying need**: Users deploying PicoClaw in production environments (likely behind systemd or Docker) require **resilient long-polling connections**. The core complaint is that silent failures — without process exit or visible errors — defeat common supervision patterns like `Restart=on-failure`. The community is asking for **self-healing reconnection logic** and/or **explicit health-check signals**.
- This is the **single most-commented and most-reacted** item in the current window, indicating it is the community's top concern.

No other issues or PRs accumulated significant comments or reactions in the last 24 hours.

## 5. Bugs & Stability

**[HIGH SEVERITY] — [#3203 — Matrix sync loop silent death after network/server disruption](https://github.com/sipeed/picoclaw/issues/3203)** *(open, 31 days, stale)*

- **Impact**: Complete and permanent loss of Matrix sync capability with zero user-visible indication. The process remains alive (exit code 0), so crash-based supervision does not recover it. This affects the core messaging functionality of the agent for any Matrix-connected deployment.
- **Root cause**: The `/sync` long-poll loop lacks reconnection logic and does not terminate the process on permanent failure.
- **Fix status**: **No fix PR exists.** The issue is marked stale, which may indicate maintainer inactivity on this critical path.
- **Severity rationale**: While this is not a data-corruption or security bug, its **silent nature and irrecoverable failure mode** make it a high-severity operational issue for any production user.

## 6. Feature Requests & Roadmap Signals

Two feature PRs signal the near-term roadmap direction:

1. **[#3299 — Exa web search provider](https://github.com/sipeed/picoclaw/pull/3299)** — This suggests PicoClaw is normalizing its web-search abstraction layer (`tools.web` / `web_search`). Branding it as "native" implies the architecture supports pluggable providers. Expect a **"web search provider interface" generification** in the next release, with Exa as the first new backend beyond defaults.

2. **[#3309 — OrcaRouter OpenAI-compatible provider](https://github.com/sipeed/picoclaw/pull/3309)** — The pattern used ("same shape as the existing...") indicates PicoClaw has an established OpenAI-compatibility extension point. The addition of OrcaRouter signals demand for **multi-vendor routing and fallback strategies** without lock-in to a single LLM API.

**Prediction**: The next minor version (likely v0.3.0) will ship both provider additions, alongside possibly a fix for the Matrix reconnection bug if maintainers re-prioritize it. The rapid succession of provider PRs suggests a **provider-expansion sprint** is underway.

## 7. User Feedback Summary

**Pain Points (explicit):**
- **Operational resilience gap**: The Matrix sync issue reflects a broader user expectation that PicoClaw should be a **set-and-forget background daemon**, not requiring manual intervention after transient network failures. Users are running this under service supervision and expecting self-healing.
- **Provider diversity demand**: The active submission of two new provider integrations within six days indicates users want **choice and redundancy** in both LLM routing and web search backends. OrcaRouter's `vendor/model` addressing specifically addresses multi-provider failover scenarios.

**Positive Signals:**
- The zh-TW localization PR being completed shows the community values **localization quality** — users are actively contributing to make the product accessible beyond English/Simplified Chinese.
- Both provider PRs were authored by different external contributors (kesku, jinhaosong-source), indicating a **healthy external contributor ecosystem** and clear, documented extension interfaces.

**Dissatisfaction (implicit):** The stale label on the most-severity bug, combined with no maintainer response in 31 days, may generate **user trust erosion** over time — the "silent death" label in the issue title reflects strong community frustration.

## 8. Backlog Watch

**[CRITICAL] — [#3203 — Matrix sync reconnection bug](https://github.com/sipeed/picoclaw/issues/3203)** *(open 31 days, 7 comments, 2 👍, marked stale)*

- **Why it matters**: This is the only open issue in the current window and is the most severe active bug. It is marked stale, and the maintainer has not responded. If this represents a pattern, **long-resident bugs may never reach the maintenance queue**, and features may outpace stability work.
- **Action needed**: Maintainers should (a) provide a status update, (b) un-stale the issue, and (c) either assign or triage a fix window. Even a workaround (e.g., documentation for `Restart=always` with watchdog) would help.

**[MONITOR] — Open provider PRs**

- **[#3299 (Exa)](https://github.com/sipeed/picoclaw/pull/3299)** and **[#3309 (OrcaRouter)](https://github.com/sipeed/picoclaw/pull/3309)** have been open for 7 and 1 days respectively, with no maintainer review comments visible. If these stall, contributor momentum could drop. These are the **highest-value pending merges** for roadmap advancement.

---

*Generated from GitHub API data for sipeed/picoclaw, snapshot 2026-08-02.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-02

## 1. Today's Overview
NanoClaw is in a period of intense, healthy development. The last 24 hours saw 16 pull requests updated (10 open, 6 merged/closed) and 2 issues, with 1 new rollup release (v2.1.54) shipping a major iMessage unification feature. Activity is high and heavily focused on reliability: the majority of merged PRs address bugs in setup, container management, and credential handling. There are no signs of stalled maintenance or community friction — the issues and PRs are substantive and collaborative, with core-team members actively participating. The project's trajectory suggests a strong focus on hardening the agent runtime and improving the multi-channel experience.

---

## 2. Releases
### v2.1.54 (Rollup)
A comprehensive rollup release covering everything merged between **v2.1.17** and **v2.1.54**.

**Key Feature:**
- **[BREAKING] Unified iMessage channel**: The previously fragmented messaging integrations are now consolidated into a single `imessage` channel with two pluggable backends, installed via the `/add-imessage` skill:
  - **Local**: Uses this Mac's `chat.db` via the Chat SDK.
  - **Hosted**: Uses native Photon integration (via `spectru...`).
  - **Migration Note**: Users with existing, separate iMessage setups will need to re-run `/add-imessage` to migrate to the new unified channel. As this is marked breaking, refer to the PR #2999 and #3164 for detailed migration steps.

---

## 3. Project Progress
Today's merged/closed PRs showcase a diversity of work, from important bug fixes to the major release feature:

- **Release Safety (#3168, merged)**: `fix(release): close post-merge safety gaps` — Improves the release pipeline's post-merge processes, likely preventing flaky or broken release states.
- **Setup Diagnostics (#3170, merged)**: `fix(setup): dispatch failure assist to the picked provider` — Directly addresses the issue raised in #3169, ensuring that when a user selects a non-Claude provider (e.g., Codex), setup diagnostics don't incorrectly route them to Claude's CLI.
- **Hosted iMessage (#3164, merged)**: `Hosted iMessage (Photon): supersede #2999 with a working registration flow` — Lands the functional hosted backend for iMessage, superseding the initial attempt in #2999. This is the foundational PR for the v2.1.54 release feature.
- **Credential Expiry Alerts (#3167, merged)**: `feat(credentials): alert when a provider credential expires` — New feature that proactively alerts on credential expiration, addressing a real-world pain point (see Bugs & Stability).
- **Codex/Copilot Compatibility (#3165, merged)**: `Codex/copilot changes` — General compatibility and functionality updates for these specific providers.
- **Potential Regression**: The migration script bug (PR #3166) — While the PR is still open, the issue it fixes may have slipped into the latest release if the rename of `insertTask` to `insertTaskRow` came after v2.1.17. This is flagged in Bugs & Stability.

---

## 4. Community Hot Topics
There are no issues with a high number of comments or reactions, but the two new issues and their corresponding PRs form a clear pattern of active community engagement and maintainer responsiveness:

- **[Issue #3171: Qodo Skills Problem](nanocoai/nanoclaw Issue #3171)**: Reports that two bundled skills (`get-qodo-rules` and `qodo-pr-resolver`) depend on a Qodo SaaS account that isn't set up, causing them to intercept normal coding requests. The **underlying need** is for a clean, default-safe experience, with integrations disabled until explicitly enabled.
  - **Response**: [PR #3172](nanocoai/nanoclaw PR #3172) immediately proposes removing the two skills.
- **[Issue #3169: Setup Failures & Claude CLI](nanocoai/nanoclaw Issue #3169)**: Reports that setup failure diagnostics wrongly offer to install Claude CLI even when a different provider was chosen. The **underlying need** is for accurate, provider-agnostic setup tooling.
  - **Response**: [PR #3170](nanocoai/nanoclaw PR #3170) (merged) fixes this exact bug.

The swift, targeted response to filed issues is a strong indicator of excellent project health.

---

## 5. Bugs & Stability
Several issues and fixes demonstrate a focused effort on runtime stability and system reliability.

- **Critical: Migration Script Broken (#3166, PR Open)** — `setup/migrate-v2/tasks.ts` imports a removed `insertTask` function, causing a `SyntaxError` that kills migration. The fix PR is open and straightforward.
- **High: Qodo Skills Intercept Requests (#3171, Issue Open)** — Broken or undesired skills hijack normal coding flows until Qodo is manually configured. A removal PR (#3172) is pending.
- **Medium: Rootless Docker Failure (#3174, PR Open)** — Agent containers fail to operate under a rootless Docker daemon due to two distinct, invisible failures. Fix PR is open.
- **Medium: Duplicate Message Delivery (#2956, PR Open)** — Agents using the `send_message` tool and also repeating the content in their final output cause duplicate messages (e.g., in WhatsApp/Telegram). The fix PR has been open since July 5th.
- **Medium: Opaque Container Kills & Expired Credentials (#3167, Merged)** — The behavior seen today: a user gets a cryptic "Read-only file system" error with no provider credential expiry warning. The new alert feature is a direct fix, but this highlights ongoing fragility in credential management. (#3168 also addresses release safety to prevent these situations.)
- **Low: Rootless Docker PR (#3174)** — Two independent failures are identified, pointing to potential architectural assumptions about Docker access that may need broader review.

---

## 6. Feature Requests & Roadmap Signals
- **Proactive Credential Alerts (Landed)**: The new credential expiry alert (#3167) addresses a clear need for operational observability. Expect future improvements in this area, such as alerts via different channels (e.g., email vs. WhatsApp) or automatic credential rotation discussions.
- **Simpler, Safer Integrations**: The immediate removal of broken Qodo skills (#3172) and the unification of iMessage (#2999/#3164) signal that the project is prioritizing a "flake-free" default experience. Users can expect more rigorous skill sandboxing or opt-in-only integrations in the future.
- **Robust Container Orchestration**: The PR for rootless Docker support (#3174) is a significant signal. As containerized agents become more standard, evolving the architecture to be fully agnostic of the Docker daemon's security model will be a major, ongoing theme.

---

## 7. User Feedback Summary
- **Pain Point: Misleading Diagnostics**: The setup issue (#3169) shows real user frustration when diagnosing a problem leads them down the wrong path (e.g., offering Claude CLI for a Codex issue).
- **Pain Point: Dead Integrations**: The state of the Qodo skills (#3171) represents a bad default experience—a feature that seems to be available but is non-functional, intruding on normal workflows.
- **Satisfaction: Responsive Maintainers**: The fact that maintainers authored and merged fixes for reported issues (e.g., #3170) and developed entire features (like the iMessage unification, #3164) based on community and core-team feedback suggests a very positive and collaborative feedback loop.

---

## 8. Backlog Watch
These long-running, important PRs are awaiting attention and have not been updated in a while, suggesting they may be stale or need a maintainer push:

- **[PR #2750](nanocoai/nanoclaw PR #2750) — fix: recover stale outbound.db journals...** (Open since June 12): A critical fix for two failure modes following container kills. It's been active for over a month and needs a final review or merge decision.
- **[PR #2956](nanocoai/nanoclaw PR #2956) — fix(agent-runner): suppress duplicate delivery...** (Open since July 5): This duplicate-message bug is an active annoyance in supported channels. The PR is complete in scope and just needs a review.
- **[PR #2801](nanocoai/nanoclaw PR #2801) — fix(router): harden untrusted router input...** (Open since June 17): Directly addresses robustness for an external-facing interface; a strong candidate for merge to improve stability.
- **[PR #3090](nanocoai/nanoclaw PR #3090) — fix(templates): prepend all top-level context Markdown** (Open since July 19): A core-team effort to fix context formatting. Its long open time with recent activity (Updated Aug 1) suggests it may be in a detailed review cycle.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-02

## 1. Today's Overview

IronClaw is in the middle of a **high-intensity architectural refactoring wave** ("Wave 2" of the reborn dependency-boundary program), with 18 issues and 24 PRs updated in the last 24 hours. The project shows **strong, coordinated momentum**: multiple stacked PRs (WS2.1→WS2.5) are progressing through the dependency-inversion effort, and a new "pi-harness adoption program" (P0/P1 priorities) is driving LLM cache-efficiency and token-accounting improvements. However, the activity is notably **core-team concentrated** — BenKurrek and ilblackdragon authored the vast majority of items. A **new contributor** (ogarciarevett) landed a small test PR, and rdisandro (a "regular" contributor) submitted a UI-only OOBE prototype. The most urgent concern is a **structural CI roll-up failure** (#6978) affecting all `workflow_dispatch` runs, which blocks reliable validation of dispatched test runs.

## 2. Releases

No new releases were published in the last 24 hours. A long-stale release PR (#5598, open since July 3) is still pending — it proposes:
- `ironclaw_common`: 0.4.2 → 0.5.0 (**API breaking** — new trait impls)
- `ironclaw_safety`: 0.2.2 → 0.2.3 (compatible)
- `ironclaw_skills`: 0.3.0 → 0.4.0 (**API breaking**)

This PR being open for a month suggests release-blocking work or prioritization of the reborn refactor over shipping.

## 3. Project Progress

**Merged/closed PRs today (8 total, most notably):**

- **#6995** — Wave 1 "truth audit": reconciled the decision record with shipped reality after seven WS1 PRs merged (docs).
- **#6996** — Closed issue #6963: inventory-driven discovery + fail-closed fixes for **eight path-keyed CI gates** that the previous sweep (#6946) missed.
- **#6998** — WS2.1: inverted `extension_host`'s product-facing ports onto `product_contracts` (behavior-free refactor).
- **#7002** — WS5: inverted webui + openai_compat onto `product_contracts`.
- **#6761** — (new contributor ogarciarevett) regression test covering generic outbound registration.

**In-flight Waves 2 PRs (all core-authored, heavily stacked):**

- **#7000** — WS2.2: resolving the `ProductSurfaceFailure` "linchpin" (largest remaining term debt)
- **#7003** — WS2.4: splitting `ironclaw_extension_manager` out of `extension_host`
- **#7004** — WS5: inverting `ironclaw_operator` ports
- **#7005** — WS5: fixing the conversations/threads naming trap + widening attachments

## 4. Community Hot Topics

- **[#6963](https://nearai/ironclaw Issue #6963) — "Path-keyed CI gates that survive #6946"** (7 comments, now closed) — BenKurrek filed this as a *tracking issue* because "a checklist row is weak tracking for eight discovered defects." All resolved by #6996. This pattern — using issues as persistent tracking for systematic defects — is a healthy project habit.
- **[#6974](https://nearai/ironclaw Issue #6974) — libSQL post-#6696 performance pathology** (2 comments) — Tool-heavy stress cases are 37–135s at p95 (vs 2.5s target). Split out of the Postgres capacity recovery issue. This is the **most severe performance regression** in flight.
- **[#6978](https://nearai/ironclaw Issue #6978) — reborn-tests.yml roll-up structural failure** (1 comment) — `workflow_dispatch` runs **always fail the roll-up** because `critical-mutation` is skipped by design but *disallowed* by the roll-up config. A CI logic bug, not a code failure.
- **[#7009](https://nearai/ironclaw Issue #7009) — Add OrcaRouter as a built-in LLM provider** (0 comments) — Community request to add a missing-but-popular LLM gateway. Simple `providers.json` addition, likely a good first-issue for external contributors.

## 5. Bugs & Stability

Ranked by severity (with fix status):

1. **[#6974](https://nearai/ironclaw Issue #6974) — libSQL thread_store_writes p95 37–135s** — Critical performance bug. The nightly stress suite now *completes* only after #6973's fixes, but tool-heavy cases are 15–54× over the 2.5s p95 target. **Fix:** #6973 (Postgres capacity recovery) is a prerequisite; no dedicated libSQL fix PR yet. **Active investigation.**
2. **[#6978](https://nearai/ironclaw Issue #6978) — CI roll-up structurally fails on workflow_dispatch** — High severity for developer velocity; every manually-dispatched test run reports *false-red*. The proof chain is documented from the workflow source (`reborn-tests.yml:788-793`). No fix PR yet.
3. **[#6993](https://nearai/ironclaw Issue #6993) — Token accounting bug in `ModelWorkRequest::for_assistant`** — **P1 bug**: estimates input tokens from the *reference string length*, not the referenced content. Leads to wrong context-budget decisions, potentially causing premature or late compaction. **Fix in scope** of pi-harness program.
4. **[#6992](https://nearai/ironclaw PR #6992) — locale-sensitive `comm` in CI crate discovery** — CI can break under UTF-8 collation (`ironclaw_events` vs `ironclaw_event_streams` ordering). **Fix PR open** (pin `LC_ALL=C`).
5. **[#6986](https://nearai/ironclaw Issue #6986) — tool-array instability breaks prompt caching** — Mid-run promotion of deferred tools invalidates cached prefixes. **Fix PR #7001** (byte-stable prefix) is open but only addresses the prompt side, not the tool-array side.

## 6. Feature Requests & Roadmap Signals

- **OrcaRouter as built-in provider (#7009)** — simple, additive, likely to ship quickly; needs a community or core PR.
- **Live-canary Slack alerts on merge-queue failures (#7007)** — operational DX feature, currently a PR, likely to merge this week.
- **OOBE automation-tasks prototype (#6994 → backend wiring #6993)** — a UI-only prototype is open; the backend wiring issue signals this is a **planned product feature** for onboarding flows.
- **Deep-link register/install gateway + private manifest support (#6780)** — large PR that is a re-port of #5409 (by neo-sky), suggesting a previously-reviewed design being revived.

**Roadmap signal (pi-harness adoption, from #6984–#6990):** A coherent P0/P1 program to:
- Add explicit Anthropic `cache_control` breakpoints (**PR #6997** open)
- Keep the cached prompt prefix byte-identical (**PR #7001** open)
- Derive compaction budget from the actual model window (instead of hardcoded 128k)
- Prevent compaction inference from polluting prompt cache / session affinity
- Fix token accounting from content-reference strings

This is the **highest-value user-facing performance work** in flight — it directly targets latency and cost.

## 7. User Feedback Summary

- **External/user-facing pain points are scarce this week** — the activity is almost entirely internal architecture/CI work.
- **Performance is the loudest user-facing signal**: the libSQL p95 issue (#6974) and the session-affinity concern (#6990) are both framed around user experience (latency, cache efficiency).
- **First-run experience is being prototyped** (OOBE automation tasks, #6994), indicating product-team interest but no user feedback yet since it's mock-data UI.
- **Community pull toward new LLM providers** (OrcaRouter, #7009) suggests users want broader provider choice with first-class support instead of the generic fallback path.

## 8. Backlog Watch

| Item | Age | Why it matters | Status |
|---|---|---|---|
| **[#5598](https://nearai/ironclaw PR #5598) — "chore: release"** | Open since **July 3 (~30 days)** | Blocks shipping `ironclaw_common` 0.5.0 + `ironclaw_skills` 0.4.0 (both breaking). External users are still on old APIs. | Needs a maintainer decision to merge or close; appears deprioritized by the reborn wave. |
| **[#6780](https://nearai/ironclaw PR #6780) — deep-link register/install gateway** | Open since July 28 | Large, fully-designed feature (re-port of #5409) with no comments in last 24h; may be waiting on reborn refactor to land first. | Needs rebase/rerouting or explicit deferral. |
| **[#5981](https://nearai/ironclaw PR #5981) / [#5982](https://nearai/ironclaw PR #5982) — queued-message steering + budget approval gate** | Open since **July 11** | Large behavior features (XL) forward-ported onto current main, with turn-boundary races fixed. They are **stacked on each other** and may be blocked by the reborn wave ordering. | Needs maintainer review/merge decision; the changed-coverage gate issue (#7006) specifically documents why ~180 lines can't be integration-tested, which may be blocking this PR. |

---

**Overall health assessment:** Structurally sound — the project has strong CI-gate discipline, systematic defect tracking (issues that track checklist rows), and a clear architectural roadmap being executed in waves. The biggest risks are (1) the **CI roll-up false-red bug** eroding trust in the gates, (2) the **libSQL performance regression** going unfixed, and (3) **release starvation** while the refactor wave occupies all core bandwidth.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Date: 2026-08-02**

---

## 1. Today's Overview

LobsterAI is showing signs of a mature project entering a stabilization phase. Activity in the last 24 hours was moderate, with 7 issues updated (6 closed, 1 still open) and 2 pull requests updated (both still open, none merged). Notably, **all 6 closed issues were marked as `[stale]`** — issues that had been lingering since April without maintainer response, now automatically closed. This suggests either a backlog cleanup effort or, more concerningly, a period of reduced maintainer engagement with the community. No new releases were published during this window. The project has two long-pending PRs (`#1224` and `#2358`) that address real user pain points (i18n issues and silent failures) but remain unmerged — a signal worth watching for contributors.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The project appears to be between release cycles.

---

## 3. Project Progress

**No PRs were merged or closed** in the last 24 hours. However, two PRs remain open and represent pending progress:

| PR | Description | Status |
|---|---|---|
| [**#1224**](https://github.com/netease-youdao/LobsterAI/pull/1224) | Fixes i18n hardcoded Chinese strings, adds Escape key support to Agent modals, and prevents duplicate delete clicks | Open since April 1 — **needs review** |
| [**#2358**](https://github.com/netease-youdao/LobsterAI/pull/2358) | Shows localized feedback when session rename fails (fixes Issue #670) | Open since July 18 — **needs review** |

> ⚠️ **Health Signal**: PR #1224 has been open for over 4 months with no merge activity. This is a red flag for contributor retention.

---

## 4. Community Hot Topics

All 7 issues updated today were created on **April 1-2** and received exactly **2 comments** each — likely bot-driven stale markers rather than genuine community discussion. The most notable items:

| Issue | Topic | 🏷️ | Signal |
|---|---|---|---|
| [**#1293**](https://github.com/netease-youdao/LobsterAI/issues/1293) | Custom MCP via HTTP doesn't work in OpenClaw engine (**1 👍**) | 🐛 Bug | Real user pain — only SSE-based MCPs work |
| [**#1223**](https://github.com/netease-youdao/LobsterAI/issues/1223) | i18n hardcoding + UX issues in Agent modals | 🌐 i18n / UX | **Still open** — has a fix PR (#1224) waiting |
| [**#1296**](https://github.com/netease-youdao/LobsterAI/issues/1296) | 3MB long image upload crashes the page | 🐛 Bug | Reliability issue, no fix PR visible |

**Key takeaway**: No fresh community engagement today. The "hot" topics are all stale. The most technically significant issue remains **#1223**, which has a fix ready but waiting for maintainer action.

---

## 5. Bugs & Stability

All bug reports updated today are **stale-closed** (no fixes shipped). Ranked by severity:

| # | Issue | Severity | Status |
|---|---|---|---|
| 1 | [**#1296**](https://github.com/netease-youdao/LobsterAI/issues/1296) — 3MB image upload crashes page, blocks all new tasks | 🔴 **High** | Closed (stale, unfixed) |
| 2 | [**#1293**](https://github.com/netease-youdao/LobsterAI/issues/1293) — Custom HTTP MCP not registered in OpenClaw engine | 🟠 **Medium** | Closed (stale, unfixed) |
| 3 | [**#1298**](https://github.com/netease-youdao/LobsterAI/issues/1298) — Model rejects short input as "too long" | 🟠 **Medium** | Closed (stale, unfixed) |
| 4 | [**#1307**](https://github.com/netease-youdao/LobsterAI/issues/1307) — Cannot edit model provider config after closing panel | 🟡 **Low-Med** | Closed (stale, unfixed) |
| 5 | [**#1305**](https://github.com/netease-youdao/LobsterAI/issues/1305) — Scheduled task history shows wrong title after deletion | 🟡 **Low** | Closed (stale, unfixed) |

> ⚠️ **Health Signal**: These bugs were reported **4 months ago** and never fixed. While some may be low-priority, **#1296** (crash on image upload) is a serious UX blocker that users reported makes the app "整体不可用" (completely unusable).

---

## 6. Feature Requests & Roadmap Signals

Two feature-oriented items were updated today:

1. [**#1302**](https://github.com/netease-youdao/LobsterAI/issues/1302) — **Code block line number toggle** (feat: cowork)
   - User requested a `#` button in code block toolbars to toggle line numbers
   - Detailed spec provided with react-syntax-highlighter integration approach
   - *Status*: Closed as stale, no implementation tracked

2. [**#1223**](https://github.com/netease-youdao/LobsterAI/issues/1223) — **i18n + UX improvements** (still open)
   - Escape key support for Agent modals
   - Delete-button duplicate-click protection
   - *Status*: Fix PR ready but unmerged

> **Prediction**: If PR #1224 merges, the i18n and Escape-key UX improvements are likely to ship in the next minor release. The line-number feature (#1302) has no champion and is unlikely to be picked up without maintainer interest.

---

## 7. User Feedback Summary

The most vocal user pain points emerging from today's data:

- **MCP compatibility with OpenClaw engine** (#1293): Users expect custom HTTP-based MCP servers to work with the engine, but only SSE is supported. This limits integration flexibility.
- **Image upload reliability** (#1296): Users are hitting hard limits with large images, and the failure state is catastrophic (blocks all new tasks, requires page reset).
- **Model token limit misconfiguration** (#1298): Users report the app incorrectly flags short inputs as over-limit, suggesting a bug in token counting or context window configuration.
- **Silent failures in UI** (#2358 PR): Users report that renaming sessions fails without any feedback — a frustrating UX gap for something so basic.
- **Read-only config panels** (#1307): A workflow-blocking bug where model provider settings become uneditable after panel close.

**Satisfaction**: No positive feedback or thank-you comments observed in this window.

---

## 8. Backlog Watch

The following require maintainer attention:

| Item | Age | Why It Matters |
|---|---|---|
| [**PR #1224**](https://github.com/netease-youdao/LobsterAI/pull/1224) — i18n + UX fix | **4+ months open** | Ready-to-merge fix for 3 documented bugs; risk of contributor abandonment |
| [**PR #2358**](https://github.com/netease-youdao/LobsterAI/pull/2358) — Rename failure feedback | **2 weeks open** | Fixes Issue #670; small, focused, and clearly beneficial |
| [**Issue #1223**](https://github.com/netease-youdao/LobsterAI/issues/1223) — i18n/UX bug cluster | **4+ months open** | Directly linked to PR #1224; unresolved i18n issues affect international users |
| [**Issue #1296**](https://github.com/netease-youdao/LobsterAI/issues/1296) — Image upload crash | **4+ months, auto-closed** | Serious crash reported; should be reopened and triaged |

> 🚨 **Attention Needed**: The stale-closing sweep is masking unresolved issues. For a healthy project, these bugs should be either **fixed, deprioritized explicitly, or documented as known limits** — not silently closed by automation.

---

*Generated from GitHub data for netease-youdao/LobsterAI. All dates refer to UTC.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest
**Date:** 2026-08-02  
**Period:** 2026-08-01 – 2026-08-02

---

## 1. Today's Overview

Moltis maintained a steady pace over the last 24 hours with three pull requests updated and no new issues filed. Two PRs were successfully merged/closed, signaling active development progress, while one remains open for review. There were no new releases published during this window, suggesting the project is in an integration and stabilization phase following recent feature work. The absence of fresh bug reports is a positive sign for overall stability. The most notable development is the expansion of security controls (operators list) and the completion of telemetry/instrumentation infrastructure, both of which are foundational for scaling the platform.

---

## 2. Releases

**None.** No new versions or tags were published in the last 24 hours. The last known release predates this window. Users should monitor the [releases page](https://github.com/moltis-org/moltis/releases) for upcoming versions.

---

## 3. Project Progress

Two PRs were merged/closed, representing meaningful advancement:

- **[#1174 — Add instrumentation and feedback collection infrastructure](https://github.com/moltis-org/moltis/pull/1174)** *(merged)*: This substantial addition introduces backend-neutral agent instrumentation with Langfuse v4 export, operational OTLP backends, and end-user reaction feedback. Key features include immutable completion-only turns, streaming/non-streaming parity, provider failover attribution, cache-aware token usage, and reasoning support. This lays the groundwork for observability and user feedback loops.

- **[#1170 — Gate /sh and privileged tools behind a per-account operators list](https://github.com/moltis-org/moltis/pull/1170)** *(merged)*: This security hardening separates access from privilege by introducing an explicit per-account `operators` list. Previously, channel senders who passed an access allowlist could reach privileged commands and host tools. The new boundary is enforced across commands, callbacks, queue replay, chat execution, and external interfaces.

One PR remains open and in review:

- **[#1182 — Allow deleting and archiving the main session](https://github.com/moltis-org/moltis/pull/1182)** *(open)*: Fixes an issue where the `main` session could not be deleted or archived. The PR drops the `main` guard in `delete_impl` and `is_archivable_entry` while preserving the current-active-channel-session archive restriction and `sessions.clear_all` behavior.

---

## 4. Community Hot Topics

There are no issues with significant comment volume or reactions in this window; all three updated PRs have zero comments and zero reactions. Activity is primarily maintainer-driven:

- **[PR #1182](https://github.com/moltis-org/moltis/pull/1182)** — The most actively discussed item (only item) is the fix for main session deletion/archiving. While low on social signals, this addresses a concrete user pain point (issue #1132) regarding session management flexibility.

- **[PR #1174](https://github.com/moltis-org/moltis/pull/1174)** — The instrumentation merge is substantial and will enable future community-driven improvements based on telemetry data. Its size suggests a major architectural milestone.

The underlying need in the active PR is simple: users expect uniform session management regardless of session type, and the current restriction on the `main` session violated that expectation.

---

## 5. Bugs & Stability

**No new bugs reported today.** The open PR #1182 addresses a known limitation (not a crash-level bug) where `main` session deletion/archival was blocked. This is a minor functional restriction rather than a regression. Severity ranking:

1. *(Low)* **Session management limitation** — `main` session cannot be deleted/archived (fix PR #1182 open). No crashes or data loss involved.

No instability indicators were observed in the latest PRs (instrumentation tests appear comprehensive per the PR description).

---

## 6. Feature Requests & Roadmap Signals

No explicit user feature requests were filed in this window. However, signals from merged PRs point to the following roadmap direction:

- **Observability & Feedback Infrastructure (likely nearing GA):** PR #1174 adds instrumentation, Langfuse export, OTLP backends, and user reaction feedback. This strongly indicates the next release will include operational telemetry and product feedback collection as first-class features.

- **Security Model Maturation:** PR #1170's per-account operators list suggests the project is formalizing role-based access for multi-tenant or team deployments.

- **Session Management Flexibility:** The open PR #1182 signals a broader theme of reducing arbitrary restrictions in favor of user-controlled session lifecycles.

**Prediction:** The next version will likely bundle the instrumentation/feedback system along with the operators list security boundary. Expect a minor version bump (e.g., 0.x.0) reflecting new features rather than a patch.

---

## 7. User Feedback Summary

No direct user feedback (comments, 👍 reactions) was captured in this window. Indirect feedback inferred from the data:

- **Pain point (historical, #1132):** Users wanted to delete or archive the `main` session. Fix is in progress (PR #1182), indicating maintainers respond to reported session-management friction.

- **Security expectations:** The operators-list change (PR #1170) likely responds to user concerns about privileged access leakage through allowlisted channels. This suggests users are deploying Moltis in shared or semi-trusted environments.

- **Observability demand:** The substantial instrumentation PR (#1174) implies user requests for better debugging, token cost tracking, and feedback loops were accumulating.

Overall, user-driven changes are being addressed with relatively short turnaround (days to weeks), suggesting healthy responsiveness.

---

## 8. Backlog Watch

**No long-unanswered issues or PRs identified** in this window:

- The only open PR (#1182) was created 2026-08-01 and is actively in review (1 day old).
- All merged PRs were handled within the last 6 days.
- No issues remain open with stale timestamps.
- No PRs have been awaiting review for extended periods.

The maintainer team (notably `penso`) is actively processing contributions, and the backlog appears well-managed. No items require escalation.

---

*Report generated from public GitHub activity data for moltis-org/moltis on 2026-08-02.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date:** 2026-08-02  
**Project:** CoPaw (github.com/agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw shows **high activity** with 9 issues and 13 PRs updated in the last 24 hours, indicating a healthy, actively maintained project. The issue tracker is entirely open (9/9), with no closures today, while the PR pipeline shows strong forward motion with 12 open and 1 closed PR. A notable cluster of **first-time contributors** (4) submitted fixes addressing real bugs—a positive signal for community engagement and project accessibility. The project is processing ~2-3 community-reported bugs per day alongside ongoing feature development (provider unification, desktop UX improvements). No new releases were published today, but the substantial PR activity suggests a release may be forthcoming.

---

## 2. Releases

No new releases were published in the last 24 hours. The latest known version remains **QwenPaw 2.0.1** (referenced in issue reports).

---

## 3. Project Progress

**Merged/Closed PRs Today:**

- **[#6598](https://github.com/agentscope-ai/QwenPaw/pull/6598) [CLOSED]** — `fix(skills): preserve plugin-sourced skill tags across reconcile cycles (#6537)` by BlackBox-Labs. This fix prevents skill tags from disappearing after restart for plugin-sourced skills. A newer open PR ([#6632](https://github.com/agentscope-ai/QwenPaw/pull/6632)) suggests a re-iteration or follow-up was needed.

**Key Open PRs Advancing Features & Fixes:**

| PR | Description | Status |
|---|---|---|
| [#6632](https://github.com/agentscope-ai/QwenPaw/pull/6632) | Skill tag preservation fix (revised approach) | Open |
| [#6631](https://github.com/agentscope-ai/QwenPaw/pull/6631) | Aligns Aliyun coding plan models with official docs | Open |
| [#6629](https://github.com/agentscope-ai/QwenPaw/pull/6629) | Triggers summarize on auto-compression when enabled | Open |
| [#6628](https://github.com/agentscope-ai/QwenPaw/pull/6628) | Uses SystemMsg for compressed memory placeholder (fixes HTTP 400 for DeepSeek) | Open |
| [#6630](https://github.com/agentscope-ai/QwenPaw/pull/6630) | Reports empty model responses to user instead of silent failure | Open |
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) | Unifies provider discovery, model metadata, routing — **large architectural change** | Open |

**Architecture/Feature PRs:**

- **[#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)** — Unifies provider discovery, model metadata, routing, and agent controls. This is a significant architectural improvement for #6167, keeping discovered candidates separate from configured models.
- **[#6622](https://github.com/agentscope-ai/QwenPaw/pull/6622)** (first-time contributor) — Adds **OrcaRouter** as a built-in provider (model router speaking native OpenAI chat.completions).
- **[#5490](https://github.com/agentscope-ai/QwenPaw/pull/5490)** — Shows tool-card images inline with gallery navigation in the console chat.
- **[#6306](https://github.com/agentscope-ai/QwenPaw/pull/6306)** — Adds a workspace shortcut to the sidebar for desktop users.

---

## 4. Community Hot Topics

**Most Discussed Issues (2+ comments):**

1. **[#6593](https://github.com/agentscope-ai/QwenPaw/issues/6593) [Feature]** — 增加统一且专业的qwenapw专用清理页面 (Unified cleanup page for QwenPaw; comments: 2)  
   *Author request: A dedicated UI to clean up accumulated agent data (auto-memory, tool outputs, session files) with manual + automated options.*

2. **[#6480](https://github.com/agentscope-ai/QwenPaw/issues/6480) [Question]** — 运行nohup命令agent都会卡住 (Agent hangs when running `nohup`/`&` commands; comments: 2)  
   *The `execute_shell_command` tool never returns to idle when processes are detached.*

3. **[#6568](https://github.com/agentscope-ai/QwenPaw/issues/6568) [Feature]** — 全局快捷键唤出浮动快速输入框 (Global hotkey for floating quick-input box; comments: 2)  
   *Similar to 豆包 (Doubao)/Raycast — lightweight input without opening the full 1280×800 main window.*

**Analysis:** The most active threads reveal two key community needs: (a) **data lifecycle management** for long-running agents, and (b) **low-friction interaction patterns** (quick input, instant cleanup). The `nohup` hang is a functional blocker affecting real workflows.

---

## 5. Bugs & Stability

**Reported Today, Ranked by Severity:**

| Issue | Severity | Description | Fix PR? |
|---|---|---|---|
| [#6619](https://github.com/agentscope-ai/QwenPaw/issues/6619) | **Critical** | `ToolCallBlock` has no field `extra_content` — crashes every streaming request with Gemini tool calls (verified, root-caused) | ✅ [#6620](https://github.com/agentscope-ai/QwenPaw/pull/6620) |
| [#6625](https://github.com/agentscope-ai/QwenPaw/issues/6625) | **High** | `delegate_external_agent` returns "completed without text output" when notifications race prompt response (ACP) | ✅ [#6623](https://github.com/agentscope-ai/QwenPaw/pull/6623) |
| [#6626](https://github.com/agentscope-ai/QwenPaw/issues/6626) | **Medium** | CI gate strips fenced Evidence blocks entirely (porting deviation from openclaw) — blocks PRs with terminal transcripts | ⚠️ No fix yet |
| [#6624](https://github.com/agentscope-ai/QwenPaw/issues/6624) | **Medium** | Auto-compression (Scroll) doesn't trigger `summarize_when_compact` memory flow; manual `/compact` works | ✅ [#6629](https://github.com/agentscope-ai/QwenPaw/pull/6629) |
| [#6480](https://github.com/agentscope-ai/QwenPaw/issues/6480) | **Medium** | `nohup`/`&` commands cause agent to hang indefinitely | ⚠️ No fix yet |

**Notable:** All reported bugs today have corresponding fix PRs except for the CI evidence-fencing issue and the `nohup` hang. Response time from PR creation to issue filing appears to be **same-day** for multiple cases.

---

## 6. Feature Requests & Roadmap Signals

**Active Requests:**

1. **[#6593](https://github.com/agentscope-ai/QwenPaw/issues/6593)** — Unified, professional cleanup page with manual + automated cleaning. *High value for long-running deployments.*
2. **[#6568](https://github.com/agentscope-ai/QwenPaw/issues/6568)** — Global hotkey floating quick-input box (豆包/Raycast-style). *Low friction interaction for desktop.*
3. **[#6621](https://github.com/agentscope-ai/QwenPaw/issues/6621)** — Multi-agent collaboration guidance: Default Agent doesn't auto-invoke other agents without explicit PROFILE.md instructions. Users want either auto-discovery or better onboarding.

**Predictions for Next Version:**

- **OrcaRouter as built-in provider** — PR is ready and small; likely to land soon ([#6622](https://github.com/agentscope-ai/QwenPaw/pull/6622)).
- **Summary on auto-compression** — Fix PR is ready; pairs with ongoing memory-system improvements ([#6629](https://github.com/agentscope-ai/QwenPaw/pull/6629)).
- **Provider/model unification** — Large architectural PR ([#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302)) is a signal that provider management will see a major UX overhaul in an upcoming release.
- **Cleanup UI** is highly requested but no implementation signals yet — likely a future milestone.

---

## 7. User Feedback Summary

**Pain Points:**

- **Data sprawl:** Users report agent data accumulating uncontrollably (memory, tool outputs, backups) with no easy way to clean up. "qwenapw会混乱不堪加大的空间占用" — becomes chaotic with large space usage ([#6593](https://github.com/agentscope-ai/QwenPaw/issues/6593)).
- **Interaction friction:** Opening the full 1280×800 window for simple questions is "太重" (too heavy) — users want instant access like Raycast ([#6568](https://github.com/agentscope-ai/QwenPaw/issues/6568)).
- **Discoverability gap:** One user spent 50+ multi-agent conversations before discovering that Default Agent doesn't auto-invoke other agents — documentation exists but was insufficient ([#6621](https://github.com/agentscope-ai/QwenPaw/issues/6621)).
- **Background process hangs:** `nohup` commands blocking agent execution is a real workflow blocker for shell-heavy users ([#6480](https://github.com/agentscope-ai/QwenPaw/issues/6480)).

**Positive Signals:**

- Explicit mention that "手动 `/compact` 可以触发" (manual trigger works) — suggesting core memory flow works when invoked correctly.
- Community members are contributing fixes rather than just filing bugs — 4 first-time contributors this week with substantive fixes.
- Users are actively reading official docs (the multi-agent docs are cited explicitly).

---

## 8. Backlog Watch

| Item | Age | Status | Attention Needed |
|---|---|---|---|
| [#5490](https://github.com/agentscope-ai/QwenPaw/pull/5490) — Inline tool-card images with gallery | 39 days | Open, no review comments | Features UI improvement; needs maintainer review |
| [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) — Provider discovery unification | 12 days | Open, active | **Large architectural change**; will impact all users — needs careful review |
| [#6306](https://github.com/agentscope-ai/QwenPaw/pull/6306) — Desktop workspace shortcut | 12 days | Open | Simple UX win; low-risk merge candidate |
| [#6480](https://github.com/agentscope-ai/QwenPaw/issues/6480) — `nohup` hang | 7 days | Open, no fix PR | **Functional blocker** for shell-heavy users; needs maintainer triage |
| [#6626](https://github.com/agentscope-ai/QwenPaw/issues/6626) — CI evidence gate strips fenced blocks | 1 day | Open, no fix | Blocking PRs with terminal transcripts; **CI infrastructure issue** |

**Maintainer Action Priority:**
1. Triage [#6480](https://github.com/agentscope-ai/QwenPaw/issues/6480) (`nohup` hang) — impacts core shell tool reliability.
2. Review [#6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) (provider unification) — large diff, likely needs design review.
3. Fix/confirm [#6626](https://github.com/agentscope-ai/QwenPaw/issues/6626) (CI evidence gate) — blocking contributor PRs.
4. Review stale PRs [#5490](https://github.com/agentscope-ai/QwenPaw/pull/5490) and [#6306](https://github.com/agentscope-ai/QwenPaw/pull/6306) — both ready for low-risk merges.

---

**Overall Health Assessment:** CoPaw is in a **healthy, active state** with strong community engagement, same-day fix PRs for high-priority bugs, and a growing contributor base. The main risks are the `nohup` hang (no fix yet) and the CI evidence-gate issue potentially frustrating contributors. The large provider-unification PR suggests significant architecture investment ahead.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the GitHub data from ZeroClaw (github.com/zeroclaw-labs/zeroclaw), here is the project digest for **2026-08-02**.

---

# 📋 ZeroClaw Project Digest — 2026-08-02

## 1. Today's Overview
ZeroClaw is in a period of intense design and security hardening, evidenced by 50 active issues and 50 open PRs updated in the last 24 hours. The majority of the most-discussed issues are high-risk RFCs targeting the upcoming v0.9.0 security architecture, specifically focusing on credential boundaries, memory lifecycle separation, and inbound authentication. While there are no new releases today, the pull request queue is massive and feature-rich, with major implementations for desktop computer-use control, an eval suite, and secure relay transport waiting for review or author action. The project shows healthy momentum but a significant bottleneck in maintainer review capacity, as most PRs are flagged with `needs-author-action` or are pending decision.

## 2. Releases
- **Current Version:** None published in the last 24 hours.
- **Note:** PR [#9648](https://github.com/zeroclaw-labs/zeroclaw/pull/9648) is a release chore bumping the version to **v0.8.4**. It is currently open and flagged with a critical warning that the translation `v0.8.4` tag must be corrected before publication.

## 3. Project Progress
- **Merged/Closed PRs:** 0 merged or closed in the last 24 hours.
- **Closed Issues:** 3 issues were closed, including:
  - [#8568](https://github.com/zeroclaw-labs/zeroclaw/issues/8568): RFC for a Mixture-of-Agents (MoA) virtual model provider (closed).
  - [#9550](https://github.com/zeroclaw-labs/zeroclaw/issues/9550): Documentation fix for a broken LinkedIn link (closed).

## 4. Community Hot Topics
The community is heavily focused on architecture and security RFCs, with the most active discussions being:

- **Memory Architecture Split:** [#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048) (16 comments) proposes separating conversation history from long-term memory. Related issue [#9103](https://github.com/zeroclaw-labs/zeroclaw/issues/9103) (10 comments) suggests decoupling authoritative storage from enrichment connectors.
- **Key Management & Auth:** [#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127) (13 comments) proposes an abstraction for master-key material sources. [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) (8 comments) discusses pluggable inbound authentication.
- **Interoperability:** [#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) (12 comments) requests an OpenAI Chat Completions compatibility adapter to allow external clients like Open WebUI to connect.
- **Safety & Control:** [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) (11 comments) proposes a tiered approval system for high-risk shell commands (allow/ask/deny), similar to Claude Code.

**Underlying Need:** The community is pushing for ZeroClaw to be more modular and secure, preparing it for enterprise deployment by separating concerns (memory, security, auth) and improving observability. These are not bug reports but foundational design discussions for v0.9.0.

## 5. Bugs & Stability
Several high-severity bugs were reported, mostly centered around security and channel integrity:

- **WhatsApp Group Permissions Bypass (S1 Critical):** [#9348](https://github.com/zeroclaw-labs/zeroclaw/issues/9348) – A security vulnerability where the WhatsApp Web channel answers every DM and group under `business` mode, ignoring the configured allowlist. **Fix RFC:** [#9397](https://github.com/zeroclaw-labs/zeroclaw/issues/9397) proposes changing the default behavior to treat an empty `allowed_groups` as deny-all (permit-none).
- **Cron Job Output Loss (S2 High):** [#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340) – CLI-created cron jobs are hardcoded to `delivery.mode = "none"`, meaning scheduled outputs are discarded silently without error.
- **Approval Token Leak (S2 High):** [#9417](https://github.com/zeroclaw-labs/zeroclaw/issues/9417) – The WhatsApp Cloud API transport leaks a live approval token on send failure or cancellation.
- **Telegram Group Handling:** PR [#9634](https://github.com/zeroclaw-labs/zeroclaw/pull/9634) addresses a fix to skip unauthorized handlers for non-mentioned group messages when `mention_only` is set.

## 6. Feature Requests & Roadmap Signals
The majority of active work is targeting the **v0.9.0 security architecture**. Key signals for the next release include:

- **Desktop Automation:** PR [#9091](https://github.com/zeroclaw-labs/zeroclaw/pull/9091) adds native macOS, Linux X11, and Windows drivers for a `computer_use` tool, addressing the long-standing RFC [#6909](https://github.com/zeroclaw-labs/zeroclaw/issues/6909).
- **Relay Security:** PR [#9080](https://github.com/zeroclaw-labs/zeroclaw/pull/9080) introduces a secure transport with mutual TLS for remote relay connections.
- **Evaluation Suite:** A series of PRs by `IftekharUddin` ([#9221](https://github.com/zeroclaw-labs/zeroclaw/pull/9221), [#9222](https://github.com/zeroclaw-labs/zeroclaw/pull/9222), [#9223](https://github.com/zeroclaw-labs/zeroclaw/pull/9223)) are building a robust eval framework with regression gating, JUnit XML reports, and LLM-judge grading.

## 7. User Feedback Summary
- **Pain Points:** Users are expressing frustration with overly complex configuration defaults that can lead to security risks (e.g., WhatsApp permissiveness). There is clear demand for "secure-by-default" behavior.
- **Cost Optimization:** [#9631](https://github.com/zeroclaw-labs/zeroclaw/issues/9631) highlights that users are spending too much money on OpenRouter due to a lack of prompt caching support, desires a stable `session_id` to be sent.
- **Usability:** The large number of `needs-author-action` PRs (e.g., [#9319](https://github.com/zeroclaw-labs/zeroclaw/pull/9319), [#8985](https://github.com/zeroclaw-labs/zeroclaw/pull/8985)) suggests that contributors are awaiting feedback or changes, which could indicate a slowdown in community momentum if not addressed.
- **Interoperability:** The high interest in the OpenAI-compatible adapter ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) indicates users want to integrate ZeroClaw with existing, popular front-ends rather than being locked into the built-in UI.

## 8. Backlog Watch
Many high-priority RFCs have been waiting for maintainer review for over a month:

- **Security & Auth Stack:**
  - [#7155](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) (Shell command confirmation tiers, created Jun 3)
  - [#6971](https://github.com/zeroclaw-labs/zeroclaw/issues/6971) (Security UX, created May 27)
  - [#7142](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) (Security decision pipeline, created Jun 3)
  - [#6996](https://github.com/zeroclaw-labs/zeroclaw/issues/6996) (Granular sandbox policy, created May 28)
- **Feature Set:**
  - [#7100](https://github.com/zeroclaw-labs/zeroclaw/issues/7100) (Per-model capability config, created Jun 2, priority p1)
  - [#6850](https://github.com/zeroclaw-labs/zeroclaw/issues/6850) (Memory policy decoupling, created May 22)

These items are tagged with `needs-maintainer-review` and have been active for over a month. The backlog of these large RFCs is the primary bottleneck for the v0.9.0 milestone.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*