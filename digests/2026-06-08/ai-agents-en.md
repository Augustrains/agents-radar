# OpenClaw Ecosystem Digest 2026-06-08

> Issues: 292 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-08 02:15 UTC

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

# OpenClaw Project Digest — 2026-06-08

## Today's Overview

OpenClaw is in **high-intensity development** with 292 issues and 500 pull requests updated in the last 24 hours — the highest velocity observed in recent months. 178 issues remain open/active while 114 were closed; 340 PRs are open with 160 merged or closed. No new releases were published today, suggesting the team is consolidating fixes ahead of a planned release. The project shows strong community engagement, with several high-priority security and regression bugs receiving maintainer attention. A notable cluster of issues involves **message loss across multiple channels** (Telegram, Slack, Feishu) and **session-state contamination** from cron triggers, indicating these are the team's current focus areas.

## Releases

None today. The latest published release remains the previous version (no new versions in the data).

## Project Progress

**160 PRs merged/closed today** — a very active day for fixes and improvements. Key developments:

- **Automerge fixes landed**: Multiple small, targeted fixes were merged via the automerge pipeline:
  - [#91235](https://github.com/openclaw/openclaw/pull/91235) — Fix Codex preserving native subagent completion results (fixes #91120)
  - [#90897](https://github.com/openclaw/openclaw/pull/90897) — Fix heartbeat exec completion showing generic fallback text instead of actual output
  - [#91230](https://github.com/openclaw/openclaw/pull/91230) — Fix cron preserving isolated agent turn payload message
  - [#91124](https://github.com/openclaw/openclaw/pull/91124) — Fix MCP server processes accumulating by not refreshing `lastUsedAt` on lease release
  - [#91231](https://github.com/openclaw/openclaw/pull/91231) — Fix Anthropic provider dropping `reasoning_content` replay signatures that caused compatibility issues
  - [#91241](https://github.com/openclaw/openclaw/pull/91241) — Fix outbound delivery retries being incorrectly consumed for budget-deferred deliveries

- **Memory system improvements**: 
  - [#91274](https://github.com/openclaw/openclaw/pull/91274) — Refactored memory core to drop redundant agent-id scoping from qmd collection names (in progress)
  - [#91299](https://github.com/openclaw/openclaw/pull/91299) — Deep Sleep dreaming phase now writes summary into DREAMS.md after sweeps

- **Channel-specific fixes**: 
  - [#90858](https://github.com/openclaw/openclaw/pull/90858) — iMessage split-send coalescing fix (closed)
  - [#88796](https://github.com/openclaw/openclaw/pull/88796) — Discord: resolve guildId from session channel for search actions (open)
  - [#89659](https://github.com/openclaw/openclaw/pull/89659) — Feishu: retry on send rate-limit errors (open)

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#25592](https://github.com/openclaw/openclaw/issues/25592)** — *Text between tool calls leaks to messaging channels* (27 comments, 1👍)
   - **Analysis**: A long-standing diamond-rated security issue. The core problem is that internal agent processing text (error handling, acknowledgments) gets routed to messaging channels like Slack and iMessage as visible messages. This is both a UX and security concern — internal processing output should never leak to end users. The issue has been stale for 3+ months with multiple claw-sweeper labels indicating it needs maintainer review, product decision, and security review before any fix PR can proceed.

2. **[#88838](https://github.com/openclaw/openclaw/issues/88838)** — *Track core session/transcript SQLite migration via accessor seam* (18 comments, 1👍)
   - **Analysis**: A maintainer-tagged issue about a large architectural migration of session/transcript state from memory to SQLite. The approach is to use a branch-by-abstraction seam to avoid a single high-risk rewrite. This signals a major internal refactoring effort that will impact session state handling and potentially enable better persistence and recovery.

3. **[#88312](https://github.com/openclaw/openclaw/issues/88312)** — *Codex app-server turn-completion stall returns* (14 comments, 3👍)
   - **Analysis**: A regression with high community interest (3 thumbs-up). The Codex app-server (ChatGPT Plus sub) experiences a stall where multi-tool agent turns fail with *"Codex stopped before confirming the turn was complete"*. This is a regression of a previously fixed issue (#84076, fixed by #85107), indicating the fix was either incomplete or re-introduced. Users on 2026.5.27+ are affected.

### Most Active PRs (by comment count — all show undefined but have high activity)

Notable large/challenging PRs under active review:

- **[#90101](https://github.com/openclaw/openclaw/pull/90101)** — *Feat: add runtime self context config and tool* (XL size, showcase feature)
- **[#78441](https://github.com/openclaw/openclaw/pull/78441)** — *Feat: forward toolsAllow from sessions_spawn* (M size, showcase feature, 3 merge risks flagged)
- **[#89045](https://github.com/openclaw/openclaw/pull/89045)** — *Fix: recover terminal session status on visible inbound turns* (L size, fixes group chat sessions stuck in `failed` status)
- **[#90994](https://github.com/openclaw/openclaw/pull/90994)** — *Fix: restore native PreToolUse relay delivery* (L size, Codex relay enforcement)

## Bugs & Stability

### Critical (P1) Regressions

| Issue | Channel/Area | Summary | Fix PR Status |
|-------|-------------|---------|---------------|
| **[#88312](https://github.com/openclaw/openclaw/issues/88312)** | Codex | Turn-completion stall regression | Needs maintainer review |
| **[#91212](https://github.com/openclaw/openclaw/issues/91212)** | Feishu | Delivery recovery starts before channel transport ready, causing silent message loss | Needs live repro |
| **[#90639](https://github.com/openclaw/openclaw/issues/90639)** | Slack | `compaction.mode: "safeguard"` allows sessions to grow to 200K+ tokens, causing wedge | Needs live repro |
| **[#91283](https://github.com/openclaw/openclaw/issues/91283)** | Security | `minSecurity` inverted — `security="full"` clamped to `"allowlist"` by agent config | **Fix PR [#91288](https://github.com/openclaw/openclaw/pull/91288) open** |
| **[#90298](https://github.com/openclaw/openclaw/issues/90991)** | Cron | Cron scheduled trigger contaminates global runtime state causing system-wide overload | Needs live repro |

### New Bugs Today (2026-06-08)

- **[#91283](https://github.com/openclaw/openclaw/issues/91283)** — **Security inversion bug**: `minSecurity` has rank order backwards, treating `full` as most restrictive instead of least restrictive. This means a session-level `security="full"` override gets clamped to `"allowlist"` by agent config, **reducing security instead of increasing it**. Fix PR [#91288](https://github.com/openclaw/openclaw/pull/91288) submitted by bladin.
- **[#90428](https://github.com/openclaw/openclaw/issues/90428)** — Open: `exec` tool triggers gateway SIGTERM restart on WSL2 with Node 24. Regression reported.

### Stale High-Severity Bugs

Several diamond-rated bugs remain open and stale (no update in 3+ months):
- **[#25592](https://github.com/openclaw/openclaw/issues/25592)** — Text leaks to channels (security, message-loss)
- **[#29387](https://github.com/openclaw/openclaw/issues/29387)** — Bootstrap files in agentDir silently ignored
- **[#31583](https://github.com/openclaw/openclaw/issues/31583)** — `exec` tool doesn't inherit skill environment variables
- **[#40001](https://github.com/openclaw/openclaw/issues/40001)** — Write tool lacks append mode, cron sessions destroy shared files

## Feature Requests & Roadmap Signals

### High Probability for Next Release

1. **Gateway-lite mode** ([#86881](https://github.com/openclaw/openclaw/issues/86881)) — Lightweight deployment mode without AI harness. Community demand for deterministic deployments. 7 comments, trending.

2. **Topic-session families** ([#90916](https://github.com/openclaw/openclaw/issues/90916)) — One assistant with multiple named context lanes. Strong use case for multi-context chat-native assistants. 7 comments, security-reviewed pending.

3. **Bounded append semantics for pre-compaction memory flush** ([#90354](https://github.com/openclaw/openclaw/issues/90354)) — Guardrails for append size and post-write validation. Addresses data-loss concerns in memory workflows.

4. **Runtime self-context** ([PR #90101](https://github.com/openclaw/openclaw/pull/90101)) — The large showcase PR adding self-context config and tool. This appears to be a foundational piece for cost-awareness and offload features.

### Emerging Signals

- **Slack tool-level progress** ([#33413](https://github.com/openclaw/openclaw/issues/33413)) — 3 thumbs-up, stale but in queue for fix shape. Community wants real-time tool status in Slack threads.
- **Model picker improvements** ([PR #90328](https://github.com/openclaw/openclaw/pull/90328)) — Exposing agent runtime metadata in model picker signals a UI focus for future releases.

## User Feedback Summary

### Pain Points

- **Message loss across channels**: Multiple users report intermediate text between tool calls being lost (Telegram [#87326](https://github.com/openclaw/openclaw/issues/87326), Feishu delivery failures [#91212](https://github.com/openclaw/openclaw/issues/91212), Slack wedge [#90639](https://github.com/openclaw/openclaw/issues/90639))
- **Stale session state**: Users frustrated that session resets from non-TUI clients don't reflect in TUI ([#38966](https://github.com/openclaw/openclaw/issues/38966)), and that gateway restarts lose in-flight approvals ([#64664](https://github.com/openclaw/openclaw/issues/64664))
- **Memory system fragility**: Reports of Dreaming generating irrelevant summaries ([#70005](https://github.com/openclaw/openclaw/issues/70005)), and memory search being aborted as timeout despite model completion ([#74586](https://github.com/openclaw/openclaw/issues/74586))
- **Configuration confusion**: Users reporting that `openclaw status` falsely reports memory as unavailable ([#57256](https://github.com/openclaw/openclaw/issues/57256)), and that `openclaw doctor` gives false positives on Gateway auth ([#65201](https://github.com/openclaw/openclaw/issues/65201))

### Satisfaction Indicators

- **High engagement**: 500 PRs updated in 24 hours indicates active community contribution and responsive maintainers
- **Quick fix turnaround**: Several P1 bugs from yesterday (e.g., [#91283](https://github.com/openclaw/openclaw/issues/91283)) already have fix PRs submitted today
- **Automerge pipeline**: A well-functioning automerge system is processing small fixes efficiently, reducing maintainer overhead

### Use Cases Represented

- **Enterprise deployments**: Multi-channel gateway setups with Slack, Mattermost, Discord, Telegram, Feishu
- **Personal assistants**: Users relying on cron scheduling, memory, and subagent spawning
- **Developer tools**: Codex integration, CLI subagents, ACP bridge sessions
- **Global users**: Issues in Chinese (Feishu) and English, indicating diverse geographic adoption

## Backlog Watch

### Stale Critical Issues Needing Maintainer Attention

These issues have been open for 3+ months and carry high-severity labels, but have no active fix PR:

| Issue | Age | Severity | Summary | Blockers |
|-------|-----|----------|---------|----------|
| [#25592](https://github.com/openclaw/openclaw/issues/25592) | 104 days | 🦞 Diamond | Text between tool calls leaks to channels | Needs maintainer review, product decision, security review |
| [#29387](https://github.com/openclaw/openclaw/issues/29387) | 100 days | 🦞 Diamond | Bootstrap files in agentDir silently ignored | Needs maintainer review, product decision, security review |
| [#22358](https://github.com/openclaw/openclaw/issues/22358) | 108 days | 🦞 Diamond | Post-subagent completion extension hook | Needs maintainer review, product decision, security review |
| [#31583](https://github.com/openclaw/openclaw/issues/31583) | 98 days | 🦞 Diamond | `exec` tool doesn't inherit skill environment variables | Needs maintainer review, product decision, security review |
| [#40001](https://github.com/openclaw/openclaw/issues/40001) | 92 days | 🦞 Diamond | Write tool lacks append mode, cron sessions destroy files | Needs product decision |
| [#29736](https://github.com/openclaw/openclaw/issues/29736) | 100 days | 🦞 Diamond | Exec approvals path ignores active state root | Needs product decision, security review |
| [#37634](https://github.com/openclaw/openclaw/issues/37634) | 94 days | 🦞 Diamond | Sandbox with `workspaceAccess: none` mounts workspace read-only | Needs maintainer review, product decision, security review |

### Recent Issues Needing Live Reproduction

These P1 issues cannot proceed until reproduction is verified:

- [#91212](https://github.com/openclaw/openclaw/issues/91212) — Feishu delivery recovery failure after restart
- [#90639](https://github.com/openclaw/openclaw/issues/90639) — Slack compaction wedge (safeguard mode)
- [#90991](https://github.com/openclaw/openclaw/issues/90991) — Cron trigger causing system-wide overload
- [#87136](https://github.com/openclaw/openclaw/issues/87136) — Compaction absolute token thresholds break with model switching

---

**Project Health Assessment**: The project is in a **healthy but high-pressure state**. The volume of PRs and issues indicates strong community momentum and active development, but the large backlog of stale diamond-rated bugs (7 issues open 3+ months) suggests systemic issues in security and session-state handling that need architectural attention. The maintainer team appears to be prioritizing P1 regressions over feature work, which is appropriate for stability. The lack of a new release in this data cycle may indicate the team is batching fixes for a planned release.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-06-08

---

## 1. Ecosystem Overview

The open-source personal AI assistant ecosystem is experiencing a **development intensity unprecedented in recent months**, with over 580 combined PRs and 480 issues updated across tracked projects in a single day. The landscape is bifurcating between **reference architecture platforms** (OpenClaw, ZeroClaw, IronClaw) driving core infrastructure innovation and **lightweight specialization forks** (PicoClaw, NanoClaw, NanoBot) optimizing for specific deployment scenarios. A clear pattern emerges: every major project is simultaneously investing in multi-channel delivery reliability, memory system robustness, and sandbox security—indicating these have become baseline expectations rather than differentiators. The ecosystem is maturing from "can it run?" to "can it run **reliably in production**?" with message loss, session state contamination, and silent failures emerging as the top cross-project pain points.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | New Release? | Health Score | Primary Phase |
|---------|---------------------|-------------------|--------------|--------------|---------------|
| **OpenClaw** | 292 | 500 | ❌ | **Very High** | High-intensity development + consolidation |
| **ZeroClaw** | 50 | 50 | ❌ (v0.8.0 prep) | **High** | Feature expansion + release prep |
| **IronClaw** | 50 | 38 | ❌ | **High** | Architecture overhaul ("Reborn") |
| **Hermes Agent** | 50 | 50 | ❌ | **High** | Rapid bug fixing + code review |
| **PicoClaw** | 21 | 21 | ✅ (nightly) | **High** | Defensive coding + quality sweep |
| **CoPaw** | 13 | 5 | ❌ | **Moderate** | Maintenance + channel stabilization |
| **NanoBot** | 8 | 18 | ❌ | **Moderate-High** | Steady feature + bug fix cycle |
| **NanoClaw** | 2 | 9 | ❌ | **Moderate** | Targeted enhancements |
| **Moltis** | 1 | 3 | ❌ | **Moderate** | Stabilization + review |
| **LobsterAI** | 15 | 0 | ❌ | **Low** | Stale bug processing, no merges |
| **NullClaw** | 0 | 0 | ❌ | **Inactive** | No activity |
| **TinyClaw** | 0 | 0 | ❌ | **Inactive** | No activity |
| **ZeptoClaw** | 0 | 0 | ❌ | **Inactive** | No activity |

**Notes on scoring:** Health Score considers merge velocity, issue closure rate, maintainer responsiveness, and security bug resolution cadence. OpenClaw's 500 PRs in 24h is an outlier even for this ecosystem.

---

## 3. OpenClaw's Position

### Advantages vs. Peers

| Dimension | OpenClaw | Next Best Competitor | Gap |
|-----------|----------|---------------------|-----|
| **Development velocity** | 500 PRs/24h | 50 PRs/24h (ZeroClaw, Hermes) | **10x higher** |
| **Issue volume/engagement** | 292 issues | 50 issues (ZeroClaw, IronClaw) | **5.8x higher** |
| **Security fix turnaround** | <24h (PR #91288) | 2-7 days typical | **Faster by order of magnitude** |
| **Channel integrations** | 10+ (Slack, TG, Feishu, iMessage, Discord, Mattermost, etc.) | 5-8 typical | **Broadest channel coverage** |
| **Reference status** | Core reference project | None | **Unique** — ecosystem depends on it |

### Technical Approach Differences

- **Multi-agent architecture:** OpenClaw's subagent spawning and Codex integration goes deeper than any competitor. Hermes Agent has Kanban workers but lacks the sophisticated isolation model.
- **Memory system maturity:** OpenClaw's Deep Sleep dreaming (DREAMS.md), Qdrant-backed memory refactoring (#91274), and compaction safeguards represent 6-12 months ahead of peers. NanoBot's context-pressure gating (#4238) is the closest comparable feature.
- **Security posture:** Only OpenClaw has diamond-rated security issues tracked with formal product-decision and security-review blockers — both a strength (rigor) and weakness (stale high-severity bugs).

### Community Size Comparison

| Metric | OpenClaw | ZeroClaw | Hermes Agent | IronClaw |
|--------|----------|----------|--------------|----------|
| **Daily PR contributors** | ~20-30 | ~5-10 | ~5-10 | ~10-15 |
| **Maintainer response time** | Hours (P1 bugs) | Days | Days | Hours (Reborn focus) |
| **Automation maturity** | Automerge pipeline working | Self-merge by authors | Manual review | Hermetic local gate |
| **International community** | Strong (Chinese Feishu + English) | Strong (Chinese + English) | English-dominant | English-dominant |

**Key insight:** OpenClaw's scale is **not just bigger but structurally different** — its automerge pipeline enables high-velocity small fixes that other projects handle manually, creating a compounding advantage in bug fix throughput.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging **independently across multiple projects**, confirming they are ecosystem-wide needs:

| Focus Area | Affected Projects | Specific Manifestations |
|------------|-------------------|------------------------|
| **Message loss prevention** | OpenClaw, NanoBot, PicoClaw, CoPaw | Telegram/Slack/Feishu delivery failures, orphan tool results dropping messages |
| **Session state management** | OpenClaw, LobsterAI, ZeroClaw | Cron contamination, skill state inconsistency, CLI-TUI desync |
| **Memory system reliability** | OpenClaw, NanoBot, NanoClaw, CoPaw | Dream bloat, compaction loops, irrelevant summaries, context pressure |
| **Sandbox/execution security** | OpenClaw, PicoClaw, ZeroClaw, Hermes Agent | Bubblewrap failures, `$HOME` reset, namespace restrictions, SIGTERM crashes |
| **Channel-specific fixes** | All active projects | iMessage, Feishu, Matrix, Telegram, Slack, Discord, WhatsApp — each project patching 1-2 channels |
| **Configuration complexity** | OpenClaw, ZeroClaw, IronClaw, NanoClaw | Config-as-code demand, migration pain, env-config conflicts |
| **Token/tool result cost optimization** | OpenClaw, LobsterAI, ZeroClaw, Moltis | Skill compilation, context-pressure gating, capped tool results |

**Strongest convergence signal:** **Message loss** is the #1 cross-project pain point, appearing in 4 of the top 5 most active projects. The ecosystem is collectively realizing that channel delivery reliability is a hard prerequisite for production adoption.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | ZeroClaw | IronClaw | Hermes Agent | PicoClaw | NanoBot |
|-----------|----------|----------|----------|--------------|----------|---------|
| **Primary users** | Enterprise, power users | Docker/container users | Security-conscious operators | Desktop/CLI developers | Mobile/ARM, hobbyists | WebUI, custom providers |
| **Core language** | Go | TypeScript/Node | Rust | Python | Go | TypeScript/Node |
| **Deployment model** | Multi-instance gateway | Docker-first | Production composition root | Desktop app + CLI | Lightweight binary | Web app (Next.js) |
| **Architecture focus** | Reference implementation | Plugin/extensions | Security isolation | UX polish | Minimal dependencies | Provider flexibility |
| **Channel breadth** | **Widest** (10+) | Broad (8+) | Moderate (Slack, WebChat) | Narrow (CLI, Desktop) | Moderate (TG, Matrix, QQ) | Moderate (WhatsApp, Feishu) |
| **Unique strength** | Scale + automation | Provider ecosystem | Security hardening | Desktop UI | ARM/mobile support | WebUI-first |
| **Unique weakness** | Stale diamond bugs | S0 data loss bug (#4627) | Slow configuration migration | Terminal escape bugs | Release cadence | CI/infra fragility |

**Strategic differentiation insight:** The ecosystem has developed a **natural division of labor**: OpenClaw drives the core reference implementation, ZeroClaw experiments with plugins and provider schema, IronClaw focuses on production-grade security, and the younger projects (PicoClaw, NanoBot) optimize for specific deployment footprints. This is healthy — no project is trying to be everything to everyone.

---

## 6. Community Momentum & Maturity

### Activity Tiers

| Tier | Projects | Characteristic | Trajectory |
|------|----------|---------------|------------|
| **Hyper-growth** | OpenClaw | 500 PRs/day, aggressive automerge, scaling challenges | **Accelerating** — may need architectural debt management |
| **High-growth** | ZeroClaw, IronClaw, Hermes Agent | 30-50 PRs/day, feature-heavy, release preparation | **Stable rapid iteration** |
| **Steady-state** | PicoClaw, NanoBot, NanoClaw, CoPaw, Moltis | 1-20 PRs/day, maintenance + targeted features | **Healthy, sustainable** |
| **Stagnant** | LobsterAI | 0 PRs merged, stale bugs accumulating | **Declining** — risk of user migration |
| **Dormant** | NullClaw, TinyClaw, ZeptoClaw | No activity | **At risk of abandonment** |

### Maturity Assessment

- **OpenClaw** is the most mature by any measure but carries **technical debt from rapid growth** — 7 diamond-rated bugs stale >3 months, security inversion bug slipped into production.
- **IronClaw** has the **most disciplined architecture** (Reborn overhaul, security audit layers) but the slowest iteration velocity relative to its ambitions.
- **ZeroClaw** shows the **highest risk profile** with an S0 data-loss bug unfixed for 75 days while continuing to merge new features — a concerning pattern.
- **PicoClaw** executed an **exceptionally clean quality sweep** today (17 issues closed, 12 PRs merged) — best hygiene of any project in this period.

---

## 7. Trend Signals

### Industry Trends Extracted from Cross-Project Feedback

1. **"Silent failure is unacceptable"** — Users across OpenClaw, ZeroClaw, CoPaw, and LobsterAI are demanding visual feedback for ongoing operations (shell execution progress, skill generation, message delivery status). The era of "it works or it doesn't, good luck debugging" is ending.

2. **Channel parity is a prerequisite** — Integration coverage is no longer a differentiator; **reliable channel-specific behavior** is. Users complain when Telegram works but Feishu silently drops messages, or when Slack streaming breaks but CLI is fine. The bar is moving from "supports X channels" to "X channels work identically well."

3. **Cost transparency is becoming critical** — Two separate projects (LobsterAI #2121, ZeroClaw #5146) have users actively questioning token waste. As LLM API costs remain non-trivial, features like skill compilation, context-pressure gating, and token usage dashboards will become table stakes.

4. **Mobile is underserved** — PicoClaw's Termux guide (closed after 4 months), Moltis's missing multiline input (#1107), and Hermes Agent's Portuguese locale request (#40239) all point to growing demand for mobile and non-English-first deployment.

5. **Configuration is a pain point** — Every major project has users complaining about configuration complexity. IronClaw's Config-as-Code epic (#3036), ZeroClaw's Docker feature flags (#3642), and OpenClaw's `minSecurity` inversion (#91283) all stem from configuration systems that grew organically rather than by design.

6. **Security hardening is accelerating** — IronClaw's Reborn security layers, OpenClaw's diamond-labeled bugs receiving formal product/security review processes, and PicoClaw's structured logging over `printf` replacement (#3050) indicate the ecosystem is preparing for enterprise adoption with actual compliance requirements.

### Value for AI Agent Developers

- **Invest in observability first**: The strongest competitive advantage you can build today is **making failures visible and debuggable** — not just fixing them silently.
- **Channel delivery reliability > channel count**: A Slack agent that never drops messages will retain users better than one that supports 8 channels with 80% reliability.
- **Configuration systems need architectural attention**: The `minSecurity` inversion bug (OpenClaw #91283) is a textbook case of configuration complexity creating security vulnerabilities. Every project should audit its config validation before adding more knobs.
- **Sandbox security is no longer optional**: With bubblewrap failures on Ubuntu 24.04 (PicoClaw, NanoBot) and SIGTERM crashes from `exec` tool (OpenClaw #90428), the ecosystem is collectively learning that running untrusted model output requires production-grade isolation.
- **Cost-aware designs will differentiate**: The projects that solve token waste (via context-pressure gating, skill compilation, result capping) before their competitors will win cost-sensitive users — especially as LLM API costs remain volatile.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-08

## 1. Today's Overview
Project activity remains elevated, with **8 issues** and **18 pull requests** updated in the last 24 hours. The open-to-closed ratio is moderate (6 open / 2 closed issues; 14 open / 4 merged/closed PRs), indicating steady throughput. Notably, the bubblewrap sandbox subsystem is receiving concentrated attention with two related bug reports and a fix PR. No new releases were published today, but multiple feature PRs are approaching maturity (version display, ANSI rendering, transcription sharing). The project appears in a healthy maintenance-and-feature cycle with active community contributions.

## 2. Releases
**No new releases today.** The latest stable version remains unchanged. Users relying on the bubblewrap sandbox should monitor issues #4236 and #4237, as fixes are in progress but not yet released.

## 3. Project Progress
**Merged/Closed PRs (4 items):**
- **#4240 — WebUI ANSI rendering** (by Re-bin): Added ANSI SGR parser to render colored output inside code blocks, with clean-text copy support. *Enhances user experience for tool output display.*
- **#4227 — Preserve empty-string reasoning_content** (by michaelxer): Fixes custom provider bug (#4105) where empty `reasoning_content=""` was coerced to `None`, causing field-level issues with DeepSeek/Kimi providers.
- **#2885 — Feishu mention resolution** (by xwind): Fixes bot mention detection and access token initialization for the Feishu channel. Resolves a long-standing community request.
- **#2663 — WhatsApp LID group mentions** (by danielphang): Normalizes JID handling for group mentions and improves swipe-reply detection.

**Features advanced (open but significant):**
- **#4235 — Version display in WebUI** (JiajunBernoulli): Adds version info with cached PyPI update check to Settings > Overview.
- **#4232 — Shared voice input** (Re-bin): Elevates transcription from channel-only to shared capability for WebUI/desktop.
- **#4238 — Context-pressure gating for microcompact** (chengyongru): Refactors compaction to be triggered by actual context pressure rather than fixed tool-result counts.
- **#4190 — Stricter tool-call validation** (chengyongru): Preserves invalid arguments for explicit rejection instead of silent repair.

## 4. Community Hot Topics
- **#4237 / #4236 — Bubblewrap sandbox bugs** (by primit1v0): Two related reports on bwrap failures — `$HOME` not reset and user namespace restrictions on Ubuntu 24.04. Each has **1 comment**. Underlying need: reliable sandbox execution on modern Linux distributions. PR #4239 (open) addresses the HOME issue.
- **#4203 — `find_legal_message_start` message loss** (by huji820): Critical bug where orphan tool results cause all messages to be discarded. **2 comments**; PR #4219 (open) fixes the root cause.
- **#4242 — Dream disabled but history still injected** (by skyline75489): When `dream.enabled=false`, the dream cursor never advances, causing Recent History to bloat the system prompt. **0 comments** — new, unaddressed.
- **#4233 — Version display request** (by viblo): Requests showing version + update check in WebUI. Promptly addressed by PR #4235. Shows responsive maintainer engagement.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix PR |
|----------|-------|-------------|--------|
| **High** | #4236 | bwrap fails on Ubuntu 24.04 due to user namespace restrictions | None yet |
| **High** | #4237 | bwrap $HOME not reset, breaking tool writes | #4239 (open) |
| **High** | #4203 | `find_legal_message_start` drops all messages with orphan tool results | #4219 (open) |
| **Medium** | #4242 | Disabled dream still injects full history into system prompt | None yet |
| **Low** | #4105 | Custom provider drops empty-string reasoning_content (closed) | #4227 (merged) |
| **Low** | #4234 | Empty-response retry duplicates user turns via API | #4234 (open) |
| **Low** | #4230 | Missing httpx timeout on streamableHttp MCP connections | #4230 (open) |

**Overall stability assessment:** Two high-severity sandbox bugs affect Ubuntu 24.04 users specifically. The message-loss bug (#4203) is a general regression risk. Other items are low-severity edge cases.

## 6. Feature Requests & Roadmap Signals

| Request | Issue | Likelihood for Next Release | Rationale |
|---------|-------|----------------------------|-----------|
| WebUI version display + update check | #4233 | **High** | PR #4235 already submitted and tested |
| Shared transcription for WebUI/desktop | #4232 | **High** | PR open, well-scoped, no controversy |
| Subagent model override via spawn tool | #4231 | **Medium** | Clear use case (cheap subagents), but API surface needs design |
| Feishu topic-group bot replies | #2256 | **Low** (closed) | Marked closed, but feature may return if community reopens |

**Roadmap signals:** The project is converging on WebUI polish (version, ANSI, voice input) and sandbox reliability. The `spawn` model override (#4231) signals demand for more flexible subagent orchestration.

## 7. User Feedback Summary
- **Pain points:** WebUI version opacity (#4233), sandbox failures on Ubuntu 24.04 (#4236, #4237), unnecessary history injection with disabled dream (#4242), custom provider reasoning content handling (#4105).
- **Use cases:** Bubblewrap sandbox users (security-conscious deployments), custom-provider users (DeepSeek/Kimi), Feishu/WhatsApp channel users (international teams), WebUI users (version awareness).
- **Satisfaction:** Positive response to ANSI rendering (#4240) and MCP URL safety (#4123). The project's quick turnaround on version display (#4235 within hours of #4233) indicates good maintainer attention.
- **Dissatisfaction:** None explicit, but the lack of version display without `/status` is a repeated minor frustration.

## 8. Backlog Watch
- **#2256 — Feishu topic-group replies** (closed 2026-06-07 after 4 comments, created March 2026): Closed without resolution. If topic-group replying is important to your deployment, consider reopening or commenting.
- **#2885 — Feishu mention fix** (merged today): Was open since April 2026. Long duration suggests Feishu channel needs more maintainer attention.
- **#2663 — WhatsApp LID mentions** (merged today): Also open since March 2026. Similar pattern — community PRs for channel fixes take 2-3 months to land.

**No currently open, unanswered issues older than 30 days require immediate maintainer attention.** The project's response cadence appears healthy for recent reports.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for June 8, 2026.

---

## Hermes Agent Project Digest | 2026-06-08

### 1. Today's Overview
The Hermes Agent project is experiencing a period of very high activity, with 50 issues and 50 pull requests updated in the last 24 hours. While only 4 issues and 1 PR were closed/merged, the vast majority of the activity indicates heavy code review, discussion, and development in progress. The project remains in a rapid cycle of bug fixing and feature development, particularly around the CLI, Desktop app, and gateway integrations. No new releases were published today, suggesting the maintainers are consolidating changes before a potential release batch.

### 2. Releases
**None.** No new releases were published today.

### 3. Project Progress
Only one PR was merged today:
- **[PR #41654] (fix):** Fixed a bug in `terminal_tool.py` where the agent would crash if a worker's current working directory (CWD) had been deleted. The fix ensures the agent falls back to the user's home directory. This resolves a crash scenario for Kanban workers and sessions operating in ephemeral environments.

Several other high-value PRs remain open and are under active development, including foundational improvements to test portability (Termux, host-state isolation) and fixes to the EventBridge MCP server session index polling.

### 4. Community Hot Topics
The most active discussions this week reveal a focus on localization and desktop user experience:

1.  **[#40239] - Portuguese (pt-BR) Language Support (3 comments, 2 👍)**
    - **Analysis:** This is the highest-reacted issue in the last 24 hours. The user notes that Hermes already has a robust `pt.yaml` locale file for the backend, but the feature request is to add it as a UI option in the Desktop app. This signals a strong desire from the Brazilian community for a first-class desktop experience, not just CLI support.

2.  **[#40494] - Loosen Right-Rail Preview Width Caps (3 comments)**
    - **Analysis:** A clear usability pain point. Users working with wide content (code, Mermaid diagrams, terminal output) find the desktop preview pane too restrictive at 38rem. The request to expand to 72rem is a straightforward, high-impact UX improvement that is likely to be adopted quickly.

3.  **[#24114] - Matrix Gateway: 2-Person Room Misclassification (2 comments, 2 👍)**
    - **Analysis:** A long-standing P1 bug that severely impacts users who rely on Matrix gating and threading. The issue describes a critical logic flaw in `_is_dm_room` that can break core gateway features. The high 👍 count and P1 severity label suggest this is a top priority for the maintainers.

### 5. Bugs & Stability
The project has a high volume of bug reports today, with several critical (P1) and high-priority (P2) issues:

- **P1 - Infinite Context Compaction Loop ([#40803]):** A critical agent bug where low `context_length` settings cause the agent to enter an infinite loop of compressing and re-compressing the same data. This renders the agent unusable in constrained environments. *No fix PR exists yet.*
- **P1 - Matrix DM Misclassification ([#24114]):** As noted above, this critical gateway bug is impacting production use cases.
- **P2 - Deps with Known CVEs ([#40176]):** Security audits flag `urllib3`, `python-multipart`, `PyJWT`, and `idna` as having known vulnerabilities. A simple dependency bump is required. *Fix likely requires a PR updating `uv.lock`.*
- **P2 - Escape Sequences Truncating Output ([#40250]):** A user-facing CLI bug where terminal escape codes cause the first few characters of responses to be cut off, degrading the interactive experience.
- **P2 - Orphaned Background Processes ([#40343]):** Background processes (e.g., from `terminal(background=true)`) are not cleaned up on CLI exit, leading to resource leaks and port conflicts.

Several less critical but notable P3 bugs were also filed, including issues with the Firecrawl web provider ignoring Hermes config values ([#40190]) and the session browser failing to accept Korean/CJK input ([#40446]).

### 6. Feature Requests & Roadmap Signals
The community is actively pushing for desktop app and developer workflow improvements:
- **High Likelihood:** **Desktop UI Customization ([#40399], 2 👍).** The request for theming, fonts, and styling has strong support. Given the user base's desire for a polished daily driver, this is a strong candidate for the next major UI iteration.
- **Medium Likelihood:** **File Deletion in Desktop UI ([#40484]).** This is a basic file management feature missing from the desktop tree. It is relatively low-effort and addresses a clear workflow gap.
- **Medium Likelihood:** **Kanban Board Integration ([#41222]).** Users want the Kanban board to be embedded in the desktop app, not run as a separate CLI process. This signals a desire for a fully integrated multi-agent workflow manager.
- **Lower Likelihood:** **Ctrl+Mouse Wheel Zoom ([#40295]).** A standard UX gesture missing from the desktop app. Likely to be considered a quick polish item for a future release.

### 7. User Feedback Summary
- **Pain Points:**
    - **Terminal/CLI Bugs:** Users are reporting issues with terminal escape sequences, orphaned background processes, and the TUI busy indicator getting stuck. This impacts the core interactive experience for CLI users.
    - **Desktop UI Rigidity:** Users find the desktop app's lack of customization (styling, theming, font choice) and limited file management (no delete) to be a barrier to daily use.
    - **Localization Gaps:** Despite strong backend multilingual support, the desktop UI is not keeping up, leaving communities (Portuguese, Russian) asking for parity.
- **Satisfaction:** The active discussion and number of feature requests indicate a highly engaged and invested user base that believes in the project's potential. Users are willing to file detailed, well-articulated issues, which is a strong sign of project health.

### 8. Backlog Watch
The following issues have been open for some time with no maintainer response or fix PR, and warrant attention:
- **[#38816]: fix(skills): treat user-configured taps as 'tap' trust level.** (Opened June 4, 0 PR events since). This is a core security and usability feature for the skills ecosystem, but it remains in limbo. Users who add custom taps are forced to use `--force` for safe skills.
- **[#38697]: fix(browser): enable SSRF guard when terminal runs in container.** (Opened June 4). A critical security fix for users in containerized environments. Its lack of movement is a potential security risk for those users.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-08

## 1. Today's Overview

PicoClaw is in a period of high maintenance activity, with 21 issues and 21 PRs updated in the last 24 hours. The project closed a remarkable 17 issues and 12 PRs, driven by a sustained code quality sweep — particularly around unchecked type assertions, silently swallowed errors, and structured logging. A new nightly build (v0.2.9-nightly.20260608.875cf4a2) has been published, though it carries a stability warning. Despite the high closure rate, four open issues point to unresolved bugs in Telegram, Matrix, and the MCP CLI that merit attention. The volume of defensive-coding patches suggests the maintainers are investing heavily in runtime robustness ahead of a stable release.

## 2. Releases

**New Release: nightly (v0.2.9-nightly.20260608.875cf4a2)**

An automated nightly build tagged `v0.2.9-nightly.20260608.875cf4a2` was published. The release is described as potentially unstable and is not recommended for production use.

- **Full Changelog**: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **No breaking changes or migration notes** are documented for this nightly.
- **Note**: The project has not shipped a stable release recently (users in the community have been requesting one — see Issue #2952 "好久没发新版本了").

## 3. Project Progress

**12 PRs merged/closed today**, reflecting a broad hygiene and feature push:

### Core Runtime & Defensive Coding
- **#3046** — Added `ok` checks for type assertions in agent startup info (merged)
- **#3042** — Handled `os.Getwd()` errors in evolution skills recall and drafts (merged)
- **#3040** — Added `ok` check for singleflight type assertion in model probe (merged)
- **#3034**, **#3035**, **#3033** — Checked `Close()` errors after file I/O in feishu resource downloads, file copies, and media downloads (all merged)
- **#3036** — Fixed default Anthropic model ID to use hyphens (`claude-sonnet-4-6`) instead of dots (merged)

### Features & Integrations
- **#3037** — Added native Kagi web search provider (merged)

### Documentation
- **#2902** — Added Android Termux guide (merged, closes #286)

### Skills System
- **#2936** — Skills now skip loading if their required binaries are missing from PATH (merged, closes #2351)

### Message Bus & Health
- **#2906** — Fixed message bus backpressure handling with bounded waiting, per-stream drop stats, and improved health visibility (merged)

## 4. Community Hot Topics

### Most Active Discussions

1. **Issue #2674** — *Codex OAuth: empty assistant response when ChatGPT backend streams* (8 comments, 4 👍)  
   [View Issue](https://github.com/sipeed/picoclaw/issues/2674)  
   *Status*: **CLOSED**. A long-standing bug (since April) involving empty responses from the ChatGPT Codex backend. The 8 comments and 4 upvotes signal it was a significant pain point for API users. The closure suggests a fix has been applied.

2. **Issue #286** — *Docs: Add guide for running PicoClaw on Android via Termux* (8 comments, 2 👍)  
   [View Issue](https://github.com/sipeed/picoclaw/issues/286)  
   *Status*: **CLOSED** (PR #2902 was merged). A four-month-old documentation request finally resolved. The sustained interest (8 comments) indicates a strong mobile-user community.

3. **Issue #2952** — *Feature: 好久没发新版本了 (Long time no new version)* (4 comments)  
   [View Issue](https://github.com/sipeed/picoclaw/issues/2952)  
   *Status*: **CLOSED** (marked stale). User reported three bugs (exec command actions, QQ channel restart loop, model provider UI) and expressed frustration at the lack of new stable releases. The closure without resolution may disappoint users expecting a stable release timeframe.

### Underlying Needs
- Users are demanding better **error feedback** and **stability** in channel integrations (Matrix, Telegram, Codex)
- The **mobile/Android** deployment path is a growing priority
- There is unspoken demand for **release cadence transparency** and more **intuitive configuration UI**

## 5. Bugs & Stability

### Open Bugs (Ranked by Severity)

| Severity | Issue | Summary | Status |
|----------|-------|---------|--------|
| **High** | [#3049](https://github.com/sipeed/picoclaw/issues/3049) | Telegram channel ignores `message.location` — no log output, no reaction | **OPEN**, no fix PR |
| **High** | [#3044](https://github.com/sipeed/picoclaw/issues/3044) | `allow_from` fails for Matrix user IDs containing colon — messages silently rejected | **OPEN**, fix PR #3045 exists |
| **High** | [#3041](https://github.com/sipeed/picoclaw/issues/3041) | `mcp add` mis-parses global flags into positionals, breaking HTTP/SSE adds and mis-naming stdio servers | **OPEN**, fix PR #3048 exists |
| **Medium** | [#2978](https://github.com/sipeed/picoclaw/issues/2978) | Feature request: add omniroute as provider (open since May 31) | **OPEN**, stale |

### Notable Fixes in Progress
- **PR #3045** (open) — Fixes Matrix `allow_from` colon parsing (addresses #3044)
- **PR #3048** (open) — Fixes `mcp add` flag parsing (addresses #3041)
- **PR #3047** (open) — Restores full JSONL history for session detail endpoint
- **PR #3050** (open) — Replaces `log.Printf`/`fmt.Printf` with structured logger (reliability improvement)
- **PR #3051** (open) — Fixes `%w` vs `%v` for error wrapping in channels and MCP

### Just-Fixed Bugs
- **#3039/#3038** — Duplicate “allow_from fails for Matrix user IDs containing colon” reports (closed as duplicates)
- **#2941** — Default config seeds `claude-sonnet-4.6` with invalid model ID (fixed in #3036)

## 6. Feature Requests & Roadmap Signals

### User-Requested Features (Open)
- **#2978** — Add omniroute as provider (no maintainer response, stale)
- **#3049** — Telegram location message support (just opened, no response yet)

### Predicted Next-Version Candidates
Based on the current PR pipeline and community activity:
1. **Structured logging overhaul** — PR #3050 is a sweeping change touching state package; likely to land in next stable
2. **Kagi web search** — Already merged (#3037), will appear in next release
3. **Android Termux guide** — Merged (#2902), expected in next stable
4. **Skills binary dependency checking** — Merged (#2936), will ship
5. **Message bus backpressure** — Merged (#2906), foundation for better reliability

### Long-Term Signals
The series of closed issues from user **jcafeitosa** (#3024–#3032) describe a structured trading/order-book subsystem (Exchange interface, Binance connectors, lock-free ring buffers, risk manager, ClawHub message types). This appears to be a planned feature track (EXM/RG series) for a future “ClawTrade” CLI. While not yet visible in open PRs, these specifications suggest a significant expansion into trading/backtesting capabilities.

## 7. User Feedback Summary

### Pain Points (Explicit)
1. **Configuration model IDs are error-prone** — #2941: Dots vs hyphens in Anthropic model names cause 404 errors for new users
2. **QQ channel instability** — #2952: Repeated restarts when sending messages after a restart
3. **Empty responses from Codex provider** — #2674: Silent failures with ChatGPT backend, requiring fallback
4. **Documentation gaps for upgrades** — #2834: Users need upgrade tutorials
5. **Skill creator is broken out-of-box** — #652: Missing dependency file prevents `skill-creator` from running

### Use Cases
- **Mobile/rPi deployment** — Running on ARM64 (Raspberry Pi, Android via Termux) is a recurring theme
- **Multi-channel agents** — Telegram, Matrix, QQ, LINE, Feishu all in active use
- **Trading automation** — The ClawTrade issue series signals commercial-grade trading bot interest

### Satisfaction Signals
- High PR merge velocity (12 merged today) indicates responsive maintainers
- The sustained issue-closing rate (17 closed in 24h) suggests the team is actively tackling backlogs

## 8. Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Summary | Priority |
|-------|-----|---------|----------|
| [#2978](https://github.com/sipeed/picoclaw/issues/2978) | 8 days | Add omniroute as provider (no comments from maintainers) | Medium — easy win for provider ecosystem |
| [#2952](https://github.com/sipeed/picoclaw/issues/2952) | 12 days | Multiple bugs reported; closed as stale without resolution (including QQ restart loop, exec command issues) | High — user experiencing regressions |
| [#652](https://github.com/sipeed/picoclaw/issues/652) | 3.5 months | Skill-creator broken out-of-box (missing `scripts/init_skill.py`) | Medium — blocks new skill development |
| [#2834](https://github.com/sipeed/picoclaw/issues/2834) | 1 month | Request for upgrade tutorial (closed stale, no guide produced) | Low — partially addressed by Termux guide |

### Risks
- **Stale-issue closure policy**: #2952 was closed as stale despite containing actionable bug reports. This may frustrate users who expect a resolution.
- **API provider fragmentation**: With Codex, OmniRoute, Kagi, and native Anthropic all in flux, the provider abstraction layer needs clear documentation and testing.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-08

## Today's Overview
NanoClaw shows high development activity today with 9 pull requests updated in the last 24 hours, including 3 closed/merged, alongside 2 open issues. The project is in a healthy maintenance and enhancement phase, with contributions spanning security gating, configuration persistence, documentation improvements, and startup reliability. Notably, the maintainer team is actively reviewing and merging PRs, including a critical upgrade-state enforcement mechanism. Community engagement remains moderate, with both recently filed issues receiving attention from maintainers.

## Releases
No new releases were published today. The latest tracked version remains around v2.0.64 (commit d144721).

## Project Progress
Three pull requests were closed/merged today, indicating forward momentum:

- **#2710** [CLOSED] — **docs(ollama): allow prompt caching by filtering the cache-busting hash** (author: markbala). Adds documentation explaining why Claude-Code-CLI → Ollama is slow out of the box and how to enable prompt caching via dependency filtering. A pure documentation improvement following guidelines.
- **#2707** [CLOSED] — **feat(upgrade): startup tripwire + upgrade marker** (author: gavrielc). Implements a startup check that refuses to launch unless the install reached the current version through a sanctioned path (`/setup`, `/update-nanoclaw`, `/migrate-nanoclaw`). A raw `git pull` now fails loudly with a self-healing message instead of silently breaking. Adds `src/upgrade-state.ts`.
- **#2706** [CLOSED] — **fix(账号轮换): 限制模式并校准切换状态** (author: tier2tech-tian). Fixes account rotation logic: prevents Codex/Gemini modes from entering Anthropic rotation, calibrates DB cursor drift before switching, sends notification immediately on rate-limit rotation success, and adds SIGTERM → SIGKILL fallback in `killGroup`.

## Community Hot Topics
- **#2711** [OPEN, filed today] **create_agent MCP tool is ungated despite "admin-only" comment** (author: jonazri, 0 comments). Reports a security discrepancy: `create_agent` is documented as admin-only but exposed to every container with no role check. Maintainers have not yet responded. This issue has high security implications. [Link](https://github.com/nanocoai/nanoclaw/issues/2711)
- **#2312** [OPEN, filed 2026-05-06] **groups/global/CLAUDE.md is unconditionally deleted** (author: mbernabeu, 2 comments). Describes a persistent dirty working tree issue where `migrateGroupsToClaudeLocal()` removes a committed file on every startup. Maintainers are aware but resolution remains pending. [Link](https://github.com/nanocoai/nanoclaw/issues/2312)
- **#2709** [OPEN, filed today] **feat(container-config): DB-backed env + blocked_hosts for ContainerConfig** (author: markbala, 0 comments). Implements maintainer-requested feature #1867: adds DB-backed JSON columns for environment variables and blocked hosts to `container_configs`. This is a significant infrastructure enhancement. [Link](https://github.com/nanocoai/nanoclaw/pull/2709)

## Bugs & Stability
| Severity | Issue/PR | Description | Fix Exists? |
|----------|----------|-------------|-------------|
| **High** | #2711 | `create_agent` MCP tool security bypass: any container can create agent groups despite "admin-only" documentation. | No PR yet |
| **Medium** | #2312 | `groups/global/CLAUDE.md` removed on every startup, causing permanent dirty working tree. | No PR yet |
| **Medium** | #2705 (OPEN) | `use-native-credential-proxy` skill silently falls back to OneCLI gateway instead of actually bypassing it. | PR #2705 open |
| **Low** | #2531 (OPEN) | Poll loop duplicates text when `send_message` fires mid-turn. | PR #2531 open |

## Feature Requests & Roadmap Signals
The following features have active PRs or recently surfaced requests that are likely candidates for the next release:

- **DB-backed container configuration** (PR #2709): Adding `env` and `blocked_hosts` as JSON columns in `container_configs`, materializing maintainer-requested enhancement #1867. High signal for inclusion in next minor release.
- **Startup upgrade enforcement** (PR #2707, already merged): Sanctioned-path upgrade requirement is now live, indicating a shift toward stricter deployment hygiene.
- **Telegram topic isolation with auto-registration** (PR #1626, open since April): Long-standing feature skill adding Telegram channel topic isolation and automatic registration. Still pending review, suggests the feature is complex but desired.
- **Unit test coverage for CLI agent** (PR #2704, open): Exporting `parseArgs` for isolated testing indicates growing interest in test infrastructure.

## User Feedback Summary
- **Security concern**: User jonazri identified that `create_agent` is documented as admin-only but no access control is enforced, creating a vulnerability. This represents a gap between documentation and implementation that frustrates security-conscious users.
- **Deployment friction**: User mbernabeu reports a persistent dirty git working tree caused by a startup cleanup script, suggesting the project's local-first deployment model has rough edges for repeatable installations.
- **Configuration complexity**: Multiple PRs (#2709, #2705) address configuration persistence and credential proxy bypass, indicating users find the current container configuration and authentication proxy setup difficult to manage in production.
- **Performance documentation**: PR #2710 (merged) and user reports about slow Ollama paths reveal user frustration with out-of-box performance and the need for better documentation around caching optimization.

## Backlog Watch
- **#1626** — **Telegram topic isolation PR** (open since 2026-04-04, 64 days). This feature skill has been open for over two months with no maintainer comments. It represents a significant community contribution that may be at risk of abandonment. [Link](https://github.com/nanocoai/nanoclaw/pull/1626)
- **#2312** — **CLAUDE.md deletion bug** (open since 2026-05-06, 33 days). Despite being a reproducible, simple bug affecting all fresh clones, it remains unresolved. The issue comments suggest the fix may require architectural changes to the migration system. [Link](https://github.com/nanocoai/nanoclaw/issues/2312)
- **#2531** — **Poll-loop duplicate text fix** (open since 2026-05-18, 21 days). A straightforward bug fix PR that has received no maintainer comments. The bug affects message integrity during mid-turn sends. [Link](https://github.com/nanocoai/nanoclaw/pull/2531)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-08

## Today's Overview

IronClaw is in a period of **intense, focused development** on the "Reborn" architecture overhaul. Activity is very high, with 50 issues updated and 38 PRs updated in the last 24 hours, indicating a large and active team. The project is heavily invested in delivering the Reborn WebUI Beta, completing host-kernel security layers, and migrating legacy API surfaces. The 16 merged/closed PRs in the last day show strong forward momentum, though the 42 open/active issues and 22 open PRs suggest the team is managing a significant workload. No new releases were published today, which is consistent with the project being deep in development rather than a release cycle.

## Releases

**None** — no new releases were published in the last 24 hours. The last release remains `ironclaw` v0.29.1 and related crates (from PR #3708, which is still open).

## Project Progress

16 PRs were merged or closed in the last 24 hours. Key advances include:

| PR | Summary | Significance |
|---|---|---|
| [#4532](https://github.com/nearai/ironclaw/pull/4532) | Add Slack allowed-channel picker for WebUI v2 | Adds admin-managed Slack channel selection for Reborn host-beta |
| [#4530](https://github.com/nearai/ironclaw/pull/4530) | Add structured model-visible tool observations | Strengthens model-facing error/recovery data without expanding the `LoopSafeSummary` surface |
| [#4511](https://github.com/nearai/ironclaw/pull/4511) | Add outbound preference facade contracts | Phase 1 of outbound delivery preference contracts in `ironclaw_product_workflow` |
| [#4516](https://github.com/nearai/ironclaw/pull/4516) | Add WebChat v2 thread deletion | Enables authenticated thread deletion with proper cross-user safety |
| [#4463](https://github.com/nearai/ironclaw/pull/4463) | Wire Slack host-beta durable stores | Connects Slack conversation, outbound, and idempotency state to filesystem-backed stores |
| [#3298](https://github.com/nearai/ironclaw/pull/3298) | Add hermetic local gate | CI quality-of-life improvement: fmt, safety, clippy, and test gate for pre-push |
| [#3565](https://github.com/nearai/ironclaw/pull/3565) | Extend nightly E2E timeout | Stability improvement for CI pipelines |

## Community Hot Topics

The most active discussions center on **Reborn architecture security and production readiness**:

1. **[#3280](https://github.com/nearai/ironclaw/issues/3280)** — *"Add ProductWorkflow and InboundTurnService facade"* (7 comments)  
   This is the central blocking issue for adding the product-facing Reborn workflow facade. It references 11 related issues and represents a major architectural milestone.

2. **[#3036](https://github.com/nearai/ironclaw/issues/3036)** — *"Configuration-as-Code for IronClaw Reborn"* (5 comments, 1 👍)  
   An epic for declarative tenant blueprints and use-case harnesses. The community/user need is clear: operators want to configure IronClaw without hand-editing `.env`, JSON, and runtime flags.

3. **[#3044](https://github.com/nearai/ironclaw/issues/3044)** — *"Add local developer runtime profiles"* (3 comments)  
   Developer experience request: a simple `ironclaw run` command that avoids manual wiring of grants, mounts, and network policy.

**Underlying themes:** The Reborn architecture is complex and operators/developers are asking for simpler, more declarative, and more secure paths. The high comment counts on P0/P1 issues show the team is responsive to these needs.

## Bugs & Stability

**No new bugs or crash reports** were filed in the last 24 hours. The project has a strong security hardening pipeline in progress:

- **[#3956](https://github.com/nearai/ironclaw/issues/3956)** — RESOLVE_NO_XDEV bind-mount containment (open, security-review-required)
- **[#3957](https://github.com/nearai/ironclaw/issues/3957)** — Third-party hook activation hardening (open, security-review-required)
- **[#3924](https://github.com/nearai/ironclaw/issues/3924)** — NoExposureGuard composition follow-ups (open)

These are proactive hardening issues, not crash reports. The project appears stable with a focus on *preventing* future bugs through rigorous audit layers.

## Feature Requests & Roadmap Signals

**Likely in next release:**

- **Slack host-beta** (PR #4532, #4463) — nearly complete, with durable store wiring merged
- **WebChat v2 thread deletion** (PR #4516) — merged, will ship soon
- **User-scoped skill management** (PR #4527) — open, but actively developed
- **Structured model-visible tool observations** (PR #4530) — merged, improves model interaction safety

**Predicted for the release after next:**

- **Configuration-as-Code** (#3036) — epic still open, likely a major feature
- **Production composition root** (#3026, #3333) — critical for production cutover
- **No-exposure safeguards** (#3032) — production-readiness blocker
- **WebUI Beta release** (#3607) — the coordination issue suggests a beta launch is the goal

## User Feedback Summary

Explicit user feedback is limited (no user-submitted issues with high 👍 counts), but the issues themselves reveal clear operator pain points:

- **Configuration friction:** Multiple hand-edited config files with no schema, diff, or audit trail (#3036)
- **Developer onboarding complexity:** Engineers must manually wire grants, mounts, and network policy for local runs (#3044)
- **Legacy v1/v2 confusion:** Blurred boundaries between v1 channels and Reborn are causing integration friction (#3572)

The team is addressing these through the Reborn architecture, which aims to simplify with typed configuration, declarative blueprints, and clean module boundaries.

## Backlog Watch

Several high-priority issues have **not been updated in over a month** despite being tagged as P0/P1 blockers:

1. **[#3026](https://github.com/nearai/ironclaw/issues/3026)** — "Add config-driven production composition root" (P0, last updated 2026-06-07, created 2026-04-28)  
   *Status:* Still open, no PR attached. Critical for production cutover.

2. **[#3032](https://github.com/nearai/ironclaw/issues/3032)** — "Add no-exposure safeguards" (P0, created 2026-04-28)  
   *Status:* Still open. Security-critical for preventing sensitive data leaks.

3. **[#3029](https://github.com/nearai/ironclaw/issues/3029)** — "Add migration and compatibility bridges" (P1, created 2026-04-28)  
   *Risk:* Without this, existing production data cannot be migrated to Reborn.

All three are part of the Reborn cutover blocker set (#2987) and have been open for over 5 weeks. While the team is actively working on related PRs (#4530, #4532), these architectural blockers remain unresolved and could delay the production cutover timeline.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for June 8, 2026, which analyzes a concentrated wave of long-standing issues updated on a single day.

---

# LobsterAI Project Digest — 2026-06-08

## Today's Overview
The LobsterAI project shows low activity over the last 24 hours, with a significant backlog of 15 stale issues receiving updates but zero new releases or merged Pull Requests. While no new bugs were introduced today, the team is processing a large wave of previously filed bugs related to UI/UX consistency and state management. However, the complete absence of merged PRs and new releases indicates a **slow development cycle** or a focus on non-public infrastructure work. The community remains engaged primarily through bug reporting rather than feature contributions.

## Releases
**None.** There are no new releases to report for this date. The project has been stable on its current version since the last publish.

## Project Progress
**Merged/Closed PRs:** 0
- No Pull Requests were merged or closed in the last 24 hours. No new features or fixes have been advanced into the codebase during this period.

## Community Hot Topics
The most active discussion was on **Issue #1509** ("skills文件长时间生成阻塞无法感知"), which garnered 2 comments. This issue highlights a fundamental user experience problem: users are left in the dark during long-running skill generation tasks. The underlying need is for **real-time progress feedback and cancellation controls** during AI operations.

Another notable topic is **Issue #2121** (newest, 0 comments) about suspected token waste due to repeated AI output. This suggests growing user anxiety about cost efficiency, a common pain point in paid-API AI assistants.

- **#1509** (skills blocking, no feedback): [Link](https://github.com/netease-youdao/LobsterAI/issues/1509)
- **#2121** (token waste suspicion): [Link](https://github.com/netease-youdao/LobsterAI/issues/2121)

## Bugs & Stability
The following bugs, all updated today, are ranked by severity:

1.  **High: Skill State Inconsistency (Feedback Loop Broken)** — **#1500**: Disabling a skill via toggle does not remove it from `activeSkillIds`, causing it to be re-injected into future conversations. This is a data integrity bug that leads to confusing behavior. [Link](https://github.com/netease-youdao/LobsterAI/issues/1500)
2.  **High: OAuth Token Loss (Data Loss)** — **#1516**: Closing the Settings panel during GitHub Copilot OAuth polling causes the success token to be silently discarded. This is a user trust issue. [Link](https://github.com/netease-youdao/LobsterAI/issues/1516)
3.  **Medium: UI State Desync** — **#1502**: Saving Agent skills does not sync `activeSkillIds` in the current session until a manual Agent switch. [Link](https://github.com/netease-youdao/LobsterAI/issues/1502)
4.  **Medium: Silent Data Loss (Notifications)** — **#1506**: IM notifications in scheduled tasks fail silently if no session is selected. [Link](https://github.com/netease-youdao/LobsterAI/issues/1506)
5.  **Low: Missing Form Validation** — **#1504**: AES Key field for POPO IM bot is not validated, allowing empty saves. [Link](https://github.com/netease-youdao/LobsterAI/issues/1504)
6.  **Low: Configuration UI Broken** — **#1512**: QQ Bot whitelist mode has no add-input field, making the feature unusable. [Link](https://github.com/netease-youdao/LobsterAI/issues/1512)
7.  **Low: Documentation** — **#1513**: Legal terms page has duplicate numbers and incomplete parentheses. [Link](https://github.com/netease-youdao/LobsterAI/issues/1513)
8.  **CI/Infra** — **#1518**: Labeler workflow has permission issues. [Link](https://github.com/netease-youdao/LobsterAI/issues/1518)

**Note:** None of these bugs have associated fix PRs yet.

## Feature Requests & Roadmap Signals
The stale issues reflect a clear user demand for **advanced data management and organization**. These are strong candidates for a future v0.4.x release:

- **Session Color Coding** (#1525) — Users want to visually distinguish sessions (like VS Code tabs).
- **Batch Export** (#1528) — Users need to export multiple sessions at once for backup or migration.
- **Message Bookmarks** (#1537) — Users need to mark important AI replies in long conversations.
- **Tag-based Filtering** (#1541) — Users want a full tag/label system to organize hundreds of sessions.
- **Local Usage Statistics** (#1532) — Users want to see their own usage stats (e.g., total messages, daily activity).

**Prediction:** The tagging (#1541) and bookmarks (#1537) features are the most likely to be prioritized next, as they directly address the "information retrieval" pain point that dominates user feedback.

## User Feedback Summary
User feedback is overwhelmingly focused on **predictability and control**. Key pain points include:
- **Frustration with "black box" behavior:** Users are angry about not knowing if the AI is working (#1509) and not understanding why it uses tokens inefficiently (#2121).
- **Confusion over state:** Users find it confusing when UI toggles do not reflect actual system state (e.g., disabling a skill that is still active).
- **Desire for power-user features:** There is a strong, repeated ask for data management features (tags, exports, bookmarks) typical of mature productivity tools.

**Satisfaction is low** due to the combination of UI bugs and a lack of advanced organizational tools.

## Backlog Watch
The following long-stale issues (updated today but created 2 months ago) require urgent maintainer attention:

- **#1500** (Skill state inconsistency) — UX broken; high-impact.
- **#1509** (Skills generation blocking) — Customer satisfaction issue.
- **#1516** (OAuth token loss) — Data loss is a critical regression.
- **#2121** (Token waste) — Community concern; needs a clear technical explanation or a fix soon.

**Recommendation:** Maintainers should triage these 15 issues quickly, assigning severity labels and either closing with "won't fix" or adding to the next sprint. The silence on these high-impact bugs is creating a negative feedback loop with the user base.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the structured project digest for **Moltis** on **2026-06-08**.

---

## Moltis Project Digest – June 8, 2026

### 1. Today's Overview
Activity on the Moltis project has cooled slightly from the previous week, with only one open issue and three open pull requests updated in the last 24 hours. No new releases were published today, indicating the team is likely in a stabilization or review phase rather than shipping new code. The three open PRs are all authored by the same core contributor (s-salamatov) and focus on infrastructure improvements: Telegram streaming behavior, session memory management, and channel visibility controls. The project appears healthy but with reduced churn—suggesting a focus on merging existing work rather than starting new features.

### 2. Releases
**No new releases were published today (June 8, 2026).** The latest release history shows no tagged versions in the recent data. There are no migration notes or breaking changes to report.

### 3. Project Progress
**No pull requests were merged or closed today.** All three PRs remain open. However, the three active PRs represent meaningful progress:
- **PR #1113 (hotfix – Telegram streaming):** Addresses a regression where the final streamed reply was not treated as final when Telegram streaming was enabled but completion notifications were disabled. This restores logical consistency for users who disable completion pings.
- **PR #1089 (tool result capping):** Introduces a cap on persisted `tool` and `tool_result` content when session history is rehydrated into provider-bound messages. This prevents memory blowouts across normal chat, streaming, retry-after-compaction, and LLM-backed compaction prompts.
- **PR #1093 (channel activity log visibility):** Adds per-account, per-channel, and per-user `activity_log` visibility settings (options: `all`, `errors_only`, `off`), with user overrides taking priority over channel/account defaults. This includes normal and attachment-based replies.

### 4. Community Hot Topics
**#1107 – [Feature] Multiline text input in mobile web UI**
- **Comments:** 1 | **Reactions:** 0
- **Link:** [Issue #1107](https://github.com/moltis-org/moltis/issues/1107)
- **Analysis:** This is the only actively discussed issue today. The user requests support for multiline text input on the mobile web interface. While it has only one comment, the underlying need is clear: mobile users currently lack a way to input formatted or multi-line text, which is a quality-of-life blocker for those who draft longer prompts or code snippets on phones. This is a relatively low-complexity UI enhancement that may be picked up if the team prioritizes mobile parity.

**No other issues or PRs have accumulated comments or reactions beyond the author and maintainer interactions.**

### 5. Bugs & Stability
**No new bugs were reported today.** The only PR related to stability is **PR #1113** (Telegram streaming hotfix), which addresses a logic bug introduced by PR #1099. The bug causes the final answer to not be streamed as expected when Telegram streaming is enabled but completion notifications are disabled. Severity: **Medium** – it affects user experience but only in a specific configuration (Telegram + stream on + completion notify off). No crashes or regressions were reported in the past 24 hours.

### 6. Feature Requests & Roadmap Signals
The only feature request open today is **Issue #1107 (multiline text input in mobile web UI)**. This is a low-effort, high-impact UI change that would directly improve the mobile experience. Given that the core team has recently been active on Telegram and channel UX (PR #1093), a mobile UI improvement could logically follow in the next minor release. The project roadmap is not publicly documented in this data, but the volume of infrastructure PRs (memory capping, visibility settings) suggests the team may be preparing for a more stable release candidate before adding new UI features.

### 7. User Feedback Summary
**Pain points:**
- Mobile web users cannot input multiline text (Issue #1107). This is a clear usability gap for on-the-go use.

**Satisfaction signals:**
- No direct positive feedback is visible in the last 24 hours. However, the lack of bug reports or complaints about recent changes suggests the project is stable and the recent PRs (especially tool result capping and Telegram hotfix) are addressing real performance and reliability concerns that users may have encountered silently.

**Use cases:**
- Telegram bot integration (streaming final replies) – PR #1113.
- Team/channel communication with activity log controls – PR #1093.
- Long-running sessions with many tool calls (memory management) – PR #1089.

### 8. Backlog Watch
**No long-unanswered issues or PRs were identified.** The oldest open PR in the dataset is PR #1089 (created June 1), which has seen updates as recently as June 7. The oldest open issue is #1107 (created June 5). Both have active maintainer attention. No items appear to be languishing without response.

---

**Project Health Summary:** Moltis is in a stable, maintenance-focused phase. The core team is actively iterating on Telegram integration, session memory safety, and channel visibility. The mobile UI gap is the clearest user-facing opportunity. No blockers or critical issues are present.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured project digest for **CoPaw** (github.com/agentscope-ai/CoPaw) based on data from **2026-06-08**.

---

## CoPaw Project Digest – 2026-06-08

### 1. Today's Overview
The CoPaw project is in a period of **moderate, maintenance-heavy activity**, with 13 issues and 5 PRs updated in the last 24 hours. While no new releases were published, the community is driving a significant **stabilization push**, particularly around the Yuanbao channel integration, which saw multiple bugs closed via targeted fixes. A major infrastructure effort is underway with a **WIP Plugin Extension infrastructure** PR, signaling a shift toward extensibility. User feedback remains vocal, with several feature requests focusing on visual model flexibility and real-time interaction feedback.

### 2. Releases
**None.**  
No new releases or release candidates were published within the last 24 hours.

### 3. Project Progress
Two PRs were merged/closed today, both authored by **jc200808**, directly addressing Yuanbao channel stability:
- **[#4983] fix(channels): store connectId from AuthBindRsp for connection tracking**  
  Resolves Issue #4978. Ensures the connection ID is captured for proper session tracking.  
  [PR Link](https://github.com/agentscope-ai/CoPaw/pull/4983)
- **[#4982] fix(channels): fix Yuanbao streaming replies silently dropped when streaming_enabled=True**  
  Resolves Issue #4979. Overrides `on_streaming_end` to properly flush the streaming buffer.  
  [PR Link](https://github.com/agentscope-ai/CoPaw/pull/4982)

Additionally, a **new first-time contributor** submitted PR **#4995**, which preserves tool output attachments and visible text when `show_tool_details` is disabled, improving UI fidelity.  
[PR Link](https://github.com/agentscope-ai/CoPaw/pull/4995)

### 4. Community Hot Topics
The most active discussions revolve around **infrastructure and usability**:

- **[#4992] [Enhancement]: Support Independent Visual Model Configuration (Fallback)**  
  Comments: 2. This request proposes adding a `visual_model` config to route image/video processing to a separate model when the main model lacks multimodal capabilities (e.g., text-only models). This reflects a desire for **model composability** without vendor lock-in.  
  [Issue Link](https://github.com/agentscope-ai/CoPaw/issues/4992)

- **[#4986] [Enhancement]: Real-time interaction display when executing shell commands**  
  Comments: 1. Users want live feedback during shell/write operations, comparing expectations to tools like Cursor and WorkBuddy. This indicates a **UX gap in agent task transparency**.  
  [Issue Link](https://github.com/agentscope-ai/CoPaw/issues/4986)

- **[#4996] [WIP PR]: Plugin Extension Infrastructure**  
  This is the most significant structural PR in flight. It proposes a unified registration mechanism for menus, routes, slots, chat extensions, and a host SDK. If merged, this will enable third-party plugin development and could be a **cornerstone for future ecosystem growth**.  
  [PR Link](https://github.com/agentscope-ai/CoPaw/pull/4996)

### 5. Bugs & Stability
Bug reports today are **medium to high severity**, with a specific cluster around the **Yuanbao channel**:

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| [#4990](https://github.com/agentscope-ai/CoPaw/issues/4990) | High | Enterprise WeChat returns "sorry, cannot answer" error after tool call. Affects v1.1.10. | **Open** – no fix PR yet. |
| [#4989](https://github.com/agentscope-ai/CoPaw/issues/4989) | High | Local Qwen 3.6-27B model (vLLM) hangs on v1.1.9/1.1.10 after successful connection test. Regression from v1.1.5.post2. | **Open** – likely a regression in the model adapter. |
| [#4993](https://github.com/agentscope-ai/CoPaw/issues/4993) | Medium | Image viewer jitters when zoomed and dragged (macOS v1.1.10). Affects console UI. | **Open** – no PR yet. |
| [#4991](https://github.com/agentscope-ai/CoPaw/issues/4991) | Low | Question-only issue lacking context. | **Open** – needs maintainer clarification. |

The previously reported Yuanbao proto issues (##4976–4980) have all been resolved with today's merged PRs.

### 6. Feature Requests & Roadmap Signals
Several feature requests suggest where the project is headed:

1. **Visual Model Fallback (#4992)** – Likely to be prioritized given high user appeal. Could appear in v1.1.11.
2. **Plugin Extension Infrastructure (#4996)** – This is a **long-term roadmap item** that, if merged, will unlock ecosystem expansion. Not imminent for the next patch release.
3. **Memory System Enhancement (#4994)** – Calls for a "hierarchical memory system" like those in mainstream agent frameworks. This signals a **strategic gap** in long-term capability.
4. **Static UI improvements (#4985)** – Approval command text wrapping and image zoom jitter (#4993) are likely quick wins for the next release.

### 7. User Feedback Summary
- **Pain Points**:
  - Regression in local model support (Qwen 3.6-27B on vLLM) causing silent failures (#4989).
  - Enterprise WeChat channel returning generic error messages after tool calls (#4990).
  - Lack of real-time feedback during shell execution (#4986) and poor command display (#4985).
- **Use Cases**:
  - Multimodal capability via external visual models (text-only models + vision fallback) (#4992).
  - Plugin extensibility for custom UI and functionality (#4996).
- **Satisfaction**:
  - Positive response to Yuanbao channel fixes (proto packaging, AuthBindRsp, streaming) shows appreciation for targeted maintenance.
  - Frustration visible in #4989, where a working setup broke between two patch versions—reducing trust in upgrade stability.

### 8. Backlog Watch
- **[#4994] [Feature]: Memory system enhancement** – Created 2026-06-07, no maintainer response. This is a **high-impact feature gap** that aligns with broader agent capabilities.  
  [Issue Link](https://github.com/agentscope-ai/CoPaw/issues/4994)

- **[#4991] [Question]: (No title)** – Minimal context provided. Needs maintainer follow-up to clarify or close.  
  [Issue Link](https://github.com/agentscope-ai/CoPaw/issues/4991)

- **[#4949] [PR]: ACP server metadata enhancements** – Open since June 3, under review. This PR extends the Agent Client Protocol server for terminal UI support. Maintainer attention needed to move forward or merge.  
  [PR Link](https://github.com/agentscope-ai/CoPaw/pull/4949)

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-08

## 1. Today's Overview

ZeroClaw shows heavy development activity with 50 issues and 50 PRs updated in the last 24 hours, though notable churn exists with 18 closed issues and 12 merged/closed PRs. The project appears to be preparing for a **v0.8.0 release** (PR #7364), with significant feature work landing on MCP management dashboards, webhook routing, and provider expansion. Community engagement remains strong across long-standing enhancement requests (many dating to March 2026) while several S1/S2 bugs remain unresolved. No new official releases were published today.

## 2. Releases

**No new releases today.**

The last published release remains prior to this digest. However, PR #7364 (`chore(release): release v0.8.0`) is currently open, indicating a **v0.8.0 release is being prepared**. This suggests new features may be imminent, including schema v3 provider architecture, outbound message queues, per-alias provider fallback chains, and new MCP/tool management UIs.

---

## 3. Project Progress

**12 PRs were merged or closed today** (10 merged, 2 closed without merge). Key advances:

| PR | Description | Status |
|---|---|---|
| [#7260](https://github.com/zeroclaw-labs/zeroclaw/pull/7260) | Added 7 new OpenAI-compatible providers (morph, github_models, upstage, featherless, arcee, lambda_ai, inception) under schema v3 | Open |
| [#7249](https://github.com/zeroclaw-labs/zeroclaw/pull/7249) | Theme enhancements: color-depth fallback, registry-generated presets, per-agent overrides | **Merged** |
| [#7190](https://github.com/zeroclaw-labs/zeroclaw/pull/7190) | Outbound message queue with sidebar and injection (replaces hard input block) | **Merged** |
| [#7209](https://github.com/zeroclaw-labs/zeroclaw/pull/7209) | In-session model/provider picker (`/model` and `/model-provider` commands) | **Merged** |
| [#7178](https://github.com/zeroclaw-labs/zeroclaw/pull/7178) | Per-alias model-provider fallback on failure (reintroduced) | **Merged** |
| [#7360](https://github.com/zeroclaw-labs/zeroclaw/pull/7360) | Fix: Quickstart modals sized by wrapped row height instead of logical line count | **Merged** |
| [#7330](https://github.com/zeroclaw-labs/zeroclaw/pull/7330) | Fix: Quickstart model-provider form UX defects | Open |
| [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) | New dashboard tabs: MCP, Skills, Plugins & Providers management | Open |
| [#7367](https://github.com/zeroclaw-labs/zeroclaw/pull/7367) | Per-alias webhook path routing for multi-instance channels | Open |
| [#7234](https://github.com/zeroclaw-labs/zeroclaw/pull/7234) | Migrate gateway/channel consolidation to MemoryStrategy | Open |

**Notable pattern**: The "DO NOT MERGE - AUTHOR WILL MERGE WHEN READY" label appears on several high-risk PRs (#7190, #7209, #7178, #7249, #7330), suggesting heavy parallel development with self-merge workflows.

---

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Summary |
|---|---|---|---|
| [#4866](https://github.com/zeroclaw-labs/zeroclaw/issues/4866) — [CLOSED] Web dashboard unavailable | **28** | 0 | Persistent bug across many versions — both web UI and Tauri desktop app show "Web dashboard not available." **Critical UX blocker** now resolved. |
| [#4710](https://github.com/zeroclaw-labs/zeroclaw/issues/4710) — Better logo | **11** | 👍2 | Community member proposed new logo design, attached images. Low priority but high community sentiment. |
| [#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146) — Token consumption minimization | **9** | 👍1 | User requests skill compilation to reduce prompt size (400+ lines → minimal). High impact for cost-sensitive users. |
| [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) — Full Docker image | **9** | 👍3 | Blocked feature request for a pre-built image with all feature flags enabled. **Blocked** status with no resolution. |
| [#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) — NapCat/OneBot channel | **9** | 0 | User cannot find NapCat or OneBot channel option for QQ integration. Requested since March 2. |

**Analysis**: The community's primary needs cluster around **accessibility barriers** — the web dashboard outage (#4866), Docker image complexity (#3642), and missing communication channels (#2503) drive the most discussion. Token cost optimization (#5146) reflects enterprise/advanced user concerns about LLM operational costs.

---

## 5. Bugs & Stability

### Highest Severity (S0 — Data Loss / Security Risk)

- **[#4627](https://github.com/zeroclaw-labs/zeroclaw/issues/4627) — file_write tool silently fails** (S0, open)
  - Files written via `file_write` are invisible on host filesystem despite reporting success.
  - Impact: Potential data loss, security risk. Status: `in-progress`.

### High Severity (S1 — Workflow Blocked)

- **[#4866](https://github.com/zeroclaw-labs/zeroclaw/issues/4866) — Web dashboard unavailable** (S1, **recently closed**)
  - Remote cause of frustration now resolved.
- **[#4827](https://github.com/zeroclaw-labs/zeroclaw/issues/4827) — auto_compact_history in channel mode** (S1, **closed**)
  - Channel mode discarding intermediate tool-call context.
- **[#5803](https://github.com/zeroclaw-labs/zeroclaw/issues/5803) — Fallback provider config ignored** (S1, **closed**)
  - Credentials resolving only from env vars, ignoring TOML config.
- **[#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) — Gemini CLI OAuth broken** (S1, open)
  - Post-authentication, all attempts return `rate_limited` errors. 3 comments, no fix PR yet.
- **[#5155](https://github.com/zeroclaw-labs/zeroclaw/issues/5155) — Delegate agents ignore prompt_injection_mode** (S1, **closed**)
  - Skills always injected in Full mode regardless of global config.

### Medium Severity (S2 — Degraded Experience)

- **[#5122](https://github.com/zeroclaw-labs/zeroclaw/issues/5122) — web_fetch allowed_private_hosts broken** (S2, **closed**)
  - Domains resolving to private IPs blocked despite being in allowlist.
- **[#4848](https://github.com/zeroclaw-labs/zeroclaw/issues/4848) — MCP not working** (S2, **closed**)
- **[#4880](https://github.com/zeroclaw-labs/zeroclaw/issues/4880) — context_compression not triggered in daemon mode** (S2, **closed**)

### Today's New Bugs (Opened/Updated June 7-8)

| Issue | Severity | Summary | Has Fix PR? |
|---|---|---|---|
| [#7366](https://github.com/zeroclaw-labs/zeroclaw/pull/7366) — fix(zerocode): restore mid-turn input | Medium | Input blocked permanently after outbound message queue PR #7190 merged | ✅ Yes (this PR) |
| [#7346](https://github.com/zeroclaw-labs/zeroclaw/pull/7346) — fix(cli): show model names | Low | `zeroclaw models list` only shows count, not names | ✅ Yes (this PR) |
| [#7274](https://github.com/zeroclaw-labs/zeroclaw/pull/7274) — schema_version not stamped on incremental saves | Medium | Config CRUD from dashboard strips schema version | ✅ Yes (this PR) |

### Regressions
- The merged PR [#7190](https://github.com/zeroclaw-labs/zeroclaw/pull/7190) (outbound message queue) shipped with a **regression** already being fixed in [#7366](https://github.com/zeroclaw-labs/zeroclaw/pull/7366): input remained blocked after the outbound queue was introduced.

---

## 6. Feature Requests & Roadmap Signals

### Likely for v0.8.0 (from open PRs and accepted issues)

| Feature | Issue/PR | Priority | Status |
|---|---|---|---|
| **MCP & Skills Dashboard Tabs** | [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) | High | Open (reviewed) |
| **Per-alias webhook routing** | [#7367](https://github.com/zeroclaw-labs/zeroclaw/pull/7367) | P2 | Open |
| **Per-alias model-provider fallback** | [#7178](https://github.com/zeroclaw-labs/zeroclaw/pull/7178) | P2 | **Merged** |
| **7 new providers** | [#7260](https://github.com/zeroclaw-labs/zeroclaw/pull/7260) | Low | Open |
| **MemoryStrategy migration** | [#7234](https://github.com/zeroclaw-labs/zeroclaw/pull/7234) | P2 | Open |

### High-Priority Accepted Features (no PR yet)

| Issue | Summary | Priority | Risk |
|---|---|---|---|
| [#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146) | Token consumption minimization via skill compilation | P2 | High |
| [#3566](https://github.com/zeroclaw-labs/zeroclaw/issues/3566) | Agent-to-Agent (A2A) protocol support | P2 | High |
| [#2767](https://github.com/zeroclaw-labs/zeroclaw/issues/2767) | Multi-agent routing | P2 | High |
| [#4760](https://github.com/zeroclaw-labs/zeroclaw/issues/4760) | Tool-calling for memory consolidation | P2 | High |
| [#4853](https://github.com/zeroclaw-labs/zeroclaw/issues/4853) | Installing skills from `.well-known` URI | P2 | High |
| [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293) | Air-gapped execution mode (RFC) | P2 | High |
| [#5127](https://github.com/zeroclaw-labs/zeroclaw/issues/5127) | Configurable bubblewrap sandbox paths | P2 | High |

### Prediction
The **v0.8.0 release** will likely ship with the merged fallback provider chains and outbound message queue, plus the new dashboard tabs and webhook routing features currently in review. The air-gapped mode (#6293) and A2A protocol (#3566) appear too high-risk for immediate inclusion.

---

## 7. User Feedback Summary

### Pain Points

1. **Web dashboard unreliability** — Issue [#4866](https://github.com/zeroclaw-labs/zeroclaw/issues/4866) with 28 comments documents months of frustration with the web UI being unavailable, requiring CLI builds. **Now closed**, but cumulative impact on trust.

2. **Docker complexity** — Issue [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) (9 comments, 👍3) echoes non-technical users struggling with feature flags and memory consumption defaults. User sentiment: "high barrier of entry."

3. **Missing channel integrations** — [#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) (QQ/NapCat, 9 comments) and [#4873](https://github.com/zeroclaw-labs/zeroclaw/issues/4873) (Feishu/Lark only calling LLM instead of Agent) show integration gaps.

4. **Token cost concerns** — [#5146](https://github.com/zeroclaw-labs/zeroclaw/issues/5146) (9 comments) highlights user frustration with sending full skill documentation on every request — particularly for repetitive queries.

5. **Logging to stdout** — [#4721](https://github.com/zeroclaw-labs/zeroclaw/issues/4721) (3 comments) — CLI users surprised logs mix with command output, breaking piping.

### Satisfaction Signals
- Multiple enhancement requests accepted and labeled `status:accepted` suggest maintainers are responsive.
- Docker user [#6760](https://github.com/zeroclaw-labs/zeroclaw/issues/6760) contributed working YAML, signaling sub-community self-help.
- Three "help wanted" labels on issues (#4853, #4721, #4703) indicate maintainers are open to community contributions.

---

## 8. Backlog Watch

### Issues Requiring Maintainer Attention

| Issue | Age | Last Update | Status Signals | Why Notable |
|---|---|---|---|---|
| [#3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642) — Full Docker image | Mar 15 (84 days) | Jun 7 | `status:blocked`, `needs-maintainer-review` | High community demand (👍3), no resolution path visible |
| [#2467](https://github.com/zeroclaw-labs/zeroclaw/issues/2467) — Webhook transforms | Mar 2 (98 days) | Jun 7 | `status:blocked` | Old, important for GitHub/GitLab webhook users |
| [#4627](https://github.com/zeroclaw-labs/zeroclaw/issues/4627) — file_write silent failure | Mar 25 (75 days) | Jun 7 | `status:in-progress` | **S0 severity** — data loss — no committed fix despite active status |
| [#5803](https://github.com/zeroclaw-labs/zeroclaw/issues/5803) — Fallback provider config ignored | Apr 16 (53 days) | **Closed Jun 7** | Fixed | Resolved after 52 days — S1 severity is concerning latency |
| [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) — Gemini OAuth broken | Mar 28 (72 days) | Jun 7 | `status:in-progress`, `needs-author-action` | S1 blocker for Gemini users, no resolution in sight |
| [#6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293) — Air-gapped RFC | May 3 (36 days) | Jun 7 | `status:blocked`, `needs-maintainer-review` | Critical for sensitive deployments, stuck in RFC review |
| [#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184) — i18n git submodule | Jun 4 (4 days) | Jun 7 | `type:rfc`, `priority:p3` | New, but important for translation maintainability |

### PRs Needing Maintainer Review
- [#6490](https://github.com/zeroclaw-labs/zeroclaw/pull/6490) — Human-readable integration category labels (open since May 6, `needs-author-action`)
- [#7361](https://github.com/zeroclaw-labs/zeroclaw/pull/7361) — Per-turn output routing + voice delivery fixes (new, broad scope across 8+ channels)

### Assessment
The S0 data loss bug [#4627](https://github.com/zeroclaw-labs/zeroclaw/issues/4627) (file_write silent failure) remaining open for 75 days with no completed fix is the **most critical backlog item**. The Gemini OAuth blocker [#4879](https://github.com/zeroclaw-labs/zeroclaw/issues/4879) at 72 days without resolution also reflects a pattern where high-severity issues linger despite active development elsewhere.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*