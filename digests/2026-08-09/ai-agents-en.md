# OpenClaw Ecosystem Digest 2026-08-09

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-09 00:43 UTC

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

Based on the provided GitHub data for OpenClaw (openclaw/openclaw), here is the project digest for 2026-08-09.

---

## 1. Today's Overview

OpenClaw shows very high activity with 500 issues and 500 PRs updated in the last 24 hours, indicating a large and actively maintained project. The main focus is on stability, with many open issues targeting critical bugs around session state, message loss, and crash loops. Two new patch releases (v2026.6.34, v2026.6.33) were published, both concentrating on hardening security boundaries for network and browser access. The project is in a heavy bug-fixing and code-hardening phase, with numerous PRs targeting the most critical issues.

## 2. Releases

Two new versions were released in the last 24 hours.

- **v2026.6.34**: Focuses on safer browser and network boundaries. It introduces sandboxed browser routes, trusted DNS targets, custom browser origins, and loopback provider endpoints that reject unsafe access paths. (#97958, #38290, #103075, #110693)
- **v2026.6.33**: Focuses on safer network and secret boundaries. It caps hostile response sizes for provider streams, Discord REST, browser fetches, and OAuth paths, and keeps Telegram credentials out of diagnostics. (#96989, #95412, #99428)

There are no explicit notes regarding breaking changes or migration steps provided for these patch releases. However, given the emphasis on security hardening and the existence of open issues related to browser functionality, users may want to review their browser and network configurations.

## 3. Project Progress

This section typically covers merged/closed PRs; however, the data provided does not detail the specific merged/closed PRs. The data does show 178 PRs were merged/closed in the last 24 hours. Among the open PRs, several target key fixes and features that are in progress.

- **Fixes for session state and stability**: PRs are actively addressing recovery issues. `fix(agents): defer requester-settle wakes until gateway request scope is ready (#119915)` and `fix(agents): prevent requester settle while child is still running (#120601)` target subagent orchestration bugs.
- **Gateway compatibility**: `fix(gateway): keep new nodes compatible with older gateways (#119981)` is a large, maintainer-reviewed PR to allow upgraded nodes to connect to older gateways during staged upgrades.
- **Infrastructure robustness**: `fix(infra): classify virtiofs mounts as rollback-journal storage (#120694)` corrects an issue with SQLite database handling on certain filesystems (like Docker Desktop and OrbStack).
- **Feature work**: A large effort is underway for a "live Desktop observer for cloud workers (Labs)" via Crabbox (`feat(gateway): live Desktop observer for cloud workers (Labs) #120727`). Additionally, a new authorization SDK contract for memory plugins is being introduced with `feat(memory): add authorization SDK contract (#120760)`.

## 4. Community Hot Topics

The most active and urgent discussions are centered on a few critical bugs.

- **#116277 - DeepSeek v4 Flash silent reply failure**: This closed issue has **179 comments**. It's a very active bug report about the model silently failing to generate a reply, posting a generic fallback error instead. The massive comment count suggests a wide user impact and significant investigation.
- **#7707 - Feature Request: Memory Trust Tagging by Source**: This open issue has **31 comments**. Users are requesting a way to tag memory entries by their trust level (user commands vs. web scrapes) to prevent malicious "memory poisoning" attacks, indicating a strong interest in security and data integrity.
- **#44925 - Subagent completion silently lost**: With **24 comments**, this P1 bug highlights a frustrating user experience where subagent results are silently lost without retry or notification, impacting data integrity. The comments and reactions show this is a major pain point.
- **#91588 - Gateway Memory Leak (P0)**: This **P0** issue with **22 comments** reports a severe memory leak that grows to 15.5GB and causes OOM crashes and restart loops, making it a top stability concern for self-hosting users.
- **#80319 - QA tool-defaults suite conflates Codex-native tools**: This issue (17 comments) is about a QA harness issue where tests conflate Codex-native tools with OpenClaw's dynamic tools. It's a discussion around the complexity of maintaining tool parity.

## 5. Bugs & Stability

The project is facing a significant number of high-severity stability and reliability issues. Here are the most critical, ranked by severity.

- **P0: Gateway Memory Leak (#91588)**: A severe memory leak causes RSS to grow to 15.5GB over days, leading to repeated OOM crashes and restart cycles. This is a critical stability issue for the core gateway.
- **P0: Startup migration preflight blocks gateway after upgrade (#112395)**: A regression where upgrading from 6.11 to 7.1 results in the gateway failing to start due to a preflight check blocking on empty migration tables.
- **P0: Regression - Gateway fails to start (#108435)**: A regression in v2026.7.1 where the gateway fails to start with systemd, ollama, or manual launch, blocking all users of that version.
- **P1: Subagent completion silently lost (#44925)**: The loss of subagent task results without any retry, notification, or auto-restart. This is a major data-loss and reliability issue.
- **P1: WhatsApp inbound image wedges lane (#96834)**: Sending an image on WhatsApp 1:1 wedges the message lane for ~3 minutes, preventing prompt processing, a major UX and performance issue.
- **P1: Gateway heap grows to 1073MB+ at idle, cron jobs fail silently (#87109)**: A memory leak on macOS causes cron jobs to fail silently under memory pressure.
- **P1: Loop detection blocks exec but does not terminate stuck agent run (#106231)**: A stuck agent loop burns resources for hours after being detected, as the system doesn't terminate the run.
- **P1: Codex app-server client closes mid-turn (#86214)**: Turns can stop mid-flight with no completion or notification during image/tool requests.
- **P1: AM embedded run aborts memory_search tool calls (#74586)**: The active-memory plugin aborts `memory_search` tool calls, classifying them as timeouts despite model completion.

**Notably**, the data shows that **all of the top 50 issues on this digest remain open**, with many flagged as `clawsweeper:need-maintainer-review` or `clawsweeper:needs-product-decision`. This suggests that while many PRs are in the works (e.g., #120601 for #44925, #119915 for #119869), the maintainers are facing a significant backlog in reviewing and triaging these high-severity bugs.

## 6. Feature Requests & Roadmap Signals

There are strong signals for upcoming features and improvements.

- **Memory Authorization SDK**: Multiple PRs (#120760, #120773) are introducing a versioned authorization contract for memory plugins, likely leading to more secure and fine-grained memory enforcement in a future version.
- **Live Desktop Observer for Cloud Workers**: The large PR `feat(gateway): live Desktop observer for cloud workers (Labs) (#120727)` is a clear roadmap signal for a "Labs" feature that will let operators visually watch and assist agents running on cloud boxes via VNC desktops.
- **Topic-Session Families (#90916)**: There is an open feature request with 8 comments for a "topic-session family" model, allowing one assistant to have multiple named context lanes, an architectural feature for more complex agent deployments.
- **Dynamic Model Discovery (#10687)**: A long-standing (open since Feb) feature request with 10 comments, asking for dynamic model discovery for providers like OpenRouter with fast-moving catalogs.
- **Per-Model Usage Logging (#13219)**: Users are requesting native per-model usage logging for cost tracking and model-mix optimization. This is an ongoing request that is likely next in line for implementation.

Based on this, the **next version is likely to include the memory authorization SDK** (since the contracts are being prepared now), and possibly an early version of the **live desktop observer**.

## 7. User Feedback Summary

User feedback is dominated by pain points around reliability, stability, and data loss.

- **Major Pain Points**:
    - **Silent failures and data loss**: Issues like '#44925 (subagent completion lost)', '#116277 (DeepSeek silent reply failure)', and '#92076 (subagent completion delivery fail)' highlight a critical problem: the agent can fail to deliver results or messages without any warning, making it seem like the tool is working when it's not. This is the most significant source of user dissatisfaction.
    - **Gateway instability and performance**: P0 issues like '#91588 (Memory Leak)' and '#87109 (Gateway heap grows)' cause severe availability problems for self-hosted users, leading to downtime and silent cron job failures. The 'crash-loop' impact tag on several top issues is a strong indicator of this frustration.
    - **Configuration and upgrade friction**: Issues like '#108435 (update fails to start),' '#112395 (upgrade preflight blocks),' and '#61009 (docs/tools/exec says host=node override is allowed... but runtime rejects it)' show users are hitting significant friction when trying to use or upgrade the software.
- **Positive/Satisfaction Signals**:
    - Despite the bugs, the very high level of issue and PR activity shows a strong, engaged community.
    - The quick turnaround of security-focused releases (v2026.6.33 and v2026.6.34 in rapid succession) indicates the team is responsive to community security concerns, which is a positive sign.
    - Users are contributing complex, well-documented bug reports with root-cause analyses, showing a high level of engagement and technical investment.

## 8. Backlog Watch

Several important issues require maintainer attention and have not yet been resolved.

- **#7707 - Feature Request: Memory Trust Tagging by Source**: This very popular issue (31 comments) from February 2026 has been open for 6 months. It addresses a serious security concern (memory poisoning) and is labeled `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`. It seems blocked, not by implementation, but by a product decision.
- **#10687 - Models: fully dynamic model discovery**: Open since February 2026, this issue (10 comments) is also labeled `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision`. It's a clear product direction signal that hasn't been acted upon for months.
- **#80131 - perf: per-request auth (5.5s) and tool bundling (8.9s) dominate gateway TTFT**: This performance issue (5 comments) highlights a significant inefficiency in the gateway's time-to-first-token. It's labeled `clawsweeper:not-repro-on-main`, which could mean it's fixed in a dev branch but not yet confirmed or released, so it remains on the backlog.
- **Open PRs Waiting on Author**: A significant number of PRs in the top 30 are labeled `status: ⏳ waiting on author` (e.g., #120398, #109163, #113901). These PRs are ready for final action, but are blocked on the author's response, suggesting a backlog in the contributor feedback loop.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report — AI Agent Landscape
**Date:** 2026-08-09

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is undergoing a **massive consolidation phase**, characterized by aggressive bug-fixing, security hardening, and architectural refactoring across all major projects. OpenClaw remains the clear core reference with 500+ daily issues/PRs, but the ecosystem is fragmenting into specialized niches: lightweight embedded options (NanoBot, PicoClaw), enterprise-grade rebuilds (IronClaw's "Reborn" migration), and privacy-focused variants (ZeroClaw). The dominant themes across all projects are **session-state integrity, token-cost transparency, MCP server reliability, and memory security** — indicating the market has moved beyond feature exploration into production-hardening. Docker/container deployment issues are the single most recurring friction point across projects, suggesting a pressing need for environment-agnostic runtime guarantees.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score* | Primary Focus |
|---------|-------------|-----------|----------------|---------------|---------------|
| **OpenClaw** | 500 | 500 | 2 patches (v2026.6.33/34) | 8/10 | Stability, security boundaries |
| **IronClaw** | 30 (80% closed) | 50 (64% closed) | None — imminent | 8/10 | "Reborn" architecture migration |
| **CoPaw** | 18 | 50 (3 merged) | None — 2.1.0b2 beta | 7/10 | MCP reliability, provider fixes |
| **Hermes Agent** | 50 | 50 (18 merged) | None — "fix before ship" | 7/10 | Desktop stability, session integrity |
| **ZeroClaw** | 50 (48 open) | 50 | None — v0.8.4 | 6/10 | Security defaults, SOP execution |
| **NanoBot** | 5 | 9 (4 merged) | None — accumulating | 7/10 | Token transparency, MCP stability |
| **PicoClaw** | 3 | 4 | None — v0.3.1 | 5/10 | Review bottleneck, stale PRs |
| **NanoClaw** | 8 | 6 (3 merged) | None | 6/10 | Channel integrations, MCP servers |
| **LobsterAI** | 1 | 3 | None | 4/10 | Maintenance phase, stale items |
| **Moltis** | 2 | 1 (merged) | None | 6/10 | Docker sandbox fixes |
| **NullClaw / TinyClaw / ZeptoClaw** | — | — | — | N/A | Inactive |

*Health Score: composite of responsiveness, closure rate, and community engagement (10 = excellent).*

---

## 3. OpenClaw's Position

**Advantages:**
- **Unmatched breadth AND depth** — 500+ daily issues/PRs dwarfs nearest competitor (IronClaw at 50), indicating dominant mindshare and contributor base
- **Rapid security response** — Two security-focused patches (v2026.6.33/34) shipped within days, addressing browser/network boundaries
- **Large maintainer team** — Can parallelize fixes across 178 PRs merged/closed daily
- **Feature pipeline depth** — Memory authorization SDK, live Desktop observer for cloud workers (Labs), topic-session families

**Technical Approach Differences:**
- **Full-stack monorepo** vs. IronClaw's modularized "Reborn" microservices refactor
- **Dynamic tool ecosystem** with Codex-native tool parity maintenance
- **Multi-surface deployment**: gateway, desktop, CLI, web, embedded (PicoClaw as derivative)

**Community Size Comparison:**
| Metric | OpenClaw | IronClaw | Hermes | ZeroClaw |
|--------|----------|----------|--------|----------|
| Daily Issues | 500 | 30 | 50 | 50 |
| Daily PRs | 500 | 50 | 50 | 50 |
| Hot Issue Comments | 179 (#116277) | 5 (#6989) | 18 (#63047) | 11 (#8043, #8424) |

OpenClaw's 179-comment issue (#116277 DeepSeek failure) alone exceeds the total discussion volume of most competing projects.

---

## 4. Shared Technical Focus Areas

**Cross-project patterns emerging this week:**

1. **MCP Server Reliability** (NanoBot #5300, CoPaw #6822, ZeroClaw #8731, OpenClaw #120760)
   - MCP connection failures crashing gateway processes or permanently blocking conversations
   - OAuth 2.1 web authorization support requested (NanoBot, PicoClaw)
   - Memory authorization SDK contract for plugins (OpenClaw, NanoClaw)

2. **Token Cost Transparency** (NanoBot #5266, IronClaw #6989, OpenClaw #13219)
   - Users reporting 1M tokens consumed in 2 hours with no observability
   - Per-iteration/request logging is the #1 most-requested feature
   - IronClaw's P1: token estimation reads content-reference strings instead of actual content

3. **Session-State Integrity** (OpenClaw #44925, Hermes #82109, NanoBot #5271)
   - Subagent completions silently lost without retry/notification
   - Stale background task references overwriting fresh session data
   - Reasoning-field preservation across forks and branches

4. **Docker/Container Sandbox Issues** (OpenClaw #120694, CoPaw #6782, Moltis #1096/#1185, NanoClaw #3177)
   - Read/Write/Edit tools failing in Docker environments
   - SQLite database lock contention on cross-mount filesystems
   - "Under Maintenance" errors in containerized deployments

5. **Security Defaults and Memory Poisoning** (OpenClaw #7707, ZeroClaw #9348/#9387, Hermes #78515)
   - Memory trust tagging by source to prevent malicious injection
   - Empty allowlists behaving as "allow all" (WhatsApp/Telegram)
   - Interactive approvals accepted from any chat member

6. **Desktop/Installer Stability** (Hermes #63047/#75778/#62171, CoPaw #6810/#6814)
   - macOS 27 beta freezes after ~5 messages
   - Duplicate updater processes on Windows
   - npm 12 allow-scripts policy breaking Linux desktop builds

---

## 5. Differentiation Analysis

| Project | Primary Differentiator | Target User | Architecture | Risk Profile |
|---------|----------------------|--------------|--------------|--------------|
| **OpenClaw** | Breadth — all channels, all models, all surfaces | Power users, enterprises | Monolithic core + plugin ecosystem | High maintenance burden |
| **IronClaw** | Enterprise-grade reliability, "Reborn" modularization | Production automation teams | Typed, domain-owned microservices | Migration complexity |
| **Hermes** | Streamlined session/compression UX | Developers wanting clean history | Node.js, desktop-first, TUI | npm/platform churn |
| **ZeroClaw** | Security-first defaults, privacy focus | Security-conscious operators | Rust-based, multi-crate workspace | Capacity constrained (48/50 issues open) |
| **NanoBot** | Lightweight, fast, token-efficient | Individual developers, hobbyists | Python, WebUI-centric | Small team, emerging |
| **CoPaw** | Chinese-market + international hybrid, Tauri desktop | Cross-border users | Desktop (Tauri) + web | Beta instability |
| **NanoClaw** | Remote MCP + channel breadth | Integration-focused teams | TypeScript, ChannelAdapter v2 | Documentation drift |
| **PicoClaw** | Embedded/constrained devices, SIMpleX/IRC | Privacy/embedded enthusiasts | Lightweight Go/Rust | Review bottleneck — risk of contributor loss |
| **LobsterAI** | Provider-agnostic gateways (LiteLLM) | Cost-conscious multi-provider users | Node.js + SQLite | Stalled performance fix (4 months) |
| **Moltis** | Sandbox portability (Docker first) | Container-heavy deployments | Sandbox abstraction layer | Small topical surface |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapidly Iterating (High momentum, shipping daily):**
- **OpenClaw** — 178 PRs merged daily; shipping security patches within 24 hours of identified needs
- **IronClaw** — 32 PRs merged in 24h, 24 issues closed (80% closure rate); "Reborn" migration closing epics at breakneck pace

**Tier 2 — Actively Stabilizing (Medium-high velocity, consolidation focus):**
- **CoPaw** — Modest merges (3/day) but 47 open PRs and immediate fix-PRs for reported bugs; pre-release stabilization
- **Hermes** — 18 PRs merged; focused on session integrity and desktop fixes; deliberately holding releases for quality
- **ZeroClaw** — High issue/PR volume, but 48/50 issues open indicating capacity constraints; active triage

**Tier 3 — Feature Development (Lower volume, targeted growth):**
- **NanoBot** — 4 merges; accumulating features (temporary chat, token diagnostics) for a future version bump
- **NanoClaw** — 3 merges including remote MCP servers; steady channel work

**Tier 4 — Maintenance Mode (Low activity, risk of stagnation):**
- **PicoClaw** — 0 PRs merged in 24h, 2 stale PRs (43+37 days) awaiting review; risk of contributor attrition
- **LobsterAI** — All items stale; 4-month-old critical fix PR untouched; requires maintainer intervention

**Inactive:** NullClaw, TinyClaw, ZeptoClaw

---

## 7. Trend Signals

**For AI agent developers, five actionable trends from community feedback:**

1. **Trust is the #1 product differentiator.** The three loudest complaints across all projects are: silent failures, untracked token consumption, and invisible data loss. Users will abandon technically superior tools for those that provide observability, audit trails, and explicit failure notifications. **Actionable:** Build per-call telemetry, non-silent retry policies, and deterministic approval semantics into your agent.

2. **MCP is the new integration battleground, but reliability is immature.** Every project with MCP support (#5300, #6822, #8731, #120760) faces gateway-crashing bugs from connection failures. The demand for OAuth 2.1 support (NanoBot, PicoClaw) signals enterprise adoption. **Actionable:** Invest in MCP connection isolation and circuit-breaking; treat remote MCP failures as recoverable events, not process-level crashes.

3. **Security defaults must be "secure by default" — not "safe by naming."** Multiple S1 bugs (ZeroClaw #9348, #9387: empty allowlist = allow all; approval accepted from any member) reveal configuration semantics that invert operator intent. **Actionable:** Audit configuration defaults for failure-mode direction; empty lists should fail-closed; approvals should require explicit role verification.

4. **Container users are mainstream, not edge-case.** Docker sandbox failures (Moltis #1096, CoPaw #6782, NanoClaw #3177) and cross-mount filesystem quirks (OpenClaw #120694) affect a majority of developers. **Actionable:** Test against Docker Desktop, OrbStack, Podman+SELinux, and virtiofs from day one — not just localhost.

5. **Memory poisoning is the emerging threat model.** The memory-trust-tagging request (OpenClaw #7707, 31 comments) and Hermes's unscanned-skill audit (#78515) show users are actively designing against prompt-injection via memory and skills. **Actionable:** Implement source provenance on all memory writes; treat agent-authored content as untrusted until validated.

---

*Report generated from 2026-08-09 community digest summaries across 12 tracked projects in the personal AI assistant / agent ecosystem.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-09

## 1. Today's Overview

NanoBot is in a **high-velocity development phase** with sustained community engagement. Over the past 24 hours, the project saw **5 open issues** (0 closed) and **9 pull requests** (4 merged/closed, 5 open), indicating a healthy mix of incoming bug reports and active feature development. The project's core maintainers are responsive, with several PRs merged on the same day they were opened. Key focus areas this week center on **token consumption transparency**, **MCP stability**, and **system reliability**. No new releases were published, but the rapid PR cycle suggests a significant release may be imminent.

## 2. Releases

No new releases were published during this reporting window. The most recent release remains unchanged, and the project appears to be accumulating features (temporary chat mode, token diagnostics, computer use tools) for a future version bump rather than releasing incrementally.

## 3. Project Progress

Four pull requests were merged/closed today, representing meaningful progress across several areas:

- **[PR #5293 — feat(usage): log per-iteration token diagnostics](https://github.com/HKUDS/nanobot/pull/5293)** *(merged)* — Adds per-iteration token logging, directly addressing issue #5266 about excessive token consumption. This marks the first concrete step toward token usage transparency.
- **[PR #5252 — feat(webui): add temporary chat mode](https://github.com/HKUDS/nanobot/pull/5252)** *(merged)* — Introduces a Temporary Chat mode to the WebUI with non-persistent, multi-turn conversations, giving users a "private browsing" option for sensitive or throwaway interactions.
- **[PR #5294 — fix(webui): prevent image hover clipping](https://github.com/HKUDS/nanobot/pull/5294)** *(merged)* — Resolves a UI visual bug where hover scaling clipped image edges in assistant previews; adds regression tests.
- **[PR #5296 — refactor: remove verified dead code](https://github.com/HKUDS/nanobot/pull/5296)** *(merged)* — Removes 19 dead-code units, 11 test-only seams, and orphaned frontend assets, while preserving six API-sensitive units for future compatibility decisions. This improves long-term maintainability.

## 4. Community Hot Topics

The most active discussion by a significant margin:

- **[Issue #5266 — Logs about token consumption (too many tokens are burned)](https://github.com/HKUDS/nanobot/issues/5266)** — *13 comments, created 8/6, still open*. The community's biggest pain point: a user reports consuming **~1 million tokens in 2 hours** with no visible activity. The demand for token transparency is acute, and the community has rallied around this issue. Notably, two PRs (#5293, #5299) addressing this are already in flight, showing strong maintainer responsiveness.

Also drawing attention:

- **[Issue #5297 — MCP OAuth web authorization support](https://github.com/HKUDS/nanobot/issues/5297)** — *2 comments*. User requests OAuth flow support for MCP servers that require web-based authorization (e.g., XMind API), specifically for remote gateway access scenarios.
- **[Issue #5295 — Docker Compose deployment failure](https://github.com/HKUDS/nanobot/issues/5295)** — *2 comments*. Deployment blocking bug: `entrypoint.sh: Permission denied` during Docker Compose startup.

## 5. Bugs & Stability

Three bugs were reported today, ranked by severity:

**High Severity:**
- **[Issue #5300 — MCP connection failure triggers cross-task crash](https://github.com/HKUDS/nanobot/issues/5300)** — The most concerning issue. When a remote MCP returns HTTP 530 (Cloudflare origin tunnel failure), the client's `anyio cancel scope` crashes across task boundaries, causing the **gateway process to hang, leak tasks, and spike CPU usage**. No dedicated fix PR yet, though this is a critical stability threat.

**Medium Severity:**
- **[Issue #5295 — Docker Compose deployment failure](https://github.com/HKUDS/nanobot/issues/5295)** — `cannot open /usr/local/bin/entrypoint.sh: Permission denied`. Likely a file permission or volume-mount misconfiguration in the deployment template. Blocks new users from deploying via Docker.

**Lower Severity / Reliability:**
- **[Issue #5298 — Unbounded MCP tool schemas inflate context](https://github.com/HKUDS/nanobot/issues/5298)** — Not a crash, but a design issue: large MCP tool sets bloat the model context window, raising cost and latency. This is a performance/cost concern rather than a functional breakdown.

**Existing bug being fixed:**
- **[PR #5271 — Stale background task session overwrite](https://github.com/HKUDS/nanobot/pull/5271)** — Still open. Fixes a race condition where a background task with a stale `Session` reference can overwrite fresh session data after a user runs `/new`. This is a data-integrity issue, not just a cosmetic one, and deserves timely review.

## 6. Feature Requests & Roadmap Signals

Several signals point to near-term roadmap priorities:

**Highly likely in next release:**
- **Token usage transparency** — Issue #5266 plus merged PR #5293 and open PR #5299 (WebUI showing per-call token breakdown) indicate this is a **top priority**. A full usage dashboard is probable.
- **Temporary/Ephemeral chat mode** — Merged PR #5252 suggests this is a planned stable feature, not just a hack.

**MCP-related roadmap items:**
- **OAuth web authorization for MCP** (Issue #5297) — With the rise of MCP servers requiring Web OAuth, this is a natural next step. The request for gateway-level auth handling suggests architectural work is needed.
- **Model-visible MCP schema budgeting** (Issue #5298) — Context-window optimization for large tool sets. May arrive alongside token usage work since both address cost.

**Longer-term / speculative:**
- **Model-agnostic computer use** (PR #4276, open since June) — A large feature adding `computer_use` and `browser` tools for desktop and DOM automation. This remains open after two months and is a substantial addition that may land in a future major release.

## 7. User Feedback Summary

Real user pain points emerged clearly this week:

**Recurring theme: Token cost anxiety.** The #1 complaint (#5266 with 13 comments) is that NanoBot silently consumes tokens at an alarming rate — one user reporting a million tokens in 2 hours. The frustration is compounded by **lack of observability**: users cannot see which calls produced which consumption. This is driving both the diagnostics PRs and the WebUI usage display. This is a **trust issue**: users can't monitor or control spend.

**MCP reliability concerns.** The MCP ecosystem is central to NanoBot's appeal, but failures are disrupting the gateway in catastrophic ways (Issue #5300), and OAuth-protected MCP servers are completely unsupported (Issue #5297). The Chinese-language request (#5297, from a user named "sunboy0523" who also filed #5300) reflects an active, international user base for whom MCP integration is mission-critical.

**Deployment friction.** The Docker-specific `Permission denied` error (#5295) suggests deployment documentation may need revision, and the error message is unhelpful — the user is met with a cryptic `/bin/sh: 0:` error with no guidance.

**Positive signals:** The tone of discussion is constructive; users are filing detailed, well-structured issues with proposed solutions. The maintainer team is responding with fixes on the same day (e.g., #5293, #5296, #5294 all opened and merged within 24 hours).

## 8. Backlog Watch

Items needing maintainer attention:

- **[PR #4276 — Model-agnostic computer use](https://github.com/HKUDS/nanobot/pull/4276)** — Open since **June 10** (60 days). A large, ambitious feature by LarFii. It's marked `[enhancement]` but has sat unreviewed for two months. If maintainers lack capacity, a triage comment with timeline expectations would be valuable.

- **[PR #5271 — Session stale-reference fix](https://github.com/HKUDS/nanobot/pull/5271)** — Open 3 days, marked `priority: p0` and `conflict`. This is a **high-severity data integrity bug** (stale background saves overwriting fresh sessions) with a fix ready. The `conflict` tag indicates merge conflicts need resolution. This should be prioritized over feature work.

- **[Issue #5266 — Token consumption logs](https://github.com/HKUDS/nanobot/issues/5266)** — The most-commented issue, still open. While PRs #5293 and #5299 are addressing it, the underlying question of **why** tokens are being consumed at such scale remains unanswered. Maintainers should investigate the root cause, not just add logging — the community needs assurance this is being actively diagnosed.

- **[PR #5292 — Matrix room-level reply fix](https://github.com/HKUDS/nanobot/pull/5292)** — Small but useful Matrix integration fix, open since today. Should be a quick review and merge.

---

*Digest generated from GitHub activity data for the 24-hour period ending 2026-08-09.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-09

---

## 1. Today's Overview

Hermes Agent is in a period of intense, high-velocity stabilization and consolidation. The project saw **50 issues** and **50 PRs** updated in the last 24 hours, with a healthy mix of new work and cleanups (12 issues closed, 18 PRs merged/closed). The dominant theme is **compression and session-state integrity**: multiple today-only merges landed fixes for reasoning-field preservation across forks (#82109), stale budget charging during compaction (#82116), and a second salvage of the cron multi-delivery UI (#82106). A significant cluster of today's activity targets **desktop installer stability on Windows and npm 12/11 allow-scripts policy**, with at least two competing PRs (#82118, #81983) addressing the same `get-windows` binding failure. Overall, the project appears heavily invested in patching regressions caused by platform/dependency churn (macOS 27 beta, npm 12) while simultaneously consolidating long-running feature PRs (Browser Use CLI mode, Claude Agent SDK provider) into mergable states. Project health is **stable but operating in a high-friction compatibility environment**.

---

## 2. Releases

**No new releases** were published in the reporting window. Users remain on the prior version, which is significant given the volume of desktop/installer bugs being reported (see #81969, #62171). Maintainers are likely in a "fix before ship" phase, with a release candidate uncertain pending resolution of the npm 12 allow-scripts breakage.

---

## 3. Project Progress

Today's merged/closed PRs (18) represent targeted fixes and feature salvages:

- **Session Integrity Fixes (merged):**
    - **#82109** — `fix(state,cli,tui-gateway): keep reasoning fields intact across forks and branches` (closes #57240; also resolves the earlier attempts #57248 and #57454 which were closed today alongside). This is a high-impact merge for anyone using session forks or `/branch`.
    - **#82116** — `fix(compression): charge stale thinking to the tail budget only on the newest assistant turn` (closes #73624). A direct fix for the measured 19-24% compression-budget waste.
- **Desktop/Feature Salvages (merged):**
    - **#82106** — `feat(desktop): support multiple cron delivery targets` (salvage of #73886, itself closed today). The checkbox-group UI is now in.
    - **#82113** — `fix(desktop): keep tool rows and notices out of the HUD band` — UX refinement for the floating HUD.
- **Billing/Metering (merged):**
    - **#82066** — `fix(anthropic): keep OAuth requests on subscription limits` — important for users on Claude subscriptions to stay in-bounds and maintain prompt-cache markers.
- **Configuration (merged):**
    - **#45014** — `Make background review toolsets configurable` — closes a long-running PR (opened June 12) to add `memory.review_toolsets` config.

**Key advancement:** The compression and fork-related fixes (#82109, #82116) directly address the most-commented bug cluster of the past week, signaling strong maintainer responsiveness to session-state risk.

---

## 4. Community Hot Topics

The most active threads underscore user frustration with **desktop stability and update anxiety**:

- **#63047 (18 comments)** — *[Bug]: Desktop app becomes completely unresponsive after ~5 messages on macOS 27 beta.* The top issue. Users are hitting a hard UI freeze — this is generating the most sustained discussion.
- **#78515 (6 comments)** — *background_review security concern: skills bypass content scan.* A security-focused community member filing a thorough defense-in-depth report.
- **#81969 (6 comments)** — *"scared to update because every other update bricks everything!"* A loud, opinionated expression of update fatigue and trust erosion. This is the **community sentiment barometer** today.
- **#40801 (6 comments)** — *Cron script-path guard rejects profile-scoped jobs referencing default profile scripts.* A subtle but longstanding (since June) bug with clear reproduction.
- **#75778 (6 comments)** — *Desktop update handoff produces duplicate `hermes-setup` process.* Directly tied to the update-reliability complaints in #81969.
- **#70846 (5 comments, 1 👍)** — *Compaction wipes message history for humans too.* A UX-critical regression: users lose their own readable history when compaction runs.

**Analysis:** The community is coalescing around three demands: 1) **Desperately needed reliability in the update channel** (no bricks, no duplicate processes), 2) **Preservation of human-readable history** through compression, and 3) **A clear security posture** on agent-authored skills.

---

## 5. Bugs & Stability

Bugs have been ranked by severity (P1 = critical impact):

| Severity | Issue | Description | Fix PR Status |
| :--- | :--- | :--- | :--- |
| **P1** | **#63047** | Desktop app hard-freezes after ~5 messages on macOS 27 beta (even Settings locked). | **No fix PR yet.** Top priority. |
| **P1** | **#81969** | User reports update-failure trauma; believes updates "brick everything." | No single fix; likely umbrella for #75778 and #62171. |
| **P1** | **#75778** | Duplicate `hermes-setup` process on desktop update masks real updater. | **No fix PR yet.** Direct contributor to P1 anxiety. |
| **P2** | **#82001** | Agent flush fails with misleading "full disk" dialog after compression; session handoff gap. | No fix PR yet. |
| **P2** | **#81322** | `lifecycle_guard` rejects benign ELF-binary paths with `embedded null byte`. | **No fix PR yet.** |
| **P2** | **#81846** | "Branch into new chat" button intermittently missing until session reopen. | Needs repro; **no fix PR yet.** |
| **P2** | **#82074** | Podman + SELinux: mounted skills dir inaccessible without `:z` flag. | **No fix PR yet.** |
| **P2** | **#81995** | Stalled MCP cold-spawn hangs tool call for full 300s timeout on dead subprocess. | **No fix PR yet.** |
| **P2** | **#81430** | `memory status` reports "disabled" despite health checks; memory not persisting on Telegram. | Needs repro; **no fix PR yet.** |
| **P2** | **#81162** | Auto voice reply blocks text response on slow TTS backends (gateway sync issue). | **No fix PR yet.** |
| **P2** | **#62171** | npm 12's new default policy breaks Linux desktop package path. | **Two competing PRs:** #82118 (merged) and #81983 (open). |
| **P3** | **#81012** | ANSI SGR sequences defeat redaction (security boundary). | **No fix PR yet.** (Security, but lower data-sensitivity). |

**Notable:** The **Windows desktop `get-windows` failure** (#62171, #81983) was a hot topic yesterday; **#82118 was merged today** to fix it, though #81983 (an equivalent approach) remains open — likely to be closed as superseded. This responsive fix is a positive health signal.

---

## 6. Feature Requests & Roadmap Signals

Active feature signals this week:

- **Browser Use CLI 3.0 mode (#81958, open):** Huge potential impact — unifies 12 browser tools into one `browser_exec` driver over all CDP backends. A "salvage" PR from a closed #66476, indicating maintainers are consolidating long-lived browser work. **Likelihood: High for next major version.**
- **Claude Agent SDK as first-class provider (#65982, open):** Official Claude Agent SDK under subscription OAuth with fail-closed metering. A landmark integration **likely targeted for next version**; the reviewer comments and repeated sweeper tags suggest active heavy scrutiny.
- **Cron "run in current conversation" (#81448, open):** `session_target: "current"` is a significant feature for live-conversation cron. Moderate risk, high utility.
- **Voice server gateway platform (#27040, open):** Generic WebSocket voice platform (Pipecat/Livekit). Long-running PR (since May), but actively updated today — likely being prepared for merge or a final decision.
- **ToolCallStormBreaker (#35573, open):** Suppress identical tool-call loops. A strong community proposal for token savings.
- **Unified global search in Cmd+K (#49103, open):** Search files, sessions, skills. A "Spotlight-like" enhancement that would improve power-user workflows significantly.
- **Memory lifecycle management UX (#78307, open):** Inspect, dedupe, and manage `MEMORY.md`/`USER.md`. Needs decision; likely a good candidate for a smaller milestone.

**Prediction:** The next release is likely a **stability-first "point release"** that includes all the session-state and fork fixes merged today, the Windows/npm installer fixes, and the background-review config. The **Browser Use mode** and **Claude Agent SDK** appear poised to land in a subsequent major/minor release.

---

## 7. User Feedback Summary

- **Update Anxiety is the loudest signal:** #81969 ("every other update bricks everything") and #75778 (duplicate updater) reflect a real, documented reliability gap — users are losing configurations and encountering confusing failure modes. The **lack of a release to include today's fixes** means the community remains in this state longer.
- **Context is invisible to humans:** #70846 (compaction wiping history) and #73624 (budget wasted on unreplayed reasoning) show deep dissatisfaction with how compression behaves — users want *their* narrative preserved, even if token math improves.
- **Model-specific pain:** #78807 (DeepSeek V4 Flash infinite reasoning loop) and #73386 (DeepSeek reasoning) suggest the community is actively exploring new models and finding integration rough edges.
- **Platform friction is high:** macOS 27 beta (#63047), Linux + npm 12 (#62171), Windows encoding (#72641), Windows installer (#81983), and SELinux/Podman (#82074) — a laundry list of environment-specific incompatibilities is straining the user base.
- **Security-conscious users are paying attention:** #78515 (unscanned skills) and #81012 (ANSI redaction bypass) show proactive community auditing and a desire for defense-in-depth.

**Overall sentiment:** Frustrated by update churn, but *engaged and detail-oriented* in reporting. The community clearly values the tool deeply and wants reliability first, features second.

---

## 8. Backlog Watch

These items have been open for an extended period and deserve maintainer attention or a clear decision:

- **#82112 (open, invalid, P3):** A PR titled "Ibranch" with zero description — flagged as `invalid` by the author. Needs closure or a template prompt to avoid noise.
- **#43997 (open, P3, 4 comments):** npm 11 `allowScripts` warnings. Now subsumed by the more critical npm 12 issue (#62171); may need re-scoping or closure.
- **#66978 (open, P2, 4 comments):** `_tui_need_npm_install` triggers on every TUI launch. A nuisance that's been open since mid-July; the root cause is identified clearly, making a fix cheap. **Good first-issue candidate.**
- **#57752 (open, P3, 2 comments):** Session-DB auto-prune is opt-in by default with no user warning. A data-hygiene issue where operators are silently accumulating disk. Needs a decision on defaults or at least a docs warning.
- **#63386 (open, P2, 3 comments):** FTS index corruption on macOS. A data-integrity bug that can break search and handoff; silent persistence could aggravate users. **Worth elevating in priority.**
- **PR #82119 (open):** OpenViking credential leakage fix — a fresh PR today, but it directly addresses a security boundary; needs a fast review cycle to avoid stalling.

**Personally notable:** All three "reasoning-field preservation" PRs (#57248, #57454, #82109) were closed/merged today — a great example of the community converging on a fix. The maintainers correctly prioritized the best-of-breed and shipped it. This is the level of responsiveness users are hoping for on #63047 and #75778 next week.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-09

## Today's Overview

PicoClaw shows moderate activity with 3 issues and 4 pull requests updated in the last 24 hours, though no new releases were published. Notably, all 4 open PRs remain unmerged — including two stale PRs (#3222, #3193) awaiting maintainer review for over a month — suggesting a potential review bottleneck. Activity is balanced across feature development (OAuth 2.1 support, IRC long-message handling), bug fixes (WhatsApp client version, CPU usage), and refactoring (DeltaChat channel cleanup). A closed issue resolves a CPU spike bug in the chat interface. The most promising development is PR #3321 targeting LLM prefix-cache optimization, signaling attention to cost/performance concerns.

**[Full issue list](https://github.com/sipeed/picoclaw/issues)** • **[Full PR list](https://github.com/sipeed/picoclaw/pulls)**

## Releases

No new releases were published in the last 24 hours. The most recent version remains **0.3.1** (referenced in bug report #3292).

## Project Progress

No PRs were merged or closed in the last 24 hours. The only closed item was issue **#3292**, a bug report resolved regarding high CPU usage. However, four PRs are actively being worked on:

- **PR #3321** — [fix(agent): move dynamic context after history to preserve prefix caching](https://github.com/sipeed/picoclaw/pull/3321): Optimizes LLM prefix caching by repositioning dynamic context blocks, reducing token costs.
- **PR #3320** — [fix(deps): bump whatsmeow to unblock WhatsApp "client outdated (405)"](https://github.com/sipeed/picoclaw/pull/3320): Fixes broken WhatsApp channel due to outdated client library.
- **PR #3222** — [refactor(deltachat): cleanup implementation, documentation -200LOC](https://github.com/sipeed/picoclaw/pull/3222): 200-LOC reduction; drops legacy features, moves secrets to JSON-RPC, renames API endpoints. **Stale — awaiting review since July 3.**
- **PR #3193** — [Added simplex channel type](https://github.com/sipeed/picoclaw/pull/3193): Introduces new SimpleX channel. **Stale — awaiting review since June 27.**

## Community Hot Topics

The most discussed items show two clear themes: *protocol robustness* and *missing modern features*.

**1. OAuth 2.1 for MCP servers ([#3302](https://github.com/sipeed/picoclaw/issues/3302))** — Created July 30, 2 comments. User requests OAuth 2.1 support for MCP servers (linked to prior issue #2546, indicating a recurring ask). Classified as "Nice-to-Have," but research indicates this likely reflects a growing enterprise/automation use case.

**2. IRC long-message handling ([#3287](https://github.com/sipeed/picoclaw/issues/3287))** — Created July 22, 4 comments (highest engagement). User wants PicoClaw to treat IRCv3 messages split across 512-byte chunks as a single cohesive message. Currently, split fragments are processed as separate messages, breaking context continuity. This is a functional gap for IRC users sending long AI prompts.

## Bugs & Stability

One bug was reported/resolved this period, plus one acute issue identified via PR:

| Issue | Channel | Severity | Status | Notes |
|-------|---------|----------|--------|-------|
| **High CPU usage** in chat input ([#3292](https://github.com/sipeed/picoclaw/issues/3292)) | Web (Firefox) | Medium | ✅ Closed | Reproduced on v0.3.1 / Linux x64; resolved. |
| **WhatsApp "Client outdated (405)"** ([PR #3320](https://github.com/sipeed/picoclaw/pull/3320)) | WhatsApp | High (service outage) | ⏳ Fix PR open | Channel dead: socket connects then drops within ~5s; no reconnect attempted. Fix bumps `whatsmeow` dependency. |

**Recommendation:** PR #3320 should be prioritized — it restores a broken production channel and unblocks affected users.

## Feature Requests & Roadmap Signals

Active requests:

1. **OAuth 2.1 for MCP servers ([#3302](https://github.com/sipeed/picoclaw/issues/3302))** — Repeated request (links to #2546); signals demand for production-grade MCP integration with modern auth standards.
2. **SimpleX channel support ([PR #3193](https://github.com/sipeed/picoclaw/pull/3193))** — A complete implementation already exists; needs maintainer review. Reflects community interest in privacy-preserving messaging.
3. **IRCv3 long-message handling ([#3287](https://github.com/sipeed/picoclaw/issues/3287))** — Direct usability fix for IRC channel.
4. **DeltaChat API modernization ([PR #3222](https://github.com/sipeed/picoclaw/pull/3222))** — Refactor improves security (secrets via JSON-RPC) and maintenance, but introduces breaking changes (`invite_link` → `join_invite_link`).

**Prediction:** OAuth 2.1 (#3302) has highest likelihood of landing next, given it's a repeated request with a clear pattern. SimpleX (#3193) and DeltaChat (#3222) are "shelf-ready" and only await review/merge.

## User Feedback Summary

- **Frustration: Stale PRs.** Users (`dim` for SimpleX, `trufae` for DeltaChat) submitted complete, well-documented PRs but have waited 43 and 37 days respectively without merge — a risk for contributor attrition.
- **Pain point: Broken channel with no recourse.** WhatsApp users experience complete channel failure with no auto-reconnect; the workaround PR (#3320) is pending.
- **Pain point: Context fragmentation in IRC.** Long AI conversations get split into unrelated messages by IRC protocol limits, degrading the assistant's performance.
- **Positive signal:** Bug #3292 (CPU usage) was closed within ~2 weeks, showing responsive bug-fixing when issues are clearly reproducible.

## Backlog Watch

⚠️ **Critical — no maintainer action yet:**

- **PR #3193 (SimpleX channel)** — Open since **June 27** (43 days) with no activity besides staleness flags. Complete feature; risk of merge conflict or contributor loss.
- **PR #3222 (DeltaChat refactor)** — Open since **July 3** (37 days). Includes breaking API changes; requires migration notes before merge.

⚠️ **Moderate — needs attention this week:**

- **PR #3320 (WhatsApp fix)** — Open 2 days; production outage for users. Should be reviewed and merged promptly.
- **PR #3321 (Prefix caching)** — Open 2 days; high-value optimization for token cost reduction. Likely low-risk.

**Health note:** The two stale open PRs represent approximately **600+ lines of community contribution** held in limbo. A maintainer pass to merge, close, or explicitly defer these would significantly improve contributor trust and project momentum.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date:** 2026-08-09

---

## 1. Today's Overview

NanoClaw saw moderate activity over the past 24 hours with 8 issues and 6 PRs updated. The project appears to be in a healthy state: three issues were closed and three PRs were merged/closed, while feature development continues on channel integrations (Mattermost, Telegram) and MCP server support. A significant environmental bug fix for Docker session database lock contention (PR #3177) was closed, resolving a stability concern. However, several new issues emerged around Discord approval reliability, attachment handling on message IDs containing path separators (Google Chat), and OneCLI secret management design forks, suggesting areas of ongoing refinement in the interaction layer.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

**Merged/Closed PRs:**

- **PR #2776** — *feat: support remote HTTP/SSE MCP servers* (by clementdecoligny) — Closed. This represents a significant architectural advancement, extending `McpServerConfig` to support both stdio (existing) and remote HTTP/SSE MCP servers via `McpServerRemoteConfig` and adding `ncl groups config add-mcp-server` CLI options.

- **PR #2777** — *feat: add /add-strava skill for official Strava MCP* (by clementdecoligny) — Closed. Adds a skill wiring the official Strava MCP endpoint into agent groups via HTTP transport, complete with host-side OAuth flow and auto-refreshing token module.

- **PR #3199** — *Add Mattermost channel integration (v2 ChannelAdapter)* (by wakqasahmed) — Closed. Fresh implementation against the current `ChannelAdapter`/`channel-registry.ts` contract, superseding the outdated pre-v2 PR #546.

**Notable:** A companion PR #3202 also adds Mattermost integration and remains open; it's likely a follow-up or refinement of the closed PR #3199. The fix for Discord approval button clicks (PR #3185) remains open and is directly tied to the closed issue #3201.

---

## 4. Community Hot Topics

- **[Issue #3200] "The Cartographer" — External Cognitive Processing Architecture** (by cyserman, 1 comment) — [Link](https://github.com/nanocoai/nanoclaw/issues/3200) — A qualitative, persona-driven issue describing a user's need for an external modular framework to sort, vet, and protect rapid multi-threaded thoughts. This signals interest in agent architectures that handle cognitive offloading and data protection for high-volume thinking.

- **[Issue #3201] Discord approval button clicks not registering** (by churchcrm-hazel, 2 comments) — [Link](https://github.com/nanocoai/nanoclaw/issues/3201) — Closed, but with the highest comment count today. The issue describes approval cards in Discord failing to record admin/owner votes, displaying "0 by [user]" even after clicking, leading to rejection of config update requests. This is directly addressed by open PR #3185.

- **[Issue #3205] Support persistent group-scoped OneCLI secret assignment** (by chiptoe-svg, 0 comments) — [Link](https://github.com/nanocoai/nanoclaw/issues/3205) — Raises a design fork in how vault secrets are assigned to agents at spawn time, with no persistent per-group model. This is a governance/security design discussion that touches multi-user credential management.

---

## 5. Bugs & Stability

**High Severity:**

- **Discord approval interactions broken** — [Issue #3201](https://github.com/nanocoai/nanoclaw/issues/3201) (Closed): Approval card clicks resolve to the wrong option, causing every approval to be rejected. Root cause appears to be a `\n` delimiter in webhook interaction `custom_id`. **Fix PR exists:** [#3185](https://github.com/nanocoai/nanoclaw/pull/3185) (Open), stripping the delimiter.

**Medium Severity:**

- **Inbound attachments silently dropped on channels with path separators in message IDs** — [Issue #3206](https://github.com/nanocoai/nanoclaw/issues/3206) (Open): `extractAttachmentFiles` gates staging on `isSafeAttachmentName(messageId)`, which rejects any value containing `/` or `\`, breaking Google Chat attachments. **No fix PR found yet.**

- **codex provider emits undeclared ProviderEvent** — [Issue #3203](https://github.com/nanocoai/nanoclaw/issues/3203) (Open): The `codex` provider on the `providers` branch emits a `file` event not declared in `ProviderEvent`, failing container typecheck on `/add-codex`. Generated images are also silently dropped. **No fix PR found yet.**

**Low Severity / Documentation:**

- **add-opencode skill references outdated Dockerfile edits** — [Issue #3204](https://github.com/nanocoai/nanoclaw/issues/3204) (Open): `SKILL.md` still instructs ARG + RUN install layers that no longer exist post `cli-tools.json` refactor; guard test asserts old shape.

**Resolved:**

- **Session database lock contention on Docker cross-mount filesystems** — [Issue #3177](https://github.com/nanocoai/nanoclaw/issues/3177) (Closed): SQLite DELETE journal mode not propagating across Docker mounts caused 29,000+ readonly errors. Fix confirmed.

---

## 6. Feature Requests & Roadmap Signals

- **Mattermost channel integration** — [PR #3202](https://github.com/nanocoai/nanoclaw/pull/3202) (Open): Adds Mattermost following the Slack pattern. Given PR #3199 was closed and this is a new open variant, Mattermost support is actively progressing and likely lands soon.

- **Remote HTTP/SSE MCP servers** — Merged in PR #2776: This foundational capability enables third-party MCP integrations (like Strava) and likely paves the way for more remote-MCP-based skills.

- **Persistent group-scoped OneCLI secret assignment** — [Issue #3205](https://github.com/nanocoai/nanoclaw/issues/3205) (Open): A multi-user secret governance model is explicitly discussed as unresolved. This could become a roadmap item for better credential isolation.

- **Telegram native rich rendering via Bot API 10.1 `sendRichMessage`** — [PR #2877](https://github.com/nanocoai/nanoclaw/pull/2877) (Open, follows-guidelines): Continues to be open and unmerged; if approved, it would significantly improve Telegram UX with rich native rendering.

---

## 7. User Feedback Summary

- **Approval flow reliability is a pain point:** Issue #3201 shows that even owner/admin roles cannot approve config updates via Discord when the bug manifests. The community reaction (fix PR from omerh) indicates this is a high-priority annoyance impacting day-to-day operations.

- **Users are pushing for more secure, granular secret management:** chiptoe-svg's issue #3205 highlights a genuine gap in multi-user environments, and the framing as a "design fork" suggests users are actively thinking about security architecture.

- **Media handling gaps persist:** Signal channel has had image/PDF attachment issues since May (Issue #2528, still open), and now Google Chat is affected by dropped attachments. These interconnected issues suggest the attachment pipeline is a recurring source of user frustration.

- **Documentation drift is confusing contributors:** Issue #3204 notes the add-opencode skill instructs edits that no longer match the codebase; this type of stale documentation increases friction for contributors and "skill" users alike.

---

## 8. Backlog Watch

- **[Issue #2528] Signal channel: image/PDF attachments unreachable from agent container** (by brentkearney, 0 comments, updated 2026-08-08) — [Link](https://github.com/nanocoai/nanoclaw/issues/2528) — Opened May 18, 2026, and still open after nearly 3 months. This is a long-standing user-facing bug that has received no comments. Attachments in Signal remain unreachable inside containers; this may deserve maintainer prioritization, especially given related attachment issues in Google Chat.

- **[PR #2877] Telegram native rich rendering via Bot API 10.1 `sendRichMessage`** (by robbyczgw-cla, updated 2026-08-08) — [Link](https://github.com/nanocoai/nanoclaw/pull/2877) — Open since June 28, 2026, with the `follows-guidelines` label. It has seen no comments and has not been merged, representing a substantial feature addition that may be awaiting maintainer review.

---

*Digest generated from GitHub activity data for 2026-08-09. All links point to the respective NanoClaw issue/PR pages.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Based on the GitHub data for IronClaw (github.com/nearai/ironclaw) for 2026-08-09, here is the project digest:

---

# IronClaw Project Digest — 2026-08-09

## 1. Today's Overview

IronClaw is in a period of very high development velocity and architectural consolidation. The project saw 30 issues and 50 PRs updated in the last 24 hours, with an unusually high closure rate: 24 of 30 issues (80%) and 32 of 50 PRs (64%) were closed or merged. The core focus remains the "Reborn" migration—a large-scale refactoring effort to modularize the legacy monolith into typed, domain-owned services. Concurrently, the team is heavily investing in robustness (outbound delivery race conditions, CI gate hardening) and surface-area expansion, with multiple large (XL-sized) PRs in flight for new features like Web Push notifications, progressive channel previews, and a Web Debug Inspector. While no new releases were tagged today, the sheer volume of merged work indicates a release is likely imminent.

## 2. Releases

**No new releases were published in the last 24 hours.**

## 3. Project Progress

The bulk of activity was focused on merging/handling a large backlog of "Reborn" migration and parity issues, alongside significant stability and feature work.

**Merged/Closed PRs (Key Highlights):**
- **[#7393] Merged** — test(disclosure): measure the Core delivery pair in the wide-catalog benchmark.
- **[#7389] Merged** — fix(live-qa): A critical fix for the `reborn-webui-v2-live-qa` lane, which had been failing every run due to relying on a retired completion-driver push record.
- **[#7382] Merged** — feat(stress): Added scripted tool-call workloads to the API stress scenario, addressing Issue #7360.
- **[#7377] Merged** — feat!: A major architectural shift where "a run acts as its invoker" (the user who invoked it), removing the shared-route subject binding. This PR also folded in the full review-hardening pass from a multi-agent audit.
- **[#7029] Merged** — fix(product): Restored durable delivery claim authority, making the CAS the sole gate for vendor egress.
- **[#6938] Merged** — fix(skills): A key UX/architecture win where the model now chooses which skill to activate, rather than the host using a keyword scorer.

**Closed Issues (Key Highlights):**
- A large batch of **Reborn migration issues** were closed, including: **#3280** (ProductWorkflow facade), **#3288** (Capability lifecycle parity), **#4118** (CLI provider parity), **#4059** (Runtime error enrichment), **#3577** (Legacy channel ports), **#3582** (WeChat channel port), **#3287** (Memory/workspace migration), **#3286** (Agent command behavior), and **#3285** (External channel adapters).
- The **#4539 Epic (Reborn approvals parity)** was closed.
- The **Web Debug Inspector** subtasks **#7226** and **#7225** were closed, indicating core implementation of the inspector is complete.

## 4. Community Hot Topics

There were no issues or PRs with an unusually high number of comments (all were under 10, with most at 0-1). The most discussed items were:

- **Issue #6989 (Open, 5 comments):** "Token accounting" — This is a P1 bug report detailing incorrect token estimation from content reference strings instead of the referenced content itself. The comments indicate active technical discussion on the fix. (https://github.com/nearai/ironclaw/issues/6989)
- **Issue #3280 (Closed, 7 comments):** The "ProductWorkflow and InboundTurnService" facade issue, which had sustained discussion during its lifecycle before being closed. (https://github.com/nearai/ironclaw/issues/3280)
- **Issue #6939 (Open, 2 comments):** "Migration tool to port legacy agent setup" — This user-feedback-driven feature request has drawn maintainer attention.

**Analysis:** The low comment counts suggest a highly efficient, bot-driven or fast-moving core team. The underlying needs surfacing are: 1) A critical need for accurate token accounting to manage costs correctly (Issue #6989), and 2) A clear demand from users for seamless migration paths from legacy tools (Issue #6939).

## 5. Bugs & Stability

**High Severity:**
- **Issue #6989 (P1):** Incorrect token estimation in `ModelWorkRequest::for_assistant`. It estimates input tokens by measuring the *length of the content reference string* rather than the content itself. This could lead to severe cost overruns and incorrect context window management. A fix is actively being discussed. (https://github.com/nearai/ironclaw/issues/6989)

**Medium Severity:**
- **PR #7395:** Fixes a TOCTOU (Time-of-check to time-of-use) race condition in `claim_delivery_attempt_for_send` that could lead to claim-loss misclassification. The fix also allows failed rows to be re-opened.
- **PR #7352:** Fixes a bug where multiple approval/auth gates on the same run could derive identical projection IDs, breaking durable delivery identity.
- **Issue #7391:** Reports that `SafetyLayer::validate_input` and `scan_inbound_for_secrets` have no caller on the live Reborn turn path, meaning the "Validate, Sanitize, Detect Leaks" stage described in security documentation is not actually enforced. This is a critical security gap. (https://github.com/nearai/ironclaw/issues/7391)

**Low Severity:**
- **PR #7341:** Restores scoped attachment reads and SSE tests in the WebUI, fixing a regression exposed by the SSE transport migration.

## 6. Feature Requests & Roadmap Signals

- **Web as a First-Class Notification Channel (PR #7398):** A large PR adding W3C Web Push (PWA) notifications to make the web app a first-party notification route, achieving parity with Slack/Telegram. This is a significant product expansion. (https://github.com/nearai/ironclaw/pull/7398)
- **Presence-based Shared Conversations (PR #7397):** A PR to enable shared conversations for Slack and Telegram, building on the invoker-identity ladder from #7377. This points toward multi-user collaboration features.
- **Generic Progressive Previews (PR #7396):** A channel-neutral progressive-preview contract, mapped to Slack's streaming APIs, suggesting an improved UX for long-running tasks.
- **Web Debug Inspector (Issue #7218):** An epic for an operator-only debug inspector for investigating prompts, activity, and model usage in the WebUI. Sub-tasks were closed, and a major PR (#7291) is open. This is a clear roadmap item for the next release.
- **Replace First-Party Coding Tools (Issue #7392):** An epic to replace IronClaw's model-visible coding tools with the exact contract from `oh-my-pi`. This is a major strategic shift in tooling. (https://github.com/nearai/ironclaw/issues/7392)

## 7. User Feedback Summary

- **High Switching Cost (Issue #6939):** The primary direct user feedback highlighted that users of the legacy product (Hermes/Openclaw) face high switching costs because there is no way to migrate their existing setup, configuration, and memory. Users are reluctant to start over with a clean slate, which could hinder adoption.
- **Reliability Concerns:** The large number of fixes targeting delivery claims, race conditions, and failed CI lanes indicates a user base that demands high reliability in production automations. The team is actively responding to this.

## 8. Backlog Watch

No issues or PRs appear to be critically abandoned, given the high-velocity closure rates. However, the following open items warrant attention for prioritization:

- **Issue #7391 (Security Gap):** The un-called safety layer functions (`validate_input`, `scan_inbound_for_secrets`) represent a critical security documentation-vs-reality mismatch. This should be prioritized above feature work. (https://github.com/nearai/ironclaw/issues/7391)
- **Epic #7218 (Web Debug Inspector):** While core pieces are closed, the main epic and a large PR (#7291) are still open. This is a large, multi-faceted feature with significant operator value. (https://github.com/nearai/ironclaw/issues/7218)
- **Epic #7392 (Tool Surface Replacement):** This new epic has high strategic importance as it defines a new standard for model-visible coding tools. Its progress should be closely watched. (https://github.com/nearai/ironclaw/issues/7392)

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the **LobsterAI Project Digest** for **2026-08-09**.

---

## 1. Today's Overview
LobsterAI is currently in a **low-activity maintenance phase**. Over the last 24 hours, only one Issue and three PRs received updates, with no new releases published. Notably, all four updated items are marked as **[stale]** , indicating that maintainer bandwidth is currently focused on triage rather than rapid feature development. The most significant piece of work in the pipeline is a performance optimization for the SQLite storage layer (PR #1193), which addresses a critical architectural flaw. While community engagement is light, the project remains healthy with open PRs pending review, though the growing stale label on several items suggests a need for maintainer attention to clear the queue.

## 2. Releases
**None.**
No new versions of LobsterAI were published in the last 24 hours, and there are no release candidates or changelogs to report.

## 3. Project Progress
**Merged/Closed PRs (1):**
- **PR #2193 [CLOSED]**: **feat: add LiteLLM as AI gateway provider**. This PR adds support for LiteLLM, allowing users to connect to 100+ LLM providers through a single OpenAI-compatible endpoint. It reuses the existing `chatWithOpenAICompatible` handler, meaning no new dependencies were introduced. The prompt of the feature is to avoid vendor lock-in and give users greater flexibility in choosing their AI backend. The closure status suggests the feature was either merged or superseded, marking a step forward in provider extensibility.

## 4. Community Hot Topics
- **Issue #1192 — Custom Default Configurations (1 comment)**: This Issue remains the most interactive discussion, though activity is sparse. The user is frustrated with the inconsistency of LLM instruction-following (specifically regarding headless browser mode) and requests a hard-coded configuration override feature. This taps into a broader user need: **desiring deterministic control over agent behavior** rather than relying on probabilistic model adherence.
- **PR #1193 — SQLite Write Amplification Fix (0 comments)**: While lacking comments, this PR is the most technically significant open item. It addresses a severe performance bug where every single row mutation triggers a full database export and file write, which is a blocking scalability issue for users with large memory stores.

## 5. Bugs & Stability
- **[High Severity] PR #1193 (Open) — Write Amplification in SQLite Storage**: This is the primary stability concern. The current implementation (`sql.js`) loads the entire database into memory and performs a full `db.export()` + `fs.writeFileSync()` on every mutation. This leads to severe performance degradation and potential data corruption risks during high-frequency writes or crashes mid-write. The proposed fix introduces debouncing and batch transactions. **Status**: Fix PR exists and is open, but needs review and merge.
- **[Medium Severity] Issue #1192 (Open) — Unreliable Tool Configuration**: While not a crash, the user reports that the agent frequently fails to respect memory-based instructions (e.g., launching a browser in headless mode), leading to a disruptive UX. This is a behavioral bug rooted in LLM non-determinism rather than code logic.

## 6. Feature Requests & Roadmap Signals
- **Hardcoded Tool Defaults (Issue #1192)**: There is a clear signal that users want **"user-intent override"** capabilities separate from LLM behavior. This suggests a roadmap item where tool parameters can have immutable defaults set by the user (e.g., `"browser_headless": true`), which the agent cannot change based on context.
- **AI Gateway Flexibility (PR #2193)**: The closure of the LiteLLM PR signals a roadmap trend toward **provider-agnostic architecture**. Future iterations may focus on integrating with more enterprise-grade proxies or local model gateways, ensuring the core works regardless of the upstream AI service.

## 7. User Feedback Summary
- **Pain Point**: Users are experiencing **"AI Anarchy"** — where the LLM agent ignores persistent instructions, leading to unwanted behavior (like popping up GUI windows). They do not trust the model to follow memory reliably and are seeking explicit "hard constraints" in the config.
- **Satisfaction**: The addition of LiteLLM (PR #2193) is likely to be welcomed by users looking to manage multiple providers, indicating a high demand for **"bring-your-own-key"** flexibility.
- **Use Case**: The primary frustration revolves around headless/cron-based automation, where users expect the agent to run silently in the background. The current failure to do so is a major impediment to using LobsterAI as a server-side automator.

## 8. Backlog Watch
- **Issue #1192 (Created: 2026-04-01)** : **Needs Maintainer Response**. This open feature request has been a topic for over four months and specifically challenges the core design philosophy. A official response acknowledging the limitation or outlining a workaround is critical to prevent user churn.
- **PR #1193 (Created: 2026-04-01)** : **Critical Performance Fix Stalled**. This PR has been open for over four months with zero comments. Given the severity of the database write issue, the lack of review is the single biggest blocker to project scalability. Maintainers should prioritize reviewing and testing this patch.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

Here is the Moltis project digest for 2026-08-09.

---

# Moltis Project Digest — 2026-08-09

## 1. Today's Overview
Moltis shows **steady maintenance activity** this week, with two issues and one pull request updated in the last 24 hours. The project is in a **consolidation phase**, focusing on stabilizing the Docker sandbox environment rather than shipping new features. The critical long-standing bug regarding `Read`/`Write`/`Edit` tools in Docker (Issue #1096) has been **closed via a directly linked fix PR (#1105)**, marking a significant resolution for container-based users. One new bug was reported regarding Apple Container 1.x sandbox detection, indicating that sandbox compatibility remains the primary friction point for the user base. There were no new releases this period.

## 2. Releases
No new releases were published in the last 24 hours. The most recent tagged version remains the current stable, with fixes likely to be batched into the next minor version.

## 3. Project Progress
- **PR #1105 (Merged/Closed): Fix Docker sandbox filesystem tool fallback** — Authored by *penso*, this PR resolves the long-standing incompatibility of sandboxed file operations in Docker environments. The fix adds regression coverage for `Read`/`Write`/`Edit`/`MultiEdit` on `/home/sandbox` and `workspace/data` paths. It implements a fallback mechanism from translated Docker host paths to direct container operations when the gateway process cannot access the host mount, while preserving existing missing-list semantics. This advances the project’s core goal of making Moltis operate seamlessly across diverse execution environments.

## 4. Community Hot Topics
- **Issue #1096 (Closed): `Read`/`Write`/`Edit` tools don't work in Docker** — This issue, open since June, was the most significant community pain point. It highlighted that the core file-editing toolchain failed for users running Moltis inside Docker containers—a common deployment pattern for AI agents. The underlying need was for **environment-agnostic filesystem operations**, regardless of host/container boundary complexities. The closure of this issue via PR #1105 is a major win for adoption in containerized workflows.
- **Issue #1185 (Open): Apple Container 1.x sandbox starts but Moltis treats it as not running** — This new report from user *mikz* indicates that while the underlying Apple container sandbox initializes successfully, Moltis’s health-check/probe logic fails to recognize its running state. This suggests a potential **state-tracking or process-detection race condition** in the sandbox lifecycle manager, specifically for Apple's 1.x container runtime.

## 5. Bugs & Stability
- **[Medium] Issue #1185 (Open): Apple Container 1.x sandbox state mismatch** — Critical for macOS users with Apple Container setups. The sandbox starts OS-level, but Moltis errors out, blocking the agent’s use. No fix PR exists yet; the core team needs to investigate the process detection logic specific to Apple Container 1.x.
- **[High — Resolved] Issue #1096 (Closed): Docker filesystem tools broken** — While now fixed, this was the highest-severity regression for Docker users. The fix in #1105 has been merged, but **community verification is recommended** to confirm the fallback works across various Docker Desktop and daemon versions.

## 6. Feature Requests & Roadmap Signals
No explicit new feature requests were filed in this window. However, the focus on sandbox filesystem fallbacks suggests the roadmap is prioritizing **infrastructure robustness over new surface area**. The resolution of the Docker issue implies the next development cycle may shift toward either **polishing Apple Container 1.x support** (given Issue #1185) or adding **new sandbox providers** with more resilient lifecycle detection. Expect the next minor release to include the merged Docker fixes and, potentially, a hotfix for the Apple Container detection issue if it gains traction.

## 7. User Feedback Summary
- **Pain Point (Docker):** Users experienced a blocker where the core toolchain (Read/Write/Edit) was non-functional, rendering the agent largely useless for file manipulation tasks. This was a direct violation of the "works out of the box" expectation.
- **Pain Point (Apple):** Users are reporting a **misleading error state** where the infrastructure is running, but Moltis loses sync with it. This indicates a transparency issue; the UI/agent logic fails to reflect the true system state.
- **Overall Sentiment:** Neutral-to-positive. The community saw a response to a major issue (Docker), but the rapid emergence of a new sandbox-specific issue suggests that **sandbox compatibility is the number one source of user dissatisfaction** heading into the next release cycle.

## 8. Backlog Watch
- **Issue #1185 (Created 2026-08-08):** This is a **new issue requiring immediate triage**. The author has completed the preflight checklist and is on the latest version. Since it concerns the Apple Container 1.x runtime, it likely requires maintainer expertise to reproduce, as it may be environment-specific.
- **Issue #1096 (Resolution Tracking):** Although the issue is closed, our digest flags it for **post-fix monitoring**. Comments on the PR indicate the need for verification across different Docker storage drivers (e.g., `overlay2` vs. `virtiofs`) to ensure the host-mount fallback doesn't introduce a performance penalty. A follow-up report would be prudent if the fix proves incomplete for exotic setups.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest - 2026-08-09

## 1. Today's Overview

CoPaw shows a notably high level of activity, with 18 issues and 50 pull requests updated in the last 24 hours. Issue volume is spread across bug reports (12), feature requests (3), and other categories, indicating substantial community engagement. There are no new releases this period; however, the high PR throughput (47 open, 3 merged/closed) suggests active development toward the next release, likely a 2.1.0 stable or 2.1.1 patch. The main focus areas include MCP reliability, performance/CPU issues on the frontend, provider compatibility (OpenAI, Gemini), and desktop (Tauri) specific problems. The project is healthy with rapid response to issues, demonstrated by numerous linked fix PRs created just days after the reports.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains **v2.1.0b2** (beta), with the latest stable being **v2.0.1** and **v2.1.0b1**. The following bugs related to these versions are actively being addressed by PRs, suggesting a fix release is likely imminent.

## 3. Project Progress

Three PRs were merged or closed during this period. All three are related to bug fixes, indicating a focus on stabilization.

- **PR #6835** ([link](https://github.com/agentscope-ai/QwenPaw/pull/6835)) - **Fixed**: "KeyError: '__aiter__'" during auto-title generation by adding a check for the offending attribute before parsing, resolving [issue #6813](https://github.com/agentscope-ai/QwenPaw/issues/6813).
- **PR #6836** ([link](https://github.com/agentscope-ai/QwenPaw/pull/6836)) - **Fixed**: MCP client sessions now correctly pass the configured `read_timeout_seconds`, a direct fix for [issue #6822](https://github.com/agentscope-ai/QwenPaw/issues/6822).
- **PR #6778** ([link](https://github.com/agentscope-ai/QwenPaw/pull/6778)) - **Closed**: A blog post regarding agent memory upgrade practices was closed and re-submitted as a new PR ([#6837](https://github.com/agentscope-ai/QwenPaw/pull/6837)) to follow the correct documentation path.

## 4. Community Hot Topics

- **Docker "Under Maintenance" Issue** - [Issue #6782](https://github.com/agentscope-ai/QwenPaw/issues/6782) is a critical, actively discussed bug (9 comments) from users of the `2.0.1` Docker version, who can't access the plugin or app marketplaces. This is a major usability blocker for the Docker distribution and likely a top priority for the team.
- **High CPU Usage at Idle** - [Issue #6828](https://github.com/agentscope-ai/QwenPaw/issues/6828) describes a ~20% CPU usage problem at idle caused by infinite CSS animations. This issue is related to the older [Issue #4558](https://github.com/agentscope-ai/QwenPaw/issues/4558), which highlighted high CPU usage during long outputs. Both point to significant frontend performance concerns, now with a fix in [PR #6834](https://github.com/agentscope-ai/QwenPaw/pull/6834).
- **OpenAI Provider Issues** - Two issues, #6811 and #6821, relate to problems with the OpenAI and thinking-mode providers, specifically around `disable_thinking` and `reasoning_content` handling. These are generating discussion and are critical for user workflows relying on these models.

## 5. Bugs & Stability

Today's bug reports focus on critical issues in the 2.1.0 beta and 2.0.1 versions, particularly in MCP, provider compatibility, and the desktop UI.

- **Critical**:
    - **Blocked Conversations after MCP Failure** - [Issue #6822](https://github.com/agentscope-ai/QwenPaw/issues/6822): A transient MCP connection failure can permanently block the active conversation. *Fix PRs exist*: [#6825](https://github.com/agentscope-ai/QwenPaw/pull/6825) and [#6836](https://github.com/agentscope-ai/QwenPaw/pull/6836).
    - **SIGBUS Crash on macOS** - [Issue #6814](https://github.com/agentscope-ai/QwenPaw/issues/6814): Opening Scroll history.db on macOS can crash the application. No fix PR is present.
    - **Installer File Lock Bugs** - [Issue #6810](https://github.com/agentscope-ai/QwenPaw/issues/6810): The Windows installer fails when files are locked by other processes (e.g., browser extensions), leading to multiple errors and install failures.
- **High**:
    - **Broken Google Gemini Provider** - [Issue #6812](https://github.com/agentscope-ai/QwenPaw/issues/6812): API calls fail due to unsupported `$schema` fields in tool schemas.
    - **Frontend Not Displaying Streamed Output** - [Issue #6820](https://github.com/agentscope-ai/QwenPaw/issues/6820): The UI doesn't show streaming outputs until the entire process is complete.
    - **Thinking-Mode Relay Errors** - [Issue #6821](https://github.com/agentscope-ai/QwenPaw/issues/6821): A 400 error is returned for thinking-mode models, possibly related to #6811.
    - **MCP `read_timeout_seconds` Not Applied** - [Issue #6822](https://github.com/agentscope-ai/QwenPaw/issues/6822) exposes this root cause, now fixed by [#6836](https://github.com/agentscope-ai/QwenPaw/pull/6836).
- **Medium**:
    - **High CPU Usage at Idle on Desktop** - [Issue #6828](https://github.com/agentscope-ai/QwenPaw/issues/6828): Caused by CSS animations. *Fix PR exists*: [#6834](https://github.com/agentscope-ai/QwenPaw/pull/6834).
    - **Homebrew ffmpeg Not Found** - [Issue #6831](https://github.com/agentscope-ai/QwenPaw/issues/6831): Local Whisper fails on macOS because the backend PATH excludes `/opt/homebrew/bin`.
    - **Incorrect Elapsed Time Display** - [Issue #6826](https://github.com/agentscope-ai/QwenPaw/issues/6826): Assistant message end times are incorrect in the UI.
- **Low**:
    - **Silent Approval Requirement** - [Issue #6819](https://github.com/agentscope-ai/QwenPaw/issues/6819): The Channel tool doesn't signal when an approval is required. *Fix PR exists*: [#6833](https://github.com/agentscope-ai/QwenPaw/pull/6833).

## 6. Feature Requests & Roadmap Signals

- **Provider Support**: [Issue #6490](https://github.com/agentscope-ai/QwenPaw/issues/6490) requests adding Volcengine Agent Plan and Xiaomi MiMo Standard API as built-in providers. This is part of a trend (see NVIDIA NIM PR #6526) to expand provider options, suggesting CoPaw is actively diversifying its third-party integrations.
- **Approval Transparency**: [Issue #6832](https://github.com/agentscope-ai/QwenPaw/issues/6832) is a strong signal toward improving AI decision transparency. It requests a natural-language description in approval prompts, aligning with best practices for explainable AI/agents. This is likely to be implemented soon.
- **Cleanup on Chat Deletion**: [Issue #6827](https://github.com/agentscope-ai/QwenPaw/issues/6827) requests an option to clean temporary files generated during a chat session when the chat is deleted. This is seen as a valuable quality-of-life improvement, likely influenced by the "26GB orphan file" bug ([PR #6799](https://github.com/agentscope-ai/QwenPaw/pull/6799)).
- **Other Signals**: PRs for an **SSE run-outcome** feature ([#5930](https://github.com/agentscope-ai/QwenPaw/pull/5930)), **Responses prompt caching** ([#6668](https://github.com/agentscope-ai/QwenPaw/pull/6668)), and **AnySearch web search** ([#6817](https://github.com/agentscope-ai/QwenPaw/pull/6817)) are being discussed and could be targets for the next minor release, indicating a strong interest in improving API automation and performance.

## 7. User Feedback Summary

- **Stability is a Primary Concern**: Beta users in the v2.1.0 cycle are reporting critical stability issues, especially on macOS (SIGBUS crashes, MCP failures) and Windows (installer issues). The progress on fix PRs is positive, but the number of critical bugs suggests the stable release should focus heavily on regression testing.
- **UI/UX Performance Issues**: There are several complaints about the frontend's performance, including high CPU usage at idle and delayed display of streamed output. Performance is a key driver of satisfaction, and these issues seem to be a real pain point.
- **Provider Compatibility**: Users are frustrated by issues with non-Qwen providers like Google Gemini and OpenAI (thinking-mode). The project's goal of being a universal agent makes provider reliability a top priority.
- **User-Visible Fixes Welcome**: The fix for the auto-title generation bug ([Issue #6813](https://github.com/agentscope-ai/QwenPaw/issues/6813)) directly addresses a user-facing feature, which is a positive sign.

## 8. Backlog Watch

- **PR #6615** ([link](https://github.com/agentscope-ai/QwenPaw/pull/6615)): This PR, "fix(config): handle corrupted agent config and invalid JSON," is more than a week old and under review. It addresses a critical startup crash, which is also relevant to the long-standing issue of agent.json corruption ([#6520](https://github.com/agentscope-ai/QwenPaw/issues/6520)).
- **Issue #4558** ([link](https://github.com/agentscope-ai/QwenPaw/issues/4558)): The long-standing issue about high CPU during long text output is seeing renewed relevance with new related reports (#6828). The fix for the new issue is in review, but this older one may need re-evaluation.
- **PR #6103** ([link](https://github.com/agentscope-ai/QwenPaw/pull/6103)): The CI coverage improvement PR has been open for some time. While not user-facing, it's crucial for long-term stability and regression prevention and might be getting pushed aside by more urgent fixes.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-09

## 1. Today's Overview

ZeroClaw shows **high sustained activity** with 50 issues and 50 PRs updated in the last 24 hours. The project is undergoing a significant **architecture consolidation phase**: multiple RFCs propose retiring standalone crates (`aardvark-sys`, `zeroclaw-robot-kit`) into `zeroclaw-hardware`, and a large PR (#9853) implementing both removals is already open. **Security remains the dominant theme** — numerous high-severity issues (S1 classified) around forbidden path bypasses, channel authorization gaps, and leak-detector false positives are actively being triaged and worked. The maintainer team is responsive, with issues receiving comments within days and several in-progress fixes. However, **48 of 50 issues remain open**, indicating a substantial backlog, with PRs like #9841 (SOP headless runs) and #9494 (superseded by #9841) showing active iteration on complex runtime features.

## 2. Releases

**No new releases in the last 24 hours.** The most recent release remains v0.8.4 (referenced in PR #9787 regarding an AUR publish issue).

## 3. Project Progress

Two items were closed/merged in the last 24 hours:

- **[#9843 [CLOSED] `bug(zerocode)`: long-lived client CPU spin alongside daemon](https://github.com/zeroclaw-labs/zeroclaw/issues/9843)** — Reported and closed on 2026-08-08; marked `r:needs-repro`, suggesting it may have been closed as unreproducible or with insufficient information.
- **[#9798 [CLOSED] `docs(sop)`: document which agent executes SOP steps](https://github.com/zeroclaw-labs/zeroclaw/pull/9798)** — Superseded by #9841, which carries the runtime fix for headless SOP execution.

**Active high-signal PRs:**

- **[#9841 (OPEN) `fix(sop)`: drive headless SOP runs and close five defects from #9494 review](https://github.com/zeroclaw-labs/zeroclaw/pull/9841)** — Canonical continuation of #9494 (which was closed as superseded). This is the main line of work fixing the critical "SOP auto-mode never executes from channel/cron triggers" bug (#9805).
- **[#9853 (OPEN) `chore(workspace)`: remove aardvark-sys and zeroclaw-robot-kit](https://github.com/zeroclaw-labs/zeroclaw/pull/9853)** — Implements the retirement of both standalone crates, clearing the path for crates.io publishing (#9381).
- **[#9854 (OPEN) `fix(providers)`: context-window discovery from family registry](https://github.com/zeroclaw-labs/zeroclaw/pull/9854)** — Replaces a brittle hand-written provider name match with registry-driven discovery.

## 4. Community Hot Topics

The most active discussions reveal **security-critical design tensions**:

- **[#8043 (11 comments, CLOSED) RFC: Retire aardvark-sys into zeroclaw-hardware](https://github.com/zeroclaw-labs/zeroclaw/issues/8043)** — Closed after ratification; its implementation is in #9853. Shows an efficient RFC-to-implementation pipeline.
- **[#8424 (11 comments, OPEN) RFC: Workspace-relative forbidden paths + .zeroclawignore](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)** — Directly addresses the [#9815 bug](https://github.com/zeroclaw-labs/zeroclaw/issues/9815) where `forbidden_paths` is unreachable for workspace paths. This RFC is the design answer to a critical security gap.
- **[#8054 (10 comments, OPEN) System prompt tool-availability mismatch across all entry points](https://github.com/zeroclaw-labs/zeroclaw/issues/8054)** — A cross-cutting correctness bug affecting channels, gateway, WebSocket, and multimodal paths. High visibility because it undermines model behavior consistency.
- **[#9348 (9 comments, OPEN) WhatsApp Web answers every DM/group under business mode](https://github.com/zeroclaw-labs/zeroclaw/issues/9348)** — **S1 security severity**. An allowlist (`allowed_groups` empty) is treated as "allow all," so a "locked down" config behaves fully open. This is the kind of bug that erodes operator trust.

**Underlying need:** The community is pushing ZeroClaw toward **defense-in-depth defaults** — "secure by default" configuration semantics, explicit permission models, and clear, auditable path/firewall rules. The number of `security:leak-detector` and `security:policy` issues suggests security auditing is a recurring community activity.

## 5. Bugs & Stability

**Severity S1 (security / workflow blocked):**

- **[#9348 (OPEN) WhatsApp Web answers every DM and group](https://github.com/zeroclaw-labs/zeroclaw/issues/9348)** — Config semantics invert allowlist intent. No fix PR yet.
- **[#8559 (OPEN) Agents stop when exiting web dashboard chat](https://github.com/zeroclaw-labs/zeroclaw/issues/8559)** — Workflow-blocking; a user-initiated exit kills agent work mid-task.
- **[#9035 (OPEN) Docker Compose gateway loopback-bound behind published port](https://github.com/zeroclaw-labs/zeroclaw/issues/9035)** — "Connection refused" despite proper port bridging.
- **[#9390 (OPEN) Emergency stop is CLI-only state file; no runtime path reads it](https://github.com/zeroclaw-labs/zeroclaw/issues/9390)** — A documented safety guarantee that is not implemented in the runtime.
- **[#9387 (OPEN) Interactive approvals accepted from any chat member](https://github.com/zeroclaw-labs/zeroclaw/issues/9387)** — Telegram, Slack, Lark, Matrix all affected.

**Severity S2 (degraded behavior):**

- **[#8731 (OPEN) Stdio MCP servers accumulating as zombies](https://github.com/zeroclaw-labs/zeroclaw/issues/8731)** — Long-running daemons leak sub-processes.
- **[#8410 (OPEN) Channel tasks lack intentional no-reply outcome](https://github.com/zeroclaw-labs/zeroclaw/issues/8410)** — Contradicts conditional-task expectations.
- **[#9843 (CLOSED) Zerocode CPU spin alongside daemon](https://github.com/zeroclaw-labs/zeroclaw/issues/9843)** — Closed, `r:needs-repro`.

**Fix PRs in flight:**

- [#9841](https://github.com/zeroclaw-labs/zeroclaw/pull/9841) addresses **#9805** (SOP auto-mode never executes) — the most critical runtime bug in the queue.
- [#9744](https://github.com/zeroclaw-labs/zeroclaw/pull/9744) (authenticated webhook ingress) addresses a whole class of unauthenticated dispatch risks.
- [#9410](https://github.com/zeroclaw-labs/zeroclaw/pull/9410) defaults command audit logging to disabled (security-honesty direction).

**Intermittent test failures:** [#9834 (OPEN, accepted)](https://github.com/zeroclaw-labs/zeroclaw/issues/9834) reports CI flakiness from shared process-global state in `zeroclaw-runtime` tests — a maintenance hazard that erodes CI signal.

## 6. Feature Requests & Roadmap Signals

**Strong roadmap signals (likely in next release):**

- **OpenAI-compatible chat completions endpoint** ([#8550](https://github.com/zeroclaw-labs/zeroclaw/issues/8550)) — Unlocks Open WebUI, LobeChat, and custom integrations. High community value; the gateway has the infrastructure to support it.
- **Workspace-relative forbidden paths + `.zeroclawignore`** ([#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)) — Directly fixes a security gap; the RFC is mature with 11 comments.
- **Web-tool surface simplification** ([#9824](https://github.com/zeroclaw-labs/zeroclaw/issues/9824)) — Reduce five overlapping tools to three distinct verbs (`web_fetch`, `web_research`, `http_request`). Aligns with the architecture consolidation trend.
- **Agent-facing config authoring** ([#9828 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/9828)) — Replaces raw `echo > config.toml` with validated, operator-approved config editing. Six-commit PR with operator-approved policy previews.
- **Telegram multi-message mode** ([#8445](https://github.com/zeroclaw-labs/zeroclaw/issues/8445)) — One message per agent turn instead of concatenated blobs.

**Deferred / long-running:**

- **MCP embedded resource blob intake** ([#9179](https://github.com/zeroclaw-labs/zeroclaw/issues/9179)) — Materialize binary blobs to workspace and strip base64 from model output. Still open since 2026-07-19.
- **Zerocode multi-session panes** ([#9739 PR](https://github.com/zeroclaw-labs/zeroclaw/pull/9739)) — Stacked PR; large feature (size:XL).

## 7. User Feedback Summary

**Pain points (recurring themes):**

- **Security configuration is unintuitive and can invert.** The WhatsApp bug ([#9348](https://github.com/zeroclaw-labs/zeroclaw/issues/9348)) and the leak-detector redaction of Solana addresses ([#9486](https://github.com/zeroclaw-labs/zeroclaw/issues/9486), [#9825](https://github.com/zeroclaw-labs/zeroclaw/issues/9825)) both frustrate users who believe they configured safe behavior but get either excessive openness or excessive redaction.
- **Workflow interruption is unacceptable.** [#8559](https://github.com/zeroclaw-labs/zeroclaw/issues/8559) (agents killed on window exit) and [#8410](https://github.com/zeroclaw-labs/zeroclaw/issues/8410) (no intentional no-reply) show users want agents to be **durable and autonomous**, not tied to a UI session.
- **Output hygiene matters.** Cron jobs discarding output silently ([#9340](https://github.com/zeroclaw-labs/zeroclaw/issues/9340)) and typing indicators that misrepresent blocked turns ([#9656](https://github.com/zeroclaw-labs/zeroclaw/issues/9656)) are quality-of-life degradations that affect trust.
- **Cost transparency is broken.** Anthropic provider reports $0.00 spend ([#9816](https://github.com/zeroclaw-labs/zeroclaw/issues/9816)) meaning **budget caps never fire** — an operational hazard for paid users.
- **Positive signal:** The community is actively contributing (PRs from JordanTheJet, IftekharUddin, Lusitaniae, egorchenkov, eugeneb50). The RFC process, while slow ([#9496](https://github.com/zeroclaw-labs/zeroclaw/issues/9496) proposes streamlining it), is producing ratified decisions that turn into PRs within days.

## 8. Backlog Watch

**Long-unanswered / needs-maintainer-attention:**

- **[#7099 (since 2026-06-02, 2 comments) Route `zeroclaw status` through CLI i18n](https://github.com/zeroclaw-labs/zeroclaw/issues/7099)** — Accepted maintainer direction (PR #5987 added bare println strings), but no PR or assignment after 2 months. Low-risk cleanup that improves i18n consistency.
- **[#5514 (since 2026-04-08, 6 comments) Batch Telegram media groups into one multimodal turn](https://github.com/zeroclaw-labs/zeroclaw/issues/5514)** — Oldest open issue in the top-30; S3 severity (minor), but a real UX gap for Telegram power users.
- **[#6663 (since 2026-05-14, 2 comments) Show tool-call progress during partial streaming (Telegram)](https://github.com/zeroclaw-labs/zeroclaw/issues/6663)** — Feature request sitting in-progress for 3 months without visible PR.
- **[#9772 (OPEN PR, since 2026-08-05) Telegram per_user_session toggle for shared group-chat sessions](https://github.com/zeroclaw-labs/zeroclaw/pull/9772)** — Marked `needs-author-action` but no maintainer review comment visible; risks stalling.

**Infrastructure risk:**

- **[#9785](https://github.com/zeroclaw-labs/zeroclaw/pull/9785) and [#9787](https://github.com/zeroclaw-labs/zeroclaw/pull/9787) (CI: Scoop/AUR publish hardening)** — Both marked `needs-author-action`. These prevent release-pipeline outages (v0.8.4 was lost to an upstream maintenance window). They protect the project's distribution channel.

**Overall assessment:** ZeroClaw is a **security-conscious, rapidly iterating project** with a healthy contributor community and clear architectural direction. The main risks are (1) the high open-issue count (48/50) suggesting capacity constraints, and (2) the recurring class of "security control does the opposite of what the name implies" bugs, which point to a need for **semantic-review of configuration defaults** across the codebase.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*