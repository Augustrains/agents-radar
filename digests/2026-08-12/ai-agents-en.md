# OpenClaw Ecosystem Digest 2026-08-12

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-12 00:52 UTC

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

Based on the GitHub data from OpenClaw for 2026-08-12, here is a structured project digest.

---

# OpenClaw Project Digest — 2026-08-12

## 1. Today's Overview

OpenClaw is exhibiting a very high level of activity with a heavy focus on stability and reliability. The project maintains a massive and dynamic issue tracker, with 500 issues and 500 PRs updated in the last 24 hours, indicating a strong, engaged community and an active maintainer response. The distribution of updates (390 open vs. 110 closed issues; 280 open vs. 220 merged/closed PRs) suggests a steady pace of both reporting and resolution. A significant cluster of recent, highly-commented issues revolves around **message delivery reliability**, **session-state corruption**, and **provider-specific integrations (Anthropic, DeepSeek, Codex)**. While no new releases were published today, the sheer volume of open PRs, many of which are flagged "ready for maintainer look," indicates a substantial queue of pending fixes and features awaiting merge.

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

This section details the most significant PRs that were merged or closed today. Unfortunately, the data provided does not include a detailed list of individual merged PRs. However, a substantial number of PRs (220) were marked as merged or closed in the last 24 hours. The following closed PRs, which address critical reliability and security concerns, represent significant progress:

- **[PR #122339](https://github.com/openclaw/openclaw/pull/122339) [Merged]**: `refactor(plugins): consolidate public artifact resolution` — A maintainer-led refactor to reduce duplication and standardize logic in the gateway's web-provider artifact resolution, improving maintainability and consistency.
- **[PR #122318](https://github.com/openclaw/openclaw/pull/122318) [Merged]**: `refactor: split agent and chat orchestration ownership` — A significant architectural refactor to separate concerns in the core orchestration logic, moving the codebase towards better modularity and easier review of state construction, streaming, and dispatch.
- **[PR #122328](https://github.com/openclaw/openclaw/pull/122328) [Merged]**: `fix(ui): match chat transcript text rendering to prototype` — A UI fix to align the Control UI's chat transcript styling with its design prototype, improving consistency for long-form reading.
- **[Issue #121675](https://github.com/openclaw/openclaw/issues/121675) [Closed]**: A **P0 Critical** boot-loop issue caused by a beta release being published without its companion plugins has been resolved, indicating a swift hotfix.

---

## 4. Community Hot Topics

The most active community discussions highlight significant reliability and trust concerns, particularly around silent failures and session management.

- **[Issue #121058](https://github.com/openclaw/openclaw/issues/121058) (62 comments):** This is the single most active issue, reporting that **silent reply failures are still occurring** even after a previous fix (#116277). The fact that this has a high comment count and was created recently (2026-08-09) suggests a severe and ongoing trust issue for users who are failing to get responses without any error. Underlying need: **Reliable, never-silent message delivery.**

- **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707) (37 comments):** A long-running feature request for **Memory Trust Tagging by Source**. This is a security-conscious feature proposal to tag memory entries by origin to prevent memory poisoning attacks. Underlying need: **Robust security against prompt injection and data tampering attacks.**

- **[Issue #92201](https://github.com/openclaw/openclaw/issues/92201) (22 comments):** This closed issue detailed a **critical bug where streamed thinking signatures from Anthropic were intermittently invalid on replay** in the embedded runner, with a recovery mechanism that never fires. Underlying need: **High reliability for multi-turn agent runs with streaming providers.**

- **[Issue #42475](https://github.com/openclaw/openclaw/issues/42475) (20 comments):** A popular feature request for **Per-agent cost budget enforcement at the gateway level**. Underlying need: **Enterprise-grade cost control and financial governance.**

Other highly active topics include a major reliability regression with Codex-backed Telegram sessions timing out ([#87744](https://github.com/openclaw/openclaw/issues/87744)), and a configurable streaming watchdog timeout for thinking models ([#68596](https://github.com/openclaw/openclaw/issues/68596)).

---

## 5. Bugs & Stability

There is a high volume of critical (P0/P1) bug reports, indicating significant stability challenges, particularly around provider integrations and core session state.

**Critical (P0):**
- **[Issue #121675](https://github.com/openclaw/openclaw/issues/121675) [Closed]**: As noted above, a release packaging error caused a boot loop. Resolved today.

**High Severity (P1):**
- **[Issue #87744](https://github.com/openclaw/openclaw/issues/87744)**: Codex-backed Telegram turns repeatedly time out. No fix PR is currently linked.
- **[Issue #74586](https://github.com/openclaw/openclaw/issues/74586)**: Embedded runner (AM plugin) aborts `memory_search` tool calls and misclassifies them as timeouts.
- **[Issue #84516](https://github.com/openclaw/openclaw/issues/84516)**: Long agent replies are **silently truncated at ~1000-1100 chars**. This is a severe silent data loss bug.
- **[Issue #53408](https://github.com/openclaw/openclaw/issues/53408)**: Tool parameters for `write` and `exec` are **silently dropped after long conversations**, leading to failures.
- **[Issue #47975](https://github.com/openclaw/openclaw/issues/47975)**: Subagent sessions persist after completion, causing the main session to become unresponsive.
- **[Issue #121953](https://github.com/openclaw/openclaw/issues/121953)**: A particularly odd bug where the `[cron:...]` prefix on messages causes DeepSeek's API to deprioritize them, stalling cron jobs.
- **[Issue #121327](https://github.com/openclaw/openclaw/pull/121327) [PR Open]**: A fix to freeze installed tool profile authority, addressing a security boundary issue.

**Medium Severity (P2):**
- **[Issue #121058](https://github.com/openclaw/openclaw/issues/121058)**: Silent reply failures still occurring. Despite being a recurring theme, no fix is linked.
- **[Issue #114154](https://github.com/openclaw/openclaw/issues/114154)**: `bundle-mcp` tool that passes policy checks is never actually used by agents, a silent integration failure.
- **[Issue #119009](https://github.com/openclaw/openclaw/issues/119009) [Closed]**: A **runaway retry loop billed $204** over two incidents. Critical cost and reliability issue.

---

## 6. Feature Requests & Roadmap Signals

Several open feature requests and open "needs-product-decision" issues suggest potential roadmap items.

- **Enhanced Governance and Controls:**
    - **[Issue #42475](https://github.com/openclaw/openclaw/issues/42475)**: Per-agent cost budgets.
    - **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707)**: Source-based memory trust tagging.
    - **[Issue #47910](https://github.com/openclaw/openclaw/issues/47910)**: Provider fallback by failure class (e.g., quarantine auth-broken providers).

- **Platform Expansion and Multi-Tenancy:**
    - **[Issue #71058](https://github.com/openclaw/openclaw/issues/71058)**: Support for multiple Azure/Teams bots on a single gateway.
    - **[Issue #66252](https://github.com/openclaw/openclaw/issues/66252)**: Per-agent TTS/STT configuration overrides for multi-language support.

- **Core UX & Usability:**
    - **[Issue #14785](https://github.com/openclaw/openclaw/issues/14785)**: Reduce tool schema token overhead (~3,500 tokens/session) to save costs and increase context space.
    - **[Issue #13700](https://github.com/openclaw/openclaw/issues/13700)**: Session snapshots (`/session save|load`) to checkpoint and branch conversations.
    - **[Issue #42840](https://github.com/openclaw/openclaw/issues/42840)**: MathJax/LaTeX support in the Control UI.

---

## 7. User Feedback Summary

- **Major Pain Point: Silent Failures.** The most significant source of user dissatisfaction is the prevalence of silent failures. The top issue is about replies failing without any error ([#121058](https://github.com/openclaw/openclaw/issues/121058)), and others report silent truncation ([#84516](https://github.com/openclaw/openclaw/issues/84516)) and silent tool parameter drops ([#53408](https://github.com/openclaw/openclaw/issues/53408)). Users are demanding explicit and reliable error reporting.
- **Reliability of Provider Integrations:** Many high-severity bugs are isolated to specific providers (Anthropic, Codex, DeepSeek), causing friction for users who rely on these. The timeouts, truncations, and stalls indicate a need for more robust and well-tested integrations.
- **Observability and Control:** Users want better observability into what model is actually being used behind a proxy ([#51441](https://github.com/openclaw/openclaw/issues/51441)) and better control over runaway resource usage, as seen in the cost-budget requests ([#42475](https://github.com/openclaw/openclaw/issues/42475)) and the $204 retry loop story ([#119009](https://github.com/openclaw/openclaw/issues/119009)).
- **Security and Trust:** The popularity of the memory-trust-tagging feature ([#7707](https://github.com/openclaw/openclaw/issues/7707)) and various security-related fixes indicates a strong user desire for hardened security and proactive mitigation of poisoning and injection attacks.

---

## 8. Backlog Watch

Several important issues have been open for months and are flagged with `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`, suggesting they are stuck in the pipeline.

- **[Issue #42475](https://github.com/openclaw/openclaw/issues/42475)** (Created: 2026-03-10): Per-agent cost budget enforcement remains undecided and unassigned after 5 months.
- **[Issue #7707](https://github.com/openclaw/openclaw/issues/7707)** (Created: 2026-02-03): The high-interest Memory Trust Tagging feature request has been open for over 6 months without a clear decision, despite having strong community engagement.
- **[Issue #14785](https://github.com/openclaw/openclaw/issues/14785)** (Created: 2026-02-12): The proposal to reduce tool schema token overhead, a clear win for cost and performance, is still awaiting maintainer review.
- **[Issue #53408](https://github.com/openclaw/openclaw/issues/53408)** (Created: 2026-03-24): This critical P1 bug (silent parameter drops) is still open with no linked fix PR, 4.5 months after creation.
- **[Issue #87744](https://github.com/openclaw/openclaw/issues/87744)** (Created: 2026-05-28): This P1 bug (Codex/Telegram timeouts) is still open and only tagged as `needs-live-repro`, indicating difficulties in diagnosis but a need for a faster resolution given its impact.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-12
**Scope:** 12 projects in the personal AI assistant / agent open-source ecosystem

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing a **second wave of maturation**, characterized by a shift from feature velocity to **reliability, security, and architectural consolidation**. Across all active projects, the dominant user pain points are **silent failures** (message drops, tool-call truncation, config inertness) and **runaway loops** (unbounded retries, repeated messages, cost overruns). Projects are investing heavily in **context-window integrity** — preventing silent task eviction, managing memory across sessions, and reducing token overhead. A clear architectural split is emerging: **monolithic assistants** (OpenClaw, Hermes, TinyClaw) versus **kernel/pluggable architectures** (IronClaw, ZeroClaw) that delegate agent loops to external runtimes. Security hardening is no longer optional; every project with meaningful activity is addressing sandbox escapes, API-key leakage, and prompt-injection resistance. The ecosystem is consolidating around **MCP compatibility** as the standard for tool integration, with multiple projects adding remote/streamable HTTP MCP support this week.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Merged/Closed PRs | Release Status | Health Score |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 220 | None | **8.5/10** — Massive volume, critical bugs persist |
| **NanoBot** | 6 | 140 | 119 | None | **8.0/10** — High merge velocity, strong hygiene |
| **Hermes Agent** | 50 | 50 | 7 | None (v0.20.0) | **7.0/10** — Active refactoring, Windows regressions |
| **PicoClaw** | 3 | 6 | 0 | None (v0.3.1) | **6.5/10** — Maintenance phase, review bottleneck |
| **NanoClaw** | 1 | 8 | 3 | None | **7.5/10** — High-velocity feature work |
| **NullClaw** | — | — | — | — | **N/A** — No activity |
| **IronClaw** | 23 | 50 | 25 | None (v1.3.0 pending) | **8.5/10** — Intense consolidation, QA-driven |
| **LobsterAI** | 4 | 10 | 7 | **2026.8.11** ✓ | **7.0/10** — Shipping steadily, open bugs |
| **TinyClaw** | — | — | — | — | **N/A** — No activity |
| **Moltis** | 0 | 2 | 0 | None | **6.5/10** — Low but purposeful |
| **CoPaw** | 23 | 49 | 25 | **v2.1.0-beta.3** ✓ | **7.5/10** — High velocity, MCP issues |
| **ZeroClaw** | 50 | 50 | 2 | None (v0.9.0 pending) | **7.5/10** — RFC-heavy, review-bound |

---

## 3. OpenClaw's Position

**Advantages vs. peers:**

- **Scale & community depth**: With 500 issues and 500 PRs updated in 24 hours, OpenClaw has the largest and most engaged community in the ecosystem — roughly **10x the issue volume** of its nearest competitor (Hermes, IronClaw, ZeroClaw at 50 each). This scale provides a formidable bug-detection and feature-request pipeline.
- **Provider breadth**: The project actively integrates with Anthropic, DeepSeek, Codex, and more, often simultaneously — a level of multi-provider support that most peers (PicoClaw, LobsterAI) handle with narrower profiles.
- **Architecture maturity**: The recent refactors (consolidating artifact resolution, splitting agent/chat orchestration ownership) indicate a codebase mature enough for structural investment.

**Technical approach differences:**

- **Gateway-centric**: OpenClaw treats the gateway as the core abstraction, with agents, channels, and providers plugging into it. This contrasts with IronClaw's kernel/ACP approach (delegating loops to external agents) and ZeroClaw's runtime-owned security pipeline.
- **Single-monolith trajectory**: While the project is refactoring for modularity, it remains architecturally a **large monolith** — unlike the more aggressive sharding efforts in Hermes (god-file decomposition) and ZeroClaw (RFC-driven componentization).

**Community size comparison:**

| Metric | OpenClaw | Next Largest (IronClaw/ZeroClaw) | Ratio |
|---|---|---|---|
| Issues updated/24h | 500 | 23–50 | 10–20x |
| PRs updated/24h | 500 | 50 | 10x |
| Top issue comments | 62 | 19 | 3x |
| Merge/close rate/24h | 220 | 25 | 9x |

**Key risk**: Silent-failure bugs (#121058, #84516, #53408) persist despite high fix velocity. The sheer issue volume may be overwhelming triage capacity, allowing P1/P2 reliability bugs to linger for months.

---

## 4. Shared Technical Focus Areas

**1. Silent Failure Elimination** *(OpenClaw, NanoClaw, IronClaw, PicoClaw)*
- OpenClaw: Silent reply failures (#121058), silent truncation (#84516), silent tool-param drops (#53408)
- NanoClaw: Inbound messages dropped on ID reuse (#3226)
- IronClaw: Context window silently evicts task (#7484)
- PicoClaw: Inert config settings (LINE webhook #3328), multi-agent history loss (#3301)

**2. Loop/Runaway Detection** *(OpenClaw, NanoBot, IronClaw, CoPaw)*
- OpenClaw: Runaway retry loop billed $204 (#119009)
- NanoBot: Repeated messages during reasoning (#5327), `/goal` spawning dozens of replies (#5256)
- IronClaw: No-progress false-positives (#7486), dead-code retry disposition (#7490)
- CoPaw: Idle CPU at ~20% from infinite CSS animations (#6828)

**3. Context-Window Integrity** *(OpenClaw, IronClaw, NanoBot, PicoClaw)*
- IronClaw: 128-message clamp evicts task (#7484), token estimator double-counts (#7485)
- NanoBot: Repeated messages during reasoning (loop eats context)
- PicoClaw: Routed chats lose history and skip auto-compaction (#3301)
- OpenClaw: Tool schema token overhead ~3,500 tokens/session (#14785)

**4. Security Hardening** *(OpenClaw, NanoBot, ZeroClaw, CoPaw)*
- NanoBot: `exec.allowPatterns` shell-chain bypass (#5306), API-key leaks (#4784, #4783)
- ZeroClaw: WebP decompression DoS (#9883), filesystem sandbox escape (#9872), WebAuthn validation
- CoPaw: Plugins silently create cron jobs / inject messages (#6916)
- OpenClaw: Memory trust tagging by source (#7707)

**5. MCP & Provider Interop** *(NanoClaw, ZeroClaw, CoPaw, IronClaw)*
- NanoClaw: Remote Streamable HTTP MCP servers (merged for Claude, Codex, OpenCode)
- ZeroClaw: Chat Completions profile for OpenAI-compat clients (RFC #8603)
- CoPaw: MCP tools periodically fail (#6732), configurable timeout (#6874)
- IronClaw: Pluggable agent loops via ACP (#7482), GitHub MCP extension startup (#7508)

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Architectural Approach |
|---|---|---|---|
| **OpenClaw** | General-purpose assistant | Power users, multi-provider | Gateway-centric monolith; massive provider/channel matrix |
| **NanoBot** | Lightweight multi-provider agent | Developers, self-hosters | Provider abstraction layer; rapid provider addition (OrcaRouter, Kimi) |
| **Hermes Agent** | Desktop-first assistant | Windows/macOS desktop users | Desktop app + gateway; deep OS integration (TTS, browser_exec) |
| **PicoClaw** | Embedded/small-footprint | Resource-constrained deployments | Minimal core; community-driven fixes |
| **NanoClaw** | MCP-forward assistant | MCP ecosystem adopters | First-class MCP tooling; Agent Plugins 1.0.0 migration |
| **IronClaw** | Kernel/pluggable runtime | Enterprise, multi-tenant | ACP-based pluggable loops; profile-agnostic durable state |
| **LobsterAI** | Cowork/desktop collaboration | NetEase Youdao users | Electron desktop; Cowork session features; per-model config |
| **Moltis** | Local-first personal data | Privacy-focused users | Local CalDAV connectors; data-as-substrate for agents |
| **CoPaw** | QwenPaw ecosystem | Chinese-speaking users | Multi-channel (QQ, WeChat); bilingual feature set; console-first |
| **ZeroClaw** | Enterprise control plane | Operators, IT teams | RFC-driven; SOP automation, security pipeline ownership |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration (high velocity, multiple releases/refactors per quarter):**
- **OpenClaw** — Massive but chaotic; 220 merges/day, P0 boot-loop fixed same-day. Maturity: **Established but reliability-strained**.
- **IronClaw** — QA-driven consolidation; 25 merges/day, systematic loop-hardening. Maturity: **Architecturally ambitious, disciplined**.
- **CoPaw** — Beta release cadence; feature + fix velocity balanced. Maturity: **Growing fast, MCP instability is key risk**.

**Tier 2 — Steady Maturity (stable cadence, clear backlog hygiene):**
- **NanoBot** — 119 merges/day, aggressive stale-PR cleanup, security-focused. Maturity: **Responsive, security-aware**.
- **ZeroClaw** — RFC-heavy process, high-quality but review-bound. Maturity: **Pre-v0.9, standardization phase**.
- **NanoClaw** — Feature-leading (MCP, plugins) but minimal community engagement. Maturity: **Core-team-led, community lagging**.

**Tier 3 — Stabilization / Maintenance (low but purposeful activity):**
- **Hermes Agent** — Refactoring-focused, Windows regressions unresolved. Maturity: **In transition**.
- **LobsterAI** — Shipping releases but inconsistent maintainer response to issues. Maturity: **Product-focused, process gaps**.
- **PicoClaw** — Maintenance mode; fix PRs queueing for review. Maturity: **Stable, under-resourced**.

**Tier 4 — Quiet / Dormant:**
- **Moltis** — Two PRs, no issues, minimal engagement.
- **NullClaw, TinyClaw, ZeptoClaw** — No activity in window.

---

## 7. Trend Signals

**1. "Silent failure" is the new P0.**
Across OpenClaw, NanoClaw, IronClaw, and PicoClaw, the most severe user-reported issues are not crashes but **silent failures**: messages dropped, tasks evicted, configs ignored, tool params truncated — all without user-visible errors. The community is demanding explicit failure surfacing ("never silent"). **Value for developers:** Instrument all failure paths with visible, actionable errors; treat "the agent ignored me" as the top reliability metric.

**2. Context-window management is the AI-agent equivalent of memory management.**
IronClaw's eviction bug, PicoClaw's history loss, and OpenClaw's token-overhead request all point to a systemic challenge: **agents running out of context with no graceful degradation**. The trend is toward pinned tasks, budget-aware eviction, and compact-on-eviction rather than silent truncation. **Value for developers:** Design context management as an explicit lifecycle (pin, evict, summarize, fail-loud) rather than an invisible tail-cut.

**3. Loop detection is becoming a standard feature, not a nice-to-have.**
NanoBot's repeated-reply bugs, OpenClaw's $204 retry-loop incident, and IronClaw's no-progress false-positives show that **unbounded agent loops are a production-reliability threat**. Projects are shipping idle bounds, repeated-call warnings, and kill-switches. **Value for developers:** Build loop detection into the agent runtime (same-tool-same-args warnings, turn budgets, idle timeouts) as a first-class feature.

**4. The kernel/pluggable-agent debate is splitting the ecosystem.**
IronClaw's ACP "kernel" direction and ZeroClaw's RFC-driven componentization contrast sharply with OpenClaw's gateway-centric monolith. The trend favors **interchangeable agent loops** (ACP, external runtimes) over single-vendor lock-in. **Value for developers:** Design agent loops behind an interface; assume the loop may be replaced by a third-party runtime.

**5. Security hardening has shifted from encryption to sandbox and injection resistance.**
The most common security bugs this week: **API-key leaks via environment leaks** (NanoBot), **sandbox bypasses via shell chains** (NanoBot, ZeroClaw), **unbounded decompression** (ZeroClaw), and **plugin-driven silent injection** (CoPaw). **Value for developers:** Audit subprocess environments, validate sandbox patterns against shell metacharacters, and require explicit user consent for plugin-installed persistence.

**6. MCP is consolidating as the universal tool standard — but remote MCP is the next frontier.**
NanoClaw merged remote Streamable HTTP MCP support; CoPaw is stabilizing flaky MCP tools; ZeroClaw's Chat Completions RFC targets OpenAI-compat clients. **Value for developers:** Adopt MCP as the tool interface; prioritize remote/streamable support for SaaS-hosted tools; expect MCP tool flakiness to be a recurring production issue.

**7. Cost governance is emerging as a product feature, not just administration.**
OpenClaw per-agent budgets (#42475), the $204 retry-loop incident (#119009), ZeroClaw token-accounting on history-trim (#9713), and token-overhead reduction requests all signal that **users are demanding financial control at the agent level**. **Value for developers:** Implement per-agent cost budgets, retry-loops with monetary bounds, and visible token accounting in the UI.

---

**Bottom line:** The ecosystem is healthy but strained — community engagement is at an all-time high, but maintainer bandwidth is the critical bottleneck across all projects. The winners in the next 12 months will be those that eliminate silent failures, implement robust loop detection, and standardize on MCP with remote support — all while keeping the agent loop replaceable.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-12

## 1. Today's Overview

NanoBot is showing strong and steady development velocity. In the last 24 hours, the repository recorded **140 pull requests updated**, with 119 merged or closed and 21 still open — indicating a very active contribution pipeline. Issue activity was lighter but meaningful, with 6 issues updated, 2 of which remain open. The project is in a healthy state with a notable focus on **security hardening** (three security-related issues/PRs) and **loop/repetition bug fixes** related to agent behavior. No new releases were published in this window, suggesting the maintainers are consolidating changes before the next version cut.

## 2. Releases

No new releases were published in the last 24 hours. Versioning activity appears paused while the maintainers process the large influx of merged PRs.

## 3. Project Progress

The 24-hour window saw 119 merged/closed PRs, indicating a high-volume merge cadence. The most notable merged items include:

- **[#5327 — Bug: repeated messages during reasoning](https://github.com/HKUDS/nanobot/issues/5327)** — Closed; addresses a bug where the agent randomly repeats the same phrase multiple times during reasoning.
- **[#4784 — Security: Provider API keys leaked between providers](https://github.com/HKUDS/nanobot/issues/4784)** — Closed; fixes a critical vulnerability where `OpenAICompatProvider._setup_env()` mutated the global `os.environ`, causing API key leakage between gateway-type providers.
- **[#4783 — Security: CLI apps run with full os.environ](https://github.com/HKUDS/nanobot/issues/4783)** — Closed; fixes API keys leaking to installed app subprocesses via an unfiltered `os.environ.copy()`.
- **[#5333 — Feature: OpenRouter Server Tools support](https://github.com/HKUDS/nanobot/issues/5333)** — Closed as an enhancement, likely paving the way for server-side tool integration.

While the majority of closed PRs are older (dating back to February–March 2026), they are marked with `[conflict]` labels, suggesting they were **closed due to conflict or staleness** rather than merged. This indicates the maintainers are actively cleaning up outdated contributions — a sign of strong backlog hygiene.

## 4. Community Hot Topics

The most active discussions in this window:

- **[Issue #5327 — Repeated messages while reasoning](https://github.com/HKUDS/nanobot/issues/5327)** (9 comments, closed) — Users reported the agent randomly repeating phrases like "Good points, let me investigate the issue" during reasoning. This is a behavioral bug that affects user experience with long-running investigations.

- **[Issue #5256 — /goal message produces dozens of repeated replies](https://github.com/HKUDS/nanobot/issues/5256)** (2 comments, open) — A related loop-behavior bug where a single `/goal` command triggers dozens of near-identical replies while awaiting user input. The user had to intervene manually to stop it.

The **underlying need** is clear: users require **predictable, non-looping agent behavior**. Both issues point to inadequate loop detection in the agent's turn-taking logic. Community sentiment is constructive — reporters provided detailed reproduction steps, enabling maintainers to act quickly.

## 5. Bugs & Stability

Bugs reported or updated in this window, ranked by severity:

| Severity | Issue/PR | Description | Status |
|----------|----------|-------------|--------|
| 🔴 Critical | [#5306 — `exec.allowPatterns` shell-chain bypass](https://github.com/HKUDS/nanobot/issues/5306) | The `exec` tool's `allowPatterns` sandbox can be bypassed via shell chains (e.g., `cmd; cmd2`), allowing unintended command execution. **Fix PR exists: [#5345](https://github.com/HKUDS/nanobot/pull/5345).** | [Open issue](https://github.com/HKUDS/nanobot/issues/5306) + [fix PR open](https://github.com/HKUDS/nanobot/pull/5345) |
| 🟠 High | [#5327 — Repeated messages during reasoning](https://github.com/HKUDS/nanobot/issues/5327) | Agent randomly repeats phrases during reasoning loops. | Closed (fixed) |
| 🟠 High | [#5256 — `/goal` produces dozens of repeated replies](https://github.com/HKUDS/nanobot/issues/5256) | Sustained-goal continuation spirals into dozens of replies when idle. **Fix PR exists: [#5257](https://github.com/HKUDS/nanobot/pull/5257)** | Open |
| 🟡 Medium | [#5344 — No loop detection on repeated tool calls](https://github.com/HKUDS/nanobot/pull/5344) | New PR to warn instead of silently spiraling when the agent calls the same tool with the same args repeatedly. | Open PR |

Two security vulnerabilities from July (##4784, ##4783) were **closed as fixed** this window, but the new `exec.allowPatterns` bypass (#5306) is a fresh critical finding with a pending fix.

## 6. Feature Requests & Roadmap Signals

Notable feature requests and signals from this window:

- **[#5333 — OpenRouter Server Tools support](https://github.com/HKUDS/nanobot/issues/5333)** — Users want to leverage OpenRouter's server-side tools (Web Search, Web Fetch, Fusion) directly in the `tools` field. This is a natural extension of NanoBot's multi-provider approach and **highly likely** to land in an upcoming release.

- **[#5328 — OrcaRouter as a named gateway provider](https://github.com/HKUDS/nanobot/pull/5328)** — An open PR to add OrcaRouter as a provider. Given the pattern of rapid provider addition (Xiaomi MiMo, OpenCode Zen, Kimi Coding in the merged pipeline), this is likely to be reviewed and merged soon.

- **[#5283 — Per-session sandbox isolation for non-WebUI channels](https://github.com/HKUDS/nanobot/pull/5283)** — Opt-in sandbox per session for CLI/Telegram channels. This aligns with the security-focused direction of the project and may be prioritized.

- **[#5342 — Redesign apps discovery (WebUI)](https://github.com/HKUDS/nanobot/pull/5342)** — A UI/UX overhaul for app discovery with curated featured batches. Signals an investment in the WebUI's user experience.

**Prediction:** The next minor release will likely include OpenRouter Server Tools, the exec pattern fix (#5345), and the loop-prevention PRs (#5257, #5344), given the project's responsiveness to security and stability issues.

## 7. User Feedback Summary

- **Positive sentiment** — Users are enthusiastic about NanoBot's capabilities. One request (#5333) explicitly opened with *"First of all, thank you for creating such an amazing project. I really appreciate it."*

- **Pain points (loop/repetition behavior)** — The most vocal complaints revolve around **agent loops**: repeated messages during reasoning, duplicated replies on `/goal`, and no visible signal when the agent is stuck. Users are forced to manually intervene. The proposed fixes (warnings, idle bounds) directly address these frustrations.

- **Security consciousness** — Community members (e.g., `hamb1y`, `YLChen-007`) are actively auditing the codebase for security issues, demonstrating a mature, security-aware user base. The maintainers' quick closure of the environment-leak issues shows responsiveness.

- **Feature appetite** — Users request support for more providers (MiMo, OrcaRouter, Kimi) and richer tooling (Tavily, inline keyboards, server tools), indicating a desire for **breadth of integrations**.

## 8. Backlog Watch

Long-standing items needing maintainer attention:

- **[PR #4291 — Subagents with configurable model presets](https://github.com/HKUDS/nanobot/pull/4291)** (open since June 11, 2026) — An enhancement to let subagents run with different models. No recent maintainer activity. Feature creep risk if left untouched too long.

- **[PR #4145 — Fix for Weather Skill](https://github.com/HKUDS/nanobot/pull/4145)** (open since June 1, 2026) — Multi-file contribution. A newer PR (#5341) also addresses Windows-safe weather skills — the older one may be superseded.

- **[Issue #5256 — `/goal` repetition bug](https://github.com/HKUDS/nanobot/issues/5256)** (open since Aug 5) — While a fix PR (#5257) exists, it is still open. Given the severity of user-facing behavior, this should be prioritized for merge.

- **Stale historical PRs** — A large batch of PRs from Feb–Mar 2026 was closed this window with `[conflict]` labels. If these were intentionally superseded, consider adding a comment to guide contributors on how to rebase or re-open.

---

*Digest generated from GitHub data as of 2026-08-12. All links point to the [HKUDS/nanobot repository](https://github.com/HKUDS/nanobot).*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the GitHub activity for Hermes Agent on 2026-08-12, here is the project digest.

---

# Hermes Agent Project Digest — 2026-08-12

## 1. Today's Overview
The Hermes Agent project is in a highly active state, with 50 issues and 50 PRs updated in the last 24 hours. The repository is currently undergoing a major architectural refactoring effort to shard large "god files" into modular components, as evidenced by several large open epics. While there were no official new releases today, the focus is on stabilization, with a significant number of bug fixes targeting Windows desktop compatibility, session-state management, and message delivery reliability. The maintainers are actively processing a high volume of incoming bug reports and community-submitted pull requests to address these regressions and feature requests.

## 2. Releases
No new releases were published today. The most recent release remains version 0.20.0, which is referenced in some of the bug reports, indicating it is the latest stable version users are running.

## 3. Project Progress
There were 7 PRs merged or closed today, though specific merged changes were not detailed in the provided data. The primary focus of the current contributions is on **fixing regressions and stabilizing existing features** rather than introducing new major functionality. The most significant activity is in the form of open PRs ready for review, which address critical bugs reported in the community. Key areas of progress include:
- **Cross-platform Fixes**: PR [#84179](https://github.com/NousResearch/hermes-agent/pull/84179) improves `hermes doctor` to detect half-installed distributions, and PR [#84178](https://github.com/NousResearch/hermes-agent/pull/84178) adds a Nix home-manager module.
- **Bug Fixes Ready for Review**: PR [#84174](https://github.com/NousResearch/hermes-agent/pull/84174) pins background process completion notifications to the spawning session, and PR [#84181](https://github.com/NousResearch/hermes-agent/pull/84181) fixes local TTS providers writing incorrect audio formats.
- **Core State Management**: PR [#84145](https://github.com/NousResearch/hermes-agent/pull/84145) adds the storage layer for a cross-process turn lease, a key step toward resolving issue [#67442](https://github.com/NousResearch/hermes-agent/issues/67442).

## 4. Community Hot Topics
The most active discussion by far is the **Epic to shard all 20 "god files"** across the repository, indicating a community- and maintainer-driven push for cleaner code architecture.

- **[#78647](https://github.com/NousResearch/hermes-agent/issues/78647) - Epic: Shard all 20 god files — repo-wide god-file decomposition** (67 comments): This epic is driving a significant refactoring effort. The community and maintainers are actively discussing the strategy for decomposing large, monolithic files into more modular and maintainable components.
- **[#67442](https://github.com/NousResearch/hermes-agent/issues/67442) - Cross-process turn serialization: CLI-continuity sessions need a DB-level lease** (14 comments): A deep technical discussion about a persistent session-state issue. This is a high-priority topic as it directly impacts the reliability of the agent's memory and session continuity.
- **[#66616](https://github.com/NousResearch/hermes-agent/issues/66616) - Skills index is stale or degraded** (13 comments): An automated probe has detected the Skills Hub documentation index is not being updated on schedule, suggesting a potential issue with the documentation build pipeline and a need for process fixes.

## 5. Bugs & Stability
Today's issue tracker shows a strong focus on stability, with several **High Severity (P1)** bugs reported, particularly around the Windows desktop experience.

- **[#83683](https://github.com/NousResearch/hermes-agent/issues/83683) (P1) - Desktop restart reaps the live gateway but never relaunches it (WeChat/QQ go silent) — regression**: A critical regression in the desktop app causing messaging gateways to go silent after a restart.
- **[#83562](https://github.com/NousResearch/hermes-agent/issues/83562) (P1) - Windows Desktop update: backend works manually but Desktop reports `Hermes backend exited (0)`**: A significant issue causing the desktop backend to fail to start after an update.
- **[#63717](https://github.com/NousResearch/hermes-agent/issues/63717) (P1) - Windows: Hermes Desktop update failures — comprehensive diagnostic with 7 correlated root causes**: An ongoing, complex problem with Windows updates, although it has not been updated in a few days.
- **[#83427](https://github.com/NousResearch/hermes-agent/issues/83427) (P2) - browser_exec crashes: pydantic_core ModuleNotFoundError when PYTHONPATH points at Hermes venv**: A compatibility issue between the desktop app and the `browser_exec` tool.
- **[#83213](https://github.com/NousResearch/hermes-agent/issues/83213) (P2) - Background process completion notifications misrouted to wrong session after /new**: A session-state bug. A fix exists in PR [#84174](https://github.com/NousResearch/hermes-agent/pull/84174).
- **[#84172](https://github.com/NousResearch/hermes-agent/issues/84172) (P2) - webhook: platform_toolsets.webhook key ignored**: A configuration bug preventing webhook sessions from accessing platform tools.
- **[#84169](https://github.com/NousResearch/hermes-agent/issues/84169) (P2) - Empty tool_calls array 400s strict providers**: An issue causing compatibility problems with strict API providers, likely due to incomplete sanitization.
- **[#84102](https://github.com/NousResearch/hermes-agent/issues/84102) (P2) - Local TTS providers write Ogg/Vorbis into .ogg paths**: This bug is fixed by open PR [#84181](https://github.com/NousResearch/hermes-agent/pull/84181).

## 6. Feature Requests & Roadmap Signals
Several feature requests signal the future direction of Hermes Agent, focusing on deeper integration and user control.

- **Enhanced Delegation Control**: Issue [#80222](https://github.com/NousResearch/hermes-agent/issues/80222) requests per-call model and reasoning_effort overrides on `delegate_task`. This is a common request for a more versatile agent.
- **New Provider Support**: Issue [#83244](https://github.com/NousResearch/hermes-agent/issues/83244) requests adding Google Antigravity as a first-class OAuth provider, indicating continuous effort to support new AI models.
- **Event Substrate Architecture**: Issue [#49190](https://github.com/NousResearch/hermes-agent/issues/49190) proposing generalizing Kanban notifications into an event substrate is a major architectural feature, suggesting a move towards a more composable and modular system. This aligns with the "god-file" sharding initiative.
- **Maintainer Response**: Many of these issues are tagged `needs-decision`, suggesting they are under review by the maintainers. The next minor or major release will likely include the K-number of small fixes for session-state and Windows stability issues that are currently ready for review in PRs.

## 7. User Feedback Summary
Real user pain points this week center heavily on the **Windows desktop experience**. Users are reporting significant frustration with update failures (issues #83562, #63717, #68760, #82186) and the application's behavior after restarts (#83683). These are critical usability issues that impact core functionality. Another common theme is **concern over data and privacy**, with users reporting that the UI leaks text-fence language (#57540) and requesting credential redaction (#84153). The high comment counts and thumbs-up reactions on these issues indicate a strongly dissatisfied segment of the Windows user base. However, the active community engagement in proposing fixes suggests a dedicated user base willing to help improve the platform.

## 8. Backlog Watch
The following issues and PRs have been open for a significant time (over a month) and may require maintainer attention to unblock.

- **[PR #53894](https://github.com/NousResearch/hermes-agent/pull/53894) (Open since Jun 28)**: A large PR to fix session-owned shell hooks for the dashboard and TUI. This PR has many labels and is complex, likely requiring extensive review.
- **[PR #53811](https://github.com/NousResearch/hermes-agent/pull/53811) (Open since Jun 27)**: A fix for a stable tiebreaker in session ordering. A small but important fix for deterministic agent behavior.
- **[Issue #57540](https://github.com/NousResearch/hermes-agent/issues/57540) (Open since Jul 3, 2 👍)**: A desktop UI bug about text-fence language leaking into rendered prose. A low-priority but visible bug affecting the desktop experience.
- **[Issue #49190](https://github.com/NousResearch/hermes-agent/issues/49190) (Open since Jun 19)**: A significant feature proposal to generalize Kanban notifications into an event substrate. This feature has been waiting for a decision for nearly two months.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for **2026-08-12**.

---

## PicoClaw Project Digest — 2026-08-12

### 1. Today's Overview
PicoClaw is in a stable maintenance phase with steady, moderate contribution activity. Over the last 24 hours, the repository saw 3 issue updates and 6 open pull requests, with **no new releases or merges** pushing the trunk forward. While feature development is paused, the community is actively submitting fixes for identified bugs, particularly around context management for routed agents and command/configuration correctness. The maintainer team has pending "stale" labels on several PRs, indicating a potential backlog in review throughput rather than a lack of community contribution.

### 2. Releases
**No new releases** were published in the last 24 hours. The project remains on version **0.3.1** (commit `2cf030d`). Users experiencing the bugs mentioned below should monitor for a potential patch release (e.g., `0.3.2`) gathering the currently open fixes.

### 3. Project Progress
**No Pull Requests were merged or closed** in the last 24 hours. The primary focus remains on the open PRs awaiting review. Key fixes queued for maintainers include:
- **`#3314`**: A fix for `customAllowPatterns` in shell commands, correcting default-deny precedence which previously blocked explicitly allowed commands like `git push`.
- **`#3316`**: A significant fix for routed-agent context management, addressing history loss, summarization, and auto-compaction failures in non-default agent chats.
- **`#3329`**: A warning-instead-of-silence fix for inert `webhook_host`/`webhook_port` configuration settings for LINE.

### 4. Community Hot Topics
The most active discussions revolve around multi-agent and channel configuration complexities:
- **[#3301 – BUG: /clear and session auto-compression don't work in routed chats](https://github.com/sipeed/picoclaw/issues/3301)**: With 3 comments, this bug highlights a core pain point for users running multi-agent setups via dispatch rules. The related fix PR **#3316** is open, suggesting the issue is acknowledged and a solution is in progress.
- **[#3294 – [stale] /list models only shows current model](https://github.com/sipeed/picoclaw/issues/3294)**: Closed, but with 3 comments, this indicates confusion over the expected behavior of the `/list models` command, with users expecting a list of all configured models rather than just the active one.

### 5. Bugs & Stability
One new bug was reported, and one critical fix is pending review:

- **High – Inert Configuration (`#3328`)**: `line.settings.webhook_host` and `webhook_port` are documented and defaulted but never read, causing silent misconfiguration for LINE channel users. **Fix PR `#3329` exists** and is open.
- **High – Multi-Agent Context Loss (`#3301`)**: Chats routed to non-default agents lose history and skip auto-compression, degrading long-session performance and context. **Fix PR `#3316` exists** and is open.
- **Low – Command Misbehavior (`#3294`)**: The `/list models` command fails to meet user expectations by only showing the current model. This was closed, likely by a stale-bot, without a fix.

### 6. Feature Requests & Roadmap Signals
- **Feature: Native Exa Web Search Provider (`#3299`)**: This open PR adds a native `tools.web` provider for Exa, expanding the platform's search capabilities beyond current options. This is a likely candidate to be merged in the next version if the maintainers approve it.
- **Feature: Telegram Topics in Private Chats (`#3315`)**: Adds support for topic threads in private bot chats, an essential fix for users leveraging Telegram's organizational features for solo assistant use.
- **Feature: Prompt Cache Token Logging (`#3317`)**: A minor but useful observability feature to log cache tokens from providers like DeepSeek, helping developers debug cost and performance.

### 7. User Feedback Summary
User activity signals a growing adoption of **complex configurations** (multi-agent routing, channel-specific settings) that currently introduce stability and capability gaps. The most vocal dissatisfaction stems from **context management failures** in routed chats, effectively breaking core assistant memory features for advanced users. There is also evident **frustration with silent configuration failures** (like the LINE webhook issue) where documented settings have no effect. However, the rapid submission of high-quality fix PRs (e.g., `#3314`, `#3316`) demonstrates a strong, technically proficient community that is actively debugging and contributing back rather than just filing complaints.

### 8. Backlog Watch
The following items require maintainer attention and have an **open PR or high impact**:
- **`#3299` (PR – Exa support)**: Open since **July 26** (17 days) without updates, risking becoming stale.
- **`#3315` (PR – Telegram Topics)**: Open since **August 3** (9 days) with no comments or reviews.
- **`#3316` (PR – Routed Context Fix)**: Open since **August 3** (9 days), directly blocks the fix for the High-severity bug `#3301`. This should be prioritized.
- **`#3314` (PR – Shell Allow Fix)**: Open since **August 3** (9 days), addressing a security/funcionality regression.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-12

## Today's Overview

NanoClaw is in a high-velocity development phase, with **8 PRs updated in the last 24 hours** (3 closed/merged, 5 still active) but only **1 new issue** filed. The core team is focused on two major thrusts: **Agent Plugins 1.0.0** (a breaking migration of agent templates, PR #3220) and **remote Streamable HTTP MCP server support** across all providers (PRs #3092, #3221). The single open bug report — silent message drops due to platform message-ID reuse (#3226) — is a serious reliability concern that currently lacks an associated fix PR. No new releases were cut today. Overall, the project is healthy and actively shipping features, but the message-dropping bug and several long-stale open PRs warrant attention.

---

## Releases

**No new releases** were published in the last 24 hours. The most recent tagged release predates today's activity window.

---

## Project Progress

Three PRs were **closed/merged** in the last 24 hours:

- **#3221 — feat(providers): remote Streamable HTTP MCP servers for codex and opencode** (*core-team*, by amit-shafnir) — Closed. This extends the remote MCP server support (originally added for Claude in #3092) to the Codex and OpenCode providers. Previously, `{ type: 'http', url }` entries in `mcpServers` would throw at config-write time for these providers; this PR fixes that gap.

- **#3092 — feat: support remote Streamable HTTP MCP servers** (*core-team*, by amit-shafnir) — Closed. The foundational engine+Claude-provider change that teaches NanoClaw to accept remote Streamable HTTP MCP servers. This is a significant interoperability upgrade, enabling SaaS-hosted MCP tools rather than only local stdio processes.

- **#3190 — feat: add Tavily MCP tool skill** (by manisrinivasan2k1) — Closed. Adds the Tavily search API as a utility skill (standalone tool in `.claude/skills/`), giving agents a web-search capability out of the box.

**Active PRs still in progress** include the Agent Plugins 1.0.0 migration (#3220), transactional upgrade support (#3195), DB backfill migration for channel destinations (#3145), and the setup-wizard template flow (#2909).

---

## Community Hot Topics

The most active work items in the last 24 hours are all **core-team led**, with community contributions taking a back seat:

- **#3226 — Inbound messages silently dropped when a platform reuses a message id** (1 comment, open since Aug 10) — This is the only issue updated today and the highest-severity community-facing problem. The reporter, dweekly, describes a scenario where the agent appears to "ignore" the user with zero indication of failure. This is an active discussion thread worth watching.

- **#3220 — feat!: agent templates become Agent Plugins 1.0.0 directories** — A breaking-change PR that migrates the template format. While it has no comments yet, the `feat!` (breaking) marker and its scope (*stamp-time symlink/caps/secret hardening* plus a *format migration*) make it a high-impact change that the community will likely react to once merged.

**Underlying need analysis:** The MCP remote-server work (#3092, #3221) signals a strong push toward **cloud/SaaS MCP ecosystem compatibility** — a feature the broader MCP tooling community has been asking for across agents. The message-dropping issue (#3226) reflects a **reliability/trust gap**: users need guarantees that their messages are never silently lost, especially in production messaging channels.

---

## Bugs & Stability

Ranked by severity:

1. **🔴 HIGH — #3226: Inbound messages silently dropped on message-ID reuse** (open, no fix PR yet)  
   *Impact:* Users are silently ignored; no error surfaced; indistinguishable from "agent doesn't care." This could erode trust in the product for production use.  
   *Fix status:* **None attached.** This is the #1 thing maintainers should pick up.

2. **🟡 MEDIUM — #2134: Apple Silicon + Colima env vars missing from launchd plist** (open since Apr 29, still active)  
   *Impact:* On Apple Silicon Macs with Colima, NanoClaw-as-a-service may lack required env vars, causing failures at startup. A long-standing setup gap.  
   *Fix status:* PR itself is the fix; awaiting review/merge.

3. **🟡 MEDIUM — #3145: DB backfill for existing wirings lacking destinations** (open)  
   *Impact:* Existing messaging-group wirings may have null destinations post-migration; this could cause messages to not route.  
   *Fix status:* PR with migration 021 proposed; awaiting review.

4. **🟢 LOW — #3195: Transactional upgrades** (open)  
   *Impact:* Failed NanoClaw upgrades could leave the install in a partial/corrupt state. This is a quality-of-life stability improvement rather than an active bug.

---

## Feature Requests & Roadmap Signals

- **Remote Streamable HTTP MCP servers (merged)** — The most significant roadmap signal. NanoClaw now supports `{ type: 'http', url }` MCP servers across Claude, Codex, and OpenCode providers. Expect follow-up documentation and possibly a skills listing in the next release.

- **Agent Plugins 1.0.0 (in progress)** — The template-to-plugin migration (#3220) plus the setup-wizard flow (#2909) suggests the next minor release will include a **first-agent creation wizard** with template stamping. This is a UX milestone for onboarding.

- **Tavily MCP skill (merged)** — Adds web search as a supported tool; signals an appetite for richer utility skills. Look for more "agent-ready" search/retrieval skills in future versions.

- **Transactional upgrades (open PR)** — If merged, this becomes an important stability feature for anyone self-hosting NanoClaw.

**Prediction:** The next NanoClaw release will likely be a **minor version bump** that includes Agent Plugins 1.0.0 (breaking template format), the setup-wizard flow, and remote MCP server support. Users should watch for migration notes on the template format change.

---

## User Feedback Summary

- **Reliability anxiety (new):** The message-drop issue (#3226) highlights a core user pain point — *"the agent ignored me"* with no diagnosable cause. This is the strongest dissatisfaction signal in the last 24h.
- **Onboarding friction (long-standing):** The Apple Silicon/Colima issue (#2134) has been open since April, indicating a persistent setup pain for macOS users with Colima-based Docker runtimes.
- **Positive signal — MCP ecosystem:** The stream of MCP-related PRs (remote HTTP support, Tavily skill) suggests users want **more external tool integration, not fewer** — a healthy sign of adoption in the MCP ecosystem.
- **Data-integrity concerns:** The DB backfill PR (#3145) suggests users are hitting data-consistency issues after migrations — a subtle trust signal that migration paths need more hardening.

---

## Backlog Watch

These items need maintainer attention:

1. **#2134 — Apple Silicon + Colima launchd env vars** (open since **Apr 29**, ~3.5 months)  
   Longest-stale open PR. The fix is small and well-scoped; it has likely been deprioritized in favor of feature work. Community users on Apple Silicon with Colima are affected daily.

2. **#2909 — Setup wizard template flow** (open since Jul 2)  
   This is part 2 of 2 for the template feature. It has no comments and is awaiting review. Since its sibling PR (#3220) is actively being iterated, this could get swept up in the next review pass.

3. **#3145 — DB backfill migration 021** (open since Jul 28)  
   A migration that fixes existing data rather than adding features. If left unreviewed, users who upgrade past a certain point may have broken wirings with null destinations.

4. **#3195 — Transactional upgrades** (open since Aug 6)  
   A stability improvement that prevents partial/failed upgrades. Medium priority but important for self-hosted production users.

---

*Data source: NanoClaw GitHub repository (nanocoai/nanoclaw), activity window 2026-08-11 → 2026-08-12.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-12

## 1. Today's Overview

IronClaw is in a period of intense architectural consolidation, with 73 items updated in the last 24 hours (23 issues, 50 PRs) and a 50/50 split between merged/closed and open PRs. The project is squarely focused on the "Reborn" rearchitecture, with a cluster of tightly-related bug fixes and design proposals centered on the agent loop, context-window management, and durable storage. A notable pattern today is the **loop hardening wave**: multiple PRs and issues (##7484, #7485, #7486, #7487, #7488, #7490) all target defects in the agent-turn runner, indicating a systematic quality pass on core execution machinery. Alongside the bug fixing, two significant epics are in flight — pluggable agent loops via ACP (#7482) and a profile-agnostic durable-state migration (#7467) — and the project saw a burst of QA-bug closures (##7246, #7247, #7294), signaling that the Railway-hosted QA instance is driving verifiable fixes into stable. The overall health signal is strong: maintainers are closing issues at a high rate, accepting contributor PRs (two from new contributors today), and showing disciplined attention to both architectural debt and user-facing regressions.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The project remains on the v1.3.0 milestone for several open epics (#7405, #6879, #7038), suggesting that next release will carry the deferred-tool discovery improvements, automation-reliability fixes, and the WebUI design-system work currently in flight.

---

## 3. Project Progress

Ten PRs were merged or closed today, revealing a mix of core-runtime fixes and user-facing corrections:

**Core Loop & Context Fixes (merged):**
- **#7503** — `fix(loop): retain accepted task across context eviction` — Pins the user task message across the 128-message tail cut and token budget; fails with `BudgetExceeded` rather than silently dropping oversized tasks. Closes #7484.
- **#7471** — `fix(processes): lease expiry recovers safe runs instead of failing them` — Isolates journal heartbeats from data-plane PostgreSQL, recovers expired runs only at replay-safe checkpoints, and fences stale executors.

**LLM & Caching (merged):**
- **#6997** — `feat(llm): explicit Anthropic cache_control breakpoints on both transports` — Closes P0 #1 of the pi-harness adoption program (#6984). Both rig/API-key and OAuth transports now place explicit breakpoints instead of relying solely on automatic caching.

**Channels & Platform (merged):**
- **#7514** — `fix: enable Railway shell for hosted volume profile` — Adds a strict release-only toggle for the hosted-single-tenant-volume profile while preserving storage paths.
- **#7470** — `fix(threads): restore listability for unprojected thread index rows` — Threads with durable rows but no ordered-projection metadata were invisible in `list_threads`; now restored.

**WebUI & QA (merged/closed):**
- **#7480** — `fix(webui): reveal long conversation titles on hover` — A new overflow-aware `MarqueeText` component animates titles on hover (closes #7481).
- **#7483** — `Fix default NEAR AI connection and model probes` — Default provider dialog now authenticates via the runtime session instead of failing on blank API keys.
- **#7488** — `fix(disclosure): bridge tools hardcoded Exclusive serialize discovery batches` — Discovery metadata lookups (`tool_search`, `tool_describe`) no longer serialize behind each other.
- **#7487** — `fix(disclosure): tool_search marks tools disclosed without returning schemas` — Restores the describe-first safety net and fixes the `oneOf` required-field collapse.
- **#7511** — `[Ignore]` (closed as invalid).

**Notably:** Three long-running QA bugs were closed today: **#7246** (agent hallucinates automation status), **#7247** (falsely claims GitHub connected), and **#7294** (incorrectly remembers a Telegram routine from another scope). These all trace to the same underlying class — agent misrepresenting state without checking — and their closure suggests the state-verification hardening is landing.

---

## 4. Community Hot Topics

**Most commented issues today:**

1. **#7482 — Epic: Pluggable agent loops — ACP executor, edge credential injection, kernel architecture** (3 comments) — This epic repositions IronClaw as the "kernel" (scheduling, tenancy, secrets mediation, egress boundary, audit) and delegates the agent loop and per-integration tool code to off-the-shelf ACP agents. The architectural direction is a major bet; the activity reflects real debate about scope and sequencing.

2. **#7317 — Proposal: Doc-Truth Verification Pipeline** (3 comments, **closed**) — Community proposal to add a CI gate ensuring docs match code after breaking changes, motivated by `origin_gate_matrix` shipping without documentation. The closure implies maintainers accepted or are acting on the idea.

3. **#7405 — Improve deferred tool discovery with complete signatures and namespace-aware catalog previews** (2 comments, **closed**) — Performance-focused enhancement to reduce model turns at large tool counts, closed today with the merge of the disclosure-discipline fixes.

4. **#7484 — fix(loop): context window silently evicts the task** (1 comment) — This is the bug behind user-visible "lost task" behavior; the fix (#7503) merged the same day, demonstrating strong issue-to-PR velocity.

**Underlying needs:** The dominant thread is **context-window integrity and model reliability** — the community is pushing hard on making the agent loop predictable: no silent evictions, no dead code in retry logic, no double-counted tokens, no false "no-progress" escapes. The second thread is **automation trustworthiness** — QA bugs about agents claiming actions they didn't take point to a demand for honest state-checking before claims. The doc-truth proposal (#7317) reflects frustration with breaking changes landing without documentation, a stability concern as the project accelerates.

---

## 5. Bugs & Stability

Ranked by severity:

**High — Context-Window Data Loss (fixes merged):**
- **#7484** — The 128-message clamp silently evicted the accepted task; fixed by **#7503** (pin task) and **#7504** (open, compact-on-eviction instead of silent loss).
- **#7485** — Token estimator double-counts ASCII, halving effective context window; two inconsistent estimators in play. Fix not yet merged.
- **#7486** — Typed no-progress escape false-positives on idempotent reads/polling; kills legitimately long runs. Design trade-off between output-hash-based `NoChange` and real stalls; fix not yet merged.

**High — Security/Delivery Integrity:**
- **#7476** — `classify_delivery_outcome` ignores `vendor_message_refs` on `Failed`, hiding partial-send evidence from the model. Companion to #7475 (notices) — this current gap leaves the model blind to "some messages sent, some failed," a compliance-relevant blind spot.

**Medium — Faulty Retry and Recovery Logic:**
- **#7490** — `retry_disposition()` is dead code; ~25 transient categories classified but never wired to drive silent redrive. Either wire it or retire it — open.
- **#7488/#7487** — Disclosure bridge tools serialized unnecessarily and disarmed the describe-first safety net; **both fixed and merged** today.

**Medium — Cross-Provider Contract Inconsistency (fix PR open):**
- **#7505** — Memory target aliases resolved only in the native provider; mem0 stores `target: "memory"` verbatim so canonical reads fail. **#7512** (open) moves resolution to the domain contract layer.

**Low — UX/Platform:**
- **#7508** — GitHub MCP extension startup shows confusing endpoint-verification prompt instead of connecting cleanly (QA bug).
- **#7489** — `result_read` 24 KiB preview ceiling plus read-before-edit gate creates a 2000-line uneditable wall; tracking issue awaiting #7435 OMP cutover.

**Overall stability assessment:** The loop-hardening wave is the right investment at the right time — the three "context window" bugs (#7484, #7485, #7486) would each cause user-visible failures (lost tasks, halved context, terminated long runs). Two of the high-severity items already have merged or open PRs, which is a healthy signal.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals for v1.3.0:**

- **Pluggable agent loops via ACP (#7482, epic)** — The most architectural item on the board. If this lands, IronClaw becomes a kernel with interchangeable ACP agents as loops, and per-integration tool code is externalized. The PR **#7513** (ACP serve command with streaming + cancel, from a new contributor) is a concrete first step and signals the ACP path is being exercised now.
- **Automation suggestion cards V1 backend (#7038 backlog, PR #7498 open)** — A narrow "suggestion generation" loop producing home-screen automation cards, exposed via new WebUI endpoints. This is user-facing growth of the automation surface.
- **Unified channel model (#7477, open, XL)** — One `ChannelAdapter` per channel (web-app, Slack, Telegram) for inbound, replies, and notifications. Design spec implemented end-to-end with enforcement; a major plumbing simplification.
- **Slack/Telegram linked-device support (#7464, #7515, open)** — Telegram linked-device auth with session custody (visible/revocable in Telegram settings) plus 8 new core Slack ops (edit, delete, reactions, open_dm, resolve_user). Channel parity is clearly a v1.3 target.
- **IdentyClaw Passport host-mediated helper (#7496)** — Practitioner request for a builtin IDCP flow since processless profiles hide `builtin.shell`; small but signals demand for identity integration.
- **WebUI Design System epic (#7038)** — Storybook + AI-first design system with a full proposal package; PR #7498 (suggestion cards) is the first backend slice to land.

**Prediction for next release:** The combination of merged fixes (#7503, #7471) and open feature PRs tagged for v1.3.0 (#7498, #7477, #7464) strongly suggests the next minor release will include: **context-window compaction**, **unified channel model**, **Telegram linked-device**, and **automation suggestion cards** — plus the long-awaited **explicit Anthropic caching** (#6997) as a performance win.

---

## 7. User Feedback Summary

**Real pain points surfacing from QA and community issues:**

- **Agent hallucination of state (critical trust issue):** Three QA bugs closed today (##7246, #7247, #7294) all involve the agent confidently claiming an action or connection exists without verifying. Users see "you already have this set up!" when nothing exists, or "GitHub is connected" then a failed GitHub call. This is a trust-eroding pattern that the describe-first and state-verification fixes are directly addressing.
- **Context loss on long conversations:** "The same stored prompt sometimes succeeds and sometimes produces nothing useful" (#6879, automation runs) and the silent 128-message eviction (#7484) both frustrate users on small models (DeepSeek V4 Flash) — a structural, not random, reliability gap.
- **Cross-scope memory leakage:** #7294 (Telegram routine from another thread) and #7505 (target alias mismatch between native and mem0) point to memory being both too loose (wrong thread recall) and too broken (canonical reads fail) depending on the provider.
- **Configuration friction:** #7508 (confusing GitHub MCP startup) and #7483 (provider dialog fails on blank API key) are onboarding friction; #7483 already fixed.
- **Deployment profile fragility:** #7467 (profile-agnostic durable state, epic) reflects real user pain — changing profiles makes existing data appear gone. PR #7456 (open) is the fix.
- **Documentation drift:** #7317 (doc-truth pipeline) was closed, indicating maintainers engaged with the complaint about unreported breaking changes.

**Satisfaction signals:** The velocity of QA-bug closures (10 closed issues today) and quick turnaround on contributor PRs (#7513 from a new contributor, #7516 from neo-sky) is a positive community signal.

---

## 8. Backlog Watch

**Items needing maintainer attention:**

- **#6879 (OPEN, epic, v1.3.0, created 2026-07-29, 0 comments from maintainers)** — "Automation runs are hit-or-miss: unattended runs execute as plain interactive chat turns" — This epic has sat untouched for ~2 weeks despite being a P0-class reliability issue for unattended operation. The 0-comment state suggests it's under-resourced; #7482's kernel/ACP direction may absorb it, but a triage note would help.
- **#5910 (OPEN, PR, created 2026-07-10, bot-authored)** — `fix: hydrate approval gates on notification open` — Over a month old, XL-sized, from `ironloopai[bot]`. Addresses a real UX gap (approval gates not delivered through the subscription path). Stale and needs review or explicit deferral.
- **#7489 (OPEN, tracking, scope: tool/builtin)** — Result-read preview ceiling (24 KiB) and the 2000-line uneditable wall: explicitly deferred to #7435 (OMP cutover), but that dependency is not linked with a status update. Worth an owner to track.
- **#7490 (OPEN, bug, scope: agent)** — `retry_disposition()` dead code: a decision (wire or retire) is overdue — dead code in a reliability-critical path is a liability.
- **#7486 (OPEN, bug, scope: agent)** — No-progress false-positives on idempotent ops: design trade-off, but long-running legitimate tasks are being terminated today. Needs a maintainer decision on the output-hash heuristic.

**Watch item:** **#7482 (Epic, pluggable agent loops)** — This is the highest-leverage architectural decision on the board; the 3 comments suggest active debate, but the epic touches tenancy, secrets, egress, and audit. Given that PR #7513 (ACP serve) is already open, the ecosystem is ahead of the design — a comment thread on sequencing would reduce integration risk.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-12

## 1. Today's Overview

LobsterAI (github.com/netease-youdao/LobsterAI) is in an active release cycle. A new version **2026.8.11** was published, featuring several Cowork usability improvements including a collapse-agent-tasks shortcut and scheduled task session markers. The day saw 10 PRs updated (7 merged/closed, 3 open) and 4 issues updated (3 closed, 1 open), indicating healthy maintenance momentum. Key fixes merged today address Escape-key modal overlay handling, per-model thinking level configuration (bug fix), and a right-click context menu for local file links in Cowork. One long-standing dependency update PR for the Electron group remains open and is over four months old, signaling potential maintenance drag.

## 2. Releases

- **LobsterAI 2026.8.11** (published 2026-08-11) — [Release notes](https://github.com/netease-youdao/LobsterAI/releases/tag/2026.8.11)
  - **feat(cowork): collapse-agent-tasks shortcut** — Adds keyboard shortcut to collapse/expand agent tasks within Cowork sessions.
  - **feat(cowork): allow modifier shortcuts while typing** — Users can now trigger shortcuts even when focus is inside an input field, with IME composition handled safely.
  - **feat(cowork): mark scheduled task sessions in sidebar** — Scheduled/running tasks are now visually distinguished in the sidebar, improving session status clarity.
  - No breaking changes or migration notes were reported.

## 3. Project Progress

Merged/closed PRs today (7 total) — [Full list](https://github.com/netease-youdao/LobsterAI/pulls?q=is%3Apr+updated%3A2026-08-11..2026-08-12+is%3Aclosed)

| PR | Title | Area | Insight |
|----|-------|------|---------|
| [#2477](https://github.com/netease-youdao/LobsterAI/pull/2477) | **Release/2026.8.10** (merged) | All areas | Merge of release branch into main: configurable model thinking levels, Cowork progress visibility, scheduled task identification, local-file workflows, startup/runtime reliability, settings interactions. |
| [#2476](https://github.com/netease-youdao/LobsterAI/pull/2476) | **feat(ui): dismiss topmost overlay on Escape** (merged) | renderer/im | Fixes nested-modal Escape handling: modal portals into body, a layer-id based system ensures only the newest overlay reacts. |
| [#2475](https://github.com/netease-youdao/LobsterAI/pull/2475) | **[OPEN] fix(model-selector): per-model thinking level** | renderer | **Bug fix (not merged yet)**: thinking-level selection was global, not per-model; Pro and Flash models clobbered each other's settings. Adds per-model persistence. |
| [#2457](https://github.com/netease-youdao/LobsterAI/pull/2457) | **feat(models): configurable thinking levels** (merged) | models | Server-driven thinking-level options and defaults, OpenClaw alias mapping (`max` → `xhigh`), per-session/per-agent persistence, versioned model request options. |
| [#2473](https://github.com/netease-youdao/LobsterAI/pull/2473) | **feat(cowork): right-click context menu for local file links** (merged) | cowork/artifacts | New LocalFileContextMenu: open-with, save-as, copy-path/contents/image, reveal-in-folder; adds a `dialog:saveFileCopy` IPC handler. |
| [#2474](https://github.com/netease-youdao/LobsterAI/pull/2474) | **fix(sidebar): align sites icon stroke weight** (merged) | renderer | Small visual polish. |
| [#1241](https://github.com/netease-youdao/LobsterAI/pull/1241) | **feat(settings): unsaved-changes confirmation** (merged, stale-closed) | settings | Closes issue #1237: dirty-check on providers snapshot, intercepts background/X/Cancel close paths. |
| [#1239](https://github.com/netease-youdao/LobsterAI/pull/1239) | **feat(main): taskbar/Dock flash on AI task completion** (merged, stale-closed) | main | Windows `flashFrame`, macOS `dock.bounce`, Linux no-op. |

## 4. Community Hot Topics

The most active discussion item today is **Issue #1237** (Settings unsaved-changes confirmation, 2 comments, closed via PR #1241) — the core need was to prevent silent loss of API Key and provider configuration. This was resolved by adding a confirm-before-close dialog with dirty detection.

**Issue #1240** (model lockout cascade) — a user on a burned-out quota (volcano engine coding plan) found that **all** brokers report "API 受限" even after switching to other agents (gemini 3 flash, gemini 3.1 pro preview). After restart the app wouldn't boot, and even restoring an older `openclaw.json` left the model state restricted, while the same API was healthy on another machine. This points to a **global rate-limit state not being reset per-provider**, and a health-check or fallback mechanism is clearly missing. This is the highest-signal stability complaint today, and the maintainer hasn't responded yet in the thread.

[#1183](https://github.com/netease-youdao/LobsterAI/issues/1183) (open, stale) — a Windows user reports a recurring overlay "OpenClaw gateway failed to start" loop after toggling a model off and saving. This has been sitting unanswered since 2026-04-01 and was revisited today without reply.

## 5. Bugs & Stability

| Severity | Issue/PR | Description | Status |
|----------|----------|-------------|--------|
| **High** | [#1240](https://github.com/netease-youdao/LobsterAI/issues/1240) (closed-stale) | **Global model lockout**: once one provider hits quota, *all* providers fail (even gemini), app unusable after restart; the API is fine on other machines. Strong evidence of a shared broken state, not user-side. | No maintainer reply; closed as stale. **Needs reopening / investigation.** |
| **Medium** | [#2475](https://github.com/netease-youdao/LobsterAI/pull/2475) (open) | Thinking-level is a **global setting**, so switching between Pro and Flash models overwrites the other's choice. A concrete regression from the new thinking-level feature. | Fix PR proposed by maintainer, not yet merged. |
| **Medium** | [#2062](https://github.com/netease-youdao/LobsterAI/issues/2062) (closed-stale) | **24h task timeout**: "Task timed out" after max duration — unclear to user whether the job continued in background. No "continue" flow defined. | No maintainer response; closed as stale. |
| **Low** | [#2476](https://github.com/netease-youdao/LobsterAI/pull/2476) (merged) | Nested overlays ignoring second Escape press — fixed. | Resolved. |
| **Low** | [#2474](https://github.com/netease-youdao/LobsterAI/pull/2474) (merged) | Icon stroke misalignment in sidebar — fixed. | Resolved. |

## 6. Feature Requests & Roadmap Signals

- **Per-model thinking levels** ([#2475](https://github.com/netease-youdao/LobsterAI/pull/2475)) — the natural evolution of the global setting introduced in 2026.8.10; the fix is already drafted, so per-model persistence should land in the next patch release.
- **Local-file workflow richness** — the new right-click context menu ([#2473](https://github.com/netease-youdao/LobsterAI/pull/2473)) with open-with, copy-image, reveal-in-folder suggests the team is actively building out the artifacts/local-files experience. Expect right-click support to extend beyond local links (e.g., across session artifacts), and possibly a file-manager view.
- **Unsaved-changes confirmation** ([#1241](https://github.com/netease-youdao/LobsterAI/pull/1241)) — the dirty-check pattern will likely be reapplied to other dialogs (e.g., Agent config, model settings) as the settings surface grows.
- **Taskbar/Dock flash** ([#1239](https://github.com/netease-youdao/LobsterAI/pull/1239)) — a long-requested UX nicety; after merging, expect companion features like notification toasts or unread counts in the taskbar.
- **24h continuous task support** ([#2062](https://github.com/netease-youdao/LobsterAI/issues/2062)) — user demand is clear; a "continue after timeout" flow is likely in design, or at least better wording/semantics on the timeout dialog (distinguish "stopped" vs "still running").

## 7. User Feedback Summary

- **Configuration safety** — users repeatedly lose API Key edits due to silent close (issue #1237). The fix PR (#1241) addresses the exact repro path; users will be satisfied once released.
- **Provider lockout fatalism** — issue #1240 user describes a scenario where one provider's quota burn makes the **whole app unhealthy**, and restarting makes it worse ("cannot start after restart"). This is a strong negative signal: no failover, no per-provider state isolation, no user-facing recovery path.
- **Cold-start / long-task UX** — the 24h timeout user (#2062) is confused about whether their task continued; long-running task semantics need explicit UI.
- **Gateway startup flakiness (Windows)** — #1183 shows users hitting a repeated "openClaw gateway failed" overlay loop after a small config toggle; this suggests either a non-idempotent save path or a gateway restart race.

Overall: users are clearly power-users (multi-provider, multi-agent, long-running tasks) and are pushing against walls in provider state isolation and background task visibility.

## 8. Backlog Watch

- **Issue #1183** — [OpenClaw gateway failed loop on Windows](https://github.com/netease-youdao/LobsterAI/issues/1183): open since 2026-04-01, zero maintainer responses; users are blocked from using the app entirely. High priority to at least triage with a reproducible-env request.
- **Issue #1240** — [Global provider lockout after quota](https://github.com/netease-youdao/LobsterAI/issues/1240): closed as stale without a maintainer response; this is a serious architectural bug — a misfiring might reappear in other users' hands.
- **PR #1277** — [Dependabot electron bump (40→43)](https://github.com/netease-youdao/LobsterAI/pull/1277): open 4+ months; Electron 43 brings security fixes and Windows/macOS compatibility improvements. Accumulating drift in the Electron stack is a future maintenance risk.
- **PR #1181** — [Hide OpenClaw main agent session from session list](https://github.com/netease-youdao/LobsterAI/pull/1181): open since April, no maintainer review; the proposed `hidden` column is a small schema addition but the logic touches the core cowork/session query layer, hence longer review queue. Notably, the 2026.8.11 release already contains "mark scheduled task sessions in sidebar", which overlaps with session-list semantics — this PR should be revisited in that light.

---

**Overall health**: The project is shipping steadily with a clear focus on Cowork UX (keyboard, sidebar, context menus) and settings safety. The main risks are (a) the unaddressed provider-lockout bug (#1240), (b) Windows gateway startup flakiness (#1183), and (c) the long-stale dependency-update PR. Maintainer response to user issues is inconsistent, with several closed-stale without any comment — a process improvement opportunity.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest
**Date:** 2026-08-12

---

## 1. Today's Overview

Moltis is showing steady, low-volume development activity today. There are **2 open pull requests** being actively updated, while no issues were modified or closed in the last 24 hours. No new releases are currently available, indicating the project is in a development/build phase rather than a distribution phase. The most significant activity centers on **#1190**, a large feature PR adding durable local CalDAV connectors, which signals continued investment in offline-first and local data capabilities. The second PR marks a subtle but important UX fix for session management. Overall, the project appears healthy but is operating on a relatively quiet cycle with no critical bugs or user-facing regressions reported.

---

## 2. Releases

**None.** No new releases, tags, or version bumps were published in the last 24 hours. No changelog, migration notes, or breaking-change documentation to report.

---

## 3. Project Progress

**Merged/Closed PRs today:** None.

**PRs actively advancing (open, updated in last 24h):**

- **[PR #1190 – Add durable local CalDAV connectors](https://github.com/moltis-org/moltis/pull/1190)** (Author: penso, updated 2026-08-11)
  - Major feature addition covering: provider-neutral connector persistence, atomic CalDAV snapshots, scheduling, projections, bounded local full-text search, prompt-compiled dataset plans, and a trusted read-only `connectors` agent tool.
  - This represents significant architectural work — moving toward local-first data access with AI-agent integration.

- **[PR #1182 – fix(sessions): allow deleting and archiving the main session](https://github.com/moltis-org/moltis/pull/1182)** (Author: shixi-li, updated 2026-08-11)
  - Fixes issue #1132 by removing the `main` session guard in `delete_impl` and `is_archivable_entry` in the gateway layer.
  - Behavioral nuance preserved: the current-active-channel-session archive restriction remains, and `sessions.clear_all` still protects main/channel-bound sessions.
  - This is a targeted bugfix/UX improvement making session management more consistent.

---

## 4. Community Hot Topics

No issues were active today, and the two open PRs each have **zero comments and zero reactions**, indicating minimal community engagement or discussion on these items at present.

**Active items (limited interaction):**

- **[PR #1190](https://github.com/moltis-org/moltis/pull/1190)** – While currently without discussion, this PR's scope (durable connectors, local search, agent tooling) touches on several underlying needs: offline data access, data sovereignty, and AI-assistant memory/persistence. It is likely to generate review discussion shortly given its size.

- **[PR #1182](https://github.com/moltis-org/moltis/pull/1182)** – Addresses a user-reported session management issue (#1132). Low complexity, expected to merge soon.

**Observation:** The lack of comment activity suggests either (a) these PRs are very fresh and under review, or (b) the community is currently in a quieter period. Either way, no heated debates, design controversies, or community friction points are visible today.

---

## 5. Bugs & Stability

**New bugs reported today:** 0

**Known issues with active fixes:**

- **Session deletion/archiving restriction for the `main` session** — Reported in issue **[#1132](https://github.com/moltis-org/moltis/issues/1132)** (pre-existing, referenced by PR #1182).
  - **Severity:** Medium (workflow annoyance, not a crash/data-loss bug).
  - **Fix status:** PR #1182 is open and addresses the root cause; pending review/merge.

**No crashes, regressions, or critical stability concerns were reported in the past 24 hours.** Overall stability appears solid.

---

## 6. Feature Requests & Roadmap Signals

While no formal feature-request issues were filed in the last 24 hours, the open PRs provide clear roadmap signals:

- **Local-first data & connectors (from PR #1190):** The project is actively implementing durable, provider-neutral local connectors with CalDAV support, atomic snapshots, scheduling, and bounded full-text search. This strongly suggests the project is prioritizing **offline capability, data ownership, and local intelligence** as a core product pillar — not just a wrapper around remote services.

- **AI agent tooling (from PR #1190):** The addition of a trusted read-only `connectors` agent tool indicates a push toward allowing AI agents to natively query and use local datasets. This points to a roadmap where Moltis acts as a **personal data substrate for AI agents**.

- **Session management UX (from PR #1182):** A quiet but consistent theme — treating the `main` session like any other session, reducing special-casing, and improving user control over their data/chat history.

**Prediction for next version:** Expect the next release to include durable local connector support, improved session management, and possibly the first iteration of agent-accessible local data tools.

---

## 7. User Feedback Summary

Direct user feedback in the last 24 hours is minimal (no issue comments, no reactions). However, indirect signals from the PRs indicate:

- **Pain point addressed:** Users being unable to delete/archive the default `main` session (issue #1132) — a control/privacy concern. Users want full ownership over their session data, including the default one.
- **Use cases emerging:** Local/offline data access with CalDAV connectivity, and enabling AI assistants to query user data locally — indicating real-world use cases around **personal information management** and **AI memory**.
- **Satisfaction indicators:** No negative feedback or bug rants visible today, and the pace of feature development (local connectors, agent tools) suggests the maintainers are aligned with user demand for privacy-respecting, local-first AI tooling.

Overall: Low noise, high signal. The community appears functional, and the work underway matches likely user desires.

---

## 8. Backlog Watch

**Items requiring maintainer attention:**

- **[Issue #1132](https://github.com/moltis-org/moltis/issues/1132) — main session cannot be deleted/archived.**
  - Open since before Aug 1, 2026. Fix PR #1182 has been open since Aug 1 and was updated Aug 11. **Needs maintainer review and merge** to close this out.

- **[PR #1190 — Durable local CalDAV connectors.**
  - Large scope, fresh (created Aug 11). **Needs timely maintainer review** to prevent it from going stale, given its size and cross-cutting nature (gateway, scheduling, storage, agent tooling).

- **[PR #1182 — Session management fix.**
  - Small, targeted, low-risk. Should be prioritized for merge to clear the backlog and address the user-reported issue.

**No long-dormant issues or abandoned PRs were identified** in the current data window. The backlog is minimal and manageable.

---

### Summary Assessment

| Dimension | Status |
|---|---|
| Project activity | Low but purposeful |
| Release cadence | Paused (no releases in window) |
| Bug severity | Low (no critical issues) |
| Community engagement | Quiet (no comments/reactions) |
| Roadmap clarity | Strong (local-first + agent tooling) |
| Backlog health | Healthy (minimal, actionable items) |

**Overall health: Good.** The project is building toward meaningful local-first and AI-agent capabilities, handling regressions quickly, and keeping the backlog lean. The main action item is maintaining momentum on PR #1190's review cycle.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-12

## 1. Today's Overview
CoPaw (QwenPaw) is in an active release cycle with **v2.1.0-beta.3** published today, accompanied by a surge of stabilization work: 49 PRs were updated in the last 24 hours (25 merged/closed) and 23 issues were touched (14 closed). The maintainers are prioritizing bug fixes around MCP reliability, LaTeX rendering, memory/context lifecycle, and cross-UI consistency, while also advancing forward-looking features like marketplace unification, AnySearch integration, and Computer Use improvements. Notably, both a security concern (silent cron/plugin injection, #6916) and a performance bug (idle CPU at ~20%, #6828) were actively discussed and addressed. Overall, the project shows high velocity with a healthy mix of community contributions, first-time contributors, and core team commits.

## 2. Releases
**v2.1.0-beta.3** — released 2026-08-11

Key changes in this beta:
- **Feature**: Files workspace blog (#6783)
- **Fix**: Stale capability cache entries are now expired and cleared on model switch (#6723)
- **Chore**: Version bumped to 2.x line

No explicit breaking changes or migration steps were communicated for this release. Users on v2.0.1 or earlier betas should monitor for the known issues below, particularly the MCP tool失效 bug (#6732) and crashes (#6919), which have been reported on v2.0.1 and v2.1.0b2 respectively.

## 3. Project Progress
Notable merged/closed PRs in the last 24h:

- **#6898** — *fix(tools): correct read_file tool description*: Tool description now matches actual behavior with text-only support; avoids QwenPaw-9B misusing it for binary files.
- **#6915** — *fix(files): repair previews and dark mode styling*: Fixed Unicode PDF/SVG preview failures, RFC 5987 filename encoding, and aligned previews with dark theme.
- **#6911** — *feat(console): unify renderable code block experience*: Unified fenced code blocks with syntax highlighting, LaTeX/Mermaid Preview/Source tabs, and theme-aware rendering.
- **#6909** — *feat(channels): warn when a bot is already used by another agent*: Advisory conflict check before enabling a channel with a bot identity in use elsewhere.
- **#6875** — *chore: update release notes for v2.1.0*: Bilingual (EN/CN) release notes, News entry for 2026-08-12, and refreshed README translations.
- **#6564** — *fix(memory): flush pending turns before compression*: Fixes #6555, ensuring auto-memory persistence is not gated on `summarize_when_compact`.
- **#6891** — *feat(computer-use): improve native input workflows*: Bounded keyboard-only sequence action with rate limiting and refreshed observations.

## 4. Community Hot Topics
- **#6732** — [CLOSED] *MCP 工具规律性失效* (MCP tools periodically fail) — 10 comments, reported by 70995781. User on v2.0.1 observed MCP tools becoming unavailable after hours, requiring a Docker container restart. The issue was closed, but no explicit root cause was documented in the summary; a related PR (#6874, configurable MCP timeout) suggests the fix direction.
- **#6893** — [CLOSED] *公式渲染问题；会话分组管理；活动会话背景* — 7 comments, reported by renzhong424. A feature bundle request: LaTeX formula rendering in chat (e.g., `$Var(\hat{X}) = ...$` renders as raw text), chat session grouping, and an active-session background. The formula part was addressed by #6911 (unified code block experience).
- **#6882** — [OPEN] *怎么集成 CopilotKit* — 3 comments, reported by taohongxiu. User asks for guidance/examples on integrating CopilotKit with QwenPaw; remains unanswered.

## 5. Bugs & Stability
**High severity:**
- **#6919** — [OPEN] *qwenpaw-v2.0.1 frequent crashes* (console channel, `console process/reply failed` Traceback) — v2.0.1 pip install on Windows with web UI. No fix PR yet.
- **#6885** — [OPEN] *Console UI crashes on Chinese IME compositionEnd during agent run* — v2.1.0b2; message queue becomes unusable with Chinese IME during agent execution. No fix PR yet.
- **#6916** — [OPEN] *Security: Plugins can silently create cron jobs and inject user-visible messages without approval* — v2.1.0b3; plugin installation can persist scheduled actions and inject user-visible messages without consent. No fix PR yet.
- **#6697** — [CLOSED] *v2.1.0b1 desktop injects PYTHONHOME into child env → every python subprocess crashes* — Windows-specific, closed presumably with a fix.

**Medium severity:**
- **#6918** — [OPEN] *Inter-agent messages spawn a new agent session per message* — concurrent "shadow instances" cause duplicate data; reported by an agent-authored issue (#6918).
- **#6871** — [CLOSED] *Frontend historical message timestamps shifted by +8h* — timezone rendering bug after view re-rendering.
- **#6828** — [CLOSED] *Console frontend at idle keeps repainting (~20% CPU)* — caused by infinite CSS animations (`ai-copilot-blink` + antd spinner); likely fixed, but not in the same release notes.
- **#6883** — [OPEN] *日记页面子文件夹内笔记分组到错误日期* (Daily page groups notes under wrong date) — v2.1.0b2+; no fix PR yet.

## 6. Feature Requests & Roadmap Signals
Strong candidates for the next version (likely v2.1.0 final or v2.1.1):

- **LaTeX/KaTeX rendering** (#6893, #5453, #4756) — multiple duplicate requests; #6911 (unified code block experience) is a direct response.
- **Inbox delivery for agent reports** (#6917) — agent should be able to push structured reports into a persistent Inbox with unread indicators, not just chat scroll.
- **Workspace isolation** (#6900) — separate agent internal workspaces from chat project directories; each chat gets its own project directory.
- **CopilotKit integration guidance** (#6882) — user request with no maintainer response yet.
- **QQ/WeChat community channels** (#6895, #6897) — user requests for a WeChat group and QQ bot throttling improvements (avoid sending every workflow step to QQ).

## 7. User Feedback Summary
Reported pain points this cycle:
- **MCP instability** (#6732) and **crashes on Windows/pip** (#6919) are the strongest dissatisfaction signals from production users.
- **LaTeX rendering** is a recurring complaint (#6893, #5453, #4756) — users expect standard Markdown math to render correctly in chat.
- **Performance at idle** (#6828) — users notice ~20% CPU burn, causing UI jank.
- **Chinese IME compatibility** (#6885) — a critical usability gap for native Chinese users.
- **Desktop UX** — font size adjustment (#4154) and window geometry persistence (#6877) are being addressed or already implemented.
- Users show positive engagement with feature requests (session grouping, active-session background, file uploads) and appreciate improvements like the unified marketplace (#6880) and web search integration (#6817).

## 8. Backlog Watch
Issues/PRs needing maintainer attention:
- **#6882** — *CopilotKit integration* — no response from maintainers for 2 days.
- **#6916** — *Plugin permission/security gap* — high-severity security concern with no fix or comment from maintainers in the last 24h.
- **#6918** — *Inter-agent session duplication bug* — actively discussed with no fix PR yet.
- **#6779** — *refactor(context): align Scroll and memory with AgentScope lifecycle* — a substantial refactor (open for 5 days) with multiple related memory PRs (#6830, #6564); needs careful review and consolidation.
- **#5869** — *feat(console, tui): expose system commands in slash autocomplete* — open for over a month, under review, no merge yet.
- **#5490** — *navigable fullscreen image gallery for chat media* — open since June 24; stalled with no recent updates from maintainers.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-12

## 1. Today's Overview

ZeroClaw shows intense but healthy activity: 50 issues and 50 PRs updated in the last 24 hours. The project is in a heavy **RFC and standardization phase**, with nine open RFCs under maintainer review across security, architecture, and tooling domains. Maintainer attention is the critical bottleneck, as evidenced by 15+ items flagged `needs-maintainer-review` or `needs-author-action`. Security hardening is a dominant theme, with three new `priority:p1` security bugs filed in the last three days (WebP decompression, filesystem sandbox escape, and WebAuthn validation). Community engagement is substantial, with top issues drawing 13–19 comments each. **No new releases** were published this period.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

**Merged/Closed PRs (2):**

- [#9932 — ci(codeql): drop rust/hard-coded-cryptographic-value](https://github.com/zeroclaw-labs/zeroclaw/pull/9932) — Merged. Removes a CodeQL query that produced 27 false-positive "critical" alerts, all inside `cfg(test)` code.

**Notable Open PRs with Recent Commits (likely to merge soon):**

- [#9885 — fix(sop): honour the documented sops_dir default in the daemon](https://github.com/zeroclaw-labs/zeroclaw/pull/9885) — Small fix ensuring SOP directory defaults are consistently applied.

- [#9841 — fix(sop): drive headless SOP runs, and close five defects from review](https://github.com/zeroclaw-labs/zeroclaw/pull/9841) — XL-sized fix continuing a community-maintainer handoff chain; carries four prior commits unchanged.

- [#9862 — fix(tools): bound direct HTTP response handling](https://github.com/zeroclaw-labs/zeroclaw/pull/9862) — L-sized security fix streaming HTTP responses instead of buffering, plus preventing redirect-following on authenticated requests.

Key features actively maturing: **SOP (Standard Operating Procedure) control plane**, **plugin config validation**, **PowerShell native shell support on Windows**, **WhatsApp Web approval flows**, and **observability integrations**.

---

## 4. Community Hot Topics

**Most Active Issues (by comment count):**

1. [#8303 — RFC: Goal mode v1 — bounded foreground Matrix work](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) — 19 comments. A fundamental control-plane proposal for durable multi-turn objectives.

2. [#8603 — RFC: ZeroClaw Chat Completions profile](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) — 18 comments. High interest from the ecosystem (Open WebUI, LobeChat, Continue.dev, LangChain); addressable market expansion.

3. [#7155 — RFC: Per-execution confirmation tier for high-risk shell commands + policy](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) — 17 comments. Reaches toward Claude Code-style `allow/ask/deny` patterns; maintained through 3 revisions with maintainer scope narrowing.

4. [#7141 — RFC: Pluggable inbound authentication and canonical principals](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) — 14 comments. At Rev 8; deep OIDC and principal-model work.

5. [#2269 — RFI: Token consumption and cost management](https://github.com/zeroclaw-labs/zeroclaw/issues/2269) — 13 comments, **CLOSED**. Community sought direction on making productized agent workloads cost-viable.

**Underlying needs visible from hot discussions:** Operators want **bounded and predictable behavior** (goal mode, iteration budgets, shell policies). Integrators want **OpenAI-compatible APIs** for drop-in adoption. The RFC process itself is being optimized ([#9496](https://github.com/zeroclaw-labs/zeroclaw/issues/9496)) — a sign the process is becoming a bottleneck.

---

## 5. Bugs & Stability

**New High-Severity Bugs (past 2 days):**

| Severity | Issue | Status |
|---|---|---|
| **S1 (blocked)** | [#9883 — Inbound WebP conversion decodes unbounded before shared validator runs](https://github.com/zeroclaw-labs/zeroclaw/issues/9883) — Unbounded decompression risk (likely DoS vector) | **Open**, accepted |
| **S2** | [#9872 — Bounded delegate target writes to delegator's workspace instead of own](https://github.com/zeroclaw-labs/zeroclaw/issues/9872) — Filesystem sandbox escape via delegation | **Open**, accepted |
| **S2** | [#9768 — daemon reload not on SIGUSR1; warning advises a signal that kills the daemon](https://github.com/zeroclaw-labs/zeroclaw/issues/9768) | **Closed** |

**Feature/regression bugs fixed recently:**

- [#9035 — Docker Compose gateway loopback-bound behind published port](https://github.com/zeroclaw-labs/zeroclaw/issues/9035) — Closed (S1 workflow blocker).
- [PR #9781 — WebAuthn assertion data validation](https://github.com/zeroclaw-labs/zeroclaw/pull/9781) — Binds to `rpIdHash`, requires User Present flag; in review.

**Quality gating:** [#9545 — gate rustdoc warnings in CI](https://github.com/zeroclaw-labs/zeroclaw/issues/9545) closed successfully, preserving a zero-rustdoc-warning baseline.

---

## 6. Feature Requests & Roadmap Signals

**Likely candidates for next release (v0.9.0):**

- **SOP (Standard Operating Procedures) 5/5 rollout** ([#8288 tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/8288)) — Daemon-owned SOP control plane; permission contract defined in [#9598](https://github.com/zeroclaw-labs/zeroclaw/issues/9598). Multiple open PRs (#9841, #9885) are converging.
- **Chat Completions (OpenAI-compatible) profile** (#8603, 18 comments) — Highest demand signal; if accepted, adoption becomes trivial for major clients.
- **Pluggable authenticated inbound + canonical principals** (#7141, Rev 8) — Identity & Access milestone.
- **PowerShell native shell on Windows** ([PR #9182](https://github.com/zeroclaw-labs/zeroclaw/pull/9182)) — Windows parity.
- **Plugin-owned Kanban board** ([#8832](https://github.com/zeroclaw-labs/zeroclaw/issues/8832)) — Novel coordination UI; likely to generate strong community demos.
- **Token accounting on history-trim events** ([PR #9713](https://github.com/zeroclaw-labs/zeroclaw/pull/9713)) — Directly addresses cost visibility complaints raised in #2269.

**Watch:** [#8303 Goal mode](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) marks a shift from single-turn agent to bounded multi-turn objectives — a key gap versus Claude Code / OpenCode competitors.

---

## 7. User Feedback Summary

- **Cost visibility is a sore point.** [#2269 (closed)](https://github.com/zeroclaw-labs/zeroclaw/issues/2269) and [#9713 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/9713) both address "tokens consumed without being able to account for them."
- **Noise and token bloat in prompts:** [PR #9561 removes filename labels](https://github.com/zeroclaw-labs/zeroclaw/pull/9561) from personality prompts — community flags unnecessary system-prompt tokens as a real cost.
- **Process overhead frustrates contributors:** [#9496 RFC](https://github.com/zeroclaw-labs/zeroclaw/issues/9496) explicitly laments "slower and more cumbersome than the decisions it is meant to support." The tracker [#8692](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) is itself a reaction to a stuck pipeline.
- **Security hardening is welcomed but incomplete:** Users report real sandbox escapes (e.g., delegate workspace escape #9872) — trust in the security model is actively being tested.
- **Positive signals:** Community members voluntarily maintain revision histories, narrow RFC scopes per maintainer feedback, and hand off PRs publicly — signs of a cooperative, mature contributor base.

---

## 8. Backlog Watch

**Items needing maintainer decision or action (aging):**

- [#7142 — RFC: Runtime-owned security decision pipeline](https://github.com/zeroclaw-labs/zeroclaw/issues/7142) — Rev 6, open since **June 3**, `needs-maintainer-review`. Core v0.9.0 security architecture; likely blocking several dependent PRs.
- [#7155 — RFC: Shell command policy (allow/ask/deny)](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) — Rev 3 since Aug 5, waiting on confirmation. High-value for Claude Code parity.
- [#6653 — Host-architecture policy for emulated installs](https://github.com/zeroclaw-labs/zeroclaw/issues/6653) — Open since **May 14**, `needs-author-action`. Losing momentum.
- [#5907 — RFC: Opt-in LSP support for ZeroCode](https://github.com/zeroclaw-labs/zeroclaw/issues/5907) — Open since **April 19**, `needs-author-action`. Unaddressed for months, yet directly ties to code-quality expectations.
- [#7887 — Runtime-owned sessions and transport adapters](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) — Broad, touching many entry points; needs maintainer boundary decisions early to avoid review churn.

**Stalled PR candidates:**

- [#9612 — WhatsApp Cloud approval token guard](https://github.com/zeroclaw-labs/zeroclaw/pull/9612) — flagged `stale-candidate`; security-relevant.
- [#9385 — WhatsApp Web request_approval](https://github.com/zeroclaw-labs/zeroclaw/pull/9385) — `stale-candidate`; massive label surface indicates scope creep risk. Likely needs splitting.

---

**Overall:** ZeroClaw is in a healthy but **review-bound** phase. The community is producing high-quality, well-revised RFCs and security fixes; the limiting factor is maintainer bandwidth. The project is positioning for a significant v0.9.0 via SOP completion, security pipeline ownership, and OpenAI-compatible ingress.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*