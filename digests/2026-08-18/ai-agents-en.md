# OpenClaw Ecosystem Digest 2026-08-18

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-18 00:29 UTC

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

# OpenClaw Project Digest — 2026-08-18

## 1. Today's Overview

OpenClaw remains in a high-activity maintenance phase with a consistently large issue and PR load. Over the past 24 hours, 500 issues and 500 PRs were updated, reflecting both a substantial open backlog (484 open issues, 382 open PRs) and steady throughput (16 closed issues, 118 merged/closed PRs). No new releases were published today. The majority of the most active discussions require maintainer review or product decisions, indicating a significant maintainer bottleneck and an accumulation of complex, cross-cutting reliability concerns rather than a surge of new bug reports. A flurry of new, small-to-medium PRs from frequent contributors (steipete, jesse-merhi, jjjhenriksen) and several "AI-assisted" PRs indicate active development and a modern CI/CD loop. Project health is stable but strained by a large volume of unresolved, high-severity (P0/P1) reliability issues that have been open for weeks to months.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent release referenced in the data is from 2026-08-13. Users on the latest stable release are cautioned to remain up-to-date, as numerous regressions and bug fixes are pending review and merge.

---

## 3. Project Progress

A significant number of pull requests (118) were merged or closed in the last day, indicating active development and rapid iteration. Key areas of advancement from recently updated PRs include:

- **CLI & Gateway Fixes**: PRs like [#125474](https://github.com/openclaw/openclaw/pull/125474) add missing `--port` options to automation commands, improving usability for users on non-default ports.
- **UI & UX Improvements**: The Control UI is a major focus, with PRs such as [#125472](https://github.com/openclaw/openclaw/pull/125472) rebuilding the agent GitHub identity panel to match the design language, and [#123356](https://github.com/openclaw/openclaw/pull/123356) adding slash command argument staging to the composer. [#124429](https://github.com/openclaw/openclaw/pull/124429) fixes the misleading display of inherited skill allowlists.
- **Security & Reliability**: The security boundary is being reinforced. [#124714](https://github.com/openclaw/openclaw/pull/124714) was closed, preventing provider environment variable leakage in error messages. A closed PR [#116489](https://github.com/openclaw/openclaw/pull/116489) established the requirement for acknowledging install policy warnings, a feature expanded upon in a closed follow-up [#120900](https://github.com/openclaw/openclaw/pull/120900). Long-standing issues are being addressed with fixes for process leaks and truthful reporting of exec timeouts ([#125466](https://github.com/openclaw/openclaw/pull/125466)) and zombie process accumulation ([#97616](https://github.com/openclaw/openclaw/issues/97616)).
- **Stability & Performance**: Several PRs target resource consumption and system stability, including [#123535](https://github.com/openclaw/openclaw/pull/123535) which prevents UI session catalog refresh storms, and [#123979](https://github.com/openclaw/openclaw/pull/123979) which fixes the build process ignoring systemd memory limits.
- **AI-Assisted Development**: A notable trend is the increasing number of "AI-assisted" PRs (e.g., [#124962](https://github.com/openclaw/openclaw/pull/124962) from an autonomous Claude Code agent, [#125469](https://github.com/openclaw/openclaw/pull/125469), [#125468](https://github.com/openclaw/openclaw/pull/125468)), showcasing the project's dogfooding and the wider ecosystem trend.

---

## 4. Community Hot Topics

The most active discussions highlight long-running, high-impact reliability and stability concerns.

- **[Issue #77598: Track live dev agent behavior and trajectory](https://github.com/openclaw/openclaw/issues/77598)** (23 comments): This is a running observational log of a maintainer's dev agent, effectively a community science experiment on agent behavior. It signals the community's deep interest in the practical, real-world operation and debugging of agents.
- **[Issue #91009: Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)** (20 comments, 👍 2): A reproducible high-impact issue where Codex hooks cause massive CPU consumption and stall the gateway. This affects users on the integrated Codex path.
- **[Issue #68596: Configurable streaming watchdog timeout](https://github.com/openclaw/openclaw/issues/68596)** (15 comments, 👍 8): This has broad support, indicating widespread pain with models that have extended reasoning times. Users want to adjust timeouts to avoid false failures with thinking models like DeepSeek-R1.
- **[Issue #62505: Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)** (15 comments, 👍 1): A regression ticket from April affecting core functionality for coding agents. The high comment count indicates the severity and the difficulty maintainers are having in diagnosing it.
- **[Issue #38327: "Cannot convert undefined or null to object" with google-vertex](https://github.com/openclaw/openclaw/issues/38327)** (14 comments, 👍 3): A P1 regression affecting a major cloud provider integration, causing embedded agents to fail. Users are eager for a fix.

Underlying Needs: The community is deeply reliant on OpenClaw for stable, long-running automation. The hottest topics are not new features but critical reliability: preventing crashes, stopping resource leaks, and ensuring message delivery. There is also strong demand for configurability to match diverse model behaviors.

---

## 5. Bugs & Stability

Today's activity reveals a significant focus on regressions and system stability, with a large backlog of unresolved critical issues.

**Critical (P0):**
- **[#70903: Persistent file-based provider cooldown blocks user for hours after billing recovery](https://github.com/openclaw/openclaw/issues/70903)**: A P0 UX blocker where users are locked out even after fixing billing issues. This has been open since April and requires product and maintainer review.

**High Severity (P1):**
- **[#91009: Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)**: A critical performance issue causing CPU exhaustion and RPC stalls.
- **[#62505: Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)**: Core functionality regression, unresolved for months. No fix PR is linked.
- **[#38327: Crash with google-vertex/gemini-3.1-pro-preview](https://github.com/openclaw/openclaw/issues/38327)**: A documented regression, has been open since March.
- **[#97616: Leaks unreaped hook/tool child processes](https://github.com/openclaw/openclaw/issues/97616)**: A regression causing zombie process accumulation and runtime degradation. Updated today, but has no linked fix PR.
- **[#78493: `sudo openclaw update` can create mixed ownership](https://github.com/openclaw/openclaw/issues/78493)**: A dangerous issue causing config corruption on macOS.
- **[#71689: Tasks registry restore fails on malformed SQLite image](https://github.com/openclaw/openclaw/issues/71689)**: Data loss risk due to SQLite corruption on startup.

**Medium/High (P1/P2) Regressions & Reliability Issues:**
- **Message Loss & Session State**: Numerous issues (e.g., [#67777](https://github.com/openclaw/openclaw/issues/67777), [#74586](https://github.com/openclaw/openclaw/issues/74586), [#39476](https://github.com/openclaw/openclaw/issues/39476), [#50093](https://github.com/openclaw/openclaw/issues/50093)) revolve around the core reliability of messaging, such as lost subagent completions, aborted memory tool calls, and duplicate messages in A2A interactions.
- **Crash Loops & Gateway Instability**: Issues like [#45224](https://github.com/openclaw/openclaw/issues/45224) (Playwright crash) and [#72015](https://github.com/openclaw/openclaw/issues/72015) (active-memory overloading gateway) can lead to full process exits and service disruption.
- **Tool Call Failures**: [#53408](https://github.com/openclaw/openclaw/issues/53408) and [#107814](https://github.com/openclaw/openclaw/issues/107814) detail models silently dropping essential tool call parameters, severely degrading agent capability.

The presence of many `no-new-fix-pr` and `needs-maintainer-review` labels on these critical issues indicates a bottleneck in maintainers addressing these long-standing problems. While many new fixes are being proposed today, they are often awaiting review or author action, suggesting that getting fixes merged is a key constraint.

---

## 6. Feature Requests & Roadmap Signals

The project is receiving a steady stream of feature requests spanning UX, scalability, and new AI capabilities. Key signals include:

- **Control UI Enhancements**: There is a clear push to improve the Control UI, with requests for MathJax/LaTeX support ([#42840](https://github.com/openclaw/openclaw/issues/42840), 10 👍), quality/UX redesigns ([#75947](https://github.com/openclaw/openclaw/issues/75947)), and configurable upload limits ([#71142](https://github.com/openclaw/openclaw/issues/71142)). Recent PRs suggest these are being actively addressed.
- **Configurability & Observability**: Users want more control over their agents. Requests include configurable streaming timeouts ([#68596](https://github.com/openclaw/openclaw/issues/68596)), per-agent dreaming schedules ([#67413](https://github.com/openclaw/openclaw/issues/67413)), skill priority configuration ([#50199](https://github.com/openclaw/openclaw/issues/50199)), and richer tracing context for plugins ([#50291](https://github.com/openclaw/openclaw/issues/50291)).
- **Scalability & Multi-Tenancy**: As users deploy OpenClaw for more complex setups, requests for multi-agent/multi-bot support are growing. This is visible in requests for multiple Azure/Teams bots ([#71058](https://github.com/openclaw/openclaw/issues/71058)) and per-agent TTS/STT configuration ([#66252](https://github.com/openclaw/openclaw/issues/66252)).
- **New AI Integrations**: Users are eager for integration with cutting-edge features, such as the Anthropic advisor tool ([#63930](https://github.com/openclaw/openclaw/issues/63930)) and multi-index embedding memory for provider failover ([#63990](https://github.com/openclaw/openclaw/issues/63990)).

Likely Next Version Candidates: The volume of merged PRs and closed issues related to the Control UI and security (install policy acknowledgements) suggests these areas will be key features of the next release. Bug fixes for the P0/P1 issues are also likely to be prioritized.

---

## 7. User Feedback Summary

Real user pain points are centered around the core promise of OpenClaw: reliable, autonomous operation.

- **Reliability is the Top Concern**: Users are frustrated by regressions that break core workflows. The title of issue [#62505](https://github.com/openclaw/openclaw/issues/62505), "Coding Agent never completes anything (worked in 2026.4.2 and earlier)," captures this sentiment perfectly. The long life and high comment count on these issues indicate growing dissatisfaction.
- **Frustration with Silent Failures**: Many complaints involve silent data loss or failures. Issues describe messages being "silently lost" ([#50093](https://github.com/openclaw/openclaw/issues/50093)), tool parameters being "silently dropped" ([#53408](https://github.com/openclaw/openclaw/issues/53408)), and context switching "fail[ing] silently" ([#58957](https://github.com/openclaw/openclaw/issues/58957)). This undermines trust in the system.
- **Performance and Efficiency Concerns**: Users are noticing and reporting performance degradation. Complaints about token waste ([#67419](https://github.com/openclaw/openclaw/issues/67419)), memory spikes causing OOM kills ([#67413](https://github.com/openclaw/openclaw/issues/67413)), and process leaks ([#97616](https://github.com/openclaw/openclaw/issues/97616)) show an expectation for high efficiency.
- **Community Appreciation Acknowledged**: Despite the issues, there is clear appreciation for the project. User Reneb-cafe in [#73537](https://github.com/openclaw/openclaw/issues/73537) states, "...thank you for OpenClaw. We've been running it as a family and business assistant... it has genuinely become part of our daily workflow. Really appreciate the work you and the team put into this."

Overall, sentiment is mixed: users see the immense potential and have integrated OpenClaw into their lives, but the backlog of unresolved regressions is causing significant friction and skepticism.

---

## 8. Backlog Watch

Several important issues have been open for a long time without a resolution or even a fix PR, requiring urgent maintainer attention.

- **[Issue #70903: Persistent file-based provider cooldown blocks user for hours after billing recovery](https://github.com/openclaw/openclaw/issues/70903)**: A P0 issue from April that can completely block users. It is marked `stale` and `needs-product-decision`.
- **[Issue #62505: Coding Agent never completes anything](https://github.com/openclaw/openclaw/issues/62505)**: A P1 regression from early April that strikes at the heart of the product's use case. Still has no fix PR.
- **[Issue #38327: Crash with google-vertex/gemini-3.1-pro-preview](https://github.com/openclaw/openclaw/issues/38327)**: A P1 regression from March affecting a major cloud provider. No fix linked.
- **[Issue #91009: Codex PreToolUse native hook relay spawns CPU-bound processes](https://github.com/openclaw/openclaw/issues/91009)**: A P1 issue from June causing severe resource exhaustion.
- **[Issue #51927: Aggregation of Duplicate Transcript/Replay Bugs](https://github.com/openclaw/openclaw/issues/69208)**: This meta-issue from April encompasses a wide class of message-loss bugs affecting multiple channels. It remains open with no clear path to resolution.
- **Open PRs Awaiting Review**: Many "ready for maintainer look" or "needs proof" PRs are waiting, including high-impact fixes like [#125474](https://github.com/openclaw/openclaw/pull/125474) (CLI `--port` support), [#124429](https://github.com/openclaw/openclaw/pull/124429) (UI skill allowlist fix), and [#123975](https://github.com/openclaw/openclaw/pull/123975) (preventing typecheck infinite loops). A backlog here delays the delivery of numerous bug fixes to users.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report — AI Agent & Personal Assistant Open-Source Ecosystem
**Date: 2026-08-18**

---

## 1. Ecosystem Overview

The personal AI assistant and agent open-source ecosystem is experiencing a bifurcation: mature, high-volume projects (OpenClaw, Hermes Agent, ZeroClaw, CoPaw) are grappling with **reliability and security debt at scale**, while mid-tier projects (NanoBot, IronClaw, Moltis, NanoClaw) are aggressively shipping new features and platform integrations. A clear pattern emerges across all active projects: **users demand configurable, observable, and secure multi-session autonomous operation** — with silent failures, message loss, and resource leaks being the most frequently cited pain points. Cross-platform support (especially Windows) remains a recurring gap, and there is growing interest in standardization efforts (A2A protocols, OpenAI-compatible APIs, MCP interoperability). The ecosystem is healthy overall — contributors are active, maintainers responsive, and feature velocity high — but the backlog of unresolved P1/P0 reliability issues in flagship projects signals a looming consolidation or quality-focused release cycle.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs (24h) | Release Status | Health Score (1-5) |
|---|---|---|---|---|---|
| OpenClaw | 500 | 500 | 118 | No release; latest 2026-08-13 | 2.5 |
| Hermes Agent | 50 | 50 | ~25 (inferred) | v0.20.3 (Aug 16) | 3.5 |
| ZeroClaw | 50 | 50 | 16 | v0.9.0 milestone in progress | 4.0 |
| CoPaw (QwenPaw) | 14 | 35 | 22 | v2.1.0 (latest) | 3.5 |
| IronClaw | 28 | 44 | 16 | v1.3.0-rc.1 (Aug 17) | 4.0 |
| NanoClaw | 4 | 41 | 25 | No release noted | 3.5 |
| LobsterAI | 7 | 21 | 17 | v4.8 (latest) | 3.0 |
| NanoBot | 3 | 15 | 5 | No release; imminent | 4.0 |
| Moltis | 3 | 9 | 6 | No release; significant merge volume | 4.0 |
| PicoClaw | 1 (new bug) | 3 (merged) | 3 | No release | 3.5 |
| NullClaw | 0 | 1 (Dependabot) | 0 | No release | 2.5 |
| TinyClaw | 0 | 0 | 0 | Inactive | 1.0 |
| ZeptoClaw | 0 | 0 | 0 | Inactive | 1.0 |

---

## 3. OpenClaw's Position

**Advantages:**
- **Undisputed market leader** by volume: 500 issues + 500 PRs updated daily vs. 50–100 for the next tier — a 5–10x community engagement advantage.
- **Largest contributor base** with frequent, named contributors (steipete, jesse-merhi) plus a growing trend of AI-assisted PRs (Claude Code autonomous agents).
- **Deepest feature surface**: Control UI, CLI, gateway, A2A interactions, skills, memory, multi-channel — a comprehensive horizontal platform.

**Technical Approach Differences:**
- OpenClaw is a **monolithic, all-in-one platform** (gateway, agents, UI, skills) while peers like Hermes Agent (modular desktop-first) and ZeroClaw (RFC-driven, pluggable security pipeline) are pursuing modular/plugin architectures. This is both a strength (out-of-box completeness) and a liability (complex cross-component regressions like the Codex hook CPU-bound issue).

**Community Size Comparison:**
| Metric | OpenClaw | Hermes Agent | ZeroClaw |
|---|---|---|---|
| Daily issue updates | 500 | 50 | 50 |
| Daily PR updates | 500 | 50 | 50 |
| Open backlog | 484 issues / 382 PRs | Not disclosed | ~40% of issues are `status:accepted` RFCs |
| Contributor style | Broad, including AI-assisted | Single strong maintainer (@andrexibiza) + robust bots | Structured RFC-driven, community-engaged |

**Key Risk:** The maintainer bottleneck and P0/P1 backlog (e.g., #70903, #62505) is the largest threat to OpenClaw's dominance — users and contributors may defect to more responsive projects.

---

## 4. Shared Technical Focus Areas

These requirements are emerging **across 3+ projects** concurrently, indicating strong market demand:

| Need | Projects Exhibiting It | Specific Evidence |
|---|---|---|
| **Silent Failure Elimination** | OpenClaw, Hermes Agent, CoPaw, NanoBot, PicoClaw | Message/session loss, image drops, tool-call failures, false success on cron attachments — all top-severity bugs |
| **Multi-Session / Multi-Agent Orchestration** | OpenClaw, Hermes, NanoBot, NanoClaw, LobsterAI, CoPaw | WebUI side conversations, A2A cross-channel comms, per-user session isolation, agent-to-agent messaging |
| **Configurable Timeouts & Resource Bounds** | OpenClaw (#68596, #67413), NanoBot (spend firewall), NanoClaw (bounded polling), Moltis (WebUI RPC timeout) | Users need tuning for thinking models (DeepSeek-R1), token budgets, process leaks |
| **Windows & Cross-Platform Reliability** | Hermes (Windows ACL gaps, no CI), NanoBot (3 Windows fixes in 1 day), ZeroClaw (new scheduled Windows tests) | Windows is treated as first-class in new project generations, second-class in older ones |
| **Per-Provider and Per-Channel Configuration** | CoPaw (#7085), OpenClaw (multiple per-agent requests), Moltis (external agent model selection) | Users want different models per channel/agent/use-case |
| **Interoperability Standards** | ZeroClaw (OpenAI-compatible API RFC), LobsterAI (A2A proposal #2500), Hermes (ACP skills), CoPaw (MCP fixes) | Drop-in compatibility with existing tooling ecosystems is a rising demand |
| **Security Hygiene** | OpenClaw (env leak fix), ZeroClaw (p1 security batch), Hermes (credential isolation), CoPaw (media URL poisoning), LobsterAI (log redaction) | API keys in URLs/logs, attachment bounds, token lifecycle, credential inheritance |

---

## 5. Differentiation Analysis

| Project | Primary Focus | Target User | Technical Architecture |
|---|---|---|---|
| **OpenClaw** | Full-featured personal AI assistant (gateway + UI + agents + skills) | Power users, families, small businesses | Monolithic Node.js, Control UI, broad channel support |
| **Hermes Agent** | Modular desktop-first agent with desktop + cloud backends | Individual developers, desktop users | Multi-process (desktop app, gateway, agent), plugin system, strong security hardening |
| **ZeroClaw** | RFC-driven, security-hardened, enterprise-grade agent | Enterprise/platform engineers | Rust, pluggable security/auth pipeline, OpenAI-compatible API in progress |
| **CoPaw (QwenPaw)** | Chinese-ecosystem-first agent with messaging integrations | Chinese power users, SME teams | TypeScript/Node.js, multi-platform channel support (DingTalk, WeChat, Feishu, OneBot/QQ) |
| **IronClaw** | High-scale, durable automation with performance optimization | Ops/automation engineers | Rust (inferred from libSQL/release tags), DB write-pressure optimization, WASM tools |
| **NanoClaw** | Lightweight, channel-adaptive agent | Community contributors, flexible deployments | Channel adapter architecture, Docker driver, session-mode flexibility |
| **NanoBot** | Reliability-focused messaging agent with WebUI | Production-adjacent users | Go-like gateway (inferred), TypeScript TUI, Telegram/WebUI focus |
| **Moltis** | Rust-engine agent with container-runtime flexibility | Developers needing container isolation | Rust, Docker/Podman/Apple Containers, ACP agent support |
| **LobsterAI** | China-market agent with Electron desktop client | Chinese consumers/power users | Electron + OpenClaw integration, dsh engine, WeChat/OpenClaw plugins |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration (merging 16–118 PRs/day, active contributors):**
- **OpenClaw** (massive volume, but bottlenecked), **Hermes Agent** (high velocity, single-maintainer risk), **ZeroClaw** (structured, RFC-driven, security-focused), **CoPaw** (stabilizing after v2.1.0, high community response), **NanoClaw** (core-team channel refactor, community PRs within 24h of bug filings).

**Tier 2 — Steady Progress (5–16 PRs/day, focused scope):**
- **IronClaw** (performance epic + notifications overhaul), **LobsterAI** (sweeping April-era backlog, dsh engine integration), **NanoBot** (telegram watchdog + TUI), **Moltis** (heartbeat config fixes, managed files library), **PicoClaw** (maintenance/hardening).

**Tier 3 — Maintenance/Stable:**
- **NullClaw** (dependabot only, dormant but presumably stable).

**Tier 4 — Inactive:**
- **TinyClaw**, **ZeptoClaw** (zero activity — likely abandoned or seasonal).

**Maturity signal:** Projects with a formal RFC process (ZeroClaw, Hermes) and automated CI/health checks (IronClaw's daily failure taxonomy, Hermes's auto-fix bots, ZeroClaw's scheduled platform tests) are maturing faster and creating more sustainable contributor on-ramps.

---

## 7. Trend Signals

1. **"Silent failure" is the #1 trust-breaker.** Across all projects, the most severe and emotionally charged issues are silent message loss, dropped attachments, and hidden tool failures. Developers who prioritize explicit error surfacing, per-attachment delivery status, and configurable watchdog timeouts will win user trust.

2. **Cost observability & budget controls are a rising class of features.** NanoBot's spend firewall request, CoPaw's token-usage inflation fix, OpenClaw's token-waste complaints, and IronClaw's DB write-pressure epic all signal that **operating cost is becoming a first-class UX concern** as agents run longer and multiply.

3. **Architecture consolidation toward multi-agent & multi-session.** The industry is moving from single-assistant-to-single-user toward **agent families that coordinate across sessions, channels, and providers**. The emergence of A2A standardization attempts (LobsterAI/VOKO), session-scoped projects (ZeroClaw RFC), cross-chat agent communication (NanoBot), and per-channel model routing (CoPaw) points to an imminent wave of multi-agent orchestration features.

4. **Security is shifting from static (rest-at-rest) to dynamic (in-transit, behavioral).** ZeroClaw's per-execution confirmation tiers, Hermes's credential-inheritance closure, CoPaw's media URL poisoning defense, and PicoClaw's attachment bounds all indicate a move toward **runtime security policies** that adapt to user intent and resource availability.

5. **Container-runtime and driver abstraction are becoming strategic.** Moltis (Docker/Podman/Apple Containers), NanoClaw (Docker driver with future WASM/process-local), and IronClaw (OMP core-tool contract for WASM) are all building abstraction seams — expecting a **multi-runtime future** where agents can execute in isolation, sandboxes, or remote compute depending on trust and performance needs.

6. **AI-assisted development is now part of the normal loop.** OpenClaw's "AI-assisted" PRs, Hermes's auto-merge bots, and the community's acceptance of agent-authored fixes indicate that **agentic CI/CD is becoming standard practice** — a signal that AI agents building AI agents is entering the mainstream.

7. **China-ecosystem projects are innovating separately but converging.** CoPaw, LobsterAI, and PicoClaw all emphasize Chinese messaging channels (WeChat, DingTalk, QQ/OneBot), Chinese cloud providers (Volcengine, Xiaomi, Qwen), and China-specific UX (Bailian/DashScope migration) — yet they're borrowing the same architecture patterns (channel adapters, provider routing, plugin systems) as Western peers, indicating a converged global pattern with regional flavors.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-18

## 1. Today's Overview
NanoBot (HKUDS/nanobot) is in a **very active development phase** with 15 PRs updated in the last 24 hours, 5 of which were merged/closed. The project is clearly past its early startup stage: work is dominated by **stability hardening** (Telegram polling recovery, gateway process identity, Windows compatibility) and **WebUI feature expansion** (session messaging, side conversations, follow-up suggestions). A notable **recovery PR (#5406)** for the native TypeScript terminal UI, which had been mistakenly merged and then reverted, signals careful maintainer oversight. Issue volume is low (3 active), and the maintainers have been closing issues with corresponding fixes (e.g., #5171 closed by PR #5156). The release cadence is zero in the last 24h, but the sheer volume of merged code suggests an imminent cut.

## 2. Releases
No new releases were published in the last 24 hours. The most recent activity suggests a release may be pending given that multiple merged PRs (e.g., Telegram watchdog, TypeScript UI) are not yet publicly available.

## 3. Project Progress
Five PRs were merged or closed, marking significant progress:

- **[#5406 — feat(cli): add native TypeScript terminal UI](https://github.com/HKUDS/nanobot/pull/5406)** *(merged)*: Re-delivers the native TypeScript TUI that was previously mishandled during a merge incident. Includes cross-terminal fixes.
- **[#5416 — fix(gateway): stabilize process identities](https://github.com/HKUDS/nanobot/pull/5416)** *(merged)*: Replaces locale-dependent macOS `ps lstart` parsing with native `proc_pidinfo` birth timestamps. A strong reliability fix for multi-platform gateway process tracking.
- **[#5410 — fix(goal): stop repeating clarification replies](https://github.com/HKUDS/nanobot/pull/5410)** *(merged, p2)*: Fixes an agent behavior where sustained goals caused the bot to repeatedly re-inject the goal after every plain-text final response. Ties to issue #4864 where a complete_goal loop was reported.
- **[#5156 — fix(telegram): recover from silently stalled polling](https://github.com/HKUDS/nanobot/pull/5156)** *(merged, p2)*: Directly fixes issue #5171 where Telegram polling would stall permanently after network blips. Includes a watchdog that rebuilds stalled connection pools.
- **[#5301 — fix(telegram): bridge stdlib logging and detect stalled polling](https://github.com/HKUDS/nanobot/pull/5301)** *(merged)*: Lower-risk observability piece split from #5156 for earlier landing.

## 4. Community Hot Topics
The most engaged item this week is the long-running **goal loop bug**:

- **[Issue #4864 — Endless loop for `<tool_call> <function=complete_goal>`](https://github.com/HKUDS/nanobot/issues/4864)** (7 comments, 1 👍, open since July 9th): The agent's `complete_goal` tool erroring due to a gateway parsing regression. The merged PR [#5410](https://github.com/HKUDS/nanobot/pull/5410) targets the "clarification repeat" mechanism, but the root parsing issue requires attention from gateway-side work being fixed in #5416.

Other notable discussions are embedded in PRs rather than Issues:

- **[PR #5364 — feat(webui): temporary side conversations](https://github.com/HKUDS/nanobot/pull/5364)** (open): Adds parallel, transient conversations in the WebUI. Mirrors power-user expectations (similar to Claude's side conversations).
- **[PR #5358 — feat(webui): session messaging via mentions](https://github.com/HKUDS/nanobot/pull/5358)**: Introduces server-owned `@name` sessions and bidirectional messaging between sessions.

**Underlying needs**: The community is clearly pushing NanoBot toward "multi-session/multi-parallel" expert workflows and demanding higher reliability in messaging integrations and long-horizon goal execution.

## 5. Bugs & Stability
Three bugs surfaced or were active in the last 24h. Ranked by severity:

1. **[Issue #4864 — Endless complete_goal loop](https://github.com/HKUDS/nanobot/issues/4864)** *(high — author reports blocked agent behavior)*: A gateway parameter-serialization regression breaks the `complete_goal` tool. No direct fix in latest batch, but related PRs (#5410) mitigate symptoms. Not yet resolved.
2. **[Issue #5171 — Telegram polling stall](https://github.com/HKUDS/nanobot/issues/5171)** *(high — silent failures, message loss)*: **Resolved** by merged PRs [#5156](https://github.com/HKUDS/nanobot/pull/5156) and [#5301](https://github.com/HKUDS/nanobot/pull/5301).
3. **[PR #5407 — Heartbeat/dream jobs fire when disabled](https://github.com/HKUDS/nanobot/pull/5407)** *(p2, regression)*: Disabling scheduled jobs via config did not retire persisted jobs; tokens burned silently. Fix PR is open, not yet merged.

**Windows/Cross-platform fixes** (themes surfacing repeatedly):
- **[PR #5341 — weather skill Windows-safe](https://github.com/HKUDS/nanobot/pull/5341)**: Windows PowerShell's curl alias breaks skill execution. Open.
- **[PR #5415 — gateway Windows venv child adoption](https://github.com/HKUDS/nanobot/pull/5415)**: Fixes Windows venv launcher PID tracking. Open.
- **[PR #5414 — Slack file download redirect validation](https://github.com/HKUDS/nanobot/pull/5414)**: Security hardening against crafted redirects. Open.
- **[PR #5413 — Provider fallback policy on exceptions](https://github.com/HKUDS/nanobot/pull/5413)**: Handles provider exceptions that bypass fallback logic. Open.
- **[PR #5412 — Flush background child logs](https://github.com/HKUDS/nanobot/pull/5412)**: Fixes block-buffered stdout in managed processes, delaying diagnostics. Open.

## 6. Feature Requests & Roadmap Signals
The most distinct feature signals:

- **[Issue #5409 — Hybrid spend firewall for LLM budgets](https://github.com/HKUDS/nanobot/issues/5409)**: A plea for configurable spend caps and loop protection to prevent runaway token bills. Signals that users are deploying NanoBot in production but are concerned about economics. This is a strong candidate for a v-next feature.
- **[PR #5408 — WebUI follow-up suggestions](https://github.com/HKUDS/nanobot/pull/5408)**: Ephemeral, chat-scoped follow-ups (similar to DeerFlow). A "prosumer" UX feature likely to be merged soon.
- **[PR #5358 — Session messaging via mentions](https://github.com/HKUDS/nanobot/pull/5358)**: Cross-chat agent communication—a "multi-agent orchestration" preview.
- The **native TypeScript TUI** (#5406) is now available — flagship UX modernization.

Prediction: Next minor version will include TUI, session mentions, and the Telegram watchdog. The **spend firewall** seems like a high-velocity community-driven must-have.

## 7. User Feedback Summary
Users are operating NanoBot in real-world, production-adjacent settings and are finding the friction:

- **Frustration**: Silent failures (Telegram), agent repetition loops that spend tokens, and config values that don't apply (e.g., "disabled" jobs still firing).
- **Force-multiplier requests**: Sessions that talk to each other (#5358), parallel side-conversations (#5364), and budget controls (#5409) indicate demand for power-user, multi-tasking autonomy.
- **Platform expectations**: Windows users are increasingly active—**three separate Windows-specific fixes** in one day (#5341, #5415, #5416) highlight that cross-platform reliability is now the norm, not the exception.
- **Satisfaction indicators**: Maintainers are reactive and transparent (e.g., #5406 recovery note), which builds trust.

## 8. Backlog Watch
- **[PR #5341 — Windows-safe weather workflow](https://github.com/HKUDS/nanobot/pull/5341)** (open since Aug 11, p2): Blocked or under-reviewed. Given other Windows issues emerged, it's likely to receive attention soon.
- **[Issue #4864 — complete_goal loop](https://github.com/HKUDS/nanobot/issues/4864)** (open since Jul 9): Root cause is gateway serialization, not fully addressed by mitigation in #5410. Needs focused maintainer attention.
- **[PR #5407 — Disabled cron jobs still fire](https://github.com/HKUDS/nanobot/pull/5407)** (p2, high user impact—silent token burn): Should be prioritized for merge, as it's a reliability bug with financial consequences for cloud users.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-18

## 1. Today's Overview

High-velocity development continues across the Hermes Agent codebase, with 50 issues and 50 PRs updated in the last 24 hours and a patch release (`v0.20.3`) rolling up ~125 merged PRs for downstream consumers. The project shows strong momentum on security hardening (credential isolation, Windows ACL gaps, browser policy fail-closed behavior), desktop stability (orphaned backend reaping, profile deletion edge cases), and gateway/state robustness (SessionDB threading fix, cron media attachment delivery). Community engagement remains moderate, with the most active discussion centered on the completed god-file sharding epic (#78647, 76 comments), a stale skills index automation issue (#66616, 48 comments), and the webhook feature package tracker (#84834). No release-blocking regressions were reported in the last 24 hours.

## 2. Releases

**v2026.8.16.2 — Hermes Agent v0.20.3** (released August 16, 2026)

Patch release designed as a stable, tagged rollup of the ~125 PRs merged since `v0.20.2`, explicitly intended for Docker images, hosted deployments, and fresh installs. No breaking changes or migration notes were included in the release description.

---

## 3. Project Progress

**Merged/closed PRs today (select highlights):**

- **[#88753 — fix(gateway,state): SessionDB off the event-loop thread + contention-safe v25 migration**](https://github.com/NousResearch/hermes-agent/pull/88753) *(closed)* — Fixes a fleet-reported gateway that could not restart due to a v25 schema migration blocking the event-loop thread, with the loop-liveness watchdog repeatedly firing exit 75.
- **[#88631 — fix(cron): manual runs no longer silently drop media attachments**](https://github.com/NousResearch/hermes-agent/pull/88631) *(closed)* — Enterprise-reported bug where `hermes cron run <job-id>` could deliver text but silently drop PDF/image attachments, reporting success; scheduled runs were unaffected.
- **[#88775 — fix(desktop): fail-stop deleted-profile reconnects and evict the stale rail badge**](https://github.com/NousResearch/hermes-agent/pull/88775) *(closed)* — Renderer-half fix for ghost rail badges surviving Bot Mode profile deletion, and fail-stop for permanently rejected reconnects.
- **[#88776 — fix(plugins): hide bundled model providers from plugin list](https://github.com/NousResearch/hermes-agent/pull/88776)** *(closed, salvage of #27268)* — Bundled `plugins/model-providers/` entries no longer clutter `hermes plugins list`.
- **[#88773 — docs: unified Gateways page, settings profile scope, plugins cleanup, Bot Mode group rows, host.openWorkspace**](https://github.com/NousResearch/hermes-agent/pull/88773) *(closed)* — Docs synced with five desktop changes merged recently.
- **[#35100 — fix(cron): surface media attachment delivery failures](https://github.com/NousResearch/hermes-agent/pull/35100)** *(closed)* — Cron media delivery now returns per-attachment errors instead of treating failures as clean success, preventing duplicate-text fallback after partial media failure.

**Open PRs advanced today:**

- **[#76616 — feat(desktop): add safe current backend restart**](https://github.com/NousResearch/hermes-agent/pull/76616) — Adds safe restart for both local and SSH backends, with ownership proof before termination in SSH mode.
- **[#68766 — fix(agent): recover sessions on transient provider outages**](https://github.com/NousResearch/hermes-agent/pull/68766) — Extended retry backoff for overload/5xx/timeout windows.
- **[#62492 — fix(config): auto-migrate stale profile config on serve/dashboard startup**](https://github.com/NousResearch/hermes-agent/pull/62492) — Fixes named profiles keeping stale config versions after `hermes update`.
- **[#84512 — fix(acp): expose installed skills as slash commands**](https://github.com/NousResearch/hermes-agent/pull/84512) — Makes installed skills visible in ACP clients like Paseo and Zed.
- **[#88774 — fix(security): fail closed when website-policy module is unavailable**](https://github.com/NousResearch/hermes-agent/pull/88774) — Replaces fail-open URL admission with strict deny when policy module can't load.

---

## 4. Community Hot Topics

- **[#78647 — Large-file decomposition: 20/20 done (CLOSED)**](https://github.com/NousResearch/hermes-agent/issues/78647) — 76 comments, 0 reactions. This repo-wide epic enforcing "god files are sharded, never reverted" generated strong community participation in architecture refactoring, signaling developer buy-in on the maintainability direction.

- **[#66616 — Skills index is stale or degraded (OPEN)**](https://github.com/NousResearch/hermes-agent/issues/66616) — 48 comments, 0 reactions. An automated freshness probe reports the Skills Hub index is 29.8h old (limit 26h). The high comment volume suggests this automation failure has been a persistent nuisance for docs consumers, though no fix PR is explicitly linked yet.

- **[#84834 — Webhook Feature Package — graph-gated repair meta-issue (OPEN)**](https://github.com/NousResearch/hermes-agent/issues/84834) — 17 comments, 0 reactions. Community is tracking the 5×2×3 webhook surface repair across ingress, execution, delivery, configuration, deployment, and docs. This is a broad, well-structured effort driven largely by one maintainer (@andrexibiza).

**Underlying need analysis:** The highest-signal discussions center on (a) maintainability through structural refactoring, (b) infrastructure automation reliability (skills index), and (c) broad surface-area feature completeness for webhook integrations — suggesting the community is pushing beyond core agent capabilities into production-integration territory.

---

## 5. Bugs & Stability

**Reported today (or updated today with new activity), ranked by severity:**

| Severity | Issue | Summary | Fix PR? |
|---|---|---|---|
| **P1** | [#53666 — clarify tool prompts don't render in chat UI](https://github.com/NousResearch/hermes-agent/issues/53666) | Users see no clarification question and replies appear empty in the desktop chat UI; CLI subprocess is where prompts are shown. Still open, no fix PR linked. | ❌ |
| **P2** | [#87654 — Vision tools disappear after first availability probe](https://github.com/NousResearch/hermes-agent/issues/87654) | `_AuxProbeClientStub` gets cached, causing `vision_analyze`/`browser_vision` to vanish from sessions after initial probe; dashboard shows enabled. | ❌ |
| **P2** | [#88758 — compression: preserve raw durable watermark through replay cleanup](https://github.com/NousResearch/hermes-agent/issues/88758) | Boundary issue between live snapshot row proof and freshly loaded durable transcript, potentially losing durable rows during B2 restore flow. | ❌ |
| **P2** | [#77305 — failed API calls consume subagent iteration budget](https://github.com/NousResearch/hermes-agent/issues/77305) | Retryable failures (HTTP 429) burn the same budget as successful calls, starving the fallback chain logic flaw. | ❌ |
| **P2** | [#79101 — API server stores virtual model alias as real model (CLOSED)**](https://github.com/NousResearch/hermes-agent/issues/79101) | Session created without explicit `model` persists its alias as real model ID, breaking subsequent chat calls; closed, fix presumably merged. | ✅ |
| **P3** | [#16552 — Docker cgroup probe failure removes resource limits (OPEN)](https://github.com/NousResearch/hermes-agent/issues/84248) | Security-audit class: cgroup probe failure can remove resource limits. | ❌ |
| **P3** | [#84246 — Archive/installer-output consumers lack uniform authenticity and finite resource bounds (OPEN)](https://github.com/NousResearch/hermes-agent/issues/84246) | Security-campaign interlock; part of EPIC #82591. | ❌ |
| **P3** | [#88706 — Security: Close use-time, provenance, and authority gaps behind #88232/#88435 (OPEN)](https://github.com/NousResearch/hermes-agent/issues/88706) | Follow-up hardening campaign for SSH credential leak path; multiple components affected. | ❌ |

**Desktop orphan-backend class:** Two issues ([#76245](https://github.com/NousResearch/hermes-agent/issues/76245) and [#80898](https://github.com/NousResearch/hermes-agent/issues/80898)) both closed today, addressing the same root class (backend not drained/killed on quit).

**Windows security gap:** [#77462 — Windows at-rest ACL hole](https://github.com/NousResearch/hermes-agent/issues/77462) remains open with `_secure_file` confirmed a no-op on Windows; marked CRITICAL on live hosts.

---

## 6. Feature Requests & Roadmap Signals

**In-flight with active PRs (likely in next release):**

- **[#44878 — Per-call output speed (tokens/sec) for desktop status bar and runtime footer**](https://github.com/NousResearch/hermes-agent/pull/44878) — Users get real-time throughput telemetry; PR still open.
- **[#60417 — Behavioral analysis with 5-axis scoring and insight cards**](https://github.com/NousResearch/hermes-agent/pull/60417) — New `/behavior` command building qualitative profiles from `state.db`; complements quantitative `/insights`.
- **[#84512 — Expose installed skills as slash commands in ACP hosts**](https://github.com/NousResearch/hermes-agent/pull/84512) — Improves integration for external ACP clients (Zed, Paseo).

**Open feature-tracker issues:**

- **[#86950 — ByteDance (TikTok Business + Douyin) Plugin Integration Feature Package**](https://github.com/NousResearch/hermes-agent/issues/86950) — 4 standard plugin integrations scoped; P3.
- **[#83565 — Child-process credential-inheritance closure (EPIC)**](https://github.com/NousResearch/hermes-agent/issues/83565) — Meta-issue binding all PRs/issues fixing trusted credentials reaching untrusted child processes.
- **[#11239 — Env-backed secret references for MCP server config in `~/.hermes/config.yaml`**](https://github.com/NousResearch/hermes-agent/issues/11239) — Requests config not be secret-bearing by default; 2 👍, opened April 16.

**Prediction:** Per-call speed display, `/behavior` insights, and ACP skill visibility are the most likely near-term additions given active PRs; TikTok/Douyin plugin integration is likely mid-term given the detailed feature-package framing.

---

## 7. User Feedback Summary

**Pain points surfacing repeatedly:**

- **Desktop UX gaps:** The BOTS sidebar showing wrong session content on click ([#88200](https://github.com/NousResearch/hermes-agent/issues/88200), closed), demo plugins enabled by default cluttering production UI ([#76064](https://github.com/NousResearch/hermes-agent/issues/76064), closed), and clarify prompts invisible in chat UI ([#53666](https://github.com/NousResearch/hermes-agent/issues/53666), open P1) show users are actively evaluating the desktop client for polish.
- **Silent data loss is the sharpest complaint:** Two of three top recent issues involved silent drop of media attachments ([#88631](https://github.com/NousResearch/hermes-agent/pull/88631), manual cron runs) and silent disappearance of vision tools ([#87654](https://github.com/NousResearch/hermes-agent/issues/87654)). Both were or are P2.
- **Install/update friction on non-standard platforms:** Termux native package path request ([#86986](https://github.com/NousResearch/hermes-agent/issues/86986), closed) highlights Android-onboarding pain; expected since Hermes is manylinux-first.
- **Windows is a second-class citizen:** The CRITICAL ACL hole ([#77462](https://github.com/NousResearch/hermes-agent/issues/77462)), the no-Windows-CI gap ([#77476](https://github.com/NousResearch/hermes-agent/issues/77476)), and the orphan-backend class ([#80898](https://github.com/NousResearch/hermes-agent/issues/80898)) all point to Windows-specific reliability gaps.

**Satisfaction signals:** The community is actively filing detailed, well-structured bug reports and feature-trackers; duplicates are being systematically folded into meta-issues (e.g., Telegram menu-button API folded into identity draft), suggesting users trust the maintainers to consolidate direction. The aggressive auto-fix and auto-merge bots ([#88777](https://github.com/NousResearch/hermes-agent/pull/88777)) keep the repo hygiene high.

---

## 8. Backlog Watch

**Issues/PRs needing maintainer attention:**

| Issue/PR | Age | Priority | Why it's stuck |
|---|---|---|---|
| [#11239 — Env-backed secret references for MCP config](https://github.com/NousResearch/hermes-agent/issues/11239) | 124 days (Apr 16) | P3 | Open since April, 2 👍; no linked work. Configuration security defaults matter, especially given the Windows ACL gap and child-process credential leakage class. |
| [#53666 — clarify prompts don't render in chat UI](https://github.com/NousResearch/hermes-agent/issues/53666) | 52 days (Jun 27) | P1 | Long-lived P1 with no fix PR. Silent loss of user-interaction is a severe UX bug for agent workflows. |
| [#44878 — Per-call output speed; long-lived PR](https://github.com/NousResearch/hermes-agent/pull/44878) | 67 days (Jun 12) | P3 | Created June 12, still open. Broad surface area (agent, CLI, TUI, desktop, gateway) likely explains the delay, but users are clearly asking for performance visibility. |
| [#53902 — Renderer GPU 98% loop, 13W power draw](https://github.com/NousResearch/hermes-agent/issues/53902) | 51 days (Jun 28) | P3 | Desktop performance regression from v0.17.0 with no linked fix; laptop users are likely affected by battery drain. |
| [#48860 — OAuth sanitizer breaks docs URL (NXDOMAIN)](https://github.com/NousResearch/hermes-agent/issues/48860) | 60 days (Jun 19) | P2 | Confirmed bug rewriting valid URLs to dead domains; no linked fix PR. |
| [#78539 — README interrupt row contradicts busy model](https://github.com/NousResearch/hermes-agent/issues/78539) | 14 days (Aug 4) | P3 | Open but now has a fix attempt: [#88770](https://github.com/NousResearch/hermes-agent/pull/88770) open as of today. |

**General observation:** The maintainer @andrexibiza is driving most high-volume refactor/feature activities, creating a bus-factor risk; several P2 bugs (vision-tool caching, iteration-budget consumption) are recent and unattended. The project overall shows healthy velocity with clear structural direction (sharding, hardening, consolidation), but Windows-specific reliability and long-stalled P1 UX bugs deserve prioritization.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-18

## 1. Today's Overview

PicoClaw is in a steady maintenance-and-hardening phase, with 7 items updated in the last 24 hours. One bug issue (#3311) was closed alongside its fix PR (#3312), which successfully addressed a critical silent-failure loop in the agent tool iteration system. Channel integration work continues on two fronts: an open Slack media-upload fix (#3340) is pending review, and a long-running Weixin multi-instance enhancement PR (#2606) was closed/merged after nearly four months of development. One new bug surfaced today regarding Google Antigravity generation issues (#3339), which may require maintainer attention. No new releases were published, and the stale-label sweep appears to be clearing older items.

## 2. Releases

No new releases were published in the last 24 hours. The project has no release notes or changelog entries to report.

## 3. Project Progress

**Three PRs were closed/merged in the last 24 hours, reflecting meaningful stability and feature improvements:**

- **PR #3312 (merged)** — `fix(agent): stop turn early on repeated identical tool failure` by lucapette: This fix resolves a critical issue where the agent loop would re-call the LLM and re-execute the same failing tool up to `max_tool_iterations`, leaving users without an answer for minutes. The fix causes the turn to stop early upon detecting identical repeated tool failures, directly addressing Issue #3311. This is a significant reliability improvement for production users.
- **PR #271 (merged)** — `fix: env overrides when config.json is missing and add regression test` by tbeaudouin05: This long-standing bug fix (opened in February) ensures `env.Parse(cfg)` runs even when `config.json` is absent, which is critical for Fly.io deployments and other environments that rely on secrets/env only. Previously, missing config files would silently default to `glm-4.7` and fail due to missing credentials. This was merged after six months, indicating thorough review.
- **PR #2606 (merged)** — `feat: enhance Weixin channel support and configuration` by dsus4wang: This four-month enhancement adds channel directory and dynamic instance handling for Weixin, improves validation and error handling for illegal channel names, and strengthens multi-instance flow stability across backend, frontend, and docs. This is a significant feature advance for the Weixin platform.

## 4. Community Hot Topics

The most active discussion in the last 24 hours centers on IRC long-message handling:

- **Issue #3287** — `[Feature] Better support long messages in IRC` by superuser-does (6 comments, created July 22, updated August 17): The community is actively discussing how PicoClaw should handle IRCv3 messages exceeding the 512-byte limit. The core challenge is that IRC clients auto-split long messages, and PicoClaw needs to treat these splits as a single cohesive message. This is a **protocol-complexity issue** — the underlying need is reliable multi-line message reconstruction, which is subtle because newlines are also message delimiters in IRC. The sustained discussion (nearly a month old) suggests maintainers may be exploring design tradeoffs.

## 5. Bugs & Stability

**New bug reported today (severity: medium):**

- **Issue #3339 (open)** — `[Bug] Antigravity generation returns generic 429 despite valid OAuth scopes and successful model discovery` by k3XD16: Google Antigravity authentication and model discovery work correctly, but every generation request returns a generic `RESOURCE_EXHAUSTED` (429) error with no quota details. This blocks all generation via Antigravity, making it a **functional blocker for users on that provider**, though it does not affect other providers. No fix PR exists yet. Severity: **medium** — it affects a single provider but completely breaks that integration.

**Bug closed with fix:**

- **Issue #3311 (closed)** — `[BUG] Repeated identical tool failure loops silently to max_tool_iterations — user never gets an answer` by lucapette: This was a **high-severity** production issue (observed over Telegram) where a tool failing with the same error repeatedly would silently spin for minutes without user reply. The fix in PR #3312 was merged, resolving the issue.

**Long-standing bug fix merged:**

- **PR #271** resolves a config-loading bug where env overrides were ignored when `config.json` was absent, causing deployments to fall back to the default model (`glm-4.7`) and fail on missing credentials. This was a **critical deployment bug** for env-only setups like Fly.io.

## 6. Feature Requests & Roadmap Signals

Two feature signals stand out today:

- **IRC long-message support (Issue #3287)**: The community clearly wants better IRCv3 long-message handling, and the discussion has been ongoing for nearly a month without a proposed fix. Given the sustained interest (6 comments) and the clear use case, this is a plausible target for an upcoming enhancement — likely requiring message-reassembly logic that distinguishes between intentional newlines and split-message continuations.

- **Weixin multi-instance support (PR #2606, merged)**: This enhancement signals that the project is investing in channel-level improvements (dynamic instance handling, better validation). This may foreshadow similar multi-instance refactoring for other channels (Slack, Telegram, Discord) in future releases.

## 7. User Feedback Summary

Real user pain points surfaced in the last 24 hours include:

- **Silent failures are the biggest frustration**: Issue #3311 documents a production incident where the agent never replied to a `git` command request over Telegram — the user waited minutes without any answer. This is a trust-breaking behavior for an AI assistant product, and the fix is welcome.
- **Provider-specific integration issues**: Issue #3339 shows a user who correctly set up OAuth scopes and confirmed model discovery, yet still hit a generic 429 — suggesting providers may need better error-surfacing and diagnostics in PicoClaw.
- **Configuration fragility**: PR #271 highlights that deployments relying on env-only configuration (without `config.json`) were silently misconfigured, failing on missing credentials due to default fallback behavior.

## 8. Backlog Watch

Items that may need maintainer attention:

- **Issue #3287** — `[Feature] Better support long messages in IRC` (open since July 22, 6 comments, no PR proposed): This is the longest-running active discussion that lacks a proposed implementation. Maintainers may want to weigh in on design constraints before the thread goes stale.
- **Issue #3339** — `[Bug] Antigravity generation returns generic 429` (opened today, 0 comments): Fresh bug with no engagement yet; needs triage to determine if it is a PicoClaw issue, a provider API issue, or a quota/rate-limit misconfiguration.
- **PR #3340** — `fix(slack): set FileSize on media upload params` (opened today, pending review): Fresh PR that addresses a Slack-go SDK v0.23.1 hard requirement for file length on upload. This fix is straightforward but blocks Slack media uploads if not merged — it may warrant quick review and merge.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-18

## 1. Today's Overview

NanoClaw is in an intense period of channel-layer and driver-architecture development. The project saw **41 PRs** updated in the last 24 hours — a very high activity level — with **25 of those merged or closed** and **16 still open**. The maintainer team (led by gavrielc) is actively landing a multi-wave "channels" refactor that introduces adapter-declared session modes, membership hooks, post-delivery hooks, and a session-runtime driver seam with Docker as the built-in realization. Community contributors are also active: two bug-fix PRs targeting task log retention and pending-message polling bound directly to issues filed less than 24 hours ago, showing a responsive maintainer community. However, the day also surfaced **4 issues**, including **3 still open**, one of which (the one-door task delivery regression) is a potentially severe bug affecting routine chat-session tasks. Overall, the project is in a healthy, fast-moving state, though the breadth of open PRs (16) suggests a substantial review backlog.

## 2. Releases

No new releases were published today (latest release date is unknown, no release data was provided).

## 3. Project Progress

**Major merged/closed PRs (25 total closed/merged)**

The day's merged work is dominated by the **channel-layer wave** lead by the core team:

- **Wave A — Shared channel-layer library + canvas cluster** ([#3305](https://github.com/nanocoai/nanoclaw/pull/3305)): Merged — syncs main into channels and lands the shared Slack Web API client plus token-key convention, and the canvas actions cluster registered via the existing registry.
- **Adapter-declared session-mode context defaults** ([#3304](https://github.com/nanocoai/nanoclaw/pull/3304)): Merged — adds optional `sessionMode` to adapter-declared per-context defaults allowing `per-thread` sessions for thread-based platforms like Slack.
- **Bridge inbound-policy registration seam** ([#3292](https://github.com/nanocoai/nanoclaw/pull/3292)): Merged — enables modules to intercept every inbound dispatch path without editing bridge source for bot-authored-message policies.
- **Setup wizard per-channel pre-step + companion-skill declarations** ([#3297](https://github.com/nanocoai/nanoclaw/pull/3297)): Merged — gives wizard extension points for programmatic credential binding and post-install companion skills.
- **Router session-created hook** ([#3293](https://github.com/nanocoai/nanoclaw/pull/3293)): Merged — notifies registered modules when an engaged message creates a brand-new session, enabling platform-specific conversation bootstrap.
- **Post-delivery hook with first-delivery context** ([#3294](https://github.com/nanocoai/nanoclaw/pull/3294)): Merged — lets channel modules observe first outbound message for onboarding affordances.
- **Generic membership-event hook on Chat SDK bridge** ([#3295](https://github.com/nanocoai/nanoclaw/pull/3295)): Merged — forwards platform member-joined events to per-channel handlers, supporting adopt-on-invite behavior.
- **extendTool — additive MCP tool schema extension** ([#3296](https://github.com/nanocoai/nanoclaw/pull/3296)): Merged — modules can extend base tool schemas additively without editing the base tool source.
- **Wave B — Defaults factory, membership, onboarding, a2a guard** ([#3309](https://github.com/nanocoai/nanoclaw/pull/3309)): Merged — completes the Slack channel layer with per-thread declared everywhere, creation-time stamps, and a2a guard.
- **Restore slack-formatting container skill** ([#3310](https://github.com/nanocoai/nanoclaw/pull/3310)): Merged — fixes a silent upstream-main merge drop of a container skill, restoring it byte-identical.

**Notable community contributions merged:**

- **fix(agent-runner): escape attachment type in agent-facing XML** ([#3300](https://github.com/nanocoai/nanoclaw/pull/3300)): Open — fixes a formatter bug where the attachment `type` field was unescaped while all others were.
- **fix(add-codex): bump @openai/codex pin** ([#3299](https://github.com/nanocoai/nanoclaw/pull/3299)): Open — addresses a time-sensitive GPT-5.4 retirement issue with a dependency pin bump.

## 4. Community Hot Topics

The most active issue and PR items (highest comment counts, reactions):

- **Issue #1143** ([closed](https://github.com/nanocoai/nanoclaw/issues/1143)) — "Skills docs reference /data/env path that no longer exists": 2 comments, auto-filed by triage bot. This 5-month-old documentation bug with only 2 comments and no upvotes is the "most discussed" issue, suggesting the project's issue tracker is heavily bot-moderated with low community interaction.
- **Issue #3203** — "codex provider emits undeclared `file` ProviderEvent" ([open](https://github.com/nanocoai/nanoclaw/issues/3203)): 1 comment, 0 upvotes. Community member mshirel identified a typecheck failure on main causing generated images to be silently dropped — a real functional regression with minimal discussion.
- **Issue #3301** — "Tasks firing in chat sessions run one-door: logs dropped, replies eaten, series unlisted" ([open](https://github.com/nanocoai/nanoclaw/issues/3301)): Filed today by glifocat with detailed root cause referencing the #2988 one-door delivery change in 2.1.48.

**Underlying needs:** The channel layer work is clearly driven by the need for functional, per-platform conversational behavior (Slack per-thread, local web chat). Community users are pushing for two things: (1) safer task execution (one-door regression, log loss), and (2) bounded resource behavior (pending-message polling backlogs). The low comment counts on issues suggest users go straight to PRs with fixes, which is a healthy sign of a contributor-friendly codebase.

## 5. Bugs & Stability

**Ranked by severity:**

1. **[HIGH — Regression, data loss]** Issue [#3301](https://github.com/nanocoai/nanoclaw/issues/3301): Since one-door task delivery (2.1.48), `kind='task'` rows firing in chat sessions switch the whole query into task mode — logs dropped, replies eaten, series unlisted. This affects pre-existing tasks still in chat sessions (user says "on my install that is every l…"). **Fix PR exists**: [#3303](https://github.com/nanocoai/nanoclaw/pull/3303) — "fix(tasks): keep run logs for task rows firing in chat sessions" (open, authored by the issue filer).

2. **[HIGH — Backlog/bounded resource]** Issue [#3289](https://github.com/nanocoai/nanoclaw/issues/3289): `getPendingMessages()` loads *every* due pending row into JavaScript before applying limits — unbounded memory for accumulated backlogs. **Fix PR exists**: [#3291](https://github.com/nanocoai/nanoclaw/pull/3291) — "fix: bound pending message polling" (open, authored by the issue filer).

3. **[MEDIUM — Typecheck failure on main, dropped images]** Issue [#3203](https://github.com/nanocoai/nanoclaw/issues/3203): codex provider emits undeclared `file` ProviderEvent; `/add-codex` fails typecheck on main; generated images silently dropped. No fix PR found in the day's update list.

4. **[LOW — Escaping bug]** PR [#3300](https://github.com/nanocoai/nanoclaw/pull/3300): `formatAttachments` fails to escape the attachment `type` field while escaping all others — an injection surface in agent-facing XML.

5. **[LOW — Docs bug, long-standing]** Issue [#1143](https://github.com/nanocoai/nanoclaw/issues/1143): Skill docs reference a `/data/env` path that no longer exists.

6. **[LOW — Silent merge loss]** PR [#3310](https://github.com/nanocoai/nanoclaw/pull/3310): The upstream-main merge silently dropped `container/skills/slack-formatting/` — no delete commit existed. Already merged, restored byte-identical.

## 6. Feature Requests & Roadmap Signals

- **Local web chat channel** is the biggest roadmap signal: two PRs attempt it — [#3298](https://github.com/nanocoai/nanoclaw/pull/3298) ("add local web chat" as a feature skill) and [#3290](https://github.com/nanocoai/nanoclaw/pull/3290) ("Add webchat channel: local browser chat via native HTTP bridge"). Two independent implementations for the same feature is notable — strong user demand for a built-in conversational UI beyond external platforms.
- **Session runtime driver seam** ([#3306](https://github.com/nanocoai/nanoclaw/pull/3306)) and its consumption ([#3307](https://github.com/nanocoai/nanoclaw/pull/3307)) are the architectural driver for the next version. Dormant selection via `NANOCLAW_RUNTIME_DRIVER` with Docker built-in means the groundwork for alternative runtimes (maybe WASM, process-local, remote) is laid, though not yet active.
- **Group/folder data-loss guards** ([#3308](https://github.com/nanocoai/nanoclaw/pull/3308)) — a safety hardening feature refusing to create groups over pre-existing folders. Likely to land next version.
- **Codex dependency pin bump** ([#3299](https://github.com/nanocoai/nanoclaw/pull/3299)) is time-sensitive (GPT-5.4 retire 2026-08-31) — expect this merged urgently, likely in a patch release.

## 7. User Feedback Summary

- **Pain — Task logs lost in chat sessions**: glifocat reports that tasks firing in chat sessions lose run logs, replies get eaten, and series are unlisted — a clear functional regression from 2.1.48's one-door task delivery. Two issues (log loss; unbounded polling) filed within 24 hours of each other by the same user, each paired with a ready fix PR — indicating responsive, clear bug reports from active users.
- **Pain — Codex-generated images dropped**: mshirel reports generated images are silently dropped because nothing consumes the `file` event — users may have been losing artifacts without realizing it.
- **Satisfaction signal — Contributor velocity**: The volume of community-contributed PRs touching source code (formatter escaping fix, codex pin bump, webchat implementations) indicates a healthy, approachable codebase for external contributors.
- **Satisfaction signal — Responsiveness**: The docs issue #1143 from March was finally closed (dated 2026-08-17 update), indicating maintainers are sweeping stale documentation debt even when community upvotes are zero.

## 8. Backlog Watch

- **Issue #1143** (closed today after 5 months, 2 comments, 0 upvotes) — an example of a long-dormant docs issue getting triage closure; now resolved.
- **Issue #3203** — codex provider typecheck failure, filed 2026-08-08, has only 1 comment and no fix PR in the pipeline 10 days later. The underlying silent dropping of generated images is a visible functionality break for anyone using `/add-codex`. This needs maintainer attention; the PR bumping the codex pin (#3299) may partially address it if the event type mismatch is resolved by the dependency update, but no explicit link is noted.
- **PR #3300** (escaping fix) and **PR #3299** (codex pin bump) — both community-filed with clear, surgical scope. They are small and straightforward; prompt review would reinforce contributor trust.
- **The 16 open PRs** (mostly core-team channel-wave stacked PRs like #3307, #3308, #3306) represent a large pending review load on top of ongoing merge activity. While this reflects an active development sprint rather than neglect, the stacked PR structure can stall if the base PR (#3306) is not merged promptly.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for **2026-08-18**.

---

# NullClaw Project Digest — 2026-08-18

## 1. Today's Overview
NullClaw is currently in a low-activity maintenance phase. Over the last 24 hours, there were zero issue updates and no new releases, indicating a quiet period for the core repository. The only activity was a single automated dependency update pull request from Dependabot, which remains open. With no user-reported issues or merged pull requests, developer focus appears to be on incremental housekeeping rather than feature development. Overall, the project is healthy but currently lacks the momentum of active community contributions.

## 2. Releases
No new releases were published for NullClaw in the last 24 hours. The latest release remains unchanged.

## 3. Project Progress
There were no merged or closed pull requests in the last 24 hours. The only update was to an existing dependency PR, which remains open. No new features, bug fixes, or documentation updates were advanced to the codebase during this period.

## 4. Community Hot Topics
- **[PR #956] [dependencies, docker] ci(deps): bump alpine from 3.23 to 3.24** ([link](https://github.com/nullclaw/nullclaw/pull/956))  
  This is the only active item, created by Dependabot. It proposes updating the base Docker image from Alpine 3.23 to 3.24 to address potential security and compatibility issues. There are no comments or reactions yet, but the underlying need is ensuring the container runtime is current with upstream Alpine patches and maintaining dependency hygiene. This PR has been open since June, suggesting low urgency or maintenance prioritization.

## 5. Bugs & Stability
No new bugs, crashes, or regressions were reported in the last 24 hours. There are no open issues indicating system instability. The project appears stable; however, the lack of recent testing or user feedback makes it difficult to assess real-world performance metrics.

## 6. Feature Requests & Roadmap Signals
No feature requests were submitted or updated in the last 24 hours. The only roadmap signal is the pending Alpine 3.24 upgrade, which is a technical dependency update rather than a user-facing feature. Without issue traffic or requested enhancements, there are no strong signals suggesting which features might appear in the next version.

## 7. User Feedback Summary
There is no user feedback, bug reports, or usage discussions recorded in the last 24 hours. The absence of both complaints and praise suggests that users are not facing immediate pain points, or that they are gathering around the project's documentation and release channels rather than the GitHub issue tracker. The lack of active user interaction makes it difficult to gauge satisfaction levels.

## 8. Backlog Watch
- **[PR #956] Alpine Image Version Bump** ([link](https://github.com/nullclaw/nullclaw/pull/956))  
  This dependency upgrade has been open since **June 15, 2026** (over two months) without review or comments. While this is a routine Dependabot change, the extended unresolved timeline could indicate a maintainer backlog or a deliberate hold. Given the nature of the change (base image security and patch level), maintainers should review this PR soon to prevent the container images from drifting too far from upstream Alpine support. If intentional, the PR should be closed for clarity.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-18

## 1. Today's Overview

IronClaw is in a period of **high-intensity engineering activity** focused on **database write-pressure reduction** (epic #7591), **notification infrastructure generalization**, and **stabilization after the v1.3.0-rc.1 release**. 44 PRs and 28 issues were updated in the last 24 hours, with a healthy mix of open work (22 issues, 28 PRs) and closed/merged items (6 issues, 16 PRs). The project shows strong momentum around a **multi-tier performance optimization initiative**, with a dedicated epic tracking estimated savings of ~60-70% in durable DB writes per turn. A **daily failure taxonomy report** (#7704) indicates an ongoing, systematic approach to quality — with a critical libSQL write-lane starvation bug (#7714) identified and a fix PR already opened. The release of v1.3.0-rc.1 signals feature-complete status for the 1.3 line, while several large PRs (Google Docs semantic editing, run-now automations, WASM response normalization) are close to landing.

## 2. Releases

**ironclaw-v1.3.0-rc.1** — released 2026-08-17, tagged `1.3.0-rc.1`.

- Build/install tags: `ironclaw-v1.3.0-rc.1`
- Install via shell script (`curl ... | sh`) or PowerShell script (both available via GitHub Releases)
- **Note:** Release notes were empty in the data; no breaking changes or migration notes were documented.

Given the scale of the write-pressure epic (#7591) and related fixes merged in recent days, the 1.3.0 GA will likely include the multi-tier write-reduction work and the notification inbox overhaul.

## 3. Project Progress

**Merged/Closed PRs (16 total in 24h):** Notable closures include:

- **#7663** — `fix(release): forward-port 1.2 fixes and thread repair` — Windows filesystem/release-smoke reliability, clean Windows JSON output, runtime `curl` healthchecks, and 1.2.0 metadata stability backported to main. *Addressed release-blocking Windows issues.*
- **#7710** — `fix(slack): address multi-agent review findings on #7682` — 7 WebUI connect-link landing hardening findings resolved; also added Slack message timestamp handling. *Closes the loop on the Slack privacy fix.*
- **#7703** — `feat(wasm): typed WIT tool response and bundled guest migration` — Superseded by #7711 (folded in); a 0.3.0 compatibility shim was deliberately **not** shipped to avoid add-then-remove churn.

**Closed Issues (6 total):** Most notably:

- **#7598** `[Tier 2] Collapse capability invocation-state writes to gate/terminal edges` — closed; this was the largest single win (−40 rows/turn) in the write-pressure epic, now implemented.
- **#7594** `[Tier 1] Route loop milestone sink through CoalescingEventSink` — closed; pure-waste reduction (~30 pool checkouts/turn off the critical path).
- **#7637** — TypeScript types added to design-system component boundaries.
- **#7647** — Deterministic no-delivery outcome for scheduled automations (feat).

**Key Open PRs advancing major features:**

- **#7718** — Google Docs semantic editing tools (4 new capabilities: structured inspection, anchored batch edits, populated tables, deterministic verification); legacy tools preserved.
- **#7708** — "Run-now" for automations across trigger domain + WebUI (atomic manual-fire, domain-separated identity).
- **#7491** — OMP core-tool contract (`read`, `write`, `edit`, `glob`, `grep`, `bash`) + engines + benchmark arm; removes old mixed tool surface.

## 4. Community Hot Topics

The most active discussions (by comment count) center on **database performance and correctness under load**:

- **#7275** (4 comments, closed) — "[CLOSED] Reborn: verify explicit persistent memory recall across conversations in production" — a customer-facing bug about memory recall gaps; now closed, presumably verified/fixed. Signals that **cross-conversation memory reliability** is a key user expectation.
- **#7591** (3 comments) — "Epic: reduce durable DB write pressure ~60% while keeping multi-worker safety" — the central epic driving most current engineering effort; four parallel code audits were performed to find the gaps.
- **#7701** (2 comments) — Tier 2 gap found *after* epic creation: reserve+reconcile collapse (22→11 rows/turn). Shows the epic is being actively refined as reviewers find new savings.
- **#3762** (2 comments) — Long-standing issue: editing `AGENTS.md` in web UI does not update system prompt. Still open since May; customer-impacting; planned for v1.4.0.

**Underlying needs:** The DB write-pressure work is about **scalability and cost** — approaching production limits on durable store throughput. The memory-recall issue (#7275) and AGENTS.md issue (#3762) both reflect **users wanting their configuration and context to actually stick** — persistent, reliable behavior across sessions.

## 5. Bugs & Stability

Bugs reported/active today, ranked by severity:

**High:**
- **#7714** — `libSQL: single shared write connection starves the resource-governor journal under bench load` — During PinchBench (147 tasks), the governor's delta journal stalled ~40s waiting for a write connection, causing cascading authority invalidations, journal replacements, permanent reservation leaks, and mislabeled `process in ...` failures. **Fix PR exists: #7717** — stops write-lane starvation from cascading through the resource governor. *Mitigation in progress.*

**Medium:**
- **#7705** — Follow-ups from #7631: unbounded shutdown flush and latching `pending_flush_error` in `CoalescingEventSink` — shutdown can hang on a wedged event backend; error state latches, potentially causing silent data loss. No fix PR yet.

**Low/QA:**
- **#7716** — Add MCP server flow missing bearer key auth and STDIO/HTTP transport options (bug_bash_P2).
- **#7715** — Telegram connection flow lacks consent/selection between bot and personal account (bug_bash_P2).

**Regression watch:** #7704 (daily failure taxonomy) identifies the storage write-lane contention as the **largest fixable ironclaw defect** in the clawbench suite (84 non-pass runs, split three ways). This aligns with #7714's root cause.

## 6. Feature Requests & Roadmap Signals

**Likely in v1.3.0/1.4.0:**

- **Notifications inbox overhaul** (epic #7687 + #7688, #7689, #7690, #7691): durable user-scoped inbox replacing the automation-approval-only center. Covers approvals, auth-required, blocked runs, run failures/completions, delivery failures. High-value UX improvement, currently in active implementation (2 PRs open).
- **Run-now for automations** (#7708): manual-fire path preserving schedule + domain-separated provenance. Strongly requested by automation users.
- **GitHub Projects v2 field manipulation** (#7719, opened today): IronClaw can update labels but not Projects v2 fields (e.g., `Main backlog priority`). This blocked an internal workflow — likely to ship soon.

**Signals for later:**

- **Native structured output finalization** (#7693): provider-neutral immutable output contract for turn/run context; enables deterministic downstream processing.
- **Durable backend suggestions** (#7694): product-surface-neutral `suggestions.list/generate/start/dismiss`; WebUI as one transport adapter.

## 7. User Feedback Summary

- **Cross-conversation memory reliability** (#7275, closed): Users expect explicit facts established in one conversation to be recalled later; this was broken in production and is now verified fixed (reborn initiative).
- **Slack privacy issue** (#7681, #7682): Users without linked accounts get a **public** "connect" nudge in shared channels — a clear privacy violation; the fix (private DM + one-click connect link) is in review.
- **AGENTS.md not propagating** (#3762): Editing identity files in WebUI does not affect system prompts — a core configuration reliability issue that has been open for 3 months and is planned for v1.4.0.
- **GitHub Projects v2 integration gap** (#7719): Users cannot manage Projects v2 priority fields through IronClaw, blocking internal triage workflows.
- **MCP server setup limitations** (#7716): Missing bearer-key auth and transport options in the Add MCP server flow — significant for enterprise users who need token-authenticated servers.
- **Telegram connection ambiguity** (#7715): Users connecting a bot vs. personal account are not asked which mode they intend — confusing and potentially privacy-relevant.

## 8. Backlog Watch

- **#3762** — `[suggested_P1, customer, v1.4.0]` Editing AGENTS.md in the web UI does not update the system prompt — **Open since 2026-05-18 (3 months)**, 2 comments. Customer-impacting, no PR yet. Planned for 1.4.0 but track it.
- **#7184** — Nostr host functions for WASM tools (reborn) — Open since 2026-08-04, no comments since creation. Contributor: `Kampouse` (new). May need maintainer help to get across the line.
- **#7513** — ACP serve command (`--acp --stdio`) — Open, contributor: new. Valuable for interoperability (Copilot CLI, VS Code); no recent traction.
- **#7406** — Dependabot bump of 4 GitHub Actions — open since 2026-08-09; low priority but should be merged to keep CI current.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-18

## 1. Today's Overview

LobsterAI shows moderate to high activity today with **21 PRs updated** in the last 24 hours — a substantial number indicating an active development cycle. Notably, **17 PRs were merged or closed** (81% closure rate), suggesting healthy merge velocity and maintainer responsiveness. A significant portion of today's merged PRs (#1636–#1642, #1661–#1669, #1675) came from a batch of feature and fix submissions originally created in April, apparently cleared in a maintenance sweep. On the issue side, **7 issues were updated**, with **6 flagged as `[stale]`** and no new issues filed today (the only non-stale issue is #2500, a project announcement from an external project). **No new releases** were published. The development focus visible today centers on **runtime integration (dsh engine, OrcaRouter provider)**, **Electron UX polish (context menus, modal behavior)**, **internationalization fixes**, and **agent workspace configuration**.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains **v4.8**, which is still referenced in user bug reports (e.g., Issue #1643 mentions "4.8版本, win11" behavior).

## 3. Project Progress

**17 PRs merged/closed today**, representing several distinct workstreams:

**Runtime & Engine Integration:**
- [#2505](https://github.com/netease-youdao/LobsterAI/pull/2505) — **feat: dsh process launcher** (renderer + main) — new DeepSeek Harness process launch capability
- [#2502](https://github.com/netease-youdao/LobsterAI/pull/2502) — **feat: dsh engine integration** (renderer, build, main, macOS) — cross-stack engine integration
- [#1663](https://github.com/netease-youdao/LobsterAI/pull/1663) — **feat(openclaw): upgrade OpenClaw to v2026.4.12** — also upgrades openclaw-weixin plugin from 1.0.3 to 2.1.8 (fixing `resolvePreferredOpenClawTmpDir is not a function` error) and removes deprecated `skipMissedJobs` config key

**Agent Management & Workspace:**
- [#1668](https://github.com/netease-youdao/LobsterAI/pull/1668) — **feat(agent): per-agent working directory configuration** — SQLite migration adds `working_directory` column; falls back to OpenClaw default `{STATE_DIR}/workspace-{agentId}/` when unset

**UX & Interaction Improvements (from 0xFLX batch):**
- [#1636](https://github.com/netease-youdao/LobsterAI/pull/1636) — **feat(cowork): floating "scroll to bottom" button** in chat window
- [#1637](https://github.com/netease-youdao/LobsterAI/pull/1637) — **feat(cowork): "regenerate" button** for AI replies
- [#1640](https://github.com/netease-youdao/LobsterAI/pull/1640) — **feat(tool-result): one-click copy buttons** for tool execution results (Bash terminal, Diff view, standard tools)
- [#1641](https://github.com/netease-youdao/LobsterAI/pull/1641) — **feat(modal): unified Esc key close** for all modals
- [#1639](https://github.com/netease-youdao/LobsterAI/pull/1639) — **fix(i18n): hardcoded English tooltips internationalized** across WindowTitleBar, SkillsButton, Schema components

**Electron & Platform Fixes:**
- [#2503](https://github.com/netease-youdao/LobsterAI/pull/2503) — **fix(electron): edit context menu** (Cut/Copy/Paste/Select All) for text inputs in main window
- [#1642](https://github.com/netease-youdao/LobsterAI/pull/1642) — **feat: Windows right-click context menu** (registered via `HKCU\Software\Classes\Directory\shell\LobsterAI`, with `--open-directory` handling)
- [#2501](https://github.com/netease-youdao/LobsterAI/pull/2501) — **fix(skills): portal upgrade progress overlay** — renders through `document.body` so it covers the full app shell; adds focused renderer logs

**Other Fixes:**
- [#1661](https://github.com/netease-youdao/LobsterAI/pull/1661) — **fix(log): sensitive data redaction in exported logs** (API keys, Bearer/OAuth tokens, request/response bodies)
- [#1667](https://github.com/netease-youdao/LobsterAI/pull/1667) — **fix(Settings): Qwen console link migrated from DashScope 灵积 to Bailian 百炼** (zero behavioral change)
- [#1669](https://github.com/netease-youdao/LobsterAI/pull/1669) — **feat: settings page model provider UX fixes** (test-connection button disable logic, custom provider display name)
- [#1675](https://github.com/netease-youdao/LobsterAI/pull/1675) — **feat(cowork): session list grouped by time periods** (置顶 → 今天 → 昨天 → 7天内 → 30天内 → 更早按月)

**Still Open PRs (4):**
- [#2506](https://github.com/netease-youdao/LobsterAI/pull/2506) — docs for dsh runtime setup
- [#2504](https://github.com/netease-youdao/LobsterAI/pull/2504) — **feat: OrcaRouter provider integration** (Anthropic/OpenAI-compatible LLM gateway, mirrors OpenRouter wiring)
- [#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — dependabot electron group bump (electron 40.2.1 → 43.4.0)
- [#1660](https://github.com/netease-youdao/LobsterAI/pull/1660) — **feat(cowork): non-main agent welcome area shows agent name/description**

## 4. Community Hot Topics

The most actively discussed items today:

- **[Issue #2500 — VOKO: A2A Cross-Platform Communication Layer](https://github.com/netease-youdao/LobsterAI/issues/2500)** — *New, 1 comment*
  The only non-stale issue updated today. An external open-source project author (VOKO) posted a self-introduction proposing cross-agent communication standards. This signals growing community interest in **agent-to-agent interoperability** and ecosystem collaboration. Worth monitoring as it touches on A2A standardization trends.

- **[Issue #1653 — groupPolicy keeps being overwritten to allowlist](https://github.com/netease-youdao/LobsterAI/issues/1653)** — *2 comments, stale*
  Recurring configuration persistence bug — user reports `groupPolicy` gets silently overwritten every few minutes. The 2 comments suggest some maintainer investigation occurred; issue remains open since April 13.

- **[PR #1660 — Non-main agent welcome area](https://github.com/netease-youdao/LobsterAI/pull/1660)** — *Open, 4 months old*
  Despite being opened in April, this PR is still open and demonstrates ongoing community interest in **personalizing non-main agent experiences** (showing agent name/description in welcome area).

- **[Issue #1644 — MD-based workflows for multi-agent orchestration](https://github.com/netease-youdao/LobsterAI/issues/1644)** — *1 comment, stale*
  Feature request for main agent to orchestrate other agents via markdown workflows, with detailed transcript showing main agent's inability to perceive sibling agents. This addresses a core multi-agent coordination gap.

**Analysis:** The pattern of April-era issues and PRs being surfaced as "updated" today suggests either a maintainer sweep (closing stale items) or automated stale-bot activity. The community's underlying need clusters around: **multi-agent orchestration** (#1644, #1660, #2500), **configuration persistence reliability** (#1653), and **external model/runtime compatibility** (#1635, #1662).

## 5. Bugs & Stability

Ranked by severity:

1. **[High] Ollama local models fail to work** — [Issue #1635](https://github.com/netease-youdao/LobsterAI/issues/1635)
   Users report qwen3 through gemma4 models all fail, while the same models work in CherryStudio (including MCP calls). This blocks users with local-model setups. No fix PR referenced.

2. **[High] Non-SSE MCP engines unusable** — [Issue #1662](https://github.com/netease-youdao/LobsterAI/issues/1662)
   Only SSE-based MCP servers work; other MCP transports can't be discovered/used. No fix PR referenced.

3. **[Medium] groupPolicy auto-overwritten** — [Issue #1653](https://github.com/netease-youdao/LobsterAI/issues/1653)
   Configuration is silently reset to `allowlist` periodically. No fix PR referenced.

4. **[Medium] Scheduled task save validation error** — [Issue #1643](https://github.com/netease-youdao/LobsterAI/issues/1643)
   Saving a scheduled task shows "还有内容未保存" error, despite the task being saved successfully. UX bug, not data-loss.

5. **[Medium] MD→Word conversion incomplete with SSE "finish reason: full"** — [Issue #1671](https://github.com/netease-youdao/LobsterAI/issues/1671)
   Large document conversions truncate when the SSE stream terminates. Related to context/window limits.

6. **[Low] Sensitive data in exported logs (FIXED)** — [PR #1661](https://github.com/netease-youdao/LobsterAI/pull/1661) merged today addresses plaintext API keys in logs. Good proactive security fix.

**Assessment:** The Ollama and non-SSE MCP issues (both from April, still open) represent the most impactful unresolved stability concerns. The log redaction fix shows the team is actively addressing security hygiene.

## 6. Feature Requests & Roadmap Signals

Strong signals from merged PRs and issues:

1. **Multi-agent orchestration** — [Issue #1644](https://github.com/netease-youdao/LobsterAI/issues/1644) requests markdown-defined workflows where the main agent can organize other agents for complex tasks. The user transcript shows main agent can't even see sibling agents. Combined with the merged per-agent workspace feature ([#1668](https://github.com/netease-youdao/LobsterAI/pull/1668)) and the open PR for personalized agent welcome areas ([#1660](https://github.com/netease-youdao/LobsterAI/pull/1660)), there's a clear roadmap push toward **richer agent independence and coordination**.

2. **Provider ecosystem expansion** — Open PR [#2504](https://github.com/netease-youdao/LobsterAI/pull/2504) adds OrcaRouter as a first-class provider (Anthropic/OpenAI-compatible gateway). Combined with today's dsh engine integration work, LobsterAI is aggressively expanding its LLM runtime compatibility.

3. **DeepSeek Harness (dsh) engine** — Three PRs today (#2502, #2505, #2506) introduce dsh as a new runtime engine. This is a significant architectural addition worth watching.

4. **Cross-platform A2A communication** — [Issue #2500](https://github.com/netease-youdao/LobsterAI/issues/2500) from VOKO project proposes a standardized cross-platform comms layer for AI agents. While this is an external pitch, the maintainers' response could signal openness to A2A standards.

**Prediction:** Next minor version will likely include the dsh engine integration, OrcaRouter provider, per-agent working directories, and the batch of UX improvements (regenerate button, scroll-to-bottom, Esc-close modals, session grouping).

## 7. User Feedback Summary

- **Local model frustration**: Multiple users ([#1635](https://github.com/netease-youdao/LobsterAI/issues/1635)) report that Ollama local models are completely broken, despite working fine in other clients. This undermines trust for privacy-conscious users who prefer local inference.

- **Configuration reliability concerns**: The recurring groupPolicy overwrite issue ([#1653](https://github.com/netease-youdao/LobsterAI/issues/1653)) suggests configuration persistence is fragile, a serious concern for power users.

- **Tool/MCP compatibility gaps**: Non-SSE MCP support missing ([#1662](https://github.com/netease-youdao/LobsterAI/issues/1662)) limits interoperability with the broader MCP ecosystem.

- **Positive UX signals**: The merged batch of UX improvements (copy buttons, regenerate, scroll-to-bottom, Esc-close, i18n fixes) addresses common usability complaints effectively. The community clearly values these refinements — they were requested and delivered.

- **Multi-agent feature demand**: Users actively want their agents to collaborate ([#1644](https://github.com/netease-youdao/LobsterAI/issues/1644)), suggesting current single-agent-per-conversation isolation is a limitation.

## 8. Backlog Watch

**Issues needing attention (all from April, still open):**

1. **[#1635](https://github.com/netease-youdao/LobsterAI/issues/1635) — Ollama local models broken** (4+ months, 1 comment, stale)
   High-impact blocker for local-model users. Unclear if maintainers reproduced; no linked PR.

2. **[#1662](https://github.com/netease-youdao/LobsterAI/issues/1662) — Non-SSE MCP unusable** (4+ months, 1 comment, stale)
   Limits MCP ecosystem compatibility. Moderate impact, no visible progress.

3. **[#1644](https://github.com/netease-youdao/LobsterAI/issues/1644) — MD-based multi-agent workflows** (4+ months, 1 comment, stale)
   Roadmap-relevant feature request. The detailed transcript and use case make this a valuable spec for the multi-agent direction.

4. **[#1653](https://github.com/netease-youdao/LobsterAI/issues/1653) — groupPolicy overwrite bug** (4+ months, 2 comments, stale)
   Configuration reliability issue. The 2 comments indicate some investigation, but no resolution path visible.

**PRs needing review:**

5. **[#1277](https://github.com/netease-youdao/LobsterAI/pull/1277) — Electron 43.4.0 bump (dependabot)** (4+ months open)
   Major version bump across major/minor (40→43). Long-dormant; likely manual verification needed.

6. **[#1660](https://github.com/netease-youdao/LobsterAI/pull/1660) — Non-main agent welcome area** (4+ months open)
   Small, well-scoped feature aligned with multi-agent roadmap direction. Should be merged or explicitly closed.

---

*Digest generated for 2026-08-18. Data source: LobsterAI GitHub repository (github.com/netease-youdao/LobsterAI).*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-18

## 1. Today's Overview

Moltis saw a burst of activity over the last 24 hours, with **9 pull requests touched** (3 still open) and **3 issues updated** (2 now closed). The project is clearly in a **high-velocity development phase**, with core infrastructure fixes landing alongside new feature work. Notably, two of the three open PRs are authored by a single contributor (Lstarsky0) addressing cron and heartbeat configuration correctness — a strong signal that the project's scheduling and agent-control planes are being actively hardened. While no new releases were cut, the volume and quality of merged PRs suggest a significant release may be imminent. Overall project health appears strong: CI gates are being enforced (one failing format check was caught and fixed), dependency updates are flowing, and the maintainer team is responsive.

## 2. Releases

No new releases were published in the last 24 hours. The project remains on its previous release, despite the unusually high volume of merged PRs — a signal that the maintainers may be consolidating changes for a larger version bump.

## 3. Project Progress

Six PRs were merged or closed in the last 24 hours, representing a mix of feature work, bug fixes, and maintenance:

- **External agent model/effort selection ([#1125](https://github.com/moltis-org/moltis/pull/1125))** — Merged after a 2-month journey. This adds first-class `models` and `efforts` configuration for external-agent providers, integrates them into the `/model` command with grouping under `external-agent/<kind>`, and persists model/effort metadata. This is a substantial UX improvement for users juggling multiple agent providers.
- **Shadow DOM piercing for browser automation ([#1103](https://github.com/moltis-org/moltis/pull/1103))** — Merged; this completes a long-running effort to make browser snapshot and ref-based lookups traverse shadow DOM boundaries efficiently. The PR carries review fixes on top of the original #1100 work, indicating careful engineering review.
- **MiniMax Code ACP agent support ([#1204](https://github.com/moltis-org/moltis/pull/1204))** — Merged. Adds a named `acp-minimax-code` external-agent kind backed by `mcode acp`, includes it in default executable detection and agent registry, and documents both automatic discovery and manual TOML configuration.
- **Configurable WebUI RPC timeout ([#1130](https://github.com/moltis-org/moltis/pull/1130))** — Merged. Resolves issue #1127, allowing users to tune the WebUI RPC timeout — a quality-of-life fix for slow network environments.
- **Dependency bumps ([#1207](https://github.com/moltis-org/moltis/pull/1207), [#1087](https://github.com/moltis-org/moltis/pull/1087))** — Two cargo dependency groups updated: `wasmtime-wasi`, `cmov`, `quinn-proto`, `serde_with` (4 updates) and `tar` 0.4.45→0.4.46.

## 4. Community Hot Topics

The most active item this week is the **Podman integration bug ([#1095](https://github.com/moltis-org/moltis/issues/1095))**, which has 2 comments and remains open after 2.5 months. The issue was updated just yesterday, suggesting continued user interest and possibly maintainer investigation. The underlying need is clear: users want Moltis to work seamlessly with Podman as a container runtime, and this issue represents a real deployment blocker for container-first users who avoid Docker licensing.

The **heartbeat config handling PR ([#1209](https://github.com/moltis-org/moltis/pull/1209))** is generating attention as it fixes a subtle but serious bug where `heartbeat.update` parameters were treated as a full config replacement rather than a patch — meaning every omitted key reverted to defaults. This kind of issue resonates with users who have complex configurations. The companion PR ([#1208](https://github.com/moltis-org/moltis/pull/1208)) fixing `active_hours` being completely ignored is similarly impactful.

## 5. Bugs & Stability

Three bugs or stability concerns are in play:

- **Podman not working ([#1095](https://github.com/moltis-org/moltis/issues/1095))** — **High severity category**: a core integration broken. Open for 2.5 months with no fix PR visible. This is the most significant unresolved bug.
- **CI format gate failure on main ([#1202](https://github.com/moltis-org/moltis/issues/1202))** — **Medium severity**: two files exceeded the 1500-line limit (`memory-zvec/src/store.rs` at 1799 lines, `gateway/src/methods/services/admin.rs` at 1531). This was caught by CI, not users, and is already resolved (issue closed). Good sign for CI enforcement.
- **Heartbeat misconfiguration bugs ([#1187](https://github.com/moltis-org/moltis/issues/1187) via PR [#1209](https://github.com/moltis-org/moltis/pull/1209) and [#1205](https://github.com/moltis-org/moltis/issues/1205) via PR [#1208](https://github.com/moltis-org/moltis/pull/1208))** — **Medium severity**: both tied to the same feature area, with fix PRs open and active. The bugs caused silent config corruption (defaults overwriting user settings) and completely ignored active-hour constraints.

## 6. Feature Requests & Roadmap Signals

Two feature-request signals are worth tracking:

- **Configurable RPC timeout ([#1127](https://github.com/moltis-org/moltis/issues/1127))** — Now **resolved** via merged PR #1130. Users on unreliable networks can tune timeouts. Watch for follow-up requests for per-endpoint timeouts rather than a single global setting.
- **Podman support ([#1095](https://github.com/moltis-org/moltis/issues/1095))** — Originally filed as a bug, this doubles as an implicit feature request for container runtime parity. Given the continued attention, expect a maintainer to prioritize this in the next 1–2 release cycles.

Looking ahead, the **managed Files library (PR [#1206](https://github.com/moltis-org/moltis/pull/1206), open)** is the strongest roadmap signal. It adds a persistent, data-directory-backed Files library with authenticated streaming APIs and a Finder-style Settings browser, plus `MOLTIS_FILES_DIR` discovery and read-only-by-default mounts across Docker, Podman, and Apple Containers. This suggests file management and cross-runtime mount parity are on the roadmap.

## 7. User Feedback Summary

Users are actively engaging with Moltis's extensibility story:

- **Positive signals**: The MiniMax Code ACP agent addition and the external-agent model/effort selection both landed quickly once opened, showing the maintainers are responsive to agent-provider breadth requests.
- **Pain points**: The Podman issue ([#1095](https://github.com/moltis-org/moltis/issues/1095)) is a persistent frustration — it has survived 2.5 months without a fix, spanning multiple releases. Users who are Podman-first are effectively blocked from running Moltis in their preferred environment.
- **Satisfaction markers**: The heartbeat bugs (#1187, #1205) were discovered by users and produced open PRs within 24 hours — a fast turnaround that demonstrates a healthy feedback-to-fix loop.
- **Adoption signals**: No negative comments about breaking changes in the dependency bumps, no user complaints on CI gate strictness.

## 8. Backlog Watch

The following items need maintainer attention:

- **Podman integration bug ([#1095](https://github.com/moltis-org/moltis/issues/1095))** — Open since June 3 (76 days), bumped yesterday, no linked PR. This is the oldest unresolved issue among active items and now the most visible backlog risk. A maintainer triage comment or a workaround would materially improve user trust.
- **Open PR: Heartbeat update-as-patch ([#1209](https://github.com/moltis-org/moltis/pull/1209))** — New (Aug 17), addresses a bug that silently corrupts user configs. Should be prioritized for merge to prevent further user-facing data loss.
- **Open PR: Active-hours enforcement ([#1208](https://github.com/moltis-org/moltis/pull/1208))** — New, companion to #1209. The two could be merged together to keep the heartbeat subsystem consistent.
- **Open PR: Managed Files library ([#1206](https://github.com/moltis-org/moltis/pull/1206))** — Large surface area (new APIs, persistent storage, mounts across three container runtimes). Requires careful security review (file upload/download/move/delete) before merge; flagging for maintainer review bandwidth planning.

---

*Data window: 2026-08-17 → 2026-08-18. Source: github.com/moltis-org/moltis.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest
**Date: 2026-08-18**

---

## 1. Today's Overview

CoPaw (QwenPaw) is in a highly active development phase, with a substantial volume of bug fixes compared to feature work. The project saw 35 PRs updated (22 merged/closed) and 14 issues updated (6 closed) in the last 24 hours, reflecting solid momentum. The recent v2.1.0 release has triggered a wave of user-reported bugs including tool-call crashes, media URL handling issues, and session-related defects. Work is concentrated on stabilizing the 2.1.0 release while community contributors are actively submitting feature integrations like the AnySearch web search provider and PowerContext memory backend. The repository has a healthy ecosystem with 10+ distinct contributors active, including first-time contributors.

---

## 2. Releases

No new releases were published in the last 24 hours. The latest available version is **v2.1.0** (post-2.0), which has been the subject of most reported issues.

---

## 3. Project Progress

**22 PRs merged/closed today** (top items):

- **[PR #7083](https://github.com/agentscope-ai/QwenPaw/pull/7083)** (merged): Compact background task list in Console UI with scroll hint — caps visible list height to prevent input area displacement.
- **[PR #7017](https://github.com/agentscope-ai/QwenPaw/pull/7017)** (merged): PawApps open without page reload; reload only when updating an already-installed app so the new bundle takes effect.
- **[PR #5151](https://github.com/agentscope-ai/QwenPaw/pull/5151)** (merged, longstanding PR from June): Fixed GitPanel tab styles — root cause was `ant-` prefix selectors conflicting with the `qwenpaw` prefixCls in ConfigProvider.
- **[PR #7036](https://github.com/agentscope-ai/QwenPaw/pull/7036)** (merged): Unified media download controls with audio download button placed in player bar, matching keyboard focus order.
- **[PR #6975](https://github.com/agentscope-ai/QwenPaw/pull/6975)** (merged): Context-usage ring now updates after `/compact` — trailing SSE events were being discarded before flush.
- **[PR #6981](https://github.com/agentscope-ai/QwenPaw/pull/6981)** (merged): Removed `/approve` and `/deny` command hints from chat input placeholders across all 7 locale files.
- **[PR #6968](https://github.com/agentscope-ai/QwenPaw/pull/6968)** (merged): Fixed token-usage inflation — image base64 was being counted as text tokens (~700k tokens for a 2MB photo), making progress ring show ~100% after two images.
- **[PR #6940](https://github.com/agentscope-ai/QwenPaw/pull/6940)** (merged): Added native DataPaw app runtime with durable analysis workspace.
- **[PR #6817](https://github.com/agentscope-ai/QwenPaw/pull/6817)** (closed): AnySearch web search integration (superseded by updated PR #7081).
- **[PR #7089](https://github.com/agentscope-ai/QwenPaw/pull/7089)** (open/related): Standalone version-driven release pipeline for datapaw plugin — ensures proper CDN publishing.

---

## 4. Community Hot Topics

**Top activity clusters today:**

1. **[Issue #6405](https://github.com/agentscope-ai/QwenPaw/issues/6405)** (closed, 7 comments) — MCP tool "Tool not found" errors after upgrading to 2.0. Despite the tool name being correctly reformatted as `[mcp-key]__[tool_name]`, the runtime fails to resolve it. This was a significant community pain point for Docker users.

2. **[Issue #7011](https://github.com/agentscope-ai/QwenPaw/issues/7011)** (open, 6 comments) — Console stop request accidentally cancels an active Feishu session under multiple UI sessions. Identity values crossed between sessions, exposing a session isolation defect.

3. **[Issue #7085](https://github.com/agentscope-ai/QwenPaw/issues/7085)** (open, 3 comments) — Per-channel model configuration request. Users want different model selections per messaging channel (e.g., DingTalk → `gpt-4o`, WeChat → `qwen-max`, Console → local llama.cpp). Currently, model config is global or agent-level only.

4. **[Issue #7063](https://github.com/agentscope-ai/QwenPaw/issues/7063)** (closed, 3 comments) — Consistency crash when agent executes tool calls in v2.1.0. Root cause identified: `async for` iterating a coroutine instead of an async generator.

5. **[PR #6515](https://github.com/agentscope-ai/QwenPaw/pull/6515)** (open) — Volcengine Agent Plan and Xiaomi MiMo V2.5 API as built-in providers. High demand for Chinese cloud provider support.

**Underlying needs:** Community is split between users of global/enterprise messaging platforms (Feishu, DingTalk) and those running local model setups. MCP compatibility and provider diversity are the most pressing concerns.

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue | Summary | Fix PR |
|----------|-------|---------|--------|
| 🔴 Critical | [#7063](https://github.com/agentscope-ai/QwenPaw/issues/7063) | **Consistent crash on every tool call** — `async for` on a coroutine → `TypeError`. Blocks core agent functionality. | Closed as invalid (likely misreport or fixed) |
| 🔴 High | [#7088](https://github.com/agentscope-ai/QwenPaw/issues/7088) | **OneBot/QQ image URL expiry poisons sessions** — signed `rkey` URLs expire (~2h), LLM server-side download fails with HTTP 400, stale URLs break subsequent replies | [PR #7087](https://github.com/agentscope-ai/QwenPaw/pull/7087) — localize remote media URLs client-side |
| 🟠 Medium | [#7011](https://github.com/agentscope-ai/QwenPaw/issues/7011) | Console stop cancels active Feishu session due to crossed session identity | None yet |
| 🟠 Medium | [#7082](https://github.com/agentscope-ai/QwenPaw/issues/7082) | `_StructuredOutputDynamicClass` not fully defined — Pydantic error during agent/toolkit init in console | None |
| 🟡 Low | [#7084](https://github.com/agentscope-ai/QwenPaw/issues/7084) | When only one history conversation exists, clicking it after opening a new chat does nothing | None |
| 🟡 Low | [#7051](https://github.com/agentscope-ai/QwenPaw/issues/7051) | Image attachments lost after session reload — backend serves data URLs, frontend shows broken thumbnails | None |
| 🟡 Low | [#7077](https://github.com/agentscope-ai/QwenPaw/issues/7077) | Plugin runtime hooks silently lost after workspace reload (hot-install) | None |
| 🟢 Info | [#7048](https://github.com/agentscope-ai/QwenPaw/issues/7048) | `qwenpaw cron update` reports success but prompt isn't updated | Closed as invalid |
| 🟢 Info | [#7076](https://github.com/agentscope-ai/QwenPaw/issues/7076) | qwenpaw-creator LLM config returns 404 on v2.1.0 | None |

---

## 6. Feature Requests & Roadmap Signals

**Likely candidates for next release (v2.1.1 or v2.2):**

1. **[#7085](https://github.com/agentscope-ai/QwenPaw/issues/7085) — Per-channel model configuration**: Multi-channel users (DingTalk/WeChat/Console) need distinct model defaults. Given the volume of messaging channel usage in this project, this is a likely roadmap item.

2. **[#7081](https://github.com/agentscope-ai/QwenPaw/pull/7081) / [#6817](https://github.com/agentscope-ai/QwenPaw/pull/6817) — AnySearch integration**: A full-featured PR adding pluggable web search, built-in MCP client, and Console config with MCP env-ref header fixes. Submitted by an external company, this could be merged as an alternative to Tavily.

3. **[#7079](https://github.com/agentscope-ai/QwenPaw/issues/7079) / [#7080](https://github.com/agentscope-ai/QwenPaw/pull/7080) — PowerContext long-term memory**: A new backend implementing the existing `BaseMemoryManager` abstraction. Plug-and-play replacement for ReMeLight memory.

4. **[#6515](https://github.com/agentscope-ai/QwenPaw/pull/6515) — Volcengine Agent Plan + Xiaomi MiMo V2.5 providers**: Adding major Chinese API providers to built-in list.

5. **[#7075](https://github.com/agentscope-ai/QwenPaw/issues/7075) — Cron job run details**: Users want start time, duration, end time, and result visibility for scheduled tasks (currently only failure messages show).

6. **[#6925](https://github.com/agentscope-ai/QwenPaw/issues/6925) — Multi-agent collaboration in a single session window**: Currently each collaboration creates a new session; users want one unified conversation view.

---

## 7. User Feedback Summary

**Pain points (from issues today):**

- **MCP tool resolution was broken for Docker users post-2.0** — the most commented thread (#6405, 7 comments). Tool naming conventions changed but runtime resolution lagged.
- **Session isolation issues** are causing real-world interruptions: a Console UI stop canceled an active Feishu conversation (#7011), and stale QQ image URLs made agents unable to see message context (#7088).
- **Chinese users face configuration hurdles**: qwenpaw-creator 404 errors and unclear per-channel model configs.
- **Local model users want better integration** with `llama.cpp` and per-channel routing.

**Satisfaction signals:**

- UI improvements (compact task list, contextual ring fixes) merged quickly after community feedback.
- First-time contributors (haosong384, kic635, cyruszhang, anysearch-ai) submitting quality PRs suggest the project's contribution experience is good.

---

## 8. Backlog Watch

The following items appear to need maintainer attention:

| Item | Age | Why It Matters |
|------|-----|----------------|
| [PR #6302](https://github.com/agentscope-ai/QwenPaw/pull/6302) — Unify provider discovery, model metadata, routing | 28+ days | Large, cross-cutting refactor of provider system; if merged, would resolve many model-configuration issues but has been sitting open for 4 weeks |
| [PR #6515](https://github.com/agentscope-ai/QwenPaw/pull/6515) — Volcengine + Xiaomi providers | 21+ days | No comments logged; third-party PR awaiting review |
| [PR #6719](https://github.com/agentscope-ai/QwenPaw/pull/6719) — Persistent workspace artifact cards | 13+ days | Substantial feature for chat/file UI parity with WorkBuddy |
| [PR #6976](https://github.com/agentscope-ai/QwenPaw/pull/6976) — Session-scoped multi project directories | 5 days | Changes file-tool semantics; needs design sign-off |
| [PR #6986](https://github.com/agentscope-ai/QwenPaw/pull/6986) — Antivirus blocking sandbox fix | 5 days | Template description unfilled, unclear impact — requires author revision |

**No critical security issues or unacknowledged `security`-labelled items were observed in today's data, indicating a healthy maintenance posture overall.**

---

*Digest generated from GitHub activity data for 2026-08-18.*

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-18

## 1. Today's Overview

ZeroClaw is in a period of heavy RFC-driven architecture and security hardening, with 50 issues and 50 PRs updated in the last 24 hours. The project is actively executing on a substantial v0.9.0 security milestone, with multiple high-priority (p1) fixes merged around credential handling, channel download bounds, and action budget atomicity. Maintainer bandwidth appears fully engaged: 16 PRs were merged/closed, and at least 40% of open issues carry `status:accepted` RFC labels, indicating a project that is methodically ratifying and implementing its roadmap despite a large open-work queue. Community participation remains strong, with several multi-week RFC discussions (notably #6808, #8603) still drawing comments, and a notable emphasis on external ecosystem interoperability (OpenAI-compatible APIs, portable agent bundles).

## 2. Releases

No new releases were published in the last 24 hours. The most recent release activity is tracked via the v0.9.0 milestone, which encompasses the auth/security/gateway breaking-change queue (#7432).

## 3. Project Progress

The last 24 hours saw **16 merged/closed PRs**, with a strong emphasis on **security hardening and CI reliability**:

**Security fixes (priority p1):**
- [PR #9973](https://github.com/zeroclaw-labs/zeroclaw/pull/9973): Removed Gemini API keys from URLs, moving them to `x-goog-api-key` headers.
- [PR #10000](https://github.com/zeroclaw-labs/zeroclaw/pull/10000): Bounded QQ and Mattermost attachment downloads to prevent resource-exhaustion attacks.
- [PR #9996](https://github.com/zeroclaw-labs/zeroclaw/pull/9996): Made action budget accounting atomic, closing a race condition in parallel tool dispatch (fixes #9849).
- [PR #9993](https://github.com/zeroclaw-labs/zeroclaw/pull/9993): Stopped implicit local file reads in email attachments.
- [PR #9612](https://github.com/zeroclaw-labs/zeroclaw/pull/9612): Fixed WhatsApp Cloud approval token lifecycle to prevent orphaned credentials.
- [PR #9765](https://github.com/zeroclaw-labs/zeroclaw/pull/9765): SOP definitions now load from the shared workspace instead of `data_dir`.

**CI and test reliability:**
- [PR #10039](https://github.com/zeroclaw-labs/zeroclaw/pull/10039): Extracted a shared Clippy runner across workflows (fixes #7884).
- [PR #10043](https://github.com/zeroclaw-labs/zeroclaw/pull/10043): Removed duplicate architecture-test guards.
- [PR #10010](https://github.com/zeroclaw-labs/zeroclaw/pull/10010): Fixed an ETXTBSY race in the cron shell test.
- [PR #9398](https://github.com/zeroclaw-labs/zeroclaw/pull/9398): Added scheduled macOS and Windows test workflows.

**Feature work merged:**
- [PR #9547](https://github.com/zeroclaw-labs/zeroclaw/pull/9547): Upgraded CPAL to 0.18 for Voice Wake.

**Core fixes:**
- [PR #9544](https://github.com/zeroclaw-labs/zeroclaw/pull/9544): Delegated agents now honor configured provider fallbacks (fixes a significant reliability gap).

## 4. Community Hot Topics

- [#6808 — RFC: Work Lanes, Board Automation, and Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808) (23 comments) — A governance RFC ratified and rolling out. Signals maintainer intent to streamline the project's own workflow, likely a response to the overhead visible in the decision-tracker issue #8692.
- [#8603 — RFC: ZeroClaw Chat Completions profile](https://github.com/zeroclaw-labs/zeroclaw/issues/8603) (23 comments) — Proposes exposing an OpenAI-compatible API. This is a high-demand interoperability feature that would make ZeroClaw usable with a vast ecosystem of existing tools (Open WebUI, LangChain, etc.).
- [#8303 — RFC: Goal mode v1](https://github.com/zeroclaw-labs/zeroclaw/issues/8303) (22 comments) — Durably binding agent work to multi-turn user objectives. Addresses a core usability gap for complex tasks.
- [#7155 — RFC: Per-execution confirmation tier for shell commands](https://github.com/zeroclaw-labs/zeroclaw/issues/7155) (20 comments) — A Claude Code-style allow/ask/deny policy. Strong signal on user demand for fine-grained security control.
- [#9487 — RFC: Runtime-owned conversation sessions](https://github.com/zeroclaw-labs/zeroclaw/issues/9487) (19 comments) — A foundational architecture shift toward clearer session ownership.

**Underlying needs across these threads:** Users are asking for (1) enterprise-grade security granularity, (2) drop-in compatibility with existing AI tooling, and (3) more durable, goal-oriented agent behavior rather than single-turn interactions.

## 5. Bugs & Stability

**High severity (p1):**
- [Issue #10023](https://github.com/zeroclaw-labs/zeroclaw/issues/10023) — Failure logs claim the requested model, not the actual pinned fallback model, misleading operational debugging. Open, in-progress. No fix PR linked yet.
- [PR #9314 — Telegram long-poll offset bug](https://github.com/zeroclaw-labs/zeroclaw/pull/9314) — Open, p1. Fixes a data-loss issue where transient failures during processing permanently lost Telegram updates. Large PR (XL), needs maintainer review.

**Medium severity (p2):**
- [Issue #9594 — Coding-agent tools charge action budget twice](https://github.com/zeroclaw-labs/zeroclaw/issues/9594) — Closed. Fixed within the atomic action budget work (#9996).
- [Issue #9849 — RateLimitedTool non-atomic budget check](https://github.com/zeroclaw-labs/zeroclaw/issues/9849) — Closed. Fixed by PR #9996.
- [PR #10038 — Cron accepts invalid `session_target`](https://github.com/zeroclaw-labs/zeroclaw/pull/10038) — Open. Fixes a silent misconfiguration acceptance.

## 6. Feature Requests & Roadmap Signals

The following features, currently under active RFC discussion, are strong candidates for upcoming releases:

- **OpenAI-compatible Chat Completions API** (#8603) — Would unlock widespread ecosystem compatibility.
- **Agent export/import bundles** ([PR #9986](https://github.com/zeroclaw-labs/zeroclaw/pull/9986)) — A CLI feature to portably move agents between installs. Open, needs review.
- **Goal mode** (#8303) — Bounded, multi-turn foreground tasks.
- **Shell command confirmation policies** (#7155) — Allow/ask/deny patterns per command.
- **Pluggable auth and security pipeline** (#7141, #7142) — Core v0.9.0 features.
- **Hailo-Ollama native provider** ([PR #9109](https://github.com/zeroclaw-labs/zeroclaw/pull/9109)) — Edge/on-prem inference support.
- **ZeroCode Option-Backspace** ([Issue #10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059)) — Small macOS UX fix, labeled `good first issue`.

The volume and sophistication of the RFC backlog, combined with the formal decision tracker (#8692) and streamlined process RFC (#9496), suggest the project is maturing its governance to keep pace with its scope ambitions.

## 7. User Feedback Summary

- **Security is front-of-mind:** Multiple p1 security fixes merged this week (Gemini key exposure, attachment bounds, approval-token orphan) show that maintainers are proactively closing real risk windows.
- **Reliability with fallbacks is a recurring theme:** Issues #9544 and #10023 both target the reliable-provider path, indicating users are relying on fallback configs in production and need accurate accounting, not just functioning retries.
- **macOS/Windows testing gaps are acknowledged:** The new scheduled platform tests (#9398) are a direct response to the need for cross-platform confidence.
- **RFC process overhead is visible to contributors:** The RFC process streamlining proposal (#9496) and the "Work Lanes" RFC (#6808) are internal acknowledgments that governance can become a bottleneck. The project is self-correcting.

## 8. Backlog Watch

- [Issue #6165 — RFC: Lighter core via external integrations](https://github.com/zeroclaw-labs/zeroclaw/issues/6165) (15 comments, `needs-maintainer-review`) — Open since 2026-04-27. This is a major architectural direction question that has been waiting nearly 4 months for a maintainer decision. The "no-stale" label suggests it is not forgotten, but the lack of a clear decision is blocking scoping for the v0.9.x line.
- [Issue #6653 — Host-architecture policy for emulated installs](https://github.com/zeroclaw-labs/zeroclaw/issues/6653) (7 comments, no `status:accepted`) — Open since 2026-05-14. Appears dormant and may be waiting on a maintainer call on whether emulation is even in scope.
- [PR #9109 — Hailo-Ollama provider](https://github.com/zeroclaw-labs/zeroclaw/pull/9109) (`needs-author-action`) — A feature PR from a non-maintainer that has been idle for over a month awaiting author updates. If abandoned, it should be closed or taken over.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*