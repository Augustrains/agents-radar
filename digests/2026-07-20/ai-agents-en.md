# OpenClaw Ecosystem Digest 2026-07-20

> Issues: 352 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-20 01:26 UTC

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

# OpenClaw Project Digest — 2026-07-20

## Today's Overview

OpenClaw remains in an intensely active development phase, with **352 issues** and **500 pull requests** updated in the last 24 hours. The project shows strong maintainer engagement—119 issues were closed and 160 PRs were merged or closed—though the 340 open PRs and 233 open/active issues indicate a growing backlog. Security and session-state reliability dominate the conversation, with a cluster of P1/P2 regressions following the recent 2026.7.1 release. No new releases were cut today, but a major refactoring tranche (PR #111527) is awaiting product decisions, suggesting a release may be imminent once these consolidations land. The project appears to be in a stabilization phase following a feature-heavy period, with maintainers prioritizing regressions and security hardening.

## Releases

No new releases today. The latest release remains **2026.7.1** (preceded by 2026.7.2-beta.3), which introduced regressions around tool-call schemas (Issue #108075, #108580) and session context tracking (Issue #108238). Users upgrading to 2026.7.1 have encountered provider schema rejections, llama.cpp grammar incompatibilities, and false context-overflow triggers.

## Project Progress

Today saw **160 merged/closed PRs**, with notable advances:

- **Security hardening:** A series of PRs from `zhanxingxin1998` introduced bounded file reads across the codebase—APNs keys (PR #111588), TLS certs (PR #111586), models.json catalogs (PR #111589), config includes (PR #111591), and Synology Chat env overrides (PR #111590)—addressing unbounded `fs.readFile` vulnerabilities.
- **Kimi K3 fix:** PR #111587 and PR #111599 resolved a critical regression where Kimi K3 subscribers on higher tiers could not use their full 1M context window, with the `k3[1m]` model alias failing with HTTP 401.
- **Telegram link preview fix:** PR #111546 closed Issue #111525, honoring `linkPreview: false` settings on streamed replies (previously only worked on non-streamed messages).
- **Apple client unification:** PR #111598 (refactored Apple offline client databases) merged, aligning iOS and macOS storage implementations—a foundational change for multi-device support.
- **UI improvements:** PR #111530 added drag-and-drop attachment support to the new-session composer, and PR #111583 introduced agent-controlled session status (attention flags, TTL) in the sessions tool.
- **Cron env fix:** PR #106100 fixed a bug where non-string env values silently wiped the entire environment for command cron jobs.

## Community Hot Topics

1. **[Issue #75] Linux/Windows Clawdbot Apps** (114 comments, 👍80)  
   *URL: openclaw/openclaw/issues/75*  
   Still the most active issue by far, this long-standing feature request for desktop clients on Linux and Windows continues to gather interest. The high reaction count signals strong community desire for platform parity with macOS/iOS. No maintainer response in recent days, though PR #111596 (Windows catalog session grouping) shows Windows-specific work continues.

2. **[Issue #7707] Memory Trust Tagging by Source** (17 comments)  
   *URL: openclaw/openclaw/issues/7707*  
   This security-focused feature request proposes tagging agent memories by trust level to prevent poisoning attacks. The 0 reactions suggest it's a niche but technically sophisticated ask from security-conscious users. No PRs yet, but it aligns with the project's growing security emphasis.

3. **[Issue #79077] Telegram Bot-to-Bot and Guest-Bot Modes** (11 comments, 👍8)  
   *URL: openclaw/openclaw/issues/79077*  
   Telegram's May 2026 platform update introduced new bot features; the community wants OpenClaw to support them. The high ratio of reactions to comments (8:11) indicates broad interest but limited detailed discussion. No linked PRs—likely awaiting product decision.

4. **[Issue #110950] Everything is a Cron** (7 comments, 👍2)  
   *URL: openclaw/openclaw/issues/110950*  
   A maintainer-authored proposal (by `steipete`) to unify heartbeat, watchers, and scheduled automation into a single cron primitive. This architectural shift would simplify the codebase but represents a breaking conceptual change. The recent update timestamp suggests active discussion.

5. **[Issue #108075] 2026.7.1 Provider Schema Rejection** (10 comments, closed)  
   *URL: openclaw/openclaw/issues/108075*  
   A P1 regression where the 2026.7.1 release caused LLM provider requests to be rejected due to invalid tool payload schemas. Closed today—the fix was likely included in one of the many merged PRs.

## Bugs & Stability

### P1 Regressions (Critical)

- **[Issue #108075]** 2026.7.1 provider schema rejection — *CLOSED*  
  **Impact:** All agent runs fail with "provider rejected the request schema." Fix merged.

- **[Issue #108580]** cron tool schema incompatible with llama.cpp grammar-constrained tool calling — *OPEN*  
  **Impact:** All chat requests fail for llama.cpp users, not just cron-related ones. No fix PR linked yet.

- **[Issue #108238]** Session context wrongly includes cacheRead in totalTokens, triggering false compression — *CLOSED*  
  **Impact:** Large-context model users see false context-overflow warnings and compaction failures. Fixed via linked PR.

- **[Issue #111519]** Telegram DM reply ownership lost after stale DM-scope cleanup in 2026.7.2-beta.3 — *OPEN*  
  **Impact:** Normal agent replies lose reply-to ownership, only delivered through fallback path. No fix PR yet.

### P2 Issues (Moderate Severity)

- **[Issue #111506]** Session lock contention on heavy contexts with rapid-fire requests — *OPEN*  
  **Impact:** LM Studio backend users with 180+ message histories experience deadlocks as agents fire requests every 1-2 seconds without waiting for previous streams to finish.

- **[Issue #109490]** Codex app-server turn interrupted after client-delegated message tool result — *OPEN*  
  **Impact:** Agents sending progress messages ("I'll do X now") via delegated tools never continue working after the message is sent.

- **[Issue #94846]** Cron isolated agentTurn treats recovered tool errors as fatal — *OPEN*  
  **Impact:** Scheduled runs that recover from early errors still get marked as failed, preventing proper completion.

- **[Issue #99910]** Memory dreaming run pegs gateway event loop for ~10 minutes — *OPEN*  
  **Impact:** Short-term memory promotion runs make the gateway completely unresponsive; channels drop.

### Stability Notes

The 2026.7.1 release introduced multiple regressions across tool schemas, context tracking, and Telegram delivery. While the schema and context bugs have been closed, the Telegram regression and llama.cpp incompatibility remain open. Several of today's merged PRs (especially the bounded file-read series) are proactive hardening rather than bug fixes.

## Feature Requests & Roadmap Signals

**Likely for next release (based on maintainer activity):**

1. **Config-surface reduction (PR #111527)** — This "review request" PR consolidates configuration options, removing the commitments feature and productizing several extensions. It's tagged `maintainer` and awaiting product decisions, suggesting it's a priority for the next release once approved.

2. **Agent-controlled session status (PR #111583)** — Agents can now set attention flags, status lines, and TTL via the sessions tool. The maintainer has already merged this, so it will ship.

3. **Pinned MCP apps dashboard (PR #111524)** — Adds rendering, lease re-minting, and durable tool grants for pinned MCP app widgets. This is a substantial feature for power users.

**Medium-term signals:**

- **Memory Trust Tagging (Issue #7707)** and **Masked Secrets (Issue #10659)** — Both are P2 security features with `needs-product-decision` labels. The security hardening in today's PRs suggests the project is receptive, but these require architecture changes.

- **Skill Permission Manifest (Issue #12219)** — A standard for skills to declare permissions. Related to the security theme, but no PR activity yet.

- **WhatsApp call events (Issue #7540)** and **listen-only mode (Issue #78963)** — Both are channel-specific enhancements that would expand monitoring capabilities.

- **"Everything is a Cron" (Issue #110950)** — A maintainer-proposed architectural refactor. If accepted, this would fundamentally change automation in OpenClaw but isn't urgent.

## User Feedback Summary

**Pain points:**

- **Upgrade regressions dominate frustration.** Multiple users report that upgrading to 2026.7.1 broke their workflows—provider schema rejections, Telegram delivery issues, context tracking bugs. The community is vocal about wanting more thorough regression testing before releases.
- **Cross-platform gaps continue.** Issue #75 (Linux/Windows clients) remains the most-upvoted issue (👍80). Windows users also report catalog session grouping bugs (PR #111596). The macOS/iOS client advantage is a persistent source of dissatisfaction for non-Apple users.
- **Configuration complexity.** PR #111527 explicitly addresses "config-surface reduction," acknowledging that configuration has grown too large. Users are reporting confusion around settings that conflict (Issue #97970—`gateway.bind: lan` vs `auth.mode: none`) or are silently ignored (Issue #110065—`compaction.enabled` read but not in schema).

**Positive signals:**

- **Security responsiveness earns trust.** The rapid series of bounded-file-read fixes and the community's engagement with security-focused issues (Memory Trust Tagging, Masked Secrets) shows the project takes security seriously.
- **Transparent development process.** The "review request" PR for config changes (#111527) and the detailed changelogs demonstrate maintainers' commitment to community involvement in breaking changes.
- **User needs are heard.** Telegram link preview suppression, drag-and-drop UI, and session status controls were user requests that shipped quickly.

## Backlog Watch

| Issue/PR | Age | Status | Why It Matters |
|----------|-----|--------|----------------|
| **Issue #75** (Linux/Windows apps) | 201 days | OPEN, 114 comments, 👍80 | Most-voted issue; no maintainer response in recent days despite continued community interest |
| **Issue #7707** (Memory Trust Tagging) | 167 days | OPEN, needs product decision | Addresses a genuine security threat (memory poisoning); no PR movement |
| **Issue #11665** (Webhook multi-turn sessions) | 162 days | OPEN, linked PR open | Documentation says feature works but code always creates new sessions; users hit this daily |
| **Issue #6615** (Exec denylist support) | 169 days | OPEN, needs product decision | Users want "allow everything except X" policies; relatively simple ask with no movement |
| **Issue #8355** (Streaming TTS for voice calls) | 167 days | OPEN, needs live repro | Voice call latency is a known UX problem; feature description includes technical approach |
| **PR #91268** (Doctor misreports trusted-proxy gateways) | 43 days | OPEN, needs proof | Fix exists but hasn't been reviewed; affects users deploying behind reverse proxies |
| **PR #83933** (Cron deleteAfterRun for manual runs) | 62 days | OPEN, needs proof | Manual cron runs incorrectly consume one-shot jobs; PR has been waiting >60 days for review |

The most concerning backlog item remains **Issue #75**—the Linux/Windows client request has been open for nearly 7 months with 114 comments and 80 upvotes, yet no recent maintainer engagement. For a project with "open" in its name, the lack of non-Apple desktop support is the single largest source of user dissatisfaction. The **exec denylist** (Issue #6615) and **webhook sessions** (Issue #11665) are simpler requests that could be addressed quickly to reduce user friction.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the community digest summaries for 2026-07-20.

---

## Cross-Project Ecosystem Comparison Report: 2026-07-20

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem remains in a state of hyperactive maturation, characterized by intense development velocity, a growing focus on security hardening and session-state reliability, and a clear bifurcation between projects prioritizing architecture refactoring and those stabilizing for user-facing releases. A dominant trend is the convergence on multi-channel support (WeChat, Discord, Teams, Mattermost) and extensibility via MCP (Model Context Protocol) servers, signaling a shift from single-chat interfaces to platform-agnostic agent infrastructure. Community feedback consistently emphasizes reliability, cross-platform parity (especially Windows/Linux), and observable performance, with several projects experiencing regression fatigue from rapid release cycles. The overall landscape shows a healthy but strained maintainer bandwidth, with many high-value PRs and issues languishing due to review bottlenecks.

### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status (24h) | Community Health Score |
|---|---|---|---|---|
| **OpenClaw** | 352 | 500 | No new release (2026.7.1 latest) | 8/10 - High activity, strong maintainer engagement but growing backlog |
| **NanoBot** | 6 | 30 | No new release | 7/10 - Healthy bug fixing and channel refactoring |
| **Hermes Agent** | 50 | 50 | No new release | 7/10 - Intense bug-fixing, but stretched maintainer attention |
| **NanoClaw** | 2 | 40 | No new release | 8/10 - High merge velocity, low new-issue count |
| **IronClaw** | 5 | 50 | No new release (Reborn refactoring) | 8/10 - Disciplined, focused execution on architecture milestone |
| **ZeroClaw** | 33 | 48 | No new release (v0.8.4 target July 31) | 6/10 - High activity but review bottlenecks on critical PRs |
| **CoPaw** | 12 | 6 | No new release (v2.0.0.post3 latest) | 6/10 - Active triage but regression issues following latest release |
| **Moltis** | 1 | 1 | **New release: 20260719.01** | 4/10 - Low activity, single feature conversation ongoing |
| **PicoClaw** | 4 | 3 | No new release | 4/10 - Stalled PRs, maintainer attention divided |
| **LobsterAI** | 3 | 3 | No new release | 2/10 - Low-activity maintenance phase, stale backlog |
| **NullClaw** | 0 | 0 | Inactive | N/A |
| **TinyClaw** | 0 | 0 | Inactive | N/A |
| **ZeptoClaw** | 0 | 0 | Inactive | N/A |

**Average PR velocity:** ~70-80 PRs per day across active projects. **Median issues updated:** ~5-6 (excluding OpenClaw outlier).

### 3. OpenClaw's Position

**Advantages:**
- **Ecosystem Leader in Scale:** With 352 issues and 500 PRs updated in 24 hours, OpenClaw dwarfs all other projects in raw development activity. This reflects the largest contributor base and maintainer team.
- **Security Responsiveness:** The rapid series of bounded-file-read fixes (APNs keys, TLS certs, config includes) demonstrates a proactive security posture that sets a benchmark for the ecosystem.
- **Feature Completeness:** OpenClaw offers the broadest range of integrations (Telegram, Kimi, Apple clients) and UI polish (drag-and-drop, session status controls).

**Technical Approach Differences:**
- **Config Centralization:** OpenClaw is actively *reducing* its configuration surface (PR #111527), while other projects like ZeroClaw are adding more granular config options (per-SOP policies, live config reloads).
- **Architecture Philosophy:** OpenClaw leans toward a monolithic reference architecture, while projects like IronClaw and NanoBot are refactoring toward self-contained modules (channels, capabilities) and WASM-based plugin systems.

**Community Size Comparison:**
- **OpenClaw** (352 issues, 500 PRs) eclipses **ZeroClaw** (33 issues, 48 PRs) and **NanoClaw** (2 issues, 40 PRs) by an order of magnitude in activity.
- The most-voted issue on OpenClaw (#75, Linux/Windows apps, 👍80) highlights a persistent gap that ZeroClaw and NanoClaw are actively filling with multi-platform support.
- OpenClaw's maintainer/contributor ratio appears lower (more PRs per maintainer), contributing to its growing backlog.

### 4. Shared Technical Focus Areas

1. **Cost Tracking & Observability (OpenClaw, Hermes, NanoBot)**
   - Users demand real-time session cost visibility, accumulator persistence across restarts, and pre-emptive rate-limit management.
   - Hermes has the most acute pain: cost resets on gateway restart and accumulator overwrites.

2. **MCP Ecosystem Expansion (OpenClaw, NanoClaw, ZeroClaw, CoPaw)**
   - Multiple projects are adding remote MCP server support (HTTP/SSE), in-tree MCP servers (yt-dlp, ffmpeg), and durable tool grants.
   - ZeroClaw and NanoClaw are furthest ahead with WASM-based runtime plugins.

3. **Session State Integrity (OpenClaw, Hermes, IronClaw)**
   - Across projects, session context tracking, cache management, and compression triggering are recurring pain points.
   - IronClaw is the most architecturally rigorous, with formal error-recoverability contracts and crash-consistency test suites.

4. **Channel Expansion (NanoClaw, ZeroClaw, CoPaw, Hermes)**
   - WeChat, Discord, Mattermost, Microsoft Teams, Nextcloud Talk are being added across projects simultaneously.
   - WhatsApp LID migration is causing fix fatigue for NanoClaw and ZeroClaw.

5. **Windows & Linux Parity (OpenClaw, ZeroClaw, NanoBot)**
   - OpenClaw's most upvoted issue; ZeroClaw has multiple Windows-specific bugs (startup failure, CI tests).
   - NanoBot had Windows UTF-8 encoding and management shim bugs fixed this update.

### 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes | NanoClaw | IronClaw | ZeroClaw |
|---|---|---|---|---|---|
| **Target User** | End-users, power users | Dev-ops professionals, enterprise | Community plugin developers | Architects, core devs | Self-hosters, ML researchers |
| **Primary Feature** | Broadest integration set, UI polish | Session state, billing, kanban workers | Multi-channel expansion, skills | Architecture refactoring (Reborn) | WASM plugins, agent governance |
| **Architecture** | Monolithic, reference implementation | Modular, agent-runtime focused | Plugin-centric, multi-channel | Module-capability paradigm | Plugin-based, RFC-driven |
| **Release Maturity** | Stable with regressions | Active stabilization | High-velocity merging | Pre-release refactoring | v0.8.x maintenance, v0.9.0 planned |
| **Community Governance** | Transparent but backlogged | Needs-decision bottleneck | Core-team driven | Disciplined, formal RFCs | RFC-heavy, author-action stalls |

### 6. Community Momentum & Maturity

**Tier 1: Hyperactive Velocity (10+ PRs merged/day)**
- **OpenClaw** & **NanoClaw** & **IronClaw** — These projects are merging code at an industrial pace, with disciplined or high-velocity cadences. OpenClaw is post-feature, stabilizing; IronClaw is refactoring foundations; NanoClaw is feature-bloating.

**Tier 2: Active & Healthy (5-10 PRs merged/day)**
- **ZeroClaw, Hermes, NanoBot** — Significant activity but with visible bottlenecks (review delays, needs-author-action labels). These projects have strong roadmaps but risk stalling if maintainer bandwidth doesn't scale.

**Tier 3: Low Activity / Maintenance**
- **CoPaw, PicoClaw** — Building community but with lower velocity. CoPaw has good triage but regression issues; PicoClaw has stalled PRs.
- **Moltis, LobsterAI** — Stable but quiet; minimal new feature work. Stale backlogs and unanswered issues risk community disengagement.

**Tier 4: Inactive**
- **NullClaw, TinyClaw, ZeptoClaw** — No recent development activity.

### 7. Trend Signals

1. **From Single-Chat to Agent Infrastructure:** The proliferation of channels (WeChat, Teams, Discord, Mattermost) and MCP servers confirms that AI agents are expected to be platform-agnostic middleware, not single-bot interfaces.

2. **Security as a First-Class Concern:** Bounded file reads (OpenClaw), memory trust tagging, credential swapping safeguards (Hermes), sandbox fallback governance (CoPaw), and confused deputy protections (ZeroClaw) show the ecosystem is maturing from "does it work?" to "is it secure?"

3. **Architecture Debt is the New Normal:** IronClaw's Reborn, ZeroClaw's WASM plugins, and NanoBot's channel refactoring all signal that first-generation architectures are straining under feature growth. Developers should expect breaking changes as projects consolidate.

4. **Observability & Cost Control are Non-Negotiable:** Hermes's cost tracking bugs and NanoBot's unmetered token waste (trigger delivery to disabled channels) highlight that users want to know what their agent costs, in real time, and stop it when it's broken.

5. **The LLM Provider Bottleneck Remains:** Caching failures with Ollama (NanoBot), schema rejections (OpenClaw), and retry loop inefficiencies (Hermes) show that agent reliability is still tightly coupled to provider reliability. Self-hosted and local model users have the worst experiences.

6. **Desktop is the Battleground:** OpenClaw's most-voted feature request is cross-platform desktop clients. ZeroClaw, NanoBot, and CoPaw all had Windows or Linux-specific fixes. The platform that delivers seamless desktop experiences (macOS, Windows, Linux) first will capture disillusioned users.

**Value for AI Agent Developers:**
- **Prioritize observability and cost tracking** — users will pay for agents they can monitor and budget.
- **Invest in MCP and WASM plugin extensibility** — the next wave will be teams building custom integrations, not using built-in ones.
- **Expect breaking architecture changes** — choose projects with clear RFC processes (IronClaw, ZeroClaw) if stability matters; choose high-velocity projects (NanoClaw) for rapid feature iteration.
- **Windows/Linux support is a competitive moat** — the market for non-macOS agent users is underserved and growing.
- **Channel diversity matters more than UI polish** — users want agents on *their* platform (WeChat, Teams, Discord) more than they want drag-and-drop compose bars.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-07-20  
**Period Covered:** Last 24 hours

---

## 1. Today's Overview

NanoBot saw **high activity** over the past 24 hours, with **6 issues updated** (5 closed, 1 open) and **30 pull requests updated** (9 merged/closed, 21 open). The project maintained strong momentum in both bug fixing and feature development, with several high-priority PRs moving through review. Notably, multiple contributors focused on channel-specific fixes (Telegram, Feishu, WhatsApp, QQ), platform compatibility (Windows UTF-8, GitStore working directory), and a significant architectural refactor to make built-in channels self-contained. No new releases were published today. The project appears healthy with a balanced mix of community bug reports, maintainer-driven improvements, and external contributions.

---

## 2. Releases

No new releases were published during this period.

---

## 3. Project Progress

**9 pull requests were merged or closed** in the last 24 hours. Key merged PRs include:

- **#4990** (`fix(triggers): reject deliveries to disabled channels`) — Closes the bug where local triggers would run agent turns after their target channel was disabled, consuming model usage unnecessarily. Submitted by the same reporter who opened the related issue (#4991).  
  [GitHub: PR #4990](https://github.com/HKUDS/nanobot/pull/4990)

- **#4834** (`fix(whatsapp): allow group ids in allowFrom`) — Restores WhatsApp group allowlist support by accepting both the incoming group JID and its bare group ID in the allowlist. This was a regression reported in issue #4823.  
  [GitHub: PR #4834](https://github.com/HKUDS/nanobot/pull/4834)

- **#4908** (`refactor(channels): make built-in channels self-contained`) — Major architectural refactor removing central coupling around channel discovery, setup, runtime loading, WebUI metadata, and i18n. All built-in channels are now self-contained packages. This is a follow-up to #4855.  
  [GitHub: PR #4908](https://github.com/HKUDS/nanobot/pull/4908)

- **#4994** (`fix(webui): resolve Windows package manager shims`) — Fixes Windows compatibility where `bun.cmd` shims were not properly resolved by `shutil.which()`.  
  [GitHub: PR #4994](https://github.com/HKUDS/nanobot/pull/4994)

- **#4995** (`fix(channels): complete dependency manifest migration`) — Completes the migration from channel extras to package-owned manifest dependencies, adding `nanobot plugins install` for CI/image installs.  
  [GitHub: PR #4995](https://github.com/HKUDS/nanobot/pull/4995)

**Open PRs of note:** 21 open PRs remain, including the session-scoped model presets (#4866), Nimble search provider (#4951), Atlas Cloud provider support (#4996), secure browser companion launch (#4997), and multiple channel-specific fixes.

---

## 4. Community Hot Topics

### Most Active Issues

1. **#1459** — `nanobot with codex-5.3-codex is lazy and doesn't actually execute`  
   - **Status:** OPEN (since 2026-03-03)  
   - **Comments:** 6 | 👍: 2  
   - **Analysis:** This long-standing issue describes a core behavioral problem where NanoBot claims it will perform an action (reading a file) but does not actually execute. The user reports frustrating back-and-forth with the agent that never leads to actual work being done. This suggests either a prompt engineering defect, an issue with tool-calling reliability, or a misunderstanding in how the agent communicates its capabilities. The 4-month open duration with only 2 upvotes suggests it may be model-specific or environment-specific rather than a universal bug.  
   [GitHub: Issue #1459](https://github.com/HKUDS/nanobot/issues/1459)

2. **#4867** — `[enhancement] Preserve exact prompt prefix to enable caching in Ollama and others`  
   - **Status:** CLOSED  
   - **Comments:** 9 | 👍: 0  
   - **Analysis:** User reports that Ollama adds 60 seconds per turn due to NanoBot not preserving the exact prompt prefix, preventing KV-cache reuse. This is described as "totally unusable with Ollama and 32 GB of VRAM." The 9 comments indicate significant discussion. Closed without resolution visible in the digest — may have been redirected or resolved via configuration.  
   [GitHub: Issue #4867](https://github.com/HKUDS/nanobot/issues/4867)

3. **#4823** — `[bug, regression] whatsapp - groups`  
   - **Status:** CLOSED  
   - **Comments:** 4 | 👍: 0  
   - **Analysis:** User reported that WhatsApp group responses now arrive in every group instead of respecting the allowlist. Fix PR #4834 was promptly merged, demonstrating responsive maintainer action to regressions.  
   [GitHub: Issue #4823](https://github.com/HKUDS/nanobot/issues/4823)

### Underlying Needs
- **Performance with local models** remains a pain point — users running Ollama with consumer GPUs (32 GB VRAM) experience severe latency.
- **Agent reliability** — the "lazy" agent behavior (#1459) undermines user trust in NanoBot's ability to follow through on stated actions.
- **Channel-specific regression response** — users expect new versions not to break existing group allowlist configurations.

---

## 5. Bugs & Stability

### New Bugs Reported (Closed today)

| Issue | Severity | Description | Fix Status |
|-------|----------|-------------|------------|
| #4991 | High | Local triggers run agent turns after their channel is disabled, wasting model usage | **Fixed** in PR #4990 (merged) |
| #4975 | Medium | CLI Apps lose UTF-8 subprocess output on Windows non-UTF-8 locales (CP936/GBK) | **Reported only** — no fix PR in this digest |
| #4980 | Medium | `GitStore` fails to initialize when workspace differs from process working directory | **Reported only** — no fix PR in this digest |

### Open Bugs in Active PRs

| PR | Issue | Severity | Description |
|----|-------|----------|-------------|
| #4982 | — | Medium | Feishu `_fallback_text_chunks` hangs when `limit <= 0` |
| #4981 | — | Medium | Telegram `_split_telegram_markdown` hangs when `max_len <= 0` |
| #4768 | #4767 | Medium | QQ WebSocket reconnection uses fixed 5-second interval (no backoff) |
| #4995 | — | Medium | Incomplete dependency migration for channels in CI/Docker |
| #4947 | #4884 | Medium | Jina Reader exposes sensitive URLs (credentials, tokens) to third party |

### Severity Assessment
The most critical bug is **#4991** (trigger delivery to disabled channels) because it directly wastes model API usage — a financial cost to users. This was fixed within hours. The Windows UTF-8 bug (#4975) is medium severity because it affects a specific platform and locale combination but can produce silent data corruption in CLI tool output. The GitStore bug (#4980) is also medium — it prevents automatic commits for users who don't run NanoBot from the workspace directory.

---

## 6. Feature Requests & Roadmap Signals

### Completed/In-Progress Features

| Feature | Status | PR | Description |
|---------|--------|----|-------------|
| Nimble search provider | **Open PR** | #4951 | New `web_search` provider |
| Atlas Cloud provider | **Open PR** | #4996 | New OpenAI-compatible gateway provider |
| Telegram custom Bot API base URL | **Open PR** | #4919 | Support for self-hosted Bot API servers |
| Model presets bound to sessions | **Open PR** | #4866 | Persist model preset selection per session |
| Secure browser companion launch | **Open PR** | #4997 | Localhost-only endpoint with HttpOnly session tokens |
| Skill type requirements checking | **Open PR** | #4300 | Allow skills to check if dependencies are available |
| Image generation settings live-apply | **Open PR** | #4964 | Hot-apply image provider/model changes in WebUI |
| Unified agent tool output in WebUI | **Open PR** | #4963 | Replace raw tool logs with one-line activity language |
| Internal turn lifecycle refactor | **Open PR** | #4993 | Unify system message handling into TurnContext state machine |

### Predictions for Next Release
Based on PR priority labels and maintainer activity:
1. **Session-scoped model presets** (#4866, priority p1) is likely to merge soon — it's a significant UX improvement for users who switch models frequently.
2. **Atlas Cloud provider** (#4996) and **Nimble search** (#4951) are clean additions that add provider diversity with low integration risk.
3. **Turn lifecycle refactor** (#4993, priority p1) signals architectural improvement to reduce internal complexity.
4. The **Jina Reader URL sanitization** (#4947) is a security fix that may be fast-tracked.

---

## 7. User Feedback Summary

### Positive Signals
- **Rapid bug fixing:** The WhatsApp group regression (#4823) was reported and fixed within days — PR #4834 was merged promptly.
- **Architectural improvements:** The channels refactor (#4908) completes a major milestone toward channel decoupling, which users had requested for easier custom channel development.

### Pain Points
1. **Ollama performance is unusable** — 60-second delays per turn (#4867) makes local model inference effectively broken, even on 32 GB VRAM hardware. This is the single most impactful negative experience reported.
2. **Agent doesn't follow through** — Issue #1459 describes an agent that verbally acknowledges tasks but never executes them, frustrating users who expect reliable tool execution.
3. **Windows compatibility** — UTF-8 encoding issues (#4975) and package manager shim issues (#4994, now fixed) indicate ongoing Windows quality gaps that affect users on non-English locales.
4. **Channel config regressions** — Users report that new releases break existing configurations (WhatsApp allowlists), suggesting insufficient regression testing for channel integrations.

### Satisfaction Indicators
- **High engagement:** 30 PRs updated in 24 hours indicates an active and responsive community.
- **Multiple contributors:** Contributors with diverse handles (kuchazi-yy, santhreal, Re-bin, gola, chengyongru, etc.) suggest a healthy open-source ecosystem.

---

## 8. Backlog Watch

### Open Issues Needing Attention

1. **#1459** — `nanobot with codex-5.3-codex is lazy and doesn't actually execute`  
   - **Open since:** 2026-03-03 (4.5 months)  
   - **Status:** No triage labels beyond initial report  
   - **Risk:** Core behavior issue that undermines agent reliability. Low upvotes (2) but 6 comments suggest it affects multiple users.  
   [GitHub: Issue #1459](https://github.com/HKUDS/nanobot/issues/1459)

2. **#4867** — `Preserve exact prompt prefix to enable caching in Ollama and others`  
   - **Status:** Closed without visible resolution  
   - **Risk:** This was a major performance blocker for local model users. If closed without a fix, affected users have no path forward. Verify resolution or reopen if necessary.  
   [GitHub: Issue #4867](https://github.com/HKUDS/nanobot/issues/4867)

### Open PRs with Long Review Cycles

| PR | Open Since | Priority | Description |
|----|-----------|----------|-------------|
| #4300 | 2026-06-11 (39 days) | unlabeled | Skill type requirements — may need maintainer review |
| #4223 | 2026-06-06 (44 days) | unlabeled | Weixin session reload fix — stale PR with conflict label |
| #4768 | 2026-07-06 (14 days) | p1+conflict | QQ reconnect backoff — has both p1 and conflict labels |

### Observation
Several PRs carry the `conflict` label (8 of the top 20 shown), suggesting merge conflicts with the `main` branch. This may indicate that these PRs need rebasing before they can be reviewed. The long-open PRs (#4300, #4223) could benefit from automated conflict detection or maintainer guidance to rebase.

---

*This digest was generated from GitHub activity data for the period 2026-07-19 00:00 UTC to 2026-07-20 00:00 UTC.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-07-20

## Today's Overview

The Hermes Agent project shows very high activity today with 50 issues and 50 PRs updated in the last 24 hours, though 44 of those issues remain open. No new releases were published today. The project's pulse is characterized by intense bug-fixing momentum across the agent runtime, gateway, and desktop components, with particular focus on session state integrity, billing accuracy, and cross-platform compatibility (macOS and Windows). The volume of `needs-repro` and `needs-decision` tags indicates maintainer attention is stretched, with several high-severity bugs (P2) remaining unassigned.

## Releases

None published today. The last release remains the most recent tagged version; no migration notes or changelog updates are available in this window.

## Project Progress

Today saw **11 PRs merged or closed**, including several meaningful fixes:

- **[PR #67596](https://github.com/NousResearch/hermes-agent/pull/67596)** — Merged: `feat(memory): add opt-in layered built-in memory retrieval`. Adds `memory.injection_mode: layered` configuration, injecting only `[core]` `MEMORY.md` entries into the system prompt while retrieving contextual entries via `memory(action="...")`. Advances the built-in-memory roadmap from #56762.
- **[PR #67742](https://github.com/NousResearch/hermes-agent/pull/67742)** — Merged: `perf(desktop): stop per-token sidebar + tool-row re-renders during streaming`. Two render-cost wins identified from code inspection, correcting streaming performance without breaking correctness.
- **[PR #64812](https://github.com/NousResearch/hermes-agent/pull/64812)** — Merged: `fix(desktop): handle Windows simple-git binary paths with spaces`. Fixes "No diff to show" on Windows when Git is installed to `C:\Program Files\Git\cmd\git.exe`.
- **[PR #66823](https://github.com/NousResearch/hermes-agent/pull/66823)** — Merged: `feat(mattermost): interactive permission-request buttons`. Adds Approve/Deny, slash-confirm, and clarify buttons to the Mattermost adapter, mirroring the WhatsApp Cloud clickback pattern.
- **[PR #67795](https://github.com/NousResearch/hermes-agent/pull/67795)** — Merged: `feat(desktop): unify custom endpoint card style with provider key rows`. UI consistency improvement for desktop settings.

Also notable: **[PR #67548](https://github.com/NousResearch/hermes-agent/issues/67757)** (referenced in issue #67757) added a credential swap on every `try_activate_fallback` call — this fix is already generating community concern about idempotency (see Bugs & Stability).

## Community Hot Topics

The most active discussions reveal deep concerns about session state, billing accuracy, and credential management:

1. **[Issue #46593](https://github.com/NousResearch/hermes-agent/issues/46593)** (6 comments, open 35 days) — Kanban worker exits with rc=0 without calling `kanban_complete`, leading to unhelpful "protocol violation" errors. The real error (e.g., `boto3 converse_stream` failure) is buried in logs. **User need:** Better error propagation and diagnostic UX in the kanban worker lifecycle. Persistent, unresolved.

2. **[Issue #67187](https://github.com/NousResearch/hermes-agent/issues/67187)** (5 comments, open 2 days) — MCP parked server revival reconnects but does not re-register tools. After a Streamable HTTP MCP server exhausts reconnects, tools remain absent even after successful reconnection. **User need:** MCP tool lifecycle must survive server restarts without manual intervention. High impact for power users running many MCP tools.

3. **[Issue #53771](https://github.com/NousResearch/hermes-agent/issues/53771)** (4 comments, open 23 days) — Large chat-gateway sessions fail with Cloudflare 502 without triggering compression. Provider returns generic 502 instead of context overflow; Hermes retries the oversized request. **User need:** Compression should trigger before the session reaches provider limits, not after error classification.

4. **[Issue #7489](https://github.com/NousResearch/hermes-agent/issues/7489)** (4 comments, 5 👍 votes) — RPM-based pre-emptive throttling using `x-ratelimit` headers. Users want proactive rate-limit avoidance rather than reactive retry/failover loops. **User need:** Intelligent provider rate-limit management. Popular request (5 thumbs-up).

## Bugs & Stability

### High Severity (P1/P2 — active or unaddressed)

| Issue | Severity | Description | Fix PR? |
|-------|----------|-------------|---------|
| [#67762](https://github.com/NousResearch/hermes-agent/issues/67762) | P2 (blocker) | `agent.session_estimated_cost_usd` resets to $0 on gateway restart. Session cost tracking is lost mid-session. | **[PR #67796](https://github.com/NousResearch/hermes-agent/pull/67796)** — open, rehydrates accumulators from SQLite |
| [#67764](https://github.com/NousResearch/hermes-agent/issues/67764) | P2 (should-fix) | `cost_status` and `cost_source` are "most-recent-call-wins" — every API call overwrites accumulated billing state. | No fix PR yet |
| [#67781](https://github.com/NousResearch/hermes-agent/issues/67781) | P2 (needs-repro) | Daily 4AM session_reset resurrected by stale-route recovery. Session ran 23h, ~$2 cost from uncleared context. | No fix PR yet |
| [#53861](https://github.com/NousResearch/hermes-agent/issues/53861) | P2 | macOS gateway stays down after update — launchd defers respawn in on-demand-only mode. Update flow doesn't verify restart. | No fix PR yet |
| [#67756](https://github.com/NousResearch/hermes-agent/issues/67756) | P2 (needs-repro) | PR #67541 hidden semantic change to `_planned_restart_notification_pending` path. Silent behavior change in restart loop logic. | No fix PR yet |
| [#67757](https://github.com/NousResearch/hermes-agent/issues/67757) | P2 (needs-repro) | PR #67548 unguarded `_swap_credential` on every `try_activate_fallback` call — idempotency concern. Credential churn risk. | No fix PR yet |

### Medium Severity (P3 — active)

| Issue | Description |
|-------|-------------|
| [#67732](https://github.com/NousResearch/hermes-agent/issues/67732) | macOS: `sudo hermes gateway install` writes plist to `/var/root`, misreports launchd as unsupported, silently falls back to root-run gateway. |
| [#67783](https://github.com/NousResearch/hermes-agent/issues/67783) | `computer_use` needs alignment with cua-driver 0.9.0 after #67123/#67052. Follow-up for evidence-driven escalation ladder. |
| [#67249](https://github.com/NousResearch/hermes-agent/issues/67249) | `active_pr` respawn guard tripped by non-PR content in comments. No operator override exists. |
| [#67286](https://github.com/NousResearch/hermes-agent/issues/67286) | Desktop files panel auto-opens after first reply in a new session. UX regression. |
| [#66917](https://github.com/NousResearch/hermes-agent/issues/66917) | Desktop file browser sidebar auto-opens on every new session when no project is active. Duplicate of #67286 pattern. |
| [#67722](https://github.com/NousResearch/hermes-agent/issues/67722) | PR #67712 dashboard fail-closed fix does not close the gap filed in #67704 — fix doesn't actually fix the underlying bug. |

**Cross-cutting theme:** Session state integrity and billing accuracy dominate today's bug reports. Three separate issues (#67762, #67764, #67781) all concern cost/session accumulators being lost or overwritten. The cost tracking code path touches `hermes_state.py`, `conversation_loop.py`, `codex_runtime.py`, and `insights.py` — indicating a systemic architecture issue rather than isolated bugs.

## Feature Requests & Roadmap Signals

Three feature requests today show clear user demand and may appear in the next minor release:

1. **[Issue #67765](https://github.com/NousResearch/hermes-agent/issues/67765)** — Show running session cost in the desktop status bar. *Likely next version:* The fix in [#67796](https://github.com/NousResearch/hermes-agent/pull/67796) is already rehydrating cost accumulators, making this feasible. Expect this if #67762 lands.

2. **[Issue #66565](https://github.com/NousResearch/hermes-agent/issues/66565)** — Session colors: inherit from project, manual override, optional auto-classification. *Possible next version:* Low implementation cost, high UX value. iTerm2-tab-color inspiration.

3. **[Issue #65905](https://github.com/NousResearch/hermes-agent/issues/65905)** — Disable persistent context-window caching for volatile provider catalogs. *Needs decision:* The maintainer-needs-decision tag suggests architectural debate about how `context_length_cache.yaml` should handle dynamic providers.

The **[PR #67718](https://github.com/NousResearch/hermes-agent/pull/67718)** (transactional external worker lifecycle) is a significant architectural addition — if merged, it would allow external supervisors to submit, lease, and finalize kanban tasks transactionally. This is a P3 feature but signals growing interest in external integration patterns.

## User Feedback Summary

**Pain points (repeated across issues):**
- **Session state loss on restart/gateway flips** — Users consistently report lost context, lost billing data, and unexpected session behavior after gateway restarts (#67762, #67781, #67764).
- **macOS installation and update fragility** — Multiple issues cite launchd misbehavior, root-vs-user plist placement, and update verification gaps (#53861, #67732).
- **Diagnostic opacity** — Users cannot tell when fallback models activate (#54509), when compression should trigger (#53771), or why kanban workers fail silently (#46593).
- **Desktop UX regression** — The auto-opening file panel on new sessions is a persistent annoyance (#67286, #66917).

**Satisfaction signals:**
- The Mattermost interactive buttons PR (#66823) was merged, indicating chat-platform parity is improving.
- Desktop streaming performance fix (#67742) was merged promptly — good maintainer responsiveness to UX issues.
- The memory layering feature (#67596) was merged, addressing a long-standing request for configurable memory injection.

## Backlog Watch

**Long-unanswered issues needing maintainer attention:**

1. **[Issue #46593](https://github.com/NousResearch/hermes-agent/issues/46593)** (open 35 days, 6 comments) — Kanban worker protocol violation error masking. Despite being a P3, the age and comment count suggest users are frustrated. No fix PR exists.

2. **[Issue #14471](https://github.com/NousResearch/hermes-agent/issues/14471)** (closed, but reopened 88 days ago) — Hermes injects unrelated AGENTS.md/CLAUDE.md/.cursorrules via tool-path discovery. This was closed but the underlying problem (post-tool-call context contamination from neighboring project files) remains unfixed according to the issue body.

3. **[Issue #7489](https://github.com/NousResearch/hermes-agent/issues/7489)** (open 100 days, 5 👍) — RPM-based pre-emptive throttling. Highly-upvoted feature request that has seen no PR activity. The user base clearly wants smarter rate-limit handling.

4. **[Issue #39429 PR](https://github.com/NousResearch/hermes-agent/pull/39429)** (open 46 days) — Fix for preserving custom provider `request_overrides` in gateway and `/model` switches. This is a critical fix for users relying on custom provider features like `extra_body` passthrough. The PR has been open for over a month with no closure.

5. **[Issue #30178](https://github.com/NousResearch/hermes-agent/issues/30178)** (open 59 days) — LM Studio per-model `context_length` regressed to 64K in 0.14.0. Affects all models. No fix PR exists despite being a clear regression with known reproduction steps.

**Maintainer bottleneck indicators:** The high count of `needs-decision` (8+ issues/PRs), `needs-repro` (3 issues), and swept items marked with `sweeper:risk-*` tags suggests the maintainer team is triaging actively but resolution velocity is constrained. The `codex` tag on several items (#53771, #65905, #66744) indicates automated or semi-automated triage is in play, but these items remain unaddressed.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-20

## 1. Today’s Overview
Project activity is moderate with 4 issues and 3 pull requests updated in the last 24 hours. No new releases were published. The community is reporting real-world integration pain points—particularly around WeChat image handling and DeltaChat channel configuration—while also surfacing a long-standing issue with provider model ID parsing that has seen no maintainer intervention for over a week. On the PR side, two fixes for Anthropic token metrics and ID normalization remain stalled, and a fresh bug fix for Antigravity token refresh scoping may unblock one common deployment failure. Overall, developer attention appears divided between critical user-facing bugs and older quality-of-life patches.

## 2. Releases
No new releases were published today. The project remains at its last known stable version.

## 3. Project Progress
No pull requests were merged or closed today. Three PRs remain open:
- **#3251** (stale, 8 days old) – Fix to capture prompt cache token usage in Anthropic providers. Could improve observability for operators monitoring cache hit rates.
- **#3202** (stale, 19 days old) – Fix for ID normalization to strip leading/trailing underscores. Important for name routing correctness but has awaited review for nearly three weeks.
- **#3267** (fresh, 1 day old) – Fix for Antigravity token refresh scope bug that causes `PERMISSION_DENIED` errors during token refresh. Appears small and targeted.

No feature advancements or merged fixes were recorded today.

## 4. Community Hot Topics
- **#3252 (Issue, open, 1 comment)** – `splitKnownProviderPrefix` strips model ID when the ID contains a known provider alias. This is a subtle but potentially high-impact bug for anyone using model IDs like `openai/gpt-4` when a provider named `openai` is present. The issue has been open for 8 days with no comment from maintainers.
  - [sipeed/picoclaw Issue #3252](https://github.com/sipeed/picoclaw/issues/3252)

- **#3268 (Issue, open, 0 comments)** – Requests that the `exec` tool’s `action` parameter default to `"run"` instead of being required. The reporter notes that LLM agents frequently omit this parameter, causing avoidable failures. This reflects a broader user expectation that common operations should have sensible defaults.
  - [sipeed/picoclaw Issue #3268](https://github.com/sipeed/picoclaw/issues/3268)

- **#3251 (PR, open, stale)** – Anthropic cache token capture patch. While not heavily commented, it represents operational interest in monitoring prompt caching effectiveness.
  - [sipeed/picoclaw PR #3251](https://github.com/sipeed/picoclaw/pull/3251)

The underlying need across all three is for **reliability and predictability**—users want their agents to work without requiring knowledge of internal implementation details.

## 5. Bugs & Stability
Three bugs were reported today, ranked by severity:

**High Severity**
- **#3266 (CLOSED)** – WeChat (Weixin) channel passes images to non-vision models before saving/checking them, causing visible errors. A fix PR may exist but is not linked. This is a channel-specific regression that degrades UX for WeChat users.
  - [sipeed/picoclaw Issue #3266](https://github.com/sipeed/picoclaw/issues/3266)

**Medium Severity**
- **#3265** – Gateway fails to start with `unknown type deltachat` error even when DeltaChat is not configured. Appears to be a channel registration bug where default scanning picks up an unsupported driver. Blocks gateway startup entirely.
  - [sipeed/picoclaw Issue #3265](https://github.com/sipeed/picoclaw/issues/3265)

**Low Severity (Usability)**
- **#3268** (described above) – `exec` tool missing default for `action`. Not a crash, but causes error-prone agent behavior.

No fix PRs are directly linked to these issues yet, though PR #3267 addresses a different authentication-scope bug with Antigravity.

## 6. Feature Requests & Roadmap Signals
- **Default action for `exec` tool (#3268)** – Likely to be accepted in the next minor release as it aligns with common “sensible defaults” philosophy.
- **Prompt cache visibility (#3251)** – If merged, this could become a standard metric exposed in monitoring dashboards.
- **Provider prefix handling (#3252)** – A fix would reduce configuration surprises for multi-provider setups; expect it in a future patch.

No major new feature proposals appeared today. The signal is primarily quality-of-life and reliability.

## 7. User Feedback Summary
Pain points center on **configuration and integration friction**:
- WeChat users face image-to-model mismatches that present as visible errors before the file is even saved (#3266).
- Gateway users are blocked by a channel scanning bug that prevents startup even when the offending channel is not configured (#3265).
- Antigravity users experience silent token refresh failures leading to `PERMISSION_DENIED` errors (#3267).
- General sentiment from #3268 suggests users expect LLM-triggered tools to be more lenient with missing parameters.

Satisfaction is likely tempered: while no severe data loss or security vulnerabilities were reported, accumulated integration bugs erode confidence in the reliability of the system.

## 8. Backlog Watch
Two PRs and one issue require maintainer attention:
- **PR #3202** (19 days stale) – ID normalization fix. Unaddressed for nearly three weeks, blocking correct behavior for agent/account names with leading underscores.
  - [sipeed/picoclaw PR #3202](https://github.com/sipeed/picoclaw/pull/3202)
- **PR #3251** (8 days stale) – Anthropic cache token capture. Low risk, moderate reward for observability.
  - [sipeed/picoclaw PR #3251](https://github.com/sipeed/picoclaw/pull/3251)
- **Issue #3252** (8 days stale) – Provider prefix stripping bug. Could affect many users with complex provider configurations; no maintainer response.
  - [sipeed/picoclaw Issue #3252](https://github.com/sipeed/picoclaw/issues/3252)

These items have received zero maintainer comments and are at risk of becoming permanently stale. A review pass is overdue.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-20

## Today's Overview
NanoClaw is experiencing a sustained high-velocity development period, with **40 PRs** updated in the last 24 hours (25 merged/closed, 15 open) and only **2 new issues** opened. The project maintains strong momentum with contributions from multiple core-team members including @amit-shafnir, @moshe-nanoco, and long-standing contributors like @CrAzyScreamx. The substantial PR merge volume (25 closed) indicates active maintenance and feature integration, while the low new-issue count (2) suggests the project is effectively addressing bugs and features through PRs rather than relying heavily on issue tracking. The 25 merged/closed PRs against only 2 new issues reflects a **healthy codebase that is actively reducing its backlog**.

## Releases
**No new releases** today. The last release appears to be prior to the current high-activity period; given the volume of merged PRs, a release announcement is likely overdue.

## Project Progress
25 PRs were merged or closed today, showcasing significant progress across multiple areas:

**Major Features Merged:**
- **[PR #1921]** feat: add `/add-weixin` skill — WeChat channel via iLink bot protocol (by @Clapeysron) — a new channel integration for Tencent's WeChat platform
- **[PR #1648]** feat: add Microsoft Teams channel (`/add-msteams`) (by @Aswinmcw) — workplace messaging integration via Bot Framework webhook
- **[PR #1594]** feat: add WeChat channel skill (by @grzhx) — another WeChat integration via Tencent iLink Bot API with QR-code auth, message chunking, and session management
- **[PR #1517]** feat: add Discord channel with image attachment support (by @misterclarity) — Discord bot with image resizing and multimodal content blocks
- **[PR #2306]** feat(yt-dlp-mcp): in-tree MCP server + `/add-ytdlp` installer (by @CrAzyScreamx) — YouTube download MCP server
- **[PR #2261]** feat(mcp): `/add-ffmpeg` — ffmpeg/ffprobe MCP server for media transformation (by @CrAzyScreamx)
- **[PR #2847]** feat: support URL-based (remote) MCP servers (by @grantland) — enables connecting to remote MCP servers over HTTP/SSE

**Channel Permissions:**
- **[PR #2278]** feat: per-wiring channel permission (read | write | read+write) (by @CrAzyScreamx) — granular channel access control

**Bug Fixes Merged:**
- **[PR #3038]** fix(whatsapp): don't translate group participants to phone JIDs (LID-mode group fix) (by @caburi00)
- **[PR #3008]** fix(whatsapp): remove cachedGroupMetadata that breaks SKDM in LID groups (by @gfnord)
- **[PR #2870]** fix(whatsapp): keep native participant addressing for group encryption (by @elancode)
- **[PR #2688]** fix(whatsapp): stop translating group participants to phone JIDs (fixes ack 421) (by @mcaldas)
- **[PR #2276]** fix(channels): URL fallback in bridge when adapter omits fetchData (by @CrAzyScreamx)
- **[PR #1087]** feat: add Telegram channel, voice transcription, and message deduplication (by @hugwi) — closed after extensive work

## Community Hot Topics
**Most Active Issues (today, by recency):**

- **[#3091] Feature request: standardize composable host extension hooks for skills (hosthooks)** — [Link](https://github.com/nanocoai/nanoclaw/issues/3091)
  - Author: @ZappoMan | Created: 2026-07-19
  - **Analysis:** This issue addresses a critical architectural pain point: community skills that need host- or runner-side behavior currently resort to string-patching NanoClaw source code. This creates conflicts when multiple skills touch the same sites and breaks on upstream refactoring. The request for standardized host extension hooks (hosthooks) reflects a growing need for **plugin infrastructure** as the skill ecosystem expands.

- **[#3089] Feature request: agent-driven skill learning** — [Link](https://github.com/nanocoai/nanoclaw/issues/3089)
  - Author: @cy83rc0llect0r | Created: 2026-07-19
  - **Analysis:** This feature request envisions NanoClaw autonomously generating skill files by recognizing repeated task-solving patterns. This signals community interest in **self-improving agent behavior** — moving beyond static skills toward meta-learning capabilities.

**Most Active PRs (today, open):**
- **[#3094]** fix(telegram): retry transient bot identity lookup — [Link](https://github.com/nanocoai/nanoclaw/pull/3094) — @amit-shafnir
- **[#3093]** fix(chat): keep typing active for processing turns — [Link](https://github.com/nanocoai/nanoclaw/pull/3093) — @amit-shafnir
- **[#3092]** feat: support remote Streamable HTTP MCP servers — [Link](https://github.com/nanocoai/nanoclaw/pull/3092) — @amit-shafnir
- **[#3090]** fix(templates): prepend all top-level context Markdown — [Link](https://github.com/nanocoai/nanoclaw/pull/3090) — @amit-shafnir
- **[#3088]** feat(ncl): surface unknown-sender holds in `ncl approvals list` — [Link](https://github.com/nanocoai/nanoclaw/pull/3088) — @moshe-nanoco

**Underlying Needs:** The concentration of WhatsApp group fixes (PRs #3038, #3008, #2870, #2688) indicates a prolonged struggle with WhatsApp's LID migration, affecting user trust in group messaging. The multiple WeChat/Discord/Teams channel PRs being merged simultaneously shows strong community demand for **multi-platform support** beyond the original WhatsApp focus.

## Bugs & Stability

**Critical (zero-day impact):**
- **WhatsApp LID group messaging** — Multiple fixes merged today (PRs #3038, #3008, #2870, #2688) addressing "waiting for this message" status and ack error 421 in LID-addressed WhatsApp groups. This has been a recurring issue since June 2026 with at least 4 separate fix attempts. **Status: Likely resolved** with the latest merges.

**High (user-facing, no crash):**
- **Telegram bot identity lookup** ([PR #3094]) — Transient failure during bot identity lookup needs retry logic. **Status: Fix open.**

**Medium (usability):**
- **Chat typing indicator** ([PR #3093]) — Typing indicator not staying active during multi-turn processing. **Status: Fix open.**
- **Context template issue** ([PR #3090]) — Top-level context Markdown not being prepended correctly. **Status: Fix open.**

The active bug-fix PRs are from core-team member @amit-shafnir, suggesting rapid internal response to newly identified issues.

## Feature Requests & Roadmap Signals

**High Likelihood (next release):**
1. **Remote MCP server support** ([PR #3092], [PR #2847]) — Connecting to MCP servers over HTTP/SSE is being actively merged, suggesting this will be a marquee feature in the next release.
2. **Multi-channel expansion** — With WeChat ([#1921], [#1594]), Discord ([#1517]), and Microsoft Teams ([#1648]) merged today, the project is clearly moving toward a **multi-platform agent** architecture.
3. **CLI improvements** ([PR #3088]) — `ncl approvals list` for unknown-sender holds indicates ongoing CLI tooling maturation.

**Medium Likelihood:**
4. **Host extension hooks** ([#3091]) — This would address the string-patching problem and enable a proper plugin ecosystem. Likely to be prioritized as skill count grows.
5. **Agent-driven skill learning** ([#3089]) — More speculative, but aligns with the project's autonomous agent philosophy.

**Prediction for Next Version (v?):** A "Channel Expansion Release" featuring stable Discord, Teams, WeChat, and Telegram channels alongside remote MCP server support.

## User Feedback Summary

**Satisfaction Signals:**
- Strong community contribution velocity (40 PRs/day) indicates an engaged developer base
- Successful channel integrations for Discord, Teams, WeChat show responsiveness to platform diversity requests
- WhatsApp fixes being actively iterated despite complexity demonstrates commitment to core channel reliability

**Pain Points:**
- **WhatsApp group reliability** has been a persistent frustration — multiple users (@caburi00, @gfnord, @elancode, @mcaldas) submitted independent fixes for LID group issues, suggesting users were actively debugging production failures
- **Skill development friction** ([#3091]) — Community developers resort to monkey-patching core code, a clear sign of dissatisfaction with the current extension model
- **Manual skill creation** ([#3089]) — The requirement to hand-write skill files is seen as a barrier to agent autonomy

**Use Case Signals:**
- Workplace deployment (Teams, Discord, WeChat)
- Media processing (yt-dlp, ffmpeg MCP servers added)
- Voice transcription (in PR #1087)

## Backlog Watch

**Critical Attention Needed:**
- **PR #1087** — Closed after 126 days (since March 2026), this massive 5-feature PR (Telegram channel, whisper.cpp voice transcription, image sending, deduplication, atomic IPC) was apparently merged after an extremely long review cycle. This suggests the project may have **PR review bottlenecks** despite high merge volume.

**PRs Requiring Maintainer Review:**
- No long-unanswered PRs visible in the top 20; the core team appears to be processing PRs quickly given the 25 merges today. However, the 15 open PRs include several from today alone, so it's too early to flag stagnation.

**Observations:**
- The project shows **healthy maintainer responsiveness** with core-team members (@amit-shafnir) actively opening fixes within 24 hours of issues.
- The clustering of WhatsApp fixes from multiple independent contributors suggests a need for **better integration testing** for WhatsApp protocol changes — the same root issue (LID addressing) was fixed 4 separate times, indicating previous fixes were incomplete or regressed.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-20

## Today's Overview

IronClaw is in an intense architecture refactoring phase ("Reborn"), with core team members driving multiple simultaneous transformation tracks. Today saw exceptional developer activity: 50 PRs updated (32 merged/closed), 5 active issues, and zero new releases. The project is consolidating its capability execution model, simplifying compile-time features, improving crash recovery, and enhancing local developer onboarding. The high PR volume and rapid closures indicate a disciplined merge cadence and focused execution toward the Reborn milestone.

## Releases

No new releases published today.

## Project Progress

**32 PRs were merged or closed** in the last 24 hours, reflecting significant architectural advancement:

**Architecture Simplification (Reborn — §5.3 Capability-Outcome Collapse):**
- [#6287 (closed)](https://github.com/nearai/ironclaw/pull/6287) — Core API flip: loop-facing results now use `host_api::Resolution` directly, collapsing the 10-variant `CapabilityOutcome` into a 5-channel model
- [#6293 (closed)](https://github.com/nearai/ironclaw/pull/6293) — Complete collapse: all capability producers emit `Resolution` directly; `CapabilityOutcome` deleted entirely
- [#6275 (closed)](https://github.com/nearai/ironclaw/pull/6275) — Added `ResolutionBatch` and loop-suspension predicate infrastructure
- [#6273 (closed)](https://github.com/nearai/ironclaw/pull/6273) — `Resolution` now carries model-visible failure diagnostics and denial content
- [#6271 (open)](https://github.com/nearai/ironclaw/pull/6271) — Resume replay payloads moved host-side via `ReplayPayloadStore` with real durable stores wired in production

**Composition & Deployment Configuration (§4.4/§5.6/§5.11):**
- [#6279 (closed)](https://github.com/nearai/ironclaw/pull/6279) — `DeploymentConfig` now covers all seven composition profiles, owning every deployment axis
- [#6280 (closed)](https://github.com/nearai/ironclaw/pull/6280) — De-prefixed local-dev builder names to reflect shared substrate

**Compile-Time & Code Cleanup:**
- [#6296 (open)](https://github.com/nearai/ironclaw/pull/6296) — Major cleanup: 14 features deleted, ~1,100 `#[cfg]` sites removed (184 files, +767 / −2,424 lines)
- [#6292 (closed)](https://github.com/nearai/ironclaw/pull/6292) — Frozen `RebornServicesApi` facade method set with regression test

**Developer Experience & Onboarding:**
- [#6285 (closed)](https://github.com/nearai/ironclaw/pull/6285) — Frictionless local-dev onboarding: auto-provision serve, REPL model wizard, `onboard` launcher
- [#6297 (open)](https://github.com/nearai/ironclaw/pull/6297) — Onboard launcher with browser auto-open and Corepack error fix
- [#6289 (open)](https://github.com/nearai/ironclaw/pull/6289) — REPL UX: thinking spinner and markdown rendering
- [#6294 (closed)](https://github.com/nearai/ironclaw/pull/6294) — Shortened onboarding quick-start documentation

**Documentation:**
- [#6291 (open)](https://github.com/nearai/ironclaw/pull/6291) — Architecture doc revision folding error-recoverability contract

**Testing Infrastructure:**
- [#6295 (closed)](https://github.com/nearai/ironclaw/pull/6295) — Crash-consistency chaos suite for turn-state; found and fixed two real crash-recovery defects

## Community Hot Topics

The most active discussions centered on the Reborn architecture consolidation:

**[Issue #6263 — InMemoryTurnStateStore retirement](https://github.com/nearai/ironclaw/issues/6263)** (8 comments)
The final store consolidation item: retiring the in-memory turn state store. Requires "Slice 0" oracle and no-livelock evidence before closure. This is the culmination of an A1–A8 slice sequence spanning checkpoint clusters, test doubles, and secrets consolidation. The underlying need is eliminating the last architectural debt item in the storage layer.

**[Issue #6274 — DeploymentConfig completion](https://github.com/nearai/ironclaw/issues/6274)** (2 comments)
Tracks finishing `DeploymentConfig` as the single composition configuration source. Phase 2 and Phase 3 landed today via PRs #6279 and #6280, with Phase 4 still pending. The conversation signals a need for unified deployment configuration across all environments.

**[Issue #6284 — Error-recoverability endgame](https://github.com/nearai/ironclaw/issues/6284)** (0 comments but strategically significant)
Defines the contract that every mid-run error must satisfy four conditions: run survives, model sees it, cause is communicated, model gets a turn to respond. This is a design philosophy anchor for the Reborn architecture.

## Bugs & Stability

**High Severity — Duplicate PDF MIME Type Bug:**
- [#6257](https://github.com/nearai/ironclaw/issues/6257) and [#6290](https://github.com/nearai/ironclaw/issues/6290) (duplicate) — `"Invalid value (attachments.mime_type)"` when sending or generating PDF files. Reported by two users (Michael Kelly via Slack and michael.kelly via Slack, possibly the same person). Suspected root cause is a file path reading issue or missing/setup-dependent tool. No fix PR has been opened yet. This is likely a regression or config issue affecting PDF file handling in attachments.

**Medium Severity — Two Crash-Recovery Defects (Now Fixed):**
PR [#6295 (closed)](https://github.com/nearai/ironclaw/pull/6295) introduced a crash-consistency chaos suite and fixed two defects it surfaced, directly supporting Issue #6263 and #6284. The suite serves as the acceptance oracle for async-write-behind changes in turn-state consolidation.

## Feature Requests & Roadmap Signals

**Reborn Architecture Completion (Imminent):**
The §5.3 capability-result collapse is nearly complete (Stage 2b merged today). Remaining work includes Stage 2a-i (PR #6271 open), Slice 0 oracle requirements, and the `InMemoryTurnStateStore` retirement. Expect the full Reborn architecture to stabilize within the next 1–2 weeks.

**Local Development Experience (Shipped Today):**
The end-to-end frictionless onboarding (PR #6285) with auto-provisioning, model wizard, and onboard launcher (PR #6297) addresses a clear user pain point. Combined with REPL UX improvements (spinner + markdown rendering in PR #6289), this suggests the project is preparing for broader developer adoption.

**Compile-Time Feature Simplification (In Progress):**
PR #6296's reduction from 38 to 24 features with ~1,100 cfg sites removed signals a drive toward simpler builds and clearer feature gates. Storage backends (libsql/postgres) are deliberately deferred as a product decision.

## User Feedback Summary

**Pain Points:**
- PDF MIME type error when generating/attaching PDF files (Issues #6257, #6290) — directly impacts file-sharing workflows
- Initial onboarding chain of dead ends (lack of WebUI token, missing user ID setup) — cited as motivation for PR #6285
- Silent CLI blocking during turns and raw markdown output — addressed by PR #6289's spinner and rendering improvements

**Satisfaction Signals:**
- The documentation shortening (PR #6294) aligns with user need for simpler setup
- The onboard launcher with automatic browser opening (PR #6297) directly addresses setup friction
- No negative feedback on the architectural changes suggests the Reborn refactoring is invisible to end users

## Backlog Watch

**[Release PR #5598](https://github.com/nearai/ironclaw/pull/5598)** (open since July 3, 2026) — This release PR has been open for 17 days with breaking changes in `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0). It is likely blocked by the in-flight Reborn architecture changes. Users depending on stable releases may be waiting; once the Reborn tracks converge, expect a major version release bundling all breaking changes.

**[Wasm dependency PR #4032](https://github.com/nearai/ironclaw/pull/4032)** (open since May 25, 2026) — This 56-day-old dependency bump for the wasm toolchain (`wit-component` 0.245.1 → 0.253.0, `wit-parser` 0.245.1 → 0.253.0) suggests the wasm-related pipeline may not be under active development during the Reborn push. May need maintainer triage to assess if still relevant.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is your project digest for **LobsterAI** covering activity on and around **2026-07-20**.

---

## LobsterAI Project Digest – 2026-07-20

### 1. Today's Overview
The project is currently in a **low-activity maintenance phase**. Over the last 24 hours, three issues and three pull requests were updated, but **zero new releases** were published, and **no fresh work (new issues/PRs) was created today**. All recent activity consists of **stale items** (last updated April 2nd) that were bumped or closed by automation. The open/closed ratio (2 open, 1 closed issues) suggests minor cleanup is occurring, but no active feature development or critical bugfixing is visible on the surface.

### 2. Releases
**No new releases** were published during this period. The latest release remains unchanged.

### 3. Project Progress
Only **one PR was closed/merged** today:

- **#1350 – [CLOSED] skills文件长时间生成阻塞无法感知**  
  *Author: jimmy-xz*  
  A PR that addressed a severe user experience gap where skill-file generation could hang without any progress indication. It was closed today (likely merged or manually closed as stale). This suggests the team has acknowledged the need for real-time generation feedback.

*Note: The two other open PRs (#1285, #1286) are dependency bump PRs by Dependabot that remain unmerged.*

### 4. Community Hot Topics
All discussions remain relatively quiet, with only 1–2 comments per item. No single topic dominates.

- **#1289 – [OPEN] feat: 为长代码块添加折叠/展开功能**  
  *Comments: 1 | 👍: 0*  
  *Link: [Issue #1289](https://github.com/netease-youdao/LobsterAI/issues/1289)*  
  **Analysis:** This feature request for code block folding remains the only substantive feature-level discussion. Users are frustrated by long AI-generated code chunks that break scroll flow. The proposal is well-defined (auto-fold after 15+ lines) and aligns with common UX patterns.

- **#1352 – [CLOSED] 任务对话框，附件上传无反应**  
  *Comments: 2 | 👍: 0*  
  *Link: [Issue #1352](https://github.com/netease-youdao/LobsterAI/issues/1352)*  
  **Analysis:** This was the only issue closed today. It reported a UI regression where attachments could not be uploaded while a task was running. The 2 comments likely include a maintainer interaction before closure.

### 5. Bugs & Stability
**No new bugs were filed today.** However, two stale bugs remain open, ranked by severity:

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **Medium** | [#1287](https://github.com/netease-youdao/LobsterAI/issues/1287) | IM robot connectivity test falsely passes with dummy credentials (appkey=1, etc.) | No fix PR identified |
| **Low-Medium** | [#1352](https://github.com/netease-youdao/LobsterAI/issues/1352) *(closed)* | Attachment upload disabled during task execution (regression) | Resolved (closed) |

**Notable:** Issue #1287 is a **validation/security gap** – the test should reject obviously invalid credentials. It has been open for over 3 months with no resolution, indicating a potential blind spot in quality checks for IM integrations.

### 6. Feature Requests & Roadmap Signals
One pending feature request stands out:

- **#1289 – Code block folding**  
  *Link: [Issue #1289](https://github.com/netease-youdao/LobsterAI/issues/1289)*  
  Likelihood for next version: **Medium**.  
  The implementation is straightforward (frontend only, already has a `CodeBlock` component with line limits). The main barrier is that the project has not released a new version in some time. This is a strong candidate for a future v2.x patch.

**No roadmap signals** (e.g., labels like `next-version` or associated milestones) were visible in current data.

### 7. User Feedback Summary
Real user pain points captured from today’s activity:

- **Pain point – No progress feedback during long generation:**  
  In PR #1350, the user explicitly described frustration with “阻塞在文件生成过程中，且并未看到任何报错和提示” (blocked during generation with no error or prompt). The same user also noted that “同模型不同龙虾需求理解有问题” – the same prompt yields inconsistent behavior between LobsterAI and Openclaw.

- **Pain point – Long code blocks hurt readability:**  
  Issue #1289 highlights that AI-generated code blocks of 15–200 lines are shown in full, forcing excessive scrolling. Users want auto-collapse behavior.

- **Satisfaction signal:** The closure of #1352 (attachment upload bug) shows the team is responsive to UI regressions, even if slowly.

### 8. Backlog Watch
These items have been **unanswered or untouched by maintainers for months** and deserve flagging:

- **#1287 – [bug] IM robot false test pass**  
  *Created: 2026-04-02 | Last activity: 2026-07-19 (stale)*  
  *Link: [Issue #1287](https://github.com/netease-youdao/LobsterAI/issues/1287)*  
  **Risk:** Credential validation gap. Any dummy credentials pass connectivity tests, which could erode trust in the setup process. **No maintainer reply.**

- **#1285 & #1286 – Dependabot PRs**  
  *Created: 2026-04-02 | Last activity: 2026-07-19 (stale)*  
  *Links: [PR #1285](https://github.com/netease-youdao/LobsterAI/pull/1285) | [PR #1286](https://github.com/netease-youdao/LobsterAI/pull/1286)*  
  **Risk:** Two dependency updates (concurrently 8 → 9, tailwindcss 3 → 4) have been open for 3+ months. These are major version bumps that include breaking changes, making them high-risk to merge without testing. Their continued staleness may indicate the maintainer is postponing a larger upgrade effort.

---

*Data sourced from the LobsterAI GitHub repository (netease-youdao/LobsterAI) as of 2026-07-20.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-20

## Today's Overview
Activity is in a low but steady state, with one new release (20260719.01) and one open PR moving memory infrastructure forward. The single issue updated in the past 24 hours remains open with ongoing community discussion, indicating sustained interest in feature work. No bugs, crashes, or regressions were reported today, suggesting current stability. Overall, the project is maintaining momentum through incremental infrastructure improvements and thoughtful feature conversations.

## Releases
**20260719.01**
- No changelog or release notes provided; likely a patch or build-related release.
- No breaking changes or migration notes documented.

## Project Progress
No PRs were merged or closed in the last 24 hours.

## Community Hot Topics
- **#574 – [Feature]: Model Routing Per Topic** ([Issue](moltis-org/moltis Issue #574))  
  *Author: azharkov78 | Updated: 2026-07-19 | Comments: 4 | 👍: 1*  
  This open enhancement request proposes topic-based routing to different underlying models. The feature would allow users to define which model handles specific subject areas (e.g., coding vs. casual chat). The issue has not received maintainer response, and with only one upvote, interest is still nascent. However, the concept aligns with emerging patterns in multi-model AI agent orchestration. Underlying need: users want more granular control over model selection to optimize cost, latency, and quality per domain.

## Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. No stability-related issues are currently open.

## Feature Requests & Roadmap Signals
- **#574 – Model Routing Per Topic** remains the sole active feature request. While early-stage, the idea of topic-based routing could complement the new `zvec` vector database backend (PR #1158) by enabling memory- or embedding-based routing decisions. Likelihood for next release: low, unless maintainers see strong community demand.

## User Feedback Summary
No new user pain points or satisfaction reports emerged in the past 24 hours. The only community interaction is a feature request with minimal support, signaling that users are either generally satisfied or not actively vocal on GitHub.

## Backlog Watch
- **#574 – Model Routing Per Topic** (open since 2026-04-06, 105 days)  
  No maintainer response or labeling exists on this issue. Given its age and the absence of moderator input, it may warrant a courtesy reply or a "needs more detail" label to guide the requester. Prolonged silence risks discouraging community contributors.
  
- **#1158 – feat(memory): add zvec vector database memory backend** (open since 2026-07-17)  
  This PR has not yet received maintainer review comments. As an experimental addition, it would benefit from technical feedback or a decision on inclusion path to avoid stagnation.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-07-20

## 1. Today's Overview

CoPaw is showing **elevated community activity** with 12 issues and 6 PRs updated in the last 24 hours, though **no new releases** were published. The project maintains a healthy pulse with 5 open PRs awaiting review (including 2 first-time-contributor submissions) and a **1-to-11 open-to-closed issue ratio** for the day, indicating active triage. The community is predominantly focused on **bug reporting and UX refinement**, with several issues surfacing regressions in the recent v2.0.0.post3 release. Notably, the "search" feature request for system tray minimization and the CIDR security PR suggest **growing enterprise/desktop adoption** of the platform.

## 2. Releases

**No new releases** were published in the last 24 hours. The latest stable version remains **v2.0.0.post3** (reflected in multiple bug reports referencing this version).

## 3. Project Progress

**Merged/Closed PRs today:** 0 (all 6 PRs remain open)

**Notable open PRs advancing key features:**

- **#6262** — `feat(agents): add one-click copy of agent configuration` (yuanxs21) — Adds `POST /api/agents/{agent_id}/copy-config` endpoint with a modal UI for selective config copying, **excluding runtime assets**. This addresses a common workflow pain point where users wanted to reuse agent configurations without duplicating sessions and media.

- **#6259** — `feat(security): support CIDR in no-auth host allowlist` (dztyykxx, first-time contributor) — Extends `security.allow_no_auth_hosts` to accept IPv4/IPv6 CIDR notation (e.g., `10.0.0.0/8`), making enterprise deployments more practical without listing individual IPs.

- **#6251** — `feat(cli): add scriptable environment reads` (wananing) — Adds `qwenpaw env get KEY` and `qwenpaw env list --json` for programmatic access to the encrypted environment store, supporting automation/CI workflows.

- **#6256** — `feat(governance): make sandbox-unavailable fallback action configurable` (JOJOCrazy123, first-time contributor) — Fixes #6250 by allowing operators to define behavior when sandbox is unavailable (approve/reject/admin-approve), improving governance for locked-down environments.

- **#6247** — `fix(memoryspace): catch OSError in _saved_tool_refs is_file() check` (zealonexp) — Direct fix for bug #6246 (see Bugs section).

## 4. Community Hot Topics

The **most commented-on issues and PRs** reveal distinct community focuses:

| Item | Type | Comments | Topic |
|------|------|----------|-------|
| [#6193](https://github.com/agentscope-ai/QwenPaw/issue/6193) | Issue | 4 comments | MCP serial startup 8x slower than parallel |
| [#6163](https://github.com/agentscope-ai/QwenPaw/issue/6163) | Issue | 3 comments | Reusable multi-step workflow orchestration |
| [#6240](https://github.com/agentscope-ai/QwenPaw/issue/6240) | Issue | 3 comments | Memory annotation leak in UI after long chats |
| [#6257](https://github.com/agentscope-ai/QwenPaw/issue/6257) | Issue | 2 comments | Duplicate thinking content across tool calls |

**Underlying needs analysis:** The #6193 MCP parallelism issue reveals a **scaling pain point** — users deploying multiple MCP clients (8+) are experiencing startup delays of 40+ seconds, which undermines the "instant-on" expectation of personal AI assistants. The passionate community engagement on #6240 (memory annotation leaking into visible chat) signals that **perceived data security and UI cleanliness** are core user concerns. The workflow orchestration request (#6163) is the strongest roadmap signal this week, echoing earlier requests for structured agent pipelines.

## 5. Bugs & Stability

**Severity ranking** (high to low):

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| 🔴 Critical | [#6246](https://github.com/agentscope-ai/QwenPaw/issue/6246) | `recall_history` crashes with `OSError: [Errno 36] File name too long` when tool results contain long paths (e.g., git diffs). Complete search/recall functionality broken. | Yes — PR #6247 |
| 🔴 Critical | [#6261](https://github.com/agentscope-ai/QwenPaw/issue/6261) | Offline code mode cannot preview files (requires online resources). Both TUI and web affected. Previously "fixed" in #5781, now regressed. | No |
| 🟡 High | [#6257](https://github.com/agentscope-ai/QwenPaw/issue/6257) | Identical thinking output across multiple tool calls in a single turn — reasoning repetition wastes tokens and confuses users. | No |
| 🟡 High | [#6255](https://github.com/agentscope-ai/QwenPaw/issue/6255) | `BadRequestError: 400` during chat sessions (v2.0.0.post3). Interrupts ongoing conversations with no recovery. Stack trace points to task_tracker.py. | No |
| 🟡 High | [#6258](https://github.com/agentscope-ai/QwenPaw/issue/6258) | OpenAI model `max_tokens` setting not honored — model ignores configured output token limits. | No |
| 🟢 Low | [#6252](https://github.com/agentscope-ai/QwenPaw/issue/6252) | Tauri desktop mode on Linux: Ctrl+wheel zoom not working. UI scaling locked. | No |

**Notable:** The #6246 fix (PR #6247) is already available, wrapping the `is_file()` call in a try/except. The #6261 offline regression suggests a **prior fix was incomplete or reverted**, requiring maintainer attention.

## 6. Feature Requests & Roadmap Signals

**Most-requested features this week:**

1. **Reusable Workflow Orchestration with Audit Trail** ([#6163](https://github.com/agentscope-ai/QwenPaw/issue/6163)) — Users want to define multi-step, reusable workflows combining `chat_with_agent`, sub-agents, and cron scheduling. **Likelihood for next minor release: Medium** – This is a significant architecture change but aligns with the existing multi-agent capabilities.

2. **Per-agent auto-memory profiles** ([#6263](https://github.com/agentscope-ai/QwenPaw/issue/6263)) — Currently all agents share `auto_memory.yaml`. Request: separate profiles so companion agents use chronological diaries while technical agents use topic-oriented memory. **Likelihood for next release: Medium** – Low implementation complexity, high user value.

3. **System tray minimization** ([#6264](https://github.com/agentscope-ai/QwenPaw/issue/6264)) — Desktop users want minimize-to-tray behavior. **Likelihood: Low-Medium** – Platform-dependent, but aligns with desktop mode growth.

4. **Collapsible thinking/tool-call blocks in UI** ([#6260](https://github.com/agentscope-ai/QwenPaw/issue/6260)) — Users want agent reasoning and tool outputs collapsed by default, showing only final results. **Likelihood: High** – UX improvement already referenced in competitor comparisons, minimal backend changes.

**Roadmap signal:** The CIDR allowlist PR (#6259) and sandbox fallback configurability (PR #6256) suggest **enterprise security is a growing focus area** for the project.

## 7. User Feedback Summary

**Pain points:** Dominant theme is **v2.0.0.post3 regression fatigue** — multiple reports (chat errors #6255, max tokens #6258, offline preview #6261) indicate the current release has quality issues. The memory annotation leak (#6240) is particularly frustrating for privacy-conscious users, as tool call internals leak into visible chat.

**Use case insights:** The MCP parallel startup request (#6193) reveals a **power-user deployment pattern**: 8+ MCP clients for complex task automation, not just simple chat. The workflow orchestration request (#6163) confirms users are outgrowing single-turn interactions and need structured, auditable pipelines.

**Satisfaction signals:** Two first-time contributors submitted PRs (#6259, #6256), indicating **good onboarding** and project documentation quality. The agent config copy feature (#6262) was clearly motivated by positive user experiences wanting to scale their setups.

**Dissatisfaction indicators:** No explicit "uninstalling" or "switching" language, but the collapsible blocks request (#6260) includes a screenshot comparison with a competitor product, suggesting users are evaluating alternatives when UX falls short.

## 8. Backlog Watch

**Issues needing maintainer attention:**

- [#6193](https://github.com/agentscope-ai/QwenPaw/issue/6193) (MCP parallel startup) — **Open since July 16**, 4 comments, 0 maintainer response. High-value performance fix already scoped to `manager.py`; could be resolved with an `asyncio.gather` refactor.

- [#6163](https://github.com/agentscope-ai/QwenPaw/issue/6163) (Workflow orchestration) — **Open since July 16**, 3 comments, no maintainer triage label. This is the most architecturally significant feature request this week; a "roadmap" or "discussion" label would set expectations.

**PRs awaiting review:**

- [#6247](https://github.com/agentscope-ai/QwenPaw/pull/6247) (fix OSError in `_saved_tool_refs`) — **Ready for review since July 18.** Direct fix for critical bug #6246; merging this would resolve one of the week's highest-severity issues.
- [#6259](https://github.com/agentscope-ai/QwenPaw/pull/6259) (CIDR support) — **First-time contributor**, open since July 19. Low-risk security enhancement; prompt review would encourage continued contribution.
- [#6262](https://github.com/agentscope-ai/QwenPaw/pull/6262) (Agent config copy) — **Open since July 19**, significant UX improvement. Requires UI/backend maintainer coordination.

**No items in backlog have remained completely unanswered for more than 48 hours**, indicating healthy triage response times.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for **2026-07-20**.

---

# ZeroClaw Project Digest: 2026-07-20

## 1. Today's Overview
ZeroClaw continues to operate at a high velocity, with **33 active issues** and **48 open pull requests** updated in the last 24 hours. The project is deep in a feature-frozen maintenance period for v0.8.4, while simultaneously pushing forward major architectural changes for v0.9.0, specifically around memory decoupling, security hardening, and runtime plugin systems. Activity is driven by 2 merged/closed PRs and 3 resolved issues, though the overwhelming volume of work-in-progress items suggests a significant bottleneck in code review and maintainer bandwidth. The ecosystem shows strong third-party contributions (e.g., Windows fixes, OpenRouter sanitization, Nextcloud Talk improvements) alongside lead maintainers (Audacity88, metalmon, JordanTheJet) driving RFC implementation.

## 2. Releases
**No new releases** were published in the last 24 hours. The latest stable release remains v0.8.3, with the maintenance track v0.8.4 targeting a July 31, 2026 ship date ([#8357](https://github.com/zeroclaw-labs/zeroclaw/issues/8357)).

## 3. Project Progress
**Closed/Merged PRs Today:** 2
- **The v0.8.3 config-driven runtime tracker closed** ([#8363](https://github.com/zeroclaw-labs/zeroclaw/issues/8363)). This milestone delivered config resolution, runtime routing, model switching, and MCP/tool-policy enforcement.
- **ACP agent selection via `?agent=` query param merged** ([#8958](https://github.com/zeroclaw-labs/zeroclaw/issues/8958)). This enables multi-agent endpoints for external ACP clients like Thunderbolt.

**Key feature advances in open PRs:**
- **SOP/HITL slot release** ([#8848](https://github.com/zeroclaw-labs/zeroclaw/pull/8848)) adds per-SOP admission policies (Parallel/Hold/Coalesce/Drop), allowing concurrent SOP execution without deadlock.
- **OpenAI Chat Completions endpoint** ([#8486](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)) nears completion, enabling gateway compatibility with LangChain, Continue.dev, and Aider.
- **Telegram multi-message streaming** ([#8561](https://github.com/zeroclaw-labs/zeroclaw/pull/8561)) adds paced multi-message delivery (configurable 800ms default) matching Discord/Matrix behavior.
- **Live config architecture docs** ([#9168](https://github.com/zeroclaw-labs/zeroclaw/pull/9168), ADR-012) codifies zero-downtime reload paths for security and channel config.

## 4. Community Hot Topics
- **RFC: Work Lanes and Board Automation** ([#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)) — 14 comments. This governance RFC remains the most discussed item, proposing label cleanup and automation to reduce maintainer overhead. The 60-day lifespan suggests it may be close to finalization.
- **Turn-level OTel trace correlation** ([#6641](https://github.com/zeroclaw-labs/zeroclaw/issues/6641)) — 8 comments. A natural follow-up to #6009 and #6190, this feature would nest LLM/tool/memory spans under a single turn trace, critical for production observability.
- **Persistent memory tracker** ([#8891](https://github.com/zeroclaw-labs/zeroclaw/issues/8891)) — 7 comments. This epic tracker (21 open items) coordinates the multi-PR rollout to bring cross-session memory to parity with mature runtimes.
- **KeySource trait RFC** ([#9127](https://github.com/zeroclaw-labs/zeroclaw/issues/9127)) — 7 comments. Proposed classification of master-key material by source/deployment form, addressing a high-risk security concern for 93 encrypted fields.

**Underlying need:** The volume of RFCs (6 active) reveals a project struggling with architectural debt. The community is pushing for formal, governance-driven decisions on memory, security, and plugin architecture rather than ad-hoc implementation.

## 5. Bugs & Stability
**High-Severity Bugs (S0/S1):**
- **[S1] Telegram channel not configurable** ([#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505)) — Users report `channels doctor` claims channels are unset even after Quickstart setup; bot unresponsive on Telegram but works in CLI.
- **[S0] Confused deputy in execute_pipeline** ([#7947](https://github.com/zeroclaw-labs/zeroclaw/issues/7947)) — `execute_pipeline` ignores per-agent `ToolAccessPolicy`, authorizing steps solely from global `[pipeline].allowed_tools`. A fix PR is needed; tracked in v0.9.0 security tracker.
- **[S1] Windows ZeroCode startup failure** ([#9117](https://github.com/zeroclaw-labs/zeroclaw/issues/9117)) — `zerocode` requires manual `ZEROCLAW_SOCKET` env var on Windows; fails with 10-second timeout on named pipe.

**Medium Severity:**
- **[S2] JIT loading fails for Qwen3.6-35B-A3B** ([#9177](https://github.com/zeroclaw-labs/zeroclaw/issues/9177)) — Manual load works, but JIT triggers "Engine protocol startup was aborted." Likely a race condition in engine lifecycle.
- **[S2] CLI secret prompts give no feedback after paste** ([#7808](https://github.com/zeroclaw-labs/zeroclaw/issues/7808)) — Hidden password input shows nothing after paste; users cannot confirm entry is accepted.

**Fix PRs in flight:**
- `fix(memory): cold start timeouts` ([#9105](https://github.com/zeroclaw-labs/zeroclaw/pull/9105)) — Raises Lucid recall timeout from 500ms to 3s for ARM cold starts.
- `fix(providers): sanitize tool-call arguments` ([#8931](https://github.com/zeroclaw-labs/zeroclaw/pull/8931)) — Prevents HTTP 400 on OpenRouter when models emit malformed JSON in `tool_calls[].function.arguments`.

## 6. Feature Requests & Roadmap Signals
**Likely for v0.8.4 (July 31 target):**
- **Memory lifecycle decoupling** ([#6850](https://github.com/zeroclaw-labs/zeroclaw/issues/6850)) — `MemoryStrategy` trait to decouple lifecycle policy from storage backends. PR activity high.
- **Conversation vs. long-term memory separation** ([#9048](https://github.com/zeroclaw-labs/zeroclaw/issues/9048)) — RFC accepted; will prevent session history from polluting curated long-term memory.

**Likely for v0.9.0:**
- **WASM-based runtime plugins** ([#8850](https://github.com/zeroclaw-labs/zeroclaw/issues/8850)) — Moving channels/tools from compile-time features to runtime-installable WASM plugins. This shrinks the binary and enables community extensions.
- **Realtime voice-host channel** ([#7943](https://github.com/zeroclaw-labs/zeroclaw/issues/7943)) — Backend-agnostic WebSocket client for voice (CrispASR, sherpa-onnx reference).
- **llama.cpp model router** ([#7539](https://github.com/zeroclaw-labs/zeroclaw/issues/7539)) — Allows quick switching between local models without config reloads.

**New today:**
- MCP embedded resource blob intake ([#9179](https://github.com/zeroclaw-labs/zeroclaw/issues/9179)) — Materializes binary MCP tool results into agent workspace.
- ACP `deliver_file` for citations ([#9178](https://github.com/zeroclaw-labs/zeroclaw/issues/9178)) — Supports `resource.blob` in ACP prompts.

## 7. User Feedback Summary
**Demand for Windows parity:** Multiple Windows-specific issues (#9117, #7461) reflect growing user adoption on non-Linux platforms. The Windows CI test suite remains a blocker (#7461).

**Pain with self-hosted deployments:**
- Provider fallback circuit breakers requested ([#7881](https://github.com/zeroclaw-labs/zeroclaw/issues/7881)) — Users want failing providers quarantined rather than endlessly retried.
- Intra-family fallback notices ([#7883](https://github.com/zeroclaw-labs/zeroclaw/issues/7883)) — Users want to know when a different model serves their request, even within the same provider.

**Quickstart friction:**
- Telegram setup broken (#8505) is blocking one of the most popular channel options.
- `--config-dir` ignored during locale detection (#9017) frustrates users with non-standard config paths.

**Third-party integration signals:**
- Thunderbolt (Mozilla Thunderbird) ACP client connected successfully (#8958) — validates ACP as a viable multi-agent protocol.
- Nextcloud Talk channel fix (#9181) shows enterprise collaboration demand.

## 8. Backlog Watch
| Item | Status | Risk | Last Update | Concern |
|---|---|---|---|---|
| **#[7947] execute_pipeline bypasses per-agent tool gating** | OPEN, in-progress | S0 (Security) | 2026-07-19 | Fix is deferred to v0.9.0; no PR assigned. This is a confirmed confused-deputy vulnerability. |
| **#[8505] Telegram channel cannot be configured** | OPEN, accepted | S1 (Blocked workflow) | 2026-07-19 | No fix PR yet. Affects a core channel; users cannot use Telegram at all. |
| **#[7897] Zero-downtime config reload** | OPEN, RFC accepted | High | 2026-07-19 | No implementation PR despite accepted RFC. Blocked by v0.9.0 timeline. | 
| **#[7461] Windows/macOS CI test suite** | OPEN, accepted | High | 2026-07-19 | Only 2 comments; no PR. Non-Linux users risk regression on every release. |
| **PR #[8486] OpenAI Chat Completions endpoint** | OPEN, needs-author-action | High | 2026-07-20 | Stalled since 2026-06-29. Author has not responded to maintainer review. Blocking LangChain/Continue.dev integration. |
| **PR #[8848] SOP HITL slot release** | OPEN, needs-author-action | High | 2026-07-20 | Large PR (XL size); author unresponsive since 2026-07-08. Critical for multi-agent governance. |

**Maintainer attention needed:** The `needs-author-action` label on 6 high-risk PRs (#8486, #8848, #8966, #8561, #8438, #9055) indicates a pattern of contributors submitting large, complex changes and then going silent. These PRs represent significant architectural work (OpenAI endpoint, SOP governance, Telegram streaming) and risk stalling if not driven to merge.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*