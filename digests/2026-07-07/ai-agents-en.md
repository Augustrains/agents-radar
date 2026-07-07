# OpenClaw Ecosystem Digest 2026-07-07

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-07 01:50 UTC

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

# OpenClaw Project Digest — 2026-07-07

## Today's Overview

Project activity remains **extremely high**, with 500 Issues and 500 PRs updated in the last 24 hours, indicating a healthy and fast-moving open-source ecosystem. However, the ratio of open/active issues (403) to closed (97) suggests a growing backlog requiring maintainer attention. The release pipeline is quiet today (no new releases). Notably, the community is heavily focused on **multi-agent orchestration stability**, **security hardening** (especially around sandboxing and private network access), and **UX improvements** across chat channels (Telegram, Slack, Feishu). Several critical P0 bugs remain open, including a session hang/duplicate-message issue that is flagged as a release blocker.

---

## Releases

**No new releases today.** The latest release is `v2026.6.11` (referenced in bug #98416), which had a known reentrancy guard issue in its published dist.

---

## Project Progress

No PRs were merged or closed today that are detailed in the top-30 list. The following **open PRs** represent active work advancing the project:

### Notable Fixes in Review
- **PR #101256** — Fixes model provider auth refresh after CLI login (ready for maintainer)
- **PR #94341** — Fixes bootstrap files being silently ignored when placed in `agentDir` (fixes #29387)
- **PR #101031** — Handles SSH sandbox stream errors to prevent unhandled exceptions
- **PR #101022** — Handles stderr stream errors in `tool_search_code` child process
- **PR #85238** — Includes pnpm 11 bins in gateway PATH (ready for maintainer)
- **PR #89744** — Fixes Discord default account startup priority (ready for maintainer)

### Notable Features in Review
- **PR #94322** — Exposes resolved agentId on plugin command context (ready for maintainer)
- **PR #94308** — Shows session costs in `openclaw status` command
- **PR #94517** — Adds `openclaw devices rename` CLI command for human-friendly device names
- **PR #94310** — Detects containerized environments to disable update suggestions

---

## Community Hot Topics

### Most Active Discussions

1. **[#75 — Linux/Windows Clawdbot Apps](https://openclaw/openclaw Issue #75)** 🔥
   - 110 comments, 81 👍 — by far the most engaged issue
   - **Need:** Cross-platform parity for desktop apps (only macOS, iOS, Android exist)
   - **Analysis:** This has been open since January and is the #1 community request. The high reaction count signals strong demand for Linux/Windows native companions.

2. **[#25592 — Text between tool calls leaks to messaging channels](https://openclaw/openclaw Issue #25592)** 
   - 33 comments, P1, Diamond Lobster rating
   - **Need:** Internal processing output must not be routed to user-visible channels
   - **Analysis:** A critical UX/security issue — agents' internal narration showing up as visible messages is unacceptable for production deployment. Maintainer review + product decision are pending.

3. **[#39604 — Add `tools.web.fetch.allowPrivateNetwork`](https://openclaw/openclaw Issue #39604)** 
   - 13 comments, 11 👍 — strong community support
   - **Need:** Opt-in private network access for `web_fetch` tool
   - **Analysis:** Security-conscious users want the ability to reach internal services when explicitly configured. A reasonable compromise between security and utility.

4. **[#43367 — Multi-agent orchestration is unstable](https://openclaw/openclaw Issue #43367)** 
   - 13 comments, P1
   - **Need:** Concurrent `agents add` overwrites config, session-lock failures, detached child work
   - **Analysis:** This is a **critical reliability gap** for users running multi-agent setups. The concurrent config overwrite alone is a data-loss risk.

5. **[#63829 — Per-agent memory-wiki vault configuration](https://openclaw/openclaw Issue #63829)** 
   - 12 comments, 9 👍
   - **Need:** Isolated knowledge wikis per agent in multi-agent setups
   - **Analysis:** Currently all agents share a global vault, which creates cross-agent contamination. High demand for this feature.

---

## Bugs & Stability

### Critical (P0 — Release Blockers)

1. **[#43661 — Session hangs indefinitely when compaction times out](https://openclaw/openclaw Issue #43661)** 
   - **Impact:** Repeated duplicate message sends, no recovery, no user-facing error
   - **Status:** Needs maintainer review, live repro needed. This is tagged `impact:ux-release-blocker`.

### High Severity (P1 — Diamond Lobster)

2. **[#25592 — Text between tool calls leaks to messaging channels](https://openclaw/openclaw Issue #25592)** 
   - Security + message loss impact. No fix PR yet.

3. **[#22676 — Signal daemon stop() race condition on SIGUSR1 restart](https://openclaw/openclaw Issue #22676)** 
   - Orphaned processes and send failures. Open since February. Has a linked PR.

4. **[#98416 — v2026.6.11 published dist missing reentrancy guard](https://openclaw/openclaw Issue #98416)** 
   - **CLOSED** — fix was identified. Commit `d2da8c79d9` adds the needed guard.

5. **[#38327 — "Cannot convert undefined or null to object" with google-vertex/gemini-3.1-pro-preview](https://openclaw/openclaw Issue #38327)** 
   - Regression in v2026.3.2. Needs live repro.

6. **[#31583 — `exec` tool does not inherit `skills.entries.*.env` environment variables](https://openclaw/openclaw Issue #31583)** 
   - Regression. Security impact (secrets not passed). Fix PR status unknown.

### Notable Regressions

- **#38439** — Webchat avatar endpoint returns 404 (regression in avatar display)
- **#41201** — Control UI Avatar not displaying (broken image, regression)
- **#43747** — Memory management is **chaotic** across users — one user gets chunking/embeddings, another gets plain file storage. No consistent behavior.

### Fix PRs Available for Review

| Issue | Fix PR | Status |
|-------|--------|--------|
| #29387 (bootstrap files ignored in agentDir) | #94341 | Needs proof |
| #94279 (containerized env update suggestions) | #94310 | Needs proof |
| #82442 (proxy upstream stream errors) | #88052 | Ready for maintainer |

---

## Feature Requests & Roadmap Signals

### Likely for Next Release (High Community Demand + Existing PRs)

1. **Linux/Windows Desktop Apps** — Issue #75, 110 comments, 81 👍. This is the #1 community request. A PR implementing these would generate massive community goodwill.

2. **Per-Agent Memory Wiki Vaults** — Issue #63829. High 👍 count, clear use case for multi-agent deployments.

3. **Private Network Access for web_fetch** — Issue #39604. 11 👍, straightforward config toggle.

4. **Session Cost Display in Status** — PR #94308 already exists and is ready for maintainer look.

5. **Agent Device Rename** — PR #94517 already exists.

### Medium-Term Roadmap Signals

- **Distributed Agent Runtime** (Issue #42026) — Splitting monolithic gateway into control plane + agent runtime. This would enable horizontal scaling.
- **Multi-Agent Collaboration Enhancement** (Issue #35203) — Capability profiling, shared blackboard, layered memory, token cost governance. An RFC with 10 comments.
- **Post-Subagent Completion Extension Hook** (Issue #22358) — Would enable structured trajectory logging.
- **Pre-Response Enforcement Hooks** (Issue #13583) — Hard gates for mandatory tool calls. Important for regulated industries.
- **Durable Natural-Language Rule Learning** (Issue #41366) — For consistent agent behavior across sessions.
- **Gateway Lifecycle Hooks** (Issue #43454) — Event-driven triggers for workspace hooks.

---

## User Feedback Summary

### Pain Points (High Dissatisfaction)

1. **Memory Management Inconsistency (Issue #43747)** — Users report wildly different memory behavior across the same version. One user gets proper chunking/embedding; another gets flat file storage. This is creating trust issues.

2. **Multi-Agent Instability (Issue #43367)** — Concurrent operations cause config corruption. Users trying to run parallel coding batches hit reliability walls.

3. **Session Compaction Timeouts (Issue #43661)** — Large sessions hang with no recovery, causing duplicate message sends. This is a **release blocker** that undermines production readiness.

4. **Tool Error Leakage to User Channels (Issue #39406)** — Transient tool failures (even when retried successfully) show visible warnings to users. Confusing UX.

5. **Cross-Platform App Gap (Issue #75)** — Linux and Windows users are second-class citizens. This limits the user base significantly.

### Satisfaction Signals

- High engagement on feature requests shows **active and invested user base** — 500+ issues and PRs updated daily.
- Multiple PRs from diverse contributors (mazhuima, cxbAsDev, steipete, fuller-stack-dev) indicate a **healthy contributor ecosystem**.
- The "Clawsweeper" automated labeling system shows sophisticated project management tooling.

### Use Cases Emerging

- **Multi-agent orchestration** for parallel coding tasks (Issue #43367)
- **Business communication** via Telegram Business Bot support (Issue #20786)
- **Quantitative/finance workflows** requiring hard enforcement gates (Issue #13583)
- **Enterprise deployment** with per-agent cost budgets (Issue #42475)

---

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Priority | Why Urgent |
|-------|-----|----------|------------|
| [#75 — Linux/Windows Apps](https://openclaw/openclaw Issue #75) | 6+ months | P2 | 81 👍, 110 comments — top community request |
| [#22676 — Signal daemon race condition](https://openclaw/openclaw Issue #22676) | 4+ months | P1 | Orphaned processes, send failures. Linked PR exists. |
| [#25592 — Text leaks between tool calls](https://openclaw/openclaw Issue #25592) | 4+ months | P1 | Security + message loss. Needs product decision. |
| [#43661 — Session compaction timeout hang](https://openclaw/openclaw Issue #43661) | 3+ months | **P0** | Release blocker. Needs live repro. |
| [#38327 — Google Vertex "null to object" error](https://openclaw/openclaw Issue #38327) | 4+ months | P1 | Regression, 10 comments, 3 👍. Needs live repro. |

### PRs Stuck in Review

| PR | Status | Days Open | Blockers |
|----|--------|-----------|----------|
| [#85238 — pnpm 11 PATH](https://openclaw/openclaw PR #85238) | Ready for maintainer | 46 | None stated |
| [#89744 — Discord startup priority](https://openclaw/openclaw PR #89744) | Ready for maintainer | 34 | None stated |
| [#88052 — Proxy error handler](https://openclaw/openclaw PR #88052) | Ready for maintainer | 38 | None stated |
| [#94344 — Memory SSRF settings](https://openclaw/openclaw PR #94344) | Ready for maintainer | 19 | None stated |

### Recommendations

1. **Triage the P0/P1 backlog** — 3+ month old critical bugs undermine user confidence. The compaction timeout (#43661) should be prioritized as a release blocker.
2. **Process "Ready for Maintainer" PRs** — 6 PRs are marked ready but unmerged. These are low-hanging fruit for improving stability and UX.
3. **Address the cross-platform app gap (#75)** — The community signal is overwhelming. Even a beta release would generate significant goodwill.
4. **Improve memory consistency (#43747)** — Divergent behavior across users suggests a configuration or timing bug that needs root-cause analysis before it erodes trust further.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report for the personal AI assistant and agent open-source ecosystem as of **2026-07-07**.

---

## 1. Ecosystem Overview

The open-source AI agent ecosystem is experiencing a **divergence in maturity and focus**. While flagship projects like **OpenClaw** and **ZeroClaw** sustain high-velocity development with hundreds of daily contributions, the landscape is increasingly shaped by two forces: a relentless push toward production-grade stability (security audits, concurrency fixes, and test infrastructure), and a surge in demand for **multi-agent orchestration, cross-platform chat parity (Telegram, Slack, Feishu, WhatsApp, Mattermost), and enterprise features** (RBAC, audit logging, compliance-ready memory). Security is a universal concern, with multiple projects simultaneously addressing sandbox escapes, SSRF vulnerabilities, and secret management gaps. A secondary tier of projects (e.g., **Hermes Agent**, **Moltis**, **LobsterAI**) are executing targeted feature pushes—such as new provider integrations and channel support—while a lower-velocity group (**NullClaw**, **ZeptoClaw**) shows signs of stagnation. The ecosystem is rapidly professionalizing, but the gap between high- and low-activity projects is widening.

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score |
|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | No release; latest v2026.6.11 | High (extreme volume, but backlog grows) |
| **NanoBot** | 47 | 500 | No release | Medium (high PR churn, but massive open PR backlog) |
| **Hermes Agent** | 50 | 50 | No release | Medium-High (focused maintenance, good fix cadence) |
| **ZeroClaw** | 50 | 50 | No release; targeting v0.8.3/v0.9.0 | High (heavy implementation, multiple tracks) |
| **PicoClaw** | 4 | 5 | No release; latest 0.3.1 | Medium-High (high quality, small scale) |
| **CoPaw** | 34 | 50 | **v1.1.12.post3** (hotfix today) | High (mature, rapid hotfix) |
| **LobsterAI** | 0 | 13 | No release | High (coordinated feature push, 12/13 PRs merged) |
| **NanoClaw** | 3 | 10 | No release; base v2.1.38 | Medium-High (documentation overhaul + bug fixes) |
| **Moltis** | 0 | 5 | No release | Medium (targeted fixes, stable) |
| **NullClaw** | 0 | 1 | No release | Low (single stale Dependabot PR) |
| **ZeptoClaw** | 0 | 0 | No release | Inactive |
| **TinyClaw** | 0 | 0 | No release | Inactive |

*Note: Health Score reflects development velocity, issue responsiveness, and release maturity relative to the ecosystem.*

## 3. OpenClaw’s Position

**Advantages vs. Peers:**
- **Unmatched community scale**: 500+ issues and PRs updated daily dwarfs every other project. No peer approaches this level of engagement.
- **Richest feature pipeline**: Topics like distributed agent runtime (RFC #42026), per-agent memory wikis (#63829), and private network access (#39604) show OpenClaw is pushing architectural boundaries far ahead of the pack.
- **Cross-platform desktop demand**: Issue #75 (Linux/Windows apps) with 81 👍 and 110 comments is the single loudest feature request in the entire ecosystem. No other project matches this user demand signal.

**Technical Approach Differences:**
- OpenClaw is the only project with a **dedicated "Clawsweeper" automated labeling system** and a formalized P0/P1 release-blocker process, indicating mature project management.
- It is the most focused on **multi-agent orchestration stability** as a core reliability requirement—a theme only beginning to emerge in other projects like ZeroClaw and NanoBot.

**Community Size Comparison:**
- OpenClaw’s community is roughly **10x larger** than the next tier (ZeroClaw, CoPaw) by raw update volume. However, its open-to-closed issue ratio (403/97) suggests a backlog risk that more efficient projects like CoPaw (25/34 merged) avoid.

## 4. Shared Technical Focus Areas

The following requirements are emerging consistently across multiple projects:

| Requirement | Projects Affected | Specific Needs |
|---|---|---|
| **Multi-agent orchestration stability** | OpenClaw, NanoBot, ZeroClaw | Session-lock failures, config corruption, detached subagents |
| **Cross-platform chat channel parity** | OpenClaw (Telegram, Slack, Feishu), NanoBot (Mattermost, Telegram), Hermes Agent (WhatsApp, QQ), ZeroClaw (Telegram, QQ, Discord), Moltis (WhatsApp), LobsterAI (Email) | Long-message splitting, streaming consistency, reconnection reliability |
| **Security hardening** | OpenClaw (private network access), NanoBot (P0 shell resource limits, SSRF pinning, audit #4815), ZeroClaw (sandbox policy, SOP auth bypass, browser path validation) | Sandboxing, secret storage, DNS rebinding, path traversal, rate limiting |
| **Memory/context management** | OpenClaw (per-agent wikis, compaction timeouts), CoPaw (auto-memory broken, compression cuts anchors), PicoClaw (cache breakpoints), Hermes Agent (cross-session data leaks) | Isolation, caching, compression, user-facing debugging |
| **Provider/model switching flexibility** | OpenClaw (auth refresh), NanoBot (OAuth warnings), ZeroClaw (per-chat model switch), PicoClaw (Gemini interop via OpenAI-compat) | Provider-agnostic tool calls, credential management |
| **Enterprise/compliance features** | OpenClaw (cost budgets, pre-response hooks), NanoClaw (local audit log), ZeroClaw (SOP engine, approval gates) | Audit trails, RBAC, compliance-ready storage |

## 5. Differentiation Analysis

| Axis | Project Cluster | Key Difference |
|---|---|---|
| **Architectural ambition** | OpenClaw (distributed runtime, multi-agent collaboration), ZeroClaw (goal-mode, SOP engine, plugin permission model) | These projects are building for horizontal scaling and regulated enterprise workflows. |
| **Stability and maintenance** | CoPaw (rapid hotfix, extensive regression testing), Moltis (targeted bug fixes, dependency upgrades) | Focus on keeping existing features reliable vs. adding new ones. |
| **Platform adoption & parity** | LobsterAI (multi-account email, xAI/Grok provider), Hermes Agent (Codex GPT-5.5, Telegram/QQ parity) | Adding specific platform integrations to win mindshare in particular regions or verticals. |
| **Security-first** | NanoBot (35-finding audit, P0 subprocess limits) | Rigorous proactive security posture, likely driven by growing enterprise scrutiny. |
| **Documentation & onboarding** | NanoClaw (4-PR documentation sweep), CoPaw (user-complexity driven) | Addressing the "learning cliff" that limits adoption in less technical user bases. |
| **Inactive / plateauing** | NullClaw, ZeptoClaw, TinyClaw | No meaningful development velocity; may be abandoned or stable but unmaintained. |

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating & High Community Engagement:**
- **OpenClaw**: Dominant in scale and vision. Risk: backlog growth (403 open issues) could overwhelm maintainers.
- **ZeroClaw**: Close second in ambition. Heavy implementation across security, channels, and goal-mode. Risk: quality gate gaps (#8753) could allow regressions.
- **CoPaw**: Most mature release cadence (hotfix shipped today). Excellent test coverage expansion. Risk: context management bugs are persistent.
- **NanoBot**: Extreme PR volume (500) but 492 open—transparency into churn is low. The security audit (#4815) signals a maturing team.

**Tier 2 — Stabilizing & Feature-Driven:**
- **Hermes Agent**: Strong fix cadence for P1 bugs. Community is vocal about gateway UX (Codex notices, cross-profile leaks).
- **LobsterAI**: Highest PR merge rate today (12/13). Moving fast on new integrations (xAI, email, Cowork UI).
- **NanoClaw**: Productive but small scale. Documentation modernization is a smart investment.
- **Moltis**: Stable, low-activity, but high-quality targeted fixes.

**Tier 3 — Maintained but Low Activity:**
- **NullClaw**: Single Dependabot PR open 22 days. No bug reports—could indicate stability or neglect.
- **ZeptoClaw / TinyClaw**: Inactive. Possibly abandoned.

## 7. Trend Signals

1. **From "Will it work?" to "Will it stay secure?"**: The ecosystem is shifting from proving agent functionality to hardening production deployments. Multiple projects (NanoBot, OpenClaw, ZeroClaw) are simultaneously addressing sandbox escapes, SSRF vulnerabilities, and secret leaks. This reflects real-world production exposure and user demand for enterprise-grade security.

2. **The Enterprise Integration Race**: Features like RBAC (Hermes Agent #527), audit logging (NanoClaw #2967), SOP engines (ZeroClaw), and gateway lifecycle hooks (OpenClaw) signal that projects are preparing for **deployment in regulated environments**. This is a direct response to enterprise customers evaluating these tools for internal use.

3. **Context is the New Bottleneck**: The most painful user-facing bugs are no longer about "agent not running" but about **context corruption**—memory leaks across sessions (Hermes Agent), compression cutting critical anchors (CoPaw), and silent memory inconsistencies (OpenClaw). As agents handle longer, multi-step tasks, the ability to maintain coherent, isolated, and debuggable context is becoming the defining quality metric.

4. **Voice and Real-Time Channels are Emerging**: ZeroClaw (Gemini Live proposal, voice satellite) and NanoClaw (Zoom voice agent) are pushing into real-time voice and meeting scenarios. This is a nascent but high-potential trend likely to accelerate as multimodal model capabilities mature.

5. **Windows and Container Parity Gaps**: Windows deployment is a consistent pain point across NanoBot (shell inconsistency), OpenClaw (desktop apps), and ZeroClaw. Docker and containerized environments also cause friction (Moltis volume mounts, OpenClaw update detection). The ecosystem remains Linux-first, and cross-platform support is a clear competitive advantage for any project that invests heavily in it.

6. **Health Warning: PR/Issue Backlog Inflation**: OpenClaw (403 open issues) and NanoBot (492 open PRs) show that high volume without proportional review capacity creates a significant **risk of contributor churn and unfixed regressions**. Projects that manage this balance, like CoPaw and LobsterAI, demonstrate better sustainability.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-07-07

## Today's Overview

NanoBot is experiencing **intense development activity** with 500 PRs updated in the last 24 hours, though 492 remain open — suggesting a large backlog of unmerged contributions. The project has 47 open issues with 39 still active, and a **major security and code quality audit** (Issue #4815) landed today with 35 findings spanning command injection, path escape, and resource exhaustion vulnerabilities. A wave of targeted fix PRs from contributors like `axelray-dev` and `hamb1y` indicates the community is actively addressing identified bugs. No new releases are published, meaning the project may be stabilizing before its next version cut.

## Releases

No new releases were published in the past 24 hours.

## Project Progress

**Merged/Closed PRs (8 total):**
- **#4654** (`goodtiding5`) — **Priority P1**: Fixed CLI interactive mode where streaming failures silently dropped final response text, ensuring users see complete answers
- **#4673** (`goodtiding5`) — **Priority P1**: Fixed Dream consolidation audit records to match real git diffs, improving `/dream-log` accuracy
- **#4459** (`goodtiding5`) — **Enhancement**: Added Mattermost channel integration (WebSocket + REST API) with streaming responses and auto-reconnect
- **#2060** (`MrKich`) — **Feature**: Shell tool now allows configurable specific paths when `restrict_to_workspace=True` (e.g., `/dev/null`)
- **#4818** (`axelray-dev`) — **Priority P2**: Fixed `web_fetch` signature handling of `None` URLs to prevent false cache entries
- **#4819** (`axelray-dev`) — **Priority P2**: Fixed consolidation lock race condition by replacing `WeakValueDictionary` with `plain dict`

**Notable Merged Fixes:**
- **#4819**: Consolidator locks can now be garbage-collected mid-operation, preventing double consolidation — a subtle concurrency bug fix

## Community Hot Topics

### Most Active Issues

1. **[#4061] OpenAI-compatible text-format tool calls not parsed** (6 comments)  
   *Closed* — Root cause identified: providers emitting plain text markup instead of structured `tool_calls`. A structural fix is needed for providers that don't conform to OpenAI's tool call format.

2. **[#4511] Windows gateway `--background` restart inconsistency** (4 comments)  
   *Closed* — PID files and logs become stale after `/restart` command on Windows. Indicates Windows-specific process management gaps.

3. **[#4544] Windows exec shell inconsistency** (3 comments)  
   *Closed* — `exec` routes single-line to `cmd.exe`, multi-line to PowerShell, causing cross-platform scripting pain for agents. A significant usability issue for Windows users.

4. **[#3436] Call external agent** (3 comments)  
   *Open* — User requests ability to delegate work to OpenCode/Codex agents. Signals demand for nano agent orchestration beyond MCP.

5. **[#4637] Telegram long message split rendering** (2 comments)  
   *Open, stale* — Long markdown messages split into trunks where only the last trunk renders correctly. A channel-specific UX regression.

### Most Active Pull Requests

1. **#4771** — WebUI document attachments support (`chengyongru`): Enables PDF/doc file uploads in the WebUI channel, with MIME validation and tests. A major UX improvement for file-heavy workflows.

2. **#1290** — Heartbeat token/callback restoration (`fengxiaohu`): Long-pending PR dating back to Feb 2026 — signals stagnation on a critical infrastructure component.

3. **#4671** — SSRF DNS pinning fix (`hamb1y`, Priority P0): Return validated resolved IPs from SSRF URL validation, pinning DNS lookups to those IPs. Directly addresses security concern about DNS rebinding attacks.

4. **#4689** — OAuth status/expiry warnings (`bingqilinweimaotai`): Adds OAuth provider visibility and token expiry warnings across CLI, WebUI, and runtime — addressing provider reliability UX.

### Underlying Needs Analysis
- **Windows parity**: Multiple Windows bugs (#4511, #4544) show the project's Linux-first design causes real pain for Windows users
- **Security hardening**: The 35-finding audit (#4815) and P0 SSRF fix (#4671) indicate growing security maturity but also exposure
- **Channel diversity**: Mattermost support (#4459) and Telegram rendering fixes (#4637) show demand for multi-platform parity

## Bugs & Stability

### High Severity (P0-P1)

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| **#4797** — No resource limits on shell subprocesses | **P0** | No ulimit/cgroups/CPU/memory caps — LLM can issue fork bombs or resource exhaustion attacks | ❌ No |
| **#4796** — `restrict_to_workspace` defaults to False | **P0** | Full filesystem exposed to LLM by default — all tools can escape workspace | ❌ No |
| **#4803** — API keys stored as plaintext in config.json | **P0-P1** | `model_dump()` includes secrets despite `repr=False` — channel tokens also plaintext | ❌ No |
| **#4795** — Streaming calls bypass wall-clock timeout | **P1** | `outer_timeout_s = None` for streaming — infinitely slow streams consume resources | ❌ No |
| **#4804** — Leaked `CancelledError` silently swallowed | **P1** | MCP AnyIO interaction can drop iterations without notification | ✅ #4814 |
| **#4805** — `suppress(Exception)` swallows tool validation errors | **P1** | Critical tool preparation errors silently fall back to raw args | ✅ #4811 |
| **#4800** — `.strip()` on list-form `msg.content` crashes | **P1** | Multimodal messages raise `AttributeError` | ✅ #4813 |
| **#4793** — Global ExecSessionManager singleton cross-session visibility | **P1** | Two concurrent sessions can see/interact with each other's exec sessions | ❌ No |
| **#4794** — Exec sessions no shutdown cleanup — orphan processes | **P1** | Child processes become orphans on gateway exit | ❌ No |

### Medium Severity (P2)

| Issue | Description |
|-------|-------------|
| **#4792** — `/stop` discards pending queue messages permanently | ❌ No fix |
| **#4791** — No channel-level rate limiting — flood risk | ❌ No fix |
| **#4798** — Concurrent file writes from different sessions not serialized | ❌ No fix |
| **#4801** — Unprotected `message['role']` dict access → KeyError | ✅ #4812 |
| **#4802** — Token budget returns spurious 128 when context window disabled | ✅ #4817 |
| **#4799** — External lookup signature creates false entry for None URLs | ✅ #4820 |

### Recently Fixed
- **#4654** — CLI streaming failure silent drop (P1, merged)
- **#4818** — Web fetch None URL cache signature (P2, merged)
- **#4819** — Consolidation lock race condition (P2, merged)

## Feature Requests & Roadmap Signals

### Most Likely for Next Release (v0.3.0)
1. **Mattermost channel support** (#4459, merged) — New complete channel integration
2. **WebUI document attachments** (#4771, open) — File uploads beyond images
3. **OAuth status/expiry warnings** (#4689, open) — Provider reliability UX
4. **SSRF DNS pinning** (#4671, open) — Security hardening likely to merge soon

### Predictive Signal
- **Security hardening wave**: The 35-finding audit (#4815) will likely trigger a batch of security fix PRs in the next 7-14 days
- **Windows parity fixes**: Multiple Windows-specific bugs suggest maintainers may need a Windows compatibility sprint
- **Channel abstraction**: Issue #4807 identifies 16 files with identical `__init__` patterns — a channel base class refactor is overdue

## User Feedback Summary

### Positive Signals
- **WebUI working well** per #4765: "the web UI is up and running already and works well" even when Python SDK fails
- **Mattermost integration welcomed**: PR #4459 adds another major enterprise channel (Slack-alternative)
- **Dream consolidation improvements**: PR #4673 fixes `/dream-log` audit accuracy, addressing a user-visible reliability issue

### Pain Points
- **Python SDK broken**: Issue #4765 reports the Python API example from docs throws immediately — a documentation vs. implementation gap
- **Windows shell inconsistency**: Issue #4544 highlights that agents writing cross-platform scripts face `cmd.exe` vs. PowerShell semantic differences, making Windows a second-class citizen
- **Telegram message rendering**: Issue #4637 shows long markdown messages visually broken — a critical UX problem for chat users
- **Long-goal skill fails**: Issue #4655 — `read_file: Error: File not found: skills/long-goal/SKILL.md` — a built-in skill path inconsistency that breaks multi-step goals
- **Silent failures**: Issue #4805 reveals tool validation errors are silently swallowed — users may never know why tools behave unexpectedly

### Satisfaction Indicators
- High contributor velocity (500 PRs updated in 24h) suggests an engaged developer community
- Multiple contributors from diverse backgrounds (China, US, international) indicate global adoption
- The detailed 35-finding audit (#4815) shows deep investment in code quality

## Backlog Watch

### Critical Long-Unanswered Items

| Item | Type | Age | Reason for Concern |
|------|------|-----|--------------------|
| **#1290** — Heartbeat token/callback restoration | PR | 131 days (Feb 2026) | Core infrastructure — conflicting/dormant; maintainer attention needed to close or merge |
| **#2060** — Shell tool configurable paths | PR | 114 days (Mar 2026) | Conflicts with workspace restriction — merged today after long stagnation |
| **#4145** — Weather Skill | PR | 36 days (Jun 2026) | Combined multi-file contribution — still open with no recent activity |
| **#3436** — Call external agent | Issue | 73 days (Apr 2026) | User request for agent orchestration — no maintainer response signals feature scoping challenges |

### Stale Issues Needing Triage
- **#4637** — Telegram long message split (5 days stale, 2 comments) — No maintainer acknowledgment despite being a visible UX bug
- **#4511** — Windows gateway restart (closed but symptoms may reoccur) — The underlying Windows process management gap is unaddressed

### Recommendations for Maintainers
1. **Triage #1290** — Heartbeat restoration has been open since February; decide to merge, close, or reassign
2. **Respond to #3436** — The external agent orchestration request has potential but needs architectural guidance
3. **Prioritize Windows parity** — Multiple bugs suggest systematic gaps; consider a `platform/windows` label and sprint
4. **Audit follow-through**: Create tracking issues for the 35 findings in #4815 to prevent them from being forgotten

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the project digest for **Hermes Agent** on **2026-07-07**.

---

## Hermes Agent Project Digest: 2026-07-07

### 1. Today's Overview

The project is experiencing a **high-volume maintenance phase**, with 50 issues and 50 pull requests updated in the last 24 hours. While there are no new releases, the development velocity is intense, showing a strong push to resolve high-severity bugs affecting platform integration, session state, and authentication. Activity is heavily concentrated on the **Codex GPT-5.5 provider** and core gateway reliability, with several critical bugs recently closed via merged PRs. However, the volume of open items (36 of each) suggests the backlog remains large, and the maintainer team is focused on targeted stabilization rather than feature-driven releases.

### 2. Releases

**None.** No new versions of Hermes Agent were released today.

### 3. Project Progress

Several significant pull requests were merged or closed today, indicating progress on critical system flaws:

- **Gateway & Session Stability:**
    - **[PR #59202 (Closed)]**: The Telegram gateway `connect()` hang on container boot was fixed, addressing a serious P1 bug where the connection could hang indefinitely.
    - **[PR #59693 (Open)]**: A fix for the QQbot gateway adapter was prepared, ensuring it accepts the new `is_reconnect` parameter to prevent startup failures.
- **Authentication & Credential Recovery (Key Theme):**
    - **[PR #59837 (Closed)]**: A major fix to the auxiliary system now allows it to recover from expired OAuth credentials for "auto" routes and stale fallback candidates, preventing infinite 401 error loops during compression and vision tasks.
    - **[PR #20837/20978 (Closed)]**: A fix was deployed to ensure that Copilot credentials are properly refreshed when using auto-routing for auxiliary tasks.
- **Desktop & UI:**
    - **[PR #40069 (Closed)]**: Fixed a desktop bug where saving settings on a remote OAuth gateway failed with `net::ERR_INVALID_ARGUMENT`.
- **Cron & Automation:**
    - **[PR #58818 (Closed)]**: Addressed a P1 bug where planned gateway restarts were silently dropping cron job output deliveries mid-flight.
    - **[PR #59910/59916 (Open)]**: Fixes for the contributor-attribution workflow were submitted to handle commits from automated fix bots.

### 4. Community Hot Topics

The most active discussions revolve around **UX friction with the Codex GPT-5.5 provider** and **architectural issues with gateway permissions**.

- **Codex Autoraise Notice Fatigue (Multiple Issues):**
    - **Issues:** [#42187](https://github.com/NousResearch/hermes-agent/issues/42187), [#47241](https://github.com/NousResearch/hermes-agent/issues/47241), [#46786](https://github.com/NousResearch/hermes-agent/issues/46786), [#54432](https://github.com/NousResearch/hermes-agent/issues/54432)
    - **Analysis:** Users are frustrated by the repetition of the "Codex gpt-5.5 autoraise" informational notice on every message in gateway sessions. While these are closed as duplicates or fixed, the high reaction count (👍10 on #42187, 👍7 on #47241) signals that this UX "noise" is a high-priority pain point for the heavy gateway user community. The underlying need is for **session-level rather than agent-instance-level "show once" guarantees**.
- **Gateway Permission Tiers:**
    - **Issue:** [#527](https://github.com/NousResearch/hermes-agent/issues/527) (11 comments, 6 👍)
    - **Analysis:** A long-standing feature request (created March) for Role-Based Access Control (RBAC) on messenger platforms. The binary "authorized/blocked" model is insufficient for family or team deployments. This is a clear signal the community wants Hermes to evolve from a single-user tool into a multi-user platform with granular control.
- **Cross-Profile Data Leak in Desktop:**
    - **Issue:** [#52401](https://github.com/NousResearch/hermes-agent/issues/52401) (2 comments, 1 👍)
    - **Analysis:** A specific and concerning bug where the Desktop app displays data (sessions, cron jobs) from the default profile when viewing a non-default profile. This is a major privacy/configuration issue for users managing multiple identities.

### 5. Bugs & Stability

The project is addressing a cluster of high-severity bugs, though no new single critical regression broke the build today.

| Severity | Issue | Title | Status | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **P1** | [#58818](https://github.com/NousResearch/hermes-agent/issues/58818) | Planned-restart fires while cron delivery is in-flight | **CLOSED** | Silent message drop. Fix merged. |
| **P1** | [#59202](https://github.com/NousResearch/hermes-agent/issues/59202) | Telegram gateway connect() hangs indefinitely | **CLOSED** | Container startup hang. Fix merged. |
| **P2** | [#59224](https://github.com/NousResearch/hermes-agent/issues/59224) | CLI `/resume` hides Desktop/WebUI sessions | **OPEN** | Feature parity gap. No fix PR yet. |
| **P2** | [#58498](https://github.com/NousResearch/hermes-agent/issues/58498) | Desktop ignores OpenAI Codex provider; routes through Nous Portal | **OPEN** | Config routing inconsistency between Desktop & CLI. |
| **P2** | [#50530](https://github.com/NousResearch/hermes-agent/issues/50530) | `google-antigravity` legacy integration issues (sub-agent crash) | **OPEN** | Persistent problems with a third-party provider. |
| **P3** | [#59896](https://github.com/NousResearch/hermes-agent/issues/59896) | `DaemonThreadPoolExecutor` breaks on Python 3.14 | **OPEN** | Future compatibility issue; fix PR [#59913](https://github.com/NousResearch/hermes-agent/pull/59913) raises Python ceiling to <3.15. |
| **P3** | [#59305](https://github.com/NousResearch/hermes-agent/issues/59305) | Desktop chat tabs leak messages across sessions (cross-tab mixing) | **OPEN** | Session state corruption in the app. |

### 6. Feature Requests & Roadmap Signals

- **Skill Authoring Tooling:** Feature requests for `hermes skills lint` ([#37352](https://github.com/NousResearch/hermes-agent/issues/37352)) and the re-landing of the **dynamic-workflow orchestration skill** ([PR #59907](https://github.com/NousResearch/hermes-agent/pull/59907)) suggest the project is investing in making skill development more robust and accessible. These are prime candidates for the next point release.
- **Rate Limit Throttling:** The proposal for RPM-based pre-emptive throttling ([#7489](https://github.com/NousResearch/hermes-agent/issues/7489)) using `x-ratelimit` headers is a proactive feature that would improve user experience by preventing 429 errors. Given the high-stability focus, this may move into a "v0.19" roadmap.
- **MCP Stateless Client:** The addition of a stateless MCP HTTP client path ([PR #58126](https://github.com/NousResearch/hermes-agent/pull/58126)) signals alignment with newer MCP protocol standards (2026-07-28), indicating forward-looking architectural work.

### 7. User Feedback Summary

- **Pain Points:**
    - **Desktop vs. CLI Parity:** Users report that the Desktop app behaves differently from the CLI (e.g., ignoring the Codex provider [#58498], hiding non-CLI sessions [#59224]). This is the top source of user confusion.
    - **Session Mixing:** Multiple reports of data leaking between sessions (channels, profiles, tabs) highlight a perception of instability in the core UI/UX layer.
- **Use Cases:**
    - **Heavy Gateway Users:** The community relies heavily on messenger platforms (Telegram, WhatsApp, QQ). Bugs here (timeouts, dropped messages) cause immediate, visible frustration.
    - **Profile Management:** Users are actively trying to manage multiple profiles (e.g., work/personal), but the cross-profile data leak bugs are undermining this workflow.
- **Satisfaction:** The swift closure of P1 bugs like the Telegram hang and the copilot auth loop suggests the team is responsive, which likely maintains a base level of trust.

### 8. Backlog Watch

The following items are important but have received no recent maintainer activity, suggesting they may be stuck in the backlog:

- **[Issue #14980](https://github.com/NousResearch/hermes-agent/issues/14980): WhatsApp bridge npm install timeout (P1, 5 comments, 3 👍)** – Created 2026-04-24. This is a blocker for users on NAS systems (e.g., Unraid). Despite being tagged P1, it remains open with no linked fix PR. **This needs triage.**
- **[Feature #527](https://github.com/NousResearch/hermes-agent/issues/527): RBAC for Gateway Permissions (11 comments, 6 👍)** – Created 2026-03-06. While it has strong community support, it is a large architectural change that has not seen formal design discussion in recent months. It is a high-signal feature that may be deferred to a major version bump.
- **[Issue #7489](https://github.com/NousResearch/hermes-agent/issues/7489): Pre-emptive RPM Throttling (2 comments, 5 👍)** – Created 2026-04-11. A well-received feature proposal without a PR or roadmap commitment. It represents a systemic improvement that could reduce the severity of future provider-related bugs.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-07-07

## 1. Today's Overview

PicoClaw is in a **high-activity, stability-focused phase** today, with 4 issues and 5 PRs updated in the last 24 hours. The community is driving critical bug fixes and thoughtful proposals around provider compatibility and prompt caching — a clear sign the project is maturing toward production-grade agent infrastructure. One major bug (#2191) was closed with a companion fix PR (#3228), while two new feature requests and a Gemini API interop bug surfaced. The project shows strong contributor momentum, led by recurring committers (AayushGupta16, jp39) addressing both correctness and developer experience.

## 2. Releases

No new releases today. The latest available version is 0.3.1 (as referenced in issue #3230).

## 3. Project Progress

**Merged/Closed PRs (1):**
- **[#3227 — Closed]** `fix(providers): resolve tool_use name/args from Function on reloaded history` by AayushGupta16 — Fixed a silent corruption bug where both `anthropic` and `anthropic_messages` providers lost tool call metadata (`Name` and `Arguments`) after the chat history was serialized and reloaded, because those fields were tagged `json:"-"` and never persisted. This is a **critical fix** for session continuity in long-running agent workflows.

**Notable Open PRs trending toward merge:**
- [#3228 — fix(anthropic-messages): send SystemParts as system blocks with cache_control](https://github.com/sipeed/picoclaw/pull/3228) — Actively resolves bug #2191, enabling per-block `cache_control` on Anthropic system prompts.
- [#3226 — fix(tools): stop write_file from coaching destructive overwrite](https://github.com/sipeed/picoclaw/pull/3226) — Corrects a UX bug where the overwrite guard actively encouraged destructive behavior.
- [#3118 — Add remote Pico WebSocket mode](https://github.com/sipeed/picoclaw/pull/3118) — Long-running feature PR for remote agent control via WebSocket.

## 4. Community Hot Topics

**Most Active Discussion (#2191 — 4 comments):**
- **[Bug: `anthropic_messages` provider ignores SystemParts, breaks Anthropic prompt caching](https://github.com/sipeed/picoclaw/issues/2191)** (CLOSED)
  - Author: whtiehack | Created: 2026-03-30 | Comments: 4 | 👍: 0
  - Analysis: This long-standing issue (3+ months) was finally resolved today via PR #3228. The root cause was a flat string serialization of `system` messages, which made Anthropic's `cache_control` markers impossible to use. The fix unlocks ~90% cost savings on repeated system prompts for heavy agent users. The delay suggests the provider abstraction layer has been a pain point needing careful design.

**Rising Discussion (#3229 — no comments yet but highly substantive):**
- **[Proposal: rolling conversation cache breakpoints for anthropic-messages](https://github.com/sipeed/picoclaw/issues/3229)** (OPEN)
  - Author: AayushGupta16 | Created: 2026-07-06
  - Analysis: Proposes extending #3228's fix with rolling cache breakpoints on conversation history — a natural next step that could cut API costs 5-10x for long-running tool-use sessions. The author references "agentic workloads" as the driving use case.

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **P0** | [#3230](https://github.com/sipeed/picoclaw/issues/3230) | Function call returns `missing thought_signature` error when Gemini API is called via OpenAI-compatible format (Cloudflare AI Gateway) | OPEN, no fix PR yet |
| **P0** | [#3227](https://github.com/sipeed/picoclaw/pull/3227) | `tool_use` name/args lost on session history reload (affects all Anthropic providers) | **CLOSED today** via PR #3227 |
| **P1** | [#2191](https://github.com/sipeed/picoclaw/issues/2191) | `anthropic_messages` ignores `SystemParts`, breaking cache_control | **CLOSED today** via PR #3228 |
| **P2** | [#3226](https://github.com/sipeed/picoclaw/pull/3226) | `write_file` tool coaches destructive overwrite instead of safe merge | Fix PR OPEN |

**Critical note on #3230:** This affects users routing Gemini through Cloudflare AI Gateway (OpenAI compat mode) — a growing deployment pattern. The error appears in versions 0.2.9 through 0.3.1, suggesting a recently introduced regression.

## 6. Feature Requests & Roadmap Signals

**High-Probability Next-Release Features:**
1. **Anthropic system prompt caching** (PR #3228) — Likely to merge within days; enables `cache_control` on `SystemParts`. Predicted impact: 60-80% cost reduction for agents with fixed system prompts.
2. **Remote WebSocket agent mode** (PR #3118) — Long-running since June 12. Adds `picoclaw agent --remote ws://...` for headless/remote control. This is a **major architectural feature** that could enable PicoClaw-as-a-service deployments.

**Speculative Roadmap Signals:**
- **Rolling conversation cache breakpoints** (Issue #3229) — If PR #3228 merges cleanly, this natural extension for dynamic conversation caching could appear in 0.4.x.
- **SearXNG authentication support** (Issue #3231) — User requested BasicAuth header support for SearXNG search tool, indicating growing use with self-hosted search engines.

## 7. User Feedback Summary

**Pain Points:**
- **Gemini/OpenAI compat interop:** VictorSu000 reports `thought_signature` error when using Gemini through Cloudflare AI Gateway — a blocker for multi-provider workflows (Issue #3230).
- **Tool call persistence:** The silent loss of tool call metadata on session reload (PR #3227) was causing agents to "forget" what tools they'd called after history serialization — a disorienting experience for long sessions.
- **Overwrite coaching:** Users perceived the `write_file` tool as "gaslighting" them into destructive overwrites when safer merge behavior exists (PR #3226).

**Use Cases Emerging:**
- **Agent-as-a-service:** WebSocket remote mode (PR #3118) points toward production deployments where PicoClaw runs as a backend service.
- **Self-hosted search:** BasicAuth for SearXNG (Issue #3231) suggests users are integrating PicoClaw with private search infrastructure.
- **Cost-sensitive deployments:** The cache_control fixes (#2191, #3229) show a user base acutely aware of API costs at scale.

**Satisfaction Indicators:**
- The community proactively files detailed, technical proposals (e.g., #3229 with 3 alternative designs).
- Repeat contributors (AayushGupta16, jp39) are fixing bugs they themselves discovered — a sign of committed power users evolving into maintainers.

## 8. Backlog Watch

**Issues/PRs Needing Maintainer Attention:**

| Issue/PR | Created | Last Updated | Status | Reason for Concern |
|----------|---------|--------------|--------|-------------------|
| [#3118](https://github.com/sipeed/picoclaw/pull/3118) | 2026-06-12 | 2026-07-06 | OPEN, no maintainer review | **25 days stale** — critical new feature (remote agent). Author has made multiple pushes but no core team response. |
| [#3115](https://github.com/sipeed/picoclaw/pull/3115) | 2026-06-12 | 2026-07-06 | OPEN, no maintainer review | **25 days stale** — fixes session-history corruption from inline base64 media. Same author (#3115 and #3118 are from jp39). |
| [#3231](https://github.com/sipeed/picoclaw/issues/3231) | 2026-07-06 | 2026-07-06 | OPEN, 0 comments | Fresh request for SearXNG BasicAuth — low urgency but no response yet. |

**Most concerning:** PR #3118 and #3115 have waited **25 days** without any maintainer feedback. These are substantial contributions (remote agent mode, media extraction fix) from a repeat contributor. Stale PRs risk contributor churn — a pattern to watch.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-07

## 1. Today's Overview
NanoClaw shows **high development velocity** with **10 PRs updated in the last 24 hours** (8 open, 2 merged/closed) and **3 issues updated** (1 closed, 2 open). The project is in a **major documentation modernization cycle**, with four PRs from contributor `glifocat` dedicated to code-grounded staleness sweeps across architecture docs, SDK deep-dives, DB schemas, and README files. Activity is concentrated on operational hardening: **two fix PRs** address silent MCP server failures and provider error recording gaps. No new releases published today; the project appears to be consolidating toward a future minor/major release.

## 2. Releases
**None.** No new releases published in the last 24 hours. Last known working base appears to be `v2.1.38` (referenced in documentation rewrite PRs).

## 3. Project Progress
**Two PRs merged/closed today:**

- **[#2967 — feat: opt-in local audit log (AUDIT_ENABLED)](https://github.com/nanocoai/nanoclaw/pull/2967)** (merged) — Adds NDJSON audit logging for all `ncl` commands with `ncl audit list` read-back and a post-write hook registry for future in-process exporters. This is a **significant internal observability feature** v1.

- **[#16 — Escape special regex characters in assistant name trigger pattern](https://github.com/nanocoai/nanoclaw/pull/16)** (closed) — Fixes a long-standing bug where special regex characters in `ASSISTANT_NAME` could break pattern matching. Originally from February 2026, now finally resolved.

**Key advancement:** The audit log feature (PR #2967) provides SIEM-shaped structured events, which is a **critical building block for compliance-minded deployments** that need immutable action trails.

## 4. Community Hot Topics
The most active discussion centers on **real-time voice agent capabilities**:

- **[#2960 — Proposal: Live Zoom voice agent + K-ai KB integration](https://github.com/nanocoai/nanoclaw/issues/2960)** (CLOSED, 1 comment, created yesterday) — A design proposal for a voice agent that joins Zoom meetings via RTMS, answers KB questions on wake phrase "Hey K-ai..." using Azure OpenAI Realtime API, and captures full transcripts for action-item extraction. **Underlying need:** Enterprise users want NanoClaw to operate in **live meeting environments**, bridging the gap between async agent interactions and real-time collaboration workflows. The closure suggests this proposal was reviewed and likely greenlit for future development.

- **[#2958 — add-teams: Teams-CLI-first credentials flow in SSF directive grammar](https://github.com/nanocoai/nanoclaw/pull/2958)** (OPEN, 0 comments but significant scope) — Rebuilds Teams integration setup from a ~7-step Azure portal walk to a single `teams login` + `teams app create` flow using Structured Skill Format. **Underlying need:** Users want **frictionless credential flows**—the old Azure portal dependency was a major onboarding barrier for Teams-based agents.

**Documentation modernization** (PRs #2961–#2964) has no direct comments but represents **silent community pain**: four separate PRs from one contributor tackling stale docs suggests users have been encountering incorrect guidance in architecture, SDK, and database documentation.

## 5. Bugs & Stability
**Three reports today, ranked by severity:**

| Severity | Issue/PR | Description | Fix Status |
|----------|----------|-------------|------------|
| **Critical** | [#2968 — MCP server spawn/connect failures are silent](https://github.com/nanocoai/nanoclaw/issues/2968) | Agent runs with missing tools and claims success when MCP servers fail to spawn. No diagnostic surfaced anywhere. | **No fix PR yet** — need maintainer response |
| **High** | [#2966 — Provider errors recorded as completed, not failed](https://github.com/nanocoai/nanoclaw/pull/2966) | Provider errors inside consumed batches are recorded as `completed`, indistinguishable from successful turns. Includes fix for missing failed acks. | **Draft fix exists** in PR #2966 |
| **Medium** | [#2965 — rate_limit_event no longer matches SDK message type](https://github.com/nanocoai/nanoclaw/pull/2965) | SDK 0.3.x changed rate-limit events from `system` subtype to `SDKRateLimitEvent` top-level type; current mapping misses them entirely. | **Fix PR #2965 open** |

**Critical concern:** #2968 means **MCP server failures are invisible**—operators can deploy broken integrations and never know. No PR addresses this yet, making it the most urgent unresolved issue.

## 6. Feature Requests & Roadmap Signals
**Explicit user requests:**

1. **Image generation** ([#2959 — Image generation](https://github.com/nanocoai/nanoclaw/issues/2959)) — User wants to generate a shop logo with "Dream design make a ascetic logo." This is a **basic use case request** that NanoClaw likely cannot fulfill today. Low complexity but signals demand for **multimodal generation** beyond text.

2. **Live Zoom voice agent** ([#2960](https://github.com/nanocoai/nanoclaw/issues/2960)) — Full design proposal for real-time meeting agent with KB integration. Likely **candidate for next minor release** given the detailed proposal and closure (suggesting acceptance).

**Roadmap signals from merged/active PRs:**
- **Structured Skill Format (SSF) buildout** (PR #2958) — credential flows being rebuilt on SSF base, likely paving way for more SSF-based skills
- **Local audit log (PR #2967)** — compliance/observability infrastructure, often a precursor to **enterprise licensing tiers**
- **Security policy (PR #2954)** — Phase 1 security reporting & triage policy signals maturation toward **responsible disclosure program**

**Prediction:** Next version (v2.2.x?) will include SSF-based Teams integration, security policy docs, and possibly the Zoom voice agent POC.

## 7. User Feedback Summary
**Pain points surfaced:**
- **Silent failures frustrate operators** — #2968 (MCP server failures invisible) directly impacts trust in deployments
- **Documentation staleness** — 4 PRs (#2961–#2964) rewriting stale docs suggests users have been misled by outdated guidance
- **Complex credential setup for Teams** — #2958 explicitly replaces a complex Azure portal walk with CLI-first approach

**Use cases demonstrated:**
- **Enterprise compliance** — audit log feature (#2967) addresses SIEM integration needs
- **Real-time collaboration** — Zoom voice agent proposal (#2960) for meeting transcription/action items
- **Small business branding** — logo generation request (#2959) suggests non-technical users expecting image capabilities

**Satisfaction signals:** High contributor velocity (10 PRs in 24h), quick review/merge cadence on bug fixes (#16 closed same day as updated), and structured proposals getting accepted (#2960 closed) indicate a **healthy, responsive maintainer team**.

## 8. Backlog Watch
**Items needing immediate maintainer attention:**

1. **[#2968 — MCP server spawn/connect failures are silent](https://github.com/nanocoai/nanoclaw/issues/2968)** — **Critical** unresolved bug, no assignee, 0 comments. Created yesterday but already urgent. Operators cannot validate MCP server status.

2. **[#2959 — Image generation](https://github.com/nanocoai/nanoclaw/issues/2959)** — Created 2026-07-06, 0 comments. Basic feature request from non-technical user. Clear **quick-win opportunity** — a simple "no" or pointer to Claude's built-in image support would close.

3. **[#2954 — Add Phase-1 security reporting & triage policy](https://github.com/nanocoai/nanoclaw/pull/2954)** — Open since 2026-07-04, marked as "Draft until both maintainer sign-offs land." Needs final approval to establish security processes.

**Long-term watch:** Original PR #16 (recently closed) sat open from February to July 2026 — suggests **regex-related bugs may have lower priority** until critical mass of issues accumulates.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-07-07**.

---

### NullClaw Project Digest – 2026-07-07

**1. Today's Overview**
NullClaw is currently in a low-activity maintenance phase. In the last 24 hours, no new issues were filed or closed, and no new releases were published. The only activity is a single open pull request (#956) from Dependabot, which has been pending for over three weeks without being merged. While the project appears stable with no active bug reports, the lack of recent merged contributions or maintainer interaction suggests a temporary slowdown in development velocity.

**2. Releases**
No new releases were published today. The project has no recent version history to report.

**3. Project Progress**
No pull requests were merged or closed today. The only PR is the open Dependabot update (see Community Hot Topics), which has not yet been actioned by maintainers.

**4. Community Hot Topics**
- **[PR #956: ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956)**
  - *Author:* dependabot[bot] | *Opened:* 2026-06-15 | *Updated:* 2026-07-06 | *Reactions:* 0
  - This is the only item with recent activity. The PR is a routine dependency update for the Docker base image (Alpine Linux 3.23 → 3.24). The lack of any comments or maintainer response for over three weeks may indicate either low urgency or a bottleneck in review capacity.

**5. Bugs & Stability**
No bugs, crashes, or regressions were reported in the last 24 hours. The project currently has no open or active issues, indicating that either the software is stable, or users are not actively raising problems.

**6. Feature Requests & Roadmap Signals**
No feature requests were filed or updated today. Based on the current data, no clear signals for upcoming feature work or roadmap changes can be identified.

**7. User Feedback Summary**
There is no explicit user feedback (comments, reactions, or discussions) recorded in the last 24 hours. The project does not show signs of active pain points or satisfaction expressions in the public issue tracker.

**8. Backlog Watch**
- **[PR #956: ci(deps): bump alpine from 3.23 to 3.24](https://github.com/nullclaw/nullclaw/pull/956)**
  - *Awaiting maintainer action since:* 2026-06-15 (22 days)
  - This is the only item in the backlog. While it is a low-risk dependency bump, prolonged neglect could create security gaps or compatibility friction for users building on the latest Docker images. A review and merge would signal healthy maintenance cadence.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-07-07

## 1. Today's Overview

The IronClaw project shows **very high activity** today following the July 4-5 US holiday weekend, with 41 issues and 50 pull requests updated in the last 24 hours. A significant **bug bash** is in progress, with 14 `[bug_bash_P2]` and `[bug_bash_P3]` issues filed by QA engineer `joe-rlo` covering critical user-facing defects in notifications, error handling, routine feedback, and UI behavior. The development team is heavily focused on **test infrastructure expansion** — particularly around the Reborn harness gate-dispatch system (PRs #5735, #5738, #5740, #5743) — and a **major frontend modernization push** via a series of `[codex]` PRs (#5730–#5732) migrating the WebUI to Vite + TypeScript + pnpm. Approximately 14 PRs were merged or closed today. No new releases were published.

## 2. Releases

**No new releases today.** The latest release chore PR (#5598) remains open and unmerged, proposing version bumps for multiple crates including `ironclaw` from 0.24.0 → 0.29.1, `ironclaw_common` 0.4.2 → 0.5.0 (with API-breaking changes), and `ironclaw_skills` 0.3.0 → 0.4.0 (API-breaking). This release has been open since July 3 and may be blocked by the active bug bash work.

## 3. Project Progress

**Merged/closed PRs (14 total):**
- **#5295** (merged): `fix(loop_support)` — stops forcing subagent goal prompts through the 512-byte safe-summary cap, a long-standing limitation affecting subagent prompt construction.
- **#5176** (closed): `docs(reborn)` — foundational design + PR0/PR1 plan for the **subagent thread harness**, reframing subagents as first-class, addressable, resumable threads.

**Active progress areas (key open PRs):**
- **WebUI frontend modernization** (PRs #5730-#5732): A coordinated four-PR sequence migrating to Vite, TypeScript, and pnpm. PR #5730 (scaffold) and #5729 (pnpm switch) are open; #5728 (ignores fix) is ready; #5731 (TypeScript migration) and #5732 (Vite embed) follow. This is a structural improvement with low risk to production behavior.
- **Reborn test infrastructure expansion**: Seven PRs (#5661, #5692, #5723, #5733, #5735, #5738, #5740, #5743) closing coverage gaps in CAS contention, egress security, gate dispatch, and lease-expiry wedge scenarios. PR #5733 is a production code change fixing a checkpoint forward-through-hooks bug (#5572).
- **Subagent thread harness** (PR #5748): New design doc for how parent threads learn subagent completion and handle crash recovery.

## 4. Community Hot Topics

- **#5713** *[CLOSED] Triggered/scheduled runs that terminate Failed deliver no Slack notification* (3 comments) — Root-caused to a match-arm gap in `slack_delivery.rs` that only builds payloads for `Completed`, `BlockedApproval`, and `BlockedAuth`, discarding `Failed` and other terminal states. This is a **silent automation failure** issue. Now closed, suggesting a fix PR was merged today.

- **#5702** *[bug_bash_P2] GitHub issue search and create capabilities fail with HTTP 403* (2 comments) — A critical integration blocker: the agent's GitHub capability is completely non-functional for issue operations despite correct configuration. No fix link yet.

- **#5553** *[bug_bash_P2] Approval notifications disappear instead of remaining in notification history* (2 comments, opened Jul 2) — Approval notifications are unreliable: they flash briefly and vanish, or never appear for subsequent approvals. This undermines the core approval workflow. Still open after 5 days.

- **#5712** *tool_search discloses full unnarrowed capability catalog under narrowed CapabilityAllowSet* (1 comment) — A **security concern**: `ToolDisclosureCapabilityPort` bypasses the caller's capability allow-set, meaning a restricted agent can still enumerate the entire catalog. Reported by `henrypark133` with a clear code-level summary.

## 5. Bugs & Stability

**High Severity:**
- **#5702** *GitHub HTTP 403 on issue search/create* — P2 blocker; the GitHub integration is entirely broken for issue operations. No fix PR yet.
- **#5553** *Approval notifications disappear* — P2; critical for approval workflow reliability. Open 5 days, no fix linked.
- **#5713** *Silent Slack notification failure* — Now closed (fix likely shipped today). Was causing triggered runs to fail without any notification.
- **#5507** *Failed routine shows "No thread attached"* — Closed. Blocks debugging/root-cause analysis for failed routines.

**Medium Severity:**
- **#5703** *Routine fails with generic error messages* — P2; users cannot diagnose failures. Related to #5552.
- **#5708** *Error banners outside chat stream* — P2; floating error UI elements disassociated from conversation context.
- **#5707** *Routine creation exposes internal implementation details* — P2; user-facing response leaks trigger names, cron syntax, internal command references.
- **#5741** *builtin.http.save fails with OutputTooLarge* — P0-level usage issue: saving large web pages fails entirely rather than truncating or streaming.
- **#5739** *Hardcoded 128K context budget ignores model's context_length* — Affects all large-context models by capping usable context at ~50% and triggering premature compaction.
- **#5734** *Official installers 404* — Download URLs use wrong tag format (`v{version}` vs `ironclaw-v{version}`). Every installer download fails.
- **#5747** *No way to unpair Slack on built-in host-beta* — Once paired, users cannot disconnect. No UI option or `/pair` workaround exists.

**Low Severity / UI:**
- #5706 (raw thread IDs in sidebar under load), #5705 (terminal icon no disable option), #5704 (image transparency during processing), #5701 (activity panel hides tool details), #5556 (chat remains highlighted after navigation) — All P3 UI polish issues from the bug bash.

## 6. Feature Requests & Roadmap Signals

- **Subagent thread harness** (PR #5176 merged, PR #5748 new): The clearest roadmap signal. Subagents are being redesigned from one-shot computations into addressable, resumable threads with parent-agent notification and crash survival. This is a foundational architectural change, likely targeting the next major release (post-bug-bash).
- **Vite/TypeScript frontend migration** (PRs #5730-#5732): Not feature work per se, but the PR descriptions hint at improved developer experience and potential for future frontend capabilities. Likely to land in the next release.
- **CAS-guarded delete** (PR #5749): New `delete_if_version` primitive on RootFilesystem, required by the subagent await-edge delivery design. Infrastructure for P1.0b features.
- **Tool permission save failure surfacing** (Issue #5698): Users cannot see when tool permission changes silently fail in WebUI v2 Settings. A UX fix being tracked.
- **Hide unsupported operator-config fields** (Issue #5696): Inference settings shows Temperature and Embeddings fields that are not supported by the API, causing failed POST requests.

**Prediction for next release:** The subagent thread harness foundation, WebUI frontend overhaul, OAuth wire-format fixes (PR #5579), and the "no-borking-failures" recovery stack (PR #5692) are likely candidates. The blocked release PR (#5598) suggests a coordinated drop once the bug bash stabilizes.

## 7. User Feedback Summary

**Pain Points (explicit in issues):**
- **Silent failures are a major trust issue**: Automated runs (scheduled/triggered) can fail without any notification (#5713). Routine failures show "No thread attached" (#5507) or generic errors (#5703). Users cannot debug why things break.
- **Approval workflow is unreliable**: Notifications for required approvals disappear (#5553), and the Slack pair cannot be undone once set (#5747). This blocks core automation use cases.
- **GitHub integration is broken**: The agent's primary capability for issue search/creation (a flagship feature) returns HTTP 403 for all operations (#5702).
- **Context limits are confusing**: The hardcoded 128K budget (#5739) wastes users' paid model context windows and causes premature truncation. No configuration escape hatch exists.
- **Installers don't work**: New users trying to install get 404s (#5734) — a first-impression blocker.
- **UI clutter and confusion**: Terminal icon cannot be hidden (#5705), error banners float outside chat context (#5708), raw UUIDs show instead of names under load (#5706), image previews ghost during processing (#5704), activity panel shows only "N tools" summary (#5701).

**Satisfaction Signals:**
- The active **bug bash** indicates the team is prioritizing user-facing quality ahead of the next release, which is a strong positive signal.
- The **WebUI modernization** (Vite/TypeScript) addresses long-standing developer feedback about frontend tooling.
- The **test infrastructure expansion** (7+ PRs) suggests engineering confidence in the Reborn architecture and a push toward production hardening.

## 8. Backlog Watch

- **Release PR #5598** (opened Jul 3, 4 days stale): The proposed release bumping 17 crates remains unmerged. It blocks all users from getting the fixes merged in the last week. May be intentionally held for bug bash completion, but deserves a status update.
- **OAuth wire-format fixes PR #5579** (opened Jul 3, 4 days old): Four spec-compliance bugs in OAuth parsing being held open. May be waiting on review or merge conflict resolution with the Reborn hot-path work.
- **Perf tracking issue #5737** (opened today, 7 findings): A second hot-path audit with 7 performance findings across memory, retrieval, skills, host infrastructure, and cross-cutting plumbing. This will generate a wave of follow-up PRs — watch for regression risk.
- **#5722 and #5744** (opened today, both blocking coverage lanes): These describe structural testability problems where real gate-dispatch and auth-resolution code paths are unreachable in the test harness. Both are foundational enabler issues that will need resolution before key coverage can be added.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-07

## Today's Overview
LobsterAI saw a highly active development day with **13 PRs updated in the last 24 hours**, 12 of which were closed or merged. This marks a significant spike in activity following a period of lower engagement, signaling a coordinated push across multiple feature areas. Zero new issues were filed or active, which may indicate the team is focusing on consolidation rather than bug triage. No new releases were cut today, though the volume of merged PRs suggests a near-term version bump is likely. Overall, the project shows strong forward momentum in its **OpenClaw agent framework**, **Cowork collaboration UI**, and **provider integration** layers.

---

## Releases
**None** — No new releases were published today. However, the high volume of merged features and fixes (see below) suggests a release candidate may be imminent.

---

## Project Progress
**12 PRs merged/closed today**, covering substantial ground across rendering, backend, and agent infrastructure:

| Area | PR | Summary |
|------|----|---------|
| **Agent Heartbeat** | [#2280](https://github.com/netease-youdao/LobsterAI/pull/2280) | Added cost-control policy for heartbeat; repaired legacy `HEARTBEAT.md` files |
| **Heartbeat Toggle** | [#2278](https://github.com/netease-youdao/LobsterAI/pull/2278) | New Settings → Agent Engine toggle to enable/disable OpenClaw heartbeat |
| **xAI (Grok) Provider** | [#2276](https://github.com/netease-youdao/LobsterAI/pull/2276) | Added OAuth PKCE login with device-code fallback; registered Grok models |
| **Email Multi-Account** | [#2275](https://github.com/netease-youdao/LobsterAI/pull/2275) | Built-in IMAP/SMTP skill now supports multiple accounts; new settings UI |
| **Cowork Home View** | [#2274](https://github.com/netease-youdao/LobsterAI/pull/2274) | Time-aware greeting, recent-tasks cards, polished quick-action UX |
| **MCP Config Fix** | [#2277](https://github.com/netease-youdao/LobsterAI/pull/2277) | Clears stale transport headers/env/args when switching MCP transport type |
| **Plugin Sync** | [#2279](https://github.com/netease-youdao/LobsterAI/pull/2279) | Hides bundled xAI plugin from user sync to avoid conflicts |
| **Cowork Context** | [#2281](https://github.com/netease-youdao/LobsterAI/pull/2281) | Prevents stale final sync from restarting context maintenance after errors |
| **Settings/Skills UI** | [#2283](https://github.com/netease-youdao/LobsterAI/pull/2283) | Optimized settings, MCP, memory, and mail UI components |
| **Settings Cleanup** | [#2284](https://github.com/netease-youdao/LobsterAI/pull/2284) | Redesigned model provider settings UI; removed home recent-tasks card |
| **Task Delivery Fix** | [#2256](https://github.com/netease-youdao/LobsterAI/pull/2256) | Fixed scheduled-task "no notification" channel not persisting; white screen on model delete |
| **Dependency Bump (open)** | [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) | Electron 40 → 43 and Electron-Builder bump (still open, last updated today) |

---

## Community Hot Topics
No issues or PRs received comments or reactions in the last 24 hours. However, the dependency bump PR [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) (Electron 40 → 43) remains **open for 96 days** and was updated today — the longest-standing open PR. This may reflect maintainer caution around Electron breaking changes or internal prioritization. No community discussion was visible, but the silence itself could indicate either satisfaction or a lack of community engagement channels.

---

## Bugs & Stability
Two bugs were fixed today (both within merged PRs):

| Severity | Bug | Fix PR | Impact |
|----------|-----|--------|--------|
| **High** | Scheduled task notification channel "不通知" failed to persist after save | [#2256](https://github.com/netease-youdao/LobsterAI/pull/2256) | Users were unable to disable notifications for scheduled tasks; form state vs. saved state mismatch |
| **High** | White screen when deleting an active chat model | [#2256](https://github.com/netease-youdao/LobsterAI/pull/2256) | Application crash with no recoverable path; likely a null reference in model selector |
| **Medium** | Cowork context maintenance restarted from stale final sync after chat errors | [#2281](https://github.com/netease-youdao/LobsterAI/pull/2281) | Could cause infinite loop or degraded agent behavior after timeout errors |
| **Low** | Stale MCP transport config (headers/env/args) persisted after form editing | [#2277](https://github.com/netease-youdao/LobsterAI/pull/2277) | Security/configuration leak; cleared fields reappeared |

**No new bugs were filed as issues today.** All fixes were handled internally via direct PRs.

---

## Feature Requests & Roadmap Signals
Today’s PRs reveal several likely roadmap items:

- **Multi-Account Email** ([#2275](https://github.com/netease-youdao/LobsterAI/pull/2275)) — Adding support for multiple IMAP/SMTP accounts with settings management strongly suggests a production-grade email agent feature is near completion.
- **xAI / Grok Integration** ([#2276](https://github.com/netease-youdao/LobsterAI/pull/2276)) — Full OAuth provider support with PKCE and device-code fallback positions LobsterAI to offer Grok as a first-class model partner, likely ahead of competitor frameworks.
- **Heartbeat Cost Control** ([#2280](https://github.com/netease-youdao/LobsterAI/pull/2280), [#2278](https://github.com/netease-youdao/LobsterAI/pull/2278)) — The new toggle and policy prompt address a previously unmanaged cost leak from periodic model calls. This suggests real-world deployments are accumulating API bills.
- **Cowork UX Polish** ([#2274](https://github.com/netease-youdao/LobsterAI/pull/2274), [#2284](https://github.com/netease-youdao/LobsterAI/pull/2284)) — Time-aware greetings, recent-task cards, and hover/focus polish indicate LobsterAI is targeting end-user friendliness, possibly for a public demo or beta release.

**Predicted for next version:** xAI provider, multi-account email, heartbeat toggle, and the Cowork home view overhaul.

---

## User Feedback Summary
No direct user feedback was captured from issues or comments today. However, the fixes reveal inferred pain points:
- **Scheduled task reliability**: The notification channel fix (#2256) suggests users were confused or frustrated by non-persisting "do not notify" settings.
- **Cost sensitivity**: The heartbeat cost-control policy (#2280) indicates power users are experiencing unexpected API charges — a real-money pain point.
- **Provider flexibility**: Adding xAI/Grok OAuth (#2276) shows demand for more model choices beyond the existing set.

Satisfaction signals are absent, but the lack of bug reports may imply the fixes merged today addressed known pain points effectively.

---

## Backlog Watch
| Item | Age | Status | Risk |
|------|-----|--------|------|
| [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — Electron 40→43 bump | **96 days open** | Open, updated today | **High** — Stale dependency could block security patches and new Electron features |
| [#2256](https://github.com/netease-youdao/LobsterAI/pull/2256) — Scheduled task & model delete fix | 5 days to merge | **Merged today** | Resolved |
| All other open items | <1 day | Fresh | None |

The **Electron bump** (#1277) remains the single largest risk item on the backlog. At 96 days, it has likely accumulated multiple minor versions behind current Electron. It is unusual that dependabot has not been force-merged given the volume of other activity — this may warrant maintainer attention for security compliance if the project serves sensitive user data.

---

*Generated from public GitHub data for LobsterAI (netease-youdao/LobsterAI). Data as of 2026-07-07.*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-07-07

## 1. Today's Overview
Moltis shows moderate development activity over the past 24 hours, with no new issues filed and no releases published, but five pull requests updated — three of which were closed or merged. The team addressed several important fixes, including a core MCP OAuth integration fix for Notion and Linear servers, Docker volume mount sanitization, and Telegram streaming consistency. A major dependency upgrade for WhatsApp integration (whatsapp-rust 0.5 → 0.6) was also merged, reflecting active platform support expansion. Overall, the project appears stable with targeted bug fixes and incremental improvements.

## 2. Releases
**None** — No new releases were published on this date.

## 3. Project Progress
Three pull requests were merged or closed in the last 24 hours:

- **#1122 — fix: drop VOLUME declarations that shadow the home bind mount** (Merged/Closed)  
  Removed problematic Docker `VOLUME` declarations that conflicted with bind-mounted home directories. Fixes deployments where the entire `./moltis-home:/home/moltis` bind mount failed due to Docker's volume behavior.  
  [PR #1122](https://github.com/moltis-org/moltis/pull/1122)

- **#1113 — hotfix(telegram): stream final replies without completion notify** (Merged/Closed)  
  Ensures Telegram edit-in-place streaming works correctly even when completion notifications are disabled. Restores expected final-reply behavior after PR #1099.  
  [PR #1113](https://github.com/moltis-org/moltis/pull/1113)

- **#1144 — feat(whatsapp): bump whatsapp-rust 0.5 → 0.6 with LID-native addressing** (Merged/Closed)  
  Major upgrade to WhatsApp integration library enabling LID (Linked ID) addressing, critical for inbound messages after WhatsApp's DM migration. Fixes outbound failures to LID-addressed peers and resolves duplicate contact registration issues.  
  [PR #1144](https://github.com/moltis-org/moltis/pull/1144)

## 4. Community Hot Topics
No issues or pull requests received significant comments or reactions in the last 24 hours. The most noteworthy active PRs are:

- **#1120 [OPEN] — fix(mcp): use direct fetch for resource_metadata URL from WWW-Authenticate**  
  Addresses MCP OAuth failures (`invalid_target`) for servers like Notion and Linear. The fix modifies `discover_and_register()` to handle relative vs. absolute URLs in `WWW-Authenticate` headers. This is critical for users relying on MCP integrations with popular SaaS tools.  
  [PR #1120](https://github.com/moltis-org/moltis/pull/1120)

- **#1087 [OPEN] — chore(deps): bump tar from 0.4.45 to 0.4.46**  
  Routine dependency update, open for over a month — likely awaiting CI approval or minor conflict resolution.  
  [PR #1087](https://github.com/moltis-org/moltis/pull/1087)

## 5. Bugs & Stability
No new bugs were reported in the last 24 hours. The following fixes were merged that address prior stability issues:

| Severity | Issue | Fix Status |
|----------|-------|------------|
| Medium | MCP OAuth fails with `invalid_target` for Notion/Linear servers | Fix PR #1120 open |
| Low | Docker VOLUME declarations shadow home bind mounts | Fixed in #1122 (merged) |
| Low | Telegram streaming fails when completion notify disabled | Fixed in #1113 (merged) |
| Medium | WhatsApp outbound messages fail to LID-addressed peers | Fixed in #1144 (merged) |

No regressions were introduced.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, merged PRs signal upcoming capabilities:

- **WhatsApp LID-native addressing** (#1144) — Indicates Moltis is prioritizing WhatsApp integration maturity and stability in response to WhatsApp's infrastructure changes. This suggests a broader shift toward supporting legacy contact migration.
- **MCP OAuth resilience** (#1120) — The fix for `resource_metadata` URL handling reveals that MCP integrations with major SaaS tools (Notion, Linear) are a focus area for upcoming releases.
- **Telegram streaming polish** (#1113) — Continued refinement of real-time messaging UX, likely aimed at enterprise users who require reliable streaming with configurable notifications.

**Prediction**: The next minor release (likely v0.x.y) will include the WhatsApp 0.6 upgrade, the MCP OAuth fix, and the Telegram streaming hotfix. Docker volume improvements suggest potential for a Docker-focused patch release.

## 7. User Feedback Summary
No explicit user feedback (comments, reactions) was recorded in the last 24 hours. Based on resolved issues and PR descriptions, the following pain points have been addressed:

- **Docker deployment friction** — Users who bind-mount entire home directories (e.g., `./moltis-home:/home/moltis`) experienced failures due to Docker's volume precedence rules. This has been fixed.
- **Telegram streaming inconsistency** — Users who disabled completion notifications found final replies were not streamed properly. This hotfix restores expected behavior.
- **WhatsApp contact migration failures** — Users experienced outbound failures to contacts migrated to LID addressing, and duplicate contact registrations. The library upgrade resolves these.

## 8. Backlog Watch
The following item on the backlog may need maintainer attention:

- **#1087 — Bump tar from 0.4.45 to 0.4.46** (Open since 2026-05-29)  
  A routine dependency update that has been open for over a month with no blockers mentioned. May require a review or rebase to merge.  
  [PR #1087](https://github.com/moltis-org/moltis/pull/1087)

No long-unanswered issues or PRs with significant community impact were identified beyond this.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the **CoPaw project digest** for **2026-07-07**, generated from the provided GitHub data.

---

## CoPaw Project Digest – 2026-07-07

### 1. Today's Overview
Project activity is extremely high, with a significant focus on **stabilization and regression testing**. A total of **34 issues** were updated (25 active) and **50 PRs** were updated (25 merged/closed), indicating a mature engineering cadge. The team released a critical hotfix (`v1.1.12.post3`) to patch an import-breaking dependency issue, and a major contributor (hanson-hex) landed a large batch of unit test suites (PRs `PR-A1` through `PR-A4`, `PR-F1` through `PR-F3`), significantly shoring up project reliability. Despite this, a high volume of bug reports—particularly regarding context management, channel connectivity, and frontend performance—suggests the project is currently in an intensive stabilization phase following recent feature growth.

### 2. Releases
- **v1.1.12.post3** (Released 2026-07-06)
    - **Changes:** Pinned the `agent-client-protocol` (ACP) dependency to `<0.11.0` to resolve a breaking change in ACP that caused older `1.x` versions of QwenPaw to crash with an `ImportError`.
    - **Breaking Changes:** None.
    - **Migration Notes:** 1.x users should upgrade directly. Users on v2.0.0 pre-release are not affected by this specific patch, but the team notes this is a fix for the 1.1.x line.

### 3. Project Progress
25 PRs were merged or closed in the last 24 hours. Key advances include:
- **Core Stability:** The patch release `v1.1.12.post3` (PR #5818) merged, fixing the critical ACP import error (Issue #5816).
- **Code Health (Testing):** Hanson-hex merged a series of regression test suites covering the **inbox**, **channels**, **approvals**, and **runtime/security** modules (PRs #5809, #5811, #5812, #5813) as well as frontend contract-guard and store tests (PRs #5807, #5808, #5810). This dramatically improves coverage reliability.
- **Bug Fixes:** Merged fixes for the double `/api` prefix bug in the Console (PR #5769) and a naive datetime stamping issue in `AgentMdManager` (PR #5768).

### 4. Community Hot Topics
The community is heavily engaged in reporting quality-of-life issues and configuration complexities:

- **Issue #5757 (Open, 11 comments): [飞书信息不回复情况]** – Users report that after the first message, the bot stops replying via Feishu (Lark) channel, indicating a persistent agent state or channel listener bug.
- **Issue #5401 (Open, 8 comments): [Console: large tool-use history causes crash]** – A frontend rendering crash when sessions contain a high number of tool calls. Users are frustrated by a white-screen experience.
- **Issue #5273 (Open, 5 comments): [v2.0.0 Pre-release Bug Tracker]** – The central tracking issue for the v2.0.0 alpha/beta releases remains active, gathering regressions.
- **Issue #5567 (Open, 2 comments): [GitHub Issue Feedback Skill]** – A user-created Skill to format reports for the GitHub repo. This signals a high desire among users to contribute effectively, but also shows the complexity of the official bug-reporting process.

### 5. Bugs & Stability
Bug volume is elevated today. The following represent the highest severity, with fixes available or in progress:

- **Critical: #5782 (Closed): [Google Gemini embedding index=None crash]** – Google Gemini API via OpenAI-compatible endpoints returned `index=None`, causing a `TypeError` and silent fallback to keyword-only search. **Fixed (CLOSED).**
- **Critical: #5816 (Closed): [ACP ImportError crash]** – A breaking ACP dependency version completely prevented the app from starting. **Fixed in v1.1.12.post3.**
- **High: #5775 (Open): [Auto-memory never triggers]** – The `auto_memory_interval` feature is completely broken in v2.0.0b3 because middleware state is lost per-request. No PR linked yet.
- **High: #5773 (Open): [Memory search breaks OpenCode channel]** – Enabling memory search causes total failure for DeepSeek models via the OCG provider. No PR linked.
- **Medium: #5710 (Open): [Context compression cuts critical anchors]** – Compression removes crucial context (e.g., channel identity), leading to inappropriate bot behavior. PR #5765 is open to fix this via a "graduated pressure relief" mechanism.
- **Medium: #5725 (Open): [Console streaming lag]** – Users report significant browser lag during streaming output, making the console nearly unusable for long answers. No PR linked.

### 6. Feature Requests & Roadmap Signals
Users are requesting **granular control and broader platform support**:

- **#5785 (Open): [Coding mode: select hidden files]** – A request to allow the Agent to access dotfiles (`.hidden`) in the workspace in coding mode. High utility for developers.
- **#5797 (Open): [Cron task notification toggle]** – Users want a per-task toggle for popup notifications rather than the current "all or nothing" approach. **Predictions:** Likely to land in the next minor release (v1.1.13 or v2.0.0) as it has strong backing (2 comments).
- **#5780 (Open): [Multi-user account management]** – A request for proper team/user management, beyond the current single-bot auth model. **Predictions:** This is a major feature. Likely targeted for v2.1.0, not the immediate stable release.
- **#5168 (Open): [Zalo Bot channel support]** – A feature request from the Vietnamese community. **Predictions:** Likely low priority unless community contributions arise.
- **#5821 (Open): [Granular media rejection]** – Instead of stripping *all* media when one type fails, filter per-type. Indicates deep use of multimodal capabilities.

### 7. User Feedback Summary
- **Positive:** The community is highly technical and engaged, creating custom skills (Issue #5567) and filing detailed, high-quality bug reports. The rapid release of hotfix `post3` shows responsiveness.
- **Negative:** A strong undercurrent of **dissatisfaction with context management**. Users report the bot "forgetting" what channel it is in (Issue #5710) or treating stale messages as active tasks (Issue #5776). The "one-size-fits-all" approach to notifications (Issue #5797) is also a recurring complaint. The **console performance** (crash on large logs, streaming lag) is a significant UX pain point.
- **Core Pain Point:** The most common complaint is the **fragility of the conversation context**—both compression losing important data and the auto-memory feature failing silently.

### 8. Backlog Watch
The following issues are open, have significant community interest, but appear to have no active fix PRs or recent maintainer attention:

- **#5253 (Open since June 17): [custom_channel listener crashes on save]** – A critical reliability bug that disables custom channels. 5 comments, no maintainer response in the excerpt.
- **#5401 (Open since June 23): [Console crash on large tool-use histories)** – This is a frontend rendering bug that locks users out of their data. Highly important for UX but no linked PR.
- **#5725 (Open since July 2): [Console streaming lag]** – A high-visibility performance issue. No linked fix despite 4 comments.
- **#5775 (Open since July 4): [Auto-memory never triggers]** – A v2.0.0 regression that completely disables a core feature. This is critical for the v2.0.0 release, but no fix PR is linked.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-07-07

## Today's Overview

ZeroClaw shows **high sustained activity** with 50 issues and 50 PRs updated in the last 24 hours, indicating a project in active development. Most issues remain open (47 of 50), and PRs are similarly weighted toward open work (41 of 50), suggesting a deep backlog under active management. No new releases were published today; the project is in a **heavy implementation phase** across multiple tracks including goal-mode features, security hardening, channel integrations, and quality gate fixes. The v0.8.3 milestone remains the primary delivery target, with v0.9.0 (auth/security/breaking changes) also accumulating work.

## Releases

None published today. The latest release remains v0.8.x (no version bump indicated).

## Project Progress

Three PRs were closed/merged in the last 24 hours:
- **#8779** — fix(zerocode): use daemon final text when no streaming text was accumulated (project will now fall back to non-streaming content)
- **#8777** — fix(zerocode): strip markdown fences from code block copy text (UX fix for copy-paste)
- **#8778** — chore: Optimize images (repo housekeeping)

Active feature work advancing:
- **Goal-mode implementation** is being split into reviewable PRs ([tracker #8681](https://github.com/zeroclaw-labs/zeroclaw/issues/8681)), with three large PRs (#8688, #8689, #8746) representing the goal tools, channel admissions, and loop-prevention fixes
- **Cron enhancements**: `uses_memory` flag exposed in CLI/tools/gateway API ([#8676](https://github.com/zeroclaw-labs/zeroclaw/pull/8676)), `shell_output_format` config for raw stdout ([#8438](https://github.com/zeroclaw-labs/zeroclaw/pull/8438))
- **Plugin permission model**: RFC under discussion with open questions on config/secrets model ([#8398](https://github.com/zeroclaw-labs/zeroclaw/issues/8398))
- **Security**: Sandbox policy config struct added ([#7821](https://github.com/zeroclaw-labs/zeroclaw/pull/7821)), browser screenshot path validation ([#8741](https://github.com/zeroclaw-labs/zeroclaw/pull/8741))

## Community Hot Topics

| Issue/PR | Comments | Topic |
|----------|----------|-------|
| [#8193](https://github.com/zeroclaw-labs/zeroclaw/issues/8193) | 16 | **MCP tools missing from TUI** — users blocked; gateway sees tools but TUI sessions don't; S1 severity; regression guard PR [#8775](https://github.com/zeroclaw-labs/zeroclaw/pull/8775) now open |
| [#6808](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) | 13 | **RFC: Work Lanes & Board Automation** — governance RFC in rollout; 11 revisions; accepted/in-progress |
| [#2503](https://github.com/zeroclaw-labs/zeroclaw/issues/2503) | 9 | **NapCat/OneBot channel request** — user needs QQ channel support; open since March 2026; accepted P2 |
| [#8681](https://github.com/zeroclaw-labs/zeroclaw/issues/8681) | 8 | **Goal-mode implementation split** — tracker for moving accepted design into reviewable PRs |
| [#8505](https://github.com/zeroclaw-labs/zeroclaw/issues/8505) | 4 | **Telegram channel not configurable** — S1 workflow block; channel doctor claims not set up despite correct config |

**Underlying need analysis**: The most commented items reveal three community pressure points:
1. **Channel reliability** — QQ, Telegram, and MCP tool visibility issues suggest the channel/adapter layer needs hardening before v0.9.0
2. **Configuration friction** — Users cannot easily configure channels or switch models mid-session
3. **Feature parity** — Users want OneBot/NapCat, OpenAI-compatible API adapters, and voice channels

## Bugs & Stability

### Critical (S1 — Workflow Blocked)
- **#8193** ([CLOSED](https://github.com/zeroclaw-labs/zeroclaw/issues/8193)): MCP tools missing from TUI — **PR [#8775](https://github.com/zeroclaw-labs/zeroclaw/pull/8775)** adds regression test guard
- **#8505** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/issues/8505)): Telegram channel cannot be configured — user verified correct config but channel doctor disagrees
- **#8675** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/issues/8675)): Malformed tool-call arguments sent unvalidated to OpenAI-format providers → provider 400 → empty reply
- **#8753** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/issues/8753)): CI quality gate misses member-crate test targets — broken test code can land on master
- **#8631** ([CLOSED](https://github.com/zeroclaw-labs/zeroclaw/issues/8631)): Headless deterministic SOP steps recorded as Completed without executing (S2, but false-green audit trail)

### High Risk
- **#8747** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/pull/8747)): SOP engine allows advancing through approval gates — fixes auth bypass in SOP workflow
- **#8690** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/pull/8690)): `/model --agent` command lacks per-sender authorization — fix gates behind sender identity check
- **#8741** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/pull/8741)): Browser screenshot can write to any path — no path validation before 2026-07-05

### New Today
- **#8780** ([OPEN](https://github.com/zeroclaw-labs/zeroclaw/issues/8780)): Feature request for realtime speech-to-speech channel (Gemini Live) — filed today with 0 comments

## Feature Requests & Roadmap Signals

### High Likelihood for Next Release (v0.8.3 or v0.9.0)
- **Goal-mode implementation** ([#8681](https://github.com/zeroclaw-labs/zeroclaw/issues/8681)) — three large PRs (#8688, #8689, #8746) already in review
- **OpenAI Chat Completions adapter** ([#8603](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) — RFC with 3 comments; would enable Open WebUI/LobeChat integration
- **Per-chat model switching** ([#8600](https://github.com/zeroclaw-labs/zeroclaw/issues/8600)) — user request from moltis migration; P2 with 2 comments
- **Realtime voice-host channel** ([#7943](https://github.com/zeroclaw-labs/zeroclaw/issues/7943)) — accepted P2; voice satellite device track ([#7944](https://github.com/zeroclaw-labs/zeroclaw/issues/7944)) also active

### Lower Priority / Speculative
- **Plugin permission model** ([#8398](https://github.com/zeroclaw-labs/zeroclaw/issues/8398)) — RFC blocked on design decisions
- **Auto-resume Code session** ([#8653](https://github.com/zeroclaw-labs/zeroclaw/issues/8653)) — P3 accepted, small scope
- **ZeroClaw logo on Agent Skills client list** ([#5262](https://github.com/zeroclaw-labs/zeroclaw/issues/5262)) — P2 accepted, no-stale

## User Feedback Summary

### Pain Points
1. **Channel configuration is brittle** — Telegram (#8505), QQ (#7872), and Discord (#7831) channels have known configuration or interaction parity issues
2. **MCP tool visibility is broken** — Users in discussion #8045 reported that MCP servers expose tools but TUI sessions don't receive them (#8193)
3. **Provider model switching is difficult** — User migrating from moltis cannot easily switch between models within a provider (#8600)
4. **Non-UTF-8 file reading returns garbled text** — `file_read` falls back to lossy UTF-8 for cp1251/Latin-1 files (#7521, #8602)

### Use Cases
- **Voice assistant** — Two connected feature requests for voice satellite + realtime voice host (#7943, #7944), plus new Gemini Live proposal (#8780)
- **Enterprise SOP automation** — Users relying on deterministic SOP execution with cron/MQTT triggers (#8631)
- **Multi-agent deployment** — Agent alias injection into system prompts (#6311) for V3 multi-agent UX

### Satisfaction Indicators
- Active community participation in RFCs (13 comments on #6808, 3 comments on #8603)
- Multiple contributors filing PRs — 12 unique PR authors in last 24h
- Users engaging with quality-gate improvements (#8753) and security hardening (#8675)

## Backlog Watch

### Issues Needing Maintainer Attention
- **#8603** ([RFC: OpenAI Chat Completions adapter](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)) — 3 comments, marked `needs-maintainer-review`, no maintainer response visible
- **#8600** ([Per-chat model switching](https://github.com/zeroclaw-labs/zeroclaw/issues/8600)) — 2 comments, `needs-maintainer-review`, no-stale
- **#8398** ([Plugin permission model RFC](https://github.com/zeroclaw-labs/zeroclaw/issues/8398)) — Blocked with open questions; 1 comment, no maintainer response
- **#8602** ([Enhanced file_read features](https://github.com/zeroclaw-labs/zeroclaw/issues/8602)) — Blocked, needs-maintainer-review, no-stale

### Stale PRs
- **#7821** ([Sandbox policy config](https://github.com/zeroclaw-labs/zeroclaw/pull/7821)) — `stale-candidate` label, 20 days since last update, `needs-author-action`
- **#8576** ([OpenAI STT env-var fallback](https://github.com/zeroclaw-labs/zeroclaw/pull/8576)) — 6 days since update, no merge activity

### Long-Open Tracker
- **#2503** ([NapCat/OneBot channel](https://github.com/zeroclaw-labs/zeroclaw/issues/2503)) — Open since 2026-03-02 (4+ months), accepted P2, no implementation visible

---

**Project Health Assessment**: ZeroClaw is in a **healthy but stretched** phase — heavy implementation across multiple tracks, active community contribution, but with several S1 workflow-blocking bugs and a growing backlog of feature requests. The quality-gate gap (#8753) is a notable engineering risk. The goal-mode and security tracks suggest v0.8.3 and v0.9.0 will introduce significant new capabilities.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*