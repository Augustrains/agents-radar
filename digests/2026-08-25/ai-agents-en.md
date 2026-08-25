# OpenClaw Ecosystem Digest 2026-08-25

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-25 00:30 UTC

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

Based on the provided GitHub data for OpenClaw (github.com/openclaw/openclaw) on 2026-08-25, here is the project digest.

---

# OpenClaw Project Digest: 2026-08-25

## 1. Today's Overview
OpenClaw is in a high-activity state, with 500 issues and 500 PRs updated in the last 24 hours. The project is actively addressing a backlog of critical reliability bugs, particularly around message delivery, session state management, and multi-agent orchestration. There is a new beta release (v2026.8.1-beta.3) focused on GPT-5.6 support and UI improvements, but the bulk of community and maintainer effort is directed at stabilizing the platform through bug fixes and addressing a significant amount of long-standing technical debt and process friction. While the sheer volume of open items suggests ongoing challenges, the high number of linked PRs indicates a responsive development effort.

## 2. Releases
- **v2026.8.1-beta.3**
  - **Highlights:**
    - **New Model Support:** Added support for GPT-5.6 Sol, Terra, Luna, and Ultra across the platform and the Codex runtime.
    - **Onboarding UX:** The Control UI's first-run setup now continues verified model setup into Custodian and optional channel configuration.
    - **Chrome Integration:** Introduced a Puppeteer-compatible CDP relay, allowing for paired Chrome sessions.
    - **Extension:** The description is cut off, but it mentions "Explicit ext..." (likely referring to explicit extension permissions or configuration).
  - **No migration notes are provided** in the summary.

## 3. Project Progress
This section focuses on merged/closed PRs that advanced the project (based on available data, many PRs are still open and awaiting review/proof).

- **Install Policy Security (Merged/Closed):** Siginificant work was completed on security around install policies.
    - **PR #116489** (`feat(security): require acknowledgement for install policy warnings`) adds a new interactive `warn` state for `security.installPolicy`, requiring operators to acknowledge warnings.
    - **PR #120900** (`feat(ui): review install policy warnings`) complements this by allowing admins to review and approve warning-gated installs from the Control UI.
- **Process Management (Merged/Closed):**
    - **PR #123975** (`fix(scripts): clean up tsgo process trees on timeout or signal`) implements a healthy process-management improvement by cleaning up the `tsgo` compiler process tree on failure, preventing resource leaks.
- **Other Closed/Merged Items:**
    - **PR #126424** (`fix(gateway): keep conversation delivery within agent bindings`) was merged, addressing a multi-agent isolation issue where conversation tools could deliver messages outside of configured agent bindings.
    - **PR #125471** (`fix(models): keep Claude CLI OAuth available in Control UI`) addresses a state bug where a valid Claude CLI OAuth profile could lose its refresh ownership after a restart, potentially breaking authentication.

## 4. Community Hot Topics
The most active discussions highlight deep concerns about reliability, state corruption, and UX friction in complex setups.

- **#125626 - "Release validation: v2026.8.1-beta.2"** (18 comments) - [Link](https://github.com/openclaw/openclaw/issues/125626)
    - This is the internal process for validating a prior beta release, showing the project's commitment to structured QA for its most impactful changes.
- **#67777 - "[Bug]: Subagent completion delivery can be lost on direct-announce timeout, drain, or orphan prune"** (12 comments) - [Link](https://github.com/openclaw/openclaw/issues/67777)
    - A critical reliability issue where subagent results can be silently lost during periods of high load or maintenance. The underlying need is for a **guaranteed, durable message delivery system** for asynchronous agent operations.
- **#97616 - "[Bug]: OpenClaw leaks unreaped hook/tool child processes, causing zombie accumulation..."** (9 comments) - [Link](https://github.com/openclaw/openclaw/issues/97616)
    - This points to a memory and resource leak. Users running stable, long-lived gateways are seeing performance degrade over time due to zombie processes, indicating a need for robust process lifecycle management.
- **#10687 - "Models: fully dynamic model discovery (OpenRouter + beyond)"** (9 comments) - [Link](https://github.com/openclaw/openclaw/issues/10687)
    - This long-standing feature request asks for a more flexible way to handle new/third-party models. The underlying need is to **decouple from a static model catalog and allow for easy integration of new providers** like OpenRouter.
- **#6757 - "Feature Request: Agent-triggered context compaction (self-compact tool)"** (8 comments) - [Link](https://github.com/openclaw/openclaw/issues/6757)
    - An agent filed this request to give agents the ability to manage their own context window. This indicates a desire for **more autonomous self-management capabilities for agents** to handle long-running tasks without human intervention.

## 5. Bugs & Stability
This section ranks reported bugs by severity, focusing on the most critical issues discussed today.

- **Critical (P0/P1) - Message Loss & Data Corruption:**
    - **#67777 (P1)** - Subagent completion delivery loss. Related PRs exist.
    - **#114020 (P1)** - Feishu/Telegram dispatch fails due to a missing lifecycle requirement (`runDispatchLifecycle`), causing a channel-wide outage. [Link](https://github.com/openclaw/openclaw/issues/114020)
    - **#125570 (P1)** - Skill Workshop `update` silently overwrites skill descriptions, breaking routing. This proposes a clear data-loss scenario. Related PRs exist. [Link](https://github.com/openclaw/openclaw/issues/125570)
    - **#126246 (P1)** - Telegram durable outbound messages can remain stuck in a state and be lost after a gateway restart. [Link](https://github.com/openclaw/openclaw/issues/126246)
- **High (P1) - Session & State Management:**
    - **#126900 (P1)** - The `maxActiveTranscriptBytes` compaction loop can wedge a session permanently if the compacted transcript remains too large. [Link](https://github.com/openclaw/openclaw/issues/126900)
    - **#126906 (P1)** - Denying the `write` tool can silently disable memory persistence, leading agents to report success for writes that never happened. This is a dangerous failure mode. [Link](https://github.com/openclaw/openclaw/issues/126906)
    - **#127852 (P1)** - Results from a "current-session" cron job can be committed to a *replacement* conversation if the original is reset mid-run. [Link](https://github.com/openclaw/openclaw/issues/127852)
- **High (P1) - Runtime & Infrastructure Robustness:**
    - **#97616 (P1)** - Zombie process accumulation, leading to performance degradation. Related PRs likely exist.
    - **#126631 (P1)** - Sandbox skills bind-mount creates root-owned directories, locking out the unprivileged user. [Link](https://github.com/openclaw/openclaw/issues/126631)

## 6. Feature Requests & Roadmap Signals
- **Long-Pending & High-Demand:**
    - **#10687 (P3, 3 reactions)** - **"Fully dynamic model discovery"** - the community is asking for better support for fast-moving catalogs like OpenRouter. This is tagged as needing a product decision but is a strong candidate for a future version.
    - **#6757 (P2)** - **"Agent-triggered context compaction"** - Active agents are requesting self-management tools, which is a roadmap signal for more sophisticated agentic workflows.
    - **#9986 (P2)** - **"Trigger model fallback on context length exceeded"** - Users want automatic model switching when a context limit is hit, not just on an API error. This is often confused as a "message loss" bug.
- **Orchestration & UI Signals:**
    - **#52803 (P2)** - **"Improve Control UI for Multi-Agent + Subagent Orchestration"** - Users are demanding better visibility and hierarchical management for complex setups.
    - **#45508 (P2)** - **"Self-hosted STT/TTS provider support in webchat"** - Users want the webchat to respect server-side TTS/STT config, bridging a gap between the CLI and web UX.
- **Smaller, Potentially "Next Up" Features:**
    - **#50205 (P3)** - **"Support configurable request labels for Gemini API calls"** - A practical request for billing cost attribution.
    - **#49740 (P2)** - **"cron job auto-retry on failure"** - A robust feature request to make schedulers more resilient to transient upstream errors.

## 7. User Feedback Summary
- **Reliability Concerns are Paramount:** A significant portion of the most commented issues revolve around message loss, failed state persistence, and silent data corruption. Users are heavily invested in multi-agent setups and are experiencing pain when messages are dropped or sessions get stuck, undermining trust in the platform's stability.
- **Frustration with Silent Failures:** Several bugs (#126906, #125570, #50677) highlight frustration that the system fails *silently* (e.g., pretending to save memory, truncating skills without proper notification). Users are asking for more explicit warnings, better error messages, and clearer visibility into what the system is doing.
- **Process Burden on Maintainers:** The sheer volume of issues and PRs tagged with `clawsweeper:needs-maintainer-review` (over 20 in the top 50 alone) suggests that while the bots (clawsweeper) are doing initial triage, there is a substantial bottleneck requiring human maintainer attention for final decision-making and fixes.

## 8. Backlog Watch
These items are marked as needing attention (maintainer review or product decision) and have remained open for a significant time, indicating they are known but unresolved.

- **#6757 (Feb 2, 2026)** - **[Feature]: Agent-triggered context compaction** - Needs product decision. [Link](https://github.com/openclaw/openclaw/issues/6757)
- **#10687 (Feb 6, 2026)** - **Models: fully dynamic model discovery** - Needs maintainer review and product decision. [Link](https://github.com/openclaw/openclaw/issues/10687)
- **#9986 (Feb 5, 2026)** - **Feature: Trigger model fallback on context length exceeded** - Needs maintainer review and product decision. [Link](https://github.com/openclaw/openclaw/issues/9986)
- **#45771 (Mar 14, 2026)** - **Feature: Built-in pace-aware rate limiting for autonomous agents** - Needs maintainer review/product decision. This prevents agents from burning through API limits. [Link](https://github.com/openclaw/openclaw/issues/45771)
- **#107707 (Jul 14, 2026)** - **Bug: Skill Workshop Apply overwrites SKILL.md with proposal text verbatim (data loss)** - Tagged P0, with a linked PR open. This is a critical data-loss bug that awaits review. [Link](https://github.com/openclaw/openclaw/issues/107707)

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant Open-Source Ecosystem

**Date**: 2026-08-25  
**Scope**: 11 projects in the OpenClaw ecosystem and adjacent agent platforms

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is characterized by **rapid iteration with stability challenges**. Across 11 projects, we observe 500+ issues and 650+ PRs updated in a single 24-hour window, with the dominant theme being **reliability engineering** — session management bugs, message delivery guarantees, and memory leak fixes appear across nearly every project. The ecosystem is bifurcating into two architectural camps: **monolithic platforms** (OpenClaw, CoPaw, IronClaw) providing full agent stacks, and **modular frameworks** (NanoBot, Moltis) emphasizing provider abstraction and embeddability. Multi-agent orchestration, durable state persistence, and OpenAI-compatible API layers are emerging as the key competitive battlegrounds. Community engagement is technically sophisticated, with users actively proposing architectural solutions rather than merely reporting bugs.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score | Velocity |
|---------|-------------|-----------|----------------|--------------|----------|
| **OpenClaw** | 500 | 500 | v2026.8.1-beta.3 (new) | ⚠️ High activity, critical bugs | Very High |
| **NanoBot** | 8 | 26 (12 merged) | No release | ✅ Healthy, responsive | High |
| **Hermes Agent** | — | 50 (11 merged) | v0.20.4/v0.20.5 | ⚠️ Stabilizing | High |
| **PicoClaw** | 2 | 3 (2 merged) | v0.3.x | ⚠️ Slow but steady | Low |
| **NanoClaw** | 2 | 21 | **v2.3.0** (new) | ✅ Healthy | Very High |
| **NullClaw** | 2 | 1 | No release | ⚠️ Bandwidth constrained | Low |
| **IronClaw** | — | 56 | v1.3.0 deployed | ✅ Healthy, disciplined | Very High |
| **LobsterAI** | 3 (closed) | 11 (10 merged) | No release | ✅ Healthy | High |
| **Moltis** | — | 19 (16 merged) | **20260824.01** (new) | ✅ Very Healthy | High |
| **CoPaw (QwenPaw)** | 50 | 47 (26 closed) | v2.1.1-beta.2 (new) | ⚠️ Active, systemic bugs | Very High |
| **ZeptoClaw** | 1 | 0 | No release | ✅ Stable/Quiet | Low |

**Health Score legend**: ✅ = Rapid fix turnaround, no critical open blockers | ⚠️ = Active but with systemic issues or slowdowns

---

## 3. OpenClaw's Position

### Advantages
- **Scale of community**: 500 issues + 500 PRs in 24h — 10-25x the volume of peers, indicating the largest user and contributor base
- **Security leadership**: Install policy acknowledgement flows (#116489), warning-gated installs (#120900)
- **Multi-agent orchestration**: Directly addressing subagent delivery guarantees (#67777), agent binding isolation (#126424)
- **Model support breadth**: GPT-5.6 family, Claude CLI OAuth, dynamic model discovery requests

### Technical Approach Differences
- **Monolithic gateway architecture**: Unlike NanoBot's modular provider layer or Moltis's adapter pattern, OpenClaw uses a unified runtime with bindings, making it more powerful but harder to stabilize
- **Puppeteer-compatible CDP relay**: Unique Chrome integration approach not seen in peers
- **Custodian + Channel configuration onboarding**: Structured setup flow unmatched by competitors

### Community Size Comparison
| Metric | OpenClaw | Nearest Peer (CoPaw) | Ratio |
|--------|----------|---------------------|-------|
| 24h issues | 500 | 50 | 10x |
| 24h PRs | 500 | 47 | 10.6x |
| Release cadence | Beta monthly | Beta monthly | Parity |
| Maintainer bottleneck | High (clawsweeper triage required) | Moderate | — |

**Verdict**: OpenClaw is the **category-defining project** but is paying the cost of that position — its scale creates a triage bottleneck that smaller, more focused projects (NanoBot, Moltis) avoid.

---

## 4. Shared Technical Focus Areas

Across 5+ projects, these requirements are emerging independently — strong signals for ecosystem-wide priorities:

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Durable message delivery** | OpenClaw (#67777), NanoBot (#5512), CoPaw (#7231), Hermes (#66616), NullClaw (#992) | Guaranteed subagent results, no lost messages on restart, session identity freezing |
| **Agent self-management** | OpenClaw (#6757), CoPaw (#7230), IronClaw (#7001), NanoBot (#5344) | Self-compact tools, context compression only when idle, byte-stable cache prefixes, loop spiral detection |
| **Multi-agent isolation** | OpenClaw (#126424), CoPaw (#7011), ZeroClaw (#10324), Hermes (#85125) | Cross-agent boundary enforcement, scoped cron tools, session identity separation |
| **OpenAI-compatible API layer** | ZeroClaw (#8603), CoPaw, OpenClaw, Moltis | Chat Completions profile, drop-in backend replacement, tool schema strict mode |
| **Provider flexibility** | OpenClaw (#10687), NanoBot (#5480), Moltis (#1240), NanoClaw (#2474), PicoClaw (#3299) | Dynamic model discovery, unified usage contracts, OAuth providers, provider abstraction |
| **Memory/state leak fixes** | OpenClaw (#97616), CoPaw (#7222), NanoBot (#5430), LobsterAI (#1193) | Zombie processes, unbounded index growth, SQLite write amplification, task group release |
| **Self-hosting configurable endpoints** | NullClaw (#993), PicoClaw, OpenClaw, IronClaw | Firecrawl endpoint config, web search providers, third-party service URLs |

---

## 5. Differentiation Analysis

| Project | Core Focus | Target Users | Architecture |
|---------|-----------|--------------|--------------|
| **OpenClaw** | Full-featured enterprise agent platform | Power users, multi-agent deployments | Monolithic gateway + UI + SDK |
| **NanoBot** | Lightweight embedding framework | Developers building agents into products | Modular provider layer, Python |
| **Hermes Agent** | Research-grade agent with skills system | AI researchers, advanced workflows | Gateway + Desktop app + Skills Hub |
| **NanoClaw** | Multi-channel ops platform | Teams using Slack/Telegram/Mattermost | Channel adapters, TypeScript |
| **IronClaw** | Production agent with strong CI culture | Enterprise deployments | Rust + WebUI, disciplined testing |
| **Moltis** | Substrate/protocol-focused | Integration-heavy power users | Universal provider abstraction (OAuth) |
| **CoPaw** | Qwen/Chinese-market agent | Chinese-speaking developers, multi-agent | Console + ReMe memory + Docker |
| **LobsterAI** | Desktop app with cowork features | Small teams collaborating | Electron, cowork, library management |
| **PicoClaw** | TUI-first minimal agent | Terminal power users | Lightweight, TUI focus (Web UI coming) |
| **NullClaw** | Self-hosted minimal gateway | Privacy-focused self-hosters | Raspberry Pi, Docker, minimal |
| **ZeptoClaw** | REPL-driven agent | CLI enthusiasts | Interactive shell |

---

## 6. Community Momentum & Maturity

### Tier 1: Rapid Iteration (shipping daily)
- **NanoClaw**: 21 PRs, v2.3.0 released, coordinated feature push toward v2.4.0
- **IronClaw**: 56 items, four-lane CI expedite program, weekly dogfooding epics
- **CoPaw**: 26 PRs closed, near-daily fixes, first-time contributor pipeline thriving
- **OpenClaw**: Massive volume but struggling to keep pace with triage

### Tier 2: Stable Growth (shipping weekly/monthly)
- **Moltis**: 16 PRs merged, 24-hour issue-to-fix turnaround, extremely healthy
- **NanoBot**: 12 PRs merged, responsive maintainers, issue-to-fix in hours
- **LobsterAI**: 10 PRs merged, steady feature work, SQLite perf fix

### Tier 3: Consolidating (stabilizing after growth)
- **Hermes Agent**: 11 PRs merged, focused on fixing timeout/hang backlog, desktop stabilization

### Tier 4: Low Activity (maintenance mode potential)
- **PicoClaw**: Stale PRs (30 days no response), Web UI speculation
- **NullClaw**: 70-day stale dependency PR, pairing UX regression
- **ZeptoClaw**: Single issue, no code motion

---

## 7. Trend Signals

1. **Reliability is the new feature**: Across 9 of 11 projects, "guaranteed delivery," "durable state," and "no silent failures" outrank new features. Users are running agents in production and treating message loss like data corruption. **Value**: Prioritize delivery guarantees and explicit error surfaces over new capabilities.

2. **Session-identity is the hardest problem**: Multiple projects report cross-session contamination — messages sent to wrong threads, stops cancelling other sessions, identity confusion. This is an unsolved architectural challenge. **Value**: A clean session-routing mechanism is a competitive differentiator.

3. **Provider abstraction is table stakes**: Dynamic discovery (OpenClaw), unified usage contracts (NanoBot), OAuth subscription providers (Moltis), AI-CLI pickers (NanoClaw) — the industry is moving beyond API keys to universal provider layers. **Value**: New projects should assume multi-provider from day one.

4. **OpenAI-compatibility is the adoption lever**: ZeroClaw's accepted RFC for Chat Completions profile, CoPaw's Responses API work, and Moltis's OpenAI-safe tool schemas all point to the same conclusion: **integration with Open WebUI/LangChain ecosystems is the fastest path to adoption**. **Value**: Implement an OpenAI-compatible endpoint early.

5. **Memory management is becoming agent-driven**: Self-compaction tools (OpenClaw #6757), idle-only compression (CoPaw #7230), and byte-stable cache prefixes (IronClaw #7001) suggest the next frontier is **agents managing their own context budgets autonomously**.

6. **Security scoping for multi-agent**: Delegate bypasses risk profiles (ZeroClaw S0), cron cross-agent boundaries, and install policy warnings (OpenClaw) indicate that **as agents multiply, per-agent security boundaries are becoming critical**.

7. **macOS is chronically under-tested**: NanoClaw's better-sqlite3 segfault, Hermes's SIGSEGV on arm64, and macOS update controller defects (NanoClaw #3506) reveal a systemic gap: extensive Linux testing, weak Apple platform coverage. **Value**: Targeting macOS stability is a low-competition differentiator.

---

## Methodology

- **Data sources**: GitHub issue/PR activity for 2026-08-24 → 2026-08-25 across 11 repositories
- **Health scoring**: Response time, fix PR existence, maintainer engagement, open critical bugs
- **Limitations**: Data reflects 24-hour window; some projects may have longer release cycles not visible in this snapshot

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-25

## 1. Today's Overview

NanoBot is experiencing a period of **exceptionally high development activity**, with 26 PRs updated in the last 24 hours (12 merged/closed, 14 open) and 8 active issues filed, nearly all within the last day. The project shows a healthy, well-structured contribution pipeline with clear labeling conventions (priority, type, test coverage), and several contributors are actively addressing both user-facing regressions and ambitious new features. Notably, contributor **yrxeva** filed 4 feature request issues yesterday and immediately followed with merged PRs for two of them, demonstrating a highly responsive issue-to-implementation loop. The maintainers appear to be prioritizing reliability fixes around session management, streaming state, and timeout handling, while the community is pushing for performance optimizations and new provider integrations.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent activity is concentrated in the `main` branch through merged PRs.

---

## 3. Project Progress

**12 PRs were merged/closed in the last 24 hours**, representing meaningful advancement across several areas:

### Performance & Infrastructure (Merged)
- **[#5507 — feat(session): SQLite FTS5 full-text search index for fast session search](https://github.com/HKUDS/nanobot/pull/5507)** (by yrxeva): Replaces linear JSONL scans with a SQLite FTS5 mirror for near-instant full-text search, with a safe fallback. Directly addresses issue [#5509](https://github.com/HKUDS/nanobot/issues/5509).
- **[#5508 — feat(gateway): add ConditionalTriggerRuntime for token-free event pre-filtering](https://github.com/HKUDS/nanobot/pull/5508)** (by yrxeva): Adds a pure-Python condition monitor runtime that only wakes the LLM when conditions match, eliminating token cost for simple event-driven automation. Addresses [#5510](https://github.com/HKUDS/nanobot/issues/5510).
- **[#5517 — test(exec): remove Windows process timing races](https://github.com/HKUDS/nanobot/pull/5517)** (by chengyongru): Stabilizes Windows-specific process cleanup with explicit root-exit/child-ready handshakes.

### Provider & Usage Stack (Merged)
- **[#5480 — refactor(providers): define typed LLM usage contract](https://github.com/HKUDS/nanobot/pull/5480)** (by chengyongru): Replaces dynamic usage dictionaries with an immutable typed `LLMUsage` contract across OpenAI, Anthropic, and Bedrock providers.
- **[#5481 — feat(usage): add unified provider usage backend](https://github.com/HKUDS/nanobot/pull/5481)** (by chengyongru): Records content-free usage rows for every retry-managed provider attempt, enabling unified usage tracking across WebUI/TUI sessions.
- **[#5496 — fix(agent): time out no-tools model requests](https://github.com/HKUDS/nanobot/pull/5496)** (by chrischen-coder): Fixes a regression where no-tools requests bypassed wall-clock timeout protection, which could stall turns indefinitely.

### Agent Fixes (Merged)
- **[#5506 — fix(agent): honor selected project workspace](https://github.com/HKUDS/nanobot/pull/5506)** (by Re-bin): Exposes the WebUI-selected project as the model's working directory, fixing a disconnect between UI state and agent context.

---

## 4. Community Hot Topics

- **[#5350 — QwenCloud provider path alongside DashScope](https://github.com/HKUDS/nanobot/issues/5350)** (2 comments, open since Aug 12): The longest-running active discussion. The community is asking for a backward-compatible provider path for **QwenCloud**, the international Qwen platform, while preserving existing DashScope configurations. This signals growing international adoption of NanoBot beyond China-focused DashScope endpoints.

- **[#5512 — WebUI stalls in spinning state after Gateway restart](https://github.com/HKUDS/nanobot/issues/5512)** (1 comment): A critical UX bug where the frontend never receives the final `goal_status: idle` push after a Gateway restart, leaving `isStreaming` permanently true. **A fix PR already exists: [#5514](https://github.com/HKUDS/nanobot/pull/5514).**

- **[#5516 — Telegram rich messages never render when streaming is enabled](https://github.com/HKUDS/nanobot/issues/5516)** (0 comments): Highlights a feature conflict — `rich_messages: true` and `streaming: true` (default) are mutually exclusive, forcing users to choose between rich formatting and live streaming.

- **[#5505 — AnySearch as web search provider](https://github.com/HKUDS/nanobot/issues/5505)** (0 comments): The AnySearch team is proposing integration as a key-optional, anonymous-quota web search provider. This reflects ecosystem interest in using NanoBot as an agent platform with pluggable search backends.

---

## 5. Bugs & Stability

Ranked by severity:

1. **[High] WebUI stalls in spinning state after Gateway restart** ([#5512](https://github.com/HKUDS/nanobot/issues/5512)) — The most severe regression reported, causing hung turns that appear "frozen" to users. Fix PR [#5514](https://github.com/HKUDS/nanobot/pull/5514) is open.

2. **[High] Agent silently spirals on repeated identical tool calls** ([PR #5344](https://github.com/HKUDS/nanobot/pull/5344)) — A stuck agent can burn its entire `max_iterations` budget calling the same tool with the same arguments, appearing frozen from the outside. Fix is pending review.

3. **[Medium] Timeout protection bypass for no-tools requests** ([PR #5496](https://github.com/HKUDS/nanobot/pull/5496)) — Already **merged**; stalled no-tools requests could hold per-session locks indefinitely.

4. **[Medium] Telegram rich messages never render with streaming** ([#5516](https://github.com/HKUDS/nanobot/issues/5516)) — Feature conflict rather than crash, but degrades the Telegram experience for users who want both streaming and rich formatting.

5. **[Low] Subagent conversation transcripts not persisted** ([PR #5291](https://github.com/HKUDS/nanobot/pull/5291)) — Open since Aug 7; subagent runs leave no full conversation traces for review. Not a crash, but a debugging/observability gap.

6. **[Low] Session reply timeout task failures not observed** ([PR #5515](https://github.com/HKUDS/nanobot/pull/5515)) — Background timeout-delivery tasks are silently discarded; failures go unobserved.

---

## 6. Feature Requests & Roadmap Signals

Strong signals from the last 24 hours indicate the following likely roadmap items:

- **Crash-safe task ledger for multi-step agent tasks** ([#5511](https://github.com/HKUDS/nanobot/issues/5511)) — Very likely to be accepted: it follows the pattern of [#5507]/[#5508] (propose + implement immediately). Addresses real pain of losing in-memory progress on restart.

- **Route cron results to configurable channels** ([#5513](https://github.com/HKUDS/nanobot/issues/5513)) — High likelihood: operational users want separation between automation noise and personal conversations, plus batch archive capabilities.

- **QwenCloud provider path** ([#5350](https://github.com/HKUDS/nanobot/issues/5350)) — Likely in the next minor release given provider unification work ([#5480](https://github.com/HKUDS/nanobot/pull/5480)) just landed; a new provider becomes easier to add.

- **Langfuse tracing for Codex provider** ([#5520](https://github.com/HKUDS/nanobot/pull/5520)) — Currently open PR; observability parity across providers is a clear theme.

- **AnySearch web search integration** ([#5505](https://github.com/HKUDS/nanobot/issues/5505)) — Lower probability in the short term, but the key-optional anonymous quota pitch is attractive.

---

## 7. User Feedback Summary

Real user pain points emerging from this data:

- **Reliability anxiety**: Multiple issues about stalled states — WebUI spinning forever ([#5512](https://github.com/HKUDS/nanobot/issues/5512)), agents appearing frozen ([#5344](https://github.com/HKUDS/nanobot/pull/5344)), timeout gaps ([#5496](https://github.com/HKUDS/nanobot/pull/5496)). Users are running NanoBot in production and losing sessions is unacceptable.

- **Provider fragmentation**: The QwenCloud vs. DashScope request signals that users have existing configuration investments and want smooth migration paths, not provider replacement.

- **Channel-specific UX needs**: Telegram users want both rich messages and streaming; cron users want delivery routing separate from conversation channels. NanoBot is being used for both interactive chat and unattended automation.

- **Observability**: Users and contributors are pushing for better visibility into agent internals — subagent transcripts ([#5291](https://github.com/HKUDS/nanobot/pull/5291)), usage tracking ([#5481](https://github.com/HKUDS/nanobot/pull/5481)), model retry status ([#5504](https://github.com/HKUDS/nanobot/pull/5504)), and Langfuse tracing ([#5520](https://github.com/HKUDS/nanobot/pull/5520)).

Satisfaction indicators: The rapid issue-to-fix turnaround (e.g., [#5512](https://github.com/HKUDS/nanobot/issues/5512) → [#5514](https://github.com/HKUDS/nanobot/pull/5514) within hours) suggests an active and responsive maintainer team.

---

## 8. Backlog Watch

Items needing maintainer attention:

- **[#4549 — feat(heartbeat): add model_override config for cheaper heartbeat model](https://github.com/HKUDS/nanobot/pull/4549)** — **Open for 60 days** (since June 26). This is a straightforward configuration enhancement that would let users route heartbeat checks to cheaper models. No comments. Likely stalled on review bandwidth.

- **[#5291 — fix(agent): persist subagent conversation transcripts](https://github.com/HKUDS/nanobot/pull/5291)** — **Open for 18 days** (since Aug 7). Significant observability improvement; no comments or reviews visible.

- **[#5344 — fix(agent): warn instead of silently spiraling on repeated identical tool calls](https://github.com/HKUDS/nanobot/pull/5344)** — **Open for 14 days** (since Aug 11). Addresses a silent failure mode that could burn token budgets; still awaiting review.

- **[#5349 — fix(tests): pass timezone_name in settings tests](https://github.com/HKUDS/nanobot/pull/5349)** — **Open for 13 days** (since Aug 12). Small deterministic test fix; would help CI stability during UTC offset windows.

- **[#5430 — fix(agent): release completed task groups](https://github.com/HKUDS/nanobot/pull/5430)** — **Open for 7 days** (since Aug 18). Memory leak fix for long-running agent loops; no activity since original posting.

---

*Digest generated automatically from GitHub activity data for 2026-08-24 → 2026-08-25. All links reference [HKUDS/nanobot](https://github.com/HKUDS/nanobot).*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the provided GitHub data for Hermes Agent (github.com/nousresearch/hermes-agent), here is the project digest for 2026-08-25.

---

### 1. Today's Overview

Hermes Agent is showing **high activity with a strong community contribution channel** (50 PRs updated, 11 merged/closed). The project is currently in a **bug-fixing and stabilization cycle**, with a heavy focus on the Desktop application, session state management, and concurrency issues that lead to hangs and crashes. A significant portion of the triage effort is centered on architectural fixes for a long-standing backlog of timeout and hang bugs, as well as improving the robustness of the tool/skills system. The velocity is high, and the maintainers are actively reviewing and merging community-submitted PRs.

### 2. Releases

**No new releases** were published in the last 24 hours. The latest tagged version referenced in the issues is `v0.20.4` / `v0.20.5`.

### 3. Project Progress

The project saw 11 PRs merged or closed in the last 24 hours. Key developments include:

- **Kanban Dispatcher Fix**: PR [#67931](https://github.com/NousResearch/hermes-agent/pull/67931) (closed) addresses the critical bug [#59499](https://github.com/NousResearch/hermes-agent/pull/59499) where the Kanban dispatcher ignored `max_in_progress_per_profile` and spawned all tasks concurrently, risking resource exhaustion. This PR makes the system more resilient to transient file growth, and the issue was closed.
- **Bug Fixes and Cleanup**: Multiple other PRs were closed, likely merging fixes related to the issues listed (e.g., Desktop session tabs, Slack streaming duplication, and other session-state risks).
- **Accessibility Momentum**: PR [#93848](https://github.com/NousResearch/hermes-agent/pull/93848) (open) is addressing findings from a desktop accessibility audit, specifically improving icon button hit targets to meet WCAG standards, indicating ongoing investment in UI/UX quality.

### 4. Community Hot Topics

The most active discussions reveal major pain points and architectural concerns:

- **[Issue #66616](https://github.com/NousResearch/hermes-agent/issues/66616) - Skills Index Watchdog (91 comments)**: This automated-probe issue is the most commented-on item, indicating a recurring infrastructure stability problem with the Skills Hub index. The continued failure of the freshness probe suggests a systemic CI/CD issue that is frustrating for the team.
- **[Issue #85125](https://github.com/NousResearch/hermes-agent/issues/85125) - Unified Deadline Layer (20 comments)**: This feature request proposes an architectural fix to eliminate the recurring timeout/hang bug classes (referencing a backlog of 400+ issues). This is a critical priority for the community and maintainers, as it acts as an umbrella for many other bug reports.
- **[Issue #25833](https://github.com/NousResearch/hermes-agent/issues/25833) - Skill Correctness Guarantees (10 comments)**: Discusses the lack of mechanism-level guarantees for self-created skills, a core feature of the agent. The community is concerned about the reliability and consistency of generated skills.
- **[Issue #80246](https://github.com/NousResearch/hermes-agent/issues/80246) - Context Compression Undercount (8 comments)**: This bug is highly relevant to users hitting false 'out-of-context' errors on long reasoning sessions with models like DeepSeek/Kimi, indicating a blocker for advanced use.

### 5. Bugs & Stability

Several new critical bugs were reported today, highlighting stability concerns:

- **High Severity (P1)**:
    - **Gateway SIGSEGV Crash**: [Issue #94248](https://github.com/NousResearch/hermes-agent/issues/94248) describes a crash (`SIGSEGV`) on macOS arm64 happening *exactly* when delegated workers hit their deadline. A potential fix, **[PR #94313](https://github.com/NousResearch/hermes-agent/pull/94313)**, has been submitted to defer hard-close during SSL reads.
    - **Update Restores Invalid State**: [Issue #94264](https://github.com/NousResearch/hermes-agent/issues/94264) warns that `hermes update --gateway` can restore syntactically invalid Python and report success, leading to a remote lockout where the agent fails on every turn.
    - **SQLite Session SystemError**: [Issue #94258](https://github.com/NousResearch/hermes-agent/issues/94258) reports an unhandled `SystemError` causing session persistence to fail despite a healthy database. This is often linked to thread-safety issues.
- **Medium Severity (P2)**:
    - **Desktop Session/Restore Failures**: A cluster of bugs around Desktop session management is emerging, including failures to restore sessions on Remote Gateways ([#93888](https://github.com/NousResearch/hermes-agent/issues/93888)), unstable pane layouts ([#92818](https://github.com/NousResearch/hermes-agent/issues/92818)), and bot-mode tab restoration issues ([#94137](https://github.com/NousResearch/hermes-agent/issues/94137)).
    - **Docker Backend Sanitization**: [Issue #92701](https://github.com/NousResearch/hermes-agent/issues/92701) (closed) identified a bug where unsanitized `task_id`s with colons broke the Docker backend with "too many colons" errors.
    - **Data Contamination**: [Issue #94078](https://github.com/NousResearch/hermes-agent/issues/94078) reports that shell startup diagnostics (stderr) can contaminate file-operation data channels, leading to corrupted file reads.
    - **Desktop Context Usage Bug**: [Issue #94001](https://github.com/NousResearch/hermes-agent/issues/94001) reports stale context usage, cross-session contamination, and slow refresh in the Desktop status bar.

### 6. Feature Requests & Roadmap Signals

Several feature requests point towards a roadmap focusing on control, user safety, and determinism:

- **Architectural Fixes**: The "unified deadline layer" ([Issue #85125](https://github.com/NousResearch/hermes-agent/issues/85125)) is a strong signal that the core agent loop is being re-architected for reliability. Expect to see PRs addressing these fundamental timeout/hang issues in upcoming releases.
- **User Control and Safety**:
    - **Plan-then-Approve Mode**: [Issue #94251](https://github.com/NousResearch/hermes-agent/issues/94251) requests a built-in mode where the agent presents a plan and does not write any files until the user approves. This is a highly-requested safety feature for production use.
    - **User-Owned Delegation**: [PR #94312](https://github.com/NousResearch/hermes-agent/pull/94312) proposes a feature allowing users to route delegated subtasks to specific providers/models without changing the parent session's model. This is a powerful power-user feature likely to be included in the next minor version.
- **System Determinism and Observability**:
    - **Deterministic Tool Catalog**: [PR #94277](https://github.com/NousResearch/hermes-agent/pull/94277) introduces a `hermes tools catalog` command, indicating a push towards better auditability and configuration management. This is likely to be merged soon.
    - **Per-Skill Reasoning Effort**: [PR #93378](https://github.com/NousResearch/hermes-agent/pull/93378) adds configurable reasoning levels per skill, allowing users granular control over performance and cost. This addresses a common user need for fine-tuning agent behavior.

### 7. User Feedback Summary

Real user pain points highlight a desire for a more stable, predictable, and controllable agent:

- **Stability and Reliability**: Users are significantly impacted by hangs, timeouts, crashes (especially on macOS/Windows Desktop), and session restoration issues. This is the biggest source of dissatisfaction.
- **Source of Truth**: Many community issues and PRs (e.g., #85125, #94312) show a community that is not just reporting bugs but actively proposing structural fixes, indicating a technically sophisticated user base willing to contribute. This is a positive sign for the project's health.
- **Control and Configuration**: Users want more granular control over agent behavior (e.g., context compression accuracy, tool capabilities, skill-specific reasoning, approval workflows). The dissatisfaction stems from the agent acting 'magically' without proper guardrails or transparency.
- **Integration Gaps**: Issues like the OpenWebUI image integration (#7895) show users want seamless integration with their existing toolchains, and any breakage in these paths is a significant pain point.

### 8. Backlog Watch

These long-standing issues require maintainer attention:

- **[Issue #25833](https://github.com/NousResearch/hermes-agent/issues/25833) (P2, Created 2026-05-14)**: "Self-created skills lack mechanism-level guarantees" is a 3-month-old crucial quality-of-life feature for the agent's core loop. A decision is needed on the approach to add verification steps to the skill-creation process.
- **[Issue #66616](https://github.com/NousResearch/hermes-agent/issues/66616) (P3, Created 2026-07-18)**: The repeated failures of the "Skills Index Watchdog" (91 comments) indicate a long-running CI/CD issue that, while automated, could undermine user trust in the docs and skill discoverability if left unaddressed.
- **[Issue #5114](https://github.com/NousResearch/hermes-agent/issues/5114) (P3, Created 2026-04-04)**: The "Autoresearch skill" feature request is a powerful idea for autonomous ML optimization loops, but it has been idle for over 4 months without a maintainer response, potentially missing a significant opportunity for differentiation.

---

**Overall Project Health**: The project is technically vibrant with a high degree of community contribution, but **stability is the primary matrix for success right now**. The volume of session-state related bugs and the focus on fixing hangs and crashes indicate the team is actively working through a technical debt backlog. The high number of feature requests for control and safety suggests that once the stability issues are resolved, the platform is well-positioned for broader adoption in more sensitive or production environments.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-25

## 1. Today's Overview

PicoClaw shows a steady but relatively quiet development cadence this week, with 2 open issues and 3 pull requests updated in the last 24 hours, though no new releases have been published. The project's hallmark feature — a TUI for the AI agent platform — remains central, but the long-requested Web UI initiative (#806) continues to generate sustained community interest, now more than six months old with 10 comments and 8 👍 reactions. Two stale items have resurfaced: an Exa web search provider PR that has been open for a month without maintainer feedback, and a Slack image upload bug that appears minor but reveals potential gaps in regression testing. Notably, two PRs merged today address a persistent config validation bug and consolidate fixes from several older open PRs, suggesting the maintainer team is actively clearing backlog. Overall, the project appears healthy but would benefit from faster response times on stale items.

## 2. Releases

No new releases were published in the last 24 hours. The most recent tagged version remains **picoclaw 0.3.x** (as referenced in issue #3338). Users tracking the project should note that the Web UI refactoring and the Exa search provider work are still in-flight and have not yet been released.

## 3. Project Progress

Two pull requests were merged/closed today, representing meaningful progress:

- **[PR #1929 — "fix: apply security credentials before config validation in web handlers"](https://github.com/sipeed/picoclaw/pull/1929) (merged)**: This bug fix addresses a frustrating experience where the web launcher's config save (PUT/PATCH `/api/config`) would fail with a validation error (`"channels.pico.token is required..."`) even when the user had correctly stored the token in `.security.yml`. The root cause was that `validateConfig()` was checking security-managed private fields before those credentials were applied. This fix is significant because it unblocks web-based configuration workflows, which is a critical path for the upcoming Web UI feature.

- **[PR #1551 — "fix: merge PR #1428 #1422 #1417"](https://github.com/sipeed/picoclaw/pull/1551) (closed/merged)**: A consolidation PR that merges fixes from three earlier open pull requests (#1428, #1422, #1417). While the individual contents are not detailed in the summary, this signals maintainers are actively cleaning up the open PR backlog — a positive sign for project health.

## 4. Community Hot Topics

- **[Issue #806 — "Add webUI support"](https://github.com/sipeed/picoclaw/issues/806) — 10 comments, 8 👍, high priority, roadmap-tagged**: This is the single most discussed item in the project right now. The request is to build a browser-based Web UI on top of the existing TUI to lower the barrier for "non-tech" users. The issue is tagged `[type: enhancement, priority: high, type: roadmap]` and the author notes "Refactoring now" in the title — strong signals this is actively being worked on. The sustained interest over 6 months and the high reaction count indicate a large community segment (likely non-developer users) who find the TUI intimidating. This is the clearest product-direction signal in the dataset.

- **[PR #3299 — "Add native Exa web search provider"](https://github.com/sipeed/picoclaw/pull/3299) — 0 comments, 0 👍, stale**: This PR adds Exa as a native `tools.web` / `web_search` provider, using Exa's `POST /search` API with `type: "auto"` and `contents.highlights`, and supporting existing date-range filters. Despite being a feature complete implementation (auth, config, filters included), it has received zero maintainer feedback in 30 days and is now flagged as stale. This typically indicates either maintainer bandwidth constraints or uncertain prioritization of search providers.

## 5. Bugs & Stability

One bug was reported today, ranked by severity:

- **[Issue #3338 — "Slack does not attach image media content"](https://github.com/sipeed/picoclaw/issues/3338) — [BUG] [stale], severity: Medium**: Slack media uploads always fail with `file.upload.v2: file size cannot be 0`. The root cause is precise: `SendMedia` builds `slack.UploadFileParameters` without setting `FileSize`, causing the slack-go SDK to reject the upload before any network call occurs. This is a straightforward bug with a clear fix (set `FileSize` field), and it affects a core integration (Slack media sharing). Severity is Medium because it's a 100% failure for image attachments but does not crash the agent, and it's isolated to one integration. There is no associated fix PR yet.

## 6. Feature Requests & Roadmap Signals

- **Web UI (Issue #806)**: The dominant feature request. The explicit "Refactoring now" note in the title, combined with the `priority: high` and `roadmap` tags, strongly suggests this will be either in the next release or actively developed in the current cycle. Prediction: Next minor version (0.4.x) will likely introduce a beta Web UI or at minimum stabilize the web launcher APIs (consistent with PR #1929 fixing web config handlers).

- **Exa web search provider (PR #3299)**: A fully-featured PR awaiting review for 30 days. The lack of maintainer response makes prediction difficult, but given the growing demand for high-quality semantic search (Exa's differentiator), there is a reasonable chance this gets merged in the next release cycle if maintainers clear the stale flag.

## 7. User Feedback Summary

- **Pain: Web access barrier.** The community's strongest voice (via #806) expresses that the TUI is "great for terminal users" but is a barrier for "non-tech" users who want to manage their PicoClaw instances from a browser. Eight users have 👍 the request, a high rate for this project.

- **Pain: Web config save bug.** The fix in PR #1929 indicates users were experiencing failed config saves even with correct tokens in `.security.yml`. This was a persistent, confusing UX issue for web launcher users.

- **Pain: Slack media attachment failures.** Users depending on Slack as a channel face a hard failure for all image uploads — a silent takeover blocking an otherwise functional channel.

- **Satisfaction signal:** The fact that the community has filed bugs with clear root causes and proposed fixes (especially around Slack `FileSize` and the Exa PR) indicates a technically engaged user base that trusts the project enough to contribute diagnostics.

## 8. Backlog Watch

- **[PR #3299 — Exa web search provider](https://github.com/sipeed/picoclaw/pull/3299) — stale for 30 days**: Zero maintainer comments despite a complete implementation. This is the most urgent item needing attention; either a review, a request for changes, or a clear "not now" to prevent contributor frustration.

- **[Issue #806 — Web UI support](https://github.com/sipeed/picoclaw/issues/806) — open 182 days**: While tagged as roadmap/high priority, the 6-month age without a merged implementation (though refactoring is indicated) deserves an explicit status update to set community expectations.

- **[Issue #3338 — Slack media size bug](https://github.com/sipeed/picoclaw/issues/3338) — 1 comment, 7 days old**: Not yet stale, but the bug reports a clear-cut defect with an obvious fix. Early maintainer acknowledgment and a linked fix PR would prevent this from becoming another stale item.

Overall, PicoClaw is in a stable-but-sluggish state. The emphasis on Web UI and web integration fixes is coherent — suggesting the project is preparing a significant user-facing usability update — but the project needs faster triage on open PRs to maintain contributor morale.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-25

## 1. Today's Overview

NanoClaw is in a period of high-velocity integration work, with 21 PRs updated in the last 24 hours — a significant burst of activity suggesting a coordinated push toward a v2.4.0 milestone. The release of **v2.3.0** with its new per-agent Slack provisioning marks a major UX inflection point, and the development team is actively consolidating channel adapters (Mattermost, Dial), hardening the update controller, and building out durable state infrastructure for crash-safe operations. Issue volume is low (2 updated), but PR volume is intense, with multiple core-team members working on interconnected features — template-based agent creation, new channel integrations, and macOS-specific stability fixes. The project appears healthy and well-maintained, with a strong contributor pipeline and active maintainer review.

## 2. Releases

**v2.3.0** is the latest release, with one significant change:

- **[BREAKING] New Slack experience**: Per-agent provisioned Slack apps, agent spawning from Slack, and UX improvements are now available. This is a **gated decision** — classic single-bot Slack installs continue to work unchanged, and existing users are asked to make a migration decision rather than being force-migrated.
- New installs and non-Slack installations are unaffected by the breaking change gate.

*Migration note*: The release notes emphasize this is a decision gate, not a forced migration — classic Slack remains fully functional.

## 3. Project Progress

Three PRs were merged or closed in the last 24 hours:

- **[#2474] feat(setup): AI-coding-CLI picker** — Closed. Adds a registry framework so setup can hand off failed steps and headless utility tasks to either Claude Code or OpenAI Codex, with future providers (Aider, Gemini-CLI) as drop-in adapters.
- **[#2475] feat(codex): surface skills + persona to codex agents** — Closed. Brings Codex agents to parity with Claude Code agents by exposing the same persona and skill catalog, making provider switching a config change instead of a content rewrite.
- **[#2767] Telegram: legacy-Markdown sanitizer obsoleted** — Closed. The workaround in `src/channels/telegram-markdown-sanitize.ts` is no longer needed since `@chat-adapter/telegram@4.30.0` fixes upstream `parse_mode` handling.

**Active feature development** (open PRs with recent updates):
- **[#3508] Durable host-coordination state** — Groundwork for crash-safe restarts: approval waiters, delivery retry counts, and stop/respawn intent currently live in process memory, meaning a crash loses state. This PR adds the DB-backed seams needed for durable coordination.
- **[#3396] + [#3428] Template-based agent creation** — Create agents from templates in chat (`create_agent` gains a `template` ref), with the Slack creation flow carrying the template ref end-to-end.
- **[#3502] + [#3507] Mattermost via NanoCo Chat SDK adapter** — Both a fix (migrate to the SDK adapter) and a new installation skill.
- **[#3503] Apple Container session driver** — A new session-driver overlay for macOS microVMs (`NANOCLAW_RUNTIME_DRIVER=container`).

## 4. Community Hot Topics

Activity is concentrated in core-team PRs rather than issue discussions, with 21 PRs updated in 24h. Key items:

- **[#3508] Durable host-coordination state** — The highest-signal PR today. Addresses a fundamental reliability gap: crash loops cause poison messages to retry forever, and "rebuild applied" state can be lost on restart. This is foundational infrastructure that multiple other features will build on.
- **[#3396] Create agents from templates in chat** — High community interest as it makes agent creation accessible from inside chat rather than requiring CLI or config work. Combined with [#3428], this represents a complete end-to-end flow.
- **[#3504] Reconcile 7 locally-committed feature branches** — A community member (Exclusiveicon) reconciled 20 commits of unpushed work against a diverged `origin/main`, rebuilding functionality on a fresh branch. This indicates significant community contribution depth, though the need to reconcile suggests discoverability/documentation of current branch state could improve.
- **[#3432] Dial channel post-merge follow-ups** — Active iteration on the recently-merged Dial channel integration: credential re-run handling, step captions, registry CI.

## 5. Bugs & Stability

**High severity:**

- **[#3497] better-sqlite3 v13 segfaults on macOS** (OPEN) — `better-sqlite3@13.0.3` segfaults inside `new Database()` on Node 22 versions older than 22.14.0. The declared Node floor is `>=22`, so affected users pass all checks but get a broken database layer — `pnpm test` cannot complete. **No fix PR yet.** This is the most pressing stability issue for macOS users.

**Medium severity (fixes in flight):**

- **[#3506] Update transaction controller incorrect on macOS** (OPEN PR) — Six fixes for the `/update-nanoclaw` transaction controller on macOS hosts, including one shared-code defect affecting Linux fallback mode. All defects were hit live during real macOS installs.
- **[#3499] Update controller symlink path comparisons** (OPEN PR) — Resolves symlinks in path comparisons, presumably failing on macOS where `/tmp` is symlinked to `/private/tmp`.
- **[#3505] Attachments routed through mailbox mounts** (OPEN PR) — Fixes attachment routing so they go through the selected mailbox mounts.

**Low severity / documentation:**

- **[#3500] Hardcoded gateway image tag during upgrade** (OPEN PR) — Documentation fix to catch a hardcoded OneCLI gateway image tag during upgrade.
- **[#3302] OneCLI gateway bind address** (OPEN PR) — Fixes `ONECLI_URL` being set to a docker bridge address that the gateway's own `docker-compose` never binds to.

## 6. Feature Requests & Roadmap Signals

Strong signal for the next minor release (v2.4.0 likely):

1. **Template-based agent creation in chat** ([#3396], [#3428]) — Clear roadmap item; the Slack flow is being re-ported after a premature merge, indicating maintainers want it done right.
2. **Durable coordination state** ([#3508]) — Foundational infrastructure that enables crash-safe restarts. Likely a v2.4.0 or v2.5.0 feature, and a prerequisite for production-grade multi-host deployments.
3. **Apple Container session driver** ([#3503]) — First overlay for the driver seam, suggesting a pattern for more runtime drivers.
4. **Mattermost via Chat SDK** ([#3502], [#3507]) — Converging adapter patterns — Mattermost now joins Dial on the Chat SDK, which reduces per-channel maintenance burden.
5. **AI-coding-CLI picker** ([#2474], [#2475]) — Closed but sets up future provider flexibility. Codex/Claude Code parity means switching providers is config-only.

**Long-running but active:** [#2361] Codex provider contract modernization and [#2337] Claude Code skill catalog for non-Claude providers — both from May, still open and being maintained.

## 7. User Feedback Summary

- **macOS stability concerns**: [#3497] (better-sqlite3 segfault) and [#3506] (update controller defects hit live during real macOS installs) both point to macOS being under-tested relative to Linux. Users hitting these are experiencing broken installs and failed update transactions.
- **Positive contributor experience**: [#3504] shows a community member invested enough to reconcile 20 unpushed commits against a diverged main. The detailed contributing guides (referenced in PR templates) appear effective.
- **Telegram users** benefit from the removal of the legacy sanitizer workaround ([#2767]) — upstream fix means one less NanoClaw-specific quirk.
- **Slack users** face a decision gate: the new per-agent provisioning is opt-in via the gating model, but the direction is clear — per-agent apps are the future, and single-bot installs will likely be deprecated eventually.
- **Active user needs**: template-based agent creation (in chat), crash-safe restarts, consistent channel adapter behavior, provider flexibility (Claude Code ↔ Codex).

## 8. Backlog Watch

No new unaddressed maintainer-attention items emerged today, but two long-running PRs deserve tracking:

- **[#2361] tighten codex provider contracts** (OPEN since May 9) — Updates the Codex provider to the current `codex app-server` JSON-RPC contract. Being actively maintained (updated Aug 24), but the 3.5-month lifespan suggests it's either complex or not a high enough priority to land.
- **[#2337] surface Claude Code skill catalog to non-Claude providers** (OPEN since May 7) — Would unlock Claude Code skills for Codex and other providers. Was likely superseded or is being absorbed into the [#2474]/[#2475] work that just merged.

**Worth watching**: [#3497] (better-sqlite3 segfault) has no fix PR after a day — if a fix doesn't land within the week, it may need escalation. The "declared floor is `>=22`" but the real floor is `22.14.0+` suggests a simple version-floor bump or a preflight check would resolve it.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-25

## 1. Today's Overview
NullClaw is showing a **quiet but active day**, with 2 open issues and 1 open PR touched in the last 24 hours, and no new releases. Activity is moderate-low: the project is in a maintenance/backlog state rather than an active development sprint. The two issues raised today highlight **configuration flexibility** and **user experience/logging concerns** around the gateway pairing flow. The lone PR is a long-running dependency bump (Alpine 3.23 → 3.24) that remains open after 10 weeks, suggesting potential CI/maintainer bottlenecks. Overall project health is stable, but there is a visible need for maintainer attention on stale PRs and the pairing token UX regression.

## 2. Releases
**No new releases** were published in the last 24 hours. The most recent release history shows no changelog activity, so there are no breaking changes or migration notes to report.

## 3. Project Progress
- **No PRs were merged or closed** in the last 24 hours. 
- The only PR updated is **#956** (dependabot) — an Alpine Docker base image bump that has been open since June 15 and is still pending review/merge.

## 4. Community Hot Topics
**Issue #993 — [ENHANCEMENT] Make Firecrawl search endpoint configurable**  
*Author: Crymfox | Created 2026-08-24 | 0 comments | [Link](https://github.com/nullclaw/nullclaw/issues/993)*  
This is the most forward-looking discussion today. The hardcoded `https://api.firecrawl.dev/v1/search` endpoint prevents self-hosted Firecrawl instances from being used. The underlying need is **deployment flexibility** — users want to run NullClaw with third-party services in self-contained environments. This is a simple config change (enviroment variable or config field) that could resolve a significant blocker for self-hosters.

**Issue #992 — [BUG] How to see pairing code if not logged to stdout and not written to disk?**  
*Author: heredos | Created 2026-08-24 | 0 comments | [Link](https://github.com/nullclaw/nullclaw/issues/992)*  
Direct fallout from a previous PR (#535) that changed logging behavior. The user spent days unable to retrieve the 6-digit pairing token for the gateway API because it now only exists in memory. This points to a **discovery/usability regression** introduced by a security improvement — the change removed one access path without providing a documented alternative.

## 5. Bugs & Stability
| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **High** | [#992](https://github.com/nullclaw/nullclaw/issues/992) | Pairing token inaccessible after #535 — no stdout output, no disk persistence, no documented retrieval method. Blocks users from configuring the gateway API entirely. | No fix PR open |
| **Low/Medium** | [#956](https://github.com/nullclaw/nullclaw/pull/956) | Docker base image outdated (Alpine 3.23 → 3.24); not a functional bug but a security/compat lag. | PR exists but unmerged |

No crashes or memory issues were reported. The primary stability concern is the **regression in the pairing flow** — it is a UX bug with zero workaround for affected users.

## 6. Feature Requests & Roadmap Signals
- **Configurable Firecrawl endpoint** ([#993](https://github.com/nullclaw/nullclaw/issues/993)): The request is straightforward — replace the const with a configurable value (env var like `FIRECRAWL_ENDPOINT` or config field). Given the low complexity and clear demand, this is a **strong candidate for the next minor release**. It aligns with NullClaw's self-hosting philosophy.
- **Pairing token fallback** ([#992](https://github.com/nullclaw/nullclaw/issues/992)): Implicitly a feature request — provide an alternative way to surface the pairing code (e.g., `--print-token` flag, file output, or a setup command). This should be prioritized alongside the bugfix.

**Prediction:** Next version will likely include an environment-variable/config-driven Firecrawl endpoint and a pairing code retrieval mechanism (CLI flag or file option).

## 7. User Feedback Summary
- **Pain Point (Critical):** The gateway API setup flow is broken for new users after #535. The pairing code is effectively invisible — the user spent multiple days attempting to configure the gateway. This suggests the project **lacks end-to-end documentation** for thesetup flow, and that security-focused changes (hiding secrets from logs) need to be paired with an accessible retrieval mechanism.
- **Pain Point (Moderate):** Self-hosted users are unable to use their own Firecrawl infrastructure due to hardcoded endpoints. This indicates that **third-party service integrations are designed for cloud/SaaS only**, which reduces the tool's appeal to the self-hosted community.
- **Satisfaction:** No positive feedback or "thank you" comments were recorded today; the signal is neutral-to-negative, focused on requests and blockers.

## 8. Backlog Watch
- **[PR #956 — Docker: bump alpine 3.23 → 3.24](https://github.com/nullclaw/nullclaw/pull/956)** — Open for **70+ days**, no activity. Likely blocked by CI or maintainer bandwidth. Container image users are running an outdated base OS; this is a basic hygiene item that should be merged or closed.
- **[Issue #992 — Pairing token visibility](https://github.com/nullclaw/nullclaw/issues/992)** — Blocking issue affecting setup; needs a maintainer response and a ticket link to the originating PR #535 for investigation.
- **[Issue #993 — Firecrawl endpoint config](https://github.com/nullclaw/nullclaw/issues/993)** — Simple enhancement, high community value; sits in "good first issue" territory and could be a quick win.

> **Health Note:** The project is in a *stable but minimally active* phase. No new features shipped in the past 24h, no regressions beyond the reported pairing issue, and a single stale dependency PR suggests the maintainers may be bandwidth-constrained. The two issues opened today are both actionable and low-effort, and addressing them would materially improve user onboarding and self-hosting flexibility.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-25

## 1. Today's Overview

IronClaw is in a **high-velocity stabilization phase**, with 56 items (issues and PRs) updated in the last 24 hours reflecting a coordinated push on both **CI reliability** and **the onboarding suggestions feature flow**. The most significant activity is a **four-lane CI expedite program** (T1–T4) where maintainer **henrypark133** is consolidating Rust setup, nextest pipelines, and E2E diagnostics — including two throwaway probe PRs (#7852, #7858) used purely for bisecting and validating Windows compatibility, demonstrating disciplined engineering under pressure. On the product side, **rdisandro** and **serrrfirat** are driving the "connect → suggest → thread" onboarding flow through its final gaps, while the **webui team (italic-jinxin)** is executing against a weekly dogfooding/QA epic (#7843) with shared component migrations and bug fixes. **No new releases** landed today; the project remains on `main` with v1.3.0 deployed in testing environments.

## 2. Releases

No new releases were published in this 24-hour window. Current deployed reference point is IronClaw 1.3.0 (commit `70795c16ed0cec21eb8cba16d2dcf851d25dc83d`).

## 3. Project Progress

The following notable pull requests were merged or closed today:

| PR | Title | Impact |
|----|-------|--------|
| [#7857](https://github.com/nearai/ironclaw/pull/7857) | `fix(webui): refresh conversations after starting suggestion` | Fixes the "suggested task thread not appearing in sidebar" bug (#7845) by refreshing the non-polling conversations query after a suggestion starts a server-side thread |
| [#7854](https://github.com/nearai/ironclaw/pull/7854) | `fix(webui): remove Gateway v2 login eyebrow` | Cosmetic cleanup removing stale branding from the login card across all 11 locale packs, with regression coverage |
| [#7821](https://github.com/nearai/ironclaw/pull/7821) | `ci: single setup-rust composite — toolchain pin, mold, centralized build profiles (T1)` | **Major CI milestone**: eliminates 43 scattered Rust toolchain invocations across 12 workflows, structurally preventing "green locally, red in CI" drift |
| [#7833](https://github.com/nearai/ironclaw/pull/7833) | `feat(suggestions): generate over the user's no-approval, read-only tools` | **Product milestone**: closes #7812 — suggestions now grounded in the user's actual connected data (Gmail, etc.) via read-only tool access, respecting user-level permissions |
| [#7794](https://github.com/nearai/ironclaw/pull/7794) | `refactor(webui): introduce shared page shell and loading primitives` | Migrates Automations, Extensions, Admin, Workspace, and Settings to shared `PageScroll`/`PageStack`/`Skeleton` primitives — a DRY consolidation |
| [#7255](https://github.com/nearai/ironclaw/pull/7255) | `docs(governance): evaluate the APDD kit` | Governance framework evaluation for IronClaw's agent product design process |
| [#7001](https://github.com/nearai/ironclaw/pull/7001) | `feat(loop): keep the cached system prefix byte-stable across model calls` | Closes #6985: stops the prompt-prefix mutation that was invalidating cache — nudges, timestamps, and per-run memory retrieval reorganized for byte-stable cache hits |

**Probes closed:** #7852 (BISECT), #7858 (Windows probe) — both throwaway diagnostic PRs, closed after reporting.

## 4. Community Hot Topics

The most active discussions this period (all with 1–3 comments; engagement remains focused on core contributors rather than broad community participation):

- **[#7812 — Onboarding suggestions: respect user-level tool permissions](https://github.com/nearai/ironclaw/issues/7812)** — 3 comments. Closed and resolved by PR #7833. The core need: suggestions were previously generated with only internal search tools, so they ignored the user's connected data entirely. This was a **fundamental product-quality gap** — the fix now grounds suggestions in real user accounts.
- **[#7798 — CI expedite T1: setup-rust composite](https://github.com/nearai/ironclaw/issues/7798)** — 3 comments. Closed by PR #7821. Underlying need: 43 duplicated `dtolnay/rust-toolchain` invocations were causing configuration drift and flaky CI. The maintainers are treating **CI reliability as a first-class product concern**, allocating multiple parallel tracks.
- **[#7297 — Error messages stack up in UI after every failed prompt](https://github.com/nearai/ironclaw/issues/7297)** — Still open, 2 comments. The UI accumulates stale error messages indefinitely after failures, degrading the experience. This is a **P2 QA bug** from bug bash that hasn't yet been assigned a fix.
- **[#7742 — Automations: bound creation preflight](https://github.com/nearai/ironclaw/issues/7742)** — Closed. Underlying need: the automation creation flow lacked an "honest execution contract" — it should distinguish authoring a future run from proving it can execute now.

## 5. Bugs & Stability

Ranked by severity:

| # | Bug | Severity | Status |
|---|-----|----------|--------|
| 1 | **[#7842 — Generic "invalid result" error during request execution](https://github.com/nearai/ironclaw/issues/7842)** | **High** — user-facing, unexplained failure | Open, no diagnosis yet; fed by x-ai-product-feedback |
| 2 | **[#7853 — Telegram personal account linking dead-ends](https://github.com/nearai/ironclaw/issues/7853)** | **High** — feature offered but non-functional | Open; the agent lacks a required tool for personal account linking |
| 3 | **[#7841 — Telegram setup dead-ends on "admin must configure"](https://github.com/nearai/ironclaw/issues/7841)** | High — related setup flow failure | Open, no diagnosis |
| 4 | **[#7856 — MCP tool discovery silently skips camelCase names](https://github.com/nearai/ironclaw/issues/7856)** | Medium — silent data loss; tools named `myTool` are inaccessible | Open; discoverability issue |
| 5 | **[#7297 — Error messages stack in UI after failures](https://github.com/nearai/ironclaw/issues/7297)** | Medium — UI degradation; P2 bug-bash item | Open; still unfixed after ~3 weeks |
| 6 | **[#7845 — Suggested task thread not in sidebar](https://github.com/nearai/ironclaw/issues/7845)** | Medium — cosmetic/UX, but confusing | **Fixed** by PR #7857 today |
| 7 | **[#7851 — Main branch CI failures](https://github.com/nearai/ironclaw/issues/7851)** | Medium — CI health | Closed; root-causing happening via T1/T2 probes |

**Context:** The two Telegram setup bugs (#7841, #7853) and the Slack connect-guidance gap (#7840) all came in through the **x-ai-product-feedback channel** (auto-posted by IronClaw itself), suggesting **integration setup flows are the #1 real-user pain point right now**.

## 6. Feature Requests & Roadmap Signals

Several issues point toward what's coming in **v1.4.0** (the next milestone tagged in issue metadata):

1. **[#7849 — Bundle an agent-first GSuite CLI for Google Workspace](https://github.com/nearai/ironclaw/issues/7849)** *(v1.4.0, P1, risk: high)* — Gmail extensions currently expose thin wire-format mappings (e.g., list returns IDs requiring follow-up reads; read returns nested MIME/base64). The proposed CLI would give the model a "thick" agent-friendly interface. **High likelihood for v1.4.0** given the P1 tag and existing GSuite extension base.

2. **[#7855 — Italian language support](https://github.com/nearai/ironclaw/issues/7855)** — Simple i18n addition, likely quick to implement given the existing 11-locale infrastructure.

3. **[#7840 — Slack connect guidance gap](https://github.com/nearai/ironclaw/issues/7840)** — Users report the app doesn't clearly guide them through Slack connection. This is a **UX onboarding gap** likely to be addressed in the current dogfooding epic (#7843).

4. **[#7825 — Sandbox egress auth: host credential broker](https://github.com/nearai/ironclaw/issues/7825)** — Extends the `gh` credential-mediation pattern (#7810) beyond GitHub to a general broker. This is a **security-architecture evolution** with broad implications.

5. **Italian i18n** (#7855) and **Gmail terminal-based setup documentation** (#6774, open since July 28) are smaller items that could land quickly.

## 7. User Feedback Summary

Real-user feedback this period, almost entirely routed through the **x-ai-product-feedback channel**:

- **Integration setup is the biggest friction point.** Three of five feedback issues relate to channel connections: Telegram personal-account linking fails (#7853), Telegram setup dead-ends with "admin must configure" (#7841), and Slack connect guidance is missing (#7840). The common thread: **the agent offers capabilities it cannot complete, with unclear error paths for users or guidance for admins**.
- **Unexplained errors undermine trust.** The generic "invalid result" error (#7842) halts a request with zero actionable context. For an AI agent product, opaque failures are particularly damaging because users can't determine if the model, tooling, or infrastructure failed.
- **Users expect suggestions grounded in their real data.** The closed #7812 reflects a design evolution: users want proactive suggestions that reflect their actual connected accounts, not generic boilerplate. This was received as a meaningful product improvement.

## 8. Backlog Watch

Items needing maintainer attention that have gone quiet or remain unresolved:

1. **[#6774 — Document Gmail terminal-based setup steps in Extensions > Registry UI](https://github.com/nearai/ironclaw/issues/6774)** — Open since **July 28** (nearly a month), only 1 comment. Users with Gmail extensions require CLI-based setup with no in-UI guidance. Still open despite the priority of the extension experience.

2. **[#7297 — Error messages stack up in UI after every failed prompt](https://github.com/nearai/ironclaw/issues/7297)** — Open since **August 6**, tagged P2, only 2 comments. The UI degradation is unglamorous but directly impacts daily usability. No fix PR has been opened in ~3 weeks.

3. **[#7456 — fix(reborn): make durable storage profile-agnostic](https://github.com/nearai/ironclaw/pull/7456)** — Large PR open since **August 10** with no visible review activity. This is a foundational storage-architecture change; a two-week stall on an XL-sized PR may indicate it's waiting on cross-team alignment on Reborn profile semantics.

4. **[#7516](https://github.com/nearai/ironclaw/pull/7516) and [#7826](https://github.com/nearai/ironclaw/pull/7826) — IronHub agent link surface + package installation** — Both from contributor **neo-sky** (marked `contributor: new`). These have been open for 13 and 2 days respectively with no visible review comments. For a new contributor shipping XL-sized PRs, the lack of maintainer response risks losing a contributor just when the project needs the momentum.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest - 2026-08-25

## 1. Today's Overview

LobsterAI maintained a healthy development velocity over the past 24 hours, with 11 PRs updated (10 merged/closed, 1 open) and 3 issues resolved (all closed as stale). The project shows strong activity in the renderer UI area, with significant feature work on library management, cowork interactions, and plugin installation UX. No new releases were published in this window. While all closed issues were marked stale, the quality and scope of merged PRs indicate active feature development and stability improvements across the platform.

## 2. Releases

No new releases were published in the last 24 hours. The project continues to operate on its existing release version.

## 3. Project Progress

The project merged 10 PRs covering multiple feature areas:

**Library & Artifacts Enhancement** (Major)
- [PR #2524](https://github.com/netease-youdao/LobsterAI/pull/2524): Introduced an isolated cross-platform thumbnail renderer supporting images, videos, PDF, Office, and HTML formats. Unified 16:9 thumbnail dimensions, caching strategies, and native fallback handling. Enhanced local artifact lifecycle management by displaying only artifacts tied to active tasks and preventing deleted-task delayed events from recreating relationships.
- [PR #2522](https://github.com/netease-youdao/LobsterAI/pull/2522): Improved file sharing and favorites interactions. Now preserves Unicode filenames during sharing packages (sanitizing only unsafe characters), maintains backward compatibility with legacy-generated filenames, and optimized favorites state with instant updates, filter removal, and failure rollback.

**Cowork/IM Improvements**
- [PR #2521](https://github.com/netease-youdao/LobsterAI/pull/2521): Fixed message selection preservation for the shared edit context menu. Assistant selected-text toolbar dismissal no longer clears selection before right-click or macOS Ctrl-click context menus open.
- [PR #2523](https://github.com/netease-youdao/LobsterAI/pull/2523): Added IM icon updates across renderer, docs, main, cowork, and IM areas.

**Plugin & Skills UX**
- [PR #2520](https://github.com/netease-youdao/LobsterAI/pull/2520): Made the plugin install modal viewport-constrained with independently scrollable content, logs, and error details. Added close button, shared modal cleanup, guarded IPC error handling, and lightweight renderer diagnostics for install attempts.
- [PR #2527](https://github.com/netease-youdao/LobsterAI/pull/2527): Skills tab now defaults to marketplace instead of persisting the last selected tab.

**Other UI/Infrastructure**
- [PR #2528](https://github.com/netease-youdao/LobsterAI/pull/2528): Added credits loading settings UI.
- [PR #2525](https://github.com/netease-youdao/LobsterAI/pull/2525): Login guide updates.
- [PR #2526](https://github.com/netease-youdao/LobsterAI/pull/2526): Updated some kit icon URLs.
- [PR #1193](https://github.com/netease-youdao/LobsterAI/pull/1193): Addressed SQLite write amplification by implementing debounce and batch transactions, eliminating the full `db.export()` + `fs.writeFileSync()` sequence on every row mutation.

## 4. Community Hot Topics

**Moderate engagement on context window configuration** ([Issue #1187](https://github.com/netease-youdao/LobsterAI/issues/1187), 3 comments, 1 👍): Users report "Context overflow: prompt too large for the model" errors with DeepSeek models. The request is to surface context window and output token settings directly in the model API configuration UI.

**Skill installation visibility bug** ([Issue #1195](https://github.com/netease-youdao/LobsterAI/issues/1195), 3 comments, 0 👍): Self-created skills install to the OpenClaw skill directory but don't appear in the LobsterAI skill panel after restart. This is a cross-system integration issue, confirmed as a reproducible bug on Windows 10 with version 2026.3.26.

**Default tool configuration override** ([Issue #1192](https://github.com/netease-youdao/LobsterAI/issues/1192), 2 comments, 0 👍): Users want a declarative "write-in" default configuration for existing tools (e.g., forcing headless browser mode) instead of relying on model instruction-following via memory, which is unreliable.

## 5. Bugs & Stability

**Skill Installation Visibility (Medium)** - [Issue #1195](https://github.com/netease-youdao/LobsterAI/issues/1195): Self-created skills not appearing in the skill panel after restart despite successful installation to the OpenClaw skill directory. This is a user-facing functionality gap in a core workflow (skill management). No linked fix PR yet.

**Context Overflow with DeepSeek (Medium)** - [Issue #1187](https://github.com/netease-youdao/LobsterAI/issues/1187): Context overflow errors with DeepSeek models due to incompatible context window settings. This could be a configuration mismatch or model-specific limitation that warrants investigation into how context windows are negotiated per model.

**SQLite Write Amplification (Resolved)** - [PR #1193](https://github.com/netease-youdao/LobsterAI/pull/1193): Eliminated performance bottleneck where every row mutation triggered a full database export and file write. Fixed via debounce and batch transactions. This is now resolved.

**Plugin Install Modal Overflow (Resolved)** - [PR #2520](https://github.com/netease-youdao/LobsterAI/pull/2520): Long error messages previously hid action buttons in the plugin install modal. Now constrained to viewport with scrollable content areas.

## 6. Feature Requests & Roadmap Signals

Several user requests point to the next version's priorities:

- **Configurable Model Context Settings**: [Issue #1187](https://github.com/netease-youdao/LobsterAI/issues/1187) requests per-model context window and output token configuration. This is likely to be scheduled given increasing LLM model variety and context differences.
- **Declarative Tool Defaults**: [Issue #1192](https://github.com/netease-youdao/LobsterAI/issues/1192) suggests offering "hard" configuration overrides for tools, potentially extending the current settings framework with default configuration injection.
- **Cross-platform Thumbnail Support**: The substantial [PR #2524](https://github.com/netease-youdao/LobsterAI/pull/2524) suggests the team is committed to robust local artifact handling. Future iterations may extend thumbnail support and asset lifecycle management.
- **Platform Integration (Windows)**: [Issue #1195](https://github.com/netease-youdao/LobsterAI/issues/1195) indicates Windows environments are actively used, reinforcing the need for continued Windows-specific testing.

## 7. User Feedback Summary

**Pain Points:**
- Context window overflow errors with models like DeepSeek remain confusing for users; they expect UI-level control over context settings.
- Cross-component integration (skills installed to OpenClaw but invisible via LobsterAI) causes confusion about system architecture and file locations.
- Relying on LLM instruction-following for persistent tool configuration (e.g., headless browser) is unreliable; users want explicit configuration injection.

**Satisfaction Indicators:**
- Positive reception to "credits loading settings UI" and login guide improvements suggests continued attention to onboarding and account experience.
- Collaborative editing context menu fixes indicate steady polish of the cowork experience.

## 8. Backlog Watch

**[PR #1277](https://github.com/netease-youdao/LobsterAI/pull/1277)** [OPEN for 4+ months]: Dependabot PR bumping the electron group (electron 40.2.1 → 43.4.1, electron-builder) across 1 directory with 2 updates. Dependencies of this age carry meaningful security/compatibility risk (3 major version jumps). Maintainers should review and merge soon or close with a planned upgrade path.

**[PR #1193](https://github.com/netease-youdao/LobsterAI/pull/1193)** [CLOSED, created 2026-04-01]: Closed despite touching the sql.js persistence layer. Since one fix in this area was accepted, the failure to merge a debounce + batch performance fix is notable. This could signal either a rejected approach or an accepted alternative soon to be released.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-25

## 1. Today's Overview

Moltis is in a **high-velocity maintenance and feature-expansion phase** with 19 PRs updated in the last 24 hours — a very busy day for the project. The team closed 16 PRs (including several multi-day efforts) and merged fixes across providers, browser sandboxing, messaging channels, and memory systems. One new release (20260824.01) was published, reflecting the day's accumulated changes. The project shows healthy momentum with active pull requests still open for Coder sandbox support, OpenAI tool-schema compatibility, and cron channel-context preservation.

---

## 2. Releases

**Version `20260824.01`** was published on 2026-08-24. No detailed changelog was included in the release metadata, but the version number correlates with the large batch of merged PRs from the past day (WhatsApp file persistence, browser stealth mode, Apple container ID fixes, and more). Operators should note this is a **calendar-versioned release** (YYYYMMDD.NN); no breaking changes or migration notes were announced.

---

## 3. Project Progress

**16 PRs were merged/closed** in the last 24 hours. Notable completed work:

| Area | PR | Summary |
|------|----|---------|
| **Providers** | [#1240](https://github.com/moltis-org/moltis/pull/1240) | New `xai-oauth` provider enabling Grok via SuperGrok/X Premium+ subscriptions (device-code OAuth) |
| **Apple sandbox** | [#1237](https://github.com/moltis-org/moltis/pull/1237) | Fixed container identifier >64 chars causing startup failures; SHA-256 suffix approach |
| **Messaging** | [#1238](https://github.com/moltis-org/moltis/pull/1238) | Tool access in shared Slack channels via `untrusted_tools` policy |
| **Messaging** | [#1228](https://github.com/moltis-org/moltis/pull/1228) | Inbound WhatsApp files persisted for local tools (20MB bound) |
| **Browser** | [#1227](https://github.com/moltis-org/moltis/pull/1227) | Obscura stealth mode enabled by default (`obscura_stealth`, configurable) |
| **Browser** | [#1229](https://github.com/moltis-org/moltis/pull/1229) | Browserless v2 container protocol support (v1 preserved as default) |
| **Gateway/security** | [#1179](https://github.com/moltis-org/moltis/pull/1179) | Node pairing signature verification — security hardening |
| **Cron** | [#1226](https://github.com/moltis-org/moltis/pull/1226) | Scheduled output delivered to originating chat (not just gateway) |
| **MCP** | [#1231](https://github.com/moltis-org/moltis/pull/1231) | Stale MCP client after server restart now resolved dynamically |
| **Memory** | [#1235](https://github.com/moltis-org/moltis/pull/1235), [#1236](https://github.com/moltis-org/moltis/pull/1236) | Config normalization (`sqlite`→`builtin`) and embedding batch bounds |
| **TTS** | [#1242](https://github.com/moltis-org/moltis/pull/1242) | Coqui no longer treated as "configured" by default — fixes false warnings |
| **Heartbeat** | [#1241](https://github.com/moltis-org/moltis/pull/1241) | `active_hours` actually enforced; `end=24:00` now valid |
| **i18n** | [#1225](https://github.com/moltis-org/moltis/pull/1225) | Major zh-TW Traditional Chinese locale overhaul |
| **Skills** | [#1234](https://github.com/moltis-org/moltis/pull/1234) | Recursive bundled sidecar files (e.g., `quick_validate.py`) now materialized |

---

## 4. Community Hot Topics

The most active items today (by comments plus recency):

1. **[Issue #1239 — xAI Grok OAuth provider](https://github.com/moltis-org/moltis/issues/1239)** — *2 comments, closed by PR #1240 in under 24 hours.* User [SP-937-215] filed a proper feature request and the maintainers shipped it immediately. Demonstrates a responsive maintainer team that acts on well-scoped requests.

2. **[Issue #1137 — Apple Container ID exceeds name limit](https://github.com/moltis-org/moltis/issues/1137)** — *1 comment, ~2 months old, now closed by PR #1237.* Long-standing bug resolved. The delay suggests this was an intermittent, environment-specific issue.

**Underlying signal:** Both hottest items are integration-edge cases (third-party subscription login, Apple-specific filesystem constraints). The community is actively using Moltis in heterogeneous environments, and the team responds quickly to clear, well-documented reports.

---

## 5. Bugs & Stability

| Severity | Bug | Status |
|----------|-----|--------|
| **High** | **Apple container ID >64 chars** causing startup failures ([#1137](https://github.com/moltis-org/moltis/issues/1137)) | Fixed in [#1237](https://github.com/moltis-org/moltis/pull/1237) |
| **High** | **Local GGUF memory embeddings can crash the process** when input exceeds 512 tokens ([PR #1236](https://github.com/moltis-org/moltis/pull/1236) — unbounded `n_batch` vs `n_ctx`) | Fixed in [#1236](https://github.com/moltis-org/moltis/pull/1236) |
| **Medium** | **MCP tool dispatch through closed client after server restart** — silent failures until next turn ([#1231](https://github.com/moltis-org/moltis/pull/1231)) | Fixed in [#1231](https://github.com/moltis-org/moltis/pull/1231) |
| **Medium** | **Red misleading warnings**: `provider 'coqui' not configured` when TTS is unset ([#1114](https://github.com/moltis-org/moltis/pull/1242) — root cause in auto-select logic) | Fixed in [#1242](https://github.com/moltis-org/moltis/pull/1242) |
| **Medium** | **`active_hours` not enforced** in heartbeat; `end=24:00` treated as invalid ([#1241](https://github.com/moltis-org/moltis/pull/1241)) | Fixed in [#1241](https://github.com/moltis-org/moltis/pull/1241) |
| **Low** | WhatsApp inbound docs exposed as metadata-only, no local file path for tools ([#1228](https://github.com/moltis-org/moltis/pull/1228)) | Fixed in [#1228](https://github.com/moltis-org/moltis/pull/1228) |

No new unfixed stability bugs remain open from today's activity.

---

## 6. Feature Requests & Roadmap Signals

Three **open PRs** indicate clear near-term roadmap items:

1. **Coder remote workspace sandbox** ([#1199](https://github.com/moltis-org/moltis/pull/1199)) — ephemeral cloud workspaces via REST API + reconnecting PTY WebSockets. Large feature (open since Aug 15); likely lands next release.
2. **OpenAI-safe tool schemas** ([#1232](https://github.com/moltis-org/moltis/pull/1232)) — `additionalProperties=false` strict-mode compliance; needed for Codex compatibility.
3. **Cron channel-context preservation** ([#1243](https://github.com/moltis-org/moltis/pull/1243)) — follow-up threads retain origin destination; complements merged [#1226](https://github.com/moltis-org/moltis/pull/1226).

**Prediction for next version:** The xAI OAuth provider (#1240, just merged) and Coder sandbox support (#1199, in review) are the headline features for the next `20260825` or `20260826` build. The OAuth pattern (OpenAI Codex → GitHub Copilot → xAI Grok) strongly suggests the team is building a universal subscription-provider abstraction.

---

## 7. User Feedback Summary

**Pain points (all resolved or resolved-by-today):**
- Apple users on newer macOS experienced sandbox startup failures due to container name length — now stable.
- Users running local GGUF embeddings hit hard crashes on long inputs — now bounded.
- WhatsApp users couldn't get files into local tools (images, documents) — now persisted.
- TTS warnings confused users when no TTS was configured — now silenced.

**Satisfaction signals:**
- Contributors are **repeat users** (SP-937-215, penso, rubenssoto, IlyaBizyaev all submitted multiple PRs) — a strong sign of an engaged developer community.
- Feature requests are being shipped within **24 hours** of filing (Issue #1239 → PR #1240).
- The new `xai-oauth` provider was requested and delivered in the same day — extremely positive responsiveness.

**Underlying user profiles:** Mix of individual developers (API-key users), **subscription owners** (Copilot, Codex, Grok), and **multi-channel power users** (WhatsApp + Slack + Telegram). Browser tooling users want stealth-first defaults (Obscura) — suggesting real-world anti-detection needs.

---

## 8. Backlog Watch

Items that may need maintainer attention — **none critical today**:

- **[PR #1199 — Coder remote workspace sandbox](https://github.com/moltis-org/moltis/pull/1199)** — open for 10 days with no comments. A major feature. Needs a review pass or maintainer input; it's the longest-pending open PR.
- **[PR #1232 — OpenAI-safe tool schemas](https://github.com/moltis-org/moltis/pull/1232)** — open 3 days, also no comments. Compatibility fix that affects Codex integration for all users; should be prioritized.
- **[PR #1243 — Cron channel context](https://github.com/moltis-org/moltis/pull/1243)** — filed today; likely will merge soon given the pace.

No issues are sitting unanswered beyond the project's rapid-response norm. The only "watch" signal is the low-comment activity on three open PRs, which may simply reflect weekend timing (Aug 23–24 weekend) rather than neglect.

---

## Project Health Assessment

**Very healthy.** The project demonstrates: rapid issue-to-fix turnaround, a contributor community with consistent names, steady release cadence, active security hardening (#1179), and a clear growth path (OAuth providers, cloud sandboxes). The mix of functional fixes (browser, messaging), infrastructure hardening (MCP, memory), and user-facing features (i18n) shows balanced engineering. No regressions or critical failure reports remain open.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-25

## 1. Today's Overview

CoPaw (QwenPaw) shows **high community activity** with 50 issues and 47 PRs updated in the last 24 hours. The project remains in active development with the release of **v2.1.1-beta.2**, focused on console artifact display improvements, video tool-result delivery on the OpenAI Responses API, and browser test fixes. A significant portion of current activity centers on **session-identity and cross-session bugs** (issues #6921, #7011, #7231), which appear to be a systemic challenge affecting multi-session console usage. The community continues to strongly advocate for **multi-agent collaboration improvements** (#3224, #6925, #3013) and **message aggregation** (#5563). Several first-time contributor PRs are in review, suggesting healthy project onboarding and documentation-driven contribution opportunities. Overall, the project is progressing steadily with substantial community engagement, though recurring stability issues around session handling and memory growth warrant close monitoring. The maintainers are actively merging fixes daily, including memory compaction restorations (#7234) and critical Docker CI corrections (#7248).

---

## 2. Releases

### v2.1.1-beta.2

A new beta release was published. Key changes:

- **feat(console)**: Added artifacts display to assistant response cards ([PR #7161](https://github.com/agentscope-ai/QwenPaw/pull/7161))
- **fix(video)**: Deliver tool-result videos on OpenAI Responses API ([PR #7061](https://github.com/agentscope-ai/QwenPaw/pull/7061))
- **test(browser)**: Boun(cy?) test fixes and stabilization

**Migration notes**: None indicating breaking changes. Existing beta users can likely upgrade seamlessly; however, users on Windows 11 (v2.1beta2) should monitor the known issue where the agent halts mid-task without visible notification ([Issue #6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)).

---

## 3. Project Progress

**Merged/Closed PRs (26 total)** in the last 24 hours:

### Memory & Stability
- **[#7234](https://github.com/agentscope-ai/QwenPaw/pull/7234) [CLOSED - DO NOT MERGE]** `fix(memory)`: Restore periodic ReMe index compaction — addresses unbounded BM25 index growth due to missing `optimize_index_cron`. Tagged DO NOT MERGE, likely being reviewed/reworked.
- **[#7247](https://github.com/agentscope-ai/QwenPaw/pull/7247) [CLOSED - DO NOT MERGE]** `fix(providers)`: Stop sending media to SiliconFlow DeepSeek V4 — prevents crashes when unnamed multimodal capability is unknown. Also DO NOT MERGE.
- **[#7248](https://github.com/agentscope-ai/QwenPaw/pull/7248) [CLOSED]** `fix(ci)`: Derive Docker boundary version from package instead of hard-coded value — resolves out-of-sync Docker release builds.

### E2E & Testing
- **[#7173](https://github.com/agentscope-ai/QwenPaw/pull/7173) [CLOSED]** `fix(e2e)`: Re-anchored agents action cells and follow project-directory API rename, fixes broken selectors from the new Backend column (#6397).
- **[#7246](https://github.com/agentscope-ai/QwenPaw/pull/7246) [OPEN]** New integration coverage: 39 router/module test files (238 cases) exercising the HTTP surface, plus hardening of flaky cases.

### Other Closed
- **[#6067](https://github.com/agentscope-ai/QwenPaw/pull/6067) [CLOSED]** `feat`: More sensitive file patterns and allow global read control.

---

## 4. Community Hot Topics

### Most Discussed Issues

| Issue | Title | Comments | Status |
|---|---|---|---|
| [#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921) | Agent stops mid-task without message (needs "continue" prompt) | 11 | OPEN |
| [#6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) | Docker plugin/app marketplace shows maintenance unavailable | 9 | CLOSED |
| [#338](https://github.com/agentscope-ai/QwenPaw/issues/338) | Webhook feature request (3+ months old) | 8 | OPEN |
| [#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) | Console stop cancels active Feishu session (cross-session) | 8 | OPEN |
| [#3224](https://github.com/agentscope-ai/QwenPaw/issues/3224) | Natural-language-driven self-evolving agent team | 7 | OPEN |
| [#5563](https://github.com/agentscope-ai/QwenPaw/issues/5563) | Aggregate multi-step responses to prevent message spam | 6 | OPEN |
| [#7224](https://github.com/agentscope-ai/QwenPaw/issues/7224) | How to connect Aider CLI as an agent (Russian) | 6 | OPEN |

### Underlying Needs
1. **Reliability of multi-step tasks** (#6921): Users report the agent "plans" but doesn't execute, requiring a manual prompt. This appears to be a **high-priority behavioral bug** affecting real workflows.
2. **Cross-session/cross-channel identity isolation** (#7011): Stop requests in one UI session cancels active conversations in another session/channel — a **systemic session management flaw**.
3. **Multi-agent collaboration UX is fragmented** (#3224, #6925, #3013): Users want agent collaboration in a single conversation view without blind spots; they are asking for a more tightly integrated, observable collaboration channel.
4. **Message flooding** (#5563): One task = 10 messages = spam; the community is requesting message aggregation/pagination.
5. **Docker marketplace accessibility** (#6782): The plugin/market going offline in Docker (now closed — likely fixed).

---

## 5. Bugs & Stability

Ranked by severity — most critical first:

### 🔴 High
1. **[#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)** — Agent halts mid-task with no visible output; stalls until manual "continue". Multi-step workflows are effectively broken in 2.1beta2 on Windows 11. **No fix PR identified.**
2. **[#7231](https://github.com/agentscope-ai/QwenPaw/issues/7231)** — Console messages can be **sent to the wrong session** when switching sessions/pages while another session is generating. **Fix PR exists: [#7237](https://github.com/agentscope-ai/QwenPaw/pull/7237) (open)** — freezes session identity for chat sends.
3. **[#7222](https://github.com/agentscope-ai/QwenPaw/issues/7222)** — qwenpaw-backend memory grows unbounded to **20.7 GB** over ~2 days of runtime; distinct from the startup leak (#9). Related to heavy text workloads. Likely tied to ReMe index issue addressed by [#7234](https://github.com/agentscope-ai/QwenPaw/pull/7234) but tagged DO NOT MERGE.

### 🟠 Medium
4. **[#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011)** — Console stop request cancels an active Feishu session under multiple UI sessions. **No direct fix PR yet.**
5. **[#7242](https://github.com/agentscope-ai/QwenPaw/issues/7242)** — Dashboard takes **6+ minutes to load** with 74 spawned agents on Docker/API mode.
6. **[#6822](https://github.com/agentscope-ai/QwenPaw/issues/6822)** — Transient streamable HTTP MCP failure **permanently blocks** the active conversation after auto-reconnect.
7. **[#7199](https://github.com/agentscope-ai/QwenPaw/issues/7199)** — `daily_paper` `write_atomic` crashes on PDFs with surrogate characters (U+D800-U+DFFF).
8. **[#7210](https://github.com/agentscope-ai/QwenPaw/issues/7210)** — Built-in tools enabled in agent.json but not injected into session function schema (tool exposure inconsistency).
9. **[#5720](https://github.com/agentscope-ai/QwenPaw/issues/5720)** — Memory leak in v1.1.12.post2 with orphaned async tasks and unclosed HTTP sessions, eventually kills the process (older report).

### 🟡 Low
10. **[#7121](https://github.com/agentscope-ai/QwenPaw/issues/7121)** — Flaky macOS nightly: timing assertion in `test_sibling_sessions_run_without_serializing` — likely addressed by [#7246](https://github.com/agentscope-ai/QwenPaw/pull/7246).

### Closed Today (Notable)
- **#6074** (session context lost on agent switch) — closed as `invalid`.
- **#7221** `reload_agent()` drops plugin workspace-scoped registrations — closed, presumably fixed.
- **#7136** File card percent-encoded mojibake for non-ASCII filenames — closed.
- **#7230** Context compression interrupting task execution — closed.

---

## 6. Feature Requests & Roadmap Signals

Signals from both issues and PRs suggest several directions for upcoming releases:

### Promising Features Currently in PR Review (first-time contributors)
- **Pawport import flow** ([PR #6960](https://github.com/agentscope-ai/QwenPaw/pull/6960)): Import instructions, settings, skills, plugins, projects from Codex/Qoder into QwenPaw — strong onboarding feature.
- **PowerContext pluggable long-term memory backend** ([PR #7080](https://github.com/agentscope-ai/QwenPaw/pull/7080)): Alternative memory backend to ReMe — likely next-version candidate if quality is proven.
- **Workspace-scoped Skill preload policy** ([PR #7183](https://github.com/agentscope-ai/QwenPaw/pull/7183), [Issue #7182](https://github.com/agentscope-ai/QwenPaw/issues/7182)): On-demand vs preload Skill loading for specialized workspaces — aligns with the community desire for agent-specific setups.
- **OAuth2 refresh token rotation persistence** ([PR #7066](https://github.com/agentscope-ai/QwenPaw/pull/7066)): Fixes remote MCP with rotating refresh tokens — high-impact for MCP ecosystem.

### Community-Requested Features Likely in Next Releases
| Feature | Issue | Predictions |
|---|---|---|
| Webhook support | [#338](https://github.com/agentscope-ai/QwenPaw/issues/338) | *3+ months old* — has been requested for a long time but still open; community may need to voice more support. |
| Per-channel model configuration | [#7085](https://github.com/agentscope-ai/QwenPaw/issues/7085) | likely in next minor release if contributor interest grows |
| Multi-agent collaboration in single session | [#6925](https://github.com/agentscope-ai/QwenPaw/issues/6925), [#3013](https://github.com/agentscope-ai/QwenPaw/issues/3013) | Being actively discussed; a UI/UX redesign may be in the roadmap |
| Context compression only when idle | [#7230](https://github.com/agentscope-ai/QwenPaw/issues/7230) (closed) | The user's suggestion was closed, but its logic may influence future defaults |
| SQL database storage for sessions/configs | [#3425](https://github.com/agentscope-ai/QwenPaw/issues/3425) | open; enterprise-focused, low community buzz currently |
| Qwen_Code third-party agent harness | [#7181](https://github.com/agentscope-ai/QwenPaw/issues/7181) | new but clearly valuable, likely prioritised |

---

## 7. User Feedback Summary

### Real User Pain Points
1. **Unreliable multi-step execution** — repeated complaints that agent "plans" and then halts ([#6921](https://github.com/agentscope-ai/QwenPaw/issues/6921)); users are constantly prompted to type "continue".
2. **Session mix-ups** — sending to the wrong conversation ([#7231](https://github.com/agentscope-ai/QwenPaw/issues/7231)), stopping another session accidentally ([#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011)), context loss when switching agents ([#6074](https://github.com/agentscope-ai/QwenPaw/issues/6074)).
3. **Memory instability** ([#7222](https://github.com/agentscope-ai/QwenPaw/issues/7222), [#5720](https://github.com/agentscope-ai/QwenPaw/issues/5720)) — background process memory grows to 20GB; user has to manually restart.
4. **Message flooding** — multi-step task creation spams the chat ([#5563](https://github.com/agentscope-ai/QwenPaw/issues/5563)).
5. **Mobile/UI usability** — dashboard homepage entry placement and mis-click risk ([#7177](https://github.com/agentscope-ai/QwenPaw/issues/7177)); agent switching requires too much scrolling ([#7179](https://github.com/agentscope-ai/QwenPaw/issues/7179)).
6. **Onerous approval modes for long-term tasks** ([#7198](https://github.com/agentscope-ai/QwenPaw/issues/7198)) — approval needed for process artifacts interrupts overnight work, making automation impractical.
7. **Chinese-speaking users are highly active** — most detailed bug reports and feature requests are in Chinese; documentation is multilingual (CN/JP/EN), suggesting a strong East-Asian user base.

### Positive Signals
- Global README documentation is being actively corrected for consistency ([PR #7255](https://github.com/agentscope-ai/QwenPaw/pull/7255)), indicating maintainership attention to community-facing docs.
- Rapid merging of bug fixes and stable releases is occurring on a near-daily cadence.
- Docker marketplace outage (#6782) was fixed and closed — user pain was acknowledged and addressed.

---

## 8. Backlog Watch

### Long-Unanswered, High-Impact Issues (needing maintainer attention)

| Issue | Created | Age | Why It Matters |
|---|---|---|---|
| [#338](https://github.com/agentscope-ai/QwenPaw/issues/338) — Webhook support | 2026-03-02 | **5.7 months** | Oldest open enhancement with active community interest (8 comments, 👍). No maintainer response visible. |
| [#2420](https://github.com/agentscope-ai/QwenPaw/issues/2420) — Multi-agent UX: guidance, triggering, identity confusion | 2026-03-27 | 5 months | Oldest multi-agent feedback still open; directly addresses core usability complaints. |
| [#3013](https://github.com/agentscope-ai/QwenPaw/issues/3013) — Multi-agent communication in same session | 2026-04-07 | 4.6 months | Very similar to #6925 (which is newer but with 4 comments); suggests repeated user requests going unresolved. |
| [#3224](https://github.com/agentscope-ai/QwenPaw/issues/3224) — Agent teams via NL | 2026-04-10 | 4.5 months | Ambitious enhancement; several sub-issues have been partially raised by others. |
| [#5720](https://github.com/agentscope-ai/QwenPaw/issues/5720) — Memory leak v1.1.12.post2 | 2026-07-02 | 1.8 months | No explicit fix mentioned; still open though a related newer leak #7222 surfaced. |

### Stale PRs Under Review
- **[#6399](https://github.com/agentscope-ai/QwenPaw/pull/6399)** — Reranker UI config panel for ReMeLightMemoryCard — open since 2026-07-23, still under review after 33 days.
- **[#7080](https://github.com/agentscope-ai/QwenPaw/pull/7080)** — PowerContext memory backend — open since 2026-08-17, under review but not merged yet.
- **[#7066](https://github.com/agentscope-ai/QwenPaw/pull/7066)** — OAuth2 refresh-token rotation persistence — open since 2026-08-16, first-time contributor, under review.

---

## Conclusion

CoPaw is in a **healthy development state**: high contribution volume, responsive maintainers, active bug triage, and a growing first-time contributor pipeline. However, **session-identity bugs, multi-agent collaboration UX, and memory growth** remain the top structural challenges — impacting daily users and some of the highest-comment issues. The maintainers should prioritise a unified session-routing fix (#7237) and the long-pending multi-agent collaboration UX improvements to address the most repeated pain points next.

---

*Data source: GitHub — agentscope-ai/CoPaw (QwenPaw). Generated for 2026-08-25 using issue/PR activity over the past 24 hours.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

# ZeptoClaw Project Digest — 2026-08-25

## 1. Today's Overview
ZeptoClaw is in a **quiet but active** phase today, with a single open issue and no new releases or merged PRs in the last 24 hours. The sole activity centers on a well-scoped feature request (#650) aimed at making the interactive REPL more robust and user-friendly, which aligns with the project's focus on developer experience. While the absence of PRs suggests a lull in code churn, the presence of a detailed, high-quality feature proposal indicates ongoing community engagement with the tool's core interaction surface. No regressions or bugs were reported, suggesting the current codebase is stable. Overall, the project appears healthy with a steady, if modest, pulse.

## 2. Releases
No new releases were published in the last 24 hours. There is no release information to report for this period.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. As a result, there are no new feature implementations, fixes, or code changes to report from merged PRs today.

## 4. Community Hot Topics
The only active discussion is **Issue #650** ([link](https://github.com/qhkm/zeptoclaw/issues/650)) — *"feat(cli): REPL UX hardening - safe Ctrl+C/Ctrl+D, lone '/' command table"* — authored by **Suraware**, with 0 comments and 0 reactions so far. While it has no direct engagement metrics yet, the issue's detailed problem statement reveals strong underlying needs from the user community:
- **Session persistence**: Users are frustrated by accidentally terminating long-running REPL sessions with an errant Ctrl+C, which currently exits silently and destroys in-progress work. The proposed fix (graceful handling of Interrupted/Eof signals) addresses a major UX friction point.
- **Command discovery**: A lone `/` input currently falls into an obscure "Unknown command" error. The user's proposal for a command table (displaying available commands) signals a desire for better discoverability and a more forgiving interface, especially for new users exploring ZeptoClaw's agent.

This issue is a strong signal that the community values the CLI agent as a primary interaction mode and expects it to behave with the robustness of mature developer tools (e.g., shells like bash/irb).

## 5. Bugs & Stability
**No bugs, crashes, or regressions** were reported in the last 24 hours. The project appears to be in a stable state with no stability concerns requiring immediate attention.

## 6. Feature Requests & Roadmap Signals
The community is actively proposing improvements to the REPL layer, centered on **UX hardening** and **error-path refinement**:
- **Safe signal handling** (Issue #650): Supporting `SigInt`/`SigQuit` with a "do you want to exit?" prompt would prevent accidental session loss.
- **In-REPL command table** for `/` alone, guiding users to available commands — a low-cost, high-value addition that improves usability.

These suggestions align with a broader trend in AI-agent CLIs toward conversational escape hatches and better command discoverability. Given the specificity and clarity of the proposal, this functionality is a **strong candidate for the next minor release (e.g., v0.6.x)**, especially if maintainers are looking to polish the interactive experience before expanding agent capabilities.

## 7. User Feedback Summary
The community's primary pain point centers on **interactive session termination** — the fear of losing work due to silent exits on Ctrl+C/Ctrl+D is a real concern that affects trust in the REPL. The user's report also hints at a **discoverability gap**: new users may struggle to know what commands are available, leading to frustrating trial-and-error with the `/` prefix. There is an implicit demand for ZeptoClaw to mirror the safety rails of mature REPLs (e.g., Python's `python` shell or Node's `repl` module), which suggests the user community views ZeptoClaw not as a prototype but as a daily-driver tool. Overall, the feedback reflects a **positive engagement** — the user took time to write a detailed, constructively critical issue, indicating investment in the project's future.

## 8. Backlog Watch
No long-unanswered or critical issues requiring maintainer attention were identified. The single open issue (#650) is recent (created yesterday) and may be awaiting maintainer review; while it is not strictly "stale," prompt triage is recommended to keep community momentum high and to incorporate the proposed UX fixes into the planning roadmap.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the provided GitHub data for ZeroClaw (github.com/zeroclaw-labs/zeroclaw), here is the project digest for 2026-08-25.

---

# ZeroClaw Project Digest - 2026-08-25

## 1. Today's Overview
The project is in a highly active development phase, with a substantial volume of work moving through the pipeline. In the last 24 hours, 50 issues and 50 PRs were updated, indicating a strong pulse from the community and core team. While no new releases were published, the focus is clearly on stabilizing the codebase, addressing critical security bugs, and processing large-scale architectural changes. The maintainers are actively triaging a significant backlog, but the presence of high-severity (S0/S1) bugs and numerous large, long-running PRs suggests that a focused effort on merging and release readiness may be the next major milestone.

## 2. Releases
No new releases were published in the last 24 hours. The latest release remains at version 0.8.4, as referenced in a user bug report.

## 3. Project Progress
The project saw 5 PRs merged or closed, along with 7 issues closed. Key movements show that the team is actively fixing critical bugs and addressing test flakiness:

- **fix(tests): fix Windows platform test failures (#10208)**: Merged. This is a major CI stability improvement, addressing unsafe `bash` command usage on Windows and other platform-specific test bugs.
- **fix(channels): populate the typed media envelope from Telegram (#9563)**: Merged. This fixes a long-standing issue where Telegram media was only parsed into text, preventing downstream components from correctly detecting image attachments.
- **fix(providers): report the served model in reliable fallback failure logs (#10027)**: Merged. This fixes a critical diagnostics bug (#10023), ensuring logs now accurately report the model that actually served a request, rather than the initially requested one.
- **Issue #10143 [Task]: Make provider-call accounting lifecycle-complete** was closed, suggesting the related work to improve observability is complete.
- **Issue #10106 [Bug]: Exact proxy selectors reject supported transcription services** was closed, confirming a fix for a config/onboarding issue.

## 4. Community Hot Topics
The most active discussions are centered around high-impact architectural changes and critical security fixes. The data shows maintainers are heavily engaged in soliciting feedback and coordinating complex work.

- **#8603 RFC: ZeroClaw Chat Completions profile (24 comments)**: This is the most active thread. The community is intensely interested in exposing agent capabilities via the OpenAI-compatible protocol to work with tools like Open WebUI and LangChain. The "accepted" status and "high" risk tag suggest this is a major feature in active design.
- **#8692 [Tracker]: Maintainer decision queue for RFCs and design issues (14 comments)**: This tracker serves as a central hub to manage the decision process for multiple RFCs, signaling a bottleneck in maintainer capacity for reviewing the influx of proposals. Its high activity shows the community is actively waiting on these decisions.
- **#7431 Feature: Pre-turn tool elicitation hints (6 comments)**: A feature request to improve natural-language routing. The conversation indicates a desire for more intuitive agent behavior without explicit commands, suggesting a focus on agent usability.
- **Security-Focused Discussions**: Issues like #10165 (delegate bypassing risk profile) and user feedback in #10324 (cron rename race) are receiving comments, highlighting a strong community focus on security and safe agent operations.

## 5. Bugs & Stability
There are several significant bugs in the currently active issues, some of which have "in-progress" PRs that might be close to merging. The number of S2 and S1 bugs is a concern, but the team's rapid triage and "in-progress" labels on many of them indicate active remediation.

- **[S0] Independent delegate bypasses risk profile (#10165)**: A critical security flaw where a delegate agent can execute high-risk commands (like `rm`) even when its own config disallows them. An S0 issue means the project is taking this extremely seriously.
- **[S2] Config metadata remains English in localized surfaces (#9363)**: A UX and internationalization bug, rated high priority for polish.
- **[S2] Interactive agent session caps context at 32k tokens (#10068)**: A functional bug causing the agent to ignore configured context limits, degrading performance on long sessions.
- **[S1] cron tools cross-agent boundary (#10324, #9948)**: A newly filed bug (and a related blocked PR) where cron jobs are not scoped to their owning agent, allowing potential unauthorized actions.
- **Provider Failure Diagnostics (#10023, #9812)**: While #10023 is closed, #9812 remains open, noting that fallback providers can carry the primary's model ID, effectively breaking the fallback mechanism. This issue has been fixed in PR #10027, which was merged today, suggesting this issue will likely be closed soon.

## 6. Feature Requests & Roadmap Signals
The project is actively considering major new features, indicated by several "accepted" RFCs and trackers.

- **OpenAI-Compatibility Layer**: The RFC #8603 for a Chat Completions profile is accepted. This is a signal that the project is moving toward being a drop-in replacement for OpenAI backends, which would be a massive adoption driver.
- **Gateway/WebSocket Decoupling (#7759)**: An accepted in-progress feature to make turns resilient to connection drops. This is a significant UX improvement for the web UI.
- **Opt-in Single-Tool Provider Rounds (#10222)**: A new RFC to allow models to take intermediate steps after tool calls within a single turn, enabling more complex agent reasoning.

**Prediction for Next Version:** The next release will likely focus heavily on the **OpenAI Chat Completions profile** and the **security fixes** currently in progress (PRs #9948, #9977, #9830). Given the S0 security issue, a patch release containing urgent security fixes may precede the next minor version.

## 7. User Feedback Summary
User feedback is a mix of pain points from real-world use and validation of the project's direction.

- **Pain Point: Model Compatibility**: Users are hitting edge cases with specific providers, such as the NVIDIA model emitting literal pseudo-syntax instead of tool calls (#9820) and providers failing to fall back correctly (#9812).
- **Pain Point: Usability & Configuration**: The context limit bug (#10068) is an immediate usability issue for advanced users. Furthermore, the complexity of configuration is a recurrent theme, highlighted by issues like #9363 (localization) and PR #9707 (fixing a config migration issue).
- **Positive Signal**: The high number of "Tracker" issues (#8692) and contributions from "principal" and "distinguished" contributors show that the power-user community is deeply invested in the project's direction, even when decisions take time.

## 8. Backlog Watch
Several long-running, high-impact items are waiting for review or action from maintainers.

- **Inactive PRs Needing Author Action**: Many significant PRs are blocked on **`needs-author-action`**, not maintainers. This includes large, critical features like:
    - `feat(runtime): expose token accounting on history-trim events` (#9713)
    - `fix(config): migrate bare vision_model_provider to dotted alias ref` (#9707)
    - `fix(channels): restore supervised shell approval routing` (#10241)
    - `feat(anthropic): handle refusals with fallback notices` (#9272)
- **Blocked PRs on Maintainers**: The project has several PRs marked `do-not-merge` and `status:blocked`, which need maintainer decisions:
    - `fix(browser): make full browser automation opt-in` (#9830)
    - `fix(ci): guard temporary React Router RSC exception` (#9637)
    - `fix(cron): scope the cron tools to the calling agent` (#9948)
- **Long-Standing Issues**: The RFC for the Chat Completions profile (#8603) has not been updated since August 24th, and the OIDC milestone tracker (#8289) from June 24th still has only one comment, indicating slow progress on a major architectural component.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*