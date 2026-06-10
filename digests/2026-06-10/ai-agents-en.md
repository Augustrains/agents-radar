# OpenClaw Ecosystem Digest 2026-06-10

> Issues: 452 | PRs: 492 | Projects covered: 13 | Generated: 2026-06-10 02:03 UTC

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

Here is the OpenClaw project digest for June 10, 2026.

---

## OpenClaw Project Digest for 2026-06-10

### 1. Today's Overview

The OpenClaw project is showing **very high activity**, with 452 issues and 492 pull requests updated in the last 24 hours. The project released two new versions today (v2026.6.5 stable and v2026.6.5-beta.6), indicating a rapid release cycle focused on stability and hotfixes. While the volume of open work and high-severity regressions suggests a pressurised period, the team is producing numerous fix PRs and maintaining a high level of community engagement. Key stability concerns revolve around session state management, message loss across multiple channels (QQ, Matrix, Discord, Telegram), and memory system reliability.

### 2. Releases

Two new releases are available today.

- **[v2026.6.5 (Stable)](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5)** and **[v2026.6.5-beta.6](https://github.com/openclaw/openclaw/releases/tag/v2026.6.5-beta.6)**
  - **Key Fix:** Both releases contain a critical fix for QQ Bot, stripping model reasoning/thinking scaffolding (e.g., `<thinking>` tags) before delivery to prevent raw internal content from leaking into user-facing channels. This addresses a major privacy and UX issue.
  - **Improvement:** MCP tool results now have better type coercion for `resource_link`, `resource`, `audio`, and malformed images, preventing crashes or silent failures from unexpected data shapes.
  - **Migration Notes:** These are minor patch releases. No breaking changes or specific migration steps are required.

### 3. Project Progress

While the PR list is dominated by open items, the data shows **137 pull requests were merged or closed** in the last 24 hours. Key areas of progress visible in the active PRs include:

- **Session & Delivery Stability:** Multiple PRs target session lane wedging and stuck-session recovery. [PR #91801](https://github.com/openclaw/openclaw/pull/91801) and [PR #91802](https://github.com/openclaw/openclaw/pull/91802) aim to release wedged lanes after aborted runs.
- **Message Loss Prevention:** [PR #88992](https://github.com/openclaw/openclaw/pull/88992) prevents silent message loss when using `message_tool` mode, recovering stranded replies if the LLM forgets to call the tool.
- **Systemd Reliability:** [PR #89858](https://github.com/openclaw/openclaw/pull/89858) fixes scope conflicts for systemd gateway units, a common deployment issue on Linux.
- **Memory Indexing:** [PR #91227](https://github.com/openclaw/openclaw/pull/91227) fixes a bug where the memory search index could be left in a permanently paused state after a rebuild/swap.

### 4. Community Hot Topics

The most active issues reflect deep user frustration with reliability and data leakage.

- **[#25592: Text between tool calls leaks to messaging channels](https://github.com/openclaw/openclaw/issues/25592)** (29 comments) - This "diamond lobster" severity issue is a top concern. Users report that internal agent processing output (error handling, narration) is being sent as visible messages in Slack and iMessage, creating a confusing and potentially embarrassing UX.
- **[#88312: Codex app-server turn-completion stall regression](https://github.com/openclaw/openclaw/issues/88312)** (15 comments, 3 👍) - A regression on the Codex app-server that causes multi-tool turns to fail with "Codex stopped before confirming the turn was complete." The fix from a previous release (#85107) appears to have broken again, causing significant frustration for users on the premium tier.
- **[#87307: Matrix thread replies regressed](https://github.com/openclaw/openclaw/issues/87307)** (14 comments) - A stable version upgrade broke Matrix thread replies, sending them as normal messages and breaking chat flows. This highlights a need for better regression testing across messaging providers.
- **[#54253: OpenClaw fails on RISC-V64](https://github.com/openclaw/openclaw/issues/54253)** (13 comments) - A growing community of users interested in RISC-V architecture is hitting an LLM request failure, blocking adoption on new hardware.
- **[#53628: `$XDG_CONFIG_HOME` not processed when installing a skill](https://github.com/openclaw/openclaw/issues/53628)** (13 comments) - A significant usability bug in the skill installation pipeline that ignores environment variables, leading to non-functional Docker setups.

### 5. Bugs & Stability

The project is facing a cluster of **high-severity bugs and regressions**, primarily around message delivery and session integrity.

- **Critical / P1:**
  - **[Codex Turn-Completion Stall (#88312)](https://github.com/openclaw/openclaw/issues/88312):** A regression that breaks multi-tool turns on the Codex app-server. A fix is likely a high priority.
  - **[Session Write-Lock Timeouts (#86538)](https://github.com/openclaw/openclaw/issues/86538):** Write-lock timeouts are blocking all delivery lanes, leading to unrecoverable session stalls. Fix PRs like [#91801](https://github.com/openclaw/openclaw/pull/91801) are in progress.
  - **[EmbeddedAttemptSessionTakeoverError (#86508)](https://github.com/openclaw/openclaw/issues/86508):** A regression on Discord causing session takeover errors and message failure. [PR #91797](https://github.com/openclaw/openclaw/pull/91797) aims to fix this by treating the agent's own no-op session rewrites as benign.
  - **[Unbounded Heap Growth (#89315)](https://github.com/openclaw/openclaw/issues/89315):** A memory leak causing the gateway to be killed by OOM on long-running Linux deployments. This is a critical stability issue for self-hosters.

### 6. Feature Requests & Roadmap Signals

The community is pushing for better configuration granularity and control.

- **Hot Predictions for Next Version:**
  - **[Per-Channel/Group/DM Model Override (#53638)](https://github.com/openclaw/openclaw/issues/53638):** Highly requested (5 comments, 2 👍), this feature would allow users to specify different models for different conversations without global overrides. This is a strong candidate for the next minor release.
  - **[Persistent Task-Status Surface (#52640)](https://github.com/openclaw/openclaw/issues/52640):** Users want a better way to see the status of long-running tasks in Discord. Given the ongoing message loss issues, improving status visibility is a logical next step.
- **Longer-Term Signals:**
  - **[Context Provenance Metadata (#54373)](https://github.com/openclaw/openclaw/issues/54373):** A sophisticated RFC proposing metadata for injected context segments to help the agent distinguish between session-start content and fresh data. This indicates a move toward more intelligent context management.
  - **[Config Options to Suppress Transient Tool Warnings (#39406)](https://github.com/openclaw/openclaw/issues/39406):** A strong UX request to stop non-fatal tool errors from spamming user channels.

### 7. User Feedback Summary

The dominant themes in user feedback are **frustration with reliability** and **concern about data/privacy**.

- **Pain Points:**
  - **Message Leaks:** The most urgent issue. Users are extremely unhappy about internal agent processing (thinking tags, tool calls) leaking into public channels ([#25592](https://github.com/openclaw/openclaw/issues/25592), [#44905](https://github.com/openclaw/openclaw/issues/44905)).
  - **Regression Fatigue:** Users are frustrated by features that break after an update (Matrix threads [#87307](https://github.com/openclaw/openclaw/issues/87307), Codex turns [#88312](https://github.com/openclaw/openclaw/issues/88312)). This suggests a need for more robust CI/CD and regression testing.
  - **Session Stalls & Message Loss:** A systemic issue where the agent becomes unresponsive or loses replies, especially on WhatsApp, Telegram, and Discord. The root cause appears to be session lock contention and event-loop stalls.

### 8. Backlog Watch

Several critical issues remain open for extended periods, requiring maintainer attention.

- **[#25592: Text between tool calls leaks](https://github.com/openclaw/openclaw/issues/25592)** (Opened Feb 24) - A severe security/UX issue that has been open for over 3 months despite its high rating. The recent fix for QQ Bot in v2026.6.5 is a positive sign, but the underlying issue appears broader.
- **[#31331: Docker + Sandbox can't `workspaceAccess`](https://github.com/openclaw/openclaw/issues/31331)** (Opened Mar 2) - This P1 bug prevents the primary sandboxing feature from working in Docker, affecting a large portion of the user base. The issue has multiple high-severity labels and linked PRs but remains open.
- **[#48003: Steer mode does not inject messages mid-turn](https://github.com/openclaw/openclaw/issues/48003)** (Opened Mar 16) - A critical feature for real-time interaction has been broken for months, blocking users who rely on mid-turn steering.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report — 2026-06-10

## 1. Ecosystem Overview

The personal AI agent open-source landscape is experiencing **intense maturation pressure**, with projects converging on reliability, security, and multi-provider interoperability while diverging on architecture and target deployment models. The top-tier projects (OpenClaw, Hermes Agent, PicoClaw, NanoClaw, and ZeroClaw) are shipping multiple fixes daily, but high-severity regressions around session management, message delivery, and credential handling indicate the ecosystem has not yet reached production-grade stability. A clear **"reliability winter"** is underway — users across every major project express frustration with tool-call leaks, session stalls, and silent message loss. Simultaneously, demand for **multi-agent coordination**, **per-conversation model selection**, and **better observability** is rising across the board, signaling that the next competitive frontier will be operational maturity rather than raw feature count.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | New Release? | Estimated Health Score |
|---|---|---|---|---|
| **OpenClaw** | 452 updated | 492 updated | ✅ v2026.6.5 + beta | 🟡 **Moderate** — high throughput but critical regressions |
| **NanoBot** | 23 updated | 23 updated | ❌ None | 🟢 **Good** — steady maintenance, low drama |
| **Hermes Agent** | 50 updated | 50 updated | ❌ None | 🟢 **Good** — active sprint, responsive triage |
| **PicoClaw** | 20 updated | 19 updated | ✅ Nightly (unstable) | 🟡 **Moderate** — security crisis dominating signal |
| **NanoClaw** | 1 updated | 43 updated (39 merged) | ❌ None | 🟢 **Good** — major backlog cleanup, consolidation phase |
| **NullClaw** | 5 updated | 8 updated | ❌ None | 🟢 **Good** — strong fix velocity, 7/8 PRs merged |
| **IronClaw** | 48 updated | 50 updated | ❌ None | 🟡 **Moderate** — pre-production crunch, 3 critical provider bugs |
| **LobsterAI** | 2 open | 5 updated | ❌ None | 🟢 **Good** — focused feature delivery |
| **CoPaw** | 37 updated | 35 updated | ✅ v1.1.11-beta.2 | 🟢 **Good** — healthy release cadence |
| **ZeroClaw** | 50 updated | 50 updated | ❌ None | 🟡 **Tense** — heavy triage, 97 open items, S1 bugs stale |
| TinyClaw | 0 | 0 | ❌ | ⚫ **Inactive** |
| Moltis | 0 | 0 | ❌ | ⚫ **Inactive** |
| ZeptoClaw | 0 | 0 | ❌ | ⚫ **Inactive** |

**Key observations:**
- **OpenClaw** dominates raw volume (452 issues, 492 PRs) but is clearly in a firefighting mode — session stalls, message leaks, and unbounded heap growth are systemic.
- **PicoClaw** was hit by a coordinated security disclosure (17 issues from one researcher), skewing its activity toward defensive hardening.
- **NanoClaw** merged 39 PRs in 24 hours — the highest closure rate — indicating a deliberate stabilization push.
- **ZeroClaw** mirrors OpenClaw in volume (50/50) but with far fewer closures (2 issues, 1 PR), suggesting it is less responsive.

---

## 3. OpenClaw's Position

**Advantages:**
- **Massive community**: 452 issues and 492 PRs in 24 hours — 9× the activity of the next-busiest project (Hermes Agent at 50/50). This creates a virtuous cycle of rapid bug discovery and fix throughput.
- **Mature release pipeline**: Two releases (stable + beta) shipped today, with critical QQ Bot thinking-tag stripping fix — shows operational discipline.
- **Broadest channel support**: Active bug reports for QQ, Matrix, Discord, Telegram, Slack, iMessage, and WhatsApp — no other project covers this many surfaces simultaneously.
- **Codex app-server integration**: Premium tier with dedicated infrastructure, indicating commercial ambitions beyond pure open-source.

**Technical approach differences:**
- **Session lane architecture**: OpenClaw uses a session-lane model with write-lock timeouts (cause of the wedged-session crisis). Most competitors use simpler per-conversation state management.
- **Message-tool pattern**: The `message_tool` recovery system (PR #88992) is unique — other projects assume the LLM always calls the tool correctly.
- **Memory indexing**: Separate memory search index with rebuild/swap lifecycle — more sophisticated than NanoBot's flat `history.jsonl` or CoPaw's monolithic context.

**Community size comparison:**
- OpenClaw's issue:PR ratio (~1:1) suggests extremely high contributor engagement per bug report.
- For context: Hermes Agent operates at ~10× less raw volume but with similar issue:PR ratio (50:50), suggesting comparable contributor density per unit of community.
- OpenClaw's highest-rated bug (#25592 — tool call leaks) has 29 comments and "diamond lobster" severity — an attention metric no other project matches.

**Weaknesses visible in data:**
- **Regression fatigue**: Multiple users complain about features breaking after updates (Matrix threads, Codex turns). CoPaw and Hermes have avoided this pattern.
- **Critical bugs aging**: #25592 (tool call leaks) is 3+ months old — a data-leakage severity issue this long unresolved would be unacceptable in enterprise deployments.
- **Scale tension**: 452 open issues suggests triage is overwhelmed. Comparatively, NanoBot (6 open issues) and NullClaw (5 open issues) are far more contained.

---

## 4. Shared Technical Focus Areas

The following requirements appear **across three or more projects**, indicating ecosystem-wide priorities:

| Requirement | Affected Projects | Specific Need |
|---|---|---|
| **Per-conversation model override** | OpenClaw (#53638), NanoBot (#4253), Hermes Agent (#21587 via Telegram multi-bot) | Users managing multiple backends (OpenRouter, local, enterprise) need per-chat model selection |
| **Multi-agent / sub-agent coordination** | OpenClaw, PicoClaw (#2937, merged), IronClaw (#4662/#4663), LobsterAI (#2132), CoPaw (#4727 AgentScope 2.0) | Agents delegating to sub-agents with visibility, handshake, and notification |
| **Session isolation / context boundary enforcement** | OpenClaw (session lane wedging), NanoBot (#4259 cross-session pollution), PicoClaw (#2796 history truncation), ZeroClaw (#5808 budget exceeded) | Users report context leaking between sessions, causing AI confusion |
| **Cron reliability / scheduled task delivery** | OpenClaw, ZeroClaw (#6037 burst launches, #6646 Telegram failures), NullClaw (#941 subprocess not spawning) | Scheduled tasks silently failing without delivery confirmation |
| **Credential lifecycle management** | OpenClaw, Hermes Agent (#43083 redacted passwords break tool calls), PicoClaw (CSRF, auth bypasses), IronClaw (#4587 Minimax config) | Redaction for security vs. preserving context for tool execution |
| **Observability / debugging / tracing** | NanoClaw (#1202 trace UI), NullClaw (#711 cross-memory), IronClaw (#4588 observer seams), CoPaw (#5009), ZeroClaw (#7385 OTel spans) | Developers need turn-level visibility for debugging multi-step interactions |
| **Message delivery reliability** | OpenClaw (silent loss, #88992 recover tool), Hermes Agent (#43122 provider icons), PicoClaw ("typing" indicator fix #943), ZeroClaw (#6646 Telegram tool failures) | Multi-channel delivery failing silently — WhatsApp, Telegram, Discord |
| **Security hardening (SSRF, CSRF, path traversal)** | PicoClaw (17 coordinated disclosures), NanoClaw (#2722 Telegram CSPRNG), CoPaw (#4981 file preview), IronClaw (#4561-#4565 audit sinks) | Production deployments demanding enterprise-grade security posture |

**Bottom line**: The ecosystem is collectively discovering that **reliability engineering** (session isolation, credential safety, cron delivery) is harder than feature engineering. The projects that solve these first will win production adopters.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | NanoClaw | PicoClaw | IronClaw | CoPaw |
|---|---|---|---|---|---|---|
| **Target user** | Power user / self-hoster, premium tier via Codex | Developer / CLI-first, community-driven | Agent builder / skill developer | Chinese-market user, multi-channel (WeChat, Feishu) | Enterprise / NEAR ecosystem, multi-tenant | Chinese-market desktop user, Qwen-oriented |
| **Architecture** | Monolithic Go core, session lanes, MCP tool model | Modular Rust core, gateway abstraction, plugin system | Rust core, skills marketplace, plugin system | Go core, channel-first design, heavy config-driven | Rust + Reborn architecture, actor-model, attachment registry | Python / AgentScope 2.0, Tauri desktop, plugin-heavy |
| **Channel strategy** | Broadest: QQ, Matrix, Discord, Telegram, Slack, iMessage, WhatsApp | Focused: Telegram, Discord, CLI, Desktop, Matrix | Slim: Telegram, Feishu, WebUI | Chinese-focused: WeChat, Feishu, QQ, LINE, OneBot | Slack, WebUI, CLI (Telegram in PR #4625) | Desktop-first, WeChat plugin, Feishu |
| **Release cadence** | Rapid (stable + beta same day) | Sprint-based (no release today) | Consolidation (no release, 39 PRs merged) | Nightly + security patches | Pre-production (no release, 25-day blocked release PR) | Beta + patch (1.1.11-beta.2) |
| **Unique strength** | Scale of community + channel breadth | Developer tooling + gateway abstraction | Skill marketplace + observability trace | Security velocity + Chinese ecosystem | Enterprise auth + NEAR blockchain integration | Desktop UX + Chinese model compatibility |
| **Weakest area** | Stability regressions, aging critical bugs | Credential management, cron reliability | Release latency (merged work unreleased) | Session UX regressions (history, scope) | Provider compatibility broken for 3 major providers | Desktop performance (Tauri migration regressions) |

**Key architectural divides:**
- **Monolithic vs. modular**: OpenClaw and PicoClaw use monolithic Go runtimes; Hermes Agent and NanoClaw use modular Rust cores with gateway abstractions. IronClaw's "Reborn" architecture is the most radical rewrite.
- **Channel-first vs. desktop-first**: OpenClaw/PicoClaw/ZeroClaw treat channels as primary interface; CoPaw/LobsterAI are desktop-first with channel plugins.
- **Security posture**: PicoClaw is currently the most security-hardened (by necessity); OpenClaw and ZeroClaw have aging critical security issues (#25592, #6876).

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid iteration (high throughput, pre-production)
| Project | Characteristic | Risk |
|---|---|---|
| **OpenClaw** | Firehose of issues + PRs, releases daily | Burning out contributors, regression cycles |
| **IronClaw** | Intense pre-production crunch (50 PRs/day), Reborn architecture | 25-day blocked release PR, 3 critical unresolved provider bugs |
| **ZeroClaw** | Heavy triage mode, 97 open items | S1 bugs aging 40+ days, low PR merge rate |

### Tier 2: Steady stabilization (moderate throughput, health indicators positive)
| Project | Characteristic | Evidence |
|---|---|---|
| **Hermes Agent** | Sprint-based, responsive triage (50/50 ratio), new contributors | 7 issues closed, 4 PRs merged, #43181 merged same day as report |
| **NanoClaw** | Consolidation phase, 39/43 PRs merged | Backlog cleanup, WebUI control panel merged after months |
| **NullClaw** | Strong fix velocity, 7/8 PRs merged | PII redactor fix, Evolink provider, all 3-day turnarounds |
| **CoPaw** | Healthy release cycle, API base URL exposed | 15 PRs merged, 1.1.11-beta.2 shipped |

### Tier 3: Minimal activity / maintenance
| Project | Characteristic |
|---|---|
| **NanoBot** | Low volume but responsive — 23 updates, no major drama |
| **LobsterAI** | Focused feature delivery — task notifications, backup system |
| TinyClaw, Moltis, ZeptoClaw | **Inactive** — no activity in 24h, likely stalled |

### Tier 4: Security-crisis mode
| Project | Characteristic |
|---|---|
| **PicoClaw** | 17 coordinated vulnerability disclosures in one day, maintainers scrambling fix PRs. Project health is moderate but **attention is fully consumed by security**, not features. |

**Maturity insight**: The most "active" projects are not necessarily the most mature. OpenClaw and ZeroClaw have high throughput but show signs of systemic stress (regression fatigue, stale critical bugs). Hermes Agent and NullClaw have lower volume but demonstrate **fix discipline** — issues move from report → fix PR → merge within days. NanoClaw's 39 PRs merged in 24h suggests a deliberate stabilization sprint.

---

## 7. Trend Signals

### 1. "Reliability is the new feature" (ecosystem-wide)
Users across OpenClaw, NanoBot, PicoClaw, ZeroClaw, and CoPaw are reporting **context pollution, silent message loss, and session stalls** as their top frustrations. The projects that differentiate on reliability (Hermes Agent, NullClaw) are gaining satisfaction signals despite smaller communities. **For developers:** Prioritize session isolation, credential lifecycle, and delivery confirmation over new features.

### 2. Multi-agent orchestration is becoming table stakes
PicoClaw merged its agent collaboration bus; IronClaw is building project-scoped automation ownership; LobsterAI's community submitted design proposals for cross-model sub-task coordination. The expectation is no longer "talk to one agent" but "deploy a team of agents that collaborate." **For developers:** Design APIs for sub-agent spawning, result propagation, and parent-child session visibility now — retrofitting is costlier.

### 3. Provider interoperability is fragile and critical
Three top-tier projects (IronClaw — DeepSeek/Minimax/strict-mode; OpenClaw — Codex regression; NanoBot — GPT-5 `max_tokens` bug; ZeroClaw — Telegram tool failures) have **provider-specific bugs blocking users today**. The ecosystem lacks a robust provider abstraction layer. **For developers:** Invest in a compatibility test suite that catches provider-specific payload differences (e.g., `max_tokens` vs `max_completion_tokens`, null handling for optionals).

### 4. Per-conversation model selection is the #1 user-facing feature request
OpenClaw (#53638), NanoBot (#4253), and Hermes Agent (#21587) all feature this request prominently. Users want to route sensitive conversations to private models, fast queries to cheap providers, and complex tasks to capable ones — **per conversation, not per session**. This is a market gap no project has cleanly filled.

### 5. Observability is an emerging competitive differentiator
NanoClaw (#1202 trace UI), IronClaw (#4588 observer seams), ZeroClaw (#7385 OTel correlation), and CoPaw (#5009 Langfuse integration) are all shipping or planning tracing/observability. Developers of multi-agent systems cannot debug without turn-level visibility. **For developers:** Expose structured logs with `turn_id`, `parent_id`, and `provider` metadata — it will be expected in 12 months.

### 6. Desktop app performance is a pain point without good options
CoPaw's Tauri migration introduced 10-minute startup lag; ZeroClaw's macOS UI has unreadable dark themes and Cmd-C as quit; Hermes Desktop has visual clipping and sync issues. **Desktop-first agents are struggling** while channel-first architectures (OpenClaw, PicoClaw) avoid these complaints. The winning form factor may not be a desktop app but a well-integrated messaging agent.

### 7. Security disclosure velocity is accelerating
PicoClaw received 17 coordinated vulnerabilities in one day; OpenClaw has a 3-month-old data leakage bug (#25592) still open; ZeroClaw's `tool_search` MCP loading creates a silent 120-second hang. As these agents gain adoption (cron jobs, file access, credential management), they become attractive targets. **For developers:** Threat model your tool execution path, not just your auth layer.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-10

## Today's Overview

NanoBot shows a **strongly active** day with 23 PRs updated in the last 24 hours, 6 open issues, and 10 merged/closed PRs. The project is in a healthy maintenance phase, with the community contributing meaningful bug fixes (particularly around OpenAI-compatible provider compatibility) and infrastructure improvements. The core team and external contributors are collaboratively addressing long-standing issues around context isolation, tool call parsing, and WebUI reliability. The documentation overhaul PR (now merged) signals growing attention to onboarding, which aligns with the increasing number of user-raised configuration and behavioral issues. No new releases were made today.

## Releases

*No new releases were published today.*

## Project Progress

**10 PRs were merged or closed** in the last 24 hours, indicating steady feature advancement and bugfix integration:

- **#4208** — **[WebUI]** "Fork from here" for completed assistant replies: Users can fork from any assistant response to create a new chat with the conversation prefix preserved. *(merged)*
- **#4177** — **[Documentation]** Comprehensive onboarding rework: new setup paths for beginners, CLI command chooser, configuration task map, deployment readiness guides. *(merged)*
- **#4265** — **[English Read skill]** Cron schedule adjusted from daily to every 2 days. *(closed)*
- **#3434** — **[Feishu channel]** LaTeX rendering via CodeCogs API, configurable with `"streaming": true`. *(closed)*
- **#3400** — **[Dream]** New `allow_edit_identity_files` config option: when `False`, Dream only edits `MEMORY.md`, protecting `SOUL.md` and `USER.md`. *(closed)*
- **#4034** — **[GitAgent Protocol]** Added `agent.yaml` + `SOUL.md` support for portable AI agents. *(closed)*
- **#4190** — **[Tool call validation]** Increased strictness: malformed arguments are now rejected rather than silently repaired to `{}`. *(closed)*

## Community Hot Topics

**Most Active Issues:**

1. **#4253** [OPEN] — [enhancement] Support overriding model per conversation  
   *Author: rombert | Comments: 3 | 👍: 0*  
   User needs to switch between OpenRouter (fast/capable) and local llamacpp (private/cheap) per conversation based on privacy and time sensitivity.  
   [Link →](https://github.com/HKUDS/nanobot/issues/4253)

2. **#4259** [OPEN] — [bug] `history.jsonl` cross-session context pollution  
   *Author: chxuan | Comments: 2 | 👍: 0*  
   Sessions are not isolated in `ContextBuilder.build_system_prompt()`, causing all un-Dreamed entries to leak into every conversation's system prompt.  
   [Link →](https://github.com/HKUDS/nanobot/issues/4259)

3. **#4061** [OPEN] — [bug] OpenAI-compatible text-format tool calls not parsed  
   *Author: hamb1y | Comments: 1 | 👍: 0*  
   Some providers output tool calls as plain text markup rather than structured `tool_calls`; the runner ignores them entirely.  
   [Link →](https://github.com/HKUDS/nanobot/issues/4061)

**Most Active PRs:**  
All PRs have 0 comments today (standard GitHub activity reporting). The highest-value discussion-generating PRs are #4268 and #4263, both addressing the same `max_tokens` vs `max_completion_tokens` issue, indicating strong maintainer attention to the provider compatibility fix.

**Underlying Needs Analysis:** The top issues reveal a clear pattern: users are increasingly deploying NanoBot with **heterogeneous provider setups** (multi-model, multi-backend) and demanding **per-conversation control**, **session isolation**, and **strict tool-call interoperability**. The community wants NanoBot to be a reliable interoperability layer, not just a thin UI wrapper.

## Bugs & Stability

| Severity | Issue | Summary | Fix PR Exists? |
|----------|-------|---------|----------------|
| **Critical** | #4259 | Cross-session `history.jsonl` context pollution — all un-Dreamed entries leak between sessions | No fix yet |
| **High** | #4061 | OpenAI-compatible text-format tool calls silently ignored | No fix yet |
| **High** | #4264 | `idleCompact` only summarizes history minus last 8 messages, losing final corrections | No fix yet |
| **High** | #4261 | GPT-5.x models receive `max_tokens` instead of `max_completion_tokens`, causing rejection | **Yes** — #4268 and #4263 (both open) |
| **Medium** | #4267 | WebUI silently drops assistant replies from rendered conversation (intermittent, token-rate-dependent) | **Yes** — #4267 (open) |
| **Medium** | #4257 | `split_message` splits inside fenced code blocks, breaking HTML rendering | **Yes** — #4257 (open) |

**Ranking Rationale:** Cross-session data leakage (#4259) is top severity because it can cause privacy violations and AI confusion. The `max_tokens` bug (#4261) has two competing PRs, showing strong maintainer engagement.

## Feature Requests & Roadmap Signals

- **#4253** — Per-conversation model override: A high-value ergonomic feature likely to appear in next release, as it aligns with the multi-provider trend.
- **#4262** — Use `botIcon` at agent mode startup: Simple enhancement with high user visibility; trivially implementable.
- **GitAgent Protocol (#4034)** — Portable agent manifest format is now merged, signaling a move toward **interoperable agent definitions**. This could become a key differentiator.
- **Dream protection (#3400)** — Users can now lock `SOUL.md` and `USER.md` from Dream edits; merged today.

**Prediction:** The next release will likely include **per-conversation model selection**, **session isolation fix**, and the **`max_completion_tokens` compatibility fix**, as these are the hottest community requests with active PRs.

## User Feedback Summary

**Pain Points (reported in issues):**
- Users managing multiple model backends are frustrated by the inability to switch models per conversation (#4253).
- Session history contamination is causing "AI confusion" and incorrect memory summarization (#4259, #4264).
- Provider compatibility is fragile: some OpenAI-compatible services simply don't work because tool call formats differ (#4061), and GPT-5.x models reject requests outright (#4261).
- The WebUI loses messages intermittently, making it unreliable for long conversations (#4267).

**Satisfaction Signals:**
- The documentation overhaul (#4177) was merged, suggesting the team is responsive to onboarding complaints.
- The "Fork from here" feature (#4208) addresses a long-standing WebUI usability gap and was well-received.

## Backlog Watch

| Item | Age | Status | Risk |
|------|-----|--------|------|
| **#4061** — Text-format tool call parsing | 12 days | Open, 1 comment | High — affects any non-standard OpenAI-compatible provider, blocking adoption |
| **#4259** — Cross-session context pollution | 1 day | Open, 2 comments | Critical — privacy/safety issue, no fix PR yet |
| **#4264** — `idleCompact` message window | 1 day | Open, 0 comments | Medium — incorrect memory summarization, no fix PR yet |
| **#4119** — Symlink workspace escape (open PR) | 10 days | Open PR | High security — blocks relative symlinks escaping workspace, needs review/merge |
| **#4193** — Memory lifecycle test harness (open PR) | 6 days | Open PR | Medium — foundational test infrastructure, important for stability |

**Maintainer Attention Needed:** Issues #4061 and #4259 have the highest impact with no fix PRs yet. PRs #4119 (symlink security) and #4193 (test harness) are important infrastructure work that should be reviewed before they grow stale.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-06-10

## 1. Today's Overview

Hermes Agent is experiencing **very high activity**, with 50 issues and 50 PRs updated in the last 24 hours — a clear signal of a busy development sprint. The project maintains a healthy open/closed ratio, with 7 issues closed and 4 PRs merged, while 43 open issues and 46 open PRs indicate a large backlog of work in progress. No new releases were published today, suggesting the team is deep in development work rather than packaging. The community is highly engaged, contributing both bug reports and feature requests across a wide range of components including the agent core, gateway, CLI, and plugins. Overall project health appears strong, with rapid triage and multiple fix PRs already in flight for today's reported bugs.

## 2. Releases

No new releases were published today.

## 3. Project Progress

**4 PRs were merged/closed today.** Notable changes that advanced:

- **[PR #43181] ** — `fix(gateway): recover unloaded launchd job during update` (by edufalcao) — Fixes macOS gateway restarts when the LaunchAgent plist exists but the job is currently unloaded. Directly addresses Issue #42006.
- **[PR #43192] ** — `fix(gateway): strip orphan think-tag close tags in progressive stream` (by testingbuddies24) — Fixes leaked `</think>` tags in live Telegram edits when opening tags are stripped upstream.
- **[PR #42516] ** — Closed Issue: Desktop sessions appearing at bottom of sidebar — likely resolved by a related PR in the pipeline.
- **[PR #40998] ** — Closed Issue: Windows installer failure — resolved.

Additional significant open PRs that advanced today:
- **[PR #43223] ** — Prevents over-scanner false positives on script-injected cron output in no-skills jobs.
- **[PR #42890] ** — Fixes Gemini native resource model ID handling (`models/...`, `tunedModels/...`).
- **[PR #43222] ** — Escalates stale-stream kills to trigger provider fallback instead of silent retry loops.

## 4. Community Hot Topics

The following issues and PRs generated the most discussion today, revealing several underlying community needs:

- **[Issue #21587] ** **(9 comments)** — Telegram Guest Bots, Bot-to-Bot, Stickers and Chat Automation. This massive feature request references Telegram's May 7 AI bot update. The community is eager for Hermes to leverage Telegram's new guest bot, bot-to-bot messaging, and sticker automation APIs for multi-agent coordination. **Underlying need:** Users want Hermes agents to collaborate autonomously on Telegram without human intermediaries.

- **[Issue #43083] ** **(6 comments)** — Passwords replaced by `***` but model reads back its own conversation history and fails on second tool call. A security-sensitive bug where credential redaction in conversation history breaks tool workflows. **Underlying need:** Better credential lifecycle management — redact from persisted history but preserve in the live execution context.

- **[Issue #42006] ** **(5 comments)** — macOS `launchd_restart` missing `bootout` before `bootstrap`, gateway falls back to detached after update. Now fixed by PR #43181. **Underlying need:** Reliable OS-native service management on macOS during updates.

- **[Issue #13107] ** **(4 comments)** — Command description override via `config.yaml` for locale support. Users want i18n-friendly bot command descriptions on Telegram/Discord. **Underlying need:** Internationalization and localization of the Hermes agent's public-facing interfaces.

- **[Issue #42506] ** **(3 comments, closed)** — Add `usememos/memos` as an official memory provider plugin. Quickly closed, suggesting it was accepted or implemented. **Underlying need:** Users want lightweight, open-source memory backends as alternatives to heavy commercial options.

## 5. Bugs & Stability

### High Severity (P1)

- **[Issue #43083] ** — Password credential redaction in conversation history breaks second tool call. The model reads back its own redacted history and fails. **Fix status:** No PR yet, but the issue author (nnnarvaez) has identified the root cause in `chat_completion_helpers.py`.
- **[Issue #43014] ** — `cron: deliver=origin` fails to resolve delivery target in CLI sessions. Cron jobs generate output but cannot deliver it. **Fix status:** No PR yet.

### Medium Severity (P2)

- **[Issue #42006] ** — macOS launchd restart failure. **Fix status:** Fixed in PR #43181 (edufalcao), now merged.
- **[Issue #43175] ** — `session_search` discovery can rehydrate huge context-compaction summaries via bookends, causing massive token waste. **Fix status:** No PR yet.
- **[Issue #43026] ** — Gemini OpenAI-compatible provider returns HTTP 400/404 via Hermes' internal HTTP client but works with direct Python requests. **Fix status:** No PR yet.
- **[Issue #37968] ** — Cron gateway approvals isolated from environment pollution (security, CVSS 7.0/High). **Fix status:** No PR yet.
- **[Issue #43146] ** — Context-file scanner false positive: bare token `praxis` flagged as C2 framework pattern blocks entire files (German word for medical practice). **Fix status:** No PR yet.

### Lower Severity (P3)

- **[Issue #42992] ** — Desktop user message bubble hides additional prompt lines (visual clipping on macOS).
- **[Issue #42962] ** — Desktop active session does not refresh after update from Telegram gateway.
- **[Issue #43042] ** — Desktop file browser ENOENT after `session.info` event.
- **[Issue #43122] ** — Messaging provider icons not dark UI theme-friendly (Matrix, Slack).
- **[Issue #41744] ** — `auxiliary.title.enabled` config ignored — title generation runs regardless.
- **[Issue #42780] ** — `HERMES_DASHBOARD_PUBLIC_URL` not respected for self-hosted OIDC callback in Docker.
- **[Issue #34070] ** — Honcho memory prefetch hang on fresh CLI subprocess (regression from v0.15.0).

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release

- **Telegram AI Bot Integration** (Issue #21587) — Guest bots, bot-to-bot, stickers, and chat automation. Given the massive community interest (9 comments, Telegram's recent API update), this is a strong candidate for an upcoming sprint. **Prediction:** Expect a design doc or experimental implementation in v0.17.0.

- **`usememos/memos` Memory Provider** (Issue #42506, closed quickly) — Likely already implemented or accepted. Expect it in the next release.

- **Per-tool Enable/Disable** (Issue #31375, 2 comments, 1 reaction) — Users want sub-toolset granularity (e.g., enable `web_search` without `web_extract`). **Prediction:** May land as a config simplification in an upcoming minor release.

- **Command Description Override via Config** (Issue #13107) — i18n friendly bot commands. Moderate complexity, high value for multilingual users.

### Longer-Term Signals

- **Kanban Review Transition** (Issue #42896) — Users want a `request-review` lifecycle action for task workflows. Indicates growing enterprise/project-management usage.
- **Desktop Recency Sort** (Issue #42767) — Users with many sessions want "most recently used" at top. UI/UX polish item.
- **`execute_code` YOLO Mode** (Issue #42921) — Power users want to bypass all approval prompts, including code execution. Debate between security vs. developer experience.
- **Session Lineage in Hooks** (Issue #42939) — Developers want `parent_session_id` in shell-hook payloads for auditing session forks (compression, branching).

## 7. User Feedback Summary

### Pain Points

- **Credential handling is fragile** — Issue #43083: Redacting passwords from conversation history breaks tool workflows. A security UX tension.
- **Config ignored warnings** — Issues #41744 (title generation toggle) and #42780 (OIDC public URL): Users express frustration when explicit config settings are silently ignored.
- **Desktop ↔ Gateway sync broken** — Issues #42962 and #43042: The desktop app doesn't live-refresh when sessions are updated from other frontends (Telegram, CLI).
- **Ollama spinner timeout** — Issue #43028: Local model users find the persistent spinner disruptive; they want quieter operation.
- **macOS update pain** — Issue #42006: Update restarts fail cleanly, requiring manual intervention.

### Use Cases

- **Multi-agent Telegram collaboration** (Issue #21587): Users want Hermes agents to appear as bot participants in group chats, not just individual chat interfaces.
- **Internationalization** (Issue #13107): Non-English users want bot commands in their language on Telegram/Discord.
- **Lightweight memory backends** (Issue #42506): Users want open-source, self-hosted memory providers (Memos) over cloud APIs.
- **Cron diagnostics** (Issue #43168): Users want richer failure notifications with provider/model/token context — not just bare exception messages.

### Satisfaction Signals

- High community engagement: 50 issues and 50 PRs updated in 24h shows active use.
- Quick closure of Issue #42506 (usememos memory provider) suggests good maintainer responsiveness.
- New contributor PRs (e.g., #43183 by ingo152, #43187 by Tranquil-Flow) indicate a welcoming project.

## 8. Backlog Watch

### Issues Needing Maintainer Attention

- **[Issue #7507] ** — `feat(matrix): add configurable reply quoting for group chats` (Created: 2026-04-11, last updated today, 2 comments). This has been open for 2 months with no PR. The `m.in_reply_to` clutter in Matrix group chats is a long-standing pain point.

- **[Issue #34070] ** — `Honcho memory prefetch hang on fresh CLI subprocess` (Created: 2026-05-28, last updated today, 2 comments). A v0.15.0 regression that hangs cron jobs and subprocess dispatchers. No fix PR in sight.

- **[Issue #37968] ** — `fix(cron): isolate gateway approvals from environment pollution` (Created: 2026-06-03, 1 comment). Security issue rated CVSS 7.0 (High) with no PR activity. This should be prioritized.

- **[Issue #40998] ** — Windows installer failure (Created: 2026-06-07, now closed). The fix worked, but the root cause for Windows installation errors may still affect other users.

### PRs Needing Review

- **[PR #43185] ** — `fix(delegate_tool): address PR #43134 multi-provider review feedback` — A follow-up to an 8-reviewer code review. This needs timely attention to land the delegate tool feature.
- **[PR #43195] ** — `chore: bundle of local patches` — Contains 5 fixes (Anthropic MiniMax auth, cron exit codes, telegram stop_typing, shutdown_forensics, TTS). Should be reviewed and merged to unblock downstream work.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-10

## Today's Overview
PicoClaw is in a phase of **high security-focused development**, with a major coordinated vulnerability disclosure (17 new security issues filed today by a single researcher) dominating the activity. Overall project activity is very high (20 issues, 19 PRs, 1 release in 24h), but the signal is heavily weighted toward defensive hardening rather than feature growth. A new nightly build (v0.2.9-nightly.20260610) was published, though marked as potentially unstable. The maintainer team is responding quickly, with several fix PRs already opened for the reported vulnerabilities.

## Releases
**Nightly build v0.2.9-nightly.20260610.b9a8fad6** published — automated, unstable, use with caution. No breaking changes or migration notes provided. Changelog: [v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)

## Project Progress
**Merged/closed PRs today (5 items):**
- [#3064](https://github.com/sipeed/picoclaw/pull/3064) — `fix(config): add ok check for type assertion in migration model name indexing` — prevents panic on malformed config (merged)
- [#2942](https://github.com/sipeed/picoclaw/pull/2942) — `fix(config): use canonical hyphenated model ID for default claude-sonnet entry` — fixes first-message failure for default Anthropic config (closed, stale)
- [#2940](https://github.com/sipeed/picoclaw/pull/2940) — `fix(providers): omit temperature for claude-opus-4-7` — resolves HTTP 400 error for deprecated parameter (closed, stale)
- [#2937](https://github.com/sipeed/picoclaw/pull/2937) — `Feat/agent collaboration` — major feature: inter-agent communication bus with mailboxes, collaboration threads, permission-aware routing (closed, stale)
- [#3086](https://github.com/sipeed/picoclaw/pull/3086) — `docs: update wechat qrcode` — minor documentation update (merged)

Additionally, several **security fix PRs were opened today** in response to vulnerability reports (listed in Bugs & Stability).

## Community Hot Topics
1. **[#2404](https://github.com/sipeed/picoclaw/issues/2404) (OPEN, 11 comments, 1 👍)** — Feature request: streaming HTTP requests to LLM backends (e.g., `"streaming": true` in config). Highest-comment issue; demonstrates strong demand for real-time output from OpenAI-compatible providers.

2. **[#2796](https://github.com/sipeed/picoclaw/issues/2796) (CLOSED, 6 comments)** — Bug: session history only shows last user message, earlier messages hidden. Addressed by PR [#2990](https://github.com/sipeed/picoclaw/pull/2990) (still open, stale). This was a significant UX pain point for Chinese-speaking users.

3. **[#2984](https://github.com/sipeed/picoclaw/issues/2984) (OPEN, 1 comment, 1 👍)** — Feature request: explicit turn completion signal for Pico WebSocket clients. External protocol clients need deterministic end-of-turn detection.

**Underlying need**: Community is pushing for better **protocol interoperability** (streaming, WebSocket signals) and **stable UX** (session history visibility). The agent collaboration PR (#2937) suggests internal architecture is evolving toward multi-agent setups.

## Bugs & Stability
**High severity — coordinated security disclosure (17 issues):**
All filed by researcher YLChen-007 on 2026-06-09. Multiple SSRF bypasses, auth bypasses, and privilege escalation vectors:

- **SSRF in `web_fetch`** — 3 bypass methods: ISATAP IPv6 literals ([#3074](https://github.com/sipeed/picoclaw/issues/3074)), `198.18.0.0/15` benchmark range ([#3077](https://github.com/sipeed/picoclaw/issues/3077)), environment proxy bypass ([#3078](https://github.com/sipeed/picoclaw/issues/3078)) — **Fix PR [#3085](https://github.com/sipeed/picoclaw/pull/3085) blocks 198.18.0.0/15**
- **Launcher access control bypass** — loopback proxying bypasses `allowed_cidrs` ([#3080](https://github.com/sipeed/picoclaw/issues/3080)), reverse proxy `RemoteAddr` trust ([#3069](https://github.com/sipeed/picoclaw/issues/3069)) — **Fix PR [#3083](https://github.com/sipeed/picoclaw/pull/3083) hardens access control**
- **CSRF on first-run password setup** ([#3072](https://github.com/sipeed/picoclaw/issues/3072)) — allows local control-plane takeover
- **WeCom group trigger policy bypass** ([#3076](https://github.com/sipeed/picoclaw/issues/3076)) — unmentioned group messages reach agent
- **MQTT `allow_from` spoofing** ([#3068](https://github.com/sipeed/picoclaw/issues/3068)) — topic `client_id` can be forged
- **LINE webhook replay** ([#3073](https://github.com/sipeed/picoclaw/issues/3073)) — duplicate event execution
- **`exec` tool vulnerabilities** — symlink race in approval hook ([#3081](https://github.com/sipeed/picoclaw/issues/3081)), `jq` environment disclosure via whitelist ([#3079](https://github.com/sipeed/picoclaw/issues/3079))
- **Feishu `allow_from` bypass** for fetched parent messages ([#3082](https://github.com/sipeed/picoclaw/issues/3082))
- **OneBot media URL arbitrary fetch** ([#3070](https://github.com/sipeed/picoclaw/issues/3070))
- **Local `skills/` auto-loading into system prompt** ([#3075](https://github.com/sipeed/picoclaw/issues/3075))
- **Authenticated WebSocket `/reload` unauthorized config reload** ([#3071](https://github.com/sipeed/picoclaw/issues/3071))

**Medium severity — other bugs fixed today:**
- **Config migration panic** ([#3064](https://github.com/sipeed/picoclaw/pull/3064)) — fixed unchecked type assertion
- **Executor workspace path false positive** ([#3087](https://github.com/sipeed/picoclaw/pull/3087), OPEN) — relative paths like `skills/calendar-query/...` falsely blocked
- **Windows console flash** ([#3061](https://github.com/sipeed/picoclaw/pull/3061), OPEN) — child process windows visible in GUI mode; follow-up to PR #2654
- **Session scope not saving** ([#3067](https://github.com/sipeed/picoclaw/pull/3067), OPEN) — `dm_scope` UI setting always reverts to default

**Stale bugs with pending fixes:**
- [#2796](https://github.com/sipeed/picoclaw/issues/2796) session history truncation — PR [#2990](https://github.com/sipeed/picoclaw/pull/2990) open 8 days
- [#2939](https://github.com/sipeed/picoclaw/issues/2939) `claude-opus-4-7` temperature deprecation — PR [#2940](https://github.com/sipeed/picoclaw/pull/2940) merged but stale
- [#2958](https://github.com/sipeed/picoclaw/issues/2958) tool_calls dropped during streaming — PR [#2987](https://github.com/sipeed/picoclaw/pull/2987) open 8 days
- Empty LLM response retry gap — PR [#2983](https://github.com/sipeed/picoclaw/pull/2983) open 9 days

## Feature Requests & Roadmap Signals
**Likely next-version candidates:**
1. **[#3088](https://github.com/sipeed/picoclaw/issues/3088)** — Replace `libolm` with `vodozemac` (official, maintained replacement). Low risk, high security value — likely fast-tracked.
2. **[#3063](https://github.com/sipeed/picoclaw/pull/3063)** — DeltaChat gateway (OPEN, 1 day old). Expands channel diversity; aligns with multi-channel architecture.
3. **[#2404](https://github.com/sipeed/picoclaw/issues/2404)** — Streaming HTTP requests. High community interest (11 comments). Could appear as config option in v0.2.10.
4. **[#2984](https://github.com/sipeed/picoclaw/issues/2984)** — Explicit turn completion signal for WebSocket. Important for external client developers.
5. **[#2917](https://github.com/sipeed/picoclaw/pull/2917)** — NEAR AI Cloud provider (stale, 20 days open). TEE-capable model support may interest enterprise users.

**Longer-term roadmap signal:** PR [#2937](https://github.com/sipeed/picoclaw/pull/2937) (Agent Collaboration Bus, now closed/merged) suggests PicoClaw is building toward **multi-agent orchestration as a core capability**.

## User Feedback Summary
**Satisfaction signals:**
- Agent collaboration PR merged — community contributors actively building multi-agent features
- Security researchers investing time in responsible disclosure (17 issues from one researcher)
- Fast maintainer response: multiple security fix PRs opened same day as disclosure
- Config migration fix merged same day as report

**Dissatisfaction signals:**
- **Session history truncation** ([#2796](https://github.com/sipeed/picoclaw/issues/2796)) — Chinese-speaking users frustrated that multi-message conversation history is broken in UI. Fix PR open 8 days, not yet merged.
- **Claude Opus 4-7 temperature error** ([#2939](https://github.com/sipeed/picoclaw/issues/2939)) — default config fails on first message. Fixed but via stale PR.
- **Context compression config ignored** ([#2968](https://github.com/sipeed/picoclaw/issues/2968)) — `/context` command shows wrong token limit regardless of settings. PR [#2988](https://github.com/sipeed/picoclaw/pull/2988) open 8 days.
- **Streaming dropout** ([#2958](https://github.com/sipeed/picoclaw/issues/2958)) — tool_calls lost during active streams. PR [#2987](https://github.com/sipeed/picoclaw/pull/2987) open 8 days.
- **Session scope setting unsaveable** ([#3067](https://github.com/sipeed/picoclaw/pull/3067)) — config UI bug where `dm_scope` always reverts; new fix PR opened today.

**Pain point pattern**: Multiple UX regressions in session management (history, scope, context display) suggest recent refactoring introduced several interacting bugs that remain unresolved for over a week.

## Backlog Watch
**Issues needing maintainer attention:**
- **[#2404](https://github.com/sipeed/picoclaw/issues/2404)** (OPEN, 64 days old) — Streaming HTTP request feature. 11 comments, only 1 reaction. High-value feature with clear demand but no assignee or linked PR.
- **[#2796](https://github.com/sipeed/picoclaw/issues/2796)** (CLOSED as stale, 34 days old) — Session history truncation. PR [#2990](https://github.com/sipeed/picoclaw/pull/2990) open 8 days, no merge activity. Core UX regression.
- **[#2917](https://github.com/sipeed/picoclaw/pull/2917)** (OPEN, 20 days old, stale) — NEAR AI Cloud provider. No reviewer activity. May be waiting for architecture alignment.
- **[#2984](https://github.com/sipeed/picoclaw/issues/2984)** (OPEN, 8 days old) — WebSocket turn completion signal. Only 1 comment from author, no response from maintainers. Community proposal may need design sign-off.
- **Stale PRs cluster (5 items)** — PRs [#2983](https://github.com/sipeed/picoclaw/pull/2983), [#2987](https://github.com/sipeed/picoclaw/pull/2987), [#2988](https://github.com/sipeed/picoclaw/pull/2988), [#2990](https://github.com/sipeed/picoclaw/pull/2990), [#2917](https://github.com/sipeed/picoclaw/pull/2917) all 8-20 days old with no maintainer review. This suggests maintainer bandwidth is constrained despite high issue throughput.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-10

## Today's Overview
NanoClaw saw high activity today with **43 pull requests updated**, of which **39 were merged or closed** — signaling a major backlog cleanup or release preparation cycle. Only **1 open issue was updated**, indicating that issue triage may be lagging behind PR velocity. No new releases were published, so these merged changes remain unreleased on the main branch. The project appears to be in a **consolidation phase** after a long feature-development push, with maintainers focusing on merging stalled PRs and fixing production bugs.

## Releases
**None** — No new releases were cut today. Significant merged work (security fixes, observability features, sandbox design docs) is waiting for a release tag.

## Project Progress
**39 PRs were merged or closed today**, spanning several major themes:

### Security & Production Fixes (Merged)
- **#2718** — `fix(feishu): cleanup zombie active_cards when agent-runner exits abnormally` — Fixes a real production bug where Feishu interactive cards showed "running" state for 50+ minutes after process timeout.
- **#2722** (Open) — `fix(telegram): use CSPRNG for pairing codes and lock down store permissions` — Security fix switching from `Math.random` to `crypto.randomInt` for pairing codes. Not yet merged.

### Observability & Infrastructure (Merged)
- **#1202** — Adds agent trace observability with a lightweight Web UI on port 3001, capturing every agent invocation, tool call inputs/outputs, and token counts.
- **#337** — Prompt trace logging for internal/external flows to JSONL files with configurable redaction.
- **#1333** — Build-time version metadata (git commit, branch, timestamp) added to logs for debugging.

### Skills & Extensibility (Merged)
- **#1309** — Skill Marketplace/Registry System — CLI commands to discover, install, and manage skills from GitHub-hosted repos.
- **#1245** — `/approve` and `/reject` skills for approval-gated capabilities.
- **#1387** — Plugin system analogous to channels (feature skill).
- **#1161** — `/setup-dev` skill for local development environment setup.

### Runner & Deployment (Merged)
- **#1285** — Direct runner mode (no Docker containers), with backward compatibility via `NANOCLAW_DIRECT_RUNNER=1` env var.
- **#1192** — Explicit Claude model configuration in code (simplification fix).
- **#212** — WebUI control panel at `localhost:3100` (Lit + Vite + Fastify) — 11 tabs across 4 groups. *This PR was blocked/pending closure and finally merged.*

### Documentation (Merged)
- **#2721** (Open) — Three new docs defining the skills-based customization contract (`customizing.md`, skills model, guidelines).
- **#1084** — NanoClaw Container Sandbox System design document.
- **#214** — Comprehensive security audit documentation (Trivy findings, SDK credential isolation).

### Other Features & Integrations (Merged)
- **#1527** — Room API proxy for music-gen and facebook services.
- **#357** — External markdown seed file support for persistence context.
- **#481** — Example structure for group-level CLAUDE.md files.

## Community Hot Topics

### Most Active Issue
- **[#1690 — Multi-runtime agent SDK abstraction (Claude + Codex + local models)](https://github.com/nanocoai/nanoclaw/issues/1690)** — 5 comments, 3 👍
  - **Analysis**: This issue proposes a plugin-style abstraction for multiple agent runtimes, mirroring the existing channel pattern. The 3 upvotes suggest strong interest in vendor-neutral agent backends. The underlying need is **avoiding lock-in to Claude while preserving NanoClaw's architecture** — users want to swap in Codex, local models, or future SDKs without rewriting integrations.

### Most Active PRs (by comment count)
- **#2722** — Telegram CSPRNG fix (security-critical, still open)
- **#2721** — Skills customization docs (still open)
- **#212** — WebUI control panel (finally merged after months of blocked status)

## Bugs & Stability

### High Severity
- **Feishu zombie cards (PR #2718, merged)** — Production bug where cards showed stale "running" state for 50+ minutes after agent-runner process timeout. **Fix merged today.**
- **Telegram pairing code predictability (PR #2722, open)** — `Math.random` used for pairing codes that gate owner-level access. CSPRNG fix proposed but **not yet merged** — this is a security vulnerability with active risk.

### Medium Severity
- **Agent trace observability (PR #1202, merged)** — Previously, no way to debug agent invocations. Now addressed.
- **Version metadata missing from logs (PR #1333, merged)** — Previously made debugging difficult. Now addressed.

### No new bugs reported today
The single open issue (#1690) is a feature request, not a bug report.

## Feature Requests & Roadmap Signals

### High Likelihood for Next Release
1. **Multi-runtime agent SDK support** — Issue #1690 is the top-voted open issue. The skills-based pattern is already established; this would extend it to agent backends.
2. **Skill Marketplace** (PR #1309, merged) — Ready for release; provides CLI-based skill discovery from GitHub repos.
3. **Direct runner mode** (PR #1285, merged) — Docker-less operation will be a major quality-of-life improvement for local dev.

### Medium Likelihood
4. **WebUI control panel** (PR #212, merged) — A full dashboard for chat, channels, tasks, skills, config, and logs.
5. **Agent trace observability** (PR #1202, merged) — Debugging and monitoring dashboard.

### Lower Likelihood / Long-term
6. **Plugin system** (PR #1387, merged) — Extends channels pattern to arbitrary integrations.
7. **Approval-gated capabilities** (PR #1245, merged) — Workflow control for sensitive operations.

**Prediction**: The next release (likely v0.9 or v1.0-beta) will focus on **operational maturity** — merging the security fixes (#2722), the WebUI, skill marketplace, and direct runner mode into a coherent release with the new documentation.

## User Feedback Summary

### Pain Points Expressed
- **Docker overhead** — PR #1285 directly responds to users wanting to run without containers for speed and simplicity.
- **Observability gaps** — "hard to find out which model is being used" (PR #1192) and lack of traceability (PR #1202) were concrete pain points.
- **Merge conflicts on updates** — The customization docs (PR #2721) explicitly cite "merge fights on update" as a user problem that skills-based customization solves.
- **Security concerns** — The Telegram pairing code fix (#2722) suggests users are security-conscious and have found vulnerabilities in production use.

### Satisfaction Signals
- The **skill marketplace** and **plugin system** suggest a healthy ecosystem desire — users want to extend NanoClaw without forking.
- **High PR velocity** (43 PRs updated in 24h, 39 merged) indicates an active, engaged contributor base.
- **Production deployments** are confirmed by the Feishu zombie card bug report — users are running NanoClaw in real environments at scale.

## Backlog Watch

### Open Issues Needing Maintainer Attention
- **[#1690 — Multi-runtime agent SDK abstraction](https://github.com/nanocoai/nanoclaw/issues/1690)** — Opened 2026-04-07, 5 comments, 3 👍. No maintainer response visible. This is a **strategic feature request** with community support that merits a design review.
- **[#2722 — Telegram CSPRNG fix](https://github.com/nanocoai/nanoclaw/pull/2722)** — Open since 2026-06-09, security-critical, no merge yet. **Action recommended**: Review and merge promptly.
- **[#2721 — Skills customization docs](https://github.com/nanocoai/nanoclaw/pull/2721)** — Open since 2026-06-09, adds critical developer documentation. **Review needed.**

### Recently Closed Items of Note
- **PR #212** (WebUI) was blocked/closed and re-opened multiple times before today's merge — this pattern suggests coordination challenges that may benefit from a project board update.
- **Several PRs** show combined `Status: Blocked, Status: Pending Closure` labels (e.g., #214, #337, #357, #380) — suggests the maintainers did a **bulk sweep** of stalled work today.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-06-10**.

---

## NullClaw Project Digest – 2026-06-10

### 1. Today's Overview
The project shows **high maintainer activity** with 8 pull requests updated and 5 issues updated in the last 24 hours. Seven PRs were merged or closed, and four issues were resolved, indicating a strong push to clear technical debt and fix user-reported bugs. While no new releases were published, the volume of merged fixes—spanning redaction false positives, provider model discovery, and Telegram UX—suggests the team is preparing for a stable point release in the near future. The remaining open issue (#941) regarding cron agent subprocess spawning is a notable gap that still requires resolution.

### 2. Releases
**None.** No new tags or releases were created in the last 24 hours.

### 3. Project Progress
Seven PRs were closed or merged today, advancing the following areas:

- **PR #945 (merged)** – Fixes a critical false-positive bug in the PII redactor where ISO date/time strings (e.g. `2026-06-02 20:17`) were erroneously flagged as phone numbers and redacted as `[PHONE_X]`.
- **PR #946 (merged)** – Improves the agent system prompt by filtering which tools are included in the text-based prompt based on `tool_filter_groups`, reducing prompt bloat while preserving full function-calling capability for dynamic MCP tools.
- **PR #947 (merged)** – Adds Evolink as a first-class OpenAI-compatible provider, expanding multi-model gateway support (GPT-5, Gemini, DeepSeek, etc.) via a single endpoint.
- **PR #943 (merged)** – Fixes the missing "typing…" indicator in Telegram when inline buttons (`callback_query`) are pressed, improving UX for interactive choice flows.
- **PR #940 (merged)** – Fixes the `/models` menu for custom OpenAI-compatible providers: instead of showing a hardcoded fallback of Claude models, the system now correctly queries the provider's `/v1/models` endpoint.
- **PR #939 (merged)** – Resolves the dead `compact_context` flag in agent config; the runtime now actually reads and honors this flag instead of always compacting context.
- **PR #711 (merged)** – A cross-memory event stream feature, allowing memory synchronization across agent instances (merged from prior work, updated recently).

### 4. Community Hot Topics
- **Issue #941 (Open) – "Agent-type cron jobs don't spawn a subprocess"**  
  *Author: weissfl | 1 comment*  
  This is the only remaining open issue updated in the last 24h. The user reports that scheduled agent jobs are marked complete but the subprocess never starts, so no Telegram message arrives. A fix PR (#948) is open but not yet merged.  
  **Underlying need:** Users require reliable, auditable execution of scheduled agent tasks—this is a foundational workflow feature.

- **PR #948 (Open) – "fix cron agent delivery attribution"**  
  *Author: DonPrus | No comments yet*  
  This PR directly addresses Issue #941 by passing delivery metadata into spawned agent subprocesses and preserving routing flags. Its success will determine whether cron agents are functional or broken for a key use case.

- **Issue #944 (Closed) – "PII redactor falsely matches date/time output as phone numbers"**  
  *Author: vernonstinebaker | 0 comments*  
  Although closed, this issue drew attention because it caused silent data loss: agents running `date` commands would see `[PHONE_X]` instead of timestamps. The fix (#945) was merged quickly, indicating high sensitivity to data integrity.

### 5. Bugs & Stability
| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **High** | #941 | Cron agent subprocess never spawns; delivery never happens | PR #948 (open) |
| **Medium** | ~~#944~~ | PII redactor corrupts date/time output with false phone matches | PR #945 (merged) |
| **Medium** | ~~#942~~ | Missing Telegram typing indicator on inline button presses | PR #943 (merged) |
| **Low** | ~~#936~~ | Custom OpenAI providers show hardcoded Claude models in `/models` | PR #940 (merged) |
| **Low** | ~~#937~~ | `compact_context` flag parsed but never used | PR #939 (merged) |

**Key stability observations:**
- The cron agent bug (#941) is the last unresolved stability issue and is **actively being worked on**.
- The PII redactor regression (#944) was a silent data corruption bug that could affect any agent using system tools that emit dates; it has been fixed.
- All other reported regressions from the last two weeks now have merged fixes.

### 6. Feature Requests & Roadmap Signals
- **Evolink provider (PR #947):** The addition of Evolink as a first-class provider signals that the team is prioritizing **multi-model gateway flexibility**. This aligns with a broader industry trend toward vendor-agnostic model access and suggests the roadmap may include more such providers (e.g., OpenRouter, Together AI).
- **Cross-memory synchronization (PR #711):** The recent update to this long-running PR suggests that **multi-agent memory sharing** is nearing production readiness. This is a major feature for users running multiple agents who want persistent shared context.
- **Cron agent delivery (PR #948):** While a fix, this also reveals a **feature gap**: scheduled agent tasks need proper delivery attribution and channel awareness. Future versions may formalize a "cron agent" lifecycle with dedicated logging and retry logic.

**Prediction:** The next minor release will likely bundle the Evolink provider, cross-memory support, and the cron agent fix under a single version bump (e.g., v0.7.x or a patch release).

### 7. User Feedback Summary
- **Pain point: Silent task failures.** The cron agent issue (#941) highlights a recurring theme: users cannot easily tell if a scheduled task actually ran. The task is marked "completed" without confirmation of delivery.
- **Pain point: Data integrity / false positives.** The PII redactor bug (#944) caused frustration because date/time outputs were silently corrupted. Users need confidence that redaction does not break agent functionality.
- **Satisfaction: Responsive fix turnaround.** Multiple users (weissfl, raskevichai, vernonstinebaker) reported bugs that were fixed and merged within 1–3 days, suggesting the maintainer team is responsive and values community reports.
- **Use case: Multi-model gateways.** The addition of Evolink (PR #947) suggests users want to switch between GPT-5, DeepSeek, Gemini, and others from a single configuration, reducing dependency lock-in.

### 8. Backlog Watch
- **PR #711 (Feat/cross memory):** This PR was created on 2026-03-23 and only saw its most recent update on 2026-06-09. It has been in progress for nearly three months. While it is now merged, its long idle period may mean integration with existing memory systems was complex. No remaining blockers are evident, but the team should monitor for regressions in memory event streaming.
- **Issue #941 (Cron agent subprocess):** This is the top-priority item needing maintainer attention. While a fix PR (#948) is open, it has not yet been merged. If the PR stalls, the cron agent feature is effectively broken for all users.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-10

## Today's Overview

IronClaw shows very high activity today with 48 updated issues (43 open) and 50 updated pull requests (45 open), indicating a major development push. The project remains in an intense pre-production phase, with the "Reborn" architecture transition dominating the roadmap — particularly the epic #3026 tracking production cutover readiness. The team is simultaneously advancing the WebUI v2 browser-driven smoke coverage (#4632), building out Slack channel routing (#4625), and addressing critical bugs affecting first-party tools and provider compatibility. No new releases were published today, as effort is concentrated on stabilization and feature completion ahead of the Reborn production milestone.

## Releases

No new releases today. The last release candidate (PR #3708) — which would bump `ironclaw_common` to 0.5.0 and `ironclaw` to 0.29.1 with breaking changes — remains open and unmerged.

## Project Progress

**Merged/Closed PRs today (5):**
- **#4669** — Added "thermo-nuclear code quality review" skill for aggressive maintainability auditing (merged)
- **#4668** — MountView-based attachment landing crate for byte storage (Track 6 of #4644) (open, active)

*Note: No PRs were explicitly reported as merged in the 24-hour window, suggesting many are still under review.*

**Closed Issues today (5):**
- **#4604** — Reborn WebUI v2 E2E task (closed, presumably tracked elsewhere)
- **#4609** — Reborn WebUI Beta auth parity audit (closed)
- **#4591** — Operator command-plane foundation for Reborn setup/config APIs (closed)
- **#4447** — Close OpenAI-compatible API migration with compatibility tests (closed)
- **#4446** — Translate projection streams to OpenAI-compatible SSE (closed)

**Advanced features in active PRs:**
- **#4664** — Project vocabulary rename on product surface (XL refactor)
- **#4663** — Project-scoped automation ownership core model
- **#4662** — Design docs for project-scoped ownership plan
- **#4671** — Extra-capabilities seam for host-supplied tools
- **#4654** — Extensible attachment format registry (first track of #4644)
- **#4670** — Bridge inbound bytes into transcript AttachmentRefs
- **#4661** — Read-only NEAR mainnet first-party extension (new contributor)
- **#4600** — Slack personal DM outbound targets
- **#4588** — Observability seams: trajectory observer + LLM provider injection
- **#4559** — Agent-driven Trace Commons onboarding via invite link
- **#4561/#4562/#4565/#4563** — Series of security audit sink improvements for MCP denials, auth failures, egress blocks

## Community Hot Topics

**Most Active Discussions:**

1. **#3026 — Epic: Reborn production wiring and cutover readiness** (3 comments)
   - The central tracking issue for the production cutover — defines how the production graph is built, validated, reported, and traffic-gated. Multiple child issues (#4551, #4621) are actively being worked.
   - *Link: [Issue #3026](https://github.com/nearai/ironclaw/issues/3026)*

2. **#4642 — Strict-mode providers' null-for-unset-optionals rejected by capability-port validation** (1 comment)
   - Affects **most first-party tools** — when LLM providers leave optional parameters unset and send `null`, the Reborn validator rejects them against non-nullable schemas. This is a high-severity regression.
   - *Link: [Issue #4642](https://github.com/nearai/ironclaw/issues/4642)*

3. **#4551 — Reborn: wire production Postgres storage config** (1 comment)
   - Child of #3026 — PostgreSQL support exists behind feature flags but the standalone binary doesn't expose it. Blocks production deployment.
   - *Link: [Issue #4551](https://github.com/nearai/ironclaw/issues/4551)*

4. **#4548 — Chat completion request serializes duplicate top-level `model` field (DeepSeek 400)** (1 comment)
   - DeepSeek API rejects requests with duplicate `model` fields when tools are included. Affects all DeepSeek users.
   - *Link: [Issue #4548](https://github.com/nearai/ironclaw/issues/4548)*

5. **#4587 — Cannot configure Minimax provider** (1 comment)
   - Secret store key metadata corruption prevents Minimax provider from working.
   - *Link: [Issue #4587](https://github.com/nearai/ironclaw/issues/4587)*

6. **#4585 — Reborn auth evidence should carry tenant identity** (1 comment)
   - Tenant-aware validation impossible because `VerifiedAuthClaim` lacks tenant identity — follow-up from review.
   - *Link: [Issue #4585](https://github.com/nearai/ironclaw/issues/4585)*

7. **#4591 — Operator command-plane foundation** (closed, 0 comments, but high impact)
   - Foundation for setup/config/diagnostics APIs — just closed, indicating progress.

## Bugs & Stability

**High Severity (blocks normal usage):**

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#4642](https://github.com/nearai/ironclaw/issues/4642) | Strict-mode providers' null-for-optionals rejected by capability-port validation — affects most first-party tools | No fix PR yet |
| [#4548](https://github.com/nearai/ironclaw/issues/4548) | DeepSeek API HTTP 400: duplicate `model` field in request body when tools included | No fix PR yet |
| [#4587](https://github.com/nearai/ironclaw/issues/4587) | Minimax provider cannot be configured; secret key metadata corruption error | No fix PR yet |

**Medium Severity (degraded experience):**

| Issue | Description | Fix PR? |
|-------|-------------|---------|
| [#4640](https://github.com/nearai/ironclaw/issues/4640) | `google-calendar list_events` returns oldest/unordered events — no `timeMin`, missing `singleEvents`/`orderBy` | No fix PR yet |
| [#4666](https://github.com/nearai/ironclaw/issues/4666) | `slack_host_state.rs` at 2,823 lines — approaching file-size cap | Tracking issue only |
| [#4665](https://github.com/nearai/ironclaw/issues/4665) | `slack_host_beta.rs` at 3,359 lines — over file-size budget | Tracking issue only |

**Stability concern:** Three critical provider regressions are unresolved simultaneously, which could block users on DeepSeek, Minimax, and any strict-mode provider (most major providers). No fix PRs are linked to any of these issues yet.

## Feature Requests & Roadmap Signals

**High-likelihood for next release:**
1. **Unified attachments** (#4644) — Multiple PRs already in flight (#4654, #4668, #4670) covering format registry, byte storage, and transcript integration. Likely to land soon.
2. **Project-scoped automation ownership** (#4662 plan, #4663 core model, #4664 surface rename) — Stacked PRs in active review.
3. **Slack channel-routed agents** (#4625) — Personal and team agent routing in Slack. Active development with #4600 already implementing personal DM targets.
4. **Admin-shared tools and skills** (#4628) — Multi-tenant tool provisioning. High business value, tracked as P1.
5. **Observability seams** (#4588, #4671) — Trajectory observer and extra-capabilities hooks for external hosts (nearai-bench). Near completion.

**Medium-likelihood:**
6. **Unified omni-search** (#4647) — Search across threads, skills, extensions, and memory. Early stage.
7. **Universal WebUI management surface** (#4635) — Extensions, skills, LLM config, automations in WebUI v2.
8. **Reborn WebUI v2 SSO** (#4636) — Multi-user authentication support.
9. **Read-only NEAR mainnet extension** (#4661) — New contributor, first-party extension in review.

**Predictions:** The next release will likely include the attachment format registry, project-scoped ownership model, Slack personal DM routing, and the observability seams — all have active, near-complete PRs. The Reborn production cutover (#3026) is the primary gate for a major release.

## User Feedback Summary

**Pain points reported today:**
- **Provider incompatibility** is the most pressing user-facing issue. DeepSeek users get HTTP 400 on tool calls (#4548). Minimax users get config errors (#4587). Any strict-mode LLM provider breaks with optional parameters (#4642).
- **Google Calendar useless by default** (#4640) — "what are my upcoming meetings?" returns the oldest events due to missing defaults. This is a poor first impression for users evaluating the Google/GSuite integration.
- **Google OAuth re-authentication frustration** (#4657) — Users complete OAuth consent but still hit auth gates for different Google APIs, creating a confusing experience.
- **Attachments silently dropped on Reborn** (#4644) — Users attaching files to Reborn conversations get no feedback that content is lost.

**Satisfaction signals:**
- **New contributor** (#4661, abbyshekit) submitted a NEAR mainnet first-party extension, suggesting the project has good contributor onboarding.
- **Trace Commons onboarding** (#4559) is being streamlined from a complex CLI flow to a simple invite-link paste, indicating responsiveness to UX feedback.
- **Security audit** improvements (#4561, #4562, #4563, #4565) suggest the team is prioritizing enterprise-grade audit logging.

## Backlog Watch

**Long-standing issues needing attention:**
- **#88 — Security hardening (device pairing, elevated mode, safe bins, media URL validation)** — Created 2026-02-14 (nearly 4 months ago), last updated today but with no resolution. Priority P2-P3 but covers fundamental security features from the OpenClaw parity list.
- **#3708 — Release PR** — Open since 2026-05-16 (25 days). Breaking changes to `ironclaw_common` (0.4.2→0.5.0) and `ironclaw_skills` (0.3.0→0.4.0) are blocked. This is the only path to getting bug fixes and improvements to users.
- **#3026** — The Reborn production epic has been open since 2026-04-28 (43 days) with deep dependencies (#4551, #4621 and others). While active, its age reflects the complexity and risk of the cutover.

**Items needing maintainer response:**
- **#4667** — "Support Ask-gated capability approvals in Reborn REPL" — Filed today, zero comments. The Reborn REPL cannot surface or resolve host approval requests for capabilities whose manifest default is `Ask`. This is a critical gap for interactive use of the Reborn CLI.
- **#4585** — "Reborn auth evidence should carry tenant identity" — Follow-up from code review. Open 1 day, but tenant-aware validation is foundational for multi-tenant deployments.

**Observation:** The release backlog (#3708) is the most concerning — 25 days open with breaking changes. Users and contributors are waiting on a release that includes the new features and bug fixes merging daily. The team should consider either merging it or creating a smaller point-release in the meantime.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-10**, based exclusively on the provided GitHub data.

---

## LobsterAI Project Digest – 2026-06-10

### 1. Today's Overview
Today marks a high-velocity day for LobsterAI, driven primarily by a robust PR cycle. The team merged/closed **4 pull requests** while only **1 remains open**, indicating strong momentum toward completing the current feature batch. The most significant push was the finalization of a **task completion notification system** and the initial implementation of **data backup and migration** capabilities. Community activity remains moderate, with two open issues—one probing future agent support and the other diagnosing a complex cross-model coordination bug. No new releases were cut today.

---

### 2. Releases
No new releases today.

---

### 3. Project Progress (Merged/Closed PRs)
Four PRs were successfully merged or closed today, advancing three key areas:

- **Feature: Task Completion Notifications**  
  [#2130 – feat(cowork): add task completion notifications](https://github.com/netease-youdao/LobsterAI/pull/2130) (Merged)  
  - Adds privacy-safe reminder notifications for Cowork sessions when LobsterAI is backgrounded.  
  - Includes a General settings toggle, macOS Dock badges, Windows taskbar overlay, and ensures no task titles or prompts are exposed.  
  - Building on this, [#2134 – Liuzhq/task complete notice](https://github.com/netease-youdao/LobsterAI/pull/2134) (Merged) restores the app window from a notification if it was destroyed/closed and fixes interaction reliability with macOS Notification Center.

- **Feature: Data Backup and Migration**  
  [#2136 – feature: data backup and migration](https://github.com/netease-youdao/LobsterAI/pull/2136) (Merged)  
  - Initial implementation of a backup/migration system spanning renderer, docs, and main processes.  
  - A subsequent temporary close [#2135 – chore: temporary close databackup](https://github.com/netease-youdao/LobsterAI/pull/2135) (Merged) suggests the team is gating this feature; it may have been merged to a dev branch but not yet enabled in production.

- **Bug Fix (Open PR):**  
  [#2133 – fix: fix export and code copy bugs](https://github.com/netease-youdao/LobsterAI/pull/2133) (Open) – Not yet merged; addresses export and code copy regressions.

---

### 4. Community Hot Topics

- **Most Active Issue: Cross-Model Sub-Task Coordination**  
  [#2132 – 跨模型子任务调用的问题](https://github.com/netease-youdao/LobsterAI/issues/2132)  
  *Author: woxinsj*  
  This issue details a deep investigation into a sub-task coordination bug. The user identified a root cause: a gateway-level function call (`call_function_gblu0nmqpcej_1`) that was neither registered as a session nor as a subagent, causing the parent task to lose visibility. They propose a design where cross-model sub-tasks adopt the same notification mechanism that already works for same-model sub-tasks, and suggest making active handshake from sub-task to parent a hard requirement. This reflects a sophisticated production-level debugging effort and signals growing enterprise-grade usage.

- **Feature Request & Community Signal: Hermes Agent Support**  
  [#2131 – LobsterAI 支持 hermes agent有计划吗？](https://github.com/netease-youdao/LobsterAI/issues/2131)  
  *Author: wtgoku-create*  
  A direct request for Hermes Agent integration. While low in reactions, the question indicates that the community is already looking for interoperability with alternative agent frameworks beyond standard LLM backends.

---

### 5. Bugs & Stability

- **Medium Severity – Export & Code Copy Regressions**  
  [#2133 – fix: fix export and code copy bugs](https://github.com/netease-youdao/LobsterAI/pull/2133) (Open PR)  
  This PR targets rendering bugs that block users from exporting work or copying generated code. The fact that no merged fix exists yet suggests these issues are current and affecting daily workflows. **No closed issue references this PR**, which may mean the bug was discovered internally rather than reported by a user.

- **Low Severity – Temporary Data Backup Gate**  
  The rapid merge of [#2135 – chore: temporary close databackup](https://github.com/netease-youdao/LobsterAI/pull/2135) after [#2136](https://github.com/netease-youdao/LobsterAI/pull/2136) suggests the backup feature may have been merged preemptively and disabled for stability reasons. No crash or data loss reports are linked today.

No critical-severity bugs were reported in the last 24 hours.

---

### 6. Feature Requests & Roadmap Signals

- **High Confidence – Cross-Model Coordination Protocol**  
  Issue [#2132](https://github.com/netease-youdao/LobsterAI/issues/2132) is effectively a design proposal for making cross-model sub-task coordination a first-class feature. Given the author's detailed root-cause analysis and proposed fix, this is likely to be prioritized. The key idea—using the same notification mechanism that works for same-model sub-tasks—is a concrete, implementable pattern.

- **Medium Confidence – Hermes Agent Integration**  
  Issue [#2131](https://github.com/netease-youdao/LobsterAI/issues/2131) asks about Hermes Agent support. No maintainer response is recorded yet. If the dev team sees this as a strategic extension, it could appear within 1–2 minor releases. If niche, it may remain a low-prio backlog item.

- **Confirmed – Data Backup & Migration (Gate/Preview)**  
  Code for [#2136](https://github.com/netease-youdao/LobsterAI/pull/2136) has been merged but temporarily disabled. This suggests the feature is planned for the next stable release, pending testing. Expect a "Data Backup & Restore" toggle in a near-term release.

---

### 7. User Feedback Summary

- **Pain Point: Multi-Model Task Orchestration**  
  The user in [#2132](https://github.com/netease-youdao/LobsterAI/issues/2132) is clearly running LobsterAI in a production-like setting with mixed models (M3 for planning/oversight, DeepSeek for execution). They felt the lack of cross-model handshake was a blocker. They expressed **dissatisfaction** with the current isolation of sub-agent sessions but **high satisfaction** with the same-model sub-task notification mechanism, which they called "值得借鉴" (worth learning from).

- **Pain Point: Incomplete Notifications**  
  The merge of [#2134](https://github.com/netease-youdao/LobsterAI/pull/2134) directly addresses a user-facing regression: task completion notifications sometimes failed to restore the app window, especially on macOS. The fix also ensures notification clicks remain actionable. This suggests users were frustrated by orphaned notifications.

- **Neutral/Positive: Data Safety**  
  No direct user complaints about data loss, but the parallel work on backup/migration ([#2136](https://github.com/netease-youdao/LobsterAI/pull/2136)) implies an internal or escalated user concern about state persistence.

---

### 8. Backlog Watch

- **No long-latency items identified today.** All open issues and PRs are from 2026-06-09 or later. The project appears actively maintained with no signs of maintainer neglect in the observed timeframe.

- **Actionable: PR #2133 still open** – The export/code copy fix PR from *fisherdaddy* has been open for 1 day without merge or further review comments. Given low activity elsewhere, it may benefit from a review prompt to avoid bit-rotting.

---

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

# CoPaw Project Digest — 2026-06-10

## Today's Overview

CoPaw shows consistently high activity with 37 issues and 35 PRs updated in the last 24 hours, reflecting strong community engagement. The project released version **1.1.11-beta.2**, adding page coordinate click support for browser control and fixing CDP timeout parameters for cross-browser switching. Key trends include a surge in developer experience requests (especially regarding startup speed, UI rendering performance, and session management), ongoing work on the major AgentScope 2.0 backend migration, and increasing interest in observability, memory self-evolution, and visual model fallback features. The community is highly engaged in both reporting bugs and proposing substantial architectural improvements.

---

## Releases

### 1.1.11-beta.2 — 2026-06-09

**What's Changed:**
- **feat(browser):** Add page coordinate click support to `browser_control` (PR #4905, by @bfglx)
- **fix(browser):** Add CDP timeout parameter and browser profile isolation for cross-browser switching (PR #4905, by @x1n95c)

**Breaking Changes:** None reported.

**Migration Notes:** No special steps required. This is a pre-release beta focused on browser control improvements.

---

## Project Progress

**Merged/Closed PRs (15 total):**

| PR | Description | Impact |
|---|---|---|
| [#5049](https://github.com/agentscope-ai/QwenPaw/pull/5049) | Zero-config free models & one-click OAuth authentication | **High** — Onboarding simplification |
| [#5043](https://github.com/agentscope-ai/QwenPaw/pull/5043) | OpenSandbox plugin with MCP protocol | **Medium** — New plugin plugin for sandboxed code execution |
| [#5048](https://github.com/agentscope-ai/QwenPaw/pull/5048) | Fix unawaited coroutine in `_broadcast_to_subscribers` | **High** — Fixes async runtime errors |
| [#5054](https://github.com/agentscope-ai/QwenPaw/pull/5054) | Complete E2E integration CI pipeline with Playwright coverage | **Infrastructure** — CI quality improvements |
| [#5055](https://github.com/agentscope-ai/QwenPaw/pull/5055) | Version bump to v1.1.11b2 | **Release** |
| [#5050](https://github.com/agentscope-ai/QwenPaw/pull/5050) | Fix system theme toggle icon clarity | **Low** — UX polish |
| [#5021](https://github.com/agentscope-ai/QwenPaw/pull/5021) | Fix `/compact` and auto-compaction ignoring model's `max_input_length` | **Medium** — Context compression correctness |
| [#4857](https://github.com/agentscope-ai/QwenPaw/pull/4857) | Enhanced make-skill flow for self-evolving skill creation | **Medium** — Skills system improvement |
| [#5056](https://github.com/agentscope-ai/QwenPaw/pull/5056) | Remove redundant channel-tests workflow | **Low** — CI cleanup |
| [#4615](https://github.com/agentscope-ai/QwenPaw/pull/4615) | Fix ACP orphan process after close | **Medium** — Process management |
| Multiple bug fix PRs | Tolerate invalid jobs in `jobs.json`, resolve session filename duplication, fix DeepSeek tool naming issues | **Varies** — Stability improvements |

**Notable Open PRs under review:**
- [#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669): Tauri auto-updater (desktop) — *waiting for review*
- [#4981](https://github.com/agentscope-ai/QwenPaw/pull/4981): Security fix for file preview path traversal — *high priority*
- [#4975](https://github.com/agentscope-ai/QwenPaw/pull/4975): Customizable column order in sessions page
- [#5058](https://github.com/agentscope-ai/QwenPaw/pull/5058): 60 integration tests for channel layer + multi-agent management

---

## Community Hot Topics

| Issue | Type | Comments | Summary |
|---|---|---|---|
| [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) | Enhancement (Closed) | 10 | Suggest borrowing Hermes Agent's **learning loop** for self-evolving skills |
| [#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003) | Bug (Closed) | 8 | Aliyun Coding Plan qwen3.7+ hangs indefinitely |
| [#4666](https://github.com/agentscope-ai/QwenPaw/issues/4666) | Bug (Closed) | 7 | Model config page lost after new session; requires restart |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | Breaking Change (Open) | 7 | **AgentScope 2.0 backend migration** — community strongly supporting |
| [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | Bug (Closed) | 5 | `/compact` command ignores model's `max_input_length` |
| [#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015) | Question (Open) | 5 | Windows desktop frontend lag and CPU spikes during task execution |
| [#5009](https://github.com/agentscope-ai/QwenPaw/issues/5009) | Feature Request (Open) | 2 | Request for built-in observability/tracing integration |

**Underlying Needs:**
- **Self-evolving agents** — Community actively following Hermes Agent and requesting agent learning loops
- **Performance at scale** — Multiple complaints about UI freezing with long conversations, CPU spikes in desktop app
- **Developer tooling** — Clear demand for tracing, observability, and better debugging tools
- **Session management UX** — Users repeatedly asking for sidebar-based session switching

---

## Bugs & Stability

### High Severity
| Bug | Issue | Status | Fix PR Exists? |
|---|---|---|---|
| Aliyun Coding Plan qwen3.7+ hangs at startup | [#5003](https://github.com/agentscope-ai/QwenPaw/issues/5003) | **Closed** | Likely fixed |
| Windows desktop startup extremely slow (Tauri migration) | [#5047](https://github.com/agentscope-ai/QwenPaw/issues/5047) | **Open** | No |
| Frontend freezes/crashes during long streaming outputs | [#4792](https://github.com/agentscope-ai/QwenPaw/issues/4792), [#5015](https://github.com/agentscope-ai/QwenPaw/issues/5015) | **Open** | No |
| Session filename duplication causing Windows MAX_PATH overflow | [#4988](https://github.com/agentscope-ai/QwenPaw/issues/4988) | **Open** | **Yes** — PR [#5036](https://github.com/agentscope-ai/QwenPaw/pull/5036) |
| Duplicate message replies in WeChat channel with active mode | [#5030](https://github.com/agentscope-ai/QwenPaw/issues/5030) | **Open** | No |

### Medium Severity
| Bug | Issue | Status | Fix PR Exists? |
|---|---|---|---|
| `/compact` ignoring model's `max_input_length` | [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | **Closed** | Yes — PR [#5021](https://github.com/agentscope-ai/QwenPaw/pull/5021) |
| DeepSeek tool naming conflicts (`.` vs `^[a-zA-Z0-9_-]+$`) | [#5045](https://github.com/agentscope-ai/QwenPaw/issues/5045) | **Closed** | Yes — PR [#5034](https://github.com/agentscope-ai/QwenPaw/pull/5034) |
| Tauri desktop external links not opening / files not downloading | [#5044](https://github.com/agentscope-ai/QwenPaw/issues/5044) | **Closed** | Yes |
| `submit_to_agent` file path bug | [#5025](https://github.com/agentscope-ai/QwenPaw/issues/5025) | **Open** | No |
| Code Open Directory only works for C drive on Windows | [#5042](https://github.com/agentscope-ai/QwenPaw/issues/5042) | **Closed** | Yes |

### Low Severity / UX
| Bug | Issue | Status |
|---|---|---|
| Reasoning content not displayed for KimiCode API | [#5013](https://github.com/agentscope-ai/QwenPaw/issues/5013) | **Closed** |
| Image preview dragging causes severe jitter | [#4993](https://github.com/agentscope-ai/QwenPaw/issues/4993) | **Open** |
| OneBot port not released on reload | [#4926](https://github.com/agentscope-ai/QwenPaw/issues/4926) | **Closed** |

**Overall Stability Assessment:** The project is actively fixing bugs, with many being closed quickly. However, **frontend performance degradation** (lag, CPU spikes, slow desktop startup) is the single largest cluster of unresolved issues, likely tied to the Tauri migration.

---

## Feature Requests & Roadmap Signals

**Likely in Next Version:**
| Feature | Issue | Rationale |
|---|---|---|
| **AgentScope 2.0 backend migration** | [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | Labeled "Breaking Change," maintainer-led, high community 👍 (2) |
| **Self-evolving skills** | [#4994](https://github.com/agentscope-ai/QwenPaw/issues/4994), [#5017](https://github.com/agentscope-ai/QwenPaw/issues/5017) | PR [#4857](https://github.com/agentscope-ai/QwenPaw/pull/4857) already merged; strong user demand |
| **Visual model fallback** | [#4992](https://github.com/agentscope-ai/QwenPaw/issues/4992) | Well-structured proposal; solves real multi-model limitation |
| **Sidebar session switching** | [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | Simple UX improvement with clear community support |

**Speculative:**
| Feature | Issue | Signal |
|---|---|---|
| **Observability integration** (Langfuse/OpenTelemetry) | [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057), [#5009](https://github.com/agentscope-ai/QwenPaw/issues/5009) | Consistent developer interest; aligns with AgentScope 2.0 tracing |
| **OpenSandbox MCP plugin** | [#4951](https://github.com/agentscope-ai/QwenPaw/issues/4951) | Already merged in PR [#5043](https://github.com/agentscope-ai/QwenPaw/pull/5043) |

---

## User Feedback Summary

| Theme | Feedback | Satisfaction Level |
|---|---|---|
| **Chinese user experience** | "QwenPaw is great domestically — localisation is excellent, clear settings, truly out-of-the-box" (#5017) | ✅ **Positive** |
| **Desktop app performance** | "Since switching from Python packaging to Tauri, startup went from 1-2 minutes to 10+ minutes, often freezes" (#5047) | ❌ **Very Dissatisfied** |
| **UI rendering** | "Frontend lags especially when streaming long responses; CPU spikes, mouse freezing" (#4792, #5015, #4917) | ❌ **Dissatisfied** |
| **Session management** | "Session management is painful; need to click twice to switch sessions. Please add sidebar" (#4971) | ❌ **Dissatisfied** |
| **Observability & monitoring** | "Need built-in tracing for multi-turn interactions, cost attribution, and latency breakdown" (#5009, #4057) | 🟡 **Requested** |
| **Memory system** | "Memory system is weak and doesn't support self-evolution; need to learn from mainstream agent frameworks" (#4994) | 🟡 **Requested** |
| **Chinese model compatibility** | "Qwen 3.6-27B works in 1.1.5 but broken in 1.1.9/1.1.10" (#4989) | ❌ **Dissatisfied** |
| **General usability** | "QwenPaw is your go-to for a complete AI desktop" (#5017) | ✅ **Highly Positive** |

---

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Created | Days Open | Priority | Reason to Watch |
|---|---|---|---|---|
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) — AgentScope 2.0 migration | 2026-05-27 | 14 days | **Critical** | Breaking change; may affect all integrations |
| [#4057](https://github.com/agentscope-ai/QwenPaw/issues/4057) — AgentScope tracing initialization | 2026-05-06 | 35 days | **Medium** | Unanswered; clear developer use case |
| [#4792](https://github.com/agentscope-ai/QwenPaw/issues/4792) — UI freeze during streaming | 2026-05-29 | 12 days | **High** | Multiple duplicates (#5015, #4917) |
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) — Qwen 3.6-27B compatibility regression | 2026-06-06 | 4 days | **High** | Regression from 1.1.5 |
| [#5009](https://github.com/agentscope-ai/QwenPaw/issues/5009) — Observability roadmap | 2026-06-08 | 2 days | **Medium** | No maintainer response yet |

### PRs Needing Review

| PR | Created | Days Open | Purpose |
|---|---|---|---|
| [#4669](https://github.com/agentscope-ai/QwenPaw/pull/4669) — Tauri auto-updater | 2026-05-25 | 16 days | Desktop UX improvement |
| [#4981](https://github.com/agentscope-ai/QwenPaw/pull/4981) — File preview security fix | 2026-06-05 | 5 days | **Security** — path traversal prevention |

---

**Project Health Score:** 🟡 **Good but with notable tension areas.** Activity level is excellent, and the maintainer team is responsive to bugs. However, the desktop Tauri migration has introduced significant performance regressions, and the upcoming AgentScope 2.0 migration will likely require substantial community testing. The strong alignment between user feature requests and recent PR merges (self-evolving skills, OpenSandbox, zero-config models) indicates good roadmap alignment.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-10

## Today's Overview

ZeroClaw shows **extremely high activity** on 2026-06-10, with **50 issues and 50 PRs updated in the last 24 hours** — well above typical daily volume for this project. Only 2 issues were closed and 1 PR was merged/closed, indicating the project is in a **heavy development and triage phase** rather than a stabilization phase. The backlog remains significant with **97 open items** across issues and PRs, and the project has had **no new releases** in this period. The project is actively shipping fixes for long-standing bugs (context budget, cron, dashboard UX) and advancing several major architectural features (per-turn output routing, multi-tenant security, observability correlation).

## Releases

**None.** No new versions were published on this date. The latest beta (v0.8.0-beta-1) continues to receive bug-fix PRs and feature work targeting the next stable release.

## Project Progress

**1 PR was merged/closed today:**

- **[PR #7425]** — **fix(runtime): resolve channel pricing via bare-type fallback in cost lookup** *(merged)*. Fixes a critical bug where channel cost tracking silently recorded `cost_usd = 0` for all channel agents, rendering per-day budget enforcement inert. The root cause was a keying mismatch in the pricing map.

**Notable open PRs advancing key features:**
- **[PR #7444]** — Fix/7376 dashboard state labeling (loading/error/live states in TUI)
- **[PR #7442]** — Fix parallel SubAgents and Delegates return reliability (runtime critical)
- **[PR #7385]** — Add turn metadata to observer events and correlate OTel spans by turn_id (large observability enhancement)
- **[PR #7367]** — Route inbound webhooks per channel alias (gateway improvement)
- **[PR #7361]** — Per-turn output routing via send_via + voice delivery fixes (XL-sized feature)
- **[PR #7348]** — Fix cron: skip overdue jobs on startup when catch_up_on_disabled (cron reliability)
- **[PR #7350]** — Wire reasoning_effort into dedicated Azure OpenAI provider

## Community Hot Topics

**Most active issues (by comment count):**

1. **[Issue #4710] — [CLOSED] Feature: A better LOGO of Zeroclaw** *(19 comments, 2 👍)*  
   A long-running community design discussion (since March 2026). Recently closed, indicating the project may have finalized its visual identity.

2. **[Issue #5862] — [OPEN] Bug: zeroclaw does not know it can add cron** *(12 comments)*  
   Users report the agent is unaware of its own cron capabilities. The agent cannot respond to "do this every day at 8 PM" because it lacks tool awareness of `zeroclaw cron`. **Underlying need:** The agent needs introspection into its own toolset, especially for scheduling — this is a UX/agent-education gap.

3. **[Issue #5937] — [OPEN] Feature: refactor providers architecture and reqwest client management** *(10 comments)*  
   A significant architectural proposal to unify provider configuration, eliminate code duplication, and standardize HTTP client construction across all provider backends. **Underlying need:** Maintainability and consistency — the current fragmented provider code is causing bugs and configuration confusion.

4. **[Issue #5982] — [OPEN] Feature: Per-sender RBAC for multi-tenant agent deployments** *(9 comments)*  
   Request for role-based access control so a single instance can serve customers, operators, and developers with isolated workspaces and tool sets. **Underlying need:** Enterprise security — ZeroClaw currently runs with a single security perimeter.

**Most upvoted:** Issue #4710 (logo design) with 2 👍 — low reaction count suggests the community is focused on functional issues rather than cosmetic ones.

## Bugs & Stability

**High-severity bug reports (P1):**

| Issue | Title | Severity | Details |
|---|---|---|---|
| [#5844] | Too much emphasis on memory | S2 | System prompt prioritizes memory over current prompt, especially in cron jobs |
| [#5808] | Default 32k context budget exceeded by system prompt + tool definitions on iteration 1 | S1 | Fresh conversations exceed budget by ~3.3x, causing perpetual preemptive trim. **Fix in progress:** PR #7440 skips futile trim when system prompt alone exceeds budget |
| [#6034] | Single/multi-turn dialogue loses user messages | S1 | Custom API returns 400 Bad Request; all providers/models fail |
| [#6721] | tool_search not in default_auto_approve → deferred_loading+webhook silently hangs 120s then auto-denies | S1 | MCP tool loading blocked in non-interactive mode |
| [#6646] | web_search_tool and web_fetch not firing via Telegram channel in v0.7.5 | S1 | Tools not responding via Telegram; **related fix:** PR #7438 addresses Telegram delivery prompt discouraging tool use |
| [#6687] | Two independent SopEngine instances per daemon | S1 | MQTT-started runs invisible to agent sop_status |
| [#6037] | Cron jobs can be launched repeatedly while still running | S1 | Jobs launch 20+ times in burst; **fix in progress:** PR #7348 |
| [#6876] | risk_profile.allowed_tools does not restrict MCP tools | S1 | Security gap by design or documentation issue |
| [#6862] | Gateway SPA fallback serves index.html for unimplemented /api/* routes | S1 | Dashboard crashes with JSON parse error |
| [#7376] | zerocode Dashboard hides unavailable/error states | S2 | Labels history as active sessions; **fix in progress:** PR #7444 |

**New bugs reported today (06-09/06-10):**
- **[#7376]** — Dashboard hides error states (P2, S2) — **PR #7444 open**
- **[#7377]** — zerocode dark themes inherit unreadable terminal foreground text (P2, S2)
- **[#7378]** — zerocode treats macOS Cmd-C as quit chord (P2, S3)
- **[#7400]** — zerocode Locale selection does nothing until restart (P3, S3)
- **[#7410]** — Gateway webhook signing secrets should be read dynamically, not cached at startup (P2)
- **[#7253]** — Web console Config: Couldn't load sections (P2, S3)
- **[#7440]** — **Fix PR open** for #5808 (context budget trim)

## Feature Requests & Roadmap Signals

**Active feature requests likely in next release (v0.8.x or v0.9.0):**

| Issue | Feature | Priority | Likelihood |
|---|---|---|---|
| [#5937] | Unify providers architecture | P2 | **High** — architectural debt blocking other work |
| [#5982] | Per-sender RBAC for multi-tenant | P2 | **Medium** — enterprise demand, but large scope |
| [#6378] | Discord bot respond only in specific channels | P2 | **High** — simple config addition, already consistent with Matrix/Nextcloud |
| [#5775] | Per-skill security permissions (scoped allow_scripts/allowed_commands) | P2 | **Medium** — security critical but design still blocked |
| [#6916] | Process-memory limits on shell/skill subprocess execution | P1 | **High** — production OOM observed |
| [#6917] | Composio action-scope filter | P2 | **Medium** — security/compliance |
| [#7248] | Persist cached input tokens in cost accounting | P2 | **Medium** — accounting accuracy |
| [#7410] | Dynamic webhook signing secrets | P2 | **High** — follow-up from recent gateway work |

**Predictions for next release:**
- **Definite:** Provider architecture refactor (PR #5937 spawned multiple sub-PRs), MCP deferred_loading fix (#6721), cron job duplicate launch fix (#6037 → PR #7348)
- **Likely:** Discord channel filtering (#6378), per-skill security permissions (#5775), dynamic webhook secrets (#7410)
- **Possible but large:** Per-sender RBAC (#5982), per-turn output routing (PR #7361)

## User Feedback Summary

**Pain points expressed by users:**

1. **Context budget limitations** (#5808): Users are hitting context limits on first interaction due to bloated system prompt + tool definitions. A user reported this blocks workflow entirely (S1 severity).

2. **Agent unaware of own capabilities** (#5862): "I ask zeroclaw to let me do something every 8:00 PM. But zeroclaw says it does not have the tools." Users expect the agent to know it can use `zeroclaw cron`.

3. **Memory overemphasis** (#5844): "It gives too much value/priority to memories... I end up getting irrelevant replies." Users want better memory vs. prompt prioritization.

4. **Cron reliability** (#6037): Jobs launching 20+ times in burst — "Expected once, got 20 times in 3 minutes."

5. **Telegram tool failures** (#6646): Web search and fetch tools not firing via Telegram channel — users report blocking their entire workflow.

6. **Dashboard UX confusion** (#7376, #7377, #7378): macOS users report Cmd-C as quit chord, dark themes unreadable, loading states indistinguishable from errors.

**Satisfaction signals:**
- Active community participation in logo design (#4710) suggests brand attachment
- Multiple users contributing PRs (hanZeng-08, singlerider, chengzhichao-xydt, databillm) indicates healthy contributor ecosystem
- Feature requests are detailed and use-case driven, suggesting advanced users deploying in production

**Dissatisfaction signals:**
- Critical S1 bugs remaining open for weeks (#5844 since April 17, #5808 since April 16)
- Security/access control gaps (#5982, #6876, #5775) indicate production deployments hitting compliance walls
- Multi-channel inconsistencies (Telegram tools not working, Discord missing features) fragment the user experience

## Backlog Watch

**Long-unanswered important items needing maintainer attention:**

| Issue | Created | Days Open | Priority | Notes |
|---|---|---|---|---|
| [#4853] | 2026-03-27 | **75 days** | P2 | Installing skills from `.well-known` URI — blocked on external standardization |
| [#5842] | 2026-04-17 | **54 days** | P2 | Track `extra_args` validation for Codex CLI security |
| [#5775] | 2026-04-15 | **56 days** | P2 | Per-skill security permissions — status:blocked |
| [#5982] | 2026-04-22 | **49 days** | P2 | Per-sender RBAC — needs-author-action |
| [#6250] | 2026-05-01 | **40 days** | P1 | Extract require_auth to route-layer middleware — no-stale |
| [#6917] | 2026-05-25 | **16 days** | P2 | Composio action-scope filter — status:blocked |
| [#7410] | 2026-06-09 | **1 day** | P2 | Dynamic webhook secrets — new, but important follow-up |

**Key observations:**
- 3 high-priority items (P1) have been open for 40+ days (#6250, #5808, #6037)
- The `needs-author-action` label on #5982 suggests a contributor has not responded to maintainer questions — this may stall multi-tenant RBAC
- #4853 (skills from `.well-known` URI) has waited 75 days for external standardization to land, but this is expected for cross-project coordination
- No PR activity on the Codex CLI security issue (#5842) despite its 54-day age — this is a security gap in the config pipeline

**Action alert:** The S1 cron burst bug (#6037) has been open since April 23 (48 days) without a merged fix, though PR #7348 is now open. This is one of the most impactful bugs for cron-dependent users.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*