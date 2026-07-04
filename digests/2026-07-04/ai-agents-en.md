# OpenClaw Ecosystem Digest 2026-07-04

> Issues: 292 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-04 01:30 UTC

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

# OpenClaw Project Digest — 2026-07-04

## Today's Overview

OpenClaw continues at high velocity with **292 active issues** and **500 PRs** updated in the last 24 hours, though the velocity is skewed toward backlog churn rather than resolution (only 93 issues and 55 PRs closed/merged). With **199 open issues** and **445 open PRs**, the project maintains a significant queue. No new releases landed today, suggesting maintainers are focused on the stabilization sprint prompted by the recent `v2026.6.11` regression wave. The top issues remain concentrated on security, session-state corruption, and message-delivery failures — indicating core reliability is the present bottleneck.

## Releases

No new releases were published today. The latest published version remains **v2026.6.11** (June 11, 2026).

## Project Progress

Of 500 PRs updated in the last 24 hours, **55 were merged or closed** — a relatively low closure rate (11%) that suggests many PRs are stuck awaiting review or proof. Notable merged/closed PRs include:

- **#99658 (closed)** — `feat(providers): add ClawRouter routing and quotas` by steipete. This adds `@openclaw/clawrouter` as an official provider package for ClawRouter credential-scoped model routing and quota management.
- **#98740 (closed)** — Fix for Mattermost 401 errors on slash commands after the plugin externalization in 6.11.
- **#98528 (closed)** — Fix for a v2026.6.11 regression where tool output (exec, web_fetch, web_search) returned empty after the first call per turn.
- **#97871 (closed)** — Fix for `openclaw agent --local` hanging with Ollama/LM Studio providers.

**Still open but with sufficient proof** and awaiting maintainer action:
- **#99154** (P0, diagnostic) — Fixes model-call stream hot-path object copies causing V8 performance degradation; rated as highest-priority open PR.
- **#99658** (already merged above)
- **#99733** (feat: Google Antigravity auth bridge) — XL-sized, with compatibility and security-boundary merge-risks flagged.

## Community Hot Topics

### Most Active Issues (by comment count)

1. **#25592** — *Text between tool calls leaks to messaging channels* (33 comments)  
   🔗 https://github.com/openclaw/openclaw/issues/25592  
   A **diamond lobster**-rated security issue where internal agent processing text (error handling, acknowledgments) gets routed to Slack/iMessage. This has been open since February 2026 and is still awaiting product decision — a sign of design stalemate.

2. **#99551** — *[Tracker] Codex worker runaway hardening sprint* (14 comments)  
   🔗 https://github.com/openclaw/openclaw/issues/99551  
   Newly created (July 3) tracker for hardening against worker incidents (ref: `019f18dc-0080-7201-a969-4efa8dd87949`). This signals incident-driven sprint prioritization.

3. **#73148** — *Image tool: opaque "Failed to optimize image" when sharp is not installed* (14 comments)  
   🔗 https://github.com/openclaw/openclaw/issues/73148  
   Users frustrated by non-obvious missing-dependency errors.

4. **#10659** — *Feature Request: Masked Secrets* (13 comments, 4 👍)  
   🔗 https://github.com/openclaw/openclaw/issues/10659  
   Request for agents to **use** API keys without being able to **see** them — a security-hardening request that aligns with the project's current security focus.

5. **#55286** (not shown in top 50 but high activity on **#6731** — safe/unsafe ClawdBot, 12 comments) and **#92043** — *180s compaction timeout failure* (11 comments, 3 👍)  
   🔗 https://github.com/openclaw/openclaw/issues/92043

### Underlying Needs
The community is demanding:
- **Security by default** — masked secrets, denylists for exec approvals, agent awareness restrictions
- **Reliability improvements** — compaction timeouts that don't loop, message delivery that doesn't strand
- **Better error messages** — opaque errors like "Failed to optimize image" erode trust

## Bugs & Stability

| Bug | Severity | Fix PR Exists? | Notes |
|-----|----------|----------------|-------|
| **#98416** — v2026.6.11 published dist missing reentrancy guard (11 comments, 5 👍) | **P1 / Diamond Lobster** | No | Reply session initialization conflicted; core chat broken |
| **#92043** — 180s compaction timeout loops (11 comments, 3 👍) | **P1 / Diamond Lobster** | No (#linked-pr-open) | Slow recoveries become unrecoverable |
| **#90361** — Intermittent `memory_search "index metadata is missing"` (5 comments, 3 👍) | **P1 / Diamond Lobster** | No (#linked-pr-open) | Reindex race condition |
| **#92241** — Gateway holds stale module paths after rollback (5 comments, 1 👍) | **P1 / Platinum Hermit** | No (#linked-pr-open) | Messages silently dropped |
| **#87299** — Spurious "Something went wrong" in large Telegram sessions (7 comments) | **P2 / Platinum Hermit** | No | Beta release blocker flagged |
| **#85714** — Final agent_message stranded when LLM forgets delivery tool (8 comments) | **P1 / Diamond Lobster** | No (#linked-pr-open) | No fallback from task_complete |
| **#98437** — MCP loopback schema warnings (5 comments, 1 👍) | **No severity rating** | No | Thousands of warnings/day |

**Worst regression in recent release:** Issue **#98416** (dist missing reentrancy guard) and **#98528** (tool output returns empty after first call) both tied to v2026.6.11. #98528 was closed — the reentrancy bug remains open.

## Feature Requests & Roadmap Signals

### High-Community-Demand Features Likely for Next Release

1. **Masked Secrets (#10659)** — Diamond lobster, 13 comments, 4 👍, maintainer-reviewed. Security is clearly a current focus; this is the most likely candidate for inclusion in the next minor release.

2. **Provider fallback by failure class (#47910)** — Platinum hermit, 7 comments. Auth-broken providers waste latency. Maintainer-reviewed, needs product decision.

3. **Per-agent plugin configuration overrides (#55401)** — Diamond lobster, 5 comments. Multi-agent setups share global plugin config — a real pain point for power users.

4. **Dynamic model discovery for OpenRouter (#10687)** — Diamond lobster, 9 comments, 3 👍. Catalog moves faster than static generation; users want to use new models immediately.

### Lower-Profit Roadmap Signals
- **Voice call streaming TTS (#8355, 4 comments, 2 👍)** — Sentence-level TTS pipeline for Twilio calls.
- **Cron job hooks (#9465, 4 comments)** — Pre/post hooks for cron jobs.
- **Ralph Loop max iterations in agent config (#6890, 4 comments, 3 👍)** — Fine-grained control over iterative prompting.
- **Multi-agent collaboration enhancement RFC (#35203, 9 comments)** — Capability profiling + shared blackboard + layered memory — a long-term architectural proposal.

**Prediction:** The next release (likely `v2026.7.x`) will include **Masked Secrets** as the headline security feature, alongside **fallback by failure class** and the **per-agent plugin config** feature. The stabilization work from the Codex worker hardening sprint (#99551) is also likely to land.

## User Feedback Summary

### Pain Points (High Frequency)
- **"Text between tool calls leaks"** (#25592) — Core UX failure; users see internal processing garbage in chat
- **"Failed to optimize image" opaque error** (#73148) — Poor developer experience for new users
- **"Compaction timeout loops"** (#92043) — Production reliability issue for long-history users
- **"Tool output returns empty after first call"** (#98528, now closed) — Recent regression causing user distrust
- **"MCP loopback schema warnings"** (#98437) — Log noise degrading observability

### User Satisfaction Signals
- 👍 reactions on **#6615** (denylist for exec-approvals, 7 👍) and **#7524** (groupScope option, 4 👍) indicate strong alignment with power-user needs
- The community is actively submitting high-quality PRs (e.g., **#99154** has "proof: sufficient" and carries maintainer attention)
- The **ClawSweeper bot** continues to autonomously find and fix bugs (#75403, #75148), which users seem to accept — though these are sometimes held up by "waiting on author" tags

### Dissatisfaction Indicators
- Several P1 bugs with no fix PR open
- Issues like **#25592** (text leaking) have been open since **February** with no product decision
- The **#98416** reentrancy guard regression shows the v2026.6.11 release had a shipped artifact that didn't match the source — a quality-process concern

## Backlog Watch

### Critical Issues Awaiting Maintainer Action
| Issue | Age | Status | Why It Matters |
|-------|-----|--------|----------------|
| **#25592** — Text between tool calls leaks | 131 days | Needs product decision | Security/UX — longest-unresolved diamond lobster |
| **#10659** — Masked Secrets | 148 days | Needs security review, product decision | Security cornerstone — requires decision |
| **#92043** — Compaction timeout loops | 24 days | Needs maintainer review, linked PR open | Crashes long sessions — design fix exists but not merged |
| **#73148** — Opaque image error | 67 days | Stale, P2 | Low-hanging UX fix for new users |
| **#98416** — Reentrancy guard missing from dist | 3 days | Needs maintainer review (info) | Fresh, high-severity regression |

### Issues Needing Reproducer / Info
- **#97871** (closed) — Agent --local hangs — has been closed, but the root cause may need broader testing
- **#87299** — Spurious "Something went wrong" — needs live repro
- **#89147** — Native hook relay starves — needs live repro

### Stale High-Priority PRs
- **#77540** — gateway session cache (P1, 62 days open) — Could meaningfully improve TTFT
- **#75179** — incremental memory sync (P2, 66 days open) — Blocked on needs-real-behavior-proof
- **#75011** — pairing.md documentation (P3, 66 days open) — Low-risk docs improvement waiting on author

**Callout:** The **#99551** tracker for Codex worker runaway hardening is brand-new (July 3) and suggests maintainers are prioritizing reliability over new features this cycle. That is encouraging for addressing the compaction (#92043) and reentrancy (#98416) bugs, but does not resolve the long-running product-decision stall on issues like #25592.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

## Cross-Project Ecosystem Comparison Report: 2026-07-04

### 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem on July 4, 2026, is in a state of **rapid, high-velocity maturation**. The landscape is dominated by a handful of major projects—**OpenClaw, NanoBot, Hermes Agent**, and **IronClaw**—each seeing hundreds of code changes daily. The core developer focus has shifted from early feature experimentation toward **stability, reliability, and production hardening**, with critical bugs in session-state, memory, and connectivity now the primary blockers. A significant second tier of projects (CoPaw, ZeroClaw, PicoClaw, NanoClaw) is advancing quickly, often by forking and specializing the core architectures to serve specific deployment needs (mobile, embedded, enterprise), while smaller projects (NullClaw, TinyClaw, Moltis) indicate the market is consolidating around the dominant players.

### 2. Activity Comparison

| Project | Issues (Updated/Closed) | PRs (Updated/Merged) | Release Status | Health Score (Qualitative) |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 292 / 93 | 500 / 55 | v2026.6.11 (Stabilization Sprint) | **Moderate** — High volume, but low closure rate (11%) and severe regression wave. |
| **NanoBot** | 29 / N/A | 38 / 6 | None today | **Good** — High velocity, focused on provider bugs and memory fixes. |
| **Hermes Agent** | 50 / 3 | 50 / 6 | None today | **Moderate** — High triage pressure, several critical bugs with no fix PRs. |
| **PicoClaw** | N/A / N/A | 17 / 5 | **v0.3.1** | **Good** — Strong connectivity focus, active community fix PRs. |
| **NanoClaw** | 1 / 0 | 17 / 2 | None today | **Stable** — Low issue count, steady feature addition, long-open PRs a concern. |
| **NullClaw** | 1 / 0 | 0 / 0 | None today | **Low** — Minimal activity, maintenance-watch state. |
| **IronClaw** | 33 / 5 | 50 / 28 | None today (0.24.0 latest) | **High** — Very high throughput, strong closure rate (56%), Reborn architecture migration is core focus. |
| **LobsterAI** | 1 / 1* | 16 / 14 | **2026.7.3** | **Good** — Healthy release cycle, focused on Cowork sub-system stability. |
| **CoPaw** | 40 / 26 | 33 / 15 | None today | **Good** — High engagement and responsiveness, but 2.0 beta has stability blockers. |
| **ZeroClaw** | 36 / N/A | 50 / 5 | None today (v0.8.2 work) | **High** — Intense development, shipping major architecture changes, new S1 bugs found. |
| **TinyClaw** | 0 / 0 | 0 / 0 | N/A | **Dormant** |
| **Moltis** | 0 / 0 | 0 / 0 | N/A | **Dormant** |
| **ZeptoClaw** | 0 / 0 | 0 / 0 | N/A | **Dormant** |

*Note: The LobsterAI issue was closed as stale.

### 3. OpenClaw's Position

OpenClaw holds a position as the **most influential core reference implementation** in the ecosystem, evidenced by its sheer scale and the number of derivative projects (PicoClaw, NanoClaw, NullClaw). Its advantages are:

- **Scale & Community Size:** With **292 active issues, 500 active PRs, and a massive developer base**, it dwarfs all other projects in raw activity. Its `@openclaw/` package ecosystem (e.g., ClawRouter) provides a structural advantage for extensibility.
- **Maturity of Tooling:** It has a dedicated **ClawSweeper bot** for autonomous bug fixing, advanced features like `ClawdBot`, and formalized security ratings ("Diamond Lobster," "Platinum Hermit").
- **Centralization Risk:** Its primary vulnerability is its own complexity. The project is currently in a "stabilization sprint" following a bad regression wave (v2026.6.11), with a low **PR closure rate of 11%** suggesting a bottleneck in maintainer review capacity. This creates an opportunity for more agile competitors.

**Comparative Weakness:** While OpenClaw offers the broadest feature set, its velocity is currently hampered by a **core-reliability bottleneck** (session-state corruption, message loss, and persistent security issues like text leaking between tool calls). This contrasts with more focused projects like NanoBot, which can fix critical provider bugs (e.g., Anthropic temperature parameter) within a day.

### 4. Shared Technical Focus Areas

Several critical themes are emerging *across* multiple projects, indicating industry-wide requirements:

- **Connection Reliability & Reconnection:** A top priority for **OpenClaw** (Mattermost 401, Gateway stale paths), **PicoClaw** (WhatsApp WebSocket timeout, Matrix sync loop death, #3178, #3219), **NanoClaw** (WhatsApp reconnect, PR #2348), **NullClaw** (Telegram stops responding, #972), and **IronClaw** (retry path unreachable, #5608). *User demand is for persistent, self-healing network connections.*

- **Memory & Context Hygiene:** A critical pain point. **OpenClaw** (compaction timeout loops, #92043), **NanoBot** (memory loss under pressure, #4044, #4307), **CoPaw** (scroll context compression bug, #5746; malformed tool-call loops, #5717), and **ZeroClaw** (MCP tool-schema cloning memory growth, #8642) are all struggling with state management. *The community wants reliable, non-corruptible agent memory.*

- **Secret & Credential Management:** A security-first focus is shared by **OpenClaw** (Masked Secrets request, #10659), **CoPaw** (secret desensitization request, #5705), **Hermes Agent** (terminal snapshots leak .env secrets, #48441), and **IronClaw** (credential injection fix, #5623; OAuth-surface guard, #5615). *Users are demanding that agents use secrets without exposing them.*

- **Model Provider Compatibility & OAuth:** Fluctuations in major model providers (especially Anthropic) are causing widespread bugs. **NanoBot** fixed an Anthropic temperature parameter rejection (#4683) and a stale default model (#4675). **Hermes Agent** reports broken Anthropic Max OAuth (#48534) due to a User-Agent block, as well as OpenAI Codex OAuth gateway isolation failure (#12058). *The ecosystem is highly sensitive to upstream API changes.*

### 5. Differentiation Analysis

| Feature/Architecture | OpenClaw | NanoBot | Hermes Agent | IronClaw | CoPaw/PicoClaw/ZeroClaw |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Primary Target User** | General developers & power users | Developers & CLI users | Multi-platform users (Desktop, API) | Enterprise, infrastructure-heavy | Specialized: CN market (CoPaw), mobile/lightweight (Pico/Nano), WASM-first (ZeroClaw) |
| **Core Arch. Philosophy** | Monolithic reference, broadest package ecosystem | Agent "Dream" system, MCP-centric | Desktop-first, multi-profile gateway (Telegram, Discord) | "Reborn" architecture, WASM plugins | Fork-based specialization: Pico/Nano simplify; ZeroClaw is Rust/WASM native |
| **Key Differentiator** | Size of community & package ecosystem | Anthropic OAuth support; rapid provider bug fixes | Multi-profile channel routing from a single gateway | WASM plugin execution, SOP engine, OIDC support | CoPaw: 2.0 beta with custom model protocol; ZeroClaw: out-of-process WASM sidecar |
| **Security Maturity** | Formal severity ratings, but design stalemates (e.g., text leaking) | Reactive, fast bug fixes | Proactive on secret redaction (PR #3651) | Defense-in-depth, identity layer auditing (high risk) | Reactive; safety features (secret masking) are requested, not yet built. |

### 6. Community Momentum & Maturity

**Tier 1: High-Velocity Iteration (Active Daily, Major Architecture Changes)**
- **OpenClaw, IronClaw, ZeroClaw** are in intense development cycles. They are shipping major features (e.g., IronClaw's Reborn migration, ZeroClaw's WASM sidecar) but are also finding and breaking things at scale. These projects are *not* stable for production without careful version pinning.

**Tier 2: Mature & Focused (Stabilizing Specific Domains)**
- **NanoBot, CoPaw, LobsterAI** are showing strong maturity. NanoBot is rapidly fixing provider-level bugs and refining its "Dream" memory system. CoPaw is crushing bugs rapidly (26 closed in 24h) as it pushes its 2.0 beta. LobsterAI is shipping stable releases with a clear focus on "Cowork" features.

**Tier 3: Niche & Distribution-Centric**
- **PicoClaw and NanoClaw** are building on core architectures to serve specific runtime targets (mobile, container, rootless Podman). Their activity is driven by platform-specific bug fixes (e.g., Android, Signal in containers).

**Tier 4: Dormant / Stale**
- **NullClaw, TinyClaw, Moltis, ZeptoClaw** show minimal to no activity, indicating they are either finished projects or have failed to gain traction.

### 7. Trend Signals

1.  **The "Memory Stability" Ceiling:** The most significant bottleneck across the ecosystem is not model capability but **agent-state and memory reliability**. Projects are spending more time fixing bugs in context compression, compaction, and session persistence than adding new features. Expect a wave of innovations around **fault-tolerant state storage** and **provable memory integrity** in the coming months.

2.  **The Rise of the Enterprise Gateway:** **Hermes Agent’s** `channel_profiles` (#40173), **IronClaw’s** `manifest-driven ingress` (#5625), and **ZeroClaw’s** `OIDC authentication` (#7141) all point toward a key trend: the agent is becoming a **multi-tenant, multi-channel enterprise gateway**, not just a personal chat bot. Requirements for RBAC, secret management, and audit trails are migrating from enterprise requests into core feature PRs.

3.  **Provider Fragmentation is the New Normal:** The ecosystem’s constant breakage from model provider API changes (Anthropic, OpenAI, GitHub) implies an emerging industry need for **provider-agnostic abstraction layers** and **automated test harnesses** that pre-validate agents against all major backends before release.

4.  **The Fork-and-Specialize Strategy is Proliferating:** The success of PicoClaw, NanoClaw, and NullClaw, each a fork of OpenClaw, validates a market strategy: take the complex, full-featured core and **optimize for a specific runtime (mobile, embedded, container) or user persona (CLI-only, minimalist).** This is a sign of a maturing ecosystem where the `claw` architecture is seen as a platform to be remixed rather than a single product.

5.  **Security is a First-Class Feature, Not an Afterthought:** "Masked Secrets," "denylists for exec approvals," "OAuth surface guards," and "SOP approval gate bypass" are not just bugs; they are architectural demands. The community is no longer accepting "we will add security later." The projects that formalize a **zero-trust, least-privilege security model** into their core architecture (e.g., OpenClaw's security ratings, IronClaw's identity layer) will likely win the trust of enterprise and power users.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for **2026-07-04**.

---

## NanoBot Project Digest (2026-07-04)

### 1. Today's Overview
The NanoBot project continues to exhibit very high development velocity, with 29 issues and 38 pull requests updated in the last 24 hours. Activity is concentrated on stability fixes, provider support (especially Anthropic), and memory/context management. While no new releases were cut, the sheer volume of code changes and community engagement signals a project in a mature, active maintenance phase with a strong focus on refining core architecture and user experience.

### 2. Releases
**No new releases today.**

### 3. Project Progress
Six pull requests were merged or closed today, indicating steady progress on the main branch:

- **[PR #4632] feat(providers): add Anthropic OAuth** ([Link](https://github.com/HKUDS/nanobot/pull/4632)) – Landed full support for Claude subscription users to authenticate via OAuth tokens (e.g., from `claude setup-token`).
- **[PR #4685] fix: omit temperature for sonnet-5** ([Link](https://github.com/HKUDS/nanobot/pull/4685)) – Fixed a critical provider bug causing 400 errors when `temperature` was sent to `claude-sonnet-5`.
- **[PR #4687] fix(providers): update Anthropic default model to claude-sonnet-4-6** ([Link](https://github.com/HKUDS/nanobot/pull/4687)) – Replaced the stale default model `claude-sonnet-4-20250514` with `claude-sonnet-4-6` across the codebase and docs.
- **[PR #4691] fix(plugins): polish optional feature controls** ([Link](https://github.com/HKUDS/nanobot/pull/4691)) – Improved UX for the new plugin system, adding graceful warnings for missing dependencies.
- **[PR #4688] feat(cli): add safe WebUI first-run launcher** ([Link](https://github.com/HKUDS/nanobot/pull/4688)) – Introduced a first-class `nanobot webui` command with config validation.
- **[PR #4396] Add optional Nanobot plugin controls** ([Link](https://github.com/HKUDS/nanobot/pull/4396)) – Merged the framework for enabling/disabling built-in features (chat, providers, docs) via CLI/WebUI.

### 4. Community Hot Topics
The community is most engaged around memory reliability and multi-user scenarios:

- **Memory Loss Under Pressure** – Issue **#4044** ([Link](https://github.com/HKUDS/nanobot/issue/4044)) and **#4307** ([Link](https://github.com/HKUDS/nanobot/issue/4307)) remain the top pain points. Users report that consolidation wipes the assistant's own delivery message, causing the agent to lose track of its own responses. A fix PR **#4280** ([Link](https://github.com/HKUDS/nanobot/pull/4280)) is active.
- **Multi-Tenant / Multi-User Memory** – Issue **#3744** ([Link](https://github.com/HKUDS/nanobot/issue/3744)) and **#4390** ([Link](https://github.com/HKUDS/nanobot/issue/4390)) show demand for managing separate `MEMORY.md` files per user or instance, especially for IM channels like WeChat.
- **Skill Management in Dreams** – Issue **#4467** ([Link](https://github.com/HKUDS/nanobot/issue/4467)) and **#3846** ([Link](https://github.com/HKUDS/nanobot/issue/3846)) request that the Dream system update existing skills rather than creating duplicates, and that skill content be preserved across multi-turn conversations.

### 5. Bugs & Stability

**Critical**
- **Process crash on MCP errors** – Issue **#4652** ([Link](https://github.com/HKUDS/nanobot/issue/4652)): Nanobot crashes immediately when an MCP tool call returns an error. **Fix PR #4666** ([Link](https://github.com/HKUDS/nanobot/pull/4666)) is open to contain malformed results.
- **Gateway crash after MCP reconnect** – Issue **#4302** ([Link](https://github.com/HKUDS/nanobot/issue/4302)): Gateway-level crash following session termination and reconnect attempts.

**High**
- **Anthropic temperature parameter reject** – Issue **#4683** ([Link](https://github.com/HKUDS/nanobot/issue/4683)) (closed): `claude-sonnet-5` rejected the `temperature` field, causing a 400 error. **Fixed by PR #4685**.
- **Stale Anthropic default model** – Issue **#4675** ([Link](https://github.com/HKUDS/nanobot/issue/4675)) (closed): Default model pointed to a May 2025 version. **Fixed by PR #4687**.
- **Windows gateway stop crash** – Issue **#4511** ([Link](https://github.com/HKUDS/nanobot/issue/4511)): Restart logic fails due to stale process info files. **Fix PR #4690** ([Link](https://github.com/HKUDS/nanobot/pull/4690)) is targeting the Windows fallback.
- **Telegram silent hang** – Issue **#3626** ([Link](https://github.com/HKUDS/nanobot/issue/3626)): Long polling connection can hang silently; bot stays alive but stops receiving updates.

**Medium**
- **Cron job ends early with subagents** – Issue **#4290** ([Link](https://github.com/HKUDS/nanobot/issue/4290)): Main agent fails to process subagent results before the job terminates.
- **Streaming failure in CLI** – Issue (via PR) **#4654** ([Link](https://github.com/HKUDS/nanobot/pull/4654)): Interactive mode loses the full response when a provider emits no streaming deltas.

### 6. Feature Requests & Roadmap Signals

Strong signals for the next minor release focus on **memory hygiene** and **platform integration**:

- **Agent-to-Agent (A2A) Orchestration** – Issue **#4179** ([Link](https://github.com/HKUDS/nanobot/issue/4179)): Proposal for native multi-agent teams (Supervisor -> Researcher -> Writer) with shared context. This is a significant architectural request.
- **Mattermost Channel Support** – PR **#4459** ([Link](https://github.com/HKUDS/nanobot/pull/4459)): Adds a new channel integration for Mattermost via WebSocket + REST, indicating a push toward enterprise team communication platforms.
- **`search_history` tool** – Issue/PR **#4440** (Issue [Link](https://github.com/HKUDS/nanobot/issue/4440), PR [Link](https://github.com/HKUDS/nanobot/pull/4439)): A read-only tool to query past conversation summaries from `history.jsonl` without bloating context.
- **`ask_clarification` tool** – Issue **#4508** ([Link](https://github.com/HKUDS/nanobot/issue/4508)): Proposed built-in tool to let the agent ask clarifying questions and end the current turn.
- **Cron job model presets** – PR **#4622** ([Link](https://github.com/HKUDS/nanobot/pull/4622)): Allows per-cron-job model/provider overrides, addressing the need for cheaper models on routine tasks.
- **Heartbeat-specific model override** – Issue **#4431** ([Link](https://github.com/HKUDS/nanobot/issue/4431)): Request to run heartbeat checks on a cheaper dedicated model.
- **WebUI PWA & Responsive Layout** – Issue/PR **#4479** ([Link](https://github.com/HKUDS/nanobot/issue/4479)) and **#4693** ([Link](https://github.com/HKUDS/nanobot/issue/4693)): Mobile usability improvements, including manifest support and swipe gestures.
- **OAuth Status & Expiry Warnings** – PR **#4689** ([Link](https://github.com/HKUDS/nanobot/pull/4689)): Proactive warnings for expiring OAuth tokens in CLI and WebUI.

### 7. User Feedback Summary

- **Pain Points**: The most frequent complaints are about **short-term memory loss** (#4044, #4307) and **MCP-related crashes** (#4652, #4302). Users are also frustrated by **Dream creating duplicate skills** (#4467) and a lack of **multi-user memory isolation** (#3744).
- **Satisfaction**: The quick closure of high-severity issues like the Anthropic temperature bug (#4683) and the default model update (#4675) shows responsiveness. The community is actively submitting PRs, indicating strong developer satisfaction and trust.
- **Use Cases**: The feature requests reveal a shift from simple chat to **multi-agent workflows** (#4179), **team communication channels** (Mattermost #4459), and **long-running automation** (cron job presets #4622, heartbeat triggers #4620).

### 8. Backlog Watch

The following items require maintainer attention or signal long-standing architectural concerns:

- **Telegram long polling hang** – Issue **#3626** ([Link](https://github.com/HKUDS/nanobot/issue/3626)): Created May 5. A persistent reliability bug affecting Telegram users has seen no confirmed fix.
- **`exec` tool authorization** – Issue **#3887** ([Link](https://github.com/HKUDS/nanobot/issue/3887)): Created May 18. Proposal for user authorization of blocked dangerous commands (e.g., `rm -rf`). This has 2 comments and 1 👍 but no maintainer response or PR.
- **Bwrap sandbox bind-mount config** – Issue **#4107** ([Link](https://github.com/HKUDS/nanobot/issue/4107)): Created May 30. Request to allow user-configurable bind mounts for the bwrap sandbox; no resolution.
- **Dream "Hunger" problem** – Issue **#3973** ([Link](https://github.com/HKUDS/nanobot/issue/3973)): Created May 23. Raises a fundamental limitation of the Dream system (relying only on `history.jsonl`), which is related to the duplicate skill issue being addressed in PR #4554 but remains open-ended.
- **Consolidation fact permanence** – Issue **#4212** ([Link](https://github.com/HKUDS/nanobot/issue/4212)): Created June 5. Warns that unconfirmed inferences can be re-injected as facts and outlive corrections. PR #4621 ([Link](https://github.com/HKUDS/nanobot/pull/4621)) attempts to add provenance context, but the issue remains open.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for **2026-07-04**.

---

## Hermes Agent Project Digest — 2026-07-04

### 1. Today's Overview
The project is experiencing **high activity** with 50 issues and 50 PRs updated in the last 24 hours, though the open/active ratio (47 open vs. 3 closed issues; 44 open vs. 6 closed PRs) indicates that the maintainers are under significant triage pressure. No new releases were published today, but the development velocity is high, with several critical fixes in flight. The community is reporting a diverse set of bugs spanning auth, caching, desktop UI, and session state, balanced by a healthy stream of feature PRs from both core contributors and external developers.

### 2. Releases
No new releases were published on 2026-07-04.

### 3. Project Progress
Today, **6 pull requests** were merged or closed, advancing the codebase:

- **[PR #56074]** `[CLOSED]` — **fix: reset in-memory _openrouter_catalog_cache on /model --refresh** by abhi-0203. Fixes a caching regression where `hermes model --refresh` would return stale catalog data because the in-memory cache wasn't cleared alongside the disk cache.
- **[PR #51592]** `[CLOSED]` — **fix(docker): avoid overlayfs copy-up storm in chmod/chown** by DamienDrash. Performance fix for Docker images, reducing three full recursive filesystem walks into a single pass, dramatically reducing Docker build times on overlay2 filesystems.
- **[PR #57909]** `[CLOSED]` — **Bug fix** for gateway adapter detection after `hermes update`, where Telegram and WhatsApp adapters were erroneously reported as unavailable.

### 4. Community Hot Topics
The most active discussions reflect deep integration pain points and requests for advanced flexibility:

- **[Issue #40173]** (👍 3, comments 3) — **feat(telegram): channel_profiles — route Telegram chats to Hermes profiles in one gateway**. A highly-upvoted request to allow a single Telegram bot process to route messages from different chats to different Hermes profiles, avoiding the overhead of running multiple gateway instances.
    - *Underlying need:* Multi-tenant or multi-personality setups on a single instance.
- **[Issue #12188]** (👍 2, comments 5) — **Setting `hermes model` config/settings inside Docker compose as env variables**. Users want to configure model providers entirely through environment variables in Docker Compose, without needing to exec into the container.
    - *Underlying need:* Streamlined, declarative Docker-based deployment.
- **[Issue #48441]** (👍 1, comments 5) — **[CLOSED Security] Terminal session snapshots leak .env secrets to disk in plaintext**. A high-severity bug that was actively discussed; the issue was closed, but the sensitivity of the fix will likely warrant extra validation.

### 5. Bugs & Stability
**Critical (P0):**
- **[Issue #57845]** — [`P0`] **Envelope-layout cache breakpoints silently no-op during tool loops** on OpenRouter + Claude, causing ~2x input cost. The cache breakpoint strategy skips effective markers during tool loops. *Status:* Open, no fix PR linked, high-priority due to direct cost impact.

**High (P1):**
- **[Issue #12058]** — [`P1`] **OpenAI Codex OAuth works in CLI, but Telegram gateway replies "No Codex credentials stored"**. A gateway-specific auth isolation bug where a profile works in the CLI but fails under the Telegram gateway.
- **[Issue #48534]** — [`P1`] **Anthropic Max OAuth fails: token exchange 404s** because Anthropic now blocks the `claude-cli/` User-Agent. The OAuth flow is completely broken for Max tier users.

**Medium (P2):**
- **[Issue #57928]** — [`P2`] **Telegram file attachment broken** when combined with slash commands (`/steer`, `/goal`). Files are silently dropped.
- **[Issue #57903]** — [`P2`] **async LLM calls block the desktop WebSocket loop** via busy-poll in interruptible API calls. *Status:* A draft fix exists in **[PR #57933]**.
- **[Issue #57905]** — [`P2`] **Windows: `computer_use` ignores `cua-driver 0.7.0` data.windows output**, causing empty window discovery.
- **[Issue #56747]** — [`P2`] **Windows: Blank terminal console windows flash** when running agent or tools via Desktop GUI.
- **[Issue #57955]** — [`P2/security] **Terminal tool bypasses SOUL.md write-protection** via shell commands like `sed -i`.
- **[Issue #57861]** — [`P2`] **Cron-triggered sessions never get Composio MCP tools attached**.

### 6. Feature Requests & Roadmap Signals
Several user-requested features point toward upcoming capabilities:

- **Multi-profile Gateway Routing (High Likelihood for v0.19.0):** **[Issue #40173]** (Telegram channel_profiles) is gaining traction and complements the ongoing multiplex work in **[PR #57563]** (fixing credential isolation for multiplexed profiles). This is a top candidate for the next minor release.
- **Configurable Discord Voice Timeout (Medium Likelihood):** **[Issue #17790]** is a simple, well-scoped feature request with a clear implementation path. Likely to be picked up as a "good first issue" or low-hanging fruit.
- **Agent Migration System (Long-term):** **[Issue #524]** (Auto-Detect & Import Settings from Claude Code, Codex, Aider, etc.) is a strategic initiative for user acquisition. This is likely on the roadmap for `v0.20.0` or later, as it involves extensive cross-tool integration.
- **Local Media Generation UI (Medium Likelihood):** **[Issue #46337]** (Custom Local STT/TTS/Image UI) flags a gap in the new Desktop app. As the desktop client matures, this is a natural follow-up.

### 7. User Feedback Summary
- **Pain Points:**
    - **Docker/Deployment Confusion:** Users find the Docker Compose documentation lacking (Issue #12188) and struggle with environment-based configuration for model providers.
    - **OAuth Fragility:** Multiple auth pathways are broken or flaky (Issues #12058, #48534, #6347), causing frustration for users relying on OAuth for Claude Max and OpenAI Codex.
    - **Desktop UX Degradation:** Post-update UI regressions (Issue #57968, flat sessions list missing) and Windows-specific graphical glitches (Issue #56747) are creating a rough experience for Desktop users.
    - **Cost Surprises:** The cache breakpoint issue (Issue #57845) is directly increasing API costs for users, a sensitive problem that erodes trust.
- **Satisfaction Signals:**
    - High engagement with **#40173** (channel_profiles) suggests users see Hermes as a powerful multi-tenant platform and want to unlock that capability without operational overhead.
    - The rapid response on security issues (Issue #48441 closed, PR #57563 for credential isolation) shows the maintainers take security seriously.

### 8. Backlog Watch
These issues are important but have remained without maintainer response for extended periods:

- **[Issue #6347]** — [`P2`, Created 2026-04-09] **Anthropic OAuth refresh path gets Cloudflare 403 and leaves Hermes PKCE creds unrefreshable**. Last updated 2026-07-03, but the core problem (Cloudflare blocking refresh) has been open since April. Users reliant on PKCE OAuth are stuck once tokens expire.
- **[Issue #524]** — [`P3`, Created 2026-03-06] **Feature: Agent Migration System**. This is a major strategic feature but has received no direct maintainer comment. It represents a significant lost opportunity for user onboarding.
- **[PR #3651]** — [`P2`, Created 2026-03-29] **feat(secrets): add phase 1 secrets tool and redaction hardening**. A long-lived open PR adding a critical security feature. It has not been merged or received a renewal review since its creation. High risk of bitrot.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-04

## Today's Overview
PicoClaw shows **high development activity** with 17 pull requests touched in the last 24 hours, 5 of which were merged or closed. The project released **v0.3.1**, though no detailed changelog is available beyond merge commits. Two open bugs remain from late June, both stale and unresolved. The PR queue shows a strong focus on **connectivity reliability** (WhatsApp, Matrix, Discord), **agent session handling**, and **config migration fixes**, signaling a maturity push around operational stability. Overall project health appears solid but with a backlog of important fixes that need maintainer attention.

## Releases
**v0.3.1** was released, but its changelog consists only of three merge commit references and no structured release notes. From associated PRs, this release likely includes:
- `nearai-provider` integration
- `codex/store-lock-type-assert` fix
- Several other unlisted changes

**No breaking changes or migration notes** have been published. Users upgrading from v0.2.x should test their configurations before production deployment.

## Project Progress
The following PRs were merged or closed today:

| PR | Title | Status |
|----|-------|--------|
| #3224 | fix(agent): clear routed agent session | Open (replaces #3223) |
| #3223 | fix(agent): clear routed agent session | Closed in favor of #3224 |
| #3128 | fix(web): explicitly ignore resp.Body.Close() errors | Merged/Closed |
| #3142 | fix(spawn): clear ForUser in sub-turn ToolResult | Merged/Closed |
| #3063 | feat: add deltachat gateway | Merged/Closed |
| #3156 | feat(pico): emit per-turn LLM token usage | Merged/Closed |

**Key advancements:**
- **Agent session routing fix**: `/clear` now correctly targets the active routed agent, not the default agent ([#3224](https://github.com/sipeed/picoclaw/pull/3224))
- **DeltaChat gateway merged**: A new messaging channel has been integrated ([#3063](https://github.com/sipeed/picoclaw/pull/3063))
- **LLM token usage emission**: Per-turn token counting now available via Pico channel ([#3156](https://github.com/sipeed/picoclaw/pull/3156))
- **Web search cleanup**: Error handling improvements in four search providers ([#3128](https://github.com/sipeed/picoclaw/pull/3128))
- **Sub-agent duplicate message fix**: Spawn sub-turn messages no longer deliver duplicates ([#3142](https://github.com/sipeed/picoclaw/pull/3142))

## Community Hot Topics
**Most active Issues:**
1. **#3182 - Android version bug** ([link](https://github.com/sipeed/picoclaw/issues/3182)) — 2 comments, 6 days stale. User cannot launch PicoClaw on Android due to path/settings issues. Attached screenshot shows service startup failure.
2. **#3178 - WhatsApp WebSocket Timeout** ([link](https://github.com/sipeed/picoclaw/issues/3178)) — 1 comment, 7 days stale. WebSocket connection to WhatsApp drops with no recovery.

**Most active PRs:**
- **#2937 - Agent Collaboration Bus** ([link](https://github.com/sipeed/picoclaw/pull/2937)) — Long-running (41 days), major feature introducing durable inter-agent communication with mailboxes and permission-aware routing.
- **#3179 - WhatsApp reconnect fix** ([link](https://github.com/sipeed/picoclaw/pull/3179)) — Addresses the exact bug from #3178; proposes async message dispatch and read deadline configuration.

**Underlying need**: Users are experiencing **connection reliability problems across messaging channels** (Android, WhatsApp, Matrix). The community is actively submitting fixes for these exact issues.

## Bugs & Stability
**High Severity:**
- **WhatsApp WebSocket Timeout (#3178)** — Open 7 days. Connection drops permanently; no automatic recovery. **Fix PR exists**: [#3179](https://github.com/sipeed/picoclaw/pull/3179) proposes async dispatch and reconnect logic. Also [#3220](https://github.com/sipeed/picoclaw/pull/3220) adds exponential backoff reconnect.

**Medium Severity:**
- **Android version launch failure (#3182)** — Open 8 days. PicoClaw cannot start service on Android; path configuration broken. No fix PR yet.
- **Config migration failure (#3218)** — Newly discovered block on v2→v3 config migration due to missing `build_info` field in `legacyDiagnosticConfig`. **Fix PR**: [#3218](https://github.com/sipeed/picoclaw/pull/3218) submitted today.

**Low Severity:**
- **Matrix sync loop death (#3219)** — Network disruptions kill Matrix sync permanently. **Fix PR**: [#3219](https://github.com/sipeed/picoclaw/pull/3219) submitted today with backoff retry.

## Feature Requests & Roadmap Signals
**New features in PR pipeline:**
- **Agent Collaboration Bus** ([#2937](https://github.com/sipeed/picoclaw/pull/2937)) — Major architecture addition for multi-agent coordination. Likely a v0.4.0 candidate.
- **Configurable model fallback chain** ([#3200](https://github.com/sipeed/picoclaw/pull/3200)) — Web UI for setting default/fallback models. Strong candidate for next minor release.
- **Simplex chat channel** ([#3193](https://github.com/sipeed/picoclaw/pull/3193)) — New communication protocol integration.
- **Discord role-based access control** ([#3217](https://github.com/sipeed/picoclaw/pull/3217)) — Fine-grained permissions for Discord bots, useful for communities.

**Predicted next version (v0.3.2) likely includes:** WhatsApp reconnection fixes, Matrix recovery, Discord RBAC, and the config migration patch—all submitted on the same day.

## User Feedback Summary
**Pain points:**
- Mobile (Android) experience is broken — unable to start or configure properly
- WhatsApp reliability is poor in production — connections die after 2-3 days with no recovery
- Configuration migration between versions is fragile
- No clear documentation for new users on setup and configuration

**Satisfaction indicators:**
- Community is actively contributing fixes (5+ unique authors in 24 hours)
- Users are pushing for multi-channel support (WhatsApp, Matrix, Discord, DeltaChat, Simplex)
- Long-running architecture discussions (Agent Collaboration Bus) suggest engaged power users

**Use cases emerging:** Production deployment on Docker, multi-agent setups, cross-channel personal AI assistants.

## Backlog Watch
**Issues needing maintainer attention:**
- **#3182 (Android)** — 8 days stale, no maintainer response. Critical for mobile users.
- **#3178 (WhatsApp timeout)** — 7 days stale, despite two fix PRs submitted today. Needs review.
- **#2937 (Agent Collaboration Bus)** — 41 days open with no merge decision. This is a major architecture PR that could block other developments.

**PRs awaiting review:**
- [#3179](https://github.com/sipeed/picoclaw/pull/3179) — WhatsApp reconnect (7 days old)
- [#3165](https://github.com/sipeed/picoclaw/pull/3165) — Seed XML tool call recovery (9 days old)
- [#3200](https://github.com/sipeed/picoclaw/pull/3200) — Model fallback chain (3 days old)
- [#3193](https://github.com/sipeed/picoclaw/pull/3193) — Simplex channel (6 days old)

**Recommendation:** The project should prioritize review of the WhatsApp reconnect PRs (#3179, #3220), the Android bug (#3182), and make a decision on the Agent Collaboration Bus (#2937) to unblock the roadmap.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-04

## Today's Overview
NanoClaw shows moderate activity with 17 pull requests updated in the last 24 hours and a single open issue. The project is in a sustained maintenance and feature-addition cycle, with a strong focus on fixing edge-case bugs in channel integrations (Signal, WhatsApp) and improving the container runtime for rootless Podman environments. The lone open issue (#2917) raises a significant performance concern about local model agents incurring unnecessary MCP tool-schema token overhead, which could impact users running cost-sensitive local deployments. The PR pipeline contains a healthy mix of bug fixes, skill additions (LINE channel, CalDAV, Google Contacts, system digest), and infrastructure improvements, with two PRs merged/closed today. No new releases were published in this window.

## Releases
*No new releases were published in the last 24 hours.*

## Project Progress
Two PRs were closed/merged today:

- **PR #2765 (closed)** – `feat(providers): add .format-lint-off` by amit-shafnir. Adds a per-provider formatting lint-disabling mechanism, likely to accommodate provider-specific code style requirements when generating or formatting agent tool outputs.

- **PR #2330 (closed)** – `fix(container): make axios MCP servers work through OneCLI's proxy` by Tij8i. Resolves a compatibility issue where axios v1.x sent absolute-form HTTP requests to the CONNECT-only proxy port, causing silent failures for MCP servers that use axios for HTTP transport. This is an important fix for any MCP server relying on HTTP/HTTPS tool calls inside OneCLI containers.

Additionally, significant work-in-progress PRs include:
- A **LINE Official Account channel adapter** (PR #2918), which would add a major Asia-Pacific messaging platform integration
- **Signal channel fixes** (PRs #2694, #2695) addressing dropped DMs and unreadable image attachments from containerized agents
- **CalDAV tool** (PR #2530) and **Google Contacts tool** (PR #2693), expanding the ecosystem of MCP-based productivity integrations
- **System digest skills** (PR #2863) for periodic or on-demand system monitoring reports

## Community Hot Topics
**Most Active Issue:**
- **Issue #2917** – *Local model as primary agents pay full MCP tool-schema token cost regardless of backend* (0 comments, 0 reactions). Although engagement is low, this issue addresses a systemic concern: when using local models (e.g., Gemma4:31B via oMLX) as the primary orchestrating agent rather than as a tool-calling backend, the full MCP tool schema (~27k tokens) is sent with every request. This represents a significant token overhead for local model users, particularly those running on resource-constrained hardware. The underlying need is for a **token-cost optimization path** for local models—potentially caching or compressing tool schemas, or allowing users to selectively enable only relevant tool subsets per session.

**Most Active PRs:**
- The most commented-on PRs are older, long-running fixes from cfis: **PR #2184** (fix poll-loop stale session), **PR #2208** (HTTP/SSE MCP transport support), and **PR #2348** (WhatsApp reconnect). These PRs have been open for 2+ months, suggesting they may be large or complex changes undergoing extended review. The community interest (evidenced by repeated updates) points to real operational pain points in channel reliability and MCP transport flexibility.

## Bugs & Stability
**High Severity:**
- **DB connection leak in container restart** (PR #2920, opened today by fix2015). The `openInboundDb()` call in `container-restart.ts` was never closed after checking for pending messages, leaking a file descriptor on every restart check. This is a **memory/resource leak** that degrades over time in long-running agent deployments. A fix PR already exists. Additional issues found in the same PR: stale references to `NANOCLAW_ADMIN_USER_IDS` (removed in v2) and a duplicate script. *Fix available.*

**Medium Severity:**
- **Signal DM dropped silently** (PR #2694, open for ~1 month). The Signal adapter fails to set `isMention`/`isGroup` flags on inbound DMs, causing the router to skip auto-creating a `messaging_group`. Users sending a direct message to their NanoClaw agent via Signal receive no response—the message is silently swallowed. *Fix PR open, not yet merged.*

- **Signal image attachments unreadable in containers** (PR #2695, open for ~1 month). The adapter emits the host file path for image attachments (`<signalDataDir>/attachments/<id>`), which is not mounted inside the agent container. Containerized agents cannot read images sent via Signal. *Fix PR staged to convert attachments to base64.*

**Low Severity:**
- **Duplicate text when `send_message` fires mid-turn** (PR #2531). Under certain timing conditions, the poll loop produces duplicated message output. *Fix PR open.*

## Feature Requests & Roadmap Signals
The following features are likely candidates for the next NanoClaw release:

1. **LINE Official Account channel** (PR #2918) – A major messaging platform for Japan, Taiwan, Thailand, and Indonesia. This would significantly expand NanoClaw's addressable user base in Asia.

2. **HTTP and SSE MCP server transports** (PR #2208) – Currently NanoClaw supports only stdio-based MCP servers. Adding HTTP and Server-Sent Events transports would allow agents to connect to remote MCP servers over the network, enabling SaaS-backed tool ecosystems.

3. **Google Contacts MCP tool** (PR #2693) – Completes the G-Suite integration trilogy (Gmail + GCal + Contacts), giving users a full productivity suite accessible via natural language.

4. **CalDAV tool** (PR #2530) – Adds calendar integration for non-Google calendar services (e.g., Nextcloud, iCloud, self-hosted CalDAV). Indicates demand for **multi-provider calendar support**.

5. **System digest skills** (PR #2863) – Adds `/setup-system-digest` and `/system-digest` slash commands for periodic or on-demand system monitoring (CPU, memory, disk, uptime). Strong operational interest from users running agents 24/7 in production.

6. **Skill fragment gating** (PR #2921) – A fix that correctly gates skill instructions to the group they belong to. This is a structural improvement that prevents skill pollution across groups, but also signals user demand for **multi-tenant or multi-purpose agent configurations**.

## User Feedback Summary
**Pain Points:**
- **Local model token inefficiency** (Issue #2917) – Users running local LLMs are paying a 27k-token overhead per request for MCP tool schemas, even when the local model is the orchestrator. For local deployments with limited context windows (Gemma4:31B), this is a meaningful cost that reduces effective conversation length.

- **Containerized attachment handling** (PRs #2694, #2695) – Signal users in container deployments face two blocking issues: DMs are silently dropped, and image attachments are unreadable. These are **critical user experience failures** that likely frustrate adoption among Signal-using teams.

- **Stale session handling** (PR #2184) – When a Claude Code session expires server-side, the raw error is delivered as a chat message before retrying. This is a visible user-facing bug that breaks conversational flow.

**Satisfaction Signals:**
- The **vibrant PR pipeline** (17 PRs updated in 24h from multiple contributors) indicates a healthy, engaged contributor community with solid code review practices (all PRs tagged with type and guidelines status).
- The addition of **productivity tools** (Google Contacts, CalDAV) and **new channels** (LINE) suggests user demand is being actively met with ecosystem expansion.

## Backlog Watch
The following items require maintainer attention due to age and unresolved status:

1. **PR #2184** (stale session handling, open since May 2) – 62 days old. A bug fix that masks a raw error from users. Likely needs review and merging—the fix appears self-contained and follows a clear pattern.

2. **PR #2348** (WhatsApp reconnect, open since May 8) – 57 days old. Large PR for channel stability; may require structural review. Could benefit from a maintainer assigning a reviewer.

3. **PR #2208** (HTTP/SSE MCP transport, open since May 3) – 61 days old. This is a **feature PR** that enables a major architectural capability. Its long open time suggests either review complexity, missing tests, or API design discussions.

4. **PR #2230** (rootless Podman user mapping, open since May 3) – 61 days old. Critical for users deploying with non-root container runtimes (e.g., GitHub Codespaces, some Kubernetes environments). The fix is small and well-scoped.

**Recommendation:** Consider batch-reviewing these older PRs (particularly #2184, #2230, and #2694/#2695 for Signal) to clear the backlog and resolve long-standing user-facing bugs. A minor release bundling these fixes would significantly improve stability for existing users.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-07-04

## Today's Overview
Project activity remains low, with only a single issue updated in the past 24 hours and no new pull requests or releases. The absence of merged PRs and new releases indicates the project is in a maintenance-watch state rather than active feature development. The singular open bug report (#972) continues to attract attention, suggesting users are encountering a recurring stability problem with the Telegram channel. Overall, project health appears stable but quiet, with maintainer bandwidth possibly focused on other priorities.

## Releases
No new releases were published today. The most recent release version remains unchanged, with no changelog entries or migration notes to report.

## Project Progress
No pull requests were updated, merged, or closed in the past 24 hours. No feature advances or fixes have been recorded for this period.

## Community Hot Topics
- **[Bug #972]** *"telegram channel stop respond after some idle time"* — This open issue, created by i11010520 on 2026-06-30 and last updated 2026-07-03, has 1 comment. It describes a scenario where the Telegram channel stops responding after a period of inactivity (e.g., overnight), while the underlying `nullclaw agent` continues to work normally when queried directly. This issue has no reactions, suggesting limited community engagement, but it represents the only active discussion point in the repository today.

- Link: [Issue #972](https://github.com/nullclaw/nullclaw/issues/972)

## Bugs & Stability
One open bug report is active:

**High Severity — Issue #972** (Telegram channel stops responding after idle time)  
- **Symptoms:** The Telegram integration dies silently after prolonged idle periods (e.g., after a night), requiring manual reconnection or restart. Backend functionality (`nullclaw agent -m "ping"`) continues to work, indicating the problem is isolated to the Telegram channel adapter or its connection handling.
- **Underlying need:** Users expect persistent, always-on connectivity for Telegram-based interactions, especially in environments where the agent runs unattended. The issue suggests a missing keepalive or reconnection mechanism.
- **No fix PR exists** as of this digest.

## Feature Requests & Roadmap Signals
No new feature requests were filed in the past 24 hours. The primary user demand evident from the active issue is for **improved connection resiliency** in the Telegram channel adapter. Based on this, the next potential version could include:
- A configurable idle-timeout or keepalive heartbeat for Telegram channels.
- An automatic reconnection routine that triggers when the channel detects silence for a threshold period.

## User Feedback Summary
The single open bug (#972) captures a key user pain point: the Telegram channel is unreliable for long-running, unattended usage. The user reports that the backend itself works correctly (proven by manual `ping`), which points to a disconnect between core agent health and channel-level connectivity. This suggests dissatisfaction with the Telegram integration’s stability, even while the core system is trusted. The lack of other feedback or praise in the project indicates either low engagement or a silent majority.

## Backlog Watch
There are no pull requests or older issues flagged for maintainer attention beyond the currently active bug. **Issue #972** should be considered a priority, given its impact on usability and the lack of any assigned milestone or maintainer response. The issue has been open for 4 days with only one user comment, which may indicate a need for maintainer triage or a status update.

- Unanswered issue: [Bug #972](https://github.com/nullclaw/nullclaw/issues/972)

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-04

## Today's Overview

IronClaw shows intense development activity with **50 PRs updated** in the last 24 hours (28 merged/closed) and **33 issues updated** (5 closed). The Reborn architecture migration dominates the codebase, with the team making significant progress on credential injection, identity management, and channel ingress infrastructure. Multiple QA-found bugs are being actively addressed, though **CI remains red on main** (Issue #5603) and several production-critical defects in the identity layer were identified. Two major PRs landed: a comprehensive type/trait cleanup (−176 lines, #5567) and a manifest-driven ingress route system (#5625). The project maintains high throughput but is clearly in a stabilization phase with the Reborn cutover approaching.

## Releases

**No new releases today.** The most recent release remains `ironclaw: 0.24.0`. However, a version bump PR (#5598) is open and would advance `ironclaw` from 0.24.0 to **0.29.1**—a significant increment indicating accumulated changes. This PR also notes breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), suggesting breaking API changes are pending release.

## Project Progress

**Key PRs merged/closed today (28 total):**

- **#5625** [CLOSED] — Manifest-projected host-ingress route + credential coherence. Re-derives the ingress concept atop current `ironclaw_host_api::ingress`, making Slack's inbound routes declared as data in extension manifests.
- **#5567** [CLOSED] — Massive type/trait cleanup: 6 traits removed, 6 DTO clusters unified, net −176 lines. Behavior-preserving refactor from the complexity audit.
- **#5619** [CLOSED] — Reborn identity layer de-slop: removed dead types, added boundary rules, CONTRACT docs, and error-path tests. Includes a DB migration.
- **#5624** [CLOSED] — Extracted host-runtime test harness + landing-policy doc, closing remaining follow-ups from #3231.
- **#5622** [CLOSED] — New `parallel-pr-review` skill that reviews multiple PRs simultaneously with subagents.
- **#5585** [CLOSED] — Refactored Reborn composition internals into clearer module boundaries (observability, lifecycle, trace capture).
- **#5107** [CLOSED] — Manifest-driven channel ingress contract covering auth, transport, secrets, and connect onboarding.
- **#5626** [OPEN] — Projects Slack ingress routes from the manifest, deleting Rust policy literals.
- **#5623** [OPEN] — Honors staged credential obligations for WASM egress, fixing a key credential injection bug.
- **#5621** [OPEN] — Experiment with OVH self-hosted runner for Reborn nextest archive production.

## Community Hot Topics

Most active discussions this period:

1. **[#3067 • 33 comments](https://github.com/nearai/ironclaw/issues/3067)** — [OPEN] Reborn integration test suite. This high-risk, P0-graded issue has been active since April, tracking end-to-end tests proving the substrate works through public entrypoints. The comment count reflects deep architectural design discussions around test strategy, not user confusion.

2. **[#3087 • 7 comments](https://github.com/nearai/ironclaw/issues/3087)** — [CLOSED] Composing `ironclaw_host_runtime` services. Now closed, this was a key architectural issue for wiring host runtime capabilities. Its closure signals progress on Reborn's service composition layer.

3. **[#5522 • 3 comments](https://github.com/nearai/ironclaw/issues/5522)** — QA bug: Reborn routine fails when Slack DM reading required but capability is missing. This is a real user-affecting bug where the agent enters a retry loop instead of gracefully reporting capability denial. The underlying need: users want clear error messages when their agent lacks permissions, not silent retries that cause confusing `Failed` status.

4. **[#5583 • 1 comment](https://github.com/nearai/ironclaw/issues/5583)** — Hallucinated call to disabled capability fails run as `model_error` instead of model-visible denial. A related UX concern: model errors should be surfaced gracefully.

## Bugs & Stability

**High Severity:**
- **[#5615](https://github.com/nearai/ironclaw/issues/5615)** (risk: high) — `bind()` has no OAuth-surface guard, defense-in-depth missing. Identified during identity layer audit. Fix in #5619.
- **[#5614](https://github.com/nearai/ironclaw/issues/5614)** (risk: high) — Cross-process divergent-email logins can split a principal. Process-local locking means two processes can mint separate identities for the same user. Fix in #5619.

**Medium Severity:**
- **[#5617](https://github.com/nearai/ironclaw/issues/5617)** (risk: medium) — OAuth login seam tested only with fakes on both sides—no integration test drives the full chain.
- **[#5616](https://github.com/nearai/ironclaw/issues/5616)** (risk: medium) — `adopt_migrated_identity` never writes `StoredUser` and reverses index/identity write order, creating "phantom users."
- **[#5608](https://github.com/nearai/ironclaw/issues/5608)** — Retry path unreachable for local-dev synthetic capabilities; retryable failures collapse into terminal `driver_unavailable`.
- **[#5605](https://github.com/nearai/ironclaw/issues/5605)** — Memory prompt-context injection is dead code in production; `memory_snippets` always empty.
- **[#5603](https://github.com/nearai/ironclaw/issues/5603)** — **CI red on main**: Docker Build missing prompts COPY + Clippy Windows unused import. This is blocking CI greenness.
- **[#5522](https://github.com/nearai/ironclaw/issues/5522)** — QA bug: Slack DM reading capability missing triggers retry loop, not graceful denial.
- **[#5512](https://github.com/nearai/ironclaw/issues/5512)** — WASM credential provider re-derives injection eligibility from manifest instead of consulting `Decision.obligations`. Fix in #5623.

**Low Severity (QA & UX):**
- **[#5510](https://github.com/nearai/ironclaw/issues/5510)** — Cannot delete old routines; forces complete restart to clear stale routines.
- **[#5507](https://github.com/nearai/ironclaw/issues/5507)** — Failed routine run shows "No thread attached," blocking debugging.
- **[#5602](https://github.com/nearai/ironclaw/issues/5602)** — Slack connection from chat returns pairing code instead of completing connection.

## Feature Requests & Roadmap Signals

- **Manifest-driven ingress (#5625, #5626)** — A clear architectural direction: moving from Rust-policy-literal ingress to manifest-declared routes for Slack, Telegram, and potentially all channels. This is landing now and likely to be in the next release.
- **Parallel PR review skill (#5622)** — New skill added today. The platform is actively expanding its skill ecosystem.
- **Reborn identity layer de-slop (#5619)** — The team is investing in production hardening of the identity system ahead of cutover.
- **Memory context injection fix (#5605)** — Once fixed, this will enable memory snippets in prompts, a key feature for agent context.
- **OVH self-hosted runner experiment (#5621)** — Infrastructure investment for faster CI, suggesting the team expects test volume to grow.

**Prediction for next release (0.29.x):** The open version bump PR #5598 (0.24→0.29) suggests a release is imminent. Expect the Reborn credential injection fix (#5623), manifest-driven ingress (#5625/5626), and identity hardening (#5619) to be included, plus the type cleanup (#5567) and composition refactor (#5585).

## User Feedback Summary

- **Slack connectivity pain (#5602, #5522):** Users report confusing Slack connection flows—pairing codes instead of completed connections, and silent retries when DMs require capabilities the agent lacks. The underlying issue: permission and authorization UX is unclear.
- **Routine management frustration (#5510, #5507):** Users cannot delete old routines or inspect failed ones. "No thread attached" on failures prevents debugging. This suggests the routine lifecycle UI/UX needs attention before general availability.
- **Capability denial transparency (#5583):** When an agent hallucinates a call to a disabled capability, the run fails silently instead of showing a clear denial message. Users need to understand what their agent can and cannot do.

## Backlog Watch

- **[#5221](https://github.com/nearai/ironclaw/issues/5221)** — Ironclaw harness backlog for `deepseek-v4-flash` (created June 25, updated July 3). Lists 12 candidate tasks for model harness support. No PR yet—moderate priority but no recent activity from the author.
- **[#3067](https://github.com/nearai/ironclaw/issues/3067)** — Reborn integration test suite (P0, high risk). Active since April 29 with 33 comments, but still open. This is the single most important test coverage gap for the Reborn cutover.
- **[#3141](https://github.com/nearai/ironclaw/issues/3141)** — Cost-based budgets into ResourceGovernor (P1, high risk). Open since May 1, last updated July 3. This is critical for production cost management and remains unassigned for implementation.
- **[#3127](https://github.com/nearai/ironclaw/issues/3127)** — Scalable capability permission UX (P1). Open since April 30. No implementation PR yet; this is foundational for user-facing capability management.
- **[#5595](https://github.com/nearai/ironclaw/issues/5595)** — Daily failure taxonomy (July 3). This recurring issue tracks benchmark failures and is healthy, but the high number of non-passing pinchbench tests (81/147 pass) indicates ongoing quality work.

---

*Generated from GitHub data for 2026-07-04. All links point to nearai/ironclaw on GitHub.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-07-04**.

---

## LobsterAI Project Digest | 2026-07-04

### 1. Today's Overview
The project had a high-activity day driven by the **merger of release/2026.7.1** into the main branch, which accounted for the bulk of the 16 updated PRs (14 closed/merged). A new minor release **2026.7.3** was cut, shipping several new features and critical fixes. While issue activity was minimal (1 stale issue closed), the development tempo was very strong, focusing on the **Cowork** sub-system, stability improvements, and UI/UX refinements. The project appears to be in a healthy release cycle with a clear focus on maturing its collaborative agent features.

### 2. Releases
**Version:** `LobsterAI 2026.7.3` (released 2026-07-03)
**Notable Changes:**
- **Service Deployment:** A new `feat: service deployment` by [@liugang519](https://github.com/liugang519) suggests improved infrastructure for deploying agents or backend services.
- **Cowork Goal Mode:** Introduction of a "goal mode" feature (`feat(cowork): add goal mode`), indicating a shift from simple chat to objective-driven agent collaboration.
- **Subagent Artifact Panel:** A new panel for subagent artifacts (`feat(cowork): add subagent artifact panel`) was added, enhancing the visibility of outputs from sub-agents.
**No breaking changes or migration notes were included in this release.**

### 3. Project Progress
Of the 14 closed/merged PRs today, the majority were bug fixes and minor improvements, but several major features landed:
- **Cowork Goal Mode (PR #2241):** The foundational implementation for goal-oriented coworking was released.
- **Service Deployment (PR #2238):** A new capability for deploying agents/services was introduced.
- **UI/UX Polish:**
    - Tooltips and authorization guidance for agent creation were improved (PR #2269).
    - Font size settings and settings UI were optimized (PR #2263).
- **Cowork Stability:**
    - **Context Maintenance Fix (PR #2266):** Clears stuck "context organizing/compacting" states on chat errors, preventing UI freezes.
    - **Plan Recovery Fix (PR #2247):** Prevents session file lock collisions during plan-mode recovery after an abort.
    - **Large Session Performance (PR #2264):** Reduces rendering workload in large, tool-heavy sessions and adds a diagnostics export tool.
- **macOS Stability (PR #2246):** Fixed a black screen issue when closing fullscreen apps.

### 4. Community Hot Topics
Activity focused entirely on internal development, with no significant community discussion in the last 24 hours. The only updated issue, **#1422** (a UI display bug for long MCP service names), was closed as stale.

### 5. Bugs & Stability
Several bugs were fixed today, indicating a strong push for stability in the Cowork module:
- **High Severity:**
    - **UI Stuck on Cowork Errors (PR #2266):** A bug causing the chat UI to remain stuck in a "compacting" state after an LLM timeout or error. **Fixed.**
    - **macOS Black Screen (PR #2246):** Closing a fullscreen app to the system tray caused a black screen. **Fixed.**
- **Medium Severity:**
    - **Subagent Panel Timestamps (PR #2261):** Timestamps in the subagent panel were incorrect due to alias errors in SQLite reads. **Fixed.**
    - **Cowork Add Menu Width (PR #2268):** The prompt add menu width was incorrect after UI changes. **Fixed.**
    - **Context Maintenance on Errors (PR #2266):** Failing compaction runs left the UI in a broken state. **Fixed.**
- **Low Severity:**
    - **Session Model Override Sync (PR #2267):** IM/channel sessions diverged from the local `modelOverride`. **Fixed.**

### 6. Feature Requests & Roadmap Signals
No new feature requests were made today. However, the heavy investment in **Cowork Goal Mode**, **context maintenance**, and **large session performance** strongly signals that the near-term roadmap is focused on making multi-agent collaboration reliable, persistent, and scalable. The addition of `service deployment` also suggests the project is moving toward an enterprise-grade deployment model.

### 7. User Feedback Summary
No direct user feedback was captured in today's data. The volume of fixes for "stuck states" (PR #2266, PR #2247) and "performance on large sessions" (PR #2264) implies these are common user pain points that the team is actively addressing. The removal of goal menu helper text (PR #2262) suggests a simplification of the UI following user confusion or feedback on the new goal mode.

### 8. Backlog Watch
Two older PRs remain open without recent maintainer activity:
- **PR #1353** ([Link](https://github.com/netease-youdao/LobsterAI/pull/1353)): A feature request for "Select All" and "Clear" buttons in the Agent skill selector (stale since April).
- **PR #1464** ([Link](https://github.com/netease-youdao/LobsterAI/pull/1464)): A fix to add duplicate validation for IM instance names (stale since April).

These are low-risk, well-defined improvements that could be considered for a future minor release, though they have not attracted any recent discussion.

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

# CoPaw Project Digest
**Date:** 2026-07-04

---

## 1. Today's Overview

CoPaw shows elevated activity today with **40 Issues** and **33 PRs** updated in the last 24 hours, indicating a significant development push. The project maintains strong community engagement with 26 closed Issues and 15 merged/closed PRs, reflecting responsive maintainer attention. Key themes dominating the past day include **context management stability** (scroll compression bug, malformed tool-call loops), **Runtime 2.0 refinements**, and **UI/UX polish** (session item unification, slash-command fixes). The 2.0 beta appears to be the primary workstream, with several first-time contributors submitting patches, signaling healthy open-source participation. No new releases were published today.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The latest releases remain unknown; users should check the project's releases page for the current stable version.

---

## 3. Project Progress

**Merged/Closed PRs (15 items):** Notable merged contributions include:

- **[#5648](https://github.com/agentscope-ai/CoPaw/pull/5648)** - `feat(memory): add configurable reranker for memory search` (lecheng2018) — Adds external rerank API support (e.g., SiliconFlow) to improve hybrid search result relevance. Backend config + implementation merged.
- **[#5647](https://github.com/agentscope-ai/CoPaw/pull/5647)** - `feat(memory): add reranker config panel to memory settings` (lecheng2018) — Frontend UI companion to #5648, providing collapsible reranker configuration in agent memory settings.
- **[#5525](https://github.com/agentscope-ai/CoPaw/pull/5525)** - `feat(sandbox): implement windows native sandbox` (ustc-mkh, first-time contributor) — Adds Windows-native sandbox support, a significant platform gap filled.
- **[#5735](https://github.com/agentscope-ai/CoPaw/pull/5735)** - `fix(providers): update GitHub Models to new endpoint and support fine-grained PAT` (wangfei010313) — Migrates from deprecated Azure endpoint to `models.github.ai/inference` and adds fine-grained PAT support.
- **[#5764](https://github.com/agentscope-ai/CoPaw/pull/5764)** - `feat: add request timeout, retry and AbortSignal support` (zhaozhuang521) — Adds configurable timeout (30s default), retry/retryDelay, and proper AbortSignal handling for improved resilience.
- **[#5506](https://github.com/agentscope-ai/CoPaw/pull/5506)** - `fix：sync execution_level to policy.yaml` (chenzhengcai, first-time) — Fixes policy execution level sync to `policy.yaml`, and respects `off` value for approval governance.
- **[#5754](https://github.com/agentscope-ai/CoPaw/pull/5754)** - `Session item unification` (zhaozhuang521, Under Review, merged) — Unifies sidebar and drawer session items into a single component.
- **[#5755](https://github.com/agentscope-ai/CoPaw/pull/5755)** - `fix(config): make agent resilient to invalid MCP client config` (rayrayraykk, Under Review, merged) — Prevents Pydantic validation failure from crashing entire agent config endpoint on bad MCP `transport` values.

**Still Open (18 PRs):** Several critical open PRs target 2.0 stability, including the scroll context compression fix ([#5765](https://github.com/agentscope-ai/CoPaw/pull/5765)) and the malformed tool-call fix ([#5761](https://github.com/agentscope-ai/CoPaw/pull/5761)).

---

## 4. Community Hot Topics

| Issue/PR | Title | Comments | Status |
|----------|-------|----------|--------|
| [#4559](https://github.com/agentscope-ai/CoPaw/issues/4559) | [Bug]: 超过40多个agent后 页面访问明显变慢 | 8 | CLOSED |
| [#5403](https://github.com/agentscope-ai/CoPaw/issues/5403) | [BUG] Browser autofill hijacks search input in Model Configuration page | 7 | CLOSED |
| [#4607](https://github.com/agentscope-ai/CoPaw/issues/4607) | [Bug]: 配置了环境变量NO_PROXY，好像没生效 | 6 | CLOSED |
| [#4625](https://github.com/agentscope-ai/CoPaw/issues/4625) | [Bug]: MiniMax-M2.5 思考过程返回 XML格式导致不兼容 | 6 | CLOSED |
| [#5705](https://github.com/agentscope-ai/CoPaw/issues/5705) | [Feature] 密钥脱敏与安全存储 | 6 | OPEN |
| [#4650](https://github.com/agentscope-ai/CoPaw/issues/4650) | [Bug]: GLM-5.1 reasoning chain not displayed via OpenAI-compatible API | 5 | CLOSED |
| [#5746](https://github.com/agentscope-ai/CoPaw/issues/5746) | [Bug]: 2.0 beta scroll 上下文压缩错误折叠当前任务 | 4 | OPEN |

**Analysis:** The community is strongly focused on **stability and edge-case fixes**. The most active issue ([#4559](https://github.com/agentscope-ai/CoPaw/issues/4559)) reveals a performance regression at scale (40+ agents). The top open feature request ([#5705](https://github.com/agentscope-ai/CoPaw/issues/5705)) around secret masking and log sanitization reflects growing enterprise/security-conscious usage. Notably, several closed bugs (browser autofill, proxy config, model compatibility) suggest maintainers are rapidly addressing reported issues, with a bias toward Chinese-language reporters indicating strong adoption in the CN market.

---

## 5. Bugs & Stability

**High Severity:**
- **[#5746](https://github.com/agentscope-ai/CoPaw/issues/5746)** — **2.0 beta: scroll context compression incorrectly collapses current task** — Causing model to reply with old messages mid-task. **Fix PR [#5765](https://github.com/agentscope-ai/CoPaw/pull/5765) is open** (niceIrene), adding active turn protection + graduated pressure relief.
- **[#5717](https://github.com/agentscope-ai/CoPaw/issues/5717)** — **Runtime 2.0 malformed tool-call history causes endless repeated tool execution** — Truncated JSON arguments lead to infinite loops. **Fix PR [#5761](https://github.com/agentscope-ai/CoPaw/pull/5761) is open** (wananing), surfaces malformed input to model.
- **[#5710](https://github.com/agentscope-ai/CoPaw/issues/5710)** — **Context compression has no protected anchor points** — Critical messages (group notifications, task instructions) can be truncated, breaking agent awareness. No fix PR yet.
- **[#5769](https://github.com/agentscope-ai/CoPaw/issues/5769)** — **2.0.0b2: Double `/api` prefix causes 404 on workspace commands endpoint** — Frontend construction bug (`/api/api/...`).

**Medium Severity:**
- **[#5759](https://github.com/agentscope-ai/CoPaw/issues/5759)** — Plan mode repeatedly reads the same unchanged file (1-2 comments).
- **[#5616](https://github.com/agentscope-ai/CoPaw/issues/5616)** — Automated tasks terminate unexpectedly with no manual intervention.
- **[#5763](https://github.com/agentscope-ai/CoPaw/issues/5763)** — Heavy tasks cause freezes and random interruptions in latest version.

**Lower Severity (Closed today):**
- [#5689](https://github.com/agentscope-ai/CoPaw/issues/5689) — Remote SSH plugin leaves artifacts after deletion (error on next start)
- [#5587](https://github.com/agentscope-ai/CoPaw/issues/5587) — Qwen-Image Tool install error
- [#5456](https://github.com/agentscope-ai/CoPaw/issues/5456) — Wrong agent identity for channel-built requests
- [#5183](https://github.com/agentscope-ai/CoPaw/issues/5183) — Pet feature broken on Wayland desktops

**Patch PRs merged today:** [#5735](https://github.com/agentscope-ai/CoPaw/pull/5735) (GitHub Models endpoint), [#5755](https://github.com/agentscope-ai/CoPaw/pull/5755) (MCP config resilience), [#5764](https://github.com/agentscope-ai/CoPaw/pull/5764) (timeout/retry), [#5768](https://github.com/agentscope-ai/CoPaw/pull/5768) (timezone-aware timestamps).

---

## 6. Feature Requests & Roadmap Signals

**High Likelihood for Next Release:**
- **[#5705](https://github.com/agentscope-ai/CoPaw/issues/5705)** — **Key/secret security improvements** (env var fallback coverage, log sanitization, ReMe log masking). Creates PR opportunities.
- **[#5609](https://github.com/agentscope-ai/CoPaw/issues/5609)** — **Custom model protocol** — Not all models use `/v1/chat/completions` (e.g., image generation endpoints). High impact for model diversity.
- **[#5711](https://github.com/agentscope-ai/CoPaw/issues/5711)** — **Competitive analysis & improvement roadmap** — Detailed gap analysis vs. industry tools (tool-call efficiency, memory, context handling).

**Medium Likelihood / Long-Term Signals:**
- **[#5767](https://github.com/agentscope-ai/CoPaw/issues/5767)** — **Console architecture limitation**: `@agentscope-ai/chat` SDK's single-session pull model blocks multi-agent/workspace evolution. Architectural change needed.
- **[#5547](https://github.com/agentscope-ai/CoPaw/issues/5547)** — **Plugin tool access to sessionId/user identity** — Needed for multi-tenant MCP tool authorization.
- **[#4642](https://github.com/agentscope-ai/CoPaw/issues/4642)** — **Plugin extensibility + workspace directory support** — Non-invasive hooks, custom agents.

**Low Likelihood / Niche:**
- [#5001](https://github.com/agentscope-ai/CoPaw/issues/5001) — 9router proxy support.
- [#4584](https://github.com/agentscope-ai/CoPaw/issues/4584) — Switch browser automation to Playwright for stability.

---

## 7. User Feedback Summary

**Pain Points:**
- **Context loss/corruption** in 2.0 beta (scroll strategy) — Users report "memory loss" mid-task, with AI responding to outdated messages ([#5746](https://github.com/agentscope-ai/CoPaw/issues/5746)).
- **Tool execution loops** from malformed JSON arguments ([#5717](https://github.com/agentscope-ai/CoPaw/issues/5717)).
- **Instability on heavy tasks** — Freezes and random terminations ([#5763](https://github.com/agentscope-ai/CoPaw/issues/5763), [#5616](https://github.com/agentscope-ai/CoPaw/issues/5616)).
- **Performance at scale** — >40 agents causes sluggishness ([#4559](https://github.com/agentscope-ai/CoPaw/issues/4559)).
- **Plugin lifecycle issues** — Improper cleanup after deletion ([#5689](https://github.com/agentscope-ai/CoPaw/issues/5689)).
- **Model compatibility** — GLM-5.1 reasoning chain not displayed ([#4650](https://github.com/agentscope-ai/CoPaw/issues/4650)), MiniMax-M2.5 XML format breakage ([#4625](https://github.com/agentscope-ai/CoPaw/issues/4625)).

**Satisfaction Indicators:**
- Rapid bug closure pace (26 Issues closed in 24h) suggests maintainers are responsive.
- Multiple first-time contributors submitting non-trivial patches (sandbox, config, JSON recovery) indicates good onboarding.
- Feature requests like secret security (#5705) show users trust CoPaw with production workloads.

**Use Cases Emerging:**
- **Enterprise deployment** — Multi-tenant MCP tool authorization, secret management, governance policy enforcement.
- **Heavy automation** — Plan mode, cron jobs, file processing.
- **Internationalization** — Chinese-language user base is very active; some English-language questions are present.

---

## 8. Backlog Watch

**Issues Needing Maintainer Attention:**
- **[#5547](https://github.com/agentscope-ai/CoPaw/issues/5547)** — "如何在plugin tool中获得当前的sessionId" — Open since Jun 26 (8 days), 2 comments. Unresolved plugin API gap blocking multi-tenant use cases.
- **[#5710](https://github.com/agentscope-ai/CoPaw/issues/5710)** — "上下文压缩无保护锚点" — Open since Jul 1 (3 days), 2 comments. No assignee or linked PR. Critical for context stability.
- **[#5616](https://github.com/agentscope-ai/CoPaw/issues/5616)** — "自动化任务,莫名其妙的终止" — Open since Jun 29 (5 days), 3 comments. Root cause unknown.

**Abandoned/Stale PRs:**
- **[#5514](https://github.com/agentscope-ai/CoPaw/pull/5514)** — "fix chat input queue session id migration" — Open since Jun 25 (9 days), no comments. Dependent on SDK upgrade; may be blocked.
- **[#5736](https://github.com/agentscope-ai/CoPaw/pull/5736)** — "add QwenPaw review bot" — Open since Jul 2 (2 days), no comments. CI infrastructure addition; low urgency.

**Overall Backlog Health:** The project is actively triaging issues, with most open Items either feature requests or critical 2.0 bugs that have corresponding fix PRs. The lack of stale assignee-less PRs is healthy. The main risk is the 2.0 beta stability (context compression, tool-call loops) which, if unresolved, could delay the stable 2.0 release.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-04

## Today's Overview

ZeroClaw remains in an intense development cycle, with 36 issues and 50 pull requests updated in the last 24 hours, reflecting a highly active contributor base. The project is shipping substantial architecture-level changes, including a prototype out-of-process WASM plugin execution sidecar (PR #8661), a multi-user authentication provider stack (PR #8672 as delivery for RFC #7141), and visual SOP authoring surfaces (PR #8590). A significant new severity-1 bug was discovered today—an approval gate bypass in the SOP engine (Issue #8678)—alongside continued fallout from long-standing Windows test failures (Issue #7462) and memory growth problems in the agent loop (Issue #8642). No new releases were published today; the project appears to be consolidating toward a v0.8.3 or v0.9.0 milestone.

## Releases

No new releases were published on 2026-07-04. The most recent pre-release information available in the tracker suggests the project is working toward **v0.8.3** (with trackers #7314, #8071, #8073) and **v0.9.0** (target for OIDC authentication, RFC #7141).

## Project Progress

**5 PRs merged/closed today** (of 50 updated). Notable advances:

- **SOP Engine Fix** (PR #8675, `fix(providers)`: omits empty assistant tool-call content in OpenAI-compatible provider requests—addresses the provider-400 empty-reply bug reported today in Issue #8675
- **Plugin Config Seeding** (PR #8662): fixes `zeroclaw plugin install` to seed config entries and surface malformed-section drops
- **Plugin Feature Graph Fix** (PR #8641): ensures backend WASM features imply `plugins-wasm` itself, preventing silent missing-subcommand binaries
- **Feature: Cron Memory Flag** (PR #8676): exposes per-cron-job `uses_memory` flag in CLI, tools, and gateway API (responds to Issue #8397)
- **Skill Install Refactor** (PR #8335): makes skills install/list/remove bundle-aware for multi-agent deployments

Key infrastructure work advanced: PR #8661 (prototype out-of-process WASM plugin host sidecar), PR #8638 (replaces hardcoded ClawHub with git-catalog skill installer), and PR #8590 (visual SOP authoring with channel fan-in and tests).

## Community Hot Topics

| Issue/PR | Comments | Topic |
|----------|----------|-------|
| [#6808 RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) | 13 | Governance RFC, accepted, rollout in progress since v0.8.0-beta-1 |
| [#7462 74 test failures on Windows](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | 8 | Unix-only test commands, path semantics, console encoding |
| [#5542 Consecutive OOM in WSL2 (CLOSED)](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) | 7 | Multi-root-cause tracker, split into #8633 and #8642 |
| [#7141 RFC: OIDC authentication provider support](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) | 7 | Security/architecture umbrella, target v0.9.0 |

The most active discussion continues around **Windows CI parity** (Issue #7462) and **memory management** (Issue #5542 root cause split). The OIDC RFC (#7141) has strong community interest and now has a delivery PR (#8672) in open review. The workflow governance RFC (#6808) represents a long-running effort (since May 2026) to make issue routing less manual.

## Bugs & Stability

### Critical/High Severity (S0–S1, newly reported today)

| Issue | Severity | Summary | Fix PR Exists? |
|-------|----------|---------|----------------|
| [#8678 SOP approval gate bypass](https://github.com/zeroclaw-labs/zeroclaw/issues/8678) | S2 | `advance_step` has no run-status guard—driver can bypass approval gate via `sop_advance` | No |
| [#8675 Malformed tool-call arguments → provider 400](https://github.com/zeroclaw-labs/zeroclaw/issues/8675) | S1 | OpenAI-wire-format providers re-serialize tool_calls verbatim without JSON validation | Yes (PR #8524) |
| [#8654 skill-review fork panic → daemon SIGSEGV](https://github.com/zeroclaw-labs/zeroclaw/issues/8654) | S1 | Out-of-range slice in `skills/review.rs:159` panics under `panic=abort` | No |
| [#8642 MCP/tool-schema cloning → unbounded RSS growth](https://github.com/zeroclaw-labs/zeroclaw/issues/8642) | S1 | Split from #5542, separate from restart-storm fix #8633 | No |

### Ongoing High-Severity Bugs (previously reported)

| Issue | Summary |
|-------|---------|
| [#8631 Headless deterministic SOP steps recorded Completed without executing](https://github.com/zeroclaw-labs/zeroclaw/issues/8631) | False-green audit trail |
| [#8563 SOPs unavailable through web dashboard chat](https://github.com/zeroclaw-labs/zeroclaw/issues/8563) | Shared SOPs not detected by agent runtime |
| [#8627 WhatsApp Web device linking broken by new passkey gate](https://github.com/zeroclaw-labs/zeroclaw/issues/8627) | Blocked on WhatsApp infrastructure change |
| [#8632 Source install with embedded-web fails before API client generated](https://github.com/zeroclaw-labs/zeroclaw/issues/8632) | Build order dependency |

## Feature Requests & Roadmap Signals

**Proxy requests gaining traction:**
- **Goal Mode** (Issue #8303, 3 comments, 1 👍): First-class durable mode for bounded autonomous sessions. PR #8393 is open with implementation, likely for v0.8.3 or v0.9.0
- **Uses_memory UI** (Issue #8677, created today): Request for web gateway checkbox for cron job memory context. PR #8676 already implements the backend
- **ZeroCode UX enhancements** (Issues #8653, #8664, #8652): Auto-resume sessions, fence copy fix, dismissal behavior—all filed by core contributor Audacity88, expected in near-term ZeroCode releases
- **Plugin & Skills Ecosystem** (Issue #8636): Follow-ups from third-party plugin authoring guide validation—signals community adoption beginning

**Likely for next release (v0.8.3):**
- Goal mode implementation (#8303 / #8393)
- WASM plugin out-of-process sidecar (#8661)
- Git-catalog skill installer (#8638)
- Cron uses_memory exposure (#8397 / #8676)

**Likely for v0.9.0:**
- OIDC multi-user authentication (#7141 / #8672)
- Full SOP visual authoring (#8590)

## User Feedback Summary

**Pain points expressed in the last 24 hours:**
- **Windows parity**: "74 test failures on Windows... CI does not catch this because Test job only runs on Linux" (#7462)
- **Memory pressure**: Two distinct memory issues identified—WSL2 OOM restart storms (fix in #8633) and a separate unbounded RSS growth from MCP tool-schema cloning (#8642)
- **Provider compatibility**: "Malformed native tool-call arguments sent unvalidated to OpenRouter/OpenAI-format providers → provider 400 → empty reply" (#8675)—significant for users relying on alternative inference providers
- **SOP reliability**: Steps recorded as completed without executing (#8631), and SOPs not available through web dashboard (#8563)
- **WhatsApp channel**: Complete workflow block for WhatsApp Web users due to Meta's new passkey/SHORTCAKE linking requirement (#8627)

**Satisfaction signals:**
- Plugin authoring guides (PR #8621) have already been validated by a third-party integrator, leading to Issue #8636 for follow-ups—positive sign for developer adoption
- RFC #8303 (goal mode) has community 👍 and engagement

## Backlog Watch

**Issues needing maintainer attention:**

| Issue | Age | Priority | Reason for Watch |
|-------|-----|----------|------------------|
| [#7462 74 Windows test failures](https://github.com/zeroclaw-labs/zeroclaw/issues/7462) | 24 days | P1 | No fix PR exists; CI blind spot blocks Windows users |
| [#8627 WhatsApp Web broken](https://github.com/zeroclaw-labs/zeroclaw/issues/8627) | 2 days | P1 | Blocked on external dependency (Meta's infrastructure); no workaround documented |
| [#8519 Cargo audit ignore drift / wasmtime-wasi CVEs](https://github.com/zeroclaw-labs/zeroclaw/issues/8519) | 4 days | P1 | In-progress; 22 RustSec advisories failing CI, audit.toml/deny.toml out of sync |
| [#8632 Source install build failure](https://github.com/zeroclaw-labs/zeroclaw/issues/8632) | 2 days | P1 | In-progress; blocks anyone building from source with embedded-web |
| [#8654 skill-review fork panics](https://github.com/zeroclaw-labs/zeroclaw/issues/8654) | 1 day | P1 | Unresolved; causes daemon SIGSEGV after tool-heavy turns |

**PRs needing review:**
- [#8393 Goal mode implementation](https://github.com/zeroclaw-labs/zeroclaw/pull/8393): 6 days open, needs-author-action label—substantial feature delivery for accepted RFC
- [#8335 Bundle-aware skills installer](https://github.com/zeroclaw-labs/zeroclaw/pull/8335): 9 days open, high risk, multi-agent deployment criticality
- [#7946 Context window usage bar](https://github.com/zeroclaw-labs/zeroclaw/pull/7946): 14 days open, touches multiple chat surfaces (ZeroCode TUI, gateway, CLI)

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*