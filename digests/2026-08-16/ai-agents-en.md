# OpenClaw Ecosystem Digest 2026-08-16

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-16 00:31 UTC

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

Based on the provided GitHub data for OpenClaw, here is the project digest for 2026-08-16.

---

### 1. Today's Overview

OpenClaw shows high activity with 500 issues and 500 PRs updated in the last 24 hours, indicating a very active development and maintenance cycle. However, the project health is mixed: there are many open bug reports (~446 open PRs) and a large backlog of issues tagged `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`, suggesting a bottleneck in maintainer capacity. Critical, recurring bugs related to message loss, session-state corruption, and subagent reliability remain prominent, though active PRs are attempting to address them. A single new beta release (`v2026.8.1-beta.2`) was published today, highlighting on-going security work but with release notes that are truncated. The community is highly engaged, but the volume of open, high-priority issues is a significant concern for long-term stability.

### 2. Releases

- **v2026.8.1-beta.2** ([Link](https://github.com/openclaw/openclaw/releases)): Released today, this beta version includes:
    - **Secret egress host binding:** A security enhancement to bind shared-store secrets to exact HTTPS destination hosts, preventing unbound sentinel substitution before plaintext egress.
    - **GPT-5.6 Ultra and runtime switching:** Mentions support for a new model and runtime switching capabilities, though details are incomplete.

### 3. Project Progress

Today saw 54 merged/closed PRs, with work focusing on stability, security, and developer experience. Key close-outs and improvements include:

- **Security Enhancements:** Two significant security PRs were closed today: [#116489](https://github.com/openclaw/openclaw/pull/116489) "feat(security): require acknowledgement for install policy warnings" and [#120900](https://github.com/openclaw/openclaw/pull/120900) "feat(ui): review install policy warnings". This introduces a new workflow for reviewing suspicious plugin or skill installs.
- **UI Fixes:** A PR was closed to fix handling of blank required strings in the Control UI update readers ([#124264](https://github.com/openclaw/openclaw/pull/124264)).
- **Workflow Improvements:** A PR to improve typechecking to fail instead of hanging forever when the compiler wedges was approved ([#123975](https://github.com/openclaw/openclaw/pull/123975)).

### 4. Community Hot Topics

The most active community discussions center on critical bugs that impact user trust and data integrity.

- **Recurring Silent Reply Failures:** [Issue #121058](https://github.com/openclaw/openclaw/issues/121058) (96 comments) remains the top topic. Users are frustrated that a previously closed issue has resurfaced. Underlying need: **absolute reliability in message delivery**.
- **Realtime Voice State Leak:** [Issue #116201](https://github.com/openclaw/openclaw/issues/116201) (66 comments) discusses unbounded state retention in voice sessions, indicating a need for **resource limits and robustness in long-running, real-time processes**.
- **Memory Trust Tagging:** [Issue #7707](https://github.com/openclaw/openclaw/issues/7707) (53 comments) is a long-standing feature request to tag memory by source to prevent poisoning, showing a strong community desire for **improved security and trust in agent memory**.
- **Text Leak Between Tool Calls:** [Issue #25592](https://github.com/openclaw/openclaw/issues/25592) (49 comments, 1 👍) is a high-severity UX bug where internal processing output is sent to messaging channels. The underlying need is for **cleaner, more intentional user-facing communication**.

### 5. Bugs & Stability

The bug landscape is dominated by P1 issues, many of which are regressions or long-standing problems that are hard to fix.

- **Critical (P1) - Widespread & Recurring:**
    - **Silent Reply Failures** ([#121058](https://github.com/openclaw/openclaw/issues/121058)): Still an unresolved, top-voted issue with no fix PR.
    - [**#91009**](https://github.com/openclaw/openclaw/issues/91009): CPU-bound `openclaw-hooks` processes stalling the gateway RPC, with 2 👍 and no fix PR.
    - [**#86684**](https://github.com/openclaw/openclaw/issues/86684): A regression where a yield parent branch is compacted at low context usage, causing potential data loss.
- **High (P1) - Specific Channel/Integration Failures:**
    - [**#41744**](https://github.com/openclaw/openclaw/issues/41744): Feishu image tool loses media before outbound delivery.
    - [**#90098**](https://github.com/openclaw/openclaw/issues/90098): Large attachment handling causes stack overflows in Control UI and gateway, with a linked open PR.
    - [**#94939**](https://github.com/openclaw/openclaw/issues/94939): State migration leaves channel conversation store empty, breaking MS Teams sends.
- **Moderate (P2) - Regressions and Performance:**
    - [**#85844**](https://github.com/openclaw/openclaw/issues/85844): Auto-update leaves stale bundle imports in the running gateway, leading to crashes.
    - [**#91223**](https://github.com/openclaw/openclaw/issues/91223): The `active-memory` plugin collapses prompt cache hit rate from 99.9% to 22%, a major performance regression.

### 6. Feature Requests & Roadmap Signals

Several long-standing feature requests continue to generate discussion, indicating strong roadmap signals.

- **Memory Trust Tagging** ([#7707](https://github.com/openclaw/openclaw/issues/7707)): This request has 53 comments over ~6 months. With the recent security-focused updates in `v2026.8.1-beta.2`, this feature addressing memory poisoning is a likely candidate for a future major release.
- **Graceful Subagent Timeouts** ([#6625](https://github.com/openclaw/openclaw/issues/6625)): This old request for pre-timeout warnings is a companion to the many active subagent reliability bugs.
- **Per-Agent TTS/STT Configuration** ([#66252](https://github.com/openclaw/openclaw/issues/66252)): As OpenClaw moves beyond a single-agent use case, per-agent configuration for multi-language support is a logical next step.
- **YAML Config Support** ([#45758](https://github.com/openclaw/openclaw/issues/45758)): A popular request (2 👍) for usability improvements, though an enhancement in this area may be deprioritized in favor of bug fixes.

### 7. User Feedback Summary

The sentiment is a mixture of frustration and concern over reliability, mixed with appreciation for the project's direction.

- **Pain Points: The biggest dissatisfaction is centered on silent failures and data loss.** Users are repeatedly hitting instances where subagent results are lost, replies are not delivered, or state is corrupted. This is eroding trust in the system for critical tasks.
- **Frustration with Recurrence:** The top issue ([#121058](https://github.com/openclaw/openclaw/issues/121058)) explicitly notes that a "closed" bug is still happening, leading to user frustration about the stability of the development cycle.
- **Security & Control Needs:** Users are proactively asking for security features like memory trust tagging and a test-fallback command, showing a desire for more granular control and a security-first mindset.

### 8. Backlog Watch

A significant number of issues are tagged with `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`. These appear to be "stuck" in the process.

- **Critical Long-Standing P1s:** Issues like [**#25592**](https://github.com/openclaw/openclaw/issues/25592) (Text leak between tool calls, created 2026-02-24) and [**#44925**](https://github.com/openclaw/openclaw/issues/44925) (Subagent completion silently lost, created 2026-03-13) are high-severity, high-comment issues that have been open for ~6 months without a clear path forward. Flagged as `needs-product-decision`, they are waiting on product strategy rather than technical solutions.
- **Security/Poisoning:** [**#7707**](https://github.com/openclaw/openclaw/issues/7707) (Memory Trust Tagging) is a critical feature request from a security standpoint that is stuck in `needs-maintainer-review` and `needs-product-decision`. Given the recent security emphasis in the latest release, prioritizing this decision would be a strong signal to the community.
- **General Trend:** The overwhelming number of `needs-maintainer-review` tags suggests that the team is struggling to keep up with the volume of community-submitted issues and PRs. This creates a bottleneck where good feedback and fixes may be delayed or lost.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-16
**Scope:** 11 Personal AI Assistant / Agent Open-Source Projects

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is rapidly bifurcating into two distinct camps: mature, high-activity platforms (OpenClaw, ZeroClaw, IronClaw, NanoBot) that are stabilizing core architectures while addressing production-scale concerns, and early-stage or niche-focused projects (PicoClaw, NullClaw, TinyClaw, ZeptoClaw) that are either in maintenance windows or early adoption phases. Across all projects, three universal themes dominate: **memory reliability and trust** (poisoning prevention, consolidation loss, cross-session context), **channel connectivity as a first-class concern** (Telegram, WhatsApp, WeChat, Slack, Matrix), and **security hardening** (credential boundaries, approval gates, secret egress controls). The ecosystem is actively converging on the OpenClaw architecture as a de facto reference standard, with derivative projects adopting its session model, plugin system, and gateway architecture while differentiating on specific channels or deployment footprints.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | PRs Merged/Closed | Release Status | Health Score |
|---------|---------------------|-------------------|-------------------|----------------|--------------|
| **OpenClaw** | 500 | 500 | 54 | Beta (v2026.8.1-beta.2) | ⚠️ High activity, critical P1 backlog |
| **ZeroClaw** | 50 | 50 | 6 | No new release | ✅ Active, RFC-heavy, robust CI |
| **Hermes Agent** | 50 | 50 | 0 | Stable (v0.20.1) | ✅ Fast iteration, security focus |
| **NanoBot** | 5 (est.) | 16 | 7 | None (patch imminent) | ✅ Healthy, WebUI maturation |
| **CoPaw** | 10 | 11 | 0 | Stable (v2.1.0) | ✅ Active contribution phase |
| **IronClaw** | 27 | 12 | 5 | None | ✅ Strong engineering phase |
| **Moltis** | 0 | 6 | 3 | None | ✅ Steady, focused |
| **LobsterAI** | 18 | 4 | 2 | None | ⚠️ Stable but quiet, backlog cleanup |
| **NanoClaw** | 0 | 22 | 1 | None | ⚠️ Productive but 19 PRs awaiting review |
| **PicoClaw** | 0 | 0 | 0 | None | ⚠️ Stalled, 2 stale PRs |
| **NullClaw** | 1 | 1 | 0 | None | ⚠️ Low-activity maintenance |
| **TinyClaw** | 0 | 0 | 0 | None | — No activity |
| **ZeptoClaw** | 0 | 0 | 0 | None | — No activity |

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Community scale is unmatched** — 500 issues and 500 PRs updated in 24h dwarfs ZeroClaw (50/50) and Hermes Agent (50/50), representing roughly 10x the community engagement of its nearest competitors.
- **Core reference architecture** — OpenClaw's gateway/hooks/session model is the de facto standard that derivative projects (NanoClaw, PicoClaw, LobsterAI) explicitly target for compatibility.
- **Feature depth** — GPT-5.6 Ultra support, secret egress host binding, install policy warnings, and subagent reliability work demonstrate a breadth unmatched by peers.

**Technical Approach Differences:**
- OpenClaw uses a **plugin/skill ecosystem with clawsweeper maintainer triage** (which is both a strength for community participation and a weakness — the maintainer queue is a recognized bottleneck).
- ZeroClaw uses a **rigorous RFC lifecycle with maintainer decision tracking** (#8692), showing a more formal governance model.
- IronClaw focuses on **database write-amplification elimination** and unbound-turns prepared-context — a performance-engineering angle OpenClaw has not emphasized.

**Community Size & Capacity Concerns:**
- OpenClaw's backlog is concerning: 446 open PRs, critical issues (silent reply failures #121058 with 96 comments) unresolved for months, and significant `needs-maintainer-review` and `needs-product-decision` backlogs. This suggests community demand is outpacing maintainer capacity.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Memory Trust & Integrity** | OpenClaw (#7707 memory poisoning), NanoBot (#5377 consolidation loss), Hermes Agent (#8457 persistent memory), LobsterAI (#2046 memory architecture) | Source-tagged memory, lossless consolidation, cross-session search, poisoning prevention |
| **Multi-Channel Reliability** | OpenClaw (Feishu image loss #41744), PicoClaw (WhatsApp 405), CoPaw (WeChat/Matrix), NanoClaw (Telegram, Discord), LobsterAI (WeChat IM) | Native protocol parity, attachment handling, sanitizer correctness, reconnect mechanisms |
| **Security & Credential Boundaries** | OpenClaw (secret egress binding), Hermes Agent (CLI approval panel #87183, dangerous-command bypass #84551), ZeroClaw (webhook audit leaks #9995, fail-open risk #9753), IronClaw (credential boundaries RFC #6971), LobsterAI (email path traversal #1885) | Unambiguous approval gates, credential egress controls, audit hygiene |
| **Session Lifecycle & State** | NanoBot (stale saves after `/new` #5271), OpenClaw (session-state corruption), Hermes Agent (session identity #82001), ZeroClaw (runtime-owned sessions #9487) | Atomic saves, cursor correctness, detach vs. delete semantics, viewer vs. owner disconnects |
| **Context Caching & Token Efficiency** | PicoClaw (#3321 prefix caching), NullClaw (#987 cache-friendly prompts), OpenClaw (active-memory plugin collapsing cache hit rate #91223), IronClaw (prepared-context turns) | Stable prompt prefixes, dynamic context placement, cache hit-rate preservation |
| **Long-Running Task Resilience** | OpenClaw (subagent reliability), Hermes Agent (slow local models #87292), NanoClaw (heartbeat stalls #3251), ZeroClaw (cron job timeout #9320) | Graceful timeouts, heartbeat robustness, liveness vs. stuck-container detection |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target Users | Architectural Standout |
|---------|--------------|--------------|----------------------|
| **OpenClaw** | Full-featured personal AI assistant, multi-channel gateway | Power users, individual agent operators | Plugin/skill ecosystem; clawsweeper triage model |
| **ZeroClaw** | Standardized, RFC-driven agent platform | Enterprise/complex deployments | Rigorous RFC lifecycle; SOP (Standard Operating Procedures) capability; security-posture focus |
| **IronClaw** | High-performance agent runtime | Production/large-scale operators | Write-amplification elimination; unbound-turns prepared-context; trajectory benchmarking |
| **Hermes Agent** | Desktop-first agent with Windows focus | Desktop/Mac/Windows users | Desktop app with messaging gateway integration; session groups |
| **NanoBot** | Multi-session collaborative WebUI workspace | Team collaboration, workflow users | Side conversations, drag-and-drop session organization, session mentions |
| **CoPaw** | Qwen/Data apps, B2B Chinese-market focus | Chinese-speaking enterprises | Native DataPaw app runtime; Matrix/WeChat integration; plugin permission system |
| **NanoClaw** | Lightweight multi-agent groups | Developers running scaled container fleets | Cross-session context propagation; channel-registration interception seams |
| **LobsterAI** | OpenClaw-compatible GUI/frontend | Non-technical users of OpenClaw | Config sync preservation; cron yield finalization; OpenClaw integration reliability |
| **Moltis** | Integration hub (calendar, email, Slack) | Productivity-focused users | Durable connectors; Slack native task cards; ephemeral Coder sandboxes |
| **PicoClaw** | Lightweight/embedded agents | Resource-constrained deployments | Minimal activity; WhatsApp dependency fix pending |
| **NullClaw** | Zig-based local agent runtime | Optimized local execution | Tool-output compression; cache-friendly prompt architecture |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating (High Velocity, High Volume):**
- **OpenClaw**, **ZeroClaw**, **Hermes Agent** — All showing 50-500 issues/PRs updated in 24h with substantial merged work. These are the ecosystem's innovation engines.

**Tier 2 — Actively Maturing (Medium-High Velocity):**
- **NanoBot**, **IronClaw**, **CoPaw** — Steady commits, clear strategic direction (WebUI workspace, performance engineering, B2B features respectively). IronClaw's discipline (all 12 perf issues closed) is exceptional.

**Tier 3 — Stabilizing / Maintenance (Low-Medium Velocity):**
- **LobsterAI**, **NanoClaw**, **Moltis** — Performing targeted fixes and backlog cleanup. NanoClaw has strong contributor gravity (19 open PRs) but is becoming a review bottleneck.

**Tier 4 — Quiet / Stalled:**
- **PicoClaw**, **NullClaw**, **TinyClaw**, **ZeptoClaw** — Minimal or zero activity. PicoClaw's two stale PRs (WhatsApp fix and prefix caching) are blocking real improvements.

---

## 7. Trend Signals

1. **Memory is the next trust frontier.** Multiple projects are acknowledging that conversation history is not safe from corruption, loss, or poisoning. The convergence on **source-tagged memory** (OpenClaw #7707, NanoBot #5377, Hermes Agent #8457) and **lossless consolidation** signals that users will demand bit-perfect persistence. Value for developers: architect memory as append-only with cursor semantics, not mutable state.

2. **Protocol-level interoperability is becoming a differentiator.** ZeroClaw's Chat Completions profile RFC (#8603) and OpenClaw's runtime switching are early moves toward **standardized agent APIs** that work with existing LLM clients (Open WebUI, LobeChat, Continue.dev). The ecosystem is converging on OpenAI-compatible APIs as the interop layer.

3. **Channel delivery is the weakest link in production confidence.** WhatsApp (PicoClaw), WeChat (LobsterAI), Feishu (OpenClaw), and Discord (NanoClaw) all show either broken or degraded native integrations. **Channel connectivity is infrastructure, not a feature** — the projects that treat it as such will win deployment trust.

4. **Performance engineering is moving from "nice-to-have" to "operational necessity."** IronClaw's write-amplification campaign, PicoClaw's prefix caching, NullClaw's tool-output compression, and OpenClaw's cache-hit-rate regression (#91223) all point to **token efficiency and database durability as hard requirements** for production agent fleets.

5. **Security postures are hardening from "trust the model" to "inspect the boundary."** The recurring themes — approval gates (Hermes Agent #87183), dangerous-command detection bypass (#84551), credential egress control (OpenClaw beta), audit hygiene (ZeroClaw #9995) — indicate that **unambiguous security contracts** are the new compliance bar for agent platforms.

6. **Multi-agent / multi-session collaboration is the next feature battleground.** NanoBot (#5358 session mentions), NanoClaw (#3257 cross-session context), Hermes Agent (#87297 session groups), and CoPaw (background task callbacks #7056) are all building toward **agents that collaborate with each other and with users across persistent identities**.

7. **CI/CD test flakiness is eroding trust across projects.** IronClaw's canary 30/30 red due to harness bugs (#7679), ZeroClaw's ETXTBSY test flake (#9965), and OpenClaw's OpenClaw-hooks stalls (#91009) all highlight that **harnest quality is now a product feature** — it directly impacts developer perception of reliability.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-16

## 1. Today's Overview

NanoBot shows a high-velocity, healthy development cycle with 16 PRs updated in the last 24 hours and a strong 7:9 closed-to-open ratio, indicating sustained merge momentum. The project is clearly in a maturation phase, with core stability work dominating: session persistence safety (#5271), consolidation memory preservation (#5379), and plugin cache revalidation (#5369) all shipped. The WebUI is the most active collaboration surface, with substantial UX work landing on session organization, side conversations, and connection resilience — a signal that the product is moving beyond core agent functionality toward a polished multi-session workspace. One bug was closed today (#5368, WebUI actions hidden during active turns) and one remains open (#5377, consolidation truncation), with fix PRs available for both. Zero new releases were published, despite the rapid fix cadence, suggesting a consolidated release may be imminent.

## 2. Releases

No new releases were published in the last 24 hours. Projects tracking the `main` branch are receiving the merged fixes directly. Given the volume and cross-cutting nature of merged fixes (session lifecycle, plugin security, WebUI interaction stability), a patch release (likely 0.3.x) consolidating changes from merged PRs #5369, #5370, #5371, #5376, and #5397 is expected within days — these all touch distinct subsystems and no breaking changes appear imminent.

## 3. Project Progress

Seven PRs were merged/closed in the last 24 hours, spanning platform integrity, WebUI UX, and developer experience:

- **Session & File State Lifecycle** — #5370 (merged) bounds per-session `FileStateStore` retention, fixing unbounded memory growth with high-cardinality session keys. Lifecycle-boundary cleanup after `/new` and SDK calls is now guaranteed.
- **Plugin Security** — #5369 (merged) closes a security gap where cached plugin skill roots could retain read access after in-place package replacement. Immutable package snapshots are now revalidated on the filesystem read path.
- **WebUI Interaction Timing** — #5371 (merged) hides copy/fork actions until `turn_end`, fixing conflicting completion signals. Handles edge cases across reasoning-only projections, resumed turns, and guidance rows.
- **Cron Scheduler Resilience** — #5376 (merged) ensures a single persistence failure (disk full, locked file) no longer permanently kills the cron scheduler — an exception-safety hard fix.
- **WebUI Model Preset Clarity** — #5399 (merged) distinguishes display labels from stable `/model` command names with localization across supported languages.
- **WebUI Range Selection & Turn Timing** — #5397 (merged) supports macOS-style Shift range selection in bulk-delete mode and preserves active-run timing through reasoning activity projections.
- **New Provider: OrcaRouter** — #5328 (closed) adds routing-gateway support exposing 150+ models from OpenAI, Anthropic, Google, DeepSeek, Qwen, MiniMax, and xAI behind a unified endpoint.

## 4. Community Hot Topics

- **#5377 — Consolidation truncation data loss** (Issue, 2 comments) — [Link](https://github.com/HKUDS/nanobot/issues/5377)
  The core concern: `Consolidator.archive()` truncates conversation history to the model's token budget, yet session cursors advance past the *entire* message batch, silently dropping messages the model never saw. While the author has already opened fix PR #5379, this issue touches a fundamental tension in NanoBot's memory architecture: bounded model-context vs. lossless session history. A fix that chunks rather than truncates (PR #5379) preserves both constraints — expect this to become a reference pattern for consolidation semantics.

- **#5358 — Session collaboration via mentions** (PR, open) — [Link](https://github.com/HKUDS/nanobot/pull/5358)
  This feature (stable `@name` identifiers for sessions, cross-session mentions, current-tab peer prioritization) has no comments, indicating the maintainer review backlog, not low interest. It converts WebUI sessions into first-class peer entities and is the most structurally significant open WebUI feature. Likely to be reviewed next week, and its session-identity model will strongly influence the design of drag-and-drop organization (#5389) and side conversations (#5364), which are already marked as conflicting.

## 5. Bugs & Stability

- **High: Stale background saves overwrite session data after `/new`** — #5271 (PR, priority p0) — [Link](https://github.com/HKUDS/nanobot/pull/5271)
  Still open after 10 days with a marked conflict. This is the highest-severity risk: a background compaction completing after `/new` can clobber the replacement session. Author proposes per-session serialization plus rejection of invalidated saves. Needs a maintainer review soon — until merged, users who issue `/new` while background tasks are mid-flight risk data loss.

- **Medium: Consolidation truncation advances cursor past dropped messages** — #5377 (Issue) / #5379 (PR) — [Link to issue](https://github.com/HKUDS/nanobot/issues/5377)
  Lossy but quiet: messages silently omitted from the model's context are also lost from the session forever. Fix PR #5379 replaces truncation with lossless bounded chunking plus deferred writes, and includes Unicode-boundary tests.

- **Low: WebUI actions appear while turn still running** — #5368 (Issue, closed) — [Link](https://github.com/HKUDS/nanobot/issues/5368)
  Closed by PR #5371 yesterday. Copy/fork actions now wait for authoritative `turn_end`. No residual risk reported.

No new crash or data-corruption-level bugs were filed in the last 24 hours despite active feature work — a positive signal for overall stability.

## 6. Feature Requests & Roadmap Signals

The active PR queue strongly signals NanoBot's roadmap direction: it is evolving from a single-session chat tool into a **multi-session collaborative workspace**:

- **Session collaboration** — #5358 (mentions between sessions) and #5364 (temporary side conversations with independent drafts/streaming/parallel sending) together transform the WebUI into a tiling window manager for agent sessions.
- **Session organization** — #5389 (drag-and-drop reordering, group creation by dropping one session onto another) delivers the information architecture for that workspace. Its parent-pane awareness suggests it was built against the latest layout engine.
- **Model management refactor** — #5400 (canonical preset-name unification across config, WebUI, sessions, Dream, and fallbacks, with inline rename) is a prerequisite for a cleaner provider UX. #5399 (merged) laid groundwork.
- **New provider surface** — #5398 (DashScope native protocol, exposing native thinking parameters) and #5328 (OrcaRouter gateway) indicate ongoing competitive provider coverage, with native-protocol support prioritized over compatible-mode for deep parameter access.

**Predicted for v0.4**: The canonical session `@name` model (#5358), side conversations (#5364), and drag-and-drop groups (#5389) are advanced, feature-complete PRs; the risk is the three-way merge, since #5364 and #5389 carry explicit conflict markers.

## 7. User Feedback Summary

- **Data integrity anxiety is the dominant theme.** The open issue (#5377) plus the stale-save bug (#5271) reflect users' concern that conversational history and session state are not yet trustworthy under stress — especially during consolidation, after `/new`, and across background jobs. The project's response has been thorough (dedicated fixes, regression tests, Unicode-boundary coverage), which should reassure the community that memory fidelity is a first-class concern.

- **WebUI completeness is outpacing user complaints.** The merged fixes (#5371, #5397, #5399) resolve previously reported UI inconsistencies (action visibility, range selection, preset naming). The open feature PRs (#5358, #5364, #5389) show users pushing for a desktop-app-level workspace, and maintainers are actively implementing that vision rather than merely fielding requests.

- **Resilience failures were silent, and users noticed.** The cron-scheduler persistence failure (PR #5376) and reconnect-safe WebUI mutations (#5401) both represent hidden failure modes — silent cron death and duplicate mutation replay after reconnect — that erode deployment confidence. Both have landed fixes with bounded replay caches and explicit error containment.

## 8. Backlog Watch

- **#5271 — Stale background saves after `/new`** (PR, priority p0, conflict) — [Link](https://github.com/HKUDS/nanobot/pull/5271)
  10 days open with a merge conflict. This is a data-loss-prevention fix at the highest priority tag, and the conflict likely stems from the same lifecycle refactor that shipped in #5370. Needs a maintainer rebase or guidance urgently.

- **#5358 — Session collaboration via mentions** (PR) — [Link](https://github.com/HKUDS/nanobot/pull/5358)
  No comments since opening despite 4 days passing. The feature is feature-complete, and its session-identity model is a dependency for the side-conversation and drag-and-drop PRs. A design review pass would de-risk the three-way WebUI feature merge.

- **#5291 — Persist subagent conversation transcripts** (PR) — [Link](https://github.com/HKUDS/nanobot/pull/5291)
  Open for 9 days without review comments. Under current behavior, subagent runs leave only the rendered announcement — no tool calls, results, or reasoning are retained. This is a developer-experience block for anyone debugging complex multi-agent workflows.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the provided GitHub data for Hermes Agent (NousResearch/hermes-agent), here is the project digest for 2026-08-16.

---

# Hermes Agent Project Digest - 2026-08-16

## 1. Today's Overview
Activity is very high, with 50 issues and 50 PRs updated in the last 24 hours. The project is actively converging on major refactoring initiatives, particularly the "Large-file decomposition" epic (#78647, now closed) and a focus on security hardening for credential handling and command approval gates. While no new releases were cut today, the issue tracker shows both P1 regressions being filed and closed, indicating a fast iteration cycle. The maintainers are actively managing backlogs by closing out large epics and triaging new bugs with severity and risk labels.

## 2. Releases
No new releases were published in the last 24 hours. The latest publicly referenced version remains **v0.20.1**, which is cited in recent bug reports for Windows and headless environments.

## 3. Project Progress
While no PRs were merged in the last 24 hours, the closure of major bug and refactoring issues indicates significant progress:

- **Large-File Decomposition Epic Complete (#78647)**: The project closed the meta-issue for sharding all repo "god-files" into clean modules, marking the completion of a 20-part refactoring effort (**Issue #78647**).
- **Critical Desktop Regression Fixed (#83683)**: A P1 issue where the desktop app on Windows killed the messaging gateway (WeChat/QQ) on restart was closed, resolving a major user-facing stability problem.
- **Session State Fixes (#82001, #69107)**: Two bugs related to session identity and state were closed, including an issue where agent turns were killed with a misleading "full disk" error after compression.
- **Bug Triage**: Eight other bugs were closed, including Windows-specific update failures (#83569), a security attribution bug (#81048), and several general issues (#4178, #50530, #70031).

## 4. Community Hot Topics
The most active discussions are centered around architecture, stability, and security:

- **"Large-file decomposition" Epic (#78647)**: With 79 comments, this was the most discussed issue of the day, though it is now closed. The community was heavily involved in the process of sharding god-files into modules.
- **Skills Index Watchdog (#66616)**: This automated probe continued to draw attention (37 comments) as the freshness of the public Skills Hub index remains a persistent quality issue, flagged as degraded.
- **Desktop Restart Reaping Gateway (#83683)**: Before its closure, this P1 bug drew 32 comments from users affected by silent messaging failures on Windows, emphasizing the criticality of desktop app reliability.
- **Persistent Session Memory (#8457)**: The long-running request for cross-session memory continues to gain traction (21 comments), highlighting a strong user desire for improved context retention ("memory").
- **Security & Approval Flow**: Two security-focused issues are generating concern: the misattribution of approval timeouts (#81048) and the bypass of dangerous-command detection via `bash -c` wrappers (#84551. The underlying need is for a more robust, unambiguous security boundary.

## 5. Bugs & Stability
The project shows a healthy balance of new P1s being filed and complex bugs being closed.

**New P1 (Critical) Issues:**
- **Security Boundary: CLI approval panel never renders (#87183)**: A critical bug where command approvals hang forever due to an environment variable leak (`HERMES_EXEC_ASK=1`) hijacking the approval flow into the gateway path. A fix PR does not exist yet.
- **Windows Stability: Desktop auto-update can wipe the build (#87331)**: A critical regression where a forced retry of the auto-updater on Windows ignores file locks and can delete the `win-unpacked` directory, destroying the installation. A fix PR does not exist yet.

**New P2 (High) Issues:**
- **Security: OAuth callback port collision on headless hosts (#87329)**: Makes interactive login impossible for MCP servers, rendering the feature unusable in that environment.
- **Feature Gap: Desktop second launch kills backend (#87295)**: A standard UX pattern (clicking the dock icon again) causes data loss.
- **Regression: Models writing fake tool calls (#83379)**: Some models are producing prose instead of structured `tool_calls`, breaking the agent loop.
- **Regression: `auxiliary.free_only` gate rejects explicitly-requested `:free` models (#85315)**: A config logic error rejects the user's explicit request and misreports the error as a payment failure.
- **Performance: Timeouts with slow local models (#87292)**: Instability with models running at >16 TPS brings the agent to a halt.
- **Security: `detect_dangerous_command` bypass via wrappers (#84551)**: Commands wrapped in `timeout` or `bash -c` bypass the approval gate, allowing dangerous commands to run unvetted.

## 6. Feature Requests & Roadmap Signals
The "innovation" and "feature" labels indicate a roadmap focused on agent intelligence and usability:

- **Active Development: Session Groups (#87297, PR)**: A PR is open to add AI-assisted session grouping, indicating work on the Persistent Session Memory feature request (#8457) is underway.
- **Active Development: Lean Compaction Mode (#87326, PR)**: A PR proposes a new `tail_mode="lean"` that scores significantly higher on recall with fewer tokens, suggesting a focus on making context compression more efficient.
- **Active Development: Desktop URL Toolbar (#87332, PR)**: A PR to add browser-style controls to the in-app preview, addressing a direct community request (#60030).
- **Strong Signal: Persistent Memory (#8457)**: The continued high level of discussion (21 comments) on this feature suggests it is a major pain point. The next minor release will likely include the "Session Groups" feature from PR #87297 to address this.
- **Strong Signal: Auto Reason Mode (#40306)**: Users continue to ask for ChatGPT-style auto-detection of reasoning effort, showing a desire for more autonomous agent behavior.

## 7. User Feedback Summary
The community feedback shows a split between power users pushing for deeper functionality and those facing basic stability hurdles.

- **Critical Pain Point (Windows & Desktop)**: Users are experiencing severe reliability issues on Windows, including auto-updates destroying the app (#87331) and gateways dying on restart (#83683). This is a major source of user dissatisfaction.
- **Security Anxiety**: The reported bypasses and misattributions in the security layer (#84551, #87183) are causing concern about the safety boundary, with users explicitly describing them as "Tier 1" issues.
- **Feature Enthusiasm**: There is clear excitement for the desktop improvements (e.g., URL toolbar PR #87332) and localization efforts (Turkish PR #87305), showing a healthy demand for a more polished desktop experience.

## 8. Backlog Watch
These items have been open for an extended period or involve complex ownership and may need maintainer attention:

- **Persistent Session Memory (#8457)**: Open since April, this high-demand feature remains in the "needs-decision" state. While PR #87297 addresses session grouping, the core "Auto-Compression" and "Cross-Session Search" functionality is still pending.
- **Skills Index Watchdog (#66616)**: The automated freshness probe has been failing for nearly a month, and the issue remains open to coordinate a fix for the public documentation pipeline.
- **`Add Revell to optional-mcps catalog` PR (#50523)**: This PR has been open since June, untouched for over a month. It has no comments and may need a decision on whether to include this third-party memory service.
- **`google-antigravity` Integration Issues (#50530)**: This P2 bug report summarizes three separate severe issues (sub-agent crashes, forced re-auth, session loss) with the Gemini provider. The issue has no updates or fix PRs linked, leaving the integration in a broken state.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-16

## 1. Today's Overview

The PicoClaw project is currently in a low-activity maintenance window. No issues were opened, closed, or updated in the last 24 hours, and no new releases were published. The only ongoing work consists of two stale pull requests (both nearly 10 days old) awaiting merge or follow-up action from maintainers. While not a sign of distress, the project's momentum is clearly stalled this week, with no features landed and no community questions pending. The two open PRs address meaningful stability improvements, making their resolution the primary near-term indicator to watch.

## 2. Releases

**None.** No new versions were published today or in the immediately preceding period. There are no release notes, breaking changes, or migration instructions to report.

## 3. Project Progress

No pull requests were merged or closed in the past 24 hours. The two open PRs remain open:

- [#3321 — fix(agent): move dynamic context after history to preserve prefix caching](https://github.com/sipeed/picoclaw/pull/3321) — Addresses a token-prefix-caching inefficiency by repositioning the per-request dynamic context block (Current Time, Runtime, Session, Sender) from within the system message to after conversation history, preserving prefix cache invalidation.
- [#3320 — fix(deps): bump whatsmeow to unblock WhatsApp "client outdated (405)"](https://github.com/sipeed/picoclaw/pull/3320) — Updates the pinned `whatsmeow` dependency to resolve WhatsApp rejecting the advertised client version, which currently kills the native WhatsApp channel with a 405 error and no reconnect.

Both PRs were authored by the same contributor, have no comments or reviews, and have not been touched since August 15.

## 4. Community Hot Topics

There are no highly active threads to report — both open PRs have zero comments and zero reactions. However, the underlying needs are worth noting analytically:

- **WhatsApp channel reliability** ([PR #3320](https://github.com/sipeed/picoclaw/pull/3320)): A broken native integration with no reconnect mechanism is a significant operational pain point for any user relying on WhatsApp-facing agents.
- **Performance / cost optimization through prefix caching** ([PR #3321](https://github.com/sipeed/picoclaw/pull/3321)): The focus on preserving prefix caching suggests users are hitting token-cost or latency ceilings in long-conversation scenarios — a classic production scaling concern for agentic systems.

Neither PR has received maintainer engagement, which may itself be a signal of review bandwidth constraints.

## 5. Bugs & Stability

One live bug substantially affecting functionality:

- **High severity — WhatsApp "Client outdated (405)"** ([PR #3320](https://github.com/sipeed/picoclaw/pull/3320)): The native WhatsApp channel connects, is dropped ~5 seconds later with a 405 error, and the system makes no reconnect attempt — leaving the channel effectively dead. A dependency bump fix is proposed in the open PR, but it has not yet been merged. No other bugs, crashes, or regressions were reported today.

## 6. Feature Requests & Roadmap Signals

No new feature requests were submitted today. Signals are limited to the open PRs, but they suggest directional priorities:

- **Protocol stability as a prerequisite for multi-channel agents**: Getting WhatsApp back online is clearly a blocking item for production deployments.
- **Cost efficiency for long-lived conversations**: The prefix-caching fix implies users are running multi-turn agents at scale where token reuse matters — expect more performance-oriented refinements in upcoming releases.

Absent maintainer responses or a release timeline, predicting the near-term roadmap is speculative, though these two fixes are likely candidates for the next patch release.

## 7. User Feedback Summary

With no issues, comments, or reactions in the last 24 hours, direct user feedback is unavailable today. Indirect signals point to two persistent pain points: channel connectivity (WhatsApp outage) and operational cost (prefix caching). There is no evidence of new dissatisfaction or emergent use cases; conversely, the complete absence of incoming issues could indicate user attrition, a quiet stable period, or low public usage of the issue tracker this week.

## 8. Backlog Watch

Two PRs require maintainer attention and are eligible for review or follow-up:

- [PR #3321 — Agent context placement / prefix caching](https://github.com/sipeed/picoclaw/pull/3321) — Open 9 days, no reviews or comments. Low risk, performance-focused; likely ready for expedited review.
- [PR #3320 — WhatsApp dependency bump](https://github.com/sipeed/picoclaw/pull/3320) — Open 9 days, no reviews or comments. Directly unblocks a fully broken production channel — prioritize for merge or at least a status update.

No long-unanswered issues are in the tracker (total issues: 0), so the two stale PRs are the only backlog items needing resolution.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-16

## 1. Today's Overview

NanoClaw is in a highly productive development phase with **22 pull requests updated in the last 24 hours**, though no new releases were published and no issues were filed or closed today. The activity is dominated by **core-team contributor gavrielc**, who has driven a remarkable 11-PR push focused on architectural seams, permissions refinement, and cross-session context — indicating intentional, systematic platform hardening rather than scattered feature additions. There are **19 open PRs** awaiting review or merge, which suggests maintainer bandwidth might become a bottleneck. The single merged PR (#3268) addresses a poll-loop lifecycle leak, showing that stability work continues alongside feature development. Notably, several older PRs (#2752 from June, #37 from February) received activity today, hinting that the maintainer is beginning to work through the backlog.

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent release history is not available in this data snapshot, so there are no changelogs, breaking-change notes, or migration guides to report at this time.

## 3. Project Progress

**Merged/Closed Today:**

- **[#3268 — `fix(poll-loop): stopped loops leaked their active query's follow-up poller`](https://github.com/nanocoai/nanoclaw/pull/3268)** — The only merged PR today. It addresses a root-cause lifecycle bug where `runPollLoop` only checked the abort signal between iterations, but the loop often parks inside `processQuery` on a stream that stays open between turns. This allowed an aborted loop to leak its active query and the 500ms follow-up poller, causing resource leaks. Now closed.
- **[#37 — `Rename to DotClaw and switch from WhatsApp to Telegram`](https://github.com/nanocoai/nanoclaw/pull/37)** — Closed after six months. This was a broad rename and channel-swap PR that appears to have been superseded by the project continuing as NanoClaw with Telegram support added via other PRs.

**Key feature/fix PRs still open but advancing today:**

- **[#3254 — Two-phase inbound batch selection](https://github.com/nanocoai/nanoclaw/pull/3254)** — Fixes a critical bug where accumulated context (trigger=0) rows could crowd out due task rows from the capped batch, causing the agent to wake but never receive the actual work.
- **[#3255 — Sender's own channel row resolution](https://github.com/nanocoai/nanoclaw/pull/3255)** — Fixes outbound delivery resolving the wrong messaging group when multiple bot identities share a room.
- **[#3256 — `messaging_groups.detached_at` migration](https://github.com/nanocoai/nanoclaw/pull/3256)** — Adds a detached_at timestamp so the bot can track when it was removed from a conversation without deleting the row (preserving wirings, sessions, and destinations).
- **[#3259 — Setup/tooling wizard fixes](https://github.com/nanocoai/nanoclaw/pull/3259)** — Three fixes including stripping heading ordinals from skill-apply step captions (wrong step numbers across skipped steps) and headless browser URL surfacing.
- **[#3269 — Telegram channel integration](https://github.com/nanocoai/nanoclaw/pull/3269)** — A community PR adding a full Telegram channel adapter. Note: This competes/overlaps with earlier Telegram work.
- **[#3257 — Cross-session context module](https://github.com/nanocoai/nanoclaw/pull/3257)** — Fanes messages into sibling sessions as "session-echo" context rows, adds DM backfill for new sessions, and a new `ncl sessions history` command.

## 4. Community Hot Topics

All PRs currently show **0 comments and 0 reactions**, making comment-count ranking ineffective. The activity signals instead come from which PRs are receiving updates and which contributors are active.

**Most notable by authorship and scope:**

- **[#3269 — Telegram channel integration by rudysmets7-strid](https://github.com/nanocoai/nanoclaw/pull/3269)** — Community contributor adding a Telegram adapter with 1483 tests passing. This is a significant integration request that has been central to the project's direction (see PR #37's rename attempt).
- **[#3251 — Heartbeat stall fix by DawoudIO](https://github.com/nanocoai/nanoclaw/pull/3251)** — Another community contributor identifying a critical bug where rate-limiting could stall heartbeats for 30+ minutes, causing false stale-container kills.
- **[#2752 — Discord URL-only attachments by chubbicorn245](https://github.com/nanocoai/nanoclaw/pull/2752)** — Open since June 12, updated today. Addresses a fundamental UX gap: Discord pasted text and images arrive as bare `[file: message.txt]` with no readable bytes.
- **[#3250 — Telegram Markdown sanitizer removal by chiptoe-svg](https://github.com/nanocoai/nanoclaw/pull/3250)** — A clean-up PR that removes a legacy workaround which downgrades `**bold**` to _italic_ in Telegram.
- **[#3253 — Model reasoning effort fix by simonechecchia](https://github.com/nanocoai/nanoclaw/pull/3253)** — Fixes the opencode integration to honor group reasoning effort in model config.

**Underlying needs:** The pattern across community PRs and the core-team's own work reveals that **Telegram support, multi-instance bot identity handling, and reliable delivery in degraded/rate-limited conditions** are the dominant concerns. Channels and delivery reliability are clearly the most invested-in areas of the codebase right now.

## 5. Bugs & Stability

Ranked by estimated severity:

1. **[CRITICAL — Heartbeat stall during rate-limiting — PR #3251](https://github.com/nanocoai/nanoclaw/pull/3251)** — Heartbeat file only updated on API events; during Claude API rate-limiting or hangs, heartbeats stall 30+ minutes, causing the sweeper to falsely kill healthy containers. No merge yet — this has production-impact potential.
2. **[HIGH — Idle container with no heartbeat file is exempt from absolute-ceiling kill — PR #3252](https://github.com/nanocoai/nanoclaw/pull/3252)** — `decideStuckAction` skips the absolute-ceiling kill when a container has no `.heartbeat` file, with no upper bound. This is an infinite-lease bug on stuck containers.
3. **[HIGH — Context rows crowd out task rows in inbound batch — PR #3254](https://github.com/nanocoai/nanoclaw/pull/3254)** — A backlog of trigger=0 context rows can push out due task work from the capped batch, so the agent never sees the actual task that woke it.
4. **[HIGH — Outbound delivery resolves wrong channel row — PR #3255](https://github.com/nanocoai/nanoclaw/pull/3255)** — When multiple bot identities (adapter instances) share one `(channel_type, platform_id)` address, delivery picks a deterministic-but-arbitrary sibling row, sending messages to the wrong identity.
5. **[MEDIUM — Stopped poll loop leaks its query + follow-up poller — PR #3268](https://github.com/nanocoai/nanoclaw/pull/3268)** — **FIXED today** (merged). Resource leak caused by abort signal only checked between iterations.
6. **[MEDIUM — Telegram `**bold**` downgraded to _italic_ — PR #3250](https://github.com/nanocoai/nanoclaw/pull/3250)** — Legacy sanitizer from the old converter is now actively harmful; the PR deletes it but needs merge.
7. **[LOW-MEDIUM — Discord attachments never reach the agent readably — PR #2752](https://github.com/nanocoai/nanoclaw/pull/2752)** — Pasted text and images are shown as bare `[file: message.txt]` references with no bytes or path.
8. **[LOW — Skill-apply heading ordinals render wrong step numbers — PR #3259](https://github.com/nanocoai/nanoclaw/pull/3259)** — Cosmetic but confusing UX regression across skipped steps and multi-skill runs.

## 6. Feature Requests & Roadmap Signals

Strong signals for what is coming in the next release, based on the core-team's own PR stack:

- **Telegram as a first-class channel** — Both core-team work (#3261, #3262) and community work (#3269, #3250) are converging on Telegram support. PR #3269 adds the full adapter; #3261 adds `setTyping` status lines, `setThreadTitle`, and `setSuggestedPrompts`; #3262 adds DM-thread normalization. **Prediction: Telegram support ships in the next minor release.**
- **Cross-session context propagation (#3257)** — A new module for agent groups that fan context into sibling sessions and backfill new DM sessions. This is a significant architecture feature, likely aimed at multi-session agent groups.
- **Richer permissions: `decline_notify` policy (#3260)** — A fourth unknown-sender policy that politely declines in the sender's DM while notifying the owner with a one-liner. Complements the existing strict/request_approval policies.
- **Channel-registration interception seam (#3266)** — A generic interceptor that lets modules consume or handle registration-card escalation before it is built. Enables auto-wiring, auto-decline, or ignoring.
- **`CreateAgentOptions.suppressCreatedNotify` (#3265)** — API surface widening for wrapper tooling that does its own provisioning and doesn't want duplicate "Agent created" messages.
- **Delivery batch preview hook (#3264)** — Lets modules peek at the whole undelivered outbound batch before rows deliver one-by-one; motivating use is prefetching expensive data.
- **Hot-start channel adapters (#3263)** — `startChannelAdapter(key)` lets newly registered adapters get the same four-step boot treatment as init-time adapters, without restart.
- **Conversation detachment tracking (#3256)** — `detached_at` column so the system knows when the bot was removed vs. never present.

**Prediction for next release:** A consolidation release that lands at least 5–8 of these core-team PRs (A1–A8 labels suggest they're planned work items), plus Telegram stabilization from #3269 and #3250.

## 7. User Feedback Summary

Quantitative feedback (reactions, comments, upvotes) is **near-zero** across all PRs — this project appears to have a small, tightly-knit contributor core rather than a broad user community actively commenting on PRs. However, qualitative signals from the PR descriptions themselves reveal real pain points:

- **Channel fidelity matters**: Users want their text to render *correctly* — Telegram users are getting italicized bold due to the sanitizer bug (#3250), and Discord users can't read pasted attachments at all (#2752). These are basic UX respects.
- **Multi-identity environments are tricky**: Users run multiple bot identities in one room, and the system currently delivers to the wrong one (#3255). The fix is ready but not yet merged.
- **Resource-constrained / rate-limited environments**: Users running many containers are hitting false kills due to heartbeat stalls (#3251) and the no-heartbeat-file infinite lease (#3252). Both have proposed fixes awaiting merge.
- **Community contributor velocity**: Several outside contributors (rudysmets7-strid, DawoudIO, chubbicorn245, chiptoe-svg, simonechecchia) are filing *specific, well-scoped, test-backed* PRs. That's a healthy signal of engaged users and a welcoming contributing guide.

**Overall satisfaction**: Moderate-to-positive. The core team is responsive and shipping fixes, but the accumulation of 19 open PRs suggests there may be delay between "fix exists" and "fix is live," which is likely the largest source of user friction today.

## 8. Backlog Watch

PRs that have been open longest and still need maintainer attention:

1. **[#2752 — `fix: stage inbound attachments that expose only a url (Discord)`](https://github.com/nanocoai/nanoclaw/pull/2752)** — **Open since 2026-06-12 (65+ days)**. Updated today but still not merged. High user impact — Discord attachments are unreadable. This is the most overdue community PR in the backlog.
2. **[#37 — `Rename to DotClaw...`](https://github.com/nanocoai/nanoclaw/pull/37)** — **Open since 2026-02-02 (6+ months)**. Closed today, so technically resolved — but it was closed *without* being merged. The project remains "nanoclaw" even though the author tried to rename it to "dotclaw." It's worth verifying the motivation — perhaps the author wanted to distance from a prior name or had trademark concerns.
3. **[#3253 — `fix(opencode): honor the group reasoning effort`](https://github.com/nanocoai/nanoclaw/pull/3253)** — Open since 2026-08-15, 1 day. Not yet reviewed; small config fix from a community contributor.
4. **[#3269 — `feat(channels): add Telegram channel integration`](https://github.com/nanocoai/nanoclaw/pull/3269)** — Open since 2026-08-15, 1 day. Significant scope (new adapter + auth flow + sanitizer); will need careful review against the core-team's own Telegram work (#3261, #3262, #3250) to avoid merge conflict or duplicated effort.

**Maintainer action needed:** The core team should prioritize reviewing and merging the **stability fixes** (#3251, #3252, #3254, #3255) before the backlog of open PRs creates merge-conflict risk with the continuous stream of new core-team PRs. The Discord attachment PR (#2752) is the longest-standing user-facing issue needs a decision: merge, request changes, or close with guidance.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-16

## 1. Today's Overview

NullClaw is in a **low-activity, maintenance-oriented state** today, with only 1 new issue and 1 open PR in the last 24 hours. No releases were published, and no PRs were merged or closed, indicating that no code changes landed upstream. The single open PR (#987) targets **long-running local agent runs**, a stability and performance concern that aligns with the project's core AI-agent focus. The only issue filed today is a straightforward feature request for **proxy support**, suggesting that user adoption is reaching environments where network restrictions are a barrier. Overall, the project appears stable but slow-moving, with maintainers potentially prioritizing quality over velocity.

## 2. Releases

No new releases were published in the last 24 hours. No changelog, breaking change notice, or migration guidance is applicable at this time.

## 3. Project Progress

**No PRs were merged or closed today.** The only open PR is #987, which is still under review and has not been integrated. Key features introduced in this PR include:

- **Cache-friendly prompt architecture:** Splitting the system prompt into a stable prefix and a variable date/time tail to improve LLM context caching efficiency.
- **Tool output compression:** Implementing a new `result_compress.zig` module to compress tool outputs before injecting them into history, while preserving full fidelity in observer logs.
- **Loop-hygiene guardrail:** Adding detection of identical repeated calls within a single turn to prevent runaway loops in extended local runs.

These changes are targeted at the **agent loop** and are likely to land in a future patch release once review completes.

## 4. Community Hot Topics

**No issues or PRs attracted comments or reactions today.** Both items are brand new (created 2026-08-15) and have zero engagement so far. The most notable item is **PR #987** (feat(agent): loop hygiene), which is technically substantive but has not yet drawn reviewer discussion or user feedback. The lack of community interaction suggests either low user awareness or the PR being submitted late in the previous day. Maintainers should proactively solicit review from experienced contributors to avoid the PR stalling.

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported in the last 24 hours.** The only open issue (#988) is an enhancement request, not a defect. The project's health metrics indicate no current stability concerns flagged by the user base. However, the existence of PR #987 targeting agent-loop stability implies that maintainers are aware of potential production issues in extended local sessions, even if users have not yet formally reported them.

## 6. Feature Requests & Roadmap Signals

The only feature request today is **Issue #988 — Proxy Support**:

> "Please add HTTP(s) and SOCKS(5h) proxy support for providers."

This is a clear infrastructure-level request, indicating that users are deploying NullClaw in **corporate networks, cloud sandboxes, or regions requiring egress control**. Given that the project is an AI agent framework, proxy support is a low-complexity, high-value addition that broadens enterprise and privacy-focused adoption. This feature is **likely to appear in the next minor version (e.g., v0.x.y)**, especially if the maintainers follow a "quick wins" roadmap model. The use of "SOCKS(5h)" suggests the requester is aware of the SOCKS5h DNS-resolution variant, indicating technical sophistication.

## 7. User Feedback Summary

The single issue filed today reveals a direct user pain point: **inability to run NullClaw in network-restricted or proxied environments**. Deriving from the author's "No response" motivation, the request is likely feature-driven rather than stemming from a failure — the user has not yet hit a bug but anticipates one. Overall sentiment is neutral-to-positive: no complaints about performance, UI, or agent quality were logged. The lack of negative feedback alongside active development suggests general user satisfaction, though the sample size (1 issue) is too small to draw strong conclusions.

## 8. Backlog Watch

**No stale or unanswered items require immediate maintainer attention.** The oldest open item is PR #987, which is only 1 day old and not yet overdue. However, given today's zero merge velocity, there is a risk that this PR could drift. Recommended action: assign a reviewer today and aim for merge within 48 hours to maintain contribution momentum and avoid contributor frustration. No other issues or PRs exceed standard response-time thresholds.

---

*Digest generated automatically for 2026-08-16 based on public GitHub activity.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-16

## 1. Today's Overview

IronClaw is in a **high-velocity performance and stabilization phase**. Activity is intense: 27 issues and 12 PRs were updated in the last 24 hours, with the majority of issues (21) closed. The dominant theme is **I/O reduction and write amplification elimination** (Tier 1/Tier 2 perf epics #7591), with three major PRs (#7628, #7629, #7676) landed to slash per-turn database writes. A significant architectural milestone also landed: PR #7634 **completes the switchover to the "unbound-turns" prepared-context model**, a foundational refactor that spawned five follow-up issues today. The Live Canary has been red 30/30 runs due to harness bugs (not product regressions), and a dedicated fix PR (#7679) is now open. The project is clearly prioritizing durability, deterministic behavior, and removing legacy debt.

## 2. Releases

**None.** No new releases were published in the last 24 hours. Work is being delivered through merged PRs rather than versioned releases.

## 3. Project Progress

Five PRs were merged/closed today, focusing heavily on performance and correctness:

- **[#7634 — feat(unbound-turns): complete the switchover to prepared-context turns](https://github.com/nearai/ironclaw/pull/7634)** *(merged, XL)* — This is the landmark architectural PR of the week. It completes the move to the unbound-turns model, ships every follow-up documented in the design epics, and passed a 71-clause conformance audit. It deliberately opened an `ironclaw_openai_compat → ironclaw_threads` dependency edge, which generated immediate follow-up governance issues (#7674).
- **[#7628 — perf(processes): remove heartbeat journal churn](https://github.com/nearai/ironclaw/pull/7628)** *(merged, M)* — Implements the conservative heartbeat subset of the Tier 1 perf epic (#7591): stops appending a permanent journal row per 5s heartbeat, keeps lease timestamps authoritative, and widens the turn-runner cadence to 15s. Massive write-amplification win.
- **[#7629 — perf: reduce trigger and outbound state writes](https://github.com/nearai/ironclaw/pull/7629)** *(merged, M)* — Moves trigger run-history pruning from every update to the initial fire claim, eliminating correlated-subquery DELETEs on the hot path.
- **[#7676 — perf(threads): coalesce thread index touches](https://github.com/nearai/ironclaw/pull/7676)** *(merged, L)* — Coalesces bursty per-thread activity into bounded writes (up to 7 CAS row rewrites per turn become ≤1), preserving monotonic CAS correctness for multi-worker safety.
- **[#7670 — chore(agents): refresh codebase knowledge graph](https://github.com/nearai/ironclaw/pull/7670)** *(merged, XS)* — CI bot snapshot refresh.

The gating of `prune_run_history` (#7595), removal of dead `advance_subscription_cursor` API (#7597), and `touch_thread_index_updated_at` coalescing (#7596) were all closed as they are addressed by these merged PRs.

## 4. Community Hot Topics

- **[#467 — Trajectory benchmark system for agent quality evaluation](https://github.com/nearai/ironclaw/issues/467)** *(4 comments, open)* — The oldest active issue with real engagement. This proposes a two-layer evaluation harness (hard assertions + LLM-as-judge) on real trajectories. The sustained interest (updated this week) signals the community's growing need to measure agent quality objectively rather than by vibes. This is a strategic investment area.
- **[#3236 — Define same-thread follow-up and steering policy (Reborn)](https://github.com/nearai/ironclaw/issues/3236)** *(3 comments, closed)* — Closed today. Covers `/btw` steering, queue visibility, and cancellation interaction. The closure suggests the deterministic run-control semantics are now fully specified (and largely implemented via the unbound-turns work).
- **The perf epic cluster (#7591)** — While individual issues have ≤1 comment, the **12 issues** closed today all belong to this epic. The sustained, systematic attack on per-turn write counts reflects a clear operational pain signal: **database write amplification is the #1 production concern for IronClaw operators**.

The underlying need across discussions is **predictability**: predictable resource consumption, predictable agent behavior, and predictable delivery channels.

## 5. Bugs & Stability

Today's report is dominated by **stability fixes** rather than new crashes:

**High severity:**
- **[#7675 — E2E: qa_6c gmail-to-sheet flake cascades across the whole provider-contracts session](https://github.com/nearai/ironclaw/issues/7675)** *(open)* — A live Gmail/emulate leg intermittently fails with a generic resource-class capability error, which then cascades and reddens the entire provider-contracts session. **No fix PR yet**; it caused a false failure on PR #7634. This is a test-infrastructure health issue affecting CI trust.

**Medium severity (harness, not product):**
- **[#7679 — stop harness bugs reddening green canary runs](https://github.com/nearai/ironclaw/pull/7679)** *(open, XL)* — The Live Canary is 30/30 red due to three harness defects failing correct product behavior and one liveness proxy. Directly targets the trust-destroying false negatives.

**Low severity (regressions found pre-merge):**
- **[#7671 — Capability dispatch stack pressure: kernel sandbox path still near the test-stack edge](https://github.com/nearai/ironclaw/issues/7671)** *(open)* — The decorator chain compiled into a single oversized poll frame causing stack overflow at default 2 MiB test threads. Mitigated by chain-boxing (f1f396cd8), but the sandbox path is still near the edge. Monitoring issue.

**Fixed today:**
- **Scheduler stale-heartbeat false failure** (#5239) — closed.
- **Production debug logging flood** (#5237) — closed.
- **[#6821 — IronHub search returning complete garbage](https://github.com/nearai/ironclaw/issues/6821)** *(closed)* — The agent reported 3 tools when 18 existed, and invented 20 non-existent skills. Significant correctness bug, now closed.

## 6. Feature Requests & Roadmap Signals

The five new issues opened today (all by `henrypark133`, all from #7634 review) are the strongest roadmap signals. They tell a clear story: **post-switchover hardening is the next release theme.**

| Issue | Direction | Prediction |
|---|---|---|
| [#7672 — Typed ToolChoice](https://github.com/nearai/ironclaw/issues/7672) | Retire overloaded `tool_choice: Option<String>`; introduce a typed enum across all 5 providers | Likely in next minor — the string-matching is a maintenance liability and inconsistent across providers |
| [#7673 — BudgetLedger accounting refinements](https://github.com/nearai/ironclaw/issues/7673) | Fix truncated-launch double-charge; ensure charge durability | **High probability for next patch** — billing correctness is a trust issue, and it currently errs conservative (over-count) |
| [#7674 — Symbol-level allowlist for dependency edges](https://github.com/nearai/ironclaw/issues/7674) | Extend architecture tests from crate-level to symbol-level | Likely fast-tracked — it took one day to go from "edge opened" to "test gap identified" |
| [#7671 — Stack pressure in kernel sandbox](https://github.com/nearai/ironclaw/issues/7671) | Reduce poll-frame size in the delegation chain | Mitigated, likely scheduled as backlog |
| [#7675 — E2E flake cascade](https://github.com/nearai/ironclaw/issues/7675) | Test-harness isolation | Likely next sprint — red CI blocks everything |

**Strategic signals:** The trajectory benchmark proposal (#467) and the completed Reborn QA automation epic (#4775) suggest the next major investment will be **quality-of-agent measurement**, moving beyond unit tests to holistic trajectory evaluation.

## 7. User Feedback Summary

The strongest user pain points visible in this data:

- **"Wasted database writes" is a recurring operational theme.** The Tier 1 perf issues (#7595, #7593, #7596) are labeled "pure waste," and the community (via maintainer `serrrfirat`) is aggressively eliminating them. Users are seeing excessive storage growth and write latency.
- **Live Canary 30/30 red** — users (and maintainers) are losing trust in CI signals. PR #7679's candid table of "harness defect vs. real failure" is exactly what the community needs.
- **IronHub discovery was broken** (#6821): a search query returned factual nonsense (3 vs 18 tools; invented skills). For an agent platform, **catalog/capability discovery is a core trust surface**; this was a visible embarrassment.
- **User satisfaction signals are strong:** 4 of the 5 new issues today are tagged `risk: low`, indicating the core system is stabilizing. Maintainers are now treating correctness follow-ups as small, safe increments.

No direct end-user feature requests surfaced today; the signal is dominated by maintainer-driven hardening.

## 8. Backlog Watch

- **[#467 — Trajectory benchmark system](https://github.com/nearai/ironclaw/issues/467)** *(open since Mar 2026, 4 comments, updated this week)* — The oldest open issue with meaningful community engagement. Not stale, but needs a champion. Updated yesterday suggests it's being actively scoped; a design PR may follow.
- **[#7599 — Widen process heartbeat interval 5s → 15-20s](https://github.com/nearai/ironclaw/issues/7599)** *(closed)* — The production config files (`docker/reborn/config.toml`) still hardcode 5s; PR #7628 shipped "a 15-second turn-runner cadence" but config siblings (3 files) may still carry 5s. **Watch for a follow-up commit** to update the remaining config templates; if not addressed, the Tier 2 write savings are only partially realized.
- **[#5672 — Replace SSE streaming with a real subscription API](https://github.com/nearai/ironclaw/issues/5672)** *(closed today)* — The WebUI v2 SSE drain-and-poll anti-pattern is officially acknowledged and closed. The underlying polling load (1–3s polls hitting Postgres) is a known perf sink; **if the closure is merely "wontfix for now," this will resurface** as WebUI usage grows.
- **[#6726 — `register_generic_channel_outbound_targets` can be a no-op](https://github.com/nearai/ironclaw/issues/6726)** *(closed)* — A surviving mutant that even dead code can pass every test tier is a **canary for weak mutation coverage** in the extension host. Worth a follow-up audit, though the issue is closed.

---

**Overall health assessment:** IronClaw is in a **strong, disciplined engineering phase**. The merge of the unbound-turns switchover (#7634) is a foundational step that the team is actively hardening. The performance work is targeted, measurable, and shipped incrementally. The main risk is **CI reliability** — the canary failures and flaky e2e tests are eroding trust in verification, and PR #7679 must land quickly. The trajectory-benchmark proposal (#467) remains the most important open strategic question.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Digest Date:** 2026-08-16  
**Data Source:** github.com/netease-youdao/LobsterAI

---

## 1. Today's Overview

LobsterAI is in a **maintenance and stabilization phase**, with no new releases during the reporting period. Activity is moderate: 18 issues updated (16 closed, 2 open) and 6 PRs updated (2 closed/merged, 4 open). The vast majority of updates are **stale-label automated closures** of issues created between late April and late May, indicating the project maintainers are actively cleaning up the backlog rather than processing new submissions. Only 2 issues remain open, both of which are product-level feature requests rather than active bugs. The most substantive technical work appears in a **recently merged PR (#2234)** addressing a core OpenClaw integration issue around cron job and child-agent finalization. The project remains active but is currently in a **low-velocity period**, focused on debt reduction and dependency upkeep (as evidenced by 4 open dependabot PRs).

---

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent release remains the previous version; no changelog, migration, or upgrade notes to report.

---

## 3. Project Progress

Two PRs were closed/merged in the last 24 hours. The most significant is:

| PR | Title | Key Change |
|----|-------|-----------|
| [#2234 (merged)](https://github.com/netease-youdao/LobsterAI/issues/2234) | fix(openclaw): cron yield descendant finalization | **Major integration fix:** Resolves a core OpenClaw flow issue where child-agent completion events did not propagate back to the parent agent after `sessions_yield` in cron scenarios. Adds a yield-continuation loop during cron finalization to support multi-round parent-agent driving until all descendants complete. Covers three test scenarios: normal parallel child agents, cron parallel child agents, and cron serial child agents. |
| [#1879 (merged)](https://github.com/netease-youdao/LobsterAI/issues/1879) | fix: preserve manually-added plugin load paths on config sync | **Config reliability fix:** Resolves silent data loss where LobsterAI's `OpenClawConfigSync.sync()` would overwrite `plugins.load.paths`, discarding manually-added paths (e.g., community plugins installed via `pm install` like `memory-lancedb-pro`). |

**Key takeaway:** These merges address **previously-reported user pain points** (config loss and cron reliability), suggesting the maintainers are methodically working through the backlog of community-reported stability issues.

---

## 4. Community Hot Topics

The most-discussed items reveal a focus on **configuration complexity, model ecosystem lock-in, and UX polish**:

| Item | Type | Comments | Topic |
|------|------|----------|-------|
| [#1849 (closed)](https://github.com/netease-youdao/LobsterAI/issues/1849) | Issue | 4 | Infinite "NO_REPLY" loop: task prematurely marked complete while model continues outputting; page shows no response data |
| [#1878 (closed)](https://github.com/netease-youdao/LobsterAI/issues/1878) | Issue | 4 | WeChat IM bot integration broken at verification step: QR scan requires 6-digit code entry on desktop client, but no input UI exists |
| [#1903 (open)](https://github.com/netease-youdao/LobsterAI/issues/1903) | Issue | 3 | **Member login failures prevent access to paid NetEase models** — critical blocker for paying users |
| [#1988 (closed)](https://github.com/netease-youdao/LobsterAI/issues/1988) | Issue | 3 | **Model forcing bug:** After update, Qwen3.6-plus is forcibly routed to NetEase's own models (no quota), breaking Alibaba Bailian coding plan integration; config overrides are ignored |

**Analysis:** The login failure (#1903) and model routing (#1988) issues are the most consequential for user retention — they directly impact the paid experience. The WeChat IM issue (#1878) is a usability blocker for a specific but popular channel. The infinite NO_REPLY issue (#1849) points to a deeper architecture problem with how completion states are managed when model streaming and task lifecycle fall out of sync.

---

## 5. Bugs & Stability

Sixteen issues were closed today, but most are stale-label closures. The significant bugs among them, ranked by severity:

| Severity | Issue | Problem | Fix Status |
|----------|-------|---------|------------|
| 🔴 **High** | [#1988](https://github.com/netease-youdao/LobsterAI/issues/1988) | **Forced model routing to NetEase models breaks third-party plans** (Alibaba Bailian + Qwen3.6-plus). Config file edits are overwritten by the system. | No fix PR yet. Affects paid third-party services. |
| 🔴 **High** | [#1849](https://github.com/netease-youdao/LobsterAI/issues/1849) | **Infinite NO_REPLY:** task completes early but model keeps streaming; UI shows no data. Likely a race condition in task lifecycle management. | No fix PR. |
| 🟠 **Medium** | [#1878](https://github.com/netease-youdao/LobsterAI/issues/1878) | **WeChat IM setup incomplete:** scanning QR prompts code verification on desktop client, but the client has no input field. | No fix PR. |
| 🟠 **Medium** | [#1971](https://github.com/netease-youdao/LobsterAI/issues/1971) | **Virtual scroll breaks with oversized elements (e.g., Mermaid diagrams):** up-scroll becomes impossible after repeated render cycles; element height changes trigger infinite re-renders. | No fix PR. |
| 🟠 **Medium** | [#2017](https://github.com/netease-youdao/LobsterAI/issues/2017) | **Local runtime detection failure:** "No built-in OpenClaw runtime (cfmind) detected" — users cannot run locally without a pre-build step that isn't documented. | No fix PR. |
| 🟡 **Low** | [#1993](https://github.com/netease-youdao/LobsterAI/issues/1993) | **AI engine connection lost** in desktop app (stable via IM bot); likely an app-specific networking/streaming issue. | No fix PR. |
| 🟡 **Low** | [#1885](https://github.com/netease-youdao/LobsterAI/issues/1885) | **Security – email skill path traversal:** `downloadAttachments` in `imap-smtp-email/scripts/imap.js` does not sanitize attachment filenames, enabling directory traversal. | No fix PR. |

**Notable:** While 16 issues were closed, the root causes of several (particularly #1849, #1988, #1878, #2017) may remain unaddressed, as stale-label closures typically indicate either "won't fix" or "cannot reproduce" outcomes. The security issue (#1885) is concerning for a production-oriented tool.

---

## 6. Feature Requests & Roadmap Signals

Several explicit feature requests and improvement suggestions are visible in the closed/opened issues:

| Request | Issue | Description | Likelihood of Implementation |
|---------|-------|-------------|------------------------------|
| **Agent Memory System** | [#2046 (open)](https://github.com/netease-youdao/LobsterAI/issues/2046) | Comprehensive memory architecture proposal: session metadata persistence, cross-session retrieval, long-term structured memory. Highly detailed with priority levels. | **High** — the project has already shipped `skill-self-evolver` and memory-related infrastructure; this appears to be a roadmap-aligned request. |
| **Professional UI Redesign** | [#1836 (closed)](https://github.com/netease-youdao/LobsterAI/issues/1836) | User feedback that UI "is too ugly" vs. competitors; suggests hiring a professional designer. | **Medium** — multiple UX polish issues (#1920, #1921) were filed suggesting iterative (not wholesale) UI improvements. |
| **Hermes Agent Integration** | [#1880 (closed)](https://github.com/netease-youdao/LobsterAI/issues/1880) | Request to integrate Hermes Agent alongside OpenClaw as an agent option (referencing Open WebUI's pattern). | **Low** — project appears committed to OpenClaw as the core runtime. |
| **OpenHuman Engine Support** | [#2016 (closed)](https://github.com/netease-youdao/LobsterAI/issues/2016) | Brief request to add the "openhuman" engine. | **Low** — no elaboration or use case provided. |
| **OpenClaw Gateway Events** | [#2036 (closed)](https://github.com/netease-youdao/LobsterAI/issues/2036) | Ask for `agent:turn` / `agent:loop` events to enable real-time state persistence. | **Medium** — aligns with ongoing reliability work (#2234). |
| **Dreaming Schema Fix** | [#2039 (closed)](https://github.com/netease-youdao/LobsterAI/issues/2039) | Documented upstream OpenClaw bug where `/dreaming on` writes config to paths memory-core doesn't recognize; suggests schema update. | **Medium** — likely to be addressed upstream and then ported. |

**Prediction:** The next version will likely include **substantial agent memory improvements** (given #2046's alignment with existing roadmap) and **continued cron/yield stabilization** (continuing #2234's work). The model-routing issue (#1988) may force a priority fix, as it directly impacts third-party paid plan users.

---

## 7. User Feedback Summary

Real pain points expressed by users in the last 24h of activity:

- **Configuration fragility:** Users report that manual config changes (plugin paths, model routing) are silently overwritten by the system, making it impossible to customize integrations (PR #1879 fixes this for plugin paths; #1988 remains for model routing).
- **Streaming/rendering race conditions:** "Task completes but nothing shows up" (#1849) and scroll crashes with large rendered elements (#1971) point to a generally fragile task-runtime-UI pipeline.
- **Paid access friction:** Member login failures (#1903) preventing access to paid NetEase models is a quality gate issue that undermines the product's value proposition.
- **Setup blockers:** Local build issues (#2017: missing runtime detection) and WeChat IM verification (#1878: missing input UI) create onboarding and channel-adoption friction.
- **UI polish dissatisfaction:** Direct criticism about aesthetics (#1836) reinforced by specific UI elaboration requests (#1920, #1921).

**Satisfaction signals:** The project's attentive maintenance of stale issues, rapid closure of duplicate/unresolvable items, and the **two meaningful PR merges today** addressing real community pain points suggest a responsive maintainer team — a positive signal for user trust.

---

## 8. Backlog Watch

Items remaining open and needing maintainer attention:

| Item | Type | Age | Why It Matters |
|------|------|-----|----------------|
| [#1903 (open)](https://github.com/netease-youdao/LobsterAI/issues/1903) | Issue | ~3 months (since 2026-05-07) | **Blocks paid users.** Login failures prevent access to paid NetEase models. No maintainer response visible. High customer-impact. |
| [#2046 (open)](https://github.com/netease-youdao/LobsterAI/issues/2046) | Issue | ~3 months (since 2026-05-25) | **Strategic roadmap item.** Comprehensive memory system proposal. Left open suggests internal deliberation, but should be formally triaged or acknowledged. |
| [#2164, #2165, #2166, #2167 (open)](https://github.com/netease-youdao/LobsterAI/issues/2164) | Dependabot PRs | ~2 months (since 2026-06-15) | **Security & maintenance debt.** Four CI dependency bumps (trufflehog, checkout, paths-filter, actions/stale) pending review for 2+ months. Stale-label risk compounds; these should be processed to avoid CI breakage. |

---

## Project Health Verdict

**Status: STABLE BUT QUIET.** The project is actively consolidating — closing old issues, merging targeted fixes, and maintaining dependencies — but is **not shipping new features or releases** this period. The two merged PRs (#2234, #1879) are substantive, technically sound fixes that speak to a healthy engineering discipline. The persistent open issues (login, model routing, memory roadmap) represent opportunities for the next release to make a significant impact on user experience and retain paying customers.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-16

## 1. Today's Overview

Moltis is in a period of moderate, focused activity. The repository shows zero open issues being actively updated in the last 24 hours, but a steady stream of six pull requests touched the codebase in the same window. Three PRs were merged/closed (a bug fix for ClawHub search, a UX enhancement for command-palette chats, and an OpenAI API routing fix), while three remain open, targeting infrastructure expansion (remote workspace sandboxes, connector persistence, and Slack integrations). No new releases were published during this period. Overall, the project exhibits healthy, steady development with a clear emphasis on integration depth and platform reliability.

## 2. Releases

No new versions were tagged or released in the last 24 hours. The most recent release remains the previous one, with no migration notes or breaking changes to report for today.

## 3. Project Progress

**Three PRs were merged/closed today, representing a mix of bug fixes and feature work:**

- **[#1196 — Fix ClawHub skill search results (Merged)](https://github.com/moltis-org/moltis/pull/1196):** Addresses a performance regression in ClawHub skill search. The fix removes per-result metadata requests that were pushing the search beyond the RPC timeout, and streamlines owner-qualified references through detail, scan, download, and install flows.

- **[#1197 — Start agent chats from command palette (Merged)](https://github.com/moltis-org/moltis/pull/1197):** Adds a UX enhancement where "Ask agent" appears as the final item in non-empty command-palette queries. It creates a fresh chat session and immediately sends the query, with proper session-tracking throughout the chat lifecycle.

- **[#1198 — Route OpenAI reasoning tool calls through Responses (Merged)](https://github.com/moltis-org/moltis/pull/1198):** Improves OpenAI integration by routing requests that combine function tools with `reasoning_effort` through the Responses API, while preserving Chat Completions behavior for other cases. This ensures consistent construction of Responses requests across streaming and non-streaming paths.

## 4. Community Hot Topics

Given the current zero-issue environment and limited comment activity on PRs, no single discussion has dominated the conversation today. However, the three open PRs represent the most substantive ongoing community and contributor attention:

- **[#1199 — Add Coder remote workspace sandbox support (Open)](https://github.com/moltis-org/moltis/pull/1199):** The newest PR today, adding a Coder sandbox backend with ephemeral workspaces via REST API and reconnecting PTY WebSockets. Supports templates, presets, parameters, and TTLs — signaling a growing need for flexible, ephemeral remote environments.

- **[#1190 — Add durable calendar, channel, and email connectors (Open)](https://github.com/moltis-org/moltis/pull/1190):** A substantial PR that introduces provider-neutral connector persistence with atomic snapshots, scheduling, projections, and local full-text search. The scope suggests the community is pushing for Moltis to serve as a more durable, PIM-oriented integration hub.

- **[#1195 — Add Slack native live task cards (Open)](https://github.com/moltis-org/moltis/pull/1195):** Enhances the Slack experience with native plan/task cards in the response stream, complete with opaque per-run IDs for privacy. It addresses a clear user need for structured, real-time task visibility in collaboration tools.

## 5. Bugs & Stability

**One bug was fixed today, with no new bugs reported in the open issue tracker:**

- **[#1196](https://github.com/moltis-org/moltis/pull/1196):** ClawHub skill search hitting RPC timeouts due to excessive per-result metadata requests. **Severity: Moderate (functional regression in search usability).** Fixed in the merged PR.

No crashes, regressions, or security-related issues were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals

While no explicit user feature requests arrived in the last 24 hours, the open PRs give a clear view of where the project is heading:

- **Ephemeral remote sandboxes (#1199):** The Coder backend signals an intent to support development in disposable cloud workspaces, a common pattern in modern AI-assisted development tools.
- **Deep integration connectors (#1190):** Durable calendars, channels, and email connectors suggest Moltis is maturing into a persistent workspace hub, not just a chat assistant.
- **Native platform UX (#1195):** Slack native cards point toward platform-specific UI polish, likely to be followed by similar treatment for other ecosystems.

Predictions: #1199 (Coder sandbox) is the most likely candidate for inclusion in the next release, given its recent creation and narrow scope. #1190 is substantial and may take longer to merge but remains a strong roadmap anchor.

## 7. User Feedback Summary

Feedback channels are currently quiet — no issues and no comments on today's PRs. Indirect signals from the codebase, however, indicate the following user-facing pain points being actively addressed:

- **Search responsiveness:** The ClawHub search fix (#1196) directly addresses a frustrating delay in skill discovery.
- **Streamlined workflow initiation:** The command-palette "Ask agent" addition (#1197) reduces friction in starting new conversations.
- **Reliable AI execution across providers:** The OpenAI Responses API routing fix (#1198) improves compatibility for users pairing reasoning models with tools.

Satisfaction appears stable, with contributors actively resolving edge cases rather than the community raising new grievances.

## 8. Backlog Watch

No stagnant or long-unanswered issues are present in the current backlog — the open issue tracker is entirely empty. For pull requests, the longest-standing open item remains:

- **[#1190 — Add durable calendar, channel, and email connectors](https://github.com/moltis-org/moltis/pull/1190):** Created 2026-08-11, it has not received comments and may need a maintainer review pass. Its breadth could be a factor; consider whether it should be split or fast-tracked for community visibility.

Continue monitoring #1190's review status, as well as the integration of #1199 and #1195, which are poised to shape Moltis' direction in the coming weeks.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-16

## Today's Overview

CoPaw (QwenPaw) is in an active development cycle with **10 issues updated** (9 open, 1 closed) and **11 PRs updated** (all open, none merged) in the last 24 hours. The project is in a **high-velocity contribution phase**, evidenced by 8 first-time-contributor PRs pending review. Today's activity clusters around **video delivery bugs** (2 issues + 1 fix PR), **CLI correctness** (1 bug + 1 fix PR), and a **broad set of feature requests** spanning console UX, notification callbacks, and plugin permissions. No new releases were cut — the project is likely accumulating changes toward a v2.2.0 milestone.

## Releases

No new releases in the last 24 hours. The latest tagged version remains **v2.1.0** (referenced across today's bug reports).

## Project Progress

**No PRs were merged or closed today.** All 11 PRs remain open and under review. Key PRs that advanced substantive features (awaiting maintainer review):

- **[#6940 — feat(pawapp): add native DataPaw app runtime and durable analysis workspace](https://github.com/agentscope-ai/QwenPaw/pull/6940)** — Large-scope feature adding a native data-analysis app runtime with durable workspaces. Significant architectural addition; awaiting review since Aug 12.
- **[#6302 — feat: unify provider discovery, model metadata, routing, and agent controls](https://github.com/agentscope-ai/QwenPaw/pull/6302)** — Catalog-driven provider model system with runtime model discovery and capability-aware routing. Long-running PR (open since Jul 21).
- **[#7033 — feat(skill-system): dynamic skill loading + auto-unload + frontmatter fix](https://github.com/agentscope-ai/QwenPaw/pull/7033)** — Adds runtime skill lifecycle (load/unload) infrastructure.
- **[#6623 — fix(acp): prevent final text loss when notifications race the prompt response](https://github.com/agentscope-ai/QwenPaw/pull/6623)** — Marked "Under Review"; fixes a race condition that could drop final text in ACP transport.
- **[#7061 — fix(video): deliver tool-result videos on OpenAI Responses API](https://github.com/agentscope-ai/QwenPaw/pull/7061)** — Committed fix directly addressing today's #7059 and #7060 bugs.

## Community Hot Topics

The most-discussed items today (by comment count and cross-referencing):

1. **[Issue #6476 — Matrix end-to-end encryption unavailable (CLOSED)](https://github.com/agentscope-ai/QwenPaw/issues/6476)** — 3 comments. Resolved 21 days after filing, but touches an important integration gap: Matrix E2EE relies on `matrix-nio` + `olm`/`vodozemac` which fail to install cleanly. Community interest in secure channels is evident.

2. **[Issue #3915 — Virtual scrolling for Console WebUI (OPEN, since Apr 28)](https://github.com/agentscope-ai/QwenPaw/issues/3915)** — 3 comments, 1 👍. Long-running performance complaint: full DOM rendering of long conversations causes severe lag. Notably *unaddressed by a fix PR* after 3.5 months.

3. **Video tool-result bugs — [Issue #7059](https://github.com/agentscope-ai/QwenPaw/issues/7059) and [Issue #7060](https://github.com/agentscope-ai/QwenPaw/issues/7060)** (1 comment each) — Both filed the same day by the same reporter, with a fix PR (#7061) submitted by the same author within 24 hours. This signals a real usability blocker: the agent claims success but the model sees nothing.

**Underlying needs:** Community members are actively testing v2.1.0 in production-like settings and hitting gaps in (a) multimodal delivery (video), (b) long-session UX, and (c) integration robustness (Matrix encryption, OAuth2 rotation).

## Bugs & Stability

Ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| 🔴 High | [#7059](https://github.com/agentscope-ai/QwenPaw/issues/7059) | `view_video` tool-result blocks silently dropped — model never receives frames (OpenAI Responses API / Volcengine Ark) | **Yes** — [#7061](https://github.com/agentscope-ai/QwenPaw/pull/7061) |
| 🔴 High | [#7060](https://github.com/agentscope-ai/QwenPaw/issues/7060) | Hardcoded 2MB video inline cap ignores provider's `max_inline_media_bytes` setting | Partially in #7061 (needs config exposure) |
| 🟠 Medium | [#7053](https://github.com/agentscope-ai/QwenPaw/issues/7053) | OAuth2 refresh never persists rotated `refresh_token` + no proactive renewal → remote MCP permanently degrades to manual re-auth | None filed yet |
| 🟠 Medium | [#7051](https://github.com/agentscope-ai/QwenPaw/issues/7051) | Console chat image attachments lost on session reload (backend serves data URL, frontend shows broken thumbnail) | None filed yet |
| 🟡 Low | [#7048](https://github.com/agentscope-ai/QwenPaw/issues/7048) | `qwenpaw cron update --text` returns success but prompt not updated for agent-type jobs (CLI silent failure) | **Yes** — [#7055](https://github.com/agentscope-ai/QwenPaw/pull/7055) |

**Stability assessment:** The video-path bugs (#7059/#7060) are correctness-critical for multimodal workflows — a silent success-with-no-data failure is the worst class of bug for agent tooling. The OAuth2 rotation bug (#7053) will progressively degrade all remote MCP integrations using rotating tokens. Notably, **no fix has been filed yet for #7053 or #7051**, and the fix for #7055 is pending review.

## Feature Requests & Roadmap Signals

Requests filed today (all on Aug 15):

1. **[#7058 — Restore native context strategy option in web UI](https://github.com/agentscope-ai/QwenPaw/issues/7058)** — v2.1.0 removed the `native` context-strategy selector; backend still supports it (`LightContextConfig.strategy: Literal["native", "scroll"]`). Regression in UI capability.

2. **[#7056 — Background task callback / notification mechanism](https://github.com/agentscope-ai/QwenPaw/issues/7056)** — `submit_to_agent` only supports polling (`check_agent_task`); user wants push notifications. Aligns with growing async-agent usage patterns.

3. **[#7052 — Plugin API system_prompt permission](https://github.com/agentscope-ai/QwenPaw/issues/7052)** — Enterprise use case: companies want to inject system prompts via plugin API without exposing them in the conversation UI. Signals B2B adoption.

4. **[#7048 (bug) → PR #7055 (fix)](https://github.com/agentscope-ai/QwenPaw/pull/7055)** — CLI correctness demand for cron management.

**Predictions for v2.2.0:** Video-cap configuration (#7060), cron model override picker (#7050, ready for review), and chat pagination (#7049) are the most likely candidates — all have open PRs awaiting merge.

## User Feedback Summary

- **Video workflows are broken or constrained:** Two reports from a power user (xiaoka76) show that the agent *claims* success but the model gets nothing — this erodes trust in the tool's multimodal claims.
- **Chinese-speaking users are highly active** (7 of 10 issues in Chinese), indicating strong adoption in Chinese-speaking markets. Three distinct users report issues (cron update, OAuth2, plugin system_prompt) — one particularly mentions a **company scenario** with proprietary prompts, suggesting B2B/enterprise trials.
- **The Matrix E2EE issue (#6476)** was eventually resolved (closed today) but illustrates friction in secure-channel setups.
- **No overt praise or frustration threads among the sampled issues** — tone is pragmatic, report-and-fix oriented.

## Backlog Watch

Issues/PRs requiring maintainer attention:

1. **[Issue #3915 — Virtual scrolling for Console WebUI (OPEN — 111 days)](https://github.com/agentscope-ai/QwenPaw/issues/3915)** — Long-standing performance complaint with no fix PR. Community has been waiting over 3.5 months for a UI responsiveness improvement on long conversations.

2. **[PR #6302 — Unify provider discovery/model routing (OPEN — 26 days)](https://github.com/agentscope-ai/QwenPaw/pull/6302)** — Major architectural PR, silent since Jul 21 (updated today without comments). Large diffs tend to stall; maintainer triage needed to avoid losing the contribution.

3. **[PR #6940 — DataPaw native app runtime (OPEN — 4 days)](https://github.com/agentscope-ai/QwenPaw/pull/6940)** — Large feature with infra references; first-time contributor. Needs maintainer response to signal engagement.

4. **[Issue #7053 — OAuth2 refresh token rotation (OPEN — 1 day)](https://github.com/agentscope-ai/QwenPaw/issues/7053)** — No fix PR filed; will compound for all rotating-token MCP providers (XMind explicitly named). High-impact bug deserving maintainer attention.

---

*Data sources: GitHub issues and PRs for agentscope-ai/CoPaw, updated 2026-08-16.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest
**2026-08-16**

---

## 1. Today's Overview

ZeroClaw is in a period of intense architectural activity, with high engineering throughput and a focus on foundational RFCs, security hardening, and provider reliability. Activity over the last 24 hours was very high: 50 issues and 50 PRs were updated, with 6 PRs merged/closed and a handful of issues resolved. The project shows strong, sustained momentum but is accumulating a significant queue of high-risk RFCs (many marked `risk:high`) that require maintainer decisions. Key themes dominating the tracker include runtime-owned conversation sessions (#9487), unified attachment architecture (#9488), security posture and credential boundaries (#6971), and multi-layered Anthropic fallback handling (PRs #9262-#9272). There were no new releases today, indicating the project may be focusing on consolidating features for a future minor release (v0.9.0 is referenced as a target for the SOP authorization contract). Overall project health looks robust, with a mature CI process, a well-defined RFC lifecycle (including a maintainer decision tracker #8692), and a strong roster of "distinguished contributors" driving large, well-scoped PRs.

---

## 2. Releases

No new releases were published in the last 24 hours. There is no new version, breaking change, or migration note to report. The last release remains the one prior to this digest window.

---

## 3. Project Progress

Today's merged/closed PRs — 6 total — all focus on **Anthropic server-side fallback and refusal handling**. A coordinated stack of PRs from contributor `IftekharUddin` was merged, completing an end-to-end feature:

- **PR #9262** (merged): Surface native Anthropic refusals as typed errors. HTTP 200 refusals with `stop_reason: "refusal"` are now correctly classified instead of being treated as empty successes. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9262)
- **PR #9263** (merged): Route refusals through client-side fallback entries, adding `is_non_retryable` classification so the reliability layer handles refusals correctly. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9263)
- **PR #9265** (merged): Adds opt-in Anthropic **server-side** fallback requests via a new config field `server_fallback_models` on `[providers.anthropic]`. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9265)
- **PR #9266** (merged): Detects server-side fallback responses by reading native response signals (`NativeChatResponse.model` and `AnthropicUsage.iterations`). [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9266)
- **PR #9268** (merged): Surfaces safeguard fallback notices in the channel orchestrator, closing the loop on the fallback stack. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9268)

This feature set significantly improves reliability and user experience when working with Anthropic's models, especially in cases of content refusals or service-side degradation. It also makes fallback behavior transparent to the end user.

Beyond merged PRs, several large, open PRs continue to advance important features (not merged today but active):

- **PR #8337** (`feat(observability): herdr agent reporting integration`) — Opt-in Herdr lifecycle reporting for the interactive CLI, reusing observer events. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/8337)
- **PR #9002** (`fix(gateway): keep agent turns alive after viewer disconnect`) — P1 fix to treat dashboard WebSocket as a viewer/controller, not an owner, preventing data loss on disconnect. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9002)
- **PR #9739** (`feat(zerocode): multi-session panes`) — Large feature adding multi-session panes and an agent sidebar to the terminal UI. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9739)

---

## 4. Community Hot Topics

The most active discussions (by comment count) all involve high-stakes architectural RFCs, indicating a community deeply engaged in proactive design:

- **#8603 — RFC: ZeroClaw Chat Completions profile** (20 comments). Author: `REL-mame`. This is the most active issue. The proposal would expose agent capabilities via the OpenAI Chat Completions protocol, enabling clients like Open WebUI, LobeChat, Continue.dev, Aider, and LangChain to use ZeroClaw. The high engagement signals strong community desire for ecosystem interoperability. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)

- **#9487 — RFC: Runtime-owned conversation sessions and transport surface adapters** (17 comments). Author: `NiuBlibing`. This is part of a broader architecture overhaul, creating a unified session ownership model across all transport surfaces. The scope and revision history show deep, detailed discussion. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9487)

- **#9488 — RFC: Unified attachment architecture for web chat and channels** (16 comments). Author: `NiuBlibing`. Companion to #9487, addressing how files and media are handled consistently. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)

- **#8692 — [Tracker]: Maintainer decision queue for RFCs and design issues** (13 comments). Author: `Audacity88`. This tracker is itself a hot topic, serving as the clearing house for pending decisions. The fact it's highly active reflects a potential bottleneck: the maintainer team may be the gating factor on the many `needs-maintainer-review` issues. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)

- **#6954 — RFC: Provenance, conversation binding, and reply contract for internally initiated agent turns** (12 comments). Author: `mov-xound-glitch`. Details the complex contract for agents triggered by cron or other non-user initiators. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)

- **#6971 — RFC: Security posture, credential boundaries, and universal ingress policy** (12 comments). Author: `Audacity88`. A broad, security-focused RFC aiming to make the system's security controls inspectable. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6971)

- **#9103 — RFC: separate authoritative memory storage from optional enrichment connectors** (12 comments). Author: `yanchenko`. A data-model RFC addressing the conflation of core memory with optional connectors like Lucid. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9103)

- **#8780 — RFC: Realtime speech-to-speech channel for Gemini Live** (11 comments). Author: `metalmon`. Recently revised to a broker contract, showing responsiveness to community feedback. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)

**Analysis:** The community is pushing heavily for (a) ecosystem compatibility (OpenAI protocol), (b) architectural clarity (sessions, attachments, memory), and (c) security visibility. The underlying need is for ZeroClaw to become a more open, more standard-compliant platform rather than a closed, proprietary agent runtime.

---

## 5. Bugs & Stability

Several new or updated bug reports and stability fixes were active today. Ranked by severity:

- **High Priority (P1):**
    - Issue **#7527** (closed): "[Bug]: macOS desktop app can reopen blank or without a window" — Critical S1 workflow-blocking bug. Was closed today, possibly due to a workaround or duplicate. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)
    - PR **#9002** (open): "fix(gateway): keep agent turns alive after viewer disconnect" — Addresses a P1 bug where work was cancelled if the web UI was closed or lost connectivity. On hold awaiting author action. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9002)
    - PR **#9320** (open): "fix(cron): bound agent job runs with a wall-clock timeout" — Addresses a P1 bug where hung cron jobs held locks indefinitely. On hold awaiting author action. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9320)
    - PR **#9753** (open): "fix(config): distinguish absent vs empty risk-profile allowed_tools" — Addresses a P1 security-relevant bug where an explicit empty list `[]` failed open instead of denying all tools. On hold awaiting author action. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9753)
    - PR **#9995** (open): "fix(hooks): harden webhook audit exports" — Addresses a P1 bug where credentials could leak into webhook audit exports. On hold awaiting author action. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9995)

- **Medium Priority (P2):**
    - Issue **#9965** (open): "[Task]: cron custom-shell test hits ETXTBSY" — A flaky test causing unrelated PRs to fail, a CI stability issue. [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)

- **Stability Fixes:**
    - PR **#9954** (open): "fix(sop): unwrap a double-encoded step output" — Fixes a schema validation issue in SOP workflows. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9954)
    - PR **#9957** (open): "fix(sop): record why a failed run failed" — Improves diagnostics for SOP failures. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9957)

**Ranking:** The P1 issues are dominated by PRs that are ready but stuck on `needs-author-action`. This is a potential cause for concern, as they address stability and security-critical bugs.

---

## 6. Feature Requests & Roadmap Signals

The most significant roadmap signals come from the RFCs and feature requests currently under discussion. A set of features are likely candidates for upcoming releases (likely v0.9.x):

- **Interoperability:** The strongest signal is the RFC for a **Chat Completions profile** (#8603). If accepted, this is a major step toward platform ubiquity. It might not be in the *next* release given its complexity, but it's a strong candidate for the version after.
- **Architecture Overhaul:** The trio of #9487 (Runtime-owned sessions) and #9488 (Unified attachments) represent a large refactor. These are likely to land incrementally over several releases.
- **SOP (Standard Operating Procedure) Milestone:** The tracker #8288 shows a plan to bring the SOP capability to "5/5" (done). This is likely a near-term goal, targeting v0.9.0 per RFC #9598.
- **CI/Dev Experience:** Several proposals aim to automate PR labeling (#9345, PR #9867) and add AI-assisted PR pre-review (#9330). These are likely near-term improvements to the contributor experience.
- **New Channels & Capabilities:**
    - **Realtime voice (Gemini Live)** — RFC #8780, a significant new channel type.
    - **Computer-use support** — RFC #6909, allowing desktop screen interaction.
    - **Agent Plugins standard** — RFC #9810, to load community plugins (`plugin.json` + `skills/` + `mcp.json`).
    - **PowerShell/Git Bash support** — Issue #7089, to make the Windows shell host configurable.
    - **Discord thread mode** — Issue #7849, to prevent conversation takeover in shared channels.

**Prediction:** The most likely features for the *next* release are the **SOP 5/5 completion**, the **Discord thread mode**, **PowerShell/Git Bash config**, and **AI-assisted PR pre-review**. These are all scoped, accepted, and some are already in progress.

---

## 7. User Feedback Summary

- **Pain Point: Anthropic Refusals and Fallbacks.** A coordinated stack of PRs (#9262-#9268) addresses user-facing reliability around Anthropic's content refusals and server-side fallbacks. Users likely experienced silent failures or opaque error messages, and this feature set makes the behavior transparent and resilient.

- **Pain Point: Losing work on disconnect (Web/Mac).** The P1 PR #9002 (keep agent turns alive after viewer disconnect) and the closed Mac bug #7527 highlight that users are frustrated by losing long-running agent work due to UI or network disconnects.

- **Pain Point: Cron Configuration and Documentation.** Issue #7762 shows that users want to run scheduled jobs with specific (cheaper) models but cannot, and they find the cron documentation missing. This is a direct request for more flexibility and better docs.

- **Pain Point: Windows Shell Limitations.** Issue #7089 suggests that the default `cmd.exe` shell is a limitation for power users who prefer PowerShell or Git Bash.

- **Pain Point: Connection Leak Detector False Positives.** Issue #9825 indicates that the security-focused leak detector is blocking legitimate use cases like payment-request URLs containing public blockchain addresses. Users need safe exceptions.

- **Satisfaction/Engagement:** The high level of contribution from "distinguished contributors" (`IftekharUddin`, `Audacity88`, `NiuBlibing`) and the detailed, revision-controlled RFC discussions indicate a healthy and highly engaged contributor community.

---

## 8. Backlog Watch

A significant number of issues and PRs are marked with `needs-author-action` and `needs-maintainer-review`. The following are important items waiting for attention:

- **Maintainer Decision Queue (the biggest bottleneck):**
    - **#8692 - [Tracker]: Maintainer decision queue for RFCs and design issues** is the central hub. It's actively used, but many RFCs are piling up. High-priority, high-risk RFCs waiting for review include:
        - **#6954 - RFC: Provenance and reply contract for internally initiated agent turns** (12 comments, waiting for maintainer review). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6954)
        - **#6971 - RFC: Security posture and universal ingress policy** (12 comments, waiting for maintainer review). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/6971)
        - **#9598 - RFC: Define the SOP capability permission contract** (waiting for maintainer review). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9598)
        - **#9621 - RFC: staged opt-in product telemetry** (waiting for maintainer review). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9621)
        - **#8603 - RFC: ZeroClaw Chat Completions profile** (the most active, waiting for maintainer review). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)

- **P1 Bug-Fix PRs stuck on `needs-author-action` (Requiring contributor response):**
    - **PR #9002** (P1, keep agent turns alive) — waiting on author. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9002)
    - **PR #9320** (P1, cron lock timeout) — waiting on author. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9320)
    - **PR #9753** (P1, security fail-open) — waiting on author. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9753)
    - **PR #9995** (P1, webhook audit secrets) — waiting on author. [Link](https://github.com/zeroclaw-labs/zeroclaw/pull/9995)

- **Other Items Waiting:**
    - **#9330 - RFC: AI-assisted PR pre-review** (needs author action). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9330)
    - **#9810 - RFC: Load Agent Plugins 1.0 standard** (needs author action). [Link](https://github.com/zeroclaw-labs/zeroclaw/issues/9810)

---

**Digest Prepared:** August 16, 2026
**Data Source:** GitHub (zeroclaw-labs/zeroclaw)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*