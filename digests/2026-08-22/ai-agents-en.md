# OpenClaw Ecosystem Digest 2026-08-22

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-22 00:29 UTC

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

# OpenClaw Project Digest — 2026-08-22

## 1. Today's Overview

OpenClaw shows a very active maintenance and release-hardening phase, with 500 issues and 500 PRs updated in the last 24 hours. The issue tracker remains heavily loaded with 488 open items, many flagged with `clawsweeper:no-new-fix-pr` and `clawsweeper:needs-maintainer-review`, indicating a significant maintainer bottleneck. PR activity is robust (117 merged/closed today), with a clear focus on addressing P0/P1 regressions reported against the `2026.8.1-beta.2` release, particularly around SQLite corruption, session state, memory leaks, and message delivery reliability. No new releases were published today. Project health is mixed: engineering output is high, but the volume of unresolved, long-standing reliability bugs (some dating back to March) suggests the backlog is a growing concern.

## 2. Releases

No new releases were published on 2026-08-22. The most recent release is the `v2026.8.1-beta.2` candidate, which is under active validation in issue #125626.

## 3. Project Progress

117 pull requests were merged or closed today. Key merged PRs highlight critical fixes and feature work:

- **#126424** (merged): A large, cross-channel fix ([`fix(gateway): keep conversation delivery within agent bindings`](https://github.com/openclaw/openclaw/pull/126424)) that addresses multi-agent operators discovering conversations or files outside their permissible bindings.
- **#116489** (merged): A security feature ([`feat(security): require acknowledgement for install policy warnings`](https://github.com/openclaw/openclaw/pull/116489)) adding an interactive acknowledgement step for `security.installPolicy` warnings.
- **#125471** (merged): Fix for the Control UI to keep Claude CLI OAuth available, resolving a refresh-ownership loss after a Gateway restart.
- **#127662** (merged): Fix for the gateway to fail streaming responses when agent runs fail, ensuring clients receive an error instead of a false success.
- Numerous smaller daily PRs (#127708, #127709, #127696, #127711) focus on UI polish, macOS app behavior, and minor bug fixes.

## 4. Community Hot Topics

The most active discussions are dominated by a few critical, high-severity issues with substantial user engagement:

- **[#91588 — Critical: Gateway Memory Leak](https://github.com/openclaw/openclaw/issues/91588)** (23 comments, P0): RSS growth from 350MB to 15.5GB over days causing OOM crashes and `launchd-handoff` restart cycles. This is a top-priority reliability concern with high user impact but no linked fix PR.
- **[#91009 — Codex PreToolUse hook relay CPU-bound](https://github.com/openclaw/openclaw/issues/91009)** (22 comments, P1): Spawns CPU-bound processes that stall gateway RPC. A bug with clear performance and reliability consequences, still awaiting a maintainer decision.
- **[#87744 — Codex-backed Telegram turns time out](https://github.com/openclaw/openclaw/issues/87744)** (18 comments, P1): Sessions repeatedly fail to reach `turn/completed`, causing message loss. High user frustration with no fix PR in sight.
- **[#125626 — Release validation: v2026.8.1-beta.2](https://github.com/openclaw/openclaw/issues/125626)** (18 comments): The ongoing validation of the beta release indicates a strong community participation in testing and a release process that is currently in a holding pattern.

**Underlying Need:** The community is heavily invested in core system stability and reliability, especially around session state management, message delivery, and memory usage. Users are reporting critical issues and are actively participating in release validation, showing a need for prompt resolution and stable releases.

## 5. Bugs & Stability

The following critical bugs were reported or are currently active, ranked by severity:

**Critical (P0) — Immediate Impact:**
- **[#91588 — Gateway Memory Leak](https://github.com/openclaw/openclaw/issues/91588):** Uncontrolled RSS growth leading to OOM crashes. **No fix PR exists.**
- **[#126821 — SQLite Corruption Recurs on Rebuilt DBs](https://github.com/openclaw/openclaw/issues/126821):** A "paralyzed gateway" mode on 2026.8.1-beta.2 causing data loss and crash loops. **No fix PR exists.**
- **[#125333 — totalTokens Inflation](https://github.com/openclaw/openclaw/issues/125333):** The fix in #123065 is incomplete, and the token inflation bug still reproduces on the beta, posing a data-accuracy issue.

**High (P1) — Major Impact:**
- **[#91009 — Codex Hook Relay CPU-bound](https://github.com/openclaw/openclaw/issues/91009):** Spawns CPU-bound processes, stalling gateway. **No fix PR exists.**
- **[#87744 — Telegram Turns Time Out](https://github.com/openclaw/openclaw/issues/87744):** Linked to message loss. **No fix PR exists.**
- **[#53408 — Write/exec Tool Params Dropped](https://github.com/openclaw/openclaw/issues/53408):** Silent parameter loss in long conversations causes incorrect behavior. **No fix PR exists.**
- **[#126246 — Telegram Durable Outbound Stuck](https://github.com/openclaw/openclaw/issues/126246):** Messages stuck in `send_attempt_started` and lost on restart. **No fix PR exists.**
- **[#45224 — Playwright Assertion Error Crashes Gateway](https://github.com/openclaw/openclaw/issues/45224):** Unhandled error causing a full crash and restart loop. **No fix PR exists.**

**Notable Fix PRs in Flight:**
- **[#120597 — Detect virtiofs/9p to prevent WAL corruption](https://github.com/openclaw/openclaw/pull/120597):** Aims to resolve SQLite WAL corruption on Docker/OrbStack/Podman. **Open.**
- **[#121478 — Preserve paired restart session refs](https://github.com/openclaw/openclaw/pull/121478):** Fixes session-state loss during restarts. **Open, ready for maintainer.**
- **[#120190 — Bounded resumable recovery for compaction](https://github.com/openclaw/openclaw/pull/120190):** Addresses failed pre-flight compaction. **Open, waiting on author.**

## 6. Feature Requests & Roadmap Signals

The community is pushing for features that improve user experience and address operational gaps:

- **UX and Interface Enhancements:**
    - [#42840 — MathJax/LaTeX Support](https://github.com/openclaw/openclaw/issues/42840): Rendering formulas in Control UI. (High 👍 count, low priority)
    - [#88154 — Slack Modal Support](https://github.com/openclaw/openclaw/issues/88154): Structured input for interactive workflows.
    - [#28300 — Theme Customization System](https://github.com/openclaw/openclaw/issues/28300): Preset themes and a studio for the Control UI.
    - [#50199 — Skill Priority Configuration](https://github.com/openclaw/openclaw/issues/50199): Intelligent skill selection.
    - [#52640 — Persistent Task-Status Surface](https://github.com/openclaw/openclaw/issues/52640): Authoritative status for long-running turns.

- **Operational and Reliability Features:**
    - [#57425 — Graceful Gateway Restart](https://github.com/openclaw/openclaw/issues/57425): Session recovery and notification on restarts.
    - [#45771 — Pace-Aware Rate Limiting](https://github.com/openclaw/openclaw/issues/45771): Built-in throttle control for autonomous agents.

- **Configuration and Control:**
    - [#53890 — Default Outbound Telegram Topic/Thread binding](https://github.com/openclaw/openclaw/issues/53890): Config-level output routing.
    - [#55249 — Session Labels/Nicknames](https://github.com/openclaw/openclaw/issues/55249): Easier session identification.

**Prediction:** Given the beta status and the focus on reliability, smaller UX features like MathJax support and session labels are likely candidates for a future minor release. More complex operational features like graceful restart are probably further out. The immediate roadmap seems heavily centered on stabilizing the current beta (SQLite, memory, delivery) before new features land.

## 7. User Feedback Summary

User feedback is a mix of frustration and constructive input, largely shaped by the current stability challenges.

**Pain Points:**
- **System Instability:** Users running production deployments report severe issues like memory leaks (#91588), SQLite corruption (#126821), and silent message loss (#87744, #53408). These directly threaten operational reliability and are a major source of dissatisfaction.
- **Frustrating Debugging Experience:** The '[Bug]: 看起来有人把工作路径hardcode进代码里](https://github.com/openclaw/openclaw/issues/51429)' issue, which turned out to be a hardcoded developer path, highlights user frustration when such obvious errors get merged.
- **Unclear Error States:** Users complain about a lack of actionable diagnostics for failures like silent context drops (#108215), SIGKILLs (#72240), and model switch failures (#58957), making it hard to troubleshoot.

**Positive Engagement:**
- **Active Bug Reporting:** The high volume of detailed, high-quality bug reports (e.g., #126821, #91588) indicates a vigilant and technically sophisticated user base that is invested in the project's success.
- **Strong Community Testing:** The release validation process for `v2026.8.1-beta.2` (#125626) shows a community willing to dedicate time to testing release candidates and reporting back, which is a positive sign for project health.

## 8. Backlog Watch

Several important, long-unanswered issues and PRs require maintainer attention:

**Critical Long-Standing Issues (P0/P1):**
- **[#91588 (P0, Memory Leak)](https://github.com/openclaw/openclaw/issues/91588):** Open since 2026-06-09, 23 comments, zero fix PRs. **Needs urgent maintainer action.**
- **[#91009 (P1, Codex Hook CPU)](https://github.com/openclaw/openclaw/issues/91009):** Open since 2026-06-06, 22 comments. **Needs a product decision and assignment.**
- **[#87744 (P1, Telegram Turn Timeout)](https://github.com/openclaw/openclaw/issues/87744):** Open since 2026-05-28, 18 comments. **Needs a maintainer review and fix.**
- **[#45224 (P1, Playwright Crash)](https://github.com/openclaw/openclaw/issues/45224):** Open since 2026-03-13. **A critical crash bug with a known cause but no fix PR.**

**Long-Standing Issues (P1/P2):**
- **[#53408 (P1, Write/Exec Params Missing)](https://github.com/openclaw/openclaw/issues/53408):** Open since 2026-03-24, 12 comments, including a maintainer. **Needs a fix.**
- **Registration of #51429:** A P2 bug [about a hardcoded path](https://github.com/openclaw/openclaw/issues/51429) open since 2026-03-21 with 13 comments. **An embarrassing regression that has been open for 5 months.**

**Stalled/Needing Proof PRs:**
- **[#121567 (P1, claude-cli narration)](https://github.com/openclaw/openclaw/pull/121567):** Status is `⏳ waiting on author` since 2026-08-10.
- **[#124448 (P1, Queued chats vs empty replies)](https://github.com/openclaw/openclaw/pull/124448):** Status is `⏳ waiting on author` since 2026-08-16.
- **[#124174 (P2, Session mutations no outcome)](https://github.com/openclaw/openclaw/pull/124174):** Status is `⏳ waiting on author` since 2026-08-15.

**Conclusion:** The project is in a high-activity state, but the sheer number of open critical issues, some lingering for months, alongside a significant volume of PRs indicates that maintainer bandwidth is a key bottleneck. The backlog of unresolved bugs and stalled PRs remains the primary risk to project health and user satisfaction.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report — 2026-08-22

## 1. Ecosystem Overview

The personal AI assistant and agent open-source landscape is in a **reliability-hardening phase** following a period of rapid feature expansion. Across all major projects, the dominant themes are: memory/session state integrity, message delivery guarantees, security sandboxing, and provider abstraction standardization. The ecosystem is bifurcating into two architectural camps — those building **gateway/multi-channel platforms** (OpenClaw, NanoClaw, Hermes Agent) and those building **standalone agent runtimes** (NanoBot, CoPaw, Moltis). Notably, the largest projects (OpenClaw, ZeroClaw, CoPaw) are all carrying **critical long-standing bugs** (memory leaks, SQLite corruption, data loss) that indicate the scalability ceiling of current architectures is being tested. The community is simultaneously demanding **proof-carrying observability** (Hermes Agent's "Architecture" series) and **configurable defaults** that respect power users.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Merged/Closed PRs | Release Status | Health Score | Primary Focus |
|---------|-------------|-----------|-------------------|----------------|--------------|---------------|
| **OpenClaw** | 500 updated / 488 open | 500 updated | 117 | v2026.8.1-beta.2 (validating) | ⚠️ **At Risk** | Reliability regression fixes |
| **Hermes Agent** | 50 updated | 50 updated | 1 | v0.20.5 (Aug 19) | 🟢 **Stable** | Architecture hardening, security |
| **NanoClaw** | 24 PRs updated | 24 updated | 11 | No release | 🟢 **Healthy** | Multi-track feature dev, Telegram overhaul |
| **ZeroClaw** | 50 updated | 50 updated | 3 | No release | ⚠️ **At Risk** | Security sandbox, S0 bug fixes |
| **CoPaw (QwenPaw)** | 34 updated | 36 updated | 12 | v2.1.1b2 bumped | 🟡 **Moderate** | v2.1.1-beta regression fixes, Hub feature |
| **NanoBot** | 5 recent | 37 updated | 23 | No release | 🟢 **Healthy** | Provider architecture refactor |
| **IronClaw** | 13 touched | 37 updated | 16 | 1.7 series | 🟢 **Healthy** | CI infrastructure overhaul |
| **Moltis** | 2 new | 8 updated | 1 | No release | 🟡 **Moderate** | Channel integration fixes |
| **LobsterAI** | 2 closed | 12 merged | 12 | v2026.8.21 | 🟢 **Healthy** | Library UX, analytics, i18n |
| **PicoClaw** | 1 new | 4 merged | 4 | No release | 🟢 **Stable** | Backlog clearing, protocol support |
| **NullClaw** | 0 | 1 open | 0 | No release | 🟢 **Stable** | Provider expansion (Eden AI) |
| **TinyClaw** | — | — | — | — | ⚪ **Inactive** | — |
| **ZeptoClaw** | — | — | — | — | ⚪ **Inactive** | — |

---

## 3. OpenClaw's Position

**Advantages:**
- **Unmatched community scale** — 500 issues/PRs updated in 24h dwarfs all peers; 117 merged PRs/day demonstrates massive contributor bandwidth
- **Multi-channel maturity** — Telegram, Slack, Discord, WhatsApp support with deep integration (though each has reliability gaps)
- **ClawSweeper automation** — automated issue triage pipeline is unique in this ecosystem
- **Release validation culture** — dedicated beta validation issue with 18+ comments shows community investment in quality

**Technical Approach Differences:**
- **Gateway-centric architecture:** OpenClaw routes all channels through a unified gateway with agent bindings — more modular than NanoBot's per-provider approach but more complex to debug (evidenced by memory leak and RPC stall issues)
- **SQLite persistence with WAL:** Unlike CoPaw's history.db (7.6G bloat) or Hermes's durable generation identity, OpenClaw's SQLite choice has proven fragile (virtiofs/9p corruption, session-state loss)
- **Hook relay system:** Codex PreToolUse hooks are CPU-bound and stall gateway RPCs — a design that differs from Hermes's typed completion proofs and IronClaw's transactional deployment plans

**Community Size Comparison:**
OpenClaw's community is roughly **10x larger** than the next-biggest project (Hermes Agent, CoPaw) by issue volume. This scale cuts both ways: more testers means faster bug discovery, but the maintainer bottleneck is severe — **5 P0/P1 issues have been open since March-June with zero fix PRs** (#91588, #91009, #87744, #45224, #53408).

**Verdict:** OpenClaw remains the **ecosystem reference implementation** but is at risk of ceding stability leadership to Hermes Agent and IronClaw if backlog continues growing.

---

## 4. Shared Technical Focus Areas

| Requirement | Projects Seeking | Specific Need |
|-------------|-----------------|---------------|
| **Session-state integrity** | OpenClaw, ZeroClaw, Hermes Agent | Persistent chat history survival across restarts; ZeroClaw's S0 data-loss on interrupted turns; OpenClaw's paired-restart refs |
| **Memory leak resolution** | OpenClaw, NanoBot | Gateway RSS growth to 15.5GB (OpenClaw #91588); DingTalk asyncio.Task leaks (NanoBot #5463) |
| **Tool-result size limits** | ZeroClaw, CoPaw | Configurable max_tool_result_chars, per-provider media caps, truncation visibility |
| **Per-session model overrides** | NanoBot, CoPaw | Users want mid-session model switching without instance restarts |
| **Provider abstraction standardization** | NanoBot, NullClaw, IronClaw | Typed usage contracts, OpenAI-compatible gateways, aggregated providers (Eden AI, ZeroRouter) |
| **Security policy enforcement** | ZeroClaw, OpenClaw, Hermes Agent | Delegate risk-profile bypass, secret redaction on egress, install-policy acknowledgments |
| **Approval workflow refinement** | CoPaw, IronClaw | Overnight autonomous work without approval prompts for scratch files only |
| **Graceful restart/update** | OpenClaw, Hermes Agent | Transactional deployment plans; session recovery on gateway restart |
| **Search/retrieval improvements** | CoPaw, NanoBot | Metasearch providers, embedding health-check configurability, cross-session memory contamination |
| **Platform-specific UX** | Hermes Agent, ZeroClaw, Moltis | Windows parity (cmd.exe hooks), macOS sleep/wake recovery, iMessage transcription |

---

## 5. Differentiation Analysis

| Project | Feature Focus | Target User | Architecture |
|---------|--------------|-------------|--------------|
| **OpenClaw** | Multi-channel gateway with bindings | Enterprise operators, power users | Gateway→agent→SQLite; hook relays |
| **Hermes Agent** | Fleet orchestration, desktop client, multi-profile | Multi-agent fleet operators | Durable generation identity, proof-carrying state; 323-PR rollups |
| **NanoClaw** | Channel SDK breadth (Matrix, Mattermost, WhatsApp) | Channel-agnostic bridge builders | Chat SDK adapters, branch-composition CI |
| **ZeroClaw** | Security-first sandboxing, ZeroRelay transport | Security-conscious enterprises | Plugin isolation, risk profiles, SOP engine |
| **CoPaw (QwenPaw)** | Creator tools, Hub multi-user, Chinese-market UX | Chinese-language users, Creator workflow | Agent.json config, session-scoped tools |
| **NanoBot** | Lightweight single-bot runtime, Dream memory | Hobbyists, single-channel users | Provider usage contracts, Dream cursor memory |
| **IronClaw** | CI/deterministic builds, MCP pluggability | Developer tooling, CI-focused teams | Rust-based, cargo-nextest, preflight gates |
| **Moltis** | WhatsApp/Slack integration polish | Messaging-first users | Channel connectors, cron/heartbeat background tasks |
| **LobsterAI** | Workbench/library, DSH experimental runtime | Academic/analytic users | Electron-like renderer/main split, cowork sessions |
| **PicoClaw** | Lightweight Go-based agent | Minimalist developers | WebFetch tooling, Anthropic-native protocol |
| **NullClaw** | Provider gateway aggregation | Multi-vendor API users | OpenAI-compatible provider classes |

---

## 6. Community Momentum & Maturity

**Tier 1 — High-velocity, feature-driven (weekly releases):**
- **NanoClaw, CoPaw, NanoBot** — merging 10-20+ PRs/day with diverse contributor bases; actively shipping features while fixing bugs

**Tier 2 — Reliability-focused, architectural hardening (monthly releases):**
- **Hermes Agent, IronClaw, LobsterAI** — deliberate investment in long-term correctness (typed proofs, CI unification, i18n compliance) over feature velocity

**Tier 3 — Stabilization/backlog-clearing (bi-weekly+):**
- **PicoClaw, NullClaw, Moltis** — low issue volume, reviewing aging PRs, incremental growth

**Tier 4 — At-risk (release-blocked):**
- **OpenClaw, ZeroClaw** — massive community engagement but critical bugs with no fixes; maintainer bandwidth is the bottleneck

**Inactive:**
- **TinyClaw, ZeptoClaw** — zero activity in 24h; likely dormant or abandoned

---

## 7. Trend Signals

1. **From "Works" to "Proves It Works"** — Hermes Agent's Architecture series (proof-carrying state, typed completion proofs) and IronClaw's deterministic preflight gates signal that **large-scale agent deployments now demand verifiable behavior**, not just feature completeness. Expect "completion proofs" to become a differentiator.

2. **Security Sandboxing is Table Stakes** — ZeroClaw's S0 delegate bypass, OpenClaw's install-policy acknowledgment, Hermes's NT-namespace path rejection (Claude Code port), and IronClaw's sandbox credential mediation all point to **security becoming a first-class feature** rather than an afterthought.

3. **Channel Fragmentation Drives Abstraction** — With Mattermost (NanoClaw), Eden AI (NullClaw), and ZeroRouter (ZeroClaw) landing, the ecosystem is consolidating toward **aggregated gateways and typed provider contracts**. Single-vendor integrations are becoming legacy.

4. **Memory is the Next Frontier** — NanoBot's Dream cursor, IronClaw's Mnesis MCP pluggability, ZeroClaw's SOP engine, and CoPaw's 7.6G history.db bloat all highlight **memory as the primary scalability constraint**. The projects that solve durable, non-leaking memory will win enterprise adoption.

5. **User-Configurable Limits** — Multiple projects face backlash over hardcoded values: OpenClaw's 60s timeouts, CoPaw's 5s health-check timeout, ZeroClaw's 32k token cap. Users demand **every timeout and limit be configurable** — a hygiene expectation that separates mature projects from immature ones.

6. **Autonomous-Mode Approval Gates** — CoPaw's "overnight autonomous work is impossible" and IronClaw's OOBE suggestion gating reveal a **tension between safety and utility**. The winning pattern is context-aware approvals (scratch files vs. pre-existing files), not blanket policies.

7. **Cross-Session Contamination** — CoPaw's memory search reading another session, ZeroClaw's Telegram reply-threads fragmenting memory, and Moltis's shared-channel tool failures point to **session isolation as an unsolved problem** across the ecosystem.

---

## Value for AI Agent Developers

| Project | Best For |
|---------|----------|
| **OpenClaw** | Production deployments at scale (with patience for reliability bugs) |
| **Hermes Agent** | Multi-agent fleets needing provable state and transactional updates |
| **CoPaw** | Chinese-market users, Creator workflows, self-hosted control planes |
| **ZeroClaw** | Security-hardened deployments, enterprise policy enforcement |
| **NanoBot** | Lightweight single-channel bots with Dream memory |
| **IronClaw** | CI/CD integrations, deterministic testing, MCP pluggability |

**Bottom line:** The ecosystem is healthy and expanding, but **reliability engineering has overtaken feature development** as the primary competitive battleground. Projects that ship fix PRs within 24h of bug reports (NanoBot, LobsterAI, IronClaw) are building trust faster than those with 5-month-old critical bugs (OpenClaw, ZeroClaw).

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Based on the GitHub data provided for NanoBot (HKUDS/nanobot) on 2026-08-22, here is the project digest:

---

## NanoBot Project Digest — 2026-08-22

### 1. Today's Overview

NanoBot is showing a **high-velocity development cycle** with significant merging activity. The project processed **37 Pull Requests** in the last 24 hours, with **23 merged or closed**, which signals strong maintainer throughput and an active contributor base. Core focus areas included **provider architecture standardization**, **memory/Dream subsystem stability**, and **WebUI/TUI polish**. While no new releases were cut today, the sheer volume of merged features and fixes suggests a major version bump may be imminent. The issue tracker is well-maintained, with 4 of the 5 recently updated issues being closed, indicating responsive maintainer engagement.

### 2. Releases

**No new releases** were published in the last 24 hours. The project is accumulating a substantial backlog of merged features (provider usage contracts, DeepSeek model support, TUI LaTeX rendering, etc.), so a release is likely within the next few days.

### 3. Project Progress

The **23 merged/closed PRs** show several major areas of advancement:

- **Provider Architecture Refactor**: PR [#5478](https://github.com/HKUDS/nanobot/pull/5478) merged a significant refactor defining a **typed LLM usage contract**, replacing dynamic dictionaries with immutable structures across OpenAI Chat, OpenAI Responses, Anthropic, and Bedrock providers.
- **Trajectory & Usage Tracking**: PR [#5479](https://github.com/HKUDS/nanobot/pull/5479) added a unified provider usage backend, recording retry-managed attempts, fallback leaves, and cancellations.
- **Bug Fixes (Cron & Dream)**: PR [#5407](https://github.com/HKUDS/nanobot/pull/5407) fixed persisted heartbeat/cron jobs not being disabled properly, and PR [#5442](https://github.com/HKUDS/nanobot/pull/5442) fixed the Dream memory cursor being permanently blocked by recovered tool errors.
- **New Feature: Metasearch Provider**: PR [#5234](https://github.com/HKUDS/nanobot/pull/5234) is open for **MST-Python**, a metasearch aggregation provider using Reciprocal Rank Fusion.
- **UX Improvements**: PR [#5476](https://github.com/HKUDS/nanobot/pull/5476) adds LaTeX-to-Unicode rendering in the TUI, and PR [#5477](https://github.com/HKUDS/nanobot/pull/5477) fixes iOS PWA safe-area handling.
- **Model Support**: PR [#5474](https://github.com/HKUDS/nanobot/pull/5474) merged support for **DeepSeek V4 Flash Vision**.
- **Safety & Security**: PR [#1149](https://github.com/HKUDS/nanobot/pull/1149) (merged) adds **PromptGuard** for prompt injection detection, while PR [#5414](https://github.com/HKUDS/nanobot/pull/5414) validates Slack file downloads across redirects.

### 4. Community Hot Topics

- **Model Switching Limitation (Issue #5198)** — [Link](https://github.com/HKUDS/nanobot/issues/5198)  
  The highest-traffic issue (4 comments) complains that NanoBot cannot switch models per-session without a full instance reconfiguration. The `/model` command and UI blip do not work as expected. This is a **high-demand UX feature** for parity with commercial AI chat UIs. The issue is now **closed**, though this may indicate a workaround was provided rather than a proper fix.

- **DingTalk Background Task Leak (Issue #5463)** — [Link](https://github.com/HKUDS/nanobot/issues/5463)  
  A **new, open bug** reports that DingTalk's inbound message handler uses `asyncio.Task` without a terminal observer, meaning background tasks may never drain or be cleaned up properly. This could lead to resource leaks in long-running gateways.

- **Metasearch Provider PR (#5234)** — [Link](https://github.com/HKUDS/nanobot/pull/5234)  
  This large open feature PR (created Aug 3) has stayed active for nearly three weeks, indicating community interest in a **more robust, aggregated search provider** beyond single-engine fallbacks.

### 5. Bugs & Stability

**High Severity:**

- **Mid-Stream Provider Errors Skip Retry (Issue #5454, Closed)** — [Link](https://github.com/HKUDS/nanobot/issues/5454)  
  A bug where `server_error` events during streaming are **not retried** once content has started streaming, leading to truncated responses. Closed, but with no visible fix PR linked, the fix may be in progress or deferred.

- **DingTalk Background Task Leak (Issue #5463, Open)** — [Link](https://github.com/HKUDS/nanobot/issues/5463)  
  The DingTalk channel may leak background tasks, potentially causing unbounded memory growth over time.

**Medium Severity:**

- **Dream Cursor Permanently Blocked (Issue #5441, Closed)** — [Link](https://github.com/HKUDS/nanobot/issues/5441)  
  Recovered tool errors incorrectly failed Dream runs and blocked the memory cursor, causing duplicate edits. **Fixed by PR #5442**.

**Low Severity:**

- **Notion MCP Connection Failure (Issue #1168, Closed)** — [Link](https://github.com/HKUDS/nanobot/issues/1168)  
  Users reported issues connecting to Notion MCP; the issue was closed after 2 comments, suggesting a workaround or user error was identified.

### 6. Feature Requests & Roadmap Signals

- **Per-Session Model Switching**: The community clearly wants the ability to change models mid-session (Issue #5198). Given the recent provider refactor (typed usage contracts), this feature is now more technically feasible. **Prediction: Likely in next minor release.**
- **Metasearch Provider (MST Python)**: PR #5234 is a major feature waiting to merge. Once reviewed, it will significantly improve search quality.
- **Manual-Only Skill Invocation**: PR #5405 is open and proposes a `disable-model-invocation` flag for skills. This has broad applicability for side-effect-heavy skills like deployment or payment.
- **Turn Observability**: PR #5420 is open and adds detailed per-turn observability and recovery, including provider usage accumulation and interrupted-work surfaces. This is a major UX upgrade.

### 7. User Feedback Summary

- **Pain Point / Dissatisfaction**: Users are **frustrated with rigid model selection**; they want the flexibility of switching models on the fly, similar to Claude or ChatGPT. The fact Issue #5198 accumulated 4 comments and was closed (likely with a workaround) suggests this remains an unmet need that could resurface.
- **Pain Point**: **MCP connectivity can be fragile**; users struggled with Notion authentication despite correct credentials.
- **Satisfaction / Positive Signals**: The high number of merged PRs and proactive bug fixes (e.g., Dream cursor, Slack redirects) indicates a responsive team. The new features (PromptGuard, LaTeX rendering, DeepSeek Vision) address both safety and usability concerns.

### 8. Backlog Watch

- **Issue #1168 (Notion MCP)** — [Link](https://github.com/HKUDS/nanobot/issues/1168)  
  Open since **February 2026**, this is **6 months old**. While closed, the underlying MCP debugging path may still lack documentation or logging improvements. At 2 comments, it received little attention.

- **PR #5234 (MST Metasearch Provider)** — [Link](https://github.com/HKUDS/nanobot/pull/5234)  
  Open for **19 days** with no visible reviewer comments in the data, this is a high-value feature PR that needs maintainer review. It is tagged `priority: p1`, indicating importance, but its lack of movement warrants watch.

- **PR #5405 (Manual-Only Skills)** — [Link](https://github.com/HKUDS/nanobot/pull/5405)  
  Open for 6 days, this feature has broad applicability but needs a decision on API naming and interaction with the existing `always: true` logic.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-22

## 1. Today's Overview

Hermes Agent is in a period of **high-velocity stabilization and architectural hardening**. The project shows 50 issues and 50 PRs updated in the last 24 hours, indicating a very active maintainer and contributor community. Activity is heavily concentrated on **reliability engineering** (install/update paths, session-state preservation, Windows platform fixes) and **security hardening** (secret redaction, credential-leak vectors, authority boundaries). The release of **v0.20.5** on August 19 rolled up ~323 PRs, providing a stable baseline for downstream consumers. A notable theme across many issues is the **"Architecture" series** (authored by andrexibiza), which proposes systemic fixes for recurring defect classes rather than one-off patches. The project is clearly investing in **proof-carrying state, transactional deployment plans, and unified control planes** as foundational invariants.

## 2. Releases

**v2026.8.19 — Hermes Agent v0.20.5** was released on August 19, 2026, as a **patch release** that rolls up **~323 PRs merged since v0.20.4** into a stable tagged release for downstream consumers (Docker images, hosted deployments, fresh installs). No breaking changes or migration notes are documented in the release notes.

## 3. Project Progress

Only **1 PR was merged/closed** in the last 24 hours:

- **[PR #85373](https://github.com/NousResearch/hermes-agent/pull/85373) [CLOSED]** — `fix(desktop): surface actionable error when Nous Cloud agent returns 503 (#85335)`. This fix improves the desktop client's error handling when a Nous-managed cloud agent returns HTTP 502/503/504, replacing the generic "Hermes backend did not become ready" message with actionable guidance. A clear quality-of-life improvement for cloud-agent users.

Additionally, **4 issues were closed**, including the large **"[COMPLETE] Large-file decomposition: 20/20 done"** epic ([#78647](https://github.com/NousResearch/hermes-agent/issues/78647)) — a significant refactoring milestone that sharded god-files into clean modules across the repo. Also closed: desktop session tab bar disappearance ([#88534](https://github.com/NousResearch/hermes-agent/issues/88534)) and a Python 3.14+ DaemonThreadPoolExecutor crash ([#91916](https://github.com/NousResearch/hermes-agent/issues/91916), marked duplicate).

## 4. Community Hot Topics

The most active discussions reveal a community deeply engaged in **reliability, security, and architectural soundness**:

1. **[Issue #78647 — Large-file decomposition epic (CLOSED, 78 comments)](https://github.com/NousResearch/hermes-agent/issues/78647)** — The most-commented issue this period. The repo-wide god-file sharding epic completed 20/20 tasks. This signals a strong maintainer commitment to code maintainability, with a standing policy that all god files are sharded and never reverted.

2. **[Issue #66616 — Skills index is stale/degraded (72 comments)](https://github.com/NousResearch/hermes-agent/issues/66616)** — A long-running automated freshness probe failure. The Skills Hub index is 29.8h old against a 26h limit. The community is clearly invested in the Skills Hub's reliability; 72 comments on an automated probe issue suggests active triage and repeated failed fix attempts.

3. **[Issue #79564 — Discord Feature Parity & Alignment Campaign (9 comments)](https://github.com/NousResearch/hermes-agent/issues/79564)** — A meta-issue coordinating a campaign to bring Hermes's Discord surface to full parity with Discord API v10/discord.py 2.7.1. Similar meta-issues exist for **WhatsApp ([#79890](https://github.com/NousResearch/hermes-agent/issues/79890))** and **Slack ([#79772](https://github.com/NousResearch/hermes-agent/issues/79772))**. This signals a strategic push for **platform feature completeness**.

4. **[Issue #91277 — Fleet update reliability tracking (7 comments)](https://github.com/NousResearch/hermes-agent/issues/91277)** — A P1 tracking issue acknowledging that install/update is "currently our least reliable capability" with ~30 open issues and ~15 open PRs all patching corners of the same problem. This is a self-aware, systematic response to a critical weakness.

**Underlying need:** The community is demanding **provable reliability and security** — not just "it works" but "here's the proof." This is visible across the "Architecture" issue series (proof-carrying state, typed completion proofs, durable generation identity) and the platform-parity campaigns.

## 5. Bugs & Stability

Bugs reported this period, ranked by severity:

| Severity | Issue | Summary | Fix PR? |
|----------|-------|---------|---------|
| **P1** | [#91277](https://github.com/NousResearch/hermes-agent/issues/91277) | Fleet update reliability is the project's least reliable capability (tracking meta-issue) | Multiple open PRs, no unified fix yet |
| **P2** | [#91927](https://github.com/NousResearch/hermes-agent/issues/91927) | Gemini session title generation fails — thinking tokens consume max_tokens budget, producing mangled markdown artifacts | **[PR #91933](https://github.com/NousResearch/hermes-agent/pull/91933)** — disables reasoning on title-generation pass |
| **P2** | [#91675](https://github.com/NousResearch/hermes-agent/issues/91675) | Windows: gateway start prints ✓ then dies after 6s liveness poll; only active profile resumes | No fix PR yet |
| **P2** | [#91684](https://github.com/NousResearch/hermes-agent/issues/91684) | Desktop approval responds 4001 "session not found" when routed to non-owning local gateway | No fix PR yet |
| **P2** | [#89083](https://github.com/NousResearch/hermes-agent/issues/89083) | Desktop chat unresponsive after macOS sleep/wake (half-open WebSocket never detected) | No fix PR yet |
| **P2** | [#90200](https://github.com/NousResearch/hermes-agent/issues/90200) | GitHub automation split authority: metadata writes succeed, repo-object writes fail with 403 | No fix PR yet |
| **P2** | [#77162](https://github.com/NousResearch/hermes-agent/issues/77162) | **Security:** exact-value applied-secret redaction missing on tool-result → provider egress path | No fix PR yet |
| **P2** | [#88758](https://github.com/NousResearch/hermes-agent/issues/88758) | Compression: raw durable watermark not preserved through replay cleanup | No fix PR yet |
| **P3** | [#43054](https://github.com/NousResearch/hermes-agent/issues/43054) | Gmail get returns only top-level MIME part — forwarded/nested email bodies dropped | No fix PR yet |
| **P3** | [#91260](https://github.com/NousResearch/hermes-agent/issues/91260) | IM entry cannot drive real multi-bot pipeline (SOUL handoff is fiction) | No fix PR yet |

**Security-critical new PR:** **[PR #91928](https://github.com/NousResearch/hermes-agent/pull/91928)** — File tools now reject Windows NT-namespace paths (`\??\...`, `\\.\...`, `\\?\UNC\...`) that leak NTLM credentials, porting Claude Code v2.1.234's hardening. This is a significant security improvement.

## 6. Feature Requests & Roadmap Signals

The "Architecture" issue series (all authored by andrexibiza) is the strongest roadmap signal:

- **[#90866](https://github.com/NousResearch/hermes-agent/issues/90866)** — Make observable state **proof-carrying** from source to side effect
- **[#90049](https://github.com/NousResearch/hermes-agent/issues/90049)** — Make **false success** a first-class defect class with typed completion proofs
- **[#90145](https://github.com/NousResearch/hermes-agent/issues/90145)** — Recovery/teardown fenced by **durable generation identity**
- **[#90144](https://github.com/NousResearch/hermes-agent/issues/90144)** — **Proof scope must equal mutation scope**
- **[#91911](https://github.com/NousResearch/hermes-agent/issues/91911)** — Make **Bot Mode identity, capability, delivery, cancellation** one control plane
- **[#88683](https://github.com/NousResearch/hermes-agent/issues/88683)** — Make install/update/bootstrap obey **one transactional deployment plan**
- **[#90150](https://github.com/NousResearch/hermes-agent/issues/90150)** — Treat **built artifacts and real protocol peers** as part of the system under test
- **[#91230](https://github.com/NousResearch/hermes-agent/issues/91230)** — **Task Completion Verification** — exact-object completion as the "sixth Hermes law"

**Prediction:** The next minor release (v0.21.x) will likely include the **transactional deployment plan** ([#88683](https://github.com/NousResearch/hermes-agent/issues/88683), [#91277](https://github.com/NousResearch/hermes-agent/issues/91277)) and the **typed completion proofs** ([#90049](https://github.com/NousResearch/hermes-agent/issues/90049)) as foundational changes. The **platform parity campaigns** (Discord, WhatsApp, Slack) will continue to land incrementally.

## 7. User Feedback Summary

**Pain points (real user reports):**

- **Windows reliability** remains a sore spot: gateway start failures ([#91675](https://github.com/NousResearch/hermes-agent/issues/91675)), approval resolution from toast clicks ([#89988](https://github.com/NousResearch/hermes-agent/pull/89988)), and cron fence timing ([#87911](https://github.com/NousResearch/hermes-agent/pull/87911)) all target Windows-specific issues.
- **macOS stability:** Desktop chat unresponsive after sleep/wake ([#89083](https://github.com/NousResearch/hermes-agent/issues/89083)) is a significant UX break.
- **Linux/Wayland:** HUD drag broken on Wayland compositors ([#82851](https://github.com/NousResearch/hermes-agent/issues/82851)) — setPosition is a no-op.
- **Multi-profile complexity:** Users report that **"SOUL handoff is fiction"** ([#91260](https://github.com/NousResearch/hermes-agent/issues/91260)) — IM entry cannot drive a real multi-bot pipeline, which is a core use case for Hermes's multi-agent fleet vision.
- **Bot mode UX:** Bot sessions hidden from Sessions sidebar with no browsing path ([#91740](https://github.com/NousResearch/hermes-agent/issues/91740)).
- **Email skill limitations:** Gmail get drops forwarded/nested email bodies ([#43054](https://github.com/NousResearch/hermes-agent/issues/43054)).
- **Provider-specific bugs:** Gemini title generation mangled ([#91927](https://github.com/NousResearch/hermes-agent/issues/91927)); OpenRouter model list frozen without TTL ([#91929](https://github.com/NousResearch/hermes-agent/pull/91929)).

**Satisfaction signals:** The community is actively contributing fixes (20+ PRs open with fresh updates), which indicates a healthy, engaged contributor base. The 323-PR rollup into v0.20.5 suggests strong momentum.

## 8. Backlog Watch

These items need maintainer attention:

1. **[Issue #66616 — Skills index stale/degraded (72 comments, open since 2026-07-18)](https://github.com/NousResearch/hermes-agent/issues/66616)** — A month-old automated probe keeps failing with no mergeable fix. The 72 comments suggest churn without resolution. This is a "death by a thousand cuts" issue that erodes community trust in the Skills Hub.

2. **[PR #58146 — reset auth cooldowns across profiles (open since 2026-07-04)](https://github.com/NousResearch/hermes-agent/pull/58146)** — A 7-week-old PR touching auth across profiles. Auth is security-critical; this deserves prompt review.

3. **[PR #54396 — prefer systemd scope for timeout check (open since 2026-06-28)](https://github.com/NousResearch/hermes-agent/pull/54396)** — Nearly 2 months old, touching gateway process management. Could be blocked on review capacity or design decisions.

4. **[PR #65784 — fail closed across Git and filesystem boundaries (open since 2026-07-16)](https://github.com/NousResearch/hermes-agent/pull/65784)** — A security-relevant disk-cleanup hardening PR, still unmerged after 5+ weeks.

5. **[PR #73006 — explicit Obsidian vault selection (open since 2026-07-28)](https://github.com/NousResearch/hermes-agent/pull/73006)** — A user-facing feature waiting 3+ weeks. The skills index issue may be blocking skills-related PRs.

6. **[Issue #76385 — Buzz gateway shows agent offline while connected (open since 2026-08-01)](https://github.com/NousResearch/hermes-agent/issues/76385)** — A transport-health vs. client-presence contract mismatch that affects user trust in the Buzz platform.

---

**Overall health assessment:** Hermes Agent is **very active and deliberately investing in architectural soundness and security** at the cost of rapid feature velocity. The volume of "Architecture" issues and the large-file decomposition completion show a maintainer team that values **long-term correctness over short-term features**. The main risk is **review/merge capacity** — many good PRs (auth, security, skills) are aging in the backlog. The community is engaged and contributing, but the **install/update reliability P1** and **Windows-specific bugs** remain the most visible user-facing weaknesses.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-22

## 1. Today's Overview

PicoClaw shows moderate activity today with 4 closed PRs and 1 new open issue, indicating steady consolidation rather than rapid development. The project has no new releases today; instead, the focus is on finalizing previously-pending pull requests that span tooling, documentation, protocol support, and skill management. All 4 PRs merged today were created weeks earlier (February–March 2026), suggesting a backlog-clearing cycle rather than fresh feature velocity. One new feature request regarding agent turn queueing (Issue #3342) opens a potentially significant design discussion. Overall, the project appears in a healthy maintenance-and-polish phase with community contributions landing steadily.

## 2. Releases

No new releases were published today. No changelog, breaking change, or migration notes to report.

## 3. Project Progress

All four merged/closed PRs today contribute to user-facing capability improvements:

- **[PR #647 — WebFetchTool text extraction with HTML entity decoding and structure preservation](https://github.com/sipeed/picoclaw/pull/647)** — An enhancement to the WebFetchTool that decodes HTML entities (`&amp;`, `&lt;`, etc.) and inserts newlines around block-level elements. This materially improves the quality of content that the agent ingests from web pages, which is a common failure point for tool-based agents.

- **[PR #1158 — Native Anthropic Messages API protocol support (fixes #269)](https://github.com/sipeed/picoclaw/pull/1158)** — Adds an `anthropic-messages` protocol prefix that uses the `/v1/messages` endpoint format directly. Resolves an interoperability gap for Anthropic-compatible proxy services that reject the current format.

- **[PR #714 — Skills CLI: install/reinstall commands, GitHub Trees API integration, subpath support](https://github.com/sipeed/picoclaw/pull/714)** — Refactors the skills command (into `skillsCmd`), adds `repo@branch` and optional subpath specifications, adds a `reinstall` subcommand with force-overwrite, and switches production installs to the GitHub Trees API for full-directory retrieval.

- **[PR #1182 — Repository guidance refactor: `AGENTS.md` made principle-based and lightweight](https://github.com/sipeed/picoclaw/pull/1182)** — A documentation revision that clarifies repository guidance as principle-first rather than a rigid checklist, updates the Go version reference to use `go.mod` as the source of truth, and adds related clarifications.

## 4. Community Hot Topics

No issues or PRs today have non-zero comments or reactions, so community engagement is currently quiet. The most notable item is the newly-filed **[Feature Request #3342 — Opt-in "after-turn" steering mode](https://github.com/sipeed/picoclaw/issues/3342)**, which proposes a non-interrupting message queue for busy sessions. Even without discussion yet, the request addresses a likely-frequent user friction point: meaning to give a follow-up instruction but accidentally aborting in-flight tool work. Expect this to gather traction and potentially influence steering-mode defaults in a future minor release.

## 5. Bugs & Stability

No new bugs, crashes, or regressions were reported today. The project had no open bug fixes today and no stability-related work merged. However, the merged **[Anthropic Messages protocol PR (#1158)](https://github.com/sipeed/picoclaw/pull/1158)** closes a compatibility gap (Issue #269) that functioned as a bug for users of Anthropic-native-only proxy endpoints. No outstanding severity-ranked bug items are present at this time.

## 6. Feature Requests & Roadmap Signals

One new feature request was filed today:

- **[Issue #3342 — Opt-in "after-turn" steering mode: queue busy-session messages instead of interrupting](https://github.com/sipeed/picoclaw/pull/3342)** — Proposes an alternative to the current mid-task-correction design. Users who send a second message while the agent is running would have their message queued until the current turn completes, instead of preempting remaining tool calls. The request explicitly frames this as opt-in, signaling that the maintainers value backward-compatibility of the current interrupt behavior.

Given the explicit "opt-in" framing and the general pattern of rapid community-driven enhancement in this project, this feature is a plausible candidate for a near-future release (e.g., 0.6 or 0.7), likely as a configurable steering mode. The merged protocol and skills improvements in today's PR set suggest the maintainers prioritize integration flexibility; this feature fits that theme well.

## 7. User Feedback Summary

The single new issue today reflects a real user pain point: the inability to send a follow-up message without truncating the current turn's tool chain. The author explicitly describes the current behavior ("Skipped due to queued user message") and requests a gentler alternative. No negative feedback, complaints, or bug reports surfaced today. The merged PRs indicate satisfaction with WebFetchTool output quality concerns, Anthropic endpoint incompatibility (reported originally as Issue #269), and skill install plumbing. Overall sentiment appears constructive, with users investing in proposals rather than filing frustration-based reports.

## 8. Backlog Watch

No issues or PRs today are stale-and-unanswered, but status of the following items should be watched by maintainers due to long open states:

- **[Issue #269 (referenced by merged PR #1158)](https://github.com/sipeed/picoclaw/pull/1158)** — The Anthropic-native compatibility gap has now been resolved as of today, so this can be closed/verified.

- **[PR #647 (WebFetchTool enhancement)](https://github.com/sipeed/picoclaw/pull/647)** — Created 2026-02-22 and only merged six months later; worth reviewing why this merged so slowly to inform contribution-thead guidance.

- **[PR #714 (skills CLI)](https://github.com/sipeed/picoclaw/pull/714)** — Created 2026-02-24, similarly lagged ~6 months to merge. The delay pattern across multiple PRs suggests the maintainer review queue is the bottleneck; if this persists, consider posting a contributor guide note about review expectations.

No other open issues or PRs remain without maintainer attention today.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-22

## 1. Today's Overview

NanoClaw is in a period of **high-velocity, multi-track feature development**, with 24 PRs updated in the last 24 hours — the strongest sustained contributor activity seen in recent weeks. The project is currently executing on **three major workstreams simultaneously**: (1) a templates-from-chat feature spanning core tooling and the Slack channel (PRs #3396, #3428), (2) a significant Telegram multi-instance/setup overhaul (PRs #3436, #3438, #3435, #3431), and (3) a broad stabilization push on the Dial channel and registry-backed skills (PRs #3432, #3424, #3403). A **notable shift** is visible in team composition: contributor `amit-shafnir` has become the most active committer, driving the Telegram and templates work, while `zvi-fried` is leading the stability/CI effort. **11 PRs were merged or closed** today, indicating the team is converting active development into shipped code at a healthy rate. However, `glifocat`'s issue #3426 reveals a **user-facing documentation/bridge inconsistency** that could erode agent trust if not addressed quickly.

## 2. Releases

**No new releases published in the last 24 hours.** The most recent version remains the current stable release. The team appears to be accumulating changes — including the container bump to Claude Code 2.1.238 (PR #3439) and several adapter fixes — which may be bundled into the next release candidate.

## 3. Project Progress

**Merged/Closed PRs today (11 total):**

- **`ci` pipeline hardening (3 PRs):** `zvi-fried` closed #3424 (test registry-backed skills against pinned registry snapshots), #3430 (restore the required `ci` check that was broken by the Node 22/24 matrix), and #3402 (accept provider file events from branch-backed providers). These PRs address **CI reliability and test coverage for registry-backed skills**.
- **Matrix adapter fix (#3403):** `zvi-fried` merged a refresh-safe ESM patch for the Matrix adapter, fixing extensionless imports that failed under Node 22. This is part of the `[main]`/`[channels]` branch-composition stabilization work.
- **WhatsApp Cloud compatibility (#3401):** Fixed a dependency on a registry helper available only on the `channels` branch; the skill now exports/typifies the registration so it composes correctly with main.
- **Driver exec contract (#3429):** `gavrielc` merged a **design-level PR** ratifying `SessionExecSpec { bin, argsTty, argsPlain }` — drivers now *describe* their exec invocation rather than *performing* it. This is a foundational API change for interactive terminal attach tooling.
- **Mattermost integration (#3202):** The long-running Mattermost channel PR (originally opened 2026-08-08) was closed, adding Mattermost as a Chat SDK channel via the community `chat-adapter-mattermost` package.
- **Dial skill fixes (#3433):** `zvi-fried` converted `/add-dial-number` to use nc directives instead of prose shell blocks, making it registry-discoverable.
- **Container bump (#3439):** Bumped Claude Code CLI to 2.1.238 and agent SDK to 0.3.238.
- **Dial channel picker (#3050):** The large Dial-in-setup feature (opened 2026-07-14) was closed after ~5 weeks of review.

## 4. Community Hot Topics

The most active items today, by engagement and cross-PR linkage:

- **Telegram multi-instance feature cluster** — PRs #3436 (named bot instances via `TELEGRAM_INSTANCES`), #3438 (setup wizard "add another bot" path), #3435 (adapter instance through pairing/CLI), #3431 (pairing card digit fix), #3437 (docs). These five PRs from `amit-shafnir` form a **cohesive feature family** that will significantly change Telegram setup UX. The cluster is the single largest area of active work. [PR #3436](https://github.com/nanocoai/nanoclaw/pull/3436) · [PR #3438](https://github.com/nanocoai/nanoclaw/pull/3438)
- **The `send_card` buttons bug** (#3426) — `glifocat` reports that the docs promise callback buttons the bridge silently drops when they lack a `url`, and agents then mis-diagnose the failure as platform incompatibility. This has **zero comments** — suggesting the maintainers haven't yet triaged it — which is concerning given its potential to confuse agent behavior at runtime. [Issue #3426](https://github.com/nanocoai/nanoclaw/issues/3426)

Analyzing the cluster: **Telegram multi-instance support** is the strongest signal. The team members are proactively adding "instance" as a first-class concept across pairing, CLI welcome, and wizard flows — this is the kind of user-requested expansion that indicates NanoClaw's Telegram support has outgrown single-bot deployment.

## 5. Bugs & Stability

Ranked by severity:

- **[Medium] `send_card` drops non-`url` actions (Issue #3426):** Documentation promises callback buttons; the bridge silently drops action entries without `url`, and agents blame the platform. The lack of a log warning or diagnostic makes this **silent data loss that misleads the agent's world model**. No fix PR yet. [Issue #3426](https://github.com/nanocoai/nanoclaw/issues/3426)
- **[Low] Telegram pairing card shows 6 digits (PR #3431):** Cosmetic fix in progress; the card apparently displays a 6-digit expectation when the actual code is shorter (or vice versa). Fix PR is open. [PR #3431](https://github.com/nanocoai/nanoclaw/pull/3431)
- **[Low] Polling adapters don't open webhook server (PR #3434):** `amit-shafnir` fixed a Chat SDK issue where polling-based adapters failed to open the webhook server — likely an edge case for hybrid adapters. [PR #3434](https://github.com/nanocoai/nanoclaw/pull/3434)
- **[Resolved] Matrix ESM import failure under Node 22 (#3403):** Merged fix using refresh-safe pnpm patches.
- **[Resolved] CI `ci` check permanently pending (#3430):** The Node 22/24 matrix broke the exact-name required check; fixed and merged.

## 6. Feature Requests & Roadmap Signals

The strongest roadmap signals come from the actual PRs in flight:

- **Templates-from-chat (PR #3396, #3428):** The `create_agent` tool gains an optional `template` ref; `ncl templates list` verb supports local and registry listings. This will likely ship in the **next minor release**, given the core-team labeling and branch strategy (`#3428` supersedes a prematurely-merged PR — a sign of careful sequencing).
- **Telegram multi-instance (PR #3436):** `TELEGRAM_INSTANCES` env + named bot instances + instance-bound pairing. This is a **quality-of-life feature for operators running multiple Telegram bots**, and the breadth of the change (setup wizard, CLI welcome, pairing, docs, bug fixes) suggests it's a coordinated initiative that is near-complete.
- **Driver `SessionExecSpec` contract (PR #3429):** Ratified today. This is **foundational for interactive terminal attach** and likely a prerequisite for IDE/terminal tooling integrations coming in a future release.
- **Mattermost channel (#3202):** Merged — adds another chat platform, expanding NanoClaw's "polyglot chat" story.

**Prediction:** The next release will bundle the templates-from-chat feature, Telegram multi-instance support, and the accumulated adapter/CI fixes. The Mattermost and Matrix work suggests a broader Channel SDK expansion effort is underway.

## 7. User Feedback Summary

- **Agent behavior misdirection (Issue #3426):** The bridge dropping `send_card` buttons without any diagnostic causes agents to **incorrectly attribute failures to the platform**. The agent even *quotes the fallback text* ("for platforms without card support") when the real issue is the bridge's own filtering. This is a **trust-corrosion bug** — the user sees the agent confidently say the wrong thing. The reporter (`glifocat`) is clearly a developer closely watching agent reasoning traces, and the implicit ask is: *bridge behavior should be surfaced to the agent* (e.g., as a warning token) rather than silently swallowed.
- **No other explicit user feedback** (comments or reactions) was visible in today's data. The community's needs surface primarily through the features being actively built: multi-bot Telegram, templates, and registry-backed channel skills.

## 8. Backlog Watch

- **[Issue #3426 — `send_card` buttons dropped, 0 comments, 1 day old]:** The silence on this issue is the concerning part. Given it involves **misleading agent behavior with user-visible consequences**, it deserves a maintainer triage comment (even if the fix is deferred). If it remains untouched for 3-5 days, consider flagging it. [Issue #3426](https://github.com/nanocoai/nanoclaw/issues/3426)
- **[PR #3287 — agent-group suffix stripping, open since 2026-08-17, updated today]:** `wakqasahmed`'s fix for inbound platform message IDs is now **6 days old** with no closure. It addresses a real bug (wrong message ID lookup in `messages-out.ts`) and was updated today — a maintainer should decide merge or request changes. [PR #3287](https://github.com/nanocoai/nanoclaw/pull/3287)
- **[PR #3050 — Dial in channel picker, closed after 5 weeks]:** Now closed, but it spent over a month in review. If that review velocity is a pattern, the templates/Telegram work (which is larger in scope) may face similar delays unless the team actively prioritizes review bandwidth.

---

**Overall health assessment:** NanoClaw is in a **healthy, high-output development phase** with strong contributor diversity (5 distinct committers today), a clear feature roadmap, and a growing channel ecosystem. The primary risks are (1) **user-facing agent behavior bugs** like #3426 that don't show up in CI and (2) **review latency** for non-core-team PRs such as #3287. The team's proactive branch-composition CI work (`[main]`/`[channels]` tag strategy) is a sign of maturing engineering discipline.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-22

## 1. Today's Overview

NullClaw is in a **quiet but constructive** phase today. No new releases were published, and no issues were updated or opened in the last 24 hours — indicating stable core functionality and a lack of active user-reported problems. Activity is centered on a single open Pull Request (#990) proposing the addition of Eden AI as an OpenAI-compatible gateway provider, which continues a deliberate pattern of expanding provider integrations without adding bespoke implementations. The project's pulse is low but purposeful, with maintainers seemingly prioritizing review of high-quality, low-risk integration PRs over rapid feature churn. Overall project health appears solid: zero open bug reports and a steady flow of incremental, well-scoped contributions.

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent release history shows no version bumps this week. Users on the latest stable release should not expect any changes or migration requirements at this time.

---

## 3. Project Progress

**Merged/Closed PRs today: 0** — No PRs were merged or closed in the last 24 hours. 

However, one PR remains **open and under review**:

- **[#990: feat(providers): add Eden AI as an OpenAI-compatible gateway](https://github.com/nullclaw/nullclaw/pull/990)** — Authored by MVS-source, this PR adds Eden AI as a gateway provider following the established pattern from #922 (NEAR AI Cloud and Atlas Cloud). It uses the existing `OpenAiCompatibleProvider` class rather than introducing a new implementation. **Why it matters:** Eden AI aggregates multiple upstream LLM vendors behind a single API key, and is EU-based — broadening NullClaw's multi-provider routing options for European users concerned with data residency.

---

## 4. Community Hot Topics

There is **one active discussion** worth noting today:

- **[PR #990: Add Eden AI as an OpenAI-compatible gateway](https://github.com/nullclaw/nullclaw/pull/990)**  
  - **Comments:** Not explicitly reported (likely low) | **Reactions:** 0  
  - **Underlying need:** The PR signals a growing community desire for **aggregated provider gateways** — single-key access to many vendors — rather than one-off integrations per model. The author explicitly references matching the shape of #922, indicating that NullClaw's provider abstraction is mature enough that contributors can add new gateways in a copy-paste fashion. The EU-based routing angle also suggests interest in **data sovereignty and compliance** as a selection criterion for AI infrastructure.

**Analysis:** No flame wars, no controversial debates — the community is collaborative and focused on expanding provider coverage efficiently.

---

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported in the last 24 hours.** The issue tracker shows a clean slate (0 open/active, 0 closed in this window). 

**Stability verdict:** This is a positive signal. The project is not receiving a flood of defect reports, which suggests the current release is performing well for users. The only code change in flight (#990) is additive and reuses battle-tested components (`OpenAiCompatibleProvider`), so regression risk is minimal.

---

## 6. Feature Requests & Roadmap Signals

While no formal feature requests were filed as issues today, the open PR provides strong roadmap signals:

| Signal | Source | Implication |
|--------|--------|-------------|
| **Aggregated gateway providers** | PR #990 (Eden AI) + reference to #922 (NEAR/Atlas Cloud) | NullClaw is actively curating a **multi-vendor gateway ecosystem**. Users increasingly expect "one key to rule them all." |
| **EU data residency** | PR #990 explicitly notes Eden AI is EU-based | Compliance and jurisdictional routing are becoming decision factors for provider selection. Expect more EU-hosted gateway proposals. |
| **Template-driven contributions** | Author reused existing provider shape without new code | The architecture is now contributor-friendly; this lowers the barrier for new gateway additions. **Prediction:** The next 2–3 versions may see 2–4 new gateway providers added via this pattern (e.g., other EU-based aggregators). |

**Likely next version inclusion:** PR #990 is a low-risk, high-value addition. If reviewed promptly, it could land in the next minor or patch release.

---

## 7. User Feedback Summary

With zero new issues and only one PR, direct user feedback today is **sparse but implicitly positive**:

- **Pain points:** None reported. No crashes, no configuration complaints, no performance grievances surfaced in the last 24 hours.
- **Use cases:** The Eden AI PR highlights a real user use case — **a developer building with multiple LLM vendors who wants to simplify key management and centralize billing** via a single gateway. The EU angle suggests a user with **compliance requirements** (GDPR, data residency) seeking a provider that meets those needs without sacrificing vendor choice.
- **Satisfaction level:** Inference from behavior — the community is contributing code (PR #990) rather than filing bug reports. This reflects confidence in the codebase and a desire to extend it. The lack of reactions on the PR (👍: 0) suggests it's still early in its review lifecycle, not a rejection.

---

## 8. Backlog Watch

**No issues** are currently languishing without maintainer attention (0 total issues). 

**One PR should be tracked for review progression:**

- **[PR #990 (Eden AI gateway)](https://github.com/nullclaw/nullclaw/pull/990)** — Created 2026-08-21, now ~24h old with no merge. While the project appears healthy, this PR is the **only active contribution**. If it sits untouched for 3–5 days, it risks contributor discouragement. **Recommendation:** Maintainers should prioritize a review pass on this PR within the next 48 hours to keep contribution momentum alive, given the pattern established by #922.

---

## Summary Verdict

| Metric | Status |
|--------|--------|
| Project Health | 🟢 **Stable** — no bugs, no release churn, focused contribution |
| Momentum | 🟡 **Moderate** — one open PR, no merges today |
| Community Engagement | 🟡 **Quiet but constructive** — contributor-driven, not issue-driven |
| Risk Level | 🟢 **Low** — additive changes only, reusing proven architecture |

**Bottom line:** NullClaw is in a healthy maintenance-and-incremental-growth phase. The provider gateway strategy is paying off in contributor accessibility. The next 48 hours of PR #990 review are the key indicator of ongoing momentum.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-22

## 1. Today's Overview

IronClaw is in a high-intensity CI infrastructure overhaul phase, with the core team executing a four-track expedite program (T1–T4) to unify and harden the project's build, test, and gate pipeline. The 24-hour window shows sustained activity: 37 PRs updated (16 merged/closed, 21 open) and 13 issues touched (9 open, 4 closed), with zero new releases. While no version shipped, the merged work contains several forward-ports to release branches and the beginning of a significant sandbox credential-mediation feature. A notable highlight is the project's first external contributor PR of the window (#7811), suggesting the community ramp from the AGENTS.md audit is beginning to pay off.

## 2. Releases

No new releases were published in this window. The GitHub Releases page in the provided data shows no tag entries for this period. The most recent release remains the 1.7 series, with patch management ongoing on the `release/2026-08-17` branch.

## 3. Project Progress

Sixteen PRs were merged or closed in the last 24 hours. The most significant items, by cluster:

- **CI Expedite Track (T2/T4 partial):** The canonical preflight gate list (`scripts/preflight-gates.sh`) is now the single source of truth for deterministic checks, with worktree-safe hooks installed via `core.hooksPath` [#7809](https://github.com/nearai/ironclaw/issues/7809). This closes the first half of Issue #7801 and provides a self-printing REPRO mechanism for future failure diagnosis.
- **Sandbox credential mediation (closed sequence #7805, #7806, #7807):** Three PRs landed that build toward the per-user managed egress model for GitHub CLI credentials. The first two establish a direct-executable sandbox path with invocation-scoped, one-shot credential staging; the final PR completes the chain by routing `gh` through the existing `builtin.shell` authorization flow [#7807](https://github.com/nearai/ironclaw/issues/7807). The re-opened #7810 indicates the maintainers chose to amplify this work rather than close it out.
- **Cross-variant bugfixes:** `IRONCLAW_REBORN_WORKSPACE_ROOT` was forward-ported to both `main` and `release/2026-08-17` after landing only on the 1.3 branch [#7804](https://github.com/nearai/ironclaw/issues/7804). Clippy 1.98 lint breakages on the release branch were also backported [#7805](https://github.com/nearai/ironclaw/issues/7805).
- **Agent guidance layer:** A repo-wide audit pruned 21.5k lines and consolidated the `tests/` directory onto the AGENTS.md convention, executed with 13 parallel auditors [#7797](https://github.com/nearai/ironclaw/issues/7797).
- **Notable:** The LLM timeout policy bug was declared closed [#7783](https://github.com/nearai/ironclaw/issues/7783), presumably with the non-streaming client issue resolved via the retry budget changes described in the issue body.

## 4. Community Hot Topics

The most active items this window are all maintainer-driven, but they signal deep architectural work with broad implications:

- **[#7801](https://github.com/nearai/ironclaw/issues/7801) — CI expedite T4 (canonical preflight)** (3 comments): The plan document for unifying the CI gate list. Underlying need: the current sprawl of per-workflow fast checks and queue gates has proven fragile; the team wants a single file that can be read by both humans and CI. This is the highest-leverage item in the window because it removes an entire class of "works locally, fails in CI" bugs.

- **[#7799](https://github.com/nearai/ironclaw/issues/7799) — CI expedite T2 (nextest pipeline)** (3 comments): Replacing sequential per-binary test loops with `cargo-nextest`. The underlying need is twofold: parallel test execution to combat PR/queue latency, and unified JUnit reporting so a single CI lap reports every failure without a detective hunt.

- **[#7798](https://github.com/nearai/ironclaw/issues/7798) — CI expedite T1 (setup-rust composite)** (2 comments): Consolidating 43 scattered `dtolnay/rust-toolchain` invocations into one composite action. This is the foundation for T2/T3; without the toolchain pin and mold linker in one place, the other tracks can't guarantee they're testing the same compiler.

- **[#7664](https://github.com/nearai/ironclaw/issues/7664) — Pluggable memory over MCP** (2 comments): The tracking issue for external memory via MCP, with Mnesis Core lined up as the first consumer. This remains the project's most visible external integration point and directly complements the sandbox credential work — both are about controlled, auditable third-party extension.

Community participation from non-core contributors remains thin but present: the Xquik MCP bundle PR (#7811) from a "new" contributor is the only externally-authored PR in the window.

## 5. Bugs & Stability

Three issues were opened as bugs; all are active and none have fix PRs yet:

- **[#7808](https://github.com/nearai/ironclaw/issues/7808) — Memory write path: redaction + taint metadata required before any external provider binds** (high severity, root-caused): The write path egresses verbatim conversation content, and only the host can fix this at write time. This is a prerequisite blocker for #7664 — no external memory provider can bind until this is fixed. The maintainer (serrrfirat) explicitly framed it as a security/trust boundary, not a feature gap.

- **[#7783](https://github.com/nearai/ironclaw/issues/7783) — LLM timeout policy (CLOSED today, medium severity)**: Structured-output finalization runs on a non-streaming client, so a stalled provider is invisible until a 60s wall-clock cap fires, and the 75s finalization deadline kills the retry. The issue is closed, but no patch PR was observed in the merged list — this should be verified as truly resolved vs. closed-for-triage.

- **[#7715](https://github.com/nearai/ironclaw/issues/7715) — Telegram connection flow lacks consent/selection between bot and personal account (CLOSED)**: Users connecting via the Railway QA instance could not tell whether they were linking a Telegram bot or their personal account. Fixed in this window via [#7803](https://github.com/nearai/ironclaw/issues/7803), which stops projecting workspace-bot pairing as a connected personal account and keeps bot credentials independent of device-link state. This is a good outcome: closed within 5 days of reporting, with a fix that addresses both UX confusion and a credential-model mismatch.

No new crashes, panics, or data-loss bugs were reported. The two infrastructure failures (clippy on release branch, workspace-root forward-port) were both fixed in the same window.

## 6. Feature Requests & Roadmap Signals

Three forward-looking features are in flight, none yet released:

- **Pluggable memory via MCP (#7664)**: The design is firm (provider crate, Mnesis as first consumer), but Issue #7808 must land first. Once redaction/taint is in place, this is the strongest candidate for the next minor release. The pattern it establishes — external systems bindable by configuration — is the project's clearest signal that IronClaw is deliberately becoming a hosting layer for third-party intelligence infrastructure.

- **GitHub CLI credential mediation (#7810, open XL PR)**: This re-opened PR supersedes the three today that closed. The feature gates outbound `gh` commands behind authorization/approval and stages one-shot credentials. This is a sandbox security-hardening feature that will land on `main` soon; the question is whether it rides into the next release or ships standalone.

- **WebUI design system (Epic #7038)**: The long-running Storybook + design-system catalog effort has two open PRs (#7257 proposal, #7750 integration) and a new shared-primitives refactor landing today (#7794). The addition of `PageScroll`/`PageStack`/`Skeleton` primitives to five routes suggests the design system is being consumed incrementally rather than in one large cutover. Expect this to continue through phases 2–3 per the superseding Epic #7781.

The notification-inbox work (Epic #7687) made decisive progress: Issues #7690 and #7689 closed, and two XL PRs (#7699 closed, #7700 open) implement actionable gates and authoritative run outcomes. The next version will likely include a durable inbox with server-backed unread state.

## 7. User Feedback Summary

The data contains little direct user feedback this window, except:

- **Telegram UX confusion (from QA instance)**: The consent/selection bug (#7715) shows that real users struggle with the multi-credential Telegram flow. The fix now clearly separates "workspace bot" from "personal account" and gates personal-account tools at dispatch time — an improvement that should reduce both confusion and accidental over-privileging.

- **LLM timeout behavior (#7783)**: Reported by a core maintainer, but the failure mode (LLM provider stalls killing runs) is a generic user pain point. The fix direction — moving finalization onto a streaming client and fitting retries into the deadline — is one users will feel as fewer "dead run" incidents.

- **OOBE suggestions gating (#7802, open PR)**: The OOBE suggestion surface is being made always-on, removing the `IRONCLAW_OOBE_SUGGESTIONS` env var. This suggests internal testing revealed users were not discovering suggestions when gated; the simplification signal is that default-on is what the team wants for first-run experience.

Overall sentiment is neutral-to-positive; no complaints about breaking changes were filed, and the release-branch lint failures were caught and fixed within the day.

## 8. Backlog Watch

- **[#7456](https://github.com/nearai/ironclaw/issues/7456) — Durable storage profile-agnostic (open 13 days, XL, core contributor)**: This PR roots Reborn profiles directly at `IRONCLAW_REBORN_HOME` with typed security envelopes. It has not been updated in the last 24h and predates the entire CI-expedite push. The change is fundamental to multi-profile tenancy isolation; the longer it sits, the more dependent PRs will pile up behind it. Worth a refresh from henrypark133 or a designated reviewer.

- **[#7491](https://github.com/nearai/ironclaw/issues/7491) — omp core-tool contract (open 11 days, XL, medium risk)**: This slices 1–4 of the coding-tool consolidation — models get six bare tool names (`read`, `write`, `edit`, `glob`, `grep`, `bash`). This is a breaking-change PR at the model-facing surface, and it's been quiet since last week. Given the LLM-dependent nature of the project, this PR likely needs careful backward-compat review before merging; it is a candidate for the next "risk: medium" release cap.

- **[#7257](https://github.com/nearai/ironclaw/issues/7257) — Design system proposal (open 17 days, docs-only)**: The proposal has been static for two weeks while the integration PR #7750 advances. The proposal should be acknowledged and either merged as a baseline or closed in favor of the executing PRs.

- **No open issues from non-maintainers are waiting on responses**; the only new-contributor PR (#7811) is from the last 24h and has not been reviewed yet.

---

**Project health assessment:** Healthy and accelerating. The team is actively paying down CI debt (T1–T4), backporting fixes to release branches within hours, and closing user-facing bugs within a week. The main risk to watch: the number of large, open XL PRs (5) that are all moving toward `main` in a short window — merge conflicts between the sandbox, coding-tool, and durable-storage lines are likely over the next few days.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-22

## 1. Today's Overview

LobsterAI shipped a release bundle (`2026.8.21`) that merges 12 PRs into `main`, including the experimental DeepSeek Harness (DSH) runtime upgrade to `0.1.1-rc.1`, a privacy-conscious analytics refactor, and multiple library/artifact UX improvements around preview, sharing, and favorites. The 24-hour window shows high merge velocity (12 closed/merged PRs) with zero new releases announced, indicating the team is consolidating post-release rather than cutting a fresh tag. Two stale issues (both from April 1) were auto-closed, reflecting an ongoing backlog hygiene effort. One PR (#1550) remains open with a stale label, suggesting a long-dormant fix waiting for maintainer attention. Overall project health is strong: active development, clear release discipline, and a mix of feature work and quality-of-life fixes.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release was `2026.8.21` (merged via PR #2519), which include:

- **DSH runtime update** to `0.1.1-rc.1` (experimental).
- **Windows integration reliability improvements**.
- **Privacy-conscious analytics** for DSH enablement and workbench usage.

No breaking changes or migration notes were documented in the merge PR.

## 3. Project Progress

The following PRs were closed/merged in the last 24 hours. Notable advances:

- **[#2518] — refactor(dsh): move usage analytics from main to renderer** (`fisherdaddy`): Relocates DSH analytics event building from IPC handlers to a renderer-side service and wires it into `DshExperimentalSettings`. Also skips re-logging analytics beacon requests. Improves architecture cleanliness and reduces main-process coupling.
- **[#2517] — fix(library): improve file sharing and favorites UX** (`liugang519`): Unicode-safe filename sanitization in share archives, legacy filename compatibility, instant favorite-state updates with failure rollback, deduplicated list refreshes, and unified quota-limit modal styling/focus/close behavior. Includes constants and automated tests.
- **[#2516] — feat: update dsh to 0.1.1-rc.1** (`fisherdaddy`): Dependency bump for the experimental DSH runtime.
- **[#2515] — feat(dsh): add usage analytics for enable toggle and workbench open** (`fisherdaddy`): Fire-and-forget analytics for DSH feature toggles and workbench open attempts (success/failure with error code), with documented event shapes in the design spec.
- **[#2514] — feat(library): optimize local artifact preview and operations** (`liugang519`): Resized preview modal with overflow constraints, removed delete-file/task entries from the artifact library, differentiated empty state vs. filter-no-results, one-click clear for search boxes, fixed quota modal placeholder substitution, and synced IPC/types/i18n/docs.
- **[#2513] — Feat/2026.8.17 library** (`liugang519`): Feature branch merge (likely aggregated library improvements).
- **[#1224] — fix(agent): i18n hardcoding, Escape key support, delete de-duplication** (`MaoQianTu`): Replaces hardcoded `'输入文件'` with `i18nService.t('coworkInputFileLabel')` (English: `Input file`), adds Escape-to-close for `AgentCreateModal`/`AgentSettingsPanel`, and guards against double-click delete. Closes #1223.
- **[#1220] — perf(cowork): eliminate N+1 queries in recentChats/conversationSearch** (`choyuenga`): Replaces per-session duplicate queries (2 per session) with batched lookups, improving list-load performance.
- **[#1219] — perf(cowork): eliminate invalid re-renders in session list/detail** (`choyuenga`): Adds `React.memo` to session items and consolidates 4 separate `useSelector` hooks in `CoworkSessionDetail`.
- **[#1218] — fix(定时任务): rebuild task list sorting** (`gongzhi-netease`): Fixes UUID-random-order issue; tasks now sort by `nextRunAtMs` with a sensible tiebreaker.
- **[#1215] — fix(im): always rebuild chat handler on setConfig** (`mingoLzm`): Ensures `setConfig` refreshes chat handlers even when platform-specific credentials (e.g., DingTalk/Telegram) are saved without a `settings` key, preventing stale `systemPrompt`/skill configs.

## 4. Community Hot Topics

Two closed issues received the most engagement (2 comments each):

- **[Issue #1223]** — *CoworkPromptInput hardcoded Chinese labels & Agent modal UX issues* (`MaoQianTu`): High-signal UX/i18n bug report covering three concrete problems: Chinese text leaking into English prompts, missing Escape-key close for Agent modals, and no double-click protection on delete. The issue was fully addressed by PR #1224, showing responsive maintainers.
  - [netease-youdao/LobsterAI Issue #1223](https://github.com/netease-youdao/LobsterAI/issues/1223)
- **[Issue #1217]** — *Random gateway restarts during use* (`blueb0ne`): Intermittent gateway restarts (3–5 times/day) on Windows 10 with version 2026.3.26, accompanied by logs. Closed as stale without a public fix, which may leave affected users without a resolution.
  - [netease-youdao/LobsterAI Issue #1217](https://github.com/netease-youdao/LobsterAI/issues/1217)

No open issues or PRs attracted new comments/reactions today.

## 5. Bugs & Stability

The following bugs were addressed today (all with fix PRs merged):

| Severity | Bug | Report/PR | Status |
|----------|-----|-----------|--------|
| **High** | Intermittent gateway restarts (3–5×/day) on Windows (Issue #1217) | [Issue #1217](https://github.com/netease-youdao/LobsterAI/issues/1217) | Closed as **stale** — no fix PR linked |
| **Medium** | Chinese label `'输入文件'` leaking into English AI prompts (i18n) | [Issue #1223](https://github.com/netease-youdao/LobsterAI/issues/1223) / [PR #1224](https://github.com/netease-youdao/LobsterAI/pull/1224) | ✅ Fixed |
| **Medium** | Stale chat handler after platform-specific credential saves (DingTalk/Telegram) — `systemPrompt`/skill changes not applied | [PR #1215](https://github.com/netease-youdao/LobsterAI/pull/1215) | ✅ Fixed |
| **Medium** | Task list ordering unpredictable due to UUID sorting; new tasks appear in random positions | [PR #1218](https://github.com/netease-youdao/LobsterAI/pull/1218) | ✅ Fixed |
| **Low–Medium** | Agent modals missing Escape-key close; delete action lacks double-click protection | [PR #1224](https://github.com/netease-youdao/LobsterAI/pull/1224) | ✅ Fixed |

**Note:** Issue #1217 (gateway restarts) was closed as stale with no linked fix. This may leave a real stability concern unresolved for Windows users. Maintainers should be aware.

## 6. Feature Requests & Roadmap Signals

Several signals indicate likely upcoming work:

- **DSH analytics & telemetry (active):** PRs #2515 and #2518 establish a pattern for privacy-conscious, fire-and-forget usage analytics. Expect more instrumentation in subsequent releases.
- **Library/artifact UX iteration (active):** PRs #2514/#2517 show a focused effort to polish the local artifact library (preview, sharing, favorites, empty states). Likely to continue with more edge-case handling.
- **i18n compliance (emerging):** PR #1224 explicitly references `AGENTS.md` compliance around hardcoded strings. Expect more audit-driven i18n fixes across the codebase.
- **Performance hardening (community-driven):** PRs #1219/#1220 address rendering and query inefficiencies in cowork sessions — likely to be followed by similar optimizations elsewhere (e.g., library lists, IM handlers).
- **Scheduled task delivery modes (dormant):** PR #1550 fixes the "no notification" delivery mode for session-created tasks. Stale for months — may be revived if the issue resurfaces in user reports.

## 7. User Feedback Summary

- **i18n pain point confirmed:** English users reported Chinese text (`'输入文件'`) embedded in AI prompts — a visible quality issue that was promptly fixed.
- **UX friction on modals:** Agent create/settings modals lacked Escape-key close and allowed accidental double-deletes; users implicitly expect standard modal behavior.
- **Task list usability:** Newly created scheduled tasks appeared in unpredictable positions, forcing users to visually scan the full list — addressed by sorting logic rewrite.
- **Stability concern (unresolved):** Windows users may still experience intermittent gateway restarts (Issue #1217); the stale closure without a fix PR means this complaint is still live in the wild.

## 8. Backlog Watch

The following item has been open for an extended period and may need maintainer attention:

- **[PR #1550] — fix(scheduledTask): omit channel/to fields when delivery mode is "none"** (`gongzhi-netease`): Open since April 7, 2026, stale-labeled; still open. Fixes a real runtime validation error ("Channel is required when multiple channels are configured") for session-created tasks with "no notification" mode. This is a user-visible bug in the scheduled task feature.
  - [netease-youdao/LobsterAI PR #1550](https://github.com/netease-youdao/LobsterAI/pull/1550)

---

*Data collected: 2026-08-22, sourced from LobsterAI GitHub activity in the last 24 hours.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for 2026-08-22.

---

# Moltis Project Digest — 2026-08-22

## 1. Today's Overview
The project is in a high-velocity state with a strong focus on bug fixing and platform hardening. Over the past 24 hours, 8 PRs were updated (7 open, 1 merged), and only 2 new issues were filed, both of which are bugs—suggesting that the existing feature set is expanding but stability is the current bottleneck. The maintainers are actively addressing integration issues across messaging channels (WhatsApp, Slack) and background tasks (cron/heartbeat). While there were no new releases today, the volume of update activity indicates a potential imminent release cycle. The community contribution is healthy, with several external contributors (e.g., `affanshahid`, `Lstarsky0`, `PeterDaveHello`) involved.

## 2. Releases
**None.**
There were no new releases published in the last 24 hours. This is notable given the number of merged and pending fixes, suggesting the maintainers are bundling changes for a future version.

## 3. Project Progress
**Merged/Closed PRs (1):**
- **[#1220 [CLOSED] fix(whatsapp): render Markdown in outbound messages](https://github.com/moltis-org/moltis/pull/1220)** by `rubenssoto`: This critical fix converts Markdown generated by the model into WhatsApp-native markup (for text and captions) just before delivery. It preserves the original Markdown in session history and the web UI, preventing "garbage" formatting in the final message.

**Active Fixes in Progress (Highlights):**
- **WhatsApp File Persistence:** [#1228](https://github.com/moltis-org/moltis/pull/1228) is working to download inbound files (up to 20MB) and persist them, ensuring local tools receive a stable `local_path` instead of just metadata.
- **Browser Stealth:** [#1227](https://github.com/moltis-org/moltis/pull/1227) enables the "Obscura" stealth mode by default to avoid detection, with a new config flag `tools.browser.obscura_stealth` for operators to disable it.
- **Cron Delivery Routing:** [#1226](https://github.com/moltis-org/moltis/pull/1226) adds a routing shortcut to ensure scheduled task outputs are delivered back to the originating chat/thread, addressing a major usability gap.
- **Windows Support:** The long-pending [#468](https://github.com/moltis-org/moltis/pull/468) was updated, fixing shell hooks on Windows by using `cmd.exe /C` instead of `sh -c`.

## 4. Community Hot Topics
While no issues have heavy comment threads yet, the most actionable items are the bug reports filed today:
- **[Issue #1223: heartbeat active_hours has no effect on a default config](https://github.com/moltis-org/moltis/issues/1223)** by `Lstarsky0`: This is a well-documented bug report highlighting that the `active_hours` setting is effectively dead code. The author provides technical detail, noting that the `is_within_active_hours` function parses the `end` time before the special-case for `"24:00"` is applied.
- **[Issue #1224: Tools stop working in shared Slack channels](https://github.com/moltis-org/moltis/issues/1224)** by `affanshahid`: Reports a functional regression where tools fail in shared Slack channels, which is a critical integration use-case for team collaboration.

**Analysis:** The interest is focused on reliability and integration. Users are testing edge cases (shared channels, default configs) and finding that the "happy path" code does not always handle them.

## 5. Bugs & Stability
Ranked by severity:

1.  **High: Tools stop working in shared Slack channels ([#1224](https://github.com/moltis-org/moltis/issues/1224))**
    - **Impact:** Blocks core functionality in a multi-user environment.
    - **Status:** No fix PR linked yet.

2.  **High: Heartbeat `active_hours` has no effect ([#1223](https://github.com/moltis-org/moltis/issues/1223))**
    - **Impact:** The feature is non-functional by default, meaning agents run when they shouldn't or vice-versa.
    - **Status:** **Fix PR exists:** [#1208](https://github.com/moltis-org/moltis/pull/1208) is open and closes this issue, but it has been pending since August 17th. This is a priority to merge.

3.  **Medium: Markdown rendering in WhatsApp (Fixed)**
    - **Impact:** Poor user experience for outbound content.
    - **Status:** Resolved via PR [#1220](https://github.com/moltis-org/moltis/pull/1220).

4.  **Medium: Local Tools missing WhatsApp file paths ([#1228](https://github.com/moltis-org/moltis/pull/1228))**
    - **Impact:** Limits the utility of local tools when processing user-provided files.
    - **Status:** PR Open.

## 6. Feature Requests & Roadmap Signals
There are no explicit new feature requests in the current issues; the focus is purely on bug fixes. However, the current PRs signal the roadmap direction:
- **Integration Hardening:** Focus on WhatsApp (Markdown, files) and Slack (permissions) suggests the team is prioritizing messaging channel reliability.
- **Security/Compliance:** PR [#1227](https://github.com/moltis-org/moltis/pull/1227) (Stealth mode) and PR [#1222](https://github.com/moltis-org/moltis/pull/1222) (validating sandbox image requests to restrict to admins) indicate a push toward enterprise security and anti-detection capabilities.
- **Developer Experience:** PR [#1225](https://github.com/moltis-org/moltis/pull/1225) improving the zh-TW locale shows a commitment to internationalization (i18n) and global usability.

## 7. User Feedback Summary
- **Pain Point (Cron/Heartbeat):** Users expect the `active_hours` setting to work out-of-the-box. The fact that it requires a special config value (`end: "24:00"`) to function is a logic flaw that undermines user trust in the scheduler ([#1223](https://github.com/moltis-org/moltis/issues/1223)).
- **Pain Point (WhatsApp):** Users are hitting formatting and file-handling issues, indicating that while the WhatsApp connector is functional, the polish is lacking (Markdown rendering, file persistence).
- **Pain Point (Slack):** Shared channel support is broken, which is a critical feature for team deployments. The user requested "full session context" in debugging, indicating a desire for better logging.
- **Satisfaction:** The community is engaged; external contributors are submitting high-quality PRs (e.g., `rubenssoto` and `Lstarsky0`), suggesting the contribution guidelines and codebase structure are welcoming.

## 8. Backlog Watch
- **[PR #468: fix(plugins): use cmd.exe on Windows for shell hooks](https://github.com/moltis-org/moltis/pull/468)**
  - **Age:** Created March 23, 2026 (5 months ago).
  - **Status:** Updated today but not merged. This is a critical fix for Windows parity. The delay suggests maintainers may be hesitant to merge due to testing overhead or cross-platform CI issues. This needs a decision (merge or close) to avoid stalling community contributions.

- **[Issue #1205 / PR #1208: Heartbeat fix](https://github.com/moltis-org/moltis/pull/1208)**
  - **Age:** PR opened August 17, 2026.
  - **Status:** Still pending review. Given the severity of the bug, this PR should be prioritized over new feature development to unblock users relying on active hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-22

## 1. Today's Overview

CoPaw (QwenPaw) shows a healthy, sustained development cadence with 34 issues and 36 PRs updated in the last 24 hours, split roughly evenly between open and closed/merged items. Activity is concentrated around the v2.1.1-beta release cycle, with several critical regression fixes already landed or in review — notably a pydantic ValidationError on `/compact` (Issue #7206), a Windows coverage pipeline fix (PR #7205), and a console e2e test repair batch (PR #7209). No new releases were published today, but a version-bump PR (v2.1.1b2) was merged, indicating an imminent patch release. Feature development remains strong in Creator (image/video providers), Hub (self-hosted multi-user control plane), and session-scoped tooling, alongside a significant number of user experience and quality-of-life fixes.

## 2. Releases

No new releases were published in the last 24 hours. However, PR #7200 (chore: bump version to v2.1.1b2) was merged, suggesting an upcoming beta patch release. Users on v2.1.1-beta.1 should watch for this update to address the known `/compact` regression documented in Issue #7206.

## 3. Project Progress

The following PRs were merged or closed today, representing concrete progress:

- **PR #7205** (test/coverage): Fixed a significant CI blind spot — Windows integration coverage had been reading 0 executed lines every night since late June. Adds a fail-closed guard to prevent silent empty collections in the future.
- **PR #7200** (chore): Version bump to v2.1.1b2, setting up the next beta release.
- **PR #7176** (perf/console): Improved long-chat-session responsiveness by eliminating repeated synchronous Markdown re-parsing during streaming and reducing WorkBox overhead.
- **PR #7112** (feat/hub): Self-hosted multi-user QwenPaw Hub merged — introduced an opt-in control plane (`qwenpaw hub --config ./qwenpaw-hub.yaml`) that runs isolated QwenPaw instances for local accounts without changing the existing `qwenpaw app` workflow.
- **PR #7209** (fix/e2e): Repaired remaining e2e cases broken by the recent console redesign (workspace unification, marketplace unification, session user-groups, virtualized sidebar, redesigned memory card).

Additionally, several long-running test-coverage feature issues were closed today (#5580, #5437, #5433, #5419, #5007, #5006, #5005, #5004), confirming the completion of the multi-sprint frontend and backend unit-test coverage plan.

## 4. Community Hot Topics

The most active discussion threads this week revolve around stability and configuration pain points:

- **[Issue #6524 — MCP backend restart requires manual reconnection](https://github.com/agentscope-ai/QwenPaw/issues/6524) — 6 comments.** High-interest bug: when a remote MCP server restarts, QwenPaw reuses a stale `mcp-session-id` over `streamable_http`, so tool discovery fails until the user manually runs `list mcp`. Underlying need: robust session lifecycle handling and automatic reconnection.

- **[Issue #6780 — Idle process deadlock (self-freeze) in v2.0.1](https://github.com/agentscope-ai/QwenPaw/issues/6780) — 4 comments.** Users report the app freezes after tens of minutes of inactivity, requiring a manual process kill. Closed, but the underlying reliability concern around idle resource management persists.

- **[Issue #7016 — Tool call 404 on streaming sessions](https://github.com/agentscope-ai/QwenPaw/issues/7016) — 3 comments.** A backend `/api/tool-calls/{id}/offload` endpoint returns 404 ("Tool call not found") during streaming, breaking tool execution.

- **[Issue #7156 — Embedding health check timeout not configurable](https://github.com/agentscope-ai/QwenPaw/issues/7156) — 3 comments.** Ollama embedding health check fails with a hardcoded 5s timeout even when the backend is warm (actual elapsed 10.4s), forcing session fallback to BM25-only retrieval.

- **[Issue #7206 — `/compact` regression in v2.1.1-beta.1](https://github.com/agentscope-ai/QwenPaw/issues/7206) — 2 comments.** Manual `/compact` fails with pydantic ValidationError when `compact_threshold_ratio == 0.9`. A confirmed regression from v2.1.0.

## 5. Bugs & Stability

Ranked by severity — critical regressions first:

1. **Critical — Compact failure in v2.1.1-beta.1** ([Issue #7206](https://github.com/agentscope-ai/QwenPaw/issues/7206)). Manual `/compact` fails with Pydantic ValidationError when `compact_threshold_ratio == 0.9`. Confirmed regression on v2.1.0. No fix PR identified yet — high priority.

2. **High — Tool call render tool schema not injected despite enabled config** ([Issue #7210](https://github.com/agentscope-ai/QwenPaw/issues/7210)). Built-in tools enabled in `agent.json` are not appearing in the session's function schema. No fix PR yet.

3. **High — Tool call 404 in streaming sessions** ([Issue #7016](https://github.com/agentscope-ai/QwenPaw/issues/7016)). `ToolResultCapMiddleware`-related offload endpoint returns 404 during streaming; possibly related to the 7.6G history.db bloat issue below.

4. **Medium — history.db bloat to 7.6G** ([Issue #7168](https://github.com/agentscope-ai/QwenPaw/issues/7168)). Closed — `recall_history` expand writes full tool outputs to `conversation_history` repeatedly. Root cause identified in `ToolResultCapMiddleware`.

5. **Medium — Injected context persists as user history** ([PR #7211](https://github.com/agentscope-ai/QwenPaw/pull/7211)). Fix PR open (first-time contributor): request-local context injected via `HookContext.inject_context()` is incorrectly persisted as visible user chat history. Needs review.

6. **Medium — `daily_paper` crash on surrogate chars** ([Issue #7199](https://github.com/agentscope-ai/QwenPaw/issues/7199)). PDFs with U+D800–U+DFFF cause `UnicodeEncodeError` in `write_atomic`. No fix PR.

7. **Medium — Embedding health check fails on warm backend** ([Issue #7156](https://github.com/agentscope-ai/QwenPaw/issues/7156)). Timeout is hardcoded (5s) and not configurable; causes unjustified BM25 fallback.

8. **Low-medium — WebView2 renderer crash at startup** ([Issue #6427](https://github.com/agentscope-ai/QwenPaw/issues/6427)). Crash in v2.0.0+post.4 (~7s after launch). Open for ~1 month.

9. **Low — Non-ASCII filename mojibake in file cards** ([Issue #7136](https://github.com/agentscope-ai/QwenPaw/issues/7136)). Percent-encoded Chinese filenames display corruption.

10. **Low — Startup hang ~85s** ([Issue #6430](https://github.com/agentscope-ai/QwenPaw/issues/6430)). Background startup stalls consistently. Open for ~1 month.

## 6. Feature Requests & Roadmap Signals

Looking at newly open feature requests (mostly from the community, filed in the last 24–48 hours) and in-flight PRs, the following themes are likely to appear in the next releases:

- **Approval/workflow refinement** ([Issue #7198](https://github.com/agentscope-ai/QwenPaw/issues/7198)) — User requests that intermediate/scratch-file operations not trigger approval in any mode, only operations on pre-existing files. Will likely be addressed by the "autonomous mode" improvements that are already under discussion internally.

- **UI configurability for inference/tool-call display** ([Issues #7196, #7203](https://github.com/agentscope-ai/QwenPaw/issues/7196)) — Users want a toggle to fold/collapse the "reasoning process" and to hide tool-call information. Multiple users cite "HerMes"-style defaults. This is an obvious UX preference and low-code change; likely to land soon.

- **Per-session model overrides** ([PR #5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)) — Opt-in per-session model overrides for a single Agent. Under review for over a month; likely to be merged next milestone.

- **Session-scoped multi project directories** ([PR #6976](https://github.com/agentscope-ai/QwenPaw/pull/6976)) — Chat sessions bound to ordered project directories, with a primary directory for relative paths/cwd. Likely to advance to merge soon.

- **Creator expansion** ([PR #7167](https://github.com/agentscope-ai/QwenPaw/pull/7167)) — Mainstream image/video providers + Anthropic/Gemini protocols + dialogue-gated video dispatch. Large surface-area PR; likely targets a feature release (e.g., 2.2).

- **Per-provider media size caps** ([Issue #7201](https://github.com/agentscope-ai/QwenPaw/issues/7201)) — Request to split a single `max_inline_media_bytes` into separate `max_image_bytes`/`max_video_bytes`/`max_audio_bytes` settings, exposed in provider advanced settings.

- **Global hotkey quick-input window** ([PR #6607](https://github.com/agentscope-ai/QwenPaw/pull/6607)) — Doubao-style `alt+space` floating quick-input window for desktop. Open for ~3 weeks; likely to be merged soon.

- **Token usage attribution by agent** ([PR #7207](https://github.com/agentscope-ai/QwenPaw/pull/7207)) — Token usage currently tracked only by (date, provider, model); this PR stamps the agent ID and adds a "By Agent" table.

## 7. User Feedback Summary

- **Satisfaction signals:** The team's strong focus on closing old feature issues (frontend/backend test coverage) is well received. The PR #7190 (qwenpaw-data as a PyPI-runnable, Docker one-shot demo) is likely to be well-received by evaluators and users.

- **Pain points from issue reports in the last 24–48h:**

  - **"Overnight autonomous work is impossible"** ([Issue #7198](https://github.com/agentscope-ai/QwenPaw/issues/7198)) — Users doing overnight jobs complain that approval prompts block unattended progress. The request is to scope approvals carefully: only pre-existing files should require approval; scratch/intermediate files should be allowed automatically.

  - **"Reasoning overlays are visual noise"** ([Issues #7196, #7203](https://github.com/agentscope-ai/QwenPaw/issues/7196)) — For legal/reporting work, the constant tool-call and reasoning churn is considered clutter. Same user asked for a default-collapsed setting.

  - **"Hardcoded values with no config escape hatch"** ([Issue #7156](https://github.com/agentscope-ai/QwenPaw/issues/7156)) — The health-check timeout being hardcoded is seen as a fundamental config problem; users want every timeout/cap adjustable.

  - **"Search memory mixing sessions in web console"** ([Issue #7193](https://github.com/agentscope-ai/QwenPaw/issues/7193)) — In the online web console, an agent's memory search retrieved content from another session of the same agent, causing it to execute the wrong task. This is a serious correctness issue for multi-session web usage.

  - **"Custom channels not appearing in MCP tool authorization rules"** ([Issue #7197](https://github.com/agentscope-ai/QwenPaw/issues/7197)) — Custom channel plugins function normally but cannot be selected in MCP tool authorization rules; a dispatching gap between channel definitions and auth rule UI.

  - **"Desktop fullscreen dialogue window is overlapped by taskbar icons"** ([Issue #7195](https://github.com/agentscope-ai/QwenPaw/issues/7195)) — Minor but common desktop platform issue.

  - **"File upload size should not be limited on desktop"** ([Issue #4854](https://github.com/agentscope-ai/QwenPaw/issues/4854)) — Closed today. Users argue the desktop app should not limit upload size since only a local path/pointer is passed to the agent; server deployments should be separately configured.

## 8. Backlog Watch

Several items are aging and in need of maintainer attention:

- **[PR #5992 — Per-session model overrides](https://github.com/agentscope-ai/QwenPaw/pull/5992) (open since 2026-07-12)** — First-time contributor PR that has been "Under Review" for over five weeks. While feature scope is small and non-breaking, the review latency may discourage new contributors.

- **[Issue #6427 — WebView2 renderer crash on startup](https://github.com/agentscope-ai/QwenPaw/issues/6427) (open since 2026-07-24)** — A reproducible platform-specific crash on Windows. No fix PR or maintainer comment in the last 2+ weeks.

- **[Issue #6430 — Startup hang ~85s](https://github.com/agentscope-ai/QwenPaw/issues/6430) (open since 2026-07-24)** — Long-standing startup performance issue, wide user impact on desktop. No visible maintainer activity.

- **[Issue #7156 — Embedding health check timeout hardcoded](https://github.com/agentscope-ai/QwenPaw/issues/7156)** — The issue suggests the timeout lives in `reme/...` module with no configuration surface. Moderate effort to fix but has wide impact (warm users get degraded retrieval). Consider nominating for the next patch.

---

*Digest generated from CoPaw GitHub repository data, 2026-08-22.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-22

## 1. Today's Overview

ZeroClaw is in a period of intense development activity, with 50 issues and 50 pull requests updated in the last 24 hours. The overwhelming majority of issues remain open (49 of 50), signaling a substantial active backlog, while the PR pipeline is similarly saturated with 47 open PRs awaiting review or merge. The project is clearly prioritizing security and stability, with multiple high-severity issues (S0/S1) and `risk:high` labels dominating the latest reports. Notably, several critical bugs relate to the security sandbox, delegate risk profile bypasses, and data loss scenarios in TUI sessions. Despite the heavy bug load, the project is also advancing substantial architectural features, including plugin logical channel activation, a secure ZeroRelay transport frontdoor, and the ZeroRouter provider preset.

## 2. Releases

No new releases were published in the last 24 hours. The latest releases are not specified in the provided data.

## 3. Project Progress

While the data shows no PRs were merged today (3 closed/merged out of 50, but details are not provided), several significant PRs are in the pipeline, indicating substantial progress in key areas:

- **Security & Sandboxing**: [PR #10093](https://github.com/zeroclaw-labs/zeroclaw/pull/10093) isolates manifest-installed plugin subprocesses by clearing the inherited host environment, and [PR #10176](https://github.com/zeroclaw-labs/zeroclaw/pull/10176) enforces Alpine non-root image metadata in Docker CI.
- **Connectivity & Architecture**: [PR #10142](https://github.com/zeroclaw-labs/zeroclaw/pull/10142) brings the ZeroRelay secure transport and browser enrollment frontdoor (superseding #9080). [PR #10146](https://github.com/zeroclaw-labs/zeroclaw/pull/10146) introduces logical channel instance activation, a major daemon construction milestone.
- **Plugin System & Compute**: [PR #9645](https://github.com/zeroclaw-labs/zeroclaw/pull/9645) adds ZeroRouter, an in-house LLM gateway provider, with a preset and device-flow login.
- **Reliability Fixes**: [PR #10197](https://github.com/zeroclaw-labs/zeroclaw/pull/10197) persists interrupted Code/ACP turn progress, directly addressing an S0 data-loss bug; [PR #10203](https://github.com/zeroclaw-labs/zeroclaw/pull/10203) bridges the `log` facade into the tracing pipeline, fixing dropped dependency logs; [PR #10209](https://github.com/zeroclaw-labs/zeroclaw/pull/10209) correctly runs pgvector setup inside its own thread.
- **Desktop & UX**: [PR #10236](https://github.com/zeroclaw-labs/zeroclaw/pull/10236) bounds daemon capture logs to 8 MiB via a hidden supervisor.

## 4. Community Hot Topics

The most active discussions center on security policy enforcement and configuration, highlighting deep user engagement with the platform's governance model.

- **[#10165](https://github.com/zeroclaw-labs/zeroclaw/issues/10165) — Independent delegate bypasses `block_high_risk_commands` on its own risk profile** (3 comments, S0 security risk). Community concern over a logical flaw where delegates can circumvent their own risk settings, which could undermine tenant isolation or safety policy. The underlying need is for a unified, non-bypassable security policy layer.
- **[#10074](https://github.com/zeroclaw-labs/zeroclaw/issues/10074) — SECURITY.md documents a CI job that was removed in April** (3 comments, closed). Highlights community vigilance over security documentation accuracy and the need for internal consistency in CI/CD processes.
- **[#10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068) — Interactive agent session caps context at 32k tokens, ignoring configured 131,072** (3 comments, P2). An active point of frustration for advanced users whose `max_context_tokens` settings are being ignored in interactive sessions, despite being far below the configured limit.
- **[#10066](https://github.com/zeroclaw-labs/zeroclaw/issues/10066) — SOP engine promotes and runs later steps before recording a step's output-schema rejection** (3 comments, S1 workflow blocked). A critical logic flaw in the SOP engine that executes dependent steps even after a schema rejection, threatening workflow integrity.
- **[#10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059) — Support Option-Backspace in ZeroCode inputs** (3 comments). The most "human" feature request, highlighting macOS user ergonomics and the need for platform-standard editing behavior in the TUI.

## 5. Bugs & Stability

The project faces significant stability and security concerns, with several critical and high-severity bugs reported.

**Critical (S0 — data loss / security risk):**
- **[#10165](https://github.com/zeroclaw-labs/zeroclaw/issues/10165)** — Delegate risk profile bypass (`rm` allowed to run). *No direct fix PR currently linked.*
- **[#10121](https://github.com/zeroclaw-labs/zeroclaw/issues/10121)** — Partial Code/ACP turns disappear (data loss) on process exit. *Mitigated by* [PR #10197](https://github.com/zeroclaw-labs/zeroclaw/pull/10197).

**High Severity (S1 — workflow blocked):**
- **[#10066](https://github.com/zeroclaw-labs/zeroclaw/issues/10066)** — SOP engine promotes steps prematurely after schema rejection.
- **[#10230](https://github.com/zeroclaw-labs/zeroclaw/issues/10230)** — Quickstart stack overflow aborting the Tokio worker (S1). *Needs reproduction.*

**High-impact / Risky Bugs (P1, `risk:high`):**
- **[#10061](https://github.com/zeroclaw-labs/zeroclaw/issues/10061)** — Provider-rejected image poisons later turns in vision-capable session (S1).
- **[#10116](https://github.com/zeroclaw-labs/zeroclaw/issues/10116)** — Oversized tool results cut middle-out byte-wise, losing critical data for the model.
- **[#10115](https://github.com/zeroclaw-labs/zeroclaw/issues/10115)** — Tool-result truncation invisible externally, making debugging difficult.
- **[#10114](https://github.com/zeroclaw-labs/zeroclaw/issues/10114)** — `max_tool_result_chars` fixed 50k default, disconnected from model context window.
- **[#10202](https://github.com/zeroclaw-labs/zeroclaw/issues/10202)** — Log records from deps never reach the tracing subscriber. *Fixed in* [PR #10203](https://github.com/zeroclaw-labs/zeroclaw/pull/10203).
- **[#10199](https://github.com/zeroclaw-labs/zeroclaw/issues/10199)** — Plugin egress connect-deadline cannot cancel blocking `getaddrinfo`.

**Other Notable Fixes & Regressions:**
- **[#10237](https://github.com/zeroclaw-labs/zeroclaw/issues/10237)** — Telegram reply-threads fragment conversation memory (newest report today).
- **[#10162](https://github.com/zeroclaw-labs/zeroclaw/issues/10162)** — Plugin install persists before config seeding, not recoverable.
- **[#10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068)** — Interactive session ignores `max_context_tokens`.

## 6. Feature Requests & Roadmap Signals

Several feature requests and design tasks signal upcoming roadmap items:

- **[#10166](https://github.com/zeroclaw-labs/zeroclaw/issues/10166)** — Default `stream_mode` to `partial` for progressive replies. This would change the default user experience and may be included in a minor release.
- **[#10168](https://github.com/zeroclaw-labs/zeroclaw/issues/10168)** — Enable the stall watchdog by default (`stall_timeout_secs`). A conservative default could be adopted for the upcoming release.
- **[#10140](https://github.com/zeroclaw-labs/zeroclaw/issues/10140)** — iMessage voice message transcription, aligning with Telegram/Slack/Discord. High-value feature for iMessage channel users.
- **[#10086](https://github.com/zeroclaw-labs/zeroclaw/issues/10086)** — Make ZeroCode Logs selectable and copyable, improving core TUI usability.
- **[#10143](https://github.com/zeroclaw-labs/zeroclaw/issues/10143)** — Lifecycle-complete provider-call accounting for exact billing and diagnostics.
- **[#10073](https://github.com/zeroclaw-labs/zeroclaw/issues/10073)** — Retire `StoragePolicy::Rolling` and extend `/api/logs` to query across segments, a significant observability improvement.
- **[#10138](https://github.com/zeroclaw-labs/zeroclaw/issues/10138)** — Fully compile the Git Channel into the `zeroclaw:debian` Docker image.

The sheer number of in-progress (`status:in-progress`) and accepted (`status:accepted`) feature tasks indicates the roadmap is well-defined and active.

## 7. User Feedback Summary

User feedback is heavily skewed toward security and reliability concerns, reflecting the platform's power-user base.

- **Pain Points**: The most common frustration is the inconsistency in security policy enforcement ([#10165](https://github.com/zeroclaw-labs/zeroclaw/issues/10165), [#10164](https://github.com/zeroclaw-labs/zeroclaw/issues/10164), [#10175](https://github.com/zeroclaw-labs/zeroclaw/issues/10175)), where configured risk profiles are bypassed or incorrectly applied. The fixed 32k token cap in interactive sessions ([#10068](https://github.com/zeroclaw-labs/zeroclaw/issues/10068)) also represents a major performance bottleneck for users wanting to leverage long-context models.
- **Desired Features**: Users are advocating for more intuitive channel behaviors (iMessage transcription [#10140](https://github.com/zeroclaw-labs/zeroclaw/issues/10140), WhatsApp display name [#10200](https://github.com/zeroclaw-labs/zeroclaw/issues/10200)), improved TUI ergonomics (selectable logs [#10086](https://github.com/zeroclaw-labs/zeroclaw/issues/10086), Option-Backspace [#10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059)), and better system defaults (streaming replies [#10166](https://github.com/zeroclaw-labs/zeroclaw/issues/10166)).
- **Satisfaction Indicators**: The quick turnaround on some issues (e.g., [#10202](https://github.com/zeroclaw-labs/zeroclaw/issues/10202) → [PR #10203](https://github.com/zeroclaw-labs/zeroclaw/pull/10203)) and the existence of accepted design tasks suggest a responsive maintainer team and a healthy feedback loop. The community is actively filing detailed, well-categorized reports, demonstrating a high level of engagement.

## 8. Backlog Watch

Several important issues and PRs are languishing and need maintainer attention.

- **[PR #9645](https://github.com/zeroclaw-labs/zeroclaw/pull/9645) — ZeroRouter preset and device-flow login** (since 2026-08-01, `needs-author-action`). A massive (size:XL), priority-p1 PR that has been sitting for three weeks. The author needs to respond to review feedback.
- **[PR #9574](https://github.com/zeroclaw-labs/zeroclaw/pull/9574) — authorize approval responders** (since 2026-07-31, `needs-author-action`). A security fix (P1) for approval validation in Telegram/Slack/Lark/Matrix channels, unaddressed for over three weeks.
- **[PR #9637](https://github.com/zeroclaw-labs/zeroclaw/pull/9637) — guard temporary React Router RSC exception** (`do-not-merge`). This large CI fix has been open since 2026-08-01, and its `do-not-merge` flag blocks progress; needs a decision on its eventual merge path.
- **[Issue #10074](https://github.com/zeroclaw-labs/zeroclaw/issues/10074) — SECURITY.md invalid CI documentation** (closed today). Although closed, this issue highlighted a doc-maintenance gap that may point to underlying process issues.
- **[#10058](https://github.com/zeroclaw-labs/zeroclaw/issues/10058), [#10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059), [#10062](https://github.com/zeroclaw-labs/zeroclaw/issues/10062), [#10086](https://github.com/zeroclaw-labs/zeroclaw/issues/10086)** — Good-first-issue ZeroCode TUI bugs have been in progress (`status:in-progress`) since Aug 17-18, but no fix PRs are linked yet.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*