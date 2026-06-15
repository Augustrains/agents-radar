# OpenClaw Ecosystem Digest 2026-06-15

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-15 02:29 UTC

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

# OpenClaw Project Digest
**Date:** 2026-06-15

---

## 1. Today's Overview

OpenClaw shows extremely high activity with 500 issues and 500 PRs updated in the last 24 hours, though this reflects the project's massive ongoing volume rather than a single-day spike. The community is actively engaged, with 405 open issues and 425 open PRs indicating a heavy triage burden on maintainers. One new beta release was published (`v2026.6.8-beta.1`). Critical stability concerns dominate the discourse, with multiple "platinum hermit" severity bugs open around session state corruption, message loss, and event loop failures. The project appears to be in a period of intense debugging following recent feature rollouts, particularly around Codex app-server integration and channel delivery improvements.

---

## 2. Releases

**New Release:** `v2026.6.8-beta.1` (2026.6.8)

**Highlights:**
- **Telegram channel delivery:** Now supports structured rich text with tables, lists, and expandable blockquotes. CLI backend delivery is now prompt-preserving. Native draft migration has been retired. Rich-media boundaries are safer.
- **WhatsApp channel delivery:** Similarly improved for richer, less brittle message handling.

**Notable:**
- This is a **beta release**; no documented breaking changes or migration notes in the provided data.

---

## 3. Project Progress

**Merged/Closed PRs (today):** 75 (out of 500 updated)

Key merged advances:

- **[PR #92943]** — Refresh memory index state after external reindex (Memory core)
- **[PR #92970]** — Fix gateway `sessions.describe` to thread `agentId` through to resolve scoped global sessions (fixes critical session routing bug)
- **[PR #92964]** — Same root cause as #92970: gateway `sessions.describe` was dropping the requested `agentId`
- **[PR #93077]** — Fix gateway `sessions.describe` scope to the requested agent
- **[PR #93054]** — Fix Control UI chat not clearing after hard `/reset`
- **[PR #91272]** — Fix queue: preserve queued platform message IDs in collect drains (fixes #36212)
- **[PR #90441]** — Fix qa-lab child process signal bleeding under Node 24
- **[PR #90330]** — Fix ChatGPT Codex streams without content-type header
- **[PR #93128]** — Fix security: bound ancestor context file walk at home directory (fixes #92561)
- **[PR #93105]** — Fix doctor: repair null `agents.list[].workspace` values (fixes #77718)

**Key Advanced Features (Open PRs):**
- **[PR #93125]** — Adds `compaction.fallbacks: string[]` for ordered model fallback chains during compaction failures (important for reliability)
- **[PR #85359]** — Adds `local_skill_route` tool for ranking available skills
- **[PR #92340]** — Feishu VC meeting invite handling
- **[PR #78381]** — Exposes embedded runner prep stage timings for plugin observability

---

## 4. Community Hot Topics

### Most Active Issues (by comments)

| Issue | Comments | Reactions | Topic |
|-------|----------|-----------|-------|
| [#80380] (Closed) | 14 | 👍4 | Updating to GA Gemini 3.1 Flash-Lite |
| [#84516] (Open) | 11 | 👍2 | Codex app-server: agent replies silently truncated at ~1000 chars |
| [#85103] (Open) | 9 | 👍1 | Model fallback chain not triggered on provider-wide quota exhaustion |
| [#85251] (Open) | 8 | 👍1 | Codex app-server emits notification:turn/started then goes silent |
| [#85126] (Open) | 8 | 👍1 | Control UI sessions auto-select wrong authProfileOverride |
| [#85030] (Open) | 8 | 👍3 | MCP tools not injected into subagent sessions |
| [#84903] (Open) | 8 | 👍2 | Single stalled agent session blocks entire Gateway event loop |
| [#83184] (Open) | 8 | 👍3 | Heartbeat-driven agent replies leave pendingFinalDelivery stuck |
| [#88951] (Open) | 8 | 👍1 | Duplicate message content (started after upgrade) |
| [#45494] (Open) | 8 | 👍0 | Cron agent jobs silently time out during LLM API outages |

### Most Active PRs (by comment count)
All 30 displayed PRs have `undefined` comment counts in the data, making direct comparison impossible. However, notable PRs with high urgency include:
- **[PR #93117]** — Fix thinking-block recovery retry after control-plane start event (P1)
- **[PR #93116]** — Fix xAI to respect ssrfPolicy and request.allowPrivateNetwork in image_generate
- **[PR #93110]** — Fix cron isolated delivery with delivery route lease store

### Analysis of Underlying Needs
The community is sharply focused on **session reliability** and **message integrity**. Users are experiencing:
1. **Silent truncation of agent replies** in Codex integrations (#84516)
2. **Failed model fallback chains** leading to complete service outages (#85103)
3. **Event loop isolation failure** where one stalled session kills the entire gateway (#84903)
4. **Session state corruption** causing wrong auth profiles (#85126), stalled heartbeats (#83184), and duplicate messages (#88951)
5. **Desire for better configuration flexibility** — compaction fallbacks (#93125), configurable page groups (#92105), and streaming mode commands (#74077)

The volume of "platinum hermit" severity issues indicates users are experiencing **production-affecting outages** that erode trust.

---

## 5. Bugs & Stability

### Critical (P0/P1 — active issues, no fix PR yet)

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#84516] | P1 Platinum | Codex agent replies silently truncated at ~1000 chars | No |
| [#85103] | P1 Platinum | Model fallback chain not triggered on quota exhaustion | No |
| [#85251] | P1 Platinum | Codex app-server goes silent mid-turn; session wedges 360s | No |
| [#84903] | P1 Platinum | Single stalled session blocks entire Gateway event loop | No |
| [#83184] | P1 Diamond | Heartbeat-driven replies leave pendingFinalDelivery stuck | No |
| [#85030] | P1 Diamond | MCP tools not injected into subagent sessions | No |
| [#88951] | P1 Silver | Duplicate message content (regression after 2026.5.27) | No |
| [#45494] | P1 Diamond | Cron jobs silently time out during LLM API outages | No |
| [#85126] | P1 Open | Control UI sessions auto-select wrong authProfileOverride | No |
| [#84536] | P1 Platinum | Preemptive context overflow silently kills embedded sessions | No |

### Critical (P0/P1 — with fix PRs open)

| Issue | Severity | Description | Fix PR |
|-------|----------|-------------|--------|
| [#84569] | P1 Diamond | WhatsApp session stalls on long model_call | [#85402] (waiting on author) |
| [#84771] | P1 Platinum | Event loop saturation during startup (28-64s delays) | No |
| [#84674] | P1 Diamond | Telegram isolated ingress spool stuck by stale .processing claim | No |
| [#92460] | P1 Platinum | Isolated cron completion drops explicit delivery.channel | [#93110] (needs proof) |
| [#92960] (via PR) | Gateway sessions.describe drops agentId | Fixed in [#92970] (merged) |

### Regressions (reported today)
- **(from closed issues)** [#90886] — Gateway hangs at startup when configured provider lacks credentials (regression v2026.4.8 → v2026.4.26) — **Closed, likely fixed**
- [#88951] — Duplicate message content started after upgrading from 2026.5.4 to 2026.5.27
- [#81484] — Discord guild reply regression in 2026.5.7 (malformed send payloads, repeated outbound loops)

### Security Issues
- **[PR #93128] (merged)** — Bound ancestor context file walk at home directory to prevent reading system files (fixes [#92561])
- **[#85030] (Open)** — MCP tools not properly injected — potential security boundary bypass in subagent sessions
- **[#81917] (Open)** — Dashboard logs bare URL despite token auto-auth, can hang on Linux/KDE browser launch
- **[#85332] (Open)** — Request for slim Docker image with configurable APT packages

---

## 6. Feature Requests & Roadmap Signals

### High-Interest Feature Requests (with community traction)

| Issue | Description | Reactions | Likely Next Version? |
|-------|-------------|-----------|---------------------|
| [#74077] | Slash command to set preview streaming mode per chat session | 👍1 | Possible — low effort, high UX impact |
| [#44395] | Heading-aware chunking + entity extraction for memory search | 👍2 | Possible — core memory improvement |
| [#56781] | Fallback model chain for compaction and LCM summaryModel | 👍1 | **Very likely** — [PR #93125] already implements this |
| [#81061] | `before_route_inbound_message` hook for channel bridging | 👍3 | Possible — high plugin developer demand |
| [#81913] | Expose stable plugin SDK surface for installed skill workflows | 👍1 | Likely — multiple PRs touching skill infrastructure |
| [#85332] | Slim Docker image with configurable APT packages | 👍1 | Low priority currently |
| [#92105] | Configurable page groups for memory-wiki | 👍1 | Possible — ecosystem plugin demand |

### Likely Next-Release Features
1. **Compaction fallbacks** ([PR #93125]) — already implemented, awaiting proof
2. **Local skill route tool** ([PR #85359]) — adds new agent capability
3. **Feishu VC meeting invites** ([PR #92340]) — channel integration expansion
4. **Encoding parameter for `read` tool** ([PR #92680]) — addressing Chinese Windows GBK files

---

## 7. User Feedback Summary

### Pain Points (high urgency)

1. **Session reliability collapse** — Multiple reports of sessions silently stalling, truncating replies, or dying without notification. Users report receiving "correct channel reply then misleading takeover message" ([#85402]).

2. **Upgrade instability** — Users repeatedly report regressions after upgrading:
   - [#88951]: "Duplicate message content started after upgrading from 2026.5.4 to 2026.5.27"
   - [#91016]: "DeepSeek Prompt Cache completely failed after upgrade to 2026.6.1, burning ~$6/hour"
   - [#85027]: "macOS LaunchAgent Gateway became unrecoverable after upgrade 2026.5.6 → 2026.5.19"

3. **Model/Hardware configuration friction** — Users express frustration when model fallbacks don't work as expected ([#85103]), auth profiles are auto-selected wrong ([#85126]), or provider integrations break across upgrades.

4. **Chinese users specific** — Reports of GBK encoding issues ([#92680]), DeepSeek cache failure costing significant money ([#91016]), and Feishu streaming rendering as cards instead of plain text ([#91886]).

### Satisfaction Signals

- **Active community contribution** — Large volume of PRs (500 updated in 24h) suggests an engaged developer community willing to submit fixes.
- **Quick turnaround on some fixes** — PRs [#92970], [#92964], [#93077] for the `sessions.describe` bug were filed and merged within 24 hours.
- **Telegram/WhatsApp improvements welcomed** — New release focused on richer delivery suggests these channels are being actively improved based on user demand.

### Dissatisfaction Signals

- **High bug count remains unaddressed** — Many P1 "platinum hermit" issues have no fix PR yet, indicating maintainer bandwidth is stretched.
- **Automated tooling friction** — `openclaw doctor --fix` failures ([#77802]), plugin update downgrade issues ([#84256]), and startup hangs ([#90886]) point to QA gaps in the update/maintenance toolchain.

---

## 8. Backlog Watch

### Long-Unanswered Important Issues (needs maintainer attention)

| Issue | Age | Severity/Impact | Status |
|-------|-----|-----------------|--------|
| [#45494] | ~94 days | P1 Diamond — cron jobs silently time out during LLM outages | Needs fix PR |
| [#56781] | ~78 days | P2 Diamond — request for compaction fallback chain | **Now addressed by [PR #93125]** |
| [#77802] | ~41 days | P2 Platinum — `doctor --fix` fails atomically | No fix PR; needs product decision |
| [#44395] | ~95 days | P2 Diamond — heading-aware memory chunking | No fix PR; needs product decision |
| [#74077] | ~47 days | P3 — streaming mode slash command | Low priority |
| [#77467] | ~42 days | P1 Diamond — MiniMax OAuth token cannot auto-refresh | No fix PR; needs maintainer review |

### PRs Stuck in Review Loop

| PR | Age | Status | Risk |
|----|-----|--------|------|
| [#85402] | 24 days | Waiting on author | Session state, message delivery |
| [#85359] | 24 days | Waiting on author | Compatibility, security boundary |
| [#81729] | 32 days | Waiting on author | Compatibility, security boundary |
| [#90625] | 10 days | Waiting on author | iOS beta documentation |
| [#93126] | Today | Waiting on author | Test coverage expansion |
| [#93111] | Today | Waiting on author | Doctor fix |

### Notable Maintainer Bottleneck

Multiple "platinum hermit" and "diamond lobster" issues carry the label `clawsweeper:needs-maintainer-review` or `clawsweeper:needs-product-decision`, suggesting the project lacks dedicated triage capacity. This is especially concerning for **session state and message loss** issues, which are existential for a chat-driven AI agent platform.

**Top 5 most critical items needing maintainer eyes (no fix PR, high impact):**
1. [#84516] — Agent replies silently truncated (Platinum)
2. [#85103] — Fallback chain not triggered (Platinum)
3. [#85251] — Codex app-server silent wedges (Platinum)
4. [#84903] — Single stalled session blocks entire event loop (Platinum)
5. [#83184] — Heartbeat delivery stuck (Diamond)

---

## Cross-Ecosystem Comparison

**Cross-Project Comparison Report: Personal AI Agent Open-Source Ecosystem**
**Date:** 2026-06-15

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is currently in a phase of intense, production-driven maturation. Projects are moving beyond experimental feature velocity toward hardening core reliability, session state integrity, and secure agent delegation. The landscape is bifurcating between large, comprehensive frameworks like OpenClaw and IronClaw, which are addressing scale and architectural debt, and smaller, focused projects like NanoBot and PicoClaw, which are refining developer experience and plugin extensibility. A clear trend across all active projects is the prioritization of security—particularly around sandboxing, credential handling, and approval flows—driven by community-led adversarial testing. Additionally, multi-modal and channel expansion (SMS, Matrix, Feishu, Zalo) reflect a growing demand for omnichannel agent deployment.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Today | Health Score (Subjective) | Notes |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | ✅ `v2026.6.8-beta.1` | ⚠️ **Saturated/Strained** | Extremely high volume; massive triage burden; critical P1 bugs open |
| **NanoBot (HKUDS)** | 5 | 44 | ❌ | ✅ **High** | Heavy merge day; systematic refactoring; few regressions |
| **Hermes Agent** | 50 | 50 | ❌ | ⚠️ **Moderate** | Security disclosures; active fix cycles; session isolation issues |
| **PicoClaw** | 5 | 8 | ✅ `nightly v0.2.9` | ✅ **Moderate** | Steady cleanup; low user friction; 3 PRs merged |
| **NanoClaw** | 7 | 11 | ❌ | ✅ **High** | Strong feature velocity; security scrutiny; fix PRs open for critical bugs |
| **NullClaw** | 1 | 0 | ❌ | 🟢 **Low/Stable** | Very low activity; 1 enhancement request |
| **IronClaw** | 38 | 43 | ❌ | ⚠️ **High/Strained** | High velocity; 6 new shell security advisories; feature + security work |
| **LobsterAI** | 2 | 4 | ❌ | 🔴 **Low/Idle** | Stale queue; 2-month-old bugs untouched; 3 unmerged feature PRs |
| **CoPaw** | 15 | 9 | ❌ | ⚠️ **High/Blocked** | 0 merges today; regression cluster; maintainer bottleneck |
| **ZeroClaw** | 42 | 50 | ❌ | ✅ **Very High** | Major consolidation; new SMS providers; quickstart UX fixes |
| **TinyClaw** | 0 | 0 | ❌ | 🟢 **Inactive** | No activity |
| **ZeptoClaw** | 0 | 0 | ❌ | 🟢 **Inactive** | No activity |
| **Moltis** | 1 | 2 | ❌ | 🟢 **Moderate/Low** | Maintenance phase; 1 feature request; no regressions |

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale of Adoption:** OpenClaw's 500+ issues/PRs updated in 24 hours dwarfs all peers. This volume signals a massive user base and an extremely active contributor community.
- **Maturity & Depth:** The project has the most comprehensive feature set, including advanced memory compaction, Codex app-server integration, rich channel delivery (Telegram/WhatsApp), and a plugin observability framework.
- **Rapid Fix Cycles:** Core team merged 75 PRs today, including same-day fixes for `sessions.describe` bugs. When focused, turnaround is fast.

**Technical Approach Differences:**
- OpenClaw uses a monolithic but modular architecture with a strong emphasis on event-loop isolation and session state machine correctness. This contrasts with NanoBot's side-effect-free config refactoring or PicoClaw's lightweight Go-based agent loop.
- Its "platinum hermit" severity rating system is unique and indicates a culture of rigorous triage, but also a fragile system under heavy load.

**Community Size Comparison:**
- OpenClaw's community is the largest and most vocal. Its bug reports are more detailed and adversarial. However, this scale also creates a bottleneck: maintainers are stretched thin, with many critical P1 bugs lacking fix PRs.

**Risk Factor:** If OpenClaw fails to stabilize session reliability (e.g., silent truncation, event loop bricks), it risks losing trust to faster-moving peers like NanoClaw or ZeroClaw, which are deliberately addressing similar use cases with less technical debt.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects:

| Need | Projects Affected | Specific Details |
|---|---|---|
| **Session Reliability & State Integrity** | OpenClaw, Hermes, NanoClaw, ZeroClaw | Silent truncation, stalled sessions, ghost sessions, duplicate messages |
| **Secure Delegation & Approval Flows** | OpenClaw, IronClaw, NanoClaw, ZeroClaw | Approval bypass, hidden MCP args, sandbox escape, shell-risk classification |
| **Fallback Chains / Provider Reliability** | OpenClaw, Hermes, NanoBot | Model fallback not triggering on quota exhaustion; silent provider failures |
| **Configuration Friction / Migration** | OpenClaw, PicoClaw, ZeroClaw, CoPaw | TOML silent drops, security.yml migration breaks, env var confusion |
| **Channel Expansion (SMS, Zalo, Feishu)** | ZeroClaw, CoPaw, NanoBot | Geographic expansion; telephony; enterprise chat |
| **Localization / Regional UX** | CoPaw, LobsterAI | Vietnamese locale, Chinese UI text issues |
| **Edge/IoT / Resource-Constrained Deployment** | Moltis, PicoClaw | Rust-only memory backend, slim Docker images |
| **Dogfooding & AI-Native Engineering** | IronClaw | Using own product for development workflow automation |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | IronClaw | ZeroClaw | NanoBot | CoPaw |
|---|---|---|---|---|---|
| **Target User** | Power users, enterprise | Core team dogfooding, Rust developers | SMB, telephony agents | Developers, low-config | Chinese market, multi-modal |
| **Core Architecture** | Event-loop, session state machine | Rust / Reborn, extension model | WASM plugins, turn engine consolidation | Side-effect-free config, modular | Python/Tauri, computer-use GUI |
| **Key Strength** | Feature depth, community size | Security culture, Rust performance | Provider breadth, SMS | Documentation, refactoring velocity | Localization, multi-agent collab |
| **Key Weakness** | Triage bottleneck, session regressions | Shell security gap, Reborn immaturity | Commit history debt, PR aging | Low issue volume, small team | Regression cluster, 0 merges today |
| **Plugin Model** | MCP + plugin SDK | Product-adapters as extensions | WASM plugins | Builtin tool toggles | Request payload transforms |
| **Security Posture** | Reactive patching | Proactive security audit | Air-gapped RFC, improving | Few disclosures | No active security work reported |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating / High Momentum:**
- **OpenClaw, ZeroClaw, IronClaw, NanoClaw** — These projects are shipping features and fixes at high velocity. They show strong contributor engagement and maintainer responsiveness (though OpenClaw is stretched). All four are addressing security and session reliability as top priorities.

**Tier 2 — Steady / Consolidating:**
- **NanoBot, PicoClaw, Hermes Agent** — Steady merge rates, focused on cleanup and documentation. Hermes has security disclosures but is active. These projects are stabilizing rather than feature-pushing.

**Tier 3 — Low Activity / Stale:**
- **LobsterAI, NullClaw, Moltis, TinyClaw, ZeptoClaw** — Low to zero activity. LobsterAI and NullClaw have unanswered issues from April. These projects risk falling behind unless maintainers re-engage.

**Tier 4 — Inactive:**
- **TinyClaw, ZeptoClaw** — No activity in 24h. Likely dormant or awaiting maintainer attention.

**Maturity Signals:**
- **IronClaw** is using its own product for development (dogfooding) — a sign of production confidence.
- **OpenClaw** and **ZeroClaw** have structured severity rating systems and RFC processes.
- **LobsterAI** is the only project with a primarily Chinese-language issue tracker; English-language projects dominate.

---

## 7. Trend Signals

From cross-project community feedback and bug patterns, the following industry trends are visible for AI agent developers:

1. **Session State is the New Reliability Frontier:** Users are abandoning agents that silently truncate, lose context, or stall mid-turn. Projects that solve session state correctness (OpenClaw's event loop fixes, ZeroClaw's turn engine consolidation) will retain trust.

2. **Security is Shifting From Theoretical to Adversarial:** The IronClaw shell approval bypass disclosures and NanoClaw's MCP hidden-args issues show that community-driven adversarial testing is now the norm. Developers must build risk classification systems that are attack-resilient, not just permissive.

3. **Multi-Provider Fallbacks are Table Stakes:** Users demand automatic model fallback on quota exhaustion, rate limiting, and provider outages. OpenClaw's compaction fallbacks and Hermes' fallback chain discussions signal this is a must-have, not a nice-to-have.

4. **Omnichannel Agents are the New CLI:** The rapid addition of SMS (ZeroClaw), Zalo (CoPaw), Matrix (Hermes), and Feishu (NanoBot) indicates that agents must meet users where they work — in chat apps, enterprise tools, and telephony.

5. **Air-Gapped / Sandboxed Execution is Emerging:** ZeroClaw's air-gapped RFC and PicoClaw's network-egress toggle for Docker terminals reflect a growing demand for running agents in compliance-heavy or security-sensitive environments.

6. **Tool-Call Visibility and Approval UX is a Differentiator:** Users across OpenClaw, ZeroClaw, and IronClaw are frustrated by hidden tool calls, silent approvals, and opaque reasoning. Transparent, per-invocation approval flows are becoming a competitive edge.

7. **AI-Native Engineering Dogfooding is Accelerating:** IronClaw's productivity initiative is a leading indicator: the most advanced agent frameworks will soon be used to build themselves, creating a virtuous cycle of capability and reliability improvements.

---

*Digest prepared from community data as of 2026-06-15. Project health scores are subjective assessments based on activity velocity, bug severity, and maintainer responsiveness.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-15

## Today's Overview

NanoBot saw a surge in development activity today, with 44 pull requests updated in the last 24 hours and 27 merged or closed—indicating a heavy merge day after a week of accumulated PRs. The issue tracker shows modest activity (5 updated), split between 2 open and 3 recently closed bugs. No new releases were published, but the high PR throughput suggests the project is approaching a release-quality milestone. The maintainer team (primarily chengyongru) is driving a broad cleanup and refactoring push across documentation, configuration plumbing, WebUI, and core agent loop boundaries.

## Releases

*No new releases in this reporting period.*

## Project Progress

**27 pull requests were merged or closed today** across several workstreams:

- **Agent & Execution Loop:** PR #4269 adds a no-tools finalization pass when `max_tool_iterations` is exhausted, giving users a concise status message instead of a generic budget notice. PR #4274 scopes recent history prompt injection by session, reducing cross-contamination from cron/dream/heartbeat events in non-unified mode. PR #4299 binds cron automations to concrete origin sessions.

- **Configuration & Tooling:** PR #4275 introduces fast-fail on invalid config files. PR #4273 adds `tools.exec.pathPrepend` for PATH lookup precedence. PR #4138 adds `tools.file.enable` to toggle built-in filesystem tools (matching existing `exec`/`web` patterns). PR #4314 breaks a tool config schema import cycle by extracting a shared `config_base` module.

- **Bug Fixes & Validation:** PR #4312 rejects malformed media attachments in the `message` tool. PR #4311 rejects non-positive file pagination limits. PR #4343 (open) adds `additionalProperties` enforcement to reject unknown builtin tool parameters.

- **Documentation & Onboarding:** PR #4177 reworks documentation entry points for beginner-friendly setup paths. PR #4245 removes old nightly/two-branch contribution guidance and CI branch filters.

- **WebUI & Channels:** PR #4248 fixes token usage heatmap timezone alignment. PR #4339 improves mobile responsiveness (spacing, wrapping, heatmap compaction). PR #4277 lazy-loads the Feishu/lark SDK to avoid heavy imports during channel discovery.

## Community Hot Topics

- **[PR #4344] Refactor config and agent loop boundaries**  
  Author: chengyongru | Status: Open | Updated: 2026-06-14  
  A substantial refactoring PR moving tool config models into side-effect-free modules and extracting narrow AgentLoop coordinators. This is the largest architectural change in the current batch and signals ongoing separation of concerns work.  
  [View PR](https://github.com/HKUDS/nanobot/pull/4344)

- **[PR #4293] fix(agent): add pending_queue to process_direct for subagent result injection**  
  Author: yorkhellen | Status: Open | Updated: 2026-06-15  
  A community-contributed fix for cron jobs and other direct calls that spawn subagents—the runner loop now waits for subagent results mid-turn instead of completing silently. This addresses a long-standing gap in the agent orchestration model.  
  [View PR](https://github.com/HKUDS/nanobot/pull/4293)

- **[PR #4330] feat(webui): add automation management view**  
  Author: chengyongru | Status: Open | Updated: 2026-06-14  
  A significant WebUI feature adding a dedicated automations surface for listing, filtering, running, pausing, and deleting user automations—with localized UI and protected system automation handling.  
  [View PR](https://github.com/HKUDS/nanobot/pull/4330)

## Bugs & Stability

**High Severity:**

1. **Issue #4309** — `/v1/chat/completions` always returns zero usage tokens. The agent loop tracks real usage but the endpoint hardcodes zero. No fix PR linked yet.  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4309)

2. **Issue #4345** — Image-strip fallback (`_strip_image_content`) leaks file paths into the text prompt when images are stripped due to provider errors, causing the model to hallucinate image content it never received. Filed today, no fix yet.  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4345)

**Medium Severity:**

3. **Issue #4333** (Closed) — Anthropic provider sends deprecated `temperature` to opus-4-8/Fable, causing 400 rejections. Fix was merged (likely in this batch of PRs).  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4333)

4. **Issue #4250** (Closed) — Telegram `split_message` breaks fenced code blocks across chunks. Fix merged.  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4250)

**Low Severity:**

5. **Issue #4262** (Closed) — Enhancement to use `botIcon` at agent mode startup instead of default "puppy" icon. Fix merged.  
   [View Issue](https://github.com/HKUDS/nanobot/issues/4262)

**Stability Notes:** PR #4337 (open) fixes ignoring empty injected payloads in the runner, preventing blank user messages from being appended mid-turn.

## Feature Requests & Roadmap Signals

- **Automation Management UI** (PR #4330) — A dedicated WebUI automations surface is in active development and likely to land in the next release, completing the automation lifecycle UX.

- **Tool Parameter Strict Validation** (PR #4343) — Enforcing `additionalProperties: false` on built-in tool schemas signals a move toward stricter runtime validation, reducing silent failures from typos.

- **Session-Bound Automations** (PR #4299, PR #4274) — The pattern of binding cron jobs and history injection to specific sessions (rather than global scope) is emerging as a design principle, likely to continue in future releases.

- **Config Architecture Refactoring** (PR #4344) — Moving tool config models into side-effect-free modules suggests the team is preparing for a cleaner plugin/tool registration API.

## User Feedback Summary

**Pain Points:**
- The OpenAI-compatible endpoint (Issue #4309) returning zero token usage breaks cost tracking for users relying on `/v1/chat/completions`—a core integration point for external tooling.
- Image processing fallback (Issue #4345) leaking file paths and causing hallucinated "sight" is a significant UX and potential privacy issue for users with image-capable models.
- Multiple users reported the Anthropic temperature deprecation breakage (Issue #4333) for the latest Claude models, reflecting friction with continuously evolving provider APIs.
- The Telegram code block splitting (Issue #4250) disrupted developer workflows sharing code via Telegram chat.

**Satisfaction Signals:**
- Documentation improvements (PR #4177) directly address beginner onboarding pain, suggesting the team is responsive to usability complaints.
- The `tools.file.enable` toggle (PR #4138) responds to deployment needs for sandboxed environments that want to restrict filesystem access exclusively to MCP servers.
- Mobile responsiveness improvements (PR #4339) address a growing user base accessing NanoBot via mobile browsers.

## Backlog Watch

- **Issue #4309** (`/v1/chat/completions` zero usage tokens) — Reported June 12, no fix PR yet. This is a significant regression for API consumers. Watch for an incoming fix given today's high merge velocity.

- **Issue #4345** (Image-strip path leak) — Filed today, severity is high due to potential file path exposure. Expect rapid response given the team's current activity level.

- **PR #4293** (Subagent result injection for direct calls) — Open since June 11 with no maintainer merge yet. This is a community contribution addressing a real gap; its age relative to the project's current merge pace suggests it may need review attention.

- **PR #4344** (Config refactor) — The largest architectural PR currently open. No comments yet; given its scope, it may require review time to land safely.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-15

## Today's Overview
Hermes Agent shows **high activity** today with 50 issues and 50 PRs updated in the last 24 hours. The project maintains a strong contributor velocity with 7 issues and 7 PRs closed/merged, indicating active maintenance and bug-fixing cycles. Notable spikes include **security disclosures** around credential exfiltration (Issues #46413, #46411), **critical stability bugs** in Matrix E2EE and Telegram connectivity (Issues #46310, #46298), and **feature requests** spanning desktop UI enhancements and Windows service support. No new releases were published today. The open/closed ratio (43/7 for both issues and PRs) suggests the project is accumulating work-in-progress while making targeted closures.

## Releases
No new releases today.

## Project Progress
**7 PRs closed/merged today** (7 of 50 updated PRs). Key advancements:

- **Bug Fixes**:
  - [#46395](https://github.com/NousResearch/hermes-agent/pull/46395) — Fixed macOS temp/scratch paths falsely flagged as sensitive, unblocking `write_file`/`patch` in temp directories.
  - [#46399](https://github.com/NousResearch/hermes-agent/pull/46399) — `terminal.env_passthrough` now falls back to `.env` file for local backend (mirrors Docker logic).
  - [#46364](https://github.com/NousResearch/hermes-agent/pull/46364) — Windows cron scripts now prefer Git Bash over WSL, fixing script execution on native Windows.
  - [#46305](https://github.com/NousResearch/hermes-agent/pull/46305) — Systemd unit staleness checks now normalize PATH to avoid false "outdated" warnings.

- **Feature Work**:
  - [#46403](https://github.com/NousResearch/hermes-agent/pull/46403) — Kanban tasks can now pin a worker model at creation time.
  - [#46349](https://github.com/NousResearch/hermes-agent/pull/46349) — **New Windows Service backend** for gateway with SCM-managed auto-restart (closes #40899).
  - [#46358](https://github.com/NousResearch/hermes-agent/pull/46358) — Docker terminal sessions can now disable network egress via `terminal.docker_network: false`.

- **Docs/Meta**: [#46352](https://github.com/NousResearch/hermes-agent/pull/46352) added missing `ELEVENLABS_API_KEY` placeholder to `.env.example`.

## Community Hot Topics

### Most Active Issues (by comments + reactions)

1. **[#7237](https://github.com/NousResearch/hermes-agent/issues/7237) — "Response truncated due to output length limit"** (46 comments, 6 👍)
   - **Status**: CLOSED. Long-standing bug where CLI/chat responses are truncated mid-stream.
   - **Analysis**: This was a high-traffic issue; its closure suggests a fix is in place for output length limits. Community relief likely.

2. **[#45058](https://github.com/NousResearch/hermes-agent/issues/45058) — "web_search/web_extract silently routes to Parallel.ai without user opt-in"** (7 comments, 14 👍)
   - **Status**: CLOSED. Privacy concern where unconfigured web tools silently switch to Parallel.ai backend.
   - **Analysis**: Strong community reaction (14 reactions) indicates privacy is a pain point. The fix likely adds explicit opt-in or fallback behavior.

3. **[#38963](https://github.com/NousResearch/hermes-agent/issues/38963) — "hermes desktop strat fail, it say no git???"** (8 comments)
   - **Status**: CLOSED. Windows desktop installer fails due to missing git detection.
   - **Analysis**: New-user onboarding friction on Windows; closure suggests a fix or documentation improvement.

4. **[#43083](https://github.com/NousResearch/hermes-agent/issues/43083) — "Passwords get replaced by *** but model reads back its own conversation history and fails"** (7 comments)
   - **Status**: OPEN, P1 priority. Credential redaction breaks tool calls when model sees redacted history.
   - **Analysis**: A critical UX bug—users' workflows fail silently due to over-zealous redaction logic.

### Most Active PRs

- **[#46415](https://github.com/NousResearch/hermes-agent/pull/46415)** — Google Workspace setup flags implementation (new today).
- **[#46348](https://github.com/NousResearch/hermes-agent/pull/46348)** — Fixes memory toolset injection when `disabled_toolsets=['memory']` is set.
- **[#46404](https://github.com/NousResearch/hermes-agent/pull/46404)** — Telegram connect timeout fix (P1, linked to #46298).
- **[#46407](https://github.com/NousResearch/hermes-agent/pull/46407)** — Matrix E2EE re-init storm fix (P1, linked to #46310).

## Bugs & Stability

### Critical (P1)

- **[#46310](https://github.com/NousResearch/hermes-agent/issues/46310)** — Matrix media sends exhaust recipient one-time keys per message, dropping messages under burst. **Fix PR [#46407](https://github.com/NousResearch/hermes-agent/pull/46407) open**.
- **[#46298](https://github.com/NousResearch/hermes-agent/issues/46298)** — Telegram adapter connect timeout; **Fix PR [#46404](https://github.com/NousResearch/hermes-agent/pull/46404) open**.
- **[#43083](https://github.com/NousResearch/hermes-agent/issues/43083)** — Password redaction breaks tool call history (OPEN, P1).

### High (P2)

- **[#45519](https://github.com/NousResearch/hermes-agent/issues/45519)** — GLM-5.2 context window misdetected as 202K (actually 1M), causing premature compression (CLOSED).
- **[#46303](https://github.com/NousResearch/hermes-agent/issues/46303)** — Concurrent sessions cross-contaminate memory and git state (OPEN, P2).
- **[#46332](https://github.com/NousResearch/hermes-agent/issues/46332)** — Windows cron scripts fail due to WSL vs Git Bash conflict; **Fix PR [#46364](https://github.com/NousResearch/hermes-agent/pull/46364) merged**.
- **[#45963](https://github.com/NousResearch/hermes-agent/issues/45963)** — Docker profile creation spawns zombie gateways (CLOSED).
- **[#44560](https://github.com/NousResearch/hermes-agent/issues/44560)** — `model.options` handler blocks on slow providers, causing WebSocket timeouts (OPEN, P2).

### Medium (P3)

- **[#40480](https://github.com/NousResearch/hermes-agent/issues/40480)** — Custom provider models missing from Desktop dropdown (OPEN).
- **[#42651](https://github.com/NousResearch/hermes-agent/issues/42651)** — Desktop shows cron jobs from other profiles (OPEN).
- **[#46131](https://github.com/NousResearch/hermes-agent/issues/46131)** — Ollama reasoning models return empty content (OPEN, P3).
- **[#46090](https://github.com/NousResearch/hermes-agent/issues/46090)** — Agent becomes extremely slow for basic tasks; user reports "hours for nothing" (OPEN, needs-repro).
- **[#46265](https://github.com/NousResearch/hermes-agent/issues/46265)** — SimpleX adapter drops DM replies due to contact ID parsing bug (OPEN, P3).

### Security Noteworthy

- **[#46413](https://github.com/NousResearch/hermes-agent/issues/46413)** — Desktop file preview can read Hermes credential stores (OPEN, filed today).
- **[#46411](https://github.com/NousResearch/hermes-agent/issues/46411)** — `read_file` can exfiltrate credential stores from sibling profiles (OPEN, filed today).

### Stability Observations
The project is addressing **concurrency and session isolation** issues (cross-contamination, zombie gateways, E2EE storms), suggesting horizontal scaling is stressing the current architecture. Two new security disclosures are concerning—both involve credential access through legitimate features.

## Feature Requests & Roadmap Signals

### High Community Interest

- **Desktop UI Usability** ([#44140](https://github.com/NousResearch/hermes-agent/issues/44140), 3 comments, 3 👍) — Auto-scroll, sidebar overlap fix, custom session groups. Likely to land soon given multiple Desktop-related PRs.
- **Session Merge** ([#44757](https://github.com/NousResearch/hermes-agent/issues/44757), 1 comment, 1 👍) — Combine session transcripts to preserve context across sessions. Moderate complexity.
- **AI Session Summaries** ([#45103](https://github.com/NousResearch/hermes-agent/issues/45103), 2 comments, 1 👍) — Hover card summaries for desktop sidebar. Draft PR promised.

### Implementation Signals (Likely in Next Release)

1. **Windows Service Backend** — PR [#46349](https://github.com/NousResearch/hermes-agent/pull/46349) is near-complete. High likelihood for v0.17.
2. **Kanban Worker Model Override** — PR [#46403](https://github.com/NousResearch/hermes-agent/pull/46403) landed today.
3. **Kept Base URL Option** ([#46192](https://github.com/NousResearch/hermes-agent/issues/46192)) — Small config enhancement, 4 comments, trivial to implement.
4. **GBrain Memory Provider Plugin** ([#46253](https://github.com/NousResearch/hermes-agent/issues/46253)) — Community-built integration with existing tooling; could land as plugin.
5. **Hide Unconfigured Providers** ([#46304](https://github.com/NousResearch/hermes-agent/issues/46304)) — Simple config toggle for cleaner UI.
6. **Uninstall Dry-Run Mode** ([#46359](https://github.com/NousResearch/hermes-agent/pull/46359)) — Ready for merge.

### Long-Term Signals

- **Hermes Workspace Integration** ([#41553](https://github.com/NousResearch/hermes-agent/issues/41553)) — Official desktop plugin system for community workspaces.
- **Configurable Fallback Stickiness** ([#23094](https://github.com/NousResearch/hermes-agent/issues/23094)) — Fine-tuning fallback behavior.
- **Configurable TUI Status Bar** ([#13490](https://github.com/NousResearch/hermes-agent/issues/13490)) — Theming and field customization.

## User Feedback Summary

### Pain Points (High Frequency)

1. **Output Truncation**: Issue #7237 dominated discussion (46 comments). Users frustrated by mid-stream cutoffs. Now closed—watch for regressions.
2. **Privacy & Security**: Strong reaction to #45058 (14 👍) shows users are vigilant about silent backend routing and data exfiltration.
3. **Onboarding Friction**: Windows (no git, #38963) and missing provider models in Desktop (#40480) frustrate new users.
4. **Session Reliability**: Cross-contamination (#46303), zombie gateways (#45963), and slow agents (#46090) degrade trust in multi-session workflows.

### Use Cases Expressed

- **Docker-based deployments**: Profile management, gateway resurrection bugs, network isolation.
- **Windows users**: Cron scripts, git detection, service management.
- **Enterprise/team use**: Multi-profile isolation, credential security, session merging.
- **Plugin/memory ecosystem**: GBrain integration, memory tool injection control, custom memory backends.

### Satisfaction/Dissatisfaction Indicators

- **Positive**: Community members offering to implement features themselves (e.g., [#45103](https://github.com/NousResearch/hermes-agent/issues/45103) "I'd like to implement this myself").
- **Frustrated**: "literally hours for nothing" (Issue #46090), "no way to disconnect" accounts (Issue #45865).
- **Vigilant**: Security researchers filing detailed disclosures ([#46413](https://github.com/NousResearch/hermes-agent/issues/46413), [#46411](https://github.com/NousResearch/hermes-agent/issues/46411))—community cares about credential safety.

## Backlog Watch

### Issues Needing Maintainer Attention

1. **[#40480](https://github.com/NousResearch/hermes-agent/issues/40480)** — Custom provider models not shown in Desktop (OPEN since June 6). No PR linked. Desktop integration of custom providers appears to be a blind spot.
2. **[#42651](https://github.com/NousResearch/hermes-agent/issues/42651)** — Desktop shows all profiles' cron jobs (OPEN since June 9). Profile-scoped UI isolation needed.
3. **[#46090](https://github.com/NousResearch/hermes-agent/issues/46090)** — Agent becomes "extremely slow" (OPEN, needs-repro). User left without resolution; may indicate memory leak or context growth issue.
4. **[#23094](https://github.com/NousResearch/hermes-agent/issues/23094)** — Configurable fallback stickiness (OPEN since May 10). Low priority but discussed for weeks.
5. **[#13490](https://github.com/NousResearch/hermes-agent/issues/13490)** — Configurable TUI status bar (OPEN since April 21). No movement.

### PRs Needing Review

- **[#46415](https://github.com/NousResearch/hermes-agent/pull/46415)** — Google Workspace setup flags (filed today, awaiting review).
- **[#46348](https://github.com/NousResearch/hermes-agent/pull/46348)** — Memory toolset injection fix (filed yesterday, no activity yet).
- **[#46398](https://github.com/NousResearch/hermes-agent/pull/46398)** — Kanban dashboard API without multipart (filed today).

### Risk: Security Disclosures Without Fixes

**[#46413](https://github.com/NousResearch/hermes-agent/issues/46413)** and **[#46411](https://github.com/NousResearch/hermes-agent/issues/46411)** are both filed today and have **no linked PRs**. Given the sensitivity (credential exfiltration), these should be addressed urgently.

---

*Digest generated 2026-06-15. Data source: GitHub NousResearch/hermes-agent.*

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-15

## 1. Today's Overview
Project activity is **moderate** with a healthy PR-to-issue ratio. 8 pull requests were updated in the last 24 hours (5 merged/closed), and 5 issues saw updates (1 closed). A new nightly build **v0.2.9-nightly.20260615** was released, continuing the project's automated delivery cadence. The maintainer team appears actively addressing code quality and bug fixes, with three contiguous cleanup PRs landing today alone. No critical regressions or security issues were surfaced.

## 2. Releases
**nightly — Nightly Build v0.2.9-nightly.20260615.13a38bd1**
- Automated build; marked as potentially unstable.
- Changelog: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **No breaking changes or migration notes** — this is a standard nightly snapshot from `main`.

## 3. Project Progress
Five PRs were merged or closed today, indicating steady forward momentum:

| PR | Change | Impact |
|----|--------|--------|
| [#2904](https://github.com/sipeed/picoclaw/pull/2904) | Fix agent loop reload and panic cleanup stability | Core agent reliability: removes goroutine leak on reload, adds synchronous recover flow |
| [#3121](https://github.com/sipeed/picoclaw/pull/3121) | Refactor `log.Printf` → structured logger in `openai_compat` | Code modernization; eliminates last raw `log` usage in provider |
| [#3122](https://github.com/sipeed/picoclaw/pull/3122) | Capture `Close()` error in `appendJSONLRecords` | Prevents silent data loss on write failures (disk full, NFS errors) |
| [#3123](https://github.com/sipeed/picoclaw/pull/3123) | Explicitly ignore `Close()` error on directory fd | Code clarity only; no functional change |
| [#3124](https://github.com/sipeed/picoclaw/pull/3124) | Handle `io.ReadAll` error in TTS error response path | Prevents silently degraded diagnostic messages when TTS API returns non-200 |

**Notable:** Two new open PRs were submitted:
- [#3118](https://github.com/sipeed/picoclaw/pull/3118) — Adds **remote Pico WebSocket mode** to the agent command (author: jp39)
- [#3120](https://github.com/sipeed/picoclaw/pull/3120) — Adds `RegisterChannelSettings` hook for out-of-tree channels, enabling third-party channel plugins without forking PicoClaw

## 4. Community Hot Topics
| Thread | Activity | Summary |
|--------|----------|---------|
| [#2978](https://github.com/sipeed/picoclaw/issues/2978) [CLOSED] | 2 comments | User requested adding **OmniRoute** as a provider. Closed as stale; no indication of implementation |
| [#3044](https://github.com/sipeed/picoclaw/issues/3044) [OPEN] | 1 comment | `allow_from` filter broken for Matrix user IDs containing colons (e.g., `@localpart:domain`) — messages silently rejected |
| [#3041](https://github.com/sipeed/picoclaw/issues/3041) [OPEN] | 1 comment | `mcp add` mis-parses global flags (`--no-color`) into positional arguments, breaking HTTP/SSE server registration |
| [#3090](https://github.com/sipeed/picoclaw/issues/3090) [OPEN] | 1 comment | **Panel** completely non-functional on Safari < iOS 16.4 |
| [#3125](https://github.com/sipeed/picoclaw/issues/3125) [OPEN] | 0 comments | `web_search` tool (Brave API) fails silently after migration to `.security.yml` — returns `"No results"` for any query |

**Underlying needs:** Users are hitting real friction with the new security config migration (#3125) and the global flags refactoring (#3041). The Matrix integration has a protocol-level bug (#3044) that makes the feature effectively unusable for standard user IDs. No issue has more than 2 comments, indicating that these are early reports without broad community discussion yet.

## 5. Bugs & Stability
**High severity:**
- **[#3125](https://github.com/sipeed/picoclaw/issues/3125)** — `web_search` silent failure with Brave API after `.security.yml` migration. **No fix PR exists.** LLM calls the tool correctly but backend returns null results. Critical for any deployment relying on web search.

**Medium severity:**
- **[#3044](https://github.com/sipeed/picoclaw/issues/3044)** — Matrix `allow_from` broken for standard user IDs containing colons. Protocol-level bug; messages silently dropped. **No fix PR.**
- **[#3041](https://github.com/sipeed/picoclaw/issues/3041)** — `mcp add` mis-parses global flags into positional arguments, breaking HTTP/SSE MCP server registration. **No fix PR.**
- **[#3090](https://github.com/sipeed/picoclaw/issues/3090)** — Panel unusable on Safari < iOS 16.4. Likely a CSS/JS compatibility issue. **No fix PR.**

**Low severity / already fixed:**
- TTS error path silent degradation — fixed in [#3124](https://github.com/sipeed/picoclaw/pull/3124)
- `appendJSONLRecords` silent write failure — fixed in [#3122](https://github.com/sipeed/picoclaw/pull/3122)

## 6. Feature Requests & Roadmap Signals
| Request | Signal |
|---------|--------|
| **[#2978](https://github.com/sipeed/picoclaw/issues/2978)** — Add OmniRoute as provider | Closed as stale; unlikely to be prioritized |
| **[#3118](https://github.com/sipeed/picoclaw/pull/3118)** — Remote Pico WebSocket mode for agent | Open PR with implementation; **likely for next stable release** |
| **[#3120](https://github.com/sipeed/picoclaw/pull/3120)** — Out-of-tree channel registration hook | Open PR; enables plugin ecosystem without forking — **high roadmap signal** |
| **[#2975](https://github.com/sipeed/picoclaw/pull/2975)** [stale] — Telegram reply-as-mention in group chats | Open PR stalled since 2026-05-30; maintainer review needed |

**Prediction:** The **out-of-tree channels** feature (#3120) aligns with PicoClaw's extensibility philosophy and is the most likely to land in the next minor version. Remote WebSocket mode (#3118) is also well-coded and may be merged soon.

## 7. User Feedback Summary
**Pain points:**
- Configuration migration to `.security.yml` broke the `web_search` tool without any error message (#3125) — frustrating for users who rely on Brave search
- Matrix users cannot use `allow_from` filtering due to a colon parsing bug (#3044) — effectively breaks access control for Matrix channels
- Safari/iOS users (especially on older devices) cannot access the Panel at all (#3090)
- The `mcp add` CLI UX regression (#3041) impacts users who invoke global flags before subcommands

**Satisfaction signals:**
- Community continues to submit well-structured PRs with thorough descriptions and verification steps
- The merger of three cleanup PRs from a single author (chengzhichao-xydt) suggests engaged external contributors
- No complaints about the core agent loop, LLM integration, or provider quality

## 8. Backlog Watch
| Item | Age | Priority |
|------|-----|----------|
| [#2975](https://github.com/sipeed/picoclaw/pull/2975) — Telegram reply-as-mention | 16 days | Medium — clean feature, awaiting review |
| [#2904](https://github.com/sipeed/picoclaw/pull/2904) — Agent loop stability fix | 26 days | **High** — was merged today, but took 25 days to resolve |
| [#2978](https://github.com/sipeed/picoclaw/issues/2978) — OmniRoute provider request | 15 days | Low — closed as stale |
| [#3044](https://github.com/sipeed/picoclaw/issues/3044) — Matrix `allow_from` bug | 8 days | **High** — protocol-level bug, no fix in sight |
| [#3041](https://github.com/sipeed/picoclaw/issues/3041) — `mcp add` flag parsing bug | 8 days | **High** — breaks MCP SSE/HTTP setup |
| [#3125](https://github.com/sipeed/picoclaw/issues/3125) — Brave search silent failure | 1 day | **Critical** — just reported, needs immediate triage |

**Maintainer attention needed:** Issues #3125, #3044, and #3041 represent real breakage in shipped features. No maintainer responses have been posted on any of these threads yet. The stale PR #2975 (Telegram feature) has been waiting for review for over two weeks.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-15

## Today's Overview

NanoClaw is in a period of high-velocity development, with **11 PRs updated** and **7 issues active** in the past 24 hours. The project shows a strong focus on **security hardening** (three new security advisories filed today), **provider architecture expansion** (Codex integration and operator-driven provider switching), and **stability fixes** for budget handling and database recovery. Five PRs were merged/closed today alongside six open PRs under active review. No new releases were published, but the trunk is accumulating significant feature and fix payloads.

## Releases

**None** — No new releases were published today. The last release date is not available in this snapshot.

## Project Progress

Five PRs were merged or closed today, signaling progress across documentation, infrastructure, and platform extensibility:

- **#2764** (closed) — *docs(CLAUDE.md): fix two relocated Key Files paths* — Corrects stale path references in the project's guiding documentation, improving developer and AI-assistant onboarding.
- **#2769** (closed) — *docs(add-codex): flag interactive auth step + add host-restart step* — Documentation fix for the Codex setup skill, preventing agent stalls during authentication.
- **#2757** (closed) — *feat(codex): Codex agent-provider payload v2 — app-server on capability seams, vault-only auth* — Major payload upgrade turning Codex into a full agent provider with vault-only authentication through OneCLI.
- **#2756** (closed) — *feat(providers): operator-driven provider selection, switching, and memory migration* — Introduces a provider registry, setup picker, installer, vault auth walkthrough, and memory-migration skill to the trunk.
- **#2758** (closed) — *feat(container): data-drive global CLI installs from cli-tools.json* — Replaces hardcoded Dockerfile CLI tool installation with a data-driven manifest pattern for easier extensibility.

**Open PRs advancing key work:**
- **#2770** (open) — Codex image event delivery fix (build-breaking issue)
- **#2759** (open) — Fix for silent budget-exhausted turn drops
- **#2750** (open) — Stale database journal recovery after container kills
- **#2732** (open) — Security hardening from multi-agent health audit

## Community Hot Topics

No single issue or PR has attracted significant comment threads or reactions (all issues show 0 comments and 0 👍). However, the **three security advisories filed by YLChen-007** represent the most substantive community engagement:

- **#2762** — *[Security] NanoClaw `add_mcp_server` approval flow allows hidden `args` and `env` to be approved and persisted without being shown to the approver* — Highlights a privilege escalation vector where an attacker-controlled agent can hide MCP server configuration details during approval.
- **#2761** — *[Security] Local gateway approval bypass via unauthenticated loopback webhook* — Describes an authentication gap that could allow local attackers to bypass approval gates.
- **#2760** — *[Security] Arbitrary local file exfiltration via `send_file` absolute path handling* — Reports insufficient path constraint on file read operations.

**Underlying need**: The security issues collectively signal that NanoClaw's agent-self-modification and MCP tooling trust model is being stress-tested as the project adds more autonomous capabilities. The community is effectively performing adversarial review of the approval and sandboxing layers.

## Bugs & Stability

**High-severity (critical):**
- **#2751** — *Budget-exhausted LLM turns are silently dropped* — Users receive no reply when token/spend budgets are exhausted. **Fix PR #2759 exists** and is open, indicating maintainers are actively addressing this.
- **#2760** — *Arbitrary local file exfiltration via send_file* — Security vulnerability allowing outbound file reads on any absolute path. No fix PR yet observed.
- **#2761** — *Local gateway approval bypass via unauthenticated loopback webhook* — Authentication gap in webhook-based approval flow. No fix PR yet observed.
- **#2762** — *Hidden args/env in MCP server approval flow* — Privilege escalation via approval UI blind spots. No fix PR yet observed.

**Medium-severity:**
- **#2767** — *Telegram legacy-Markdown sanitizer obsoleted by upstream fix* — Code duplication issue now that `@chat-adapter/telegram@4.30.0` supports native MarkdownV2. Low impact, code cleanup opportunity.
- **#2516 / #2640** — *Stale outbound.db journals after container kills* — Data durability issue. **Fix PR #2750 exists** and is open.

**Low-severity:**
- **#2763** (closed) — *docs(CLAUDE.md): Key Files table points at two relocated files* — Documentation stale path issue, already fixed in PR #2764.

## Feature Requests & Roadmap Signals

**Active features nearing integration:**
- **Codex as a full agent provider** (PR #2757, merged) — A major architectural addition, positioning Codex alongside existing providers with vault-only auth and host capability seams.
- **Operator-driven provider selection** (PR #2756, merged) — Users will gain explicit control over which agent provider(s) are active, with memory migration between providers.
- **Data-driven CLI tooling** (PR #2758, merged) — A platform-composability improvement where skills register CLI dependencies via a JSON manifest.

**User-requested / community-predicted next features:**
- **Prompt caching for Claude provider** (#2768) — Request to `enablePromptCaching` by default to reduce costs and latency on long-running agent sessions. Likely to land as a small provider fix in the next release.
- **Telegram MarkdownV2 native support** (#2767) — Once resolved, the legacy sanitizer can be removed, simplifying the Telegram channel code.
- **Budget exhaustion user notifications** (#2751, fix #2759) — Feature-adjacent fix; expect a user-facing error message pattern to be adopted in the provider error handling.

## User Feedback Summary

**Pain points identified:**
1. **Silent failures on budget exhaustion** (#2751) — Users are confused when agents stop responding without explanation. The fix is already in progress.
2. **Stale documentation paths** (#2763) — AI coding assistants and human developers hit dead ends when following the "Key Files" table. Already fixed.
3. **Codex authentication stalls** (#2769) — During setup, agents hang waiting for interactive auth without a TTY. Documentation fix incoming.
4. **Security trust model concerns** (#2760–2762) — Sophisticated users (likely security researchers) are probing the self-modification and approval flows, indicating concern about running autonomous agents with tool access.

**Satisfaction signals:** The quick turnaround on merging fixes (PR #2764 for the docs path issue, PR #2769 for Codex auth docs) suggests maintainers are responsive. The volume of feature work (providers, Codex, container improvements) shows active investment.

## Backlog Watch

No items in this snapshot appear to be long-ignored, but the following warrant attention:

- **#2750** (open since 2026-06-12) — *Fix: recover stale outbound.db journals* — A complex fix addressing multiple related issues (#2516, #2640). It has been open for 3 days with no recent activity. Maintainers should prioritize review as it affects data durability.
- **#2732** (open since 2026-06-11) — *Harden host + agent-runner from health audit findings* — A 19-file security hardening PR from an audit. It has been open for 4 days. Given the three new security issues filed today (#2760–2762), merging or providing an update on this PR would signal that the audit findings are being addressed.
- **Three security issues (#2760, #2761, #2762)** — Filed yesterday with no fix PRs yet. While not "long-unanswered" by time, their severity (security vulnerabilities) makes them high-priority for triage and response.

---

**Overall Health: Active development cycle with strong feature velocity. Security posture is under community scrutiny — a healthy sign for a project handling autonomous agent execution. The maintainers are merging PRs at a healthy cadence and have fix PRs open for the most critical user-facing bug (budget exhaustion). Next release will likely include Codex v2, provider switching, and critical fixes for budget handling and database recovery.**

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for June 15, 2026.

---

## NullClaw Project Digest: 2026-06-15

### 1. Today's Overview
Project activity remains very low. Over the last 24 hours, there were no merged Pull Requests, no new releases, and only a single new Issue opened. The project appears to be in a quiet maintenance phase, with the community relying primarily on the existing feature set. The only update today reflects a specific enhancement request from a user, rather than internal development progress.

### 2. Releases
**None.** No new releases were published today, nor have any been recorded in the recent past. Users are likely still running the latest stable version from a prior release cycle.

### 3. Project Progress
**No progress today.** There were no Pull Requests updated (open, merged, or closed) in the last 24 hours. No features were advanced, and no fixes were committed.

### 4. Community Hot Topics
**1 Active Issue (No Comments/Reactions)**
- **#955 [OPEN] [enhancement] Identity based authentication support for Azure OpenAI LLM Provider**
  - *Author:* kunalk16 | *Updated:* 2026-06-15
  - *Link:* [Issue #955](https://github.com/nullclaw/nullclaw/issues/955)
  - *Analysis:* This is the only item updated in the last 24 hours. The underlying need is for enterprises that enforce strict security policies (AAD-managed identities, policy restrictions on API keys) within Azure subscriptions. The user is requesting support for `DefaultTokenCredential` to allow agents to authenticate using the developer’s Azure CLI login context. This suggests a growing demand for enterprise-grade, keyless authentication in the Azure OpenAI integration.

### 5. Bugs & Stability
**No bugs reported today.** The absence of bug reports or crash-related issues suggests the current stable release is performing reliably for the existing user base, or that the user base is currently inactive.

### 6. Feature Requests & Roadmap Signals
**1 Active Request**
- **Issue #955 – Identity based authentication for Azure OpenAI LLM Provider**
  - *Signal:* This request is likely to gain traction if Project NullClaw targets enterprise users. Given the policy-driven shift in Azure toward managed identities, supporting `DefaultTokenCredential` is a natural evolution for the LLM provider layer. If the maintainer prioritizes compliance and enterprise adoption, this feature is a strong candidate for the next minor release.

### 7. User Feedback Summary
- **Pain Point:** One user is explicitly blocked by organizational security policies that prevent the use of API keys for Azure OpenAI. They are currently unable to use the project in their environment.
- **Use Case:** Enterprise deployment of AI agents within Azure ecosystems where conditional access policies and managed identity requirements are enforced.
- **Satisfaction/Dissatisfaction:** No indicators of dissatisfaction with existing features were detected. The user submitting the request was polite and constructive, indicating a desire to continue using NullClaw rather than switching to a competitor.

### 8. Backlog Watch
**No critical backlog items require immediate attention.** There are no long-standing, unanswered Issues or stale Pull Requests in the current data window. The project backlog appears clean, which may indicate either good maintenance hygiene or a very low volume of incoming contributions.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-15

## Today's Overview

IronClaw shows very high development velocity today with 38 issues and 43 PRs updated in the last 24 hours, indicating intense engineering activity. The project is mid-cycle with no new releases, suggesting a focus on feature work and security hardening before the next version cut. A significant cluster of shell security advisories (6 issues) filed by YLChen-007 dominates the security landscape, while the core team continues advancing the Reborn architecture with runtime context, attachment support, and workflow automation. The project also launched a major productivity initiative (#4878) aiming to make the team AI-native by using IronClaw itself to accelerate its own development. Overall project health is strong but under strain from both feature velocity and security disclosure volume.

## Releases

No new releases in the last 24 hours. The pending release PR #3708 (`ironclaw: 0.24.0 -> 0.29.1`) remains open with breaking changes in `ironclaw_common` (0.4.2 -> 0.5.0) and `ironclaw_skills` (0.3.0 -> 0.4.0).

## Project Progress

17 PRs were merged or closed today, reflecting significant throughput:

**Merged/Closed PRs:**
- **#4873** (henrypark133, core) — Re-homed the approval→auth→final-reply Slack delivery e2e test that was born-broken in PR #4839; closes #4847
- **#4844** (henrypark133, core) — Fixed Slack gate route filtering to use raw gate string comparison instead of closure-based matching, eliminating per-route allocation bugs
- **#4836** (henrypark133, core) — **[Merged]** Implemented runtime-context slice that surfaces connected channels, delivery state, and run origin to the model; closes #4828
- **#4738** (ilblackdragon, core) — **[Merged]** Wired attachment upload UX into Reborn WebChat v2 SPA; closes #4644

**Key features that advanced:**
- Runtime context now communicates channel connectivity and delivery targets to the model (PR #4836 merged)
- Attachment pipeline progressed with image support for vision-capable models (PR #4871 opened)
- Slack integration moved toward product-adapter extension model (PR #4778)
- Run-borking terminal errors being addressed with failure explanation and retryable runs (PR #4841)

## Community Hot Topics

**Most Active Issues:**
- **#4851** (CLOSED, henrypark133) — Trusted-trigger origin laundering through adapter_kind string; thread classification as a type (Option 7). 1 comment. Core team identifying and patching architectural trust issues in the trigger pipeline. [Link](https://github.com/nearai/ironclaw/issues/4851)
- **#4848** (CLOSED, henrypark133) — Auth-resume matching by per-invocation identity (input_ref), not just capability_id. Fixes slot-reuse bug where auth-resumes could match wrong invocations. [Link](https://github.com/nearai/ironclaw/issues/4848)
- **#4644** (OPEN, ilblackdragon) — Universal attachments across channels: wiring v1 pipeline into Reborn + extensible format registry + polished web UX. This large-scope enhancement is the parent of multiple sub-tasks now actively tracked. [Link](https://github.com/nearai/ironclaw/issues/4644)

**Most Active PRs:**
- **#4791** (hanakannzashi, OPEN) — Fixes code block overflow in WebUI, keeping overflow local to code blocks. Low-risk, design-focused fix for chat readability. [Link](https://github.com/nearai/ironclaw/pull/4791)
- **#4778** (serrrfirat, OPEN) — Representing Slack as a product-adapter extension, removing from hardcoded built-in channel list. Architectural shift toward extensibility. [Link](https://github.com/nearai/ironclaw/pull/4778)
- **#4838** (henrypark133, OPEN) — Explicit gate-open feedback for busy threads: replaces defer-and-drain with direct rejection + notice. User is the retry actor. [Link](https://github.com/nearai/ironclaw/pull/4838)

**Underlying needs:** The community is driving toward architectural purity (type-safe triggers, per-invocation identity, extensible channels) while also pushing for concrete UX improvements (attachment support, mobile responsiveness, clearer error feedback).

## Bugs & Stability

**Critical Security Issues (6 new advisories today):**

| Issue | Title | Status | Fix PR |
|-------|-------|--------|--------|
| #4865 | Shell approval boundary bypass via transparent `env /bin/sh -c` wrapper | OPEN | None yet |
| #4864 | Shell approval wrapper bypass allows high-risk commands to inherit prior auto-approval | OPEN | None yet |
| #4863 | High-risk shell approval bypass via transparent `env`/shell wrappers after auto-approval | OPEN | None yet |
| #4862 | Shell tool approval bypass via GNU `sort --compress-program` | OPEN | None yet |
| #4861 | Approval bypass in shell tool risk classification allows newline-chained destructive commands | OPEN | None yet |
| #4797 | `write_file` sandbox escape through dangling final symlink | OPEN | None yet |

**Explanation:** All filed by YLChen-007, these represent a coordinated security audit of the `shell` tool's risk classification system. The core vulnerability pattern is that risk classification relies on prefix/command matching that can be evaded through shell wrappers (`env`, `/bin/sh -c`), GNU tool delegation (`sort --compress-program`), or newline chaining. These are high-severity because they allow destructive commands to bypass the intended approval floor.

**Other significant bugs reported today:**

- **#4884** (OPEN, sunglow666) — Reborn Google Calendar auth prompt incorrectly requests access token instead of guiding through OAuth flow. Severity: Medium (blocks extension usability). [Link](https://github.com/nearai/ironclaw/issues/4884)
- **#4874** (OPEN, cuongdcdev) — WebChat v2 chat send fails with "Illegal invocation" when accessed over plain HTTP from non-localhost host. Severity: Medium (blocks non-local testing). [Link](https://github.com/nearai/ironclaw/issues/4874)
- **#4870** (OPEN, krishna-505) — Reborn WebUI WebSocket helper conflicts with v2 auth contract: `openEventSocket()` uses `?token=` but v2 auth explicitly rejects query-token auth on WebSocket routes. Severity: Medium. [Link](https://github.com/nearai/ironclaw/issues/4870)
- **#4852** (OPEN, sunglow666) — Reborn shell command not visible in approval dialog or Activity history. Severity: Medium (usability/trust gap). [Link](https://github.com/nearai/ironclaw/issues/4852)
- **#4857** (OPEN, sunglow666) — Clean state incorrectly shows NEAR AI provider as ACTIVE in Settings when no provider configured. Severity: Low (misleading UI). [Link](https://github.com/nearai/ironclaw/issues/4857)
- **#4868** (OPEN, krishna-505) — Settings provider actions clip offscreen on mobile viewport. Severity: Low (mobile UX). [Link](https://github.com/nearai/ironclaw/issues/4868)

**Previously reported bug with fix:** #4751 (Large response fails with provider tool arguments exceed 16384 bytes) was CLOSED, likely fixed.

## Feature Requests & Roadmap Signals

**Engineering Productivity Initiative (NEW — #4878):**
think-in-universe launched a meta-initiative to make the IronClaw team AI-native by using IronClaw itself for planning, implementation, review, testing, security, and collaboration. Sub-tasks created today:
- **#4882** — Build Coding Agent Cloud Workflow: assign issues to a bot for automated PR creation
- **#4881** — Add Preview Deployments for IronClaw PRs (Vercel-like experience)
- **#4880** — Automate Code Review and Review Comment Resolution
- **#4883** — Improve Test Coverage Tracking and Regression Protection

**Prediction for next version:** This initiative signals that IronClaw's own team will dogfood coding agent workflows, likely accelerating the Reborn coding agent features. Expect preview deployments and AI review automation in the next 1-2 releases.

**Reborn Feature Progression:**
- **#4644** (attachments) — Progressing well with both backend (#4677) and frontend (#4738) merged; vision support (#4871) just opened
- **#4875** — Split runtime_context.rs (1025 lines) into separate modules for data model, prompt rendering, and fetch contract
- **#4877** — Wire communication-context provider for Production runtime profile (currently only local-dev)

**Product-Adapters as Extensions:**
PR #4778 signals a roadmap shift: Slack is being refactored from a hardcoded built-in channel to a host-bundled Reborn extension. This pattern enables third-party channel development.

## User Feedback Summary

**Pain Points from Dogfooding (#4692, #4879):**
- think-in-universe's dogfooding logs (week of 06/08 and new week 06/15) capture first-run usability issues including configuration friction, model-provider setup confusion, and startup problems. These tracking issues aggregate real user frustration from daily use.
- **#4884** (Google Calendar OAuth) — Users are hitting authentication flows that don't match expected UX patterns, suggesting the OAuth integration layer needs refinement.

**Positive Signals:**
- The team is actively dogfooding their own product (competitive advantage for quality)
- Multiple PRs show careful attention to UX detail (code block overflow #4791, mobile layout #4868)
- The productivity initiative (#4878) indicates mature team culture and product confidence

**Dissatisfaction Indicators:**
- Shell approval bypass chain (6 issues) suggests the risk classification model needs fundamental redesign, not patching
- #4874 (HTTP invocation error) is a regression affecting developer experience on non-localhost hosts

## Backlog Watch

**Oldest Open PRs Needing Attention:**
- **#3708** (ironclaw-ci[bot], OPEN since 2026-05-16) — Release PR with breaking changes in `ironclaw_common` and `ironclaw_skills`. Blocked for 30 days. This is the current release pipeline bottleneck. [Link](https://github.com/nearai/ironclaw/pull/3708)
- **#4002** (dependabot[bot], OPEN since 2026-05-24) — GitHub Actions dependency bump with 16 updates, including major version bumps (actions/checkout v4→v6). 22 days stale. [Link](https://github.com/nearai/ironclaw/pull/4002)
- **#4499** (dependabot[bot], OPEN since 2026-06-05) — Tokio ecosystem bump (tokio-tungstenite, tokio-postgres-rustls, hyper). 10 days stale. [Link](https://github.com/nearai/ironclaw/pull/4499)

**Expired Dogfooding Tracker:**
- **#4692** (think-in-universe, OPEN since 2026-06-10) — Week 06/08-06/14 dogfooding findings. 5 days stale with no new comments. May need rotation to #4879 (new week started). [Link](https://github.com/nearai/ironclaw/issues/4692)

**Security Disclosure Gap:**
- The 6 shell security advisories (#4861-#4865, #4797) have no linked fix PRs yet. With multiple disclosure types (wrapper bypass, delegation bypass, sandbox escape), the maintainers need to prioritize a coordinated security release.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the structured project digest for **LobsterAI** based on GitHub data from **2026-06-15**.

---

# LobsterAI Project Digest – 2026-06-15

## 1. Today's Overview
Activity on the LobsterAI repository remains **low**, with only 2 issues and 4 PRs updated in the last 24 hours, none of which were created today. All items are marked as `[stale]`, indicating a possible development pause or reduced maintainer bandwidth. No new releases were published. The most notable activity comes from three open long-running feature PRs (#1429, #1430, #1431) targeting the Cowork session experience, and one closed bugfix PR (#1465) addressing a persistent ghost session bug.

## 2. Releases
**None.** No new versions were tagged in the last 24 hours.

## 3. Project Progress
Only one PR was merged or closed today:
- **[PR #1465 – Closed] fix(scheduled-tasks): 已删除的定时任务重启后作为幽灵会话重新出现**  
  *Author: linlihua*  
  This fix resolves a critical data integrity bug where deleted scheduled tasks would reappear as empty "ghost" sessions after an application restart. The root cause was a missing cleanup of local SQLite `cowork_sessions` records when a cron task was deleted.  
  **Link:** [PR #1465](https://github.com/netease-youdao/LobsterAI/pull/1465)

No other PRs were merged today.

## 4. Community Hot Topics
The following issues and PRs have attracted the most attention (comments, reactions), though activity remains low:

- **Issue #1434** – [OPEN] "Language set to Chinese, but search results in agent skill tab show English UI text"  
  *Comments: 1* | *Created: 2026-04-03*  
  This is a persistent localization bug that has not been addressed in over two months.  
  **Link:** [Issue #1434](https://github.com/netease-youdao/LobsterAI/issues/1434)

- **Issue #1435** – [OPEN] "New custom agent: long name overflows modal, poor display"  
  *Comments: 1* | *Created: 2026-04-03*  
  A UI/UX issue that also remains untouched since April.  
  **Link:** [Issue #1435](https://github.com/netease-youdao/LobsterAI/issues/1435)

- **PR #1429** – [OPEN] feat(cowork): in-session message search with mark.js highlighting  
  *Created: 2026-04-03*  
  This feature PR, while closed in terms of code changes, has not been merged. It would add a much-requested search-in-conversation feature.  
  **Link:** [PR #1429](https://github.com/netease-youdao/LobsterAI/pull/1429)

**Underlying need:** Users are expressing frustration with incomplete localization and UI polish, while power users are waiting for productivity enhancements like in-session search and session timers.

## 5. Bugs & Stability
No new bugs were reported today. The following stale but unaddressed bugs remain:

- **Issue #1434** – Localization bug: Chinese UI shows English text (Medium severity, no fix PR)  
  **Link:** [Issue #1434](https://github.com/netease-youdao/LobsterAI/issues/1434)

- **Issue #1435** – UI overflow: long agent name breaks modal layout (Low severity, no fix PR)  
  **Link:** [Issue #1435](https://github.com/netease-youdao/LobsterAI/issues/1435)

There are no crash or regression reports in the current data window.

## 6. Feature Requests & Roadmap Signals
No new feature requests were filed today. However, three significant feature PRs remain open and could indicate the next minor release direction:

- **PR #1429** – In-session message search (mark.js) – likely to land in next vX.Y release.  
- **PR #1430** – Prevent system sleep during long-running Cowork sessions (Electron `powerSaveBlocker`).  
- **PR #1431** – Real-time elapsed timer in StreamingActivityBar.

These features address reliability and user experience during long-running agent tasks. If merged, they would represent a meaningful quality-of-life update.

## 7. User Feedback Summary
While no explicit user feedback was posted in the last 24 hours, the persistent open issues reveal:
- **Pain point #1:** Localization inconsistency (Chinese locale still shows English text in agent skill search) – frustration since April.
- **Pain point #2:** Poor UI handling of long agent names – a basic UX failure.
- **Pain point #3:** Ghost sessions after deleting scheduled tasks (now fixed in PR #1465, but not yet released).

Overall, user satisfaction may be slightly dampened by lack of UI polish, but the ongoing feature PRs suggest the team is investing in deeper reliability and productivity.

## 8. Backlog Watch
The following items have been stale for over two months and require maintainer attention:

- **Issue #1434** (created 2026-04-03) – Chinese localization bug.  
  **Link:** [Issue #1434](https://github.com/netease-youdao/LobsterAI/issues/1434)

- **Issue #1435** (created 2026-04-03) – Agent name overflow UI bug.  
  **Link:** [Issue #1435](https://github.com/netease-youdao/LobsterAI/issues/1435)

- **PR #1429, #1430, #1431** (all created 2026-04-03) – Three feature PRs for Cowork session improvements remain unmerged and unreviewed.  
  **Links:** [PR #1429](https://github.com/netease-youdao/LobsterAI/pull/1429), [PR #1430](https://github.com/netease-youdao/LobsterAI/pull/1430), [PR #1431](https://github.com/netease-youdao/LobsterAI/pull/1431)

**Recommendation:** Prioritize review and merge of the three Cowork feature PRs and the localization/UI issues to improve perceived project momentum and user satisfaction.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-15

## 1. Today's Overview
Activity remains moderate today with 1 open issue and 2 open pull requests, no merges or releases. The community is contributing via a dependency bump and a Dockerfile bug fix, while a single feature request around a Rust-based memory backend surfaced. No critical regressions were reported. Overall, the project shows steady maintenance with focused improvements.

## 2. Releases
No new releases today. The latest available release remains unreported.

## 3. Project Progress
No PRs were merged or closed today. The two open PRs represent work in progress:

- **PR #1122** (open, by sayotte): Fixes a Dockerfile issue where `VOLUME` declarations shadowed the home bind mount. This is a non-breaking fix that improves container deployment behavior.
- **PR #1121** (open, by dependabot[bot]): Bumps `esbuild` from 0.25.12 to 0.28.1 across the `npm_and_yarn` group in `/crates/web/ui`. This is a routine dependency update with no breaking changes expected.

[PR #1122](https://github.com/moltis-org/moltis/pull/1122) | [PR #1121](https://github.com/moltis-org/moltis/pull/1121)

## 4. Community Hot Topics
The only active issue today is the most discussed item:

- **Issue #1123** (open, by joeblew999): Requests adding a pure-Rust `turbovec` backend as an alternative memory store for extreme edge compression. This is a feature request with 0 comments and 0 reactions, suggesting it is early-stage with little community engagement yet. The underlying need appears to be enabling Moltis to run efficiently on very resource-constrained devices, likely for edge or IoT deployments.

[Issue #1123](https://github.com/moltis-org/moltis/issues/1123)

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported today. The project appears stable with no active stability issues.

## 6. Feature Requests & Roadmap Signals
The lone feature request today (#1123) signals interest in extreme edge compression performance via a pure-Rust vector backend. This is a niche but forward-looking enhancement that aligns with growing edge computing use cases. If accepted, it may appear in an upcoming minor or patch release, but given its early stage, it is more likely a candidate for the next major or minor version after community evaluation.

## 7. User Feedback Summary
No user feedback or pain points were voiced in today's issues or PRs. The absence of complaints or support requests suggests general satisfaction with the current release. The feature request (#1123) implies a user interested in smaller-footprint deployments, though no concrete dissatisfaction was expressed.

## 8. Backlog Watch
No long-unanswered issues or PRs were flagged today. All open items were created or updated within the last 24 hours, indicating maintainers are keeping pace with new contributions. No items require urgent maintainer attention.

---

**Project Health Summary**: Moltis is in a healthy maintenance phase with low activity, no regressions, and a focus on dependency hygiene and Docker usability. The single feature request points toward future edge/compression capabilities, while the project remains stable for current users.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the structured project digest for **CoPaw (github.com/agentscope-ai/CoPaw)** based on the provided GitHub data for **2026-06-15**.

---

# CoPaw Project Digest – 2026-06-15

## 1. Today's Overview
The project is experiencing a period of **high community engagement** (15 updated Issues, 9 updated PRs), but with **zero mergers or closures**. This indicates a bottleneck in maintainer bandwidth, as the team is processing a growing volume of user feedback and contributions without clearing the queue. Activity is centered on **regression bugs** (v1.1.11.post2), **new feature requests** (localization, platform support), and **first-time contributor** PRs aimed at fixing systemic issues. The release pipeline is currently cold, with no new releases today.

## 2. Releases
- **New Releases:** None

## 3. Project Progress
No PRs were **merged or closed** today. All 9 open PRs remain in review status. Notable active PRs include:
- **[#5188] Request payload transforms** (sanfran1068) – Adds a plugin-level SDK hook for modifying chat request payloads before sending.
- **[#5187] feat(computer-use): Windows desktop GUI automation** (jinglinpeng) – Implements UIA-based automation for the agent to control the Windows desktop, paired with a Tauri Control Mode UI.
- **[#5141] fix: tool card loading spinner** (zhaozhuang521) – Fixes UI responsiveness issues for shell commands and unregistered tools.

**First-time contributor cluster (nguyenthanhthe):**
- **[#5176]** Fix: Command text overflow on approval UI.
- **[#5178]** Feat: Session filter by title (#4999).
- **[#5179]** Fix: Expand multi-agent collaboration trigger keywords.
- **[#5180]** Fix: Increase cron/heartbeat timeout and add autonomous context prompt.
- **[#5175]** Feat: Partial Vietnamese locale support.

## 4. Community Hot Topics
- **[#5047] Windows Tauri desktop startup 10x slower** (moolawooda)
  - *Comments: 4* | *Root pain:* Migration from Python to Tauri caused 10+ minute startup and repeated freezes. This is a **critical user experience regression** affecting Windows 11 users.
- **[#5156] Feature: Support kimi-for-coding / allowlist for uv** (wjt0321)
  - *Comments: 5* | *Need:* Users subscribed to Kimi's coding tier cannot leverage their existing paid subscriptions. Suggests adding a provider whitelist for `uv`.
- **[#5161] Long conversation causes QwenPaw to hang** (tecgic)
  - *Comments: 2* | *Severity:* High. The app becomes completely unresponsive after many turns, affecting power users.
- **[#5168] Feature: Add official Zalo Bot channel** (lamnguyen3119)
  - *Comments: 1* | *Market signal:* Strong demand from Vietnamese users for integration with Zalo, indicating geographic expansion of the user base.

## 5. Bugs & Stability
*Ranked by severity:*

| Severity | Issue # | Title | Status | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Critical** | #5161 | Long conversation hangs QwenPaw | Open | App becomes unresponsive. No fix PR yet. |
| **High** | #5047 | Tauri desktop startup 10x slower | Open | Startup time regression. No fix PR. |
| **High** | #5163 | Gemini tool calling regression in v1.1.11.post2 | Open | Working in v1.1.10, broken in .post2. |
| **High** | #5171 | Context compression loss (agent personas) | Open | Zero-token compression destroys context. |
| **Medium** | #5184 | Local model providers not showing in .post2 | Open | v1.1.11 feature broken in patch. |
| **Medium** | #5181 | Plugin pip install infinite cmd window popups | Open | Dependency install loops on network failure. |
| **Low** | #5177 | DingTalk chat sessions invisible in console | Open | Session data exists but not indexed in `chats.json`. |

**Key finding:** A clear **regression pattern** between v1.1.10 and v1.1.11.post2 (Issues #5163, #5184) is affecting core functionality (Gemini tool calling, local provider visibility).

## 6. Feature Requests & Roadmap Signals
- **[#5185] Feature: Real-time timestamp (HH:MM:SS) in agent context** (lgcheng105) – Users want agents to know exact time without calling `get_current_time`. A high-quality, low-effort UX improvement likely to land soon.
- **[#5182] Feature: Unified model config** (hongweifei) – Support for vector, text, audio, video model configs in a single schema. Signals a push toward multi-modal unification.
- **[#5168] Zalo Bot support** (lamnguyen3119) – Strong regional demand. Likely to appear as an official channel if contributor momentum continues (related: 2 Vietnamese locale PRs today).
- **[#5167] Feat: Improve Feishu CardKit streaming for long replies** (wjt0321) – Current streaming is "one character at a time" for long responses. A performance optimization request.
- **[#5156] Kimi-for-coding + uv whitelist** (wjt0321) – Permission-level provider integration model.

**Prediction for next release:** Time-stamping in agent context (#5185) and the Zalo channel (#5168) are the most likely new features, given the strong community backing and existing localization PRs.

## 7. User Feedback Summary
- **Pain Points:**
  - **Performance regression:** Desktop startup time (10+ minutes) is the loudest complaint, affecting daily usability.
  - **Context loss:** Long-session hangs (#5161) and token compression destroying context (#5171) are breaking advanced workflows.
  - **Plugin ecosystem friction:** Windows popups during dependency install (#5181) and missing local providers (#5184) degrade the user experience.
- **Use Cases:**
  - **Vietnamese market:** Multiple PRs and issues (Zalo, Vietnamese locale) signal a rapidly growing user base in Vietnam.
  - **Coding assistants:** Users subscribed to Kimi for Coding want to route their paid subscription through CoPaw.
  - **Multi-modal agent automation:** The `computer-use` PR (#5187) indicates interest in agent-driven GUI automation.
- **Satisfaction/Dissatisfaction:** Generally positive community engagement, but frustration is growing over **unfixed regressions**. The first-time contributor surge shows a healthy onboarding experience, but these contributors are fixing issues that the core team has not yet addressed.

## 8. Backlog Watch
These issues have remained open for 3+ days without a maintainer response or fix PR:

| Issue # | Age (days) | Title | Potential Impact |
| :--- | :--- | :--- | :--- |
| #5047 | 6 | Windows Tauri desktop 10x slower | **Critical** – Blocks daily use for Windows segment. |
| #5156 | 3 | Kimi-for-coding / uv whitelist | **Medium** – Adds friction for paying Kimi users. |
| #5163 | 3 | Gemini tool calling regression | **High** – Affects multi-model setups. |
| #5171 | 2 | Context compression loss | **High** – Destroys agent continuity. |

**Recommendation:** Issue #5047 (startup slowness) and #5163 (Gemini regression) should be prioritized for a hotfix release (v1.1.12) to restore baseline stability before adding new features.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for June 15, 2026, compiled from the provided GitHub data.

---

## ZeroClaw Project Digest: 2026-06-15

### 1. Today's Overview

ZeroClaw is in a period of **intense, high-quality engineering activity**. Over the last 24 hours, 42 issues and 50 pull requests were updated, indicating a very healthy and responsive development cycle. The project shows a strong focus on **stability and security**, with critical fixes landing for production blockers related to provider handling and configuration, as well as a major consolidation of the core agent "turn engine." While no new releases were cut today, a significant number of merged features and fixes from the past week are being polished, suggesting a release may be imminent.

### 2. Releases

**None.** There were no new releases of ZeroClaw in the last 24 hours.

### 3. Project Progress

While only 3 PRs were reported as merged/closed, the activity suggests a major consolidation effort is underway. Notable developments include:

- **Turn Engine Consolidation:** Issue #7415 (RFC: Unify three agent turn engines) was marked as closed, and its implementation was described as a "single consolidation PR" (PR #7540, which has since been merged). This is a **major architectural win** that will reduce complexity and bugs in the core agent loop.
- **SMS Provider Onslaught:** A wave of new SMS channel integrations led by user `theonlyhennygod` have officially landed. This adds support for **Vonage, Sinch, Plivo, and Telnyx**, making ZeroClaw a much more versatile platform for telephony-based agents.
- **Environment Parity:** PR #7549 landed a critical fix to align plugin installation and discovery paths, ensuring that WASM plugins installed via the CLI are now correctly found by the runtime, gateway, and skills systems.
- **Quickstart & Experience:** Multiple small but impactful PRs landed to improve the `zeroclaw quickstart` UX, including auto-lowercasing agent aliases (PR #7637) and prompting for webhook ports (PR #7610).

### 4. Community Hot Topics

The most active discussions reveal the community's focus on **secure delegation, architecture simplification, and quality of life improvements**.

- **#3642 [CLOSED] - Full Docker Image:** With 13 comments and 3 👍, this request for a feature-rich Docker image highlights a clear barrier for new/non-technical users. The closure suggests a solution was found, likely making it easier to run complex configurations.
    - *Link:* [Issue #3642](https://github.com/zeroclaw-labs/zeroclaw/issues/3642)

- **#6808 [OPEN] - RFC: Work Lanes, Board Automation:** This RFC (11 comments) shows the maintainer team is actively seeking to improve its own internal processes, indicating a mature project focused on long-term maintainability.
    - *Link:* [Issue #6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)

- **#7470 [OPEN] - Delegation Bug (High Priority):** With 7 comments, this critical S1 bug is a major pain point for users requiring complex multi-agent workflows. The community is actively discussing the proper gating logic for tool permissions between delegated agents.
    - *Link:* [Issue #7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)

- **#6293 [OPEN] - Air-Gapped Execution Mode RFC:** This long-running discussion (5 comments) for an air-gapped/sandboxed execution mode remains a hot topic, indicating a strong demand for enterprise-grade security and privacy features.
    - *Link:* [Issue #6293](https://github.com/zeroclaw-labs/zeroclaw/issues/6293)

### 5. Bugs & Stability

Bugs reported today are largely focused on edge cases and configuration errors, rather than systemic failures. The project is currently **highly stable** and actively patching regressions.

- **Critical (S1 - Workflow Blocked):**
    - **#7470 [OPEN]** - `delegate` tool fails when delegation target has an empty `allowed_tools` list. **FIX PR EXISTS:** PR #7592 adds documentation for this requirement, and PR #7583 aims to fix the underlying runtime logic.
        - *Link:* [Issue #7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)

- **High (S2 - Degraded Behavior):**
    - **#6856 [OPEN]** - `show_tool_calls` configuration option missing from the schema v3 channel configuration. **FIX PR STATUS:** Unknown.
        - *Link:* [Issue #6856](https://github.com/zeroclaw-labs/zeroclaw/issues/6856)
    - **PR #5892 [OPEN]:** Two production blockers for OpenAI-compatible providers: an empty `tool_choice` field and orphaned `tool_use` IDs. This is a **large, long-running fix** that is crucial for provider reliability.
        - *Link:* [PR #5892](https://github.com/zeroclaw-labs/zeroclaw/pull/5892)

- **Medium:**
    - **PR #7617 / #7580:** Fix for users accidentally creating extra TOML table levels in provider config, causing serde to silently drop fields.
    - **PR #7616:** Fix for Groq provider failing when assistant messages contain `reasoning` content on outbound replay.
    - **PR #7614:** Fix for the install script failing to detect musl libc on Linux.

### 6. Feature Requests & Roadmap Signals

The project roadmap is clearly evolving towards **enterprise security, better UX, and a broader ecosystem**.

- **Likely Next Release:**
    - **Security/Delegation:** The fixes for the delegate tool (#7470, #7583) are must-haves for any user running multi-agent workflows.
    - **Cron Pause/Resume:** PR #7666 adds the ability to pause/resume scheduled tasks via the gateway API and web UI, a direct upgrade from the current delete-only interface.

- **Long-term Roadmap Signals:**
    - **Air-Gapped Execution (#6293):** This RFC is a strong signal of intent for a production-grade security model.
    - **Memory Dream Mode (#6693):** This feature, a periodic memory consolidation engine, is a direct step towards more autonomous and context-aware agents.
    - **Provider Ecosystem Expansion:** The multitude of recently merged provider integrations (Featherless, Lambda, Arcee, Inception Labs) shows a commitment to offering maximum choice and competitive pricing for users.

### 7. User Feedback Summary

- **Pain Points:**
    - **Configuration Complexity:** Users are hitting silent failures from misconfigured TOML files (e.g., nested aliases in #7617, missing webhook ports in #7610). The new quickstart validations directly address this.
    - **High Barrier to Entry:** The request for a "full" Docker image (#3642) confirms that feature-flag-based binaries create friction for non-technical users.
    - **Multi-Agent Workflow Hurdles:** The critical bug #7470 highlights a real-world frustration for users trying to set up reviewer/research agent hierarchies.

- **Satisfaction:**
    - **Greatly appreciated tool:** User `MushiTheMoshi` in issue #6847 explicitly thanked the team, calling ZeroClaw the "Best tool out there," indicating strong user satisfaction.
    - **Responsive Development:** The rapid merging of multiple new providers (Phonix, Sonos, Spotify, etc.) demonstrates strong alignment with community feature requests.

### 8. Backlog Watch

The following items require maintainer attention:

- **#6074 [OPEN] - Audit of Lost Commits:** This issue tracks 153 commits that were lost in a bulk revert nearly three months ago. It has been marked as `in-progress` but has only 2 comments and no linked PR. This is a major engineering debt item that requires resolution.
    - *Link:* [Issue #6074](https://github.com/zeroclaw-labs/zeroclaw/issues/6074)

- **#5892 [OPEN] - Provider Production Blockers:** This PR, fixing two critical bugs for OpenAI-compatible providers, has been open since April 19. While it's an active PR, its age in a fast-moving project is a concern. It is currently flagged with `needs-author-action`.
    - *Link:* [PR #5892](https://github.com/zeroclaw-labs/zeroclaw/pull/5892)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*