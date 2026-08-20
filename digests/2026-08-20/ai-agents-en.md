# OpenClaw Ecosystem Digest 2026-08-20

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-20 00:30 UTC

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

Based on the GitHub data provided for OpenClaw (github.com/openclaw/openclaw), here is the project digest for 2026-08-20.

---

### 1. Today's Overview

OpenClaw shows extremely high activity, with 500 issues and 500 PRs updated in the last 24 hours. The project is in a heavy maintenance phase, processing a significant backlog of bugs and feature requests, with approximately 93 PRs merged or closed in this period. The issue tracker is dominated by P1 and P2 severity bugs, many flagged with the [`clawsweeper:needs-maintainer-review`](https://github.com/openclaw/openclaw/labels/clawsweeper%3Aneeds-maintainer-review) and [`clawsweeper:needs-product-decision`](https://github.com/openclaw/openclaw/labels/clawsweeper%3Aneeds-product-decision) labels, indicating a triage bottleneck. While no new releases were published today, the high volume of merged PRs and the presence of release validation issues (e.g., [#125626](https://github.com/openclaw/openclaw/issues/125626)) suggest active preparation for upcoming patches.

---

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Project Progress

Approximately 93 pull requests were merged or closed today. Key areas of progress identified from the top PRs include:

- **UI/UX Fixes:** Several fixes for the Web UI were merged, including dismissing session hovercards before menus open ([#126345](https://github.com/openclaw/openclaw/pull/126345)) and adding the ability to review and acknowledge install policy warnings in the Control UI ([#120900](https://github.com/openclaw/openclaw/pull/120900)).
- **State & Migration Stability:** A critical fix was merged to restore upgrades from `2026.7.2-beta.4` agent state, addressing a Doctor/Gateway startup mismatch ([#126354](https://github.com/openclaw/openclaw/pull/126354)).
- **Cron & Alerting:** A fix was merged to honor failure alert thresholds, preventing alert storms for failing automations ([#126483](https://github.com/openclaw/openclaw/pull/126483)).
- **Security & Policy:** A significant feature was merged to require acknowledgement for security.installPolicy warning, enhancing operator oversight on suspicious installs ([#116489](https://github.com/openclaw/openclaw/pull/116489)).
- **Performance:** Work continues on hardening the bootstrap-context event loop and adding substage timing for better performance diagnostics ([#89040](https://github.com/openclaw/openclaw/pull/89040)).

---

### 4. Community Hot Topics

The most active discussions, indicated by high comment counts, focus on severe reliability issues:

- **[#116201: Realtime voice work can retain unbounded provider and consult state](https://github.com/openclaw/openclaw/issues/116201)** (60 comments): The highest-activity issue, centered on resource management and potential memory leaks in realtime voice sessions.
- **[#44925: Subagent completion silently lost — no retry, no notification](https://github.com/openclaw/openclaw/issues/44925)** (26 comments): A long-running, critical issue about silent data loss in subagent task orchestration, which continues to attract user attention.
- **[#77598: Track live dev agent behavior and trajectory](https://github.com/openclaw/openclaw/issues/77598)** (22 comments): A running observational log of a developer agent, serving as a real-world field test and generating insights into agent behavior.
- **[#62505: Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)** (15 comments): A P1 regression where the coding agent becomes unresponsive, causing significant user frustration.

The underlying need in these hot topics is clear: **reliability and trust**. Users are deeply concerned about silent failures, data loss, and unresponsive agents, which undermine the core value proposition of an autonomous AI assistant.

---

### 5. Bugs & Stability

Severity is high, with multiple P0 and P1 regressions reported or updated today:

- **P0 Crash-Loop & Startup Failures:**
    - [#108435](https://github.com/openclaw/openclaw/issues/108435): Gateway fails to start after update to 2026.7.1 (`Error: gateway did not start`).
    - [#70903](https://github.com/openclaw/openclaw/issues/70903): Persistent file-based provider cooldown blocks users for hours after billing recovery.
- **P1 Data Loss & Message Loss (Critical):**
    - [#44925](https://github.com/openclaw/openclaw/issues/44925): Subagent results are silently lost on timeout/failure.
    - [#40001](https://github.com/openclaw/openclaw/issues/40001): `write` tool lacks append mode, causing cron sessions to overwrite and destroy shared files.
    - [#94939](https://github.com/openclaw/openclaw/issues/94939): State migration leaves MS Teams conversation store empty, breaking proactive sends.
    - [#123360](https://github.com/openclaw/openclaw/issues/123360): Memory-core dreaming discards successful narratives and writes fallback placeholders.
- **P1 Session-State & Regression Issues:**
    - [#62505](https://github.com/openclaw/openclaw/issues/62505): A regression where the Coding Agent never completes tasks.
    - [#115546](https://github.com/openclaw/openclaw/issues/115546): CLI-budget compaction fails 100% of the time with timeouts firing far below the deadline, leading to a "death-spiral".
    - [#114234](https://github.com/openclaw/openclaw/issues/114234): Usage-cost refresh lock permanently freezes in containers due to PID reuse.

**Fix PRs exist for many of these:** For instance, fixes are in progress for the events around [#111498](https://github.com/openclaw/openclaw/issues/111498) (workspace-state migration), [#119796](https://github.com/openclaw/openclaw/issues/119796) (Windows test teardown bug), and [#114234](https://github.com/openclaw/openclaw/issues/114234) (usage-cost lock). The volume of `clawsweeper` bot labels combined with P1 status suggests a pipeline that successfully identifies issues but is overwhelmed by the number requiring human intervention.

---

### 6. Feature Requests & Roadmap Signals

Several feature requests with significant user interest were updated today:

- **[#9016: Expose OpenRouter usage cost to agent runtime](https://github.com/openclaw/openclaw/issues/9016)**: Users want cost transparency in their agent interactions, indicating a desire for better cost-management tools.
- **[#60572: Multi-Slot Memory Architecture](https://github.com/openclaw/openclaw/issues/60572)**: This request to support multiple simultaneous memory providers suggests the current single-slot plugin limit is seen as a bottleneck for advanced users.
- **[#63930: Support Anthropic advisor tool](https://github.com/openclaw/openclaw/issues/63930)**: A call to integrate new server-side tools from providers, showing the community proactively tracks upstream model capabilities.
- **[#56781: Feature request: fallback model chain for compaction and LCM summaryModel](https://github.com/openclaw/openclaw/issues/56781)**: Users want resilience against single-model failures, reinforcing the dominant theme of reliability.

**Prediction:** The volume and persistence of issues around state management, data loss, and provider reliability suggest the **next version will strongly focus on hardening the core execution and state-persistence layers**. The "Multi-Slot Memory Architecture" and cost-tracking features are more speculative but have enough support to be scheduled soon.

---

### 7. User Feedback Summary

A clear pattern of user pain points emerges from the issue activity:

- **Silent Failures & Data Loss:** The most common and severe complaint. Users repeatedly report scenarios where the agent fails silently, loses data ([#44925](https://github.com/openclaw/openclaw/issues/44925), [#40001](https://github.com/openclaw/openclaw/issues/40001)), or stops responding without explanation ([#62505](https://github.com/openclaw/openclaw/issues/62505)). This creates a crisis of confidence in the system's reliability.
- **Fragile State and Migrations:** Users upgrading OpenClaw frequently hit regressions related to state migration and auth recovery ([#108435](https://github.com/openclaw/openclaw/issues/108435), [#111498](https://github.com/openclaw/openclaw/issues/111498)). This friction with the update process discourages users from staying on the latest version.
- **Cross-Platform Inconsistencies:** Several bugs are exclusive to Windows or macOS, such as issues with file locks on Windows ([#119796](https://github.com/openclaw/openclaw/issues/119796)) and failed memory detection on macOS ([#47273](https://github.com/openclaw/openclaw/issues/47273)), indicating a need for more robust cross-platform testing.

---

### 8. Backlog Watch

Some critical issues have been open for a long time and continue to gather attention, indicating significant impact and strategic importance:

- **[#70903: Persistent file-based provider cooldown blocks user for hours after billing recovery](https://github.com/openclaw/openclaw/issues/70903)** (Created 2026-04-24): A P0 issue causing prolonged lockouts even after a user fixes the root cause (e.g., billing). The label `needs-product-decision` suggests this has been waiting for a design choice for nearly 4 months.
- **[#44925: Subagent completion silently lost](https://github.com/openclaw/openclaw/issues/44925)** (Created 2026-03-13): A P1 stability bug with 26 comments and no fix PR, representing a major gap in task orchestration reliability.
- **[#16670: Onboarding Wizard should include Memory/Embedding setup as a mandatory step](https://github.com/openclaw/openclaw/issues/16670)** (Created 2026-02-15): A UX friction issue where a core feature is easy to miss during setup, leading to user confusion and feature underutilization. It, too, is awaiting a product decision.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant & Agent Open-Source Ecosystem

**Date:** 2026-08-20

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by intense, sustained development activity across a spectrum of projects ranging from core infrastructure (OpenClaw) to niche specialized agents (PicoClaw, NullClaw). The dominant themes are reliability hardening and stability, with the most active projects (OpenClaw, NanoBot, Hermes Agent, CoPaw, ZeroClaw) all processing hundreds of issues and PRs daily. While feature development continues, the community's collective voice is increasingly focused on addressing silent failures, data integrity, cross-platform consistency, and resilient upgrade paths. No project published a new release on August 20, suggesting a consolidation phase where teams are merging fixes ahead of future patch releases or milestones.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs | New Releases | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | ~93 | None | 🟡 Active, triage bottleneck |
| **NanoBot** | 5 | 24 | 8 | None | 🟢 Healthy, responsive |
| **Hermes Agent** | 41 (open) | 42 (open) | 8 | None | 🟡 Fragile delivery, responsive dev |
| **PicoClaw** | 1 closed | 2 | 2 (1 merge) | None | 🟢 Stable, low activity |
| **NanoClaw** | 3 new | 34 | 25 | None | 🟢 Highly productive |
| **NullClaw** | 0 | 1 | 0 | None | 🟢 Stable, minimal activity |
| **IronClaw** | 14 | 38 | 16 | v1.3.0 (yesterday) | 🟢 High velocity, feature push |
| **LobsterAI** | 0 new | 8 merged | 8 | None (2026.4.3 latest) | 🟡 Stable dev, stale issues |
| **TinyClaw** | — | — | — | — | ⚪ Inactive (24h) |
| **Moltis** | 3 bugs closed | 10 | 5 | 20260818.10 (Aug 18) | 🟢 Responsive, security-focused |
| **CoPaw** | 50 | 47 | 17 | None (2.1.0 latest) | 🟡 High velocity, trust issues |
| **ZeptoClaw** | — | — | — | — | ⚪ Inactive (24h) |
| **ZeroClaw** | 42 | 50 | 2 | None (v0.8.4 latest) | 🟡 Intense, architectural focus |

*Health Score: 🟢 Green (stable, responsive), 🟡 Yellow (active but with bottlenecks/friction), 🔴 Red (critical issues), ⚪ (no activity)

---

## 3. OpenClaw's Position

**Advantages:**
- **Unmatched community scale:** With 500 issues and 500 PRs updated in 24 hours, OpenClaw operates at 10-20x the activity level of its nearest peers (CoPaw, ZeroClaw, IronClaw). This translates to a larger contributor pool, faster bug discovery, and a more mature ecosystem of plugins and integrations.
- **Comprehensive feature surface:** OpenClaw addresses the full spectrum of personal AI needs — voice, coding, memory, multi-channel (Teams, Slack, Discord), and a rich Web UI — whereas peers often specialize (e.g., NanoClaw on Slack/Telegram, IronClaw on sandboxing).
- **Active state-migration and reliability engineering:** The project demonstrates a deep commitment to upgrade-path stability (e.g., fix for `2026.7.2-beta.4` agent state) and engages with the community through a dedicated `clawsweeper` bot.

**Technical Approach Differences:**
- OpenClaw's architecture appears more monolithic and feature-integrated compared to NanoBot's lightweight modularity and ZeroClaw's Rust-based, plugin-driven design.
- Its memory system ("multi-slot" architecture) is more ambitious than NanoBot's or PicoClaw's simpler approaches.

**Community Size Comparison:**
- OpenClaw's community is likely 50-100x larger than smaller projects like NullClaw or PicoClaw, as evidenced by the sheer volume of daily interactions.

**Challenges:**
- The sheer volume of issues creates a **triage bottleneck**, with many critical P1/P0 bugs marked `needs-maintainer-review` or `needs-product-decision` for extended periods (up to 4 months, e.g., #70903). This can erode user trust despite the project's overall progress.

---

## 4. Shared Technical Focus Areas

Across projects, several systemic requirements are emerging:

| Need / Requirement | Projects (Examples) | Evidence |
|---|---|---|
| **Reliability: Silent Failure Elimination** | OpenClaw (#44925, #62505), CoPaw (#7102), LobsterAI (#1569), Hermes Agent (#66616) | Users demand no silent data loss, unresponsive agents, or hidden stream stalls. |
| **Upgrade/Install Path Stability** | Hermes Agent (`hermes update` breaks installs), LobsterAI (v2026.4.3 regressions), CoPaw (#3005 install breaks app) | Fragile update paths destroy trust; `hermes update` is a "release-blocker." |
| **Identity & State Migration** | OpenClaw (MS Teams state empty), Moltis (Apple Container version parsing), LobsterAI (SSE race conditions) | Correct state persistence and migration across versions/platforms is critical. |
| **Fallback Model Chains & Resilience** | OpenClaw (#56781), NanoBot (#5403), CoPaw (#2089), IronClaw (#7600) | Demand for fallback chains to prevent single-model failures from halting workflows. |
| **Cost Transparency & Management** | OpenClaw (#9016), NanoClaw (#5438, #5440) | Users want granular cost tracking and budget-based controls. |
| **Memory/Context Integrity & Scaling** | OpenClaw (#60572 multi-slot), NanoBot (#5440, #5441 compaction), PicoClaw (routed-agent history) | Memory is the most complex and fragile subsystem; users demand accuracy and no data bleed. |
| **Windows as a First-Class Platform** | Hermes Agent (BSOD), ZeroClaw (74 test failures), OpenClaw (file locks) | Cross-platform consistency is a recurring pain point. |
| **Cross-Platform UX Consistency** | Hermes Agent (Desktop-Gateway), CoPaw (mobile UI), LobsterAI (installer fixes) | Users expect a quality experience regardless of device or OS. |

---

## 5. Differentiation Analysis

| Project | Target User | Core Strength | Architecture | Key Trade-off |
|---|---|---|---|---|
| **OpenClaw** | Power users, developers, tinkerers | Extreme feature breadth, massive community | Monolithic, Python-centric | Requires intensive maintenance and triage; complex install/config |
| **NanoBot** | Developers wanting a reliable, lightweight assistant | Focused UX (WebUI/TUI), quick fixes, memory hygiene | Modular, lightweight | Smaller feature surface; limited channel integrations |
| **Hermes Agent** | Developers, enterprise on Windows & Mac | Cross-platform Desktop app, CLI, multi-platform (Discord, webhooks) | Monolithic with salvage-PR workflow | Fragile update pipeline; desktop-gateway integration friction |
| **IronClaw** | Self-hosters, automation-focused users | Sandboxing (Docker), automations, release discipline | Feature-branch, release-candidate pipeline | Smaller community; complex architecture under active development |
| **CoPaw** | Desktop-native users (Windows), multi-channel (Chinese platforms) | Desktop app, multi-channel, local model support | Heavily feature-integrated | Trust issues (data loss, freezes); weak feature request response |
| **ZeroClaw** | Developers building custom agents with ZeroCode | ZeroCode (editor-like UI), WASM plugin architecture, Rust core | Rust high-performance core, plugin-based | Windows support lags; architectural RFCs create decision backlog |
| **NanoClaw** | Slack/Telegram-centric teams | Slack/SMS/voice channel adapters, multi-agent Slack features | Channel-centric | Primarily Slack-focused; setup robustness issues in headless envs |
| **PicoClaw / NullClaw** | Niche, smaller communities | Telegram UX (Pico), star-history README (Null) | Lightweight | Low activity; maintainer bandwidth is a bottleneck |
| **LobsterAI** | Chinese-market users (IM platforms: DingTalk, Feishu, WeChat) | Multi-IM channel support, Windows installer polish | Integration-heavy | Stale issue tracker (4-month gap); version 2026.4.3 has regressions |
| **Moltis** | Developers focused on Apple/WhatsApp/OpenAI ecosystem | Security hardening, modern APIs (Responses API), configurable backends | Modular backend | Narrow channel focus (Apple/WhatsApp) |

---

## 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High Velocity, Large Community)**
- **OpenClaw** — Largest, fastest-moving; triage is the bottleneck.
- **CoPaw** — High issue/PR velocity; user trust is at risk due to unaddressed data-loss reports.
- **ZeroClaw** — Intense architectural development; RFC-driven process; huge potential but needs faster decision-making.

**Tier 2: Stabilizing & Feature-Building (Medium-High Velocity, Balanced Focus)**
- **NanoBot** — Responsive, healthy pace; excellent for a focused tool.
- **IronClaw** — High velocity with disciplined release management; shipping v1.3.0 and prepping v1.4.0.
- **Hermes Agent** — Developer velocity high, but delivery fragility (updates) and Windows issues create friction. Salvage-PR workflow indicates a knowledge-transfer bottleneck.
- **NanoClaw** — Very productive; feature-complete Slack path; community engaged on new channels (Dial, Cursor).

**Tier 3: Low Activity / Stabilized**
- **Moltis** — Healthy, focused sprints; security hardening; stable release cadence.
- **PicoClaw** — Low activity, stable, but needs to merge stale PRs.
- **LobsterAI** — Development active (8 PRs/day) but issue tracker is stale; a patch release is imminent.
- **NullClaw** — Essentially dormant; pending housekeeping PR.

**Tier 4: Inactive (24h)**
- **TinyClaw**, **ZeptoClaw** — No activity in the last 24 hours; potential for stagnation or quiet maintenance.

---

## 7. Trend Signals

1. **Reliability is the #1 battleground.** Across all major projects, users are demanding an end to silent failures. The most successful projects (OpenClaw, NanoBot, Hermes) are explicitly shipping fixes for stalls, data loss, and unresponsive agents. **Value:** AI agent developers must prioritize observability (turn tracking, watchdog timers, explicit error surfaces) over feature breadth.

2. **"Agentic Workflows" require "Agentic Safety."** Features like CoPaw's stalled-stream detection (#7150), OpenClaw's provider fallback chains (#56781), and NullClaw's dependency shift to token-free services (star-history) signal a move toward self-healing, resilient agent loops.

3. **Memory is the new "core."** Projects are investing heavily in memory compaction (NanoBot), multi-slot architectures (OpenClaw), and per-agent knowledge-graph scoping (ZeroClaw). The future belongs to assistants that remember accurately and privately.

4. **Windows support is a differentiator.** The repeated failures on Windows (Hermes BSOD, ZeroClaw CI, OpenClaw file locks) represent a significant opportunity for a project to gain trust by delivering a truly solid Windows experience.

5. **The "desktop app" is becoming mainstream.** Hermes Agent (Desktop), CoPaw (Desktop 2.1.0), and IronClaw (WebUI) are converging on a polished GUI layer that abstracts away the complexities of the agent runtime. Expect this trend to continue.

6. **Community pressure for explicit roadmaps and "won't fix" decisions.** CoPaw's silent closure of high-interest issues (#2089, #2296) and ZeroClaw's decision queue tracker (#8692) show a community demand for transparency. Projects that communicate decisions clearly will retain trust.

---

*Data sources: GitHub issue and PR activity for each project during 2026-08-19 to 2026-08-20 (24-hour window), as summarized above.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-20

## 1. Today's Overview

NanoBot's development pace has intensified significantly over the last 24 hours, with 24 pull requests updated and 5 issues active. The project shows a healthy focus on stability and bug-fixing: 8 PRs were merged or closed, including critical fixes for WebUI timeout behavior, TUI command discoverability, and memory compaction performance. However, a handful of `priority: p0` and `p1` fixes remain open with merge conflicts, indicating that while the community is actively contributing, maintainer bandwidth for conflict resolution may be a bottleneck. Two related issue clusters — around legacy `socks://` proxy support and OAuth failures in Docker — have direct fix PRs in flight, suggesting these will be resolved shortly.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

Eight pull requests were merged or closed in the past day, spanning several areas:

**WebUI & TUI:**
- **[#5438 — fix(webui): return promptly after Ctrl-C](https://github.com/HKUDS/nanobot/pull/5438)** — Merged. Fixes a hang on exit by releasing WebUI client leases with `wait_for_stop=False` on both foreground exit paths and lets the gateway client monitor handle shutdown.
- **[#5443 — fix(tui): expose /exit in command menu](https://github.com/HKUDS/nanobot/pull/5443)** — Merged. Registers `/exit` as a TUI-local command action and includes it in slash-command discovery and completion.

**Memory & Compaction:**
- **[#5440 — perf(memory): reuse conversation prefix for local compaction](https://github.com/HKUDS/nanobot/pull/5440)** — Merged. Improves consolidation by building requests from the ordinary model-facing system/history prefix instead of a separate path, preserving structured tool calls while disabling tool execution during consolidation.

**Skills:**
- **[#5341 — fix(skills): make weather workflow Windows-safe](https://github.com/HKUDS/nanobot/pull/5341)** — Merged. Replaces bare `curl` in weather skill examples with a Windows-compatible invocation, avoiding PowerShell alias conflicts.

**Core Features (older items closed):**
- **[#4527 — Add ask_clarification tool](https://github.com/HKUDS/nanobot/pull/4527)** — Closed. Adds a built-in `ask_clarification` tool with focused question/type/context/options parameters; short-circuits agent turns and preserves the clarification through trimming.
- **[#4282 — feat: add file management features to the settings view](https://github.com/HKUDS/nanobot/pull/4282)** — Closed. Adds a folder-browsing feature to the settings UI, letting users inspect and modify Agent/SOUL config files without SSH'ing into the host.

## 4. Community Hot Topics

**Most Discussed Issue:**
- **[#2493 — LANGSMITH is not working (anymore) after latest update](https://github.com/HKUDS/nanobot/issues/2493)** — 7 comments, 1 reaction. The removal of `litellm_provider.py` broke langchain.com integration. Notably, this issue was **created five months ago** (March 2026) but is still open, indicating a persistent integration gap that users care about.

**Prolific Contributor Activity:**
The `yu-xin-c` account has three open PRs in flight this week around agent lifecycle management:
- [#5430 — fix(agent): release completed task groups](https://github.com/HKUDS/nanobot/pull/5430)
- [#5431 — fix(agent): report background task failures](https://github.com/HKUDS/nanobot/pull/5431)
- [#5405 — feat(skills): support manual-only invocation](https://github.com/HKUDS/nanobot/pull/5405)

These focus on fixing subtle background-task lifecycle bugs and add a `disable-model-invocation` skill flag for side-effect-heavy skills (deploy, publish). The underlying theme is reliability of long-running agent loops — a critical trust factor for autonomous agent usage.

## 5. Bugs & Stability

Ranked by severity, with fix PRs noted where they exist:

**High:**
- **[#5271 — fix(session): prevent stale background task saves from overwriting session data](https://github.com/HKUDS/nanobot/pull/5271)** — Open, `priority: p0`, with merge conflicts. Fixes stale background work clobbering session data after `/new` lifecycle replacement. This is a data-integrity bug and the longest-pending p0.
- **[#5403 — fix(memory): use API-reported prompt tokens to trigger consolidation](https://github.com/HKUDS/nanobot/pull/5403)** — Open, `priority: p1`, with conflicts. Fixes [issue #5402](https://github.com/HKUDS/nanobot/issues/5402): tiktoken undercounts prompt tokens by 30–50%, so context consolidation never triggers and conversations exceed the window undetected.

**Medium:**
- **[#5441 — Dream: a single recovered tool error permanently blocks the memory cursor](https://github.com/HKUDS/nanobot/issues/5441)** — Open. A recovered `edit_file` error causes the run to be marked "not complete", leaving `memory/.dream_cursor` unchanged, so the same batch is reprocessed forever, duplicating edits. Fix PR: **[#5442](https://github.com/HKUDS/nanobot/pull/5442)** (open).
- **[#5425 — Support legacy socks:// proxy URLs for custom OpenAI-compatible providers](https://github.com/HKUDS/nanobot/issues/5425)** — Open. Requests fail before reaching the provider when a `socks://` alias is configured. Fix PR: **[#5439](https://github.com/HKUDS/nanobot/pull/5439)** intentionally supports only standard `socks5://`; the legacy alias will **not** be normalized — users must update configs.
- **[#5444 — Failed to login OpenAI via OAuth in Docker](https://github.com/HKUDS/nanobot/issues/5444)** — Open. OAuth token storage fails inside Docker with permission errors. Two fix PRs are available: **[#5446](https://github.com/HKUDS/nanobot/pull/5446)** (routes storage through nanobot's data dir) and **[#5445](https://github.com/HKUDS/nanobot/pull/5445)** (persist OAuth client data in Docker volume).

**Low:**
- **[#2493 — LANGSMITH regression](https://github.com/HKUDS/nanobot/issues/2493)** — Long-standing regression from `litellm_provider.py` removal; no fix PR in flight.

## 6. Feature Requests & Roadmap Signals

**Likely candidates for next release:**

- **Manual-only skill invocation** ([#5405](https://github.com/HKUDS/nanobot/pull/5405)) — `disable-model-invocation: true` frontmatter flag. Expected to merge given active iteration and clear use case for deployment/publishing skills.
- **Follow-up suggestions in WebUI** ([#5408](https://github.com/HKUDS/nanobot/pull/5408)) — Ephemeral, chat-scoped suggestions after successful turns, mirroring DeerFlow interaction patterns. A UI-polish feature with broad appeal.
- **Turn observability and safe recovery in WebUI** ([#5420](https://github.com/HKUDS/nanobot/pull/5420)) — Projects each turn into one answer surface, retains ordered reasoning/tool/file edits, and shows interrupted work as exceptions. This improves transparency for multi-step agent runs.

**Early-stage / speculative:**

- **Paid MCP security-scan integration** ([#5447](https://github.com/HKUDS/nanobot/issues/5447)) — A user proposes integrating with ScanPay, a Solana x402 micropayment scanner, as a paid MCP service. This is an external commercial proposal rather than a core-feature request; unlikely to be built in, but signals interest in monetized MCP tools in the ecosystem.

- **Nano timer core tool** ([#4853](https://github.com/HKUDS/nanobot/pull/4853)) — A dependency-free tool returning UTC/local time, IANA timezone conversion with DST handling, and calendar fields. Open since July with conflicts; small and useful, but stalled on conflict resolution.

## 7. User Feedback Summary

**Pain points:**
- **Docker OAuth reliability** is the most common friction point this week (issues #5444, plus fix PRs #5445/#5446). Users expect credentials to persist across container replacements and the non-root user to have write access.
- **Memory/compaction correctness** continues to surface (issues #5441, #5402). The Dream loop and token-triggered consolidation have been repeatedly patched, suggesting the memory system is the project's most complex and fragile subsystem.
- **Proxy compatibility** — users rely on legacy `socks://` URLs, and the maintainers' decision to only support standard `socks5://` will require user-side configuration changes. This may cause a brief spike in support questions.

**Satisfaction signals:**
- The weather skill Windows fix (#5341) and TUI `/exit` discoverability (#5443) show the team is responsive to small polish items that affect day-to-day UX.
- The `ask_clarification` tool finally closed after nearly two months (#4527), adding a long-requested interaction primitive.

## 8. Backlog Watch

**Needs maintainer attention:**

- **[#2493 — LANGSMITH integration broken](https://github.com/HKUDS/nanobot/issues/2493)** — Open since March 2026 (5 months). No fix PR exists. If this integration is still supported, it needs an explicit decision (fix vs. deprecate).

- **[#5271 — fix(session): prevent stale background task saves](https://github.com/HKUDS/nanobot/pull/5271)** — `priority: p0`, open since August 6 with merge conflicts. A data-integrity fix blocking on trivial conflict resolution; should be prioritized.

- **[#5403 — fix(memory): use API-reported prompt tokens](https://github.com/HKUDS/nanobot/pull/5403)** — `priority: p1`, open since August 16 with conflicts. Context-window overflow can lead to silent degradation; this should be merged promptly.

- **[#4853 — nano_timer core tool](https://github.com/HKUDS/nanobot/pull/4853)** — Open since July 8 with conflicts. Small, self-contained feature; either merge or request the author to rebase.

- **[#5257 — fix(agent): bound sustained-goal continuation when idle](https://github.com/HKUDS/nanobot/pull/5257)** — Open since August 5, `priority: p2`. Fixes an admission bug where "follow up daily, forever" goals with no terminal condition are recorded as sustained goals, keeping them `active` indefinitely. Important correctness fix for goal-based automation.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Digest Date:** 2026-08-20
**Data Window:** 2026-08-19 to 2026-08-20 (24h)

---

## 1. Today's Overview

Hermes Agent is in a period of **intense bug-fixing and stabilization**, with 41 open issues and 42 open PRs actively being worked on. The project shows **high maintainer engagement** — a significant number of salvaged PRs (e.g., #90389, #90387, #90381) are being cherry-picked onto current main, and there's a clear pattern of `hermes-seaeye[bot]`-driven auto-fixes (#90384). However, **no new releases** were published in this window, suggesting the team is consolidating fixes ahead of a major version. The most critical concern is a **severe Windows stability bug** (#89614) causing blue screens of death, which is drawing immediate attention alongside a batch of P1/P2 regressions in the update pipeline.

---

## 2. Releases

**No new releases published in this data window.**

The absence of releases, combined with the high volume of merged/salvaged PRs, suggests the project is in a stabilization phase. Users are reporting issues with the current version (v0.20.0) that have likely already been fixed on `main` but not yet shipped, contributing to user frustration (see #83529).

---

## 3. Project Progress

While 8 PRs were merged/closed, the most meaningful progress is in **salvaged PRs** cherry-picked onto main. Key advances:

- **CLI Fixes (Salvaged):** PR #[90389](https://github.com/NousResearch/hermes-agent/pull/90389) fixes `hermes -z` silently dropping `-s/--skills`; PR #[90381](https://github.com/NousResearch/hermes-agent/pull/90381) fixes `/whoami` reporting "Unknown command"; PR #[90387](https://github.com/NousResearch/hermes-agent/pull/90387) eliminates 69 bogus self-collision warnings per startup from skill scans.
- **Desktop Ghost Rows:** PR #[90370](https://github.com/NousResearch/hermes-agent/pull/90370) fixes a frustrating UI bug where deleted archived sessions left ghost rows that spin forever.
- **Windows Encoding:** PR #[90046](https://github.com/NousResearch/hermes-agent/pull/90046) fixes process-scan output decoding, using the machine code page instead of hardcoded UTF-8 — directly mitigating the `svchost.exe` blue-screen incident (#89614).
- **Context Meter Fix:** PR #[90378](https://github.com/NousResearch/hermes-agent/pull/90378) resolves a missing/wrong context meter in the Desktop statusbar.
- **Closed Meta-Issues:** The "Copilot route: reasoning_effort 'ultra' clamps to 'medium'" (#74295) and "reasoning_effort 'ultra' rejected by GLM API" (#70058) both closed, indicating the reasoning-effort handling has been fixed.

---

## 4. Community Hot Topics

The most active discussion this window is a **systemic infrastructure problem**, not just a single bug:

- **[#66616 — Skills Index is Stale/Degraded (60 comments, 30 days old)](https://github.com/NousResearch/hermes-agent/issues/66616):** This automated watchdog issue remains the most-commented item. The skills index is repeatedly exceeding its freshness limit (29.8h vs 26h limit), degrading the `/docs/skills` hub. The community's implicit need is for **reliable documentation infrastructure**. With a P3 priority, this is chronically under-served.

- **[#84834 — Webhook Feature Package Meta-Issue (19 comments)](https://github.com/NousResearch/hermes-agent/issues/84834):** A "graph-gated repair" tracker for the entire webhook surface (ingress, execution, delivery, UI, docs). This shows active community-driven architecture around webhooks, with a plan to fix 5×2×3 failure modes. The related PR #[90385](https://github.com/NousResearch/hermes-agent/pull/90385) (handoff to Discord) suggests the fix package is being implemented.

- **[#79564 — Discord Feature Parity Campaign (8 comments)](https://github.com/NousResearch/hermes-agent/issues/79564):** A meta-issue to bring the Discord surface to full parity with discord.py 2.7.1 / API v10. PR #[90383](https://github.com/NousResearch/hermes-agent/pull/90383) on smart multiplex lobby routing is a direct outcome.

**Analysis:** The community is driving toward **broader gateway/platform maturity** (Discord parity, webhook robustness) while the maintainers are focused on **core stability** (CLI, update path, Windows). The gap between community ambition and maintainer capacity may explain the high backlog of long-lived PRs like #3335 (Zulip) and #27040 (voice server).

---

## 5. Bugs & Stability

### Critical (P0/P1)

- **[#89614 — Hermes kills `svchost.exe` → repeated 0xEF blue screens (P1, Windows)](https://github.com/NousResearch/hermes-agent/issues/89614):** **CRITICAL.** A stale-PID `taskkill /F /PID` is killing the Windows critical process, causing repeated BSODs. This is the most severe bug. Fix PR exists: #[90046](https://github.com/NousResearch/hermes-agent/pull/90046) addresses the encoding, but the root cause of wrong PID targeting needs verification. **Severity: Catastrophic (data loss / system unusable).**

- **[#83529 — `hermes update` destroys hermes (P1, Debian)](https://github.com/NousResearch/hermes-agent/issues/83529):** A botched update path leaves the install in a non-functional state. Given the P1 tag, this is a release-blocker. No dedicated fix PR found in window, but related recovery-loop issue #[79539](https://github.com/NousResearch/hermes-agent/issues/79539) suggests the update logic has deeper problems.

### High (P2)

- **[#89897 — [CLOSED] Codex tool follow-ups send unsupported `prompt_cache_retention` to gpt-5.6-sol (P0, fixed)](https://github.com/NousResearch/hermes-agent/issues/89897):** Closed, indicating a fix was shipped or reverted.
- **[#90159 — `hermes update` installs mcp 2.0.0 over pinned 1.28.1, silently breaking HTTP/SSE MCP servers (P2)](https://github.com/NousResearch/hermes-agent/issues/90159):** Dependency pinning violation. It's a "silent" breaker — all HTTP MCP servers stop connecting while gateway reports healthy. **Update reliability is a major theme today.**
- **[#90299 — False-positive "TERMINAL_CWD in .env" warning on every startup (P2)](https://github.com/NousResearch/hermes-agent/issues/90299):** The deprecation warning logic is misreading the environment. Marked as duplicate, suggesting a fix exists elsewhere.
- **[#90229 — Desktop file tree stuck on skeleton forever after boot (P2, Windows, needs-repro)](https://github.com/NousResearch/hermes-agent/issues/90229):** Intermittent rendering failure of the right-sidebar file tree.

### Medium (P3)

- **[#90360 — `sessions archive` filters return empty for recent desktop sessions (P2)](https://github.com/NousResearch/hermes-agent/issues/90360)**
- **[#90365 — Model settings "Expensive Model Warning" has no confirm button (P2)](https://github.com/NousResearch/hermes-agent/issues/90365)**
- **[#84064 — `config set` breaks on provider keys containing literal dots (P2)](https://github.com/NousResearch/hermes-agent/issues/84064)**
- **[#89823 — [CLOSED] Bot Mode 'Create on' picker never appears (fixed)](https://github.com/NousResearch/hermes-agent/issues/89823)**

---

## 6. Feature Requests & Roadmap Signals

Several feature PRs advanced significantly, indicating near-term roadmap focus:

- **Pluggable Computer Use Backends:** PR #[90380](https://github.com/NousResearch/hermes-agent/pull/90380) (supersedes #61311) creates one seam for container/sandbox/remote-desktop runtimes. This unblocks PR #[61507](https://github.com/NousResearch/hermes-agent/pull/61507) — **Desktop-managed Computer Use bridge** — which is a major capability for remote agent control. **Predict in v0.21.**
- **Claude Agent SDK Provider:** PR #[65982](https://github.com/NousResearch/hermes-agent/pull/65982) brings the official Claude Agent SDK under subscription OAuth. Long-running (since July), still open with no recent comments. Likely complex; **predict in v0.22+**.
- **Zulip Integration:** PR #[3335](https://github.com/NousResearch/hermes-agent/pull/3335) (6 months old) is being updated to the new platform plugin system. Shows community demand for more chat platforms.
- **Generic Voice Server Gateway:** PR #[27040](https://github.com/NousResearch/hermes-agent/pull/27040) (3 months old, P3) would connect Hermes to telephony/WebRTC via Pipecat/Livekit.
- **Keyless Web Search:** PR #[90313](https://github.com/NousResearch/hermes-agent/pull/90313) makes `web_search` work out-of-the-box using Parallel/Exa free tier endpoints. Low risk, high value for onboarding. **Predict in v0.21.**
- **Unhide Sessions:** PR #[90388](https://github.com/NousResearch/hermes-agent/pull/90388) adds `sessions unhide` and `--include-hidden` — a recovery affordance for the durable `hidden` flag. **Predict in v0.21.**

**User-requested features (issues) showing traction:** #[89995](https://github.com/NousResearch/hermes-agent/issues/89995) (Expose Bot Mode group chats in web dashboard), #[90007](https://github.com/NousResearch/hermes-agent/issues/90007) (Low-memory Windows execution profile), #[63852](https://github.com/NousResearch/hermes-agent/issues/63852) (Native fallback-chain readiness check) — all waiting for design decisions (`needs-decision` label).

---

## 7. User Feedback Summary

**Pain Points (High Frequency):**

- **Update/Patch Management:** Three issues today directly involve broken updates (#83529, #90159, #79539). The `hermes update` command is the single biggest source of user frustration — it can destroy the install, break MCP dependencies, and create unrecoverable loops. The message: **shipping a stable update path is table stakes.**
- **Windows Platform Reliability:** Beyond the BSOD (#89614), Windows users suffer from file-tree skeletons (#90229), build failures (#90134), and process-scan issues (#90046). This platform needs dedicated QA.
- **Desktop-Gateway Integration Friction:** Users report the Desktop failing to connect to `hermes serve` (#85605), remote-primary setups starting unwanted loopback agents (#90316), and auth issues (#90333, #84483). The Desktop app's remote-connection story is still rough.

**Satisfaction Signals:**

- The rapid closure of `reasoning_effort` issues (#74295, #70058) shows that when bugs are picked up, they're fixed well.
- The salvage-PR workflow (cherry-picking old fixes) is efficient, but it also signals that **original PR authors may feel ignored** — several salvaged fixes cite "earliest complete fix" from months ago.

**Use Cases Emergining:**

- **Bot Mode / Group Chat** is a growing area (issues #89995, #89497, #89823, PR #89901) — users want multi-agent rooms to work reliably.
- **Webhook-to-Discord handoffs** (#90385) suggest enterprise automation workflows using Hermes as a connector.

---

## 8. Backlog Watch

These items need maintainer attention:

- **[#66616 — Stale Skills Index (60 comments, 30 days open)](https://github.com/NousResearch/hermes-agent/issues/66616):** The watchdog deadline is being missed repeatedly. Community is likely to start flagging this as unmaintained — documentation infrastructure is a trust signal.
- **[#3335 — Zulip Integration (6 months open)](https://github.com/NousResearch/hermes-agent/pull/3335):** A massive feature PR that is being updated but never merged. Maintainers should either assign a reviewer or close it to set expectations.
- **[#27040 — Voice Server Gateway (3 months open)](https://github.com/NousResearch/hermes-agent/pull/27040):** Similarly large-scope; lacks reviewers.
- **[#65982 — Claude Agent SDK Provider (35 days open)](https://github.com/NousResearch/hermes-agent/pull/65982):** Complex, high-value; needs a clear roadmap decision.
- **[#61507 — Desktop Computer Use Bridge (42 days open)](https://github.com/NousResearch/hermes-agent/pull/61507):** Blocked by #90380. Now unblocked — needs a merge decision soon.
- **[#85744 — Show persisted usage without live agent (6 days open, duplicate of #42772)](https://github.com/NousResearch/hermes-agent/pull/85744):** The original proposal (#42772) is from an older era; this reimplementation incorporates feedback. Needs review to close the loop.
- **[#79539 — Windows missing base interpreter recovery loop (15 days, P2)](https://github.com/NousResearch/hermes-agent/issues/79539):** Follow-up to a "closed as implemented" issue that clearly wasn't. This signals the issue tracker has a **systemic closure-without-verification problem**.

---

**Overall Health Assessment:** Hermes Agent is **stable in development but fragile in delivery**. The engineering team is responsive to critical bugs (P0/P1 addressed within days), but the update pipeline and Windows platform are consistently weak points. The community's enthusiasm for platform expansion (Discord, Zulip, webhooks, voice) currently outpaces the maintainers' capacity to review and merge. The high volume of salvaged PRs suggests a **knowledge-transfer bottleneck** — original contributors wait months while their fixes are cherry-picked by others.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for 2026-08-20.

---

# PicoClaw Project Digest — 2026-08-20

## 1. Today's Overview
PicoClaw is in a relatively low-activity phase today, with only one issue closed and no new releases. The main highlight is the closure of a long-standing bug related to banner output corrupting shell completion scripts, which represents a solid quality-of-life win. The pull request queue shows four stale PRs lingering (two open, two closed), indicating a potential bottleneck in the review process. Notably, a new and substantial feature PR for Telegram UX was merged, signaling that the maintainers are prioritizing channel-specific improvements. However, the lack of releases and the presence of open PRs with no maintainer response suggests a need for more active triage.

## 2. Releases
No new releases were published in the last 24 hours.

## 3. Project Progress
Two PRs were closed/merged today, though only one represents an actual merge of new code.

- **[PR #3341: feat(telegram): add interactive command UX and formatted ephemeral fallback](https://github.com/sipeed/picoclaw/pull/3341)** (Merged): This is a significant enhancement for the Telegram integration. It replaces the CLI-style full subcommand grammar with an interactive command UX, reduces the verbosity of the `/help` output, and adds a formatted ephemeral fallback for structured content. This will considerably improve the user experience for Telegram-based interactions.
- **[PR #3200: feat(models): add configurable default fallback chain](https://github.com/sipeed/picoclaw/pull/3200)** (Closed/Stale): This feature request, proposing a configurable model fallback chain for the web UI, was closed as stale. It was open since July and may have been superseded or deprioritized.

## 4. Community Hot Topics
The most active discussion today is from the closure of a long-running bug.

- **[Issue #1305: [BUG] new banner print to STDOUT, break completion flow](https://github.com/sipeed/picoclaw/issues/1305)** (4 comments): This bug, tracked since March, was closed today. Users were frustrated that a banner printout corrupted the output of `picoclaw completion zsh`, breaking their shell completion setup. The high comment count and long duration indicate this was a real pain point for the community. The user's underlying need is for the CLI to adhere to standard POSIX output conventions, ensuring programmatic workflows are not polluted by informational messages.

## 5. Bugs & Stability
- **[Critical / Fixed] CLI Output Corruption (Issue #1305, fixed via PR #1008)**: This was a high-severity bug where a banner printed to STDOUT broke shell completion flows. The issue was reported as far back as March and was finally closed with a fix that likely moves the banner to STDERR. This highlights a regression that persisted for months and is now resolved.

## 6. Feature Requests & Roadmap Signals
The merged Telegram UX PR is a strong signal that the project is actively investing in improving bot interactions. While the "default fallback chain" feature (PR #3200) was closed as stale, it represents a user desire for more resilient model configurations. The open PRs also point to the direction of future development:

- **[PR #3315: Support topics in private bot chats](https://github.com/sipeed/picoclaw/pull/3315)**: This patches a Telegram-specific gap where topic support only worked for `IsForum` chats and not private ones, likely making its way into a future release.
- **[PR #3316: Routed-agent context management not respecting history](https://github.com/sipeed/picoclaw/pull/3316)**: This addresses a significant bug in routed-agent memory handling, another critical area for agent-based workflows.

## 7. User Feedback Summary
The community feedback is a mix of relief and lingering needs:
- **Positive:** The Telegram UX improvements are generally welcome, aiming for a more intuitive interface.
- **Frustration (Resolved):** The long-standing issue with the bash/zsh completion being broken by the banner (Issue #1305) caused significant frustration, and its closure today will be well-received by power users who rely on the CLI.
- **Lingering Concern:** The bug regarding routed-agent context management (PR #3316) indicates users are actively using advanced agent routing and expect robust long-term memory, a core feature for "personal AI assistant" use cases.

## 8. Backlog Watch
Two PRs remain open with no maintainer comments, both being flagged as stale. Their long duration without engagement suggests they need immediate attention.

- **[PR #3316: fix: routed-agent context management not respecting history](https://github.com/sipeed/picoclaw/pull/3316)**: Opened on August 3rd, this is a critical bug fix for a core feature (agent memory). The lack of response for over two weeks is concerning, as it directly impacts user trust in the agent's capabilities.
- **[PR #3315: Support topics in private bot chats](https://github.com/sipeed/picoclaw/pull/3315)**: Also opened on August 3rd, this is a smaller, targeted feature fix for Telegram. The lack of a review for such a simple enhancement may indicate maintainer bandwidth issues and risks losing the contribution.

These stale PRs are the most pressing items for maintainers to review, merge, or close.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**2026-08-20**

---

## 1. Today's Overview

NanoClaw is in a period of heavy development and maintenance activity. The project saw 34 pull requests updated in the last 24 hours, with 25 merged or closed—indicating a highly productive day. Three new issues were filed, all related to setup robustness on clean machines and a carrier-level SMS delivery bug. The core-team is actively addressing Node.js runtime compatibility (PR #3360) and Slack agent flow improvements (PRs #3361, #3362), while the community continues to push the Dial channel integration (#3041, #3050) forward. Overall, the project is healthy, responsive, and shipping at a steady clip.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent release remains the one preceding this digest window.

---

## 3. Project Progress

25 PRs were merged or closed today. Notable items that advanced the codebase:

| PR | Title | Focus |
|----|-------|-------|
| [#3357](https://github.com/nanocoai/nanoclaw/pull/3357) | `setup: --slack-agents installs the whole Slack agents feature` | **Merged** — Introduces the `--slack-agents` setup flag to install the full Slack agents feature (child bots, shared rooms, canvases, DM onboarding). Base install now yields just the core Slack bot experience. |
| [#3358](https://github.com/nanocoai/nanoclaw/pull/3358) | `slack: split the payload — base adapter in /add-slack, agents feature in /slack-agent-flow` | **Merged** — Companion to #3357; splits Slack channel payloads along the flag boundary and adapts the agents payload to the async central DB. |
| [#3342](https://github.com/nanocoai/nanoclaw/pull/3342) | `feat(slack): decline owner-absent channel invites instead of carding them` | **Merged** — Owner-absent Slack channel invites are now declined in place rather than escalated to the owner as an approval card. Closes a potential security gap where the bot appeared present before its owner approved. |
| [#3340](https://github.com/nanocoai/nanoclaw/pull/3340) | `fix(approvals): record the delivering instance on pending_approvals` | **Merged** — Adds an `instance` column to `pending_approvals` so OneCLI credential cards are posted/edited by the same bot identity that owns the DM. |
| [#3339](https://github.com/nanocoai/nanoclaw/pull/3339) | `fix(setup): fail closed when a stored sign-in cannot be verified` | **Merged** — A stored NanoClaw account credential that cannot be checked (e.g., `unreachable`) is now treated as a failure, not a pass. |
| [#3341](https://github.com/nanocoai/nanoclaw/pull/3341) | `fix(provisioning): derive the Slack service from the credential's issuer` | **Merged** — Pairs the install token issuer (account service) with the spender (Slack service), preventing mismatched deployments. |
| [#3344](https://github.com/nanocoai/nanoclaw/pull/3344) | `feat(provisioning): optional request-origin metadata on app creation` | **Merged** — Adds four optional metadata fields describing the origin of app-creation requests. |
| [#3345](https://github.com/nanocoai/nanoclaw/pull/3345) | `feat(setup): forward optional client metadata on Slack service requests` | **Merged** — Sends `client_version` and other metadata with Slack service requests during setup. |
| [#3351](https://github.com/nanocoai/nanoclaw/pull/3351) | `feat(telegram): add approved group connection picker` | **Merged** — Adds `/connect_group` DM command backed by Telegram's native group picker, routed through the existing approval flow. |
| [#3352](https://github.com/nanocoai/nanoclaw/pull/3352) | `docs(telegram): document approved group connection flow` | **Merged** — Documentation for the new Telegram group connection flow. |
| [#3025](https://github.com/nanocoai/nanoclaw/pull/3025) | `fix(container): raise the agent SDK's 32000 output-token cap to the max` | **Merged** — Removes the output-token ceiling for agents, allowing larger responses. |

---

## 4. Community Hot Topics

The most active discussion items today (ranked by comment/reaction count):

1. **Dial Channel Integration (PRs [#3041](https://github.com/nanocoai/nanoclaw/pull/3041), [#3050](https://github.com/nanocoai/nanoclaw/pull/3050))** — Open, created 2026-07-14, still active. These two PRs add a complete Dial channel adapter (SMS + AI voice calls) and fold it into the setup wizard. The sustained activity (>5 weeks) and length of the discussion reflect the complexity of the adapter and the community's strong interest in SMS/voice as a channel.

2. **Node.js Runtime Compatibility ([#3359](https://github.com/nanocoai/nanoclaw/issues/3359), [#3360](https://github.com/nanocoai/nanoclaw/pull/3360))** — A community user (glifocat) hit a hard failure on Node 26 with `better-sqlite3` 11.10.0. The core team responded within hours with PR #3360, upgrading to `better-sqlite3` 13.0.3 and raising the host minimum to Node 22. This was the most actionable and time-sensitive topic of the day.

3. **Slack Agent Flow Prerequisites (PRs [#3361](https://github.com/nanocoai/nanoclaw/pull/3361), [#3362](https://github.com/nanocoai/nanoclaw/pull/3362))** — Two new open PRs tightening the Slack agents feature: exposing decline-notification overrides (`dedupeKey`, `declineText`, `fyiText`) and validating prerequisites before copying/registering payloads.

**Underlying need analysis:** The Dial channel effort signals a community push toward asynchronous voice/SMS communication. The Slack work shows the maintainers are hardening a feature that replaces human approval with automated decline. The Node 26 issue underscores a broader pain: the project's dependency chain lags current Node LTS and toolchain releases.

---

## 5. Bugs & Stability

**Three new issues filed today, ranked by severity:**

1. **High — [Dial SMS delivery falsely marked as "delivered" when carrier rejects after send](https://github.com/nanocoai/nanoclaw/issues/3353)** — Created by glifocat. Once Dial accepts an SMS, the session records `status = 'delivered'`. If the carrier rejects it afterwards, nothing re-examines that decision. The retry budget is never touched, and neither agent nor owner is notified. This is a correctness/data-integrity bug that could erode user trust. **No fix PR yet.**

2. **High — [Node 26 passes `check_node` but `better-sqlite3` 11.10.0 fails to build](https://github.com/nanocoai/nanoclaw/issues/3359)** — Created by glifocat. On macOS arm64 with Node 26.7.0, setup passes the version check (which only has a lower bound) but aborts at bootstrap with `deps_failed`. **Fix PR #3360 exists** (upgrade to better-sqlite3 13.0.3, raise minimum to Node 22) — pending review/merge.

3. **Medium — [Setup leaves 0-byte channel files on failed `git show` copy; OneCLI check runs before its PATH fix (non-login/headless install)](https://github.com/nanocoai/nanoclaw/issues/3354)** — Created by glifocat. Two setup bugs surface over non-login SSH sessions: (a) `git show <ref>:<path> > <file>` produces a 0-byte file on failure instead of aborting; (b) a PATH check runs before the script exports `~/.local/bin` to PATH. Both share a root cause: setup assumes an interactive/login shell. **No fix PR yet; PR #3249 (open) partially addresses Node-range handling but not these specific shell issues.**

**Additionally:** PR [#3025](https://github.com/nanocoai/nanoclaw/pull/3025) (merged today) raised the agent SDK's output-token cap from 32,000 to the model max — resolving what was effectively a silent truncation bug.

---

## 6. Feature Requests & Roadmap Signals

Strong signals for the next version(s):

1. **Cursor Agent SDK Provider (PRs [#3355](https://github.com/nanocoai/nanoclaw/pull/3355), [#3356](https://github.com/nanocoai/nanoclaw/pull/3356))** — Both open, both created 2026-08-19. These add Cursor as a first-class agent provider, with `/add-cursor` setup skill and the SDK payload. Expect this to land soon given the core-team tags.

2. **Agent Mailbox Seam and Registry ([#3349](https://github.com/nanocoai/nanoclaw/pull/3349))** — Open, created today. Adds a pluggable mailbox registry (SQLite remains default) shared by both NanoClaw and the agents it runs. This is an architectural enabler for future multi-agent coordination.

3. **Dial Channel (SMS + AI voice calls) (PRs [#3041](https://github.com/nanocoai/nanoclaw/pull/3041), [#3050](https://github.com/nanocoai/nanoclaw/pull/3050))** — Still open after 5+ weeks. The fact that the core team has not closed or merged these suggests they are being actively reviewed. The carrier-rejection bug (#3353) was likely found during that review and will need to be addressed before merge.

4. **Slack Agents Feature Complete (PRs [#3361](https://github.com/nanocoai/nanoclaw/pull/3361), [#3362](https://github.com/nanocoai/nanoclaw/pull/3362))** — Both open, created today. These finish the `--slack-agents` installation path with proper override seams and prerequisite validation.

5. **Telegram Approved Group Connections** — Merged today ([#3351](https://github.com/nanocoai/nanoclaw/pull/3351)). A completed feature that adds a native group picker and security boundary.

**Prediction:** The next minor release will likely include the Cursor provider, agent mailbox registry, Node 22+ minimum, and the full Slack agents feature set. The Dial channel may slip to a subsequent release if the delivery-status bug needs more design work.

---

## 7. User Feedback Summary

The community (primarily represented by **glifocat**) surfaced three distinct pain points today:

1. **Setup fragility on non-interactive/headless environments** ([#3354](https://github.com/nanocoai/nanoclaw/issues/3354)) — Clean SSH installs break silently: 0-byte files and PATH order assumptions. Users expect `nanoclaw.sh` to be robust regardless of shell interactivity.

2. **Node version support lag** ([#3359](https://github.com/nanocoai/nanoclaw/issues/3359)) — The project's minimum-version check gave false confidence: it passed on Node 26 but the dependency tree couldn't build. The user would have preferred an early, explicit failure or a warning, not a mid-bootstrap crash.

3. **Delivery-status accuracy for SMS** ([#3353](https://github.com/nanocoai/nanoclaw/issues/3353)) — The user expects a message rejected by the carrier to not appear as "delivered," and wants the retry budget and notification pipeline to respect that fate.

**Satisfaction signals:** The speed of response to the Node 26 issue (PR opened same day) and the volume of merged core-team PRs suggest a responsive, well-maintained project. The community is actively testing edge cases and filing quality issues — a hallmark of engaged users.

---

## 8. Backlog Watch

Items that need maintainer attention:

1. **[PR #3249](https://github.com/nanocoai/nanoclaw/pull/3249) — `fix(setup): handle an existing Node outside the supported range`** — Open since 2026-08-14, updated 2026-08-19 but with no merge. Given the Node 26 issue (#3359) demonstrates the exact gap this PR addresses, priority should be raised.

2. **[PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) / [#3041](https://github.com/nanocoai/nanoclaw/pull/3041) — Dial channel integration** — Open for over 5 weeks. The associated bug (#3353) affects trust in the adapter's correctness. Maintainers should either approve, request specific changes, or provide a timeline to the community.

3. **[Issue #3353](https://github.com/nanocoai/nanoclaw/issues/3353)** — No fix PR yet. The delivery-status bug will only grow in impact as the Dial channel (if merged) gains users.

4. **[Issue #3354](https://github.com/nanocoai/nanoclaw/issues/3354)** — No fix PR yet. The 0-byte-file and PATH-order bugs are particularly nasty because they fail silently; a first-time headless install might appear to succeed while producing corrupt configurations.

---

*Data source: github.com/nanocoai/nanoclaw — issues and PRs updated in the 24 hours ending 2026-08-20.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-08-20**.

---

# NullClaw Project Digest — 2026-08-20

## 1. Today's Overview
NullClaw is currently in a **low-activity maintenance phase** over the last 24 hours. There were **zero new issues** reported and **zero releases** published, indicating a period of stability with no major user-facing bugs surfacing. The only activity was a single **open Pull Request (#989)** aimed at fixing a broken README chart, which remains unmerged. While no features advanced or merged today, the presence of a pending fix suggests maintainers are addressing minor documentation/infrastructure quality issues. Overall, the project appears stable but with limited momentum; the primary health signal is the need to merge pending housekeeping PRs.

## 2. Releases
No new releases were published in the last 24 hours. This section is omitted due to lack of data.

## 3. Project Progress
No Pull Requests were merged or closed today. The sole open PR remains pending review:

- **[PR #989: fix: restore broken star history chart](https://github.com/nullclaw/nullclaw/pull/989)**
  - **Status:** Open
  - **Author:** FaintFlower
  - **Summary:** Fixes the broken star history chart in the README, which currently fails due to restrictions on the GitHub stargazer API. The PR migrates the chart to rely on `star-history.dera.page`, a token-free service, to ensure the chart renders correctly.

No feature work advanced to completion in this window.

## 4. Community Hot Topics
There is minimal community engagement today; the single active PR has **zero comments and zero reactions**. The underlying need driving PR #989 is **project presentation and accessibility**—users and maintainers want the README's visual data (star history) to be functional without requiring complex authentication or API tokens. While this is not a high-traffic discussion, it highlights a broader user concern about the reliability of GitHub's public API for third-party tools. Maintainers should prioritize reviewing this PR to prevent stagnation, as broken visuals can deter new contributors evaluating the project.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. The project appears stable in its current state. The only known issue—the broken star history chart—is a **documentation/presentation defect** of low severity, and the aforementioned **[PR #989](https://github.com/nullclaw/nullclaw/pull/989)** serves as the direct fix. No other stability concerns are on the radar.

## 6. Feature Requests & Roadmap Signals
There were no feature requests submitted today. However, the pending PR #989 signals a subtle roadmap direction: **reducing dependency on rate-limited or restricted GitHub APIs** in favor of lightweight, token-free external services. Looking ahead, we predict the next minor release might include this infrastructure fix, potentially alongside other README/documentation improvements. For the near-term roadmap, users might expect a continued focus on project polish (docs and visual aids) rather than new functional capabilities, given the current development lull.

## 7. User Feedback Summary
With zero new issues or closed PRs, there is no new direct user feedback today. The single actionable signal comes from contributor *FaintFlower*, who identified a **real pain point**: the README's primary visual metric (star growth) was inaccessible due to API limitations, which likely frustrated users and potential contributors who wanted to gauge project popularity. The suggested shift to `star-history.dera.page` also reflects a user preference for **simple, reliable, and authentication-free tools**. Overall sentiment appears neutral-to-positive, with no complaints filed; the community is passive awaiting maintainer action on the pending fix.

## 8. Backlog Watch
The following item requires immediate maintainer attention to prevent it from aging into a stale PR:

- **[PR #989 (Open): fix: restore broken star history chart](https://github.com/nullclaw/nullclaw/pull/989)**
  - Created **2026-08-19**; remains unreviewed for 24+ hours.
  - **Risk:** If left unattended, the README will continue to display a broken chart, and the PR may eventually require conflict resolution if other docs change.
  - **Action:** Maintainers should review and merge promptly, as the change is low-risk (URL swap) and directly improves project presentation.

There are no long-unanswered issues in the backlog at this time.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Based on the GitHub data provided for IronClaw on 2026-08-20, here is the project digest:

---

## 🦾 IronClaw Project Digest — 2026-08-20

### 1. Today's Overview
IronClaw is in a high-velocity **feature and stabilization push** ahead of its v1.4.0 milestone. The project shipped **v1.3.0** to stable yesterday, and the team has already shifted focus to the next iteration, landing foundational work on **persistent sandboxes** and **automation preflight checks**. Activity is intense, with 38 PRs updated and 14 issues updated in the last 24 hours, marking a significant push by core contributors. The "capability-response-normalization" stack (PRs #7686, #7692, #7711) is a major architectural theme, alongside a heavy CI reliability effort to unblock the merge queue (#7756). While the project shows momentum, the volume of open PRs (22) and "XL" sized changes suggests a need for careful review bandwidth to avoid bottlenecks.

### 2. Releases
**`ironclaw-v1.3.0` - 2026-08-19**

A **stable promotion** of the release candidate `1.3.0-rc.2`. This release focuses on hardening and validation, with no new production features listed.

- **Key Fix:** The most critical fix addresses an upgrade path issue: **Upgrades from version 1.2 now correctly accept and preserve the released extension `activation_state` field**, preventing a crash-loop during startup.
- **Migration Notes:** This fix is specifically for users upgrading from v1.2, ensuring that extension states are handled gracefully during the transition.

---

### 3. Project Progress (Merged/Closed PRs)
The project saw significant progress yesterday, with 16 PRs merged or closed. Key highlights include:

- **Release & CI Stabilization:**
    - **[#7754](https://github.com/nearai/ironclaw/pull/7754)**: `chore(release)`: Promoted `1.3.0-rc.2` to stable **v1.3.0**.
    - **[#7756](https://github.com/nearai/ironclaw/pull/7756)**: `fix(ci)`: **Bounded every unbounded CI operation** (apt hangs, uncapped jobs, external downloads). This directly addresses merge queue timeouts.

- **Onboarding & UX:**
    - **[#6994](https://github.com/nearai/ironclaw/pull/6994)**: `feat(webui)`: Closed the massive **OOBE (Onboarding) automation-tasks prototype**, including the carousel, inline cards, and agent-mode pill.

- **Technical Debt & Refactoring:**
    - **[#7686](https://github.com/nearai/ironclaw/pull/7686)**: `refactor(runtime)`: **Centralized capability outcome processing** (PR 1 of the normalization plan #7627). This is behavior-preserving and lays groundwork for better error handling.

- **Sandbox & Architecture:**
    - **[#7741](https://github.com/nearai/ironclaw/pull/7741)**: `feat(sandbox)`: Closed the initial attempt at **per-thread persistent containers with Docker Exec**, reducing per-command overhead from 1-2.5s to ~40ms.

### 4. Community Hot Topics
The most active discussions are focused on deep technical architecture and UX improvements.

- **[#7732](https://github.com/nearai/ironclaw/pull/7732) — Epic: Persistent per-user sandbox (7 comments)**: This is the **most commented-on issue**. The community is actively discussing the shift from per-command containers to persistent, per-user sandboxes via `iron-proxy`. The discussion highlights the need to resolve the tension between `builtin.shell` routing and the new persistent model.
- **[#6994](https://github.com/nearai/ironclaw/pull/6994) — OOBE Automation-Tasks Prototype**: While closed, this PR was likely a major forum for discussion on onboarding UX, given its size (XL) and scope (docs + implementation). It signals a strong desire to reduce "blank slate" user friction.
- **[#7603](https://github.com/nearai/ironclaw/pull/7603) — Batch BeforeModel checkpoints (2 comments)**: This issue on performance optimization (reducing checkpoint disk writes by ~14 rows/turn) indicates a community focus on **runtime performance and reducing overhead**.

### 5. Bugs & Stability
Several bugs were reported, with a mix of critical and UX-level severity.

- **High — [#7748](https://github.com/nearai/ironclaw/pull/7748)**: `bug`: **"IronClaw got confused and stopped working."** A vague but critical report of a user-facing functional failure. No fix PR yet.
- **Medium — [#7745](https://github.com/nearai/ironclaw/pull/7745)**: `qa-bug`: **Copilot MCP extension install fails** with `auth_required`, duplicate catalog entries, and unclear token types. This blocks a common user workflow.
- **Low/UX — [#7744](https://github.com/nearai/ironclaw/pull/7744)**: `qa-bug`: **Cron job UI is missing edit and test buttons**, limiting user control over automations.
- **Infrastructure — [#7756](https://github.com/nearai/ironclaw/pull/7756)**: A **CI-related bug** (unbounded `apt-get` operations) that caused merge queue timeouts. This was fixed in PR #7756.

### 6. Feature Requests & Roadmap Signals
The roadmap for **v1.4.0** is clearly taking shape.

- **Persistent Sandboxing**: The epic **[#7732](https://github.com/nearai/ironclaw/pull/7732)** is a v1.4.0 target. It aims to replace the ephemeral per-command containers with persistent per-user sandboxes.
- **Onboarding Overhaul**: The closing of the OOBE prototype [#6994](https://github.com/nearai/ironclaw/pull/6994) signals a major UX push. The related epic **[#7044](https://github.com/nearai/ironclaw/pull/7044)** ("Onboarding to channel-first approach") was closed, suggesting the design phase is complete and implementation is gearing up.
- **Automation Preflight (PR #7743)**: This feature establishes a "bounded creation preflight" for automations, which is likely part of the effort to make automations more reliable and user-friendly. It ties directly into the automation epic [#6879](https://github.com/nearai/ironclaw/issues/6879).
- **Local MCP Support ([#7757](https://github.com/nearai/ironclaw/pull/7757))**: A new PR is actively addressing the inability to connect to local MCP servers, which violates the principle of having a "local computer" and is a likely candidate for a patch release or v1.4.0.

### 7. User Feedback Summary
- **"It just got confused and stopped working"** ([#7748](https://github.com/nearai/ironclaw/pull/7748)): This is the most alarming piece of feedback, indicating that users are still hitting a hard failure state where the agent becomes unproductive. This is a **top-priority issue** requiring immediate investigation.
- **Need for Local MCP**: The persistent issue [#5998](https://github.com/nearai/ironclaw/pull/5998) (open since July) underscores that users expect the agent to be able to talk to local services on their own machine.

### 8. Backlog Watch
These issues have been open for a significant time and need attention.

- **[#5998](https://github.com/nearai/ironclaw/pull/5998) — No transport for a local (on-device) MCP server** (open since 07-11): This is a **major functional gap** for a personal AI assistant. The fact that it has been open for over a month and was just recently addressed in PR #7757 suggests it was a known limitation. It is crucial to get this fix merged and released.
- **[#7255](https://github.com/nearai/ironclaw/pull/7255) — Governance framework evaluation (APDD kit)**: This large docs PR has been open since 08-05. While not code, it represents a significant investment in process. Its slow review could indicate the team is stretched thin on reviewing large, non-code changes, potentially delaying broader DX improvements.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest
**Date: 2026-08-20** | Source: github.com/netease-youdao/LobsterAI

---

## 1. Today's Overview

LobsterAI shows a **steady-state maintenance pattern** with **no new releases** published in the last 24 hours. The project processed **8 closed PRs** (all merged) against **6 open issues** that remain stale (last updated ~4 months ago). Notably, **all 8 merged PRs were authored and merged on 2026-08-19**, indicating an active development push this week. The issue tracker shows **no new bug reports in the last 24 hours**, and all existing issues are tagged `[stale]`, suggesting either good stability or a need for issue backlog grooming. The PR activity focuses heavily on **Windows installer fixes, bug fixes from April, and UX improvements**, indicating the team is clearing a QA/closing backlog rather than shipping new features.

---

## 2. Releases

**No new releases in the last 24 hours.**

The latest known release remains **version 2026.4.3** (referenced in [Issue #1566](https://github.com/netease-youdao/LobsterAI/issues/1566)). Users on this version have reported several regressions (see Bugs & Stability section), so a new release addressing these issues may be imminent given the cluster of fix PRs merged today.

---

## 3. Project Progress

**8 PRs merged today**, spanning infrastructure, bug fixes, and UX polish:

### Windows Installer / Build (3 PRs)
- **[PR #2512](https://github.com/netease-youdao/LobsterAI/pull/2512)** — `fix(installer): hide banner for dictbind silent package` — Hides a plugin-owned silent Banner specifically for dictbind silent channel artifacts while preserving behavior elsewhere; includes spec updates and contract coverage.
- **[PR #2511](https://github.com/netease-youdao/LobsterAI/pull/2511)** — `fix(installer): support silent upload-first web builds` — Adds a two-pass Windows web-installer flow for NOS-hosted payloads, rebuilding only the signed stub while reusing the uploaded payload, with SHA-256 invariants to prevent payload invalidation.
- **[PR #1582](https://github.com/netease-youdao/LobsterAI/pull/1582)** — `fix(setup-python): 检测并覆盖旧版本的pip文件` — Fixes pip recursion errors caused by stale `__main__.py` files from older installs not being overwritten; improves `checkRuntimeHealth` to validate file contents, not just existence.

### Bug Fixes (3 PRs)
- **[PR #1570](https://github.com/netease-youdao/LobsterAI/pull/1570)** — `fix(scheduledTasks): editing a disabled task re-enables it` — Fixes a logic bug where `enabled` was hardcoded to `true` on save in edit mode; now reads and preserves the task's current state.
- **[PR #1576](https://github.com/netease-youdao/LobsterAI/pull/1576)** — `fix(api): SSE 流监听器竞态条件` — Fixes a race condition where an old request's async abort callback could clear the new request's SSE listeners (shared `cleanupFunctions` array), causing silent streaming data loss.
- **[PR #1573](https://github.com/netease-youdao/LobsterAI/pull/1573)** — `feat(im): 为 IM 渠道新增斜杠命令支持` — Adds slash commands (`/help`, `/status`, `/new`, `/compact`) for IM channels (Telegram/钉钉/飞书/Discord/QQ/微信), enabling lightweight session control without desktop client.

### UX Improvements (2 PRs)
- **[PR #1578](https://github.com/netease-youdao/LobsterAI/pull/1578)** — `feat(permission-modal): 权限审批弹窗增加 Bash 命令语法高亮` — Adds syntax highlighting to Bash commands in the permission approval modal, helping users quickly spot risky flags like `rm -rf` or `--force`.
- **[PR #1580](https://github.com/netease-youdao/LobsterAI/pull/1580)** — `feat(prompt-input): 输入框图片附件展示缩略图预览` — Replaces the generic photo icon with 64×64 thumbnail previews for image attachments, with a hover-to-delete action.

---

## 4. Community Hot Topics

**Issue #1569** — *[提问后不运行，也不显示任何信息](https://github.com/netease-youdao/LobsterAI/issues/1569)* — **5 comments, most active issue**
> **Content:** Unknown failure: user asks a question, nothing runs, nothing displays. No error output at all. *Note: This may be related to the SSE race condition fixed in PR #1576.*

**Issue #1566** — *[最新版本无论输入什么都回复相同内容](https://github.com/netease-youdao/LobsterAI/issues/1566)* — **2 comments**
> **Content:** Version 2026.4.3 replies with identical content regardless of input. Logs attached. *High severity: core functionality broken.*

**Issue #1561** — *[模型无法获取上传的文件](https://github.com/netease-youdao/LobsterAI/issues/1561)* — **2 comments**
> **Content:** Regression: file uploads no longer visible to the model. Previous versions placed files in the project directory and the model could search there; new versions break this flow.

**Analysis:** The most active issues all cluster around **regressions in version 2026.4.3** — silent failures, identical responses, and broken file uploads. These are quality-of-life and core-functionality issues that should be prioritized. The underlying need is clearly for a **patch release** — several fix PRs merged today (e.g., #1576 for SSE race, #1582 for pip) likely address these.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| 🔴 **Critical** | [#1566](https://github.com/netease-youdao/LobsterAI/issues/1566) | **Identical responses to any input** on v2026.4.3 — core LLM interaction broken | Not found |
| 🔴 **Critical** | [#1569](https://github.com/netease-youdao/LobsterAI/issues/1569) | **Silent failure** — no execution, no error output, no feedback | Possibly [#1576](https://github.com/netease-youdao/LobsterAI/pull/1576) (SSE race) |
| 🟠 **High** | [#1561](https://github.com/netease-youdao/LobsterAI/issues/1561) | **File uploads invisible to model** — regression from project-directory behavior | Not found |
| 🟡 **Medium** | [#1551](https://github.com/netease-youdao/LobsterAI/issues/1551) | **Gateway repeatedly restarts** on network environment changes | Not found |
| ⚪ **Low** | [#1563](https://github.com/netease-youdao/LobsterAI/issues/1563) | **Typos in traffic package service terms** legal text | Not applicable |

**Note:** All bugs were filed 2026-04-08 and remain **open and stale** (~4 months without maintainer response). PR #1576 directly addresses a plausible root cause for #1569's silent streaming loss, and PR #1582 fixes pip issues that may relate to setup failures.

---

## 6. Feature Requests & Roadmap Signals

**Explicit requests from users:**

1. **[Issue #1567](https://github.com/netease-youdao/LobsterAI/issues/1567)** — *Input box quick-action buttons:* Stop current session, compress context, force-stop fallback, and a `/help` command. This matches the slash-command functionality **already merged in PR #1573**, suggesting the community's asks are being actively addressed.

2. **IM channel controls** (implied by PR #1573): Users want lightweight control of Agent sessions from chat platforms without the desktop client — already shipped.

3. **File attachment visibility** (Issue #1561): The model should "know" about uploaded files, as in older versions. This is a regression to fix, not a new feature.

**Prediction for next release:** Expect a **patch release (v2026.4.4 or similar)** that includes:
- Fixes from PRs #1576 (SSE race), #1582 (pip), #1570 (scheduled tasks)
- Slash command support for IM channels from PR #1573
- UX improvements from #1578 & #1580 (already merged)
- Windows installer robustness from #2511 & #2512

---

## 7. User Feedback Summary

**Pain points (from issues):**

- **Silent failures** (#1569): The most frustrating UX — no error message, no indication of what went wrong. Users are left guessing.
- **Regression anxiety** (#1561, #1566): Users report features that *used to work* breaking in new versions — file visibility and consistent responses. This erodes trust in updates.
- **Recovery mechanisms** (#1567): Users explicitly ask for escape hatches — stop/compact/fresh-start buttons — when things go wrong, indicating they *expect* failures and want control.
- **Environmental fragility** (#1551): Network changes causing gateway restarts — an edge case for mobile/roaming users.

**Positive signals:**
- No new bug reports in the last 24 hours.
- The fix rate (8 PRs merged today) is strong relative to open issue count.

**Overall sentiment:** Users are **moderately dissatisfied** with v2026.4.3 stability but engaged enough to file detailed reports with logs and screenshots. The community's feature requests are being shipped, which is a positive signal for trust recovery.

---

## 8. Backlog Watch

⚠️ **All 6 open issues are marked `[stale]` and have not received maintainer responses in ~4 months.**

**Critical attention needed:**

1. **[Issue #1566 — Identical responses bug](https://github.com/netease-youdao/LobsterAI/issues/1566)** — Core functionality broken, 4 months unanswered. This is a release-blocking bug that must be triaged immediately.

2. **[Issue #1569 — Silent failures](https://github.com/netease-youdao/LobsterAI/issues/1569)** — 5 comments, no maintainer reply. PR #1576 likely fixes this, but the issue should be linked and closed.

3. **[Issue #1561 — File upload regression](https://github.com/netease-youdao/LobsterAI/issues/1561)** — Recent feature regression, needs a fix PR or a rollback plan.

4. **[Issue #1551 — Gateway restart loop](https://github.com/netease-youdao/LobsterAI/issues/1551)** — Environmental edge case, but annoying enough to warrant a fix or workaround.

5. **[PR #2511](https://github.com/netease-youdao/LobsterAI/pull/2511) & [#2512](https://github.com/netease-youdao/LobsterAI/pull/2512)** — Merged today; verify the Windows installer changes are released and tested, since install issues (like #1582) have historically caused user-side problems.

**Recommendation:** Establish a stale-issue grooming policy. Four months without a maintainer response on critical bugs is a community trust risk, even with a healthy merge rate.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Based on the GitHub data for Moltis (moltis-org/moltis) for 2026-08-20, here is the project digest.

---

## Moltis Project Digest — 2026-08-20

### 1. Today's Overview
The project shows a **high and focused level of activity**, with a burst of 10 PRs updated in the last 24 hours and 3 bugs closed. The development focus is heavily weighted toward **fixing backend integration issues** (Apple Container, OpenAI routing) and **hardening security** (CWE-306 vault authentication). All open PRs are from the last two days, indicating maintainers are actively shepherding these changes to merge. The presence of three separate, non-trivial security fixes in the pipeline suggests a possible security audit or self-imposed hardening sprint. Overall, this signifies a healthy, responsive project in a stabilization and polish phase.

### 2. Releases
**New Release:** `20260818.10` (2026-08-18)

### 3. Project Progress
Five PRs were merged or closed today, marking significant progress in backend reliability and LLM integration:

- **Apple Container Backend Fixes:** Two major fixes landed for the Apple Container backend.
  - [PR #1215](https://github.com/moltis-org/moltis/pull/1215) now correctly applies memory, CPU, and PID limits to sandboxes, resolving resource limit issues. This directly addresses closed bug [#1188](https://github.com/moltis-org/moltis/issues/1188).
  - [PR #1214](https://github.com/moltis-org/moltis/pull/1214) fixes a critical status-parsing bug across Apple Container versions (1.x vs. pre-1.x), addressing the "sandbox starts but is reported as not running" issue [#1185](https://github.com/moltis-org/moltis/issues/1185).
- **OpenAI Routing Enhancements:** The team completed a series of changes to model routing.
  - [PR #1213](https://github.com/moltis-org/moltis/pull/1213) adds test coverage for the new GPT-5.6 Luna model and ensures the model-health list stays in sync.
  - [PR #1212](https://github.com/moltis-org/moltis/pull/1212) fixes a regression where explicitly configuring the official OpenAI URL would bypass the experimental Responses API routing (see #1198).
  - [PR #1198](https://github.com/moltis-org/moltis/pull/1198) was merged, finalizing the routing of OpenAI reasoning tool calls through the Responses API, with Chat Completions retained as a fallback for other cases. This explains the fix in #1212 and contributes to closing bug [#1181](https://github.com/moltis-org/moltis/issues/1181).

### 4. Community Hot Topics
- **[Issue #1185](https://github.com/moltis-org/moltis/issues/1185): "[Bug]: Apple Container 1.x sandbox starts but Moltis treats it as not running"** — This issue, though closed, had the most discussion (3 comments) in the last 24 hours. The discussion reflects user stress around **identifying and debugging subtle version-compatibility issues** with container backends, which could lead to frustrating phantom failures.

### 5. Bugs & Stability
Three bugs were closed today, all fixed by incoming PRs. Ranked by severity:

1.  **Critical - Unauthenticated Vault Brute-Force (CWE-306):** [PR #1216](https://github.com/moltis-org/moltis/pull/1216) fixes a vulnerability where any remote caller could attempt to unlock the vault without authentication. This is a severe security issue that takes top priority.
2.  **High - Phantom Sandbox State:** The Apple Container status parsing failure ([PR #1214](https://github.com/moltis-org/moltis/pull/1214)) could cause the system to believe a sandbox is down when it's actually running, potentially leading to incorrect agent behavior.
3.  **Medium - Resource Limit Bypass:** [PR #1215](https://github.com/moltis-org/moltis/pull/1215) fixes sandbox memory and CPU limits not being applied, which could lead to a single job consuming all host resources.
4.  **Medium - Model Routing Regression:** [PR #1212](https://github.com/moltis-org/moltis/pull/1212) fixes a regression where certain configurations (explicit OpenAI URL) would incorrectly disable the new Responses API routing path, breaking tool-calling for users with specific setups.

### 6. Feature Requests & Roadmap Signals
The most significant roadmap signal is the **continued investment in the Responses API** and GPT-5.6 model support. The PRs suggest a strategy to default to this modern API for its improved tool-calling and reasoning capabilities, with a clear fallback to legacy Chat Completions for reliability.

There is also a clear theme of **making the system more configurable**. The open PRs to make the untrusted-turn tool ceiling ([#1219](https://github.com/moltis-org/moltis/pull/1219)) and WhatsApp push name ([#1218](https://github.com/moltis-org/moltis/pull/1218)) configurable point to a desire to reduce hardcoded behavior and allow for more user customization.

### 7. User Feedback Summary
User pain points this week centered on **deep integration bugs** rather than UX. The issues reported (Apple Container sandbox misreporting, resource limits ignored) suggest users are actively using advanced backend features. Their quick reporting and the maintainers' equally quick fixes indicate a **high level of engagement** and a tight feedback loop. There is also potential user frustration around configurability, as seen in the PRs fixing hardcoded settings for tool policies, push names, and heartbeat schedules.

### 8. Backlog Watch
This delivery cycle shows no major signs of maintainer neglect. The open PRs up for review include:

- **[PR #1208](https://github.com/moltis-org/moltis/pull/1208): "fix(cron): honor heartbeat active hours"** (Opened 2026-08-17) — This fix for a documented but non-functional feature has been open for a few days, and might be waiting for review.
- **[PR #1217](https://github.com/moltis-org/moltis/pull/1217): "fix(whatsapp): treat a reply to the bot as addressing it"** (Opened 2026-08-19) — A behavior fix for the WhatsApp channel that is pending merge.

All other open PRs are from today, so they are not considered backlogged.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-20

---

## 1. Today's Overview

CoPaw is in a **high-velocity maintenance burst** with 50 issues and 47 PRs touched in the last 24 hours. Activity skews heavily toward **bug fixing and stability hardening** (8 of the top PRs are fixes) rather than new features. The reopened installer/corruption issue (#2884) plus the stalled-stream freeze bug (#7102) suggest user trust is being tested, but the project is responding quickly — dedicated fix PRs exist for both. No new releases shipped today. The close ratio (46 closed vs 4 open issues) indicates strong triage discipline, though the long tail of stale issues from March–April still being bulk-closed suggests some housekeeping may be automated.

---

## 2. Releases

**No new releases** published in the last 24 hours. Users remain on QwenPaw Desktop 2.1.0 (referenced in issue #7102) and CoPaw v1.0.0.post3 (issue #2856).

---

## 3. Project Progress

Several merged/closed PRs advanced stability and UX today:

| PR | Description | Status |
|---|---|---|
| [#6986](https://github.com/agentscope-ai/CoPaw/pull/6986) | **fix(sandbox): fix antivirus software blocking issues** — addresses the recurring AV-kill problem reported by multiple users | Merged |
| [#7103](https://github.com/agentscope-ai/CoPaw/pull/7103) | **test(integration): expand coverage** for routing, channels (DingTalk, Feishu, Matrix, QQ, Telegram, WeChat, WeCom, OneBot), tools, MCP, and coding projects | Merged |
| [#7137](https://github.com/agentscope-ai/CoPaw/pull/7137) | **fix(console): polish model selector styles** | Merged |
| [#7151](https://github.com/agentscope-ai/CoPaw/pull/7151) | **feat(console): add folder creation** to Files directory browser with icon refinements | Merged |

**Notable open PRs** (merged status pending but substantive):

- [#7150](https://github.com/agentscope-ai/CoPaw/pull/7150) — **fix: detect and recover from stalled LLM streams** (directly targets #7102, the freeze bug)
- [#7146](https://github.com/agentscope-ai/CoPaw/pull/7146) — **fix(view_image): freeze remote images** with SSRF/bounded-download protections before persisting
- [#7135](https://github.com/agentscope-ai/CoPaw/pull/7135) — **fix(envs): preserve corrupt files and write atomically**

---

## 4. Community Hot Topics

**Highest engagement — Issue #2884** (27 comments, closed): [链接](https://github.com/agentscope-ai/CoPaw/issues/2884)

> User reports their home directory was **nearly wiped clean** and CoPaw itself was deleted after leaving their machine idle over lunch. Highly alarming — whether a real vulnerability or user error, this needs a clear post-mortem. The fact it was closed (presumably resolved/explained) without appearing in release notes suggests work is needed on **safety guardrails and user communication** around destructive operations.

**Issue #2301** (10 comments, closed, 👍1): [链接](https://github.com/agentscope-ai/CoPaw/issues/2301) — Feature wishlist: one-click update button, `/approve` as buttons instead of text, auto model-switching with a ranking ladder, built-in self-reflection/self-evolution, browser/mobile state sync, and additional providers (Zhipu, Meituan). Strong signal for **UX polish and model resilience**.

**Issue #2035** (10 comments, closed): [链接](https://github.com/agentscope-ai/CoPaw/issues/2035) — Multi-agent collaboration: how to bind each agent to a different bot, multi-agent collaborative conversations. **April issue, closed only now** — lag suggests the feature gap is real.

**Issue #7102** (9 comments, open): [链接](https://github.com/agentscope-ai/CoPaw/issues/7102) — **QwenPaw 2.1.0 freezes ≥10 minutes** when using GLM 5.3, no tokens, no thinking output. Fix PR #7150 is under review.

**Issue #2723** (9 comments, closed): [链接](https://github.com/agentscope-ai/CoPaw/issues/2723) — Switching channels **erases the current task** entirely (requirements and agent execution). Critical UX flaw for multitasking users.

**Issue #2377** (9 comments, closed): [链接](https://github.com/agentscope-ai/CoPaw/issues/2377) — Agent **stops working after only a few files** when asked to process 1500 files, despite batching/pause-resume settings.

---

## 5. Bugs & Stability

Ranked by severity:

| # | Issue | Description | Fix PR? |
|---|---|---|---|
| 1 | [#2884](https://github.com/agentscope-ai/CoPaw/issues/2884) | **Home directory wiped** + CoPaw deleted | None published |
| 2 | [#7102](https://github.com/agentscope-ai/CoPaw/issues/7102) | **Indefinite freeze**, "Thinking" state persists, no tokens (QwenPaw 2.1.0 + GLM 5.3) | [#7150](https://github.com/agentscope-ai/CoPaw/pull/7150) |
| 3 | [#2723](https://github.com/agentscope-ai/CoPaw/issues/2723) | **Task loss on channel switch** — agent, requirements, and progress all vanish | None |
| 4 | [#3005](https://github.com/agentscope-ai/CoPaw/issues/3005) | **Install breaks app startup** (pip upgrade + PowerShell installer) | None |
| 5 | [#6847](https://github.com/agentscope-ai/CoPaw/issues/6847) | **Antivirus kills QwenPaw** during task execution; WorkBuddy unaffected | [#6986](https://github.com/agentscope-ai/CoPaw/pull/6986) (merged) |
| 6 | [#7034](https://github.com/agentscope-ai/CoPaw/issues/7034) | **`async for` TypeError** in ReactAgent tool execution (Python 3.12) | None |
| 7 | [#2663](https://github.com/agentscope-ai/CoPaw/issues/2663) | **Settings don't persist** — UI reverts to English/light mode on restart; tasks stall mid-run | None |
| 8 | [#7135](https://github.com/agentscope-ai/CoPaw/pull/7135) | **Corrupt env files** may be overwritten — PR preserves and writes atomically | Open PR |

**Pattern**: Freezes, task loss, and AV interference dominate. The project is actively fixing two of the top three (#7102, #6847), which is good, but #2723 (data loss on channel switch) and #2884 (directory wipe) are trust-critical and need public root-cause analysis.

---

## 6. Feature Requests & Roadmap Signals

Strong, repeated signals across issues:

| Request | Votes/Comments | Evidence |
|---|---|---|
| **Auto model-switching / fallbacks** | 🔥🔥🔥 | #2301 (asked), #2089 (closed, asked for fallbacks), #3260 ("multiple AI providers per agent") |
| **One-click updates, as buttons** | 🔥🔥 | #2301 — update button, `/approve` as buttons |
| **Multi-agent ↔ multi-bot binding & collaboration** | 🔥🔥 | #2035 (10 comments), #2385 (CLI port design flaw breaks this) |
| **Mobile/web continuation & sync** | 🔥🔥 | #2301 — continue from phone; #2856 — mobile UI barely usable |
| **Better browser automation** | 🔥 | #3261 — bot detection triggers, can't reuse login state |
| **Larger local models (14B/27B/32B)** | 🔥 | #2856 — 9B too small; #2776 — user interest in VRAM profiles |
| **File operation rollback (undo)** | 🔥 | #2590 — recovering accidentally deleted files (design discussion with 7 comments) |
| **Deeper reasoning/execution (DeerFlow/LongGraph-style)** | 🟡 | #3074, #3260 |
| **Custom gateway support (non-OpenAI formats)** | 🟡 | #2296 — enterprise private LLM gateways |
| **Self-evolution / self-reflection** | 🟡 | #2301 — "make it better the more you use it" |

**Next-release predictions**: The stalled-stream watchdog (#7150) and remote-image freezing (#7146) are likely to land in the next patch. The Volcengine/MiMo provider PR (#6515) and multi-project session directories (#6976) are the closest to feature-level merges. **Auto model-fallback** is the most-requested feature with zero maintainer response — expects to appear soon given user pressure.

---

## 7. User Feedback Summary

**Pain points (repeat offenders):**

- **Task interruption with no resume path** — #2377 (dump after a few files), #2663 (stall mid-task, pause button dead), #2723 (task erased entirely)
- **Model instability** — #7102 freezes, #2598 non-thinking models underperform in Skills, #2089 API limits kill workflows
- **Install/upgrade fragility** — #3005, #3177, #7076 (404 errors in config)
- **AV/interference** — #6847 (AV kills process; competitor doesn't suffer), #2884 (home dir wiped)
- **Mobile experience** — #2856: "phone browser view is terrible, can't even see the input box"

**Positive signals:**

- Local model performance: #2776 — "very smooth token output" on RTX 3080 10G with copaw-flash-4b — indicates reasonable local viability
- Users express "would be great/awesome" enthusiasm repeatedly (#2301) — the product concept resonates, execution gaps frustrate

**Underlying narrative**: Users *want* CoPaw as a trusted autonomous agent — they're pushing it against real workloads (batch file processing, long-running research, automated email via #6800). But today it feels **fragile under sustained autonomous operation**: context limits, stream stalls, no crash recovery, no undo. The most common emotional note is "it worked for a bit, then died without explanation."

---

## 8. Backlog Watch

Items that need maintainer attention:

| Item | Age | Status | Why it matters |
|---|---|---|---|
| [#2035](https://github.com/agentscope-ai/CoPaw/issues/2035) — Multi-agent multi-bot binding | Since Mar 21 (~5 months) | Closed today, no roadmap answer visible | Second most-commented issue; feature is core to agentic vision |
| [#2089](https://github.com/agentscope-ai/CoPaw/issues/2089) — **Fallback models** | Since Mar 23 (~5 months) | Closed, no merged PR referenced | Top requested resilience feature; unaddressed |
| [#2296](https://github.com/agentscope-ai/CoPaw/issues/2296) — Enterprise gateway support | Since Mar 25 | Closed, no PR | Enterprise adoption blocker (needs custom headers/data formats) |
| [#2385](https://github.com/agentscope-ai/CoPaw/issues/2385) — CLI port management breaks multi-agent | Since Mar 27 | Closed, no fix referenced | Design flaw actively breaking a core feature |
| [#2590](https://github.com/agentscope-ai/CoPaw/issues/2590) — **File operation rollback** | Since Mar 30, 7 comments | Closed, no implementation result visible | Directly addresses the #2884 class of trust-destroying bugs |
| [#7102](https://github.com/agentscope-ai/CoPaw/issues/7102) — Freeze with GLM 5.3 | Aug 18 (2 days) | Open, fix PR under review | Needs fast merge + release |

**Context on closures**: A bulk of March–April issues were closed on Aug 19. This may be a migration to a new tracking system, a clean-sweep, or genuine fixes (that timeframe matching the merged AV fix is plausible). But for #2035, #2089, and #2385 — all closed without visible resolution — the community deserves explicit "won't fix / future roadmap" statements rather than silent closure.

---

### Project Health Summary

| Dimension | Status |
|---|---|
| Development velocity | 🟢 High (17 merged/closed PRs in 24h) |
| Responsiveness to bugs | 🟢 Good for recent regressions (#7102, #6847) |
| Responsiveness to feature requests | 🟡 Weak — 5-month-old top requests closed without visible resolution |
| Trust & safety | 🔴 Data-loss reports (#2884, #2723) without public post-mortems |
| Release cadence | 🟡 None in 24h; last known: 2.1.0 (Aug) / 1.0.0.post3 (older) |

---

*Data source: [github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw) — retrieved 2026-08-20.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the provided GitHub data for ZeroClaw (zeroclaw-labs/zeroclaw), here is the project digest for 2026-08-20.

---

## ZeroClaw Project Digest — 2026-08-20

### 1. Today's Overview

ZeroClaw is in a period of intense architectural and security-focused development. Activity is extremely high, with 42 issues and 50 pull requests updated in the last 24 hours, though the number of new items is lower, suggesting a focus on iterating on existing work. The project is in the midst of several large, cross-cutting RFCs and trackers (e.g., session ownership, WASM plugin architecture, and anti-slop code remediation) that are driving significant refactoring, especially within the Rust codebase.

The maintainer team is highly active, with many discussions marked `needs-maintainer-review` and several complex PRs from distinguished contributors awaiting further input or author action. While there are no new releases today, the level of activity indicates a substantial amount of work is in progress toward what will likely be a major upcoming release.

### 2. Releases

No new releases were published in the last 24 hours. The most recent release remains v0.8.4, which shipped prior to this period.

### 3. Project Progress

Only two PRs were closed or merged today, but they are highly significant:

- **[PR #10145 (CLOSED)]:** This PR, titled 'chore: withdrawn', was closed by the author, JordanTheJet. While the reason is not specified in the data, this signals that a possibly problematic approach was abandoned in favor of other active efforts.
- **[Issue #10067 (CLOSED)]:** A high-severity bug regarding tool-result truncation was closed. The issue was re-scoped after initial analysis proved the original report incorrect, leading to a fix for the actual issue of byte-wise structured output truncation and a lack of operator visibility.

The most substantive progress is happening in large, open PRs that are inching toward completion:

- **[PR #9694]** - `feat(zerocode): expose the SOP pane as a read-only status view` - This highlights a focus on improving operator visibility into Standard Operating Procedures (SOPs). While not merged, its continued activity suggests it is nearing final review.
- **[PR #9745]** - `fix(memory): add per-agent attribution and scoping to the knowledge graph` - A critical security and correctness fix to prevent data leakage between agents using the shared knowledge graph. This has progressed, indicating a strong focus on multi-tenant data isolation.
- **[PR #10134]** and **[PR #10129]** - Both by JordanTheJet, these refactoring PRs aim to remove panic candidates from runtime and tool paths, aligning with the project's anti-slop policy. Their creation yesterday shows an aggressive push toward production hardening.

### 4. Community Hot Topics

The most active discussions reveal a community deeply concerned with architecture, security, and long-term maintainability.

- **[Issue #9487: RFC: Runtime-owned conversation sessions and transport surface adapters (20 comments)]** - This is the central architectural debate on how conversation sessions should be owned and managed by the runtime. The high level of engagement indicates this is a foundational decision that will shape the project's future, aiming to unify various entry points and add durable semantics.
- **[Issue #7462: [Bug]: 74 test failures on Windows (18 comments)]** - A long-standing (since June) and critical portability issue. The sustained engagement highlights community frustration with Windows support, a key pain point for user adoption. The need for a robust CI solution for Windows is a clear takeaway.
- **[Issue #10118: [Tracker]: Rust anti-slop policy debt remediation (16 comments)]** - This tracker is coordinating a massive cleanup of code patterns that conflict with the project's new production-code policy (307 candidates). It shows a strong commitment to code quality with a strict, community-visible process.
- **[Issue #6165: RFC: Prefer a lighter ZeroClaw core through external integrations (16 comments)]** - A long-running debate about modularizing the core. The community is actively discussing which integrations should be built-in versus optional, indicating a desire for a more streamlined, less complex default installation.
- **[Issue #8692: [Tracker]: Maintainer decision queue for RFCs and design issues (13 comments)]** - This tracker is itself a hot topic, acting as a public roadmap for pending maintainer decisions. It demonstrates a high level of process transparency and community involvement in the project's governance.

### 5. Bugs & Stability

Today's updates show a strong focus on identifying and fixing critical stability and security bugs.

**Critical (S0/S1):**
- **[Issue #9976]:** `bug(provider): stop logging Anthropic credential fragments` - An **S0 security risk** where debug-level logging exposes parts of API credentials. The fix is likely in progress, but this is the highest priority item.
- **[Issue #10066]:** `[Bug]: SOP engine promotes and runs later steps before recording a step's output-schema rejection` - An **S1 workflow-blocking** bug where the engine executes subsequent steps even after a validation failure. The fix (PR #10134) includes work on SOP dispatch, suggesting a fix is imminent.
- **[Issue #10067]:** `[Bug]: tool-result truncation is a fixed 50,000 chars, invisible to operators...` - This was **closed**, meaning a fix was found and implemented (or re-scoped) during this period.
- **[Issue #9290]:** `[Bug]: Windows desktop installer fails at launch with missing TaskDialogIndirect` - An **S1** user-facing bug preventing the desktop app from launching on Windows, compounding the Windows support issues.

**High Priority (P1/P2):**
- **[Issue #9397]** - RFC on empty WhatsApp Web `allowed_groups` acting as permit-none (security hardening).
- **[Issue #10106]** - [Bug]: Exact proxy selectors rejecting supported transcription services (broken configuration).
- **[Issue #10045]** - [Bug]: Persisted image markers retaining temporary source paths (data consistency).

**Fixes in Progress:**
- **[PR #9447]** - `fix(anthropic): classify incomplete terminal responses` - This large, in-progress PR aims to fix critical bugs related to the Anthropic provider (related to #9976 and general response handling).

### 6. Feature Requests & Roadmap Signals

Several open issues provide a clear signal for future development:

- **[Issue #10141: [Feature]: Please make sessions usable]** - A direct user request expressing frustration with session management in ZeroCode. This will likely drive UX improvements in the Zed editor-like interface.
- **[Issue #10076: RFC: Comprehensive WASM plugin architecture]** - A forward-looking proposal to expand the plugin system to cover all components ("everything is a plugin"). This is a major architectural signal that could define the roadmap for v0.9.0 or v1.0.
- **[Issue #10086: [Feature]: Make ZeroCode Logs text selectable and copyable]** - A small, quality-of-life feature request that is likely easy to implement in the short term.
- **[Issue #10059: [Feature]: Support Option-Backspace word deletion in ZeroCode text inputs]** - Another macOS-specific UX improvement, tagged as a `good first issue`, suggesting low complexity.
- **[PR #10142]:** `feat(relay): secure transport and browser enrollment frontdoor` - This new PR signals a major effort to improve remote access and security by introducing mutual TLS and a secure relay (ZeroRelay).

### 7. User Feedback Summary

The most explicit user feedback comes from Issue #10141, where klonuo expresses clear frustration with the current session management ("It's quite frustrating to get into previous session"). The quality-of-life feature requests (Option-Backspace, copyable logs) also point to a user base paying attention to detail in the ZeroCode interface.

The long-standing Windows issues (#7462, #9290) are a persistent source of dissatisfaction. The active, 18-comment thread on test failures suggests a significant portion of the community is on Windows and feels let down by the lack of first-class support and CI coverage.

There is a clear split in sentiment: the community is highly engaged and supportive of the architectural RFCs and security hardening, but they are also vocal about immediate usability issues, particularly on Windows and in the ZeroCode interface.

### 8. Backlog Watch

The following items are critical, long-running, and require attention to unblock progress:

- **[Issue #7462 (created 2026-06-10):]** The Windows test failure bug is over two months old with no fix in sight. This is a major blocker for Windows users and should be a top priority for the maintainers.
- **[Issue #8692 (created 2026-07-04):]** The "Maintainer decision queue" itself suggests a bottleneck. Many high-impact RFCs (like #9487, #6165) are awaiting a final decision, and the pace of new proposals (like #10076) may be outpacing the maintainers' capacity to review them.
- **[PR #9320 (created 2026-07-23):]** `fix(cron): bound agent job runs with a wall-clock timeout` - This high-risk PR from a distinguished contributor has been open for nearly a month and is marked with `needs-author-action`. It appears stalled, and its fix is important for system stability.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*