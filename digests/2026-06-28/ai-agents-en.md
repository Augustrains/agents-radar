# OpenClaw Ecosystem Digest 2026-06-28

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-28 02:07 UTC

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

# OpenClaw Project Digest — 2026-06-28

## 1. Today's Overview

OpenClaw is in a period of **extremely high activity** but also **significant maintenance churn**. With 500 issues and 500 PRs updated in the last 24 hours, the project shows signs of both rapid community engagement and a growing backlog of unresolved problems. Of the 500 open issues, 487 remain active, and a striking 451 out of 500 PRs are still open — indicating a **review bottleneck** where contributions pile up faster than maintainers can process. No new releases were published today. The project's health is mixed: strong feature development momentum is undercut by persistent stability problems, especially around session state management, message delivery reliability, and memory leaks that affect production deployments.

## 2. Releases

*No new releases today.*

---

## 3. Project Progress

**Merged/Closed PRs today (49 total):**

| Notable Merged/Closed PR | Description |
|---|---|
| [#95964](https://github.com/openclaw/openclaw/pull/95964) | **Persist hosted catalog snapshots in state** — part of the hosted marketplace feed stack, enabling offline-available plugin catalogs |
| [#68936](https://github.com/openclaw/openclaw/pull/68936) | **Autofix pipeline + Windows daemon** — adds a Claude Agent SDK-powered PR review autofix loop plus a Windows background supervisor for the gateway |
| [#97150](https://github.com/openclaw/openclaw/pull/97150) | **Link local e2e tests into QA coverage** — mature testing infrastructure improvements |
| [#65382](https://github.com/openclaw/openclaw/pull/65382) | **Format common cron intervals in UI** — UX improvement for cron schedule display |

**Key themes in today's closed work:**
- **Hosted marketplace infrastructure** advancing (PR #95964), suggesting a future ClawHub/plugin store capability
- **Windows support** improvements (PR #68936 — background daemon)
- **Testing/QA** rigor increasing (PR #97150)

---

## 4. Community Hot Topics

### Most Active Issues (by comment count)

| Issue | Comments | Summary |
|---|---|---|
| [#58450](https://github.com/openclaw/openclaw/issues/58450) 🐚 **platinum hermit** | 15 | Agent promises follow-up but never actually starts any background action — user-facing state is misleading |
| [#92201](https://github.com/openclaw/openclaw/issues/92201) 🦞 **diamond lobster** | 15 | Anthropic thinking signatures intermittently invalid on replay; recovery wrapper never fires |
| [#50090](https://github.com/openclaw/openclaw/issues/50090) 🦞 **diamond lobster** | 15 | **Community Skill Development & ClawHub** — long-standing meta-issue about the gap between skill ecosystem promise and reality |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) 🦞 **diamond lobster** | 14 | **Critical regression**: Coding Agent "never completes anything" — worked in v2026.4.2 |
| [#57901](https://github.com/openclaw/openclaw/issues/57901) 🦞 **diamond lobster** | 14 | Safeguard compaction ignores `compaction.model` config — uses session model instead |
| [#63216](https://github.com/openclaw/openclaw/issues/63216) 🐚 **platinum hermit** | 11 | Repeated hard context-overflow resets despite high `reserveTokensFloor` — retry loop re-injects bootstrap |

### Most Upvoted Issues (by 👍)

| Issue | 👍 | Theme |
|---|---|---|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | 9 | **Per-agent memory-wiki vault** — strong demand for isolated knowledge bases in multi-agent setups |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | 7 | **MathJax/LaTeX in Control UI** — academic/STEM users need formula rendering |
| [#53599](https://github.com/openclaw/openclaw/issues/53599) | 5 | **Chrome extension browser relay removed** — cross-machine browser control regression affects managed hosting |

### Analysis

The community's most pressing concerns cluster around **three themes**:

1. **Session state reliability** — Issues #58450, #63216, #62505, #50165 all describe agents that appear to work (respond, promise follow-ups, show "completed" status) but fail to actually perform the underlying work. This undermines trust in the core agent execution model.

2. **Multi-agent/collaboration gaps** — Issues #63829 (per-agent memory), #65374 (dreaming system contaminating agent identity), #56692 (group chat context blurring) show the community pushing OpenClaw beyond single-agent scenarios and finding architectural limitations.

3. **Skill ecosystem frustration** — Issue #50090 (now 3 months old with 15 comments) captures deep dissatisfaction with the gap between promised "write a SKILL.md, publish to ClawHub" experience and the actual broken onboarding, missing XDG_CONFIG_HOME handling (#53628), and undocumented issues.

---

## 5. Bugs & Stability

### Critical/High Severity (P1) Bugs Active Today

| Issue | Severity | Description | Fix PR Exists? |
|---|---|---|---|
| [#92201](https://github.com/openclaw/openclaw/issues/92201) | P1 🦞 diamond lobster | Anthropic thinking signatures invalid on replay; recovery wrapper never fires | No |
| [#62505](https://github.com/openclaw/openclaw/issues/62505) | P1 🦞 diamond lobster | **Regression**: Coding Agent never completes anything (worked in v2026.4.2) | No |
| [#63216](https://github.com/openclaw/openclaw/issues/63216) | P1 🐚 platinum hermit | Hard context-overflow resets loop despite high compaction headroom | No |
| [#57326](https://github.com/openclaw/openclaw/issues/57326) | P1 🦞 diamond lobster | CLI-backed helper paths still bypass CLI dispatch | No |
| [#65624](https://github.com/openclaw/openclaw/issues/65624) | P1 🦞 diamond lobster | Mattermost slash commands expose reusable command tokens in cleartext (CVSS 7.6/8.6) | No |
| [#51396](https://github.com/openclaw/openclaw/issues/51396) | P1 🦞 diamond lobster | `clearUnboundScopes` strips operator scopes for non-local token-auth clients | No |
| [#53599](https://github.com/openclaw/openclaw/issues/53599) | P1 🦞 diamond lobster | Chrome extension browser relay removed — breaks cross-machine hosting (regression) | No |
| [#45224](https://github.com/openclaw/openclaw/issues/45224) | P1 🐚 platinum hermit | Unhandled Playwright assertion error crashes entire Gateway process | No |

### Memory & Performance Issues

| Issue | Problem |
|---|---|
| [#55334](https://github.com/openclaw/openclaw/issues/55334) 🐚 **platinum hermit** | `sessions.json` unbounded growth (~50-100 MB/min) causes gateway OOM — `skillsSnapshot` duplicated per session |
| [#54155](https://github.com/openclaw/openclaw/issues/54155) 🦐 gold shrimp | Gateway memory leak: 389MB → 14.7GB over 4 days with session accumulation |
| [#95915](https://github.com/openclaw/openclaw/issues/95915) 🦞 diamond lobster *(CLOSED)* | Heap not released on embedded run abort — persistent lock causes gradual exhaustion |

### Recently Closed Bugs (Today)

| Issue | Fix |
|---|---|
| [#95833](https://github.com/openclaw/openclaw/issues/95833) | Subagent abort-settle fails to release `.jsonl.lock`, permanently breaking session — **now closed** |
| [#95915](https://github.com/openclaw/openclaw/issues/95915) | Heap not released on embedded run abort — **now closed** |

**Assessment:** The project has a **serious accumulation of P1 bugs**, many of which (e.g., #62505 coding agent regression, #92201 Anthropic signature invalidity) directly impact core agent functionality. The fact that these issues have open "clawsweeper:needs-maintainer-review" and "needs-product-decision" labels suggests maintainers are aware but either blocked or resource-constrained. The only two bugs closed today were reported just 5-6 days ago (#95833 from June 22, #95915 from June 23), indicating rapid triage for the most recent reports, but older issues remain open for months.

---

## 6. Feature Requests & Roadmap Signals

### High-Community-Support Features

| Issue | 👍 | Feature | Likely Ship Timeline |
|---|---|---|---|
| [#63829](https://github.com/openclaw/openclaw/issues/63829) | 9 | **Per-agent memory-wiki vault** — isolated knowledge bases | **Likely next release** (strong demand, clear architecture) |
| [#42840](https://github.com/openclaw/openclaw/issues/42840) | 7 | **MathJax/LaTeX in Control UI** | Moderate; depends on UI team bandwidth |
| [#60572](https://github.com/openclaw/openclaw/issues/60572) | 3 | **Multi-slot memory architecture** — separate providers per memory layer | Long-term; architectural change |
| [#58818](https://github.com/openclaw/openclaw/issues/58818) | 2 | **Guarantee last N raw messages in agent context** — survive compaction/reset | **Likely next release** (complements compaction fixes) |
| [#54794](https://github.com/openclaw/openclaw/issues/54794) | 2 | **Telegram Inline Query support** (`@botname` in any chat) | Moderate; Telegram-specific |

### Roadmap Signals from Active PRs

- **Hosted marketplace (ClawHub)**: PR #95969 (catalog source profile validation) + #95964 (state persistence) suggest a **plugin marketplace** is actively in development, potentially for the next major release.
- **Windows native support**: PR #97086 (Windows MXC sandbox backend) + #68936 (Windows daemon) signal expanding beyond Linux-first.
- **Microsoft Teams multi-account**: PR #97340 enables multiple bot identities per gateway.
- **Provider circuit breakers**: PR #64127 adds quota exhaustion handling — important for production reliability.

### Prediction for Next Release

Based on active PRs and community demand, the next release will likely include:
1. **Hosted marketplace/ClawHub catalog** infrastructure
2. **Per-agent memory isolation** (addressing #63829)
3. **Context overflow recovery improvements** (multiple PRs targeting #63216)
4. **Windows daemon and MXC sandbox** support

---

## 7. User Feedback Summary

### Recurring Pain Points

| Pain Point | Evidence | Frequency |
|---|---|---|
| **"Agent promises but doesn't deliver"** | #58450, #62505, #50165 — agents say they'll do something, then don't | High (multiple P1/P2 issues) |
| **Memory/session leaks kill production deployments** | #55334 (OOM), #54155 (14.7GB leak), #95915 (heap retention) | Critical (affects uptime) |
| **Multi-agent context confusion** | #65374 (dreaming contaminates identity), #56692 (group chat blurring), #52249 (ACP parent stuck) | Growing (as multi-agent adoption increases) |
| **Skill ecosystem broken** | #50090 (long-running meta-issue), #53628 (XDG_CONFIG_HOME not processed), #51429 (hardcoded paths) | High (ecosystem trust eroding) |
| **Configuration/hardcoded paths** | #51429 (wangtao's path merged into code), #53628 (env vars not interpreted) | Alarming (quality control concern) |
| **Message delivery failures** | #54531 (Telegram/Discord silent drops), #50093 (WhatsApp backfill), #58514 (Google Chat ignored) | Moderate (channel-specific but frustrating) |

### Notable User Quotes (paraphrased from issues)

> "Coding Agent just doesn't do _anything_ apart from vague status updates and apologies for vagueness" — #62505 (drpau)

> "Some wangtao hardcoded his working space path into the code and somebody merged and published it" — #51429 (buggiant-coder) [translated from Chinese]

> "The gap between promise and practice is wide right now" — #50090 (ocdlmv1) on ClawHub skills

> "OpenClaw status reports memory as unavailable even though the live gateway plugin is working" — #57256 (leofaoro)

### Satisfaction Signals

- High 👍 counts on feature requests (#63829 with 9, #42840 with 7) indicate an **engaged, passionate community** that invests time in improvement proposals
- Multiple contributors submitting PRs (#97342, #97343, #97344 all from today) shows active development interest
- The "rating: 🐚 platinum hermit" and "🦞 diamond lobster" labels on many issues indicate the community's own severity assessment is **highly critical** — users are taking time to properly classify and escalate issues

---

## 8. Backlog Watch

### Issues Longest Open Without Resolution (Stale, No Fix PR)

| Issue | Created | Age | Priority | Reason for Concern |
|---|---|---|---|---|
| [#35203](https://github.com/openclaw/openclaw/issues/35203) | 2026-03-05 | **115 days** | P2 | Mult-agent collaboration RFC with 9 comments — zero maintainer resolution |
| [#50090](https://github.com/openclaw/openclaw/issues/50090) | 2026-03-19 | **101 days** | P2 | ClawHub/skill ecosystem — core to platform growth, yet unresolved |
| [#51429](https://github.com/openclaw/openclaw/issues/51429) | 2026-03-21 | **99 days** | P2 | **Hardcoded developer path merged into production code** — security/code review failure |
| [#51396](https://github.com/openclaw/openclaw/issues/51396) | 2026-03-21 | **99 days** | P1 | `clearUnboundScopes` strips operator scopes — security regression |
| [#50165](https://github.com/openclaw/openclaw/issues/50165) | 2026-03-19 | **101 days** | P2 | Subagents appear completed before work actually finishes |
| [#53628](https://github.com/openclaw/openclaw/issues/53628) | 2026-03-24 | **96 days** | P2 | `XDG_CONFIG_HOME` not processed during skill install |

### PRs Awaiting Maintainer Action (Longest Open)

| PR | Created | Age | Status |
|---|---|---|---|
| [#58482](https://github.com/openclaw/openclaw/pull/58482) | 2026-03-31 | **89 days** | Needs real-behavior-proof |
| [#64127](https://github.com/openclaw/openclaw/pull/64127) | 2026-04-10 | **79 days** | Needs proof |
| [#59414](https://github.com/openclaw/openclaw/pull/59414) | 2026-04-02 | **87 days** | Waiting on author |
| [#74163](https://github.com/openclaw/openclaw/pull/74163) | 2026-04-29 | **60 days** | Needs proof |
| [#90239](https://github.com/openclaw/openclaw/pull/90239) | 2026-06-04 | **24 days** | Ready for maintainer look |
| [#90259](https://github.com/openclaw/openclaw/pull/90259) | 2026-06-04 | **24 days** | Waiting on author |

### Alerts for Maintainers

1. **Issue #51429** (hardcoded developer path) is a **code quality and security red flag** — 99 days open suggests the review process that missed it also hasn't addressed it.
2. **PR #90239** and **#90259** (session history family lookup + carryover summaries, both XL size) have been "ready for maintainer look" / "waiting on author" since June 4 — these directly address the session state reliability issues (#63216, #55334) that are top community pain points.
3. **PR #95969** (hosted catalog validation) has been "ready for maintainer look" since June 23 — this is key infrastructure for the ClawHub marketplace that the community has been waiting 100+ days for.

---

*Digest generated from GitHub data as of 2026-06-28. All links reference openclaw/openclaw repository.*

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report, synthesized from the provided community digests.

---

### Cross-Project Comparison Report: Personal AI Agent Ecosystem
**Date:** 2026-06-28

#### 1. Ecosystem Overview

The personal AI agent open-source landscape is characterized by intense, churn-heavy activity focused on moving beyond single-turn chat into autonomous, multi-agent, and production-grade systems. The top-tier projects (OpenClaw, Hermes Agent, IronClaw) are grappling with scaling pains, manifesting as critical review bottlenecks, memory leaks, and security regressions that undermine trust in core agent execution. A second wave of smaller, more focused projects (NanoClaw, NullClaw, Moltis, PicoClaw) are addressing specific developer pain points—such as platform compatibility and secure tool execution—with less community friction. Universal themes across the ecosystem include a push for robust multi-agent memory isolation, secure credential management, extensible tool ecosystems (MCP), and the stabilization of long-running autonomous sessions against crashes and data loss.

#### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score / Signal |
| :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | 500 | 500 | No new release | **Fair** – High churn, critical review bottleneck, serious P1 bugs, skill ecosystem frustration. |
| **Hermes Agent** | 50 | 50 | No new release (v0.15.x) | **Good** – High signal-to-noise bug fixing sprint; Windows stability gaps remain. |
| **IronClaw** | 11 | 50 | Pending (#5311) | **Very Good** – Strong delivery pace on capability-policy epic; minor OAuth bugs. |
| **ZeroClaw** | 41 | 50 | No new release (v0.8.2) | **Good** – Intense development for v0.8.3 milestone; one critical 73-day-old S1 bug. |
| **CoPaw** | 5 | 14 | No new release | **Good** – Focused on testing/stability; conversation data loss bug is critical concern. |
| **NanoBot** | N/A | 46 | No new release | **Good** – Rapid security fix sprint; good community engagement. |
| **PicoClaw** | 3 | 4 | No new release | **Stable** – Steady contributions; new Matrix crypto bug needs triage. |
| **LobsterAI** | 2 | 8 | No new release | **Fair** – Moderate activity; two critical Windows regressions unaddressed. |
| **NanoClaw** | 1 | 8 | No new release | **Weak** – Low activity; critical `/update-skills` silent failure in review. |
| **NullClaw** | 1 | 1 | No new release | **Low** – Light activity; Android build bug unanswered for 66 days. |
| **Moltis** | 1 | 1 | No new release | **Low** – Maintenance phase; one new macOS bug, no major features. |
| **TinyClaw / ZeptoClaw** | 0 | 0 | No activity | **Dormant** |

#### 3. OpenClaw's Position

**Advantages:**
- **Largest Community & Ecosystem Ambition:** OpenClaw has the most significant community engagement (500 issues/PRs updated daily) and is actively building the "ClawHub" marketplace, mirroring a platform strategy. It also has the broadest feature set, including the agent collaboration bus, skill system, and multiple channel adapters.
- **Rich Tool & Agent Infrastructure:** It has the most mature agent execution model, including subagents, a dreaming/compaction system, and a hosted marketplace, setting the bar for feature depth.

**Technical Approach Differences:**
- **All-in-One Monolith vs. Modular:** OpenClaw’s approach is more monolithic, bundling everything into a single project (`openclaw/openclaw`). In contrast, projects like **IronClaw** use a Rust-based, library-oriented architecture (`ironclaw_common`, `ironclaw_skills`), while **ZeroClaw** is building a WASM-first plugin runtime.
- **Scalability Pains:** OpenClaw's high activity is creating a **review bottleneck** (451 out of 500 PRs are open) and a **critical stability gap**. It has the highest number of unresolved P1 bugs, particularly around session state reliability, which directly undermines its core value proposition.

**Community Size Comparison:**
- OpenClaw dominates in raw community numbers, but the sentiment is a mix of high engagement and high frustration. Projects like **IronClaw**, **ZeroClaw**, and **Hermes Agent** have smaller communities but show higher ratios of resolved issues and feature delivery per update.

#### 4. Shared Technical Focus Areas

The following requirements are emerging across multiple projects:

| Requirement | Projects Involved | Specific Needs |
| :--- | :--- | :--- |
| **Multi-Agent Memory Isolation** | **OpenClaw**, **PicoClaw**, **CoPaw** | Per-agent knowledge bases / wikis (OpenClaw #63829); agent collaboration bus with isolated history (PicoClaw #2937); conversation loss on crash (CoPaw #5579). |
| **Secure Credential Management** | **Hermes Agent**, **NanoBot**, **LobsterAI** | Credential pool rewrite not dropping concurrent additions (Hermes #19566); secrets leaked in logs (Hermes #22016); login-shell secrets leak (NanoBot #4518). |
| **Extensible Tool Ecosystem (MCP)** | **ZeroClaw**, **OpenClaw**, **LobsterAI** | MCP resource & prompt support beyond tools (ZeroClaw #4467); SSE/HTTP MCP transport (LobsterAI #1001); hosted plugin marketplace (OpenClaw #95964, #95969). |
| **Backward Compatibility & Regressions** | **ZeroClaw**, **CoPaw**, **LobsterAI** | Regression in coding agent completion (OpenClaw #62505); model provider abstraction breaking custom vendors (CoPaw #5584); Windows installer crash in 2026.6.1 (LobsterAI #2215). |
| **Robust Session & State Persistence** | **OpenClaw**, **Hermes Agent**, **CoPaw** | Memory leaks causing OOM (OpenClaw #55334, #54155); silent conversation loss on shutdown (CoPaw #5579); PID-file race causing restart loops (Hermes #21549). |

#### 5. Differentiation Analysis

| Differentiation | Projects | Strategy & Target User |
| :--- | :--- | :--- |
| **Breadth vs. Depth** | **OpenClaw** (Breadth) vs. **IronClaw**, **ZeroClaw** (Depth) | OpenClaw aims to be the one-stop shop. IronClaw focuses on Rust-based performance and production-grade APIs. ZeroClaw focuses on a WASM-first, high-security plugin model. |
| **Target User** | **OpenClaw**: General power users / hobbyists. **Hermes Agent**: Desktop-heavy / interactive users. **IronClaw**: Developers building custom, deployable agent services. **ZeroClaw**: Security-conscious, advanced developers. **NanoClaw**: Minimalist CLI / channel users. **LobsterAI**: Lower-code / easier deployment for non-developers. | |
| **Architecture** | **IronClaw** (Rust, crate-based, Reborn stack). **ZeroClaw** (Go, WASM plugins). **OpenClaw** (TypeScript, monorepo). **Hermes Agent** (Python, heavy desktop focus). | Rust vs. Go vs. TypeScript/JS reflects different performance and ecosystem priorities. IronClaw’s Reborn stack is a deliberate rewrite for production stability. |
| **Platform Support** | **LobsterAI**, **Hermes Agent**: Strong Windows desktop focus. **NullClaw**: Potential for mobile (Android/Termux). **OpenClaw**: Linux-first, improving Windows via daemon. | Platform support is a key differentiator for desktop-first vs. server-first deployments. |

#### 6. Community Momentum & Maturity

- **Top Tier (Rapid Iteration & High Engagement):** **OpenClaw**, **ZeroClaw**, **IronClaw**, **Hermes Agent**. These projects see daily massive PR/issue volumes and are pushing major features (marketplaces, capability policies, WASM runtimes). OpenClaw is the most volatile; IronClaw is the most organized.
- **Stabilizing / Bug-Fix Sprint:** **NanoBot**, **CoPaw**. These projects are currently in a sprint to fix security issues and stabilize after major releases, with less emphasis on new features.
- **Steady & Low-Churn:** **PicoClaw**, **Moltis**, **NanoClaw**. These projects are seeing consistent but low levels of activity, often from a small core of contributors. They are either in maintenance mode or focused on niche improvements.
- **Dormant:** **TinyClaw**, **ZeptoClaw**. No activity reported.

#### 7. Trend Signals

1.  **The "Autonomous Agent Reliability Cliff":** User feedback across the ecosystem strongly indicates that current models are good at *promising* autonomous behavior but poor at *delivering* it reliably. Issues like "agent promises but doesn't act" (OpenClaw) and "never completes anything" (OpenClaw) signal a core UX gap that needs fundamental architectural solutions (e.g., verification gates, better task queuing).
2.  **Security is Shifting Left, but Painfully:** The rapid triage of credential leakage (Hermes, NanoBot) and shell injection vulnerabilities (NanoBot) shows that security is becoming a first-class concern, but the volume of these issues suggests it is still an afterthought in initial design.
3.  **The "Local-First vs. Cloud-First" Trade-off:** Projects are explicitly engineering for either. **OpenClaw** invests heavily in a hosted marketplace, whereas **ZeroClaw** focuses on WASM sandboxing and supply-chain signing for local security. **CoPaw** and **Moltis** are explicitly targeting smaller, local LLMs. This is a fundamental split that will define user personas.
4.  **The "Observability Gap":** The lack of persistent session state and checkpointing (CoPaw #5579, OpenClaw memory leaks) is a major blocker for adopting these agents in any kind of production or semi-autonomous workflow. Users want agents they can trust to run without constant supervision, which requires robust state management.
5.  **Cross-Platform Friction as a Barrier:** The ecosystem is still Linux-dominated. Windows and macOS users face significant, often unaddressed, bugs (Hermes, LobsterAI, NullClaw). Projects that successfully solve cross-platform deployment (e.g., IronClaw’s Rust portability) will have a major strategic advantage.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

Here is the NanoBot project digest for June 28, 2026.

---

## NanoBot Project Digest: 2026-06-28

### 1. Today's Overview
The project experienced an exceptionally high-volume day, with **46** pull requests updated in the last 24 hours, of which **29** were merged or closed. This pace, combined with 7 closed issues, indicates a sustained effort to stabilize the codebase following recent security disclosures and bug reports. The development team appears to be focusing on triaging a backlog of issues related to streaming reliability, session management, and core provider logic. The 46 PRs updated in a single day suggests a coordinated push, possibly involving a hackathon or a dedicated bug-fix sprint.

### 2. Releases
No new releases were tagged today.

### 3. Project Progress
A significant number of PRs were merged today, indicating strong progress on stability and security.

- **Security Fixes:** Two critical security fixes were merged.
    - **PR #4562** (open) addresses the `exec.allowPatterns` shell-chain bypass by validating each segment of a chained command. A fix for the login-shell secrets leak (#4518) is also in the pipeline.
    - **PR #4533** (merged) fixes a collision where distinct session keys (e.g., `telegram:a_b` vs `telegram:a:b`) mapped to the same file on disk.
- **Provider & Streaming Stability:** A series of high-priority bug fixes from developer `axelray-dev` were merged:
    - **PR #4531**: Fixes stream delta coalescing to include `_stream_id`, preventing interleaved streams from merging.
    - **PR #4532**: Fixes the Anthropic provider to normalize content blocks missing a `type` field.
    - **PR #4530**: Deduplicates tool call IDs in the non-stream parser, matching the logic already present in the streaming parser.
- **Cron Feature:** A long-running feature branch was finalized with the merge of **PR #4357** and **PR #4225**, adding a `silent` mode and `lock_recipient` to cron jobs. This allows background monitoring tasks to run without spamming the user unless there is something to report.
- **Testing & Reliability:** **PR #4523** fixed a flaky test (`test_keeps_n_most_recent`) caused by sub-millisecond timestamp collisions on modern filesystems.

### 4. Community Hot Topics
The most active discussions and feature work today center on the Tool Use (MCP) and Cron subsystems, as well as user-facing UI improvements.

- **Feature: MCP Image Handling ([PR #4542](https://github.com/HKUDS/nanobot/pull/4542)):** This PR, authored by `codedragoncom`, aims to deliver image content from MCP (Model Context Protocol) tools as artifacts instead of raw base64 strings. It has received significant attention, indicating strong community interest in richer tool interactions (e.g., image generation or analysis).
- **Feature: Cron Silent Mode & Locking ([PR #4225](https://github.com/HKUDS/nanobot/pull/4225) & [#4357](https://github.com/HKUDS/nanobot/pull/4357)):** The merged work on silent cron jobs was a highly requested feature for background monitoring. The underlying need is for headless, reliable background agents that don't produce noise.
- **Bug: WebUI Stuck on Reconnect ([PR #4565](https://github.com/HKUDS/nanobot/pull/4565)):** This fix for the open issue #4500 is highly active. The user pain point is a poor UX where the interface appears busy with no way to stop the stalled task.
- **Feature: `ask_clarification` Tool ([PR #4527](https://github.com/HKUDS/nanobot/pull/4527)):** This open PR proposes a built-in tool for the agent to halt and ask the user for clarification. This suggests a community desire for more autonomous, yet cautious, agent behavior that seeks input before acting on ambiguous instructions.

### 5. Bugs & Stability
Two **high-severity security bugs** were disclosed and actively fixed today, dominating the stability narrative.

- **Critical - Security Bypass ([#4521](https://github.com/HKUDS/nanobot/issues/4521)):** The `exec.allowPatterns` feature could be bypassed via shell chaining (`&&`, `||`). A fix is proposed in **PR #4562**. This represents a major integrity risk for users relying on this feature for sandboxing.
- **High - Secrets Leakage ([#4518](https://github.com/HKUDS/nanobot/issues/4518)):** The `exec` tool’s default login-shell execution could leak secrets from shell startup files (e.g., `.bashrc`). This is a regression in environment hygiene.
- **Medium - Anthropic API Rejection ([#4060](https://github.com/HKUDS/nanobot/issues/4060)]):** The Anthropic provider could send malformed payloads (missing `type` field), causing API errors. Fixed in **PR #4532**.
- **Low-Medium - Stuck WebUI Stream ([#4500](https://github.com/HKUDS/nanobot/issues/4500)):** A UX bug where a server restart leaves the WebUI in an unresponsive "processing" state. A fix is in review in **PR #4565**.
- **Low - Session Key Collision ([#4057](https://github.com/HKUDS/nanobot/issues/4057)):** Session files could overwrite each other due to "lossy" filename sanitization. Fixed in **PR #4533**.

### 6. Feature Requests & Roadmap Signals
The project’s roadmap appears to be moving toward higher reliability, richer agent capabilities, and better integration with external tools.

- **Advanced Agent Loop ([PR #4534](https://github.com/HKUDS/nanobot/pull/4534)):** A substantial PR proposes a "verification gate" and "provider recovery" layer. This signals a move toward an agent that can self-heal from provider errors and verify its own outputs.
- **Per-Session Model Presets ([PR #4555](https://github.com/HKUDS/nanobot/pull/4555)):** This suggests a roadmap feature allowing users to assign different LLMs to different conversations, enabling task-specific model selection.
- **Dream Module Enhancements ([PR #4554](https://github.com/HKUDS/nanobot/pull/4554) & [#4556](https://github.com/HKUDS/nanobot/pull/4556)):** Improvements to the "Dream" (memory consolidation) module to prevent duplicate skills and allow model overrides suggest a need for more robust and controllable long-term memory.
- **Predictions for v0.2.3:**
    - Merging of the security fixes (#4521, #4518).
    - The WebUI stream fix (#4565).
    - The MCP image artifact support (#4542).
    - The advanced agent loop (#4534) is more likely for a later minor version (v0.3.0) due to its complexity.

### 7. User Feedback Summary
- **Pain Point: Bloated Dependencies (#660):** A user expressed frustration that the "ultra-lightweight" claim is contradicted by the mandatory Node.js dependency in the Dockerfile. This indicates a desire for a truly minimal footprint, possibly suggesting a move to make Node.js optional.
- **Pain Point: Unreliable UI State (#4500):** Users are experiencing a frustrating "stuck" state in the WebUI after internal restarts, where the stop button is non-functional. This detracts from the polish of the user experience.
- **Satisfaction: Security Transparency:** The rapid triage and PR creation for the two security issues (#4521, #4518) shows a responsive development team, which is likely well-received by the community.

### 8. Backlog Watch
- **#660 - Bloated Node.js Dependency:** While closed today, this issue has 5 👍 and 14 comments. The maintainer's resolution or follow-up (e.g., making Node.js optional) will be watched by the community. This is a potential catalyst for architectural discussions in future milestones.
- **#4371 - Context Caching Breakpoint:** This open PR suggests adding a breakpoint in the context builder to improve prompt caching management. While not explicitly "long-unanswered," it has been open for 12 days with no recent comments from maintainers, despite being tagged as an enhancement. It may be deprioritized in favor of the more urgent bug fixes.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — June 28, 2026

## Today's Overview
Hermes Agent saw a surge of activity on June 28, with **50 issues updated** (36 open/active, 14 closed) and **50 PRs updated** (30 open, 20 merged/closed) in the last 24 hours. No new releases were published, and the project remains at **v0.15.x** with a tagging gap between `main` and the latest release (`v0.15.2` via `v2026.5.29.2`). A significant mass of fixes landed today—over 20 PRs merged—spanning credential security, gateway stability, provider fallback logic, and TUI completion performance. The maintainer @teknium1 drove most of the day's corrections, indicating a coordinated bug-squashing push.

## Releases
No new releases today. The latest published release remains **Hermes v0.15.2 (2026.5.29.2)**, with users reporting a discrepancy where `hermes update` shows only "7 commits behind" but does not advance to the tagged release ([Issue #38618](https://github.com/NousResearch/hermes-agent/issues/38618)).

## Project Progress
**20 PRs were merged or closed today.** Key advances:
- **Credential security & pool management:** PR [#53896](https://github.com/NousResearch/hermes-agent/pull/53896) (fixes #19566) preserves concurrently added credentials during credential pool rotation rewrites. PR [#53899](https://github.com/NousResearch/hermes-agent/pull/53899) resolves Anthropic keychain/file credential mismatch when one side expires. PR [#53907](https://github.com/NousResearch/hermes-agent/pull/53907) redacts full credential set on outbound chat paths (security fix).
- **Gateway stability:** PRs [#53897](https://github.com/NousResearch/hermes-agent/pull/53897) and [#14130](https://github.com/NousResearch/hermes-agent/pull/14130) bound adapter teardown awaits on the shutdown path, fixing PID-file race and restart loops (addressing #14128). PR [#36913](https://github.com/NousResearch/hermes-agent/pull/36913) adds timeouts to disconnect calls.
- **Provider routing & auxiliary fixes:** PR [#53901](https://github.com/NousResearch/hermes-agent/pull/53901) unblocks message queues on OpenRouter "no endpoints" image 404 errors. PR [#53900](https://github.com/NousResearch/hermes-agent/pull/53900) makes 401 auth errors trigger the auxiliary fallback chain. PR [#53895](https://github.com/NousResearch/hermes-agent/pull/53895) routes TUI completion RPCs to a pool to prevent UI freeze.
- **OpenRouter billing issues:** Multiple PRs target the recurring problem of paid auxiliary model fallbacks bypassing user free-only configuration (related to #24029, #44894).

## Community Hot Topics

| Issue/PR | Comments | Reactions | Link |
|----------|----------|-----------|------|
| Windows desktop app fails to compile (Issue #40187) | 14 | 1 👍 | [Link](https://github.com/NousResearch/hermes-agent/issues/40187) |
| OpenAI-Codex credential pool drops newly added credentials (Iss#19566, now closed) | 9 | 1 👍 | [Link](https://github.com/NousResearch/hermes-agent/issues/19566) |
| Hermes Desktop v40.9.3 crash on Windows 11 startup (Issue #38216) | 8 | 0 | [Link](https://github.com/NousResearch/hermes-agent/issues/38216) |
| Paid auxiliary model fallbacks bypassing free-only config (Issue #24029, closed) | 5 | 3 👍 | [Link](https://github.com/NousResearch/hermes-agent/issues/24029) |
| Gateway launchd double-spawn death spiral (Issue #21549, closed) | 5 | 0 | [Link](https://github.com/NousResearch/hermes-agent/issues/21549) |
| NVIDIA NIM `extra_body` translation strips `chat_template_kwargs` (Issue #50703) | 5 | 0 | [Link](https://github.com/NousResearch/hermes-agent/issues/50703) |
| Telegram message duplication (Issue #53449) | 3 | 0 | [Link](https://github.com/NousResearch/hermes-agent/issues/53449) |

**Analysis:** The most active threads reveal three persistent community pain points: **Windows desktop stability** (#40187, #38216), **credential and billing surprises** (#19566, #24029), and **provider-specific translation bugs** (#50703, #53449). The high engagement on #24029 (3 👍, 5 comments) signals widespread frustration with the auxiliary task billing bypass issue—users expect their explicit free-only configuration to be honored absolutely.

## Bugs & Stability

### Critical/High Severity (P1)
- **[CLOSED] OPENAI-Codex credential pool drops new credentials** (Issue #19566) — Concurrent credential rotation rewrites could silently delete recently added credentials. **Fixed** by PR #53896.
- **[CLOSED] Gateway double-spawn death spiral** (Issue #21549) — macOS `launchd` spawning two gateway instances simultaneously caused infinite restart loop. **Fixed** by PRs #53897, #14130, #19946.
- **[CLOSED] Auxiliary tasks bypassing free-only configuration** (Issue #24029) — Hardcoded paid model fallbacks for `title_generation`, `compression`, etc. despite user free-only config. **Fixed** by PR #53900 (401 fallback) and PR #53906 (credential pool exhaustion fallback).
- **[CLOSED] Security flaw: `hermes debug share` exposes private data** (Issue #22016) — Log files uploaded to public URLs contained prompts and user info. **Fixed**.
- **[CLOSED] CLI interrupt/stop not working** (Issue #22176) — `/stop` command and "stop" typing did not halt runaway agents. **Status: closed** (fix details not in today's PRs).
- **[OPEN] Telegram message duplication** (Issue #53449) — Short/medium replies delivered twice on Telegram due to strict visible-vs-final match logic. **Has open PR** #53912 fixing the silent empty-turn path.

### Medium Severity (P2)
- **[OPEN] NVIDIA NIM `extra_body` stripping `chat_template_kwargs`** (Issue #50703) — Prevents `thinking_mode` from reaching the main model. **No fix PR yet.**
- **[OPEN] Windows desktop app compile failure** (Issue #40187) — Error during electron-builder phase. **No fix PR yet.**
- **[OPEN] Desktop ENOENT: session.info CWD overwrite** (Issue #43042) — File browser resets to "unreadable" after `session.info` event. **No fix PR yet.**
- **[OPEN] `hermes skills update` doesn't refresh content_hash** (Issue #41176) — Permanent false `update_available` status. **No fix PR yet.**
- **[OPEN] Desktop crashes on Windows 11 startup** (Issue #38216) — `0x80000003` breakpoint exception. **No fix PR yet.**

### Low Severity (P3)
- Update reporting mismatch (Issue #38618), Desktop session lineage display (Issue #50192), claim verification mechanism (Issue #26742), Amazon Bedrock `service_tier` support (Issue #31322).

## Feature Requests & Roadmap Signals

### Strongly requested this week:
1. **Managed Agent Runtime contracts** (Issue #26675) — Wants first-class multi-agent workflow contracts on top of existing Kanban/SessionDB infrastructure. Would be a major expansion.
2. **Claim verification & audit mechanism** (Issue #26742) — Structured assistant verification/auditing, currently requires out-of-tree patching.
3. **Self-created skill correctness guarantees** (Issue #25833) — Mechanism-level guarantees for correctness and execution consistency of auto-created skills.

### Security flags:
- Full credential set redaction on outbound chat (#53907) — **Now merged.**
- Persistent `windows_hide_flags` crash on Discord voice (Issue #53874) — Shows platform-specific code path defect.

### Prediction: v0.16.0 candidate features
The density of credential pool fixes (#53896, #53899, #53906, #53913) and gateway stability patches suggests a **v0.16.x release** focusing on **credential management reliability**, **auxiliary task billing compliance**, and **gateway shutdown robustness**. The TUI freeze fix (#53895) and Telegram duplication work (#53912) are likely to be included.

## User Feedback Summary

### Pain Points (negative signals)
- **"My free-only config burned my OpenRouter credits"** — Multiple users (#24029, #44894) report being billed for auxiliary tasks despite explicit free-only model configuration. Core issue: hardcoded paid fallback models (`gemini-3-flash-preview`) bypass user config.
- **"Custom configs vanished after update"** (Issue #25272) — v0.13.0 update wiped all custom model configurations.
- **"CLI interrupt doesn't work"** (Issue #22176) — Users cannot stop runaway agents.
- **"Desktop crashes on Windows startup"** (Issue #38216) — `0x80000003` exception renders app unusable.

### Satisfaction Signals (positive trends)
- **Rapid bug closure:** 14 issues closed in 24 hours, including the credential pool loss (#19566), billing bypass (#24029), and gateway death spiral (#21549). Users seeing fixes land quickly.
- **Security responses:** PR #53907 redacting full credentials on outbound chat and PR #53896 preserving concurrent credential additions show proactive security hardening.
- **Community contributions:** User @teknium1 and other contributors (ChaostixZix, zedzhu, Harry-DWAC) pushing fixes daily.

### Use Cases Represented
- **Windows desktop users** (compilation/crash issues)
- **OpenRouter users** (free-only billing bypass)
- **Telegram/Feishu/Discord gateway users** (message duplication, crashes, shutdown hangs)
- **Multi-agent workflow developers** (runtime contracts request)
- **Enterprise/security-conscious users** (credential audit, redaction, claim verification)

## Backlog Watch

### Issues requiring maintainer attention (30+ days, no fix PR):
1. **[[OPEN] Issue #25833](https://github.com/NousResearch/hermes-agent/issues/25833)** — Self-created skill correctness guarantees (created May 14, last updated June 27). P3, no fix PR.
2. **[[OPEN] Issue #26742](https://github.com/NousResearch/hermes-agent/issues/26742)** — Claim verification & audit mechanism (created May 16, last updated June 27). P3, no fix PR.
3. **[[OPEN] Issue #26675](https://github.com/NousResearch/hermes-agent/issues/26675)** — Managed Agent Runtime contracts (created May 16, last updated June 28). P3, no fix PR.

### New issues today needing initial response (24 hours):
4. **[[OPEN] Issue #53874](https://github.com/NousResearch/hermes-agent/issues/53874)** — Discord voice input crashes on Linux (`windows_hide_flags` not defined). Created June 28, no comments from maintainers.
5. **[[OPEN] Issue #53898](https://github.com/NousResearch/hermes-agent/issues/53898)** — `hermes plugins list` can't see pip-installed entry-point plugins, though runtime loads them. Created June 28, no maintainer response.
6. **[[OPEN] Issue #53916](https://github.com/NousResearch/hermes-agent/pull/53916)** — MCP HTTP transport crashes on JSON-string headers in config.yaml. **New PR, pending review.**

### Older concerns:
- [#38216](https://github.com/NousResearch/hermes-agent/issues/38216) (Windows 11 crash, June 3) — **No fix PR** despite being a startup blocker. Severity: P2, 8 comments.
- [#40187](https://github.com/NousResearch/hermes-agent/issues/40187) (Desktop compile failure, June 6) — **No fix PR** despite 14 comments. Severity: P2.
- [#41176](https://github.com/NousResearch/hermes-agent/issues/41176) (Skills update hash not refreshed, June 7) — **No fix PR** reported. Severity: P2.
- [#43042](https://github.com/NousResearch/hermes-agent/issues/43042) (Desktop ENOENT on session.info, June 9) — **No fix PR** reported. Severity: P3.
- [#48338](https://github.com/NousResearch/hermes-agent/issues/48338) (System role injection causing HTTP 400 on vLLM/Qwen, June 18) — **No fix PR** reported. Severity: P2.

---

**Project health assessment:** High activity with strong signal-to-noise ratio—most of today's 20+ merged PRs address real user-reported bugs, not cosmetic changes. The credential/billing security work is commendable. However, the **persistent Windows desktop crash** (#38216, now 25 days old) and **compile failure** (#40187, 22 days old) without fix PRs are concerning gaps in cross-platform support. The **update version mismatch** (#38618, 24 days old) creates user confusion about the release process. Maintainers should prioritize these three Windows-specific issues for a near-term patch release.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-06-28

## Today's Overview
PicoClaw saw moderate activity with 3 issues updated and 4 PRs active in the last 24 hours. Two bugs were closed (one a long-standing Windows path issue), one new Matrix crypto bug was opened, and two PRs were merged—notably a long-running Agent Collaboration Bus feature (#2937) that closed after 34 days. No new releases were published. Overall project health appears stable with steady community contributions, though the backlog of unmerged PRs (2 open from today) and one new unaddressed bug suggest maintainer attention is slightly stretched.

## Releases
No new releases were published today.

## Project Progress
- **Agent Collaboration (#2937 — CLOSED/MERGED):** A major feature adding a first-class internal Agent Collaboration Bus was merged after 34 days. It introduces per-agent mailboxes, collaboration threads with isolated session history, structured message envelopes with delivery state tracking, and permission-aware routing. This is a foundational capability for multi-agent workflows.
- **MCP Flag Fix (#3048 — CLOSED/MERGED):** Fixed `mcp add` argument parsing to properly reject unknown pre-positional flags (e.g., `--no-color`) that leaked into the custom parser due to `DisableFlagParsing: true`. A robustness improvement for the MCP tooling.

## Community Hot Topics
- **Telegram Permission Control (#3114)** — This closed feature request received 2 comments and 1 👍, asking for per-chat-type permission levels (private/group/channel) to prevent dangerous commands in group contexts. The underlying need is clear: current `allow_from` whitelisting is too coarse for multi-channel deployments, and the author specifically flags shell `exec` and file modification risks. Expect this to be prioritized as a security concern.
- **Windows Path Bug (#2472)** — Closed after 78 days with 7 comments, fixing `list_dir` returning `invalid argument` on Windows due to backslash/slash mismatch. This was a subtle Go `os.Root` compatibility issue affecting cross-platform users.
- **Simplex Channel PR (#3193)** — Newly opened today by user "dim", adding a simplex channel type. No comments yet, but the feature extends PicoClaw's channel architecture. Maintainer interest or pushback is unknown.

## Bugs & Stability
**High — Crypto Not Enabled (#3194) — NEW, OPEN**  
Reported by Damian-o2 for Matrix channel: `Received encrypted message but crypto is not enabled`. PicoClaw v0.2.4 with Go 1.25.8, from commit `ed618e1`. Steps to reproduce: connect a Matrix gateway with encryption enabled. This is a blocking bug for anyone using Matrix with E2EE. **No fix PR exists yet.** Severity: high because encrypted messages are silently unhandled.

**Medium — Windows Path Separator (#2472) — CLOSED**  
Closed today. System-level `list_dir` failure on Windows due to backslashes passed to `os.Root`. Fix was merged; no regressions expected.

**Low — LINE Channel Body.Close() (#3189) — OPEN (PR)**  
PR from chengzhichao-xydt explicitly ignores `resp.Body.Close()` errors in LINE channel's `Send` and `classifySDKError`. Minor cleanup; no functional impact.

## Feature Requests & Roadmap Signals
- **Agent Collaboration Bus (just merged)** — Likely to be the headline feature of the next minor release (0.3.x?), enabling multi-agent architectures. Expect documentation and tutorials to follow.
- **Telegram Permission Levels (#3114 — closed)** — Despite being closed, its high community reaction (1 👍, strong security argument) suggests it will be implemented soon. The proposal is well-scoped: restrict `exec`, `write_file`, `edit_file` in group/channel contexts.
- **Simplex Channel (#3193 — open PR)** — A new channel type being contributed. If merged, it signals continued expansion of connectivity options, possibly for IoT or one-way notification use cases.
- **MCP Flag Parsing Fix (#3048 — merged)** — Improved CLI ergonomics for MCP. This will ship in the next release without breaking changes.

## User Feedback Summary
- **Pain point: Cross-platform path handling** — The #2472 Windows bug (78 days, 7 comments) highlights friction for non-Linux users. PicoClaw's Go-based architecture needs consistent path normalization.
- **Pain point: Channel security granularity** — #3114 signals that users deploying PicoClaw in Telegram groups want guardrails against accidental or malicious use of powerful tools. The lack of per-context permission controls is a real deployment blocker.
- **Pain point: Matrix encryption** — #3194 (opened today) shows that Matrix E2EE integration is incomplete, surprising users who expect it to work.
- **Satisfaction: Agent collaboration** — The merging of #2937 (34 days in review) suggests strong maintainer commitment to multi-agent features, likely satisfying power users and developers building complex workflows.

## Backlog Watch
**Issue #3194 — "Received encrypted message but crypto is not enabled"**  
*Just opened today* — no maintainer response yet. Possibly a configuration issue or a genuine code gap. Needs triage and either a fix or a documentation update clarifying Matrix crypto requirements. *Priority: high* — blocks Matrix E2EE users completely.

**PR #3193 — "Added simplex channel type"**  
*Opened today* — no comments from maintainers. Unclear if this is an accepted concept or needs design discussion. *Watch:* if maintainers are silent for >72 hours, it may indicate capacity issues or the need for more justification.

**PR #3189 — "fix(line): explicitly ignore resp.Body.Close() errors"**  
*Opened today* — low-severity, but if unmerged for days, signals maintainer focus on higher-priority work. No risk, but keep an eye.

**No long-unanswered items** — The oldest open item (outside of stale-closed ones) is from today. The project appears responsive to recent activity.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-28

## 1. Today's Overview
The NanoClaw project is in a moderate activity state with 8 open pull requests updated in the last 24 hours and no new releases. A single open issue (#2868) highlights a critical bug where `/update-skills` silently fails to refresh adapter code or pinned dependencies for already-installed channels. Community contributions are focused on fixing this issue and improving container runner and signal-cli resilience, alongside feature additions for OpenCode and dashboard support. No PRs were merged today, indicating the project is in a review-and-refine cycle rather than a rapid-delivery phase.

## 2. Releases
No new releases were published in the last 24 hours. The most recent release history shows no tags or versions to report.

## 3. Project Progress
No pull requests were merged or closed in the last 24 hours. The 8 open PRs represent the ongoing work:
- **Critical fix in review**: PR #2873 (by glifocat) directly addresses issue #2868 by splitting pre-flight from credentials to allow `/update-skills` to refresh code.
- **Signal stability fix**: PR #2874 (by bogdano2) aims to prevent crash-looping when signal-cli experiences boot flaps.
- **Container runner cleanup**: PR #2822 (by CutSnake01) removes a dead `/workspace/global` mount; PR #2823 removes a stale CLAUDE.md; PR #2824 drops outdated "Global Memory" instructions from the seed prompt.
- **Feature additions**: PR #2872 (by grantland) allows per-group model overrides for OpenCode agents via `container_configs.model`; PR #2871 adds a dashboard pusher that collects state snapshots every 60 seconds.

## 4. Community Hot Topics
The most active discussion centers on issue #2868 and its associated fix PR #2873:

- **Issue #2868** (open, 1 comment): `/update-skills` silently skips code/deps refresh for installed channels, nullifying a CHANGELOG migration that requires users to re-run `/add-<channel>`. This represents a serious usability gap where users believe they are updating but get no effect.
  - [Issue #2868](https://github.com/nanocoai/nanoclaw/issues/2868)

- **PR #2873** (open, by glifocat): The fix splits pre-flight validation from credential checking, enabling `/update-skills` to actually refresh channel adapter code and dependencies.
  - [PR #2873](https://github.com/nanocoai/nanoclaw/pull/2873)

No other issues or PRs have attracted comments or reactions today, suggesting focused work rather than broad community debate.

## 5. Bugs & Stability
**High Severity:**
- **Issue #2868** — `/update-skills` is a silent no-op for already-installed channels; pre-flight skips the code/deps refresh entirely. This is a regression-level bug that breaks the intended migration path for channel updates. A fix PR (#2873) exists and is in open review.
  - [Issue #2868](https://github.com/nanocoai/nanoclaw/issues/2868) | [Fix PR #2873](https://github.com/nanocoai/nanoclaw/pull/2873)

**Medium Severity:**
- **PR #2874** — signal-cli crash-looping on boot flaps. This is an operational stability issue for users relying on the Signal channel. A fix is proposed to add resilience.
  - [PR #2874](https://github.com/nanocoai/nanoclaw/pull/2874)

**Low Severity (cleanup):**
- PRs #2822, #2823, #2824 address dead mounts, stale files, and outdated instructions—these are maintenance items that reduce confusion but do not cause active crashes.

## 6. Feature Requests & Roadmap Signals
Two feature PRs were opened today, both by grantland, signaling infrastructure expansion:
- **PR #2871** — Dashboard pusher for NanoClaw state snapshots. This suggests an upcoming dashboard server integration for monitoring and observability.
- **PR #2872** — Per-group model overrides for OpenCode agents. This enables multi-model deployment within an OpenCode setup, a power-user feature for flexible agent configurations.

No user-submitted feature requests were filed as new issues in the last 24 hours. These PRs are author-driven enhancements likely targeting the next minor release.

**Predictions for next version:**
- Dashboard integration (PR #2871)
- OpenCode per-group model configuration (PR #2872)
- Fix for `/update-skills` regression (PR #2873)
- Signal channel stability improvement (PR #2874)

## 7. User Feedback Summary
The primary pain point visible today is the **broken `/update-skills` command**. Users who follow CHANGELOG instructions to "re-run `/add-<channel>`" to pick up updates find that the command silently does nothing. This erodes trust in the upgrade process and forces manual workarounds.

No explicit satisfaction signals or use case descriptions were posted in the last 24 hours. The Signal crash-loop fix (PR #2874) indirectly suggests user frustration with the channel's unreliability on boot.

## 8. Backlog Watch
Three PRs by CutSnake01 (all opened 2026-06-20) remain open and unreviewed for 8 days:
- **PR #2822** — Remove dead `/workspace/global` mount
- **PR #2823** — Remove groups/global/CLAUDE.md that host deletes on startup
- **PR #2824** — Drop stale "Global Memory" instruction from seed prompt

These are low-risk cleanup PRs, but their age suggests maintainer bandwidth is constrained or they are deprioritized. If left unmerged, the stale instructions and dead mounts may cause confusion for new contributors and operators over time.
- [PR #2822](https://github.com/nanocoai/nanoclaw/pull/2822)
- [PR #2823](https://github.com/nanocoai/nanoclaw/pull/2823)
- [PR #2824](https://github.com/nanocoai/nanoclaw/pull/2824)

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-28

## 1. Today's Overview
Project activity is **light** with only 1 new pull request and 1 issue updated in the last 24 hours. No new releases were published. The open PR introduces a significant new feature for structured tool approval flows, while the sole active issue concerns a reproducible build failure on Android/Termux. Community engagement remains moderate, with no merge activity today.

## 2. Releases
**None** — No new versions were released in the last 24 hours.

## 3. Project Progress
**No pull requests were merged or closed today.**

The only PR activity is an open submission:
- **[PR #969](https://github.com/nullclaw/nullclaw/pull/969) (open):** Implements a two-turn structured approval flow for tools (shell tool and others returning `ApprovalRequired`). The agent catches the error, stores a `PendingApproval`, and emits an `--approval--` SSE event for the UI to render an approval dialog. This is a **new feature** and has not yet been integrated.

## 4. Community Hot Topics
The most active discussion is:

- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868) (open, 4 comments):** A user reports that `zig build -Doptimize=ReleaseSmall` fails with `AccessDenied` when attempting to link `options.zig`. The environment is Android/Termux (aarch64) running Zig 0.16.0 and NullClaw v2026.4.17. The error occurs during file linking via `linkat`, suggesting a filesystem permission constraint or a Zig toolchain incompatibility on Android. No maintainer or community response has been posted yet, indicating the issue may require deeper investigation into Android's sandboxed filesystem behavior.

## 5. Bugs & Stability
**One bug report is active today:**

- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868) — Build failure on Android/Termux**  
  **Severity: Medium-High** — The bug blocks building NullClaw on a mobile platform that is explicitly used by developers. The error `AccessDenied` on `linkat` suggests a possible sandbox restriction (Termux uses a limited `/tmp`) or a linking issue with Zig 0.16.0 on aarch64 Android.  
  **Status:** No fix PR exists yet. The issue is 2 months old with no maintainer response.

## 6. Feature Requests & Roadmap Signals
- **[PR #969](https://github.com/nullclaw/nullclaw/pull/969)** introduces a **structured approval system** for tool execution. This is a clear roadmap signal: the project is moving toward safer human-in-the-loop interactions, likely required for production use of the shell tool. The pattern (error-based capture → SSE event → UI render) suggests an emerging architecture for secure tool delegation.

- **No user-submitted feature requests** were posted or updated in the last 24h.

**Prediction:** The structured approval flow will likely be merged into the next minor release (v2026.5.x or v2026.6.x), assuming code review passes.

## 7. User Feedback Summary
- **Pain point (Android cross-build):** The only active issue reflects a user attempting to use NullClaw on a mobile Linux environment (Termux). The build failure after 2 months of silence may indicate a gap in platform support.
- **Satisfaction signals:** No positive or negative user satisfaction comments were observed today.
- **Use case:** The PR author (valonmulolli) is contributing a production-grade authorization flow—suggesting real-world deployment requiring secure shell access.

## 8. Backlog Watch
- **[Issue #868](https://github.com/nullclaw/nullclaw/issues/868)** — **Unanswered for 66 days.** This is the most critical backlog item. The issue blocks building on Android/Termux, a non-trivial platform. A maintainer response or workaround would be valuable to avoid contributor churn from mobile developers.
- **[PR #969](https://github.com/nullclaw/nullclaw/pull/969)** — New today; no review yet. Should be monitored for maintainer attention to prevent prolonged open time.

---

*Generated from NullClaw GitHub data, snapshot 2026-06-28.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-28

## Today's Overview

**High-velocity engineering sprint continues**, with 50 pull requests and 11 issues updated in the last 24 hours. The **capability-policy epic (#5261) reached its delivery milestone**, with all five component issues and four related PRs merged/closed — delivering a complete four-dimension policy model (availability, identity, configuration, approval) with admin REST surface and DB-backed user roles. The active PR count (28 open) is elevated, reflecting both the size of ongoing work (three XL-sized PRs targeting QA infrastructure and chat history) and a backlog of 2 dependabot PRs awaiting merge. No new releases were cut today, but a release PR from yesterday (#5311) remains open and ready.

**Project health:** Strong forward momentum with disciplined feature gating (capability-policy stack is Reborn-only, no engine v2 entanglement). The CI/release pipeline shows some friction — a nightly E2E fail persists from May, and the release PR has stalled for 2 days with breaking API changes in `ironclaw_common` and `ironclaw_skills`.

---

## Releases

**No new releases** were published in the last 24 hours.

The pending release PR **#5311** ([link](https://github.com/nearai/ironclaw/pull/5311)) from 2026-06-26 remains unmerged. It includes breaking API changes:
- `ironclaw_common`: 0.4.2 → 0.5.0
- `ironclaw_skills`: 0.3.0 → 0.4.0
- `ironclaw`: 0.24.0 → 0.29.1

Users and downstream consumers should watch for this release, which will require migration.

---

## Project Progress

**22 PRs were merged/closed** in the last 24 hours. The dominant theme is **capability-policy delivery**:

### Capability Policy (Epic #5261) — Now Complete
All five component issues were closed:
- **#5272**: REST-created local users + dynamic auth ([link](https://github.com/nearai/ironclaw/issues/5272))
- **#5268**: Admin REST surface (four dimensions) + action catalog ([link](https://github.com/nearai/ironclaw/issues/5268))
- **#5273**: Four-dimension policy: delta store + PolicyResolver + enforcement ([link](https://github.com/nearai/ironclaw/issues/5273))
- **#5267**: Availability resolver at dispatch seam ([link](https://github.com/nearai/ironclaw/issues/5267))
- **#5266**: Reborn DB-backed user role + admin gate ([link](https://github.com/nearai/ironclaw/issues/5266))
- **#5261**: EPIC root ([link](https://github.com/nearai/ironclaw/issues/5261))

Core implementation PRs (all merged):
- **#5262**: `ironclaw_capability_policy` crate — pure model ([link](https://github.com/nearai/ironclaw/pull/5262))
- **#5344**: Engine — delta store + resolver + identity/config/approval ([link](https://github.com/nearai/ironclaw/pull/5344))
- **#5349**: Availability dimension (depends on #4544) ([link](https://github.com/nearai/ironclaw/pull/5349))
- **#5355**: Control plane — REST users + admin grants ([link](https://github.com/nearai/ironclaw/pull/5355))

### Other Merged Fixes/Chores
- **#5270**: DB-backed user role on WebChat-v2 caller ([link](https://github.com/nearai/ironclaw/pull/5270))
- **#5271**: Dependency bump — 47 updates across the everything-else group ([link](https://github.com/nearai/ironclaw/pull/5271))
- **#5364**: "Always allow eligible tools" default flipped to ON ([link](https://github.com/nearai/ironclaw/issues/5364))
- **#5370**: WebUI v2 frontend Node tooling pinned to Node 22 ([link](https://github.com/nearai/ironclaw/pull/5370))
- **#5382**: Fix hosted volume runtime startup (regression from PR #5346) ([link](https://github.com/nearai/ironclaw/pull/5382))

---

## Community Hot Topics

### Most Active Items (by comments/reactions)

1. **#5272** — REST-created local users (2 comments) — Closed yesterday as prerequisite for manual DB-wired testing of capability policy. Author zetyquickly provided a detailed redesign note superseding the env-token approach. [Issue link](https://github.com/nearai/ironclaw/issues/5272)

2. **#5261** — Capability-policy epic (1 comment, but epic-level tracking) — Closed yesterday. This epic tracked the entire capability-policy feature across four dimensions (availability, identity, configuration, approval) on the Reborn stack only. Users following per-user auth should monitor for follow-up tickets. [Issue link](https://github.com/nearai/ironclaw/issues/5261)

3. **#4928** — Notion OAuth redirects to localhost in Railway deployment (1 comment) — Significant user-facing bug: Notion MCP authorization works locally but generates unreachable `localhost` callbacks on Railway deployed instances. A clear regression in deployment environment handling. [Issue link](https://github.com/nearai/ironclaw/issues/4928)

4. **#5378** — Google OAuth token refresh fails with BackendUnavailable (0 comments but raised by `thisisjoshford`) — Reauth forced every ~1 hour on `hosted-single-tenant` and `local-dev` profiles. Impacts all Google-backed capabilities (Gmail, Calendar, Drive). No fix PR yet. [Issue link](https://github.com/nearai/ironclaw/issues/5378)

### Underlying Needs

The community and core contributors are clearly focused on **multi-user administration and production readiness**. The capability-policy work directly addresses the lack of fine-grained user permissions, which has been a pain point for deployments with more than one user. The OAuth bugs (Notion callback, Google token refresh) indicate that **production deployment profiles** (`hosted-single-tenant`) still have rougher edges in secret/redirect handling.

---

## Bugs & Stability

| Issue | Severity | Status | Summary |
|-------|----------|--------|---------|
| **#4928** — Notion OAuth localhost redirect on Railway | **High** | Open (since Jun 15) | Notion MCP authorization produces localhost callback URL in railway deployment; fix not identified yet |
| **#5378** — Google OAuth token refresh BackendUnavailable | **High** | Open (Jun 27) | Forces reauth every ~1 hour for Gmail, Calendar, Drive; affects `hosted-single-tenant` and `local-dev` |
| **#4108** — Nightly E2E failed | **Medium** | Open (since May 27, updated yesterday only via automation re-run) | Nightly E2E pipeline failure persists; last run on commit `5298504a`; extensions job failed; no fix identified |
| **#5364** — "Always allow eligible tools" default | **Low** | Closed (fixed) | UX issue — per-call approval prompts by default. Fixed by flipping default to ON. |
| **#5382** — Hosted volume runtime startup regression | **Medium** | Closed (fix merged) | PR #5346 caused `HostedSingleTenantVolume` to not be registered at startup. Fix merged same day. |

**Moderate severity day** — two high-severity bugs affect production users (OAuth/authorization failures), but zero regressions introduced by the capability-policy massive merge chain. The nightly E2E failure is a lingering concern, having been open for 32 days with no resolution.

---

## Feature Requests & Roadmap Signals

### Explicit Feature Requests
- **#5385** — Add Capability Policy (opened yesterday, 0 comments) — Requests fine-grained user configuration with owner/admin/member roles. Notably, this was opened *after* the epic #5261 was already closed, suggesting the requester may not have been tracking the project. However, it signals real user demand for the exact feature that just shipped. [Issue link](https://github.com/nearai/ironclaw/issues/5385)

### Implicit Roadmap Signals
The active open PRs suggest the following are in progress:
- **Reborn WebUI v2 QA infrastructure** — PR #5354 (live canary) and PR #5380 (QA matrix coverage) are both XL-sized and open, indicating expanding test coverage for the new UI.
- **Integration test framework** — PR #5381 establishes an in-process integration test framework for the Reborn stack, faking only model providers. This is a significant infrastructure investment that will improve regression detection.
- **Chat history port** — PR #5371 porting legacy browser coverage to Reborn WebUI, suggesting the new UI is nearing production parity.
- **Retry button fix** — PR #5365 fixing the chat Retry button (was a no-op stub), indicating the WebUI v2 chat is being refined for end-users.

### Predictions for Next Version
The capability-policy feature (epic #5261) will be the headline in the next release. Expect the pending release PR #5311 to merge within days, shipping with the breaking API changes in `ironclaw_common` and `ironclaw_skills`. Given the QA infrastructure work, the next release is likely **within 1 week**.

---

## User Feedback Summary

### Pain Points (direct from issues)
1. **OAuth callback handling broken in production** — Notion (issue #4928) and Google (issue #5378) integrations fail in deployed environments. Users deploying on Railway or using `hosted-single-tenant` profiles cannot reliably use third-party integrations.

2. **Per-call approval prompts default UX** — Addressed by #5364 (fixed), but users experienced friction from the default requiring manual approval for every tool invocation.

3. **Nightly pipeline instability** — Issue #4108 has been failing nightly for over a month without public explanation or fix timeline.

### Positive Signals
- The capability-policy feature, which directly addresses the request from #5385 and earlier #4628, shipped in its entirety within 4 days of epic creation — demonstrating **responsive development** to user needs.
- The retry button fix (#5365) and chat history port (#5371) show that WebUI v2, while still in development, is being actively polished for real-world use.

---

## Backlog Watch

### Long-Unanswered Issues Needing Maintainer Attention

| Issue | Age | Priority Signal |
|-------|-----|----------------|
| **#4108** — Nightly E2E failure | **32 days** (since May 27) | High — automated testing pipeline is consistently failing; no diagnostic or fix PR exists. Updated yesterday only by the nightly automation re-running, not by human triage. |
| **#4928** — Notion OAuth localhost redirect | **13 days** (since Jun 15) | High — blocks production use of Notion MCP integration. Only 1 comment (author's initial report), no maintainer response. |

### Stale PRs
- **#4498** — serde_yml bump (dependabot) — **23 days** stale, no maintainer interaction. [PR link](https://github.com/nearai/ironclaw/pull/4498)
- **#5114** — tokio-ecosystem bump (dependabot) — **7 days** stale, no maintainer interaction. [PR link](https://github.com/nearai/ironclaw/pull/5114)

**Recommendation:** The nightly E2E failure (#4108) and Notion OAuth bug (#4928) are the most impactful items lacking maintainer attention. The stale dependabot PRs are lower risk but should be merged or closed to reduce open-PR count noise.

---

*Digest generated from IronClaw GitHub data for 2026-06-28. Metrics: 11 issues updated, 50 PRs updated, 0 releases.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-28

## 1. Today's Overview
Project activity is **moderate** with 2 new issues and 8 PRs updated in the past 24 hours. All 7 closed PRs are labeled `[stale]`, indicating maintainers are actively cleaning up older work rather than shipping new features. No new releases were published. The two open issues report **severe Windows-specific stability problems** (installer failure and backup-induced freeze), both authored by the same user (woxinsj) with zero comments, suggesting these are still unconfirmed by maintainers. Overall health is stable but with notable Windows regressions unaddressed.

## 2. Releases
**No new releases** in the past 24 hours.

---

## 3. Project Progress

### Merged/Closed PRs (7 items, all labeled `[stale]`)

| PR | Summary | Impact |
|----|---------|--------|
| [#1001](https://github.com/netease-youdao/LobsterAI/pull/1001) | **hotfix: SSE & streaming HTTP MCP support** — `mcpServerManager.ts` previously only enabled `stdio` transport; added SSE/HTTP transport startup logic | Core MCP protocol expansion |
| [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446) | **fix(openclaw): gateway restart loop** — Two bugs fixed: race condition in process exit handling + zombie process detection causing infinite restart spiral (linked to #1400) | Critical stability fix for 4.1 upgrade |
| [#1448](https://github.com/netease-youdao/LobsterAI/pull/1448) | **fix(i18n): Agent settings English strings** — `delete` button missing i18n key; added `deleteAgent`, `confirmDeleteAgent`, `noMatchingSkills` keys | UX polish for international users |
| [#1449](https://github.com/netease-youdao/LobsterAI/pull/1449) | **feat(cowork): scheduled task session grouping** — Sidebar now folds repeated task executions into collapsible groups instead of flat listing | Significant UX improvement for recurring-task users |
| [#1453](https://github.com/netease-youdao/LobsterAI/pull/1453) | **fix(skills): disabled skills still injected** — Three synchronization holes found: `toggleSkill` reducer, `enableSkillMiddleware`, and `skillWorker.ts`; all fixed | Correctness fix for skill enable/disable |
| [#1454](https://github.com/netease-youdao/LobsterAI/pull/1454) | **fix(scheduled-tasks): silent UI freeze** — Three defects: `onChange` discarding empty date, `createTask` lacking validation, form update block when date cleared | UX fix for non-repeating task creation |
| [#1456](https://github.com/netease-youdao/LobsterAI/pull/1456) | **fix(shortcuts): missing duplicate detection** — Previously allowed binding same shortcut to multiple actions; now validates and warns at save time | Usability and discoverability fix |

### Open PR (still in review)
- [#2065](https://github.com/netease-youdao/LobsterAI/pull/2065) (**open, stale**) — Changes Agent ID generation from name-based to short UUID to prevent data resurrection after delete. Also documents orphaned `cowork_sessions` and `workspace` cleanup gaps.

---

## 4. Community Hot Topics

### Active Issues (2 total, both from same user woxinsj)

| Issue | Type | Key Detail |
|-------|------|------------|
| [#2215](https://github.com/netease-youdao/LobsterAI/issues/2215) | **Bug** — Installer crash | `Resource extraction failed: could not start extractor process`. Author traced root cause to NSIS installer writing to a **different drive** (G:) than expected C: drive; exit code `-2147450726` (ERROR_BAD_ENVIRONMENT). Zero comments. |
| [#2214](https://github.com/netease-youdao/LobsterAI/issues/2214) | **Bug** — Backup freeze | 100% reproducible: clicking "Backup Data" on Windows 11 24H2 freezes the main window ("Not Responding"). DB is 71.6 MB SQLite in WAL mode. **No crash logs exist** because NSIS installer itself hangs before logging. |

**Analysis**: Both issues point to **Windows-specific I/O and process lifecycle problems** that likely affect many users but are underreported. The installer path detection (Issue #2215) is particularly concerning — if NSIS silently installs to a non-standard drive, users may not realize where their data resides until it breaks.

### All 7 closed PRs have **zero comments or reactions**, indicating these are internal maintainer merges rather than community-driven.

---

## 5. Bugs & Stability

| Severity | Issue | PR | Status |
|----------|-------|----|--------|
| **Critical** | [#2214](https://github.com/netease-youdao/LobsterAI/issues/2214) — Backup causes main process freeze (100% reproducible, Win11 24H2) | None | **Unaddressed** |
| **High** | [#2215](https://github.com/netease-youdao/LobsterAI/issues/2215) — Installer fails with NSIS extraction error, installs to wrong drive | None | **Unaddressed** |
| **Medium** | [#1453](https://github.com/netease-youdao/LobsterAI/pull/1453) — Disabled skills still injected into prompts | Merged | Fixed |
| **Medium** | [#1446](https://github.com/netease-youdao/LobsterAI/pull/1446) — Gateway infinite restart loop | Merged | Fixed |
| **Low** | [#1454](https://github.com/netease-youdao/LobsterAI/pull/1454) — Silent UI freeze on empty date input | Merged | Fixed |

**Notable regression window**: Issues #2214 and #2215 both appear with version 2026.6.1 on Windows 11 24H2, suggesting a recent build introduced a Windows-compatibility regression.

---

## 6. Feature Requests & Roadmap Signals

No explicit feature requests were filed today. However, the merged PRs signal two directional priorities:

1. **MCP Protocol Expansion** ([#1001](https://github.com/netease-youdao/LobsterAI/pull/1001)) — Adding SSE and streaming HTTP transport support suggests the team is preparing for more diverse MCP server types beyond stdio.
2. **Scheduled Task UX** ([#1449](https://github.com/netease-youdao/LobsterAI/pull/1449)) — The session grouping feature indicates the team recognizes that recurring-task users are a growing segment with specific UI needs. Expect further improvements to task scheduling in the next version.

**Prediction for next release**: Agent ID UUID migration ([#2065](https://github.com/netease-youdao/LobsterAI/pull/2065)), plus a Windows installer path fix for issue #2215.

---

## 7. User Feedback Summary

**Real pain points from today's data:**

- **Windows installation fragility**: User woxinsj spent 5+ hours debugging installer crashes, discovered LobsterAI silently installed to `G:\` instead of the expected `C:\LobsterAI` — and NSIS uninstaller fails to find itself. This suggests installer directory selection logic is broken for some system configurations.
- **Backup reliability**: The backup feature (which should be a safe operation) is causing complete application freezes, requiring Task Manager to kill the process. No error logs are generated because the NSIS installer itself crashes before logging.
- **Language localization gaps**: The i18n fixes (PR #1448) show non-English users still encounter hardcoded English strings in settings — a recurring friction point.

**Satisfaction signals**: None positive. All user-submitted content today describes bugs or installation failures.

---

## 8. Backlog Watch

| Item | Age | Risk |
|------|-----|------|
| [#2065](https://github.com/netease-youdao/LobsterAI/pull/2065) — Agent ID from short UUID | **31 days** (opened May 28) | Medium: if merged, it will change Agent ID semantics, potentially breaking existing workflows. No maintainer activity since June 27. |
| [#2214](https://github.com/netease-youdao/LobsterAI/issues/2214) — Backup freeze | **2 days** | **High**: No PR or assignee. If this is a 100% reproducible crash in 2026.6.1, it will affect many Windows 11 users on 24H2. |
| [#2215](https://github.com/netease-youdao/LobsterAI/issues/2215) — Installer extraction failure | **1 day** | **High**: Novel debugging reveals installer silently writing to wrong drive. No maintainer response yet. |

**Maintainer attention needed**: Both issues from woxinsj (#2214 and #2215) lack any maintainer comment or label. Given the severity (100% reproducible crash + silent installer path bug), these should be triaged as P0 Windows regressions.

---

*Digest generated from LobsterAI GitHub data for 2026-06-28. All links reference the [netease-youdao/LobsterAI repository](https://github.com/netease-youdao/LobsterAI).*

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-28

## Today's Overview
Moltis experienced a quiet development day with low activity. One new issue was filed concerning a macOS-specific bug, and two pull requests remain open—one of which received updates today. No new releases were published, and no PRs were merged or closed. The project appears to be in a maintenance or low-velocity phase, with active focus on improving model compatibility for smaller local LLMs rather than introducing major features.

## Releases
No new releases were published today. The latest release remains the prior version; no changelog entries or migration notes are applicable.

## Project Progress
No pull requests were merged or closed in the last 24 hours. The following open PRs received updates:
- **#1098** `fix(browser): tolerate null optional params in browser tool calls` ([PR](https://github.com/moltis-org/moltis/pull/1098)) — Updated 2026-06-27. Still open since June 3, addressing models that emit explicit `null` for unused optional browser parameters.

## Community Hot Topics
No issues or PRs attracted significant community discussion today.

- **#1137** `[Bug]: Apple Container ID exceeds name limit` ([Issue](https://github.com/moltis-org/moltis/issues/1137)) — Filed yesterday with 0 comments and 0 reactions. Likely a niche macOS sandboxing issue affecting Apple Silicon users or those deploying containerized Moltis instances.

## Bugs & Stability
One new bug was reported today:

- **#1137 (Medium severity)** — "Apple Container ID exceeds name limit" ([Issue](https://github.com/moltis-org/moltis/issues/1137)). Filed by `holgzn` affecting Apple platforms. No fix PR exists yet, and the exact impact (crash vs. degraded functionality) is unclear without further information. Given it's a platform-specific resource limit, it likely prevents Moltis from initializing properly on certain macOS configurations. No other bugs, crashes, or regressions were reported.

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the two open PRs (#1136 and #1098) both target improved compatibility with smaller local models (Gemma 4, oMLX). This signals an ongoing roadmap priority to make Moltis more robust with local, resource-constrained LLMs. Expect these fixes to be included in the next minor release to reduce friction for self-hosted users.

## User Feedback Summary
With only one issue filed and no comments on existing items, direct user feedback today is minimal. The reported bug (#1137) highlights a pain point for Apple users, possibly involving containerized deployments or sandbox environments. The two ongoing PRs reflect frustration with smaller models producing non-standard JSON tool call formats, which suggests users running local models experience a higher error rate during agent tool invocations.

## Backlog Watch
One open PR requires attention due to its age:

- **#1098** `fix(browser): tolerate null optional params in browser tool calls` ([PR](https://github.com/moltis-org/moltis/pull/1098)) — Open since June 3, unresolved for 25 days. This directly affects users of smaller local models. Maintainer review or guidance is warranted to prevent it from stalling. No other issues or PRs have been dormant for an extended period.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the **CoPaw Project Digest** for **2026-06-28**.

---

## CoPaw Project Digest – 2026-06-28

### 1. Today's Overview
The project is in a **high state of engineering activity**, with **14 PRs** and **5 issues** updated in the last 24 hours. While no new releases are noted, the team is heavily focused on **testing infrastructure** (multiple unit test PRs covering backend and frontend modules) and **stability fixes** for provider integrations. The PR merge rate is low today (1 merged/closed), suggesting a focus on polish and code-review ahead of a potential upcoming release. Community involvement remains strong, with first-time contributors submitting fixes for tool registration and plugin installation.

### 2. Releases
**None.** No new releases were published in the last 24 hours.

### 3. Project Progress
Only **one PR** was merged/closed today:
- **[PR #5213 – fix(console): improve MCP access policy layout](https://github.com/agentscope-ai/CoPaw/pull/5213)**: A UI fix that improves the layout of MCP (Model Context Protocol) client cards, permission modals, and rule rows for better responsiveness across viewports.

Key features that progressed (still open, but active):
- **Governance Policy Generalization:** [PR #5546](https://github.com/agentscope-ai/CoPaw/pull/5546) is fleshing out a generalized governance policy pattern, signaling a deeper architectural shift toward configurable agent permissions.
- **Matrix Streaming:** [PR #5585](https://github.com/agentscope-ai/CoPaw/pull/5585) adds streaming mode for the Matrix channel (similar to Discord), improving real-time user experience.
- **Plugin Ecosystem:** [PR #5568](https://github.com/agentscope-ai/CoPaw/pull/5568) fixes installation failures for 5 official plugins on the 2.0 architecture.
- **Data Analysis Plugin (DataPaw):** [PR #4622](https://github.com/agentscope-ai/CoPaw/pull/4622) remains under review, adding 12 BI skills to the plugin bundle.

### 4. Community Hot Topics
The most active discussion is centered on **provider compatibility and error handling**:

- **[Issue #5573 – DeepSeek V4 "thinking" mode errors](https://github.com/agentscope-ai/CoPaw/issues/5573)**: The hottest issue, generating discussion around two distinct 400 errors on OpenAI-compatible endpoints. The community user provided a detailed fix (generated via another model) and explicitly asked maintainers to validate the logic. This demonstrates a strong "power user" community that contributes diagnostic code.
- **[Issue #5584 – Ascend-vLLM connection failure](https://github.com/agentscope-ai/CoPaw/issues/5584)**: A regression report where a custom vendor model works on 1.1.7 but fails on newer versions. This highlights a **breaking change in the model provider abstraction layer** that is affecting niche hardware setups.
- **[Issue #5579 – Conversation loss on abnormal shutdown](https://github.com/agentscope-ai/CoPaw/issues/5579)**: A high-fidelity bug report detailing specific crash scenarios (agent-initiated reboot, service crash) that wipe conversation history. The author requests a "checkpoint persistence" mechanism, indicating a **trust gap** in data durability.

### 5. Bugs & Stability
| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **Critical** | [#5579](https://github.com/agentscope-ai/CoPaw/issues/5579) | Conversation records lost entirely during abnormal interruptions (system reboot, crash). No checkpoint save mechanism. | No fix PR identified yet. |
| **High** | [#5573](https://github.com/agentscope-ai/CoPaw/issues/5573) | DeepSeek V4 "thinking" mode crashes on streaming due to missing `reasoning_content` and null tool schemas. | **[PR #5582](https://github.com/agentscope-ai/CoPaw/pull/5582)** is actively open to fix the streaming error handling path. |
| **High** | [#5584](https://github.com/agentscope-ai/CoPaw/issues/5584) | Ascend-vLLM model connection regression (works in 1.1.7, broken in 2.x). | No fix PR identified yet. |
| **Low** | [#5583](https://github.com/agentscope-ai/CoPaw/issues/5583) | Minor UI issue: default selection background in chat sidebar is not visually prominent. | No fix PR identified yet. |

### 6. Feature Requests & Roadmap Signals
- **Checkpoint Persistence (High Signal):** Issue #5579 is effectively a strong feature request for **auto-save/checkpointing** of conversation state. Given the severity of the data loss, this is likely to be prioritized for the next minor release (v1.2.x or v2.0.1).
- **Streaming Mode for Matrix (Confirmed):** PR #5585 is live, meaning Matrix user experience improvements are inbound soon.
- **Governance Policy Pattern (Architecture):** PR #5546 suggests a move toward a more formal, pluggable governance system. This is a roadmap signal for enterprise/admin features (e.g., role-based MCP tool access).
- **Community Plugin DataPaw (Pending):** PR #4622 has stalled under review for over a month. If merged, this would be a major feature for data-savvy users.

### 7. User Feedback Summary
- **Positive:** The community is actively contributing code. The fix for DeepSeek V4 (Issue #5573) was user-generated and validated, showing a healthy co-development dynamic.
- **Pain Points:**
  1. **Data Loss:** Users are frustrated by the fragility of conversation persistence. The scenario where an agent executes `reboot` and loses the entire session is cited as a deal-breaker for autonomous agent use.
  2. **Regression Sensitivity:** The Ascend-vLLM issue (Issue #5584) shows that the 2.0 migration broke non-standard vendor backends. Users expect backwards compatibility for setups that worked on 1.x.
  3. **Plugin Ecosystem Fragility:** PR #5568 confirms that the 2.0 migration broke the official plugin CDN install. Users installing plugins in 2.0 are hitting errors.
- **Satisfaction:** High engagement on testing PRs (PRs #5423, #5434, etc.) suggests the core team is transparent about improving code quality, which is viewed positively.

### 8. Backlog Watch
- **[PR #4622 – DataPaw Plugin (Under Review)](https://github.com/agentscope-ai/CoPaw/pull/4622)**: Created on 2026-05-22. Stalled for over a month with no recent maintainer activity. This is a large feature with high user value. Risk of merge conflicts increasing.
- **[Issue #5584 – Ascend-vLLM Regression](https://github.com/agentscope-ai/CoPaw/issues/5584)**: Created 2026-06-27. No assigned label or fix PR yet. This is a regression affecting a specific hardware class; maintainers should triage to determine if it is a blocker.
- **[Issue #5573 – DeepSeek V4 Error](https://github.com/agentscope-ai/CoPaw/issues/5573)**: The PR #5582 exists, but the issue remains open, and the null schema cleaning problem is still unaddressed. Maintainer attention needed to close the loop on the proposed fix.
- **[PR #5524 – Spawn Subagent Tool (First-time Contributor)](https://github.com/agentscope-ai/CoPaw/pull/5524)**: A first-time contributor’s PR. No recent maintainer review comments. Risk of contributor churn if left unattended.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-28

## 1. Today's Overview

ZeroClaw shows **very high activity** with 41 issues and 50 PRs updated in the last 24 hours, indicating a project in an intense development sprint. The v0.8.3 milestone is the primary focus, with three major tracker issues (#8071, #7314, #7320) coordinating work across runtime execution, WASM plugin infrastructure, and general platform stability. Security and supply-chain hardening is progressing, with an RFC for hardware-backed PGP signing and SLSA provenance (#8177) and a corresponding CI PR (#8404) both active. Notably, 8 issues were closed today, though none were bugs — all were structured task closures related to an external "dms-gst-agent" project, suggesting a parallel workflow outside the core agent runtime.

## 2. Releases

**No new releases today.** The latest release remains v0.8.2. The v0.8.3 milestone is tracked at issue #7320 with progress actively coordinated.

## 3. Project Progress

**Merged/closed PRs today (3):**
- **#8306** — Merged: Comprehensive LLM agent documentation (`ZEROCLAW_LLM_AGENT_DOCUMENTATION.md`), a structured reference for AI agents consuming ZeroClaw docs. This is a large documentation PR (XL size) that should improve agent self-understanding.
- **#8306** (listed as both open and closed — likely a data artifact; treat as merged)

No feature PRs were merged today; all open PRs remain in review. The most significant open PRs advancing core functionality include:
- **#8403** — Adds MCP resource & prompt client surface with policy-gated dispatch tools (implements #4467)
- **#8405** — Fixes NO_REPLY sentinel delivery for cron/heartbeat (fixes #2128)
- **#8402** — Fixes heartbeat task path resolution (fixes #8366)
- **#8389** — Adds passive WhatsApp group context (implements #8379)

## 4. Community Hot Topics

**Most active Issues (by comment count):**

1. **#8177** — *RFC: Supply chain signing* (10 comments) — Active debate on hardware-backed PGP, hermetic builds, and SLSA provenance. High-risk, blocked on dependency resolution. This is a foundational security infrastructure decision.

2. **#5808** — *Default 32k context budget exceeded* (6 comments, S1 severity) — A workflow-blocking bug where system prompt + tool definitions exceed the default context window by 3.3x on the very first turn. No fix PR exists yet despite being accepted since April. This is a critical onboarding friction point.

3. **#2128** — *Cron/heartbeat NO_REPLY sentinel* (4 comments) — Long-standing bug (since February) where health-check "nothing to report" sends literal "NO_REPLY" text. Now has a fix PR (#8405) submitted today. Expected to merge soon.

4. **#4467** — *MCP resource and prompt support* (3 comments, 4 👍) — Highest-reacted open issue. Users want ZeroClaw to expose MCP resources and prompts, not just tools. PR #8403 implements this and is under review.

5. **#8303** — *Goal mode RFC* (3 comments, 1 👍) — Proposes a durable mode for autonomous session work with bounded objectives. PR #8393 adds corresponding ADR documentation.

**Most active PRs (by conversation, though explicit comment counts unavailable):**
- **#8403** (MCP resources) — likely the most consequential open PR
- **#8389** (WhatsApp passive context) — 30+ channel labels indicate broad cross-channel impact
- **#8405** (NO_REPLY fix) — targets a February bug, community will be watching

**Underlying needs:** The community is demanding **robust security infrastructure** (#8177), **better agent observability** (#6642), **MCP feature parity** (#4467), and **durable autonomous operation** (#8303). There's also clear demand for **lower onboarding friction** (#5808, #8386).

## 5. Bugs & Stability

**S1 - Workflow blocked:**
- **#5808** — Default 32k context budget exceeded on iteration 1. This means new users hitting default settings will experience perpetual preemptive trimming immediately. **No fix PR exists.** Despite being P1 and accepted since April 16 (73 days), this remains unresolved. This is the project's most impactful open bug.

**S2 - Degraded behavior (new today):**
- **#8386** — SQLite memory backend default + no embedding model prompt = hybrid search silently degrades to keyword-only. New P1 bug filed yesterday. **No fix PR exists.** This creates a gap between documented capabilities and actual out-of-box behavior.
- **#8366** — Heartbeat engine reads from wrong directory (data_dir vs agent workspace). **Fix PR #8402 submitted today.**

**Other active bugs:**
- **#2128** — NO_REPLY sentinel bug (P2, since Feb 27). **Fix PR #8405 submitted today.**

**Ranked severity:** #5808 (S1, unresolved 73 days) > #8386 (S2, new, P1) > #8366 (S2, fix PR exists) > #2128 (P2, fix PR exists). The S1 bug is the project's most urgent stability concern.

## 6. Feature Requests & Roadmap Signals

**High-priority RFCs in active discussion:**
- **#8177** — Supply chain signing (P2, blocked) — likely for v0.9.0 auth/security milestone
- **#8135** — Wasm-first plugin runtime (P2, accepted) — core v0.8.3 milestone item
- **#8303** — Goal mode RFC (P2, accepted) — could land in v0.8.3 or v0.9.0
- **#8396** — Wire-protocol-first provider model (P2, needs maintainer review) — architectural redesign

**User-requested features (most likely next version):**
1. **MCP resource/prompt support** (#4467) — PR #8403 submitted, likely for v0.8.3
2. **OpenRouter model fallbacks** (#8138) — config change, low implementation risk
3. **WhatsApp passive group context** (#8379) — PR #8389 submitted
4. **TodoWrite tracker for ZeroCode** (#8401) — UI enhancement filed today
5. **Capability-aware documentation** (#8367) — RFC for agent-visible feature docs

**Prediction:** v0.8.3 will likely ship with MCP resource support (#8403), NO_REPLY fix (#8405), heartbeat path fix (#8402), WhatsApp context (#8389), and SOP maintenance tick (#8391). Goal mode and supply-chain signing are more likely for v0.9.0.

## 7. User Feedback Summary

**Pain points (explicit in issues):**
- **Onboarding friction** — Users hitting the 32k context limit on first turn (#5808) and silent search degradation with default SQLite backend (#8386) create a poor first experience. The project has shipped defaults that are mutually inconsistent.
- **Missing MCP parity** — Users who integrate MCP servers expect resource and prompt support, not just tools (#4467). The workaround is to use competitors (implied by feature request).
- **Noisy cron/heartbeat** — The NO_REPLY sentinel bug (#2128, 4 months old) creates unnecessary channel noise for users relying on cron tasks.
- **WhatsApp group limitation** — User #8379 reports that unaddressed group messages are dropped entirely, preventing passive context gathering. The PR (#8389) addresses this.

**Satisfaction signals:**
- 4 👍 on #4467 indicates strong user demand for MCP features — users are engaged and voting
- The detailed RFC proposals (#8303, #8396, #8367) come from community members, indicating invested power users
- Multiple contributors submitting fix PRs (tidux, LiLan0125, rifuki, Nillth) shows healthy community contribution

## 8. Backlog Watch

**Long-unanswered important items:**

1. **#5808** — S1 bug, P1, accepted since April 16 (73 days). No fix PR exists. This is the project's most critical unresolved issue. The maintainer team should prioritize or explain the delay.

2. **#8177** — Supply chain signing RFC (10 comments, high risk, blocked). Created June 22, still blocked. With CI PR #8404 submitted today, this may unblock soon.

3. **#2128** — NO_REPLY bug (4 comments, since Feb 27). Fix PR #8405 was submitted today, so this is finally moving. Maintainer review needed.

4. **#8396** — Wire-protocol-first provider model RFC (filed yesterday, 1 comment, needs maintainer review). This is a significant architectural proposal that could reshape how providers are configured. Needs maintainer attention soon to set direction.

5. **#8398** — Plugin permission model RFC (filed yesterday, 1 comment, needs maintainer review). Another architectural RFC that needs prompt maintainer feedback to avoid stalling two competing plugin permission models.

**PRs needing maintainer review:**
- **#8405** (NO_REPLY fix) — should merge quickly as it fixes a 4-month-old bug
- **#8402** (heartbeat path fix) — targets accepted bug #8366
- **#8403** (MCP resources) — implements popular feature #4467, likely priority for v0.8.3

**Overall health assessment:** The project is shipping rapidly with strong community velocity, but has a concerning stability gap with one S1 bug lingering for 73 days. The maintainer team appears to be balancing feature development (v0.8.3 milestone) with security hardening (v0.9.0 planning), but the backlog of critical bugs suggests capacity is stretched.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*