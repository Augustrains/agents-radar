# OpenClaw Ecosystem Digest 2026-06-07

> Issues: 301 | PRs: 500 | Projects covered: 13 | Generated: 2026-06-07 02:10 UTC

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

Here is the OpenClaw project digest for 2026-06-07, generated from the provided GitHub data.

---

### OpenClaw Project Digest: 2026-06-07

#### 1. Today's Overview
The OpenClaw project is in a high-activity state, with 301 issues and 500 pull requests updated in the last 24 hours. The release of two beta versions (v2026.6.5-beta.1 and .2) indicates active stabilization efforts. However, the high volume of open PRs (400) and critical bug reports suggests that the project is currently prioritizing bug fixes and stability over new feature development. A significant number of "platinum hermit" and "diamond lobster" rated issues signal persistent, high-impact regressions that are demanding maintainer attention.

#### 2. Releases
Two new beta releases were published: **v2026.6.5-beta.1** and **v2026.6.5-beta.2**.

- **Key Changes:**
    - **QQBot Fix:** A critical fix prevents raw model thinking/reasoning output (e.g., `<thinking>` tags) from leaking into channel replies. (PRs #89913, #90132)
    - **MCP Tool Improvements:** Results from MCP tools are now coerced for data types such as `resource_link`, `resource`, `audio`, and malformed images, improving robustness.
- **Migration Notes:** These are beta releases on the path to a stable v2026.6.5. Users on the `latest` npm tag (v2026.6.1) should await the stable release. No breaking changes are explicitly mentioned, but users of QQBot should verify that thinking content is no longer leaked.

#### 3. Project Progress
Today saw 100 PRs merged or closed. Key areas of progress include:

- **Gateway & Configuration:** A fix for the `openclaw configure` wizard now masks sensitive input like the gateway token, improving security. (PR #91059)
- **UI Stability:** A fix for the WebUI's Skills panel corrects a bug where toggling a skill inadvertently affected the state of a different skill in the list. (PR #89681)
- **Anthropic Provider:** Support for Claude Haiku 4.5 has been added to the static model catalog. (PR #90110)
- **UI/UX Polish:** An important fix now collapses non-terminal internal tool errors (e.g., a search returning no results) in the WebChat timeline, preventing confusing red banners from appearing when the final reply is successful. (PR #90122)
- **Session Management:** A new PR introduces logic to prune stale gateway model-run probe sessions, preventing session table bloat. (PR #91057)

#### 4. Community Hot Topics
The community is most engaged around regressions in core functionality, particularly with the latest stable release (v2026.6.1).

- **#90083 ([OPEN])** - **Critical:** OpenAI ChatGPT Responses transport fails with `invalid_provider_content_type` for GPT-5.4/5.5. This is a high-impact bug blocking users of the latest OpenAI models. (14 comments, 3 👍)
- **#88312 ([OPEN])** - **Regression:** The "Codex stopped before confirming the turn was complete" error has returned in v2026.5.27. Users are frustrated as this is a regression of a previously fixed bug (#84076). (13 comments, 3 👍)
- **#90991 ([OPEN])** - **Stability:** A cron schedule trigger is suspected of contaminating global runtime state, causing transient "system-wide overload" failures for all users. (7 comments, 1 👍)
- **#91018 ([OPEN])** - **Cost Impact:** Upgrading to 2026.6.1 has reportedly broken DeepSeek's prompt cache, leading to a $6 cost increase in one hour for one user. This is a severe financial stability issue for users on consumption-based plans. (4 comments, 1 👍)

#### 5. Bugs & Stability
The data shows a significant number of high-severity, recently reported bugs. The most critical are:

- **Critical (P1, Platinum Hermit Rating):**
    - **OpenAI GPT-5.4/5.5 Transport Failure (#90083):** As noted above, blocks use of newest models. **Status:** No fix PR linked.
    - **Cron Trigger Runtime Contamination (#90991):** Causes system-wide failures. **Status:** No fix PR linked.
    - **DeepSeek Prompt Cache Inefficiency (#91018):** Causes severe cost spikes. **Status:** No fix PR linked.
    - **Subagent Compaction Routing Bug (#90925):** Subagent completion crashes on the Codex/OAuth route. **Status:** No fix PR linked.
    - **Gateway Hang on Startup (#90886):** The gateway hangs at startup if a configured provider lacks credentials. **Status:** No fix PR linked.
    - **Codex App-Server Turn-Completion Stall (#88312):** Regression of a previously fixed bug. **Status:** No fix PR linked.

- **High (P1, Diamond Lobster Rating):**
    - **Orphaned Lock Files (#49603):** Lock files not cleared on gateway restart, causing potential startup failures. **Status:** No fix PR linked.
    - **Agent Internal Thinking Exposed (#64267):** A security and confidentiality bug exposing internal AI reasoning to end-users. **Status:** No fix PR linked.

#### 6. Feature Requests & Roadmap Signals
- **Per-candidate Retry Count (#59413):** A request for model fallback to retry a failing provider before switching. This is critical for users of pool-based API proxies. Given the focus on stability, this is a strong candidate for the next version.
- **Topic-Session Families (#90916):** A sophisticated request for an assistant to maintain multiple isolated conversation contexts. This signals advanced use cases but is likely a longer-term roadmap item (P2).
- **Self-hosted STT/TTS (#45508):** Users want to use their own TTS/STT services in the webchat instead of the browser's built-in API. This is a persistent request (created Mar 2026) for a more self-hosted experience.
- **Gateway-Side Circuit Breaker (#62615):** A request to automatically stop retrying sessions that are in a persistent failure loop. This is another stability-focused feature that may be prioritized.
- **Better Local Model Support (#89265):** A user request to treat local/open-weight models as first-class citizens. This signals a growing demand for privacy and cost control.

#### 7. User Feedback Summary
- **Pain Points:** The dominant theme is frustration with **regressions** in the latest stable releases. Users upgrading to v2026.6.1 are experiencing broken API transports (OpenAI, DeepSeek) and inflated costs. The recurrence of previously fixed bugs (e.g., Codex turn-completion stall) is a significant source of dissatisfaction.
- **User Behavior:** Users are actively reporting bugs, participating in reproducible steps, and expressing financial concerns (e.g., "burned $6 in one hour").
- **Unmet Needs:** There is a clear need for more robust regression testing before stable releases. The high number of "needs-maintainer-review" tags suggests a bottleneck in the triage process.

#### 8. Backlog Watch
Several high-severity issues have been open for weeks, signaling a heavy burden on the maintainer team.

- **#49603 ([OPEN])** - **"Orphaned lock files not cleared..." (Created: March 18)**: A P1 issue open for nearly 3 months. The fix requires sweeping locks owned by the current PID on restart.
- **#64267 ([OPEN])** - **"OpenClaw 2026.4.9 exposes agent internal thinking..." (Created: April 10)**: A P1 security and confidentiality bug open for nearly 2 months. The fix likely requires sanitizing internal model output.
- **#58730 ([OPEN])** - **"exec() sandbox isolation..." (Created: April 1)**: A comprehensive feature request for security improvements, currently languishing with multiple "needs" labels (review, product decision, etc.).
- **#68280 ([OPEN])** - **"fail fast on missing local probe auth" (Created: April 17)**: A fix for CLI status command behavior, still "waiting on author" nearly two months later.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report you requested.

---

## Cross-Project Ecosystem Report: Open-Source AI Agent Frameworks
**Date:** 2026-06-07
**Analyst:** AI Agent Ecosystem Senior Analyst

### 1. Ecosystem Overview

The open-source personal AI assistant and agent ecosystem is in a period of **intense, multi-faceted maturation**. Projects are no longer just proving conversational ability; they are racing to solve **production-grade challenges** including streaming reliability, multi-user context isolation, financial stability (prompt caching), and deterministic workflow execution. A clear bifurcation is emerging between projects focused on **broad, multi-channel consumer agents** (e.g., OpenClaw, NanoBot) and those building **specialized infrastructure** for developers and edge deployment (e.g., PicoClaw, ZeptoClaw). The ecosystem's primary pain point, echoed across nearly every project, is **regression management**—users consistently report frustration with stable updates breaking core features, indicating a systemic need for better CI/CD and integration testing practices. The push toward **WASM plugin ecosystems** (ZeroClaw) and **deterministic sub-agent engines** (Hermes Agent, LobsterAI) signals a shift from monolithic agents to modular, composable architectures.

### 2. Activity Comparison

| Project | Updated Issues (24h) | Updated PRs (24h) | Merged/Closed Today | Release Today | Health Score (Qualitative) |
|---|---|---|---|---|---|
| **OpenClaw** | 301 | 500 | 100 | ✅ (2 beta) | Moderate (High activity but critical regressions) |
| **ZeroClaw** | 39 | 50 | 5 | ❌ | High (Fast bug-fix cadence, rapid feature expansion) |
| **PicoClaw** | 12 | 18 | 15 | ✅ (nightly) | High (Major stability sweep, new features merged) |
| **NanoBot** | 7 | 24 | 10 | ❌ | High (Broad contributor diversity, responsive maintainers) |
| **Hermes Agent** | 50 | 50 | 11 | ❌ | Moderate (High volume but significant backlog of critical bugs) |
| **IronClaw** | ~10 | 31 | 10 | ❌ | Moderate (Active development but pending release blocking) |
| **NanoClaw** | 2 | 14 | 3 | ❌ | Moderate (Healthy maintenance, few regressions) |
| **LobsterAI** | 6 | 0 | 0 | ❌ | Low (Minimal activity, 2-month-old bugs unaddressed) |
| **CoPaw** | 11 | 0 | 0 | ❌ | Critical (High-severity regressions, no fix PRs) |
| **Moltis** | 3 | 0 | 0 | ❌ | Low (Low activity, new bugs unaddressed) |
| **NullClaw** | 0 | 0 | 0 | ❌ | Dormant |
| **TinyClaw** | 0 | 0 | 0 | ❌ | Dormant |
| **ZeptoClaw** | 2 | 1 | 0 | ❌ | Good (Focused maintenance, clear roadmap) |

### 3. OpenClaw's Position

- **Advantages vs. Peers:**
    - **Scale:** With 301 issues and 500 PRs updated in 24 hours, OpenClaw has the largest and most active contributor base in the ecosystem by a significant margin.
    - **Release Cadence:** OpenClaw is the only project publishing multiple beta releases in a single day, demonstrating a strong commitment to rapid iteration.
    - **Feature Depth:** Support for Claude Haiku 4.5, MCP tool improvements, and UI/UX polishing (e.g., collapsing non-terminal errors) shows a mature, detail-oriented team.
- **Technical Approach Differences:**
    - OpenClaw relies on a **`openclaw configure` wizard** for security (masking sensitive input), suggesting a focus on ease-of-setup for non-developer users. In contrast, PicoClaw and ZeptoClaw use YAML/TOML configuration files, appealing to developers.
    - Its **`compact` command** and session management logic are more sophisticated than many peers, but the high number of regressions (e.g., Codex turn-completion stall) suggests a more complex codebase with less robust refactoring guardrails.
- **Community Size Comparison:**
    - OpenClaw's community is the largest by raw engagement. However, zero upvotes on many of its critical bug reports (e.g., #90083, #88312) may indicate either a small group of very active users or that bugs are being discovered internally. In contrast, ZeroClaw's high-severity bugs see rapid community engagement and thumbs-ups.
- **Key Weakness:** The sheer volume of work is creating a **bottleneck**. The backlog of P1 issues (#49603, #64267) open for months indicates a risk of the maintainer team being overwhelmed by the project's own scale.

### 4. Shared Technical Focus Areas

The following requirements are emerging from **multiple projects simultaneously**, indicating cross-cutting industry needs:

1.  **Integration Reliability & Error Handling:**
    - **Projects:** NanoBot, ZeroClaw, PicoClaw, CoPaw, Moltis
    - **Specific Needs:** Fixes for streaming parsing correctness (NanoBot #4228), handling of malformed API responses (OpenClaw, CoPaw #4989), and silent failures in MCP tool connections (NanoBot #4211).
2.  **Security & Data Isolation:**
    - **Projects:** NanoBot, Hermes Agent, PicoClaw, ZeroClaw
    - **Needs:** Per-user memory isolation (NanoBot #2968), per-MCP-server access control (NanoBot #2533), sandboxing for tool execution (NanoBot #4221, PicoClaw #3022), and SSRF guards for MCP URLs (NanoBot #4123, ZeroClaw #7335).
3.  **Deterministic Workflows & Agent Orchestration:**
    - **Projects:** Hermes Agent, LobsterAI, NanoBot, NanoClaw
    - **Needs:** The ability to execute repetitive tasks without LLM re-planning (Hermes Agent #5354), support for cron/scheduled tasks (NanoBot, LobsterAI, Moltis), and agent-to-agent communication protocols (PicoClaw, Hermes Agent).
4.  **Model & Provider Caching Efficiency:**
    - **Projects:** OpenClaw, NanoBot
    - **Needs:** Users are reporting severe cost increases due to broken prompt caching (OpenClaw #91018) and prefix shifting that defeats caching entirely (NanoBot #4222). This highlights a growing pain point for consumption-based API users.
5.  **Multi-User & Channel Support:**
    - **Projects:** NanoBot, Hermes Agent, PicoClaw
    - **Needs:** Hardware- or memory-level isolation for users in shared deployments (NanoBot, Hermes Agent), robust support for specific channels like WhatsApp, DingTalk, and Google Chat (all three), and fixes for duplicate message delivery (NanoClaw #2697).

### 5. Differentiation Analysis

| Feature / Target | OpenClaw (Consumer Agent) | ZeroClaw (Developer Platform) | PicoClaw (Edge/Hardware) | Hermes Agent (Autonomous Agent) |
|---|---|---|---|---|
| **Primary User** | End-users, community managers | Developers, plugin authors | Embedded engineers, scripters | Power users, DevOps |
| **Core Strength** | Chat, release cadence | WASM plugin ecosystem, security | Stability, minimal overhead | Autonomous workflows, tooling |
| **Key Differentiator** | User-friendly wizard, GUI | Plugin registry, sandboxed plugins | Tiny binary, Go-routines | "Deterministic" engine requests |
| **Biggest Risk** | Regressions from rapid change | Complexity of WASM adoption | Niche hardware focus | Backlog of critical bugs |
| **Community Vibe** | Reactive, but community-driven | Planned, roadmap-driven | Policing, code-quality focused | Frustrated with regressions |

- **NanoBot** sits between OpenClaw and ZeroClaw, focusing on **multi-user enterprise readiness** (per-user memory, access control) and **infrastructure reliability** (streaming fixes). It is the most "enterprise-ready" framework for shared deployments.
- **IronClaw** (Reborn architecture) is the most **architecturally innovative**, with a focus on product workflow routing and OpenAI-compatible API layers, targeting backend integration.
- **CoPaw** and **LobsterAI** are lagging in activity but have strong niche communities (China market for CoPaw, coding environment for LobsterAI). Their low activity this week may be temporary but is a warning sign.
- **ZeptoClaw** is the most **focused project**, solely optimizing binary size for robot/edge deployment. It is not competing in the broader agent ecosystem.

### 6. Community Momentum & Maturity

- **Tier 1 (High Momentum, Rapid Iteration):**
    - **ZeroClaw, PicoClaw, NanoBot.** These projects show healthy, maintainer-driven cadence, broad contributor diversity, and effective bug fixing. Release velocity is high, and security/functionality features are landing daily.
- **Tier 2 (High Activity but Struggling):**
    - **OpenClaw, Hermes Agent.** Massive contributor engagement is a positive, but critical regressions and unresolved P1 backlogs signal that the community may be outpacing the core maintainer team. Without investment in triage and testing infrastructure, these projects risk developer churn.
- **Tier 3 (Stable/Maintenance Phase):**
    - **NanoClaw, IronClaw, ZeptoClaw.** These projects are less active but show clear, deliberate progress. They are in a consolidation phase, polishing existing features rather than expanding.
- **Tier 4 (Stalling):**
    - **LobsterAI, CoPaw, Moltis.** Low activity with unresolved bugs from April is a warning. Users are reporting regressions but receiving no response. These projects may be at risk of losing community trust.

### 7. Trend Signals

Several industry trends emerge from the feedback and code changes across these projects:

1.  **From "Chat Assistant" to "Autonomous Worker":** Users are no longer satisfied with chat. They want agents that can run scheduled tasks (cron), handle repetitive workflows deterministically, and integrate with external tools (Slack, Discord, GitHub). This is driving demand for **rule engines, workflow orchestration, and sub-agent delegation**.
2.  **The Plugin Economy is the Next Frontier:** ZeroClaw's investment in WASM plugins, coupled with NanoBot's MCP security controls and PicoClaw's tool policy filters, signals a future where agents are extended not by forking the codebase, but by installing sandboxed plugins. The **remote plugin registry** (ZeroClaw) is a critical enabler for this.
3.  **Cost of Intelligence is Becoming a UX Problem:** Users are acutely aware of API costs. Broken prompt caching (OpenClaw), prefix shifting (NanoBot), and unnecessary LLM calls for simple tasks (Hermes Agent) are now being reported as bugs. Future success will depend on **efficient token usage** and transparent cost controls.
4.  **Security is a Shared Pain, Not a Feature:** The proliferation of SSRF guards, MCP access controls, memory isolation, and per-user policies across every major project shows that security is now table-stakes. Projects that treat security as an afterthought (like Moltis's authentication bug will quickly lose users.
5.  **Regressions are the Number One Trust Killer:** The most common sentiment across all projects is frustration from breaking changes in stable releases. The community is signaling a need for **long-term support (LTS) releases** and **comprehensive end-to-end test suites** before any new feature lands.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-06-07

## 1. Today's Overview

NanoBot is seeing exceptional community activity today with 24 pull requests updated in 24 hours (10 merged/closed) and 7 issues updated (3 closed). The 24 PRs represent a surge in contributor engagement, with 14 still open for review. While no new releases are published, the project is processing a high volume of merges from long-running feature branches and urgent bug fixes. The most active areas this week are streaming response parsing correctness, MCP security hardening, session history edge cases, and WhatsApp bridge reliability improvements. Project health appears strong with broad contributor diversity and responsive maintainers, though the backlog of 14 open PRs suggests some review bottlenecks may be forming.

## 2. Releases

No new releases today. The latest published version remains **nanobot v0.1.4.post6**.

## 3. Project Progress

**Merged/Closed PRs (10 total):**

- **#4228** (`Yuxin-Lou`) — fix: preserve empty reasoning_content in streaming response parsing. Fixes issue #4105 where custom providers losing `reasoning_content=""` caused downstream API errors with DeepSeek thinking mode. *(PR: https://github.com/HKUDS/nanobot/pull/4228)*
- **#2968** (`franciscomaestre`) — feat(memory): per-user memory isolation via `agents.defaults.per_user_memory`. Major multi-user enabling feature allowing separate `MEMORY.md`/`history.jsonl` per user. *(PR: https://github.com/HKUDS/nanobot/pull/2968)*
- **#2555** (`franciscomaestre`) — fix(whatsapp-bridge): close existing clients on new connection to prevent duplicate messages. *(PR: https://github.com/HKUDS/nanobot/pull/2555)*
- **#2533** (`franciscomaestre`) — feat: per-MCP-server allowFrom access control. Security feature for multi-user deployments. *(PR: https://github.com/HKUDS/nanobot/pull/2533)*
- **#2532** (`franciscomaestre`) — feat(search): add Serper.dev as Google Search provider. *(PR: https://github.com/HKUDS/nanobot/pull/2532)*
- **#2529** (`franciscomaestre`) — fix(whatsapp-bridge): download audio messages for transcription. *(PR: https://github.com/HKUDS/nanobot/pull/2529)*
- **#2528** (`franciscomaestre`) — fix(whatsapp-bridge): drop messages older than startup to avoid replaying history. *(PR: https://github.com/HKUDS/nanobot/pull/2528)*
- **#4195** (`Re-bin`) — feat(desktop): polish desktop shell and shared WebUI surfaces. First open desktop surface preparation. *(PR: https://github.com/HKUDS/nanobot/pull/4195)*
- **#4209** (`04cb`) — fix(providers): allow dropping default OpenAI image params via null extraBody. Fixes issue #4167 where `response_format` was rejected by compatible APIs. *(PR: https://github.com/HKUDS/nanobot/pull/4209)*
- **#4211** (`pblocz`) — [CLOSED] SDK stdio MCP cancel scope error. Fixes the task cancellation crash at shutdown. *(Issue: https://github.com/HKUDS/nanobot/issues/4211)*

## 4. Community Hot Topics

1. **#2573 — GitHub Copilot login failure** (closed, 9 👍)  
   Users reporting `Authorization header is badly formatted` error when running `nanobot provider login github-copilot`. Suspected regression after switching from litellm to OpenAI library. High community interest (9 thumbs up).  
   *(Issue: https://github.com/HKUDS/nanobot/issues/2573)*

2. **#4222 — max_messages truncation and microcompact invalidate prefix/prompt caching** (open, 0 comments)  
   A well-analyzed deep-dive bug report explaining how two context governance mechanisms (`max_messages` truncation and microcompact) cause the message prefix to shift every turn, defeating LLM prompt caching. Signals growing usage of caching-dependent workflows.  
   *(Issue: https://github.com/HKUDS/nanobot/issues/4222)*

3. **#4218 — WebUI Cron Job Management** (open)  
   Feature request for UI-based cron job management. User highlights that while CLI is fully-featured, requiring manual editing of `config.json` is error-prone. Indicates demand for WebUI parity with CLI capabilities.  
   *(Issue: https://github.com/HKUDS/nanobot/issues/4218)*

4. **#4220 — GitHub Copilot for Business/Enterprise support** (open)  
   Request for GHE/Copilot for Business API endpoint support. Shows enterprise adoption interest beyond individual GitHub accounts.  
   *(Issue: https://github.com/HKUDS/nanobot/issues/4220)*

## 5. Bugs & Stability

| Severity | Issue | Description | Fix Status |
|----------|-------|-------------|------------|
| **High** | #4222 | `max_messages` truncation + microcompact causes prefix to shift every turn, defeating all LLM prompt caching | No PR yet |
| **Medium** | #4105 | Custom provider drops `reasoning_content=""` from tool_call messages → breaks APIs requiring empty string | Fixed in #4228 (merged), #4227 (open) |
| **Medium** | #4211 | SDK leaves stdio MCP open → runtime error at shutdown | Closed (fix merged) |
| **Low** | #4167 | Image generation fails with OpenAI-compatible APIs lacking `response_format` support | Fixed in #4209 (merged) |
| **Low** | #4221 | Relative symlink workspace escape in ExecTool → security risk | PR #4221 (open) |

The two most impactful fixed bugs this week are the `reasoning_content` empty-string coercion (#4105) and the OpenAI image `response_format` rejection (#4167), both affecting production workflows with custom providers.

## 6. Feature Requests & Roadmap Signals

**Predicted for next release:**

1. **Per-user memory isolation** (#2968) — already merged, likely shipping in v0.1.5. Enables multi-user deployments where agents maintain separate context.
2. **WhatsApp bridge reliability bundle** (multiple PRs from `franciscomaestre`: #2555, #2528, #2529, #4226) — five merged PRs this week alone targeting the WhatsApp Baileys bridge. Strong signal that multi-channel production stability is a priority.
3. **Desktop shell preparation** (#4195) — merged, indicates NanoBot is preparing a desktop-native surface alongside the existing WebUI.
4. **Serper.dev search provider** (#2532) — merged, broadening web search options beyond existing providers.

**User-requested for future:**

- **WebUI Cron management** (#4218) — likely to be developed given the pattern of recent WebUI improvements.
- **GitHub Copilot Enterprise** (#4220) — lower priority but relevant for organizational adoption.
- **AssemblyAI transcription** (#4224, open PR) — new provider option for audio transcription, likely to merge.

## 7. User Feedback Summary

**Pain points expressed:**
- GitHub Copilot login failure (#2573) caused frustration with 9 reactions — the highest-traffic issue despite being closed.
- Users report "error-prone" manual `config.json` editing for cron jobs (#4218), preferring UI controls.
- Production users experience "permanent silent dead loop" when WeChat session tokens expire (#4223 PR description), forcing complete re-authentication.
- Multi-user deployments face "personal data mixing" without memory isolation (#2968 PR description).

**Positive signals:**
- Broad contributor diversity with distinct domains: MCP security (`yu-xin-c`), WhatsApp infrastructure (`franciscomaestre`), streaming correctness (`michaelxer`, `Yuxin-Lou`), UI/desktop (`Re-bin`).
- Bug reports show deep technical understanding (e.g., #4222's analysis of prompt caching mechanics), indicating mature user base.

## 8. Backlog Watch

| Item | Age | Issue/PR | Concern |
|------|-----|----------|---------|
| **#4033 — Chat sender identity for multi-user channels** | 10 days (open) | [PR](https://github.com/HKUDS/nanobot/pull/4033) | Important for Discord/multi-user context, no review activity since May 28 |
| **#4094 — Channel dispatch durability & stream identity** | 9 days (open) | [PR](https://github.com/HKUDS/nanobot/pull/4094) | Fixes WebSocket message persistence issue #4062, needs review |
| **#4123 — SSRF guard for MCP URLs** | 7 days (open) | [PR](https://github.com/HKUDS/nanobot/pull/4123) | Security hardening, low review activity despite importance |
| **#4219 — Drop orphan tool results before trimming history** | 1 day (open) | [PR](https://github.com/HKUDS/nanobot/pull/4219) | Fixes #4203, fresh but related to #4229 — may need coordination between PRs |
| **#4222 — prefix/prompt caching invalidation** | 1 day | [Issue](https://github.com/HKUDS/nanobot/issues/4222) | Brand new, but if caching is important to the project's performance story, this needs early attention |

**Notable:** The channel dispatch durability PR (#4094) and chat sender identity (#4033) both from `hamb1y` have been open for over a week with no maintainer comments, which could discourage first-time or infrequent contributors. The MCP SSRF guard (#4123) from `yu-xin-c` — who has multiple security-related PRs — is similarly awaiting review. These form the core of the emerging review bottleneck.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Here is the Hermes Agent project digest for 2026-06-07.

---

## Hermes Agent Project Digest: 2026-06-07

### 1. Today's Overview
Project activity is extremely high today, with a significant spike in both issue reporting and pull request submission. Approximately 50 issues and 50 PRs were updated in the last 24 hours, suggesting a large wave of community testing and development following a recent major update. The majority of activity is focused on bug fixes and stability patches, with a notable number of PRs targeting configuration, Desktop application, and gateway concerns. There are no new formal releases to review, but the volume of incoming fixes indicates a busy period of stabilization.

### 2. Releases
**No new releases were published in the last 24 hours.** The project digest date (2026-06-07) shows no new version tags or release artifacts. All observed activity is targeting the `main` branch and is likely destined for a future patch release.

### 3. Project Progress
In the last 24 hours, 11 PRs were merged or closed. Key advances include:
- **Documentation Clarity:** PRs #35565 (aligned Google Workspace setup flags), #40774 (clarified Signal tool-progress support), and #40912 (clarified Kanban orchestrator vs. decomposer roles) were merged, improving user onboarding.
- **Bug Fixes:** A critical fix in PR #40866 (`fix(session): honor --source flag`) was merged, enabling proper third-party integration tagging. The fix for the high-severity QQ Bot CPU spin (PR linked to #31193) was also closed.

### 4. Community Hot Topics
The most active discussion revolves around feature requests and high-impact bugs:

- **[Feature Request]: Deterministic Workflow Engine (#5354, 8 comments, 8 👍):** This is the most popular open issue. The community is asking for a "Lobster-style" engine to handle repetitive, mission-critical tasks without re-planning via an LLM. This suggests a strong desire for a "rules engine" or scheduled task mode to reduce latency and cost.
- **[Bug]: macOS DMG arm64-only (#37505, 6 comments):** A significant compatibility issue where the official Desktop DMG fails on Intel Macs. This is a high-friction point for users on older hardware.
- **[Bug]: Background Process Notifications Not Delivering (#6718, 3 comments):** A persistent reliability issue where the agent fails to get notified about completed background tasks or cron jobs, impacting autonomous operation.
- **[Feature]: Agent Activity API & Emotional State Exposure (#13529, 1 comment):** While less active, this request for a structured API to query the agent's state (what it's doing, its "emotions") shows a desire for deeper integration with external systems like Home Assistant.

### 5. Bugs & Stability
A significant number of stability and regression bugs were reported today. Severity ranking based on peer labeling and impact:

- **Critical (P1):**
    - **macOS Gateway Launchd Domain Breakage (#40831):** A regression from a recent PR hardcodes the wrong launchd domain (`user/<uid>` vs `gui/<uid>`), breaking the gateway on standard macOS setups. A fix PR (#40878) was opened immediately.
- **High (P2):**
    - **Hermes fails with Gemma4 / Ollama (#39281):** The model hits max output tokens and stops responding, suggesting a configuration or model interaction bug.
    - **CLI Input Lockup on Lazy Deps (#40490, closed):** A critical UX failure where the terminal becomes completely unresponsive when installing missing dependencies. Already fixed.
    - **DingTalk Proactive Messaging Failure (#40818):** Cron and cross-platform message send fail, severely limiting the adapter's utility.
    - **Approval Timeout Bypasses Security (#40877):** A high-severity behavioral bug; if a user doesn't approve an action in time, the LLM interprets it as a system failure and tries again, potentially bypassing the intended security denial.
- **Medium (P3):**
    - **Terminal Escape Sequences Truncating Output (#40250)**
    - **Camofox Hardcoded 30s Timeout (#40843, fix PR #40886)**
    - **Desktop Installer Fails on Paths with Spaces (#40820)**
    - **Dashboard Ignores Plugin Auxiliary Model Slots (#40880)**

### 6. Feature Requests & Roadmap Signals
Beyond the popular "Deterministic Workflow Engine" (#5354), several new feature requests signal potential roadmap items:

- **Native Audio Passthrough (#40873):** Users want to bypass Hermes's TTS/Voice pipeline and send raw audio to models like Gemma4 that support native audio input. This is a strong signal for supporting multimodal-first models.
- **Injection of Current Wall Clock Time (#40881):** While a small fix, a PR was opened to inject the current time on every API turn. This addresses a classic "temporal awareness" drift issue in long-running agent sessions.
- **Cursor Provider Integration (#40876):** A user submitted a PR to integrate Cursor's Agent API as a first-class provider. This is interesting as it suggests users want to run Hermes logic using Cursor's hosted and specialized models.
- **File Tree Deletion in Desktop (#40484):** A simple but high-utility UX request for basic file management within the Desktop app.

### 7. User Feedback Summary
Real user pain points highlighted today include:
- **Frustration with Installation & Configuration:** Intel Mac users are locked out (#37505), users on drives with spaces can't install (#40820), and the CLI setup is corrupted by raw escape sequences on Windows (#40840, fix PR #40887).
- **Reliability Concerns:** Background tasks and cron jobs silently fail to notify the agent (#6718), and the gateway has persistent WebSocket/launchd issues on macOS (#38412, #40831).
- **Confusing UX:** The Telegram chat "jumps" during agent processing (#40885), and the send button in Desktop isn't visible until a space is typed (#39436).
- **High Demand for Cost-Effective Automation:** The high vote count on the Deterministic Workflow Engine suggests satisfaction with the agent’s reasoning capabilities, but dissatisfaction with its cost and verbosity for simple, repeated tasks.

### 8. Backlog Watch
Several important issues remain open without a clear resolution path or maintainer response:

- **[Feature] Agent Activity API & Emotional State Exposure (#13529, last updated 2026-04-21):** This request has been open for over a month with no maintainer activity. It represents a significant feature gap for power users integrating Hermes with home automation.
- **[Bug] SSRF Blocking Web Tools in NVIDIA OpenShell (#32217, last updated 2026-05-25):** A blocking issue for users running Hermes in secure sandboxes. This is a tricky networking problem but causes a complete failure of web tools.
- **[Bug] Concurrent Checkpoint Preflight Side Effects (#34827, closed but complex):** While closed, this bug revealed a dangerous race condition in the tool executor. The community should watch for regressions related to concurrent tool operations.
- **[Bug] Desktop Dashboard ASAR Path Issue (#39472, last updated 2026-06-05):** A critical frontend failure on macOS where the dashboard is not served. This appears to be a post-update issue with no fix merged yet.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the project digest for PicoClaw, based on the provided GitHub data for 2026-06-07.

---

## PicoClaw Project Digest
**Date:** 2026-06-07
**Source Data:** github.com/sipeed/picoclaw

### 1. Today's Overview
PicoClaw is experiencing a **high-velocity development cycle**, with 18 PRs and 12 Issues updated in the last 24 hours. While a new nightly build was released, the most significant activity is a **coordinated push of nine new Issues by user `jcafeitosa`** targeting the creation of a financial exchange infrastructure (`ClawTrade`), including a CLI, CI/CD pipeline, and specific Binance connectors. Concurrently, contributor `chengzhichao-xydt` is driving a **major stability sweep**, submitting a series of defensive code fixes across multiple channels (LINE, Slack, WhatsApp) and internal components to resolve potential panics, goroutine leaks, and silent failures. Overall project health appears strong, featuring a mix of ambitious new feature development and necessary robustness improvements.

### 2. Releases
**`nightly` (v0.2.9-nightly.20260607.7d2b0c2a)**
- **Description:** Automated nightly build, may be unstable.
- **Changelog:** [Compare v0.2.9...main](https://github.com/sipeed/picoclaw/compare/v0.2.9...main)
- **Analysis:** No stable version was released today. Users relying on stable builds should remain on v0.2.9. The nightly includes all changes merged up to this point, including extensive bug fixes from today’s activity.

### 3. Project Progress
Today was a **major cleanup and stabilization day**, with 15 PRs being merged or closed. Key advancements include:
- **Stability & Reliability (Merged):** Contributor `chengzhichao-xydt` merged a series of critical fixes:
    - **Goroutine Leak Fix:** [PR #3014](https://github.com/sipeed/picoclaw/pull/3014) & [PR #3016](https://github.com/sipeed/picoclaw/pull/3016) Fixed goroutine leaks in `Manager.Reload()` by properly cancelling old dispatch tasks.
    - **Nil Pointer Guards:** [PR #3021](https://github.com/sipeed/picoclaw/pull/3021) & [PR #3016](https://github.com/sipeed/picoclaw/pull/3016) Added nil checks for agent access to prevent panics.
    - **Type Assertion Safety:** [PR #3022](https://github.com/sipeed/picoclaw/pull/3022), [PR #3019](https://github.com/sipeed/picoclaw/pull/3019) Added `ok` checks for `sync.Map` and type-switch captures to prevent panics.
    - **Error Handling:** [PR #3023](https://github.com/sipeed/picoclaw/pull/3023) & [PR #3017](https://github.com/sipeed/picoclaw/pull/3017) Fixed silent failures by checking `Close()` and `io.Copy` errors in updater and media encoding functions.
- **Channel & Provider Support:**
    - **Google Chat:** [PR #830](https://github.com/sipeed/picoclaw/pull/830) merged, adding official Google Chat channel support.
    - **DeepSeek Protocol:** [PR #1112](https://github.com/sipeed/picoclaw/pull/1112) merged, fixing a protocol detection issue to allow deepseek models via modelscope.cn.
    - **WhatsApp Builds:** [Issue #2625](https://github.com/sipeed/picoclaw/pull/2625) was closed, indicating the requested enhancement to include WhatsApp support in default builds was resolved.
- **Agent & Tooling:**
    - **Tool Policy Filters:** [PR #2838](https://github.com/sipeed/picoclaw/pull/2838) merged, allowing `AGENT.md` frontmatter to include `allow`/`deny` policies for tool and MCP server access.
    - **Multi-Agent Framework:** [PR #423](https://github.com/sipeed/picoclaw/pull/423) (a WIP) was closed, establishing a base for a multi-agent collaboration framework with shared context.
- **Documentation:** [PR #2662](https://github.com/sipeed/picoclaw/pull/2662) & [PR #3013](https://github.com/sipeed/picoclaw/pull/3013) improved provider documentation and removed references to missing scripts.

### 4. Community Hot Topics
The most active discussion today centered on **expanding PicoClaw's integration and communication capabilities**:
- **WhatsApp Support in Default Builds:** [Issue #2625](https://github.com/sipeed/picoclaw/pull/2625) (8 comments, 1 👍) was a high-interest feature request from a user on a Raspberry Pi Zero 2 who struggled to compile WhatsApp support manually. Its closure indicates the team has addressed this pain point.
- **Agent-to-Agent Communication:** [Issue #2929](https://github.com/sipeed/picoclaw/pull/2929) (3 comments, 2 👍) requested first-class peer-to-peer communication for agents, moving beyond the current `spawn`/`delegate` model. This reflects a strong user desire for more sophisticated, cooperative multi-agent workflows.

### 5. Bugs & Stability
Today’s activity focused heavily on identifying and resolving latent bugs. One new, user-reported bug was filed:
- **High Severity (New Bug, Fix in Progress):** **QQ Channel Connection Failure on Windows** [Issue #3015](https://github.com/sipeed/picoclaw/pull/3015). Users on Windows are unable to start the QQ gateway due to a token retrieval timeout. This is a blocking issue for QQ users on Windows.
- **High Severity (Fixed):** Multiple patches from `chengzhichao-xydt` fixed potential **panics** (nil agent, nil type assertions), **goroutine leaks** (on reload), and **data corruption** (silent write failures). These were systemic issues found via code audit, not user reports.
- **Medium Severity (Fixed):** **Workspace URL Validation** [PR #2965](https://github.com/sipeed/picoclaw/pull/2965) fixed a bug where the workspace guard incorrectly blocked `/`-less URLs in `curl` commands.
- **Low Severity (Fixed):** **Frontend Copy Button** [PR #2711](https://github.com/sipeed/picoclaw/pull/2711) fixed a clipboard API error in HTTP environments.

### 6. Feature Requests & Roadmap Signals
The most significant signal for the project's future direction is the **large batch of Issues filed by `jcafeitosa`** around the `ClawTrade` subsystem. These issues (e.g., [EX-001](https://github.com/sipeed/picoclaw/pull/3024), [EX-002](https://github.com/sipeed/picoclaw/pull/3025), [RG-001](https://github.com/sipeed/picoclaw/pull/3029)) define a **crypto/financial exchange interface** with extremely high-performance requirements (e.g., 1M updates/s lock-free order book, <50μs WebSocket latency). This suggests PicoClaw is pivoting or expanding to become an AI agent framework for algorithmic trading and financial analysis.

**Likely Next Version Features:**
- A complete `ClawTrade` module with Binance support.
- The new Slack channel filtering/formatting features from [PR #3020](https://github.com/sipeed/picoclaw/pull/3020).
- i18n support for Traditional Chinese (`zh-TW`) from [PR #2935](https://github.com/sipeed/picoclaw/pull/2935).

### 7. User Feedback Summary
- **Pain Point (Resolved):** A user on a Raspberry Pi Zero 2 ([Issue #2625](https://github.com/sipeed/picoclaw/pull/2625)) expressed frustration at the lack of pre-compiled builds with WhatsApp support, making updates difficult. This was a clear request for better platform/feature support in official binaries.
- **Use Case:** Users are deploying PicoClaw on low-power edge hardware (e.g., Raspberry Pi) and require integrations with popular consumer messaging apps like WhatsApp.
- **New Complexity:** The wave of `ClawTrade` issues suggests an emerging user/developer base interested in applying AI agents to high-frequency financial data, moving beyond simple chat agents.

### 8. Backlog Watch
- **Stale Documentation PR:** The **Traditional Chinese (zh-TW) locale** PR [#2935](https://github.com/sipeed/picoclaw/pull/2935) has been open since May 24 (14 days). It is flagged as `[stale]` and has received no comments from maintainers. This documentation addition could improve accessibility for a significant user base.
- **Stale Feature Request (Closed):** The **agent-to-agent communication** request [#2929](https://github.com/sipeed/picoclaw/pull/2929) and the **tool policy filters** PR [#2838](https://github.com/sipeed/picoclaw/pull/2838) were both marked `[stale]` before being closed, indicating that while the multi-agent framework from PR #423 was merged, the specific peer-to-peer communication layer has been deprioritized or addressed in a different form.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-06-07

## Today's Overview
NanoClaw saw moderate activity today with **14 pull requests** updated and **2 new issues** opened. The project remains in a healthy maintenance-and-evolution phase: three PRs were merged/closed, all targeting conformance and stability improvements across the skill library, host runtime, and dashboard integration. The **Skills Conformance initiative** (PR #2698) was a major theme, signaling a push toward upgrade-maintainable skill structures. Two open issues surfaced real-user friction in the setup experience and CLI rebuild logic, both with actionable root causes. No new releases were cut today.

## Releases
**No new releases** were published today.

## Project Progress
Three pull requests were merged or closed today, all advancing the project's structural health:

- **[PR #2698 — Skills conformance: exemplars + fleet retrofit](https://github.com/nanocoai/nanoclaw/pull/2698)** (closed) — Retrofitted the entire skill library to be *upgrade-maintainable*: every skill now conforms to the skills model with minimal additive reach-ins, a test for each integration point, an idempotent `REMOVE.md`, and no `VERIFY.md`. Skills that could not conform were retired or rewritten. This is the foundational work for ensuring skills survive core codebase refactors.

- **[PR #2696 — feat(add-dashboard): make the skill conformant (drift fix + shipped test)](https://github.com/nanocoai/nanoclaw/pull/2696)** (closed) — First exemplar of the new upgradeability model. The dashboard skill had silent drift: five DB module imports had moved during a core reorganization. Fixed the imports, added an in-process-seam integration test, and made the skill the model for all future retrofits.

- **[PR #2697 — feat(host): single-instance lock to prevent duplicate messages](https://github.com/nanocoai/nanoclaw/pull/2697)** (closed) — Fixed a real-user problem where running two host processes (e.g., dev + installed service) caused duplicate message deliveries, as each host independently spawned containers for the same due message. Added a system-level lock file to enforce single-instance execution.

## Community Hot Topics
- **[Issue #2703 — Recommended setup path leaves CLI unwired, `pnpm run chat hi` hangs for 120s](https://github.com/nanocoai/nanoclaw/issues/2703)** — Opened by `bigintersmind`, zero comments but high potential impact. A fresh install following the recommended path advertises `pnpm run chat hi` in the "Try these" panel, but the CLI/local channel isn't wired. The command hangs for two minutes before timing out with no diagnostic hint. **Underlying need:** The setup flow should either wire the CLI channel automatically or suppress commands that depend on unconfigured channels. This is a UX regression for new users.

- **[Issue #2701 — `ncl groups restart --rebuild` fails with misleading error when no packages configured](https://github.com/nanocoai/nanoclaw/issues/2701)** — Opened by `jtheducation-ctrl`. The rebuild command unconditionally requires package installation, failing with "No packages to install" when both `packages_apt` and `packages_npm` are empty. A normal restart succeeds. **Underlying need:** Rebuild should skip package installation gracefully when no packages are defined, not force users to install empty package lists.

- **[PR #2531 — fix(poll-loop): suppress duplicate text when send_message fires mid-turn](https://github.com/nanocoai/nanoclaw/pull/2531)** — Open since May 18, this 19-day-old PR continues to get updates. It addresses a subtle timing issue where user messages could appear duplicated during active conversation turns. The persistence of this PR suggests the fix requires careful coordination with other poll-loop changes.

## Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **High** | [#2703 — Setup path leaves CLI unwired, `pnpm run chat hi` hangs 120s](https://github.com/nanocoai/nanoclaw/issues/2703) | Open | Blocks new-user onboarding entirely. No comments or fix PR yet. |
| **Medium** | [#2701 — `ncl groups restart --rebuild` fails with misleading error](https://github.com/nanocoai/nanoclaw/issues/2701) | Open | Breaks a documented workflow; easy to fix by skipping empty package lists. |
| **Medium** | [PR #2695 — Signal adapter can't read inbound image attachments](https://github.com/nanocoai/nanoclaw/pull/2695) | Open, fix PR | Images sent via Signal are unreachable inside the container because the attachment path isn't mounted. Fix stages them as base64. |
| **Medium** | [PR #2694 — Signal adapter drops inbound DMs silently](https://github.com/nanocoai/nanoclaw/pull/2694) | Open, fix PR | Missing `isMention`/`isGroup` flags on inbound Signal DMs causes the router to drop them entirely. Fix adds proper flagging. |
| **Low** | [PR #2699 — CLI generates non-letter-leading IDs for CRUD create](https://github.com/nanocoai/nanoclaw/pull/2699) | Open, fix PR | `ncl groups create` uses `crypto.randomUUID()`, which can produce IDs starting with a digit. OneCLI rejects these; fix forces letter-leading IDs. |
| **Low** | [PR #2531 — Duplicate text when send_message fires mid-turn](https://github.com/nanocoai/nanoclaw/pull/2531) | Open, fix PR | Long-standing (19 days) poll-loop timing issue causing duplicate message text. |

## Feature Requests & Roadmap Signals
- **[PR #2693 — Add Google Contacts tool (MCP server)](https://github.com/nanocoai/nanoclaw/pull/2693)** — A new utility skill adding `/add-google-contacts-tool`, completing the Google office suite integration alongside Gmail and Google Calendar. Uses a bundled stdio MCP server. Likely to land in the next minor release as it's a clean, additive skill.

- **[PR #2208 — Support HTTP and SSE MCP server transports](https://github.com/nanocoai/nanoclaw/pull/2208)** — Open since May 3, this feature adds support for remote MCP servers beyond the current stdio transport. Still active with recent updates. If merged, it would significantly expand the ecosystem of tools agents can use.

- **[PR #2700 — /add-slack skill: switch to Socket Mode setup](https://github.com/nanocoai/nanoclaw/pull/2700)** — Fixes the Slack onboarding skill to use Socket Mode instead of HTTP webhooks, removing the need for a publicly reachable URL. This is a UX improvement for self-hosted users behind NAT/firewalls.

## User Feedback Summary
- **Pain point — Setup confusion:** The recommended setup path is broken for CLI-based usage (Issue #2703). Users following instructions verbatim hit a 2-minute timeout with no error explanation. This is the highest-priority UX issue open.

- **Pain point — Signal channel incomplete:** Two Signal adapter bugs (PR #2695, PR #2694) mean image attachments are invisible and private messages are silently dropped. For Signal users, the channel is effectively broken for anything beyond basic group text.

- **Pain point — Duplicate messages:** The single-instance lock fix (PR #2697, merged) suggests users running both development and production instances were experiencing duplicate message delivery, a confusing and disruptive bug.

- **Satisfaction signal — Skill retrofitting welcomed:** The closure of PR #2698 (Skills Conformance) with three exemplar PRs demonstrates the maintainers are investing in structural quality, which users of the skill library have requested for months (as seen in prior issue comments about skill drift).

## Backlog Watch
- **[PR #2230 — fix(container-runner): map host user via keep-id on rootless podman](https://github.com/nanocoai/nanoclaw/pull/2230)** — Open since May 3 (35 days). This PR addresses container permission issues for rootless Podman users, a growing deployment model. No maintainer comments visible. Important for containerization stability.

- **[PR #2349 — fix(mount-security): tolerate allowlist entries missing path field](https://github.com/nanocoai/nanoclaw/pull/2349)** — Open since May 8 (30 days). A security hardening fix that makes mount allowlists more robust against malformed entries. Still actively updated as of today, but no merge signal.

- **[PR #2184 — fix(poll-loop): retry immediately on stale session instead of delivering error](https://github.com/nanocoai/nanoclaw/pull/2184)** — Open since May 2 (36 days). Fixes a user-visible bug where stale Claude Code sessions caused raw errors in chat. Recently updated (June 6) with new commits, suggesting it's near completion.

- **No issues or PRs flagged for maintainer attention** on the current data; all open items have active authors or recent activity.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-06-07

## Today's Overview
Project activity is high, with 31 PRs updated in the last 24 hours, 10 of which were merged or closed. The core team is driving **Reborn** architecture forward across multiple lanes (Notion MCP, WebUI sessions, OpenAI compatibility, Slack channel routing), while performing critical CI and stability work. The CI pipeline is actively being reorganized to isolate Reborn-only changes from legacy tests. A nightly E2E failure (Issue #4108, open since May 27) remains a known stability concern. No new releases were published today.

## Releases
No new releases were published in the last 24 hours. The pending release PR (#3708, opened May 16) contains breaking API changes for `ironclaw_common` (0.4.2 → 0.5.0) and `ironclaw_skills` (0.3.0 → 0.4.0), as well as a major version bump for the main `ironclaw` crate (0.24.0 → 0.29.1). This release has accumulated several weeks of CI review and may merge soon.

## Project Progress
**10 PRs merged/closed today** across several workstreams:

- **Reborn Architecture & Design** — Two design docs were merged: `docs/reborn/2026-06-04-subagent-compaction-design.md` (PRs #4486, #4485), defining the unified subagent/compaction/post-capability-stage model.
- **Developer Experience & CI** — PR #4520 closed, reclassifying Reborn-only tests to skip legacy test partitions, improving CI speed and accuracy.
- **Safety & Stability** — PR #4508 closed, converting repeated capability-call signatures from immediate stops into a two-stage warning gate with persisted state and loop-control signals.
- **Slack Channel Integration** — PR #4509 closed, adding product workflow subject routing for Slack channel IDs, with DM fallback and shared subject support.
- **AI Agent Integrity** — PR #4467 (not in top 20 but part of the 31) likely advanced host API safety corrections.

## Community Hot Topics
1. **PR #3708 — Release Preparation (Open since May 16)**  
   [Link](https://github.com/nearai/ironclaw/pull/3708)  
   Despite zero comments, this is the longest-pending open PR and contains breaking changes across core crates. The silence likely indicates internal coordination, not neglect—this affects every downstream consumer.

2. **PR #4511 — Outbound Preference Facade Contracts (XL, open, core contributor)**  
   [Link](https://github.com/nearai/ironclaw/pull/4511)  
   Large-scale architectural change adding delivery preference contracts to `ironclaw_product_workflow`. Signals deepening Reborn product workflow infrastructure.

3. **PR #4186 — Local-Dev Approval Gates (XL, open, core contributor)**  
   [Link](https://github.com/nearai/ironclaw/pull/4186)  
   Core contributor PR converting effectful capability calls into approval gates. Represents hardening for safe development workflows, likely targeted for next release.

## Bugs & Stability
- **Issue #4108 — Nightly E2E Failure (Open since May 27, severe)**  
  [Link](https://github.com/nearai/ironclaw/issues/4108)  
  ❗ Critical: Nightly E2E scheduled run failing, specifically the `Full E2E / E2E (extensions)` job. No fix PR exists yet. This blocks confidence in automated testing of the extensions subsystem.
  
- **PR #4523 — System Sentinel Deserialization Fix (Open, low risk, regular contributor)**  
  [Link](https://github.com/nearai/ironclaw/pull/4523)  
  Fixes a silent rejection of `\x1fSYSTEM\x1f` sentinel in `TenantId`/`UserId` deserialization, which was causing `service_unavailable` errors on LLM settings endpoints. Moderate severity for production systems—this fix is ready for review.

- **PR #3981 — Runtime HTTP Redaction Tests (Open since May 24, new contributor)**  
  [Link](https://github.com/nearai/ironclaw/pull/3981)  
  Adds test coverage for sensitive-header redaction markers. No fix needed, but the long open time suggests maintainer review bandwidth is tight.

## Feature Requests & Roadmap Signals
- **Notion MCP Integration** — Issue #3805 (closed) requested implementing Notion MCP capability discovery. This aligns with the Reborn lane 5 roadmap for first concrete MCP tool packaging.
- **OpenAI-Compatible Chat Completions** — PRs #4489 and #4495 (both open, core contributors) add `chatcmpl-*` refs and route non-streaming `POST /v1/chat/completions` through ProductWorkflow. These are strong signals for an upcoming OpenAI-compatible API layer in Reborn.
- **WebUI Session Capabilities** — PR #4519 (open) adds `GET /api/webchat/v2/session` endpoint with admin detection. Points toward richer WebUI permissions management.
- **Thread Deletion in WebChat v2** — PR #4516 (open, L size) adds DELETE thread route with scope-based authorization. Indicates maturity of the WebChat feature set.

**Prediction for next release:** Expect OpenAI-compatible endpoints, Slack channel routing, and Reborn config seeding (PR #4517) to land together, possibly in the long-pending release PR #3708.

## User Feedback Summary
No direct user issues were filed in the last 24 hours. However, the E2E test failure (Issue #4108) and the sentinel deserialization fix (PR #4523) both point to real operational pain points: unreliable CI signals and silent failures in LLM settings endpoints. The repeated-call warning gate (PR #4508) suggests internal feedback that loop-control was too aggressive for legitimate multi-step capabilities.

## Backlog Watch
- **PR #3981 — Runtime HTTP Redaction Tests**  
  [Link](https://github.com/nearai/ironclaw/pull/3981)  
  Open since May 24 from a **new contributor**. This PR adds security-relevant test coverage with zero links to issues. It has not received maintainer review or comments in 14 days. **Risk:** New contributor may lose engagement without acknowledgment.
  
- **PR #4002 — CI Dependency Bump (dependabot)**  
  [Link](https://github.com/nearai/ironclaw/pull/4002)  
  Open since May 24 with 16 dependency updates (including `actions/checkout` 4→6). While low risk, stale CI dependency PRs can cause cascading version conflicts.

- **Issue #4108 — Nightly E2E Failure (Open since May 27)**  
  [Link](https://github.com/nearai/ironclaw/issues/4108)  
  No fix PR exists. Without resolution, confidence in E2E test reliability continues to erode, risking regressions in extensions and integration workflows.

---

*Report generated from GitHub data for nearai/ironclaw, 2026-06-07.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for **2026-06-07**, generated from the provided GitHub data.

---

## LobsterAI Project Digest: 2026-06-07

### 1. Today's Overview

The project shows low activity today, with no new releases or code merges in the last 24 hours. While two pull requests were closed, they were both from April and appear to have been stale; no new code is being actively integrated. The primary signal comes from the issue tracker, where 6 open issues were updated, indicating ongoing user engagement but a maintenance bottleneck. The project appears to be in a stabilization phase with a significant backlog of 2+ month-old bugs receiving attention again.

### 2. Releases

No new releases were published today.

### 3. Project Progress

Two pull requests were closed today, both marked as stale:

- **#1529 [CLOSED] - feat(cowork): Batch export sessions to JSON**
  - *Author:* MaoQianTu
  - *Summary:* Added an export button to batch mode, allowing users to export selected cowork sessions into a structured JSON file (includes session ID, title, agent, messages, etc.). This feature addresses user needs for data portability.
  - *Link:* [PR #1529](https://github.com/netease-youdao/LobsterAI/pull/1529)

- **#1530 [CLOSED] - feat(scheduledTask): Agent selector for new tasks**
  - *Author:* gongzhi-netease
  - *Summary:* When multiple agents are enabled, users can now select which agent a new scheduled task belongs to during creation. Previously, all tasks defaulted to the main agent, causing confusion. The new selector appears next to the model picker.
  - *Link:* [PR #1530](https://github.com/netease-youdao/LobsterAI/pull/1530)

**Note:** Both PRs were created on 2026-04-07 and closed today. Their closure likely represents a backlog cleanup rather than a recent development push.

### 4. Community Hot Topics

Only one issue received a comment today, reflecting low immediate community engagement.

- **Most Active Issue:** **#2120 - "建议" (Suggestion)**
  - *Comments:* 1
  - *Author:* nbjoe
  - *Summary:* This is the only issue created today (not stale). The user proposes three features: (1) a task pre-input queue (inspired by WorkBuddy) to improve workflow continuity, (2) extending single-task runtime to prevent premature termination during long scripts, and (3) adjusting the skill UI from a dual-column layout to a triple-column layout for better use of widescreen monitors (2560x1600).
  - *Link:* [Issue #2120](https://github.com/netease-youdao/LobsterAI/issues/2120)

This issue represents a power user advocating for productivity improvements and UI polish.

### 5. Bugs & Stability

No new bugs were filed today. However, four stale bugs (all from April) received activity (likely automated stale-bot pings or minor updates), indicating they remain unresolved and potentially affect users.

- **High Severity - Task Completion Failure**
  - **#1496:** Task shows as "completed" but returns no results. User reports a visual discrepancy between UI state and actual output.
  - *Link:* [Issue #1496](https://github.com/netease-youdao/LobsterAI/issues/1496)

- **Medium Severity - Process Interruption**
  - **#1495:** User reports persistent, unexplained process interruptions ("无缘无故中断进程"). Unsure if the issue is client-side or model-side. This is the only bug receiving a positive reaction (1 👍).
  - *Link:* [Issue #1495](https://github.com/netease-youdao/LobsterAI/issues/1495)

- **Low Severity - UI State Loss (3 related issues)**
  - **#1468, #1469, #1470:** A series of UX bugs where closing modals (Agent creation, Agent settings, MCP server config) without saving results in silent data loss. No confirmation dialog is shown.
  - *Links:* [#1468](https://github.com/netease-youdao/LobsterAI/issues/1468), [#1469](https://github.com/netease-youdao/LobsterAI/issues/1469), [#1470](https://github.com/netease-youdao/LobsterAI/issues/1470)

**No fix PRs exist for any of these bugs.**

### 6. Feature Requests & Roadmap Signals

The most actionable feature request comes from **Issue #2120**, which contains three clear signals:

1.  **Task Queue System:** User wants to pre-input a next task while the current one is running, inspired by WorkBuddy. This implies a desire for batch/queue-based execution rather than manual one-by-one triggering.
2.  **Configurable Task Timeout:** The user ran a long data-script that was terminated by Claw (monitoring tool). A user-configurable timeout or an "unlimited" mode for long-running tasks is requested.
3.  **UI Responsiveness:** The skill interface (dual columns) is not optimal on high-resolution widescreen displays. A responsive grid (e.g., 3 columns) is requested.

**Prediction:** The task queue feature is a strong candidate for the next minor release, as it improves usability without breaking existing workflows. UI layout changes are low-risk and likely to be picked up quickly.

### 7. User Feedback Summary

- **Pain Points (Stability):** Two users report task interruption issues (#1495, #2120). One user saw tasks "completing" with no output (#1496). These are the highest-impact negative experiences.
- **Pain Points (UX):** A single user (MaoQianTu) filed three separate, detailed bugs about silent data loss in modals (#1468, #1469, #1470). This represents a mature, testing-oriented user who values data integrity.
- **Satisfaction Indicators:** The project has sufficient active users to file detailed feature requests and bug reports, indicating a dedicated user base. However, the lack of resolution on stale issues suggests a risk of user churn.

### 8. Backlog Watch

The following stale issues (unchanged since April) have been updated today but remain unanswered by maintainers. They represent the most critical maintenance debt:

- **#1496:** Task completion failure (2 months old) – *No response from maintainers.*
- **#1495:** Unexplained process interruption (2 months old) – *No response from maintainers.*
- **#1468, #1469, #1470:** Modal state loss bugs (2 months old) – *No response from maintainers.*

**Warning:** These bugs are now 60+ days old with zero comments from the LobsterAI team. The closure of stale PRs today suggests the team is cleaning up, but these issues remain unaddressed. Maintainer attention is urgently needed.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest – 2026-06-07

## Today's Overview
Activity on the Moltis GitHub has been **low** over the past 24 hours. No new releases or pull requests were recorded, and the three open issues remain unmerged and are all from yesterday (2026-06-06). The lack of any closed issues or merged PRs suggests maintainer focus may be elsewhere or that the project is in a quiet period following recent updates. Two of the three open reports are bugs, and one is a feature request, indicating ongoing user friction but no active resolution today.

## Releases
**None.** No new releases were published in the last 24 hours.

## Project Progress
No pull requests were merged or closed in the last 24 hours. No features or fixes advanced through the PR pipeline during this period.

## Community Hot Topics
The most active issue by comments is **Issue #1112** ([moltis-org/moltis Issue #1112](https://github.com/moltis-org/moltis/issues/1112)) with 1 comment, reported by methompson. The bug describes that disabling authentication in the Docker setup does not actually disable auth, which likely blocks non-expert users from debugging or deploying quickly. The other two issues have zero comments each, suggesting the community has not yet engaged deeply with the cron-related reports. Underlying needs appear to center on **configuration reliability** and **notification management**.

## Bugs & Stability
Two bugs were reported today, both open with no associated fix PRs:

- **Issue #1112** (Severity: High) — *[Bug]: Disabling auth doesn't seem to disable auth (Docker)*  
  User methompson reports that setting auth to disabled has no effect in Docker deployments. This is a potential security/configuration blocker.  
  [GitHub Link](https://github.com/moltis-org/moltis/issues/1112)

- **Issue #1111** (Severity: Medium) — *[Bug]: Archiving a cron session has no visible effect*  
  User IlyaBizyaev reports that archiving cron sessions does not produce any visible outcome, suggesting a UI/logic gap.  
  [GitHub Link](https://github.com/moltis-org/moltis/issues/1111)

No fix PRs have been opened for either bug as of this digest.

## Feature Requests & Roadmap Signals
One feature request was filed today:

- **Issue #1110** — *[Feature]: A keyword to suppress cron job notifications, like NO_REPLY*  
  User IlyaBizyaev requests the ability to silence notifications for cron jobs (similar to a `NO_REPLY` keyword). This is a **quality-of-life enhancement** that would likely appeal to automated/headless deployments. Given its simplicity and clear use case, it could be targeted for the next minor release (if maintainers adopt a fast-track for small features).  
  [GitHub Link](https://github.com/moltis-org/moltis/issues/1110)

## User Feedback Summary
Real user pain points visible today include:
- **Authentication configuration is unreliable** (Issue #1112) — users cannot trust the disabling of auth.
- **Cron session management is confusing** (Issue #1111) — archiving does nothing, which may undermine trust in session lifecycle features.
- **Cron notification noise** (Issue #1110) — users want finer control over alert frequency, indicating Moltis is being used in automated pipelines where silent execution is expected.

Overall sentiment is **mildly dissatisfied** due to unresolved configuration and UI bugs.

## Backlog Watch
No issues or PRs were identified as long-unanswered in this window. All three items were opened yesterday (2026-06-06) and have not yet received maintainer response. The lack of any older unanswered issues suggests the backlog is currently well-managed, but quick triage on the two bugs (Issue #1112 and #1111) would prevent them from becoming stale.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Here is the project digest for **CoPaw** based on data from **2026-06-07**.

---

## CoPaw Project Digest – 2026-06-07

### 1. Today's Overview
The CoPaw project is currently in a **high-activity bug-fixing phase** following the release of v1.1.10. There were **11 Issues updated in the last 24 hours** (9 open, 2 closed) and **zero Pull Requests**, indicating a bottleneck in merge activity or a focus on triage rather than code landing. User reports indicate significant regressions in **Coding Mode, Windows file system handling, and local model connectivity** between versions 1.1.9 and 1.1.10. No new releases were published today, suggesting the team is likely consolidating a patch release. The spike in high-severity bugs (especially No. 4987, 4988, 4989) signals a need for immediate stabilization efforts.

### 2. Releases
**None.** No new releases were published today. The latest available version remains **v1.1.10**.

### 3. Project Progress
**Merged/Closed PRs today:** 0. No PRs were updated in the last 24 hours.
- **Two Issues were closed today:** Issue [#4661 (Bug: memory compression not working)](https://github.com/agentscope-ai/QwenPaw/issues/4661) was resolved, and Issue [#4984 (Housekeeper: approval command works)](https://github.com/agentscope-ai/QwenPaw/issues/4984) was closed as "not a bug."
- **No feature advances or fixes landed via PRs today.**

### 4. Community Hot Topics
The following Issues generated the most discussion and reactions:

- **[#4937 – /compact command ignores model's max_input_length](https://github.com/agentscope-ai/QwenPaw/issues/4937)** (5 comments)
  - *Analysis:* Users are frustrated that after manually configuring a 512K window for certain models (e.g., MiniMax M3), the `/compact` command reverts to a 128K default. This suggests a gap between configuration logic and the runtime environment.
- **[#4661 – v1.1.8post1 context compression regression](https://github.com/agentscope-ai/QwenPaw/issues/4661)** (6 comments, now closed)
  - *Analysis:* A related regression from the previous version. The fix for v1.1.9/1.1.10 appears to have only partially addressed the issue, as #4937 remains open.
- **[#4886 – Feature request: MAX Messenger channel](https://github.com/agentscope-ai/QwenPaw/issues/4886)** (2 comments)
  - *Analysis:* Russian-speaking users are requesting support for MAX (a dominant messenger in Russia). Signals growing international user base and demand for localization.

**Underlying need:** Users are demanding consistency between configuration (UI/API) and execution. The repeated "context compression defaults to 128K" bugs indicate a systemic caching or priority logic flaw.

### 5. Bugs & Stability
**High Severity (Ranked):**

1. **[#4989 – Local model (千问3.6-27B) hangs on v1.1.9 & 1.1.10](https://github.com/agentscope-ai/QwenPaw/issues/4989)**
   - *Impact:* Users cannot use local models at all. No error logs, no response. Works on v1.1.5.post2. **Likely a silent regression in OpenAI protocol parsing.**
2. **[#4988 – Windows MAX_PATH overflow due to duplicated session ID in filename](https://github.com/agentscope-ai/QwenPaw/issues/4988)**
   - *Impact:* Application crashes on Windows due to filename path length exceeding 260 characters. Root cause: session ID is appended twice in the filename. **Blocks Windows users entirely.**
3. **[#4987 – Session switch always fails in Coding Mode](https://github.com/agentscope-ai/QwenPaw/issues/4987)**
   - *Impact:* Fully broken UX in Coding Mode on v1.1.10 (was working on v1.1.9). Users cannot switch sessions.
4. **[#4937 – /compact ignores model's max_input_length](https://github.com/agentscope-ai/QwenPaw/issues/4937)**
   - *Impact:* Context compression logic ignores user-configured limits.

**Medium/Low Severity:**
- **[#4990 – WeChat Work error on tool invocation close](https://github.com/agentscope-ai/QwenPaw/issues/4990)** (1 comment) – Minor UX bug.
- **[#4985 – Delete file command text overflow without wrapping](https://github.com/agentscope-ai/QwenPaw/issues/4985)** (1 comment) – UI polish issue.

**No fix PRs exist for any of these bugs.**

### 6. Feature Requests & Roadmap Signals
Four feature requests (enhancements) were discussed today:

| Issue | Feature | Likelihood for Next Version |
|-------|---------|-----------------------------|
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | Session sidebar for one-click switching | **Medium** – The current "two-click" flow is a top UX complaint. |
| [#4886](https://github.com/agentscope-ai/QwenPaw/issues/4886) | MAX Messenger channel | **Low** – Requires channel integration, lower priority than stability. |
| [#4986](https://github.com/agentscope-ai/QwenPaw/issues/4986) | Real-time Shell output streaming (like Cursor) | **Medium** – Strong UX demand; would increase user trust in file/shell operations. |
| [#4985](https://github.com/agentscope-ai/QwenPaw/issues/4985) | Text wrapping in command output | **High** – Simple CSS fix, low risk. Likely in next patch. |

**Prediction:** The next release (v1.1.11) will focus heavily on stability (fixing #4987, #4988, #4989) before any new features land. #4971 might be bundled as a minor UX improvement.

### 7. User Feedback Summary
- **Pain points (high volume, high urgency):**
  - Regressions between v1.1.9/1.1.10 and v1.1.5 (local models, session switching, Windows file paths) are causing users to downgrade or block upgrades.
  - Context compression logic is opaque and fails to honor explicit configuration.
  - Lack of real-time feedback during file/shell operations creates confusion.
- **Satisfaction signals:**
  - Users are willing to write detailed bug reports (each issue has 1–5 comments with steps to reproduce).
  - Positive reaction to the `/approval approve` magic command (Issue #4984 was closed as "solved, thanks!" – clear satisfaction).
  - Growing community interest in new channel integrations (MAX).
- **Dissatisfaction triggers:**
  - "No error logs" is a recurring theme (#4989, #4990). Silent failures erode trust.
  - Windows path issue is a hard blocker for a significant portion of the user base.

### 8. Backlog Watch
Open issues needing maintainer attention (no recent maintainer comment, high impact):

| Issue | Age | Why it matters |
|-------|-----|----------------|
| [#4937](https://github.com/agentscope-ai/QwenPaw/issues/4937) | 4 days | Affects all users with models >128K context. No maintainer response yet. |
| [#4971](https://github.com/agentscope-ai/QwenPaw/issues/4971) | 2 days | Major UX improvement request. Simple session sidebar, long-standing complaint. |
| [#4886](https://github.com/agentscope-ai/QwenPaw/issues/4886) | 5 days | International user request – no maintainer response. |

**Urgent Action Item:** The three high-severity regressions (#4987, #4988, #4989) landed in the last 24 hours and have no fix PR in sight. The core team should prioritize creating hotfix branches for these before more users upgrade to v1.1.10.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

**ZeptoClaw Project Digest — 2026-06-07**

**1. Today's Overview**
The ZeptoClaw project shows moderate but focused activity over the last 24 hours, with two issues updated and one open pull request maintained. A binary-size strategy debate has reached a critical juncture: after landing PR #611 with a relaxed 7.5MB gate, maintainers are now tightening toward a true "robot moat" target of 7MB, specifically for aarch64. No new releases are in flight, signaling a consolidation phase after the recent CI infrastructure changes. Overall, project health is stable, with high-value CI hardening taking precedence over new features.

**2. Releases**
No new releases have been published. The project continues on the same version as of 2026-06-07.

**3. Project Progress**
Only one pull request remains in play:
- **#611 (Open)** — *[chore(ci): promote binary-size to PR gate at 7.5MB]* — Authored by qhkm on June 1, last updated June 6. This PR drops the `if:` guard so the binary-size job runs on every PR and lowers the gate. No PRs were merged or closed today.

**4. Community Hot Topics**
The two updated issues represent the community's primary area of concern this week:
- **#612 (Closed)** — *[chore(perf): audit ~800KB binary-size drift since 6.2MB low water mark, tighten gate to 7MB]* — With 1 comment, this closed issue documents the discussion around the current 6.98MB darwin-arm64 binary vs. the strategic 7MB ceiling. The closure indicates the audit is complete, but the gate remains at 7.5MB.
- **#629 (Open, P2-high)** — *[chore(ci): add aarch64 binary-size gate at 7MB (the actual robot moat)]* — Created June 6, this issue zeroes in on the real deployment constraint: the aarch64 binary must fit the "6MB + buffer" robot moat. This is the new focal point for the binary-size effort, likely to supersede the now-closed #612 discussion.

**5. Bugs & Stability**
No bugs, crashes, or regressions were reported in the last 24 hours. The binary-size drift identified in #612 was resolved through the audit (issue closed), and no associated bug-fix PRs were opened.

**6. Feature Requests & Roadmap Signals**
No new feature requests from users were recorded. The roadmap signal is clear: the maintainer-driven priority is to finalize the aarch64 binary-size gate at 7MB (as captured in #629). This suggests the next version will likely include a stricter CI gate for ARM targets, reflecting a production-readiness push for embedded/robot deployments.

**7. User Feedback Summary**
No user pain points, use cases, or satisfaction indicators were captured in the last 24 hours. Current activity remains internally driven by maintainers optimizing CI for deployment size constraints.

**8. Backlog Watch**
No long-unanswered issues or PRs needing maintainer attention were identified. The only open PR (#611) and open issue (#629) are actively managed by the author/maintainer (qhkm), with the most recent updates within 1 day. The backlog is effectively clear.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-06-07

## Today's Overview

The ZeroClaw project is experiencing a period of **intense development velocity**, with 50 PRs updated and 39 issues updated in the last 24 hours—indicating a highly active engineering team pushing toward multiple concurrent milestones (v0.8.0, v0.8.1, v0.8.2, v0.8.3). Today saw **5 merged/closed PRs** and **15 closed issues**, with strong focus on bug fixes across the Telegram channel, security policy, gateway, and web UI. The most significant activity cluster is the **WASM plugin ecosystem**, with multiple new plugin PRs (n8n, ACE-Step, Stable Diffusion WebUI, Nominatim, LanguageTool, Ollama Embed) landing simultaneously, suggesting a coordinated push to expand ZeroClaw's plugin library. No new releases were published today.

## Releases

**No new releases** were published today (2026-06-07). The latest public release remains v0.8.0-beta-1. The project is actively tracking toward v0.8.0 stable via tracking issue [#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112).

---

## Project Progress

**Merged/Closed PRs today (5):**

| PR | Description | Status |
|---|---|---|
| [#7334](https://github.com/zeroclaw-labs/zeroclaw/pull/7334) | fix(channels/telegram): clamp zero draft update interval (fixes #7332) | ✅ Merged |
| [#7281](https://github.com/zeroclaw-labs/zeroclaw/pull/7281) | fix(policy): stop path guard false-positives on heredoc bodies and non-path tildes (fixes #7133) | ✅ Merged |
| [#7297](https://github.com/zeroclaw-labs/zeroclaw/pull/7297) | feat(gateway): per-request agent dispatch for POST /webhook via ?agent= | ✅ Merged |
| [#7252](https://github.com/zeroclaw-labs/zeroclaw/issues/7252) | [Bug]: session/kill can rehydrate killed ACP sessions from durable history (S0 severity) | ✅ Fixed/Closed |
| [#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126) | [Bug]: Web UI "Clear all" only wipes rendered messages, not the backend session history | ✅ Fixed/Closed |

**Key features that advanced today:**
- **WASM plugin ecosystem expansion**: Six new plugin PRs landed (n8n workflow trigger [#7328](https://github.com/zeroclaw-labs/zeroclaw/pull/7328), ACE-Step music generation [#7331](https://github.com/zeroclaw-labs/zeroclaw/pull/7331), Stable Diffusion WebUI [#7325](https://github.com/zeroclaw-labs/zeroclaw/pull/7325), Nominatim geocoding [#7327](https://github.com/zeroclaw-labs/zeroclaw/pull/7327), LanguageTool grammar check [#7326](https://github.com/zeroclaw-labs/zeroclaw/pull/7326), Ollama Embed local embeddings [#7324](https://github.com/zeroclaw-labs/zeroclaw/pull/7324))
- **Plugin infrastructure hardening**: Sandbox isolation with resource limits/SSRF guard ([#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335)), namespace plugin tools + rate limiting ([#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337)), default signature_mode to permissive ([#7336](https://github.com/zeroclaw-labs/zeroclaw/pull/7336)), remote plugin registry + `zeroclaw plugin search` ([#7333](https://github.com/zeroclaw-labs/zeroclaw/pull/7333))
- **Web dashboard expansion**: MCP, Skills, Plugins & Providers dashboard tabs ([#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229)), plugin lifecycle endpoints + management UI stubs ([#7235](https://github.com/zeroclaw-labs/zeroclaw/pull/7235))
- **Tool refactoring**: Extracted duplicate domain/URL validation in browser/web tools ([#7340](https://github.com/zeroclaw-labs/zeroclaw/pull/7340))
- **Fix for plugin-bundled skills loading**: `read_skill` tool now supports plugin-bundled and bounded skills ([#7245](https://github.com/zeroclaw-labs/zeroclaw/pull/7245))

---

## Community Hot Topics

### Most Active Issues (by comment count)

1. **[#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601)** — [OPEN] "Add subscription-native OAuth support for Ollama Cloud, z.ai, Kimi, MiniMax" (7 comments, 👍1)
   - **Analysis**: This long-standing feature request (since April 2026) continues to gather community interest. Users want OAuth-based authentication for four major Chinese/cloud AI providers, reflecting demand for ZeroClaw to support emerging AI platforms beyond OpenAI. The "blocked" status suggests dependency on upstream provider APIs or internal authentication refactoring.

2. **[#7184](https://github.com/zeroclaw-labs/zeroclaw/issues/7184)** — [OPEN] "RFC: Move translated .ftl and .po files into a git submodule" (4 comments)
   - **Analysis**: A structural proposal to extract translation files into a git submodule to reduce repository noise from translation churn. Indicates i18n maintenance is becoming a scaling concern for the project.

3. **[#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715)** — [OPEN] "Delete unneeded branches from main repository" (4 comments)
   - **Analysis**: A housekeeping request—user reports 200+ stale branches polluting the repository. This signals a need for automated branch cleanup policies as the contributor base grows.

4. **[#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141)** — [OPEN] "OIDC Authentication Provider support" (4 comments)
   - **Analysis**: A tracking issue for v0.9.0—pluggable OIDC auth. This is a major architecture change tied to enterprise deployments, suggesting ZeroClaw is targeting organizational/SSO environments.

5. **[#6915](https://github.com/zeroclaw-labs/zeroclaw/issues/6915)** — [CLOSED] "Skill-scoped tool activation" (3 comments)
   - **Analysis**: Recently closed—enables skills to temporarily activate tools not in the agent's `allowed_tools` set. This was a high-risk security feature that required careful implementation, now resolved.

### Most Active PRs (by activity)

- **[#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229)** — "MCP, Skills, Plugins & Providers dashboard tabs" (XL-sized, high risk, heavy discussion)
- **[#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335)** — "Sandbox isolation: resource limits, SSRF guard, env scoping" (foundational plugin security)
- **[#7340](https://github.com/zeroclaw-labs/zeroclaw/pull/7340)** — "Extract duplicate domain/URL validation" (quality-of-life refactor)

---

## Bugs & Stability

### Critical/High Severity Bugs Fixed Today

| Issue | Title | Severity | Fix PR |
|---|---|---|---|
| [#7252](https://github.com/zeroclaw-labs/zeroclaw/issues/7252) | session/kill can rehydrate killed ACP sessions from durable history | **S0** - Data loss / security risk | Fixed, no separate PR |
| [#6978](https://github.com/zeroclaw-labs/zeroclaw/issues/6978) | Redact nested secrets in object-array property displays | **S0** - Data loss / security risk | Fixed, closed |
| [#7332](https://github.com/zeroclaw-labs/zeroclaw/issues/7332) | Telegram partial streaming accepts zero draft update interval, floods edits | **S2** - Degraded | [#7334](https://github.com/zeroclaw-labs/zeroclaw/pull/7334) ✅ |
| [#7133](https://github.com/zeroclaw-labs/zeroclaw/issues/7133) | Path-policy false-positive on ~ tokens in quoted/heredoc command data | **S2** - Degraded | [#7281](https://github.com/zeroclaw-labs/zeroclaw/pull/7281) ✅ |
| [#7151](https://github.com/zeroclaw-labs/zeroclaw/issues/7151) | Observability tool_call telemetry leaks onto chat WebSocket, permanent "unknown" tool cards | **S2** - Degraded | Fixed, closed |
| [#7197](https://github.com/zeroclaw-labs/zeroclaw/issues/7197) | Web toolbar slow + spawns visible cmd windows on Windows | **S2** - Degraded | Fixed, closed |
| [#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126) | Web UI "Clear all" only wipes frontend, not backend session history | **S2** - Degraded | Fixed, closed |
| [#7156](https://github.com/zeroclaw-labs/zeroclaw/issues/7156) | Reload banner shows persistent `gateway.paired_tokens` drift that never clears | **S3** - Minor | Fixed, closed |

### Open Bugs with High Risk

| Issue | Title | Risk | Status |
|---|---|---|---|
| [#6906](https://github.com/zeroclaw-labs/zeroclaw/issues/6906) | Improve Nix flake (expose package/module, not toolchain) | Medium | Blocked |
| [#6875](https://github.com/zeroclaw-labs/zeroclaw/issues/6875) | Tool call parser doesn't handle `<tool_calls>` plural tags (Llama 4 Scout) | Medium | ✅ Closed today |
| [#6906](https://github.com/zeroclaw-labs/zeroclaw/issues/6906) | Nix flake needs improvement | Medium | Blocked |

**Trend**: The team is effectively addressing S0 and S1 bugs with rapid closure. Today saw 8 bug fixes closed, including two S0 security/data-loss issues. The Telegram draft update interval bug ([#7332](https://github.com/zeroclaw-labs/zeroclaw/issues/7332)) was opened and fixed on the same day, demonstrating quick response.

---

## Feature Requests & Roadmap Signals

### User-Requested Features (Not Yet Accepted/Handled)

| Issue | Feature | Risk | Signal |
|---|---|---|---|
| [#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601) | OAuth support for Ollama Cloud, z.ai, Kimi, MiniMax | High | +1 reactions, 7 comments—strong demand |
| [#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) | Pre-hook skip gates for cron jobs/SOP triggers | High | 2 comments, blocked—user wants conditional execution |
| [#5775](https://github.com/zeroclaw-labs/zeroclaw/issues/5775) | Per-skill security permissions (scoped scripts/commands) | High | 2 comments, blocked—security granularity gap |

### Active Trackers / Release Predictions

| Tracker | Milestone | Status | Likely Content |
|---|---|---|---|
| [#7112](https://github.com/zeroclaw-labs/zeroclaw/issues/7112) | **v0.8.0** | Active | Config/tool-call-parser stable, schema cleanup, breaking changes |
| [#6970](https://github.com/zeroclaw-labs/zeroclaw/issues/6970) | **v0.8.1** | Active | Channels, providers, tools integration queue |
| [#7314](https://github.com/zeroclaw-labs/zeroclaw/issues/7314) | **v0.8.2** | Active | WASM plugin program (FND-001, WIT, host functions) |
| [#7320](https://github.com/zeroclaw-labs/zeroclaw/issues/7320) | **v0.8.3** | Active | MCP dashboard + web/plugin management surfaces |
| [#7141](https://github.com/zeroclaw-labs/zeroclaw/issues/7141) | **v0.9.0** | Planned | OIDC auth provider support |

**Prediction**: v0.8.0 likely ships within 1–2 weeks given today's bug closure cadence. The WASM plugin push (v0.8.2) may overlap with v0.8.0 if the plugin infrastructure PRs merge quickly.

---

## User Feedback Summary

### Pain Points Addressed This Week
- **Telegram bot sending raw scratchpad/tool transcripts** ([#7068](https://github.com/zeroclaw-labs/zeroclaw/issues/7068)) — fixed, was a P1 regression with Codex backend
- **Web UI "Clear all" didn't actually clear backend state** ([#7126](https://github.com/zeroclaw-labs/zeroclaw/issues/7126)) — confusing UX, now fixed
- **Windows users experiencing visible cmd popups** ([#7197](https://github.com/zeroclaw-labs/zeroclaw/issues/7197)) — degraded experience, fixed
- **Policy false-positives blocking legitimate commands** ([#7133](https://github.com/zeroclaw-labs/zeroclaw/issues/7133)) — heredoc bodies incorrectly scanned as path arguments, fixed

### Ongoing Pain Points (Still Open)
- **200+ stale branches** ([#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715)) — repository organization friction for contributors
- **Nix flake users can't install zeroclaw package** ([#6906](https://github.com/zeroclaw-labs/zeroclaw/issues/6906)) — blocked, Nix users limited to toolchain only
- **Global script/command permissions** ([#5775](https://github.com/zeroclaw-labs/zeroclaw/issues/5775)) — security-conscious users want per-skill sandboxing
- **Cron job pre-hook gates** ([#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607)) — users want conditional job execution

### Sentiment Indicators
- **Positive**: Plugin ecosystem expansion (6 new self-hosted plugins) shows commitment to "own your stack" philosophy
- **Negative**: OAuth support for non-OpenAI providers has been open since April with no resolution—may frustrate users of Asian/alternative cloud providers
- **Mixed**: WASM pursuit is ambitious; users appreciate direction but may fear complexity (per RFC [#7338](https://github.com/zeroclaw-labs/zeroclaw/issues/7338) on HookRunner bridge)

---

## Backlog Watch

### Issues Needing Maintainer Attention

| Issue | Age | Status | Why It Matters |
|---|---|---|---|
| [#5601](https://github.com/zeroclaw-labs/zeroclaw/issues/5601) | 58 days | Blocked, accepted | OAuth for 4 providers—most-reacted open issue, community waiting |
| [#5607](https://github.com/zeroclaw-labs/zeroclaw/issues/5607) | 58 days | Blocked, accepted | Cron pre-hook gates—core scheduling feature request |
| [#5775](https://github.com/zeroclaw-labs/zeroclaw/issues/5775) | 53 days | Blocked, accepted | Per-skill security—critical for multi-skill deployments |
| [#5908](https://github.com/zeroclaw-labs/zeroclaw/issues/5908) | 49 days | Blocked, accepted | CI/CD Debian container builds—infrastructure gap |
| [#6715](https://github.com/zeroclaw-labs/zeroclaw/issues/6715) | 22 days | Blocked, accepted | Stale branch cleanup—contributor experience |
| [#6906](https://github.com/zeroclaw-labs/zeroclaw/issues/6906) | 13 days | Blocked, accepted | Nix flake package—Nix user blocker |

### PRs Needing Review/Attention

| PR | Age | Base | Risk |
|---|---|---|---|
| [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) | 3 days | master | High (XL-sized, introduces 4 dashboard tabs) |
| [#7245](https://github.com/zeroclaw-labs/zeroclaw/pull/7245) | 2 days | master | High (fixes plugin-bundled skill loading) |
| [#7256](https://github.com/zeroclaw-labs/zeroclaw/pull/7256) | 2 days | master | Medium (Lark/Feishu hardening, 2 prod bug fixes) |
| [#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335) | 1 day | master | Medium (plugin sandbox isolation—foundational) |
| [#7333](https://github.com/zeroclaw-labs/zeroclaw/pull/7333) | 1 day | master | Medium (remote plugin registry—adoption bottleneck fix) |

**Callout**: The [#7229](https://github.com/zeroclaw-labs/zeroclaw/pull/7229) PR (MCP + 4 dashboard tabs) has been open for 3 days and is a dependency for [#7235](https://github.com/zeroclaw-labs/zeroclaw/pull/7235). Unblocking this will unblock the stacked plugin lifecycle endpoints PR. The WASM plugin PRs ([#7335](https://github.com/zeroclaw-labs/zeroclaw/pull/7335), [#7336](https://github.com/zeroclaw-labs/zeroclaw/pull/7336), [#7337](https://github.com/zeroclaw-labs/zeroclaw/pull/7337)) are stacked on each other and represent the core v0.8.2 milestone—early review would help maintain velocity.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/Augustrains/agents-radar).*