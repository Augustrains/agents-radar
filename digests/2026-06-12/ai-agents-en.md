# OpenClaw Ecosystem Digest 2026-06-12

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-12 02:10 UTC

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

Here is the OpenClaw project digest for June 12, 2026, based on the provided GitHub data.

---

### OpenClaw Project Digest
**Date:** 2026-06-12

### 1. Today's Overview

The OpenClaw project is experiencing an extremely high level of community activity, with 500 issues and 500 pull requests updated in the last 24 hours. This volume suggests a major release or significant breaking change, as the vast majority of issues remain open (476) while a critical mass of PRs await review (388 open vs. 112 merged/closed). The project is releasing multiple patches daily to address a wave of bugs and regressions, particularly around session management, authentication, and provider configuration. While no new releases were published today, the constant stream of fixes indicates a highly engaged but stressed maintenance cycle.

### 2. Releases

- **No new releases were published today.** The most recent stable version referenced in the data is `2026.6.5`, which appears to have introduced several regressions that are now being actively addressed in the current PRs.

### 3. Project Progress

Today, 112 PRs were either merged or closed, indicating a strong push to stabilize the codebase. Key areas of progress include:

- **Critical Bug Fixes:** Several high-priority fixes were advanced.
    - **PR #92225** (`Fix disabled heartbeat one-shot cron retries`) targets a core scheduling issue.
    - **PR #92178** (`fix(gateway): guard formatAuditList against non-string items`) prevents a WebSocket crash.
    - **PR #92181** (`fix(agents): align /btw model resolution with runtime aliases`) fixes a model routing issue.
- **Infrastructure Improvements:**
    - **PR #92311** (`ci: split plugin ClawHub publishing paths`) improves the CI/CD pipeline for plugin distribution.
    - **PR #68936** (Closed) (`Autofix: add PR review autofix pipeline + Windows daemon`) suggests a significant investment in automation for code review and Windows support.
- **Feature Enhancements:**
    - **PR #91632** (`feat: add tool search directory mode`) introduces a new mode for managing large tool catalogs.
    - **PR #86655** (`feat(claude): add claude-bridge app-server harness extension`) is a large PR that aims to improve native support for Anthropic models.

### 4. Community Hot Topics

The community is most vocal around stability, platform support, and security.

- **#75 [Linux/Windows Clawdbot Apps]** (109 comments, 79 👍): The most discussed issue remains the request for desktop apps on non-macOS platforms, highlighting a critical gap in the user experience for a large segment of users. [Issue #75](https://github.com/openclaw/openclaw/issues/75)
- **#39604 [Feature: tools.web.fetch.allowPrivateNetwork]** (13 comments, 9 👍): There is strong demand for the ability to allow the `web_fetch` tool to access private networks, indicating many users run OpenClaw within internal infrastructures or want it to interact with local services. [Issue #39604](https://github.com/openclaw/openclaw/issues/39604)
- **#6615 [Feature: Add denylist support for exec-approvals]** (7 comments, 7 👍): Users want more flexible security policies, specifically to "allow all except X" for command execution, rather than the current binary allow/deny system. [Issue #6615](https://github.com/openclaw/openclaw/issues/6615)
- **#20786 [Feature: Telegram Business Bot support]** (8 comments, 6 👍): There is a clear desire to leverage Telegram's Business features for bot interactions, suggesting a growing user base using the platform for professional use cases. [Issue #20786](https://github.com/openclaw/openclaw/issues/20786)

### 5. Bugs & Stability

The project is facing a significant number of P1 (critical) bugs, many of which are regressions from recent updates.

- **Critical (P1):**
    - **[Bug]: Agent replies to previous message instead of current message (session context confusion)** (#32296): A major user-facing bug causing conversations to become misaligned. [Issue #32296](https://github.com/openclaw/openclaw/issues/32296)
    - **[Bug]: Signal daemon stop() race condition on SIGUSR1 restart** (#22676): This critical race condition can lead to orphaned processes and service failures during configuration reloads. [Issue #22676](https://github.com/openclaw/openclaw/issues/22676)
    - **[Bug]: Bootstrap files in agentDir are silently ignored** (#29387): A key feature (per-agent bootstrapping) is completely broken, rendering agent-specific configs useless. [Issue #29387](https://github.com/openclaw/openclaw/issues/29387)
    - **Isolated cron consistently fails with "LLM request failed"** (#91363): Cron jobs, a core automation feature, are completely broken for many users. [Issue #91363](https://github.com/openclaw/openclaw/issues/91363)
    - **Several other P1 bugs** related to Telegram routing (#41165), multi-agent stability (#43367), and `exec` tool environment variable inheritance (#31583) are actively impacting users.

- **Regressions:**
    - **Bug: control ui requires device identity (use HTTPS or localhost secure context)** (#32473): A recent change has broken the control UI for users on certain network setups. [Issue #32473](https://github.com/openclaw/openclaw/issues/32473)
    - **"Cannot convert undefined or null to object" with Google Vertex** (#38327): Update `2026.3.2` broke compatibility with a major model provider. [Issue #38327](https://github.com/openclaw/openclaw/issues/38327)

**Mitigation:** Several PRs are in the pipeline to address these issues, including #92225 (heartbeat/cron), #92178 (gateway crash), and #91330 (message-tool replies).

### 6. Feature Requests & Roadmap Signals

The community is primarily requesting features that enhance security, multi-agent collaboration, and platform integration.

- **Likely for Next Version:**
    - **Masked Secrets / Memory Trust Tagging:** Issues #10659 and #7707 point to a deep concern about security and data poisoning. The high activity suggests a security-focused patch is imminent.
    - **Tiered Bootstrap File Loading:** The feature proposed in #22438 has a companion PR (#22439) that is still open, suggesting it is a strong candidate for the next major release.
    - **Improved Multi-Agent Orchestration:** Issue #35203 ([RFC] Multi-Agent Collaboration Enhancement) is a comprehensive proposal for capability profiling and shared memory, signaling a major roadmap focus.

- **Longer-Term Roadmap:**
    - **Platform Expansion:** The demand for Linux/Windows apps (#75) and prebuilt Android APKs (#9443) is clear but unresolved.
    - **Sandboxing & Permissions:** A cluster of issues (#7722, #39979, #37634) call for more granular and configurable filesystem and execution sandboxing.
    - **Backup/Restore Utility:** Issue #13616 requesting a standardized backup/restore mechanism is a sign of a maturing project being used in production environments.

### 7. User Feedback Summary

User sentiment is mixed, reflecting a project with powerful capabilities that is currently struggling with stability.

- **Pain Points:**
    1.  **Regressions:** The most common complaint, with multiple users reporting "worked before, now fails" scenarios after updating (#32473, #38327, #31583).
    2.  **Cron Job Instability:** Users are frustrated with cron jobs failing intermittently or consistently, which undermines a core "fire-and-forget" use case (#85888, #91363).
    3.  **Session Context Confusion:** The agent's failure to track the current conversation (#32296) is a critical source of dissatisfaction, making the agent feel unreliable.
    4.  **Lack of Platform Support:** Users feel left out without native apps for Linux and Windows, with some going so far as to create issues on behalf of others (e.g., issue #9443).
    5.  **File System & Security Complexity:** Users are finding the current security and sandboxing models too simplistic, leading to data loss (#40001) or security concerns (#10659).

- **Use Cases:**
    - Automation (cron jobs, sub-agents)
    - Multi-platform communication management (Telegram, iMessage, Slack)
    - Internal tooling and API orchestration (private networks, custom providers)
    - Development and coding assistance

### 8. Backlog Watch

A number of high-impact issues and PRs have been open for a long time without resolution, requiring maintainer attention.

- **Issues:**
    - **#75 [Linux/Windows Clawdbot Apps]**: Open for over 5 months with 109 comments. This is the single most requested feature and a major gap for the project's growth.
    - **#6731 [Feature: safe/unsafe ClawdBot]**: Open for over 4 months. The suggestion to rewrite in Rust is a significant architectural proposal that has not been formally addressed.
    - **#13616 [Add backup/restore utility]**: Open for 4 months. This is a critical production-readiness feature that remains unaddressed.

- **Pull Requests (Awaiting Review):**
    - **#75961 [Feat/discord slash command deploy 75888]**: Open for over a month. A large PR for a significant platform feature that has yet to be reviewed.
    - **#18860 [feat(agents): expose tools and their schemas via new after_tools_resolved hook]**: Open for nearly 4 months. This plugin API enhancement would greatly improve the ecosystem. It receives periodic updates but lacks a final decision.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report based on the provided community digest summaries.

---

### Cross-Project Comparison Report: AI Agent Open-Source Ecosystem
**Date:** 2026-06-12

#### 1. Ecosystem Overview

The personal AI assistant open-source landscape is experiencing an intense, dual-paced cycle of innovation and stabilization. A major architectural shift toward **multi-agent runtimes** and **agent collaboration** is underway, with several projects launching or heavily developing this paradigm. However, this rapid iteration has created significant stability debt, particularly in desktop application reliability and session management. The ecosystem is also converging on critical needs for more robust security models, persistent long-term memory, and seamless multi-platform support, indicating a market maturing from experimental tooling to production-ready personal infrastructure.

#### 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Release Status | Health Score | Activity Tier |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | No release (Stabilizing `2026.6.5`) | 🟡 Moderate | Ultra-High |
| **CoPaw** | 33 | 42 | **2 patch releases today** (`.post1`, `.post2`) | 🟠 Stressed | High |
| **IronClaw** | 30 | 47 | No release (Prepping "Reborn") | 🟢 Strong | High |
| **Hermes Agent** | 50 | 50 | No release (v0.15.1 latest) | 🟡 Moderate | High |
| **LobsterAI** | 2 | 19 | No release (Prepping next major) | 🟢 Strong | High |
| **ZeroClaw** | 50 | 50 | **v0.8.0 released today** | 🟠 Turbulent | High |
| **PicoClaw** | 6 | 31 | Nightly build (v0.2.9-nightly) | 🟢 Strong | High |
| **NanoBot** | 4 | 19 | No release | 🟡 Moderate | Medium |
| **NanoClaw** | 2 | 15 | No release | 🟢 Strong | Medium |
| **Moltis** | 1 | 1 | No release | 🟢 Stable | Low |
| **NullClaw** | 1 | 0 | No release | 🟢 Stable | Low |
| **TinyClaw** | 0 | 0 | No release | 🟢 Dormant | None |
| **ZeptoClaw** | 0 | 0 | No release | 🟢 Dormant | None |

**Key Observations:**
- **OpenClaw** dominates raw activity volume, but the 500/500 ratio is a signal of maintenance overload rather than healthy progress.
- **ZeroClaw** is the most volatile, with a major release creating a wave of critical bugs.
- **CoPaw** is in full firefighting mode, releasing two patches in one day to address a desktop client crisis.

#### 3. OpenClaw's Position

**Advantages vs Peers:**
- **Ecosystem Size & Mindshare:** OpenClaw is the clear market leader by community activity, acting as the core reference implementation. Its issue volume is an order of magnitude larger than most peers, giving it a vast feedback loop.
- **Plugin Ecosystem:** Its dedicated CI for plugin distribution (PR #92311) and tool search directory mode (PR #91632) suggest a more mature and organized ecosystem for extensions compared to most peers.
- **Third-Party Integration:** Strong native support for major platforms (Telegram Business, Claude bridge) is broader than more niche projects like Moltis or NullClaw.

**Technical Approach Differences:**
- **Multi-Agent Architecture:** Unlike ZeroClaw (which just launched its multi-agent daemon) or Hermes Agent (which uses a sub-agent pattern), OpenClaw appears to be evolving more organically from a single-agent core, with features like "Agent Collaboration Bus" (seen in PicoClaw) being a key future direction.
- **Stability is a Liability:** While powerful, OpenClaw suffers from a high regression rate and a backlog of critical bugs (e.g., session confusion, broken cron jobs). This contrasts sharply with the more disciplined, focused bug-fixing cadence seen in NanoClaw or the controlled "Reborn" rollout of IronClaw.

**Community Size Comparison (Proxy: Issue/PR Volume):**
- **Tier 1 (10,000+):** OpenClaw
- **Tier 2 (100-1,000):** Hermes Agent, ZeroClaw, CoPaw, IronClaw
- **Tier 3 (10-100):** PicoClaw, LobsterAI, NanoBot, NanoClaw
- **Tier 4 (0-10):** Moltis, NullClaw, TinyClaw, ZeptoClaw

#### 4. Shared Technical Focus Areas

Multiple projects are independently converging on the same set of requirements, validating these as industry-wide needs:

1.  **Multi-Agent Orchestration & Collaboration:** **PicoClaw** (Agent Collaboration Bus PR #2937), **LobsterAI** (Issue #1462 for multi-agent rooms), **ZeroClaw** (v0.8.0 multi-agent daemon), and **OliveAlpaca** (swarm collaboration request) are all building or requesting the ability to coordinate specialist agents.
2.  **Long-Term Memory & Learning:** **ZeroClaw** ("Dream Mode" #5849) and **NanoClaw** (Memory System Redesign #1356) are both tackling the problem of moving beyond ephemeral context windows to persistent, reflective agent memory.
3.  **Granular Security & Permissions:** **OpenClaw** (denylist for exec-approvals #6615, private network access #39604), **ZeroClaw** (broken `tool_filter_groups` #6699), and **PicoClaw** (dynamic MCP headers #2696) all highlight a move from binary allow/deny to nuanced, context-aware security policies.
4.  **Desktop Client Reliability:** **CoPaw** (critical desktop crashes), **Hermes Agent** (desktop UI crashes), and **OpenClaw** (dev build failures) are all struggling with the stability of their desktop applications, a key friction point for end-users.
5.  **Model Capability Introspection:** **PicoClaw** (Issue #3108 on image hallucination with non-vision models) and **IronClaw** (handling invalid model config as tool failure) both point to a need for the agent to understand its own model's capabilities before calling tools.

#### 5. Differentiation Analysis

| Feature Axis | OpenClaw | ZeroClaw | IronClaw | NanoBot | LobsterAI | CoPaw |
|---|---|---|---|---|---|---|
| **Core Architecture** | Single-agent, evolving to multi-agent | **Multi-agent daemon (v0.8.0)** | Single-agent "Reborn" | Single-agent SDK | Single-agent | Single-agent, planning AgentScope 2.0 |
| **Target User** | Power users / developers | Advanced deployers / fleet managers | Enterprise operators | Embedded developers | Enterprise / Chinese market | Power users / self-hosters |
| **Key Feature** | Plugin ecosystem / Claude bridge | Agent fleets / "Dream Mode" | Configuration-as-Code / Observability | **Skills/Provider modularity** | **Computer Use MVP** / Real-time ASR | Qwen model integration / Langfuse |
| **Primary Channel** | Telegram / iMessage / Slack | WhatsApp / Cron | Slack / NEAR AI | Slack / SiliconFlow | Feishu / Gmail | DingTalk / Telegram |
| **Stability Posture** | Regressive / Firefighting | **Turbulent (just released)** | Controlled rollout | Moderate | Controlled | Crisis mode |

#### 6. Community Momentum & Maturity

- **Rapidly Iterating (High Risk/High Reward):** **ZeroClaw** and **CoPaw** are burning hard. ZeroClaw is pushing a major architectural boundary, while CoPaw is trying to stabilize a flagship release. Both risk alienating users with instability but may leapfrog competitors in capability.
- **Controlled Build-Out:** **IronClaw** and **PicoClaw** are executing disciplined development sprints. They are not releasing as frequently, but their code quality and focus on infrastructure (CI, release gates, QA automation) suggest a path to a more mature, production-grade product.
- **Feature Ramp-Up:** **LobsterAI** and **NanoBot** are adding distinct, high-value features (Computer Use, ASR, model failover) without major stability crises. They are carving out specific niches rather than competing on core architecture.
- **Stabilizing & Consolidating:** **OpenClaw** and **Hermes Agent** have vast feature sets but are now paying the price of complexity with high regression rates. Their next phase must be a dedicated stability sprint to maintain user trust.
- **Low Activity / Niche:** **Moltis**, **NullClaw**, **TinyClaw**, and **ZeptoClaw** are either dormant or serving very specific use cases. They are not driving ecosystem trends.

#### 7. Trend Signals

1.  **The Rise of the "Agent Fleet":** The multi-agent pattern is the single strongest signal in the ecosystem. Projects are moving beyond single-assistant paradigms to systems of collaborating specialized agents. For developers, this means building skills that are composable and designed to be orchestrated by a supervisor agent.
2.  **Security as a First-Class Feature, Not an Afterthought:** The community's frustration with broken tool filters and lack of granular permissions is a clear market signal. The future of agent platforms will be defined by their security model. Developers should prepare for more complex and mandatory security configuration.
3.  **The "Desktop Reliability" Tax:** The most common user complaint across all projects is desktop application crashes. This is a universal pain point that any AI agent developer targeting end-users must prioritize. It is a hygiene factor, not a differentiator.
4.  **Local Model Support is Not a Nice-to-Have:** The frustration with regressions in local model support (CoPaw, NullClaw) and the demand for configurable timeouts (NanoBot) confirms that a significant segment of the user base is running private, self-hosted LLMs. This trend towards data sovereignty and cost control is persistent.
5.  **Context Management is the New Bottleneck:** As agents grow more complex, the naive "stuff everything into a 32k token window" approach is breaking. The community is demanding context compression (CoPaw's "Headroom"), intelligent memory consolidation (ZeroClaw's "Dream Mode"), and session stability. The next frontier of agent performance will be in sophisticated context management systems.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-12

## 1. Today's Overview

The NanoBot project is in a period of **high active development**, with 19 pull requests updated in the last 24 hours (13 open, 6 merged/closed) and 4 issues updated (2 closed, 2 open). No new releases were published, but the PR pipeline is dense with significant feature work, bug fixes, and infrastructure improvements. The community is contributing actively, particularly around session stability, multi-provider support, and sandbox compatibility. The maintainer team appears responsive, with several AI-assisted PRs and quick turnarounds on validated bugs.

## 2. Releases

**No new releases** as of 2026-06-12. The absence of a release cadence suggests the project may be accumulating changes for a larger release, or is in a post-release stabilization phase. Users tracking the issue #4233 (version display in WebUI) may appreciate a tagged release for easy version reference.

## 3. Project Progress

**6 pull requests were merged or closed today:**

| PR | Description | Type |
|---|---|---|
| [#4289](HKUDS/nanobot PR #4289) | Slack channel: add `groupRequireMention` for finer-grained allowlist control | Feature |
| [#4281](HKUDS/nanobot PR #4281) | SiliconFlow transcription provider registration | Feature |
| [#4257](HKUDS/nanobot PR #4257) | Fix `split_message` to be fenced-code-block-aware | Bug Fix |
| [#4020](HKUDS/nanobot PR #4020) | Make stream-idle timeout configurable per-provider | Enhancement |
| [#4298](HKUDS/nanobot PR #4298) | Worktree feature + Hermes research doc | Documentation |
| [#4297](HKUDS/nanobot PR #4297) | Worktree feature + Hermes research doc (duplicate) | Documentation |

**Notable closed PRs reflecting project direction:**
- **Slack mention control** ([#4289](HKUDS/nanobot PR #4289)): Adds nuanced channel-level mention requirements, moving beyond binary allowlist/blocklist.
- **Transcription expansion** ([#4281](HKUDS/nanobot PR #4281)): SiliconFlow as a new transcription provider, reusing the existing OpenAI-compatible adapter.
- **Stream timeout flexibility** ([#4020](HKUDS/nanobot PR #4020)): Addresses a long-standing pain point for local LLM users where the 90s default timeout was too aggressive.

## 4. Community Hot Topics

### Most Active Issues
- [#4233](HKUDS/nanobot Issue #4233) **(CLOSED)** — "Show the nanobot version in the webui somewhere" — 2 comments, low emoji count, but the underlying need for user-facing version awareness is clear.
- [#4305](HKUDS/nanobot Issue #4305) **(OPEN)** — "Multiple custom providers: ?" — 0 comments yet but was created yesterday; the topic (multi-provider support) is also being addressed in PR [#3239](HKUDS/nanobot PR #3239) (open since April).

### Most Active Pull Requests
- [#4306](HKUDS/nanobot PR #4306) **(OPEN, newest)** — Fix orphaned tool results in session history — addresses a session-level data integrity issue affecting API compatibility.
- [#4296](HKUDS/nanobot PR #4296) **(OPEN)** — Python SDK expansion — 592 lines changed, expands from a minimal facade to a full developer API with session/memory/runtime controls.

**Underlying needs:** There is clear community demand for **session stability** (orphaned tool results, subagent lifecycle, cron job completion) and **provider flexibility** (multiple custom providers, configurable timeouts, new transcription backends). The multi-provider discussion in #4305 and #3239 suggests the single "custom" provider slot is a bottleneck for users with complex infrastructure.

## 5. Bugs & Stability

### High Severity
1. **MCP Gateway Crash on Reconnect** ([#4302](HKUDS/nanobot Issue #4302), OPEN) — `nanobot gateway` crashes with `RuntimeError` when a `streamableHttp` MCP server session terminates and reconnects. A fix PR exists ([#4303](HKUDS/nanobot PR #4303)) that closes tracked generators during `_close_server`.
2. **Sandbox Failure on Ubuntu 24.04** ([#4236](HKUDS/nanobot Issue #4236), CLOSED) — Bubblewrap sandbox fails on modern Linux distributions with restricted user namespaces. Likely closed with a documentation or config workaround.

### Medium Severity
- **Orphaned Tool Results** ([#4306](HKUDS/nanobot PR #4306)) — Session history can contain `role:"tool"` messages with no matching `tool_call_id`, breaking strict OpenAI/Anthropic API compatibility. PR #4306 provides a fix.
- **Subagent Task Completion Gap** ([#4304](HKUDS/nanobot PR #4304)) — Cron jobs marking complete before spawned subagents finish. Fix is in PR review.
- **Fenced Code Block Splitting** ([#4257](HKUDS/nanobot PR #4257)) — Message splitting landed inside code fences, producing broken HTML. Now merged.

### Low Severity
- **Codex Duplicate Reasoning Items** ([#4021](HKUDS/nanobot PR #4021), OPEN) — Occasional `400 Duplicate item found` errors in OpenAI Codex provider. Fix in PR form but not yet merged.

**Overall stability assessment:** No confirmed regressions in the last 24 hours. The MCP reconnect crash is the most urgent open bug, with a targeted fix under review.

## 6. Feature Requests & Roadmap Signals

### Likely in Next Version
- **Multi-provider support** (PR [#3239](HKUDS/nanobot PR #3239), issue [#4305](HKUDS/nanobot Issue #4305)) — the most requested feature in the current pipeline. Multiple users need more than one "custom" or "openai" provider configuration.
- **Skills caching** (PR [#4301](HKUDS/nanobot PR #4301)) — Performance improvement to avoid repeated directory scans. Low risk, high value for large skill sets.
- **Cron job session binding** (PR [#4299](HKUDS/nanobot PR #4299)) — Scheduled automations will be bound to sessions and defer until idle, a significant UX improvement for cron users.

### Emerging Signals
- **Desktop app removal** (PR [#4294](HKUDS/nanobot PR #4294)) — The Electron-based desktop app is being moved out of the core repo, suggesting a cleaner separation between core SDK and platform-specific UIs.
- **Python SDK expansion** (PR [#4296](HKUDS/nanobot PR #4296)) — Moving from a minimal `bot.run()` facade to richer runtime control signals a push toward developer-oriented API maturity.
- **Gateway CLI management** (PR [#3538](HKUDS/nanobot PR #3538), OPEN since April) — Start/stop/restart commands for the gateway process, stagnating but needed for operational deployments.

## 7. User Feedback Summary

### Pain Points Expressed
- **Version unawareness** (#4233): Users want version shown in WebUI, plus upgrade notifications.
- **Ubuntu 24.04 sandbox incompatibility** (#4236): Production deployment friction on modern systems.
- **MCP reconnect failures** (#4302): Disrupts running gateway instances; a stability blocker.
- **Cron job subagent lifecycle** (#4290, referenced in #4304): Jobs finish prematurely, work is lost.
- **Provider flexibility** (#4305, #3239): Single "custom" provider slot insufficient for multi-endpoint setups.

### Satisfaction Signals
- **Stream timeout configurability** (PR [#4020] closed): Users running local LLMs (Ollama, LM Studio) will benefit from per-provider timeout tuning.
- **Slack mention controls** (PR [#4289] merged): More granular channel-level @mention requirements, directly responding to enterprise Slack deployment feedback.
- **SiliconFlow transcription** (PR [#4281] merged): New provider option without complex configuration.

## 8. Backlog Watch

### Issues Needing Maintainer Attention
- [#4305](HKUDS/nanobot Issue #4305) — "Multiple custom providers" — Created 2026-06-11, zero comments/engagement from maintainers. The topic has a stale PR ([#3239](HKUDS/nanobot PR #3239), open since April 17) that may need rebasing or decision.

### Stale PRs of Concern
- [#4021](HKUDS/nanobot PR #4021) — Codex dedup fix (AI-assisted) — open since May 27, no merge activity. 16 days stale. The bug it fixes (400 errors) is reproducible and annoying for Codex users.
- [#3538](HKUDS/nanobot PR #3538) — Gateway CLI commands — open since April 29, 44 days stale. Essential for operational users; maintainer review needed.
- [#3239](HKUDS/nanobot PR #3239) — Multi-provider support — open since April 17, 56 days stale. Conflicts with newly opened issue #4305 suggesting the community is not giving up on this feature.

### Recommendations
- **Prioritize session stability fixes**: MCP reconnect (#4302/#4303) and orphaned tool results (#4306) directly impact production reliability.
- **Resolve multi-provider design**: The community is clearly asking via both an old PR and a new issue. A decision (accept, redesign, or reject with explanation) would reduce uncertainty.
- **Review the stale gateway CLI PR** (#3538): Gateway management is a common operational need; leaving this unaddressed may push users to alternative solutions.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-06-12  
**Data Source:** GitHub (github.com/nousresearch/hermes-agent)

---

## 1. Today's Overview

Hermes Agent shows **high activity** today with 50 issues and 50 PRs updated in the last 24 hours. The project maintains a strong development cadence with 9 closed/merged PRs today and 8 issues resolved. However, the open-to-closed ratio is concerning: 42 open issues vs 8 closed, and 44 open PRs vs 6 merged/closed. The most critical development is a **P1 severity bug** (Issue #44585) involving cron jobs inheriting paid provider state, potentially causing unauthorized spending. The community is actively contributing, with 14 new PRs opened today alone addressing bugs from Discord reconnection failures to desktop build failures. No new releases were published.

---

## 2. Releases

**No new releases today.** The latest available version remains v0.15.1 (2026.5.29) as noted in Issue #37812.

---

## 3. Project Progress

**Merged/Closed PRs today (6 total):**

- **#43660** — `fix(desktop): persist composer drafts across reloads` — Prevents user prompt loss on app reload/crash
- **#40674** — `fix(desktop): survive app/CLI version skew` — Fixes desktop boot failure when CLI and app versions mismatch; caps desktop.log growth
- **#44169** — `feat(desktop): auto-detect RTL paragraph direction in chat` — Arabic/Hebrew/Persian/Urdu support
- **#44065** — `feat(desktop): per-message automatic RTL/bidi text direction` — Companion RTL fix for individual messages
- **#44192** — `feat(feishu): add cardkit v1 streaming card support (schema 2.0)` — Real-time streaming output for Feishu
- **#44571** — `fix(desktop): harden dictation and native alerts` — Closed by author as not upstream-mergeable

**Feature advancements today:**
- **RTL/bidi text support** — Two PRs merged for desktop chat Arabic/Hebrew rendering
- **Feishu streaming cards** — CardKit v1 integration for real-time AI output in Feishu
- **Composer draft persistence** — User prompts survive app reloads

---

## 4. Community Hot Topics

| Issue/PR | Comments | Reactions | Topic |
|----------|----------|-----------|-------|
| [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) | 11 | 0 🔥 | Skills index stale/degraded (automated watchdog) |
| [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) | 7 | 3 👍 | Model switch as agent-callable tool for self-routing |
| [#37812](https://github.com/NousResearch/hermes-agent/issues/37812) | 7 | 4 👍 | Desktop app UI not rendering approval prompts |
| [#38945](https://github.com/NousResearch/hermes-agent/issues/38945) | 6 | 0 | MCP tools not exposed in Desktop/TUI |
| [#44121](https://github.com/NousResearch/hermes-agent/issues/44121) | 6 | 0 | `npm ci` fails on clean checkout |

**Analysis:** The most active issue (#38240) is an automated watchdog failure — the skills index hasn't been refreshed, indicating a potential CI/CD pipeline issue. The most *user-engaged* topic is #16525 (autonomous model routing), which garnered 3 upvotes — users want the agent to self-select models based on task complexity. #37812 (approval prompts not rendering) has 4 👍, suggesting desktop UX is a pain point.

---

## 5. Bugs & Stability

### P1 Critical
- **[#44585](https://github.com/NousResearch/hermes-agent/issues/44585)** — *Cron inherits temporary paid provider state* — Cron jobs continued making paid calls after operator attempted to stop them. **Real spending risk.** No fix PR yet.
  
### P2 High
- **[#44541](https://github.com/NousResearch/hermes-agent/issues/44541)** — *Discord cron delivery fails after reconnect* — Fix PR [#44599](https://github.com/NousResearch/hermes-agent/pull/44599) opened today
- **[#44560](https://github.com/NousResearch/hermes-agent/issues/44560)** — *Model options handler blocks on sync HTTP calls* — Fix PR [#44598](https://github.com/NousResearch/hermes-agent/pull/44598) opened today
- **[#44580](https://github.com/NousResearch/hermes-agent/issues/44580)** — *`hermes update` reports success when desktop rebuild fails* — Fix PR [#44591](https://github.com/NousResearch/hermes-agent/pull/44591) opened today
- **[#44499](https://github.com/NousResearch/hermes-agent/issues/44499)** — *Desktop agent ignores explicit MCP browser config* — Uses built-in browser tools instead
- **[#40344](https://github.com/NousResearch/hermes-agent/issues/40344)** — *WebUI profile state.db not created for new profiles* — Session data leaks to main DB
- **[#43657](https://github.com/NousResearch/hermes-agent/issues/43657)** — *aiohttp ClientSession leak after auxiliary tasks* — Resource leak with warnings
- **[#44497](https://github.com/NousResearch/hermes-agent/issues/44497)** — *Duplicate responses to same message* — Context not cleared or thread cross-fire

### P3 Medium
- **Desktop UI crashes**: [#44562](https://github.com/NousResearch/hermes-agent/issues/44562), [#41693](https://github.com/NousResearch/hermes-agent/issues/41693) — `tapClientLookup: Index X out of bounds` renderer crashes (white screen)
- **IME composition bug**: [#40544](https://github.com/NousResearch/hermes-agent/issues/40544) — Enter during IME still submits inline edit
- **Dashboard CLI bugs**: [#44567](https://github.com/NousResearch/hermes-agent/issues/44567) — Commands block while dashboard runs
- **Folder attach fails**: [#44581](https://github.com/NousResearch/hermes-agent/issues/44581) — Drag-and-drop errors, copy-paste silently ignored
- **/undo not working**: [#44543](https://github.com/NousResearch/hermes-agent/issues/44543) — Slash command has no effect on Windows
- **Update deadlock**: [#44557](https://github.com/NousResearch/hermes-agent/issues/44557) — Studio updater killed when parent exits
- **Plugin hooks**: [#44582](https://github.com/NousResearch/hermes-agent/issues/44582) — `pre_tool_call` hook never called
- **Web search backend**: [#43883](https://github.com/NousResearch/hermes-agent/issues/43883) — `anysearch` backend silently falls back to DuckDuckGo

**Positive signal:** Most P2 bugs already have fix PRs opened today, indicating rapid response from maintainers.

---

## 6. Feature Requests & Roadmap Signals

### Likely for Next Release:
1. **[#16525](https://github.com/NousResearch/hermes-agent/issues/16525)** — *Agent-callable model_switch tool* — High engagement (3 👍), enables autonomous complexity-based routing. Core architectural improvement.
2. **RTL/Bidi support** — Two PRs merged today (#44169, #44065). Being actively deployed.
3. **Rust-backed install manager** — PR [#44067](https://github.com/NousResearch/hermes-agent/pull/44067) adds install/repair/uninstall orchestration. Suggests future focus on distribution quality.
4. **Feishu CardKit streaming** — PR [#44594](https://github.com/NousResearch/hermes-agent/pull/44594) for real-time streaming in Feishu. Shows enterprise platform investment.

### Needs Maintainer Sign-off:
- **[#14285](https://github.com/NousResearch/hermes-agent/issues/14285)** — *Xiaomi MiMo token plan support* — Open since April, 2 👍. Provider diversity request.
- **[#44548](https://github.com/NousResearch/hermes-agent/issues/44548)** — *`.hermes/.env` not propagated to MCP servers* — Causes credential duplication friction. Environment management improvement.
- **[#44513](https://github.com/NousResearch/hermes-agent/issues/44513)** — *Docs: local OpenAI-compatible endpoints in model picker* — Documentation request for providers pattern.

### Predictions:
- **Version 0.16.0** will likely include: RTL support, composer draft persistence, Feishu streaming, and the Rust manager for Hermes Desktop updates.
- **Model routing improvements** (Issue #16525) could be a headliner feature for the next major release, as it fundamentally changes agent autonomy.

---

## 7. User Feedback Summary

**Positive Signals:**
- 3 PRs merged addressing desktop RTL support — multilingual users are being heard
- Composer draft persistence (#43660) addresses a common "lost work" frustration
- Discord rate-limit retry (#44542) shows responsiveness to connectivity issues

**Pain Points (Repeated across issues):**

| Category | Frequency | Symptoms |
|----------|-----------|----------|
| **Desktop UI instability** | 5+ issues | `tapClientLookup` crashes, folder picker clipping, IME bugs, /undo broken |
| **Update/install failures** | 4 issues | Deadlocks, false success reports, background process conflicts |
| **MCP tool inconsistency** | 3 issues | Browser MCP ignored, tools not exposed, env vars not propagated |
| **Provider/model issues** | 3+ issues | Token plan missing, model picker gaps, pay-as-you-go limitations |
| **Cross-platform regressions** | 2 issues | Linux setup incomplete, Windows dashboard blocking |

**Notable user quotes (paraphrased from issues):**
- "Todoist workflows are materially worse than in Claude Code or Codex" (#38945)
- "Real spending on a provider I had already attempted to shut off" (#44585 — P1 billing bug)
- "Neither normal nor remote help. Complete deadlock." (#44557 — update deadlock)

**Overall Sentiment:** Users are pushing Hermes hard (many feature requests, complex workflows) but hitting desktop reliability issues and environment configuration friction. The active community engagement (14+ new PRs today from community contributors) suggests strong developer buy-in, but end-user experience needs stability improvements.

---

## 8. Backlog Watch

| Issue | Age | Category | Why It Matters |
|-------|-----|----------|----------------|
| [#16525](https://github.com/NousResearch/hermes-agent/issues/16525) | 46 days (Apr 27) | Feature | 3 👍, 7 comments — Model routing is a core architecture decision |
| [#14285](https://github.com/NousResearch/hermes-agent/issues/14285) | 50 days (Apr 23) | Feature | Xiaomi provider support — Cloud market expansion |
| [#37812](https://github.com/NousResearch/hermes-agent/issues/37812) | 9 days | Bug (P2) | Desktop approval prompts broken — security/UX blocker |
| [#38945](https://github.com/NousResearch/hermes-agent/issues/38945) | 8 days | Bug (P2) | MCP tools not reliable — core integration path broken |
| [#38240](https://github.com/NousResearch/hermes-agent/issues/38240) | 9 days | Infrastructure | Skills index stale — automated CI/CD failure signal |
| [#40344](https://github.com/NousResearch/hermes-agent/issues/40344) | 6 days | Bug (P2) | Profile data isolation — session data leak |
| [#40544](https://github.com/NousResearch/hermes-agent/issues/40544) | 6 days | Bug (P3) | IME inline edit — blocks East Asian users from full editing |
| [#41693](https://github.com/NousResearch/hermes-agent/issues/41693) | 4 days | Bug (P3) | Desktop renderer crash — user-facing stability issue |

**Critical backlog item:** [#38240 — Skills Index Watchdog](https://github.com/NousResearch/hermes-agent/issues/38240) is a CI/CD pipeline health issue, not a user-facing bug, but it affects all documentation and skills discovery. If the skills index remains stale, new features won't be discoverable through `/docs/skills`.

---

**Project Health Assessment: 🟡 MODERATE**  
High velocity on bug fixes (especially for today's P2 issues), strong community contributions, but accumulating desktop stability debt and one P1 billing-critical bug. The open PR/issue ratio (44:42) suggests maintainer bandwidth may be stretched. Next release should focus on desktop reliability and the model routing feature to address the top user requests.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date**: 2026-06-12  
**Analysis Period**: Last 24 hours

---

## Today's Overview

PicoClaw shows **high development activity** today with 31 pull requests updated and 1 new nightly release. The project maintains strong momentum with 6 issues updated (3 open, 3 closed) and 18 PRs merged or closed, indicating sustained maintenance velocity. The codebase is undergoing **significant dependency upgrades** (10+ Dependabot PRs) alongside targeted bug fixes and feature work. The nightly build `v0.2.9-nightly.20260612.413d3749` signals continued pre-release iteration. Notably, several long-standing bugs (tool_calls dropping, Windows path issues) have fix PRs active, suggesting upcoming stability improvements. Overall project health appears **robust** with balanced attention to new features, bug fixes, and operational hardening.

---

## Releases

**New Release**: `nightly` build — `v0.2.9-nightly.20260612.413d3749`  
- **Type**: Automated nightly build (may be unstable)  
- **Changelog**: [Compare v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)  
- **No breaking changes or migration notes documented** for this release.  
- **Recommendation**: Use for testing only; production users should stay on stable releases.

---

## Project Progress

### Merged/Closed PRs Today (18 total)

**Critical Bug Fixes:**
- [#2957](https://github.com/sipeed/picoclaw/pull/2957) — **fix(channels): prevent tool_calls from being dropped during streaming** — Resolves issue #2958 where `tool_calls` messages were lost on consecutive requests via pico channel. Fix excludes tool_calls from auxiliary message filtering.

**Security & Stability:**
- [#2955](https://github.com/sipeed/picoclaw/pull/2955) — **fix: verify process identity in singleton PID check** — Prevents startup failures when PID file contains PID reused by unrelated processes (e.g., `systemd-resolved`).
- [#3060](https://github.com/sipeed/picoclaw/pull/3060) — **fix: use `%w` for error wrapping** — Fixes broken `errors.Is`/`errors.As` chains in skills helper, handles uncaught `json.MarshalIndent` error.

**Configuration & Channel Fixes:**
- [#2956](https://github.com/sipeed/picoclaw/pull/2956) — **fix: preserve channel enabled state when merging security.yml** — Prevents channels from being incorrectly disabled after security credentials load.
- [#2934](https://github.com/sipeed/picoclaw/pull/2934) — **fix(channels): allow WhatsApp native mode with `use_native` flag** — Enables native whatsmeow mode when `bridge_url` is not configured.
- [#3067](https://github.com/sipeed/picoclaw/pull/3067) — **fix: add `DmScope` field to SessionConfig** — Persists the "Session Scope" setting across page reloads.
- [#2947](https://github.com/sipeed/picoclaw/pull/2947) — **fix: correct `claude-sonnet-4.6` model ID to use hyphens** — Resolves HTTP 404 errors on first use with erroneous Anthropic configuration.

**MCP & Integration:**
- [#2696](https://github.com/sipeed/picoclaw/pull/2696) — **feat(mcp): support per-request dynamic headers from channel context** — Channels can now forward HTTP headers (e.g., Authorization) to MCP servers per-request via `InboundContext.Raw`.

**Dependency Upgrades (10+ merged):**
- AWS SDK v2 config and core packages updated
- `github.com/modelcontextprotocol/go-sdk` from 1.5.0 → 1.6.1
- `golang.org/x/sync` from 0.20.0 → 0.21.0

---

## Community Hot Topics

### Most Active Issues

1. **[#2472](https://github.com/sipeed/picoclaw/issues/2472) — [BUG] list_dir returns "invalid argument" on Windows**  
   - **Comments**: 5 | **Reactions**: 👍 1  
   - **Status**: OPEN | **Created**: Apr 10 (2+ months old)  
   - **Analysis**: Long-standing Windows compatibility issue where `list_dir` fails because backslashes are passed to Go's `fs.FS` which requires forward slashes. Community need: **cross-platform file tool parity**. This issue has been open for 2 months without a fix PR, indicating Windows support gaps.

2. **[#3094](https://github.com/sipeed/picoclaw/issues/3094) — [Bug] Async sub-agent (spawn) duplicate messages**  
   - **Comments**: 1 | **Status**: OPEN  
   - **Analysis**: Fresh, high-impact bug: when using `spawn` tool, sub-agent results are delivered twice — once raw and once summarized by the main agent. Affects Telegram/Feishu channels. Signals need for **sub-agent output deduplication**.

3. **[#3108](https://github.com/sipeed/picoclaw/issues/3108) — [BUG] Image description hallucinates with non-vision models**  
   - **Comments**: 0 | **Status**: OPEN | **Created**: Yesterday  
   - **Analysis**: Critical UX issue: `deepseek-v4-flash` requested to describe images produces hallucinated responses. Root cause: model is text-only but system still attempts image description. User need: **model capability detection** before invoking vision tools.

### Most Active Pull Requests

1. **[#2937](https://github.com/sipeed/picoclaw/pull/2937) — Feat/agent collaboration (OPEN)**  
   - **Analysis**: Major architectural PR introducing "Agent Collaboration Bus" with per-agent mailboxes, isolated session threads, and permission-aware delivery. This is the **most significant feature in progress**, likely planned for v0.3.0.

2. **[#3048](https://github.com/sipeed/picoclaw/pull/3048) — fix(mcp): reject unknown pre-positional flags in add (OPEN)**  
   - **Analysis**: Fixes MCP command argument parsing bug where root flags (e.g., `--no-color`) leak into subcommand parser.

---

## Bugs & Stability

### High Severity Bugs (Open)

1. **[#3108](https://github.com/sipeed/picoclaw/issues/3108) — Image hallucination with non-vision models**  
   - **Severity**: HIGH — Produces false information. No fix PR yet.  
   - **Impact**: Users get fabricated image descriptions when using text-only models.

2. **[#3094](https://github.com/sipeed/picoclaw/issues/3094) — Sub-agent duplicate messages**  
   - **Severity**: MEDIUM-HIGH — Spams channels with duplicate content.  
   - **Impact**: Poor UX in channel integrations (Telegram, Feishu). No fix PR yet.

3. **[#2472](https://github.com/sipeed/picoclaw/issues/2472) — Windows `list_dir` invalid argument**  
   - **Severity**: MEDIUM — Blocks file tool usage on Windows.  
   - **Impact**: Windows users cannot use `list_dir` tool. **No fix PR after 2 months**.

### Medium Severity Bugs (Recently Fixed)

4. **[#2958](https://github.com/sipeed/picoclaw/issues/2958) — Tool_calls dropped during streaming**  
   - **Status**: CLOSED | **Fix**: [#2957](https://github.com/sipeed/picoclaw/pull/2957) merged  
   - **Impact**: Previously caused silent data loss in pico channel.

### Security Issue (Closed)

5. **[#3080](https://github.com/sipeed/picoclaw/issues/3080) — `allowed_cidrs` bypass via loopback proxying**  
   - **Status**: CLOSED | **Severity**: MEDIUM  
   - **Impact**: First-run setup could bypass IP restrictions via same-host proxying.

---

## Feature Requests & Roadmap Signals

### In Flight (Open PRs signaling roadmap direction)

| PR | Feature | Likely Version |
|---|---|---|
| [#2937](https://github.com/sipeed/picoclaw/pull/2937) | **Agent Collaboration Bus** — inter-agent mailboxes, collaboration threads | v0.3.0 (major) |
| [#2696](https://github.com/sipeed/picoclaw/pull/2696) | **MCP per-request dynamic headers** from channel context | v0.2.9+ |
| [#3107](https://github.com/sipeed/picoclaw/pull/3107) | **GitHub Copilot SDK integration** (dependency bump to v1.0.1) | Future |

### Predicted Near-Term Additions

- **Windows cross-platform support** (pressure from #2472, 2 months unresolved)
- **Model capability introspection** — preventing vision tool calls on text-only models (pressure from #3108)
- **Sub-agent output deduplication** — fix for #3094 likely to land soon given its impact

---

## User Feedback Summary

### Real Pain Points

1. **Windows incompatibility** (#2472) — `list_dir` completely broken on Windows, core file tool unusable. Affects Windows developers and enterprise users.

2. **Channel message duplication** (#3094) — Sub-agent workflows produce duplicate messages in Telegram/Feishu, disrupting conversation flow.

3. **Model hallucination** (#3108) — Text-only models produce entirely fabricated image descriptions, undermining trust in tool outputs.

4. **Configuration persistence issues** (#3067, #2956) — Settings changes lost on page reload, channel states incorrectly reset after security config merge.

5. **Connection reliability** (#2958, fixed) — Tool call messages silently lost during streaming, difficult to debug.

### Satisfaction Signals

- High PR throughput (31 updated) indicates **responsive maintainer team**
- Multiple bug fixes merged within hours/days of reporting (e.g., #3067, #3080)
- Active community contributions: 3 external contributors (loafoe, yuxuan-7814, dtapps) had fixes merged today

---

## Backlog Watch

### Long-Unanswered Issues Needing Attention

| Issue | Age | Why It Matters |
|---|---|---|
| [#2472](https://github.com/sipeed/picoclaw/issues/2472) — Windows `list_dir` | **63 days** | Core tool broken on major platform. Multiple workaround requests, no maintainer response or fix PR. |
| [#2954](https://github.com/sipeed/picoclaw/issues/2954) — 32-bit Android unsupported | **16 days** | Closed as stale without resolution. Blocks Android Termux users on older/32-bit devices. |

### Open PRs Lacking Review

| PR | Days Open | Staleness Risk |
|---|---|---|
| [#2937](https://github.com/sipeed/picoclaw/pull/2937) — Agent collaboration | **19 days** | HIGH — Major architectural PR; risk of merge conflicts growing. |
| [#2956](https://github.com/sipeed/picoclaw/pull/2956) — Security.yml channel state fix | **16 days** | MEDIUM — Stale label applied, despite being a functional fix. |
| [#3048](https://github.com/sipeed/picoclaw/pull/3048) — MCP flag parsing fix | **5 days** | LOW — Recently opened. |

### Recommendation
The **Windows compatibility issue (#2472)** is the most pressing backlog item — it has been open 2+ months with no response from maintainers, affecting a significant user segment. The **agent collaboration PR (#2937)** requires prompt review before it diverges further from `main`.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-12

## Today's Overview
NanoClaw experienced a highly active development day with 15 pull requests updated in the last 24 hours, 9 of which were merged or closed—indicating strong forward momentum. One issue was opened and one closed, maintaining a lean open issue count at 1. The project saw no new releases, but the flurry of merged PRs suggests a significant batch of fixes and features is queued for the next version. Activity is assessed as **very high**, with multiple contributors driving bug fixes, infrastructure hardening, and new skill-based features.

## Releases
**No new releases** today. The last release date is not provided; the project appears to be in an active development cycle between releases.

## Project Progress
Nine pull requests were merged or closed today, representing substantial progress across several areas:

### Feature Additions (Merged/Closed)
- **#2740** — **Per-group idle timeout**: Adds clean exit for ephemeral session containers, improving resource management. (gavrielc)
- **#2739** — **Raw-route registry for webhooks**: Allows non-Chat-SDK webhooks to be appended as routes, broadening integration flexibility. (gavrielc)
- **#2737** — **Approval-resolved callback registry**: Modules can now observe approval resolution additively, enabling more modular approval flows. (gavrielc)
- **#2734** — **Delivery action read side**: Adds `getDeliveryAction` to the action registry, completing the read path. (gavrielc)
- **#2733** — **Native channel-instance dimension**: Introduces multi-bot substrate support, a foundational architectural addition for running multiple bot instances per channel. (gavrielc)

### Bug Fixes (Merged/Closed)
- **#2738** — **Fix `writeOutboundDirect` read-only mode**: Resolves the critical bug where outbound DB was opened read-only, silently dropping command-gate denial responses. (gavrielc)
- **#2736** — **Fix host-sweep grace period**: Prevents premature sweep of freshly-woken containers with stale processing claims. (gavrielc)
- **#2735** — **Fix Chat SDK bridge approval cards**: Now records the acting user on resolved approval cards for audit clarity. (gavrielc)
- **#2741** — **Fix setup handoff context**: Auto-submits handoff context as Claude's first prompt, fixing interactive setup flow. (gavrielc)

### Documentation
- **#2685** (open, updated) — **Signal adapter docs**: Updated for group typing, outbound reactions, and quote-reply fixes. (ira-at-work)

A notable pattern: contributor **gavrielc** authored 7 of the 9 merged PRs, showing concentrated feature development alongside critical bug fixes.

## Community Hot Topics

### Most Active Issue
- **[#1356 — Agent memory system redesign](https://nanocoai/nanoclaw/issues/1356)** (OPEN, 2 comments, 6 👍)
  - Created 2026-03-23, still active after ~3 months. This long-standing architectural issue tracks research findings on scaling the current markdown-based memory system (~54 files, 83 KB). The 6 upvotes indicate strong community interest in a more scalable solution. The issue's longevity and lack of a linked PR suggest this is a complex, high-effort redesign that the team is still researching.

### Most Active PRs
- **[#2742 — PR Factory recipe](https://nanocoai/nanoclaw/pull/2742)** (OPEN, no comments yet) — A published "recipe" for turning PRs into automated review, triage, and testing workflows run by agents. This is a meta-feature (an agent-managed PR workflow) that could significantly impact how the project itself operates.
- **[#2611 — Preserve caller context after approval](https://nanocoai/nanoclaw/pull/2611)** (OPEN, updated today) — A security-related PR from Hinotoi-agent that ensures administrative approvals preserve the original caller context. This has been open since May 25 and received no comments, suggesting it may need maintainer review.

**Underlying need analysis**: The activity pattern suggests the community is pushing for two major things: 1) **scalability of agent coordination** (memory system redesign, multi-bot substrate, PR factories), and 2) **reliability of core infrastructure** (database read-only bugs, container lifecycle, approval context preservation).

## Bugs & Stability

| Severity | Bug | Status | Fix PR |
|----------|-----|--------|--------|
| **Critical** | `writeOutboundDirect()` opens outbound DB read-only, causing `SQLITE_READONLY` INSERT failures; command-gate deny responses silently dropped | Closed issue (#2495) | ✅ **#2738** (merged) |
| **High** | `wirings create` CLI command skips required `agent_destinations` side effect, causing agents to not receive messages from new chats | Open PR (#2743) | 🔄 #2743 (open, fix in review) |
| **High** | Host sweep prematurely kills freshly-woken containers with stale processing claims | Merged | ✅ **#2736** (merged) |
| **Medium** | Signal adapter drops agent `add_reaction` tool output and ignores inbound reaction envelopes | Open PR (#2744) | 🔄 #2744 (open) |
| **Medium** | Chat SDK bridge approval cards not recording acting user | Merged | ✅ **#2735** (merged) |
| **Medium** | Setup handoff to Claude doesn't auto-submit context | Merged | ✅ **#2741** (merged) |

**Assessment**: The critical database bug (#2495) represents a significant reliability issue that may have silently dropped denial responses for weeks (issue opened May 15). Its fix (#2738) was among today's merges. The open wirings bug (#2743) could cause silent message delivery failures in new chat setups.

## Feature Requests & Roadmap Signals

### Strong Signals (likely in next version)
1. **Agent memory system redesign** (#1356, 6 👍) — The most-upvoted issue, suggesting a more scalable memory architecture is a top community priority. The lack of a PR may mean the team is still designing this.
2. **PR Factory** (#2742) — If adopted, this "recipe" for agent-managed PR review could change how the project processes contributions. It's a meta-feature that signals growing sophistication in agent orchestration.
3. **Multi-bot channel support** (#2733, merged) — The "native channel-instance dimension" is now merged, enabling multi-bot substrate. This architectural change will likely enable future features around bot teams and channel partitioning.

### Emerging Patterns
- **Security hardening**: PR #2611 (caller context preservation) and #2732 (health audit fixes) show a focus on security and operational robustness.
- **Webhook/API extensibility**: #2739 (raw-route registry) expands the project's ability to integrate with non-Chat-SDK services.

**Prediction**: The next release will likely include the merged infrastructure improvements (multi-bot, idle timeout, approval callbacks) alongside the critical database fix. The memory redesign (#1356) may remain in design phase.

## User Feedback Summary

### Pain Points (explicit in issues/PRs)
1. **Silent failures**: The read-only database bug (#2495) meant error handling silently failed—denial responses were dropped without user awareness. This undermines trust in the system's reliability.
2. **Missing side effects**: The `wirings create` bug (#2743) means users creating new chat wirings may believe agents are connected when they aren't. This is a poor onboarding experience.
3. **Container lifecycle fragility**: Multiple fixes to container lifecycle (#2736, #2732) suggest users on Docker Desktop and similar platforms experience hard-to-debug crashes.
4. **Signal adapter incompleteness**: Reactions not working (#2744) and group typing indicators being added (#2685) suggest Signal users find the adapter functional but missing expected messaging features.

### Satisfaction Indicators
- The high volume of merged PRs (9 in one day) indicates an **active and responsive maintainer team**.
- The #2742 "PR Factory" recipe suggests contributors are finding the platform powerful enough to automate parts of its own development workflow—a strong vote of confidence.
- Multiple contributors (WormyOne, gavrielc, ira-at-work, sturdy4days) are building on top of the framework, indicating **good developer extensibility**.

## Backlog Watch

### Long-unanswered Items Needing Maintainer Attention

| Item | Age | Priority |
|------|-----|----------|
| **[#2611 — Preserve caller context after approval](https://nanocoai/nanoclaw/pull/2611)** | 18 days open (since May 25) | **High** — Security-related PR from contributor Hinotoi-agent. Zero comments. If accepted, it fixes a legitimate security concern where approval replay may lose context. Needs maintainer review. |
| **[#1356 — Agent memory system redesign](https://nanocoai/nanoclaw/issues/1356)** | ~3 months open | **Medium-High** — Community-voted (6👍) architectural issue. While the team may be actively researching, the lack of linked PRs or status updates since March could frustrate contributors eager to see progress. A status comment from maintainers would be valuable. |
| **[#2742 — PR Factory recipe](https://nanocoai/nanoclaw/pull/2742)** | 1 day old | **Low urgency** but high potential impact. No comments yet. Maintainers should evaluate quickly if this meta-workflow aligns with the project's direction. |

### Recommendations
- **#2611** should be reviewed promptly given its security implications.
- **#1356** would benefit from a maintainer update summarizing design decisions or blockers to keep the community engaged.
- **#2744** (Signal reactions fix) and **#2743** (wirings fix) are new and should receive timely review to maintain contributor momentum.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-06-12

## Today's Overview
NullClaw is in a low-activity period, with only 1 issue updated in the last 24 hours and no pull request or release activity. The single open issue reports a user-facing bug with local model integration via Ollama, suggesting that core functionality for local LLM support may still have rough edges. The project currently has no new releases or merged work today, indicating a quiet day in development.

## Releases
No new releases were published on 2026-06-12. The latest available release remains unchanged.

## Project Progress
No pull requests were merged or closed today. No feature advancements or bug fixes were delivered in the last 24 hours.

## Community Hot Topics
The only active discussion today revolves around one issue:

- **[#952 [OPEN] [bug] Local model using ollama returns incomplete answers](https://github.com/nullclaw/nullclaw/issues/952)**  
  *Author: bloodgroup-cplusplus | Created: 2026-06-11 | Updated: 2026-06-11 | Comments: 0 | 👍: 0*  
  This issue describes a problem where the agent, using a Gemma model pulled via Ollama, does not respond in complete sentences. The user included a screenshot illustrating truncated or incomplete output. Despite being freshly filed, it has received no comments or upvotes yet, suggesting low immediate community engagement.

**Underlying need**: Users want reliable, complete responses when using locally hosted models through Ollama integration. The truncated output signals potential issues with token generation limits, response streaming, or prompt handling in the Ollama adapter.

## Bugs & Stability
One bug was reported today, classified as **medium severity** — it affects output quality but does not crash the system:

- **[Bug] Incomplete answers with Ollama + Gemma (Issue #952)**  
  The agent returns partial, cut-off sentences when using a local Gemma model via Ollama. The root cause is unclear but may involve stream termination, context window truncation, or a missing response completion check. No fix PRs are currently associated with this issue.

*No crashes, regressions, or security-related bugs reported today.*

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the reported Ollama issue (#952) indirectly signals user demand for:
- **Robust local model support** — users expect parity in response quality between local and remote models.
- **Graceful handling of truncated responses** — the system should detect and retry or warn when a model's response is cut off.

If this pattern persists, the next minor version may include improvements to Ollama response assembly and completion validation.

## User Feedback Summary
User pain points today center on the **reliability of local LLM integration**. The single active report indicates that while Ollama model pulling and basic execution work, the agent's output quality suffers when serving responses through local models. The user did not express explicit dissatisfaction beyond the bug report, but the lack of complete sentences degrades the assistant's perceived usefulness. No positive feedback or use-case reports were logged today.

## Backlog Watch
No long-unanswered issues or pending PRs currently require maintainer attention. The project's backlog appears clean, with the only open item being the newly filed #952. There are no stale issues or PRs awaiting response for extended periods.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-12

## 1. Today's Overview

IronClaw is in an intense development sprint, with 47 PRs and 30 issues updated in the last 24 hours — reflecting high-velocity work on the "Reborn" architecture. The team closed 25 PRs and 13 issues, indicating strong delivery momentum toward Reborn production readiness. Development is concentrated on Reborn binary QA automation, Slack integration hardening, credential and configuration management, and UI/UX bugfixing. No new releases were published today, but significant code is flowing into `main` and QA branches.

---

## 2. Releases

**No new releases today.** The last release draft (PR #3708) remains open, proposing version bumps (`ironclaw` 0.24.0 → 0.29.1) with API-breaking changes in `ironclaw_common` and `ironclaw_skills`. That release has not yet merged.

---

## 3. Project Progress

**25 PRs merged/closed today**, advancing several major workstreams:

**Reborn Binary & Infrastructure**
- [#4786](https://github.com/nearai/ironclaw/pull/4786) — Promote `main` to QA branch (merge train)
- [#4615](https://github.com/nearai/ironclaw/pull/4615) — Make `build_reborn_runtime` launchable in production profile against PostgreSQL
- [#4619](https://github.com/nearai/ironclaw/pull/4619) — Enforce production cutover gate before serving Reborn traffic
- [#4620](https://github.com/nearai/ironclaw/pull/4620) — Add backend-parity readiness coverage for production graph
- [#4551](https://github.com/nearai/ironclaw/pull/4551) — Wire Reborn production Postgres storage config

**Slack & Outbound Delivery**
- [#4753](https://github.com/nearai/ironclaw/pull/4753) — Slack gate routing: conversation-keyed delivered-gate routes for bare "approve" resolution (Phase B)
- [#4757](https://github.com/nearai/ironclaw/pull/4757) — Fix triggered automation runs navigating to blank screen
- [#4782](https://github.com/nearai/ironclaw/pull/4782) — Unify outbound state store so WebUI delivery defaults reach Slack delivery

**Extensions & Credentials**
- [#4744](https://github.com/nearai/ironclaw/pull/4744) — Gate extension activation and harden GSuite OAuth runtime
- [#4700](https://github.com/nearai/ironclaw/pull/4700) — Auto-enable NEAR AI MCP when NEAR AI credentials configured
- [#4699](https://github.com/nearai/ironclaw/pull/4699) — Fix NEAR AI MCP fallback web search tool name

**Observability & APIs**
- [#4595](https://github.com/nearai/ironclaw/pull/4595) — Runtime readiness and status APIs for operator inspection
- [#4593](https://github.com/nearai/ironclaw/pull/4593) — Effective config API for list/get/set/validate/precedence/redaction
- [#4714](https://github.com/nearai/ironclaw/pull/4714) — Return failed/cancelled states from OpenAI Responses retrieve

**Bugfixes**
- [#4784](https://github.com/nearai/ironclaw/pull/4784) — Handle capability runtime unavailability as tool failure instead of aborting agent loop
- [#4683](https://github.com/nearai/ironclaw/pull/4683) — Fix generic "driver unavailable" error for invalid model configuration
- [#4766](https://github.com/nearai/ironclaw/pull/4766) — Fix chat runtime not using UI-saved NEAR AI credentials after restart
- [#4705](https://github.com/nearai/ironclaw/pull/4705) — Fix NEAR AI SSO setup failure in local environment

---

## 4. Community Hot Topics

### Most Active Discussions

| Issue/PR | Comments | Topic |
|---|---|---|
| [#3036](https://github.com/nearai/ironclaw/issues/3036) | 7 | Epic: Configuration-as-Code for IronClaw Reborn — tenant blueprints and use-case harnesses |
| [#4766](https://github.com/nearai/ironclaw/issues/4766) | 2 | Chat runtime doesn't use UI-saved NEAR AI credentials after restart *(CLOSED)* |
| [#4703](https://github.com/nearai/ironclaw/issues/4703) | 2 | NEAR AI model picker saves display name instead of model ID |

### Analysis

The **Configuration-as-Code epic** (#3036) remains the longest-running active discussion, reflecting a core architectural need: operators want to manage IronClaw declaratively with schema, versioning, and audit trails instead of hand-editing `.env` and JSON files. This has been open since April 28 with sustained interest.

The **credential and model configuration issues** (#4766, #4703, #4765) cluster around the same user pain — configuration that doesn't "stick" or displays incorrectly after save. These are small bugs but high-friction ones that significantly impact first-run experience.

---

## 5. Bugs & Stability

### High Severity

| Issue | Description | Fix Status |
|---|---|---|
| [#4761](https://github.com/nearai/ironclaw/issues/4761) | Agent stops after repeated tool failures instead of recovering — workspace writes fail silently | Open (no fix PR) |
| [#4783](https://github.com/nearai/ironclaw/issues/4783) | Credential-less WASM extension capabilities fail dispatch with network obligation error before execution — blocks pure-compute extensions | Open (analyzed; PR likely pending) |
| [#4762](https://github.com/nearai/ironclaw/issues/4762) | Failed tool workflow causes follow-up messages and activity ordering to become inconsistent | Open |
| [#4751](https://github.com/nearai/ironclaw/issues/4751) | Large response request fails — provider tool arguments exceed 16KB limit | Open |

### Medium Severity

| Issue | Description | Fix Status |
|---|---|---|
| [#4764](https://github.com/nearai/ironclaw/issues/4764) | Denying shell approval leaves tool invocation pending with no user feedback | Open |
| [#4770](https://github.com/nearai/ironclaw/issues/4770) | Tool activity stops updating after page refresh (possible SSE reconnect issue) | Open |
| [#4759](https://github.com/nearai/ironclaw/issues/4759) | Workspace path is duplicated when using workspace-relative paths | Open |
| [#4750](https://github.com/nearai/ironclaw/issues/4750) | Workspace files not discoverable from WebUI after creation | Open |
| [#4748](https://github.com/nearai/ironclaw/issues/4748) | Code block Wrap/No Wrap toggle has no visible effect | Open |

### Important Pattern

The agent-tool-failure recovery issues (#4761, #4762) are particularly concerning — the agent enters an inconsistent state after tool errors, with follow-up messages appearing out of order or disappearing entirely. This suggests a deeper issue in the tool workflow state machine.

---

## 6. Feature Requests & Roadmap Signals

### Likely in Next Release

1. **Configuration-as-Code** (#3036) — The epic continues to gather interest; expect tenant blueprints and declarative configuration to be a major milestone
2. **Automated QA for Reborn binary** (#4775) — A new epic today outlines 22 deterministic test suites; this is clearly a priority
3. **Observability seams** (PR #4588) — Trajectory observer hooks and LLM provider injection for benchmarking; likely to merge soon
4. **Outbound delivery targets** (PR #4779, #4780) — Model-visible delivery target selection before creating routines/triggers

### User-Requested Features

| Issue | Request | Status |
|---|---|---|
| [#4776](https://github.com/nearai/ironclaw/issues/4776) | Global "Always Allow" setting for eligible tools | Open |
| [#4750](https://github.com/nearai/ironclaw/issues/4750) | Workspace file browser/discovery in WebUI | Open |
| [#4771](https://github.com/nearai/ironclaw/issues/4771) | Run/thread-scoped operator log filtering | Open |

---

## 7. User Feedback Summary

### Pain Points (from issue reports)

- **Credential persistence**: Users save NEAR AI credentials in the UI, but they're lost on restart (#4766) — high frustration for a basic configuration flow
- **Model confusion**: The model picker saves display names instead of model IDs (#4703), causing silent failures when the display name is not a valid model identifier
- **SSO setup friction**: GitHub/Google SSO fails with "Invalid frontend_callback" in local environments (#4705)
- **Tool approval opacity**: Denying shell approval leaves no feedback (#4764); approval dialogs lack context about what's being approved (#4701)
- **Workspace invisibility**: Files created by agents aren't discoverable from the WebUI (#4750)

### Satisfaction Signals

- The **NEAR AI MCP auto-enable** (#4700) was likely well-received — it removes a manual setup step
- **Observability improvements** (#4595, #4593) give operators inspection APIs they've been needing
- The **Slack delivery fixes** (#4753, #4782) address a critical use-case (triggered-run delivery to Slack DM)

### Underlying Need

Users consistently ask for: (1) configuration that persists and validates, (2) visible workspace state, (3) clear tool approval UX, (4) graceful error recovery. The Reborn WebUI v2 is still maturing through these "surface polish" issues.

---

## 8. Backlog Watch

### Issues Needing Attention

| Issue | Age | Status | Concern |
|---|---|---|---|
| [#3036](https://github.com/nearai/ironclaw/issues/3036) | 45 days (Apr 28) | Open, active | Configuration-as-Code epic; requires architectural design |
| [#3708](https://github.com/nearai/ironclaw/pull/3708) | 27 days (May 16) | Open | Release PR with breaking changes; not yet merged |
| [#4108](https://github.com/nearai/ironclaw/issues/4108) | 16 days (May 27) | Open | Nightly E2E CI failures; still unresolved |
| [#4588](https://github.com/nearai/ironclaw/pull/4588) | 3 days (Jun 9) | Open | Observability seams PR; 0 comments — may need review attention |

### Risk Items

1. **Nightly E2E failures** (#4108) have been open for 16 days with no resolution — this degrades CI confidence
2. The **release PR** (#3708) contains breaking changes in two crates and has been open since May 16; version bumps may be blocking downstream consumers
3. The **credential-less WASM extensions bug** (#4783) blocks pure-compute extension capabilities, which is architecturally important for the extension ecosystem

### Looking Ahead

The project is clearly prioritizing **Reborn production readiness** (Postgres wiring, cutover gates, QA automation) and **Slack/outbound delivery** for the near-term milestone. Configuration-as-Code (#3036) and extension ecosystem (#4783, #4776) are the next architectural layers once the core Reborn runtime stabilizes.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-06-12

## 1. Today's Overview
The LobsterAI project shows **very high activity** with 19 PRs updated in the last 24 hours, nearly all merged or closed (18), leaving just 1 open. The 2 open issues indicate low community concern volume, but the feature-request pipeline is active. The development cadence suggests a **major feature push** underway, particularly around Cowork (shared workspaces) and Computer Use automation. No new releases were published today, but the volume of merged code points toward an imminent version bump.

## 2. Releases
**None.** No new releases were created in the last 24 hours. The project appears to be consolidating features before the next tagged release.

## 3. Project Progress
**18 PRs merged/closed today**, covering several major feature areas:

- **Cowork & Collaboration:**  
  - [#2152](https://github.com/netease-youdao/LobsterAI/pull/2152) — Extended pre-send model sync timeout from 30s to 90s for slow gateways.  
  - [#2148](https://github.com/netease-youdao/LobsterAI/pull/2148) — Added **real-time ASR voice input** for Cowork, with WebSocket streaming and PCM audio chunking.  
  - [#2147](https://github.com/netease-youdao/LobsterAI/pull/2147) — Fixed race where stopped startup turns could still send chat messages.  
  - [#2145](https://github.com/netease-youdao/LobsterAI/pull/2145) — Improved context continuity after OpenClaw compaction (post-compaction quality).  
  - [#1481](https://github.com/netease-youdao/LobsterAI/pull/1481) — Scroll-friendly skill badge layout in prompt bar.

- **Computer Use MVP:**  
  - [#2143](https://github.com/netease-youdao/LobsterAI/pull/2143) — Added **Computer Use MVP** for Windows x64, including a built-in kit, MCP server bridge for app/window/input control, and runtime lifecycle wiring.

- **Sharing & Access Control:**  
  - [#2151](https://github.com/netease-youdao/LobsterAI/pull/2151) — File sharing support.  
  - [#2146](https://github.com/netease-youdao/LobsterAI/pull/2146) — HTML share now supports switching between **share code** and **public access** modes.

- **Stability & Infrastructure:**  
  - [#2149](https://github.com/netease-youdao/LobsterAI/pull/2149) — Raised V8 heap limit for OpenClaw gateway to reduce OOM crashes.  
  - [#2142](https://github.com/netease-youdao/LobsterAI/pull/2142) — Fixed NSIS destructive init on Windows and redesigned engine loading page.  
  - [#2144](https://github.com/netease-youdao/LobsterAI/pull/2144) — Updated portal fallback URLs to new domain.

- **UI/UX Polish (older stale PRs merged):**  
  - [#1459](https://github.com/netease-youdao/LobsterAI/pull/1459) — Skill hover tooltips with full description.  
  - [#1478](https://github.com/netease-youdao/LobsterAI/pull/1478) — Fixed CopyButton memory leak on unmount.  
  - [#1479](https://github.com/netease-youdao/LobsterAI/pull/1479) — Reject duplicate skill folder on install.  
  - [#1480](https://github.com/netease-youdao/LobsterAI/pull/1480) — Toast + refresh after skill install.  
  - [#1482](https://github.com/netease-youdao/LobsterAI/pull/1482) — Fixed scheduled task editor clearing description & enabling state.  
  - [#1483](https://github.com/netease-youdao/LobsterAI/pull/1483) — **Automatic model failover** when primary model errors (rate limit, timeout).  
  - [#1484](https://github.com/netease-youdao/LobsterAI/pull/1484) — **Gmail email trigger** for auto agent activation.

## 4. Community Hot Topics
The two open issues are relatively quiet, but reveal key user concerns:

- **[#1462](https://github.com/netease-youdao/LobsterAI/issues/1462) — Feature request: per-agent model binding & multi-agent rooms**  
  *Created Apr 4, 2 comments, stale label.*  
  The user explicitly requests two features: (1) each agent can be assigned its own model, and (2) a "room" concept where a manager agent dispatches tasks to sub-agents. The user mentions preferring LobsterAI over Ali's Hiclaws product. **Underlying need:** Users want flexible, production-grade multi-agent orchestration, not just single-agent chat.

- **[#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) — Suspicious repeated output / token waste**  
  *Created Jun 7, 1 comment.*  
  The user reports repeated output text consuming excessive tokens and suspects a bug. Likely a model or context management issue. No PRs directly address this yet.

**No maintainer responses visible** on either issue, which may cause frustration.

## 5. Bugs & Stability
| Severity | Issue/PR | Description | Resolution |
|----------|----------|-------------|------------|
| **High** | [#2149](https://github.com/netease-youdao/LobsterAI/pull/2149) (PR) | OOM crashes in OpenClaw gateway under long-running multi-channel workloads | Merged: raised V8 heap limit |
| **Medium** | [#2147](https://github.com/netease-youdao/LobsterAI/pull/2147) (PR) | Stopped startup turns could still send chat messages | Merged: cancel on stop |
| **Medium** | [#2152](https://github.com/netease-youdao/LobsterAI/pull/2152) (PR) | Pre-send model sync timeout (30s default) dropped messages under long cold-starts | Merged: increased to 90s |
| **Low** | [#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) (Issue) | Repeated output / token waste, suspected claw bug | Open, no fix yet |
| **Low** | [#1478](https://github.com/netease-youdao/LobsterAI/pull/1478) (PR) | CopyButton memory leak on component unmount | Merged |
| **Low** | [#1482](https://github.com/netease-youdao/LobsterAI/pull/1482) (PR) | Scheduled task editor corrupts description & enabled state | Merged |

## 6. Feature Requests & Roadmap Signals
Based on merged PRs and open issues, the following features are likely to appear in the next version:

- **Multi-agent orchestration** (from [#1462](https://github.com/netease-youdao/LobsterAI/issues/1462)) — per-agent model binding and manager/dispatch rooms. This is the #1 user request, but not yet addressed by any PR.
- **Computer Use** (Windows) — now landed as MVP in [#2143](https://github.com/netease-youdao/LobsterAI/pull/2143).
- **Real-time ASR voice input** — landed in [#2148](https://github.com/netease-youdao/LobsterAI/pull/2148).
- **Automatic model failover** — landed in [#1483](https://github.com/netease-youdao/LobsterAI/pull/1483).
- **Gmail agent triggers** — landed in [#1484](https://github.com/netease-youdao/LobsterAI/pull/1484).

**Prediction:** Next release (likely 4.4 or 4.5) will highlight Computer Use, real-time voice, model failover, and enhanced sharing. Multi-agent rooms may wait for a later milestone.

## 7. User Feedback Summary
- **Positive:** Users express high satisfaction with multi-instance support (issue #1462). The project is preferred over a competing product (Ali's Hiclaws).
- **Pain points:**
  - **Model binding per agent** — top missing feature request.
  - **Token waste from repeated output** — reported as a bug, not yet fixed.
  - **Tooltip truncation** — skill descriptions truncated in UI (fixed in #1459, merged today).
- **Sentiment:** Generally positive but users want more sophisticated agent collaboration.

## 8. Backlog Watch
- **[#1462](https://github.com/netease-youdao/LobsterAI/issues/1462) — Per-agent model binding & multi-agent rooms**  
  *Status: Open since Apr 4, stale label, 2 comments, no maintainer reply.*  
  **Risk:** This is the most upvoted feature request with explicit comparison to a competitor. Lack of response may push users to alternatives.

- **[#2121](https://github.com/netease-youdao/LobsterAI/issues/2121) — Repeated output / token waste**  
  *Status: Open since Jun 7, 1 comment.*  
  **Risk:** Could indicate a regression in token management or model output handling. No maintainer acknowledgement yet.

- **[#1459](https://github.com/netease-youdao/LobsterAI/pull/1459) — Skill hover tooltip**  
  *Status: Open since Apr 3 (merged today).*  
  **Note:** This was a long-stale PR that finally merged — positive sign for backlog cleanup.

**Maintainer attention needed:** Response to #1462 and #2121 to reassure users and clarify roadmap.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-06-12

## Today's Overview
Activity remains calm, with only one open issue and one open pull request updated in the last 24 hours. No new releases were published, and no items were merged or closed. The single bug report concerns Fastmail MCP authorization, while the open PR addresses a WhatsApp reply delivery issue. Overall project health appears stable, though the low throughput may indicate maintainer bandwidth constraints or a lull in development velocity.

## Releases
None this period.

## Project Progress
**No PRs were merged or closed today.**  
The only open PR remains under review:
- **#1116** [OPEN] `fix(whatsapp): deliver replies to @lid chats via PN JID rewrite` — Author: juanlotito, created 2026-06-12  
  This fix addresses a case where replies to privacy-enabled senders in @lid chats were silently dropped. The agent produced replies visible in the web UI, but the outbound sender never delivered the message and no "Delivered" receipt was received. The PR rewrites the PN JID to ensure proper routing.  
  [View PR #1116](https://github.com/moltis-org/moltis/pull/1116)

## Community Hot Topics
**Most active discussion:**
- **Issue #1115** [OPEN] [bug] `[Bug]: Fastmail MCP Authorisation` by kmath313 (updated 2026-06-11, 1 comment)  
  The reporter has confirmed they searched existing issues and are using the latest Moltis version. The issue appears to involve authentication or authorization failures when connecting Fastmail via MCP. Community reaction is neutral (0 👍), but the single comment suggests some maintainer or user engagement.  
  [View Issue #1115](https://github.com/moltis-org/moltis/issues/1115)

## Bugs & Stability
**Open bugs (ranked by severity):**

1. **Medium Severity — Fastmail MCP Authorization** (Issue #1115)  
   Fastmail integration fails during MCP authorization. The reporter indicates they are on the latest version. No fix PR exists yet. This could block users relying on Fastmail for email-based AI agent capabilities.  
   [View Issue #1115](https://github.com/moltis-org/moltis/issues/1115)

2. **Medium Severity — WhatsApp @lid Chat Delivery** (Addressed by PR #1116, not yet merged)  
   Replies to privacy-enabled senders in @lid chats were silently dropped. The problem was reproducible and is now fixed in an open PR awaiting review. No live fix is available yet.  
   [View PR #1116](https://github.com/moltis-org/moltis/pull/1116)

## Feature Requests & Roadmap Signals
No explicit feature requests were filed today. However, the Fastmail MCP authorization issue may hint at user demand for broader MCP provider support or better error handling during OAuth flows. The WhatsApp delivery fix suggests ongoing investment in WhatsApp channel reliability, which could be a precursor to more advanced WhatsApp features (e.g., media replies, group chat support). No clear signals for the next version.

## User Feedback Summary
- **Pain points:** Fastmail MCP authorization is failing, blocking a specific email integration use case. WhatsApp replies to privacy-enabled contacts are not delivering, affecting private communication reliability.
- **Use cases:** Users are deploying Moltis as an AI agent gateway connected to Fastmail (email-based agent) and WhatsApp (chat-based agent), relying on full-duplex message delivery.
- **Satisfaction/dissatisfaction:** No overt expressions of frustration, but the open bug with no fix PR yet may cause concern among Fastmail users. The WhatsApp fix in PR is a proactive user-contributed solution, indicating a collaborative community.

## Backlog Watch
No long-unanswered issues or PRs were identified today. Both open items are recent (created within the last 24–48 hours) and have received some maintainer attention. No items appear to be neglected. However, if the Fastmail issue (Issue #1115) remains unaddressed for an extended period, it may warrant escalation.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-06-12

## 1. Today's Overview

CoPaw is in an intense release stabilization phase, with **33 issues updated** and **42 PRs touched** in the last 24 hours — the highest single-day activity in recent weeks. Two patch releases (`v1.1.11.post1`, `v1.1.11.post2`) were rushed out to address critical desktop client crashes, SSL certificate failures, and UI regressions introduced in `v1.1.11`. Despite the high velocity, the project shows clear stress: multiple users report **memory blow-ups** on Windows Tauri desktop, **process fork bombs**, and **broken file downloads** persisting across patches. The community is actively contributing — 7 first-time-contributor PRs arrived today — but the core team is clearly firefighting. The looming **AgentScope 2.0 backend migration (Issue #4727)** remains open and unresolved, suggesting a major architectural refactor is waiting in the wings once stability is restored.

## 2. Releases

**Two patch releases shipped today:**

### v1.1.11.post2 (latest)
- **Style fix:** truncate tool card titles to single line with ellipsis (PR #5119 by @zhaozhuang521)
- **Chore:** version bump to 1.1.11.post2 (PR #5124 by @rayrayraykk)
- **⚠️ Despite the patch, users report issues persist** (see Bugs section)

### v1.1.11.post1
- **Revert:** "fix(pack): compile-check discord after conda-unpack" — suggests the original fix was problematic
- **Chore:** release duty checklist established

**Migration notes:** These are hotfix releases. No schema or config changes. Users experiencing SSL crashes or memory exhaustion should upgrade to `.post2` immediately — though reports suggest the memory leak may not be fully resolved.

---

## 3. Project Progress

### Merged Today (19 PRs closed/merged)
| PR | Title | Significance |
|----|-------|--------------|
| [#5119](https://github.com/agentscope-ai/QwenPaw/pull/5119) | style: truncate tool card titles | LIVE in v1.1.11.post2 |
| [#5124](https://github.com/agentscope-ai/QwenPaw/pull/5124) | chore: bump version to 1.1.11post2 | LIVE |
| [#5120](https://github.com/agentscope-ai/QwenPaw/pull/5120) | Release Duty v1.1.11.post1 | Pipeline automation |
| [#5126](https://github.com/agentscope-ai/QwenPaw/pull/5126) | Release Duty v1.1.11.post2 | Pipeline automation |

### Notable Open PRs Advancing
- **[#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) — Runtime 2.0 modular architecture** (Under Review): Massive refactor replacing the monolithic `Runner` with composable units + `ToolCoordinator` layer. This is the foundation for the AgentScope 2.0 migration.
- **[#5028](https://github.com/agentscope-ai/QwenPaw/pull/5028) — Isolate keychain master key per install** (Under Review): Security fix preventing cross-install credential collisions on macOS.
- **[#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) — Agent OS Driver** (Under Review): Unifying abstraction for MCP/A2A/ACP protocols — a major architecture investment.
- **[#5128](https://github.com/agentscope-ai/QwenPaw/pull/5128) — Group Langfuse observations by agent loop**: Fixes fragmented tracing in agent ReAct loops.
- **[#5121](https://github.com/agentscope-ai/QwenPaw/pull/5121) — Release Verification Gate**: Automated pre-publish health checks to catch broken builds before they hit users.

---

## 4. Community Hot Topics

### Most Active Issues

| Issue | Comments | Topic |
|-------|----------|-------|
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | 9 | **[Breaking Change]** Migrate backend from AgentScope 1.x to 2.0 — the single most impactful roadmap item, still in planning |
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) | 8 | **Bug: Scheduled tasks created by agents don't trigger** — agent-generated cron jobs silently broken |
| [#5106](https://github.com/agentscope-ai/QwenPaw/issues/5106) | 7 | **Critical: SSL cert error + infinite processes → black screen** on Windows Tauri |
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) | 6 | **Local model regression:** Qwen 3.6-27B works in 1.1.5 but broken in 1.1.9/1.1.10 |
| [#3817](https://github.com/agentscope-ai/QwenPaw/issues/3817) | 5 | **Long-standing:** Vector model config resets to empty on container restart |
| [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) | 5 | **OpenSSL 3.5 regression** blocking Desktop startup — root-caused to Python's DER parsing |
| [#5095](https://github.com/agentscope-ai/QwenPaw/issues/5095) | 5 | **Windows v1.1.11 desktop completely unable to start** |

### Underlying Needs Analysis
The community is **polarized between bleeding-edge users** (who want swarm collaboration, Headroom compression, code completion) and **stability-seeking power users** (who are hitting showstopper desktop crashes). The highest-comment issues are all **blockers** — users cannot use the product at all. This is a red flag for project health: the release pipeline is outpacing quality assurance.

---

## 5. Bugs & Stability

### 🔴 Critical (Active blocking)

| Bug | Severity | Status | Fix Exists? |
|-----|----------|--------|-------------|
| [#5106](https://github.com/agentscope-ai/QwenPaw/issues/5106) — SSL cert error + fork bomb on Windows Tauri | **CRITICAL** — black screen, memory exhaustion | Reported as open, labels: bug | Partially (PR #5088 sandbox work) |
| [#5086](https://github.com/agentscope-ai/QwenPaw/issues/5086) — OpenSSL 3.5 regression blocking Desktop | **CRITICAL** — cannot start | Closed as duplicate of #5106 | Root cause identified: Python DER parsing bug |
| [#5138](https://github.com/agentscope-ai/QwenPaw/issues/5138) — Windows client process count grows indefinitely (v1.1.11.post2) | **CRITICAL** — memory 90%+ | Open, reported TODAY | No fix PR visible |
| [#5095](https://github.com/agentscope-ai/QwenPaw/issues/5095) — Windows desktop v1.1.11 won't start | **CRITICAL** | Closed | Fix unclear from issue |

### 🟡 High Severity

| Bug | Status | Notes |
|-----|--------|-------|
| [#5140](https://github.com/agentscope-ai/QwenPaw/issues/5140) — .docx/.pdf downloads return 404 (v1.1.11.post2) | Open (TODAY) | Text files work; binaries broken. Persisted across patches. |
| [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) — Local Qwen model not responding (v1.1.9/1.1.10) | Closed | Regression from 1.1.5, root cause unclear |
| [#5064](https://github.com/agentscope-ai/QwenPaw/issues/5064) — Agent-created scheduled tasks don't fire | Open | 8 comments, no fix PR |
| [#5098](https://github.com/agentscope-ai/QwenPaw/issues/5098) — Memory search results display as `unknown` in UI | Open | New UI rendering bug |
| [#5137](https://github.com/agentscope-ai/QwenPaw/issues/5137) — Vector model config lost on save when card collapsed | Open (TODAY) | UI state serialization bug |
| [#5122](https://github.com/agentscope-ai/QwenPaw/issues/5122) — Context compression stats mismatch with actual API input | Open | Suspects MCP/tool metadata inflating context |
| [#5102](https://github.com/agentscope-ai/QwenPaw/issues/5102) — File attachments broken in v1.1.11 | Closed | Regression reported; apparent fix attempted |

### 🟢 Fixed or Mitigated
- [#5126](https://github.com/agentscope-ai/QwenPaw/issues/5126) — Release duty v1.1.11.post2 passed verification
- [#4989](https://github.com/agentscope-ai/QwenPaw/issues/4989) — Local model broken (closed, likely fixed?)

**Overall stability assessment:** 🟠 **Concerning.** Multiple CRITICAL desktop crashes reported across Tauri and PyInstaller builds. Two hotfix releases in one day suggest a reactive rather than proactive QA process. The Windows desktop experience is particularly fragile.

---

## 6. Feature Requests & Roadmap Signals

### High-Value Requested Features

| Feature | Issue | Comments | Likely Next Version? |
|---------|-------|----------|---------------------|
| **Agent Team/Swarm Collaboration** | [#5139](https://github.com/agentscope-ai/QwenPaw/issues/5139) | 1 (TODAY) | 🟡 Unlikely until Runtime 2.0 lands |
| **Headroom context compression (60-95% token savings)** | [#5063](https://github.com/agentscope-ai/QwenPaw/issues/5063) | 3 | 🟢 High potential — aligns with context concern trend |
| **Conversation queues (interrupt/steer/queue modes)** | [#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103) + [#5116](https://github.com/agentscope-ai/QwenPaw/issues/5116) | 2+1 | 🟢 Emerging theme — multiple users asking for this |
| **Per-turn token/context usage display** | [#5103](https://github.com/agentscope-ai/QwenPaw/issues/5103) | 2 | 🟢 **Already being implemented** — PR #5130 exists |
| **DingTalk private deployment custom endpoints** | [#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887) | 3 | 🟡 Enterprise need, but not urgent |
| **Code completion in Coding mode** | [#5131](https://github.com/agentscope-ai/QwenPaw/issues/5131) | 1 | 🟠 Nice-to-have, low signal |
| **Quote/reference text for follow-up (like Perplexity)** | [#5110](https://github.com/agentscope-ai/QwenPaw/issues/5110) | 1 | 🟡 Useful UX improvement |
| **Tool Guard approval collapse/persist after decision** | [#5107](https://github.com/agentscope-ai/QwenPaw/issues/5107) | 1 | 🟢 Simple UI fix likely to ship soon |

### Roadmap Signals
- **Runtime 2.0 (PR #5078)** is the most consequential architectural change — it directly enables modular agent composition and the AgentScope 2.0 migration.
- **Langfuse observability (PR #5128)** signals a push toward production-grade monitoring.
- **Agent OS Driver (PR #5067)** indicates multi-protocol agent orchestration is a strategic direction.
- **DataPaw plugin (PR #4622)** shows plugin ecosystem growth — 12 BI skills bundled.

---

## 7. User Feedback Summary

### Pain Points (most frequent)
1. **Desktop client crashes** — "black screen", "endless processes", "memory 90%", "can't start" — multiple users across Windows Tauri and PyInstaller builds. The dominant complaint.
2. **File download regression** — `.docx`/`.pdf`/images return 404. Text works. Users having to roll back to 1.1.10.
3. **Local model regressions** — Qwen model works in 1.1.5, broken in newer versions. Users losing trust in upgrades.
4. **Scheduled task unreliability** — agents can create cron jobs but they silently don't fire.
5. **Memory search UI rendering bug** — shows `unknown` instead of file paths. Functionally works but confusing.
6. **Vector model config not persisting** — known bug since April (#3817), still not fully fixed.

### Positive Signals
- Users are actively exploring features (scheduled tasks, memory search, context compression).
- Several users migrating from/workflow-switching with other tools (OpenClaw, WorkBuddy, JiuwenSwarm) — indicating market competition awareness.
- First-time contributors are arriving with meaningful PRs (Portuguese i18n, changelog agent, AionUI design replication).
- The `enable_thinking` configuration (#5132) shows power users are fine-tuning model behavior.

### Satisfaction Indicators
- **Low:** High-frustration language ("无法正常使用", "没法用!", "回退到1.1.10") indicates customer churn risk.
- **Moderate:** Users who can keep working by not upgrading or using Docker are stable but wary.

---

## 8. Backlog Watch

### Aging Issues Needing Maintainer Attention

| Issue | Age | Last Update | Why It Matters |
|-------|-----|-------------|----------------|
| [#3817](https://github.com/agentscope-ai/QwenPaw/issues/3817) | **53 days** | 2026-06-11 | Vector model config reset on container restart — reported April 24, still unfixed. Workaround discussed but no official fix. |
| [#1533](https://github.com/agentscope-ai/QwenPaw/issues/1533) | **89 days** | 2026-06-11 | `install.sh` hangs due to curl output flood. Trivial fix proposed, still open. |
| [#4727](https://github.com/agentscope-ai/QwenPaw/issues/4727) | **16 days (created May 27)** | 2026-06-12 | **Breaking Change** — AgentScope 2.0 migration. No PR yet. This is the biggest roadmap item and it's not moving. |
| [#4887](https://github.com/agentscope-ai/QwenPaw/issues/4887) | **10 days** | 2026-06-11 | DingTalk custom endpoint for enterprise. Unresolved. |
| [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) | **21 days (PR opened)** | 2026-06-11 | DataPaw plugin — first-time contributor, still "Under Review" after 3 weeks. Risk of contributor burnout. |

### PRs Needing Review
| PR | Days Open | Reviewer Needed? |
|----|-----------|-----------------|
| [#4622](https://github.com/agentscope-ai/QwenPaw/pull/4622) — DataPaw plugin | 21 | Yes — contributor may lose motivation |
| [#5078](https://github.com/agentscope-ai/QwenPaw/pull/5078) — Runtime 2.0 | 2 | Under active review — this is moving |
| [#5067](https://github.com/agentscope-ai/QwenPaw/pull/5067) — Agent OS Driver | 2 | Under review |
| [#5036](https://github.com/agentscope-ai/QwenPaw/pull/5036) — Session filename fix | 3 | Last activity today — positive |

---

## Executive Summary

CoPaw is in a **stabilization firefight** following the v1.1.11 release. Today's two hotfixes (.post1, .post2) addressed some cosmetic issues and release pipeline problems, but the core desktop crash bugs (SSL fork bomb, infinite process growth) remain open. The community is vocal: 33 issues updated, 42 PRs touched, but 7+ are showstopper bugs. 

**Key risks:**
1. **Desktop reliability crisis** — Windows Tauri users are having the worst experience. This could damage trust.
2. **Local model regressions** — users who self-host are hit hardest, and they are the most loyal community.
3. **Aging backlog** — #3817 (53 days old) and #1533 (89 days old) signal low priority on community pain points.

**Bright spots:**
- Runtime 2.0 and Agent OS Driver PRs represent strategic architecture investments.
- First-time contributor pipeline is healthy — 7 new contributors today.
- Langfuse integration, per-turn token stats, and skill market improvements show product maturation.

**Recommendation:** Prioritize a **stability sprint** — fix the desktop memory leaks and file download regression before adding new features. The current velocity is sacrificing quality.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the ZeroClaw project digest for June 12, 2026.

---

## ZeroClaw Project Digest: 2026-06-12

### 1. Today's Overview

ZeroClaw v0.8.0, "the big one," has just landed, representing a major architecture shift towards a multi-agent daemon. However, the immediate aftermath shows a firehose of activity: 50 open issues and 50 pull requests were updated in the last 24 hours, suggesting the community is rapidly testing and reporting feedback on the new release. The project is in a high-velocity but turbulent state, with a focus on squashing critical regressions and stabilizing the new multi-agent unified runtime.

### 2. Releases

**v0.8.0** was released today. This is a major milestone that fundamentally changes the ZeroClaw architecture.

- **Key Change:** The daemon now runs many named agents from a single process, each with its own workspace, memory, model provider, security policy, channels, and personality.
- **Configuration:** A rewritten configuration schema is included, alongside automatic migration from older setups.
- **Breaking Changes:** This is a paradigm shift (from single-agent to multi-agent runtime). Users should expect configuration schema incompatibilities and review the full changelog for migration specifics.

### 3. Project Progress

Two PRs were merged/closed today, both focused on release stabilization and the v0.8.0 launch:

- **Merged [#7520](https://github.com/zeroclaw-labs/zeroclaw/pull/7520):** A CI fix to install a cross-compilation g++ for ARM glibc targets, which was blocking the v0.8.0 Release Stable build. This unblocked the official release.
- **Closed [#7519](https://github.com/zeroclaw-labs/zeroclaw/pull/7519):** A fix for the configuration system's `[[mcp.servers]]` editor, which was not persisting per-field edits to disk. This resolves a major configuration usability bug introduced in a recent PR ([#7267](https://github.com/zeroclaw-labs/zeroclaw/pull/7267)).

### 4. Community Hot Topics

The most active discussions highlight major pain points and desired features for the new v0.8.0 architecture:

- **[#5849 - Feature: Dream Mode](https://github.com/zeroclaw-labs/zeroclaw/issues/5849)** (17 comments): A request for a background process that consolidates memories and reflects on interactions. This is a highly popular feature request signaling a strong desire for agents with persistent, learning long-term memory.
- **[#6699 - Bug: tool_filter_groups no-op](https://github.com/zeroclaw-labs/zeroclaw/issues/6699)** (7 comments): A high-priority bug report detailing how the `tool_filter_groups` configuration does not work for real MCP tools. This is a critical workflow blocker for users relying on tool security policies, and a fix is under development (status: `in-progress`).
- **[#7470 - Bug: Delegate agentic mode rejects empty allowed_tools](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)** (7 comments, created today): A newly reported S1 bug where multi-agent delegation fails when a sub-agent has an empty `allowed_tools` list. This is a significant design flaw in the new multi-agent runtime that blocks complex workflows.
- **[#5808 - Bug: Perpetual context trimming](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)** (3 comments): Users report that the default 32k context budget is immediately exceeded by system prompts and tool definitions, causing the agent to perpetually trim context from the very first interaction. This is a usability regression in v0.8.0 for users with complex tool sets.

### 5. Bugs & Stability

The project is dealing with a wave of S1 and S2 severity bugs, many related to the new v0.8.0 architecture. Key issues with high risk include:

- **S1 / Critical:**
    - **[#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470) (New):** Delegate agentic mode rejects empty `risk_profile.allowed_tools`. (Fix PR not yet created).
    - **[#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037):** Cron jobs can launch repeatedly while still running, causing runaway execution. A fix PR exists ([#6038](https://github.com/zeroclaw-labs/zeroclaw/pull/6038)) but is tagged `needs-author-action`.
    - **[#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542):** Consecutive Out-Of-Memory errors in WSL2, leading to process death.
    - **[#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699):** `tool_filter_groups` is a no-op for real MCP tools, rendering agent security policies ineffective.
- **S2 / High:**
    - **[#6173](https://github.com/zeroclaw-labs/zeroclaw/issues/6173):** `model_switch` tool does not persist the model change across turns, and the gateway/UI ignores it entirely.
    - **[#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903):** MCP stdio child processes leak (one orphan per heartbeat tick), accumulating over the daemon's lifetime.
- **Security:**
    - **[#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470):** Multi-agent delegation bypasses tool restrictions.
    - **[#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699):** `tool_filter_groups` is ineffective, negating agent-level security policies.

### 6. Feature Requests & Roadmap Signals

The community is actively pushing for features that turn ZeroClaw from a task-runner into a proactive, learning system:

- **Autonomous Memory & Learning [#5849](https://github.com/zeroclaw-labs/zeroclaw/issues/5849):** "Dream Mode" is the top-voted feature, indicating a strong desire for agents that consolidate experiences and improve over time. This is a strong candidate for a future v0.9.x release.
- **Advanced Health & Monitoring [#6391](https://github.com/zeroclaw-labs/zeroclaw/issues/6391):** For users running fleets of agents, real heartbeat tracking is critical. The request to derive health status from WebSocket message activity is a clear roadmap signal for production-grade features.
- **Fleet Management CLI [#6390](https://github.com/zeroclaw-labs/zeroclaw/issues/6390):** The request for a `zeroclaw node add <url>` command to register remote daemons directly aligns with the multi-agent vision. This is a logical next step for v0.8.x.

### 7. User Feedback Summary

The v0.8.0 release has generated a lot of feedback, both positive and negative.

- **Pain Points (Dissatisfaction):**
    - **Configuration & Security are broken:** Users are reporting that security features like tool filtering (`allowed_tools`/`denied_tools`) are either a no-op ([#6699](https://github.com/zeroclaw-labs/zeroclaw/issues/6699)) or block workflows ([#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)). This is the most prominent source of frustration, as it prevents users from safely deploying the new multi-agent system.
    - **Context Trimming is too aggressive:** The default context budget is immediately exceeded, causing the agent to constantly forget its instructions ([#5808](https://github.com/zeroclaw-labs/zeroclaw/issues/5808)).
    - **Platform-Specific Issues:** Users on Windows ([#7214](https://github.com/zeroclaw-labs/zeroclaw/pull/7214)) and WSL2 ([#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542)) are encountering critical system-level bugs (process execution, OOM).
- **Use Cases:**
    - The active discussion on delegate agents ([#7470](https://github.com/zeroclaw-labs/zeroclaw/issues/7470)) explicitly details a "multi-agent reviewer/research setup," where a supervisor agent delegates to specialist sub-agents. This is a core use case for the new architecture.
    - The persistent `cron` failures ([#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037), [#6224](https://github.com/zeroclaw-labs/zeroclaw/issues/6224)) show heavy reliance on scheduled workflows, with a particular need for reliable delivery to messaging channels like WhatsApp.

### 8. Backlog Watch

Several high-risk issues and PRs have been open for a month or more and are at risk of becoming stale, requiring maintainer attention:

- **[#6037](https://github.com/zeroclaw-labs/zeroclaw/issues/6037) - Bug: Repeated Cron Job Execution** (1 comment): An S1 bug open since April 23 with a fix PR ([#6038](https://github.com/zeroclaw-labs/zeroclaw/pull/6038)) that is tagged `needs-author-action`.
- **[#5542](https://github.com/zeroclaw-labs/zeroclaw/issues/5542) - Bug: OOM in WSL2** (S0 risk): A data-loss/security risk bug open since April 9 that has no fix linked and is tagged `r:needs-repro`.
- **[#5903](https://github.com/zeroclaw-labs/zeroclaw/issues/5903) - Bug: MCP stdio Process Leak** (S1 risk): Open since April 19 with no linked fix, this represents a significant resource drain for any production daemon.
- **[#5661](https://github.com/zeroclaw-labs/zeroclaw/pull/5661) - PR: Wire Cron CLI Delivery Flags** (XL size): Open since April 12 and tagged `needs-author-action` & `stale-candidate`. This is a significant enhancement to the cron system that is at risk of being abandoned.
- **[#6085](https://github.com/zeroclaw-labs/zeroclaw/pull/6085) - PR: Default Session TTL** (HIGH risk): Open since April 24 and tagged `needs-author-action`, this fix is important for preventing unbounded session storage.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*