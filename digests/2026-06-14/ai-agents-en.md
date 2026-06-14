# OpenClaw Ecosystem Digest 2026-06-14

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-14 02:13 UTC

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

# OpenClaw Project Digest — 2026-06-14

---

## 1. Today's Overview

OpenClaw shows **extremely high activity** with 500 issues and 500 PRs updated in the last 24 hours — an unusually dense day of community engagement and maintainer attention. Two new beta releases arrived (v2026.6.7-beta.1 and v2026.6.8-beta.1), both focused on **channel delivery robustness** across Telegram, WhatsApp, Slack, and Feishu. However, the project continues to grapple with a **backlog of high-severity bugs** — several P0/P1 issues around memory leaks, silent message loss, subagent timeouts, and security vulnerabilities remain open for weeks. While the release cadence is healthy, the volume of open critical issues suggests the project is struggling to keep pace with community-reported regressions.

---

## 2. Releases

**Two new beta releases today:**

### v2026.6.8-beta.1
- **Telegram**: Structured rich text delivery with tables, lists, expandable blockquotes; CLI backend delivery improvements; retired native draft migration; safer rich-media boundaries
- **WhatsApp**: Richer, more reliable message delivery
- **Breaking changes**: None documented; backward-compatible improvements

### v2026.6.7-beta.1
- **Slack**: Same-channel finals persist in transcripts
- **Image tool**: Top-level `image` message-tool now sends attached media
- **Telegram**: Expandable blockquotes and spool improvements
- **General**: Silent replies, progress drafts, paged action results tightened

**Migration notes**: No breaking changes reported. Users on previous beta channels can upgrade via `npm install -g openclaw@latest`.

---

## 3. Project Progress

**Today's merged/closed PRs (192 total):**

- [#92826](https://github.com/openclaw/openclaw/pull/92826) — `fix(outbound): suppress media sends without delivery identity` (QQBot cron/TTS fix)
- [#92829](https://github.com/openclaw/openclaw/pull/92829) — `ci: migrate Claude workflows to AWS Bedrock` (infrastructure modernization)
- [#88059](https://github.com/openclaw/openclaw/pull/88059) — `feat(browser): extend --labels overlay to full-page and element captures` (merged after maintainer review)

**Features that advanced:**
- **Browser tool**: Full-page label overlays now merge-ready; ClawSweeper automerge loop enabled
- **Memory search**: Concurrent execution for `corpus=all` mode (PR [#92833](https://github.com/openclaw/openclaw/pull/92833))
- **CodeMirror 6 JSON editor**: Proposed for raw config view (PR [#75466](https://github.com/openclaw/openclaw/pull/75466))
- **Claude bridge extension**: New `app-server harness` for native Anthropic model support (PR [#86655](https://github.com/openclaw/openclaw/pull/86655))
- **Performance**: Export-state cache for QMD sessions (PR [#77158](https://github.com/openclaw/openclaw/pull/77158))

**Today's closed issues (109):** Included a P1 cron runtime contamination bug ([#90991](https://github.com/openclaw/openclaw/issues/90991)) and several stale/regression items.

---

## 4. Community Hot Topics

**Most commented issues (last 24h):**

1. **[#44925](https://github.com/openclaw/openclaw/issues/44925) — [P1] Subagent completion silently lost** (19 comments)
   - *Need*: Reliable subagent task orchestration with proper error surfacing. Users report agents silently dropping work with no retry, no notification, and no auto-restart on timeout — a critical reliability gap for multi-agent workflows.

2. **[#48183](https://github.com/openclaw/openclaw/issues/48183) — [P2] Feishu monitor state cleanup memory leak** (18 comments)
   - *Need*: HTTP server map entries persist after monitor stop; potential long-running memory leak. Users running Feishu integration at scale report degradation over time.

3. **[#54253](https://github.com/openclaw/openclaw/issues/54253) — [P2] LLM Request Failed on RISC-V64** (14 comments, 4 👍)
   - *Need*: Architecture support for RISC-V64 systems. The community is experimenting with OpenClaw on non-x86 hardware, and platform compatibility is becoming a pain point.

4. **[#90991](https://github.com/openclaw/openclaw/issues/90991) — [P1] Cron trigger contaminates global runtime state** (13 comments, now CLOSED)
   - *Need*: Scheduled tasks must not leak state across sessions. This was a high-severity system-wide overload issue fixed in today's cycle.

5. **[#45740](https://github.com/openclaw/openclaw/issues/45740) — [P2] gh-issues skill: untrusted body injection** (13 comments)
   - *Need*: Security — raw GitHub issue bodies injected into sub-agent prompts without sanitization. Community flagged prompt injection risk from third-party content.

**Most upvoted issue today:** [#42840](https://github.com/openclaw/openclaw/issues/42840) — MathJax/LaTeX support for Control UI (6 👍) — shows strong demand for scientific/mathematical communication features.

---

## 5. Bugs & Stability

### P0 Critical
- **[#91588](https://github.com/openclaw/openclaw/issues/91588) — Gateway memory leak (350MB → 15.5GB over days)**
  - *Impact*: Repeated OOM crashes, `launchd-handoff` restart cycles
  - *Fix PR*: None yet; needs maintainer review and product decision

### P1 High
- **[#44925](https://github.com/openclaw/openclaw/issues/44925) — Subagent completion silently lost** (no retry/notification)
  - *Fix PR*: Linked PR open; needs maintainer review
- **[#48003](https://github.com/openclaw/openclaw/issues/48003) — Steer mode does not inject mid-turn** (message loss in running turns)
  - *Fix PR*: Linked PR open
- **[#43367](https://github.com/openclaw/openclaw/issues/43367) — Multi-agent orchestration unstable** (config overwrites, session-lock failures)
  - *Fix PR*: Linked PR open
- **[#46786](https://github.com/openclaw/openclaw/issues/46786) — `tools.elevated.enabled` breaks exec routing** (regression)
  - *Fix PR*: None yet; security-impact regression
- **[#85251](https://github.com/openclaw/openclaw/issues/85251) — Codex app-server goes silent mid-turn** (session wedges for 360s)
  - *Fix PR*: Fix shape clear, source repro available

### P2 Medium
- **[#45565](https://github.com/openclaw/openclaw/issues/45565) — Gateway lifecycle warnings clutter active channels**
- **[#44910](https://github.com/openclaw/openclaw/issues/44910) — OpenAI Codex errors leak into user chat**
- **[#45494](https://github.com/openclaw/openclaw/issues/45494) — Cron jobs silently time out on LLM API outages** (instead of fast-failing)
- **[#43661](https://github.com/openclaw/openclaw/issues/43661) — Session hangs on compaction timeout** (duplicate message sends)

### Regressions
- **[#43747](https://github.com/openclaw/openclaw/issues/43747) — Memory management chaos** (inconsistent chunking/embedding across users)
- **[#38327](https://github.com/openclaw/openclaw/issues/38327) — "Cannot convert undefined or null to object"** with google-vertex/gemini-3.1
- **[#48045](https://github.com/openclaw/openclaw/issues/48045) — Browser tool silently discards downloads** via CDP

---

## 6. Feature Requests & Roadmap Signals

**Most requested features visible in today's data:**

| Request | Issue | Community Interest | Likelihood for Next Version |
|---------|-------|-------------------|----------------------------|
| **Memory Trust Tagging by Source** | [#7707](https://github.com/openclaw/openclaw/issues/7707) | Security-focused; 10 comments | **Low** — still in design phase; needs security review |
| **Per-agent cost budget enforcement** | [#42475](https://github.com/openclaw/openclaw/issues/42475) | 12 comments; operator use case | **Medium** — practical demand, clear scope |
| **MathJax/LaTeX rendering** in Control UI | [#42840](https://github.com/openclaw/openclaw/issues/42840) | 6 👍 highest today | **Medium** — quick UI win, high user visibility |
| **YAML config file support** | [#45758](https://github.com/openclaw/openclaw/issues/45758) | 2 👍, 7 comments | **Low** — nice-to-have; no implementation started |
| **Pre-reset memory flush** (before `/new`) | [#45608](https://github.com/openclaw/openclaw/issues/45608) | 4 👍, memory preservation | **Medium** — complements existing compaction flush |
| **Per-skill model routing** | [#43260](https://github.com/openclaw/openclaw/issues/43260) | 1 👍, CLOSED | **Already rejected/closed** — not on roadmap |
| **Path-scoped RWX permissions** for tools | [#39979](https://github.com/openclaw/openclaw/issues/39979) | Security; 7 comments | **Low** — requires architectural change |

**Prediction for v2026.7.x:**
- Memory trust tagging may enter design review given security momentum
- Per-agent cost budgets are likely to see a POC — the code scaffolding (`session-cost-usage.ts`) already exists
- MathJax/LaTeX support is a cheap high-visibility win that could ship quickly

---

## 7. User Feedback Summary

**Pain points (recurring themes):**

1. **Silent failures are the #1 frustration**
   - Subagent work lost with no notification ([#44925](https://github.com/openclaw/openclaw/issues/44925))
   - Cron jobs timeout silently on API errors ([#45494](https://github.com/openclaw/openclaw/issues/45494))
   - Browser tool discards downloads without warning ([#48045](https://github.com/openclaw/openclaw/issues/48045))
   - TUI `--session` mode not live-streaming messages ([#45388](https://github.com/openclaw/openclaw/issues/45388))

2. **Memory/context management is confusing and inconsistent**
   - Memory chunking varies across users ([#43747](https://github.com/openclaw/openclaw/issues/43747))
   - Context window over-reporting ([#39857](https://github.com/openclaw/openclaw/issues/39857))
   - Compaction timeouts cause duplicate sends ([#43661](https://github.com/openclaw/openclaw/issues/43661))

3. **Multi-agent orchestration is unreliable in practice**
   - Concurrent `agents add` corrupts config ([#43367](https://github.com/openclaw/openclaw/issues/43367))
   - Session write-locks block delivery lanes ([#86538](https://github.com/openclaw/openclaw/issues/86538))
   - No auto-retry or error surfacing for subagent failures ([#44925](https://github.com/openclaw/openclaw/issues/44925))

**Positive signals:**
- Telegram/WhatsApp delivery improvements in v2026.6.8-beta.1 address long-standing formatting complaints
- Users are actively experimenting on RISC-V64 and other architectures — enthusiasm for platform portability
- Community is providing detailed repro steps and root cause analysis (e.g., [#91588](https://github.com/openclaw/openclaw/issues/91588) memory leak with full environment details)

**Satisfaction mix:** High engagement suggests an active, invested user base, but the density of P1/P0 bugs indicates frustration with reliability, especially for production/cron deployments.

---

## 8. Backlog Watch

**Issues needing maintainer attention (last maintainer touch >30 days):**

| Issue | Age | Status | Reason for Concern |
|-------|-----|--------|-------------------|
| [#7707](https://github.com/openclaw/openclaw/issues/7707) — Memory Trust Tagging | 133 days | Needs maintainer review + security review | Community feature request with no design decision |
| [#39979](https://github.com/openclaw/openclaw/issues/39979) — Path-scoped RWX permissions | 98 days | Needs maintainer review + security review | Security architecture feature — silent for 3+ months |
| [#40418](https://github.com/openclaw/openclaw/issues/40418) — Session memory preservation | 97 days | Needs product decision | Competing with [#45608](https://github.com/openclaw/openclaw/issues/45608) — no direction set |
| [#40786](https://github.com/openclaw/openclaw/issues/40786) — Backup exclude patterns | 97 days | Linked PR open, needs review | Simple CLI improvement stuck in review |
| [#41165](https://github.com/openclaw/openclaw/issues/41165) — Telegram DMs polluting main session | 97 days | P1, needs live repro | Core routing bug — stale for 3 months |

**Stale issues that may need closure decisions:**
- [#42475](https://github.com/openclaw/openclaw/issues/42475) — Cost budget enforcement (stale, 96 days)
- [#45758](https://github.com/openclaw/openclaw/issues/45758) — YAML config (stale, P3, 92 days)
- [#39857](https://github.com/openclaw/openclaw/issues/39857) — Context window over-reporting (CLOSED today after 98 days)

**PRs waiting on author/maintainer >14 days:**
- [#46794](https://github.com/openclaw/openclaw/pull/46794) — Device pairing setup codes (91 days, P1, `waiting on author`)
- [#86655](https://github.com/openclaw/openclaw/pull/86655) — Claude bridge extension (20 days, `waiting on author`)
- [#90741](https://github.com/openclaw/openclaw/pull/90741) — Auth-profile fingerprint cache (9 days, `waiting on author`)

---

*Generated from 500 issues and 500 PRs updated 2026-06-13 to 2026-06-14. Data reflects activity up to digest generation time.*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report.

---

## Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date:** 2026-06-14

### 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is in a period of **intense, bifurcated development**. On one side, large reference implementations like OpenClaw and ZeroClaw are grappling with the reliability challenges of scale—memory leaks, multi-agent orchestration failures, and silent message loss dominate their backlogs. On the other side, a wave of smaller, rapidly iterating projects (NanoBot, PicoClaw, NanoClaw) are pushing boundaries in user experience, security hardening, and platform portability (RISC-V, Chinese messaging apps). A consistent theme across all projects is the community’s demand for **end-to-end reliability over raw feature count**, with "silent failures" being the single most-cited frustration. The ecosystem is maturing from experimental tooling toward production-grade infrastructure, but the gap between community expectation and maintainer bandwidth is palpable, particularly in OpenClaw and Hermes Agent.

### 2. Activity Comparison

| Project | Issues (Last 24h) | PRs (Last 24h) | Release Status (Today) | Health Score / Signal |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 (high, backlogged) | 500 (high, dense) | ✅ v2026.6.8-beta.1, v2026.6.7-beta.1 | ⚠️ **Strained** – High activity, but P0/P1 bugs are accumulating faster than they are resolved. |
| **ZeroClaw** | 42 (moderate) | 50 (high) | 🟡 None (tracking v0.8.1) | ⚠️ **Rapid but Fragile** – High development velocity, but S1 (workflow-blocked) bugs in the WebSocket gateway and macOS first-run experience are eroding trust. |
| **Hermes Agent** | 50 (high) | 50 (high) | ❌ None (last release aged) | ⚠️ **Cautious** – Extremely high community contribution rate (48 open PRs), but a very low resolution rate (7 issues closed, 2 PRs merged). Maintainer bandwidth is the bottleneck. |
| **NanoBot** | 5 (low) | 19 (high) | ❌ None | ✅ **Healthy** – Strong development velocity with responsive maintainers. A batch of hotfixes was merged within hours of bug reports. |
| **CoPaw** | 8 (moderate) | 8 (moderate) | ❌ None (v1.1.11b1) | ✅ **Stabilizing** – Focused on bug fixes and localization. A cluster of edge-case fix PRs is pending review. |
| **NanoClaw** | 1 (very low) | 15 (high, mostly closed) | ❌ None | ✅ **Stable Integration** – Successfully cleared a large backlog of 14 PRs in one day. Project is in a consolidation phase. |
| **IronClaw** | 2 (low) | 22 (high) | ❌ None (PR #3708 stale for 29 days) | ✅ **High-Velocity Sprint** – Aggressively closing an attachment-handling epic. The Slack re-approval loop regression is the primary risk. |
| **PicoClaw** | 2 (low) | 7 (moderate) | ✅ v0.2.9-nightly.20260614 | ✅ **Steady Polish** – Healthy merge cadence with focus on stability, vision fixes, and localization. |
| **LobsterAI** | 4 (stale) | 5 (stale) | ❌ None | ❌ **Low Activity** – All open items are over 60 days stale. No new activity or maintainer responses. |
| **NullClaw** | 2 (low) | 1 (low) | ❌ None | ⚠️ **Critical Bug Block** – A single critical use-after-free bug in cron jobs is the project's entire focus. A fix PR is awaiting review. |
| **Moltis** | 1 (low) | 1 (low) | ❌ None | ✅ **Targeted Stability** – Focused on a single OAuth regression for MCP servers. Low noise, clear focus. |
| **TinyClaw** | 0 | 0 | N/A | 🔴 **Inactive** – No activity in the last 24 hours. |
| **ZeptoClaw** | 0 | 0 | N/A | 🔴 **Inactive** – No activity in the last 24 hours. |

### 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Ecosystem Scale & Discovery**: OpenClaw’s 500+ issues and PRs in 24 hours dwarf all other projects, reflecting an order-of-magnitude larger user and contributor base. This creates a rich knowledge base and plugin/meme ecosystem that smaller projects struggle to replicate.
- **Channel Breadth**: OpenClaw continues to lead in channel delivery support, with simultaneous improvements to Telegram, WhatsApp, Slack, and Feishu. ZeroClaw and IronClaw are catching up but lack the same breadth.
- **Release Cadence**: Two beta releases in a single day demonstrates a robust CI/CD pipeline. IronClaw (29 days stale PR) and ZeroClaw (no release today) are lagging in this metric.

**Technical Approach Differences:**
- **Monolithic Core, Community Patchwork**: OpenClaw follows a "big core + community plugin" model, which leads to its high issue/PR volume. In contrast, **ZeroClaw** is exploring a dynamic-library plugin system (RFC #7420) to better modularize the codebase, aiming to reduce the core maintenance burden.
- **Risk Profile**: OpenClaw’s aggressive release cycle (two betas/day) prioritizes feature velocity, accepting beta-stage bugs. **NanoClaw** and **IronClaw** take a more conservative approach, batching changes for larger, more stable releases.

**Community Size Comparison:**
OpenClaw’s 500 daily items represent a community that is *10x larger* than its nearest competitor (ZeroClaw at ~50 items). This gives OpenClaw unmatched feedback loops and bug discovery but also means it is the most publicly exposed to reliability critiques.

### 4. Shared Technical Focus Areas

Several high-impact requirements are emerging across projects:

- **Agent-to-Agent Orchestration Reliability**: **OpenClaw** (#44925), **OpenClaw** (#43367), and **NanoClaw** (#2267) all struggle with reliable subagent task routing, error surfacing, and session-lock contention. The community demands "fire-and-forget" that actually works.
- **Memory & Context Management**: **OpenClaw** (#43747), **Hermes Agent** (#10771, #42405), **CoPaw** (#5171), and **OpenClaw** (#7707) all report issues with memory chunking inconsistency, silent compaction failures, and the need for trust tagging. Users want predictable, non-destructive memory management.
- **Silent Failure Eradication**: This is the #1 ecosystem-wide pain point. **OpenClaw** (#44925, #45494), **NullClaw** (#941), **CoPaw** (#5172), and **NanoBot** (#4322) all have bugs where agents silently drop tasks, time out, or crash without notification.
- **Third-Party Platform Compatibility**: Integration stability is a cross-cutting concern. **Moltis** (#1119) struggles with Notion/Linear OAuth, **NanoBot** (#4333) with Anthropic model breakage, and **Hermes Agent** (#45813) with GitHub Copilot. The ecosystem needs a more robust abstraction layer for provider compatibility.
- **Rich (Structured) Messaging**: **Hermes Agent** (#44428), **ZeroClaw** (#7531), and **OpenClaw** (v2026.6.8-beta.1) are all racing to support rich text, cards, and structured formats for Telegram, WhatsApp, and Chinese platforms (QQ, DingTalk, WeChat).

### 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | Hermes Agent | NanoBot |
| :--- | :--- | :--- | :--- | :--- |
| **Primary Focus** | Channel delivery breadth & feature velocity | Plugin architecture & enterprise scale | Community-driven features & rich UI | Performance & developer UX |
| **Target User** | Power users & broad-channel integrators | Enterprise & multi-agent fleets | Desktop-first, all-in-one enthusiasts | Developers & sandbox users |
| **Architecture** | Monolithic core with heavy CI | Plug-in system (contested RFCs) | Electron desktop + TUI | Python with WebUI and CLI TUI |
| **Release Strategy** | Multiple beta releases daily | Batch changes for stable releases | No recent release; may be preparing a major version | No recent release; major features in PRs |
| **Key Risk** | Bug backlog can erode trust | S1 bugs in core gateway | Maintainer bottleneck | Minor env-var sensitivity |
| **Key Strength** | Massive community & channel support | Advanced plugin & delegation concepts | High community *contribution* rate | Very responsive bug-fix cycle |

### 6. Community Momentum & Maturity

**Tier 1: Rapidly Iterating (High Feature Velocity, Moderate Stability)**
- **OpenClaw**: Unmatched activity volume, but the sheer density of P0/P1 bugs suggests a "move fast and break things" phase.
- **ZeroClaw**: High PR velocity with two major plugin RFCs competing for adoption. The v0.8.1 stabilization is critical.
- **Hermes Agent**: Massive community *contribution* activity, but maintainer bandwidth is the gating factor for resolution.

**Tier 2: Stabilizing & Polishing (High Merge Rate, Focused Backlogs)**
- **NanoBot**: Exceptional responsiveness; a textbook example of a project balancing new features (TUI, TTS, WebUI parity) with rapid hotfixes.
- **IronClaw**: Aggressively closing a major epic (attachments). The Slack regression is the main drag on stability.
- **NanoClaw**: Successfully cleared a large backlog. Project is in a healthy consolidation phase.
- **PicoClaw**: Steady and reliable. Focused on cross-platform fixes (TTS, vision routing) and localization.
- **CoPaw**: Strong stabilization phase, though the Windows Tauri performance regression (#5047) is a cloud on the horizon.

**Tier 3: Low Activity / Maintenance Mode**
- **LobsterAI**: All items are stale. The project appears to be in a low-maintenance phase.
- **TinyClaw & ZeptoClaw**: No activity detected. These projects may be dormant.

**Tier 4: Critical-Stalled**
- **NullClaw** & **Moltis**: These are functionally blocked by a single critical bug or PR awaiting review. Their health depends on a single maintainer action.

### 7. Trend Signals

1.  **The "Silent Failure" Crisis is the Industry's Top Gap**: Across OpenClaw, NullClaw, CoPaw, and NanoBot, the strongest user demand is for **transparent error handling**. The era of "the agent just stopped working" is ending; developers need to invest in retry logic, error surfacing, and observability.

2.  **Platform Portability is a Growth Vector**: **RISC-V64** (OpenClaw #54253), **macOS first-run** (ZeroClaw #7527), **Windows Tauri performance** (CoPaw #5047), and **Vietnamese/Zalo** (CoPaw #5168, #5169) signal that the user base is expanding beyond the English-speaking, x86 Linux developer. Localization and platform support are now community-driven requirements.

3.  **The "Plugin/Extension" War is Beginning**: ZeroClaw’s two competing RFCs for plugin systems (#7420 vs #7497) signal a fundamental architectural debate. The outcome will determine whether ZeroClaw becomes a nimble, modular platform or remains a tightly integrated monolith. This is a key decision for the ecosystem.

4.  **Multi-Agent Orchestration Needs a Standard**: The reliability failures in subagent orchestration (#44925 in OpenClaw, #43367 in OpenClaw, #2267 in NanoClaw) are not isolated bugs; they indicate a missing abstraction for session-lock, routing, and error propagation. A **community-driven RFC for cross-agent execution semantics** could be a defining contribution.

5.  **Rich UI is the New Battleground**: With Hermes Agent’s rich chat surface PR (#45895), NanoBot’s TUI (#4329), and IronClaw’s WebChat v2, the race is on to move beyond the CLI. The project that delivers a "best-in-class" web or desktop experience (that is reliable) will capture the next wave of non-developer users.

6.  **Community is Building Missing Features**: The most optimistic signal is that users are not just filing bug reports; they are submitting PRs for major features they want (Hermes Agent’s rich chat UI, NullClaw’s cron fix, CoPaw’s skill tag download). This high contribution rate is a strong indicator of long-term project health, provided maintainers can keep pace with the review queue.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-14

## 1. Today's Overview

NanoBot shows **very high development velocity** with 19 PRs updated in the last 24 hours (5 merged/closed, 14 open) and 5 issues updated (2 open, 3 closed). The project is in a **major feature rollout phase** with multiple concurrent workstreams: a new TUI for the CLI agent, WebUI automation management, settings parity between config.json and the WebUI, and a configurable TTS system. The maintainer team is actively addressing regressions from recent merges, with several hotfix PRs submitted within hours of bug reports. No new releases were cut today.

## 2. Releases

No new releases published today.

---

## 3. Project Progress — Merged/Closed PRs

**5 PRs merged/closed today:**

| PR | Summary | Type |
|---|---|---|
| [#4098](https://github.com/HKUDS/nanobot/pull/4098) (hamb1y) | Fix exec workspace symlink guard and path precedence — blocks symlink escapes, prepends `pathAppend` on Unix | Bug fix |
| [#4314](https://github.com/HKUDS/nanobot/pull/4314) (chengyongru) | Break tool config schema import cycle — moves shared Pydantic base to `nanobot.config_base` | Refactor |
| [#4326](https://github.com/HKUDS/nanobot/pull/4326) (tangtaizong666) | Fix `idleCompact` to summarize full session tail including recent suffix | Bug fix |
| [#4327](https://github.com/HKUDS/nanobot/pull/4327) (chengyongru) | Fix WebUI startup blocking on slow gateway routes — moves slow handlers off event loop | Performance |
| [#4313](https://github.com/HKUDS/nanobot/pull/4313) (La-Volpe) | WebUI / config.json settings parity — new write endpoints for temperature, tool limits, memory etc. | Feature |

**Feature advancements:** The `idleCompact` fix (#4326) directly addresses a critical memory consistency bug. The WebUI performance fix (#4327) eliminates a startup-blocking issue. The config parity PR (#4313) closes a long-standing gap between file-based and WebUI configuration.

---

## 4. Community Hot Topics

### Most Active Discussions

| Issue/PR | Comments | Status |
|---|---|---|
| [#193](https://github.com/HKUDS/nanobot/issues/193) — "Ollama api support?" | 15 comments | CLOSED |
| [#4333](https://github.com/HKUDS/nanobot/issues/4333) — "Anthropic provider sends deprecated `temperature` to opus-4-8" | 0 comments (but has open fix PR) | OPEN |

### Analysis

- **Ollama API support (#193, closed):** Despite being 4 months old with 15 comments, this issue closed without a resolution visible in the data. The user only sees vLLM support and asks about Ollama compatibility — a common demand from the local-model community. The closure without public resolution may frustrate users who want local model flexibility.
- **Anthropic `temperature` regression (#4333):** Filed yesterday, already has a fix PR (#4334). This demonstrates responsive maintainers but also highlights a testing gap — the `omit_temperature` check was hardcoded to a single model name, breaking all newer Anthropic models. The community is relying on users to discover regressions.

**Underlying need:** Users want broad provider compatibility (Ollama, newer Anthropic models) with minimal config friction. The rapid fix cycle for #4333 shows the team prioritizes provider reliability.

---

## 5. Bugs & Stability

### High Severity

1. **NameError: `session_key` is not defined in `context.py`** ([#4322](https://github.com/HKUDS/nanobot/issues/4322)) — Crashes agent at startup after merging `origin/main` into a feature branch. Root cause: a refactor extracted `_build_memory_context` but missed a variable reference. **No fix PR yet.** Critical for anyone on `fix/prompt-caching` branch.

2. **Anthropic `temperature` parameter blocks all requests** ([#4333](https://github.com/HKUDS/nanobot/issues/4333)) — Affects `claude-opus-4-8` and "Fable" models. Every request returns HTTP 400. **Fix PR #4334 submitted** — widens `omit_temperature` to cover opus-4-8 and fable.

### Medium Severity

3. **MCP `streamableHttp` server crash on reconnect** ([#4303](https://github.com/HKUDS/nanobot/pull/4303)) — `RuntimeError: Attempted to exit cancel scope in a different task`. **Fix PR #4334 submitted** — closes tracked generators properly.

4. **Codex image SSE parsing incomplete** ([#4332](https://github.com/HKUDS/nanobot/pull/4332)) — `RemoteProtocolError` on incomplete chunked reads. **Fix PR #4332 submitted** — stops parsing after `response.completed`.

### Low Severity

5. **Env-var template resolution failures** — Three PRs ([#4323](https://github.com/HKUDS/nanobot/pull/4323), [#4324](https://github.com/HKUDS/nanobot/pull/4324), [#4325](https://github.com/HKUDS/nanobot/pull/4325)) fix cases where `${VAR}` templates are not resolved in transcription config, settings read paths, and settings update paths. **All with open fix PRs.**

---

## 6. Feature Requests & Roadmap Signals

### Likely in Next Version

- **CLI Terminal UI** ([#4329](https://github.com/HKUDS/nanobot/pull/4329)) — Adds a full interactive TUI for `nanobot agent` with markdown rendering, slash commands, session management, and multimodal input. The PR description is extensive. This is a **major UX shift** from the Rich-Live loop.
- **WebUI Automation Management** ([#4330](https://github.com/HKUDS/nanobot/pull/4330)) — Complete UI for listing, filtering, running, pausing, and deleting automations. Includes i18n support.
- **Multi-provider TTS** ([#4316](https://github.com/HKUDS/nanobot/pull/4316)) — OpenAI, Groq (Orpheus), and ElevenLabs support with WebUI controls. Includes agent discoverability docs.
- **Subagent model presets** ([#4291](https://github.com/HKUDS/nanobot/pull/4291)) — Subagents can use different models than parent via named presets.
- **WebUI reverse proxy support** ([#4328](https://github.com/HKUDS/nanobot/pull/4328)) — Correctly serves under sub-paths like `/nanobot/`.

### User-Requested

- **Tool filesystem enable/disable toggle** ([#4138](https://github.com/HKUDS/nanobot/pull/4138)) — Parity with `exec` and `web` tool groups. Already has an open PR.

### Predictions

The TUI PR (#4329) is massive and would fundamentally change the primary user interface. Given the project's velocity, this could land in the next minor release (0.x) alongside the automation management view (#4330) and TTS (#4316). The config parity work (#4313) suggests a push toward making the WebUI a full config management tool.

---

## 7. User Feedback Summary

### Pain Points

- **Provider compatibility gaps:** Users report Anthropic model breakage (#4333) and ask about Ollama support (#193). The hardcoded model exclusion pattern is fragile.
- **Configuration inconsistency:** Multiple env-var resolution bugs (#4323, #4324, #4325) indicate credential management is error-prone. Users who set environment variables get silent failures.
- **Startup performance:** The WebUI blocking on slow gateway routes (#4327) has been fixed, but it suggests the startup path has optimization opportunities.
- **Session memory loss:** The `idleCompact` bug (#4264) caused incorrect history summaries, potentially losing user corrections and task completions. The fix (#4326) addresses this.

### Use Cases

- **Conversational troubleshooting:** Users iterate with the model, correcting errors over multiple turns — the `idleCompact` bug directly impacted this workflow.
- **Remote sandbox deployments:** The request for filesystem tool toggling (#4138) indicates users want to delegate all file operations to configured MCP servers, not built-in tools.
- **Multimodal interaction:** The TUI PR (#4329) includes local image attachments and audio transcription, suggesting rich input is desired.
- **Multi-model workflows:** Subagent model presets (#4291) imply users want parent agents orchestrating specialized sub-agents with different capabilities.

### Satisfaction Signals

- The rapid bug-fix cycle (e.g., #4333 → #4334 in <1 day) suggests active maintainer engagement.
- The config parity work (#4313) directly addresses a long-standing user complaint about WebUI limitations.

---

## 8. Backlog Watch

### Items Needing Maintainer Attention

| Item | Issue | Status | Concern |
|---|---|---|---|
| Ollama API support | [#193](https://github.com/HKUDS/nanobot/issues/193) | CLOSED without resolution | 15 comments, 4 months old. Closing without addressing may signal deprioritization of local-model users. |
| `session_key` crash on startup | [#4322](https://github.com/HKUDS/nanobot/issues/4322) | OPEN, 1 comment | No fix PR yet. Blocks users on `fix/prompt-caching` branch. Needs urgent triage. |
| Tool filesystem enable toggle | [#4138](https://github.com/HKUDS/nanobot/pull/4138) | OPEN, 0 comments since June 1 | Has a complete PR but no merge. May be blocked on broader architectural decisions. |

### Watch Items

- The `fix/prompt-caching` branch merge appears to have introduced at least one regression (#4322). If this is a major ongoing refactor, more regressions may surface.
- The 14 open PRs suggest the maintainers may be stretched thin merging simultaneously. Several PRs touch the same code paths (`settings_api.py`, `context.py`), raising merge conflict risk.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-14

## Today's Overview

Hermes Agent is experiencing a period of **exceptionally high community activity**, with 50 issues and 50 pull requests updated in the last 24 hours. Open issues dominate at 43, while only 7 were closed, suggesting a surge of bug reports and feature requests outpacing resolution. The PR pipeline is heavily overloaded—48 of 50 recently updated PRs remain open, with only 2 merged or closed. There are **no new releases**, and the last tagged release appears to be some time ago, which may be contributing to community frustration as users wait for fixes to land in stable form. The project remains highly responsive to community contributions, but maintainer bandwidth appears strained.

## Releases

**None.** No new releases are recorded in the observed period. The lack of stable releases may be contributing to the accumulation of open issues and PRs awaiting review.

## Project Progress

Despite the high volume of open items, several meaningful PRs were submitted today that address core stability and feature gaps:

- **#45916** — `feat(state): honor HERMES_DISABLE_FTS_TRIGRAM to skip the trigram FTS index` — Allows users to disable CJK substring search index to save ~70 MB of storage. Useful for non-CJK deployments.
- **#45915** — `fix(mcp): validate tool timeout config values` — Adds type validation for MCP server timeout config, preventing crashes from malformed config values.
- **#45914** — `feat(skills): add caveman ultra-compressed communication skill` — A novel skill adaptation for ultra-compressed agent output with 6 intensity levels and ~65% average compression.
- **#45905** — `fix(update): prevent desktop app breakage by checking build stamp file` — Prevents the update process from removing desktop build artifacts.
- **#45895** — `feat(dashboard): add rich chat surface` — A major UI enhancement adding a mature, self-hosted chat interface to the Hermes dashboard.
- **#45866** — `feat(desktop): native OS notifications with per-type toggles` — Adds native OS notifications (Electron) with per-notification-type enable/disable toggles.
- **#45859** — `fix: show Codex autoraise notice once per profile` — Persists the Codex gpt-5.5 compression notice marker so it only appears once per profile.
- **#45867** — `feat(provider): add OpenRouter Fusion support` — Adds OpenRouter Fusion as a provider-managed server tool for chat-completions requests.
- **#45872** — `fix(gateway): reduce Discord noise and harden recovery` — Restores gateway noise reduction and safety work from a backup branch, resolving conflicts.
- **#45874** — `fix(config): wire reset_by_platform YAML field into load_gateway_config()` — Fixes a silent config ignoring bug where `reset_by_platform:` in `gateway.yaml` was never read.

**Closed issues today** include: #44927 (duplicate streaming auto-follow request), #44942 (skill-update backup corruption), #45826 (macOS file tool test failures), and #27988 (Codex Azure Foundry incomplete status mapping fix).

## Community Hot Topics

The most active discussions reveal deep user investment in **rich messaging**, **memory management**, and **desktop usability**:

| Issue/PR | Comments | Reactions | Summary |
|----------|----------|-----------|---------|
| [#501 — Feature: Web UI Gateway](https://github.com/NousResearch/hermes-agent/issues/501) | 14 | 🎉 1 | Long-running feature request (since March) for a local web UI. Comments indicate this is the **most wanted missing feature** across the community. The PR #45895 (rich chat surface) may partially address this. |
| [#10771 — Auto Dream memory consolidation](https://github.com/NousResearch/hermes-agent/issues/10771) | 8 | 👍 5 | Request for periodic automatic memory cleanup and deduplication. Users report **"stale relative dates"** and accumulated garbage. 5 upvotes signal strong demand. |
| [#44428 — Telegram Bot API 10.1 Rich Messages](https://github.com/NousResearch/hermes-agent/issues/44428) | 5 | 👍 3 | Community excitement about Telegram's new rich formatting. Duplicate #45864 also exists, indicating high demand for structured outputs. |
| [#42366 — Hermes Desktop no auto-scroll](https://github.com/NousResearch/hermes-agent/issues/42366) | 2 | 👍 3 | Core UX bug: chat doesn't auto-scroll and input prompt disappears during output. 3 upvotes despite low comments. Duplicate #44927 (now closed) had 3 reactions. |
| [#45863 — WhatsApp Cloud calls sidecar](https://github.com/NousResearch/hermes-agent/pull/45863) | undefined | 👍 0 | Ambitious PR adding WhatsApp Cloud Calling sidecar with WebRTC offer/answer handling. |
| [#45895 — Rich chat surface](https://github.com/NousResearch/hermes-agent/pull/45895) | undefined | 👍 0 | Major PR adding a mature chat UI. Author states they "really wanted a proper mature chat-ui" so Hermes becomes "all in one package." |

**Underlying need**: The community clearly wants a **first-class web/desktop UI** to replace CLI-only workflows. Simultaneously, **rich formatting** (Telegram, Feishu, Discord) and **automatic memory maintenance** are top pain points. Users are building these features themselves rather than waiting for core team.

## Bugs & Stability

### Critical/Priority 1 Bugs
- **(CLOSED) #29205** — Anthropic fallback fails after Codex reasoning-only empty turns due to trailing assistant prefill. **Closed** — fix appears to have landed.
- **(CLOSED) #27988** — Codex Responses adapter maps complete final_answer to finish_reason=incomplete on Azure Foundry. **Closed**.

### Priority 2 Bugs (Active)
| Issue | Component | Summary | Fix PR? |
|-------|-----------|---------|---------|
| [#23975](https://github.com/NousResearch/hermes-agent/issues/23975) | agent/gateway | Context compression interrupted by gateway messages → fallback summary marker. Long-standing (since May). | None visible |
| [#44666](https://github.com/NousResearch/hermes-agent/issues/44666) | config | `api_key_env` alias silently ignored in custom provider config → falls through to "no-key-required". | None visible |
| [#31155](https://github.com/NousResearch/hermes-agent/issues/31155) | agent/delegate | `delegation.model` override ignored — subagents always inherit parent model. | None visible |
| [#42405](https://github.com/NousResearch/hermes-agent/issues/42405) | memory | Memory at capacity → `replace` zero-match retry loop → silent hang. | None visible |
| [#43586](https://github.com/NousResearch/hermes-agent/issues/43586) | config | Bare `provider: custom` with `key_env:` sends "no-key-required". Duplicate of #44666 pattern. | None visible |
| [#45860](https://github.com/NousResearch/hermes-agent/issues/45860) | cli | 3 Windows installation bugs: missing hermes.exe after interrupted update, etc. | None visible |
| [#45813](https://github.com/NousResearch/hermes-agent/issues/45813) | provider/copilot | HTTP 400 errors with GitHub Copilot (non ACP). | None visible |
| [#45674](https://github.com/NousResearch/hermes-agent/issues/45674) | cli/mcp | `hermes mcp list` crashes with AttributeError when a server entry is a string. | None visible |
| [#45792](https://github.com/NousResearch/hermes-agent/issues/45792) | config/docker | Hermes inside Docker doesn't understand its environment. | None visible |
| [#45869](https://github.com/NousResearch/hermes-agent/pull/45869) | provider | Fix for `model.base_url` from config being silently dropped. **Fix PR exists** | **#45869** |

### Priority 3 Bugs (Active)
| Issue | Component | Summary |
|-------|-----------|---------|
| [#45493](https://github.com/NousResearch/hermes-agent/issues/45493) | Matrix | Agent's own thread-initial message lost from next-turn context. |
| [#42366](https://github.com/NousResearch/hermes-agent/issues/42366) | Desktop/TUI | No auto-scroll + input prompt disappears during output. |
| [#42228](https://github.com/NousResearch/hermes-agent/issues/42228) | Desktop/TUI | Compressed sessions move into "No workspace" because continuation cwd is null. |
| [#45877](https://github.com/NousResearch/hermes-agent/issues/45877) | cron | Cron review blocks read-only tools (read_file, search_files). |
| [#45913](https://github.com/NousResearch/hermes-agent/issues/45913) | Desktop | Chinese language bug: scroll won't reach bottom + outline click navigation inaccurate. |

### Key Stability Observations
- **Memory subsystem is fragile**: Multiple issues (#19245, #42405, #33907) around session crashes, orphaned JSON files, and infinite retry loops. This is the highest-risk area.
- **Config parsing is inconsistent**: At least 3 bugs (#44666, #43586, #45674) where config fields are silently ignored or crash on malformed input.
- **Desktop app has UX regressions**: Auto-scroll and session workspace navigation bugs suggest the recent desktop code needs attention.

## Feature Requests & Roadmap Signals

### Likely in Next Version
1. **Rich chat/dashboard UI** — PR #45895 (rich chat surface) is a mature, heavily tested community contribution. Given the pent-up demand (#501 has 14 comments since March), the core team may fast-track this.
2. **Telegram Rich Messages** — Two parallel issues (#44428, #45864) and a feature request for `sendRichMessage` tool support (#45854). Telegram API 10.1 launched June 11, and users expect Hermes to support it quickly.
3. **Automatic Memory Consolidation** (#10771) — 5 upvotes, inspired by Claude Code's "Auto Dream." Community is building workarounds; official support would reduce bug reports in the memory subsystem.

### Possible Future Features
- **Native OS notifications** (PR #45866) — Already submitted, likely to merge.
- **OpenRouter Fusion** (PR #45867) — Already submitted.
- **Caveman compressed communication** (PR #45914) — Novel but niche; may be merged as a skill example.
- **WhatsApp Cloud Calling** (PR #45863) — Advanced sidecar integration; may take longer to stabilize.
- **Predefined keyboard inputs for WhatsApp/Telegram** (#45912) — Approval workflows with keyboard shortcuts.

### Strategic Signals
- **No new releases** suggests the team is consolidating for a major version bump.
- **Chinese language users** are increasingly reporting bugs (#45913 in Chinese, #22417 in Chinese), indicating growing international adoption.
- **Community is building missing features** (dashboard UI, caveman skill, WhatsApp calling) rather than waiting — a sign of high engagement but also unmet roadmap gaps.

## User Feedback Summary

### Pain Points (High Frequency)
1. **"No web/desktop UI"** — The single most complained-about gap. Users say "Every major competitor has one" and want Hermes to be "all in one package."
2. **"Memory is broken"** — Orphaned sessions, retry loops, stale dates. Users hitting capacity limits get no response at all (#42405).
3. **"Config is confusing"** — Multiple bugs where documented config fields are silently ignored. Users report "thought I set it up correctly but it falls through."
4. **"Desktop app UX is regressing"** — Auto-scroll broken, session navigation broken on macOS and Windows.
5. **"Windows installation fragile"** — Interrupted updates break the binary; Docker environment not detected.

### Positive Signals
- **High community contribution rate** — 48 open PRs, many from first-time contributors. Users are investing significant time building features.
- **International usage growing** — Issues in Chinese (#45913, #22417), Matrix integration enhancements (#45493), Feishu card support PR (#45907).
- **Feature velocity on PRs** — Rich chat, native notifications, OpenRouter Fusion, WhatsApp calling all submitted in a single day.

## Backlog Watch

### Critical Unanswered Issues
| Issue | Opened | Last Updated | Days Unanswered | Why It Matters |
|-------|--------|-------------|-----------------|----------------|
| [#501](https://github.com/NousResearch/hermes-agent/issues/501) — Web UI Gateway | 2026-03-06 | 2026-06-14 | **100 days** | Most-upvoted feature request. 14 comments. Closed but no official implementation roadmap. |
| [#19245](https://github.com/NousResearch/hermes-agent/issues/19245) — Orphaned session not recovered after crash | 2026-05-03 | 2026-06-13 | **42 days** | Data loss bug. Users lose entire conversations after crashes. |
| [#22417](https://github.com/NousResearch/hermes-agent/issues/22417) — ThinkCheck reasoning engine showcase | 2026-05-09 | 2026-06-14 | **36 days** | Third-party integration showcase; no maintainer response. |
| [#23975](https://github.com/NousResearch/hermes-agent/issues/23975) — Context compression interrupted by gateway messages | 2026-05-11 | 2026-06-13 | **34 days** | Core agent reliability issue. No assignee, no fix PR. |

### PRs Needing Review
| PR | Component | Last Updated | Days Without Merge | Risk |
|----|-----------|-------------|-------------------|------|
| [#45763](https://github.com/NousResearch/hermes-agent/pull/45763) — fix: match custom credential pools via agent.requested_provider | agent/provider | 2026-06-13 | 1 day | Fixing 229 mismatches and 28 503 errors in 7 days — **high impact** |
| [#45863](https://github.com/NousResearch/hermes-agent/pull/45863) — Handle WhatsApp Cloud calls | gateway | 2026-06-13 | 1 day | New feature, likely needs review |
| [#45841](https://github.com/NousResearch/hermes-agent/pull/45841) — fix: flip foreground view to warm session synchronously | desktop | 2026-06-13 | 1 day | Fixes regression in session resumption |

### Red Flags
- **The project appears to have no active maintainer responses** on many high-importance issues. Issues like #23975 (context compression reliability) and #19245 (data loss after crash) have had zero maintainer comments since filing.
- **Duplicate issues are not being consolidated efficiently** — #44428 and #45864 are both Telegram Rich Messages; #44666 and #43586 are both key_env config bugs. The duplicate label is used but not consistently.
- **No release tag for over a month** (allowing for project cadence). Combined with 48 open PRs, this suggests a large release is being prepared, but the lack of communication is causing user frustration visible in issue comments.

---

**Project Health Score: ⚠️ Cautious (High Activity / Low Resolution Rate)**

*Activity is extremely high (50 issues, 50 PRs in 24h), but the resolution rate is low (7 issues closed, 2 PRs merged). The community is building what they want themselves, but core bugs (memory corruption, config parsing, desktop regressions) remain unaddressed. The next release needs to focus on stability and the long-awaited Web UI to maintain momentum.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-14

## 1. Today's Overview
The PicoClaw project shows **moderate activity** today, with 7 PRs updated (5 merged/closed) and 2 issues updated (1 closed) in the last 24 hours. A new nightly build `v0.2.9-nightly.20260614` was released. The merge cadence is healthy, with several bugfixes and one open feature PR advancing. The single open issue (#3012) regarding token consumption under Evolution mode remains under discussion, suggesting users are hitting a real cost/performance trade-off. Overall, the project is in a **steady maintenance and polish phase**, with contributions focused on stability, vision pipeline improvements, and localization support.

## 2. Releases
- **Nightly Build:** `v0.2.9-nightly.20260614.cf67dd38`  
  *Automated build — may be unstable.*  
  **Changelog:** [compare/v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
  *No breaking changes or migration notes provided.*  

## 3. Project Progress
**Merged/Closed PRs today (5):**

| PR | Title | Description |
|----|-------|-------------|
| [#2935](https://github.com/sipeed/picoclaw/pull/2935) | docs(i18n): add Traditional Chinese (zh-TW) locale and READMEs | Full Traditional Chinese README, contributor guide, and frontend i18n locale — expands documentation accessibility. |
| [#3065](https://github.com/sipeed/picoclaw/pull/3065) | fix(seahorse): explicitly ignore Close() errors on PRAGMA/migration failure paths | Cleans up linter warnings in `pkg/seahorse/short_engine.go`. |
| [#3066](https://github.com/sipeed/picoclaw/pull/3066) | fix: explicitly ignore Close() errors on temp file write/sync failure paths | Consistency fixes across normalization, WeCom media, and filesystem tooling. |
| [#3117](https://github.com/sipeed/picoclaw/pull/3117) | fix(agent): route media turns to image models | **Key fix:** Routes `load_image` follow-ups and media turns to configured image model instead of retrying on text-only model — directly resolves hallucination bug #3108. |
| [#3119](https://github.com/sipeed/picoclaw/pull/3119) | fix(tts): support OpenRouter voice overrides and fallback | Adds `extra_body` field for per-model voice/format overrides for OpenAI TTS, plus automatic single-retry fallback when `response_format` fails. |

**Still Open (2):**  
- [#2964](https://github.com/sipeed/picoclaw/pull/2964) — Image input compression  
- [#3118](https://github.com/sipeed/picoclaw/pull/3118) — Remote Pico WebSocket mode to agent

## 4. Community Hot Topics
- **[#3108](https://github.com/sipeed/picoclaw/issues/3108) (CLOSED) — Image description hallucinations with text-only models**  
  *Reported by afjcjsbx, 0 comments, closed today.*  
  The active model (e.g., `deepseek/deepseek-v4-flash`) lacks vision support, yet PicoClaw loads the image and produces unrelated answers. **Underlying need:** robust model capability detection and graceful fallback to vision-capable models.  
  *Resolved by PR [#3117](https://github.com/sipeed/picoclaw/pull/3117).*

- **[#3012](https://github.com/sipeed/picoclaw/issues/3012) (OPEN) — Continuous token consumption when evolution is enabled**  
  *Reported by xpader, 3 comments, 0 👍, updated 13h ago.*  
  User reports tokens being consumed every minute with Evolution Mode in Draft, Code Path Trigger set. **Underlying need:** better transparency/control over periodic evolution checks, or an option to disable auto-re-evaluation. Expect further discussion as this is the only open bug with community engagement.

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **High** | [#3108](https://github.com/sipeed/picoclaw/issues/3108) — Image hallucination when active model lacks vision | **CLOSED (fixed)** | Fix merged in PR #3117 — user-facing output corruption. |
| **Medium** | [#3012](https://github.com/sipeed/picoclaw/issues/3012) — Continuous token drain with Evolution enabled | **OPEN** | No fix PR yet. Could indicate a misconfiguration or missing rate-limit. |
| **Low** | [#3065](https://github.com/sipeed/picoclaw/pull/3065) / [#3066](https://github.com/sipeed/picoclaw/pull/3066) — Linter warnings on unhandled `Close()` errors | **CLOSED (fixed)** | Code quality, no user-facing impact. |

## 6. Feature Requests & Roadmap Signals
- **[#2964](https://github.com/sipeed/picoclaw/pull/2964) — Image input compression (OPEN)**  
  Adds configurable multi-level compression before building vision payloads. Currently only `max_media_size` is enforced. This addresses user pain around over-sized image uploads and potential cost savings. **Likely to merge soon** given active dev interest.

- **[#3118](https://github.com/sipeed/picoclaw/pull/3118) — Remote Pico WebSocket mode (OPEN)**  
  Adds `picoclaw agent --remote ws://...` capability. Enables remote agent operation — a **major UX expansion** for distributed/deployed PicoClaw instances. High roadmap significance.

- **[#3119](https://github.com/sipeed/picoclaw/pull/3119) — OpenRouter TTS overrides (MERGED)**  
  Already merged. Points to growing OpenRouter ecosystem support.

**Prediction for next stable release:** Image compression (`#2964`) and remote WebSocket mode (`#3118`) are strong candidates for `v0.3.0` or next feature release.

## 7. User Feedback Summary
- **Pain point:** Token consumption in Evolution Mode is frustrating (`#3012`). User wants predictable cost behavior.
- **Pain point:** Vision hallucination (`#3108`) was a clear reliability issue — now patched.
- **Positive signal:** Two code-quality PRs from community contributor `chengzhichao-xydt` show active quality control culture.
- **Positive signal:** `maxmilian` contributed Traditional Chinese localization, indicating growing non-English user base.
- **No major user complaints** about the nightly build or general stability observed today.

## 8. Backlog Watch
- **No high-priority backlog items** are currently languishing.  
- **[#2964](https://github.com/sipeed/picoclaw/pull/2964) (OPEN since 2026-05-28, 17 days)** is the oldest open feature PR. Maintainers may want to review and merge soon to avoid stall.  
- **[#3012](https://github.com/sipeed/picoclaw/issues/3012) (OPEN since 2026-06-05, 9 days)** has 3 comments but no maintainer assignment or fix PR. If token drain is reproducible, it warrants swift triage.

---
*Generated from GitHub data for 2026-06-14 23:59 UTC.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-14

## Today's Overview
Project activity is **high**, driven primarily by a wave of long-standing PRs being merged or closed (14 of 15 PRs updated in the last 24 hours). The single new issue was a user-submitted deletion request posted to the wrong repository, indicating no new bugs or feature requests were filed today. The lone open PR (#2732) is a critical security/hardening effort that remains under review. No new releases were cut, suggesting the project is consolidating a large batch of merged changes ahead of a potential upcoming release. Overall, the project appears to be in a **stable integration phase** with strong contributor throughput.

## Releases
No new releases were published today.

## Project Progress
Fourteen pull requests were closed or merged in the last 24 hours, representing a significant backlog of features and fixes that landed today:

### New Features & Enhancements
- **#2754** — `onExchangeComplete` provider hook and slash-command interruption support for agent-runner
- **#2747** — SDK 2.2.1 bump with credential-stub mounts and machine-checkable pins (OneCLI integration)
- **#2746** — Agent-surfaces capability seam: host-side registry for provider capability declarations
- **#2745** — Opt-in persistent memory scaffold for providers (configurable retention via `TTL`)
- **#2203** — Signal reaction support (inbound + outbound), mirroring chat-sdk-bridge patterns
- **#2072** — Ollama multimodal support: `images` field for base64-encoded attachments from inbox paths
- **#2071** — Signal now routes all non-audio attachments through the inbox path (PDFs, docs, archives, images)
- **#2084** — Daily project backup system with local/S3 backends, full and per-agent restore CLI
- **#2070** — `extractAttachmentFiles()` now accepts host-path attachments (not just base64)
- **#2040** — Signal outbound attachments now supported via signal-cli's JSON-RPC

### Bug Fixes
- **#2670** — Self-healing fix for poisoned-resume crash loops in agent-runner (fixes #2669)
- **#2267** — Agent-to-agent replies now correctly route back to the originating session, not always the newest
- **#2277** — Mid-query routing context refresh on follow-up messages (fixed frozen routing on cron-then-chat sequences)
- **#2692** — Poll-loop now retries transient 5xx API errors and notifies on exhaustion

## Community Hot Topics
The single most active item today is the open PR #2732, which has no comments recorded but represents the only remaining open item. No issues or PRs attracted significant discussion.

- **#2732 [OPEN]** — Harden host + agent-runner from health audit findings  
  *Author: caburi00* — Security-hardening PR based on a multi-agent adversarial health audit. Addresses container lifecycle vulnerabilities (bind-mount realpath fixes for Docker Desktop, crash-on-spawn circuit breakers, max container enforcement, daemon-level kill fallback).  
  👉 [nanocoai/nanoclaw PR #2732](https://github.com/nanocoai/nanoclaw/pull/2732)

## Bugs & Stability
**No new bugs were reported today** (issue #2755 was a deletion request for cross-posted content). However, several stability fixes landed from previous reports:

| Severity | Bug | Fix PR | Status |
|----------|-----|--------|--------|
| **Critical** | Poisoned-resume crash loop on corrupt transcript | #2670 | Merged |
| **High** | Agent-to-agent replies routing to wrong session | #2267 | Merged |
| **High** | Transient 5xx API errors causing silent failures | #2692 | Merged |
| **Medium** | Frozen routing context on mid-query follow-ups | #2277 | Merged |

The **critical** fix (#2670) addresses a crash-loop scenario where a corrupt `thinking`/`redacted_thinking` block caused infinite restarts. The existing `isSessionInvalid` recovery never triggered because the error surfaced as a result event, not a thrown exception. This has now been merged and is available in the codebase.

## Feature Requests & Roadmap Signals
No new feature requests were filed today. However, the merged PRs reveal clear roadmap directions:

### Likely in Next Release (v2.x)
- **Persistent memory scaffold** (#2745) — Providers can opt into a memory storage system with configurable TTL. This is a foundational capability for long-running agents.
- **Agent-surfaces capability seam** (#2746) — A host-side registry letting providers declare their capabilities. This enables more intelligent routing and provider discovery.
- **SDK 2.2.1 integration** (#2747) — OneCLI credential-stub mounts and machine-checkable pins suggest improved security around credential management.
- **onExchangeComplete hook** (#2754) — Enables providers to react to exchange completion, opening the door for analytics, logging, or post-processing pipelines.

### Longer-Term Signals
The dense batch of Signal-related PRs (#2040, #2071, #2203) suggests Signal integration is maturing rapidly, with full multimodal support and bidirectional file/reaction capabilities now landeding. The backup system (#2084) indicates production-readiness concerns are being addressed.

## User Feedback Summary
No direct user feedback was captured today. The sole issue (#2755) was a user who accidentally posted to the wrong repository, which is a neutral signal. The silence on user-reported issues may indicate either:
- The community is actively testing the recent merged changes but has not yet filed feedback.
- The project is in a consolidation phase where maintainers are pushing through backlogs before broader community engagement.

## Backlog Watch
**No long-unanswered issues or PRs** currently require maintainer attention. The project shows strong maintainer responsiveness, with 14 items successfully closed today. The lone open PR (#2732) was updated today and is actively being worked. The project's backlog appears well-managed and current.

**Notable**: PR #2732 is the highest-priority open item — it represents an adversarial security audit fix. Given that 14 other PRs were processed today, maintainers likely have bandwidth to review and merge this item shortly, making it the one to watch for the next digest cycle.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 14, 2026.

---

## NullClaw Project Digest — 2026-06-14

### 1. Today's Overview
Project activity remains moderate, with two issues and one pull request updated in the last 24 hours. No new releases were published today. The maintainer community is actively discussing a critical bug regarding agent-type cron jobs failing silently, and a fix PR has already been submitted by the community. While feature requests continue to accumulate, the primary focus of recent engagement is on stability and core messaging reliability.

### 2. Releases
**None.** No new releases were published today.

### 3. Project Progress
- **No PRs were merged or closed today.**
- A new fix PR was opened but remains in review status (see Bugs & Stability).

### 4. Community Hot Topics
- **#941 [OPEN] Agent-type cron jobs don't spawn a subprocess — Telegram delivery never happens** (7 comments)
  - **Link:** [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)
  - **Analysis:** This is the most active thread. The reporter describes a scenario where scheduled `agent` jobs are marked complete but never actually spawn the agent process, resulting in silent delivery failures. The discussion indicates multiple users experienced this, and the community has identified a root cause (use-after-free on the channel pointer).
- **#954 [OPEN] Fix: one-shot cron jobs silently fail to deliver messages (use-after-free in OutboundMessage.channel)** (undefined comments)
  - **Link:** [PR #954](https://github.com/nullclaw/nullclaw/pull/954)
  - **Analysis:** This PR is directly linked to the issue above and was authored by a community contributor. It specifically addresses the memory safety bug. The PR has no comments yet, suggesting it is awaiting maintainer review.

### 5. Bugs & Stability
- **Critical: Use-after-free in OutboundMessage.channel causes silent delivery failure for one-shot cron jobs**
  - **Impact:** Jobs marked as completed silently fail to deliver messages via any channel (Telegram, Mattermost). No error is surfaced to users.
  - **Fix PR:** #954 (open, awaiting review) — [Link to PR](https://github.com/nullclaw/nullclaw/pull/954)
  - **Related Issue:** #941 — [Link to Issue](https://github.com/nullclaw/nullclaw/issues/941)
  - **Ranking:** **Critical** — Affects all users running one-shot agent cron jobs with delivery channels.
- **No new bugs, crashes, or regressions reported today beyond the above.**

### 6. Feature Requests & Roadmap Signals
- **#914 [OPEN] [enhancement] Create JIRA access tool** (1 comment)
  - **Link:** [Issue #914](https://github.com/nullclaw/nullclaw/issues/914)
  - **Signal:** This is a standalone feature request to integrate JIRA directly into the agent platform, allowing agents to read, create, update, and comment on tickets. While the request is over a month old with minimal discussion, it signals a growing need for project management tooling integration. Likelihood for next version: Low-to-moderate, likely gated behind current stability fixes.

### 7. User Feedback Summary
- **Pain Point:** Silent failures in scheduled agent jobs remain the top concern. Users report frustration that jobs appear to complete but deliver no output, eroding trust in the scheduling system.
- **Use Case:** Scheduled automation delivery to Telegram/Mattermost is a core expected behavior, and the current bug undermines a primary value proposition of the platform.
- **Satisfaction:** Neutral-to-negative regarding scheduling reliability; positive sentiment toward the community contributor who submitted the fix PR.

### 8. Backlog Watch
- **#914 — JIRA access tool feature request** (Created: 2026-05-13)
  - **Link:** [Issue #914](https://github.com/nullclaw/nullclaw/issues/914)
  - **Status:** Unanswered by maintainers; no roadmap commitment or design feedback provided in 32 days.
  - **Risk:** Low urgency today, but if left unattended, community may perceive low interest in enterprise integrations.
- **#941 — Agent-type cron job bug** (Created: 2026-05-31)
  - **Link:** [Issue #941](https://github.com/nullclaw/nullclaw/issues/941)
  - **Status:** Open 14 days without formal maintainer triage. The fix PR (#954) exists but has not been reviewed. This is the highest priority item needing maintainer attention.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for 2026-06-14.

---

## IronClaw Project Digest
**Date:** 2026-06-14

### 1. Today's Overview

The IronClaw project is experiencing a **high-activity sprint**, driven by a significant push to stabilize the Slack integration and finalize the attachment handling feature (epic #4644). In the last 24 hours, 22 pull requests were updated (17 open, 5 merged/closed) and 2 issues were active, indicating a robust development phase. The core team is aggressively closing out dependency tracks for attachments while simultaneously addressing regressions in the "reborn" runtime, particularly around authentication gates. While there are no new releases today, the maturity of several merged PRs suggests a release may be imminent.

### 2. Releases

**None.** No new releases were published in the last 24 hours. The most recent release is tracked in PR #3708, which is still open.

### 3. Project Progress

Five pull requests were successfully merged or closed today, signaling the completion of several key features:

- **Attachment Infrastructure Locked:** The critical **Track 6** (byte storage) was completed with the merge of PR #4668 (`MountView-based attachment landing crate`). This was the foundation for the inbound bridge (#4670) and the core contract (#4655), both also merged. The Team has now finalized the pipeline for ingesting file bytes, storing them, and linking them to transcripts.
- **WebChat Upload Live:** The final piece of the user-facing path, PR #4672, was closed, enabling inline file uploads in the WebChat v2 interface. Users can now attach files directly in the browser.
- **Format Standardization:** PR #4654 was closed, unifying the scattered attachment format lists into a single registry in `ironclaw_common`, which should prevent "CSV uploaded as text" type bugs.

### 4. Community Hot Topics

The most active discussions are occurring within the core team’s PRs regarding Slack reliability and runtime improvements.

- **#4839 - [OPEN] fix: preserve invocation identity across auth-gate re-dispatch** (1 comment)
    - **Link:** `nearai/ironclaw` PR #4839
    - **Analysis:** This is the highest-priority fix addressing a critical Slack regression where Reborn capabilities requiring two-step authorization (e.g., OAuth + approval) forced users through multiple unnecessary approval gates. The underlying need is for **transparent, single-prompt authorization flows**, which is essential for user trust in the agent.

- **#4836 - [OPEN] feat(runtime-context): surface connected channels, delivery state, and run origin** (1 comment)
    - **Link:** `nearai/ironclaw` PR #4836
    - **Analysis:** This work addresses a major model confusion point by providing the LLM with context about *where* a run started and *which* channels (Slack, Gmail) are already connected. The community (and users) are asking for agents that are aware of their own capabilities and environment, reducing "Hallucinated actions" (e.g., the agent saying "I cannot access Slack" while Slack is connected).

### 5. Bugs & Stability

One new, high-severity bug is under active investigation, alongside a persistent nightly failure.

- **CRITICAL: Slack Re-Approval Loop (PR #4839, #4844, #4843)**
    - **Issue:** Multiple bugs were found causing a "re-approval loop" in the Slack channel (#4839). A single user action (e.g., checking Gmail) could generate 4+ consecutive approval requests.
    - **Status:** Core developer **henrypark133** has a dedicated fix chain (PRs #4839, #4843, #4844, #4840) now open to resolve the identity preservation, gate-filtering, and delivery-fanout bugs causing this regression.
    - **Severity:** Critical. This degrades the "reborn" experience to unusable for Slack users.

- **HIGH: Nightly E2E Failure (Issue #4108)**
    - **Link:** `nearai/ironclaw` Issue #4108
    - **Issue:** The scheduled **Nightly E2E** test for the `v2-engine` failed on commit `2a4e017fd2`.
    - **Status:** Open for 18 days. No specific PR has been linked to fix this yet, which suggests the root cause is either non-trivial or the failure is considered an intermittent infrastructure issue.
    - **Severity:** High. A stale nightly failure blocks CI confidence for all developers.

- **MEDIUM: Run-borking Failures (PR #4841)**
    - **Issue:** Unhandled failures (e.g., `HostUnavailable`) in the reborn runtime cause opaque "run-borked" errors with no recovery path.
    - **Status:** PR #4841 is open to convert these to explainable, retryable errors.
    - **Severity:** Medium. A quality-of-life issue for power users.

### 6. Feature Requests & Roadmap Signals

The current activity strongly signals the features likely to land in the next minor version (targeting v0.30):

- **Rich Media Handling (Attachment Epic #4644):** The "WebChat v2 SPA" UX (#4738) and extracted text from documents (#4676) are the final two open PRs in this epic. Once merged, IronClaw agents will be able to **see and read files** (PDFs, images via text extraction) uploaded by users. This is the headline feature for the next release.
- **Routine API (PR #4264):** The `POST /api/routines` endpoint from contributor **wcc945** remains open. This external API gateway endpoint would allow external systems to create routines, moving IronClaw towards a more service-oriented architecture.
- **Runtime Transparency:** PR #4777 (Slack state persistence) and #4836 (runtime context) suggest the team is focused on making the model’s "state of the world" more visible to the user, reducing confusion.

### 7. User Feedback Summary

While explicit user comments are sparse in this data, the activity reveals clear pain points from QA testing:

- **Pain Point: Slack "Re-Approval Loop"** is the most significant negative signal. Users on Slack (QA) are experiencing a frustrating, multi-step approval process for single actions. The volume of fixes (4 PRs) dedicated to this indicates high dissatisfaction.
- **Pain Point: "Cannot use Slack" hallucination.** Users report the model saying a product is unavailable even when it is connected. PR #4780 and #4777 directly address this by adding "outbound target discovery" guidance to the model's prompt.
- **Positive Signal: Attachment Upload.** The closure of PR #4672 (WebChat upload) implies that internal testing of file attachments has passed, which is likely a high-satisfaction feature for end-users.

### 8. Backlog Watch

The following important items require maintainer attention:

- **Issue #4108 - Nightly E2E Failure (18 days stale).**
    - **Link:** `nearai/ironclaw` Issue #4108
    - **Watch Reason:** A persistent CI failure that has not been resolved or triaged for over two weeks. It is a risk to release quality and should be investigated or acknowledged.

- **PR #4264 - Routine Create Endpoint (14 days stale).**
    - **Link:** `nearai/ironclaw` PR #4264
    - **Watch Reason:** This is the last remaining open PR from a *new contributor*. It adds a valuable API endpoint but has no recent activity from the author or maintainers. Risk of being abandoned. The maintainers should review to encourage the contribution.

- **PR #3708 - Release PR (29 days stale).**
    - **Link:** `nearai/ironclaw` PR #3708
    - **Watch Reason:** This release PR from `ironclaw-ci` has been open for nearly a month. While the team might be waiting for the current attachment/Sprint epics to land, this open PR implies the last automated release attempt hit a breaking change that wasn't ready to ship. It should be updated or closed.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **June 14, 2026**.

---

## LobsterAI Project Digest – 2026-06-14

### 1. Today's Overview
The project shows **low activity** over the last 24 hours, with **4 open issues** and **5 pull requests** all updated, though none were created today. All items are marked as `stale` (last updated over two months ago), indicating a potential lull in active development or maintainer bandwidth. **No new releases** were published. The community has reported several unresolved bugs regarding skill management and UI/UX for agents, while two significant PRs (artifacts preview pipeline and skill import validation) remain open for over two months awaiting merge.

### 2. Releases
**None.** No new releases were published on this date.

### 3. Project Progress
Two PRs were **closed** (merged) today, both focused on fixing UI/UX issues:
- **#1466** – *fix(mcp): modal close button unreachable when content grows tall*  
  by @linlihua. Resolved a scrolling issue in the MCP server form modal where cancel/submit buttons became inaccessible with many environment variables.
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1466)
- **#1467** – *fix(shortcuts): display Cmd (⌘) instead of Ctrl on macOS*  
  by @linlihua. Fixed keyboard shortcut labels to respect platform conventions (macOS vs Windows/Linux).
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1467)

Three other PRs remain open: skill badge UI rework (#1440), extensible preview pipeline (#1441), and skill import validation (#1445).

### 4. Community Hot Topics
The most discussed items (by comments) are:

- **#1443** – *[stale] 有计划支持新版本的openclaw吗？*  
  by @Juzisuan965 (2 comments). User reports breaking changes after upgrading to OpenClaw v2026.3.24 causing runtime errors. No maintainer response yet.
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1443)

- **#1437** – *[stale] 创建定时任务时，计划选择不重复，清空日历，点击【创建任务】按钮没反应*  
  by @xuzx-code (1 comment). A silent UI failure: no error shown when creating a non-repeating scheduled task.
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1437)

**Underlying need:** Users are encountering real functional gaps (OpenClaw compatibility, task creation, skill state management) without timely maintainer feedback, suggesting a need for more active community support.

### 5. Bugs & Stability
All four open issues are **bug reports**, ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | #1443 | OpenClaw v2026.3.24 breaking change causes startup failure | No |
| **High** | #1439 | Disabled skills still callable in conversation | No |
| **Medium** | #1442 | Agent skills not displayed after conversation, only after re-switching | No |
| **Low** | #1437 | Silent failure when creating non-repeating scheduled task | No |

**#1439** is particularly concerning as it suggests a **data integrity / state management bug**—disabling a skill should immediately prevent its invocation.

All bugs are over two months old with no assigned maintainer or linked fix PRs.

### 6. Feature Requests & Roadmap Signals
Two notable open PRs indicate ongoing feature work:

- **#1441** – *feat(artifacts): add extensible preview pipeline for HTML, React and Mermaid*  
  by @febugcoder. A rebased version of a previously conflicted PR adding a modular preview system for Cowork sessions. Likely to merge once reviewed.
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1441)

- **#1440** – *feat(cowork): 将已选技能标签移至输入框内顶部展示*  
  by @gongzhi-netease. UI improvement moving active skill badges from crowded toolbar to input area top. Indicates focus on **skill management UX**.
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1440)

**Prediction:** The next release will likely include: (1) the preview pipeline for artifacts, (2) skill badge UI improvements, and (3) skill import duplication prevention (#1445).

### 7. User Feedback Summary
**Pain points reported:**
- **OpenClaw incompatibility** – Users upgrading to latest OpenClaw releases hit breaking changes with no migration guide or notice.
- **Skill state inconsistency** – Skills that are disabled still function in dialogue (#1439); Agent skill visibility breaks after conversation (#1442).
- **Silent UI failures** – Creating scheduled tasks fails without error messages (#1437).
- **Import quality** – ZIP imports produce random directory names, and duplicate skills are silently created (#1445).

**Satisfaction indicators:** The two merged macOS/UI fixes (#1466, #1467) show responsive maintainer attention to **platform-specific UX details**, which users appreciate.

### 8. Backlog Watch
The following items are **critical or stale** with no recent maintainer activity:

- **#1443** – *OpenClaw support* (created Apr 3, 0 responses from maintainers)  
  *Impact:* Project may become incompatible with latest OpenClaw, blocking upgrades.
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1443)

- **#1445** – *Skill import validation* (created Apr 3, open PR, no merge)  
  *Impact:* Duplicate skills degrade prompt quality and model routing.
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1445)

- **#1441** – *Artifacts preview pipeline* (created Apr 3, open PR, awaiting review)  
  *Impact:* Significant feature enhancement stalled for two months.
  [View PR](https://github.com/netease-youdao/LobsterAI/pull/1441)

- **#1439** – *Disabled skills still callable* (created Apr 3, no assignee, no fix)  
  *Impact:* Users cannot reliably control Agent behavior.
  [View Issue](https://github.com/netease-youdao/LobsterAI/issues/1439)

**Recommendation:** Assign maintainers to #1443 and #1439 as top priority; merge #1445 and #1441 to clear the feature backlog.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-14

## Today's Overview
Activity on the Moltis repository remains low but focused, with only 1 issue and 1 PR updated in the last 24 hours. The single issue is a reported bug in the MCP OAuth flow, and the single PR is a direct fix for that bug — indicating the maintainer or contributor is actively addressing a user-reported regression. No new releases or merges occurred today. Overall, the project appears stable with a targeted response to a specific integration problem.

## Releases
No new releases were published today. The latest available version remains unchanged.

## Project Progress
No pull requests were merged or closed today. The only PR (#1120) remains open and is awaiting review or final testing. It proposes a fix for the OAuth `invalid_target` error affecting Notion and Linear MCP servers.

## Community Hot Topics
The most active conversation today revolves around a single bug report and its corresponding fix:

- **[Issue #1119 – [Bug]: MCP OAuth fails with `invalid_target` for servers using `resource_metadata` in WWW-Authenticate](https://github.com/moltis-org/moltis/issues/1119)**  
  Reported by xzavrel, this issue documents a failure when adding remote MCP servers (Notion, Linear) that include the `resource_metadata` parameter in the `WWW-Authenticate` header during OAuth. The flow opens a browser but returns an `invalid_target` JSON error. The issue has 1 comment and no reactions but is the primary focal point today.

- **[PR #1120 – fix(mcp): use direct fetch for resource_metadata URL from WWW-Authenticate](https://github.com/moltis-org/moltis/pull/1120)**  
  Authored by the same reporter, this PR provides a fix. The root cause is identified as `discover_and_register()` incorrectly passing the `resource_metadata` URL to `fetch_resource_metadata()`. The PR is currently open and untriaged by maintainers.

**Underlying need**: Users integrating popular third-party MCP servers (Notion, Linear) that follow a specific OAuth extension pattern are blocked from completing authorization. The community is actively self-fixing.

## Bugs & Stability
One bug was reported today, ranked as **moderate severity** (blocks a specific integration path but does not crash the entire system):

- **Bug**: MCP OAuth fails with `invalid_target` when the server returns a `resource_metadata` parameter in the `WWW-Authenticate` header.  
  **Affected servers**: Notion, Linear.  
  **Fix available?**: Yes, PR #1120 exists and is open.  
  **Workaround**: None documented yet.

No crashes, regressions, or security issues were reported.

## Feature Requests & Roadmap Signals
No feature requests were submitted today. The only community signal is the implicit request for better compatibility with OAuth extensions used by popular MCP servers. This fix (PR #1120) is likely to be merged in the next patch version if it passes review.

## User Feedback Summary
Today's single user interaction (via issue #1119) reveals a clear pain point: users attempting to connect Moltis to third-party MCP services (Notion, Linear) encounter an authentication failure that is not user-facing in diagnostic error labels. The user who reported the bug also contributed a fix, suggesting moderate technical sophistication but frustration with the current broken integration path. No positive feedback or praise was recorded.

## Backlog Watch
No long-unanswered important issues or PRs were identified in today's data. The project appears to have a manageable backlog with current active items receiving timely attention. No items older than 48 hours are pending maintainer response.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-14

## 1. Today's Overview

CoPaw shows moderate activity over the last 24 hours, with 8 issues and 8 PRs updated, but no new releases. One bug was closed (#5172 — a chat freeze issue), while seven open issues remain active. PR activity is dominated by a single contributor (ly-wang19) who submitted 7 fix PRs targeting edge-case crashes, but all remain open under review. The project appears to be in a **stabilization phase**: no new features were merged today, and the backlog of open review PRs (6) suggests maintainer bandwidth may be constrained. Community enthusiasm is visible in localization and platform integration requests (Vietnamese language, Zalo Bot), but the most urgent signals come from reported blocking bugs.

## 2. Releases

**No new releases** in the last 24 hours. The latest available version remains `v1.1.11b1` (as referenced in bug reports). No migration notes or changelogs to report.

## 3. Project Progress

Two PRs were merged/closed today:

- **[PR #2498 — Closed] fix(agents): use console language when creating agent and fallback unsupported langs**  
  *Author: Alneys* — Fixes a long-standing issue where newly created agents always defaulted to English regardless of the user's UI language. The fix reads `localStorage` language during creation and adds server-side fallback for unsupported languages. This is a significant UX improvement for international users.

- **[PR #4969 — Closed] feat(skill): Add skill tag batch download**  
  *Author: Leirunlin* — Implements tag filtering for skill batch download to workspace. Resolves issue #2961. This is the only feature-level advancement in the digest period.

No other PRs progressed from open to merged. Six PRs remain open, all from contributor ly-wang19, covering a range of edge-case fixes (see Bugs section).

## 4. Community Hot Topics

- **[Issue #5156 — OPEN] [enhancement] Feature request: support kimi-for-coding / add uv whitelist**  
  *4 comments, 0 reactions*  
  User wjt0321 requests that Kimi (from Moonshot AI) be added to the allowed provider list. The core pain point: users who subscribe to Kimi's "coding" tier cannot use their existing subscription with CoPaw, forcing them to either pay for a separate API key or remain locked out. This taps into a broader community desire for **multi-model flexibility and BYO-subscription support**.

- **[Issue #5172 — CLOSED] [bug] Chat freezes after idle period, requires manual stop**  
  *1 comment, closed*  
  This bug received fast attention and was closed, likely acknowledged if not fully resolved. The user reports a severe issue: after a period of inactivity, the chat endlessly waits for a response; pressing "stop" reveals `Error: Task has been cancelled!`. For QQ/WeChat integrations this is a showstopper.

- **[Issue #5169 — OPEN] [enhancement] Add Vietnamese (vi) interface language**  
  *2 comments*  
  User biencuong proposes adding Vietnamese as the seventh interface language, following the same pattern as Indonesian (#4219) and Brazilian Portuguese. This signals growing interest from the Vietnamese developer community.

- **[Issue #5168 — OPEN] Feature request: official Zalo Bot channel**  
  *1 comment*  
  Zalo is Vietnam's dominant messaging platform. Community member lamnguyen3119 requests first-class integration, mirroring the existing Telegram/WhatsApp/Discord channels. This could open CoPaw to a large SEA user base.

## 5. Bugs & Stability

| Severity | Issue | Summary | Fix PR exists? |
|----------|-------|---------|----------------|
| **Critical** | #5172 *(closed)* | Chat freezes after idle; session never recovers without manual stop. Reported on QQ/WeChat channels where manual intervention is impossible. | Now closed, presumed acknowledged. |
| **High** | #5171 | Context compression can zero out entire context if the agent's persona file exceeds the token threshold, causing complete information loss and task interruption. | No open fix PR. |
| **High** | #5174 | Cron/heartbeat agents cannot produce knowledge files (no `write_file` or `spawn_subagent`). Heartbeat agent is a "should-do" only — may not execute knowledge extraction at all. | No open fix PR. |
| **Medium** | #5047 | Windows Tauri desktop client takes 10+ minutes to start vs 1-2 minutes in previous Python build, often hangs on launch. User reports on Windows 11 25H2, CPU i7-11800H, 32GB RAM. | No fix PR directly linked, but perf-related. |
| **Medium-Low** | #5035 *(PR)* | `LlamaCppBackend.get_version()` uses hardcoded 4-digit slice for build number; will break when build exceeds 9999. | ✅ PR #5035 open, under review. |
| **Low** | #5037 *(PR)* | Empty `Exec=` line in Linux `.desktop` files causes IndexError during browser detection. | ✅ PR #5037 open, under review. |
| **Low** | #5038 *(PR)* | `LightContextManager.pre_reply()` crashes on empty message list. | ✅ PR #5038 open, under review. |
| **Low** | #5040 *(PR)* | Single malformed job in `jobs.json` causes entire cron load to fail. | ✅ PR #5040 open, under review. |
| **Low** | #5041 *(PR)* | Backup fails entirely if a single file in agent workspace is unreadable (e.g., permission errors on Windows). | ✅ PR #5041 open, under review. |

All six open PRs from ly-wang19 address edge-case crashes that are likely rare but painful when triggered. The cluster suggests a **targeted code audit** of robustness boundaries. The critical #5171 (context compression data loss) and #5174 (cron limitations) have no fix PRs yet and should be prioritized.

## 6. Feature Requests & Roadmap Signals

- **kimi-for-coding / uv whitelist (#5156)** — High-demand feature for users with existing Kimi subscriptions. Likely to be picked up if the project aims to boost model provider coverage. Could land in next minor release.
- **Vietnamese language support (#5169)** — Low implementation complexity (i18n file addition). Following precedent of #4219 (Indonesian) and Brazil Portuguese, this has high community goodwill ROI.
- **Zalo Bot channel (#5168)** — Medium complexity; requires a new integration module similar to Telegram/Discord. Strategic value for SEA market expansion.
- **Skill tag batch download (#4969, merged today)** — Already implemented; will appear in next release.

The shift of PR #2498 (agent creation language fix) from March to June closure suggests maintainers work through a **queue of non-critical improvements** alongside bug fixes. Next release likely to include: language/creation fixes, skill tag filtering, and possibly one of the pending `ly-wang19` fix PRs.

## 7. User Feedback Summary

- **Pain point: Performance regression** — Users are deeply frustrated by the Tauri desktop transition. Issue #5047 describes a 10x startup slowdown ("10+ minutes" vs "1-2 minutes"). This is a regression that could drive users back to Python builds or away from the desktop client entirely.
- **Pain point: Chat reliability** — Issue #5172 (now closed) reflects a severe UX failure: chat sessions that silently hang after idle. For power users with long-running agents or channel integrations (QQ/WeChat), this is a deal-breaker. The user's tone is angry ("这么严重问题竟然一直存在" — "such a serious problem has existed all along").
- **Pain point: Context compression fragility** — Issue #5171 reveals a design flaw: compression that doesn't account for agent persona files, leading to total context loss. The user likely lost ongoing tasks.
- **Satisfaction signal: Internationalization progress** — Requests for Vietnamese and Zalo integration signal growing trust in the project's multilingual roadmap. Users cite precedent (Indonesian, Brazilian Portuguese) as evidence the team cares about non-English audiences.
- **Use case: Cron/heartbeat automation** — Issue #5174 suggests advanced users are trying to build scheduled knowledge extraction pipelines, hitting undocumented limitations. This indicates the project is being used beyond simple chat.

## 8. Backlog Watch

| Item | Age | Type | Concern |
|------|-----|------|---------|
| **#5047 – Windows Tauri slow startup** | Opened 2026-06-09 (5 days) | Bug | No fix PR; high user impact. Unaddressed, this could erode desktop user base. |
| **#5171 – Context compression data loss** | Opened 2026-06-13 (1 day) | Bug | High severity; no fix PR yet. New issue, but should be prioritized. |
| **#5174 – Cron/heartbeat limitations** | Opened 2026-06-13 (1 day) | Bug | Medium severity; may be by-design but documentation gap. |
| **#5156 – kimi-for-coding support** | Opened 2026-06-12 (2 days) | Feature | No maintainer response yet on feasibility. |
| **#5168 – Zalo Bot channel** | Opened 2026-06-13 (1 day) | Feature | No maintainer response. |
| **ly-wang19 PRs (#5035, #5037, #5038, #5040, #5041, #5170)** | Opened 2026-06-09 to 2026-06-13 | Fix | All 6 PRs are "Under Review" but none have been merged in 5 days. This cluster of low-risk, high-coverage bug fixes should ideally be merged rapidly to clear the review queue and reduce project risk. |

**Key concern:** The six `ly-wang19` PRs are collectively on hold. They fix real, if rare, crashes. Their continued open status may reflect either maintainer bandwidth or pre-merge requirements (CI checks, second reviewer). A batch merge would improve project stability metrics immediately.

---

*Generated from CoPaw GitHub data for 2026-06-14. Data source: agentscope-ai/CoPaw on GitHub.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-14

## Today's Overview
ZeroClaw is in a period of **high-intensity development** with 42 issues and 50 PRs updated in the last 24 hours. The project continues to stabilize around its v0.8.x release line, with significant focus on **gateway reliability**, **plugin system architecture**, and **user experience polish**. The community is actively contributing fixes and features, with 17 issues closed and 10 PRs merged/closed today. Notably, the project is wrestling with several **S1 (workflow-blocked) bugs** in the WebSocket gateway and Web UI dashboard, suggesting growing pains from recent architectural changes. No new releases were cut today, but the v0.8.1 integration tracker (#6970) remains active.

## Releases
**None** — No new releases were published on 2026-06-14. The latest available version remains **v0.8.0-beta-1** (referenced in issue #6876).

## Project Progress
**Merged/Closed PRs today (10 total):**
- **#7398** (merged) — `feat(cron): add pause/resume for scheduled tasks` — Adds `enabled` field to `cron_add`/`cron_update` endpoints and a `PATCH /api/cron/:id` route, allowing users to toggle scheduled jobs without deletion/recreation ([PR #7398](https://github.com/zeroclaw-labs/zeroclaw/pull/7398)).
- **#7415** (closed) — RFC for unifying the three agent turn engines (`run_tool_call_loop` + `turn_streamed` + `Agent::turn`) was **executed as a single consolidation PR** per maintainer direction ([Issue #7415](https://github.com/zeroclaw-labs/zeroclaw/issues/7415)).
- **#7378** (closed) — Fixed macOS Cmd-C being misinterpreted as the quit chord in zerocode TUI ([Issue #7378](https://github.com/zeroclaw-labs/zeroclaw/issues/7378)).
- **#7377** (closed) — Fixed dark themes inheriting unreadable terminal foreground text ([Issue #7377](https://github.com/zeroclaw-labs/zeroclaw/issues/7377)).
- **#6723** (closed) — Fixed native OpenAI provider hardcoding 120s timeout while ignoring `timeout_secs` config ([Issue #6723](https://github.com/zeroclaw-labs/zeroclaw/issues/6723)).
- **#6876** (closed) — Clarified that `risk_profile.allowed_tools` does not restrict MCP tools by design (documentation gap resolved) ([Issue #6876](https://github.com/zeroclaw-labs/zeroclaw/issues/6876)).
- **#5570**, **#5470**, **#6223**, **#7507** were also closed, addressing SQLite memory backend performance, runtime safety issues, WhatsApp web_fetch compatibility, and a quickstart infinite redraw loop respectively.

## Community Hot Topics
- **Dream Mode — Periodic Memory Consolidation (#5849)** — The top-commented open issue (18 comments) proposes a lightweight background process that consolidates memories and updates long-term knowledge structures during idle periods. This represents strong community interest in **autonomous agent behavior** and **memory architecture enhancement** ([Issue #5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)).
- **Multi-database session backends (#6893)** — A high-risk XL-sized PR adding Postgres, Oracle, MySQL, and Db2 session persistence backends for multi-agent fleets. This signals enterprise/scale-out use cases gaining traction ([PR #6893](https://github.com/zeroclaw-labs/zeroclaw/pull/6893)).
- **Per-turn output routing via send_via (#7361)** — An XL-sized enhancement PR addressing voice delivery fixes and double-send bugs across 10+ channel types (Slack, Telegram, Discord, Matrix, etc.). Indicates **multi-channel reliability** is a key community concern ([PR #7361](https://github.com/zeroclaw-labs/zeroclaw/pull/7361)).
- **RFC: Native Dynamic-Library Plugin System (#7420)** and **RFC: OCI-Compliant Container Registries for Plugins (#7497)** — Two competing plugin architecture proposals generating architectural discussion, suggesting the community is actively shaping ZeroClaw's extensibility model ([Issue #7420](https://github.com/zeroclaw-labs/zeroclaw/issues/7420), [Issue #7497](https://github.com/zeroclaw-labs/zeroclaw/issues/7497)).

## Bugs & Stability
**S1 — Workflow Blocked:**
- **#7563 (NEW)** — `canvas-store` regression in WS chat/ACP sessions breaks `/canvas` after PR #6986. The Web UI canvas page remains empty after WebSocket chat uses the canvas tool ([Issue #7563](https://github.com/zeroclaw-labs/zeroclaw/issues/7563)).
- **#7542 (NEW)** — `ask_user` tool fails instantly with "Channel closed before receiving a response" in gateway web dashboard sessions. **Fix PRs exist**: #7584, #7586, #7588 (multiple attempts by xuwei-xy, all open) ([Issue #7542](https://github.com/zeroclaw-labs/zeroclaw/issues/7542)).
- **#7527 (NEW)** — macOS app (v0.8.0, Homebrew install) cannot detect granted permissions, displays empty page, and disappears on restart ([Issue #7527](https://github.com/zeroclaw-labs/zeroclaw/issues/7527)).
- **#7523 (OPEN)** — Web dashboard not available at `http://127.0.0.1:42617/` after `brew install zeroclaw` on macOS; frontend build required ([Issue #7523](https://github.com/zeroclaw-labs/zeroclaw/issues/7523)).

**S2 — Degraded Behavior:**
- **#7521 (NEW)** — `file_read` tool cannot decode non-UTF-8 text (cp1251/Latin-1/Shift-JIS), falling back to `U+FFFD` replacement characters ([Issue #7521](https://github.com/zeroclaw-labs/zeroclaw/issues/7521)).

**S3 — Minor Issues:**
- **#7509** — Self-test `find_asset_url_picks_correct_gnu_over_android` fails on Windows hosts (zip asset filtering logic) — closed ([Issue #7509](https://github.com/zeroclaw-labs/zeroclaw/issues/7509)).

## Feature Requests & Roadmap Signals
**Likely for v0.8.1 (per tracker #6970):**
- **Llama.cpp model router (#7539)** — Quick-switching of local models for smaller tasks ([Issue #7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)).
- **Multi-session support in gateway web chat UI (#7543)** — Session sidebar with new/switch/rename/delete, allowing independent conversations ([Issue #7543](https://github.com/zeroclaw-labs/zeroclaw/issues/7543)).
- **Streaming card messages for QQ/DingTalk/WeChat/Feishu (#7531)** — Reducing user wait time for rich card messages in Chinese messaging platforms ([Issue #7531](https://github.com/zeroclaw-labs/zeroclaw/issues/7531)).
- **WhatsApp message reactions (#7518)** — Parity with Telegram/Discord/Matrix `ack_reactions` support ([Issue #7518](https://github.com/zeroclaw-labs/zeroclaw/issues/7518)).

**Speculative for v0.9.0+:**
- **Delegation with different risk profiles (#7514)** — Allowing subagents to have separate risk profiles, enabling better security separation of concerns ([Issue #7514](https://github.com/zeroclaw-labs/zeroclaw/issues/7514)).
- **Dream Mode (#5849)** — Periodic memory consolidation could become a flagship autonomous capability if accepted.
- **OCI-Compliant Plugin Registry (#7497)** — If adopted, would fundamentally change how plugins are distributed and discovered.

## User Feedback Summary
**Pain Points:**
- **macOS first-run experience is broken** — Multiple users report that Homebrew-installed ZeroClaw (v0.8.0) fails to display the web dashboard without manual frontend builds, and the desktop app crashes on permission detection (#7527, #7523).
- **WebSocket gateway reliability issues** — The `ask_user` tool is completely broken in web dashboard sessions, blocking any workflow requiring user approval (#7542).
- **Canvas regression** — A recent change (#6986) introduced a regression that breaks canvas visualization in the web UI (#7563).
- **Multi-byte text encoding gaps** — Users with non-UTF-8 file content (Cyrillic, CJK) cannot use `file_read` effectively (#7521).
- **Chinese messaging platform integration** — Users of QQ, DingTalk, WeChat, Feishu experience long waits for card messages; streaming support is requested (#7531).

**Satisfaction Signals:**
- Community members actively contribute PRs (xuwei-xy, Audacity88, JordanTheJet, singlerider) suggesting high engagement.
- The open architecture discussions (plugin systems, turn engine unification) indicate a mature community capable of shaping the project's technical direction.

## Backlog Watch
- **#5849 — Dream Mode (OPEN, 18 comments, p2, accepted, no-stale)** — Last updated 2026-06-13. High community interest but no assigned owner or implementation PR. May require architectural decisions around the memory subsystem first ([Issue #5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)).
- **#6823 — Zerocode ACP Bridge tracker (OPEN, p2, accepted, no-stale)** — Client-side connection layer for the TUI-to-daemon RPC. Last updated 2026-06-13. One of two core trackers (#6825, #6826) for the TUI initiative that have been open since May 21 without visible implementation PRs ([Issue #6823](https://github.com/zeroclaw-labs/zeroclaw/issues/6823)).
- **#6289 — Prompt-triggered install suggestions (OPEN, p2, accepted, no-stale)** — Last updated 2026-06-13. User-facing feature that would significantly improve plugin discoverability, but blocked on plugin system decisions ([Issue #6289](https://github.com/zeroclaw-labs/zeroclaw/issues/6289)).
- **#5797 — TLS CA cert support for custom providers (OPEN, 4 years old)** — A long-standing PR adding `tls_ca_cert_path` for corporate/private PKI. Still open with `needs-author-action` label, suggesting author hasn't responded to review feedback ([PR #5797](https://github.com/zeroclaw-labs/zeroclaw/pull/5797)).
- **#6684 — Skill manage patch error distinction (OPEN, needs-author-action)** — PR stacked on #6667 with unresolved author action required; risks staleness ([PR #6684](https://github.com/zeroclaw-labs/zeroclaw/pull/6684)).
- **#6667 — Background review fork + skill_manage tool (OPEN, XL, needs-author-action)** — Large integration PR for skill improvement that has been open since May 14. Risks accumulating merge conflicts ([PR #6667](https://github.com/zeroclaw-labs/zeroclaw/pull/6667)).

---

*Generated from GitHub data on 2026-06-14. All links refer to `zeroclaw-labs/zeroclaw` repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*